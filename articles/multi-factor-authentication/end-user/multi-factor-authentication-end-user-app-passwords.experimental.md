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
ms.openlocfilehash: 1ecc2bdef5ff7ef8ed8dded7dc12428ce9657821
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a><span data-ttu-id="0f8b5-104">Azure Multi-factor Authentication에서 앱 암호란 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="0f8b5-104">What are App Passwords in Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="0f8b5-105">Exchange Active Sync를 사용하는 Apple 네이티브 메일 클라이언트와 같은 특정 비브라우저 앱은 현재 다단계 인증을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-105">Certain non-browser apps, such as the Apple native email client that uses Exchange Active Sync, currently do not support multi-factor authentication.</span></span> <span data-ttu-id="0f8b5-106">다단계 인증은 사용자 기준으로 사용되도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-106">Multi-factor authentication is enabled per user.</span></span>  <span data-ttu-id="0f8b5-107">즉, 다음과 같은 경우 사용자가 다단계 인증을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-107">This means that a user can't use multi-factor authentication if:</span></span>

- <span data-ttu-id="0f8b5-108">사용자가 다단계 인증을 사용하도록 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-108">The user has been enabled for multi-factor authentication</span></span>
- <span data-ttu-id="0f8b5-109">사용자가 비브라우저 앱을 사용하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-109">The user is trying to use a non-browser app.</span></span>

<span data-ttu-id="0f8b5-110">사용자는 앱 암호를 통해 앱을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-110">An app password allows the user to use the app.</span></span>

<span data-ttu-id="0f8b5-111">앱 암호를 만든 후 이러한 비브라우저 앱에서 원래 암호 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-111">Once you have an app password, you use it in place of your original password with these non-browser apps.</span></span> <span data-ttu-id="0f8b5-112">2단계 인증에 등록하면 Microsoft는 누군가가 두 번째 인증을 수행할 수 없으면 사용자의 암호로도 로그인하지 못하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-112">When you register for two-step verification, you're telling Microsoft not to let anyone sign in with your password if they can't also perform the second verification.</span></span> <span data-ttu-id="0f8b5-113">휴대폰의 Apple 네이티브 메일 클라이언트는 2단계 인증을 요청할 수 없기 때문에 로그인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-113">The Apple native email client on your phone can't sign in as you because it can't ask for two-step verification.</span></span> <span data-ttu-id="0f8b5-114">이 문제에 해결책은 일상적으로 사용하지 않는 좀 더 안전한 앱 암호를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-114">The solution to this problem is to create a more secure app password that you don't use day-to-day.</span></span> <span data-ttu-id="0f8b5-115">앱 암호는 2단계 인증을 지원하지 않는 그러한 앱을 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-115">App passwords are only for those apps that can't support two-step verification.</span></span> <span data-ttu-id="0f8b5-116">앱에서 다단계 인증을 우회하여 계속 작동하도록 앱 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-116">Use the app password so that apps can bypass multi-factor authentication and continue to work.</span></span>


