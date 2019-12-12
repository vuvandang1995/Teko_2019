# Giới thiệu
- Dùng Terraform để quản lý dns của bạn trên cloudflare
# Chi tiết
- Cloudflare là nhà cung cấp quản lý dns trung gian, đứng giữa `browser`và `server`của bạn
- Nghĩa là: CloudFlare cho phép bạn tạo các zone và giúp quản lý và trỏ domain dễ dàng hơn.
  - Khi trỏ domain, nếu bạn bật mode `proxied = true`, điều đó có nghĩa là, request từ `browser` -> ip của CloudFlare -> `servercuar bạn`, nếu `proxied = flalse`, request sẽ đi thẳng vào server của bạn
  
