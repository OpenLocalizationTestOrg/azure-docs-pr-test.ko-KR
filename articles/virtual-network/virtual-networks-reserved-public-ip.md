---
title: "예약 된 IP 주소 (클래식)-PowerShell aaaManage Azure | Microsoft Docs"
description: "예약 된 IP 주소 (클래식) 이해 및 방법을 toomanage PowerShell을 사용 하 게 합니다."
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
ms.openlocfilehash: c0a77b2ab8b1ab9bef6015c903eb735ea4358a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reserved-ip-addresses-classic"></a><span data-ttu-id="8c5cb-103">예약된 IP 주소(클래식)</span><span class="sxs-lookup"><span data-stu-id="8c5cb-103">Reserved IP addresses (Classic)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8c5cb-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="8c5cb-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="8c5cb-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c5cb-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="8c5cb-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8c5cb-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="8c5cb-107">템플릿</span><span class="sxs-lookup"><span data-stu-id="8c5cb-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="8c5cb-108">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="8c5cb-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

<span data-ttu-id="8c5cb-109">Azure의 IP 주소는 두 범주 즉, 동적 IP 및 예약된 IP로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-109">IP addresses in Azure fall into two categories: dynamic and reserved.</span></span> <span data-ttu-id="8c5cb-110">Azure에서 관리하는 공용 IP 주소는 기본적으로 동적입니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-110">Public IP addresses managed by Azure are dynamic by default.</span></span> <span data-ttu-id="8c5cb-111">해당 IP 주소 (VIP) 지정 된 클라우드 서비스에 사용 되는 hello 있다는 것을 의미 하거나 tooaccess 리소스 종료 되거나 중지 (할당 취소) 되 면 VM 또는 역할 인스턴스를 직접 (ILPIP) 시간 tootime에서 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-111">That means that hello IP address used for a given cloud service (VIP) or tooaccess a VM or role instance directly (ILPIP) can change from time tootime, when resources are shut down or stopped (deallocated).</span></span>

