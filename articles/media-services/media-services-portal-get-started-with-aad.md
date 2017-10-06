---
title: "hello Azure 포털을 사용 하 여 Azure AD 인증 시작 aaaGet | Microsoft Docs"
description: "Azure 포털 tooaccess Azure Active Directory (Azure AD) 인증 tooconsume toouse hello Azure 미디어 서비스 API hello 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 497ad1806b3fd1262802adefb6e12b65ee9f2d61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-ad-authentication-by-using-hello-azure-portal"></a><span data-ttu-id="62646-103">Hello Azure 포털을 사용 하 여 Azure AD 인증 시작</span><span class="sxs-lookup"><span data-stu-id="62646-103">Get started with Azure AD authentication by using hello Azure portal</span></span>

<span data-ttu-id="62646-104">어떻게 toouse hello Azure 포털 tooaccess Azure Active Directory (Azure AD) 인증 tooaccess hello Azure 미디어 서비스 API에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="62646-104">Learn how toouse hello Azure portal tooaccess Azure Active Directory (Azure AD) authentication tooaccess hello Azure Media Services API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62646-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="62646-105">Prerequisites</span></span>

- <span data-ttu-id="62646-106">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="62646-106">An Azure account.</span></span> <span data-ttu-id="62646-107">계정이 없는 경우 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="62646-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="62646-108">Media Services 계정.</span><span class="sxs-lookup"><span data-stu-id="62646-108">A Media Services account.</span></span> <span data-ttu-id="62646-109">자세한 내용은 참조 [hello Azure 포털을 사용 하 여 Azure 미디어 서비스 계정을 만들려면](media-services-portal-create-account.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="62646-109">For more information, see [Create an Azure Media Services account by using hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="62646-110">Hello를 검토 해야 [Azure AD 인증 개요를 사용 하 여 Azure 미디어 서비스 API에 액세스](media-services-use-aad-auth-to-access-ams-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="62646-110">Make sure you review hello [Accessing Azure Media Services API with Azure AD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="62646-111">Azure Media Services와 함께 Azure AD 인증을 사용할 때 두 가지 인증 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="62646-111">When you use Azure AD authentication with Azure Media Services, you have two authentication options:</span></span>

- <span data-ttu-id="62646-112">**사용자 인증**.</span><span class="sxs-lookup"><span data-stu-id="62646-112">**User authentication**.</span></span> <span data-ttu-id="62646-113">미디어 서비스 리소스와 앱 toointeract hello를 사용 하는 사람을 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="62646-113">Authenticate a person who is using hello app toointeract with Media Services resources.</span></span> <span data-ttu-id="62646-114">먼저 hello 대화형 응용 프로그램에는 hello 사용자에 게 자격 라는 메시지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62646-114">hello interactive application should first prompt hello user for credentials.</span></span> <span data-ttu-id="62646-115">권한 있는 사용자 toomonitor 인코딩 작업에서 사용 하 여 관리 콘솔 응용 프로그램은 라이브 스트리밍 또는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="62646-115">An example is a management console app used by authorized users toomonitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="62646-116">**서비스 주체 인증**.</span><span class="sxs-lookup"><span data-stu-id="62646-116">**Service principal authentication**.</span></span> <span data-ttu-id="62646-117">서비스를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="62646-117">Authenticate a service.</span></span> <span data-ttu-id="62646-118">이 인증 방법을 일반적으로 사용하는 응용 프로그램은 디먼 서비스, 중간 계층 서비스 또는 예약된 작업(예: 웹앱, 함수 앱, 논리 앱, API 또는 마이크로 서비스)을 실행하는 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="62646-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs: web apps, function apps, logic apps, APIs, or a microservice.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="62646-119">현재 미디어 서비스는 hello Azure 액세스 제어 서비스 인증 모델을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="62646-119">Currently, Media Services supports hello Azure Access Control service authentication model.</span></span> <span data-ttu-id="62646-120">그러나 Access Control 권한 부여는 2018년 6월 1일부로 더 이상 사용되지 않을 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="62646-120">However, Access Control authorization will be deprecated on June 1, 2018.</span></span> <span data-ttu-id="62646-121">Toohello Azure AD 인증 모델을 최대한 빨리 마이그레이션하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="62646-121">We recommend that you migrate toohello Azure AD authentication model as soon as possible.</span></span>

