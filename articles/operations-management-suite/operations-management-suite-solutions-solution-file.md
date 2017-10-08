---
title: "Operations Management Suite (OMS)에서 aaaCreating 관리 솔루션 | Microsoft Docs"
description: "패키지에 포함 된 관리 시나리오를 제공 하 여 hello 기능 Operations Management Suite (OMS)을 확장 하는 관리 솔루션을 고객 tootheir OMS 작업 영역을 추가할 수 있습니다.  이 문서에서는 관리 솔루션 toobe를 만드는 방법에 대 한 내용은 사용자가 자신의 환경에서 사용 또는 사용 가능한 tooyour 고객을 제공 합니다."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/30/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f408df1b21f519fd1eb2cbeb19cca18f6c4161f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a><span data-ttu-id="bb008-104">OMS(Operations Management Suite)(미리 보기)에서 관리 솔루션 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="bb008-104">Creating a management solution file in Operations Management Suite (OMS) (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="bb008-105">현재 Preview로 제공되는 OMS의 사용자 지정 솔루션 만들기에 대한 예비 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="bb008-106">아래에 설명 된 모든 스키마 주체 toochange입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-106">Any schema described below is subject toochange.</span></span>  

<span data-ttu-id="bb008-107">OMS(Operations Management Suite)의 관리 솔루션은 [Resource Manager 템플릿](../azure-resource-manager/resource-manager-template-walkthrough.md)으로 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-107">Management solutions in Operations Management Suite (OMS) are implemented as [Resource Manager templates](../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>  <span data-ttu-id="bb008-108">hello 주 작업 tooauthor 관리 솔루션 너무 방법을 학습 하는 방법을 이해[템플릿으로 작성할](../azure-resource-manager/resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-108">hello main task in learning how tooauthor management solutions is learning how too[author a template](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>  <span data-ttu-id="bb008-109">이 문서에서는 사용 중인 솔루션에 대 한 서식 파일의 고유한 정보를 제공 하 고 어떻게 tooconfigure 일반적인 솔루션 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-109">This article provides unique details of templates used for solutions and how tooconfigure typical solution resources.</span></span>


## <a name="tools"></a><span data-ttu-id="bb008-110">도구</span><span class="sxs-lookup"><span data-stu-id="bb008-110">Tools</span></span>

<span data-ttu-id="bb008-111">모든 텍스트 편집기 toowork 솔루션 파일을 사용할 수 있지만 hello 다음 문서에에서 설명 된 대로 Visual Studio 또는 Visual Studio Code에서 제공 하는 hello 기능을 활용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-111">You can use any text editor toowork with solution files, but we recommend leveraging hello features provided in Visual Studio or Visual Studio Code as described in hello following articles.</span></span>

- [<span data-ttu-id="bb008-112">Visual Studio를 통해 Azure 리소스 그룹 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="bb008-112">Creating and deploying Azure resource groups through Visual Studio</span></span>](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [<span data-ttu-id="bb008-113">Visual Studio 코드에서 Azure Resource Manager 템플릿으로 작업</span><span class="sxs-lookup"><span data-stu-id="bb008-113">Working with Azure Resource Manager Templates in Visual Studio Code</span></span>](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a><span data-ttu-id="bb008-114">구조</span><span class="sxs-lookup"><span data-stu-id="bb008-114">Structure</span></span>
<span data-ttu-id="bb008-115">hello 관리 솔루션 파일의 기본 구조는 동일 hello은 한 [리소스 관리자 템플릿](../azure-resource-manager/resource-group-authoring-templates.md#template-format) 은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-115">hello basic structure of a management solution file is hello same as a [Resource Manager Template](../azure-resource-manager/resource-group-authoring-templates.md#template-format) which is as follows.</span></span>  <span data-ttu-id="bb008-116">각 hello 섹션 아래 hello 최상위 수준 요소에 설명 하 고와 솔루션의 내용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-116">Each of hello sections below describes hello top level elements and and their contents in a solution.</span></span>  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a><span data-ttu-id="bb008-117">매개 변수</span><span class="sxs-lookup"><span data-stu-id="bb008-117">Parameters</span></span>
<span data-ttu-id="bb008-118">[매개 변수](../azure-resource-manager/resource-group-authoring-templates.md#parameters) hello 관리 솔루션을 설치할 때 hello 사용자에서 필요로 하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-118">[Parameters](../azure-resource-manager/resource-group-authoring-templates.md#parameters) are values that you require from hello user when they install hello management solution.</span></span>  <span data-ttu-id="bb008-119">모든 솔루션에 포함될 표준 매개 변수가 있고, 특정 솔루션에 필요한 다른 매개 변수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-119">There are standard parameters that all solutions will have, and you can add additional parameters as required for your particular solution.</span></span>  <span data-ttu-id="bb008-120">사용자에서는 어떻게 매개 변수 값 솔루션을 설치할 때 hello 특정 매개 변수 및 hello 솔루션이 설치 되는 방법에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-120">How users will provide parameter values when they install your solution will depend on hello particular parameter and how hello solution is being installed.</span></span>

<span data-ttu-id="bb008-121">사용자가 hello 통해 관리 솔루션을 설치 하는 경우 [Azure 마켓플레이스](operations-management-suite-solutions.md#finding-and-installing-management-solutions) 또는 [Azure 빠른 시작 템플릿](operations-management-suite-solutions.md#finding-and-installing-management-solutions) 증명된 tooselect는는 [OMS 작업 영역 및 자동화 계정 ](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span><span class="sxs-lookup"><span data-stu-id="bb008-121">When a user installs your management solution through hello [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) or [Azure QuickStart templates](operations-management-suite-solutions.md#finding-and-installing-management-solutions) they are prompted tooselect an [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span></span>  <span data-ttu-id="bb008-122">이들은 각각 hello 표준 매개 변수 사용 되는 toopopulate hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-122">These are used toopopulate hello values of each of hello standard parameters.</span></span>  <span data-ttu-id="bb008-123">hello 사용자에 게 묻지 않습니다 toodirectly hello 표준 매개 변수 값을 제공 하지만 모든 추가 매개 변수를 증명된 tooprovide 값입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-123">hello user is not prompted toodirectly provide values for hello standard parameters, but they are prompted tooprovide values for any additional parameters.</span></span>

<span data-ttu-id="bb008-124">Hello 사용자 솔루션을 설치 하는 경우 [또 다른 방법은](operations-management-suite-solutions.md#finding-and-installing-management-solutions), 모든 표준 매개 변수 및 모든 추가 매개 변수 값을 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-124">When hello user installs your solution [another method](operations-management-suite-solutions.md#finding-and-installing-management-solutions), they must provide a value for all standard parameters and all additional parameters.</span></span>

<span data-ttu-id="bb008-125">샘플 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-125">A sample parameter is shown below.</span></span>  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

<span data-ttu-id="bb008-126">다음 표에서 hello 매개 변수의 hello 특성을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-126">hello following table describes hello attributes of a parameter.</span></span>

| <span data-ttu-id="bb008-127">특성</span><span class="sxs-lookup"><span data-stu-id="bb008-127">Attribute</span></span> | <span data-ttu-id="bb008-128">설명</span><span class="sxs-lookup"><span data-stu-id="bb008-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="bb008-129">type</span><span class="sxs-lookup"><span data-stu-id="bb008-129">type</span></span> |<span data-ttu-id="bb008-130">Hello 매개 변수에 대 한 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-130">Data type for hello parameter.</span></span> <span data-ttu-id="bb008-131">hello 사용자에 게 표시 하는 hello 입력된 컨트롤 hello 데이터 형식에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-131">hello input control displayed for hello user depends on hello data type.</span></span><br><br><span data-ttu-id="bb008-132">bool - 드롭다운 상자</span><span class="sxs-lookup"><span data-stu-id="bb008-132">bool - Drop down box</span></span><br><span data-ttu-id="bb008-133">string - 텍스트 상자</span><span class="sxs-lookup"><span data-stu-id="bb008-133">string - Text box</span></span><br><span data-ttu-id="bb008-134">int - 텍스트 상자</span><span class="sxs-lookup"><span data-stu-id="bb008-134">int - Text box</span></span><br><span data-ttu-id="bb008-135">securestring - 암호 필드</span><span class="sxs-lookup"><span data-stu-id="bb008-135">securestring - Password field</span></span><br> |
| <span data-ttu-id="bb008-136">카테고리</span><span class="sxs-lookup"><span data-stu-id="bb008-136">category</span></span> |<span data-ttu-id="bb008-137">Hello 매개 변수에 대 한 선택적 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-137">Optional category for hello parameter.</span></span>  <span data-ttu-id="bb008-138">매개 변수가 hello 같은 범주로 그룹화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-138">Parameters in hello same category are grouped together.</span></span> |
| <span data-ttu-id="bb008-139">control</span><span class="sxs-lookup"><span data-stu-id="bb008-139">control</span></span> |<span data-ttu-id="bb008-140">string 매개 변수의 추가 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-140">Additional functionality for string parameters.</span></span><br><br><span data-ttu-id="bb008-141">datetime - Datetime 컨트롤이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-141">datetime - Datetime control is displayed.</span></span><br><span data-ttu-id="bb008-142">guid-Guid 값은 자동으로 생성 하 고 hello 매개 변수가 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-142">guid - Guid value is automatically generated, and hello parameter is not displayed.</span></span> |
| <span data-ttu-id="bb008-143">설명</span><span class="sxs-lookup"><span data-stu-id="bb008-143">description</span></span> |<span data-ttu-id="bb008-144">Hello 매개 변수에 대 한 선택적 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-144">Optional description for hello parameter.</span></span>  <span data-ttu-id="bb008-145">정보 풍선이 다음 toohello 매개 변수에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-145">Displayed in an information balloon next toohello parameter.</span></span> |

### <a name="standard-parameters"></a><span data-ttu-id="bb008-146">표준 매개 변수</span><span class="sxs-lookup"><span data-stu-id="bb008-146">Standard parameters</span></span>
<span data-ttu-id="bb008-147">hello 다음 표에 모든 관리 솔루션에 대 한 표준 매개 변수 hello 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-147">hello following table lists hello standard parameters for all management solutions.</span></span>  <span data-ttu-id="bb008-148">Hello Azure 마켓플레이스 또는 퀵 스타트 서식 파일에서 솔루션을 설치할 때에 메시지를 표시 하는 대신 hello 사용자에 대 한 이러한 값은 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-148">These values are populated for hello user instead of prompting for them when your solution is installed from hello Azure Marketplace or Quickstart templates.</span></span>  <span data-ttu-id="bb008-149">다른 방법으로 hello 솔루션이 설치 된 경우 hello 사용자에 대 한 값을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-149">hello user must provide values for them if hello solution is installed with another method.</span></span>

> [!NOTE]
> <span data-ttu-id="bb008-150">hello Azure 마켓플레이스와 퀵 스타트 템플릿의 hello 사용자 인터페이스 hello 표에 hello 매개 변수 이름에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-150">hello user interface in hello Azure Marketplace and Quickstart templates is expecting hello parameter names in hello table.</span></span>  <span data-ttu-id="bb008-151">다른 매개 변수 이름을 사용 하는 경우 다음 hello 묻는 고객을 위해 및은 자동으로 채워지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-151">If you use different parameter names then hello user will be prompted for them, and they will not be automatically populated.</span></span>
>
>

| <span data-ttu-id="bb008-152">매개 변수</span><span class="sxs-lookup"><span data-stu-id="bb008-152">Parameter</span></span> | <span data-ttu-id="bb008-153">형식</span><span class="sxs-lookup"><span data-stu-id="bb008-153">Type</span></span> | <span data-ttu-id="bb008-154">설명</span><span class="sxs-lookup"><span data-stu-id="bb008-154">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="bb008-155">accountName</span><span class="sxs-lookup"><span data-stu-id="bb008-155">accountName</span></span> |<span data-ttu-id="bb008-156">string</span><span class="sxs-lookup"><span data-stu-id="bb008-156">string</span></span> |<span data-ttu-id="bb008-157">Azure Automation 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-157">Azure Automation account name.</span></span> |
| <span data-ttu-id="bb008-158">pricingTier</span><span class="sxs-lookup"><span data-stu-id="bb008-158">pricingTier</span></span> |<span data-ttu-id="bb008-159">string</span><span class="sxs-lookup"><span data-stu-id="bb008-159">string</span></span> |<span data-ttu-id="bb008-160">Log Analytics 작업 영역 및 Azure Automation 계정의 가격 책정 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-160">Pricing tier of both Log Analytics workspace and Azure Automation account.</span></span> |
| <span data-ttu-id="bb008-161">regionId</span><span class="sxs-lookup"><span data-stu-id="bb008-161">regionId</span></span> |<span data-ttu-id="bb008-162">string</span><span class="sxs-lookup"><span data-stu-id="bb008-162">string</span></span> |<span data-ttu-id="bb008-163">Azure 자동화 계정 hello의 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-163">Region of hello Azure Automation account.</span></span> |
| <span data-ttu-id="bb008-164">solutionName</span><span class="sxs-lookup"><span data-stu-id="bb008-164">solutionName</span></span> |<span data-ttu-id="bb008-165">string</span><span class="sxs-lookup"><span data-stu-id="bb008-165">string</span></span> |<span data-ttu-id="bb008-166">Hello 솔루션의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-166">Name of hello solution.</span></span>  <span data-ttu-id="bb008-167">퀵 스타트 템플릿을 통해 솔루션을 배포 하는 경우 다음 정의 해야 solutionName 매개 변수로 대신 hello 사용자 toospecify 하나 필요로 하는 문자열을 정의할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-167">If you are deploying your solution through Quickstart templates, then you should define solutionName as a parameter so you can define a string instead requiring hello user toospecify one.</span></span> |
| <span data-ttu-id="bb008-168">workspaceName</span><span class="sxs-lookup"><span data-stu-id="bb008-168">workspaceName</span></span> |<span data-ttu-id="bb008-169">string</span><span class="sxs-lookup"><span data-stu-id="bb008-169">string</span></span> |<span data-ttu-id="bb008-170">Log Analytics 작업 영역 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-170">Log Analytics workspace name.</span></span> |
| <span data-ttu-id="bb008-171">workspaceRegionId</span><span class="sxs-lookup"><span data-stu-id="bb008-171">workspaceRegionId</span></span> |<span data-ttu-id="bb008-172">string</span><span class="sxs-lookup"><span data-stu-id="bb008-172">string</span></span> |<span data-ttu-id="bb008-173">지역 hello 로그 분석 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-173">Region of hello Log Analytics workspace.</span></span> |


<span data-ttu-id="bb008-174">다음은 hello 구조를 복사 하 고 솔루션 파일에 붙여 넣을 수 있는 hello 표준 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-174">Following is hello structure of hello standard parameters that you can copy and paste into your solution file.</span></span>  

    "parameters": {
        "workspaceName": {
            "type": "string",
            "metadata": {
                "description": "A valid Log Analytics workspace name"
            }
        },
        "accountName": {
               "type": "string",
               "metadata": {
                   "description": "A valid Azure Automation account name"
               }
        },
        "workspaceRegionId": {
               "type": "string",
               "metadata": {
                   "description": "Region of hello Log Analytics workspace"
            }
        },
        "regionId": {
            "type": "string",
            "metadata": {
                "description": "Region of hello Azure Automation account"
            }
        },
        "pricingTier": {
            "type": "string",
            "metadata": {
                "description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
        }
    }


<span data-ttu-id="bb008-175">Hello 구문 사용 하 여 hello 솔루션의 다른 요소에서 tooparameter 값 참조 **매개 변수 ('parameter name')**합니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-175">You refer tooparameter values in other elements of hello solution with hello syntax **parameters('parameter name')**.</span></span>  <span data-ttu-id="bb008-176">예를 들어 tooaccess hello 작업 영역 이름을, 사용 하 여 **parameters('workspaceName')**</span><span class="sxs-lookup"><span data-stu-id="bb008-176">For example, tooaccess hello workspace name, you would use **parameters('workspaceName')**</span></span>

## <a name="variables"></a><span data-ttu-id="bb008-177">variables</span><span class="sxs-lookup"><span data-stu-id="bb008-177">Variables</span></span>
<span data-ttu-id="bb008-178">[변수](../azure-resource-manager/resource-group-authoring-templates.md#variables) 은 hello 관리 솔루션의 나머지 hello에에서 사용할 수 있는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-178">[Variables](../azure-resource-manager/resource-group-authoring-templates.md#variables) are values that you will use in hello rest of hello management solution.</span></span>  <span data-ttu-id="bb008-179">이러한 값이 노출된 toohello 사용자 hello 솔루션을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-179">These values are not exposed toohello user installing hello solution.</span></span>  <span data-ttu-id="bb008-180">이들은 의도 한 tooprovide hello 작성자를 한 곳 hello 솔루션 전체의 여러 번 사용할 수 있는 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-180">They are intended tooprovide hello author with a single location where they can manage values that may be used multiple times throughout hello solution.</span></span> <span data-ttu-id="bb008-181">모든 값 특정 tooyour 솔루션에에서 넣어야 변수 hello에 코딩 하는 것과 반대로 toohard로 **리소스** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-181">You should put any values specific tooyour solution in variables as opposed toohard coding them in hello **resources** element.</span></span>  <span data-ttu-id="bb008-182">쉽게 hello 코드를 더 쉽게 읽을 수 있고 있습니다 tooeasily 이후 버전에서 이러한 값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-182">This makes hello code more readable and allows you tooeasily change these values in later versions.</span></span>

<span data-ttu-id="bb008-183">다음은 솔루션에 일반적인 매개 변수를 사용한 **variables** 요소의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-183">Following is an example of a **variables** element with typical parameters used in solutions.</span></span>

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="bb008-184">Hello 구문 사용 하 여 hello 솔루션을 통해 toovariable 값 참조 **변수 ('변수 이름')**합니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-184">You refer toovariable values through hello solution with hello syntax **variables('variable name')**.</span></span>  <span data-ttu-id="bb008-185">예를 들어 tooaccess hello SolutionName 변수를 사용 하 여 **variables('SolutionName')**합니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-185">For example, tooaccess hello SolutionName variable, you would use **variables('SolutionName')**.</span></span>

<span data-ttu-id="bb008-186">여러 값 집합이 있는 복잡한 변수를 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-186">You can also define complex variables that multiple sets of values.</span></span>  <span data-ttu-id="bb008-187">이러한 변수는 서로 다른 형식의 리소스에 대해 여러 속성을 정의하는 관리 솔루션에서 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-187">These are particularly useful in management solutions where you are defining multiple properties for different types of resources.</span></span>  <span data-ttu-id="bb008-188">예를 들어 hello 솔루션 변수 toohello 다음 위에 표시 된 재구성 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-188">For example, you could restructure hello solution variables shown above toohello following.</span></span>

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="bb008-189">Hello 구문 사용 하 여 hello 솔루션을 통해 toovariable 값을 참조 하는 경우에 **variables('variable name').property**합니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-189">In this case, you refer toovariable values through hello solution with hello syntax **variables('variable name').property**.</span></span>  <span data-ttu-id="bb008-190">예를 들어 tooaccess hello 솔루션 이름 변수, 사용 하 여 **variables('Solution') 합니다. 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-190">For example, tooaccess hello Solution Name variable, you would use **variables('Solution').Name**.</span></span>

## <a name="resources"></a><span data-ttu-id="bb008-191">리소스</span><span class="sxs-lookup"><span data-stu-id="bb008-191">Resources</span></span>
<span data-ttu-id="bb008-192">[리소스](../azure-resource-manager/resource-group-authoring-templates.md#resources) 관리 솔루션 설치 및 구성 하는 hello 다른 리소스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-192">[Resources](../azure-resource-manager/resource-group-authoring-templates.md#resources) define hello different resources that your management solution will install and configure.</span></span>  <span data-ttu-id="bb008-193">가장 큰 hello 및 hello 템플릿의 가장 복잡 한 부분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-193">This will be hello largest and most complex portion of hello template.</span></span>  <span data-ttu-id="bb008-194">Hello 구조와 전체 설명은 리소스 요소를 가져올 수 있습니다 [제작 Azure 리소스 관리자 템플릿을](../azure-resource-manager/resource-group-authoring-templates.md#resources)합니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-194">You can get hello structure and complete description of resource elements in [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span></span>  <span data-ttu-id="bb008-195">일반적으로 정의하는 여러 리소스는 이 설명서의 다른 문서에 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-195">Different resources that you will typically define are detailed in other articles in this documentation.</span></span> 


### <a name="dependencies"></a><span data-ttu-id="bb008-196">종속성</span><span class="sxs-lookup"><span data-stu-id="bb008-196">Dependencies</span></span>
<span data-ttu-id="bb008-197">hello **dependsOn** 지정 하는 요소는 [종속성](../azure-resource-manager/resource-group-define-dependencies.md) 다른 리소스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-197">hello **dependsOn** elements specifies a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on another resource.</span></span>  <span data-ttu-id="bb008-198">Hello 솔루션을 설치할 때 생성 된 모든 종속성 될 때까지 리소스가 만들어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-198">When hello solution is installed, a resource is not created until all of its dependencies have been created.</span></span>  <span data-ttu-id="bb008-199">예를 들어 솔루션이 [작업 리소스](operations-management-suite-solutions-resources-automation.md#automation-jobs)를 사용하여 설치될 경우 솔루션에서 [Runbook을 시작](operations-management-suite-solutions-resources-automation.md#runbooks)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-199">For example, your solution might [start a runbook](operations-management-suite-solutions-resources-automation.md#runbooks) when it's installed using a [job resource](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span></span>  <span data-ttu-id="bb008-200">hello 작업 리소스 hello runbook 리소스 toomake hello 작업을 만들기 전에 해당 hello runbook을 만들 있는지 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-200">hello job resource would be dependent on hello runbook resource toomake sure that hello runbook is created before hello job is created.</span></span>

### <a name="oms-workspace-and-automation-account"></a><span data-ttu-id="bb008-201">OMS 작업 영역 및 Automation 계정</span><span class="sxs-lookup"><span data-stu-id="bb008-201">OMS workspace and Automation account</span></span>
<span data-ttu-id="bb008-202">관리 솔루션을 필요로 [OMS 작업 영역](../log-analytics/log-analytics-manage-access.md) toocontain 뷰 및 [자동화 계정](../automation/automation-security-overview.md#automation-account-overview) toocontain runbook 및 관련 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-202">Management solutions require an [OMS workspace](../log-analytics/log-analytics-manage-access.md) toocontain views and an [Automation account](../automation/automation-security-overview.md#automation-account-overview) toocontain runbooks and related resources.</span></span>  <span data-ttu-id="bb008-203">이러한 hello hello 솔루션의 리소스 만들어지고 hello 솔루션 자체에 정의 되지 않아야 하기 전에 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-203">These must be available before hello resources in hello solution are created and should not be defined in hello solution itself.</span></span>  <span data-ttu-id="bb008-204">hello 사용자는 [작업 영역 및 계정 지정](operations-management-suite-solutions.md#oms-workspace-and-automation-account) 경우 여 솔루션을 배포 하지만 hello 작성자 hello 포인트 다음을 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-204">hello user will [specify a workspace and account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) when they deploy your solution, but as hello author you should consider hello following points.</span></span>

## <a name="solution-resource"></a><span data-ttu-id="bb008-205">솔루션 리소스</span><span class="sxs-lookup"><span data-stu-id="bb008-205">Solution resource</span></span>
<span data-ttu-id="bb008-206">각 솔루션에 필요한 hello에 리소스 항목 **리소스** hello 솔루션 자체를 정의 하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-206">Each solution requires a resource entry in hello **resources** element that defines hello solution itself.</span></span>  <span data-ttu-id="bb008-207">유형의 아무런 **Microsoft.OperationsManagement/solutions** 있고 hello 구조를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-207">This will have a type of **Microsoft.OperationsManagement/solutions** and have hello following structure.</span></span> <span data-ttu-id="bb008-208">여기에 [표준 매개 변수](#parameters) 및 [변수](#variables) 하는 hello 솔루션의 toodefine 일반적으로 사용 되는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-208">This includes [standard parameters](#parameters) and [variables](#variables) that are typically used toodefine properties of hello solution.</span></span>


    {
      "name": "[concat(variables('Solution').Name, '[' ,parameters('workspacename'), ']')]",
      "location": "[parameters('workspaceRegionId')]",
      "tags": { },
      "type": "Microsoft.OperationsManagement/solutions",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
        <list-of-resources>
      ],
      "properties": {
        "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
        "referencedResources": [
            <list-of-referenced-resources>
        ],
        "containedResources": [
            <list-of-contained-resources>
        ]
      },
      "plan": {
        "name": "[concat(variables('Solution').Name, '[' ,parameters('workspaceName'), ']')]",
        "Version": "[variables('Solution').Version]",
        "product": "[variables('ProductName')]",
        "publisher": "[variables('Solution').Publisher]",
        "promotionCode": ""
      }
    }




### <a name="dependencies"></a><span data-ttu-id="bb008-209">종속성</span><span class="sxs-lookup"><span data-stu-id="bb008-209">Dependencies</span></span>
<span data-ttu-id="bb008-210">hello 솔루션 리소스 있어야는 [종속성](../azure-resource-manager/resource-group-define-dependencies.md) 하므로 tooexist hello 솔루션 만들기 전에 hello 솔루션의 다른 모든 리소스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-210">hello solution resource must have a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on every other resource in hello solution since they need tooexist before hello solution can be created.</span></span>  <span data-ttu-id="bb008-211">Hello에 각 리소스에 대 한 항목을 추가 하 여이 작업을 수행 **dependsOn** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-211">You do this by adding an entry for each resource in hello **dependsOn** element.</span></span>

### <a name="properties"></a><span data-ttu-id="bb008-212">properties</span><span class="sxs-lookup"><span data-stu-id="bb008-212">Properties</span></span>
<span data-ttu-id="bb008-213">hello 솔루션 리소스에는 다음 표에 hello에 hello 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-213">hello solution resource has hello properties in hello following table.</span></span>  <span data-ttu-id="bb008-214">이 참조 하 고 hello 솔루션이 설치 된 후 hello 리소스 관리 되는 방식을 정의 하는 hello 솔루션에 포함 된 hello 리소스가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-214">This includes hello resources referenced and contained by hello solution which defines how hello resource is managed after hello solution is installed.</span></span>  <span data-ttu-id="bb008-215">어느 hello에 hello 솔루션의 각 리소스를 나열 해야 **referencedResources** 또는 hello **containedResources** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-215">Each resource in hello solution should be listed in either hello **referencedResources** or hello **containedResources** property.</span></span>

| <span data-ttu-id="bb008-216">속성</span><span class="sxs-lookup"><span data-stu-id="bb008-216">Property</span></span> | <span data-ttu-id="bb008-217">설명</span><span class="sxs-lookup"><span data-stu-id="bb008-217">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="bb008-218">workspaceResourceId</span><span class="sxs-lookup"><span data-stu-id="bb008-218">workspaceResourceId</span></span> |<span data-ttu-id="bb008-219">hello 형태로 hello 로그 분석 작업 영역 ID  *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<작업 영역 이름을\>*합니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-219">ID of hello Log Analytics workspace in hello form *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<Workspace Name\>*.</span></span> |
| <span data-ttu-id="bb008-220">referencedResources</span><span class="sxs-lookup"><span data-stu-id="bb008-220">referencedResources</span></span> |<span data-ttu-id="bb008-221">Hello 솔루션을 제거할 때 제거 해야 하는 hello 솔루션의 리소스 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-221">List of resources in hello solution that should not be removed when hello solution is removed.</span></span> |
| <span data-ttu-id="bb008-222">containedResources</span><span class="sxs-lookup"><span data-stu-id="bb008-222">containedResources</span></span> |<span data-ttu-id="bb008-223">Hello 솔루션을 제거할 때 제거 하는 hello 솔루션의 리소스 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-223">List of resources in hello solution that should be removed when hello solution is removed.</span></span> |

<span data-ttu-id="bb008-224">위의 hello 예제 runbook, 일정 및 보기를 포함 하는 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-224">hello example  above is for a solution with a runbook, a schedule, and view.</span></span>  <span data-ttu-id="bb008-225">hello 일정 및 runbook은 *참조* hello에 **속성** 요소 하므로 hello 솔루션을 제거할 때 제거 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-225">hello schedule and runbook are *referenced* in hello  **properties**  element so they are not removed when hello solution is removed.</span></span>  <span data-ttu-id="bb008-226">hello 보기는 *포함* 않았으므로 hello 솔루션을 제거할 때 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-226">hello view is *contained* so it is removed when hello solution is removed.</span></span>

### <a name="plan"></a><span data-ttu-id="bb008-227">계획</span><span class="sxs-lookup"><span data-stu-id="bb008-227">Plan</span></span>
<span data-ttu-id="bb008-228">hello **계획** hello 솔루션 리소스의 엔터티에 포함 된 다음 표는 hello에 hello 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-228">hello **plan** entity of hello solution resource has hello properties in hello following table.</span></span>

| <span data-ttu-id="bb008-229">속성</span><span class="sxs-lookup"><span data-stu-id="bb008-229">Property</span></span> | <span data-ttu-id="bb008-230">설명</span><span class="sxs-lookup"><span data-stu-id="bb008-230">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="bb008-231">name</span><span class="sxs-lookup"><span data-stu-id="bb008-231">name</span></span> |<span data-ttu-id="bb008-232">Hello 솔루션의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-232">Name of hello solution.</span></span> |
| <span data-ttu-id="bb008-233">버전</span><span class="sxs-lookup"><span data-stu-id="bb008-233">version</span></span> |<span data-ttu-id="bb008-234">Hello 작성자를 기준으로 hello 솔루션 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-234">Version of hello solution as determined by hello author.</span></span> |
| <span data-ttu-id="bb008-235">product</span><span class="sxs-lookup"><span data-stu-id="bb008-235">product</span></span> |<span data-ttu-id="bb008-236">두 가지 범주인 tooidentify hello 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-236">Unique string tooidentify hello solution.</span></span> |
| <span data-ttu-id="bb008-237">publisher</span><span class="sxs-lookup"><span data-stu-id="bb008-237">publisher</span></span> |<span data-ttu-id="bb008-238">Hello 솔루션의 게시자입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-238">Publisher of hello solution.</span></span> |



## <a name="sample"></a><span data-ttu-id="bb008-239">샘플</span><span class="sxs-lookup"><span data-stu-id="bb008-239">Sample</span></span>
<span data-ttu-id="bb008-240">Hello 다음 위치에서 샘플 솔루션 리소스를 사용 하 여 솔루션 파일을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-240">You can view samples of solution files with a solution resource at hello following locations.</span></span>

- [<span data-ttu-id="bb008-241">Automation 리소스</span><span class="sxs-lookup"><span data-stu-id="bb008-241">Automation resources</span></span>](operations-management-suite-solutions-resources-automation.md#sample)
- [<span data-ttu-id="bb008-242">검색 및 경고 리소스</span><span class="sxs-lookup"><span data-stu-id="bb008-242">Search and alert resources</span></span>](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a><span data-ttu-id="bb008-243">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bb008-243">Next steps</span></span>
* <span data-ttu-id="bb008-244">[저장 된 검색 및 알림 추가](operations-management-suite-solutions-resources-searches-alerts.md) tooyour 관리 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-244">[Add saved searches and alerts](operations-management-suite-solutions-resources-searches-alerts.md) tooyour management solution.</span></span>
* <span data-ttu-id="bb008-245">[뷰 추가](operations-management-suite-solutions-resources-views.md) tooyour 관리 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-245">[Add views](operations-management-suite-solutions-resources-views.md) tooyour management solution.</span></span>
* <span data-ttu-id="bb008-246">[Runbook 및 기타 자동화 리소스를 추가](operations-management-suite-solutions-resources-automation.md) tooyour 관리 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-246">[Add runbooks and other Automation resources](operations-management-suite-solutions-resources-automation.md) tooyour management solution.</span></span>
* <span data-ttu-id="bb008-247">세부 사항을 hello [제작 Azure 리소스 관리자 템플릿을](../azure-resource-manager/resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-247">Learn hello details of [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="bb008-248">[Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates)에서 다양한 Resource Manager 템플릿 샘플을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="bb008-248">Search [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates) for samples of different Resource Manager templates.</span></span>
