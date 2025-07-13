---
category: Browser
---

# useUrlSearchParams

响应式 [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams)

## 用法

```js
import { useUrlSearchParams } from '@vueuse/core'

const params = useUrlSearchParams('history')

console.log(params.foo) // 'bar'

params.foo = 'bar'
params.vueuse = 'awesome'
// URL 更新为 `?foo=bar&vueuse=awesome`
```

### 哈希模式

当在哈希模式路由中使用时，将 `mode` 设置为 `hash`

```js
import { useUrlSearchParams } from '@vueuse/core'

const params = useUrlSearchParams('hash')

params.foo = 'bar'
params.vueuse = 'awesome'
// URL 更新为 `#/your/route?foo=bar&vueuse=awesome`
```

### 哈希参数

当在历史模式路由中使用，但想要使用哈希作为参数时，将 `mode` 设置为 `hash-params`

```js
import { useUrlSearchParams } from '@vueuse/core'

const params = useUrlSearchParams('hash-params')

params.foo = 'bar'
params.vueuse = 'awesome'
// URL 更新为 `/your/route#foo=bar&vueuse=awesome`
```

### 自定义 stringify 函数

你可以通过 `stringify` 选项提供自定义函数来自定义 URL 参数的序列化方式。
当你需要特殊格式的查询字符串时，这会很有用。

```js
import { useUrlSearchParams } from '@vueuse/core'

// 自定义 stringify 函数：移除空值的等号（当值为空时，仅保留键名，不输出等号)
const params = useUrlSearchParams('history', {
  stringify: (params) => {
    return params.toString().replace(/=(&|$)/g, '$1')
  }
})

params.foo = ''
params.bar = 'value'
// URL 更新为 `?foo&bar=value`，而不是 `?foo=&bar=value`
```
