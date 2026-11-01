# Redis RDB 與 AOF

Redis 把資料放在記憶體。若需要重啟後恢復資料，就要依可接受的遺失範圍選持久化方式。

- **RDB（Redis Database）快照**：定期保存資料集。適合整批還原，但故障時可能失去上次快照之後的寫入；產生快照也會消耗資源。
- **AOF（Append-Only File，附加式檔案）**：記錄寫入命令供重播。通常能縮短遺失窗口，但不保證每筆都已落盤；範圍取決於 `appendfsync` 設定與故障類型。AOF 重寫可控制檔案成長。

例如購物車若每分鐘存 RDB，突然斷電可能失去最後一分鐘的更新。改用 AOF 也須檢查同步設定，而非假設完全不會遺失。兩者可依需求併用。

持久化檔案不等於獨立備份。仍要備份到其他位置，並定期測試能否還原。

參考：[Redis 官方：Persistence](https://redis.io/docs/latest/operate/oss_and_stack/management/persistence/)。

## 相關筆記

- [[主從複製]]
