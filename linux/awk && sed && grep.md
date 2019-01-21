---


---

<h1 id="awk--sed--grep">awk &amp;&amp; sed &amp;&amp; grep</h1>
<p>awk、grep、sed是linux操作文本的三大利器，也是必须掌握的linux命令之一。三者的功能都是处理文本，但侧重点各不相同，其中属awk功能最强大，但也最复杂。grep最适合单纯的查找或匹配文本，sed更适合编辑匹配到的文本，awk更适合格式化文本，对文本进行较复杂格式处理。</p>
<h2 id="example">example</h2>
<p>test.log内容如下：</p>
<pre class=" language-txt"><code class="prism  language-txt">20170102 admin,password Open
20170801 nmask,nmask close
20180902 nm4k,test filter
</code></pre>
<h2 id="awk">awk</h2>
<p>AWK是一种处理文本文件的语言，是一个强大的文本分析工具；awk是以列为划分计数的，$0表示所有列，$1表示第一列，$2表示第二列。</p>
<h2 id="awk-参数">awk 参数</h2>
<ul>
<li>-F 指定输入文件折分隔符，如-F:</li>
<li>-v 赋值一个用户定义变量，如-v a=1</li>
<li>-f 从脚本文件中读取awk命令</li>
</ul>
<h2 id="分隔符">分隔符</h2>
<p>每行按空格分割列，并输出第1、4列</p>
<pre class=" language-shell"><code class="prism  language-shell">$ awk '{print $1,$4}' test.log

或者

$ cat test.log | awk '{print $1,$4}'
</code></pre>
<h2 id="自定义分隔符">自定义分隔符</h2>
<p>使用","进行分割，参数用-F</p>
<pre class=" language-shell"><code class="prism  language-shell">awk -F, '{print $1, $2}' test.log
</code></pre>
<p>使用多个分隔符，先使用空格分割，然后对分隔结果再使用“,”分隔</p>
<pre class=" language-shell"><code class="prism  language-shell">awk -F '[ ,]' '{print $1, $2, $3}' test.log
</code></pre>
<h2 id="设置变量">设置变量</h2>
<p>设置awk自定义变量，用参数-v</p>
<pre class=" language-shell"><code class="prism  language-shell">cat test.log | awk -v a=1 '{print $1, $1+a}'
</code></pre>
<p>注意：-v a之间要空格<br>
字符串拼接：（用“”而不是+）</p>
<pre class=" language-shell"><code class="prism  language-shell">cat test.log | awk -v a=\" '{print a""$0""a}'
</code></pre>
<h2 id="逻辑判断">逻辑判断</h2>
<p>输出第一列为20170801的记录</p>
<pre class=" language-shell"><code class="prism  language-shell">cat test.log | awk '$1==20170801 {print}'
</code></pre>
<p>输出第二列不是nmask,nmask的记录</p>
<pre class=" language-shell"><code class="prism  language-shell">cat test.log | awk '$2!="nmask,nmask" {print}'
</code></pre>
<h2 id="内建变量">内建变量</h2>
<p>NR参数：输出行号</p>
<pre class=" language-shell"><code class="prism  language-shell">cat test.log | awk '{print NR,$1,$2,$3}'
</code></pre>
<h2 id="正则表达式">正则表达式</h2>
<p>输出第二列中包括nm开头的所有记录</p>
<pre class=" language-shell"><code class="prism  language-shell">cat test.log | awk '$2 ~ /nm.*/ {print}'
</code></pre>
<p>输出包含2017开头的所有记录</p>
<pre class=" language-shell"><code class="prism  language-shell">cat test.log | awk '/2017.*/ {print}'
</code></pre>
<p>注意：这里没有~，因为没有指定是哪一列</p>
<h2 id="忽略大小写ingorecase1">忽略大小写{INGORECASE=1}</h2>
<pre class=" language-shell"><code class="prism  language-shell">cat test.log | awk '{IGNORECASE=1} /nmask/ {print}'
</code></pre>
<h2 id="匹配取反-">匹配取反 !~</h2>
<pre class=" language-shell"><code class="prism  language-shell">cat test.log | awk '$2 !~ /nmask/ {print}'
</code></pre>
<h2 id="内置函数">内置函数</h2>
<h3 id="substr字符串截取">substr字符串截取</h3>
<p>截取第一列的第一到第四个字符</p>
<pre class=" language-shell"><code class="prism  language-shell">cat test.log | awk '{print substr($1,1,4)}'
</code></pre>
<h3 id="split切分字符串">split切分字符串</h3>
<p>以逗号分隔第2列的数据，并输出第2列的内容</p>
<pre class=" language-shell"><code class="prism  language-shell">cat test.log | awk '{split($2,a,",");print a[1],a[2]}'
</code></pre>
<h3 id="gsub-替换">gsub 替换</h3>
<p>将第2列中的nmask替换成mMask</p>
<pre class=" language-shell"><code class="prism  language-shell">cat test.log | awk '{gsub("nmask","nMask",$2);print}'
</code></pre>
<h2 id="grep">grep</h2>
<p>linux grep命令用于查找文件里符合条件的字符串</p>
<h3 id="usage">usage</h3>
<ul>
<li>递归查询</li>
</ul>
<pre class=" language-shell"><code class="prism  language-shell">grep -r nmask /etc/
</code></pre>
<ul>
<li>查询取反</li>
</ul>
<pre class=" language-shell"><code class="prism  language-shell">grep -v test test.log
</code></pre>
<h2 id="sed">sed</h2>
<p>Linux sed命令是利用script来处理文本文件。</p>
<h3 id="参数">参数</h3>
<ul>
<li>-e 以选项中指定的script来处理输入的文本文件</li>
<li>-f 以选项中指定的script文件来处理输入的文本文件</li>
<li>-h 显示帮助</li>
<li>-n 仅显示script处理后的结果</li>
<li>-V 显示版本信息</li>
</ul>
<h3 id="动作">动作</h3>
<ul>
<li>a: 新增，a的后边可以接字符串，而这些字串会在下一行出现</li>
<li>i: 插入，i的后边可以接字串，而这些字串会在上一行出现</li>
<li>c: 取代，c的后边可以接字串，这些字串可以取代n1, n2之间的行</li>
<li>d: 删除</li>
<li>s: 取代，通常这个s的动作可以搭配正规表示法！如s/old/new/g</li>
</ul>
<h3 id="插入操作">插入操作</h3>
<p>在test.log文件的第4行后插入一行，内容为nmask</p>
<pre class=" language-shell"><code class="prism  language-shell">sed -e 4a\nmask test.log
</code></pre>
<h3 id="删除操作">删除操作</h3>
<p>删除test.log的第2行、第3行数据</p>
<pre class=" language-shell"><code class="prism  language-shell">cat test.log | sed '2,3d'
</code></pre>
<p>匹配删除，删除行中有nmask字符串的</p>
<pre class=" language-shell"><code class="prism  language-shell">nl test.log | sed '/nmask/d'
</code></pre>
<h3 id="替换操作">替换操作</h3>
<pre class=" language-shell"><code class="prism  language-shell">sed 's/要被取代的字符串/新的字符串/g'
</code></pre>

