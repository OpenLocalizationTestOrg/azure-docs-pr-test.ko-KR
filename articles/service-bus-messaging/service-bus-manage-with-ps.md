---
title: "PowerShell을 사용한 Azure Service Bus 리소스 관리 | Microsoft Docs"
description: "PowerShell 모듈을 사용하여 Service Bus 리소스 만들기 및 관리"
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
ms.openlocfilehash: 1205f9fcabf5788c970fbce257aa5ad04f32cddc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-manage-service-bus-resources"></a><span data-ttu-id="894e3-103">PowerShell을 사용하여 Service Bus 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="894e3-103">Use PowerShell to manage Service Bus resources</span></span>

<span data-ttu-id="894e3-104">Microsoft Azure PowerShell은 Azure 서비스의 배포와 관리를 제어하고 자동화하는 데 사용할 수 있는 스크립팅 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="894e3-104">Microsoft Azure PowerShell is a scripting environment that you can use to control and automate the deployment and management of Azure services.</span></span> <span data-ttu-id="894e3-105">이 문서에서는 [Service Bus Resource Manager PowerShell 모듈](/powershell/module/azurerm.servicebus)을 사용하여 로컬 Azure PowerShell 콘솔 또는 스크립트를 통해 Service Bus 엔터티(네임스페이스, 쿼리, 토픽 및 구독)를 프로비전하고 관리하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="894e3-105">This article describes how to use the [Service Bus Resource Manager PowerShell module](/powershell/module/azurerm.servicebus) to provision and manage Service Bus entities (namespaces, queues, topics, and subscriptions) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="894e3-106">Azure Resource Manager 템플릿을 사용하여 Service Bus 엔터티를 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="894e3-106">You can also manage Service Bus entities using Azure Resource Manager templates.</span></span> <span data-ttu-id="894e3-107">자세한 내용은 [Azure Resource Manager 템플릿을 사용하여 서비스 버스 리소스를 만드는 방법](service-bus-resource-manager-overview.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="894e3-107">For more information, see the article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="894e3-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="894e3-108">Prerequisites</span></span>

<span data-ttu-id="894e3-109">이 작업을 수행하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="894e3-109">Before you begin, you'll need the following:</span></span>

* <span data-ttu-id="894e3-110">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="894e3-110">An Azure subscription.</span></span> <span data-ttu-id="894e3-111">구독을 얻는 방법에 대한 자세한 내용은 [구매 옵션][purchase options], [구성원 제공 항목][member offers] 또는 [무료 계정][free account]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="894e3-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="894e3-112">Azure PowerShell이 설치된 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="894e3-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="894e3-113">관련 지침은 [Azure PowerShell Cmdlet 시작](/powershell/azure/get-started-azureps)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="894e3-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="894e3-114">PowerShell 스크립트, NuGet 패키지 및 .NET Framework 전반에 대한 지식</span><span class="sxs-lookup"><span data-stu-id="894e3-114">A general understanding of PowerShell scripts, NuGet packages, and the .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="894e3-115">시작</span><span class="sxs-lookup"><span data-stu-id="894e3-115">Get started</span></span>

<span data-ttu-id="894e3-116">첫 번째 단계는 PowerShell을 사용하여 Azure 계정 및 Azure 구독에 로그인하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="894e3-116">The first step is to use PowerShell to log in to your Azure account and Azure subscription.</span></span> <span data-ttu-id="894e3-117">[Azure PowerShell cmdlet 시작](/powershell/azure/get-started-azureps)의 지침에 따라 Azure 계정에 로그인하고, Azure 구독에서 리소스를 검색하고 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="894e3-117">Follow the instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) to log in to your Azure account, and retrieve and access the resources in your Azure subscription.</span></span>

## <a name="provision-a-service-bus-namespace"></a><span data-ttu-id="894e3-118">서비스 버스 네임스페이스 프로비전</span><span class="sxs-lookup"><span data-stu-id="894e3-118">Provision a Service Bus namespace</span></span>

