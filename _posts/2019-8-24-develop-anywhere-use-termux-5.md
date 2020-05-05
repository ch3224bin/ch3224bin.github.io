---
layout: post
title: "Termux를 사용해 어디서든 개발하자 - 4부"
categories: [개발,취미,Termux]
comments: true
---
# Termux 위에 Ubuntu - JDK를 설치하자

드디어 Java를 사용하고 싶어 졌다. 하지만 Termux에서는 공식적으로 jdk를 지원하지 않는다.  
진짜 jdk를 설치하고 싶다면 arch linux나 ubuntu를 Termux에 설치하여 사용하기를 권장한다. 띠용~?

# Ubuntu를 설치하자

설치 방법은 간단하다.  
아래 명령을 순서대로 따라하면 설치가 완료된다.

```bash
pkg install proot wget

mkdir ~/ubuntu_directory

cd ~/ubuntu_directory

wget https://raw.githubusercontent.com/Neo-Oli/termux-ubuntu/master/ubuntu.sh

bash ubuntu.sh

./ubuntu_directory/start-ubuntu.sh
```

출처 : [Termux Wiki](https://wiki.termux.com/wiki/Ubuntu)

# JDK, Gradle 설치

이제 우분투 환경에서 다시 필요한 패키지를 싹 설치해 주면 된다.  
jdk와 gradle도 아래와 같이 그냥 설치하면 되니 편하다.

```bash
apt-get install default-jdk
apt-get install gradle
```

springboot 프로젝트를 하나 만들어서 돌려보았는데 문제 없이 돌아간다.

# 마치며

Termux에서 우분투를 실행하는 것은 꽤 무거운 작업이다.  
배터리가 좀 더 빠르게 줄어드는게 보이니 마음이 불편하다.  
무선충전기 또는 블루투스 키보드가 있으신 분들은 맘껏 쓰셔요~  
저는 크흡.. ㅠㅠ