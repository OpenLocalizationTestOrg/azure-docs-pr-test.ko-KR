---
title: "Azure AD 응용 프로그램 프록시 aaaSingle 로그온 tooapps | Microsoft Docs"
description: "Single sign on hello Azure 포털에서에서 Azure AD 응용 프로그램 프록시 게시 된 온-프레미스 응용 프로그램에 설정 합니다."
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
ms.openlocfilehash: 5ff288d36163b74215677d9e34c93c985ac33d54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a><span data-ttu-id="591de-103">응용 프로그램 프록시를 사용하여 Single Sign-On에 대한 암호 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="591de-103">Password vaulting for single sign-on with Application Proxy</span></span>

<span data-ttu-id="591de-104">Azure Active Directory 응용 프로그램 프록시는 원격 직원들이 안전하게 액세스할 수 있도록 온-프레미스 응용 프로그램을 게시하여 생산성을 개선하는 데 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="591de-104">Azure Active Directory Application Proxy helps you improve productivity by publishing on-premises applications so that remote employees can securely access them, too.</span></span> <span data-ttu-id="591de-105">Hello Azure 포털에서에서 single sign-on (SSO) toothese 앱을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="591de-105">In hello Azure portal, you can also set up single sign-on (SSO) toothese apps.</span></span> <span data-ttu-id="591de-106">사용자가 Azure AD와 tooauthenticate 하기만 하 고 다시 toosign 필요 없이 엔터프라이즈 응용 프로그램에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="591de-106">Your users only need tooauthenticate with Azure AD, and they can access your enterprise application without having toosign in again.</span></span>

<span data-ttu-id="591de-107">응용프로그램 프록시에서는 여러 [Single Sign-On 모드](application-proxy-sso-overview.md)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="591de-107">Application Proxy supports several [single sign-on modes](application-proxy-sso-overview.md).</span></span> <span data-ttu-id="591de-108">암호 기반 로그인은 인증에 사용자 이름/암호 조합을 사용하는 응용 프로그램을 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="591de-108">Password-based sign-on is intended for applications that use a username/password combination for authentication.</span></span> <span data-ttu-id="591de-109">응용 프로그램에 대 한 암호 기반 로그온 구성 하면 사용자가 toohello 온-프레미스 응용 프로그램에서 한 번 toosign 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="591de-109">When you configure password-based sign-on for your application, your users have toosign in toohello on-premises application once.</span></span> <span data-ttu-id="591de-110">그 후 Azure Active Directory hello 로그인 정보를 저장 하 고 자동으로 제공 toohello 응용 프로그램 사용자가 원격으로 액세스 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="591de-110">After that, Azure Active Directory stores hello sign-in information and automatically provides it toohello application when your users access it remotely.</span></span> 

<span data-ttu-id="591de-111">이미 응용 프로그램 프록시를 사용하여 앱을 게시하고 테스트했을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="591de-111">You should already have published and tested your app with Application Proxy.</span></span> <span data-ttu-id="591de-112">그렇지 않은 경우 hello 단계에 따라 [Azure AD 응용 프로그램 프록시를 사용 하 여 응용 프로그램을 게시](application-proxy-publish-azure-portal.md) 여기로 돌아와 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="591de-112">If not, follow hello steps in [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md) then come back here.</span></span> 

## <a name="set-up-password-vaulting-for-your-application"></a><span data-ttu-id="591de-113">응용 프로그램에 대한 암호 보관 설정</span><span class="sxs-lookup"><span data-stu-id="591de-113">Set up password vaulting for your application</span></span>

1. <span data-ttu-id="591de-114">Toohello 로그인 [Azure 포털](https://portal.azure.com) 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="591de-114">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="591de-115">**Azure Active Directory** > **Enterprise 응용 프로그램** > **모든 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="591de-115">Select **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="591de-116">Hello 목록에서 sso를 tooset hello 앱을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="591de-116">From hello list, select hello app that you want tooset up with SSO.</span></span>  
4. <span data-ttu-id="591de-117">**Single Sign-On**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="591de-117">Select **Single sign-on**.</span></span>

   ![Single Sign-On 선택](./media/application-proxy-sso-azure-portal/select-sso.png)

5. <span data-ttu-id="591de-119">Hello SSO 모드 선택 **암호 기반 로그온**합니다.</span><span class="sxs-lookup"><span data-stu-id="591de-119">For hello SSO mode, choose **Password-based Sign-on**.</span></span>
6. <span data-ttu-id="591de-120">Hello 로그온 URL에 대 한 URL을 입력 hello hello 페이지에 대 한 사용자가 tooyour 앱 hello 회사 네트워크 외부에서 자신의 사용자 이름 및 암호 toosign를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="591de-120">For hello Sign-on URL, enter hello URL for hello page where users enter their username and password toosign in tooyour app outside of hello corporate network.</span></span> <span data-ttu-id="591de-121">이 응용 프로그램 프록시를 통해 hello 앱을 게시할 때 만들어진 외부 URL hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="591de-121">This may be hello External URL that you created when you published hello app through Application Proxy.</span></span> 

   ![암호 기반 로그온 선택 및 URL 입력](./media/application-proxy-sso-azure-portal/password-sso.png)

7. <span data-ttu-id="591de-123">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="591de-123">Select **Save**.</span></span>

<!-- Need toorepro?
7. hello page should tell you that a sign-in form was successfully detected at hello provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow hello instructions toopoint out where hello sign-in credentials go. 
-->

## <a name="test-your-app"></a><span data-ttu-id="591de-124">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="591de-124">Test your app</span></span>

<span data-ttu-id="591de-125">원격 액세스 tooyour 응용 프로그램에 대해 구성 된 tooexternal URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="591de-125">Go tooexternal URL that you configured for remote access tooyour application.</span></span> <span data-ttu-id="591de-126">이러한 앱에 대 한 자격 증명 (또는 액세스로 설정 하는 테스트 계정의 자격 증명 hello)를 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="591de-126">Sign in with your credentials for that app (or hello credentials for a test account that you set up with access).</span></span> <span data-ttu-id="591de-127">성공적으로 로그인 하면 있습니다 수 tooleave hello 앱와 자격 증명을 다시 입력 하지 않고 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="591de-127">Once you sign in successfully, you should be able tooleave hello app and come back without entering your credentials again.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="591de-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="591de-128">Next steps</span></span>

- <span data-ttu-id="591de-129">다른 방법으로 tooimplement에 대해 알아보세요 [Single sign on 응용 프로그램 프록시](application-proxy-sso-overview.md)</span><span class="sxs-lookup"><span data-stu-id="591de-129">Read about other ways tooimplement [Single sign-on with Application Proxy](application-proxy-sso-overview.md)</span></span>
- <span data-ttu-id="591de-130">[Azure AD 응용 프로그램 프록시를 사용하여 앱에 원격으로 액세스하는 경우 보안 고려 사항](application-proxy-security-considerations.md)을 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="591de-130">Learn about [Security considerations for accessing apps remotely with Azure AD Application Proxy](application-proxy-security-considerations.md)</span></span>