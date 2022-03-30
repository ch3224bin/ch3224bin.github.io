---
layout: post
title: "[쿠버네티스] 디플로이먼트 변경 일시 중지(롤아웃, 롤백)"
categories: [개발, 쿠버네티스]
comments: true
---

도서 [쿠버네티스 완벽 가이드](http://www.yes24.com/product/goods/103206901)의 일부를 발췌

매니페스트를 수정하고 내가 파드를 직접 하나씩 죽어야할 필요가 있었다.  
보통 [kubectl 치트 시트](https://kubernetes.io/ko/docs/reference/kubectl/cheatsheet/)에 명령어가 다 있는데, 이 명령어는 없어서 적어 본다.

### 업데이트 정지, 해제

```shell
# 업데이트 일시 정지
$ kubectl rollout pause deployment sample-deployment

# 업데이트 일시 정지 해제
$ kubectl rollout resume deployment sample-deployment
```

### 변경된 매니페스트를 적용하고, 롤아웃 상태를 보면 업데이트 되지 않는다.

```shell
$ kubectl rollout status deployment sample-deployment
```

### pause 상태에서는 롤백도 되지 않는다.

```shell
$ kubectl rollout undo deployment sample-deployment
```