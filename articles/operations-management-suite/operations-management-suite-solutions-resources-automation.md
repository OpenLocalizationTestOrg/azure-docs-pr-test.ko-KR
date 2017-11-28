---
title: "OMS 솔루션의 aaaAzure 자동화 리소스 | Microsoft Docs"
description: "OMS의 솔루션에서 수집 하 고 모니터링 데이터를 처리 하는 등의 Azure 자동화 tooautomate 프로세스 runbook 일반적으로 포함 됩니다.  이 문서에서는 설명 방법을 tooinclude runbook 및 관련된 해당 리소스에는 솔루션입니다."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 5281462e-f480-4e5e-9c19-022f36dce76d
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 82a156f89bf77ce25e52e5e4596261ec07a24dae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-automation-resources-tooan-oms-management-solution-preview"></a><span data-ttu-id="3a59e-104">Azure 자동화 리소스 tooan OMS 관리 솔루션 (미리 보기) 추가</span><span class="sxs-lookup"><span data-stu-id="3a59e-104">Adding Azure Automation resources tooan OMS management solution (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="3a59e-105">현재 Preview로 제공되는 OMS의 사용자 지정 솔루션 만들기에 대한 예비 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="3a59e-106">아래에 설명 된 모든 스키마 주체 toochange입니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-106">Any schema described below is subject toochange.</span></span>   


<span data-ttu-id="3a59e-107">[OMS의 관리 솔루션](operations-management-suite-solutions.md) 수집 하 고 모니터링 데이터를 처리 하는 등의 Azure 자동화 tooautomate 프로세스에는 일반적으로 runbook을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-107">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include runbooks in Azure Automation tooautomate processes such as collecting and processing monitoring data.</span></span>  <span data-ttu-id="3a59e-108">또한 toorunbooks, 자동화 계정을 사용 하는 hello runbook hello 솔루션에서 지원 되는 일정 및 변수와 같은 자산을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-108">In addition toorunbooks, Automation accounts includes assets such as variables and schedules that support hello runbooks used in hello solution.</span></span>  <span data-ttu-id="3a59e-109">이 문서에서는 설명 방법을 tooinclude runbook 및 관련된 해당 리소스에는 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-109">This article describes how tooinclude runbooks and their related resources in a solution.</span></span>

