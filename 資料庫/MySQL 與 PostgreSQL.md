# MySQL 與 PostgreSQL

**術語**：SQL＝結構化查詢語言（Structured Query Language）。

MySQL 與 PostgreSQL 都是關聯式資料庫，支援交易、索引與外鍵。選型先看查詢與維運需求，不要只問「哪個比較快」。

| 面向 | MySQL | PostgreSQL |
| --- | --- | --- |
| 授權 | Community Edition 使用 GPL（GNU General Public License）；另有商業支援 | 使用 PostgreSQL License |
| 外鍵 | InnoDB 支援並檢查；MyISAM 不支援 | 支援外鍵約束 |
| 資料型別 | 支援 JSON（JavaScript Object Notation）；功能受版本與儲存引擎影響 | 支援 JSONB、陣列與自訂型別等 |
| 擴充 | 複製、分區與外部方案 | 複製、分區與擴充套件；水平分片另需設計 |

例如訂單系統要保證「訂單必須對應有效顧客」。MySQL 的 InnoDB 與 PostgreSQL 都能使用外鍵；不能說 MySQL 不檢查外鍵。若需要特定 JSON 查詢或擴充套件，先驗證各版本是否支援。

性能取決於索引、SQL、資料規模、設定與硬體。用相同資料模型和負載測試，並評估授權、團隊經驗與維運成本，沒有普遍勝者。

參考：[MySQL 8.4：InnoDB 外鍵](https://dev.mysql.com/doc/refman/8.4/en/create-table-foreign-keys.html)、[PostgreSQL 授權](https://www.postgresql.org/about/licence/)。

## 選型時做一個小型實驗

若要儲存商品與訂單，先確認兩套資料庫都能滿足交易、外鍵與索引需求；如果依賴 PostgreSQL 的 JSONB 索引或某種擴充套件，再針對該特性做實測。反過來，既有團隊已熟悉 MySQL 且功能足夠時，換引擎會增加遷移、備份與監控成本。

可行路徑包括沿用既有引擎並改善索引／查詢、在相同資料與負載下比較兩者，或在確有差異時才遷移。避免拿不同硬體或不同索引配置的基準測試下結論。

參考：[MySQL 8.4 Reference Manual](https://dev.mysql.com/doc/refman/8.4/en/)、[PostgreSQL Documentation](https://www.postgresql.org/docs/current/)。
