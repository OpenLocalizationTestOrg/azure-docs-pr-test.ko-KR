---
title: "Azure AD Connect: Seamless Single Sign-On 문제 해결 | Microsoft Docs"
description: "이 항목에서는 Azure AD Seamless SSO(Azure Active Directory Seamless Single Sign-On) 문제를 해결하는 방법을 설명합니다."
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
ms.openlocfilehash: bc4ff9125553c8918df3a1f84041560a5b7d4cd8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-azure-active-directory-seamless-single-sign-on"></a><span data-ttu-id="92124-104">Azure Active Directory Seamless Single Sign-On 문제 해결</span><span class="sxs-lookup"><span data-stu-id="92124-104">Troubleshoot Azure Active Directory Seamless Single Sign-On</span></span>

<span data-ttu-id="92124-105">이 문서에서는 Azure AD Seamless Single Sign-On과 관련된 일반적인 문제에 대한 문제 해결 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92124-105">This article helps you find troubleshooting information about common issues regarding Azure AD Seamless Single Sign-On.</span></span>

## <a name="known-issues"></a><span data-ttu-id="92124-106">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="92124-106">Known issues</span></span>

- <span data-ttu-id="92124-107">30개 이상의 AD 포리스트를 동기화하면 Azure AD Connect를 통해 Seamless SSO를 활성화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="92124-107">If you are synchronizing 30 or more AD forests, you can't enable Seamless SSO using Azure AD Connect.</span></span> <span data-ttu-id="92124-108">이 경우 테넌트에서 이 기능을 [수동으로 활성화](#manual-reset-of-azure-ad-seamless-sso)하여 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92124-108">As a workaround, you can [manually enable](#manual-reset-of-azure-ad-seamless-sso) the feature on your tenant.</span></span>
- <span data-ttu-id="92124-109">"로컬 인트라넷" 영역 대신 "신뢰할 수 있는 사이트" 영역에 Azure AD 서비스 URL(https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net)을 추가하면 **사용자가 로그인 할 수 없습니다**.</span><span class="sxs-lookup"><span data-stu-id="92124-109">Adding Azure AD service URLs (https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net) to the "Trusted sites" zone instead of the "Local intranet" zone **blocks users from signing in**.</span></span>
- <span data-ttu-id="92124-110">Firefox 및 Edge의 개인 검색 모드에서는 Seamless SSO가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="92124-110">Seamless SSO doesn't work in private browsing mode on Firefox and Edge.</span></span> <span data-ttu-id="92124-111">또한 Internet Explorer에서 향상된 보호 모드가 켜져 있을 때도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="92124-111">And also on Internet Explorer when Enhanced Protection mode is turned on.</span></span>

>[!IMPORTANT]
><span data-ttu-id="92124-112">최근 고객이 신고한 문제를 조사하기 위해 에지에 대한 지원을 롤백했습니다.</span><span class="sxs-lookup"><span data-stu-id="92124-112">We recently rolled back support for Edge to investigate customer-reported issues.</span></span>

## <a name="check-status-of-the-feature"></a><span data-ttu-id="92124-113">기능의 상태 확인</span><span class="sxs-lookup"><span data-stu-id="92124-113">Check status of the feature</span></span>

