---


---

<h1 id="http-状态码">http 状态码</h1>
<h2 id="状态码分类">状态码分类</h2>
<p>HTTP状态码分为5类</p>

<table>
<thead>
<tr>
<th>总结范围</th>
<th>已定义范围</th>
<th>类别</th>
</tr>
</thead>
<tbody>
<tr>
<td>100-199</td>
<td>100-101</td>
<td>信息</td>
</tr>
<tr>
<td>200-299</td>
<td>200-206</td>
<td>成功</td>
</tr>
<tr>
<td>300-399</td>
<td>300-305</td>
<td>重定向</td>
</tr>
<tr>
<td>400-499</td>
<td>400-415</td>
<td>客户端错误</td>
</tr>
<tr>
<td>500-599</td>
<td>500-505</td>
<td>服务器错误</td>
</tr>
</tbody>
</table><h2 id="状态码">状态码</h2>
<p>HTTP/1.1规范定义的所有状态码的快速参考，表中概述了每种状态码及其含义。</p>

<table>
<thead>
<tr>
<th>状态码</th>
<th>原因短语</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr>
<td>100</td>
<td>continue</td>
<td>受到了请求的起始部分，客户端应该继续请求</td>
</tr>
<tr>
<td>101</td>
<td>Switch Protocols</td>
<td>服务器正根据客户端的指示将协议切换成Update首部列出的协议</td>
</tr>
<tr>
<td>200</td>
<td>OK</td>
<td>服务器已成功</td>
</tr>
<tr>
<td>201</td>
<td>Created</td>
<td>对那些要服务器创建对象的请求来说，资源创建完毕</td>
</tr>
<tr>
<td>202</td>
<td>Accepted</td>
<td>请求已接受，但服务器尚未处理</td>
</tr>
<tr>
<td>203</td>
<td>No Content</td>
<td>响应报文包含一些首部和一个状态行，但不包含实体的主体内容</td>
</tr>
<tr>
<td>204</td>
<td>Reset Content</td>
<td>另一个主要用于浏览器的代码。意思是浏览器应该重置当前页面上所有的HTML表单</td>
</tr>
<tr>
<td>206</td>
<td>Partial Content</td>
<td>部分请求成功</td>
</tr>
<tr>
<td>300</td>
<td>Multiple Choices</td>
<td>客户端请求了实际指向多个资源的URL。这个代码是和一个选项列表一起返回的，然后用户就可以选择他希望使用的选项了</td>
</tr>
<tr>
<td>301</td>
<td>Moved Permanently</td>
<td>请求的URL已搬走。响应中应该包含一个Location URL，说明资源现在所处的位置</td>
</tr>
<tr>
<td>302</td>
<td>Found</td>
<td>与状态码301类似，但这里的搬离是临时的。客户端应该用Location首部给出的URL对资源进行临时定位</td>
</tr>
<tr>
<td>303</td>
<td>See Other</td>
<td>告诉客户端应该用另一个URL获取资源。这个新的URL位于响应报文的Location首部</td>
</tr>
<tr>
<td>304</td>
<td>Not Modify</td>
<td>客户端可以通过她们所包含的请求首部发起条件请求。这个代码说明资源未发生过变化</td>
</tr>
<tr>
<td>305</td>
<td>Use Proxy</td>
<td>必须通过代理访问资源，代理的位置是在Location首部中给出</td>
</tr>
<tr>
<td>307</td>
<td>temporary Redirect</td>
<td>和状态码301类似，但客户端应该用Location首部给出的URL对资源进行临时定位</td>
</tr>
<tr>
<td>400</td>
<td>Bad request</td>
<td>告诉客户端它发送了一条异常请求</td>
</tr>
<tr>
<td>401</td>
<td>Unauthorized</td>
<td>与适当的首部一起返回，在客户端获得资源访问权之前，请它进行身份认证</td>
</tr>
<tr>
<td>402</td>
<td>Payment Required</td>
<td>当前状态码未使用</td>
</tr>
<tr>
<td>403</td>
<td>Forbidden</td>
<td>服务器拒绝了请求</td>
</tr>
<tr>
<td>404</td>
<td>Not Found</td>
<td>服务器无法找到所请求的URL</td>
</tr>
<tr>
<td>405</td>
<td>Method Not Allowed</td>
<td>请求中有一个所请求的URI不支持的方法。响应中应该包括一个Allow首部，以告知客户端所请求的资源支持使用哪些方法</td>
</tr>
<tr>
<td>406</td>
<td>Not Accepted</td>
<td>客户端可以指定一些参数来说明希望接收哪些类型的实体。服务器没有资源与客户端可接受的URL相互匹配时可使用此代码</td>
</tr>
<tr>
<td>407</td>
<td>Proxy Authentication Required</td>
<td>和状态码401类似，但用于需要进行资源认证的代理服务器</td>
</tr>
<tr>
<td>408</td>
<td>request Timeout</td>
<td>如果客户端完成其请求时花费的时间太长，服务器可以回送这个状态码并关闭连接</td>
</tr>
<tr>
<td>409</td>
<td>Conflict</td>
<td>发出的请求在资源上造成一些冲突</td>
</tr>
<tr>
<td>410</td>
<td>Gone</td>
<td>除了服务器曾持有这些资源以外，与状态码404类似</td>
</tr>
<tr>
<td>411</td>
<td>Length Required</td>
<td>服务器要求在请求报文中包含Content-Length首部时会使用这个代码。发起的请求中若没有Content-Length首部，服务器是不会接收此资源请求的。</td>
</tr>
<tr>
<td>412</td>
<td>Precondition Failed</td>
<td>如果客户端发起了一个条件请求</td>
</tr>
<tr>
<td>413</td>
<td>Request Entity Too Large</td>
<td>客户端发送的实体主体部分比服务器能够或者希望处理的要大</td>
</tr>
<tr>
<td>414</td>
<td>Request URI Too Long</td>
<td>客户端发送的请求所携带的求求URL超过了服务其能够或者希望处理的长度</td>
</tr>
<tr>
<td>415</td>
<td>Unsupported Media Type</td>
<td>服务器无法理解或不支持客户端所发送的实体的内容类型</td>
</tr>
<tr>
<td>416</td>
<td>Request Range Not Satisfiable</td>
<td>请求报文请求的是某范围内的指定资源，但那个范围无效，或者未得到满足</td>
</tr>
<tr>
<td>417</td>
<td>Expectation Failed</td>
<td>请求的Except首部包含了一个预期内容，但服务器无法满足</td>
</tr>
<tr>
<td>500</td>
<td>Internal Server Error</td>
<td>服务器遇到一个错误，使其无法为请求提供服务</td>
</tr>
<tr>
<td>501</td>
<td>Not Implement</td>
<td>服务器无法满足客户端请求的某个功能</td>
</tr>
<tr>
<td>502</td>
<td>Bad gateway</td>
<td>作为代理或网关使用的服务器遇到了来自响应链中上游的无效响应</td>
</tr>
<tr>
<td>503</td>
<td>Service Unavailable</td>
<td>服务器目前无法为请求提供服务，但过一段时间就可以恢复服务</td>
</tr>
<tr>
<td>504</td>
<td>Gateway timeout</td>
<td>与状态码408类似，但是响应来自网关或代理在等待另一台服务器的响应时出现了超时</td>
</tr>
<tr>
<td>505</td>
<td>HTTP Version Not Support</td>
<td>服务器受到的请求是以它不支持或不愿支持的协议版本表示的</td>
</tr>
</tbody>
</table>
