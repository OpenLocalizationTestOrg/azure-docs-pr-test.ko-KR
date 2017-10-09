---
title: "aaaConfigure 인증 및 권한 부여를 호출 하는 사용자 지정 응용 프로그램에 대 한 Azure 시간 시계열 인 사이트 API hello | Microsoft Docs"
description: "이 자습서에서는 어떻게 tooconfigure 인증 및 권한 부여를 호출 하는 사용자 지정 응용 프로그램에 대 한 hello Azure 시간 시계열 인 사이트 API에 설명"
keywords: 
services: time-series-insights
documentationcenter: 
author: dmdenmsft
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/24/2017
ms.author: dmden
ms.openlocfilehash: 5043468bfc2af3c0d27e8602508d92ba2848409e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-azure-time-series-insights-api"></a><span data-ttu-id="1dd41-103">Azure Time Series Insights API에 대한 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="1dd41-103">Authentication and authorization for Azure Time Series Insights API</span></span>

<span data-ttu-id="1dd41-104">이 문서에서는 tooconfigure를 호출 하는 사용자 지정 응용 프로그램의 Azure 시간 시계열 인 사이트 API hello 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-104">This article explains how tooconfigure a custom application that calls hello Azure Time Series Insights API.</span></span>

## <a name="service-principal"></a><span data-ttu-id="1dd41-105">서비스 주체</span><span class="sxs-lookup"><span data-stu-id="1dd41-105">Service principal</span></span>

<span data-ttu-id="1dd41-106">이 섹션에서는 응용 프로그램 tooaccess tooconfigure 시간 시계열 인 사이트 API hello 응용 프로그램을 대신 하 여 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-106">This section explains how tooconfigure an application tooaccess hello Time Series Insights API on behalf of hello application.</span></span> <span data-ttu-id="1dd41-107">hello 응용 프로그램 수 데이터 쿼리하거나 hello 사용자 자격 증명이 아니라 응용 프로그램 자격 증명으로 hello 시간 계열 Insights 환경에 참조 데이터에 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-107">hello application can then query data or publish reference data in hello Time Series Insights environment with application credentials and not hello user credentials.</span></span>

<span data-ttu-id="1dd41-108">시간 시계열 Insights tooaccess 하는 응용 프로그램을 사용 하는 경우에 Azure Active Directory 응용 프로그램을 설정 하 고 hello 시간 계열 Insights 환경에서 hello 데이터 액세스 정책을 할당 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-108">When you have an application that needs tooaccess Time Series Insights, you must set up an Azure Active Directory application and assign hello data access policies in hello Time Series Insights environment.</span></span> <span data-ttu-id="1dd41-109">이 방법은 것이 좋습니다 toorunning hello 앱 자신의 자격 증명 때문에:</span><span class="sxs-lookup"><span data-stu-id="1dd41-109">This approach is preferable toorunning hello app under your own credentials because:</span></span>

* <span data-ttu-id="1dd41-110">권한을 toohello 응용 프로그램 id가 다른 고유한 사용 권한을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-110">You can assign permissions toohello app identity that are different from your own permissions.</span></span> <span data-ttu-id="1dd41-111">일반적으로 이러한 권한은 제한 된 tooexactly 어떤 hello 앱 toodo 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-111">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span> <span data-ttu-id="1dd41-112">예를 들어 hello 앱 tooonly 특정 시간 시계열 Insights 환경에서 데이터를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-112">For example, you can allow hello app tooonly read data in a particular Time Series Insights environment.</span></span>
* <span data-ttu-id="1dd41-113">사용자의 책임을 변경 하는 경우 toochange hello 응용 프로그램의 자격 증명이 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-113">You don't have toochange hello app's credentials if your responsibilities change.</span></span>
* <span data-ttu-id="1dd41-114">무인 설치 스크립트를 실행 하는 경우 인증서 또는 응용 프로그램 키 tooautomate 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-114">You can use a certificate or an application key tooautomate authentication when you're running an unattended script.</span></span>

