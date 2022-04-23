---
layout: post
title: "[Cortex] multi-tenant global view 설정하기"
categories: [개발, Cortex]
comments: true
---

Cortex는 tenant 별로 시계열 데이터를 수집할 수 있다.  
만약 tenant가 팀별로 되어 있고, 각 팀의 지표를 종합적으로 보고 싶을때 아래와 같은 설정을 통해 global view를 제공할 수 있다.

## Cortex Configuration

자세한 사항은 [링크](https://cortexmetrics.io/docs/configuration/configuration-file/#supported-contents-and-default-values-of-the-config-file)를 참고한다.  
아래와 같이 기본 설정을 추가하면 global view를 제공할 수 있게 된다.  

```yaml
# tenant 기능을 사용한다.
# CLI flag: -auth.enabled
auth_enabled: true

# 아래의 설정이 global view를 사용하게 해준다.
# CLI flag: -tenant-federation.enabled
tenant_federation:
  enabled: true
```

## Prometheus Configuration

프로메테우스의 prometheus.yml 설정에서 remote_write에 아래와 같은 설정이 추가되어야 한다.

```yaml
remote_write:
  - url: http://<cortex>/prometheus/api/v1/push
    headers:
      X-Scope-OrgID: <org>
```

## Query API

tenant 별 쿼리는 http header `X-Scope-OrgID` 에 tenant 값을 지정하여 할 수 있다.  
multi-tenant 쿼리를 할때는 tenant 사이에 파이프(|)를 연결해 주면 된다.

각 tenant team1, team2, team3을 같이 조회하고 싶다면 아래와 같이 설정한다.

```text
X-Scope-OrgID: team1|team2|team3
```

![QUERY API](/images/posts/2022-04-23/cotex-multi-tenant-query.png)
<span style="color:gray;">위와 같이 테스트 해보자</span>


## 출처

- [https://www.youtube.com/watch?v=VPBKNfRRytg](https://www.youtube.com/watch?v=VPBKNfRRytg)
- [https://cortexmetrics.io/docs/configuration/configuration-file/#supported-contents-and-default-values-of-the-config-file](https://cortexmetrics.io/docs/configuration/configuration-file/#supported-contents-and-default-values-of-the-config-file)
- [https://cortexmetrics.io/docs/proposals/cross-tenant-query-federation](https://cortexmetrics.io/docs/proposals/cross-tenant-query-federation)