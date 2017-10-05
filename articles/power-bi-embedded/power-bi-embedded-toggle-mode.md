---
title: "Azure Power BI Embedded에서 보고서에 대해 보기 및 편집 모드 간 전환 | Microsoft Docs"
description: "Power BI Embedded 내에서 보고서에 대해 보기 및 편집 모드 간을 전환하는 방법을 알아봅니다."
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
ms.openlocfilehash: f73bf05b41523a5833cc9366fb84cb7021b4b7a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="toggle-between-view-and-edit-mode-for-reports-in-power-bi-embedded"></a><span data-ttu-id="8ca49-103">Power BI Embedded에서 보고서에 대해 보기 및 편집 모드 간 전환</span><span class="sxs-lookup"><span data-stu-id="8ca49-103">Toggle between view and edit mode for reports in Power BI Embedded</span></span>

<span data-ttu-id="8ca49-104">Power BI Embedded 내에서 보고서에 대해 보기 및 편집 모드 간을 전환하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8ca49-104">Learn how to toggle between view and edit mode for your reports within Power BI Embedded.</span></span>

## <a name="creating-an-access-token"></a><span data-ttu-id="8ca49-105">액세스 토큰 만들기</span><span class="sxs-lookup"><span data-stu-id="8ca49-105">Creating an access token</span></span>

<span data-ttu-id="8ca49-106">보고서를 보고 편집할 수 있는 기능을 제공하는 액세스 토큰을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca49-106">You will need to create an access token that gives you the ability to both view and edit a report.</span></span> <span data-ttu-id="8ca49-107">보고서를 편집하고 저장하려면 **Report.ReadWrite** 토큰 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca49-107">To edit and save a report, you will need the **Report.ReadWrite** token permission.</span></span> <span data-ttu-id="8ca49-108">자세한 내용은 [Power BI Embedded에서 인증 및 권한 부여](power-bi-embedded-app-token-flow.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8ca49-108">For more information, see [Authenticating and authorizing in Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

> [!NOTE]
> <span data-ttu-id="8ca49-109">이러한 조건이 충족될 경우 기존 보고서를 편집하고 변경 내용을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca49-109">This will allow you to edit and save changes to an existing report.</span></span> <span data-ttu-id="8ca49-110">**다른 이름으로 저장**을 지원하는 기능을 원할 경우 추가 권한을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca49-110">If you would also like the function of supporting **Save As**, you will need to supply additional permissions.</span></span> <span data-ttu-id="8ca49-111">자세한 내용은 [범위](power-bi-embedded-app-token-flow.md#scopes)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8ca49-111">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Report.ReadWrite";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="embed-configuration"></a><span data-ttu-id="8ca49-112">Embed 구성</span><span class="sxs-lookup"><span data-stu-id="8ca49-112">Embed configuration</span></span>

<span data-ttu-id="8ca49-113">편집 모드에 있을 때 저장 단추를 보려면 사용 권한과 viewMode를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca49-113">You will need to supply permissions and a viewMode in order to see the save button when in edit mode.</span></span> <span data-ttu-id="8ca49-114">자세한 내용은 [Embed 구성 정보](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8ca49-114">For more information, see [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span></span>

<span data-ttu-id="8ca49-115">예를 들어 JavaScript에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca49-115">For example in JavaScript:</span></span>

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
        permissions: models.Permissions.ReadWrite /*both save & save as buttons will be visible*/,
        viewMode: models.ViewMode.View,
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

<span data-ttu-id="8ca49-116">여기서는 **models.ViewMode.View**로 설정된 **viewMode**를 기준으로 보기 모드에서 보고서를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca49-116">This will indicate to embed the report in view mode based on **viewMode** being set to **models.ViewMode.View**.</span></span>

## <a name="view-mode"></a><span data-ttu-id="8ca49-117">보기 모드</span><span class="sxs-lookup"><span data-stu-id="8ca49-117">View mode</span></span>

<span data-ttu-id="8ca49-118">편집 모드인 경우 다음 JavaScript를 사용하여 보기 모드로 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca49-118">You can use the following JavaScript to switch into view mode, if you are in edit mode.</span></span>

```
// Get a reference to the embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference to the embedded report.
report = powerbi.get(reportContainer);

// Switch to view mode.
report.switchMode("view");

```

## <a name="edit-mode"></a><span data-ttu-id="8ca49-119">편집 모드</span><span class="sxs-lookup"><span data-stu-id="8ca49-119">Edit mode</span></span>

<span data-ttu-id="8ca49-120">보기 모드인 경우 다음 JavaScript를 사용하여 편집 모드로 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca49-120">You can use the following JavaScript to switch into edit mode, if you are in view mode.</span></span>

```
// Get a reference to the embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference to the embedded report.
report = powerbi.get(reportContainer);

// Switch to edit mode.
report.switchMode("edit");

```

## <a name="see-also"></a><span data-ttu-id="8ca49-121">참고 항목</span><span class="sxs-lookup"><span data-stu-id="8ca49-121">See also</span></span>

[<span data-ttu-id="8ca49-122">샘플 시작</span><span class="sxs-lookup"><span data-stu-id="8ca49-122">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="8ca49-123">보고서 포함</span><span class="sxs-lookup"><span data-stu-id="8ca49-123">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="8ca49-124">Power BI Embedded에서 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="8ca49-124">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="8ca49-125">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="8ca49-125">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="8ca49-126">JavaScript Embed 샘플</span><span class="sxs-lookup"><span data-stu-id="8ca49-126">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="8ca49-127">PowerBI-CSharp Git 리포지토리</span><span class="sxs-lookup"><span data-stu-id="8ca49-127">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="8ca49-128">PowerBI-Node Git 리포지토리</span><span class="sxs-lookup"><span data-stu-id="8ca49-128">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="8ca49-129">궁금한 점이 더 있나요?</span><span class="sxs-lookup"><span data-stu-id="8ca49-129">More questions?</span></span> [<span data-ttu-id="8ca49-130">Power BI 커뮤니티를 이용하세요.</span><span class="sxs-lookup"><span data-stu-id="8ca49-130">Try the Power BI Community</span></span>](http://community.powerbi.com/)
