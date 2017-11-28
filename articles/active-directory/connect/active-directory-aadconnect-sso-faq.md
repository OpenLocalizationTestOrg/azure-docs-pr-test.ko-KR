---
title: "Azure AD Connect: Seamless Single Sign-On Single Sign-On - FAQ(질문과 대답) | Microsoft Docs"
description: "대답 toofrequently 묻는 질문에 대 한 Azure Active Directory 원활한 Single Sign-on입니다."
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
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: e91e7950670633c08c180ece873f7451fa19eef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-frequently-asked-questions"></a><span data-ttu-id="620e3-104">Azure Active Directory Seamless Single Sign-On: FAQ(질문과 대답)</span><span class="sxs-lookup"><span data-stu-id="620e3-104">Azure Active Directory Seamless Single Sign-On: Frequently asked questions</span></span>

<span data-ttu-id="620e3-105">이 문서에서는 Azure Active Directory Seamless SSO(Seamless Single Sign-On)에 대한 질문과 대답을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-105">In this article, we address frequently asked questions about Azure Active Directory Seamless Single Sign-On (Seamless SSO).</span></span> <span data-ttu-id="620e3-106">새로운 내용을 계속 확인해 주세요.</span><span class="sxs-lookup"><span data-stu-id="620e3-106">Keep checking back for new content.</span></span>

>[!IMPORTANT]
><span data-ttu-id="620e3-107">hello 원활한 SSO 기능은 현재 미리 보기 중입니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-107">hello Seamless SSO feature is currently in preview.</span></span>

## <a name="what-sign-in-methods-do-seamless-sso-work-with"></a><span data-ttu-id="620e3-108">Seamless SSO에서 사용되는 로그인 방법은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="620e3-108">What sign-in methods do Seamless SSO work with?</span></span>

<span data-ttu-id="620e3-109">원활한 SSO 어느 hello 함께 사용할 [암호 해시 동기화](active-directory-aadconnectsync-implement-password-synchronization.md) 또는 [통과 인증](active-directory-aadconnect-pass-through-authentication.md) 로그인 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-109">Seamless SSO can be combined with either hello [Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) or [Pass-through Authentication](active-directory-aadconnect-pass-through-authentication.md) sign-in methods.</span></span> <span data-ttu-id="620e3-110">그러나 AD FS(Active Directory Federation Services)에는 이 기능을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-110">However this feature cannot be used with Active Directory Federation Services (ADFS).</span></span>

## <a name="is-seamless-sso-a-free-feature"></a><span data-ttu-id="620e3-111">Seamless SSO는 평가판 체험 기능인가요?</span><span class="sxs-lookup"><span data-stu-id="620e3-111">Is Seamless SSO a free feature?</span></span>

<span data-ttu-id="620e3-112">원활한 SSO 무료 기능이 며 toouse Azure AD의 유료 버전 필요가 없는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-112">Seamless SSO is a free feature and you don't need any paid editions of Azure AD toouse it.</span></span> <span data-ttu-id="620e3-113">Hello 기능이 일반 공급 하는 경우 무료에 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-113">It remains free when hello feature reaches general availability.</span></span>

## <a name="what-applications-take-advantage-of-domainhint-or-loginhint-parameter-capability-of-seamless-sso"></a><span data-ttu-id="620e3-114">Seamless SSO의 `domain_hint` 또는 `login_hint` 매개 변수 기능을 활용하는 응용 프로그램은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="620e3-114">What applications take advantage of `domain_hint` or `login_hint` parameter capability of Seamless SSO?</span></span>

<span data-ttu-id="620e3-115">Hello 목록은 이러한 매개 변수 및 hello 하지는 보내는 응용 프로그램을 컴파일 hello 과정에는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-115">We are in hello process of compiling hello list of applications that send these parameters and hello ones that don't.</span></span> <span data-ttu-id="620e3-116">에 관심이 있는 응용 프로그램의 경우에 hello 설명 섹션에 알려 주십시오.</span><span class="sxs-lookup"><span data-stu-id="620e3-116">If you have applications that are interested in, let us know in hello comments section.</span></span>

## <a name="does-seamless-sso-support-alternate-id-as-hello-username-instead-of-userprincipalname"></a><span data-ttu-id="620e3-117">원활한 SSO ¿ø `Alternate ID` 사용자 이름 대신 hello 대로 `userPrincipalName`?</span><span class="sxs-lookup"><span data-stu-id="620e3-117">Does Seamless SSO support `Alternate ID` as hello username, instead of `userPrincipalName`?</span></span>

