---
title: "Azure Active Directory ID 보호 용어집 | Microsoft Docs"
description: "Azure Active Directory ID 보호 용어집"
services: active-directory
keywords: "Azure Active Directory ID 보호, Cloud App Discovery, 응용 프로그램 관리, 보안, 위험, 위험 수준, 취약성, 보안 정책, 용어집"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 833119a5-33d6-4482-adda-fa35218c72c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 2cf64925cff9a78cf83532a1cfd231f7a1d98304
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-glossary"></a><span data-ttu-id="69bf9-104">Azure Active Directory ID 보호 용어집</span><span class="sxs-lookup"><span data-stu-id="69bf9-104">Azure Active Directory Identity Protection Glossary</span></span>
### <a name="at-risk-user"></a><span data-ttu-id="69bf9-105">위험(사용자)</span><span class="sxs-lookup"><span data-stu-id="69bf9-105">At risk (User)</span></span>
<span data-ttu-id="69bf9-106">하나 이상의 활성 위험 이벤트가 있는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-106">A user with one or more active risk events.</span></span> 

### <a name="atypical-sign-in-location"></a><span data-ttu-id="69bf9-107">비정상적인 로그인 위치</span><span class="sxs-lookup"><span data-stu-id="69bf9-107">Atypical sign-in location</span></span>
<span data-ttu-id="69bf9-108">특정 사용자, 비슷한 사용자 또는 테넌트에 일반적이지 않은 지리적 위치에서 시도하는 로그인입니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-108">A sign-in from a geographic location that is not typical for the specific user, similar users, or the tenant.</span></span>

### <a name="azure-ad-identity-protection"></a><span data-ttu-id="69bf9-109">Azure AD ID 보호</span><span class="sxs-lookup"><span data-stu-id="69bf9-109">Azure AD Identity Protection</span></span>
<span data-ttu-id="69bf9-110">조직의 ID에 영향을 주는 위험 이벤트와 잠재적 취약성에 대한 통합된 뷰를 제공하는 Azure Active Directory의 보안 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-110">A security module of Azure Active Directory that provides a consolidated view into risk events and potential vulnerabilities affecting an organization’s identities.</span></span>

### <a name="conditional-access"></a><span data-ttu-id="69bf9-111">조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="69bf9-111">Conditional access</span></span>
<span data-ttu-id="69bf9-112">리소스에 대한 액세스를 보호하는 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-112">A policy for securing access to resources.</span></span> <span data-ttu-id="69bf9-113">조건부 액세스 규칙은 Azure Active Directory에 저장되고 리소스에 대한 액세스 권한을 부여하기 전에 Azure AD에서 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-113">Conditional access rules are stored in the Azure Active Directory and are evaluated by Azure AD before granting access to the resource.</span></span>  <span data-ttu-id="69bf9-114">예제 규칙은 사용자 위치, 장치 상태 또는 사용자 인증 방법에 따라 액세스를 제한하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-114">Example rules include restricting access based on user location, device health or user authentication method.</span></span>

### <a name="credentials"></a><span data-ttu-id="69bf9-115">자격 증명</span><span class="sxs-lookup"><span data-stu-id="69bf9-115">Credentials</span></span>
<span data-ttu-id="69bf9-116">로컬 및 네트워크 리소스에 대한 액세스 권한을 얻는 데 사용되는 ID 및 ID의 증명을 포함하는 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-116">Information that includes identification and proof of identification that is used to gain access to local and network resources.</span></span> <span data-ttu-id="69bf9-117">자격 증명의 예는 사용자 이름 및 암호, 스마트 카드 및 인증서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-117">Examples of credentials are user names and passwords, smart cards, and certificates.</span></span>

### <a name="event"></a><span data-ttu-id="69bf9-118">이벤트</span><span class="sxs-lookup"><span data-stu-id="69bf9-118">Event</span></span>
<span data-ttu-id="69bf9-119">Azure Active Directory에서 작업의 기록입니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-119">A record of an activity in Azure Active Directory.</span></span>

### <a name="false-positive-risk-event"></a><span data-ttu-id="69bf9-120">가양성(위험 이벤트)</span><span class="sxs-lookup"><span data-stu-id="69bf9-120">False-positive (risk event)</span></span>
<span data-ttu-id="69bf9-121">위험 이벤트 상태는 ID 보호 사용자가 수동으로 설정하며 위험 이벤트를 조사하여 위험 이벤트로 플래그가 잘못 지정되었다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-121">A risk event status set manually by an Identity Protection user, indicating that the risk event was investigated and was incorrectly flagged as a risk event.</span></span>

