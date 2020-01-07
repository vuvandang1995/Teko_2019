### khi xóa prometheus, cần xoá các thứ sau

* crd

```
kubectl delete crd prometheuses.monitoring.coreos.com
kubectl delete crd prometheusrules.monitoring.coreos.com
kubectl delete crd servicemonitors.monitoring.coreos.com
kubectl delete crd podmonitors.monitoring.coreos.com
kubectl delete crd alertmanagers.monitoring.coreos.com
```

* validatingwebhookconfigurations.admissionregistration.k8s.io
`kubectl -n namespace delete validatingwebhookconfigurations.admissionregistration.k8s.io name_`

* mutatingwebhookconfigurations.admissionregistration.k8s.io
`kubectl -n namespace delete mutatingwebhookconfigurations.admissionregistration.k8s.io name_`

* xóa cả các service, configmap, ... ở các namespace nếu còn. Nhất là ở `kube-system` namespace

