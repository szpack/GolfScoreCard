# 高尔夫赛事角标助手 · Golf Overlay

**Masters-style broadcast golf shot info overlay generator**  
作者 / Contact: szpack@qq.com

---

## 快速使用 / Quick Start

1. 打开 `golf-scorecard.html`（Chrome / Safari / iPhone）
2. 在下方控制栏依次设置：**球员姓名 → 洞号 → Par → 距离 → 击球类型**
3. 点击 **"下一杆 NEXT SHOT"** 推进击球计数
4. 本洞完成后选择成绩（Birdie / Par / Bogey …）
5. 点击 **"导出 EXPORT PNG"** → 下载透明/黑底 PNG

---

## 导出说明 / Export

| 选项 | 说明 |
|------|------|
| **4K (2160p)** | 默认，3840×2160，适合 4K 剪辑 |
| **1080p** | 1920×1080，标准高清 |
| **透明** | 透明底，直接叠加到剪辑软件 |
| **黑底** | 纯黑背景，便于色键/测试 |

导出文件名格式：`hole01_shot02_approach_birdie_2160p.png`

---

## 整场记录 / Round Scoring

- 每次点击"新洞"时，当前洞的杆数会自动写入计分卡
- 底部显示计分卡条（18洞全程）+ 总杆数 / 杆差
- 在 **设置 ⚙** 中可开启"本场总分"在角标上显示（Gross 或 To Par）

---

## 参考背景图 / Reference Background

- 点击预览区空白处上传照片作为背景参考
- 背景仅用于预览对齐，**不会出现在导出 PNG 中**
- 上传后在**设置 ⚙ → 参考背景图**中调节透明度 / 隐藏 / 清除

---

## 数据存储 / Data Persistence

- 所有状态通过 **localStorage** 自动保存（版本号：v3）
- 刷新页面后自动恢复
- 清空本轮：设置 ⚙ → **清空本轮 Reset Round**（有确认弹窗）

---

## 键盘快捷键 / Keyboard Shortcuts

| 键 | 功能 |
|----|------|
| `N` / `→` | 下一杆 Next Shot |
| `U` / `Ctrl+Z` | 撤销 Undo Shot |
| `H` | 新洞 New Hole |
| `B` | Birdie |
| `P` | Par |
| `G` | Bogey |
| `Enter` | 导出 Export PNG |

---

## iPhone 横屏使用建议

1. Safari 打开 HTML 文件（可从 iCloud Drive / Files）
2. 手机横置
3. 使用大按钮控制，双指可缩放参考背景图
4. 拖动角标卡片可自由定位（松手后自动保存）

---

## 技术架构 / Architecture

```
Single-file HTML (no build step, no external dependencies)
├── CSS Design Tokens (TH object mirrors :root vars)
├── STATE MODULE     — S{} object + undo stacks
├── RENDERER MODULE  — drawOverlay(ctx, {scale,ox,oy,forExport})
│   └── Preview + Export share IDENTICAL render call
├── EXPORT MODULE    — doExport() → Canvas → PNG download
├── UI SYNC          — syncUI() called after every commit()
└── INTERACTION      — drag/pan/pinch on Canvas
```

Schema version field in localStorage prevents data corruption on upgrade.
