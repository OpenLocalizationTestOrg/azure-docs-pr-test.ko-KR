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
# <a name="how-tooset-a-static-internal-private-ip-address-using-powershell-classic"></a>PowerShell (클래식)를 사용 하 여 고정 내부 개인 IP tooset을 처리 하는 방법
대부분의 경우에서 가상 컴퓨터에 대 한 고정 내부 IP 주소 toospecify가 필요 하지는 않습니다. 가상 네트워크의 VM은 사용자가 지정한 범위의 내부 IP 주소를 자동으로 받습니다. 그러나 특정한 상황에서는 특정 VM에 고정 IP 주소를 지정하는 것이 적합한 경우도 있습니다. 예를 들어 VM은 진행 중인 toorun DNS 또는 도메인 컨트롤러가 될 경우. 고정 내부 IP 주소에 hello VM 중지/프로 비전 해제 상태 통한 경우에 유지 됩니다. 

> [!IMPORTANT]
> Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello를 사용 하는 것이 좋습니다 [리소스 관리자 배포 모델](virtual-networks-static-private-ip-arm-ps.md)합니다.
> 
> 

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a>어떻게 tooverify 특정 IP 주소를 사용할 수 있는 경우
tooverify 경우 hello IP 주소 *10.0.0.7* 라는 vnet에 사용할 수 *TestVnet*, hello 다음 PowerShell 명령을 실행 하 고 확인에 대 한 hello 값 *IsAvailable*:

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> Tootest hello 명령을 위에 안전한 환경에서 원하는 경우 hello 지침에 따라 [가상 네트워크 (클래식)를 만들고](virtual-networks-create-vnet-classic-pportal.md) toocreate 라는 vnet *TestVnet* hello를 사용 하 여 확인  *10.0.0.0/8* 주소 공간입니다.
> 
> 

## <a name="how-toospecify-a-static-internal-ip-when-creating-a-vm"></a>어떻게 toospecify VM을 만들 때 고정 내부 IP
hello 아래의 PowerShell 스크립트 라는 새 클라우드 서비스를 만듭니다. *TestService*다음 Azure에서 이미지를 검색 합니다 V 만듭니다 *TestVM* hello hello 검색 이미지를 사용 하는 새 클라우드 서비스 집합 이라는 서브넷에 VM toobe hello *서브넷-1*, 설정 및 *10.0.0.7* hello VM에 대 한 정적 내부 ip:

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-tooretrieve-static-internal-ip-information-for-a-vm"></a>어떻게 tooretrieve 정적 내부 IP에 대 한 정보는 VM
tooview hello 고정 내부 IP 정보 hello에 대 한 위의 hello 스크립트를 사용 하 여 만든 VM hello 다음 PowerShell 명령을 실행 하 고 hello에 대 한 값이 확인 *IpAddress*:

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

## <a name="how-tooremove-a-static-internal-ip-from-a-vm"></a>어떻게 tooremove VM에서 고정 내부 ip 주소
tooremove hello 고정 내부 IP hello 다음 PowerShell 명령을 실행 toohello VM 위의 hello 스크립트에 추가 합니다.

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-tooadd-a-static-internal-ip-tooan-existing-vm"></a>어떻게 tooadd 정적 내부 IP tooan 기존 VM
tooadd 정적 내부 IP toohello 사용 하 여 만든 녀석 위의 hello 스크립트 명령을 다음 VM:

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a>다음 단계
[예약된 IP](virtual-networks-reserved-public-ip.md)

[인스턴스 수준 공용 IP(ILPIP)](virtual-networks-instance-level-public-ip.md)

[예약된 IP REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx)

