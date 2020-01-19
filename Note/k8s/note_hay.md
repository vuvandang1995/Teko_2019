# Kubectl proxy

`kubectl proxy`

- Khi chạy lệnh này, `kubectl`sẽ proxy api của cluster ra máy local cho ta.

![proxy](../../images/kube-proxy.png)

- Dùng lệnh `kubectl get pod pod_name -o yaml` để lấy `selfLink`:

![selfLink](../../images/selfLink.png)

- Khi đó, ta có thể xem chi tiết pod đó trên trình duyệt bằng cách sau: 

![selfLinkpod](../../images/selfLinkpod.png)

- Muốn xem kết quả xử lý pod đó mà không cần portforword service nữa:

![proxypod](../../images/proxypod.png)

# Autoscale HPA
- Autoscale cho replicaset, deployment, ...
- Có 2 cách để tạo autoscale:
  - Cách 1: tạo bằng lệnh
    - `kubectl autoscale deploy deployment_name --min=3 --max=5`
    - khi chạy lệnh trên, sẽ tạo cho deployment 1 hpa, default mức CPU để scale là 80%
  - Cách 2: tạo bằng file yaml định nghĩa HPA
  
  
