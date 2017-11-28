---
title: "클라우드 서비스 tooa aaaConnect 사용자 지정 도메인 컨트롤러 | Microsoft Docs"
description: "자세한 내용은 방법 tooconnect 웹/작업자 역할 tooa 사용자 지정 AD 도메인 PowerShell 및 AD 도메인 확장명을 사용 하 여"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 1e2d7c87-d254-4e7a-a832-67f84411ec95
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 9540190ccf17c03e55159c6c68429eee29e0a558
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-azure-cloud-services-roles-tooa-custom-ad-domain-controller-hosted-in-azure"></a><span data-ttu-id="c2a50-103">Azure 클라우드 서비스 역할 tooa 사용자 지정 Azure에서 호스트 되는 AD 도메인 컨트롤러를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2a50-103">Connecting Azure Cloud Services Roles tooa custom AD Domain Controller hosted in Azure</span></span>
<span data-ttu-id="c2a50-104">먼저 Azure에서 Virtual Network(VNet)를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c2a50-104">We will first set up a Virtual Network (VNet) in Azure.</span></span> <span data-ttu-id="c2a50-105">그런 다음 Active Directory 도메인 컨트롤러 (Azure 가상 컴퓨터에서 호스트 됨) toohello VNet 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2a50-105">We will then add an Active Directory Domain Controller (hosted on an Azure Virtual Machine) toohello VNet.</span></span> <span data-ttu-id="c2a50-106">다음으로, 우리는 추가 기존 클라우드 서비스 역할 toohello 미리 VNet을 만든 다음 toohello 도메인 컨트롤러에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2a50-106">Next, we will add existing cloud service roles toohello pre-created VNet, then connect them toohello Domain Controller.</span></span>

<span data-ttu-id="c2a50-107">시작 하기 전에 몇 가지 고려에서 사항 tookeep의:</span><span class="sxs-lookup"><span data-stu-id="c2a50-107">Before we get started, couple of things tookeep in mind:</span></span>

1. <span data-ttu-id="c2a50-108">이 자습서에서는 PowerShell을 사용 하므로 Azure PowerShell을 설치 하 고 toogo을 준비 했는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2a50-108">This tutorial uses PowerShell, so make sure you have Azure PowerShell installed and ready toogo.</span></span> <span data-ttu-id="c2a50-109">Azure PowerShell 설정을 tooget 도움말 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="c2a50-109">tooget help with setting up Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="c2a50-110">AD 도메인 컨트롤러 및 웹/작업자 역할 인스턴스 toobe hello VNet에에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c2a50-110">Your AD Domain Controller and Web/Worker Role instances need toobe in hello VNet.</span></span>

<span data-ttu-id="c2a50-111">이 단계별 가이드를 따르고 모든 문제를 실행 하는 경우를 남겨 주세요 hello hello 문서의 뒷부분에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2a50-111">Follow this step-by-step guide and if you run into any issues, leave us a comment at hello end of hello article.</span></span> <span data-ttu-id="c2a50-112">주시면 드리겠습니다 tooyou (예, 않습니다 읽은 의견).</span><span class="sxs-lookup"><span data-stu-id="c2a50-112">Someone will get back tooyou (yes, we do read comments).</span></span>

<span data-ttu-id="c2a50-113">hello 네트워크가 hello 클라우드 서비스에서 참조 하는 **클래식 가상 네트워크**합니다.</span><span class="sxs-lookup"><span data-stu-id="c2a50-113">hello network that is referenced by hello cloud service must be a **classic virtual network**.</span></span>

