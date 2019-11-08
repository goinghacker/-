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

四. 什么是索引？
    
    是一种帮助mysql高效的获取数据的数据结构，这些数据结构以某种方式引用数据，这种结构就是索引。   
    
五. 对比一下B+树索引和 Hash索引？
      B+ Tree索引和Hash索引区别 哈希索引适合等值查询，但是不无法进行范围查询 哈希索引没办法利用索引完成排序 
      哈希索引不支持多列联合索引的最左匹配规则 如果有大量重复键值得情况下，哈希索引的效率会很低，因为存在哈希碰撞问题。
      
六. 聚簇索引和覆盖索引  聚簇索引和非聚簇索引的区别？

      聚簇索引是数据和索引文件是同一文件，常用于innodb中，在该索引实现方式中B+Tree的叶子节点上的data就是数据本身 
      非聚簇索引常用于myiSam中，索引文件和数据文件不在同一文件
      因为非聚簇索引一般需要先查询对应索引文件，再去查询数据文件，相对聚簇索引要慢，但当非局促索引用到覆盖索引时，
          就不需要回表查询；
