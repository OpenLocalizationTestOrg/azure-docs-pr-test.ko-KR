---
title: "Azure AD 응용 프로그램 프록시를 사용하여 앱 게시 | Microsoft Docs"
description: "클래식 포털에서 Azure AD 응용 프로그램 프록시를 사용하여 온-프레미스 응용 프로그램을 클라우드에 게시합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 96490c0d060fe5486a7235a5aa76380c8d9b5d4f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="ff01e-103">Azure AD 응용 프로그램 프록시를 사용하여 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="ff01e-103">Publish applications using Azure AD Application Proxy</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ff01e-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ff01e-104">Azure portal</span></span>](application-proxy-publish-azure-portal.md)
> * [<span data-ttu-id="ff01e-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="ff01e-105">Azure classic portal</span></span>](active-directory-application-proxy-publish.md)

<span data-ttu-id="ff01e-106">Azure AD 응용 프로그램 프록시를 통해 온-프레미스 응용 프로그램을 인터넷에 액세스되도록 게시하여 원격 작업자를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-106">Azure AD Application Proxy helps you support remote workers by publishing on-premises applications to be accessed over the internet.</span></span> <span data-ttu-id="ff01e-107">이제 [Azure 클래식 포털에서 응용 프로그램 프록시를 사용하도록 설정](active-directory-application-proxy-enable.md)했어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-107">By this point, you should already have [enabled Application Proxy in the Azure classic portal](active-directory-application-proxy-enable.md).</span></span> <span data-ttu-id="ff01e-108">이 문서에서는 로컬 네트워크에 실행 중인 응용 프로그램을 게시하는 단계를 안내하고 네트워크 외부에서 안전한 원격 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-108">This article walks you through the steps to publish applications that are running on your local network and provide secure remote access from outside your network.</span></span> <span data-ttu-id="ff01e-109">이 문서를 완료하면 응용 프로그램에 개인 설정된 정보 또는 보안 요구 사항을 구성할 준비가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-109">After you complete this article, you'll be ready to configure the application with personalized information or security requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="ff01e-110">응용 프로그램 프록시는 Premium 또는 Basic 버전의 Azure Active Directory로 업그레이드하는 경우에만 사용할 수 있는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-110">Application Proxy is a feature that is available only if you upgraded to the Premium or Basic edition of Azure Active Directory.</span></span> <span data-ttu-id="ff01e-111">자세한 내용은 [Azure Active Directory 버전](active-directory-editions.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff01e-111">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span> <span data-ttu-id="ff01e-112">응용 프로그램 프록시를 사용하려는 경우 [Azure Portal에서 응용 프로그램을 게시](application-proxy-publish-azure-portal.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-112">If you want to use Application Proxy, you can [Publish applications in the Azure portal](application-proxy-publish-azure-portal.md).</span></span>

## <a name="publish-an-app-using-the-wizard"></a><span data-ttu-id="ff01e-113">마법사를 사용하여 앱 게시</span><span class="sxs-lookup"><span data-stu-id="ff01e-113">Publish an app using the wizard</span></span>
1. <span data-ttu-id="ff01e-114">[Azure 클래식 포털](https://manage.windowsazure.com/)에서 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-114">Sign in as an administrator in the [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="ff01e-115">Active Directory로 이동하여 응용 프로그램 프록시를 사용하도록 설정한 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-115">Go to Active Directory and select the directory where you enabled Application Proxy.</span></span>
   
    ![Active Directory - 아이콘](./media/active-directory-application-proxy-publish/ad_icon.png)
3. <span data-ttu-id="ff01e-117">**응용 프로그램** 탭을 클릭한 다음 화면 맨 위에 있는 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-117">Click the **Applications** tab, and then click the **Add** button at the bottom of the screen</span></span>
   
    ![응용 프로그램 추가](./media/active-directory-application-proxy-publish/aad_appproxy_selectdirectory.png)
4. <span data-ttu-id="ff01e-119">**네트워크 외부에서 액세스할 수 있는 응용 프로그램 게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-119">Select **Publish an application that will be accessible from outside your network**.</span></span>
   
    ![네트워크 외부에서 액세스할 수 있는 응용 프로그램 게시](./media/active-directory-application-proxy-publish/aad_appproxy_addapp.png)
5. <span data-ttu-id="ff01e-121">응용 프로그램에 대한 다음과 같은 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-121">Provide the following information about your application:</span></span>
   
   * <span data-ttu-id="ff01e-122">**이름**: 사용자가 알기 쉬운 응용 프로그램의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-122">**Name**: The user-friendly name for your application.</span></span> <span data-ttu-id="ff01e-123">디렉터리 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-123">It must be unique within your directory.</span></span>
   * <span data-ttu-id="ff01e-124">**내부 URL**: 응용 프로그램 프록시 커넥터가 개인 네트워크 내부에서 응용 프로그램에 액세스하는 데 사용하는 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-124">**Internal URL**: The address that the Application Proxy Connector uses to access the application from inside your private network.</span></span> <span data-ttu-id="ff01e-125">나머지 서버는 게시되지 않은 반면 게시할 백 앤드 서버에 특정 경로를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-125">You can provide a specific path on the backend server to publish, while the rest of the server is unpublished.</span></span> <span data-ttu-id="ff01e-126">이러한 방식으로 동일한 서버에 다른 사이트를 게시하고 각각에 고유한 이름 및 액세스 규칙을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-126">In this way, you can publish different sites on the same server, and give each one its own name and access rules.</span></span>
     
     > [!TIP]
     > <span data-ttu-id="ff01e-127">경로를 게시하는 경우 응용 프로그램에 필요한 이미지, 스크립트 및 스타일 시트를 모두 포함하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-127">If you publish a path, make sure that it includes all the necessary images, scripts, and style sheets for your application.</span></span> <span data-ttu-id="ff01e-128">예를 들어 앱이 https://yourapp/app에 위치하고 https://yourapp/media에 있는 이미지를 사용하는 경우 https://yourapp/을 경로로 게시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-128">For example, if your app is at https://yourapp/app and uses images located at https://yourapp/media, then you should publish https://yourapp/ as the path.</span></span>
     > 
     > 
   * <span data-ttu-id="ff01e-129">**사전 인증 메서드**: 응용 프로그램 프록시가 응용 프로그램에 대한 액세스를 제공하기 전에 사용자를 확인하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-129">**Preauthentication Method**: How Application Proxy verifies users before giving them access to your application.</span></span> <span data-ttu-id="ff01e-130">드롭다운 메뉴에서 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-130">Choose one of the options from the drop-down menu.</span></span>
     
     * <span data-ttu-id="ff01e-131">Azure Active Directory: 응용 프로그램 프록시는 Azure AD를 사용하여 로그인하는 사용자를 리디렉션하여 디렉터리와 응용 프로그램에 대한 사용 권한을 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-131">Azure Active Directory: Application Proxy redirects users to sign in with Azure AD, which authenticates their permissions for the directory and application.</span></span>
     * <span data-ttu-id="ff01e-132">통과: 사용자는 응용 프로그램에 액세스하도록 인증할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-132">Passthrough: Users don't have to authenticate to access the application.</span></span>
     
     ![응용 프로그램 속성](./media/active-directory-application-proxy-publish/aad_appproxy_appproperties.png)  
6. <span data-ttu-id="ff01e-134">마법사를 마치려면 화면 아래쪽에 있는 확인 표시를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-134">To finish the wizard, click the check mark at the bottom of the screen.</span></span> <span data-ttu-id="ff01e-135">이제 응용 프로그램이 Azure AD에 정의되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-135">The application is now defined in Azure AD.</span></span>

## <a name="assign-users-and-groups-to-the-application"></a><span data-ttu-id="ff01e-136">응용 프로그램에 사용자 및 그룹 할당</span><span class="sxs-lookup"><span data-stu-id="ff01e-136">Assign users and groups to the application</span></span>
<span data-ttu-id="ff01e-137">사용자가 게시된 응용 프로그램에 액세스하기 위해서는 개별적으로 또는 그룹에 할당되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-137">In order for your users to access your published application, you need to assign them either individually or in groups.</span></span> <span data-ttu-id="ff01e-138">(자신에게도 액세스 권한을 할당합니다.) 할당되는 사용자마다 Azure Basic 이상의 라이선스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-138">(Remember to assign yourself access, too.) Each user you assign needs a license for Azure Basic or higher.</span></span> <span data-ttu-id="ff01e-139">개별적으로 또는 그룹에 라이선스를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-139">You can assign licenses individually or to groups.</span></span> <span data-ttu-id="ff01e-140">자세한 내용은 [응용 프로그램에 사용자 할당](active-directory-applications-guiding-developers-assigning-users.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff01e-140">For more information, see [Assigning users to an application](active-directory-applications-guiding-developers-assigning-users.md).</span></span> 

<span data-ttu-id="ff01e-141">사전 인증이 필요한 앱의 경우 사용자를 할당하면 응용 프로그램을 사용할 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-141">For apps that require preauthentication, assigning a user grants permission to use the application.</span></span> <span data-ttu-id="ff01e-142">사전 인증이 필요 없는 앱의 경우 사용자를 할당하면 사용자가 액세스 패널을 통해 응용 프로그램에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-142">For apps that don't require preauthentication, assigning a user means that the user can access the application through the access panel.</span></span>

1. <span data-ttu-id="ff01e-143">앱 추가 마법사를 마친 후에 응용 프로그램에 대한 빠른 시작 페이지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-143">After finishing the Add App wizard, you see the Quick Start page for your application.</span></span> <span data-ttu-id="ff01e-144">앱에 대한 액세스 권한이 있는 사용자를 관리하려면 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-144">To manage who has access to the app, select **Users and groups**.</span></span>
   
    ![응용 프로그램 프록시 빠른 시작 할당 사용자 - 스크린샷](./media/active-directory-application-proxy-publish/aad_appproxy_usersgroups.png)
2. <span data-ttu-id="ff01e-146">디렉터리에서 특정 그룹을 검색 하거나 모든 사용자를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-146">Search for specific groups in your directory, or show all your users.</span></span> <span data-ttu-id="ff01e-147">검색 결과를 표시하려면 확인 표시를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-147">To display the search results, click the check mark.</span></span>
   
      ![그룹 또는 사용자 검색 - 스크린샷](./media/active-directory-application-proxy-publish/aad_appproxy_search.png)
3. <span data-ttu-id="ff01e-149">이 앱에 할당하려는 각 사용자나 그룹을 선택하고 **할당**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-149">Select each user or group you want to assign to this app and click **Assign**.</span></span> <span data-ttu-id="ff01e-150">이 작업을 확인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-150">You are asked to confirm this action.</span></span>

> [!NOTE]
> <span data-ttu-id="ff01e-151">Windows 통합 인증 앱에 대해 온-프레미스 Active Directory에서 동기화되는 사용자와 그룹만 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-151">For Integrated Windows Authentication apps, you can assign only users and groups that are synced from your on-premises Active Directory.</span></span> <span data-ttu-id="ff01e-152">Microsoft 계정 및 게스트를 사용하여 로그인하는 사용자는 Azure Active Directory 응용 프로그램 프록시를 사용하여 게시된 앱에 할당할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-152">Users who sign in with a Microsoft account and guests cannot be assigned for apps published with Azure Active Directory Application Proxy.</span></span> <span data-ttu-id="ff01e-153">사용자가 게시하는 앱과 동일한 도메인의 일부인 자격 증명을 사용하여 로그인하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-153">Make sure your users sign in with credentials that are part of the same domain as the app you are publishing.</span></span>
> 
> 

## <a name="test-your-published-application"></a><span data-ttu-id="ff01e-154">게시된 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="ff01e-154">Test your published application</span></span>
<span data-ttu-id="ff01e-155">응용 프로그램을 게시하면 게시한 URL로 이동하여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-155">Once you have published your application, you can test it out by navigating to the URL that you published.</span></span> <span data-ttu-id="ff01e-156">액세스할 수 있는지, 올바르게 렌더링되었는지 및 모든 것이 예상대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-156">Make sure that you can access it, that it renders correctly, and that everything works as expected.</span></span> <span data-ttu-id="ff01e-157">문제가 발생하거나 오류 메시지가 나타날 경우 [문제 해결 가이드](active-directory-application-proxy-troubleshoot.md)를 사용해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-157">If you have trouble or get an error message, try the [troubleshooting guide](active-directory-application-proxy-troubleshoot.md).</span></span>

## <a name="configure-your-application"></a><span data-ttu-id="ff01e-158">응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="ff01e-158">Configure your application</span></span>
<span data-ttu-id="ff01e-159">게시된 앱을 수정하거나 구성 페이지에서 고급 옵션을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-159">You can modify published apps or set up advanced options on the Configure page.</span></span> <span data-ttu-id="ff01e-160">이 페이지에서 이름을 변경하거나 로고를 업로드하여 앱을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-160">On this page, you can customize your app by changing the name or uploading a logo.</span></span> <span data-ttu-id="ff01e-161">또한 사전 인증 방법 또는 Multi-Factor Authentication과 같은 액세스 규칙을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-161">You can also manage access rules like the preauthentication method or multi-factor authentication.</span></span>

![고급 구성](./media/active-directory-application-proxy-publish/aad_appproxy_configure.png)

<span data-ttu-id="ff01e-163">Azure Active Directory 응용 프로그램 프록시를 사용하여 응용 프로그램을 게시하면 Azure AD의 응용 프로그램 목록에 표시되므로 해당 위치에서 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-163">After you publish applications using Azure Active Directory Application Proxy, they appear in the Applications list in Azure AD, and you can manage them there.</span></span>

<span data-ttu-id="ff01e-164">응용 프로그램을 게시한 후 응용 프로그램 프록시 서비스를 사용하지 않도록 설정하면 개인 네트워크 외부에서 더 이상 응용 프로그램에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-164">If you disable Application Proxy services after you have published applications, the applications are no longer accessible from outside your private network.</span></span> <span data-ttu-id="ff01e-165">사용자는 계속해서 평소처럼 응용 프로그램 온-프레미스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-165">Your users can still access the applications on-premises as usual.</span></span>

<span data-ttu-id="ff01e-166">응용 프로그램을 확인하고 액세스할 수 있는지 확인하려면 응용 프로그램의 이름을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-166">To view an application and make sure that it is accessible, double-click the name of the application.</span></span> <span data-ttu-id="ff01e-167">응용 프로그램 프록시 서비스를 사용할 수 없고 응용 프로그램을 사용할 수 없는 경우 화면 위쪽에 경고 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-167">If the Application Proxy service is disabled and the application is not available, a warning message appears at the top of the screen.</span></span>

<span data-ttu-id="ff01e-168">응용 프로그램을 삭제하려면 목록에서 응용 프로그램을 선택한 다음 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ff01e-168">To delete an application, select an application in the list and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff01e-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ff01e-169">Next steps</span></span>
* [<span data-ttu-id="ff01e-170">고유한 도메인 이름을 사용하여 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="ff01e-170">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)
* [<span data-ttu-id="ff01e-171">Single Sign-On 사용</span><span class="sxs-lookup"><span data-stu-id="ff01e-171">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="ff01e-172">조건부 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="ff01e-172">Enable conditional access</span></span>](active-directory-application-proxy-conditional-access.md)
* [<span data-ttu-id="ff01e-173">클레임 인식 응용 프로그램으로 작업</span><span class="sxs-lookup"><span data-stu-id="ff01e-173">Working with claims aware applications</span></span>](active-directory-application-proxy-claims-aware-apps.md)

<span data-ttu-id="ff01e-174">최신 뉴스 및 업데이트는 [응용 프로그램 프록시 블로그](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="ff01e-174">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>