### <a name="identity"></a><span data-ttu-id="69bf9-122">ID</span><span class="sxs-lookup"><span data-stu-id="69bf9-122">Identity</span></span>
<span data-ttu-id="69bf9-123">암호 또는 인증서와 같은 조건에 따라 인증이라는 방법으로 확인되어야 하는 개인 및 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-123">A person or entity that must be verified by means of authentication, based on criteria such as password or a certificate.</span></span>

### <a name="identity-risk-event"></a><span data-ttu-id="69bf9-124">ID 위험 이벤트</span><span class="sxs-lookup"><span data-stu-id="69bf9-124">Identity risk event</span></span>
<span data-ttu-id="69bf9-125">ID 보호에서 비정상으로 플래그가 지정되고 ID가 손상되었음을 나타낼 수 있는 AAD 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-125">AAD event that was flagged as anomalous by Identity Protection, and may indicate that an identity has been compromised.</span></span>

### <a name="ignored-risk-event"></a><span data-ttu-id="69bf9-126">무시된(위험 이벤트)</span><span class="sxs-lookup"><span data-stu-id="69bf9-126">Ignored (risk event)</span></span>
<span data-ttu-id="69bf9-127">위험 이벤트가 수정 작업을 수행하지 않고 닫혀 있음을 나타내는 ID 보호 사용자가 수동으로 설정한 위험 이벤트 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-127">A risk event status set manually by an Identity Protection user, indicating that the risk event is closed without taking a remediation action.</span></span>

### <a name="impossible-travel-from-atypical-locations"></a><span data-ttu-id="69bf9-128">비정상적 위치에서 불가능한 이동</span><span class="sxs-lookup"><span data-stu-id="69bf9-128">Impossible travel from atypical locations</span></span>
<span data-ttu-id="69bf9-129">동일한 사용자에 대한 두 개의 로그인이 감지되는 경우, 하나 이상이 비정상적인 로그인 위치에서 비롯되고 두 로그인 간의 시간이 이러한 위치 간의 물리적인 이동에 걸리는 시간보다 짧으면 트리거되는 위험 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-129">A risk event triggered when two sign-ins for the same user are detected, where at least one of them is from an atypical sign-in location, and where the time between the sign-ins is shorter than the minimum time it would take to physically travel between these locations.</span></span>  

### <a name="investigation"></a><span data-ttu-id="69bf9-130">조사</span><span class="sxs-lookup"><span data-stu-id="69bf9-130">Investigation</span></span>
<span data-ttu-id="69bf9-131">수정 또는 완화 단계가 필요한지를 결정하고 ID가 어떻게 손상되었고 손상된 ID가 어떻게 사용되었는지를 이해하기 위해 활동, 로그 및 위험 이벤트와 관련된 위험 기타 관련 정보를 검토하는 과정입니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-131">The process of reviewing the activities, logs, and other relevant information related to a risk event to decide whether remediation or mitigation steps are necessary, understand if and how the identity was compromised, and understand how the compromised identity was used.</span></span>

### <a name="leaked-credentials"></a><span data-ttu-id="69bf9-132">유출된 자격 증명</span><span class="sxs-lookup"><span data-stu-id="69bf9-132">Leaked credentials</span></span>
<span data-ttu-id="69bf9-133">연구원이 Dark 웹에 공개적으로 게시하여 현재 사용자 자격 증명(사용자 이름 및 암호)가 발견된 경우 트리거되는 위험 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-133">A risk event triggered when current user credentials (user name and password) are found posted publicly in the Dark   web by our researchers.</span></span>

### <a name="mitigation"></a><span data-ttu-id="69bf9-134">해결 방법</span><span class="sxs-lookup"><span data-stu-id="69bf9-134">Mitigation</span></span>
<span data-ttu-id="69bf9-135">ID 또는 장치를 안전한 상태로 복원하지 않고 공격자의 능력을 제한하거나 제거하여 공격에 노출된 ID 또는 장치를 악용하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-135">An action to limit or eliminate the ability of an attacker to exploit a compromised identity or device without restoring the identity or device to a safe state.</span></span> <span data-ttu-id="69bf9-136">완화 조치는 ID 또는 장치와 연결된 이전 위험 이벤트를 확인하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-136">A mitigation does not resolve previous risk events associated with the identity or device.</span></span>

