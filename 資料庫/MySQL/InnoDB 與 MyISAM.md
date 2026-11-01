# InnoDB 與 MyISAM

MySQL 的儲存引擎決定資料表如何處理交易、鎖與故障。一般業務資料優先使用預設的 **InnoDB**。

| 面向 | InnoDB | MyISAM |
| --- | --- | --- |
| 交易與回滾 | 支援 | 不支援 |
| 外鍵 | 支援 | 不支援 |
| 鎖 | 支援記錄鎖；範圍依查詢而異 | 主要使用表級鎖 |
| 當機恢復 | 有交易日誌與崩潰恢復 | 沒有相同的交易式保證 |

例如轉帳扣款成功後，程式在入帳前失敗。InnoDB 可用同一交易回滾；MyISAM 不能靠 `ROLLBACK` 還原已寫入資料。MyISAM 不一定比較快或省資源，應按實際讀寫負載測試。

交易與複製不能取代獨立備份；即使使用 InnoDB，也要定期驗證能否還原。

參考：[MySQL 8.4：InnoDB](https://dev.mysql.com/doc/refman/8.4/en/innodb-introduction.html)、[MyISAM](https://dev.mysql.com/doc/refman/8.4/en/myisam-storage-engine.html)。

## 相關筆記

- [[轉帳與 ACID]]
