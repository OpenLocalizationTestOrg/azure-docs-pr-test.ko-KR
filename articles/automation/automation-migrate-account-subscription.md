---
title: "자동화 계정 및 리소스 마이그레이션 | Microsoft Docs"
description: "이 문서에서는 Azure 자동화의 자동화 계정 및 관련 리소스를 구독 간에 이동하는 방법을 설명합니다."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9c2db4a2-f324-48dc-8ce7-3343bf7230d5
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte
ms.openlocfilehash: 687da15bdaf854254321b59350f47549781676f5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-automation-account-and-resources"></a><span data-ttu-id="e986d-103">자동화 계정 및 리소스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="e986d-103">Migrate Automation Account and resources</span></span>
<span data-ttu-id="e986d-104">자동화 계정 및 연결된 된 리소스 (즉, 자산, runbook, 모듈 등)를 Azure 포털에서 만든 다른 또는 하나의 구독에서 다른 한 리소스 그룹에서 마이그레이션에 대해 손쉽게 수행할 수 있습니다 [리소스 이동](../azure-resource-manager/resource-group-move-resources.md) Azure Portal에서 사용할 수 있는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="e986d-104">For Automation accounts and its associated resources (i.e. assets, runbooks, modules, etc.) that you have created in the Azure portal and want to migrate from one resource group to another or from one subscription to another, you can accomplish this easily with the [move resources](../azure-resource-manager/resource-group-move-resources.md) feature available in the Azure portal.</span></span> <span data-ttu-id="e986d-105">그러나 이 작업을 계속하기 전에 다음 [리소스를 이동하기 전의 검사 목록](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources)과 아래의 자동화 관련 목록을 검토해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e986d-105">However, before proceeding with this action, you should first review the following [checklist before moving resources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) and additionally, the list below specific to Automation.</span></span>   

1. <span data-ttu-id="e986d-106">대상 구독/리소스 그룹은 원본이 있는 동일한 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e986d-106">The destination subscription/resource group must be in same region as the source.</span></span>  <span data-ttu-id="e986d-107">즉, 자동화 계정을 여러 지역 간에 이동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e986d-107">Meaning, Automation accounts cannot be moved across regions.</span></span>
2. <span data-ttu-id="e986d-108">리소스(예: Runbook, 작업 등)를 이동할 때 원본 그룹과 대상 그룹은 작업 기간 동안 잠겨 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e986d-108">When moving resources (e.g. runbooks, jobs, etc.), both the source group and the target group are locked for the duration of the operation.</span></span> <span data-ttu-id="e986d-109">쓰기 및 삭제 작업은 이동이 완료될 때까지 그룹에서 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="e986d-109">Write and delete operations are blocked on the groups until the move completes.</span></span>  
3. <span data-ttu-id="e986d-110">기존 구독의 리소스 또는 구독 ID를 참조하는 모든 Runbook 또는 변수는 마이그레이션이 완료된 후에 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e986d-110">Any runbooks or variables which reference a resource or subscription ID from the existing subscription will need to be updated after migration is completed.</span></span>   

> [!NOTE]
> <span data-ttu-id="e986d-111">이 기능은 클래식 자동화 리소스 이동을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e986d-111">This feature does not support moving Classic automation resources.</span></span>
>
>

## <a name="to-move-the-automation-account-using-the-portal"></a><span data-ttu-id="e986d-112">포털을 사용하여 자동화 계정을 이동하려면</span><span class="sxs-lookup"><span data-stu-id="e986d-112">To move the Automation Account using the portal</span></span>
1. <span data-ttu-id="e986d-113">자동화 계정에서 블레이드 위쪽에 있는 **이동**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e986d-113">From your Automation account, click **Move** at the top of the blade.</span></span><br> <span data-ttu-id="e986d-114">![이동 옵션](media/automation-migrate-account-subscription/automation-menu-move.png)</span><span class="sxs-lookup"><span data-stu-id="e986d-114">![Move option](media/automation-migrate-account-subscription/automation-menu-move.png)</span></span><br>
2. <span data-ttu-id="e986d-115">**리소스 이동** 블레이드에는 자동화 계정 및 리소스 그룹 둘 다에 관련된 리소스가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e986d-115">On the **Move resources** blade, note that it presents resources related to both your Automation account and your resource group(s).</span></span>  <span data-ttu-id="e986d-116">드롭다운 목록에서 **구독** 및 **리소스 그룹**을 선택하거나 **새 리소스 그룹 만들기** 옵션을 선택한 후 제공된 필드에 새 리소스 그룹 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e986d-116">Select the **subscription** and **resource group** from the drop-down lists, or select the option **create a new resource group** and enter a new resource group name in the field provided.</span></span>  
3. <span data-ttu-id="e986d-117">검토한 후 *리소스를 이동한 후 새 리소스 ID를 사용하려면 도구 및 스크립트를 업데이트해야 한다는 사실을 이해*했음을 확인하는 확인란을 선택한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e986d-117">Review and select the checkbox to acknowledge you *understand tools and scripts will need to be updated to use new resource IDs after resources have been moved* and then click **OK**.</span></span><br> <span data-ttu-id="e986d-118">![리소스 이동 블레이드](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span><span class="sxs-lookup"><span data-stu-id="e986d-118">![Move Resources Blade](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span></span><br>   

