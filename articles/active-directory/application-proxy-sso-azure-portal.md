---
title: "Azure AD 응용 프로그램 프록시를 사용하여 앱에 SSO(Single sign-on) | Microsoft Docs"
description: "Azure Portal에서 Azure AD 응용 프로그램을 사용하여 게시된 온-프레미스 응용 프로그램에 대한 SSO(Single sign-on)를 켭니다."
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
ms.date: 07/20/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 9ddc0c1bd5f2cbb24f6761cfd041b820ee6464b8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a><span data-ttu-id="bf113-103">응용 프로그램 프록시를 사용하여 Single Sign-On에 대한 암호 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="bf113-103">Password vaulting for single sign-on with Application Proxy</span></span>

<span data-ttu-id="bf113-104">Azure Active Directory 응용 프로그램 프록시는 원격 직원들이 안전하게 액세스할 수 있도록 온-프레미스 응용 프로그램을 게시하여 생산성을 개선하는 데 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bf113-104">Azure Active Directory Application Proxy helps you improve productivity by publishing on-premises applications so that remote employees can securely access them, too.</span></span> <span data-ttu-id="bf113-105">Azure Portal에서는 이러한 앱에 대한 SSO(Single Sign-On)을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf113-105">In the Azure portal, you can also set up single sign-on (SSO) to these apps.</span></span> <span data-ttu-id="bf113-106">사용자는 Azure AD만으로 인증해야 하며, 다시 로그인할 필요 없이 엔터프라이즈 응용 프로그램에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf113-106">Your users only need to authenticate with Azure AD, and they can access your enterprise application without having to sign in again.</span></span>

<span data-ttu-id="bf113-107">응용프로그램 프록시에서는 여러 [Single Sign-On 모드](application-proxy-sso-overview.md)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bf113-107">Application Proxy supports several [single sign-on modes](application-proxy-sso-overview.md).</span></span> <span data-ttu-id="bf113-108">암호 기반 로그인은 인증에 사용자 이름/암호 조합을 사용하는 응용 프로그램을 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bf113-108">Password-based sign-on is intended for applications that use a username/password combination for authentication.</span></span> <span data-ttu-id="bf113-109">응용 프로그램에 대한 암호 기반 로그인을 구성하는 경우 사용자는 온-프레미스 응용 프로그램에 한 번 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf113-109">When you configure password-based sign-on for your application, your users have to sign in to the on-premises application once.</span></span> <span data-ttu-id="bf113-110">그런 다음 Azure Active Directory에서 로그인 정보를 저장하고 사용자가 원격으로 액세스할 때 응용 프로그램에 자동으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bf113-110">After that, Azure Active Directory stores the sign-in information and automatically provides it to the application when your users access it remotely.</span></span> 

<span data-ttu-id="bf113-111">이미 응용 프로그램 프록시를 사용하여 앱을 게시하고 테스트했을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bf113-111">You should already have published and tested your app with Application Proxy.</span></span> <span data-ttu-id="bf113-112">그렇지 않은 경우 [Azure AD 응용 프로그램 프록시를 사용하여 응용 프로그램 게시](application-proxy-publish-azure-portal.md)의 단계를 수행한 다음 여기로 다시 돌아옵니다.</span><span class="sxs-lookup"><span data-stu-id="bf113-112">If not, follow the steps in [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md) then come back here.</span></span> 

## <a name="set-up-password-vaulting-for-your-application"></a><span data-ttu-id="bf113-113">응용 프로그램에 대한 암호 보관 설정</span><span class="sxs-lookup"><span data-stu-id="bf113-113">Set up password vaulting for your application</span></span>

1. <span data-ttu-id="bf113-114">관리자로 [Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="bf113-114">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="bf113-115">**Azure Active Directory** > **Enterprise 응용 프로그램** > **모든 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf113-115">Select **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="bf113-116">목록에서 SSO로 설정할 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf113-116">From the list, select the app that you want to set up with SSO.</span></span>  
4. <span data-ttu-id="bf113-117">**Single Sign-On**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf113-117">Select **Single sign-on**.</span></span>

   ![Single Sign-On 선택](./media/application-proxy-sso-azure-portal/select-sso.png)

5. <span data-ttu-id="bf113-119">SSO 모드에 대해 **암호 기반 로그온**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf113-119">For the SSO mode, choose **Password-based Sign-on**.</span></span>
6. <span data-ttu-id="bf113-120">로그온 URL에 대해 사용자가 회사 네트워크 외부에서 앱에 로그인하기 위해 사용자 이름과 암호를 입력하는 페이지에 대한 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bf113-120">For the Sign-on URL, enter the URL for the page where users enter their username and password to sign in to your app outside of the corporate network.</span></span> <span data-ttu-id="bf113-121">이 URL은 응용 프로그램 프록시를 통해 앱을 게시할 때 만든 외부 URL일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf113-121">This may be the External URL that you created when you published the app through Application Proxy.</span></span> 

   ![암호 기반 로그온 선택 및 URL 입력](./media/application-proxy-sso-azure-portal/password-sso.png)

7. <span data-ttu-id="bf113-123">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf113-123">Select **Save**.</span></span>

<!-- Need to repro?
7. The page should tell you that a sign-in form was successfully detected at the provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow the instructions to point out where the sign-in credentials go. 
-->

## <a name="test-your-app"></a><span data-ttu-id="bf113-124">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="bf113-124">Test your app</span></span>

<span data-ttu-id="bf113-125">응용 프로그램에 원격으로 액세스하도록 구성된 외부 URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bf113-125">Go to external URL that you configured for remote access to your application.</span></span> <span data-ttu-id="bf113-126">해당 앱에 대한 자격 증명(또는 액세스 권한으로 설정한 테스트 계정에 대한 자격 증명)으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="bf113-126">Sign in with your credentials for that app (or the credentials for a test account that you set up with access).</span></span> <span data-ttu-id="bf113-127">로그인한 후에는 자격 증명을 다시 입력하지 않아도 앱에서 나갔다가 다시 돌아올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf113-127">Once you sign in successfully, you should be able to leave the app and come back without entering your credentials again.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bf113-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bf113-128">Next steps</span></span>

- <span data-ttu-id="bf113-129">[응용 프로그램 프록시를 사용하는 Single Sign-On](application-proxy-sso-overview.md)을 구현하는 다른 방법에 대해 읽기</span><span class="sxs-lookup"><span data-stu-id="bf113-129">Read about other ways to implement [Single sign-on with Application Proxy](application-proxy-sso-overview.md)</span></span>
- <span data-ttu-id="bf113-130">[Azure AD 응용 프로그램 프록시를 사용하여 앱에 원격으로 액세스하는 경우 보안 고려 사항](application-proxy-security-considerations.md)을 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="bf113-130">Learn about [Security considerations for accessing apps remotely with Azure AD Application Proxy](application-proxy-security-considerations.md)</span></span>