### <a name="multi-factor-authentication"></a><span data-ttu-id="69bf9-137">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="69bf9-137">Multi-factor authentication</span></span>
<span data-ttu-id="69bf9-138">인증서 등 사용자가 가진 정보를 포함하는 두 개 이상의 인증 방법이 필요한 인증 방법입니다. 사용자 이름, 암호 또는 암호 문구 등 사용자가 아는 정보 혹은 지문 등 물리적 특성 및 개인 서명 등 개인 특성일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-138">An authentication method that requires two or more authentication methods, which may include something the user has, such a certificate; something the user knows, such as user names, passwords, or pass phrases; physical attributes, such as a thumbprint; and personal attributes, such as a personal signature.</span></span>

### <a name="offline-detection"></a><span data-ttu-id="69bf9-139">오프라인 검색</span><span class="sxs-lookup"><span data-stu-id="69bf9-139">Offline detection</span></span>
<span data-ttu-id="69bf9-140">잘못된 부분을 감지하고 이미 발생한 이벤트에 대한 사후 로그인 시도와 같은 이벤트의 위험을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-140">The detection of anomalies and evaluation of the risk of an event such as sign-in attempt after the fact, for an event that has already happened.</span></span>

### <a name="policy-condition"></a><span data-ttu-id="69bf9-141">정책 조건</span><span class="sxs-lookup"><span data-stu-id="69bf9-141">Policy condition</span></span>
<span data-ttu-id="69bf9-142">엔터티(그룹, 사용자, 앱, 장치 플랫폼, 장치 상태, IP 범위, 클라이언트 형식)를 정의하는 보안 정책의 일부는 정책에 포함되었거나 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-142">A part of a security policy which defines the entities (groups, users, apps, device platforms, Device states, IP ranges, client types) included in the policy or excluded from it.</span></span>

### <a name="policy-rule"></a><span data-ttu-id="69bf9-143">정책 규칙</span><span class="sxs-lookup"><span data-stu-id="69bf9-143">Policy rule</span></span>
<span data-ttu-id="69bf9-144">정책을 트리거하는 상황 및 정책이 트리거될 때 수행된 작업을 설명하는 보안 정책의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-144">The part of a security policy which describes the circumstances that would trigger the policy, and the actions taken when the policy is triggered.</span></span>

### <a name="prevention"></a><span data-ttu-id="69bf9-145">방지</span><span class="sxs-lookup"><span data-stu-id="69bf9-145">Prevention</span></span>
<span data-ttu-id="69bf9-146">손상이 우려되거나 손상된 ID 또는 장치를 남용하여 조직에 대한 손상을 방지하는 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-146">An action to prevent damage to the organization through abuse of an identity or device suspected or know to be compromised.</span></span> <span data-ttu-id="69bf9-147">예방 조치는 장치 또는 ID를 보호하지 않고 이전 위험 이벤트를 해결하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-147">A prevention action does not secure the device or identity, and does not resolve previous risk events.</span></span>

### <a name="privileged-user"></a><span data-ttu-id="69bf9-148">권한 있는(사용자)</span><span class="sxs-lookup"><span data-stu-id="69bf9-148">Privileged (user)</span></span>
<span data-ttu-id="69bf9-149">위험 이벤트가 발생한 경우 사용자는 전역 관리자, 대금 청구 관리자, 서비스 관리자, 사용자 관리자 및 암호 관리자와 같은 Azure Active Directory에서 하나 이상의 리소스에 대한 영구 또는 임시 관리자 권한을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-149">A user that at the time of a risk event, had permanent or temporary admin permissions to one or more resource in Azure Active Directory, such as a Global Administrator, Billing Administrator, Service Administrator, User administrator, and Password Administrator.</span></span> 

### <a name="real-time"></a><span data-ttu-id="69bf9-150">실시간</span><span class="sxs-lookup"><span data-stu-id="69bf9-150">Real-time</span></span>
<span data-ttu-id="69bf9-151">실시간 탐지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69bf9-151">See Real-time detection.</span></span>

### <a name="real-time-detection"></a><span data-ttu-id="69bf9-152">실시간 탐지</span><span class="sxs-lookup"><span data-stu-id="69bf9-152">Real-time detection</span></span>
<span data-ttu-id="69bf9-153">잘못된 부분을 감지하고 이미 발생한 이벤트에 대한 이벤트를 진행하기 전에 로그인 시도와 같은 이벤트의 위험을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-153">The detection of anomalies and evaluation of the risk of an event such as sign-in attempt before the event is allowed to proceed.</span></span>

