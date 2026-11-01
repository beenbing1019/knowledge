# TCP 與 UDP

**術語**：DNS＝網域名稱系統（Domain Name System）；HTTP＝超文字傳輸協定（Hypertext Transfer Protocol）；IP＝網際網路協定（Internet Protocol）。

傳輸控制協定（TCP，Transmission Control Protocol）提供有序的位元組串流。使用者資料報協定（UDP，User Datagram Protocol）傳送獨立資料報，保留每則資料報的邊界。

| 比較 | TCP | UDP |
| --- | --- | --- |
| 建立連線 | 先握手 | 沒有 TCP 式握手 |
| 資料形態 | 位元組串流，應用自行切分訊息 | 一則一則的資料報 |
| 遺失與順序 | 重傳、有序交付、流量與壅塞控制 | 本身不保證送達、順序或不重複 |
| 用途 | 安全殼層協定（SSH，Secure Shell）、傳統 HTTP/1.1 與 HTTP/2 | DNS、即時影音、承載 QUIC／HTTP/3 |

例如傳檔案通常需要完整、有序的資料，TCP 省去應用自行處理重傳。即時通話可能寧可略過太晚抵達的聲音片段；UDP 讓應用自行決定要不要重傳。**UDP 不代表一定比較快**；QUIC 就在 UDP 之上自行處理可靠性與壅塞控制。

若資料報超過路徑最大傳輸單元（MTU，Maximum Transmission Unit），可能發生 IP 分片或傳送失敗。實務上應避免依賴大量分片。

## 三個常見選擇

1. 傳報表檔案：用 TCP 提供有序交付，再由應用驗證檔案與儲存結果；UDP 自行補足可靠性較費工。
2. 即時語音：可用 UDP 並容忍逾時封包；若需加密與壅塞控制，使用有相應機制的協定，而不是直接把 UDP 當成完整方案。
3. 網站走 HTTP/3：使用基於 UDP 的 QUIC；QUIC 自行實作可靠串流與壅塞控制，不能把 HTTP/3 描述成「不可靠的 HTTP」。

比較時先問需要資料報邊界、延遲限制、有序交付或可自行控制重傳；不要只按「速度快慢」選。

參考：[RFC 9293：TCP](https://www.rfc-editor.org/rfc/rfc9293)、[RFC 768：UDP](https://www.rfc-editor.org/rfc/rfc768)。

## 相關筆記

- [[TCP 連線建立與關閉]]
- [[UDP 資料報結構]]
- [[HTTP 與 HTTPS]]
