---
title: "aaaMigrate 자동화 계정 및 리소스 | Microsoft Docs"
description: "이 문서에서는 어떻게 toomove 자동화 계정에 Azure 자동화와 연결 된 리소스가 하나의 구독만 tooanother에서 설명 합니다."
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
ms.openlocfilehash: 201c9091cd2d78d7ea407c1e5fb27f366bb4fa8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-automation-account-and-resources"></a><span data-ttu-id="46ab1-103">자동화 계정 및 리소스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="46ab1-103">Migrate Automation Account and resources</span></span>
<span data-ttu-id="46ab1-104">자동화 계정 및 연결된 된 리소스 (즉, 자산, runbook, 모듈, 등)를 hello Azure 포털에서에서 만든 하나의 리소스에서 toomigrate tooanother 그룹 또는 하나의 구독 tooanother에서이를 쉽게 수행할 수 있습니다. hello [리소스 이동](../azure-resource-manager/resource-group-move-resources.md) hello Azure 포털에서에서 사용할 수 있는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="46ab1-104">For Automation accounts and its associated resources (i.e. assets, runbooks, modules, etc.) that you have created in hello Azure portal and want toomigrate from one resource group tooanother or from one subscription tooanother, you can accomplish this easily with hello [move resources](../azure-resource-manager/resource-group-move-resources.md) feature available in hello Azure portal.</span></span> <span data-ttu-id="46ab1-105">그러나이 작업을 계속 하기 전에 먼저 검토 해야 hello 다음 [리소스를 이동 하기 전에 검사 목록](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) 및 특정 tooAutomation 아래 또한 hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="46ab1-105">However, before proceeding with this action, you should first review hello following [checklist before moving resources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) and additionally, hello list below specific tooAutomation.</span></span>   

1. <span data-ttu-id="46ab1-106">hello 대상 구독/리소스 그룹 hello 소스와 동일한 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46ab1-106">hello destination subscription/resource group must be in same region as hello source.</span></span>  <span data-ttu-id="46ab1-107">즉, 자동화 계정을 여러 지역 간에 이동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="46ab1-107">Meaning, Automation accounts cannot be moved across regions.</span></span>
2. <span data-ttu-id="46ab1-108">리소스 (예:: runbook, 작업, 등)를 이동할 때는 hello 소스 그룹과 hello 대상 그룹을 모두 hello hello 작업 동안 잠깁니다.</span><span class="sxs-lookup"><span data-stu-id="46ab1-108">When moving resources (e.g. runbooks, jobs, etc.), both hello source group and hello target group are locked for hello duration of hello operation.</span></span> <span data-ttu-id="46ab1-109">쓰기 및 삭제 작업 hello 이동이 완료 될 때까지 hello 그룹에서 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46ab1-109">Write and delete operations are blocked on hello groups until hello move completes.</span></span>  
3. <span data-ttu-id="46ab1-110">모든 runbook 또는 hello 기존 구독에서 리소스 또는 구독 ID를 참조할 수 있는 변수 toobe 마이그레이션이 완료 된 후에 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46ab1-110">Any runbooks or variables which reference a resource or subscription ID from hello existing subscription will need toobe updated after migration is completed.</span></span>   

> [!NOTE]
> <span data-ttu-id="46ab1-111">이 기능은 클래식 자동화 리소스 이동을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="46ab1-111">This feature does not support moving Classic automation resources.</span></span>
>
>

