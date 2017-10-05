---
title: "고정 내부 개인 IP - Azure VM - 클래식"
description: "고정 내부 개인 IP(DIP) 및 관리 방법 이해"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 93444c6f-af1b-41f8-a035-77f5c0302bf0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.openlocfilehash: cf9ee59ca4e44ed01836c2efb1f4df5f073bf6e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-set-a-static-internal-private-ip-address-using-powershell-classic"></a><span data-ttu-id="c323d-103">PowerShell을 사용하여 고정 내부 개인 IP를 설정하는 방법(기본)</span><span class="sxs-lookup"><span data-stu-id="c323d-103">How to set a static internal private IP address using PowerShell (Classic)</span></span>
<span data-ttu-id="c323d-104">대부분의 경우 가상 컴퓨터에 고정 내부 IP 주소를 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c323d-104">In most cases, you won’t need to specify a static internal IP address for your virtual machine.</span></span> <span data-ttu-id="c323d-105">가상 네트워크의 VM은 사용자가 지정한 범위의 내부 IP 주소를 자동으로 받습니다.</span><span class="sxs-lookup"><span data-stu-id="c323d-105">VMs in a virtual network will automatically receive an internal IP address from a range that you specify.</span></span> <span data-ttu-id="c323d-106">그러나 특정한 상황에서는 특정 VM에 고정 IP 주소를 지정하는 것이 적합한 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c323d-106">But in certain cases, specifying a static IP address for a particular VM makes sense.</span></span> <span data-ttu-id="c323d-107">예를 들어 VM에서 DNS를 실행하거나 VM을 도메인 컨트롤러로 구성하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="c323d-107">For example, if your VM is going to run DNS or will be a domain controller.</span></span> <span data-ttu-id="c323d-108">고정 내부 IP 주소는 중지 상태 및 프로비전 해제 상태에서도 VM에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="c323d-108">A static internal IP address stays with the VM even through a stop/deprovision state.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c323d-109">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c323d-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c323d-110">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c323d-110">This article covers using the classic deployment model.</span></span> <span data-ttu-id="c323d-111">새로운 배포는 대부분 [Resource Manager 배포 모델](virtual-networks-static-private-ip-arm-ps.md)을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c323d-111">Microsoft recommends that most new deployments use the [Resource Manager deployment model](virtual-networks-static-private-ip-arm-ps.md).</span></span>
> 
> 

## <a name="how-to-verify-if-a-specific-ip-address-is-available"></a><span data-ttu-id="c323d-112">특정 IP 주소를 사용할 수 있는지 확인하는 방법</span><span class="sxs-lookup"><span data-stu-id="c323d-112">How to verify if a specific IP address is available</span></span>
<span data-ttu-id="c323d-113">IP 주소 *10.0.0.7*을 *TestVnet*이라는 이름의 VNet에서 사용할 수 있는지 확인하려면 다음 PowerShell 명령을 실행하고 *IsAvailable* 값을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c323d-113">To verify if the IP address *10.0.0.7* is available in a vnet named *TestVnet*, run the following PowerShell command and verify the value for *IsAvailable*:</span></span>

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> <span data-ttu-id="c323d-114">안전한 환경에서 위 명령을 테스트하려는 경우 [가상 네트워크 만들기(클래식)](virtual-networks-create-vnet-classic-pportal.md)의 지침에 따라 *TestVnet*이라는 이름의 VNet을 만들어 *10.0.0.0/8* 주소 공간을 사용하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c323d-114">If you want to test the command above in a safe environment follow the guidelines in [Create a virtual network (classic)](virtual-networks-create-vnet-classic-pportal.md) to create a vnet named *TestVnet* and ensure it uses the *10.0.0.0/8* address space.</span></span>
> 
> 

