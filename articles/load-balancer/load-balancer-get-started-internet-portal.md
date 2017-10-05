---
title: "인터넷 연결 부하 분산 장치 만들기 - Azure Portal | Microsoft Docs"
description: "Azure 포털을 사용하여 Resource Manager에서 인터넷 연결 부하 분산 장치를 만드는 방법에 대해 알아봅니다."
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: aa9d26ca-3d8a-4a99-83b7-c410dd20b9d0
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: annahar
ms.openlocfilehash: db7c328b2ba7008b9d34275341fa4bad9522b028
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-the-azure-portal"></a><span data-ttu-id="49cc8-103">Azure 포털을 사용하여 인터넷 연결 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="49cc8-103">Creating an Internet-facing load balancer using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="49cc8-104">포털</span><span class="sxs-lookup"><span data-stu-id="49cc8-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="49cc8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="49cc8-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="49cc8-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="49cc8-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="49cc8-107">템플릿</span><span class="sxs-lookup"><span data-stu-id="49cc8-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="49cc8-108">이 문서에서는 Resource Manager 배포 모델에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="49cc8-109">또한 [클래식 배포를 사용하여 인터넷 연결 부하 분산 장치를 만드는 방법을 배울 수 있습니다](load-balancer-get-started-internet-classic-portal.md).</span><span class="sxs-lookup"><span data-stu-id="49cc8-109">You can also [Learn how to create an Internet-facing load balancer using classic deployment](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

<span data-ttu-id="49cc8-110">부하 분산 장치를 만들기 위해 수행되는 개별 작업의 순서를 알아보고 부하 분산 장치를 만들기 위해 수행해야 하는 작업을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-110">This covers the sequence of individual tasks that have to be done to create a load balancer and explain in detail what is being done to accomplish the goal.</span></span>

## <a name="what-is-required-to-create-an-internet-facing-load-balancer"></a><span data-ttu-id="49cc8-111">인터넷 연결 부하 분산 장치를 만드는 데 필요한 항목은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="49cc8-111">What is required to create an Internet-facing load balancer?</span></span>

<span data-ttu-id="49cc8-112">부하 분산 장치를 배포하려면 다음 개체를 만들고 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-112">You need to create and configure the following objects to deploy a load balancer.</span></span>

* <span data-ttu-id="49cc8-113">프런트 엔드 IP 구성 - 들어오는 네트워크 트래픽에 대한 공용 IP 주소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-113">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="49cc8-114">백 엔드 주소 풀 - 부하 분산 장치의 네트워크 트래픽을 받는 가상 컴퓨터에 대한 NIC(네트워크 인터페이스)를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-114">Back-end address pool - contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="49cc8-115">부하 분산 규칙 - 백 엔드 주소 풀에 있는 포트에 부하 분산 장치의 공용 포트를 매핑하는 규칙을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-115">Load balancing rules - contains rules mapping a public port on the load balancer to port in the back-end address pool.</span></span>
* <span data-ttu-id="49cc8-116">인바운드 NAT 규칙 - 백 엔드 주소 풀에 있는 특정 가상 컴퓨터에 대한 포트에 부하 분산 장치의 공용 포트를 매핑하는 규칙을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-116">Inbound NAT rules - contains rules mapping a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="49cc8-117">프로브 - 백 엔드 주소 풀의 가상 컴퓨터 인스턴스의 가용성을 확인하는 데 사용하는 상태 프로브를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-117">Probes - contains health probes used to check availability of virtual machines instances in the back-end address pool.</span></span>

