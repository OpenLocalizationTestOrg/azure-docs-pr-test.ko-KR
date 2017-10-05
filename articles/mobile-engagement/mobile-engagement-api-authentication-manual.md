---
title: "Mobile Engagement REST API를 사용한 인증 - 수동 설치"
description: "Mobile Engagement REST API에 대한 인증을 수동으로 설정하는 방법을 설명합니다."
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
ms.openlocfilehash: 9d6132e1a01be489b8e8e28a0219cf8a0b50b318
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a><span data-ttu-id="bcaa1-103">Mobile Engagement REST API를 사용한 인증 - 수동 설치</span><span class="sxs-lookup"><span data-stu-id="bcaa1-103">Authenticate with Mobile Engagement REST APIs - manual setup</span></span>
<span data-ttu-id="bcaa1-104">이 부록 설명서는 [Mobile Engagement REST API를 사용한 인증](mobile-engagement-api-authentication.md)을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-104">This is an appendix documentation to [Authenticate with Mobile Engagement REST APIs](mobile-engagement-api-authentication.md).</span></span> <span data-ttu-id="bcaa1-105">먼저 읽고 상황을 파악하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-105">Make sure you read it first to get the context.</span></span> <span data-ttu-id="bcaa1-106">Azure 포털을 사용하여 Mobile Engagement REST API에 대한 인증을 설정하기 위해 일회성 설치 프로세스를 수행하는 대체 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-106">This describes an alternate way to do the One-time setup for setting up your authentication for the Mobile Engagement REST APIs using the Azure Portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="bcaa1-107">아래 지침은 [Active Directory 가이드](../azure-resource-manager/resource-group-create-service-principal-portal.md) 를 기반으로 하며 Mobile Engagement API에 대한 인증을 위해 필요한 항목을 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-107">The instructions below are based on this [Active Directory guide](../azure-resource-manager/resource-group-create-service-principal-portal.md) and customized for what is required for authentication for Mobile Engagement APIs.</span></span> <span data-ttu-id="bcaa1-108">따라서 아래 단계를 자세히 이해하려면 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-108">So refer to it if you want to understand the steps below in detail.</span></span> 
> 
> 