<span data-ttu-id="620e3-118">예.</span><span class="sxs-lookup"><span data-stu-id="620e3-118">Yes.</span></span> <span data-ttu-id="620e3-119">원활한 SSO 지원 `Alternate ID` hello와 같이 Azure AD Connect에서 구성 된 경우 사용자 이름으로 [여기](active-directory-aadconnect-get-started-custom.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-119">Seamless SSO supports `Alternate ID` as hello username when configured in Azure AD Connect as shown [here](active-directory-aadconnect-get-started-custom.md).</span></span> <span data-ttu-id="620e3-120">모든 Office 365 응용 프로그램에서 `Alternate ID`를 지원하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-120">Not all Office 365 applications support `Alternate ID`.</span></span> <span data-ttu-id="620e3-121">Hello 지원 정책 toohello 특정 한 응용 프로그램의 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="620e3-121">Refer toohello specific application's documentation for hello support statement.</span></span>

## <a name="i-want-tooregister-non-windows-10-devices-with-azure-ad-without-using-ad-fs-can-i-use-seamless-sso-instead"></a><span data-ttu-id="620e3-122">AD FS를 사용 하지 않고 Azure AD 사용 하 여 비-Windows 10 장치 tooregister 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-122">I want tooregister non-Windows 10 devices with Azure AD, without using AD FS.</span></span> <span data-ttu-id="620e3-123">Seamless SSO를 대신 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="620e3-123">Can I use Seamless SSO instead?</span></span>

<span data-ttu-id="620e3-124">2.1 이상 hello 버전 필요한이 시나리오는 예, [작업 공간 연결 클라이언트](https://www.microsoft.com/download/details.aspx?id=53554)합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-124">Yes, this scenario needs version 2.1 or later of hello [workplace-join client](https://www.microsoft.com/download/details.aspx?id=53554).</span></span>

## <a name="how-can-i-roll-over-hello-kerberos-decryption-key-of-hello-azureadssoacct-computer-account"></a><span data-ttu-id="620e3-125">Hello의 hello Kerberos 암호 해독 키를 통해 롤백될 수는 어떻게 `AZUREADSSOACCT` 컴퓨터 계정을?</span><span class="sxs-lookup"><span data-stu-id="620e3-125">How can I roll over hello Kerberos decryption key of hello `AZUREADSSOACCT` computer account?</span></span>

<span data-ttu-id="620e3-126">Toofrequently hello의 hello Kerberos 암호 해독 키를 롤오버할 반드시 `AZUREADSSOACCT` 컴퓨터 계정 (Azure AD를 나타냄) 온-프레미스에서 만든 AD 포리스트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-126">It is important toofrequently roll over hello Kerberos decryption key of hello `AZUREADSSOACCT` computer account (which represents Azure AD) created in your on-premises AD forest.</span></span>

>[!IMPORTANT]
><span data-ttu-id="620e3-127">배포 하기 hello Kerberos 암호 해독 키를 통해 30 일 마다 적어도 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-127">We highly recommend that you roll over hello Kerberos decryption key at least every 30 days.</span></span>

<span data-ttu-id="620e3-128">Azure AD Connect를 실행 중인 hello 온-프레미스 서버에서 다음이 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-128">Follow these steps on hello on-premises server where you are running Azure AD Connect:</span></span>

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a><span data-ttu-id="620e3-129">1단계.</span><span class="sxs-lookup"><span data-stu-id="620e3-129">Step 1.</span></span> <span data-ttu-id="620e3-130">Seamless SSO가 사용하도록 설정된 AD 포리스트 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-130">Get list of AD forests where Seamless SSO has been enabled</span></span>

1. <span data-ttu-id="620e3-131">첫째, 다운로드 및 설치 hello [Microsoft Online Services 로그인 도우미](http://go.microsoft.com/fwlink/?LinkID=286152)합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-131">First, download, and install hello [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span>
2. <span data-ttu-id="620e3-132">다운로드 하 고 hello 설치 [Windows PowerShell 용 Azure Active Directory 모듈을 64 비트](http://go.microsoft.com/fwlink/p/?linkid=236297)합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-132">Then download and install hello [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>
3. <span data-ttu-id="620e3-133">Toohello 이동 `%programfiles%\Microsoft Azure Active Directory Connect` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-133">Navigate toohello `%programfiles%\Microsoft Azure Active Directory Connect` folder.</span></span>
4. <span data-ttu-id="620e3-134">이 명령을 사용 하 여 hello 원활한 SSO PowerShell 모듈 가져오기: `Import-Module .\AzureADSSO.psd1`합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-134">Import hello Seamless SSO PowerShell module using this command: `Import-Module .\AzureADSSO.psd1`.</span></span>
5. <span data-ttu-id="620e3-135">관리자 권한으로 PowerShell을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-135">Run PowerShell as an Administrator.</span></span> <span data-ttu-id="620e3-136">PowerShell에서 `New-AzureADSSOAuthenticationContext`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-136">In PowerShell, call `New-AzureADSSOAuthenticationContext`.</span></span> <span data-ttu-id="620e3-137">이 명령은 팝업 tooenter를 제공 해야 테 넌 트의 전역 관리자 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-137">This command should give you a popup tooenter your tenant's Global Administrator credentials.</span></span>
6. <span data-ttu-id="620e3-138">`Get-AzureADSSOStatus`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-138">Call `Get-AzureADSSOStatus`.</span></span> <span data-ttu-id="620e3-139">이 명령에이 기능이 설정 되는 AD 포리스트 ("hello"도메인 목록 보고) 목록 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-139">This command provides you hello list of AD forests (look at hello "Domains" list) on which this feature has been enabled.</span></span>

### <a name="step-2-update-hello-kerberos-decryption-key-on-each-ad-forest-that-it-was-set-it-up-on"></a><span data-ttu-id="620e3-140">2단계.</span><span class="sxs-lookup"><span data-stu-id="620e3-140">Step 2.</span></span> <span data-ttu-id="620e3-141">설정 된 것 각 AD 포리스트에서 hello Kerberos 암호 해독 키를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-141">Update hello Kerberos decryption key on each AD forest that it was set it up on</span></span>

1. <span data-ttu-id="620e3-142">`$creds = Get-Credential`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-142">Call `$creds = Get-Credential`.</span></span> <span data-ttu-id="620e3-143">메시지가 표시 되 면 hello AD 포리스트 의도 대 한 hello 도메인 관리자 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-143">When prompted, enter hello Domain Administrator credentials for hello intended AD forest.</span></span>
2. <span data-ttu-id="620e3-144">`Update-AzureADSSOForest -OnPremCredentials $creds`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-144">Call `Update-AzureADSSOForest -OnPremCredentials $creds`.</span></span> <span data-ttu-id="620e3-145">이 명령은 업데이트 hello hello에 대 한 Kerberos 암호 해독 키 `AZUREADSSOACCT` 이 특정 AD 포리스트의 컴퓨터 계정 및 Azure AD에서 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-145">This command updates hello Kerberos decryption key for hello `AZUREADSSOACCT` computer account in this specific AD forest and updates it in Azure AD.</span></span>
3. <span data-ttu-id="620e3-146">이전 단계에서 hello 기능을 설정 하는 각 AD 포리스트에 대 한 hello를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-146">Repeat hello preceding steps for each AD forest that you’ve set up hello feature on.</span></span>

>[!IMPORTANT]
><span data-ttu-id="620e3-147">확인을 _하지_ hello 실행 `Update-AzureADSSOForest` 명령을 한 번 이상.</span><span class="sxs-lookup"><span data-stu-id="620e3-147">Ensure that you _don't_ run hello `Update-AzureADSSOForest` command more than once.</span></span> <span data-ttu-id="620e3-148">그렇지 않으면 hello 기능 hello 시간 사용자의 Kerberos 티켓 만료 되 고 온-프레미스 Active Directory에서 발급 될 때까지 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-148">Otherwise, hello feature stops working until hello time your users' Kerberos tickets expire and are reissued by your on-premises Active Directory.</span></span>

## <a name="how-can-i-disable-seamless-sso"></a><span data-ttu-id="620e3-149">Seamless SSO를 사용하지 않으려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="620e3-149">How can I disable Seamless SSO?</span></span>

<span data-ttu-id="620e3-150">Seamless SSO는 Azure AD Connect를 통해 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-150">Seamless SSO can be disabled using Azure AD Connect.</span></span>

<span data-ttu-id="620e3-151">Azure AD Connect를 실행하고 “사용자 로그인 페이지 변경”(Change user sign-in page)을 선택하고 “다음”을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-151">Run Azure AD Connect, choose "Change user sign-in page" and click "Next".</span></span> <span data-ttu-id="620e3-152">그런 다음 hello "Enable single sign on" 옵션의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-152">Then uncheck hello "Enable single sign on" option.</span></span> <span data-ttu-id="620e3-153">Hello 마법사를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-153">Continue through hello wizard.</span></span> <span data-ttu-id="620e3-154">Hello 마법사를 완료 한 후 테 넌 트에 원활한 SSO 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-154">After completion of hello wizard, Seamless SSO is disabled on your tenant.</span></span>

<span data-ttu-id="620e3-155">그러나 화면에 다음과 같은 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-155">However, you see a message on screen that reads as follows:</span></span>

<span data-ttu-id="620e3-156">"Single sign on 이제 사용 하지 않으면 없지만 추가적인 수동 단계 tooperform에 순서 toocomplete 정리 합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-156">"Single sign-on is now disabled, but there are additional manual steps tooperform in order toocomplete clean-up.</span></span> <span data-ttu-id="620e3-157">자세한 정보”</span><span class="sxs-lookup"><span data-stu-id="620e3-157">Learn more"</span></span>

<span data-ttu-id="620e3-158">toocomplete 프로세스 hello Azure AD Connect를 실행 중인 hello 온-프레미스 서버에 수동 단계를 수행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="620e3-158">toocomplete hello process, follow these manual steps on hello on-premises server where you are running Azure AD Connect:</span></span>

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a><span data-ttu-id="620e3-159">1단계.</span><span class="sxs-lookup"><span data-stu-id="620e3-159">Step 1.</span></span> <span data-ttu-id="620e3-160">Seamless SSO가 사용하도록 설정된 AD 포리스트 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-160">Get list of AD forests where Seamless SSO has been enabled</span></span>

1. <span data-ttu-id="620e3-161">첫째, 다운로드 및 설치 hello [Microsoft Online Services 로그인 도우미](http://go.microsoft.com/fwlink/?LinkID=286152)합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-161">First, download, and install hello [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span>
2. <span data-ttu-id="620e3-162">다운로드 하 고 hello 설치 [Windows PowerShell 용 Azure Active Directory 모듈을 64 비트](http://go.microsoft.com/fwlink/p/?linkid=236297)합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-162">Then download and install hello [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>
3. <span data-ttu-id="620e3-163">Toohello 이동 `%programfiles%\Microsoft Azure Active Directory Connect` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-163">Navigate toohello `%programfiles%\Microsoft Azure Active Directory Connect` folder.</span></span>
4. <span data-ttu-id="620e3-164">이 명령을 사용 하 여 hello 원활한 SSO PowerShell 모듈 가져오기: `Import-Module .\AzureADSSO.psd1`합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-164">Import hello Seamless SSO PowerShell module using this command: `Import-Module .\AzureADSSO.psd1`.</span></span>
5. <span data-ttu-id="620e3-165">관리자 권한으로 PowerShell을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-165">Run PowerShell as an Administrator.</span></span> <span data-ttu-id="620e3-166">PowerShell에서 `New-AzureADSSOAuthenticationContext`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-166">In PowerShell, call `New-AzureADSSOAuthenticationContext`.</span></span> <span data-ttu-id="620e3-167">이 명령은 팝업 tooenter를 제공 해야 테 넌 트의 전역 관리자 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-167">This command should give you a popup tooenter your tenant's Global Administrator credentials.</span></span>
6. <span data-ttu-id="620e3-168">`Get-AzureADSSOStatus`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-168">Call `Get-AzureADSSOStatus`.</span></span> <span data-ttu-id="620e3-169">이 명령에이 기능이 설정 되는 AD 포리스트 ("hello"도메인 목록 보고) 목록 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-169">This command provides you hello list of AD forests (look at hello "Domains" list) on which this feature has been enabled.</span></span>

### <a name="step-2-manually-delete-hello-azureadssoacct-computer-account-from-each-ad-forest-that-you-see-listed"></a><span data-ttu-id="620e3-170">2단계.</span><span class="sxs-lookup"><span data-stu-id="620e3-170">Step 2.</span></span> <span data-ttu-id="620e3-171">Hello를 수동으로 삭제 `AZUREADSSOACCT` 나열 하는 각 AD 포리스트에서에서 컴퓨터 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-171">Manually delete hello `AZUREADSSOACCT` computer account from each AD forest that you see listed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="620e3-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="620e3-172">Next steps</span></span>

- <span data-ttu-id="620e3-173">[**빠른 시작**](active-directory-aadconnect-sso-quick-start.md) - Azure AD Seamless SSO를 준비하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-173">[**Quick Start**](active-directory-aadconnect-sso-quick-start.md) - Get up and running Azure AD Seamless SSO.</span></span>
- <span data-ttu-id="620e3-174">[**기술 심층 분석**](active-directory-aadconnect-sso-how-it-works.md) - 이 기능의 작동 방식을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-174">[**Technical Deep Dive**](active-directory-aadconnect-sso-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="620e3-175">[**문제를 해결** ](active-directory-aadconnect-troubleshoot-sso.md) -tooresolve 공통 hello 기능으로 발급 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-175">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="620e3-176">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 새로운 기능 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="620e3-176">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
