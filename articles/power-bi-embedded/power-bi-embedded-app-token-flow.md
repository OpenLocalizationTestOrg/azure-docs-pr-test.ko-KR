---
title: "Power BI Embedded에서 인증 및 권한 부여"
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
ms.openlocfilehash: 93027f0f5467e0b21c47bbcbc84c67cdd50b26b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a><span data-ttu-id="8f61b-103">Power BI Embedded에서 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="8f61b-103">Authenticating and authorizing with Power BI Embedded</span></span>

<span data-ttu-id="8f61b-104">Power BI Embedded 서비스는 명시적인 최종 사용자 인증 대신 인증 및 권한 부여에 대한 **키** 및 **앱 토큰**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-104">The Power BI Embedded service uses **Keys** and **App Tokens** for authentication and authorization, instead of explicit end-user authentication.</span></span> <span data-ttu-id="8f61b-105">이 모델에서 응용 프로그램이 최종 사용자에 대한 인증 및 권한 부여를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-105">In this model, your application manages authentication and authorization for your end-users.</span></span> <span data-ttu-id="8f61b-106">필요한 경우 앱이 서비스에 요청된 보고서를 렌더링하라고 지시하는 앱 토큰을 만들어 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-106">When necessary, your app creates and sends the App Tokens that tells our service to render the requested report.</span></span> <span data-ttu-id="8f61b-107">이 디자인에서는 앱이 사용자 인증 및 권한 부여에 Azure Active Directory를 사용할 수는 있지만 그럴 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-107">This design doesn't require your app to use Azure Active Directory for user authentication and authorization, although you still can.</span></span>

## <a name="two-ways-to-authenticate"></a><span data-ttu-id="8f61b-108">인증에 대한 두 가지 방법</span><span class="sxs-lookup"><span data-stu-id="8f61b-108">Two ways to authenticate</span></span>

<span data-ttu-id="8f61b-109">**키** - 모든 Power BI Embedded REST API 호출에 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-109">**Key** -  You can use keys for all Power BI Embedded REST API calls.</span></span> <span data-ttu-id="8f61b-110">키는 **Azure 포털**에서 **모든 설정**, **액세스 키**를 차례로 선택하여 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-110">The keys can be found in the **Azure portal** by clicking on **All settings** and then **Access keys**.</span></span> <span data-ttu-id="8f61b-111">키는 항상 암호처럼 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-111">Always treat your key as if it were a password.</span></span> <span data-ttu-id="8f61b-112">특정 작업 영역 컬렉션에서 모든 REST API 호출을 수행하는 권한이 이러한 키에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-112">These keys have permissions to make any REST API call on a particular workspace collection.</span></span>

<span data-ttu-id="8f61b-113">REST 호출에서 키를 사용하려면 다음 권한 부여 헤더를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-113">To use a key on a REST call, add the following authorization header:</span></span>            

    Authorization: AppKey {your key}

<span data-ttu-id="8f61b-114">**앱 토큰** - 앱 토큰은 모든 포함 요청에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-114">**App token** - App tokens are used for all embedding requests.</span></span> <span data-ttu-id="8f61b-115">클라이언트 쪽에서 실행되도록 설계되었으므로 단일 보고서로 제한되며 만료 시간을 설정하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-115">They’re designed to be run client-side, so they're restricted to a single report and it’s best practice to set an expiration time.</span></span>

<span data-ttu-id="8f61b-116">앱 토큰은 사용자 키 중 하나로 서명된 JWT(JSON Web Token)입니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-116">App tokens are a JWT (JSON Web Token) that is signed by one of your keys.</span></span>

<span data-ttu-id="8f61b-117">앱 토큰은 다음 클레임을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-117">Your app token can contain the following claims:</span></span>

