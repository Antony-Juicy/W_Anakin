## http/https 区别?

1、https 协议需要到 CA 申请证书，一般免费证书较少，因而需要一定费用。

2、http 是超文本传输协议，信息是明文传输，https 则是具有安全性的 ssl/tls 加密传输协议。

3、http 和 https 使用的是完全不同的连接方式，用的端口也不一样，前者是 80，后者是 443。

4、http 的连接很简单，是无状态的；HTTPS 协议是由 SSL/TLS+HTTP 协议构建的可进行加密传输、身份认证的网络协议，比 http 协议安全。

## HTTP 1.0 / 1.1 / 2.0 在并发请求上的主要区别是什么？

1. HTTP 1.0

每次 TCP 连接都只能发送一个请求，当服务器响应后就会关闭此连接，下次再发请求还需要再次建立 TCP 连接。

2. HTTP 1.1

默认采用持续连接，TCP 连接默认不关闭，可以被多个请求复用，不用显示的声明 keep-alive。

增加了管道机制，在同一个 TCP 连接里，允许多个请求同时发送，增加了一定的并发性。

同一个 TCP 连接里，所有的数据通信是按照顺序进行的，如果服务器响应慢，回有很多的请求在排队，造成“对头阻塞”

3. HTTP 2.0

加了双工模式，客户端可以同时发送多个请求，服务器也可以同时响应多个请求，解决了 HTTP 的对头阻塞问题

使用了多路复用技术，同一个 TCP 连接可以并发处理多个请求。 服务器可以主动向客服端发送数据

## HTTP / 1.1 长连接和 / 2.0 多路复用的区别？

1.1：同一时间一个 TCP 连接只能处理一个请求，采用一问一答的形式，上一个请求响应才能处理下一个请求。由于浏览器最大连接数的限制，所以才有了最大并发请求的限制。

2.0: 痛域名下所有通信都在单个连接上完成。

## HTTP / 1.1 为什么不能实现多路复用呢？

- HTTP/2 基于二进制帧的协议。
- HTTP/1.1 基于文本分割解析的协议

## 缓存策略

缓存策略可以分为**强缓存**和**协商缓存**，这两种缓存策略都是通过设置 HTTP Header 来实现的

## 强缓存

- 强缓存可以通过设置两种 HTTP Header 来实现： **Expires** 和 **Cache-Control** 。 =一死派儿死 全死肯求
- 强缓存表示在缓存期间是不需要重新请求的， state code 为 200。
- Exprires 的值为服务端返回的数据到期时间。当再次请求时的请求时间小于返回的此时间，则直接使用缓存数据。但由于服务端时间和客户端时间可能有误差，这也将导致缓存命中的误差，另一方面，Expires 是 HTTP1.0 的产物，故现在大多数使用 Cache-Control 替代。

Cache-Control 有很多属性，不同的属性代表的意义也不同。

- private：客户端可以缓存 「派位特」

- public：客户端和代理服务器都可以缓存。「跑不累可」

- max-age=t：缓存内容将在 t 秒后失效

- no-cache：需要使用协商缓存来验证缓存数据 「no 卡去」

- no-store：所有内容都不会缓存。 「no 死到」

## 协商缓存

协商缓存需要进行对比判断是否可以使用缓存。浏览器第一次请求数据时，服务器会将缓存标识与数据一起响应给客户端，客户端将它们备份至缓存中。再次请求时，客户端会将缓存中的标识发送给服务器，服务器根据此标识判断。若未失效，返回 304 状态码，浏览器拿到此状态码就可以直接使用缓存数据了。

这时通过设置两种 HTTP Header 实现：**Last - Modified**  和  **Etag**。

Last-Modified：服务器在响应请求时，会告诉浏览器资源的最后修改时间。 「拉斯莫提 fied」

Etag：服务器响应请求时，通过此字段告诉浏览器当前资源在服务器生成的唯一标识（生成规则由服务器决定）

## 刷新对于强缓存和协商缓存的影响

\1. 当 ctrl+f5 强制刷新网页时，直接从服务器加载，跳过强缓存和协商缓存。

\2. 当 f5 刷新网页时，跳过强缓存，但是会检查协商缓存。

\3. 浏览器地址栏中写入 URL，回车 浏览器发现缓存中有这个文件了，不用继续请求了，直接去缓存拿。（最快）

## cookie,localStorage 和 sessionStorage 的区别

Cookie:一般由服务器生成，可设置失效时间。如果在浏览器端生成 Cookie，如果使用 cookie 保存过多数据会带来性能问题.localstorage:除非被清除，否则永久保存。仅在客户端（即浏览器）中保存，不参与和服务器的通信 sessionStorage：仅在当前会话下有效，关闭页面或浏览器后被清除。仅在客户端（即浏览器）中保存，不参与和服务器的通信

## 把网址写到浏览器到你看到的网页整个流程？

1.在浏览器地址栏中输入网址

2.浏览器获取这个网址之后，会先去缓存中看看有没有要访问的资源，从浏览器缓存-系统缓存-路由缓存中查看，如果有就不再进行 hhtp 请求，直接从缓存中加载资源。否则进行步骤 3

3.浏览器拿到域名自动去向 DNS(域名系统)服务器发起请求，查询用户输入的域名对应的 ip 地址

4.浏览器拿到 ip 地址后，通过 ip 地址和端口号和服务器建立 tcp 连接。

5.三次“握手”建立连接成功之后，浏览器开始向服务器发起 http 请求，并通过 http 协议将请求信息包装成请求报文（包含请求行、请求头、空行、请求体），然后通过 socket 发送到服务器

6.当服务器接收到客户端浏览器发送过来的请求报文时候，按照 HTTP 协议将请求报文解析出来

7.然后服务器拿着请求报文中的请求信息（例如请求路径 url），做相应的业务逻辑处理操作

8.当业务逻辑处理操作完成之后，服务器将发送给浏览器的数据按照 http 协议包装成响应报文（响应行、响应头、空行、响应体）

9.然后服务器将响应报文发送给浏览器

10.浏览器接收到响应报文后，按照 HTTP 协议将响应报文解析出来

11.浏览器拿到响应报文中响应体的数据开始渲染 html、css，执行 javaScript

12.如果在解析的过程（从上到下）中，发现有外链的标签（link、css、img）

13.浏览器会自动对该标签指向的 路径地址 发起新的请求，同上。
