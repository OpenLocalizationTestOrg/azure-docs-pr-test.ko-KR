---
title: "Azure Active Directory 인증으로 Azure 미디어 서비스 API aaaAccess | Microsoft Docs"
description: "개념 및 단계 tootake toouse Azure Active Directory (Azure AD) tooauthenticate 액세스 toohello Azure 미디어 서비스 API에 알아봅니다."
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
ms.openlocfilehash: bb8f75f39100dc37098260c24ab4a199ef689d46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="access-hello-azure-media-services-api-with-azure-ad-authentication"></a><span data-ttu-id="718a7-103">Azure AD 인증 hello Azure 미디어 서비스 API에 액세스</span><span class="sxs-lookup"><span data-stu-id="718a7-103">Access hello Azure Media Services API with Azure AD authentication</span></span>
 
<span data-ttu-id="718a7-104">hello Azure 미디어 서비스 API는 RESTful API입니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-104">hello Azure Media Services API is a RESTful API.</span></span> <span data-ttu-id="718a7-105">REST API를 사용 하 여 또는 사용 가능한 클라이언트 Sdk를 사용 하 여 미디어 리소스에 대 한 tooperform 작업 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-105">You can use it tooperform operations on media resources by using a REST API or by using available client SDKs.</span></span> <span data-ttu-id="718a7-106">Azure Media Services는 Microsoft .NET용 Media Services 클라이언트 SDK를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-106">Azure Media Services offers a Media Services client SDK for Microsoft .NET.</span></span> <span data-ttu-id="718a7-107">toobe tooaccess 미디어 서비스 리소스와 hello 미디어 서비스 API 권한을 부여, 사용자 먼저를 인증 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-107">toobe authorized tooaccess Media Services resources and hello Media Services API, you must first be authenticated.</span></span> 

