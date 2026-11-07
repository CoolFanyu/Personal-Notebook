# PersonalNotebook  #docs #linefilter

A Sublime-style notebook built around Line Filter: grep-like, instant filtering of every line in the current document.

## Quick start

- Open server.log. The filter bar is prefilled with ERROR|WARN (regex mode).
- Press Enter / Shift+Enter to jump to the next / previous result line.
- Switch Include to Exclude to drop the matching lines instead.
- Turn on Fold unmatched to collapse non-matching lines in the editor. Line numbers stay unchanged.
- Use the results panel to copy lines, export them to a new tab, or delete lines in place (Ctrl+Z undoes it).
- Try regex: ^\s+at finds stack traces, latency=\d{3,}ms finds slow requests.
- The EN / 中文 button in the status bar (or Alt+L) switches the interface language.

## Open and save files

- Open (Ctrl+O, or drag files onto the window) loads text files into new tabs.
- Save (Ctrl+S) writes back to the original file when the browser allows it.
- Save As (Ctrl+Shift+S) writes the note to a new file and links the tab to it.
- A dot on a tab means the note has changes that are not saved to a file yet.
- To save straight into the original file, open the standalone HTML file in Chrome or Edge.
- Inside the claude.ai viewer the browser cannot grant write access, so Save offers a downloaded copy instead.
- Notes are also kept in this browser automatically, so closing the page does not lose them.

## Filter options

    Include       keep matching lines
    Exclude       drop matching lines
    .*            regular expression mode
    Aa            match case
    Context       show N lines around each match (Include mode)
    Fold          collapse non-matching lines in the editor

## Shortcuts

    Ctrl+P            go to note
    Ctrl+Shift+P      command palette
    Ctrl+O            open file
    Ctrl+S            save
    Ctrl+Shift+S      save as
    Ctrl+Shift+F      open the filter bar (Alt+F and Ctrl+F also work)
    Alt+R / Alt+C     regex / match case
    Alt+L             switch language
    Ctrl+D            select next occurrence
    Ctrl+Shift+Up/Down  move line up / down
    Ctrl+Shift+D      duplicate line
    Ctrl+/            toggle comment
    Ctrl+G            go to line (or type :120 in the palette)
    Ctrl+B            toggle sidebar
    Alt+N / Alt+W     new / close tab

## Architecture

    UI shell        sidebar, tabs, filter bar, results panel, status bar
    Editor core     CodeMirror 5 + sublime keymap, one Doc per tab
    Filter engine   filterLines(texts, filter) -> kinds[] (pure function)
    Decorations     line highlight, fold, minimap, results list
    File I/O        File System Access API, file input, downloads capability
    Storage         localStorage (notes and preferences)
