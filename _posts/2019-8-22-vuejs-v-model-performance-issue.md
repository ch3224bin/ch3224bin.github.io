---
layout: post
title: "Vue.js v-model의 퍼포먼스 이슈"
categories: [개발,취미,Vue.js]
comments: true
---
# 앱을 하나 만들고 있는데 글씨를 입력할때 너무 버벅인다.  

[stackoverflow](https://stackoverflow.com/questions/42427845/how-to-make-vuejs-respond-faster-when-using-v-model-on-large-data-sets)를 찾아보니, v-model 퍼포먼스 관련 질문이 있었다.

`v-model.lazy`를 사용하라는 답변이 채택되어 있으나 효과는 없었다.

그 밑에 채택이 안된 답변이 효과가 있어서 적용했다.
```javascript
:value="mod.description" @change="v => mod.description = v"
```
