---
title: "앱 서비스 응용 프로그램에 대해 Facebook 인증을 구성하는 방법"
description: "앱 서비스 응용 프로그램에 대해 Facebook 인증을 구성하는 방법을 알아봅니다."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: b6b4f062-fcb4-47b3-b75a-ec4cb51a62fd
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: c1b4c91d384c56c4f55bf8d31ced250f51c0d837
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-facebook-login"></a><span data-ttu-id="7dfd5-103">Facebook 로그인을 사용하도록 앱 서비스 응용 프로그램을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="7dfd5-103">How to configure your App Service application to use Facebook login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="7dfd5-104">이 항목에서는 Facebook을 인증 공급자로 사용하도록 Azure 앱 서비스를 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-104">This topic shows you how to configure Azure App Service to use Facebook as an authentication provider.</span></span>

<span data-ttu-id="7dfd5-105">이 토픽의 절차를 완료하려면 검증된 메일 주소와 휴대폰 번호가 포함된 Facebook 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-105">To complete the procedure in this topic, you must have a Facebook account that has a verified email address and a mobile phone number.</span></span> <span data-ttu-id="7dfd5-106">새 Facebook 계정을 만들려면 [facebook.com]으로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-106">To create a new Facebook account, go to [facebook.com].</span></span>

## <span data-ttu-id="7dfd5-107"><a name="register"> </a>Facebook을 사용하여 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="7dfd5-107"><a name="register"> </a>Register your application with Facebook</span></span>
1. <span data-ttu-id="7dfd5-108">[Azure 포털]에 로그온한 다음 응용 프로그램으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-108">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="7dfd5-109">**URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-109">Copy your **URL**.</span></span> <span data-ttu-id="7dfd5-110">Facebook 앱을 구성하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-110">You will use this to configure your Facebook app.</span></span>
2. <span data-ttu-id="7dfd5-111">다른 브라우저 창에서 [Facebook 개발자] 웹 사이트로 이동한 다음 Facebook 계정 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-111">In another browser window, navigate to the [Facebook Developers] website and sign-in with your Facebook account credentials.</span></span>
3. <span data-ttu-id="7dfd5-112">(옵션) 아직 등록하지 않은 경우 **Apps** > **Register as a Developer**를 클릭하고 정책에 동의한 후 등록 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-112">(Optional) If you have not already registered, click **Apps** > **Register as a Developer**, then accept the policy and follow the registration steps.</span></span>
4. <span data-ttu-id="7dfd5-113">**My Apps** > **Add a New App** > **Website** > **Skip and Create App ID**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-113">Click **My Apps** > **Add a New App** > **Website** > **Skip and Create App ID**.</span></span> 
5. <span data-ttu-id="7dfd5-114">**표시 이름**에 앱의 고유한 이름을 입력하고 **연락처 전자 메일**을 입력하며 앱의 **범주**를 선택한 다음 **앱 ID 만들기**를 클릭하고 보안 검사를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-114">In **Display Name**, type a unique name for your app, type your **Contact Email**, choose a **Category** for your app, then click **Create App ID** and complete the security check.</span></span> <span data-ttu-id="7dfd5-115">새 Facebook 앱에 대한 개발자 대시보드로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-115">This takes you to the developer dashboard for your new Facebook app.</span></span>
6. <span data-ttu-id="7dfd5-116">"Facebook 로그인"에서 **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-116">Under "Facebook Login," click **Get Started**.</span></span> <span data-ttu-id="7dfd5-117">응용 프로그램의 **리디렉션 URI**를 **유효한 OAuth 리디렉션 URI**에 추가한 다음 **변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-117">Add your application's **Redirect URI** to **Valid OAuth redirect URIs**, then click **Save Changes**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="7dfd5-118">리디렉션 URI는 경로 */.auth/login/facebook/callback*이 추가된 응용 프로그램의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-118">Your redirect URI is the URL of your application appended with the path, */.auth/login/facebook/callback*.</span></span> <span data-ttu-id="7dfd5-119">예: `https://contoso.azurewebsites.net/.auth/login/facebook/callback`</span><span class="sxs-lookup"><span data-stu-id="7dfd5-119">For example, `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span></span> <span data-ttu-id="7dfd5-120">HTTPS 체계를 사용 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-120">Make sure that you are using the HTTPS scheme.</span></span>
   > 
   > 
