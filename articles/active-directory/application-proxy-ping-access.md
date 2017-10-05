---
title: "Azure AD 응용 프로그램 프록시용 PingAccess를 통한 헤더 기반 인증 | Microsoft Docs"
description: "PingAccess 및 앱 프록시를 사용하여 응용 프로그램을 게시하여 헤더 기반 인증을 지원합니다."
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
ms.openlocfilehash: 58034ab8830cf655199875b448948ea14dc04a70
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="header-based-authentication-for-single-sign-on-with-application-proxy-and-pingaccess"></a><span data-ttu-id="34d9b-103">응용 프로그램 프록시 및 PingAccess를 사용하여 Single Sign-On에 대한 헤더 기반 인증</span><span class="sxs-lookup"><span data-stu-id="34d9b-103">Header-based authentication for single sign-on with Application Proxy and PingAccess</span></span>

<span data-ttu-id="34d9b-104">Azure Active Directory 응용 프로그램 프록시 및 PingAccess는 Azure Active Directory 고객에게 더 많은 응용 프로그램에 대한 액세스를 제공하도록 파트너 관계를 맺고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-104">Azure Active Directory Application Proxy and PingAccess have partnered together to provide Azure Active Directory customers with access to even more applications.</span></span> <span data-ttu-id="34d9b-105">PingAccess는 [기존 응용 프로그램 프록시 제품](active-directory-application-proxy-get-started.md)을 확장하여 인증에 헤더를 사용하는 응용 프로그램에 대한 Single Sign-On 액세스를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-105">PingAccess expands the [existing Application Proxy offerings](active-directory-application-proxy-get-started.md) to include single sign-on access to applications that use headers for authentication.</span></span>

## <a name="what-is-pingaccess-for-azure-ad"></a><span data-ttu-id="34d9b-106">Azure AD용 PingAccess는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="34d9b-106">What is PingAccess for Azure AD?</span></span>

<span data-ttu-id="34d9b-107">Azure Active Directory용 PingAccess는 인증에 헤더를 사용하는 응용 프로그램에 대한 액세스 및 Single Sign-On을 사용자에게 부여할 수 있도록 하는 PingAccess 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-107">PingAccess for Azure Active Directory is an offering of PingAccess that enables you to give users access and single sign-on to applications that use headers for authentication.</span></span> <span data-ttu-id="34d9b-108">응용 프로그램 프록시는 Azure AD를 사용하여 액세스를 인증한 다음 커넥터 서비스를 통해 트래픽을 전달하여 다른 앱과 같이 이러한 앱을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-108">Application Proxy treats these apps like any other, using Azure AD to authenticate access and then passing traffic through the connector service.</span></span> <span data-ttu-id="34d9b-109">PingAccess는 응용 프로그램에서 읽을 수 있는 형식으로 인증을 받도록 앱 앞에 위치하고 Azure AD의 액세스 토큰을 헤더로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-109">PingAccess sits in front of the apps and translates the access token from Azure AD into a header so that the application receives the authentication in the format it can read.</span></span>

<span data-ttu-id="34d9b-110">사용자는 회사 앱을 사용하기 위해 로그인할 때 다른 점을 알아차리지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-110">Your users won’t notice anything different when they sign in to use your corporate apps.</span></span> <span data-ttu-id="34d9b-111">여전히 어디에서든지 모든 장치에서 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-111">They can still work from anywhere on any device.</span></span> 

<span data-ttu-id="34d9b-112">응용 프로그램 프록시 커넥터는 해당 인증 유형에 관계 없이 모든 앱에 원격 트래픽을 보내므로 계속해서 자동으로 부하 균형을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-112">Since the Application Proxy connectors direct remote traffic to all apps regardless of their authentication type, they’ll continue to load balance automatically, as well.</span></span>

## <a name="how-do-i-get-access"></a><span data-ttu-id="34d9b-113">액세스 권한은 어떻게 얻을 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="34d9b-113">How do I get access?</span></span>