<span data-ttu-id="e986d-119">이 작업을 완료하는 데는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e986d-119">This action will take several minutes to complete.</span></span>  <span data-ttu-id="e986d-120">**알림**에 유효성 검사 및 마이그레이션을 비롯한 각 작업의 상태와 최종 완료 시기가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e986d-120">In **Notifications**, you will be presented with a status of each action that takes place - validation, migration, and then finally when it is completed.</span></span>     

## <a name="to-move-the-automation-account-using-powershell"></a><span data-ttu-id="e986d-121">PowerShell을 사용하여 자동화 계정을 이동하려면</span><span class="sxs-lookup"><span data-stu-id="e986d-121">To move the Automation Account using PowerShell</span></span>
<span data-ttu-id="e986d-122">기존 자동화 리소스를 다른 리소스 그룹 또는 구독으로 이동하려면 **Get-AzureRmResource** cmdlet을 사용하여 특정 자동화 계정을 가져온 다음 **Move-AzureRmResource** cmdlet을 사용하여 이동을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e986d-122">To move existing Automation resources to another resource group or subscription, use the  **Get-AzureRmResource** cmdlet to get the specific Automation account and then **Move-AzureRmResource** cmdlet to perform the move.</span></span>

<span data-ttu-id="e986d-123">첫 번째 예제는 자동화 계정을 새 리소스 그룹으로 이동하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e986d-123">The first example shows how to move an Automation account to a new resource group.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

<span data-ttu-id="e986d-124">위의 코드 예제를 실행하면 이 작업을 수행할지 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e986d-124">After you execute the above code example, you will be prompted to verify you want to perform this action.</span></span>  <span data-ttu-id="e986d-125">**예** 를 클릭하고 스크립트가 진행되도록 허용하면 마이그레이션을 수행하는 동안 알림이 수신되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e986d-125">Once you click **Yes** and allow the script to proceed, you will not receive any notifications while it's performing the migration.</span></span>  

<span data-ttu-id="e986d-126">새 구독으로 이동하려면 *DestinationSubscriptionId* 매개 변수 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e986d-126">To move to a new subscription, include a value for the *DestinationSubscriptionId* parameter.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

<span data-ttu-id="e986d-127">앞의 예제에서와 마찬가지로 이동할지 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e986d-127">As with the previous example, you will be prompted to confirm the move.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="e986d-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e986d-128">Next steps</span></span>
* <span data-ttu-id="e986d-129">리소스를 새 리소스 그룹이나 구독으로 이동하는 방법에 대한 자세한 내용은 [새 리소스 그룹 또는 구독으로 리소스 이동](../azure-resource-manager/resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="e986d-129">For more information about moving resources to new resource group or subscription, see [Move  resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md)</span></span>
* <span data-ttu-id="e986d-130">Azure 자동화의 역할 기반 액세스 제어에 대한 자세한 내용은 [Azure 자동화에서 역할 기반 액세스 제어](automation-role-based-access-control.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e986d-130">For more information about Role-based Access Control in Azure Automation, refer to [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="e986d-131">구독을 관리하기 위한 PowerShell cmdlet에 대한 자세한 내용은 [Resource Manager에서 Azure PowerShell 사용](../azure-resource-manager/powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="e986d-131">To learn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="e986d-132">구독을 관리하기 위한 포털 기능에 대한 자세한 내용은 [Azure 포털을 사용하여 리소스 관리](../azure-resource-manager/resource-group-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e986d-132">To learn about portal features for managing your subscription, see [Using the Azure Portal to manage resources](../azure-resource-manager/resource-group-portal.md).</span></span>
