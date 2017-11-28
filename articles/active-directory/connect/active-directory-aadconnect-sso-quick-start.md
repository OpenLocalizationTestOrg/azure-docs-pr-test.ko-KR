---
title: "Azure AD Connect: Seamless Single Sign-On - 빠른 시작 | Microsoft Docs"
description: "이 문서에서는 Azure Active Directory 원활한 Single Sign-on을 tooget 시작 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 97d40ed41b3bfad9ff7e11ddbdb8de594ee85de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a><span data-ttu-id="888b6-104">Azure Active Directory Seamless Single Sign-On: 빠른 시작</span><span class="sxs-lookup"><span data-stu-id="888b6-104">Azure Active Directory Seamless Single Sign-On: Quick start</span></span>

## <a name="how-toodeploy-seamless-sso"></a><span data-ttu-id="888b6-105">어떻게 toodeploy 원활한 SSO</span><span class="sxs-lookup"><span data-stu-id="888b6-105">How toodeploy Seamless SSO</span></span>

<span data-ttu-id="888b6-106">Azure Active Directory 원활한 Single Sign-on (Azure AD 원활한 SSO) 자동으로 사용자가 자신의 회사 데스크톱 연결 된 tooyour 회사 네트워크에서 서로에 서명 합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-106">Azure Active Directory Seamless Single Sign-On (Azure AD Seamless SSO) automatically signs users in when they are on their corporate desktops connected tooyour corporate network.</span></span> <span data-ttu-id="888b6-107">에 사용자가 쉽게 액세스할 tooyour 클라우드 기반 응용 프로그램 추가 온-프레미스 구성 요소 필요 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-107">It provides your users easy access tooyour cloud-based applications without needing any additional on-premises components.</span></span>

>[!IMPORTANT]
><span data-ttu-id="888b6-108">hello 원활한 SSO 기능은 현재 미리 보기 중입니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-108">hello Seamless SSO feature is currently in preview.</span></span>

<span data-ttu-id="888b6-109">toofollow 해야 원활한 SSO toodeploy 다음이 단계:</span><span class="sxs-lookup"><span data-stu-id="888b6-109">toodeploy Seamless SSO, you need toofollow these steps:</span></span>

## <a name="step-1-check-prerequisites"></a><span data-ttu-id="888b6-110">1단계: 필수 조건 확인</span><span class="sxs-lookup"><span data-stu-id="888b6-110">Step 1: Check prerequisites</span></span>

<span data-ttu-id="888b6-111">필수 구성 요소를 다음 해당 hello 적절 한지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-111">Ensure that hello following prerequisites are in place:</span></span>

1. <span data-ttu-id="888b6-112">Azure AD Connect 서버 설정: 로그인 방법으로 [통과 인증](active-directory-aadconnect-pass-through-authentication.md)을 사용하는 경우 더 이상의 작업이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-112">Set up your Azure AD Connect server: If you use [Pass-through Authentication](active-directory-aadconnect-pass-through-authentication.md) as your sign-in method, no further action is required.</span></span> <span data-ttu-id="888b6-113">로그인 방법으로 [암호 해시 동기화](active-directory-aadconnectsync-implement-password-synchronization.md)를 사용하고 Azure AD Connect와 Azure AD 사이에 방화벽이 있는 경우 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-113">If you use [Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) as your sign-in method, and if there is a firewall between Azure AD Connect and Azure AD, ensure that:</span></span>
- <span data-ttu-id="888b6-114">Azure AD Connect 버전 1.1.484.0 이상을 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-114">You are using versions 1.1.484.0 or later of Azure AD Connect.</span></span>
- <span data-ttu-id="888b6-115">Azure AD Connect 서버에서 `*.msappproxy.net` URL 및 443 포트를 통해 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-115">Azure AD Connect can communicate with `*.msappproxy.net` URLs and over port 443.</span></span> <span data-ttu-id="888b6-116">이 필수 구성이 요소는 실제 사용자 로그인에 대해 hello 기능을 사용 하도록 설정 하는 경우에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-116">This prerequisite is applicable only when you enable hello feature, not for actual user sign-ins.</span></span>
- <span data-ttu-id="888b6-117">Azure AD Connect 직접 IP 연결 toohello 정확해 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/details.aspx?id=41653)합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-117">Azure AD Connect can make direct IP connections toohello [Azure data center IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="888b6-118">다시이 필수 구성이 요소는 hello 기능을 사용 하는 경우에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-118">Again, this prerequisite is applicable only when you enable hello feature.</span></span>
2. <span data-ttu-id="888b6-119">TooAzure AD를 동기화 하는 각 AD 포리스트에 대 한 도메인 관리자 자격 증명 필요 (Azure AD Connect를 사용 하 여) 및 원하는 tooenable 원활한 SSO 조직과 사용자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-119">You need Domain Administrator credentials for each AD forest that you synchronize tooAzure AD (using Azure AD Connect) and for whose users you want tooenable Seamless SSO.</span></span>

