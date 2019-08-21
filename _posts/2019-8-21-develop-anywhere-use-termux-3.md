---
layout: post
title: "Termux를 사용해 어디서든 개발하자 - 2부"
categories: [개발,취미,Termux]
comments: true
---
# Vim에 NERDTree 끼얹기
IDE로 주로 작업하던 나 같은 사람이 vim을 사용하면 여러모로 불편하다.  
특히 여러 파일을 요리조리 옮겨가며 작업을 해야하는데,  
매번 `:e 파일명`으로 작업할 수가 없다.

이런 고민은 NERDTree가 해결해 준다.

![alt nerdtree](/images/posts/2019-08-21/nerdtree-vim.jpg)*NERDTree의 장엄한 모습*

생으로 vim을 사용하다가 NERDTree를 접하면 정말이지 신세경이다.

설치는 Vundle을 플러그인을 사용한다.  
.vimrc 수정하여 vundle 안쪽에 추가한다.
```
Plugin 'scrooloose/nerdtree'
```
`:w`, `:so %`, `:PluginInstall` 순으로 입력하여 설치를 완료한다.

vim을 다시 실행시키고 `:NERDTree`를 입력하면 그 위용이 드러난다.

# NERDTree 단축키
마우스 없이 파일 탐색을 하는데,  
우리 동년배가 쓰던 MS-DOS시절 M과는 차이가 있다.

우선 화살표로 탐색을 하는게 아니고,  
에디터와 NERDTree를 와리가리 해야한다.

## 이동
- ctrl + w, h <NERDTree로 이동>
- ctrl + w, l <오른쪽 화면으로 이동>
- h,j,k,w <화살표와 같다>

## 탭으로 열기
NERDTree에 커서가 있을때 파일 선택 후
- t <탭으로 열기>
- T <탭으로 열지만 화면 뒤에서 연다>
- gt <이전 탭으로 이동>
- gT <다음 탭으로 이동>
대소문자 구분이 있다.

## 파일, 디렉토리 작업
- m <메뉴열기>
  - a <추가 (디렉토리는 끝에 /를 붙인다.)>
  - m <이동, 파일,디렉토리명 변경>
  - c <복사>
  - d <삭제>
## 편의기능
- cd <선택된 디렉토리를 작업디렉토리(CWD)로 변경>
- CD CWD를 ROOT로 변경.
- :Bookmark <선택항목 북마크에 추가>
- B <북마크 보기, 북마크에서 d로 항목삭제>
- C <선택된 디렉토리를 root로 만듦>
- I <히든파일 보기 토글>
- o <디렉토리 토글>
- O <디렉토리 리커시브 열기>
- A <NERDTree를 전체화면으로 토글>
- r <새로고침>

더 많은 다축키는 `?`를 눌러서 확인한다.  
도움말을 닫으려면 다시 `?`를 누른다.

# NERDTree TIP
NERDTree를 열고닫고 토글하려면,  
`:NERDTreeToggle`이라고 처야되는데 너무 길다.

.vimrc를 수정해서 단축키를 만들 수 있다.  
```
let mapleader=";"
nnoremap <Leader>n :NERDTreeToggle<CR>
```
이제 `;n`을 치면 NERDTree가 토글되어 보인다.

이것이 바로 소확행인가... ㅠㅠ