> [!NOTE]
> <span data-ttu-id="3a59e-110">hello 샘플이이 문서에서 사용 하 여 매개 변수 및 필수 또는 일반적인 toomanagement 솔루션 중 하나에 설명 된 있는 변수 [Operations Management Suite (OMS)에서 관리 솔루션 만들기](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="3a59e-110">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="3a59e-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3a59e-111">Prerequisites</span></span>
<span data-ttu-id="3a59e-112">이 문서는 익숙한 이미 hello 다음 정보를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-112">This article assumes that you're already familiar with hello following information.</span></span>

- <span data-ttu-id="3a59e-113">어떻게 너무[관리 솔루션을 만들어](operations-management-suite-solutions-creating.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-113">How too[create a management solution](operations-management-suite-solutions-creating.md).</span></span>
- <span data-ttu-id="3a59e-114">hello의 구조는 [솔루션 파일](operations-management-suite-solutions-solution-file.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-114">hello structure of a [solution file](operations-management-suite-solutions-solution-file.md).</span></span>
- <span data-ttu-id="3a59e-115">어떻게 너무[리소스 관리자 템플릿을 작성](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="3a59e-115">How too[author Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>

## <a name="automation-account"></a><span data-ttu-id="3a59e-116">Automation 계정</span><span class="sxs-lookup"><span data-stu-id="3a59e-116">Automation account</span></span>
<span data-ttu-id="3a59e-117">Azure Automation의 모든 리소스는 [Automation 계정](../automation/automation-security-overview.md#automation-account-overview)에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-117">All resources in Azure Automation are contained in an [Automation account](../automation/automation-security-overview.md#automation-account-overview).</span></span>  <span data-ttu-id="3a59e-118">에 설명 된 대로 [OMS 작업 영역 및 자동화 계정](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello 자동화 계정 hello 관리 솔루션에 포함 되어 있지 않지만 hello 솔루션을 설치 하기 전에 존재 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-118">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello Automation account isn't included in hello management solution but must exist before hello solution is installed.</span></span>  <span data-ttu-id="3a59e-119">사용할 수 없으면 hello 솔루션 설치 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-119">If it isn't available, then hello solution install will fail.</span></span>

<span data-ttu-id="3a59e-120">각 자동화 리소스의 hello 이름에는 자동화 계정 hello 이름이 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-120">hello name of each Automation resource includes hello name of its Automation account.</span></span>  <span data-ttu-id="3a59e-121">Hello 사용 하 여 hello 솔루션에서 이렇게 **accountName** hello 다음 runbook 리소스의 예제에서와 같이 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-121">This is done in hello solution with hello **accountName** parameter as in hello following example of a runbook resource.</span></span>

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a><span data-ttu-id="3a59e-122">Runbook</span><span class="sxs-lookup"><span data-stu-id="3a59e-122">Runbooks</span></span>
<span data-ttu-id="3a59e-123">Hello 솔루션을 설치할 때 만들어질 수 있도록 hello 솔루션 파일에 hello 솔루션에서 사용 하는 모든 runbook을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-123">You should include any runbooks used by hello solution in hello solution file so that they're created when hello solution is installed.</span></span>  <span data-ttu-id="3a59e-124">Hello runbook tooa 공용 위치 솔루션을 설치 하는 모든 사용자가 액세스할 수 있는 게시 해야 하므로 하지만 hello 서식 파일에서 hello runbook의 hello 본문을 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-124">You cannot contain hello body of hello runbook in hello template though, so you should publish hello runbook tooa public location where it can be accessed by any user installing your solution.</span></span>

<span data-ttu-id="3a59e-125">[Azure 자동화 runbook](../automation/automation-runbook-types.md) 리소스 유형의 **Microsoft.Automation/automationAccounts/runbooks** 있고 hello 구조를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-125">[Azure Automation runbook](../automation/automation-runbook-types.md) resources have a type of **Microsoft.Automation/automationAccounts/runbooks** and have hello following structure.</span></span> <span data-ttu-id="3a59e-126">여기에 일반적인 변수 및 매개 변수 복사 하 고이 코드 조각은 솔루션 파일에 붙여 하 고 hello 매개 변수 이름을 변경할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-126">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
        "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
        "type": "Microsoft.Automation/automationAccounts/runbooks",
        "apiVersion": "[variables('AutomationApiVersion')]",
        "dependsOn": [
        ],
        "location": "[parameters('regionId')]",
        "tags": { },
        "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
                "uri": "[variables('Runbook').Uri]",
                "version": [variables('Runbook').Version]"
            }
        }
    }


<span data-ttu-id="3a59e-127">runbook에 대 한 hello 속성 hello 다음 표에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-127">hello properties for runbooks are described in hello following table.</span></span>

| <span data-ttu-id="3a59e-128">속성</span><span class="sxs-lookup"><span data-stu-id="3a59e-128">Property</span></span> | <span data-ttu-id="3a59e-129">설명</span><span class="sxs-lookup"><span data-stu-id="3a59e-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a59e-130">runbookType</span><span class="sxs-lookup"><span data-stu-id="3a59e-130">runbookType</span></span> |<span data-ttu-id="3a59e-131">Hello runbook의 hello 유형을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-131">Specifies hello types of hello runbook.</span></span> <br><br> <span data-ttu-id="3a59e-132">Script - PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="3a59e-132">Script - PowerShell script</span></span> <br><span data-ttu-id="3a59e-133">PowerShell - PowerShell 워크플로</span><span class="sxs-lookup"><span data-stu-id="3a59e-133">PowerShell - PowerShell workflow</span></span> <br> <span data-ttu-id="3a59e-134">GraphPowerShell - 그래픽 PowerShell 스크립트 runbook</span><span class="sxs-lookup"><span data-stu-id="3a59e-134">GraphPowerShell - Graphical PowerShell script runbook</span></span> <br> <span data-ttu-id="3a59e-135">GraphPowerShellWorkflow - 그래픽 PowerShell 워크플로 runbook</span><span class="sxs-lookup"><span data-stu-id="3a59e-135">GraphPowerShellWorkflow - Graphical PowerShell workflow runbook</span></span> |
| <span data-ttu-id="3a59e-136">logProgress</span><span class="sxs-lookup"><span data-stu-id="3a59e-136">logProgress</span></span> |<span data-ttu-id="3a59e-137">지정 하는지 여부를 [진행률 레코드](../automation/automation-runbook-output-and-messages.md) hello runbook에 대 한 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-137">Specifies whether [progress records](../automation/automation-runbook-output-and-messages.md) should be generated for hello runbook.</span></span> |
| <span data-ttu-id="3a59e-138">logVerbose</span><span class="sxs-lookup"><span data-stu-id="3a59e-138">logVerbose</span></span> |<span data-ttu-id="3a59e-139">지정 하는지 여부를 [상세 레코드](../automation/automation-runbook-output-and-messages.md) hello runbook에 대 한 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-139">Specifies whether [verbose records](../automation/automation-runbook-output-and-messages.md) should be generated for hello runbook.</span></span> |
| <span data-ttu-id="3a59e-140">설명</span><span class="sxs-lookup"><span data-stu-id="3a59e-140">description</span></span> |<span data-ttu-id="3a59e-141">Hello runbook에 대 한 선택적 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-141">Optional description for hello runbook.</span></span> |
| <span data-ttu-id="3a59e-142">publishContentLink</span><span class="sxs-lookup"><span data-stu-id="3a59e-142">publishContentLink</span></span> |<span data-ttu-id="3a59e-143">Hello runbook의 hello 콘텐츠를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-143">Specifies hello content of hello runbook.</span></span> <br><br><span data-ttu-id="3a59e-144">uri-hello runbook의 Uri toohello 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-144">uri - Uri toohello content of hello runbook.</span></span>  <span data-ttu-id="3a59e-145">이 URL은 PowerShell 및 Script runbook의 경우 .ps1 파일이 되고 그래프 runbook의 경우 내보낸 그래픽 runbook 파일이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-145">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="3a59e-146">버전-고유한 추적에 대 한 hello runbook의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-146">version - Version of hello runbook for your own tracking.</span></span> |


## <a name="automation-jobs"></a><span data-ttu-id="3a59e-147">Automation 작업</span><span class="sxs-lookup"><span data-stu-id="3a59e-147">Automation jobs</span></span>
<span data-ttu-id="3a59e-148">Azure Automation에서 Runbook을 시작하면 자동화 작업이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-148">When you start a runbook in Azure Automation, it creates an automation job.</span></span>  <span data-ttu-id="3a59e-149">Hello 관리 솔루션을 설치할 때 runbook 자동화 작업 리소스 tooyour 솔루션 tooautomatically 시작을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-149">You can add an automation job resource tooyour solution tooautomatically start a runbook when hello management solution is installed.</span></span>  <span data-ttu-id="3a59e-150">이 방법은 hello 솔루션의 초기 구성에 사용 되는 일반적으로 사용 되는 toostart runbook에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-150">This method is typically used toostart runbooks that are used for initial configuration of hello solution.</span></span>  <span data-ttu-id="3a59e-151">toostart 정기적으로 runbook 만들기는 [일정](#schedules) 및 [작업 일정](#job-schedules)</span><span class="sxs-lookup"><span data-stu-id="3a59e-151">toostart a runbook at regular intervals, create a [schedule](#schedules) and a [job schedule](#job-schedules)</span></span>

<span data-ttu-id="3a59e-152">작업 리소스에는 형식이 **Microsoft.Automation/automationAccounts/jobs** 있고 hello 구조를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-152">Job resources have a type of **Microsoft.Automation/automationAccounts/jobs** and have hello following structure.</span></span>  <span data-ttu-id="3a59e-153">여기에 일반적인 변수 및 매개 변수 복사 하 고이 코드 조각은 솔루션 파일에 붙여 하 고 hello 매개 변수 이름을 변경할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-153">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', parameters('Runbook').JobGuid)]",
      "type": "Microsoft.Automation/automationAccounts/jobs",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
      ],
      "tags": { },
      "properties": {
        "runbook": {
          "name": "[variables('Runbook').Name]"
        },
        "parameters": {
          "Parameter1": "[[variables('Runbook').Parameter1]",
          "Parameter2": "[[variables('Runbook').Parameter2]"
        }
      }
    }

<span data-ttu-id="3a59e-154">다음 표에 hello 자동화 작업에 대 한 hello 속성 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-154">hello properties for automation jobs are described in hello following table.</span></span>

| <span data-ttu-id="3a59e-155">속성</span><span class="sxs-lookup"><span data-stu-id="3a59e-155">Property</span></span> | <span data-ttu-id="3a59e-156">설명</span><span class="sxs-lookup"><span data-stu-id="3a59e-156">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a59e-157">runbook</span><span class="sxs-lookup"><span data-stu-id="3a59e-157">runbook</span></span> |<span data-ttu-id="3a59e-158">Hello runbook toostart의 hello 이름의 단일 이름 엔터티.</span><span class="sxs-lookup"><span data-stu-id="3a59e-158">Single name entity with hello name of hello runbook toostart.</span></span> |
| <span data-ttu-id="3a59e-159">매개 변수</span><span class="sxs-lookup"><span data-stu-id="3a59e-159">parameters</span></span> |<span data-ttu-id="3a59e-160">Hello runbook에 필요한 각 매개 변수 값에 대 한 엔터티.</span><span class="sxs-lookup"><span data-stu-id="3a59e-160">Entity for each parameter value required by hello runbook.</span></span> |

<span data-ttu-id="3a59e-161">hello runbook 이름 및 toohello runbook 보낸 모든 매개 변수 값 toobe hello 작업에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-161">hello job includes hello runbook name and any parameter values toobe sent toohello runbook.</span></span>  <span data-ttu-id="3a59e-162">hello 작업 해야 [의존](operations-management-suite-solutions-solution-file.md#resources) hello runbook부터 시작 하는 hello runbook hello 작업 보다 먼저 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-162">hello job should [depend on](operations-management-suite-solutions-solution-file.md#resources) hello runbook that it's starting since hello runbook must be created before hello job.</span></span>  <span data-ttu-id="3a59e-163">시작해야 하는 Runbook이 여러 개 있는 경우 작업을 먼저 실행해야 하는 다른 작업에 종속되게 하여 순서를 정의 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-163">If you have multiple runbooks that should be started you can define their order by having a job depend on any other jobs that should be run first.</span></span>

<span data-ttu-id="3a59e-164">작업 리소스의 hello 이름 매개 변수를 통해 일반적으로 할당 된 GUID를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-164">hello name of a job resource must contain a GUID which is typically assigned by a parameter.</span></span>  <span data-ttu-id="3a59e-165">GUID 매개 변수에 대한 자세한 내용은 [OMS(Operations Management Suite)의 관리 솔루션 만들기](operations-management-suite-solutions-solution-file.md#parameters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a59e-165">You can read more about GUID parameters in [Creating solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span></span>  


## <a name="certificates"></a><span data-ttu-id="3a59e-166">인증서</span><span class="sxs-lookup"><span data-stu-id="3a59e-166">Certificates</span></span>
<span data-ttu-id="3a59e-167">[Azure 자동화 자격 증명](../automation/automation-certificates.md) 유형의 **Microsoft.Automation/automationAccounts/certificates** 있고 hello 구조를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-167">[Azure Automation certificates](../automation/automation-certificates.md) have a type of **Microsoft.Automation/automationAccounts/certificates** and have hello following structure.</span></span> <span data-ttu-id="3a59e-168">여기에 일반적인 변수 및 매개 변수 복사 하 고이 코드 조각은 솔루션 파일에 붙여 하 고 hello 매개 변수 이름을 변경할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-168">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
      "type": "Microsoft.Automation/automationAccounts/certificates",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "base64Value": "[variables('Certificate').Base64Value]",
        "thumbprint": "[variables('Certificate').Thumbprint]"
      }
    }



<span data-ttu-id="3a59e-169">다음 표에 hello 인증서 리소스에 대 한 hello 속성 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-169">hello properties for Certificates resources are described in hello following table.</span></span>

| <span data-ttu-id="3a59e-170">속성</span><span class="sxs-lookup"><span data-stu-id="3a59e-170">Property</span></span> | <span data-ttu-id="3a59e-171">설명</span><span class="sxs-lookup"><span data-stu-id="3a59e-171">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a59e-172">base64Value</span><span class="sxs-lookup"><span data-stu-id="3a59e-172">base64Value</span></span> |<span data-ttu-id="3a59e-173">Hello 인증서에 대 한 base 64 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-173">Base 64 value for hello certificate.</span></span> |
| <span data-ttu-id="3a59e-174">thumbprint</span><span class="sxs-lookup"><span data-stu-id="3a59e-174">thumbprint</span></span> |<span data-ttu-id="3a59e-175">Hello 인증서에 대 한 지문입니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-175">Thumbprint for hello certificate.</span></span> |



## <a name="credentials"></a><span data-ttu-id="3a59e-176">자격 증명</span><span class="sxs-lookup"><span data-stu-id="3a59e-176">Credentials</span></span>
<span data-ttu-id="3a59e-177">[Azure 자동화 자격 증명](../automation/automation-credentials.md) 유형의 **Microsoft.Automation/automationAccounts/credentials** 있고 hello 구조를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-177">[Azure Automation credentials](../automation/automation-credentials.md) have a type of **Microsoft.Automation/automationAccounts/credentials** and have hello following structure.</span></span>  <span data-ttu-id="3a59e-178">여기에 일반적인 변수 및 매개 변수 복사 하 고이 코드 조각은 솔루션 파일에 붙여 하 고 hello 매개 변수 이름을 변경할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-178">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 


    {
      "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
      "type": "Microsoft.Automation/automationAccounts/credentials",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "userName": "[parameters('credentialUsername')]",
        "password": "[parameters('credentialPassword')]"
      }
    }

