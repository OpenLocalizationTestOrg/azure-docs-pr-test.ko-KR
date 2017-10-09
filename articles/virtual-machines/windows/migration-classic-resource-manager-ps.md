---
title: "관리자 powershell aaaMigrate tooResource | Microsoft Docs"
description: "이 문서에서는 안내 hello IaaS 리소스 (Vm) 가상 컴퓨터, 가상 네트워크 (Vnet) 및 저장소 계정과 같은 플랫폼에서 지 원하는 마이그레이션 클래식 tooAzure 리소스 관리자 (ARM)에서 Azure PowerShell 명령을 사용 하 여"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2b3dff9b-2e99-4556-acc5-d75ef234af9c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: b5b2987da292f1c241be71a354b0c2e1a96a07c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-powershell"></a>Azure PowerShell을 사용 하 여 IaaS 리소스 클래식 tooAzure 리소스 관리자에서 마이그레이션
이러한 단계에 Azure PowerShell toouse toomigrate 인프라 hello 클래식 배포 모델 toohello Azure 리소스 관리자 배포 모델에서 서비스 (IaaS) 리소스 그룹으로 명령 하는 방법을 보여 줍니다.

원하는 경우 마이그레이션할 수도 있습니다 리소스 hello를 사용 하 여 [Azure 명령줄 인터페이스 (Azure CLI)](../linux/migration-classic-resource-manager-cli.md)합니다.

* 지원 되는 마이그레이션 시나리오에 대 한 배경, 참조 [클래식 tooAzure 리소스 관리자에서에서 IaaS 리소스의 플랫폼에서 지 원하는 마이그레이션](migration-classic-resource-manager-overview.md)합니다.
* 자세한 지침 및 마이그레이션 연습에 대 한 참조 [클래식 tooAzure 리소스 관리자에서에서 마이그레이션 플랫폼 지원에 기술 심층 분석](migration-classic-resource-manager-deep-dive.md)합니다.
* [가장 일반적인 마이그레이션 오류 검토](migration-classic-resource-manager-errors.md)

<br>
다음 단계는 toobe 마이그레이션 프로세스 중에 실행 해야 하는 순서도 tooidentify hello 순서는

