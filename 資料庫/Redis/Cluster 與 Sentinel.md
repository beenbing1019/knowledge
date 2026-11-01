# Redis Cluster 與 Sentinel

兩種方案都能處理主節點故障，但只有 **Redis Cluster** 會把資料分散到多個主節點。

| 方案 | 資料配置 | 故障切換 |
| --- | --- | --- |
| Cluster | 16,384 個雜湊槽（hash slot）分配到不同主節點 | 節點間協調，提升可用複本 |
| Sentinel | 單一主節點與複本，不分片 | Sentinel 監控並協調提升複本，提供新主節點位置 |

Cluster 以 CRC16 計算鍵所屬的槽；需要讓多個鍵位於同一槽時，可用雜湊標籤（hash tag），如 `{user42}:a`、`{user42}:b`。客戶端須支援重新導向與主節點變更。

例如快取容量超過單台機器時，考慮 Cluster 分片；如果容量夠，但希望主機故障後自動切換，可考慮 Sentinel。分片會增加跨槽操作成本。兩者都採非同步複製，主節點故障、網路分割或複本落後時，可能暫時不可用或遺失尚未同步資料。**Cluster 不靠 Sentinel 完成切換。**

參考：[Redis 官方：Cluster](https://redis.io/docs/latest/operate/oss_and_stack/management/scaling/)、[Sentinel](https://redis.io/docs/latest/operate/oss_and_stack/management/sentinel/)。

## 相關筆記

- [[主從複製]]
- [[06 分割槽與分片]]
