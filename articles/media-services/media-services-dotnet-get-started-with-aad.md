---
title: "Azure AD 인증.NET을 사용 하 여 Azure 미디어 서비스 API tooaccess aaaUse | Microsoft Docs"
description: "이 항목에서는 Azure 미디어 서비스 하는 Azure Active Directory (Azure AD) 인증 tooaccess toouse 방법을 보여 줍니다..net AMS () API입니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 2f750e460d9e476ad92e96adeac6500cb692cd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-ad-authentication-tooaccess-azure-media-services-api-with-net"></a><span data-ttu-id="d165d-103">Azure AD 인증 tooaccess Azure 미디어 서비스 API를 사용 하 여.net</span><span class="sxs-lookup"><span data-stu-id="d165d-103">Use Azure AD authentication tooaccess Azure Media Services API with .NET</span></span>

<span data-ttu-id="d165d-104">windowsazure.mediaservices 4.0.0.4부터는 Azure Media Services에서 Azure AD(Azure Active Directory) 기반 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-104">Starting with windowsazure.mediaservices 4.0.0.4, Azure Media Services supports authentication based on Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="d165d-105">이 항목에서는 Azure AD 인증 tooaccess Microsoft.net Azure 미디어 서비스 API toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-105">This topic shows you how toouse Azure AD  authentication tooaccess Azure Media Services API with Microsoft .NET.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d165d-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d165d-106">Prerequisites</span></span>

