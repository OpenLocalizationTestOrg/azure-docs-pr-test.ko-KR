---
title: "aaaCreate 응용 프로그램 게이트웨이-Azure 포털 | Microsoft Docs"
description: "사용 하 여 응용 프로그램 게이트웨이 toocreate 포털 hello 하는 방법에 대해 알아봅니다"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 54dffe95-d802-4f86-9e2e-293f49bd1e06
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 24c1d5701eae372cd233162ceb58dea36a3b6a39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-hello-portal"></a><span data-ttu-id="79bda-103">Hello 포털과 응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="79bda-103">Create an application gateway with hello portal</span></span>

<span data-ttu-id="79bda-104">[Application Gateway](application-gateway-introduction.md)는 ADC(응용 프로그램 배달 컨트롤러)를 서비스로 제공하여 다양한 7계층 부하 분산 기능을 제공하는 전용 가상 어플라이언스입니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-104">[Application Gateway](application-gateway-introduction.md) is a dedicated virtual appliance providing application delivery controller (ADC) as a service, offering various layer 7 load balancing capabilities for your application.</span></span> <span data-ttu-id="79bda-105">이 문서에서는 하 hello 단계 toocreate 응용 프로그램 게이트웨이 hello Azure 포털을 사용 하 고 백 엔드 멤버인 기존 서버를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-105">This article takes you through hello steps toocreate an Application Gateway using hello Azure portal and adding an existing server as a backend member.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="79bda-106">TooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="79bda-106">Log in tooAzure</span></span>

