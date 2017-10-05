---
title: "클라우드 서비스당 여러 VIP"
description: "MultiVIP 및 클라우드 서비스에서 여러 VIP를 설정하는 방법에 대한 개요입니다."
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
ms.openlocfilehash: f40e0501eed8d5f296e7c79d8a35705a695ae6fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a><span data-ttu-id="ce598-103">클라우드 서비스당 여러 VIP 구성</span><span class="sxs-lookup"><span data-stu-id="ce598-103">Configure multiple VIPs for a cloud service</span></span>

<span data-ttu-id="ce598-104">Azure에서 제공하는 IP 주소를 사용하여 공용 인터넷을 통해 Azure 클라우드 서비스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-104">You can access Azure cloud services over the public Internet by using an IP address provided by Azure.</span></span> <span data-ttu-id="ce598-105">이 공용 IP 주소는 Azure Load Balancer에 연결되며 클라우드 서비스 내의 VM(가상 컴퓨터) 인스턴스가 아니기 때문에 VIP(가상 IP)라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-105">This public IP address is referred to as a VIP (virtual IP) since it is linked to the Azure load balancer, and not the Virtual Machine (VM) instances within the cloud service.</span></span> <span data-ttu-id="ce598-106">단일 VIP를 사용하여 클라우드 서비스 내의 모든 VM 인스턴스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-106">You can access any VM instance within a cloud service by using a single VIP.</span></span>

<span data-ttu-id="ce598-107">그러나 동일한 클라우드 서비스에 대한 진입점으로 둘 이상의 VIP가 필요할 수 있는 시나리오도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-107">However, there are scenarios in which you may need more than one VIP as an entry point to the same cloud service.</span></span> <span data-ttu-id="ce598-108">예를 들어 각 사이트가 서로 다른 고객 또는 테넌트에 대해 호스트되므로 클라우드 서비스에서 기본 포트 443을 사용하여 SSL에 연결해야 하는 여러 웹 사이트를 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-108">For instance, your cloud service may host multiple websites that require SSL connectivity using the default port of 443, as each site is hosted for a different customer, or tenant.</span></span> <span data-ttu-id="ce598-109">이 시나리오에서는 각 웹 사이트에 대해 다른 공용 연결 IP 주소를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-109">In this scenario, you need to have a different public facing IP address for each website.</span></span> <span data-ttu-id="ce598-110">아래 다이어그램은 동일한 공용 포트에 여러 SSL 인증서가 필요한 일반적인 다중 테넌트 웹 호스팅을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-110">The diagram below illustrates a typical multi-tenant web hosting with a need for multiple SSL certificates on the same public port.</span></span>

![다중 VIP SSL 시나리오](./media/load-balancer-multivip/Figure1.png)

<span data-ttu-id="ce598-112">위 예제에서 모든 VIP는 동일한 공용 포트(443)를 사용하며, 모든 웹 사이트를 호스트하는 클라우드 서비스의 내부 IP 주소에 대한 고유한 개인 포트에서 하나 이상의 부하 분산 VM으로 트래픽이 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-112">In the example above, all VIPs use the same public port (443) and traffic is redirected to one or more load balanced VMs on a unique private port for the internal IP address of the cloud service hosting all the websites.</span></span>

> [!NOTE]
> <span data-ttu-id="ce598-113">여러 VIP를 사용해야 하는 또 다른 상황은 동일한 가상 컴퓨터 집합에서 여러 개의 SQL AlwaysOn 가용성 그룹 수신기를 호스트하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-113">Another situation requiring the use the multiple VIPs is hosting multiple SQL AlwaysOn availability group listeners on the same set of Virtual Machines.</span></span>

