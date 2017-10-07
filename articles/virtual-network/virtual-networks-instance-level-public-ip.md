---
title: "aaaAzure 인스턴스 수준 공용 IP (클래식) 주소 | Microsoft Docs"
description: "인스턴스 수준 공용 IP (ILPIP) 주소를 이해 하 고 어떻게 toomanage PowerShell을 사용 하 게 합니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 07eef6ec-7dfe-4c4d-a2c2-be0abfb48ec5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: 832143ee6fdd80b634e1cebfddc759a8cacda583
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="instance-level-public-ip-classic-overview"></a><span data-ttu-id="8a582-103">인스턴스 수준 공용 Ip(클래식) 개요</span><span class="sxs-lookup"><span data-stu-id="8a582-103">Instance level public IP (Classic) overview</span></span>
<span data-ttu-id="8a582-104">인스턴스 수준 공용 IP (ILPIP)는 toohello 클라우드 서비스에 있는 VM 또는 역할 인스턴스에 보다는 tooa 클라우드 서비스 또는 VM 역할 인스턴스를 직접 할당할 수 있는 공용 IP 주소.</span><span class="sxs-lookup"><span data-stu-id="8a582-104">An instance level public IP (ILPIP) is a public IP address that you can assign directly tooa VM or Cloud Services role instance, rather than toohello cloud service that your VM or role instance reside in.</span></span> <span data-ttu-id="8a582-105">ILPIP hello 대신 tooyour 클라우드 서비스에 할당 된 hello 가상 IP (VIP)를 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8a582-105">An ILPIP doesn’t take hello place of hello virtual IP (VIP) that is assigned tooyour cloud service.</span></span> <span data-ttu-id="8a582-106">보다 tooconnect를 사용할 수 있는 추가 IP 주소를는 직접 tooyour VM 또는 역할 인스턴스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a582-106">Rather, it’s an additional IP address that you can use tooconnect directly tooyour VM or role instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8a582-107">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a582-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="8a582-108">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a582-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="8a582-109">Resource Manager를 통해 VM을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8a582-109">Microsoft recommends creating VMs through Resource Manager.</span></span> <span data-ttu-id="8a582-110">Azure에서 [IP 주소](virtual-network-ip-addresses-overview-classic.md) 가 어떻게 작동하는지 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a582-110">Make sure you understand how [IP addresses](virtual-network-ip-addresses-overview-classic.md) work in Azure.</span></span>

![ILPIP 및 VIP 간의 차이](./media/virtual-networks-instance-level-public-ip/Figure1.png)

<span data-ttu-id="8a582-112">VIP를 사용 하 여 hello 클라우드 서비스에 액세스 하는 그림 1에 나와 있는 것 처럼, hello 하는 동안 개별 Vm은 일반적으로 사용 하 여 액세스할 VIP:&lt;포트 번호&gt;합니다.</span><span class="sxs-lookup"><span data-stu-id="8a582-112">As shown in Figure 1, hello cloud service is accessed using a VIP, while hello individual VMs are normally accessed using VIP:&lt;port number&gt;.</span></span> <span data-ttu-id="8a582-113">ILPIP tooa 할당 하 여 VM 수 있는 특정 VM에 해당 IP 주소를 사용 하 여 직접 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a582-113">By assigning an ILPIP tooa specific VM, that VM can be accessed directly using that IP address.</span></span>

<span data-ttu-id="8a582-114">Azure에서 클라우드 서비스를 만들 때 해당 DNS A 레코드가 자동으로 만들어집니다 정규화 된 도메인 이름 (FQDN)을 통해 tooallow 액세스 toohello 서비스 hello 실제 VIP를 사용 하는 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a582-114">When you create a cloud service in Azure, corresponding DNS A records are created automatically tooallow access toohello service through a fully qualified domain name (FQDN), instead of using hello actual VIP.</span></span> <span data-ttu-id="8a582-115">허용 액세스 toohello VM 또는 역할 인스턴스에 FQDN으로 hello ILPIP 대신는 ILPIP 대 한 동일한 프로세스에서 발생 하는 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="8a582-115">hello same process happens for an ILPIP, allowing access toohello VM or role instance by FQDN instead of hello ILPIP.</span></span> <span data-ttu-id="8a582-116">예를 들어, 명명 된 클라우드 서비스를 만드는 경우 *contosoadservice*, 라는 웹 역할을 구성 하 고 *contosoweb* 두 개의 인스턴스에 다음 Azure 레지스터 hello hello 인스턴스에 대 한 기록:</span><span class="sxs-lookup"><span data-stu-id="8a582-116">For instance, if you create a cloud service named *contosoadservice*, and you configure a web role named *contosoweb* with two instances, Azure registers hello following A records for hello instances:</span></span>

* <span data-ttu-id="8a582-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="8a582-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span></span>
* <span data-ttu-id="8a582-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="8a582-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span></span> 

