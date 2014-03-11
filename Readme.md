#NodeJs学习 Express+jade+socket.io的聊天室
<p style="margin-top: 5px; margin-bottom: 5px; font-family: sans-serif; font-size: 16px; line-height: 24px;">
	&nbsp; &nbsp;聊天室页面不能刷新 刷新会断开连接 考虑解决方法
</p>
<p style="margin-top: 5px; margin-bottom: 5px; font-family: sans-serif; font-size: 16px; line-height: 24px;">
	&nbsp; &nbsp;聊天室中能保存100条信息
</p>
<p style="margin-top: 5px; margin-bottom: 5px; font-family: sans-serif; font-size: 16px; line-height: 24px;">
	&nbsp; &nbsp;本聊天室基于NodeJs+chrome浏览器完成
</p>
###笔记
<p style="margin-top: 5px; margin-bottom: 5px; font-family: sans-serif; font-size: 16px; line-height: 24px;">
	&nbsp; &nbsp;1.首先制作html页面,完成后转义成jade编码
</p>
<p style="margin-top: 5px; margin-bottom: 5px; font-family: sans-serif; font-size: 16px; line-height: 24px;">
	&nbsp; &nbsp; &nbsp; 聊天室的页面基本只有一个页面,使用的方式是连接时候显示登陆用户名界面,
</p>
<p style="margin-top: 5px; margin-bottom: 5px; font-family: sans-serif; font-size: 16px; line-height: 24px;">
	&nbsp; &nbsp; &nbsp; 检测用户名没有问题之后再将登陆界面hide,show出聊天室页面.
</p>
<p style="margin-top: 5px; margin-bottom: 5px; font-family: sans-serif; font-size: 16px; line-height: 24px;">
	&nbsp; &nbsp;2.完成界面之后,依据界面开发app.js,app.js中需要改造和express结合的socket.io
</p>
<p style="margin-top: 5px; margin-bottom: 5px; font-family: sans-serif; font-size: 16px; line-height: 24px;">
	&nbsp; &nbsp; &nbsp; 具体代码如下
</p>
<p style="margin-top: 5px; margin-bottom: 5px; font-family: sans-serif; font-size: 16px; line-height: 24px;">
	&nbsp; &nbsp; &nbsp; &nbsp; var server = http.createServer(app);
</p>
<p style="margin-top: 5px; margin-bottom: 5px; font-family: sans-serif; font-size: 16px; line-height: 24px;">
	&nbsp; &nbsp; &nbsp; &nbsp; var io = require('socket.io').listen(server);
</p>
<p style="margin-top: 5px; margin-bottom: 5px; font-family: sans-serif; font-size: 16px; line-height: 24px;">
	&nbsp; &nbsp; &nbsp; 拿到io对象这样就能对客户端进行操作了.
</p>
<p style="margin-top: 5px; margin-bottom: 5px; font-family: sans-serif; font-size: 16px; line-height: 24px;">
	&nbsp; &nbsp;3.页面中作为登陆用户名的表单需要使用客户端的socket.io将提交内容通知给服务器端的socket.io
</p>
<p style="margin-top: 5px; margin-bottom: 5px; font-family: sans-serif; font-size: 16px; line-height: 24px;">
	&nbsp; &nbsp; &nbsp; 客户端的socket对象获取方法为:
</p>
<p style="margin-top: 5px; margin-bottom: 5px; font-family: sans-serif; font-size: 16px; line-height: 24px;">
	&nbsp; &nbsp; &nbsp; &nbsp; 先导入socket.io.js库文件,然后 var socket = io.connect();即获得socket对象
</p>
<p style="margin-top: 5px; margin-bottom: 5px; font-family: sans-serif; font-size: 16px; line-height: 24px;">
	&nbsp; &nbsp; &nbsp; &nbsp; 用户名需要在客户端预先验证是否合法在传给后台.
</p>
<p style="margin-top: 5px; margin-bottom: 5px; font-family: sans-serif; font-size: 16px; line-height: 24px;">
	&nbsp; &nbsp; &nbsp; &nbsp; 用户名通过socket.on('username', usernameVal, callback)的方式通知服务器,并且创建一个用户名是否重名的回调函数
</p>
<p style="margin-top: 5px; margin-bottom: 5px; font-family: sans-serif; font-size: 16px; line-height: 24px;">
	&nbsp; &nbsp;4.服务器端的用户名使用一个数组保存,检测用户名是否重名.
</p>
<p style="margin-top: 5px; margin-bottom: 5px; font-family: sans-serif; font-size: 16px; line-height: 24px;">
	&nbsp; &nbsp; &nbsp; 将用户名保存在socket中,当连接断开的时候,将此用户删除
</p>
<p style="margin-top: 5px; margin-bottom: 5px; font-family: sans-serif; font-size: 16px; line-height: 24px;">
	&nbsp; &nbsp; &nbsp; 调用客户端的回调.创建成功就隐藏登陆,显示聊天室
</p>
<p style="margin-top: 5px; margin-bottom: 5px; font-family: sans-serif; font-size: 16px; line-height: 24px;">
	&nbsp; &nbsp;5.聊天室中的消息默认是保存100条,超过100条会shift掉之前的数据,这个数据是保存在数组中的
</p>
<p style="margin-top: 5px; margin-bottom: 5px; font-family: sans-serif; font-size: 16px; line-height: 24px;">
	&nbsp; &nbsp; &nbsp; *暂未解决的问题: html未转义,会被脚本侵入
</p>
<p style="margin-top: 5px; margin-bottom: 5px; font-family: sans-serif; font-size: 16px; line-height: 24px;">
	&nbsp; &nbsp;6.添加聊天室中登出的操作 添加button,监听click事件
</p>
