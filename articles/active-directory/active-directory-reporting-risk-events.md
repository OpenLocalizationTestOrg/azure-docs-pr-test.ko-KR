---
title: "Active Directory 위험 이벤트 aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: d771c1f43707744aac728c4f72000d855cbd6e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-risk-events"></a><span data-ttu-id="4834e-104">Azure Active Directory 위험 이벤트</span><span class="sxs-lookup"><span data-stu-id="4834e-104">Azure Active Directory risk events</span></span>

<span data-ttu-id="4834e-105">공격자는 사용자의 id를 도용 하 여 액세스 tooan 환경 수 hello 포함 된 대부분의 보안 위반 걸릴 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-105">hello vast majority of security breaches take place when attackers gain access tooan environment by stealing a user’s identity.</span></span> <span data-ttu-id="4834e-106">손상된 ID를 검색하는 것은 쉬운 작업이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-106">Discovering compromised identities is no easy task.</span></span> <span data-ttu-id="4834e-107">Azure Active Directory 적응 컴퓨터 학습 알고리즘 및 추론 toodetect 의심 스러운 동작을 관련된 tooyour 사용자 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-107">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="4834e-108">검색된 각 의심스러운 동작은 *위험 이벤트*라는 레코드에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-108">Each detected suspicious action is stored in a record called *risk event*.</span></span>

<span data-ttu-id="4834e-109">현재, Azure Active Directory는 6가지 유형의 위험 이벤트를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-109">Currently, Azure Active Directory detects six types of risk events:</span></span>

