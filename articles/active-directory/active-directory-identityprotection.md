---
title: "Azure Active Directory ID 보호 | Microsoft Docs"
description: "Azure AD ID 보호를 사용하여 손상된 ID 및 장치를 악용하는 공격자의 능력을 제한하고 이전에 손상이 우려되거나 손상된 ID 또는 장치를 보호할 수 있는 방법을 알아봅니다."
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
ms.openlocfilehash: 0c7a8d68c0df729441e3f7faa5cd06066db1261d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-identity-protection"></a><span data-ttu-id="bacfe-104">Azure Active Directory ID 보호</span><span class="sxs-lookup"><span data-stu-id="bacfe-104">Azure Active Directory Identity Protection</span></span>

<span data-ttu-id="bacfe-105">Azure Active Directory ID 보호는 Azure AD Premium P2 버전의 기능으로, 다음 작업을 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-105">Azure Active Directory Identity Protection is a feature of the Azure AD Premium P2 edition that enables you to:</span></span>

- <span data-ttu-id="bacfe-106">조직의 ID에 영향을 미치는 잠재적인 취약점을 검색</span><span class="sxs-lookup"><span data-stu-id="bacfe-106">Detect potential vulnerabilities affecting your organization’s identities</span></span>

- <span data-ttu-id="bacfe-107">조직 ID와 관련된 검색된 의심스러운 작업에 대한 자동화된 응답 구성</span><span class="sxs-lookup"><span data-stu-id="bacfe-107">Configure automated responses to detected suspicious actions that are related to your organization’s identities</span></span>  

- <span data-ttu-id="bacfe-108">의심스러운 인시던트 조사 및 해결을 위한 작업 수행</span><span class="sxs-lookup"><span data-stu-id="bacfe-108">Investigate suspicious incidents and take appropriate action to resolve them</span></span>   


## <a name="getting-started"></a><span data-ttu-id="bacfe-109">시작</span><span class="sxs-lookup"><span data-stu-id="bacfe-109">Getting started</span></span>

<span data-ttu-id="bacfe-110">Microsoft는 10년 넘게 클라우드 기반 ID를 보호하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-110">Microsoft secures cloud-based identities for more than a decade.</span></span> <span data-ttu-id="bacfe-111">Azure Active Directory ID 보호를 사용하는 경우 사용자 환경에서 Microsoft가 ID 보호를 위해 사용하는 것과 동일한 보호 시스템을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-111">With Azure Active Directory Identity Protection, in your environment, you can use the same protection systems Microsoft uses to secure identities.</span></span>

<span data-ttu-id="bacfe-112">대부분의 보안 침해는 공격자가 사용자의 ID를 도용하여 환경에 대한 액세스 권한을 얻을 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-112">The vast majority of security breaches take place when attackers gain access to an environment by stealing a user’s identity.</span></span> <span data-ttu-id="bacfe-113">시간이 지나면서 공격자는 점점 더 효과적으로 제3자 침해를 활용하고 정교한 피싱 공격을 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-113">Over the years, attackers have become increasingly effective in leveraging third party breaches and using sophisticated phishing attacks.</span></span> <span data-ttu-id="bacfe-114">일단 공격자가 더 낮은 권한을 가진 사용자 계정에 대한 액세스 권한을 얻게 되면 측면 이동을 통해 비교적 간단하게 중요한 회사 리소스에 대한 액세스 권한을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-114">As soon as an attacker gains access to even low privileged user accounts, it is relatively easy for them to gain access to important company resources through lateral movement.</span></span>

<span data-ttu-id="bacfe-115">이에 따라 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-115">As a consequence of this, you need to:</span></span>

- <span data-ttu-id="bacfe-116">해당 권한 수준에 관계 없이 모든 ID 보호</span><span class="sxs-lookup"><span data-stu-id="bacfe-116">Protect all identities regardless of their privilege level</span></span>

- <span data-ttu-id="bacfe-117">손상된 ID가 남용되지 않도록 사전에 방지</span><span class="sxs-lookup"><span data-stu-id="bacfe-117">Proactively prevent compromised identities from being abused</span></span>

<span data-ttu-id="bacfe-118">손상된 ID를 검색하는 것은 쉬운 작업이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-118">Discovering compromised identities is no easy task.</span></span> <span data-ttu-id="bacfe-119">Azure Active Directory는 적응 Machine Learning 알고리즘 및 추론을 사용하여 잠재적으로 손상된 ID를 나타낼 수 있는 비정상 상태 및 의심스러운 인시던트를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-119">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect anomalies and suspicious incidents that indicate potentially compromised identities.</span></span> <span data-ttu-id="bacfe-120">ID 보호는 이 데이터를 사용하여 검색된 문제를 평가하고 적절한 완화 또는 수정 작업을 수행할 수 있도록 하는 보고서 및 경고를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-120">Using this data, Identity Protection generates reports and alerts that enable you to evaluate the detected issues and take appropriate mitigation or remediation actions.</span></span>

<span data-ttu-id="bacfe-121">Azure Active Directory ID 보호는 모니터링 및 보고 도구 이상입니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-121">Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span></span> <span data-ttu-id="bacfe-122">조직의 ID를 보호하려면 지정된 위험 수준에 도달했을 때 검색된 문제에 자동으로 대응하는 위험 기반 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-122">To protect your organization's identities, you can configure risk-based policies that automatically respond to detected issues when a specified risk level has been reached.</span></span> <span data-ttu-id="bacfe-123">Azure Active Directory 및 EMS에서 제공되는 다른 조건부 액세스 제어 외에도 이러한 정책은 암호 재설정 및 Multi-Factor Authentication 적용을 포함하는 적응형 수정 작업을 자동으로 차단하거나 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-123">These policies, in addition to other conditional access controls provided by Azure Active Directory and EMS, can either automatically block or initiate adaptive remediation actions including password resets and multi-factor authentication enforcement.</span></span>


#### <a name="identity-protection-capabilities"></a><span data-ttu-id="bacfe-124">ID 보호 기능</span><span class="sxs-lookup"><span data-stu-id="bacfe-124">Identity Protection capabilities</span></span>

<span data-ttu-id="bacfe-125">**취약점 및 위험 계정 검색:**</span><span class="sxs-lookup"><span data-stu-id="bacfe-125">**Detecting vulnerabilities and risky accounts:**</span></span>  

* <span data-ttu-id="bacfe-126">취약점을 강조 표시하여 전반적인 보안 포스처를 개선하도록 사용자 지정 권장 사항 제공</span><span class="sxs-lookup"><span data-stu-id="bacfe-126">Providing custom recommendations to improve overall security posture by highlighting vulnerabilities</span></span>
* <span data-ttu-id="bacfe-127">로그인 위험 수준 계산</span><span class="sxs-lookup"><span data-stu-id="bacfe-127">Calculating sign-in risk levels</span></span>
* <span data-ttu-id="bacfe-128">사용자 위험 수준 계산</span><span class="sxs-lookup"><span data-stu-id="bacfe-128">Calculating user risk levels</span></span>


<span data-ttu-id="bacfe-129">**위험 이벤트 조사:**</span><span class="sxs-lookup"><span data-stu-id="bacfe-129">**Investigating risk events:**</span></span>

* <span data-ttu-id="bacfe-130">위험 이벤트에 대한 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="bacfe-130">Sending notifications for risk events</span></span>
* <span data-ttu-id="bacfe-131">관련된 컨텍스트 정보를 사용하여 위험 이벤트 조사</span><span class="sxs-lookup"><span data-stu-id="bacfe-131">Investigating risk events using relevant and contextual information</span></span>
* <span data-ttu-id="bacfe-132">기본 워크플로를 제공하여 조사 추적</span><span class="sxs-lookup"><span data-stu-id="bacfe-132">Providing basic workflows to track investigations</span></span>
* <span data-ttu-id="bacfe-133">암호 재설정 등 수정 작업에 쉬운 액세스 제공</span><span class="sxs-lookup"><span data-stu-id="bacfe-133">Providing easy access to remediation actions such as password reset</span></span>

