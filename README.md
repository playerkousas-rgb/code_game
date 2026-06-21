# 🎮 CODE_GAME — Cipher Lab Interactive Prototype

一個**單檔 HTML 互動遊戲原型**,展示 Cipher Lab plugin 的核心玩法。

- **5 種遊戲模式** + 完整生涯紀錄系統
- **程式化音效**(Web Audio API,無需任何音檔)
- **本地儲存**(localStorage,跨 session 保留進度)
- **成就系統**(8 個可解鎖成就)
- **零依賴 / 零 build step** — 任何瀏覽器直接打開就跑

## 🎮 5 種模式

| 模式 | 玩法 | 適合 |
|------|------|------|
| ⚡ **反射訓練** (Reflex Drill) | 隨機單字母,加權偏重弱點,Combo 節奏 | 個人訓練 |
| 📜 **故事斬件** (Story Chunk) | 領袖輸入文字,你一段一段解碼,揭曉整篇 | 主題活動 |
| 🏃 **橫向捲動跑酷** (Side-Scroll Run) | Mario 式無盡跑酷,答對跳、答錯扣命 | 遊戲化訓練 |
| ⚔️ **一對一對戰** (Head-to-Head Duel) | 兩部手機對戰,HP 條、取消窗口、傷害特效 | 友誼賽 |
| 👹 **魔王討伐** (Boss Raid) | 小隊 8 人合作,3 階段密碼魔王 | 童軍小隊活動 |

## 🔓 包含的密碼(全部英文輸出)

| Cipher | 在 Combo Chain | 視覺 |
|--------|----------------|------|
| **Morse Code** | ✅ core | · 跟 — 不同顏色 |
| **Semaphore** | ✅ core | 每字母畫小人旗號 |
| **Pigpen** | ✅ core | 每字母畫幾何形狀 |
| **Grid** | ✅ core (預設 key = `SCOUT`) | 金邊 cell,輸出 SC/SO/OU/UT 等童軍座標 |
| **Phone T9** | ✅ high-priority | 數字 + 按幾下 |
| **Braille** | ✅ low-priority | 6 點 grid |

(NATO / Caesar / Atbash / Reverse 留給 Study,不進 Combo Chain)

## 🎨 視覺風格

- **角色**:Cyber Scout(cyberpunk 風格,頭盔 visor + 發光 core + energy sword)
- **BOSS**:Cipher Warden(魔法師,連帽斗篷 + 繞行符號 + 旋轉魔法陣)
- **背景**:dark navy + cyan/violet gradient + animated grid + parallax
- **特效**:CSS keyframes + SVG particles,純 CSS

## 🔊 音效系統

**Web Audio API 程式化生成**,無需任何音檔:

| 事件 | 音效 |
|------|------|
| ✅ 答對 | 660→1320Hz 正弦掃頻(ding) |
| ❌ 答錯 | 180Hz 方波短促(buzz) |
| 🔥 Combo 上升 | 880→1760Hz 三角波(combo bump) |
| ⚡ Cancel clash | 白噪音爆裂(impact) |
| 🦘 跳躍 | 440→880Hz 三角波(spring) |
| 💥 受傷 | 220→110Hz 鋸齒波(thud) |
| ⚔️ 攻擊 | 短白噪音 + 600→300Hz(slash) |
| 👹 Boss 受傷 | 120→60Hz + 80Hz sub-bass(heavy) |
| 💀 KO | 440→80Hz 鋸齒(fall) |

可在 Landing 頁右下角切換開關。

## 💾 本地儲存(localStorage)

`cipherLab_save` 物件儲存:

```json
{
  "reflex":     { "bestScore": 0, "bestCombo": 0, "totalRuns": 0, "perfectRuns": 0 },
  "story":      { "bestScore": 0, "bestCombo": 0, "totalStories": 0 },
  "sidescroll": { "bestDistance": 0, "bestScore": 0, "bestCombo": 0, "totalRuns": 0 },
  "duel":       { "wins": 0, "losses": 0, "perfectWins": 0 },
  "boss":       { "raidsCompleted": 0, "raidsWon": 0, "mvpCount": 0 },
  "weakLetters": { "Morse": { "S": 5, "B": 3 } },
  "achievements": ["first_run", "combo_10"],
  "lastPlayed": 1234567890
}
```

按 Landing 頁「📊 生涯紀錄」查看全部。

## 🏆 成就列表

| ID | 名稱 | 解鎖條件 |
|----|------|---------|
| `first_run` | 首次遊玩 | 完成任何一局 |
| `combo_10` | Combo ×10 | 達到 10 連擊 |
| `combo_15` | Combo ×15 | 達到 15 連擊(最高倍率) |
| `perfect_run` | 完美一輪 | 0 失誤完成一局 |
| `first_win` | 首次勝利 | 在對戰中獲勝 |
| `boss_slayer` | 魔王擊殺者 | Boss Raid 通關 |
| `patrol_mvp` | 小隊 MVP | Boss Raid 中成為 MVP |
| `marathoner` | 馬拉松跑者 | Side-Scroll 跑超過 5000m |

## 🚀 部署到 Vercel

### 從這個 repo 部署

1. 去 https://vercel.com → 登入
2. "Add New Project"
3. 選 `playerkousas-rgb/CODE_GAME` repo
4. Framework Preset: **Other**
5. Root Directory: 留空
6. 按 Deploy

Vercel 會自動識別 `vercel.json` 並用 `@vercel/static` 部署。

### 自建 repo

```bash
git clone https://github.com/playerkousas-rgb/CODE_GAME.git
cd CODE_GAME
# 修改 .git/config 指向你的 repo
git remote set-url origin https://github.com/<你>/CODE_GAME.git
git push -u origin main
```

## 💻 本地開發

```bash
# 直接瀏覽器打開
open index.html

# 或用 http server
python3 -m http.server 8080
# → http://localhost:8080
```

## 📊 檔案大小

- `index.html`:**144 KB**(單檔包含 CSS + JS + SVG + 音效 + 儲存邏輯)
- `package.json`:444 B
- `vercel.json`:368 B
- 零外部依賴、零 build step

## 🔗 對應的設計文件

對應的完整 plugin 設計規格在 `/design-outline.md`(v0.7),962 行,涵蓋:
- 6 種反射密碼(reflex ciphers)
- 4 種遊戲模式
- Multi-device Leader / Scout / Audience 架構
- Troop Router marketplace 整合計畫

## 📝 License

MIT — 自由使用,可用於個人和商業項目。
所有角色美術都是 inline SVG 手繪,無需第三方授權。