> [!NOTE]
> <span data-ttu-id="8a582-119">각 VM 또는 역할 인스턴스에 대해 하나의 ILPIP를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a582-119">You can assign only one ILPIP for each VM or role instance.</span></span> <span data-ttu-id="8a582-120">구독 당 too5 ILPIPs를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a582-120">You can use up too5 ILPIPs per subscription.</span></span> <span data-ttu-id="8a582-121">다중 NIC VM에는 ILPIP가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8a582-121">ILPIPs are not supported for multi-NIC VMs.</span></span>
> 
> 

## <a name="why-would-i-request-an-ilpip"></a><span data-ttu-id="8a582-122">ILPIP를 요청하는 이유</span><span class="sxs-lookup"><span data-stu-id="8a582-122">Why would I request an ILPIP?</span></span>
<span data-ttu-id="8a582-123">Toobe 수 tooconnect tooyour VM 싶거나 역할 인스턴스는 IP 주소에 따라 직접 할당 tooit hello 클라우드를 사용 하는 대신 서비스 VIP:&lt;포트 번호&gt;, VM 또는 역할 인스턴스에 대 한 ILPIP를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a582-123">If you want toobe able tooconnect tooyour VM or role instance by an IP address assigned directly tooit, rather than using hello cloud service VIP:&lt;port number&gt;, request an ILPIP for your VM or your role instance.</span></span>

* <span data-ttu-id="8a582-124">**활성 FTP** -ILPIP tooa VM을 할당 하 여 모든 포트에서 트래픽을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a582-124">**Active FTP** - By assigning an ILPIP tooa VM, it can receive traffic on any port.</span></span> <span data-ttu-id="8a582-125">끝점 VM tooreceive 트래픽이 hello에 대 한 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8a582-125">Endpoints are not required for hello VM tooreceive traffic.</span></span>  <span data-ttu-id="8a582-126">Hello FTP 프로토콜에 대 한 자세한 내용은 [FTP 프로토콜 개요] (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview)를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="8a582-126">See (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview)[FTP Protocol Overview] for details on hello FTP protocol.</span></span>
* <span data-ttu-id="8a582-127">**아웃 바운드 IP** -VM이 hello에서 시작 되는 아웃 바운드 트래픽이 매핑된 toohello hello 소스로 ILPIP 및 hello ILPIP hello VM tooexternal 엔터티를 고유 하 게 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a582-127">**Outbound IP** - Outbound traffic originating from hello VM is mapped toohello ILPIP as hello source and hello ILPIP uniquely identifies hello VM tooexternal entities.</span></span>

> [!NOTE]
> <span data-ttu-id="8a582-128">Hello 지난, ILPIP 주소 참조 tooas 공용 PIP (IP) 주소를 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8a582-128">In hello past, an ILPIP address was referred tooas a public IP (PIP) address.</span></span>
> 

## <a name="manage-an-ilpip-for-a-vm"></a><span data-ttu-id="8a582-129">VM에 대한 ILPIP 관리</span><span class="sxs-lookup"><span data-stu-id="8a582-129">Manage an ILPIP for a VM</span></span>
<span data-ttu-id="8a582-130">작업을 수행 하는 hello를 사용 하면 toocreate, 할당 및 Vm에서 ILPIPs 제거:</span><span class="sxs-lookup"><span data-stu-id="8a582-130">hello following tasks enable you toocreate, assign, and remove ILPIPs from VMs:</span></span>

### <a name="how-toorequest-an-ilpip-during-vm-creation-using-powershell"></a><span data-ttu-id="8a582-131">어떻게 toorequest PowerShell을 사용 하 여 VM 만드는 동안 ILPIP</span><span class="sxs-lookup"><span data-stu-id="8a582-131">How toorequest an ILPIP during VM creation using PowerShell</span></span>
<span data-ttu-id="8a582-132">PowerShell 스크립트 뒤 hello 클라우드 서비스를 만든 *ftp 서비스*, Azure에서 이미지를 검색, 명명 된 VM을 만듭니다 *FTPInstance* hello 검색 이미지를 사용 하 여 집합 hello VM toouse는 ILPIP hello VM toohello 새 서비스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a582-132">hello following PowerShell script creates a cloud service named *FTPService*, retrieves an image from Azure, creates a VM named *FTPInstance* using hello retrieved image, sets hello VM toouse an ILPIP, and adds hello VM toohello new service:</span></span>

