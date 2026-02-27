# Golf Overlay Generator v2

PGA Tour 风格高尔夫 vlog 字幕条生成器，零依赖纯 HTML，支持 iPhone Safari。

---

## 快速上手

1. 下载 `golf-scorecard.html`
2. 双击用 **Chrome / Safari** 打开（也可以上传到 Netlify Drop 或 GitHub Pages）
3. 调整参数 → 点 **EXPORT PNG** → 文件下载到本地

---

## 界面说明

```
┌─────────────────────────────────┐
│  Header: 画幅选择 + Safe Zone    │
├─────────────────────────────────┤
│  Preview (16:9/9:16/1:1)        │
│  └── 转播条叠加预览              │
├─────────────────────────────────┤
│  控制面板                        │
│  Hole · Par · Yards · Status    │
│  Shot Type · Hole Result        │
│  [NEXT SHOT] [NEW HOLE] [↩]     │
│  [EXPORT PNG] Transparent/Black │
└─────────────────────────────────┘
```

---

## 工作流（一洞 ≤ 3 步）

| 步骤 | 操作 |
|------|------|
| 1 | 设好洞号 / Par（默认记忆上一洞） |
| 2 | 点 **NEXT SHOT** 推进（自动推断击球类型） |
| 3 | 完洞后点结果（Birdie/Par/Bogey…）→ Export |

**键盘快捷键：**
- `→` / `n` — Next Shot
- `N` — New Hole
- `Ctrl/Cmd + Z` — Undo
- `Enter` — Export PNG

---

## 自动 Shot Type 逻辑

| Par | 杆数 | 自动识别 |
|-----|------|---------|
| 任意 | 第 1 杆 | TEE SHOT |
| Par 3 | 第 2 杆 | PUTTING |
| Par 4 | 第 2 杆 | APPROACH |
| Par 4 | 第 3 杆 | PUTTING |
| Par 5 | 第 2 杆 | APPROACH |
| Par 5 | 第 3 杆 | CHIP |
| Par 5 | 第 4 杆 | PUTTING |
| 任意 | 达到/超过 Par | PUTTING |

手动点击 Shot Type 按钮可覆盖自动，切到下一杆后恢复自动。

---

## 导出说明

| 选项 | 说明 |
|------|------|
| **Transparent PNG** | 无背景，直接拖入剪映/Premiere 叠加轨道 |
| **Black BG PNG**    | 黑底，用于检查对齐或 Luma Key |
| **1920×1080**       | 标准 1080p（约 800×176px 字幕条） |
| **3840×2160**       | 4K，适合高分辨率时间线 |

文件名格式：`hole01_shot02_approach_385yd_birdie.png`

---

## GitHub Pages 部署

```bash
# 1. 新建 GitHub 仓库
# 2. 上传 golf-scorecard.html → 重命名为 index.html
# 3. Settings → Pages → Source: main / root → Save
# 4. 访问 https://yourname.github.io/your-repo/
```

或使用 **Netlify Drop**（最快，无需注册）：
1. 打开 https://app.netlify.com/drop
2. 把 `golf-scorecard.html` 改名为 `index.html` 拖进去
3. 立刻获得公开链接，iPhone Safari 直接使用

---

## iPhone 使用说明

1. 将文件上传到 iCloud Drive
2. Safari 地址栏输入 Netlify/GitHub Pages 链接（推荐）
3. 点击「分享」→「添加到主屏幕」可当 App 使用
4. 导出的图片保存在 Safari「下载」文件夹（文件 App → 下载）

---

## 技术说明

- **零依赖**：纯 HTML + CSS + Vanilla JS
- **状态管理**：单一 `state` 对象 + `localStorage` 持久化
- **导出**：Canvas 2D API 手绘（不依赖 html2canvas）
- **Safe Zone**：仅编辑时可见，导出时不包含
