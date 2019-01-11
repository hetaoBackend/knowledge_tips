---


---

<h1 id="kubernetes-使用命令详解">Kubernetes 使用命令详解</h1>
<p>使用Kubernetes就是在全面拥抱微服务架构。<br>
微服务架构的核心是将一个巨大的单体应用分解为很多小的互相连接的微服务，一个微服务背后可能有多个实例副本在支撑，副本的数量可能会随着系统的负荷变化而进行调整，内嵌的负载均衡器在这里发挥了重要作用。</p>
<p>master上运行Kubernetes API Server、Kubernetes Controller Manager、Kubernetes Scheduler</p>
<p>node上运行kubelet、kube-proxy、Docker Engine</p>
<p>一旦Node被纳入集群管理范围，kubelet进程就会定时向Master节点汇报自身的情报，这样master可以获知每个Node的资源使用情况，并实现高效均衡的资源调度策略。</p>
<pre><code>kubectl get nodes
kubectl describe node &lt;node_name&gt;
</code></pre>
<p>Pod是Kubernetes的最基本单位，每个Pod都包含根容器Pause和其他业务容器</p>

