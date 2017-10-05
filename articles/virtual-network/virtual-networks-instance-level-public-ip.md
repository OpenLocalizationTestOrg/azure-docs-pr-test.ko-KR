---
title: "Azure 인스턴스 수준 공용 IP(클래식) 주소 | Microsoft Docs"
description: "ILPIP(인스턴스 수준 공용 IP) 주소 및 PowerShell을 사용하여 이를 관리하는 방법을 알아봅니다."
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
ms.openlocfilehash: 773043f2841ec7539b0d49357dec6bcb9f4f78a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="instance-level-public-ip-classic-overview"></a><span data-ttu-id="e62da-103">인스턴스 수준 공용 Ip(클래식) 개요</span><span class="sxs-lookup"><span data-stu-id="e62da-103">Instance level public IP (Classic) overview</span></span>
<span data-ttu-id="e62da-104">ILPIP(인스턴스 수준 공용 IP)는 해당 VM 또는 역할 인스턴스가 상주하는 클라우드 서비스가 아닌 VM 또는 Cloud Services 역할 인스턴스에 직접 할당할 수 있는 공용 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-104">An instance level public IP (ILPIP) is a public IP address that you can assign directly to a VM or Cloud Services role instance, rather than to the cloud service that your VM or role instance reside in.</span></span> <span data-ttu-id="e62da-105">ILPIP는 클라우드 서비스에 할당된 VIP(가상 IP)의 위치를 차지하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-105">An ILPIP doesn’t take the place of the virtual IP (VIP) that is assigned to your cloud service.</span></span> <span data-ttu-id="e62da-106">VM 또는 역할 인스턴스에 직접 연결을 사용할 수 있는 추가 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-106">Rather, it’s an additional IP address that you can use to connect directly to your VM or role instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e62da-107">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="e62da-108">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="e62da-109">Resource Manager를 통해 VM을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-109">Microsoft recommends creating VMs through Resource Manager.</span></span> <span data-ttu-id="e62da-110">Azure에서 [IP 주소](virtual-network-ip-addresses-overview-classic.md) 가 어떻게 작동하는지 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-110">Make sure you understand how [IP addresses](virtual-network-ip-addresses-overview-classic.md) work in Azure.</span></span>

![ILPIP 및 VIP 간의 차이](./media/virtual-networks-instance-level-public-ip/Figure1.png)

<span data-ttu-id="e62da-112">그림 1에 표시된 것과 같이, 클라우드 서비스는 VIP를 사용하여 액세스하지만 개별 VM은 보통 VIP:&lt;포트 번호&gt;를 사용하여 액세스됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-112">As shown in Figure 1, the cloud service is accessed using a VIP, while the individual VMs are normally accessed using VIP:&lt;port number&gt;.</span></span> <span data-ttu-id="e62da-113">특정 VM에 ILPIP를 할당하면 해당 VM은 해당 IP 주소를 사용하여 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-113">By assigning an ILPIP to a specific VM, that VM can be accessed directly using that IP address.</span></span>

<span data-ttu-id="e62da-114">Azure에서 클라우드 서비스를 만들면 해당 DNS A 레코드가 자동으로 만들어져, 실제 VIP를 사용하지 않고 정규화된 도메인 이름(FQDN)을 통해 서비스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-114">When you create a cloud service in Azure, corresponding DNS A records are created automatically to allow access to the service through a fully qualified domain name (FQDN), instead of using the actual VIP.</span></span> <span data-ttu-id="e62da-115">동일한 프로세스가 ILPIP에 대해 발생하며 ILPIP 대신 FQDN으로 VM 또는 역할 인스턴스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-115">The same process happens for an ILPIP, allowing access to the VM or role instance by FQDN instead of the ILPIP.</span></span> <span data-ttu-id="e62da-116">예를 들어, *contosoadservice*라는 클라우드 서비스를 만들고 두 인스턴스가 있는 *contosoweb*이라는 웹 역할을 구성한 경우, Azure는 인스턴스에 대해 다음 A 레코드를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-116">For instance, if you create a cloud service named *contosoadservice*, and you configure a web role named *contosoweb* with two instances, Azure registers the following A records for the instances:</span></span>

