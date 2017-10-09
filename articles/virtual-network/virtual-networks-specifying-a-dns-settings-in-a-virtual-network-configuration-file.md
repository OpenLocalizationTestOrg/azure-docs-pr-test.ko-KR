---
title: "가상 네트워크 구성 파일에서 DNS 설정을 aaaSpecifying | Microsoft Docs"
description: "가상 네트워크 구성을 사용 하 여 가상 네트워크의 DNS 서버 설정을 toochange hello 클래식 배포 모델에서 파일을 어떻게"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a8905927-92ac-42b5-8c33-8e42c000692c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: d53a658773e1c930b5a28a701db0be9edd26565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-virtual-network-configuration-file"></a><span data-ttu-id="8569a-103">가상 네트워크 구성 파일에서 DNS 설정 지정</span><span class="sxs-lookup"><span data-stu-id="8569a-103">Specifying DNS settings in a virtual network configuration file</span></span>
<span data-ttu-id="8569a-104">네트워크 구성 파일을 두 개의 요소가 toospecify 도메인 이름 (DNS System) 설정을 사용할 수 있는: **DnsServers** 및 **DnsServerRef**합니다.</span><span class="sxs-lookup"><span data-stu-id="8569a-104">A network configuration file has two elements that you can use toospecify Domain Name System (DNS) settings: **DnsServers** and **DnsServerRef**.</span></span> <span data-ttu-id="8569a-105">IP 주소를 지정 하 여 DNS 서버 목록을 추가할 수 있으며 이름 toohello 참조 **DnsServers** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="8569a-105">You can add a list of DNS servers by specifying their IP addresses and reference names toohello **DnsServers** element.</span></span> <span data-ttu-id="8569a-106">그런 다음 사용할 수는 **DnsServerRef** 요소 toospecify hello DnsServers 요소에서 DNS 서버 항목은 가상 네트워크 내의 다른 네트워크 사이트에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8569a-106">You can then use a **DnsServerRef** element toospecify which DNS server entries from hello DnsServers element are used for different network sites within your virtual network.</span></span>

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="8569a-107">이 문서에서는 hello 클래식 배포 모델에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8569a-107">This article covers hello classic deployment model.</span></span>

<span data-ttu-id="8569a-108">hello 네트워크 구성 파일 요소 다음 hello를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8569a-108">hello network configuration file may contain hello following elements.</span></span> <span data-ttu-id="8569a-109">hello 각 요소의 제목은 값 설정 hello 요소에 대 한 추가 정보를 제공 하는 연결 된 tooa 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="8569a-109">hello title of each element is linked tooa page that provides additional information about hello element value settings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8569a-110">어떻게 tooconfigure hello 네트워크 구성 파일에 대 한 정보를 참조 하십시오. [네트워크 구성 파일을 사용 하 여 가상 네트워크 구성](virtual-networks-using-network-configuration-file.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8569a-110">For information about how tooconfigure hello network configuration file, see [Configure a Virtual Network Using a Network Configuration File](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="8569a-111">Hello 네트워크 구성 파일에 포함 된 각 요소에 대 한 정보를 참조 하십시오. [Azure 가상 네트워크 구성 스키마](https://msdn.microsoft.com/library/azure/jj157100.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="8569a-111">For information about each element contained in hello network configuration file, see [Azure Virtual Network Configuration Schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
> 
> 

[<span data-ttu-id="8569a-112">Dns 요소</span><span class="sxs-lookup"><span data-stu-id="8569a-112">Dns Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <Dns>
      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>
    </Dns>

> [!WARNING]
> <span data-ttu-id="8569a-113">hello **이름** hello에 대 한 특성 **DnsServer** 요소 hello에 대 한 참조로만 사용 됩니다 **DnsServerRef** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="8569a-113">hello **name** attribute in hello **DnsServer** element is used only as a reference for hello **DnsServerRef** element.</span></span> <span data-ttu-id="8569a-114">DNS 서버 hello에 대 한 호스트 이름을 hello를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8569a-114">It does not represent hello host name for hello DNS server.</span></span> <span data-ttu-id="8569a-115">각 **DnsServer** 특성 값 hello 전체 Microsoft Azure 구독에서 고유 해야</span><span class="sxs-lookup"><span data-stu-id="8569a-115">Each **DnsServer** attribute value must be unique across hello entire Microsoft Azure subscription</span></span>
> 
> 

[<span data-ttu-id="8569a-116">가상 네트워크 사이트 요소</span><span class="sxs-lookup"><span data-stu-id="8569a-116">Virtual Network Sites Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <DnsServersRef>
      <DnsServerRef name="ID1" />
      <DnsServerRef name="ID2" />
      <DnsServerRef name="ID3" />
    </DnsServersRef>

> [!NOTE]
> <span data-ttu-id="8569a-117">주문 toospecify hello 가상 네트워크 사이트 요소에 대 한이 설정은, 이전에 hello DNS 요소에 정의 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8569a-117">In order toospecify this setting for hello Virtual Network Sites element, it must be previously defined in hello DNS element.</span></span> <span data-ttu-id="8569a-118">hello DnsServerRef *이름* hello 가상 네트워크 사이트 요소 dns 서버에 대 한 hello DNS 요소에 지정 된 tooa 이름 값을 참조 해야 *이름*합니다.</span><span class="sxs-lookup"><span data-stu-id="8569a-118">hello DnsServerRef *name* in hello Virtual Network Sites element must refer tooa name value specified in hello DNS element for DnsServer *name*.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="8569a-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8569a-119">Next steps</span></span>
* <span data-ttu-id="8569a-120">Hello 이해 [Azure 가상 네트워크 구성 스키마](http://go.microsoft.com/fwlink/?LinkId=248093)합니다.</span><span class="sxs-lookup"><span data-stu-id="8569a-120">Understand hello [Azure Virtual Network Configuration Schema](http://go.microsoft.com/fwlink/?LinkId=248093).</span></span>
* <span data-ttu-id="8569a-121">Hello 이해 [Azure 서비스 구성 스키마](https://msdn.microsoft.com/library/windowsazure/ee758710)합니다.</span><span class="sxs-lookup"><span data-stu-id="8569a-121">Understand hello [Azure Service Configuration Schema](https://msdn.microsoft.com/library/windowsazure/ee758710).</span></span>
* <span data-ttu-id="8569a-122">[네트워크 구성 파일을 사용하여 가상 네트워크 구성](virtual-networks-using-network-configuration-file.md)</span><span class="sxs-lookup"><span data-stu-id="8569a-122">[Configure a virtual network using Network configuration files](virtual-networks-using-network-configuration-file.md).</span></span>

