---
title: "데이터 레이크 저장소 Vnet에서 aaaConnect tooAzure | Microsoft Docs"
description: "Azure Vnet에서 tooAzure 데이터 레이크 저장소 연결"
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
ms.openlocfilehash: c695dcf49fe4e1a87a90729cf085a938f3b51fe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="access-azure-data-lake-store-from-vms-within-an-azure-vnet"></a><span data-ttu-id="f5106-103">Azure VNET 내 VM에서 Azure Data Lake Store 액세스</span><span class="sxs-lookup"><span data-stu-id="f5106-103">Access Azure Data Lake Store from VMs within an Azure VNET</span></span>
<span data-ttu-id="f5106-104">Azure Data Lake Store는 공용 인터넷 IP 주소에서 실행되는 PaaS 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="f5106-104">Azure Data Lake Store is a PaaS service that runs on public Internet IP addresses.</span></span> <span data-ttu-id="f5106-105">일반적으로 toohello 공용 인터넷 수를 연결할 수 있는 모든 서버 tooAzure 데이터 레이크 저장소 끝점으로 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5106-105">Any server that can connect toohello public Internet can typically connect tooAzure Data Lake Store endpoints as well.</span></span> <span data-ttu-id="f5106-106">기본적으로 Azure Vnet에 있는 모든 Vm hello 인터넷에 액세스할 수 있습니다 및 따라서 Azure 데이터 레이크 저장소에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5106-106">By default, all VMs that are in Azure VNETs can access hello Internet and hence can access Azure Data Lake Store.</span></span> <span data-ttu-id="f5106-107">그러나 VNET toonot의 가능한 tooconfigure Vm은 인터넷 액세스 toohello 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5106-107">However, it is possible tooconfigure VMs in a VNET toonot have access toohello Internet.</span></span> <span data-ttu-id="f5106-108">이러한 Vm에 대 한 액세스 tooAzure 데이터 레이크 저장소 제한도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5106-108">For such VMs, access tooAzure Data Lake Store is restricted as well.</span></span> <span data-ttu-id="f5106-109">Azure Vnet의 Vm에 대 한 공용 인터넷 액세스가 차단 수행할 수 있습니다 hello 방법 중 하나를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5106-109">Blocking public Internet access for VMs in Azure VNETs can be done using any of hello following approach.</span></span>

* <span data-ttu-id="f5106-110">NSG(네트워크 보안 그룹) 구성</span><span class="sxs-lookup"><span data-stu-id="f5106-110">By configuring Network Security Groups (NSG)</span></span>
* <span data-ttu-id="f5106-111">UDR(사용자 정의 경로) 구성</span><span class="sxs-lookup"><span data-stu-id="f5106-111">By configuring User Defined Routes (UDR)</span></span>
* <span data-ttu-id="f5106-112">BGP (업계 표준 동적 라우팅 프로토콜)를 통해 경로 교환 하 여 ExpressRoute 사용 되는 경우 해당 블록 toohello 인터넷 액세스</span><span class="sxs-lookup"><span data-stu-id="f5106-112">By exchanging routes via BGP (industry standard dynamic routing protocol) when ExpressRoute is used that block access toohello Internet</span></span>

<span data-ttu-id="f5106-113">이 문서에서는 tooenable 제한 tooaccess hello 세 가지 방법 중 하나를 사용 하 여 리소스 위에 나열 된는 Azure Vm에서 toohello Azure Data Lake 저장소에 액세스 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="f5106-113">In this article, you will learn how tooenable access toohello Azure Data Lake Store from Azure VMs which have been restricted tooaccess resources using one of hello three methods listed above.</span></span>

## <a name="enabling-connectivity-tooazure-data-lake-store-from-vms-with-restricted-connectivity"></a><span data-ttu-id="f5106-114">제한 된 연결에 사용할 수 있도록 연결 tooAzure Vm에서 데이터 레이크 저장소</span><span class="sxs-lookup"><span data-stu-id="f5106-114">Enabling connectivity tooAzure Data Lake Store from VMs with restricted connectivity</span></span>
<span data-ttu-id="f5106-115">이러한 Vm에서 tooaccess Azure 데이터 레이크 저장소, Azure 데이터 레이크 저장소 계정 hello를 사용할 수 있는 tooaccess hello IP 주소 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5106-115">tooaccess Azure Data Lake Store from such VMs, you must configure them tooaccess hello IP address where hello Azure Data Lake Store account is available.</span></span> <span data-ttu-id="f5106-116">계정을 hello DNS 이름을 확인 하 여 데이터 레이크 저장소 계정에 대 한 hello IP 주소를 확인할 수 있습니다 (`<account>.azuredatalakestore.net`).</span><span class="sxs-lookup"><span data-stu-id="f5106-116">You can identify hello IP addresses for your Data Lake Store accounts by resolving hello DNS names of your accounts (`<account>.azuredatalakestore.net`).</span></span> <span data-ttu-id="f5106-117">이를 위해 **nslookup**와 같은 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5106-117">For this you can use tools such as **nslookup**.</span></span> <span data-ttu-id="f5106-118">컴퓨터에서 명령 프롬프트를 열고 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5106-118">Open a command prompt on your computer and run hello following command.</span></span>

    nslookup mydatastore.azuredatalakestore.net

