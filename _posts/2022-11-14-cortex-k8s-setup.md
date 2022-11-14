---
layout: post
title: "Kubernetes 환경에 Cortex 설치하기"
categories: [Cortex, Monitoring, Prometheus]
comments: true
---

Cortex를 K8s 환경에 설치 하는 방법을 간략하게 적어봅니다.

## 설치 환경

Cortex는 메모리를 많이 사용하는 편입니다. 특히 Ingester 컴포넌트는 노드에 단독으로 설치하는 것이 좋습니다.  
아래는 테스트 환경에서 설치한다고 생각하고 적겠습니다. K8s는 1.19.0 이상이 필요합니다.  

## 설치 방법

Helm Chart를 사용하여 설치합니다. [링크](https://github.com/cortexproject/cortex-helm-chart)  
해당 사이트에 자세한 방법이 있으나 여기에도 같이 적어 봅니다.  
(Helm 사용법 및 설치 방법은 [여기](https://helm.sh/)를 참고하세요.)

#### helm repository 추가

```
helm repo add cortex-helm https://cortexproject.github.io/cortex-helm-chart
```
#### 설정파일 없이 Cortex Install

```
  helm install cortex --namespace cortex cortex-helm/cortex
```

간단하게 설치가 완료되었습니다. 모든 옵션은 Helm Chart에서 정의한 기본값으로 설정이 됩니다. 기본값은 [여기](https://github.com/cortexproject/cortex-helm-chart)에서 확인할 수 있습니다.  

#### 설정파일 지정하여 Cortex Install

만약 설정값을 변경하고자 할때는 [파일](https://github.com/cortexproject/cortex-helm-chart/blob/master/values.yaml)을 받아 수정합니다.
그리고 아래와 같이 설정파일 경로를 지정하여 설치합니다.
```
  helm install cortex --namespace cortex -f my-cortex-values.yaml cortex-helm/cortex
```

#### 업그레이드 방법

설정값을 수정한 이후에는 아래와 같이 업그레이드하여 적용합니다.

```
  helm upgrade cortex -f my-cortex-values.yaml cortex-helm/cortex
```


## 그 다음 할일

Cortex의 아키텍처를 보시면 Block Storage 라는 것이 있습니다. 기존에는 Chunk Storage를 사용했으나 Deprecated 되었습니다.
시계열이 블록으로 저장되는데, 이 블록을 어느 장기저장소에 저장할 것인지 설정이 필요합니다.

더 중요한 것은 시계열 저장소는 만들었는데, 아직 시계열을 받을 수 있는 서비스 주소는 오픈하지 않았습니다. 위 설치 방법에 따르면 cortex-nginx라는 서비스와 deployment가 같이 설치가 됩니다. 이를 통해 요청을 받으면 되는데, 어떤 Ingress Controller를 사용할지가 정하기 나름입니다.
