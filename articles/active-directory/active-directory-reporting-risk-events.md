---
title: "Azure Active Directory 위험 이벤트 | Microsoft Docs"
description: "이 항목에서는 위험 이벤트의 자세한 개요를 제공합니다."
services: active-directory
keywords: "Azure Active Directory ID 보호, 보안, 위험, 위험 이벤트, 취약점, 보안 정책"
author: MarkusVi
manager: femila
ms.assetid: fa2c8b51-d43d-4349-8308-97e87665400b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 71ab5cb02ac70871fb8207ab9220b45d1c842dde
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-risk-events"></a><span data-ttu-id="24a9a-104">Azure Active Directory 위험 이벤트</span><span class="sxs-lookup"><span data-stu-id="24a9a-104">Azure Active Directory risk events</span></span>

<span data-ttu-id="24a9a-105">대부분의 보안 침해는 공격자가 사용자의 ID를 도용하여 환경에 대한 액세스 권한을 얻을 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-105">The vast majority of security breaches take place when attackers gain access to an environment by stealing a user’s identity.</span></span> <span data-ttu-id="24a9a-106">손상된 ID를 검색하는 것은 쉬운 작업이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-106">Discovering compromised identities is no easy task.</span></span> <span data-ttu-id="24a9a-107">Azure Active Directory는 적응 기계 학습 알고리즘 및 추론을 사용하여 사용자의 계정과 관련된 의심스러운 작업을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-107">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user accounts.</span></span> <span data-ttu-id="24a9a-108">검색된 각 의심스러운 동작은 *위험 이벤트*라는 레코드에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-108">Each detected suspicious action is stored in a record called *risk event*.</span></span>

<span data-ttu-id="24a9a-109">현재, Azure Active Directory는 6가지 유형의 위험 이벤트를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-109">Currently, Azure Active Directory detects six types of risk events:</span></span>

