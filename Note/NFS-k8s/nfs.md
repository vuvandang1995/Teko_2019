### NFS làm storage trong k8s, chia sẻ volume
- *B1*: Cài đặt nfs-server

```
sudo apt-get update

sudo apt-get install nfs-kernel-server -y

systemctl enable nfs-server

systemctl start nfs-server
```

- *B2* tạo folder để share

```
vi /etc/exports

/data/k8stest/sf  *(rw,sync,no_subtree_check,insecure)

mkdir -p /data/k8stest/sf

chown –R 777 /data/k8stest/sf
```
- *B3* Cài nfs-client-provider trên k8s
  - link: https://github.com/helm/charts/tree/master/stable/nfs-client-provisioner
  