## <a name="toomove-hello-automation-account-using-hello-portal"></a><span data-ttu-id="46ab1-112">toomove hello hello 포털을 사용 하는 자동화 계정</span><span class="sxs-lookup"><span data-stu-id="46ab1-112">toomove hello Automation Account using hello portal</span></span>
1. <span data-ttu-id="46ab1-113">자동화 계정에서 클릭 **이동** hello hello 블레이드 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46ab1-113">From your Automation account, click **Move** at hello top of hello blade.</span></span><br> <span data-ttu-id="46ab1-114">![이동 옵션](media/automation-migrate-account-subscription/automation-menu-move.png)</span><span class="sxs-lookup"><span data-stu-id="46ab1-114">![Move option](media/automation-migrate-account-subscription/automation-menu-move.png)</span></span><br>
2. <span data-ttu-id="46ab1-115">Hello에 **리소스 이동** 블레이드, 자동화 계정 및 리소스 그룹 리소스 관련된 tooboth 제공 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="46ab1-115">On hello **Move resources** blade, note that it presents resources related tooboth your Automation account and your resource group(s).</span></span>  <span data-ttu-id="46ab1-116">선택 hello **구독** 및 **리소스 그룹** hello 드롭 다운 목록 또는 select hello 옵션에서 **새 리소스 그룹 만들기** 에 새 리소스 그룹 이름을 입력 하 고 hello 필드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="46ab1-116">Select hello **subscription** and **resource group** from hello drop-down lists, or select hello option **create a new resource group** and enter a new resource group name in hello field provided.</span></span>  
3. <span data-ttu-id="46ab1-117">검토 및 선택 hello 확인란 tooacknowledge 있습니다 *도구 및 스크립트는 이해 필요 업데이트 toobe toouse 새 리소스 Id는 리소스를 이동한 후* 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="46ab1-117">Review and select hello checkbox tooacknowledge you *understand tools and scripts will need toobe updated toouse new resource IDs after resources have been moved* and then click **OK**.</span></span><br> <span data-ttu-id="46ab1-118">![리소스 이동 블레이드](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span><span class="sxs-lookup"><span data-stu-id="46ab1-118">![Move Resources Blade](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span></span><br>   

<span data-ttu-id="46ab1-119">이 작업은 몇 분 toocomplete를 소요 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46ab1-119">This action will take several minutes toocomplete.</span></span>  <span data-ttu-id="46ab1-120">**알림**에 유효성 검사 및 마이그레이션을 비롯한 각 작업의 상태와 최종 완료 시기가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="46ab1-120">In **Notifications**, you will be presented with a status of each action that takes place - validation, migration, and then finally when it is completed.</span></span>     

## <a name="toomove-hello-automation-account-using-powershell"></a><span data-ttu-id="46ab1-121">toomove hello PowerShell을 사용 하는 자동화 계정</span><span class="sxs-lookup"><span data-stu-id="46ab1-121">toomove hello Automation Account using PowerShell</span></span>
<span data-ttu-id="46ab1-122">toomove 기존 자동화 리소스 tooanother 리소스 그룹이 나 hello를 사용 하 여 구독 **Get AzureRmResource** cmdlet tooget hello 특정 자동화 계정 차례로 **Move-azurermresource** cmdlet tooperform hello 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="46ab1-122">toomove existing Automation resources tooanother resource group or subscription, use hello  **Get-AzureRmResource** cmdlet tooget hello specific Automation account and then **Move-AzureRmResource** cmdlet tooperform hello move.</span></span>

<span data-ttu-id="46ab1-123">첫 번째 예에서는 hello toomove 자동화 tooa 새 리소스 그룹을 고려 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="46ab1-123">hello first example shows how toomove an Automation account tooa new resource group.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

<span data-ttu-id="46ab1-124">위 코드 예제는 hello를 실행 한 다음 메시지 표시 tooverify tooperform이이 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46ab1-124">After you execute hello above code example, you will be prompted tooverify you want tooperform this action.</span></span>  <span data-ttu-id="46ab1-125">클릭 한 후 **예** 허용 스크립트 tooproceed hello, hello 마이그레이션을 수행 하는 동안 모든 알림이 표시 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="46ab1-125">Once you click **Yes** and allow hello script tooproceed, you will not receive any notifications while it's performing hello migration.</span></span>  

<span data-ttu-id="46ab1-126">toomove tooa 새 구독을 hello에 대 한 값이 포함 *DestinationSubscriptionId* 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="46ab1-126">toomove tooa new subscription, include a value for hello *DestinationSubscriptionId* parameter.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

<span data-ttu-id="46ab1-127">Hello 앞의 예제에서와 마찬가지로 증명된 tooconfirm hello 이동 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46ab1-127">As with hello previous example, you will be prompted tooconfirm hello move.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="46ab1-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="46ab1-128">Next steps</span></span>
* <span data-ttu-id="46ab1-129">이동 리소스 toonew 리소스 그룹이 나 구독에 대 한 자세한 내용은 참조 [리소스 toonew 리소스 그룹이 나 구독 이동](../azure-resource-manager/resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="46ab1-129">For more information about moving resources toonew resource group or subscription, see [Move  resources toonew resource group or subscription](../azure-resource-manager/resource-group-move-resources.md)</span></span>
* <span data-ttu-id="46ab1-130">Azure 자동화에서 역할 기반 액세스 제어에 대 한 자세한 내용은 참조 너무[Azure 자동화에서 역할 기반 액세스 제어](automation-role-based-access-control.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="46ab1-130">For more information about Role-based Access Control in Azure Automation, refer too[Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="46ab1-131">구독을 관리 하기 위한 PowerShell cmdlet에 대 한 toolearn 참조 [Azure PowerShell 사용 하 여 리소스 관리자와](../azure-resource-manager/powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="46ab1-131">toolearn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="46ab1-132">구독을 관리 하기 위한 포털 기능에 대 한 toolearn 참조 [hello Azure 포털 toomanage 리소스를 사용 하 여](../azure-resource-manager/resource-group-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="46ab1-132">toolearn about portal features for managing your subscription, see [Using hello Azure Portal toomanage resources](../azure-resource-manager/resource-group-portal.md).</span></span>
