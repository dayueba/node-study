REST vs RPC

Stub负责调用参数和返回值的流化\(serialization\)、 参数的打包解包，以及负责网络层的通信。Client端一 般叫Stub，Server端一般叫Skeleton。

在做API服务器开发时，很多人都会遇到这个问题——选择REST还是RPC。RPC相比REST的优点主要有3点:

1. RPC+Protobuf采用的是TCP做传输协议，REST直接使用HTTP做应用层协议，这种区别导致REST在调用性能上会比RPC+Protobuf低

2. RPC不像REST那样，每一个操作都要抽象成对资源的增删改 查，在实际开发中，有很多操作很难抽象成资源，比如登录操 作。所以在实际开发中并不能严格按照REST规范来写API，RPC就不存在这个问题

3. RPC屏蔽网络细节、易用，和本地调用类似

这里的易用指的是调用方式上的易用性。在做RPC开发 时，开发过程很烦琐，需要先写一个DSL描述文件，然 后用代码生成器生成各种语言代码，当描述文件有更改 时，必须重新定义和编译，维护性差。

但是REST相较RPC也有很多优势:

轻量级，简单易用，维护性和扩展性都比较好

1. REST相对更规范，更标准，更通用，无论哪种语言都支持HTTP协议，可以对接外部很多系统，只要满足HTTP调用即 可，更适合对外，RPC会有语言限制，不同语言的RPC调用 起来很麻烦

2. JSON格式可读性更强，开发调试都很方便

3. 在开发过程中，如果严格按照REST规范来写API，API看起来更清晰，更容易被大家理解

在实际开发中，严格按照REST规范来写很难，只能尽 可能RESTful化。



其实业界普遍采用的做法是，内部系统之间调用用RPC，对外用REST，因为内部系统之间可能调用很频繁，需要RPC的高性能支 撑。对外用REST更易理解，更通用些。当然以现有的服务器性能， 如果两个系统间调用不是特别频繁，对性能要求不是非常高，以笔者 的开发经验来看，REST的性能完全可以满足。本小册不是讨论微服 务，所以不存在微服务之间的高频调用场景，此外REST在实际开发 中，能够满足绝大部分的需求场景，所以RPC的性能优势可以忽 略，相反基于REST的其他优势，笔者更倾向于用REST来构建API服务器，本小册正是用REST⻛格来构建API的。





