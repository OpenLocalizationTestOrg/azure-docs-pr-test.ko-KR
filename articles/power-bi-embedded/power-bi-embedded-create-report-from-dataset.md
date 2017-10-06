---
title: "Power BI 포함 Azure에서 데이터 집합에서 새 보고서 aaaCreate | Microsoft Docs"
description: "Power BI Embedded 보고서는 이제 자체 응용 프로그램의 데이터 집합에서 만들 수 있습니다."
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
ms.openlocfilehash: 41a0a52e4c833313f495bb5ff14749203fef9b41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a><span data-ttu-id="a9324-103">Power BI Embedded의 데이터 집합에서 새 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="a9324-103">Create a new report from a dataset in Power BI Embedded</span></span>

<span data-ttu-id="a9324-104">Power BI Embedded 보고서는 이제 자체 응용 프로그램의 데이터 집합에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-104">Power BI Embedded reports can now be created from a dataset in your own application.</span></span> 

<span data-ttu-id="a9324-105">hello 인증 메서드는 보고서의 toothat 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-105">hello authentication method is similar toothat of report embed.</span></span> <span data-ttu-id="a9324-106">액세스 토큰을 특정 tooa 데이터 집합은 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-106">It is based on access tokens that are specific tooa dataset.</span></span> <span data-ttu-id="a9324-107">PowerBI.com에 사용되는 토큰은AAD(Azure Active Directory)에서 발급되고 Power BI Embedded 토큰은 사용자의 자체 서비스에서 발급됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-107">Tokens used for PowerBI.com are issued by Azure Active Directory (AAD) and Power BI Embedded tokens are issued by your own service.</span></span>

<span data-ttu-id="a9324-108">Hello createing 포함 된 보고서를 특정 데이터 집합에 대해 발급 한 토큰 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-108">When createing an Embedded report, hello tokens issued are for a specific dataset.</span></span> <span data-ttu-id="a9324-109">토큰을 연결 해야 할지 hello로 URL을 포함 hello에 동일한 요소 tooensure 각각에 고유한 토큰이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-109">Tokens should be associated with hello embed URL on hello same element tooensure each has a unique token.</span></span> <span data-ttu-id="a9324-110">순서로 toocreate 포함 된 보고서, *Dataset.Read 및 Workspace.Report.Create* hello 액세스 토큰의 범위를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-110">In order toocreate an Embedded report, *Dataset.Read and Workspace.Report.Create* scopes must be provided in hello access token.</span></span>

## <a name="create-access-token-needed-toocreate-new-report"></a><span data-ttu-id="a9324-111">액세스 토큰 필요한 toocreate 새 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="a9324-111">Create access token needed toocreate new report</span></span>

<span data-ttu-id="a9324-112">Power BI Embedded는 HMAC 서명 JSON Web Token에 해당하는 Embed 토큰을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-112">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="a9324-113">hello 토큰은 Azure Power BI 포함 작업 영역 컬렉션에서 hello 액세스 키로 서명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-113">hello tokens are signed with hello access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="a9324-114">기본적으로 토큰을 포함, 됩니다 하 읽기 사용된 tooprovide 응용 프로그램으로 tooa 보고서 tooembed만 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-114">Embed tokens, by default, are used tooprovide read only access tooa report tooembed into an application.</span></span> <span data-ttu-id="a9324-115">Embed 토큰은 특정 보고서에 대해 발급되며 Embed URL에 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-115">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="a9324-116">액세스 토큰 hello 액세스 키가 사용 되는 toosign/암호화 hello 토큰으로 hello 서버에 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-116">Access tokens should be created on hello server as hello access keys are used toosign/encrypt hello tokens.</span></span> <span data-ttu-id="a9324-117">방법에 대 한 내용은 toocreate, 액세스 토큰이 참조 [인증 하 고 Power BI embedded 허가](power-bi-embedded-app-token-flow.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-117">For information on how toocreate an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="a9324-118">또한 hello을 검토할 수 [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) 메서드.</span><span class="sxs-lookup"><span data-stu-id="a9324-118">You can also review hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="a9324-119">이 모양을 hello.NET SDK를 사용 하 여 Power BI에 대 한 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-119">Here is an example of what this would look like using hello .NET SDK for Power BI.</span></span>