### <a name="remediated-risk-event"></a><span data-ttu-id="69bf9-154">수정된(위험 이벤트)</span><span class="sxs-lookup"><span data-stu-id="69bf9-154">Remediated (risk event)</span></span>
<span data-ttu-id="69bf9-155">위험 이벤트 상태는 ID 보호에서 자동으로 설정되며 위험 이벤트가 이러한 유형의 위험 이벤트에 대한 표준 수정 작업을 사용하여 수정된다는 점을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-155">A risk event status set automatically by Identity Protection, indicating that the risk event was remediated using the standard remediation action for this type of risk event.</span></span> <span data-ttu-id="69bf9-156">예를 들어, 사용자 암호가 다시 설정되면 이전 암호가 손상되었음을 나타내는 많은 위험 이벤트가 자동으로 수정됩니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-156">For example, when the user password is reset, many risk events that indicate that the previous password was compromised are automatically remediated.</span></span>

### <a name="remediation"></a><span data-ttu-id="69bf9-157">재구성</span><span class="sxs-lookup"><span data-stu-id="69bf9-157">Remediation</span></span>
<span data-ttu-id="69bf9-158">이전에 손상이 우려되거나 손상된 ID 또는 장치를 보호하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-158">An action to secure an identity or a device that were previously suspected or known to be compromised.</span></span> <span data-ttu-id="69bf9-159">수정 작업은 ID 또는 장치를 안전한 상태로 복원하고 ID 또는 장치와 연결된 이전 위험 이벤트를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-159">A remediation action restores the identity or device to a safe state, and resolves previous risk events associated with the identity or device.</span></span>

### <a name="resolved-risk-event"></a><span data-ttu-id="69bf9-160">확인된(위험 이벤트)</span><span class="sxs-lookup"><span data-stu-id="69bf9-160">Resolved (risk event)</span></span>
<span data-ttu-id="69bf9-161">사용자가 ID 보호 외부에서 적절한 수정 작업을 수행했으며 위험 이벤트가 닫힌 것으로 간주되어야 한다는 점을 나타내며 ID 보호 사용자가 수동으로 설정한 위험 이벤트 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-161">A risk event status set manually by an Identity Protection user, indicating that the user took an appropriate remediation action outside Identity Protection, and that the risk event should be considered closed.</span></span>

### <a name="risk-event-status"></a><span data-ttu-id="69bf9-162">위험 이벤트 상태</span><span class="sxs-lookup"><span data-stu-id="69bf9-162">Risk event status</span></span>
<span data-ttu-id="69bf9-163">이벤트가 활성 상태인지, 닫힌 경우 이유가 무엇인지를 나타내는 위험 이벤트의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-163">A property of a risk event, indicating whether the event is active, and if closed, the reason for closing it.</span></span>

### <a name="risk-event-type"></a><span data-ttu-id="69bf9-164">위험 이벤트 유형</span><span class="sxs-lookup"><span data-stu-id="69bf9-164">Risk event type</span></span>
<span data-ttu-id="69bf9-165">위험한 것으로 간주되는 이벤트를 발생시킨 비정상의 유형을 나타내는 위험 이벤트에 대한 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-165">A category for the risk event, indicating the type of anomaly that caused the event to be considered risky.</span></span>

### <a name="risk-level-risk-event"></a><span data-ttu-id="69bf9-166">위험 수준(위험 이벤트)</span><span class="sxs-lookup"><span data-stu-id="69bf9-166">Risk level (risk event)</span></span>
<span data-ttu-id="69bf9-167">ID 보호 사용자가 조직에 대한 위험을 줄이기 위해 수행하는 동작을 우선하도록 하는 위험 이벤트의 심각도를 표시(높음, 중간 또는 낮음)합니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-167">An indication (High, Medium, or Low) of the severity of the risk event to help Identity Protection users prioritize the actions they take to reduce the risk to their organization.</span></span> 

### <a name="risk-level-sign-in"></a><span data-ttu-id="69bf9-168">위험 수준(로그인)</span><span class="sxs-lookup"><span data-stu-id="69bf9-168">Risk level (sign-in)</span></span>
<span data-ttu-id="69bf9-169">사용자의 ID를 사용하려는 다른 사용자라는 특정 로그인에 대한 가능성을 표시(높음, 중간 또는 낮음)합니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-169">An indication (High, Medium, or Low) of the likelihood that for a specific sign-in, someone else is attempting to use the user’s identity.</span></span>

