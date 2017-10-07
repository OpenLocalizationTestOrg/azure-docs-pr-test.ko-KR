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
# <a name="connecting-azure-cloud-services-roles-tooa-custom-ad-domain-controller-hosted-in-azure"></a>Azure 클라우드 서비스 역할 tooa 사용자 지정 Azure에서 호스트 되는 AD 도메인 컨트롤러를 연결 합니다.
먼저 Azure에서 Virtual Network(VNet)를 설정합니다. 그런 다음 Active Directory 도메인 컨트롤러 (Azure 가상 컴퓨터에서 호스트 됨) toohello VNet 추가 합니다. 다음으로, 우리는 추가 기존 클라우드 서비스 역할 toohello 미리 VNet을 만든 다음 toohello 도메인 컨트롤러에 연결 합니다.

시작 하기 전에 몇 가지 고려에서 사항 tookeep의:

1. 이 자습서에서는 PowerShell을 사용 하므로 Azure PowerShell을 설치 하 고 toogo을 준비 했는지를 확인 합니다. Azure PowerShell 설정을 tooget 도움말 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.
2. AD 도메인 컨트롤러 및 웹/작업자 역할 인스턴스 toobe hello VNet에에서 필요합니다.

이 단계별 가이드를 따르고 모든 문제를 실행 하는 경우를 남겨 주세요 hello hello 문서의 뒷부분에서 설명 합니다. 주시면 드리겠습니다 tooyou (예, 않습니다 읽은 의견).

hello 네트워크가 hello 클라우드 서비스에서 참조 하는 **클래식 가상 네트워크**합니다.

## <a name="create-a-virtual-network"></a>Virtual Network 만들기
Hello Azure 포털 또는 PowerShell을 사용 하 여 Azure에서 가상 네트워크를 만들 수 있습니다. 이 자습서에서는 PowerShell을 사용합니다. 사용 하 여 가상 네트워크 toocreate hello Azure 포털에서 참조 [가상 네트워크 만들기](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)합니다.

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

## <a name="create-a-virtual-machine"></a>가상 컴퓨터 만들기
Hello 가상 네트워크 설정을 마치면 toocreate AD 도메인 컨트롤러가 필요 합니다. 이 자습서는 Azure 가상 컴퓨터에서 AD 도메인 컨트롤러를 설정합니다.

toodo이 명령을 수행 하는 hello를 사용 하 여 PowerShell 통해 가상 컴퓨터를 만듭니다.

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

## <a name="promote-your-virtual-machine-tooa-domain-controller"></a>에 가상 컴퓨터 tooa 도메인 컨트롤러 수준 올리기
가상 컴퓨터 tooconfigure hello AD 도메인 컨트롤러로 toolog toohello VM에서에서 필요한 및 구성 합니다.

toohello VM에서에서 toolog, PowerShell에서 다음 명령을 사용 하 여 hello 통해 hello RDP 파일을 가져올 수 있습니다.

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

Toohello VM에에서 로그인 하면 가상 컴퓨터를 다음 hello 단계별 가이드에서 AD 도메인 컨트롤러에 설정 [어떻게 고객 AD 도메인 컨트롤러 tooset](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx)합니다.

## <a name="add-your-cloud-service-toohello-virtual-network"></a>가상 네트워크에 클라우드 서비스 toohello 추가
다음으로, 해야 tooadd에 클라우드 서비스 배포 toohello 새 VNet입니다. toodo Visual Studio를 사용 하 여 hello 관련 섹션 tooyour cscfg를 추가 하 여 클라우드 서비스 cscfg 수정이 또는 원하는 편집기를 환영 합니다.

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

다음 클라우드 서비스 프로젝트를 빌드하고 tooAzure 배포 합니다. 클라우드 서비스 패키지 tooAzure 배포 tooget 도움말 참조 [어떻게 tooCreate 클라우드 서비스 및 배포](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)

## <a name="connect-your-webworker-roles-toohello-domain"></a>웹/작업자 역할 toohello 도메인 연결
Azure에서 클라우드 서비스 프로젝트 배포 되 면 hello AD 도메인 확장명을 사용 하 여 역할 인스턴스 toohello 사용자 지정 AD 도메인을 연결 합니다. tooadd hello AD 도메인 확장명 tooyour 기존 클라우드 서비스 배포 및 조인 hello 사용자 지정 도메인을 hello 다음 powershell에서 명령을 실행 합니다.

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

지금까지 전반적인 내용을 알아보았습니다.

클라우드 서비스에 조인된 tooyour 사용자 지정 도메인 컨트롤러 여야 합니다. 사용할 수 있는 다른 옵션에 대 한 자세한 hello toolearn 원하는 어떻게 tooconfigure AD 도메인 확장명을 사용 하 여 hello PowerShell 도움말입니다. 다음은 몇 가지 예제입니다.

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
