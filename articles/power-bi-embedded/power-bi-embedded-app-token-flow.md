---
title: "aaaAuthenticating 및 Power BI embedded 권한 부여"
description: "Power BI Embedded에서 인증 및 권한 부여"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 1c1369ea-7dfd-4b6e-978b-8f78908fd6f6
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 483ca0499e8d03584e1151d3d278c0179d4b8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a><span data-ttu-id="bd452-103">Power BI Embedded에서 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="bd452-103">Authenticating and authorizing with Power BI Embedded</span></span>

<span data-ttu-id="bd452-104">Power BI 포함 서비스 hello를 사용 하 여 **키** 및 **앱 토큰** 인증 및 권한 부여 명시적 최종 사용자 인증 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-104">hello Power BI Embedded service uses **Keys** and **App Tokens** for authentication and authorization, instead of explicit end-user authentication.</span></span> <span data-ttu-id="bd452-105">이 모델에서 응용 프로그램이 최종 사용자에 대한 인증 및 권한 부여를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-105">In this model, your application manages authentication and authorization for your end-users.</span></span> <span data-ttu-id="bd452-106">필요한 경우 응용 프로그램 만들고 우리의 서비스 toorender에 알리는 hello 앱 토큰 hello 요청한 보고서를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-106">When necessary, your app creates and sends hello App Tokens that tells our service toorender hello requested report.</span></span> <span data-ttu-id="bd452-107">이 디자인 여전히 수는 있지만 사용자 인증 및 권한 부여에 대 한 Azure Active Directory에 앱 toouse가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-107">This design doesn't require your app toouse Azure Active Directory for user authentication and authorization, although you still can.</span></span>

## <a name="two-ways-tooauthenticate"></a><span data-ttu-id="bd452-108">두 가지 방법으로 tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="bd452-108">Two ways tooauthenticate</span></span>

<span data-ttu-id="bd452-109">**키** - 모든 Power BI Embedded REST API 호출에 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-109">**Key** -  You can use keys for all Power BI Embedded REST API calls.</span></span> <span data-ttu-id="bd452-110">hello에 hello 키를 찾을 수 **Azure 포털** 를 클릭 하 여 **모든 설정을** 차례로 **액세스 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-110">hello keys can be found in hello **Azure portal** by clicking on **All settings** and then **Access keys**.</span></span> <span data-ttu-id="bd452-111">키는 항상 암호처럼 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-111">Always treat your key as if it were a password.</span></span> <span data-ttu-id="bd452-112">이러한 키에는 사용 권한을 toomake 특정 작업 영역 컬렉션에서 모든 REST API를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-112">These keys have permissions toomake any REST API call on a particular workspace collection.</span></span>

<span data-ttu-id="bd452-113">toouse REST 호출의 키를 권한 부여 헤더 뒤에 오는 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-113">toouse a key on a REST call, add hello following authorization header:</span></span>            

    Authorization: AppKey {your key}

<span data-ttu-id="bd452-114">**앱 토큰** - 앱 토큰은 모든 포함 요청에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-114">**App token** - App tokens are used for all embedding requests.</span></span> <span data-ttu-id="bd452-115">제한 하므로 실행 하는 디자인 된 toobe 클라이언트 쪽 하기가 tooa 단일 보고서 및 해당 하는 모범 사례 tooset 만료 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-115">They’re designed toobe run client-side, so they're restricted tooa single report and it’s best practice tooset an expiration time.</span></span>

<span data-ttu-id="bd452-116">앱 토큰은 사용자 키 중 하나로 서명된 JWT(JSON Web Token)입니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-116">App tokens are a JWT (JSON Web Token) that is signed by one of your keys.</span></span>

<span data-ttu-id="bd452-117">응용 프로그램 토큰 클레임에 따라 hello를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-117">Your app token can contain hello following claims:</span></span>

