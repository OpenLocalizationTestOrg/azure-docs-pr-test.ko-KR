---
title: "응용 프로그램 서비스 응용 프로그램에 대 한 aaaHow tooconfigure Twitter 인증"
description: "자세한 방법을 응용 프로그램 서비스 응용 프로그램에 대 한 tooconfigure Twitter 인증 합니다."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: c6dc91d7-30f6-448c-9f2d-8e91104cde73
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 0d16ac44d7b54e3567b793a904059d31ab1d8911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-twitter-login"></a><span data-ttu-id="774b8-103">어떻게 tooconfigure 앱 서비스 응용 프로그램 toouse Twitter 로그인</span><span class="sxs-lookup"><span data-stu-id="774b8-103">How tooconfigure your App Service application toouse Twitter login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="774b8-104">이 항목에서는 tooconfigure Azure 앱 서비스를 인증 공급자로 Twitter toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-104">This topic shows you how tooconfigure Azure App Service toouse Twitter as an authentication provider.</span></span>

<span data-ttu-id="774b8-105">이 항목의 toocomplete hello 절차, 확인 된 전자 메일 주소와 전화 번호를 가진 Twitter 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-105">toocomplete hello procedure in this topic, you must have a Twitter account that has a verified email address and phone number.</span></span> <span data-ttu-id="774b8-106">새 Twitter 계정 toocreate 너무 이동<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-106">toocreate a new Twitter account, go too<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span></span>

## <span data-ttu-id="774b8-107"><a name="register"> </a>Twitter를 사용하여 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="774b8-107"><a name="register"> </a>Register your application with Twitter</span></span>
1. <span data-ttu-id="774b8-108">Toohello 로그온 [Azure 포털], tooyour 응용 프로그램을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="774b8-109">**URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-109">Copy your **URL**.</span></span> <span data-ttu-id="774b8-110">이 tooconfigure Twitter 앱을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-110">You will use this tooconfigure your Twitter app.</span></span>
2. <span data-ttu-id="774b8-111">Toohello 이동 [Twitter 개발자] 웹 사이트, Twitter 계정 자격 증명으로 로그인 하 고 클릭 **Create New App**합니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-111">Navigate toohello [Twitter Developers] website, sign in with your Twitter account credentials, and click **Create New App**.</span></span>
3. <span data-ttu-id="774b8-112">Hello 입력 **이름** 및 **설명** 새 앱에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-112">Type in hello **Name** and a **Description** for your new app.</span></span> <span data-ttu-id="774b8-113">응용 프로그램에서 붙여넣기 **URL** hello에 대 한 **웹 사이트** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-113">Paste in your application's **URL** for hello **Website** value.</span></span> <span data-ttu-id="774b8-114">Hello에 대 한 다음 **콜백 URL**, hello 붙여 **콜백 URL** 앞에서 복사한 합니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-114">Then, for hello **Callback URL**, paste hello **Callback URL** you copied earlier.</span></span> <span data-ttu-id="774b8-115">이 hello 경로 추가 되므로 모바일 응용 프로그램 게이트웨이 */.auth/login/twitter/callback*합니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-115">This is your Mobile App gateway appended with hello path, */.auth/login/twitter/callback*.</span></span> <span data-ttu-id="774b8-116">예: `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="774b8-116">For example, `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span></span> <span data-ttu-id="774b8-117">Hello HTTPS 체계를 사용 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-117">Make sure that you are using hello HTTPS scheme.</span></span>
4. <span data-ttu-id="774b8-118">Hello 아래쪽 hello 페이지에 읽고 hello 조건에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-118">At hello bottom hello page, read and accept hello terms.</span></span> <span data-ttu-id="774b8-119">그런 다음 **Create your Twitter application**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-119">Then click **Create your Twitter application**.</span></span> <span data-ttu-id="774b8-120">이 레지스터 hello 앱 hello 응용 프로그램 세부 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-120">This registers hello app displays hello application details.</span></span>
5. <span data-ttu-id="774b8-121">Hello 클릭 **설정** 탭 **Twitter 사용 하 여이 응용 프로그램 사용 toobe toosign 허용**, 클릭 **업데이트 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-121">Click hello **Settings** tab, check **Allow this application toobe used toosign in with Twitter**, then click **Update Settings**.</span></span>
6. <span data-ttu-id="774b8-122">선택 hello **키와 액세스 토큰이** 탭 합니다. Hello 값을 메모 **소비자 키 (API 키)** 및 **소비자 암호 (API Secret)**합니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-122">Select hello **Keys and Access Tokens** tab. Make a note of hello values of **Consumer Key (API Key)** and **Consumer secret (API Secret)**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="774b8-123">hello 소비자 암호는는 중요 한 보안 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-123">hello consumer secret is an important security credential.</span></span> <span data-ttu-id="774b8-124">다른 사람과 이 암호를 공유하거나 앱과 함께 배포하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="774b8-124">Do not share this secret with anyone or distribute it with your app.</span></span>
   > 
   > 

## <span data-ttu-id="774b8-125"><a name="secrets"></a>Twitter 추가 정보 tooyour 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="774b8-125"><a name="secrets"> </a>Add Twitter information tooyour application</span></span>
1. <span data-ttu-id="774b8-126">Hello에 다시 [Azure 포털], tooyour 응용 프로그램을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-126">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="774b8-127">**Settings**를 클릭한 다음 **Authentication / Authorization**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-127">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="774b8-128">경우 hello 인증 / 권한 부여 기능은 활성화 되지 않으면, 너무 hello 스위치 설정**에**합니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-128">If hello Authentication / Authorization feature is not enabled, turn hello switch too**On**.</span></span>
3. <span data-ttu-id="774b8-129">**Twitter**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-129">Click **Twitter**.</span></span> <span data-ttu-id="774b8-130">이전에 얻은 값을 hello 앱 ID와 응용 프로그램 암호에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-130">Paste in hello App ID and App Secret values which you obtained previously.</span></span> <span data-ttu-id="774b8-131">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-131">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="774b8-132">기본적으로 앱 서비스 인증을 제공 하지만 콘텐츠 액세스 권한이 tooyour 사이트 및 Api 제한 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-132">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="774b8-133">앱 코드에서 사용자 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-133">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="774b8-134">Twitter에 의해 인증 (선택 사항) toorestrict 액세스 tooyour 사이트 tooonly 사용자 설정 **요청이 인증 되지 않은 경우 동작 tootake** 너무**Twitter**합니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-134">(Optional) toorestrict access tooyour site tooonly users authenticated by Twitter, set **Action tootake when request is not authenticated** too**Twitter**.</span></span> <span data-ttu-id="774b8-135">이 경우 모든 요청을 인증할 수 하 고 인증 되지 않은 모든 요청은 인증에 대 한 리디렉션된 tooTwitter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-135">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooTwitter for authentication.</span></span>
5. <span data-ttu-id="774b8-136">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-136">Click **Save**.</span></span>

<span data-ttu-id="774b8-137">앱에 인증을 위해 준비 toouse Twitter 됩니다.</span><span class="sxs-lookup"><span data-stu-id="774b8-137">You are now ready toouse Twitter for authentication in your app.</span></span>

## <span data-ttu-id="774b8-138"><a name="related-content"> </a>관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="774b8-138"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-twitter-authentication/app-service-twitter-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-twitter-authentication/mobile-app-twitter-settings.png

<!-- URLs. -->

[Twitter 개발자]: http://go.microsoft.com/fwlink/p/?LinkId=268300
[Azure 포털]: https://portal.azure.com/
[xamarin]: ../app-services-mobile-app-xamarin-ios-get-started-users.md
