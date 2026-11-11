# TrailGuard TW｜山徑守護者

以證據為基礎的臺灣高山行程規劃與風險決策支援代理人。它服務自組隊的行前決策：把天氣、步程、水源、許可、路況與高山症風險收成一份可追溯的「行前決策包」，而不是一段不能查來源的行程建議。

目前狀態：**設計完成，系統尚未實作，實驗尚未執行。** 指標都是目標，不是結果。

## 這個 repo 裡有什麼

| 路徑 | 內容 |
|---|---|
| [DESIGN.md](DESIGN.md) | 系統設計：問題、需求、架構、資料、演算法、預定介面、評估協定 |
| [docs/proposal-analysis](docs/proposal-analysis) | 提案對照與 A4 橫式資訊圖 |

`docs/proposal-analysis` 內的檔案：

- `期末專題提案作業規範.pdf`：作業規範
- `A2Z outline example.pdf`：A–Z 大綱
- `山徑守護提案解析.pdf`：提案與上述兩份文件的對照
- `TrailGuard_TW_資訊圖表_A4橫式.pdf`：八欄摘要圖
- `TrailGuard_TW_系統性解析資訊圖表_A4橫式.pdf`：高密度編號解析圖

## 設計要點

- **雙核**：LLM 負責理解、規劃與解釋；Python 負責計算與驗證。紅旗判定不交給 LLM。
- **證據鏈**：重要數字要有來源。沒有來源的數字不輸出（No source, no number）。
- **硬性紅旗**：颱風、封閉等條件直接 NO-GO，不能被其他優點抵銷。
- **決策包**：安全、平衡、進取三個候選行程，加上風險說明、撤退點與離線緊急卡。

八個模組的對位在 [DESIGN.md §3](DESIGN.md)：使用者情境、輸入、規劃、資料工具、知識、決策、輸出，以及跨層的 Safety & Evidence。

## 驗收目標

這些數字定義在 [DESIGN.md §2.4](DESIGN.md)。截至設計文件 v0.1，都還沒有量測。

| 指標 | 目標 |
|---|---|
| CSR，硬性限制滿足率 | ≥ 85% |
| EGR，數值可追溯比例 | ≥ 95% |
| False-Safe Rate，不安全卻給 GO | ≤ 2% |
| 步程 MAE | ≤ 20% |
| 專家接受度 | ≥ 4.0 |
| SUS | ≥ 75 |
| 完整規劃 P95 延遲 | ≤ 60 秒 |

評估設計是 90 個核心情境加 30 個壓力／對抗案例，共 120。協定與空白結果表在 [DESIGN.md §11](DESIGN.md)。

## 怎麼讀

1. 先看本頁，確認這是設計階段。
2. 讀 [DESIGN.md](DESIGN.md) 的 §1 問題、§3 架構、§8 演算法。
3. 若要對作業規範，打開 `docs/proposal-analysis` 的系統性解析圖。

[DESIGN.md §10](DESIGN.md) 寫了文件產生腳本與未來 API 的預定指令。那些程式與 `requirements.txt` **不在這個 repo**。`uvicorn app.main:app`、`python scripts/eval.py` 也還沒有。
