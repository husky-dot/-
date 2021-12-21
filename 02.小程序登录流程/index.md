

原文：https://zhuanlan.zhihu.com/p/116506244

思考：简述一下小程序的登录流程

* 通过 wx.login() 获取到用户的code
* 然后把 code 发送给我们的后端，后端收到到，会连 appid, appscrept 一起发送给微信服务器
* 微信服务器验证成功会返回了 openid
* 我们后端拿到 openid 后，会从数据库里找，如果没找到说明是新用户，如果有，则继续往下走。
* 后端用 openid 生成对应 token 并返回给小程序
* 小程序收到 token 后，保存到 storage 里面
* 下次请求，会先从 storage 里面获取，然后发给后端
* 后端拿到 token 会先校验有效期，有效则通知小程序执行登入后的操作
* 无效则重新登录