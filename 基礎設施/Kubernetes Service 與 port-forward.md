# Kubernetes Service 與 port-forward

要在本機暫時測試 Pod，可用 `port-forward`；要讓叢集中的服務有穩定入口，使用 Service。兩者用途不同。

## 本機暫時連線

```bash
kubectl port-forward pod/<pod-name> 8000:3000
```

本機 `8000` 轉到 Pod 的 `3000`。指令停止，轉送就結束；預設只綁定本機，不是公開網站的做法。

## 透過 Service 連線

```bash
kubectl expose pod <pod-name> --name=<service-name> --type=NodePort --port=3000 --target-port=3000
kubectl get services
```

`--port` 是 Service 的埠；`--target-port` 是 Pod 應用監聽的埠。**NodePort** 另在節點上配置埠，外部是否可連仍取決於節點網路、防火牆與環境。在 minikube 可查詢可用網址：

```bash
minikube service <service-name> --url
```

`<pod-name>` 和 `<service-name>` 是待替換的名稱。上述直接公開 Pod 適合示範；正式部署通常由 Deployment 管理 Pod，並用標籤選擇器讓 Service 找到後端。若 Pod 換了位置，Service 才能持續提供穩定入口。

參考：[Kubernetes 官方：kubectl expose](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_expose/)。

## 哪種入口適合？

- 只想在自己的筆電暫時檢查 Pod：`kubectl port-forward`；程序中斷後就不能連，也不提供正式對外入口。
- 叢集內服務彼此連線：使用 `ClusterIP` Service 和網域名稱系統（DNS，Domain Name System）名稱，不必替每個 Pod 建公開埠。
- 對外服務：可選 `NodePort`、`LoadBalancer` 或 Ingress／Gateway；實際可用性依叢集與網路環境而定。`NodePort` 並不保證雲端或本機都能從公網連到。

Service 透過選擇器追蹤符合條件的 Pod，並提供較穩定的存取點；它不保證 Pod 健康，仍需 readiness probe、足夠複本與監控。

參考：[Kubernetes：Service](https://kubernetes.io/docs/concepts/services-networking/service/)、[kubectl port-forward](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_port-forward/)。

## 相關筆記

- [[Docker 核心元件]]