<span data-ttu-id="bacfe-134">**위험 기준 조건부 액세스 정책:**</span><span class="sxs-lookup"><span data-stu-id="bacfe-134">**Risk-based conditional access policies:**</span></span>

* <span data-ttu-id="bacfe-135">로그인을 차단하거나 Multi-Factor Authentication 과제를 요구하여 위험한 로그인을 완화하는 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-135">Policy to mitigate risky sign-ins by blocking sign-ins or requiring multi-factor authentication challenges.</span></span>
* <span data-ttu-id="bacfe-136">위험한 사용자 계정 차단 및 보호 정책</span><span class="sxs-lookup"><span data-stu-id="bacfe-136">Policy to block or secure risky user accounts</span></span>
* <span data-ttu-id="bacfe-137">Multi-Factor Authentication에 사용자 등록 요구 정책</span><span class="sxs-lookup"><span data-stu-id="bacfe-137">Policy to require users to register for multi-factor authentication</span></span>



## <a name="identity-protection-roles"></a><span data-ttu-id="bacfe-138">ID 보호 역할</span><span class="sxs-lookup"><span data-stu-id="bacfe-138">Identity Protection roles</span></span>

<span data-ttu-id="bacfe-139">ID 보호 구현에 관련된 관리 작업의 부하를 분산하기 위해 몇 가지 역할을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-139">To load balance the management activities around your Identity Protection implementation, you can assign several roles.</span></span> <span data-ttu-id="bacfe-140">Azure AD ID 보호는 3가지 디렉터리 역할을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-140">Azure AD Identity Protection supports 3 directory roles:</span></span>

| <span data-ttu-id="bacfe-141">역할</span><span class="sxs-lookup"><span data-stu-id="bacfe-141">Role</span></span>                         | <span data-ttu-id="bacfe-142">가능한 작업</span><span class="sxs-lookup"><span data-stu-id="bacfe-142">Can do</span></span>                          | <span data-ttu-id="bacfe-143">불가능한 작업</span><span class="sxs-lookup"><span data-stu-id="bacfe-143">Cannot do</span></span>
| :--                          | ---                                |  ---   |
| <span data-ttu-id="bacfe-144">전역 관리자</span><span class="sxs-lookup"><span data-stu-id="bacfe-144">Global administrator</span></span>         | <span data-ttu-id="bacfe-145">ID 보호에 대한 완전한 액세스, ID 보호 등록</span><span class="sxs-lookup"><span data-stu-id="bacfe-145">Full access to Identity Protection, Onboard Identity Protection</span></span>| |
| <span data-ttu-id="bacfe-146">보안 관리자</span><span class="sxs-lookup"><span data-stu-id="bacfe-146">Security administrator</span></span>       | <span data-ttu-id="bacfe-147">ID 보호에 대한 완전한 액세스</span><span class="sxs-lookup"><span data-stu-id="bacfe-147">Full access to Identity Protection</span></span> | <span data-ttu-id="bacfe-148">ID 보호 등록, 사용자의 암호 재설정</span><span class="sxs-lookup"><span data-stu-id="bacfe-148">Onboard Identity Protection,  reset passwords for a user</span></span> |
| <span data-ttu-id="bacfe-149">보안 판독기</span><span class="sxs-lookup"><span data-stu-id="bacfe-149">Security reader</span></span>              | <span data-ttu-id="bacfe-150">ID 보호에 대한 읽기 전용 액세스</span><span class="sxs-lookup"><span data-stu-id="bacfe-150">Ready-only access to Identity Protection</span></span> | <span data-ttu-id="bacfe-151">ID 보호 등록, 사용자 수정, 정책 구성, 암호 재설정</span><span class="sxs-lookup"><span data-stu-id="bacfe-151">Onboard Identity Protection, remidiate users, configure policies,  reset passwords</span></span> |




