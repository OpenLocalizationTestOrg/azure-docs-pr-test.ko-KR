---
title: "Application Gateway 만들기 - Azure Portal | Microsoft Docs"
description: "포털을 사용하여 응용 프로그램 게이트웨이를 만드는 방법을 알아봅니다."
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
ms.openlocfilehash: d3c39cfe3159cd4059a81f966fb551175188278b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-application-gateway-with-the-portal"></a><span data-ttu-id="df59e-103">포털을 사용하여 Application Gateway 만들기</span><span class="sxs-lookup"><span data-stu-id="df59e-103">Create an application gateway with the portal</span></span>

<span data-ttu-id="df59e-104">[Application Gateway](application-gateway-introduction.md)는 ADC(응용 프로그램 배달 컨트롤러)를 서비스로 제공하여 다양한 7계층 부하 분산 기능을 제공하는 전용 가상 어플라이언스입니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-104">[Application Gateway](application-gateway-introduction.md) is a dedicated virtual appliance providing application delivery controller (ADC) as a service, offering various layer 7 load balancing capabilities for your application.</span></span> <span data-ttu-id="df59e-105">이 문서에서는 Azure Portal을 사용하여 Application Gateway를 만들고 기존 서버를 백 엔드 멤버로 추가하는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-105">This article takes you through the steps to create an Application Gateway using the Azure portal and adding an existing server as a backend member.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="df59e-106">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="df59e-106">Log in to Azure</span></span>

