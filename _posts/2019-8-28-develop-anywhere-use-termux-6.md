---
layout: post
title: "Termux를 사용해 어디서든 개발하자 - 5부"
categories: [개발,취미,Termux]
comments: true
---
# 자동완성 기능을 추가하자. coc.nvim
IDE의 꿀맛을 못 잊었다. 사람의 기억력에는 한계가 있는 법.  
어찌 모든 프로퍼티들을 외울 수 있을까.  
`coc.nvim`이 좋다고 하니 까라보자.  

# vim-plug 설치
`coc.nvim` 홈페이지의 설치 안내를 보니, Vundle설치는 안내가 되어있지 않다.   
쫄보인 나는 안내대로 `vim-plug`를 설치한다.

아래 명령어를 실행한다.
```bash
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

`.vimrc`에 아래 구문을 추가한다.
```
call plug#begin('~/.vim/plugged')
call plug#end()
```

# coc.nvim을 설치하자.
위 begin과 end사이에 아래 구문을 넣는다.
```
Plug 'neoclide/coc.nvim', {'branch': 'release'}
```

`:so %`, `:PlugInstall`을 순서대로 실행한다.  

나는 vue.js를 개발하고 있으니 아래의 language server들을 추가한다.
```
:CocInstall coc-tsserver
:CocInstall coc-json
:CocInstall coc-vetur
```
추가되었다는 문구가 나올때까지 기다린다.

# 테스트 해보자
![alt 자동완성](/images/posts/2019-08-28/coc-0.jpg)
![alt 자동완성](/images/posts/2019-08-28/coc-1.jpg)
![alt 자동완성](/images/posts/2019-08-28/coc-2.jpg)*[여기까지 아름다운 모습들]*

Html 태그를 닫으려 하자 오류가 발생한다.
![alt 자동완성](/images/posts/2019-08-28/coc-3.jpg)*[아름답지 못한 모습 ]*

# 파일 자동완성 기능은 끄자.
`/`를 입력하면 루트 아래의 하위 디렉토리를 자동완성으로 보여준다.  
나는 루트 권한이 없으므로 위의 아름답지 못한 오류가 발생한다.

파일 자동완성은 쓸일이 없을 것 같아 껐다.  
물론 무시하는 옵션도 있지만 안씀.

`:CocConfig`를 입력하면 설정파일이 열린다.  
아래의 구문을 입력하고 vim을 껐다 키자.(파일에 아무 내용도 없다면 {} 열고 닫고 넣야야 한다.)
```json
"coc.source.file.enable": false
```

# 욕심을 더 내어 UltiSnips도 사용해 보자.
Vim에서는 abbr을 이용한 상용구 지원을 한다.  
거기에 더 현란한 기술을 쓰고 싶다면?
```
Plug 'SirVer/ultisnips'
```

`:so %`, `:PlugInstall` 설치하자.  

아래의 단축키 설정도 `.vimrc`에 추가한다.
```
" ultisnips settins
let g:UltiSnipsExpandTrigger="<Tab>"
let g:UltiSnipsJumpForwardTrigger="<Tab>"
let g:UltiSnipsJumpBackwardTrigger="<S-Tab>"
let g:UltiSnipsEditSplit="vertical"
let g:UltiSnipsSnippetDirectories = ['UltiSnips']
```

`coc.nvim`과 연동을 위해 아래 명령을입력한다.
```
:CocInstall coc-ultisnips
```

`~/.vim/UltiSnips` 디렉토리 안에 `vue.snippets`파일을 만들었다.
```
snippet "<([^\s].*)" "tag <...></...>" r
<`!p snip.rv=match.group(1)`>
	$0
</`!p snip.rv=match.group(1)`>
endsnippet
```

`<div`를 써준후 `tab`키를 누르면 아래 코드가 자동완성 된다.
```html
<div>
    _
</div>
```