## <a name="step-2-enable-hello-feature"></a><span data-ttu-id="888b6-120">2 단계: hello 기능 사용</span><span class="sxs-lookup"><span data-stu-id="888b6-120">Step 2: Enable hello feature</span></span>

<span data-ttu-id="888b6-121">Azure AD Seamless SSO는 [Azure AD Connect](active-directory-aadconnect.md)를 통해 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-121">Seamless SSO can be enabled using [Azure AD Connect](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="888b6-122">Azure AD Connect의 새로 설치를 수행 하는 경우 선택 hello [사용자 지정 설치 경로가](active-directory-aadconnect-get-started-custom.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-122">If you are doing a fresh installation of Azure AD Connect, choose hello [custom installation path](active-directory-aadconnect-get-started-custom.md).</span></span> <span data-ttu-id="888b6-123">페이지 "사용자 로그인" hello hello "Enable single sign on" 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-123">At hello "User sign-in" page, check hello "Enable single sign on" option.</span></span>

![Azure AD Connect - 사용자 로그인](./media/active-directory-aadconnect-sso/sso8.png)

<span data-ttu-id="888b6-125">Azure AD Connect가 이미 설치되어 있는 경우 Azure AD Connect에서 "사용자 로그인 변경 페이지"를 선택하고 "다음"을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-125">If you already have an installation of Azure AD Connect, choose "Change user sign-in page" on Azure AD Connect and click "Next".</span></span> <span data-ttu-id="888b6-126">Hello "Enable single sign on" 옵션을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-126">Then check hello "Enable single sign on" option.</span></span>

