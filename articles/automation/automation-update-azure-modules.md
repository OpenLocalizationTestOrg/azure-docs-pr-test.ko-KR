---
title: "Azure Automation에서 Azure 모듈 업데이트 | Microsoft Docs"
description: "이 문서에서는 Azure Automation에 기본적으로 제공되는 일반 Azure PowerShell 모듈을 즉시 업데이트하는 방법을 설명합니다."
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2017
ms.author: magoedte
ms.openlocfilehash: ed8c97b642d406a05817ec6c67f31a1b4bce93b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-update-azure-powershell-modules-in-azure-automation"></a><span data-ttu-id="4346a-103">Azure Automation에서 Azure PowerShell 모듈을 업데이트하는 방법</span><span class="sxs-lookup"><span data-stu-id="4346a-103">How to update Azure PowerShell modules in Azure Automation</span></span>

<span data-ttu-id="4346a-104">기본적으로 각 Automation 계정에 가장 일반적인 Azure PowerShell 모듈이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4346a-104">The most common Azure PowerShell modules are provided by default in each Automation account.</span></span>  <span data-ttu-id="4346a-105">Azure 팀이 Azure 모듈을 정기적으로 업데이트하므로 포털에서 새 버전이 사용 가능하면 사용자가 계정에서 모듈을 업데이트할 수 있는 방법을 Automation 계정에 제공하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4346a-105">The Azure team updates the Azure modules regularly, so in the Automation account we provide a way for you to update the modules in the account when new versions are available from the portal.</span></span>  

<span data-ttu-id="4346a-106">제품 그룹에 의해 모듈이 정기적으로 업데이트되므로 매개 변수의 이름이 바뀌거나 cmdlet을 완전히 사용 중단하는 등 변경 유형에 따라 Runbook에 부정적인 영향을 미칠 수 있는 변경 사항이 포함된 cmdlet에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4346a-106">Because modules are updated regularly by the product group, changes can occur with the  included cmdlets, which may negatively impact your runbooks depending on the type of change, such as renaming a parameter or deprecating a cmdlet entirely.</span></span> <span data-ttu-id="4346a-107">자동화하는 프로세스 및 Runbook에 영향을 주지 않으려면 계속하기 전에 테스트 및 유효성 검사를 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4346a-107">To avoid impacting your runbooks and the processes they automate, it is strongly recommended that you test and validate before proceeding.</span></span>  <span data-ttu-id="4346a-108">이 용도의 전용 Automation 계정이 없는 경우 하나 만들어 PowerShell 모듈 업데이트와 같은 반복적인 변경 외에도 Runbook을 개발하는 동안 다양한 시나리오와 순열을 테스트하는 데 사용하는 것이 좋습니다</span><span class="sxs-lookup"><span data-stu-id="4346a-108">If you do not have a dedicated Automation account intended for this purpose, consider creating one so that you can test many different scenarios and permutations during the development of your runbooks, in addition to iterative changes such as updating the PowerShell modules.</span></span>  <span data-ttu-id="4346a-109">결과 유효성을 검사하고 필요한 변경 사항을 적용한 후에는 수정이 필요한 모든 Runbook의 마이그레이션 조정을 계속하고 프로덕션 환경에서 아래에 설명된 대로 업데이트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4346a-109">After the results are validated and you have applied any changes required, proceed with coordinating the migration of any runbooks that required modification and perform the update as described below in production.</span></span>     

## <a name="updating-azure-modules"></a><span data-ttu-id="4346a-110">Azure 모듈 업데이트</span><span class="sxs-lookup"><span data-stu-id="4346a-110">Updating Azure Modules</span></span>

