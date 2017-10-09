---
title: "aaaMove VM (클래식) 또는 클라우드 서비스 역할 인스턴스 tooa 다른 서브넷-Azure PowerShell | Microsoft Docs"
description: "자세한 내용은 방법 toomove (클래식) Vm 클라우드 서비스 역할 인스턴스 tooa PowerShell을 사용 하는 다른 서브넷 및 합니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: de4135c7-dc5b-4ffa-84cc-1b8364b7b427
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c8d2de56f42a91be4a665414ea9641ffd46588fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-vm-classic-or-cloud-services-role-instance-tooa-different-subnet-using-powershell"></a>VM (클래식) 또는 클라우드 서비스 역할 인스턴스 tooa 다른 서브넷 PowerShell을 사용 하 여 이동
Hello에 PowerShell toomove tooanother 한 서브넷에서에서 Vm (클래식)을 사용할 수 있습니다 동일한 가상 네트워크 (VNet). PowerShell을 사용 하는 대신 hello CSCFG 파일을 편집 하 여 역할 인스턴스를 이동할 수 있습니다.

> [!NOTE]
> 이 문서에서는 hello 클래식 배포 모델을 통해 toomove Vm을 배포 하는 방법을 설명 합니다.
> 
> 

Vm tooanother 서브넷을 이동 하는 이유 Hello 기존 서브넷 너무 작습니다 인해 확장할 수 없는 경우 서브넷 마이그레이션 유용 합니다. tooexisting 해당 서브넷에 Vm을 실행 합니다. 이 경우 새, 더 큰 서브넷을 만들고 hello Vm toohello 새 서브넷을 마이그레이션할 수 있습니다 다음 마이그레이션이 완료 된 후에 hello 이전 빈 서브넷을 삭제할 수 있습니다.

## <a name="how-toomove-a-vm-tooanother-subnet"></a>어떻게 toomove VM tooanother 서브넷
toomove VM 템플릿으로 아래 hello 예제를 사용 하 여 hello Set-azuresubnet PowerShell cmdlet을 실행 합니다. Hello 아래 예제에서는 이동 TestVM 서브넷에서 tooSubnet 2입니다. 있는지 tooedit hello 예제 tooreflect 환경 이어야 합니다. 하는 절차의 일부로 hello Update-azurevm cmdlet을 실행할 때마다 다시 시작 됩니다 VM hello 업데이트 프로세스의 일부로 참고 합니다.

    Get-AzureVM –ServiceName TestVMCloud –Name TestVM `
    | Set-AzureSubnet –SubnetNames Subnet-2 `
    | Update-AzureVM

VM에 대 한 고정 내부 개인 ip 주소를 지정한 경우 tooclear 해당 설정을 hello VM tooa 새 서브넷을 이동할 수 있습니다. 이 경우 다음 hello를 사용 합니다.

    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM
    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Set-AzureSubnet -SubnetNames Subnet-2 `
    | Update-AzureVM

## <a name="toomove-a-role-instance-tooanother-subnet"></a>역할 인스턴스 tooanother 서브넷 toomove
역할 인스턴스를 toomove hello CSCFG 파일을 편집 합니다. Hello 아래 예제에서는 이동 "role0"을 기존 가상 네트워크의 *VNETName* 서브넷에서 너무*서브넷 2*합니다. Hello 역할 인스턴스가 이미 배포 되었기 때문에 변경 하기만 하면 hello 서브넷 이름이 e t-2 = 합니다. 있는지 tooedit hello 예제 tooreflect 환경 이어야 합니다.

    <NetworkConfiguration>
        <VirtualNetworkSite name="VNETName" />
        <AddressAssignments>
           <InstanceAddress roleName="Role0">
                <Subnets><Subnet name="Subnet-2" /></Subnets>
           </InstanceAddress>
        </AddressAssignments>
    </NetworkConfiguration> 