<span data-ttu-id="ce598-114">VIP는 기본적으로 동적이므로 클라우드 서비스에 할당된 실제 IP 주소가 시간에 따라 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-114">VIPs are dynamic by default, which means that the actual IP address assigned to the cloud service may change over time.</span></span> <span data-ttu-id="ce598-115">이러한 문제가 발생하지 않도록 서비스에 대해 VIP를 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-115">To prevent that from happening, you can reserve a VIP for your service.</span></span> <span data-ttu-id="ce598-116">예약된 VIP에 대한 자세한 내용은 [예약된 공용 IP](../virtual-network/virtual-networks-reserved-public-ip.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ce598-116">To learn more about reserved VIPs, see [Reserved Public IP](../virtual-network/virtual-networks-reserved-public-ip.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ce598-117">VIP 및 예약된 IP의 가격에 대한 자세한 내용은 [IP 주소 가격](https://azure.microsoft.com/pricing/details/ip-addresses/) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ce598-117">Please see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/) for information on pricing on VIPs and reserved IPs.</span></span>

<span data-ttu-id="ce598-118">PowerShell을 통해 클라우드 서비스에서 사용하는 VIP를 확인하고, VIP를 추가 및 제거하고, VIP를 끝점에 연결하고, 특정 VIP에 부하 분산을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-118">You can use PowerShell to verify the VIPs used by your cloud services, as well as add and remove VIPs, associate a VIP to an endpoint, and configure load balancing on a specific VIP.</span></span>

## <a name="limitations"></a><span data-ttu-id="ce598-119">제한 사항</span><span class="sxs-lookup"><span data-stu-id="ce598-119">Limitations</span></span>

<span data-ttu-id="ce598-120">이때 다중 VIP 기능은 다음과 시나리오로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-120">At this time, Multi VIP functionality is limited to the following scenarios:</span></span>

* <span data-ttu-id="ce598-121">**IaaS만**.</span><span class="sxs-lookup"><span data-stu-id="ce598-121">**IaaS only**.</span></span> <span data-ttu-id="ce598-122">VM을 포함하는 클라우드 서비스에 대해서 다중 VIP만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-122">You can only enable Multi VIP for cloud services that contain VMs.</span></span> <span data-ttu-id="ce598-123">PaaS 시나리오에서 역할 인스턴스와 함께 다중 VIP를 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-123">You cannot use Multi VIP in PaaS scenarios with role instances.</span></span>
* <span data-ttu-id="ce598-124">**PowerShell만**.</span><span class="sxs-lookup"><span data-stu-id="ce598-124">**PowerShell only**.</span></span> <span data-ttu-id="ce598-125">PowerShell을 사용하여 다중 VIP만 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-125">You can only manage Multi VIP by using PowerShell.</span></span>

<span data-ttu-id="ce598-126">이러한 제한은 일시적이며 언제든지 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-126">These limitations are temporary, and may change at any time.</span></span> <span data-ttu-id="ce598-127">향후 변경 내용을 확인하려면 이 페이지를 다시 방문해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-127">Make sure to revisit this page to verify future changes.</span></span>

## <a name="how-to-add-a-vip-to-a-cloud-service"></a><span data-ttu-id="ce598-128">클라우드 서비스에 VIP를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="ce598-128">How to add a VIP to a cloud service</span></span>
<span data-ttu-id="ce598-129">서비스를 VIP를 추가하려면 다음 PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-129">To add a VIP to your service, run the following PowerShell command:</span></span>

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

<span data-ttu-id="ce598-130">이 명령은 다음 예제와 유사한 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-130">This command displays a result similar to the following sample:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-to-remove-a-vip-from-a-cloud-service"></a><span data-ttu-id="ce598-131">클라우드 서비스에서 VIP를 제거하는 방법</span><span class="sxs-lookup"><span data-stu-id="ce598-131">How to remove a VIP from a cloud service</span></span>
<span data-ttu-id="ce598-132">위 예제에서 서비스에 추가된 VIP를 제거하려면 다음 PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-132">To remove the VIP added to your service in the example above, run the following PowerShell command:</span></span>

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> <span data-ttu-id="ce598-133">연결된 끝점이 없는 경우에만 VIP를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-133">You can only remove a VIP if it has no endpoints associated to it.</span></span>


## <a name="how-to-retrieve-vip-information-from-a-cloud-service"></a><span data-ttu-id="ce598-134">클라우드 서비스에서 VIP 정보를 검색하는 방법</span><span class="sxs-lookup"><span data-stu-id="ce598-134">How to retrieve VIP information from a Cloud Service</span></span>
<span data-ttu-id="ce598-135">클라우드 서비스와 연결된 VIP를 검색하려면 다음 PowerShell 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-135">To retrieve the VIPs associated with a cloud service, run the following PowerShell script:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="ce598-136">이 스크립트는 다음 예제와 유사한 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-136">The script displays a result similar to the following sample:</span></span>

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

<span data-ttu-id="ce598-137">이 예제에서는 클라우드 서비스에 다음 3개의 VIP가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-137">In this example, the cloud service has 3 VIPs:</span></span>

* <span data-ttu-id="ce598-138">**Vip1** 은 기본 VIP로, IsDnsProgrammedName의 값이 true로 설정되었기 때문에 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-138">**Vip1** is the default VIP, you know that because the value for IsDnsProgrammedName is set to true.</span></span>
* <span data-ttu-id="ce598-139">**Vip2** 및 **Vip3**은 IP 주소가 없으므로 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-139">**Vip2** and **Vip3** are not used as they do not have any IP addresses.</span></span> <span data-ttu-id="ce598-140">끝점을 VIP에 연결하는 경우에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-140">They will only be used if you associate an endpoint to the VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="ce598-141">끝점과 연결된 후에는 추가 VIP에 대한 요금이 구독에 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-141">Your subscription will only be charged for extra VIPs once they are associated with an endpoint.</span></span> <span data-ttu-id="ce598-142">가격에 대한 자세한 내용은 [IP 주소 가격](https://azure.microsoft.com/pricing/details/ip-addresses/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ce598-142">For more information on pricing, see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/).</span></span>

## <a name="how-to-associate-a-vip-to-an-endpoint"></a><span data-ttu-id="ce598-143">VIP를 끝점에 연결하는 방법</span><span class="sxs-lookup"><span data-stu-id="ce598-143">How to associate a VIP to an endpoint</span></span>

<span data-ttu-id="ce598-144">클라우드 서비스의 VIP를 끝점에 연결하려면 다음 PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-144">To associate a VIP on a cloud service to an endpoint, run the following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

<span data-ttu-id="ce598-145">이 명령은 포트 *80*에서 *Vip2*라는 VIP에 연결된 끝점을 만들고, 포트 *8080*에서 *TCP*를 사용하여 *myService*라는 클라우드 서비스에 있는 *myVM1*이라는 VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-145">The command creates an endpoint linked to the VIP called *Vip2* on port *80*, and links it to the VM named *myVM1* in a cloud service named *myService* using *TCP* on port *8080*.</span></span>

<span data-ttu-id="ce598-146">구성을 확인하려면 다음 PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-146">To verify the configuration, run the following PowerShell command:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="ce598-147">출력은 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-147">The output looks similar to the following example:</span></span>

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

## <a name="how-to-enable-load-balancing-on-a-specific-vip"></a><span data-ttu-id="ce598-148">특정 VIP에서 부하 분산을 사용하도록 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="ce598-148">How to enable load balancing on a specific VIP</span></span>

<span data-ttu-id="ce598-149">부하 분산을 위해 단일 VIP를 여러 가상 컴퓨터에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-149">You can associate a single VIP with multiple virtual machines for load balancing purposes.</span></span> <span data-ttu-id="ce598-150">예를 들어 *myService*라는 클라우드 서비스와 *myVM1* 및 *myVM2*라는 두 개의 가상 컴퓨터가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-150">For example, you have a cloud service named *myService*, and two virtual machines named *myVM1* and *myVM2*.</span></span> <span data-ttu-id="ce598-151">클라우드 서비스에는 여러 VIP가 있고, 그중의 하나가 *Vip2*입니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-151">And your cloud service has multiple VIPs, one of them named *Vip2*.</span></span> <span data-ttu-id="ce598-152">*Vip2*의 포트 *81*로 전송된 모든 트래픽을 포트 *8181*에서 *myVM1* 및 *myVM2* 간에 부하 분산하려는 경우 다음 PowerShell 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-152">If you want to ensure that all traffic to port *81* on *Vip2* is balanced between *myVM1* and *myVM2* on port *8181*, run the following PowerShell script:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

<span data-ttu-id="ce598-153">다른 VIP를 사용하도록 부하 분산 장치를 업데이트할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-153">You can also update your load balancer to use a different VIP.</span></span> <span data-ttu-id="ce598-154">예를 들어 아래 PowerShell 명령을 실행하면 부하 분산 집합이 Vip1이라는 VIP를 사용하도록 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce598-154">For example, if you run the PowerShell command below, you will change the load balancing set to use a VIP named Vip1:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a><span data-ttu-id="ce598-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ce598-155">Next Steps</span></span>

[<span data-ttu-id="ce598-156">Azure 부하 분산에 대한 Log Analytics</span><span class="sxs-lookup"><span data-stu-id="ce598-156">Log analytics for Azure Load Balance</span></span>](load-balancer-monitor-log.md)

[<span data-ttu-id="ce598-157">인터넷 연결 부하 분산 장치 개요</span><span class="sxs-lookup"><span data-stu-id="ce598-157">Internet facing load balancer overview</span></span>](load-balancer-internet-overview.md)

[<span data-ttu-id="ce598-158">인터넷 연결 부하 분산 장치 시작</span><span class="sxs-lookup"><span data-stu-id="ce598-158">Get started on Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="ce598-159">가상 네트워크 개요</span><span class="sxs-lookup"><span data-stu-id="ce598-159">Virtual Network Overview</span></span>](../virtual-network/virtual-networks-overview.md)

[<span data-ttu-id="ce598-160">예약된 IP REST API</span><span class="sxs-lookup"><span data-stu-id="ce598-160">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)
