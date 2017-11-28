---
title: "응용 프로그램 서비스 응용 프로그램에 대 한 aaaHow tooconfigure Microsoft 계정 인증"
description: "자세한 방법을 응용 프로그램 서비스 응용 프로그램에 대 한 tooconfigure Microsoft 계정을 인증 합니다."
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
ms.openlocfilehash: d86d8dab26a189f4454082fc18e44e3fb6e0a01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-microsoft-account-login"></a><span data-ttu-id="8ec50-103">어떻게 tooconfigure 앱 서비스 응용 프로그램 toouse Microsoft 계정 로그인</span><span class="sxs-lookup"><span data-stu-id="8ec50-103">How tooconfigure your App Service application toouse Microsoft Account login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="8ec50-104">이 항목에서는 Microsoft 계정으로 인증 공급자로 tooconfigure Azure 앱 서비스 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec50-104">This topic shows you how tooconfigure Azure App Service toouse Microsoft Account as an authentication provider.</span></span> 

## <span data-ttu-id="8ec50-105"><a name="register-microsoft-account"> </a>Microsoft 계정을 사용하여 앱 등록</span><span class="sxs-lookup"><span data-stu-id="8ec50-105"><a name="register-microsoft-account"> </a>Register your app with Microsoft Account</span></span>
1. <span data-ttu-id="8ec50-106">Toohello 로그온 [Azure 포털], tooyour 응용 프로그램을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec50-106">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="8ec50-107">복사 프로그램 **URL**이며 나중에 tooconfigure 응용 프로그램에 Microsoft 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec50-107">Copy your **URL**, which later you use tooconfigure your app with Microsoft Account.</span></span>
2. <span data-ttu-id="8ec50-108">Toohello 이동 [내 응용 프로그램] hello Microsoft 계정 개발자 센터에서에서 페이지 하 고 필요한 경우 Microsoft 계정으로 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec50-108">Navigate toohello [My Applications] page in hello Microsoft Account Developer Center, and log on with your Microsoft account, if required.</span></span>
3. <span data-ttu-id="8ec50-109">**앱 추가**를 클릭한 후 응용 프로그램 이름을 입력하고 **응용 프로그램 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec50-109">Click **Add an app**, then type an application name, and click **Create application**.</span></span>
4. <span data-ttu-id="8ec50-110">Hello 메모 **응용 프로그램 ID**와 마찬가지로 나중에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec50-110">Make a note of hello **Application ID**, as you will need it later.</span></span> 
5. <span data-ttu-id="8ec50-111">"플랫폼" 아래에서 **플랫폼 추가** 를 클릭하고 "웹"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec50-111">Under "Platforms," click **Add Platform** and select "Web".</span></span>
6. <span data-ttu-id="8ec50-112">응용 프로그램에 대 한 "리디렉션 Uri" 공급 hello 끝점을 클릭 한 다음 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec50-112">Under "Redirect URIs" supply hello endpoint for your application, then click **Save**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="8ec50-113">프로그램 리디렉션 URI는 hello 경로 추가 되므로 응용 프로그램의 hello URL */.auth/login/microsoftaccount/callback*합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec50-113">Your redirect URI is hello URL of your application appended with hello path, */.auth/login/microsoftaccount/callback*.</span></span> <span data-ttu-id="8ec50-114">예: `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span><span class="sxs-lookup"><span data-stu-id="8ec50-114">For example, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span></span>   
   > <span data-ttu-id="8ec50-115">Hello HTTPS 체계를 사용 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec50-115">Make sure that you are using hello HTTPS scheme.</span></span>
   
7. <span data-ttu-id="8ec50-116">"응용 프로그램 암호" 아래에서 **새 암호 생성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec50-116">Under "Application Secrets," click **Generate New Password**.</span></span> <span data-ttu-id="8ec50-117">표시 된 hello 값을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="8ec50-117">Make note of hello value that appears.</span></span> <span data-ttu-id="8ec50-118">Hello 페이지를 벗어나면 되 면 다시 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ec50-118">Once you leave hello page, it will not be displayed again.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="8ec50-119">hello 암호가 중요 한 보안 자격 증명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec50-119">hello password is an important security credential.</span></span> <span data-ttu-id="8ec50-120">클라이언트 응용 프로그램 내에서 배포 하거나 hello 암호 다른 사람과 공유 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="8ec50-120">Do not share hello password with anyone or distribute it within a client application.</span></span>

## <span data-ttu-id="8ec50-121"><a name="secrets"></a>Microsoft 계정 추가 정보 tooyour 응용 프로그램 서비스 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="8ec50-121"><a name="secrets"> </a>Add Microsoft Account information tooyour App Service application</span></span>
1. <span data-ttu-id="8ec50-122">Hello에 다시 [Azure 포털]tooyour 응용 프로그램을 탐색, 클릭, **설정** > **인증 / 권한 부여**합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec50-122">Back in hello [Azure portal], navigate tooyour application, click **Settings** > **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="8ec50-123">경우 hello 인증 / 권한 부여 기능은 활성화 되지 않으면, 전환 **에**합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec50-123">If hello Authentication / Authorization feature is not enabled, switch it **On**.</span></span>
3. <span data-ttu-id="8ec50-124">**Microsoft 계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec50-124">Click **Microsoft Account**.</span></span> <span data-ttu-id="8ec50-125">이전에 얻은 hello 응용 프로그램 ID 및 암호 값에 붙여 넣고 필요에 따라 응용 프로그램에 필요한 모든 범위를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec50-125">Paste in hello Application ID and Password values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="8ec50-126">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec50-126">Then click **OK**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="8ec50-127">기본적으로 앱 서비스 인증을 제공 하지만 콘텐츠 액세스 권한이 tooyour 사이트 및 Api 제한 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ec50-127">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="8ec50-128">앱 코드에서 사용자 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec50-128">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="8ec50-129">(선택 사항) toorestrict 액세스 tooyour 사이트 tooonly 사용자 Microsoft 계정에 의해 인증 설정 **요청이 인증 되지 않은 경우 동작 tootake** 너무**Microsoft 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec50-129">(Optional) toorestrict access tooyour site tooonly users authenticated by Microsoft account, set **Action tootake when request is not authenticated** too**Microsoft Account**.</span></span> <span data-ttu-id="8ec50-130">이 경우 모든 요청을 인증할 수 하 고 인증 되지 않은 모든 요청을 리디렉션하 tooMicrosoft 계정 인증에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec50-130">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooMicrosoft account for authentication.</span></span>
5. <span data-ttu-id="8ec50-131">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec50-131">Click **Save**.</span></span>

<span data-ttu-id="8ec50-132">이제 준비 toouse Microsoft 계정 인증에 대 한 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="8ec50-132">You are now ready toouse Microsoft Account for authentication in your app.</span></span>

## <span data-ttu-id="8ec50-133"><a name="related-content"> </a>관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="8ec50-133"><a name="related-content"> </a>Related content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[내 응용 프로그램]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Azure 포털]: https://portal.azure.com/