<span data-ttu-id="3a59e-179">자격 증명 리소스에 대 한 hello 속성 hello 다음 표에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-179">hello properties for Credential resources are described in hello following table.</span></span>

| <span data-ttu-id="3a59e-180">속성</span><span class="sxs-lookup"><span data-stu-id="3a59e-180">Property</span></span> | <span data-ttu-id="3a59e-181">설명</span><span class="sxs-lookup"><span data-stu-id="3a59e-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a59e-182">userName</span><span class="sxs-lookup"><span data-stu-id="3a59e-182">userName</span></span> |<span data-ttu-id="3a59e-183">Hello 자격 증명에 대 한 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-183">User name for hello credential.</span></span> |
| <span data-ttu-id="3a59e-184">암호</span><span class="sxs-lookup"><span data-stu-id="3a59e-184">password</span></span> |<span data-ttu-id="3a59e-185">Hello 자격 증명에 대 한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-185">Password for hello credential.</span></span> |


## <a name="schedules"></a><span data-ttu-id="3a59e-186">일정</span><span class="sxs-lookup"><span data-stu-id="3a59e-186">Schedules</span></span>
<span data-ttu-id="3a59e-187">[Azure 자동화 일정](../automation/automation-schedules.md) 유형의 **Microsoft.Automation/automationAccounts/schedules** 있고 hello hello 구조를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-187">[Azure Automation schedules](../automation/automation-schedules.md) have a type of **Microsoft.Automation/automationAccounts/schedules** and have hello hello following structure.</span></span> <span data-ttu-id="3a59e-188">여기에 일반적인 변수 및 매개 변수 복사 하 고이 코드 조각은 솔루션 파일에 붙여 하 고 hello 매개 변수 이름을 변경할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-188">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
      "type": "microsoft.automation/automationAccounts/schedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Schedule').Description]",
        "startTime": "[parameters('scheduleStartTime')]",
        "timeZone": "[parameters('scheduleTimeZone')]",
        "isEnabled": "[variables('Schedule').IsEnabled]",
        "interval": "[variables('Schedule').Interval]",
        "frequency": "[variables('Schedule').Frequency]"
      }
    }