## <a name="create-a-virtual-network"></a><span data-ttu-id="c2a50-114">Virtual Network 만들기</span><span class="sxs-lookup"><span data-stu-id="c2a50-114">Create a Virtual Network</span></span>
<span data-ttu-id="c2a50-115">Hello Azure 포털 또는 PowerShell을 사용 하 여 Azure에서 가상 네트워크를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2a50-115">You can create a Virtual Network in Azure using hello Azure portal or PowerShell.</span></span> <span data-ttu-id="c2a50-116">이 자습서에서는 PowerShell을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c2a50-116">For this tutorial, we will use PowerShell.</span></span> <span data-ttu-id="c2a50-117">사용 하 여 가상 네트워크 toocreate hello Azure 포털에서 참조 [가상 네트워크 만들기](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c2a50-117">toocreate a Virtual Network using hello Azure portal, see [Create Virtual Network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

```powershell
#Create Virtual Network

$vnetStr =
@"<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
    <VirtualNetworkConfiguration>
    <VirtualNetworkSites>
        <VirtualNetworkSite name="[your-vnet-name]" Location="West US">
        <AddressSpace>
            <AddressPrefix>[your-address-prefix]</AddressPrefix>
        </AddressSpace>
        <Subnets>
            <Subnet name="[your-subnet-name]">
            <AddressPrefix>[your-subnet-range]</AddressPrefix>
            </Subnet>
        </Subnets>
        </VirtualNetworkSite>
    </VirtualNetworkSites>
    </VirtualNetworkConfiguration>
</NetworkConfiguration>
"@;

$vnetConfigPath = "<path-to-vnet-config>"
Set-AzureVNetConfig -ConfigurationPath $vnetConfigPath
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="c2a50-118">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="c2a50-118">Create a Virtual Machine</span></span>
<span data-ttu-id="c2a50-119">Hello 가상 네트워크 설정을 마치면 toocreate AD 도메인 컨트롤러가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2a50-119">Once you have completed setting up hello Virtual Network, you will need toocreate an AD Domain Controller.</span></span> <span data-ttu-id="c2a50-120">이 자습서는 Azure 가상 컴퓨터에서 AD 도메인 컨트롤러를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c2a50-120">For this tutorial, we will be setting up an AD Domain Controller on an Azure Virtual Machine.</span></span>

<span data-ttu-id="c2a50-121">toodo이 명령을 수행 하는 hello를 사용 하 여 PowerShell 통해 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c2a50-121">toodo this, create a virtual machine through PowerShell using hello following commands:</span></span>

```powershell
# Initialize variables
# VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.

$vnetname = '<your-vnet-name>'
$subnetname = '<your-subnet-name>'
$vmsvc1 = '<your-hosted-service>'
$vm1 = '<your-vm-name>'
$username = '<your-username>'
$password = '<your-password>'
$affgrp = '<your- affgrp>'

# Create a VM and add it toohello Virtual Network

New-AzureQuickVM -Windows -ServiceName $vmsvc1 -Name $vm1 -ImageName $imgname -AdminUsername $username -Password $password -AffinityGroup $affgrp -SubnetNames $subnetname -VNetName $vnetname
```

## <a name="promote-your-virtual-machine-tooa-domain-controller"></a><span data-ttu-id="c2a50-122">에 가상 컴퓨터 tooa 도메인 컨트롤러 수준 올리기</span><span class="sxs-lookup"><span data-stu-id="c2a50-122">Promote your Virtual Machine tooa Domain Controller</span></span>
<span data-ttu-id="c2a50-123">가상 컴퓨터 tooconfigure hello AD 도메인 컨트롤러로 toolog toohello VM에서에서 필요한 및 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2a50-123">tooconfigure hello Virtual Machine as an AD Domain Controller, you will need toolog in toohello VM and configure it.</span></span>

<span data-ttu-id="c2a50-124">toohello VM에서에서 toolog, PowerShell에서 다음 명령을 사용 하 여 hello 통해 hello RDP 파일을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2a50-124">toolog in toohello VM, you can get hello RDP file through PowerShell, use hello following commands:</span></span>

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

<span data-ttu-id="c2a50-125">Toohello VM에에서 로그인 하면 가상 컴퓨터를 다음 hello 단계별 가이드에서 AD 도메인 컨트롤러에 설정 [어떻게 고객 AD 도메인 컨트롤러 tooset](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c2a50-125">Once you are signed in toohello VM, set up your Virtual Machine as an AD Domain Controller by following hello step-by-step guide on [How tooset up your customer AD Domain Controller](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span></span>

## <a name="add-your-cloud-service-toohello-virtual-network"></a><span data-ttu-id="c2a50-126">가상 네트워크에 클라우드 서비스 toohello 추가</span><span class="sxs-lookup"><span data-stu-id="c2a50-126">Add your Cloud Service toohello Virtual Network</span></span>
<span data-ttu-id="c2a50-127">다음으로, 해야 tooadd에 클라우드 서비스 배포 toohello 새 VNet입니다.</span><span class="sxs-lookup"><span data-stu-id="c2a50-127">Next, you need tooadd your cloud service deployment toohello new VNet.</span></span> <span data-ttu-id="c2a50-128">toodo Visual Studio를 사용 하 여 hello 관련 섹션 tooyour cscfg를 추가 하 여 클라우드 서비스 cscfg 수정이 또는 원하는 편집기를 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2a50-128">toodo this, modify your cloud service cscfg by adding hello relevant sections tooyour cscfg using Visual Studio or hello editor of your choice.</span></span>

```xml
<ServiceConfiguration serviceName="[hosted-service-name]" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="[os-family]" osVersion="*">
    <Role name="[role-name]">
    <Instances count="[number-of-instances]" />
    </Role>
    <NetworkConfiguration>

    <!--optional-->
    <Dns>
        <DnsServers><DnsServer name="[dns-server-name]" IPAddress="[ip-address]" /></DnsServers>
    </Dns>
    <!--optional-->

    <!--VNet settings
        VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.-->
    <VirtualNetworkSite name="[virtual-network-name]" />
    <AddressAssignments>
        <InstanceAddress roleName="[role-name]">
        <Subnets>
            <Subnet name="[subnet-name]" />
        </Subnets>
        </InstanceAddress>
    </AddressAssignments>
    <!--VNet settings-->

    </NetworkConfiguration>
</ServiceConfiguration>
```

<span data-ttu-id="c2a50-129">다음 클라우드 서비스 프로젝트를 빌드하고 tooAzure 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2a50-129">Next build your cloud services project and deploy it tooAzure.</span></span> <span data-ttu-id="c2a50-130">클라우드 서비스 패키지 tooAzure 배포 tooget 도움말 참조 [어떻게 tooCreate 클라우드 서비스 및 배포](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span><span class="sxs-lookup"><span data-stu-id="c2a50-130">tooget help with deploying your cloud services package tooAzure, see [How tooCreate and Deploy a Cloud Service](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span></span>

## <a name="connect-your-webworker-roles-toohello-domain"></a><span data-ttu-id="c2a50-131">웹/작업자 역할 toohello 도메인 연결</span><span class="sxs-lookup"><span data-stu-id="c2a50-131">Connect your web/worker roles toohello domain</span></span>
<span data-ttu-id="c2a50-132">Azure에서 클라우드 서비스 프로젝트 배포 되 면 hello AD 도메인 확장명을 사용 하 여 역할 인스턴스 toohello 사용자 지정 AD 도메인을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2a50-132">Once your cloud service project is deployed on Azure, connect your role instances toohello custom AD domain using hello AD Domain Extension.</span></span> <span data-ttu-id="c2a50-133">tooadd hello AD 도메인 확장명 tooyour 기존 클라우드 서비스 배포 및 조인 hello 사용자 지정 도메인을 hello 다음 powershell에서 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2a50-133">tooadd hello AD Domain Extension tooyour existing cloud services deployment and join hello custom domain, execute hello following commands in PowerShell:</span></span>

```powershell
# Initialize domain variables

$domain = '<your-domain-name>'
$dmuser = '$domain\<your-username>'
$dmpswd = '<your-domain-password>'
$dmspwd = ConvertTo-SecureString $dmpswd -AsPlainText -Force
$dmcred = New-Object System.Management.Automation.PSCredential ($dmuser, $dmspwd)

# Add AD Domain Extension toohello cloud service roles

Set-AzureServiceADDomainExtension -Service <your-cloud-service-hosted-service-name> -Role <your-role-name> -Slot <staging-or-production> -DomainName $domain -Credential $dmcred -JoinOption 35
```

<span data-ttu-id="c2a50-134">지금까지 전반적인 내용을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="c2a50-134">And that's it.</span></span>

<span data-ttu-id="c2a50-135">클라우드 서비스에 조인된 tooyour 사용자 지정 도메인 컨트롤러 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2a50-135">Your cloud services should be joined tooyour custom domain controller.</span></span> <span data-ttu-id="c2a50-136">사용할 수 있는 다른 옵션에 대 한 자세한 hello toolearn 원하는 어떻게 tooconfigure AD 도메인 확장명을 사용 하 여 hello PowerShell 도움말입니다.</span><span class="sxs-lookup"><span data-stu-id="c2a50-136">If you would like toolearn more about hello different options available for how tooconfigure AD Domain Extension, use hello PowerShell help.</span></span> <span data-ttu-id="c2a50-137">다음은 몇 가지 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="c2a50-137">A couple of examples follow:</span></span>

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
