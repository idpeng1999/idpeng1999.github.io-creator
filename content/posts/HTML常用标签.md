---
title: "HTML常用标签"
date: 2021-10-28T23:02:29+08:00
draft: false
categories: [前端]
---
## 搜索技巧：
[谷歌搜索](https://www.google.com/)<br>
**mdn + xx(标签)**
## a 标签的用法

### href

```html
<ul>
  <li><a href="http://baidu.com">百度</a></li>
  <li><a href="https://baidu.com">百度</a></li>
  <li><a href="//baidu.com">百度</a></li>
  
  <li><a href="/a/b/index.html">/a/b/index.html页面</a></li>
  <li><a href="./index.html">index.html页面</a></li>
  
  
  
  <li><a href="123456789@163.com">Email</a></li>
  <li><a href="123456789">Phone</a></li>
</ul>
```

```
注意: 可以使用 href="#top" 或者 href="#" 链接返回到页面顶部。
```

<br/>

### target

- _self: **当前页面加载**。此值是默认的，如果没有指定属性的话。
- _blank: **新窗口打开**。
- _parent: 加载响应到当前的浏览上下文的**父浏览**上下文。如果没有parent框架或者浏览上下文，此选项的行为方式与 _self 相同。
- _top: IHTML4中：加载的响应成完整的，原来的窗口，取消所有其它frame。 HTML5中：加载响应进入顶层浏览上下文（即，浏览上下文，它是当前的一个的祖先，并且没有parent）。如果没有parent框架或者浏览上下文，此选项的行为方式相同_self

  <br/>

### 作用

- 跳转外部页面
- 跳转内部锚点
- 跳转到邮箱或电话等

[a](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/a)

## img 标签的用法

```html
<img class="fit-picture" src="1.jpg" alt="网络错误">
```

- src 属性是必须的，它包含了你想嵌入的图片的文件路径。
- alt 属性包含一条对图像的文本描述，这不是强制性的。如果由于某种原因无法加载图像，普通浏览器也会在页面上显示alt 属性中的备用文本：例如，网络错误、内容被屏蔽或链接过期时。

  [img](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/img)

## table 标签的用法

```html
<table>
    <thead>
        <tr>
            <th colspan="2">The table header</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>The table body</td>
            <td>with two columns</td>
        </tr>
    </tbody>
</table>
```

[table](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/table)