1. <span data-ttu-id="bcaa1-109">[클래식 포털](https://manage.windowsazure.com/)을 통해 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-109">Login to your Azure Account through the [classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="bcaa1-110">왼쪽 창에서 **Active Directory** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-110">Select **Active Directory** from the left pane.</span></span>
   
     ![Active Directory 선택][1]
3. <span data-ttu-id="bcaa1-112">Azure 포털에서 **기본 Active Directory** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-112">Choose the **Default Active Directory** in your Azure portal.</span></span> 
   
     ![디렉터리 선택][2]
   
   > [!IMPORTANT]
   > <span data-ttu-id="bcaa1-114">이 방법은 사용자 계정의 기본 Active Directory에서 작업할 경우 작동하며 사용자가 계정에 만든 Active Directory에서 수행하는 경우 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-114">This approach works only when you are working in the default Active Directory of your account and will not work if you are doing this in an Active Directory that you have created in your account.</span></span> 
   > 
   > 
4. <span data-ttu-id="bcaa1-115">디렉터리에서 응용 프로그램을 보려면 **응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-115">To view the applications in your directory, click on **Applications**.</span></span>
   
     ![응용 프로그램 보기][3]
5. <span data-ttu-id="bcaa1-117">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-117">Click on **ADD**.</span></span> 
   
     ![응용 프로그램 추가][4]
6. <span data-ttu-id="bcaa1-119">**내 조직에서 개발 중인 응용 프로그램 추가**</span><span class="sxs-lookup"><span data-stu-id="bcaa1-119">Click on **Add an application my organization is developing**</span></span>
   
     ![새 응용 프로그램][5]
7. <span data-ttu-id="bcaa1-121">응용 프로그램의 이름을 입력하고 응용 프로그램의 유형을 **웹 응용 프로그램 및/또는 웹 API** 로 선택하고 다음 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-121">Fill in name of the application and select the type of application as **WEB APPLICATION AND/OR WEB API** and click the next button.</span></span>
   
     ![응용 프로그램 이름 지정][6]
8. <span data-ttu-id="bcaa1-123">**로그인 URL** 및 **앱 ID URI**에 대한 더미 URL을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-123">You can provide any dummy URLs for **SIGN-ON URL** and **APP ID URI**.</span></span> <span data-ttu-id="bcaa1-124">이것은 시나리오에 사용되지 않고 URL 자체의 유효성도 검사되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-124">They are not used for our scenario and the URLs themselves are not validated.</span></span>  
   
     ![응용 프로그램 속성][7]
9. <span data-ttu-id="bcaa1-126">이 단계가 끝나면 다음과 같이 이전에 제공한 이름을 가진 AAD 앱이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-126">At the end of this, you will have an AAD app with the name you provided previously like the following.</span></span> <span data-ttu-id="bcaa1-127">이것이 **AD\_APP\_NAME**이며 메모해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-127">This is your **AD\_APP\_NAME** and make a note of it.</span></span>  
   
     ![앱 이름][8]
10. <span data-ttu-id="bcaa1-129">앱 이름을 클릭하고 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-129">Click on the app name and click on **Configure**.</span></span>
    
      ![앱 구성][9]
11. <span data-ttu-id="bcaa1-131">API 호출에 **CLIENT\_ID**로 사용할 수 있는 클라이언트 ID를 메모해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-131">Make a note of the CLIENT ID that will be used as **CLIENT\_ID** for your API calls.</span></span> 
    
     ![앱 구성][10]
12. <span data-ttu-id="bcaa1-133">**키** 섹션으로 스크롤하고 가급적이면 2년(만료) 기간인 키를 추가하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-133">Scroll down to the **Keys** section and add a key with preferably 2 years (expiry) duration and click **Save**.</span></span> 
    
     ![앱 구성][11]
13. <span data-ttu-id="bcaa1-135">지금 표시되고 저장되지 않아서 다시 표시되지 않으므로 표시된 키에 대한 값을 즉시 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-135">Immediately copy the value which is shown for the key as it is only shown now and is not stored so will not be displayed ever again.</span></span> <span data-ttu-id="bcaa1-136">분실한 경우 새 키를 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-136">If you lose it then you will have to generate a new key.</span></span> <span data-ttu-id="bcaa1-137">API 호출에 대한 **CLIENT_SECRET**입니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-137">This will be the **CLIENT_SECRET** for your API calls.</span></span> 
    
     ![앱 구성][12]
    
    > [!IMPORTANT]
    > <span data-ttu-id="bcaa1-139">이 키는 지정한 기간 후에 만료 됩니다. 따라서 기간이 되어 갱신하지 않으면 API 인증은 더 이상 작동하지 않습니다. </span><span class="sxs-lookup"><span data-stu-id="bcaa1-139">This key will expire at the end of the duration that you specified so make sure to renew it when the time comes otherwise your API authentication will not work anymore.</span></span> <span data-ttu-id="bcaa1-140">또한 손상되었다고 생각하는 경우 이 키를 삭제하고 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-140">You can also delete and recreate this key if you think that it has been compromised.</span></span>
    > 
    > 
14. <span data-ttu-id="bcaa1-141">**끝점 보기** 단추를 클릭하면 **앱 끝점** 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-141">Click on **VIEW ENDPOINTS** button now which will open up the **App Endpoints** dialog box.</span></span> 
    
    ![][13]
15. <span data-ttu-id="bcaa1-142">앱 끝점 대화 상자에서 **OAUTH 2.0 토큰 끝점**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-142">From the App Endpoints dialog box, copy the **OAUTH 2.0 TOKEN ENDPOINT**.</span></span> 
    
    ![][14]
16. <span data-ttu-id="bcaa1-143">이 끝점은 URL의 GUID가 **TENANT_ID**인 다음과 같은 형식입니다. 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-143">This endpoint will be in the following form where the GUID in the URL is your **TENANT_ID** so make a note of it:</span></span> 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. <span data-ttu-id="bcaa1-144">이제 이 앱에 권한을 구성하도록 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-144">Now we will proceed to configure the permissions on this app.</span></span> <span data-ttu-id="bcaa1-145">이를 위해 [Azure 포털](https://portal.azure.com)을 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-145">For this you will have to open up the [Azure portal](https://portal.azure.com).</span></span> 
18. <span data-ttu-id="bcaa1-146">**리소스 그룹**을 열고 **Mobile Engagement** 리소스 그룹을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-146">Click on **Resource Groups** and find the **Mobile Engagement** resource group.</span></span>  
    
    ![][15]
19. <span data-ttu-id="bcaa1-147">**Mobile Engagement** 리소스 그룹을 찾고 거기서 **설정** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-147">Click the **Mobile Engagement** resource group and navigate to the **Settings** blade here.</span></span> 
    
    ![][16]
20. <span data-ttu-id="bcaa1-148">설정 블레이드에서 **사용자**를 클릭하고 **추가**를 클릭하여 사용자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-148">Click on **Users** in the Settings blade and then click on **Add** to add a user.</span></span> 
    
    ![][17]
21. <span data-ttu-id="bcaa1-149">**역할 선택**</span><span class="sxs-lookup"><span data-stu-id="bcaa1-149">Click on **Select a role**</span></span>
    
    ![][18]
22. <span data-ttu-id="bcaa1-150">**소유자**</span><span class="sxs-lookup"><span data-stu-id="bcaa1-150">Click on **Owner**</span></span>
    
    ![][19]
23. <span data-ttu-id="bcaa1-151">검색 상자에서 응용 프로그램 **AD\_APP\_NAME**의 이름을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-151">Search for the name of your application **AD\_APP\_NAME** in the Search box.</span></span> <span data-ttu-id="bcaa1-152">여기에 기본적으로 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-152">You will not see this by default here.</span></span> <span data-ttu-id="bcaa1-153">찾게 되면 선택하고 블레이드 맨 아래에서 **선택** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-153">Once you find it, select it and click on **Select** at the bottom of the blade.</span></span> 
    
    ![][20]
24. <span data-ttu-id="bcaa1-154">**액세스 추가** 블레이드에서 **1 사용자, 0 그룹**으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-154">On the **Add Access** blade, it will show up as **1 user, 0 groups**.</span></span> <span data-ttu-id="bcaa1-155">이 블레이드에서 **확인** 을 클릭하여 변경 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-155">Click **OK** on this blade to confirm the change.</span></span> 
    
    ![][21]

<span data-ttu-id="bcaa1-156">필요한 AAD 구성을 완료했으므로 API를 호출하도록 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bcaa1-156">You have now completed the required AAD configuration and you are all set to call the APIs.</span></span> 

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



