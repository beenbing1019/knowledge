# B-tree 與 Hash 索引

索引像查書的目錄，讓資料庫不必每次翻完整本書。選哪種索引，要先看儲存引擎支援什麼。

| 查詢方式 | B-tree（InnoDB 常用） | Hash（例如 MEMORY 引擎） |
| --- | --- | --- |
| 等值比對 `=`、`<=>` | 支援 | 支援 |
| 範圍與排序 | 可利用索引順序 | 不支援 |
| 最左前綴 | 複合索引可依規則利用 | 不支援 |

例如訂單要找「日期介於兩天之間」並依時間排序，B-tree 可利用鍵的順序；Hash 適合等值查找，無法按鍵值順序掃描。但 **InnoDB 不能讓使用者把一般索引改建成 Hash**。其主鍵是聚簇 B-tree；Adaptive Hash Index 是內部最佳化，不是 `CREATE INDEX ... USING HASH`。

Hash 查找平均複雜度看似 O(1)，也不能據此斷定實際查詢一定快。資料分布、索引選擇性和記憶體都會影響結果。

參考：[MySQL 8.4：B-tree 與 Hash 索引](https://dev.mysql.com/doc/refman/8.4/en/index-btree-hash.html)、[MEMORY 儲存引擎](https://dev.mysql.com/doc/refman/8.4/en/memory-storage-engine.html)。

## 相關筆記

- [[索引設計]]