<span data-ttu-id="718a7-108">Media Services는 [Azure AD(Azure Active Directory) 기반 인증](../active-directory/active-directory-whatis.md)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-108">Media Services supports [Azure Active Directory (Azure AD)-based authentication](../active-directory/active-directory-whatis.md).</span></span> <span data-ttu-id="718a7-109">hello Azure 미디어 REST 서비스를 사용 하려면 hello 사용자나 응용 프로그램에서는 hello REST API 요청에 있어야 하거나 hello **참가자** 또는 **소유자** 역할 tooaccess hello 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-109">hello Azure Media REST service requires that hello user or application that makes hello REST API requests have either hello **Contributor** or **Owner** role tooaccess hello resources.</span></span> <span data-ttu-id="718a7-110">자세한 내용은 참조 [hello Azure 포털에서에서 역할 기반 액세스 제어를 시작 하려면](../active-directory/role-based-access-control-what-is.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-110">For more information, see [Get started with Role-Based Access Control in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="718a7-111">현재 미디어 서비스는 hello Azure 액세스 제어 서비스 인증 모델을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-111">Currently, Media Services supports hello Azure Access Control service authentication model.</span></span> <span data-ttu-id="718a7-112">그러나 Access Control 권한 부여는 2018년 6월 1일부로 더 이상 사용되지 않을 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-112">However, Access Control authorization will be deprecated on June 1, 2018.</span></span> <span data-ttu-id="718a7-113">Toohello Azure AD 인증 모델을 최대한 빨리 마이그레이션하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-113">We recommend that you migrate toohello Azure AD authentication model as soon as possible.</span></span>

<span data-ttu-id="718a7-114">이 문서에서는 tooaccess REST 또는.NET Api를 사용 하 여 미디어 서비스 API를 hello 하는 방법의 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-114">This document gives an overview of how tooaccess hello Media Services API by using REST or .NET APIs.</span></span>

## <a name="access-control"></a><span data-ttu-id="718a7-115">Access Control</span><span class="sxs-lookup"><span data-stu-id="718a7-115">Access control</span></span>

<span data-ttu-id="718a7-116">Hello Azure 미디어 REST 요청 toosucceed hello 호출 하는 사용자 hello tooaccess 시도 하는 미디어 서비스 계정에 대 한 소유자 또는 참가자 역할이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-116">For hello Azure Media REST request toosucceed, hello calling user must have a Contributor or Owner role for hello Media Services account it is trying tooaccess.</span></span>  
<span data-ttu-id="718a7-117">미디어 리소스 (계정) 액세스 toonew 사용자 또는 앱 hello 소유자 역할을 가진 사용자만 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-117">Only a user with hello Owner role can give media resource (account) access toonew users or apps.</span></span> <span data-ttu-id="718a7-118">hello 참가자 역할 hello 미디어 리소스에만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-118">hello Contributor role can access only hello media resource.</span></span>
<span data-ttu-id="718a7-119">권한이 없는 요청은 상태 코드 401로 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-119">Unauthorized requests fail, with status code of 401.</span></span> <span data-ttu-id="718a7-120">이 오류 코드가 표시 되 면 hello 참가자 또는 소유자 역할 hello 사용자 미디어 서비스 계정에 대 한 할당 하면 사용자가 있는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-120">If you see this error code, check whether your user has hello Contributor or Owner role assigned for hello user's Media Services account.</span></span> <span data-ttu-id="718a7-121">Hello Azure 포털에서에서이 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-121">You can check this in hello Azure portal.</span></span> <span data-ttu-id="718a7-122">미디어 계정에 검색 하 고 hello를 클릭 한 다음 **액세스 제어** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-122">Search for your media account, and then click hello **Access control** tab.</span></span> 

![액세스 제어 탭](./media/media-services-use-aad-auth-to-access-ams-api/media-services-access-control.png)

## <a name="types-of-authentication"></a><span data-ttu-id="718a7-124">인증 형식</span><span class="sxs-lookup"><span data-stu-id="718a7-124">Types of authentication</span></span> 
 
<span data-ttu-id="718a7-125">Azure Media Services와 함께 Azure AD 인증을 사용할 때 두 가지 인증 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-125">When you use Azure AD authentication with Azure Media Services, you have two authentication options:</span></span>

- <span data-ttu-id="718a7-126">**사용자 인증**.</span><span class="sxs-lookup"><span data-stu-id="718a7-126">**User authentication**.</span></span> <span data-ttu-id="718a7-127">미디어 서비스 리소스와 앱 toointeract hello를 사용 하는 사람을 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-127">Authenticate a person who is using hello app toointeract with Media Services resources.</span></span> <span data-ttu-id="718a7-128">먼저 hello 대화형 응용 프로그램에는 hello 사용자의 자격 증명에 대 한 hello 사용자 라는 메시지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-128">hello interactive application should first prompt hello user for hello user's credentials.</span></span> <span data-ttu-id="718a7-129">권한 있는 사용자 toomonitor 인코딩 작업에서 사용 하 여 관리 콘솔 응용 프로그램은 라이브 스트리밍 또는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-129">An example is a management console app used by authorized users toomonitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="718a7-130">**서비스 주체 인증**.</span><span class="sxs-lookup"><span data-stu-id="718a7-130">**Service principal authentication**.</span></span> <span data-ttu-id="718a7-131">서비스를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-131">Authenticate a service.</span></span> <span data-ttu-id="718a7-132">이 인증 방법을 일반적으로 사용하는 응용 프로그램은 디먼 서비스, 중간 계층 서비스 또는 예약된 작업을 실행하는 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-132">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs.</span></span> <span data-ttu-id="718a7-133">예로는 웹앱, 함수 앱, 논리 앱, API 및 마이크로 서비스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-133">Examples are web apps, function apps, logic apps, API, and microservices.</span></span>

### <a name="user-authentication"></a><span data-ttu-id="718a7-134">사용자 인증</span><span class="sxs-lookup"><span data-stu-id="718a7-134">User authentication</span></span> 

<span data-ttu-id="718a7-135">Hello 사용자 인증 방법을 사용 해야 하는 응용 프로그램은 관리 또는 네이티브 응용 프로그램 모니터링: 모바일 앱, Windows 앱 및 콘솔 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-135">Applications that should use hello user authentication method are management or monitoring native apps: mobile apps, Windows apps, and Console applications.</span></span> <span data-ttu-id="718a7-136">이러한 종류의 솔루션 hello 다음 시나리오 중 하나에 hello 서비스와의 인간 상호 작용 하려는 경우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-136">This type of solution is useful when you want human interaction with hello service in one of hello following scenarios:</span></span>

- <span data-ttu-id="718a7-137">인코딩 작업에 대한 대시보드 모니터링.</span><span class="sxs-lookup"><span data-stu-id="718a7-137">Monitoring dashboard for your encoding jobs.</span></span>
- <span data-ttu-id="718a7-138">라이브 스트림에 대한 대시보드 모니터링.</span><span class="sxs-lookup"><span data-stu-id="718a7-138">Monitoring dashboard for your live streams.</span></span>
- <span data-ttu-id="718a7-139">미디어 서비스 계정에서 데스크톱 또는 모바일 사용자에 게 tooadminister 리소스에 대 한 응용 프로그램을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-139">Management application for desktop or mobile users tooadminister resources in a Media Services account.</span></span>

> [!NOTE]
> <span data-ttu-id="718a7-140">이 인증 방법은 소비자 지향 응용 프로그램에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-140">This authentication method should not be used for consumer-facing applications.</span></span> 

<span data-ttu-id="718a7-141">네이티브 응용 프로그램 먼저 Azure AD에서 액세스 토큰을 획득 하 고 그런 다음 HTTP 요청 toohello 미디어 서비스 REST API를 만들 때 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-141">A native application must first acquire an access token from Azure AD, and then use it when you make HTTP requests toohello Media Services REST API.</span></span> <span data-ttu-id="718a7-142">Hello 액세스 토큰 toohello 요청 헤더를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-142">Add hello access token toohello request header.</span></span> 

<span data-ttu-id="718a7-143">다음 다이어그램 hello 일반적인 대화형 응용 프로그램의 인증 흐름을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-143">hello following diagram shows a typical interactive application authentication flow:</span></span> 

![원시 앱 다이어그램](./media/media-services-use-aad-auth-to-access-ams-api/media-services-native-aad-app1.png)

<span data-ttu-id="718a7-145">Hello 다이어그램 앞, hello 숫자 시간 순서에 따라 hello 요청의 hello 흐름을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-145">In hello preceding diagram, hello numbers represent hello flow of hello requests in chronological order.</span></span>

> [!NOTE]
> <span data-ttu-id="718a7-146">모든 앱 공유 hello hello 사용자 인증 방법을 사용 하면 동일한 (기본값) 네이티브 응용 프로그램 클라이언트 ID 및 네이티브 응용 프로그램 리디렉션 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-146">When you use hello user authentication method, all apps share hello same (default) native application client ID and native application redirect URI.</span></span> 

1. <span data-ttu-id="718a7-147">사용자에게 자격 증명을 묻는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-147">Prompt a user for credentials.</span></span>
2. <span data-ttu-id="718a7-148">매개 변수 뒤 hello로 Azure AD 액세스 토큰을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-148">Request an Azure AD access token with hello following parameters:</span></span>  

    * <span data-ttu-id="718a7-149">Azure AD 테넌트 끝점.</span><span class="sxs-lookup"><span data-stu-id="718a7-149">Azure AD tenant endpoint.</span></span>

        <span data-ttu-id="718a7-150">hello Azure 포털에서에서 hello 테 넌 트 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-150">hello tenant information can be retrieved from hello Azure portal.</span></span> <span data-ttu-id="718a7-151">Hello 오른쪽 위 모서리에 hello 로그인 한 사용자의 hello 이름 위에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-151">Place your cursor over hello name of hello signed-in user in hello top right corner.</span></span>
    * <span data-ttu-id="718a7-152">Media Services 리소스 URI.</span><span class="sxs-lookup"><span data-stu-id="718a7-152">Media Services resource URI.</span></span> 

        <span data-ttu-id="718a7-153">이 URI는 동일 hello에 있는 미디어 서비스 계정에 대 한 hello 동일한 Azure 환경 (예를 들어 https://rest.media.azure.net).</span><span class="sxs-lookup"><span data-stu-id="718a7-153">This URI is hello same for Media Services accounts that are in hello same Azure environment (for example, https://rest.media.azure.net).</span></span>

    * <span data-ttu-id="718a7-154">Media Services(원시) 응용 프로그램 클라이언트 ID.</span><span class="sxs-lookup"><span data-stu-id="718a7-154">Media Services (native) application client ID.</span></span>
    * <span data-ttu-id="718a7-155">Media Services(원시) 응용 프로그램 리디렉션 URI.</span><span class="sxs-lookup"><span data-stu-id="718a7-155">Media Services (native) application redirect URI.</span></span>
    * <span data-ttu-id="718a7-156">REST Media Services의 리소스 URI.</span><span class="sxs-lookup"><span data-stu-id="718a7-156">Resource URI for REST Media Services.</span></span>
        
        <span data-ttu-id="718a7-157">hello URI hello REST API 끝점을 (예를 들어 https://test03.restv2.westus.media.azure.net/api/)을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-157">hello URI represents hello REST API endpoint (for example, https://test03.restv2.westus.media.azure.net/api/).</span></span>

    <span data-ttu-id="718a7-158">이러한 매개 변수에 대해 tooget 값 참조 [hello Azure 포털 tooaccess Azure AD 인증 설정을 사용](media-services-portal-get-started-with-aad.md) hello 사용자 인증 옵션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-158">tooget values for these parameters, see [Use hello Azure portal tooaccess Azure AD authentication settings](media-services-portal-get-started-with-aad.md) using hello user authentication option.</span></span>

3. <span data-ttu-id="718a7-159">hello Azure AD 액세스 토큰은 toohello 클라이언트를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-159">hello Azure AD access token is sent toohello client.</span></span>
4. <span data-ttu-id="718a7-160">hello 클라이언트 hello Azure AD 액세스 토큰으로 요청 toohello Azure 미디어 REST API를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-160">hello client sends a request toohello Azure Media REST API with hello Azure AD access token.</span></span>
5. <span data-ttu-id="718a7-161">클라이언트 hello 가져옵니다 미디어 서비스에서 다시 hello 데이터를.</span><span class="sxs-lookup"><span data-stu-id="718a7-161">hello client gets back hello data from Media Services.</span></span>

<span data-ttu-id="718a7-162">Rest toouse Azure AD 인증 toocommunicate hello 미디어 서비스.NET SDK 클라이언트를 사용 하 여 요청 하는 방식에 대 한 정보를 참조 하십시오. [사용 하 여 Azure AD 인증 tooaccess hello.NET을 사용 하 여 미디어 서비스 API](media-services-dotnet-get-started-with-aad.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-162">For information about how toouse Azure AD authentication toocommunicate with REST requests by using hello Media Services .NET client SDK, see [Use Azure AD authentication tooaccess hello Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span> 

<span data-ttu-id="718a7-163">Hello 미디어 서비스.NET SDK 클라이언트를 사용 하지 않는 경우에 2 단계에서 설명 하는 hello 매개 변수를 사용 하 여 Azure AD 액세스 토큰 요청을 수동으로 만들 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-163">If you are not using hello Media Services .NET client SDK, you must manually create an Azure AD access token request by using hello parameters described in step 2.</span></span> <span data-ttu-id="718a7-164">자세한 내용은 참조 [어떻게 toouse hello Azure AD 인증 라이브러리 tooget hello Azure AD 토큰](../active-directory/develop/active-directory-authentication-libraries.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-164">For more information, see [How toouse hello Azure AD Authentication Library tooget hello Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

### <a name="service-principal-authentication"></a><span data-ttu-id="718a7-165">서비스 주체 인증</span><span class="sxs-lookup"><span data-stu-id="718a7-165">Service principal authentication</span></span>

<span data-ttu-id="718a7-166">이 인증 방법을 일반적으로 사용하는 응용 프로그램은 중간 계층 서비스 및 예약된 작업(예: 웹앱, 함수 앱, 논리 앱, API 및 마이크로 서비스)을 실행하는 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-166">Applications that commonly use this authentication method are apps that run middle-tier services and scheduled jobs: web apps, function apps, logic apps, APIs, and microservices.</span></span> <span data-ttu-id="718a7-167">이 인증 방법은 있는 보겠습니다 toouse 서비스 계정 toomanage 리소스 대화형 응용 프로그램에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-167">This authentication method also is suitable for interactive applications in which you might want toouse a service account toomanage resources.</span></span>

<span data-ttu-id="718a7-168">Hello 서비스 보안 주체 인증 메서드 toobuild 소비자 시나리오를 사용 하는 경우 인증 일반적으로 처리 되 hello (일부 API)를 통해 중간 계층에서 모바일 또는 데스크톱 응용 프로그램에서 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-168">When you use hello service principal authentication method toobuild consumer scenarios, authentication typically is handled in hello middle tier (through some API) and not directly in a mobile or desktop application.</span></span> 

<span data-ttu-id="718a7-169">toouse이이 메서드를 Azure AD 응용 프로그램을 만들고 서비스 보안 주체는 자체 테 넌 트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-169">toouse this method, create an Azure AD application and service principal in its own tenant.</span></span> <span data-ttu-id="718a7-170">Hello 응용 프로그램을 만든 후에 hello 응용 프로그램 소유자 또는 참가자 역할 액세스 toohello 미디어 서비스 계정을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-170">After you create hello application, give hello app Contributor or Owner role access toohello Media Services account.</span></span> <span data-ttu-id="718a7-171">PowerShell 스크립트 또는 Azure CLI를 사용 하 여 hello Azure 포털에서에서이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-171">You can do this in hello Azure portal, by using Azure CLI, or with a PowerShell script.</span></span> <span data-ttu-id="718a7-172">기존 Azure AD 응용 프로그램을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-172">You also can use an existing Azure AD application.</span></span> <span data-ttu-id="718a7-173">등록 하 고 Azure AD 앱 및 서비스 사용자를 관리할 수 있습니다 [hello Azure 포털에서에서](media-services-portal-get-started-with-aad.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-173">You can register and manage your Azure AD app and service principal [in hello Azure portal](media-services-portal-get-started-with-aad.md).</span></span> <span data-ttu-id="718a7-174">[Azure CLI 2.0](media-services-use-aad-auth-to-access-ams-api.md) 또는 [PowerShell](media-services-powershell-create-and-configure-aad-app.md)을 사용하여 이 작업을 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-174">You also can do this by using [Azure CLI 2.0](media-services-use-aad-auth-to-access-ams-api.md) or [PowerShell](media-services-powershell-create-and-configure-aad-app.md).</span></span> 

![중간 계층 앱](./media/media-services-use-aad-auth-to-access-ams-api/media-services-principal-service-aad-app1.png)

<span data-ttu-id="718a7-176">Azure AD 응용 프로그램을 만든 후 다음 설정을 hello에 대 한 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-176">After you create your Azure AD application, you get values for hello following settings.</span></span> <span data-ttu-id="718a7-177">인증을 위해서는 다음 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-177">You need these values for authentication:</span></span>

- <span data-ttu-id="718a7-178">클라이언트 ID</span><span class="sxs-lookup"><span data-stu-id="718a7-178">Client ID</span></span> 
- <span data-ttu-id="718a7-179">클라이언트 암호</span><span class="sxs-lookup"><span data-stu-id="718a7-179">Client secret</span></span> 

<span data-ttu-id="718a7-180">Hello 앞 그림, hello 숫자 hello 요청 시간 순서에 따라 hello 흐름을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-180">In hello preceding figure, hello numbers represent hello flow of hello requests in chronological order:</span></span>
    
1. <span data-ttu-id="718a7-181">Hello 매개 변수 뒤에 있는 Azure AD 액세스 토큰을 요청 하는 중간 계층 응용 프로그램 (웹 API 또는 웹 응용 프로그램):</span><span class="sxs-lookup"><span data-stu-id="718a7-181">A middle-tier app (web API or web application) requests an Azure AD access token that has hello following parameters:</span></span>  

    * <span data-ttu-id="718a7-182">Azure AD 테넌트 끝점.</span><span class="sxs-lookup"><span data-stu-id="718a7-182">Azure AD tenant endpoint.</span></span>

        <span data-ttu-id="718a7-183">hello Azure 포털에서에서 hello 테 넌 트 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-183">hello tenant information can be retrieved from hello Azure portal.</span></span> <span data-ttu-id="718a7-184">Hello 오른쪽 위 모서리에 hello 로그인 한 사용자의 hello 이름 위에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-184">Place your cursor over hello name of hello signed-in user in hello top right corner.</span></span>
    * <span data-ttu-id="718a7-185">Media Services 리소스 URI.</span><span class="sxs-lookup"><span data-stu-id="718a7-185">Media Services resource URI.</span></span> 

        <span data-ttu-id="718a7-186">이 URI는 동일 hello에 있는 미디어 서비스 계정에 대 한 hello 동일한 Azure 환경 (예를 들어 https://rest.media.azure.net).</span><span class="sxs-lookup"><span data-stu-id="718a7-186">This URI is hello same for Media Services accounts that are located in hello same Azure environment (for example, https://rest.media.azure.net).</span></span>

    * <span data-ttu-id="718a7-187">REST Media Services의 리소스 URI.</span><span class="sxs-lookup"><span data-stu-id="718a7-187">Resource URI for REST Media Services.</span></span>

        <span data-ttu-id="718a7-188">hello URI hello REST API 끝점을 (예를 들어 https://test03.restv2.westus.media.azure.net/api/)을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-188">hello URI represents hello REST API endpoint (for example, https://test03.restv2.westus.media.azure.net/api/).</span></span>

    * <span data-ttu-id="718a7-189">Azure AD 응용 프로그램 값: hello 클라이언트 ID와 클라이언트 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-189">Azure AD application values: hello client ID and client secret.</span></span>
    
    <span data-ttu-id="718a7-190">이러한 매개 변수에 대해 tooget 값 참조 [hello Azure 포털 tooaccess Azure AD 인증 설정을 사용 하 여](media-services-portal-get-started-with-aad.md) hello 서비스 보안 주체 인증 옵션을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-190">tooget values for these parameters, see [Use hello Azure portal tooaccess Azure AD authentication settings](media-services-portal-get-started-with-aad.md) by using hello service principal authentication option.</span></span>

2. <span data-ttu-id="718a7-191">hello Azure AD 액세스 토큰은 toohello 중간 계층을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-191">hello Azure AD access token is sent toohello middle tier.</span></span>
4. <span data-ttu-id="718a7-192">hello 중간 계층 hello Azure AD 토큰으로 요청 toohello Azure 미디어 REST API를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-192">hello middle tier sends request toohello Azure Media REST API with hello Azure AD token.</span></span>
5. <span data-ttu-id="718a7-193">hello 중간 계층에서에서 반환 되 hello 데이터 미디어 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-193">hello middle tier gets back hello data from Media Services.</span></span>

<span data-ttu-id="718a7-194">Rest toouse Azure AD 인증 toocommunicate hello 미디어 서비스.NET SDK 클라이언트를 사용 하 여 요청 하는 방식에 대 한 자세한 내용은 참조 [사용 하 여 Azure AD 인증.NET을 사용 하 여 Azure 미디어 서비스 API tooaccess](media-services-dotnet-get-started-with-aad.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-194">For more information about how toouse Azure AD authentication toocommunicate with REST requests by using hello Media Services .NET client SDK, see [Use Azure AD authentication tooaccess Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span> 

<span data-ttu-id="718a7-195">Hello 미디어 서비스.NET SDK 클라이언트를 사용 하지 않는 경우에 1 단계에서 설명 된 매개 변수를 사용 하 여 Azure AD 토큰 요청을 수동으로 만들 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-195">If you are not using hello Media Services .NET client SDK, you must manually create an Azure AD token request by using parameters described in step 1.</span></span> <span data-ttu-id="718a7-196">자세한 내용은 참조 [어떻게 toouse hello Azure AD 인증 라이브러리 tooget hello Azure AD 토큰](../active-directory/develop/active-directory-authentication-libraries.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-196">For more information, see [How toouse hello Azure AD Authentication Library tooget hello Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="718a7-197">문제 해결</span><span class="sxs-lookup"><span data-stu-id="718a7-197">Troubleshooting</span></span>

<span data-ttu-id="718a7-198">예외: "hello 원격 서버에 오류가 반환 되었습니다: (401) 권한이 없음."</span><span class="sxs-lookup"><span data-stu-id="718a7-198">Exception: "hello remote server returned an error: (401) Unauthorized."</span></span>

<span data-ttu-id="718a7-199">해결 방법: hello 미디어 서비스 REST 요청 toosucceed hello 호출 하는 사용자 이어야 합니다 hello tooaccess 시도 하는 미디어 서비스 계정에에서는 소유자 또는 참가자 역할.</span><span class="sxs-lookup"><span data-stu-id="718a7-199">Solution: For hello Media Services REST request toosucceed, hello calling user must be a Contributor or Owner role in hello Media Services account it is trying tooaccess.</span></span> <span data-ttu-id="718a7-200">자세한 내용은 참조 hello [액세스 제어](media-services-use-aad-auth-to-access-ams-api.md#access-control) 섹션.</span><span class="sxs-lookup"><span data-stu-id="718a7-200">For more information, see hello [Access control](media-services-use-aad-auth-to-access-ams-api.md#access-control) section.</span></span>

## <a name="resources"></a><span data-ttu-id="718a7-201">리소스</span><span class="sxs-lookup"><span data-stu-id="718a7-201">Resources</span></span>

<span data-ttu-id="718a7-202">hello 다음 문서는 Azure AD 인증의 개념을 간략하게 설명:</span><span class="sxs-lookup"><span data-stu-id="718a7-202">hello following articles are overviews of Azure AD authentication concepts:</span></span> 

- [<span data-ttu-id="718a7-203">Azure AD로 해결된 인증 시나리오</span><span class="sxs-lookup"><span data-stu-id="718a7-203">Authentication scenarios addressed by Azure AD</span></span>](../active-directory/develop/active-directory-authentication-scenarios.md#basics-of-authentication-in-azure-ad)
- [<span data-ttu-id="718a7-204">Azure AD에서 응용 프로그램 추가, 업데이트 또는 제거</span><span class="sxs-lookup"><span data-stu-id="718a7-204">Add, update, or remove an application in Azure AD</span></span>](../active-directory/develop/active-directory-integrating-applications.md)
- [<span data-ttu-id="718a7-205">PowerShell을 사용하여 역할 기반 액세스 제어 구성 및 관리</span><span class="sxs-lookup"><span data-stu-id="718a7-205">Configure and manage Role-Based Access Control by using PowerShell</span></span>](../active-directory/role-based-access-control-manage-access-powershell.md)

## <a name="next-steps"></a><span data-ttu-id="718a7-206">다음 단계</span><span class="sxs-lookup"><span data-stu-id="718a7-206">Next steps</span></span>

* <span data-ttu-id="718a7-207">너무 hello Azure 포털을 사용 하 여[Azure AD 인증 tooconsume Azure 미디어 서비스 API에 액세스](media-services-portal-get-started-with-aad.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-207">Use hello Azure portal too[access Azure AD authentication tooconsume Azure Media Services API](media-services-portal-get-started-with-aad.md).</span></span>
* <span data-ttu-id="718a7-208">Azure AD 인증도 사용할[.NET을 사용 하 여 Azure 미디어 서비스 API에 액세스](media-services-dotnet-get-started-with-aad.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="718a7-208">Use Azure AD authentication too[access Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

