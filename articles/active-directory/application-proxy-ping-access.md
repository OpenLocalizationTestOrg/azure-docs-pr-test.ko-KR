---
title: "Azure AD 응용 프로그램 프록시에 대 한 aaaHeader 기반 인증 PingAccess 사용 | Microsoft Docs"
description: "PingAccess 및 응용 프로그램 프록시 toosupport 헤더 기반 인증으로 응용 프로그램을 게시 합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 38fe3e7a41a71f4ae6c75f014e44c722f773bd22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="header-based-authentication-for-single-sign-on-with-application-proxy-and-pingaccess"></a><span data-ttu-id="ac831-103">응용 프로그램 프록시 및 PingAccess를 사용하여 Single Sign-On에 대한 헤더 기반 인증</span><span class="sxs-lookup"><span data-stu-id="ac831-103">Header-based authentication for single sign-on with Application Proxy and PingAccess</span></span>

<span data-ttu-id="ac831-104">Azure Active Directory 응용 프로그램 프록시 및 PingAccess 관계를 맺고 함께 tooprovide 액세스 tooeven 사용 하는 Azure Active Directory 고객 더 많은 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-104">Azure Active Directory Application Proxy and PingAccess have partnered together tooprovide Azure Active Directory customers with access tooeven more applications.</span></span> <span data-ttu-id="ac831-105">PingAccess 확장 hello [기존의 응용 프로그램 프록시 서비스](active-directory-application-proxy-get-started.md) tooinclude single sign-on 액세스 tooapplications 인증에 대 한 헤더를 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-105">PingAccess expands hello [existing Application Proxy offerings](active-directory-application-proxy-get-started.md) tooinclude single sign-on access tooapplications that use headers for authentication.</span></span>

## <a name="what-is-pingaccess-for-azure-ad"></a><span data-ttu-id="ac831-106">Azure AD용 PingAccess는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="ac831-106">What is PingAccess for Azure AD?</span></span>

<span data-ttu-id="ac831-107">Azure Active Directory에 대 한 PingAccess toogive 사용자가 액세스할 수 있도록 하는 PingAccess 및 single sign on tooapplications 인증에 대 한 헤더를 사용 하는 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-107">PingAccess for Azure Active Directory is an offering of PingAccess that enables you toogive users access and single sign-on tooapplications that use headers for authentication.</span></span> <span data-ttu-id="ac831-108">응용 프로그램 프록시는 Azure AD tooauthenticate 액세스를 사용 하 여와 hello 커넥터 서비스를 통해 트래픽을 전달 요, 이러한 앱을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-108">Application Proxy treats these apps like any other, using Azure AD tooauthenticate access and then passing traffic through hello connector service.</span></span> <span data-ttu-id="ac831-109">PingAccess는 hello 앱 앞에 배치 하 고 hello 응용 프로그램을 읽을 수는 hello 형태로 hello 인증을 받을 수 있도록 Azure AD에서 액세스 토큰 hello 헤더로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-109">PingAccess sits in front of hello apps and translates hello access token from Azure AD into a header so that hello application receives hello authentication in hello format it can read.</span></span>

<span data-ttu-id="ac831-110">회사 앱 toouse에 로그인 할 때 사용자가 다른 있어서는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-110">Your users won’t notice anything different when they sign in toouse your corporate apps.</span></span> <span data-ttu-id="ac831-111">여전히 어디에서든지 모든 장치에서 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-111">They can still work from anywhere on any device.</span></span> 

<span data-ttu-id="ac831-112">Hello 응용 프로그램 프록시 커넥터의 인증 유형에 관계 없이 원격 트래픽을 tooall 앱을 지시 하는 경우 이후 자동으로 tooload 균형을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-112">Since hello Application Proxy connectors direct remote traffic tooall apps regardless of their authentication type, they’ll continue tooload balance automatically, as well.</span></span>

## <a name="how-do-i-get-access"></a><span data-ttu-id="ac831-113">액세스 권한은 어떻게 얻을 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="ac831-113">How do I get access?</span></span>

