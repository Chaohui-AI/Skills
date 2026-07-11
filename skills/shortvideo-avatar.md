# 数字人视频生成

## 能力描述

使用指定数字人的形象和声音生成视频。

## 何时调用

| 用户意图 | 用户示例 | 调用接口 |
|----------|----------|----------|
| 生成视频 | "用张三生成一条视频，脚本是：大家好..."、"创建一条数字人视频" | `/shortvideo-avatar/create` |
| 查询进度 | "视频生成好了没？"、"查一下 TASK20260708001 的状态" | `/shortvideo-avatar/detail` |

### 工作流程

```
用户请求生成视频
    ↓
1. 调用 /model-avatar/list 查询数字人，获取 modelCode
    ↓
2. 调用 /model-avatar/data-list 查询形象和声音，获取 modelFigureId、modelVoiceId
    ↓
3. 调用 /shortvideo-avatar/create 创建任务，获取 taskCode
    ↓
4. 调用 /shortvideo-avatar/detail 查询进度，直到 status=2（成功）或 status=3（失败）
    ↓
5. 返回视频链接给用户
```

### 注意事项

- 生成视频前必须先从「数字人管理」能力获取 `modelCode`、`modelFigureId`、`modelVoiceId`
- 视频生成是异步任务，需要轮询 `/shortvideo-avatar/detail` 获取结果
- `status=1` 表示生成中，`status=2` 表示成功，`status=3` 表示失败

## 接口

### /shortvideo-avatar/create - 创建生成任务

### 请求参数

| 参数名 | 类型     | 必填 | 说明 |
|--------|--------|------|------|
| videos | array\<object\> | 是 | 视频列表 |
| videos[].modelCode | string | 是 | 数字人编号 |
| videos[].modelFigureId | number | 是 | 数字人形象编号 |
| videos[].modelVoiceId | number | 是 | 数字人声音编号 |
| videos[].script | string | 是 | 口播脚本内容 |

### 请求示例

```json
{
    "api_name": "/shortvideo-avatar/create",
    "videos": [
        {
            "modelCode": "AVATAR001",
            "modelFigureId": 1,
            "modelVoiceId": 1,           
            "script": "大家好，今天给大家介绍一款非常好用的产品。它采用了最新的技术，能够帮助您提升工作效率。"
        }
    ],
    "skill_version": "0.0.1"
}
```

### 返回结果

| 字段名 | 类型 | 说明 |
|--------|------|------|
| data | array\<object\> | 创建的任务列表 |
| data[].taskCode | string | 任务编号 |

### 返回示例

```json
{
    "status": "success",
    "message": "操作成功",
    "code": 1,
    "data": [
        {
            "task_code": "TASK20260708001"
        }
    ]
}
```

### /shortvideo-avatar/detail - 查询任务详情

### 请求参数

| 参数名           | 类型     | 必填 | 说明   |
|---------------|--------|------|------|
| taskCode      | string | 是 | 任务编号 |

### 请求示例

```json
{
    "api_name": "/shortvideo-avatar/detail",
    "taskCode": "TASK20260708001",
    "skill_version": "0.0.1"
}
```

### 返回结果

| 字段名 | 类型 | 说明 |
|--------|------|------|
| taskCode | string | 任务编号 |
| status | number | 生成状态：1-生成中、2-成功、3-失败 |
| result | object | 生成结果 |
| result.video_url | string | 视频链接 |
| result.video_duration | number | 视频市场，单位：秒 |
| result.video_cover_url | string | 视频封面链接 |
| stage | number | 生成阶段 |
| message | string | 生成失败原因 |

### 返回示例

```json
{
    "status": "success",
    "message": "操作成功",
    "code": 1,
    "data": [
        {
            "task_code": "TASK20260708001",
            "status": 2,
            "result": {
                "video_url": "",
                "video_duration": 12.30,
                "video_cover_url": ""
            },
            "stage": 1,
            "message": "失败原因"
        }
    ]
}
```