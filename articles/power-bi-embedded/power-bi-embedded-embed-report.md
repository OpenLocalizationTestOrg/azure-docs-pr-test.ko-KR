---
title: "Azure Power BI Embedded에 보고서 포함 | Microsoft Docs"
description: "Power BI Embedded에 있는 보고서를 응용 프로그램에 포함하는 방법을 알아봅니다."
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
ms.openlocfilehash: 3d865af2418c9c557c861a379766a125d75cebf1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="embed-a-report-in-power-bi-embedded"></a><span data-ttu-id="2b883-103">Power BI Embedded에서 보고서 포함</span><span class="sxs-lookup"><span data-stu-id="2b883-103">Embed a report in Power BI Embedded</span></span>

<span data-ttu-id="2b883-104">Power BI Embedded에 있는 보고서를 응용 프로그램에 포함하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-104">Learn how to embed a report that is in Power BI Embedded into your application.</span></span>

<span data-ttu-id="2b883-105">실제로 응용 프로그램에 보고서를 포함하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-105">We will look at how to actually embed a report into your application.</span></span> <span data-ttu-id="2b883-106">여기서는 작업 영역 컬렉션의 작업 영역 내에 보고서가 이미 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-106">This is assuming you already have a report that exists within a workspace in your workspace collection.</span></span> <span data-ttu-id="2b883-107">해당 단계를 아직 완료하지 않으면 [Power BI Embedded 시작](power-bi-embedded-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2b883-107">If you haven't done that step yet, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

<span data-ttu-id="2b883-108">JavaScript와 함께 .NET(C#) 또는 Node.js SDK를 사용하여 Power BI Embedded로 응용 프로그램을 손쉽게 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-108">You can use the .NET (C#) or Node.js SDK, along with JavaScript, to easily build your application with Power BI Embedded.</span></span> 

## <a name="using-the-access-keys-to-use-rest-apis"></a><span data-ttu-id="2b883-109">액세스 키를 사용하여 REST API 사용</span><span class="sxs-lookup"><span data-stu-id="2b883-109">Using the access keys to use REST APIs</span></span>

<span data-ttu-id="2b883-110">REST API를 호출하려면 지정된 작업 영역 컬렉션에 대해 Azure Portal에서 가져올 수 있는 액세스 키를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-110">In order to call the REST API, you can pass the access key which you can get from the Azure portal for a given workspace collection.</span></span> <span data-ttu-id="2b883-111">자세한 내용은 [Power BI Embedded 시작](power-bi-embedded-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2b883-111">For more information, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="get-a-report-id"></a><span data-ttu-id="2b883-112">보고서 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="2b883-112">Get a report id</span></span>

<span data-ttu-id="2b883-113">모든 액세스 토큰은 보고서를 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-113">Every access token is based on a report.</span></span> <span data-ttu-id="2b883-114">포함할 보고서에 대해 지정된 보고서 ID를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-114">You will need to get the given report id for the report that you want to embed.</span></span> <span data-ttu-id="2b883-115">이 작업은 [보고서 가져오기](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST API 호출에 따라 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-115">This can be done based on calls to the [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST API.</span></span> <span data-ttu-id="2b883-116">이렇게 하면 보고서 ID와 Embed URL이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-116">This will return the report id and the embed url.</span></span> <span data-ttu-id="2b883-117">이 작업은 Power BI .NET SDK를 사용하거나 REST API를 직접 호출하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-117">This can be done using the Power BI .NET SDK or calling the REST API directly.</span></span>

### <a name="using-the-power-bi-net-sdk"></a><span data-ttu-id="2b883-118">Power BI .NET SDK 사용</span><span class="sxs-lookup"><span data-stu-id="2b883-118">Using the Power BI .NET SDK</span></span>

<span data-ttu-id="2b883-119">.NET SDK를 사용하는 경우 Azure Portal에서 가져오는 액세스 키를 기준으로 하는 토큰 자격 증명을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-119">When using the .NET SDK, you will need to create a token credential which is based on the access key you get from the Azure portal.</span></span> <span data-ttu-id="2b883-120">이렇게 하려면 [Power BI API NuGet 패키지](https://www.nuget.org/profiles/powerbi)를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-120">This requires that you install the [Power BI API NuGet package](https://www.nuget.org/profiles/powerbi).</span></span>

<span data-ttu-id="2b883-121">**NuGet 패키지 설치**</span><span class="sxs-lookup"><span data-stu-id="2b883-121">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Api
```

<span data-ttu-id="2b883-122">**C# 코드**</span><span class="sxs-lookup"><span data-stu-id="2b883-122">**C# code**</span></span>

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select the report that you want to work with from the collection of reports.
```

### <a name="calling-the-rest-api-directly"></a><span data-ttu-id="2b883-123">REST API 직접 호출</span><span class="sxs-lookup"><span data-stu-id="2b883-123">Calling the REST API directly</span></span>

```
System.Net.WebRequest request = System.Net.WebRequest.Create("https://api.powerbi.com/v1.0/collections/{collectionName}/workspaces/{workspaceId}/Reports") as System.Net.HttpWebRequest;

request.Method = "GET";
request.ContentLength = 0;
request.Headers.Add("Authorization", String.Format("AppKey {0}", accessToken.Value));

using (var response = request.GetResponse() as System.Net.HttpWebResponse)
{
    using (var reader = new System.IO.StreamReader(response.GetResponseStream()))
    {
        // Work with JSON response to get the report you want to work with.
    }

}
```

## <a name="create-an-access-token"></a><span data-ttu-id="2b883-124">액세스 토큰 만들기</span><span class="sxs-lookup"><span data-stu-id="2b883-124">Create an access token</span></span>

<span data-ttu-id="2b883-125">Power BI Embedded는 HMAC 서명 JSON Web Token에 해당하는 Embed 토큰을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-125">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="2b883-126">이러한 토큰은 Azure Power BI Embedded 작업 영역 컬렉션의 액세스 키로 서명됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-126">The tokens are signed with the access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="2b883-127">기본적으로 응용 프로그램에 포함할 보고서에 대해 읽기 전용 액세스를 제공하기 위해 Embed 토큰이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-127">Embed tokens, by default, are used to provide read only access to a report to embed into an application.</span></span> <span data-ttu-id="2b883-128">Embed 토큰은 특정 보고서에 대해 발급되며 Embed URL에 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-128">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="2b883-129">서명/토큰 암호화에 액세스 키가 사용되므로 서버에서 액세스 토큰을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-129">Access tokens should be created on the server as the access keys are used to sign/encrypt the tokens.</span></span> <span data-ttu-id="2b883-130">액세스 토큰을 만드는 방법에 대한 자세한 내용은 [Power BI Embedded에서 인증 및 권한 부여](power-bi-embedded-app-token-flow.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2b883-130">For information on how to create an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="2b883-131">[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) 메서드를 검토할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-131">You can also review the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="2b883-132">다음은 Power BI용 .NET SDK를 사용할 경우의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-132">Here is an example of what this would look like using the .NET SDK for Power BI.</span></span>

<span data-ttu-id="2b883-133">이전에 검색한 보고서 ID를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-133">You will use the report id that you retrieved earlier.</span></span> <span data-ttu-id="2b883-134">Embed 토큰이 만들어지면 액세스 키를 사용하여 javascript 관점에서 사용할 수 있는 토큰을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-134">Once the embed token is created, you will then use the access key to generate the token which you can use from the javascript perspective.</span></span> <span data-ttu-id="2b883-135">*PowerBIToken 클래스*를 사용하려면 [Power BI Core NuGut 패키지](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-135">The *PowerBIToken class* requires that you install the [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="2b883-136">**NuGet 패키지 설치**</span><span class="sxs-lookup"><span data-stu-id="2b883-136">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="2b883-137">**C# 코드**</span><span class="sxs-lookup"><span data-stu-id="2b883-137">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-to-embed-tokens"></a><span data-ttu-id="2b883-138">Embed 토큰에 사용 권한 범위 추가</span><span class="sxs-lookup"><span data-stu-id="2b883-138">Adding permission scopes to embed tokens</span></span>

<span data-ttu-id="2b883-139">Embed 토큰으로 사용하는 경우 액세스 권한을 제공하는 리소스 사용을 제한하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-139">When using Embed tokens, you may want to restrict usage of the resources you give access to.</span></span> <span data-ttu-id="2b883-140">이러한 이유로 범위가 지정된 사용 권한으로 토큰을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-140">For this reason, you can generate a token with scoped permissions.</span></span> <span data-ttu-id="2b883-141">자세한 내용은 [범위](power-bi-embedded-app-token-flow.md#scopes)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2b883-141">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes)</span></span>

## <a name="embed-using-javascript"></a><span data-ttu-id="2b883-142">JavaScript를 사용하여 포함</span><span class="sxs-lookup"><span data-stu-id="2b883-142">Embed using JavaScript</span></span>

<span data-ttu-id="2b883-143">액세스 토큰 및 보고서 ID를 설정한 후 JavaScript를 사용하여 보고서를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-143">After you have the access token and the report id, we can embed the report using JavaScript.</span></span> <span data-ttu-id="2b883-144">이렇게 하려면 nuget [Power BI JavaScript 패키지](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-144">This requires that you install the nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="2b883-145">embedUrl은 https://embedded.powerbi.com/appTokenReportEmbed가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-145">The embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="2b883-146">[ 샘플](https://microsoft.github.io/PowerBI-JavaScript/demo/)을 사용하여 기능을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-146">You can use the [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) to test functionality.</span></span> <span data-ttu-id="2b883-147">또한 사용할 수 있는 다양한 작업에 대한 코드 예제도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-147">It also gives code examples for the different operations that are available.</span></span>

<span data-ttu-id="2b883-148">**NuGet 패키지 설치**</span><span class="sxs-lookup"><span data-stu-id="2b883-148">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="2b883-149">**JavaScript 코드**</span><span class="sxs-lookup"><span data-stu-id="2b883-149">**JavaScript code**</span></span>

```
<script src="/scripts/powerbi.js"></script>
<div id="reportContainer"></div>

var embedConfiguration = {
    type: 'report',
    accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
    id: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed'
};

var $reportContainer = $('#reportContainer');
var report = powerbi.embed($reportContainer.get(0), embedConfiguration);
```

### <a name="set-the-size-of-embedded-elements"></a><span data-ttu-id="2b883-150">포함된 요소의 크기 설정</span><span class="sxs-lookup"><span data-stu-id="2b883-150">Set the size of embedded elements</span></span>

<span data-ttu-id="2b883-151">보고서는 컨테이너의 크기에 따라 자동으로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-151">The report will automatically be embedded based on the size of its container.</span></span> <span data-ttu-id="2b883-152">Embed의 기본 크기를 재정의하려면 CSS 클래스 특성 또는 너비/높이에 대한 인라인 스타일을 추가하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b883-152">To override the default size of the embeds simply add a CSS class attribute or inline styles for width & height.</span></span>

## <a name="see-also"></a><span data-ttu-id="2b883-153">참고 항목</span><span class="sxs-lookup"><span data-stu-id="2b883-153">See also</span></span>

[<span data-ttu-id="2b883-154">샘플 시작</span><span class="sxs-lookup"><span data-stu-id="2b883-154">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="2b883-155">Power BI Embedded에서 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="2b883-155">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="2b883-156">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="2b883-156">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="2b883-157">JavaScript Embed 샘플</span><span class="sxs-lookup"><span data-stu-id="2b883-157">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="2b883-158">Power BI JavaScript 패키지</span><span class="sxs-lookup"><span data-stu-id="2b883-158">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="2b883-159">[Power BI API NuGet 패키지](https://www.nuget.org/profiles/powerbi)
[Power BI Core NuGut 패키지](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span><span class="sxs-lookup"><span data-stu-id="2b883-159">[Power BI API NuGet package](https://www.nuget.org/profiles/powerbi)
[Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span></span>  
[<span data-ttu-id="2b883-160">PowerBI-CSharp Git 리포지토리</span><span class="sxs-lookup"><span data-stu-id="2b883-160">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="2b883-161">PowerBI-Node Git 리포지토리</span><span class="sxs-lookup"><span data-stu-id="2b883-161">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="2b883-162">궁금한 점이 더 있나요?</span><span class="sxs-lookup"><span data-stu-id="2b883-162">More questions?</span></span> [<span data-ttu-id="2b883-163">Power BI 커뮤니티를 이용하세요.</span><span class="sxs-lookup"><span data-stu-id="2b883-163">Try the Power BI Community</span></span>](http://community.powerbi.com/)
