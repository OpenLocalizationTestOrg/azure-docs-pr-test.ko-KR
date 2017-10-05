---
title: "앱 서비스 응용 프로그램에 대해 Twitter 인증을 구성하는 방법"
description: "앱 서비스 응용 프로그램에 대해 Twitter 인증을 구성하는 방법을 알아봅니다."
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
ms.openlocfilehash: afde020b7817dc58ecea24eb4a09cf93d0986eb2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-twitter-login"></a><span data-ttu-id="b0097-103">Twitter 로그인을 사용하도록 앱 서비스 응용 프로그램을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="b0097-103">How to configure your App Service application to use Twitter login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="b0097-104">이 항목에서는 Twitter를 인증 공급자로 사용하도록 Azure 앱 서비스를 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-104">This topic shows you how to configure Azure App Service to use Twitter as an authentication provider.</span></span>

<span data-ttu-id="b0097-105">이 항목의 절차를 완료하려면 검증된 전자 메일 주소 및 전화 번호가 포함된 Twitter 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-105">To complete the procedure in this topic, you must have a Twitter account that has a verified email address and phone number.</span></span> <span data-ttu-id="b0097-106">새 Twitter 계정을 만들려면 <a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-106">To create a new Twitter account, go to <a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span></span>

## <span data-ttu-id="b0097-107"><a name="register"> </a>Twitter를 사용하여 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="b0097-107"><a name="register"> </a>Register your application with Twitter</span></span>
1. <span data-ttu-id="b0097-108">[Azure 포털]에 로그인한 다음 응용 프로그램으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-108">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="b0097-109">**URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-109">Copy your **URL**.</span></span> <span data-ttu-id="b0097-110">Twitter 앱을 구성하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-110">You will use this to configure your Twitter app.</span></span>
2. <span data-ttu-id="b0097-111">[Twitter 개발자] 웹 사이트로 이동하고 Twitter 계정 자격 증명을 사용하여 로그인한 다음 **새 앱 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-111">Navigate to the [Twitter Developers] website, sign in with your Twitter account credentials, and click **Create New App**.</span></span>
3. <span data-ttu-id="b0097-112">새 앱에 대한 **이름** 및 **설명**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-112">Type in the **Name** and a **Description** for your new app.</span></span> <span data-ttu-id="b0097-113">**Website** 값으로 응용 프로그램의 **URL**을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-113">Paste in your application's **URL** for the **Website** value.</span></span> <span data-ttu-id="b0097-114">그런 다음에 **Callback URL**에 앞서 복사한 **Callback URL**을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-114">Then, for the **Callback URL**, paste the **Callback URL** you copied earlier.</span></span> <span data-ttu-id="b0097-115">이는 */.auth/login/twitter/callback*경로를 사용하여 추가된 모바일 앱 게이트웨이입니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-115">This is your Mobile App gateway appended with the path, */.auth/login/twitter/callback*.</span></span> <span data-ttu-id="b0097-116">예: `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="b0097-116">For example, `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span></span> <span data-ttu-id="b0097-117">HTTPS 체계를 사용 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-117">Make sure that you are using the HTTPS scheme.</span></span>
4. <span data-ttu-id="b0097-118">페이지 맨 아래에서 사용 약관을 읽고 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-118">At the bottom the page, read and accept the terms.</span></span> <span data-ttu-id="b0097-119">그런 다음 **Create your Twitter application**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-119">Then click **Create your Twitter application**.</span></span> <span data-ttu-id="b0097-120">앱이 등록되고 응용 프로그램 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-120">This registers the app displays the application details.</span></span>
5. <span data-ttu-id="b0097-121">**Settings** 탭을 클릭하고 **Allow this application to be used to sign in with Twitter**를 선택한 다음 **Update Settings**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-121">Click the **Settings** tab, check **Allow this application to be used to sign in with Twitter**, then click **Update Settings**.</span></span>
6. <span data-ttu-id="b0097-122">**Keys and Access Tokens** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-122">Select the **Keys and Access Tokens** tab.</span></span> <span data-ttu-id="b0097-123">**Consumer Key (API Key)** 및 **Consumer secret (API Secret)**의 값을 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-123">Make a note of the values of **Consumer Key (API Key)** and **Consumer secret (API Secret)**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b0097-124">소비자 암호는 중요한 보안 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-124">The consumer secret is an important security credential.</span></span> <span data-ttu-id="b0097-125">다른 사람과 이 암호를 공유하거나 앱과 함께 배포하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b0097-125">Do not share this secret with anyone or distribute it with your app.</span></span>
   > 
   > 

## <span data-ttu-id="b0097-126"><a name="secrets"> </a>응용 프로그램에 Twitter 정보 추가</span><span class="sxs-lookup"><span data-stu-id="b0097-126"><a name="secrets"> </a>Add Twitter information to your application</span></span>
1. <span data-ttu-id="b0097-127">[Azure 포털]로 돌아가서 응용 프로그램으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-127">Back in the [Azure portal], navigate to your application.</span></span> <span data-ttu-id="b0097-128">**Settings**를 클릭한 다음 **Authentication / Authorization**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-128">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="b0097-129">인증/권한 부여 기능이 사용하도록 설정되지 않은 경우 스위치를 **On**으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-129">If the Authentication / Authorization feature is not enabled, turn the switch to **On**.</span></span>
3. <span data-ttu-id="b0097-130">**Twitter**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-130">Click **Twitter**.</span></span> <span data-ttu-id="b0097-131">앞에서 얻은 App ID 및 App Secret 값을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-131">Paste in the App ID and App Secret values which you obtained previously.</span></span> <span data-ttu-id="b0097-132">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-132">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="b0097-133">기본적으로 앱 서비스는 인증을 제공하지만 사이트 콘텐츠 및 API에 액세스하는 권한을 제한하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-133">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="b0097-134">앱 코드에서 사용자 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-134">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="b0097-135">(선택 사항) Twitter에서 인증된 사용자만 사이트에 액세스하도록 제한하려면 **Twitter**에 **요청이 인증되지 않으면 수행할 동작**을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-135">(Optional) To restrict access to your site to only users authenticated by Twitter, set **Action to take when request is not authenticated** to **Twitter**.</span></span> <span data-ttu-id="b0097-136">이렇게 하려면 모든 요청이 인증되어야 하며 모든 인증되지 않은 요청은 인증을 위해 Twitter에 리디렉션되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-136">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Twitter for authentication.</span></span>
5. <span data-ttu-id="b0097-137">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-137">Click **Save**.</span></span>

<span data-ttu-id="b0097-138">이제 앱에서 Twitter를 인증에 사용할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b0097-138">You are now ready to use Twitter for authentication in your app.</span></span>

## <span data-ttu-id="b0097-139"><a name="related-content"> </a>관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="b0097-139"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-twitter-authentication/app-service-twitter-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-twitter-authentication/mobile-app-twitter-settings.png

<!-- URLs. -->

<span data-ttu-id="b0097-140">[Twitter 개발자]: http://go.microsoft.com/fwlink/p/?LinkId=268300</span><span class="sxs-lookup"><span data-stu-id="b0097-140">[Twitter Developers]: http://go.microsoft.com/fwlink/p/?LinkId=268300</span></span>
<span data-ttu-id="b0097-141">[Azure 포털]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="b0097-141">[Azure portal]: https://portal.azure.com/</span></span>
[xamarin]: ../app-services-mobile-app-xamarin-ios-get-started-users.md