- [<span data-ttu-id="24a9a-110">자격 증명이 손실된 사용자</span><span class="sxs-lookup"><span data-stu-id="24a9a-110">Users with leaked credentials</span></span>](#leaked-credentials) 
- [<span data-ttu-id="24a9a-111">익명 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="24a9a-111">Sign-ins from anonymous IP addresses</span></span>](#sign-ins-from-anonymous-ip-addresses) 
- [<span data-ttu-id="24a9a-112">비정상적 위치로 불가능한 이동</span><span class="sxs-lookup"><span data-stu-id="24a9a-112">Impossible travel to atypical locations</span></span>](#impossible-travel-to-atypical-locations) 
- [<span data-ttu-id="24a9a-113">알 수 없는 위치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="24a9a-113">Sign-ins from unfamiliar locations</span></span>](#sign-in-from-unfamiliar-locations)
- [<span data-ttu-id="24a9a-114">감염된 장치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="24a9a-114">Sign-ins from infected devices</span></span>](#sign-ins-from-infected-devices) 
- [<span data-ttu-id="24a9a-115">의심스러운 작업이 있는 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="24a9a-115">Sign-ins from IP addresses with suspicious activity</span></span>](#sign-ins-from-ip-addresses-with-suspicious-activity) 


![위험 이벤트](./media/active-directory-reporting-risk-events/91.png)

<span data-ttu-id="24a9a-117">이 항목에서는 위험 이벤트의 자세한 개요와 이를 사용하여 Azure AD ID를 보호하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-117">This topic gives you a detailed overview of what risk events are and how you can use them to protect your Azure AD identities.</span></span>


## <a name="risk-event-types"></a><span data-ttu-id="24a9a-118">위험 이벤트 유형</span><span class="sxs-lookup"><span data-stu-id="24a9a-118">Risk event types</span></span>

<span data-ttu-id="24a9a-119">위험 이벤트 유형 속성은 위험 이벤트 레코드가 만들어진 의심스러운 동작의 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-119">The risk event type property is an identifier for the suspicious action a risk event record has been created for.</span></span>  
<span data-ttu-id="24a9a-120">검색 프로세스에 대한 Microsoft의 지속적인 투자는 다음과 같은 결과를 가져왔습니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-120">Microsoft's continuous investments into the detection process lead to:</span></span>

- <span data-ttu-id="24a9a-121">기존 위험 이벤트의 검색 정확도 향상</span><span class="sxs-lookup"><span data-stu-id="24a9a-121">Improvements to the detection accuracy of existing risk events</span></span> 
- <span data-ttu-id="24a9a-122">향후 추가될 새 위험 이벤트 유형</span><span class="sxs-lookup"><span data-stu-id="24a9a-122">New risk event types that will be added in the future</span></span>

### <a name="leaked-credentials"></a><span data-ttu-id="24a9a-123">유출된 자격 증명</span><span class="sxs-lookup"><span data-stu-id="24a9a-123">Leaked credentials</span></span>

<span data-ttu-id="24a9a-124">사이버 범죄자가 합법적인 사용자의 유효한 암호를 손상시키는 경우 범죄자는 종종 이러한 자격 증명을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-124">When cybercriminals compromise valid passwords of legitimate users, the criminals often share those credentials.</span></span> <span data-ttu-id="24a9a-125">보통 이러한 작업은 Dark 웹 또는 붙여넣기 사이트에 공개적으로 게시하거나 암시장에서 자격 증명을 거래 또는 판매하는 방식으로 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-125">This is usually done by posting them publicly on the dark web or paste sites or by trading or selling the credentials on the black market.</span></span> <span data-ttu-id="24a9a-126">Microsoft 유출된 자격 증명 서비스는 공개 및 Dark 웹 사이트를 모니터링하고 다음 대상과 협력하여 사용자 이름/암호 쌍을 획득합니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-126">The Microsoft leaked credentials service acquires username / password pairs by monitoring public and dark web sites and by working with:</span></span>

- <span data-ttu-id="24a9a-127">연구원</span><span class="sxs-lookup"><span data-stu-id="24a9a-127">Researchers</span></span>
- <span data-ttu-id="24a9a-128">사법 기관</span><span class="sxs-lookup"><span data-stu-id="24a9a-128">Law enforcement</span></span>
- <span data-ttu-id="24a9a-129">Microsoft 보안 팀</span><span class="sxs-lookup"><span data-stu-id="24a9a-129">Security teams at Microsoft</span></span>
- <span data-ttu-id="24a9a-130">신뢰할 수 있는 기타 소스</span><span class="sxs-lookup"><span data-stu-id="24a9a-130">Other trusted sources</span></span> 

<span data-ttu-id="24a9a-131">서비스에서 사용자 이름/암호 쌍을 획득하면 AAD에 대해 사용자의 현재 유효한 자격 증명인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-131">When the service acquires username / password pairs, they are checked against AAD users' current valid credentials.</span></span> <span data-ttu-id="24a9a-132">일치하면 사용자의 암호가 손상된 것이며 *누출된 자격 증명 위험 이벤트*가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-132">When a match is found, it means that a user's password has been compromised, and a *leaked credentials risk event* is created.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="24a9a-133">익명 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="24a9a-133">Sign-ins from anonymous IP addresses</span></span>

<span data-ttu-id="24a9a-134">이 위험 이벤트 유형은 익명 프록시 IP 주소로 식별된 IP 주소에서 시도하여 성공적으로 로그인한 사용자를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-134">This risk event type identifies users who have successfully signed in from an IP address that has been identified as an anonymous proxy IP address.</span></span> <span data-ttu-id="24a9a-135">이 프록시는 해당 장치의 IP 주소를 숨기려는 사용자가 사용하며 악의적인 의도로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-135">These proxies are used by people who want to hide their device’s IP address, and may be used for malicious intent.</span></span>


### <a name="impossible-travel-to-atypical-locations"></a><span data-ttu-id="24a9a-136">비정상적 위치로 불가능한 이동</span><span class="sxs-lookup"><span data-stu-id="24a9a-136">Impossible travel to atypical locations</span></span>

<span data-ttu-id="24a9a-137">이 위험 이벤트 유형은 지역적으로 떨어진 위치에서 시작한 두 번의 로그인을 식별합니다. 과거 동작을 고려하면 이 위치 중 하나 이상이 사용자에 대해 불규칙적입니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-137">This risk event type identifies two sign-ins originating from geographically distant locations, where at least one of the locations may also be atypical for the user, given past behavior.</span></span> <span data-ttu-id="24a9a-138">또한 두 번의 로그인 간의 시간은 사용자가 첫 번째 위치에서 두 번째 위치로 이동하는 데 걸리는 시간보다 짧습니다. 이는 서로 다른 사용자가 동일한 자격 증명을 사용하고 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-138">In addition, the time between the two sign-ins is shorter than the time it would have taken the user to travel from the first location to the second, indicating that a different user is using the same credentials.</span></span> 

<span data-ttu-id="24a9a-139">조직의 다른 사용자가 정기적으로 사용하는 VPN 및 위치와 같은 불가능한 이동 조건에 영향을 주는 확실한 "*가양성*"을 무시하는 기계 학습 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-139">This machine learning algorithm that ignores obvious "*false positives*" contributing to the impossible travel condition, such as VPNs and locations regularly used by other users in the organization.</span></span>  <span data-ttu-id="24a9a-140">시스템에는 새 사용자의 로그인 동작을 알아보는 동안 14일의 초기 학습 기간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-140">The system has an initial learning period of 14 days during which it learns a new user’s sign-in behavior.</span></span>

### <a name="sign-in-from-unfamiliar-locations"></a><span data-ttu-id="24a9a-141">잘 모르는 위치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="24a9a-141">Sign-in from unfamiliar locations</span></span>

<span data-ttu-id="24a9a-142">이 위험 이벤트 유형은 새로운/알 수 없는 위치를 확인하기 위해 과거 로그인 위치(IP, 위도/경도 및 ASN)를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-142">This risk event type considers past sign-in locations (IP, Latitude / Longitude and ASN) to determine new / unfamiliar locations.</span></span> <span data-ttu-id="24a9a-143">시스템은 사용자가 사용한 이전 위치에 대한 정보를 저장하고 이러한 "익숙한" 위치를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-143">The system stores information about previous locations used by a user, and considers these “familiar” locations.</span></span> <span data-ttu-id="24a9a-144">로그인이 익숙한 위치 목록에 없는 위치에서 발생하는 경우 위험 이벤트가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-144">The risk event is triggered when the sign-in occurs from a location that's not already in the list of familiar locations.</span></span> <span data-ttu-id="24a9a-145">시스템에는 새로운 위치를 알 수 없는 위치의 플래그로 지정하지 않는 30일의 초기 학습 기간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-145">The system has an initial learning period of 30 days, during which it does not flag any new locations as unfamiliar locations.</span></span> <span data-ttu-id="24a9a-146">또한 시스템은 익숙한 장치 및 익숙한 위치에 지리적으로 가까운 위치에서 시도한 로그인을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-146">The system also ignores sign-ins from familiar devices, and locations that are geographically close to a familiar location.</span></span> 

### <a name="sign-ins-from-infected-devices"></a><span data-ttu-id="24a9a-147">감염된 장치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="24a9a-147">Sign-ins from infected devices</span></span>

<span data-ttu-id="24a9a-148">이 위험 이벤트 유형은 적극적으로 봇 서버와 통신한다고 알려진 맬웨어로 감염된 장치에서 시도한 로그인을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-148">This risk event type identifies sign-ins from devices infected with malware, that are known to actively communicate with a bot server.</span></span> <span data-ttu-id="24a9a-149">봇 서버와 접촉했던 IP 주소에 대해 사용자의 장치의 IP 주소를 상호 연결하여 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-149">This is determined by correlating IP addresses of the user’s device against IP addresses that were in contact with a bot server.</span></span> 

### <a name="sign-ins-from-ip-addresses-with-suspicious-activity"></a><span data-ttu-id="24a9a-150">의심스러운 작업이 있는 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="24a9a-150">Sign-ins from IP addresses with suspicious activity</span></span>
<span data-ttu-id="24a9a-151">이 위험 이벤트 유형은 짧은 기간 동안에 여러 사용자 계정에서 실패한 로그인 시도가 많이 확인되는 IP 주소를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-151">This risk event type identifies IP addresses from which a high number of failed sign-in attempts were seen, across multiple user accounts, over a short period of time.</span></span> <span data-ttu-id="24a9a-152">이는 공격자가 사용하는 IP 주소의 트래픽 패턴과 일치하며 계정이 이미 또는 손상되었거나 손상될 것이라는 확실한 지표입니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-152">This matches traffic patterns of IP addresses used by attackers, and is a strong indicator that accounts are either already or are about to be compromised.</span></span> <span data-ttu-id="24a9a-153">조직의 다른 사용자가 정기적으로 사용하는 IP 주소와 같은 명백한 "*가양성*"을 무시하는 기계 학습 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-153">This is a machine learning algorithm that ignores obvious "*false-positives*", such as IP addresses that are regularly used by other users in the organization.</span></span>  <span data-ttu-id="24a9a-154">시스템에는 새 사용자 및 새 테넌트의 로그인 동작을 알아보는 14일의 초기 학습 기간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-154">The system has an initial learning period of 14 days where it learns the sign-in behavior of a new user and new tenant.</span></span>


## <a name="detection-type"></a><span data-ttu-id="24a9a-155">검색 유형</span><span class="sxs-lookup"><span data-stu-id="24a9a-155">Detection type</span></span>

<span data-ttu-id="24a9a-156">검색 유형 속성은 위험 이벤트의 검색 기간에 대한 지표입니다(실시간 또는 오프라인).</span><span class="sxs-lookup"><span data-stu-id="24a9a-156">The detection type property is an indicator (Real-time or Offline) for the detection timeframe of a risk event.</span></span>  
<span data-ttu-id="24a9a-157">현재 대부분의 위험 이벤트는 위험 이벤트가 발생되고 사후 처리 작업에서 오프라인으로 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-157">Currently, most risk events are detected offline in a post-processing operation after the risk event has occurred.</span></span>

<span data-ttu-id="24a9a-158">다음 표에는 검색 유형이 관련 보고서에 표시되는 데 걸리는 시간이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-158">The following table lists the amount of time it takes for a detection type to show up in a related report:</span></span>

| <span data-ttu-id="24a9a-159">검색 유형</span><span class="sxs-lookup"><span data-stu-id="24a9a-159">Detection Type</span></span> | <span data-ttu-id="24a9a-160">보고 대기 시간</span><span class="sxs-lookup"><span data-stu-id="24a9a-160">Reporting Latency</span></span> |
| --- | --- |
| <span data-ttu-id="24a9a-161">실시간</span><span class="sxs-lookup"><span data-stu-id="24a9a-161">Real-time</span></span> | <span data-ttu-id="24a9a-162">5~10분</span><span class="sxs-lookup"><span data-stu-id="24a9a-162">5 to 10 minutes</span></span> |
| <span data-ttu-id="24a9a-163">오프라인</span><span class="sxs-lookup"><span data-stu-id="24a9a-163">Offline</span></span> | <span data-ttu-id="24a9a-164">2~4시간</span><span class="sxs-lookup"><span data-stu-id="24a9a-164">2 to 4 hours</span></span> |


<span data-ttu-id="24a9a-165">Azure Active Directory가 검색하는 위험 이벤트 유형의 경우 검색 유형은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-165">For the risk event types Azure Active Directory detects, the detection types are:</span></span>

| <span data-ttu-id="24a9a-166">위험 이벤트 유형</span><span class="sxs-lookup"><span data-stu-id="24a9a-166">Risk Event Type</span></span> | <span data-ttu-id="24a9a-167">검색 유형</span><span class="sxs-lookup"><span data-stu-id="24a9a-167">Detection Type</span></span> |
| :-- | --- | 
| [<span data-ttu-id="24a9a-168">자격 증명이 손실된 사용자</span><span class="sxs-lookup"><span data-stu-id="24a9a-168">Users with leaked credentials</span></span>](#leaked-credentials) | <span data-ttu-id="24a9a-169">오프라인</span><span class="sxs-lookup"><span data-stu-id="24a9a-169">Offline</span></span> |
| [<span data-ttu-id="24a9a-170">익명 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="24a9a-170">Sign-ins from anonymous IP addresses</span></span>](#sign-ins-from-anonymous-ip-addresses) | <span data-ttu-id="24a9a-171">실시간</span><span class="sxs-lookup"><span data-stu-id="24a9a-171">Real-time</span></span> |
| [<span data-ttu-id="24a9a-172">비정상적 위치로 불가능한 이동</span><span class="sxs-lookup"><span data-stu-id="24a9a-172">Impossible travel to atypical locations</span></span>](#impossible-travel-to-atypical-locations) | <span data-ttu-id="24a9a-173">오프라인</span><span class="sxs-lookup"><span data-stu-id="24a9a-173">Offline</span></span> |
| [<span data-ttu-id="24a9a-174">알 수 없는 위치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="24a9a-174">Sign-ins from unfamiliar locations</span></span>](#sign-in-from-unfamiliar-locations) | <span data-ttu-id="24a9a-175">실시간</span><span class="sxs-lookup"><span data-stu-id="24a9a-175">Real-time</span></span> |
| [<span data-ttu-id="24a9a-176">감염된 장치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="24a9a-176">Sign-ins from infected devices</span></span>](#sign-ins-from-infected-devices) | <span data-ttu-id="24a9a-177">오프라인</span><span class="sxs-lookup"><span data-stu-id="24a9a-177">Offline</span></span> |
| [<span data-ttu-id="24a9a-178">의심스러운 작업이 있는 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="24a9a-178">Sign-ins from IP addresses with suspicious activity</span></span>](#sign-ins-from-ip-addresses-with-suspicious-activity) | <span data-ttu-id="24a9a-179">오프라인</span><span class="sxs-lookup"><span data-stu-id="24a9a-179">Offline</span></span>|


## <a name="risk-level"></a><span data-ttu-id="24a9a-180">위험 수준</span><span class="sxs-lookup"><span data-stu-id="24a9a-180">Risk level</span></span>

<span data-ttu-id="24a9a-181">위험 이벤트의 위험 수준 속성은 위험 이벤트의 심각도 및 신뢰도에 대한 지표입니다(높음, 보통 또는 낮음).</span><span class="sxs-lookup"><span data-stu-id="24a9a-181">The risk level property of a risk event is an indicator (High, Medium, or Low) for the severity and the confidence of a risk event.</span></span> <span data-ttu-id="24a9a-182">이 속성은 수행해야 하는 작업의 우선 순위를 지정하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-182">This property helps you to prioritize the actions you must take.</span></span> 

<span data-ttu-id="24a9a-183">위험 이벤트의 심각도는 신호의 강도를 ID 손상의 예측 변수로 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-183">The severity of the risk event represents the strength of the signal as a predictor of identity compromise.</span></span>  
<span data-ttu-id="24a9a-184">신뢰도는 가양성의 가능성에 대한 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-184">The confidence is an indicator for the possibility of false positives.</span></span> 

<span data-ttu-id="24a9a-185">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-185">For example,</span></span> 

* <span data-ttu-id="24a9a-186">**높음**: 신뢰도 및 심각도가 높은 위험 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-186">**High**: High confidence and high severity risk event.</span></span> <span data-ttu-id="24a9a-187">이러한 이벤트는 사용자의 ID가 손상되었음을 나타내는 확실한 지표이며 영향을 받는 모든 사용자는 즉시 수정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-187">These events are strong indicators that the user’s identity has been compromised, and any user accounts impacted should be remediated immediately.</span></span>

* <span data-ttu-id="24a9a-188">**보통**: 심각도가 높지만 신뢰도가 낮은 위험 이벤트 또는 그 반대의 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-188">**Medium**: High severity, but lower confidence risk event, or vice versa.</span></span> <span data-ttu-id="24a9a-189">이러한 이벤트는 잠재적으로 위험하며 영향을 받는 사용자 계정은 수정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-189">These events are potentially risky, and any user accounts impacted should be remediated.</span></span>

* <span data-ttu-id="24a9a-190">**낮음**: 신뢰도 및 심각도가 낮은 위험 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-190">**Low**: Low confidence and low severity risk event.</span></span> <span data-ttu-id="24a9a-191">이 이벤트는 즉각적인 조치가 필요하지 않을 수 있지만 다른 위험 이벤트와 결합되면 ID가 손상되었음을 확실하게 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-191">This event may not require an immediate action, but when combined with other risk events, may provide a strong indication that the identity is compromised.</span></span>

![위험 수준](./media/active-directory-reporting-risk-events/01.png)

### <a name="leaked-credentials"></a><span data-ttu-id="24a9a-193">유출된 자격 증명</span><span class="sxs-lookup"><span data-stu-id="24a9a-193">Leaked credentials</span></span>

<span data-ttu-id="24a9a-194">사용자 이름 및 암호를 공격자가 사용할 수 있다고 명백히 표시하기 때문에 유출된 자격 증명 위험 이벤트는 **높음**으로 분류됩니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-194">Leaked credentials risk events are classified as a **High**, because they provide a clear indication that the user name and password are available to an attacker.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="24a9a-195">익명 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="24a9a-195">Sign-ins from anonymous IP addresses</span></span>

<span data-ttu-id="24a9a-196">익명 IP 주소는 계정 손상을 확실히 표시하지 않기 때문에 이 위험 이벤트 유형의 위험 수준은 **보통**입니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-196">The risk level for this risk event type is **Medium** because an anonymous IP address is not a strong indication of an account compromise.</span></span>  
<span data-ttu-id="24a9a-197">사용자에게 즉시 문의하여 익명 IP 주소를 사용했는지를 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-197">We recommend that you immediately contact the user to verify if they were using anonymous IP addresses.</span></span>


### <a name="impossible-travel-to-atypical-locations"></a><span data-ttu-id="24a9a-198">비정상적 위치로 불가능한 이동</span><span class="sxs-lookup"><span data-stu-id="24a9a-198">Impossible travel to atypical locations</span></span>

<span data-ttu-id="24a9a-199">불가능한 이동은 일반적으로 해커가 성공적으로 로그인할 수 있는 훌륭한 지표입니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-199">Impossible travel is usually a good indicator that a hacker was able to successfully sign-in.</span></span> <span data-ttu-id="24a9a-200">그러나 사용자가 새 장치를 사용하거나 조직의 다른 사용자가 일반적으로 사용하지 않는 VPN을 사용하여 이동하는 경우 가양성이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-200">However, false-positives may occur when a user is traveling using a new device or using a VPN that is typically not used by other users in the organization.</span></span> <span data-ttu-id="24a9a-201">가양성의 다른 원본은 서버 IP 및 클라이언트 IP를 정확하지 않게 전달하는 응용 프로그램이며 응용 프로그램의 백 엔드가 호스팅되는 데이터 센터에서 발생하는 로그인의 모양을 가져올 수 있습니다(대개 이러한 Microsoft 데이터 센터는 Microsoft에서 소유한 고유의 IP 주소를 발생시키는 로그인의 모양을 제공할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="24a9a-201">Another source of false-positives is applications that incorrectly pass server IPs as client IPs, which may give the appearance of sign-ins taking place from the data center where that application’s back-end is hosted (often these are Microsoft datacenters, which may give the appearance of sign-ins taking place from Microsoft owned IP addresses).</span></span> <span data-ttu-id="24a9a-202">이러한 가양성의 결과로 이 위험 이벤트에 대한 위험 수준은 **보통**입니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-202">As a result of these false-positives, the risk level for this risk event is **Medium**.</span></span>

> [!TIP]
> <span data-ttu-id="24a9a-203">[명명된 위치](active-directory-named-locations.md)를 구성하여 이 위험 이벤트 형식에 대해 보고된 가양성의 양을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-203">You can reduce the amount of reported false-positves for this risk event type by configuring [named locations](active-directory-named-locations.md).</span></span> 

### <a name="sign-in-from-unfamiliar-locations"></a><span data-ttu-id="24a9a-204">잘 모르는 위치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="24a9a-204">Sign-in from unfamiliar locations</span></span>

<span data-ttu-id="24a9a-205">알 수 없는 위치는 공격자가 도난당한 ID를 사용할 수 있다는 확실한 표시를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-205">Unfamiliar locations can provide a strong indication that an attacker is able to use a stolen identity.</span></span> <span data-ttu-id="24a9a-206">가양성은 사용자가 이동하거나, 새 장치를 사용하거나, 새 VPN을 사용할 때 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-206">False-positives may occur when a user is traveling, is trying out a new device, or is using a new VPN.</span></span> <span data-ttu-id="24a9a-207">이러한 가양성의 결과로 이 이벤트 유형의 위험 수준은 **보통**입니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-207">As a result of these false positives, the risk level for this event type is **Medium**.</span></span>

### <a name="sign-ins-from-infected-devices"></a><span data-ttu-id="24a9a-208">감염된 장치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="24a9a-208">Sign-ins from infected devices</span></span>

<span data-ttu-id="24a9a-209">이 위험 이벤트는 사용자 장치가 아닌 IP 주소를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-209">This risk event identifies IP addresses, not user devices.</span></span> <span data-ttu-id="24a9a-210">여러 장치에서 단일 IP 주소를 지지하고 일부만 봇 네트워크에서 제어하는 경우 다른 장치에서 시도한 로그인은 이 이벤트를 불필요하게 트리거할 수 있습니다. 이러한 이유로 해당 위험 이벤트를 **낮음**으로 분류합니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-210">If several devices are behind a single IP address, and only some are controlled by a bot network, sign-ins from other devices my trigger this event unnecessarily, which is the reason for classifying this risk event as **Low**.</span></span>  

<span data-ttu-id="24a9a-211">사용자에게 연락하고 모든 사용자 장치를 검사하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-211">We recommend that you contact the user and scan all the user's devices.</span></span> <span data-ttu-id="24a9a-212">사용자의 개인 장치가 감염되었거나 이전에 언급했듯이 사용자 이외의 다른 사람이 사용자와 동일한 IP 주소에서 감염된 장치를 사용했을 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-212">It is also possible that a user's personal device is infected, or as mentioned earlier, that someone else was using an infected device from the same IP address as the user.</span></span> <span data-ttu-id="24a9a-213">감염된 장치는 종종 바이러스 백신 소프트웨어로 아직 식별되지 않는 맬웨어로 감염됩니다. 또한 장치에 감염을 일으킬 수 있는 잘못된 사용자 습관을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-213">Infected devices are often infected by malware that have not yet been identified by anti-virus software, and may also indicate as bad user habits that may have caused the device to become infected.</span></span>

<span data-ttu-id="24a9a-214">맬웨어 감염을 해결하는 방법에 대한 자세한 내용은 [맬웨어 보호 센터](http://go.microsoft.com/fwlink/?linkid=335773&clcid=0x409)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24a9a-214">For more information about how to address malware infections, see the [Malware Protection Center](http://go.microsoft.com/fwlink/?linkid=335773&clcid=0x409).</span></span>


### <a name="sign-ins-from-ip-addresses-with-suspicious-activity"></a><span data-ttu-id="24a9a-215">의심스러운 작업이 있는 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="24a9a-215">Sign-ins from IP addresses with suspicious activity</span></span>

<span data-ttu-id="24a9a-216">사용자에게 문의하여 의심스럽다고 표시된 IP 주소에서 실제로 로그인했는지를 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-216">We recommend that you contact the user to verify if they actually signed in from an IP address that was marked as suspicious.</span></span> <span data-ttu-id="24a9a-217">일부가 의심스러운 작업에 책임이 있을 수 있는 반면 동일한 IP 주소에 여러 장치가 있을 수 있으므로 이 이벤트 유형의 위험 수준은 "**보통**"입니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-217">The risk level for this event type is “**Medium**” because several devices may be behind the same IP address, while only some may be responsible for the suspicious activity.</span></span> 


 
## <a name="next-steps"></a><span data-ttu-id="24a9a-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="24a9a-218">Next steps</span></span>

<span data-ttu-id="24a9a-219">위험 이벤트는 Azure AD의 ID 보호에 대한 기반입니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-219">Risk events are the foundation for protecting your Azure AD's identities.</span></span> <span data-ttu-id="24a9a-220">Azure AD는 현재 여섯 가지 위험 이벤트를 감지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-220">Azure AD can currently detect six risk events:</span></span> 


| <span data-ttu-id="24a9a-221">위험 이벤트 유형</span><span class="sxs-lookup"><span data-stu-id="24a9a-221">Risk Event Type</span></span> | <span data-ttu-id="24a9a-222">위험 수준</span><span class="sxs-lookup"><span data-stu-id="24a9a-222">Risk Level</span></span> | <span data-ttu-id="24a9a-223">검색 유형</span><span class="sxs-lookup"><span data-stu-id="24a9a-223">Detection Type</span></span> |
| :-- | --- | --- |
| [<span data-ttu-id="24a9a-224">자격 증명이 손실된 사용자</span><span class="sxs-lookup"><span data-stu-id="24a9a-224">Users with leaked credentials</span></span>](#leaked-credentials) | <span data-ttu-id="24a9a-225">높음</span><span class="sxs-lookup"><span data-stu-id="24a9a-225">High</span></span> | <span data-ttu-id="24a9a-226">오프라인</span><span class="sxs-lookup"><span data-stu-id="24a9a-226">Offline</span></span> |
| [<span data-ttu-id="24a9a-227">익명 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="24a9a-227">Sign-ins from anonymous IP addresses</span></span>](#sign-ins-from-anonymous-ip-addresses) | <span data-ttu-id="24a9a-228">중간</span><span class="sxs-lookup"><span data-stu-id="24a9a-228">Medium</span></span> | <span data-ttu-id="24a9a-229">실시간</span><span class="sxs-lookup"><span data-stu-id="24a9a-229">Real-time</span></span> |
| [<span data-ttu-id="24a9a-230">비정상적 위치로 불가능한 이동</span><span class="sxs-lookup"><span data-stu-id="24a9a-230">Impossible travel to atypical locations</span></span>](#impossible-travel-to-atypical-locations) | <span data-ttu-id="24a9a-231">중간</span><span class="sxs-lookup"><span data-stu-id="24a9a-231">Medium</span></span> | <span data-ttu-id="24a9a-232">오프라인</span><span class="sxs-lookup"><span data-stu-id="24a9a-232">Offline</span></span> |
| [<span data-ttu-id="24a9a-233">알 수 없는 위치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="24a9a-233">Sign-ins from unfamiliar locations</span></span>](#sign-in-from-unfamiliar-locations) | <span data-ttu-id="24a9a-234">중간</span><span class="sxs-lookup"><span data-stu-id="24a9a-234">Medium</span></span> | <span data-ttu-id="24a9a-235">실시간</span><span class="sxs-lookup"><span data-stu-id="24a9a-235">Real-time</span></span> |
| [<span data-ttu-id="24a9a-236">감염된 장치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="24a9a-236">Sign-ins from infected devices</span></span>](#sign-ins-from-infected-devices) | <span data-ttu-id="24a9a-237">낮음</span><span class="sxs-lookup"><span data-stu-id="24a9a-237">Low</span></span> | <span data-ttu-id="24a9a-238">오프라인</span><span class="sxs-lookup"><span data-stu-id="24a9a-238">Offline</span></span> |
| [<span data-ttu-id="24a9a-239">의심스러운 작업이 있는 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="24a9a-239">Sign-ins from IP addresses with suspicious activity</span></span>](#sign-ins-from-ip-addresses-with-suspicious-activity) | <span data-ttu-id="24a9a-240">중간</span><span class="sxs-lookup"><span data-stu-id="24a9a-240">Medium</span></span> | <span data-ttu-id="24a9a-241">오프라인</span><span class="sxs-lookup"><span data-stu-id="24a9a-241">Offline</span></span>|

<span data-ttu-id="24a9a-242">사용자 환경에서 검색된 위험 이벤트는 어디에서 확인할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="24a9a-242">Where can you find the risk events that have been detected in your environment?</span></span>
<span data-ttu-id="24a9a-243">두 곳에서 보고된 위험 이벤트를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-243">There are two places where you review reported risk events:</span></span>

 - <span data-ttu-id="24a9a-244">**Azure AD 보고** - 위험 이벤트는 Azure AD의 보안 보고서의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-244">**Azure AD reporting** - Risk events are part of Azure AD's security reports.</span></span> <span data-ttu-id="24a9a-245">자세한 내용은 [위험에 노출된 사용자 보안 보고서](active-directory-reporting-security-user-at-risk.md) 및 [위험한 로그인 보안 보고서](active-directory-reporting-security-risky-sign-ins.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24a9a-245">For more details, see the [users at risk security report](active-directory-reporting-security-user-at-risk.md) and the [risky sign-ins security report](active-directory-reporting-security-risky-sign-ins.md).</span></span>

 - <span data-ttu-id="24a9a-246">**Azure AD ID 보호** - 위험 이벤트는 [Azure Active Directory ID 보호](active-directory-identityprotection.md) 보고 기능의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-246">**Azure AD Identity Protection** - Risk events are also part of [Azure Active Directory Identity Protection's](active-directory-identityprotection.md) reporting capabilities.</span></span>
    

<span data-ttu-id="24a9a-247">위험 이벤트의 감지는 ID 보호의 중요한 측면을 나타내는 반면 수동으로 해결하거나 조건부 액세스 정책을 구성하여 자동화된 응답을 구현하는 옵션도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24a9a-247">While the detection of risk events already represents an important aspect of protecting your identities, you also have the option to either manually address them or even implement automated responses by configuring conditional access policies.</span></span> <span data-ttu-id="24a9a-248">자세한 내용은 [Azure Active Directory ID 보호](active-directory-identityprotection.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24a9a-248">For more details, see of [Azure Active Directory Identity Protection's](active-directory-identityprotection.md).</span></span>
 
