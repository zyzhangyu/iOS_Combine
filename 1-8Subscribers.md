# 1-8Subscribers
While Subscriber is the protocol used to receive data throughout a pipeline, the subscriber typically refers to the end of a pipeline.

There are two subscribers built-in to Combine: Assign and Sink. There is a subscriber built in to SwiftUI: onReceive.

Subscribers can support cancellation, which terminates a subscription and shuts down all the stream processing prior to any Completion sent by the publisher. Both Assign and Sink conform to the Cancellable protocol.

When you are storing a reference to your own subscriber in order to clean up later, you generally want a reference to cancel the subscription. AnyCancellable provides a type-erased reference that converts any subscriber to the type AnyCancellable, allowing the use of .cancel() on that reference, but not access to the subscription itself (which could, for instance, request more data). It is important to store a reference to the subscriber, as when the reference is deallocated it will implicitly cancel its operation.

Assign applies values passed down from the publisher to an object defined by a keypath. The keypath is set when the pipeline is created. An example of this in Swift might look like:

虽然Subscriber是用于在整个管道中接收数据的协议，但Subscriber通常指的是管道的末端。

Combine内置有两个订阅者。Assign和Sink。SwiftUI内置有一个订阅者：onReceive。

订阅者可以支持取消，它可以终止订阅，并在发布者发送任何完成之前关闭所有的流处理。Assign和Sink都符合Cancellable协议。

当你为了以后的清理而存储对自己的订阅者的引用时，你一般希望有一个引用来取消订阅。AnyCancellable提供了一个类型被擦除的引用，它将任何订阅者转换为AnyCancellable类型，允许在该引用上使用.cancell()，但不允许访问该订阅本身（例如，它可以请求更多的数据）。存储对订阅者的引用很重要，因为当引用被deallocated时，它将隐式地取消其操作。

Assign 将从发布者传递下来的值应用到由 keypath 定义的对象上。关键路径是在创建管道时设置的。在Swift中的一个例子可能是这样的。


```swift
.assign(to: \.isEnabled, on: signupButton)
```

Sink accepts a closure that receives any resulting values from the publisher. This allows the developer to terminate a pipeline with their own code. This subscriber is also extremely helpful when writing unit tests to validate either publishers or pipelines. An example of this in Swift might look like:

Sink接受一个闭包，从发布者那里接收任何结果值。这允许开发者用自己的代码终止管道。当编写单元测试来验证发布者或管道时，这个订阅者也非常有用。在Swift中的一个例子可能是这样的。


```swift
.sink { receivedValue in
    print("The end result was \(String(describing: receivedValue))")
}
```

Other subscribers are part of other Apple frameworks. For example, nearly every control in SwiftUI can act as a subscriber. The View protocol in SwiftUI defines an .onReceive(publisher) function to use views as a subscriber. The onReceive function takes a closure akin to sink that can manipulate @State or @Bindings within SwiftUI.

An example of that in SwiftUI might look like:
其他的订阅者是苹果其他框架的一部分。例如，几乎SwiftUI中的每一个控件都可以作为一个订阅者。SwiftUI中的View协议定义了一个.onReceive(publisher)函数来使用view作为订阅者。onReceive函数采取一个类似于sink的闭包，可以在SwiftUI中操纵@State或@Bindings。

在SwiftUI中，一个例子可能是这样的。


```swift
struct MyView : View {

    @State private var currentStatusValue = "ok"
    var body: some View {
        Text("Current status: \(currentStatusValue)")
            .onReceive(MyPublisher.currentStatusPublisher) { newStatus in
                self.currentStatusValue = newStatus
            }
    }
}
```
For any type of UI object (UIKit, AppKit, or SwiftUI), Assign can be used with pipelines to update properties.

对于任何类型的UI对象（UIKit、AppKit或SwiftUI），Assign可以与管道一起使用，以更新属性。

