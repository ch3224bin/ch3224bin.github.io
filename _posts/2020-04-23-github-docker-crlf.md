---
layout: post
title: "git clone한 소스 윈도우에서 docker로 돌렸을 때"
categories: [개발,Docker,Git]
comments: true
---
## 사건 개요

`스프링 마이크로 서비스 코딩 공작소`라는 책을 사서 예제를 윈도우10에서 돌려보고 있다.

```bash
docker-compose -f docker/common/docker-compose.yml up
```

위의  명령어를 실행하니 아래와 같은 오류가 발생하고 돌아가질 않는다.

```bash
... 어쩌고 ...
/bin/sh: ./run.sh: not found
... 저쩌고 ...
exited with code 127
```

## 발생 원인

원인은 `git clone https://github.com/gilbutITbook/006962.git example` git clone으로 예제소스를 받았는데,  
윈도우에서 소스를 받으면 공백문자가 LF -> CRLF로 변경된다.

리눅스 플래폼으로 docker가 실행되면서 CRLF로 끝나는 명령어를 제대로 실행 못 한 것 같다.

## 해결 방법

1. 그냥 zip으로 소스 다운 받는다.
2. git clone 시 LF -> CRLF로 바꾸는 설정을 끈다.

``` bash
git config --global core.autocrlf false
```