<span data-ttu-id="49cc8-118">Azure 리소스 관리자의 분산 장치 구성 요소에 대한 자세한 내용은 [부하 분산 장치에 대한 Azure 리소스 관리자 지원](load-balancer-arm.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-118">You can get more information about load balancer components with Azure Resource Manager at [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-a-load-balancer-in-azure-portal"></a><span data-ttu-id="49cc8-119">Azure 포털에서 부하 분산 장치 설정</span><span class="sxs-lookup"><span data-stu-id="49cc8-119">Set up a load balancer in Azure portal</span></span>

> [!IMPORTANT]
> <span data-ttu-id="49cc8-120">이 예제에서는 **myVNet**이라는 가상 네트워크가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-120">This example assumes you have a virtual network called **myVNet**.</span></span> <span data-ttu-id="49cc8-121">이렇게 하려면 [가상 네트워크 만들기](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="49cc8-121">Refer to [create virtual network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) to do this.</span></span> <span data-ttu-id="49cc8-122">또한 **myVNet** 내에 **LB-Subnet-BE**라는 서브넷이 있고 **web1** 및 **web2**라는 2개의 VM이 **myVNet**의 **myAvailSet**이라는 동일한 가용성 집합 내에 각각 포함되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-122">It also assumes there is a subnet within **myVNet** called **LB-Subnet-BE** and two VMs called **web1** and **web2** respectively within the same availability set called **myAvailSet** in **myVNet**.</span></span> <span data-ttu-id="49cc8-123">VM을 만들려면 [이 링크](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="49cc8-123">Refer to [this link](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to create VMs.</span></span>

1. <span data-ttu-id="49cc8-124">브라우저에서 Azure 포털 [http://portal.azure.com](http://portal.azure.com) 으로 이동하고 Azure 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-124">From a browser navigate to the Azure portal: [http://portal.azure.com](http://portal.azure.com) and login with your Azure account.</span></span>
2. <span data-ttu-id="49cc8-125">화면 왼쪽 상단에서 **새로 만들기** > **네트워킹** > **부하 분산 장치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-125">On the top left-hand side of the screen select **New** > **Networking** > **Load Balancer.**</span></span>
3. <span data-ttu-id="49cc8-126">**부하 분산 장치 만들기** 블레이드에서 부하 분산 장치의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-126">In the **Create load balancer** blade, type a name for your load balancer.</span></span> <span data-ttu-id="49cc8-127">여기서는 **myLoadBalancer**라고 지칭합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-127">Here it is called **myLoadBalancer**.</span></span>
4. <span data-ttu-id="49cc8-128">**형식**에서 **Public**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-128">Under **Type**, select **Public**.</span></span>
5. <span data-ttu-id="49cc8-129">**공용 IP 주소** 아래에서 **myPublicIP**이라는 새 공용 IP를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-129">Under **Public IP address**, create a new public IP called **myPublicIP**.</span></span>
6. <span data-ttu-id="49cc8-130">리소스 그룹에서 **myRG**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-130">Under Resource Group, select **myRG**.</span></span> <span data-ttu-id="49cc8-131">그런 다음 해당 **위치**를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-131">Then select an appropriate **Location**, and then click **OK**.</span></span> <span data-ttu-id="49cc8-132">부하 분산 장치는 배포를 시작하며 배포를 성공적으로 완료하는 데 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-132">The load balancer will then start to deploy and will take a few minutes to successfully complete deployment.</span></span>

    ![부하 분산 장치에 대한 리소스 그룹 업데이트](./media/load-balancer-get-started-internet-portal/1-load-balancer.png)

## <a name="create-a-back-end-address-pool"></a><span data-ttu-id="49cc8-134">백 엔드 주소 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="49cc8-134">Create a back-end address pool</span></span>

1. <span data-ttu-id="49cc8-135">부하 분산 장치가 성공적으로 배포되면 리소스 내에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-135">Once your load balancer has successfully deployed, select it from within your resources.</span></span> <span data-ttu-id="49cc8-136">설정에서 백 엔드 풀을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-136">Under settings, select Backend Pools.</span></span> <span data-ttu-id="49cc8-137">백 엔드 풀의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-137">Type a name for your backend pool.</span></span> <span data-ttu-id="49cc8-138">표시되는 블레이드 위쪽의 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-138">Then click on the **Add** button toward the top of the blade that shows up.</span></span>
2. <span data-ttu-id="49cc8-139">**백 엔드 풀 추가** 블레이드에서 **가상 컴퓨터 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-139">Click on **Add a virtual machine** in the **Add backend pool** blade.</span></span>  <span data-ttu-id="49cc8-140">**가용성 집합** 아래에서 **가용성 집합**을 선택하고 **myAvailSet**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-140">Select **Choose an availability set** under **Availability set** and select **myAvailSet**.</span></span> <span data-ttu-id="49cc8-141">다음으로, 블레이드의 가상 컴퓨터 섹션에서 **가상 컴퓨터 선택**을 선택하고 부하 분산을 위해 만들어진 두 개의 VM인 **web 1** 및 **web2**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-141">Next, select **Choose the virtual machines** under the Virtual Machines section in the blade and click on **web1** and **web2**, the two VMs created for load balancing.</span></span> <span data-ttu-id="49cc8-142">아래 이미지에 표시된 대로 있는 왼쪽의 파란색 확인 표시를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-142">Ensure that both have blue check marks to the left as shown in the image below.</span></span> <span data-ttu-id="49cc8-143">**가상 컴퓨터 선택** 블레이드에서 확인을 클릭한 후 **선택**을 클릭한 다음 **백 엔드 풀 추가** 블레이드에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-143">Then, click **Select** in that blade followed by OK in the **Choose Virtual machines** blade and then **OK** in the **Add backend pool** blade.</span></span>

    ![<span data-ttu-id="49cc8-144">백 엔드 주소 풀에 추가</span><span class="sxs-lookup"><span data-stu-id="49cc8-144">Adding to the backend address pool -</span></span> ](./media/load-balancer-get-started-internet-portal/3-load-balancer-backend-02.png)

3. <span data-ttu-id="49cc8-145">알림 드롭다운 목록에 **web1** 및 **web2** 둘 다에 대한 네트워크 인터페이스 업데이트 외에 부하 분산 장치 백 엔드 풀 저장과 관련된 업데이트가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-145">Check to make sure your notifications drop down list has an update regarding saving the load balancer backend pool in addition to updating the network interface for both the VMs **web1** and **web2**.</span></span>

## <a name="create-a-probe-lb-rule-and-nat-rules"></a><span data-ttu-id="49cc8-146">프로브, LB 규칙 및 NAT 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="49cc8-146">Create a probe, LB rule, and NAT rules</span></span>

1. <span data-ttu-id="49cc8-147">상태 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-147">Create a health probe.</span></span>

    <span data-ttu-id="49cc8-148">부하 분산 장치의 설정에서 프로브를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-148">Under Settings of your load balancer, select Probes.</span></span> <span data-ttu-id="49cc8-149">그런 후 블레이드 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-149">Then click **Add** located at the top of the blade.</span></span>

    <span data-ttu-id="49cc8-150">프로브를 구성하는 방법에는 HTTP 또는 TCP의 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-150">There are two ways to configure a probe: HTTP or TCP.</span></span> <span data-ttu-id="49cc8-151">이 예제에서는 HTTP가 표시되지만 TCP도 비슷한 방식으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-151">This example shows HTTP, but TCP can be configured in a similar manner.</span></span>
    <span data-ttu-id="49cc8-152">필요한 정보를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-152">Update the necessary information.</span></span> <span data-ttu-id="49cc8-153">설명대로 **myLoadBalancer**가 포트 80에서 트래픽 로드를 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-153">As mentioned, **myLoadBalancer** will load balance traffic on Port 80.</span></span> <span data-ttu-id="49cc8-154">선택한 경로는 HealthProbe.aspx이고, 간격은 15초이고, 비정상 임계값은 2입니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-154">The path selected is HealthProbe.aspx, Interval is 15 seconds, and Unhealthy threshold is 2.</span></span> <span data-ttu-id="49cc8-155">완료되면 **확인**을 클릭하여 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-155">Once finished, click **OK** to create the probe.</span></span>

    <span data-ttu-id="49cc8-156">'I' 아이콘 위에 포인터를 가져가 이러한 개별 구성 및 요구 사항에 맞게 변경하는 방법을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-156">Hover your pointer over the 'i' icon to learn more about these individual configurations and how they can be changed to cater to your requirements.</span></span>

    ![프로브 추가](./media/load-balancer-get-started-internet-portal/4-load-balancer-probes.png)

2. <span data-ttu-id="49cc8-158">부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-158">Create a load balancer rule.</span></span>

    <span data-ttu-id="49cc8-159">부하 분산 장치의 설정 섹션에서 부하 분산 규칙을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-159">Click on Load balancing rules in the Settings section of your load balancer.</span></span> <span data-ttu-id="49cc8-160">새 블레이드에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-160">In the new blade, click on **Add**.</span></span> <span data-ttu-id="49cc8-161">규칙 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-161">Name your rule.</span></span> <span data-ttu-id="49cc8-162">여기서는 HTTP입니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-162">Here, it is HTTP.</span></span> <span data-ttu-id="49cc8-163">프런트 엔드 포트 및 백 엔드 포트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-163">Choose the frontend port and Backend port.</span></span> <span data-ttu-id="49cc8-164">여기서는 둘 다에 대해 80이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-164">Here, 80 is chosen for both.</span></span> <span data-ttu-id="49cc8-165">백 엔드 풀로 **LB-backend**를 선택하고 프로브로는 이전에 만든 **HealthProbe**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-165">Choose **LB-backend** as your Backend pool and the previously created **HealthProbe** as the Probe.</span></span> <span data-ttu-id="49cc8-166">요구 사항에 따라 다른 구성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-166">Other configurations can be set according to your requirements.</span></span> <span data-ttu-id="49cc8-167">그런 후 확인을 클릭하여 부하 분산 규칙을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-167">Then click OK to save the load balancing rule.</span></span>

    ![부하 분산 규칙 추가](./media/load-balancer-get-started-internet-portal/5-load-balancing-rules.png)

3. <span data-ttu-id="49cc8-169">인바운드 NAT 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="49cc8-169">Create inbound NAT rules</span></span>

    <span data-ttu-id="49cc8-170">부하 분산 장치의 설정 섹션에서 인바운드 NAT 규칙을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-170">Click on Inbound NAT rules under the settings section of your load balancer.</span></span> <span data-ttu-id="49cc8-171">새 블레이드에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-171">In the new blade that, click **Add**.</span></span> <span data-ttu-id="49cc8-172">인바운드 NAT 규칙의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-172">Then name your inbound NAT rule.</span></span> <span data-ttu-id="49cc8-173">여기서는 **inboundNATrule1**입니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-173">Here it is called **inboundNATrule1**.</span></span> <span data-ttu-id="49cc8-174">대상은 이전에 만든 공용 IP여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-174">The destination should be the Public IP previously created.</span></span> <span data-ttu-id="49cc8-175">서비스에서 사용자 지정을 선택하고 사용하려는 프로토콜을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-175">Select Custom under Service and select the protocol you would like to use.</span></span> <span data-ttu-id="49cc8-176">여기서는 TCP가 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-176">Here TCP is selected.</span></span> <span data-ttu-id="49cc8-177">이 경우 포트 3441 및 대상 포트 3389를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-177">Enter the port, 3441, and the Target port, in this case, 3389.</span></span> <span data-ttu-id="49cc8-178">그런 후 확인을 클릭하여 이 규칙을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-178">then click OK to save this rule.</span></span>

    <span data-ttu-id="49cc8-179">첫 번째 규칙이 생성된 후 포트 3442에서 대상 포트 3389로의 inboundNATrule2라는 두 번째 인바운드 NAT 규칙에 대해 이 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-179">Once the first rule is created, repeat this step for the second inbound NAT rule called inboundNATrule2 from port 3442 to Target port 3389.</span></span>

    ![인바운드 NAT 규칙 추가](./media/load-balancer-get-started-internet-portal/6-load-balancer-inbound-nat-rules.png)

## <a name="remove-a-load-balancer"></a><span data-ttu-id="49cc8-181">부하 분산 장치 제거하기</span><span class="sxs-lookup"><span data-stu-id="49cc8-181">Remove a Load Balancer</span></span>

<span data-ttu-id="49cc8-182">부하 분산 장치를 삭제하려면 제거하려는 부하 분산 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-182">To delete a load balancer, select the load balancer you want to remove.</span></span> <span data-ttu-id="49cc8-183">*부하 분산 장치* 블레이드에서 블레이드의 맨위에 있는 **삭제** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-183">In the *Load Balancer* blade, click on **Delete** located at the top of the blade.</span></span> <span data-ttu-id="49cc8-184">그런 후 확인할지 묻는 메시지가 표시되면 **예** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="49cc8-184">Then select **Yes** when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49cc8-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="49cc8-185">Next steps</span></span>

[<span data-ttu-id="49cc8-186">내부 부하 분산 장치 구성 시작</span><span class="sxs-lookup"><span data-stu-id="49cc8-186">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="49cc8-187">부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="49cc8-187">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="49cc8-188">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="49cc8-188">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
