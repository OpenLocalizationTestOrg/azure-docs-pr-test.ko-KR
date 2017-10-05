---
title: "Azure AD Connect: Seamless Single Sign-On - 빠른 시작 | Microsoft Docs"
description: "이 문서에서는 Azure Active Directory Seamless Single Sign-On을 시작하는 방법을 설명합니다."
services: active-directory
keywords: "Azure AD Connect의 정의, Active Directory 설치, Azure AD에 대한 필수 구성 요소, SSO, Single Sign-on"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 977108687734a5eb7f7a30419de2a6bdef184d0e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a><span data-ttu-id="91f02-104">Azure Active Directory Seamless Single Sign-On: 빠른 시작</span><span class="sxs-lookup"><span data-stu-id="91f02-104">Azure Active Directory Seamless Single Sign-On: Quick start</span></span>

## <a name="how-to-deploy-seamless-sso"></a><span data-ttu-id="91f02-105">Seamless SSO를 배포하는 방법</span><span class="sxs-lookup"><span data-stu-id="91f02-105">How to deploy Seamless SSO</span></span>

<span data-ttu-id="91f02-106">Azure AD Seamless SSO(Azure Active Directory Seamless Single Sign-On)는 회사 네트워크에 연결된 회사 데스크톱에 있을 때 사용자를 자동으로 서명합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-106">Azure Active Directory Seamless Single Sign-On (Azure AD Seamless SSO) automatically signs users in when they are on their corporate desktops connected to your corporate network.</span></span> <span data-ttu-id="91f02-107">추가 온-프레미스 구성 요소가 없어도 사용자가 클라우드 기반 응용 프로그램에 쉽게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-107">It provides your users easy access to your cloud-based applications without needing any additional on-premises components.</span></span>

>[!IMPORTANT]
><span data-ttu-id="91f02-108">Seamless SSO 기능은 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-108">The Seamless SSO feature is currently in preview.</span></span>

<span data-ttu-id="91f02-109">Seamless SSO를 배포하려면 다음 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-109">To deploy Seamless SSO, you need to follow these steps:</span></span>

## <a name="step-1-check-prerequisites"></a><span data-ttu-id="91f02-110">1단계: 필수 조건 확인</span><span class="sxs-lookup"><span data-stu-id="91f02-110">Step 1: Check prerequisites</span></span>

<span data-ttu-id="91f02-111">다음 필수 조건이 충족되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-111">Ensure that the following prerequisites are in place:</span></span>

1. <span data-ttu-id="91f02-112">Azure AD Connect 서버 설정: 로그인 방법으로 [통과 인증](active-directory-aadconnect-pass-through-authentication.md)을 사용하는 경우 더 이상의 작업이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-112">Set up your Azure AD Connect server: If you use [Pass-through Authentication](active-directory-aadconnect-pass-through-authentication.md) as your sign-in method, no further action is required.</span></span> <span data-ttu-id="91f02-113">로그인 방법으로 [암호 해시 동기화](active-directory-aadconnectsync-implement-password-synchronization.md)를 사용하고 Azure AD Connect와 Azure AD 사이에 방화벽이 있는 경우 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-113">If you use [Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) as your sign-in method, and if there is a firewall between Azure AD Connect and Azure AD, ensure that:</span></span>
- <span data-ttu-id="91f02-114">Azure AD Connect 버전 1.1.484.0 이상을 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-114">You are using versions 1.1.484.0 or later of Azure AD Connect.</span></span>
- <span data-ttu-id="91f02-115">Azure AD Connect 서버에서 `*.msappproxy.net` URL 및 443 포트를 통해 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-115">Azure AD Connect can communicate with `*.msappproxy.net` URLs and over port 443.</span></span> <span data-ttu-id="91f02-116">이 필수 조건은 실제 사용자 로그인을 위해서가 아니라 해당 기능을 사용하도록 설정한 경우에만 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-116">This prerequisite is applicable only when you enable the feature, not for actual user sign-ins.</span></span>
- <span data-ttu-id="91f02-117">Azure AD Connect는 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/details.aspx?id=41653)에 직접적인 IP 연결을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-117">Azure AD Connect can make direct IP connections to the [Azure data center IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="91f02-118">다시금 이 필수 조건은 해당 기능을 사용하도록 설정한 경우에만 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-118">Again, this prerequisite is applicable only when you enable the feature.</span></span>
2. <span data-ttu-id="91f02-119">Azure AD Connect를 통해 Azure AD와 동기화하는 각 AD 포리스트에 대해, 그리고 Seamless SSO를 사용하도록 설정할 사용자에 대해 도메인 관리자 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-119">You need Domain Administrator credentials for each AD forest that you synchronize to Azure AD (using Azure AD Connect) and for whose users you want to enable Seamless SSO.</span></span>