1. <span data-ttu-id="4346a-111">Automation 계정의 모듈 계정 블레이드에는 **Azure 모듈 업데이트**라고 하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4346a-111">In the Modules blade of your Automation account there is an option called **Update Azure Modules**.</span></span>  <span data-ttu-id="4346a-112">이 옵션은 항상 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4346a-112">It is always enabled.</span></span><br><br> <span data-ttu-id="4346a-113">![모듈 블레이드의 Azure 모듈 업데이트 옵션](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span><span class="sxs-lookup"><span data-stu-id="4346a-113">![Update Azure Modules option in Modules blade](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span></span>

2. <span data-ttu-id="4346a-114">**Azure 모듈 업데이트**를 클릭하면 계속 진행할 것인지 묻는 확인 알림이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4346a-114">Click **Update Azure Modules** and you will be presented with a confirmation notification that asks you if you want to continue.</span></span><br><br> <span data-ttu-id="4346a-115">![Azure 모듈 업데이트 알림](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span><span class="sxs-lookup"><span data-stu-id="4346a-115">![Update Azure Modules notification](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span></span>

3. <span data-ttu-id="4346a-116">**예**를 클릭하면 모듈 업데이트 프로세스가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="4346a-116">Click **Yes** and the module update process will begin.</span></span>  <span data-ttu-id="4346a-117">업데이트 프로세스에서 다음 모듈을 업데이트하는 데 15-20분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="4346a-117">The update process takes about 15-20 minutes to update the following modules:</span></span>

  * <span data-ttu-id="4346a-118">Azure</span><span class="sxs-lookup"><span data-stu-id="4346a-118">Azure</span></span>
  * <span data-ttu-id="4346a-119">Azure.Storage</span><span class="sxs-lookup"><span data-stu-id="4346a-119">Azure.Storage</span></span>
  * <span data-ttu-id="4346a-120">AzureRm.Automation</span><span class="sxs-lookup"><span data-stu-id="4346a-120">AzureRm.Automation</span></span>
  * <span data-ttu-id="4346a-121">AzureRm.Compute</span><span class="sxs-lookup"><span data-stu-id="4346a-121">AzureRm.Compute</span></span>
  * <span data-ttu-id="4346a-122">AzureRm.Profile</span><span class="sxs-lookup"><span data-stu-id="4346a-122">AzureRm.Profile</span></span>
  * <span data-ttu-id="4346a-123">AzureRm.Resources</span><span class="sxs-lookup"><span data-stu-id="4346a-123">AzureRm.Resources</span></span>
  * <span data-ttu-id="4346a-124">AzureRm.Sql</span><span class="sxs-lookup"><span data-stu-id="4346a-124">AzureRm.Sql</span></span>
  * <span data-ttu-id="4346a-125">AzureRm.Storage</span><span class="sxs-lookup"><span data-stu-id="4346a-125">AzureRm.Storage</span></span>

    <span data-ttu-id="4346a-126">모듈이 이미 최신 상태이면 프로세스가 몇 초 안에 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="4346a-126">If the modules are already up to date, then the process will complete in a few seconds.</span></span>  <span data-ttu-id="4346a-127">업데이트 프로세스가 완료되면 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4346a-127">When the update process completes you will be notified.</span></span><br><br> ![Azure 모듈 업데이트 상태 업데이트](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> <span data-ttu-id="4346a-129">Azure Automation은 새로운 예약된 작업이 실행될 때 Automation 계정에서 최신 모듈을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4346a-129">Azure Automation will use the latest modules in your Automation account when a new scheduled job is run.</span></span>    

<span data-ttu-id="4346a-130">runbook에서 이러한 Azure PowerShell 모듈의 cmdlet을 사용하여 Azure 리소스를 관리하는 경우 최신 모듈을 사용하도록 매달 이 업데이트 프로세스를 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4346a-130">If you use cmdlets from these Azure PowerShell modules in your runbooks to manage Azure resources, then you will want to perform this update process every month or so to assure that you have the latest modules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4346a-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4346a-131">Next steps</span></span>

* <span data-ttu-id="4346a-132">통합 모듈에 대해 알아보고 Automation을 다른 시스템, 서비스 또는 솔루션과 통합하는 사용자 지정 모듈을 만드는 방법을 알아보려면 [통합 모듈](automation-integration-modules.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4346a-132">To learn more about Integration Modules and how to create custom modules to further integrate Automation with other systems, services, or solutions, see [Integration Modules](automation-integration-modules.md).</span></span>

* <span data-ttu-id="4346a-133">[GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) 또는 [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md)를 사용하여 Automation Runbook 및 구성 포트폴리오의 릴리스를 중앙에서 관리하고 제어하는 원본 제어 통합을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="4346a-133">Consider source control integration using [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) or [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) to centrally manage and control releases of your Automation runbook and configuration portfolio.</span></span>  