7. <span data-ttu-id="7dfd5-121">왼쪽 탐색에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-121">In the left-hand navigation, click **Settings**.</span></span> <span data-ttu-id="7dfd5-122">**App Secret** 필드에서 **Show**를 클릭하고 요청될 경우 암호를 제공한 다음 **App ID** 및 **App Secret** 값을 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-122">On the **App Secret** field, click **Show**, provide your password if requested, then make a note of the values of **App ID** and **App Secret**.</span></span> <span data-ttu-id="7dfd5-123">나중에 이 값을 사용하여 Azure에서 응용 프로그램을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-123">You use these later to configure your application in Azure.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="7dfd5-124">앱 암호는 중요한 보안 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-124">The app secret is an important security credential.</span></span> <span data-ttu-id="7dfd5-125">다른 사람과 이 암호를 공유하거나 클라이언트 응용 프로그램 내에 배포하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-125">Do not share this secret with anyone or distribute it within a client application.</span></span>
   > 
   > 
8. <span data-ttu-id="7dfd5-126">응용 프로그램을 등록하는 데 사용된 Facebook 계정이 앱의 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-126">The Facebook account which was used to register the application is an administrator of the app.</span></span> <span data-ttu-id="7dfd5-127">지금은 관리자만 이 응용 프로그램에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-127">At this point, only administrators can sign into this application.</span></span> <span data-ttu-id="7dfd5-128">다른 Facebook 계정을 인증하려면 **앱 검토**를 클릭하고 **공용 <your-app-name> 만들기**를 사용하도록 설정하여 Facebook 인증을 사용한 일반 공용 액세스를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-128">To authenticate other Facebook accounts, click **App Review** and enable **Make <your-app-name> public** to enable general public access using Facebook authentication.</span></span>

## <span data-ttu-id="7dfd5-129"><a name="secrets"> </a>응용 프로그램에 Facebook 정보 추가</span><span class="sxs-lookup"><span data-stu-id="7dfd5-129"><a name="secrets"> </a>Add Facebook information to your application</span></span>
1. <span data-ttu-id="7dfd5-130">[Azure 포털]로 돌아가서 응용 프로그램으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-130">Back in the [Azure portal], navigate to your application.</span></span> <span data-ttu-id="7dfd5-131">**설정** > **인증 / 권한 부여**를 클릭하고 **App Service 인증**이 **켜기**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-131">Click **Settings** > **Authentication / Authorization**, and make sure that **App Service Authentication** is **On**.</span></span>
2. <span data-ttu-id="7dfd5-132">**Facebook**을 클릭하고 이전에 가져온 앱 ID 및 앱 암호 값을 붙여넣습니다. 필요한 경우 응용 프로그램에 필요한 모든 범위를 사용하도록 설정한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-132">Click **Facebook**, paste in the App ID and App Secret values which you obtained previously, optionally enable any scopes needed by your application, then click **OK**.</span></span>
   
    ![][0]
   
    <span data-ttu-id="7dfd5-133">기본적으로 앱 서비스는 인증을 제공하지만 사이트 콘텐츠 및 API에 액세스하는 권한을 제한하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-133">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="7dfd5-134">앱 코드에서 사용자 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-134">You must authorize users in your app code.</span></span>
3. <span data-ttu-id="7dfd5-135">(옵션) Facebook에서 인증된 사용자만 사이트에 액세스하도록 제한하려면 **Facebook**에 **요청이 인증되지 않으면 수행할 동작**을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-135">(Optional) To restrict access to your site to only users authenticated by Facebook, set **Action to take when request is not authenticated** to **Facebook**.</span></span> <span data-ttu-id="7dfd5-136">이렇게 하려면 모든 요청이 인증되어야 하며 모든 인증되지 않은 요청은 인증을 위해 Facebook에 리디렉션되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-136">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Facebook for authentication.</span></span>
4. <span data-ttu-id="7dfd5-137">인증 구성이 완료되면 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-137">When done configuring authentication, click **Save**.</span></span>

<span data-ttu-id="7dfd5-138">이제 앱에서 Facebook을 인증에 사용할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7dfd5-138">You are now ready to use Facebook for authentication in your app.</span></span>

## <span data-ttu-id="7dfd5-139"><a name="related-content"> </a>관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="7dfd5-139"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
<span data-ttu-id="7dfd5-140">[Facebook 개발자]: http://go.microsoft.com/fwlink/p/?LinkId=268286</span><span class="sxs-lookup"><span data-stu-id="7dfd5-140">[Facebook Developers]: http://go.microsoft.com/fwlink/p/?LinkId=268286</span></span>
<span data-ttu-id="7dfd5-141">[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285</span><span class="sxs-lookup"><span data-stu-id="7dfd5-141">[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285</span></span>
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
<span data-ttu-id="7dfd5-142">[Azure 포털]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="7dfd5-142">[Azure portal]: https://portal.azure.com/</span></span>