<span data-ttu-id="34d9b-114">이 시나리오는 Azure Active Directory 및 PingAccess 간의 파트너 관계를 통해 제공되므로 두 서비스에 대한 라이선스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-114">Since this scenario is offered through a partnership between Azure Active Directory and PingAccess, you need licenses for both services.</span></span> <span data-ttu-id="34d9b-115">그러나 Azure Active Directory Premium 구독에는 최대 20개의 응용 프로그램을 보장하는 기본 PingAccess 라이선스가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-115">However, Azure Active Directory Premium subscriptions include a basic PingAccess license that covers up to 20 applications.</span></span> <span data-ttu-id="34d9b-116">헤더 기반 응용 프로그램을 20개 이상 게시해야 하는 경우 PingAccess에서 라이선스를 추가로 구입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-116">If you need to publish more than 20 header-based applications, you can purchase an additional license from PingAccess.</span></span> 

<span data-ttu-id="34d9b-117">자세한 내용은 [Azure Active Directory 버전](active-directory-editions.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="34d9b-117">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="publish-your-application-in-azure"></a><span data-ttu-id="34d9b-118">Azure에 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="34d9b-118">Publish your application in Azure</span></span>

<span data-ttu-id="34d9b-119">이 문서는 처음으로 이 시나리오를 사용하여 앱을 게시하는 사람들을 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-119">This article is intended for people who are publishing an app with this scenario for the first time.</span></span> <span data-ttu-id="34d9b-120">게시 단계 외에도 응용 프로그램과 PingAccess를 시작하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-120">It walks through how to get started with both Application and PingAccess, in addition to the publishing steps.</span></span> <span data-ttu-id="34d9b-121">두 서비스를 이미 구성했지만 게시 단계에서 리프레셔를 원하는 경우 커넥터 설치를 건너뛰고 [응용 프로그램 프록시를 사용하여 Azure AD에 앱 추가](#add-your-app-to-Azure-AD-with-Application-Proxy)로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-121">If you’ve already configured both services but want a refresher on the publishing steps, you can skip the connector installation and move on to [Add your app to Azure AD with Application Proxy](#add-your-app-to-Azure-AD-with-Application-Proxy).</span></span>

>[!NOTE]
><span data-ttu-id="34d9b-122">이 시나리오는 Azure AD와 PingAccess 간의 파트너 관계이므로 일부 지침은 Ping ID 사이트에 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-122">Since this scenario is a partnership between Azure AD and PingAccess, some of the instructions exist on the Ping Identity site.</span></span>

### <a name="install-an-application-proxy-connector"></a><span data-ttu-id="34d9b-123">응용 프로그램 프록시 커넥터 설치</span><span class="sxs-lookup"><span data-stu-id="34d9b-123">Install an Application Proxy connector</span></span>

<span data-ttu-id="34d9b-124">이미 응용 프로그램 프록시를 사용하도록 설정되어 있고 커넥터가 설치되어 있는 경우 이 섹션을 건너뛰고 [응용 프로그램 프록시를 사용하여 Azure AD에 앱 추가](#add-your-app-to-azure-ad-with-application-proxy)로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-124">If you already have Application Proxy enabled, and have a connector installed, you can skip this section and move on to [Add your app to Azure AD with Application Proxy](#add-your-app-to-azure-ad-with-application-proxy).</span></span>

<span data-ttu-id="34d9b-125">응용 프로그램 프록시 커넥터는 원격 직원의 트래픽을 게시된 앱으로 전달하는 Windows Server 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-125">The Application Proxy connector is a Windows Server service that directs the traffic from your remote employees to your published apps.</span></span> <span data-ttu-id="34d9b-126">자세한 설치 지침은 [Azure Portal에서 응용 프로그램 프록시 사용](active-directory-application-proxy-enable.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="34d9b-126">For more detailed installation instructions, see [Enable Application Proxy in the Azure portal](active-directory-application-proxy-enable.md).</span></span>

1. <span data-ttu-id="34d9b-127">전역 관리자 권한으로 [Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-127">Sign in to the [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="34d9b-128">**Azure Active Directory** > **응용 프로그램 프록시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-128">Select **Azure Active Directory** > **Application proxy**.</span></span>
3. <span data-ttu-id="34d9b-129">**커넥터 다운로드**를 선택하여 응용 프로그램 프록시 커넥터 다운로드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-129">Select **Download Connector** to start the Application Proxy connector download.</span></span> <span data-ttu-id="34d9b-130">설치 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-130">Follow the installation instructions.</span></span>

   ![응용 프로그램 프록시를 사용하도록 설정하고 커넥터 다운로드](./media/application-proxy-ping-access/install-connector.png)

4. <span data-ttu-id="34d9b-132">커넥터를 다운로드하면 디렉터리에 대해 응용 프로그램 프록시가 자동으로 활성화되지만 그렇지 않은 경우 **응용 프로그램 프록시 사용**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-132">Downloading the connector should automatically enable Application Proxy for your directory, but if not you can select **Enable Application Proxy**.</span></span>


### <a name="add-your-app-to-azure-ad-with-application-proxy"></a><span data-ttu-id="34d9b-133">응용 프로그램 프록시를 사용하여 Azure AD에 앱 추가</span><span class="sxs-lookup"><span data-stu-id="34d9b-133">Add your app to Azure AD with Application Proxy</span></span>

<span data-ttu-id="34d9b-134">Azure Portal에서 수행해야 하는 두 가지 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-134">There are two actions you need to take in the Azure portal.</span></span> <span data-ttu-id="34d9b-135">먼저 응용 프로그램 프록시를 사용하여 응용 프로그램을 게시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-135">First, you need to publish your application with Application Proxy.</span></span> <span data-ttu-id="34d9b-136">그런 다음 PingAccess 단계에서 사용할 수 있는 해당 앱에 대한 정보를 수집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-136">Then, you need to collect some information about the app that you can use during the PingAccess steps.</span></span>

<span data-ttu-id="34d9b-137">앱을 게시하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-137">Follow these steps to publish your app.</span></span> <span data-ttu-id="34d9b-138">1 ~ 8 단계에 대한 자세한 연습은 [Azure AD 응용 프로그램 프록시를 사용하여 응용 프로그램 게시](application-proxy-publish-azure-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="34d9b-138">For a more detailed walkthrough of steps 1-8, see [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

1. <span data-ttu-id="34d9b-139">마지막 섹션에 있지 않았던 경우 전역 관리자로 [Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-139">If you didn't in the last section, sign in to the [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="34d9b-140">**Azure Active Directory** > **Enterprise 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-140">Select **Azure Active Directory** > **Enterprise applications**.</span></span>
3. <span data-ttu-id="34d9b-141">블레이드의 위쪽에서 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-141">Select **Add** at the top of the blade.</span></span>
4. <span data-ttu-id="34d9b-142">**온-프레미스 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-142">Select **On-premises application**.</span></span>
5. <span data-ttu-id="34d9b-143">새 앱에 대한 정보로 필수 필드를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-143">Fill out the required fields with information about your new app.</span></span> <span data-ttu-id="34d9b-144">설정에 대해 다음 지침을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-144">Use the following guidance for the settings:</span></span>
   - <span data-ttu-id="34d9b-145">**내부 URL**: 회사 네트워크에 있을 때 일반적으로 앱의 로그인 페이지로 안내하는 URL을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-145">**Internal URL**: Normally you provide the URL that takes you to the app’s sign in page when you’re on the corporate network.</span></span> <span data-ttu-id="34d9b-146">이 시나리오의 경우 커넥터에서 PingAccess 프록시를 앱의 기본 페이지로 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-146">For this scenario the connector needs to treat the PingAccess proxy as the front page of the app.</span></span> <span data-ttu-id="34d9b-147">`https://<host name of your PA server>:<port>` 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-147">Use this format: `https://<host name of your PA server>:<port>`.</span></span> <span data-ttu-id="34d9b-148">포트는 기본적으로 3000이지만 PingAccess에서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-148">The port is 3000 by default, but you can configure it in PingAccess.</span></span>
   - <span data-ttu-id="34d9b-149">**사전 인증 방법**: Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="34d9b-149">**Pre-authentication method**: Azure Active Directory</span></span>
   - <span data-ttu-id="34d9b-150">**헤더에서 URL 변환**: 아니요</span><span class="sxs-lookup"><span data-stu-id="34d9b-150">**Translate URL in Headers**: No</span></span>

   >[!NOTE]
   ><span data-ttu-id="34d9b-151">첫 번째 응용 프로그램인 경우 3000 포트를 사용하여 시작하고 PingAccess 구성을 변경하면 다시 돌아와서 이 설정을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-151">If this is your first application, use port 3000 to start and come back to update this setting if you change your PingAccess configuration.</span></span> <span data-ttu-id="34d9b-152">두 번째 이상의 앱인 경우 PingAccess에서 구성한 수신기와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-152">If this is your second or later app, this will need to match the Listener you’ve configured in PingAccess.</span></span> <span data-ttu-id="34d9b-153">[PingAccess의 수신기](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-153">Learn more about [listeners in PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span></span>

6. <span data-ttu-id="34d9b-154">블레이드의 아래쪽에서 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-154">Select **Add** at the bottom of the blade.</span></span> <span data-ttu-id="34d9b-155">응용 프로그램이 추가되고 빠른 시작 메뉴가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-155">Your application is added, and the quick start menu opens.</span></span>
7. <span data-ttu-id="34d9b-156">빠른 시작 메뉴에서 **테스트할 사용자 지정**을 선택하고 응용 프로그램에 하나 이상의 사용자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-156">In the quick start menu, select **Assign a user for testing**, and add at least one user to the application.</span></span> <span data-ttu-id="34d9b-157">이 테스트 계정에 온-프레미스 응용 프로그램에 대한 액세스 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-157">Make sure this test account has access to the on-premises application.</span></span>
8. <span data-ttu-id="34d9b-158">**할당**을 선택하여 테스트 사용자 할당을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-158">Select **Assign** to save the test user assignment.</span></span>
9. <span data-ttu-id="34d9b-159">앱 관리 블레이드에서 **Single Sign-On**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-159">On the app management blade, select **Single sign-on**.</span></span>
10. <span data-ttu-id="34d9b-160">드롭다운 메뉴에서 **헤더 기반 로그온**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-160">Choose **Header-based sign-on** from the drop-down menu.</span></span> <span data-ttu-id="34d9b-161">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-161">Select **Save**.</span></span>

   >[!TIP]
   ><span data-ttu-id="34d9b-162">헤더 기반 Single Sign-On을 처음 사용하는 경우 PingAccess를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-162">If this is your first time using header-based single sign-on, you need to install PingAccess.</span></span> <span data-ttu-id="34d9b-163">Azure 구독이 PingAccess 설치와 자동으로 연결되도록 하려면 이 Single Sign-On 페이지의 링크를 사용하여 PingAccess를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-163">To make sure your Azure subscription is automatically associated with your PingAccess installation, use the link on this single sign-on page to download PingAccess.</span></span> <span data-ttu-id="34d9b-164">지금 다운로드 사이트를 열거나 나중에 이 페이지로 다시 돌아올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-164">You can open the download site now, or come back to this page later.</span></span> 

   ![헤더 기반 로그온 선택](./media/application-proxy-ping-access/sso-header.PNG)

11. <span data-ttu-id="34d9b-166">Enterprise 응용 프로그램 블레이드를 닫거나 왼쪽으로 스크롤하여 Azure Active Directory 메뉴로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-166">Close the Enterprise applications blade or scroll all the way to the left to return to the Azure Active Directory menu.</span></span>
12. <span data-ttu-id="34d9b-167">**앱 등록**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-167">Select **App registrations**.</span></span>

   ![앱 등록 선택](./media/application-proxy-ping-access/app-registrations.png)

13. <span data-ttu-id="34d9b-169">방금 추가한 앱을 선택한 다음 **회신 URL**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-169">Select the app you just added, then **Reply URLs**.</span></span>

   ![회신 URL 선택](./media/application-proxy-ping-access/reply-urls.png)

14. <span data-ttu-id="34d9b-171">5단계에서 앱에 할당한 외부 URL이 회신 URL 목록에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-171">Check to see if the external URL that you assigned to your app in step 5 is in the Reply URLs list.</span></span> <span data-ttu-id="34d9b-172">그렇지 않은 경우 지금 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-172">If it’s not, add it now.</span></span>
15. <span data-ttu-id="34d9b-173">앱 설정 블레이드에서 **필요한 권한**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-173">On the app settings blade, select **Required permissions**.</span></span>

  ![필요한 권한 선택](./media/application-proxy-ping-access/required-permissions.png)

16. <span data-ttu-id="34d9b-175">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-175">Select **Add**.</span></span> <span data-ttu-id="34d9b-176">API의 경우 **Windows Azure Active Directory**를 선택한 다음 **선택**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-176">For the API, choose **Windows Azure Active Directory**, then **Select**.</span></span> <span data-ttu-id="34d9b-177">사용 권한의 경우 **모든 응용 프로그램 읽기 및 작성**을 선택한 다음 **로그인 및 사용자 프로필 읽기**, **선택** 및 **완료**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-177">For the permissions, choose **Read and write all applications** and **Sign in and read user profile**, then **Select** and **Done**.</span></span>  

  ![권한 선택](./media/application-proxy-ping-access/select-permissions.png)

### <a name="collect-information-for-the-pingaccess-steps"></a><span data-ttu-id="34d9b-179">PingAccess 단계에 대한 정보 수집</span><span class="sxs-lookup"><span data-stu-id="34d9b-179">Collect information for the PingAccess steps</span></span>

1. <span data-ttu-id="34d9b-180">앱 설정 블레이드에서 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-180">On your app settings blade, select **Properties**.</span></span> 

  ![속성 선택](./media/application-proxy-ping-access/properties.png)

2. <span data-ttu-id="34d9b-182">**응용 프로그램 ID** 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-182">Save the **Application Id** value.</span></span> <span data-ttu-id="34d9b-183">이 값은 PingAccess를 구성할 때 클라이언트 ID에 대해 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-183">This is used for the client ID when you configure PingAccess.</span></span>
3. <span data-ttu-id="34d9b-184">앱 설정 블레이드에서 **키**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-184">On the app settings blade, select **Keys**.</span></span>

  ![키 선택](./media/application-proxy-ping-access/Keys.png)

4. <span data-ttu-id="34d9b-186">키 설명을 입력하고 드롭다운 메뉴에서 만료 날짜를 선택하여 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-186">Create a key by entering a key description and choosing an expiration date from the drop-down menu.</span></span>
5. <span data-ttu-id="34d9b-187">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-187">Select **Save**.</span></span> <span data-ttu-id="34d9b-188">**값** 필드에 GUID가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-188">A GUID appears in the **Value** field.</span></span>

  <span data-ttu-id="34d9b-189">이 창을 닫은 후 이 값을 다시 볼 수 없으므로 지금 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-189">Save this value now, as you won’t be able to see it again after you close this window.</span></span>

  ![새 키 만들기](./media/application-proxy-ping-access/create-keys.png)

6. <span data-ttu-id="34d9b-191">앱 등록 블레이드를 닫거나 왼쪽으로 스크롤하여 Azure Active Directory 메뉴로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-191">Close the App registrations blade or scroll all the way to the left to return to the Azure Active Directory menu.</span></span>
7. <span data-ttu-id="34d9b-192">**속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-192">Select **Properties**.</span></span>
8. <span data-ttu-id="34d9b-193">**디렉터리 ID** GUID를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-193">Save the **Directory ID** GUID.</span></span>

### <a name="optional---update-graphapi-to-send-custom-fields"></a><span data-ttu-id="34d9b-194">선택 사항 - 사용자 지정 필드를 보내도록 GraphAPI 업데이트</span><span class="sxs-lookup"><span data-stu-id="34d9b-194">Optional - Update GraphAPI to send custom fields</span></span>

<span data-ttu-id="34d9b-195">Azure AD에서 인증에 대해 전송하는 보안 토큰의 목록은 [Azure AD 토큰 참조](./develop/active-directory-token-and-claims.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="34d9b-195">For a list of security tokens that Azure AD sends for authentication, see [Azure AD token reference](./develop/active-directory-token-and-claims.md).</span></span> <span data-ttu-id="34d9b-196">다른 토큰을 전송하는 사용자 지정 클레임이 필요한 경우 GraphAPI를 사용하여 앱 필드 *acceptMappedClaims*를 **True**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-196">If you need a custom claim that sends other tokens, use GraphAPI to set the app field *acceptMappedClaims* to **True**.</span></span> <span data-ttu-id="34d9b-197">Azure AD Graph Explorer 또는 MS Graph를 사용하여 이 구성을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-197">You can use either Azure AD Graph Explorer or MS Graph to make this configuration.</span></span> 

<span data-ttu-id="34d9b-198">이 예에서는 Graph Explorer를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-198">This example uses Graph Explorer:</span></span>

```
PATCH https://graph.windows.net/myorganization/applications/<object_id_GUID_of_your_application> 

{
  "acceptMappedClaims":true
}
```

## <a name="download-pingaccess-and-configure-your-app"></a><span data-ttu-id="34d9b-199">PingAccess 다운로드 및 앱 구성</span><span class="sxs-lookup"><span data-stu-id="34d9b-199">Download PingAccess and configure your app</span></span>

<span data-ttu-id="34d9b-200">이제 Azure Active Directory 설정 단계를 모두 완료했으므로 PingAccess 구성으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-200">Now that you've completed all the Azure Active Directory setup steps, you can move on to configuring PingAccess.</span></span> 

<span data-ttu-id="34d9b-201">이 시나리오의 PingAccess 부분에 대한 자세한 단계는 Ping ID 문서, [Azure AD용 PingAccess 구성](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)에서 계속됩니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-201">The detailed steps for the PingAccess part of this scenario continue in the Ping Identity documentation, [Configure PingAccess for Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).</span></span>

<span data-ttu-id="34d9b-202">이러한 단계는 PingAccess 계정이 아직 없는 경우 PingAccess 계정을 얻고, PingAccess 서버를 설치하고, Azure Portal에서 복사한 디렉터리 ID로 Azure AD OIDC 공급자 연결을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-202">Those steps walk you through the process of getting a PingAccess account if you don't already have one, installing the PingAccess Server, and creating an Azure AD OIDC Provider connection with the Directory ID that you copied from the Azure portal.</span></span> <span data-ttu-id="34d9b-203">그런 다음 응용 프로그램 ID 및 키 값을 사용하여 PingAccess에서 웹 세션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-203">Then, you use the Application ID and Key values to create a Web Session on PingAccess.</span></span> <span data-ttu-id="34d9b-204">그런 다음 ID 매핑을 설정하고 가상 호스트, 사이트 및 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-204">After that, you can set up identity mapping and create a virtual host, site, and application.</span></span>

### <a name="test-your-app"></a><span data-ttu-id="34d9b-205">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="34d9b-205">Test your app</span></span>

<span data-ttu-id="34d9b-206">이러한 모든 단계를 완료하면 앱이 준비되고 실행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-206">When you've completed all these steps, your app should be up and running.</span></span> <span data-ttu-id="34d9b-207">테스트하려면 브라우저를 열고 Azure에 앱을 게시할 때 만든 외부 URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-207">To test it, open a browser and navigate to the external URL that you created when you published the app in Azure.</span></span> <span data-ttu-id="34d9b-208">앱에 할당한 테스트 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="34d9b-208">Sign in with the test account that you assigned to the app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34d9b-209">다음 단계</span><span class="sxs-lookup"><span data-stu-id="34d9b-209">Next steps</span></span>

- [<span data-ttu-id="34d9b-210">Azure AD에 대한 PingAccess 구성(영문)</span><span class="sxs-lookup"><span data-stu-id="34d9b-210">Configure PingAccess for Azure AD</span></span>](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)
- [<span data-ttu-id="34d9b-211">Azure AD 응용 프로그램 프록시에서 Single Sign-On을 제공하는 방법</span><span class="sxs-lookup"><span data-stu-id="34d9b-211">How does Azure AD Application Proxy provide single sign-on?</span></span>](application-proxy-sso-overview.md)
- [<span data-ttu-id="34d9b-212">응용 프로그램 프록시 문제 해결</span><span class="sxs-lookup"><span data-stu-id="34d9b-212">Troubleshoot Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)
