---
name: Chaohui-AI-Skills
description: 超会 AI 助手 — 创建数字人口播视频任务
version: 0.0.1
metadata:
    author: 超会 AI
    homepage: https://www.chaohui.ai
---

# 超会 AI Skills 

通过 Agent API Gateway 调用超会 AI 接口，提供数字人相关能力。

## 支持的能力

| 能力 | 说明             | 用户示例 | 详细说明                   |
|------|----------------|----------|------------------------|
| 数字人管理 | 查询数字人，以及数字人的形象和声音 | "列出所有数字人" | `model-avatar.md` |
| 数字人视频生成 | 创建数字人视频生成任务，以及查询任务详情 | "用 XX 数字人使用 XX 脚本生成一条视频" | `shortvideo-avatar.md` |

## 接口调用规范

### 统一入口

```
POST https://skill.chaohui.ai/agent/gateway
```

### 鉴权方式

- **Header**: `Authorization: Bearer $CHAOHUI_API_KEY`
- **CHAOHUI_API_KEY**：从环境变量获取，格式 `sk-xxxxxxxx`
- 若未设置，提示用户：`export CHAOHUI_API_KEY=<你的 API Key>`
- API Key 绑定用户身份，所有需要用户身份的接口会自动注入，无需手动传入

### 请求格式

- **Method**: POST
- **Content-Type**: application/json
- **Body**: JSON，`api_name` 指定接口，其余为接口业务参数，每次请求必须带 `skill_version`

```bash
curl -X POST "https://skill.chaohui.ai/agent/gateway" \
    -H "Authorization: Bearer $CHAOHUI_API_KEY" \
    -H "Content-Type: application/json" \
    -d '{"api_name": "/shortvideo-avatar/create", "videos": [], "skill_version": "0.0.1"}'
```

### 请求示例

#### ✅ 正确：业务参数平铺在 body 顶层

```json
{
    "api_name": "/shortvideo-avatar/create",
    "videos": [],
    "skill_version": "0.0.1"
}
```

#### ❌ 错误：不要把业务参数包在 params 内

```json
{
    "api_name": "/shortvideo-avatar/create",
    "params": {
        "videos": []
    },
    "skill_version": "1.0.0"
}
```

上面的错误写法会导致 `videos` 未被转发。

### 响应格式

- **JSON**
- **status**：状态，success 表示成功、error 表示失败
- **message**: 响应失败的原因
- **code**：错误码，1 表示正常，非 1 表示具体错误
- **data**：响应成功的数据

#### ✅ 成功响应：

```json
{
    "status": "success",
    "message": "操作成功",
    "code": 1,
    "data": {}
}
```

#### ❌ 失败响应：

```json
{
    "status": "error",
    "message": "错误描述",
    "code": -1
}
```

### 通用规则

1. **版本上报**：每次请求 body 必须包含 `"skill_version": "0.0.1"`（取本文件顶部 `version` 字段的值），用于服务端检查版本更新。如果回包中出现 `upgrade_info` 字段，必须立即暂停当前操作，按照 `upgrade_info.message` 中的指引完成升级，升级完成后再重新执行用户请求，**不得忽略该字段**。

2. **参数平铺**：业务参数必须和 `api_name`、`skill_version` 放在同一层；不要包在 `params`、`data`、`body` 等对象里。只有接口文档明确声明的数组/对象字段才允许作为业务字段传入。

3. **能力文档预检**：调用任何接口前，必须先根据「支持的能力」表阅读对应说明文件（如数字人视频生成先阅读 `shortvideo-avatar.md`），确认接口参数、字段含义和工作流。**禁止仅凭字段名或经验猜测含义**。

4. **字段解释优先级**：解释接口回包时，以对应说明文件中的字段说明为准；如果回包字段名和直觉含义冲突，必须服从说明文件，**不得直接翻译字段名**。