<span data-ttu-id="3a59e-189">다음 표에 hello 일정 리소스에 대 한 hello 속성 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-189">hello properties for schedule resources are described in hello following table.</span></span>

| <span data-ttu-id="3a59e-190">속성</span><span class="sxs-lookup"><span data-stu-id="3a59e-190">Property</span></span> | <span data-ttu-id="3a59e-191">설명</span><span class="sxs-lookup"><span data-stu-id="3a59e-191">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a59e-192">설명</span><span class="sxs-lookup"><span data-stu-id="3a59e-192">description</span></span> |<span data-ttu-id="3a59e-193">Hello 일정에 대 한 선택적 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-193">Optional description for hello schedule.</span></span> |
| <span data-ttu-id="3a59e-194">startTime</span><span class="sxs-lookup"><span data-stu-id="3a59e-194">startTime</span></span> |<span data-ttu-id="3a59e-195">일정의 hello 시작 시간을 DateTime 개체로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-195">Specifies hello start time of a schedule as a DateTime object.</span></span> <span data-ttu-id="3a59e-196">변환 된 tooa 수 있으면 문자열을 제공할 수 있습니다 유효한 날짜/시간입니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-196">A string can be provided if it can be converted tooa valid DateTime.</span></span> |
| <span data-ttu-id="3a59e-197">isEnabled</span><span class="sxs-lookup"><span data-stu-id="3a59e-197">isEnabled</span></span> |<span data-ttu-id="3a59e-198">Hello 일정이 사용 되는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-198">Specifies whether hello schedule is enabled.</span></span> |
| <span data-ttu-id="3a59e-199">interval</span><span class="sxs-lookup"><span data-stu-id="3a59e-199">interval</span></span> |<span data-ttu-id="3a59e-200">hello 형식 hello 일정에 대 한 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-200">hello type of interval for hello schedule.</span></span><br><br><span data-ttu-id="3a59e-201">일</span><span class="sxs-lookup"><span data-stu-id="3a59e-201">day</span></span><br><span data-ttu-id="3a59e-202">시간</span><span class="sxs-lookup"><span data-stu-id="3a59e-202">hour</span></span> |
| <span data-ttu-id="3a59e-203">frequency</span><span class="sxs-lookup"><span data-stu-id="3a59e-203">frequency</span></span> |<span data-ttu-id="3a59e-204">Hello 일정 빈도 (일) 또는 시간에 발생 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-204">Frequency that hello schedule should fire in number of days or hours.</span></span> |

<span data-ttu-id="3a59e-205">일정 시작 시간을 hello 보다 큰 값으로 현재 시간 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-205">Schedules must have a start time with a value greater than hello current time.</span></span>  <span data-ttu-id="3a59e-206">진행 중인 toobe 설치 되었을 때를 알 수 없습니다 없으므로 변수로이 값을 제공할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-206">You cannot provide this value with a variable since you would have no way of knowing when it's going toobe installed.</span></span>

<span data-ttu-id="3a59e-207">Hello 솔루션의 일정 리소스를 사용할 때 두 가지 전략을 다음 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-207">Use one of hello following two strategies when using schedule resources in a solution.</span></span>

