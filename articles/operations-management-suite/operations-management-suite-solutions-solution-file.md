---
title: "OMS(Operations Management Suite)의 관리 솔루션 만들기 | Microsoft Docs"
description: "관리 솔루션은 고객이 OMS 작업 영역에 추가할 수 있는 패키지 관리 시나리오를 제공하여 OMS(Operations Management Suite)의 기능을 확장합니다.  이 문서에서는 자체 환경에 사용할 관리 솔루션 또는 고객에게 제공할 관리 솔루션을 만드는 방법에 대해 자세히 설명합니다."
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
ms.openlocfilehash: ee3462c13101d18921dc488b08c79e1e4e02ff3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a><span data-ttu-id="91618-104">OMS(Operations Management Suite)(미리 보기)에서 관리 솔루션 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="91618-104">Creating a management solution file in Operations Management Suite (OMS) (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="91618-105">현재 Preview로 제공되는 OMS의 사용자 지정 솔루션 만들기에 대한 예비 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="91618-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="91618-106">아래 설명된 스키마는 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91618-106">Any schema described below is subject to change.</span></span>  

<span data-ttu-id="91618-107">OMS(Operations Management Suite)의 관리 솔루션은 [Resource Manager 템플릿](../azure-resource-manager/resource-manager-template-walkthrough.md)으로 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="91618-107">Management solutions in Operations Management Suite (OMS) are implemented as [Resource Manager templates](../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>  <span data-ttu-id="91618-108">관리 솔루션을 작성하는 방법에서 주요 작업은 [템플릿 작성](../azure-resource-manager/resource-group-authoring-templates.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="91618-108">The main task in learning how to author management solutions is learning how to [author a template](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>  <span data-ttu-id="91618-109">이 문서에서는 솔루션에 사용되는 템플릿의 고유한 세부 정보와 일반적인 솔루션 리소스를 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="91618-109">This article provides unique details of templates used for solutions and how to configure typical solution resources.</span></span>


## <a name="tools"></a><span data-ttu-id="91618-110">도구</span><span class="sxs-lookup"><span data-stu-id="91618-110">Tools</span></span>

<span data-ttu-id="91618-111">아무 텍스트 편집기나 사용하여 솔루션 파일로 작업할 수 있지만 다음 문서에 설명된 대로 Visual Studio 또는 Visual Studio 코드에서 제공되는 기능을 활용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="91618-111">You can use any text editor to work with solution files, but we recommend leveraging the features provided in Visual Studio or Visual Studio Code as described in the following articles.</span></span>

- [<span data-ttu-id="91618-112">Visual Studio를 통해 Azure 리소스 그룹 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="91618-112">Creating and deploying Azure resource groups through Visual Studio</span></span>](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [<span data-ttu-id="91618-113">Visual Studio 코드에서 Azure Resource Manager 템플릿으로 작업</span><span class="sxs-lookup"><span data-stu-id="91618-113">Working with Azure Resource Manager Templates in Visual Studio Code</span></span>](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a><span data-ttu-id="91618-114">구조</span><span class="sxs-lookup"><span data-stu-id="91618-114">Structure</span></span>
<span data-ttu-id="91618-115">관리 솔루션 파일의 기본 구조는 다음과 같은 [리소스 관리자 템플릿](../azure-resource-manager/resource-group-authoring-templates.md#template-format)과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="91618-115">The basic structure of a management solution file is the same as a [Resource Manager Template](../azure-resource-manager/resource-group-authoring-templates.md#template-format) which is as follows.</span></span>  <span data-ttu-id="91618-116">이어지는 각 섹션에서는 솔루션의 최상위 수준 요소와 그 콘텐츠에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="91618-116">Each of the sections below describes the top level elements and and their contents in a solution.</span></span>  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a><span data-ttu-id="91618-117">매개 변수</span><span class="sxs-lookup"><span data-stu-id="91618-117">Parameters</span></span>
<span data-ttu-id="91618-118">[매개 변수](../azure-resource-manager/resource-group-authoring-templates.md#parameters)는 사용자가 관리 솔루션을 설치할 때 사용자에게 요구할 값입니다.</span><span class="sxs-lookup"><span data-stu-id="91618-118">[Parameters](../azure-resource-manager/resource-group-authoring-templates.md#parameters) are values that you require from the user when they install the management solution.</span></span>  <span data-ttu-id="91618-119">모든 솔루션에 포함될 표준 매개 변수가 있고, 특정 솔루션에 필요한 다른 매개 변수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91618-119">There are standard parameters that all solutions will have, and you can add additional parameters as required for your particular solution.</span></span>  <span data-ttu-id="91618-120">사용자가 솔루션을 설치할 때 매개 변수 값을 제공하는 방법은 솔루션 설치 방법과 특정 매개 변수에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="91618-120">How users will provide parameter values when they install your solution will depend on the particular parameter and how the solution is being installed.</span></span>

<span data-ttu-id="91618-121">사용자가 [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) 또는 [Azure 빠른 시작 템플릿](operations-management-suite-solutions.md#finding-and-installing-management-solutions)을 통해 관리 솔루션을 설치할 경우에는 [OMS 작업 영역 및 Automation 계정](operations-management-suite-solutions.md#oms-workspace-and-automation-account)을 선택하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="91618-121">When a user installs your management solution through the [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) or [Azure QuickStart templates](operations-management-suite-solutions.md#finding-and-installing-management-solutions) they are prompted to select an [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span></span>  <span data-ttu-id="91618-122">이러한 템플릿은 각 표준 매개 변수의 값을 채우는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="91618-122">These are used to populate the values of each of the standard parameters.</span></span>  <span data-ttu-id="91618-123">사용자에게는 표준 매개 변수의 값을 직접 제공하라는 메시지가 표시되지 않고 추가 매개 변수의 값을 제공하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="91618-123">The user is not prompted to directly provide values for the standard parameters, but they are prompted to provide values for any additional parameters.</span></span>

<span data-ttu-id="91618-124">사용자가 솔루션을 [다른 방법](operations-management-suite-solutions.md#finding-and-installing-management-solutions)으로 설치할 경우에는 모든 표준 매개 변수와 모든 추가 매개 변수의 값을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91618-124">When the user installs your solution [another method](operations-management-suite-solutions.md#finding-and-installing-management-solutions), they must provide a value for all standard parameters and all additional parameters.</span></span>

<span data-ttu-id="91618-125">샘플 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="91618-125">A sample parameter is shown below.</span></span>  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

<span data-ttu-id="91618-126">다음 표에서는 매개 변수의 특성을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="91618-126">The following table describes the attributes of a parameter.</span></span>

| <span data-ttu-id="91618-127">특성</span><span class="sxs-lookup"><span data-stu-id="91618-127">Attribute</span></span> | <span data-ttu-id="91618-128">설명</span><span class="sxs-lookup"><span data-stu-id="91618-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="91618-129">type</span><span class="sxs-lookup"><span data-stu-id="91618-129">type</span></span> |<span data-ttu-id="91618-130">매개 변수의 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="91618-130">Data type for the parameter.</span></span> <span data-ttu-id="91618-131">사용자에게 표시되는 입력 컨트롤은 데이터 형식에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="91618-131">The input control displayed for the user depends on the data type.</span></span><br><br><span data-ttu-id="91618-132">bool - 드롭다운 상자</span><span class="sxs-lookup"><span data-stu-id="91618-132">bool - Drop down box</span></span><br><span data-ttu-id="91618-133">string - 텍스트 상자</span><span class="sxs-lookup"><span data-stu-id="91618-133">string - Text box</span></span><br><span data-ttu-id="91618-134">int - 텍스트 상자</span><span class="sxs-lookup"><span data-stu-id="91618-134">int - Text box</span></span><br><span data-ttu-id="91618-135">securestring - 암호 필드</span><span class="sxs-lookup"><span data-stu-id="91618-135">securestring - Password field</span></span><br> |
| <span data-ttu-id="91618-136">카테고리</span><span class="sxs-lookup"><span data-stu-id="91618-136">category</span></span> |<span data-ttu-id="91618-137">매개 변수의 선택적 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="91618-137">Optional category for the parameter.</span></span>  <span data-ttu-id="91618-138">같은 범주의 매개 변수는 함께 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="91618-138">Parameters in the same category are grouped together.</span></span> |
| <span data-ttu-id="91618-139">control</span><span class="sxs-lookup"><span data-stu-id="91618-139">control</span></span> |<span data-ttu-id="91618-140">string 매개 변수의 추가 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="91618-140">Additional functionality for string parameters.</span></span><br><br><span data-ttu-id="91618-141">datetime - Datetime 컨트롤이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="91618-141">datetime - Datetime control is displayed.</span></span><br><span data-ttu-id="91618-142">guid - Guid 값이 자동으로 생성되고 매개 변수가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91618-142">guid - Guid value is automatically generated, and the parameter is not displayed.</span></span> |
| <span data-ttu-id="91618-143">설명</span><span class="sxs-lookup"><span data-stu-id="91618-143">description</span></span> |<span data-ttu-id="91618-144">매개 변수에 대한 선택적 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="91618-144">Optional description for the parameter.</span></span>  <span data-ttu-id="91618-145">매개 변수 옆에 정보 풍선으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="91618-145">Displayed in an information balloon next to the parameter.</span></span> |

### <a name="standard-parameters"></a><span data-ttu-id="91618-146">표준 매개 변수</span><span class="sxs-lookup"><span data-stu-id="91618-146">Standard parameters</span></span>
<span data-ttu-id="91618-147">다음 표에는 모든 관리 솔루션에 대한 표준 매개 변수가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="91618-147">The following table lists the standard parameters for all management solutions.</span></span>  <span data-ttu-id="91618-148">솔루션이 Azure Marketplace 또는 빠른 시작 템플릿에서 설치될 경우 매개 변수에 대한 메시지가 표시되지 않고 이러한 값이 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="91618-148">These values are populated for the user instead of prompting for them when your solution is installed from the Azure Marketplace or Quickstart templates.</span></span>  <span data-ttu-id="91618-149">솔루션이 다른 방법으로 설치될 경우 사용자가 값을 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91618-149">The user must provide values for them if the solution is installed with another method.</span></span>

> [!NOTE]
> <span data-ttu-id="91618-150">Azure Marketplace 및 빠른 시작 템플릿의 사용자 인터페이스에는 테이블의 매개 변수 이름을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91618-150">The user interface in the Azure Marketplace and Quickstart templates is expecting the parameter names in the table.</span></span>  <span data-ttu-id="91618-151">다른 매개 변수 이름을 사용하면 사용자에게 매개 변수에 대한 메시지가 표시되고 매개 변수가 자동으로 채워지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91618-151">If you use different parameter names then the user will be prompted for them, and they will not be automatically populated.</span></span>
>
>

| <span data-ttu-id="91618-152">매개 변수</span><span class="sxs-lookup"><span data-stu-id="91618-152">Parameter</span></span> | <span data-ttu-id="91618-153">형식</span><span class="sxs-lookup"><span data-stu-id="91618-153">Type</span></span> | <span data-ttu-id="91618-154">설명</span><span class="sxs-lookup"><span data-stu-id="91618-154">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="91618-155">accountName</span><span class="sxs-lookup"><span data-stu-id="91618-155">accountName</span></span> |<span data-ttu-id="91618-156">string</span><span class="sxs-lookup"><span data-stu-id="91618-156">string</span></span> |<span data-ttu-id="91618-157">Azure Automation 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="91618-157">Azure Automation account name.</span></span> |
| <span data-ttu-id="91618-158">pricingTier</span><span class="sxs-lookup"><span data-stu-id="91618-158">pricingTier</span></span> |<span data-ttu-id="91618-159">string</span><span class="sxs-lookup"><span data-stu-id="91618-159">string</span></span> |<span data-ttu-id="91618-160">Log Analytics 작업 영역 및 Azure Automation 계정의 가격 책정 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="91618-160">Pricing tier of both Log Analytics workspace and Azure Automation account.</span></span> |
| <span data-ttu-id="91618-161">regionId</span><span class="sxs-lookup"><span data-stu-id="91618-161">regionId</span></span> |<span data-ttu-id="91618-162">string</span><span class="sxs-lookup"><span data-stu-id="91618-162">string</span></span> |<span data-ttu-id="91618-163">Azure Automation 계정의 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="91618-163">Region of the Azure Automation account.</span></span> |
| <span data-ttu-id="91618-164">solutionName</span><span class="sxs-lookup"><span data-stu-id="91618-164">solutionName</span></span> |<span data-ttu-id="91618-165">string</span><span class="sxs-lookup"><span data-stu-id="91618-165">string</span></span> |<span data-ttu-id="91618-166">솔루션의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="91618-166">Name of the solution.</span></span>  <span data-ttu-id="91618-167">빠른 시작 템플릿을 통해 솔루션을 배포하는 경우 사용자에게 지정하도록 요구하는 대신 문자열을 정의할 수 있도록 solutionName을 매개 변수로 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91618-167">If you are deploying your solution through Quickstart templates, then you should define solutionName as a parameter so you can define a string instead requiring the user to specify one.</span></span> |
| <span data-ttu-id="91618-168">workspaceName</span><span class="sxs-lookup"><span data-stu-id="91618-168">workspaceName</span></span> |<span data-ttu-id="91618-169">string</span><span class="sxs-lookup"><span data-stu-id="91618-169">string</span></span> |<span data-ttu-id="91618-170">Log Analytics 작업 영역 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="91618-170">Log Analytics workspace name.</span></span> |
| <span data-ttu-id="91618-171">workspaceRegionId</span><span class="sxs-lookup"><span data-stu-id="91618-171">workspaceRegionId</span></span> |<span data-ttu-id="91618-172">string</span><span class="sxs-lookup"><span data-stu-id="91618-172">string</span></span> |<span data-ttu-id="91618-173">Log Analytics 작업 영역의 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="91618-173">Region of the Log Analytics workspace.</span></span> |


<span data-ttu-id="91618-174">다음은 솔루션 파일에 복사하여 붙여넣을 수 있는 표준 매개 변수 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="91618-174">Following is the structure of the standard parameters that you can copy and paste into your solution file.</span></span>  

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
                   "description": "Region of the Log Analytics workspace"
            }
        },
        "regionId": {
            "type": "string",
            "metadata": {
                "description": "Region of the Azure Automation account"
            }
        },
        "pricingTier": {
            "type": "string",
            "metadata": {
                "description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
        }
    }


<span data-ttu-id="91618-175">**parameters('매개 변수 이름')** 구문을 사용하여 솔루션의 다른 요소에 있는 매개 변수 값을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91618-175">You refer to parameter values in other elements of the solution with the syntax **parameters('parameter name')**.</span></span>  <span data-ttu-id="91618-176">예를 들어 작업 영역 이름에 액세스하려면 **parameters('workspaceName')**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="91618-176">For example, to access the workspace name, you would use **parameters('workspaceName')**</span></span>

## <a name="variables"></a><span data-ttu-id="91618-177">변수</span><span class="sxs-lookup"><span data-stu-id="91618-177">Variables</span></span>
<span data-ttu-id="91618-178">[Variables](../azure-resource-manager/resource-group-authoring-templates.md#variables)는 관리 솔루션의 나머지 부분에 사용할 값입니다.</span><span class="sxs-lookup"><span data-stu-id="91618-178">[Variables](../azure-resource-manager/resource-group-authoring-templates.md#variables) are values that you will use in the rest of the management solution.</span></span>  <span data-ttu-id="91618-179">이러한 값은 솔루션을 설치하는 사용자에게 노출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91618-179">These values are not exposed to the user installing the solution.</span></span>  <span data-ttu-id="91618-180">작성자가 솔루션을 만드는 동안 여러 번 사용할지도 모르는 값을 관리할 수 있는 단일 위치를 제공하는 것이 이러한 값의 목적입니다.</span><span class="sxs-lookup"><span data-stu-id="91618-180">They are intended to provide the author with a single location where they can manage values that may be used multiple times throughout the solution.</span></span> <span data-ttu-id="91618-181">솔루션 관련 값을 **resources** 요소로 하드 코드하지 않고 해당 값을 변수에 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91618-181">You should put any values specific to your solution in variables as opposed to hard coding them in the **resources** element.</span></span>  <span data-ttu-id="91618-182">이렇게 하면 코드를 더 쉽게 읽을 수 있고 이후 버전에서 이들 값을 쉽게 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91618-182">This makes the code more readable and allows you to easily change these values in later versions.</span></span>

<span data-ttu-id="91618-183">다음은 솔루션에 일반적인 매개 변수를 사용한 **variables** 요소의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="91618-183">Following is an example of a **variables** element with typical parameters used in solutions.</span></span>

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="91618-184">**variables('변수 이름')** 구문을 사용하여 솔루션 전체의 변수 값을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91618-184">You refer to variable values through the solution with the syntax **variables('variable name')**.</span></span>  <span data-ttu-id="91618-185">예를 들어 SolutionName 변수에 액세스하려면 **variables('solutionName')**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="91618-185">For example, to access the SolutionName variable, you would use **variables('SolutionName')**.</span></span>

<span data-ttu-id="91618-186">여러 값 집합이 있는 복잡한 변수를 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91618-186">You can also define complex variables that multiple sets of values.</span></span>  <span data-ttu-id="91618-187">이러한 변수는 서로 다른 형식의 리소스에 대해 여러 속성을 정의하는 관리 솔루션에서 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="91618-187">These are particularly useful in management solutions where you are defining multiple properties for different types of resources.</span></span>  <span data-ttu-id="91618-188">예를 들어 위에 표시된 솔루션 변수를 다음으로 재구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91618-188">For example, you could restructure the solution variables shown above to the following.</span></span>

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="91618-189">이 경우 **variables('변수 이름').property** 구문을 사용하여 솔루션 전체의 변수 값을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91618-189">In this case, you refer to variable values through the solution with the syntax **variables('variable name').property**.</span></span>  <span data-ttu-id="91618-190">예를 들어 SolutionName 변수에 액세스하려면 **variables('솔루션').Name**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="91618-190">For example, to access the Solution Name variable, you would use **variables('Solution').Name**.</span></span>

## <a name="resources"></a><span data-ttu-id="91618-191">리소스</span><span class="sxs-lookup"><span data-stu-id="91618-191">Resources</span></span>
<span data-ttu-id="91618-192">[리소스](../azure-resource-manager/resource-group-authoring-templates.md#resources)는 관리 솔루션에서 설치 및 구성할 다양한 리소스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="91618-192">[Resources](../azure-resource-manager/resource-group-authoring-templates.md#resources) define the different resources that your management solution will install and configure.</span></span>  <span data-ttu-id="91618-193">이번 파트가 아마도 템플릿에서 가장 크고 복잡한 내용일 것입니다.</span><span class="sxs-lookup"><span data-stu-id="91618-193">This will be the largest and most complex portion of the template.</span></span>  <span data-ttu-id="91618-194">리소스 요소의 구조와 전체 설명은 [Azure Resource Manager 템플릿 작성](../azure-resource-manager/resource-group-authoring-templates.md#resources)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91618-194">You can get the structure and complete description of resource elements in [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span></span>  <span data-ttu-id="91618-195">일반적으로 정의하는 여러 리소스는 이 설명서의 다른 문서에 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91618-195">Different resources that you will typically define are detailed in other articles in this documentation.</span></span> 


### <a name="dependencies"></a><span data-ttu-id="91618-196">종속성</span><span class="sxs-lookup"><span data-stu-id="91618-196">Dependencies</span></span>
<span data-ttu-id="91618-197">**dependsOn** 요소는 다른 리소스에 대한 [종속성](../azure-resource-manager/resource-group-define-dependencies.md)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="91618-197">The **dependsOn** elements specifies a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on another resource.</span></span>  <span data-ttu-id="91618-198">솔루션이 설치될 때 모든 리소스의 종속성이 만들어진 후에야 리소스가 만들어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91618-198">When the solution is installed, a resource is not created until all of its dependencies have been created.</span></span>  <span data-ttu-id="91618-199">예를 들어 솔루션이 [작업 리소스](operations-management-suite-solutions-resources-automation.md#automation-jobs)를 사용하여 설치될 경우 솔루션에서 [Runbook을 시작](operations-management-suite-solutions-resources-automation.md#runbooks)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91618-199">For example, your solution might [start a runbook](operations-management-suite-solutions-resources-automation.md#runbooks) when it's installed using a [job resource](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span></span>  <span data-ttu-id="91618-200">작업이 만들어지기 전에 runbook이 만들어지도록 작업 리소스는 runbook 리소스에 종속됩니다.</span><span class="sxs-lookup"><span data-stu-id="91618-200">The job resource would be dependent on the runbook resource to make sure that the runbook is created before the job is created.</span></span>

### <a name="oms-workspace-and-automation-account"></a><span data-ttu-id="91618-201">OMS 작업 영역 및 Automation 계정</span><span class="sxs-lookup"><span data-stu-id="91618-201">OMS workspace and Automation account</span></span>
<span data-ttu-id="91618-202">관리 솔루션은 뷰를 포함하는 [OMS 작업 영역](../log-analytics/log-analytics-manage-access.md)과 Runbook 및 관련 리소스를 포함하는 [Automation 계정](../automation/automation-security-overview.md#automation-account-overview)이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="91618-202">Management solutions require an [OMS workspace](../log-analytics/log-analytics-manage-access.md) to contain views and an [Automation account](../automation/automation-security-overview.md#automation-account-overview) to contain runbooks and related resources.</span></span>  <span data-ttu-id="91618-203">이러한 항목은 솔루션의 리소스가 만들어지기 전에 제공되어야 하며 솔루션 자체에 정의될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="91618-203">These must be available before the resources in the solution are created and should not be defined in the solution itself.</span></span>  <span data-ttu-id="91618-204">사용자는 솔루션을 배포할 때 [작업 영역과 계정을 지정](operations-management-suite-solutions.md#oms-workspace-and-automation-account)하지만, 작성자는 다음 사항을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91618-204">The user will [specify a workspace and account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) when they deploy your solution, but as the author you should consider the following points.</span></span>

## <a name="solution-resource"></a><span data-ttu-id="91618-205">솔루션 리소스</span><span class="sxs-lookup"><span data-stu-id="91618-205">Solution resource</span></span>
<span data-ttu-id="91618-206">각 솔루션은 솔루션 자체를 정의하는 요소인 **resources** 요소에 리소스 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="91618-206">Each solution requires a resource entry in the **resources** element that defines the solution itself.</span></span>  <span data-ttu-id="91618-207">유형은 **Microsoft.OperationsManagement/solutions**이고 구조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="91618-207">This will have a type of **Microsoft.OperationsManagement/solutions** and have the following structure.</span></span> <span data-ttu-id="91618-208">여기에는 일반적으로 솔루션의 속성을 정의하는 데 사용되는 [표준 매개 변수](#parameters) 및 [변수](#variables)가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="91618-208">This includes [standard parameters](#parameters) and [variables](#variables) that are typically used to define properties of the solution.</span></span>


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




### <a name="dependencies"></a><span data-ttu-id="91618-209">종속성</span><span class="sxs-lookup"><span data-stu-id="91618-209">Dependencies</span></span>
<span data-ttu-id="91618-210">솔루션이 만들어지기 전에 솔루션 리소스가 있어야 하므로 솔루션 리소스는 솔루션의 모든 다른 리소스에 대해 [종속성](../azure-resource-manager/resource-group-define-dependencies.md)을 가져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91618-210">The solution resource must have a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on every other resource in the solution since they need to exist before the solution can be created.</span></span>  <span data-ttu-id="91618-211">**dependsOn** 요소에서 각 리소스의 항목을 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91618-211">You do this by adding an entry for each resource in the **dependsOn** element.</span></span>

### <a name="properties"></a><span data-ttu-id="91618-212">속성</span><span class="sxs-lookup"><span data-stu-id="91618-212">Properties</span></span>
<span data-ttu-id="91618-213">솔루션 리소스는 테이블의 속성을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="91618-213">The solution resource has the properties in the following table.</span></span>  <span data-ttu-id="91618-214">여기에는 솔루션 설치 후 리소스 관리 방식을 정의하는 솔루션에서 참조 및 포함하는 리소스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="91618-214">This includes the resources referenced and contained by the solution which defines how the resource is managed after the solution is installed.</span></span>  <span data-ttu-id="91618-215">솔루션의 각 리소스는 **referencedResources** 또는 **containedResources** 속성에 나열되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91618-215">Each resource in the solution should be listed in either the **referencedResources** or the **containedResources** property.</span></span>

| <span data-ttu-id="91618-216">속성</span><span class="sxs-lookup"><span data-stu-id="91618-216">Property</span></span> | <span data-ttu-id="91618-217">설명</span><span class="sxs-lookup"><span data-stu-id="91618-217">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="91618-218">workspaceResourceId</span><span class="sxs-lookup"><span data-stu-id="91618-218">workspaceResourceId</span></span> |<span data-ttu-id="91618-219">Log Analytics 작업 영역의 ID이며 *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<작업 영역 이름\>*형식입니다.</span><span class="sxs-lookup"><span data-stu-id="91618-219">ID of the Log Analytics workspace in the form *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<Workspace Name\>*.</span></span> |
| <span data-ttu-id="91618-220">referencedResources</span><span class="sxs-lookup"><span data-stu-id="91618-220">referencedResources</span></span> |<span data-ttu-id="91618-221">솔루션을 제거해도 함께 제거되면 안 되는 솔루션의 리소스 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="91618-221">List of resources in the solution that should not be removed when the solution is removed.</span></span> |
| <span data-ttu-id="91618-222">containedResources</span><span class="sxs-lookup"><span data-stu-id="91618-222">containedResources</span></span> |<span data-ttu-id="91618-223">솔루션을 제거하면 함께 제거되어야 하는 솔루션의 리소스 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="91618-223">List of resources in the solution that should be removed when the solution is removed.</span></span> |

<span data-ttu-id="91618-224">위의 예제는 runbook, 일정, 보기가 포함된 솔루션과 관련됩니다.</span><span class="sxs-lookup"><span data-stu-id="91618-224">The example  above is for a solution with a runbook, a schedule, and view.</span></span>  <span data-ttu-id="91618-225">일정 및 runbook은 **properties** 요소에서 *참조*되므로 솔루션이 제거될 때 제거되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91618-225">The schedule and runbook are *referenced* in the  **properties**  element so they are not removed when the solution is removed.</span></span>  <span data-ttu-id="91618-226">보기는 *포함*되어 있으므로 솔루션을 제거하면 함께 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="91618-226">The view is *contained* so it is removed when the solution is removed.</span></span>

### <a name="plan"></a><span data-ttu-id="91618-227">계획</span><span class="sxs-lookup"><span data-stu-id="91618-227">Plan</span></span>
<span data-ttu-id="91618-228">솔루션 리소스의 **plan** 엔터티는 테이블의 속성을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="91618-228">The **plan** entity of the solution resource has the properties in the following table.</span></span>

| <span data-ttu-id="91618-229">속성</span><span class="sxs-lookup"><span data-stu-id="91618-229">Property</span></span> | <span data-ttu-id="91618-230">설명</span><span class="sxs-lookup"><span data-stu-id="91618-230">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="91618-231">name</span><span class="sxs-lookup"><span data-stu-id="91618-231">name</span></span> |<span data-ttu-id="91618-232">솔루션의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="91618-232">Name of the solution.</span></span> |
| <span data-ttu-id="91618-233">버전</span><span class="sxs-lookup"><span data-stu-id="91618-233">version</span></span> |<span data-ttu-id="91618-234">솔루션 버전은 작성자가 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="91618-234">Version of the solution as determined by the author.</span></span> |
| <span data-ttu-id="91618-235">product</span><span class="sxs-lookup"><span data-stu-id="91618-235">product</span></span> |<span data-ttu-id="91618-236">솔루션을 식별하는 고유 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="91618-236">Unique string to identify the solution.</span></span> |
| <span data-ttu-id="91618-237">publisher</span><span class="sxs-lookup"><span data-stu-id="91618-237">publisher</span></span> |<span data-ttu-id="91618-238">솔루션의 게시자입니다.</span><span class="sxs-lookup"><span data-stu-id="91618-238">Publisher of the solution.</span></span> |



## <a name="sample"></a><span data-ttu-id="91618-239">샘플</span><span class="sxs-lookup"><span data-stu-id="91618-239">Sample</span></span>
<span data-ttu-id="91618-240">다음 위치에서 솔루션 리소스를 사용하는 솔루션 파일의 샘플을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91618-240">You can view samples of solution files with a solution resource at the following locations.</span></span>

- [<span data-ttu-id="91618-241">Automation 리소스</span><span class="sxs-lookup"><span data-stu-id="91618-241">Automation resources</span></span>](operations-management-suite-solutions-resources-automation.md#sample)
- [<span data-ttu-id="91618-242">검색 및 경고 리소스</span><span class="sxs-lookup"><span data-stu-id="91618-242">Search and alert resources</span></span>](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a><span data-ttu-id="91618-243">다음 단계</span><span class="sxs-lookup"><span data-stu-id="91618-243">Next steps</span></span>
* <span data-ttu-id="91618-244">관리 솔루션에 [저장된 검색 및 경고를 추가](operations-management-suite-solutions-resources-searches-alerts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="91618-244">[Add saved searches and alerts](operations-management-suite-solutions-resources-searches-alerts.md) to your management solution.</span></span>
* <span data-ttu-id="91618-245">관리 솔루션에 대한 [보기를 추가](operations-management-suite-solutions-resources-views.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="91618-245">[Add views](operations-management-suite-solutions-resources-views.md) to your management solution.</span></span>
* <span data-ttu-id="91618-246">관리 솔루션에 [Runbook 및 기타 Automation 리소스를 추가](operations-management-suite-solutions-resources-automation.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="91618-246">[Add runbooks and other Automation resources](operations-management-suite-solutions-resources-automation.md) to your management solution.</span></span>
* <span data-ttu-id="91618-247">[Azure Resource Manager 템플릿 작성](../azure-resource-manager/resource-group-authoring-templates.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="91618-247">Learn the details of [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="91618-248">[Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates)에서 다양한 Resource Manager 템플릿 샘플을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="91618-248">Search [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates) for samples of different Resource Manager templates.</span></span>
