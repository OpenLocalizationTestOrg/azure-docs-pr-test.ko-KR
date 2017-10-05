---
title: "OMS(Operations Management Suite) 관리 솔루션의 보기 | Microsoft Docs"
description: "OMS(Operations Management Suite)의 관리 솔루션은 대개 데이터를 시각화하기 위한 하나 이상의 보기를 포함합니다.  이 문서에서는 뷰 디자이너에서 만들어진 보기를 내보내고 관리 솔루션에 포함하는 방법을 설명합니다. "
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 570b278c-2d47-4e5a-9828-7f01f31ddf8c
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: 533b5564a805e0b41f2b1a4ad92e12b133220952
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a><span data-ttu-id="2717b-104">OMS(Operations Management Suite) 관리 솔루션의 보기(Preview)</span><span class="sxs-lookup"><span data-stu-id="2717b-104">Views in Operations Management Suite (OMS) management solutions (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="2717b-105">현재 Preview로 제공되는 OMS의 사용자 지정 솔루션 만들기에 대한 예비 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="2717b-106">아래 설명된 스키마는 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-106">Any schema described below is subject to change.</span></span>    
>
>

<span data-ttu-id="2717b-107">[OMS(Operations Management Suite)의 관리 솔루션](operations-management-suite-solutions.md)은 대개 데이터를 시각화하기 위한 하나 이상의 보기를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-107">[Management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions.md) will typically include one or more views to visualize data.</span></span>  <span data-ttu-id="2717b-108">이 문서에서는 [뷰 디자이너](../log-analytics/log-analytics-view-designer.md)에서 만들어진 보기를 내보내고 관리 솔루션에 포함하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-108">This article describes how to export a view created by the [View Designer](../log-analytics/log-analytics-view-designer.md) and include it in a management solution.</span></span>  

> [!NOTE]
> <span data-ttu-id="2717b-109">이 문서의 샘플에는 관리 솔루션에 필요하거나 공통적이며 [OMS(Operations Management Suite)의 관리 솔루션 만들기](operations-management-suite-solutions-creating.md)에서 설명한 매개 변수와 변수가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-109">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="2717b-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2717b-110">Prerequisites</span></span>
<span data-ttu-id="2717b-111">이 문서에서는 [관리 솔루션을 만드는](operations-management-suite-solutions-creating.md) 방법과 솔루션 파일의 구조를 잘 알고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-111">This article assumes that you're already familiar with how to [create a management solution](operations-management-suite-solutions-creating.md) and the structure of a solution file.</span></span>

## <a name="overview"></a><span data-ttu-id="2717b-112">개요</span><span class="sxs-lookup"><span data-stu-id="2717b-112">Overview</span></span>
<span data-ttu-id="2717b-113">관리 솔루션에 보기를 포함하려면 [솔루션 파일](operations-management-suite-solutions-creating.md)에서 이에 대한 **리소스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-113">To include a view in a management solution, you create a **resource** for it in the [solution file](operations-management-suite-solutions-creating.md).</span></span>  <span data-ttu-id="2717b-114">보기의 세부 구성을 설명하는 JSON은 일반적으로 복잡하며 일반적인 솔루션 작성자가 수동으로 만들 수 있는 것이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-114">The JSON that describes the view's detailed configuration is typically complex though and not something that a typical solution author would be able to create manually.</span></span>  <span data-ttu-id="2717b-115">가장 일반적인 방법은 [뷰 디자이너](../log-analytics/log-analytics-view-designer.md)를 사용하여 보기를 만들고, 내보내고 나서, 세부 구성을 솔루션에 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-115">The most common method is to create the view using the [View Designer](../log-analytics/log-analytics-view-designer.md), export it, and then add its detailed configuration to the solution.</span></span>

<span data-ttu-id="2717b-116">보기를 솔루션에 추가하는 기본 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-116">The basic steps to add a view to a solution are as follows.</span></span>  <span data-ttu-id="2717b-117">각 단계는 아래 섹션에서 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-117">Each step is described in further detail in the sections below.</span></span>

1. <span data-ttu-id="2717b-118">보기를 파일로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-118">Export the view to a file.</span></span>
2. <span data-ttu-id="2717b-119">솔루션에서 보기 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-119">Create the view resource in the solution.</span></span>
3. <span data-ttu-id="2717b-120">보기 세부 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-120">Add the view details.</span></span>

## <a name="export-the-view-to-a-file"></a><span data-ttu-id="2717b-121">보기를 파일로 내보내기</span><span class="sxs-lookup"><span data-stu-id="2717b-121">Export the view to a file</span></span>
<span data-ttu-id="2717b-122">[Log Analytics 뷰 디자이너](../log-analytics/log-analytics-view-designer.md)의 지침에 따라 보기를 파일로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-122">Follow the instructions at [Log Analytics View Designer](../log-analytics/log-analytics-view-designer.md) to export a view to a file.</span></span>  <span data-ttu-id="2717b-123">내보낸 파일의 형식은 [솔루션 파일과 같은 요소](operations-management-suite-solutions-solution-file.md)가 포함된 JSON 형식이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-123">The exported file will be in JSON format with the same [elements as the solution file](operations-management-suite-solutions-solution-file.md).</span></span>  

<span data-ttu-id="2717b-124">보기 파일의 **resources** 요소에는 OMS 작업 영역을 나타내는 **Microsoft.OperationalInsights/workspaces** 형식의 리소스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-124">The **resources** element of the view file will have a resource with a type of **Microsoft.OperationalInsights/workspaces** that represents the OMS workspace.</span></span>  <span data-ttu-id="2717b-125">이 요소에는 보기를 나타내고 세부 구성이 들어 있는 **views** 형식의 하위 요소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-125">This element will have a subelement with a type of **views** that represents the view and contains its detailed configuration.</span></span>  <span data-ttu-id="2717b-126">이 요소의 세부 정보를 복사하여 솔루션에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-126">You will copy the details of this element and then copy it into your solution.</span></span>

## <a name="create-the-view-resource-in-the-solution"></a><span data-ttu-id="2717b-127">솔루션에서 보기 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="2717b-127">Create the view resource in the solution</span></span>
<span data-ttu-id="2717b-128">솔루션 파일의 **resources** 요소에 다음 보기 리소스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-128">Add the following view resource to the **resources** element of your solution file.</span></span>  <span data-ttu-id="2717b-129">이 작업에는 아래 설명된, 추가해야 하는 변수가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-129">This uses variables that are described below that you must also add.</span></span>  <span data-ttu-id="2717b-130">**Dashboard** 및 **OverviewTile** 속성은 내보낸 보기 파일의 해당 속성으로 덮어쓸 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-130">Note that the **Dashboard** and **OverviewTile** properties are placeholders that you will overwrite with the corresponding properties from the exported view file.</span></span>

    {
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
        "type": "Microsoft.OperationalInsights/workspaces/views",
        "location": "[parameters('workspaceregionId')]",
        "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
        "dependson": [
            ],
        "properties": {
            "Id": "[variables('ViewName')]",
            "Name": "[variables('ViewName')]",
            "DisplayName": "[variables('ViewName')]",
            "Description": "",
            "Author": "[variables('ViewAuthor')]",
            "Source": "Local",
            "Dashboard": ,
            "OverviewTile":
        }
    }

<span data-ttu-id="2717b-131">솔루션 파일의 variables 요소에 다음 변수를 추가하고 해당 값을 솔루션의 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-131">Add the following variables to the variables element of the solution file and replace the values to those for your solution.</span></span>

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of the view."
    "ViewName": "Provide a name for the view here."


<span data-ttu-id="2717b-132">이제 내보낸 보기 파일의 전체 보기 리소스를 복사할 수 있지만, 해당 리소스가 솔루션에서 작동하려면 다음과 같이 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-132">Note that you could copy the entire view resource from your exported view file, but you would need to make the following changes for it to work in your solution.</span></span>  

* <span data-ttu-id="2717b-133">보기 리소스의 **type**을 **views**에서 **Microsoft.OperationalInsights/workspaces**로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-133">The **type** for the view resource needs to be changed from **views** to **Microsoft.OperationalInsights/workspaces**.</span></span>
* <span data-ttu-id="2717b-134">작업 영역 이름을 포함하도록 보기 리소스의 **name** 속성을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-134">The **name** property for the view resource needs to be changed to include the workspace name.</span></span>
* <span data-ttu-id="2717b-135">솔루션에 작업 영역 리소스가 정의되어 있지 않으므로 작업 영역의 종속성을 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-135">The dependency on the workspace needs to be removed since the workspace resource isn't defined in the solution.</span></span>
* <span data-ttu-id="2717b-136">**DisplayName** 속성을 보기에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-136">**DisplayName** property needs to be added to the view.</span></span>  <span data-ttu-id="2717b-137">**Id**, **Name** 및 **DisplayName**이 모두 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-137">The **Id**, **Name**, and **DisplayName** must all match.</span></span>
* <span data-ttu-id="2717b-138">필요한 매개 변수 집합과 일치하도록 매개 변수 이름을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-138">Parameter names must be changed to match the required set of parameters.</span></span>
* <span data-ttu-id="2717b-139">변수는 솔루션에서 정의되고 적절한 속성에서 사용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-139">Variables should be defined in the solution and used in the appropriate properties.</span></span>

## <a name="add-the-view-details"></a><span data-ttu-id="2717b-140">보기 세부 정보 추가</span><span class="sxs-lookup"><span data-stu-id="2717b-140">Add the view details</span></span>
<span data-ttu-id="2717b-141">내보낸 보기 파일의 보기 리소스에는 보기의 세부 구성이 들어 있는 **properties** 요소의 두 가지 요소 **Dashboard** 및 **OverviewTile**이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-141">The view resource in the exported view file will contain two elements in the **properties** element named **Dashboard** and **OverviewTile** which contain the detailed configuration of the view.</span></span>  <span data-ttu-id="2717b-142">이 두 가지 요소와 해당 내용을 솔루션 파일에 있는 보기 리소스의 **properties** 요소에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-142">Copy these two elements and their contents into the **properties** element of the view resource in your solution file.</span></span>

## <a name="example"></a><span data-ttu-id="2717b-143">예</span><span class="sxs-lookup"><span data-stu-id="2717b-143">Example</span></span>
<span data-ttu-id="2717b-144">예를 들어 다음 샘플에서는 보기가 있는 단순 솔루션 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-144">For example, the following sample shows a simple solution file with a view.</span></span>  <span data-ttu-id="2717b-145">공간 문제로 **Dashboard** 및 **OverviewTile** 내용에는 줄임표(...)가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-145">Ellipses (...) are shown for the **Dashboard** and **OverviewTile** contents for space reasons.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspaceName": {
                "type": "string"
            },
            "accountName": {
                "type": "string"
            },
            "workspaceRegionId": {
                "type": "string"
            },
            "regionId": {
                "type": "string"
            },
            "pricingTier": {
                "type": "string"
            }
        },
        "variables": {
            "SolutionVersion": "1.1",
            "SolutionPublisher": "Contoso",
            "SolutionName": "Contoso Solution",
            "LogAnalyticsApiVersion": "2015-11-01-preview",
            "ViewAuthor":  "user@contoso.com",
            "ViewDescription":  "This is a sample view.",
            "ViewName":  "Contoso View"
        },
        "resources": [
            {
                "name": "[concat(variables('SolutionName'), '(' ,parameters('workspacename'), ')')]",
                "location": "[parameters('workspaceRegionId')]",
                "tags": { },
                "type": "Microsoft.OperationsManagement/solutions",
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "dependsOn": [
                    "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspacename'), '/views/', variables('ViewName'))]"
                ],
                "properties": {
                    "workspaceResourceId": "[concat(resourceGroup().id, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspacename'))]",
                    "referencedResources": [
                    ],
                    "containedResources": [
                        "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/views/', variables('ViewName'))]"
                    ]
                },
                "plan": {
                    "name": "[concat(variables('SolutionName'), '(' ,parameters('workspaceName'), ')')]",
                    "Version": "[variables('SolutionVersion')]",
                    "product": "ContosoSolution",
                    "publisher": "[variables('SolutionPublisher')]",
                    "promotionCode": ""
                }
            },
            {
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
                "type": "Microsoft.OperationalInsights/workspaces/views",
                "location": "[parameters('workspaceregionId')]",
                "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
                "dependson": [
                ],
                "properties": {
                    "Id": "[variables('ViewName')]",
                    "Name": "[variables('ViewName')]",
                    "DisplayName": "[variables('ViewName')]",
                    "Description": "[variables('ViewDescription')]",
                    "Author": "[variables('ViewAuthor')]",
                    "Source": "Local",
                    "Dashboard": ...,
                    "OverviewTile": ...
                }
            }
          ]
    }




## <a name="next-steps"></a><span data-ttu-id="2717b-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2717b-146">Next steps</span></span>
* <span data-ttu-id="2717b-147">[관리 솔루션](operations-management-suite-solutions-creating.md)을 만드는 방법에 대한 자세한 내용을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="2717b-147">Learn complete details of creating [management solutions](operations-management-suite-solutions-creating.md).</span></span>
* <span data-ttu-id="2717b-148">[관리 솔루션에 Automation runbook](operations-management-suite-solutions-resources-automation.md)을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2717b-148">Include [Automation runbooks in your management solution](operations-management-suite-solutions-resources-automation.md).</span></span>
