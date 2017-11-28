---
title: "aaaHow toouse Azure MFA에서 앱 암호? | Microsoft Docs"
description: "이 페이지에 앱 암호 및 무엇 인지에 대해 설명 하는 사용자가 도움이 될 큰지에 tooAzure MFA에 사용 합니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 345b757b-5a2b-48eb-953f-d363313be9e5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: bf2c11edc0ca81f2950eff0f7a3a24c8a5b34623
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a><span data-ttu-id="489e3-104">Azure Multi-factor Authentication에서 앱 암호란 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="489e3-104">What are App Passwords in Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="489e3-105">현재 Exchange Active Sync를 사용 하는 hello Apple 네이티브 메일 클라이언트와 같은 특정 비 브라우저 앱은 다단계 인증을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-105">Certain non-browser apps, such as hello Apple native email client that uses Exchange Active Sync, currently do not support multi-factor authentication.</span></span> <span data-ttu-id="489e3-106">다단계 인증은 사용자 기준으로 사용되도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-106">Multi-factor authentication is enabled per user.</span></span> <span data-ttu-id="489e3-107">이 사용자가 multi-factor authentication에 대해 활성화 된 toouse 비 브라우저 앱이 하려고 하는 경우는 것 toodo 수 없습니다 따라서 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-107">This means that if a user has been enabled for multi-factor authentication and they are attempting toouse non-browser apps, they will be unable toodo so.</span></span> <span data-ttu-id="489e3-108">앱 암호에는이 toooccur 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-108">An app password allows this toooccur.</span></span>

<span data-ttu-id="489e3-109">앱 암호를 만든 후 이러한 비브라우저 앱에서 원래 암호 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-109">Once you have an app password, you use this in place of your original password with these non-browser apps.</span></span> <span data-ttu-id="489e3-110">Hello 두 번째 확인을 수행할 수도 수 없는 경우 암호를 사용 하 여 Microsoft 모든 사용자가 로그인 toolet 하지을 지시 하는 2 단계 인증을 등록 하면 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-110">This is because when you register for two-step verification, you're telling Microsoft not toolet anyone sign in with your password if they can't also perform hello second verification.</span></span> <span data-ttu-id="489e3-111">휴대폰에서 hello Apple 네이티브 메일 클라이언트 로그인 할 수 없습니다와 2 단계 인증을 요청할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-111">hello Apple native email client on your phone can't sign in as you because it can't ask for two-step verification.</span></span> <span data-ttu-id="489e3-112">hello이 방법은 사용 하지 않는 좀 더 안전한 앱 암호 toocreate 일상적인, 하지만 2 단계 인증을 지원 하지 못하는 이러한 앱에 대해서만 합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-112">hello solution for this is toocreate a more secure app password that you don't use day-to-day, but only for those apps that can't support two-step verification.</span></span> <span data-ttu-id="489e3-113">앱에서 multi-factor authentication을 바이패스 하 고 toowork 계속할 수 있도록 hello 앱 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-113">Use hello app password so that apps can bypass multi-factor authentication and continue toowork.</span></span>

