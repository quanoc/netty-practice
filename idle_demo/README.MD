[Netty 超时机制及心跳程序实现](https://www.cnblogs.com/wxd0108/p/6516199.html)

Netty 的超时类型 IdleState 主要分为：

- ALL_IDLE : 一段时间内没有数据接收或者发送
- READER_IDLE ： 一段时间内没有数据接收
- WRITER_IDLE ： 一段时间内没有数据发送

在 Netty 的 timeout 包下，主要类有：

- IdleStateEvent ： 超时的事件
- IdleStateHandler ： 超时状态处理
- ReadTimeoutHandler ： 读超时状态处理
- WriteTimeoutHandler ： 写超时状态处理

```
new IdleStateHandler(READ_IDEL_TIME_OUT,
			WRITE_IDEL_TIME_OUT, ALL_IDEL_TIME_OUT, TimeUnit.SECONDS));	
```
上述例子，在 IdleStateHandler 中定义了读超时的时间是 4 秒， 写超时的时间是 5 秒，其他所有的超时时间是 7 秒。

### 应用 IdleStateHandler

既然 IdleStateHandler 包括了读\写超时状态处理，那么很多时候 ReadTimeoutHandler 、 WriteTimeoutHandler 都可以不用使用。定义另一个名为 HeartbeatHandlerInitializer 的 ChannelInitializer ：