<span data-ttu-id="1dd41-115">이 문서 하는 것을 단계별로 tooperform Azure 포털 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-115">This article shows you how tooperform those steps through hello Azure portal.</span></span> <span data-ttu-id="1dd41-116">여기서 hello 응용 프로그램은 한 조직에서 의도 한 toorun 단일 테 넌 트 응용 프로그램에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-116">It focuses on a single-tenant application where hello application is intended toorun in only one organization.</span></span> <span data-ttu-id="1dd41-117">일반적으로 단일 조직에서 실행되는 LOB(기간 업무) 응용 프로그램에 대해 단일 테넌트 응용 프로그램을 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-117">You typically use single-tenant applications for line-of-business applications that run in your organization.</span></span>

<span data-ttu-id="1dd41-118">hello 설정 흐름 이라는 세 단계로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-118">hello setup flow consists of three high-level steps:</span></span>

1. <span data-ttu-id="1dd41-119">Azure Active Directory에서 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-119">Create an application in Azure Active Directory.</span></span>
2. <span data-ttu-id="1dd41-120">이 응용 프로그램 tooaccess hello 시간 계열 Insights 환경에 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-120">Authorize this application tooaccess hello Time Series Insights environment.</span></span>
3. <span data-ttu-id="1dd41-121">Hello 응용 프로그램 ID 및 키 tooacquire 토큰 toohello 사용 하 여 `"https://api.timeseries.azure.com/"` 대상 또는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-121">Use hello application ID and key tooacquire a token toohello `"https://api.timeseries.azure.com/"` audience or resource.</span></span> <span data-ttu-id="1dd41-122">hello 토큰 사용된 toocall hello 시간 시계열 인 사이트 API 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-122">hello token can then be used toocall hello Time Series Insights API.</span></span>

<span data-ttu-id="1dd41-123">자세한 단계 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-123">Here are hello detailed steps:</span></span>

1. <span data-ttu-id="1dd41-124">Hello Azure 포털에서에서 선택 **Azure Active Directory** > **앱 등록** > **새 응용 프로그램 등록**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-124">In hello Azure portal, select **Azure Active Directory** > **App registrations** > **New application registration**.</span></span>

   ![Azure Active Directory에서 새 응용 프로그램 등록](media/authentication-and-authorization/active-directory-new-application-registration.png)  

2. <span data-ttu-id="1dd41-126">Hello 응용 프로그램 이름, 선택 hello 유형 toobe 제공 **웹 응용 프로그램 / API**, 모든 유효한 URI 선택 **로그온 URL**, 클릭 하 고 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-126">Give hello application a name, select hello type toobe **Web app / API**, select any valid URI for **Sign-on URL**, and click **Create**.</span></span>

   ![Azure Active Directory에서 hello 응용 프로그램 만들기](media/authentication-and-authorization/active-directory-create-web-api-application.png)

3. <span data-ttu-id="1dd41-128">새로 만든된 응용 프로그램을 선택 하 고 해당 응용 프로그램 ID tooyour 원하는 텍스트 편집기에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-128">Select your newly created application and copy its application ID tooyour favorite text editor.</span></span>

   ![Hello 응용 프로그램 ID를 복사 합니다.](media/authentication-and-authorization/active-directory-copy-application-id.png)

4. <span data-ttu-id="1dd41-130">선택 **키**, 선택 hello 만료 hello 키 이름을 입력 하 고 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-130">Select **Keys**, enter hello key name, select hello expiration, and click **Save**.</span></span>

   ![응용 프로그램 키 선택](media/authentication-and-authorization/active-directory-application-keys.png)

   ![Hello 키 이름 및 만료를 입력 하 고 저장을 클릭 합니다.](media/authentication-and-authorization/active-directory-application-keys-save.png)

5. <span data-ttu-id="1dd41-133">Hello 키 tooyour 원하는 텍스트 편집기에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-133">Copy hello key tooyour favorite text editor.</span></span>

   ![Hello 응용 프로그램 키를 복사 합니다.](media/authentication-and-authorization/active-directory-copy-application-key.png)

6. <span data-ttu-id="1dd41-135">Hello 시간 계열 Insights 환경에 대 한 선택 **데이터 액세스 정책을** 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-135">For hello Time Series Insights environment, select **Data Access Policies** and click **Add**.</span></span>

   ![새 데이터 액세스 정책 toohello 시간 계열 Insights 환경 추가](media/authentication-and-authorization/time-series-insights-data-access-policies-add.png)

