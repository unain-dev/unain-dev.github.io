---
layout: post
title: "Mysql ERROR : not connected 에러"
# date: 2021-12-10 12:34:43 +0900
categories: Mysql
---

### mysql에서 루트에 접근하고자 쿼리문을 쳤을 때 나는 오류이다.

- root 계정에 접근
    `mysql -u root -p`
- 오류 발생
    `ERROR: Not connected`
- 해결
    `\connect root@localhost`