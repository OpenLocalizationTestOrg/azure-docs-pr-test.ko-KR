---
title: "Active Directory Id 보호 플레이 북 aaaAzure | Microsoft Docs"
description: "Azure AD Identity Protection을 통해 방법을 공격자가 tooexploit 노출된 된 id의 toolimit hello 능력 또는 장치와 toosecure id 또는 장치 의심 되는 또는 알려진 toobe를 이전에 손상에 대해 알아봅니다."
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
ms.openlocfilehash: 6252bc133fc0c0f84800ee245a04bbf62d4cd25b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-playbook"></a><span data-ttu-id="8f0c2-104">Azure Active Directory ID 보호 플레이 북</span><span class="sxs-lookup"><span data-stu-id="8f0c2-104">Azure Active Directory Identity Protection playbook</span></span>
<span data-ttu-id="8f0c2-105">이 플레이 북은 다음 작업을 수행하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-105">This playbook helps you to:</span></span>

* <span data-ttu-id="8f0c2-106">위험 이벤트 시뮬레이션 및 취약성 여 hello Id 보호 환경에서 데이터를 채울</span><span class="sxs-lookup"><span data-stu-id="8f0c2-106">Populate data in hello Identity Protection environment by simulating risk events and vulnerabilities</span></span>
* <span data-ttu-id="8f0c2-107">위험 기반 조건부 액세스 정책을 설정 및 테스트 이러한 정책의 hello 영향</span><span class="sxs-lookup"><span data-stu-id="8f0c2-107">Set up risk-based conditional access policies and test hello impact of these policies</span></span>

## <a name="simulating-risk-events"></a><span data-ttu-id="8f0c2-108">위험 이벤트 시뮬레이션</span><span class="sxs-lookup"><span data-stu-id="8f0c2-108">Simulating Risk Events</span></span>
<span data-ttu-id="8f0c2-109">이 섹션에서는 위험 이벤트 유형만 hello를 시뮬레이트하기 위한 단계를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-109">This section provides you with steps for simulating hello following risk event types:</span></span>

* <span data-ttu-id="8f0c2-110">익명 IP 주소에서 로그인(초급)</span><span class="sxs-lookup"><span data-stu-id="8f0c2-110">Sign-ins from anonymous IP addresses (easy)</span></span>
* <span data-ttu-id="8f0c2-111">잘 모르는 위치에서 로그인(중급)</span><span class="sxs-lookup"><span data-stu-id="8f0c2-111">Sign-ins from unfamiliar locations (moderate)</span></span>
* <span data-ttu-id="8f0c2-112">이동 불가능 tooatypical 위치 (어려운)</span><span class="sxs-lookup"><span data-stu-id="8f0c2-112">Impossible travel tooatypical locations (difficult)</span></span>

<span data-ttu-id="8f0c2-113">안전한 방법으로 다른 위험 이벤트를 시뮬레이션할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-113">Other risk events cannot be simulated in a secure manner.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="8f0c2-114">익명 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="8f0c2-114">Sign-ins from anonymous IP addresses</span></span>
<span data-ttu-id="8f0c2-115">이 위험 이벤트 유형은 익명 프록시 IP 주소로 식별된 IP 주소에서 시도하여 성공적으로 로그인한 사용자를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-115">This risk event type identifies users who have successfully signed in from an IP address that has been identified as an anonymous proxy IP address.</span></span> <span data-ttu-id="8f0c2-116">이러한 프록시는 원하는 toohide 사람에 의해 해당 장치의 IP 주소를 사용 하 고 악의적인 의도에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-116">These proxies are used by people who want toohide their device’s IP address and may be used for malicious intent.</span></span>

<span data-ttu-id="8f0c2-117">**익명 IP에서 로그인에 toosimulate 수행할 단계를 수행 하는 hello**:</span><span class="sxs-lookup"><span data-stu-id="8f0c2-117">**toosimulate a sign-in from an anonymous IP, perform hello following steps**:</span></span>