> [!NOTE]
> <span data-ttu-id="489e3-114">Outlook을 포함한 Office 2013 클라이언트는 새로운 인증 프로토콜을 지원하며 2단계 인증과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-114">Office 2013 clients (including Outlook) support new authentication protocols and can be used with two-step verification.</span></span>  <span data-ttu-id="489e3-115">즉, 일단 이렇게 설정되면 Office 2013 클라이언트에서 앱 암호를 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-115">This means that once enabled, app passwords are not required for use with Office 2013 clients.</span></span>  <span data-ttu-id="489e3-116">자세한 내용은 [발표된 Office 2013 최신 인증 공개 미리 보기](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="489e3-116">For more information, see [Office 2013 modern authentication public preview announced](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span></span>


## <a name="how-toouse-app-passwords"></a><span data-ttu-id="489e3-117">어떻게 toouse 앱 암호</span><span class="sxs-lookup"><span data-stu-id="489e3-117">How toouse app passwords</span></span>
<span data-ttu-id="489e3-118">hello는 다음과 같은 방법에 일부의 tooremember toouse 앱 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-118">hello following are some things tooremember on how toouse app passwords.</span></span>

* <span data-ttu-id="489e3-119">사용자 고유의 앱 암호를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-119">You don't create your own app passwords.</span></span> <span data-ttu-id="489e3-120">대신 앱 암호는 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-120">Instead, they are automatically generated.</span></span> <span data-ttu-id="489e3-121">앱 당 한 번씩만 tooenter hello 앱 암호에만 한 대신 것이 더 안전 하 게 toouse 더 복잡 한, 자동으로 생성 된 암호를 기억할 수 있는 하나를 만들어 합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-121">Since you only have tooenter hello app password once per app, it's safer toouse a more complex, automatically generated password rather than making one that you can remember.</span></span>
* <span data-ttu-id="489e3-122">현재 사용자 당 40개의 암호로 제한되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-122">Currently there is a limit of 40 passwords per user.</span></span> <span data-ttu-id="489e3-123">Hello 제한에 도달한 후 toocreate 하나를 시도 하면 새를 만들기 전에 기존 앱 암호 중 하나는 메시지 표시 toodelete 됩니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-123">If you attempt toocreate one after you have reached hello limit, you will be prompted toodelete one of your existing app passwords before you create a new one.</span></span>
* <span data-ttu-id="489e3-124">응용 프로그램 단위가 아니라 장치별로 앱 암호 하나만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-124">You should use one app password per device, not per application.</span></span> <span data-ttu-id="489e3-125">예를 들어 노트북에 사용할 앱 암호를 하나 만든 다음 노트북의 모든 응용 프로그램에 이 앱 암호를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-125">For example, you can create one app password for your laptop and use that app password for all of your applications on that laptop.</span></span> <span data-ttu-id="489e3-126">그런 다음 모든 앱에 대 한 두 번째 응용 프로그램 암호 toouse를 바탕 화면에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-126">Then, create a second app password toouse for all your apps on your desktop.</span></span> 
* <span data-ttu-id="489e3-127">처음 등록할 때 2 단계 인증에 대 한 하나의 앱 암호 hello를 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-127">You are given one app password hello first time you register for two-step verification.</span></span>  <span data-ttu-id="489e3-128">추가 암호가 필요한 경우 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-128">If you need additional ones, you can create them.</span></span>



## <a name="creating-and-deleting-app-passwords"></a><span data-ttu-id="489e3-129">앱 암호 만들기 및 삭제</span><span class="sxs-lookup"><span data-stu-id="489e3-129">Creating and deleting app passwords</span></span>
<span data-ttu-id="489e3-130">초기 로그인 중에 사용할 수 있는 앱 암호가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-130">During your initial sign-in you are given an app password that you can use.</span></span>  <span data-ttu-id="489e3-131">또한 나중에 앱 암호를 만들고 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-131">Additionally you can also create and delete app passwords later on.</span></span>  <span data-ttu-id="489e3-132">이 방법은 다단계 인증을 사용하는 방법에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-132">How you do this depends on how you use multi-factor authentication.</span></span> <span data-ttu-id="489e3-133">다음 응답 hello toomanage 앱 암호를 어디로 해야 toodetermine 관련 질문:</span><span class="sxs-lookup"><span data-stu-id="489e3-133">Answer hello following questions toodetermine where you should go toomanage app passwords:</span></span> 

1. <span data-ttu-id="489e3-134">개인 Microsoft 계정에 대해 2단계 인증을 사용합니까?</span><span class="sxs-lookup"><span data-stu-id="489e3-134">Do you use two-step verification for your personal Microsoft account?</span></span> <span data-ttu-id="489e3-135">그렇다면 toohello 참조 해야 [앱 암호와 2 단계 인증](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) 문서에 대 한 도움말입니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-135">If yes, you should refer toohello [App passwords and two-step verification](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) article for help.</span></span> <span data-ttu-id="489e3-136">그렇지 않은 경우, 두 tooquestion을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-136">If no, continue tooquestion two.</span></span>

2. <span data-ttu-id="489e3-137">이제 직장이나 학교 계정에 대해 2단계 인증을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-137">Ok, so you use two-step verification for your work or school account.</span></span> <span data-ttu-id="489e3-138">사용 합니까 것 toosign tooOffice 365 앱에서?</span><span class="sxs-lookup"><span data-stu-id="489e3-138">Do you use it toosign in tooOffice 365 apps?</span></span> <span data-ttu-id="489e3-139">그러한 경우를 참조 해야 너무[Office 365에 대 한 앱 암호를 만들](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) 에 대 한 도움말입니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-139">If yes, you should refer too[Create an app password for Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) for help.</span></span> <span data-ttu-id="489e3-140">그렇지 않은 경우, 3 tooquestion를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-140">If no, continue tooquestion three.</span></span> 

3. <span data-ttu-id="489e3-141">Microsoft Azure에서 2단계 인증을 사용합니까?</span><span class="sxs-lookup"><span data-stu-id="489e3-141">Do you use two-step verification with Microsoft Azure?</span></span> <span data-ttu-id="489e3-142">그러한 경우 계속 toohello [hello Azure 포털에서에서 앱 암호를 관리](#manage-app-passwords-in-the-Azure-portal) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="489e3-142">If yes, continue toohello [Manage app passwords in hello Azure portal](#manage-app-passwords-in-the-Azure-portal) section of this article.</span></span> <span data-ttu-id="489e3-143">그렇지 않은 경우, tooquestion 4를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-143">If no, continue tooquestion four.</span></span>

4. <span data-ttu-id="489e3-144">2단계 인증을 사용하는 위치를 모르십니까?</span><span class="sxs-lookup"><span data-stu-id="489e3-144">Not sure where you use two-step verification?</span></span> <span data-ttu-id="489e3-145">Toohello 계속 [hello MyApps 포털과 응용 프로그램 암호 관리](#manage-app-passwords-with-the-myapps-portal) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="489e3-145">Continue toohello [Manage app passwords with hello MyApps portal](#manage-app-passwords-with-the-myapps-portal) section of this article.</span></span> 


## <a name="manage-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="489e3-146">Hello Azure 포털에서에서 앱 암호를 관리</span><span class="sxs-lookup"><span data-stu-id="489e3-146">Manage app passwords in hello Azure portal</span></span>
<span data-ttu-id="489e3-147">Azure를 사용한 2 단계 인증을 사용 하는 경우 원하는 hello Azure 포털을 통해 toocreate 앱 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-147">If you use two-step verification with Azure, you want toocreate app passwords through hello Azure portal.</span></span>

### <a name="toocreate-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="489e3-148">hello Azure 포털에서에서 toocreate 앱 암호</span><span class="sxs-lookup"><span data-stu-id="489e3-148">toocreate app passwords in hello Azure portal</span></span>
1. <span data-ttu-id="489e3-149">Azure 클래식 포털 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-149">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="489e3-150">Hello 위쪽에 사용자 이름을 마우스 오른쪽 단추로 클릭 하 고 추가 보안 확인을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-150">At hello top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="489e3-151">Hello 위쪽에, hello 검사 페이지에서 앱 암호를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-151">On hello proofup page, at hello top, select app passwords</span></span>
4. <span data-ttu-id="489e3-152">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-152">Click **Create**.</span></span>
5. <span data-ttu-id="489e3-153">Hello 앱 암호에 대 한 이름을 입력 하 고 클릭 **다음**</span><span class="sxs-lookup"><span data-stu-id="489e3-153">Enter a name for hello app password and click **Next**</span></span>
6. <span data-ttu-id="489e3-154">Hello 앱 암호 toohello 클립보드로 복사한 응용 프로그램에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-154">Copy hello app password toohello clipboard and paste it into your app.</span></span>
   
   ![클라우드](./media/multi-factor-authentication-end-user-app-passwords/app2.png)


### <a name="toodelete-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="489e3-156">hello Azure 포털에서에서 toodelete 앱 암호</span><span class="sxs-lookup"><span data-stu-id="489e3-156">toodelete app passwords in hello Azure portal</span></span>
1. <span data-ttu-id="489e3-157">Azure 클래식 포털 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-157">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="489e3-158">Hello 위쪽에 사용자 이름을 마우스 오른쪽 단추로 클릭 하 고 추가 보안 확인을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-158">At hello top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="489e3-159">다음 tooadditional 보안 확인 hello 위쪽 선택 **앱 암호입니다.**</span><span class="sxs-lookup"><span data-stu-id="489e3-159">At hello top, next tooadditional security verification, select **app passwords.**</span></span>
4. <span data-ttu-id="489e3-160">다음 toohello 앱 암호 toodelete, 원하는 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-160">Next toohello app password you want toodelete, select **Delete**.</span></span>
5. <span data-ttu-id="489e3-161">클릭 하 여 hello 삭제를 확인 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-161">Confirm hello deletion by clicking **yes**.</span></span>
6. <span data-ttu-id="489e3-162">Hello 앱 암호를 삭제 한 후 클릭할 수 있는 **닫습니다**합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-162">Once hello app password is deleted, you can click **close**.</span></span>


## <a name="manage-app-passwords-with-hello-myapps-portal"></a><span data-ttu-id="489e3-163">Hello MyApps 포털과 앱 암호를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-163">Manage app passwords with hello MyApps portal.</span></span>
<span data-ttu-id="489e3-164">다단계 인증을 사용 하는 방법을 확실 하지 않은 경우 다음 수 항상 만들고 hello myapps 포털을 통해 앱 암호 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-164">If you are not sure how you use multi-factor authentication, then you can always create and delete app passwords through hello myapps portal.</span></span>

### <a name="toocreate-an-app-password-using-hello-myapps-portal"></a><span data-ttu-id="489e3-165">사용 하 여 앱 암호 toocreate hello Myapps 포털</span><span class="sxs-lookup"><span data-stu-id="489e3-165">toocreate an app password using hello Myapps portal</span></span>
1. <span data-ttu-id="489e3-166">역시 로그인[https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="489e3-166">Sign in too[https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="489e3-167">Hello 위쪽, 오른쪽에 있는 사용자 이름을 클릭 하 고 선택 **프로필**합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-167">Click your name at hello top right, and choose **Profile**.</span></span>
3. <span data-ttu-id="489e3-168">**추가 보안 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-168">Select **Additional Security Verification**.</span></span>
   <span data-ttu-id="489e3-169">![추가 보안 인증 선택 - 스크린샷](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span><span class="sxs-lookup"><span data-stu-id="489e3-169">![Select additional security verification - screenshot](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span></span>

4. <span data-ttu-id="489e3-170">**앱 암호**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-170">Select **app passwords**.</span></span>
   <span data-ttu-id="489e3-171">![앱 암호 선택 - 스크린샷](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span><span class="sxs-lookup"><span data-stu-id="489e3-171">![Select app passwords - screenshot](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span></span>

5. <span data-ttu-id="489e3-172">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-172">Click **Create**.</span></span>
6. <span data-ttu-id="489e3-173">Hello 앱 암호에 대 한 이름을 입력 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-173">Enter a name for hello app password and click **Next**.</span></span>
7. <span data-ttu-id="489e3-174">Hello 앱 암호 toohello 클립보드로 복사한 응용 프로그램에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-174">Copy hello app password toohello clipboard and paste it into your app.</span></span>
   <span data-ttu-id="489e3-175">![앱 암호 만들기](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span><span class="sxs-lookup"><span data-stu-id="489e3-175">![Create an app password](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span></span>

### <a name="toodelete-an-app-password-using-hello-myapps-portal"></a><span data-ttu-id="489e3-176">사용 하 여 앱 암호 toodelete hello Myapps 포털</span><span class="sxs-lookup"><span data-stu-id="489e3-176">toodelete an app password using hello Myapps portal</span></span>
1. <span data-ttu-id="489e3-177">역시 로그인[https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="489e3-177">Sign in too[https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="489e3-178">Hello 위쪽에, 프로필을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-178">At hello top, select profile.</span></span>
3. <span data-ttu-id="489e3-179">**추가 보안 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-179">Select **Additional Security Verification**.</span></span>

   ![추가 보안 인증 선택 - 스크린샷](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. <span data-ttu-id="489e3-181">**앱 암호**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-181">Select **app passwords**.</span></span>

   ![앱 암호 선택 - 스크린샷](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. <span data-ttu-id="489e3-183">다음 toohello 앱 암호 toodelete, 원하는 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-183">Next toohello app password you want toodelete, click **Delete**.</span></span>

   ![앱 암호 삭제](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. <span data-ttu-id="489e3-185">것인지 확인 하는 toodelete 해당 암호를 클릭 하 여 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-185">Confirm that you want toodelete that password by clicking **yes**.</span></span>
7. <span data-ttu-id="489e3-186">Hello 앱 암호를 삭제 한 후 클릭할 수 있는 **닫습니다**합니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-186">Once hello app password is deleted, you can click **close**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="489e3-187">다음 단계</span><span class="sxs-lookup"><span data-stu-id="489e3-187">Next steps</span></span>

- [<span data-ttu-id="489e3-188">2단계 인증 설정 관리</span><span class="sxs-lookup"><span data-stu-id="489e3-188">Manage your two-step verification settings</span></span>](multi-factor-authentication-end-user-manage-settings.md)

- <span data-ttu-id="489e3-189">Hello 사용해 [Microsoft Authenticator 앱](microsoft-authenticator-app-how-to.md) tooverify 사용자 로그인을 대신 텍스트 또는 호출 응용 프로그램 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="489e3-189">Try out hello [Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) tooverify your sign-ins with app notifications, instead of receiving texts or calls.</span></span> 