## <a name="select-hello-authentication-method"></a><span data-ttu-id="62646-122">Hello 인증 방법 선택</span><span class="sxs-lookup"><span data-stu-id="62646-122">Select hello authentication method</span></span>

1. <span data-ttu-id="62646-123">Hello에 [Azure 포털](https://portal.azure.com/), 미디어 서비스 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="62646-123">In hello [Azure portal](https://portal.azure.com/), select your Media Services account.</span></span>
2. <span data-ttu-id="62646-124">방법을 선택 tooconnect toohello 미디어 서비스 API입니다.</span><span class="sxs-lookup"><span data-stu-id="62646-124">Select how tooconnect toohello Media Services API.</span></span>

    ![연결 방법 선택 페이지](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started01.png)

## <a name="user-authentication"></a><span data-ttu-id="62646-126">사용자 인증</span><span class="sxs-lookup"><span data-stu-id="62646-126">User authentication</span></span>

<span data-ttu-id="62646-127">tooconnect toohello 미디어 서비스 API를 사용 하 여 hello 사용자 인증 옵션, 클라이언트 응용 프로그램 hello 필요한 toorequest 매개 변수 뒤 hello에 Azure AD 토큰:</span><span class="sxs-lookup"><span data-stu-id="62646-127">tooconnect toohello Media Services API by using hello user authentication option, hello client app needs toorequest an Azure AD token that has hello following parameters:</span></span>  

* <span data-ttu-id="62646-128">Azure AD 테넌트 끝점</span><span class="sxs-lookup"><span data-stu-id="62646-128">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="62646-129">Media Services 리소스 URI</span><span class="sxs-lookup"><span data-stu-id="62646-129">Media Services resource URI</span></span>
* <span data-ttu-id="62646-130">Media Services(원시) 응용 프로그램 클라이언트 ID</span><span class="sxs-lookup"><span data-stu-id="62646-130">Media Services (native) application client ID</span></span> 
* <span data-ttu-id="62646-131">Media Services(원시) 응용 프로그램 리디렉션 URI</span><span class="sxs-lookup"><span data-stu-id="62646-131">Media Services (native) application redirect URI</span></span> 
* <span data-ttu-id="62646-132">REST Media Services의 리소스 URI</span><span class="sxs-lookup"><span data-stu-id="62646-132">Resource URI for REST Media Services</span></span>

<span data-ttu-id="62646-133">Hello에 이러한 매개 변수에 대해 hello 값을 가져올 수 **사용자 인증을 사용 하 여 미디어 서비스 API** 페이지.</span><span class="sxs-lookup"><span data-stu-id="62646-133">You can get hello values for these parameters on hello **Media Services API with user authentication** page.</span></span> 

![사용자 인증으로 연결 페이지](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started02.png)

<span data-ttu-id="62646-135">미디어 서비스 API toohello hello 미디어 서비스 Microsoft.NET SDK를 사용 하 여 연결 하는 경우 hello 값 hello SDK의 일부분으로 사용할 수 있는 tooyou이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="62646-135">If you connect toohello Media Services API by using hello Media Services Microsoft .NET SDK, hello required values are available tooyou as part of hello SDK.</span></span> <span data-ttu-id="62646-136">자세한 내용은 참조 [사용 하 여 Azure AD 인증 tooaccess hello.NET을 사용 하 여 Azure 미디어 서비스 API](media-services-dotnet-get-started-with-aad.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="62646-136">For more information, see [Use Azure AD authentication tooaccess hello Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="62646-137">Hello 미디어 서비스.NET SDK 클라이언트를 사용 하지 않는 경우 앞에서 설명한 hello 매개 변수를 사용 하 여 Azure AD 토큰 요청을 수동으로 만들 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62646-137">If you're not using hello Media Services .NET client SDK, you must manually create an Azure AD token request by using hello parameters discussed earlier.</span></span> <span data-ttu-id="62646-138">자세한 내용은 참조 [어떻게 toouse hello Azure AD 인증 라이브러리 tooget hello Azure AD 토큰](../active-directory/develop/active-directory-authentication-libraries.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="62646-138">For more information, see [How toouse hello Azure AD Authentication Library tooget hello Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

## <a name="service-principal-authentication"></a><span data-ttu-id="62646-139">서비스 주체 인증</span><span class="sxs-lookup"><span data-stu-id="62646-139">Service principal authentication</span></span>

<span data-ttu-id="62646-140">tooconnect toohello 미디어 서비스 API를 사용 하 여 서비스 보안 주체 옵션 hello, 중간 계층 응용 프로그램 (웹 API 또는 웹 응용 프로그램) 필요한 toorequest 매개 변수 뒤 hello에 Azure AD 토큰:</span><span class="sxs-lookup"><span data-stu-id="62646-140">tooconnect toohello Media Services API by using hello service principal option, your middle-tier app (web API or web application) needs toorequest an Azure AD token that has hello following parameters:</span></span>  

* <span data-ttu-id="62646-141">Azure AD 테넌트 끝점</span><span class="sxs-lookup"><span data-stu-id="62646-141">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="62646-142">Media Services 리소스 URI</span><span class="sxs-lookup"><span data-stu-id="62646-142">Media Services resource URI</span></span> 
* <span data-ttu-id="62646-143">REST Media Services의 리소스 URI</span><span class="sxs-lookup"><span data-stu-id="62646-143">Resource URI for REST Media Services</span></span>
* <span data-ttu-id="62646-144">Azure AD 응용 프로그램 값: hello **클라이언트 ID** 및 **클라이언트 암호**</span><span class="sxs-lookup"><span data-stu-id="62646-144">Azure AD application values: hello **client ID** and **client secret**</span></span>

<span data-ttu-id="62646-145">Hello에 이러한 매개 변수에 대해 hello 값을 가져올 수 **tooMedia 서비스 API 서비스 사용자와 연결** 페이지.</span><span class="sxs-lookup"><span data-stu-id="62646-145">You can get hello values for these parameters on hello **Connect tooMedia Services API with service principal** page.</span></span> <span data-ttu-id="62646-146">이 페이지 toocreate 새로운 Azure를 사용 하 여 AD 응용 프로그램 또는 tooselect 기존 합니다.</span><span class="sxs-lookup"><span data-stu-id="62646-146">Use this page toocreate a new Azure AD application or tooselect an existing one.</span></span> <span data-ttu-id="62646-147">Hello Azure AD 앱을 선택한 후 hello 클라이언트 ID (응용 프로그램 ID) 가져오고 hello 클라이언트 암호 (키) 값을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62646-147">After you select hello Azure AD app, you can get hello client ID (Application ID) and generate hello client secret (key) values.</span></span> 

![서비스 주체로 연결 페이지](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started04.png)

<span data-ttu-id="62646-149">Hello 때 **서비스 사용자** hello 첫 번째 Azure AD 응용 프로그램이 hello 다음 조건을 충족 하는 선택, 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="62646-149">When hello **Service Principal** blade opens, hello first Azure AD application that meets hello following criteria is selected:</span></span>

- <span data-ttu-id="62646-150">등록된 Azure AD 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="62646-150">It is a registered Azure AD application.</span></span>
- <span data-ttu-id="62646-151">Hello 계정에 참가자 또는 Owner Role-Based 액세스 제어 권한을 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="62646-151">It has Contributor or Owner Role-Based Access Control permissions on hello account.</span></span>

<span data-ttu-id="62646-152">후에 만들거나 Azure AD 앱 선택 만들고 수 있습니다 및 클라이언트 암호 (키)를 복사할 hello 클라이언트 ID (응용 프로그램 ID)입니다.</span><span class="sxs-lookup"><span data-stu-id="62646-152">After you create or select an Azure AD app, you can create and copy a client secret (key) and hello client ID (Application ID).</span></span> <span data-ttu-id="62646-153">hello 클라이언트 암호 및 클라이언트 ID는이 시나리오에서는 필요한 tooget hello 액세스 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="62646-153">hello client secret and client ID are required tooget hello access token in this scenario.</span></span>

<span data-ttu-id="62646-154">사용 권한을 toocreate Azure AD 앱 도메인 내에서 없다면 hello 블레이드의 hello Azure AD 앱 컨트롤 표시 되지 않습니다 하 고 경고 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62646-154">If you don't have permissions toocreate Azure AD apps in your domain, hello Azure AD app controls of hello blade are not shown, and a warning message is displayed.</span></span>

<span data-ttu-id="62646-155">미디어 서비스 API toohello hello 미디어 서비스.NET SDK를 사용 하 여 연결 하는 경우 참조 [사용 하 여 Azure AD 인증 tooaccess hello.NET을 사용 하 여 Azure 미디어 서비스 API](media-services-dotnet-get-started-with-aad.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="62646-155">If you connect toohello Media Services API by using hello Media Services .NET SDK, see [Use Azure AD authentication tooaccess hello Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="62646-156">Hello 미디어 서비스.NET SDK 클라이언트를 사용 하지 않는 경우 수동으로 앞에서 설명한 hello 매개 변수를 사용 하 여 Azure AD 토큰 요청을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62646-156">If you are not using hello Media Services .NET client SDK, you must manually create an Azure AD token request using hello parameters discussed earlier.</span></span> <span data-ttu-id="62646-157">자세한 내용은 참조 [어떻게 toouse hello Azure AD 인증 라이브러리 tooget hello Azure AD 토큰](../active-directory/develop/active-directory-authentication-libraries.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="62646-157">For more information, see [How toouse hello Azure AD Authentication Library tooget hello Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

### <a name="get-hello-client-id-and-client-secret"></a><span data-ttu-id="62646-158">Hello 클라이언트 ID 및 클라이언트 암호 가져오기</span><span class="sxs-lookup"><span data-stu-id="62646-158">Get hello client ID and client secret</span></span>

<span data-ttu-id="62646-159">기존 Azure AD 응용 프로그램 또는 선택 하면 선택 hello 옵션 toocreate 새 hello 다음 단추가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62646-159">After you select an existing Azure AD app or select hello option toocreate a new one, hello following buttons appear:</span></span>

![[사용 권한 관리] 단추 및 [응용 프로그램 관리] 단추](./media/media-services-portal-get-started-with-aad/media-services-portal-manage.png)

<span data-ttu-id="62646-161">Azure AD 응용 프로그램 블레이드 tooopen hello 클릭 **응용 프로그램 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="62646-161">tooopen hello Azure AD application blade, click **Manage application**.</span></span> <span data-ttu-id="62646-162">Hello에 **응용 프로그램 관리** 블레이드에서 hello 앱의 클라이언트 ID (응용 프로그램 ID)를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62646-162">On hello **Manage application** blade, you can get hello app's client ID (Application ID).</span></span> <span data-ttu-id="62646-163">선택 하면 클라이언트 암호 (키), toogenerate **키**합니다.</span><span class="sxs-lookup"><span data-stu-id="62646-163">toogenerate a client secret (key), select **Keys**.</span></span>

![응용 프로그램 블레이드 키 관리 옵션](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started06.png) 

### <a name="manage-permissions-and-hello-application"></a><span data-ttu-id="62646-165">사용 권한 및 hello 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="62646-165">Manage permissions and hello application</span></span>

<span data-ttu-id="62646-166">Hello Azure AD 응용 프로그램을 선택한 후에 hello 응용 프로그램 및 권한을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62646-166">After you select hello Azure AD application, you can manage hello application and permissions.</span></span> <span data-ttu-id="62646-167">tooset 다른 응용 프로그램을 Azure AD 응용 프로그램 tooaccess 클릭 **사용 권한을 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="62646-167">tooset up your Azure AD application tooaccess other applications, click **Manage permissions**.</span></span> <span data-ttu-id="62646-168">키 및 회신 Url 또는 tooedit hello 응용 프로그램의 매니페스트를 변경 하는 등의 관리 작업을 클릭 **응용 프로그램 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="62646-168">For management tasks, such as changing keys and reply URLs, or tooedit hello application’s manifest, click **Manage application**.</span></span>

### <a name="edit-hello-apps-settings-or-manifest"></a><span data-ttu-id="62646-169">Hello 응용 프로그램의 설정을 편집 하거나 매니페스트</span><span class="sxs-lookup"><span data-stu-id="62646-169">Edit hello app's settings or manifest</span></span>

<span data-ttu-id="62646-170">클릭 하 여 tooedit hello 응용 프로그램의 설정 또는 매니페스트를 **응용 프로그램 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="62646-170">tooedit hello app's settings or manifest, click **Manage application**.</span></span>

![응용 프로그램 관리 페이지](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started05.png)

## <a name="next-steps"></a><span data-ttu-id="62646-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="62646-172">Next steps</span></span>

<span data-ttu-id="62646-173">시작 [tooyour 계정에 파일 업로드](media-services-portal-upload-files.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="62646-173">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>
