---
title: "Azure 예약 IP 주소(클래식) 관리 - PowerShell | Microsoft Docs"
description: "예약된 IP 주소(클래식)과 PowerShell을 사용하여 관리하는 방법을 이해합니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 34652a55-3ab8-4c2d-8fb2-43684033b191
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: 5e9c83cebec96c6bc8afd53b0c637d7af899746f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="reserved-ip-addresses-classic"></a><span data-ttu-id="f6a9c-103">예약된 IP 주소(클래식)</span><span class="sxs-lookup"><span data-stu-id="f6a9c-103">Reserved IP addresses (Classic)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f6a9c-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="f6a9c-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="f6a9c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6a9c-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="f6a9c-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f6a9c-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="f6a9c-107">템플릿</span><span class="sxs-lookup"><span data-stu-id="f6a9c-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="f6a9c-108">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="f6a9c-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

<span data-ttu-id="f6a9c-109">Azure의 IP 주소는 두 범주 즉, 동적 IP 및 예약된 IP로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-109">IP addresses in Azure fall into two categories: dynamic and reserved.</span></span> <span data-ttu-id="f6a9c-110">Azure에서 관리하는 공용 IP 주소는 기본적으로 동적입니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-110">Public IP addresses managed by Azure are dynamic by default.</span></span> <span data-ttu-id="f6a9c-111">즉, 지정된 클라우드 서비스에 사용되는 IP 주소(VIP) 또는 VM이나 역할 인스턴스에 직접 액세스하는 데 사용되는 IP 주소(ILPIP)는 리소스가 종료 또는 중지(할당 취소)된 경우 때때로 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-111">That means that the IP address used for a given cloud service (VIP) or to access a VM or role instance directly (ILPIP) can change from time to time, when resources are shut down or stopped (deallocated).</span></span>

<span data-ttu-id="f6a9c-112">IP 주소의 변경을 방지하기 위해 IP 주소를 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-112">To prevent IP addresses from changing, you can reserve an IP address.</span></span> <span data-ttu-id="f6a9c-113">예약된 IP는 VIP로만 사용할 수 있으므로 리소스가 종료 또는 중지(할당 취소)된 때에도 클라우드 서비스의 IP 주소가 동일하게 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-113">Reserved IPs can be used only as a VIP, ensuring that the IP address for the cloud service remains the same, even as resources are shut down or stopped (deallocated).</span></span> <span data-ttu-id="f6a9c-114">또한 VIP로 사용하는 기존의 동적 IP를 예약된 IP 주소로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-114">Furthermore, you can convert existing dynamic IPs used as a VIP to a reserved IP address.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f6a9c-115">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-115">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f6a9c-116">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-116">This article covers using the classic deployment model.</span></span> <span data-ttu-id="f6a9c-117">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-117">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="f6a9c-118">[Resource Manager 배포 모델](virtual-network-ip-addresses-overview-arm.md)을 사용하여 고정 공용 IP 주소를 예약하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-118">Learn how to reserve a static public IP address using the [Resource Manager deployment model](virtual-network-ip-addresses-overview-arm.md).</span></span>

