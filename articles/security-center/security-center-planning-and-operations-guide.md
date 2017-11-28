---
title: "aaaSecurity 센터 계획 및 운영 가이드 | Microsoft Docs"
description: "이 문서를 사용 하면 tooplan 일상적인 작업에 대 한 고려 사항 및 Azure 보안 센터를 채택 하기 전에."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f984e4a2-ac97-40bf-b281-2f7f473494c4
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: yurid
ms.openlocfilehash: b0a0a6f5fd56fbd46f7736928c99e3bcd0b1e140
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-planning-and-operations-guide"></a><span data-ttu-id="25192-103">Azure 보안 센터 계획 및 작업 가이드</span><span class="sxs-lookup"><span data-stu-id="25192-103">Azure Security Center planning and operations guide</span></span>
<span data-ttu-id="25192-104">이 가이드는 정보 기술 (IT) 전문가, IT 설계자, 정보 보안 분석가 및 해당 조직이 toouse Azure 보안 센터를 계획 하는 클라우드 관리자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-104">This guide is for information technology (IT) professionals, IT architects, information security analysts, and cloud administrators whose organizations are planning toouse Azure Security Center.</span></span>

>[!NOTE] 
><span data-ttu-id="25192-105">보안 센터는 초기 년 6 월 2017 년 부터는 hello Microsoft Monitoring Agent toocollect를 사용 하 고 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-105">Beginning in early June 2017, Security Center will use hello Microsoft Monitoring Agent toocollect and store data.</span></span> <span data-ttu-id="25192-106">참조 [Azure 보안 센터 플랫폼 마이그레이션](security-center-platform-migration.md) toolearn 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-106">See [Azure Security Center Platform Migration](security-center-platform-migration.md) toolearn more.</span></span> <span data-ttu-id="25192-107">이 문서의 정보 hello 전환 toohello Microsoft Monitoring Agent 후 보안 센터 기능을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="25192-107">hello information in this article represents Security Center functionality after transition toohello Microsoft Monitoring Agent.</span></span>
>

## <a name="planning-guide"></a><span data-ttu-id="25192-108">계획 가이드</span><span class="sxs-lookup"><span data-stu-id="25192-108">Planning guide</span></span>
<span data-ttu-id="25192-109">이 가이드의 단계와 사용자의 보안 센터 사용 하면 조직의 보안 요구 사항 및 클라우드 관리 모델에 따라 toooptimize 참고할 수 있는 작업 집합을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-109">This guide covers a set of steps and tasks that you can follow toooptimize your use of Security Center based on your organization’s security requirements and cloud management model.</span></span> <span data-ttu-id="25192-110">tootake 완전히 활용 보안 센터를 중요 한 toounderstand 어떻게 서로 다른 개인 또는 팀에 조직 hello 서비스 toomeet 보안 개발 및 작동, 모니터링, 관리, 사용 및 사고 대응 요구 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-110">tootake full advantage of Security Center, it is important toounderstand how different individuals or teams in your organization use hello service toomeet secure development and operations, monitoring, governance, and incident response needs.</span></span> <span data-ttu-id="25192-111">hello 주요 영역 tooconsider toouse 보안 센터를 계획할 때에</span><span class="sxs-lookup"><span data-stu-id="25192-111">hello key areas tooconsider when planning toouse Security Center are:</span></span>

* <span data-ttu-id="25192-112">보안 역할 및 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="25192-112">Security Roles and Access Controls</span></span>
* <span data-ttu-id="25192-113">보안 정책 및 권장 사항</span><span class="sxs-lookup"><span data-stu-id="25192-113">Security Policies and Recommendations</span></span>
* <span data-ttu-id="25192-114">데이터 수집 및 저장</span><span class="sxs-lookup"><span data-stu-id="25192-114">Data Collection and Storage</span></span>
* <span data-ttu-id="25192-115">지속적인 보안 모니터링</span><span class="sxs-lookup"><span data-stu-id="25192-115">Ongoing Security Monitoring</span></span>
* <span data-ttu-id="25192-116">사고 대응</span><span class="sxs-lookup"><span data-stu-id="25192-116">Incident Response</span></span>

<span data-ttu-id="25192-117">Hello 다음 섹션에 설명 합니다 방법을 tooplan 각 영역에 대 한 요구 사항에 따라 이러한 권장 사항을 적용 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25192-117">In hello next section, you will learn how tooplan for each one of those areas and apply those recommendations based on your requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="25192-118">읽기 [질문과 대답 (FAQ) Azure 보안 센터](security-center-faq.md) hello 디자인 및 계획 단계 동안 유용할 수 수도 있는 일반적인 질문의 목록에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-118">Read [Azure Security Center frequently asked questions (FAQ)](security-center-faq.md) for a list of common questions that can also be useful during hello designing and planning phase.</span></span>
> 

## <a name="security-roles-and-access-controls"></a><span data-ttu-id="25192-119">보안 역할 및 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="25192-119">Security roles and access controls</span></span>
<span data-ttu-id="25192-120">Hello 크기 및 사용자의 조직 구조에 따라 여러 개인과 팀 보안 센터 tooperform 다른 보안 관련 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25192-120">Depending on hello size and structure of your organization, multiple individuals and teams may use Security Center tooperform different security-related tasks.</span></span> <span data-ttu-id="25192-121">다음 다이어그램 hello 가상의 사용자 및 해당 역할 및 보안 책임의 예를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25192-121">In hello following diagram you have an example of fictitious personas and their respective roles and security responsibilities:</span></span>

![역할](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig01-new.png)

<span data-ttu-id="25192-123">보안 센터 이러한 개인 toomeet 이러한 다양 한 책임을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25192-123">Security Center enables these individuals toomeet these various responsibilities.</span></span> <span data-ttu-id="25192-124">예:</span><span class="sxs-lookup"><span data-stu-id="25192-124">For example:</span></span>