* <span data-ttu-id="e62da-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="e62da-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span></span>
* <span data-ttu-id="e62da-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="e62da-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span></span> 

> [!NOTE]
> <span data-ttu-id="e62da-119">각 VM 또는 역할 인스턴스에 대해 하나의 ILPIP를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-119">You can assign only one ILPIP for each VM or role instance.</span></span> <span data-ttu-id="e62da-120">구독당 최대 5개의 ILPIP를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-120">You can use up to 5 ILPIPs per subscription.</span></span> <span data-ttu-id="e62da-121">다중 NIC VM에는 ILPIP가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-121">ILPIPs are not supported for multi-NIC VMs.</span></span>
> 
> 

## <a name="why-would-i-request-an-ilpip"></a><span data-ttu-id="e62da-122">ILPIP를 요청하는 이유</span><span class="sxs-lookup"><span data-stu-id="e62da-122">Why would I request an ILPIP?</span></span>
<span data-ttu-id="e62da-123">클라우드 서비스 VIP:&lt;포트 번호&gt;를 사용하지 않고 직접 할당된 IP 주소로 VM 또는 역할 인스턴스에 연결할 수 있게 하려면 VM 또는 역할 인스턴스에 대한 ILPIP를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-123">If you want to be able to connect to your VM or role instance by an IP address assigned directly to it, rather than using the cloud service VIP:&lt;port number&gt;, request an ILPIP for your VM or your role instance.</span></span>

* <span data-ttu-id="e62da-124">**활성 FTP** - VM에 ILPIP를 할당하면 어떤 포트에서도 트래픽을 수신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-124">**Active FTP** - By assigning an ILPIP to a VM, it can receive traffic on any port.</span></span> <span data-ttu-id="e62da-125">끝점이 없어도 VM에서 트래픽을 수신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-125">Endpoints are not required for the VM to receive traffic.</span></span>  <span data-ttu-id="e62da-126">FTP 프로토콜에 대한 자세한 내용은 (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview)[FTP Protocol Overview] 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e62da-126">See (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview)[FTP Protocol Overview] for details on the FTP protocol.</span></span>
* <span data-ttu-id="e62da-127">**아웃바운드 IP** - VM에서 발생하는 아웃바운드 트래픽은 원본으로 ILPIP에 매핑되며 ILPIP는 외부 엔터티에 대한 VM을 고유하게 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-127">**Outbound IP** - Outbound traffic originating from the VM is mapped to the ILPIP as the source and the ILPIP uniquely identifies the VM to external entities.</span></span>

> [!NOTE]
> <span data-ttu-id="e62da-128">과거에는 ILPIP 주소를 PIP(공용 IP) 주소라고 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-128">In the past, an ILPIP address was referred to as a public IP (PIP) address.</span></span>
> 

## <a name="manage-an-ilpip-for-a-vm"></a><span data-ttu-id="e62da-129">VM에 대한 ILPIP 관리</span><span class="sxs-lookup"><span data-stu-id="e62da-129">Manage an ILPIP for a VM</span></span>
<span data-ttu-id="e62da-130">다음 작업을 통해 VM에서 ILPIP를 생성, 할당 및 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-130">The following tasks enable you to create, assign, and remove ILPIPs from VMs:</span></span>

### <a name="how-to-request-an-ilpip-during-vm-creation-using-powershell"></a><span data-ttu-id="e62da-131">PowerShell을 사용하여 VM 생성 중 ILPIP를 요청하는 방법</span><span class="sxs-lookup"><span data-stu-id="e62da-131">How to request an ILPIP during VM creation using PowerShell</span></span>
<span data-ttu-id="e62da-132">다음 PowerShell 스크립트는 *FTPService*라는 클라우드 서비스를 만들고, Azure에서 이미지를 검색하고, 검색된 이미지를 사용하여 *FTPInstance*라는 VM을 만들고, ILPIP를 사용하도록 VM을 설정하고, VM을 새 서비스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-132">The following PowerShell script creates a cloud service named *FTPService*, retrieves an image from Azure, creates a VM named *FTPInstance* using the retrieved image, sets the VM to use an ILPIP, and adds the VM to the new service:</span></span>

