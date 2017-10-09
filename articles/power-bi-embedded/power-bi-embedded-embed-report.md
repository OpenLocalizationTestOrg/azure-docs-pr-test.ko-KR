---
title: "Power BI 포함 Azure에서 보고서 aaaEmbed | Microsoft Docs"
description: "자세한 내용은 방법 tooembed 응용 프로그램에 Power BI 포함에 있는 보고서입니다."
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
ms.openlocfilehash: f25344bbd0b9c092ef19da04d0b455d453b426a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="embed-a-report-in-power-bi-embedded"></a><span data-ttu-id="6d7ea-103">Power BI Embedded에서 보고서 포함</span><span class="sxs-lookup"><span data-stu-id="6d7ea-103">Embed a report in Power BI Embedded</span></span>

<span data-ttu-id="6d7ea-104">자세한 내용은 방법 tooembed 응용 프로그램에 Power BI 포함에 있는 보고서입니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-104">Learn how tooembed a report that is in Power BI Embedded into your application.</span></span>

<span data-ttu-id="6d7ea-105">Tooactually 응용 프로그램에 보고서를 포함 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-105">We will look at how tooactually embed a report into your application.</span></span> <span data-ttu-id="6d7ea-106">여기서는 작업 영역 컬렉션의 작업 영역 내에 보고서가 이미 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-106">This is assuming you already have a report that exists within a workspace in your workspace collection.</span></span> <span data-ttu-id="6d7ea-107">해당 단계를 아직 완료하지 않으면 [Power BI Embedded 시작](power-bi-embedded-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-107">If you haven't done that step yet, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

<span data-ttu-id="6d7ea-108">Hello.NET (C#) 또는 Node.js SDK JavaScript와 함께 사용할 수 있는데, tooeasily Power BI embedded 응용 프로그램을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-108">You can use hello .NET (C#) or Node.js SDK, along with JavaScript, tooeasily build your application with Power BI Embedded.</span></span> 

## <a name="using-hello-access-keys-toouse-rest-apis"></a><span data-ttu-id="6d7ea-109">Hello 액세스 키 toouse REST Api를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="6d7ea-109">Using hello access keys toouse REST APIs</span></span>

<span data-ttu-id="6d7ea-110">순서 toocall hello REST API, hello 지정한 작업 영역 컬렉션에 대 한 Azure 포털에서에서 얻을 수 hello 액세스 키를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-110">In order toocall hello REST API, you can pass hello access key which you can get from hello Azure portal for a given workspace collection.</span></span> <span data-ttu-id="6d7ea-111">자세한 내용은 [Power BI Embedded 시작](power-bi-embedded-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-111">For more information, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="get-a-report-id"></a><span data-ttu-id="6d7ea-112">보고서 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="6d7ea-112">Get a report id</span></span>

<span data-ttu-id="6d7ea-113">모든 액세스 토큰은 보고서를 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-113">Every access token is based on a report.</span></span> <span data-ttu-id="6d7ea-114">Tooget hello tooembed hello 보고서에 대 한 보고서 id를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-114">You will need tooget hello given report id for hello report that you want tooembed.</span></span> <span data-ttu-id="6d7ea-115">이렇게 호출 toohello에 따라 [보고서 가져오기](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST API입니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-115">This can be done based on calls toohello [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST API.</span></span> <span data-ttu-id="6d7ea-116">이 id와 hello url을 포함 하는 hello 보고서를 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-116">This will return hello report id and hello embed url.</span></span> <span data-ttu-id="6d7ea-117">이렇게 하려면 Power BI.NET SDK hello를 사용 하 여 또는 hello REST API를 직접 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-117">This can be done using hello Power BI .NET SDK or calling hello REST API directly.</span></span>

### <a name="using-hello-power-bi-net-sdk"></a><span data-ttu-id="6d7ea-118">Power BI.NET SDK hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="6d7ea-118">Using hello Power BI .NET SDK</span></span>

<span data-ttu-id="6d7ea-119">Hello.NET SDK를 사용할 경우 toocreate hello Azure 포털에서에서 가져올 hello 선택 키를 기반으로 하는 토큰 자격 증명 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-119">When using hello .NET SDK, you will need toocreate a token credential which is based on hello access key you get from hello Azure portal.</span></span> <span data-ttu-id="6d7ea-120">Hello를 설치 하는이 위해서는 [Power BI API NuGet 패키지](https://www.nuget.org/profiles/powerbi)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-120">This requires that you install hello [Power BI API NuGet package](https://www.nuget.org/profiles/powerbi).</span></span>

<span data-ttu-id="6d7ea-121">**NuGet 패키지 설치**</span><span class="sxs-lookup"><span data-stu-id="6d7ea-121">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Api
```

<span data-ttu-id="6d7ea-122">**C# 코드**</span><span class="sxs-lookup"><span data-stu-id="6d7ea-122">**C# code**</span></span>

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select hello report that you want toowork with from hello collection of reports.
```

### <a name="calling-hello-rest-api-directly"></a><span data-ttu-id="6d7ea-123">REST API 호출 hello을 직접</span><span class="sxs-lookup"><span data-stu-id="6d7ea-123">Calling hello REST API directly</span></span>

```
System.Net.WebRequest request = System.Net.WebRequest.Create("https://api.powerbi.com/v1.0/collections/{collectionName}/workspaces/{workspaceId}/Reports") as System.Net.HttpWebRequest;

request.Method = "GET";
request.ContentLength = 0;
request.Headers.Add("Authorization", String.Format("AppKey {0}", accessToken.Value));

using (var response = request.GetResponse() as System.Net.HttpWebResponse)
{
    using (var reader = new System.IO.StreamReader(response.GetResponseStream()))
    {
        // Work with JSON response tooget hello report you want toowork with.
    }

}
```

## <a name="create-an-access-token"></a><span data-ttu-id="6d7ea-124">액세스 토큰 만들기</span><span class="sxs-lookup"><span data-stu-id="6d7ea-124">Create an access token</span></span>

<span data-ttu-id="6d7ea-125">Power BI Embedded는 HMAC 서명 JSON Web Token에 해당하는 Embed 토큰을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-125">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="6d7ea-126">hello 토큰은 Azure Power BI 포함 작업 영역 컬렉션에서 hello 액세스 키로 서명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-126">hello tokens are signed with hello access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="6d7ea-127">기본적으로 토큰을 포함, 됩니다 하 읽기 사용된 tooprovide 응용 프로그램으로 tooa 보고서 tooembed만 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-127">Embed tokens, by default, are used tooprovide read only access tooa report tooembed into an application.</span></span> <span data-ttu-id="6d7ea-128">Embed 토큰은 특정 보고서에 대해 발급되며 Embed URL에 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-128">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="6d7ea-129">액세스 토큰 hello 액세스 키가 사용 되는 toosign/암호화 hello 토큰으로 hello 서버에 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-129">Access tokens should be created on hello server as hello access keys are used toosign/encrypt hello tokens.</span></span> <span data-ttu-id="6d7ea-130">방법에 대 한 내용은 toocreate, 액세스 토큰이 참조 [인증 하 고 Power BI embedded 허가](power-bi-embedded-app-token-flow.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-130">For information on how toocreate an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="6d7ea-131">또한 hello을 검토할 수 [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) 메서드.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-131">You can also review hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="6d7ea-132">이 모양을 hello.NET SDK를 사용 하 여 Power BI에 대 한 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-132">Here is an example of what this would look like using hello .NET SDK for Power BI.</span></span>

<span data-ttu-id="6d7ea-133">앞서 검색 hello 보고서 id를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-133">You will use hello report id that you retrieved earlier.</span></span> <span data-ttu-id="6d7ea-134">Hello 포함 되 면 토큰이 만들어질, hello javascript 관점에서 사용할 수 있는 hello 액세스 키 toogenerate hello 토큰 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-134">Once hello embed token is created, you will then use hello access key toogenerate hello token which you can use from hello javascript perspective.</span></span> <span data-ttu-id="6d7ea-135">hello *PowerBIToken 클래스* hello를 설치 해야 [Power BI 핵심 NuGut 패키지](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-135">hello *PowerBIToken class* requires that you install hello [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="6d7ea-136">**NuGet 패키지 설치**</span><span class="sxs-lookup"><span data-stu-id="6d7ea-136">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="6d7ea-137">**C# 코드**</span><span class="sxs-lookup"><span data-stu-id="6d7ea-137">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-tooembed-tokens"></a><span data-ttu-id="6d7ea-138">사용 권한 범위 tooembed 토큰 추가</span><span class="sxs-lookup"><span data-stu-id="6d7ea-138">Adding permission scopes tooembed tokens</span></span>

<span data-ttu-id="6d7ea-139">Embed 토큰을 사용 하 여 hello 리소스에 대 한 액세스를 부여 toorestrict 사용을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-139">When using Embed tokens, you may want toorestrict usage of hello resources you give access to.</span></span> <span data-ttu-id="6d7ea-140">이러한 이유로 범위가 지정된 사용 권한으로 토큰을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-140">For this reason, you can generate a token with scoped permissions.</span></span> <span data-ttu-id="6d7ea-141">자세한 내용은 [범위](power-bi-embedded-app-token-flow.md#scopes)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-141">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes)</span></span>

## <a name="embed-using-javascript"></a><span data-ttu-id="6d7ea-142">JavaScript를 사용하여 포함</span><span class="sxs-lookup"><span data-stu-id="6d7ea-142">Embed using JavaScript</span></span>

<span data-ttu-id="6d7ea-143">Hello 액세스 토큰 및 hello 보고서 id를 설정한 후 JavaScript를 사용 하 여 hello 보고서를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-143">After you have hello access token and hello report id, we can embed hello report using JavaScript.</span></span> <span data-ttu-id="6d7ea-144">Hello nuget을 설치 하는이 위해서는 [Power BI JavaScript 패키지](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-144">This requires that you install hello nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="6d7ea-145">hello embedUrl https://embedded.powerbi.com/appTokenReportEmbed 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-145">hello embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="6d7ea-146">Hello를 사용할 수 있습니다 [JavaScript 보고서 포함 예제](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-146">You can use hello [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest functionality.</span></span> <span data-ttu-id="6d7ea-147">또한 hello 사용할 수 있는 다른 작업에 대 한 코드 예제를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-147">It also gives code examples for hello different operations that are available.</span></span>

<span data-ttu-id="6d7ea-148">**NuGet 패키지 설치**</span><span class="sxs-lookup"><span data-stu-id="6d7ea-148">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="6d7ea-149">**JavaScript 코드**</span><span class="sxs-lookup"><span data-stu-id="6d7ea-149">**JavaScript code**</span></span>

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

### <a name="set-hello-size-of-embedded-elements"></a><span data-ttu-id="6d7ea-150">포함 된 요소의 hello 크기 설정</span><span class="sxs-lookup"><span data-stu-id="6d7ea-150">Set hello size of embedded elements</span></span>

<span data-ttu-id="6d7ea-151">hello 보고서 자동으로 포함 됩니다 해당 컨테이너의 hello 크기에 따라.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-151">hello report will automatically be embedded based on hello size of its container.</span></span> <span data-ttu-id="6d7ea-152">hello의 toooverride hello 기본 크기를 포함 하기만 하면 너비 및 높이 대 한 CSS 클래스 특성 또는 인라인 스타일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-152">toooverride hello default size of hello embeds simply add a CSS class attribute or inline styles for width & height.</span></span>

## <a name="see-also"></a><span data-ttu-id="6d7ea-153">참고 항목</span><span class="sxs-lookup"><span data-stu-id="6d7ea-153">See also</span></span>

[<span data-ttu-id="6d7ea-154">샘플 시작</span><span class="sxs-lookup"><span data-stu-id="6d7ea-154">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="6d7ea-155">Power BI Embedded에서 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="6d7ea-155">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="6d7ea-156">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="6d7ea-156">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="6d7ea-157">JavaScript Embed 샘플</span><span class="sxs-lookup"><span data-stu-id="6d7ea-157">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="6d7ea-158">Power BI JavaScript 패키지</span><span class="sxs-lookup"><span data-stu-id="6d7ea-158">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="6d7ea-159">[Power BI API NuGet 패키지](https://www.nuget.org/profiles/powerbi)
[Power BI Core NuGut 패키지](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span><span class="sxs-lookup"><span data-stu-id="6d7ea-159">[Power BI API NuGet package](https://www.nuget.org/profiles/powerbi)
[Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span></span>  
[<span data-ttu-id="6d7ea-160">PowerBI-CSharp Git 리포지토리</span><span class="sxs-lookup"><span data-stu-id="6d7ea-160">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="6d7ea-161">PowerBI-Node Git 리포지토리</span><span class="sxs-lookup"><span data-stu-id="6d7ea-161">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="6d7ea-162">궁금한 점이 더 있나요?</span><span class="sxs-lookup"><span data-stu-id="6d7ea-162">More questions?</span></span> [<span data-ttu-id="6d7ea-163">Power BI 커뮤니티 hello를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6d7ea-163">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