- <span data-ttu-id="3a59e-208">Hello 일정의 시작 시간 hello에 대 한 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-208">Use a parameter for hello start time of hello schedule.</span></span>  <span data-ttu-id="3a59e-209">Hello 솔루션을 설치할 때이 라는 hello 사용자 tooprovide 값 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-209">This will prompt hello user tooprovide a value when they install hello solution.</span></span>  <span data-ttu-id="3a59e-210">일정이 여러 개 있는 경우 둘 이상의 일정에 단일 매개 변수 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-210">If you have multiple schedules, you could use a single parameter value for more than one of them.</span></span>
- <span data-ttu-id="3a59e-211">Hello 솔루션이 설치 될 때 시작 하는 runbook을 사용 하 여 hello 일정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-211">Create hello schedules using a runbook that starts when hello solution is installed.</span></span>  <span data-ttu-id="3a59e-212">이렇게 하면 한 번 하지만 포함할 수 없습니다 hello 사용자 toospecify의 hello 요구 사항이 제거 hello 일정 솔루션 hello 솔루션을 제거할 때 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-212">This removes hello requirement of hello user toospecify a time, but you can't contain hello schedule in your solution so it will be removed when hello solution is removed.</span></span>


### <a name="job-schedules"></a><span data-ttu-id="3a59e-213">작업 일정</span><span class="sxs-lookup"><span data-stu-id="3a59e-213">Job schedules</span></span>
<span data-ttu-id="3a59e-214">작업 일정 리소스는 Runbook과 일정을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-214">Job schedule resources link a runbook with a schedule.</span></span>  <span data-ttu-id="3a59e-215">형식이 **Microsoft.Automation/automationAccounts/jobSchedules** 있고 hello hello 구조를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-215">They have a type of **Microsoft.Automation/automationAccounts/jobSchedules** and have hello hello following structure.</span></span>  <span data-ttu-id="3a59e-216">여기에 일반적인 변수 및 매개 변수 복사 하 고이 코드 조각은 솔루션 파일에 붙여 하 고 hello 매개 변수 이름을 변경할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-216">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
      "type": "microsoft.automation/automationAccounts/jobSchedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
        "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
      ],
      "tags": {
      },
      "properties": {
        "schedule": {
          "name": "[variables('Schedule').Name]"
        },
        "runbook": {
          "name": "[variables('Runbook').Name]"
        }
      }
    }


<span data-ttu-id="3a59e-217">작업 일정에 대 한 hello 속성 hello 다음 표에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-217">hello properties for job schedules are described in hello following table.</span></span>

| <span data-ttu-id="3a59e-218">속성</span><span class="sxs-lookup"><span data-stu-id="3a59e-218">Property</span></span> | <span data-ttu-id="3a59e-219">설명</span><span class="sxs-lookup"><span data-stu-id="3a59e-219">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a59e-220">일정 이름</span><span class="sxs-lookup"><span data-stu-id="3a59e-220">schedule name</span></span> |<span data-ttu-id="3a59e-221">단일 **이름** hello 일정의 hello 이름의 엔터티가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-221">Single **name** entity with hello name of hello schedule.</span></span> |
| <span data-ttu-id="3a59e-222">Runbook 이름</span><span class="sxs-lookup"><span data-stu-id="3a59e-222">runbook name</span></span>  |<span data-ttu-id="3a59e-223">단일 **이름** hello runbook의 hello 이름의 엔터티가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-223">Single **name** entity with hello name of hello runbook.</span></span>  |



## <a name="variables"></a><span data-ttu-id="3a59e-224">variables</span><span class="sxs-lookup"><span data-stu-id="3a59e-224">Variables</span></span>
<span data-ttu-id="3a59e-225">[Azure 자동화 변수](../automation/automation-variables.md) 유형의 **Microsoft.Automation/automationAccounts/variables** 있고 hello 구조를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-225">[Azure Automation variables](../automation/automation-variables.md) have a type of **Microsoft.Automation/automationAccounts/variables** and have hello following structure.</span></span>  <span data-ttu-id="3a59e-226">여기에 일반적인 변수 및 매개 변수 복사 하 고이 코드 조각은 솔루션 파일에 붙여 하 고 hello 매개 변수 이름을 변경할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-226">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span>

    {
      "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
      "type": "microsoft.automation/automationAccounts/variables",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Variable').Description]",
        "isEncrypted": "[variables('Variable').Encrypted]",
        "type": "[variables('Variable').Type]",
        "value": "[variables('Variable').Value]"
      }
    }

<span data-ttu-id="3a59e-227">다음 표에 hello 변수 리소스에 대 한 hello 속성 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-227">hello properties for variable resources are described in hello following table.</span></span>

| <span data-ttu-id="3a59e-228">속성</span><span class="sxs-lookup"><span data-stu-id="3a59e-228">Property</span></span> | <span data-ttu-id="3a59e-229">설명</span><span class="sxs-lookup"><span data-stu-id="3a59e-229">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a59e-230">설명</span><span class="sxs-lookup"><span data-stu-id="3a59e-230">description</span></span> | <span data-ttu-id="3a59e-231">Hello 변수에 대 한 선택적 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-231">Optional description for hello variable.</span></span> |
| <span data-ttu-id="3a59e-232">isEncrypted</span><span class="sxs-lookup"><span data-stu-id="3a59e-232">isEncrypted</span></span> | <span data-ttu-id="3a59e-233">Hello 변수를 암호화 해야 하는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-233">Specifies whether hello variable should be encrypted.</span></span> |
| <span data-ttu-id="3a59e-234">type</span><span class="sxs-lookup"><span data-stu-id="3a59e-234">type</span></span> | <span data-ttu-id="3a59e-235">이 속성은 현재 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-235">This property currently has no effect.</span></span>  <span data-ttu-id="3a59e-236">hello 변수의 데이터 형식은 hello hello 초기 값으로 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-236">hello data type of hello variable will be determined by hello initial value.</span></span> |
| <span data-ttu-id="3a59e-237">값</span><span class="sxs-lookup"><span data-stu-id="3a59e-237">value</span></span> | <span data-ttu-id="3a59e-238">Hello 변수에 대 한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-238">Value for hello variable.</span></span> |

> [!NOTE]
> <span data-ttu-id="3a59e-239">hello **형식** 현재 속성이 만들려는 hello 변수에 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-239">hello **type** property currently has no effect on hello variable being created.</span></span>  <span data-ttu-id="3a59e-240">hello 변수의 데이터 형식은 hello hello 값으로 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-240">hello data type for hello variable will be determined by hello value.</span></span>  

