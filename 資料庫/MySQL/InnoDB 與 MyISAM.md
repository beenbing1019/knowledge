# InnoDB 與 MyISAM

MySQL 的儲存引擎決定資料表如何處理交易、鎖與故障。一般業務資料優先使用預設的 **InnoDB**。

| 面向 | InnoDB | MyISAM |
| --- | --- | --- |
| 交易與回滾 | 支援 | 不支援 |
| 外鍵 | 支援 | 不支援 |
| 鎖 | 支援記錄鎖；範圍依查詢而異 | 主要使用表級鎖 |
| 當機恢復 | 有交易日誌與崩潰恢復 | 沒有相同的交易式保證 |

例如轉帳扣款成功後，程式在入帳前失敗。InnoDB 可用同一交易回滾；MyISAM 不能靠 `ROLLBACK` 還原已寫入資料。MyISAM 不一定比較快或省資源，應按實際讀寫負載測試。

InnoDB 的緩衝池（Buffer Pool）會快取讀過的資料頁與索引頁，減少重複磁碟讀取。若相同查詢偶爾快、偶爾慢，先量測資料是否已快取、儲存與查詢計畫；不能只憑快慢斷定是引擎差異。緩衝池會使用記憶體，調整大小仍要留給作業系統與其他程序足夠空間。

交易與複製不能取代獨立備份；即使使用 InnoDB，也要定期驗證能否還原。

參考：[MySQL 8.4：InnoDB](https://dev.mysql.com/doc/refman/8.4/en/innodb-introduction.html)、[MyISAM](https://dev.mysql.com/doc/refman/8.4/en/myisam-storage-engine.html)、[Buffer Pool](https://dev.mysql.com/doc/refman/8.4/en/innodb-buffer-pool.html)。

## 實務取捨

- 訂單與付款要一起提交：選 InnoDB；若用 MyISAM，應用無法靠 `ROLLBACK` 還原部分成功的寫入。
- 舊系統仍有 MyISAM 表：先確認是否依賴其特殊行為，再規劃轉換及備份；不是看到「表鎖」就立刻替換，需在相同負載測試。
- 報表讀取很慢：先檢查查詢計畫、索引及資料量；更換儲存引擎不是通用效能解法。

無論選哪種引擎，仍須獨立備份、權限控制與復原演練。

## 相關筆記

- [[轉帳與 ACID]]
