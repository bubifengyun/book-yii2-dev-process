# 附录-己 HTTP 状态码

参考网页：
+ https://zh.wikipedia.org/wiki/HTTP%E7%8A%B6%E6%80%81%E7%A0%81
+ http://www.zuojj.com/archives/124.html

下面内容全是转载 http://www.zuojj.com/archives/124.html ,表示感谢。

<article class="article-content">
			<h3>一、状态码与原因短语</h3>
<p>状态码（HTTP Status Code）是试图理解和满足请求的三位数字的整数码，而原因短语（Reason-Phrase）是为了给出的关于状态码的文本描述。状态码用于控制条件，而原因短语（Reason-Phrase）是让用户便于阅读。客户端不需要检查和显示原因短语。</p>
<h3>二、状态码的分类</h3>
<p>状态码的第一位数字定义响应类型。后两位数字没有任何分类角色。第一位数字有五种值：</p>
<table id="tank_table" class="article_con_table" border="1" cellpadding="5" cellspacing="0" align="center" width="100%">
<thead>
<tr>
<th></th>
<th>已定义范围</th>
<th>分类</th>
</tr>
</thead>
<tbody>
<tr>
<td>1XX</td>
<td>100-101</td>
<td>信息提示状态码</td>
</tr>
<tr>
<td>2XX</td>
<td>200-206</td>
<td>成功状态码</td>
</tr>
<tr>
<td>3XX</td>
<td>300-307</td>
<td>重定向状态码</td>
</tr>
<tr>
<td>4XX</td>
<td>400-417</td>
<td>客户端错误状态码</td>
</tr>
<tr>
<td>5XX</td>
<td>500-505</td>
<td>服务器错误状态码</td>
</tr>
</tbody>
</table>
<h3></h3>
<h3></h3>
<h3></h3>
<h3></h3>
<h3></h3>
<h3>三、状态码对照表</h3>
<table class="article_con_table" border="1" cellpadding="5" cellspacing="0" width="100%">
<thead>
<tr>
<th width="70">状态代码</th>
<th width="120">状态信息</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr>
<td>100</td>
<td>Continue</td>
<td>初始的请求已经接受，客户应当继续发送请求的其余部分。（HTTP 1.1新）</td>
</tr>
<tr>
<td>101</td>
<td>Switching Protocols</td>
<td>服务器将遵从客户的请求转换到另外一种协议（HTTP 1.1新）</td>
</tr>
<tr>
<td>200</td>
<td>OK</td>
<td>一切正常，对GET和POST请求的应答文档跟在后面。</td>
</tr>
<tr>
<td>201</td>
<td>Created</td>
<td>服务器已经创建了文档，Location头给出了它的URL。</td>
</tr>
<tr>
<td>202</td>
<td>Accepted</td>
<td>已经接受请求，但处理尚未完成。</td>
</tr>
<tr>
<td>203</td>
<td>Non-Authoritative Information</td>
<td>文档已经正常地返回，但一些应答头可能不正确，因为使用的是文档的拷贝（HTTP 1.1新）。</td>
</tr>
<tr>
<td>204</td>
<td>No Content</td>
<td>没有新文档，浏览器应该继续显示原来的文档。如果用户定期地刷新页面，而Servlet可以确定用户文档足够新，这个状态代码是很有用的。</td>
</tr>
<tr>
<td>205</td>
<td>Reset Content</td>
<td>没有新的内容，但浏览器应该重置它所显示的内容。用来强制浏览器清除表单输入内容（HTTP 1.1新）。</td>
</tr>
<tr>
<td>206</td>
<td>Partial Content</td>
<td>客户发送了一个带有Range头的GET请求，服务器完成了它（HTTP 1.1新）。</td>
</tr>
<tr>
<td>300</td>
<td>Multiple Choices</td>
<td>客户请求的文档可以在多个位置找到，这些位置已经在返回的文档内列出。如果服务器要提出优先选择，则应该在Location应答头指明。</td>
</tr>
<tr>
<td>301</td>
<td>Moved Permanently</td>
<td>客户请求的文档在其他地方，新的URL在Location头中给出，浏览器应该自动地访问新的URL。</td>
</tr>
<tr>
<td>302</td>
<td>Found</td>
<td>类似于301，但新的URL应该被视为临时性的替代，而不是永久性的。注意，在HTTP1.0中对应的状态信息是“Moved Temporatily”。出现该状态代码时，浏览器能够自动访问新的URL，因此它是一个很有用的状态代码。注意这个状态代码有时候可以和301替换使用。例如，如果浏览器错误地请求http://host/~user（缺少了后面的斜杠），有的服务器 返回301，有的则返回302。严格地说，我们只能假定只有当原来的请求是GET时浏览器才会自动重定向。请参见307。</td>
</tr>
<tr>
<td>303</td>
<td>See Other</td>
<td>类似于301/302，不同之处在于，如果原来的请求是POST，Location头指定的重定向目标文档应该通过GET提取（HTTP 1.1新）。</td>
</tr>
<tr>
<td>304</td>
<td>Not Modified</td>
<td>客户端有缓冲的文档并发出了一个条件性的请求（一般是提供If-Modified-Since头表示客户只想比指定日期更新的文档）。服务器告 诉客户，原来缓冲的文档还可以继续使用。</td>
</tr>
<tr>
<td>305</td>
<td>Use Proxy</td>
<td>客户请求的文档应该通过Location头所指明的代理服务器提取（HTTP 1.1新）。</td>
</tr>
<tr>
<td>307</td>
<td>Temporary Redirect</td>
<td>和302 （Found）相同。许多浏览器会错误地响应302应答进行重定向，即使原来的请求是POST，即使它实际上只能在POST请求的应答是303时才能重定 向。由于这个原因，HTTP 1.1新增了307，以便更加清除地区分几个状态代码：当出现303应答时，浏览器可以跟随重定向的GET和POST请求；如果是307应答，则浏览器只 能跟随对GET请求的重定向。（HTTP 1.1新）</td>
</tr>
<tr>
<td>400</td>
<td>Bad Request</td>
<td>请求出现语法错误。</td>
</tr>
<tr>
<td>401</td>
<td>Unauthorized</td>
<td>客户试图未经授权访问受密码保护的页面。应答中会包含一个WWW-Authenticate头，浏览器据此显示用户名字/密码对话框，然后在填 写合适的Authorization头后再次发出请求。</td>
</tr>
<tr>
<td>403</td>
<td>Forbidden</td>
<td>资源不可用。服务器理解客户的请求，但拒绝处理它。通常由于服务器上文件或目录的权限设置导致。</td>
</tr>
<tr>
<td>404</td>
<td>Not Found</td>
<td>无法找到指定位置的资源。这也是一个常用的应答。</td>
</tr>
<tr>
<td>405</td>
<td>Method Not Allowed</td>
<td>请求方法（GET、POST、HEAD、DELETE、PUT、TRACE等）对指定的资源不适用。（HTTP 1.1新）</td>
</tr>
<tr>
<td>406</td>
<td>Not Acceptable</td>
<td>指定的资源已经找到，但它的MIME类型和客户在Accpet头中所指定的不兼容（HTTP 1.1新）。</td>
</tr>
<tr>
<td>407</td>
<td>Proxy Authentication Required</td>
<td>类似于401，表示客户必须先经过代理服务器的授权。（HTTP 1.1新）</td>
</tr>
<tr>
<td>408</td>
<td>Request Timeout</td>
<td>在服务器许可的等待时间内，客户一直没有发出任何请求。客户可以在以后重复同一请求。（HTTP 1.1新）</td>
</tr>
<tr>
<td>409</td>
<td>Conflict</td>
<td>通常和PUT请求有关。由于请求和资源的当前状态相冲突，因此请求不能成功。（HTTP 1.1新）</td>
</tr>
<tr>
<td>410</td>
<td>Gone</td>
<td>所请求的文档已经不再可用，而且服务器不知道应该重定向到哪一个地址。它和404的不同在于，返回407表示文档永久地离开了指定的位置，而 404表示由于未知的原因文档不可用。（HTTP 1.1新）</td>
</tr>
<tr>
<td>411</td>
<td>Length Required</td>
<td>服务器不能处理请求，除非客户发送一个Content-Length头。（HTTP 1.1新）</td>
</tr>
<tr>
<td>412</td>
<td>Precondition Failed</td>
<td>请求头中指定的一些前提条件失败（HTTP 1.1新）。</td>
</tr>
<tr>
<td>413</td>
<td>Request Entity Too Large</td>
<td>目标文档的大小超过服务器当前愿意处理的大小。如果服务器认为自己能够稍后再处理该请求，则应该提供一个Retry-After头（HTTP 1.1新）。</td>
</tr>
<tr>
<td>414</td>
<td>Request URI Too Long</td>
<td>URI太长（HTTP 1.1新）。</td>
</tr>
<tr>
<td>416</td>
<td>Requested Range Not Satisfiable</td>
<td>服务器不能满足客户在请求中指定的Range头。（HTTP 1.1新）</td>
</tr>
<tr>
<td>500</td>
<td>Internal Server Error</td>
<td>服务器遇到了意料不到的情况，不能完成客户的请求。</td>
</tr>
<tr>
<td>501</td>
<td>Not Implemented</td>
<td>服务器不支持实现请求所需要的功能。例如，客户发出了一个服务器不支持的PUT请求。</td>
</tr>
<tr>
<td>502</td>
<td>Bad Gateway</td>
<td>服务器作为网关或者代理时，为了完成请求访问下一个服务器，但该服务器返回了非法的应答。</td>
</tr>
<tr>
<td>503</td>
<td>Service Unavailable</td>
<td>服务器由于维护或者负载过重未能应答。例如，Servlet可能在数据库连接池已满的情况下返回503。服务器返回503时可以提供一个 Retry-After头。</td>
</tr>
<tr>
<td>504</td>
<td>Gateway Timeout</td>
<td>由作为代理或网关的服务器使用，表示不能及时地从远程服务器获得应答。（HTTP 1.1新）</td>
</tr>
<tr>
<td>505</td>
<td>HTTP Version Not Supported</td>
<td>服务器不支持请求中所指明的HTTP版本。（HTTP 1.1新）</td>
</tr>
</tbody>
</table>
<p>HTTP状态码是可扩展的。HTTP应用程序不需要理解所有已注册状态码的含义，尽管那样的理解显而易见是很合算的。但是，应用程序必须了解由第一位数字指定的状态码的类型，任何未被识别的响应将被看作是该类型的x00状态，<i>有一个例外就是未被识别的响应不能缓存</i>。例如，如果客户端收到一个未被识别的状态码431，则可以安全的假定请求有错，并且它会对待此响应就像它接收了一个状态码是400的响应。在这种情况下，用户代理（user agent）应当把实体和响应一起提交给用户，因为实体很可能包括人可读的关于解释不正常状态的信息。</p>
<h3>参考链接</h3>
<p>http://blog.csdn.net/wuwenxiang91322/article/details/7936115</p>
<div class="copyright_con"><p>转载声明：</p><p>本文标题：<a title="" data-original-title="" href="http://www.zuojj.com/archives/124.html">HTTP状态码及对照表</a></p><p>本文链接：http://www.zuojj.com/archives/124.html，转载请注明转自<a title="" data-original-title="" href="http://www.zuojj.com">Benjamin-专注前端开发和用户体验</a></p></div>

      
	</article>