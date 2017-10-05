---
title: "서비스 구성 파일에서 DNS 설정 지정 | Microsoft Docs"
description: "가상 네트워크에 대한 서비스 구성 파일을 사용하여 사용자 지정 DNS 설정 지정"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 467a4b99-8691-40b3-b640-e25e49675c71
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/24/2016
ms.author: jdial
ms.openlocfilehash: 0fba2ea06827aff29a7a092933edb8120d668b29
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a><span data-ttu-id="f74e5-103">서비스 구성 파일에서 DNS 설정 지정</span><span class="sxs-lookup"><span data-stu-id="f74e5-103">Specifying DNS Settings in a Service Configuration File</span></span>
## <a name="dns-elements"></a><span data-ttu-id="f74e5-104">DNS 요소</span><span class="sxs-lookup"><span data-stu-id="f74e5-104">DNS elements</span></span>
<span data-ttu-id="f74e5-105">서비스 구성 파일은 서비스에서 사용할 도메인 이름 시스템(DNS) 서버에 대한 IPv4 주소 목록과 함께 DnsServers 요소를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f74e5-105">A service configuration file may contain a DnsServers element with a list of IPv4 addresses for the Domain Name System (DNS) servers that the service will use.</span></span> <span data-ttu-id="f74e5-106">서비스 구성 파일의 설정은 네트워크 구성 파일의 설정보다 우선합니다.</span><span class="sxs-lookup"><span data-stu-id="f74e5-106">Settings in the service configuration file take precedence over settings in the network configuration file.</span></span> <span data-ttu-id="f74e5-107">자세한 내용은 [Azure 서비스 구성 스키마(.cscfg 파일)](https://msdn.microsoft.com/library/azure/ee758710.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f74e5-107">For more information, see [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span></span>

<span data-ttu-id="f74e5-108">**네트워크 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="f74e5-108">**NetworkConfiguration element**</span></span>

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> <span data-ttu-id="f74e5-109">**DnsServer** 요소 내 **이름** 특성은 참조 이름으로만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f74e5-109">The **name** attribute in the **DnsServer** element is used only as a reference name.</span></span> <span data-ttu-id="f74e5-110">DNS 서버에 대한 호스트 이름은 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f74e5-110">It does not represent the host name for the DNS server.</span></span> <span data-ttu-id="f74e5-111">각 **DnsServer** 특성 값은 전체 Microsoft Azure 구독에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f74e5-111">Each **DnsServer** attribute value must be unique across the entire Microsoft Azure subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="f74e5-112">참고 항목</span><span class="sxs-lookup"><span data-stu-id="f74e5-112">See Also</span></span>
[<span data-ttu-id="f74e5-113">Azure 서비스 구성 스키마(.cscfg)</span><span class="sxs-lookup"><span data-stu-id="f74e5-113">Azure Service Configuration Schema (.cscfg)</span></span>](https://msdn.microsoft.com/library/windowsazure/ee758710)

[<span data-ttu-id="f74e5-114">Azure 가상 네트워크 구성 스키마</span><span class="sxs-lookup"><span data-stu-id="f74e5-114">Azure Virtual Network Configuration Schema</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

[<span data-ttu-id="f74e5-115">네트워크 구성 파일을 사용하여 가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="f74e5-115">Configure a Virtual Network Using Network Configuration Files</span></span>](http://go.microsoft.com/fwlink/?LinkId=248094)

[<span data-ttu-id="f74e5-116">관리 포털의 가상 네트워크 설정 정보</span><span class="sxs-lookup"><span data-stu-id="f74e5-116">About Virtual Network settings in the Management Portal</span></span>](http://go.microsoft.com/fwlink/?LinkId=248092)

