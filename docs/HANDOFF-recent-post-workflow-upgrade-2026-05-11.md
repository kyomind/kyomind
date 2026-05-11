# recent-post workflow 升級 Handoff

整理日期：2026-05-11

## 任務摘要

本次任務是檢查 `kyomind/kyomind` 的 GitHub Actions workflow [recent-post.yml](/Users/kyo/Code/kyomind/.github/workflows/recent-post.yml)，只做「不改變行為」的版本更新。

目標不是重寫 workflow，也不是調整文章更新邏輯，而是找出明顯過舊、可安全升級的 action 版本。

## 已完成結果

已完成的更新只有一項：

- `actions/checkout@v3` 升級為 `actions/checkout@v6`

目前 workflow 關鍵片段如下：

```yaml
steps:
  - name: Checkout
    uses: actions/checkout@v6
  - name: Pull in my posts
    uses: gautamkrishnar/blog-post-workflow@v1
```

## 為什麼只改這一行

這次檢查過後，`actions/checkout@v3` 是唯一明顯過舊、而且可以保守升級的元件。

原因：

- WeaMind repo 目前全面使用 `actions/checkout@v6`
- `actions/checkout` 官方目前最新 major 也是 `v6`
- 從 `v3` 升到 `v6` 不需要改 workflow 結構，屬於低風險升級

## 為什麼沒有動 blog-post-workflow

`gautamkrishnar/blog-post-workflow@v1` 這次沒有更動，這是刻意決定，不是漏掉。

原因：

- 該 action 官方 README 範例目前仍使用 `@v1`
- 它的穩定發行線仍屬於 1.x 系列
- 直接把 `@v1` 改成特定 patch、commit SHA、或其他標記，已經不只是「更新舊版元件」，而是在改版本管理策略
- 本次任務要求是不改變行為，因此保守做法是先不動它

換句話說，這次的判斷不是「第三方 action 不重要」，而是「它目前沒有明顯過舊到需要立即升級，而且改法會牽涉版本固定策略」

## 參考依據

這次判斷主要參考兩個來源：

1. 本 repo 當前 workflow 狀態
2. WeaMind repo 現行 workflow 的 action 版本

對照結果：

- WeaMind 已使用 `actions/checkout@v6`
- WeaMind 對第三方 action 普遍採取更審慎的版本策略，有些用 major tag，有些直接 pin commit SHA

因此這次在 `kyomind` repo 只升 GitHub 官方 action、先不碰第三方 action，是合理且一致的做法。

## 驗證結果

這次更新後已確認：

- [recent-post.yml](/Users/kyo/Code/kyomind/.github/workflows/recent-post.yml) YAML 診斷正常
- diff 只包含一行變更：`actions/checkout@v3 -> @v6`
- workflow 的 trigger、permissions、feed URL、template、date format 都未改動

## 後續若要再進一步優化

如果未來要再碰這份 workflow，建議分清楚兩種任務：

1. 版本更新
2. 版本固定策略調整

這次只做第 1 類。

若未來要做第 2 類，才適合重新評估是否要把第三方 action 改成：

- 指定更明確的 minor / patch tag
- 或直接 pin commit SHA

但那應該被視為另一個明確任務，而不是這次的延伸手順。

## 待處理事項

目前沒有待處理 issue。

## MEMOS

- `recent-post.yml` 目前已完成保守升級，唯一改動是 `actions/checkout@v6`
- `gautamkrishnar/blog-post-workflow@v1` 是刻意保留，不是遺漏
- 下次若新 AI 接手，不要再直接假設 `@v1` 就是舊；先確認官方 README 與 release 策略
- 這個 repo 的目標是保持 profile automation 穩定，因此 workflow 修改應偏保守