![Azure AD Connect - 사용자 로그인 변경](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

<span data-ttu-id="888b6-128">Toohello "Enable single sign on" 페이지에 도달할 때까지 hello 마법사를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-128">Continue through hello wizard until you get toohello "Enable single sign on" page.</span></span> <span data-ttu-id="888b6-129">TooAzure AD를 동기화 하는 각 AD 포리스트에 대 한 도메인 관리자 자격 증명을 제공 (Azure AD Connect를 사용 하 여) 및 원하는 tooenable 원활한 SSO 조직과 사용자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-129">Provide Domain Administrator credentials for each AD forest that you synchronize tooAzure AD (using Azure AD Connect) and for whose users you want tooenable Seamless SSO.</span></span> 

<span data-ttu-id="888b6-130">Hello 마법사를 완료 한 후 테 넌 트에 원활한 SSO는 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-130">After completion of hello wizard, Seamless SSO is enabled on your tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="888b6-131">hello 도메인 관리자 자격 증명이 Azure AD 또는 Azure AD Connect에 저장 되지 않습니다 않는 사용 되는 tooenable hello 기능.</span><span class="sxs-lookup"><span data-stu-id="888b6-131">hello Domain Administrator credentials are not stored in Azure AD Connect or in Azure AD, but are only used tooenable hello feature.</span></span>

<span data-ttu-id="888b6-132">이러한 지침은 tooverify 원활한 SSO을 올바르게 설정 했는지를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-132">Follow these instructions tooverify that you have enabled Seamless SSO correctly:</span></span>

1. <span data-ttu-id="888b6-133">Toohello 로그인 [Azure Active Directory 관리 센터](https://aad.portal.azure.com) 테 넌 트에 대 한 hello 전역 관리자 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-133">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with hello Global Administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="888b6-134">선택 **Azure Active Directory** hello 왼쪽 탐색 모음에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-134">Select **Azure Active Directory** on hello left-hand navigation.</span></span>
3. <span data-ttu-id="888b6-135">**Azure AD Connect**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-135">Select **Azure AD Connect**.</span></span>
4. <span data-ttu-id="888b6-136">해당 hello 확인 **원활한 Single Sign-on** 기능으로 표시 **Enabled**합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-136">Verify that hello **Seamless Single Sign-On** feature shows as **Enabled**.</span></span>

![Azure Portal - Azure AD Connect 블레이드](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-hello-feature"></a><span data-ttu-id="888b6-138">3 단계: 롤아웃 hello 기능</span><span class="sxs-lookup"><span data-stu-id="888b6-138">Step 3: Roll out hello feature</span></span>

<span data-ttu-id="888b6-139">tooroll hello 기능 tooyour 사용자가 Active Directory에서 그룹 정책을 통해 tooadd 두 (https://autologon.microsoftazuread-sso.com 및 https://aadg.windows.net.nsatc.net) Azure AD Url toousers' 인트라넷 영역 설정 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-139">tooroll out hello feature tooyour users, you need tooadd two Azure AD URLs (https://autologon.microsoftazuread-sso.com and https://aadg.windows.net.nsatc.net) toousers' Intranet zone settings via Group Policy in Active Directory.</span></span>

>[!NOTE]
> <span data-ttu-id="888b6-140">hello (Internet Explorer와 신뢰할 수 있는 사이트 Url의 집합을 공유) 하는 경우 Windows에서 Internet Explorer 및 Google Chrome에 대 한 지침만 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-140">hello following instructions only work for Internet Explorer and Google Chrome on Windows  (if it shares set of trusted site URLs with Internet Explorer).</span></span> <span data-ttu-id="888b6-141">Mozilla Firefox 및 Google Chrome mac을 tooset 지침에 대 한 hello 다음 섹션을 읽어</span><span class="sxs-lookup"><span data-stu-id="888b6-141">Read hello next section for instructions tooset up Mozilla Firefox and Google Chrome on Mac.</span></span>

### <a name="why-do-you-need-toomodify-users-intranet-zone-settings"></a><span data-ttu-id="888b6-142">Toomodify 사용자 인트라넷 영역 설정을 왜 필요 합니까?</span><span class="sxs-lookup"><span data-stu-id="888b6-142">Why do you need toomodify users' Intranet zone settings?</span></span>

<span data-ttu-id="888b6-143">기본적으로 hello 브라우저 URL에서 hello 오른쪽 영역 (인터넷 또는 인트라넷) 자동으로 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-143">By default, hello browser automatically calculates hello right zone (Internet or Intranet) from a URL.</span></span> <span data-ttu-id="888b6-144">예를 들어 http://contoso/ 인 매핑된 toohello 인트라넷 영역 반면 http://intranet.contoso.com/ 매핑된 toohello 인터넷 영역 (하기 때문에 마침표를 포함 하는 hello URL).</span><span class="sxs-lookup"><span data-stu-id="888b6-144">For example, http://contoso/ is mapped toohello Intranet zone, whereas http://intranet.contoso.com/ is mapped toohello Internet zone (because hello URL contains a period).</span></span> <span data-ttu-id="888b6-145">해당 URL toohello 브라우저의 인트라넷 영역 명시적으로 추가 하지 않는 브라우저 hello 두 개의 Azure AD Url--같은 Kerberos 티켓 tooa 클라우드 끝점을 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-145">Browsers don't send Kerberos tickets tooa cloud endpoint - like hello two Azure AD URLs - unless its URL is explicitly added toohello browser's Intranet zone.</span></span>

### <a name="detailed-steps"></a><span data-ttu-id="888b6-146">자세한 단계</span><span class="sxs-lookup"><span data-stu-id="888b6-146">Detailed steps</span></span>

1. <span data-ttu-id="888b6-147">Hello 그룹 정책 관리 도구를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-147">Open hello Group Policy Management tool.</span></span>
2. <span data-ttu-id="888b6-148">Hello 적용된 toosome 또는 모든 사용자가 그룹 정책을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-148">Edit hello Group Policy that is applied toosome or all your users.</span></span> <span data-ttu-id="888b6-149">이 예제에서는 사용 하 여 hello **기본 도메인 정책**합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-149">In this example, we use hello **Default Domain Policy**.</span></span>
3. <span data-ttu-id="888b6-150">너무 이동**사용자 구성 \ 관리 템플릿 \ Components\Internet 보게 제어 Panel\Security 페이지** 선택 **사이트 할당 목록 tooZone**합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-150">Navigate too**User Configuration\Administrative Templates\Windows Components\Internet Explorer\Internet Control Panel\Security Page** and select **Site tooZone Assignment List**.</span></span>
<span data-ttu-id="888b6-151">![Single Sign-On](./media/active-directory-aadconnect-sso/sso6.png)</span><span class="sxs-lookup"><span data-stu-id="888b6-151">![Single sign-on](./media/active-directory-aadconnect-sso/sso6.png)</span></span>  
4. <span data-ttu-id="888b6-152">Hello 정책을 사용 하도록 설정 하 고 다음 값 (Azure AD Url Kerberos 티켓 전달 되어)에 hello 및 데이터 입력 (*1* 인트라넷 영역을 나타냅니다) hello 대화 상자에서.</span><span class="sxs-lookup"><span data-stu-id="888b6-152">Enable hello policy, and enter hello following values (Azure AD URLs where Kerberos tickets are forwarded) and data (*1* indicates Intranet zone) in hello dialog box.</span></span>

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> <span data-ttu-id="888b6-153">Toodisallow 원활한 SSO 액세스를 사용 하 여 예를 들어, 일부 사용자가 이러한 사용자가 공유 키오스크-에 로그인 하는 경우 설정 값 앞에 너무 hello*4*합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-153">If you want toodisallow some users from using Seamless SSO - for instance, if these users are signing in on shared kiosks - set hello preceding values too*4*.</span></span> <span data-ttu-id="888b6-154">이 작업 hello Azure AD Url toohello 제한 된 사이트 영역에 추가 하 고 원활한 SSO hello 항상 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-154">This action adds hello Azure AD URLs toohello Restricted Zone, and fails Seamless SSO all hello time.</span></span>

5. <span data-ttu-id="888b6-155">**확인**을 클릭하고 **확인**을 다시 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-155">Click **OK** and **OK** again.</span></span>

![SSO(Single sign-on)](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a><span data-ttu-id="888b6-157">브라우저 고려 사항</span><span class="sxs-lookup"><span data-stu-id="888b6-157">Browser considerations</span></span>

#### <a name="mozilla-firefox"></a><span data-ttu-id="888b6-158">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="888b6-158">Mozilla Firefox</span></span>

<span data-ttu-id="888b6-159">Mozilla Firefox는 Kerberos 인증을 자동으로 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-159">Mozilla Firefox doesn't automatically do Kerberos Authentication.</span></span> <span data-ttu-id="888b6-160">각 사용자에 게 toomanually 단계를 수행 하는 hello를 사용 하 여 Azure AD hello Url tootheir Firefox 설정을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-160">Each user has toomanually add hello Azure AD URLs tootheir Firefox settings using hello following steps:</span></span>
1. <span data-ttu-id="888b6-161">Firefox를 실행 하 고 입력 `about:config` hello 주소 표시줄에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-161">Run Firefox and enter `about:config` in hello address bar.</span></span> <span data-ttu-id="888b6-162">표시되는 모든 알림을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-162">Dismiss any notifications that you see.</span></span>
2. <span data-ttu-id="888b6-163">Hello에 대 한 검색 **network.negotiate-auth.trusted-uri** 기본 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-163">Search for hello **network.negotiate-auth.trusted-uris** preference.</span></span> <span data-ttu-id="888b6-164">이 기본 설정은 Firefox의 신뢰할 수 있는 Kerberos 인증 사이트를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-164">This preference lists Firefox's trusted sites for Kerberos authentication.</span></span>
3. <span data-ttu-id="888b6-165">마우스 오른쪽 단추로 클릭하고 "수정"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-165">Right-click and select "Modify".</span></span>
4. <span data-ttu-id="888b6-166">입력 "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" hello 필드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-166">Enter "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" in hello field.</span></span>
5. <span data-ttu-id="888b6-167">"확인"을 클릭 하 고 hello 브라우저를 다시 여세요.</span><span class="sxs-lookup"><span data-stu-id="888b6-167">Click "OK" and reopen hello browser.</span></span>

#### <a name="safari-on-mac-os"></a><span data-ttu-id="888b6-168">Mac OS의 Safari</span><span class="sxs-lookup"><span data-stu-id="888b6-168">Safari on Mac OS</span></span>

<span data-ttu-id="888b6-169">Mac OS를 실행 하는 hello 컴퓨터 조인된 tooAD 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="888b6-169">Ensure that hello machine running Mac OS is joined tooAD.</span></span> <span data-ttu-id="888b6-170">방법에 지침을 참조 하십시오. toodo 하 [여기](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf)합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-170">See instructions on how toodo that [here](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span></span>

#### <a name="google-chrome-on-mac-os"></a><span data-ttu-id="888b6-171">Mac OS의 Google 크롬</span><span class="sxs-lookup"><span data-stu-id="888b6-171">Google Chrome on Mac OS</span></span>

<span data-ttu-id="888b6-172">Mac OS 및 기타 Windows 이외의 플랫폼에서 Google Chrome에 대 한 참조 너무[이 여기서](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) toowhitelist 통합된 인증에 대 한 Azure AD Url hello 하는 방법에 대 한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-172">For Google Chrome on Mac OS and other non-Windows platforms, refer too[this article](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) for information on how toowhitelist hello Azure AD URLs for integrated authentication.</span></span>

<span data-ttu-id="888b6-173">제 3 자 Active Directory 그룹 정책을 사용 하 여 Mac 사용자에 게 Azure AD Url tooFirefox hello 및 Google Chrome 확장 tooroll가이 문서의 범위를 벗어난 경우</span><span class="sxs-lookup"><span data-stu-id="888b6-173">Using third-party Active Directory Group Policy extensions tooroll out hello Azure AD URLs tooFirefox and Google Chrome on Mac users is outside of this article's scope.</span></span>

#### <a name="known-limitations"></a><span data-ttu-id="888b6-174">알려진 제한 사항</span><span class="sxs-lookup"><span data-stu-id="888b6-174">Known limitations</span></span>

<span data-ttu-id="888b6-175">Firefox 및 Edge 브라우저의 개인 검색 모드에서는 Seamless SSO가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-175">Seamless SSO doesn't work in private browsing mode on Firefox and Edge browsers.</span></span> <span data-ttu-id="888b6-176">또한 실행 되지 Internet Explorer hello 브라우저 확장 된 보호 모드에서 실행 중인 경우.</span><span class="sxs-lookup"><span data-stu-id="888b6-176">It also doesn't work on Internet Explorer if hello browser is running in Enhanced Protection mode.</span></span>

>[!IMPORTANT]
><span data-ttu-id="888b6-177">에서는 최근에 롤백 가장자리 tooinvestigate에 대 한 지원 고객이 신고한 문제.</span><span class="sxs-lookup"><span data-stu-id="888b6-177">We recently rolled back support for Edge tooinvestigate customer-reported issues.</span></span>

## <a name="step-4-test-hello-feature"></a><span data-ttu-id="888b6-178">4 단계: hello 기능 테스트</span><span class="sxs-lookup"><span data-stu-id="888b6-178">Step 4: Test hello feature</span></span>

<span data-ttu-id="888b6-179">특정 사용자에 대 한 tootest hello 기능을 확인할 _모든_ hello 다음 조건이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-179">tootest hello feature for a specific user, ensure that _all_ hello following conditions are in place:</span></span>
  - <span data-ttu-id="888b6-180">hello 사용자가 회사 장치 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-180">hello user is signing in on a corporate device.</span></span>
  - <span data-ttu-id="888b6-181">hello 장치를 이전에 결합 된 tooyour Active Directory (AD) 도메인 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-181">hello device has been previously joined tooyour Active Directory (AD) domain.</span></span>
  - <span data-ttu-id="888b6-182">hello 장치에 직접 연결 tooyour DC (도메인 컨트롤러)를 찾거나 hello 회사 유선 또는 무선 네트워크에 VPN 연결과 같이 원격 액세스 연결을 통해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-182">hello device has a direct connection tooyour Domain Controller (DC), either on hello corporate wired or wireless network or via a remote access connection, such as a VPN connection.</span></span>
  - <span data-ttu-id="888b6-183">있는 [hello 기능 롤아웃](##step-3-roll-out-the-feature) toothis 사용자 그룹 정책을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-183">You have [rolled out hello feature](##step-3-roll-out-the-feature) toothis user using Group Policy.</span></span>

<span data-ttu-id="888b6-184">tootest hello 시나리오 hello 사용자가 hello 사용자 이름, 하지만 하지 hello 암호를 입력 하는 위치:</span><span class="sxs-lookup"><span data-stu-id="888b6-184">tootest hello scenario where hello user enters only hello username, but not hello password:</span></span>
- <span data-ttu-id="888b6-185">새 개인 브라우저 세션에서 *https://myapps.microsoft.com/*에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-185">Sign into *https://myapps.microsoft.com/* in a new private browser session.</span></span>

<span data-ttu-id="888b6-186">tootest hello 시나리오를 hello 권한이 없습니다. tooenter hello 사용자 이름 또는 hello 암호:</span><span class="sxs-lookup"><span data-stu-id="888b6-186">tootest hello scenario where hello user doesn't have tooenter hello username or hello password:</span></span> 
- <span data-ttu-id="888b6-187">새 개인 브라우저 세션에서 *https://myapps.microsoft.com/contoso.onmicrosoft.com*에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-187">Sign into *https://myapps.microsoft.com/contoso.onmicrosoft.com* in a new private browser session.</span></span> <span data-ttu-id="888b6-188">"*contoso*"를 테넌트의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-188">Replace "*contoso*" with your tenant's name.</span></span>
- <span data-ttu-id="888b6-189">또는 새 개인 브라우저 세션에서 *https://myapps.microsoft.com/contoso.com*에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-189">Or sign into *https://myapps.microsoft.com/contoso.com* in a new private browser session.</span></span> <span data-ttu-id="888b6-190">"*contoso.com*"을 테넌트에서 확인된 도메인(페더레이션 도메인이 아님)으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-190">Replace "*contoso.com*" with a verified domain (not a federated domain) in your tenant.</span></span>

## <a name="step-5-roll-over-keys"></a><span data-ttu-id="888b6-191">5단계: 키 롤오버</span><span class="sxs-lookup"><span data-stu-id="888b6-191">Step 5: Roll over keys</span></span>

<span data-ttu-id="888b6-192">2 단계에서에서 Azure AD Connect를 사용 하도록 설정한 원활한 SSO 모든 hello AD 포리스트에의 컴퓨터 계정 (Azure AD를 나타냄)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-192">In Step 2, Azure AD Connect creates computer accounts (representing Azure AD) in all hello AD forests on which you have enabled Seamless SSO.</span></span> <span data-ttu-id="888b6-193">[여기](active-directory-aadconnect-sso-how-it-works.md)에서 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="888b6-193">Learn more in detail [here](active-directory-aadconnect-sso-how-it-works.md).</span></span> <span data-ttu-id="888b6-194">보안 향상된을 위해 이러한 컴퓨터 계정의 hello Kerberos 암호 해독 키를 자주 롤오버는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-194">For improved security, it is recommended that  you frequently roll over hello Kerberos decryption keys of these computer accounts.</span></span>

>[!IMPORTANT]
><span data-ttu-id="888b6-195">이 단계 toodo 필요 하지 않습니다 _즉시_ hello 기능을 활성화 한 경우.</span><span class="sxs-lookup"><span data-stu-id="888b6-195">You don't need toodo this step _immediately_ after you have enabled hello feature.</span></span> <span data-ttu-id="888b6-196">30 일 마다 적어도 hello Kerberos 암호 해독 키 롤오버 됩니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-196">Roll over hello Kerberos decryption keys at least every 30 days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="888b6-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="888b6-197">Next steps</span></span>

- <span data-ttu-id="888b6-198">[**기술 심층 분석**](active-directory-aadconnect-sso-how-it-works.md) - 이 기능의 작동 방식을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-198">[**Technical Deep Dive**](active-directory-aadconnect-sso-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="888b6-199">[**질문과 대답** ](active-directory-aadconnect-sso-faq.md) -toofrequently 질문과 대답을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-199">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="888b6-200">[**문제를 해결** ](active-directory-aadconnect-troubleshoot-sso.md) -tooresolve 공통 hello 기능으로 발급 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-200">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="888b6-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 새로운 기능 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="888b6-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
