# 数字人管理

## 能力描述

查询数字人，以及数字人的形象和声音信息。

## 何时调用

- 用户需要查询数字人时
- 用户需要查询指定数字人的形象或声音时

## 接口

### /model-avatar/list - 查询数字人列表

### 请求参数

| 参数名 | 类型     | 必填 | 说明 |
|--------|--------|------|------|
| searchModelCodeOrTitle | string | 否 | 搜索指定模型编号或名称 |
| page | number | 否 | 分页页数：默认 1 |
| pageSize | number | 否 | 分页每页数量：默认 20 |

### 请求示例

```json
{
    "searchModelCodeOrTitle": "张三",
    "page": 1,
    "pageSize": 20
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
| searchType | number | 是 | 搜索类型：0-全部，1-形象，2-声音 |
| searchTitle | string | 否 | 搜索形象或声音名称 |

### 请求示例

```json
{
    "modelCode": "AVATAR20260708001",
    "searchType": 0,
    "searchTitle": "室内"
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