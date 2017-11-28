---
title: "응용 프로그램 서비스 응용 프로그램에 대 한 aaaHow tooconfigure Google 인증"
description: "자세한 방법을 응용 프로그램 서비스 응용 프로그램에 대 한 tooconfigure Google 인증 합니다."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: 2b2f9abf-9120-4aac-ac5b-4a268d9b6e2b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 9175c40b78c859e9e191504c41cd0bb9a3380ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-google-login"></a><span data-ttu-id="2b4ae-103">어떻게 tooconfigure 앱 서비스 응용 프로그램 toouse Google 로그인</span><span class="sxs-lookup"><span data-stu-id="2b4ae-103">How tooconfigure your App Service application toouse Google login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="2b4ae-104">이 항목에서는 Azure 앱 서비스 toouse tooconfigure 인증 공급자 인 Google에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-104">This topic shows you how tooconfigure Azure App Service toouse Google as an authentication provider.</span></span>

<span data-ttu-id="2b4ae-105">이 항목의 toocomplete hello 절차, 확인 된 전자 메일 주소를 보유 하는 Google 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-105">toocomplete hello procedure in this topic, you must have a Google account that has a verified email address.</span></span> <span data-ttu-id="2b4ae-106">새 Google 계정 toocreate 너무 이동[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-106">toocreate a new Google account, go too[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>

## <span data-ttu-id="2b4ae-107"><a name="register"> </a>Google을 사용하여 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="2b4ae-107"><a name="register"> </a>Register your application with Google</span></span>
1. <span data-ttu-id="2b4ae-108">Toohello 로그온 [Azure 포털], tooyour 응용 프로그램을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="2b4ae-109">복사 프로그램 **URL**이며 이후 tooconfigure Google 앱을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-109">Copy your **URL**, which you use later tooconfigure your Google app.</span></span>
2. <span data-ttu-id="2b4ae-110">Toohello 이동 [Google api](http://go.microsoft.com/fwlink/p/?LinkId=268303) 사이트 Google 계정 자격 증명을 사용 하 여 로그인을 클릭 **프로젝트 만들기**, 제공 된 **프로젝트 이름**, 클릭  **만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-110">Navigate toohello [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303) website, sign in with your Google account credentials, click **Create Project**, provide a **Project name**, then click **Create**.</span></span>
3. <span data-ttu-id="2b4ae-111">**Social APIs** 아래에서 **Google+ API**, **Enable**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-111">Under **Social APIs** click **Google+ API** and then **Enable**.</span></span>
4. <span data-ttu-id="2b4ae-112">왼쪽 탐색, hello에 **자격 증명** > **OAuth 동의 화면**을 선택한 후 사용자 **전자 메일 주소**를 입력 한 **제품이름**를 클릭 하 고 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-112">In hello left navigation, **Credentials** > **OAuth consent screen**, then select your **Email address**,  enter a **Product Name**, and click **Save**.</span></span>
5. <span data-ttu-id="2b4ae-113">Hello에 **자격 증명** 탭을 클릭 **자격 증명을 만들어** > **OAuth 클라이언트 ID**을 선택한 후 **웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-113">In hello **Credentials** tab, click **Create credentials** > **OAuth client ID**, then select **Web application**.</span></span>
6. <span data-ttu-id="2b4ae-114">붙여넣기 hello 앱 서비스 **URL** 에 앞에서 복사한 있습니다 **자바 스크립트 원본**, 프로그램 리디렉션 붙여 URI에 **권한이 리디렉션 URI**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-114">Paste hello App Service **URL** you copied earlier into **Authorized JavaScript Origins**, then paste your redirect URI into **Authorized Redirect URI**.</span></span> <span data-ttu-id="2b4ae-115">리디렉션 URI는 hello 경로 추가 되므로 응용 프로그램의 hello URL hello */.auth/login/google/callback*합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-115">hello redirect URI is hello URL of your application appended with hello path, */.auth/login/google/callback*.</span></span> <span data-ttu-id="2b4ae-116">예: `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-116">For example, `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span></span> <span data-ttu-id="2b4ae-117">Hello HTTPS 체계를 사용 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-117">Make sure that you are using hello HTTPS scheme.</span></span> <span data-ttu-id="2b4ae-118">그런 다음 **Create**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-118">Then click **Create**.</span></span>
7. <span data-ttu-id="2b4ae-119">Hello 다음 화면에서 적어 hello 값 hello 클라이언트의 ID 및 클라이언트 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-119">On hello next screen, make a note of hello values of hello client ID and client secret.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2b4ae-120">hello 클라이언트 암호는는 중요 한 보안 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-120">hello client secret is an important security credential.</span></span> <span data-ttu-id="2b4ae-121">다른 사람과 이 암호를 공유하거나 클라이언트 응용 프로그램 내에 배포하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-121">Do not share this secret with anyone or distribute it within a client application.</span></span>


## <span data-ttu-id="2b4ae-122"><a name="secrets"></a>Google 추가 정보 tooyour 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2b4ae-122"><a name="secrets"> </a>Add Google information tooyour application</span></span>
1. <span data-ttu-id="2b4ae-123">Hello에 다시 [Azure 포털], tooyour 응용 프로그램을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-123">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="2b4ae-124">**Settings**를 클릭한 다음 **Authentication / Authorization**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-124">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="2b4ae-125">경우 hello 인증 / 권한 부여 기능은 활성화 되지 않으면, 너무 hello 스위치 설정**에**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-125">If hello Authentication / Authorization feature is not enabled, turn hello switch too**On**.</span></span>
3. <span data-ttu-id="2b4ae-126">**Google**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-126">Click **Google**.</span></span> <span data-ttu-id="2b4ae-127">이전에 얻은 hello 앱 ID 및 응용 프로그램 암호 값에 붙여 넣고 필요에 따라 응용 프로그램에 필요한 모든 범위를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-127">Paste in hello App ID and App Secret values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="2b4ae-128">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-128">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="2b4ae-129">기본적으로 앱 서비스 인증을 제공 하지만 콘텐츠 액세스 권한이 tooyour 사이트 및 Api 제한 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-129">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="2b4ae-130">앱 코드에서 사용자 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-130">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="2b4ae-131">(선택 사항) toorestrict 액세스 tooyour 사이트 tooonly 사용자 Google에 의해 인증 설정 **요청이 인증 되지 않은 경우 동작 tootake** 너무**Google**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-131">(Optional) toorestrict access tooyour site tooonly users authenticated by Google, set **Action tootake when request is not authenticated** too**Google**.</span></span> <span data-ttu-id="2b4ae-132">이 경우 모든 요청을 인증할 수 하 고 인증 되지 않은 모든 요청은 인증에 대 한 리디렉션된 tooGoogle 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-132">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooGoogle for authentication.</span></span>
5. <span data-ttu-id="2b4ae-133">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-133">Click **Save**.</span></span>

<span data-ttu-id="2b4ae-134">이제 준비 toouse Google 인증에 대 한 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ae-134">You are now ready toouse Google for authentication in your app.</span></span>

## <span data-ttu-id="2b4ae-135"><a name="related-content"> </a>관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="2b4ae-135"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[Azure 포털]: https://portal.azure.com/

