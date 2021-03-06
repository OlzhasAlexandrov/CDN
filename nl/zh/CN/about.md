---

copyright:
  years: 2017, 2018
lastupdated: "2018-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# 关于 Content Delivery Network (CDN)

Content Delivery Network (CDN) 是边缘服务器的集合，这些服务器在国家/地区或世界的各个部分进行分布。Web 内容会通过其所在地理区域与请求内容的客户最近的边缘服务器来提供。通过此项技术，最终用户收到内容的延迟时间缩短，为客户交付更好的总体体验。

## CDN 如何工作？

CDN 通过在世界各地的边缘服务器上高速缓存 Web 内容来达成其目的。当客户请求 Web 内容时，内容请求会路由到地理位置与该客户最近的边缘服务器。通过减少内容必须传输的距离，CDN 提供最优的吞吐量、最短的等待时间和提高的性能。使用基于 Akamai 的 IBM Cloud Content Delivery Network，内容提供商能以最少的配置实现在全球各地高效传递请求的内容。

IBM Cloud Content Delivery Network 服务包含以下主要功能：
  * 主机服务器源支持
  * Object Storage 源支持
  * 支持具有非重复路径的多个源
  * 基于路径的 CDN 映射
  * 清除高速缓存的内容
  * 生存时间 (TTL)
  * 使用图形视图查看度量
  * 具有通配符证书 的 HTTPS 支持
  * 主机头支持
  * 提供旧内容
  * “忽略高速缓存键中的查询自变量”功能
  * 内容压缩
  * 大型文件优化
  * 视频点播

## 功能描述

### 主机服务器源支持