| <span data-ttu-id="8f61b-118">클레임</span><span class="sxs-lookup"><span data-stu-id="8f61b-118">Claim</span></span> | <span data-ttu-id="8f61b-119">설명</span><span class="sxs-lookup"><span data-stu-id="8f61b-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8f61b-120">**ver**</span><span class="sxs-lookup"><span data-stu-id="8f61b-120">**ver**</span></span> |<span data-ttu-id="8f61b-121">앱 토큰의 버전으로</span><span class="sxs-lookup"><span data-stu-id="8f61b-121">The version of the app token.</span></span> <span data-ttu-id="8f61b-122">현재 버전은 0.2.0입니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-122">0.2.0 is the current version.</span></span> |
| <span data-ttu-id="8f61b-123">**aud**</span><span class="sxs-lookup"><span data-stu-id="8f61b-123">**aud**</span></span> |<span data-ttu-id="8f61b-124">토큰의 의도한 수신자입니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-124">The intended recipient of the token.</span></span> <span data-ttu-id="8f61b-125">Power BI Embedded의 경우 "https://analysis.windows.net/powerbi/api"를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-125">For Power BI Embedded use: “https://analysis.windows.net/powerbi/api”.</span></span> |
| <span data-ttu-id="8f61b-126">**iss**</span><span class="sxs-lookup"><span data-stu-id="8f61b-126">**iss**</span></span> |<span data-ttu-id="8f61b-127">토큰을 발급한 응용 프로그램을 나타내는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-127">A string indicating the application which issued the token.</span></span> |
| <span data-ttu-id="8f61b-128">**type**</span><span class="sxs-lookup"><span data-stu-id="8f61b-128">**type**</span></span> |<span data-ttu-id="8f61b-129">생성되는 앱 토큰의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-129">The type of app token which is being created.</span></span> <span data-ttu-id="8f61b-130">현재 지원되는 유일한 유형은 **embed**입니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-130">Current the only supported type is **embed**.</span></span> |
| <span data-ttu-id="8f61b-131">**wcn**</span><span class="sxs-lookup"><span data-stu-id="8f61b-131">**wcn**</span></span> |<span data-ttu-id="8f61b-132">토큰이 발급되는 대상 작업 영역 컬렉션 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-132">Workspace collection name the token is being issued for.</span></span> |
| <span data-ttu-id="8f61b-133">**wid**</span><span class="sxs-lookup"><span data-stu-id="8f61b-133">**wid**</span></span> |<span data-ttu-id="8f61b-134">토큰이 발급되는 대상 작업 영역 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-134">Workspace ID the token is being issued for.</span></span> |
| <span data-ttu-id="8f61b-135">**rid**</span><span class="sxs-lookup"><span data-stu-id="8f61b-135">**rid**</span></span> |<span data-ttu-id="8f61b-136">토큰이 발급되는 보고서 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-136">Report ID the token is being issued for.</span></span> |
| <span data-ttu-id="8f61b-137">**username** (선택 사항)</span><span class="sxs-lookup"><span data-stu-id="8f61b-137">**username** (optional)</span></span> |<span data-ttu-id="8f61b-138">RLS에 사용되며 RLS 규칙을 적용할 때 사용자를 식별하는 데 사용할 수 있는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-138">Used with RLS, this is a string that can help identify the user when applying RLS rules.</span></span> |
| <span data-ttu-id="8f61b-139">**roles** (선택 사항)</span><span class="sxs-lookup"><span data-stu-id="8f61b-139">**roles** (optional)</span></span> |<span data-ttu-id="8f61b-140">행 수준 보안 규칙을 적용할 때 선택할 역할이 들어 있는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-140">A string containing the roles to select when applying Row Level Security rules.</span></span> <span data-ttu-id="8f61b-141">둘 이상의 역할을 전달하는 경우 문자열 배열로 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-141">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="8f61b-142">**scp**(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="8f61b-142">**scp** (optional)</span></span> |<span data-ttu-id="8f61b-143">사용 권한 범위를 포함하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-143">A string containing the permissions scopes.</span></span> <span data-ttu-id="8f61b-144">둘 이상의 역할을 전달하는 경우 문자열 배열로 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-144">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="8f61b-145">**exp** (선택 사항)</span><span class="sxs-lookup"><span data-stu-id="8f61b-145">**exp** (optional)</span></span> |<span data-ttu-id="8f61b-146">토큰이 만료될 시간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-146">Indicates the time in which the token will expire.</span></span> <span data-ttu-id="8f61b-147">Unix 타임스탬프로 전달되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-147">These should be passed in as Unix timestamps.</span></span> |
| <span data-ttu-id="8f61b-148">**nbf** (선택 사항)</span><span class="sxs-lookup"><span data-stu-id="8f61b-148">**nbf** (optional)</span></span> |<span data-ttu-id="8f61b-149">토큰이 유효해지는 시작 시간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-149">Indicates the time in which the token starts being valid.</span></span> <span data-ttu-id="8f61b-150">Unix 타임스탬프로 전달되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-150">These should be passed in as Unix timestamps.</span></span> |

<span data-ttu-id="8f61b-151">샘플 앱 토큰은 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-151">A sample app token will look like this:</span></span>

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

<span data-ttu-id="8f61b-152">디코딩되면 결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-152">When decoded, it will look something like this:</span></span>

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

<span data-ttu-id="8f61b-153">앱 토큰을 쉽게 생성하는 SDK 내에서 사용할 수 있는 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-153">There are methods available within the SDKs that make creation of apptokens easier.</span></span> <span data-ttu-id="8f61b-154">예를 들어, .NET의 경우 [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) 클래스 및 [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) 메서드를 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-154">For example, for .NET you can look at the [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) class and the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methods.</span></span>

<span data-ttu-id="8f61b-155">.NET SDK의 경우 [범위](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes)를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-155">For the .NET SDK, you can refer to [Scopes](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span></span>

## <a name="scopes"></a><span data-ttu-id="8f61b-156">범위</span><span class="sxs-lookup"><span data-stu-id="8f61b-156">Scopes</span></span>

<span data-ttu-id="8f61b-157">Embed 토큰으로 사용하는 경우 액세스 권한을 제공하는 리소스 사용을 제한하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-157">When using Embed tokens, you may want to restrict usage of the resources you give access to.</span></span> <span data-ttu-id="8f61b-158">이러한 이유로 범위가 지정된 사용 권한으로 토큰을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-158">For this reason, you can generate a token with scoped permissions.</span></span>

<span data-ttu-id="8f61b-159">Power BI Embedded에 사용 가능한 범위는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-159">The following are the available scopes for Power BI Embedded.</span></span>

|<span data-ttu-id="8f61b-160">범위</span><span class="sxs-lookup"><span data-stu-id="8f61b-160">Scope</span></span>|<span data-ttu-id="8f61b-161">설명</span><span class="sxs-lookup"><span data-stu-id="8f61b-161">Description</span></span>|
|---|---|
|<span data-ttu-id="8f61b-162">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="8f61b-162">Dataset.Read</span></span>|<span data-ttu-id="8f61b-163">지정된 데이터 집합을 읽을 수 있는 사용 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-163">Provides permission to read the specified dataset.</span></span>|
|<span data-ttu-id="8f61b-164">Dataset.Write</span><span class="sxs-lookup"><span data-stu-id="8f61b-164">Dataset.Write</span></span>|<span data-ttu-id="8f61b-165">지정된 데이터 집합을 쓸 수 있는 사용 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-165">Provides permission to write to the specified dataset.</span></span>|
|<span data-ttu-id="8f61b-166">Dataset.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="8f61b-166">Dataset.ReadWrite</span></span>|<span data-ttu-id="8f61b-167">지정된 데이터 집합을 읽고 쓸 수 있는 사용 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-167">Provides permission to read and write to the specificed dataset.</span></span>|
|<span data-ttu-id="8f61b-168">Report.Read</span><span class="sxs-lookup"><span data-stu-id="8f61b-168">Report.Read</span></span>|<span data-ttu-id="8f61b-169">지정된 보고서를 볼 수 있는 사용 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-169">Provides permission to view the specified report.</span></span>|
|<span data-ttu-id="8f61b-170">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="8f61b-170">Report.ReadWrite</span></span>|<span data-ttu-id="8f61b-171">지정된 보고서를 보고 편집할 수 있는 사용 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-171">Provides permission to view and edit the specified report.</span></span>|
|<span data-ttu-id="8f61b-172">Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="8f61b-172">Workspace.Report.Create</span></span>|<span data-ttu-id="8f61b-173">지정된 작업 영역 내에서 새 보고서를 만들 수 있는 사용 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-173">Provides permission to create a new report within the specified workspace.</span></span>|
|<span data-ttu-id="8f61b-174">Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="8f61b-174">Workspace.Report.Copy</span></span>|<span data-ttu-id="8f61b-175">지정된 작업 영역 내에서 기존 보고서를 복제할 수 있는 사용 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-175">Provides permission to clone an existing report within the specified workspace.</span></span>|

<span data-ttu-id="8f61b-176">다음과 같은 범위 간의 공백을 사용하여 여러 범위를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-176">You can supply multiple scopes by using a space between the scopes like the following.</span></span>

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

<span data-ttu-id="8f61b-177">**필요한 클레임 - 범위**</span><span class="sxs-lookup"><span data-stu-id="8f61b-177">**Required claims - scopes**</span></span>

<span data-ttu-id="8f61b-178">scp: {scopesClaim} scopesClaim은 문자열 또는 문자열의 배열로서 작업 영역 리소스(예: 보고서, 데이터 집합 등)에 허용되는 사용 권한을 확인할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="8f61b-178">scp: {scopesClaim} scopesClaim can be either a string or array of strings, noting the allowed permissions to workspace resources (Report, Dataset, etc.)</span></span>

<span data-ttu-id="8f61b-179">정의된 범위를 사용하여 디코딩된 토큰은 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-179">A decoded token, with scopes defined, would look similar to the following.</span></span>

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

### <a name="operations-and-scopes"></a><span data-ttu-id="8f61b-180">작업 및 범위</span><span class="sxs-lookup"><span data-stu-id="8f61b-180">Operations and scopes</span></span>

|<span data-ttu-id="8f61b-181">작업</span><span class="sxs-lookup"><span data-stu-id="8f61b-181">Operation</span></span>|<span data-ttu-id="8f61b-182">대상 리소스</span><span class="sxs-lookup"><span data-stu-id="8f61b-182">Target resource</span></span>|<span data-ttu-id="8f61b-183">토큰 사용 권한</span><span class="sxs-lookup"><span data-stu-id="8f61b-183">Token permissions</span></span>|
|---|---|---|
|<span data-ttu-id="8f61b-184">데이터 집합을 기반으로 새 메모리 내 보고서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-184">Create (in-memory) a new report based on a dataset.</span></span>|<span data-ttu-id="8f61b-185">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="8f61b-185">Dataset</span></span>|<span data-ttu-id="8f61b-186">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="8f61b-186">Dataset.Read</span></span>|
|<span data-ttu-id="8f61b-187">데이터 집합을 기반으로 새 메모리 내 보고서를 만들고 보고서를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-187">Create (in-memory) a new report based on a dataset and save the report.</span></span>|<span data-ttu-id="8f61b-188">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="8f61b-188">Dataset</span></span>|<span data-ttu-id="8f61b-189">* Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="8f61b-189">* Dataset.Read</span></span><br><span data-ttu-id="8f61b-190">* Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="8f61b-190">* Workspace.Report.Create</span></span>|
|<span data-ttu-id="8f61b-191">기존 메모리 내 보고서를 보고 탐색/편집합니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-191">View and explore/edit (in-memory) an existing report.</span></span> <span data-ttu-id="8f61b-192">Report.Read는 Dataset.Read를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-192">Report.Read implies Dataset.Read.</span></span> <span data-ttu-id="8f61b-193">그러면 편집 내용을 저장하는 사용 권한을 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-193">This will not allow permissions to save edits.</span></span>|<span data-ttu-id="8f61b-194">보고서</span><span class="sxs-lookup"><span data-stu-id="8f61b-194">Report</span></span>|<span data-ttu-id="8f61b-195">Report.Read</span><span class="sxs-lookup"><span data-stu-id="8f61b-195">Report.Read</span></span>|
|<span data-ttu-id="8f61b-196">기존 보고서를 편집하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-196">Edit and save an existing report.</span></span>|<span data-ttu-id="8f61b-197">보고서</span><span class="sxs-lookup"><span data-stu-id="8f61b-197">Report</span></span>|<span data-ttu-id="8f61b-198">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="8f61b-198">Report.ReadWrite</span></span>|
|<span data-ttu-id="8f61b-199">보고서(다른 이름으로 저장)의 복사본을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-199">Save a copy of a report (Save As).</span></span>|<span data-ttu-id="8f61b-200">보고서</span><span class="sxs-lookup"><span data-stu-id="8f61b-200">Report</span></span>|<span data-ttu-id="8f61b-201">* Report.Read</span><span class="sxs-lookup"><span data-stu-id="8f61b-201">* Report.Read</span></span><br><span data-ttu-id="8f61b-202">* Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="8f61b-202">* Workspace.Report.Copy</span></span>|

## <a name="heres-how-the-flow-works"></a><span data-ttu-id="8f61b-203">다음은 흐름 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-203">Here's how the flow works</span></span>
1. <span data-ttu-id="8f61b-204">응용 프로그램에 API 키 복사</span><span class="sxs-lookup"><span data-stu-id="8f61b-204">Copy the API keys to your application.</span></span> <span data-ttu-id="8f61b-205">**Azure Portal**에서 키를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-205">You can get the keys in **Azure Portal**.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. <span data-ttu-id="8f61b-206">토큰이 클레임을 어설션하며 만료 시간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-206">Token asserts a claim and has an expiration time.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. <span data-ttu-id="8f61b-207">토큰이 API 액세스 키로 서명됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-207">Token gets signed with an API access keys.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. <span data-ttu-id="8f61b-208">사용자가 보고서 보기를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-208">User requests to view a report.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. <span data-ttu-id="8f61b-209">API 액세스 키로 토큰의 유효성이 검사됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-209">Token is validated with an API access keys.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. <span data-ttu-id="8f61b-210">Power BI Embedded에서 사용자에게 보고서를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-210">Power BI Embedded sends a report to user.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

<span data-ttu-id="8f61b-211">**Power BI Embedded** 에서 사용자에게 보고서를 보낸 후 사용자는 사용자 지정 앱에서 보고서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-211">After **Power BI Embedded** sends a report to the user, the user can view the report in your custom app.</span></span> <span data-ttu-id="8f61b-212">예를 들어 [판매 데이터 PBIX 분석 샘플](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix)을 가져온 경우 샘플 웹앱이 다음과 같이 보입니다.</span><span class="sxs-lookup"><span data-stu-id="8f61b-212">For example, if you imported the [Analyzing Sales Data PBIX sample](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), the sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a><span data-ttu-id="8f61b-213">참고 항목</span><span class="sxs-lookup"><span data-stu-id="8f61b-213">See Also</span></span>

[<span data-ttu-id="8f61b-214">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="8f61b-214">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="8f61b-215">Microsoft Power BI Embedded 샘플 시작</span><span class="sxs-lookup"><span data-stu-id="8f61b-215">Get started with Microsoft Power BI Embedded sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="8f61b-216">일반적인 Microsoft Power BI Embedded 시나리오</span><span class="sxs-lookup"><span data-stu-id="8f61b-216">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="8f61b-217">Microsoft Power BI Embedded 시작</span><span class="sxs-lookup"><span data-stu-id="8f61b-217">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)  
[<span data-ttu-id="8f61b-218">PowerBI-CSharp Git 리포지토리</span><span class="sxs-lookup"><span data-stu-id="8f61b-218">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
<span data-ttu-id="8f61b-219">궁금한 점이 더 있나요?</span><span class="sxs-lookup"><span data-stu-id="8f61b-219">More questions?</span></span> [<span data-ttu-id="8f61b-220">Power BI 커뮤니티를 이용하세요.</span><span class="sxs-lookup"><span data-stu-id="8f61b-220">Try the Power BI Community</span></span>](http://community.powerbi.com/)

