# travelweb
旅游网站
2020年5月27日 23:55 初次提交项目，完善了注册功能(验证码，邮箱激活)
html一般用户用户前台访问，而jsp一般用于工作人员后台操作，因为静态页面html比jsp速度快。
利用三层架构：web层 domain层 dao层
html -> servlet -> service -> dao -> 数据库
html提交注册表单，从servlet回来的数据，不能直接放在html中显示，
因为之前是用jsp的时候，可以用 request域或者session域可以保存这些数据并在jsp中显示一些错误的提示信息
那么在html中要想显示这些错误信息，我们就需要利用ajax 来完成表单提交
因为Ajax可以完成服务器和客户端的一个交互，将来如果注册失败了，可以在html页面给一些错误提示信息。

html 页面：使用js完成表单校验，使用Ajax 完成表单提交，注册成功，跳转到成功页面。
servlet作用：获取Ajax 提交的数据，将数据封装成User对象，调用service中方法，由service返回值来判定servlet的返回给Ajax的提示信息
service作用：由于被servlet的调用，其中service中有注册的方法，但是service也不知道该不该注册，所以先问问Dao有没有该用户 。
Dao 作用：dao说，我有两种方式，第一种，查看数据库中，有没有你要找的User，如果没有，Dao给service返回没有，这个时候service决策让Dao去
将这个新用户添加上，表示注册，Dao说OK，没问题，Dao就此调用了保存用户信息的方式，保存好了后，给service返回值，代表保存好了。
service收到信息后，回送给servlet，进而servlet告诉Ajax，当Ajax知道数据库中有此用户名，就会在html上显示说，此用户已注册，
反之，如果Ajax知道此用户是刚刚保存到数据库，进而跳转页面到注册成功。

表单提交分为：发送数据给服务器，跳转页面。
发送数据给服务器，在html中用Ajax，即异步提交数据，
提交表单是一个同步的过程，而我们异步操作不是提交表单，而是提交数据。
通过发送Ajax请求给服务器，看看用户是否存在，如果用户存在，我们就不提交表单，如果用户不存在，我们再提交表单。
注重js的学习以及jQuery，Ajax

因为用户名查询只能查询出一个对象，所以我们只需要queryForObject就好了

在注册过程中，会发生java.lang.NullPointerException: inStream parameter is null 这种错误，
解决办法：https://blog.csdn.net/nanhuaibeian/article/details/105451718
就是找不到druid.properties

犯了一个致命的错误：@WebServlet("activeUserServlet")  少些了一个"/"
Caused by: java.lang.IllegalArgumentException: Invalid <url-pattern> activeUserServlet in servlet mapping