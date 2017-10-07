---
title: "aaaStatic 내부 개인 IP-Azure VM-클래식"
description: "고정 내부 Ip (Dip)를 이해 하 고 어떻게 toomanage에"
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
ms.openlocfilehash: 5abe1c59f2f3ed19bcf56c269dfe57ac32d4f601
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-a-static-internal-private-ip-address-using-powershell-classic"></a><span data-ttu-id="20816-103">PowerShell (클래식)를 사용 하 여 고정 내부 개인 IP tooset을 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="20816-103">How tooset a static internal private IP address using PowerShell (Classic)</span></span>
<span data-ttu-id="20816-104">대부분의 경우에서 가상 컴퓨터에 대 한 고정 내부 IP 주소 toospecify가 필요 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="20816-104">In most cases, you won’t need toospecify a static internal IP address for your virtual machine.</span></span> <span data-ttu-id="20816-105">가상 네트워크의 VM은 사용자가 지정한 범위의 내부 IP 주소를 자동으로 받습니다.</span><span class="sxs-lookup"><span data-stu-id="20816-105">VMs in a virtual network will automatically receive an internal IP address from a range that you specify.</span></span> <span data-ttu-id="20816-106">그러나 특정한 상황에서는 특정 VM에 고정 IP 주소를 지정하는 것이 적합한 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20816-106">But in certain cases, specifying a static IP address for a particular VM makes sense.</span></span> <span data-ttu-id="20816-107">예를 들어 VM은 진행 중인 toorun DNS 또는 도메인 컨트롤러가 될 경우.</span><span class="sxs-lookup"><span data-stu-id="20816-107">For example, if your VM is going toorun DNS or will be a domain controller.</span></span> <span data-ttu-id="20816-108">고정 내부 IP 주소에 hello VM 중지/프로 비전 해제 상태 통한 경우에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="20816-108">A static internal IP address stays with hello VM even through a stop/deprovision state.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="20816-109">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20816-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="20816-110">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="20816-110">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="20816-111">대부분의 새로운 배포 hello를 사용 하는 것이 좋습니다 [리소스 관리자 배포 모델](virtual-networks-static-private-ip-arm-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="20816-111">Microsoft recommends that most new deployments use hello [Resource Manager deployment model](virtual-networks-static-private-ip-arm-ps.md).</span></span>
> 
> 

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a><span data-ttu-id="20816-112">어떻게 tooverify 특정 IP 주소를 사용할 수 있는 경우</span><span class="sxs-lookup"><span data-stu-id="20816-112">How tooverify if a specific IP address is available</span></span>
<span data-ttu-id="20816-113">tooverify 경우 hello IP 주소 *10.0.0.7* 라는 vnet에 사용할 수 *TestVnet*, hello 다음 PowerShell 명령을 실행 하 고 확인에 대 한 hello 값 *IsAvailable*:</span><span class="sxs-lookup"><span data-stu-id="20816-113">tooverify if hello IP address *10.0.0.7* is available in a vnet named *TestVnet*, run hello following PowerShell command and verify hello value for *IsAvailable*:</span></span>

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> <span data-ttu-id="20816-114">Tootest hello 명령을 위에 안전한 환경에서 원하는 경우 hello 지침에 따라 [가상 네트워크 (클래식)를 만들고](virtual-networks-create-vnet-classic-pportal.md) toocreate 라는 vnet *TestVnet* hello를 사용 하 여 확인  *10.0.0.0/8* 주소 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="20816-114">If you want tootest hello command above in a safe environment follow hello guidelines in [Create a virtual network (classic)](virtual-networks-create-vnet-classic-pportal.md) toocreate a vnet named *TestVnet* and ensure it uses hello *10.0.0.0/8* address space.</span></span>
> 
> 

## <a name="how-toospecify-a-static-internal-ip-when-creating-a-vm"></a><span data-ttu-id="20816-115">어떻게 toospecify VM을 만들 때 고정 내부 IP</span><span class="sxs-lookup"><span data-stu-id="20816-115">How toospecify a static internal IP when creating a VM</span></span>
<span data-ttu-id="20816-116">hello 아래의 PowerShell 스크립트 라는 새 클라우드 서비스를 만듭니다. *TestService*다음 Azure에서 이미지를 검색 합니다 V 만듭니다 *TestVM* hello hello 검색 이미지를 사용 하는 새 클라우드 서비스 집합 이라는 서브넷에 VM toobe hello *서브넷-1*, 설정 및 *10.0.0.7* hello VM에 대 한 정적 내부 ip:</span><span class="sxs-lookup"><span data-stu-id="20816-116">hello PowerShell script below creates a new cloud service named *TestService*, then retrieves an image from Azure, then creates a VM named *TestVM* in hello new cloud service using hello retrieved image, sets hello VM toobe in a subnet named *Subnet-1*, and sets *10.0.0.7* as a static internal IP for hello VM:</span></span>

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-tooretrieve-static-internal-ip-information-for-a-vm"></a><span data-ttu-id="20816-117">어떻게 tooretrieve 정적 내부 IP에 대 한 정보는 VM</span><span class="sxs-lookup"><span data-stu-id="20816-117">How tooretrieve static internal IP information for a VM</span></span>
<span data-ttu-id="20816-118">tooview hello 고정 내부 IP 정보 hello에 대 한 위의 hello 스크립트를 사용 하 여 만든 VM hello 다음 PowerShell 명령을 실행 하 고 hello에 대 한 값이 확인 *IpAddress*:</span><span class="sxs-lookup"><span data-stu-id="20816-118">tooview hello static internal IP information for hello VM created with hello script above, run hello following PowerShell command and observe hello values for *IpAddress*:</span></span>

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

## <a name="how-tooremove-a-static-internal-ip-from-a-vm"></a><span data-ttu-id="20816-119">어떻게 tooremove VM에서 고정 내부 ip 주소</span><span class="sxs-lookup"><span data-stu-id="20816-119">How tooremove a static internal IP from a VM</span></span>
<span data-ttu-id="20816-120">tooremove hello 고정 내부 IP hello 다음 PowerShell 명령을 실행 toohello VM 위의 hello 스크립트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="20816-120">tooremove hello static internal IP added toohello VM in hello script above, run hello following PowerShell command:</span></span>

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-tooadd-a-static-internal-ip-tooan-existing-vm"></a><span data-ttu-id="20816-121">어떻게 tooadd 정적 내부 IP tooan 기존 VM</span><span class="sxs-lookup"><span data-stu-id="20816-121">How tooadd a static internal IP tooan existing VM</span></span>
<span data-ttu-id="20816-122">tooadd 정적 내부 IP toohello 사용 하 여 만든 녀석 위의 hello 스크립트 명령을 다음 VM:</span><span class="sxs-lookup"><span data-stu-id="20816-122">tooadd a static internal IP toohello VM created using hello script above, runt he following command:</span></span>

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="20816-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="20816-123">Next steps</span></span>
[<span data-ttu-id="20816-124">예약된 IP</span><span class="sxs-lookup"><span data-stu-id="20816-124">Reserved IP</span></span>](virtual-networks-reserved-public-ip.md)

[<span data-ttu-id="20816-125">인스턴스 수준 공용 IP(ILPIP)</span><span class="sxs-lookup"><span data-stu-id="20816-125">Instance-Level Public IP (ILPIP)</span></span>](virtual-networks-instance-level-public-ip.md)

[<span data-ttu-id="20816-126">예약된 IP REST API</span><span class="sxs-lookup"><span data-stu-id="20816-126">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)

