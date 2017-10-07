---
title: "aaaUse PowerShell toomanage Azure 이벤트 허브 리소스 | Microsoft Docs"
description: "PowerShell 모듈 toocreate를 사용 하 여 이벤트 허브 및 관리"
services: event-hubs
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: d79cb307c2b4a031d059ce6ca67117ffc0b4600b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-event-hubs-resources"></a>PowerShell toomanage 이벤트 허브 리소스를 사용 하 여

Microsoft Azure PowerShell은 toocontrol를 사용 하 고 Azure 서비스의 hello 배포 및 관리를 자동화할 수 있는 스크립팅 환경입니다. 이 문서에서는 설명 방법을 toouse hello [이벤트 허브 리소스 관리자 PowerShell 모듈](/powershell/module/azurerm.eventhub) tooprovision 이벤트 허브 엔터티 (네임 스페이스, 개별 이벤트 허브 및 소비자 그룹) 하 고 관리 하는 로컬 Azure PowerShell 콘솔을 사용 하 여 또는 스크립트입니다.

Azure Resource Manager 템플릿을 사용하여 Event Hubs 리소스를 관리할 수도 있습니다. 자세한 내용은 hello 문서 참조 [Azure 리소스 관리자 템플릿을 사용 하 여 이벤트 허브 및 소비자 그룹을 가진 이벤트 허브 네임 스페이스를 만들려면](event-hubs-resource-manager-namespace-event-hub.md)합니다.

## <a name="prerequisites"></a>필수 조건

시작 하기 전에 hello 다음이 필요 합니다.

* Azure 구독. 구독을 얻는 방법에 대한 자세한 내용은 [구매 옵션][purchase options], [구성원 제공 항목][member offers] 또는 [무료 계정][free account]을 참조하세요.
* Azure PowerShell이 설치된 컴퓨터 관련 지침은 [Azure PowerShell Cmdlet 시작](/powershell/azure/get-started-azureps)을 참조하세요.
* PowerShell 스크립트, NuGet 패키지 및.NET Framework hello 일반 이해 해야 합니다.

## <a name="get-started"></a>시작

hello 첫 단계는 tooyour Azure 계정에에서 PowerShell toolog toouse 및 Azure 구독입니다. Hello 지침에 따라 [Azure PowerShell cmdlet과 함께 시작](/powershell/azure/get-started-azureps) toolog tooyour Azure 계정에에서 다음 검색 및 Azure 구독에서 hello 리소스에 액세스 합니다.

## <a name="provision-an-event-hubs-namespace"></a>Event Hubs 네임스페이스 프로비전

이벤트 허브 네임 스페이스를 사용할 때는 hello를 사용할 수 있습니다 [Get AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [새로 AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [제거 AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace) 및 [집합 AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlet.

이 예에서는 hello 스크립트;에 몇 가지 지역 변수를 만듭니다. `$Namespace` 및 `$Location`합니다.

* `$Namespace`hello toowork는 원하는 hello 이벤트 허브 네임 스페이스 이름이입니다.
* `$Location`hello 데이터 센터를 식별 했습니다 hello 네임 스페이스 준비 합니다.
* `$CurrentNamespace`에서는 검색 하거나이 작성 하는 hello 참조 네임 스페이스를 저장 합니다.

실제 스크립트에서 `$Namespace` 및 `$Location`은(는) 매개 변수로 전달할 수 있습니다.

이 부분의 hello 스크립트는 다음 hello:

1. 시도 tooretrieve hello로는 이벤트 허브 네임 스페이스 이름을 지정 합니다.
2. Hello 네임 스페이스가 있으면 발견 한를 보고 합니다.
3. Hello 네임 스페이스 없으면 hello 네임 스페이스 만들고 hello 새로 생성 된 네임 스페이스를 검색 합니다.

    ```powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
    }
    ```

## <a name="create-an-event-hub"></a>이벤트 허브 만들기

toocreate 이벤트 허브 hello 스크립트를 사용 하 여 hello 이전 섹션에서 네임 스페이스 확인을 수행 합니다. 그런 다음 사용 하는 hello [새로 AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) cmdlet toocreate hello 이벤트 허브:

```powershell
# Check if event hub already exists
$CurrentEH = Get-AzureRMEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName

if($CurrentEH)
{
    Write-Host "hello event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $EventHubName event hub does not exist."
    Write-Host "Creating hello $EventHubName event hub in hello $Location region..."
    New-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -Location $Location -MessageRetentionInDays 3
    $CurrentEH = Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $EventHubName event hub in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="create-a-consumer-group"></a>소비자 그룹 만들기

내에서 이벤트 허브 소비자 그룹 toocreate hello 네임 스페이스 및 이벤트 허브 검사 hello 스크립트를 사용 하 여 hello 이전 섹션에서 수행 됩니다. 그런 다음 hello를 사용 하 여 [새로 AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) hello 이벤트 허브 내 cmdlet toocreate hello 소비자 그룹입니다. 예:

```powershell
# Check if consumer group already exists
$CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -ErrorAction Ignore

if($CurrentCG)
{
    Write-Host "hello consumer group $ConsumerGroupName in event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $ConsumerGroupName consumer group does not exist."
    Write-Host "Creating hello $ConsumerGroupName consumer group in hello $Location region..."
    New-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
    $CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $ConsumerGroupName consumer group in event hub $EventHubName in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

#### <a name="set-user-metadata"></a>사용자 메타데이터 설정

이전 섹션 hello을 hello 스크립트를 실행 한 후 hello를 사용할 수 있습니다 [집합 AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) hello 다음 예제와 같이 소비자 그룹의 cmdlet tooupdate hello 속성:

```powershell
# Set some user metadata on hello CG
Write-Host "Setting hello UserMetadata field too'Testing'"
Set-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -UserMetadata "Testing"
# Show result
Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
```

## <a name="remove-event-hub"></a>이벤트 허브 제거

만든 tooremove hello 이벤트 허브를 hello를 사용할 수 있습니다 `Remove-*` hello 다음 예제와 같이 cmdlet:

```powershell
# Clean up
Remove-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
Remove-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
Remove-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
```

## <a name="next-steps"></a>다음 단계

- Hello 전체 이벤트 허브 리소스 관리자 PowerShell 모듈 설명서를 참조 하십시오. [여기](/powershell/module/azurerm.eventhub)합니다. 이 페이지에는 사용 가능한 모든 cmdlet이 표시됩니다.
- Azure 리소스 관리자 템플릿을 사용 하는 방법에 대 한 내용은 hello 문서 참조 [Azure 리소스 관리자 템플릿을 사용 하 여 이벤트 허브 및 소비자 그룹을 가진 이벤트 허브 네임 스페이스를 만들려면](event-hubs-resource-manager-namespace-event-hub.md)합니다.
- [Event Hubs .NET 관리 라이브러리](event-hubs-management-libraries.md)에 대한 정보

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
