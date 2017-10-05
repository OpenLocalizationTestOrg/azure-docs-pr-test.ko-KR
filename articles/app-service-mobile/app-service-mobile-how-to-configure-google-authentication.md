---
title: "앱 서비스 응용 프로그램에 대해 Google 인증을 구성하는 방법"
description: "앱 서비스 응용 프로그램에 대해 Google 인증을 구성하는 방법을 알아봅니다."
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
ms.openlocfilehash: d6c1707f67d986487e5a45e76ffc9a02ddf16eb1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-google-login"></a><span data-ttu-id="9b7a4-103">Google 로그인을 사용하도록 앱 서비스 응용 프로그램을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="9b7a4-103">How to configure your App Service application to use Google login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="9b7a4-104">이 항목에서는 Google을 인증 공급자로 사용하도록 Azure 앱 서비스를 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-104">This topic shows you how to configure Azure App Service to use Google as an authentication provider.</span></span>

<span data-ttu-id="9b7a4-105">이 항목의 절차를 완료하려면 검증된 메일 주소가 포함된 Google 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-105">To complete the procedure in this topic, you must have a Google account that has a verified email address.</span></span> <span data-ttu-id="9b7a4-106">새 Google 계정을 만들려면 [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302)으로 이동하십시오.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-106">To create a new Google account, go to [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>

## <span data-ttu-id="9b7a4-107"><a name="register"> </a>Google을 사용하여 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="9b7a4-107"><a name="register"> </a>Register your application with Google</span></span>
1. <span data-ttu-id="9b7a4-108">[Azure 포털]에 로그온한 다음 응용 프로그램으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-108">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="9b7a4-109">**URL**을 복사하여 나중에 Google 앱을 구성하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-109">Copy your **URL**, which you use later to configure your Google app.</span></span>
2. <span data-ttu-id="9b7a4-110">[Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303) 웹 사이트로 이동하고 Google 계정 자격 증명으로 로그인하고 **프로젝트 만들기**를 클릭하고 **프로젝트 이름**을 입력한 후 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-110">Navigate to the [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303) website, sign in with your Google account credentials, click **Create Project**, provide a **Project name**, then click **Create**.</span></span>
3. <span data-ttu-id="9b7a4-111">**Social APIs** 아래에서 **Google+ API**, **Enable**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-111">Under **Social APIs** click **Google+ API** and then **Enable**.</span></span>
4. <span data-ttu-id="9b7a4-112">왼쪽 탐색에서 **Credentials** > **OAuth consent screen**을 클릭하고 **Email address**를 선택한 다음 **Product Name**을 입력하고 **Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-112">In the left navigation, **Credentials** > **OAuth consent screen**, then select your **Email address**,  enter a **Product Name**, and click **Save**.</span></span>
5. <span data-ttu-id="9b7a4-113">**Credentials** 탭에서**Create credentials** > **OAuth client ID**를 클릭하고 **Web application**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-113">In the **Credentials** tab, click **Create credentials** > **OAuth client ID**, then select **Web application**.</span></span>
6. <span data-ttu-id="9b7a4-114">앞서 복사한 App Service **URL**을 **Authorized JavaScript Origins**에 붙여넣고, 리디렉션 URI를**Authorized Redirect URI**에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-114">Paste the App Service **URL** you copied earlier into **Authorized JavaScript Origins**, then paste your redirect URI into **Authorized Redirect URI**.</span></span> <span data-ttu-id="9b7a4-115">리디렉션 URI는 경로 */.auth/login/google/callback*이 추가된 응용 프로그램의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-115">The redirect URI is the URL of your application appended with the path, */.auth/login/google/callback*.</span></span> <span data-ttu-id="9b7a4-116">예: `https://contoso.azurewebsites.net/.auth/login/google/callback`</span><span class="sxs-lookup"><span data-stu-id="9b7a4-116">For example, `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span></span> <span data-ttu-id="9b7a4-117">HTTPS 체계를 사용 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-117">Make sure that you are using the HTTPS scheme.</span></span> <span data-ttu-id="9b7a4-118">그런 다음 **Create**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-118">Then click **Create**.</span></span>
7. <span data-ttu-id="9b7a4-119">다음 화면에서 클라이언트 ID 및 클라이언트 암호 값을 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-119">On the next screen, make a note of the values of the client ID and client secret.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="9b7a4-120">클라이언트 암호는 중요한 보안 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-120">The client secret is an important security credential.</span></span> <span data-ttu-id="9b7a4-121">다른 사람과 이 암호를 공유하거나 클라이언트 응용 프로그램 내에 배포하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-121">Do not share this secret with anyone or distribute it within a client application.</span></span>


## <span data-ttu-id="9b7a4-122"><a name="secrets"> </a>응용 프로그램에 Google 정보 추가</span><span class="sxs-lookup"><span data-stu-id="9b7a4-122"><a name="secrets"> </a>Add Google information to your application</span></span>
1. <span data-ttu-id="9b7a4-123">[Azure 포털]로 돌아가서 응용 프로그램으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-123">Back in the [Azure portal], navigate to your application.</span></span> <span data-ttu-id="9b7a4-124">**Settings**를 클릭한 다음 **Authentication / Authorization**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-124">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="9b7a4-125">인증/권한 부여 기능이 사용하도록 설정되지 않은 경우 스위치를 **On**으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-125">If the Authentication / Authorization feature is not enabled, turn the switch to **On**.</span></span>
3. <span data-ttu-id="9b7a4-126">**Google**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-126">Click **Google**.</span></span> <span data-ttu-id="9b7a4-127">이전에 가져온 앱 ID 및 앱 암호 값을 붙여넣고 필요에 따라 응용 프로그램에 필요한 범위를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-127">Paste in the App ID and App Secret values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="9b7a4-128">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-128">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="9b7a4-129">기본적으로 앱 서비스는 인증을 제공하지만 사이트 콘텐츠 및 API에 액세스하는 권한을 제한하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-129">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="9b7a4-130">앱 코드에서 사용자 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-130">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="9b7a4-131">(선택 사항) Google에서 인증된 사용자만 사이트에 액세스하도록 제한하려면 **Google**에 **요청이 인증되지 않으면 수행할 동작**을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-131">(Optional) To restrict access to your site to only users authenticated by Google, set **Action to take when request is not authenticated** to **Google**.</span></span> <span data-ttu-id="9b7a4-132">이렇게 하려면 모든 요청이 인증되어야 하며 모든 인증되지 않은 요청은 인증을 위해 Google에 리디렉션되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-132">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Google for authentication.</span></span>
5. <span data-ttu-id="9b7a4-133">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-133">Click **Save**.</span></span>

<span data-ttu-id="9b7a4-134">이제 앱에서 Google을 인증에 사용할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9b7a4-134">You are now ready to use Google for authentication in your app.</span></span>

## <span data-ttu-id="9b7a4-135"><a name="related-content"> </a>관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="9b7a4-135"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[Azure 포털]: https://portal.azure.com/

