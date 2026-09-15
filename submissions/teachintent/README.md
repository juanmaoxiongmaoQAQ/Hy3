# TeachIntent · 基于 Hy3 的教学意图驱动语音规划系统

> 本目录是 **独立应用仓库** 的提交说明，完整代码、文档与演示案例位于：
> **https://github.com/juanmaoxiongmaoQAQ/TeachIntent**
>
> 对应 Issue：[#4 Build a vibe-coded application powered by Hy3](https://github.com/Tencent-Hunyuan/Hy3/issues/4)

## 项目简介

TeachIntent 是一个面向智能教育场景的 **教学意图驱动 AI 教学语音规划系统**。

系统输入教学内容、教学情境、学生状态和明确的教学意图，通过 Hy3 API 生成结构化 Speech Plan，显式规划 AI 教师：

- **说什么**：生成符合教学目标的教师话语；
- **怎么说**：生成必要的表达与韵律控制计划。

TeachIntent 将 Hy3 作为 **Pedagogical Speech Planner（教学语音规划器）**，把高层教学意图转化为结构化、可检查、可执行的教学计划。

## Hy3 在系统中的角色

整体流程：

教学内容 + 教学情境 + 学生状态 + 教学意图
→ Hy3 API
→ Structured Speech Plan
→ Verbal Plan（说什么）+ Delivery Plan（怎么说）
→ 独立计划质量检查 / 可选语音执行

Hy3 负责核心教学规划。

项目全程通过 API 调用 Hy3：

- 不训练 Hy3；
- 不微调 Hy3；
- 不进行 Hy3 本地推理部署；
- API Key 仅通过服务端环境变量配置，不写入源码。

## 主要功能

### 六类教学意图

系统支持：

- 了解学情（Elicitation）
- 提供支架（Scaffolding）
- 讲解知识（Explanation）
- 纠错反馈（Corrective Feedback）
- 支持性反馈（Supportive Feedback）
- 拓展提升（Extension）

### 结构化 Speech Plan

Hy3 输出统一的结构化教学语音计划：

- Verbal Plan：AI 教师具体应该说什么；
- Delivery Plan：需要采用什么表达方式。

计划通过 JSON Schema / Pydantic 进行结构校验，可由 Evaluator、Web 前端和下游语音模块直接使用。

### 独立计划质量检查

TeachIntent 提供六维质量检查：

- 教学意图一致性
- 内容忠实性
- 学生状态适配
- 教学策略充分性
- 表达控制必要性
- 表达与教学目标一致性

评价结果保留证据定位，便于人工复核。

质量检查针对 **Speech Plan**，不是最终音频质量。

### Web 可交互前端

项目提供 React Web 前端，包括：

- 首页
- 在线体验
- 示例库
- 教学意图对比

### 可选语音执行

Speech Plan 可以进一步交给语音渲染模块执行。

语音不是项目核心要求，TeachIntent 的主要贡献是 **教学意图 → 结构化教学语音计划** 的规划层。

## 端到端 Demo

仓库已经提供多个完整教学案例，包括：

1. **纠错反馈**
   - 回应学生关于速度与加速度的错误理解
   - Hy3 生成纠错型教师回应与表达计划
   - 系统完成六维质量检查

2. **提供支架**
   - 为仍需自主思考的学生提供有限提示
   - Hy3 根据 Scaffolding 意图生成支架式回应
   - 系统检查教学策略与表达方式

3. **支持性反馈**
   - 根据学生已有正确进展生成支持性回应
   - 当无需额外表达控制时，Delivery Plan 可以保持为空

公开仓库中已保存可直接浏览的案例、评价结果和示例音频，无需 API Key 即可查看。

## 对照 Issue #4 要求

| 要求 | TeachIntent |
|---|---|
| 全程通过 API 调用 Hy3，不训练 / 微调 / 本地推理 | ✅ |
| 至少 1 个可交互前端 | ✅ React Web |
| 至少 2 个端到端 Demo 流程 | ✅ 多个完整教学案例 |
| ≤ 2 min 视频或 GIF | ✅ [TeachIntent 产品演示](https://github.com/juanmaoxiongmaoQAQ/TeachIntent/blob/main/docs/demo.mp4) |
| 项目开源 | ✅ Public GitHub repository |
| README 写明 Hy3 在系统中的角色 | ✅ |
| 独立应用仓库 | ✅ https://github.com/juanmaoxiongmaoQAQ/TeachIntent |

## 开发协作说明

本项目在活动开发过程中使用 WorkBuddy 辅助代码实现、工程迭代与调试。

项目的问题定义、系统设计、教学意图体系、实验方案、结果核验、产品决策及最终交付由项目作者负责。

## 项目地址

https://github.com/juanmaoxiongmaoQAQ/TeachIntent

详细环境配置、Web 启动方式、API 配置和示例说明请参阅独立项目 README。

## 演示视频

≤ 2 分钟 Demo 视频：

[▶ TeachIntent 产品演示](https://github.com/juanmaoxiongmaoQAQ/TeachIntent/blob/main/docs/demo.mp4)

## 声明

本项目为腾讯犀牛鸟开源实战活动中的个人开源实践作品，并非腾讯官方发布，不代表腾讯公司立场。

本 PR 仅提交 TeachIntent 项目说明与独立仓库链接，**不修改 Hy3 仓库自身的模型或核心代码。**