7. <span data-ttu-id="1dd41-137">Hello에 **사용자 선택** 대화 상자, 붙여넣기 hello 응용 프로그램 이름 (2 단계) 또는 (3 단계)에서 응용 프로그램 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-137">In hello **Select User** dialog box, paste hello application name (from step 2) or application ID (from step 3).</span></span>

   ![Hello 사용자 선택 대화 상자에서 응용 프로그램 찾기](media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png)

8. <span data-ttu-id="1dd41-139">선택 hello 역할 (**판독기** 데이터를 쿼리 하기 위한 **참가자** 데이터를 쿼리 및 참조 데이터 변경에 대 한)를 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-139">Select hello role (**Reader** for querying data, **Contributor** for querying data and changing reference data) and click **Ok**.</span></span>

   ![판독기 또는 참가자로 hello 역할 선택 대화 상자에서 선택](media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png)

9. <span data-ttu-id="1dd41-141">클릭 하 여 hello 정책 저장 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-141">Save hello policy by clicking **Ok**.</span></span>

10. <span data-ttu-id="1dd41-142">(3 단계)에서 응용 프로그램 ID hello 및 hello 응용 프로그램을 대신 하 여 응용 프로그램 (5 단계)에서 키 tooacquire hello 토큰을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-142">Use hello application ID (from step 3) and application key (from step 5) tooacquire hello token on behalf of hello application.</span></span> <span data-ttu-id="1dd41-143">hello 토큰 전달 될 수 hello에 `Authorization` hello 응용 프로그램 호출 시간 시계열 인 사이트 API hello 때 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-143">hello token can then be passed in hello `Authorization` header when hello application calls hello Time Series Insights API.</span></span>

    <span data-ttu-id="1dd41-144">C#을 사용 하는 경우에 hello 코드 tooacquire hello 토큰 hello 응용 프로그램을 대신 하 여 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-144">If you're using C#, you can use hello following code tooacquire hello token on behalf of hello application.</span></span> <span data-ttu-id="1dd41-145">전체 샘플은 [C#을 사용하여 데이터 쿼리](time-series-insights-query-data-csharp.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1dd41-145">For a complete sample, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

    ```csharp
    var authenticationContext = new AuthenticationContext(
        "https://login.microsoftonline.com/common",
        TokenCache.DefaultShared);

    AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
        // Set hello resource URI toohello Azure Time Series Insights API
        resource: "https://api.timeseries.azure.com/", 
        clientCredential: new ClientCredential(
            // Application ID of application registered in Azure Active Directory
            clientId: "1bc3af48-7e2f-4845-880a-c7649a6470b8", 
            // Application key of hello application that's registered in Azure Active Directory
            clientSecret: "aBcdEffs4XYxoAXzLB1n3R2meNCYdGpIGBc2YC5D6L2="));

    string accessToken = token.AccessToken;
    ```

## <a name="next-steps"></a><span data-ttu-id="1dd41-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1dd41-146">Next steps</span></span>

<span data-ttu-id="1dd41-147">응용 프로그램에서 hello 응용 프로그램 ID 및 키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-147">Use hello application ID and key in your application.</span></span> <span data-ttu-id="1dd41-148">Hello 시간 시계열 인 사이트 API를 호출 하는 샘플 코드에 대 한 참조 [C#을 사용 하 여 데이터를 쿼리할](time-series-insights-query-data-csharp.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd41-148">For sample code that calls hello Time Series Insights API, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="1dd41-149">참고 항목</span><span class="sxs-lookup"><span data-stu-id="1dd41-149">See also</span></span>

* <span data-ttu-id="1dd41-150">[API를 쿼리하여](/rest/api/time-series-insights/time-series-insights-reference-queryapi) hello 전체 쿼리 API 참조에 대 한</span><span class="sxs-lookup"><span data-stu-id="1dd41-150">[Query API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) for hello full Query API reference</span></span>
* [<span data-ttu-id="1dd41-151">서비스를 hello Azure 포털에서에서 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1dd41-151">Create a service principal in hello Azure portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
