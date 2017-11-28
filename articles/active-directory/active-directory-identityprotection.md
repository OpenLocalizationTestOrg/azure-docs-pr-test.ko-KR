---
title: "Active Directory Id 보호 aaaAzure | Microsoft Docs"
description: "Azure AD Identity Protection을 통해 방법을 공격자가 tooexploit 노출된 된 id의 toolimit hello 능력 또는 장치와 toosecure id 또는 장치 의심 되는 또는 알려진 toobe를 이전에 손상에 대해 알아봅니다."
services: active-directory
keywords: "Azure Active Directory ID 보호, 클라우드 앱 검색, 응용 프로그램 관리, 보안, 위험, 위험 수준, 취약점, 보안 정책"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ecca4f3cdb65585687cf44a80024f26c7cab22ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection"></a><span data-ttu-id="10e3d-104">Azure Active Directory ID 보호</span><span class="sxs-lookup"><span data-stu-id="10e3d-104">Azure Active Directory Identity Protection</span></span>

<span data-ttu-id="10e3d-105">Azure Active Directory Id 보호는 수 있도록 Azure AD Premium P2 hello 버전의 기능:</span><span class="sxs-lookup"><span data-stu-id="10e3d-105">Azure Active Directory Identity Protection is a feature of hello Azure AD Premium P2 edition that enables you to:</span></span>

- <span data-ttu-id="10e3d-106">조직의 ID에 영향을 미치는 잠재적인 취약점을 검색</span><span class="sxs-lookup"><span data-stu-id="10e3d-106">Detect potential vulnerabilities affecting your organization’s identities</span></span>

- <span data-ttu-id="10e3d-107">자동화 된 응답이 toodetected 의심 스러운 동작을 관련된 tooyour 조직의 identities 구성</span><span class="sxs-lookup"><span data-stu-id="10e3d-107">Configure automated responses toodetected suspicious actions that are related tooyour organization’s identities</span></span>  

- <span data-ttu-id="10e3d-108">의심 스러운 문제를 조사 하 고 적절 한 조치 tooresolve 수행을</span><span class="sxs-lookup"><span data-stu-id="10e3d-108">Investigate suspicious incidents and take appropriate action tooresolve them</span></span>   


## <a name="getting-started"></a><span data-ttu-id="10e3d-109">시작</span><span class="sxs-lookup"><span data-stu-id="10e3d-109">Getting started</span></span>

<span data-ttu-id="10e3d-110">Microsoft는 10년 넘게 클라우드 기반 ID를 보호하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-110">Microsoft secures cloud-based identities for more than a decade.</span></span> <span data-ttu-id="10e3d-111">Azure Active Directory Id 보호 사용자 환경에서 사용할 수 있습니다 hello 동일한 보호 시스템 Microsoft toosecure identities를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-111">With Azure Active Directory Identity Protection, in your environment, you can use hello same protection systems Microsoft uses toosecure identities.</span></span>

<span data-ttu-id="10e3d-112">공격자는 사용자의 id를 도용 하 여 액세스 tooan 환경 수 hello 포함 된 대부분의 보안 위반 걸릴 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-112">hello vast majority of security breaches take place when attackers gain access tooan environment by stealing a user’s identity.</span></span> <span data-ttu-id="10e3d-113">Hello 년간 공격자가 되 고 제 3 자 위반을 활용 하 고 정교한 피싱 공격을 사용 하는 효과적인 점점 더 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-113">Over hello years, attackers have become increasingly effective in leveraging third party breaches and using sophisticated phishing attacks.</span></span> <span data-ttu-id="10e3d-114">공격자 액세스 tooeven 낮은 권한이 가진된 사용자 계정에는 즉시 해당 측면 확대를 통해 toogain tooimportant 회사 리소스에 액세스에 대 한 비교적 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-114">As soon as an attacker gains access tooeven low privileged user accounts, it is relatively easy for them toogain access tooimportant company resources through lateral movement.</span></span>

<span data-ttu-id="10e3d-115">이에 따라 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-115">As a consequence of this, you need to:</span></span>

- <span data-ttu-id="10e3d-116">해당 권한 수준에 관계 없이 모든 ID 보호</span><span class="sxs-lookup"><span data-stu-id="10e3d-116">Protect all identities regardless of their privilege level</span></span>

- <span data-ttu-id="10e3d-117">손상된 ID가 남용되지 않도록 사전에 방지</span><span class="sxs-lookup"><span data-stu-id="10e3d-117">Proactively prevent compromised identities from being abused</span></span>

<span data-ttu-id="10e3d-118">손상된 ID를 검색하는 것은 쉬운 작업이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-118">Discovering compromised identities is no easy task.</span></span> <span data-ttu-id="10e3d-119">적응 기계 학습 알고리즘을 사용 하 여 azure Active Directory 및 추론 toodetect 비정상 보고서 및 잠재적으로 나타내는 의심 스러운 인시던트 손상 identities 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-119">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect anomalies and suspicious incidents that indicate potentially compromised identities.</span></span> <span data-ttu-id="10e3d-120">이 데이터를 사용 하 여 Id 보호는 보고서를 생성 tooevaluate hello를 사용할 수 있는 경고 문제를 발견 했습니다 및 적절 한 완화 또는 재구성 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-120">Using this data, Identity Protection generates reports and alerts that enable you tooevaluate hello detected issues and take appropriate mitigation or remediation actions.</span></span>

<span data-ttu-id="10e3d-121">Azure Active Directory ID 보호는 모니터링 및 보고 도구 이상입니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-121">Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span></span> <span data-ttu-id="10e3d-122">tooprotect 조직의 id를 지정 된 위험 수준에 도달 했을 때 toodetected 문제를 자동으로 응답 하는 위험 기반 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-122">tooprotect your organization's identities, you can configure risk-based policies that automatically respond toodetected issues when a specified risk level has been reached.</span></span> <span data-ttu-id="10e3d-123">이러한 정책에서는 또한 tooother 조건부 Azure Active Directory 및 EMS에서 제공 하는 컨트롤에 액세스할 자동으로 차단 하거나 암호 재설정 및 다단계 인증 적용을 포함 한 적응 업데이트 관리 작업을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-123">These policies, in addition tooother conditional access controls provided by Azure Active Directory and EMS, can either automatically block or initiate adaptive remediation actions including password resets and multi-factor authentication enforcement.</span></span>


#### <a name="identity-protection-capabilities"></a><span data-ttu-id="10e3d-124">ID 보호 기능</span><span class="sxs-lookup"><span data-stu-id="10e3d-124">Identity Protection capabilities</span></span>

<span data-ttu-id="10e3d-125">**취약점 및 위험 계정 검색:**</span><span class="sxs-lookup"><span data-stu-id="10e3d-125">**Detecting vulnerabilities and risky accounts:**</span></span>  

* <span data-ttu-id="10e3d-126">사용자 지정 권장 사항을 tooimprove 제공 취약점을 강조 표시 하 여 전반적인 보안 상태</span><span class="sxs-lookup"><span data-stu-id="10e3d-126">Providing custom recommendations tooimprove overall security posture by highlighting vulnerabilities</span></span>
* <span data-ttu-id="10e3d-127">로그인 위험 수준 계산</span><span class="sxs-lookup"><span data-stu-id="10e3d-127">Calculating sign-in risk levels</span></span>
* <span data-ttu-id="10e3d-128">사용자 위험 수준 계산</span><span class="sxs-lookup"><span data-stu-id="10e3d-128">Calculating user risk levels</span></span>


<span data-ttu-id="10e3d-129">**위험 이벤트 조사:**</span><span class="sxs-lookup"><span data-stu-id="10e3d-129">**Investigating risk events:**</span></span>

* <span data-ttu-id="10e3d-130">위험 이벤트에 대한 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="10e3d-130">Sending notifications for risk events</span></span>
* <span data-ttu-id="10e3d-131">관련된 컨텍스트 정보를 사용하여 위험 이벤트 조사</span><span class="sxs-lookup"><span data-stu-id="10e3d-131">Investigating risk events using relevant and contextual information</span></span>
* <span data-ttu-id="10e3d-132">Tootrack 조사 기본 워크플로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-132">Providing basic workflows tootrack investigations</span></span>
* <span data-ttu-id="10e3d-133">쉽게 액세스할 수 tooremediation 암호 다시 설정 하는 등의 작업</span><span class="sxs-lookup"><span data-stu-id="10e3d-133">Providing easy access tooremediation actions such as password reset</span></span>

