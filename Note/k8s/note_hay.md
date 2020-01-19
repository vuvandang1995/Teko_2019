## Kubectl proxy

`kubectl proxy`

- Khi chạy lệnh này, `kubectl`sẽ proxy api của cluster ra máy local cho ta.

![proxy](../images/kube-proxy.png)

- Dùng lệnh `kubectl get pod pod_name -o yaml` để lấy `selfLink`:

![selfLink](../images/selfLink.png)

- Khi đó, ta có thể xem chi tiết pod đó trên trình duyệt bằng cách sau: 

![selfLinkpod](../images/selfLinkpod.png)

- Muốn xem kết quả xử lý pod đó : 

![proxypod](../images/proxypod.png)
