## Bạn có thể lập lịch chạy gitlab-CI
- Tình huống: Bạn muốn định kì lúc 4h sáng hàng ngày chạy 1 gitlab-ci để làm 1 việc gì đó. Cụ thể ở đây, mình viết gilab-ci để chạy 1 đoạn script xóa những runner đang có status offline.
- Gitlab-CI config:

```
stages:
- you-say-run

run:clean-up-gitlab-runner:
  stage: you-say-run
  image: tekohub/curl
  script:
  - apk add --update bash
  - cd clean-up-gitlab-runner
  - ./clean-up-gitlab-runners-offline
  tags:
  - ci-general
  only:
    refs:
      - master
    variables:
      - $CLEAN_UP
```
- **Ý nghĩa đoạn gitlab-ci là:**
  - runner pull repo về, chạy đoạn script `clean-up-gitlab-runners-offline` khi và chỉ khi ở trên `master` brach và có variable truyền vào là `CLEAN_UP`. cụ thể xem hình bên dưới

- và lập lịch cho nó ở:

![lập lịch](../../images/laplich.png)