<span data-ttu-id="10e3d-134">**위험 기준 조건부 액세스 정책:**</span><span class="sxs-lookup"><span data-stu-id="10e3d-134">**Risk-based conditional access policies:**</span></span>

* <span data-ttu-id="10e3d-135">정책 toomitigate 위험한 로그인 하 여 로그인을 차단 하거나 다단계 인증 챌린지를 요구 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-135">Policy toomitigate risky sign-ins by blocking sign-ins or requiring multi-factor authentication challenges.</span></span>
* <span data-ttu-id="10e3d-136">정책 tooblock 또는 보안 위험 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="10e3d-136">Policy tooblock or secure risky user accounts</span></span>
* <span data-ttu-id="10e3d-137">Multi-factor authentication에 대해 정책 toorequire 사용자 tooregister</span><span class="sxs-lookup"><span data-stu-id="10e3d-137">Policy toorequire users tooregister for multi-factor authentication</span></span>



## <a name="identity-protection-roles"></a><span data-ttu-id="10e3d-138">ID 보호 역할</span><span class="sxs-lookup"><span data-stu-id="10e3d-138">Identity Protection roles</span></span>

<span data-ttu-id="10e3d-139">tooload 균형 hello 관리 활동 Id 보호 구현 주위 몇 가지 역할을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-139">tooload balance hello management activities around your Identity Protection implementation, you can assign several roles.</span></span> <span data-ttu-id="10e3d-140">Azure AD ID 보호는 3가지 디렉터리 역할을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-140">Azure AD Identity Protection supports 3 directory roles:</span></span>

| <span data-ttu-id="10e3d-141">역할</span><span class="sxs-lookup"><span data-stu-id="10e3d-141">Role</span></span>                         | <span data-ttu-id="10e3d-142">가능한 작업</span><span class="sxs-lookup"><span data-stu-id="10e3d-142">Can do</span></span>                          | <span data-ttu-id="10e3d-143">불가능한 작업</span><span class="sxs-lookup"><span data-stu-id="10e3d-143">Cannot do</span></span>
| :--                          | ---                                |  ---   |
| <span data-ttu-id="10e3d-144">전역 관리자</span><span class="sxs-lookup"><span data-stu-id="10e3d-144">Global administrator</span></span>         | <span data-ttu-id="10e3d-145">전체 액세스 tooIdentity 보호, 등록 Id 보호</span><span class="sxs-lookup"><span data-stu-id="10e3d-145">Full access tooIdentity Protection, Onboard Identity Protection</span></span>| |
| <span data-ttu-id="10e3d-146">보안 관리자</span><span class="sxs-lookup"><span data-stu-id="10e3d-146">Security administrator</span></span>       | <span data-ttu-id="10e3d-147">전체 액세스 tooIdentity 보호</span><span class="sxs-lookup"><span data-stu-id="10e3d-147">Full access tooIdentity Protection</span></span> | <span data-ttu-id="10e3d-148">ID 보호 등록, 사용자의 암호 재설정</span><span class="sxs-lookup"><span data-stu-id="10e3d-148">Onboard Identity Protection,  reset passwords for a user</span></span> |
| <span data-ttu-id="10e3d-149">보안 판독기</span><span class="sxs-lookup"><span data-stu-id="10e3d-149">Security reader</span></span>              | <span data-ttu-id="10e3d-150">읽기 전용 액세스 tooIdentity 보호</span><span class="sxs-lookup"><span data-stu-id="10e3d-150">Ready-only access tooIdentity Protection</span></span> | <span data-ttu-id="10e3d-151">ID 보호 등록, 사용자 수정, 정책 구성, 암호 재설정</span><span class="sxs-lookup"><span data-stu-id="10e3d-151">Onboard Identity Protection, remidiate users, configure policies,  reset passwords</span></span> |




