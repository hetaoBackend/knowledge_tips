---


---

<h1 id="kubernetes-权威指南">Kubernetes 权威指南</h1>
<p>使用Kubernetes就是在全面拥抱微服务架构。<br>
微服务架构的核心是将一个巨大的单体应用分解为很多小的互相连接的微服务，一个微服务背后可能有多个实例副本在支撑，副本的数量可能会随着系统的负荷变化而进行调整，内嵌的负载均衡器在这里发挥了重要作用。</p>
<p>master上运行Kubernetes API Server、Kubernetes Controller Manager、Kubernetes Scheduler</p>
<p>node上运行kubelet、kube-proxy、Docker Engine</p>
<p>一旦Node被纳入集群管理范围，kubelet进程就会定时向Master节点汇报自身的情报，这样master可以获知每个Node的资源使用情况，并实现高效均衡的资源调度策略。</p>
<pre><code>kubectl get nodes
kubectl describe node &lt;node_name&gt;
</code></pre>
<ul>
<li>Pod是Kubernetes的最基本单位，每个Pod都包含根容器Pause和其他业务容器，引入业务容器并且不易死亡的Pause作为Pod的根容器，以它的状态代表整个容器组的状态。</li>
<li>Pod里的多个业务容器共享Pause容器的IP，共享Pause容器挂接的Volume，这样简化了密切联系的业务容器之间的通信问题，也很好解决了他们之间的文件共享问题。</li>
<li>Kubernetes为每个Pod都分配了唯一的IP地址，称之为PodIP，一个Pod里的多个容器共享PodIP地址。Kubernetes要求底层网络支持集群之间任意两个Pod之间的TCP/IP直接通信，这通常采用虚拟二层网络技术实现，例如Flannel、Openvswitch等，因此在Kubernete中，一个Pod里的容器与另外一个主机上的Pod容器能够直接通信。</li>
<li>Pod其实有两种类型：普通Pod及静态Pod，后者比较特殊，它并不放在Kubernates的etcd存储中，而是存放在某个具体的Node上的一个具体文件中，并且只在此Node上启动运行。而普通的Pod一旦被创建，就会被放入到etcd中存储，随后会被Kubernetes Master调度到某个具体的Node上并进行绑定，随后该Pod被对应的Node上的kubelet进程实例化成一组相关的Docker容器并启动。</li>
<li>在默认情况下，当Pod中某个容器停止时，Kubernetes会自动检测到这个问题并且重新启动这个Pod（重启Pod里的所有容器），如果Pod所在的Node宕机，则会将这个Node上的所有Pod重新调度到其他节点上。</li>
</ul>
<h3 id="label">Label</h3>
<ul>
<li>Label是key=value的键值对，其中key与value由用户自己指定。Label可以附加到各种资源对象上，例如：Node、Pod、Service、RC等，一个资源对象可以定义任意数量的Label，同一个Label也可以被添加到任意数量的资源对象上去，Label通常在资源对象定义时确定，也可以在对象创建后动态添加或删除。</li>
<li>name = redis-slave</li>
<li>env != production</li>
<li>name in (redis-master, redis-slave)</li>
<li>name not in (php-frontend)</li>
<li>kube-controller进程通过资源对象RC上定义的LabelSelector来筛选要监控的Pod副本的数量，从而实现Pod副本的数量始终符合预期设定的全自动控制流程。</li>
<li>kube-proxy进程通过Service的Label Selector来选择对应的Pod，自动建立起每个Service到对应Pod的请求转发路由表，从而实现Service的智能负载均衡机制。</li>
<li>通过对某些Node定义特定的Label，并且在Pod定义文件中使用Node Selector这种标签调度策略，kube-scheduler进程可以实现Pod“定向调度”的特性。</li>
</ul>

