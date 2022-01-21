---
layout: post
title: "sessionStorage setItem 조회 안되는 이유"
categories: React.js, ES6
---

## sessionStorage

- setItem 시, 반드시 JSON.stringify(object)로 object를 string화 해야한다.

- getItem 시, 반드시 JSON.parse(sessionStorage.getItem(keyName))으로 JSON 형태로 파싱시켜야한다.
