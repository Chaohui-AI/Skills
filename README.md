# Chaohui.AI Skills

为 AI Agent 提供超会 AI 能力的 Skill 集合，支持数字人视频等功能。

## 安装

```bash
npx skills add Chaohui-AI/Skills -g
```

## 配置

使用前需要设置超会 AI API Key：

1. 前往 [https://app.chaohui.ai/#/dashboard/skills](https://app.chaohui.ai/#/dashboard/skills) 获取你的 API Key
2. 设置环境变量：

```bash
export CHAOHUI_API_KEY=sk-xxxxxxxx
```

> API Key 绑定用户身份，所有需要用户身份的接口会自动注入，无需手动传入。

## 使用

安装后直接用自然语言与 Agent 对话即可：

```
"帮我生成一条数字人口播视频"
```

## 功能

| 能力        | 说明          | 详细文档                                                  |
|-----------|-------------|-------------------------------------------------------|
| 数字人口播视频生成 | 支持创建和查询生成任务 | [`shortvideo-avatar.md`](skills/shortvideo-avatar.md) |

## 版本

当前版本：**1.0.0**

每次请求自动携带版本号，服务端会通过 `upgrade_info` 字段通知升级。

## 许可证

[Apache-2.0](./LICENSE) — Copyright © 2026 Tencent