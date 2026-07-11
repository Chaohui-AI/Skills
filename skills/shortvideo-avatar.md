# 数字人视频生成

## 能力描述

使用指定数字人的形象和声音生成视频。

## 何时调用

- 用户需要生成数字人视频
- 用户提供了数字人形象和声音、脚本等必要信息

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
    "videos": [
        {
            "modelCode": "AVATAR001",
            "modelFigureId": 1,
            "modelVoiceId": 1,           
            "script": "大家好，今天给大家介绍一款非常好用的产品。它采用了最新的技术，能够帮助您提升工作效率。"
        }
    ]
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
    "taskCode": "TASK20260708001"
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