<span data-ttu-id="a9324-120">이 예제에는 toocreat hello에 대 한 새 보고서에 원하는 데이터 집합 id 우리의 개가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-120">In this example, we have our dataset id that we want toocreat hello new report on.</span></span> <span data-ttu-id="a9324-121">또한 tooadd hello 범위에 대 한 필요 *Dataset.Read 및 Workspace.Report.Create*합니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-121">We also need tooadd hello scopes for *Dataset.Read and Workspace.Report.Create*.</span></span>

<span data-ttu-id="a9324-122">hello *PowerBIToken 클래스* hello를 설치 해야 [Power BI 핵심 NuGut 패키지](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-122">hello *PowerBIToken class* requires that you install hello [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="a9324-123">**NuGet 패키지 설치**</span><span class="sxs-lookup"><span data-stu-id="a9324-123">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="a9324-124">**C# 코드**</span><span class="sxs-lookup"><span data-stu-id="a9324-124">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a><span data-ttu-id="a9324-125">비어 있는 새 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="a9324-125">Create a new blank report</span></span>

<span data-ttu-id="a9324-126">Hello 순서 toocreate 새 보고서에서에서 만들 구성을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-126">In order toocreate a new report, hello create configuration should be provided.</span></span> <span data-ttu-id="a9324-127">Toocreate hello 보고서를 원하는 hello 액세스 토큰, hello embedURL 및 hello datasetID 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-127">This should include hello access token, hello embedURL and hello datasetID that we want toocreate hello report against.</span></span> <span data-ttu-id="a9324-128">Hello nuget을 설치 하는이 위해서는 [Power BI JavaScript 패키지](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-128">This requires that you install hello nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="a9324-129">hello embedUrl https://embedded.powerbi.com/appTokenReportEmbed 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-129">hello embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="a9324-130">Hello를 사용할 수 있습니다 [JavaScript 보고서 포함 예제](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-130">You can use hello [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest functionality.</span></span> <span data-ttu-id="a9324-131">또한 hello 사용할 수 있는 다른 작업에 대 한 코드 예제를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-131">It also gives code examples for hello different operations that are available.</span></span>

<span data-ttu-id="a9324-132">**NuGet 패키지 설치**</span><span class="sxs-lookup"><span data-stu-id="a9324-132">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="a9324-133">**JavaScript 코드**</span><span class="sxs-lookup"><span data-stu-id="a9324-133">**JavaScript code**</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);
```

<span data-ttu-id="a9324-134">호출 *powerbi.createReport()* 편집 모드에 빈 캔버스 hello 내에 표시 하면 *div* 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-134">Calling *powerbi.createReport()* will make a blank canvas in edit mode appear within hello *div* element.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a><span data-ttu-id="a9324-135">새 보고서 저장</span><span class="sxs-lookup"><span data-stu-id="a9324-135">Save new reports</span></span>

<span data-ttu-id="a9324-136">hello 보고서 생성 되지 것입니다 실제로 hello를 호출할 때까지 **다른 이름으로 저장** 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-136">hello report will not actually be created until you call hello **save as** operation.</span></span> <span data-ttu-id="a9324-137">파일 메뉴에서 또는 JavaScript에서 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-137">This can be done from file menu or from JavaScript.</span></span>

```
 // Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);
    
    var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);
```

> [!IMPORTANT]
> <span data-ttu-id="a9324-138">**다른 이름으로 저장**을 호출해야만 새 보고서가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-138">A new report is created only after **save as** is called.</span></span> <span data-ttu-id="a9324-139">을 저장 한 후 hello 캔버스 편집 모드 및 하지 hello 보고서에 hello 데이터 집합을 계속 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-139">After you save, hello canvas will still show hello dataset in edit mode and not hello report.</span></span> <span data-ttu-id="a9324-140">다른 보고서의 경우 처럼 tooreload hello에 대 한 새 보고서를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-140">You will need tooreload hello new report like you would any other report.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-hello-new-report"></a><span data-ttu-id="a9324-141">Hello 새 보고서를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-141">Load hello new report</span></span>

<span data-ttu-id="a9324-142">Hello 새 보고서와 함께 순서 toointeract tooembed hello 새 보고서에 맞게 hello 응용 프로그램을 일반 보고서, 의미, 새 토큰을 포함 하는 동일한 방식으로 발급 해야 하는 hello 및 호출 hello에이 메서드를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-142">In order toointeract with hello new report you need tooembed it in hello same way hello application embeds a regular report, meaning, a new token must be issued specifically for hello new report and then call hello embed method.</span></span>

```
<div id="reportContainer"></div>
  
var embedConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MJ',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: '5dac7a4a-4452-46b3-99f6-a25915e0fe54',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
```

## <a name="automate-save-and-load-of-a-new-report-using-hello-saved-event"></a><span data-ttu-id="a9324-143">저장 자동화 및 이벤트를 "저장" hello를 사용 하 여 새 보고서 로드</span><span class="sxs-lookup"><span data-stu-id="a9324-143">Automate save and load of a new report using hello "saved" event</span></span>

<span data-ttu-id="a9324-144">"다른 이름으로 저장" 순서 tooautomate hello 프로세스에서의 이벤트를 "저장" hello 사용 하 여 다음 수 있게 하는 hello 새 보고서를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-144">In order tooautomate hello process of "save as" and then loading hello new report you can make use of hello "saved" Event.</span></span> <span data-ttu-id="a9324-145">Hello 저장 작업이 완료 되 고 새 reportId hello, 보고서 이름, hello 이전 reportId (있는 경우)를 포함 하는 Json 개체가 반환 하 고 hello 작업에 다른 이름으로 저장 하면 또는 저장이 이벤트가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-145">This event is fired when hello save operation is complete and it returns a Json object containing hello new reportId, report name, hello old reportId(if there was one) and if hello operation was saveAs or save.</span></span>

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

<span data-ttu-id="a9324-146">hello 새 reportId 걸리고 hello 새 토큰을 만들 것으로 구성 된 hello 새 보고서를 포함 하는 tooAutomate hello 프로세스 "저장" hello 이벤트에서 수신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9324-146">tooAutomate hello process you can listen on hello "saved" event, take hello new reportId, create hello new token and embed hello new report with it.</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);


   var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);

    // report.on will add an event handler which prints tooLog window.
    report.on("saved", function(event) {
        
         // get new Token
         var newReportId =  event.detail.reportObjectId;

        // create new Token. This is a function that hello application should provide
        var newToken = createAccessToken(newReportId,scopes /*provide hello wanted scopes*/);
        
        
    var embedConfiguration = {
        accessToken: newToken ,
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: newReportId,
    };

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
       
   // report.off removes a given event handler if it exists.
   report.off("saved");
    });
```

## <a name="see-also"></a><span data-ttu-id="a9324-147">참고 항목</span><span class="sxs-lookup"><span data-stu-id="a9324-147">See also</span></span>

[<span data-ttu-id="a9324-148">샘플 시작</span><span class="sxs-lookup"><span data-stu-id="a9324-148">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="a9324-149">보고서 저장</span><span class="sxs-lookup"><span data-stu-id="a9324-149">Save reports</span></span>](power-bi-embedded-save-reports.md)  
[<span data-ttu-id="a9324-150">보고서 포함</span><span class="sxs-lookup"><span data-stu-id="a9324-150">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="a9324-151">Power BI Embedded에서 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="a9324-151">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="a9324-152">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="a9324-152">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="a9324-153">JavaScript Embed 샘플</span><span class="sxs-lookup"><span data-stu-id="a9324-153">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="a9324-154">Power BI Core NuGut 패키지</span><span class="sxs-lookup"><span data-stu-id="a9324-154">Power BI Core NuGut Package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[<span data-ttu-id="a9324-155">Power BI JavaScript 패키지</span><span class="sxs-lookup"><span data-stu-id="a9324-155">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="a9324-156">궁금한 점이 더 있나요?</span><span class="sxs-lookup"><span data-stu-id="a9324-156">More questions?</span></span> [<span data-ttu-id="a9324-157">Power BI 커뮤니티 hello를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a9324-157">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