```powershell
New-AzureService -ServiceName FTPService -Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"} `
New-AzureVMConfig -Name FTPInstance -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| Set-AzurePublicIP -PublicIPName ftpip | New-AzureVM -ServiceName FTPService -Location "Central US"
```

### <a name="how-tooretrieve-ilpip-information-for-a-vm"></a><span data-ttu-id="8a582-133">어떻게 VM에 대 한 tooretrieve ILPIP 정보</span><span class="sxs-lookup"><span data-stu-id="8a582-133">How tooretrieve ILPIP information for a VM</span></span>
<span data-ttu-id="8a582-134">tooview hello hello 앞의 스크립트를 사용 하 여 만든 VM hello에 대 한 ILPIP 정보 hello 다음 PowerShell 명령을 실행 하 고 hello에 대 한 값이 확인 *PublicIPAddress* 및 *PublicIPName*:</span><span class="sxs-lookup"><span data-stu-id="8a582-134">tooview hello ILPIP information for hello VM created with hello previous script, run hello following PowerShell command and observe hello values for *PublicIPAddress* and *PublicIPName*:</span></span>

```powershell
Get-AzureVM -Name FTPInstance -ServiceName FTPService
```

<span data-ttu-id="8a582-135">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="8a582-135">Expected output:</span></span>
 
    DeploymentName              : FTPService
    Name                        : FTPInstance
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : ReadyRole
    IpAddress                   : 100.74.118.91
    InstanceStateDetails        : 
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : FTPInstance
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : FTPInstance
    AvailabilitySetName         : 
    DNSName                     : http://ftpservice888.cloudapp.net/
    Status                      : ReadyRole
    GuestAgentStatus            :   Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 104.43.142.188
    PublicIPName                : ftpip
    NetworkInterfaces           : {}
    ServiceName                 : FTPService
    OperationDescription        : Get-AzureVM
    OperationId                 : 568d88d2be7c98f4bbb875e4d823718e
    OperationStatus             : OK

### <a name="how-tooremove-an-ilpip-from-a-vm"></a><span data-ttu-id="8a582-136">어떻게 tooremove VM에서 ILPIP</span><span class="sxs-lookup"><span data-stu-id="8a582-136">How tooremove an ILPIP from a VM</span></span>
<span data-ttu-id="8a582-137">tooremove hello ILPIP hello 다음 PowerShell 명령을 실행 하는 hello 이전 스크립트에서는 toohello VM 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8a582-137">tooremove hello ILPIP added toohello VM in hello previous script, run hello following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Remove-AzurePublicIP | Update-AzureVM
```

### <a name="how-tooadd-an-ilpip-tooan-existing-vm"></a><span data-ttu-id="8a582-138">어떻게 tooadd ILPIP tooan 기존 VM</span><span class="sxs-lookup"><span data-stu-id="8a582-138">How tooadd an ILPIP tooan existing VM</span></span>
<span data-ttu-id="8a582-139">tooadd ILPIP toohello 이전, hello 스크립트를 사용 하 여 만든 VM hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a582-139">tooadd an ILPIP toohello VM created using hello script previous, run hello following command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Set-AzurePublicIP -PublicIPName ftpip2 | Update-AzureVM
```

## <a name="manage-an-ilpip-for-a-cloud-services-role-instance"></a><span data-ttu-id="8a582-140">Cloud Services 역할 인스턴스에 대한 ILPIP 관리</span><span class="sxs-lookup"><span data-stu-id="8a582-140">Manage an ILPIP for a Cloud Services role instance</span></span>

<span data-ttu-id="8a582-141">tooadd ILPIP tooa 클라우드 서비스 역할 인스턴스 완료 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a582-141">tooadd an ILPIP tooa Cloud Services role instance, complete hello following steps:</span></span>

1. <span data-ttu-id="8a582-142">Hello의 단계를 hello를 완료 하 여 클라우드 서비스 hello hello.cscfg 파일을 다운로드 [tooConfigure 클라우드 서비스 방법](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) 문서.</span><span class="sxs-lookup"><span data-stu-id="8a582-142">Download hello .cscfg file for hello cloud service by completing hello steps in hello [How tooConfigure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>
2. <span data-ttu-id="8a582-143">Hello를 추가 하 여 업데이트 hello.cscfg 파일 `InstanceAddress` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="8a582-143">Update hello .cscfg file by adding hello `InstanceAddress` element.</span></span> <span data-ttu-id="8a582-144">hello 다음 샘플 추가 라는 ILPIP *MyPublicIP* tooa 역할 인스턴스 라는 *WebRole1*:</span><span class="sxs-lookup"><span data-stu-id="8a582-144">hello following sample adds an ILPIP named *MyPublicIP* tooa role instance named *WebRole1*:</span></span> 

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ILPIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
          <ConfigurationSettings>
        <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
          </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <InstanceAddress roleName="WebRole1">
        <PublicIPs>
          <PublicIP name="MyPublicIP" domainNameLabel="MyPublicIP" />
            </PublicIPs>
          </InstanceAddress>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>
    ```
3. <span data-ttu-id="8a582-145">Hello의 단계를 hello를 완료 하 여 클라우드 서비스 hello hello.cscfg 파일을 업로드 [tooConfigure 클라우드 서비스 방법](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) 문서.</span><span class="sxs-lookup"><span data-stu-id="8a582-145">Upload hello .cscfg file for hello cloud service by completing hello steps in hello [How tooConfigure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a582-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8a582-146">Next steps</span></span>
* <span data-ttu-id="8a582-147">이해 어떻게 [IP 주소 지정](virtual-network-ip-addresses-overview-classic.md) hello 클래식 배포 모델에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a582-147">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in hello classic deployment model.</span></span>
* <span data-ttu-id="8a582-148">[예약된 IP](virtual-networks-reserved-public-ip.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8a582-148">Learn about [Reserved IPs](virtual-networks-reserved-public-ip.md).</span></span>
