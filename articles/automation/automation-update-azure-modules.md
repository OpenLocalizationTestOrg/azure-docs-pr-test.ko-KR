---
title: "aaaUpdate Azure의 Azure 자동화 모듈 | Microsoft Docs"
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
ms.openlocfilehash: afa404a643349f044e55be2280e435b575049dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-azure-powershell-modules-in-azure-automation"></a><span data-ttu-id="651c6-103">어떻게 Azure 자동화에서 tooupdate Azure PowerShell 모듈</span><span class="sxs-lookup"><span data-stu-id="651c6-103">How tooupdate Azure PowerShell modules in Azure Automation</span></span>

<span data-ttu-id="651c6-104">hello 가장 일반적인 Azure PowerShell 모듈에서 각 자동화 계정은 기본적으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="651c6-104">hello most common Azure PowerShell modules are provided by default in each Automation account.</span></span>  <span data-ttu-id="651c6-105">Azure 모듈 hello 자동화 계정에서에서 우리는 방법을 제공 tooupdate hello 모듈 hello 계정에 새 버전 hello 포털에서 사용할 수 없는 경우 하므로 정기적으로 hello hello Azure 팀 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="651c6-105">hello Azure team updates hello Azure modules regularly, so in hello Automation account we provide a way for you tooupdate hello modules in hello account when new versions are available from hello portal.</span></span>  

<span data-ttu-id="651c6-106">모듈은 hello 제품 그룹에 의해 정기적으로 업데이트 하기 때문에 변경 내용을 변경 매개 변수 이름 바꾸기 또는 cmdlet을 완전히 사용 되지 않도록 지정 하는 등의 hello 형식에 따라 runbook에 부정적인 영향을 줄 수를 포함 하는 hello cmdlet과 함께 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="651c6-106">Because modules are updated regularly by hello product group, changes can occur with hello  included cmdlets, which may negatively impact your runbooks depending on hello type of change, such as renaming a parameter or deprecating a cmdlet entirely.</span></span> <span data-ttu-id="651c6-107">runbook과 hello에 영향을 주지 tooavoid 자동화 프로세스, 테스트 하 고 계속 하기 전에 유효성을 검사 하는 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="651c6-107">tooavoid impacting your runbooks and hello processes they automate, it is strongly recommended that you test and validate before proceeding.</span></span>  <span data-ttu-id="651c6-108">이 목적을 위한 전용된 자동화 계정이 없는 경우 hello hello를 업데이트 하는 등 추가 tooiterative 변경 내용에서 runbook 개발 하는 동안 다양 한 시나리오 및 순열을 테스트할 수 있도록 하나를 만들어 보십시오 PowerShell 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="651c6-108">If you do not have a dedicated Automation account intended for this purpose, consider creating one so that you can test many different scenarios and permutations during hello development of your runbooks, in addition tooiterative changes such as updating hello PowerShell modules.</span></span>  <span data-ttu-id="651c6-109">Hello 결과 유효성을 검사 하 고 필요한 변경 내용을 적용 한 후 필요한 수정 하는 모든 runbook의 hello 마이그레이션 조정 계속 되 고 프로덕션 환경에서 아래 설명 된 대로 hello 업데이트를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="651c6-109">After hello results are validated and you have applied any changes required, proceed with coordinating hello migration of any runbooks that required modification and perform hello update as described below in production.</span></span>     

## <a name="updating-azure-modules"></a><span data-ttu-id="651c6-110">Azure 모듈 업데이트</span><span class="sxs-lookup"><span data-stu-id="651c6-110">Updating Azure Modules</span></span>