- <span data-ttu-id="d165d-107">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="d165d-107">An Azure account.</span></span> <span data-ttu-id="d165d-108">자세한 내용은 [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d165d-108">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="d165d-109">Media Services 계정.</span><span class="sxs-lookup"><span data-stu-id="d165d-109">A Media Services account.</span></span> <span data-ttu-id="d165d-110">자세한 내용은 참조 [hello Azure 포털을 사용 하 여 Azure 미디어 서비스 계정 만들기](media-services-portal-create-account.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-110">For more information, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="d165d-111">최신 hello [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-111">hello latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span>
- <span data-ttu-id="d165d-112">Hello 항목 익숙하다고 [AAD 인증 개요를 사용 하 여 Azure 미디어 서비스 API에 액세스](media-services-use-aad-auth-to-access-ams-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-112">Familiarity with hello topic [Accessing Azure Media Services API with AAD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="d165d-113">Azure Media Services와 함께 Azure AD 인증을 사용할 때 다음 두 가지 방법 중 하나로 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-113">When you're using Azure AD authentication with Azure Media Services, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="d165d-114">**사용자 인증** hello 앱 toointeract Azure 미디어 서비스 리소스와 함께 사용 하는 사람을 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-114">**User authentication** authenticates a person who is using hello app toointeract with Azure Media Services resources.</span></span> <span data-ttu-id="d165d-115">먼저 hello 대화형 응용 프로그램에는 hello 사용자에 게 자격 라는 메시지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-115">hello interactive application should first prompt hello user for credentials.</span></span> <span data-ttu-id="d165d-116">예에는 라이브 스트리밍 또는 권한이 있는 사용자 toomonitor 인코딩 작업에서 사용 하는 관리 콘솔 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-116">An example is a management console app that's used by authorized users toomonitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="d165d-117">**서비스 주체 인증**은 서비스를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-117">**Service principal authentication** authenticates a service.</span></span> <span data-ttu-id="d165d-118">이 인증 방법을 일반적으로 사용하는 응용 프로그램은 디먼 서비스, 중간 계층 서비스 또는 예약된 작업(예: 웹앱, 함수 앱, 논리 앱, API 또는 마이크로 서비스)을 실행하는 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs, such as web apps, function apps, logic apps, APIs, or microservices.</span></span>

>[!IMPORTANT]
><span data-ttu-id="d165d-119">현재 Azure Media Services는 Azure Access Control Service 인증 모델을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-119">Azure Media Service currently supports an Azure Access Control Service  authentication model.</span></span> <span data-ttu-id="d165d-120">그러나 액세스 제어 권한 부여는 toobe 2018 년 6 월 1에서 더 이상 사용 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-120">However, Access Control authorization is going toobe deprecated on June 1, 2018.</span></span> <span data-ttu-id="d165d-121">Tooan Azure Active Directory 인증 모델을 최대한 빨리 마이그레이션하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-121">We recommend that you migrate tooan Azure Active Directory authentication model as soon as possible.</span></span>

## <a name="get-an-azure-ad-access-token"></a><span data-ttu-id="d165d-122">Azure AD 액세스 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="d165d-122">Get an Azure AD access token</span></span>

<span data-ttu-id="d165d-123">Azure AD 인증 tooconnect toohello Azure 미디어 서비스 API를 hello 클라이언트 응용 프로그램 toorequest Azure AD 액세스 토큰을 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-123">tooconnect toohello Azure Media Services API with Azure AD authentication, hello client app needs toorequest an Azure AD access token.</span></span> <span data-ttu-id="d165d-124">Hello 미디어 서비스.NET SDK tooacquire는 Azure AD 액세스 토큰은 래핑된 하 고 hello를 간소화 하는 방법에 대 한 hello 정보의 많은 클라이언트를 사용 하는 경우 [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) 및 [AzureAdTokenCredentials ](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-124">When you use hello Media Services .NET client SDK, many of hello details about how tooacquire an Azure AD access token are wrapped and simplified for you in hello [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) and [AzureAdTokenCredentials](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) classes.</span></span> 

<span data-ttu-id="d165d-125">예를 들어 않아도 tooprovide hello Azure AD 인증 기관, URI, 미디어 서비스 리소스 또는 네이티브 Azure AD 응용 프로그램 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-125">For example, you don't need tooprovide hello Azure AD authority, Media Services resource URI, or native Azure AD application details.</span></span> <span data-ttu-id="d165d-126">이들은 hello Azure AD 액세스 토큰 공급자 클래스에서 이미 구성 되어 있는 잘 알려진 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-126">These are well-known values that are already configured by hello Azure AD access token provider class.</span></span> 

<span data-ttu-id="d165d-127">Azure 미디어 서비스.NET SDK를 사용 하지 않는 경우 hello를 사용 하는 것이 좋습니다 [Azure AD 인증 라이브러리](../active-directory/develop/active-directory-authentication-libraries.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-127">If you are not using Azure Media Service .NET SDK, we recommend that you use hello [Azure AD Authentication Library](../active-directory/develop/active-directory-authentication-libraries.md).</span></span> <span data-ttu-id="d165d-128">Azure AD 인증 라이브러리와 toouse 해야 하는 hello 매개 변수에 대 한 tooget 값 참조 [hello Azure 포털 tooaccess Azure AD 인증 설정을 사용 하 여](media-services-portal-get-started-with-aad.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-128">tooget values for hello parameters that you need toouse with Azure AD Authentication Library, see [Use hello Azure portal tooaccess Azure AD authentication settings](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="d165d-129">교체 hello의 기본 구현은 hello hello 옵션도 제공 **AzureAdTokenProvider** 사용자 구현으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-129">You also have hello option of replacing hello default implementation of hello **AzureAdTokenProvider** with your own implementation.</span></span>

## <a name="install-and-configure-azure-media-services-net-sdk"></a><span data-ttu-id="d165d-130">Azure Media Services .NET SDK 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="d165d-130">Install and configure Azure Media Services .NET SDK</span></span>

>[!NOTE] 
><span data-ttu-id="d165d-131">미디어 서비스.NET SDK hello로 toouse Azure AD 인증을 해야 toohave hello 최신 [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-131">toouse Azure AD authentication with hello Media Services .NET SDK, you need toohave hello latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span> <span data-ttu-id="d165d-132">또한 참조 toohello 추가 **Microsoft.IdentityModel.Clients.ActiveDirectory** 어셈블리입니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-132">Also, add a reference toohello **Microsoft.IdentityModel.Clients.ActiveDirectory** assembly.</span></span> <span data-ttu-id="d165d-133">기존 앱을 사용 하는 경우 포함 hello **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** 어셈블리입니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-133">If you are using an existing app, include hello **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** assembly.</span></span> 

1. <span data-ttu-id="d165d-134">Visual Studio를 사용하여 새 C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-134">Create a new C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="d165d-135">사용 하 여 hello [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) NuGet 패키지 tooinstall **Azure 미디어 서비스.NET SDK**합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-135">Use hello [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) NuGet package tooinstall **Azure Media Services .NET SDK**.</span></span> 

    <span data-ttu-id="d165d-136">NuGet을 사용 하 여 tooadd 참조 수행할 단계를 수행 하는 hello:에서 **솔루션 탐색기**를 hello 프로젝트 이름을 마우스 오른쪽 단추로 클릭 한 다음 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-136">tooadd references by using NuGet, take hello following steps: in **Solution Explorer**, right-click hello project name, and then select **Manage NuGet packages**.</span></span> <span data-ttu-id="d165d-137">그런 다음 **windowsazure.mediaservices**를 검색하고 **설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-137">Then, search for **windowsazure.mediaservices** and select **Install**.</span></span>
    
    <span data-ttu-id="d165d-138">또는</span><span class="sxs-lookup"><span data-stu-id="d165d-138">-or-</span></span>

    <span data-ttu-id="d165d-139">실행 hello 다음에 명령을 **패키지 관리자 콘솔** Visual Studio에서.</span><span class="sxs-lookup"><span data-stu-id="d165d-139">Run hello following command in **Package Manager Console** in Visual Studio.</span></span>

        Install-Package windowsazure.mediaservices -Version 4.0.0.4

3. <span data-ttu-id="d165d-140">추가 **를 사용 하 여** tooyour 소스 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-140">Add **using** tooyour source code.</span></span>

        using Microsoft.WindowsAzure.MediaServices.Client; 

## <a name="use-user-authentication"></a><span data-ttu-id="d165d-141">사용자 인증 사용</span><span class="sxs-lookup"><span data-stu-id="d165d-141">Use user authentication</span></span>

<span data-ttu-id="d165d-142">tooconnect toohello hello 사용자 인증 옵션과 함께 Azure 미디어 서비스 API, hello 클라이언트 응용 프로그램에는 Azure AD 토큰을 사용 하 여 매개 변수 뒤 hello toorequest 항목이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-142">tooconnect toohello Azure Media Service API with hello user authentication option, hello client app needs toorequest an Azure AD token by using hello following parameters:</span></span>  

- <span data-ttu-id="d165d-143">Azure AD 테넌트 끝점.</span><span class="sxs-lookup"><span data-stu-id="d165d-143">Azure AD tenant endpoint.</span></span> <span data-ttu-id="d165d-144">hello Azure 포털에서에서 hello 테 넌 트 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-144">hello tenant information can be retrieved from hello Azure portal.</span></span> <span data-ttu-id="d165d-145">Hello 로그인 한 사용자 hello 오른쪽 위 모서리에 올려 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-145">Hover over hello signed-in user in hello upper-right corner.</span></span>
- <span data-ttu-id="d165d-146">Media Services 리소스 URI.</span><span class="sxs-lookup"><span data-stu-id="d165d-146">Media Services resource URI.</span></span>
- <span data-ttu-id="d165d-147">Media Services(원시) 응용 프로그램 클라이언트 ID.</span><span class="sxs-lookup"><span data-stu-id="d165d-147">Media Services (native) application client ID.</span></span> 
- <span data-ttu-id="d165d-148">Media Services(원시) 응용 프로그램 리디렉션 URI.</span><span class="sxs-lookup"><span data-stu-id="d165d-148">Media Services (native) application redirect URI.</span></span> 

<span data-ttu-id="d165d-149">이러한 매개 변수에 대 한 hello 값에서 찾을 수 있습니다 **AzureEnvironments.AzureCloudEnvironment**합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-149">hello values for these parameters can be found in **AzureEnvironments.AzureCloudEnvironment**.</span></span> <span data-ttu-id="d165d-150">hello **AzureEnvironments.AzureCloudEnvironment** 상수이 함수는 hello.NET SDK tooget에서 공용 Azure 데이터 센터에 대 한 hello 오른쪽 환경 변수 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-150">hello **AzureEnvironments.AzureCloudEnvironment** constant is a helper in hello .NET SDK tooget hello right environment variable settings for a public Azure Data Center.</span></span> 

<span data-ttu-id="d165d-151">공용 데이터 센터 전용 hello에에서 미디어 서비스에 액세스 하기 위한 미리 정의 된 환경 설정을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-151">It contains pre-defined environment settings for accessing Media Services in hello public data centers only.</span></span> <span data-ttu-id="d165d-152">독립 또는 정부 클라우드 지역의 경우 **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment** 또는 **AzureGermanCloudEnvironment**를 각각 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-152">For sovereign or government cloud regions, you can use **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment**, or **AzureGermanCloudEnvironment** respectively.</span></span>

<span data-ttu-id="d165d-153">다음 코드 예제는 hello 토큰을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-153">hello following code example creates a token:</span></span>
    
    var tokenCredentials = new AzureAdTokenCredentials("microsoft.onmicrosoft.com", AzureEnvironments.AzureCloudEnvironment);
    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
  
<span data-ttu-id="d165d-154">toostart 미디어 서비스를 대상으로 프로그래밍 해야 toocreate는 **CloudMediaContext** hello 서버 컨텍스트를 나타내는 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-154">toostart programming against Media Services, you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="d165d-155">hello **CloudMediaContext** 작업, 자산, 파일, 액세스 정책 및 로케이터를 포함 하 여 참조 tooimportant 컬렉션이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-155">hello **CloudMediaContext** includes references tooimportant collections including jobs, assets, files, access policies, and locators.</span></span> 

<span data-ttu-id="d165d-156">또한 toopass hello 해야 **리소스 미디어 REST 서비스에 대 한 URI** toohello **CloudMediaContext** 생성자입니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-156">You also need toopass hello **resource URI for Media REST Services** toohello **CloudMediaContext** constructor.</span></span> <span data-ttu-id="d165d-157">tooget hello 리소스 URI 미디어 REST 서비스에서 toohello Azure 포털에에서 로그인 사용자의 Azure 미디어 서비스 계정 선택에 대 한 선택 **API 액세스**를 선택한 후 **tooAzure 미디어 서비스 사용자와 연결 인증**합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-157">tooget hello resource URI for Media REST Services, sign in toohello Azure portal, select your Azure Media Services account, select **API access**, and then select **Connect tooAzure Media Services with user authentication**.</span></span> 

<span data-ttu-id="d165d-158">hello 다음 코드 예제에서는 한 **CloudMediaContext** 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="d165d-158">hello following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);

<span data-ttu-id="d165d-159">다음 예제는 hello toocreate Azure AD 토큰 및 hello 컨텍스트가 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-159">hello following example shows how toocreate hello Azure AD token and hello context:</span></span>

    namespace AADAuthSample
    {
        class Program
        {
            static void Main(string[] args)
            {
                // Specify your Azure AD tenant domain, for example "microsoft.onmicrosoft.com".
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR AAD TENANT DOMAIN HERE}", AzureEnvironments.AzureCloudEnvironment);
    
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
            }
    
        }
    }

>[!NOTE]
><span data-ttu-id="d165d-160">라고 표시 하는 예외를 발생 하는 경우 "hello 원격 서버에 오류가 반환 되었습니다: (401) 권한 없음" hello 참조 [액세스 제어](media-services-use-aad-auth-to-access-ams-api.md#access-control) Azure 미디어 서비스 API에 액세스의 Azure AD 인증 개요 섹션.</span><span class="sxs-lookup"><span data-stu-id="d165d-160">If you get an exception that says "hello remote server returned an error: (401) Unauthorized," see hello [Access control](media-services-use-aad-auth-to-access-ams-api.md#access-control) section of Accessing Azure Media Services API with Azure AD authentication overview.</span></span>

## <a name="use-service-principal-authentication"></a><span data-ttu-id="d165d-161">서비스 주체 인증 사용</span><span class="sxs-lookup"><span data-stu-id="d165d-161">Use service principal authentication</span></span>
    
<span data-ttu-id="d165d-162">tooconnect toohello Azure 미디어 서비스 API hello 서비스 보안 주체 옵션으로, 중간 계층 응용 프로그램 (웹 API 또는 웹 응용 프로그램) 매개 변수 뒤 hello로 toorequests는 Azure AD 토큰 항목이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-162">tooconnect toohello Azure Media Services API with hello service principal option, your middle-tier app (web API or web application) needs toorequests an Azure AD token with hello following parameters:</span></span>  

- <span data-ttu-id="d165d-163">Azure AD 테넌트 끝점.</span><span class="sxs-lookup"><span data-stu-id="d165d-163">Azure AD tenant endpoint.</span></span> <span data-ttu-id="d165d-164">hello Azure 포털에서에서 hello 테 넌 트 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-164">hello tenant information can be retrieved from hello Azure portal.</span></span> <span data-ttu-id="d165d-165">Hello 로그인 한 사용자 hello 오른쪽 위 모서리에 올려 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-165">Hover over hello signed-in user in hello upper-right corner.</span></span>
- <span data-ttu-id="d165d-166">Media Services 리소스 URI.</span><span class="sxs-lookup"><span data-stu-id="d165d-166">Media Services resource URI.</span></span>
- <span data-ttu-id="d165d-167">Azure AD 응용 프로그램 값: hello **클라이언트 ID** 및 **클라이언트 암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-167">Azure AD application values: hello **Client ID** and **Client secret**.</span></span>

<span data-ttu-id="d165d-168">hello에 대 한 값을 hello **클라이언트 ID** 및 **클라이언트 암호** hello Azure 포털에서에서 매개 변수를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-168">hello values for hello **Client ID** and **Client secret** parameters can be found in hello Azure portal.</span></span> <span data-ttu-id="d165d-169">자세한 내용은 참조 [Azure 포털 hello 사용 하 여 Azure AD 인증 시작](media-services-portal-get-started-with-aad.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-169">For more information, see [Getting started with Azure AD authentication using hello Azure portal](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="d165d-170">hello 다음 코드 예제에서는 토큰을 사용 하 여 만듭니다 hello **AzureAdTokenCredentials** 사용 하는 생성자 **AzureAdClientSymmetricKey** 매개 변수로:</span><span class="sxs-lookup"><span data-stu-id="d165d-170">hello following code example creates a token by using hello **AzureAdTokenCredentials** constructor that takes **AzureAdClientSymmetricKey** as a parameter:</span></span> 
    
    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                AzureEnvironments.AzureCloudEnvironment);

    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

<span data-ttu-id="d165d-171">Hello를 지정할 수도 있습니다 **AzureAdTokenCredentials** 사용 하는 생성자 **AzureAdClientCertificate** 매개 변수로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-171">You can also specify hello **AzureAdTokenCredentials** constructor that takes **AzureAdClientCertificate** as a parameter.</span></span> 

<span data-ttu-id="d165d-172">방법에 대 한 지침은 toocreate 참조, Azure AD에서 사용할 수 있는 형태로 인증서를 구성 하 고 [tooAzure AD 인증서-수동 구성 단계를 사용 하 여 디먼 앱에 인증](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-172">For instructions about how toocreate and configure a certificate in a form that can be used by Azure AD, see [Authenticating tooAzure AD in daemon apps with certificates - manual configuration steps](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).</span></span>

    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientCertificate("{YOUR CLIENT ID HERE}", "{YOUR CLIENT CERTIFICATE THUMBPRINT}"), 
                                AzureEnvironments.AzureCloudEnvironment);

<span data-ttu-id="d165d-173">toostart 미디어 서비스를 대상으로 프로그래밍 해야 toocreate는 **CloudMediaContext** hello 서버 컨텍스트를 나타내는 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-173">toostart programming against Media Services, you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="d165d-174">또한 toopass hello 해야 **리소스 미디어 REST 서비스에 대 한 URI** toohello **CloudMediaContext** 생성자입니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-174">You also need toopass hello **resource URI for Media REST Services** toohello **CloudMediaContext** constructor.</span></span> <span data-ttu-id="d165d-175">Hello를 얻을 수 **리소스 미디어 REST 서비스에 대 한 URI** hello도 Azure 포털의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-175">You can get hello **resource URI for Media REST Services** value from hello Azure portal as well.</span></span>

<span data-ttu-id="d165d-176">hello 다음 코드 예제에서는 한 **CloudMediaContext** 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="d165d-176">hello following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
<span data-ttu-id="d165d-177">다음 예제는 hello toocreate Azure AD 토큰 및 hello 컨텍스트가 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-177">hello following example shows how toocreate hello Azure AD token and hello context:</span></span>

    namespace AADAuthSample
    {
    
        class Program
        {
            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                            new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                            AzureEnvironments.AzureCloudEnvironment);
            
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".      
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
    
                Console.ReadLine();
            }
    
        }
    }

## <a name="next-steps"></a><span data-ttu-id="d165d-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d165d-178">Next steps</span></span>

<span data-ttu-id="d165d-179">시작 [tooyour 계정에 파일 업로드](media-services-dotnet-upload-files.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d165d-179">Get started with [uploading files tooyour account](media-services-dotnet-upload-files.md).</span></span>
