# 1-7Subjects
Subjects are a special case of publisher that also adhere to the Subject protocol. This protocol requires subjects to have a .send(_:) method to allow the developer to send specific values to a subscriber (or pipeline).

Subjects can be used to "inject" values into a stream, by calling the subject’s .send(_:) method. This is useful for integrating existing imperative code with Combine.

A subject can also broadcast values to multiple subscribers. If multiple subscribers are connected to a subject, it will fan out values to the multiple subscribers when send(_:) is invoked. A subject is also frequently used to connect or cascade multiple pipelines together, especially to fan out to multiple pipelines.

A subject does not blindly pass through the demand from its subscribers. Instead, it provides an aggregation point for demand. A subject will not signal for demand to its connected publishers until it has received at least one subscriber itself. When it receives any demand, it then signals for unlimited demand to connected publishers. With the subject supporting multiple subscribers, any subscribers that have not requested data with a demand are not provided the data until they do.

There are two types of built-in subjects with Combine: CurrentValueSubject and PassthroughSubject. They act similarly, the difference being CurrentValueSubject remembers and requires an initial state, where PassthroughSubject does not. Both will provide updated values to any subscribers when .send() is invoked.

Both CurrentValueSubject and PassthroughSubject are also useful for creating publishers for objects conforming to ObservableObject. This protocol is supported by a number of declarative components within SwiftUI.


Subjects是发布者的一种特殊情况，它也遵守Subject协议。这个协议要求subjects有一个.send(_:)方法，允许开发者向订阅者（或管道）发送特定的值。

通过调用subject的.send(_:)方法，subject可以用来将值 "注入 "到一个流中。这对于将现有的命令式代码与Combine集成是很有用的。

一个subject还可以将值广播给多个订阅者。如果多个订阅者连接到一个subject，那么当调用send(_:)时，它将向多个订阅者扇形输出值。一个subject也经常被用来连接或级联多个管道，特别是向多个管道扇出值。

一个subject并不盲目地传递来自其订阅者的需求。相反，它提供了一个需求的聚集点。一个主体在自己收到至少一个用户之前，不会向其连接的发布者发出需求信号。当它收到任何需求时，它就会向连接的发布者发出无限需求信号。在主体支持多个订阅者的情况下，任何没有需求数据的订阅者都不会被提供数据，直到他们提出需求。

Combine内置的主题有两种类型。CurrentValueSubject和PassthroughSubject。它们的作用类似，不同的是CurrentValueSubject会记住并需要一个初始状态，而PassthroughSubject不需要。当调用.send()时，两者都会向任何订阅者提供更新的值。

CurrentValueSubject和PassthroughSubject对于为符合ObservableObject的对象创建发布者也很有用。SwiftUI中的许多声明性组件都支持这个协议。