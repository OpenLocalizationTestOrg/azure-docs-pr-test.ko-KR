---
title: "Azure Power BI Embedded의 데이터 집합에서 새 보고서 만들기 | Microsoft Docs"
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
ms.openlocfilehash: 457f53aa76059dbb2faed6b264102f1f59b9918a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a><span data-ttu-id="34252-103">Power BI Embedded의 데이터 집합에서 새 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="34252-103">Create a new report from a dataset in Power BI Embedded</span></span>

<span data-ttu-id="34252-104">Power BI Embedded 보고서는 이제 자체 응용 프로그램의 데이터 집합에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34252-104">Power BI Embedded reports can now be created from a dataset in your own application.</span></span> 

<span data-ttu-id="34252-105">인증 방법은 보고서 포함의 경우와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="34252-105">The authentication method is similar to that of report embed.</span></span> <span data-ttu-id="34252-106">이 방법은 특정 데이터 집합에만 적용되는 액세스 토큰을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="34252-106">It is based on access tokens that are specific to a dataset.</span></span> <span data-ttu-id="34252-107">PowerBI.com에 사용되는 토큰은AAD(Azure Active Directory)에서 발급되고 Power BI Embedded 토큰은 사용자의 자체 서비스에서 발급됩니다.</span><span class="sxs-lookup"><span data-stu-id="34252-107">Tokens used for PowerBI.com are issued by Azure Active Directory (AAD) and Power BI Embedded tokens are issued by your own service.</span></span>

<span data-ttu-id="34252-108">포함된 보고서를 만드는 경우 발급되는 토큰은 특정 데이터 집합에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="34252-108">When createing an Embedded report, the tokens issued are for a specific dataset.</span></span> <span data-ttu-id="34252-109">각각이 고유한 토큰을 갖도록 하기 위해 토큰을 같은 요소의 Embed URL에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34252-109">Tokens should be associated with the embed URL on the same element to ensure each has a unique token.</span></span> <span data-ttu-id="34252-110">포함된 보고서를 만들기 위해 액세스 토큰에 *Dataset.Read 및 Workspace.Report.Create* 범위를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34252-110">In order to create an Embedded report, *Dataset.Read and Workspace.Report.Create* scopes must be provided in the access token.</span></span>

## <a name="create-access-token-needed-to-create-new-report"></a><span data-ttu-id="34252-111">새 보고서를 만드는 데 필요한 액세스 토큰 만들기</span><span class="sxs-lookup"><span data-stu-id="34252-111">Create access token needed to create new report</span></span>

