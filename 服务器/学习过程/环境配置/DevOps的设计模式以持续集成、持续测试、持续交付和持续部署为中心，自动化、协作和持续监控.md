# DevOps的设计模式以持续集成、持续测试、持续交付和持续部署为中心，自动化、协作和持续监控是DevOps中使用的一些其他设计模式。


【持续集成】

持续集成是不断地将源代码集成到一个新的构建或发布的过程，源代码可以在本地存储中，也可以在GitHub或AWS CodeCommit中。

【持续测试】

连续测试新的构建或发布即持续测试，Jenkins之类的工具为持续测试提供了几个特性：在Jenkins的每个阶段都有用户去输入，它提供了一些插件，如Docker构建步骤插件，分别测试每个Docker应用阶段：运行容器、上传镜像、停止容器。

【持续交付】

持续交付为终端用户提供新的构建，以便在生产中部署，对于Docker应用，持续交付包括在Docker Hub或Amazon EC2容器等存储库中提供Docker镜像的每个新版本/标记。

【持续部署】

持续部署是不断地部署Docker镜像的最新版本，每当一个Docker镜像的新版本/标签可用时，Docker镜像就会被部署到生产环境中，Kubernetes 容器管理器已经提供了一些功能，如滚动更新，无需中断即可将Docker镜像升级到最新的服务，Jenkins滚动更新是自动化的，当Docker镜像的新版本/标签可用时，就会不断更新。

【持续监控】

持续监控可以监控正在运行应用的过程，类似于Sematext可以监控Docker应用，部署Sematext Docker代理来监控Kubernetes的集群指标并收集日志。

【自动化】

对于Docker应用，可以自动安装一些如Kubernetes这种非常复杂的工具，在其1.4版本中包含了名为Kubeadm的新工具，可以在Ubuntu和CentOS上自动安装Kubernetes上，但CoreOS上不支持Kubeadm工具。

【协作】

协作涉及到跨团队的工作和资源共享，如不同的开发团队可以在GitHub库中开发Docker镜像的不同版本代码，所有的Docker镜像标签都被构建并不断上传至Docker Hub，Jenkins提供了许多分支渠道项目，用于从GitHub存储库等存储库的多个分支中构建代码。
