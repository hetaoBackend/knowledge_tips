---


---

<h1 id="kubernetes">Kubernetes</h1>
<h2 id="重要概念">重要概念</h2>
<p>kubernetes，来源于希腊语，表示“舵手”</p>
<ul>
<li>kubernetes 是容器编排系统，是一个开源的平台，可以实现集群的自动化部署、自动扩缩容、维护等功能。可以在无力或虚拟机的kubernetes集群上运行容器化应用，kubernetes能提供一个以“容器为中心的基础架构”，满足在生产环境中运行应用的一些常见需求，如：
<ul>
<li>多个进程（作为容器运行）协同工作</li>
<li>存储系统挂载</li>
<li>Distributing secrets</li>
<li>应用健康检测</li>
<li>应用实例的复制</li>
<li>Pod自动伸缩/扩展</li>
<li>Naming and discovering</li>
<li>负载均衡</li>
<li>滚动更新</li>
<li>资源监控</li>
<li>日志访问</li>
<li>调试应用程序</li>
<li>提供认证和授权</li>
</ul>
</li>
</ul>
<h3 id="kubernetes重要组件">kubernetes重要组件</h3>
<ul>
<li>etcd: KV store</li>
<li>api server: 提供kubernetes api, 以RESTful接口方式提供给外部和内部组件调用，封装操作对象，并将操作对象持久化到etcd中。</li>
<li>scheduler: 集群的调度器，负责pod在集群节点中的调度分配。</li>
<li>controller-manager: 负责各种集群控制器的执行。</li>
<li>kubelet: 管理某节点上的pod生命周期，同时汇报node的相关信息。</li>
<li>kube-proxy: 提供网络代理和负载均衡，对应service，并根据service创建代理</li>
</ul>
<h3 id="namingspace">Namingspace</h3>
<ol>
<li>资源隔离的一种手段</li>
<li>不同NS中的资源不能相互访问</li>
<li>多租户的一种常见解决方案</li>
</ol>
<p>拥有名称，和Resource进行关联</p>
<h4 id="resource">Resource</h4>
<ul>
<li>概念
<ol>
<li>集群中的一种资源对象</li>
<li>处于某个命名空间中</li>
<li>可以持久化存储到Etcd中</li>
<li>资源是有状态的</li>
<li>资源是可以关联的</li>
<li>资源是可以限定使用配额</li>
</ol>
</li>
<li>属性
<ol>
<li>名称</li>
<li>类型</li>
<li>Label：用于选择</li>
<li>资源自定义模板</li>
<li>资源实例</li>
<li>资源生命周期</li>
<li>事件记录（events）</li>
<li>特定的一些动作</li>
</ol>
</li>
<li>关联
<ol>
<li>ResourceQuta</li>
<li>Namespace</li>
</ol>
</li>
</ul>
<p><strong>Kubernetes中几乎所有重要概念都是资源</strong></p>
<h4 id="label">Label</h4>
<ul>
<li>概念
<ol>
<li>一个key-value键值对</li>
<li>可以任意定义</li>
<li>可以贴在Resource对象上</li>
<li>用来过滤和选择某种资源</li>
</ol>
</li>
<li>属性
<ol>
<li>key、value</li>
</ol>
</li>
<li>关联
<ol>
<li>Resource</li>
<li>Label Selector</li>
</ol>
</li>
</ul>
<h3 id="master节点">Master节点</h3>
<ul>
<li>概念
<ol>
<li>Kubernetes集群的管理节点</li>
<li>负责集群的管理</li>
<li>提供集群的资源数据访问入口</li>
</ol>
</li>
<li>属性
<ol>
<li>Etcd存储服务</li>
<li>API Server进程</li>
<li>Controller Manager服务进程</li>
<li>Scheduler服务进程</li>
</ol>
</li>
<li>关联：
<ul>
<li>工作节点Node</li>
</ul>
</li>
</ul>
<h3 id="node">Node</h3>
<ul>
<li>概念
<ol>
<li>一个linux主机</li>
<li>Kubernetes中的工作节点（负载节点）</li>
<li>启动和管理Kubernetes中的pod实例</li>
<li>接受Master节点的管理指令</li>
<li>具有一定的自我修复能力</li>
</ol>
</li>
<li>属性
<ol>
<li>名称与IP</li>
<li>系统资源信息</li>
<li>运行Docker Engine服务</li>
<li>运行了Kubernetes的一个守护进程kubelet</li>
<li>运行了Kubernetes的负载均衡器kube-proxy</li>
<li>拥有状态</li>
</ol>
</li>
<li>关联
<ol>
<li>Master节点</li>
</ol>
</li>
</ul>

