# PM 模板與 OrderManagementSystem 規則差異

比較基準：PM 模板 main；OrderManagementSystem main 及待合併 PR #33。下表區分本次已改內容與待決策建議，建議不視為已授權。

## 本次已統一

- 兩邊以根目錄 AGENTS.md 集中管理功能範圍與一次性處理規則，CLAUDE.md 引用它。
- 主動提議不等於核准；永久行為、一次性資料處理與本次不做分開列明。
- RD 遇到新增產品行為或擴大範圍，由 PM 交由使用者決定，PM 不自行批准。
- 一次性處理優先 DB／專用腳本；寫腳本與執行資料修改分開授權；既有同範圍授權不重複詢問。
- PM 檢查未核准功能；PM 模板的 Reviewer 額外明定此情況必須退回。
- 保留 OrderManagementSystem 的明確 project／文件／資料項目 ID、Firestore updateTime 與稽核要求。

## 尚存差異與統一建議（尚未套用）

| 項目 | PM 模板 | OrderManagementSystem | 建議 |
|---|---|---|---|
| 審查角色 | RD → Reviewer → Tester | RD、Tester；PR 前完整 Security 審查 | 共用 Reviewer 做規格與品質審查；保留 OMS 專案資安關卡 |
| 事實與決策文件 | SYSTEM_STATUS、DECISIONS、BACKLOG 分工 | 主要依 SYSTEM_STATUS，待辦另放 docs/plans/BACKLOG.md | 共用三文件職責；先確認舊決策與待辦搬移方式 |
| 待辦／規劃分支 | 拍板後規劃與成果同分支、同 PR | 未開工規劃與待辦位於 claude/backlog-notes，開工後複製規劃 | 建議採模板的一需求一分支一 PR；OMS 分支遷移須另行確認 |
| 問答與立案 | 問問題不進開發流程；點子可暫記 | 任何需求先記 backlog 並推送專用分支 | 共用「問答不立案、確認要做才規劃」 |
| 規劃呈現 | 全文顯示 | 內容或連結均可 | 對使用者顯示完整範圍及取捨，再確認 |
| RD 自測／Tester 證據 | 明定 RD 全測通過，Tester 附指令與輸出 | RD 回報未同等強制，Tester 有整套測試但證據規定較少 | 共用有證據的驗收；純文件修改檢查內容與差異即可 |
| 退回次數 | 最多退回兩次，再由使用者決定 | 未設上限 | 採最多兩次，避免自行無限迭代 |
| 模型／記憶 | 角色檔未固定模型；RD 有 memory: project | RD、Tester 固定 model: opus；Security 預設；RD 無 memory | 按執行平台設定；若統一 Sol，先確認平台支援的模型名稱，不將 Codex 名稱直接塞進 Claude frontmatter |
| 上下文恢復 | 明定查未合併分支／PR與最新規劃 | 沒有同等完整章節 | 補恢復檢查，但已核准工作不用重複授權 |
| PR／完成定義 | 開 PR 等使用者 merge，合併後完成 | 有 merge 禁令，但階段 7 在 commit 後即称完成 | 統一「待合併」與「已完成」，由使用者合併 |
| PM 模板 README | 仍寫舊的 docs PR 先合 main 與七階段 | 不適用 | README 應對齊現有 CLAUDE.md 的八階段及單一 PR，避免入口文件互相矛盾 |

## 建議的統一方向

以 PM 模板的流程作為共用基底，保留 OMS 的 Firestore 安全與資料操作規範。先確認上表流程取捨，再處理待辦分支／文件遷移、角色與模型設定；本次不搬資料、不修改產品功能、不代為合併。
