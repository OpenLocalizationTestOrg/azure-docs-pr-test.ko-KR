---
title: "Active Directory 응용 프로그램 등록 aaaAzure | Microsoft Docs"
description: "이 문서에서 설명 하는 방법을 toouse hello Azure 포털 tooregister Azure Active Directory와 응용 프로그램"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 7dc7b89f-653f-405a-b5f4-2c1288720c15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: priyamo
ms.reviewer: elisol
ms.openlocfilehash: 0134e299dcc53919a6f789a0878a1cf64a8e244d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="register-your-application-with-your-azure-active-directory-tenant"></a><span data-ttu-id="3c85a-103">Azure Active Directory 테넌트로 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="3c85a-103">Register your application with your Azure Active Directory tenant</span></span>

<span data-ttu-id="3c85a-104">Azure Active Directory (Azure AD) 테 넌 트와 Azure 포털 tooregister hello 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-104">You can use hello Azure portal tooregister your application with your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="3c85a-105">Hello 응용 프로그램에 대 한 응용 프로그램 ID 만들고 tooreceive 토큰 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-105">This creates an Application ID for hello application, and enables it tooreceive tokens.</span></span>

1. <span data-ttu-id="3c85a-106">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-106">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3c85a-107">Hello hello 페이지의 맨 위 오른쪽 모서리에서 사용자 계정을 선택 하 여 Azure AD 테 넌 트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-107">Choose your Azure AD tenant by selecting your account in hello top right corner of hello page.</span></span>
3. <span data-ttu-id="3c85a-108">Hello 왼쪽의 탐색 창에서 선택 **더 서비스**, 클릭 **앱 등록**를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-108">In hello left-hand navigation pane, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
4. <span data-ttu-id="3c85a-109">Hello 화면에 따라 수행 하 고 새 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-109">Follow hello prompts and create a new application.</span></span> <span data-ttu-id="3c85a-110">웹 응용 프로그램 또는 네이티브 응용 프로그램에 대한 구체적인 예제를 원하는 경우 [빠른 시작](active-directory-developers-guide.md)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-110">If you'd like specific examples for web applications or native applications, check out our [quickstarts](active-directory-developers-guide.md).</span></span>
  * <span data-ttu-id="3c85a-111">웹 응용 프로그램에서는 hello 제공 **로그온 URL**, hello 응용 프로그램의 기준 URL을 설정 하는 예: 사용자가 로그인이 변수인 `http://localhost:12345`합니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-111">For Web Applications, provide hello **Sign-On URL**, which is hello base URL of your app, where users can sign in e.g `http://localhost:12345`.</span></span>
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * <span data-ttu-id="3c85a-112">네이티브 응용 프로그램에 제공 된 **리디렉션 URI**, tooreturn 토큰 응답을 사용 하 여 Azure AD는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-112">For Native Applications, provide a **Redirect URI**, which Azure AD uses tooreturn token responses.</span></span> <span data-ttu-id="3c85a-113">값 특정 tooyour 응용 프로그램을 입력 합니다. 예:`http://MyFirstAADApp`</span><span class="sxs-lookup"><span data-stu-id="3c85a-113">Enter a value specific tooyour application, .e.g `http://MyFirstAADApp`</span></span>
5. <span data-ttu-id="3c85a-114">Azure AD 할당 hello 응용 프로그램 id입니다. 고유한 클라이언트 식별자, 응용 프로그램 등록을 마친 후</span><span class="sxs-lookup"><span data-stu-id="3c85a-114">Once you've completed registration, Azure AD assigns your application a unique client identifier, hello Application ID.</span></span>

## <a name="update-application-settings-from-hello-azure-portal"></a><span data-ttu-id="3c85a-115">Hello Azure 포털에서에서 응용 프로그램 설정 업데이트</span><span class="sxs-lookup"><span data-stu-id="3c85a-115">Update application settings from hello Azure portal</span></span>

<span data-ttu-id="3c85a-116">Azure 포털 hello를 사용 하 여 기존 응용 프로그램의 설정을 쉽게 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-116">You can easily modify an existing application's settings using hello Azure portal.</span></span> <span data-ttu-id="3c85a-117">예를 들어 좋습니다 tooconfigure Azure AD 토큰 응답을 발급 하는 회신 URL.</span><span class="sxs-lookup"><span data-stu-id="3c85a-117">For example, you may want tooconfigure a reply URL, which is where Azure AD issues token responses.</span></span> <span data-ttu-id="3c85a-118">Tooconfigure 권한 tooother 응용 프로그램을 할 수 있습니다, 인스턴스 tooallow에 대 한 응용 프로그램 tooaccess hello Microsoft Graph API입니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-118">You may also want tooconfigure permissions tooother applications, for instance tooallow your application tooaccess hello Microsoft Graph API.</span></span> <span data-ttu-id="3c85a-119">이 모든 hello 응용 프로그램 설정 페이지를 통해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-119">You can do all this through hello application settings page.</span></span>

