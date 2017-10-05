---
title: "Azure Active Directory 인증으로 Azure Media Services API 액세스 | Microsoft Docs"
description: "Azure Media Services API에 대한 액세스를 인증하는 데 Azure AD(Azure Active Directory)를 사용하기 위해 수행할 단계와 개념에 대해 알아봅니다."
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
ms.openlocfilehash: 0e1217afb0a37353793c64ae927b741d9fee4954
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="access-the-azure-media-services-api-with-azure-ad-authentication"></a><span data-ttu-id="1a5fe-103">Azure AD 인증을 사용하여 Azure Media Services API 액세스</span><span class="sxs-lookup"><span data-stu-id="1a5fe-103">Access the Azure Media Services API with Azure AD authentication</span></span>
 
<span data-ttu-id="1a5fe-104">Azure Media Services API는 RESTful API입니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-104">The Azure Media Services API is a RESTful API.</span></span> <span data-ttu-id="1a5fe-105">이 API와 REST API 또는 제공되는 클라이언트 SDK를 사용하여 미디어 리소스에 대한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-105">You can use it to perform operations on media resources by using a REST API or by using available client SDKs.</span></span> <span data-ttu-id="1a5fe-106">Azure Media Services는 Microsoft .NET용 Media Services 클라이언트 SDK를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-106">Azure Media Services offers a Media Services client SDK for Microsoft .NET.</span></span> <span data-ttu-id="1a5fe-107">Media Services 리소스 및 Media Services API에 액세스할 수 있는 권한을 부여하려면 먼저 인증을 거쳐야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-107">To be authorized to access Media Services resources and the Media Services API, you must first be authenticated.</span></span> 

