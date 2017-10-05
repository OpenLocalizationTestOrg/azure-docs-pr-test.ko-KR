---
title: "Vnet에서 Azure Data Lake Store 연결 | Microsoft 문서"
description: "Azure VNET에서 Azure Data Lake Store에 연결합니다."
services: data-lake-store,data-catalog
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 683fcfdc-cf93-46c3-b2d2-5cb79f5e9ea5
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ff7d28d7b53e872b804788647b1e672fafcf6995
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="access-azure-data-lake-store-from-vms-within-an-azure-vnet"></a><span data-ttu-id="80ea3-103">Azure VNET 내 VM에서 Azure Data Lake Store 액세스</span><span class="sxs-lookup"><span data-stu-id="80ea3-103">Access Azure Data Lake Store from VMs within an Azure VNET</span></span>
<span data-ttu-id="80ea3-104">Azure Data Lake Store는 공용 인터넷 IP 주소에서 실행되는 PaaS 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="80ea3-104">Azure Data Lake Store is a PaaS service that runs on public Internet IP addresses.</span></span> <span data-ttu-id="80ea3-105">공용 인터넷에 연결할 수 있는 서버는 일반적으로 Azure Data Lake Store 끝점에도 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ea3-105">Any server that can connect to the public Internet can typically connect to Azure Data Lake Store endpoints as well.</span></span> <span data-ttu-id="80ea3-106">기본적으로 Azure VNET에 있는 모든 VM은 인터넷에 액세스할 수 있으므로 Azure Data Lake Store에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ea3-106">By default, all VMs that are in Azure VNETs can access the Internet and hence can access Azure Data Lake Store.</span></span> <span data-ttu-id="80ea3-107">그러나 VNET에서 VM을 인터넷에 액세스하지 못하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ea3-107">However, it is possible to configure VMs in a VNET to not have access to the Internet.</span></span> <span data-ttu-id="80ea3-108">이러한 VM의 경우 Azure Data Lake Store에 대한 액세스도 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="80ea3-108">For such VMs, access to Azure Data Lake Store is restricted as well.</span></span> <span data-ttu-id="80ea3-109">Azure VNET의 VM에 대한 공용 인터넷 액세스를 차단하려면 다음 방법 중 하나를 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ea3-109">Blocking public Internet access for VMs in Azure VNETs can be done using any of the following approach.</span></span>

* <span data-ttu-id="80ea3-110">NSG(네트워크 보안 그룹) 구성</span><span class="sxs-lookup"><span data-stu-id="80ea3-110">By configuring Network Security Groups (NSG)</span></span>
* <span data-ttu-id="80ea3-111">UDR(사용자 정의 경로) 구성</span><span class="sxs-lookup"><span data-stu-id="80ea3-111">By configuring User Defined Routes (UDR)</span></span>
* <span data-ttu-id="80ea3-112">BGP(업계 표준 동적 라우팅 프로토콜)를 통해 경로 교환(ExpressRoute를 사용하여 인터넷에 대한 액세스를 차단하는 경우)</span><span class="sxs-lookup"><span data-stu-id="80ea3-112">By exchanging routes via BGP (industry standard dynamic routing protocol) when ExpressRoute is used that block access to the Internet</span></span>

<span data-ttu-id="80ea3-113">이 문서에서는 위에서 나열한 세 가지 방법 중 하나를 사용하여 리소스에 액세스하도록 제한된 Azure VM에서 Azure Data Lake Store에 액세스할 수 있도록 설정하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="80ea3-113">In this article, you will learn how to enable access to the Azure Data Lake Store from Azure VMs which have been restricted to access resources using one of the three methods listed above.</span></span>

## <a name="enabling-connectivity-to-azure-data-lake-store-from-vms-with-restricted-connectivity"></a><span data-ttu-id="80ea3-114">연결이 제한된 VM에서 Azure Data Lake Store에 대한 연결 사용 설정</span><span class="sxs-lookup"><span data-stu-id="80ea3-114">Enabling connectivity to Azure Data Lake Store from VMs with restricted connectivity</span></span>
<span data-ttu-id="80ea3-115">이러한 VM에서 Azure Data Lake Store에 액세스하려면 Azure Data Lake Store 계정을 사용할 수 있는 IP 주소에 액세스하도록 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ea3-115">To access Azure Data Lake Store from such VMs, you must configure them to access the IP address where the Azure Data Lake Store account is available.</span></span> <span data-ttu-id="80ea3-116">계정의 DNS 이름(`<account>.azuredatalakestore.net`)을 확인하여 Data Lake Store 계정의 IP 주소를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ea3-116">You can identify the IP addresses for your Data Lake Store accounts by resolving the DNS names of your accounts (`<account>.azuredatalakestore.net`).</span></span> <span data-ttu-id="80ea3-117">이를 위해 **nslookup**와 같은 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ea3-117">For this you can use tools such as **nslookup**.</span></span> <span data-ttu-id="80ea3-118">컴퓨터에서 명령 프롬프트를 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="80ea3-118">Open a command prompt on your computer and run the following command.</span></span>

    nslookup mydatastore.azuredatalakestore.net