## <a name="step-2-enable-the-feature"></a><span data-ttu-id="91f02-120">2단계: 기능 활성화</span><span class="sxs-lookup"><span data-stu-id="91f02-120">Step 2: Enable the feature</span></span>

<span data-ttu-id="91f02-121">Azure AD Seamless SSO는 [Azure AD Connect](active-directory-aadconnect.md)를 통해 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-121">Seamless SSO can be enabled using [Azure AD Connect](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="91f02-122">Azure AD Connect를 새로 설치하는 경우 [사용자 지정 설치 경로](active-directory-aadconnect-get-started-custom.md)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-122">If you are doing a fresh installation of Azure AD Connect, choose the [custom installation path](active-directory-aadconnect-get-started-custom.md).</span></span> <span data-ttu-id="91f02-123">"사용자 로그인" 페이지에서 "Single Sign-On 사용" 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-123">At the "User sign-in" page, check the "Enable single sign on" option.</span></span>

![Azure AD Connect - 사용자 로그인](./media/active-directory-aadconnect-sso/sso8.png)

<span data-ttu-id="91f02-125">Azure AD Connect가 이미 설치되어 있는 경우 Azure AD Connect에서 "사용자 로그인 변경 페이지"를 선택하고 "다음"을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-125">If you already have an installation of Azure AD Connect, choose "Change user sign-in page" on Azure AD Connect and click "Next".</span></span> <span data-ttu-id="91f02-126">그다음에 "Single Sign-On 사용" 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-126">Then check the "Enable single sign on" option.</span></span>

