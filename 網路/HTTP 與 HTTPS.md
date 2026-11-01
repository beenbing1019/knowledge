# HTTP 與 HTTPS

超文字傳輸協定（HTTP，Hypertext Transfer Protocol）負責網頁請求與回應。HTTPS 是透過傳輸層安全性協定（TLS，Transport Layer Security）保護 HTTP 的傳輸。

| 比較 | HTTP | HTTPS |
| --- | --- | --- |
| 傳輸內容 | 預設明文，途中可能被讀取或修改 | TLS 保護機密性與完整性 |
| 常見預設埠 | 80 | 443 |
| 身分驗證 | 沒有 TLS 憑證驗證 | 用憑證鏈與網域名稱驗證伺服器 |

例如在咖啡店 Wi-Fi 輸入登入資料。若網站只用 HTTP，途中設備可能讀到或改寫內容；HTTPS 可保護這段傳輸。TLS 握手協商金鑰並驗證身分，應用資料通常用對稱加密，不是伺服器私鑰直接解密每筆資料。

HTTP/1.1 與 HTTP/2 的 HTTPS 常走傳輸控制協定（TCP，Transmission Control Protocol）。HTTP/3 走以使用者資料報協定（UDP，User Datagram Protocol）為基礎的 QUIC，並整合 TLS 1.3。

**界線**：HTTPS 不能修復惡意網站、受感染裝置或伺服器漏洞；IP 位址等連線中繼資料也不會全部隱藏。憑證驗證不能任意關閉。

## 相關筆記

- [[TCP 與 UDP]]
