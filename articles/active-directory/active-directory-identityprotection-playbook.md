---
title: "Azure Active Directory ID 보호 플레이 북 | Microsoft Docs"
description: "Azure AD ID 보호를 사용하여 손상된 ID 및 장치를 악용하는 공격자의 능력을 제한하고 이전에 손상이 우려되거나 손상된 ID 또는 장치를 보호할 수 있는 방법을 알아봅니다."
services: active-directory
keywords: "Azure Active Directory ID 보호, 클라우드 앱 검색, 응용 프로그램 관리, 보안, 위험, 위험 수준, 취약점, 보안 정책"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 60836abf-f0e9-459d-b344-8e06b8341d25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 2ecd07faed785fa6aa179ac1cca35a70d965e1dc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-playbook"></a><span data-ttu-id="c7767-104">Azure Active Directory ID 보호 플레이 북</span><span class="sxs-lookup"><span data-stu-id="c7767-104">Azure Active Directory Identity Protection playbook</span></span>
<span data-ttu-id="c7767-105">이 플레이 북은 다음 작업을 수행하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-105">This playbook helps you to:</span></span>

* <span data-ttu-id="c7767-106">위험 이벤트 및 취약성을 시뮬레이트하여 ID 보호 환경에 데이터 채우기</span><span class="sxs-lookup"><span data-stu-id="c7767-106">Populate data in the Identity Protection environment by simulating risk events and vulnerabilities</span></span>
* <span data-ttu-id="c7767-107">위험 기반 조건부 액세스 정책을 설정하고 이러한 정책의 영향 테스트</span><span class="sxs-lookup"><span data-stu-id="c7767-107">Set up risk-based conditional access policies and test the impact of these policies</span></span>

## <a name="simulating-risk-events"></a><span data-ttu-id="c7767-108">위험 이벤트 시뮬레이션</span><span class="sxs-lookup"><span data-stu-id="c7767-108">Simulating Risk Events</span></span>
<span data-ttu-id="c7767-109">이 섹션에서는 다음 위험 이벤트 유형을 시뮬레이트하는 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-109">This section provides you with steps for simulating the following risk event types:</span></span>

* <span data-ttu-id="c7767-110">익명 IP 주소에서 로그인(초급)</span><span class="sxs-lookup"><span data-stu-id="c7767-110">Sign-ins from anonymous IP addresses (easy)</span></span>
* <span data-ttu-id="c7767-111">잘 모르는 위치에서 로그인(중급)</span><span class="sxs-lookup"><span data-stu-id="c7767-111">Sign-ins from unfamiliar locations (moderate)</span></span>
* <span data-ttu-id="c7767-112">비정상적 위치로 불가능한 이동(고급)</span><span class="sxs-lookup"><span data-stu-id="c7767-112">Impossible travel to atypical locations (difficult)</span></span>

<span data-ttu-id="c7767-113">안전한 방법으로 다른 위험 이벤트를 시뮬레이션할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-113">Other risk events cannot be simulated in a secure manner.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="c7767-114">익명 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="c7767-114">Sign-ins from anonymous IP addresses</span></span>
<span data-ttu-id="c7767-115">이 위험 이벤트 유형은 익명 프록시 IP 주소로 식별된 IP 주소에서 시도하여 성공적으로 로그인한 사용자를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-115">This risk event type identifies users who have successfully signed in from an IP address that has been identified as an anonymous proxy IP address.</span></span> <span data-ttu-id="c7767-116">이 프록시는 해당 장치의 IP 주소를 숨기려는 사용자가 사용하며 악의적인 의도로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-116">These proxies are used by people who want to hide their device’s IP address and may be used for malicious intent.</span></span>

<span data-ttu-id="c7767-117">**익명 IP에서 로그인을 시뮬레이트하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c7767-117">**To simulate a sign-in from an anonymous IP, perform the following steps**:</span></span>

