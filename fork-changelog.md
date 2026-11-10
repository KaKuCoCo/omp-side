# Fork 變更紀錄

本紀錄以 `wolfiesch/omp-side` 的 `main` 作為上游基準，按提交順序列出 `KaKuCoCo/omp-side` 的 `windows` 分支專屬變更，不含上游提交。日期為 Git 作者日期。

## 2026-11-08

- 支援在 Windows 的 Tern 啟動及管理 `/side`。
  - Windows 不使用 `/usr/bin/env` 包裝，改用 `PATHEXT` 尋找執行檔。
  - 依 PowerShell 引號規則辨識 pane 命令，因為 Tern 透過使用者的 PowerShell 啟動命令並回報其字串。
- 修正 `/side --pull` watcher。
  - 改為監看已準備好的子 session 檔案。
  - 原本掃描目錄時，該檔已存在，導致 watcher 不會回傳子 session 的回答。
- 更新 README。
  - 說明 Windows Tern 的需求、PowerShell 限制和 fork 的安裝方式，並反映 `--pull` watcher 的行為。
  - 提交未另述文件修改的原因。
- 清理啟動失敗的子 session 檔案。
  - 刪除預先建立的子 session 檔，避免留下沒有 spawn 紀錄的孤兒檔案。
  - 此清理條件由後續提交限縮。
- 移除 README 中 `Alt+S` 尚未驗證的限制。
  - 提交訊息記錄實體按鍵與 `tern send` 均可開啟 fork。
- 限縮子 session 檔案的清理條件。
  - 僅在尚未送出含子 session 檔名的啟動命令時刪除檔案，否則保留檔案並回報路徑。
  - 啟動或後續操作失敗時，fork 仍可能已執行，刪檔會遺失其記錄。
- 記錄 `--pull` watcher 的讀取起點。
  - 在準備子 session 後、啟動前記錄檔案大小。
  - 避免漏掉終端開啟或聚焦期間寫入的回答。
- 調整 Tern fork 的 scope。
  - 改用 CLI 實際路由的 daemon socket，優先取非空的 `TERN_DAEMON_SOCKET`，否則取 `TERN_PANE_SOCKET`。
  - 避免不同 daemon 的 scope 相同，進而錯認、聚焦或關閉其他 pane。
