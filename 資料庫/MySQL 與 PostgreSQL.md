# MySQL 與 PostgreSQL

MySQL 與 PostgreSQL 都是關聯式資料庫，支援交易、索引與外鍵。選型先看查詢與維運需求，不要只問「哪個比較快」。

| 面向 | MySQL | PostgreSQL |
| --- | --- | --- |
| 授權 | Community Edition 使用 GPL；另有商業支援 | 使用 PostgreSQL License |
| 外鍵 | InnoDB 支援並檢查；MyISAM 不支援 | 支援外鍵約束 |
| 資料型別 | 支援 JSON；功能受版本與儲存引擎影響 | 支援 JSONB、陣列與自訂型別等 |
| 擴充 | 複製、分區與外部方案 | 複製、分區與擴充套件；水平分片另需設計 |

例如訂單系統要保證「訂單必須對應有效顧客」。MySQL 的 InnoDB 與 PostgreSQL 都能使用外鍵；不能說 MySQL 不檢查外鍵。若需要特定 JSON 查詢或擴充套件，先驗證各版本是否支援。

性能取決於索引、SQL、資料規模、設定與硬體。用相同資料模型和負載測試，並評估授權、團隊經驗與維運成本，沒有普遍勝者。

參考：[MySQL 8.4：InnoDB 外鍵](https://dev.mysql.com/doc/refman/8.4/en/create-table-foreign-keys.html)、[PostgreSQL 授權](https://www.postgresql.org/about/licence/)。
