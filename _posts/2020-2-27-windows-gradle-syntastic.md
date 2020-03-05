---
layout: post
title: "Windows에서 vim gradle-syntastic-plugin 설정"
categories: [개발,취미,Vim,Java]
comments: true
---
Vim에서 Java 코드를 작성하고 싶어졌다.

나는 Windows에서 Neovim을 terminal 세팅으로 사용하고 있다. 

이런저런 이야기는 생략하고 본론으로 바 로 들어간다.  

# gradle-syntastic-plugin의 동작원리
[gradle-syntastic-plugin](https://github.com/Scuilion/gradle-syntastic-plugin) 에 자세한 설치 방법이 적혀있다.  
(먼저 [syntastic](https://github.com/vim-syntastic/syntastic) 이 설치가 되어있어야 한다.)

```
let g:syntastic_java_javac_config_file_enabled = 1
```

.vimrc에 위의 설정을 하면 cwd에 위치한 **.syntastic_javac_config** 파일을 읽어와 문법오류체크에 필요한 클래스패스를 확인한다.  

이 플러그인은 gradle build시 클래스패스를 모아 위 파일을 생성한다.  

# Windows에서의 문제
클래스패스의 디렉토리를 '\'로 나타내는데 Vim의 syntastic가 이걸 이스케이프 시퀀스로 처리해버린다.(\n \b 같이) 

```
:SyntasticJavacEditClasspath
```

Vim에서 위 명령어를 치면 잘 깨져나오는 것을 볼 수 있다. 
때문에 제대로 동작을 안한다.  

# 해결
**.syntastic_javac_config**파일에서 \를 /로 변경해주는 task를 build.gradle에 추가했다.  

```groovy
task replaceSlash {
  doLast {
    File file = project.file('.syntastic_javac_config')
    String text = file.text.replace('\\', '/')
    file.write(text)
  }
}

syntastic.finalizedBy(replaceSlash)
```

# 마치며
이미 이슈가 2015년에 올라와 있는데 5년이 가도록 아무도 고치고 있지 않다. 

[Slashes in syntastic_javac_config](https://github.com/Scuilion/gradle-syntastic-plugin/issues/6)

