# Claude Code PM 工作流模板

讓 Claude Code(建議搭配 Opus 等級模型)扮演 **PM**,把實作派給 `rd` subagent、
驗收交給每次全新的 `tester` subagent 的協作模板。適合開新專案時直接複製使用。

## 內容物

| 檔案 | 用途 |
|---|---|
| `CLAUDE.md` | PM 的角色設定與七階段流程(每次對話自動載入) |
| `.claude/agents/rd.md` | RD 工程師 subagent(可讀寫、跑指令;附 project 級 agent memory) |
| `.claude/agents/tester.md` | Tester subagent(只讀 + 跑測試,每次全新) |
| `docs/SYSTEM_STATUS.md` | 唯一事實來源:系統現況 + 功能清單(subagent 看不到對話,全靠它) |
| `docs/plans/` | 每次需求的規劃書,檔名 `NNN_YYYY-MM-DD_大綱.md` |

## 開新專案的用法

1. 把整份模板複製到新專案根目錄(`CLAUDE.md`、`.claude/`、`docs/`)。
2. 開專案第一天,先請 PM 帶你把 `docs/SYSTEM_STATUS.md` 的「系統概觀」填好
   (技術棧、如何啟動、測試指令)。
3. 之後每個需求都走流程:討論 → 規劃書 → 你說「確認」→ 派工 RD → Tester 驗收 → commit。

## 注意事項

- `rd.md` 用了 `memory: project`(agent 持久記憶),需要 Claude Code v2.1.33 以上;
  它會在 `.claude/agent-memory/rd/` 累積 codebase 知識,可一併進版控。不想要就把
  frontmatter 那行刪掉。
- Tester 的「不能改檔案」是靠 tools 白名單(沒有 Write/Edit)+ prompt 約束。
  但它有 Bash 才能跑測試,而 Bash 理論上能寫檔——若要硬性防護,可在
  `.claude/settings.json` 加 permission deny 規則或 PreToolUse hook。
