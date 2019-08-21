---
layout: post
title: "Termux를 사용해 어디서든 개발하자 - 1부"
categories: [개발,취미,Termux]
comments: true
---
# Termux Package Management
이제부터 vim으로 코딩을 하기에 vim을 설치한다.
```
pkg install vim
```
`pkg`라는 명령어는 `apt-get`과 비슷하다.  
apt repository를 사용한다고 하니, 이보다 더 좋을 수 없다.

list-all 옵션으로 설치가능한 패키지 목록을 볼 수 있다.
```
pkg list-all

-- 내가 설치한 패키지 목록은
pkg list-installed

-- 삭제는
pkg uninstall [package name]
```

직접 deb파일을 다운 받아 설치 할 수도 있다.
deb라니.. 기대한 것 이상으로 좋다.
```
dpkg -i ./pagekage.deb

-- 삭제는
dpkg --remove [package name]

-- 설치된 목록은 이렇게 본다.
dpkg -l
```

그리고 nodejs를 설치하면 npm 사용이 가능하고,  
ruby를 설치하면 gem 사용이 가능하다.

# Termux Tip
나와 같이 하드웨어 키보드를 사용한다면 아래와 같은 유용한 단축키를 쓸 수 있다.  
Ctrl과 Alt를 누른 상태로
- 'C' -> 세션을 새로 연다.
- 화살표 아래(또는 'N') -> 다음 세션으로 이동
- 화살표 위(또는 'P') -> 이전 세션으로 이동
- 'V' -> 클립보드의 내용을 붙여 넣는다.
- +/- -> 텍스트 사이즈 조정.(손가락 두개로 해도 된다.)

# Vim을 사용하자
나의 계획은 Linux on Dex의 gui를 지원하는 ubuntu에서  
vscode나 IntelliJ를 사용하여 편하게 코딩하는 거였다.

하지만 돈이 없으면 몸이 고생하는법.
<span style="color: gray;">(나쁜것 만은 아니다. 왠지 해커같고 폼은 산다.)</span>

나는 vi명령어를 i, wq, q! 정도 밖에 모른다.  
모르면 배워야지... vim을 설치하고 vimtutor를 실행한다.
```
vimtutor
```
영어로 써진 화면이 뜨는데 키워드만 보고 따라하면 간단한 vi명령어를 익힐 수 있다.

본격적으로 Vim을 사용하기 앞서 자신에게 맞는 환경 설정이 필요하다.  
<span style="color: gray;">(환경설정은 일반적인 리눅스 환경과 같다.)</span>  
```
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
vi ~/.vimrc
```
나는 플러그인 설치를 위해 Vundle을 사용했다.  
.vimrc에 아래 구문을 추가해서 사용하면 된다.  
```
" syntax highlight를 켠다.
syntax on

call vundle#begin()
Plugin 'VundleVim/Vundle.vim'
... 기타 사용하고 싶은 플러그인 추가.
call vundle#end()
```
그리고 `:w`, `:so %`, `:PluginInstall` 순으로 입력하여 설치를 완료한다.

나는 vue를 사용할 건데, vue에 맞는 syntax highlight가 되어 있지 않다.
github에 vim plugin [vim-vue](https://github.com/posva/vim-vue) 가 있어 고대로 따라하였다.
![alt termux vim](/images/posts/2019-08-21/termux-vim.jpg)
*[termux에서 vim으로 vue파일을 편집하는 화면]*

이 글도 termux환경에서 작성했다.
