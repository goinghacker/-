一. tcp三次握手四次挥手，为什么？

      一次握手:
      Client将标志位SYN置1，随机产生一个值seq=J,并将数据包发给Server 
      Client进入SYN_SENT状态，等待Server确认
      第二次握手:
      Server收到数据包后标志位SYN=1知道Client请求建立连接，Server将标志位SYN和ACK都置1，
      随机产生一个值,并将数据包发给Client确认连接请求，Server进入SYN_RCVD状态
      第三次握手:
      Client收到确认后若ACK为1，则将该数据包发送给Server，Server检查ACK为1则连接建立成功，
      Client与Server进入ESTABLISHED状态完成三次握手，可以传输数据

      第一次挥手：
      Clien发送一个FIN，用来关闭Client到Server的数据传送，Client进入FIN_WAIT_1状态。
      第二次挥手：
      Server收到FIN后，发送一个ACK给Client,Server进入CLOSE_WAIT状态。
      第三次挥手：
      Server发送一个FIN，用来关闭Server到Client的数据传送，Server进入LAST_ACK状态。
      第四次挥手：
      Client收到FIN后，Client进入TIME_WAIT状态，发送ACK给Server，Server进入CLOSED状态，完成四次握手。
   
二. PHP与nginx怎样通信的？

     Nginx通过监听端口找到需要访问的PHP文件，与fast-CGI建立连接，fast-CGI接收数据，PHP-fpm管理fast-CGI进程，挂了就重新启动，
     fast-CGI执行PHP程序，完成数据获取后通过该连接把数据返回给Nginx，Nginx返回给客户端
     
三. 常见的http状态码有哪些？分别发生的场景是什么？分别是怎么处理排查定位到这些状态码，并解决？

    403 （禁止） 服务器拒绝请求。例：没有权限去读取某个文件路径。（forbidden）
    404 （未找到） 服务器找不到请求的网页。例：请求的页面丢失。（not found）
    500 （服务器内部错误） 服务器遇到错误，无法完成请求.例：当PHP内存溢出，超出默认的设置内存值，会报500
    502 （错误网关） 服务器作为网关或代理，从上游服务器收到无效响应。例：Nginx配置错误，或者Nginx某个服务未开启。


