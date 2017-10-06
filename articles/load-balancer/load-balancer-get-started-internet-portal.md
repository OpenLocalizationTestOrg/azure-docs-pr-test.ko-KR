---
title: "aaaCreate 인터넷 연결 부하 분산 장치-Azure 포털 | Microsoft Docs"
description: "Toocreate 인터넷 연결 부하 분산 장치 리소스 관리자를 사용 하 여 Azure 포털을 hello 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: 390ba8ec1474c54cf2c0022c4a3c219d21b1a659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-hello-azure-portal"></a><span data-ttu-id="b4630-103">Hello Azure 포털을 사용 하 여 인터넷 연결 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="b4630-103">Creating an Internet-facing load balancer using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b4630-104">포털</span><span class="sxs-lookup"><span data-stu-id="b4630-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="b4630-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b4630-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="b4630-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b4630-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="b4630-107">템플릿</span><span class="sxs-lookup"><span data-stu-id="b4630-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="b4630-108">이 문서에서는 hello 리소스 관리자 배포 모델에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="b4630-109">수도 있습니다 [toocreate 인터넷 연결 부하 분산 장치 클래식 배포를 사용 하는 방법에 대해 알아봅니다](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="b4630-109">You can also [Learn how toocreate an Internet-facing load balancer using classic deployment](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

<span data-ttu-id="b4630-110">이 설명 hello 일련의 개별 태스크 수행 toobe toocreate 부하 분산 장치 및 tooaccomplish hello 목표 수행 되는 내용을 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-110">This covers hello sequence of individual tasks that have toobe done toocreate a load balancer and explain in detail what is being done tooaccomplish hello goal.</span></span>

## <a name="what-is-required-toocreate-an-internet-facing-load-balancer"></a><span data-ttu-id="b4630-111">필요한 toocreate 인터넷 연결 부하 분산 장치는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="b4630-111">What is required toocreate an Internet-facing load balancer?</span></span>

<span data-ttu-id="b4630-112">Toocreate 필요 하 고이 정보를 개체 toodeploy 부하 분산 장치 뒤 hello를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-112">You need toocreate and configure hello following objects toodeploy a load balancer.</span></span>

