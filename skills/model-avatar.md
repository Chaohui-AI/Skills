# 数字人管理

## 能力描述

查询数字人，以及数字人的形象和声音信息。

## 何时调用

| 用户意图 | 用户示例 | 调用接口 |
|----------|----------|----------|
| 列出所有数字人 | "我有哪些数字人？"、"列出我的数字人" | `/model-avatar/list` |
| 搜索数字人 | "有没有叫「张三」的数字人？"、"帮我找「李四」" | `/model-avatar/list`（带 searchTitle） |
| 查询数字人形象 | "张三有哪些形象？"、"查看张三的形象列表" | `/model-avatar/data-list`（searchType=1） |
| 查询数字人声音 | "张三有哪些声音？"、"查看张三的声音列表" | `/model-avatar/data-list`（searchType=2） |

### 注意事项

- 生成视频前必须先调用此能力获取 `modelCode`、`modelFigureId`、`modelVoiceId`
- `searchType=1` 表示形象，`searchType=2` 表示声音

## 接口

### /model-avatar/list - 查询数字人列表

### 请求参数

| 参数名 | 类型     | 必填 | 说明 |
|--------|--------|------|------|
| searchTitle | string | 否 | 搜索关键词 |
| page | number | 否 | 分页页数：默认 1 |
| pageSize | number | 否 | 分页每页数量：默认 10 |

### 请求示例

```json
{
    "api_name": "/model-avatar/list",
    "searchTitle": "张三",
    "page": 1,
    "pageSize": 20,
    "skill_version": "0.0.1"
}
```

### 返回结果

| 字段名 | 类型 | 说明 |
|--------|------|------|
| current_page | number | 当前分页页数 |
| data | array\<object\> | 列表 |
| data[].model_code | number | 数字人编号 |
| data[].title | string | 数字人名称 |

### 返回示例

```json
{
    "status": "success",
    "message": "操作成功",
    "code": 1,
    "data": {
        "current_page": 1,
        "data": [
            {
                "task_code": "AVATAR20260708001",
                "title": ""
            }
        ]
    }
}
```

### /model-avatar/data-list - 查询指定数字人的形象或声音列表

### 请求参数

| 参数名           | 类型     | 必填 | 说明   |
|---------------|--------|------|------|
| modelCode | string | 是 | 数字人编号 |
| searchType | number | 是 | 搜索类型：1-形象，2-声音 |
| searchTitle | string | 否 | 搜索形象或声音名称 |
| page | number | 否 | 分页页数：默认 1 |
| pageSize | number | 否 | 分页每页数量：默认 10 |

### 请求示例

```json
{
    "api_name": "/model-avatar/data-list",
    "modelCode": "AVATAR20260708001",
    "searchType": 1,
    "searchTitle": "室内",
    "page": 1,
    "pageSize": 20,
    "skill_version": "0.0.1"
}
```

### 返回结果

| 字段名 | 类型 | 说明 |
|--------|------|------|
| current_page | number | 当前分页页数 |
| data | array\<object\> | 列表 |
| data[].data_id | number | 形象或声音编号 |
| data[].type | number | 类型：1-形象、2-声音 |
| data[].title | string | 形象或声音名称 |

### 返回示例

```json
{
    "status": "success",
    "message": "操作成功",
    "code": 1,
    "data": {
        "current_page": 1,
        "data": [
            {
                "data_id": 1,
                "type": 1,
                "title": "形象名称"
            }
        ]
    }
}
```