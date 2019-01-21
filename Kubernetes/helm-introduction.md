---


---

<h1 id="helm-introduction">Helm Introduction</h1>
<h2 id="helm-工作原理">Helm 工作原理</h2>
<h3 id="基本概念">基本概念</h3>
<p>Helm 的三个基本概念</p>
<ol>
<li>Chart: Helm应用（package），包括该应用的所有 Kubernetes manifest 模板，类似于 YUM RPM 或 Apt dpkg文件</li>
<li>Repository: Helm package 存储仓库</li>
<li>Release：chart的部署实例，每个chart可以部署一个或多个release</li>
</ol>
<h3 id="工作原理">工作原理</h3>
<p>Helm包括两个部分，helm客户端和tiller服务端。</p>
<h4 id="helm-客户端">Helm 客户端</h4>
<p>helm客户端是一个命令行工具，负责管理 charts、repository和release。它通过gRPC API（使用kubectl port-forward 将tiller的端口映射到本地，然后在通过映射后的端口跟tiller通信）向 tiller 发送请求，并由tiller来管理对应的 Kubernetes 资源。</p>
<h4 id="tiller-服务端">tiller 服务端</h4>
<p>tiller 接收来自 helm 客户端的请求，并把相关资源的操作发送到Kubernetes，负责管理（安装、查询、升级或删除等）和跟踪Kubernetes资源。为了方便管理，tiller 把 release 的相关信息保存在 kubernetes 的 ConfigMap中。<br>
tiller 对外暴露 gRPC API，供 helm 客户端调用。</p>
<h3 id="helm-charts">Helm Charts</h3>
<p>Helm 使用 Chart 来管理 Kubernetes manifest 文件。每个 chart 都至少包括</p>
<ol>
<li>应用的基本信息 Chart.yaml</li>
<li>一个或多个Kubernetes manifest 文件模板（放置在templates/目录中），可以包括Pod、Deployment、Service等各种Kubernetes资源</li>
</ol>
<h3 id="helm-命令参考">Helm 命令参考</h3>
<ol>
<li>查询 charts
<ul>
<li>helm search</li>
<li>helm search mysql</li>
</ul>
</li>
<li>查询package 详细信息
<ul>
<li>helm inspect stable/mariadb</li>
</ul>
</li>
<li>部署 package
<ul>
<li>helm install stable/mysql</li>
</ul>
</li>
<li>查询服务（Release）列表
<ul>
<li>helm ls</li>
<li>helm status quieting-warthog</li>
</ul>
</li>
<li>升级和回滚release
<ul>
<li>helm upgrade -f panda.yaml happy-panda stable/mariadb</li>
<li>helm rollback happy-panda 1</li>
</ul>
</li>
<li>删除release
<ul>
<li>helm delete quieting-wartog</li>
</ul>
</li>
<li>repo 管理
<ul>
<li>helm repo add …</li>
<li>helm repo list</li>
<li>helm repo index</li>
</ul>
</li>
<li>chart 管理
<ul>
<li>helm create deis-workflow</li>
<li>helm init</li>
<li>helm package deis-workflow</li>
</ul>
</li>
</ol>

