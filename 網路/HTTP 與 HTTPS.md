# HTTP 與 HTTPS

超文字傳輸協定（HTTP，Hypertext Transfer Protocol）負責網頁請求與回應。HTTPS 是透過傳輸層安全性協定（TLS，Transport Layer Security）保護 HTTP 的傳輸。

| 比較 | HTTP | HTTPS |
| --- | --- | --- |
| 傳輸內容 | 預設明文，途中可能被讀取或修改 | TLS 保護機密性與完整性 |
| 常見預設埠 | 80 | 443 |
| 身分驗證 | 沒有 TLS 憑證驗證 | 用憑證鏈與網域名稱驗證伺服器 |

例如在咖啡店 Wi-Fi 輸入登入資料。若網站只用 HTTP，途中設備可能讀到或改寫內容；HTTPS 可保護這段傳輸。TLS 握手協商金鑰並驗證身分，應用資料通常用對稱加密，不是伺服器私鑰直接解密每筆資料。

HTTP/1.1 與 HTTP/2 的 HTTPS 常走傳輸控制協定（TCP，Transmission Control Protocol）。HTTP/3 走以使用者資料報協定（UDP，User Datagram Protocol）為基礎的 QUIC，並整合 TLS 1.3。

**界線**：HTTPS 不能修復惡意網站、受感染裝置或伺服器漏洞；網際網路協定（IP，Internet Protocol）位址等連線中繼資料也不會全部隱藏。憑證驗證不能任意關閉。

## 如何落實與排查？

- 登入與付款頁：全面使用 HTTPS，驗證憑證和主機名稱；以 HTTP 僅作重新導向會留下第一次連線被攔截的風險，可評估 HSTS（HTTP Strict Transport Security）。
- 憑證顯示錯誤：先查網域名稱、有效期限及憑證鏈；不要在正式環境關閉憑證驗證。
- 伺服器後端仍透過明文網路互傳機敏資料：瀏覽器到入口使用 HTTPS 不代表內部每段都受到保護，須按信任邊界設計 TLS。

參考：[MDN：HTTP Overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)、[MDN：HTTPS](https://developer.mozilla.org/en-US/docs/Glossary/HTTPS)。

## 相關筆記

- [[TCP 與 UDP]]
