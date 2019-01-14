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
<h3 id="replication-controller-rc">Replication Controller (RC)</h3>
<ul>
<li>RC 是 Kubernetes中一个期望的场景，即声明某种Pod的副本数量在任意时刻都符合某个预期值，所以RC的定义包括如下几个部分:
<ol>
<li>Pod 期待的副本数（replicas）</li>
<li>用于筛选目标Pod的Label Selector</li>
<li>当Pod的副本数量小于预期数量的时候，用于创建新Pod的Pod模板（template）</li>
</ol>
</li>
<li>当我们定义一个RC并提交到Kubernetes集群中以后，Master节点上的Controller Manager组件就得到通知，定期巡检系统中当前存活的目标Pod，并确保目标Pod实例的数量刚好等于此RC的期望值，如果有过多的Pod副本在运行，系统就会停掉一些Pod，否则系统就会再手动创建一些Pod。</li>
</ul>
<h3 id="deployment">Deployment</h3>
<ul>
<li>Deployment是为了更好地解决Pod的编排问题。</li>
<li>Deployment的典型应用场景有以下几个：
<ol>
<li>创建一个Deployment对象来生成对应的Replica Set并完成Pod副本的创建过程。</li>
<li>检查Deployment的状态来看部署动作是否完成（Pod副本的数量是否达到预期的值）。</li>
<li>更新Deployment以创建新的Pod</li>
<li>如果当前Deployment不稳定，则回滚到一个早先的Deployment版本</li>
<li>挂起或者恢复一个Deployment</li>
</ol>
</li>
</ul>
<h3 id="service">Service</h3>
<ul>
<li>Kubernetes的Service定义了一个服务的访问入口地址，前段的应用（Pod）通过这个入口地址访问其背后的一组由Pod副本组成的集群实例，Service与其后端Pod副本集群之间则是通过Label Selector来实现“无缝对接”的。而RC的作用实际上是保证Service的服务能力和服务质量始终处于预期的标准。</li>
<li>既然每个Pod都会分配一个单独的IP地址，而且每个Pod都提供一个独立的Endpoint(Pod IP + ContainerPort) 以被客户端访问，现在多个Pod副本组成一个集群来提供服务，会部署一个负载均衡器，为这组Pod开启一个对外的服务端口，并且将这些Pod的Endpoint列表加入服务端口的转发列表中，客户端就可以通过负载均衡器的对外IP地址+服务端口来访问此服务，而客户端的请求最后会被转发到哪个Pod，则由负载均衡器的算法决定。</li>
<li>运行在每个Node上的kube-proxy进程其实就是一个智能的软件负载均衡器，它负责把对Service的请求转发到后端的某个Pod实例上，并在内部实现服务的负载均衡与会话保持机制。</li>
<li>Kubernetes中，Service不是共用一个负载均衡器的IP地址，而是每个service分配一个全局唯一的虚拟IP地址，这个虚拟IP地址就成为ClusterIP。</li>
<li>Service一旦创建，它的clusterIP不会发生改变，Service的name和Service的ClusterIP地址做一个DNS域名映射即可。</li>
</ul>
<h3 id="kubernetes的服务发现机制">Kubernetes的服务发现机制</h3>
<ul>
<li>任何分布式系统都会涉及“服务发现”这个基础问题，大部分分布式系统通过提供特定的API接口来实现服务发现的功能，这样会导致平台的侵入性太强。</li>
<li>通过环境变量的形式来讲ClusterIP与Service进行绑定‘’</li>
<li>Node IP: Node节点的IP地址;</li>
<li>Pod IP: Pod的IP地址；</li>
<li>Cluster IP: Service的IP地址。</li>
<li>Node IP是kubernetes集群中每个节点的物理网卡的IP地址，这是一个真实存在的物理网络，所有属于这个网络的服务器之间都能通过这个网络直接通信，不管它们中是否有部分节点不属于这个Kubernetes集群。这也表明Kubernetes集群之外的节点访问Kubernetes集群之内的某个节点或者TCP/IP服务的时候，必须要通过NodeIP进行通信。</li>
<li>其次，Pod IP是每个Pod的IP地址，它是Docker Engine根据docker0网桥的IP地址段进行分配的，通常是一个虚拟的二层网络，Kubernetes要求位于不同Node上的Pod能够彼此直接通信，所以Kubernetes里一个Pod里的容器访问另外一个Pod里的容器，就是通过Pod IP所在的虚拟二层网络进行通信的，而真实的TCP/IP流量则是通过Node IP所在的物理网卡流出。</li>
<li>Cluster IP是一个虚拟的IP
<ol>
<li>Cluster IP仅仅作用于Kubernetes Service这个对象，并由Kubernetes管理和分配IP地址（来源于Cluster IP地址池）</li>
<li>Cluster IP无法被ping，因为没有一个“实体网络对象”来响应</li>
<li>Cluster IP只能结合Service Port组成一个具体的通信端口，单独的Cluster IP不具备TCP/IP通信的基础，并且它们属于Kubernetes集群这样一个封闭的空间，集群以外的节点如果要访问这个通信端口，则需要做一些额外工作。</li>
<li>在Kubernetes集群之内，Node IP网、Pod IP网与Cluster IP网之间的通信，采用的是Kubernetes自己设计的路由规则</li>
</ol>
</li>
<li>Service向外暴露
<ol>
<li>NodePort的方式，在Kubernetes集群里的每个Node上为需要外部访问的Service开启一个对应的TCP监听端口，外部系统只要用任意一个Node的IP地址+具体的NodePort端口号即可访问服务。</li>
<li>LoadBalancer的方式，Kubernetes会自动创建一个对应的Load balancer实例并返回它的IP地址供外部客户端使用。</li>
</ol>
</li>
</ul>
<h3 id="volume">Volume</h3>
<ul>
<li>Volume是Pod中能够被多个容器访问的共享目录，生命周期与Pod一致
<ol>
<li>emptyDir</li>
<li>hostPath</li>
<li>NFS</li>
</ol>
</li>
</ul>
<h3 id="persistent-volume">Persistent Volume</h3>
<ul>
<li>PV可以理解成Kubernetes集群中的某个网络存储中对应的一块存储，它与Volume很类似，但有以下区别：
<ol>
<li>PV只能是网路存储，不属于任何Node，但可以在每个Node上访问。</li>
<li>PV并不是定义在Pod上的。而是独立于Pod之外定义。</li>
<li>PV目前只有几种类型</li>
</ol>
</li>
</ul>
<h3 id="namespace">Namespace</h3>
<ul>
<li>Namespace（命名空间）是Kubernetes系统中的用于实现多租户的资源隔离。Namespace通过将集群内部的资源对象“分配”到不同的Namespace中，形成逻辑上分组的不同项目、小组或用户组，便于不同的分组在共享使用整个集群的资源的同事还能被分别管理。</li>
<li></li>
</ul>