<span data-ttu-id="3a59e-241">Hello hello 변수의 초기 값을 설정 하는 경우에 hello 올바른 데이터 형식으로 구성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-241">If you set hello initial value for hello variable, it must be configured as hello correct data type.</span></span>  <span data-ttu-id="3a59e-242">다음 표에서 hello hello 서로 다른 데이터 형식을 허용 및 구문을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-242">hello following table provides hello different data types allowable and their syntax.</span></span>  <span data-ttu-id="3a59e-243">JSON 값이 예상된 tooalways 되었음을 참고 hello 따옴표 안에 특수 문자를 따옴표로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-243">Note that values in JSON are expected tooalways be enclosed in quotes with any special characters within hello quotes.</span></span>  <span data-ttu-id="3a59e-244">Hello 문자열 따옴표로로 문자열 값을 지정할 수는 예를 들어 (hello 이스케이프 문자를 사용 하 여 (\\)) 동안 하나의 집합만 따옴표는 숫자 값이 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-244">For example, a string value would be specified by quotes around hello string (using hello escape character (\\)) while a numeric value would be specified with one set of quotes.</span></span>

| <span data-ttu-id="3a59e-245">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="3a59e-245">Data type</span></span> | <span data-ttu-id="3a59e-246">설명</span><span class="sxs-lookup"><span data-stu-id="3a59e-246">Description</span></span> | <span data-ttu-id="3a59e-247">예제</span><span class="sxs-lookup"><span data-stu-id="3a59e-247">Example</span></span> | <span data-ttu-id="3a59e-248">너무 확인</span><span class="sxs-lookup"><span data-stu-id="3a59e-248">Resolves too</span></span>|
|:--|:--|:--|:--|
| <span data-ttu-id="3a59e-249">string</span><span class="sxs-lookup"><span data-stu-id="3a59e-249">string</span></span>   | <span data-ttu-id="3a59e-250">값을 큰따옴표로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-250">Enclose value in double quotes.</span></span>  | <span data-ttu-id="3a59e-251">"\"Hello world\""</span><span class="sxs-lookup"><span data-stu-id="3a59e-251">"\"Hello world\""</span></span> | <span data-ttu-id="3a59e-252">"Hello world"</span><span class="sxs-lookup"><span data-stu-id="3a59e-252">"Hello world"</span></span> |
| <span data-ttu-id="3a59e-253">numeric</span><span class="sxs-lookup"><span data-stu-id="3a59e-253">numeric</span></span>  | <span data-ttu-id="3a59e-254">작은따옴표가 있는 숫자 값</span><span class="sxs-lookup"><span data-stu-id="3a59e-254">Numeric value with single quotes.</span></span>| <span data-ttu-id="3a59e-255">"64"</span><span class="sxs-lookup"><span data-stu-id="3a59e-255">"64"</span></span> | <span data-ttu-id="3a59e-256">64</span><span class="sxs-lookup"><span data-stu-id="3a59e-256">64</span></span> |
| <span data-ttu-id="3a59e-257">부울</span><span class="sxs-lookup"><span data-stu-id="3a59e-257">boolean</span></span>  | <span data-ttu-id="3a59e-258">따옴표로 묶은 **true** 또는 **false**.</span><span class="sxs-lookup"><span data-stu-id="3a59e-258">**true** or **false** in quotes.</span></span>  <span data-ttu-id="3a59e-259">이 값은 소문자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-259">Note that this value must be lowercase.</span></span> | <span data-ttu-id="3a59e-260">"true"</span><span class="sxs-lookup"><span data-stu-id="3a59e-260">"true"</span></span> | <span data-ttu-id="3a59e-261">true</span><span class="sxs-lookup"><span data-stu-id="3a59e-261">true</span></span> |
| <span data-ttu-id="3a59e-262">Datetime</span><span class="sxs-lookup"><span data-stu-id="3a59e-262">datetime</span></span> | <span data-ttu-id="3a59e-263">직렬화된 날짜 값.</span><span class="sxs-lookup"><span data-stu-id="3a59e-263">Serialized date value.</span></span><br><span data-ttu-id="3a59e-264">특정 날짜에 대 한 PowerShell toogenerate hello Convertto-json cmdlet이이 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-264">You can use hello ConvertTo-Json cmdlet in PowerShell toogenerate this value for a particular date.</span></span><br><span data-ttu-id="3a59e-265">예제: get-date "5/24/2017 13:14:57" \\</span><span class="sxs-lookup"><span data-stu-id="3a59e-265">Example: get-date "5/24/2017 13:14:57" \\</span></span>| <span data-ttu-id="3a59e-266">ConvertTo-Json</span><span class="sxs-lookup"><span data-stu-id="3a59e-266">ConvertTo-Json</span></span> | <span data-ttu-id="3a59e-267">"\\/Date(1495656897378)\\/"</span><span class="sxs-lookup"><span data-stu-id="3a59e-267">"\\/Date(1495656897378)\\/"</span></span> | <span data-ttu-id="3a59e-268">2017-05-24 13:14:57</span><span class="sxs-lookup"><span data-stu-id="3a59e-268">2017-05-24 13:14:57</span></span> |

## <a name="modules"></a><span data-ttu-id="3a59e-269">모듈</span><span class="sxs-lookup"><span data-stu-id="3a59e-269">Modules</span></span>
<span data-ttu-id="3a59e-270">관리 솔루션에 toodefine 않아도 [전역 모듈](../automation/automation-integration-modules.md) 가 항상 자동화 계정에서 사용할 수 있으므로 runbook으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-270">Your management solution does not need toodefine [global modules](../automation/automation-integration-modules.md) used by your runbooks because they will always be available in your Automation account.</span></span>  <span data-ttu-id="3a59e-271">Runbook에서 사용 하는 다른 모듈에 대 한 리소스 tooinclude가 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-271">You do need tooinclude a resource for any other module used by your runbooks.</span></span>

