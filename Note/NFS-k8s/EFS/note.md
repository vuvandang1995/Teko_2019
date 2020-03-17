### Tạo nsf trong eks
- Link hướng dẫn gốc: https://aws.amazon.com/vi/premiumsupport/knowledge-center/eks-persistent-storage/
- có 1 lưu ý: 
  - tạo thư mục trên filesystem của efs trước, rồi mới mount được vào pod thông qua pv, nếu k tạo trước, auto mount vào `/`
  - k thể mount chung 1 filesystem trong cùng 1 pod
  