| <span data-ttu-id="bd452-118">클레임</span><span class="sxs-lookup"><span data-stu-id="bd452-118">Claim</span></span> | <span data-ttu-id="bd452-119">설명</span><span class="sxs-lookup"><span data-stu-id="bd452-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bd452-120">**ver**</span><span class="sxs-lookup"><span data-stu-id="bd452-120">**ver**</span></span> |<span data-ttu-id="bd452-121">hello 응용 프로그램 토큰의 hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-121">hello version of hello app token.</span></span> <span data-ttu-id="bd452-122">0.2.0는 hello 현재 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-122">0.2.0 is hello current version.</span></span> |
| <span data-ttu-id="bd452-123">**aud**</span><span class="sxs-lookup"><span data-stu-id="bd452-123">**aud**</span></span> |<span data-ttu-id="bd452-124">hello는 hello 토큰의 올바른 받는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-124">hello intended recipient of hello token.</span></span> <span data-ttu-id="bd452-125">Power BI Embedded의 경우 "https://analysis.windows.net/powerbi/api"를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-125">For Power BI Embedded use: “https://analysis.windows.net/powerbi/api”.</span></span> |
| <span data-ttu-id="bd452-126">**iss**</span><span class="sxs-lookup"><span data-stu-id="bd452-126">**iss**</span></span> |<span data-ttu-id="bd452-127">Hello 토큰을 발급 한 hello 응용 프로그램을 나타내는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-127">A string indicating hello application which issued hello token.</span></span> |
| <span data-ttu-id="bd452-128">**type**</span><span class="sxs-lookup"><span data-stu-id="bd452-128">**type**</span></span> |<span data-ttu-id="bd452-129">생성 되 고 있는 응용 프로그램 토큰의 hello 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-129">hello type of app token which is being created.</span></span> <span data-ttu-id="bd452-130">Hello만 지원 됩니다. 현재 유형은 **포함**합니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-130">Current hello only supported type is **embed**.</span></span> |
| <span data-ttu-id="bd452-131">**wcn**</span><span class="sxs-lookup"><span data-stu-id="bd452-131">**wcn**</span></span> |<span data-ttu-id="bd452-132">에 대 한 작업 영역 컬렉션 이름 hello 토큰을 발급 되 고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-132">Workspace collection name hello token is being issued for.</span></span> |
| <span data-ttu-id="bd452-133">**wid**</span><span class="sxs-lookup"><span data-stu-id="bd452-133">**wid**</span></span> |<span data-ttu-id="bd452-134">작업 영역 ID hello 토큰에 대해 실행 되 고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-134">Workspace ID hello token is being issued for.</span></span> |
| <span data-ttu-id="bd452-135">**rid**</span><span class="sxs-lookup"><span data-stu-id="bd452-135">**rid**</span></span> |<span data-ttu-id="bd452-136">에 대 한 ID hello 토큰 발급 되 고 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-136">Report ID hello token is being issued for.</span></span> |
| <span data-ttu-id="bd452-137">**username** (선택 사항)</span><span class="sxs-lookup"><span data-stu-id="bd452-137">**username** (optional)</span></span> |<span data-ttu-id="bd452-138">RLS로 사용 되는, RLS 규칙을 적용할 때 hello 사용자를 식별 하는 데 도움이 되는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-138">Used with RLS, this is a string that can help identify hello user when applying RLS rules.</span></span> |
| <span data-ttu-id="bd452-139">**roles** (선택 사항)</span><span class="sxs-lookup"><span data-stu-id="bd452-139">**roles** (optional)</span></span> |<span data-ttu-id="bd452-140">행 수준 보안 규칙을 적용할 때 hello 역할 tooselect를 포함 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-140">A string containing hello roles tooselect when applying Row Level Security rules.</span></span> <span data-ttu-id="bd452-141">둘 이상의 역할을 전달하는 경우 문자열 배열로 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-141">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="bd452-142">**scp**(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="bd452-142">**scp** (optional)</span></span> |<span data-ttu-id="bd452-143">Hello 권한 범위를 포함 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-143">A string containing hello permissions scopes.</span></span> <span data-ttu-id="bd452-144">둘 이상의 역할을 전달하는 경우 문자열 배열로 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-144">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="bd452-145">**exp** (선택 사항)</span><span class="sxs-lookup"><span data-stu-id="bd452-145">**exp** (optional)</span></span> |<span data-ttu-id="bd452-146">hello 토큰이 만료 되므로 hello 시간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-146">Indicates hello time in which hello token will expire.</span></span> <span data-ttu-id="bd452-147">Unix 타임스탬프로 전달되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-147">These should be passed in as Unix timestamps.</span></span> |
| <span data-ttu-id="bd452-148">**nbf** (선택 사항)</span><span class="sxs-lookup"><span data-stu-id="bd452-148">**nbf** (optional)</span></span> |<span data-ttu-id="bd452-149">hello에 토큰 유효 시작 hello 시간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-149">Indicates hello time in which hello token starts being valid.</span></span> <span data-ttu-id="bd452-150">Unix 타임스탬프로 전달되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-150">These should be passed in as Unix timestamps.</span></span> |

<span data-ttu-id="bd452-151">샘플 앱 토큰은 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-151">A sample app token will look like this:</span></span>

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

<span data-ttu-id="bd452-152">디코딩되면 결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-152">When decoded, it will look something like this:</span></span>

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

<span data-ttu-id="bd452-153">Hello apptokens 만드는 쉽게 해 주는 Sdk에서 사용할 수 있는 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-153">There are methods available within hello SDKs that make creation of apptokens easier.</span></span> <span data-ttu-id="bd452-154">예를 들어.net 살펴보면 hello [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) 클래스 및 hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) 메서드.</span><span class="sxs-lookup"><span data-stu-id="bd452-154">For example, for .NET you can look at hello [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) class and hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methods.</span></span>

<span data-ttu-id="bd452-155">Hello.NET SDK를 참조할 수 있습니다 너무[범위](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-155">For hello .NET SDK, you can refer too[Scopes](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span></span>

## <a name="scopes"></a><span data-ttu-id="bd452-156">범위</span><span class="sxs-lookup"><span data-stu-id="bd452-156">Scopes</span></span>

<span data-ttu-id="bd452-157">Embed 토큰을 사용 하 여 hello 리소스에 대 한 액세스를 부여 toorestrict 사용을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-157">When using Embed tokens, you may want toorestrict usage of hello resources you give access to.</span></span> <span data-ttu-id="bd452-158">이러한 이유로 범위가 지정된 사용 권한으로 토큰을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-158">For this reason, you can generate a token with scoped permissions.</span></span>

<span data-ttu-id="bd452-159">Power BI 포함에 대 한 hello 사용할 수 있는 범위는 hello 다음과가 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-159">hello following are hello available scopes for Power BI Embedded.</span></span>

|<span data-ttu-id="bd452-160">범위</span><span class="sxs-lookup"><span data-stu-id="bd452-160">Scope</span></span>|<span data-ttu-id="bd452-161">설명</span><span class="sxs-lookup"><span data-stu-id="bd452-161">Description</span></span>|
|---|---|
|<span data-ttu-id="bd452-162">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="bd452-162">Dataset.Read</span></span>|<span data-ttu-id="bd452-163">권한을 제공 tooread hello 데이터 집합을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-163">Provides permission tooread hello specified dataset.</span></span>|
|<span data-ttu-id="bd452-164">Dataset.Write</span><span class="sxs-lookup"><span data-stu-id="bd452-164">Dataset.Write</span></span>|<span data-ttu-id="bd452-165">지정 된 사용 권한 toowrite toohello 제공 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-165">Provides permission toowrite toohello specified dataset.</span></span>|
|<span data-ttu-id="bd452-166">Dataset.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="bd452-166">Dataset.ReadWrite</span></span>|<span data-ttu-id="bd452-167">사용 권한 tooread 및 쓰기 toohello 컴파일되고 데이터 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-167">Provides permission tooread and write toohello specificed dataset.</span></span>|
|<span data-ttu-id="bd452-168">Report.Read</span><span class="sxs-lookup"><span data-stu-id="bd452-168">Report.Read</span></span>|<span data-ttu-id="bd452-169">권한을 제공 tooview hello 보고서를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-169">Provides permission tooview hello specified report.</span></span>|
|<span data-ttu-id="bd452-170">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="bd452-170">Report.ReadWrite</span></span>|<span data-ttu-id="bd452-171">사용 권한 tooview 및 편집 hello 지정 된 보고서를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-171">Provides permission tooview and edit hello specified report.</span></span>|
|<span data-ttu-id="bd452-172">Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="bd452-172">Workspace.Report.Create</span></span>|<span data-ttu-id="bd452-173">제공 사용 권한 toocreate 지정 hello 내에서 새 보고서 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-173">Provides permission toocreate a new report within hello specified workspace.</span></span>|
|<span data-ttu-id="bd452-174">Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="bd452-174">Workspace.Report.Copy</span></span>|<span data-ttu-id="bd452-175">제공 사용 권한 tooclone 지정 hello 내의 기존 보고서 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-175">Provides permission tooclone an existing report within hello specified workspace.</span></span>|

<span data-ttu-id="bd452-176">Hello 다음과 같은 hello 범위 사이 공백을 사용 하 여 여러 범위를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-176">You can supply multiple scopes by using a space between hello scopes like hello following.</span></span>

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

<span data-ttu-id="bd452-177">**필요한 클레임 - 범위**</span><span class="sxs-lookup"><span data-stu-id="bd452-177">**Required claims - scopes**</span></span>

<span data-ttu-id="bd452-178">scp: {scopesClaim} scopesClaim 문자열 또는 허용 된 권한을 tooworkspace 리소스 (예: 보고서, 데이터 집합) hello 주목할 문자열의 배열 될 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="bd452-178">scp: {scopesClaim} scopesClaim can be either a string or array of strings, noting hello allowed permissions tooworkspace resources (Report, Dataset, etc.)</span></span>

<span data-ttu-id="bd452-179">범위를 정의 하는 디코딩된 토큰을 비슷한 toohello 다음과 유사할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-179">A decoded token, with scopes defined, would look similar toohello following.</span></span>

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "scp": "Report.Read",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

### <a name="operations-and-scopes"></a><span data-ttu-id="bd452-180">작업 및 범위</span><span class="sxs-lookup"><span data-stu-id="bd452-180">Operations and scopes</span></span>

|<span data-ttu-id="bd452-181">작업</span><span class="sxs-lookup"><span data-stu-id="bd452-181">Operation</span></span>|<span data-ttu-id="bd452-182">대상 리소스</span><span class="sxs-lookup"><span data-stu-id="bd452-182">Target resource</span></span>|<span data-ttu-id="bd452-183">토큰 사용 권한</span><span class="sxs-lookup"><span data-stu-id="bd452-183">Token permissions</span></span>|
|---|---|---|
|<span data-ttu-id="bd452-184">데이터 집합을 기반으로 새 메모리 내 보고서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-184">Create (in-memory) a new report based on a dataset.</span></span>|<span data-ttu-id="bd452-185">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="bd452-185">Dataset</span></span>|<span data-ttu-id="bd452-186">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="bd452-186">Dataset.Read</span></span>|
|<span data-ttu-id="bd452-187">(메모리) 데이터 집합을 기반으로 새 보고서 만들고 hello 보고서를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-187">Create (in-memory) a new report based on a dataset and save hello report.</span></span>|<span data-ttu-id="bd452-188">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="bd452-188">Dataset</span></span>|<span data-ttu-id="bd452-189">* Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="bd452-189">* Dataset.Read</span></span><br><span data-ttu-id="bd452-190">* Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="bd452-190">* Workspace.Report.Create</span></span>|
|<span data-ttu-id="bd452-191">기존 메모리 내 보고서를 보고 탐색/편집합니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-191">View and explore/edit (in-memory) an existing report.</span></span> <span data-ttu-id="bd452-192">Report.Read는 Dataset.Read를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-192">Report.Read implies Dataset.Read.</span></span> <span data-ttu-id="bd452-193">이것은 toosave 편집 권한이 없도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-193">This will not allow permissions toosave edits.</span></span>|<span data-ttu-id="bd452-194">보고서</span><span class="sxs-lookup"><span data-stu-id="bd452-194">Report</span></span>|<span data-ttu-id="bd452-195">Report.Read</span><span class="sxs-lookup"><span data-stu-id="bd452-195">Report.Read</span></span>|
|<span data-ttu-id="bd452-196">기존 보고서를 편집하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-196">Edit and save an existing report.</span></span>|<span data-ttu-id="bd452-197">보고서</span><span class="sxs-lookup"><span data-stu-id="bd452-197">Report</span></span>|<span data-ttu-id="bd452-198">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="bd452-198">Report.ReadWrite</span></span>|
|<span data-ttu-id="bd452-199">보고서(다른 이름으로 저장)의 복사본을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-199">Save a copy of a report (Save As).</span></span>|<span data-ttu-id="bd452-200">보고서</span><span class="sxs-lookup"><span data-stu-id="bd452-200">Report</span></span>|<span data-ttu-id="bd452-201">* Report.Read</span><span class="sxs-lookup"><span data-stu-id="bd452-201">* Report.Read</span></span><br><span data-ttu-id="bd452-202">* Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="bd452-202">* Workspace.Report.Copy</span></span>|

## <a name="heres-how-hello-flow-works"></a><span data-ttu-id="bd452-203">Hello 흐름이 작동 하는 방법을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-203">Here's how hello flow works</span></span>
1. <span data-ttu-id="bd452-204">Hello API 키 tooyour 응용 프로그램을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-204">Copy hello API keys tooyour application.</span></span> <span data-ttu-id="bd452-205">hello 키를 확인할 수 있습니다 **Azure 포털**합니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-205">You can get hello keys in **Azure Portal**.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. <span data-ttu-id="bd452-206">토큰이 클레임을 어설션하며 만료 시간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-206">Token asserts a claim and has an expiration time.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. <span data-ttu-id="bd452-207">토큰이 API 액세스 키로 서명됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-207">Token gets signed with an API access keys.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. <span data-ttu-id="bd452-208">사용자가 보고서 tooview를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-208">User requests tooview a report.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. <span data-ttu-id="bd452-209">API 액세스 키로 토큰의 유효성이 검사됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-209">Token is validated with an API access keys.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. <span data-ttu-id="bd452-210">Power BI 포함 보고서 toouser를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-210">Power BI Embedded sends a report toouser.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

<span data-ttu-id="bd452-211">후 **Power BI 포함** 보고서 toohello 사용자 보냅니다 hello 사용자 사용자 지정 응용 프로그램에서 hello 보고서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-211">After **Power BI Embedded** sends a report toohello user, hello user can view hello report in your custom app.</span></span> <span data-ttu-id="bd452-212">예를 들어, hello를 가져온 경우 [샘플 판매 데이터 분석 PBIX](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), hello 샘플 웹 응용 프로그램은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bd452-212">For example, if you imported hello [Analyzing Sales Data PBIX sample](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), hello sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a><span data-ttu-id="bd452-213">참고 항목</span><span class="sxs-lookup"><span data-stu-id="bd452-213">See Also</span></span>

[<span data-ttu-id="bd452-214">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="bd452-214">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="bd452-215">Microsoft Power BI Embedded 샘플 시작</span><span class="sxs-lookup"><span data-stu-id="bd452-215">Get started with Microsoft Power BI Embedded sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="bd452-216">일반적인 Microsoft Power BI Embedded 시나리오</span><span class="sxs-lookup"><span data-stu-id="bd452-216">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="bd452-217">Microsoft Power BI Embedded 시작</span><span class="sxs-lookup"><span data-stu-id="bd452-217">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)  
[<span data-ttu-id="bd452-218">PowerBI-CSharp Git 리포지토리</span><span class="sxs-lookup"><span data-stu-id="bd452-218">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
<span data-ttu-id="bd452-219">궁금한 점이 더 있나요?</span><span class="sxs-lookup"><span data-stu-id="bd452-219">More questions?</span></span> [<span data-ttu-id="bd452-220">Power BI 커뮤니티 hello를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="bd452-220">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

