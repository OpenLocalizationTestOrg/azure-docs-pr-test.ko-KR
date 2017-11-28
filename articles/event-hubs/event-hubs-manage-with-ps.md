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
# <a name="use-powershell-toomanage-event-hubs-resources"></a><span data-ttu-id="d470f-103">PowerShell toomanage 이벤트 허브 리소스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="d470f-103">Use PowerShell toomanage Event Hubs resources</span></span>

<span data-ttu-id="d470f-104">Microsoft Azure PowerShell은 toocontrol를 사용 하 고 Azure 서비스의 hello 배포 및 관리를 자동화할 수 있는 스크립팅 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="d470f-104">Microsoft Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of Azure services.</span></span> <span data-ttu-id="d470f-105">이 문서에서는 설명 방법을 toouse hello [이벤트 허브 리소스 관리자 PowerShell 모듈](/powershell/module/azurerm.eventhub) tooprovision 이벤트 허브 엔터티 (네임 스페이스, 개별 이벤트 허브 및 소비자 그룹) 하 고 관리 하는 로컬 Azure PowerShell 콘솔을 사용 하 여 또는 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="d470f-105">This article describes how toouse hello [Event Hubs Resource Manager PowerShell module](/powershell/module/azurerm.eventhub) tooprovision and manage Event Hubs entities (namespaces, individual event hubs, and consumer groups) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="d470f-106">Azure Resource Manager 템플릿을 사용하여 Event Hubs 리소스를 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d470f-106">You can also manage Event Hubs resources using Azure Resource Manager templates.</span></span> <span data-ttu-id="d470f-107">자세한 내용은 hello 문서 참조 [Azure 리소스 관리자 템플릿을 사용 하 여 이벤트 허브 및 소비자 그룹을 가진 이벤트 허브 네임 스페이스를 만들려면](event-hubs-resource-manager-namespace-event-hub.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d470f-107">For more information, see hello article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d470f-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d470f-108">Prerequisites</span></span>

<span data-ttu-id="d470f-109">시작 하기 전에 hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d470f-109">Before you begin, you'll need hello following:</span></span>

* <span data-ttu-id="d470f-110">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="d470f-110">An Azure subscription.</span></span> <span data-ttu-id="d470f-111">구독을 얻는 방법에 대한 자세한 내용은 [구매 옵션][purchase options], [구성원 제공 항목][member offers] 또는 [무료 계정][free account]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d470f-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="d470f-112">Azure PowerShell이 설치된 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="d470f-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="d470f-113">관련 지침은 [Azure PowerShell Cmdlet 시작](/powershell/azure/get-started-azureps)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d470f-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="d470f-114">PowerShell 스크립트, NuGet 패키지 및.NET Framework hello 일반 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d470f-114">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="d470f-115">시작</span><span class="sxs-lookup"><span data-stu-id="d470f-115">Get started</span></span>

<span data-ttu-id="d470f-116">hello 첫 단계는 tooyour Azure 계정에에서 PowerShell toolog toouse 및 Azure 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="d470f-116">hello first step is toouse PowerShell toolog in tooyour Azure account and Azure subscription.</span></span> <span data-ttu-id="d470f-117">Hello 지침에 따라 [Azure PowerShell cmdlet과 함께 시작](/powershell/azure/get-started-azureps) toolog tooyour Azure 계정에에서 다음 검색 및 Azure 구독에서 hello 리소스에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="d470f-117">Follow hello instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) toolog in tooyour Azure account, then retrieve and access hello resources in your Azure subscription.</span></span>

## <a name="provision-an-event-hubs-namespace"></a><span data-ttu-id="d470f-118">Event Hubs 네임스페이스 프로비전</span><span class="sxs-lookup"><span data-stu-id="d470f-118">Provision an Event Hubs namespace</span></span>

