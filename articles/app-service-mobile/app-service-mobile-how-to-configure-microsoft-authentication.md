---
title: "앱 서비스 응용 프로그램에 대해 Microsoft 계정 인증을 구성하는 방법"
description: "앱 서비스 응용 프로그램에 대해 Microsoft 계정 인증을 구성하는 방법을 알아봅니다."
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: ffbc6064-edf6-474d-971c-695598fd08bf
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 67386b03ae4cc683fe00e11e8dad19d1442eff09
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-microsoft-account-login"></a><span data-ttu-id="e4676-103">Microsoft 계정 로그인을 사용하도록 앱 서비스 응용 프로그램을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="e4676-103">How to configure your App Service application to use Microsoft Account login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="e4676-104">이 항목에서는 Microsoft 계정을 인증 공급자로 사용하도록 Azure 앱 서비스를 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-104">This topic shows you how to configure Azure App Service to use Microsoft Account as an authentication provider.</span></span> 

## <span data-ttu-id="e4676-105"><a name="register-microsoft-account"> </a>Microsoft 계정을 사용하여 앱 등록</span><span class="sxs-lookup"><span data-stu-id="e4676-105"><a name="register-microsoft-account"> </a>Register your app with Microsoft Account</span></span>
1. <span data-ttu-id="e4676-106">[Azure Portal]에 로그온한 다음 응용 프로그램으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-106">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="e4676-107">**URL**을 복사하여 나중에 Microsoft 계정으로 응용 프로그램을 구성하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-107">Copy your **URL**, which later you use to configure your app with Microsoft Account.</span></span>
2. <span data-ttu-id="e4676-108">Microsoft 계정 개발자 센터의 [내 응용 프로그램] 페이지로 이동하고 필요한 경우 Microsoft 계정으로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-108">Navigate to the [My Applications] page in the Microsoft Account Developer Center, and log on with your Microsoft account, if required.</span></span>
3. <span data-ttu-id="e4676-109">**앱 추가**를 클릭한 후 응용 프로그램 이름을 입력하고 **응용 프로그램 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-109">Click **Add an app**, then type an application name, and click **Create application**.</span></span>
4. <span data-ttu-id="e4676-110">나중에 필요하므로 **응용 프로그램 ID**를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-110">Make a note of the **Application ID**, as you will need it later.</span></span> 
5. <span data-ttu-id="e4676-111">"플랫폼" 아래에서 **플랫폼 추가** 를 클릭하고 "웹"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-111">Under "Platforms," click **Add Platform** and select "Web".</span></span>
6. <span data-ttu-id="e4676-112">"리디렉션 URI" 아래에서 응용 프로그램에 대한 끝점을 입력한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-112">Under "Redirect URIs" supply the endpoint for your application, then click **Save**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="e4676-113">리디렉션 URI는 경로 */.auth/login/microsoftaccount/callback*이 추가된 응용 프로그램의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-113">Your redirect URI is the URL of your application appended with the path, */.auth/login/microsoftaccount/callback*.</span></span> <span data-ttu-id="e4676-114">예: `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`</span><span class="sxs-lookup"><span data-stu-id="e4676-114">For example, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span></span>   
   > <span data-ttu-id="e4676-115">HTTPS 체계를 사용 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-115">Make sure that you are using the HTTPS scheme.</span></span>
   
7. <span data-ttu-id="e4676-116">"응용 프로그램 암호" 아래에서 **새 암호 생성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-116">Under "Application Secrets," click **Generate New Password**.</span></span> <span data-ttu-id="e4676-117">표시되는 값을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-117">Make note of the value that appears.</span></span> <span data-ttu-id="e4676-118">이 페이지를 떠나면 다시 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-118">Once you leave the page, it will not be displayed again.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e4676-119">암호는 중요한 보안 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-119">The password is an important security credential.</span></span> <span data-ttu-id="e4676-120">다른 사람과 암호를 공유하거나 클라이언트 응용 프로그램 내에 배포하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="e4676-120">Do not share the password with anyone or distribute it within a client application.</span></span>

## <span data-ttu-id="e4676-121"><a name="secrets"> </a>앱 서비스 응용 프로그램에 Microsoft 계정 정보 추가</span><span class="sxs-lookup"><span data-stu-id="e4676-121"><a name="secrets"> </a>Add Microsoft Account information to your App Service application</span></span>
1. <span data-ttu-id="e4676-122">[Azure Portal]로 돌아가서 응용 프로그램으로 이동하여 **설정** > **인증/권한 부여**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-122">Back in the [Azure portal], navigate to your application, click **Settings** > **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="e4676-123">인증/권한 부여 기능이 사용하도록 설정되지 않은 경우 스위치를 **켭니다**.</span><span class="sxs-lookup"><span data-stu-id="e4676-123">If the Authentication / Authorization feature is not enabled, switch it **On**.</span></span>
3. <span data-ttu-id="e4676-124">**Microsoft 계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-124">Click **Microsoft Account**.</span></span> <span data-ttu-id="e4676-125">이전에 가져온 응용 프로그램 ID 및 암호 값을 붙여넣고 필요에 따라 응용 프로그램에 필요한 범위를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-125">Paste in the Application ID and Password values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="e4676-126">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-126">Then click **OK**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="e4676-127">기본적으로 앱 서비스는 인증을 제공하지만 사이트 콘텐츠 및 API에 액세스하는 권한을 제한하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-127">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="e4676-128">앱 코드에서 사용자 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-128">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="e4676-129">(선택 사항) Microsoft 계정에서 인증된 사용자만 사이트에 액세스하도록 제한하려면 **Microsoft 계정**에 **요청이 인증되지 않으면 수행할 동작**을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-129">(Optional) To restrict access to your site to only users authenticated by Microsoft account, set **Action to take when request is not authenticated** to **Microsoft Account**.</span></span> <span data-ttu-id="e4676-130">이렇게 하려면 모든 요청이 인증되어야 하며 모든 인증되지 않은 요청은 인증을 위해 Microsoft 계정에 리디렉션되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-130">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Microsoft account for authentication.</span></span>
5. <span data-ttu-id="e4676-131">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-131">Click **Save**.</span></span>

<span data-ttu-id="e4676-132">이제 앱에서 Microsoft 계정을 인증에 사용할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-132">You are now ready to use Microsoft Account for authentication in your app.</span></span>

## <span data-ttu-id="e4676-133"><a name="related-content"> </a>관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="e4676-133"><a name="related-content"> </a>Related content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[내 응용 프로그램]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Azure Portal]: https://portal.azure.com/
