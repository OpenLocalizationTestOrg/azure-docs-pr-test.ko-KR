---
title: "Azure AD 응용 프로그램 프록시를 사용 하 여 aaaPublish 앱 | Microsoft Docs"
description: "Hello 클래식 포털에서 Azure AD 응용 프로그램 프록시를 통해 온-프레미스 응용 프로그램 toohello 클라우드를 게시 합니다."
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
ms.openlocfilehash: 7926998314c65521ae48aebcceb33cb0c67e0b87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="c98f8-103">Azure AD 응용 프로그램 프록시를 사용하여 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="c98f8-103">Publish applications using Azure AD Application Proxy</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c98f8-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c98f8-104">Azure portal</span></span>](application-proxy-publish-azure-portal.md)
> * [<span data-ttu-id="c98f8-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="c98f8-105">Azure classic portal</span></span>](active-directory-application-proxy-publish.md)

<span data-ttu-id="c98f8-106">Azure AD 응용 프로그램 프록시를 사용 하면 온-프레미스 응용 프로그램 toobe hello를 통해 액세스를 게시 하 여 원격 작업자를 지 원하는 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-106">Azure AD Application Proxy helps you support remote workers by publishing on-premises applications toobe accessed over hello internet.</span></span> <span data-ttu-id="c98f8-107">이제 이미 있어야 [hello Azure 클래식 포털에서에서 응용 프로그램 프록시를 사용 하도록 설정](active-directory-application-proxy-enable.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-107">By this point, you should already have [enabled Application Proxy in hello Azure classic portal](active-directory-application-proxy-enable.md).</span></span> <span data-ttu-id="c98f8-108">이 문서는 로컬 네트워크에서 실행 되는 hello 단계 toopublish 응용 프로그램을 단계별로 하 고 네트워크 외부에서 보안 원격 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-108">This article walks you through hello steps toopublish applications that are running on your local network and provide secure remote access from outside your network.</span></span> <span data-ttu-id="c98f8-109">이 문서를 완료 한 후 개인 설정 된 정보 또는 보안 요구 사항과 준비 tooconfigure hello 응용 프로그램 수 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-109">After you complete this article, you'll be ready tooconfigure hello application with personalized information or security requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="c98f8-110">응용 프로그램 프록시는 toohello Premium 또는 Azure Active directory Basic edition을 업그레이드 한 경우에 사용할 수 있는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-110">Application Proxy is a feature that is available only if you upgraded toohello Premium or Basic edition of Azure Active Directory.</span></span> <span data-ttu-id="c98f8-111">자세한 내용은 [Azure Active Directory 버전](active-directory-editions.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c98f8-111">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span> <span data-ttu-id="c98f8-112">응용 프로그램 프록시 toouse 하려는 경우 다음을 할 수 있습니다 [hello Azure 포털에서에서 응용 프로그램을 게시](application-proxy-publish-azure-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-112">If you want toouse Application Proxy, you can [Publish applications in hello Azure portal](application-proxy-publish-azure-portal.md).</span></span>

## <a name="publish-an-app-using-hello-wizard"></a><span data-ttu-id="c98f8-113">Hello 마법사를 사용 하 여 앱 게시</span><span class="sxs-lookup"><span data-stu-id="c98f8-113">Publish an app using hello wizard</span></span>
1. <span data-ttu-id="c98f8-114">Hello에 관리자 권한으로 로그인 [Azure 클래식 포털](https://manage.windowsazure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-114">Sign in as an administrator in hello [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="c98f8-115">디렉터리 tooActive 이동한 다음 응용 프로그램 프록시를 설정한 hello 디렉터리를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-115">Go tooActive Directory and select hello directory where you enabled Application Proxy.</span></span>
   
    ![Active Directory - 아이콘](./media/active-directory-application-proxy-publish/ad_icon.png)
3. <span data-ttu-id="c98f8-117">Hello 클릭 **응용 프로그램** 탭을 클릭 한 다음 hello **추가** hello hello 화면 맨 아래에 단추</span><span class="sxs-lookup"><span data-stu-id="c98f8-117">Click hello **Applications** tab, and then click hello **Add** button at hello bottom of hello screen</span></span>
   
    ![응용 프로그램 추가](./media/active-directory-application-proxy-publish/aad_appproxy_selectdirectory.png)
4. <span data-ttu-id="c98f8-119">**네트워크 외부에서 액세스할 수 있는 응용 프로그램 게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-119">Select **Publish an application that will be accessible from outside your network**.</span></span>
   
    ![네트워크 외부에서 액세스할 수 있는 응용 프로그램 게시](./media/active-directory-application-proxy-publish/aad_appproxy_addapp.png)
5. <span data-ttu-id="c98f8-121">Hello 다음 응용 프로그램에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-121">Provide hello following information about your application:</span></span>
   
   * <span data-ttu-id="c98f8-122">**이름**: hello 응용 프로그램에 대 한 알기 쉬운 이름.</span><span class="sxs-lookup"><span data-stu-id="c98f8-122">**Name**: hello user-friendly name for your application.</span></span> <span data-ttu-id="c98f8-123">디렉터리 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-123">It must be unique within your directory.</span></span>
   * <span data-ttu-id="c98f8-124">**내부 URL**: 응용 프로그램 프록시 커넥터 hello hello 주소 tooaccess hello 내부에서 응용 프로그램 사용자가 개인 네트워크를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-124">**Internal URL**: hello address that hello Application Proxy Connector uses tooaccess hello application from inside your private network.</span></span> <span data-ttu-id="c98f8-125">Hello 서버 hello 나머지 게시 하지 않은 동안 hello 백 엔드 서버 toopublish에 특정 경로 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-125">You can provide a specific path on hello backend server toopublish, while hello rest of hello server is unpublished.</span></span> <span data-ttu-id="c98f8-126">이러한 방식으로 서로 다른 사이트를 게시할 수 있습니다 동일한 서버 hello 되 고 각각 고유한 이름 및 액세스 규칙을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-126">In this way, you can publish different sites on hello same server, and give each one its own name and access rules.</span></span>
     
     > [!TIP]
     > <span data-ttu-id="c98f8-127">경로 게시 하는 경우 모든 hello 필요한 이미지, 스크립트 및 응용 프로그램에 대 한 스타일 시트를 포함 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-127">If you publish a path, make sure that it includes all hello necessary images, scripts, and style sheets for your application.</span></span> <span data-ttu-id="c98f8-128">예를 들어 앱 https://yourapp/app에 https://yourapp/media에 있는 이미지를 사용 하는 경우 다음 게시 해야 https://yourapp/ hello 경로로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-128">For example, if your app is at https://yourapp/app and uses images located at https://yourapp/media, then you should publish https://yourapp/ as hello path.</span></span>
     > 
     > 
   * <span data-ttu-id="c98f8-129">**사전 인증 방법을**: 응용 프로그램 프록시에 어떻게 액세스 tooyour 응용 프로그램을 제공 하기 전에 사용자를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-129">**Preauthentication Method**: How Application Proxy verifies users before giving them access tooyour application.</span></span> <span data-ttu-id="c98f8-130">Hello 드롭 다운 메뉴에서 hello 옵션 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-130">Choose one of hello options from hello drop-down menu.</span></span>
     
     * <span data-ttu-id="c98f8-131">Azure Active Directory: 응용 프로그램 프록시는 hello 디렉터리와 응용 프로그램에 대 한 사용 권한을 인증 하는 Azure AD 사용 하 여 사용자가 toosign을 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-131">Azure Active Directory: Application Proxy redirects users toosign in with Azure AD, which authenticates their permissions for hello directory and application.</span></span>
     * <span data-ttu-id="c98f8-132">사용자가 통과: tooauthenticate tooaccess hello 응용 프로그램을 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-132">Passthrough: Users don't have tooauthenticate tooaccess hello application.</span></span>
     
     ![응용 프로그램 속성](./media/active-directory-application-proxy-publish/aad_appproxy_appproperties.png)  
6. <span data-ttu-id="c98f8-134">toofinish hello 마법사 hello hello 화면 맨 아래에 hello 확인 표시를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-134">toofinish hello wizard, click hello check mark at hello bottom of hello screen.</span></span> <span data-ttu-id="c98f8-135">hello 응용 프로그램은 이제 Azure AD에서 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-135">hello application is now defined in Azure AD.</span></span>

## <a name="assign-users-and-groups-toohello-application"></a><span data-ttu-id="c98f8-136">사용자 및 그룹 toohello 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="c98f8-136">Assign users and groups toohello application</span></span>
<span data-ttu-id="c98f8-137">tooaccess 게시 된 응용 프로그램 사용자에 대 한 주문, tooassign 필요한을 개별적으로 또는 그룹에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-137">In order for your users tooaccess your published application, you need tooassign them either individually or in groups.</span></span> <span data-ttu-id="c98f8-138">(Tooassign 기억 너무 직접 액세스 합니다.) 할당되는 사용자마다 Azure Basic 이상의 라이선스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-138">(Remember tooassign yourself access, too.) Each user you assign needs a license for Azure Basic or higher.</span></span> <span data-ttu-id="c98f8-139">개별적으로 라이선스를 할당할 수 있습니다 또는 toogroups 합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-139">You can assign licenses individually or toogroups.</span></span> <span data-ttu-id="c98f8-140">자세한 내용은 참조 [tooan 응용 프로그램 사용자를 할당](active-directory-applications-guiding-developers-assigning-users.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-140">For more information, see [Assigning users tooan application](active-directory-applications-guiding-developers-assigning-users.md).</span></span> 

<span data-ttu-id="c98f8-141">사전 인증 필요로 하는 응용 프로그램의 경우 toouse hello 응용 프로그램 사용 권한 부여에 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-141">For apps that require preauthentication, assigning a user grants permission toouse hello application.</span></span> <span data-ttu-id="c98f8-142">필요 하지 않은 앱에 대 한 사전 인증을 사용자 지정 의미 해당 hello 사용자 hello 액세스 패널을 통해 hello 응용 프로그램에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-142">For apps that don't require preauthentication, assigning a user means that hello user can access hello application through hello access panel.</span></span>

1. <span data-ttu-id="c98f8-143">Hello 앱 추가 마법사 완료 후 빠른 응용 프로그램 페이지를 시작 하는 hello를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-143">After finishing hello Add App wizard, you see hello Quick Start page for your application.</span></span> <span data-ttu-id="c98f8-144">access toohello 앱을 가진 toomanage 선택 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-144">toomanage who has access toohello app, select **Users and groups**.</span></span>
   
    ![응용 프로그램 프록시 빠른 시작 할당 사용자 - 스크린샷](./media/active-directory-application-proxy-publish/aad_appproxy_usersgroups.png)
2. <span data-ttu-id="c98f8-146">디렉터리에서 특정 그룹을 검색 하거나 모든 사용자를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-146">Search for specific groups in your directory, or show all your users.</span></span> <span data-ttu-id="c98f8-147">toodisplay hello 검색 결과 hello 확인 표시를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-147">toodisplay hello search results, click hello check mark.</span></span>
   
      ![그룹 또는 사용자 검색 - 스크린샷](./media/active-directory-application-proxy-publish/aad_appproxy_search.png)
3. <span data-ttu-id="c98f8-149">각 사용자 또는 그룹 tooassign toothis 응용 프로그램을 클릭 하 여 **할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-149">Select each user or group you want tooassign toothis app and click **Assign**.</span></span> <span data-ttu-id="c98f8-150">tooconfirm이이 작업을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-150">You are asked tooconfirm this action.</span></span>

> [!NOTE]
> <span data-ttu-id="c98f8-151">Windows 통합 인증 앱에 대해 온-프레미스 Active Directory에서 동기화되는 사용자와 그룹만 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-151">For Integrated Windows Authentication apps, you can assign only users and groups that are synced from your on-premises Active Directory.</span></span> <span data-ttu-id="c98f8-152">Microsoft 계정 및 게스트를 사용하여 로그인하는 사용자는 Azure Active Directory 응용 프로그램 프록시를 사용하여 게시된 앱에 할당할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-152">Users who sign in with a Microsoft account and guests cannot be assigned for apps published with Azure Active Directory Application Proxy.</span></span> <span data-ttu-id="c98f8-153">Hello의 일부인 자격 증명으로 로그인 사용자가 있는지 확인 hello 앱을 게시 하는 동일한 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-153">Make sure your users sign in with credentials that are part of hello same domain as hello app you are publishing.</span></span>
> 
> 

## <a name="test-your-published-application"></a><span data-ttu-id="c98f8-154">게시된 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="c98f8-154">Test your published application</span></span>
<span data-ttu-id="c98f8-155">응용 프로그램을 게시 한 게시 toohello URL을 탐색 하 여 아웃를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-155">Once you have published your application, you can test it out by navigating toohello URL that you published.</span></span> <span data-ttu-id="c98f8-156">액세스할 수 있는지, 올바르게 렌더링되었는지 및 모든 것이 예상대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-156">Make sure that you can access it, that it renders correctly, and that everything works as expected.</span></span> <span data-ttu-id="c98f8-157">문제가 발생 하거나 오류 메시지가 나타날 경우 시도 hello [문제 해결 가이드](active-directory-application-proxy-troubleshoot.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-157">If you have trouble or get an error message, try hello [troubleshooting guide](active-directory-application-proxy-troubleshoot.md).</span></span>

## <a name="configure-your-application"></a><span data-ttu-id="c98f8-158">응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="c98f8-158">Configure your application</span></span>
<span data-ttu-id="c98f8-159">게시 된 앱을 수정 하거나 hello 구성 페이지에서 고급 옵션을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-159">You can modify published apps or set up advanced options on hello Configure page.</span></span> <span data-ttu-id="c98f8-160">이 페이지에서는 hello 이름 변경 또는 로고를 업로드 하 여 앱을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-160">On this page, you can customize your app by changing hello name or uploading a logo.</span></span> <span data-ttu-id="c98f8-161">또한 사전 인증 방법 또는 multi-factor authentication hello와 같은 액세스 규칙을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-161">You can also manage access rules like hello preauthentication method or multi-factor authentication.</span></span>

![고급 구성](./media/active-directory-application-proxy-publish/aad_appproxy_configure.png)

<span data-ttu-id="c98f8-163">응용 프로그램을 게시 한 후 Azure Active Directory 응용 프로그램 프록시를 사용 하 여 Azure AD에서 hello 응용 프로그램 목록에 표시 하 고 있습니다 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-163">After you publish applications using Azure Active Directory Application Proxy, they appear in hello Applications list in Azure AD, and you can manage them there.</span></span>

<span data-ttu-id="c98f8-164">응용 프로그램 프록시 서비스를 사용 하지 않도록 응용 프로그램을 게시 한 후, hello 응용 프로그램은 개인 네트워크 외부에서 액세스할 수 있는 더 이상.</span><span class="sxs-lookup"><span data-stu-id="c98f8-164">If you disable Application Proxy services after you have published applications, hello applications are no longer accessible from outside your private network.</span></span> <span data-ttu-id="c98f8-165">사용자가 계속 수 액세스 hello 응용 프로그램이 온-프레미스 평소와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-165">Your users can still access hello applications on-premises as usual.</span></span>

<span data-ttu-id="c98f8-166">입력 한 tooview 응용 프로그램 있는지 한다는 액세스할 수 hello 응용 프로그램의 hello 이름을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-166">tooview an application and make sure that it is accessible, double-click hello name of hello application.</span></span> <span data-ttu-id="c98f8-167">Hello 응용 프로그램 프록시 서비스를 사용 하지 않도록 설정 하는 경우 hello 응용 프로그램을 사용할 수 없으면 hello hello 화면 위쪽에 경고 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-167">If hello Application Proxy service is disabled and hello application is not available, a warning message appears at hello top of hello screen.</span></span>

<span data-ttu-id="c98f8-168">응용 프로그램 toodelete hello 목록에서 응용 프로그램을 선택 하 고 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="c98f8-168">toodelete an application, select an application in hello list and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c98f8-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c98f8-169">Next steps</span></span>
* [<span data-ttu-id="c98f8-170">고유한 도메인 이름을 사용하여 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="c98f8-170">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)
* [<span data-ttu-id="c98f8-171">Single Sign-On 사용</span><span class="sxs-lookup"><span data-stu-id="c98f8-171">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="c98f8-172">조건부 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="c98f8-172">Enable conditional access</span></span>](active-directory-application-proxy-conditional-access.md)
* [<span data-ttu-id="c98f8-173">클레임 인식 응용 프로그램으로 작업</span><span class="sxs-lookup"><span data-stu-id="c98f8-173">Working with claims aware applications</span></span>](active-directory-application-proxy-claims-aware-apps.md)

<span data-ttu-id="c98f8-174">Hello 최신 뉴스 및 업데이트에 대 한 체크 아웃 hello [응용 프로그램 프록시 블로그](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="c98f8-174">For hello latest news and updates, check out hello [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>

