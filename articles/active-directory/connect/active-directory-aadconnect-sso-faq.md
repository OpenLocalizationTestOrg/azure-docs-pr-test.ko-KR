---
title: "Azure AD Connect: Seamless Single Sign-On Single Sign-On - FAQ(질문과 대답) | Microsoft Docs"
description: "Azure Active Directory Seamless Single Sign-On에 대한 질문과 대답입니다."
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
ms.openlocfilehash: 518b2719f24be96dffba3458f6c15e65f16b7e0d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-frequently-asked-questions"></a><span data-ttu-id="6825c-104">Azure Active Directory Seamless Single Sign-On: FAQ(질문과 대답)</span><span class="sxs-lookup"><span data-stu-id="6825c-104">Azure Active Directory Seamless Single Sign-On: Frequently asked questions</span></span>

<span data-ttu-id="6825c-105">이 문서에서는 Azure Active Directory Seamless SSO(Seamless Single Sign-On)에 대한 질문과 대답을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-105">In this article, we address frequently asked questions about Azure Active Directory Seamless Single Sign-On (Seamless SSO).</span></span> <span data-ttu-id="6825c-106">새로운 내용을 계속 확인해 주세요.</span><span class="sxs-lookup"><span data-stu-id="6825c-106">Keep checking back for new content.</span></span>

>[!IMPORTANT]
><span data-ttu-id="6825c-107">Seamless SSO 기능은 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-107">The Seamless SSO feature is currently in preview.</span></span>

## <a name="what-sign-in-methods-do-seamless-sso-work-with"></a><span data-ttu-id="6825c-108">Seamless SSO에서 사용되는 로그인 방법은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="6825c-108">What sign-in methods do Seamless SSO work with?</span></span>

<span data-ttu-id="6825c-109">Seamless SSO는 [암호 해시 동기화](active-directory-aadconnectsync-implement-password-synchronization.md) 또는 [통과 인증](active-directory-aadconnect-pass-through-authentication.md) 로그인 방법과 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-109">Seamless SSO can be combined with either the [Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) or [Pass-through Authentication](active-directory-aadconnect-pass-through-authentication.md) sign-in methods.</span></span> <span data-ttu-id="6825c-110">그러나 AD FS(Active Directory Federation Services)에는 이 기능을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-110">However this feature cannot be used with Active Directory Federation Services (ADFS).</span></span>

## <a name="is-seamless-sso-a-free-feature"></a><span data-ttu-id="6825c-111">Seamless SSO는 평가판 체험 기능인가요?</span><span class="sxs-lookup"><span data-stu-id="6825c-111">Is Seamless SSO a free feature?</span></span>

<span data-ttu-id="6825c-112">평가판 체험 기능이며, Azure AD 유료 버전으로 이 기능을 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-112">Seamless SSO is a free feature and you don't need any paid editions of Azure AD to use it.</span></span> <span data-ttu-id="6825c-113">이 기능은 일반 공급될 때도 추가 비용 없이 제공될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-113">It remains free when the feature reaches general availability.</span></span>

## <a name="what-applications-take-advantage-of-domainhint-or-loginhint-parameter-capability-of-seamless-sso"></a><span data-ttu-id="6825c-114">Seamless SSO의 `domain_hint` 또는 `login_hint` 매개 변수 기능을 활용하는 응용 프로그램은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="6825c-114">What applications take advantage of `domain_hint` or `login_hint` parameter capability of Seamless SSO?</span></span>

<span data-ttu-id="6825c-115">이러한 매개 변수를 보내는 응용 프로그램 목록과 그렇지 않은 응용 프로그램 목록을 작성하는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-115">We are in the process of compiling the list of applications that send these parameters and the ones that don't.</span></span> <span data-ttu-id="6825c-116">관심 있는 응용 프로그램이 있으시면 의견 섹션에 알려주세요.</span><span class="sxs-lookup"><span data-stu-id="6825c-116">If you have applications that are interested in, let us know in the comments section.</span></span>

## <a name="does-seamless-sso-support-alternate-id-as-the-username-instead-of-userprincipalname"></a><span data-ttu-id="6825c-117">Seamless SSO에서는 사용자 이름으로 `userPrincipalName` 대신 `Alternate ID`를 지원하는가요?</span><span class="sxs-lookup"><span data-stu-id="6825c-117">Does Seamless SSO support `Alternate ID` as the username, instead of `userPrincipalName`?</span></span>

