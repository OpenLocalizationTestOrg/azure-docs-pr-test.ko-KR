---
title: "Power BI 포함 Azure에서 보고서에 대 한 보기와 편집 모드 간에 aaaToggle | Microsoft Docs"
description: "자세한 방법을 Power BI 포함 내 보고서에 대 한 보기와 편집 모드 간에 tootoggle 합니다."
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
ms.openlocfilehash: c9e3da5f9ae74d221af650adebde7c9d83b38a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="toggle-between-view-and-edit-mode-for-reports-in-power-bi-embedded"></a><span data-ttu-id="1d8a9-103">Power BI Embedded에서 보고서에 대해 보기 및 편집 모드 간 전환</span><span class="sxs-lookup"><span data-stu-id="1d8a9-103">Toggle between view and edit mode for reports in Power BI Embedded</span></span>

<span data-ttu-id="1d8a9-104">자세한 방법을 Power BI 포함 내 보고서에 대 한 보기와 편집 모드 간에 tootoggle 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8a9-104">Learn how tootoggle between view and edit mode for your reports within Power BI Embedded.</span></span>

## <a name="creating-an-access-token"></a><span data-ttu-id="1d8a9-105">액세스 토큰 만들기</span><span class="sxs-lookup"><span data-stu-id="1d8a9-105">Creating an access token</span></span>

<span data-ttu-id="1d8a9-106">Toocreate hello 기능 tooboth 보기 및 보고서를 편집 하면 액세스 토큰이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8a9-106">You will need toocreate an access token that gives you hello ability tooboth view and edit a report.</span></span> <span data-ttu-id="1d8a9-107">tooedit 보고서를 저장 해야 hello 및 **Report.ReadWrite** 권한 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="1d8a9-107">tooedit and save a report, you will need hello **Report.ReadWrite** token permission.</span></span> <span data-ttu-id="1d8a9-108">자세한 내용은 [Power BI Embedded에서 인증 및 권한 부여](power-bi-embedded-app-token-flow.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d8a9-108">For more information, see [Authenticating and authorizing in Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1d8a9-109">Tooedit를 허용 되 고 변경 내용을 tooan 기존 보고서를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8a9-109">This will allow you tooedit and save changes tooan existing report.</span></span> <span data-ttu-id="1d8a9-110">Hello 함수를 지원할도 원하면 **다른 이름으로 저장**, toosupply 추가 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8a9-110">If you would also like hello function of supporting **Save As**, you will need toosupply additional permissions.</span></span> <span data-ttu-id="1d8a9-111">자세한 내용은 [범위](power-bi-embedded-app-token-flow.md#scopes)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d8a9-111">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Report.ReadWrite";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="embed-configuration"></a><span data-ttu-id="1d8a9-112">Embed 구성</span><span class="sxs-lookup"><span data-stu-id="1d8a9-112">Embed configuration</span></span>

<span data-ttu-id="1d8a9-113">Toosupply 사용 권한 및 save 편집 모드에 있을 때 단추 순서 toosee hello에 viewMode 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8a9-113">You will need toosupply permissions and a viewMode in order toosee hello save button when in edit mode.</span></span> <span data-ttu-id="1d8a9-114">자세한 내용은 [Embed 구성 정보](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d8a9-114">For more information, see [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span></span>

<span data-ttu-id="1d8a9-115">예를 들어 JavaScript에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8a9-115">For example in JavaScript:</span></span>

```
   <div id="reportContainer"></div>

    // Get models. Models, it contains enums that can be used.
    var models = window['powerbi-client'].models;

    // Embed configuration used toodescribe hello what and how tooembed.
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

    // Get a reference toohello embedded report HTML element
    var reportContainer = $('#reportContainer')[0];

    // Embed hello report and display it within hello div container.
    var report = powerbi.embed(reportContainer, config);
```

<span data-ttu-id="1d8a9-116">이 기반으로 하는 보기 모드에서 tooembed hello 보고서 나타냅니다 **viewMode** 너무 설정**모델. ViewMode.View**합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8a9-116">This will indicate tooembed hello report in view mode based on **viewMode** being set too**models.ViewMode.View**.</span></span>

## <a name="view-mode"></a><span data-ttu-id="1d8a9-117">보기 모드</span><span class="sxs-lookup"><span data-stu-id="1d8a9-117">View mode</span></span>

<span data-ttu-id="1d8a9-118">편집 모드에 있는 경우 JavaScript tooswitch 보기 모드에 따라 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d8a9-118">You can use hello following JavaScript tooswitch into view mode, if you are in edit mode.</span></span>

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooview mode.
report.switchMode("view");

```

## <a name="edit-mode"></a><span data-ttu-id="1d8a9-119">편집 모드</span><span class="sxs-lookup"><span data-stu-id="1d8a9-119">Edit mode</span></span>

<span data-ttu-id="1d8a9-120">모드는 보이는 경우 hello JavaScript tooswitch 편집 모드에 따라 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d8a9-120">You can use hello following JavaScript tooswitch into edit mode, if you are in view mode.</span></span>

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooedit mode.
report.switchMode("edit");

```

## <a name="see-also"></a><span data-ttu-id="1d8a9-121">참고 항목</span><span class="sxs-lookup"><span data-stu-id="1d8a9-121">See also</span></span>

[<span data-ttu-id="1d8a9-122">샘플 시작</span><span class="sxs-lookup"><span data-stu-id="1d8a9-122">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="1d8a9-123">보고서 포함</span><span class="sxs-lookup"><span data-stu-id="1d8a9-123">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="1d8a9-124">Power BI Embedded에서 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="1d8a9-124">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="1d8a9-125">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="1d8a9-125">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="1d8a9-126">JavaScript Embed 샘플</span><span class="sxs-lookup"><span data-stu-id="1d8a9-126">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="1d8a9-127">PowerBI-CSharp Git 리포지토리</span><span class="sxs-lookup"><span data-stu-id="1d8a9-127">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="1d8a9-128">PowerBI-Node Git 리포지토리</span><span class="sxs-lookup"><span data-stu-id="1d8a9-128">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="1d8a9-129">궁금한 점이 더 있나요?</span><span class="sxs-lookup"><span data-stu-id="1d8a9-129">More questions?</span></span> [<span data-ttu-id="1d8a9-130">Power BI 커뮤니티 hello를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="1d8a9-130">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
