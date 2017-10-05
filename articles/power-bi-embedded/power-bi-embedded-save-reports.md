---
title: "Azure Power BI Embedded에서 보고서 저장 | Microsoft Docs"
description: "Power BI Embedded 내에서 보고서를 저장하는 방법을 알아봅니다. 성공적인 작업을 위해서는 적절한 사용 권한이 필요합니다."
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: ad895004cc2972f2ded81566186325a16d401151
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="save-reports-in-power-bi-embedded"></a><span data-ttu-id="24767-104">Power BI Embedded에서 보고서 저장</span><span class="sxs-lookup"><span data-stu-id="24767-104">Save reports in Power BI Embedded</span></span>

<span data-ttu-id="24767-105">Power BI Embedded 내에서 보고서를 저장하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="24767-105">Learn how to save reports within Power BI embedded.</span></span> <span data-ttu-id="24767-106">성공적인 작업을 위해서는 적절한 사용 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="24767-106">This requires proper permissions in order to work successfully.</span></span>

<span data-ttu-id="24767-107">Power BI Embedded 내에서 기존 보고서를 편집하고 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24767-107">Within Power BI Embedded, you can edit existing reports and save them.</span></span> <span data-ttu-id="24767-108">새 보고서를 만들고 새 보고서로 저장하여 보고서를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24767-108">You can also create a new report and save as a new report to create one.</span></span>

<span data-ttu-id="24767-109">보고서를 저장하려면 먼저 올바른 범위를 지정하여 특정 보고서에 대한 토큰을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24767-109">In order to save a report you first need to create a token for the specific report with the right scopes:</span></span>

* <span data-ttu-id="24767-110">저장을 사용하려면 Report.ReadWrite 범위가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="24767-110">To enable save Report.ReadWrite scope is required</span></span>
* <span data-ttu-id="24767-111">다른 이름으로 저장을 사용하려면 Report.Read 및 Workspace.Report.Copy 범위가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="24767-111">To enable save as, Report.Read and Workspace.Report.Copy scopes are required</span></span>
* <span data-ttu-id="24767-112">저장 및 다른 이름으로 저장을 사용하려면 Report.ReadWrite 및 Workspace.Report.Copy가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="24767-112">To enable save and save as, Report.ReadWrite and Workspace.Report.Copy are requierd</span></span>

<span data-ttu-id="24767-113">파일 메뉴에서 적절한 저장/다른 이름으로 저장 단추를 각각 사용하기 위해서는 보고서를 포함할 때 Embed 구성에서 적절한 사용 권한을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24767-113">Respectively in order to enable the right save/save as buttons in file menu you need to provide the right permission in the Embed configuration when you Embed the report:</span></span>

* <span data-ttu-id="24767-114">models.Permissions.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="24767-114">models.Permissions.ReadWrite</span></span>
* <span data-ttu-id="24767-115">models.Permissions.Copy</span><span class="sxs-lookup"><span data-stu-id="24767-115">models.Permissions.Copy</span></span>
* <span data-ttu-id="24767-116">models.Permissions.All</span><span class="sxs-lookup"><span data-stu-id="24767-116">models.Permissions.All</span></span>

