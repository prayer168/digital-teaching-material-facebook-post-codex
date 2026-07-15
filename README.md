# Digital Teaching Material & Facebook Post Codex Skill

一套整合「數位互動教材開發、品質驗證、GitHub Pages 發布、社群預覽縮圖，以及中英 Facebook 貼文」的 Codex Skill。

這個 Skill 適合把既有的 HTML、CSS、JavaScript、SVG 或 Vite 教材骨架完成為可在課堂使用的互動教材，也能單獨產生繁體中文與英文 Facebook 貼文。當使用者說「收工」時，Skill 會啟動完整的教材驗證、版本提交、GitHub Pages 發布、社群縮圖與貼文交付流程。

## 主要功能

- 建立、補完或修改跨學科數位互動教材。
- 查核名稱、公式、數值、年代、地圖、字形、文化符號與時效資訊。
- 製作精準 SVG、CSS、JavaScript 動畫、互動模擬與闖關題。
- 建立「學習目標 → 視覺／互動 → 學生任務 → 成功證據」對應關係。
- 驗證桌機、平板、手機、鍵盤、觸控與降低動畫模式。
- 建立並驗證 `1200 × 630` 社群分享縮圖。
- 加入 Open Graph 與 Twitter Card metadata。
- 產生同一區塊內的繁體中文與英文 Facebook 貼文。
- 在「收工」流程中完成 GitHub Pages 發布與公開版驗證。

## 安裝

### Windows PowerShell

```powershell
git clone https://github.com/prayer168/digital-teaching-material-facebook-post-codex.git `
  "$env:USERPROFILE\.codex\skills\digital-teaching-material-facebook-post-codex"
```

若已經安裝，請更新現有版本：

```powershell
Set-Location "$env:USERPROFILE\.codex\skills\digital-teaching-material-facebook-post-codex"
git pull
```

安裝或更新後，重新開啟 Codex，讓技能清單重新載入。

## 使用方式

可直接指定 Skill：

```text
使用 $digital-teaching-material-facebook-post-codex，幫我完成這份互動教材。
```

也可以提出符合用途的自然語言請求，Codex 會依技能描述判斷是否載入。

### 1. 製作或修改教材

```text
幫我把這份光的折射教材補完整，加入互動模擬、闖關題，並檢查手機版。
```

Skill 會盤點教材、建立學習目標、查核內容、完成視覺與互動，最後執行正式建置和跨裝置驗證。除非使用者要求發布或說「收工」，不會擅自部署。

### 2. 只產生 Facebook 貼文

```text
幫這個教材寫一篇 Facebook 貼文：https://example.com/lesson/
```

預設輸出同一個易複製區塊，依序包含：

```text
【繁體中文】
[繁體中文貼文]

【English】
[English post]
```

如果網址屬於目前專案或使用者控制的網站，Skill 也會檢查或更新社群縮圖與 Open Graph metadata；不會修改第三方網站。

### 3. 教材加社群分享

```text
完成教材後，幫我製作 Facebook 分享縮圖和中英貼文。
```

Skill 會先通過教材品質與部署閘門，再建立縮圖、metadata 和雙語貼文，避免分享尚未完成或內容錯誤的教材。

### 4. 「收工」完整流程

在教材任務中輸入：

```text
收工
```

「收工」不是一般道別，而是授權執行既定收尾工作：

1. 重跑正式 build、內容與互動驗證。
2. 檢查桌機、平板、手機、鍵盤與觸控操作。
3. 建立或更新 GitHub repository。
4. 啟用並驗證 GitHub Pages。
5. 建立 `1200 × 630` 社群縮圖及正式 metadata。
6. 產生並保存繁中、英文 Facebook 貼文。
7. 回報公開網址、commit、縮圖與驗證結果。

任何部署閘門失敗時，Skill 會停止發布並說明阻擋原因，不會強制覆寫遠端資料。

## 品質原則

- 每張圖、動畫與互動都必須對應明確學習目標。
- 重要概念至少交叉核對兩個可信來源。
- 優先改善教材原生 SVG、CSS 與 JavaScript，不用裝飾圖掩蓋問題。
- 保留既有且合理的教材架構，不強迫所有專案使用相同頁籤。
- 支援滑鼠、觸控、鍵盤與 `prefers-reduced-motion`。
- 至少在 `1440 × 1000`、`768 × 1024`、`390 × 844` 三種 viewport 實際驗證。
- 正式建置、視覺檢查、互動測試與公開部署未通過前，不宣告完成。

## Repository 與 GitHub Pages 規則

- 一份教材使用一個可辨識主題的專用 repository。
- repository 名稱優先採教材資料夾名稱或簡潔英文名稱，使用 kebab-case。
- 除非使用者明確要求，不把新教材放進無關舊 repo 的子資料夾。
- 發布前確認 GitHub CLI 已登入，並先檢查遠端是否有未知內容。
- 不使用 force push 覆寫無法安全整合的遠端內容。

完整「收工」發布需要另外安裝 `github-pages-html-deploy` Skill。

## Skill 結構

```text
digital-teaching-material-facebook-post-codex/
├── SKILL.md
├── README.md
├── agents/
│   └── openai.yaml
├── references/
│   ├── facebook-post-workflow.md
│   ├── finish-publish-share.md
│   ├── post-kickoff-polish.md
│   └── precision-visual-interaction-qa.md
└── scripts/
    └── publish-skill.ps1
```

各檔案用途：

- `SKILL.md`：觸發條件、任務路由與核心工作流程。
- `agents/openai.yaml`：Codex UI 顯示名稱、說明與預設提示。
- `facebook-post-workflow.md`：中英貼文、語氣、格式與連結預覽規則。
- `finish-publish-share.md`：「收工」發布與社群分享流程。
- `post-kickoff-polish.md`：七頁籤教材骨架的補完與檢查規則。
- `precision-visual-interaction-qa.md`：跨學科精準度、視覺、動畫、互動、無障礙與瀏覽器驗證標準。
- `publish-skill.ps1`：驗證、提交並發布 Skill 本身的輔助腳本。

## 驗證 Skill

修改 Skill 後，使用 Skill Creator 的驗證工具：

```powershell
$env:PYTHONUTF8 = "1"
python "$env:USERPROFILE\.codex\skills\.system\skill-creator\scripts\quick_validate.py" `
  "$env:USERPROFILE\.codex\skills\digital-teaching-material-facebook-post-codex"
```

## 發布 Skill 更新

確認本次變更範圍並準備推送至 GitHub 後，可執行：

```powershell
Set-Location "$env:USERPROFILE\.codex\skills\digital-teaching-material-facebook-post-codex"
powershell -ExecutionPolicy Bypass -File .\scripts\publish-skill.ps1 `
  -Message "Describe the skill update"
```

Repository：<https://github.com/prayer168/digital-teaching-material-facebook-post-codex>
