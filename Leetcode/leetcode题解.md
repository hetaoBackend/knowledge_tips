---


---

<h1 id="leetcode-题解">LeetCode 题解</h1>
<h2 id="leetcode-379">leetcode 379</h2>
<p>初始时有 <em>n</em> 个灯泡关闭。 第 1 轮，你打开所有的灯泡。 第 2 轮，每两个灯泡你关闭一次。 第 3 轮，每三个灯泡切换一次开关（如果关闭则开启，如果开启则关闭）。第 <em>i</em> 轮，每 <em>i</em> 个灯泡切换一次开关。 对于第 <em>n</em> 轮，你只切换最后一个灯泡的开关。 找出 <em>n</em> 轮后有多少个亮着的灯泡。</p>
<p>题解：<br>
&nbsp; &nbsp; &nbsp; &nbsp; 只有平方数才会操作奇数次，此时灯亮着</p>
<pre class=" language-python"><code class="prism  language-python"> <span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
       <span class="token keyword">def</span> <span class="token function">bulbSwitch</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> n<span class="token punctuation">)</span><span class="token punctuation">:</span>
           <span class="token triple-quoted-string string">"""
           :type n: int
           :rtype: int
           """</span>
           i <span class="token operator">=</span> <span class="token number">1</span>
           <span class="token keyword">while</span> i <span class="token operator">**</span> <span class="token number">2</span> <span class="token operator">&lt;=</span> n<span class="token punctuation">:</span>
   	        i <span class="token operator">+=</span> <span class="token number">1</span>
   	    <span class="token keyword">return</span> i <span class="token operator">-</span> <span class="token number">1</span>
</code></pre>
<h2 id="leetcode-687">leetcode 687</h2>
<p>给定一个二叉树，找到最长的路径，这个路径中的每个节点具有相同值。 这条路径可以经过也可以不经过根节点。</p>
<p><strong>注意</strong>：两个节点之间的路径长度由它们之间的边数表示。</p>
<p>题解：<br>
&nbsp; &nbsp; &nbsp; &nbsp; 通过变量来存储二叉树的路径长度，不断进行比较，一旦断路则清零重来</p>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    
    <span class="token keyword">def</span> <span class="token function">longestUnivaluePath</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> root<span class="token punctuation">)</span><span class="token punctuation">:</span>
        self<span class="token punctuation">.</span>ans <span class="token operator">=</span> <span class="token number">0</span>
        self<span class="token punctuation">.</span>_univaluePath<span class="token punctuation">(</span>root<span class="token punctuation">)</span>
        <span class="token keyword">return</span> self<span class="token punctuation">.</span>ans
    
    <span class="token keyword">def</span> <span class="token function">_univaluePath</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> root<span class="token punctuation">)</span><span class="token punctuation">:</span>
        <span class="token keyword">if</span> <span class="token operator">not</span> root<span class="token punctuation">:</span> <span class="token keyword">return</span> <span class="token number">0</span>
        l <span class="token operator">=</span> self<span class="token punctuation">.</span>_univaluePath<span class="token punctuation">(</span>root<span class="token punctuation">.</span>left<span class="token punctuation">)</span> <span class="token keyword">if</span> root<span class="token punctuation">.</span>left <span class="token keyword">else</span> <span class="token operator">-</span><span class="token number">1</span>
        r <span class="token operator">=</span> self<span class="token punctuation">.</span>_univaluePath<span class="token punctuation">(</span>root<span class="token punctuation">.</span>right<span class="token punctuation">)</span> <span class="token keyword">if</span> root<span class="token punctuation">.</span>right <span class="token keyword">else</span> <span class="token operator">-</span><span class="token number">1</span>
        pl <span class="token operator">=</span> l <span class="token operator">+</span> <span class="token number">1</span> <span class="token keyword">if</span> l <span class="token operator">&gt;=</span> <span class="token number">0</span> <span class="token operator">and</span> root<span class="token punctuation">.</span>val <span class="token operator">==</span> root<span class="token punctuation">.</span>left<span class="token punctuation">.</span>val <span class="token keyword">else</span> <span class="token number">0</span>
        pr <span class="token operator">=</span> r <span class="token operator">+</span> <span class="token number">1</span> <span class="token keyword">if</span> r <span class="token operator">&gt;=</span> <span class="token number">0</span> <span class="token operator">and</span> root<span class="token punctuation">.</span>val <span class="token operator">==</span> root<span class="token punctuation">.</span>right<span class="token punctuation">.</span>val <span class="token keyword">else</span> <span class="token number">0</span>
        self<span class="token punctuation">.</span>ans <span class="token operator">=</span> <span class="token builtin">max</span><span class="token punctuation">(</span>self<span class="token punctuation">.</span>ans<span class="token punctuation">,</span> pl <span class="token operator">+</span> pr<span class="token punctuation">)</span>
        <span class="token keyword">return</span> <span class="token builtin">max</span><span class="token punctuation">(</span>pl<span class="token punctuation">,</span> pr<span class="token punctuation">)</span>
</code></pre>