![Azure AD Connect - 사용자 로그인 변경](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

<span data-ttu-id="91f02-128">"Single Sign-On 사용" 페이지에 도달할 때까지 마법사를 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-128">Continue through the wizard until you get to the "Enable single sign on" page.</span></span> <span data-ttu-id="91f02-129">Azure AD Connect를 통해 Azure AD와 동기화하는 각 AD 포리스트에 대해, 그리고 Seamless SSO를 사용하도록 설정할 사용자에 대해 도메인 관리자 자격 증명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-129">Provide Domain Administrator credentials for each AD forest that you synchronize to Azure AD (using Azure AD Connect) and for whose users you want to enable Seamless SSO.</span></span> 

<span data-ttu-id="91f02-130">마법사를 완료하면 테넌트에서 SSO Seamless를 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-130">After completion of the wizard, Seamless SSO is enabled on your tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="91f02-131">도메인 관리자 자격 증명은 Azure AD Connect 또는 Azure AD에 저장되지는 않지만 이 기능을 사용하도록 설정하는 데에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-131">The Domain Administrator credentials are not stored in Azure AD Connect or in Azure AD, but are only used to enable the feature.</span></span>

<span data-ttu-id="91f02-132">다음 지침에 따라 Seamless SSO를 올바르게 설정했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-132">Follow these instructions to verify that you have enabled Seamless SSO correctly:</span></span>

1. <span data-ttu-id="91f02-133">테넌트에 대한 전역 관리자 자격 증명을 사용하여 [Azure Active Directory 관리 센터](https://aad.portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-133">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with the Global Administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="91f02-134">왼쪽 탐색에서 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-134">Select **Azure Active Directory** on the left-hand navigation.</span></span>
3. <span data-ttu-id="91f02-135">**Azure AD Connect**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-135">Select **Azure AD Connect**.</span></span>
4. <span data-ttu-id="91f02-136">**Seamless Single Sign-on** 기능이 **설정**으로 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-136">Verify that the **Seamless Single Sign-On** feature shows as **Enabled**.</span></span>

![Azure Portal - Azure AD Connect 블레이드](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-the-feature"></a><span data-ttu-id="91f02-138">3단계: 기능 배포</span><span class="sxs-lookup"><span data-stu-id="91f02-138">Step 3: Roll out the feature</span></span>

<span data-ttu-id="91f02-139">이 기능을 사용자에게 배포하려면 Active Directory의 그룹 정책을 통해 사용자의 인트라넷 영역 설정에 두 개의 Azure AD URL(https://autologon.microsoftazuread-sso.com 및 https://aadg.windows.net.nsatc.net)을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-139">To roll out the feature to your users, you need to add two Azure AD URLs (https://autologon.microsoftazuread-sso.com and https://aadg.windows.net.nsatc.net) to users' Intranet zone settings via Group Policy in Active Directory.</span></span>

>[!NOTE]
> <span data-ttu-id="91f02-140">다음 지침은 Windows의 Internet Explorer 및 Google Chrome(Internet Explorer와 신뢰할 수 있는 사이트 URL 집합을 공유하는 경우)에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-140">The following instructions only work for Internet Explorer and Google Chrome on Windows  (if it shares set of trusted site URLs with Internet Explorer).</span></span> <span data-ttu-id="91f02-141">Mac에서 Mozilla Firefox 및 Chrome을 설정하는 지침은 다음 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91f02-141">Read the next section for instructions to set up Mozilla Firefox and Google Chrome on Mac.</span></span>

### <a name="why-do-you-need-to-modify-users-intranet-zone-settings"></a><span data-ttu-id="91f02-142">사용자의 인트라넷 영역 설정을 수정해야 하는 이유</span><span class="sxs-lookup"><span data-stu-id="91f02-142">Why do you need to modify users' Intranet zone settings?</span></span>

<span data-ttu-id="91f02-143">기본적으로 브라우저는 URL에서 올바른 영역(인터넷 또는 인트라넷)을 자동으로 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-143">By default, the browser automatically calculates the right zone (Internet or Intranet) from a URL.</span></span> <span data-ttu-id="91f02-144">예를 들어 http://contoso/는 인트라넷 영역에 매핑되지만, http://intranet.contoso.com/은 인터넷 영역에 매핑됩니다(URL에 마침표가 포함되어 있기 때문).</span><span class="sxs-lookup"><span data-stu-id="91f02-144">For example, http://contoso/ is mapped to the Intranet zone, whereas http://intranet.contoso.com/ is mapped to the Internet zone (because the URL contains a period).</span></span> <span data-ttu-id="91f02-145">브라우저는 URL이 브라우저의 인트라넷 영역에 명시적으로 추가되지 않는 한 클라우드 끝점(예: 두 개의 Azure AD URL)에 Kerberos 티켓을 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-145">Browsers don't send Kerberos tickets to a cloud endpoint - like the two Azure AD URLs - unless its URL is explicitly added to the browser's Intranet zone.</span></span>

### <a name="detailed-steps"></a><span data-ttu-id="91f02-146">자세한 단계</span><span class="sxs-lookup"><span data-stu-id="91f02-146">Detailed steps</span></span>

1. <span data-ttu-id="91f02-147">그룹 정책 관리 도구를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-147">Open the Group Policy Management tool.</span></span>
2. <span data-ttu-id="91f02-148">일부 또는 모든 사용자에게 적용되는 그룹 정책을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-148">Edit the Group Policy that is applied to some or all your users.</span></span> <span data-ttu-id="91f02-149">이 예에서는 **기본 도메인 정책**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-149">In this example, we use the **Default Domain Policy**.</span></span>
3. <span data-ttu-id="91f02-150">**User Configuration\Administrative Templates\Windows Components\Internet Explorer\Internet Control Panel\Security Page**로 이동하고 **영역에 대한 사이트 할당 목록**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-150">Navigate to **User Configuration\Administrative Templates\Windows Components\Internet Explorer\Internet Control Panel\Security Page** and select **Site to Zone Assignment List**.</span></span>
<span data-ttu-id="91f02-151">![Single Sign-On](./media/active-directory-aadconnect-sso/sso6.png)</span><span class="sxs-lookup"><span data-stu-id="91f02-151">![Single sign-on](./media/active-directory-aadconnect-sso/sso6.png)</span></span>  
4. <span data-ttu-id="91f02-152">정책을 활성화하고 대화 상자에 다음 값(Kerberos 티켓이 전달되는 Azure AD URL) 및 데이터(*1*은 인트라넷 영역을 나타냄)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-152">Enable the policy, and enter the following values (Azure AD URLs where Kerberos tickets are forwarded) and data (*1* indicates Intranet zone) in the dialog box.</span></span>

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> <span data-ttu-id="91f02-153">일부 사용자가 공유 키오스크에 로그인하는 경우와 같이 이러한 사용자가 Seamless SSO를 사용하지 못하게 하려면 이전 값을 *4*로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-153">If you want to disallow some users from using Seamless SSO - for instance, if these users are signing in on shared kiosks - set the preceding values to *4*.</span></span> <span data-ttu-id="91f02-154">이 작업은 Azure AD URL을 [제한된 영역]에 추가하고 Seamless SSO가 항상 실패하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-154">This action adds the Azure AD URLs to the Restricted Zone, and fails Seamless SSO all the time.</span></span>

5. <span data-ttu-id="91f02-155">**확인**을 클릭하고 **확인**을 다시 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-155">Click **OK** and **OK** again.</span></span>

![SSO(Single sign-on)](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a><span data-ttu-id="91f02-157">브라우저 고려 사항</span><span class="sxs-lookup"><span data-stu-id="91f02-157">Browser considerations</span></span>

#### <a name="mozilla-firefox"></a><span data-ttu-id="91f02-158">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="91f02-158">Mozilla Firefox</span></span>

<span data-ttu-id="91f02-159">Mozilla Firefox는 Kerberos 인증을 자동으로 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-159">Mozilla Firefox doesn't automatically do Kerberos Authentication.</span></span> <span data-ttu-id="91f02-160">각 사용자는 다음 단계에 따라 Firefox 설정에 Azure AD URL을 수동으로 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-160">Each user has to manually add the Azure AD URLs to their Firefox settings using the following steps:</span></span>
1. <span data-ttu-id="91f02-161">Firefox를 실행하고 주소 표시줄에 `about:config`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-161">Run Firefox and enter `about:config` in the address bar.</span></span> <span data-ttu-id="91f02-162">표시되는 모든 알림을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-162">Dismiss any notifications that you see.</span></span>
2. <span data-ttu-id="91f02-163">**network.negotiate-auth.trusted-uris** 기본 설정을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-163">Search for the **network.negotiate-auth.trusted-uris** preference.</span></span> <span data-ttu-id="91f02-164">이 기본 설정은 Firefox의 신뢰할 수 있는 Kerberos 인증 사이트를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-164">This preference lists Firefox's trusted sites for Kerberos authentication.</span></span>
3. <span data-ttu-id="91f02-165">마우스 오른쪽 단추로 클릭하고 "수정"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-165">Right-click and select "Modify".</span></span>
4. <span data-ttu-id="91f02-166">필드에서 "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net"을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-166">Enter "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" in the field.</span></span>
5. <span data-ttu-id="91f02-167">"확인"을 클릭하고 브라우저를 다시 엽니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-167">Click "OK" and reopen the browser.</span></span>

#### <a name="safari-on-mac-os"></a><span data-ttu-id="91f02-168">Mac OS의 Safari</span><span class="sxs-lookup"><span data-stu-id="91f02-168">Safari on Mac OS</span></span>

<span data-ttu-id="91f02-169">Mac OS를 실행하는 컴퓨터가 AD에 가입되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-169">Ensure that the machine running Mac OS is joined to AD.</span></span> <span data-ttu-id="91f02-170">작업을 수행하는 방법에 대한 지침을 [여기](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91f02-170">See instructions on how to do that [here](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span></span>

#### <a name="google-chrome-on-mac-os"></a><span data-ttu-id="91f02-171">Mac OS의 Google 크롬</span><span class="sxs-lookup"><span data-stu-id="91f02-171">Google Chrome on Mac OS</span></span>

<span data-ttu-id="91f02-172">Mac OS 및 기타 Windows가 아닌 플랫폼에서 Google 크롬의 경우 통합 인증을 위해 Azure AD URL을 허용 목록에 추가하는 방법은 [이 문서](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91f02-172">For Google Chrome on Mac OS and other non-Windows platforms, refer to [this article](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) for information on how to whitelist the Azure AD URLs for integrated authentication.</span></span>

<span data-ttu-id="91f02-173">타사 Active Directory 그룹 정책 확장을 사용하여 Mac 사용자의 Firefox 및 Google Chrome에 Azure AD URL을 배포하는 방법은 이 문서의 범위를 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-173">Using third-party Active Directory Group Policy extensions to roll out the Azure AD URLs to Firefox and Google Chrome on Mac users is outside of this article's scope.</span></span>

#### <a name="known-limitations"></a><span data-ttu-id="91f02-174">알려진 제한 사항</span><span class="sxs-lookup"><span data-stu-id="91f02-174">Known limitations</span></span>

<span data-ttu-id="91f02-175">Firefox 및 Edge 브라우저의 개인 검색 모드에서는 Seamless SSO가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-175">Seamless SSO doesn't work in private browsing mode on Firefox and Edge browsers.</span></span> <span data-ttu-id="91f02-176">또한 브라우저가 고급 보호 모드에서 실행 중인 경우 Internet Explorer에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-176">It also doesn't work on Internet Explorer if the browser is running in Enhanced Protection mode.</span></span>

>[!IMPORTANT]
><span data-ttu-id="91f02-177">최근 고객이 신고한 문제를 조사하기 위해 에지에 대한 지원을 롤백했습니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-177">We recently rolled back support for Edge to investigate customer-reported issues.</span></span>

## <a name="step-4-test-the-feature"></a><span data-ttu-id="91f02-178">4단계: 기능 테스트</span><span class="sxs-lookup"><span data-stu-id="91f02-178">Step 4: Test the feature</span></span>

<span data-ttu-id="91f02-179">특정 사용자에 대한 기능을 테스트하려면 다음 조건이 _모두_ 제대로 갖추어져 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-179">To test the feature for a specific user, ensure that _all_ the following conditions are in place:</span></span>
  - <span data-ttu-id="91f02-180">사용자가 회사 장치에 로그인하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-180">The user is signing in on a corporate device.</span></span>
  - <span data-ttu-id="91f02-181">장치가 이전에 AD(Active Directory) 도메인에 가입되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-181">The device has been previously joined to your Active Directory (AD) domain.</span></span>
  - <span data-ttu-id="91f02-182">장치는 회사의 유선/무선 네트워크 또는 원격 액세스 연결(예: VPN 연결)을 통해 DC(도메인 컨트롤러)에 직접 연결되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-182">The device has a direct connection to your Domain Controller (DC), either on the corporate wired or wireless network or via a remote access connection, such as a VPN connection.</span></span>
  - <span data-ttu-id="91f02-183">그룹 정책을 사용하여 해당 사용자에게 [기능을 배포](##step-3-roll-out-the-feature)했습니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-183">You have [rolled out the feature](##step-3-roll-out-the-feature) to this user using Group Policy.</span></span>

<span data-ttu-id="91f02-184">사용자가 암호가 아니라 사용자 이름만 입력하는 시나리오를 테스트하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-184">To test the scenario where the user enters only the username, but not the password:</span></span>
- <span data-ttu-id="91f02-185">새 개인 브라우저 세션에서 *https://myapps.microsoft.com/*에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-185">Sign into *https://myapps.microsoft.com/* in a new private browser session.</span></span>

<span data-ttu-id="91f02-186">사용자가 사용자 이름이나 암호를 입력할 필요가 없는 시나리오를 테스트하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-186">To test the scenario where the user doesn't have to enter the username or the password:</span></span> 
- <span data-ttu-id="91f02-187">새 개인 브라우저 세션에서 *https://myapps.microsoft.com/contoso.onmicrosoft.com*에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-187">Sign into *https://myapps.microsoft.com/contoso.onmicrosoft.com* in a new private browser session.</span></span> <span data-ttu-id="91f02-188">"*contoso*"를 테넌트의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-188">Replace "*contoso*" with your tenant's name.</span></span>
- <span data-ttu-id="91f02-189">또는 새 개인 브라우저 세션에서 *https://myapps.microsoft.com/contoso.com*에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-189">Or sign into *https://myapps.microsoft.com/contoso.com* in a new private browser session.</span></span> <span data-ttu-id="91f02-190">"*contoso.com*"을 테넌트에서 확인된 도메인(페더레이션 도메인이 아님)으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-190">Replace "*contoso.com*" with a verified domain (not a federated domain) in your tenant.</span></span>

## <a name="step-5-roll-over-keys"></a><span data-ttu-id="91f02-191">5단계: 키 롤오버</span><span class="sxs-lookup"><span data-stu-id="91f02-191">Step 5: Roll over keys</span></span>

<span data-ttu-id="91f02-192">2단계에서, Azure AD Connect는 Seamless SSO를 사용하도록 설정한 모든 AD 포리스트에서 컴퓨터 계정(Azure AD를 나타냄)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-192">In Step 2, Azure AD Connect creates computer accounts (representing Azure AD) in all the AD forests on which you have enabled Seamless SSO.</span></span> <span data-ttu-id="91f02-193">[여기](active-directory-aadconnect-sso-how-it-works.md)에서 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="91f02-193">Learn more in detail [here](active-directory-aadconnect-sso-how-it-works.md).</span></span> <span data-ttu-id="91f02-194">향상된 보안을 위해 이러한 컴퓨터 계정의 Kerberos 암호 해독 키를 자주 롤오버하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-194">For improved security, it is recommended that  you frequently roll over the Kerberos decryption keys of these computer accounts.</span></span>

>[!IMPORTANT]
><span data-ttu-id="91f02-195">이 기능을 사용하도록 설정한 후에는 이 단계를 _즉시_ 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-195">You don't need to do this step _immediately_ after you have enabled the feature.</span></span> <span data-ttu-id="91f02-196">적어도 30일마다 Kerberos 암호 해독 키를 롤오버합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-196">Roll over the Kerberos decryption keys at least every 30 days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="91f02-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="91f02-197">Next steps</span></span>

- <span data-ttu-id="91f02-198">[**기술 심층 분석**](active-directory-aadconnect-sso-how-it-works.md) - 이 기능의 작동 방식을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-198">[**Technical Deep Dive**](active-directory-aadconnect-sso-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="91f02-199">[**FAQ(질문과 대답)**](active-directory-aadconnect-sso-faq.md) - 질문과 대답을 다루고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-199">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="91f02-200">[**문제 해결**](active-directory-aadconnect-troubleshoot-sso.md) - 기능과 관련된 일반적인 문제를 해결하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-200">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="91f02-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 새로운 기능 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="91f02-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