```powershell
New-AzureService -ServiceName FTPService -Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"} `
New-AzureVMConfig -Name FTPInstance -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| Set-AzurePublicIP -PublicIPName ftpip | New-AzureVM -ServiceName FTPService -Location "Central US"
```

### <a name="how-to-retrieve-ilpip-information-for-a-vm"></a><span data-ttu-id="e62da-133">VM에 대한 ILPIP 정보를 검색하는 방법</span><span class="sxs-lookup"><span data-stu-id="e62da-133">How to retrieve ILPIP information for a VM</span></span>
<span data-ttu-id="e62da-134">위의 스크립트를 사용하여 만든 VM에 대한 ILPIP 정보를 보려면, 다음 PowerShell 명령을 실행하고 *PublicIPAddress* 및 *PublicIPName*의 값을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-134">To view the ILPIP information for the VM created with the previous script, run the following PowerShell command and observe the values for *PublicIPAddress* and *PublicIPName*:</span></span>

```powershell
Get-AzureVM -Name FTPInstance -ServiceName FTPService
```

<span data-ttu-id="e62da-135">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="e62da-135">Expected output:</span></span>
 
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

### <a name="how-to-remove-an-ilpip-from-a-vm"></a><span data-ttu-id="e62da-136">VM에서 ILPIP를 제거하는 방법</span><span class="sxs-lookup"><span data-stu-id="e62da-136">How to remove an ILPIP from a VM</span></span>
<span data-ttu-id="e62da-137">위의 스크립트에서 VM에 추가된 ILPIP를 제거하려면 다음 PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-137">To remove the ILPIP added to the VM in the previous script, run the following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Remove-AzurePublicIP | Update-AzureVM
```

### <a name="how-to-add-an-ilpip-to-an-existing-vm"></a><span data-ttu-id="e62da-138">기존 VM에 ILPIP를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="e62da-138">How to add an ILPIP to an existing VM</span></span>
<span data-ttu-id="e62da-139">위의 스크립트를 사용하여 만든 VM에 ILPIP를 추가하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-139">To add an ILPIP to the VM created using the script previous, run the following command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Set-AzurePublicIP -PublicIPName ftpip2 | Update-AzureVM
```

## <a name="manage-an-ilpip-for-a-cloud-services-role-instance"></a><span data-ttu-id="e62da-140">Cloud Services 역할 인스턴스에 대한 ILPIP 관리</span><span class="sxs-lookup"><span data-stu-id="e62da-140">Manage an ILPIP for a Cloud Services role instance</span></span>

<span data-ttu-id="e62da-141">Cloud Services 역할 인스턴스에 ILPIP를 추가하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-141">To add an ILPIP to a Cloud Services role instance, complete the following steps:</span></span>

1. <span data-ttu-id="e62da-142">[Cloud Services를 구성하는 방법](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) 문서의 단계를 완료하여 클라우드 서비스에 대한 .cscfg 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-142">Download the .cscfg file for the cloud service by completing the steps in the [How to Configure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>
2. <span data-ttu-id="e62da-143">`InstanceAddress` 요소를 추가하여 .cscfg 파일을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-143">Update the .cscfg file by adding the `InstanceAddress` element.</span></span> <span data-ttu-id="e62da-144">다음 샘플에서는 *WebRole1* 역할 인스턴스에 *MyPublicIP*라는 ILPIP를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-144">The following sample adds an ILPIP named *MyPublicIP* to a role instance named *WebRole1*:</span></span> 

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
3. <span data-ttu-id="e62da-145">[Cloud Services를 구성하는 방법](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) 문서의 단계를 완료하여 클라우드 서비스에 대한 .cscfg 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-145">Upload the .cscfg file for the cloud service by completing the steps in the [How to Configure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e62da-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e62da-146">Next steps</span></span>
* <span data-ttu-id="e62da-147">클래식 배포 모델에서 [IP 주소 지정](virtual-network-ip-addresses-overview-classic.md) 이 어떻게 작동하는지 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-147">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in the classic deployment model.</span></span>
* <span data-ttu-id="e62da-148">[예약된 IP](virtual-networks-reserved-public-ip.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e62da-148">Learn about [Reserved IPs](virtual-networks-reserved-public-ip.md).</span></span>