<span data-ttu-id="f5106-119">hello 출력 hello 다음과 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5106-119">hello output resembles hello following.</span></span> <span data-ttu-id="f5106-120">에 대 한 가치 hello **주소** 속성은 데이터 레이크 저장소 계정에 연결 된 hello IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="f5106-120">hello value against **Address** property is hello IP address associated with your Data Lake Store account.</span></span>

    Non-authoritative answer:
    Name:    1434ceb1-3a4b-4bc0-9c69-a0823fd69bba-mydatastore.projectcabostore.net
    Address:  104.44.88.112
    Aliases:  mydatastore.azuredatalakestore.net


### <a name="enabling-connectivity-from-vms-restricted-by-using-nsg"></a><span data-ttu-id="f5106-121">NSG를 사용하여 제한된 VM에서 연결을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="f5106-121">Enabling connectivity from VMs restricted by using NSG</span></span>
<span data-ttu-id="f5106-122">그러면 액세스 toohello 데이터 레이크 저장소 IP 주소를 허용 하는 다른 NSG를 만들 수 있습니다 NSG 규칙은 사용 tooblock toohello 인터넷에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5106-122">When a NSG rule is used tooblock access toohello Internet, then you can create another NSG that allows access toohello Data Lake Store IP Address.</span></span> <span data-ttu-id="f5106-123">NSG 규칙에 대한 자세한 내용은 [네트워크 보안 그룹이란?](../virtual-network/virtual-networks-nsg.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5106-123">More information on NSG rules is available at [What is a Network Security Group?](../virtual-network/virtual-networks-nsg.md).</span></span> <span data-ttu-id="f5106-124">Toocreate Nsg 확인 하는 방법에 대 한 지침은 [어떻게 toomanage Nsg를 사용 하 여 Azure 포털을 hello](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5106-124">For instructions on how toocreate NSGs see [How toomanage NSGs using hello Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>

### <a name="enabling-connectivity-from-vms-restricted-by-using-udr-or-expressroute"></a><span data-ttu-id="f5106-125">UDR 또는 ExpressRoute를 사용하여 제한된 VM에서 연결을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="f5106-125">Enabling connectivity from VMs restricted by using UDR or ExpressRoute</span></span>
<span data-ttu-id="f5106-126">경로, UDRs 하거나 BGP 교환 경로 사용 되는 tooblock 액세스 toohello 인터넷을 특수 경로 toobe Vm 이러한 서브넷에 있는 데이터 레이크 저장소 끝점에 액세스할 수 있도록 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5106-126">When routes, either UDRs or BGP-exchanged routes, are used tooblock access toohello Internet, a special route needs toobe configured so that VMs in such subnets can access Data Lake Store endpoints.</span></span> <span data-ttu-id="f5106-127">자세한 내용은 [사용자 정의 경로란?](../virtual-network/virtual-networks-udr-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5106-127">For more information, see [What are User Defined Routes?](../virtual-network/virtual-networks-udr-overview.md).</span></span> <span data-ttu-id="f5106-128">UDR 만들기에 대한 지침은 [Resource Manager에서 UDR 만들기](../virtual-network/virtual-network-create-udr-arm-ps.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5106-128">For instructions on creating UDRs, see [Create UDRs in Resource Manager](../virtual-network/virtual-network-create-udr-arm-ps.md).</span></span>

### <a name="enabling-connectivity-from-vms-restricted-by-using-expressroute"></a><span data-ttu-id="f5106-129">ExpressRoute를 사용하여 제한된 VM에서 연결을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="f5106-129">Enabling connectivity from VMs restricted by using ExpressRoute</span></span>
<span data-ttu-id="f5106-130">ExpressRoute 회로 구성 된 온-프레미스 서버 hello 데이터 레이크 저장소 공용 피어 링을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5106-130">When an ExpressRoute circuit is configured, hello on-premises servers can access Data Lake Store through public peering.</span></span> <span data-ttu-id="f5106-131">공용 피어링을 위한 ExpressRoute 구성에 대한 자세한 내용은 [ExpressRoute FAQ](../expressroute/expressroute-faqs.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5106-131">More details on configuring ExpressRoute for public peering is available at [ExpressRoute FAQs](../expressroute/expressroute-faqs.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="f5106-132">참고 항목</span><span class="sxs-lookup"><span data-stu-id="f5106-132">See also</span></span>
* [<span data-ttu-id="f5106-133">Azure Data Lake Store 개요</span><span class="sxs-lookup"><span data-stu-id="f5106-133">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
* [<span data-ttu-id="f5106-134">Azure Data Lake Store에 저장된 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="f5106-134">Securing data stored in Azure Data Lake Store</span></span>](data-lake-store-security-overview.md)