<span data-ttu-id="3a59e-272">[통합 모듈](../automation/automation-integration-modules.md) 유형의 **Microsoft.Automation/automationAccounts/modules** 있고 hello 구조를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-272">[Integration modules](../automation/automation-integration-modules.md) have a type of **Microsoft.Automation/automationAccounts/modules** and have hello following structure.</span></span>  <span data-ttu-id="3a59e-273">여기에 일반적인 변수 및 매개 변수 복사 하 고이 코드 조각은 솔루션 파일에 붙여 하 고 hello 매개 변수 이름을 변경할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-273">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span>

    {
      "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
      "type": "Microsoft.Automation/automationAccounts/modules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "dependsOn": [
      ],
      "properties": {
        "contentLink": {
          "uri": "[variables('Module').Uri]"
        }
      }
    }


<span data-ttu-id="3a59e-274">리소스 모듈에 대 한 hello 속성 hello 다음 표에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-274">hello properties for module resources are described in hello following table.</span></span>

| <span data-ttu-id="3a59e-275">속성</span><span class="sxs-lookup"><span data-stu-id="3a59e-275">Property</span></span> | <span data-ttu-id="3a59e-276">설명</span><span class="sxs-lookup"><span data-stu-id="3a59e-276">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a59e-277">contentLink</span><span class="sxs-lookup"><span data-stu-id="3a59e-277">contentLink</span></span> |<span data-ttu-id="3a59e-278">Hello 모듈의 hello 내용을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-278">Specifies hello content of hello module.</span></span> <br><br><span data-ttu-id="3a59e-279">uri-hello 모듈의 Uri toohello 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-279">uri - Uri toohello content of hello module.</span></span>  <span data-ttu-id="3a59e-280">이 URL은 PowerShell 및 Script runbook의 경우 .ps1 파일이 되고 그래프 runbook의 경우 내보낸 그래픽 runbook 파일이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-280">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="3a59e-281">버전-고유한 추적에 대 한 hello 모듈의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-281">version - Version of hello module for your own tracking.</span></span> |

<span data-ttu-id="3a59e-282">hello runbook hello runbook 하기 전에 만든 hello 모듈 리소스 tooensure에 의존 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-282">hello runbook should depend on hello module resource tooensure that it's created before hello runbook.</span></span>

### <a name="updating-modules"></a><span data-ttu-id="3a59e-283">모듈 업데이트</span><span class="sxs-lookup"><span data-stu-id="3a59e-283">Updating modules</span></span>
<span data-ttu-id="3a59e-284">일정을 사용 하는 runbook을 포함 하는 관리 솔루션을 업데이트 하는 경우 솔루션의 hello 새 버전에 해당 runbook에서 사용 하는 새 모듈 hello 이전 버전의 hello 모듈이 hello runbook에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-284">If you update a management solution that includes a runbook that uses a schedule, and hello new version of your solution has a new module used by that runbook, then hello runbook may use hello old version of hello module.</span></span>  <span data-ttu-id="3a59e-285">Hello runbook 솔루션에서 다음을 포함 하 고 만들 작업 toorun 해야 다른 runbook 하기 전에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-285">You should include hello following runbooks in your solution and create a job toorun them before any other runbooks.</span></span>  <span data-ttu-id="3a59e-286">이렇게 하면 모든 모듈을 runbook은 사용 하기 전에 필요한 hello로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-286">This will ensure that any modules are updated as required before hello runbooks are loaded.</span></span>

* <span data-ttu-id="3a59e-287">[업데이트 ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) 은 hello 최신 버전의 모든 솔루션에는 runbook에서 사용 하는 hello 모듈 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-287">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) will ensure that all of hello modules used by runbooks in your solution are hello latest version.</span></span>  
* <span data-ttu-id="3a59e-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) hello 일정 리소스 tooensure hello runbook을 사용 하 여 hello 최신 모듈로 toothem 연결 되어 있는 모든는 다시 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) will reregister all of hello schedule resources tooensure that hello runbooks linked toothem with use hello latest modules.</span></span>




## <a name="sample"></a><span data-ttu-id="3a59e-289">샘플</span><span class="sxs-lookup"><span data-stu-id="3a59e-289">Sample</span></span>
<span data-ttu-id="3a59e-290">다음은 hello 다음 리소스를 포함 하는 포함 하는 솔루션의 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-290">Following is a sample of a solution that include that includes hello following resources:</span></span>

- <span data-ttu-id="3a59e-291">Runbook -</span><span class="sxs-lookup"><span data-stu-id="3a59e-291">Runbook.</span></span>  <span data-ttu-id="3a59e-292">공용 GitHub 리포지토리에 저장된 샘플 Runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-292">This is a sample runbook stored in a public GitHub repository.</span></span>
- <span data-ttu-id="3a59e-293">Hello 솔루션을 설치할 때 hello runbook을 시작 하는 자동화 작업</span><span class="sxs-lookup"><span data-stu-id="3a59e-293">Automation job that starts hello runbook when hello solution is installed.</span></span>
- <span data-ttu-id="3a59e-294">일정 및 작업 일정 한 간격 toostart hello runbook을 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-294">Schedule and job schedule toostart hello runbook at regular intervals.</span></span>
- <span data-ttu-id="3a59e-295">인증서</span><span class="sxs-lookup"><span data-stu-id="3a59e-295">Certificate.</span></span>
- <span data-ttu-id="3a59e-296">자격 증명</span><span class="sxs-lookup"><span data-stu-id="3a59e-296">Credential.</span></span>
- <span data-ttu-id="3a59e-297">변수</span><span class="sxs-lookup"><span data-stu-id="3a59e-297">Variable.</span></span>
- <span data-ttu-id="3a59e-298">모듈 -</span><span class="sxs-lookup"><span data-stu-id="3a59e-298">Module.</span></span>  <span data-ttu-id="3a59e-299">이 hello [OMSIngestionAPI 모듈](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) 데이터 tooLog 분석을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-299">This is hello [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) for writing data tooLog Analytics.</span></span> 

