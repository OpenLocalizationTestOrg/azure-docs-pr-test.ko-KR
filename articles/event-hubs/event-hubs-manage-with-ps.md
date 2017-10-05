---
title: "PowerShell을 사용한 Azure Event Hubs 리소스 관리 | Microsoft Docs"
description: "PowerShell 모듈을 사용하여 Event Hubs 만들기 및 관리"
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
ms.openlocfilehash: 2b49c01153b1104612e6ebf9c88566fc40d1f635
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="use-powershell-to-manage-event-hubs-resources"></a><span data-ttu-id="2fb01-103">PowerShell을 사용하여 Event Hubs 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="2fb01-103">Use PowerShell to manage Event Hubs resources</span></span>

<span data-ttu-id="2fb01-104">Microsoft Azure PowerShell은 Azure 서비스의 배포와 관리를 제어하고 자동화하는 데 사용할 수 있는 스크립팅 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb01-104">Microsoft Azure PowerShell is a scripting environment that you can use to control and automate the deployment and management of Azure services.</span></span> <span data-ttu-id="2fb01-105">이 문서에서는 [Event Hubs Resource Manager PowerShell 모듈](/powershell/module/azurerm.eventhub)을 사용하여 로컬 Azure PowerShell 콘솔 또는 스크립트를 통해 Event Hubs 엔터티(네임스페이스, 개별 이벤트 허브 및 소비자 그룹)를 프로비전하고 관리하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb01-105">This article describes how to use the [Event Hubs Resource Manager PowerShell module](/powershell/module/azurerm.eventhub) to provision and manage Event Hubs entities (namespaces, individual event hubs, and consumer groups) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="2fb01-106">Azure Resource Manager 템플릿을 사용하여 Event Hubs 리소스를 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fb01-106">You can also manage Event Hubs resources using Azure Resource Manager templates.</span></span> <span data-ttu-id="2fb01-107">자세한 내용은 문서 [Azure Resource Manager 템플릿을 사용하여 이벤트 허브 및 소비자 그룹이 있는 Event Hubs 네임스페이스 만들기](event-hubs-resource-manager-namespace-event-hub.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fb01-107">For more information, see the article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2fb01-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2fb01-108">Prerequisites</span></span>

<span data-ttu-id="2fb01-109">이 작업을 수행하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb01-109">Before you begin, you'll need the following:</span></span>

* <span data-ttu-id="2fb01-110">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="2fb01-110">An Azure subscription.</span></span> <span data-ttu-id="2fb01-111">구독을 얻는 방법에 대한 자세한 내용은 [구매 옵션][purchase options], [구성원 제공 항목][member offers] 또는 [무료 계정][free account]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fb01-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="2fb01-112">Azure PowerShell이 설치된 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="2fb01-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="2fb01-113">관련 지침은 [Azure PowerShell Cmdlet 시작](/powershell/azure/get-started-azureps)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fb01-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="2fb01-114">PowerShell 스크립트, NuGet 패키지 및 .NET Framework 전반에 대한 지식</span><span class="sxs-lookup"><span data-stu-id="2fb01-114">A general understanding of PowerShell scripts, NuGet packages, and the .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="2fb01-115">시작</span><span class="sxs-lookup"><span data-stu-id="2fb01-115">Get started</span></span>

<span data-ttu-id="2fb01-116">첫 번째 단계는 PowerShell을 사용하여 Azure 계정 및 Azure 구독에 로그인하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb01-116">The first step is to use PowerShell to log in to your Azure account and Azure subscription.</span></span> <span data-ttu-id="2fb01-117">[Azure PowerShell cmdlet 시작](/powershell/azure/get-started-azureps)의 지침에 따라 Azure 계정에 로그인한 다음, Azure 구독에서 리소스를 검색하고 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb01-117">Follow the instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) to log in to your Azure account, then retrieve and access the resources in your Azure subscription.</span></span>

## <a name="provision-an-event-hubs-namespace"></a><span data-ttu-id="2fb01-118">Event Hubs 네임스페이스 프로비전</span><span class="sxs-lookup"><span data-stu-id="2fb01-118">Provision an Event Hubs namespace</span></span>

