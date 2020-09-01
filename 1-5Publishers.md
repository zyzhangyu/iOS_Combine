# 1-5Publishers
The publisher is the provider of data. The publisher protocol has a strict contract returning values when asked from subscribers, and possibly terminating with an explicit completion enumeration.

Just and Future are common sources to start your own publisher from a value or asynchronous function.

Many publishers will immediately provide data when requested by a subscriber. In some cases, a publisher may have a separate mechanism to enable it to return data after subscription. This is codified by the protocol ConnectablePublisher. A publisher conforming to ConnectablePublisher will have an additional mechanism to start the flow of data after a subscriber has provided a request. This could be a separate .connect() call on the publisher itself. The other option is .autoconnect(), which will start the flow of data as soon as a subscriber requests it.

Combine provides a number of additional convenience publishers:

发布者是数据的提供者。发布者协议有一个严格的合同，当从订阅者那里询问时返回值，并可能以一个显式的完成枚举终止。

Just和Future是常见的来源，可以从一个值或异步函数中启动自己的发布器。

许多发布者在被订阅者请求时将立即提供数据。在某些情况下，一个发布者可能有一个单独的机制，使它能够在订阅后返回数据。这是由协议ConnectablePublisher编纂的。一个符合ConnectablePublisher的发布者将有一个额外的机制来启动订阅者提供请求后的数据流。这可以是对发布者本身的一个单独的.connect()调用。另一个选项是.autoconnect()，它将在订阅者提出请求后立即启动数据流。

Combine提供了一些额外的便利性发布器。
1.Just
2.Future
3.Deferred
4.Empty
5.Sequence
6.Fail
7.Record
8.Share
9.Multicast
10.ObservableObject
11.@Published




* A number of Apple API outside of Combine provide publishers as well.

* SwiftUI uses the @Published and @ObservedObject property wrappers, provided by Combine, to implicitly creates a publisher and support its declarative view mechanisms.
Combine之外的一些苹果API也提供了发布者。

SwiftUI使用Combine提供的@Published和@ObservedObject属性包装器，隐式创建一个发布者，并支持其声明式视图机制。
Foundation:

    URLSession.dataTaskPublisher

    .publisher on KVO instance

    NotificationCenter

    Timer

    Result








 