![Hello 마이그레이션 단계를 보여 주는 스크린샷](media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-plan-for-migration"></a>1단계: 마이그레이션 계획
클래식 tooResource 관리자에서에서 IaaS 리소스를 마이그레이션하기를 평가할 때 권장 되는 몇 가지 모범 사례는 다음과 같습니다.

* Hello 자세히 읽고 [지원 하 고 기능 및 구성을 지원 되지 않는](migration-classic-resource-manager-overview.md)합니다. 지원 되지 않는 구성 또는 기능을 사용 하는 가상 컴퓨터를 설정한 경우에 발표 hello 구성/기능 지원 toobe 나올 때까지 기다리는 것이 좋습니다. 또는, 요구에 적합 한, 해당 기능을 제거 하거나 해당 구성 tooenable 마이그레이션을 밖으로 이동 합니다.
* 현재 인프라 및 응용 프로그램을 배포 하는 스크립트를 자동화 하는 경우 마이그레이션에 대 한 이러한 스크립트를 사용 하 여 toocreate 유사한 테스트 설치 프로그램을 시도 하십시오. Hello Azure 포털을 사용 하 여 샘플 환경, 설정할 수 있습니다.

> [!IMPORTANT]
> 응용 프로그램 게이트웨이 클래식 tooResource 관리자에서에서 마이그레이션에 대 한 현재 지원 되지 않습니다. toomigrate 응용 프로그램 게이트웨이 사용 하 여 클래식 가상 네트워크 준비 작업 toomove hello 네트워크를 실행 하기 전에 hello 게이트웨이 제거 합니다. Hello 마이그레이션을 완료 한 후 hello Azure 리소스 관리자에서 게이트웨이 다시 연결 합니다.
>
>Express 경로 게이트웨이 tooExpressRoute 회로 다른 구독에 연결 하는 자동으로 마이그레이션할 수 없습니다. 이러한 경우 hello express 경로 게이트웨이 제거 하 고 hello 가상 네트워크 마이그레이션 다음 hello 게이트웨이 다시 만듭니다. 참조 하십시오 [마이그레이션할 ExpressRoute 회로 및 가상 네트워크를 hello 클래식 toohello 리소스 관리자 배포 모델에서 연결 된](../../expressroute/expressroute-migration-classic-resource-manager.md) 자세한 정보에 대 한 합니다.
>
>

## <a name="step-2-install-hello-latest-version-of-azure-powershell"></a>2 단계: hello 최신 버전의 Azure PowerShell 설치
두 가지 기본 옵션 tooinstall Azure PowerShell: [PowerShell 갤러리](https://www.powershellgallery.com/profiles/azure-sdk/) 또는 [웹 플랫폼 설치 관리자 (WebPI)](http://aka.ms/webpi-azps)합니다. WebPI는 매월 업데이트를 수신합니다. PowerShell 갤러리는 지속적으로 업데이트를 수신합니다. 이 문서는 Azure PowerShell 버전 2.1.0을 기반으로 합니다.

설치 지침을 참조 하십시오. [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

<br>

## <a name="step-3-ensure-that-you-are-an-administrator-for-hello-subscription-in-azure-portal"></a>3 단계: Azure 포털에서 구독 hello에 대 한 관리자가 있는지 확인 하십시오.
tooperform이이 마이그레이션 hello에 hello 구독에 대 한 공동 관리자로 추가 해야 [Azure 포털](https://portal.azure.com)합니다.

1. Hello에 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 허브 메뉴에서 선택 **구독**합니다. 표시되지 않으면 **추가 서비스**를 선택합니다.
3. Hello 적절 한 등록 항목을 찾은 다음 hello를 살펴보고 **내 역할** 필드입니다. 공동 관리자에 대 한 hello 값 해야 _계정 관리자_합니다.

공동 관리자 수 tooadd 없는 경우 후 서비스 관리자 또는 공동 관리자에 요청 hello 구독 tooget 직접 추가 합니다.   

## <a name="step-4-set-your-subscription-and-sign-up-for-migration"></a>4단계: 구독 설정 및 마이그레이션에 등록
먼저, PowerShell 프롬프트를 시작합니다. 마이그레이션에 대해 필요한 tooset 모두 기본에 대 한 사용자 환경 및 리소스 관리자입니다.

Hello 리소스 관리자 모델에 대 한 tooyour 계정에 로그인 합니다.

```powershell
    Login-AzureRmAccount
```

Hello 다음 명령을 사용 하 여 hello 사용 가능한 구독을 가져옵니다.

```powershell
    Get-AzureRMSubscription | Sort Name | Select Name
```

현재 세션 hello에 대 한 Azure 구독을 설정 합니다. 이 예제에서는 집합 hello 기본 구독 이름을 너무**내 Azure 구독**합니다. 사용자의 정보로 hello 예제 구독 이름을 바꿉니다.

```powershell
    Select-AzureRmSubscription –SubscriptionName "My Azure Subscription"
```

> [!NOTE]
> 등록은 일회성 단계이지만 마이그레이션 전에 한 번은 수행해야 합니다. 등록을 하지 않고 hello 다음과 같은 오류 메시지가 표시 됩니다.
>
> *BadRequest : 구독이 마이그레이션에 대해 등록되지 않았습니다.*
>
>

다음 명령을 hello를 사용 하 여 hello 마이그레이션 리소스 공급자를 등록 합니다.

```powershell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

5 분까지 hello 등록 toofinish 잠시 기다려 주십시오. 다음 명령을 hello를 사용 하 여 hello 승인의 hello 상태를 확인할 수 있습니다.

```powershell
    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

계속 진행하기 전에 RegistrationState가 `Registered` 인지 확인합니다.

이제 hello 클래식 모델에 대 한 tooyour 계정에 로그인 합니다.

```powershell
    Add-AzureAccount
```

Hello 다음 명령을 사용 하 여 hello 사용 가능한 구독을 가져옵니다.

```powershell
    Get-AzureSubscription | Sort SubscriptionName | Select SubscriptionName
```

현재 세션 hello에 대 한 Azure 구독을 설정 합니다. 이 예에서는 설정 hello 기본 구독 너무**내 Azure 구독**합니다. 사용자의 정보로 hello 예제 구독 이름을 바꿉니다.

```powershell
    Select-AzureSubscription –SubscriptionName "My Azure Subscription"
```

<br>

## <a name="step-5-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a>5 단계: hello VNET 또는 현재 배포의 Azure 지역에서에서 Azure 리소스 관리자 가상 컴퓨터에 충분 한 코어가 있는지 확인
다음 PowerShell 명령을 toocheck hello 현재 코어 수 있는 Azure 리소스 관리자의 hello를 사용할 수 있습니다. 코어 할당량을 대 한 자세한 정보는 toolearn 참조 [제한 및 Azure 리소스 관리자 hello](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)합니다.

Hello에 hello 가용성을 확인 하는이 예제 **West US** 영역입니다. 사용자의 정보로 hello 예제 영역 이름을 바꿉니다.

```powershell
Get-AzureRmVMUsage -Location "West US"
```

## <a name="step-6-run-commands-toomigrate-your-iaas-resources"></a>6 단계: 실행 명령 toomigrate IaaS 리소스
> [!NOTE]
> 여기에서 설명 하는 모든 hello 작업은 idempotent입니다. 지원 되지 않는 기능 또는 구성 오류 이외의 문제가 있는 경우 hello를 다시 시도 하는 것이 좋습니다 준비, 중단 또는 작업을 커밋합니다. hello 플랫폼에는 다음 hello 작업을 다시 시도 합니다.
>
>

## <a name="step-61-option-1---migrate-virtual-machines-in-a-cloud-service-not-in-a-virtual-network"></a>6.1단계: 옵션 1 - 클라우드 서비스(가상 네트워크가 아님)에서 가상 컴퓨터 마이그레이션
다음 명령을, hello를 사용 하 여 클라우드 서비스로 이동한 다음 선택 hello 클라우드 서비스 toomigrate 원하는 hello 목록을 가져옵니다. 가상 네트워크에 있는 hello 클라우드 서비스에 Vm hello 또는 웹 또는 작업자 역할을 서로 hello 명령은 오류 메시지를 반환 합니다.

```powershell
    Get-AzureService | ft Servicename
```

Hello 클라우드 서비스에 대 한 hello 배포 이름을 가져옵니다. 이 예제에서는 hello 서비스 이름이 **내 서비스**합니다. Hello 예제에서는 서비스 이름을 고유한 서비스 이름으로 바꿉니다.

```powershell
    $serviceName = "My Service"
    $deployment = Get-AzureDeployment -ServiceName $serviceName
    $deploymentName = $deployment.DeploymentName
```

마이그레이션에 대 한 hello 클라우드 서비스의 hello 가상 컴퓨터를 준비 합니다. 두 옵션 toochoose를 해야합니다.

* **옵션 1. Hello Vm tooa 플랫폼 만든 가상 네트워크 마이그레이션**

    첫째, 명령 뒤 hello를 사용 하 여 hello 클라우드 서비스를 마이그레이션할 수 있는 경우 유효성 검사:

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    $validate.ValidationMessages
    ```

    hello 앞의 명령은 모든 경고 및 오류를 표시를 마이그레이션하지 못하도록 차단 합니다. 유효성 검사 성공 하는 경우 toohello 이동할 수 있습니다 **준비** 단계:

    ```powershell
    Move-AzureService -Prepare -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    ```
* **옵션 2. Tooan hello 리소스 관리자 배포 모델에서 기존 가상 네트워크 마이그레이션**

    이 예제에서는 집합 hello 리소스 그룹 이름은 너무**myResourceGroup**, 가상 네트워크 이름이 너무 hello**myVirtualNetwork** 서브넷 이름이 너무 hello 및**mySubNet**합니다. Hello 리소스 이름을 사용 하 여 hello 예제 hello 이름을 바꿉니다.

    ```powershell
    $existingVnetRGName = "myResourceGroup"
    $vnetName = "myVirtualNetwork"
    $subnetName = "mySubNet"
    ```

    먼저, 다음 명령을 hello를 사용 하 여 hello 가상 네트워크를 마이그레이션할 수 있는 경우 유효성 검사:

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName -VirtualNetworkName $vnetName -SubnetName $subnetName
    $validate.ValidationMessages
    ```

    hello 앞의 명령은 모든 경고 및 오류를 표시를 마이그레이션하지 못하도록 차단 합니다. 유효성 검사가 성공 하면 다음 계속 진행할 수 준비 단계를 수행 하는 hello:

    ```powershell
        Move-AzureService -Prepare -ServiceName $serviceName -DeploymentName $deploymentName `
        -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName `
        -VirtualNetworkName $vnetName -SubnetName $subnetName
    ```

Hello 옵션 앞에의 하 나와 hello 준비 작업에 성공 하면 hello Vm의 hello 마이그레이션 상태를 쿼리 합니다. Hello에 포함 된 있는지 확인 하세요 `Prepared` 상태입니다.

이 예제에서는 집합 hello VM 이름을 너무**myVM**합니다. 이름 예 hello 사용자 VM 이름으로 대체 합니다.

```powershell
    $vmName = "myVM"
    $vm = Get-AzureVM -ServiceName $serviceName -Name $vmName
    $vm.VM.MigrationState
```

PowerShell 또는 hello Azure 포털을 사용 하 여 리소스를 준비 하는 hello에 대 한 hello 구성을 확인 합니다. 마이그레이션 준비 하지 않은 경우 toogo 백 toohello 이전 상태 hello 다음 명령을 사용 합니다.

```powershell
    Move-AzureService -Abort -ServiceName $serviceName -DeploymentName $deploymentName
```

좋아 보입니다. hello 준비 구성, 앞으로 이동 수 있고 hello 리소스 hello 다음 명령을 사용 하 여 적용 됩니다.

```powershell
    Move-AzureService -Commit -ServiceName $serviceName -DeploymentName $deploymentName
```

## <a name="step-61-option-2---migrate-virtual-machines-in-a-virtual-network"></a>6.1단계: 옵션 2 - 가상 네트워크에서 가상 컴퓨터 마이그레이션

가상 컴퓨터 toomigrate hello 가상 네트워크를 마이그레이션 가상 네트워크에 있습니다. 가상 컴퓨터 hello hello 가상 네트워크와 함께 자동으로 마이그레이션합니다. Toomigrate 않겠다고 선택 hello 가상 네트워크입니다.
> [!NOTE]
> [단일 클래식 가상 컴퓨터 마이그레이션](migrate-single-classic-to-resource-manager.md) hello 가상 컴퓨터의 hello VHD (OS 및 데이터) 파일을 사용 하 여 관리 되는 디스크와 새 리소스 관리자 가상 컴퓨터를 만들어 합니다.
<br>

> [!NOTE]
> 가상 네트워크 이름은 hello hello에 표시 된 항목에서 다를 수 있습니다 새 포털입니다. hello 새 Azure 포털 이름을 표시 하는 hello로 `[vnet-name]` 있지만 hello 실제 가상 네트워크 이름은 유형이 `Group [resource-group-name] [vnet-name]`합니다. Hello 명령을 사용 하 여 조회 hello 실제 가상 네트워크 이름을 마이그레이션하기 전에 `Get-AzureVnetSite | Select -Property Name` hello에서 보기 또는 Azure 포털을 이전 합니다. 

이 예제에서는 집합 hello 가상 네트워크 이름이 너무**myVnet**합니다. 사용자의 정보로 hello 예제에서는 가상 네트워크 이름을 바꿉니다.

```powershell
    $vnetName = "myVnet"
```

> [!NOTE]
> 지원 되지 않는 구성으로 웹 또는 작업자 역할 또는 Vm을 포함 하는 hello 가상 네트워크, 경우에 유효성 검사 오류 메시지를 가져옵니다.
>
>

첫째, hello 다음 명령을 사용 하 여 hello 가상 네트워크를 마이그레이션하는 경우 유효성 검사:

```powershell
    Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
```

hello 앞의 명령은 모든 경고 및 오류를 표시를 마이그레이션하지 못하도록 차단 합니다. 유효성 검사가 성공 하면 다음 계속 진행할 수 준비 단계를 수행 하는 hello:

```powershell
    Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
```

Hello Azure 포털 또는 Azure PowerShell을 사용 하 여 가상 컴퓨터를 준비 하는 hello에 대 한 hello 구성을 확인 합니다. 마이그레이션 준비 하지 않은 경우 toogo 백 toohello 이전 상태 hello 다음 명령을 사용 합니다.

```powershell
    Move-AzureVirtualNetwork -Abort -VirtualNetworkName $vnetName
```

좋아 보입니다. hello 준비 구성, 앞으로 이동 수 있고 hello 리소스 hello 다음 명령을 사용 하 여 적용 됩니다.

```powershell
    Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
```

## <a name="step-62-migrate-a-storage-account"></a>6.2단계 저장소 계정 마이그레이션
Hello 가상 컴퓨터를 마이그레이션하거나 완료 하 고 나면 hello 저장소 계정을 마이그레이션하는 것이 좋습니다.

저장소 계정 hello를 마이그레이션하기 전에 앞에 필수 구성 요소 검사를 수행 하십시오.

* **Hello 저장소 계정에 해당 디스크가 저장 되는 클래식 가상 컴퓨터 마이그레이션**

    명령 앞 hello 저장소 계정에서 모든 hello 클래식 VM 디스크의 역할 이름 및 DiskName 속성을 반환 합니다. 역할 이름에는 디스크를 연결 된 hello 가상 컴퓨터 toowhich hello 이름입니다. 명령 앞 디스크 마이그레이션을 수행 하기 전에 이러한 디스크가 연결 되어 해당 가상 컴퓨터 toowhich 마이그레이션됩니다를 확인 한 다음 반환 하는 경우 저장소 계정 hello 합니다.
    ```powershell
     $storageAccountName = 'yourStorageAccountName'
      Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Select-Object -ExpandProperty AttachedTo -Property `
      DiskName | Format-List -Property RoleName, DiskName

    ```
* **Hello 저장소 계정에 저장 하는 연결 되지 않은 클래식 VM 디스크를 삭제 합니다.**

    Hello 저장소에서 클래식 VM 디스크를 연결 되지 않은 다음 명령을 사용 하 여 계정을 찾습니다.

    ```powershell
        $storageAccountName = 'yourStorageAccountName'
        Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Where-Object -Property AttachedTo -EQ $null | Format-List -Property DiskName  

    ```
    위의 명령이 디스크를 반환하면 다음 명령을 사용하여 다음과 같은 디스크를 삭제합니다.

    ```powershell
       Remove-AzureDisk -DiskName 'yourDiskName'
    ```
* **Hello 저장소 계정에 저장 된 VM 이미지를 삭제**

    명령 앞 OS 디스크 hello 저장소 계정에 저장 된 모든 hello VM 이미지를 반환 합니다.
     ```powershell
        Get-AzureVmImage | Where-Object { $_.OSDiskConfiguration.MediaLink -ne $null -and $_.OSDiskConfiguration.MediaLink.Host.Contains($storageAccountName)`
                                } | Select-Object -Property ImageName, ImageLabel
     ```
     명령 앞 hello 저장소 계정에 저장 된 데이터 디스크와 모든 hello VM 이미지 반환 합니다.
     ```powershell

        Get-AzureVmImage | Where-Object {$_.DataDiskConfigurations -ne $null `
                                         -and ($_.DataDiskConfigurations | Where-Object {$_.MediaLink -ne $null -and $_.MediaLink.Host.Contains($storageAccountName)}).Count -gt 0 `
                                        } | Select-Object -Property ImageName, ImageLabel
     ```
    앞의 명령을 사용 하 여 명령을 위에 반환한 모든 hello VM 이미지를 삭제 합니다.
    ```powershell
    Remove-AzureVMImage -ImageName 'yourImageName'
    ```

다음 명령을 hello를 사용 하 여 마이그레이션 위한 저장소 계정당의 유효성을 검사 합니다. 이 예에서 hello 저장소 계정 이름은 **myStorageAccount**합니다. Hello 예제 이름을의 고유한 저장소 계정 hello 이름으로 바꿉니다.

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Validate -StorageAccountName $storageAccountName
```

다음 단계는 마이그레이션에 대 한 tooPrepare hello 저장소 계정

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Prepare -StorageAccountName $storageAccountName
```

Hello Azure 포털 또는 Azure PowerShell을 사용 하 여 저장소 계정을 준비 하는 hello에 대 한 hello 구성을 확인 합니다. 마이그레이션 준비 하지 않은 경우 toogo 백 toohello 이전 상태 hello 다음 명령을 사용 합니다.

```powershell
    Move-AzureStorageAccount -Abort -StorageAccountName $storageAccountName
```

좋아 보입니다. hello 준비 구성, 앞으로 이동 수 있고 hello 리소스 hello 다음 명령을 사용 하 여 적용 됩니다.

```powershell
    Move-AzureStorageAccount -Commit -StorageAccountName $storageAccountName
```

## <a name="next-steps"></a>다음 단계
* [클래식 tooAzure 리소스 관리자에서에서 리소스를 IaaS 플랫폼에서 지 원하는 마이그레이션 개요](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [클래식 tooAzure 리소스 관리자에서에서 마이그레이션 플랫폼 지원에 기술 심층 분석](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [클래식 tooAzure 리소스 관리자에서에서 IaaS 리소스의 마이그레이션 계획](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [CLI toomigrate IaaS 리소스 클래식 tooAzure 리소스 관리자를에서 사용 하 여](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [클래식 tooAzure 리소스 관리자에서에서 IaaS 리소스의 마이그레이션 지원에 대 한 커뮤니티 도구](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [가장 일반적인 마이그레이션 오류 검토](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [클래식 tooAzure 리소스 관리자에서에서 마이그레이션 IaaS 리소스에 대 한 가장 자주 묻는 질문 검토 hello](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