<span data-ttu-id="2fb01-119">Event Hubs 네임스페이스를 사용할 때 [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Remove-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace) 및 [Set-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fb01-119">When working with Event Hubs namespaces, you can use the [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Remove-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace), and [Set-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlets.</span></span>

<span data-ttu-id="2fb01-120">이 예제에서는 스크립트에 `$Namespace`과(와) `$Location`(이)라는 몇 가지 로컬 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2fb01-120">This example creates a few local variables in the script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="2fb01-121">`$Namespace`는 사용하려는 Event Hubs 네임스페이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2fb01-121">`$Namespace` is the name of the Event Hubs namespace with which we want to work.</span></span>
* <span data-ttu-id="2fb01-122">`$Location`은(는) 네임스페이스를 프로비전할 데이터 센터를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb01-122">`$Location` identifies the data center in which will we provision the namespace.</span></span>
* <span data-ttu-id="2fb01-123">`$CurrentNamespace`에는 검색하거나 만드는 참조 네임스페이스가 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fb01-123">`$CurrentNamespace` stores the reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="2fb01-124">실제 스크립트에서 `$Namespace` 및 `$Location`은(는) 매개 변수로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fb01-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="2fb01-125">스크립트의 이 부분은 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb01-125">This part of the script does the following:</span></span>

1. <span data-ttu-id="2fb01-126">지정된 이름의 Event Hubs 네임스페이스를 검색하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb01-126">Attempts to retrieve an Event Hubs namespace with the specified name.</span></span>
2. <span data-ttu-id="2fb01-127">네임스페이스가 있으면 발견된 항목을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb01-127">If the namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="2fb01-128">네임스페이스가 없으면 만든 다음 새로 만든 네임스페이스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb01-128">If the namespace is not found, it creates the namespace and then retrieves the newly created namespace.</span></span>

    ```powershell
    # Query to see if the namespace currently exists
    $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
   
    # Check if the namespace already exists or needs to be created
    if ($CurrentNamespace)
    {
        Write-Host "The namespace $Namespace already exists in the $Location region:"
        # Report what was found
        Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "The $Namespace namespace does not exist."
        Write-Host "Creating the $Namespace namespace in the $Location region..."
        New-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
        Write-Host "The $Namespace namespace in Resource Group $ResGrpName in the $Location region has been successfully created."
    }
    ```

## <a name="create-an-event-hub"></a><span data-ttu-id="2fb01-129">이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="2fb01-129">Create an event hub</span></span>

<span data-ttu-id="2fb01-130">이벤트 허브를 만들려면 이전 섹션의 스크립트를 사용하여 네임스페이스 확인을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb01-130">To create an event hub, perform a namespace check using the script in the previous section.</span></span> <span data-ttu-id="2fb01-131">그런 다음, [New-AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) cmdlet을 사용하여 이벤트 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2fb01-131">Then, use the [New-AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) cmdlet to create the event hub:</span></span>

```powershell
# Check if event hub already exists
$CurrentEH = Get-AzureRMEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName

if($CurrentEH)
{
    Write-Host "The event hub $EventHubName already exists in the $Location region:"
    # Report what was found
    Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "The $EventHubName event hub does not exist."
    Write-Host "Creating the $EventHubName event hub in the $Location region..."
    New-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -Location $Location -MessageRetentionInDays 3
    $CurrentEH = Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "The $EventHubName event hub in Resource Group $ResGrpName in the $Location region has been successfully created."
}
```

### <a name="create-a-consumer-group"></a><span data-ttu-id="2fb01-132">소비자 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="2fb01-132">Create a consumer group</span></span>

<span data-ttu-id="2fb01-133">이벤트 허브 내에 소비자 그룹을 만들려면 이전 섹션의 스크립트를 사용하여 네임스페이스 및 이벤트 허브 확인을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2fb01-133">To create a consumer group within an event hub, perform the namespace and event hub checks using the scripts in the previous section.</span></span> <span data-ttu-id="2fb01-134">그런 다음, [New-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) cmdlet을 사용하여 이벤트 허브 내에 소비자 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2fb01-134">Then, use the [New-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) cmdlet to create the consumer group within the event hub.</span></span> <span data-ttu-id="2fb01-135">예:</span><span class="sxs-lookup"><span data-stu-id="2fb01-135">For example:</span></span>

```powershell
# Check if consumer group already exists
$CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -ErrorAction Ignore

if($CurrentCG)
{
    Write-Host "The consumer group $ConsumerGroupName in event hub $EventHubName already exists in the $Location region:"
    # Report what was found
    Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "The $ConsumerGroupName consumer group does not exist."
    Write-Host "Creating the $ConsumerGroupName consumer group in the $Location region..."
    New-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
    $CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "The $ConsumerGroupName consumer group in event hub $EventHubName in Resource Group $ResGrpName in the $Location region has been successfully created."
}
```

#### <a name="set-user-metadata"></a><span data-ttu-id="2fb01-136">사용자 메타데이터 설정</span><span class="sxs-lookup"><span data-stu-id="2fb01-136">Set user metadata</span></span>

<span data-ttu-id="2fb01-137">이전 섹션의 스크립트를 실행한 후 [Set-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) cmdlet을 사용하여 다음 예제와 같이 소비자 그룹의 속성을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fb01-137">After executing the scripts in the preceding sections, you can use the [Set-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) cmdlet to update the properties of a consumer group, as in the following example:</span></span>

```powershell
# Set some user metadata on the CG
Write-Host "Setting the UserMetadata field to 'Testing'"
Set-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -UserMetadata "Testing"
# Show result
Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
```

## <a name="remove-event-hub"></a><span data-ttu-id="2fb01-138">이벤트 허브 제거</span><span class="sxs-lookup"><span data-stu-id="2fb01-138">Remove event hub</span></span>

<span data-ttu-id="2fb01-139">만든 이벤트 허브를 제거하려면 다음 예제와 같이 `Remove-*` cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fb01-139">To remove the event hubs you created, you can use the `Remove-*` cmdlets, as in the following example:</span></span>

```powershell
# Clean up
Remove-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
Remove-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
Remove-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
```

## <a name="next-steps"></a><span data-ttu-id="2fb01-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2fb01-140">Next steps</span></span>

- <span data-ttu-id="2fb01-141">[여기](/powershell/module/azurerm.eventhub)에서 전체 Event Hubs Resource Manager PowerShell 모듈 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fb01-141">See the complete Event Hubs Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.eventhub).</span></span> <span data-ttu-id="2fb01-142">이 페이지에는 사용 가능한 모든 cmdlet이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fb01-142">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="2fb01-143">Azure Resource Manager 템플릿 사용에 대한 자세한 내용은 문서 [Azure Resource Manager 템플릿을 사용하여 이벤트 허브 및 소비자 그룹이 있는 Event Hubs 네임스페이스 만들기](event-hubs-resource-manager-namespace-event-hub.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fb01-143">For information about using Azure Resource Manager templates, see the article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>
- <span data-ttu-id="2fb01-144">[Event Hubs .NET 관리 라이브러리](event-hubs-management-libraries.md)에 대한 정보</span><span class="sxs-lookup"><span data-stu-id="2fb01-144">Information about [Event Hubs .NET management libraries](event-hubs-management-libraries.md).</span></span>

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
