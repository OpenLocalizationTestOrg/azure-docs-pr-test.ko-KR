---
title: "클라우드 서비스에 대 한 Vip aaaMutiple"
description: "MultiVIP의 개요 및 방법을 tooset 여러 vip가 클라우드 서비스"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 85f6d26a-3df5-4b8e-96a1-92b2793b5284
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: b3e0f2b24968cb75a7064484a09ffe94505bb70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a><span data-ttu-id="6a393-103">클라우드 서비스당 여러 VIP 구성</span><span class="sxs-lookup"><span data-stu-id="6a393-103">Configure multiple VIPs for a cloud service</span></span>

<span data-ttu-id="6a393-104">Azure에서 제공 하는 IP 주소를 사용 하 여 공용 인터넷 hello를 통해 Azure 클라우드 서비스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-104">You can access Azure cloud services over hello public Internet by using an IP address provided by Azure.</span></span> <span data-ttu-id="6a393-105">이 공용 IP 주소는 참조 된 tooas VIP (가상 IP) toohello Azure 부하 분산 장치, 및 하지 hello 클라우드 서비스 내에서 가상 컴퓨터 (VM) 인스턴스를 hello 연결 되어 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-105">This public IP address is referred tooas a VIP (virtual IP) since it is linked toohello Azure load balancer, and not hello Virtual Machine (VM) instances within hello cloud service.</span></span> <span data-ttu-id="6a393-106">단일 VIP를 사용하여 클라우드 서비스 내의 모든 VM 인스턴스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-106">You can access any VM instance within a cloud service by using a single VIP.</span></span>

<span data-ttu-id="6a393-107">그러나 둘 이상의 VIP를 할 수 있는 시나리오가 있습니다. 항목 지점 toohello로 동일한 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-107">However, there are scenarios in which you may need more than one VIP as an entry point toohello same cloud service.</span></span> <span data-ttu-id="6a393-108">예를 들어, 클라우드 서비스 테 넌 트 나 각 사이트는 서로 다른 고객에 대 한 호스트 hello 기본 포트 443 사용 하 여 SSL 연결을 해야 하는 여러 웹 사이트를 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-108">For instance, your cloud service may host multiple websites that require SSL connectivity using hello default port of 443, as each site is hosted for a different customer, or tenant.</span></span> <span data-ttu-id="6a393-109">이 시나리오에서는 각 웹 사이트에 대 한 toohave는 다른 공용 IP 주소 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-109">In this scenario, you need toohave a different public facing IP address for each website.</span></span> <span data-ttu-id="6a393-110">hello 아래 다이어그램에서는 일반적인 다중 테 넌 트 웹 호스팅 필요한 동일 hello에 여러 SSL 인증서에 대 한 공용 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-110">hello diagram below illustrates a typical multi-tenant web hosting with a need for multiple SSL certificates on hello same public port.</span></span>

![다중 VIP SSL 시나리오](./media/load-balancer-multivip/Figure1.png)

<span data-ttu-id="6a393-112">위의 모든 Vip 사용 하 여 hello hello 예제에서 캡슐화 된 트래픽과 같은 공용 포트 (443)가 리디렉션된 tooone 또는 모든 hello 웹 사이트를 호스팅하는 hello 클라우드 서비스의 hello 내부 IP 주소에 대 한 고유한 개인 포트에 분산 된 Vm를 로드 하는 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-112">In hello example above, all VIPs use hello same public port (443) and traffic is redirected tooone or more load balanced VMs on a unique private port for hello internal IP address of hello cloud service hosting all hello websites.</span></span>

> [!NOTE]
> <span data-ttu-id="6a393-113">다른 상황 필요한 hello 사용 하 여 hello 여러 vip가 hello 동일한 가상 컴퓨터의 설정에서 여러 SQL AlwaysOn 가용성 그룹 수신기를 호스팅입니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-113">Another situation requiring hello use hello multiple VIPs is hosting multiple SQL AlwaysOn availability group listeners on hello same set of Virtual Machines.</span></span>