<span data-ttu-id="25192-125">**Jeff(클라우드 워크로드 소유자)**</span><span class="sxs-lookup"><span data-stu-id="25192-125">**Jeff (Cloud Workload Owner)**</span></span>

* <span data-ttu-id="25192-126">클라우드 워크로드와 관련 리소스를 관리</span><span class="sxs-lookup"><span data-stu-id="25192-126">Manage a cloud workload and its related resources</span></span>
* <span data-ttu-id="25192-127">회사 보안 정책에 따라 보호를 구현하고 유지 관리하는 업무를 담당</span><span class="sxs-lookup"><span data-stu-id="25192-127">Responsible for implementing and maintaining protections in accordance with company security policy</span></span>

<span data-ttu-id="25192-128">**Ellen(CISO/CIO)**</span><span class="sxs-lookup"><span data-stu-id="25192-128">**Ellen (CISO/CIO)**</span></span>

* <span data-ttu-id="25192-129">Hello 회사에 대 한 보안의 모든 측면에 대 한 책임</span><span class="sxs-lookup"><span data-stu-id="25192-129">Responsible for all aspects of security for hello company</span></span>
* <span data-ttu-id="25192-130">Toounderstand hello 회사의 보안 상태는 클라우드 워크 로드 간에</span><span class="sxs-lookup"><span data-stu-id="25192-130">Wants toounderstand hello company's security posture across cloud workloads</span></span>
* <span data-ttu-id="25192-131">요구 사항 toobe 주요 공격 및 위험에 대 한 안내</span><span class="sxs-lookup"><span data-stu-id="25192-131">Needs toobe informed of major attacks and risks</span></span>

<span data-ttu-id="25192-132">**David(IT 보안)**</span><span class="sxs-lookup"><span data-stu-id="25192-132">**David (IT Security)**</span></span>

* <span data-ttu-id="25192-133">집합 회사 tooensure hello에 대 한 적절 한 보호 사용 되는 보안 정책</span><span class="sxs-lookup"><span data-stu-id="25192-133">Sets company security policies tooensure hello appropriate protections are in place</span></span>
* <span data-ttu-id="25192-134">정책 준수 여부를 모니터링</span><span class="sxs-lookup"><span data-stu-id="25192-134">Monitors compliance with policies</span></span>
* <span data-ttu-id="25192-135">경영진 또는 감사를 위한 보고서를 작성</span><span class="sxs-lookup"><span data-stu-id="25192-135">Generates reports for leadership or auditors</span></span>

<span data-ttu-id="25192-136">**Judy(보안 운영)**</span><span class="sxs-lookup"><span data-stu-id="25192-136">**Judy (Security Operations)**</span></span>

* <span data-ttu-id="25192-137">모니터링 하 고 응답 toosecurity 경고 24/7</span><span class="sxs-lookup"><span data-stu-id="25192-137">Monitors and responds toosecurity alerts 24/7</span></span>
* <span data-ttu-id="25192-138">작업 소유자 tooCloud 또는 IT 보안 분석가 에스컬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-138">Escalates tooCloud Workload Owner or IT Security Analyst</span></span>

<span data-ttu-id="25192-139">**Sam(보안 분석가)**</span><span class="sxs-lookup"><span data-stu-id="25192-139">**Sam (Security Analyst)**</span></span>

* <span data-ttu-id="25192-140">공격 여부 조사</span><span class="sxs-lookup"><span data-stu-id="25192-140">Investigate attacks</span></span>
* <span data-ttu-id="25192-141">클라우드 작업 소유자 tooapply 재구성 작업</span><span class="sxs-lookup"><span data-stu-id="25192-141">Work with Cloud Workload Owner tooapply remediation</span></span> 

<span data-ttu-id="25192-142">보안 센터를 사용 하 여 [역할 기반 액세스 제어 (RBAC)](../active-directory/role-based-access-control-configure.md)를 제공 하는 [기본 제공 역할](../active-directory/role-based-access-built-in-roles.md) toousers, 그룹 및 Azure 서비스에에서 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25192-142">Security Center uses [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md), which provides [built-in roles](../active-directory/role-based-access-built-in-roles.md) that can be assigned toousers, groups, and services in Azure.</span></span> <span data-ttu-id="25192-143">정보 표시 사용자가 보안 센터를 열면 tooresources 액세스할 수 있는 관련 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-143">When a user opens Security Center, they only see information related tooresources they have access to.</span></span> <span data-ttu-id="25192-144">즉, hello 사용자가 소유자, 참가자 또는 판독기 toohello 구독 또는 리소스 그룹의 리소스에 속하는 hello 역할을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-144">Which means hello user is assigned hello role of Owner, Contributor, or Reader toohello subscription or resource group that a resource belongs to.</span></span> <span data-ttu-id="25192-145">또한 toothese 역할에는 두 개의 특정 보안 센터 역할이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25192-145">In addition toothese roles, there are two specific Security Center roles:</span></span>

- <span data-ttu-id="25192-146">**보안 판독기**: toothis 역할에 속하는 사용자 수 tooview 권한 tooSecurity 센터 권장 사항, 경고, 정책 및 상태를 포함 하는 수는 있지만 수 toomake 변경 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="25192-146">**Security reader**: user that belongs toothis role is be able tooview rights tooSecurity Center, which includes recommendations, alerts, policy, and health, but it won't be able toomake changes.</span></span>
- <span data-ttu-id="25192-147">**보안 관리자**: 동일 하지만 보안 판독기 수 hello 보안 정책 업데이트도 해제 권장 사항 및 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-147">**Security admin**: same as security reader but it can also update hello security policy, dismiss recommendations and alerts.</span></span>

