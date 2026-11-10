# Fork changelog

上游：[wolfiesch/omp-side](https://github.com/wolfiesch/omp-side)

## 2026-11-10

### Changed
- 呼叫 `tern` 時優先使用 pane 環境的 `TERN_EXE`，再找 `PATH`。
  - 原因：`TERN_EXE` 就是啟動該 pane 的 Tern，不必把 Tern 資料夾加進 `PATH`。
  - 上游：未回報。

## 2026-11-08

### Added
- 支援在 Windows 的 Tern 啟動與管理 `/side`。
  - 原因：原本僅支援 macOS 與 Linux。
  - 上游：未回報。

### Changed
- 子 session 檔只在啟動命令尚未送出時才刪除。
  - 原因：命令送出後 fork 可能已在執行，刪檔會遺失記錄。
- README 補上 Windows 需求與限制，移除 `Alt+S` 未驗證的說明。
  - 原因：Windows 支援需要說明；`Alt+S` 已實測可用。

### Fixed
- `/side --pull` 改為監看已準備好的子 session 檔。
  - 原因：掃描目錄時檔案已存在，watcher 收不到回答。
- `--pull` 從啟動前的檔案大小開始讀取。
  - 原因：終端開啟期間寫入的回答會被漏掉。
- Tern 的 scope 改用實際路由的 daemon socket。
  - 原因：不同 daemon 的 scope 相同，可能錯認或關閉其他 pane。

## 已移除
