# cross-domain-request-1  
#跨域请求解决方案一  window.name

##什么是同源
同源是指，域名，协议，端口相同

## 解决方案原理

name 在浏览器环境中是一个全局/window对象的属性，且当在 frame 中加载新页面时，name 的属性值依旧保持不变。通过在 iframe 中加载一个资源，该目标页面将设置 frame 的 name 属性。此 name 属性值可被获取到，以访问 Web 服务发送的信息。但 name 属性仅对相同域名的 frame 可访问。这意味着为了访问 name 属性，当远程 Web 服务页面被加载后，必须导航 frame 回到原始域。同源策略依旧防止其他 frame 访问 name 属性。一旦 name 属性获得，销毁 frame 。

window对象的name属性是一个很特别的属性，当该window的location变化，然后重新加载，它的name属性可以依然保持不变。
依此原理，我们可以在页面A中用iframe加载其他域的页面B，而页面B中用JavaScript把需要传递的数据赋值给 window.name，页面A的iframe加载完成之后，页面A修改iframe的地址，将其变成同域的一个地址，然后就可以读出window.name的值了。
## 解决方案优点

1. 它是安全的。也就是说，它和其他的基于安全传输的 frame 一样安全，例如 Fragment Identifier messaging （FIM）和 Subspace。(I)Frames 也有他们自己的安全问题，由于 frame 可以改变其他 frame 的 location，但是这个是非常不同的安全溢出，通常不太严重。
2. 它比 FIM 更快，因为它不用处理小数据包大小的 Fragment Identifier ，并且它不会有更多的 IE 上的“机关枪”声音效果。它也比 Subspace 快，Subspace 需要加载两个 Iframe 和两个本地的 HTML 文件来处理一个请求。window.name 仅需要一个 Iframe 和一个本地文件。
3. 它比 FIM 和 Subspace 更简单和安全。FIM 稍微复杂，而 Subspace 非常复杂。Subspace 也有一些额外的限制和安装要求，如预先声明所有的目标主机和拥有针对若干不同特殊主机的 DNS 入口。window.name 非常简单和容易使用。
4. 它不需要任何插件（比如 Flash）或者替代技术（例如 Java）。

## DEMO说明
文件夹a和b是两个不同的服务器（端口号不同），a服务器上的public文件夹中的app.html要请求b服务器中的public文件夹下的data.html中的数据，实现方式见app.html。

## 使用方式
1. 分别在a文件夹下和b文件夹下执行 npm install
2. 分别启动服务器 npm start
3. a服务器端口号是3000，b服务器端口号为4000
4. 访问localhost:3000/app.html

## 参考文章
http://blog.csdn.net/bao19901210/article/details/21458001

http://bbs.blueidea.com/thread-3085629-1-1.html

http://www.planabc.net/2008/09/01/window_name_transport/
