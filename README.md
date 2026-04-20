# workout-tracker

A simple CLI-based workout planner and tracker for Hermès Agent.

---

## 功能 | Features

- 📋 运动计划管理（按周几分组，每组独立重量）
- 🏋️ 交互式训练记录（逐一动作记录完成次数）
- 📊 训练历史查看
- 🔄 跳过/重置/补录支持

---

## 文件结构 | File Structure

```
workout-tracker/
├── SKILL.md              # Skill definition for Hermès
├── README.md             # This file
├── scripts/
│   └── workout.py        # Core CLI script
└── data/
    ├── plan.example.json # 示例计划（示例文件）
    ├── plan.json         # 实际计划（已忽略）
    └── history.json      # 历史记录（已忽略）
```

---

## 使用方法 | Usage

所有操作通过 Hermès 自然语言指令完成，无需手动运行脚本。

### 计划管理 | Plan Management

```prompt
# 从文字描述生成计划（AI 自动转 JSON 保存）
运动计划 每天早上跑步30分钟，周三做俯卧撑和卷腹各3组

# 查看当前计划
运动计划查看

# 从本地 JSON 文件导入计划
运动计划导入 /path/to/plan.json
```

### 训练 | Training

```prompt
# 开始今日训练（交互式，逐一动作记录）
开始运动

# 跳过当前动作，进入下一个
跳过此动作
```

### 历史 | History

```prompt
# 查看近30天训练历史
运动历史

# 查看近 N 天历史
运动历史 90
```

### 数据管理 | Data Management

```prompt
# 重置今日训练记录（重新开始）
重置今日

# 重置指定日期的训练记录
重置日期 2026-04-18

# 手动添加历史记录（补录）
添加记录 2026-04-18 俯卧撑 10+10+10, 卷腹 15×3
```

---

## 数据格式 | Data Format

`plan.json` 示例（新版每组级格式）:

```json
{
  "name": "我的训练计划",
  "mode": "weekly",
  "schedule": {
    "monday": [
      {
        "name": "坐姿划船",
        "sets": [
          {"weight_kg": 25, "reps": 8},
          {"weight_kg": 25, "reps": 8},
          {"weight_kg": 25, "reps": 8, "dropset": true}
        ]
      }
    ]
  }
}
```

---

## 在 Hermès 中使用 | Using in Hermès

| 命令 | 说明 |
|------|------|
| `运动计划 <文字>` | 文字 → 自动生成 JSON 计划 |
| `运动计划 <json>` | 直接导入 JSON |
| `运动计划查看` | 查看当前计划 |
| `开始运动` | 开始今日训练 |
| `跳过此动作` | 跳过当前动作 |
| `运动历史 [天数]` | 查看历史记录 |
| `添加记录 <日期> <动作>` | 补录历史 |
| `重置今日` | 清除今天记录 |

---

## License

MIT
