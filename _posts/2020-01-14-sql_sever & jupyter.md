---
layout: post
title: "sql_server"
date: 2020-02-11
tag: sql
---





[jupyter && sql sever](https://docs.microsoft.com/zh-tw/sql/advanced-analytics/python/setup-python-client-tools-sql?view=sql-server-ver15)





## 安装 SQL Server 的硬件和软件要求

- 2019/07/24

适用对象：**是**SQL Server（仅限 Windows）

**以下注意事项适用于所有版本：**

- 我们建议在使用 NTFS 或 ReFS 文件格式的计算机上运行 SQL Server 。 支持但建议不要在使用 FAT32 文件系统的计算机上安装 SQL Server ，因为它没有 NTFS 或 ReFS 文件系统安全。
- SQL Server 安装程序将阻止在只读驱动器、映射的驱动器或压缩驱动器上进行安装。
- 如果通过远程桌面连接 RDC 客户端上本地资源中的介质来启动安装程序，安装将会失败。 若要执行远程安装，介质必须处于网络共享状态，或是物理计算机或虚拟机的本地介质。 SQL Server 安装介质要么处于网络共享状态，要么是映射的驱动器、本地驱动器，或者是虚拟机的 ISO。
- 安装 SQL Server Management Studio 时，必须先安装 .NET 4.6.1 必备组件。 SQL Server Management Studio 处于选中状态时，安装程序将自动安装 .NET 4.6.1。
- SQL Server 安装程序安装该产品所需的以下软件组件：
  - SQL Server Native Client
  - SQL Server 安装程序支持文件
- 有关在 Windows Server 2012 或 Windows 8 上安装 SQL Server 的最低版本要求，请参阅[在 Windows Server 2012 或 Windows 8 上安装 SQL Server](https://support.microsoft.com/kb/2681562)。

## 硬件和软件要求

以下要求适用于所有安装：

| 组件           | 要求                                                         |
| :------------- | :----------------------------------------------------------- |
| .NET Framework | SQL Server 2016 (13.x) RC1 和更高版本需要 .NET Framework 4.6 才能运行数据库引擎、Master Data Services 或复制。 SQL Server 安装程序自动安装 .NET Framework。 还可以从[适用于 Windows 的 Microsoft .NET Framework 4.6（Web 安装程序）](https://support.microsoft.com/kb/3045560)手动安装 .NET Framework。  SQL Server 2019 (15.x) 需要安装 .NET Framework 4.6.2。 可从[下载中心](https://www.microsoft.com/download/details.aspx?id=53344)获取  有关 .NET Framework 4.6 的详细信息、建议和指南，请参阅 [面向开发人员的 .NET Framework 部署指南](https://msdn.microsoft.com/library/ee942965(v=vs.110).aspx)。  在安装 .NET Framework 4.6 之前，Windows 8.1 和 Windows Server 2012 R2 需要 [KB2919355](https://support.microsoft.com/kb/2919355)。 |
| 网络软件       | SQL Server 支持的操作系统具有内置网络软件。 独立安装项的命名实例和默认实例支持以下网络协议：共享内存、命名管道、TCP/IP 和 VIA。  **注意：** 故障转移群集不支持 VIA 协议。 与 SQL Server 实例在同一故障转移群集节点上运行的客户端或应用程序可以使用 Shared Memory 协议，通过其本地管道地址连接到 SQL Server。 不过，这种连接无法感知群集，因此会在实例故障转移后无法连接。 因此，不建议使用这种连接，只能用于极个别的方案。  **重要提示：** 不推荐使用 VIA 协议。 此功能处于维护模式并且可能会在 Microsoft SQL Server 将来的版本中被删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。  有关网络协议和网络库的详细信息，请参阅 [Network Protocols and Network Libraries](https://docs.microsoft.com/zh-cn/sql/sql-server/install/network-protocols-and-network-libraries?view=sql-server-ver15)。 |
| 硬盘           | SQL Server 要求最少 6 GB 的可用硬盘空间。  磁盘空间要求将随所安装的 SQL Server 组件不同而发生变化。 有关详细信息，请参阅本文后面部分的[硬盘空间要求](https://docs.microsoft.com/zh-cn/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-ver15#HardDiskSpace) 。 有关支持的数据文件存储类型的信息，请参阅 [Storage Types for Data Files](https://docs.microsoft.com/zh-cn/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-ver15#StorageTypes)。 |
| 驱动器         | 从磁盘进行安装时需要相应的 DVD 驱动器。                      |
| 监视器         | SQL Server 要求有 Super-VGA (800x600) 或更高分辨率的显示器。 |
| Internet       | 使用 Internet 功能需要连接 Internet（可能需要付费）。        |

 备注

在虚拟机上运行 SQL Server 的速度要慢于在本机上运行，因为虚拟化有开销。



## 处理器、内存和操作系统要求

以下内存和处理器要求适用于所有版本的 SQL Server：

| 组件       | 要求                                                         |
| :--------- | :----------------------------------------------------------- |
| 内存*      | **最低要求：**  Express Edition：512 MB  所有其他版本：1 GB  **建议：**  Express Edition：1 GB  所有其他版本：至少 4 GB，并且应随着数据库大小的增加而增加来确保最佳性能。 |
| 处理器速度 | 最低要求：x64 处理器： 1.4 GHz  **建议：** 2.0 GHz 或更快    |
| 处理器类型 | x64 处理器：AMD Opteron、AMD Athlon 64、支持 Intel EM64T 的 Intel Xeon，以及支持 EM64T 的 Intel Pentium IV |

 备注

仅 x64 处理器支持 SQL Server 的安装。 x86 处理器不再支持此安装。

*内存至少必须有 2GB RAM，才能在“数据库引擎服务” (DQS) 中安装数据质量服务器组件。此要求不同于 SQL Server 的最低内存要求。 

## 硬盘空间要求

在安装 SQL Server的过程中，Windows Installer 会在系统驱动器中创建临时文件。 在运行安装程序以安装或升级 SQL Server之前，请检查系统驱动器中是否有至少 6.0 GB 的可用磁盘空间用来存储这些文件。 即使在将 SQL Server 组件安装到非默认驱动器中时，此项要求也适用。

实际硬盘空间需求取决于系统配置和您决定安装的功能。 下表提供了 SQL Server 各组件对磁盘空间的要求。

| **功能**                                                     | **磁盘空间要求** |
| :----------------------------------------------------------- | :--------------- |
| 数据库引擎 和数据文件、复制、全文搜索以及 Data Quality Services | 1480 MB          |
| 数据库引擎 （如上所示）带有 R Services（数据库内）           | 2744 MB          |
| 数据库引擎 （如上所示）带有针对外部数据的 PolyBase 查询服务  | 4194 MB          |
| Analysis Services 和数据文件                                 | 698 MB           |
| Reporting Services                                           | 967 MB           |
| Microsoft R Server （独立）                                  | 280 MB           |
| Reporting Services - SharePoint                              | 1203 MB          |
| 用于 SharePoint 产品的 Reporting Services 外接程序           | 325 MB           |
| 数据质量客户端                                               | 121 MB           |
| 客户端工具连接                                               | 328 MB           |
| Integration Services                                         | 306 MB           |
| 客户端组件（除 SQL Server 联机丛书组件和 Integration Services 工具之外） | 445 MB           |
| Master Data Services                                         | 280 MB           |
| 用于查看和管理帮助内容的SQL Server 联机丛书组件*             | 27 MB            |
| 所有功能                                                     | 8030 MB          |

*下载的联机丛书内容需要 200 MB 的磁盘空间。



## 在域控制器上安装 SQL Server

出于安全方面的考虑，我们建议您不要将 SQL Server 安装在域控制器上。 SQL Server 安装程序不会阻止在作为域控制器的计算机上进行安装，但存在以下限制：

- 在域控制器上，无法在本地服务帐户下运行 SQL Server 服务。

- 将 SQL Server 安装到计算机上之后，无法将此计算机从域成员更改为域控制器。 必须先卸载 SQL Server ，然后才能将主机计算机更改为域控制器。

- 将 SQL Server 安装到计算机上之后，无法将此计算机从域控制器更改为域成员。 必须先卸载 SQL Server ，然后才能将主机计算机更改为域成员。

- 在群集节点用作域控制器的情况下，不支持SQL Server 故障转移群集实例。

- 只读域控制器不支持 SQL Server。 SQL Server 安装程序不能在只读域控制器上创建安全组或设置 SQL Server 服务帐户。 在这种情况下，安装将失败。

   备注

  此限制也适用于域成员节点上的安装。

- 在仅可以访问只读域控制器的环境中不支持 SQL Server 故障转移群集实例。

   备注

  此限制也适用于域成员节点上的安装。





## 参考文档



https://docs.microsoft.com/zh-cn/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-ver15