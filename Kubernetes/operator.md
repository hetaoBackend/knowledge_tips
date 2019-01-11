---


---

<h1 id="operator">Operator</h1>
<h2 id="overview">overview</h2>
<p>&nbsp; &nbsp; &nbsp; &nbsp; An Operator is a method of packaging, deploying and managing a Kubernetes application. A kubernetes application is an application that is  both deployed on Kubernetes and managed using the kubernetes APIs and kubectl tooling.<br>
&nbsp; &nbsp; &nbsp; &nbsp; To be able to make the most of Kubernetes, you need a set of cohensive APIs to extend in order to serve and manage your applications that run on Kubernetes. You can think of Operators as the runtime that manages this type of application on Kubernetes.</p>
<h2 id="the-operator-framework">The Operator Framework</h2>
<p>&nbsp; &nbsp; &nbsp; &nbsp; The Operator Framework is an open source project that provides developer and runtime Kubernetes tools, enabling you to accelerate the development of an Operator. The Operator Framework includes:</p>
<ul>
<li>Operator SDK<br>
Enables developers to build Operators based on their expertise without requiring knowledge of Kubernetes API complexities.</li>
<li>Operator Lifecycle Manager<br>
Oversees installation, updates, and management of the lifecycle of all of the operators (and their associated services) running across a Kubernetes cluster</li>
<li>Operator Metering<br>
Operator Metering (joining the coming months): Enable usage reporting for Operators that provide specialized services</li>
</ul>
<h2 id="build-with-the-operator-sdk">Build with the Operator SDK</h2>
<p>&nbsp; &nbsp; &nbsp; &nbsp; The SDK provides the tools to build, test and package Operators. Initially, the SDK facilitates the marriage of an application’s business logic (for example, how to scale, upgrade, or backup) with the Kubernetes API to execute those operations. Over time, the SDK can allow engineers to make applications smarter and have the user experience of cloud services. Leading practices and code patterns that are shared across operators are included in the SDK to help prevent reinventing the wheel.</p>
<hr>
<h2 id="lifecycle-of-an-operator">Lifecycle of an Operator</h2>
<p>&nbsp; &nbsp; &nbsp; &nbsp; Once built, Operator need to be deployed on a kubernetes cluster. The Operator Lifecycle Manager is the backplane that facilitates management of Operators on a Kubernetes cluster. With it, administrators can control what Operators are available in what namespaces and who can interact with running operators. They can also manage the overall lifecycle of operators and their resources, such as triggering updates to both an Operator and it’s resources.</p>

