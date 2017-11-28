---
title: "Operations Management Suite (OMS) 관리 솔루션에 aaaViews | Microsoft Docs"
description: "Operations Management Suite (OMS)에서 관리 솔루션에는 하나 이상의 보기 toovisualize 데이터 일반적으로 포함 됩니다.  이 문서 방법을 tooexport 뷰를 만들 hello 뷰 디자이너에서 설명 하 고 관리 솔루션에 포함 합니다. "
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
ms.openlocfilehash: 303861465014a27289f831332b3d95925c0ae66d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a><span data-ttu-id="be979-104">OMS(Operations Management Suite) 관리 솔루션의 보기(Preview)</span><span class="sxs-lookup"><span data-stu-id="be979-104">Views in Operations Management Suite (OMS) management solutions (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="be979-105">현재 Preview로 제공되는 OMS의 사용자 지정 솔루션 만들기에 대한 예비 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="be979-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="be979-106">아래에 설명 된 모든 스키마 주체 toochange입니다.</span><span class="sxs-lookup"><span data-stu-id="be979-106">Any schema described below is subject toochange.</span></span>    
>
>

<span data-ttu-id="be979-107">[Operations Management Suite (OMS)에서 관리 솔루션](operations-management-suite-solutions.md) 는 일반적으로 하나 이상의 보기 toovisualize 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="be979-107">[Management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions.md) will typically include one or more views toovisualize data.</span></span>  <span data-ttu-id="be979-108">이 문서에서 설명 하는 방법을 tooexport 뷰를 만들 hello 여 [뷰 디자이너](../log-analytics/log-analytics-view-designer.md) 관리 솔루션에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="be979-108">This article describes how tooexport a view created by hello [View Designer](../log-analytics/log-analytics-view-designer.md) and include it in a management solution.</span></span>  

> [!NOTE]
> <span data-ttu-id="be979-109">hello 샘플이이 문서에서 사용 하 여 매개 변수 및 필수 또는 일반적인 toomanagement 솔루션 중 하나에 설명 된 있는 변수 [Operations Management Suite (OMS)에서 관리 솔루션 만들기](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="be979-109">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="be979-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="be979-110">Prerequisites</span></span>
<span data-ttu-id="be979-111">이 문서에서는 하 이미 방법을 잘 알고 너무 가정[관리 솔루션을 만들어](operations-management-suite-solutions-creating.md) 및 솔루션 파일의 hello 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="be979-111">This article assumes that you're already familiar with how too[create a management solution](operations-management-suite-solutions-creating.md) and hello structure of a solution file.</span></span>

## <a name="overview"></a><span data-ttu-id="be979-112">개요</span><span class="sxs-lookup"><span data-stu-id="be979-112">Overview</span></span>
<span data-ttu-id="be979-113">만들 tooinclude 관리 솔루션에는 보기는 **리소스** hello에 대 한 [솔루션 파일](operations-management-suite-solutions-creating.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="be979-113">tooinclude a view in a management solution, you create a **resource** for it in hello [solution file](operations-management-suite-solutions-creating.md).</span></span>  <span data-ttu-id="be979-114">hello hello 보기의 세부 구성을 나타내는 JSON은 일반적으로 복잡 하지만 및 문제가 되지 일반적인 솔루션 작성자 수 toocreate 수동으로 수 있다고 합니다.</span><span class="sxs-lookup"><span data-stu-id="be979-114">hello JSON that describes hello view's detailed configuration is typically complex though and not something that a typical solution author would be able toocreate manually.</span></span>  <span data-ttu-id="be979-115">hello 가장 일반적인 방법은 hello를 사용 하 여 toocreate hello 뷰 [뷰 디자이너](../log-analytics/log-analytics-view-designer.md), 내보내고 해당 자세한 구성 toohello 솔루션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="be979-115">hello most common method is toocreate hello view using hello [View Designer](../log-analytics/log-analytics-view-designer.md), export it, and then add its detailed configuration toohello solution.</span></span>

<span data-ttu-id="be979-116">hello 기본 단계 tooadd 보기 tooa 솔루션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="be979-116">hello basic steps tooadd a view tooa solution are as follows.</span></span>  <span data-ttu-id="be979-117">각 단계는 아래 hello 섹션에서 더 자세히 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be979-117">Each step is described in further detail in hello sections below.</span></span>

1. <span data-ttu-id="be979-118">Hello 보기 tooa 파일을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="be979-118">Export hello view tooa file.</span></span>
2. <span data-ttu-id="be979-119">Hello 솔루션의 hello 보기 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="be979-119">Create hello view resource in hello solution.</span></span>
3. <span data-ttu-id="be979-120">Hello 세부 정보 보기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="be979-120">Add hello view details.</span></span>

## <a name="export-hello-view-tooa-file"></a><span data-ttu-id="be979-121">Hello 보기 tooa 파일 내보내기</span><span class="sxs-lookup"><span data-stu-id="be979-121">Export hello view tooa file</span></span>
<span data-ttu-id="be979-122">Hello 지침에 따라 [로그 분석 뷰 디자이너](../log-analytics/log-analytics-view-designer.md) tooexport 뷰 tooa 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="be979-122">Follow hello instructions at [Log Analytics View Designer](../log-analytics/log-analytics-view-designer.md) tooexport a view tooa file.</span></span>  <span data-ttu-id="be979-123">hello 내보낸된 파일은 될 JSON 형식으로 hello 동일 [hello 솔루션 파일로 요소](operations-management-suite-solutions-solution-file.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="be979-123">hello exported file will be in JSON format with hello same [elements as hello solution file](operations-management-suite-solutions-solution-file.md).</span></span>  

<span data-ttu-id="be979-124">hello **리소스** hello 보기 파일의 요소는 유형의 사용 하 여 리소스를 갖게 됩니다 **Microsoft.OperationalInsights/workspaces** 나타내는 hello OMS 작업 영역을 합니다.</span><span class="sxs-lookup"><span data-stu-id="be979-124">hello **resources** element of hello view file will have a resource with a type of **Microsoft.OperationalInsights/workspaces** that represents hello OMS workspace.</span></span>  <span data-ttu-id="be979-125">이 요소에는의 형식과 subelement 포함 될 **뷰** 하는 자세한 구성을 포함 하 hello 보기를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="be979-125">This element will have a subelement with a type of **views** that represents hello view and contains its detailed configuration.</span></span>  <span data-ttu-id="be979-126">이 요소의 hello 세부 정보 복사한 다음 솔루션에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="be979-126">You will copy hello details of this element and then copy it into your solution.</span></span>

## <a name="create-hello-view-resource-in-hello-solution"></a><span data-ttu-id="be979-127">Hello 솔루션에서 hello 보기 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="be979-127">Create hello view resource in hello solution</span></span>
<span data-ttu-id="be979-128">다음 보기 리소스 toohello hello 추가 **리소스** 솔루션 파일의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="be979-128">Add hello following view resource toohello **resources** element of your solution file.</span></span>  <span data-ttu-id="be979-129">이 작업에는 아래 설명된, 추가해야 하는 변수가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="be979-129">This uses variables that are described below that you must also add.</span></span>  <span data-ttu-id="be979-130">해당 hello 참고 **대시보드** 및 **OverviewTile** 속성 하는 자리 표시자 hello hello 내보낸된 보기 파일에서 해당 속성을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="be979-130">Note that hello **Dashboard** and **OverviewTile** properties are placeholders that you will overwrite with hello corresponding properties from hello exported view file.</span></span>

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

<span data-ttu-id="be979-131">Hello 솔루션 파일의 변수 toohello 변수 요소 다음에 오는 hello를 추가 하 고 솔루션에 대 한 hello 값 toothose 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="be979-131">Add hello following variables toohello variables element of hello solution file and replace hello values toothose for your solution.</span></span>

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of hello view."
    "ViewName": "Provide a name for hello view here."


<span data-ttu-id="be979-132">참고 내보낸된 보기 파일 에서만 hello 전체 보기 리소스를 복사할 수 toowork 솔루션에서 toomake hello에 대 한 변경 내용을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be979-132">Note that you could copy hello entire view resource from your exported view file, but you would need toomake hello following changes for it toowork in your solution.</span></span>  

* <span data-ttu-id="be979-133">hello **형식** hello 보기에 대 한 리소스에서 변경 toobe이 필요한 **뷰** 너무**Microsoft.OperationalInsights/workspaces**합니다.</span><span class="sxs-lookup"><span data-stu-id="be979-133">hello **type** for hello view resource needs toobe changed from **views** too**Microsoft.OperationalInsights/workspaces**.</span></span>
* <span data-ttu-id="be979-134">hello **이름** hello 보기 리소스에 대 한 속성 변경 toobe tooinclude hello 작업 영역 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="be979-134">hello **name** property for hello view resource needs toobe changed tooinclude hello workspace name.</span></span>
* <span data-ttu-id="be979-135">hello 작업 영역에 대 한 hello 종속성 toobe hello 작업 공간 리소스 hello 솔루션에 정의 되어 있지 이후 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be979-135">hello dependency on hello workspace needs toobe removed since hello workspace resource isn't defined in hello solution.</span></span>
* <span data-ttu-id="be979-136">**DisplayName** 속성 요구 toobe toohello 보기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="be979-136">**DisplayName** property needs toobe added toohello view.</span></span>  <span data-ttu-id="be979-137">hello **Id**, **이름**, 및 **DisplayName** 모두 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be979-137">hello **Id**, **Name**, and **DisplayName** must all match.</span></span>
* <span data-ttu-id="be979-138">매개 변수 이름을 변경 해야 toomatch hello 매개 변수 집합이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="be979-138">Parameter names must be changed toomatch hello required set of parameters.</span></span>
* <span data-ttu-id="be979-139">변수는 hello 솔루션에 정의 하 고 hello 적절 한 속성에 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be979-139">Variables should be defined in hello solution and used in hello appropriate properties.</span></span>

## <a name="add-hello-view-details"></a><span data-ttu-id="be979-140">Hello 뷰 세부 정보 추가</span><span class="sxs-lookup"><span data-stu-id="be979-140">Add hello view details</span></span>
<span data-ttu-id="be979-141">hello 보기 리소스 hello에 내보낸 파일은 hello에 두 개의 요소를 포함 하는 보기 **속성** 라는 요소 **대시보드** 및 **OverviewTile** hello를 포함 하는 hello 보기의 자세한 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="be979-141">hello view resource in hello exported view file will contain two elements in hello **properties** element named **Dashboard** and **OverviewTile** which contain hello detailed configuration of hello view.</span></span>  <span data-ttu-id="be979-142">이 두 요소 및 해당 내용을 hello에 복사한 **속성** 솔루션 파일에 hello 보기 리소스의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="be979-142">Copy these two elements and their contents into hello **properties** element of hello view resource in your solution file.</span></span>

## <a name="example"></a><span data-ttu-id="be979-143">예제</span><span class="sxs-lookup"><span data-stu-id="be979-143">Example</span></span>
<span data-ttu-id="be979-144">예를 들어 다음 예제는 hello는 보기를 통해 간단한 솔루션 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="be979-144">For example, hello following sample shows a simple solution file with a view.</span></span>  <span data-ttu-id="be979-145">줄임표 (...) hello에 대 한 표시 **대시보드** 및 **OverviewTile** 공간 원인에 대 한 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="be979-145">Ellipses (...) are shown for hello **Dashboard** and **OverviewTile** contents for space reasons.</span></span>

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




## <a name="next-steps"></a><span data-ttu-id="be979-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="be979-146">Next steps</span></span>
* <span data-ttu-id="be979-147">[관리 솔루션](operations-management-suite-solutions-creating.md)을 만드는 방법에 대한 자세한 내용을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="be979-147">Learn complete details of creating [management solutions](operations-management-suite-solutions-creating.md).</span></span>
* <span data-ttu-id="be979-148">[관리 솔루션에 Automation runbook](operations-management-suite-solutions-resources-automation.md)을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="be979-148">Include [Automation runbooks in your management solution](operations-management-suite-solutions-resources-automation.md).</span></span>