> [!NOTE]
> <span data-ttu-id="24767-117">액세스 토큰에도 적절한 범위가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="24767-117">Your access token also needs the appropriate scopes.</span></span> <span data-ttu-id="24767-118">자세한 내용은 [범위](power-bi-embedded-app-token-flow.md#scopes)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24767-118">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span></span>

## <a name="embed-report-in-edit-mode"></a><span data-ttu-id="24767-119">편집 모드에서 보고서 포함</span><span class="sxs-lookup"><span data-stu-id="24767-119">Embed report in edit mode</span></span>

<span data-ttu-id="24767-120">앱 내에서 편집 모드로 보고서를 포함하려고 하므로 Embed 구성에서 올바른 속성을 전달하고 powerbi.embed()를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="24767-120">Let's say you want to Embed a report in edit mode inside your app, to do so just pass the right properties in Embed configuration and call powerbi.embed().</span></span> <span data-ttu-id="24767-121">편집 모드에 있을 때 저장 및 다른 이름으로 저장 단추를 보려면 사용 권한과 viewMode를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24767-121">You will need to supply permissions and a viewMode in order to see the save and save as buttons when in edit mode.</span></span> <span data-ttu-id="24767-122">자세한 내용은 [Embed 구성 정보](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24767-122">For more information, see [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span></span>

<span data-ttu-id="24767-123">예를 들어 JavaScript에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="24767-123">For example in JavaScript:</span></span>

```
   <div id="reportContainer"></div>

    // Get models. Models, it contains enums that can be used.
    var models = window['powerbi-client'].models;

    // Embed configuration used to describe the what and how to embed.
    // This object is used when calling powerbi.embed.
    // This also includes settings and options such as filters.
    // You can find more information at https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details.
    var config= {
        type: 'report',
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        id:  '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
        permissions: models.Permissions.All /*both save & save as buttons will be visible*/,
        viewMode: models.ViewMode.Edit,
        settings: {
            filterPaneEnabled: true,
            navContentPaneEnabled: true
        }
    };

    // Get a reference to the embedded report HTML element
    var reportContainer = $('#reportContainer')[0];

    // Embed the report and display it within the div container.
    var report = powerbi.embed(reportContainer, config);
```

<span data-ttu-id="24767-124">이제 보고서가 편집 모드에서 앱에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="24767-124">Now a report will be embedded in your app in edit mode.</span></span>

## <a name="save-report"></a><span data-ttu-id="24767-125">보고서 저장</span><span class="sxs-lookup"><span data-stu-id="24767-125">Save report</span></span>

<span data-ttu-id="24767-126">적절한 토큰 및 사용 권한을 사용하여 편집 모드에서 보고서를 포함한 후에는 파일 메뉴 또는 javascript에서 보고서를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24767-126">After Embbeding the report in edit mode with the right token and permissions you can save the report from the file menu or from javascript:</span></span>

```
 // Get a reference to the embedded report.
    report = powerbi.get(reportContainer);

 // Save report
    report.save();
```

## <a name="save-as"></a><span data-ttu-id="24767-127">다른 이름으로 저장</span><span class="sxs-lookup"><span data-stu-id="24767-127">Save as</span></span>

```
// Get a reference to the embedded report.
    report = powerbi.get(reportContainer);
    
    var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);
```

> [!IMPORTANT]
> <span data-ttu-id="24767-128">*다른 이름으로 저장* 이후에만 새 보고서가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="24767-128">Only after *save as* is a new report created.</span></span> <span data-ttu-id="24767-129">저장 후에는 여전히 캔버스에서 새 보고서가 아닌 이전 보고서가 편집 모드로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="24767-129">After the save, the canvas is still showing the old report in edit mode and not the new report.</span></span> <span data-ttu-id="24767-130">만들어진 새 보고서를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24767-130">You will need to embed the new report that was created.</span></span> <span data-ttu-id="24767-131">이렇게 하려면 보고서가 만들어질 때마다 새 액세스 토큰이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="24767-131">This requires a new access token as they are created per report.</span></span>

<span data-ttu-id="24767-132">그런 다음 *다른 이름으로 저장* 후에 새 보고서를 로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24767-132">You will then need to load the new report after a *save as*.</span></span> <span data-ttu-id="24767-133">이것은 보고서를 포함하는 것과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="24767-133">This is similar to embedding any report.</span></span>

```
<div id="reportContainer"></div>
  
var embedConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MJ',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: '5dac7a4a-4452-46b3-99f6-a25915e0fe54',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
```

## <a name="see-also"></a><span data-ttu-id="24767-134">참고 항목</span><span class="sxs-lookup"><span data-stu-id="24767-134">See also</span></span>

[<span data-ttu-id="24767-135">샘플 시작</span><span class="sxs-lookup"><span data-stu-id="24767-135">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="24767-136">보고서 포함</span><span class="sxs-lookup"><span data-stu-id="24767-136">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="24767-137">데이터 집합에서 새 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="24767-137">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="24767-138">Power BI Embedded에서 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="24767-138">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="24767-139">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="24767-139">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="24767-140">JavaScript Embed 샘플</span><span class="sxs-lookup"><span data-stu-id="24767-140">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="24767-141">궁금한 점이 더 있나요?</span><span class="sxs-lookup"><span data-stu-id="24767-141">More questions?</span></span> [<span data-ttu-id="24767-142">Power BI 커뮤니티를 이용하세요.</span><span class="sxs-lookup"><span data-stu-id="24767-142">Try the Power BI Community</span></span>](http://community.powerbi.com/)