1. <span data-ttu-id="c7767-118">[Tor 브라우저](https://www.torproject.org/projects/torbrowser.html.en)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-118">Download the [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span></span>
2. <span data-ttu-id="c7767-119">Tor 브라우저를 사용하여 [https://myapps.microsoft.com](https://myapps.microsoft.com)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-119">Using the Tor Browser, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>   
3. <span data-ttu-id="c7767-120">**익명 IP 주소에서 로그인** 보고서에 표시하려는 계정의 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-120">Enter the credentials of the account you want to appear in the **Sign-ins from anonymous IP addresses** report.</span></span>

<span data-ttu-id="c7767-121">로그인이 5분 이내에 ID 보호 대시보드에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-121">The sign-in will show up on the Identity Protection dashboard within 5 minutes.</span></span> 

### <a name="sign-ins-from-unfamiliar-locations"></a><span data-ttu-id="c7767-122">알 수 없는 위치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="c7767-122">Sign-ins from unfamiliar locations</span></span>
<span data-ttu-id="c7767-123">알 수 없는 위치 위험은 새로운 위치/알 수 없는 위치를 확인하기 위해 과거 로그인 위치(IP, 위도/경도 및 ASN)를 고려하는 실시간 로그인 평가 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-123">The unfamiliar locations risk is a real-time sign-in evaluation mechanism that considers past sign-in locations (IP, Latitude / Longitude and ASN) to determine new / unfamiliar locations.</span></span> <span data-ttu-id="c7767-124">시스템은 이전 IP, 위도/경도 및 사용자의 ASN을 저장하고 익숙한 위치인지 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-124">The system stores previous IPs, Latitude / Longitude, and ASNs of a user and considers these to be familiar locations.</span></span> <span data-ttu-id="c7767-125">로그인 위치가 기존의 익숙한 위치 중 하나와 일치하지 않는 경우 로그인 위치는 알 수 없는 위치로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-125">A sign-in location is considered unfamiliar if the sign-in location does not match any of the existing familiar locations.</span></span>

<span data-ttu-id="c7767-126">Azure Active Directory ID 보호:</span><span class="sxs-lookup"><span data-stu-id="c7767-126">Azure Active Directory Identity Protection:</span></span>  

* <span data-ttu-id="c7767-127">새로운 위치를 알 수 없는 위치의 플래그로 지정하지 않는 14일의 초기 학습 기간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-127">has an initial learning period of 14 days during which it does not flag any new locations as unfamiliar locations.</span></span>
* <span data-ttu-id="c7767-128">익숙한 장치 및 기존의 익숙한 위치에 지리적으로 가까운 위치에서 시도한 로그인을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-128">ignores sign-ins from familiar devices and locations that are geographically close to an existing familiar location.</span></span>

<span data-ttu-id="c7767-129">알 수 없는 위치를 시뮬레이트하려면 계정이 이전에 로그인하지 않은 위치 및 장치에서 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-129">To simulate unfamiliar locations, you have to sign in from a location and device that the account has not signed in from before.</span></span> 

<span data-ttu-id="c7767-130">**익숙하지 않은 위치에서 로그인을 시뮬레이트하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c7767-130">**To simulate a sign-in from an unfamiliar location, perform the following steps**:</span></span>

1. <span data-ttu-id="c7767-131">적어도 14일의 로그인 기록이 있는 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-131">Choose an account that has at least a 14-day sign-in history.</span></span> 
2. <span data-ttu-id="c7767-132">다음 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-132">Do either:</span></span>
   
   <span data-ttu-id="c7767-133">a.</span><span class="sxs-lookup"><span data-stu-id="c7767-133">a.</span></span> <span data-ttu-id="c7767-134">VPN을 사용하는 동안 [https://myapps.microsoft.com](https://myapps.microsoft.com) 로 이동하고 위험 이벤트를 시뮬레이트하려는 계정의 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-134">While using a VPN, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com) and enter the credentials of the account you want to simulate the risk event for.</span></span>
   
   <span data-ttu-id="c7767-135">b.</span><span class="sxs-lookup"><span data-stu-id="c7767-135">b.</span></span> <span data-ttu-id="c7767-136">계정의 자격 증명을 사용하여 로그인하는 다른 위치에 연결을 요청합니다(권장하지 않음).</span><span class="sxs-lookup"><span data-stu-id="c7767-136">Ask an associate in a different location to sign in using the account’s credentials (not recommended).</span></span>

<span data-ttu-id="c7767-137">로그인이 5분 이내에 ID 보호 대시보드에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-137">The sign-in will show up on the Identity Protection dashboard within 5 minutes.</span></span>

### <a name="impossible-travel-to-atypical-location"></a><span data-ttu-id="c7767-138">비정상적 위치로 불가능한 이동</span><span class="sxs-lookup"><span data-stu-id="c7767-138">Impossible travel to atypical location</span></span>
<span data-ttu-id="c7767-139">알고리즘이 기계 학습을 사용하여 익숙한 장치에서 불가능한 이동 또는 디렉터리의 다른 사용자가 사용하는 VPN에서 시도한 로그인 등 가양성을 걸러내기 때문에 불가능한 이동 조건을 시뮬레이트하는 작업은 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-139">Simulating the impossible travel condition is difficult because the algorithm uses machine learning to weed out false-positives such as impossible travel from familiar devices, or sign-ins from VPNs that are used by other users in the directory.</span></span> <span data-ttu-id="c7767-140">또한 알고리즘은 위험 이벤트의 생성을 시작하기 전에 사용자에 대한 3-14일 간의 로그인 기록이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-140">Additionally, the algorithm requires a sign-in history of 3 to 14 days for the user before it begins generating risk events.</span></span>

<span data-ttu-id="c7767-141">**비정상적 위치로 불가능한 이동을 시뮬레이트하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c7767-141">**To simulate an impossible travel to atypical location, perform the following steps**:</span></span>

1. <span data-ttu-id="c7767-142">표준 브라우저를 사용하여 [https://myapps.microsoft.com](https://myapps.microsoft.com)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-142">Using your standard browser, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>  
2. <span data-ttu-id="c7767-143">불가능한 이동 위험 이벤트를 생성하려는 계정의 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-143">Enter the credentials of the account you want to generate an impossible travel risk event for.</span></span>
3. <span data-ttu-id="c7767-144">사용자 에이전트를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-144">Change your user agent.</span></span> <span data-ttu-id="c7767-145">사용자 에이전트 전환기 추가 기능을 사용하여 개발자 도구에서 Internet Explorer의 사용자 에이전트를 변경하거나 Firefox 또는 Chrome에서 사용자 에이전트를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-145">You can change user agent in Internet Explorer from Developer Tools, or change your user agent in Firefox or Chrome using a user-agent switcher add-on.</span></span>
4. <span data-ttu-id="c7767-146">사용자의 IP 주소를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-146">Change your IP address.</span></span> <span data-ttu-id="c7767-147">VPN, Tor 추가 기능을 사용하거나 다른 데이터 센터의 Azure에서 새 컴퓨터를 스핀업하여 사용자의 IP 주소를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-147">You can change your IP address by using a VPN, a Tor add-on, or spinning up a new machine in Azure in a different data center.</span></span>
5. <span data-ttu-id="c7767-148">이전과 동일한 자격 증명을 사용하여 이전에 로그인한 후 몇 분 내에 [https://myapps.microsoft.com](https://myapps.microsoft.com) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-148">Sign-in to [https://myapps.microsoft.com](https://myapps.microsoft.com) using the same credentials as before and within a few minutes after the previous sign-in.</span></span>

<span data-ttu-id="c7767-149">로그인이 2-4시간 이내에 ID 보호 대시보드에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-149">The sign-in will show up in the Identity Protection dashboard within 2-4 hours.</span></span><br>
<span data-ttu-id="c7767-150">포함된 복잡한 기계 학습 모델 때문에 선택되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-150">Because of the complex machine learning models involved, there is a chance it will not get picked up.</span></span><br> <span data-ttu-id="c7767-151">여러 Azure AD 계정에 이러한 단계를 복제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-151">You might want to replicate these steps for multiple Azure AD accounts.</span></span>

## <a name="simulating-vulnerabilities"></a><span data-ttu-id="c7767-152">취약점 시뮬레이션</span><span class="sxs-lookup"><span data-stu-id="c7767-152">Simulating vulnerabilities</span></span>
<span data-ttu-id="c7767-153">취약점은 잘못된 행위자에 의해 악용될 수 있는 Azure AD 환경의 단점입니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-153">Vulnerabilities are weaknesses in an Azure AD environment that can be exploited by a bad actor.</span></span> <span data-ttu-id="c7767-154">현재 3가지 유형의 취약점은 Azure AD의 다른 기능을 활용하는 Azure AD ID 보호에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-154">Currently 3 types of vulnerabilities are surfaced in Azure AD Identity Protection that leverage other features of Azure AD.</span></span> <span data-ttu-id="c7767-155">이러한 기능이 설정되면 이러한 취약성이 ID 보호 대시보드에 자동으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-155">These Vulnerabilities will be displayed on the Identity Protection dashboard automatically once these features are set up.</span></span>

* <span data-ttu-id="c7767-156">Azure AD [Multi-Factor Authentication이란?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="c7767-156">Azure AD [Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>
* <span data-ttu-id="c7767-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c7767-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>
* <span data-ttu-id="c7767-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c7767-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="user-compromise-risk"></a><span data-ttu-id="c7767-159">사용자 손상 위험</span><span class="sxs-lookup"><span data-stu-id="c7767-159">User compromise risk</span></span>
<span data-ttu-id="c7767-160">**사용자 손상 위험을 테스트하려면 다음 단계를 수행합니다**.</span><span class="sxs-lookup"><span data-stu-id="c7767-160">**To test User compromise risk, perform the following steps**:</span></span>

1. <span data-ttu-id="c7767-161">테넌트에 대한 전역 관리자 자격 증명을 사용하여 [https://portal.azure.com](https://portal.azure.com) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-161">Sign-in to [https://portal.azure.com](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="c7767-162">**ID 보호**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-162">Navigate to **Identity Protection**.</span></span> 
3. <span data-ttu-id="c7767-163">기본 **Azure AD ID 보호** 블레이드에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-163">On the main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="c7767-164">**포털 설정** 블레이드의 **보안 규칙**에서 **사용자 손상 위험**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-164">On the **Portal Settings** blade, under **Security rules**, click **User compromise risk**.</span></span> 
5. <span data-ttu-id="c7767-165">**로그인 위험** 블레이드에서 **규칙 사용**을 끈 다음 **저장** 설정을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-165">On the **Sign in Risk** blade, turn **Enable rule** off, and then click **Save** settings.</span></span>
6. <span data-ttu-id="c7767-166">지정된 사용자 계정의 경우 알 수 없는 위치 또는 익명 IP 위험 이벤트를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-166">For a given user account, simulate an unfamiliar locations or anonymous IP risk event.</span></span> <span data-ttu-id="c7767-167">해당 사용자에 대한 사용자 위험 수준을 **보통**으로 상승합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-167">This will elevate the user risk level for that user to **Medium**.</span></span>
7. <span data-ttu-id="c7767-168">몇 분 정도 기다린 후에 사용자에 대한 해당 사용자 수준이 **보통**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-168">Wait a few minutes, and then verify that user level for your user is **Medium**.</span></span>
8. <span data-ttu-id="c7767-169">**포털 설정** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-169">Go to the **Portal Settings** blade.</span></span>
9. <span data-ttu-id="c7767-170">**사용자 손상 위험** 블레이드의 **규칙 사용**에서 **켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-170">On the **User Compromise Risk** blade, under **Enable rule**, select **On** .</span></span> 
10. <span data-ttu-id="c7767-171">다음 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-171">Select one of the following options:</span></span>
    
    <span data-ttu-id="c7767-172">a.</span><span class="sxs-lookup"><span data-stu-id="c7767-172">a.</span></span> <span data-ttu-id="c7767-173">차단하려면 **로그인 차단**에서 **보통**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-173">To block, select **Medium** under **Block sign in**.</span></span>
    
    <span data-ttu-id="c7767-174">b.</span><span class="sxs-lookup"><span data-stu-id="c7767-174">b.</span></span> <span data-ttu-id="c7767-175">보안 암호 변경을 적용하려면 **Multi-Factor Authentication 요구**에서 **보통**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-175">To enforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
11. <span data-ttu-id="c7767-176">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-176">Click **Save**.</span></span>
12. <span data-ttu-id="c7767-177">이제 위험 수준이 상승한 사용자로 로그인하여 위험 기반 조건부 액세스를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-177">You can now test risk-based conditional access by signing in using a user with an elevated risk level.</span></span> <span data-ttu-id="c7767-178">사용자 위험이 보통인 경우 정책 구성에 따라 로그인이 차단되거나 암호를 변경하도록 강제됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-178">If the user risk is Medium, depending on the configuration of your policy, your sign-in is be either blocked or you are forced to change your password.</span></span> 
    <br><br><span data-ttu-id="c7767-179">
    ![플레이 북](./media/active-directory-identityprotection-playbook/201.png "플레이 북")
    </span><span class="sxs-lookup"><span data-stu-id="c7767-179">
![Playbook](./media/active-directory-identityprotection-playbook/201.png "Playbook")
</span></span><br>

## <a name="sign-in-risk"></a><span data-ttu-id="c7767-180">로그인 위험</span><span class="sxs-lookup"><span data-stu-id="c7767-180">Sign-in risk</span></span>
<span data-ttu-id="c7767-181">**로그인 위험을 테스트하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c7767-181">**To test a sign in risk, perform the following steps:**</span></span>

1. <span data-ttu-id="c7767-182">테넌트에 대한 전역 관리자 자격 증명을 사용하여 [https://portal.azure.com ](https://portal.azure.com) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-182">Sign-in to [https://portal.azure.com ](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="c7767-183">**ID 보호**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-183">Navigate to **Identity Protection**.</span></span>
3. <span data-ttu-id="c7767-184">기본 **Azure AD ID 보호** 블레이드에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-184">On the main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="c7767-185">**포털 설정** 블레이드의 **보안 규칙**에서 **로그인 위험**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-185">On the **Portal Settings** blade, under **Security rules**, click **Sign in risk**.</span></span>
5. <span data-ttu-id="c7767-186">에 * * 위험에 로그인 * * 블레이드를 **에** 아래 **사용 규칙이**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-186">On the **Sign in Risk **blade, select **On** under **Enable rule**.</span></span> 
6. <span data-ttu-id="c7767-187">다음 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-187">Select one of the following options:</span></span>
   
   <span data-ttu-id="c7767-188">a.</span><span class="sxs-lookup"><span data-stu-id="c7767-188">a.</span></span> <span data-ttu-id="c7767-189">차단하려면 **로그인 차단**에서 **보통**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-189">To block, select **Medium** under **Block sign in**</span></span>
   
   <span data-ttu-id="c7767-190">b.</span><span class="sxs-lookup"><span data-stu-id="c7767-190">b.</span></span> <span data-ttu-id="c7767-191">보안 암호 변경을 적용하려면 **Multi-Factor Authentication 요구**에서 **보통**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-191">To enforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
7. <span data-ttu-id="c7767-192">차단하려면 로그인 차단에서 보통을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-192">To block, select Medium under Block sign in.</span></span>
8. <span data-ttu-id="c7767-193">Multi-Factor Authentication을 적용하려면 **Multi-Factor Authentication 요구**에서 **보통**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-193">To enforce multi-factor authentication, select **Medium** under **Require multi-factor authentication**.</span></span>
9. <span data-ttu-id="c7767-194">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-194">Click on **Save**.</span></span>
10. <span data-ttu-id="c7767-195">이제 둘 다 **보통** 위험 이벤트이기 때문에 알 수 없는 위치 또는 익명 IP 위험 이벤트를 시뮬레이트하여 위험 기반 조건부 액세스를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7767-195">You can now test risk-based conditional access by simulating the unfamiliar locations or anonymous IP risk events because they are both **Medium** risk events.</span></span>


<span data-ttu-id="c7767-196">![플레이 북](./media/active-directory-identityprotection-playbook/200.png "플레이 북")</span><span class="sxs-lookup"><span data-stu-id="c7767-196">![Playbook](./media/active-directory-identityprotection-playbook/200.png "Playbook")</span></span>


## <a name="see-also"></a><span data-ttu-id="c7767-197">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c7767-197">See also</span></span>
* [<span data-ttu-id="c7767-198">Azure Active Directory ID 보호</span><span class="sxs-lookup"><span data-stu-id="c7767-198">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