> [!NOTE]
> <span data-ttu-id="0f8b5-117">Outlook을 포함한 Office 2013 클라이언트는 새로운 인증 프로토콜을 지원하며 2단계 인증과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-117">Office 2013 clients (including Outlook) support new authentication protocols and can be used with two-step verification.</span></span> <span data-ttu-id="0f8b5-118">Office 2013 클라이언트는 앱 암호를 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-118">App passwords are not required for use with Office 2013 clients.</span></span>  <span data-ttu-id="0f8b5-119">자세한 내용은 [발표된 Office 2013 최신 인증 공개 미리 보기](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-119">For more information, see [Office 2013 modern authentication public preview announced](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span></span>


## <a name="how-to-use-app-passwords"></a><span data-ttu-id="0f8b5-120">앱 암호를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="0f8b5-120">How to use app passwords</span></span>
<span data-ttu-id="0f8b5-121">다음은 앱 암호에 대해 알아야 할 중요 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-121">Here are some things to know about app passwords:</span></span>

* <span data-ttu-id="0f8b5-122">사용자 고유의 앱 암호를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-122">You don't create your own app passwords.</span></span> <span data-ttu-id="0f8b5-123">자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-123">They are automatically generated.</span></span>
* <span data-ttu-id="0f8b5-124">현재 사용자 당 40개의 암호로 제한되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-124">Currently there is a limit of 40 passwords per user.</span></span> 
* <span data-ttu-id="0f8b5-125">앱 암호를 제한에 도달한 후에 만들려고 하면 기존 앱 암호 중 하나를 삭제해야 새로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-125">If you try to create an app password after you have reached the limit, you'll have to delete one of your existing app passwords before you create a new one.</span></span>
* <span data-ttu-id="0f8b5-126">응용 프로그램 단위가 아니라 장치별로 앱 암호 하나만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-126">Use one app password per device, not per application.</span></span> <span data-ttu-id="0f8b5-127">예를 들어 노트북에 사용할 앱 암호를 하나 만든 다음 노트북의 모든 응용 프로그램에 이 앱 암호를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-127">For example, you can create one app password for your laptop and use that app password for all of your applications on that laptop.</span></span> <span data-ttu-id="0f8b5-128">그런 다음 바탕 화면에 있는 모든 앱에 사용할 두 번째 앱 암호를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-128">Then, create a second app password to use for all your apps on your desktop.</span></span> 
* <span data-ttu-id="0f8b5-129">처음으로 2단계 인증에 등록하면 앱 암호가 하나만 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-129">You are given one app password the first time you register for two-step verification.</span></span>  <span data-ttu-id="0f8b5-130">추가 암호가 필요한 경우 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-130">If you need additional ones, you can create them.</span></span>



## <a name="creating-and-deleting-app-passwords"></a><span data-ttu-id="0f8b5-131">앱 암호 만들기 및 삭제</span><span class="sxs-lookup"><span data-stu-id="0f8b5-131">Creating and deleting app passwords</span></span>
<span data-ttu-id="0f8b5-132">초기 로그인 중에 사용할 수 있는 앱 암호가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-132">During your initial sign-in, you are given an app password that you can use.</span></span>  <span data-ttu-id="0f8b5-133">또한 나중에 앱 암호를 만들고 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-133">You can also create and delete app passwords later on.</span></span> <span data-ttu-id="0f8b5-134">앱 암호 삭제 방법은 다단계 인증을 사용하는 방법에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-134">How you delete app passwords depends on how you use multi-factor authentication.</span></span> <span data-ttu-id="0f8b5-135">다음 질문에 대답하여 앱 암호를 관리해야 하는 위치를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-135">Answer the following questions to determine where you should go to manage app passwords:</span></span> 

1. <span data-ttu-id="0f8b5-136">개인 Microsoft 계정에 대해 2단계 인증을 사용합니까?</span><span class="sxs-lookup"><span data-stu-id="0f8b5-136">Do you use two-step verification for your personal Microsoft account?</span></span> <span data-ttu-id="0f8b5-137">그렇다면 [앱 암호 및 2단계 인증](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) 문서를 참조하여 도움을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-137">If yes, you should refer to the [App passwords and two-step verification](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) article for help.</span></span> <span data-ttu-id="0f8b5-138">그렇지 않은 경우 2번 질문으로 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-138">If no, continue to question two.</span></span>

2. <span data-ttu-id="0f8b5-139">이제 직장이나 학교 계정에 대해 2단계 인증을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-139">Ok, so you use two-step verification for your work or school account.</span></span> <span data-ttu-id="0f8b5-140">Office 365 앱에 로그인하는 데 2단계 인증을 사용합니까?</span><span class="sxs-lookup"><span data-stu-id="0f8b5-140">Do you use it to sign in to Office 365 apps?</span></span> <span data-ttu-id="0f8b5-141">그렇다면 [Office 365용 앱 암호 만들기](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183)를 참조하여 도움을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-141">If yes, you should refer to [Create an app password for Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) for help.</span></span> <span data-ttu-id="0f8b5-142">그렇지 않은 경우 3번 질문으로 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-142">If no, continue to question three.</span></span> 

3. <span data-ttu-id="0f8b5-143">Microsoft Azure에서 2단계 인증을 사용합니까?</span><span class="sxs-lookup"><span data-stu-id="0f8b5-143">Do you use two-step verification with Microsoft Azure?</span></span> <span data-ttu-id="0f8b5-144">그렇다면 이 문서의 [Azure Portal에서 앱 암호 관리](#manage-app-passwords-in-the-Azure-portal) 섹션에서 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-144">If yes, continue to the [Manage app passwords in the Azure portal](#manage-app-passwords-in-the-Azure-portal) section of this article.</span></span> <span data-ttu-id="0f8b5-145">그렇지 않은 경우 4번 질문으로 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-145">If no, continue to question four.</span></span>

4. <span data-ttu-id="0f8b5-146">2단계 인증을 사용하는 위치를 모르십니까?</span><span class="sxs-lookup"><span data-stu-id="0f8b5-146">Not sure where you use two-step verification?</span></span> <span data-ttu-id="0f8b5-147">이 문서의 [MyApps 포털에서 앱 암호 관리](#manage-app-passwords-with-the-myapps-portal) 섹션에서 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-147">Continue to the [Manage app passwords with the MyApps portal](#manage-app-passwords-with-the-myapps-portal) section of this article.</span></span> 


## <a name="manage-app-passwords-in-the-azure-portal"></a><span data-ttu-id="0f8b5-148">Azure Portal에서 앱 암호 관리</span><span class="sxs-lookup"><span data-stu-id="0f8b5-148">Manage app passwords in the Azure portal</span></span>
<span data-ttu-id="0f8b5-149">Azure에서 2단계 인증을 사용하는 경우 Azure Portal을 통해 앱 암호를 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-149">If you use two-step verification with Azure, you want to create app passwords through the Azure portal.</span></span>

### <a name="to-create-app-passwords-in-the-azure-portal"></a><span data-ttu-id="0f8b5-150">Azure 포털에서 앱 암호를 만들려면</span><span class="sxs-lookup"><span data-stu-id="0f8b5-150">To create app passwords in the Azure portal</span></span>
1. <span data-ttu-id="0f8b5-151">Azure 클래식 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-151">Sign in to the Azure classic portal.</span></span>
2. <span data-ttu-id="0f8b5-152">위쪽에서 사용자 이름을 마우스 오른쪽 단추로 클릭하고 [추가 보안 인증]을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-152">At the top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="0f8b5-153">검사 페이지 위쪽에서 앱 암호를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-153">On the proofup page, at the top, select app passwords</span></span>
4. <span data-ttu-id="0f8b5-154">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-154">Click **Create**.</span></span>
5. <span data-ttu-id="0f8b5-155">앱 암호의 이름을 입력하고 **다음**</span><span class="sxs-lookup"><span data-stu-id="0f8b5-155">Enter a name for the app password and click **Next**</span></span>
6. <span data-ttu-id="0f8b5-156">앱 암호를 클립보드에 복사하고 앱에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-156">Copy the app password to the clipboard and paste it into your app.</span></span>
   
   ![클라우드](./media/multi-factor-authentication-end-user-app-passwords/app2.png)


### <a name="to-delete-app-passwords-in-the-azure-portal"></a><span data-ttu-id="0f8b5-158">Azure 포털에서 앱 암호를 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="0f8b5-158">To delete app passwords in the Azure portal</span></span>
1. <span data-ttu-id="0f8b5-159">Azure 클래식 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-159">Sign in to the Azure classic portal.</span></span>
2. <span data-ttu-id="0f8b5-160">위쪽에서 사용자 이름을 마우스 오른쪽 단추로 클릭하고 [추가 보안 인증]을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-160">At the top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="0f8b5-161">위쪽에서 [추가 보안 인증] 옆에 있는 **앱 암호**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-161">At the top, next to additional security verification, select **app passwords.**</span></span>
4. <span data-ttu-id="0f8b5-162">삭제할 앱 암호 옆에 있는 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-162">Next to the app password you want to delete, select **Delete**.</span></span>
5. <span data-ttu-id="0f8b5-163">**예**를 클릭하여 삭제를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-163">Confirm the deletion by clicking **yes**.</span></span>
6. <span data-ttu-id="0f8b5-164">앱 암호가 삭제되면 **닫기**를 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-164">Once the app password is deleted, you can click **close**.</span></span>


## <a name="manage-app-passwords-with-the-myapps-portal"></a><span data-ttu-id="0f8b5-165">MyApps 포털에서 앱 암호 관리</span><span class="sxs-lookup"><span data-stu-id="0f8b5-165">Manage app passwords with the MyApps portal.</span></span>
<span data-ttu-id="0f8b5-166">다단계 인증을 사용하는 방법을 잘 모르는 경우 MyApps 포털을 통해 언제든지 앱 암호를 만들고 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-166">If you are not sure how you use multi-factor authentication, then you can always create and delete app passwords through the myapps portal.</span></span>

### <a name="to-create-an-app-password-using-the-myapps-portal"></a><span data-ttu-id="0f8b5-167">Myapps 포털을 사용하여 앱 암호를 만들려면</span><span class="sxs-lookup"><span data-stu-id="0f8b5-167">To create an app password using the Myapps portal</span></span>
1. <span data-ttu-id="0f8b5-168">[https://myapps.microsoft.com](https://myapps.microsoft.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-168">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="0f8b5-169">오른쪽 위에서 이름을 클릭하고 **프로필**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-169">Click your name at the top right, and choose **Profile**.</span></span>
3. <span data-ttu-id="0f8b5-170">**추가 보안 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-170">Select **Additional Security Verification**.</span></span>
   <span data-ttu-id="0f8b5-171">![추가 보안 인증 선택 - 스크린샷](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span><span class="sxs-lookup"><span data-stu-id="0f8b5-171">![Select additional security verification - screenshot](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span></span>

4. <span data-ttu-id="0f8b5-172">**앱 암호**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-172">Select **app passwords**.</span></span>
   <span data-ttu-id="0f8b5-173">![앱 암호 선택 - 스크린샷](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span><span class="sxs-lookup"><span data-stu-id="0f8b5-173">![Select app passwords - screenshot](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span></span>

5. <span data-ttu-id="0f8b5-174">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-174">Click **Create**.</span></span>
6. <span data-ttu-id="0f8b5-175">앱 암호의 이름을 입력하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-175">Enter a name for the app password and click **Next**.</span></span>
7. <span data-ttu-id="0f8b5-176">앱 암호를 클립보드에 복사하고 앱에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-176">Copy the app password to the clipboard and paste it into your app.</span></span>
   <span data-ttu-id="0f8b5-177">![앱 암호 만들기](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span><span class="sxs-lookup"><span data-stu-id="0f8b5-177">![Create an app password](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span></span>

### <a name="to-delete-an-app-password-using-the-myapps-portal"></a><span data-ttu-id="0f8b5-178">Myapps 포털을 사용하여 앱 암호를 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="0f8b5-178">To delete an app password using the Myapps portal</span></span>
1. <span data-ttu-id="0f8b5-179">[https://myapps.microsoft.com](https://myapps.microsoft.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-179">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="0f8b5-180">위쪽에서 프로필을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-180">At the top, select profile.</span></span>
3. <span data-ttu-id="0f8b5-181">**추가 보안 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-181">Select **Additional Security Verification**.</span></span>

   ![추가 보안 인증 선택 - 스크린샷](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. <span data-ttu-id="0f8b5-183">**앱 암호**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-183">Select **app passwords**.</span></span>

   ![앱 암호 선택 - 스크린샷](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. <span data-ttu-id="0f8b5-185">제거할 앱 암호 옆에 있는 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-185">Next to the app password you want to delete, click **Delete**.</span></span>

   ![앱 암호 삭제](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. <span data-ttu-id="0f8b5-187">**예**를 클릭하여 암호를 삭제할 것인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-187">Confirm that you want to delete that password by clicking **yes**.</span></span>
7. <span data-ttu-id="0f8b5-188">앱 암호가 삭제되면 **닫기**를 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-188">Once the app password is deleted, you can click **close**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f8b5-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0f8b5-189">Next steps</span></span>

- [<span data-ttu-id="0f8b5-190">2단계 인증 설정 관리</span><span class="sxs-lookup"><span data-stu-id="0f8b5-190">Manage your two-step verification settings</span></span>](multi-factor-authentication-end-user-manage-settings.md)

- <span data-ttu-id="0f8b5-191">[Microsoft Authenticator 앱](microsoft-authenticator-app-how-to.md)을 사용하여 텍스트 또는 전화를 받는 대신 앱 알림으로 로그인을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8b5-191">Try out the [Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) to verify your sign-ins with app notifications, instead of receiving texts or calls.</span></span> 