## <a name="how-to-specify-a-static-internal-ip-when-creating-a-vm"></a><span data-ttu-id="c323d-115">VM을 만들 때 고정 내부 IP를 지정하는 방법</span><span class="sxs-lookup"><span data-stu-id="c323d-115">How to specify a static internal IP when creating a VM</span></span>
<span data-ttu-id="c323d-116">아래의 PowerShell 스크립트는 *TestService*라는 새 클라우드 서비스를 만들고 Azure에서 이미지를 검색합니다. 그다음에 이 이미지를 사용하여 새 클라우드 서비스에 *TestVM*이라는 VM을 만들고 이 VM을 *Subnet-1*이라는 서브넷에 속하도록 설정하고 VM의 고정 내부 IP로 *10.0.0.7*을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c323d-116">The PowerShell script below creates a new cloud service named *TestService*, then retrieves an image from Azure, then creates a VM named *TestVM* in the new cloud service using the retrieved image, sets the VM to be in a subnet named *Subnet-1*, and sets *10.0.0.7* as a static internal IP for the VM:</span></span>

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-to-retrieve-static-internal-ip-information-for-a-vm"></a><span data-ttu-id="c323d-117">VM의 고정 내부 IP 정보를 검색하는 방법</span><span class="sxs-lookup"><span data-stu-id="c323d-117">How to retrieve static internal IP information for a VM</span></span>
<span data-ttu-id="c323d-118">위의 스크립트를 사용하여 만든 VM의 고정 내부 IP 정보를 보려면 다음 PowerShell 명령을 실행하고 *IpAddress*의 값을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c323d-118">To view the static internal IP information for the VM created with the script above, run the following PowerShell command and observe the values for *IpAddress*:</span></span>

    Get-AzureVM -Name TestVM -ServiceName TestService

    DeploymentName              : TestService
    Name                        : TestVM
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : Provisioning
    IpAddress                   : 10.0.0.7
    InstanceStateDetails        : Windows is preparing your computer for first use...
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : TestVM
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : rsR2-797
    AvailabilitySetName         : 
    DNSName                     : http://testservice000.cloudapp.net/
    Status                      : Provisioning
    GuestAgentStatus            : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 
    PublicIPName                : 
    NetworkInterfaces           : {}
    ServiceName                 : TestService
    OperationDescription        : Get-AzureVM
    OperationId                 : 34c1560a62f0901ab75cde4fed8e8bd1
    OperationStatus             : OK

## <a name="how-to-remove-a-static-internal-ip-from-a-vm"></a><span data-ttu-id="c323d-119">VM에서 고정 내부 IP를 제거하는 방법</span><span class="sxs-lookup"><span data-stu-id="c323d-119">How to remove a static internal IP from a VM</span></span>
<span data-ttu-id="c323d-120">위의 스크립트에서 VM에 추가된 고정 내부 IP를 제거하려면 다음 PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c323d-120">To remove the static internal IP added to the VM in the script above, run the following PowerShell command:</span></span>

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-to-add-a-static-internal-ip-to-an-existing-vm"></a><span data-ttu-id="c323d-121">기존 VM에 고정 내부 IP를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="c323d-121">How to add a static internal IP to an existing VM</span></span>
<span data-ttu-id="c323d-122">위의 스크립트를 사용하여 만든 VM에 고정 내부 IP를 추가하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c323d-122">To add a static internal IP to the VM created using the script above, runt he following command:</span></span>

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="c323d-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c323d-123">Next steps</span></span>
[<span data-ttu-id="c323d-124">예약된 IP</span><span class="sxs-lookup"><span data-stu-id="c323d-124">Reserved IP</span></span>](virtual-networks-reserved-public-ip.md)

[<span data-ttu-id="c323d-125">인스턴스 수준 공용 IP(ILPIP)</span><span class="sxs-lookup"><span data-stu-id="c323d-125">Instance-Level Public IP (ILPIP)</span></span>](virtual-networks-instance-level-public-ip.md)

[<span data-ttu-id="c323d-126">예약된 IP REST API</span><span class="sxs-lookup"><span data-stu-id="c323d-126">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)