<span data-ttu-id="79bda-107">Toohello Azure 포털에 로그인 [http://portal.azure.com](http://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="79bda-107">Log in toohello Azure portal at [http://portal.azure.com](http://portal.azure.com)</span></span>

## <a name="create-application-gateway"></a><span data-ttu-id="79bda-108">응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="79bda-108">Create application gateway</span></span>

<span data-ttu-id="79bda-109">toocreate 응용 프로그램 게이트웨이 단계를 완료 하는 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-109">toocreate an application gateway, complete hello steps that follow.</span></span> <span data-ttu-id="79bda-110">Application Gateway에는 자체 서브넷이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-110">Application gateway requires its own subnet.</span></span> <span data-ttu-id="79bda-111">가상 네트워크를 만들 때 상태로 두고 충분 한 주소 공간 toohave 여러 서브넷을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-111">When creating a virtual network, ensure that you leave enough address space toohave multiple subnets.</span></span> <span data-ttu-id="79bda-112">Hello 응용 프로그램 게이트웨이 배포 tooa 서브넷 되 면 다른 응용 프로그램 게이트웨이 tooit은 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-112">After hello application gateway is deployed tooa subnet, only other application gateways can be added tooit.</span></span>

1. <span data-ttu-id="79bda-113">Hello 포털의 hello 즐겨찾기 창에서 클릭 **새로 만들기**</span><span class="sxs-lookup"><span data-stu-id="79bda-113">In hello Favorites pane of hello portal, click **New**</span></span>
1. <span data-ttu-id="79bda-114">Hello에 **새로** 블레이드에서 클릭 **네트워킹**합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-114">In hello **New** blade, click **Networking**.</span></span> <span data-ttu-id="79bda-115">Hello에 **네트워킹** 블레이드에서 클릭 **응용 프로그램 게이트웨이**hello 다음 이미지에에서 나타난 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="79bda-115">In hello **Networking** blade, click **Application Gateway**, as shown in hello following image:</span></span>

    ![Application Gateway 만들기][1]

1. <span data-ttu-id="79bda-117">Hello에 **기본 사항** 나타나는 블레이드 hello 다음 값을 입력 한 다음 클릭 **확인**:</span><span class="sxs-lookup"><span data-stu-id="79bda-117">In hello **Basics** blade that appears, enter hello following values, then click **OK**:</span></span>

   | <span data-ttu-id="79bda-118">**설정**</span><span class="sxs-lookup"><span data-stu-id="79bda-118">**Setting**</span></span> | <span data-ttu-id="79bda-119">**값**</span><span class="sxs-lookup"><span data-stu-id="79bda-119">**Value**</span></span> | <span data-ttu-id="79bda-120">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="79bda-120">**Details**</span></span>|
   |---|---|---|
   |<span data-ttu-id="79bda-121">**Name**</span><span class="sxs-lookup"><span data-stu-id="79bda-121">**Name**</span></span>|<span data-ttu-id="79bda-122">AdatumAppGateway</span><span class="sxs-lookup"><span data-stu-id="79bda-122">AdatumAppGateway</span></span>|<span data-ttu-id="79bda-123">hello 응용 프로그램 게이트웨이의 hello 이름</span><span class="sxs-lookup"><span data-stu-id="79bda-123">hello name of hello application gateway</span></span>|
   |<span data-ttu-id="79bda-124">**계층**</span><span class="sxs-lookup"><span data-stu-id="79bda-124">**Tier**</span></span>|<span data-ttu-id="79bda-125">Standard</span><span class="sxs-lookup"><span data-stu-id="79bda-125">Standard</span></span>|<span data-ttu-id="79bda-126">사용 가능한 값은 표준 또는 WAF입니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-126">Available values are Standard and WAF.</span></span> <span data-ttu-id="79bda-127">방문 [웹 응용 프로그램 방화벽](application-gateway-web-application-firewall-overview.md) toolearn WAF에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-127">Visit [web application firewall](application-gateway-web-application-firewall-overview.md) toolearn more about WAF.</span></span>|
   |<span data-ttu-id="79bda-128">**SKU 크기**</span><span class="sxs-lookup"><span data-stu-id="79bda-128">**SKU Size**</span></span>|<span data-ttu-id="79bda-129">중간</span><span class="sxs-lookup"><span data-stu-id="79bda-129">Medium</span></span>|<span data-ttu-id="79bda-130">표준 계층을 선택할 때 제공되는 옵션으로 소형, 중형 및 대형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-130">Choices when choosing Standard tier are Small, Medium, and Large.</span></span> <span data-ttu-id="79bda-131">WAF 계층을 선택할 때 옵션은 중간 및 대형 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-131">When choosing WAF tier, options are Medium and Large only.</span></span>|
   |<span data-ttu-id="79bda-132">**인스턴스 수**</span><span class="sxs-lookup"><span data-stu-id="79bda-132">**Instance count**</span></span>|<span data-ttu-id="79bda-133">2</span><span class="sxs-lookup"><span data-stu-id="79bda-133">2</span></span>|<span data-ttu-id="79bda-134">고가용성에 대 한 응용 프로그램 게이트웨이 hello의 인스턴스 수입니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-134">Number of instances of hello application gateway for high availability.</span></span> <span data-ttu-id="79bda-135">인스턴스 수 1은 테스트 목적으로만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-135">Instance counts of 1 should only be used for testing purposes.</span></span>|
   |<span data-ttu-id="79bda-136">**구독**</span><span class="sxs-lookup"><span data-stu-id="79bda-136">**Subscription**</span></span>|<span data-ttu-id="79bda-137">[구독 이름]</span><span class="sxs-lookup"><span data-stu-id="79bda-137">[Your subscription]</span></span>|<span data-ttu-id="79bda-138">구독 toocreate hello 응용 프로그램 게이트웨이 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-138">Select a subscription toocreate hello application gateway in.</span></span>|
   |<span data-ttu-id="79bda-139">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="79bda-139">**Resource group**</span></span>|<span data-ttu-id="79bda-140">**새로 만들기:** AdatumAppGatewayRG</span><span class="sxs-lookup"><span data-stu-id="79bda-140">**Create new:** AdatumAppGatewayRG</span></span>|<span data-ttu-id="79bda-141">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-141">Create a resource group.</span></span> <span data-ttu-id="79bda-142">hello 리소스 그룹 이름은 선택한 hello 구독 내에서 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-142">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="79bda-143">리소스 그룹을 읽기 hello에 대 한 자세한 toolearn [리소스 관리자](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) 개요 문서.</span><span class="sxs-lookup"><span data-stu-id="79bda-143">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="79bda-144">**위치**:</span><span class="sxs-lookup"><span data-stu-id="79bda-144">**Location**</span></span>|<span data-ttu-id="79bda-145">미국 서부</span><span class="sxs-lookup"><span data-stu-id="79bda-145">West US</span></span>||

1. <span data-ttu-id="79bda-146">Hello에 **설정** 아래에 나타나는 블레이드 **가상 네트워크**, 클릭 **가상 네트워크를 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-146">In hello **Settings** blade that appears under **Virtual network**, click **Choose a virtual network**.</span></span> <span data-ttu-id="79bda-147">hello **가상 네트워크 선택** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-147">hello **Choose virtual network** blade opens.</span></span>  <span data-ttu-id="79bda-148">클릭 **새로 만들기** tooopen hello **가상 네트워크 만들기** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-148">Click **Create new** tooopen hello **Create virtual network** blade.</span></span>

   ![가상 네트워크 선택][2]

1. <span data-ttu-id="79bda-150">Hello에 **만들기 가상 네트워크 블레이드** hello 다음 값을 입력 한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-150">On hello **Create virtual network blade** enter hello following values, then click **OK**.</span></span> <span data-ttu-id="79bda-151">hello **가상 네트워크 만들기** 및 **가상 네트워크 선택** 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-151">hello **Create virtual network** and **Choose virtual network** blades close.</span></span> <span data-ttu-id="79bda-152">이 단계는 hello를 채웁니다 **서브넷** 필드 hello에 **설정** 블레이드 hello 서브넷을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-152">This step populates hello **Subnet** field on hello **Settings** blade with hello subnet chosen.</span></span>

   | <span data-ttu-id="79bda-153">**설정**</span><span class="sxs-lookup"><span data-stu-id="79bda-153">**Setting**</span></span> | <span data-ttu-id="79bda-154">**값**</span><span class="sxs-lookup"><span data-stu-id="79bda-154">**Value**</span></span> | <span data-ttu-id="79bda-155">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="79bda-155">**Details**</span></span>|
   |---|---|---|
   |<span data-ttu-id="79bda-156">**Name**</span><span class="sxs-lookup"><span data-stu-id="79bda-156">**Name**</span></span>|<span data-ttu-id="79bda-157">AdatumAppGatewayVNET</span><span class="sxs-lookup"><span data-stu-id="79bda-157">AdatumAppGatewayVNET</span></span>|<span data-ttu-id="79bda-158">Hello 응용 프로그램 게이트웨이의 이름</span><span class="sxs-lookup"><span data-stu-id="79bda-158">Name of hello application gateway</span></span>|
   |<span data-ttu-id="79bda-159">**주소 공간**</span><span class="sxs-lookup"><span data-stu-id="79bda-159">**Address Space**</span></span>|<span data-ttu-id="79bda-160">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="79bda-160">10.0.0.0/16</span></span>|<span data-ttu-id="79bda-161">이 hello hello 가상 네트워크 주소 공간</span><span class="sxs-lookup"><span data-stu-id="79bda-161">This is hello address space for hello virtual network</span></span>|
   |<span data-ttu-id="79bda-162">**서브넷 이름**</span><span class="sxs-lookup"><span data-stu-id="79bda-162">**Subnet name**</span></span>|<span data-ttu-id="79bda-163">AppGatewaySubnet</span><span class="sxs-lookup"><span data-stu-id="79bda-163">AppGatewaySubnet</span></span>|<span data-ttu-id="79bda-164">응용 프로그램 게이트웨이 hello에 대 한 hello 서브넷의 이름</span><span class="sxs-lookup"><span data-stu-id="79bda-164">Name of hello subnet for hello application gateway</span></span>|
   |<span data-ttu-id="79bda-165">**서브넷 주소 범위**</span><span class="sxs-lookup"><span data-stu-id="79bda-165">**Subnet address range**</span></span>|<span data-ttu-id="79bda-166">10.0.0.0/28</span><span class="sxs-lookup"><span data-stu-id="79bda-166">10.0.0.0/28</span></span>|<span data-ttu-id="79bda-167">이 서브넷이 백 엔드 풀 멤버에 대 한 hello 가상 네트워크의 서브넷을 더 추가 허용</span><span class="sxs-lookup"><span data-stu-id="79bda-167">This subnet allows more additional subnets in hello virtual network for backend pool members</span></span>|

1. <span data-ttu-id="79bda-168">Hello에 **설정** 아래 블레이드 **프런트 엔드 IP 구성**, 선택 **공용** hello로 **IP 주소 유형**</span><span class="sxs-lookup"><span data-stu-id="79bda-168">On hello **Settings** blade under **Frontend IP configuration**, choose **Public** as hello **IP address type**</span></span>

1. <span data-ttu-id="79bda-169">Hello에 **설정** 아래 블레이드 **공용 IP 주소** 클릭 **공용 IP 주소 선택**, hello **공용 IP 주소 선택** 블레이드를 엽니다 를 클릭 하 여 **새로 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-169">On hello **Settings** blade under **Public IP address** click **Choose a public IP address**, hello **Choose public IP address** blade opens, click **Create new**.</span></span>

   ![공용 IP 선택][3]

1. <span data-ttu-id="79bda-171">Hello에 **공용 IP 주소 만들기** 블레이드에서 hello 기본값을 허용 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-171">On hello **Create public IP address** blade, accept hello default value, and click **OK**.</span></span> <span data-ttu-id="79bda-172">hello 블레이드를 닫고 hello 채웁니다 **공용 IP 주소** hello 공용 IP 주소로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-172">hello blade closes and populates hello **Public IP address** with hello public IP address chosen.</span></span>

1. <span data-ttu-id="79bda-173">Hello에 **설정** 아래 블레이드 **수신기 구성**, 클릭 **HTTP** 아래 **프로토콜**합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-173">On hello **Settings** blade under **Listener configuration**, click **HTTP** under **Protocol**.</span></span> <span data-ttu-id="79bda-174">Hello에 hello 포트 toouse 입력 **포트** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-174">Enter hello port toouse in hello **Port** field.</span></span>

2. <span data-ttu-id="79bda-175">클릭 **확인** hello에 **설정을** 블레이드 toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-175">Click **OK** on hello **Settings** blade toocontinue.</span></span>

1. <span data-ttu-id="79bda-176">Hello에서 hello 설정을 검토 **요약** 블레이드에 대 한 클릭 **확인** hello 응용 프로그램 게이트웨이 toostart 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-176">Review hello settings on hello **Summary** blade and click **OK** toostart creation of hello application gateway.</span></span> <span data-ttu-id="79bda-177">응용 프로그램 게이트웨이 장기 실행 작업을 만들고 시간 toocomplete를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-177">Creating an application gateway is a long running task and takes time toocomplete.</span></span>

## <a name="add-servers-toobackend-pools"></a><span data-ttu-id="79bda-178">서버 toobackend 풀 추가</span><span class="sxs-lookup"><span data-stu-id="79bda-178">Add servers toobackend pools</span></span>

<span data-ttu-id="79bda-179">Hello 응용 프로그램 게이트웨이 만든 후 hello 응용 프로그램 toobe 부하 분산을 호스트 하는 hello 시스템 toobe toohello 추가 된 응용 프로그램 게이트웨이 여전히 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-179">Once you create hello application gateway, hello systems that host hello application toobe load balanced still need toobe added toohello application gateway.</span></span> <span data-ttu-id="79bda-180">hello IP 주소, FQDN 또는 이러한 서버의 Nic toohello 백 엔드 주소 풀에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-180">hello IP addresses, FQDN, or NICs of these servers are added toohello backend address pools.</span></span>

### <a name="ip-address-or-fqdn"></a><span data-ttu-id="79bda-181">IP 주소 또는 FQDN</span><span class="sxs-lookup"><span data-stu-id="79bda-181">IP Address or FQDN</span></span>

1. <span data-ttu-id="79bda-182">Hello Azure 포털에서에서 만든 hello 응용 프로그램 게이트웨이와 **즐겨찾기** 창에서 클릭 **모든 리소스**합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-182">With hello application gateway created, in hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="79bda-183">Hello 클릭 **AdatumAppGateway** 에 응용 프로그램 게이트웨이 모든 리소스 블레이드를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-183">Click hello **AdatumAppGateway** application gateway in hello All resources blade.</span></span> <span data-ttu-id="79bda-184">이미 선택한 hello 구독에 여러 자원이 인 경우 입력 하면 **AdatumAppGateway** hello에 **이름별으로 필터링...**</span><span class="sxs-lookup"><span data-stu-id="79bda-184">If hello subscription you selected already has several resources in it, you can enter **AdatumAppGateway** in hello **Filter by name…**</span></span> <span data-ttu-id="79bda-185">상자 tooeasily 액세스 hello 응용 프로그램 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-185">box tooeasily access hello application gateway.</span></span>

1. <span data-ttu-id="79bda-186">만든 hello 응용 프로그램 게이트웨이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-186">hello application gateway you created is displayed.</span></span> <span data-ttu-id="79bda-187">클릭 **백 엔드 풀**, hello 현재 백 엔드 풀을 선택 하 고 **appGatewayBackendPool**, hello **appGatewayBackendPool** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-187">Click **Backend pools**, and select hello current backend pool **appGatewayBackendPool**, hello **appGatewayBackendPool** blade opens.</span></span>

   ![Application Gateway 백 엔드 풀][4]

1. <span data-ttu-id="79bda-189">클릭 **대상 추가** FQDN 값의 tooadd IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-189">Click **Add Target** tooadd IP addresses of FQDN values.</span></span> <span data-ttu-id="79bda-190">선택 **IP 주소 또는 FQDN** hello로 **형식** hello 필드에 IP 주소 또는 FQDN을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-190">Choose **IP address or FQDN** as hello **Type** and enter your IP address or FQDN in hello field.</span></span> <span data-ttu-id="79bda-191">추가 백 엔드 풀 멤버에 대해 이 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-191">Repeat this step for additional backend pool members.</span></span> <span data-ttu-id="79bda-192">완료하면 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-192">When done click **Save**.</span></span>

### <a name="virtual-machine-and-nic"></a><span data-ttu-id="79bda-193">가상 컴퓨터 및 NIC</span><span class="sxs-lookup"><span data-stu-id="79bda-193">Virtual Machine and NIC</span></span>

<span data-ttu-id="79bda-194">백 엔드 풀 구성원으로 가상 컴퓨터 NIC를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-194">You can also add Virtual Machine NICs as backend pool members.</span></span> <span data-ttu-id="79bda-195">응용 프로그램 게이트웨이 hello와 동일한 가상 네트워크를 통해 사용할 수 있는 hello 내에서 가상 컴퓨터만 hello 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-195">Only virtual machines within hello same virtual network as hello Application Gateway are available through hello dropdown.</span></span>

1. <span data-ttu-id="79bda-196">Hello Azure 포털에서에서 만든 hello 응용 프로그램 게이트웨이와 **즐겨찾기** 창에서 클릭 **모든 리소스**합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-196">With hello application gateway created, in hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="79bda-197">Hello 클릭 **AdatumAppGateway** 에 응용 프로그램 게이트웨이 모든 리소스 블레이드를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-197">Click hello **AdatumAppGateway** application gateway in hello All resources blade.</span></span> <span data-ttu-id="79bda-198">이미 선택한 hello 구독에 여러 자원이 인 경우 입력 하면 **AdatumAppGateway** hello에 **이름별으로 필터링...**</span><span class="sxs-lookup"><span data-stu-id="79bda-198">If hello subscription you selected already has several resources in it, you can enter **AdatumAppGateway** in hello **Filter by name…**</span></span> <span data-ttu-id="79bda-199">상자 tooeasily 액세스 hello 응용 프로그램 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-199">box tooeasily access hello application gateway.</span></span>

1. <span data-ttu-id="79bda-200">만든 hello 응용 프로그램 게이트웨이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-200">hello application gateway you created is displayed.</span></span> <span data-ttu-id="79bda-201">클릭 **백 엔드 풀**, hello 현재 백 엔드 풀을 선택 하 고 **appGatewayBackendPool**, hello **appGatewayBackendPool** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-201">Click **Backend pools**, and select hello current backend pool **appGatewayBackendPool**, hello **appGatewayBackendPool** blade opens.</span></span>

   ![Application Gateway 백 엔드 풀][5]

1. <span data-ttu-id="79bda-203">클릭 **대상 추가** FQDN 값의 tooadd IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-203">Click **Add Target** tooadd IP addresses of FQDN values.</span></span> <span data-ttu-id="79bda-204">선택 **가상 컴퓨터** hello로 **형식** hello 가상 컴퓨터 및 NIC toouse 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-204">Choose **Virtual Machine** as hello **Type** and select hello virtual machine and NIC toouse.</span></span> <span data-ttu-id="79bda-205">완료하면 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-205">When done click **Save**</span></span>

   > [!NOTE]
   > <span data-ttu-id="79bda-206">가상 컴퓨터에만 응용 프로그램 게이트웨이 hello hello 드롭다운 상자에서에서 사용할 수 있는 동일한 가상 네트워크를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-206">Only virtual machines in hello same virtual network as hello application gateway are available in hello drop down box.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="79bda-207">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="79bda-207">Clean up resources</span></span>

<span data-ttu-id="79bda-208">더 이상 필요 hello 리소스 그룹, 응용 프로그램 게이트웨이 및 모든 관련된 리소스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-208">When no longer needed, delete hello resource group, application gateway, and all related resources.</span></span> <span data-ttu-id="79bda-209">따라서 toodo hello 응용 프로그램 게이트웨이 블레이드를 클릭 hello 리소스 그룹을 선택 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-209">toodo so, select hello resource group from hello application gateway blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79bda-210">다음 단계</span><span class="sxs-lookup"><span data-stu-id="79bda-210">Next steps</span></span>

<span data-ttu-id="79bda-211">이 시나리오에서는 응용 프로그램 게이트웨이 배포 및 서버 toohello 백 엔드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-211">In this scenario, you deployed an application gateway and added a server toohello backend.</span></span> <span data-ttu-id="79bda-212">hello 다음 단계는 tooconfigure hello 응용 프로그램 게이트웨이 설정 수정 및 hello 게이트웨이의 조정 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-212">hello next steps are tooconfigure hello application gateway by modifying settings, and adjusting rules in hello gateway.</span></span> <span data-ttu-id="79bda-213">다음 문서는 hello를 방문 하 여 다음이 단계를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-213">These steps can be found by visiting hello following articles:</span></span>

<span data-ttu-id="79bda-214">사용자 지정 상태 toocreate 방문 하 여 조사 하는 방법에 대해 알아봅니다 [만들 사용자 지정 상태 프로브](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="79bda-214">Learn how toocreate custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="79bda-215">어떻게 tooconfigure SSL 오프 로딩 및 take hello 비용이 많이 드는 SSL 암호 해독 해제 하면 웹 서버 방문 하 여 자세한 [SSL 오프 로드 구성](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="79bda-215">Learn how tooconfigure SSL Offloading and take hello costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

<span data-ttu-id="79bda-216">자세한 내용은 방법 tooprotect 응용 프로그램을 [웹 응용 프로그램 방화벽](application-gateway-webapplicationfirewall-overview.md) 응용 프로그램 게이트웨이의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="79bda-216">Learn how tooprotect your applications with [Web Application Firewall](application-gateway-webapplicationfirewall-overview.md) a feature of application gateway.</span></span>

<!--Image references-->
[1]: ./media/application-gateway-create-gateway-portal/figure1.png
[2]: ./media/application-gateway-create-gateway-portal/figure2.png
[3]: ./media/application-gateway-create-gateway-portal/figure3.png
[4]: ./media/application-gateway-create-gateway-portal/figure4.png
[5]: ./media/application-gateway-create-gateway-portal/figure5.png
[scenario]: ./media/application-gateway-create-gateway-portal/scenario.png
