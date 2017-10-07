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
# <a name="use-powershell-toomanage-service-bus-resources"></a><span data-ttu-id="94acd-103">PowerShell toomanage 서비스 버스 리소스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="94acd-103">Use PowerShell toomanage Service Bus resources</span></span>

<span data-ttu-id="94acd-104">Microsoft Azure PowerShell은 toocontrol를 사용 하 고 Azure 서비스의 hello 배포 및 관리를 자동화할 수 있는 스크립팅 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="94acd-104">Microsoft Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of Azure services.</span></span> <span data-ttu-id="94acd-105">이 문서에서는 설명 방법을 toouse hello [서비스 버스 리소스 관리자 PowerShell 모듈](/powershell/module/azurerm.servicebus) tooprovision 서비스 버스 엔터티 (네임 스페이스, 큐, 토픽 및 구독) 하 고 관리 하는 로컬 Azure PowerShell 콘솔을 사용 하 여 또는 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="94acd-105">This article describes how toouse hello [Service Bus Resource Manager PowerShell module](/powershell/module/azurerm.servicebus) tooprovision and manage Service Bus entities (namespaces, queues, topics, and subscriptions) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="94acd-106">Azure Resource Manager 템플릿을 사용하여 Service Bus 엔터티를 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94acd-106">You can also manage Service Bus entities using Azure Resource Manager templates.</span></span> <span data-ttu-id="94acd-107">자세한 내용은 hello 문서 참조 [Azure 리소스 관리자 템플릿을 사용 하 여 서비스 버스 만들기 리소스](service-bus-resource-manager-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="94acd-107">For more information, see hello article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94acd-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="94acd-108">Prerequisites</span></span>

<span data-ttu-id="94acd-109">시작 하기 전에 hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="94acd-109">Before you begin, you'll need hello following:</span></span>

* <span data-ttu-id="94acd-110">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="94acd-110">An Azure subscription.</span></span> <span data-ttu-id="94acd-111">구독을 얻는 방법에 대한 자세한 내용은 [구매 옵션][purchase options], [구성원 제공 항목][member offers] 또는 [무료 계정][free account]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="94acd-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="94acd-112">Azure PowerShell이 설치된 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="94acd-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="94acd-113">관련 지침은 [Azure PowerShell Cmdlet 시작](/powershell/azure/get-started-azureps)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="94acd-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="94acd-114">PowerShell 스크립트, NuGet 패키지 및.NET Framework hello 일반 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94acd-114">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="94acd-115">시작</span><span class="sxs-lookup"><span data-stu-id="94acd-115">Get started</span></span>

<span data-ttu-id="94acd-116">hello 첫 단계는 tooyour Azure 계정에에서 PowerShell toolog toouse 및 Azure 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="94acd-116">hello first step is toouse PowerShell toolog in tooyour Azure account and Azure subscription.</span></span> <span data-ttu-id="94acd-117">Hello 지침에 따라 [Azure PowerShell cmdlet과 함께 시작](/powershell/azure/get-started-azureps) toolog tooyour Azure 계정 및 Azure 구독에서 hello 리소스를 검색 하 고 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="94acd-117">Follow hello instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) toolog in tooyour Azure account, and retrieve and access hello resources in your Azure subscription.</span></span>

## <a name="provision-a-service-bus-namespace"></a><span data-ttu-id="94acd-118">서비스 버스 네임스페이스 프로비전</span><span class="sxs-lookup"><span data-stu-id="94acd-118">Provision a Service Bus namespace</span></span>

