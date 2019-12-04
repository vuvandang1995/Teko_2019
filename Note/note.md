## Git submodules
- Sử dụng `git submodules` repo này có thể sử dụng repo khác.
- link: https://kipalog.com/posts/Lam-viec-voi-git-submodule

## circle ci validate config cli
- link: https://circleci.com/docs/2.0/local-cli/#quick-installation


## Teraform 
```
module "records__id-dev_teko_vn" {
  source  = "../../mod/records"
  zone_id = cloudflare_zone.default.id

  name = "id-dev.teko.vn"
  records = [
    {
      type    = "A"
      value   = "35.240.235.171"
      ttl     = "1"
      proxied = true
    },
  ]
}
```

- Nếu `proxied = true` nghĩa là có ssl, domain sẽ trỏ về ip của Cloudflare(thực chất vẫn trỏ về ip của mình định nghĩa kia, chỉ là giấu đi thôi)
- Nếu `proxied = false` nghĩa là k có ssl, domain sẽ trỏ thẳng về ip mình định nghĩa bên trên
