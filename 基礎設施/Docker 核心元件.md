# Docker 核心元件

輸入 `docker run` 時，**客戶端**把請求交給**守護程序**，後者協調執行環境。理解這條路徑，比背元件清單更容易排查問題。

1. **Docker 客戶端（Docker Client，`docker`）**：接收指令，透過 Docker API 與守護程序溝通。
2. **Docker 守護程序（Docker Daemon，`dockerd`）**：管理映像、容器、網路與儲存，並呼叫容器執行環境。
3. **映像（Docker Image）與容器（Container）**：映像定義檔案與設定；容器是以映像建立的實例，詳見 [[Docker 映像與容器]]。
4. **登錄服務（Registry）**：儲存與分發映像。例如從 Docker Hub 或私有 registry 取得映像。
5. **網路（Networking）**：決定容器彼此、容器與外部如何通訊。橋接、主機及覆蓋網路各有用途。
6. **儲存（Storage）**：可寫層保存容器暫時變更；資料卷保存需要跨容器生命週期保留的資料。

**Docker Compose** 用設定檔管理多容器應用，例如一起啟動網站與資料庫。它是輔助工具，不是啟動單一容器時必備的核心元件。

若網站容器重建後上傳圖片消失，先檢查圖片是否只放在容器可寫層，而非資料卷或外部儲存。

## 相關筆記

- [[Docker 映像與容器]]
- [[Kubernetes Service 與 port-forward]]
