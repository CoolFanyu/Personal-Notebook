# PersonalNotebook  #docs #linefilter

Sublime 風格的 Notebook，核心是 Line Filter：像 grep 一樣，即時過濾目前這份文件的每一行。
A Sublime-style notebook built around Line Filter: grep-like, instant filtering of every line in the current document.

## 快速開始 / Quick start

- 切到 server.log，Filter Bar 已預填 ERROR|WARN（Regex 模式）
  Open server.log. The filter bar is prefilled with ERROR|WARN (regex mode).
- Enter / Shift+Enter 在結果行之間跳轉
  Enter / Shift+Enter jumps to the next / previous result line.
- 把 Include 改成 Exclude，就會排除符合的行
  Switch Include to Exclude to drop the matching lines instead.
- 開啟「摺疊未匹配行」(Fold unmatched)，未匹配的行會在編輯器內摺疊，行號保持原樣
  Turn on Fold unmatched to collapse non-matching lines in the editor; line numbers stay unchanged.
- 結果面板可以複製、匯出成新分頁，或原地刪除行（可用 Ctrl+Z 還原）
  The results panel can copy lines, export them to a new tab, or delete lines in place (Ctrl+Z undoes it).
- 試試 Regex：^\s+at 找出所有堆疊追蹤，latency=\d{3,}ms 找出慢請求
  Try regex: ^\s+at finds stack traces, latency=\d{3,}ms finds slow requests.
- 狀態列的「EN / 中文」按鈕（或 Alt+L）可切換介面語言
  The EN / 中文 button in the status bar (or Alt+L) switches the interface language.

## Filter 選項 / Filter options

    Include       只保留匹配行 / keep matching lines
    Exclude       排除匹配行 / drop matching lines
    .*            Regex 模式 / regular expression mode
    Aa            大小寫相符 / match case
    Context       Include 模式下顯示前後 N 行 / show N lines around each match
    Fold          在編輯器內摺疊未匹配行 / collapse non-matching lines

## 快捷鍵 / Shortcuts

    Ctrl+P            跳到筆記 / go to note
    Ctrl+Shift+P      指令面板 / command palette
    Ctrl+Shift+F      開啟 Filter Bar（Alt+F、Ctrl+F 也可以）/ open the filter bar
    Alt+R / Alt+C     Regex / 大小寫 / regex / match case
    Alt+L             切換語言 / switch language （CN/ENG）
    Ctrl+D            選取下一個相同字串 / select next occurrence
    Ctrl+Shift+↑/↓    整行上移 / 下移 / move line up / down
    Ctrl+Shift+D      複製整行 / duplicate line
    Ctrl+/            切換註解 / toggle comment
    Ctrl+G            跳到行號（或在 Palette 輸入 :120）/ go to line
    Ctrl+B            收合側邊欄 / toggle sidebar
    Alt+N / Alt+W     新增 / 關閉分頁 / new / close tab

## 架構 / Architecture

    UI shell        側邊欄、分頁、Filter Bar、結果面板、狀態列 / sidebar, tabs, filter bar, results, status bar
    Editor core     CodeMirror 5 + sublime keymap，每個分頁一個 Doc / one Doc per tab
    Filter engine   filterLines(texts, filter) → kinds[]（純函式 / pure function）
    Decorations     行高亮、Fold、Minimap、Results / line highlight, fold, minimap, results
    Storage         localStorage（筆記與偏好 / notes and preferences）
