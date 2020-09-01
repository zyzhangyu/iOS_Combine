# 1-3Back pressure
Combine is designed such that the subscriber controls the flow of data, and because of that it also controls processing that happens in the pipeline. This is a feature of Combine called back-pressure.

This means that the subscriber drives the processing within a pipeline by providing information about how much information it wants or can accept. When a subscriber is connected to a publisher, it requests data based with a specific Demand.

The demand request is propagated up through the composed pipeline. Each operator in turn accepting the request for data and in turn requesting information from the publishers to which it is connected.
Combine的设计使用户控制数据流，因此它也控制了管道中发生的处理。这是Combine的一个特点，叫做Back Pressure。

这意味着订阅者通过提供关于它想要或可以接受多少信息的信息来驱动管道内的处理。当一个订阅者连接到一个发布者时，它根据一个特定的Demand请求数据。

该需求请求通过组成的管道向上传播。每个操作者依次接受数据的请求，并依次向所连接的发布者请求信息。

In the first release of the Combine framework - in iOS 13 prior to iOS 13.3 and macOS prior to 10.15.2 - when the subscriber requested data with a Demand, that call itself was asynchronous. Because this process acted as the driver which triggered attached operators and ultimately the source publisher, it meant that there were scenarios where data might appear to be lost. Due to this, in iOS 13.3 and later Combine releases, the process of requesting demand has been updated to a synchronous/blocking call. In practice, this means that you can be a bit more certain of having any pipelines created and fully engaged prior to a publisher receiving the request to send any data.

There is an extended thread on the Swift forums about this topic, if you are interested in reading the history.
在Combine框架的第一个版本中--在iOS 13.3之前的iOS 13和10.15.2之前的macOS中--当用户用Demand请求数据时，该调用本身是异步的。因为这个过程充当了触发附加运营商并最终触发源发布者的驱动程序，这意味着有可能出现数据丢失的情况。由于这一点，在iOS 13.3及以后的Combine版本中，请求需求的过程已经更新为同步/阻塞调用。在实践中，这意味着您可以更确定地在发布者收到发送任何数据的请求之前创建并完全参与任何管道。

在Swift论坛上有一个关于这个话题的扩展线程，如果你有兴趣阅读历史。


With the subscriber driving this process, it allows Combine to support cancellation. Subscribers all conform to the Cancellable protocol. This means they all have a function cancel() that can be invoked to terminate a pipeline and stop all related processing.

When a pipeline has been cancelled, the pipeline is not expected to be restarted. Rather than restarting a cancelled pipeline, the developer is expected to create a new pipeline.

有了订阅者推动这个过程，就可以让Combine支持取消。订阅者都符合Cancelable协议。这意味着它们都有一个函数cancel()，可以调用它来终止管道并停止所有相关处理。

当一个管道被取消后，不希望管道被重新启动。开发者不需要重新启动被取消的管道，而是要创建一个新的管道。