1. <span data-ttu-id="8f0c2-118">Hello 다운로드 [Tor 브라우저](https://www.torproject.org/projects/torbrowser.html.en)합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-118">Download hello [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span></span>
2. <span data-ttu-id="8f0c2-119">Hello Tor 브라우저를 사용 하 여 이동 너무[https://myapps.microsoft.com](https://myapps.microsoft.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-119">Using hello Tor Browser, navigate too[https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>   
3. <span data-ttu-id="8f0c2-120">Hello에 tooappear hello 계정 hello 자격 증명을 입력 **익명 IP 주소에서 로그인** 보고서입니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-120">Enter hello credentials of hello account you want tooappear in hello **Sign-ins from anonymous IP addresses** report.</span></span>

<span data-ttu-id="8f0c2-121">hello에 대 한 로그인에 표시 됩니다 hello Id 보호 대시보드 5 분 이내입니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-121">hello sign-in will show up on hello Identity Protection dashboard within 5 minutes.</span></span> 

### <a name="sign-ins-from-unfamiliar-locations"></a><span data-ttu-id="8f0c2-122">알 수 없는 위치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="8f0c2-122">Sign-ins from unfamiliar locations</span></span>
<span data-ttu-id="8f0c2-123">hello 생소 한 위치 위험은 로그인 위치 지난 간주 하는 실시간 로그인 평가 메커니즘 (IP, 위도 / 경도 및 ASN) toodetermine 새 / 생소 한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-123">hello unfamiliar locations risk is a real-time sign-in evaluation mechanism that considers past sign-in locations (IP, Latitude / Longitude and ASN) toodetermine new / unfamiliar locations.</span></span> <span data-ttu-id="8f0c2-124">hello 시스템 저장 이전 ip 주소로 위도 / 경도 및 사용자의 Asn 이러한 toobe 친숙 한 위치 않은 것으로 간주 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-124">hello system stores previous IPs, Latitude / Longitude, and ASNs of a user and considers these toobe familiar locations.</span></span> <span data-ttu-id="8f0c2-125">로그인 위치 hello 로그인 위치와 일치 하지 않으면 hello 기존 친숙 한 위치에 익숙하지 않은 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-125">A sign-in location is considered unfamiliar if hello sign-in location does not match any of hello existing familiar locations.</span></span>

<span data-ttu-id="8f0c2-126">Azure Active Directory ID 보호:</span><span class="sxs-lookup"><span data-stu-id="8f0c2-126">Azure Active Directory Identity Protection:</span></span>  

* <span data-ttu-id="8f0c2-127">새로운 위치를 알 수 없는 위치의 플래그로 지정하지 않는 14일의 초기 학습 기간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-127">has an initial learning period of 14 days during which it does not flag any new locations as unfamiliar locations.</span></span>
* <span data-ttu-id="8f0c2-128">친숙 한 장치 및 위치를 지리적으로 닫기 tooan 기존 친숙 한 위치에서 로그인을 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-128">ignores sign-ins from familiar devices and locations that are geographically close tooan existing familiar location.</span></span>

<span data-ttu-id="8f0c2-129">toosimulate 생소 한 위치를가지고 toosign 위치와 hello 계정에 로그인 하지에서 하기 전에 장치에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-129">toosimulate unfamiliar locations, you have toosign in from a location and device that hello account has not signed in from before.</span></span> 

<span data-ttu-id="8f0c2-130">**로그인 생소 한 위치에서 toosimulate 수행할 단계를 수행 하는 hello**:</span><span class="sxs-lookup"><span data-stu-id="8f0c2-130">**toosimulate a sign-in from an unfamiliar location, perform hello following steps**:</span></span>

1. <span data-ttu-id="8f0c2-131">적어도 14일의 로그인 기록이 있는 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-131">Choose an account that has at least a 14-day sign-in history.</span></span> 
2. <span data-ttu-id="8f0c2-132">다음 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-132">Do either:</span></span>
   
   <span data-ttu-id="8f0c2-133">a.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-133">a.</span></span> <span data-ttu-id="8f0c2-134">VPN을 사용 하는 동안 이동 너무[https://myapps.microsoft.com](https://myapps.microsoft.com) toosimulate hello 위험 이벤트에 대 한 hello 계정 hello 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-134">While using a VPN, navigate too[https://myapps.microsoft.com](https://myapps.microsoft.com) and enter hello credentials of hello account you want toosimulate hello risk event for.</span></span>
   
   <span data-ttu-id="8f0c2-135">b.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-135">b.</span></span> <span data-ttu-id="8f0c2-136">(권장 하지 않음) hello 계정의 자격 증명을 사용 하 여 다른 위치 toosign에서 동료에 게 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-136">Ask an associate in a different location toosign in using hello account’s credentials (not recommended).</span></span>

<span data-ttu-id="8f0c2-137">hello에 대 한 로그인에 표시 됩니다 hello Id 보호 대시보드 5 분 이내입니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-137">hello sign-in will show up on hello Identity Protection dashboard within 5 minutes.</span></span>

### <a name="impossible-travel-tooatypical-location"></a><span data-ttu-id="8f0c2-138">이동 불가능 tooatypical 위치</span><span class="sxs-lookup"><span data-stu-id="8f0c2-138">Impossible travel tooatypical location</span></span>
<span data-ttu-id="8f0c2-139">Hello 알고리즘 거짓 긍정 hello 디렉터리에 다른 사용자가 사용 되는 Vpn에서 로그인 등 친숙 한 장치에서 이동 불가능으로 컴퓨터 학습 tooweed 사용 하기 때문에 hello 이동 불가능 조건을 시뮬레이션 하는 것은 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-139">Simulating hello impossible travel condition is difficult because hello algorithm uses machine learning tooweed out false-positives such as impossible travel from familiar devices, or sign-ins from VPNs that are used by other users in hello directory.</span></span> <span data-ttu-id="8f0c2-140">또한 hello 알고리즘 위험 이벤트 생성을 시작 하기 전에 3 too14 일 로그인 기록을 hello 사용자에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-140">Additionally, hello algorithm requires a sign-in history of 3 too14 days for hello user before it begins generating risk events.</span></span>

<span data-ttu-id="8f0c2-141">**toosimulate 이동 불가능 tooatypical 위치를 사용 하는 단계를 수행 하는 hello 수행**:</span><span class="sxs-lookup"><span data-stu-id="8f0c2-141">**toosimulate an impossible travel tooatypical location, perform hello following steps**:</span></span>

1. <span data-ttu-id="8f0c2-142">표준 브라우저를 사용 하 여 이동 너무[https://myapps.microsoft.com](https://myapps.microsoft.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-142">Using your standard browser, navigate too[https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>  
2. <span data-ttu-id="8f0c2-143">Toogenerate에 대 한 이동 불가능 위험 이벤트를 원하는 hello 계정의 hello 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-143">Enter hello credentials of hello account you want toogenerate an impossible travel risk event for.</span></span>
3. <span data-ttu-id="8f0c2-144">사용자 에이전트를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-144">Change your user agent.</span></span> <span data-ttu-id="8f0c2-145">사용자 에이전트 전환기 추가 기능을 사용하여 개발자 도구에서 Internet Explorer의 사용자 에이전트를 변경하거나 Firefox 또는 Chrome에서 사용자 에이전트를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-145">You can change user agent in Internet Explorer from Developer Tools, or change your user agent in Firefox or Chrome using a user-agent switcher add-on.</span></span>
4. <span data-ttu-id="8f0c2-146">사용자의 IP 주소를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-146">Change your IP address.</span></span> <span data-ttu-id="8f0c2-147">VPN, Tor 추가 기능을 사용하거나 다른 데이터 센터의 Azure에서 새 컴퓨터를 스핀업하여 사용자의 IP 주소를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-147">You can change your IP address by using a VPN, a Tor add-on, or spinning up a new machine in Azure in a different data center.</span></span>
5. <span data-ttu-id="8f0c2-148">로그인 너무[https://myapps.microsoft.com](https://myapps.microsoft.com) 이전 처럼 및 hello 이전 로그인 후 몇 분 내에 동일한 자격 증명을 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-148">Sign-in too[https://myapps.microsoft.com](https://myapps.microsoft.com) using hello same credentials as before and within a few minutes after hello previous sign-in.</span></span>

<span data-ttu-id="8f0c2-149">hello에 대 한 로그인에에서 표시 됩니다 hello Id 보호 대시보드 2-4 시간 이내입니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-149">hello sign-in will show up in hello Identity Protection dashboard within 2-4 hours.</span></span><br>
<span data-ttu-id="8f0c2-150">학습 모델에 관련 된 복잡 한 컴퓨터 hello 인해 하도록 선택 하지 됩니다 것 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-150">Because of hello complex machine learning models involved, there is a chance it will not get picked up.</span></span><br> <span data-ttu-id="8f0c2-151">여러 Azure AD 계정에 대 한 tooreplicate 다음이 단계를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-151">You might want tooreplicate these steps for multiple Azure AD accounts.</span></span>

## <a name="simulating-vulnerabilities"></a><span data-ttu-id="8f0c2-152">취약점 시뮬레이션</span><span class="sxs-lookup"><span data-stu-id="8f0c2-152">Simulating vulnerabilities</span></span>
<span data-ttu-id="8f0c2-153">취약점은 잘못된 행위자에 의해 악용될 수 있는 Azure AD 환경의 단점입니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-153">Vulnerabilities are weaknesses in an Azure AD environment that can be exploited by a bad actor.</span></span> <span data-ttu-id="8f0c2-154">현재 3가지 유형의 취약점은 Azure AD의 다른 기능을 활용하는 Azure AD ID 보호에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-154">Currently 3 types of vulnerabilities are surfaced in Azure AD Identity Protection that leverage other features of Azure AD.</span></span> <span data-ttu-id="8f0c2-155">이러한 취약점 나타납니다 hello Identity Protection 대시보드에서 자동으로 이러한 기능이 설정 되 면 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-155">These Vulnerabilities will be displayed on hello Identity Protection dashboard automatically once these features are set up.</span></span>

* <span data-ttu-id="8f0c2-156">Azure AD [Multi-Factor Authentication이란?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="8f0c2-156">Azure AD [Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>
* <span data-ttu-id="8f0c2-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8f0c2-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>
* <span data-ttu-id="8f0c2-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="8f0c2-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="user-compromise-risk"></a><span data-ttu-id="8f0c2-159">사용자 손상 위험</span><span class="sxs-lookup"><span data-stu-id="8f0c2-159">User compromise risk</span></span>
<span data-ttu-id="8f0c2-160">**사용자 손상 위험 tootest 수행할 단계를 수행 하는 hello**:</span><span class="sxs-lookup"><span data-stu-id="8f0c2-160">**tootest User compromise risk, perform hello following steps**:</span></span>

1. <span data-ttu-id="8f0c2-161">로그인 너무[https://portal.azure.com](https://portal.azure.com) 테 넌 트에 대 한 전역 관리자 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-161">Sign-in too[https://portal.azure.com](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="8f0c2-162">너무 이동**Id 보호**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-162">Navigate too**Identity Protection**.</span></span> 
3. <span data-ttu-id="8f0c2-163">주 hello에 **Azure AD Identity Protection** 블레이드에서 클릭 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-163">On hello main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="8f0c2-164">Hello에 **포털 설정** 블레이드 아래 **보안 규칙**, 클릭 **사용자 손상 위험**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-164">On hello **Portal Settings** blade, under **Security rules**, click **User compromise risk**.</span></span> 
5. <span data-ttu-id="8f0c2-165">Hello에 **위험에 로그인** 블레이드에서 설정 **사용 규칙이** 있는데 클릭 **저장** 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-165">On hello **Sign in Risk** blade, turn **Enable rule** off, and then click **Save** settings.</span></span>
6. <span data-ttu-id="8f0c2-166">지정된 사용자 계정의 경우 알 수 없는 위치 또는 익명 IP 위험 이벤트를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-166">For a given user account, simulate an unfamiliar locations or anonymous IP risk event.</span></span> <span data-ttu-id="8f0c2-167">이 권한 상승 해당 사용자에 대 한 hello 사용자 위험 수준을 너무**보통**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-167">This will elevate hello user risk level for that user too**Medium**.</span></span>
7. <span data-ttu-id="8f0c2-168">몇 분 정도 기다린 후에 사용자에 대한 해당 사용자 수준이 **보통**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-168">Wait a few minutes, and then verify that user level for your user is **Medium**.</span></span>
8. <span data-ttu-id="8f0c2-169">Toohello 이동 **포털 설정** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-169">Go toohello **Portal Settings** blade.</span></span>
9. <span data-ttu-id="8f0c2-170">Hello에 **사용자 손상 위험** 블레이드 아래 **사용 규칙이**선택, **에** 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-170">On hello **User Compromise Risk** blade, under **Enable rule**, select **On** .</span></span> 
10. <span data-ttu-id="8f0c2-171">Hello 다음 옵션 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-171">Select one of hello following options:</span></span>
    
    <span data-ttu-id="8f0c2-172">a.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-172">a.</span></span> <span data-ttu-id="8f0c2-173">tooblock, **보통** 아래 **블록 로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-173">tooblock, select **Medium** under **Block sign in**.</span></span>
    
    <span data-ttu-id="8f0c2-174">b.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-174">b.</span></span> <span data-ttu-id="8f0c2-175">선택 tooenforce 보안 된 암호 변경 **보통** 아래 **multi-factor authentication 필요**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-175">tooenforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
11. <span data-ttu-id="8f0c2-176">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-176">Click **Save**.</span></span>
12. <span data-ttu-id="8f0c2-177">이제 위험 수준이 상승한 사용자로 로그인하여 위험 기반 조건부 액세스를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-177">You can now test risk-based conditional access by signing in using a user with an elevated risk level.</span></span> <span data-ttu-id="8f0c2-178">Hello 사용자 위험 중간 이면 hello 구성 정책에 따라 사용자 로그인이 차단 하거나 또는 toochange 강제 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-178">If hello user risk is Medium, depending on hello configuration of your policy, your sign-in is be either blocked or you are forced toochange your password.</span></span> 
    <br><br><span data-ttu-id="8f0c2-179">
    ![플레이 북](./media/active-directory-identityprotection-playbook/201.png "플레이 북")
    </span><span class="sxs-lookup"><span data-stu-id="8f0c2-179">
![Playbook](./media/active-directory-identityprotection-playbook/201.png "Playbook")
</span></span><br>

## <a name="sign-in-risk"></a><span data-ttu-id="8f0c2-180">로그인 위험</span><span class="sxs-lookup"><span data-stu-id="8f0c2-180">Sign-in risk</span></span>
<span data-ttu-id="8f0c2-181">**tootest 위험 로그인 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="8f0c2-181">**tootest a sign in risk, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f0c2-182">로그인 너무[https://portal.azure.com ](https://portal.azure.com) 테 넌 트에 대 한 전역 관리자 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-182">Sign-in too[https://portal.azure.com ](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="8f0c2-183">너무 이동**Id 보호**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-183">Navigate too**Identity Protection**.</span></span>
3. <span data-ttu-id="8f0c2-184">주 hello에 **Azure AD Identity Protection** 블레이드에서 클릭 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-184">On hello main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="8f0c2-185">Hello에 **포털 설정** 블레이드 아래 **보안 규칙**, 클릭 **위험 로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-185">On hello **Portal Settings** blade, under **Security rules**, click **Sign in risk**.</span></span>
5. <span data-ttu-id="8f0c2-186">Hello에 * * 위험 로그인 * * 블레이드를 **에** 아래 **사용 규칙이**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-186">On hello **Sign in Risk **blade, select **On** under **Enable rule**.</span></span> 
6. <span data-ttu-id="8f0c2-187">Hello 다음 옵션 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-187">Select one of hello following options:</span></span>
   
   <span data-ttu-id="8f0c2-188">a.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-188">a.</span></span> <span data-ttu-id="8f0c2-189">tooblock, **보통** 아래 **블록에 로그인**</span><span class="sxs-lookup"><span data-stu-id="8f0c2-189">tooblock, select **Medium** under **Block sign in**</span></span>
   
   <span data-ttu-id="8f0c2-190">b.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-190">b.</span></span> <span data-ttu-id="8f0c2-191">선택 tooenforce 보안 된 암호 변경 **보통** 아래 **multi-factor authentication 필요**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-191">tooenforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
7. <span data-ttu-id="8f0c2-192">tooblock, 블록 아래 선택 중간에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-192">tooblock, select Medium under Block sign in.</span></span>
8. <span data-ttu-id="8f0c2-193">tooenforce multi-factor authentication을 선택 **보통** 아래 **multi-factor authentication 필요**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-193">tooenforce multi-factor authentication, select **Medium** under **Require multi-factor authentication**.</span></span>
9. <span data-ttu-id="8f0c2-194">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-194">Click on **Save**.</span></span>
10. <span data-ttu-id="8f0c2-195">이제 hello 생소 한 위치를 시뮬레이션 하 여 위험을 기준으로 조건부 액세스를 테스트할 수 있습니다 또는 둘 다 되기 때문에 익명 IP 위험 이벤트 **보통** 이벤트 위험 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f0c2-195">You can now test risk-based conditional access by simulating hello unfamiliar locations or anonymous IP risk events because they are both **Medium** risk events.</span></span>


<span data-ttu-id="8f0c2-196">![플레이 북](./media/active-directory-identityprotection-playbook/200.png "플레이 북")</span><span class="sxs-lookup"><span data-stu-id="8f0c2-196">![Playbook](./media/active-directory-identityprotection-playbook/200.png "Playbook")</span></span>


## <a name="see-also"></a><span data-ttu-id="8f0c2-197">참고 항목</span><span class="sxs-lookup"><span data-stu-id="8f0c2-197">See also</span></span>
* [<span data-ttu-id="8f0c2-198">Azure Active Directory ID 보호</span><span class="sxs-lookup"><span data-stu-id="8f0c2-198">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

