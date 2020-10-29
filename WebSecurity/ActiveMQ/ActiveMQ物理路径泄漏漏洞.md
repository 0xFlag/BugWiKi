<h1>ActiveMQ物理路径泄漏漏洞</h1>
<h2>一、漏洞简介</h2>
<p>Apache ActiveMQ默认消息队列61616端口对外，61616端口使用了OpenWire协议，这个端口会暴露服务器相关信息，这些相关信息实际上是debug信息。会返回应用名称，JVM，操作系统以及内核版本等信息。</p>
<h2>二、漏洞影响</h2>
<p>apache-activemq-5.14.0 to apache-activemq-5.14.5
  apache-activemq-5.15.0 to apache-activemq-5.15.2</p>
<h2>三、复现过程</h2>
<img src="https://github.com/0xFlag/BugWiKi/blob/main/WebSecurity/ActiveMQ/images/rId1.png"/>