<span data-ttu-id="d470f-119">이벤트 허브 네임 스페이스를 사용할 때는 hello를 사용할 수 있습니다 [Get AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [새로 AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [제거 AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace) 및 [집합 AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d470f-119">When working with Event Hubs namespaces, you can use hello [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Remove-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace), and [Set-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlets.</span></span>

<span data-ttu-id="d470f-120">이 예에서는 hello 스크립트;에 몇 가지 지역 변수를 만듭니다. `$Namespace` 및 `$Location`합니다.</span><span class="sxs-lookup"><span data-stu-id="d470f-120">This example creates a few local variables in hello script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="d470f-121">`$Namespace`hello toowork는 원하는 hello 이벤트 허브 네임 스페이스 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="d470f-121">`$Namespace` is hello name of hello Event Hubs namespace with which we want toowork.</span></span>
* <span data-ttu-id="d470f-122">`$Location`hello 데이터 센터를 식별 했습니다 hello 네임 스페이스 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="d470f-122">`$Location` identifies hello data center in which will we provision hello namespace.</span></span>
* <span data-ttu-id="d470f-123">`$CurrentNamespace`에서는 검색 하거나이 작성 하는 hello 참조 네임 스페이스를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d470f-123">`$CurrentNamespace` stores hello reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="d470f-124">실제 스크립트에서 `$Namespace` 및 `$Location`은(는) 매개 변수로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d470f-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="d470f-125">이 부분의 hello 스크립트는 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="d470f-125">This part of hello script does hello following:</span></span>

1. <span data-ttu-id="d470f-126">시도 tooretrieve hello로는 이벤트 허브 네임 스페이스 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d470f-126">Attempts tooretrieve an Event Hubs namespace with hello specified name.</span></span>
2. <span data-ttu-id="d470f-127">Hello 네임 스페이스가 있으면 발견 한를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d470f-127">If hello namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="d470f-128">Hello 네임 스페이스 없으면 hello 네임 스페이스 만들고 hello 새로 생성 된 네임 스페이스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="d470f-128">If hello namespace is not found, it creates hello namespace and then retrieves hello newly created namespace.</span></span>

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

## <a name="create-an-event-hub"></a><span data-ttu-id="d470f-129">이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="d470f-129">Create an event hub</span></span>

<span data-ttu-id="d470f-130">toocreate 이벤트 허브 hello 스크립트를 사용 하 여 hello 이전 섹션에서 네임 스페이스 확인을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d470f-130">toocreate an event hub, perform a namespace check using hello script in hello previous section.</span></span> <span data-ttu-id="d470f-131">그런 다음 사용 하는 hello [새로 AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) cmdlet toocreate hello 이벤트 허브:</span><span class="sxs-lookup"><span data-stu-id="d470f-131">Then, use hello [New-AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) cmdlet toocreate hello event hub:</span></span>

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

### <a name="create-a-consumer-group"></a><span data-ttu-id="d470f-132">소비자 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="d470f-132">Create a consumer group</span></span>

<span data-ttu-id="d470f-133">내에서 이벤트 허브 소비자 그룹 toocreate hello 네임 스페이스 및 이벤트 허브 검사 hello 스크립트를 사용 하 여 hello 이전 섹션에서 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d470f-133">toocreate a consumer group within an event hub, perform hello namespace and event hub checks using hello scripts in hello previous section.</span></span> <span data-ttu-id="d470f-134">그런 다음 hello를 사용 하 여 [새로 AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) hello 이벤트 허브 내 cmdlet toocreate hello 소비자 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="d470f-134">Then, use hello [New-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) cmdlet toocreate hello consumer group within hello event hub.</span></span> <span data-ttu-id="d470f-135">예:</span><span class="sxs-lookup"><span data-stu-id="d470f-135">For example:</span></span>

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

#### <a name="set-user-metadata"></a><span data-ttu-id="d470f-136">사용자 메타데이터 설정</span><span class="sxs-lookup"><span data-stu-id="d470f-136">Set user metadata</span></span>

<span data-ttu-id="d470f-137">이전 섹션 hello을 hello 스크립트를 실행 한 후 hello를 사용할 수 있습니다 [집합 AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) hello 다음 예제와 같이 소비자 그룹의 cmdlet tooupdate hello 속성:</span><span class="sxs-lookup"><span data-stu-id="d470f-137">After executing hello scripts in hello preceding sections, you can use hello [Set-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) cmdlet tooupdate hello properties of a consumer group, as in hello following example:</span></span>

```powershell
# Set some user metadata on hello CG
Write-Host "Setting hello UserMetadata field too'Testing'"
Set-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -UserMetadata "Testing"
# Show result
Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
```

## <a name="remove-event-hub"></a><span data-ttu-id="d470f-138">이벤트 허브 제거</span><span class="sxs-lookup"><span data-stu-id="d470f-138">Remove event hub</span></span>

<span data-ttu-id="d470f-139">만든 tooremove hello 이벤트 허브를 hello를 사용할 수 있습니다 `Remove-*` hello 다음 예제와 같이 cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d470f-139">tooremove hello event hubs you created, you can use hello `Remove-*` cmdlets, as in hello following example:</span></span>

```powershell
# Clean up
Remove-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
Remove-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
Remove-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
```

## <a name="next-steps"></a><span data-ttu-id="d470f-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d470f-140">Next steps</span></span>

- <span data-ttu-id="d470f-141">Hello 전체 이벤트 허브 리소스 관리자 PowerShell 모듈 설명서를 참조 하십시오. [여기](/powershell/module/azurerm.eventhub)합니다.</span><span class="sxs-lookup"><span data-stu-id="d470f-141">See hello complete Event Hubs Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.eventhub).</span></span> <span data-ttu-id="d470f-142">이 페이지에는 사용 가능한 모든 cmdlet이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d470f-142">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="d470f-143">Azure 리소스 관리자 템플릿을 사용 하는 방법에 대 한 내용은 hello 문서 참조 [Azure 리소스 관리자 템플릿을 사용 하 여 이벤트 허브 및 소비자 그룹을 가진 이벤트 허브 네임 스페이스를 만들려면](event-hubs-resource-manager-namespace-event-hub.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d470f-143">For information about using Azure Resource Manager templates, see hello article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>
- <span data-ttu-id="d470f-144">[Event Hubs .NET 관리 라이브러리](event-hubs-management-libraries.md)에 대한 정보</span><span class="sxs-lookup"><span data-stu-id="d470f-144">Information about [Event Hubs .NET management libraries](event-hubs-management-libraries.md).</span></span>

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