1. <span data-ttu-id="3c85a-120">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3c85a-121">Hello hello 페이지의 맨 위 오른쪽 모서리에서 사용자 계정을 선택 하 여 Azure AD 테 넌 트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-121">Choose your Azure AD tenant by selecting your account in hello top right corner of hello page.</span></span>
3. <span data-ttu-id="3c85a-122">Hello 왼쪽의 탐색 창에서 선택 **더 서비스**, 클릭 **앱 등록**, hello 목록에서 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-122">In hello left-hand navigation pane, choose **More Services**, click **App Registrations**, and choose your application from hello list.</span></span>
4. <span data-ttu-id="3c85a-123">클릭 **설정을** tooopen hello 응용 프로그램에 대 한 hello 설정 페이지를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-123">Click **Settings** tooopen up hello settings page for hello application.</span></span>
  * <span data-ttu-id="3c85a-124">hello **속성** 페이지 hello hello 응용 프로그램에 대 한 일반 정보를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-124">hello **Properties** page lets you modify hello general information for hello application.</span></span> <span data-ttu-id="3c85a-125">Hello 응용 프로그램 이름, hello 로그온 URL 및 hello 로그 아웃 URL이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-125">This includes hello application name, hello sign-on URL, and hello logout URL.</span></span>
  * <span data-ttu-id="3c85a-126">hello **회신 Url** 페이지에서는 Azure AD 토큰 응답을 전송 하는 위치는 회신 URL을 tooadd 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-126">hello **Reply URLs** page allows you tooadd a reply URL, which is where Azure AD sends token responses.</span></span>
  * <span data-ttu-id="3c85a-127">hello **소유자** 페이지에서는 tooadd 응용 프로그램 소유자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-127">hello **Owners** page allows you tooadd application owners.</span></span>
  * <span data-ttu-id="3c85a-128">hello **권한을** 페이지에서는 hello 앱에 대 한 권한을 tooconfigure 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-128">hello **Permissions** page allows you tooconfigure permissions for hello app.</span></span> <span data-ttu-id="3c85a-129">예를 들어 tooaccess hello Microsoft Graph API를 클릭 하 여 **추가** 선택 **Microsoft Graph** hello API 선택기에서 hello 권한이 필요한 경우 예를 들어 다음 선택 **디렉터리 데이터 읽기 **.</span><span class="sxs-lookup"><span data-stu-id="3c85a-129">For example, tooaccess hello Microsoft Graph API, click **Add** and select **Microsoft Graph** in hello API selector, then choose hello permission required, for example **Read Directory Data**.</span></span>
  * <span data-ttu-id="3c85a-130">hello **키** 페이지에서는 tooadd 응용 프로그램 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-130">hello **Keys** page allows you tooadd application secrets.</span></span> <span data-ttu-id="3c85a-131">hello 비밀만 표시 한 번를 만든 후 즉시 있는지 toocopy를 수 있으므로 더 이상 사용 하기 위해.</span><span class="sxs-lookup"><span data-stu-id="3c85a-131">hello secret will only be displayed once immediately after creation, so make sure toocopy it for further use.</span></span>

## <a name="use-hello-inline-manifest-editor"></a><span data-ttu-id="3c85a-132">Hello 인라인 매니페스트 편집기를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="3c85a-132">Use hello inline manifest editor</span></span>

<span data-ttu-id="3c85a-133">Hello 인라인 매니페스트 편집기 toomodify 특정 응용 프로그램 속성에 직접 노출 되지 않는 hello Azure 포털을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-133">You can use hello inline manifest editor toomodify certain application properties that are not exposed directly in hello Azure portal.</span></span> <span data-ttu-id="3c85a-134">예를 들어 toomodify hello 응용 프로그램의 앱 ID URI를 사용할 수 있습니다 또는 tooenable hello oauth 2.0 암시적 흐름 대신 hello 기본 권한 부여 코드 흐름을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-134">For example, you can use it toomodify hello application's App ID URI or tooenable hello OAuth2.0 implicit flow instead of hello default authorization grant code flow.</span></span>

1. <span data-ttu-id="3c85a-135">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-135">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3c85a-136">Hello hello 페이지의 맨 위 오른쪽 모서리에서 사용자 계정을 선택 하 여 Azure AD 테 넌 트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-136">Choose your Azure AD tenant by selecting your account in hello top right corner of hello page.</span></span>
3. <span data-ttu-id="3c85a-137">Hello 왼쪽의 탐색 창에서 선택 **더 서비스**, 클릭 **앱 등록**, hello 목록에서 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-137">In hello left-hand navigation pane, choose **More Services**, click **App Registrations**, and choose your application from hello list.</span></span>
4. <span data-ttu-id="3c85a-138">클릭 **매니페스트** hello 응용 프로그램 페이지 tooopen hello 인라인 매니페스트 편집기에서.</span><span class="sxs-lookup"><span data-stu-id="3c85a-138">Click **Manifest** from hello application page tooopen hello inline manifest editor.</span></span>
5. <span data-ttu-id="3c85a-139">변경 내용을 toohello 매니페스트 하 고 싶다면 저장 직접 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-139">You can directly make changes toohello manifest and save it when you're ready.</span></span> <span data-ttu-id="3c85a-140">또는 hello 매니페스트 tooopen를 다운로드할 수 있습니다 프로그램 즐겨 찾는 편집기 및 업로드 hello에서 매니페스트를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-140">Alternatively, you can download hello manifest tooopen it in your favorite editor and upload hello updated manifest.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c85a-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3c85a-141">Next Steps</span></span>

1. <span data-ttu-id="3c85a-142">체크 아웃 hello [퀵 스타트](active-directory-developers-guide.md) Azure AD를 사용 하 여 인증을 수행 하는 응용 프로그램의 자세한 연습에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-142">Check out hello [Quickstarts](active-directory-developers-guide.md) for detailed walkthroughs of applications performing authentication using Azure AD.</span></span>
2. <span data-ttu-id="3c85a-143">[GitHub](https://github.com/azure-samples)에서 코드 샘플에 대한 전체 목록을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3c85a-143">Check out our full list of code samples in [GitHub](https://github.com/azure-samples).</span></span>
