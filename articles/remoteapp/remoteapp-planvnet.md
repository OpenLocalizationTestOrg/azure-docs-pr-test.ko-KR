---
title: "Azure RemoteApp 컬렉션에 대해 가상 네트워크를 계획하는 방법 | Microsoft 문서"
description: "Azure RemoteApp 컬렉션에 대한 가상 네트워크를 계획하는 방법에 대해 알아봅니다."
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: ad9aff0e-f374-49c0-951d-4a7be1c36de0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 1eb8115b13fb18074b4c4726b69e3d9faf387c32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-plan-your-virtual-network-for-azure-remoteapp"></a><span data-ttu-id="c8a98-103">Azure RemoteApp에 대한 가상 네트워크를 계획하는 방법</span><span class="sxs-lookup"><span data-stu-id="c8a98-103">How to plan your virtual network for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c8a98-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a98-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="c8a98-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="c8a98-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="c8a98-106">이 문서에서는 Azure RemoteApp에 대한 Azure 가상 네트워크(VNET) 및 서브넷을 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a98-106">This document describes how to set up your Azure virtual network (VNET) and the subnet for Azure RemoteApp.</span></span> <span data-ttu-id="c8a98-107">Azure 가상 네트워크에 익숙하지 않은 경우 클라우드로 네트워크 인프라를 가상화하고 Azure 및 온-프레미스 리소스로 하이브리드 솔루션을 만들 수 있도록 하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c8a98-107">If you are unfamiliar with Azure virtual networks, this is a capability that helps you to virtualize your network infrastructure to the cloud and to create hybrid solutions with Azure and your on-premises resources.</span></span> <span data-ttu-id="c8a98-108">해당 서비스에 대한 자세한 내용은 [여기](../virtual-network/virtual-networks-overview.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a98-108">You can read more about it [here](../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="c8a98-109">Azure RemoteApp을 배포하고 있는 가상 네트워크의 트래픽(수신 및 송신)에 대한 보안 정책을 정의하려는 경우 Azure 가상 네트워크의 배포의 나머지 부분에서 Azure RemoteApp에 대한 별도 서브넷을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a98-109">If you want to define security policies for traffic (both incoming and outgoing) in your virtual network where you are deploying Azure RemoteApp, we strongly recommend creating a separate subnet for Azure RemoteApp from the rest of your deployments in the Azure virtual network.</span></span> <span data-ttu-id="c8a98-110">Azure 가상 네트워크 서브넷에 대한 보안 정책을 정의하는 방법에 대한 자세한 내용은 [NSG(네트워크 보안 그룹)란?](../virtual-network/virtual-networks-nsg.md)을 읽어 보세요.</span><span class="sxs-lookup"><span data-stu-id="c8a98-110">For more information on how to define security policies on your Azure virtual network subnet, please read [What is a Network Security Group (NSG)?](../virtual-network/virtual-networks-nsg.md).</span></span>

## <a name="types-of-azure-remoteapp-collections-with-azure-virtual-networks"></a><span data-ttu-id="c8a98-111">Azure 가상 네트워크를 사용한 Azure RemoteApp 컬렉션 형식</span><span class="sxs-lookup"><span data-stu-id="c8a98-111">Types of Azure RemoteApp collections with Azure virtual networks</span></span>
<span data-ttu-id="c8a98-112">다음 그래픽은 가상 네트워크를 사용하려는 경우 두 가지 다른 컬렉션 옵션을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a98-112">The following graphics show the two different collection options when you want to use a virtual network.</span></span>

### <a name="azure-remoteapp-cloud-collection-with-vnet"></a><span data-ttu-id="c8a98-113">VNET을 통한 Azure RemoteApp 클라우드 컬렉션</span><span class="sxs-lookup"><span data-stu-id="c8a98-113">Azure RemoteApp cloud collection with VNET</span></span>
 ![VNET을 통한 Azure RemoteApp - 클라우드 컬렉션](./media/remoteapp-planvpn/ra-cloudvpn.png)

<span data-ttu-id="c8a98-115">Azure RemoteApp 컬렉션을 나타내며 여기에서 액세스가 필요한 RemoteApp 세션이 호스팅하는 모든 리소스는 Azure에서 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8a98-115">This represents an Azure RemoteApp collection where all the resources that the RemoteApp session hosts need to access are deployed in Azure.</span></span> <span data-ttu-id="c8a98-116">Azure에 있는 RemoteApp VNET 또는 다른 VNET과 같이 동일한 VNET에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a98-116">They can be in the same VNET as the RemoteApp VNET or a different VNET in Azure.</span></span>

### <a name="azure-remoteapp-hybrid-collection-with-vnet"></a><span data-ttu-id="c8a98-117">VNET을 통한 Azure RemoteApp 하이브리드 컬렉션</span><span class="sxs-lookup"><span data-stu-id="c8a98-117">Azure RemoteApp hybrid collection with VNET</span></span>
![VNET을 통한 Azure RemoteApp - 하이브리드 컬렉션](./media/remoteapp-planvpn/ra-hybridvpn.png)

<span data-ttu-id="c8a98-119">Azure RemoteApp 컬렉션을 나타내며 여기에서 액세스가 필요한 RemoteApp 세션이 호스팅하는 일부 리소스는 온-프레미스에서 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8a98-119">This represents an Azure RemoteApp collection where some of the resources that the RemoteApp session hosts need to access are deployed on-premises.</span></span> <span data-ttu-id="c8a98-120">RemoteApp VNET은 사이트 간 VPN 또는 Express Route와 같은 Azure 하이브리드 기술을 사용하여 온-프레미스 네트워크에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8a98-120">The RemoteApp VNET is linked to the on-premises network using Azure hybrid technologies like site-to-site VPN or Express Route.</span></span>

## <a name="how-the-system-works"></a><span data-ttu-id="c8a98-121">시스템 작동 방식</span><span class="sxs-lookup"><span data-stu-id="c8a98-121">How the system works</span></span>
<span data-ttu-id="c8a98-122">실제로 Azure RemoteApp은 Azure 가상 컴퓨터(업로드된 이미지)를 프로비전하는 동안 선택한 가상 네트워크 서브넷에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a98-122">Under the covers Azure RemoteApp deploys Azure virtual machines (with your uploaded image) to the virtual network subnet that you chose during provisioning.</span></span> <span data-ttu-id="c8a98-123">하이브리드 컬렉션을 선택한 경우 가상 네트워크에 제공된 DNS 서버를 통해 프로비전 워크플로에 입력한 도메인 컨트롤러의 FQDN을 해결하기 위해 노력합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a98-123">If you opted for a hybrid collection, we try to resolve the FQDN of the domain controller you entered in the provisioning workflow with the DNS server provided in the virtual network.</span></span>  
<span data-ttu-id="c8a98-124">기존 가상 네트워크에 연결하고 있는 경우 Azure RemoteApp 서브넷에서 네트워크 보안 그룹의 필요한 포트를 노출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a98-124">If you are connecting to an existing virtual network, make sure to expose the necessary ports in your network security groups in your Azure RemoteApp subnet.</span></span> 

<span data-ttu-id="c8a98-125">[Azure RemoteApp에 대해 충분히 큰 서브넷](remoteapp-vnetsizing.md)을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a98-125">We recommend you use a [large enough  subnet for Azure RemoteApp](remoteapp-vnetsizing.md).</span></span> <span data-ttu-id="c8a98-126">Azure 가상 네트워크에서 가장 많이 지원되는 것은 /8(CIDR 서브넷 정의 사용)입니다.</span><span class="sxs-lookup"><span data-stu-id="c8a98-126">The largest supported by Azure Virtual network is /8 (using CIDR subnet definitions).</span></span> <span data-ttu-id="c8a98-127">사용자의 서브넷은 더 많은 사용자가 응용 프로그램에 액세스할 때 확장하는 동안 모든 Azure RemoteApp VM을 수용하기에 충분해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a98-127">Your subnet should be large enough to accommodate all the Azure RemoteApp VMs during scale-up when more users are accessing the apps.</span></span> 

<span data-ttu-id="c8a98-128">다음은 가상 네트워크 서브넷에서 사용하도록 설정해야 하는 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="c8a98-128">Following are the things you will need to enable on your virtual network subnet:</span></span> 

1. <span data-ttu-id="c8a98-129">서브넷 아웃바운드 트래픽은 내부 Azure RemoteApp 서비스 중 하나와 통신하도록 포트 범위 10101-10175에서 허용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a98-129">Outbound traffic from the subnet should be allowed on port range 10101-10175 to communicate with one of the internal Azure RemoteApp services.</span></span>
2. <span data-ttu-id="c8a98-130">아웃바운드 트래픽은 포트 443의 Azure 저장소에 연결하도록 서브넷에서 허용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a98-130">Outbound traffic should be allowed from your subnet to connect to Azure Storage on port 443</span></span>
3. <span data-ttu-id="c8a98-131">Azure에서 호스팅되는 Active Directory가 있는 경우 Azure RemoteApp에 대한 가상 네트워크 서브넷 내의 모든 VM은 해당 도메인 컨트롤러에 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a98-131">If you have Active Directory hosted in Azure, make sure any VM within the virtual network subnet for Azure RemoteApp is able to connect to that domain controller.</span></span> <span data-ttu-id="c8a98-132">가상 네트워크의 DNS는 해당 도메인 컨트롤러의 FQDN을 확인할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a98-132">The DNS in the virtual network should be able to resolve the FQDN of this domain controller.</span></span>

## <a name="virtual-network-with-forced-tunneling"></a><span data-ttu-id="c8a98-133">강제 터널링을 통한 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="c8a98-133">Virtual network with forced tunneling</span></span>
<span data-ttu-id="c8a98-134">[강제 터널링](../vpn-gateway/vpn-gateway-about-forced-tunneling.md) 은 이제 모든 새 Azure RemoteApp 컬렉션에 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8a98-134">[Forced tunneling](../vpn-gateway/vpn-gateway-about-forced-tunneling.md) is now supported for all new Azure RemoteApp collections.</span></span> <span data-ttu-id="c8a98-135">현재 강제 터널링을 지원하기 위해 기존 컬렉션의 마이그레이션이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a98-135">We currently do not support the migration of an existing collection to support forced tunneling.</span></span>  <span data-ttu-id="c8a98-136">Azure RemoteApp에 연결 중인 VNET을 사용하여 모든 기존 컬렉션을 삭제하고 컬렉션에서 활성화된 강제 터널링을 가져오도록 새 것을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a98-136">You will have to delete all your existing collections using the VNET that you are linking to Azure RemoteApp and create a new one to get forced tunneling enabled on your collections.</span></span> 

