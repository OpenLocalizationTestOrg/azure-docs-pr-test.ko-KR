---
title: "OMS 솔루션의 Azure Automation 리소스 | Microsoft Docs"
description: "OMS의 솔루션에는 일반적으로 모니터링 데이터를 수집하고 처리하는 등의 프로세스를 자동화하기 위한 Azure Automation의 runbook이 포함됩니다.  이 문서에서는 솔루션에 runbook과 관련 리소스를 포함하는 방법을 설명합니다."
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
ms.openlocfilehash: c1909183a33ed03d8165671cff25cc8b83b77733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="adding-azure-automation-resources-to-an-oms-management-solution-preview"></a><span data-ttu-id="2e884-104">OMS 관리 솔루션에 Azure Automation 리소스 추가(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="2e884-104">Adding Azure Automation resources to an OMS management solution (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="2e884-105">현재 Preview로 제공되는 OMS의 사용자 지정 솔루션 만들기에 대한 예비 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="2e884-106">아래 설명된 스키마는 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-106">Any schema described below is subject to change.</span></span>   


<span data-ttu-id="2e884-107">[OMS의 관리 솔루션](operations-management-suite-solutions.md)에는 일반적으로 모니터링 데이터를 수집하고 처리하는 등의 프로세스를 자동화하기 위한 Azure Automation의 runbook이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-107">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include runbooks in Azure Automation to automate processes such as collecting and processing monitoring data.</span></span>  <span data-ttu-id="2e884-108">runbook 외에도 Automation 계정에는 솔루션에서 사용되는 runbook을 지원하는 변수, 일정 등의 자산이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-108">In addition to runbooks, Automation accounts includes assets such as variables and schedules that support the runbooks used in the solution.</span></span>  <span data-ttu-id="2e884-109">이 문서에서는 솔루션에 runbook과 관련 리소스를 포함하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-109">This article describes how to include runbooks and their related resources in a solution.</span></span>

> [!NOTE]
> <span data-ttu-id="2e884-110">이 문서의 샘플에는 관리 솔루션에 필요하거나 공통적이며 [OMS(Operations Management Suite)의 관리 솔루션 만들기](operations-management-suite-solutions-creating.md)에서 설명한 매개 변수와 변수가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-110">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="2e884-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2e884-111">Prerequisites</span></span>
<span data-ttu-id="2e884-112">이 문서에서는 이미 다음 정보에 대해 잘 알고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-112">This article assumes that you're already familiar with the following information.</span></span>

- <span data-ttu-id="2e884-113">방법: [관리 솔루션 만들기](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="2e884-113">How to [create a management solution](operations-management-suite-solutions-creating.md).</span></span>
- <span data-ttu-id="2e884-114">구조: [솔루션 파일](operations-management-suite-solutions-solution-file.md)</span><span class="sxs-lookup"><span data-stu-id="2e884-114">The structure of a [solution file](operations-management-suite-solutions-solution-file.md).</span></span>
- <span data-ttu-id="2e884-115">방법: [Resource Manager 템플릿 작성](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="2e884-115">How to [author Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>

## <a name="automation-account"></a><span data-ttu-id="2e884-116">Automation 계정</span><span class="sxs-lookup"><span data-stu-id="2e884-116">Automation account</span></span>
<span data-ttu-id="2e884-117">Azure Automation의 모든 리소스는 [Automation 계정](../automation/automation-security-overview.md#automation-account-overview)에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-117">All resources in Azure Automation are contained in an [Automation account](../automation/automation-security-overview.md#automation-account-overview).</span></span>  <span data-ttu-id="2e884-118">[OMS 작업 영역 및 Automation 계정](operations-management-suite-solutions.md#oms-workspace-and-automation-account)에서 설명한 대로 Automation 계정은 관리 솔루션에 포함되지 않지만, 솔루션이 설치되기 전에 존재해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-118">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) the Automation account isn't included in the management solution but must exist before the solution is installed.</span></span>  <span data-ttu-id="2e884-119">계정을 사용할 수 없으면 솔루션 설치에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-119">If it isn't available, then the solution install will fail.</span></span>

<span data-ttu-id="2e884-120">각 Automation 리소스의 이름에는 해당 Automation 계정의 이름이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-120">The name of each Automation resource includes the name of its Automation account.</span></span>  <span data-ttu-id="2e884-121">이 작업은 다음 runbook 리소스 예제와 같이 **accountName** 매개 변수가 포함된 솔루션에서 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-121">This is done in the solution with the **accountName** parameter as in the following example of a runbook resource.</span></span>

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a><span data-ttu-id="2e884-122">Runbook</span><span class="sxs-lookup"><span data-stu-id="2e884-122">Runbooks</span></span>
<span data-ttu-id="2e884-123">솔루션에서 사용되는 모든 Runbook을 솔루션 파일에 포함해야 솔루션을 설치할 때 이러한 Runbook이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-123">You should include any runbooks used by the solution in the solution file so that they're created when the solution is installed.</span></span>  <span data-ttu-id="2e884-124">하지만 Runbook 본문은 템플릿에 포함할 수 없으므로 솔루션을 설치하는 모든 사용자가 액세스할 수 있는 공용 위치에 해당 Runbook을 게시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-124">You cannot contain the body of the runbook in the template though, so you should publish the runbook to a public location where it can be accessed by any user installing your solution.</span></span>

<span data-ttu-id="2e884-125">[Azure Automation Runbook](../automation/automation-runbook-types.md) 리소스의 형식은 **Microsoft.Automation/automationAccounts/runbooks**이며, 다음과 같은 구조를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-125">[Azure Automation runbook](../automation/automation-runbook-types.md) resources have a type of **Microsoft.Automation/automationAccounts/runbooks** and have the following structure.</span></span> <span data-ttu-id="2e884-126">여기에는 일반 변수 및 매개 변수가 포함되어 있으므로 이 코드 조각을 복사하여 솔루션 파일에 붙여넣고 매개 변수 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-126">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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


<span data-ttu-id="2e884-127">Runbook의 속성은 다음 표에서 설명하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-127">The properties for runbooks are described in the following table.</span></span>

| <span data-ttu-id="2e884-128">속성</span><span class="sxs-lookup"><span data-stu-id="2e884-128">Property</span></span> | <span data-ttu-id="2e884-129">설명</span><span class="sxs-lookup"><span data-stu-id="2e884-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2e884-130">runbookType</span><span class="sxs-lookup"><span data-stu-id="2e884-130">runbookType</span></span> |<span data-ttu-id="2e884-131">runbook 유형을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-131">Specifies the types of the runbook.</span></span> <br><br> <span data-ttu-id="2e884-132">Script - PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="2e884-132">Script - PowerShell script</span></span> <br><span data-ttu-id="2e884-133">PowerShell - PowerShell 워크플로</span><span class="sxs-lookup"><span data-stu-id="2e884-133">PowerShell - PowerShell workflow</span></span> <br> <span data-ttu-id="2e884-134">GraphPowerShell - 그래픽 PowerShell 스크립트 runbook</span><span class="sxs-lookup"><span data-stu-id="2e884-134">GraphPowerShell - Graphical PowerShell script runbook</span></span> <br> <span data-ttu-id="2e884-135">GraphPowerShellWorkflow - 그래픽 PowerShell 워크플로 runbook</span><span class="sxs-lookup"><span data-stu-id="2e884-135">GraphPowerShellWorkflow - Graphical PowerShell workflow runbook</span></span> |
| <span data-ttu-id="2e884-136">logProgress</span><span class="sxs-lookup"><span data-stu-id="2e884-136">logProgress</span></span> |<span data-ttu-id="2e884-137">runbook에 대한 [진행률 레코드](../automation/automation-runbook-output-and-messages.md)를 생성해야 하는지 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-137">Specifies whether [progress records](../automation/automation-runbook-output-and-messages.md) should be generated for the runbook.</span></span> |
| <span data-ttu-id="2e884-138">logVerbose</span><span class="sxs-lookup"><span data-stu-id="2e884-138">logVerbose</span></span> |<span data-ttu-id="2e884-139">runbook에 대한 [세부 정보 레코드](../automation/automation-runbook-output-and-messages.md)를 생성해야 하는지 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-139">Specifies whether [verbose records](../automation/automation-runbook-output-and-messages.md) should be generated for the runbook.</span></span> |
| <span data-ttu-id="2e884-140">설명</span><span class="sxs-lookup"><span data-stu-id="2e884-140">description</span></span> |<span data-ttu-id="2e884-141">runbook에 대한 선택적 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-141">Optional description for the runbook.</span></span> |
| <span data-ttu-id="2e884-142">publishContentLink</span><span class="sxs-lookup"><span data-stu-id="2e884-142">publishContentLink</span></span> |<span data-ttu-id="2e884-143">runbook의 내용을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-143">Specifies the content of the runbook.</span></span> <br><br><span data-ttu-id="2e884-144">uri - runbook 내용의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-144">uri - Uri to the content of the runbook.</span></span>  <span data-ttu-id="2e884-145">이 URL은 PowerShell 및 Script runbook의 경우 .ps1 파일이 되고 그래프 runbook의 경우 내보낸 그래픽 runbook 파일이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-145">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="2e884-146">version - 자체적으로 추적하기 위한 runbook 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-146">version - Version of the runbook for your own tracking.</span></span> |


## <a name="automation-jobs"></a><span data-ttu-id="2e884-147">Automation 작업</span><span class="sxs-lookup"><span data-stu-id="2e884-147">Automation jobs</span></span>
<span data-ttu-id="2e884-148">Azure Automation에서 Runbook을 시작하면 자동화 작업이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-148">When you start a runbook in Azure Automation, it creates an automation job.</span></span>  <span data-ttu-id="2e884-149">솔루션에 자동화 작업 리소스를 추가하여 관리 솔루션이 설치될 때 자동으로 Runbook을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-149">You can add an automation job resource to your solution to automatically start a runbook when the management solution is installed.</span></span>  <span data-ttu-id="2e884-150">이 방법은 일반적으로 솔루션의 초기 구성에 사용되는 Runbook을 시작하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-150">This method is typically used to start runbooks that are used for initial configuration of the solution.</span></span>  <span data-ttu-id="2e884-151">일정한 간격으로 Runbook을 시작하려면 [일정](#schedules)과 [작업 일정](#job-schedules)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-151">To start a runbook at regular intervals, create a [schedule](#schedules) and a [job schedule](#job-schedules)</span></span>

<span data-ttu-id="2e884-152">작업 리소스의 형식은 **Microsoft.Automation/automationAccounts/jobs**이며, 다음과 같은 구조를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-152">Job resources have a type of **Microsoft.Automation/automationAccounts/jobs** and have the following structure.</span></span>  <span data-ttu-id="2e884-153">여기에는 일반 변수 및 매개 변수가 포함되어 있으므로 이 코드 조각을 복사하여 솔루션 파일에 붙여넣고 매개 변수 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-153">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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

<span data-ttu-id="2e884-154">자동화 작업의 속성은 다음 표에서 설명하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-154">The properties for automation jobs are described in the following table.</span></span>

| <span data-ttu-id="2e884-155">속성</span><span class="sxs-lookup"><span data-stu-id="2e884-155">Property</span></span> | <span data-ttu-id="2e884-156">설명</span><span class="sxs-lookup"><span data-stu-id="2e884-156">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2e884-157">runbook</span><span class="sxs-lookup"><span data-stu-id="2e884-157">runbook</span></span> |<span data-ttu-id="2e884-158">시작할 Runbook의 이름을 포함하는 단일 이름 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-158">Single name entity with the name of the runbook to start.</span></span> |
| <span data-ttu-id="2e884-159">매개 변수</span><span class="sxs-lookup"><span data-stu-id="2e884-159">parameters</span></span> |<span data-ttu-id="2e884-160">Runbook에 필요한 각 매개 변수 값의 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-160">Entity for each parameter value required by the runbook.</span></span> |

<span data-ttu-id="2e884-161">작업에는 runbook 이름과 runbook으로 전송되는 모든 매개 변수 값이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-161">The job includes the runbook name and any parameter values to be sent to the runbook.</span></span>  <span data-ttu-id="2e884-162">작업 전에 Runbook을 만들어야 하므로 작업은 시작하는 Runbook에 따라 [달라집니다](operations-management-suite-solutions-solution-file.md#resources).</span><span class="sxs-lookup"><span data-stu-id="2e884-162">The job should [depend on](operations-management-suite-solutions-solution-file.md#resources) the runbook that it's starting since the runbook must be created before the job.</span></span>  <span data-ttu-id="2e884-163">시작해야 하는 Runbook이 여러 개 있는 경우 작업을 먼저 실행해야 하는 다른 작업에 종속되게 하여 순서를 정의 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-163">If you have multiple runbooks that should be started you can define their order by having a job depend on any other jobs that should be run first.</span></span>

<span data-ttu-id="2e884-164">작업 리소스의 이름에는 보통 매개 변수를 통해 할당되는 GUID가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-164">The name of a job resource must contain a GUID which is typically assigned by a parameter.</span></span>  <span data-ttu-id="2e884-165">GUID 매개 변수에 대한 자세한 내용은 [OMS(Operations Management Suite)의 관리 솔루션 만들기](operations-management-suite-solutions-solution-file.md#parameters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e884-165">You can read more about GUID parameters in [Creating solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span></span>  


## <a name="certificates"></a><span data-ttu-id="2e884-166">인증서</span><span class="sxs-lookup"><span data-stu-id="2e884-166">Certificates</span></span>
<span data-ttu-id="2e884-167">[Azure Automation 인증서](../automation/automation-certificates.md)의 형식은 **Microsoft.Automation/automationAccounts/certificates**이며, 다음과 같은 구조를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-167">[Azure Automation certificates](../automation/automation-certificates.md) have a type of **Microsoft.Automation/automationAccounts/certificates** and have the following structure.</span></span> <span data-ttu-id="2e884-168">여기에는 일반 변수 및 매개 변수가 포함되어 있으므로 이 코드 조각을 복사하여 솔루션 파일에 붙여넣고 매개 변수 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-168">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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



<span data-ttu-id="2e884-169">인증서 리소스의 속성은 다음 표에서 설명하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-169">The properties for Certificates resources are described in the following table.</span></span>

| <span data-ttu-id="2e884-170">속성</span><span class="sxs-lookup"><span data-stu-id="2e884-170">Property</span></span> | <span data-ttu-id="2e884-171">설명</span><span class="sxs-lookup"><span data-stu-id="2e884-171">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2e884-172">base64Value</span><span class="sxs-lookup"><span data-stu-id="2e884-172">base64Value</span></span> |<span data-ttu-id="2e884-173">인증서에 대한 Base 64 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-173">Base 64 value for the certificate.</span></span> |
| <span data-ttu-id="2e884-174">thumbprint</span><span class="sxs-lookup"><span data-stu-id="2e884-174">thumbprint</span></span> |<span data-ttu-id="2e884-175">인증서의 지문입니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-175">Thumbprint for the certificate.</span></span> |



## <a name="credentials"></a><span data-ttu-id="2e884-176">자격 증명</span><span class="sxs-lookup"><span data-stu-id="2e884-176">Credentials</span></span>
<span data-ttu-id="2e884-177">[Azure Automation 자격 증명](../automation/automation-credentials.md)의 형식은 **Microsoft.Automation/automationAccounts/credentials**이며, 다음과 같은 구조를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-177">[Azure Automation credentials](../automation/automation-credentials.md) have a type of **Microsoft.Automation/automationAccounts/credentials** and have the following structure.</span></span>  <span data-ttu-id="2e884-178">여기에는 일반 변수 및 매개 변수가 포함되어 있으므로 이 코드 조각을 복사하여 솔루션 파일에 붙여넣고 매개 변수 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-178">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 


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

<span data-ttu-id="2e884-179">자격 증명 리소스의 속성은 다음 표에서 설명하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-179">The properties for Credential resources are described in the following table.</span></span>

| <span data-ttu-id="2e884-180">속성</span><span class="sxs-lookup"><span data-stu-id="2e884-180">Property</span></span> | <span data-ttu-id="2e884-181">설명</span><span class="sxs-lookup"><span data-stu-id="2e884-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2e884-182">userName</span><span class="sxs-lookup"><span data-stu-id="2e884-182">userName</span></span> |<span data-ttu-id="2e884-183">인증서의 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-183">User name for the credential.</span></span> |
| <span data-ttu-id="2e884-184">password</span><span class="sxs-lookup"><span data-stu-id="2e884-184">password</span></span> |<span data-ttu-id="2e884-185">인증서의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-185">Password for the credential.</span></span> |


## <a name="schedules"></a><span data-ttu-id="2e884-186">일정</span><span class="sxs-lookup"><span data-stu-id="2e884-186">Schedules</span></span>
<span data-ttu-id="2e884-187">[Azure Automation 일정](../automation/automation-schedules.md)의 형식은 **Microsoft.Automation/automationAccounts/schedules**이며, 다음과 같은 구조를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-187">[Azure Automation schedules](../automation/automation-schedules.md) have a type of **Microsoft.Automation/automationAccounts/schedules** and have the the following structure.</span></span> <span data-ttu-id="2e884-188">여기에는 일반 변수 및 매개 변수가 포함되어 있으므로 이 코드 조각을 복사하여 솔루션 파일에 붙여넣고 매개 변수 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-188">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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

<span data-ttu-id="2e884-189">일정 리소스의 속성은 다음 테이블에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-189">The properties for schedule resources are described in the following table.</span></span>

| <span data-ttu-id="2e884-190">속성</span><span class="sxs-lookup"><span data-stu-id="2e884-190">Property</span></span> | <span data-ttu-id="2e884-191">설명</span><span class="sxs-lookup"><span data-stu-id="2e884-191">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2e884-192">설명</span><span class="sxs-lookup"><span data-stu-id="2e884-192">description</span></span> |<span data-ttu-id="2e884-193">일정에 대한 선택적 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-193">Optional description for the schedule.</span></span> |
| <span data-ttu-id="2e884-194">startTime</span><span class="sxs-lookup"><span data-stu-id="2e884-194">startTime</span></span> |<span data-ttu-id="2e884-195">일정 시작 시간을 DateTime 개체로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-195">Specifies the start time of a schedule as a DateTime object.</span></span> <span data-ttu-id="2e884-196">적합한 DateTime으로 변환될 수 있는 경우 문자열을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-196">A string can be provided if it can be converted to a valid DateTime.</span></span> |
| <span data-ttu-id="2e884-197">isEnabled</span><span class="sxs-lookup"><span data-stu-id="2e884-197">isEnabled</span></span> |<span data-ttu-id="2e884-198">일정 사용 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-198">Specifies whether the schedule is enabled.</span></span> |
| <span data-ttu-id="2e884-199">interval</span><span class="sxs-lookup"><span data-stu-id="2e884-199">interval</span></span> |<span data-ttu-id="2e884-200">일정 간격의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-200">The type of interval for the schedule.</span></span><br><br><span data-ttu-id="2e884-201">일</span><span class="sxs-lookup"><span data-stu-id="2e884-201">day</span></span><br><span data-ttu-id="2e884-202">시간</span><span class="sxs-lookup"><span data-stu-id="2e884-202">hour</span></span> |
| <span data-ttu-id="2e884-203">frequency</span><span class="sxs-lookup"><span data-stu-id="2e884-203">frequency</span></span> |<span data-ttu-id="2e884-204">특정 기간(일 또는 시간) 내에 일정이 실행되는 빈도입니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-204">Frequency that the schedule should fire in number of days or hours.</span></span> |

<span data-ttu-id="2e884-205">일정에는 현재 시간보다 큰 값을 가진 시작 시간이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-205">Schedules must have a start time with a value greater than the current time.</span></span>  <span data-ttu-id="2e884-206">변수를 설치할 시기를 알 수 없으므로 해당 변수에 이 값을 제공할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-206">You cannot provide this value with a variable since you would have no way of knowing when it's going to be installed.</span></span>

<span data-ttu-id="2e884-207">솔루션에서 일정 리소스를 사용하는 경우 다음 두 가지 전략 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-207">Use one of the following two strategies when using schedule resources in a solution.</span></span>

- <span data-ttu-id="2e884-208">일정의 시작 시간에 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-208">Use a parameter for the start time of the schedule.</span></span>  <span data-ttu-id="2e884-209">이렇게 하면 솔루션을 설치할 때 사용자에게 값을 제공하도록 요구하는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-209">This will prompt the user to provide a value when they install the solution.</span></span>  <span data-ttu-id="2e884-210">일정이 여러 개 있는 경우 둘 이상의 일정에 단일 매개 변수 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-210">If you have multiple schedules, you could use a single parameter value for more than one of them.</span></span>
- <span data-ttu-id="2e884-211">솔루션을 설치할 때 시작되는 Runbook을 사용하여 일정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-211">Create the schedules using a runbook that starts when the solution is installed.</span></span>  <span data-ttu-id="2e884-212">이렇게 하면 사용자가 시간을 지정하지 않아도 되지만 솔루션에 일정을 포함할 수 없으므로 솔루션을 제거할 때 일정도 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-212">This removes the requirement of the user to specify a time, but you can't contain the schedule in your solution so it will be removed when the solution is removed.</span></span>


### <a name="job-schedules"></a><span data-ttu-id="2e884-213">작업 일정</span><span class="sxs-lookup"><span data-stu-id="2e884-213">Job schedules</span></span>
<span data-ttu-id="2e884-214">작업 일정 리소스는 Runbook과 일정을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-214">Job schedule resources link a runbook with a schedule.</span></span>  <span data-ttu-id="2e884-215">작업 일정 리소스의 형식은 **Microsoft.Automation/automationAccounts/jobSchedules**이며, 다음과 같은 구조를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-215">They have a type of **Microsoft.Automation/automationAccounts/jobSchedules** and have the the following structure.</span></span>  <span data-ttu-id="2e884-216">여기에는 일반 변수 및 매개 변수가 포함되어 있으므로 이 코드 조각을 복사하여 솔루션 파일에 붙여넣고 매개 변수 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-216">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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


<span data-ttu-id="2e884-217">작업 일정의 속성은 다음 표에서 설명하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-217">The properties for job schedules are described in the following table.</span></span>

| <span data-ttu-id="2e884-218">속성</span><span class="sxs-lookup"><span data-stu-id="2e884-218">Property</span></span> | <span data-ttu-id="2e884-219">설명</span><span class="sxs-lookup"><span data-stu-id="2e884-219">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2e884-220">일정 이름</span><span class="sxs-lookup"><span data-stu-id="2e884-220">schedule name</span></span> |<span data-ttu-id="2e884-221">일정의 이름을 포함하는 단일 **이름** 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-221">Single **name** entity with the name of the schedule.</span></span> |
| <span data-ttu-id="2e884-222">Runbook 이름</span><span class="sxs-lookup"><span data-stu-id="2e884-222">runbook name</span></span>  |<span data-ttu-id="2e884-223">runbook 이름을 포함하는 단일 **name** 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-223">Single **name** entity with the name of the runbook.</span></span>  |



## <a name="variables"></a><span data-ttu-id="2e884-224">변수</span><span class="sxs-lookup"><span data-stu-id="2e884-224">Variables</span></span>
<span data-ttu-id="2e884-225">[Azure Automation 변수](../automation/automation-variables.md)의 형식은 **Microsoft.Automation/automationAccounts/variables**이며, 다음과 같은 구조를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-225">[Azure Automation variables](../automation/automation-variables.md) have a type of **Microsoft.Automation/automationAccounts/variables** and have the following structure.</span></span>  <span data-ttu-id="2e884-226">여기에는 일반 변수 및 매개 변수가 포함되어 있으므로 이 코드 조각을 복사하여 솔루션 파일에 붙여넣고 매개 변수 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-226">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span>

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

<span data-ttu-id="2e884-227">변수 리소스의 속성은 다음 표에서 설명하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-227">The properties for variable resources are described in the following table.</span></span>

| <span data-ttu-id="2e884-228">속성</span><span class="sxs-lookup"><span data-stu-id="2e884-228">Property</span></span> | <span data-ttu-id="2e884-229">설명</span><span class="sxs-lookup"><span data-stu-id="2e884-229">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2e884-230">설명</span><span class="sxs-lookup"><span data-stu-id="2e884-230">description</span></span> | <span data-ttu-id="2e884-231">변수에 대한 선택적 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-231">Optional description for the variable.</span></span> |
| <span data-ttu-id="2e884-232">isEncrypted</span><span class="sxs-lookup"><span data-stu-id="2e884-232">isEncrypted</span></span> | <span data-ttu-id="2e884-233">변수를 암호화해야 하는지 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-233">Specifies whether the variable should be encrypted.</span></span> |
| <span data-ttu-id="2e884-234">type</span><span class="sxs-lookup"><span data-stu-id="2e884-234">type</span></span> | <span data-ttu-id="2e884-235">이 속성은 현재 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-235">This property currently has no effect.</span></span>  <span data-ttu-id="2e884-236">변수의 데이터 형식은 초기 값에 의해 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-236">The data type of the variable will be determined by the initial value.</span></span> |
| <span data-ttu-id="2e884-237">값</span><span class="sxs-lookup"><span data-stu-id="2e884-237">value</span></span> | <span data-ttu-id="2e884-238">변수의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-238">Value for the variable.</span></span> |

> [!NOTE]
> <span data-ttu-id="2e884-239">**type** 속성은 현재 생성 중인 변수에 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-239">The **type** property currently has no effect on the variable being created.</span></span>  <span data-ttu-id="2e884-240">변수의 데이터 형식은 해당 값에 의해 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-240">The data type for the variable will be determined by the value.</span></span>  

<span data-ttu-id="2e884-241">변수에 대한 초기 값을 설정하는 경우 올바른 데이터 형식으로 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-241">If you set the initial value for the variable, it must be configured as the correct data type.</span></span>  <span data-ttu-id="2e884-242">다음 표에서는 허용 가능한 여러 데이터 형식과 해당 구문을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-242">The following table provides the different data types allowable and their syntax.</span></span>  <span data-ttu-id="2e884-243">JSON의 값에서는 항상 특수 문자를 인용 부호로 묶고 전체 값도 인용 부호로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-243">Note that values in JSON are expected to always be enclosed in quotes with any special characters within the quotes.</span></span>  <span data-ttu-id="2e884-244">예를 들어 문자열 값은 따옴표로 묶고(이스케이프 문자(\\) 사용), 숫자 값은 하나의 인용 부호 세트로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-244">For example, a string value would be specified by quotes around the string (using the escape character (\\)) while a numeric value would be specified with one set of quotes.</span></span>

| <span data-ttu-id="2e884-245">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="2e884-245">Data type</span></span> | <span data-ttu-id="2e884-246">설명</span><span class="sxs-lookup"><span data-stu-id="2e884-246">Description</span></span> | <span data-ttu-id="2e884-247">예제</span><span class="sxs-lookup"><span data-stu-id="2e884-247">Example</span></span> | <span data-ttu-id="2e884-248">결과 값</span><span class="sxs-lookup"><span data-stu-id="2e884-248">Resolves to</span></span> |
|:--|:--|:--|:--|
| <span data-ttu-id="2e884-249">string</span><span class="sxs-lookup"><span data-stu-id="2e884-249">string</span></span>   | <span data-ttu-id="2e884-250">값을 큰따옴표로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-250">Enclose value in double quotes.</span></span>  | <span data-ttu-id="2e884-251">"\"Hello world\""</span><span class="sxs-lookup"><span data-stu-id="2e884-251">"\"Hello world\""</span></span> | <span data-ttu-id="2e884-252">"Hello world"</span><span class="sxs-lookup"><span data-stu-id="2e884-252">"Hello world"</span></span> |
| <span data-ttu-id="2e884-253">numeric</span><span class="sxs-lookup"><span data-stu-id="2e884-253">numeric</span></span>  | <span data-ttu-id="2e884-254">작은따옴표가 있는 숫자 값</span><span class="sxs-lookup"><span data-stu-id="2e884-254">Numeric value with single quotes.</span></span>| <span data-ttu-id="2e884-255">"64"</span><span class="sxs-lookup"><span data-stu-id="2e884-255">"64"</span></span> | <span data-ttu-id="2e884-256">64</span><span class="sxs-lookup"><span data-stu-id="2e884-256">64</span></span> |
| <span data-ttu-id="2e884-257">부울</span><span class="sxs-lookup"><span data-stu-id="2e884-257">boolean</span></span>  | <span data-ttu-id="2e884-258">따옴표로 묶은 **true** 또는 **false**.</span><span class="sxs-lookup"><span data-stu-id="2e884-258">**true** or **false** in quotes.</span></span>  <span data-ttu-id="2e884-259">이 값은 소문자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-259">Note that this value must be lowercase.</span></span> | <span data-ttu-id="2e884-260">"true"</span><span class="sxs-lookup"><span data-stu-id="2e884-260">"true"</span></span> | <span data-ttu-id="2e884-261">true</span><span class="sxs-lookup"><span data-stu-id="2e884-261">true</span></span> |
| <span data-ttu-id="2e884-262">Datetime</span><span class="sxs-lookup"><span data-stu-id="2e884-262">datetime</span></span> | <span data-ttu-id="2e884-263">직렬화된 날짜 값.</span><span class="sxs-lookup"><span data-stu-id="2e884-263">Serialized date value.</span></span><br><span data-ttu-id="2e884-264">PowerShell에서 ConvertTo-Json cmdlet을 사용하여 특정 날짜에 대해 이 값을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-264">You can use the ConvertTo-Json cmdlet in PowerShell to generate this value for a particular date.</span></span><br><span data-ttu-id="2e884-265">예제: get-date "5/24/2017 13:14:57" \\</span><span class="sxs-lookup"><span data-stu-id="2e884-265">Example: get-date "5/24/2017 13:14:57" \\</span></span>| <span data-ttu-id="2e884-266">ConvertTo-Json</span><span class="sxs-lookup"><span data-stu-id="2e884-266">ConvertTo-Json</span></span> | <span data-ttu-id="2e884-267">"\\/Date(1495656897378)\\/"</span><span class="sxs-lookup"><span data-stu-id="2e884-267">"\\/Date(1495656897378)\\/"</span></span> | <span data-ttu-id="2e884-268">2017-05-24 13:14:57</span><span class="sxs-lookup"><span data-stu-id="2e884-268">2017-05-24 13:14:57</span></span> |

## <a name="modules"></a><span data-ttu-id="2e884-269">모듈</span><span class="sxs-lookup"><span data-stu-id="2e884-269">Modules</span></span>
<span data-ttu-id="2e884-270">관리 솔루션은 Automation 계정에서 항상 사용할 수 있으므로 Runbook에서 사용하는 [전역 모듈](../automation/automation-integration-modules.md)을 정의할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-270">Your management solution does not need to define [global modules](../automation/automation-integration-modules.md) used by your runbooks because they will always be available in your Automation account.</span></span>  <span data-ttu-id="2e884-271">Runbook에서 사용하는 다른 모듈에 대한 리소스를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-271">You do need to include a resource for any other module used by your runbooks.</span></span>

<span data-ttu-id="2e884-272">[통합 모듈](../automation/automation-integration-modules.md)의 형식은 **Microsoft.Automation/automationAccounts/modules**이며, 다음과 같은 구조를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-272">[Integration modules](../automation/automation-integration-modules.md) have a type of **Microsoft.Automation/automationAccounts/modules** and have the following structure.</span></span>  <span data-ttu-id="2e884-273">여기에는 일반 변수 및 매개 변수가 포함되어 있으므로 이 코드 조각을 복사하여 솔루션 파일에 붙여넣고 매개 변수 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-273">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span>

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


<span data-ttu-id="2e884-274">모듈 리소스의 속성은 다음 표에서 설명하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-274">The properties for module resources are described in the following table.</span></span>

| <span data-ttu-id="2e884-275">속성</span><span class="sxs-lookup"><span data-stu-id="2e884-275">Property</span></span> | <span data-ttu-id="2e884-276">설명</span><span class="sxs-lookup"><span data-stu-id="2e884-276">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2e884-277">contentLink</span><span class="sxs-lookup"><span data-stu-id="2e884-277">contentLink</span></span> |<span data-ttu-id="2e884-278">모듈의 내용을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-278">Specifies the content of the module.</span></span> <br><br><span data-ttu-id="2e884-279">uri - 모듈 내용에 대한 Uri입니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-279">uri - Uri to the content of the module.</span></span>  <span data-ttu-id="2e884-280">이 URL은 PowerShell 및 Script runbook의 경우 .ps1 파일이 되고 그래프 runbook의 경우 내보낸 그래픽 runbook 파일이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-280">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="2e884-281">version - 자체적으로 추적하기 위한 모듈의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-281">version - Version of the module for your own tracking.</span></span> |

<span data-ttu-id="2e884-282">모듈 리소스가 Runbook보다 먼저 만들어지도록 Runbook이 해당 리소스에 종속되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-282">The runbook should depend on the module resource to ensure that it's created before the runbook.</span></span>

### <a name="updating-modules"></a><span data-ttu-id="2e884-283">모듈 업데이트</span><span class="sxs-lookup"><span data-stu-id="2e884-283">Updating modules</span></span>
<span data-ttu-id="2e884-284">일정을 사용하는 runbook이 포함된 관리 솔루션을 업데이트하는데 해당 runbook에 사용되는 새 모듈이 솔루션의 새 버전에 포함된 경우 runbook은 이전 버전의 모듈을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-284">If you update a management solution that includes a runbook that uses a schedule, and the new version of your solution has a new module used by that runbook, then the runbook may use the old version of the module.</span></span>  <span data-ttu-id="2e884-285">솔루션에 다음 runbook을 포함하고 다른 runbook 전에 runbook을 실행할 작업을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-285">You should include the following runbooks in your solution and create a job to run them before any other runbooks.</span></span>  <span data-ttu-id="2e884-286">이렇게 하면 runbook이 로드되기 전에 필요한 경우 모듈이 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-286">This will ensure that any modules are updated as required before the runbooks are loaded.</span></span>

* <span data-ttu-id="2e884-287">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript)을 사용하면 솔루션에서 runbook에 사용된 모든 모듈이 최신 버전이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-287">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) will ensure that all of the modules used by runbooks in your solution are the latest version.</span></span>  
* <span data-ttu-id="2e884-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript)를 사용하면 일정 리소스에 연결된 runbook이 최신 모듈을 사용하도록 모든 일정 리소스가 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) will reregister all of the schedule resources to ensure that the runbooks linked to them with use the latest modules.</span></span>




## <a name="sample"></a><span data-ttu-id="2e884-289">샘플</span><span class="sxs-lookup"><span data-stu-id="2e884-289">Sample</span></span>
<span data-ttu-id="2e884-290">다음은 다음 리소스를 포함하는 솔루션의 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-290">Following is a sample of a solution that include that includes the following resources:</span></span>

- <span data-ttu-id="2e884-291">Runbook -</span><span class="sxs-lookup"><span data-stu-id="2e884-291">Runbook.</span></span>  <span data-ttu-id="2e884-292">공용 GitHub 리포지토리에 저장된 샘플 Runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-292">This is a sample runbook stored in a public GitHub repository.</span></span>
- <span data-ttu-id="2e884-293">자동화 작업 - 솔루션을 설치할 때 Runbook을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-293">Automation job that starts the runbook when the solution is installed.</span></span>
- <span data-ttu-id="2e884-294">일정 및 작업 일정 - 일정한 간격으로 Runbook을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-294">Schedule and job schedule to start the runbook at regular intervals.</span></span>
- <span data-ttu-id="2e884-295">인증서</span><span class="sxs-lookup"><span data-stu-id="2e884-295">Certificate.</span></span>
- <span data-ttu-id="2e884-296">자격 증명</span><span class="sxs-lookup"><span data-stu-id="2e884-296">Credential.</span></span>
- <span data-ttu-id="2e884-297">변수</span><span class="sxs-lookup"><span data-stu-id="2e884-297">Variable.</span></span>
- <span data-ttu-id="2e884-298">모듈 -</span><span class="sxs-lookup"><span data-stu-id="2e884-298">Module.</span></span>  <span data-ttu-id="2e884-299">Log Analytics에 데이터를 쓰는 [OMSIngestionAPI 모듈 ](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5)입니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-299">This is the [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) for writing data to Log Analytics.</span></span> 

<span data-ttu-id="2e884-300">이 샘플에서는 리소스 정의의 값을 하드 코딩하는 대신 솔루션에 일반적으로 사용되는 [표준 솔루션 매개 변수](operations-management-suite-solutions-solution-file.md#parameters) 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-300">The sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed to hardcoding values in the resource definitions.</span></span>


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
            "description": "GUID for the schedule link to runbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for the runbook job.",
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




## <a name="next-steps"></a><span data-ttu-id="2e884-301">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2e884-301">Next steps</span></span>
* <span data-ttu-id="2e884-302">[솔루션에 보기를 추가](operations-management-suite-solutions-resources-views.md)하여 수집된 데이터를 시각화합니다.</span><span class="sxs-lookup"><span data-stu-id="2e884-302">[Add a view to your solution](operations-management-suite-solutions-resources-views.md) to visualize collected data.</span></span>
