---
title: "Azure AD 응용 프로그램 프록시를 사용하여 앱 게시 | Microsoft Docs"
description: "Azure Portal에서 Azure AD 응용 프로그램 프록시를 사용하여 클라우드에 온-프레미스 응용 프로그램을 게시합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: e00a939f2b20ab8e0a2ddf0ff91e59db440213ac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="64ea0-103">Azure AD 응용 프로그램 프록시를 사용하여 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="64ea0-103">Publish applications using Azure AD Application Proxy</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="64ea0-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="64ea0-104">Azure portal</span></span>](application-proxy-publish-azure-portal.md)
> * [<span data-ttu-id="64ea0-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="64ea0-105">Azure classic portal</span></span>](active-directory-application-proxy-publish.md)

<span data-ttu-id="64ea0-106">Azure AD(Active Directory) 응용 프로그램 프록시를 사용하면 인터넷을 통해 액세스할 수 있는 온-프레미스 응용 프로그램을 게시하여 원격 작업자를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-106">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications to be accessed over the internet.</span></span> <span data-ttu-id="64ea0-107">Azure Portal을 통해 이러한 응용 프로그램을 게시하여 네트워크 외부에서 보안 원격 액세스를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-107">You can publish these applications through the Azure portal to provide secure remote access from outside your network.</span></span>

<span data-ttu-id="64ea0-108">이 문서에서는 응용 프로그램 프록시를 통해 온-프레미스 앱을 게시하는 방법을 단계별로 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-108">This article walks you through the steps to publish an on-premises app with Application Proxy.</span></span> <span data-ttu-id="64ea0-109">이 문서를 완료하면 사용자가 원격으로 앱에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-109">After you complete this article, your users will be able to access your app remotely.</span></span> <span data-ttu-id="64ea0-110">그리고 Single Sign-On, 개인 설정 정보 및 보안 요구 사항과 같이 응용 프로그램에 대한 추가 기능을 구성할 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-110">And you'll be ready to configure extra features for the application like single sign-on, personalized information, and security requirements.</span></span>

<span data-ttu-id="64ea0-111">응용 프로그램 프록시를 처음 사용하는 경우 [온-프레미스 응용 프로그램에 보안된 원격 액세스를 제공하는 방법](active-directory-application-proxy-get-started.md) 문서에서 이 기능에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="64ea0-111">If you're new to Application Proxy, learn more about this feature with the article [How to provide secure remote access to on-premises applications](active-directory-application-proxy-get-started.md).</span></span>


## <a name="publish-an-on-premises-app-for-remote-access"></a><span data-ttu-id="64ea0-112">원격 액세스를 위한 온-프레미스 앱 게시</span><span class="sxs-lookup"><span data-stu-id="64ea0-112">Publish an on-premises app for remote access</span></span>

<span data-ttu-id="64ea0-113">다음 단계에 따라 응용 프로그램 프록시를 사용하여 앱을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-113">Follow these steps to publish your apps with Application Proxy.</span></span> <span data-ttu-id="64ea0-114">조직에 대한 커넥터를 아직 다운로드하여 구성하지 않은 경우 먼저 [응용 프로그램 프록시를 시작하고 커넥터를 설치](active-directory-application-proxy-enable.md)한 다음 앱을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-114">If you haven't already downloaded and configured a connector for your organization, go to [Get started with Application Proxy and install the connector](active-directory-application-proxy-enable.md) first, and then publish your app.</span></span>

> [!TIP]
> <span data-ttu-id="64ea0-115">응용 프로그램 프록시를 처음 테스트하는 경우 암호 기반 인증으로 설정된 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-115">If you're testing out Application Proxy for the first time, choose an application that's set up for password-based authentication.</span></span> <span data-ttu-id="64ea0-116">응용 프로그램 프록시에서는 다른 유형의 인증을 지원하지만 암호 기반 앱이 가장 빠르고 쉽게 시작하고 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-116">Application Proxy supports other types of authentication, but password-based apps are the easiest to get up and running quickly.</span></span> 

1. <span data-ttu-id="64ea0-117">[Azure Portal](https://portal.azure.com/)에서 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-117">Sign in as an administrator in the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="64ea0-118">**Azure Active Directory** > **Enterprise 응용 프로그램** > **새로운 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-118">Select **Azure Active Directory** > **Enterprise applications** > **New application**.</span></span>

  ![엔터프라이즈 응용 프로그램 추가](./media/application-proxy-publish-azure-portal/add-app.png)

3. <span data-ttu-id="64ea0-120">**모두**를 선택한 다음 **온-프레미스 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-120">Select **All**, then select **On-premises application**.</span></span>  

  ![응용 프로그램 직접 추가](./media/application-proxy-publish-azure-portal/add-your-own.png)

4. <span data-ttu-id="64ea0-122">응용 프로그램에 대한 다음과 같은 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-122">Provide the following information about your application:</span></span>

   - <span data-ttu-id="64ea0-123">**이름**: 액세스 패널 및 Azure Portal에 표시될 응용 프로그램의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-123">**Name**: The name of the application that will appear on the access panel and in the Azure portal.</span></span> 

   - <span data-ttu-id="64ea0-124">**내부 URL**: 개인 네트워크 내부에서 응용 프로그램에 액세스하는 데 사용하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-124">**Internal URL**: The URL that you use to access the application from inside your private network.</span></span> <span data-ttu-id="64ea0-125">나머지 서버는 게시되지 않은 반면 게시할 백 앤드 서버에 특정 경로를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-125">You can provide a specific path on the backend server to publish, while the rest of the server is unpublished.</span></span> <span data-ttu-id="64ea0-126">이렇게 하면 다른 앱과 동일한 서버에 여러 사이트를 게시하고 각 사이트에 고유한 이름과 액세스 규칙을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-126">In this way, you can publish different sites on the same server as different apps, and give each one its own name and access rules.</span></span>

     > [!TIP]
     > <span data-ttu-id="64ea0-127">경로를 게시하는 경우 응용 프로그램에 필요한 이미지, 스크립트 및 스타일 시트를 모두 포함하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-127">If you publish a path, make sure that it includes all the necessary images, scripts, and style sheets for your application.</span></span> <span data-ttu-id="64ea0-128">예를 들어 앱이 https://yourapp/app에 위치하고 https://yourapp/media에 있는 이미지를 사용하는 경우 https://yourapp/을 경로로 게시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-128">For example, if your app is at https://yourapp/app and uses images located at https://yourapp/media, then you should publish https://yourapp/ as the path.</span></span> <span data-ttu-id="64ea0-129">이 내부 URL은 사용자에게 표시되는 방문 페이지일 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-129">This internal URL doesn't have to be the landing page your users see.</span></span> <span data-ttu-id="64ea0-130">자세한 내용은 [게시된 앱에 대해 사용자 지정 홈페이지 설정](application-proxy-office365-app-launcher.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="64ea0-130">For more information, see [Set a custom home page for published apps](application-proxy-office365-app-launcher.md).</span></span>

   - <span data-ttu-id="64ea0-131">**외부 URL**: 네트워크 외부에서 앱에 액세스하기 위해 사용자가 이동할 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-131">**External URL**: The address your users will go to in order to access the app from outside your network.</span></span> <span data-ttu-id="64ea0-132">기본 응용 프로그램 프록시 도메인을 사용하지 않으려면 [Azure AD 응용 프로그램 프록시에서 사용자 지정 도메인 작업](active-directory-application-proxy-custom-domains.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="64ea0-132">If you don't want to use the default Application Proxy domain, read about [custom domains in Azure AD Application Proxy](active-directory-application-proxy-custom-domains.md).</span></span>
   - <span data-ttu-id="64ea0-133">**사전 인증**: 응용 프로그램 프록시가 사용자에게 응용 프로그램에 대한 액세스 권한을 부여하기 전에 사용자를 확인하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-133">**Pre Authentication**: How Application Proxy verifies users before giving them access to your application.</span></span> 

     - <span data-ttu-id="64ea0-134">Azure Active Directory: 응용 프로그램 프록시는 Azure AD를 사용하여 로그인하는 사용자를 리디렉션하여 디렉터리와 응용 프로그램에 대한 사용 권한을 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-134">Azure Active Directory: Application Proxy redirects users to sign in with Azure AD, which authenticates their permissions for the directory and application.</span></span> <span data-ttu-id="64ea0-135">조건부 액세스 및 Multi-Factor Authentication과 같은 Azure AD 보안 기능을 활용할 수 있도록 이 옵션을 기본값으로 유지하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-135">We recommend keeping this option as the default, so that you can take advantage of Azure AD security features like conditional access and Multi-Factor Authentication.</span></span>
     - <span data-ttu-id="64ea0-136">통과: 사용자는 응용 프로그램에 액세스하기 위해 Azure Active Directory에 대해 인증할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-136">Passthrough: Users don't have to authenticate against Azure Active Directory to access the application.</span></span> <span data-ttu-id="64ea0-137">백 엔드에 대한 인증 요구 사항은 여전히 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-137">You can still set up authentication requirements on the backend.</span></span>
   - <span data-ttu-id="64ea0-138">**커넥터 그룹**: 커넥터는 응용 프로그램에 대한 원격 액세스를 처리하고, 커넥터 그룹은 지역, 네트워크 또는 용도별로 커넥터와 앱을 구성하는 데 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-138">**Connector Group**: Connectors process the remote access to your application, and connector groups help you organize connectors and apps by region, network, or purpose.</span></span> <span data-ttu-id="64ea0-139">아직 만든 커넥터 그룹이 없는 경우 앱이 **Default**(기본값)로 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-139">If you don't have any connector groups created yet, your app is assigned to **Default**.</span></span>

   ![응용 프로그램 구성](./media/application-proxy-publish-azure-portal/configure-app.png)
5. <span data-ttu-id="64ea0-141">필요한 경우 추가 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-141">If necessary, configure additional settings.</span></span> <span data-ttu-id="64ea0-142">대부분의 응용 프로그램에서는 다음과 같은 설정을 기본 상태로 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-142">For most applications, you should keep these settings in their default states.</span></span> 
   - <span data-ttu-id="64ea0-143">**백 엔드 응용 프로그램 시간 제한**: 응용 프로그램의 인증 및 연결 속도가 느린 경우에만 이 값을 **Long**(길게)으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-143">**Backend Application Timeout**: Set this value to **Long** only if your application is slow to authenticate and connect.</span></span> 
   - <span data-ttu-id="64ea0-144">**헤더의 URL 변환**: 응용 프로그램이 인증 요청에서 원래 호스트 헤더를 요구하지 않는 한 이 값을 **Yes**(예)로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-144">**Translate URLs in Headers**: Keep this value as **Yes** unless your application required the original host header in the authentication request.</span></span>
   - <span data-ttu-id="64ea0-145">**응용 프로그램 본문의 URL 변환**: 다른 온-프레미스 응용 프로그램에 HTML 링크를 하드 코드하지 않고 사용자 지정 도메인을 사용하지 않는 한 이 값을 **No**(아니요)로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-145">**Translate URLs in Application Body**: Keep this value as **No** unless you have hardcoded HTML links to other on-premises applications, and don't use custom domains.</span></span> <span data-ttu-id="64ea0-146">자세한 내용은 [응용 프로그램 프록시를 사용한 링크 변환](application-proxy-link-translation.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="64ea0-146">For more information, see [Link translation with Application Proxy](application-proxy-link-translation.md).</span></span>
   
   ![응용 프로그램 구성](./media/application-proxy-publish-azure-portal/additional-settings.png)

6. <span data-ttu-id="64ea0-148">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-148">Select **Add**.</span></span>


## <a name="add-a-test-user"></a><span data-ttu-id="64ea0-149">테스트 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="64ea0-149">Add a test user</span></span> 

<span data-ttu-id="64ea0-150">앱이 제대로 게시되었는지 테스트하려면 테스트 사용자 계정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-150">To test that your app was published correctly, add a test user account.</span></span> <span data-ttu-id="64ea0-151">이 계정에 이미 회사 네트워크 내부에서 앱에 액세스할 수 있는 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-151">Verify that this account already has permissions to access the app from inside the corporate network.</span></span>

1. <span data-ttu-id="64ea0-152">[빠른 시작] 블레이드로 돌아가서 **테스트할 사용자 지정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-152">Back on the Quick start blade, select **Assign a user for testing**.</span></span>

  ![테스트할 사용자 지정](./media/application-proxy-publish-azure-portal/assign-user.png)

2. <span data-ttu-id="64ea0-154">[사용자 및 그룹] 블레이드에서 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-154">On the Users and groups blade, select **Add**.</span></span>

  ![사용자 또는 그룹 추가](./media/application-proxy-publish-azure-portal/add-user.png)

3. <span data-ttu-id="64ea0-156">[할당 추가] 블레이드에서 **사용자 및 그룹**을 선택한 다음 추가할 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-156">On the Add assignment blade, select **Users and groups** then choose the account you want to add.</span></span> 
4. <span data-ttu-id="64ea0-157">**할당**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-157">Select **Assign**.</span></span>

## <a name="test-your-published-app"></a><span data-ttu-id="64ea0-158">게시된 앱 테스트</span><span class="sxs-lookup"><span data-stu-id="64ea0-158">Test your published app</span></span>

<span data-ttu-id="64ea0-159">브라우저에서 게시 단계에서 구성한 외부 URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-159">In your browser, navigate to the external URL that you configured during the publish step.</span></span> <span data-ttu-id="64ea0-160">시작 화면이 표시되고 설정한 테스트 계정으로 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-160">You should see the start screen, and be able to sign in with the test account you set up.</span></span>

![게시된 앱 테스트](./media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a><span data-ttu-id="64ea0-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="64ea0-162">Next steps</span></span>
- <span data-ttu-id="64ea0-163">[커넥터 다운로드](active-directory-application-proxy-enable.md) 및 [커넥터 그룹 만들기](active-directory-application-proxy-connectors-azure-portal.md)를 수행하여 별도의 네트워크와 위치에 응용 프로그램을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-163">[Download connectors](active-directory-application-proxy-enable.md) and [create connector groups](active-directory-application-proxy-connectors-azure-portal.md) to publish applications on separate networks and locations.</span></span>

- <span data-ttu-id="64ea0-164">새로 게시된 앱에 대해 [Single Sign-On을 설정](application-proxy-sso-azure-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="64ea0-164">[Set up single sign-on](application-proxy-sso-azure-portal.md) for your newly published app</span></span>
