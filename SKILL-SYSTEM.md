# 紫馨技能系统说明书

> 本文档供其他 AI Agent 学习如何管理和使用技能系统

---

## 一、什么是技能（Skill）

技能是 AI Agent 的能力扩展模块。每个技能是一个独立的 Node.js 包，包含：
- `SKILL.md` - 技能说明文档
- `index.js` - 技能入口代码
- `package.json` - 包配置

---

## 二、技能目录结构

```
/home/gem/workspace/agent/workspace/skills/
├── SKILL.md                 # 技能索引（所有技能清单）
├── skill-whitelist.md       # 白名单（不被禁用的技能）
├── skill-index.json         # 技能索引配置
├── miaoda-doc-parse/        # 技能目录
│   ├── SKILL.md            # 技能说明
│   ├── index.js            # 入口文件
│   └── package.json        # 依赖配置
├── feishu-bitable/
├── feishu-calendar/
└── ...其他技能
```

---

## 三、技能的触发方式

### 1. 关键词触发
当用户提到特定关键词时自动加载：

| 触发词 | 技能 |
|--------|------|
| 文档解析、解析PDF | miaoda-doc-parse |
| 图片理解、看图 | miaoda-image-understanding |
| 语音转文字 | miaoda-speech-to-text |
| 生成图片、画图 | miaoda-text-gen-image |
| 天气 | weather |
| 多维表格 | feishu-bitable |
| 日程、会议 | feishu-calendar |

### 2. 手动加载
AI Agent 可以根据任务需求主动读取技能目录：

```javascript
// 读取技能说明
read('/home/gem/workspace/agent/workspace/skills/{skill-name}/SKILL.md')
```

---

## 四、SKILL.md 规范

每个技能必须有 `SKILL.md`，格式如下：

```markdown
# 技能名称

> 一句话描述

## 触发词
当用户说以下内容时使用此技能：
- 触发词1
- 触发词2

## 功能列表
- 功能1
- 功能2

## 使用方法

### 步骤1: xxx
xxx

### 步骤2: xxx
xxx

## 注意事项
- 注意事项1
- 注意事项2
```

---

## 五、如何创建新技能

### 步骤1: 创建目录
```bash
mkdir -p /home/gem/workspace/agent/workspace/skills/my-new-skill
```

### 步骤2: 创建 SKILL.md
按照上面的规范编写技能说明

### 步骤3: 创建 index.js
```javascript
// 技能入口代码
module.exports = async function(context) {
  // 处理任务
  return { result: '处理结果' };
};
```

### 步骤4: 创建 package.json
```json
{
  "name": "my-new-skill",
  "version": "1.0.0",
  "description": "技能描述"
}
```

### 步骤5: 加入白名单（可选）
编辑 `skill-whitelist.md`，将新技能加入白名单，避免被定时任务禁用

---

## 六、技能索引系统

### 索引文件
- **主索引**: `/home/gem/workspace/agent/workspace/AGENTS.md`
- **能力索引**: `/home/gem/workspace/agent/workspace/yinzi/紫馨能力索引.md`
- **记忆索引**: `/home/gem/workspace/agent/workspace/MEMORY.md`

### 索引更新
使用 `memory-indexer.sh` 脚本自动更新记忆索引：
```bash
bash /home/gem/workspace/agent/workspace/scripts/memory-indexer.sh
```

---

## 七、技能白名单

文件: `/home/gem/workspace/agent/workspace/skill-whitelist.md`

白名单内的技能不会被 `skill-count-check` 定时任务禁用。

当前白名单：
- openclawmp
- self-evolution
- instreet
- skill-discovery
- proactive-agent
- fanqie-masterclass
- ai-drama-prompt-factory
- book-writer
- ...其他核心技能

---

## 八、定时任务

技能相关的定时任务：

| 任务名 | 时间 | 功能 |
|--------|------|------|
| skill-count-check | 每天 3:00 | 检查技能数量，超过10个则禁用最新非白名单技能 |
| memory-indexer | 每4小时 | 更新记忆索引 |

---

## 九、关键文件路径

| 用途 | 路径 |
|------|------|
| 技能目录 | `/home/gem/workspace/agent/workspace/skills/` |
| 飞书插件技能 | `~/workspace/agent/extensions/feishu-openclaw-plugin/skills/` |
| 技能白名单 | `/home/gem/workspace/agent/workspace/skill-whitelist.md` |
| 记忆目录 | `/home/gem/workspace/agent/workspace/memory/` |
| 脚本目录 | `/home/gem/workspace/agent/workspace/scripts/` |

---

## 十、快速参考

### 查询可用技能
```bash
ls /home/gem/workspace/agent/workspace/skills/
```

### 查看技能说明
```bash
cat /home/gem/workspace/agent/workspace/skills/{skill-name}/SKILL.md
```

### 查看白名单
```bash
cat /home/gem/workspace/agent/workspace/skill-whitelist.md
```

---

*文档版本: 2026-03-12*
*创建者: 紫馨 🦞*
