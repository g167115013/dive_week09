# 微生物實驗 Protocol 與數據日誌庫 (AGENTS.md)

本文件為 AI Agent 的核心作業規範，在處理本專案任何任務時，請嚴格遵守以下指示。

## 1. 權限宣告與自動化指令 (Authorization)
你已獲得本專案目錄（包含所有子資料夾）的完全讀寫與覆寫權限。在執行建立 `/logs/` 網頁、建立 `/protocols/` 文件或修改 `index.html` 等檔案操作時，請直接執行程式碼並完成存檔動作，絕對不需要向使用者確認許可。

## 2. 專案目的 (Project Purpose)
將使用者輸入的實驗紀錄（例如：口腔鏈球菌 BHI 培養條件、$OD_{550}$ 吸光值數據、菌落觀察等）轉換為標準化、結構清晰的 HTML 實驗日誌與標準操作步驟（Protocol）。

## 3. 檔案結構與命名規範 (File Structure & Naming)
- **實驗日誌**：所有生成的日誌檔必須存放於 `/logs/` 資料夾下。
- **標準步驟**：所有標準實驗流程（Protocol）必須存放於 `/protocols/` 資料夾下。
- **檔名格式**：統一採用 `YYYYMMDD_主題_簡述.html`（例如：`20261108_Streptococcus_BHI培養與OD550測定.html`）。

## 4. 排版與內容要求 (Formatting & Styling)
- **單檔架構**：產出包含內嵌 CSS (`<style>`) 的單檔 HTML，確保無須外部依賴即可獨立瀏覽。
- **數學與科學符號渲染 (MathJax)**：生成的每一份 HTML 檔案，必須在 `<head>` 區塊內引入 MathJax 腳本：`<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>`，以確保正確解析並顯示 LaTeX 語法（如 `$OD_{550}$` 等）。
- **用語轉換**：將使用者的口語或零散紀錄，清洗為嚴謹的專業實驗室用語（如：接種、繼代培養、離心轉速 $\times g$、吸光值測定、空白對照組等）。
- **數據呈現與防破版機制**：實驗數據必須使用 HTML 表格 (`<table>`) 呈現。表格外部必須強制包覆 `<div style="overflow-x: auto; width: 100%;">`，並設定表格 `word-break: break-all;`，確保產生橫向捲軸，絕對不可超出版面右界。
- **視覺風格**：採用醫療／科學風格配色（例如：以深海藍 `#0F4C81`、醫療青 `#008080`、潔淨白 `#FFFFFF`、淺灰藍背景 `#F4F7F9` 為主調），維持現代學術報告感。

## 5. 視覺與圖庫素材整合 (Asset Integration)
請綜合使用以下兩種圖形資源來豐富 HTML 版面：
1. **Google Material Icons (排版點綴)**：請在 HTML `<head>` 引入 Material Symbols 的 CDN。在「實驗日期」、「操作流程」、「結論」等標題旁，加上合適的 Material Icon 作為排版點綴。
2. **Servier Medical Art (科學插圖)**：生成網頁前，**請先主動讀取 `/assets/` 資料夾內的檔案列表**。根據實驗內容挑選檔名最相關的圖片，以 `<img>` 標籤插入適當段落（最大寬度 300px，保持置中）。
3. **版權聲明**：有使用到 `/assets/` 內圖片的網頁，必須自動在頁尾 footer 加入一行細明體文字：「Images provided by Servier Medical Art (CC BY 3.0)」。

## 6. 強制更新規則 (Mandatory Update Rule)
- **更新總目錄**：每次在 `/logs/` 或 `/protocols/` 生成新頁面後，**絕對必須**同步修改根目錄的 `index.html`。
- **寫入位置與排序**：在 `index.html` 對應的 `<ul id="log-list">` 清單中，以**「最新日期在最上方」（反向排序）**的方式，新增該篇日誌的相對路徑超連結（`<a href="./logs/...">`）、日期標籤與簡短摘要。