<span data-ttu-id="f6a9c-119">Azure의 IP 주소에 대한 자세한 내용을 알아보려면 [IP 주소](virtual-network-ip-addresses-overview-classic.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-119">To learn more about IP addresses in Azure, read the [IP addresses](virtual-network-ip-addresses-overview-classic.md) article.</span></span>

## <a name="when-do-i-need-a-reserved-ip"></a><span data-ttu-id="f6a9c-120">예약된 IP는 언제 필요한가요?</span><span class="sxs-lookup"><span data-stu-id="f6a9c-120">When do I need a reserved IP?</span></span>
* <span data-ttu-id="f6a9c-121">**IP가 구독에서 예약되어 있는지 확인하려고 합니다**.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-121">**You want to ensure that the IP is reserved in your subscription**.</span></span> <span data-ttu-id="f6a9c-122">어떤 상황에서도 구독에서 해제되지 않을 IP 주소를 예약하려는 경우 예약된 공용 IP를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-122">If you want to reserve an IP address that is not released from your subscription under any circumstance, you should use a reserved public IP.</span></span>  
* <span data-ttu-id="f6a9c-123">**중지 상태 또는 할당 취소 상태(VM)에서도 IP를 클라우드 서비스에서 유지하려고 합니다**.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-123">**You want your IP to stay with your cloud service even across stopped or deallocated state (VMs)**.</span></span> <span data-ttu-id="f6a9c-124">클라우드 서비스의 VM이 종료 또는 중지(할당 취소)된 경우에도 변경되지 않는 IP 주소를 사용하여 서비스에 액세스할 수 있도록 설정하기를 원합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-124">If you want your service to be accessed by using an IP address that doesn't change, even when VMs in the cloud service are shut down or stop (deallocated).</span></span>
* <span data-ttu-id="f6a9c-125">**Azure의 아웃바운드 트래픽이 예측 가능한 IP 주소를 사용하는지 확인하려고 합니다**.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-125">**You want to ensure that outbound traffic from Azure uses a predictable IP address**.</span></span> <span data-ttu-id="f6a9c-126">특정 IP 주소의 트래픽만 허용하도록 온-프레미스 방화벽을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-126">You may have your on-premises firewall configured to allow only traffic from specific IP addresses.</span></span> <span data-ttu-id="f6a9c-127">IP를 예약하면 원본 IP 주소를 알고 있으므로 IP 변경 때문에 방화벽 규칙을 업데이트할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-127">By reserving an IP, you know the source IP address, and don't need to update your firewall rules due to an IP change.</span></span>

## <a name="faq"></a><span data-ttu-id="f6a9c-128">FAQ</span><span class="sxs-lookup"><span data-stu-id="f6a9c-128">FAQ</span></span>
1. <span data-ttu-id="f6a9c-129">모든 Azure 서비스에 예약된 IP를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="f6a9c-129">Can I use a reserved IP for all Azure services?</span></span> <br>
    <span data-ttu-id="f6a9c-130">아니요.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-130">No.</span></span> <span data-ttu-id="f6a9c-131">예약된 IP는 VM 및 VIP를 통해 노출되는 클라우드 서비스 인스턴스 역할에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-131">Reserved IPs can only be used for VMs and cloud service instance roles exposed through a VIP.</span></span>
2. <span data-ttu-id="f6a9c-132">예약된 IP를 몇 개까지 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="f6a9c-132">How many reserved IPs can I have?</span></span> <br>
    <span data-ttu-id="f6a9c-133">자세한 내용은 참조는 [Azure 제한](../azure-subscription-service-limits.md#networking-limits) 문서.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-133">For details, see the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
3. <span data-ttu-id="f6a9c-134">예약된 IP는 사용 요금이 있나요?</span><span class="sxs-lookup"><span data-stu-id="f6a9c-134">Is there a charge for reserved IPs?</span></span> <br>
    <span data-ttu-id="f6a9c-135">때때로 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-135">Sometimes.</span></span> <span data-ttu-id="f6a9c-136">가격 책정 정보는 [예약된 IP 주소 가격 책정 정보](http://go.microsoft.com/fwlink/?LinkID=398482)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-136">For pricing details, see the [Reserved IP Address Pricing Details](http://go.microsoft.com/fwlink/?LinkID=398482) page.</span></span>
4. <span data-ttu-id="f6a9c-137">IP 주소를 어떻게 예약하나요?</span><span class="sxs-lookup"><span data-stu-id="f6a9c-137">How do I reserve an IP address?</span></span> <br>
    <span data-ttu-id="f6a9c-138">PowerShell을 사용할 수 있습니다는 [Azure 관리 REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx), 또는 [Azure 포털](https://portal.azure.com) Azure 지역에서 IP 주소를 예약 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-138">You can use PowerShell, the [Azure Management REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx), or the [Azure portal](https://portal.azure.com) to reserve an IP address in an Azure region.</span></span> <span data-ttu-id="f6a9c-139">예약된 IP 주소는 구독에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-139">A reserved IP address is associated to your subscription.</span></span>
5. <span data-ttu-id="f6a9c-140">선호도 그룹 기반 VNet에서 예약된 IP를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="f6a9c-140">Can I use a reserved IP with affinity group-based VNets?</span></span> <br>
    <span data-ttu-id="f6a9c-141">아니요.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-141">No.</span></span> <span data-ttu-id="f6a9c-142">예약된 IP는 지역 VNet에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-142">Reserved IPs are only supported in regional VNets.</span></span> <span data-ttu-id="f6a9c-143">예약된 IP는 선호도 그룹과 연결된 VNet에 대해 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-143">Reserved IPs are not supported for VNets that are associated with affinity groups.</span></span> <span data-ttu-id="f6a9c-144">VNet을 지역 또는 선호도 그룹과 연결하는 방법에 대한 자세한 내용은 [지역 VNet 및 선호도 그룹 정보](virtual-networks-migrate-to-regional-vnet.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-144">For more information about associating a VNet with a region or affinity group, see the [About Regional VNets and Affinity Groups](virtual-networks-migrate-to-regional-vnet.md) article.</span></span>

## <a name="manage-reserved-vips"></a><span data-ttu-id="f6a9c-145">예약된 VIP 관리</span><span class="sxs-lookup"><span data-stu-id="f6a9c-145">Manage reserved VIPs</span></span>

<span data-ttu-id="f6a9c-146">[PowerShell 설치 및 구성](/powershell/azure/overview) 문서에 나오는 단계를 완료하여 PowerShell을 설치 및 구성했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-146">Ensure you have installed and configured PowerShell by completing the steps in the [Install and configure PowerShell](/powershell/azure/overview) article.</span></span> 

<span data-ttu-id="f6a9c-147">예약된 IP를 사용하려면 먼저 구독에 예약된 IP를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-147">Before you can use reserved IPs, you must add it to your subscription.</span></span> <span data-ttu-id="f6a9c-148">*미국 중부* 위치에서 사용할 수 있는 공용 IP 주소 풀에서 예약된 IP를 만들려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-148">To create a reserved IP from the pool of public IP addresses available in the *Central US* location, run the following command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"
```

<span data-ttu-id="f6a9c-149">그러나 예약할 IP를 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-149">Notice, however, that you cannot specify what IP is being reserved.</span></span> <span data-ttu-id="f6a9c-150">구독에서 예약된 IP 주소를 보려면 다음 PowerShell 명령을 실행하고 *ReservedIPName* 및 *Address*의 값을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-150">To view what IP addresses are reserved in your subscription, run the following PowerShell command, and notice the values for *ReservedIPName* and *Address*:</span></span>

```powershell
Get-AzureReservedIP
```

<span data-ttu-id="f6a9c-151">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="f6a9c-151">Expected output:</span></span>

    ReservedIPName       : MyReservedIP
    Address              : 23.101.114.211
    Id                   : d73be9dd-db12-4b5e-98c8-bc62e7c42041
    Label                :
    Location             : Central US
    State                : Created
    InUse                : False
    ServiceName          :
    DeploymentName       :
    OperationDescription : Get-AzureReservedIP
    OperationId          : 55e4f245-82e4-9c66-9bd8-273e815ce30a
    OperationStatus      : Succeeded

>[!NOTE]
><span data-ttu-id="f6a9c-152">PowerShell을 사용하여 예약된 IP 주소를 만들 때 예약된 IP를 만들 리소스 그룹을 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-152">When you create a reserved IP address with PowerShell, you cannot specify a resource group to create the reserved IP in.</span></span> <span data-ttu-id="f6a9c-153">Azure에서 *Default-Networking*이라는 리소스 그룹에 자동으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-153">Azure places it into a resource group named *Default-Networking* automatically.</span></span> <span data-ttu-id="f6a9c-154">[Azure Portal](http://portal.azure.com)을 사용하여 예약된 IP를 만드는 경우 원하는 어떤 리소스 그룹도 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-154">If you create the reserved IP using the [Azure portal](http://portal.azure.com), you can specify any resource group you choose.</span></span> <span data-ttu-id="f6a9c-155">그러나 *Default-Networking* 이외의 리소스 그룹에서 예약된 IP를 만드는 경우 `Get-AzureReservedIP` 및 `Remove-AzureReservedIP`와 같은 명령으로 예약된 IP를 참조할 때마다 이름 *Group resource-group-name reserved-ip-name*을 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-155">If you create the reserved IP in a resource group other than *Default-Networking* however, whenever you reference the reserved IP with commands such as `Get-AzureReservedIP` and `Remove-AzureReservedIP`, you must reference the name *Group resource-group-name reserved-ip-name*.</span></span>  <span data-ttu-id="f6a9c-156">예를 들어 *myResourceGroup* 리소스 그룹에 *myReservedIP*라는 예약된 IP를 만드는 경우 예약된 IP의 이름을 *Group myResourceGroup myReservedIP*로 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-156">For example, if you create a reserved IP named *myReservedIP* in a resource group named *myResourceGroup*, you must reference the name of the reserved IP as *Group myResourceGroup myReservedIP*.</span></span>   

<span data-ttu-id="f6a9c-157">IP를 예약하면 예약된 IP는 삭제될 때까지 계속 구독에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-157">Once an IP is reserved, it remains associated to your subscription until you delete it.</span></span> <span data-ttu-id="f6a9c-158">예약된 IP를 삭제하려면 다음 PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-158">To delete a reserved IP, run the following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIP -ReservedIPName "MyReservedIP"
```

## <a name="reserve-the-ip-address-of-an-existing-cloud-service"></a><span data-ttu-id="f6a9c-159">기존 클라우드 서비스의 IP 주소 예약</span><span class="sxs-lookup"><span data-stu-id="f6a9c-159">Reserve the IP address of an existing cloud service</span></span>
<span data-ttu-id="f6a9c-160">`-ServiceName` 매개 변수를 추가하여 기존 클라우드 서비스의 IP 주소를 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-160">You can reserve the IP address of an existing cloud service by adding the `-ServiceName` parameter.</span></span> <span data-ttu-id="f6a9c-161">*미국 중부* 위치에서 클라우드 서비스 *TestService*의 IP 주소를 예약하려면 다음 PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-161">To reserve the IP address of a cloud service *TestService* in the *Central US* location, run the following PowerShell command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US" -ServiceName TestService
```

## <a name="associate-a-reserved-ip-to-a-new-cloud-service"></a><span data-ttu-id="f6a9c-162">예약된 IP를 새 클라우드 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="f6a9c-162">Associate a reserved IP to a new cloud service</span></span>
<span data-ttu-id="f6a9c-163">다음 스크립트는 예약된 새 IP를 만든 후 *TestService*라는 이름의 새 클라우드 서비스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-163">The following script creates a new reserved IP, then associates it to a new cloud service named *TestService*.</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService -ReservedIPName MyReservedIP -Location "Central US"
```

> [!NOTE]
> <span data-ttu-id="f6a9c-164">클라우드 서비스에서 사용할 예약된 IP를 만들 때 여전히 인바운드 통신에 *VIP:&lt;포트 번호>*를 사용하여 VM을 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-164">When you create a reserved IP to use with a cloud service, you still refer to the VM by using *VIP:&lt;port number>* for inbound communication.</span></span> <span data-ttu-id="f6a9c-165">IP를 예약했다고 VM에 직접 연결할 수 있다는 의미는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-165">Reserving an IP does not mean you can connect to the VM directly.</span></span> <span data-ttu-id="f6a9c-166">예약된 IP는 VM이 배포된 클라우드 서비스에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-166">The reserved IP is assigned to the cloud service that the VM has been deployed to.</span></span> <span data-ttu-id="f6a9c-167">IP 통해 VM에 직접 연결하려는 경우 인스턴스 수준 공용 IP를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-167">If you want to connect to a VM by IP directly, you have to configure an instance-level public IP.</span></span> <span data-ttu-id="f6a9c-168">인스턴스 수준 공용 IP(ILPIP라고 함)는 VM에 직접 할당된 공용 IP의 한 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-168">An instance-level public IP is a type of public IP (called an ILPIP) that is assigned directly to your VM.</span></span> <span data-ttu-id="f6a9c-169">ILPIP는 예약할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-169">It cannot be reserved.</span></span> <span data-ttu-id="f6a9c-170">자세한 내용은 [인스턴스 수준 공용 IP(ILPIP)](virtual-networks-instance-level-public-ip.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-170">For more information, read the [Instance-level Public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) article.</span></span>
> 

## <a name="remove-a-reserved-ip-from-a-running-deployment"></a><span data-ttu-id="f6a9c-171">실행 중인 배포에서 예약된 IP 제거</span><span class="sxs-lookup"><span data-stu-id="f6a9c-171">Remove a reserved IP from a running deployment</span></span>
<span data-ttu-id="f6a9c-172">새 클라우드 서비스에 추가된 예약된 IP를 제거하려면 다음 PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-172">To remove a reserved IP added to a new cloud service, run the following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService
```

> [!NOTE]
> <span data-ttu-id="f6a9c-173">실행 중인 배포에서 예약된 IP를 제거해도 구독에서 예약이 제거되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-173">Removing a reserved IP from a running deployment does not remove the reservation from your subscription.</span></span> <span data-ttu-id="f6a9c-174">단지 구독의 다른 리소스에서 사용할 수 있도록 IP가 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-174">It simply frees the IP to be used by another resource in your subscription.</span></span>
> 

## <a name="associate-a-reserved-ip-to-a-running-deployment"></a><span data-ttu-id="f6a9c-175">실행 중인 배포에 예약된 IP 연결</span><span class="sxs-lookup"><span data-stu-id="f6a9c-175">Associate a reserved IP to a running deployment</span></span>
<span data-ttu-id="f6a9c-176">다음 명령은 *TestVM2*라는 새 VM을 사용하여 *TestService2*라는 클라우드 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-176">The following commands create a cloud service named *TestService2* with a new VM named *TestVM2*.</span></span> <span data-ttu-id="f6a9c-177">그러면 기존의 예약된 IP *MyReservedIP*가 클라우드 서비스에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-177">The existing reserved IP named *MyReservedIP* is then associated to the cloud service.</span></span>

```powershell
$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM2 -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService2 -Location "Central US"

Set-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService2
```

## <a name="associate-a-reserved-ip-to-a-cloud-service-by-using-a-service-configuration-file"></a><span data-ttu-id="f6a9c-178">서비스 구성 파일을 사용하여 클라우드 서비스에 예약된 IP 연결</span><span class="sxs-lookup"><span data-stu-id="f6a9c-178">Associate a reserved IP to a cloud service by using a service configuration file</span></span>
<span data-ttu-id="f6a9c-179">서비스 구성(CSCFG) 파일을 사용하여 클라우드 서비스에 예약된 IP를 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-179">You can also associate a reserved IP to a cloud service by using a service configuration (CSCFG) file.</span></span> <span data-ttu-id="f6a9c-180">다음 샘플 xml에서는 *MyReservedIP*라는 예약된 VIP를 사용하도록 클라우드 서비스를 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-180">The following sample xml shows how to configure a cloud service to use a reserved VIP named *MyReservedIP*:</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ReservedIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
        <ConfigurationSettings>
          <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
        </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <ReservedIPs>
           <ReservedIP name="MyReservedIP"/>
          </ReservedIPs>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>

## <a name="next-steps"></a><span data-ttu-id="f6a9c-181">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f6a9c-181">Next steps</span></span>
* <span data-ttu-id="f6a9c-182">클래식 배포 모델에서 [IP 주소 지정](virtual-network-ip-addresses-overview-classic.md) 이 어떻게 작동하는지 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-182">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in the classic deployment model.</span></span>
* <span data-ttu-id="f6a9c-183">[예약된 개인 IP 주소](virtual-networks-reserved-private-ip.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-183">Learn about [reserved private IP addresses](virtual-networks-reserved-private-ip.md).</span></span>
* <span data-ttu-id="f6a9c-184">[ILPIP(인스턴스 수준 공용 IP) 주소](virtual-networks-instance-level-public-ip.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f6a9c-184">Learn about [Instance Level Public IP (ILPIP) addresses](virtual-networks-instance-level-public-ip.md).</span></span>