<span data-ttu-id="94acd-119">서비스 버스 네임 스페이스를 사용할 때는 hello를 사용할 수 있습니다 [Get AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [새로 AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [제거-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), 및 [집합 AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="94acd-119">When working with Service Bus namespaces, you can use hello [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), and [Set-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlets.</span></span>

<span data-ttu-id="94acd-120">이 예에서는 hello 스크립트;에 몇 가지 지역 변수를 만듭니다. `$Namespace` 및 `$Location`합니다.</span><span class="sxs-lookup"><span data-stu-id="94acd-120">This example creates a few local variables in hello script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="94acd-121">`$Namespace`hello toowork는 원하는 hello 서비스 버스 네임 스페이스 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="94acd-121">`$Namespace` is hello name of hello Service Bus namespace with which we want toowork.</span></span>
* <span data-ttu-id="94acd-122">`$Location`hello 데이터 센터를 식별 했습니다 hello 네임 스페이스 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="94acd-122">`$Location` identifies hello data center in which will we provision hello namespace.</span></span>
* <span data-ttu-id="94acd-123">`$CurrentNamespace`에서는 검색 하거나이 작성 하는 hello 참조 네임 스페이스를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="94acd-123">`$CurrentNamespace` stores hello reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="94acd-124">실제 스크립트에서 `$Namespace` 및 `$Location`은(는) 매개 변수로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94acd-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="94acd-125">이 부분의 hello 스크립트는 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="94acd-125">This part of hello script does hello following:</span></span>

1. <span data-ttu-id="94acd-126">시도 tooretrieve hello로 서비스 버스 네임 스페이스 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="94acd-126">Attempts tooretrieve a Service Bus namespace with hello specified name.</span></span>
2. <span data-ttu-id="94acd-127">Hello 네임 스페이스가 있으면 발견 한를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="94acd-127">If hello namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="94acd-128">Hello 네임 스페이스 없으면 hello 네임 스페이스 만들고 hello 새로 생성 된 네임 스페이스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="94acd-128">If hello namespace is not found, it creates hello namespace and then retrieves hello newly created namespace.</span></span>
   
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

### <a name="create-a-namespace-authorization-rule"></a><span data-ttu-id="94acd-129">네임스페이스 권한 부여 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="94acd-129">Create a namespace authorization rule</span></span>

<span data-ttu-id="94acd-130">hello 다음 예제에서는 어떻게 toomanage 네임 스페이스 권한 부여 규칙을 사용 하 여 hello [새로 AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [집합 AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), 및 [제거 AzureRmServiceBusNamespaceAuthorizationRule cmdlet](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule)합니다.</span><span class="sxs-lookup"><span data-stu-id="94acd-130">hello following example shows how toomanage namespace authorization rules using hello [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), and [Remove-AzureRmServiceBusNamespaceAuthorizationRule cmdlets](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span></span>

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

## <a name="create-a-queue"></a><span data-ttu-id="94acd-131">큐 만들기</span><span class="sxs-lookup"><span data-stu-id="94acd-131">Create a queue</span></span>

<span data-ttu-id="94acd-132">toocreate 큐 나 항목에는 hello 스크립트를 사용 하 여 hello 이전 섹션에서 네임 스페이스 확인을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="94acd-132">toocreate a queue or topic, perform a namespace check using hello script in hello previous section.</span></span> <span data-ttu-id="94acd-133">그런 다음 hello 큐를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94acd-133">Then, create hello queue:</span></span>

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

### <a name="modify-queue-properties"></a><span data-ttu-id="94acd-134">큐 속성 수정</span><span class="sxs-lookup"><span data-stu-id="94acd-134">Modify queue properties</span></span>

<span data-ttu-id="94acd-135">Hello 섹션 앞의 hello 스크립트를 실행 한 후 hello를 사용할 수 있습니다 [집합 AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) hello 다음 예제와 같이 큐의 cmdlet tooupdate hello 속성:</span><span class="sxs-lookup"><span data-stu-id="94acd-135">After executing hello script in hello preceding section, you can use hello [Set-AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) cmdlet tooupdate hello properties of a queue, as in hello following example:</span></span>

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a><span data-ttu-id="94acd-136">다른 서비스 버스 엔터티 프로비전</span><span class="sxs-lookup"><span data-stu-id="94acd-136">Provisioning other Service Bus entities</span></span>

<span data-ttu-id="94acd-137">Hello를 사용할 수 있습니다 [서비스 버스 PowerShell 모듈](/powershell/module/azurerm.servicebus) tooprovision 항목 및 구독 같은 다른 엔터티에 합니다.</span><span class="sxs-lookup"><span data-stu-id="94acd-137">You can use hello [Service Bus PowerShell module](/powershell/module/azurerm.servicebus) tooprovision other entities, such as topics and subscriptions.</span></span> <span data-ttu-id="94acd-138">이러한 cmdlet은 유사한 구문상 toohello 큐 만들기 cmdlet hello 이전 단원에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="94acd-138">These cmdlets are syntactically similar toohello queue creation cmdlets demonstrated in hello previous section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94acd-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="94acd-139">Next steps</span></span>

- <span data-ttu-id="94acd-140">Hello 전체 서비스 버스 리소스 관리자 PowerShell 모듈 설명서를 참조 하십시오. [여기](/powershell/module/azurerm.servicebus)합니다.</span><span class="sxs-lookup"><span data-stu-id="94acd-140">See hello complete Service Bus Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.servicebus).</span></span> <span data-ttu-id="94acd-141">이 페이지에는 사용 가능한 모든 cmdlet이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="94acd-141">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="94acd-142">Azure 리소스 관리자 템플릿을 사용 하는 방법에 대 한 내용은 hello 문서 참조 [Azure 리소스 관리자 템플릿을 사용 하 여 서비스 버스 만들기 리소스](service-bus-resource-manager-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="94acd-142">For information about using Azure Resource Manager templates, see hello article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>
- <span data-ttu-id="94acd-143">[Service Bus .NET 관리 라이브러리](service-bus-management-libraries.md)에 대한 정보</span><span class="sxs-lookup"><span data-stu-id="94acd-143">Information about [Service Bus .NET management libraries](service-bus-management-libraries.md).</span></span>

<span data-ttu-id="94acd-144">몇 가지 다른 방식으로 toomanage 서비스 버스 엔터티 다음 블로그 게시물에 설명 된 대로</span><span class="sxs-lookup"><span data-stu-id="94acd-144">There are some alternate ways toomanage Service Bus entities, as described in these blog posts:</span></span>

* [<span data-ttu-id="94acd-145">어떻게 toocreate 서비스 버스 큐, 항목 및 PowerShell 스크립트를 사용 하 여 구독</span><span class="sxs-lookup"><span data-stu-id="94acd-145">How toocreate Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="94acd-146">어떻게 toocreate 서비스 버스 Namespace 및 PowerShell 스크립트를 사용 하 여 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="94acd-146">How toocreate a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [<span data-ttu-id="94acd-147">Service Bus PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="94acd-147">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
