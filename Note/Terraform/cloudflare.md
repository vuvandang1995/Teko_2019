# Giới thiệu
- Dùng Terraform để quản lý dns của bạn trên cloudflare
# Lưu ý 1
- Cloudflare là nhà cung cấp quản lý dns trung gian, đứng giữa `browser`và `server`của bạn
- Nghĩa là: CloudFlare cho phép bạn tạo các zone và giúp quản lý và trỏ domain dễ dàng hơn.
  - Khi trỏ domain, nếu bạn bật mode `proxied = true`, điều đó có nghĩa là, request từ `browser` -> ip của `CloudFlare` -> `servercuar bạn`, nếu `proxied = flalse`, request sẽ đi thẳng vào server của bạn
  - Việc bật mode `proxied = true`, sẽ giúp bạn tránh được tấn công DDos, vì request từ `browser` -> ip của `CloudFlare`
  - **Lưu ý**: bạn có thể bật mode https từ `browser` -> ip của `CloudFlare`, nhưng phía server của bạn, app cũng phải được cấu hình https

# Lưu ý 2
- khi dùng `terraform` chạy gitlab-ci để quản lý dns trên `CloudFlare`, bạn cần lưu trữ file backend (file chứa xxx.tfstate) nơi khác. ví dụ như gsc, s3, ...
  
- Cấu hình ví dụ:

```
provider "cloudflare" {}

terraform {
  backend "gcs" {
    bucket = "devopsnd95-terraform"
    prefix = "terraform-state"
  }
}
```
 - **Lưu ý**: bạn phải setup variabels cho gitlab-runner: `CLOUDFLARE_API_KEY`, `CLOUDFLARE_EMAIL`, `GOOGLE_CREDENTIALS` (key để có quyền ghi và đọc bucket lưu file tfstate bên trên)
 
 
