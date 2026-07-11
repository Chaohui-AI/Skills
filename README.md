# 超会 AI Skills

为 AI Agent 提供超会 AI 能力的 Skill 集合，支持数字人形象、声音管理，以及视频生成等功能。

## 安装

```bash
npx skills add Chaohui-AI/Skills -g
```

## 配置

使用前需要设置 API Key：

1. 前往 [https://app.chaohui.ai/](https://app.chaohui.ai/) （空间管理 - API）
2. 设置 API Key：

```bash
export CHAOHUI_API_KEY=sk-xxxxxxxx
```

> API Key 绑定用户身份，所有需要用户身份的接口会自动注入，无需手动传入。

## 使用

安装后直接用自然语言与 AI Agent 对话即可：

```
"帮我生成一条数字人口播视频"
"列出我所有的数字人"
"用张三生成一条介绍产品的视频"
```

### 工作流程

**生成数字人视频的完整流程**：

1. **查询数字人列表** → 获取 `modelCode`
2. **查询数字人形象和声音** → 获取 `modelFigureId` 和 `modelVoiceId`
3. **创建视频生成任务** → 获取 `taskCode`
4. **查询任务进度** → 获取生成结果

## 功能

| 能力        | 说明          | 详细文档                                                  |
|-----------|-------------|-------------------------------------------------------|
| 数字人管理 | 查询数字人，以及数字人的形象和声音 | [`model-avatar.md`](skills/model-avatar.md) |
| 数字人视频生成 | 创建数字人视频生成任务，以及查询任务详情 | [`shortvideo-avatar.md`](skills/shortvideo-avatar.md) |