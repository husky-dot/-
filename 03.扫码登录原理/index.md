

原文：https://juejin.cn/post/6844904111398191117

思考：简述一下扫码登录原理


扫码登录可以分为三个阶段：待扫描、已扫描待确认、已确认。我们就一一来看看这三个阶段。

待扫描阶段

 PC 端携带设备信息想服务端发起生成二维码请求，服务端会生成唯一的二维码 ID。PC 端接受到二维码 ID 之后，将二维码 ID 以二维码的形式展示，等待移动端扫码。此时在 PC 端会启动一个定时器，轮询查询二维码的状态。如果移动端未扫描的话，那么一段时间后二维码将会失效。

 已扫描待确认阶段

 移动端扫描二维码，获取二维码 ID，然后将手机端登录的信息凭证（token）和 二维码 ID 作为参数发送给服务端，服务端接受请求后，会将 token 与二维码 ID 关联，。然后会生成一个一次性 token，这个 token 会返回给移动端，一次性 token 用作确认时候的凭证。

 PC 端的定时器，会轮询到二维码的状态已经发生变化，会将 PC 端的二维码更新为已扫描，请确认。

 已确认

 移动端携带上一步骤中获取的临时 token ，确认登录，服务端校对完成后，会更新二维码状态，并且给 PC 端生成一个正式的 token ，后续 PC 端就是持有这个 token 访问服务端。