通过提供源主机名、协议、端口号以及可选的提供内容的路径，IBM Cloud Content Delivery Network (CDN) 可以配置为从主机服务器源提供内容。缺省路径为“/\*”。协议可以为 HTTP 和/或 HTTPS。Akamai 仅支持特定端口号。请参阅[常见问题及解答](faqs.html#are-there-any-restrictions-on-what-http-and-https-port-numbers-are-allowed-for-akamai-)，以获取支持的端口号/范围。目前，HTTPS 是使用通配符证书支持的，这意味着服务只能通过以 `.cdnedge.bluemix.net` 结尾的 CNAME 进行访问。请参阅[使用通配符证书支持的 HTTPS](about.html#https-with-wildcard-certificate-) 功能描述，以获取更多信息。

### Object Storage 源支持

通过提供_端点_、_存储区名称_、_协议_和_端口_，IBM Cloud CDN 可以配置为从 Object Storage 端点提供内容。（可选）可以指定文件扩展名列表，以仅允许对具有这些扩展名的文件进行高速缓存。存储区中的所有对象都需要设置有匿名读访问权或公共读访问权。有关[如何使用 CDN 设置 IBM Bluemix Object Storage](https://console.bluemix.net/docs/tutorials/static-files-cdn.html#accelerate-delivery-of-static-files-using-a-cdn) 的此教程提供了更多详细信息。

### 支持具有非重复路径的多个源

在某些情况下，您可能想要从不同的源服务器传递某些内容。例如，您可能需要不同源服务器提供的某些照片或视频。IBM Cloud CDN 提供了用于使用多个路径设置多个源服务器的选项。此选项支持灵活使用数据存储方式和存储位置。为源服务器提供的路径对于 CDN 应该唯一。源服务器本身并不需要唯一。

### 基于路径的 CDN 映射

通过在创建 CDN 时提供路径，可以将 IBM Cloud CDN 服务限制于源服务器上的特定目录路径。最终用户只能访问该目录路径中的内容。例如，如果使用“/videos”路径创建了 CDN www.example.com，那么只能通过 `www.example.com/videos/` 对其进行访问。

### 清除高速缓存的内容

IBM Cloud CDN 提供了方便快捷地从边缘服务器中除去或“清除”高速缓存内容的功能。目前清除只能用于文件路径。目前，使用 Akamai 实施的清除会在大约 5 秒内清除文件。该 UI 还提供了查看清除历史记录以及将特定清除路径标记为收藏夹的功能。

### 生存时间 (TTL)

生存时间指示边缘服务器将对该特定文件或目录路径的内容进行高速缓存的时间量（以秒为单位）。首次创建 CDN 时，将为路径（“/\*”）创建全局生存时间 (TTL)，缺省时间为 3600 秒。TTL 的最小值为 30 秒，最大值为 2147483647 秒。对于每个条目，TTL 路径对于 CDN 都应该唯一。如果多个路径与一个给定内容相匹配，那么将向该内容应用最近配置的路径匹配项。例如，假设有两个 TTL，先创建了 `/example/file`，生存时间值为 3000 秒，随后创建了 `/example/*`，生存时间值为 4000 秒。虽然 `/example/file` 更具体，但因为 `/example/*` 是最近创建的，所以 `/example/file` 的 TTL 为 4000 秒。创建 TTL 条目后，可以针对路径和/或时间对其进行编辑。也可以将其删除。

### 使用图形视图查看度量

单个 CDN 的度量在该 CDN 映射的客户门户的“概览”选项卡上提供。根据 CDN 的使用情况计算两种类型的度量：一种以图形显示一段时间内度量；一种显示为汇总值。

对于以图形显示一段时间内变化的度量，可以看到三个折线图和一个饼图。三个折线图是：**带宽**、**命中数（按映射）**和**命中数（按类型）**。折线图显示在指定时间范围内每天的活动。**带宽**和**命中数（按映射）**是单折线图，而**命中数（按类型）**的细分会针对提供的每种命中类型显示一条折线。饼图以百分比形式显示 CDN 映射带宽的区域性细分。

为汇总值显示的度量包括**带宽用量** (GB)、对 CDN 边缘服务器的**命中总数**以及**命中率**。命中率指示由边缘服务器传递内容次数的百分比，而不是通过其源传递次数的百分比。目前，命中率显示为所有 CDN 映射的函数，而不仅仅是正在查看的映射。

缺省情况下，汇总数字和图表缺省为显示最近 30 天的度量，但您可以通过[客户门户网站 ![外部链接图标 ](../../icons/launch-glyph.svg "外部链接图标 ")](https://control.softlayer.com/) 更改此值。两个类别都能够显示 7 天、15 天、30 天、60 天或 90 天时间段的度量。

### 具有通配符证书 的 HTTPS 支持

通配符证书是将 Web 内容安全地交付到终端用户的一种最经济的方法。配置 CDN 或源路径时，通过选择 `HTTPS 端口`可启用此功能。在使用通配符证书对 HTTPS 启用 CDN 映射后，边缘服务器会通过 HTTPS 联系源服务器。如果源服务器指定为主机名，那么缺省情况下，边缘服务器会使用源主机名作为服务器名称指示 (SNI) 头，与源服务器进行传输层安全性 (TLS) 协商。但是，如果源服务器指定为 IP 地址，那么 CDN 的主机名将会用作 SNI 头。源证书必须由认可的认证中心 (CA) 签署。

使用通配符证书时，**仅**最终用户有权使用 CNAME 来访问服务。例如，如果域为 `example.com`，并且 CNAME 为 `example.cdnedge.bluemix.net`，那么**只能**通过 `https://example.cdnedge.bluemix.net` 来访问 CDN 服务。请参阅[常见问题及解答](faqs.html#what-should-be-the-expected-behavior-when-loading-the-cname-or-hostname-on-your-browser-for-the-supported-cdn-protocols-)，以了解将 HTTPS 与通配符证书配合使用的含义。

作为行业最佳实践，Akamai 只信任根证书，而不信任中间证书，因为信任的中间证书集会频繁更改。出于安全目的，Akamai 仅包含 Akamai 信任库中的根证书认证中心。因此，源必须将包括叶证书和所有中间证书（不包括根证书）在内的整个证书链，作为与边缘服务器的 SSL 握手的一部分发送。您可以在[此处](https://community.akamai.com/docs/DOC-4447-ssltls-certificate-chains-for-akamai-managed-certificates)找到 Akamai 信任的证书。

### 主机头支持

边缘服务器与源主机通信时会使用主机头。此功能为源主机上的 Web 服务配置方式提供了灵活性。如果未提供主机头输入，那么将源服务器指定为主机名（而不是 IP 地址）时，服务会将源服务器主机名作为缺省 HTTP 主机头。如果主机头没有作为输入提供，并且源服务器作为 IP 地址提供，那么 CDN 主机名（也称为 CDN 域名）会用作缺省 HTTP 主机头。

### 遵守头

“遵守头”选项支持源中的 HTTP 头配置覆盖相应的 CDN 配置。缺省情况下，此功能已开启，但可以将其关闭。

### 提供旧内容

CDN 边缘服务器收到用户请求，并且未对请求的内容高速缓存时，边缘服务器会联系源主机以访存该内容。然后会将该内容高速缓存为该内容指定的生存时间 (TTL) 持续时间。如果在 TTL 到期后收到用户请求，边缘服务器会联系源主机以访存该内容。如果出于某种原因（例如，源主机停止运行或发生网络问题）而无法访问源服务器，那么边缘服务器会向请求提供到期（旧）内容。此功能由 Akamai 支持，并且**不能**关闭。

### “忽略高速缓存键中的查询自变量”功能

Akamai 边缘服务器在所谓的“高速缓存存储”上高速缓存内容。要使用“高速缓存存储”中的内容，边缘服务器会使用“高速缓存键”。通常，高速缓存键是基于最终用户的 URL 的一部分生成的。在某些情况下，URL 包含的查询函数自变量对于各个用户不同，但传递的内容是相同的。缺省情况下，Akamai 会使用查询函数的自变量来生成高速缓存键，因此会为每个用户生成唯一的高速缓存键。这并不是最佳方法，因为它会导致边缘服务器联系源服务器以使用其他高速缓存键来获取已高速缓存的内容。**忽略高速缓存键中的查询自变量**功能支持指定生成高速缓存键时应该忽略的查询自变量。此功能适用于 CDN 映射配置的`创建`或`更新`，也适用于源路径的`创建`或`更新`。

**注：**高速缓存键查询自变量可以在创建 CDN 映射后在“设置”选项卡进行配置。对于源路径，可以在源路径`创建`或`更新`期间进行配置。

### 内容压缩

缺省情况下，在 Akamai CDN 中针对以下内容类型已启用内容压缩：
* text/html*
* text/css*
* text/xml*
* text/json
* text/javascript*
* text/plain*
* application/x-javascript*
* application/json
* application/xml*

压缩由边缘服务器进行处理时，内容必须至少为 10 kB。在某些情况下，压缩由源服务器负责处理，在这种情况下，要压缩的文件大小没有限制。如果内容已经由源服务器进行压缩，那么不会再次对其进行压缩。要启用内容压缩，请求头必须定义 `Accept-Encoding: gzip`。

### 大型文件优化

通过大型文件优化，CDN 网络可以优化大于 10 MB 的内容传递。此支持可提高大型文件的性能，并减少等待时间和下载时间。如果不使用此功能，CDN 传递的文件大小不能超过 1.8 GB。此功能支持下载大于 1.8 GB 但不超过 320 GB 的文件。

要使大型文件优化生效，**必须**在源服务器上启用字节范围请求。Akamai CDN 针对此优化采用的技术称为“部分对象高速缓存”。请求大型文件时，边缘服务器会检查文件是否符合大小要求。这意味着向源服务器请求的大于 10 MB 的文件将以区块形式提供。区块到达边缘服务器后，会对其进行高速缓存并立即提供给用户。与此同时，边缘服务器将预取下一个区块，从而减少等待时间。此过程会一直持续，直到检索完整个文件或连接终止。  

启用此功能后，与提供小于 10 MB 的内容关联的性能成本会略有下降。因此，建议此功能仅用于提供大型文件。一个典型的用例是在 CDN 配置中创建新的源路径，并为该路径启用大型文件优化。

### 视频点播

**视频点播**性能优化能够跨多种网络类型提供高质量流。通过利用分布式网络的动态负载分配功能，基于 Akamai 的 IBM Cloud CDN 支持您针对大批受众迅速进行扩展，不管您是否计划过这样做。

**视频点播**针对 HLS、DASH、HDS 和 HSS 等分段流格式的分发进行了优化。目前，**不**支持实时视频流。您可以通过从“设置”选项卡上**优化对象**下的下拉菜单中选择**视频点播**选项来启用此功能，或者在创建新的源路径期间启用此功能。仅当优化视频文件的传递时才应启用此功能。
