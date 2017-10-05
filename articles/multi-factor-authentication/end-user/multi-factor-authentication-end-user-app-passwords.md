---
title: "Azure MFA에서 앱 암호를 사용하는 방법 | Microsoft Docs"
description: "이 페이지는 사용자가 앱 암호란 무엇이며 Azure MFA와 관련해서 암호가 어떤 용도로 사용되는지를 이해하는 데 도움이 됩니다."
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
ms.openlocfilehash: fe8fb3b6e249fbe6bc0f8e55c4267f09cfcfcff5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a><span data-ttu-id="def13-104">Azure Multi-factor Authentication에서 앱 암호란 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="def13-104">What are App Passwords in Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="def13-105">Exchange Active Sync를 사용하는 Apple 네이티브 메일 클라이언트와 같은 특정 비브라우저 앱은 현재 다단계 인증을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="def13-105">Certain non-browser apps, such as the Apple native email client that uses Exchange Active Sync, currently do not support multi-factor authentication.</span></span> <span data-ttu-id="def13-106">다단계 인증은 사용자 기준으로 사용되도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="def13-106">Multi-factor authentication is enabled per user.</span></span> <span data-ttu-id="def13-107">즉, 다단계 인증을 사용할 수 있도록 설정된 사용자는 비브라우저 앱을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="def13-107">This means that if a user has been enabled for multi-factor authentication and they are attempting to use non-browser apps, they will be unable to do so.</span></span> <span data-ttu-id="def13-108">그렇지만 앱 암호를 사용하면 가능해집니다.</span><span class="sxs-lookup"><span data-stu-id="def13-108">An app password allows this to occur.</span></span>

<span data-ttu-id="def13-109">앱 암호를 만든 후 이러한 비브라우저 앱에서 원래 암호 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="def13-109">Once you have an app password, you use this in place of your original password with these non-browser apps.</span></span> <span data-ttu-id="def13-110">이는 2단계 인증을 위해 등록할 때 두 번째 인증을 수행할 수 없는 경우에도 누군가가 암호로 로그인하지 못하도록 Microsoft에 알리기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="def13-110">This is because when you register for two-step verification, you're telling Microsoft not to let anyone sign in with your password if they can't also perform the second verification.</span></span> <span data-ttu-id="def13-111">휴대폰의 Apple 네이티브 메일 클라이언트는 2단계 인증을 요청할 수 없기 때문에 로그인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="def13-111">The Apple native email client on your phone can't sign in as you because it can't ask for two-step verification.</span></span> <span data-ttu-id="def13-112">이에 대한 해결 방법은 일상적으로 사용하지 않는 보다 안전한 앱 암호를 만드는 것이지만 2단계 인증을 지원할 수 없는 앱에만 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="def13-112">The solution for this is to create a more secure app password that you don't use day-to-day, but only for those apps that can't support two-step verification.</span></span> <span data-ttu-id="def13-113">앱에서 다단계 인증을 우회하여 계속 작동하도록 앱 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-113">Use the app password so that apps can bypass multi-factor authentication and continue to work.</span></span>