<span data-ttu-id="1a5fe-108">Media Services는 [Azure AD(Azure Active Directory) 기반 인증](../active-directory/active-directory-whatis.md)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-108">Media Services supports [Azure Active Directory (Azure AD)-based authentication](../active-directory/active-directory-whatis.md).</span></span> <span data-ttu-id="1a5fe-109">Azure Media REST 서비스의 경우 REST API 요청을 하는 사용자 또는 응용 프로그램이 리소스에 액세스하기 위해 **참가자** 또는 **소유자** 역할을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-109">The Azure Media REST service requires that the user or application that makes the REST API requests have either the **Contributor** or **Owner** role to access the resources.</span></span> <span data-ttu-id="1a5fe-110">자세한 내용은 [Azure Portal에서 역할 기반 액세스 제어 시작](../active-directory/role-based-access-control-what-is.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-110">For more information, see [Get started with Role-Based Access Control in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="1a5fe-111">현재 Media Services는 Azure Access Control 서비스 인증 모델을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-111">Currently, Media Services supports the Azure Access Control service authentication model.</span></span> <span data-ttu-id="1a5fe-112">그러나 Access Control 권한 부여는 2018년 6월 1일부로 더 이상 사용되지 않을 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-112">However, Access Control authorization will be deprecated on June 1, 2018.</span></span> <span data-ttu-id="1a5fe-113">가능한 빨리 Azure AD 인증 모델로 마이그레이션하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-113">We recommend that you migrate to the Azure AD authentication model as soon as possible.</span></span>

<span data-ttu-id="1a5fe-114">이 문서에서는 REST 또는 .NET API를 사용하여 Media Services API에 액세스하는 방법에 대한 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-114">This document gives an overview of how to access the Media Services API by using REST or .NET APIs.</span></span>

## <a name="access-control"></a><span data-ttu-id="1a5fe-115">Access Control</span><span class="sxs-lookup"><span data-stu-id="1a5fe-115">Access control</span></span>

<span data-ttu-id="1a5fe-116">Azure Media REST 요청이 성공하기 위해서는 호출하는 사용자에게 액세스를 시도하는 Media Services 계정에 대한 참가자 또는 소유자 역할이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-116">For the Azure Media REST request to succeed, the calling user must have a Contributor or Owner role for the Media Services account it is trying to access.</span></span>  
<span data-ttu-id="1a5fe-117">소유자 역할이 있는 사용자만 새 사용자 또는 앱에 미디어 리소스(계정) 액세스 권한을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-117">Only a user with the Owner role can give media resource (account) access to new users or apps.</span></span> <span data-ttu-id="1a5fe-118">참가자 역할은 미디어 리소스만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-118">The Contributor role can access only the media resource.</span></span>
<span data-ttu-id="1a5fe-119">권한이 없는 요청은 상태 코드 401로 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-119">Unauthorized requests fail, with status code of 401.</span></span> <span data-ttu-id="1a5fe-120">이 오류 코드가 표시되면 사용자에게 사용자의 Media Services 계정에 대한 참가자 또는 소유자 역할이 할당되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-120">If you see this error code, check whether your user has the Contributor or Owner role assigned for the user's Media Services account.</span></span> <span data-ttu-id="1a5fe-121">Azure Portal에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-121">You can check this in the Azure portal.</span></span> <span data-ttu-id="1a5fe-122">미디어 계정을 검색한 후 **액세스 제어** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-122">Search for your media account, and then click the **Access control** tab.</span></span> 

![액세스 제어 탭](./media/media-services-use-aad-auth-to-access-ams-api/media-services-access-control.png)

## <a name="types-of-authentication"></a><span data-ttu-id="1a5fe-124">인증 형식</span><span class="sxs-lookup"><span data-stu-id="1a5fe-124">Types of authentication</span></span> 
 
<span data-ttu-id="1a5fe-125">Azure Media Services와 함께 Azure AD 인증을 사용할 때 두 가지 인증 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-125">When you use Azure AD authentication with Azure Media Services, you have two authentication options:</span></span>

- <span data-ttu-id="1a5fe-126">**사용자 인증**.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-126">**User authentication**.</span></span> <span data-ttu-id="1a5fe-127">Media Services 리소스와 상호 작용하는 데 앱을 사용하는 사용자를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-127">Authenticate a person who is using the app to interact with Media Services resources.</span></span> <span data-ttu-id="1a5fe-128">대화형 응용 프로그램은 먼저 사용자에게 사용자의 자격 증명을 묻는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-128">The interactive application should first prompt the user for the user's credentials.</span></span> <span data-ttu-id="1a5fe-129">예제는 권한 있는 사용자가 인코딩 작업 또는 라이브 스트리밍을 모니터링하기 위해 사용한 관리 콘솔 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-129">An example is a management console app used by authorized users to monitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="1a5fe-130">**서비스 주체 인증**.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-130">**Service principal authentication**.</span></span> <span data-ttu-id="1a5fe-131">서비스를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-131">Authenticate a service.</span></span> <span data-ttu-id="1a5fe-132">이 인증 방법을 일반적으로 사용하는 응용 프로그램은 디먼 서비스, 중간 계층 서비스 또는 예약된 작업을 실행하는 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-132">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs.</span></span> <span data-ttu-id="1a5fe-133">예로는 웹앱, 함수 앱, 논리 앱, API 및 마이크로 서비스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-133">Examples are web apps, function apps, logic apps, API, and microservices.</span></span>

### <a name="user-authentication"></a><span data-ttu-id="1a5fe-134">사용자 인증</span><span class="sxs-lookup"><span data-stu-id="1a5fe-134">User authentication</span></span> 

<span data-ttu-id="1a5fe-135">사용자 인증 방법을 사용해야 하는 응용 프로그램은 관리 또는 모니터링 원시 앱(모바일 앱, Windows 앱 및 콘솔 응용 프로그램)입니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-135">Applications that should use the user authentication method are management or monitoring native apps: mobile apps, Windows apps, and Console applications.</span></span> <span data-ttu-id="1a5fe-136">이러한 유형의 솔루션은 다음 시나리오 중 하나에서 서비스에 대해 사용자 개입하려는 경우 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-136">This type of solution is useful when you want human interaction with the service in one of the following scenarios:</span></span>

- <span data-ttu-id="1a5fe-137">인코딩 작업에 대한 대시보드 모니터링.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-137">Monitoring dashboard for your encoding jobs.</span></span>
- <span data-ttu-id="1a5fe-138">라이브 스트림에 대한 대시보드 모니터링.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-138">Monitoring dashboard for your live streams.</span></span>
- <span data-ttu-id="1a5fe-139">데스크톱 또는 모바일 사용자가 Media Services 계정에서 리소스를 관리할 수 있는 관리 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-139">Management application for desktop or mobile users to administer resources in a Media Services account.</span></span>

> [!NOTE]
> <span data-ttu-id="1a5fe-140">이 인증 방법은 소비자 지향 응용 프로그램에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-140">This authentication method should not be used for consumer-facing applications.</span></span> 

<span data-ttu-id="1a5fe-141">먼저, 원시 응용 프로그램은 Azure AD에서 액세스 토큰을 획득한 후 Media Services REST API에 대해 HTTP 요청을 수행할 때 이 토큰을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-141">A native application must first acquire an access token from Azure AD, and then use it when you make HTTP requests to the Media Services REST API.</span></span> <span data-ttu-id="1a5fe-142">액세스 토큰을 요청의 요청 헤더에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-142">Add the access token to the request header.</span></span> 

<span data-ttu-id="1a5fe-143">다음 다이어그램은 일반적인 대화형 응용 프로그램 인증 흐름을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-143">The following diagram shows a typical interactive application authentication flow:</span></span> 

![원시 앱 다이어그램](./media/media-services-use-aad-auth-to-access-ams-api/media-services-native-aad-app1.png)

<span data-ttu-id="1a5fe-145">이전 다이어그램에서 숫자는 요청 흐름을 시간 순서로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-145">In the preceding diagram, the numbers represent the flow of the requests in chronological order.</span></span>

> [!NOTE]
> <span data-ttu-id="1a5fe-146">사용자 인증 방법을 사용하는 경우 모든 앱에서 동일한 (기본) 원시 응용 프로그램 클라이언트 ID 및 원시 응용 프로그램 리디렉션 URI를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-146">When you use the user authentication method, all apps share the same (default) native application client ID and native application redirect URI.</span></span> 

1. <span data-ttu-id="1a5fe-147">사용자에게 자격 증명을 묻는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-147">Prompt a user for credentials.</span></span>
2. <span data-ttu-id="1a5fe-148">다음 매개 변수로 Azure AD 액세스 토큰을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-148">Request an Azure AD access token with the following parameters:</span></span>  

    * <span data-ttu-id="1a5fe-149">Azure AD 테넌트 끝점.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-149">Azure AD tenant endpoint.</span></span>

        <span data-ttu-id="1a5fe-150">Azure Portal에서 테넌트 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-150">The tenant information can be retrieved from the Azure portal.</span></span> <span data-ttu-id="1a5fe-151">오른쪽 위 모서리에서 로그인한 사용자의 이름 위로 커서를 둡니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-151">Place your cursor over the name of the signed-in user in the top right corner.</span></span>
    * <span data-ttu-id="1a5fe-152">Media Services 리소스 URI.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-152">Media Services resource URI.</span></span> 

        <span data-ttu-id="1a5fe-153">이 URI는 동일한 Azure 환경(예: https://rest.media.azure.net )에 있는 Media Services 계정에 대해서는 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-153">This URI is the same for Media Services accounts that are in the same Azure environment (for example, https://rest.media.azure.net).</span></span>

    * <span data-ttu-id="1a5fe-154">Media Services(원시) 응용 프로그램 클라이언트 ID.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-154">Media Services (native) application client ID.</span></span>
    * <span data-ttu-id="1a5fe-155">Media Services(원시) 응용 프로그램 리디렉션 URI.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-155">Media Services (native) application redirect URI.</span></span>
    * <span data-ttu-id="1a5fe-156">REST Media Services의 리소스 URI.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-156">Resource URI for REST Media Services.</span></span>
        
        <span data-ttu-id="1a5fe-157">이 URI는 REST API 끝점(예: https://test03.restv2.westus.media.azure.net/api/)을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-157">The URI represents the REST API endpoint (for example, https://test03.restv2.westus.media.azure.net/api/).</span></span>

    <span data-ttu-id="1a5fe-158">이러한 매개 변수 값을 가져오려면 사용자 인증 옵션과 [Azure Portal을 사용하여 Azure AD 인증 설정 액세스](media-services-portal-get-started-with-aad.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-158">To get values for these parameters, see [Use the Azure portal to access Azure AD authentication settings](media-services-portal-get-started-with-aad.md) using the user authentication option.</span></span>

3. <span data-ttu-id="1a5fe-159">Azure AD 액세스 토큰이 클라이언트로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-159">The Azure AD access token is sent to the client.</span></span>
4. <span data-ttu-id="1a5fe-160">클라이언트는 Azure AD 액세스 토큰과 함께 Azure Media REST API로 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-160">The client sends a request to the Azure Media REST API with the Azure AD access token.</span></span>
5. <span data-ttu-id="1a5fe-161">클라이언트는 Media Services에서 데이터를 다시 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-161">The client gets back the data from Media Services.</span></span>

<span data-ttu-id="1a5fe-162">Media Services .NET 클라이언트 SDK를 사용하여 REST 요청과 통신하기 위해 Azure AD 인증을 사용하는 방법에 대한 자세한 내용은 [Azure AD 인증을 사용하여 .NET으로 Media Services API 액세스](media-services-dotnet-get-started-with-aad.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-162">For information about how to use Azure AD authentication to communicate with REST requests by using the Media Services .NET client SDK, see [Use Azure AD authentication to access the Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span> 

<span data-ttu-id="1a5fe-163">Media Services .NET 클라이언트 SDK를 사용하지 않는 경우 2단계에서 설명한 매개 변수를 사용하여 Azure AD 액세스 토큰 요청을 수동으로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-163">If you are not using the Media Services .NET client SDK, you must manually create an Azure AD access token request by using the parameters described in step 2.</span></span> <span data-ttu-id="1a5fe-164">자세한 내용은 [Azure AD 인증 라이브러리를 사용하여 Azure AD 토큰 가져오기](../active-directory/develop/active-directory-authentication-libraries.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-164">For more information, see [How to use the Azure AD Authentication Library to get the Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

### <a name="service-principal-authentication"></a><span data-ttu-id="1a5fe-165">서비스 주체 인증</span><span class="sxs-lookup"><span data-stu-id="1a5fe-165">Service principal authentication</span></span>

<span data-ttu-id="1a5fe-166">이 인증 방법을 일반적으로 사용하는 응용 프로그램은 중간 계층 서비스 및 예약된 작업(예: 웹앱, 함수 앱, 논리 앱, API 및 마이크로 서비스)을 실행하는 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-166">Applications that commonly use this authentication method are apps that run middle-tier services and scheduled jobs: web apps, function apps, logic apps, APIs, and microservices.</span></span> <span data-ttu-id="1a5fe-167">이 인증 방법은 리소스를 관리하는 데 서비스 계정을 사용하려는 대화형 응용 프로그램에도 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-167">This authentication method also is suitable for interactive applications in which you might want to use a service account to manage resources.</span></span>

<span data-ttu-id="1a5fe-168">소비자 시나리오를 빌드하는 데 서비스 주체 인증 방법을 사용하는 경우 일반적으로 모바일 또는 데스크톱 응용 프로그램에서 직접 처리되지 않고 중간 계층에서 일부 API를 통해 인증이 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-168">When you use the service principal authentication method to build consumer scenarios, authentication typically is handled in the middle tier (through some API) and not directly in a mobile or desktop application.</span></span> 

<span data-ttu-id="1a5fe-169">이 방법을 사용하려면 자체 테넌트에 Azure AD 응용 프로그램 및 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-169">To use this method, create an Azure AD application and service principal in its own tenant.</span></span> <span data-ttu-id="1a5fe-170">응용 프로그램을 만든 후 Media Services 계정에 앱 참가자 또는 소유자 역할 액세스 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-170">After you create the application, give the app Contributor or Owner role access to the Media Services account.</span></span> <span data-ttu-id="1a5fe-171">Azure Portal에서 Azure CLI를 사용하거나 PowerShell 스크립트로 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-171">You can do this in the Azure portal, by using Azure CLI, or with a PowerShell script.</span></span> <span data-ttu-id="1a5fe-172">기존 Azure AD 응용 프로그램을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-172">You also can use an existing Azure AD application.</span></span> <span data-ttu-id="1a5fe-173">[Azure Portal](media-services-portal-get-started-with-aad.md)에서 Azure AD 앱 및 서비스 주체를 등록 및 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-173">You can register and manage your Azure AD app and service principal [in the Azure portal](media-services-portal-get-started-with-aad.md).</span></span> <span data-ttu-id="1a5fe-174">[Azure CLI 2.0](media-services-use-aad-auth-to-access-ams-api.md) 또는 [PowerShell](media-services-powershell-create-and-configure-aad-app.md)을 사용하여 이 작업을 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-174">You also can do this by using [Azure CLI 2.0](media-services-use-aad-auth-to-access-ams-api.md) or [PowerShell](media-services-powershell-create-and-configure-aad-app.md).</span></span> 

![중간 계층 앱](./media/media-services-use-aad-auth-to-access-ams-api/media-services-principal-service-aad-app1.png)

<span data-ttu-id="1a5fe-176">Azure AD 응용 프로그램을 만든 후 다음 설정에 대한 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-176">After you create your Azure AD application, you get values for the following settings.</span></span> <span data-ttu-id="1a5fe-177">인증을 위해서는 다음 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-177">You need these values for authentication:</span></span>

- <span data-ttu-id="1a5fe-178">클라이언트 ID</span><span class="sxs-lookup"><span data-stu-id="1a5fe-178">Client ID</span></span> 
- <span data-ttu-id="1a5fe-179">클라이언트 암호</span><span class="sxs-lookup"><span data-stu-id="1a5fe-179">Client secret</span></span> 

<span data-ttu-id="1a5fe-180">이전 그림에서 숫자는 요청 흐름을 시간 순서로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-180">In the preceding figure, the numbers represent the flow of the requests in chronological order:</span></span>
    
1. <span data-ttu-id="1a5fe-181">중간 계층 앱(웹 API 또는 웹 응용 프로그램)은 다음 매개 변수가 있는 Azure AD 액세스 토큰을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-181">A middle-tier app (web API or web application) requests an Azure AD access token that has the following parameters:</span></span>  

    * <span data-ttu-id="1a5fe-182">Azure AD 테넌트 끝점.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-182">Azure AD tenant endpoint.</span></span>

        <span data-ttu-id="1a5fe-183">Azure Portal에서 테넌트 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-183">The tenant information can be retrieved from the Azure portal.</span></span> <span data-ttu-id="1a5fe-184">오른쪽 위 모서리에서 로그인한 사용자의 이름 위로 커서를 둡니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-184">Place your cursor over the name of the signed-in user in the top right corner.</span></span>
    * <span data-ttu-id="1a5fe-185">Media Services 리소스 URI.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-185">Media Services resource URI.</span></span> 

        <span data-ttu-id="1a5fe-186">이 URI는 동일한 Azure 환경(예: https://rest.media.azure.net )에 있는 Media Services 계정에 대해서는 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-186">This URI is the same for Media Services accounts that are located in the same Azure environment (for example, https://rest.media.azure.net).</span></span>

    * <span data-ttu-id="1a5fe-187">REST Media Services의 리소스 URI.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-187">Resource URI for REST Media Services.</span></span>

        <span data-ttu-id="1a5fe-188">이 URI는 REST API 끝점(예: https://test03.restv2.westus.media.azure.net/api/)을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-188">The URI represents the REST API endpoint (for example, https://test03.restv2.westus.media.azure.net/api/).</span></span>

    * <span data-ttu-id="1a5fe-189">Azure AD 응용 프로그램 값: 클라이언트 ID 및 클라이언트 암호.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-189">Azure AD application values: the client ID and client secret.</span></span>
    
    <span data-ttu-id="1a5fe-190">이러한 매개 변수 값을 가져오려면 서비스 주체 인증 옵션과 [Azure Portal을 사용하여 Azure AD 인증 설정 액세스](media-services-portal-get-started-with-aad.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-190">To get values for these parameters, see [Use the Azure portal to access Azure AD authentication settings](media-services-portal-get-started-with-aad.md) by using the service principal authentication option.</span></span>

2. <span data-ttu-id="1a5fe-191">Azure AD 액세스 토큰이 중간 계층으로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-191">The Azure AD access token is sent to the middle tier.</span></span>
4. <span data-ttu-id="1a5fe-192">중간 계층은 Azure AD 토큰과 함께 Azure Media REST API로 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-192">The middle tier sends request to the Azure Media REST API with the Azure AD token.</span></span>
5. <span data-ttu-id="1a5fe-193">중간 계층은 Media Services에서 데이터를 다시 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-193">The middle tier gets back the data from Media Services.</span></span>

<span data-ttu-id="1a5fe-194">Media Services .NET 클라이언트 SDK를 사용하여 REST 요청과 통신하기 위해 Azure AD 인증을 사용하는 방법에 대한 자세한 내용은 [Azure AD 인증을 사용하여 .NET으로 Azure Media Services API 액세스](media-services-dotnet-get-started-with-aad.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-194">For more information about how to use Azure AD authentication to communicate with REST requests by using the Media Services .NET client SDK, see [Use Azure AD authentication to access Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span> 

<span data-ttu-id="1a5fe-195">Media Services .NET 클라이언트 SDK를 사용하지 않는 경우 1단계에서 설명한 매개 변수를 사용하여 Azure AD 토큰 요청을 수동으로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-195">If you are not using the Media Services .NET client SDK, you must manually create an Azure AD token request by using parameters described in step 1.</span></span> <span data-ttu-id="1a5fe-196">자세한 내용은 [Azure AD 인증 라이브러리를 사용하여 Azure AD 토큰 가져오기](../active-directory/develop/active-directory-authentication-libraries.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-196">For more information, see [How to use the Azure AD Authentication Library to get the Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="1a5fe-197">문제 해결</span><span class="sxs-lookup"><span data-stu-id="1a5fe-197">Troubleshooting</span></span>

<span data-ttu-id="1a5fe-198">예외: “원격 서버에서 (401) 권한 없음 오류를 반환했습니다.”</span><span class="sxs-lookup"><span data-stu-id="1a5fe-198">Exception: "The remote server returned an error: (401) Unauthorized."</span></span>

<span data-ttu-id="1a5fe-199">해결 방법: Media Services REST 요청이 성공하기 위해서는 호출하는 사용자에게 액세스를 시도하는 Media Services 계정에 대한 참가자 또는 소유자 역할이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-199">Solution: For the Media Services REST request to succeed, the calling user must be a Contributor or Owner role in the Media Services account it is trying to access.</span></span> <span data-ttu-id="1a5fe-200">자세한 내용은 [액세스 제어](media-services-use-aad-auth-to-access-ams-api.md#access-control) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-200">For more information, see the [Access control](media-services-use-aad-auth-to-access-ams-api.md#access-control) section.</span></span>

## <a name="resources"></a><span data-ttu-id="1a5fe-201">리소스</span><span class="sxs-lookup"><span data-stu-id="1a5fe-201">Resources</span></span>

<span data-ttu-id="1a5fe-202">다음 문서는 Azure AD 인증 개념을 간략히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-202">The following articles are overviews of Azure AD authentication concepts:</span></span> 

- [<span data-ttu-id="1a5fe-203">Azure AD로 해결된 인증 시나리오</span><span class="sxs-lookup"><span data-stu-id="1a5fe-203">Authentication scenarios addressed by Azure AD</span></span>](../active-directory/develop/active-directory-authentication-scenarios.md#basics-of-authentication-in-azure-ad)
- [<span data-ttu-id="1a5fe-204">Azure AD에서 응용 프로그램 추가, 업데이트 또는 제거</span><span class="sxs-lookup"><span data-stu-id="1a5fe-204">Add, update, or remove an application in Azure AD</span></span>](../active-directory/develop/active-directory-integrating-applications.md)
- [<span data-ttu-id="1a5fe-205">PowerShell을 사용하여 역할 기반 액세스 제어 구성 및 관리</span><span class="sxs-lookup"><span data-stu-id="1a5fe-205">Configure and manage Role-Based Access Control by using PowerShell</span></span>](../active-directory/role-based-access-control-manage-access-powershell.md)

## <a name="next-steps"></a><span data-ttu-id="1a5fe-206">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1a5fe-206">Next steps</span></span>

* <span data-ttu-id="1a5fe-207">Azure Portal을 사용하여 [Azure AD 인증에 액세스하고 Azure Media Services API를 사용](media-services-portal-get-started-with-aad.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-207">Use the Azure portal to [access Azure AD authentication to consume Azure Media Services API](media-services-portal-get-started-with-aad.md).</span></span>
* <span data-ttu-id="1a5fe-208">Azure AD 인증을 사용하여 [.NET으로 Azure Media Services API에 액세스](media-services-dotnet-get-started-with-aad.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a5fe-208">Use Azure AD authentication to [access Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