<span data-ttu-id="6a393-114">Vip는 hello 실제 IP 주소로 toohello 클라우드 서비스에 할당 된 시간이 지남에 따라 변경 될 수 있다는 의미는 기본적으로 동적입니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-114">VIPs are dynamic by default, which means that hello actual IP address assigned toohello cloud service may change over time.</span></span> <span data-ttu-id="6a393-115">기능을 예약할 수 있습니다 VIP를 서비스에 대 한 tooprevent 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-115">tooprevent that from happening, you can reserve a VIP for your service.</span></span> <span data-ttu-id="6a393-116">예약 된 Vip에 대해 자세히 toolearn 참조 [예약 된 공용 IP](../virtual-network/virtual-networks-reserved-public-ip.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-116">toolearn more about reserved VIPs, see [Reserved Public IP](../virtual-network/virtual-networks-reserved-public-ip.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6a393-117">VIP 및 예약된 IP의 가격에 대한 자세한 내용은 [IP 주소 가격](https://azure.microsoft.com/pricing/details/ip-addresses/) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a393-117">Please see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/) for information on pricing on VIPs and reserved IPs.</span></span>

<span data-ttu-id="6a393-118">PowerShell tooverify hello 클라우드 서비스에 사용 된 Vip를 사용 하 여으로 및 Vip 제거, VIP tooan 끝점 연결을 추가한 특정 VIP에서 부하 분산을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-118">You can use PowerShell tooverify hello VIPs used by your cloud services, as well as add and remove VIPs, associate a VIP tooan endpoint, and configure load balancing on a specific VIP.</span></span>

## <a name="limitations"></a><span data-ttu-id="6a393-119">제한 사항</span><span class="sxs-lookup"><span data-stu-id="6a393-119">Limitations</span></span>

<span data-ttu-id="6a393-120">이때 다중 VIP 기능은 다음 시나리오는 제한 된 toohello 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-120">At this time, Multi VIP functionality is limited toohello following scenarios:</span></span>

* <span data-ttu-id="6a393-121">**IaaS만**.</span><span class="sxs-lookup"><span data-stu-id="6a393-121">**IaaS only**.</span></span> <span data-ttu-id="6a393-122">VM을 포함하는 클라우드 서비스에 대해서 다중 VIP만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-122">You can only enable Multi VIP for cloud services that contain VMs.</span></span> <span data-ttu-id="6a393-123">PaaS 시나리오에서 역할 인스턴스와 함께 다중 VIP를 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-123">You cannot use Multi VIP in PaaS scenarios with role instances.</span></span>
* <span data-ttu-id="6a393-124">**PowerShell만**.</span><span class="sxs-lookup"><span data-stu-id="6a393-124">**PowerShell only**.</span></span> <span data-ttu-id="6a393-125">PowerShell을 사용하여 다중 VIP만 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-125">You can only manage Multi VIP by using PowerShell.</span></span>

<span data-ttu-id="6a393-126">이러한 제한은 일시적이며 언제든지 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-126">These limitations are temporary, and may change at any time.</span></span> <span data-ttu-id="6a393-127">이 페이지 tooverify 변경될지 toorevisit 있는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-127">Make sure toorevisit this page tooverify future changes.</span></span>

## <a name="how-tooadd-a-vip-tooa-cloud-service"></a><span data-ttu-id="6a393-128">어떻게 tooadd VIP tooa 클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="6a393-128">How tooadd a VIP tooa cloud service</span></span>
<span data-ttu-id="6a393-129">다음 PowerShell 명령을 hello 실행 tooadd VIP tooyour 서비스:</span><span class="sxs-lookup"><span data-stu-id="6a393-129">tooadd a VIP tooyour service, run hello following PowerShell command:</span></span>

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

<span data-ttu-id="6a393-130">이 명령은 다음 예제 결과 유사한 toohello를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-130">This command displays a result similar toohello following sample:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-tooremove-a-vip-from-a-cloud-service"></a><span data-ttu-id="6a393-131">어떻게 tooremove VIP 클라우드 서비스에서</span><span class="sxs-lookup"><span data-stu-id="6a393-131">How tooremove a VIP from a cloud service</span></span>
<span data-ttu-id="6a393-132">다음 PowerShell 명령이 실행된 hello 위의 hello 예제 tooyour 서비스를 추가 하는 VIP tooremove hello:</span><span class="sxs-lookup"><span data-stu-id="6a393-132">tooremove hello VIP added tooyour service in hello example above, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> <span data-ttu-id="6a393-133">연결 끝점 tooit 없는 경우에 VIP를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-133">You can only remove a VIP if it has no endpoints associated tooit.</span></span>


## <a name="how-tooretrieve-vip-information-from-a-cloud-service"></a><span data-ttu-id="6a393-134">어떻게 클라우드 서비스에서 VIP tooretrieve 정보</span><span class="sxs-lookup"><span data-stu-id="6a393-134">How tooretrieve VIP information from a Cloud Service</span></span>
<span data-ttu-id="6a393-135">hello 다음 PowerShell 스크립트를 실행 하는 클라우드 서비스와 연결 된 Vip tooretrieve hello:</span><span class="sxs-lookup"><span data-stu-id="6a393-135">tooretrieve hello VIPs associated with a cloud service, run hello following PowerShell script:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="6a393-136">hello 스크립트 샘플 다음 결과 유사한 toohello를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-136">hello script displays a result similar toohello following sample:</span></span>

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

<span data-ttu-id="6a393-137">이 예제에서는 hello 클라우드 서비스에 3 Vip:</span><span class="sxs-lookup"><span data-stu-id="6a393-137">In this example, hello cloud service has 3 VIPs:</span></span>

* <span data-ttu-id="6a393-138">**Vip1** 기본 VIP는 hello, 것을 알고 있다면 IsDnsProgrammedName에 대 한 hello 값 tootrue 설정 되어 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-138">**Vip1** is hello default VIP, you know that because hello value for IsDnsProgrammedName is set tootrue.</span></span>
* <span data-ttu-id="6a393-139">**Vip2** 및 **Vip3**은 IP 주소가 없으므로 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-139">**Vip2** and **Vip3** are not used as they do not have any IP addresses.</span></span> <span data-ttu-id="6a393-140">이러한 작업은 끝점 toohello VIP를 연결 하는 경우에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-140">They will only be used if you associate an endpoint toohello VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="6a393-141">끝점과 연결된 후에는 추가 VIP에 대한 요금이 구독에 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-141">Your subscription will only be charged for extra VIPs once they are associated with an endpoint.</span></span> <span data-ttu-id="6a393-142">가격에 대한 자세한 내용은 [IP 주소 가격](https://azure.microsoft.com/pricing/details/ip-addresses/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a393-142">For more information on pricing, see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/).</span></span>

## <a name="how-tooassociate-a-vip-tooan-endpoint"></a><span data-ttu-id="6a393-143">어떻게 tooassociate VIP tooan 끝점</span><span class="sxs-lookup"><span data-stu-id="6a393-143">How tooassociate a VIP tooan endpoint</span></span>

<span data-ttu-id="6a393-144">tooassociate VIP hello 다음 PowerShell 명령을 실행 한 클라우드 서비스 tooan 끝점:</span><span class="sxs-lookup"><span data-stu-id="6a393-144">tooassociate a VIP on a cloud service tooan endpoint, run hello following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

<span data-ttu-id="6a393-145">hello 명령은 라는 toohello 연결 된 VIP 끝점 *Vip2* 포트에서 *80*, toohello 라는 VM 연결 *myVM1* 클라우드 서비스에서 명명 된  *myService* 를 사용 하 여 *TCP* 포트에서 *8080*합니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-145">hello command creates an endpoint linked toohello VIP called *Vip2* on port *80*, and links it toohello VM named *myVM1* in a cloud service named *myService* using *TCP* on port *8080*.</span></span>

<span data-ttu-id="6a393-146">다음 PowerShell 명령을 hello 실행 tooverify hello 구성:</span><span class="sxs-lookup"><span data-stu-id="6a393-146">tooverify hello configuration, run hello following PowerShell command:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="6a393-147">hello 출력은 다음 예제와 비슷한 toohello 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-147">hello output looks similar toohello following example:</span></span>

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         : 191.238.74.13
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

## <a name="how-tooenable-load-balancing-on-a-specific-vip"></a><span data-ttu-id="6a393-148">특정 vip 분산 tooenable을 로드 하는 방법</span><span class="sxs-lookup"><span data-stu-id="6a393-148">How tooenable load balancing on a specific VIP</span></span>

<span data-ttu-id="6a393-149">부하 분산을 위해 단일 VIP를 여러 가상 컴퓨터에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-149">You can associate a single VIP with multiple virtual machines for load balancing purposes.</span></span> <span data-ttu-id="6a393-150">예를 들어 *myService*라는 클라우드 서비스와 *myVM1* 및 *myVM2*라는 두 개의 가상 컴퓨터가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-150">For example, you have a cloud service named *myService*, and two virtual machines named *myVM1* and *myVM2*.</span></span> <span data-ttu-id="6a393-151">클라우드 서비스에는 여러 VIP가 있고, 그중의 하나가 *Vip2*입니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-151">And your cloud service has multiple VIPs, one of them named *Vip2*.</span></span> <span data-ttu-id="6a393-152">모든 트래픽이 tooport tooensure 하려는 경우 *81* 에 *Vip2* 간에 분산 *myVM1* 및 *myVM2* 포트에서 *8181* 실행 hello 다음 PowerShell 스크립트:</span><span class="sxs-lookup"><span data-stu-id="6a393-152">If you want tooensure that all traffic tooport *81* on *Vip2* is balanced between *myVM1* and *myVM2* on port *8181*, run hello following PowerShell script:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

<span data-ttu-id="6a393-153">부하 분산 장치 toouse 다른 VIP를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-153">You can also update your load balancer toouse a different VIP.</span></span> <span data-ttu-id="6a393-154">예를 들어 hello 아래 PowerShell 명령을 실행 하는 경우 hello 부하 분산 집합 toouse Vip1 라는 VIP를 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a393-154">For example, if you run hello PowerShell command below, you will change hello load balancing set toouse a VIP named Vip1:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a><span data-ttu-id="6a393-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6a393-155">Next Steps</span></span>

[<span data-ttu-id="6a393-156">Azure 부하 분산에 대한 Log Analytics</span><span class="sxs-lookup"><span data-stu-id="6a393-156">Log analytics for Azure Load Balance</span></span>](load-balancer-monitor-log.md)

[<span data-ttu-id="6a393-157">인터넷 연결 부하 분산 장치 개요</span><span class="sxs-lookup"><span data-stu-id="6a393-157">Internet facing load balancer overview</span></span>](load-balancer-internet-overview.md)

[<span data-ttu-id="6a393-158">인터넷 연결 부하 분산 장치 시작</span><span class="sxs-lookup"><span data-stu-id="6a393-158">Get started on Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="6a393-159">가상 네트워크 개요</span><span class="sxs-lookup"><span data-stu-id="6a393-159">Virtual Network Overview</span></span>](../virtual-network/virtual-networks-overview.md)

[<span data-ttu-id="6a393-160">예약된 IP REST API</span><span class="sxs-lookup"><span data-stu-id="6a393-160">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)