<span data-ttu-id="6825c-118">예.</span><span class="sxs-lookup"><span data-stu-id="6825c-118">Yes.</span></span> <span data-ttu-id="6825c-119">Seamless SSO는 [여기서](active-directory-aadconnect-get-started-custom.md) 보여주듯이 Azure AD Connect에서 구성할 때 `Alternate ID`를 사용자 이름으로 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-119">Seamless SSO supports `Alternate ID` as the username when configured in Azure AD Connect as shown [here](active-directory-aadconnect-get-started-custom.md).</span></span> <span data-ttu-id="6825c-120">모든 Office 365 응용 프로그램에서 `Alternate ID`를 지원하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-120">Not all Office 365 applications support `Alternate ID`.</span></span> <span data-ttu-id="6825c-121">지원 내용은 특정 응용 프로그램의 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6825c-121">Refer to the specific application's documentation for the support statement.</span></span>

## <a name="i-want-to-register-non-windows-10-devices-with-azure-ad-without-using-ad-fs-can-i-use-seamless-sso-instead"></a><span data-ttu-id="6825c-122">AD FS를 사용하지 않고 비Windows 10 장치를 Azure AD에 등록하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-122">I want to register non-Windows 10 devices with Azure AD, without using AD FS.</span></span> <span data-ttu-id="6825c-123">Seamless SSO를 대신 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="6825c-123">Can I use Seamless SSO instead?</span></span>

