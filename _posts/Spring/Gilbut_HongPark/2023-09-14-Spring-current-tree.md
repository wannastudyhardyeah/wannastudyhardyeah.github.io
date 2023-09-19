---
title: 1.1. 프로젝트 생성
author: wannastudyhardyeah
date: 2023-09-14 01:17:00 +0800
categories: [Spring]
tags: [Spring, Java]
math: true

---
현재 길벗 출판사의 스프링 책을 통해 카피코딩하는 내용을 정리하려 한다.<br>
일단, 11장까지의 프로젝트 파일의 구조를 정리해보려 한다.<br>

```powershell
├── src
│   ├── main
│   │   ├── java
│   │   │   └── com.example.firstproject
│   │   │       ├── api
│   │   │       │   └── ArticleAPiController.java
│   │   │       ├── controller
│   │   │       │   └── ArticleController.java
│   │   │       ├── dto  
│   │   │       │   └── ArticleForm.java
│   │   │       ├── entity
│   │   │       │   └── Article.java
│   │   │       └── repository
│   │   │           └── ArticleRepository.java
|   |   |
│   │   └── resources
│   │       ├── application.properties
│   │       ├── data.sql
│   │       │
│   │       └── templates
│   │           ├── articles
│   │           │   ├── edit.mustache
│   │           │   ├── index.mustache
│   │           │   ├── new.mustache
│   │           │   └── show.mustache
│   │           └── layouts 
│   │               ├── footer.mustache
│   │               └── header.mustache

```