<span data-ttu-id="bacfe-152">자세한 내용은 [Azure Active Directory에서 관리자 역할 할당](active-directory-assign-admin-roles-azure-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bacfe-152">For more details, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span></span>



## <a name="detection"></a><span data-ttu-id="bacfe-153">감지</span><span class="sxs-lookup"><span data-stu-id="bacfe-153">Detection</span></span>

### <a name="vulnerabilities"></a><span data-ttu-id="bacfe-154">취약점</span><span class="sxs-lookup"><span data-stu-id="bacfe-154">Vulnerabilities</span></span>

<span data-ttu-id="bacfe-155">Azure Active Directory ID 보호는 구성을 분석하고 사용자의 ID에 영향을 줄 수 있는 취약점을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-155">Azure Active Directory Identity Protection analyses your configuration and detects vulnerabilities that can have an impact on your user's identities.</span></span> <span data-ttu-id="bacfe-156">자세한 내용은 [Azure Active Directory ID 보호에서 검색되는 취약성](active-directory-identityprotection-vulnerabilities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bacfe-156">For more details, see [Vulnerabilities detected by Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span></span>

### <a name="risk-events"></a><span data-ttu-id="bacfe-157">위험 이벤트</span><span class="sxs-lookup"><span data-stu-id="bacfe-157">Risk events</span></span>

<span data-ttu-id="bacfe-158">Azure Active Directory는 적응 Machine Learning 알고리즘 및 추론을 사용하여 사용자의 ID와 관련된 의심스러운 작업을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-158">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user's identities.</span></span> <span data-ttu-id="bacfe-159">시스템은 검색된 각 의심스러운 작업에 대한 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-159">The system creates a record for each detected suspicious action.</span></span> <span data-ttu-id="bacfe-160">이러한 레코드를 위험 이벤트라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-160">These records are also known as risk events.</span></span>  
<span data-ttu-id="bacfe-161">자세한 내용은 [Azure Active Directory 위험 이벤트](active-directory-identity-protection-risk-events.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bacfe-161">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>


## <a name="investigation"></a><span data-ttu-id="bacfe-162">조사</span><span class="sxs-lookup"><span data-stu-id="bacfe-162">Investigation</span></span>
<span data-ttu-id="bacfe-163">ID 보호를 통한 이동은 일반적으로 ID 보호 대시보드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-163">Your journey through Identity Protection typically starts with the Identity Protection dashboard.</span></span>

<span data-ttu-id="bacfe-164">![수정](./media/active-directory-identityprotection/1000.png "수정")</span><span class="sxs-lookup"><span data-stu-id="bacfe-164">![Remediation](./media/active-directory-identityprotection/1000.png "Remediation")</span></span>

<span data-ttu-id="bacfe-165">대시보드는 다음에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-165">The dashboard gives you access to:</span></span>

* <span data-ttu-id="bacfe-166">**위험 플래그가 지정된 사용자**, **위험 이벤트** 및 **취약성**과 같은 보고서</span><span class="sxs-lookup"><span data-stu-id="bacfe-166">Reports such as **Users flagged for risk**, **Risk events** and **Vulnerabilities**</span></span>
* <span data-ttu-id="bacfe-167">**보안 정책**, **알림** 및 **다단계 인증 등록** 구성과 같은 설정</span><span class="sxs-lookup"><span data-stu-id="bacfe-167">Settings such as the configuration of your **Security Policies**, **Notifications** and **multi-factor authentication registration**</span></span>

<span data-ttu-id="bacfe-168">일반적으로 조사를 위한 시작점으로, 위험 이벤트와 관련된 활동, 로그 및 기타 관련 정보를 검토하여 재구성 또는 완화 단계가 필요한지 여부, ID가 손상된 방식 및 손상된 ID가 사용된 방식을 결정하는 과정입니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-168">It is typically your starting point for investigation, which is the process of reviewing the activities, logs, and other relevant information related to a risk event to decide whether remediation or mitigation steps are necessary,  and how the identity was compromised, and understand how the compromised identity was used.</span></span>

<span data-ttu-id="bacfe-169">Azure Active Directory 보호에서 전자 메일을 통해 보내는 [알림](active-directory-identityprotection-notifications.md) 에 조사 활동을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-169">You can tie your investigation activities to the [notifications](active-directory-identityprotection-notifications.md) Azure Active Directory Protection sends per email.</span></span>

<span data-ttu-id="bacfe-170">다음 섹션에서는 조사와 관련된 자세한 내용 및 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-170">The following sections provide you with more details and the steps that are related to an investigation.</span></span>  


## <a name="risky-sign-ins"></a><span data-ttu-id="bacfe-171">위험한 로그인</span><span class="sxs-lookup"><span data-stu-id="bacfe-171">Risky sign-ins</span></span>

<span data-ttu-id="bacfe-172">Azure Active Directory는 [위험 이벤트 유형](active-directory-reporting-risk-events.md#risk-event-types)을 실시간 및 오프라인으로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-172">Azure Active Directory detects [risk event types](active-directory-reporting-risk-events.md#risk-event-types) in real-time and offline.</span></span> <span data-ttu-id="bacfe-173">사용자 로그인 중에 검색된 각 위험 이벤트는 위험한 로그인이라는 논리적 개념을 파생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-173">Each risk event that has been detected for a sign-in of a user contributes to a logical concept called risky sign-in.</span></span> <span data-ttu-id="bacfe-174">위험한 로그인은 사용자 계정의 정당한 소유자가 수행하지 않았을 수 있는 로그인 시도에 대한 지표입니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-174">A risky sign-in is an indicator for a sign-in attempt that might not have been performed by the legitimate owner of a user account.</span></span>


### <a name="sign-in-risk-level"></a><span data-ttu-id="bacfe-175">로그인 위험 수준</span><span class="sxs-lookup"><span data-stu-id="bacfe-175">Sign-in risk level</span></span>

<span data-ttu-id="bacfe-176">로그인 위험 수준은 로그인 시도를 사용자 계정의 합법적인 소유자가 수행하지 않았을 가능성에 대한 지표입니다(높음, 중간 또는 낮음).</span><span class="sxs-lookup"><span data-stu-id="bacfe-176">A sign-in risk level is an indication (High, Medium, or Low) of the likelihood that a sign-in attempt was not performed by the legitimate owner of a user account.</span></span>

### <a name="mitigating-sign-in-risk-events"></a><span data-ttu-id="bacfe-177">로그인 위험 이벤트 완화</span><span class="sxs-lookup"><span data-stu-id="bacfe-177">Mitigating sign-in risk events</span></span>

<span data-ttu-id="bacfe-178">완화는 ID 또는 장치를 안전한 상태로 복원하지 않고 손상된 ID 또는 장치를 악용하는 공격자의 능력을 제한하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-178">A mitigation is an action to limit the ability of an attacker to exploit a compromised identity or device without restoring the identity or device to a safe state.</span></span> <span data-ttu-id="bacfe-179">완화 조치는 ID 또는 장치와 연결된 이전 로그인 위험 이벤트를 해결하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-179">A mitigation does not resolve previous sign-in risk events associated with the identity or device.</span></span>

<span data-ttu-id="bacfe-180">위험한 로그인을 자동으로 완화하기 위해 로그인 위험 보안 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-180">To mitigate risky sign-ins automatically, you can configure sign-in risk security policicies.</span></span> <span data-ttu-id="bacfe-181">이러한 정책을 사용하여 사용자 또는 로그인의 위험 수준을 고려하여 위험한 로그인을 차단하거나 사용자가 Multi-Factor Authentication을 수행하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-181">Using these policies, you consider the risk level of the user or the sign-in to block risky sign-ins or require the user to perform multi-factor authentication.</span></span> <span data-ttu-id="bacfe-182">이러한 작업은 공격자가 피해를 일으키는 도난 당한 ID를 악용하지 않도록 방지하며 ID를 보호할 시간을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-182">These actions may prevent an attacker from exploiting a stolen identity to cause damage, and may give you some time to secure the identity.</span></span>

### <a name="sign-in-risk-security-policy"></a><span data-ttu-id="bacfe-183">로그인 위험 보안 정책</span><span class="sxs-lookup"><span data-stu-id="bacfe-183">Sign-in risk security policy</span></span>
<span data-ttu-id="bacfe-184">로그인 위험 정책은 특정 로그인에 대한 위험을 평가하고 미리 정의된 조건 및 규칙에 따라 완화를 적용하는 조건부 액세스 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-184">A sign-in risk policy is a conditional access policy that evaluates the risk to a specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

<span data-ttu-id="bacfe-185">![로그인 위험 정책](./media/active-directory-identityprotection/1014.png "로그인 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="bacfe-185">![Sign-in risk policy](./media/active-directory-identityprotection/1014.png "Sign-in risk policy")</span></span>

<span data-ttu-id="bacfe-186">Azure AD ID 보호를 사용하면 다음을 사용하여 위험한 로그인을 완화하도록 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-186">Azure AD Identity Protection helps you manage the mitigation of risky sign-ins by enabling you to:</span></span>

* <span data-ttu-id="bacfe-187">정책이 적용되는 사용자 및 그룹 설정:</span><span class="sxs-lookup"><span data-stu-id="bacfe-187">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="bacfe-188">![로그인 위험 정책](./media/active-directory-identityprotection/1015.png "로그인 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="bacfe-188">![Sign-in risk policy](./media/active-directory-identityprotection/1015.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="bacfe-189">정책을 트리거하는 로그인 위험 수준 임계값 설정(낮음, 보통 또는 높음):</span><span class="sxs-lookup"><span data-stu-id="bacfe-189">Set the sign-in risk level threshold (low, medium, or high) that triggers the policy:</span></span>

    <span data-ttu-id="bacfe-190">![로그인 위험 정책](./media/active-directory-identityprotection/1016.png "로그인 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="bacfe-190">![Sign-in risk policy](./media/active-directory-identityprotection/1016.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="bacfe-191">정책이 트리거할 때 적용될 컨트롤 설정:</span><span class="sxs-lookup"><span data-stu-id="bacfe-191">Set the controls to be enforced when the policy triggers:</span></span>  

    <span data-ttu-id="bacfe-192">![로그인 위험 정책](./media/active-directory-identityprotection/1017.png "로그인 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="bacfe-192">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="bacfe-193">정책 상태 전환:</span><span class="sxs-lookup"><span data-stu-id="bacfe-193">Switch the state of your policy:</span></span>

    <span data-ttu-id="bacfe-194">![MFA 등록](./media/active-directory-identityprotection/403.png "MFA 등록")</span><span class="sxs-lookup"><span data-stu-id="bacfe-194">![MFA Registration](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="bacfe-195">활성화하기 전에 변경의 영향 검토 및 평가:</span><span class="sxs-lookup"><span data-stu-id="bacfe-195">Review and evaluate the impact of a change before activating it:</span></span>

    <span data-ttu-id="bacfe-196">![로그인 위험 정책](./media/active-directory-identityprotection/1018.png "로그인 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="bacfe-196">![Sign-in risk policy](./media/active-directory-identityprotection/1018.png "Sign-in risk policy")</span></span>

#### <a name="what-you-need-to-know"></a><span data-ttu-id="bacfe-197">알아야 하는 작업</span><span class="sxs-lookup"><span data-stu-id="bacfe-197">What you need to know</span></span>
<span data-ttu-id="bacfe-198">다단계 인증을 요구하는 로그인 위험 보안 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-198">You can configure a sign-in risk security policy to require multi-factor authentication:</span></span>

<span data-ttu-id="bacfe-199">![로그인 위험 정책](./media/active-directory-identityprotection/1017.png "로그인 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="bacfe-199">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>

<span data-ttu-id="bacfe-200">그러나 보안상의 이유로 이 설정은 다단계 인증에 이미 등록된 사용자에게만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-200">However, for security reasons, this setting only works for users that have already been registered for multi-factor authentication.</span></span> <span data-ttu-id="bacfe-201">아직 다단계 인증에 등록되지 않은 사용자가 다단계 인증을 요구하는 조건을 충족하는 경우 해당 사용자는 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-201">If the condition to require multi-factor authentication is satisfied for a user who is not yet registered for multi-factor authentication, the user is blocked.</span></span>

<span data-ttu-id="bacfe-202">위험한 로그인에 대해 다단계 인증을 요구하려면 다음을 수행하는 것이 좋습니다</span><span class="sxs-lookup"><span data-stu-id="bacfe-202">As a best practice, if you want to require multi-factor authentication for risky sign-ins, you should:</span></span>

1. <span data-ttu-id="bacfe-203">영향을 받는 사용자에 대해 [다단계 인증 등록 정책](#multi-factor-authentication-registration-policy)을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-203">Enable the [multi-factor authentication registration policy](#multi-factor-authentication-registration-policy) for the affected users.</span></span>
2. <span data-ttu-id="bacfe-204">영향을 받는 사용자가 위험하지 않은 세션에 로그인하여 MFA 등록을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-204">Require the affected users to login in a non-risky session to perform a MFA registration</span></span>

<span data-ttu-id="bacfe-205">이러한 단계를 완료하면 위험한 로그인에 대해 다단계 인증이 요구됩니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-205">Completing these steps ensures that multi-factor authentication is required for a risky sign-in.</span></span>

#### <a name="best-practices"></a><span data-ttu-id="bacfe-206">모범 사례</span><span class="sxs-lookup"><span data-stu-id="bacfe-206">Best practices</span></span>
<span data-ttu-id="bacfe-207">**높음** 임계값을 선택하면 정책이 트리거되는 횟수를 줄이고 사용자에게 미치는 영향을 최소화합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-207">Choosing a **High** threshold reduces the number of times a policy is triggered and minimizes the impact to users.</span></span>  

<span data-ttu-id="bacfe-208">그러나 정책에서 위험 플래그가 지정된 **낮음** 및 **보통** 로그인을 제외하며, 이는 공격자가 손상된 ID를 악용하지 못하도록 차단하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-208">However, it excludes **Low** and **Medium** sign-ins flagged for risk from the policy, which may not block an attacker from exploiting a compromised identity.</span></span>

<span data-ttu-id="bacfe-209">정책을 설정 하는 경우</span><span class="sxs-lookup"><span data-stu-id="bacfe-209">When setting the policy,</span></span>

* <span data-ttu-id="bacfe-210">다단계 인증이 없는/있을 수 없는 사용자 제외</span><span class="sxs-lookup"><span data-stu-id="bacfe-210">Exclude users who do not/cannot have multi-factor authentication</span></span>
* <span data-ttu-id="bacfe-211">정책을 사용하지 않는 것이 실용적이지 않은 로캘에서 사용자를 제외합니다(예: 기술 지원팀에 액세스 권한 없음).</span><span class="sxs-lookup"><span data-stu-id="bacfe-211">Exclude users in locales where enabling the policy is not practical (for example no access to helpdesk)</span></span>
* <span data-ttu-id="bacfe-212">많은 가양성(개발자, 보안 분석가)을 생성할 수 있는 사용자를 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-212">Exclude users who are likely to generate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="bacfe-213">초기 정책이 롤아웃하는 동안 또는 최종 사용자가 확인하는 과제를 최소화해야 하는 경우 **높음** 임계값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-213">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="bacfe-214">조직에서 보안을 강화해야 하는 경우 **낮음** 임계값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-214">Use a **Low**  threshold if your organization requires greater security.</span></span> <span data-ttu-id="bacfe-215">**낮은** 임계값을 선택하면 추가 사용자 로그인 과제가 발생하지만 보안이 강화됩니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-215">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="bacfe-216">대부분의 조직에 권장되는 기본값은 **보통** 임계값에 대한 규칙을 구성하여 유용성과 보안 간의 균형을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-216">The recommended default for most organizations is to configure a rule for a **Medium** threshold to strike a balance between usability and security.</span></span>

<span data-ttu-id="bacfe-217">로그인 위험 정책은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-217">The sign-in risk policy is:</span></span>

* <span data-ttu-id="bacfe-218">최신 인증을 사용하여 모든 브라우저 트래픽 및 로그인에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-218">Applied to all browser traffic and sign-ins using modern authentication.</span></span>
* <span data-ttu-id="bacfe-219">ADFS 등 페더레이션된 IDP에서 WS-Trust 끝점을 사용하지 않도록 설정하여 이전 보안 프로토콜을 사용하는 응용 프로그램에 적용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-219">Not applied to applications using older security protocols by disabling the WS-Trust endpoint at the federated IDP, such as ADFS.</span></span>

<span data-ttu-id="bacfe-220">ID 보호 콘솔의 **위험 이벤트** 페이지에서는 모든 이벤트를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-220">The **Risk Events** page in the Identity Protection console lists all events:</span></span>

* <span data-ttu-id="bacfe-221">이 정책은 다음에 적용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-221">This policy was applied to</span></span>
* <span data-ttu-id="bacfe-222">작업을 검토하고 작업이 적절한지 여부를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-222">You can review the activity and determine whether the action was appropriate or not</span></span>

<span data-ttu-id="bacfe-223">관련 사용자 환경에 대한 개요는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bacfe-223">For an overview of the related user experience, see:</span></span>

* [<span data-ttu-id="bacfe-224">위험한 로그인 복구</span><span class="sxs-lookup"><span data-stu-id="bacfe-224">Risky sign-in recovery</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [<span data-ttu-id="bacfe-225">위험한 로그인 차단됨</span><span class="sxs-lookup"><span data-stu-id="bacfe-225">Risky sign-in blocked</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [<span data-ttu-id="bacfe-226">Azure AD ID 보호를 사용하는 로그인 환경</span><span class="sxs-lookup"><span data-stu-id="bacfe-226">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)  

<span data-ttu-id="bacfe-227">**관련 구성 대화 상자를 열려면**</span><span class="sxs-lookup"><span data-stu-id="bacfe-227">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="bacfe-228">**Azure AD ID 보호** 블레이드의 **구성** 섹션에서 **로그인 위험 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-228">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **Sign-in risk policy**.</span></span>

    <span data-ttu-id="bacfe-229">![사용자 위험 정책](./media/active-directory-identityprotection/1014.png "사용자 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="bacfe-229">![User ridk policy](./media/active-directory-identityprotection/1014.png "User ridk policy")</span></span>



## <a name="users-flagged-for-risk"></a><span data-ttu-id="bacfe-230">위험에 대한 플래그가 지정된 사용자</span><span class="sxs-lookup"><span data-stu-id="bacfe-230">Users flagged for risk</span></span>

<span data-ttu-id="bacfe-231">사용자에 대해 Azure Active Directory에서 검색된 모든 활성 [위험 이벤트](active-directory-identity-protection-risk-events.md)는 사용자 위험이라는 논리적 개념을 파생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-231">All active [risk events](active-directory-identity-protection-risk-events.md) that were detected by Azure Active Directory for a user contribute to a logical concept called user risk.</span></span> <span data-ttu-id="bacfe-232">위험 플래그가 지정된 사용자는 손상되었을 수 있는 사용자 계정에 대한 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-232">A user flagged for risk is an indicator for a user account that might have been compromised.</span></span>

![위험에 대한 플래그가 지정된 사용자](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a><span data-ttu-id="bacfe-234">사용자 위험 수준</span><span class="sxs-lookup"><span data-stu-id="bacfe-234">User risk level</span></span>

<span data-ttu-id="bacfe-235">사용자 위험 수준은 사용자의 ID가 손상된 가능성을 표시(높음, 보통 또는 낮음)합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-235">A user risk level is an indication (High, Medium, or Low) of the likelihood that the user’s identity has been compromised.</span></span> <span data-ttu-id="bacfe-236">사용자의 ID와 연결된 사용자 위험 이벤트에 따라 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-236">It is calculated based on the user risk events that are associated with a user's identity.</span></span>

<span data-ttu-id="bacfe-237">위험 이벤트의 상태는 **활성** 또는 **종료됨**입니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-237">The status of a risk event is either **Active** or **Closed**.</span></span> <span data-ttu-id="bacfe-238">**활성** 상태인 위험 이벤트만이 사용자 위험 수준 계산에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-238">Only risk events that are **Active** contribute to the user risk level calculation.</span></span>

<span data-ttu-id="bacfe-239">사용자 위험 수준은 다음 입력을 사용하여 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-239">The user risk level is calculated using the following inputs:</span></span>

* <span data-ttu-id="bacfe-240">사용자에 영향을 주는 활성 위험 이벤트</span><span class="sxs-lookup"><span data-stu-id="bacfe-240">Active risk events impacting the user</span></span>
* <span data-ttu-id="bacfe-241">이러한 이벤트의 위험 수준</span><span class="sxs-lookup"><span data-stu-id="bacfe-241">Risk level of these events</span></span>
* <span data-ttu-id="bacfe-242">수정 작업이 수행되었는지 여부</span><span class="sxs-lookup"><span data-stu-id="bacfe-242">Whether any remediation actions have been taken</span></span>

<span data-ttu-id="bacfe-243">![사용자 위험](./media/active-directory-identityprotection/1031.png "사용자 위험")</span><span class="sxs-lookup"><span data-stu-id="bacfe-243">![User risks](./media/active-directory-identityprotection/1031.png "User risks")</span></span>

<span data-ttu-id="bacfe-244">사용자 위험 수준을 사용하여 위험한 사용자의 로그인을 차단하는 조건부 액세스 정책을 만들 수 있고 해당 암호를 안전하게 변경하도록 강제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-244">You can use the user risk levels to create conditional access policies that block risky users from signing in, or force them to securely change their password.</span></span>

### <a name="closing-risk-events-manually"></a><span data-ttu-id="bacfe-245">수동으로 위험 이벤트 닫기</span><span class="sxs-lookup"><span data-stu-id="bacfe-245">Closing risk events manually</span></span>

<span data-ttu-id="bacfe-246">대부분의 경우에서 자동으로 위험 이벤트를 닫도록 다시 설정된 보안 암호와 같은 수정 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-246">In most cases, you will take remediation actions such as a secure password reset to automatically close risk events.</span></span> <span data-ttu-id="bacfe-247">그러나 불가능할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-247">However, this might not always be possible.</span></span>  
<span data-ttu-id="bacfe-248">예를 들어 다음과 같은 경우에 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-248">This is, for example, the case, when:</span></span>

* <span data-ttu-id="bacfe-249">활성 위험 이벤트가 있는 사용자가 삭제된 경우</span><span class="sxs-lookup"><span data-stu-id="bacfe-249">A user with Active risk events has been deleted</span></span>
* <span data-ttu-id="bacfe-250">조사 결과, 보고된 위험 이벤트가 합법적인 사용자에 의해 수행된 것으로 드러난 경우</span><span class="sxs-lookup"><span data-stu-id="bacfe-250">An investigation reveals that a reported risk event has been perform by the legitimate user</span></span>

<span data-ttu-id="bacfe-251">**활성** 상태인 위험 이벤트는 사용자 위험 계산에 사용될 수 있기 때문에 수동으로 위험 이벤트를 닫아서 위험 수준을 낮춰야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-251">Because risk events that are **Active** contribute to the user risk calculation, you may have to manually lower a risk level by closing risk events manually.</span></span>  
<span data-ttu-id="bacfe-252">조사하는 과정 동안 이러한 작업을 수행하여 위험 이벤트의 상태를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-252">During the course of investigation, you can choose to take any of these actions to change the status of a risk event:</span></span>

<span data-ttu-id="bacfe-253">![작업](./media/active-directory-identityprotection/34.png "작업")</span><span class="sxs-lookup"><span data-stu-id="bacfe-253">![Actions](./media/active-directory-identityprotection/34.png "Actions")</span></span>

* <span data-ttu-id="bacfe-254">**해결** - 위험 이벤트를 검사한 후에 ID 보호 외부에서 적절한 수정 작업을 수행하고 위험 이벤트가 닫힌 것으로 간주되어야 한다고 판단하는 경우 이벤트를 "해결됨"으로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-254">**Resolve** - If after investigating a risk event, you took an appropriate remediation action outside Identity Protection, and you believe that the risk event should be considered closed, mark the event as Resolved.</span></span> <span data-ttu-id="bacfe-255">해결된 이벤트는 위험 이벤트의 상태를 닫힘으로 설정하고 위험 이벤트는 더 이상 사용자 위험에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-255">Resolved events will set the risk event’s status to Closed and the risk event will no longer contribute to user risk.</span></span>
* <span data-ttu-id="bacfe-256">**가양성으로 표시** - 경우에 따라 위험 이벤트를 조사하여 플래그 지정이 위험으로 잘못 지정되었음을 발견할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-256">**Mark as false-positive** - In some cases, you may investigate a risk event and discover that it was incorrectly flagged as a risky.</span></span> <span data-ttu-id="bacfe-257">위험 이벤트를 가양성으로 표시하여 이러한 발생 횟수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-257">You can help reduce the number of such occurrences by marking the risk event as False-positive.</span></span> <span data-ttu-id="bacfe-258">기계 학습 알고리즘이 나중에 비슷한 이벤트를 분류하는 작업을 개선하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-258">This will help the machine learning algorithms to improve the classification of similar events in the future.</span></span> <span data-ttu-id="bacfe-259">가양성 이벤트가 **닫힘** 상태이면 더 이상 사용자 위험에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-259">The status of false-positive events is to **Closed** and they will no longer contribute to user risk.</span></span>
* <span data-ttu-id="bacfe-260">**무시** - 수정 작업을 수행하지 않지만 위험 이벤트를 활성 목록에서 제거하려면 위험 이벤트를 무시로 표시할 수 있고 이벤트 상태가 닫히게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-260">**Ignore** - If you have not taken any remediation action, but want the risk event to be removed from the active list, you can mark a risk event Ignore and the event status will be Closed.</span></span> <span data-ttu-id="bacfe-261">무시된 이벤트는 사용자 위험에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-261">Ignored events do not contribute to user risk.</span></span> <span data-ttu-id="bacfe-262">이 옵션은 이례적인 상황에서만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-262">This option should only be used under unusual circumstances.</span></span>
* <span data-ttu-id="bacfe-263">**다시 활성화** - 수동으로 종료된(**해결**, **가양성** 또는 **무시** 선택) 위험 이벤트는 이벤트 상태를 **활성**으로 다시 설정하여 다시 활성화될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-263">**Reactivate** - Risk events that were manually closed (by choosing **Resolve**, **False positive**, or **Ignore**) can be reactivated, setting the event status back to **Active**.</span></span> <span data-ttu-id="bacfe-264">다시 활성화된 위험 이벤트는 사용자 위험 수준 계산에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-264">Reactivated risk events contribute to the user risk level calculation.</span></span> <span data-ttu-id="bacfe-265">수정(예: 보안 암호를 다시 설정)을 통해 닫힌 위험 이벤트를 다시 활성화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-265">Risk events closed through remediation (such as a secure password reset) cannot be reactivated.</span></span>

<span data-ttu-id="bacfe-266">**관련 구성 대화 상자를 열려면**</span><span class="sxs-lookup"><span data-stu-id="bacfe-266">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="bacfe-267">**Azure AD ID 보호** 블레이드의 **조사** 아래에 있는 **위험 이벤트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-267">On the **Azure AD Identity Protection** blade, under **Investigate**, click **Risk events**.</span></span>

    <span data-ttu-id="bacfe-268">![암호 수동 다시 설정](./media/active-directory-identityprotection/1002.png "암호 수동 다시 설정")</span><span class="sxs-lookup"><span data-stu-id="bacfe-268">![Manual password reset](./media/active-directory-identityprotection/1002.png "Manual password reset")</span></span>
2. <span data-ttu-id="bacfe-269">**위험 이벤트** 목록에서 위험을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-269">In the **Risk events** list, click a risk.</span></span>

    <span data-ttu-id="bacfe-270">![암호 수동 다시 설정](./media/active-directory-identityprotection/1003.png "암호 수동 다시 설정")</span><span class="sxs-lookup"><span data-stu-id="bacfe-270">![Manual password reset](./media/active-directory-identityprotection/1003.png "Manual password reset")</span></span>
3. <span data-ttu-id="bacfe-271">위험 블레이드에서 사용자를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-271">On the risk blade, right-click a user.</span></span>

    <span data-ttu-id="bacfe-272">![암호 수동 다시 설정](./media/active-directory-identityprotection/1004.png "암호 수동 다시 설정")</span><span class="sxs-lookup"><span data-stu-id="bacfe-272">![Manual password reset](./media/active-directory-identityprotection/1004.png "Manual password reset")</span></span>

### <a name="closing-all-risk-events-for-a-user-manually"></a><span data-ttu-id="bacfe-273">사용자에 대한 모든 위험 이벤트를 수동으로 닫기</span><span class="sxs-lookup"><span data-stu-id="bacfe-273">Closing all risk events for a user manually</span></span>
<span data-ttu-id="bacfe-274">수동으로 사용자에 대한 위험 이벤트를 개별적으로 닫는 대신 Azure Active Directory ID 보호는 한 번의 클릭으로 사용자에 대한 모든 이벤트를 닫는 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-274">Instead of manually closing risk events for a user individually, Azure Active Directory Identity Protection also provides you with a method to close all events for a user with one click.</span></span>

<span data-ttu-id="bacfe-275">![작업](./media/active-directory-identityprotection/2222.png "작업")</span><span class="sxs-lookup"><span data-stu-id="bacfe-275">![Actions](./media/active-directory-identityprotection/2222.png "Actions")</span></span>

<span data-ttu-id="bacfe-276">**모든 이벤트 해제**를 클릭하면 모든 이벤트가 닫히고 영향을 받는 사용자가 더 이상 위험에 노출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-276">When you click **Dismiss all events**, all events are closed and the affected user is no longer at risk.</span></span>

### <a name="remediating-user-risk-events"></a><span data-ttu-id="bacfe-277">사용자 위험 이벤트 수정</span><span class="sxs-lookup"><span data-stu-id="bacfe-277">Remediating user risk events</span></span>

<span data-ttu-id="bacfe-278">수정은 이전에 손상이 우려되거나 손상된 ID 또는 장치를 보호하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-278">A remediation is an action to secure an identity or a device that was previously suspected or known to be compromised.</span></span> <span data-ttu-id="bacfe-279">수정 작업은 ID 또는 장치를 안전한 상태로 복원하고 ID 또는 장치와 연결된 이전 위험 이벤트를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-279">A remediation action restores the identity or device to a safe state, and resolves previous risk events associated with the identity or device.</span></span>

<span data-ttu-id="bacfe-280">사용자 위험 이벤트를 수정하려면 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-280">To remediate user risk events, you can:</span></span>

* <span data-ttu-id="bacfe-281">보안 암호 재설정을 수행하여 수동으로 사용자 위험 이벤트 수정</span><span class="sxs-lookup"><span data-stu-id="bacfe-281">Perform a secure password reset to remediate user risk events manually</span></span>
* <span data-ttu-id="bacfe-282">사용자 위험 보안 정책을 구성하여 자동으로 사용자 위험 이벤트 완화 또는 수정</span><span class="sxs-lookup"><span data-stu-id="bacfe-282">Configure a user risk security policy to mitigate or remediate user risk events automatically</span></span>
* <span data-ttu-id="bacfe-283">감염된 장치를 재이미징</span><span class="sxs-lookup"><span data-stu-id="bacfe-283">Re-image the infected device</span></span>  

#### <a name="manual-secure-password-reset"></a><span data-ttu-id="bacfe-284">수동으로 안전한 암호 다시 설정</span><span class="sxs-lookup"><span data-stu-id="bacfe-284">Manual secure password reset</span></span>
<span data-ttu-id="bacfe-285">안전한 암호 다시 설정은 여러 위험 이벤트를 효과적으로 수정하며 수행될 때 자동으로 이러한 위험 이벤트를 닫고 사용자 위험 수준을 다시 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-285">A secure password reset is an effective remediation for many risk events, and when performed, automatically closes these risk events and recalculates the user risk level.</span></span> <span data-ttu-id="bacfe-286">ID 보호 대시보드를 사용하여 위험한 사용자에 대한 암호 다시 설정을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-286">You can use the Identity Protection dashboard to initiate a password reset for a risky user.</span></span>

<span data-ttu-id="bacfe-287">관련 대화 상자에 암호를 다시 설정할 수 있는 두 가지 방법이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-287">The related dialog provides two different methods to reset a password:</span></span>

<span data-ttu-id="bacfe-288">**암호 다시 설정** - 사용자가 다단계 인증을 위해 등록한 경우 자체 복구할 수 있도록 하려면 **사용자가 암호를 다시 설정해야 합니다**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-288">**Reset password** - Select **Require the user to reset their password** to allow the user to self-recover if the user has registered for multi-factor authentication.</span></span> <span data-ttu-id="bacfe-289">사용자가 다음 번에 로그인하는 동안 사용자는 Multi-Factor Authentication 과제를 성공적으로 해결해야 하며 암호를 변경하도록 강제됩니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-289">During the user's next sign-in, the user will be required to solve a multi-factor authentication challenge successfully and then, forced to change the password.</span></span> <span data-ttu-id="bacfe-290">사용자 계정이 Multi-Factor Authentication에 등록되지 않은 경우 이 옵션을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-290">This option isn't available if the user account is not already registered multi-factor authentication.</span></span>

<span data-ttu-id="bacfe-291">**임시 암호** - 즉시 기존 암호를 무효화하고 사용자에 대한 새 임시 암호를 만들려면 **임시 암호 생성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-291">**Temporary password** - Select **Generate a temporary password** to immediately invalidate the existing password, and create a new temporary password for the user.</span></span> <span data-ttu-id="bacfe-292">사용자에 대한 대체 전자 메일 주소 또는 사용자의 관리자에게 새 임시 암호를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-292">Send the new temporary password to an alternate email address for the user or to the user's manager.</span></span> <span data-ttu-id="bacfe-293">암호가 임시적이기 때문에 사용자는 로그인 시 암호를 변경하라는 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-293">Because the password is temporary, the user will be prompted to change the password upon sign-in.</span></span>

<span data-ttu-id="bacfe-294">![정책](./media/active-directory-identityprotection/1005.png "정책")</span><span class="sxs-lookup"><span data-stu-id="bacfe-294">![Policy](./media/active-directory-identityprotection/1005.png "Policy")</span></span>

<span data-ttu-id="bacfe-295">**관련 구성 대화 상자를 열려면**</span><span class="sxs-lookup"><span data-stu-id="bacfe-295">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="bacfe-296">**Azure AD ID 보호** 블레이드에서 **위험 플래그가 지정된 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-296">On the **Azure AD Identity Protection** blade, click **Users flagged for risk**.</span></span>

    <span data-ttu-id="bacfe-297">![암호 수동 다시 설정](./media/active-directory-identityprotection/1006.png "암호 수동 다시 설정")</span><span class="sxs-lookup"><span data-stu-id="bacfe-297">![Manual password reset](./media/active-directory-identityprotection/1006.png "Manual password reset")</span></span>
2. <span data-ttu-id="bacfe-298">사용자 목록에서 하나 이상의 위험 이벤트와 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-298">From the list of users, select a user with at least one risk events.</span></span>

    <span data-ttu-id="bacfe-299">![암호 수동 다시 설정](./media/active-directory-identityprotection/1007.png "암호 수동 다시 설정")</span><span class="sxs-lookup"><span data-stu-id="bacfe-299">![Manual password reset](./media/active-directory-identityprotection/1007.png "Manual password reset")</span></span>
3. <span data-ttu-id="bacfe-300">사용자 블레이드에서 **암호 재설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-300">On the user blade, click **Reset password**.</span></span>

    <span data-ttu-id="bacfe-301">![암호 수동 다시 설정](./media/active-directory-identityprotection/1008.png "암호 수동 다시 설정")</span><span class="sxs-lookup"><span data-stu-id="bacfe-301">![Manual password reset](./media/active-directory-identityprotection/1008.png "Manual password reset")</span></span>

### <a name="user-risk-security-policy"></a><span data-ttu-id="bacfe-302">사용자 위험 보안 정책</span><span class="sxs-lookup"><span data-stu-id="bacfe-302">User risk security policy</span></span>
<span data-ttu-id="bacfe-303">사용자 위험 보안 정책은 특정 사용자에 대한 위험 수준을 평가하고 미리 정의된 조건 및 규칙에 따라 수정 및 완화 작업을 적용하는 조건부 액세스 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-303">A user risk security policy is a conditional access policy that evaluates the risk level to a specific user and applies remediation and mitigation actions based on predefined conditions and rules.</span></span>

<span data-ttu-id="bacfe-304">![사용자 위험 정책](./media/active-directory-identityprotection/1009.png "사용자 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="bacfe-304">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

<span data-ttu-id="bacfe-305">Azure AD ID 보호를 사용하면 다음을 사용하여 위험에 플래그가 지정된 사용자의 완화 및 수정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-305">Azure AD Identity Protection helps you manage the mitigation and remediation of users flagged for risk by enabling you to:</span></span>

* <span data-ttu-id="bacfe-306">정책이 적용되는 사용자 및 그룹 설정:</span><span class="sxs-lookup"><span data-stu-id="bacfe-306">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="bacfe-307">![사용자 위험 정책](./media/active-directory-identityprotection/1010.png "사용자 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="bacfe-307">![User ridk policy](./media/active-directory-identityprotection/1010.png "User ridk policy")</span></span>
* <span data-ttu-id="bacfe-308">정책을 트리거하는 사용자 위험 수준 임계값 설정(낮음, 보통 또는 높음):</span><span class="sxs-lookup"><span data-stu-id="bacfe-308">Set the user risk level threshold (low, medium, or high) that triggers the policy:</span></span>

    <span data-ttu-id="bacfe-309">![사용자 위험 정책](./media/active-directory-identityprotection/1011.png "사용자 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="bacfe-309">![User ridk policy](./media/active-directory-identityprotection/1011.png "User ridk policy")</span></span>
* <span data-ttu-id="bacfe-310">정책이 트리거할 때 적용될 컨트롤 설정:</span><span class="sxs-lookup"><span data-stu-id="bacfe-310">Set the controls to be enforced when the policy triggers:</span></span>

    <span data-ttu-id="bacfe-311">![사용자 위험 정책](./media/active-directory-identityprotection/1012.png "사용자 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="bacfe-311">![User ridk policy](./media/active-directory-identityprotection/1012.png "User ridk policy")</span></span>
* <span data-ttu-id="bacfe-312">정책 상태 전환:</span><span class="sxs-lookup"><span data-stu-id="bacfe-312">Switch the state of your policy:</span></span>

    <span data-ttu-id="bacfe-313">![사용자 위험 정책](./media/active-directory-identityprotection/403.png "MFA 등록")</span><span class="sxs-lookup"><span data-stu-id="bacfe-313">![User ridk policy](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="bacfe-314">활성화하기 전에 변경의 영향 검토 및 평가:</span><span class="sxs-lookup"><span data-stu-id="bacfe-314">Review and evaluate the impact of a change before activating it:</span></span>

    <span data-ttu-id="bacfe-315">![사용자 위험 정책](./media/active-directory-identityprotection/1013.png "사용자 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="bacfe-315">![User ridk policy](./media/active-directory-identityprotection/1013.png "User ridk policy")</span></span>

<span data-ttu-id="bacfe-316">**높음** 임계값을 선택하면 정책이 트리거되는 횟수를 줄이고 사용자에게 미치는 영향을 최소화합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-316">Choosing a **High** threshold reduces the number of times a policy is triggered and minimizes the impact to users.</span></span>
<span data-ttu-id="bacfe-317">그러나 정책에서 위험 플래그가 지정된 **낮음** 및 **보통** 사용자를 제외하며, 이는 이전에 손상이 의심되거나 손상된 것으로 확인된 ID 또는 장치를 보호하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-317">However, it excludes **Low** and **Medium** users flagged for risk from the policy, which may not secure identities or devices that were previously suspected or known to be compromised.</span></span>

<span data-ttu-id="bacfe-318">정책을 설정 하는 경우</span><span class="sxs-lookup"><span data-stu-id="bacfe-318">When setting the policy,</span></span>

* <span data-ttu-id="bacfe-319">많은 가양성(개발자, 보안 분석가)을 생성할 수 있는 사용자를 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-319">Exclude users who are likely to generate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="bacfe-320">정책을 사용하지 않는 것이 실용적이지 않은 로캘에서 사용자를 제외합니다(예: 기술 지원팀에 액세스 권한 없음).</span><span class="sxs-lookup"><span data-stu-id="bacfe-320">Exclude users in locales where enabling the policy is not practical (for example no access to helpdesk)</span></span>
* <span data-ttu-id="bacfe-321">초기 정책이 롤아웃하는 동안 또는 최종 사용자가 확인하는 과제를 최소화해야 하는 경우 **높음** 임계값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-321">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="bacfe-322">조직이 보안을 강화해야 하는 경우 **낮음** 임계값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-322">Use a **Low** threshold if your organization requires greater security.</span></span> <span data-ttu-id="bacfe-323">**낮은** 임계값을 선택하면 추가 사용자 로그인 과제가 발생하지만 보안이 강화됩니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-323">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="bacfe-324">대부분의 조직에 권장되는 기본값은 **보통** 임계값에 대한 규칙을 구성하여 유용성과 보안 간의 균형을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-324">The recommended default for most organizations is to configure a rule for a **Medium** threshold to strike a balance between usability and security.</span></span>

<span data-ttu-id="bacfe-325">관련 사용자 환경에 대한 개요는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bacfe-325">For an overview of the related user experience, see:</span></span>

* <span data-ttu-id="bacfe-326">[손상된 계정 복구 흐름](active-directory-identityprotection-flows.md#compromised-account-recovery)</span><span class="sxs-lookup"><span data-stu-id="bacfe-326">[Compromised account recovery flow](active-directory-identityprotection-flows.md#compromised-account-recovery).</span></span>  
* <span data-ttu-id="bacfe-327">[손상된 계정 차단됨 흐름](active-directory-identityprotection-flows.md#compromised-account-blocked)</span><span class="sxs-lookup"><span data-stu-id="bacfe-327">[Compromised account blocked flow](active-directory-identityprotection-flows.md#compromised-account-blocked).</span></span>  

<span data-ttu-id="bacfe-328">**관련 구성 대화 상자를 열려면**</span><span class="sxs-lookup"><span data-stu-id="bacfe-328">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="bacfe-329">**Azure AD ID 보호** 블레이드의 **구성** 섹션에서 **사용자 위험 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-329">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **User risk policy**.</span></span>

    <span data-ttu-id="bacfe-330">![사용자 위험 정책](./media/active-directory-identityprotection/1009.png "사용자 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="bacfe-330">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

### <a name="mitigating-user-risk-events"></a><span data-ttu-id="bacfe-331">사용자 위험 이벤트 완화</span><span class="sxs-lookup"><span data-stu-id="bacfe-331">Mitigating user risk events</span></span>
<span data-ttu-id="bacfe-332">관리자는 사용자 위험 보안 정책을 설정하여 위험 수준에 따라 로그인 시 사용자를 차단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-332">Administrators can set a user risk security policy to block users upon sign-in depending on the risk level.</span></span>

<span data-ttu-id="bacfe-333">로그인 차단:</span><span class="sxs-lookup"><span data-stu-id="bacfe-333">Blocking a sign-in:</span></span>

* <span data-ttu-id="bacfe-334">영향을 받는 사용자에 대한 새 사용자 위험 이벤트의 생성 방지</span><span class="sxs-lookup"><span data-stu-id="bacfe-334">Prevents the generation of new user risk events for the affected user</span></span>
* <span data-ttu-id="bacfe-335">관리자가 사용자의 ID에 영향을 주는 위험 이벤트를 수동으로 수정하고 안전한 상태로 복원할 수 있음</span><span class="sxs-lookup"><span data-stu-id="bacfe-335">Enables administrators to manually remediate the risk events affecting the user's identity and restore it to a secure state</span></span>



## <a name="multi-factor-authentication-registration-policy"></a><span data-ttu-id="bacfe-336">Multi-Factor Authentication 등록 정책</span><span class="sxs-lookup"><span data-stu-id="bacfe-336">Multi-factor authentication registration policy</span></span>
<span data-ttu-id="bacfe-337">Azure Multi-Factor Authentication은 사용자 이름 및 암호 이외의 다른 내용을 사용해야 하는 사람인지를 확인하는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-337">Azure multi-factor authentication is a method of verifying who you are that requires the use of more than just a username and password.</span></span> <span data-ttu-id="bacfe-338">사용자 로그인 및 트랜잭션에 대한 보안의 두 번째 계층을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-338">It provides a second layer of security to user sign-ins and transactions.</span></span>  
<span data-ttu-id="bacfe-339">다음과 같은 이유로, 사용자 로그인에 Azure Multi-Factor Authentication을 요구하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-339">We recommend that you require Azure multi-factor authentication for user sign-ins because it:</span></span>

* <span data-ttu-id="bacfe-340">다양한 간편한 확인 옵션과 함께 강력한 인증 제공</span><span class="sxs-lookup"><span data-stu-id="bacfe-340">Delivers strong authentication with a range of easy verification options</span></span>
* <span data-ttu-id="bacfe-341">조직에서 계정 손상을 방지 및 복구하도록 준비하는 데 중요한 역할 수행</span><span class="sxs-lookup"><span data-stu-id="bacfe-341">Plays a key role in preparing your organization to protect and recover from account compromises</span></span>

<span data-ttu-id="bacfe-342">![사용자 위험 정책](./media/active-directory-identityprotection/1019.png "사용자 위험 정책")</span><span class="sxs-lookup"><span data-stu-id="bacfe-342">![User ridk policy](./media/active-directory-identityprotection/1019.png "User ridk policy")</span></span>

<span data-ttu-id="bacfe-343">자세한 내용은 [Azure Multi-Factor Authentication 정의](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="bacfe-343">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

<span data-ttu-id="bacfe-344">Azure AD ID 보호를 사용하면 다음을 지원하는 정책을 구성하여 Multi-Factor Authentication 등록의 롤아웃을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-344">Azure AD Identity Protection helps you manage the roll-out of multi-factor authentication registration by configuring a policy that enables you to:</span></span>

* <span data-ttu-id="bacfe-345">정책이 적용되는 사용자 및 그룹 설정:</span><span class="sxs-lookup"><span data-stu-id="bacfe-345">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="bacfe-346">![MFA 정책](./media/active-directory-identityprotection/1020.png "MFA 정책")</span><span class="sxs-lookup"><span data-stu-id="bacfe-346">![MFA policy](./media/active-directory-identityprotection/1020.png "MFA policy")</span></span>
* <span data-ttu-id="bacfe-347">정책이 트리거할 때 적용될 컨트롤 설정:</span><span class="sxs-lookup"><span data-stu-id="bacfe-347">Set the controls to be enforced when the policy triggers::</span></span>  

    <span data-ttu-id="bacfe-348">![MFA 정책](./media/active-directory-identityprotection/1021.png "MFA 정책")</span><span class="sxs-lookup"><span data-stu-id="bacfe-348">![MFA policy](./media/active-directory-identityprotection/1021.png "MFA policy")</span></span>
* <span data-ttu-id="bacfe-349">정책 상태 전환:</span><span class="sxs-lookup"><span data-stu-id="bacfe-349">Switch the state of your policy:</span></span>

    <span data-ttu-id="bacfe-350">![MFA 정책](./media/active-directory-identityprotection/403.png "MFA 정책")</span><span class="sxs-lookup"><span data-stu-id="bacfe-350">![MFA policy](./media/active-directory-identityprotection/403.png "MFA policy")</span></span>
* <span data-ttu-id="bacfe-351">현재 등록 상태 보기:</span><span class="sxs-lookup"><span data-stu-id="bacfe-351">View the current registration status:</span></span>

    <span data-ttu-id="bacfe-352">![MFA 정책](./media/active-directory-identityprotection/1022.png "MFA 정책")</span><span class="sxs-lookup"><span data-stu-id="bacfe-352">![MFA policy](./media/active-directory-identityprotection/1022.png "MFA policy")</span></span>

<span data-ttu-id="bacfe-353">관련 사용자 환경에 대한 개요는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bacfe-353">For an overview of the related user experience, see:</span></span>

* <span data-ttu-id="bacfe-354">[Multi-Factor Authentication 등록 흐름](active-directory-identityprotection-flows.md#multi-factor-authentication-registration)</span><span class="sxs-lookup"><span data-stu-id="bacfe-354">[Multi-factor authentication registration flow](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span></span>  
* <span data-ttu-id="bacfe-355">[Azure AD ID 보호를 사용하는 로그인 환경](active-directory-identityprotection-flows.md)</span><span class="sxs-lookup"><span data-stu-id="bacfe-355">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span></span>  

<span data-ttu-id="bacfe-356">**관련 구성 대화 상자를 열려면**</span><span class="sxs-lookup"><span data-stu-id="bacfe-356">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="bacfe-357">**Azure AD ID 보호** 블레이드의 **구성** 섹션에서 **다단계 인증 등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bacfe-357">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **Multi-factor authentication registration**.</span></span>

    <span data-ttu-id="bacfe-358">![MFA 정책](./media/active-directory-identityprotection/1019.png "MFA 정책")</span><span class="sxs-lookup"><span data-stu-id="bacfe-358">![MFA policy](./media/active-directory-identityprotection/1019.png "MFA policy")</span></span>

## <a name="next-steps"></a><span data-ttu-id="bacfe-359">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bacfe-359">Next steps</span></span>
* [<span data-ttu-id="bacfe-360">Channel 9: Azure AD 및 ID 표시: ID 보호 미리 보기</span><span class="sxs-lookup"><span data-stu-id="bacfe-360">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span></span>](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [<span data-ttu-id="bacfe-361">Azure Active Directory ID 보호 활성화</span><span class="sxs-lookup"><span data-stu-id="bacfe-361">Enabling Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-enable.md)

* [<span data-ttu-id="bacfe-362">Azure Active Directory ID 보호에서 검색하는 취약성</span><span class="sxs-lookup"><span data-stu-id="bacfe-362">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-vulnerabilities.md)

* [<span data-ttu-id="bacfe-363">Azure Active Directory 위험 이벤트</span><span class="sxs-lookup"><span data-stu-id="bacfe-363">Azure Active Directory risk events</span></span>](active-directory-identity-protection-risk-events.md)

* [<span data-ttu-id="bacfe-364">Azure Active Directory ID 보호 알림</span><span class="sxs-lookup"><span data-stu-id="bacfe-364">Azure Active Directory Identity Protection notifications</span></span>](active-directory-identityprotection-notifications.md)

* [<span data-ttu-id="bacfe-365">Azure Active Directory ID 보호 플레이 북</span><span class="sxs-lookup"><span data-stu-id="bacfe-365">Azure Active Directory Identity Protection playbook</span></span>](active-directory-identityprotection-playbook.md)

* [<span data-ttu-id="bacfe-366">Azure Active Directory ID 보호 용어집</span><span class="sxs-lookup"><span data-stu-id="bacfe-366">Azure Active Directory Identity Protection glossary</span></span>](active-directory-identityprotection-glossary.md)

* [<span data-ttu-id="bacfe-367">Azure AD ID 보호를 사용하는 로그인 환경</span><span class="sxs-lookup"><span data-stu-id="bacfe-367">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)

* [<span data-ttu-id="bacfe-368">Azure Active Directory ID 보호 - 사용자를 차단 해제하는 방법</span><span class="sxs-lookup"><span data-stu-id="bacfe-368">Azure Active Directory Identity Protection - How to unblock users</span></span>](active-directory-identityprotection-unblock-howto.md)

* [<span data-ttu-id="bacfe-369">Azure Active Directory ID 보호 및 Microsoft Graph 시작</span><span class="sxs-lookup"><span data-stu-id="bacfe-369">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>](active-directory-identityprotection-graph-getting-started.md)
