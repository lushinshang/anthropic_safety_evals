# 分數之前，先問量的是什麼：Anthropic 談怎麼做出站得住的安全評測

Anthropic 在 2026 年 11 月 13 日發表〈Building strong safety evaluations〉（Engineering；Ruth Appel 等 8 位作者），借用心理學在再現危機後的改革（預先登記、更好的測量、更嚴謹的統計），整理出建 AI 安全評測的做法：先確定量的是什麼（自殺自傷情境下拒答率往往是錯的量尺；多輪評測報「適當回應率」，單輪評測把有害請求的無害回應率與良性請求的拒答率成對量）、用多輪模擬逼近真實、評分器要先對人工標註校準、報告要附信賴區間與完整設定。本導讀依原文的生命週期（安全第一、設計、執行、報告）逐段說明，並把文中數字逐一對照 Anthropic 系統卡：大多相符；60% 與 94% 比的是 API 與 claude.ai 兩種設定，不是加一句系統提示詞的前後；多輪 100 題／單輪 1,000 題下限與「網路搜尋評測即時監控」只見於原文。

> **製作聲明**：本導讀的分析與撰稿由 AI 模型完成，不是人類分析，也沒有經過人工逐句校稿。主控與撰稿：Claude Opus 5.5（Claude Code）；全文譯文：Claude Sonnet 初譯、Claude Opus 逐段審校、Claude Opus 5.5 合併；查證：Claude Opus 研究代理、agy（Gemini 4 Argon、Gemini 3.8 Flash），主控再開系統卡與官方頁核對；審稿：Claude Opus 事實、編輯兩路與終審，最後由 Claude Opus 依 editor-in-chief 潤稿準則潤稿並標示重點；插圖：以程式繪製的 SVG，沒有使用生成式影像，也沒有複製原文的圖。分工見導讀文末〈製作說明〉。

## 檔案

| 檔案 | 說明 |
|---|---|
| `index.html` | 導讀網頁（單檔，直接用瀏覽器開啟；圖片用相對路徑） |
| `translation-zh.html` | 原文全文繁中譯文（非官方，AI 模型翻譯與審校，未經人工校稿；原文圖片未收錄，只保留圖說譯文） |
| `anthropic_safety_evals.md` | 導讀 Markdown 原稿 |
| `images/` | 封面 `hero.svg`／`hero-mobile.svg`、`og-hero.jpg`；說明圖 `fig-multiturn-pipeline-zh(-mobile).svg`、`fig-grader-agreement-zh(-mobile).svg` |
| `qa/` | 版面驗收紀錄 `checks.md`、截圖（桌面 1440×900、手機 390×844）、`qa_result.json`、外部連結檢查 `links-round-2.txt` |
| `research/` | 需求、證據帳本、研究筆記、透鏡備忘、審稿紀錄、譯文分段與術語表、建置設定 |

## 原始素材

- 原文：〈Building strong safety evaluations〉，Anthropic，2026-11-13（頁面 2026-11-17 更新），https://www.anthropic.com/research/building-strong-safety-evaluations
- 逐字稿：不適用（來源是網頁文章）。本機抽出的全文純文字與原始 HTML 只存在本次工作的 scratchpad，未複製進本目錄。

## 重要來源

- 官方／第一手：Claude Fable 5.1 & Mythos 5.1 System Card（https://www.anthropic.com/claude-fable-5-1-mythos-5-1-system-card ）、Claude Opus 5.5 System Card（https://www.anthropic.com/claude-opus-5-5-system-card ）、Fable 5.1 系統提示詞（https://platform.claude.com/docs/en/release-notes/system-prompts/claude-fable-5-1 ）、Anthropic 資安事件分析與改進說明、OpenAI〈The Hugging Face incident and the road ahead〉、OpenAI〈Introducing SWE-bench Verified〉。
- 研究論文：Open Science Collaboration（Science 2015）、構念效度（arXiv 2511.04703）、LLM 評審偏誤（arXiv 2404.13076、2306.05685）等，完整清單見導讀〈來源清單〉。

## 狀態

僅本機完成（2026-11-21）。未發布、未初始化獨立 Git、未推送。資料截至 2026-11-21。本導讀為非官方整理，原文版權屬 Anthropic 與原作者。
