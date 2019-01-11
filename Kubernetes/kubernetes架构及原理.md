---


---

<h1 id="kubernetes架构及原理">Kubernetes架构及原理</h1>
<h2 id="架构图">架构图</h2>
<p><img src="https://github.com/hetaoBackend/knowledge_tips/raw/master/Kubernetes/picture/kubernetes_arch.png" alt="avatar"></p>
<h2 id="网络机制">网络机制</h2>
<ul>
<li>Proxy-IP: 代理层公网地址IP，外部访问应用的网管服务器。【实际需要关注的IP】</li>
<li>Service-IP: Service的固定虚拟IP，Service-IP是内部，外部无法寻址到</li>
<li>Node-IP: 容器宿主机的主机IP</li>
<li>Container-Bridge-IP: 容器网桥 (docker0) IP，容器的网络都需要通过容器网桥转发</li>
<li>Pod-IP: Pod的IP，等效于Pod中网络容器的Container-IP</li>
<li>Container-IP: 容器的IP，容器的网络是个隔离的网络空间</li>
</ul>
<h3 id="同一个node内的两个pod之间的通信">同一个Node内的两个pod之间的通信</h3>
<p><img src="https://github.com/hetaoBackend/knowledge_tips/raw/master/Kubernetes/picture/node_contact.png" alt="avatar"></p>
<h3 id="不同node内的两个pod之间的通信">不同Node内的两个pod之间的通信</h3>
<p><img src="https://github.com/hetaoBackend/knowledge_tips/raw/master/Kubernetes/picture/node_contact_node.png" alt="avatar"></p>
<h3 id="通过service向外界提供服务">通过service向外界提供服务</h3>
<p><img src="https://github.com/hetaoBackend/knowledge_tips/raw/master/Kubernetes/picture/net_arch.png" alt="avatar"></p>
<h3 id="通过nodeport向外界提供服务">通过NodePort向外界提供服务</h3>
<p><img src="https://github.com/hetaoBackend/knowledge_tips/raw/master/Kubernetes/picture/nodePort.png" alt="avatar"></p>