<span data-ttu-id="6825c-124">예, 이 시나리오에는 [작업 공간 연결 클라이언트](https://www.microsoft.com/download/details.aspx?id=53554) 버전 2.1 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-124">Yes, this scenario needs version 2.1 or later of the [workplace-join client](https://www.microsoft.com/download/details.aspx?id=53554).</span></span>

## <a name="how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account"></a><span data-ttu-id="6825c-125">`AZUREADSSOACCT` 컴퓨터 계정의 Kerberos 암호 해독 키를 롤오버하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="6825c-125">How can I roll over the Kerberos decryption key of the `AZUREADSSOACCT` computer account?</span></span>

<span data-ttu-id="6825c-126">온-프레미스 AD 포리스트에 만든 `AZUREADSSOACCT` 컴퓨터 계정(Azure AD를 나타냄)의 Kerberos 암호 해독 키를 자주 롤오버하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-126">It is important to frequently roll over the Kerberos decryption key of the `AZUREADSSOACCT` computer account (which represents Azure AD) created in your on-premises AD forest.</span></span>

>[!IMPORTANT]
><span data-ttu-id="6825c-127">적어도 30일마다 Kerberos 암호 해독 키를 롤오버하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-127">We highly recommend that you roll over the Kerberos decryption key at least every 30 days.</span></span>

<span data-ttu-id="6825c-128">Azure AD Connect를 실행 중인 온-프레미스 서버에서 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-128">Follow these steps on the on-premises server where you are running Azure AD Connect:</span></span>

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a><span data-ttu-id="6825c-129">1단계.</span><span class="sxs-lookup"><span data-stu-id="6825c-129">Step 1.</span></span> <span data-ttu-id="6825c-130">Seamless SSO가 사용하도록 설정된 AD 포리스트 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-130">Get list of AD forests where Seamless SSO has been enabled</span></span>

1. <span data-ttu-id="6825c-131">먼저 [Microsoft Online Services 로그인 도우미](http://go.microsoft.com/fwlink/?LinkID=286152)를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-131">First, download, and install the [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span>
2. <span data-ttu-id="6825c-132">그런 다음 [Windows PowerShell 용 64비트 Azure Active Directory 모듈](http://go.microsoft.com/fwlink/p/?linkid=236297)을 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-132">Then download and install the [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>
3. <span data-ttu-id="6825c-133">`%programfiles%\Microsoft Azure Active Directory Connect` 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-133">Navigate to the `%programfiles%\Microsoft Azure Active Directory Connect` folder.</span></span>
4. <span data-ttu-id="6825c-134">다음 명령을 사용하여 Seamless SSO PowerShell 모듈을 가져옵니다. `Import-Module .\AzureADSSO.psd1`</span><span class="sxs-lookup"><span data-stu-id="6825c-134">Import the Seamless SSO PowerShell module using this command: `Import-Module .\AzureADSSO.psd1`.</span></span>
5. <span data-ttu-id="6825c-135">관리자 권한으로 PowerShell을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-135">Run PowerShell as an Administrator.</span></span> <span data-ttu-id="6825c-136">PowerShell에서 `New-AzureADSSOAuthenticationContext`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-136">In PowerShell, call `New-AzureADSSOAuthenticationContext`.</span></span> <span data-ttu-id="6825c-137">이 명령으로 테넌트의 전역 관리자 자격 증명을 입력하라는 팝업 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-137">This command should give you a popup to enter your tenant's Global Administrator credentials.</span></span>
6. <span data-ttu-id="6825c-138">`Get-AzureADSSOStatus`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-138">Call `Get-AzureADSSOStatus`.</span></span> <span data-ttu-id="6825c-139">사용하도록 설정된 AD 포리스트 목록("도메인" 목록에 있음)이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-139">This command provides you the list of AD forests (look at the "Domains" list) on which this feature has been enabled.</span></span>

### <a name="step-2-update-the-kerberos-decryption-key-on-each-ad-forest-that-it-was-set-it-up-on"></a><span data-ttu-id="6825c-140">2단계.</span><span class="sxs-lookup"><span data-stu-id="6825c-140">Step 2.</span></span> <span data-ttu-id="6825c-141">설정된 각 AD 포리스트에서 Kerberos 암호 해독 키를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-141">Update the Kerberos decryption key on each AD forest that it was set it up on</span></span>

1. <span data-ttu-id="6825c-142">`$creds = Get-Credential`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-142">Call `$creds = Get-Credential`.</span></span> <span data-ttu-id="6825c-143">메시지가 표시되면 의도한 AD 포리스트에 대한 도메인 관리자 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-143">When prompted, enter the Domain Administrator credentials for the intended AD forest.</span></span>
2. <span data-ttu-id="6825c-144">`Update-AzureADSSOForest -OnPremCredentials $creds`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-144">Call `Update-AzureADSSOForest -OnPremCredentials $creds`.</span></span> <span data-ttu-id="6825c-145">이 명령은 이 특정 AD 포리스트에서 `AZUREADSSOACCT` 컴퓨터 계정에 대한 Kerberos 암호 해독 키를 업데이트하고 Azure AD에서 키를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-145">This command updates the Kerberos decryption key for the `AZUREADSSOACCT` computer account in this specific AD forest and updates it in Azure AD.</span></span>
3. <span data-ttu-id="6825c-146">기능을 설정한 각 AD 포리스트에 대해 위의 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-146">Repeat the preceding steps for each AD forest that you’ve set up the feature on.</span></span>

>[!IMPORTANT]
><span data-ttu-id="6825c-147">`Update-AzureADSSOForest` 명령을 두 번 이상 실행하지 _않아야 합니다_.</span><span class="sxs-lookup"><span data-stu-id="6825c-147">Ensure that you _don't_ run the `Update-AzureADSSOForest` command more than once.</span></span> <span data-ttu-id="6825c-148">그렇지 않으면 해당 기능은 사용자의 Kerberos 티켓이 만료되고 온-프레미스 Active Directory에 의해 재발급될 때까지 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-148">Otherwise, the feature stops working until the time your users' Kerberos tickets expire and are reissued by your on-premises Active Directory.</span></span>

## <a name="how-can-i-disable-seamless-sso"></a><span data-ttu-id="6825c-149">Seamless SSO를 사용하지 않으려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="6825c-149">How can I disable Seamless SSO?</span></span>

<span data-ttu-id="6825c-150">Seamless SSO는 Azure AD Connect를 통해 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-150">Seamless SSO can be disabled using Azure AD Connect.</span></span>

<span data-ttu-id="6825c-151">Azure AD Connect를 실행하고 “사용자 로그인 페이지 변경”(Change user sign-in page)을 선택하고 “다음”을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-151">Run Azure AD Connect, choose "Change user sign-in page" and click "Next".</span></span> <span data-ttu-id="6825c-152">그런 다음 “Single Sign-On 사용” 옵션의 선택을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-152">Then uncheck the "Enable single sign on" option.</span></span> <span data-ttu-id="6825c-153">마법사를 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-153">Continue through the wizard.</span></span> <span data-ttu-id="6825c-154">마법사를 완료하면 테넌트에서 SSO Seamless를 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-154">After completion of the wizard, Seamless SSO is disabled on your tenant.</span></span>

<span data-ttu-id="6825c-155">그러나 화면에 다음과 같은 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-155">However, you see a message on screen that reads as follows:</span></span>

<span data-ttu-id="6825c-156">“Single Sign-On을 이제 사용하지 않도록 설정했습니다. 하지만 정리를 완료하기 위해 수행할 추가 수동 단계가 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-156">"Single sign-on is now disabled, but there are additional manual steps to perform in order to complete clean-up.</span></span> <span data-ttu-id="6825c-157">자세한 정보”</span><span class="sxs-lookup"><span data-stu-id="6825c-157">Learn more"</span></span>

<span data-ttu-id="6825c-158">이 과정을 완료하려면 Azure AD Connect를 실행 중인 온-프레미스 서버에서 다음 수동 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-158">To complete the process, follow these manual steps on the on-premises server where you are running Azure AD Connect:</span></span>

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a><span data-ttu-id="6825c-159">1단계.</span><span class="sxs-lookup"><span data-stu-id="6825c-159">Step 1.</span></span> <span data-ttu-id="6825c-160">Seamless SSO가 사용하도록 설정된 AD 포리스트 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-160">Get list of AD forests where Seamless SSO has been enabled</span></span>

1. <span data-ttu-id="6825c-161">먼저 [Microsoft Online Services 로그인 도우미](http://go.microsoft.com/fwlink/?LinkID=286152)를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-161">First, download, and install the [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span>
2. <span data-ttu-id="6825c-162">그런 다음 [Windows PowerShell 용 64비트 Azure Active Directory 모듈](http://go.microsoft.com/fwlink/p/?linkid=236297)을 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-162">Then download and install the [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>
3. <span data-ttu-id="6825c-163">`%programfiles%\Microsoft Azure Active Directory Connect` 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-163">Navigate to the `%programfiles%\Microsoft Azure Active Directory Connect` folder.</span></span>
4. <span data-ttu-id="6825c-164">다음 명령을 사용하여 Seamless SSO PowerShell 모듈을 가져옵니다. `Import-Module .\AzureADSSO.psd1`</span><span class="sxs-lookup"><span data-stu-id="6825c-164">Import the Seamless SSO PowerShell module using this command: `Import-Module .\AzureADSSO.psd1`.</span></span>
5. <span data-ttu-id="6825c-165">관리자 권한으로 PowerShell을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-165">Run PowerShell as an Administrator.</span></span> <span data-ttu-id="6825c-166">PowerShell에서 `New-AzureADSSOAuthenticationContext`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-166">In PowerShell, call `New-AzureADSSOAuthenticationContext`.</span></span> <span data-ttu-id="6825c-167">이 명령으로 테넌트의 전역 관리자 자격 증명을 입력하라는 팝업 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-167">This command should give you a popup to enter your tenant's Global Administrator credentials.</span></span>
6. <span data-ttu-id="6825c-168">`Get-AzureADSSOStatus`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-168">Call `Get-AzureADSSOStatus`.</span></span> <span data-ttu-id="6825c-169">사용하도록 설정된 AD 포리스트 목록("도메인" 목록에 있음)이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-169">This command provides you the list of AD forests (look at the "Domains" list) on which this feature has been enabled.</span></span>

### <a name="step-2-manually-delete-the-azureadssoacct-computer-account-from-each-ad-forest-that-you-see-listed"></a><span data-ttu-id="6825c-170">2단계.</span><span class="sxs-lookup"><span data-stu-id="6825c-170">Step 2.</span></span> <span data-ttu-id="6825c-171">나열된 각 AD 포리스트에서 `AZUREADSSOACCT` 컴퓨터 계정을 수동으로 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-171">Manually delete the `AZUREADSSOACCT` computer account from each AD forest that you see listed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6825c-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6825c-172">Next steps</span></span>

- <span data-ttu-id="6825c-173">[**빠른 시작**](active-directory-aadconnect-sso-quick-start.md) - Azure AD Seamless SSO를 준비하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-173">[**Quick Start**](active-directory-aadconnect-sso-quick-start.md) - Get up and running Azure AD Seamless SSO.</span></span>
- <span data-ttu-id="6825c-174">[**기술 심층 분석**](active-directory-aadconnect-sso-how-it-works.md) - 이 기능의 작동 방식을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-174">[**Technical Deep Dive**](active-directory-aadconnect-sso-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="6825c-175">[**문제 해결**](active-directory-aadconnect-troubleshoot-sso.md) - 기능과 관련된 일반적인 문제를 해결하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-175">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="6825c-176">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 새로운 기능 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="6825c-176">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
