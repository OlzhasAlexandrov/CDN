---

copyright:
  years: 2017
lastupdated: "2017-10-03"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# 벤더 컨테이너
`SoftLayer_Container_Network_CdnMarketplace_Vendor` 콜렉션에는 벤더 API에서 이용하는 속성이 포함됩니다. 


클래스 `SoftLayer_Container_Network_CdnMarketplace_Vendor`  
* `vendorName`: 현재 IBM Cloud CDN 제공자의 이름입니다.  
* `featureSummary`: 벤더 기능에 대한 간단한 요약입니다.  
* `features`: 벤더에서 지원하는 기능 목록입니다.  
* `status`: 벤더가 IBM Cloud에서 사용 가능한 옵션인지 여부를 표시합니다.


`listVendors` API에 대한 호출을 사용하여 기능 뿐만 아니라 사용 가능한 벤더 목록을 표시합니다.

```php
$vendors = $client->listVendors();
``` 
이전 API 호출의 출력 결과는 다음과 유사합니다.
```php
SoftLayer_Container_Network_CdnMarketplace_Vendor Object
(
    [vendorName] => akamai
    [featureSummary] => Performance, Reliability and Scale
    [features] => Web Delivery, Content Caching, Content Purge, HTTP/HTTPS Support
    [status] => ACTIVE
)

```