- [<span data-ttu-id="4834e-110">자격 증명이 손실된 사용자</span><span class="sxs-lookup"><span data-stu-id="4834e-110">Users with leaked credentials</span></span>](#leaked-credentials) 
- [<span data-ttu-id="4834e-111">익명 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="4834e-111">Sign-ins from anonymous IP addresses</span></span>](#sign-ins-from-anonymous-ip-addresses) 
- [<span data-ttu-id="4834e-112">이동 불가능 tooatypical 위치</span><span class="sxs-lookup"><span data-stu-id="4834e-112">Impossible travel tooatypical locations</span></span>](#impossible-travel-to-atypical-locations) 
- [<span data-ttu-id="4834e-113">알 수 없는 위치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="4834e-113">Sign-ins from unfamiliar locations</span></span>](#sign-in-from-unfamiliar-locations)
- [<span data-ttu-id="4834e-114">감염된 장치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="4834e-114">Sign-ins from infected devices</span></span>](#sign-ins-from-infected-devices) 
- [<span data-ttu-id="4834e-115">의심스러운 작업이 있는 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="4834e-115">Sign-ins from IP addresses with suspicious activity</span></span>](#sign-ins-from-ip-addresses-with-suspicious-activity) 


![위험 이벤트](./media/active-directory-reporting-risk-events/91.png)

<span data-ttu-id="4834e-117">이 항목에서는 위험 이벤트의 자세한 개요는 하 고 사용 하는 방법으로 tooprotect Azure AD id 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-117">This topic gives you a detailed overview of what risk events are and how you can use them tooprotect your Azure AD identities.</span></span>


## <a name="risk-event-types"></a><span data-ttu-id="4834e-118">위험 이벤트 유형</span><span class="sxs-lookup"><span data-stu-id="4834e-118">Risk event types</span></span>

<span data-ttu-id="4834e-119">hello 위험 이벤트 유형 속성은 hello 의심 스러운 동작 위험 이벤트 레코드에 대 한 식별자에 대해 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-119">hello risk event type property is an identifier for hello suspicious action a risk event record has been created for.</span></span>  
<span data-ttu-id="4834e-120">Microsoft의 지속적인 투자 hello 검색 프로세스를 사항이 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-120">Microsoft's continuous investments into hello detection process lead to:</span></span>

- <span data-ttu-id="4834e-121">기존 위험 이벤트의 toohello 검색 정확도 향상</span><span class="sxs-lookup"><span data-stu-id="4834e-121">Improvements toohello detection accuracy of existing risk events</span></span> 
- <span data-ttu-id="4834e-122">Hello 앞에 추가 될 새 위험 이벤트 유형</span><span class="sxs-lookup"><span data-stu-id="4834e-122">New risk event types that will be added in hello future</span></span>

### <a name="leaked-credentials"></a><span data-ttu-id="4834e-123">유출된 자격 증명</span><span class="sxs-lookup"><span data-stu-id="4834e-123">Leaked credentials</span></span>

<span data-ttu-id="4834e-124">사이버 범죄자 들 손상 합법적인 사용자의 유효한 암호 때 hello 범죄자는 종종 해당 자격 증명을 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-124">When cybercriminals compromise valid passwords of legitimate users, hello criminals often share those credentials.</span></span> <span data-ttu-id="4834e-125">이 게시 함으로써 공개적으로 hello 어두운 붙여넣기 또는 웹 사이트 또는에 거래 또는 hello 자격 증명 hello 검정 시장에 판매 하 여 일반적으로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-125">This is usually done by posting them publicly on hello dark web or paste sites or by trading or selling hello credentials on hello black market.</span></span> <span data-ttu-id="4834e-126">hello Microsoft 유출 자격 증명 서비스 획득 사용자 이름 / 암호 쌍을 사용 하 여 및 어두운 및 공용 웹 사이트를 모니터링 하 여:</span><span class="sxs-lookup"><span data-stu-id="4834e-126">hello Microsoft leaked credentials service acquires username / password pairs by monitoring public and dark web sites and by working with:</span></span>

- <span data-ttu-id="4834e-127">연구원</span><span class="sxs-lookup"><span data-stu-id="4834e-127">Researchers</span></span>
- <span data-ttu-id="4834e-128">사법 기관</span><span class="sxs-lookup"><span data-stu-id="4834e-128">Law enforcement</span></span>
- <span data-ttu-id="4834e-129">Microsoft 보안 팀</span><span class="sxs-lookup"><span data-stu-id="4834e-129">Security teams at Microsoft</span></span>
- <span data-ttu-id="4834e-130">신뢰할 수 있는 기타 소스</span><span class="sxs-lookup"><span data-stu-id="4834e-130">Other trusted sources</span></span> 

<span data-ttu-id="4834e-131">Hello 서비스 사용자 이름을 획득 하는 경우 / 암호 쌍은 대해 검사 하 여 AAD 사용자의 현재 유효한 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-131">When hello service acquires username / password pairs, they are checked against AAD users' current valid credentials.</span></span> <span data-ttu-id="4834e-132">일치하면 사용자의 암호가 손상된 것이며 *누출된 자격 증명 위험 이벤트*가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-132">When a match is found, it means that a user's password has been compromised, and a *leaked credentials risk event* is created.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="4834e-133">익명 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="4834e-133">Sign-ins from anonymous IP addresses</span></span>

<span data-ttu-id="4834e-134">이 위험 이벤트 유형은 익명 프록시 IP 주소로 식별된 IP 주소에서 시도하여 성공적으로 로그인한 사용자를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-134">This risk event type identifies users who have successfully signed in from an IP address that has been identified as an anonymous proxy IP address.</span></span> <span data-ttu-id="4834e-135">이러한 프록시는 원하는 toohide 사람에 의해 해당 장치의 IP 주소를 사용 하 고 악의적인 공격에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-135">These proxies are used by people who want toohide their device’s IP address, and may be used for malicious intent.</span></span>


### <a name="impossible-travel-tooatypical-locations"></a><span data-ttu-id="4834e-136">이동 불가능 tooatypical 위치</span><span class="sxs-lookup"><span data-stu-id="4834e-136">Impossible travel tooatypical locations</span></span>

<span data-ttu-id="4834e-137">이 위험 이벤트 유형 식별 2 회의 로그인 동작 과거 여기서 hello 위치 중 하나 이상을 수도 있습니다 hello 사용자에 대 한 불규칙, 지리적으로 멀리 떨어진 위치에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-137">This risk event type identifies two sign-ins originating from geographically distant locations, where at least one of hello locations may also be atypical for hello user, given past behavior.</span></span> <span data-ttu-id="4834e-138">또한 hello 두 로그인 간 hello 시간은 것이 소요 되었을 hello 사용자 tootravel hello 첫 번째 위치 toohello에서 두 번째 hello 시간 미만, 동일 hello 다른 사용자가 사용 되 고 있는지를 나타내는 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-138">In addition, hello time between hello two sign-ins is shorter than hello time it would have taken hello user tootravel from hello first location toohello second, indicating that a different user is using hello same credentials.</span></span> 

<span data-ttu-id="4834e-139">이 확실 한 무시 하는 기계 학습 알고리즘 "*거짓 긍정*" Vpn 및 hello 조직의 다른 사용자가 정기적으로 사용 되는 위치와 같은 toohello 이동 불가능 조건 기여 합니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-139">This machine learning algorithm that ignores obvious "*false positives*" contributing toohello impossible travel condition, such as VPNs and locations regularly used by other users in hello organization.</span></span>  <span data-ttu-id="4834e-140">hello 시스템 14 일은 새 사용자의 로그인 동작을 파악 하는 초기 학습 기간을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-140">hello system has an initial learning period of 14 days during which it learns a new user’s sign-in behavior.</span></span>

### <a name="sign-in-from-unfamiliar-locations"></a><span data-ttu-id="4834e-141">잘 모르는 위치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="4834e-141">Sign-in from unfamiliar locations</span></span>

<span data-ttu-id="4834e-142">로그인 위치 지난 고려이 위험 이벤트 유형 (IP, 위도 / 경도 및 ASN) toodetermine 새 / 생소 한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-142">This risk event type considers past sign-in locations (IP, Latitude / Longitude and ASN) toodetermine new / unfamiliar locations.</span></span> <span data-ttu-id="4834e-143">hello 시스템 사용자가 사용 되는 이전 위치에 대 한 정보를 저장 하 고 이러한 "친숙 한" 위치를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-143">hello system stores information about previous locations used by a user, and considers these “familiar” locations.</span></span> <span data-ttu-id="4834e-144">hello 위험 이벤트는 hello 로그인 hello 위치 목록에 친숙 하지 않은 위치에서 발생 하는 경우에 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-144">hello risk event is triggered when hello sign-in occurs from a location that's not already in hello list of familiar locations.</span></span> <span data-ttu-id="4834e-145">hello 시스템에 없는 것 표시 하지 않습니다 새 위치를 잘 모르는 위치로 30 일의 초기 학습 기간에는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-145">hello system has an initial learning period of 30 days, during which it does not flag any new locations as unfamiliar locations.</span></span> <span data-ttu-id="4834e-146">hello 시스템도 친숙 한 장치에서 로그인을 무시 하 고 있는 지리적 위치 tooa 친숙 한 위치를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-146">hello system also ignores sign-ins from familiar devices, and locations that are geographically close tooa familiar location.</span></span> 

### <a name="sign-ins-from-infected-devices"></a><span data-ttu-id="4834e-147">감염된 장치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="4834e-147">Sign-ins from infected devices</span></span>

<span data-ttu-id="4834e-148">이 위험 이벤트 유형을 알려진 tooactively 봇 서버와 통신 하는 맬웨어에 감염 된 장치에서 로그인을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-148">This risk event type identifies sign-ins from devices infected with malware, that are known tooactively communicate with a bot server.</span></span> <span data-ttu-id="4834e-149">이 작업은 봇 서버와 접촉 되어 있는 IP 주소에 대 한 hello 사용자의 장치의 IP 주소를 상호 연결 하 여 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-149">This is determined by correlating IP addresses of hello user’s device against IP addresses that were in contact with a bot server.</span></span> 

### <a name="sign-ins-from-ip-addresses-with-suspicious-activity"></a><span data-ttu-id="4834e-150">의심스러운 작업이 있는 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="4834e-150">Sign-ins from IP addresses with suspicious activity</span></span>
<span data-ttu-id="4834e-151">이 위험 이벤트 유형은 짧은 기간 동안에 여러 사용자 계정에서 실패한 로그인 시도가 많이 확인되는 IP 주소를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-151">This risk event type identifies IP addresses from which a high number of failed sign-in attempts were seen, across multiple user accounts, over a short period of time.</span></span> <span data-ttu-id="4834e-152">이 공격자의 목표가 사용 되는 IP 주소의 트래픽 패턴 일치 하며 된 계정 중 하나는 이미 파일이 나 toobe 손상에 대 한 강한 지표.</span><span class="sxs-lookup"><span data-stu-id="4834e-152">This matches traffic patterns of IP addresses used by attackers, and is a strong indicator that accounts are either already or are about toobe compromised.</span></span> <span data-ttu-id="4834e-153">이 확실 한 무시 하는 기계 학습 알고리즘 "*거짓 긍정*"와 같은 IP 주소에 정기적으로 hello 조직의 다른 사용자가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-153">This is a machine learning algorithm that ignores obvious "*false-positives*", such as IP addresses that are regularly used by other users in hello organization.</span></span>  <span data-ttu-id="4834e-154">hello 시스템에 있는 새 사용자와 새 테 넌 트의 hello 로그인 동작을 파악 초기 학습 기간이 14 일입니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-154">hello system has an initial learning period of 14 days where it learns hello sign-in behavior of a new user and new tenant.</span></span>


## <a name="detection-type"></a><span data-ttu-id="4834e-155">검색 유형</span><span class="sxs-lookup"><span data-stu-id="4834e-155">Detection type</span></span>

<span data-ttu-id="4834e-156">hello 검색 type 속성은 표시기 (실시간 또는 오프 라인)는 위험 이벤트의 hello 검색 기간에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-156">hello detection type property is an indicator (Real-time or Offline) for hello detection timeframe of a risk event.</span></span>  
<span data-ttu-id="4834e-157">현재 대부분 위험 이벤트는 오프 라인 상태로 확인 후 처리 작업에서 hello 위험 이벤트 발생 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-157">Currently, most risk events are detected offline in a post-processing operation after hello risk event has occurred.</span></span>

<span data-ttu-id="4834e-158">다음 표에서 hello hello 기간 차지 검색 유형 tooshow에 대 한 관련된 보고서에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-158">hello following table lists hello amount of time it takes for a detection type tooshow up in a related report:</span></span>

| <span data-ttu-id="4834e-159">검색 유형</span><span class="sxs-lookup"><span data-stu-id="4834e-159">Detection Type</span></span> | <span data-ttu-id="4834e-160">보고 대기 시간</span><span class="sxs-lookup"><span data-stu-id="4834e-160">Reporting Latency</span></span> |
| --- | --- |
| <span data-ttu-id="4834e-161">실시간</span><span class="sxs-lookup"><span data-stu-id="4834e-161">Real-time</span></span> | <span data-ttu-id="4834e-162">too10 5 분</span><span class="sxs-lookup"><span data-stu-id="4834e-162">5 too10 minutes</span></span> |
| <span data-ttu-id="4834e-163">오프라인</span><span class="sxs-lookup"><span data-stu-id="4834e-163">Offline</span></span> | <span data-ttu-id="4834e-164">2 too4 시간</span><span class="sxs-lookup"><span data-stu-id="4834e-164">2 too4 hours</span></span> |


<span data-ttu-id="4834e-165">Azure Active Directory 검색 hello 위험 이벤트 유형, hello 검색 유형은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-165">For hello risk event types Azure Active Directory detects, hello detection types are:</span></span>

| <span data-ttu-id="4834e-166">위험 이벤트 유형</span><span class="sxs-lookup"><span data-stu-id="4834e-166">Risk Event Type</span></span> | <span data-ttu-id="4834e-167">검색 유형</span><span class="sxs-lookup"><span data-stu-id="4834e-167">Detection Type</span></span> |
| :-- | --- | 
| [<span data-ttu-id="4834e-168">자격 증명이 손실된 사용자</span><span class="sxs-lookup"><span data-stu-id="4834e-168">Users with leaked credentials</span></span>](#leaked-credentials) | <span data-ttu-id="4834e-169">오프라인</span><span class="sxs-lookup"><span data-stu-id="4834e-169">Offline</span></span> |
| [<span data-ttu-id="4834e-170">익명 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="4834e-170">Sign-ins from anonymous IP addresses</span></span>](#sign-ins-from-anonymous-ip-addresses) | <span data-ttu-id="4834e-171">실시간</span><span class="sxs-lookup"><span data-stu-id="4834e-171">Real-time</span></span> |
| [<span data-ttu-id="4834e-172">이동 불가능 tooatypical 위치</span><span class="sxs-lookup"><span data-stu-id="4834e-172">Impossible travel tooatypical locations</span></span>](#impossible-travel-to-atypical-locations) | <span data-ttu-id="4834e-173">오프라인</span><span class="sxs-lookup"><span data-stu-id="4834e-173">Offline</span></span> |
| [<span data-ttu-id="4834e-174">알 수 없는 위치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="4834e-174">Sign-ins from unfamiliar locations</span></span>](#sign-in-from-unfamiliar-locations) | <span data-ttu-id="4834e-175">실시간</span><span class="sxs-lookup"><span data-stu-id="4834e-175">Real-time</span></span> |
| [<span data-ttu-id="4834e-176">감염된 장치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="4834e-176">Sign-ins from infected devices</span></span>](#sign-ins-from-infected-devices) | <span data-ttu-id="4834e-177">오프라인</span><span class="sxs-lookup"><span data-stu-id="4834e-177">Offline</span></span> |
| [<span data-ttu-id="4834e-178">의심스러운 작업이 있는 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="4834e-178">Sign-ins from IP addresses with suspicious activity</span></span>](#sign-ins-from-ip-addresses-with-suspicious-activity) | <span data-ttu-id="4834e-179">오프라인</span><span class="sxs-lookup"><span data-stu-id="4834e-179">Offline</span></span>|


## <a name="risk-level"></a><span data-ttu-id="4834e-180">위험 수준</span><span class="sxs-lookup"><span data-stu-id="4834e-180">Risk level</span></span>

<span data-ttu-id="4834e-181">위험 이벤트의 hello 위험 수준 속성은 hello 심각도 및 위험 이벤트의 hello 신뢰성에 대 한 표시기 (높음, 중간 또는 낮음)입니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-181">hello risk level property of a risk event is an indicator (High, Medium, or Low) for hello severity and hello confidence of a risk event.</span></span> <span data-ttu-id="4834e-182">이 속성을 사용 tooprioritize hello 작업을 수행 해야 하면 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-182">This property helps you tooprioritize hello actions you must take.</span></span> 

<span data-ttu-id="4834e-183">hello 위험 이벤트의 심각도 hello identity 손상의 예측 hello 신호의 hello 강도를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-183">hello severity of hello risk event represents hello strength of hello signal as a predictor of identity compromise.</span></span>  
<span data-ttu-id="4834e-184">hello 신뢰도의 거짓 긍정 hello 가능성에 대 한 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-184">hello confidence is an indicator for hello possibility of false positives.</span></span> 

<span data-ttu-id="4834e-185">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-185">For example,</span></span> 

* <span data-ttu-id="4834e-186">**높음**: 신뢰도 및 심각도가 높은 위험 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-186">**High**: High confidence and high severity risk event.</span></span> <span data-ttu-id="4834e-187">이러한 이벤트는 강력한 표시기 hello 사용자의 id가 손상 된 및 영향을 받는 모든 사용자 계정에 즉시 재구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-187">These events are strong indicators that hello user’s identity has been compromised, and any user accounts impacted should be remediated immediately.</span></span>

* <span data-ttu-id="4834e-188">**보통**: 심각도가 높지만 신뢰도가 낮은 위험 이벤트 또는 그 반대의 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-188">**Medium**: High severity, but lower confidence risk event, or vice versa.</span></span> <span data-ttu-id="4834e-189">이러한 이벤트는 잠재적으로 위험하며 영향을 받는 사용자 계정은 수정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-189">These events are potentially risky, and any user accounts impacted should be remediated.</span></span>

* <span data-ttu-id="4834e-190">**낮음**: 신뢰도 및 심각도가 낮은 위험 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-190">**Low**: Low confidence and low severity risk event.</span></span> <span data-ttu-id="4834e-191">이 이벤트 즉각적 조치가 필요 하지 않을 수 있지만 다른 위험 이벤트와 함께 사용 하면 identity hello는 손상 된를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-191">This event may not require an immediate action, but when combined with other risk events, may provide a strong indication that hello identity is compromised.</span></span>

![위험 수준](./media/active-directory-reporting-risk-events/01.png)

### <a name="leaked-credentials"></a><span data-ttu-id="4834e-193">유출된 자격 증명</span><span class="sxs-lookup"><span data-stu-id="4834e-193">Leaked credentials</span></span>

<span data-ttu-id="4834e-194">위험 이벤트로 분류 된 자격 증명을 유출는 **높은**뚜렷한 hello 사용자 이름 및 암호는 사용할 수 있는 tooan 공격자를 제공 하므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-194">Leaked credentials risk events are classified as a **High**, because they provide a clear indication that hello user name and password are available tooan attacker.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="4834e-195">익명 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="4834e-195">Sign-ins from anonymous IP addresses</span></span>

<span data-ttu-id="4834e-196">이 위험 이벤트 유형에 대 한 hello 위험 수준이 **보통** 익명 IP 주소는 계정 손상의 강력한 표시 없기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-196">hello risk level for this risk event type is **Medium** because an anonymous IP address is not a strong indication of an account compromise.</span></span>  
<span data-ttu-id="4834e-197">익명 IP 주소 사용 중인 경우 hello 사용자 tooverify 즉시 문의 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-197">We recommend that you immediately contact hello user tooverify if they were using anonymous IP addresses.</span></span>


### <a name="impossible-travel-tooatypical-locations"></a><span data-ttu-id="4834e-198">이동 불가능 tooatypical 위치</span><span class="sxs-lookup"><span data-stu-id="4834e-198">Impossible travel tooatypical locations</span></span>

<span data-ttu-id="4834e-199">이동 불가능는 일반적으로 해커가 수 toosuccessfully 로그인 했음을 나타내는 좋은 지표로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-199">Impossible travel is usually a good indicator that a hacker was able toosuccessfully sign-in.</span></span> <span data-ttu-id="4834e-200">그러나 거짓 긍정 hello 조직의 다른 사용자가 일반적으로 사용 되지 않는 VPN 또는 새 장치를 사용 하 여 사용자가 이동 중 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-200">However, false-positives may occur when a user is traveling using a new device or using a VPN that is typically not used by other users in hello organization.</span></span> <span data-ttu-id="4834e-201">거짓 긍정의 다른 소스는 클라이언트 hello 모양을 초래할 수 있는 Ip로 올바르게 서버 Ip를 전달 하는 응용 프로그램 로그인 수행 하 고 여기서 해당 응용 프로그램의 백 엔드 hello 데이터 센터에서 호스팅되는 (종종 이들은 Microsoft 데이터 센터 hello 모양을 제공 될 수 있습니다 하는 로그인의 IP 주소를 소유 microsoft에서 수행).</span><span class="sxs-lookup"><span data-stu-id="4834e-201">Another source of false-positives is applications that incorrectly pass server IPs as client IPs, which may give hello appearance of sign-ins taking place from hello data center where that application’s back-end is hosted (often these are Microsoft datacenters, which may give hello appearance of sign-ins taking place from Microsoft owned IP addresses).</span></span> <span data-ttu-id="4834e-202">이 위험 이벤트에 대 한 hello 위험 수준을 이러한 거짓 긍정의 결과로 **보통**합니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-202">As a result of these false-positives, hello risk level for this risk event is **Medium**.</span></span>

> [!TIP]
> <span data-ttu-id="4834e-203">구성 하 여이 위험 이벤트 유형에 대 한 보고 된 false positves hello 양을 줄일 수 있습니다 [명명 된 위치](active-directory-named-locations.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-203">You can reduce hello amount of reported false-positves for this risk event type by configuring [named locations](active-directory-named-locations.md).</span></span> 

### <a name="sign-in-from-unfamiliar-locations"></a><span data-ttu-id="4834e-204">잘 모르는 위치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="4834e-204">Sign-in from unfamiliar locations</span></span>

<span data-ttu-id="4834e-205">생소 한 위치 수 toouse id를 도난 당한 경우 공격자가 임을 나타냅니다를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-205">Unfamiliar locations can provide a strong indication that an attacker is able toouse a stolen identity.</span></span> <span data-ttu-id="4834e-206">가양성은 사용자가 이동하거나, 새 장치를 사용하거나, 새 VPN을 사용할 때 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-206">False-positives may occur when a user is traveling, is trying out a new device, or is using a new VPN.</span></span> <span data-ttu-id="4834e-207">이 종류의 이벤트에 대 한 hello 위험 수준을 이러한 가양성 결과로 **보통**합니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-207">As a result of these false positives, hello risk level for this event type is **Medium**.</span></span>

### <a name="sign-ins-from-infected-devices"></a><span data-ttu-id="4834e-208">감염된 장치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="4834e-208">Sign-ins from infected devices</span></span>

<span data-ttu-id="4834e-209">이 위험 이벤트는 사용자 장치가 아닌 IP 주소를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-209">This risk event identifies IP addresses, not user devices.</span></span> <span data-ttu-id="4834e-210">경우는 단일 IP 주소를 뒤에 여러 장치가 고 일부는에 의해 제어 bot 네트워크에서 다른 장치에서 로그인 트리거 내이 이벤트 불필요 하 게이 위험 이벤트를 분류 하기 위한 hello 이유 변수인으로 **낮은**합니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-210">If several devices are behind a single IP address, and only some are controlled by a bot network, sign-ins from other devices my trigger this event unnecessarily, which is hello reason for classifying this risk event as **Low**.</span></span>  

<span data-ttu-id="4834e-211">Hello 사용자에 게 문의 한 모든 hello 사용자의 장치를 검색 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-211">We recommend that you contact hello user and scan all hello user's devices.</span></span> <span data-ttu-id="4834e-212">사용자의 개인 장치에 감염 되었거나 hello에서 감염 된 장치에 사용 된 하 다른 사람 앞에서 설명한 것 처럼 동일한 IP 주소 hello 사용자로 수 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-212">It is also possible that a user's personal device is infected, or as mentioned earlier, that someone else was using an infected device from hello same IP address as hello user.</span></span> <span data-ttu-id="4834e-213">감염 된 장치는 바이러스 백신 소프트웨어에서 아직 확인 되지 않은 및 감염 hello 장치 toobecome를 일으킬 수 있는 잘못 된 사용자 습관으로 나타낼 수도 있습니다는 맬웨어에 감염 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-213">Infected devices are often infected by malware that have not yet been identified by anti-virus software, and may also indicate as bad user habits that may have caused hello device toobecome infected.</span></span>

<span data-ttu-id="4834e-214">방법에 대 한 자세한 내용은 tooaddress 맬웨어 감염 참조 hello [맬웨어 보호 센터](http://go.microsoft.com/fwlink/?linkid=335773&clcid=0x409)합니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-214">For more information about how tooaddress malware infections, see hello [Malware Protection Center](http://go.microsoft.com/fwlink/?linkid=335773&clcid=0x409).</span></span>


### <a name="sign-ins-from-ip-addresses-with-suspicious-activity"></a><span data-ttu-id="4834e-215">의심스러운 작업이 있는 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="4834e-215">Sign-ins from IP addresses with suspicious activity</span></span>

<span data-ttu-id="4834e-216">로그인 한 경우 이러한 실제로 의심으로 표시 된 IP 주소에서 사용자 tooverify hello를 문의 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-216">We recommend that you contact hello user tooverify if they actually signed in from an IP address that was marked as suspicious.</span></span> <span data-ttu-id="4834e-217">이 종류의 이벤트에 대 한 hello 위험 수준이 "**보통**" hello 뒤 여러 장치에 있을 수 있으므로 hello 의심 스러운 활동에 대 한 책임 수 있지만 일부의 동일한 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-217">hello risk level for this event type is “**Medium**” because several devices may be behind hello same IP address, while only some may be responsible for hello suspicious activity.</span></span> 


 
## <a name="next-steps"></a><span data-ttu-id="4834e-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4834e-218">Next steps</span></span>

<span data-ttu-id="4834e-219">위험 이벤트는 사용자 Azure AD id 보호 하기 위한 hello foundation입니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-219">Risk events are hello foundation for protecting your Azure AD's identities.</span></span> <span data-ttu-id="4834e-220">Azure AD는 현재 여섯 가지 위험 이벤트를 감지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-220">Azure AD can currently detect six risk events:</span></span> 


| <span data-ttu-id="4834e-221">위험 이벤트 유형</span><span class="sxs-lookup"><span data-stu-id="4834e-221">Risk Event Type</span></span> | <span data-ttu-id="4834e-222">위험 수준</span><span class="sxs-lookup"><span data-stu-id="4834e-222">Risk Level</span></span> | <span data-ttu-id="4834e-223">검색 유형</span><span class="sxs-lookup"><span data-stu-id="4834e-223">Detection Type</span></span> |
| :-- | --- | --- |
| [<span data-ttu-id="4834e-224">자격 증명이 손실된 사용자</span><span class="sxs-lookup"><span data-stu-id="4834e-224">Users with leaked credentials</span></span>](#leaked-credentials) | <span data-ttu-id="4834e-225">높음</span><span class="sxs-lookup"><span data-stu-id="4834e-225">High</span></span> | <span data-ttu-id="4834e-226">오프라인</span><span class="sxs-lookup"><span data-stu-id="4834e-226">Offline</span></span> |
| [<span data-ttu-id="4834e-227">익명 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="4834e-227">Sign-ins from anonymous IP addresses</span></span>](#sign-ins-from-anonymous-ip-addresses) | <span data-ttu-id="4834e-228">중간</span><span class="sxs-lookup"><span data-stu-id="4834e-228">Medium</span></span> | <span data-ttu-id="4834e-229">실시간</span><span class="sxs-lookup"><span data-stu-id="4834e-229">Real-time</span></span> |
| [<span data-ttu-id="4834e-230">이동 불가능 tooatypical 위치</span><span class="sxs-lookup"><span data-stu-id="4834e-230">Impossible travel tooatypical locations</span></span>](#impossible-travel-to-atypical-locations) | <span data-ttu-id="4834e-231">중간</span><span class="sxs-lookup"><span data-stu-id="4834e-231">Medium</span></span> | <span data-ttu-id="4834e-232">오프라인</span><span class="sxs-lookup"><span data-stu-id="4834e-232">Offline</span></span> |
| [<span data-ttu-id="4834e-233">알 수 없는 위치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="4834e-233">Sign-ins from unfamiliar locations</span></span>](#sign-in-from-unfamiliar-locations) | <span data-ttu-id="4834e-234">중간</span><span class="sxs-lookup"><span data-stu-id="4834e-234">Medium</span></span> | <span data-ttu-id="4834e-235">실시간</span><span class="sxs-lookup"><span data-stu-id="4834e-235">Real-time</span></span> |
| [<span data-ttu-id="4834e-236">감염된 장치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="4834e-236">Sign-ins from infected devices</span></span>](#sign-ins-from-infected-devices) | <span data-ttu-id="4834e-237">낮음</span><span class="sxs-lookup"><span data-stu-id="4834e-237">Low</span></span> | <span data-ttu-id="4834e-238">오프라인</span><span class="sxs-lookup"><span data-stu-id="4834e-238">Offline</span></span> |
| [<span data-ttu-id="4834e-239">의심스러운 작업이 있는 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="4834e-239">Sign-ins from IP addresses with suspicious activity</span></span>](#sign-ins-from-ip-addresses-with-suspicious-activity) | <span data-ttu-id="4834e-240">중간</span><span class="sxs-lookup"><span data-stu-id="4834e-240">Medium</span></span> | <span data-ttu-id="4834e-241">오프라인</span><span class="sxs-lookup"><span data-stu-id="4834e-241">Offline</span></span>|

<span data-ttu-id="4834e-242">사용자는 어디 hello 사용자 환경에서 검색 된 위험 이벤트?</span><span class="sxs-lookup"><span data-stu-id="4834e-242">Where can you find hello risk events that have been detected in your environment?</span></span>
<span data-ttu-id="4834e-243">두 곳에서 보고된 위험 이벤트를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-243">There are two places where you review reported risk events:</span></span>

 - <span data-ttu-id="4834e-244">**Azure AD 보고** - 위험 이벤트는 Azure AD의 보안 보고서의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-244">**Azure AD reporting** - Risk events are part of Azure AD's security reports.</span></span> <span data-ttu-id="4834e-245">자세한 내용은 참조 hello [위험 보안 보고서에 사용자가](active-directory-reporting-security-user-at-risk.md) hello 및 [위험한 로그인 보안 보고서](active-directory-reporting-security-risky-sign-ins.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-245">For more details, see hello [users at risk security report](active-directory-reporting-security-user-at-risk.md) and hello [risky sign-ins security report](active-directory-reporting-security-risky-sign-ins.md).</span></span>

 - <span data-ttu-id="4834e-246">**Azure AD ID 보호** - 위험 이벤트는 [Azure Active Directory ID 보호](active-directory-identityprotection.md) 보고 기능의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-246">**Azure AD Identity Protection** - Risk events are also part of [Azure Active Directory Identity Protection's](active-directory-identityprotection.md) reporting capabilities.</span></span>
    

<span data-ttu-id="4834e-247">Hello 검색 하는 위험 이벤트 이미 id를 보호 하는 중요 한 측면을 나타내는 동안 hello 옵션 tooeither를 수동으로 해결할 또는 조건부 액세스 정책을 구성 하 여 자동화 된 응답을 구현할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4834e-247">While hello detection of risk events already represents an important aspect of protecting your identities, you also have hello option tooeither manually address them or even implement automated responses by configuring conditional access policies.</span></span> <span data-ttu-id="4834e-248">자세한 내용은 [Azure Active Directory ID 보호](active-directory-identityprotection.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4834e-248">For more details, see of [Azure Active Directory Identity Protection's](active-directory-identityprotection.md).</span></span>
 