<span data-ttu-id="92124-114">테넌트에서 Seamless SSO 기능이 여전히 **활성화**되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-114">Ensure that the Seamless SSO feature is still **Enabled** on your tenant.</span></span> <span data-ttu-id="92124-115">[Azure Active Directory 관리 센터](https://aad.portal.azure.com/)의 **Azure AD Connect** 블레이드로 이동하여 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92124-115">You can check status by going to the **Azure AD Connect** blade on the [Azure Active Directory admin center](https://aad.portal.azure.com/).</span></span>

![Azure Active Directory 관리 센터 - Azure AD Connect 블레이드](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="sign-in-failure-reasons-on-the-azure-active-directory-admin-center"></a><span data-ttu-id="92124-117">Azure Active Directory 관리 센터에서 로그인이 실패한 이유</span><span class="sxs-lookup"><span data-stu-id="92124-117">Sign-in failure reasons on the Azure Active Directory admin center</span></span>

<span data-ttu-id="92124-118">Seamless SSO를 사용하여 사용자 로그인 문제를 해결하려면 [Azure Active Directory 관리 센터](https://aad.portal.azure.com/)에서 [로그인 활동 보고서](../active-directory-reporting-activity-sign-ins.md)를 살펴보는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="92124-118">A good place to start troubleshooting user sign-in issues with Seamless SSO is to look at the [sign-in activity report](../active-directory-reporting-activity-sign-ins.md) on the [Azure Active Directory admin center](https://aad.portal.azure.com/).</span></span>

![Azure Active Directory 관리 센터 - 로그인 보고서](./media/active-directory-aadconnect-sso/sso9.png)

<span data-ttu-id="92124-120">[Azure Active Directory 관리 센터](https://aad.portal.azure.com/)에서 **Azure Active Directory** -> **로그인**으로 차례로 이동하고 특정 사용자의 로그인 활동을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-120">Navigate to **Azure Active Directory** -> **Sign-ins** on the [Azure Active Directory admin center](https://aad.portal.azure.com/) and click a specific user's sign-in activity.</span></span> <span data-ttu-id="92124-121">**로그인 오류 코드** 필드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="92124-121">Look for the **SIGN-IN ERROR CODE** field.</span></span> <span data-ttu-id="92124-122">다음 표를 사용하여 해당 필드의 값을 실패 이유 및 해결에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-122">Map the value of that field to a failure reason and resolution using the following table:</span></span>

|<span data-ttu-id="92124-123">로그인 오류 코드</span><span class="sxs-lookup"><span data-stu-id="92124-123">Sign-in error code</span></span>|<span data-ttu-id="92124-124">로그인 실패 이유</span><span class="sxs-lookup"><span data-stu-id="92124-124">Sign-in failure reason</span></span>|<span data-ttu-id="92124-125">해결 방법</span><span class="sxs-lookup"><span data-stu-id="92124-125">Resolution</span></span>
| --- | --- | ---
| <span data-ttu-id="92124-126">81001</span><span class="sxs-lookup"><span data-stu-id="92124-126">81001</span></span> | <span data-ttu-id="92124-127">사용자의 Kerberos 티켓이 너무 큽니다.</span><span class="sxs-lookup"><span data-stu-id="92124-127">User's Kerberos ticket is too large.</span></span> | <span data-ttu-id="92124-128">사용자의 그룹 멤버 자격 수를 줄이고 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-128">Reduce user's group memberships and try again.</span></span>
| <span data-ttu-id="92124-129">81002</span><span class="sxs-lookup"><span data-stu-id="92124-129">81002</span></span> | <span data-ttu-id="92124-130">사용자의 Kerberos 티켓에 대한 유효성을 검사할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="92124-130">Unable to validate user's Kerberos ticket.</span></span> | <span data-ttu-id="92124-131">[문제 해결 검사 목록](#troubleshooting-checklist)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="92124-131">See [troubleshooting checklist](#troubleshooting-checklist).</span></span>
| <span data-ttu-id="92124-132">81003</span><span class="sxs-lookup"><span data-stu-id="92124-132">81003</span></span> | <span data-ttu-id="92124-133">사용자의 Kerberos 티켓에 대한 유효성을 검사할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="92124-133">Unable to validate user's Kerberos ticket.</span></span> | <span data-ttu-id="92124-134">[문제 해결 검사 목록](#troubleshooting-checklist)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="92124-134">See [troubleshooting checklist](#troubleshooting-checklist).</span></span>
| <span data-ttu-id="92124-135">81004</span><span class="sxs-lookup"><span data-stu-id="92124-135">81004</span></span> | <span data-ttu-id="92124-136">Kerberos 인증 시도가 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="92124-136">Kerberos authentication attempt failed.</span></span> | <span data-ttu-id="92124-137">[문제 해결 검사 목록](#troubleshooting-checklist)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="92124-137">See [troubleshooting checklist](#troubleshooting-checklist).</span></span>
| <span data-ttu-id="92124-138">81008</span><span class="sxs-lookup"><span data-stu-id="92124-138">81008</span></span> | <span data-ttu-id="92124-139">사용자의 Kerberos 티켓에 대한 유효성을 검사할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="92124-139">Unable to validate user's Kerberos ticket.</span></span> | <span data-ttu-id="92124-140">[문제 해결 검사 목록](#troubleshooting-checklist)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="92124-140">See [troubleshooting checklist](#troubleshooting-checklist).</span></span>
| <span data-ttu-id="92124-141">81009</span><span class="sxs-lookup"><span data-stu-id="92124-141">81009</span></span> | <span data-ttu-id="92124-142">사용자의 Kerberos 티켓에 대한 유효성을 검사할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="92124-142">"Unable to validate user's Kerberos ticket.</span></span> | <span data-ttu-id="92124-143">[문제 해결 검사 목록](#troubleshooting-checklist)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="92124-143">See [troubleshooting checklist](#troubleshooting-checklist).</span></span>
| <span data-ttu-id="92124-144">81010</span><span class="sxs-lookup"><span data-stu-id="92124-144">81010</span></span> | <span data-ttu-id="92124-145">사용자의 Kerberos 티켓이 만료되었거나 잘못되었으므로 Seamless SSO가 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="92124-145">Seamless SSO failed because the user's Kerberos ticket has expired or is invalid.</span></span> | <span data-ttu-id="92124-146">사용자는 회사 네트워크 내부의 도메인 가입 장치에서 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-146">User needs to sign in from a domain-joined device inside your corporate network.</span></span>
| <span data-ttu-id="92124-147">81011</span><span class="sxs-lookup"><span data-stu-id="92124-147">81011</span></span> | <span data-ttu-id="92124-148">사용자의 Kerberos 티켓 정보에 기반하여 사용자 개체를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="92124-148">Unable to find user object based on information in the user's Kerberos ticket.</span></span> | <span data-ttu-id="92124-149">Azure AD Connect를 사용하여 사용자 정보를 Azure AD와 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-149">Use Azure AD Connect to synchronize user information into Azure AD.</span></span>
| <span data-ttu-id="92124-150">81012</span><span class="sxs-lookup"><span data-stu-id="92124-150">81012</span></span> | <span data-ttu-id="92124-151">Azure AD에 로그인하려는 사용자가 장치에 로그인한 사용자와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="92124-151">The user trying to sign in to Azure AD is different from the user signed into the device.</span></span> | <span data-ttu-id="92124-152">다른 장치에서 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-152">Sign in from a different device.</span></span>
| <span data-ttu-id="92124-153">81013</span><span class="sxs-lookup"><span data-stu-id="92124-153">81013</span></span> | <span data-ttu-id="92124-154">사용자의 Kerberos 티켓 정보에 기반하여 사용자 개체를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="92124-154">Unable to find user object based on information in the user's Kerberos ticket.</span></span> |<span data-ttu-id="92124-155">Azure AD Connect를 사용하여 사용자 정보를 Azure AD와 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-155">Use Azure AD Connect to synchronize user information into Azure AD.</span></span> 

## <a name="troubleshooting-checklist"></a><span data-ttu-id="92124-156">문제 해결 검사 목록</span><span class="sxs-lookup"><span data-stu-id="92124-156">Troubleshooting checklist</span></span>

<span data-ttu-id="92124-157">다음 검사 목록을 사용하여 Seamless SSO 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-157">Use the following checklist to troubleshoot Seamless SSO issues:</span></span>

- <span data-ttu-id="92124-158">Azure AD Connect에서 Seamless SSO 기능이 활성화되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-158">Check if the Seamless SSO feature is enabled in Azure AD Connect.</span></span> <span data-ttu-id="92124-159">차단된 포트 등과 같은 이유로 기능을 활성화할 수 없으면 모든 [필수 조건](active-directory-aadconnect-sso-quick-start.md#step-1-check-prerequisites)가 제대로 충족되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-159">If you can't enable the feature (for example, due to a blocked port), ensure that you have all the [pre-requisites](active-directory-aadconnect-sso-quick-start.md#step-1-check-prerequisites) in place.</span></span>
- <span data-ttu-id="92124-160">이러한 Azure AD URL(https://autologon.microsoftazuread-sso.com 및 https://aadg.windows.net.nsatc.net)이 모두 사용자의 인트라넷 영역 설정의 일부인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-160">Check if both these Azure AD URLs (https://autologon.microsoftazuread-sso.com and https://aadg.windows.net.nsatc.net) are part of the user's Intranet zone settings.</span></span>
- <span data-ttu-id="92124-161">회사 장치가 AD 도메인에 가입되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-161">Ensure the corporate device is joined to the AD domain.</span></span>
- <span data-ttu-id="92124-162">사용자가 AD 도메인 계정으로 장치에 로그인했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-162">Ensure the user is logged on to the device using an AD domain account.</span></span>
- <span data-ttu-id="92124-163">사용자의 계정이 Seamless SSO가 설정된 AD 포리스트에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-163">Ensure that the user's account is from an AD forest where Seamless SSO has been set up.</span></span>
- <span data-ttu-id="92124-164">장치가 회사 네트워크에 연결되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-164">Ensure the device is connected on the corporate network.</span></span>
- <span data-ttu-id="92124-165">장치의 시간이 Active Directory 및 도메인 컨트롤러의 시간과 동기화되고 서로 5분 이내에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-165">Ensure that the device's time is synchronized with the Active Directory's and the Domain Controllers' time and is within five minutes of each other.</span></span>
- <span data-ttu-id="92124-166">명령 프롬프트에서 **klist** 명령을 사용하여 장치의 기존 Kerberos 티켓을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-166">List existing Kerberos tickets on the device using the **klist** command from a command prompt.</span></span> <span data-ttu-id="92124-167">`AZUREADSSOACCT` 컴퓨터 계정으로 발급된 티켓이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-167">Check if tickets issued for the `AZUREADSSOACCT` computer account are present.</span></span> <span data-ttu-id="92124-168">사용자의 Kerberos 티켓은 일반적으로 12시간 동안 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-168">Users' Kerberos tickets are typically valid for 12 hours.</span></span> <span data-ttu-id="92124-169">Active Directory에 다른 설정이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92124-169">You may have  different settings in your Active Directory.</span></span>
- <span data-ttu-id="92124-170">**klist purge** 명령을 사용하여 장치에서 기존 Kerberos 티켓을 제거한 다음 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-170">Purge existing Kerberos tickets from the device using the **klist purge** command, and try again.</span></span>
- <span data-ttu-id="92124-171">JavaScript 관련 문제가 있는지 확인하려면 브라우저의 콘솔 로그("개발자 도구" 아래)를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-171">To determine if there are JavaScript-related issues, review the console logs of the browser (under "Developer Tools").</span></span>
- <span data-ttu-id="92124-172">[도메인 컨트롤러 로그](#domain-controller-logs)도 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="92124-172">Review the [Domain Controller logs](#domain-controller-logs) as well.</span></span>

### <a name="domain-controller-logs"></a><span data-ttu-id="92124-173">도메인 컨트롤러 로그</span><span class="sxs-lookup"><span data-stu-id="92124-173">Domain Controller logs</span></span>

<span data-ttu-id="92124-174">도메인 컨트롤러에서 성공 감사가 사용되면 사용자가 Seamless SSO를 사용하여 로그인할 때마다 보안 항목이 이벤트 로그에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="92124-174">If success auditing is enabled on your Domain Controller, then every time a user signs in using Seamless SSO a security entry is recorded in the Event log.</span></span> <span data-ttu-id="92124-175">다음 쿼리를 사용하여 이러한 보안 이벤트를 찾을 수 있습니다(**AzureADSSOAcc$** 컴퓨터 계정과 연결된 **4769** 이벤트 찾기)</span><span class="sxs-lookup"><span data-stu-id="92124-175">You can find these security events using the following query (look for event **4769** associated with the computer account **AzureADSSOAcc$**):</span></span>

```
    <QueryList>
      <Query Id="0" Path="Security">
    <Select Path="Security">*[EventData[Data[@Name='ServiceName'] and (Data='AZUREADSSOACC$')]]</Select>
      </Query>
    </QueryList>
```

## <a name="manual-reset-of-the-feature"></a><span data-ttu-id="92124-176">기능의 수동 다시 설정</span><span class="sxs-lookup"><span data-stu-id="92124-176">Manual reset of the feature</span></span>

<span data-ttu-id="92124-177">문제 해결이 도움이 되지 않으면 테넌트에서 해당 기능을 수동으로 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92124-177">If troubleshooting didn't help, you can manually reset the feature on your tenant.</span></span> <span data-ttu-id="92124-178">Azure AD Connect를 실행 중인 온-프레미스 서버에서 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="92124-178">Follow these steps on the on-premises server where you are running Azure AD Connect:</span></span>

### <a name="step-1-import-the-seamless-sso-powershell-module"></a><span data-ttu-id="92124-179">1단계: Seamless SSO PowerShell 모듈 가져오기</span><span class="sxs-lookup"><span data-stu-id="92124-179">Step 1: Import the Seamless SSO PowerShell module</span></span>

1. <span data-ttu-id="92124-180">먼저 [Microsoft Online Services 로그인 도우미](http://go.microsoft.com/fwlink/?LinkID=286152)를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-180">First, download, and install the [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span>
2. <span data-ttu-id="92124-181">그런 다음 [Windows PowerShell 용 64비트 Azure Active Directory 모듈](http://go.microsoft.com/fwlink/p/?linkid=236297)을 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-181">Then download and install the [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>
3. <span data-ttu-id="92124-182">`%programfiles%\Microsoft Azure Active Directory Connect` 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-182">Navigate to the `%programfiles%\Microsoft Azure Active Directory Connect` folder.</span></span>
4. <span data-ttu-id="92124-183">다음 명령을 사용하여 Seamless SSO PowerShell 모듈을 가져옵니다. `Import-Module .\AzureADSSO.psd1`</span><span class="sxs-lookup"><span data-stu-id="92124-183">Import the Seamless SSO PowerShell module using this command: `Import-Module .\AzureADSSO.psd1`.</span></span>

### <a name="step-2-get-the-list-of-ad-forests-on-which-seamless-sso-has-been-enabled"></a><span data-ttu-id="92124-184">2단계: Seamless SSO가 사용하도록 설정된 AD 포리스트 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="92124-184">Step 2: Get the list of AD forests on which Seamless SSO has been enabled</span></span>

1. <span data-ttu-id="92124-185">관리자 권한으로 PowerShell을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-185">Run PowerShell as Administrator.</span></span> <span data-ttu-id="92124-186">PowerShell에서 `New-AzureADSSOAuthenticationContext`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-186">In PowerShell, call `New-AzureADSSOAuthenticationContext`.</span></span> <span data-ttu-id="92124-187">메시지가 표시되면 테넌트의 전역 관리자 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-187">When prompted, enter your tenant's Global Administrator credentials.</span></span>
2. <span data-ttu-id="92124-188">`Get-AzureADSSOStatus`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-188">Call `Get-AzureADSSOStatus`.</span></span> <span data-ttu-id="92124-189">사용하도록 설정된 AD 포리스트 목록("도메인" 목록에 있음)이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="92124-189">This command provides you the list of AD forests (look at the "Domains" list) on which this feature has been enabled.</span></span>

### <a name="step-3-disable-seamless-sso-for-each-ad-forest-that-it-was-set-it-up-on"></a><span data-ttu-id="92124-190">3단계: 사용하도록 설정된 각 AD 포리스트에 대한 Seamless SSO 비활성화</span><span class="sxs-lookup"><span data-stu-id="92124-190">Step 3: Disable Seamless SSO for each AD forest that it was set it up on</span></span>

1. <span data-ttu-id="92124-191">`$creds = Get-Credential`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-191">Call `$creds = Get-Credential`.</span></span> <span data-ttu-id="92124-192">메시지가 표시되면 의도한 AD 포리스트에 대한 도메인 관리자 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-192">When prompted, enter the Domain Administrator credentials for the intended AD forest.</span></span>
2. <span data-ttu-id="92124-193">`Disable-AzureADSSOForest -OnPremCredentials $creds`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-193">Call `Disable-AzureADSSOForest -OnPremCredentials $creds`.</span></span> <span data-ttu-id="92124-194">이 명령은 이 특정 AD 포리스트에 대한 온-프레미스 도메인 컨트롤러에서 `AZUREADSSOACCT` 컴퓨터 계정을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-194">This command removes the `AZUREADSSOACCT` computer account from the on-premises Domain Controller for this specific AD forest.</span></span>
3. <span data-ttu-id="92124-195">기능을 설정한 각 AD 포리스트에 대해 위의 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-195">Repeat the preceding steps for each AD forest that you’ve set up the feature on.</span></span>

### <a name="step-4-enable-seamless-sso-for-each-ad-forest"></a><span data-ttu-id="92124-196">4단계: 각 AD 포리스트에 대한 Seamless SSO 활성화</span><span class="sxs-lookup"><span data-stu-id="92124-196">Step 4: Enable Seamless SSO for each AD forest</span></span>

1. <span data-ttu-id="92124-197">`Enable-AzureADSSOForest`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-197">Call `Enable-AzureADSSOForest`.</span></span> <span data-ttu-id="92124-198">메시지가 표시되면 의도한 AD 포리스트에 대한 도메인 관리자 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-198">When prompted, enter the Domain Administrator credentials for the intended AD forest.</span></span>
2. <span data-ttu-id="92124-199">기능을 설정하려는 각 AD 포리스트에 대해 위의 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-199">Repeat the preceding steps for each AD forest that you want to set up the feature on.</span></span>

### <a name="step-5-enable-the-feature-on-your-tenant"></a><span data-ttu-id="92124-200">5단계.</span><span class="sxs-lookup"><span data-stu-id="92124-200">Step 5.</span></span> <span data-ttu-id="92124-201">테넌트에서 기능 활성화</span><span class="sxs-lookup"><span data-stu-id="92124-201">Enable the feature on your tenant</span></span>

<span data-ttu-id="92124-202">`Enable-AzureADSSO`를 호출하고 `Enable: ` 프롬프트에서 "true"를 입력하여 테넌트에서 해당 기능을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="92124-202">Call `Enable-AzureADSSO` and type in "true" at the `Enable: ` prompt to turn on the feature in your tenant.</span></span>
