---
layout: post
title: "REST Assured의 JsonPath는 Groovy의 GPath 문법을 사용한다"
categories: [개발, rest-assured]
comments: true
---

인수테스트 작성을 위해 REST Assured를 사용했다.  
rest-assured에서 jsonpath 라이브러리를 제공하는데, 난 이게 [이 JsonPath](https://github.com/json-path/JsonPath) 라이브러리를 사용하는 줄 알았다.

어쩐지 해당 라이브러리의 문법이 적용이 잘 안되었는데, 아직 개발이 안되서 그런건 줄 착각하고 있었다. 내 인지 능력에 문제가 있음이 분명하다.

오늘은 전보다 조금 복잡한 json 탐색을 하려는데, 잘 안되서 [api 문서](https://www.javadoc.io/doc/io.rest-assured/json-path/4.5.1/io/restassured/path/json/JsonPath.html)를 보니 [Groovy의 GPath](https://groovy-lang.org/processing-xml.html) 문법을 사용한다고 첫 문단에 적혀 있는 걸 봤다.

그렇구나.. 아래와 같이 적용해 봤는데, 잘 동작한다.

```java
assertThat(jsonPath.param("name", "mece").getString("list.find{it -> it.name == name}.age")).isEqualTo("25");
```