<span data-ttu-id="10e3d-152">자세한 내용은 [Azure Active Directory에서 관리자 역할 할당](active-directory-assign-admin-roles-azure-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="10e3d-152">For more details, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span></span>



## <a name="detection"></a><span data-ttu-id="10e3d-153">감지</span><span class="sxs-lookup"><span data-stu-id="10e3d-153">Detection</span></span>

### <a name="vulnerabilities"></a><span data-ttu-id="10e3d-154">취약점</span><span class="sxs-lookup"><span data-stu-id="10e3d-154">Vulnerabilities</span></span>

<span data-ttu-id="10e3d-155">Azure Active Directory ID 보호는 구성을 분석하고 사용자의 ID에 영향을 줄 수 있는 취약점을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-155">Azure Active Directory Identity Protection analyses your configuration and detects vulnerabilities that can have an impact on your user's identities.</span></span> <span data-ttu-id="10e3d-156">자세한 내용은 [Azure Active Directory ID 보호에서 검색되는 취약성](active-directory-identityprotection-vulnerabilities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="10e3d-156">For more details, see [Vulnerabilities detected by Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span></span>

### <a name="risk-events"></a><span data-ttu-id="10e3d-157">위험 이벤트</span><span class="sxs-lookup"><span data-stu-id="10e3d-157">Risk events</span></span>

<span data-ttu-id="10e3d-158">Azure Active Directory 적응 컴퓨터 학습 알고리즘 및 추론 toodetect 의심 스러운 동작을 관련된 tooyour 사용자 id를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-158">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect suspicious actions that are related tooyour user's identities.</span></span> <span data-ttu-id="10e3d-159">hello 시스템이 각 검색 된 의심 스러운 동작에 대 한 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-159">hello system creates a record for each detected suspicious action.</span></span> <span data-ttu-id="10e3d-160">이러한 레코드를 위험 이벤트라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-160">These records are also known as risk events.</span></span>  
<span data-ttu-id="10e3d-161">자세한 내용은 [Azure Active Directory 위험 이벤트](active-directory-identity-protection-risk-events.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="10e3d-161">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>


## <a name="investigation"></a><span data-ttu-id="10e3d-162">조사</span><span class="sxs-lookup"><span data-stu-id="10e3d-162">Investigation</span></span>
<span data-ttu-id="10e3d-163">일반적으로 시간이 되 셨 Id 보호 hello Identity Protection 대시보드 붙습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-163">Your journey through Identity Protection typically starts with hello Identity Protection dashboard.</span></span>

<span data-ttu-id="10e3d-164">![수정](./media/active-directory-identityprotection/1000.png "수정")</span><span class="sxs-lookup"><span data-stu-id="10e3d-164">![Remediation](./media/active-directory-identityprotection/1000.png "Remediation")</span></span>

<span data-ttu-id="10e3d-165">hello 대시보드에 액세스할을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-165">hello dashboard gives you access to:</span></span>

* <span data-ttu-id="10e3d-166">**위험 플래그가 지정된 사용자**, **위험 이벤트** 및 **취약성**과 같은 보고서</span><span class="sxs-lookup"><span data-stu-id="10e3d-166">Reports such as **Users flagged for risk**, **Risk events** and **Vulnerabilities**</span></span>
* <span data-ttu-id="10e3d-167">설정의 hello 구성 예: 프로그램 **보안 정책**, **알림** 및 **다단계 인증 등록**</span><span class="sxs-lookup"><span data-stu-id="10e3d-167">Settings such as hello configuration of your **Security Policies**, **Notifications** and **multi-factor authentication registration**</span></span>

<span data-ttu-id="10e3d-168">일반적으로 조사는 hello 프로세스 hello 활동, 로그 및 관련된 tooa 위험 이벤트 toodecide 업데이트 관리 또는 완화 단계는 필요 여부는 기타 관련 정보를 검토 하 고, hello identity 어 떠 시작 합니다. hello identity를 노출 하는 방법을 이해 하 고 손상 되 면 사용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-168">It is typically your starting point for investigation, which is hello process of reviewing hello activities, logs, and other relevant information related tooa risk event toodecide whether remediation or mitigation steps are necessary,  and how hello identity was compromised, and understand how hello compromised identity was used.</span></span>

<span data-ttu-id="10e3d-169">조사 활동 toohello에 연결할 수 있습니다 [알림](active-directory-identityprotection-notifications.md) 전자 메일 당 전송 되는 Azure Active Directory 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-169">You can tie your investigation activities toohello [notifications](active-directory-identityprotection-notifications.md) Azure Active Directory Protection sends per email.</span></span>

<span data-ttu-id="10e3d-170">hello 다음 섹션에서는 제공 자세한 내용 및 관련된 tooan 조사 중인 hello 단계.</span><span class="sxs-lookup"><span data-stu-id="10e3d-170">hello following sections provide you with more details and hello steps that are related tooan investigation.</span></span>  


## <a name="risky-sign-ins"></a><span data-ttu-id="10e3d-171">위험한 로그인</span><span class="sxs-lookup"><span data-stu-id="10e3d-171">Risky sign-ins</span></span>

<span data-ttu-id="10e3d-172">Azure Active Directory는 [위험 이벤트 유형](active-directory-reporting-risk-events.md#risk-event-types)을 실시간 및 오프라인으로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-172">Azure Active Directory detects [risk event types](active-directory-reporting-risk-events.md#risk-event-types) in real-time and offline.</span></span> <span data-ttu-id="10e3d-173">사용자의 로그인 기능에 대해 검색 된 각 위험 이벤트 위험한 로그인 라는 tooa 논리적 개념을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-173">Each risk event that has been detected for a sign-in of a user contributes tooa logical concept called risky sign-in.</span></span> <span data-ttu-id="10e3d-174">위험한 로그인이 없습니다 수행 되었을 수도 사용자 계정의 hello 정당한 소유자가 로그인 시도에 대 한 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-174">A risky sign-in is an indicator for a sign-in attempt that might not have been performed by hello legitimate owner of a user account.</span></span>


### <a name="sign-in-risk-level"></a><span data-ttu-id="10e3d-175">로그인 위험 수준</span><span class="sxs-lookup"><span data-stu-id="10e3d-175">Sign-in risk level</span></span>

<span data-ttu-id="10e3d-176">로그인 위험 수준을 나타냅니다 (높음, 중간 또는 낮음) hello 가능성의 로그인 시도 하는 사용자 계정의 hello 합법적인 소유자에 의해 수행 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-176">A sign-in risk level is an indication (High, Medium, or Low) of hello likelihood that a sign-in attempt was not performed by hello legitimate owner of a user account.</span></span>

### <a name="mitigating-sign-in-risk-events"></a><span data-ttu-id="10e3d-177">로그인 위험 이벤트 완화</span><span class="sxs-lookup"><span data-stu-id="10e3d-177">Mitigating sign-in risk events</span></span>

<span data-ttu-id="10e3d-178">완화는 hello id 또는 장치 tooa 안전 상태를 복원 하지 않고 장치나 공격자가 tooexploit 노출된 된 id의 작업 toolimit hello 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-178">A mitigation is an action toolimit hello ability of an attacker tooexploit a compromised identity or device without restoring hello identity or device tooa safe state.</span></span> <span data-ttu-id="10e3d-179">한 완화 수단 hello id 또는 장치와 관련 된 이전 로그인 위험 이벤트 확인 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-179">A mitigation does not resolve previous sign-in risk events associated with hello identity or device.</span></span>

<span data-ttu-id="10e3d-180">toomitigate 위험한 로그인 로그인 위험 보안 policicies 자동으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-180">toomitigate risky sign-ins automatically, you can configure sign-in risk security policicies.</span></span> <span data-ttu-id="10e3d-181">Hello 사용자 또는 로그인 tooblock hello의 hello 위험 수준을 로그인 위험한 고려 하거나 hello 사용자 tooperform multi-factor authentication 요구 이러한 정책을 사용 하 여, 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-181">Using these policies, you consider hello risk level of hello user or hello sign-in tooblock risky sign-ins or require hello user tooperform multi-factor authentication.</span></span> <span data-ttu-id="10e3d-182">이러한 작업 하면 공격자가 도난된 identity toocause 손상 악용 하지 않을 수 있으며 시간 toosecure hello id를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-182">These actions may prevent an attacker from exploiting a stolen identity toocause damage, and may give you some time toosecure hello identity.</span></span>

### <a name="sign-in-risk-security-policy"></a><span data-ttu-id="10e3d-183">로그인 위험 보안 정책</span><span class="sxs-lookup"><span data-stu-id="10e3d-183">Sign-in risk security policy</span></span>
<span data-ttu-id="10e3d-184">로그인 위험 정책은 hello 위험 tooa 특정 로그인 평가 하 고 미리 정의 된 조건 및 규칙에 따라 완화 기능이 적용 되는 조건부 액세스 정책이입니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-184">A sign-in risk policy is a conditional access policy that evaluates hello risk tooa specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

<span data-ttu-id="10e3d-185">![로그인 위험 정책](./media/active-directory-identityprotection/1014.png "로그인 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="10e3d-185">![Sign-in risk policy](./media/active-directory-identityprotection/1014.png "Sign-in risk policy")</span></span>

<span data-ttu-id="10e3d-186">Azure AD Identity Protection 위험한 로그인의 hello 완화 하 여 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-186">Azure AD Identity Protection helps you manage hello mitigation of risky sign-ins by enabling you to:</span></span>

* <span data-ttu-id="10e3d-187">Hello 사용자 및 그룹 hello 정책 설정에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-187">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="10e3d-188">![로그인 위험 정책](./media/active-directory-identityprotection/1015.png "로그인 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="10e3d-188">![Sign-in risk policy](./media/active-directory-identityprotection/1015.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="10e3d-189">Hello 로그인 위험 수준 임계값 (낮음, 보통 또는 높음) hello 정책 트리거하는 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-189">Set hello sign-in risk level threshold (low, medium, or high) that triggers hello policy:</span></span>

    <span data-ttu-id="10e3d-190">![로그인 위험 정책](./media/active-directory-identityprotection/1016.png "로그인 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="10e3d-190">![Sign-in risk policy](./media/active-directory-identityprotection/1016.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="10e3d-191">집합 hello 컨트롤 toobe hello 정책을 트리거하면 적용:</span><span class="sxs-lookup"><span data-stu-id="10e3d-191">Set hello controls toobe enforced when hello policy triggers:</span></span>  

    <span data-ttu-id="10e3d-192">![로그인 위험 정책](./media/active-directory-identityprotection/1017.png "로그인 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="10e3d-192">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="10e3d-193">정책 hello 상태 전환:</span><span class="sxs-lookup"><span data-stu-id="10e3d-193">Switch hello state of your policy:</span></span>

    <span data-ttu-id="10e3d-194">![MFA 등록](./media/active-directory-identityprotection/403.png "MFA 등록")</span><span class="sxs-lookup"><span data-stu-id="10e3d-194">![MFA Registration](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="10e3d-195">검토 하 고 변경 하기를 활성화 하기 전에 hello 영향을 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-195">Review and evaluate hello impact of a change before activating it:</span></span>

    <span data-ttu-id="10e3d-196">![로그인 위험 정책](./media/active-directory-identityprotection/1018.png "로그인 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="10e3d-196">![Sign-in risk policy](./media/active-directory-identityprotection/1018.png "Sign-in risk policy")</span></span>

#### <a name="what-you-need-tooknow"></a><span data-ttu-id="10e3d-197">필요한 tooknow</span><span class="sxs-lookup"><span data-stu-id="10e3d-197">What you need tooknow</span></span>
<span data-ttu-id="10e3d-198">로그인 위험 보안 정책 toorequire multi-factor authentication을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-198">You can configure a sign-in risk security policy toorequire multi-factor authentication:</span></span>

<span data-ttu-id="10e3d-199">![로그인 위험 정책](./media/active-directory-identityprotection/1017.png "로그인 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="10e3d-199">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>

<span data-ttu-id="10e3d-200">그러나 보안상의 이유로 이 설정은 다단계 인증에 이미 등록된 사용자에게만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-200">However, for security reasons, this setting only works for users that have already been registered for multi-factor authentication.</span></span> <span data-ttu-id="10e3d-201">Hello 조건 toorequire multi-factor authentication 사용자에 게 multi-factor authentication에 아직 등록 되지 않았습니다 충족 하는 hello 사용자가 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-201">If hello condition toorequire multi-factor authentication is satisfied for a user who is not yet registered for multi-factor authentication, hello user is blocked.</span></span>

<span data-ttu-id="10e3d-202">모범 사례로, 로그인을 위한 위험한, toorequire 다단계 인증을 사용 하려는 경우 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-202">As a best practice, if you want toorequire multi-factor authentication for risky sign-ins, you should:</span></span>

1. <span data-ttu-id="10e3d-203">Hello를 사용 하도록 설정 [다단계 인증 등록 정책](#multi-factor-authentication-registration-policy) hello에 대 한 영향을 받는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-203">Enable hello [multi-factor authentication registration policy](#multi-factor-authentication-registration-policy) for hello affected users.</span></span>
2. <span data-ttu-id="10e3d-204">Hello 영향을 받는 사용자 toologin 위험한 비 세션 tooperform에 MFA 등록 필요</span><span class="sxs-lookup"><span data-stu-id="10e3d-204">Require hello affected users toologin in a non-risky session tooperform a MFA registration</span></span>

<span data-ttu-id="10e3d-205">이러한 단계를 완료하면 위험한 로그인에 대해 다단계 인증이 요구됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-205">Completing these steps ensures that multi-factor authentication is required for a risky sign-in.</span></span>

#### <a name="best-practices"></a><span data-ttu-id="10e3d-206">모범 사례</span><span class="sxs-lookup"><span data-stu-id="10e3d-206">Best practices</span></span>
<span data-ttu-id="10e3d-207">선택는 **높은** 임계값 정책이 트리거되고 hello 영향 toousers 최소화 횟수 hello 수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-207">Choosing a **High** threshold reduces hello number of times a policy is triggered and minimizes hello impact toousers.</span></span>  

<span data-ttu-id="10e3d-208">그러나이 메서드를 제외 **낮은** 및 **보통** 공격자가 악용 노출된 된 id를 차단할 수 있는 hello 정책에서 위험에 대 한 플래그가 지정 된 로그인.</span><span class="sxs-lookup"><span data-stu-id="10e3d-208">However, it excludes **Low** and **Medium** sign-ins flagged for risk from hello policy, which may not block an attacker from exploiting a compromised identity.</span></span>

<span data-ttu-id="10e3d-209">설정이 정책을 hello 하는 경우</span><span class="sxs-lookup"><span data-stu-id="10e3d-209">When setting hello policy,</span></span>

* <span data-ttu-id="10e3d-210">다단계 인증이 없는/있을 수 없는 사용자 제외</span><span class="sxs-lookup"><span data-stu-id="10e3d-210">Exclude users who do not/cannot have multi-factor authentication</span></span>
* <span data-ttu-id="10e3d-211">로캘에서 여기서 hello 정책 사용 불가능 한 사용자를 제외 (예를 들어 없는 액세스 toohelpdesk)</span><span class="sxs-lookup"><span data-stu-id="10e3d-211">Exclude users in locales where enabling hello policy is not practical (for example no access toohelpdesk)</span></span>
* <span data-ttu-id="10e3d-212">가능성이 높은 toogenerate 많이 거짓 긍정 (개발자, 보안 분석가) 인 사용자를 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-212">Exclude users who are likely toogenerate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="10e3d-213">초기 정책이 롤아웃하는 동안 또는 최종 사용자가 확인하는 과제를 최소화해야 하는 경우 **높음** 임계값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-213">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="10e3d-214">조직에서 보안을 강화해야 하는 경우 **낮음** 임계값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-214">Use a **Low**  threshold if your organization requires greater security.</span></span> <span data-ttu-id="10e3d-215">**낮은** 임계값을 선택하면 추가 사용자 로그인 과제가 발생하지만 보안이 강화됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-215">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="10e3d-216">기본 권장 대부분의 조직에 대 한 규칙 tooconfigure을는 hello는 **보통** 임계값 toostrike 보안과 유용성 간의 균형입니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-216">hello recommended default for most organizations is tooconfigure a rule for a **Medium** threshold toostrike a balance between usability and security.</span></span>

<span data-ttu-id="10e3d-217">hello 로그인 위험 정책은 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-217">hello sign-in risk policy is:</span></span>

* <span data-ttu-id="10e3d-218">적용 된 tooall 브라우저 트래픽과 최신 인증을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-218">Applied tooall browser traffic and sign-ins using modern authentication.</span></span>
* <span data-ttu-id="10e3d-219">ADFS와 같은 페더레이션 hello IDP에서 hello WS-트러스트 끝점을 사용 하지 않도록 설정 하 여 이전 보안 프로토콜을 사용 하 여 적용된 되지 않았습니다. tooapplications 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-219">Not applied tooapplications using older security protocols by disabling hello WS-Trust endpoint at hello federated IDP, such as ADFS.</span></span>

<span data-ttu-id="10e3d-220">hello **위험 이벤트** hello Id 보호 콘솔 페이지에서에서 모든 이벤트를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-220">hello **Risk Events** page in hello Identity Protection console lists all events:</span></span>

* <span data-ttu-id="10e3d-221">이 정책은 다음에 적용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-221">This policy was applied to</span></span>
* <span data-ttu-id="10e3d-222">Hello 활동을 검토 하 고 hello 작업이 적절 한 되었는지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-222">You can review hello activity and determine whether hello action was appropriate or not</span></span>

<span data-ttu-id="10e3d-223">사용자 환경 관련 hello에 대 한 개요를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-223">For an overview of hello related user experience, see:</span></span>

* [<span data-ttu-id="10e3d-224">위험한 로그인 복구</span><span class="sxs-lookup"><span data-stu-id="10e3d-224">Risky sign-in recovery</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [<span data-ttu-id="10e3d-225">위험한 로그인 차단됨</span><span class="sxs-lookup"><span data-stu-id="10e3d-225">Risky sign-in blocked</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [<span data-ttu-id="10e3d-226">Azure AD ID 보호를 사용하는 로그인 환경</span><span class="sxs-lookup"><span data-stu-id="10e3d-226">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)  

<span data-ttu-id="10e3d-227">**tooopen hello 관련된 구성 대화 상자**:</span><span class="sxs-lookup"><span data-stu-id="10e3d-227">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="10e3d-228">Hello에 **Azure AD Identity Protection** 블레이드 hello **구성** 섹션에서 클릭 **위험 정책을 로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-228">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **Sign-in risk policy**.</span></span>

    <span data-ttu-id="10e3d-229">![사용자 위험 정책](./media/active-directory-identityprotection/1014.png "사용자 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="10e3d-229">![User ridk policy](./media/active-directory-identityprotection/1014.png "User ridk policy")</span></span>



## <a name="users-flagged-for-risk"></a><span data-ttu-id="10e3d-230">위험에 대한 플래그가 지정된 사용자</span><span class="sxs-lookup"><span data-stu-id="10e3d-230">Users flagged for risk</span></span>

<span data-ttu-id="10e3d-231">모든 활성 [이벤트 위험](active-directory-identity-protection-risk-events.md) 사용자 기여 사용자 위험 라는 tooa 논리적 개념에 대 한 Azure Active Directory에서 검색 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-231">All active [risk events](active-directory-identity-protection-risk-events.md) that were detected by Azure Active Directory for a user contribute tooa logical concept called user risk.</span></span> <span data-ttu-id="10e3d-232">위험 플래그가 지정된 사용자는 손상되었을 수 있는 사용자 계정에 대한 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-232">A user flagged for risk is an indicator for a user account that might have been compromised.</span></span>

![위험에 대한 플래그가 지정된 사용자](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a><span data-ttu-id="10e3d-234">사용자 위험 수준</span><span class="sxs-lookup"><span data-stu-id="10e3d-234">User risk level</span></span>

<span data-ttu-id="10e3d-235">위험 수준의 사용자는 나타냅니다 (높음, 중간 또는 낮음) hello 유사도 hello 사용자의 id가 손상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-235">A user risk level is an indication (High, Medium, or Low) of hello likelihood that hello user’s identity has been compromised.</span></span> <span data-ttu-id="10e3d-236">사용자의 id와 연결 된 hello 사용자 위험 이벤트로 따라 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-236">It is calculated based on hello user risk events that are associated with a user's identity.</span></span>

<span data-ttu-id="10e3d-237">hello 상태 위험 이벤트는 **활성** 또는 **닫힘**합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-237">hello status of a risk event is either **Active** or **Closed**.</span></span> <span data-ttu-id="10e3d-238">만 있는 이벤트의 위험 **활성** 기여 toohello 사용자 위험 수준 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-238">Only risk events that are **Active** contribute toohello user risk level calculation.</span></span>

<span data-ttu-id="10e3d-239">hello 사용자 위험 수준은 입력 다음 hello를 사용 하 여 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-239">hello user risk level is calculated using hello following inputs:</span></span>

* <span data-ttu-id="10e3d-240">Hello 사용자 영향을 미치는 활성 위험 이벤트</span><span class="sxs-lookup"><span data-stu-id="10e3d-240">Active risk events impacting hello user</span></span>
* <span data-ttu-id="10e3d-241">이러한 이벤트의 위험 수준</span><span class="sxs-lookup"><span data-stu-id="10e3d-241">Risk level of these events</span></span>
* <span data-ttu-id="10e3d-242">수정 작업이 수행되었는지 여부</span><span class="sxs-lookup"><span data-stu-id="10e3d-242">Whether any remediation actions have been taken</span></span>

<span data-ttu-id="10e3d-243">![사용자 위험](./media/active-directory-identityprotection/1031.png "사용자 위험")</span><span class="sxs-lookup"><span data-stu-id="10e3d-243">![User risks](./media/active-directory-identityprotection/1031.png "User risks")</span></span>

<span data-ttu-id="10e3d-244">Hello 사용자 위험 수준 toocreate 조건부 액세스 정책의 위험한 사용자 로그인을 차단할 사용 하거나 강제로 할 수 있습니다 toosecurely가 암호를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-244">You can use hello user risk levels toocreate conditional access policies that block risky users from signing in, or force them toosecurely change their password.</span></span>

### <a name="closing-risk-events-manually"></a><span data-ttu-id="10e3d-245">수동으로 위험 이벤트 닫기</span><span class="sxs-lookup"><span data-stu-id="10e3d-245">Closing risk events manually</span></span>

<span data-ttu-id="10e3d-246">대부분의 경우 보안 암호를 재설정 tooautomatically 닫기 위험 이벤트와 같은 수정 작업을 맡은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-246">In most cases, you will take remediation actions such as a secure password reset tooautomatically close risk events.</span></span> <span data-ttu-id="10e3d-247">그러나 불가능할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-247">However, this might not always be possible.</span></span>  
<span data-ttu-id="10e3d-248">이 경우, 예를 들어 hello 경우:</span><span class="sxs-lookup"><span data-stu-id="10e3d-248">This is, for example, hello case, when:</span></span>

* <span data-ttu-id="10e3d-249">활성 위험 이벤트가 있는 사용자가 삭제된 경우</span><span class="sxs-lookup"><span data-stu-id="10e3d-249">A user with Active risk events has been deleted</span></span>
* <span data-ttu-id="10e3d-250">조사는 hello 합법적인 사용자가 보고 된 위험 상황을 수행 된 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-250">An investigation reveals that a reported risk event has been perform by hello legitimate user</span></span>

<span data-ttu-id="10e3d-251">위험 이벤트를는 **활성** toohello 사용자 위험 계산 참가, toomanually 위험 이벤트를 수동으로 닫고 위험 수준을 낮출 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-251">Because risk events that are **Active** contribute toohello user risk calculation, you may have toomanually lower a risk level by closing risk events manually.</span></span>  
<span data-ttu-id="10e3d-252">조사 hello 과정을 선택할 수 있습니다 tootake 위험 이벤트의 이러한 동작 toochange hello 상태 중 하나:</span><span class="sxs-lookup"><span data-stu-id="10e3d-252">During hello course of investigation, you can choose tootake any of these actions toochange hello status of a risk event:</span></span>

<span data-ttu-id="10e3d-253">![작업](./media/active-directory-identityprotection/34.png "작업")</span><span class="sxs-lookup"><span data-stu-id="10e3d-253">![Actions](./media/active-directory-identityprotection/34.png "Actions")</span></span>

* <span data-ttu-id="10e3d-254">**해결** -Identity Protection 외부 적절 한 업데이트 관리 작업을 수행한 위험 이벤트를 검토 하 고 해당 hello 위험 이벤트 고려할 닫힌 경우 "해결 됨"로 표시 hello 이벤트 판단 되는 경우.</span><span class="sxs-lookup"><span data-stu-id="10e3d-254">**Resolve** - If after investigating a risk event, you took an appropriate remediation action outside Identity Protection, and you believe that hello risk event should be considered closed, mark hello event as Resolved.</span></span> <span data-ttu-id="10e3d-255">확인할된 이벤트는 상태 tooClosed hello 위험 이벤트를 설정 하 고 hello 위험 이벤트 toouser 위험 주지 더 이상.</span><span class="sxs-lookup"><span data-stu-id="10e3d-255">Resolved events will set hello risk event’s status tooClosed and hello risk event will no longer contribute toouser risk.</span></span>
* <span data-ttu-id="10e3d-256">**가양성으로 표시** - 경우에 따라 위험 이벤트를 조사하여 플래그 지정이 위험으로 잘못 지정되었음을 발견할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-256">**Mark as false-positive** - In some cases, you may investigate a risk event and discover that it was incorrectly flagged as a risky.</span></span> <span data-ttu-id="10e3d-257">거짓 긍정으로 hello 위험 이벤트를 표시 하 여 hello 이러한 발생 수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-257">You can help reduce hello number of such occurrences by marking hello risk event as False-positive.</span></span> <span data-ttu-id="10e3d-258">이 hello 기계 hello 향후의 비슷한 이벤트가 알고리즘 tooimprove hello 분류 학습 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-258">This will help hello machine learning algorithms tooimprove hello classification of similar events in hello future.</span></span> <span data-ttu-id="10e3d-259">hello 거짓 긍정 이벤트 상태가 너무**닫힘** 및 toouser 위험을 더 이상 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-259">hello status of false-positive events is too**Closed** and they will no longer contribute toouser risk.</span></span>
* <span data-ttu-id="10e3d-260">**Ignore** -업데이트 관리 작업을 되지 않았을 hello 활성 목록에서 제거 하는 위험 이벤트 toobe hello, 무시 하는 위험 이벤트를 표시할 수 있습니다 및 hello 이벤트 상태 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-260">**Ignore** - If you have not taken any remediation action, but want hello risk event toobe removed from hello active list, you can mark a risk event Ignore and hello event status will be Closed.</span></span> <span data-ttu-id="10e3d-261">무시 이벤트 toouser 위험을 기여 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-261">Ignored events do not contribute toouser risk.</span></span> <span data-ttu-id="10e3d-262">이 옵션은 이례적인 상황에서만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-262">This option should only be used under unusual circumstances.</span></span>
* <span data-ttu-id="10e3d-263">**다시 활성화** -수동으로 종료 된 이벤트를 위험 (선택 하 여 **해결**, **거짓 긍정**, 또는 **무시**) 활성화할 수 hello 설정 이벤트 상태 너무 다시**활성**합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-263">**Reactivate** - Risk events that were manually closed (by choosing **Resolve**, **False positive**, or **Ignore**) can be reactivated, setting hello event status back too**Active**.</span></span> <span data-ttu-id="10e3d-264">다시 활성화 된 위험 이벤트 toohello 사용자 위험 수준 계산을 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-264">Reactivated risk events contribute toohello user risk level calculation.</span></span> <span data-ttu-id="10e3d-265">수정(예: 보안 암호를 다시 설정)을 통해 닫힌 위험 이벤트를 다시 활성화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-265">Risk events closed through remediation (such as a secure password reset) cannot be reactivated.</span></span>

<span data-ttu-id="10e3d-266">**tooopen hello 관련된 구성 대화 상자**:</span><span class="sxs-lookup"><span data-stu-id="10e3d-266">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="10e3d-267">Hello에 **Azure AD Identity Protection** 블레이드 아래 **조사**, 클릭 **이벤트 위험**합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-267">On hello **Azure AD Identity Protection** blade, under **Investigate**, click **Risk events**.</span></span>

    <span data-ttu-id="10e3d-268">![암호 수동 다시 설정](./media/active-directory-identityprotection/1002.png "암호 수동 다시 설정")</span><span class="sxs-lookup"><span data-stu-id="10e3d-268">![Manual password reset](./media/active-directory-identityprotection/1002.png "Manual password reset")</span></span>
2. <span data-ttu-id="10e3d-269">Hello에 **이벤트 위험** 목록에서 위험을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-269">In hello **Risk events** list, click a risk.</span></span>

    <span data-ttu-id="10e3d-270">![암호 수동 다시 설정](./media/active-directory-identityprotection/1003.png "암호 수동 다시 설정")</span><span class="sxs-lookup"><span data-stu-id="10e3d-270">![Manual password reset](./media/active-directory-identityprotection/1003.png "Manual password reset")</span></span>
3. <span data-ttu-id="10e3d-271">Hello 위험 블레이드에서 사용자를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-271">On hello risk blade, right-click a user.</span></span>

    <span data-ttu-id="10e3d-272">![암호 수동 다시 설정](./media/active-directory-identityprotection/1004.png "암호 수동 다시 설정")</span><span class="sxs-lookup"><span data-stu-id="10e3d-272">![Manual password reset](./media/active-directory-identityprotection/1004.png "Manual password reset")</span></span>

### <a name="closing-all-risk-events-for-a-user-manually"></a><span data-ttu-id="10e3d-273">사용자에 대한 모든 위험 이벤트를 수동으로 닫기</span><span class="sxs-lookup"><span data-stu-id="10e3d-273">Closing all risk events for a user manually</span></span>
<span data-ttu-id="10e3d-274">수동으로 사용자에 대 한 위험 이벤트를 개별적으로 종료, 하는 대신 Azure Active Directory Id 보호도 하면 메서드 tooclose 이벤트를 모두 한 번의 클릭으로 사용자에 대 한 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-274">Instead of manually closing risk events for a user individually, Azure Active Directory Identity Protection also provides you with a method tooclose all events for a user with one click.</span></span>

<span data-ttu-id="10e3d-275">![작업](./media/active-directory-identityprotection/2222.png "작업")</span><span class="sxs-lookup"><span data-stu-id="10e3d-275">![Actions](./media/active-directory-identityprotection/2222.png "Actions")</span></span>

<span data-ttu-id="10e3d-276">클릭할 때 **이벤트를 모두 해제**, 이벤트를 모두 닫혀 있고 hello 영향을 받는 사용자가 더 이상 위험에 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-276">When you click **Dismiss all events**, all events are closed and hello affected user is no longer at risk.</span></span>

### <a name="remediating-user-risk-events"></a><span data-ttu-id="10e3d-277">사용자 위험 이벤트 수정</span><span class="sxs-lookup"><span data-stu-id="10e3d-277">Remediating user risk events</span></span>

<span data-ttu-id="10e3d-278">업데이트 관리 작업은 id 또는 이전에 의심 하거나 toobe 알려진 장치를 손상 하는 작업 toosecure입니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-278">A remediation is an action toosecure an identity or a device that was previously suspected or known toobe compromised.</span></span> <span data-ttu-id="10e3d-279">수정 작업 hello id 또는 장치 tooa 안전 상태를 복원 하 고 hello id 또는 장치와 관련 된 이전 위험 이벤트를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-279">A remediation action restores hello identity or device tooa safe state, and resolves previous risk events associated with hello identity or device.</span></span>

<span data-ttu-id="10e3d-280">tooremediate 사용자 위험 이벤트를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-280">tooremediate user risk events, you can:</span></span>

* <span data-ttu-id="10e3d-281">보안 된 암호 재설정 tooremediate 사용자 위험 이벤트를 수동으로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-281">Perform a secure password reset tooremediate user risk events manually</span></span>
* <span data-ttu-id="10e3d-282">사용자 위험 보안 정책 toomitigate 구성 하거나 사용자 위험 이벤트를 자동으로 재구성</span><span class="sxs-lookup"><span data-stu-id="10e3d-282">Configure a user risk security policy toomitigate or remediate user risk events automatically</span></span>
* <span data-ttu-id="10e3d-283">Hello 감염 된 장치를 이미지로 다시 설치</span><span class="sxs-lookup"><span data-stu-id="10e3d-283">Re-image hello infected device</span></span>  

#### <a name="manual-secure-password-reset"></a><span data-ttu-id="10e3d-284">수동으로 안전한 암호 다시 설정</span><span class="sxs-lookup"><span data-stu-id="10e3d-284">Manual secure password reset</span></span>
<span data-ttu-id="10e3d-285">보안 암호를 재설정 많은 위험 이벤트에 대 한 효과적인 조치가 및 수행 되 면 자동으로 이러한 위험 이벤트를 닫고 hello 사용자 위험 수준 다시 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-285">A secure password reset is an effective remediation for many risk events, and when performed, automatically closes these risk events and recalculates hello user risk level.</span></span> <span data-ttu-id="10e3d-286">Hello Identity Protection 대시보드 tooinitiate 암호 재설정 위험한 사용자에 대해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-286">You can use hello Identity Protection dashboard tooinitiate a password reset for a risky user.</span></span>

<span data-ttu-id="10e3d-287">hello 관련된 대화 상자에서는 두 가지 방법이 tooreset 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-287">hello related dialog provides two different methods tooreset a password:</span></span>

<span data-ttu-id="10e3d-288">**암호 재설정** -선택 **hello 사용자 tooreset 자신의 암호를 요구** tooallow hello 사용자 tooself 복구 hello 사용자가 multi-factor authentication에 등록 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="10e3d-288">**Reset password** - Select **Require hello user tooreset their password** tooallow hello user tooself-recover if hello user has registered for multi-factor authentication.</span></span> <span data-ttu-id="10e3d-289">Hello 사용자의 다음에 로그인 하는 동안 hello 사용자는 multi-factor authentication 질문이 성공적으로 필요한 toosolve 및 다음, 강제 toochange hello 암호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-289">During hello user's next sign-in, hello user will be required toosolve a multi-factor authentication challenge successfully and then, forced toochange hello password.</span></span> <span data-ttu-id="10e3d-290">이 옵션 hello 사용자 계정이 등록 된 multi-factor authentication이 아닌 경우에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-290">This option isn't available if hello user account is not already registered multi-factor authentication.</span></span>

<span data-ttu-id="10e3d-291">**임시 암호** -선택 **임시 암호가 생성** tooimmediately hello 기존 암호를 무효화 하 고 hello 사용자에 대 한 새 임시 암호를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-291">**Temporary password** - Select **Generate a temporary password** tooimmediately invalidate hello existing password, and create a new temporary password for hello user.</span></span> <span data-ttu-id="10e3d-292">Hello 새 임시 암호 tooan 대체 전자 메일 주소를 hello 사용자나 toohello 사용자의 관리자에 대 한 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-292">Send hello new temporary password tooan alternate email address for hello user or toohello user's manager.</span></span> <span data-ttu-id="10e3d-293">Hello 암호 임시 이기 때문에 hello 사용자 로그인 시 증명된 toochange hello 암호가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-293">Because hello password is temporary, hello user will be prompted toochange hello password upon sign-in.</span></span>

<span data-ttu-id="10e3d-294">![정책](./media/active-directory-identityprotection/1005.png "정책")</span><span class="sxs-lookup"><span data-stu-id="10e3d-294">![Policy](./media/active-directory-identityprotection/1005.png "Policy")</span></span>

<span data-ttu-id="10e3d-295">**tooopen hello 관련된 구성 대화 상자**:</span><span class="sxs-lookup"><span data-stu-id="10e3d-295">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="10e3d-296">Hello에 **Azure AD Identity Protection** 블레이드에서 클릭 **위험에 대 한 플래그가 지정 된 사용자가**합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-296">On hello **Azure AD Identity Protection** blade, click **Users flagged for risk**.</span></span>

    <span data-ttu-id="10e3d-297">![암호 수동 다시 설정](./media/active-directory-identityprotection/1006.png "암호 수동 다시 설정")</span><span class="sxs-lookup"><span data-stu-id="10e3d-297">![Manual password reset](./media/active-directory-identityprotection/1006.png "Manual password reset")</span></span>
2. <span data-ttu-id="10e3d-298">사용자의 hello 목록에서 하나 이상의 위험 이벤트와 사용자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-298">From hello list of users, select a user with at least one risk events.</span></span>

    <span data-ttu-id="10e3d-299">![암호 수동 다시 설정](./media/active-directory-identityprotection/1007.png "암호 수동 다시 설정")</span><span class="sxs-lookup"><span data-stu-id="10e3d-299">![Manual password reset](./media/active-directory-identityprotection/1007.png "Manual password reset")</span></span>
3. <span data-ttu-id="10e3d-300">Hello 사용자 블레이드 클릭 **암호 재설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-300">On hello user blade, click **Reset password**.</span></span>

    <span data-ttu-id="10e3d-301">![암호 수동 다시 설정](./media/active-directory-identityprotection/1008.png "암호 수동 다시 설정")</span><span class="sxs-lookup"><span data-stu-id="10e3d-301">![Manual password reset](./media/active-directory-identityprotection/1008.png "Manual password reset")</span></span>

### <a name="user-risk-security-policy"></a><span data-ttu-id="10e3d-302">사용자 위험 보안 정책</span><span class="sxs-lookup"><span data-stu-id="10e3d-302">User risk security policy</span></span>
<span data-ttu-id="10e3d-303">사용자 위험 보안 정책은 hello 위험 수준 tooa 특정 사용자를 평가 하 고 미리 정의 된 조건 및 규칙에 따라 수정 및 완화 작업을 적용 하는 조건부 액세스 정책을입니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-303">A user risk security policy is a conditional access policy that evaluates hello risk level tooa specific user and applies remediation and mitigation actions based on predefined conditions and rules.</span></span>

<span data-ttu-id="10e3d-304">![사용자 위험 정책](./media/active-directory-identityprotection/1009.png "사용자 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="10e3d-304">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

<span data-ttu-id="10e3d-305">Azure AD Identity Protection hello 완화 및 수정 하 여 위험에 대 한 플래그가 지정 된 사용자를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-305">Azure AD Identity Protection helps you manage hello mitigation and remediation of users flagged for risk by enabling you to:</span></span>

* <span data-ttu-id="10e3d-306">Hello 사용자 및 그룹 hello 정책 설정에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-306">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="10e3d-307">![사용자 위험 정책](./media/active-directory-identityprotection/1010.png "사용자 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="10e3d-307">![User ridk policy](./media/active-directory-identityprotection/1010.png "User ridk policy")</span></span>
* <span data-ttu-id="10e3d-308">Hello 사용자 위험 수준 임계값 (낮음, 보통 또는 높음) hello 정책 트리거하는 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-308">Set hello user risk level threshold (low, medium, or high) that triggers hello policy:</span></span>

    <span data-ttu-id="10e3d-309">![사용자 위험 정책](./media/active-directory-identityprotection/1011.png "사용자 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="10e3d-309">![User ridk policy](./media/active-directory-identityprotection/1011.png "User ridk policy")</span></span>
* <span data-ttu-id="10e3d-310">집합 hello 컨트롤 toobe hello 정책을 트리거하면 적용:</span><span class="sxs-lookup"><span data-stu-id="10e3d-310">Set hello controls toobe enforced when hello policy triggers:</span></span>

    <span data-ttu-id="10e3d-311">![사용자 위험 정책](./media/active-directory-identityprotection/1012.png "사용자 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="10e3d-311">![User ridk policy](./media/active-directory-identityprotection/1012.png "User ridk policy")</span></span>
* <span data-ttu-id="10e3d-312">정책 hello 상태 전환:</span><span class="sxs-lookup"><span data-stu-id="10e3d-312">Switch hello state of your policy:</span></span>

    <span data-ttu-id="10e3d-313">![사용자 위험 정책](./media/active-directory-identityprotection/403.png "MFA 등록")</span><span class="sxs-lookup"><span data-stu-id="10e3d-313">![User ridk policy](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="10e3d-314">검토 하 고 변경 하기를 활성화 하기 전에 hello 영향을 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-314">Review and evaluate hello impact of a change before activating it:</span></span>

    <span data-ttu-id="10e3d-315">![사용자 위험 정책](./media/active-directory-identityprotection/1013.png "사용자 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="10e3d-315">![User ridk policy](./media/active-directory-identityprotection/1013.png "User ridk policy")</span></span>

<span data-ttu-id="10e3d-316">선택는 **높은** 임계값 정책이 트리거되고 hello 영향 toousers 최소화 횟수 hello 수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-316">Choosing a **High** threshold reduces hello number of times a policy is triggered and minimizes hello impact toousers.</span></span>
<span data-ttu-id="10e3d-317">그러나이 메서드를 제외 **낮은** 및 **보통** 수 하지를 보호 하는 id 또는 장치 hello 정책에서 위험에 대 한 플래그가 지정 된 이전에 의심 사용자나 손상 toobe 알려진 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-317">However, it excludes **Low** and **Medium** users flagged for risk from hello policy, which may not secure identities or devices that were previously suspected or known toobe compromised.</span></span>

<span data-ttu-id="10e3d-318">설정이 정책을 hello 하는 경우</span><span class="sxs-lookup"><span data-stu-id="10e3d-318">When setting hello policy,</span></span>

* <span data-ttu-id="10e3d-319">가능성이 높은 toogenerate 많이 거짓 긍정 (개발자, 보안 분석가) 인 사용자를 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-319">Exclude users who are likely toogenerate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="10e3d-320">로캘에서 여기서 hello 정책 사용 불가능 한 사용자를 제외 (예를 들어 없는 액세스 toohelpdesk)</span><span class="sxs-lookup"><span data-stu-id="10e3d-320">Exclude users in locales where enabling hello policy is not practical (for example no access toohelpdesk)</span></span>
* <span data-ttu-id="10e3d-321">초기 정책이 롤아웃하는 동안 또는 최종 사용자가 확인하는 과제를 최소화해야 하는 경우 **높음** 임계값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-321">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="10e3d-322">조직이 보안을 강화해야 하는 경우 **낮음** 임계값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-322">Use a **Low** threshold if your organization requires greater security.</span></span> <span data-ttu-id="10e3d-323">**낮은** 임계값을 선택하면 추가 사용자 로그인 과제가 발생하지만 보안이 강화됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-323">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="10e3d-324">기본 권장 대부분의 조직에 대 한 규칙 tooconfigure을는 hello는 **보통** 임계값 toostrike 보안과 유용성 간의 균형입니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-324">hello recommended default for most organizations is tooconfigure a rule for a **Medium** threshold toostrike a balance between usability and security.</span></span>

<span data-ttu-id="10e3d-325">사용자 환경 관련 hello에 대 한 개요를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-325">For an overview of hello related user experience, see:</span></span>

* <span data-ttu-id="10e3d-326">[손상된 계정 복구 흐름](active-directory-identityprotection-flows.md#compromised-account-recovery)</span><span class="sxs-lookup"><span data-stu-id="10e3d-326">[Compromised account recovery flow](active-directory-identityprotection-flows.md#compromised-account-recovery).</span></span>  
* <span data-ttu-id="10e3d-327">[손상된 계정 차단됨 흐름](active-directory-identityprotection-flows.md#compromised-account-blocked)</span><span class="sxs-lookup"><span data-stu-id="10e3d-327">[Compromised account blocked flow](active-directory-identityprotection-flows.md#compromised-account-blocked).</span></span>  

<span data-ttu-id="10e3d-328">**tooopen hello 관련된 구성 대화 상자**:</span><span class="sxs-lookup"><span data-stu-id="10e3d-328">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="10e3d-329">Hello에 **Azure AD Identity Protection** 블레이드 hello **구성** 섹션에서 클릭 **사용자 위험 정책**합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-329">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **User risk policy**.</span></span>

    <span data-ttu-id="10e3d-330">![사용자 위험 정책](./media/active-directory-identityprotection/1009.png "사용자 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="10e3d-330">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

### <a name="mitigating-user-risk-events"></a><span data-ttu-id="10e3d-331">사용자 위험 이벤트 완화</span><span class="sxs-lookup"><span data-stu-id="10e3d-331">Mitigating user risk events</span></span>
<span data-ttu-id="10e3d-332">관리자는 로그인 시 사용자 위험 보안 정책 tooblock 사용자 hello 위험 수준에 따라 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-332">Administrators can set a user risk security policy tooblock users upon sign-in depending on hello risk level.</span></span>

<span data-ttu-id="10e3d-333">로그인 차단:</span><span class="sxs-lookup"><span data-stu-id="10e3d-333">Blocking a sign-in:</span></span>

* <span data-ttu-id="10e3d-334">Hello 영향을 받는 사용자에 대 한 새 사용자 위험 이벤트 hello 생성할을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-334">Prevents hello generation of new user risk events for hello affected user</span></span>
* <span data-ttu-id="10e3d-335">수 있도록 관리자 toomanually hello 사용자의 id에 영향을 주는 hello 위험 이벤트를 수정 하 고 tooa 보안 상태를 복원</span><span class="sxs-lookup"><span data-stu-id="10e3d-335">Enables administrators toomanually remediate hello risk events affecting hello user's identity and restore it tooa secure state</span></span>



## <a name="multi-factor-authentication-registration-policy"></a><span data-ttu-id="10e3d-336">Multi-Factor Authentication 등록 정책</span><span class="sxs-lookup"><span data-stu-id="10e3d-336">Multi-factor authentication registration policy</span></span>
<span data-ttu-id="10e3d-337">Azure multi-factor authentication은 사용자를 확인 하는 것 이상의 사용자 이름 및 암호 사용 하 여 hello를 해야 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-337">Azure multi-factor authentication is a method of verifying who you are that requires hello use of more than just a username and password.</span></span> <span data-ttu-id="10e3d-338">보안 toouser 로그인 및 트랜잭션에 두 번째 계층을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-338">It provides a second layer of security toouser sign-ins and transactions.</span></span>  
<span data-ttu-id="10e3d-339">다음과 같은 이유로, 사용자 로그인에 Azure Multi-Factor Authentication을 요구하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-339">We recommend that you require Azure multi-factor authentication for user sign-ins because it:</span></span>

* <span data-ttu-id="10e3d-340">다양한 간편한 확인 옵션과 함께 강력한 인증 제공</span><span class="sxs-lookup"><span data-stu-id="10e3d-340">Delivers strong authentication with a range of easy verification options</span></span>
* <span data-ttu-id="10e3d-341">중요 한 역할 조직 tooprotect를 준비 하 고 계정 손상 복구</span><span class="sxs-lookup"><span data-stu-id="10e3d-341">Plays a key role in preparing your organization tooprotect and recover from account compromises</span></span>

<span data-ttu-id="10e3d-342">![사용자 위험 정책](./media/active-directory-identityprotection/1019.png "사용자 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="10e3d-342">![User ridk policy](./media/active-directory-identityprotection/1019.png "User ridk policy")</span></span>

<span data-ttu-id="10e3d-343">자세한 내용은 [Azure Multi-Factor Authentication 정의](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="10e3d-343">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

<span data-ttu-id="10e3d-344">Azure AD Identity Protection 수 있도록 하는 정책을 구성 하 여 hello 롤아웃 multi-factor authentication 등록을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-344">Azure AD Identity Protection helps you manage hello roll-out of multi-factor authentication registration by configuring a policy that enables you to:</span></span>

* <span data-ttu-id="10e3d-345">Hello 사용자 및 그룹 hello 정책 설정에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-345">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="10e3d-346">![MFA 정책](./media/active-directory-identityprotection/1020.png "MFA 정책")</span><span class="sxs-lookup"><span data-stu-id="10e3d-346">![MFA policy](./media/active-directory-identityprotection/1020.png "MFA policy")</span></span>
* <span data-ttu-id="10e3d-347">Hello 정책 트리거할 때 적용 하는 집합 hello 컨트롤 toobe::</span><span class="sxs-lookup"><span data-stu-id="10e3d-347">Set hello controls toobe enforced when hello policy triggers::</span></span>  

    <span data-ttu-id="10e3d-348">![MFA 정책](./media/active-directory-identityprotection/1021.png "MFA 정책")</span><span class="sxs-lookup"><span data-stu-id="10e3d-348">![MFA policy](./media/active-directory-identityprotection/1021.png "MFA policy")</span></span>
* <span data-ttu-id="10e3d-349">정책 hello 상태 전환:</span><span class="sxs-lookup"><span data-stu-id="10e3d-349">Switch hello state of your policy:</span></span>

    <span data-ttu-id="10e3d-350">![MFA 정책](./media/active-directory-identityprotection/403.png "MFA 정책")</span><span class="sxs-lookup"><span data-stu-id="10e3d-350">![MFA policy](./media/active-directory-identityprotection/403.png "MFA policy")</span></span>
* <span data-ttu-id="10e3d-351">Hello 현재 등록 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-351">View hello current registration status:</span></span>

    <span data-ttu-id="10e3d-352">![MFA 정책](./media/active-directory-identityprotection/1022.png "MFA 정책")</span><span class="sxs-lookup"><span data-stu-id="10e3d-352">![MFA policy](./media/active-directory-identityprotection/1022.png "MFA policy")</span></span>

<span data-ttu-id="10e3d-353">사용자 환경 관련 hello에 대 한 개요를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-353">For an overview of hello related user experience, see:</span></span>

* <span data-ttu-id="10e3d-354">[Multi-Factor Authentication 등록 흐름](active-directory-identityprotection-flows.md#multi-factor-authentication-registration)</span><span class="sxs-lookup"><span data-stu-id="10e3d-354">[Multi-factor authentication registration flow](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span></span>  
* <span data-ttu-id="10e3d-355">[Azure AD ID 보호를 사용하는 로그인 환경](active-directory-identityprotection-flows.md)</span><span class="sxs-lookup"><span data-stu-id="10e3d-355">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span></span>  

<span data-ttu-id="10e3d-356">**tooopen hello 관련된 구성 대화 상자**:</span><span class="sxs-lookup"><span data-stu-id="10e3d-356">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="10e3d-357">Hello에 **Azure AD Identity Protection** 블레이드 hello **구성** 섹션에서 클릭 **multi-factor authentication 등록**합니다.</span><span class="sxs-lookup"><span data-stu-id="10e3d-357">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **Multi-factor authentication registration**.</span></span>

    <span data-ttu-id="10e3d-358">![MFA 정책](./media/active-directory-identityprotection/1019.png "MFA 정책")</span><span class="sxs-lookup"><span data-stu-id="10e3d-358">![MFA policy](./media/active-directory-identityprotection/1019.png "MFA policy")</span></span>

## <a name="next-steps"></a><span data-ttu-id="10e3d-359">다음 단계</span><span class="sxs-lookup"><span data-stu-id="10e3d-359">Next steps</span></span>
* [<span data-ttu-id="10e3d-360">Channel 9: Azure AD 및 ID 표시: ID 보호 미리 보기</span><span class="sxs-lookup"><span data-stu-id="10e3d-360">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span></span>](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [<span data-ttu-id="10e3d-361">Azure Active Directory ID 보호 활성화</span><span class="sxs-lookup"><span data-stu-id="10e3d-361">Enabling Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-enable.md)

* [<span data-ttu-id="10e3d-362">Azure Active Directory ID 보호에서 검색하는 취약성</span><span class="sxs-lookup"><span data-stu-id="10e3d-362">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-vulnerabilities.md)

* [<span data-ttu-id="10e3d-363">Azure Active Directory 위험 이벤트</span><span class="sxs-lookup"><span data-stu-id="10e3d-363">Azure Active Directory risk events</span></span>](active-directory-identity-protection-risk-events.md)

* [<span data-ttu-id="10e3d-364">Azure Active Directory ID 보호 알림</span><span class="sxs-lookup"><span data-stu-id="10e3d-364">Azure Active Directory Identity Protection notifications</span></span>](active-directory-identityprotection-notifications.md)

* [<span data-ttu-id="10e3d-365">Azure Active Directory ID 보호 플레이 북</span><span class="sxs-lookup"><span data-stu-id="10e3d-365">Azure Active Directory Identity Protection playbook</span></span>](active-directory-identityprotection-playbook.md)

* [<span data-ttu-id="10e3d-366">Azure Active Directory ID 보호 용어집</span><span class="sxs-lookup"><span data-stu-id="10e3d-366">Azure Active Directory Identity Protection glossary</span></span>](active-directory-identityprotection-glossary.md)

* [<span data-ttu-id="10e3d-367">Azure AD ID 보호를 사용하는 로그인 환경</span><span class="sxs-lookup"><span data-stu-id="10e3d-367">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)

* [<span data-ttu-id="10e3d-368">Azure Active Directory Id 보호-어떻게 toounblock 사용자</span><span class="sxs-lookup"><span data-stu-id="10e3d-368">Azure Active Directory Identity Protection - How toounblock users</span></span>](active-directory-identityprotection-unblock-howto.md)

* [<span data-ttu-id="10e3d-369">Azure Active Directory ID 보호 및 Microsoft Graph 시작</span><span class="sxs-lookup"><span data-stu-id="10e3d-369">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>](active-directory-identityprotection-graph-getting-started.md)