### <a name="risk-level-user-compromise"></a><span data-ttu-id="69bf9-170">위험 수준(사용자 손상)</span><span class="sxs-lookup"><span data-stu-id="69bf9-170">Risk level (user compromise)</span></span>
<span data-ttu-id="69bf9-171">ID가 손상된 가능성을 표시(높음, 중간 또는 낮음)합니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-171">An indication (High, Medium, or Low) of the likelihood that an identity has been compromised.</span></span>

### <a name="risk-level-vulnerability"></a><span data-ttu-id="69bf9-172">위험 수준(취약점)</span><span class="sxs-lookup"><span data-stu-id="69bf9-172">Risk level (vulnerability)</span></span>
<span data-ttu-id="69bf9-173">ID 보호 사용자가 조직에 대한 위험을 줄이기 위해 수행하는 동작을 우선하도록 하는 취약점의 심각도를 표시(높음, 중간 또는 낮음)합니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-173">An indication (High, Medium, or Low) of the severity of the vulnerability to help Identity Protection users prioritize the actions they take to reduce the risk to their organization.</span></span>

### <a name="secure-identity"></a><span data-ttu-id="69bf9-174">보안(ID)</span><span class="sxs-lookup"><span data-stu-id="69bf9-174">Secure (identity)</span></span>
<span data-ttu-id="69bf9-175">잠재적으로 노출된 ID를 비교할 수 없는 상태로 복원하기 위해 이미지로 다시 설치한 암호 변경 또는 컴퓨터와 같은 수정 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-175">Take remediation action such as a password change or machine reimaging to restore a potentially compromised identity to an uncompromised state.</span></span>

### <a name="security-policy"></a><span data-ttu-id="69bf9-176">보안 정책</span><span class="sxs-lookup"><span data-stu-id="69bf9-176">Security policy</span></span>
<span data-ttu-id="69bf9-177">정책 규칙 및 조건의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-177">A collection of policy rules and condition.</span></span> <span data-ttu-id="69bf9-178">사용자, 그룹, 앱, 장치, 장치 플랫폼, 장치 상태, IP 범위 및 Auth2.0 클라이언트 유형과 같은 엔터티에 정책을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-178">A policy can be applied to entities such as users, groups, apps, devices, device platforms, device states, IP ranges, and Auth2.0 client types.</span></span> <span data-ttu-id="69bf9-179">정책을 사용하는 경우 정책에 포함된 엔터티가 리소스에 토큰을 발급할 때마다 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-179">When a policy is enabled, it is evaluated whenever an entity included in the policy is issued a token for a resource.</span></span>

### <a name="sign-in-v"></a><span data-ttu-id="69bf9-180">로그인(v)</span><span class="sxs-lookup"><span data-stu-id="69bf9-180">Sign in (v)</span></span>
<span data-ttu-id="69bf9-181">Azure Active Directory의 ID를 인증하려면.</span><span class="sxs-lookup"><span data-stu-id="69bf9-181">To authenticate to an identity in Azure Active Directory.</span></span>

### <a name="sign-in-n"></a><span data-ttu-id="69bf9-182">로그인(n)</span><span class="sxs-lookup"><span data-stu-id="69bf9-182">Sign-in (n)</span></span>
<span data-ttu-id="69bf9-183">Azure Active Directory에서 ID를 인증하는 프로세스 또는 동작이며 이 작업을 캡처하는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-183">The process or action of authenticating an identity in Azure Active Directory, and the event that captures this operation.</span></span>

### <a name="sign-in-from-anonymous-ip-address"></a><span data-ttu-id="69bf9-184">익명 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="69bf9-184">Sign-in from anonymous IP address</span></span>
<span data-ttu-id="69bf9-185">익명 프록시 IP 주소로 식별된 IP 주소에서 성공적인 로그인 후에 트리거된 위험 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-185">A risk event triggered after a successful sign-in from IP address that has been identified as an anonymous proxy IP address.</span></span>

### <a name="sign-in-from-infected-device"></a><span data-ttu-id="69bf9-186">감염된 장치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="69bf9-186">Sign-in from infected device</span></span>
<span data-ttu-id="69bf9-187">하나 이상의 손상된 장치에서 사용된다고 알려진 IP 주소에서 로그인이 시작되는 경우 트리거된 위험 이벤트는 봇 서버와 적극적으로 통신하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-187">A risk event triggered when a sign-in originates from an IP address which is known to be used by one or more compromised devices, which are actively attempting to communicate with a bot server.</span></span>