<span data-ttu-id="8c5cb-112">가 변경할 tooprevent IP 주소, IP 주소를 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-112">tooprevent IP addresses from changing, you can reserve an IP address.</span></span> <span data-ttu-id="8c5cb-113">예약 된 Ip 남아 리소스가 종료 되는 때에 동일 hello 또는 중지 (할당 취소) hello 클라우드 서비스에 대 한 hello IP 주소가 있는지 확인 한 VIP로만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-113">Reserved IPs can be used only as a VIP, ensuring that hello IP address for hello cloud service remains hello same, even as resources are shut down or stopped (deallocated).</span></span> <span data-ttu-id="8c5cb-114">또한 VIP tooa 예약 된 IP 주소로 사용 되는 기존 동적 Ip를 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-114">Furthermore, you can convert existing dynamic IPs used as a VIP tooa reserved IP address.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8c5cb-115">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-115">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8c5cb-116">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-116">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="8c5cb-117">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-117">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="8c5cb-118">고정 공용 IP 주소를 사용 하 여 tooreserve hello 하는 방법에 대해 알아봅니다 [리소스 관리자 배포 모델](virtual-network-ip-addresses-overview-arm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-118">Learn how tooreserve a static public IP address using hello [Resource Manager deployment model](virtual-network-ip-addresses-overview-arm.md).</span></span>

<span data-ttu-id="8c5cb-119">Azure에서 toolearn IP에 대 한 주소, hello 읽기 [IP 주소](virtual-network-ip-addresses-overview-classic.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-119">toolearn more about IP addresses in Azure, read hello [IP addresses](virtual-network-ip-addresses-overview-classic.md) article.</span></span>

## <a name="when-do-i-need-a-reserved-ip"></a><span data-ttu-id="8c5cb-120">예약된 IP는 언제 필요한가요?</span><span class="sxs-lookup"><span data-stu-id="8c5cb-120">When do I need a reserved IP?</span></span>
* <span data-ttu-id="8c5cb-121">**IP hello tooensure 구독에서 예약 되는 것이 원하는**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-121">**You want tooensure that hello IP is reserved in your subscription**.</span></span> <span data-ttu-id="8c5cb-122">어떤 상황에서 구독에서 해제 되 고 있는 IP 주소가 tooreserve 하려는 경우 예약된 된 공용 IP를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-122">If you want tooreserve an IP address that is not released from your subscription under any circumstance, you should use a reserved public IP.</span></span>  
* <span data-ttu-id="8c5cb-123">**클라우드 서비스와 IP toostay에 걸쳐 중지 또는 상태 (Vm)를 할당 취소 하려는**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-123">**You want your IP toostay with your cloud service even across stopped or deallocated state (VMs)**.</span></span> <span data-ttu-id="8c5cb-124">변경 되지 않는 IP 주소를 사용 하 여 액세스 하 여 서비스 toobe 원한다 면 hello의 Vm 클라우드 하는 경우에 서비스를 종료 또는 중지 (할당 해제) 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-124">If you want your service toobe accessed by using an IP address that doesn't change, even when VMs in hello cloud service are shut down or stop (deallocated).</span></span>
* <span data-ttu-id="8c5cb-125">**Azure의 아웃 바운드 트래픽이 예측 가능한 IP 주소를 사용 하는 tooensure 원하는**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-125">**You want tooensure that outbound traffic from Azure uses a predictable IP address**.</span></span> <span data-ttu-id="8c5cb-126">특정 IP 주소에서 온-프레미스 방화벽 구성 tooallow만 트래픽이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-126">You may have your on-premises firewall configured tooallow only traffic from specific IP addresses.</span></span> <span data-ttu-id="8c5cb-127">IP를 예약 하 여 알고 hello 원본 IP 주소, 및 tooupdate tooan IP 변경 인해 방화벽 규칙에 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-127">By reserving an IP, you know hello source IP address, and don't need tooupdate your firewall rules due tooan IP change.</span></span>

## <a name="faq"></a><span data-ttu-id="8c5cb-128">FAQ</span><span class="sxs-lookup"><span data-stu-id="8c5cb-128">FAQ</span></span>
1. <span data-ttu-id="8c5cb-129">모든 Azure 서비스에 예약된 IP를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="8c5cb-129">Can I use a reserved IP for all Azure services?</span></span> <br>
    <span data-ttu-id="8c5cb-130">아니요.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-130">No.</span></span> <span data-ttu-id="8c5cb-131">예약된 IP는 VM 및 VIP를 통해 노출되는 클라우드 서비스 인스턴스 역할에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-131">Reserved IPs can only be used for VMs and cloud service instance roles exposed through a VIP.</span></span>
2. <span data-ttu-id="8c5cb-132">예약된 IP를 몇 개까지 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="8c5cb-132">How many reserved IPs can I have?</span></span> <br>
    <span data-ttu-id="8c5cb-133">자세한 내용은 참조 hello [Azure 제한](../azure-subscription-service-limits.md#networking-limits) 문서.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-133">For details, see hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
3. <span data-ttu-id="8c5cb-134">예약된 IP는 사용 요금이 있나요?</span><span class="sxs-lookup"><span data-stu-id="8c5cb-134">Is there a charge for reserved IPs?</span></span> <br>
    <span data-ttu-id="8c5cb-135">때때로 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-135">Sometimes.</span></span> <span data-ttu-id="8c5cb-136">가격 세부 정보를 보려면 참조 hello [예약 된 IP 주소 가격 정보](http://go.microsoft.com/fwlink/?LinkID=398482) 페이지.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-136">For pricing details, see hello [Reserved IP Address Pricing Details](http://go.microsoft.com/fwlink/?LinkID=398482) page.</span></span>
4. <span data-ttu-id="8c5cb-137">IP 주소를 어떻게 예약하나요?</span><span class="sxs-lookup"><span data-stu-id="8c5cb-137">How do I reserve an IP address?</span></span> <br>
    <span data-ttu-id="8c5cb-138">PowerShell을 사용할 있습니다, hello [Azure 관리 REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx), 또는 hello [Azure 포털](https://portal.azure.com) tooreserve Azure 지역에서 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-138">You can use PowerShell, hello [Azure Management REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx), or hello [Azure portal](https://portal.azure.com) tooreserve an IP address in an Azure region.</span></span> <span data-ttu-id="8c5cb-139">예약 된 IP 주소 연결된 tooyour 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-139">A reserved IP address is associated tooyour subscription.</span></span>
5. <span data-ttu-id="8c5cb-140">선호도 그룹 기반 VNet에서 예약된 IP를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="8c5cb-140">Can I use a reserved IP with affinity group-based VNets?</span></span> <br>
    <span data-ttu-id="8c5cb-141">아니요.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-141">No.</span></span> <span data-ttu-id="8c5cb-142">예약된 IP는 지역 VNet에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-142">Reserved IPs are only supported in regional VNets.</span></span> <span data-ttu-id="8c5cb-143">예약된 IP는 선호도 그룹과 연결된 VNet에 대해 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-143">Reserved IPs are not supported for VNets that are associated with affinity groups.</span></span> <span data-ttu-id="8c5cb-144">VNet 지역 또는 선호도 그룹을 연결 하는 방법에 대 한 자세한 내용은 참조 hello [지역 Vnet 및 선호도 그룹](virtual-networks-migrate-to-regional-vnet.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-144">For more information about associating a VNet with a region or affinity group, see hello [About Regional VNets and Affinity Groups](virtual-networks-migrate-to-regional-vnet.md) article.</span></span>

## <a name="manage-reserved-vips"></a><span data-ttu-id="8c5cb-145">예약된 VIP 관리</span><span class="sxs-lookup"><span data-stu-id="8c5cb-145">Manage reserved VIPs</span></span>

<span data-ttu-id="8c5cb-146">설치 하 고 PowerShell hello의 hello 단계를 완료 하 여 구성 확인 [설치 PowerShell을 구성 하 고](/powershell/azure/overview) 문서.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-146">Ensure you have installed and configured PowerShell by completing hello steps in hello [Install and configure PowerShell](/powershell/azure/overview) article.</span></span> 

<span data-ttu-id="8c5cb-147">예약 된 Ip를 사용 하려면 먼저 tooyour 구독을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-147">Before you can use reserved IPs, you must add it tooyour subscription.</span></span> <span data-ttu-id="8c5cb-148">공용 IP의 hello 풀에서 예약 된 IP toocreate hello에 사용할 수 있는 주소 *중앙 미국* hello 다음 명령을 실행 합니다. 위치:</span><span class="sxs-lookup"><span data-stu-id="8c5cb-148">toocreate a reserved IP from hello pool of public IP addresses available in hello *Central US* location, run hello following command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"
```

<span data-ttu-id="8c5cb-149">그러나 예약할 IP를 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-149">Notice, however, that you cannot specify what IP is being reserved.</span></span> <span data-ttu-id="8c5cb-150">tooview에서는 어떤 IP 주소 hello 다음 PowerShell 명령을 실행 합니다. 구독에서 예약 되어 있으며 hello 값에 유의 하세요 *ReservedIPName* 및 *주소*:</span><span class="sxs-lookup"><span data-stu-id="8c5cb-150">tooview what IP addresses are reserved in your subscription, run hello following PowerShell command, and notice hello values for *ReservedIPName* and *Address*:</span></span>

```powershell
Get-AzureReservedIP
```

<span data-ttu-id="8c5cb-151">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="8c5cb-151">Expected output:</span></span>

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
><span data-ttu-id="8c5cb-152">PowerShell 사용 하 여 예약된 된 IP 주소를 만들 때의 리소스 그룹 toocreate hello 예약 된 IP를 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-152">When you create a reserved IP address with PowerShell, you cannot specify a resource group toocreate hello reserved IP in.</span></span> <span data-ttu-id="8c5cb-153">Azure에서 *Default-Networking*이라는 리소스 그룹에 자동으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-153">Azure places it into a resource group named *Default-Networking* automatically.</span></span> <span data-ttu-id="8c5cb-154">Hello를 사용 하 여 hello 예약 된 IP를 만들면 [Azure 포털](http://portal.azure.com), 선택한 리소스 그룹을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-154">If you create hello reserved IP using hello [Azure portal](http://portal.azure.com), you can specify any resource group you choose.</span></span> <span data-ttu-id="8c5cb-155">그러나 이외의 다른 리소스 그룹에서 hello 예약 된 IP를 만드는 경우 *기본 네트워킹* 참조할 경우 항상 hello 예약 된 IP 명령과 같은 `Get-AzureReservedIP` 및 `Remove-AzureReservedIP`, hello이름을참조해야*그룹 리소스 그룹 이름 예약 된 ip 이름 간*합니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-155">If you create hello reserved IP in a resource group other than *Default-Networking* however, whenever you reference hello reserved IP with commands such as `Get-AzureReservedIP` and `Remove-AzureReservedIP`, you must reference hello name *Group resource-group-name reserved-ip-name*.</span></span>  <span data-ttu-id="8c5cb-156">예를 들어, 명명 된 예약된 된 IP를 만들면 *인 myReservedIP* 리소스 그룹 이름은 *myResourceGroup*,으로 hello 예약 된 IP의 hello 이름을 참조 해야 *그룹 myResourceGroup 인 myReservedIP*합니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-156">For example, if you create a reserved IP named *myReservedIP* in a resource group named *myResourceGroup*, you must reference hello name of hello reserved IP as *Group myResourceGroup myReservedIP*.</span></span>   

<span data-ttu-id="8c5cb-157">IP 예약 되 면 삭제 하기 전까지 연결된 tooyour 구독 남아 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-157">Once an IP is reserved, it remains associated tooyour subscription until you delete it.</span></span> <span data-ttu-id="8c5cb-158">toodelete 예약 된 IP 다음 PowerShell 명령이 실행된 hello:</span><span class="sxs-lookup"><span data-stu-id="8c5cb-158">toodelete a reserved IP, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIP -ReservedIPName "MyReservedIP"
```

## <a name="reserve-hello-ip-address-of-an-existing-cloud-service"></a><span data-ttu-id="8c5cb-159">기존 클라우드 서비스의 hello IP 주소를 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-159">Reserve hello IP address of an existing cloud service</span></span>
<span data-ttu-id="8c5cb-160">Hello를 추가 하 여 기존 클라우드 서비스의 hello IP 주소를 예약할 수 있습니다 `-ServiceName` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-160">You can reserve hello IP address of an existing cloud service by adding hello `-ServiceName` parameter.</span></span> <span data-ttu-id="8c5cb-161">클라우드 서비스의 tooreserve hello IP 주소 *TestService* hello에 *중앙 미국* hello 다음 PowerShell 명령을 실행 합니다. 위치:</span><span class="sxs-lookup"><span data-stu-id="8c5cb-161">tooreserve hello IP address of a cloud service *TestService* in hello *Central US* location, run hello following PowerShell command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US" -ServiceName TestService
```

## <a name="associate-a-reserved-ip-tooa-new-cloud-service"></a><span data-ttu-id="8c5cb-162">예약 된 IP tooa 새 클라우드 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="8c5cb-162">Associate a reserved IP tooa new cloud service</span></span>
<span data-ttu-id="8c5cb-163">hello 다음 스크립트에서는 새로운 예약된 된 IP 다음 라는 tooa 새 클라우드 서비스가 연결 *TestService*합니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-163">hello following script creates a new reserved IP, then associates it tooa new cloud service named *TestService*.</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService -ReservedIPName MyReservedIP -Location "Central US"
```

> [!NOTE]
> <span data-ttu-id="8c5cb-164">사용 하 여 toohello VM 클라우드 서비스와 예약 된 IP toouse를 만들면 여전히 참조 *VIP:&lt;포트 번호 >* 인바운드 통신에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-164">When you create a reserved IP toouse with a cloud service, you still refer toohello VM by using *VIP:&lt;port number>* for inbound communication.</span></span> <span data-ttu-id="8c5cb-165">IP 예약 의미가 toohello VM에 직접 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-165">Reserving an IP does not mean you can connect toohello VM directly.</span></span> <span data-ttu-id="8c5cb-166">hello 예약 된 IP가 할당 toohello 클라우드 서비스 VM이 배포 된 hello 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-166">hello reserved IP is assigned toohello cloud service that hello VM has been deployed to.</span></span> <span data-ttu-id="8c5cb-167">직접 tooconnect tooa IP 통해 VM을 원하는 경우 인스턴스 수준 공용 IP tooconfigure 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-167">If you want tooconnect tooa VM by IP directly, you have tooconfigure an instance-level public IP.</span></span> <span data-ttu-id="8c5cb-168">인스턴스 수준 공용 IP는 VM tooyour 직접 할당 된 공용 IP (한 ILPIP 라고 함)의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-168">An instance-level public IP is a type of public IP (called an ILPIP) that is assigned directly tooyour VM.</span></span> <span data-ttu-id="8c5cb-169">ILPIP는 예약할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-169">It cannot be reserved.</span></span> <span data-ttu-id="8c5cb-170">자세한 내용은 hello 읽을 [인스턴스 수준 공용 IP (ILPIP)](virtual-networks-instance-level-public-ip.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-170">For more information, read hello [Instance-level Public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) article.</span></span>
> 

## <a name="remove-a-reserved-ip-from-a-running-deployment"></a><span data-ttu-id="8c5cb-171">실행 중인 배포에서 예약된 IP 제거</span><span class="sxs-lookup"><span data-stu-id="8c5cb-171">Remove a reserved IP from a running deployment</span></span>
<span data-ttu-id="8c5cb-172">tooremove 예약 된 IP 추가 tooa 새 클라우드 서비스를 hello 다음 PowerShell 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-172">tooremove a reserved IP added tooa new cloud service, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService
```

> [!NOTE]
> <span data-ttu-id="8c5cb-173">실행 중인 배포에서 예약된 된 IP를 제거 해도 구독에서 hello 예약이 제거 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-173">Removing a reserved IP from a running deployment does not remove hello reservation from your subscription.</span></span> <span data-ttu-id="8c5cb-174">단순히 구독에서 다른 리소스에서 사용 하는 hello IP toobe를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-174">It simply frees hello IP toobe used by another resource in your subscription.</span></span>
> 

## <a name="associate-a-reserved-ip-tooa-running-deployment"></a><span data-ttu-id="8c5cb-175">배포 실행 예약 된 IP tooa 연결</span><span class="sxs-lookup"><span data-stu-id="8c5cb-175">Associate a reserved IP tooa running deployment</span></span>
<span data-ttu-id="8c5cb-176">hello 다음 명령을 클라우드 서비스를 만들 라는 *TestService2* 명명 된 새 VM과 *TestVM2*합니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-176">hello following commands create a cloud service named *TestService2* with a new VM named *TestVM2*.</span></span> <span data-ttu-id="8c5cb-177">예약 된 IP 이름이 hello 기존 *인 MyReservedIP* 관련된 toohello 클라우드 서비스에 있으면 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-177">hello existing reserved IP named *MyReservedIP* is then associated toohello cloud service.</span></span>

```powershell
$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM2 -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService2 -Location "Central US"

Set-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService2
```

## <a name="associate-a-reserved-ip-tooa-cloud-service-by-using-a-service-configuration-file"></a><span data-ttu-id="8c5cb-178">서비스 구성 파일을 사용 하 여 예약 된 IP tooa 클라우드 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="8c5cb-178">Associate a reserved IP tooa cloud service by using a service configuration file</span></span>
<span data-ttu-id="8c5cb-179">서비스 구성 (CSCFG) 파일을 사용 하 여 예약 된 IP tooa 클라우드 서비스를 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-179">You can also associate a reserved IP tooa cloud service by using a service configuration (CSCFG) file.</span></span> <span data-ttu-id="8c5cb-180">hello 다음 샘플 xml 표시 방법을 tooconfigure 예약 된 VIP는 클라우드 서비스 toouse 라는 *인 MyReservedIP*:</span><span class="sxs-lookup"><span data-stu-id="8c5cb-180">hello following sample xml shows how tooconfigure a cloud service toouse a reserved VIP named *MyReservedIP*:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8c5cb-181">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8c5cb-181">Next steps</span></span>
* <span data-ttu-id="8c5cb-182">이해 어떻게 [IP 주소 지정](virtual-network-ip-addresses-overview-classic.md) hello 클래식 배포 모델에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-182">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in hello classic deployment model.</span></span>
* <span data-ttu-id="8c5cb-183">[예약된 개인 IP 주소](virtual-networks-reserved-private-ip.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-183">Learn about [reserved private IP addresses](virtual-networks-reserved-private-ip.md).</span></span>
* <span data-ttu-id="8c5cb-184">[ILPIP(인스턴스 수준 공용 IP) 주소](virtual-networks-instance-level-public-ip.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-184">Learn about [Instance Level Public IP (ILPIP) addresses](virtual-networks-instance-level-public-ip.md).</span></span>

