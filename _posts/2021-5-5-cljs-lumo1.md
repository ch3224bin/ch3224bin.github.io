---
layout: post
title: "ClojureScript와 Lumo를 사용하여 윈도우 배경이미지 추가하기 - 1"
categories: [개발,취미,Clojure]
comments: true
---

Clojure에 관심이 생겨 간단한 스크립트를 Clojure를 사용하여 만들어 보고자 한다.

## 하고자 하는 작업

윈도우 로그인 시 나오는 배경이미지가 그렇게 이쁠 수 없다.

새로운 이미지가 나올때마다 스틸하여 내 배경화면 슬라이드쇼로 쓰고 싶다.

## Lumo 설치

Clojure를 빠르게 실행시키기 위해 선택하였다.

Lumo github : <https://github.com/anmonteiro/lumo>

2019년에 마지막 커밋이 있다. 비주류 언어의 안타까운 생태계...

```bash
$ sudo npm install -g lumo-cljs --unsafe-perm
```

## Hello, World 작성

난 Clojure에 대해 1도 모름으로 Hello, World!를 먼저 찍어본다.

1. 파일 생성

```bash
$ vi hello.cljs
```

2. 코드 작성

```clojure
#!/usr/bin/env lumo

(println "Hello, World!")
```

3. 실행권한 부여 후 실행

```bash
$ chmod +x hello.cljs
$ ./hello.cljs
```

## 마치며

헬로월드를 찍어보았으니, clojurescript 퀵스타트를 좀 보면서 코드를 추가해 봐야겠다.

