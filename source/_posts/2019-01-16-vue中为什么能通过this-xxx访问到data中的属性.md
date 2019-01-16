---
title: vue中为什么能通过this.xxx访问到data中的属性
date: 2019-01-16 21:21:54
tags:
---

# 涉及的知识点
1. `Object.defineProperty`函数的使用

<!-- more -->

# 一个例子
```javascript
function noop () {}
const sharedPropertyDefinition = {
  enumerable: true,
  configurable: true,
  get: noop,
  set: noop
}
function proxy (target, sourceKey, key) {
  sharedPropertyDefinition.get = function () {
    return this[sourceKey][key]
  }
  sharedPropertyDefinition.set = function (val) {
    this[sourceKey][key] = val
  }

  Object.defineProperty(target, key, sharedPropertyDefinition)
}

function proxyPropertyDataToRoot (obj, proxyPropertyName) {
  const root = obj
  const proxyObj = obj[proxyPropertyName]
  const keys = Object.keys(proxyObj)
  let len = keys.length
  while(len--) {
    const key = keys[len]
    proxy(root, proxyPropertyName, key)
  }
}

const obj = {
  data: {
    a: 'a',
    b: 'b'
  }
}

proxyPropertyDataToRoot(obj, 'data')

console.log(obj.a) // 'a'
console.log(obj.b) // 'b'

```