<span data-ttu-id="3a59e-300">샘플 사용 하 여 hello [표준 솔루션 매개 변수](operations-management-suite-solutions-solution-file.md#parameters) 와 솔루션에 일반적으로 사용 되는 변수 hello 리소스 정의에서 toohardcoding 값을 반대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-300">hello sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed toohardcoding values in hello resource definitions.</span></span>


    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "workspaceName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Log Analytics workspace."
          }
        },
        "accountName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Automation account."
          }
        },
        "workspaceregionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Log Analytics workspace."
          }
        },
        "regionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Automation account."
          }
        },
        "pricingTier": {
          "type": "string",
          "metadata": {
            "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account."
          }
        },
        "certificateBase64Value": {
          "type": "string",
          "metadata": {
            "Description": "Base 64 value for certificate."
          }
        },
        "certificateThumbprint": {
          "type": "securestring",
          "metadata": {
            "Description": "Thumbprint for certificate."
          }
        },
        "credentialUsername": {
          "type": "string",
          "metadata": {
            "Description": "Username for credential."
          }
        },
        "credentialPassword": {
          "type": "securestring",
          "metadata": {
            "Description": "Password for credential."
          }
        },
        "scheduleStartTime": {
          "type": "string",
          "metadata": {
            "Description": "Start time for shedule."
          }
        },
        "scheduleTimeZone": {
          "type": "string",
          "metadata": {
            "Description": "Time zone for schedule."
          }
        },
        "scheduleLinkGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello schedule link toorunbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello runbook job.",
            "control": "guid"
          }
        }
      },
      "variables": {
        "SolutionName": "MySolution",
        "SolutionVersion": "1.0",
        "SolutionPublisher": "Contoso",
        "ProductName": "SampleSolution",
    
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31",
    
        "Runbook": {
          "Name": "MyRunbook",
          "Description": "Sample runbook",
          "Type": "PowerShell",
          "Uri": "https://raw.githubusercontent.com/user/myrepo/master/samples/MyRunbook.ps1",
          "JobGuid": "[parameters('runbookJobGuid')]"
        },
    
        "Certificate": {
          "Name": "MyCertificate",
          "Base64Value": "[parameters('certificateBase64Value')]",
          "Thumbprint": "[parameters('certificateThumbprint')]"
        },
    
        "Credential": {
          "Name": "MyCredential",
          "UserName": "[parameters('credentialUsername')]",
          "Password": "[parameters('credentialPassword')]"
        },
    
        "Schedule": {
          "Name": "MySchedule",
          "Description": "Sample schedule",
          "IsEnabled": "true",
          "Interval": "1",
          "Frequency": "hour",
          "StartTime": "[parameters('scheduleStartTime')]",
          "TimeZone": "[parameters('scheduleTimeZone')]",
          "LinkGuid": "[parameters('scheduleLinkGuid')]"
        },
    
        "Variable": {
          "Name": "MyVariable",
          "Description": "Sample variable",
          "Encrypted": 0,
          "Type": "string",
          "Value": "'This is my string value.'"
        },
    
        "Module": {
          "Name": "OMSIngestionAPI",
          "Uri": "https://devopsgallerystorage.blob.core.windows.net/packages/omsingestionapi.1.3.0.nupkg"
        }
      },
      "resources": [
        {
          "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
          "location": "[parameters('workspaceRegionId')]",
          "tags": { },
          "type": "Microsoft.OperationsManagement/solutions",
          "apiVersion": "[variables('LogAnalyticsApiVersion')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
            "referencedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
            ],
            "containedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]"
            ]
          },
          "plan": {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
            "Version": "[variables('SolutionVersion')]",
            "product": "[variables('ProductName')]",
            "publisher": "[variables('SolutionPublisher')]",
            "promotionCode": ""
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
          "type": "Microsoft.Automation/automationAccounts/runbooks",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "location": "[parameters('regionId')]",
          "tags": { },
          "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
              "uri": "[variables('Runbook').Uri]",
              "version": "1.0.0.0"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').JobGuid)]",
          "type": "Microsoft.Automation/automationAccounts/jobs",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
          ],
          "tags": { },
          "properties": {
            "runbook": {
              "name": "[variables('Runbook').Name]"
            },
            "parameters": {
              "targetSubscriptionId": "[subscription().subscriptionId]",
              "resourcegroup": "[resourceGroup().name]",
              "automationaccount": "[parameters('accountName')]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
          "type": "Microsoft.Automation/automationAccounts/certificates",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "Base64Value": "[variables('Certificate').Base64Value]",
            "Thumbprint": "[variables('Certificate').Thumbprint]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
          "type": "Microsoft.Automation/automationAccounts/credentials",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "userName": "[variables('Credential').UserName]",
            "password": "[variables('Credential').Password]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
          "type": "microsoft.automation/automationAccounts/schedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Schedule').Description]",
            "startTime": "[variables('Schedule').StartTime]",
            "timeZone": "[variables('Schedule').TimeZone]",
            "isEnabled": "[variables('Schedule').IsEnabled]",
            "interval": "[variables('Schedule').Interval]",
            "frequency": "[variables('Schedule').Frequency]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
          "type": "microsoft.automation/automationAccounts/jobSchedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
          ],
          "tags": {
          },
          "properties": {
            "schedule": {
              "name": "[variables('Schedule').Name]"
            },
            "runbook": {
              "name": "[variables('Runbook').Name]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
          "type": "microsoft.automation/automationAccounts/variables",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Variable').Description]",
            "isEncrypted": "[variables('Variable').Encrypted]",
            "type": "[variables('Variable').Type]",
            "value": "[variables('Variable').Value]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
          "type": "Microsoft.Automation/automationAccounts/modules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "properties": {
            "contentLink": {
              "uri": "[variables('Module').Uri]"
            }
          }
        }
    
      ],
      "outputs": { }
    }




## <a name="next-steps"></a><span data-ttu-id="3a59e-301">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3a59e-301">Next steps</span></span>
* <span data-ttu-id="3a59e-302">[보기 tooyour 솔루션 추가](operations-management-suite-solutions-resources-views.md) toovisualize 데이터를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a59e-302">[Add a view tooyour solution](operations-management-suite-solutions-resources-views.md) toovisualize collected data.</span></span>
