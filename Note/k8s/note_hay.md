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
  
  
# Deployment, Replicaset, Pod
- `Replicaset`quản lý các `Pod`, nó đảm bảo số lượng các pod tồn tại trong 1 thời điểm thông qua tham số `replica: 3`
- `Deployment` quản lý các `replicaset`
- Khi tạo một `deployment`, nó sinh ra một `replicaset`tương ứng. 
- **Khi bạn update Deployment, nó sẽ sinh ra một bản Replicaset, tương ứng với những gì bạn update Deployemnt. Điểu này có nghĩa rằng, bạn có thể dựa vào số replicaset của Deployment đó, để biết số lần update, mỗi lần update cái gì, và có thể rollback lại tới bản replicaset nào bạn muốn**

![replicaset](../../images/replicaset.png)

- Xem lịch sử update `Deployment`:

![history-deployment](../../images/history-deployment.png)

- Xem chi tiết lần update đó :

![history-revison](../../images/history-revison.png)

- `rollback` `deployment` lại bản replicaset nào, dự vào `revision` của replicaset:

`kubectl -n authen-service rollout undo deployment authen-api-app --to-revision=2`