<span data-ttu-id="80ea3-119">출력은 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="80ea3-119">The output resembles the following.</span></span> <span data-ttu-id="80ea3-120">**Address** 속성에 대한 값은 Data Lake Store 계정과 연결된 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="80ea3-120">The value against **Address** property is the IP address associated with your Data Lake Store account.</span></span>

    Non-authoritative answer:
    Name:    1434ceb1-3a4b-4bc0-9c69-a0823fd69bba-mydatastore.projectcabostore.net
    Address:  104.44.88.112
    Aliases:  mydatastore.azuredatalakestore.net


### <a name="enabling-connectivity-from-vms-restricted-by-using-nsg"></a><span data-ttu-id="80ea3-121">NSG를 사용하여 제한된 VM에서 연결을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="80ea3-121">Enabling connectivity from VMs restricted by using NSG</span></span>
<span data-ttu-id="80ea3-122">NSG 규칙을 사용하여 인터넷 액세스를 차단하면 Data Lake Store IP 주소에 액세스할 수 있는 다른 NSG를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ea3-122">When a NSG rule is used to block access to the Internet, then you can create another NSG that allows access to the Data Lake Store IP Address.</span></span> <span data-ttu-id="80ea3-123">NSG 규칙에 대한 자세한 내용은 [네트워크 보안 그룹이란?](../virtual-network/virtual-networks-nsg.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="80ea3-123">More information on NSG rules is available at [What is a Network Security Group?](../virtual-network/virtual-networks-nsg.md).</span></span> <span data-ttu-id="80ea3-124">NSG를 만드는 방법에 대한 지침은 [Azure Portal을 사용하여 NSG를 관리하는 방법](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="80ea3-124">For instructions on how to create NSGs see [How to manage NSGs using the Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>

### <a name="enabling-connectivity-from-vms-restricted-by-using-udr-or-expressroute"></a><span data-ttu-id="80ea3-125">UDR 또는 ExpressRoute를 사용하여 제한된 VM에서 연결을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="80ea3-125">Enabling connectivity from VMs restricted by using UDR or ExpressRoute</span></span>
<span data-ttu-id="80ea3-126">UDR 또는 BGP 교환 경로 중 하나를 사용하여 인터넷 액세스를 차단하는 경우 해당 서브넷의 VM이 Data Lake Store 끝점에 액세스할 수 있도록 특별한 경로를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ea3-126">When routes, either UDRs or BGP-exchanged routes, are used to block access to the Internet, a special route needs to be configured so that VMs in such subnets can access Data Lake Store endpoints.</span></span> <span data-ttu-id="80ea3-127">자세한 내용은 [사용자 정의 경로란?](../virtual-network/virtual-networks-udr-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="80ea3-127">For more information, see [What are User Defined Routes?](../virtual-network/virtual-networks-udr-overview.md).</span></span> <span data-ttu-id="80ea3-128">UDR 만들기에 대한 지침은 [Resource Manager에서 UDR 만들기](../virtual-network/virtual-network-create-udr-arm-ps.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="80ea3-128">For instructions on creating UDRs, see [Create UDRs in Resource Manager](../virtual-network/virtual-network-create-udr-arm-ps.md).</span></span>

### <a name="enabling-connectivity-from-vms-restricted-by-using-expressroute"></a><span data-ttu-id="80ea3-129">ExpressRoute를 사용하여 제한된 VM에서 연결을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="80ea3-129">Enabling connectivity from VMs restricted by using ExpressRoute</span></span>
<span data-ttu-id="80ea3-130">ExpressRoute 회로가 구성되면 온-프레미스 서버는 공용 피어링을 통해 Data Lake Store에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ea3-130">When an ExpressRoute circuit is configured, the on-premises servers can access Data Lake Store through public peering.</span></span> <span data-ttu-id="80ea3-131">공용 피어링을 위한 ExpressRoute 구성에 대한 자세한 내용은 [ExpressRoute FAQ](../expressroute/expressroute-faqs.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ea3-131">More details on configuring ExpressRoute for public peering is available at [ExpressRoute FAQs](../expressroute/expressroute-faqs.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="80ea3-132">참고 항목</span><span class="sxs-lookup"><span data-stu-id="80ea3-132">See also</span></span>
* [<span data-ttu-id="80ea3-133">Azure Data Lake Store 개요</span><span class="sxs-lookup"><span data-stu-id="80ea3-133">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
* [<span data-ttu-id="80ea3-134">Azure Data Lake Store에 저장된 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="80ea3-134">Securing data stored in Azure Data Lake Store</span></span>](data-lake-store-security-overview.md)