<span data-ttu-id="ac831-114">이 시나리오는 Azure Active Directory 및 PingAccess 간의 파트너 관계를 통해 제공되므로 두 서비스에 대한 라이선스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-114">Since this scenario is offered through a partnership between Azure Active Directory and PingAccess, you need licenses for both services.</span></span> <span data-ttu-id="ac831-115">그러나 Azure Active Directory Premium 구독에 too20 응용 프로그램을 검사 하는 기본 PingAccess 라이선스가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-115">However, Azure Active Directory Premium subscriptions include a basic PingAccess license that covers up too20 applications.</span></span> <span data-ttu-id="ac831-116">20 개 이상의 헤더 기반 응용 프로그램 toopublish 해야 할 경우 PingAccess에서 추가 라이센스를 구입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-116">If you need toopublish more than 20 header-based applications, you can purchase an additional license from PingAccess.</span></span> 

<span data-ttu-id="ac831-117">자세한 내용은 [Azure Active Directory 버전](active-directory-editions.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac831-117">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="publish-your-application-in-azure"></a><span data-ttu-id="ac831-118">Azure에 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="ac831-118">Publish your application in Azure</span></span>

<span data-ttu-id="ac831-119">이 문서는 사용자에 게 게시 하는 hello에 대 한이 시나리오를 사용 하 여 앱 처음으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-119">This article is intended for people who are publishing an app with this scenario for hello first time.</span></span> <span data-ttu-id="ac831-120">Tooget를 어떻게 시작 응용 프로그램과 PingAccess, 또한 toohello 게시 단계 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-120">It walks through how tooget started with both Application and PingAccess, in addition toohello publishing steps.</span></span> <span data-ttu-id="ac831-121">두 서비스를 이미 구성한 해도 hello 게시 단계 세부 정보를 원하는 경우 hello 커넥터 설치를 건너뛰고 너무 이동[응용 프로그램 프록시는 AD에 앱 tooAzure 추가](#add-your-app-to-Azure-AD-with-Application-Proxy)합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-121">If you’ve already configured both services but want a refresher on hello publishing steps, you can skip hello connector installation and move on too[Add your app tooAzure AD with Application Proxy](#add-your-app-to-Azure-AD-with-Application-Proxy).</span></span>

>[!NOTE]
><span data-ttu-id="ac831-122">이 시나리오는 Azure AD 간의 파트너 관계 이므로 hello Ping Id 사이트에 있는 hello 명령 중 일부는 PingAccess, 및입니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-122">Since this scenario is a partnership between Azure AD and PingAccess, some of hello instructions exist on hello Ping Identity site.</span></span>

### <a name="install-an-application-proxy-connector"></a><span data-ttu-id="ac831-123">응용 프로그램 프록시 커넥터 설치</span><span class="sxs-lookup"><span data-stu-id="ac831-123">Install an Application Proxy connector</span></span>

<span data-ttu-id="ac831-124">응용 프로그램 프록시를 사용 하 고, 이미 있고는 커넥터가 설치 되어 있는 경우이 섹션을 건너뛰고 너무 이동[응용 프로그램 프록시는 AD에 앱 tooAzure 추가](#add-your-app-to-azure-ad-with-application-proxy)합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-124">If you already have Application Proxy enabled, and have a connector installed, you can skip this section and move on too[Add your app tooAzure AD with Application Proxy](#add-your-app-to-azure-ad-with-application-proxy).</span></span>

<span data-ttu-id="ac831-125">hello 응용 프로그램 프록시 커넥터는 Windows 서버에서 원격 직원 tooyour hello 트래픽을 전송 하는 서비스에 게시 된 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-125">hello Application Proxy connector is a Windows Server service that directs hello traffic from your remote employees tooyour published apps.</span></span> <span data-ttu-id="ac831-126">설치 지침 보다 자세한 참조 [hello Azure 포털에서에서 응용 프로그램 프록시를 사용 하도록 설정](active-directory-application-proxy-enable.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-126">For more detailed installation instructions, see [Enable Application Proxy in hello Azure portal](active-directory-application-proxy-enable.md).</span></span>

1. <span data-ttu-id="ac831-127">Toohello 로그인 [Azure 포털](https://portal.azure.com) 전역 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-127">Sign in toohello [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="ac831-128">**Azure Active Directory** > **응용 프로그램 프록시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-128">Select **Azure Active Directory** > **Application proxy**.</span></span>
3. <span data-ttu-id="ac831-129">선택 **커넥터 다운로드** toostart hello 응용 프로그램 프록시 커넥터 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-129">Select **Download Connector** toostart hello Application Proxy connector download.</span></span> <span data-ttu-id="ac831-130">Hello 설치 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-130">Follow hello installation instructions.</span></span>

   ![응용 프로그램 프록시를 사용 하도록 설정 하 고 hello 커넥터를 다운로드 합니다.](./media/application-proxy-ping-access/install-connector.png)

4. <span data-ttu-id="ac831-132">Hello connector 다운로드 자동으로 사용 하도록 설정 해야 응용 프로그램 프록시 본인이 아니신가요 선택할 수 있지만 디렉터리에 대 한 **응용 프로그램 프록시를 사용 하도록 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-132">Downloading hello connector should automatically enable Application Proxy for your directory, but if not you can select **Enable Application Proxy**.</span></span>


### <a name="add-your-app-tooazure-ad-with-application-proxy"></a><span data-ttu-id="ac831-133">사용자 응용 프로그램 tooAzure AD 응용 프로그램 프록시를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-133">Add your app tooAzure AD with Application Proxy</span></span>

<span data-ttu-id="ac831-134">Tootake hello Azure 포털에에서 필요한 두 가지 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-134">There are two actions you need tootake in hello Azure portal.</span></span> <span data-ttu-id="ac831-135">먼저 toopublish 응용 프로그램 프록시 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-135">First, you need toopublish your application with Application Proxy.</span></span> <span data-ttu-id="ac831-136">그런 다음 해야 toocollect hello PingAccess 단계 중에 사용할 수 있는 hello 앱에 대 한 정보.</span><span class="sxs-lookup"><span data-stu-id="ac831-136">Then, you need toocollect some information about hello app that you can use during hello PingAccess steps.</span></span>

<span data-ttu-id="ac831-137">이러한 단계 toopublish 응용 프로그램을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-137">Follow these steps toopublish your app.</span></span> <span data-ttu-id="ac831-138">1 ~ 8 단계에 대한 자세한 연습은 [Azure AD 응용 프로그램 프록시를 사용하여 응용 프로그램 게시](application-proxy-publish-azure-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac831-138">For a more detailed walkthrough of steps 1-8, see [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

1. <span data-ttu-id="ac831-139">Toohello hello 마지막 섹션에서 그렇지 않은 경우 로그인 [Azure 포털](https://portal.azure.com) 전역 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-139">If you didn't in hello last section, sign in toohello [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="ac831-140">**Azure Active Directory** > **Enterprise 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-140">Select **Azure Active Directory** > **Enterprise applications**.</span></span>
3. <span data-ttu-id="ac831-141">선택 **추가** hello hello 블레이드 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-141">Select **Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="ac831-142">**온-프레미스 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-142">Select **On-premises application**.</span></span>
5. <span data-ttu-id="ac831-143">새 응용 프로그램에 대 한 정보가 필요한 hello 필드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-143">Fill out hello required fields with information about your new app.</span></span> <span data-ttu-id="ac831-144">Hello hello 설정에 대 한 지침을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-144">Use hello following guidance for hello settings:</span></span>
   - <span data-ttu-id="ac831-145">**내부 URL**: 작업을 수행 해야 toohello 응용 프로그램의 로그인 페이지에 hello 회사 네트워크에 있는 경우 hello URL을 제공 하는 일반적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-145">**Internal URL**: Normally you provide hello URL that takes you toohello app’s sign in page when you’re on hello corporate network.</span></span> <span data-ttu-id="ac831-146">이 시나리오에 대 한 hello 커넥터는 tootreat hello PingAccess 프록시 (hello) 프런트 페이지 hello 응용 프로그램에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-146">For this scenario hello connector needs tootreat hello PingAccess proxy as hello front page of hello app.</span></span> <span data-ttu-id="ac831-147">`https://<host name of your PA server>:<port>` 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-147">Use this format: `https://<host name of your PA server>:<port>`.</span></span> <span data-ttu-id="ac831-148">hello 포트는 기본적으로 3000 있지만 PingAccess에서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-148">hello port is 3000 by default, but you can configure it in PingAccess.</span></span>
   - <span data-ttu-id="ac831-149">**사전 인증 방법**: Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ac831-149">**Pre-authentication method**: Azure Active Directory</span></span>
   - <span data-ttu-id="ac831-150">**헤더에서 URL 변환**: 아니요</span><span class="sxs-lookup"><span data-stu-id="ac831-150">**Translate URL in Headers**: No</span></span>

   >[!NOTE]
   ><span data-ttu-id="ac831-151">첫 번째 응용 프로그램의 경우 포트 3000 toostart를 사용 하 여 방문 하 여 tooupdate이이 설정을 PingAccess 구성을 변경 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="ac831-151">If this is your first application, use port 3000 toostart and come back tooupdate this setting if you change your PingAccess configuration.</span></span> <span data-ttu-id="ac831-152">이 두 번째 이상 앱을이 수신기 PingAccess에 구성한 toomatch hello를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-152">If this is your second or later app, this will need toomatch hello Listener you’ve configured in PingAccess.</span></span> <span data-ttu-id="ac831-153">[PingAccess의 수신기](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-153">Learn more about [listeners in PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span></span>

6. <span data-ttu-id="ac831-154">선택 **추가** hello hello 블레이드 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-154">Select **Add** at hello bottom of hello blade.</span></span> <span data-ttu-id="ac831-155">응용 프로그램은 추가 되 고 hello 빠른 시작 메뉴가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-155">Your application is added, and hello quick start menu opens.</span></span>
7. <span data-ttu-id="ac831-156">Hello 빠른 시작 메뉴에서 선택 **테스트 하기 위한 사용자 지정**, 적어도 한 명의 사용자 toohello 응용 프로그램을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-156">In hello quick start menu, select **Assign a user for testing**, and add at least one user toohello application.</span></span> <span data-ttu-id="ac831-157">이 테스트 계정 액세스 toohello 온-프레미스 응용 프로그램에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-157">Make sure this test account has access toohello on-premises application.</span></span>
8. <span data-ttu-id="ac831-158">선택 **할당** toosave hello 테스트 사용자 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-158">Select **Assign** toosave hello test user assignment.</span></span>
9. <span data-ttu-id="ac831-159">Hello 응용 프로그램 관리 블레이드의 선택 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-159">On hello app management blade, select **Single sign-on**.</span></span>
10. <span data-ttu-id="ac831-160">선택 **헤더 기반 로그온** hello 드롭 다운 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-160">Choose **Header-based sign-on** from hello drop-down menu.</span></span> <span data-ttu-id="ac831-161">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-161">Select **Save**.</span></span>

   >[!TIP]
   ><span data-ttu-id="ac831-162">헤더 기반 single sign on을 사용 하 여 처음으로 이면 tooinstall PingAccess 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-162">If this is your first time using header-based single sign-on, you need tooinstall PingAccess.</span></span> <span data-ttu-id="ac831-163">toomake Azure 구독이 확실 PingAccess 설치 프로그램에서이 single sign-on 페이지 toodownload PingAccess hello 연결을 사용 하 여 자동으로 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-163">toomake sure your Azure subscription is automatically associated with your PingAccess installation, use hello link on this single sign-on page toodownload PingAccess.</span></span> <span data-ttu-id="ac831-164">이제 hello 다운로드 사이트를 열 수도 있고 나중에 다시 toothis 페이지 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-164">You can open hello download site now, or come back toothis page later.</span></span> 

   ![헤더 기반 로그온 선택](./media/application-proxy-ping-access/sso-header.PNG)

11. <span data-ttu-id="ac831-166">Hello 엔터프라이즈 응용 프로그램 블레이드를 닫거나 모든 hello 방식으로 toohello 왼쪽된 tooreturn toohello Azure Active Directory 메뉴 스크롤하십시오.</span><span class="sxs-lookup"><span data-stu-id="ac831-166">Close hello Enterprise applications blade or scroll all hello way toohello left tooreturn toohello Azure Active Directory menu.</span></span>
12. <span data-ttu-id="ac831-167">**앱 등록**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-167">Select **App registrations**.</span></span>

   ![앱 등록 선택](./media/application-proxy-ping-access/app-registrations.png)

13. <span data-ttu-id="ac831-169">방금 추가한 다음 선택 hello 앱 **회신 Url**합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-169">Select hello app you just added, then **Reply URLs**.</span></span>

   ![회신 URL 선택](./media/application-proxy-ping-access/reply-urls.png)

14. <span data-ttu-id="ac831-171">Hello 외부 URL이 할당 된 tooyour 앱 5 단계에서 목록에 있으면 hello 회신 Url toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-171">Check toosee if hello external URL that you assigned tooyour app in step 5 is in hello Reply URLs list.</span></span> <span data-ttu-id="ac831-172">그렇지 않은 경우 지금 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-172">If it’s not, add it now.</span></span>
15. <span data-ttu-id="ac831-173">Hello 응용 프로그램 설정 블레이드에서 선택 **필요한 권한**합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-173">On hello app settings blade, select **Required permissions**.</span></span>

  ![필요한 권한 선택](./media/application-proxy-ping-access/required-permissions.png)

16. <span data-ttu-id="ac831-175">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-175">Select **Add**.</span></span> <span data-ttu-id="ac831-176">Hello API에 대 한 선택 **Windows Azure Active Directory**, 다음 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-176">For hello API, choose **Windows Azure Active Directory**, then **Select**.</span></span> <span data-ttu-id="ac831-177">Hello 사용 권한에 대 한 선택 **읽기 및 모든 응용 프로그램 쓰기** 및 **로그인 및 사용자 프로필 읽기**, 다음 **선택** 및 **수행**합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-177">For hello permissions, choose **Read and write all applications** and **Sign in and read user profile**, then **Select** and **Done**.</span></span>  

  ![권한 선택](./media/application-proxy-ping-access/select-permissions.png)

### <a name="collect-information-for-hello-pingaccess-steps"></a><span data-ttu-id="ac831-179">Hello PingAccess 단계에 대 한 정보를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-179">Collect information for hello PingAccess steps</span></span>

1. <span data-ttu-id="ac831-180">앱 설정 블레이드에서 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-180">On your app settings blade, select **Properties**.</span></span> 

  ![속성 선택](./media/application-proxy-ping-access/properties.png)

2. <span data-ttu-id="ac831-182">Hello 저장 **응용 프로그램 Id** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-182">Save hello **Application Id** value.</span></span> <span data-ttu-id="ac831-183">이 값은 PingAccess를 구성할 때 hello 클라이언트 ID에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-183">This is used for hello client ID when you configure PingAccess.</span></span>
3. <span data-ttu-id="ac831-184">Hello 응용 프로그램 설정 블레이드에서 선택 **키**합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-184">On hello app settings blade, select **Keys**.</span></span>

  ![키 선택](./media/application-proxy-ping-access/Keys.png)

4. <span data-ttu-id="ac831-186">키 설명을 입력 하 고 hello 드롭 다운 메뉴에서 만료 날짜를 선택 하 여 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-186">Create a key by entering a key description and choosing an expiration date from hello drop-down menu.</span></span>
5. <span data-ttu-id="ac831-187">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-187">Select **Save**.</span></span> <span data-ttu-id="ac831-188">Hello에 표시 되는 GUID **값** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-188">A GUID appears in hello **Value** field.</span></span>

  <span data-ttu-id="ac831-189">이 값을 저장 이제 수 toosee 수 없을 것으로 그 후에 다시이 창을 닫으십시오.</span><span class="sxs-lookup"><span data-stu-id="ac831-189">Save this value now, as you won’t be able toosee it again after you close this window.</span></span>

  ![새 키 만들기](./media/application-proxy-ping-access/create-keys.png)

6. <span data-ttu-id="ac831-191">Hello 앱 등록 블레이드를 닫거나 모든 hello 방식으로 toohello 왼쪽된 tooreturn toohello Azure Active Directory 메뉴 스크롤하십시오.</span><span class="sxs-lookup"><span data-stu-id="ac831-191">Close hello App registrations blade or scroll all hello way toohello left tooreturn toohello Azure Active Directory menu.</span></span>
7. <span data-ttu-id="ac831-192">**속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-192">Select **Properties**.</span></span>
8. <span data-ttu-id="ac831-193">Hello 저장 **디렉터리 ID** GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-193">Save hello **Directory ID** GUID.</span></span>

### <a name="optional---update-graphapi-toosend-custom-fields"></a><span data-ttu-id="ac831-194">선택 사항-업데이트 GraphAPI toosend 사용자 지정 필드</span><span class="sxs-lookup"><span data-stu-id="ac831-194">Optional - Update GraphAPI toosend custom fields</span></span>

<span data-ttu-id="ac831-195">Azure AD에서 인증에 대해 전송하는 보안 토큰의 목록은 [Azure AD 토큰 참조](./develop/active-directory-token-and-claims.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac831-195">For a list of security tokens that Azure AD sends for authentication, see [Azure AD token reference](./develop/active-directory-token-and-claims.md).</span></span> <span data-ttu-id="ac831-196">GraphAPI tooset hello 응용 프로그램 필드를 사용 하 여 기타 토큰을 전송 하는 사용자 지정 클레임을 해야 할 경우 *acceptMappedClaims* 너무**True**합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-196">If you need a custom claim that sends other tokens, use GraphAPI tooset hello app field *acceptMappedClaims* too**True**.</span></span> <span data-ttu-id="ac831-197">Azure AD 그래프 탐색기 또는 MS 그래프 toomake이이 구성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-197">You can use either Azure AD Graph Explorer or MS Graph toomake this configuration.</span></span> 

<span data-ttu-id="ac831-198">이 예에서는 Graph Explorer를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-198">This example uses Graph Explorer:</span></span>

```
PATCH https://graph.windows.net/myorganization/applications/<object_id_GUID_of_your_application> 

{
  "acceptMappedClaims":true
}
```

## <a name="download-pingaccess-and-configure-your-app"></a><span data-ttu-id="ac831-199">PingAccess 다운로드 및 앱 구성</span><span class="sxs-lookup"><span data-stu-id="ac831-199">Download PingAccess and configure your app</span></span>

<span data-ttu-id="ac831-200">모든 hello Azure Active Directory 설정 단계를 완료 하면 했으므로 tooconfiguring PingAccess에 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-200">Now that you've completed all hello Azure Active Directory setup steps, you can move on tooconfiguring PingAccess.</span></span> 

<span data-ttu-id="ac831-201">hello hello PingAccess 부분에서는이 시나리오에 대 한 자세한 단계에서에서 계속 Ping Identity 설명서 hello [Azure AD에 대 한 구성 PingAccess](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-201">hello detailed steps for hello PingAccess part of this scenario continue in hello Ping Identity documentation, [Configure PingAccess for Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).</span></span>

<span data-ttu-id="ac831-202">이러한 단계 PingAccess 계정이 아직 없는 경우, hello PingAccess 서버를 설치 하 고 hello hello Azure 포털에서에서 복사한 디렉터리 ID가 있는 Azure AD OIDC 공급자 연결을 만드는 hello 프로세스를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-202">Those steps walk you through hello process of getting a PingAccess account if you don't already have one, installing hello PingAccess Server, and creating an Azure AD OIDC Provider connection with hello Directory ID that you copied from hello Azure portal.</span></span> <span data-ttu-id="ac831-203">그런 다음 PingAccess에 hello 응용 프로그램 ID 및 키 값 toocreate 웹 세션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-203">Then, you use hello Application ID and Key values toocreate a Web Session on PingAccess.</span></span> <span data-ttu-id="ac831-204">그런 다음 ID 매핑을 설정하고 가상 호스트, 사이트 및 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-204">After that, you can set up identity mapping and create a virtual host, site, and application.</span></span>

### <a name="test-your-app"></a><span data-ttu-id="ac831-205">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="ac831-205">Test your app</span></span>

<span data-ttu-id="ac831-206">이러한 모든 단계를 완료하면 앱이 준비되고 실행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-206">When you've completed all these steps, your app should be up and running.</span></span> <span data-ttu-id="ac831-207">tootest, 브라우저를 열고 Azure의 hello 앱을 게시할 때 만든 toohello 외부 URL을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-207">tootest it, open a browser and navigate toohello external URL that you created when you published hello app in Azure.</span></span> <span data-ttu-id="ac831-208">해당 할당된 toohello 앱 hello 테스트 계정으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac831-208">Sign in with hello test account that you assigned toohello app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac831-209">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ac831-209">Next steps</span></span>

- [<span data-ttu-id="ac831-210">Azure AD에 대한 PingAccess 구성(영문)</span><span class="sxs-lookup"><span data-stu-id="ac831-210">Configure PingAccess for Azure AD</span></span>](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)
- [<span data-ttu-id="ac831-211">Azure AD 응용 프로그램 프록시에서 Single Sign-On을 제공하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac831-211">How does Azure AD Application Proxy provide single sign-on?</span></span>](application-proxy-sso-overview.md)
- [<span data-ttu-id="ac831-212">응용 프로그램 프록시 문제 해결</span><span class="sxs-lookup"><span data-stu-id="ac831-212">Troubleshoot Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)