1. <span data-ttu-id="651c6-111">Hello 모듈의 자동화 계정 블레이드는 이라는 옵션이 **업데이트 Azure 모듈**합니다.</span><span class="sxs-lookup"><span data-stu-id="651c6-111">In hello Modules blade of your Automation account there is an option called **Update Azure Modules**.</span></span>  <span data-ttu-id="651c6-112">이 옵션은 항상 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="651c6-112">It is always enabled.</span></span><br><br> <span data-ttu-id="651c6-113">![모듈 블레이드의 Azure 모듈 업데이트 옵션](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span><span class="sxs-lookup"><span data-stu-id="651c6-113">![Update Azure Modules option in Modules blade](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span></span>

2. <span data-ttu-id="651c6-114">클릭 **업데이트 Azure 모듈** toocontinue 원하면 묻는 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="651c6-114">Click **Update Azure Modules** and you will be presented with a confirmation notification that asks you if you want toocontinue.</span></span><br><br> <span data-ttu-id="651c6-115">![Azure 모듈 업데이트 알림](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span><span class="sxs-lookup"><span data-stu-id="651c6-115">![Update Azure Modules notification](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span></span>

3. <span data-ttu-id="651c6-116">클릭 **예** hello 모듈 업데이트 프로세스가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="651c6-116">Click **Yes** and hello module update process will begin.</span></span>  <span data-ttu-id="651c6-117">다음 모듈 15 20 분 tooupdate hello에 대 한 hello 업데이트 프로세스를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="651c6-117">hello update process takes about 15-20 minutes tooupdate hello following modules:</span></span>

  * <span data-ttu-id="651c6-118">Azure</span><span class="sxs-lookup"><span data-stu-id="651c6-118">Azure</span></span>
  * <span data-ttu-id="651c6-119">Azure.Storage</span><span class="sxs-lookup"><span data-stu-id="651c6-119">Azure.Storage</span></span>
  * <span data-ttu-id="651c6-120">AzureRm.Automation</span><span class="sxs-lookup"><span data-stu-id="651c6-120">AzureRm.Automation</span></span>
  * <span data-ttu-id="651c6-121">AzureRm.Compute</span><span class="sxs-lookup"><span data-stu-id="651c6-121">AzureRm.Compute</span></span>
  * <span data-ttu-id="651c6-122">AzureRm.Profile</span><span class="sxs-lookup"><span data-stu-id="651c6-122">AzureRm.Profile</span></span>
  * <span data-ttu-id="651c6-123">AzureRm.Resources</span><span class="sxs-lookup"><span data-stu-id="651c6-123">AzureRm.Resources</span></span>
  * <span data-ttu-id="651c6-124">AzureRm.Sql</span><span class="sxs-lookup"><span data-stu-id="651c6-124">AzureRm.Sql</span></span>
  * <span data-ttu-id="651c6-125">AzureRm.Storage</span><span class="sxs-lookup"><span data-stu-id="651c6-125">AzureRm.Storage</span></span>

    <span data-ttu-id="651c6-126">Hello 모듈 toodate 위로 이므로 hello 프로세스는 몇 초 안에 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="651c6-126">If hello modules are already up toodate, then hello process will complete in a few seconds.</span></span>  <span data-ttu-id="651c6-127">Hello 업데이트 프로세스가 완료 되 면 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="651c6-127">When hello update process completes you will be notified.</span></span><br><br> ![Azure 모듈 업데이트 상태 업데이트](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> <span data-ttu-id="651c6-129">Azure 자동화 새 예약 된 작업이 실행 될 때 자동화 계정에서 hello 최신 모듈을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="651c6-129">Azure Automation will use hello latest modules in your Automation account when a new scheduled job is run.</span></span>    

<span data-ttu-id="651c6-130">Cmdlet을 사용 하는 경우 프로그램 runbook toomanage Azure에서에서 이러한 Azure PowerShell 모듈에서 다음 리소스를 됩니다 tooperform이 업데이트 프로세스 매월 하거나 지금 적용 해야 tooassure hello 최신 모듈.</span><span class="sxs-lookup"><span data-stu-id="651c6-130">If you use cmdlets from these Azure PowerShell modules in your runbooks toomanage Azure resources, then you will want tooperform this update process every month or so tooassure that you have hello latest modules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="651c6-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="651c6-131">Next steps</span></span>

* <span data-ttu-id="651c6-132">통합 모듈 및 사용자 지정 모듈 toofurther toocreate 다른 시스템, 서비스 또는 솔루션을 자동화에 통합 하는 방법을 자세히 toolearn 참조 [통합 모듈](automation-integration-modules.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="651c6-132">toolearn more about Integration Modules and how toocreate custom modules toofurther integrate Automation with other systems, services, or solutions, see [Integration Modules](automation-integration-modules.md).</span></span>

* <span data-ttu-id="651c6-133">사용 하 여 소스 제어 통합 하는 것이 좋습니다. [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) 또는 [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally 관리 및 자동화 runbook 및 구성 포트폴리오 릴리스의 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="651c6-133">Consider source control integration using [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) or [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally manage and control releases of your Automation runbook and configuration portfolio.</span></span>  
