---
title: 关于我所不知道的babel属性only的用法
date: 2022-06-17 02:58:24
tags: babel,only
---

在转译三方包的时候发现即使在 Webpack 的 include 属性中将其引入，但目标模块仍未被转译。 检查发现是配置文件中 only 属性导致。如下：

```javascript
env: {
    production: {
        only: ['app', 'libs', 'share'],
        plugins: []
    }
}
```

only 属性的值是一个数组，规定了编译的匹配规则，只会去编译数组中指定的模块(或目录)，对于不在数组中的模块或目录是不会被编译的。如上例，babel 只会去编译 app、libs 和 share 目录中的代码，未被指定的不会被编译。
这就是为什么出现上面问题的原因。

所以，如果要编译指定模块或第三方的包，将其添加到 only 中即可。

**参考**：

- https://www.babeljs.cn/docs/options
