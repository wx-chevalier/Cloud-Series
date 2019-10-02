![](https://i.postimg.cc/8kvMhcZL/image.png)

# 虚拟化与云计算

在计算机科学中，虚拟化技术（Virtualization）是一种资源管理（优化）技术，将计算机的各种物理资源（e.g. CPU、内存以及磁盘空间、网络适配器等 IO 设备）予以抽象、转换，然后呈现出来的一个可供分割并任意组合为一个或多个（虚拟）计算机的配置环境。虚拟化技术打破了计算机内部实体结构间不可切割的障碍，使用户能够以比原本更好的配置方式来应用这些计算机硬件资源。而这些资源的虚拟形式将不受现有架设方式，地域或物理配置所限制。虚拟化技术是一个广义的术语，根据不同的对象类型可以细分为：

- 平台虚拟化（Platform Virtualization）：针对计算机和操作系统的虚拟化。

- 资源虚拟化（Resource Virtualization）：针对特定的系统资源的虚拟化，如内存、存储、网络资源等。

- 应用程序虚拟化（Application Virtualization）：包括仿真、模拟、解释技术等，如 Java 虚拟机（JVM）。

![虚拟化技术发展](https://s2.ax1x.com/2019/08/31/mx0hXn.jpg)

如 [DevOps 与 SRE 实战](https://ngte-be.gitbook.io/i/devops) 中所述，容器解除了开发和运维之间的隔阂，但同时也带来了一些挑战，比如频繁的发布变更如何控制，如何控制容器集群的行为，如何拆分应用到容器之中等。这是一个专门用于容器编排调度的工具呼之欲出，Kubernetes 的出现彻底改变了局面，可以说它直接改变了应用的基础架构。

![应用基础架构变迁](https://i.postimg.cc/fL83bjCV/image.png)

# 虚拟机

虚拟机由某些特定的硬件和内核虚拟化组成，运行客户操作系统。称为管理程序的软件创建虚拟化硬件，其可以包括虚拟磁盘，虚拟网络接口，虚拟 CPU 等。虚拟机还包括可以与此虚拟硬件通信的宾客内核。管理程序可以托管，这意味着它是一些在主机操作系统（MacOS）上运行的软件，如示例中所示。它也可以是裸机，直接在机器硬件上运行（替换你的操作系统）。无论哪种方式，管理程序方法都被认为是重量级的，因为它需要虚拟化多个部分（如果不是全部硬件和内核）。

![](https://i.postimg.cc/gcxWt8FX/image.png)

VM 需要硬件虚拟化才能实现机器级隔离，而容器则只需要在同一操作系统内进行隔离操作。 随着隔离空间数量的增加，开销差异变得非常明显。

# 容器

在过去几年里，云平台发展迅速，但其中困扰运维工程师最多的，是需要为各种迥异的开发语言安装相应的运行时环境。虽然自动化运维工具可以降低环境搭建的复杂度，但仍然不能从根本上解决环境的问题。

![](https://i.postimg.cc/W41KFcsF/image.png)

Docker 的出现成为了软件开发行业新的分水岭，容器技术的成熟也标志着技术新纪元的开启。Docker 提供了让开发工程师可以将应用和依赖封装到一个可移植的容器中的能力，这项举措使得 Docker 大有席卷整个软件行业并且进而改变行业游戏规则的趋势，这像极了当年智能手机刚出现时的场景——改变了整个手机行业的游戏规则。Docker 通过集装箱式的封装方式，让开发工程师和运维工程师都能够以 Docker 所提供的镜像分发的标准化方式发布应用，使得异构语言不再是捆绑团队的枷锁。

![](https://i.postimg.cc/V6R8yWsn/image.png)

容器是包含应用程序代码，配置和依赖关系的软件包，可提供运营效率和生产力。容器为我们提供了可预测的，可重复的和不可变的运行预期，容器的兴起是 DevOps 即服务的一个巨大推动因素，可以克服当今面临的最大安全障碍。容器化通过在操作系统级别进行虚拟化来使应用程序可移植，从而创建基于内核的隔离的封装系统。容器化的应用程序可以放在任何地方，无需依赖项运行或需要整个 VM，从而消除了依赖关系。

作为独立的单元，容器能够在任何主机操作系统，CentOS，Ubuntu，MacOS，甚至是像 Windows 这样的非 UNIX 系统中运行。容器还充当标准化的工作或计算单元。一个常见的范例是每个容器运行单个 Web 服务器，数据库的单个分片或单个 Spark 工作程序等，只需要扩展容器的数量就能够便捷地扩展应用。每个容器都有一个固定的资源配置（CPU，RAM，线程数等），并且扩展应用程序需要只扩展容器的数量而不是单个资源原语。当应用程序需要按比例放大或缩小时，这为工程师提供了更容易的抽象。容器也是实现微服务架构的一个很好的工具，每个微服务只是一组协作容器。例如，可以使用单个主容器和多个从容器来实现 Redis 微服务。

# Kubernetes 与编排

随着虚拟化技术的成熟和分布式架构的普及，用来部署、管理和运行应用的云平台被越来越多地提及。IaaS、PaaS 和 SaaS 是云计算的三种基本服务类型，分别表示关注硬件基础设施的基础设施即服务、关注软件和中间件平台的平台即服务，以及关注业务应用的软件即服务。容器的出现，使原有的基于虚拟机的云主机应用，彻底转变为更加灵活和轻量的容器与编排调度的云平台应用。

![](https://i.postimg.cc/6qxTzd39/image.png)

然而容器单元越来越散落使得管理成本逐渐上升，大家对容器编排工具的需求前所未有的强烈，Kubernetes、Mesos、Swarm 等为云原生应用提供了强有力的编排和调度能力，它们是云平台上的分布式操作系统。容器编排是通常可以部署多个容器以通过自动化实现应用程序的过程。像 Kubernetes 和 Docker Swarm 这样的容器管理和容器编排引擎，使用户能够指导容器部署并自动执行更新，运行状况监视和故障转移过程。

Kubernetes 是目前世界范围内关注度最高的开源项目，它是一个出色的容器编排系统，用于提供一站式服务。Kubernetes 出身于互联网行业巨头 Google，它借鉴了由上百位工程师花费十多年时间打造的 Borg 系统的理念，安装极其简易，网络层对接方式十分灵活。Kubernetes 和 Mesos 的出色表现给行业中各类工程师的工作模式带来了颠覆性的改变。他们再也不用关注每一台服务器，当服务器出现问题时，只要将其换掉即可。业务开发工程师不必再过分关注非功能需求，只需专注自己的业务领域即可。而中间件开发工程师则需要开发出健壮的云原生中间件，用来连接业务应用与云平台。

Kubernetes、Service Mesh 和 Serverless 三者共同演绎不同层次的封装和向上屏蔽下面的细节。Kubernetes 引入了不同的设计模式，实现对各种云资源全新、有效和优雅的抽象和管理模式，让集群的管理和应用发布变成了件相当轻松且不易出错的事。被广泛采用的微服务软件架构将分布式应用的各种复杂度迁移到了服务之间，如何通过全局一致、体系化、规范化和无侵入的手段进行治理就变成了微服务软件架构下至关重要的内容。Kubernetes 细化的应用程序的分解粒度，同时将服务发现、配置管理、负载均衡和健康检查等作为基础设施的功能，简化了应用程序的开发。而 Kubernetes 这种声明式配置尤其适合 CI/CD 流程，况且现在还有如 Helm、Draft、Spinnaker、Skaffold 等开源工具可以帮助我们发布 Kuberentes 应用。

![](https://i.postimg.cc/J0gGNr9m/image.png)

Service Mesh 通过将各服务所共用和与环境相关的内容剥离到部署于每个服务边上的 Sidecar 进程而轻松地做到了。这一剥离动作使得服务与平台能充分解耦而方便各自演进与发展，也使得服务变轻而有助于改善服务启停的及时性。Service Mesh 因为将那些服务治理相关的逻辑剥离到了 Sidecar 中且作为独立进程，所以 Sidecar 所实现的功能天然地支持多语言，为上面的服务采用多语言开发创造了更为有利的条件。通过 Service Mesh 对整个网络的服务流量进行技术收口，让异地多活这样涉及流量调度的系统工程实现起来更加优雅、简洁与有效，也能更加方便地实现服务版本升级时的灰度、回滚而改善安全生产质量。由于技术收口，给服务流量的治理和演进、排错、日志采集的经济性等疑难问题创造了新的发展空间。

# About

## Home & More | 延伸阅读

![技术视野](https://s2.ax1x.com/2019/09/30/uJWQTx.md.jpg)

您可以通过以下导航来在 Gitbook 中阅读笔者的系列文章，涵盖了技术资料归纳、编程语言与理论、Web 与大前端、服务端开发与基础架构、云计算与大数据、数据科学与人工智能、产品设计等多个领域：

- 知识体系：《[Awesome Lists | CS 资料集锦](https://ngte-al.gitbook.io/i/)》、《[Awesome CheatSheets | 速学速查手册](https://ngte-ac.gitbook.io/i/)》、《[Awesome Interviews | 求职面试必备](https://github.com/wx-chevalier/Awesome-Interviews)》、《[Awesome RoadMaps | 程序员进阶指南](https://github.com/wx-chevalier/Awesome-RoadMaps)》、《[Awesome MindMaps | 知识脉络思维脑图](https://github.com/wx-chevalier/Awesome-MindMaps)》、《[Awesome-CS-Books | 开源书籍（.pdf）汇总](https://github.com/wx-chevalier/Awesome-CS-Books)》

- 编程语言：《[编程语言理论](https://ngte-pl.gitbook.io/i/)》、《[Java 实战](https://ngte-pl.gitbook.io/i/java/java)》、《[JavaScript 实战](https://ngte-pl.gitbook.io/i/javascript/javascript)》、《[Go 实战](https://ngte-pl.gitbook.io/i/go/go)》、《[Python 实战](https://ngte-pl.gitbook.io/i/python/python)》、《[Rust 实战](https://ngte-pl.gitbook.io/i/rust/rust)》

- 软件工程、模式与架构：《[编程范式与设计模式](https://ngte-se.gitbook.io/i/)》、《[数据结构与算法](https://ngte-se.gitbook.io/i/)》、《[软件架构设计](https://ngte-se.gitbook.io/i/)》、《[整洁与重构](https://ngte-se.gitbook.io/i/)》、《[研发方式与工具](https://ngte-se.gitbook.io/i/)》

* Web 与大前端：《[现代 Web 全栈开发与工程架构](https://ngte-web.gitbook.io/i/)》、《[数据可视化](https://ngte-fe.gitbook.io/i/)》、《[iOS](https://ngte-fe.gitbook.io/i/)》、《[Android](https://ngte-fe.gitbook.io/i/)》、《[混合开发与跨端应用](https://ngte-fe.gitbook.io/i/)》

* 服务端开发实践与工程架构：《[服务端基础](https://ngte-be.gitbook.io/i/)》、《[微服务与云原生](https://ngte-be.gitbook.io/i/)》、《[测试与高可用保障](https://ngte-be.gitbook.io/i/)》、《[DevOps](https://ngte-be.gitbook.io/i/)》、《[Spring](https://github.com/wx-chevalier/Spring-Series)》、《[信息安全与渗透测试](https://ngte-be.gitbook.io/i/)》

* 分布式基础架构：《[分布式系统](https://ngte-infras.gitbook.io/i/)》、《[分布式计算](https://ngte-infras.gitbook.io/i/)》、《[数据库](https://github.com/wx-chevalier/Database-Series)》、《[网络](https://ngte-infras.gitbook.io/i/)》、《[虚拟化与云计算](https://github.com/wx-chevalier/Cloud-Series)》、《[Linux 与操作系统](https://github.com/wx-chevalier/Linux-Series)》

* 数据科学，人工智能与深度学习：《[数理统计](https://ngte-aidl.gitbook.io/i/)》、《[数据分析](https://ngte-aidl.gitbook.io/i/)》、《[机器学习](https://ngte-aidl.gitbook.io/i/)》、《[深度学习](https://ngte-aidl.gitbook.io/i/)》、《[自然语言处理](https://ngte-aidl.gitbook.io/i/)》、《[工具与工程化](https://ngte-aidl.gitbook.io/i/)》、《[行业应用](https://ngte-aidl.gitbook.io/i/)》

* 产品设计与用户体验：《[产品设计](https://ngte-pd.gitbook.io/i/)》、《[交互体验](https://ngte-pd.gitbook.io/i/)》、《[项目管理](https://ngte-pd.gitbook.io/i/)》

* 行业应用：《[行业迷思](https://github.com/wx-chevalier/Business-Series)》、《[功能域](https://github.com/wx-chevalier/Business-Series)》、《[电子商务](https://github.com/wx-chevalier/Business-Series)》、《[智能制造](https://github.com/wx-chevalier/Business-Series)》

此外，你还可前往 [xCompass](https://wx-chevalier.github.io/home/#/search) 交互式地检索、查找需要的文章/链接/书籍/课程；或者在 [MATRIX 文章与代码索引矩阵](https://github.com/wx-chevalier/Developer-Zero-To-Mastery)中查看文章与项目源代码等更详细的目录导航信息。最后，你也可以关注微信公众号：『**某熊的技术之路**』以获取最新资讯。