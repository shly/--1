# cross-domain-request-1  
#跨域请求解决方案一  window.name

##什么是同源
同源是指，域名，协议，端口相同

## 解决方案原理
window对象的name属性是一个很特别的属性，当该window的location变化，然后重新加载，它的name属性可以依然保持不变。
依此原理，我们可以在页面A中用iframe加载其他域的页面B，而页面B中用JavaScript把需要传递的数据赋值给 window.name，页面A的iframe加载完成之后，页面A修改iframe的地址，将其变成同域的一个地址，然后就可以读出window.name的值了。

## DEMO说明
文件夹a和b是两个不同的服务器（端口号不同），a服务器上的public文件夹中的app.html要请求b服务器中的public文件夹下的data.html中的数据，实现方式见app.html。

## 使用方式
1 分别在a文件夹下和b文件夹下执行 npm install
2 分别启动服务器 npm start
3 a服务器端口号是3000，b服务器端口号为4000
4 访问localhost:3000/app.html

## 参考文章
http://blog.csdn.net/bao19901210/article/details/21458001

http://bbs.blueidea.com/thread-3085629-1-1.html