> [!NOTE]
> <span data-ttu-id="def13-114">Outlook을 포함한 Office 2013 클라이언트는 새로운 인증 프로토콜을 지원하며 2단계 인증과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="def13-114">Office 2013 clients (including Outlook) support new authentication protocols and can be used with two-step verification.</span></span>  <span data-ttu-id="def13-115">즉, 일단 이렇게 설정되면 Office 2013 클라이언트에서 앱 암호를 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="def13-115">This means that once enabled, app passwords are not required for use with Office 2013 clients.</span></span>  <span data-ttu-id="def13-116">자세한 내용은 [발표된 Office 2013 최신 인증 공개 미리 보기](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="def13-116">For more information, see [Office 2013 modern authentication public preview announced](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span></span>


## <a name="how-to-use-app-passwords"></a><span data-ttu-id="def13-117">앱 암호를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="def13-117">How to use app passwords</span></span>
<span data-ttu-id="def13-118">다음은 앱 암호를 사용하는 방법과 관련해서 유의해야 할 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="def13-118">The following are some things to remember on how to use app passwords.</span></span>

* <span data-ttu-id="def13-119">사용자 고유의 앱 암호를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="def13-119">You don't create your own app passwords.</span></span> <span data-ttu-id="def13-120">대신 앱 암호는 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="def13-120">Instead, they are automatically generated.</span></span> <span data-ttu-id="def13-121">앱마다 앱 암호를 한 번만 입력하면 되므로 기억할 수 있는 암호를 만드는 것보다 더 복잡한 자동 생성 암호를 사용하는 것이 더 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-121">Since you only have to enter the app password once per app, it's safer to use a more complex, automatically generated password rather than making one that you can remember.</span></span>
* <span data-ttu-id="def13-122">현재 사용자 당 40개의 암호로 제한되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="def13-122">Currently there is a limit of 40 passwords per user.</span></span> <span data-ttu-id="def13-123">이 제한에 도달한 후에 만들려고 하면 기존 앱 암호 중 하나를 삭제해야 새로 만들 수 있다는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="def13-123">If you attempt to create one after you have reached the limit, you will be prompted to delete one of your existing app passwords before you create a new one.</span></span>
* <span data-ttu-id="def13-124">응용 프로그램 단위가 아니라 장치별로 앱 암호 하나만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-124">You should use one app password per device, not per application.</span></span> <span data-ttu-id="def13-125">예를 들어 노트북에 사용할 앱 암호를 하나 만든 다음 노트북의 모든 응용 프로그램에 이 앱 암호를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="def13-125">For example, you can create one app password for your laptop and use that app password for all of your applications on that laptop.</span></span> <span data-ttu-id="def13-126">그런 다음 바탕 화면에 있는 모든 앱에 사용할 두 번째 앱 암호를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="def13-126">Then, create a second app password to use for all your apps on your desktop.</span></span> 
* <span data-ttu-id="def13-127">처음으로 2단계 인증에 등록하면 앱 암호가 하나만 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="def13-127">You are given one app password the first time you register for two-step verification.</span></span>  <span data-ttu-id="def13-128">추가 암호가 필요한 경우 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="def13-128">If you need additional ones, you can create them.</span></span>



## <a name="creating-and-deleting-app-passwords"></a><span data-ttu-id="def13-129">앱 암호 만들기 및 삭제</span><span class="sxs-lookup"><span data-stu-id="def13-129">Creating and deleting app passwords</span></span>
<span data-ttu-id="def13-130">초기 로그인 중에 사용할 수 있는 앱 암호가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="def13-130">During your initial sign-in you are given an app password that you can use.</span></span>  <span data-ttu-id="def13-131">또한 나중에 앱 암호를 만들고 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="def13-131">Additionally you can also create and delete app passwords later on.</span></span>  <span data-ttu-id="def13-132">이 방법은 다단계 인증을 사용하는 방법에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="def13-132">How you do this depends on how you use multi-factor authentication.</span></span> <span data-ttu-id="def13-133">다음 질문에 대답하여 앱 암호를 관리해야 하는 위치를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-133">Answer the following questions to determine where you should go to manage app passwords:</span></span> 

1. <span data-ttu-id="def13-134">개인 Microsoft 계정에 대해 2단계 인증을 사용합니까?</span><span class="sxs-lookup"><span data-stu-id="def13-134">Do you use two-step verification for your personal Microsoft account?</span></span> <span data-ttu-id="def13-135">그렇다면 [앱 암호 및 2단계 인증](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) 문서를 참조하여 도움을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="def13-135">If yes, you should refer to the [App passwords and two-step verification](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) article for help.</span></span> <span data-ttu-id="def13-136">그렇지 않은 경우 2번 질문으로 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-136">If no, continue to question two.</span></span>

2. <span data-ttu-id="def13-137">이제 직장이나 학교 계정에 대해 2단계 인증을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-137">Ok, so you use two-step verification for your work or school account.</span></span> <span data-ttu-id="def13-138">Office 365 앱에 로그인하는 데 2단계 인증을 사용합니까?</span><span class="sxs-lookup"><span data-stu-id="def13-138">Do you use it to sign in to Office 365 apps?</span></span> <span data-ttu-id="def13-139">그렇다면 [Office 365용 앱 암호 만들기](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183)를 참조하여 도움을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="def13-139">If yes, you should refer to [Create an app password for Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) for help.</span></span> <span data-ttu-id="def13-140">그렇지 않은 경우 3번 질문으로 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-140">If no, continue to question three.</span></span> 

3. <span data-ttu-id="def13-141">Microsoft Azure에서 2단계 인증을 사용합니까?</span><span class="sxs-lookup"><span data-stu-id="def13-141">Do you use two-step verification with Microsoft Azure?</span></span> <span data-ttu-id="def13-142">그렇다면 이 문서의 [Azure Portal에서 앱 암호 관리](#manage-app-passwords-in-the-Azure-portal) 섹션에서 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-142">If yes, continue to the [Manage app passwords in the Azure portal](#manage-app-passwords-in-the-Azure-portal) section of this article.</span></span> <span data-ttu-id="def13-143">그렇지 않은 경우 4번 질문으로 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-143">If no, continue to question four.</span></span>

4. <span data-ttu-id="def13-144">2단계 인증을 사용하는 위치를 모르십니까?</span><span class="sxs-lookup"><span data-stu-id="def13-144">Not sure where you use two-step verification?</span></span> <span data-ttu-id="def13-145">이 문서의 [MyApps 포털에서 앱 암호 관리](#manage-app-passwords-with-the-myapps-portal) 섹션에서 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-145">Continue to the [Manage app passwords with the MyApps portal](#manage-app-passwords-with-the-myapps-portal) section of this article.</span></span> 


## <a name="manage-app-passwords-in-the-azure-portal"></a><span data-ttu-id="def13-146">Azure Portal에서 앱 암호 관리</span><span class="sxs-lookup"><span data-stu-id="def13-146">Manage app passwords in the Azure portal</span></span>
<span data-ttu-id="def13-147">Azure에서 2단계 인증을 사용하는 경우 Azure Portal을 통해 앱 암호를 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-147">If you use two-step verification with Azure, you want to create app passwords through the Azure portal.</span></span>

### <a name="to-create-app-passwords-in-the-azure-portal"></a><span data-ttu-id="def13-148">Azure 포털에서 앱 암호를 만들려면</span><span class="sxs-lookup"><span data-stu-id="def13-148">To create app passwords in the Azure portal</span></span>
1. <span data-ttu-id="def13-149">Azure 클래식 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-149">Sign in to the Azure classic portal.</span></span>
2. <span data-ttu-id="def13-150">위쪽에서 사용자 이름을 마우스 오른쪽 단추로 클릭하고 [추가 보안 인증]을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-150">At the top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="def13-151">검사 페이지 위쪽에서 앱 암호를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-151">On the proofup page, at the top, select app passwords</span></span>
4. <span data-ttu-id="def13-152">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-152">Click **Create**.</span></span>
5. <span data-ttu-id="def13-153">앱 암호의 이름을 입력하고 **다음**</span><span class="sxs-lookup"><span data-stu-id="def13-153">Enter a name for the app password and click **Next**</span></span>
6. <span data-ttu-id="def13-154">앱 암호를 클립보드에 복사하고 앱에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="def13-154">Copy the app password to the clipboard and paste it into your app.</span></span>
   
   ![클라우드](./media/multi-factor-authentication-end-user-app-passwords/app2.png)


### <a name="to-delete-app-passwords-in-the-azure-portal"></a><span data-ttu-id="def13-156">Azure 포털에서 앱 암호를 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="def13-156">To delete app passwords in the Azure portal</span></span>
1. <span data-ttu-id="def13-157">Azure 클래식 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-157">Sign in to the Azure classic portal.</span></span>
2. <span data-ttu-id="def13-158">위쪽에서 사용자 이름을 마우스 오른쪽 단추로 클릭하고 [추가 보안 인증]을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-158">At the top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="def13-159">위쪽에서 [추가 보안 인증] 옆에 있는 **앱 암호**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-159">At the top, next to additional security verification, select **app passwords.**</span></span>
4. <span data-ttu-id="def13-160">삭제할 앱 암호 옆에 있는 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-160">Next to the app password you want to delete, select **Delete**.</span></span>
5. <span data-ttu-id="def13-161">**예**를 클릭하여 삭제를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-161">Confirm the deletion by clicking **yes**.</span></span>
6. <span data-ttu-id="def13-162">앱 암호가 삭제되면 **닫기**를 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="def13-162">Once the app password is deleted, you can click **close**.</span></span>


## <a name="manage-app-passwords-with-the-myapps-portal"></a><span data-ttu-id="def13-163">MyApps 포털에서 앱 암호 관리</span><span class="sxs-lookup"><span data-stu-id="def13-163">Manage app passwords with the MyApps portal.</span></span>
<span data-ttu-id="def13-164">다단계 인증을 사용하는 방법을 잘 모르는 경우 MyApps 포털을 통해 언제든지 앱 암호를 만들고 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="def13-164">If you are not sure how you use multi-factor authentication, then you can always create and delete app passwords through the myapps portal.</span></span>

### <a name="to-create-an-app-password-using-the-myapps-portal"></a><span data-ttu-id="def13-165">Myapps 포털을 사용하여 앱 암호를 만들려면</span><span class="sxs-lookup"><span data-stu-id="def13-165">To create an app password using the Myapps portal</span></span>
1. <span data-ttu-id="def13-166">[https://myapps.microsoft.com](https://myapps.microsoft.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-166">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="def13-167">오른쪽 위에서 이름을 클릭하고 **프로필**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-167">Click your name at the top right, and choose **Profile**.</span></span>
3. <span data-ttu-id="def13-168">**추가 보안 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-168">Select **Additional Security Verification**.</span></span>
   <span data-ttu-id="def13-169">![추가 보안 인증 선택 - 스크린샷](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span><span class="sxs-lookup"><span data-stu-id="def13-169">![Select additional security verification - screenshot](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span></span>

4. <span data-ttu-id="def13-170">**앱 암호**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-170">Select **app passwords**.</span></span>
   <span data-ttu-id="def13-171">![앱 암호 선택 - 스크린샷](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span><span class="sxs-lookup"><span data-stu-id="def13-171">![Select app passwords - screenshot](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span></span>

5. <span data-ttu-id="def13-172">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-172">Click **Create**.</span></span>
6. <span data-ttu-id="def13-173">앱 암호의 이름을 입력하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-173">Enter a name for the app password and click **Next**.</span></span>
7. <span data-ttu-id="def13-174">앱 암호를 클립보드에 복사하고 앱에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="def13-174">Copy the app password to the clipboard and paste it into your app.</span></span>
   <span data-ttu-id="def13-175">![앱 암호 만들기](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span><span class="sxs-lookup"><span data-stu-id="def13-175">![Create an app password](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span></span>

### <a name="to-delete-an-app-password-using-the-myapps-portal"></a><span data-ttu-id="def13-176">Myapps 포털을 사용하여 앱 암호를 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="def13-176">To delete an app password using the Myapps portal</span></span>
1. <span data-ttu-id="def13-177">[https://myapps.microsoft.com](https://myapps.microsoft.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-177">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="def13-178">위쪽에서 프로필을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-178">At the top, select profile.</span></span>
3. <span data-ttu-id="def13-179">**추가 보안 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-179">Select **Additional Security Verification**.</span></span>

   ![추가 보안 인증 선택 - 스크린샷](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. <span data-ttu-id="def13-181">**앱 암호**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-181">Select **app passwords**.</span></span>

   ![앱 암호 선택 - 스크린샷](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. <span data-ttu-id="def13-183">제거할 앱 암호 옆에 있는 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-183">Next to the app password you want to delete, click **Delete**.</span></span>

   ![앱 암호 삭제](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. <span data-ttu-id="def13-185">**예**를 클릭하여 암호를 삭제할 것인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-185">Confirm that you want to delete that password by clicking **yes**.</span></span>
7. <span data-ttu-id="def13-186">앱 암호가 삭제되면 **닫기**를 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="def13-186">Once the app password is deleted, you can click **close**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="def13-187">다음 단계</span><span class="sxs-lookup"><span data-stu-id="def13-187">Next steps</span></span>

- [<span data-ttu-id="def13-188">2단계 인증 설정 관리</span><span class="sxs-lookup"><span data-stu-id="def13-188">Manage your two-step verification settings</span></span>](multi-factor-authentication-end-user-manage-settings.md)

- <span data-ttu-id="def13-189">[Microsoft Authenticator 앱](microsoft-authenticator-app-how-to.md)을 사용하여 텍스트 또는 전화를 받는 대신 앱 알림으로 로그인을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="def13-189">Try out the [Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) to verify your sign-ins with app notifications, instead of receiving texts or calls.</span></span> 
