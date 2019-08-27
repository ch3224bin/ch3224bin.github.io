---
layout: post
title: "Termux를 사용해 어디서든 개발하자 - 3부"
categories: [개발,취미,Termux]
comments: true
---
# Vim을 좀 더 편하게
Termux 덕분에 Vim의 매력에 강제로 빠지게 되었다.  
그냥 쓰려면 조금 불편하다..  
좀 더 편해지고 싶다면? 미리미리 불편한 작업을 해두자.

# 상태바에 멋을 더하자 - vim-airline
`Plugin 'vim-airline/vim-airline'`

![alt vim-airline](/images/posts/2019-08-23/vim-airline.jpg)*[멋이 상승했다.]*

상태바가 좀 더 멋스러워졌다.  
거기에 약간의 설정을 추가하면 화면 상단에 열려있는 버퍼를 볼 수 있다.
```
" vim-airline settings
" 상단 버퍼 목록 켜기
let g:airline#extensions#tabline#enabled = 1
" 파일명만 출력
let g:airline#extensions#tabline#fnamemod = ':t'
```

# 파일 찾기 - CtrlP
IDE의 소중함을 알려주는 Vim.  
그동안 내가 외우는 파일명은 쉽게 찾아 가지 않았던가?  
Vim에서는 `Plugin 'ctrlpvim/ctrlp.vim'`가 필요하다.  
`:CtrlP`를 치면 파일 검색을 할 수 있다. 대단해~  
아래처럼 단축키를 지정해서 편히 쓰자.
```
" CtrlP
nmap <Leader>p :CtrlP<CR>
nmap <Leader>bb :CtrlPBuffer<CR>
nmap <Leader>bm :CtrlPMixed<CR>
nmap <Leader>bs :CtrlPMRU<CR>

" CtrlP settings
let g:ctrlp_custom_ignore = {
  \ 'dir': '\v[\/](\.(git|hg|svg)|\_site|node_modules)$',
  \ 'file': '\v\.(exe|so|dll|class)$'
  \ }

" 가장 가까운 디렉토리를 cwd로 사용
let g:ctrlp_working_path_mode = 'r'
```

![alt vim-ctrlp](/images/posts/2019-08-23/vim-ctrlp.jpg)*[파일 검색이 된다. 게다가 빠릿빠릿함.]*

# 버퍼를 좀 더 편하게 관리하자 - Buffergator
`Plugin 'jeetsukumaran/vim-buffergator'`  
기존에는 버퍼를 이동할때 `:bn`, `:bp`를 쓰고,  
버퍼를 지울때는 `:bd`를 사용했다.

이 플러그인을 사용하면 버퍼를 목록에서 편하게 관리할 수 있다.

![alt vim-buffergator](/images/posts/2019-08-23/vim-buffergator.jpg)*[열려있는 버퍼를 확인 할 수 있다.]*

아래처럼 단축키를 설정하면 편하다.
```
" Buffergator
nmap <Leader>jj :BuffergatorMruCyclePrev<CR>
nmap <Leader>kk :BuffergatorMruCycleNext<CR>
nmap <Leader>bl :BuffergatorOpen<CR>
" 현재 버퍼를 닫고 이전 버퍼로 이동
nmap <Leader>bq :bp <BAR> bd #<CR>

" Buffergator settings
let g:buffergator_viewport_split_policy = 'B'
let g:buffergator_suppress_keymaps = 1
let g:buffergator_mru_cycle_loop = 1
```

# 이 장을 마치며
소스를 주로 수정하는 작업을 하다보니, Vim의 활용이 절실하다.  
본래 소중함을 모르고 쓰던 것을을 하나하나 직접 설정하며 쓰는게 Vim의 매력 포인트같다.  
조금은 불편하지만 스마트폰으로 코딩한다는게 너무 재밌지 않은가?  
그것도 폼나게 Vim으로~