<span data-ttu-id="34252-112">Power BI Embedded는 HMAC 서명 JSON Web Token에 해당하는 Embed 토큰을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="34252-112">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="34252-113">이러한 토큰은 Azure Power BI Embedded 작업 영역 컬렉션의 액세스 키로 서명됩니다.</span><span class="sxs-lookup"><span data-stu-id="34252-113">The tokens are signed with the access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="34252-114">기본적으로 응용 프로그램에 포함할 보고서에 대해 읽기 전용 액세스를 제공하기 위해 Embed 토큰이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="34252-114">Embed tokens, by default, are used to provide read only access to a report to embed into an application.</span></span> <span data-ttu-id="34252-115">Embed 토큰은 특정 보고서에 대해 발급되며 Embed URL에 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34252-115">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="34252-116">서명/토큰 암호화에 액세스 키가 사용되므로 서버에서 액세스 토큰을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34252-116">Access tokens should be created on the server as the access keys are used to sign/encrypt the tokens.</span></span> <span data-ttu-id="34252-117">액세스 토큰을 만드는 방법에 대한 자세한 내용은 [Power BI Embedded에서 인증 및 권한 부여](power-bi-embedded-app-token-flow.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="34252-117">For information on how to create an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="34252-118">[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) 메서드를 검토할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34252-118">You can also review the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="34252-119">다음은 Power BI용 .NET SDK를 사용할 경우의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="34252-119">Here is an example of what this would look like using the .NET SDK for Power BI.</span></span>

<span data-ttu-id="34252-120">이 예제에는 새 보고서를 만들 데이터 집합 ID가 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="34252-120">In this example, we have our dataset id that we want to creat the new report on.</span></span> <span data-ttu-id="34252-121">*Dataset.Read 및 Workspace.Report.Create*의 범위도 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34252-121">We also need to add the scopes for *Dataset.Read and Workspace.Report.Create*.</span></span>

<span data-ttu-id="34252-122">*PowerBIToken 클래스*를 사용하려면 [Power BI Core NuGut 패키지](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34252-122">The *PowerBIToken class* requires that you install the [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="34252-123">**NuGet 패키지 설치**</span><span class="sxs-lookup"><span data-stu-id="34252-123">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="34252-124">**C# 코드**</span><span class="sxs-lookup"><span data-stu-id="34252-124">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a><span data-ttu-id="34252-125">비어 있는 새 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="34252-125">Create a new blank report</span></span>

<span data-ttu-id="34252-126">새 보고서를 만들기 위해 만들기 구성이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="34252-126">In order to create a new report, the create configuration should be provided.</span></span> <span data-ttu-id="34252-127">여기에는 보고서를 만들 액세스 토큰, embedURL 및 datasetID가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="34252-127">This should include the access token, the embedURL and the datasetID that we want to create the report against.</span></span> <span data-ttu-id="34252-128">이렇게 하려면 nuget [Power BI JavaScript 패키지](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34252-128">This requires that you install the nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="34252-129">embedUrl은 https://embedded.powerbi.com/appTokenReportEmbed가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34252-129">The embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="34252-130">[ 샘플](https://microsoft.github.io/PowerBI-JavaScript/demo/)을 사용하여 기능을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34252-130">You can use the [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) to test functionality.</span></span> <span data-ttu-id="34252-131">또한 사용할 수 있는 다양한 작업에 대한 코드 예제도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="34252-131">It also gives code examples for the different operations that are available.</span></span>

<span data-ttu-id="34252-132">**NuGet 패키지 설치**</span><span class="sxs-lookup"><span data-stu-id="34252-132">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="34252-133">**JavaScript 코드**</span><span class="sxs-lookup"><span data-stu-id="34252-133">**JavaScript code**</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);
```

<span data-ttu-id="34252-134">*powerbi.createReport()*를 호출하면 편집 모드의 빈 캔버스가 *div* 요소 내에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="34252-134">Calling *powerbi.createReport()* will make a blank canvas in edit mode appear within the *div* element.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a><span data-ttu-id="34252-135">새 보고서 저장</span><span class="sxs-lookup"><span data-stu-id="34252-135">Save new reports</span></span>

<span data-ttu-id="34252-136">**다른 이름으로 저장** 작업을 호출할 때까지 실제로 보고서는 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="34252-136">The report will not actually be created until you call the **save as** operation.</span></span> <span data-ttu-id="34252-137">파일 메뉴에서 또는 JavaScript에서 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34252-137">This can be done from file menu or from JavaScript.</span></span>

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
> <span data-ttu-id="34252-138">**다른 이름으로 저장**을 호출해야만 새 보고서가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="34252-138">A new report is created only after **save as** is called.</span></span> <span data-ttu-id="34252-139">저장을 해도 캔버스에는 보고서가 아닌 편집 모드의 데이터 집합이 계속 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="34252-139">After you save, the canvas will still show the dataset in edit mode and not the report.</span></span> <span data-ttu-id="34252-140">다른 보고서의 경우처럼 새 보고서를 다시 로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34252-140">You will need to reload the new report like you would any other report.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-the-new-report"></a><span data-ttu-id="34252-141">새 보고서 로드</span><span class="sxs-lookup"><span data-stu-id="34252-141">Load the new report</span></span>

<span data-ttu-id="34252-142">응용 프로그램이 일반 보고서를 포함하는 것과 같은 방식으로 포함하려는 새 보고서와 상호 작용하기 위해서는 새 보고서용으로 특수하게 새 토큰을 발급한 다음 embed 메서드를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34252-142">In order to interact with the new report you need to embed it in the same way the application embeds a regular report, meaning, a new token must be issued specifically for the new report and then call the embed method.</span></span>

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

## <a name="automate-save-and-load-of-a-new-report-using-the-saved-event"></a><span data-ttu-id="34252-143">"saved" 이벤트를 사용하여 새 보고서의 저장 및 로드 자동화</span><span class="sxs-lookup"><span data-stu-id="34252-143">Automate save and load of a new report using the "saved" event</span></span>

<span data-ttu-id="34252-144">"다른 이름으로 저장" 프로세스를 자동화한 다음 새 보고서를 로드하기 위해 "saved" 이벤트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34252-144">In order to automate the process of "save as" and then loading the new report you can make use of the "saved" Event.</span></span> <span data-ttu-id="34252-145">이 이벤트는 save 작업이 완료되고 새 보고서 ID, 보고서 이름, 이전 보고서 ID(있는 경우)를 포함하는 Json 개체를 반환할 때 및 작업이 saveAs 또는 save일 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="34252-145">This event is fired when the save operation is complete and it returns a Json object containing the new reportId, report name, the old reportId(if there was one) and if the operation was saveAs or save.</span></span>

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

<span data-ttu-id="34252-146">"saved" 이벤트를 수신할 수 있는 프로세스를 자동화하려면 새 보고서 ID를 가져오고 새 토큰을 만든 다음 새 보고서를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="34252-146">To Automate the process you can listen on the "saved" event, take the new reportId, create the new token and embed the new report with it.</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);


   var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);

    // report.on will add an event handler which prints to Log window.
    report.on("saved", function(event) {
        
         // get new Token
         var newReportId =  event.detail.reportObjectId;

        // create new Token. This is a function that the application should provide
        var newToken = createAccessToken(newReportId,scopes /*provide the wanted scopes*/);
        
        
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

## <a name="see-also"></a><span data-ttu-id="34252-147">참고 항목</span><span class="sxs-lookup"><span data-stu-id="34252-147">See also</span></span>

[<span data-ttu-id="34252-148">샘플 시작</span><span class="sxs-lookup"><span data-stu-id="34252-148">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="34252-149">보고서 저장</span><span class="sxs-lookup"><span data-stu-id="34252-149">Save reports</span></span>](power-bi-embedded-save-reports.md)  
[<span data-ttu-id="34252-150">보고서 포함</span><span class="sxs-lookup"><span data-stu-id="34252-150">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="34252-151">Power BI Embedded에서 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="34252-151">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="34252-152">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="34252-152">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="34252-153">JavaScript Embed 샘플</span><span class="sxs-lookup"><span data-stu-id="34252-153">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="34252-154">Power BI Core NuGut 패키지</span><span class="sxs-lookup"><span data-stu-id="34252-154">Power BI Core NuGut Package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[<span data-ttu-id="34252-155">Power BI JavaScript 패키지</span><span class="sxs-lookup"><span data-stu-id="34252-155">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="34252-156">궁금한 점이 더 있나요?</span><span class="sxs-lookup"><span data-stu-id="34252-156">More questions?</span></span> [<span data-ttu-id="34252-157">Power BI 커뮤니티를 이용하세요.</span><span class="sxs-lookup"><span data-stu-id="34252-157">Try the Power BI Community</span></span>](http://community.powerbi.com/)