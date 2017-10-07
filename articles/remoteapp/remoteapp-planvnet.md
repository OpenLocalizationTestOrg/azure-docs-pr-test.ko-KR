---
title: "aaaHow tooplan Azure RemoteApp 컬렉션에 대 한 가상 네트워크 | Microsoft Docs"
description: "자세한 내용은 방법 tooplan Azure RemoteApp 컬렉션에 대 한 가상 네트워크입니다."
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
ms.openlocfilehash: d7eeefc3c66815b18f9338e2e428585e6f81a12a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooplan-your-virtual-network-for-azure-remoteapp"></a><span data-ttu-id="9aab4-103">어떻게 tooplan Azure RemoteApp에 대 한 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="9aab4-103">How tooplan your virtual network for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9aab4-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9aab4-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="9aab4-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="9aab4-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="9aab4-106">이 문서에서는 설명 어떻게 tooset Azure 가상 네트워크 (VNET) 및 Azure RemoteApp에 대 한 hello 서브넷을 합니다.</span><span class="sxs-lookup"><span data-stu-id="9aab4-106">This document describes how tooset up your Azure virtual network (VNET) and hello subnet for Azure RemoteApp.</span></span> <span data-ttu-id="9aab4-107">Azure 가상 네트워크를 잘 모르는 경우 이것이 사용 하 여 네트워크 인프라 toohello 클라우드와 toocreate 하이브리드 솔루션 Azure와 온-프레미스 리소스 toovirtualize 하는 데 도움이 되는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="9aab4-107">If you are unfamiliar with Azure virtual networks, this is a capability that helps you toovirtualize your network infrastructure toohello cloud and toocreate hybrid solutions with Azure and your on-premises resources.</span></span> <span data-ttu-id="9aab4-108">해당 서비스에 대한 자세한 내용은 [여기](../virtual-network/virtual-networks-overview.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9aab4-108">You can read more about it [here](../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="9aab4-109">Azure RemoteApp을 배포 하는 가상 네트워크의 (수신 및 송신) 트래픽에 대 한 보안 정책을 toodefine를 하려는 경우 좋습니다 hello 나머지 hello Azure에서에서 배포를 Azure RemoteApp에 대 한 별도 서브넷을 만드는 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="9aab4-109">If you want toodefine security policies for traffic (both incoming and outgoing) in your virtual network where you are deploying Azure RemoteApp, we strongly recommend creating a separate subnet for Azure RemoteApp from hello rest of your deployments in hello Azure virtual network.</span></span> <span data-ttu-id="9aab4-110">어떻게 toodefine 보안 정책에서 Azure 가상 네트워크 서브넷에 대 한 자세한 내용은 읽으십시오 [는 보안 그룹 NSG (네트워크) 이란?](../virtual-network/virtual-networks-nsg.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9aab4-110">For more information on how toodefine security policies on your Azure virtual network subnet, please read [What is a Network Security Group (NSG)?](../virtual-network/virtual-networks-nsg.md).</span></span>

## <a name="types-of-azure-remoteapp-collections-with-azure-virtual-networks"></a><span data-ttu-id="9aab4-111">Azure 가상 네트워크를 사용한 Azure RemoteApp 컬렉션 형식</span><span class="sxs-lookup"><span data-stu-id="9aab4-111">Types of Azure RemoteApp collections with Azure virtual networks</span></span>
<span data-ttu-id="9aab4-112">hello 다음 그래픽 옵션을 표시할 hello 두 개의 다른 컬렉션 toouse 가상 네트워크를 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="9aab4-112">hello following graphics show hello two different collection options when you want toouse a virtual network.</span></span>

### <a name="azure-remoteapp-cloud-collection-with-vnet"></a><span data-ttu-id="9aab4-113">VNET을 통한 Azure RemoteApp 클라우드 컬렉션</span><span class="sxs-lookup"><span data-stu-id="9aab4-113">Azure RemoteApp cloud collection with VNET</span></span>
 ![VNET을 통한 Azure RemoteApp - 클라우드 컬렉션](./media/remoteapp-planvpn/ra-cloudvpn.png)

<span data-ttu-id="9aab4-115">Azure의 hello RemoteApp 세션 호스트에 필요 하며 tooaccess hello 리소스를 모두 배포 되는 위치 Azure RemoteApp 컬렉션을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9aab4-115">This represents an Azure RemoteApp collection where all hello resources that hello RemoteApp session hosts need tooaccess are deployed in Azure.</span></span> <span data-ttu-id="9aab4-116">RemoteApp VNET을 hello로 동일한 VNET 또는 Azure에서 서로 다른 VNET hello에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9aab4-116">They can be in hello same VNET as hello RemoteApp VNET or a different VNET in Azure.</span></span>

### <a name="azure-remoteapp-hybrid-collection-with-vnet"></a><span data-ttu-id="9aab4-117">VNET을 통한 Azure RemoteApp 하이브리드 컬렉션</span><span class="sxs-lookup"><span data-stu-id="9aab4-117">Azure RemoteApp hybrid collection with VNET</span></span>
![VNET을 통한 Azure RemoteApp - 하이브리드 컬렉션](./media/remoteapp-planvpn/ra-hybridvpn.png)

<span data-ttu-id="9aab4-119">여기서 hello RemoteApp 세션 호스트에 필요 하며 tooaccess hello 리소스 중 일부는 온-프레미스 배포 Azure RemoteApp 컬렉션을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9aab4-119">This represents an Azure RemoteApp collection where some of hello resources that hello RemoteApp session hosts need tooaccess are deployed on-premises.</span></span> <span data-ttu-id="9aab4-120">RemoteApp VNET을 hello는 사이트 간 VPN 또는 Express 경로 같은 Azure 하이브리드 기술을 사용 하 여 연결 된 toohello 온-프레미스 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="9aab4-120">hello RemoteApp VNET is linked toohello on-premises network using Azure hybrid technologies like site-to-site VPN or Express Route.</span></span>

## <a name="how-hello-system-works"></a><span data-ttu-id="9aab4-121">Hello 시스템 작동 하는 방법</span><span class="sxs-lookup"><span data-stu-id="9aab4-121">How hello system works</span></span>
<span data-ttu-id="9aab4-122">Azure RemoteApp hello에서는 Azure 가상 컴퓨터 (업로드 된 이미지)를 구축 하는 동안 선택한 toohello 가상 네트워크 서브넷을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="9aab4-122">Under hello covers Azure RemoteApp deploys Azure virtual machines (with your uploaded image) toohello virtual network subnet that you chose during provisioning.</span></span> <span data-ttu-id="9aab4-123">하이브리드 컬렉션을 선택한 경우 tooresolve hello hello 가상 네트워크에서 제공 하는 hello DNS 서버를 통해 워크플로 프로 비전 하는 hello에 입력 한 hello 도메인 컨트롤러의 FQDN을 시도 했습니다.</span><span class="sxs-lookup"><span data-stu-id="9aab4-123">If you opted for a hybrid collection, we try tooresolve hello FQDN of hello domain controller you entered in hello provisioning workflow with hello DNS server provided in hello virtual network.</span></span>  
<span data-ttu-id="9aab4-124">Tooan 기존 가상 네트워크를 연결 하는 경우 Azure RemoteApp 서브넷에서 네트워크 보안 그룹에 있는지 tooexpose hello 필요한 포트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9aab4-124">If you are connecting tooan existing virtual network, make sure tooexpose hello necessary ports in your network security groups in your Azure RemoteApp subnet.</span></span> 

<span data-ttu-id="9aab4-125">[Azure RemoteApp에 대해 충분히 큰 서브넷](remoteapp-vnetsizing.md)을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9aab4-125">We recommend you use a [large enough  subnet for Azure RemoteApp](remoteapp-vnetsizing.md).</span></span> <span data-ttu-id="9aab4-126">가장 큰 hello Azure 가상 네트워크에서 지원 되 는/8 (CIDR 서브넷 정의 사용).</span><span class="sxs-lookup"><span data-stu-id="9aab4-126">hello largest supported by Azure Virtual network is /8 (using CIDR subnet definitions).</span></span> <span data-ttu-id="9aab4-127">서브넷에 충분히 큰 tooaccommodate 하는 동안 모든 hello Azure RemoteApp Vm 수직 hello 앱에 액세스 하는 더 많은 사용자가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9aab4-127">Your subnet should be large enough tooaccommodate all hello Azure RemoteApp VMs during scale-up when more users are accessing hello apps.</span></span> 

<span data-ttu-id="9aab4-128">다음은 가상 네트워크 서브넷에서 tooenable 필요한 hello 작업:</span><span class="sxs-lookup"><span data-stu-id="9aab4-128">Following are hello things you will need tooenable on your virtual network subnet:</span></span> 

1. <span data-ttu-id="9aab4-129">Hello 서브넷의 아웃 바운드 트래픽이 hello 내부 Azure RemoteApp 서비스 중 하나가 지정 된 포트 범위 10101 10175 toocommunicate에서 허용 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9aab4-129">Outbound traffic from hello subnet should be allowed on port range 10101-10175 toocommunicate with one of hello internal Azure RemoteApp services.</span></span>
2. <span data-ttu-id="9aab4-130">서브넷 tooconnect tooAzure 포트 443에서 저장소에서에서 허용 되는 아웃 바운드 트래픽은</span><span class="sxs-lookup"><span data-stu-id="9aab4-130">Outbound traffic should be allowed from your subnet tooconnect tooAzure Storage on port 443</span></span>
3. <span data-ttu-id="9aab4-131">Azure에서 호스트 되는 Active Directory를 사용 하도록 설정한 경우에 Azure RemoteApp에 대 한 hello 가상 네트워크 서브넷 내에서 VM 수 tooconnect toothat 도메인 컨트롤러 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9aab4-131">If you have Active Directory hosted in Azure, make sure any VM within hello virtual network subnet for Azure RemoteApp is able tooconnect toothat domain controller.</span></span> <span data-ttu-id="9aab4-132">hello 가상 네트워크에 DNS hello 수 tooresolve hello이 도메인 컨트롤러의 FQDN 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9aab4-132">hello DNS in hello virtual network should be able tooresolve hello FQDN of this domain controller.</span></span>

## <a name="virtual-network-with-forced-tunneling"></a><span data-ttu-id="9aab4-133">강제 터널링을 통한 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="9aab4-133">Virtual network with forced tunneling</span></span>
<span data-ttu-id="9aab4-134">[강제 터널링](../vpn-gateway/vpn-gateway-about-forced-tunneling.md) 은 이제 모든 새 Azure RemoteApp 컬렉션에 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="9aab4-134">[Forced tunneling](../vpn-gateway/vpn-gateway-about-forced-tunneling.md) is now supported for all new Azure RemoteApp collections.</span></span> <span data-ttu-id="9aab4-135">에서는 현재 마이그레이션을 지원 하지 않는 hello 강제 터널링 하는 기존 컬렉션 toosupport입니다.</span><span class="sxs-lookup"><span data-stu-id="9aab4-135">We currently do not support hello migration of an existing collection toosupport forced tunneling.</span></span>  <span data-ttu-id="9aab4-136">Toodelete hello VNET tooAzure RemoteApp을 연결 하는 강제 터널링을 사용 하면 컬렉션에 새 하나의 tooget 만들기를 사용 하 여 모든 기존 컬렉션 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9aab4-136">You will have toodelete all your existing collections using hello VNET that you are linking tooAzure RemoteApp and create a new one tooget forced tunneling enabled on your collections.</span></span> 