* <span data-ttu-id="b4630-113">프런트 엔드 IP 구성 - 들어오는 네트워크 트래픽에 대한 공용 IP 주소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-113">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="b4630-114">백 엔드 주소 풀-hello hello 부하 분산 장치에서 가상 컴퓨터 tooreceive 네트워크 트래픽에 대 한 Nic (네트워크 인터페이스)를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-114">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="b4630-115">부하 분산 규칙-hello 백 엔드 주소 풀의 부하 분산 장치 tooport hello에 공용 포트 매핑 규칙을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-115">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="b4630-116">인바운드 NAT 규칙-hello hello 백 엔드 주소 풀에서 특정 가상 컴퓨터에 대 한 부하 분산 장치 tooa 포트에 공용 포트 매핑 규칙을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-116">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="b4630-117">프로브-hello 백 엔드 주소 풀에 있는 가상 컴퓨터 인스턴스의 사용 된 검색 toocheck 가용성 상태를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-117">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="b4630-118">Azure 리소스 관리자의 분산 장치 구성 요소에 대한 자세한 내용은 [부하 분산 장치에 대한 Azure 리소스 관리자 지원](load-balancer-arm.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-118">You can get more information about load balancer components with Azure Resource Manager at [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-a-load-balancer-in-azure-portal"></a><span data-ttu-id="b4630-119">Azure 포털에서 부하 분산 장치 설정</span><span class="sxs-lookup"><span data-stu-id="b4630-119">Set up a load balancer in Azure portal</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4630-120">이 예제에서는 **myVNet**이라는 가상 네트워크가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-120">This example assumes you have a virtual network called **myVNet**.</span></span> <span data-ttu-id="b4630-121">너무 참조[가상 네트워크 만들기](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) toodo이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-121">Refer too[create virtual network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) toodo this.</span></span> <span data-ttu-id="b4630-122">또한 내에 있는 서브넷은 가정 **myVNet** 호출 **LB 서브넷 수** 두 vm이 호출 **web1** 및 **web2** 각각 내 동일한 가용성 집합 이라는 hello **myAvailSet** 에 **myVNet**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-122">It also assumes there is a subnet within **myVNet** called **LB-Subnet-BE** and two VMs called **web1** and **web2** respectively within hello same availability set called **myAvailSet** in **myVNet**.</span></span> <span data-ttu-id="b4630-123">너무 참조[이 링크](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toocreate Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-123">Refer too[this link](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toocreate VMs.</span></span>

1. <span data-ttu-id="b4630-124">브라우저에서 Azure 포털 toohello 이동: [http://portal.azure.com](http://portal.azure.com) 및 Azure 계정으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-124">From a browser navigate toohello Azure portal: [http://portal.azure.com](http://portal.azure.com) and login with your Azure account.</span></span>
2. <span data-ttu-id="b4630-125">Hello의 왼쪽 위에 hello 화면에 선택 **새로** > **네트워킹** > **부하 분산 장치입니다.**</span><span class="sxs-lookup"><span data-stu-id="b4630-125">On hello top left-hand side of hello screen select **New** > **Networking** > **Load Balancer.**</span></span>
3. <span data-ttu-id="b4630-126">Hello에 **부하 분산 장치 만들기** 블레이드, 부하 분산 장치에 대 한 이름 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-126">In hello **Create load balancer** blade, type a name for your load balancer.</span></span> <span data-ttu-id="b4630-127">여기서는 **myLoadBalancer**라고 지칭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-127">Here it is called **myLoadBalancer**.</span></span>
4. <span data-ttu-id="b4630-128">**형식**에서 **Public**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-128">Under **Type**, select **Public**.</span></span>
5. <span data-ttu-id="b4630-129">**공용 IP 주소** 아래에서 **myPublicIP**이라는 새 공용 IP를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-129">Under **Public IP address**, create a new public IP called **myPublicIP**.</span></span>
6. <span data-ttu-id="b4630-130">리소스 그룹에서 **myRG**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-130">Under Resource Group, select **myRG**.</span></span> <span data-ttu-id="b4630-131">그런 다음 해당 **위치**를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-131">Then select an appropriate **Location**, and then click **OK**.</span></span> <span data-ttu-id="b4630-132">hello 부하 분산 장치 다음 toodeploy를 시작 및 toosuccessfully 완전 한 배포는 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-132">hello load balancer will then start toodeploy and will take a few minutes toosuccessfully complete deployment.</span></span>

    ![부하 분산 장치에 대한 리소스 그룹 업데이트](./media/load-balancer-get-started-internet-portal/1-load-balancer.png)

## <a name="create-a-back-end-address-pool"></a><span data-ttu-id="b4630-134">백 엔드 주소 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="b4630-134">Create a back-end address pool</span></span>

1. <span data-ttu-id="b4630-135">부하 분산 장치가 성공적으로 배포되면 리소스 내에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-135">Once your load balancer has successfully deployed, select it from within your resources.</span></span> <span data-ttu-id="b4630-136">설정에서 백 엔드 풀을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-136">Under settings, select Backend Pools.</span></span> <span data-ttu-id="b4630-137">백 엔드 풀의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-137">Type a name for your backend pool.</span></span> <span data-ttu-id="b4630-138">Hello 클릭 **추가** 단추 맨 위에서 hello hello 블레이드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-138">Then click on hello **Add** button toward hello top of hello blade that shows up.</span></span>
2. <span data-ttu-id="b4630-139">클릭 **가상 컴퓨터 추가** hello에 **백 엔드 풀 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-139">Click on **Add a virtual machine** in hello **Add backend pool** blade.</span></span>  <span data-ttu-id="b4630-140">**가용성 집합** 아래에서 **가용성 집합**을 선택하고 **myAvailSet**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-140">Select **Choose an availability set** under **Availability set** and select **myAvailSet**.</span></span> <span data-ttu-id="b4630-141">다음으로, 선택 **hello 가상 컴퓨터를 선택할** 아래에서 가상 컴퓨터 섹션 hello 블레이드 hello을 클릭할 **web1** 및 **web2**, 부하 분산을 위해 만든 두 개의 Vm hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-141">Next, select **Choose hello virtual machines** under hello Virtual Machines section in hello blade and click on **web1** and **web2**, hello two VMs created for load balancing.</span></span> <span data-ttu-id="b4630-142">파란색 확인 표시가 toohello hello 이미지 아래에 나와 있는 것 처럼 왼쪽 모두 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-142">Ensure that both have blue check marks toohello left as shown in hello image below.</span></span> <span data-ttu-id="b4630-143">클릭 **선택** hello에 확인 뒤 해당 블레이드에서 **선택 가상 컴퓨터** 블레이드 차례로 **확인** hello에 **백 엔드 풀 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-143">Then, click **Select** in that blade followed by OK in hello **Choose Virtual machines** blade and then **OK** in hello **Add backend pool** blade.</span></span>

    ![<span data-ttu-id="b4630-144">Toohello 백 엔드 주소 풀-추가</span><span class="sxs-lookup"><span data-stu-id="b4630-144">Adding toohello backend address pool -</span></span> ](./media/load-balancer-get-started-internet-portal/3-load-balancer-backend-02.png)

3. <span data-ttu-id="b4630-145">Toomake 알림에 드롭다운 목록에 있는지에 대 한 업데이트 확인 Vm hello 둘 다에 대 한 추가 tooupdating hello 네트워크 인터페이스에 hello 부하 분산 장치 백 엔드 풀 저장에 관한 **web1** 및 **web2**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-145">Check toomake sure your notifications drop down list has an update regarding saving hello load balancer backend pool in addition tooupdating hello network interface for both hello VMs **web1** and **web2**.</span></span>

## <a name="create-a-probe-lb-rule-and-nat-rules"></a><span data-ttu-id="b4630-146">프로브, LB 규칙 및 NAT 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="b4630-146">Create a probe, LB rule, and NAT rules</span></span>

1. <span data-ttu-id="b4630-147">상태 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-147">Create a health probe.</span></span>

    <span data-ttu-id="b4630-148">부하 분산 장치의 설정에서 프로브를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-148">Under Settings of your load balancer, select Probes.</span></span> <span data-ttu-id="b4630-149">클릭 **추가** hello hello 블레이드 위쪽에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-149">Then click **Add** located at hello top of hello blade.</span></span>

    <span data-ttu-id="b4630-150">두 가지 방법으로 tooconfigure는 프로브는: HTTP 또는 TCP입니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-150">There are two ways tooconfigure a probe: HTTP or TCP.</span></span> <span data-ttu-id="b4630-151">이 예제에서는 HTTP가 표시되지만 TCP도 비슷한 방식으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-151">This example shows HTTP, but TCP can be configured in a similar manner.</span></span>
    <span data-ttu-id="b4630-152">Hello 필요한 정보를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-152">Update hello necessary information.</span></span> <span data-ttu-id="b4630-153">설명대로 **myLoadBalancer**가 포트 80에서 트래픽 로드를 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-153">As mentioned, **myLoadBalancer** will load balance traffic on Port 80.</span></span> <span data-ttu-id="b4630-154">선택한 hello 경로 HealthProbe.aspx 간격은 15 초 있고, 비정상 임계값은 2입니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-154">hello path selected is HealthProbe.aspx, Interval is 15 seconds, and Unhealthy threshold is 2.</span></span> <span data-ttu-id="b4630-155">완료 되 면 클릭 **확인** toocreate hello 프로브 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-155">Once finished, click **OK** toocreate hello probe.</span></span>

    <span data-ttu-id="b4630-156">'I' hello 아이콘 toolearn 이러한 개별 구성 및 변경 된 toocater tooyour 요구 사항을 수 있는 방법에 대 한 자세한 위로 마우스 포인터를 가져갑니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-156">Hover your pointer over hello 'i' icon toolearn more about these individual configurations and how they can be changed toocater tooyour requirements.</span></span>

    ![프로브 추가](./media/load-balancer-get-started-internet-portal/4-load-balancer-probes.png)

2. <span data-ttu-id="b4630-158">부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-158">Create a load balancer rule.</span></span>

    <span data-ttu-id="b4630-159">설정 섹션의 부하 분산 장치 부하 분산 규칙 hello에서 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-159">Click on Load balancing rules in hello Settings section of your load balancer.</span></span> <span data-ttu-id="b4630-160">Hello 새 블레이드에서 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-160">In hello new blade, click on **Add**.</span></span> <span data-ttu-id="b4630-161">규칙 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-161">Name your rule.</span></span> <span data-ttu-id="b4630-162">여기서는 HTTP입니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-162">Here, it is HTTP.</span></span> <span data-ttu-id="b4630-163">Hello 프런트 엔드 포트와 백 엔드 포트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-163">Choose hello frontend port and Backend port.</span></span> <span data-ttu-id="b4630-164">여기서는 둘 다에 대해 80이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-164">Here, 80 is chosen for both.</span></span> <span data-ttu-id="b4630-165">선택 **LB 백 엔드** 백 엔드 풀 및 이전에 만든 hello와 **HealthProbe** 프로브 hello으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-165">Choose **LB-backend** as your Backend pool and hello previously created **HealthProbe** as hello Probe.</span></span> <span data-ttu-id="b4630-166">Tooyour 요구 사항에 따라 다른 구성은 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-166">Other configurations can be set according tooyour requirements.</span></span> <span data-ttu-id="b4630-167">확인 toosave hello 부하 분산 규칙을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-167">Then click OK toosave hello load balancing rule.</span></span>

    ![부하 분산 규칙 추가](./media/load-balancer-get-started-internet-portal/5-load-balancing-rules.png)

3. <span data-ttu-id="b4630-169">인바운드 NAT 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="b4630-169">Create inbound NAT rules</span></span>

    <span data-ttu-id="b4630-170">부하 분산 장치의 hello 설정 섹션에서 인바운드 NAT 규칙을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-170">Click on Inbound NAT rules under hello settings section of your load balancer.</span></span> <span data-ttu-id="b4630-171">클릭 하는 hello 새 블레이드에서 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-171">In hello new blade that, click **Add**.</span></span> <span data-ttu-id="b4630-172">인바운드 NAT 규칙의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-172">Then name your inbound NAT rule.</span></span> <span data-ttu-id="b4630-173">여기서는 **inboundNATrule1**입니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-173">Here it is called **inboundNATrule1**.</span></span> <span data-ttu-id="b4630-174">hello 대상은 공용 IP가 이전에 만든 hello 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-174">hello destination should be hello Public IP previously created.</span></span> <span data-ttu-id="b4630-175">서비스에서 사용자 지정을 선택 하 고 원하는 toouse hello 프로토콜을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-175">Select Custom under Service and select hello protocol you would like toouse.</span></span> <span data-ttu-id="b4630-176">여기서는 TCP가 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-176">Here TCP is selected.</span></span> <span data-ttu-id="b4630-177">3441, hello 포트를 입력 하 고 대상 포트,이 경우 3389 hello 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-177">Enter hello port, 3441, and hello Target port, in this case, 3389.</span></span> <span data-ttu-id="b4630-178">이 규칙 확인 toosave 키를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-178">then click OK toosave this rule.</span></span>

    <span data-ttu-id="b4630-179">Hello 첫 번째 규칙을 만든 후 hello 두 번째 인바운드 NAT 규칙 포트 3442 tooTarget 포트 3389에서에서 inboundNATrule2 호출에 대해이 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-179">Once hello first rule is created, repeat this step for hello second inbound NAT rule called inboundNATrule2 from port 3442 tooTarget port 3389.</span></span>

    ![인바운드 NAT 규칙 추가](./media/load-balancer-get-started-internet-portal/6-load-balancer-inbound-nat-rules.png)

## <a name="remove-a-load-balancer"></a><span data-ttu-id="b4630-181">부하 분산 장치 제거하기</span><span class="sxs-lookup"><span data-stu-id="b4630-181">Remove a Load Balancer</span></span>

<span data-ttu-id="b4630-182">toodelete 선택 hello 부하 분산 장치 부하 분산 장치 tooremove 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-182">toodelete a load balancer, select hello load balancer you want tooremove.</span></span> <span data-ttu-id="b4630-183">Hello에 *부하 분산 장치* 블레이드를 클릭 **삭제** hello hello 블레이드 위쪽에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-183">In hello *Load Balancer* blade, click on **Delete** located at hello top of hello blade.</span></span> <span data-ttu-id="b4630-184">그런 후 확인할지 묻는 메시지가 표시되면 **예** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4630-184">Then select **Yes** when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4630-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b4630-185">Next steps</span></span>

[<span data-ttu-id="b4630-186">내부 부하 분산 장치 구성 시작</span><span class="sxs-lookup"><span data-stu-id="b4630-186">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="b4630-187">부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="b4630-187">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="b4630-188">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="b4630-188">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
