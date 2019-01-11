---


---

<h1 id="markdown-guide">MarkDown Guide</h1>
<h2 id="grammar">Grammar</h2>
<blockquote>
<p>Coding,net 为软件开发者提供基于云计算技术的软件开发平台，包括项目管理，代码托管，运行空间和质量控制等等。</p>
</blockquote>
<blockquote>
<h2 id="这是一个标题">这是一个标题</h2>
<ol>
<li>这是第一行列表项</li>
<li>这是第二行列表项</li>
</ol>
<p>给出一些例子代码：</p>
<p>return shell_exec(<code>echo $input | $markdown_script</code>);</p>
</blockquote>
<h3 id="列表">列表</h3>
<ul>
<li>Red</li>
<li>Green</li>
<li>Blue</li>
</ul>
<ol>
<li>Red</li>
<li>Green</li>
<li>Blue</li>
</ol>
<ul>
<li>Coding.net有一些主要功能：
<blockquote>
<p>代码托管平台</p>
</blockquote>
</li>
</ul>
<ul>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" disabled=""> 不勾选</li>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" disabled=""> 勾选</li>
</ul>
<pre class=" language-ruby"><code class="prism  language-ruby"><span class="token keyword">require</span> <span class="token string">'redcarpet'</span>
markdown <span class="token operator">=</span> <span class="token constant">Redcarpet</span><span class="token punctuation">.</span><span class="token keyword">new</span><span class="token punctuation">(</span><span class="token string">"Hello World!"</span><span class="token punctuation">)</span>
puts markdown<span class="token punctuation">.</span>to_html
</code></pre>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">import</span> math
<span class="token keyword">print</span><span class="token punctuation">(</span>math<span class="token punctuation">.</span>pi<span class="token punctuation">)</span>
</code></pre>
<p><em>Coding, 让开发更简单</em><br>
<em>coding, 让开发更简单</em></p>
<p><strong>hetao</strong><br>
<strong>hetao</strong></p>
<p><a>百度</a></p>
<hr>

<table>
<thead>
<tr>
<th>First Header</th>
<th>Second Header</th>
<th>Third Header</th>
</tr>
</thead>
<tbody>
<tr>
<td>Content Cell</td>
<td>Content Cell</td>
<td>Content Cell</td>
</tr>
<tr>
<td>Content Cell</td>
<td>Content Cell</td>
<td>Content Cell</td>
</tr>
</tbody>
</table><hr>

<table>
<thead>
<tr>
<th align="left">First Header</th>
<th align="center">Second Header</th>
<th align="right">Third Header</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left">Left</td>
<td align="center">Center</td>
<td align="right">Right</td>
</tr>
<tr>
<td align="left">Left</td>
<td align="center">Center</td>
<td align="right">Right</td>
</tr>
</tbody>
</table><hr>
<h3 id="indent">indent</h3>
<p>&amp;nbsp; can be used to show space<br>
tab can use four &amp;nbsp;</p>