<span data-ttu-id="25192-148">위에서 설명한 hello 보안 센터 역할 저장소, 웹 및 모바일, 사물 인터넷 등 Azure의 액세스 tooother 서비스 영역을 갖지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="25192-148">hello Security Center roles described above do not have access tooother service areas of Azure such as Storage, Web & Mobile, or Internet of Things.</span></span>  

> [!NOTE]
> <span data-ttu-id="25192-149">사용자는 최소한 구독, 리소스 그룹 소유자 또는 참가자 toobe 수 toosee Azure 보안 센터 toobe 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-149">A user needs toobe at least a subscription, resource group owner, or contributor toobe able toosee Security Center in Azure.</span></span> 
> 
> 

<span data-ttu-id="25192-150">Hello 가상 사용자를 사용 하 여 다음 RBAC가 필요 합니다. hello hello 이전 다이어그램에 설명이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25192-150">Using hello personas explained in hello previous diagram, hello following RBAC would be needed:</span></span>

<span data-ttu-id="25192-151">**Jeff(클라우드 워크로드 소유자)**</span><span class="sxs-lookup"><span data-stu-id="25192-151">**Jeff (Cloud Workload Owner)**</span></span>

* <span data-ttu-id="25192-152">리소스 그룹 소유자/협업자</span><span class="sxs-lookup"><span data-stu-id="25192-152">Resource Group Owner/Collaborator</span></span>

<span data-ttu-id="25192-153">**David(IT 보안)**</span><span class="sxs-lookup"><span data-stu-id="25192-153">**David (IT Security)**</span></span>

* <span data-ttu-id="25192-154">구독 소유자/협력자 또는 보안 관리자</span><span class="sxs-lookup"><span data-stu-id="25192-154">Subscription Owner/Collaborator or Security Admin</span></span>

<span data-ttu-id="25192-155">**Judy(보안 운영)**</span><span class="sxs-lookup"><span data-stu-id="25192-155">**Judy (Security Operations)**</span></span>

* <span data-ttu-id="25192-156">구독 판독기 또는 보안 사용자 tooview 경고</span><span class="sxs-lookup"><span data-stu-id="25192-156">Subscription Reader or Security Reader tooview Alerts</span></span>
* <span data-ttu-id="25192-157">구독 소유자/협력자 또는 보안 관리자 필요한 toodismiss 경고</span><span class="sxs-lookup"><span data-stu-id="25192-157">Subscription Owner/Collaborator or Security Admin required toodismiss Alerts</span></span>

<span data-ttu-id="25192-158">**Sam(보안 분석가)**</span><span class="sxs-lookup"><span data-stu-id="25192-158">**Sam (Security Analyst)**</span></span>

* <span data-ttu-id="25192-159">구독 사용자 tooview 경고</span><span class="sxs-lookup"><span data-stu-id="25192-159">Subscription Reader tooview Alerts</span></span>
* <span data-ttu-id="25192-160">구독 소유자/공동 작업자 필요한 toodismiss 경고</span><span class="sxs-lookup"><span data-stu-id="25192-160">Subscription Owner/Collaborator required toodismiss Alerts</span></span>
* <span data-ttu-id="25192-161">Toohello 작업 영역 액세스 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25192-161">Access toohello workspace may be required</span></span>

<span data-ttu-id="25192-162">다른 중요 한 정보 tooconsider:</span><span class="sxs-lookup"><span data-stu-id="25192-162">Some other important information tooconsider:</span></span>

* <span data-ttu-id="25192-163">구독 소유자/참가자 및 보안 관리자만 보안 정책을 편집할 수 있음</span><span class="sxs-lookup"><span data-stu-id="25192-163">Only subscription Owners/Contributors and Security Admins can edit a security policy</span></span>
* <span data-ttu-id="25192-164">구독 및 리소스 그룹 소유자 및 참가자만 리소스에 대한 보안 권장 사항을 적용할 수 있음</span><span class="sxs-lookup"><span data-stu-id="25192-164">Only subscription and resource group Owners and Contributors can apply security recommendations for a resource</span></span>

<span data-ttu-id="25192-165">RBAC를 사용 하 여 보안 센터에 대 한 액세스 제어를 계획할 때는 보안 센터를 사용 하는 조직에 게 있는지 toounderstand 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25192-165">When planning access control using RBAC for Security Center, be sure toounderstand who in your organization will be using Security Center.</span></span> <span data-ttu-id="25192-166">또한 수행할 작업 유형을 확인한 다음 RBAC을 적합하게 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-166">Also, what types of tasks they will be performing and then configure RBAC accordingly.</span></span>

> [!NOTE]
> <span data-ttu-id="25192-167">Hello를 할당 하는 것이 좋습니다 사이의 역할 작업 사용자 toocomplete에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-167">We recommend that you assign hello least permissive role needed for users toocomplete their tasks.</span></span> <span data-ttu-id="25192-168">예를 들어 사용자에 게 리소스의 hello 보안 상태에 대 한 정보 tooview 하지만 권장 구성 적용 정책 편집 등의 작업 수행 하지만 hello 읽기 역할을 할당 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-168">For example, users who only need tooview information about hello security state of resources but not take action, such as applying recommendations or editing policies, should be assigned hello Reader role.</span></span>
> 
> 

## <a name="security-policies-and-recommendations"></a><span data-ttu-id="25192-169">보안 정책 및 권장 사항</span><span class="sxs-lookup"><span data-stu-id="25192-169">Security policies and recommendations</span></span>
<span data-ttu-id="25192-170">지정 된 hello 내의 리소스에 대 한 권장 되는 컨트롤의 hello 집합을 정의 하는 보안 정책을 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-170">A security policy defines hello set of controls, which are recommended for resources within hello specified subscription.</span></span> <span data-ttu-id="25192-171">보안 센터 tooyour 회사의 보안 요구 사항 및 응용 프로그램의 hello 유형 또는 hello 데이터의 민감도 따라 정책을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-171">In Security Center, you define policies according tooyour company's security requirements and hello type of applications or sensitivity of hello data.</span></span>