### <a name="sign-in-from-ip-address-with-suspicious-activity"></a><span data-ttu-id="69bf9-188">의심스러운 동작으로 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="69bf9-188">Sign-in from IP address with suspicious activity</span></span>
<span data-ttu-id="69bf9-189">짧은 기간 동안 여러 사용자 계정에서 여러 번 실패한 로그인을 시도한 IP 주소의 성공적인 로그인 후에 트리거된 위험 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-189">A risk event triggered after a successful sign-in from an IP address with a high number of failed login attempts across multiple user accounts over a short period of time.</span></span>

### <a name="sign-in-from-unfamiliar-location"></a><span data-ttu-id="69bf9-190">알 수 없는 위치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="69bf9-190">Sign-in from unfamiliar location</span></span>
<span data-ttu-id="69bf9-191">사용자가 새 위치(IP, 위도/경도 및 ASN)에서 성공적으로 로그인한 경우 트리거되는 위험 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-191">A risk event triggered when a user successfully signs in from a new location (IP, Latitude/Longitude and ASN).</span></span>

### <a name="sign-in-risk"></a><span data-ttu-id="69bf9-192">로그인 위험</span><span class="sxs-lookup"><span data-stu-id="69bf9-192">Sign-in risk</span></span>
<span data-ttu-id="69bf9-193">위험 수준(로그인)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69bf9-193">See Risk level (sign-in)</span></span>

### <a name="sign-in-risk-policy"></a><span data-ttu-id="69bf9-194">로그인 위험 정책</span><span class="sxs-lookup"><span data-stu-id="69bf9-194">Sign-in risk policy</span></span>
<span data-ttu-id="69bf9-195">특정 로그인에 대한 위험을 평가하고 미리 정의된 조건 및 규칙에 따라 완화를 적용하는 조건부 액세스 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-195">A conditional access policy that evaluates the risk to a specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

### <a name="user-compromise-risk"></a><span data-ttu-id="69bf9-196">사용자 손상 위험</span><span class="sxs-lookup"><span data-stu-id="69bf9-196">User compromise risk</span></span>
<span data-ttu-id="69bf9-197">위험 수준(사용자 손상)을 참조하세요</span><span class="sxs-lookup"><span data-stu-id="69bf9-197">See Risk level (user compromise)</span></span>

### <a name="user-risk"></a><span data-ttu-id="69bf9-198">사용자 위험</span><span class="sxs-lookup"><span data-stu-id="69bf9-198">User risk</span></span>
<span data-ttu-id="69bf9-199">위험 수준(사용자 손상)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69bf9-199">See Risk level (user compromise).</span></span>

### <a name="user-risk-policy"></a><span data-ttu-id="69bf9-200">사용자 위험 정책</span><span class="sxs-lookup"><span data-stu-id="69bf9-200">User risk policy</span></span>
<span data-ttu-id="69bf9-201">로그인을 고려하고 미리 정의된 조건 및 규칙에 따라 완화를 적용하는 조건부 액세스 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-201">A conditional access policy that considers the sign-in and applies mitigations based on predefined conditions and rules.</span></span>

### <a name="users-flagged-for-risk"></a><span data-ttu-id="69bf9-202">위험에 대한 플래그가 지정된 사용자</span><span class="sxs-lookup"><span data-stu-id="69bf9-202">Users flagged for risk</span></span>
<span data-ttu-id="69bf9-203">활성화되거나 수정된 위험 이벤트를 가진 사용자입니다</span><span class="sxs-lookup"><span data-stu-id="69bf9-203">Users that have risk events which are either active or remediated</span></span>

### <a name="vulnerability"></a><span data-ttu-id="69bf9-204">취약점</span><span class="sxs-lookup"><span data-stu-id="69bf9-204">Vulnerability</span></span>
<span data-ttu-id="69bf9-205">디렉터리가 악용 또는 위협에 취약하게 만드는 Azure Active Directory의 구성 또는 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="69bf9-205">A configuration or condition in Azure Active Directory which makes the directory susceptible to exploits or threats.</span></span>

## <a name="see-also"></a><span data-ttu-id="69bf9-206">참고 항목</span><span class="sxs-lookup"><span data-stu-id="69bf9-206">See also</span></span>
* [<span data-ttu-id="69bf9-207">Azure Active Directory ID 보호</span><span class="sxs-lookup"><span data-stu-id="69bf9-207">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

