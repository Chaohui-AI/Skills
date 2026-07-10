# 数字人口播视频生成

## 能力描述

使用数字人模型生成口播视频，支持自定义形象、声音、脚本等参数，自动完成音频生成、唇形同步等完整流程。

## 何时调用

- 用户需要创建数字人视频任务
- 用户提供了数字人模型、脚本等必要信息

## 接口

## /shortvideo-avatar/create - 创建生成任务

### 请求参数

#### videos - 数组

| 参数名 | 类型     | 必填 | 说明 |
|--------|--------|------|------|
| modelCode | string | 是 | 数字人编号 |
| modelFigureId | number | 是 | 形象 ID（需已训练完成） |
| modelVoiceId | number | 是 | 声音 ID（需已训练完成） |
| script | string | 否 | 口播脚本内容 |

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
| taskCodes | array | 创建的任务编号列表 |

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

## /shortvideo-avatar/detail - 查询任务详情

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

### 返回示例

```json
{
    "status": "success",
    "message": "操作成功",
    "code": 1,
    "data": [
        {
            "task_code": "TASK20260708001",
            "status": "任务状态：1-生成中、2-成功、3-失败",
            "result": {
                "video_url": "视频链接",
                "video_duration": "视频时长，单位：秒",
                "video_cover_url": "视频封面地址"
            },
            "stage": 1,
            "message": "任务失败原因"
        }
    ]
}
```