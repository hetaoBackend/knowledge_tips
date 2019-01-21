---


---

<p>Kubernetes中ingress与kube-proxy的关系</p>
<ul>
<li>ingress是Kubernetes向外提供微服务的一种方式，通过利用Nginx、Haproxy或Traefik等负载均衡器来暴露集群内服务的工具。</li>
<li>借助Kubernetes的Service机制，Service可以以标签的形式选定一组带有指定标签的Pod，并监控和自动负载他们的Pod IP，那么我们向外暴露只暴露Service IP就行了。这就是NodePort模式，即在每个节点上开起一个端口，然后转发到内部Pod IP上；</li>
<li>采用NodePort方式暴露服务面临一个坑爹的问题，服务一旦躲起来，NodePort在每个节点上开启的端口会及其庞大，而且难以维护；Nignx只监听一个端口，按照域名向后转发；</li>
<li>Ingress直接解析域名，并绕过kube-proxy，直接与Pod进行通信，依靠Service内部本身的负载均衡机制</li>
<li>一旦使用Ingress来实现负载分发的功能，Ingress Controller便将根据Ingress的规则设置将客户端请求直接转发到Service的后端Endpoint上，跳过kube-proxy设置的iptables转发规则。</li>
</ul>

