# 🏛️ 三省六部 · Edict

> 用 1300 年前的帝国制度，重新设计 AI 多 Agent 协作架构

## 项目概述

**三省六部 Edict** 是一个基于 OpenClaw 的多 Agent 协作系统，用中国古代的三省六部制度来设计 AI 多 Agent 协作架构。

**核心特点**：
- 12 个 AI Agent（11 个业务角色 + 1 个兼容角色）
- 制度性审核（门下省专职审核，可封驳）
- 实时看板（军机处 Kanban + 时间线）
- 任务干预（叫停 / 取消 / 恢复）
- 完整流转审计（奏折存档）

## 架构

```
你 (皇上) → 太子 (分拣) → 中书省 (规划) → 门下省 (审议) → 尚书省 (派发) → 六部 (执行) → 回奏
```

### Agent 角色

| 角色 | 功能 |
|------|------|
| 太子 | 消息分拣，闲聊/指令分离 |
| 中书省 | 任务规划与拆分 |
| 门下省 | 审核封驳（核心差异） |
| 尚书省 | 任务派发与调度 |
| 六部 | 并行执行（吏/户/礼/兵/刑/工） |
| 军机处 | 实时看板监控 |

## 安装条件

| 条件 | 需求 | 状态 |
|------|------|------|
| OpenClaw | 必需 | ✅ |
| Python | 3.9+ | ✅ 3.10+ |
| Node.js | 18+ | ✅ 22.x |
| Docker | 可选 | - |

## 快速安装

```bash
# 1. 克隆项目
git clone https://github.com/cft0808/edict.git
cd edict

# 2. 运行安装脚本
chmod +x install.sh && ./install.sh

# 3. 配置消息渠道（飞书）
openclaw channels add --type feishu --agent taizi

# 4. 启动服务
# 终端1：数据刷新
bash scripts/run_loop.sh

# 终端2：看板服务器
python3 dashboard/server.py

# 5. 打开看板
open http://127.0.0.1:7891
```

## 使用方法

### 发送任务

通过消息渠道发送任务（太子会自动识别）：

```
请帮我用 Python 写一个文本分类器：
1. 使用 scikit-learn
2. 支持多分类
3. 输出混淆矩阵
```

### 任务流转

```
收件 → 太子分拣 → 中书规划 → 门下审议 → 已派发 → 执行中 → 已完成
```

### 看板功能

- 📋 旨意看板 - 观察任务流转
- 🔭 省部调度 - 部门工作分布
- 📜 奏折阁 - 任务归档

## 与其他框架对比

| | CrewAI | MetaGPT | AutoGen | **三省六部** |
|---|:---:|:---:|:---:|:---:|
| 审核机制 | ❌ | ⚠️ | ⚠️ | **✅ 门下省专职审核** |
| 实时看板 | ❌ | ❌ | ❌ | **✅** |
| 任务干预 | ❌ | ❌ | ❌ | **✅ 叫停/取消/恢复** |
| 流转审计 | ⚠️ | ⚠️ | ❌ | **✅ 完整奏折** |

## 文档链接

- [README](https://github.com/cft0808/edict)
- [架构文档](https://github.com/cft0808/edict/blob/main/docs/task-dispatch-architecture.md)
- [快速上手](https://github.com/cft0808/edict/blob/main/docs/getting-started.md)

## 技术栈

- **后端**: Python (stdlib only, 无额外依赖)
- **前端**: React 18 + TypeScript + Vite + Zustand
- **框架**: OpenClaw
- **部署**: Docker 支持

## License

MIT

---

*本文档由 AI 整理并存入知识库*
