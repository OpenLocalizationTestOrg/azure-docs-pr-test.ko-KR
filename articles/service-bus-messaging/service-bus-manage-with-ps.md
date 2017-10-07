---
title: "aaaUse PowerShell toomanage Azure 서비스 버스 리소스 | Microsoft Docs"
description: "PowerShell 모듈 toocreate를 사용 하 고 서비스 버스 리소스 관리"
services: service-bus-messaging
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/06/2017
ms.author: sethm
ms.openlocfilehash: 737044def913c5798e7e05fc4f1aeece76c8f4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-service-bus-resources"></a>PowerShell toomanage 서비스 버스 리소스를 사용 하 여

Microsoft Azure PowerShell은 toocontrol를 사용 하 고 Azure 서비스의 hello 배포 및 관리를 자동화할 수 있는 스크립팅 환경입니다. 이 문서에서는 설명 방법을 toouse hello [서비스 버스 리소스 관리자 PowerShell 모듈](/powershell/module/azurerm.servicebus) tooprovision 서비스 버스 엔터티 (네임 스페이스, 큐, 토픽 및 구독) 하 고 관리 하는 로컬 Azure PowerShell 콘솔을 사용 하 여 또는 스크립트입니다.

Azure Resource Manager 템플릿을 사용하여 Service Bus 엔터티를 관리할 수도 있습니다. 자세한 내용은 hello 문서 참조 [Azure 리소스 관리자 템플릿을 사용 하 여 서비스 버스 만들기 리소스](service-bus-resource-manager-overview.md)합니다.

## <a name="prerequisites"></a>필수 조건

시작 하기 전에 hello 다음이 필요 합니다.

* Azure 구독. 구독을 얻는 방법에 대한 자세한 내용은 [구매 옵션][purchase options], [구성원 제공 항목][member offers] 또는 [무료 계정][free account]을 참조하세요.
* Azure PowerShell이 설치된 컴퓨터 관련 지침은 [Azure PowerShell Cmdlet 시작](/powershell/azure/get-started-azureps)을 참조하세요.
* PowerShell 스크립트, NuGet 패키지 및.NET Framework hello 일반 이해 해야 합니다.

## <a name="get-started"></a>시작

hello 첫 단계는 tooyour Azure 계정에에서 PowerShell toolog toouse 및 Azure 구독입니다. Hello 지침에 따라 [Azure PowerShell cmdlet과 함께 시작](/powershell/azure/get-started-azureps) toolog tooyour Azure 계정 및 Azure 구독에서 hello 리소스를 검색 하 고 액세스 합니다.

## <a name="provision-a-service-bus-namespace"></a>서비스 버스 네임스페이스 프로비전

