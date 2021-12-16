---
layout: post
title: "application.property 분리하기 & 주입하기 & 변수 사용하기"
date: 2021-12-16 12:34:43 +0900
categories: Spring
---

1. `src/main/resources/`에 `application-API-KEY.property` 파일 추가.

2.

```
	package com.ssafy.vue.config;

	import org.springframework.beans.factory.annotation.Value;
	import org.springframework.boot.ApplicationArguments;
	import org.springframework.boot.ApplicationRunner;
	import org.springframework.boot.context.properties.ConfigurationProperties;
	import org.springframework.stereotype.Component;

	@Component
	@ConfigurationProperties("api")
	public class KeyConfig implements ApplicationRunner{

		private String key;
		private String GEO_API_KEY;
		private String KAKAO_MAP_API_KEY;
		private String consumer_key;
		private String consumer_secret;

		public String getGEO_API_KEY() {
			return GEO_API_KEY;
		}

		public void setGEO_API_KEY(String gEO_API_KEY) {
			GEO_API_KEY = gEO_API_KEY;
		}

		public String getKAKAO_MAP_API_KEY() {
			return KAKAO_MAP_API_KEY;
		}

		public void setKAKAO_MAP_API_KEY(String kAKAO_MAP_API_KEY) {
			KAKAO_MAP_API_KEY = kAKAO_MAP_API_KEY;
		}

		public String getConsumer_key() {
			return consumer_key;
		}

		public void setConsumer_key(String consumer_key) {
			this.consumer_key = consumer_key;
		}

		public String getConsumer_secret() {
			return consumer_secret;
		}

		public void setConsumer_secret(String consumer_secret) {
			this.consumer_secret = consumer_secret;
		}

		@Override
		public void run(ApplicationArguments args) throws Exception {
			// TODO Auto-generated method stub
	//		System.out.println(getKey());
		}

		public String getKey() {
			return key;
		}

		public void setKey(String key) {
			this.key = key;
		}

	}
```