<span data-ttu-id="df59e-107">Azure Portal([http://portal.azure.com](http://portal.azure.com))에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-107">Log in to the Azure portal at [http://portal.azure.com](http://portal.azure.com)</span></span>

## <a name="create-application-gateway"></a><span data-ttu-id="df59e-108">응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="df59e-108">Create application gateway</span></span>

<span data-ttu-id="df59e-109">Application Gateway를 만들려면 다음 단계를 완료하세요.</span><span class="sxs-lookup"><span data-stu-id="df59e-109">To create an application gateway, complete the steps that follow.</span></span> <span data-ttu-id="df59e-110">Application Gateway에는 자체 서브넷이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-110">Application gateway requires its own subnet.</span></span> <span data-ttu-id="df59e-111">가상 네트워크를 만들 때 여러 서브넷을 둘 수 있는 충분한 주소 공간이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-111">When creating a virtual network, ensure that you leave enough address space to have multiple subnets.</span></span> <span data-ttu-id="df59e-112">응용 프로그램 게이트웨이가 서브넷에 배포된 후에는 다른 응용 프로그램 게이트웨이만 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-112">After the application gateway is deployed to a subnet, only other application gateways can be added to it.</span></span>

1. <span data-ttu-id="df59e-113">포털의 즐겨찾기 창에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-113">In the Favorites pane of the portal, click **New**</span></span>
1. <span data-ttu-id="df59e-114">**새로 만들기** 블레이드에서 **네트워킹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-114">In the **New** blade, click **Networking**.</span></span> <span data-ttu-id="df59e-115">다음 그림과 같이 **네트워킹** 블레이드에서 **Application Gateway**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-115">In the **Networking** blade, click **Application Gateway**, as shown in the following image:</span></span>

    ![Application Gateway 만들기][1]

1. <span data-ttu-id="df59e-117">표시되는 **기본 사항** 블레이드에서 다음 값을 입력한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-117">In the **Basics** blade that appears, enter the following values, then click **OK**:</span></span>

   | <span data-ttu-id="df59e-118">**설정**</span><span class="sxs-lookup"><span data-stu-id="df59e-118">**Setting**</span></span> | <span data-ttu-id="df59e-119">**값**</span><span class="sxs-lookup"><span data-stu-id="df59e-119">**Value**</span></span> | <span data-ttu-id="df59e-120">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="df59e-120">**Details**</span></span>|
   |---|---|---|
   |<span data-ttu-id="df59e-121">**Name**</span><span class="sxs-lookup"><span data-stu-id="df59e-121">**Name**</span></span>|<span data-ttu-id="df59e-122">AdatumAppGateway</span><span class="sxs-lookup"><span data-stu-id="df59e-122">AdatumAppGateway</span></span>|<span data-ttu-id="df59e-123">Application Gateway의 이름</span><span class="sxs-lookup"><span data-stu-id="df59e-123">The name of the application gateway</span></span>|
   |<span data-ttu-id="df59e-124">**계층**</span><span class="sxs-lookup"><span data-stu-id="df59e-124">**Tier**</span></span>|<span data-ttu-id="df59e-125">Standard</span><span class="sxs-lookup"><span data-stu-id="df59e-125">Standard</span></span>|<span data-ttu-id="df59e-126">사용 가능한 값은 표준 또는 WAF입니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-126">Available values are Standard and WAF.</span></span> <span data-ttu-id="df59e-127">[웹 응용 프로그램 방화벽](application-gateway-web-application-firewall-overview.md)을 방문하여 WAF에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="df59e-127">Visit [web application firewall](application-gateway-web-application-firewall-overview.md) to learn more about WAF.</span></span>|
   |<span data-ttu-id="df59e-128">**SKU 크기**</span><span class="sxs-lookup"><span data-stu-id="df59e-128">**SKU Size**</span></span>|<span data-ttu-id="df59e-129">중간</span><span class="sxs-lookup"><span data-stu-id="df59e-129">Medium</span></span>|<span data-ttu-id="df59e-130">표준 계층을 선택할 때 제공되는 옵션으로 소형, 중형 및 대형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-130">Choices when choosing Standard tier are Small, Medium, and Large.</span></span> <span data-ttu-id="df59e-131">WAF 계층을 선택할 때 옵션은 중간 및 대형 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-131">When choosing WAF tier, options are Medium and Large only.</span></span>|
   |<span data-ttu-id="df59e-132">**인스턴스 수**</span><span class="sxs-lookup"><span data-stu-id="df59e-132">**Instance count**</span></span>|<span data-ttu-id="df59e-133">2</span><span class="sxs-lookup"><span data-stu-id="df59e-133">2</span></span>|<span data-ttu-id="df59e-134">고가용성을 위한 Application Gateway의 인스턴스 수입니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-134">Number of instances of the application gateway for high availability.</span></span> <span data-ttu-id="df59e-135">인스턴스 수 1은 테스트 목적으로만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-135">Instance counts of 1 should only be used for testing purposes.</span></span>|
   |<span data-ttu-id="df59e-136">**구독**</span><span class="sxs-lookup"><span data-stu-id="df59e-136">**Subscription**</span></span>|<span data-ttu-id="df59e-137">[구독 이름]</span><span class="sxs-lookup"><span data-stu-id="df59e-137">[Your subscription]</span></span>|<span data-ttu-id="df59e-138">응용 프로그램 게이트웨이를 만들 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-138">Select a subscription to create the application gateway in.</span></span>|
   |<span data-ttu-id="df59e-139">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="df59e-139">**Resource group**</span></span>|<span data-ttu-id="df59e-140">**새로 만들기:** AdatumAppGatewayRG</span><span class="sxs-lookup"><span data-stu-id="df59e-140">**Create new:** AdatumAppGatewayRG</span></span>|<span data-ttu-id="df59e-141">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-141">Create a resource group.</span></span> <span data-ttu-id="df59e-142">리소스 그룹 이름은 선택한 구독 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-142">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="df59e-143">리소스 그룹에 대해 자세히 알아보려면 [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) 개요 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="df59e-143">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="df59e-144">**위치**:</span><span class="sxs-lookup"><span data-stu-id="df59e-144">**Location**</span></span>|<span data-ttu-id="df59e-145">미국 서부</span><span class="sxs-lookup"><span data-stu-id="df59e-145">West US</span></span>||

1. <span data-ttu-id="df59e-146">**가상 네트워크** 아래에 표시되는 **설정** 블레이드에서 **가상 네트워크 선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-146">In the **Settings** blade that appears under **Virtual network**, click **Choose a virtual network**.</span></span> <span data-ttu-id="df59e-147">**가상 네트워크 선택** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-147">The **Choose virtual network** blade opens.</span></span>  <span data-ttu-id="df59e-148">**새로 만들기**를 클릭하여 **가상 네트워크 만들기** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-148">Click **Create new** to open the **Create virtual network** blade.</span></span>

   ![가상 네트워크 선택][2]

1. <span data-ttu-id="df59e-150">**가상 네트워크 만들기** 블레이드에서 다음 값을 입력한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-150">On the **Create virtual network blade** enter the following values, then click **OK**.</span></span> <span data-ttu-id="df59e-151">**가상 네트워크 만들기** 및 **가상 네트워크 선택** 블레이드가 닫힙니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-151">The **Create virtual network** and **Choose virtual network** blades close.</span></span> <span data-ttu-id="df59e-152">이 단계에서는 **설정** 블레이드의 **서브넷** 필드를 선택한 서브넷으로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-152">This step populates the **Subnet** field on the **Settings** blade with the subnet chosen.</span></span>

   | <span data-ttu-id="df59e-153">**설정**</span><span class="sxs-lookup"><span data-stu-id="df59e-153">**Setting**</span></span> | <span data-ttu-id="df59e-154">**값**</span><span class="sxs-lookup"><span data-stu-id="df59e-154">**Value**</span></span> | <span data-ttu-id="df59e-155">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="df59e-155">**Details**</span></span>|
   |---|---|---|
   |<span data-ttu-id="df59e-156">**Name**</span><span class="sxs-lookup"><span data-stu-id="df59e-156">**Name**</span></span>|<span data-ttu-id="df59e-157">AdatumAppGatewayVNET</span><span class="sxs-lookup"><span data-stu-id="df59e-157">AdatumAppGatewayVNET</span></span>|<span data-ttu-id="df59e-158">Application Gateway의 이름</span><span class="sxs-lookup"><span data-stu-id="df59e-158">Name of the application gateway</span></span>|
   |<span data-ttu-id="df59e-159">**주소 공간**</span><span class="sxs-lookup"><span data-stu-id="df59e-159">**Address Space**</span></span>|<span data-ttu-id="df59e-160">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="df59e-160">10.0.0.0/16</span></span>|<span data-ttu-id="df59e-161">가상 네트워크에 대한 주소 공간</span><span class="sxs-lookup"><span data-stu-id="df59e-161">This is the address space for the virtual network</span></span>|
   |<span data-ttu-id="df59e-162">**서브넷 이름**</span><span class="sxs-lookup"><span data-stu-id="df59e-162">**Subnet name**</span></span>|<span data-ttu-id="df59e-163">AppGatewaySubnet</span><span class="sxs-lookup"><span data-stu-id="df59e-163">AppGatewaySubnet</span></span>|<span data-ttu-id="df59e-164">Application Gateway의 서브넷 이름</span><span class="sxs-lookup"><span data-stu-id="df59e-164">Name of the subnet for the application gateway</span></span>|
   |<span data-ttu-id="df59e-165">**서브넷 주소 범위**</span><span class="sxs-lookup"><span data-stu-id="df59e-165">**Subnet address range**</span></span>|<span data-ttu-id="df59e-166">10.0.0.0/28</span><span class="sxs-lookup"><span data-stu-id="df59e-166">10.0.0.0/28</span></span>|<span data-ttu-id="df59e-167">이 서브넷을 사용하면 백 엔드 풀 멤버가 가상 네트워크에서 추가 서브넷을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-167">This subnet allows more additional subnets in the virtual network for backend pool members</span></span>|

1. <span data-ttu-id="df59e-168">**설정** 블레이드의 **프런트 엔드 IP 구성** 아래에서 **IP 주소 유형**으로 **공용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-168">On the **Settings** blade under **Frontend IP configuration**, choose **Public** as the **IP address type**</span></span>

1. <span data-ttu-id="df59e-169">**설정** 블레이드의 **공용 IP 주소** 아래에서 **공용 IP 주소 선택**을 클릭하여 **공용 IP 주소 선택** 블레이드를 열고, **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-169">On the **Settings** blade under **Public IP address** click **Choose a public IP address**, the **Choose public IP address** blade opens, click **Create new**.</span></span>

   ![공용 IP 선택][3]

1. <span data-ttu-id="df59e-171">**공용 IP 주소 만들기** 블레이드에서 기본값을 그대로 적용하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-171">On the **Create public IP address** blade, accept the default value, and click **OK**.</span></span> <span data-ttu-id="df59e-172">블레이드를 닫고 **공용 IP 주소**를 선택된 공용 IP 주소로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-172">The blade closes and populates the **Public IP address** with the public IP address chosen.</span></span>

1. <span data-ttu-id="df59e-173">**설정** 블레이드의 **수신기 구성** 아래에서 **프로토콜** 아래에 있는 **HTTP**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-173">On the **Settings** blade under **Listener configuration**, click **HTTP** under **Protocol**.</span></span> <span data-ttu-id="df59e-174">**포트** 필드에 사용할 포트를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-174">Enter the port to use in the **Port** field.</span></span>

2. <span data-ttu-id="df59e-175">**설정** 블레이드에서 **확인**을 클릭하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-175">Click **OK** on the **Settings** blade to continue.</span></span>

1. <span data-ttu-id="df59e-176">**요약** 블레이드에서 설정을 검토하고 **확인**을 클릭하여 Application Gateway 만들기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-176">Review the settings on the **Summary** blade and click **OK** to start creation of the application gateway.</span></span> <span data-ttu-id="df59e-177">응용 프로그램 게이트웨이 만들기는 장기 실행 작업이므로 완료하는 데 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-177">Creating an application gateway is a long running task and takes time to complete.</span></span>

## <a name="add-servers-to-backend-pools"></a><span data-ttu-id="df59e-178">백 엔드 풀에 서버 추가</span><span class="sxs-lookup"><span data-stu-id="df59e-178">Add servers to backend pools</span></span>

<span data-ttu-id="df59e-179">응용 프로그램 게이트웨이를 만든 후에는 부하 분산을 위해 응용 프로그램을 호스팅하는 시스템도 응용 프로그램 게이트웨이에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-179">Once you create the application gateway, the systems that host the application to be load balanced still need to be added to the application gateway.</span></span> <span data-ttu-id="df59e-180">이러한 서버의 IP 주소, FQDN 또는 NIC는 백 엔드 주소 풀에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-180">The IP addresses, FQDN, or NICs of these servers are added to the backend address pools.</span></span>

### <a name="ip-address-or-fqdn"></a><span data-ttu-id="df59e-181">IP 주소 또는 FQDN</span><span class="sxs-lookup"><span data-stu-id="df59e-181">IP Address or FQDN</span></span>

1. <span data-ttu-id="df59e-182">Application Gateway를 만든 후 Azure Portal의 **즐겨찾기** 창에서 **모든 리소스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-182">With the application gateway created, in the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="df59e-183">모든 리소스 블레이드에서 **AdatumAppGateway** Application Gateway를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-183">Click the **AdatumAppGateway** application gateway in the All resources blade.</span></span> <span data-ttu-id="df59e-184">선택한 구독에 이미 여러 개의 리소스가 있는 경우 **이름을 기준으로 필터링...**에 **AdatumAppGateway**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-184">If the subscription you selected already has several resources in it, you can enter **AdatumAppGateway** in the **Filter by name…**</span></span> <span data-ttu-id="df59e-185">응용 프로그램 게이트웨이에 간편하게 액세스할 수 있는 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-185">box to easily access the application gateway.</span></span>

1. <span data-ttu-id="df59e-186">만든 Application Gateway가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-186">The application gateway you created is displayed.</span></span> <span data-ttu-id="df59e-187">**백 엔드 풀**을 클릭하고 현재 백 엔드 풀인 **appGatewayBackendPool**을 선택합니다. 그러면 **appGatewayBackendPool** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-187">Click **Backend pools**, and select the current backend pool **appGatewayBackendPool**, the **appGatewayBackendPool** blade opens.</span></span>

   ![Application Gateway 백 엔드 풀][4]

1. <span data-ttu-id="df59e-189">**대상 추가**를 클릭하여 FQDN 값의 IP 주소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-189">Click **Add Target** to add IP addresses of FQDN values.</span></span> <span data-ttu-id="df59e-190">**IP 주소 또는 FQDN**을 **형식**으로 선택하고 필드에 IP 주소 또는 FQDN을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-190">Choose **IP address or FQDN** as the **Type** and enter your IP address or FQDN in the field.</span></span> <span data-ttu-id="df59e-191">추가 백 엔드 풀 멤버에 대해 이 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-191">Repeat this step for additional backend pool members.</span></span> <span data-ttu-id="df59e-192">완료하면 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-192">When done click **Save**.</span></span>

### <a name="virtual-machine-and-nic"></a><span data-ttu-id="df59e-193">가상 컴퓨터 및 NIC</span><span class="sxs-lookup"><span data-stu-id="df59e-193">Virtual Machine and NIC</span></span>

<span data-ttu-id="df59e-194">백 엔드 풀 구성원으로 가상 컴퓨터 NIC를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-194">You can also add Virtual Machine NICs as backend pool members.</span></span> <span data-ttu-id="df59e-195">Application Gateway로써 같은 가상 네트워크에 있는 가상 컴퓨터만 드롭다운을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-195">Only virtual machines within the same virtual network as the Application Gateway are available through the dropdown.</span></span>

1. <span data-ttu-id="df59e-196">Application Gateway를 만든 후 Azure Portal의 **즐겨찾기** 창에서 **모든 리소스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-196">With the application gateway created, in the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="df59e-197">모든 리소스 블레이드에서 **AdatumAppGateway** Application Gateway를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-197">Click the **AdatumAppGateway** application gateway in the All resources blade.</span></span> <span data-ttu-id="df59e-198">선택한 구독에 이미 여러 개의 리소스가 있는 경우 **이름을 기준으로 필터링...**에 **AdatumAppGateway**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-198">If the subscription you selected already has several resources in it, you can enter **AdatumAppGateway** in the **Filter by name…**</span></span> <span data-ttu-id="df59e-199">응용 프로그램 게이트웨이에 간편하게 액세스할 수 있는 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-199">box to easily access the application gateway.</span></span>

1. <span data-ttu-id="df59e-200">만든 Application Gateway가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-200">The application gateway you created is displayed.</span></span> <span data-ttu-id="df59e-201">**백 엔드 풀**을 클릭하고 현재 백 엔드 풀인 **appGatewayBackendPool**을 선택합니다. 그러면 **appGatewayBackendPool** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-201">Click **Backend pools**, and select the current backend pool **appGatewayBackendPool**, the **appGatewayBackendPool** blade opens.</span></span>

   ![Application Gateway 백 엔드 풀][5]

1. <span data-ttu-id="df59e-203">**대상 추가**를 클릭하여 FQDN 값의 IP 주소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-203">Click **Add Target** to add IP addresses of FQDN values.</span></span> <span data-ttu-id="df59e-204">**가상 컴퓨터**를 **형식**으로 선택하고 사용할 가상 컴퓨터 및 NIC를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-204">Choose **Virtual Machine** as the **Type** and select the virtual machine and NIC to use.</span></span> <span data-ttu-id="df59e-205">완료하면 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-205">When done click **Save**</span></span>

   > [!NOTE]
   > <span data-ttu-id="df59e-206">Application Gateway와 같은 가상 네트워크에 있는 가상 컴퓨터만 드롭다운 상자를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-206">Only virtual machines in the same virtual network as the application gateway are available in the drop down box.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="df59e-207">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="df59e-207">Clean up resources</span></span>

<span data-ttu-id="df59e-208">더 이상 필요하지 않은 리소스 그룹, 가상 컴퓨터 및 모든 관련 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-208">When no longer needed, delete the resource group, application gateway, and all related resources.</span></span> <span data-ttu-id="df59e-209">이렇게 하려면 응용 프로그램 게이트웨이 블레이드에서 해당 리소스 그룹을 선택하고 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-209">To do so, select the resource group from the application gateway blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df59e-210">다음 단계</span><span class="sxs-lookup"><span data-stu-id="df59e-210">Next steps</span></span>

<span data-ttu-id="df59e-211">이 시나리오에서는 응용 프로그램 게이트웨이를 배포하고 서버를 백 엔드에 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-211">In this scenario, you deployed an application gateway and added a server to the backend.</span></span> <span data-ttu-id="df59e-212">다음 단계에서는 설정을 수정하고, 게이트웨이의 규칙을 조정하여 Application Gateway를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-212">The next steps are to configure the application gateway by modifying settings, and adjusting rules in the gateway.</span></span> <span data-ttu-id="df59e-213">이러한 단계는 다음 문서에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-213">These steps can be found by visiting the following articles:</span></span>

<span data-ttu-id="df59e-214">[사용자 지정 상태 프로브 만들기](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="df59e-214">Learn how to create custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="df59e-215">[SSL 오프로드 구성](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="df59e-215">Learn how to configure SSL Offloading and take the costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

<span data-ttu-id="df59e-216">응용 프로그램 게이트웨이의 기능인 [웹 응용 프로그램 방화벽](application-gateway-webapplicationfirewall-overview.md)을 사용하여 웹 사이트를 보호하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="df59e-216">Learn how to protect your applications with [Web Application Firewall](application-gateway-webapplicationfirewall-overview.md) a feature of application gateway.</span></span>

<!--Image references-->
[1]: ./media/application-gateway-create-gateway-portal/figure1.png
[2]: ./media/application-gateway-create-gateway-portal/figure2.png
[3]: ./media/application-gateway-create-gateway-portal/figure3.png
[4]: ./media/application-gateway-create-gateway-portal/figure4.png
[5]: ./media/application-gateway-create-gateway-portal/figure5.png
[scenario]: ./media/application-gateway-create-gateway-portal/scenario.png
