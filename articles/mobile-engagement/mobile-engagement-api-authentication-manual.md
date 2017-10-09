---
title: "Mobile Engagement REST Api-수동 설치로 aaaAuthenticate"
description: "Toomanually Mobile Engagement REST Api에 대 한 인증을 설정 하는 방법을 설명 합니다."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2e79f9c9-41e4-45ac-b427-3b8338675163
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 3884f94afcd6b9a62bfcf498fb6ee84bb6e837b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a><span data-ttu-id="84476-103">Mobile Engagement REST API를 사용한 인증 - 수동 설치</span><span class="sxs-lookup"><span data-stu-id="84476-103">Authenticate with Mobile Engagement REST APIs - manual setup</span></span>
<span data-ttu-id="84476-104">이 부록 설명서 너무는[Mobile Engagement REST Api로 인증](mobile-engagement-api-authentication.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="84476-104">This is an appendix documentation too[Authenticate with Mobile Engagement REST APIs](mobile-engagement-api-authentication.md).</span></span> <span data-ttu-id="84476-105">첫 번째 tooget hello 컨텍스트의 읽이 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84476-105">Make sure you read it first tooget hello context.</span></span> <span data-ttu-id="84476-106">이 설명 hello Mobile Engagement REST Api를 사용 하 여 Azure 포털을 hello에 대 한 대체 방법을 toodo hello 일회성에 대해 설정 된 사용자 인증 설정이 끝났습니다.</span><span class="sxs-lookup"><span data-stu-id="84476-106">This describes an alternate way toodo hello One-time setup for setting up your authentication for hello Mobile Engagement REST APIs using hello Azure Portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="84476-107">아래의 hello 지침 기반으로이 [Active Directory 가이드](../azure-resource-manager/resource-group-create-service-principal-portal.md) 와 Mobile Engagement Api에 대 한 인증을 위해 필요한 사항에 대 한 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="84476-107">hello instructions below are based on this [Active Directory guide](../azure-resource-manager/resource-group-create-service-principal-portal.md) and customized for what is required for authentication for Mobile Engagement APIs.</span></span> <span data-ttu-id="84476-108">따라서 아래 toounderstand hello 단계를 자세히 하려는 경우 tooit을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="84476-108">So refer tooit if you want toounderstand hello steps below in detail.</span></span> 
> 
> 

1. <span data-ttu-id="84476-109">Hello 통해 Azure 계정 로그인 tooyour [클래식 포털](https://manage.windowsazure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="84476-109">Login tooyour Azure Account through hello [classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="84476-110">선택 **Active Directory** hello 왼쪽된 창에서.</span><span class="sxs-lookup"><span data-stu-id="84476-110">Select **Active Directory** from hello left pane.</span></span>
   
     ![Active Directory 선택][1]
3. <span data-ttu-id="84476-112">Hello 선택 **Active Directory 기본** Azure 포털에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="84476-112">Choose hello **Default Active Directory** in your Azure portal.</span></span> 
   
     ![디렉터리 선택][2]
   
   > [!IMPORTANT]
   > <span data-ttu-id="84476-114">이 방법은 hello 기본 Active Directory의 계정에서에서 작업 하 고 사용자가 만든 계정에 Active Directory에서 이렇게 하는 경우 작동 하지 것입니다는 경우에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="84476-114">This approach works only when you are working in hello default Active Directory of your account and will not work if you are doing this in an Active Directory that you have created in your account.</span></span> 
   > 
   > 
4. <span data-ttu-id="84476-115">디렉터리의 tooview hello 응용 프로그램에서 클릭 **응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="84476-115">tooview hello applications in your directory, click on **Applications**.</span></span>
   
     ![응용 프로그램 보기][3]
5. <span data-ttu-id="84476-117">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="84476-117">Click on **ADD**.</span></span> 
   
     ![응용 프로그램 추가][4]
6. <span data-ttu-id="84476-119">**내 조직에서 개발 중인 응용 프로그램 추가**</span><span class="sxs-lookup"><span data-stu-id="84476-119">Click on **Add an application my organization is developing**</span></span>
   
     ![새 응용 프로그램][5]
7. <span data-ttu-id="84476-121">Hello 응용 프로그램 이름 선택 hello 유형의 응용 프로그램으로를 입력 **웹 응용 프로그램 및/또는 웹 API** hello 다음 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="84476-121">Fill in name of hello application and select hello type of application as **WEB APPLICATION AND/OR WEB API** and click hello next button.</span></span>
   
     ![응용 프로그램 이름 지정][6]
8. <span data-ttu-id="84476-123">**로그인 URL** 및 **앱 ID URI**에 대한 더미 URL을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84476-123">You can provide any dummy URLs for **SIGN-ON URL** and **APP ID URI**.</span></span> <span data-ttu-id="84476-124">이 시나리오에 사용 되지 않는 및 자체 hello Url 유효성이 검사 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84476-124">They are not used for our scenario and hello URLs themselves are not validated.</span></span>  
   
     ![응용 프로그램 속성][7]
9. <span data-ttu-id="84476-126">이 hello 끝 hello 다음과 같이 이전에 제공한 hello 이름의 AAD 응용 프로그램 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84476-126">At hello end of this, you will have an AAD app with hello name you provided previously like hello following.</span></span> <span data-ttu-id="84476-127">이것이 **AD\_APP\_NAME**이며 메모해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="84476-127">This is your **AD\_APP\_NAME** and make a note of it.</span></span>  
   
     ![앱 이름][8]
10. <span data-ttu-id="84476-129">Hello 응용 프로그램 이름을 클릭 하 고 클릭 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="84476-129">Click on hello app name and click on **Configure**.</span></span>
    
      ![앱 구성][9]
11. <span data-ttu-id="84476-131">Hello로 사용 될 클라이언트 ID를 메모해 **클라이언트\_ID** API를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="84476-131">Make a note of hello CLIENT ID that will be used as **CLIENT\_ID** for your API calls.</span></span> 
    
     ![앱 구성][10]
12. <span data-ttu-id="84476-133">Toohello 아래로 스크롤하여 **키** 섹션 가급적 2 년 (만료) 기간을 사용 하 여 키를 추가 하 고 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="84476-133">Scroll down toohello **Keys** section and add a key with preferably 2 years (expiry) duration and click **Save**.</span></span> 
    
     ![앱 구성][11]
13. <span data-ttu-id="84476-135">즉시 hello 값 복사만 이제 표시 하는 저장 되지 않으므로 다시 표시 되지 것입니다 hello 키에 대 한 표시 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84476-135">Immediately copy hello value which is shown for hello key as it is only shown now and is not stored so will not be displayed ever again.</span></span> <span data-ttu-id="84476-136">분실 한 경우 다음 나면 toogenerate 새 키입니다.</span><span class="sxs-lookup"><span data-stu-id="84476-136">If you lose it then you will have toogenerate a new key.</span></span> <span data-ttu-id="84476-137">Hello 됩니다 **CLIENT_SECRET** API를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="84476-137">This will be hello **CLIENT_SECRET** for your API calls.</span></span> 
    
     ![앱 구성][12]
    
    > [!IMPORTANT]
    > <span data-ttu-id="84476-139">이 키는 hello 시간이 되 고, 그렇지 API 인증 하는 경우 더 이상 작동 하지 것입니다 너무 확인 되었는지 toorenew 지정한 hello 기간의 hello 끝에 만료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84476-139">This key will expire at hello end of hello duration that you specified so make sure toorenew it when hello time comes otherwise your API authentication will not work anymore.</span></span> <span data-ttu-id="84476-140">또한 손상되었다고 생각하는 경우 이 키를 삭제하고 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84476-140">You can also delete and recreate this key if you think that it has been compromised.</span></span>
    > 
    > 
14. <span data-ttu-id="84476-141">클릭 **끝점 보기** 이제 hello를 열 수 있는 단추 **앱 끝점** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="84476-141">Click on **VIEW ENDPOINTS** button now which will open up hello **App Endpoints** dialog box.</span></span> 
    
    ![][13]
15. <span data-ttu-id="84476-142">Hello 앱 끝점 대화 상자에서 복사 hello **OAUTH 2.0 토큰 끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="84476-142">From hello App Endpoints dialog box, copy hello **OAUTH 2.0 TOKEN ENDPOINT**.</span></span> 
    
    ![][14]
16. <span data-ttu-id="84476-143">이 끝점 hello hello hello URL의 GUID는 폼을 다음에 포함 될 프로그램 **TENANT_ID** 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="84476-143">This endpoint will be in hello following form where hello GUID in hello URL is your **TENANT_ID** so make a note of it:</span></span> 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. <span data-ttu-id="84476-144">이제이 응용 프로그램에 대 한 hello 권한을 tooconfigure 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84476-144">Now we will proceed tooconfigure hello permissions on this app.</span></span> <span data-ttu-id="84476-145">이 대 한 hello tooopen 갖습니다 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="84476-145">For this you will have tooopen up hello [Azure portal](https://portal.azure.com).</span></span> 
18. <span data-ttu-id="84476-146">클릭 **리소스 그룹** hello 및 **Mobile Engagement** 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="84476-146">Click on **Resource Groups** and find hello **Mobile Engagement** resource group.</span></span>  
    
    ![][15]
19. <span data-ttu-id="84476-147">Hello 클릭 **Mobile Engagement** 리소스 그룹화 하 고 탐색 toohello **설정** 블레이드 여기 합니다.</span><span class="sxs-lookup"><span data-stu-id="84476-147">Click hello **Mobile Engagement** resource group and navigate toohello **Settings** blade here.</span></span> 
    
    ![][16]
20. <span data-ttu-id="84476-148">클릭 **사용자** 설정 블레이드에서 hello와 클릭 **추가** tooadd 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="84476-148">Click on **Users** in hello Settings blade and then click on **Add** tooadd a user.</span></span> 
    
    ![][17]
21. <span data-ttu-id="84476-149">**역할 선택**</span><span class="sxs-lookup"><span data-stu-id="84476-149">Click on **Select a role**</span></span>
    
    ![][18]
22. <span data-ttu-id="84476-150">**소유자**</span><span class="sxs-lookup"><span data-stu-id="84476-150">Click on **Owner**</span></span>
    
    ![][19]
23. <span data-ttu-id="84476-151">응용 프로그램의 hello 이름에 대해 **AD\_앱\_이름** hello 검색 상자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84476-151">Search for hello name of your application **AD\_APP\_NAME** in hello Search box.</span></span> <span data-ttu-id="84476-152">여기에 기본적으로 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84476-152">You will not see this by default here.</span></span> <span data-ttu-id="84476-153">를 찾은 후 선택 하 고 클릭 **선택** hello hello 블레이드 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84476-153">Once you find it, select it and click on **Select** at hello bottom of hello blade.</span></span> 
    
    ![][20]
24. <span data-ttu-id="84476-154">Hello에 **액세스 추가** 블레이드에서 것으로 표시 됩니다 **사용자 1, 0 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="84476-154">On hello **Add Access** blade, it will show up as **1 user, 0 groups**.</span></span> <span data-ttu-id="84476-155">클릭 **확인** 이 블레이드 tooconfirm hello 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="84476-155">Click **OK** on this blade tooconfirm hello change.</span></span> 
    
    ![][21]

<span data-ttu-id="84476-156">필요한 hello AAD 구성을 완료 했으므로 되며 모든 집합 toocall hello Api 합니다.</span><span class="sxs-lookup"><span data-stu-id="84476-156">You have now completed hello required AAD configuration and you are all set toocall hello APIs.</span></span> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication-manual/active-directory.png
[2]: ./media/mobile-engagement-api-authentication-manual/active-directory-details.png
[3]: ./media/mobile-engagement-api-authentication-manual/view-applications.png
[4]: ./media/mobile-engagement-api-authentication-manual/add-icon.png
[5]: ./media/mobile-engagement-api-authentication-manual/what-do-you-want-to-do.png
[6]: ./media/mobile-engagement-api-authentication-manual/tell-us-about-your-application.png
[7]: ./media/mobile-engagement-api-authentication-manual/app-properties.png
[8]: ./media/mobile-engagement-api-authentication-manual/aad-app.png
[9]: ./media/mobile-engagement-api-authentication-manual/configure-menu.png
[10]: ./media/mobile-engagement-api-authentication-manual/client-id.png
[11]: ./media/mobile-engagement-api-authentication-manual/client_secret.png
[12]: ./media/mobile-engagement-api-authentication-manual/keys.png
[13]: ./media/mobile-engagement-api-authentication-manual/view-endpoints.png
[14]: ./media/mobile-engagement-api-authentication-manual/app-endpoints.png
[15]: ./media/mobile-engagement-api-authentication-manual/resource-groups.png
[16]: ./media/mobile-engagement-api-authentication-manual/resource-groups-settings.png
[17]: ./media/mobile-engagement-api-authentication-manual/add-users.png
[18]: ./media/mobile-engagement-api-authentication-manual/add-role.png
[19]: ./media/mobile-engagement-api-authentication-manual/select-role.png
[20]: ./media/mobile-engagement-api-authentication-manual/add-user-select.png
[21]: ./media/mobile-engagement-api-authentication-manual/add-access-final.png



