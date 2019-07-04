> 在我们日常 Web 开发中，或多或少的都接触过 HTTP 状态码，那这些状态码代表什么意思呢？如何熟记它们？熟记这些状态码又有什么好处呢？下面我就为大家一一道来，可以把本片文章‘收藏’以备不时之需。

## HTTP 状态代码表示什么意思？
HTTP 状态码（英语：HTTP Status Code）是用以表示 HTTP 响应状态的 3 位数字代码。比如：
- 1xx：消息
- 2xx：成功
- 3xx：重定向
- 4xx：客户端错误
- 5xx：服务器错误

熟记这些状态码可以让我们在快速定位 Web 开发中遇到的问题、编写符合规范的接口服务，那么下面就让我们看看这些死板的 3 位数字都是什么意思。撸猫爱好者，请注意：前方高能，屏住呼吸，一大波可爱的小猫咪即将来袭！

## 一、1xx 消息
这一类型的状态码，代表请求已被接受，需要继续处理。这类响应是临时响应，表示客户应该采取的其它行动。

### 100 Continue（继续）
![](https://img.hellogithub.com/06/100.jpeg)

服务器已经接收到请求头，请求者应当继续提出请求。服务器返回此代码表示已收到请求的第一部分，正在等待其余部分。

### 101 Switching Protocols（切换协议）
![](https://img.hellogithub.com/06/101.jpg)

服务器已经理解了客户端的请求，并将通过 Upgrade 消息头通知客户端采用不同的协议来完成这个请求。在发送完这个响应后，服务器将会切换到在 Upgrade 消息头中定义的那些协议。

只有在切换新的协议更好的进行通信。例如：切换到新的 HTTP 版本（如 HTTP/2）比旧版本更有优势、或切换到一个实时且同步的协议（如 WebSocket）等


## 二、2xx 成功
这一类型的状态码，代表请求已成功被服务器接收、理解、并接受。

### 200 OK（成功）
![](https://img.hellogithub.com/06/200.jpg)

已成功处理了请求。出现此状态码是表示正常状态。

### 201 Created（已创建）	
![](https://img.hellogithub.com/06/201.jpg)

请求成功并且服务器创建了新的资源。

### 202 Accepted（已接受）
![](https://img.hellogithub.com/06/202.jpg)

服务器已接受请求，但尚未处理。

### 203 Non-Authoritative Information（非授权信息）
![](https://img.hellogithub.com/06/203.jpg)

服务器已成功处理了请求，但返回的信息可能来自另一来源。

### 204 No Content（无内容）
![](https://img.hellogithub.com/06/204.jpg)

服务器成功处理了请求，但没有返回任何内容。

### 206 Partial Content（部分内容）	
![](https://img.hellogithub.com/06/206.jpg)

服务器成功处理了部分 GET 请求。

## 三、3xx 重定向
这类状态码代表需要客户端采取进一步的操作才能完成请求。通常，这些状态码用来重定向，后续的请求地址（重定向目标）在本次响应的 Location 域中指明。
当且仅当后续的请求所使用的方法是 GET 或者 HEAD 时，用户浏览器才可以在没有用户介入的情况下自动提交所需要的后续请求。

客户端应当自动监测无限循环重定向（例如：A->A，或者A->B->C->A），因为这会导致服务器和客户端大量不必要的资源消耗。按照 HTTP/1.0 版规范的建议，浏览器不应自动访问超过5次的重定向。

### 300 Multiple Choices（多种选择）
![](https://img.hellogithub.com/06/300.jpg)

针对请求，服务器可执行多种操作。服务器可根据请求者选择一项操作，或提供操作列表供请求者选择。

### 301 Moved Permanently（永久移动）
![](https://img.hellogithub.com/06/301.jpg)

请求的资源已永久移动到新位置。服务器返回此响应（对 GET 或 HEAD 请求的响应）时，会自动将请求者转到新位置。

### 302 Move Temporarily（临时移动）
![](https://img.hellogithub.com/06/302.jpg)

请求的资源临时从不同的 URI 响应请求。由于这样的重定向是临时的，客户端应当继续向原有地址发送以后的请求。只有在 Cache-Control 或 Expires 中进行了指定的情况下，这个响应才是可缓存的。

### 303 See Other（查看其他位置）
![](https://img.hellogithub.com/06/303.jpg)

对应当前请求的响应可以在另一个 URL 上被找到，而且客户端应当采用 GET 的方式访问那个资源。这个方法的存在主要是为了允许由脚本激活的 POST 请求输出重定向到一个新的资源。这个新的 URI 不是原始资源的替代引用。同时，303响应禁止被缓存。当然，第二个请求（重定向）可能被缓存。

### 304 Not Modified（未修改）
![](https://img.hellogithub.com/06/304.jpg)

自从上次请求后，请求的资源未修改过。服务器返回此响应时，不会返回资源的内容，因此可节省带宽和开销。

### 305 Use Proxy（使用代理）
![](https://img.hellogithub.com/06/305.jpg)

请求者只能使用代理访问请求的网页。如果服务器返回此响应，还表示请求者应使用代理。

### 307 Temporary Redirect（临时重定向）
![](https://img.hellogithub.com/06/307.jpg)

服务器目前从不同位置的网页响应请求，但请求者应继续使用原有位置来响应以后的请求。 此代码与响应 GET 和 HEAD 请求的 301 代码类似，会自动将请求者转到不同的位置，但您不应使用此代码来告诉搜索引擎爬虫某个页面或网站已经移动，因为搜索引擎爬虫会继续抓取原有位置并编制索引。

## 四、4xx 客户端错误
这类的状态码代表了客户端看起来可能发生了错误，妨碍了服务器的处理。


### 400 Bad Request（错误请求）
![](https://img.hellogithub.com/06/400.jpg)

服务器不理解请求的语法。

### 401 Unauthorized（未授权）
![](https://img.hellogithub.com/06/401.jpg)

请求要求身份验证。 对于需要登录的网页，服务器可能返回此响应。

### 403 Forbidden（禁止）
![](https://img.hellogithub.com/06/403.jpg)

服务器拒绝请求。

### 404 Not Found（未找到）
![](https://img.hellogithub.com/06/404.jpg)

服务器找不到请求的资源。 例如，对于服务器上不存在的资源经常会返回此代码。

### 405 Method Not Allowed（方法禁用）
![](https://img.hellogithub.com/06/405.jpg)

禁用请求中指定的方法（HTTP METHOD）。

### 406 Not Acceptable（不接受）
![](https://img.hellogithub.com/06/406.jpg)

请求的资源的内容特性无法满足请求头中的条件，因而无法生成响应实体，该请求不可接受。

### 408 Request Timeout（请求超时）
![](https://img.hellogithub.com/06/408.jpg)

服务器等候请求时发生超时。

### 409 Conflict（冲突）
![](https://img.hellogithub.com/06/409.jpg)

由于和被请求的资源的当前状态之间存在冲突，请求无法完成。

### 410 Gone（已删除）
![](https://img.hellogithub.com/06/410.jpg)

如果请求的资源已永久删除，服务器就会返回此响应。 

### 411 Length Required（需要有效长度）
![](https://img.hellogithub.com/06/411.jpg)

务器不接受不含有效内容长度标头字段的请求。


### 412 Precondition Failed（未满足前提条件）
![](https://img.hellogithub.com/06/412.jpg)

服务器未满足请求者在请求中设置的其中一个前提条件。

### 413 Request Entity Too Large（请求实体过大）
![](https://img.hellogithub.com/06/413.jpg)

服务器无法处理请求，因为请求实体过大，超出服务器的处理能力。

### 414 Request-URI Too Long（请求的 URI 过长）
![](https://img.hellogithub.com/06/414.jpg)

请求的 URI（通常为网址）过长，服务器无法处理。


### 415 Unsupported Media Type（不支持的媒体类型）
![](https://img.hellogithub.com/06/415.jpg)

请求的格式不受请求页面的支持。


### 416 Requested Range Not Satisfiable（请求范围不符合要求）
![](https://img.hellogithub.com/06/416.jpg)

如果页面无法提供请求的范围，则服务器会返回此状态代码。

### 417 Expectation Failed（未满足期望值）
![](https://img.hellogithub.com/06/417.jpg)

服务器未满足"Expect"请求头字段的要求。

### 429 Too Many Requests（请求太频繁）
![](https://img.hellogithub.com/06/429.jpg)

用户在给定的时间内发送了太多的请求。旨在用于网络限速。


### 431 Request Header Fields Too Large（请求头字段过大）
![](https://img.hellogithub.com/06/431.jpg)

服务器不愿处理请求，因为一个或多个头字段过大。


## 五、5xx 服务器错误
这类状态码代表了服务器在处理请求的过程中有错误或者异常状态发生，也有可能是服务器意识到以当前的软硬件资源无法完成对请求的处理。

### 500 Internal Server Error（服务器内部错误）	
![](https://img.hellogithub.com/06/500.jpg)

服务器遇到错误，无法完成请求。

### 502 Bad Gateway（错误网关）
![](https://img.hellogithub.com/06/502.jpg)

服务器作为网关或代理，从上游服务器收到无效响应。

### 503 Service Unavailable（服务不可用）
![](https://img.hellogithub.com/06/503.jpg)

服务器目前无法使用（由于超载或停机维护）。 通常，这只是暂时状态。

### 504 Gateway Timeout（网关超时）
![](https://img.hellogithub.com/06/504.jpg)

服务器作为网关或代理，但是没有及时从上游服务器收到请求。


## 参考
- 维基百科 HTTP 状态码
- https://http.cat/

## 最后
![](https://img.hellogithub.com/website-qr.png)

欢迎关注 HelloGitHub 公众号，您的每一个关注、留言、转载、点赞，都是对我们最大的鼓励和肯定！

写完这篇文章我都想养只猫了，名字叫 “200”。

欢迎留言写出你家猫的品种和你对他的爱称，我很好奇有没有给自己家猫起名叫 “404” 的小伙伴😂
