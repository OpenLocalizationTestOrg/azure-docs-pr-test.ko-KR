---
title: "Vm (클래식)-Azure PowerShell에 대 한 aaaConfigure 개인 IP 주소 | Microsoft Docs"
description: "Tooconfigure 개인 IP PowerShell을 사용 하 여 가상 컴퓨터 (클래식)를 해결 하는 방법을 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 60c7b489-46ae-48af-a453-2b429a474afd
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 99546ee9c2c4eb9aa7b67f30721d37ef9b2944f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-powershell"></a><span data-ttu-id="cd9ec-103">PowerShell을 사용하여 가상 컴퓨터(클래식)에 대한 개인 IP 주소 구성</span><span class="sxs-lookup"><span data-stu-id="cd9ec-103">Configure private IP addresses for a virtual machine (Classic) using PowerShell</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="cd9ec-104">이 문서에서는 hello 클래식 배포 모델에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd9ec-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="cd9ec-105">수도 있습니다 [hello 리소스 관리자 배포 모델에서 정적 개인 IP 주소 관리](virtual-networks-static-private-ip-arm-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cd9ec-105">You can also [manage a static private IP address in hello Resource Manager deployment model](virtual-networks-static-private-ip-arm-ps.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="cd9ec-106">아래의 hello 예제 PowerShell 명령을 이미 만든 단순한 환경을 기대 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd9ec-106">hello sample PowerShell commands below expect a simple environment already created.</span></span> <span data-ttu-id="cd9ec-107">이 문서에 표시 된 대로 toorun hello 명령을 원하는 경우 먼저 hello 테스트 환경을 구축에 설명 된 [VNet을 만든](virtual-networks-create-vnet-classic-netcfg-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cd9ec-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [Create a VNet](virtual-networks-create-vnet-classic-netcfg-ps.md).</span></span>

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a><span data-ttu-id="cd9ec-108">어떻게 tooverify 특정 IP 주소를 사용할 수 있는 경우</span><span class="sxs-lookup"><span data-stu-id="cd9ec-108">How tooverify if a specific IP address is available</span></span>
<span data-ttu-id="cd9ec-109">tooverify 경우 hello IP 주소 *192.168.1.101* 라는 VNet에 사용할 수 *TestVNet*, hello 다음 PowerShell 명령을 실행 하 고 확인에 대 한 hello 값 *IsAvailable*:</span><span class="sxs-lookup"><span data-stu-id="cd9ec-109">tooverify if hello IP address *192.168.1.101* is available in a VNet named *TestVNet*, run hello following PowerShell command and verify hello value for *IsAvailable*:</span></span>

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 192.168.1.101 

<span data-ttu-id="cd9ec-110">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="cd9ec-110">Expected output:</span></span>

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="cd9ec-111">어떻게 toospecify 정적 개인 IP 주소는 VM을 만들 때</span><span class="sxs-lookup"><span data-stu-id="cd9ec-111">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="cd9ec-112">아래의 PowerShell 스크립트 hello 라는 새 클라우드 서비스를 만듭니다 *TestService*, 그런 다음 Azure에서 이미지를 검색, 명명 된 VM을 만듭니다 *DNS01* hello 새 클라우드 서비스에 hello 검색 이미지를 사용 하 여 설정 명명 된 서브넷에 VM toobe hello *프런트 엔드*, 설정 및 *192.168.1.7* hello VM에 대 한 정적 개인 IP 주소와:</span><span class="sxs-lookup"><span data-stu-id="cd9ec-112">hello PowerShell script below creates a new cloud service named *TestService*, then retrieves an image from Azure, creates a VM named *DNS01* in hello new cloud service using hello retrieved image, sets hello VM toobe in a subnet named *FrontEnd*, and sets *192.168.1.7* as a static private IP address for hello VM:</span></span>

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage | where {$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name DNS01 -InstanceSize Small -ImageName $image.ImageName |
      Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! |
      Set-AzureSubnet –SubnetNames FrontEnd |
      Set-AzureStaticVNetIP -IPAddress 192.168.1.7 |
      New-AzureVM -ServiceName TestService –VNetName TestVNet

<span data-ttu-id="cd9ec-113">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="cd9ec-113">Expected output:</span></span>

    WARNING: No deployment found in service: 'TestService'.
    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    New-AzureService     fcf705f1-d902-011c-95c7-b690735e7412 Succeeded      
    New-AzureVM          3b99a86d-84f8-04e5-888e-b6fc3c73c4b9 Succeeded  

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="cd9ec-114">어떻게 tooretrieve 정적 개인 IP 주소는 VM에 대 한 정보</span><span class="sxs-lookup"><span data-stu-id="cd9ec-114">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="cd9ec-115">tooview hello 정적 개인 IP 주소 VM hello 다음 PowerShell 명령을 실행 합니다. 위의 hello 스크립트를 사용 하 여 만든 hello에 대 한 정보 및 hello에 대 한 값이 확인 *IpAddress*:</span><span class="sxs-lookup"><span data-stu-id="cd9ec-115">tooview hello static private IP address information for hello VM created with hello script above, run hello following PowerShell command and observe hello values for *IpAddress*:</span></span>

    Get-AzureVM -Name DNS01 -ServiceName TestService

<span data-ttu-id="cd9ec-116">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="cd9ec-116">Expected output:</span></span>

    DeploymentName              : TestService
    Name                        : DNS01
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : Provisioning
    IpAddress                   : 192.168.1.7
    InstanceStateDetails        : Windows is preparing your computer for first use...
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : DNS01
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

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="cd9ec-117">어떻게 tooremove 정적 개인 IP는 VM에서을 해결합니다</span><span class="sxs-lookup"><span data-stu-id="cd9ec-117">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="cd9ec-118">다음 PowerShell 명령이 실행된 hello 위의 hello 스크립트 toohello VM을 추가 하는 tooremove hello 정적 개인 IP 주소:</span><span class="sxs-lookup"><span data-stu-id="cd9ec-118">tooremove hello static private IP address added toohello VM in hello script above, run hello following PowerShell command:</span></span>

    Get-AzureVM -ServiceName TestService -Name DNS01 |
      Remove-AzureStaticVNetIP |
      Update-AzureVM

<span data-ttu-id="cd9ec-119">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="cd9ec-119">Expected output:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Update-AzureVM       052fa6f6-1483-0ede-a7bf-14f91f805483 Succeeded

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="cd9ec-120">정적 개인 IP tooadd tooan 기존 VM을 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="cd9ec-120">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="cd9ec-121">정적 개인 IP 주소 toohello VM 사용 하 여 만든 녀석 위의 hello 스크립트 명령을 다음 tooadd:</span><span class="sxs-lookup"><span data-stu-id="cd9ec-121">tooadd a static private IP address toohello VM created using hello script above, runt he following command:</span></span>

    Get-AzureVM -ServiceName TestService -Name DNS01 |
      Set-AzureStaticVNetIP -IPAddress 192.168.1.7 |
      Update-AzureVM

<span data-ttu-id="cd9ec-122">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="cd9ec-122">Expected output:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Update-AzureVM       77d8cae2-87e6-0ead-9738-7c7dae9810cb Succeeded 

## <a name="next-steps"></a><span data-ttu-id="cd9ec-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cd9ec-123">Next steps</span></span>
* <span data-ttu-id="cd9ec-124">[예약된 공용 IP](virtual-networks-reserved-public-ip.md) 주소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cd9ec-124">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="cd9ec-125">[ILPIP(인스턴스 수준 공용 IP)](virtual-networks-instance-level-public-ip.md) 주소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cd9ec-125">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="cd9ec-126">Hello 참조 [예약 된 IP REST Api](https://msdn.microsoft.com/library/azure/dn722420.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="cd9ec-126">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