<span data-ttu-id="25192-172">Hello 다음 다이어그램에에서 표시 된 대로 hello 구독 내에서 tooall 리소스 그룹을 전파 하는 hello 구독 수준에 자동으로 설정 된 정책:</span><span class="sxs-lookup"><span data-stu-id="25192-172">Policies that are enabled in hello subscription level automatically propagate tooall resources groups within hello subscription as shown in hello following diagram:</span></span>

![보안 정책](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig2-newUI.png)

> [!NOTE]
> <span data-ttu-id="25192-174">어떤 정책이 변경 된 tooreview 필요한 경우 사용할 수 있습니다 [Azure 감사 로그](https://blogs.msdn.microsoft.com/cloud_solution_architect/2015/03/10/audit-logs-for-azure-events/)합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-174">If you need tooreview which policies were changed, you can use [Azure Audit Logs](https://blogs.msdn.microsoft.com/cloud_solution_architect/2015/03/10/audit-logs-for-azure-events/).</span></span> <span data-ttu-id="25192-175">정책 변경은 항상 Azure 감사 로그에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="25192-175">Policy changes are always logged in Azure Audit Logs.</span></span>
> 
> 

### <a name="security-recommendations"></a><span data-ttu-id="25192-176">보안 권장 사항</span><span class="sxs-lookup"><span data-stu-id="25192-176">Security recommendations</span></span>
<span data-ttu-id="25192-177">보안 정책을 구성 하기 전에 각 hello 검토 [보안 권장 사항](security-center-recommendations.md), 이러한 정책은 다양 한 구독 및 리소스 그룹에 적절 한 되는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-177">Before configuring security policies, review each of hello [security recommendations](security-center-recommendations.md), and determine whether these policies are appropriate for your various subscriptions and resource groups.</span></span> <span data-ttu-id="25192-178">것도 중요 한 toounderstand 조치를 취해야 tooaddress [보안 권장 사항](https://docs.microsoft.com/en-us/azure/security-center/security-center-recommendations) 조직에서 누가 새 권장 사항 및 라인 hello 필요한 단계에 대 한 모니터링을 담당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25192-178">It is also important toounderstand what action should be taken tooaddress [Security Recommendations](https://docs.microsoft.com/en-us/azure/security-center/security-center-recommendations) and who in your organization will be responsible for monitoring for new recommendations and taking hello needed steps.</span></span>

<span data-ttu-id="25192-179">Security Center는 Azure 구독에 대한 보안 연락처 세부 정보를 제공하는 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-179">Security Center will recommend that you provide security contact details for your Azure subscription.</span></span> <span data-ttu-id="25192-180">이 정보는 Microsoft toocontact 하 여 사용 Microsoft 보안 대응 센터 (MSRC) hello 발견 불법 또는 무단 당사자가 고객 데이터에 액세스 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25192-180">This information will be used by Microsoft toocontact you if hello Microsoft Security Response Center (MSRC) discovers that your customer data has been accessed by an unlawful or unauthorized party.</span></span> <span data-ttu-id="25192-181">읽기 [Azure 보안 센터에서 보안 연락처 세부 정보를 제공](security-center-provide-security-contact-details.md) 방법에 대 한 자세한 내용은 tooenable이이 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-181">Read [Provide security contact details in Azure Security Center](security-center-provide-security-contact-details.md) for more information on how tooenable this recommendation.</span></span>

## <a name="data-collection-and-storage"></a><span data-ttu-id="25192-182">데이터 수집 및 저장</span><span class="sxs-lookup"><span data-stu-id="25192-182">Data collection and storage</span></span>
<span data-ttu-id="25192-183">Azure 보안 센터 hello Microsoft Monitoring Agent를 사용 하 여 –이 hello Operations Management Suite 및 로그 분석 서비스 – 가상 컴퓨터에서 보안 데이터 toocollect hello 동일한 에이전트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-183">Azure Security Center uses hello Microsoft Monitoring Agent – this is hello same agent used by hello Operations Management Suite and Log Analytics service – toocollect security data from your virtual machines.</span></span> <span data-ttu-id="25192-184">이 에이전트에서 수집된 데이터는 Log Analytics 작업 영역에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="25192-184">Data collected from this agent will be stored in your Log Analytics workspace(s).</span></span>

### <a name="agent"></a><span data-ttu-id="25192-185">에이전트</span><span class="sxs-lookup"><span data-stu-id="25192-185">Agent</span></span>

<span data-ttu-id="25192-186">Hello 보안 정책에서 데이터 수집을 활성화 한 후 Microsoft Monitoring Agent hello (에 대 한 [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents) 또는 [Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents))에 지원 되는 모든 Azure Vm 및 만들어진 새로 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-186">After data collection is enabled in hello security policy, hello Microsoft Monitoring Agent (for [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents) or [Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents)) is installed on all supported Azure VMs and any new ones that are created.</span></span>  <span data-ttu-id="25192-187">현재 hello hello VM에 이미 설치 된 Microsoft Monitoring Agent hello Azure 보안 센터를 활용 하는 경우 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-187">If hello VM already has hello Microsoft Monitoring Agent installed, Azure Security Center will leverage hello current installed agent.</span></span> <span data-ttu-id="25192-188">hello 에이전트 프로세스 디자인 된 toobe 침투성 이며 VM 성능에 최소한의 영향을 줄 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-188">hello agent’s process is designed toobe non-invasive and have very minimal impact on VM performance.</span></span>

<span data-ttu-id="25192-189">Microsoft 모니터링 에이전트에 대 한 Windows hello 사용 하 여 TCP 포트 443 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-189">hello Microsoft Monitoring Agent for Windows requires use TCP port 443.</span></span> <span data-ttu-id="25192-190">Hello 참조 [문제 해결 문서](security-center-troubleshooting-guide.md) 추가 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-190">See hello [Troubleshooting article](security-center-troubleshooting-guide.md) for additional details.</span></span>

<span data-ttu-id="25192-191">특정 시점에 toodisable 데이터 수집을 원하는 경우 있습니다 수 해제 hello 보안 정책에서.</span><span class="sxs-lookup"><span data-stu-id="25192-191">If at some point you want toodisable Data Collection, you can turn it off in hello security policy.</span></span> <span data-ttu-id="25192-192">그러나 다른 Azure management에서 hello Microsoft Monitoring Agent를 사용할 수 있으며 서비스를 모니터링, hello 에이전트 제거 되지 것입니다 자동으로 하기 때문에 해제 하면 보안 센터에서 데이터를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-192">However, because hello Microsoft Monitoring Agent may be used by other Azure management and monitoring services, hello agent will not be uninstalled automatically when you turn off data collection in  Security Center.</span></span> <span data-ttu-id="25192-193">필요한 경우 hello 에이전트를 수동으로 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25192-193">You can manually uninstall hello agent if needed.</span></span>

> [!NOTE]
> <span data-ttu-id="25192-194">toofind hello 읽기를 지원 되는 Vm의 목록 [질문과 대답 (FAQ) Azure 보안 센터](security-center-faq.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-194">toofind a list of supported VMs, read hello [Azure Security Center frequently asked questions (FAQ)](security-center-faq.md).</span></span>
> 

### <a name="workspace"></a><span data-ttu-id="25192-195">작업 영역</span><span class="sxs-lookup"><span data-stu-id="25192-195">Workspace</span></span>

<span data-ttu-id="25192-196">(Azure 보안 센터) 대신 하 여 Microsoft Monitoring Agent는 기존 로그 분석 중에 저장 되는 hello에서 수집 된 데이터 또는 연결 된 Azure 구독 새 중 계정 hello hello VM의 지역을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-196">Data collected from hello Microsoft Monitoring Agent (on behalf of Azure Security Center) will be stored in either an existing Log Analytics workspace(s) associated with your Azure subscription or a new workspace(s), taking into account hello Geo of hello VM.</span></span> 

<span data-ttu-id="25192-197">Hello Azure 포털, Azure 보안 센터에서 만든을 포함 하 여, 로그 분석 작업 영역 목록이 toosee를 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25192-197">In hello Azure portal, you can browse toosee a list of your Log Analytics workspaces, including any created by Azure Security Center.</span></span> <span data-ttu-id="25192-198">새 작업 영역에 관련된 리소스 그룹이 만들어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25192-198">A related resource group will be created for new workspaces.</span></span> <span data-ttu-id="25192-199">둘 다 다음과 같은 명명 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="25192-199">Both will follow this naming convention:</span></span> 

* <span data-ttu-id="25192-200">작업 영역: *DefaultWorkspace-[subscription-ID]-[geo]*</span><span class="sxs-lookup"><span data-stu-id="25192-200">Workspace: *DefaultWorkspace-[subscription-ID]-[geo]*</span></span>
* <span data-ttu-id="25192-201">리소스 그룹: *DefaultResouceGroup-[geo]*</span><span class="sxs-lookup"><span data-stu-id="25192-201">Resource Group: *DefaultResouceGroup-[geo]*</span></span>

<span data-ttu-id="25192-202">Azure Security Center에서 만든 작업 영역의 경우 데이터는 30일 동안 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="25192-202">For workspaces created by Azure Security Center, data is retained for 30 days.</span></span> <span data-ttu-id="25192-203">작업 영역을 종료 하는 데 보존은 가격 책정 계층 hello 작업 영역을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-203">For exiting workspaces, retention is based on hello workspace pricing tier.</span></span>

> [!NOTE]
> <span data-ttu-id="25192-204">Microsoft는 강력한 약정 tooprotect hello 개인 정보 및이 데이터의 보안을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-204">Microsoft make strong commitments tooprotect hello privacy and security of this data.</span></span> <span data-ttu-id="25192-205">Microsoft toostrict 규정 준수 및 보안 지침을 따르는-toooperating 서비스 코딩 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-205">Microsoft adheres toostrict compliance and security guidelines—from coding toooperating a service.</span></span> <span data-ttu-id="25192-206">데이터 처리 및 개인 정보 보호에 대한 자세한 내용은 [Azure Security Center 데이터 보안](security-center-data-security.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25192-206">For more information about data handling and privacy, read [Azure Security Center Data Security](security-center-data-security.md).</span></span>
> 

## <a name="ongoing-security-monitoring"></a><span data-ttu-id="25192-207">지속적인 보안 모니터링</span><span class="sxs-lookup"><span data-stu-id="25192-207">Ongoing security monitoring</span></span>
<span data-ttu-id="25192-208">초기 구성 및 보안 센터 권장 사항 적용 한 후 다음 단계 hello 보안 센터 운영 프로세스 고려 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-208">After initial configuration and application of Security Center recommendations, hello next step is considering Security Center operational processes.</span></span>

<span data-ttu-id="25192-209">보안 센터 hello 클릭할 수 있는 Azure 포털에서에서 tooaccess **찾아보기** 유형과 **보안 센터** hello에 **필터** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="25192-209">tooaccess Security Center from hello Azure portal you can click **Browse** and type **Security Center** in hello **Filter** field.</span></span> <span data-ttu-id="25192-210">hello 뷰는 hello 사용자 가져옵니다 기반으로 하는 toothese 적용 된 필터, 아래 hello 예제 주소를 지정 하는 많은 문제 toobe 된 환경을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="25192-210">hello views that hello user gets are according toothese applied filters, hello example below shows an environment with many issues toobe addressed:</span></span>

![dashboard](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig6.png)

> [!NOTE]
> <span data-ttu-id="25192-212">보안 센터 일반 운영 절차를 방해 하지 않도록, 수 동적으로 배포를 모니터링 하 고 사용 하도록 설정한 hello 보안 정책에 따라 권장 사항을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-212">Security Center will not interfere with your normal operational procedures, it will passively monitor your deployments and provide recommendations based on hello security policies you enabled.</span></span>

<span data-ttu-id="25192-213">먼저 현재 Azure 환경에 대 한 보안 센터 toouse에서 선택, 하는 경우 hello에서 변환을 수행할 수 있는 모든 권장 사항을 검토 하 고 있는지 확인 **권장 사항을** 타일 또는 리소스 당 (**계산** **네트워킹**, **데이터 및 저장소**, **응용 프로그램**).</span><span class="sxs-lookup"><span data-stu-id="25192-213">When you first opt in toouse Security Center for your current Azure environment, make sure that you review all recommendations, which can be done in hello **Recommendations** tile or per resource (**Compute**, **Networking**, **Storage & data**, **Application**).</span></span>

<span data-ttu-id="25192-214">모든 권장 사항을 해결 되 면 hello **방지** 섹션 주소가 지정 된 모든 리소스에 대 한 녹색 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-214">Once you address all recommendations, hello **Prevention** section should be green for all resources that were addressed.</span></span> <span data-ttu-id="25192-215">지속적인 모니터링이 시점에서 ý ´ ï 이후 hello 리소스 보안 상태 및 권장 사항 타일의 변화에 따라 작업만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25192-215">Ongoing monitoring at this point becomes easier since you will only take actions based on changes in hello resource security health and recommendations tiles.</span></span>

<span data-ttu-id="25192-216">hello **검색** 섹션은 더 사후, 이들은 중 하나가 진행 중인은 now, 또는 지난 hello에서 발생 했으며 보안 센터 컨트롤과 제 3 자 시스템에서 검색 된 하는 문제에 대 한 경고입니다.</span><span class="sxs-lookup"><span data-stu-id="25192-216">hello **Detection** section is more reactive, these are alerts regarding issues that are either taking place now, or occurred in hello past and were detected by Security Center controls and 3rd party systems.</span></span> <span data-ttu-id="25192-217">hello 보안 경고 타일 hello 각 날짜 및 해당 배포 hello 다른 심각도 범주 (낮음, 보통, 높음) 사이 발견 된 위협 검색 경고 수를 나타내는 막대 그래프에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25192-217">hello Security Alerts tile will show bar graphs that represent hello number of threat detection alerts that were found in each day, and their distribution among hello different severity categories (low, medium, high).</span></span> <span data-ttu-id="25192-218">보안 경고에 대 한 자세한 내용은 [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-218">For more information about Security Alerts, read [Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md).</span></span>

> [!NOTE]
> <span data-ttu-id="25192-219">Microsoft Power BI toovisualize 보안 센터 데이터 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25192-219">You can also leverage Microsoft Power BI toovisualize your Security Center data.</span></span> <span data-ttu-id="25192-220">[Power BI로 Azure Security Center 데이터에서 정보 얻기](security-center-powerbi.md)를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="25192-220">Read [Get insights from Azure Security Center data with Power BI](security-center-powerbi.md).</span></span>
> 
> 

### <a name="monitoring-for-new-or-changed-resources"></a><span data-ttu-id="25192-221">새 또는 변경된 리소스 모니터링</span><span class="sxs-lookup"><span data-stu-id="25192-221">Monitoring for new or changed resources</span></span>
<span data-ttu-id="25192-222">대부분의 Azure 환경은 동적이며, 새 리소스가 일정 기준, 구성 또는 변경에 따라 확장 및 분리됩니다. 보안 센터를 사용 하면 이러한 새 리소스의 hello 보안 상태에 대 한 가시성을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-222">Most Azure environments are dynamic, with new resources being spun up and down on a regular basis, configurations or changes, etc. Security Center helps ensure that you have visibility into hello security state of these new resources.</span></span>

<span data-ttu-id="25192-223">새 리소스 (Vm, SQL Db) tooyour Azure 환경에 추가 하면 보안 센터 자동으로 이러한 리소스를 검색 하 고 toomonitor의 보안을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-223">When you add new resources (VMs, SQL DBs) tooyour Azure Environment, Security Center will automatically discover these resources and begin toomonitor their security.</span></span> <span data-ttu-id="25192-224">또한 PaaS 웹 역할 및 작업자 역할이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="25192-224">This also includes PaaS web roles and worker roles.</span></span> <span data-ttu-id="25192-225">Hello 데이터 수집을 활성화 한 경우 [보안 정책](security-center-policies.md)추가 모니터링 기능을 설정할 자동으로 가상 컴퓨터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-225">If Data Collection is enabled in hello [Security Policy](security-center-policies.md), additional monitoring capabilities will be enabled automatically for your virtual machines.</span></span>

![주요 영역](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig3-newUI.png)

1. <span data-ttu-id="25192-227">가상 컴퓨터의 경우 **방지** 섹션에서 **계산**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-227">For virtual machines, click **Compute**, under **Prevention** section.</span></span> <span data-ttu-id="25192-228">Hello에 관련 데이터 또는 관련된 권장 사항을 사용 하도록 설정 된 모든 문제 표시지 것입니다 **개요** 탭 및 **권장 사항을 모니터링** 섹션.</span><span class="sxs-lookup"><span data-stu-id="25192-228">Any issues with enabling data or related recommendations will be surfaced in hello **Overview** tab, and **Monitoring Recommendations** section.</span></span>
2. <span data-ttu-id="25192-229">보기 hello **권장 사항을** toosee 부분, 보안 위험 hello 새 리소스에 대해 확인 된 경우.</span><span class="sxs-lookup"><span data-stu-id="25192-229">View hello **Recommendations** toosee what, if any, security risks were identified for hello new resource.</span></span>
3. <span data-ttu-id="25192-230">새 Vm tooyour 환경에 추가 되 면 hello 운영 체제만 처음 설치는 매우 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="25192-230">It is very common that when new VMs are added tooyour environment, only hello operating system is initially installed.</span></span> <span data-ttu-id="25192-231">hello 리소스 소유자 이러한 Vm에서 사용할 수 있는 다른 앱 일부 시간 toodeploy 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25192-231">hello resource owner might need some time toodeploy other apps that will be used by these VMs.</span></span>  <span data-ttu-id="25192-232">이상적으로이 작업의 최종 목적은 hello를 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-232">Ideally, you should know hello final intent of this workload.</span></span> <span data-ttu-id="25192-233">Toobe 응용 프로그램 서버에 배포할?</span><span class="sxs-lookup"><span data-stu-id="25192-233">Is it going toobe an Application Server?</span></span> <span data-ttu-id="25192-234">내용에이에 따라 새 작업은 진행 중인 toobe, 적절 한 hello를 사용 하도록 설정할 수 **보안 정책**,이 워크플로의 세 번째 단계인 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-234">Based on what this new workload is going toobe, you can enable hello appropriate **Security Policy**, which is hello third step in this workflow.</span></span>
4. <span data-ttu-id="25192-235">새 리소스 tooyour Azure 환경에 추가 되 면 있기 hello에 새 경고 나타나는지 **보안 경고** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="25192-235">As new resources are added tooyour Azure environment, it is possible that new alerts appear in hello **Security Alerts** tile.</span></span> <span data-ttu-id="25192-236">항상이 타일에 새로운 경고가 없는지 확인 하 고 tooSecurity 센터 권장 사항에 따라 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-236">Always verify if there are new alerts in this tile and take actions according tooSecurity Center recommendations.</span></span>

<span data-ttu-id="25192-237">또한 tooregularly 모니터 hello 상태 보안 위험에 생성 된 기존 리소스 tooidentify 구성 변경을 권장 기준과 보안 경고에서 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-237">You will also want tooregularly monitor hello state of existing resources tooidentify configuration changes that have created security risks, drift from recommended baselines, and security alerts.</span></span> <span data-ttu-id="25192-238">Hello 보안 센터 대시보드를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-238">Start at hello Security Center dashboard.</span></span> <span data-ttu-id="25192-239">여기에서 일관적 세 가지 주요 영역 tooreview를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-239">From there you have three major areas tooreview on a consistent basis.</span></span>

![작업](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig4-newUI.png)

1. <span data-ttu-id="25192-241">hello **방지** 섹션 패널 빠른 액세스 tooyour 주요 리소스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-241">hello **Prevention** section panel provides you quick access tooyour key resources.</span></span> <span data-ttu-id="25192-242">이 옵션 toomonitor 계산, 네트워킹, 저장소 및 데이터와 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-242">Use this option toomonitor Compute, Networking, Storage & data and Applications.</span></span>
2. <span data-ttu-id="25192-243">hello **권장 사항을** 패널에서는 tooreview 보안 센터 권장 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="25192-243">hello **Recommendations** panel enables you tooreview Security Center recommendations.</span></span> <span data-ttu-id="25192-244">지속적인 모니터링 하는 동안이 정상 hello 초기 보안 센터 설정에서 모든 권장 사항을 해결 하는 이후 매일 권장 사항을 권한이 없다는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25192-244">During your ongoing monitoring you may find that you don’t have recommendations on a daily basis, which is normal since you addressed all recommendations on hello initial Security Center setup.</span></span> <span data-ttu-id="25192-245">이러한 이유로 있습니다 수 새 정보에이 섹션 매일 없으며 tooaccess 있어야 합니다 필요에 따라 것입니다.</span><span class="sxs-lookup"><span data-stu-id="25192-245">For this reason, you may not have new information in this section every day and will just need tooaccess it as needed.</span></span>
3. <span data-ttu-id="25192-246">hello **검색** 섹션 매우 자주 또는 아주 드물게 기준 변경 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25192-246">hello **Detection** section might change on either a very frequent or very infrequent basis.</span></span> <span data-ttu-id="25192-247">항상 보안 경고를 검토하고 보안 센터 권장 사항에 따라 조치를 취합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-247">Always review your security alerts and take actions based on Security Center recommendations.</span></span>

## <a name="incident-response"></a><span data-ttu-id="25192-248">사고 대응</span><span class="sxs-lookup"><span data-stu-id="25192-248">Incident response</span></span>
<span data-ttu-id="25192-249">보안 센터 감지 하 고 사용자에 게 경고 toothreats 발생할 때.</span><span class="sxs-lookup"><span data-stu-id="25192-249">Security Center detects and alerts you toothreats as they occur.</span></span> <span data-ttu-id="25192-250">조직에서는 새 보안 경고에 대 한 모니터링 및 필요한 tooinvestigate 추가로으로 작업을 수행 하거나 hello 공격을 해결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-250">Organizations should monitor for new security alerts and take action as needed tooinvestigate further or remediate hello attack.</span></span> <span data-ttu-id="25192-251">Security Center 위협 감지 기능이 작동하는 방법에 대한 자세한 내용은 [Azure Security Center 감지 기능](security-center-detection-capabilities.md)을 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="25192-251">For more information on how Security Center threat detection works, read [Azure Security Center detection capabilities](security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="25192-252">이 문서에서 되어 있지 않으면 hello 의도 tooassist 사고 대응 계획을 직접 만드는 동안 하겠습니다 hello 클라우드 수명 주기에서 Microsoft Azure 보안 응답 toouse hello 기반으로 사고 대응 단계에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-252">While this article doesn’t have hello intent tooassist you creating your own Incident Response plan, we are going toouse Microsoft Azure Security Response in hello Cloud lifecycle as hello foundation for incident response stages.</span></span> <span data-ttu-id="25192-253">hello 단계 hello 다음 다이어그램에에서 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25192-253">hello stages are shown in hello following diagram:</span></span>

![의심되는 활동](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-1.png)

> [!NOTE]
> <span data-ttu-id="25192-255">National Institute of Standards hello 및 기술 NIST ()를 사용할 수 있습니다 [컴퓨터 보안 인시던트를 처리 가이드](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf) 참조 tooassist으로 직접 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25192-255">You can use hello National Institute of Standards and Technology (NIST) [Computer Security Incident Handling Guide](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf) as a reference tooassist you building your own.</span></span>
> 

<span data-ttu-id="25192-256">보안 센터 알림을 hello 단계를 수행 하는 동안 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25192-256">You can use Security Center Alerts during hello following stages:</span></span>

* <span data-ttu-id="25192-257">**감지**: 하나 이상의 리소스에서 의심스러운 작업을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-257">**Detect**: identify a suspicious activity in one or more resources.</span></span> 
* <span data-ttu-id="25192-258">**평가**: hello 초기 평가 tooobtain hello 의심 스러운 활동에 대 한 자세한 정보를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-258">**Assess**: perform hello initial assessment tooobtain more information about hello suspicious activity.</span></span>
* <span data-ttu-id="25192-259">**진단**: hello 재구성 단계 tooconduct hello 기술 프로시저 tooaddress hello 문제를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-259">**Diagnose**: use hello remediation steps tooconduct hello technical procedure tooaddress hello issue.</span></span>

<span data-ttu-id="25192-260">각 보안 경고 사용할 수 있는 정보를 제공 toobetter hello 공격의 hello 특성을 이해 하 고 가능한 완화 기능을 제안 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-260">Each Security Alert provides information that can be used toobetter understand hello nature of hello attack and suggest possible mitigations.</span></span> <span data-ttu-id="25192-261">일부 경고는 또한 링크 tooeither 정보 Azure 내에서 더 많은 정보 또는 tooother 원본을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-261">Some alerts also provide links tooeither more information or tooother sources of information within Azure.</span></span> <span data-ttu-id="25192-262">추가 연구 및 toobegin 완화를 제공 하는 hello 정보를 사용할 수 있습니다 및 작업 영역에 저장 되어 있는 보안 관련 데이터를 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25192-262">You can use hello information provided for further research and toobegin mitigation, and you can also search security-related data that is stored in your workspace.</span></span>

<span data-ttu-id="25192-263">hello 다음 예제는 수행 하는 의심 스러운 RDP 활동.</span><span class="sxs-lookup"><span data-stu-id="25192-263">hello following example shows a suspicious RDP activity taking place:</span></span>

![의심되는 활동](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-ga.png)

<span data-ttu-id="25192-265">볼 수 있듯이이 블레이드는 hello 공격이 발생 hello 시간과 관련 된 세부 정보를 표시, 원본 호스트 이름은 hello, 대상 VM hello 및 또한 권장 단계를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-265">As you can see, this blade shows details regarding hello time that hello attack took place, hello source hostname, hello target VM and also gives recommendation steps.</span></span> <span data-ttu-id="25192-266">일부 경우 hello에 hello 공격에 대 한 소스 정보는 비어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25192-266">In some circumstances hello source information of hello attack may be empty.</span></span> <span data-ttu-id="25192-267">이러한 동작 유형에 대한 자세한 내용은 [Azure Security Center 경고에 누락된 원본 정보](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/25/missing-source-information-in-azure-security-center-alerts/) 를 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="25192-267">Read [Missing Source Information in Azure Security Center Alerts](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/25/missing-source-information-in-azure-security-center-alerts/) for more information about this type of behavior.</span></span>

<span data-ttu-id="25192-268">Hello에 [tooLeverage 인시던트 응답에 대 한 Azure 보안 센터 & Microsoft Operations Management Suite을 hello 어떻게](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703) 비디오 볼 수 있습니다 수 있는 각 보안 센터를 사용할 수 있는 방법을 toounderstand 일부 데모 이러한 단계 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="25192-268">In hello [How tooLeverage hello Azure Security Center & Microsoft Operations Management Suite for an Incident Response](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703) video you can see some demonstrations that can help you toounderstand how Security Center can be used in each one of those stages.</span></span>

> [!NOTE]
> <span data-ttu-id="25192-269">읽기 [인시던트 응답에 대 한 Azure 보안 센터 Leveraging](security-center-incident-response.md) toouse 보안 센터 기능 tooassist 처리 하는 방법은 사고 대응 하는 동안 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-269">Read [Leveraging Azure Security Center for Incident Response](security-center-incident-response.md) for more information on how toouse Security Center capabilities tooassist you during your Incident Response process.</span></span> 
> 
> 

## <a name="see-also"></a><span data-ttu-id="25192-270">참고 항목</span><span class="sxs-lookup"><span data-stu-id="25192-270">See also</span></span>
<span data-ttu-id="25192-271">이 문서에서는 방법에 대해 배웠습니다 tooplan 보안 센터 채택 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-271">In this document, you learned how tooplan for Security Center adoption.</span></span> <span data-ttu-id="25192-272">보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="25192-272">toolearn more about Security Center, see hello following:</span></span>

* [<span data-ttu-id="25192-273">관리 하 고 Azure 보안 센터에서 toosecurity 경고 응답</span><span class="sxs-lookup"><span data-stu-id="25192-273">Managing and responding toosecurity alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* <span data-ttu-id="25192-274">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="25192-274">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="25192-275">[Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="25192-275">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) — Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="25192-276">[Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="25192-276">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="25192-277">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) - Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="25192-277">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>