<span data-ttu-id="894e3-119">Service Bus 네임 페이스를 사용할 때 [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace) 및 [Set-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="894e3-119">When working with Service Bus namespaces, you can use the [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), and [Set-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlets.</span></span>

<span data-ttu-id="894e3-120">이 예제에서는 스크립트에 `$Namespace`과(와) `$Location`(이)라는 몇 가지 로컬 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="894e3-120">This example creates a few local variables in the script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="894e3-121">`$Namespace`은(는) 사용하려는 Service Bus 네임스페이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="894e3-121">`$Namespace` is the name of the Service Bus namespace with which we want to work.</span></span>
* <span data-ttu-id="894e3-122">`$Location`은(는) 네임스페이스를 프로비전할 데이터 센터를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="894e3-122">`$Location` identifies the data center in which will we provision the namespace.</span></span>
* <span data-ttu-id="894e3-123">`$CurrentNamespace`에는 검색하거나 만드는 참조 네임스페이스가 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="894e3-123">`$CurrentNamespace` stores the reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="894e3-124">실제 스크립트에서 `$Namespace` 및 `$Location`은(는) 매개 변수로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="894e3-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="894e3-125">스크립트의 이 부분은 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="894e3-125">This part of the script does the following:</span></span>

1. <span data-ttu-id="894e3-126">지정된 이름의 Service Bus 네임스페이스 검색을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="894e3-126">Attempts to retrieve a Service Bus namespace with the specified name.</span></span>
2. <span data-ttu-id="894e3-127">네임스페이스가 있으면 발견된 항목을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="894e3-127">If the namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="894e3-128">네임스페이스가 없으면 만든 다음 새로 만든 네임스페이스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="894e3-128">If the namespace is not found, it creates the namespace and then retrieves the newly created namespace.</span></span>
   
    ``` powershell
    # Query to see if the namespace currently exists
    $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
   
    # Check if the namespace already exists or needs to be created
    if ($CurrentNamespace)
    {
        Write-Host "The namespace $Namespace already exists in the $Location region:"
        # Report what was found
        Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "The $Namespace namespace does not exist."
        Write-Host "Creating the $Namespace namespace in the $Location region..."
        New-AzureRmServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
        Write-Host "The $Namespace namespace in Resource Group $ResGrpName in the $Location region has been successfully created."
                
    }
    ```

### <a name="create-a-namespace-authorization-rule"></a><span data-ttu-id="894e3-129">네임스페이스 권한 부여 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="894e3-129">Create a namespace authorization rule</span></span>

<span data-ttu-id="894e3-130">다음 예제에서는 [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule) 및 [Remove-AzureRmServiceBusNamespaceAuthorizationRule cmdlet](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule)을 사용하여 네임스페이스 권한 부여 규칙을 관리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="894e3-130">The following example shows how to manage namespace authorization rules using the [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), and [Remove-AzureRmServiceBusNamespaceAuthorizationRule cmdlets](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span></span>

```powershell
# Query to see if rule exists
$CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

# Check if the rule already exists or needs to be created
if ($CurrentRule)
{
    Write-Host "The $AuthRule rule already exists for the namespace $Namespace."
}
else
{
    Write-Host "The $AuthRule rule does not exist."
    Write-Host "Creating the $AuthRule rule for the $Namespace namespace..."
    New-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule -Rights @("Listen","Send")
    $CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
    Write-Host "The $AuthRule rule for the $Namespace namespace has been successfully created."

    Write-Host "Setting rights on the namespace"
    $authRuleObj = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

    Write-Host "Remove Send rights"
    $authRuleObj.Rights.Remove("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Add Send and Manage rights to the namespace"
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

## <a name="create-a-queue"></a><span data-ttu-id="894e3-131">큐 만들기</span><span class="sxs-lookup"><span data-stu-id="894e3-131">Create a queue</span></span>

<span data-ttu-id="894e3-132">큐 또는 토픽을 만들려면 이전 섹션에서와 같이 스크립트를 사용해서 네임스페이스를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="894e3-132">To create a queue or topic, perform a namespace check using the script in the previous section.</span></span> <span data-ttu-id="894e3-133">그런 후 큐를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="894e3-133">Then, create the queue:</span></span>

```powershell
# Check if queue already exists
$CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName

if($CurrentQ)
{
    Write-Host "The queue $QueueName already exists in the $Location region:"
}
else
{
    Write-Host "The $QueueName queue does not exist."
    Write-Host "Creating the $QueueName queue in the $Location region..."
    New-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -EnablePartitioning $True
    $CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName
    Write-Host "The $QueueName queue in Resource Group $ResGrpName in the $Location region has been successfully created."
}
```

### <a name="modify-queue-properties"></a><span data-ttu-id="894e3-134">큐 속성 수정</span><span class="sxs-lookup"><span data-stu-id="894e3-134">Modify queue properties</span></span>

<span data-ttu-id="894e3-135">이전 섹션의 스크립트를 실행한 후 [Set-AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) cmdlet을 사용하여 다음 예제와 같이 큐의 속성을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="894e3-135">After executing the script in the preceding section, you can use the [Set-AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) cmdlet to update the properties of a queue, as in the following example:</span></span>

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a><span data-ttu-id="894e3-136">다른 서비스 버스 엔터티 프로비전</span><span class="sxs-lookup"><span data-stu-id="894e3-136">Provisioning other Service Bus entities</span></span>

<span data-ttu-id="894e3-137">[Service Bus PowerShell 모듈](/powershell/module/azurerm.servicebus)을 사용하여 토픽 및 구독 같은 다른 엔터티를 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="894e3-137">You can use the [Service Bus PowerShell module](/powershell/module/azurerm.servicebus) to provision other entities, such as topics and subscriptions.</span></span> <span data-ttu-id="894e3-138">이러한 cmdlet은 이전 섹션에 설명된 큐 만들기 cmdlet과 구문상 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="894e3-138">These cmdlets are syntactically similar to the queue creation cmdlets demonstrated in the previous section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="894e3-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="894e3-139">Next steps</span></span>

- <span data-ttu-id="894e3-140">[여기](/powershell/module/azurerm.servicebus)에서 전체 Service Bus Resource Manager PowerShell 모듈 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="894e3-140">See the complete Service Bus Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.servicebus).</span></span> <span data-ttu-id="894e3-141">이 페이지에는 사용 가능한 모든 cmdlet이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="894e3-141">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="894e3-142">Azure Resource Manager 템플릿 사용에 대한 자세한 내용은 [Azure Resource Manager 템플릿을 사용하여 서비스 버스 리소스를 만드는 방법](service-bus-resource-manager-overview.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="894e3-142">For information about using Azure Resource Manager templates, see the article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>
- <span data-ttu-id="894e3-143">[Service Bus .NET 관리 라이브러리](service-bus-management-libraries.md)에 대한 정보</span><span class="sxs-lookup"><span data-stu-id="894e3-143">Information about [Service Bus .NET management libraries](service-bus-management-libraries.md).</span></span>

<span data-ttu-id="894e3-144">다음 블로그 게시물에 설명된 것처럼 Service Bus 엔터티를 관리하는 몇 가지 다른 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="894e3-144">There are some alternate ways to manage Service Bus entities, as described in these blog posts:</span></span>

* [<span data-ttu-id="894e3-145">PowerShell 스크립트를 사용하여 서비스 버스 큐, 토픽 및 구독을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="894e3-145">How to create Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="894e3-146">PowerShell 스크립트를 사용하여 서비스 버스 네임스페이스 및 이벤트 허브를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="894e3-146">How to create a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [<span data-ttu-id="894e3-147">Service Bus PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="894e3-147">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
