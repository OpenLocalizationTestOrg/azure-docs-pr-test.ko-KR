---
title: "여러 Nic-Azure PowerShell을 사용 하 여 VM (클래식) aaaCreate | Microsoft Docs"
description: "자세한 내용은 방법 toocreate PowerShell을 사용 하 여 여러 Nic 사용 하 여 VM (클래식)."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6e50f39a-2497-4845-a5d4-7332dbc203c5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 90c967929bb418042c3fb7079e0f69246faac53c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a>PowerShell을 사용하여 다중 NIC이 있는 VM(클래식) 만들기

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

Azure에서 가상 컴퓨터 (Vm)를 만들고 Vm의 여러 네트워크 인터페이스 (Nic) tooeach 첨부할 수 있습니다. 여러 NIC를 사용하면 NIC 간에 트래픽 유형을 분리할 수 있습니다. 예를 들어 toohello 인터넷에 연결 되어 있지 내부 리소스와만 통신 다른 동안 NIC 인터넷 hello와 통신할 수 있는 하나. 여러 Nic에 걸쳐 hello 기능 tooseparate 네트워크 트래픽을 응용 프로그램을 배달 및 WAN 최적화 솔루션 등에 많은 네트워크 가상 어플라이언스를 필요 합니다.

> [!IMPORTANT]
> Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. 자세한 내용은 방법 tooperform hello를 사용 하 여 이러한 단계 [리소스 관리자 배포 모델](virtual-network-deploy-multinic-arm-ps.md)합니다.

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

hello 다음 단계 사용 하 여 명명 된 리소스 그룹 *IaaSStory* hello 웹 서버 및 리소스 그룹에 대 한 명명 된 *IaaSStory 백 엔드* hello DB 서버에 대 한 합니다.

## <a name="prerequisites"></a>필수 조건

Hello DB 서버를 만들려면 먼저 toocreate hello *IaaSStory* 이 시나리오에 대 한 모든 hello 필요한 리소스의 리소스 그룹입니다. 이러한 리소스를 전체 hello 수행 하는 단계는 toocreate 합니다. Hello hello 단계를 수행 하 여 가상 네트워크 만들기 [가상 네트워크 만들기](virtual-networks-create-vnet-classic-netcfg-ps.md) 문서.

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a>Hello 백 엔드 Vm 만들기
hello 백 엔드 Vm hello 생성의 다음 리소스는 hello에 따라 달라 집니다.

* **백 엔드 서브넷**. hello 데이터베이스 서버는 별도 서브넷 toosegregate 트래픽의 일부가 됩니다. 아래의 hello 스크립트 라는 vnet에이 서브넷 tooexist 리라 전망 *WTestVnet*합니다.
* **데이터 디스크용 저장소 계정**. 성능 향상을 위해 hello 데이터베이스 서버에 데이터 디스크 hello 프리미엄 저장소 계정을 사용 해야 하는 반도체 드라이브 (SSD) 기술을 사용 합니다. 있는지 hello toosupport 프리미엄 저장소를 배포 하는 Azure 위치를 확인 합니다.
* **가용성 집합**. 모든 데이터베이스 서버를 추가할 tooa 단일 가용성 집합, tooensure hello Vm 중 하나 이상이 실행 되 고 유지 관리 합니다.

### <a name="step-1---start-your-script"></a>1단계 - 스크립트 시작
Hello 사용 되는 전체 PowerShell 스크립트를 다운로드할 수 있습니다 [여기](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1)합니다. 사용자 환경에서 toochange hello 스크립트 toowork 아래 hello 단계를 수행 합니다.

1. Hello에 위의 배포 된 기존 리소스 그룹에 따라 hello 변수 값 변경 [필수 구성 요소](#Prerequisites)합니다.

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. Hello 값을 변경 hello 값을 기반으로 hello 변수 원하는 toouse 백 엔드 배포에 대 한 합니다.

    ```powershell
    $backendCSName         = "IaaSStory-Backend"
    $prmStorageAccountName = "iaasstoryprmstorage"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $diskSize              = 127
    $vmNamePrefix          = "DB"
    $dataDiskSuffix        = "datadisk"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a>2단계 - VM에 필요한 리소스 만들기
모든 Vm에 대 한 hello 데이터 디스크에 대 한 새 클라우드 서비스와 저장소 계정 toocreate가 필요 합니다. 또한 해야 toospecify 이미지 및 로컬 관리자 계정을 hello Vm에 대 한 합니다. 이러한 리소스를 완료 하는 toocreate hello 다음 단계:

1. 새 클라우드 서비스 만들기

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. 새 프리미엄 저장소 계정 만들기

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. 구독에 대 한 현재 저장소 계정을 hello로 위에서 만든 집합 hello 저장소 계정입니다.

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. Hello VM에 대 한 이미지를 선택 합니다.

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. Hello 로컬 관리자 계정 자격 증명을 설정 합니다.

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a>3단계: VM 만들기
처럼 많은 Vm을 하 고 만들 때 hello 필요한 Nic 및 Vm hello 루프 내 루프 toocreate toouse가 필요 합니다. toocreate hello Nic Vm에 단계를 수행 하는 hello를 실행 합니다.

1. 시작 된 `for` 루프 toorepeat hello 명령을 toocreate VM 한 두 개의 nic가 필요에 따라 여러 번의 hello hello 값에 기반 `$numberOfVMs` 변수입니다.

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. 만들기는 `VMConfig` hello 이미지, 크기 및 가용성 hello VM에 대 한 집합을 지정 하는 개체입니다.

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. Windows VM으로 hello VM을 프로 비전 합니다.

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. Hello 기본 NIC 설정 하 고 고정 IP 주소를 할당 합니다.

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. 각 VM에 두 번째 NIC를 추가합니다.

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. 각 VM에 대 한 toodata 디스크를 만듭니다.

    ```powershell
    $dataDisk1Name = $vmName + "-" + $dataDiskSuffix + "-1"    
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk1Name `
    -LUN 0

    $dataDisk2Name = $vmName + "-" + $dataDiskSuffix + "-2"   
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk2Name `
    -LUN 1
    ```

7. 각 VM 및 종료 hello 루프를 만듭니다.

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-hello-script"></a>4 단계-실행 hello 스크립트
다운로드 하 고 변경 했으므로 hello 스크립트 toocreate hello 백 엔드 데이터베이스 여러 Nic 포함 하는 Vm을 스크립트 그 아니다를 요구 사항에 기반 합니다.

1. 스크립트를 저장 하 고 hello에서 실행 **PowerShell** 명령 프롬프트 또는 **PowerShell ISE**합니다. 아래와 같이 hello 초기 출력에 나타납니다.

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. 필요한 자격 증명 프롬프트가 hello 및 클릭에서 hello 정보를 채울 **확인**합니다. 아래 hello 출력 반환 됩니다.

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