서비스 버스 네임 스페이스를 사용할 때는 hello를 사용할 수 있습니다 [Get AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [새로 AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [제거-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), 및 [집합 AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlet.

이 예에서는 hello 스크립트;에 몇 가지 지역 변수를 만듭니다. `$Namespace` 및 `$Location`합니다.

* `$Namespace`hello toowork는 원하는 hello 서비스 버스 네임 스페이스 이름이입니다.
* `$Location`hello 데이터 센터를 식별 했습니다 hello 네임 스페이스 준비 합니다.
* `$CurrentNamespace`에서는 검색 하거나이 작성 하는 hello 참조 네임 스페이스를 저장 합니다.

실제 스크립트에서 `$Namespace` 및 `$Location`은(는) 매개 변수로 전달할 수 있습니다.

이 부분의 hello 스크립트는 다음 hello:

1. 시도 tooretrieve hello로 서비스 버스 네임 스페이스 이름을 지정 합니다.
2. Hello 네임 스페이스가 있으면 발견 한를 보고 합니다.
3. Hello 네임 스페이스 없으면 hello 네임 스페이스 만들고 hello 새로 생성 된 네임 스페이스를 검색 합니다.
   
    ``` powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
                
    }
    ```

### <a name="create-a-namespace-authorization-rule"></a>네임스페이스 권한 부여 규칙 만들기

hello 다음 예제에서는 어떻게 toomanage 네임 스페이스 권한 부여 규칙을 사용 하 여 hello [새로 AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [집합 AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), 및 [제거 AzureRmServiceBusNamespaceAuthorizationRule cmdlet](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule)합니다.

```powershell
# Query toosee if rule exists
$CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

# Check if hello rule already exists or needs toobe created
if ($CurrentRule)
{
    Write-Host "hello $AuthRule rule already exists for hello namespace $Namespace."
}
else
{
    Write-Host "hello $AuthRule rule does not exist."
    Write-Host "Creating hello $AuthRule rule for hello $Namespace namespace..."
    New-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule -Rights @("Listen","Send")
    $CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
    Write-Host "hello $AuthRule rule for hello $Namespace namespace has been successfully created."

    Write-Host "Setting rights on hello namespace"
    $authRuleObj = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

    Write-Host "Remove Send rights"
    $authRuleObj.Rights.Remove("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Add Send and Manage rights toohello namespace"
    $authRuleObj.Rights.Add("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj
    $authRuleObj.Rights.Add("Manage")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Show value of primary key"
    $CurrentKey = Get-AzureRmServiceBusNamespaceKey -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
        
    Write-Host "Remove this authorization rule"
    Remove-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
}
```

## <a name="create-a-queue"></a>큐 만들기

toocreate 큐 나 항목에는 hello 스크립트를 사용 하 여 hello 이전 섹션에서 네임 스페이스 확인을 수행 합니다. 그런 다음 hello 큐를 만듭니다.

```powershell
# Check if queue already exists
$CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName

if($CurrentQ)
{
    Write-Host "hello queue $QueueName already exists in hello $Location region:"
}
else
{
    Write-Host "hello $QueueName queue does not exist."
    Write-Host "Creating hello $QueueName queue in hello $Location region..."
    New-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -EnablePartitioning $True
    $CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName
    Write-Host "hello $QueueName queue in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="modify-queue-properties"></a>큐 속성 수정

Hello 섹션 앞의 hello 스크립트를 실행 한 후 hello를 사용할 수 있습니다 [집합 AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) hello 다음 예제와 같이 큐의 cmdlet tooupdate hello 속성:

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a>다른 서비스 버스 엔터티 프로비전

Hello를 사용할 수 있습니다 [서비스 버스 PowerShell 모듈](/powershell/module/azurerm.servicebus) tooprovision 항목 및 구독 같은 다른 엔터티에 합니다. 이러한 cmdlet은 유사한 구문상 toohello 큐 만들기 cmdlet hello 이전 단원에서 설명 합니다.

## <a name="next-steps"></a>다음 단계

- Hello 전체 서비스 버스 리소스 관리자 PowerShell 모듈 설명서를 참조 하십시오. [여기](/powershell/module/azurerm.servicebus)합니다. 이 페이지에는 사용 가능한 모든 cmdlet이 표시됩니다.
- Azure 리소스 관리자 템플릿을 사용 하는 방법에 대 한 내용은 hello 문서 참조 [Azure 리소스 관리자 템플릿을 사용 하 여 서비스 버스 만들기 리소스](service-bus-resource-manager-overview.md)합니다.
- [Service Bus .NET 관리 라이브러리](service-bus-management-libraries.md)에 대한 정보

몇 가지 다른 방식으로 toomanage 서비스 버스 엔터티 다음 블로그 게시물에 설명 된 대로

* [어떻게 toocreate 서비스 버스 큐, 항목 및 PowerShell 스크립트를 사용 하 여 구독](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [어떻게 toocreate 서비스 버스 Namespace 및 PowerShell 스크립트를 사용 하 여 이벤트 허브](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [Service Bus PowerShell 스크립트](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
