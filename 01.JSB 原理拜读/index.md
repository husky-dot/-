
原文：[JSB 原理与实践](https://mp.weixin.qq.com/s/G5CRcR4HS3FZ6qzo5k08tA)

思考几个问题：

* 什么是 JSB
* 怎么实现(原理)



#### 什么是 JSB

JSB 是让 web 端和 Native 端得以实现双向通信。

要实现双向通信，自然要实现 Native 向 Web 发送消息和 Web 向 Native 发送消息。

Native 向 Web 发送消息基本原理上是在 WebView 容器中动态地执行一段 JS 脚本，通常情况下是调用一个挂载在全局上下文的方法。

Web 向 Native 发送消息本质上就是某段 JS 代码的执行端上是可感知的，目前业界主流的实现方案有两种，分别是拦截式和注入式。

拦截式具体指的是 Native 拦截 Web 发出的 URL 请求，双方在此之前约定一个 JSB 请求格式，如果该请求是 JSB 则进行相应的处理，若不是则直接转发。

注入式的原理是通过 WebView 提供的接口向 JS 全局上下文对象（window）中注入对象或者方法，当 JS 调用时，可直接执行相应的 Native 代码逻辑，从而达到 Web 调用 Native 的目的。