---
title: "보안 센터 계획 및 작업 가이드| Microsoft Docs"
description: "이 문서는 Azure 보안 센터 도입 전 계획과 일상 운영과 관련한 고려 사항을 지원합니다."
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
ms.openlocfilehash: c502e4363dbaa37455d1aad90d1e9fa855fd09b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-security-center-planning-and-operations-guide"></a><span data-ttu-id="cc941-103">Azure 보안 센터 계획 및 작업 가이드</span><span class="sxs-lookup"><span data-stu-id="cc941-103">Azure Security Center planning and operations guide</span></span>
<span data-ttu-id="cc941-104">이 가이드는 Azure Security Center의 사용을 계획 중인 정보 기술(IT) 전문가, IT 설계자, 정보 보안 분석가 및 클라우드 관리자를 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-104">This guide is for information technology (IT) professionals, IT architects, information security analysts, and cloud administrators whose organizations are planning to use Azure Security Center.</span></span>

>[!NOTE] 
><span data-ttu-id="cc941-105">2017년 6월 초를 시작으로 Security Center는 Microsoft Monitoring Agent를 사용하여 데이터를 수집 및 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-105">Beginning in early June 2017, Security Center will use the Microsoft Monitoring Agent to collect and store data.</span></span> <span data-ttu-id="cc941-106">자세한 내용은 [Azure Security Center 플랫폼 마이그레이션](security-center-platform-migration.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc941-106">See [Azure Security Center Platform Migration](security-center-platform-migration.md) to learn more.</span></span> <span data-ttu-id="cc941-107">이 문서의 정보는 Microsoft Monitoring Agent로 전환된 후의 Security Center 기능을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-107">The information in this article represents Security Center functionality after transition to the Microsoft Monitoring Agent.</span></span>
>

## <a name="planning-guide"></a><span data-ttu-id="cc941-108">계획 가이드</span><span class="sxs-lookup"><span data-stu-id="cc941-108">Planning guide</span></span>
<span data-ttu-id="cc941-109">이 가이드에서는 조직의 보안 요구 사항과 클라우드 관리 모델에 따라 보안 센터의 사용을 최적화하기 위해 따를 수 있는 일련의 단계 및 작업을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-109">This guide covers a set of steps and tasks that you can follow to optimize your use of Security Center based on your organization’s security requirements and cloud management model.</span></span> <span data-ttu-id="cc941-110">Security Center를 완벽하게 활용하려면 조직의 서로 다른 개인 또는 팀이 보안 개발 및 운영, 모니터링, 관리 및 사고 대응 요구에 맞게 서비스를 사용하는 방법에 대해 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-110">To take full advantage of Security Center, it is important to understand how different individuals or teams in your organization use the service to meet secure development and operations, monitoring, governance, and incident response needs.</span></span> <span data-ttu-id="cc941-111">보안 센터의 사용을 계획할 때 고려할 주요 영역은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-111">The key areas to consider when planning to use Security Center are:</span></span>

* <span data-ttu-id="cc941-112">보안 역할 및 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="cc941-112">Security Roles and Access Controls</span></span>
* <span data-ttu-id="cc941-113">보안 정책 및 권장 사항</span><span class="sxs-lookup"><span data-stu-id="cc941-113">Security Policies and Recommendations</span></span>
* <span data-ttu-id="cc941-114">데이터 수집 및 저장</span><span class="sxs-lookup"><span data-stu-id="cc941-114">Data Collection and Storage</span></span>
* <span data-ttu-id="cc941-115">지속적인 보안 모니터링</span><span class="sxs-lookup"><span data-stu-id="cc941-115">Ongoing Security Monitoring</span></span>
* <span data-ttu-id="cc941-116">사고 대응</span><span class="sxs-lookup"><span data-stu-id="cc941-116">Incident Response</span></span>

<span data-ttu-id="cc941-117">다음 섹션에서는 요구 사항에 따라 이러한 각각의 영역을 계획하고 권장 사항을 적용하는 방법에 대해 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-117">In the next section, you will learn how to plan for each one of those areas and apply those recommendations based on your requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="cc941-118">[Azure 보안 센터 FAQ(질문과 대답)](security-center-faq.md) 설계 및 계획 단계에서 유용할 수 있는 일반적인 질문의 목록을 읽어 보세요.</span><span class="sxs-lookup"><span data-stu-id="cc941-118">Read [Azure Security Center frequently asked questions (FAQ)](security-center-faq.md) for a list of common questions that can also be useful during the designing and planning phase.</span></span>
> 

## <a name="security-roles-and-access-controls"></a><span data-ttu-id="cc941-119">보안 역할 및 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="cc941-119">Security roles and access controls</span></span>
<span data-ttu-id="cc941-120">조직의 규모와 구조에 따라, 여러 개인과 팀이 보안 센터를 통해 서로 다른 보안 관련 업무를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-120">Depending on the size and structure of your organization, multiple individuals and teams may use Security Center to perform different security-related tasks.</span></span> <span data-ttu-id="cc941-121">다음 다이어그램에는 가상의 사용자와 그 역할 및 보안 책임의 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-121">In the following diagram you have an example of fictitious personas and their respective roles and security responsibilities:</span></span>

![역할](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig01-new.png)

<span data-ttu-id="cc941-123">이러한 개인들은 보안 센터를 통해 다양한 책임에 부합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-123">Security Center enables these individuals to meet these various responsibilities.</span></span> <span data-ttu-id="cc941-124">예:</span><span class="sxs-lookup"><span data-stu-id="cc941-124">For example:</span></span>

<span data-ttu-id="cc941-125">**Jeff(클라우드 워크로드 소유자)**</span><span class="sxs-lookup"><span data-stu-id="cc941-125">**Jeff (Cloud Workload Owner)**</span></span>

* <span data-ttu-id="cc941-126">클라우드 워크로드와 관련 리소스를 관리</span><span class="sxs-lookup"><span data-stu-id="cc941-126">Manage a cloud workload and its related resources</span></span>
* <span data-ttu-id="cc941-127">회사 보안 정책에 따라 보호를 구현하고 유지 관리하는 업무를 담당</span><span class="sxs-lookup"><span data-stu-id="cc941-127">Responsible for implementing and maintaining protections in accordance with company security policy</span></span>

<span data-ttu-id="cc941-128">**Ellen(CISO/CIO)**</span><span class="sxs-lookup"><span data-stu-id="cc941-128">**Ellen (CISO/CIO)**</span></span>

* <span data-ttu-id="cc941-129">회사의 모든 보안 업무를 담당</span><span class="sxs-lookup"><span data-stu-id="cc941-129">Responsible for all aspects of security for the company</span></span>
* <span data-ttu-id="cc941-130">클라우드 워크로드에 걸쳐 회사의 보안 태세를 파악하고자 함</span><span class="sxs-lookup"><span data-stu-id="cc941-130">Wants to understand the company's security posture across cloud workloads</span></span>
* <span data-ttu-id="cc941-131">주요 공격 및 위험에 대해 숙지해야 함</span><span class="sxs-lookup"><span data-stu-id="cc941-131">Needs to be informed of major attacks and risks</span></span>

<span data-ttu-id="cc941-132">**David(IT 보안)**</span><span class="sxs-lookup"><span data-stu-id="cc941-132">**David (IT Security)**</span></span>

* <span data-ttu-id="cc941-133">적절한 보호 조치가 마련되도록 회사 보안 정책을 설정</span><span class="sxs-lookup"><span data-stu-id="cc941-133">Sets company security policies to ensure the appropriate protections are in place</span></span>
* <span data-ttu-id="cc941-134">정책 준수 여부를 모니터링</span><span class="sxs-lookup"><span data-stu-id="cc941-134">Monitors compliance with policies</span></span>
* <span data-ttu-id="cc941-135">경영진 또는 감사를 위한 보고서를 작성</span><span class="sxs-lookup"><span data-stu-id="cc941-135">Generates reports for leadership or auditors</span></span>

<span data-ttu-id="cc941-136">**Judy(보안 운영)**</span><span class="sxs-lookup"><span data-stu-id="cc941-136">**Judy (Security Operations)**</span></span>

* <span data-ttu-id="cc941-137">보안 경고를 연중무휴(24/7) 모니터링하고 대응</span><span class="sxs-lookup"><span data-stu-id="cc941-137">Monitors and responds to security alerts 24/7</span></span>
* <span data-ttu-id="cc941-138">클라우드 워크로드 소유자 또는 IT 보안 분석가에게 보안 문제 제기</span><span class="sxs-lookup"><span data-stu-id="cc941-138">Escalates to Cloud Workload Owner or IT Security Analyst</span></span>

<span data-ttu-id="cc941-139">**Sam(보안 분석가)**</span><span class="sxs-lookup"><span data-stu-id="cc941-139">**Sam (Security Analyst)**</span></span>

* <span data-ttu-id="cc941-140">공격 여부 조사</span><span class="sxs-lookup"><span data-stu-id="cc941-140">Investigate attacks</span></span>
* <span data-ttu-id="cc941-141">클라우드 워크로드 소유자와 함께 해결책 적용</span><span class="sxs-lookup"><span data-stu-id="cc941-141">Work with Cloud Workload Owner to apply remediation</span></span> 

<span data-ttu-id="cc941-142">Security Center는 Azure에서 사용자, 그룹 및 서비스에 [기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)을 제공하는 [RBAC(역할 기반 액세스 제어)](../active-directory/role-based-access-control-configure.md)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-142">Security Center uses [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md), which provides [built-in roles](../active-directory/role-based-access-built-in-roles.md) that can be assigned to users, groups, and services in Azure.</span></span> <span data-ttu-id="cc941-143">사용자가 Security Center를 열면 액세스한 리소스와 관련된 정보만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-143">When a user opens Security Center, they only see information related to resources they have access to.</span></span> <span data-ttu-id="cc941-144">이는 구독 또는 리소스가 속한 리소스 그룹에 대한 소유자, 참가자 또는 읽기 권한자의 역할이 사용자에게 할당된다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-144">Which means the user is assigned the role of Owner, Contributor, or Reader to the subscription or resource group that a resource belongs to.</span></span> <span data-ttu-id="cc941-145">이러한 역할 외에도 두 개의 특정한 Security Center 역할이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-145">In addition to these roles, there are two specific Security Center roles:</span></span>

- <span data-ttu-id="cc941-146">**보안 읽기 권한자**: 이 역할에 속하는 사용자는 권장 사항, 경고, 정책 및 상태를 포함하여 Security Center에 대한 권한을 볼 수 있지만 변경할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-146">**Security reader**: user that belongs to this role is be able to view rights to Security Center, which includes recommendations, alerts, policy, and health, but it won't be able to make changes.</span></span>
- <span data-ttu-id="cc941-147">**보안 관리자**: 보안 읽기 권한자와 동일하지만 보안 정책을 업데이트하고 권장 사항 및 경고를 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-147">**Security admin**: same as security reader but it can also update the security policy, dismiss recommendations and alerts.</span></span>

<span data-ttu-id="cc941-148">위에서 설명한 Security Center 역할은 Storage, 웹 및 모바일, 사물 인터넷 등 Azure의 다른 서비스 영역에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-148">The Security Center roles described above do not have access to other service areas of Azure such as Storage, Web & Mobile, or Internet of Things.</span></span>  

> [!NOTE]
> <span data-ttu-id="cc941-149">사용자는 적어도 Azure에서 Security Center를 볼 수 있는 구독, 리소스 그룹 소유자 또는 참가자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-149">A user needs to be at least a subscription, resource group owner, or contributor to be able to see Security Center in Azure.</span></span> 
> 
> 

<span data-ttu-id="cc941-150">이전 다이어그램에 설명된 가상 사용자를 사용하는 경우 다음 RBAC가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-150">Using the personas explained in the previous diagram, the following RBAC would be needed:</span></span>

<span data-ttu-id="cc941-151">**Jeff(클라우드 워크로드 소유자)**</span><span class="sxs-lookup"><span data-stu-id="cc941-151">**Jeff (Cloud Workload Owner)**</span></span>

* <span data-ttu-id="cc941-152">리소스 그룹 소유자/협업자</span><span class="sxs-lookup"><span data-stu-id="cc941-152">Resource Group Owner/Collaborator</span></span>

<span data-ttu-id="cc941-153">**David(IT 보안)**</span><span class="sxs-lookup"><span data-stu-id="cc941-153">**David (IT Security)**</span></span>

* <span data-ttu-id="cc941-154">구독 소유자/협력자 또는 보안 관리자</span><span class="sxs-lookup"><span data-stu-id="cc941-154">Subscription Owner/Collaborator or Security Admin</span></span>

<span data-ttu-id="cc941-155">**Judy(보안 운영)**</span><span class="sxs-lookup"><span data-stu-id="cc941-155">**Judy (Security Operations)**</span></span>

* <span data-ttu-id="cc941-156">경고를 보는 구독 읽기 권한자 또는 보안 읽기 권한자</span><span class="sxs-lookup"><span data-stu-id="cc941-156">Subscription Reader or Security Reader to view Alerts</span></span>
* <span data-ttu-id="cc941-157">경고를 해제하는 데 필요한 구독 소유자/협력자 또는 보안 관리자</span><span class="sxs-lookup"><span data-stu-id="cc941-157">Subscription Owner/Collaborator or Security Admin required to dismiss Alerts</span></span>

<span data-ttu-id="cc941-158">**Sam(보안 분석가)**</span><span class="sxs-lookup"><span data-stu-id="cc941-158">**Sam (Security Analyst)**</span></span>

* <span data-ttu-id="cc941-159">경고를 보는 구독 읽기 권한자</span><span class="sxs-lookup"><span data-stu-id="cc941-159">Subscription Reader to view Alerts</span></span>
* <span data-ttu-id="cc941-160">경고를 해제하는 데 필요한 구독 소유자/협력자</span><span class="sxs-lookup"><span data-stu-id="cc941-160">Subscription Owner/Collaborator required to dismiss Alerts</span></span>
* <span data-ttu-id="cc941-161">작업 영역에 대한 액세스가 필요할 수 있음</span><span class="sxs-lookup"><span data-stu-id="cc941-161">Access to the workspace may be required</span></span>

<span data-ttu-id="cc941-162">고려가 필요한 몇 가지 다른 중요 정보:</span><span class="sxs-lookup"><span data-stu-id="cc941-162">Some other important information to consider:</span></span>

* <span data-ttu-id="cc941-163">구독 소유자/참가자 및 보안 관리자만 보안 정책을 편집할 수 있음</span><span class="sxs-lookup"><span data-stu-id="cc941-163">Only subscription Owners/Contributors and Security Admins can edit a security policy</span></span>
* <span data-ttu-id="cc941-164">구독 및 리소스 그룹 소유자 및 참가자만 리소스에 대한 보안 권장 사항을 적용할 수 있음</span><span class="sxs-lookup"><span data-stu-id="cc941-164">Only subscription and resource group Owners and Contributors can apply security recommendations for a resource</span></span>

<span data-ttu-id="cc941-165">Security Center의 RBAC을 사용하여 액세스 제어를 계획하는 경우, Security Center를 사용할 조직 내 대상을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-165">When planning access control using RBAC for Security Center, be sure to understand who in your organization will be using Security Center.</span></span> <span data-ttu-id="cc941-166">또한 수행할 작업 유형을 확인한 다음 RBAC을 적합하게 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-166">Also, what types of tasks they will be performing and then configure RBAC accordingly.</span></span>

> [!NOTE]
> <span data-ttu-id="cc941-167">사용자가 자신의 작업을 완료하는 데 필요한 최소한의 역할을 할당하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-167">We recommend that you assign the least permissive role needed for users to complete their tasks.</span></span> <span data-ttu-id="cc941-168">예를 들어, 리소스의 보안 상태에 대한 정보를 보기만 하고 권장 사항 적용이나 정책 편집 등의 조치는 취하지 않는 사용자라면 읽기 권한자 역할을 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-168">For example, users who only need to view information about the security state of resources but not take action, such as applying recommendations or editing policies, should be assigned the Reader role.</span></span>
> 
> 

## <a name="security-policies-and-recommendations"></a><span data-ttu-id="cc941-169">보안 정책 및 권장 사항</span><span class="sxs-lookup"><span data-stu-id="cc941-169">Security policies and recommendations</span></span>
<span data-ttu-id="cc941-170">보안 정책은 지정된 구독 내에서 리소스에 대해 권장되는 제어 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-170">A security policy defines the set of controls, which are recommended for resources within the specified subscription.</span></span> <span data-ttu-id="cc941-171">보안 센터에서 회사의 보안 요구 사항 및 응용 프로그램 유형 또는 데이터 민감도에 따라 정책을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-171">In Security Center, you define policies according to your company's security requirements and the type of applications or sensitivity of the data.</span></span>

<span data-ttu-id="cc941-172">구독 수준에서 실행된 정책은 다음 다이어그램에 표시된 것처럼 구독 내 모든 리소스 그룹에 자동으로 전파됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-172">Policies that are enabled in the subscription level automatically propagate to all resources groups within the subscription as shown in the following diagram:</span></span>

![보안 정책](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig2-newUI.png)

> [!NOTE]
> <span data-ttu-id="cc941-174">어떤 정책이 변경되었는지 검토가 필요한 경우 [Azure 감사 로그](https://blogs.msdn.microsoft.com/cloud_solution_architect/2015/03/10/audit-logs-for-azure-events/)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-174">If you need to review which policies were changed, you can use [Azure Audit Logs](https://blogs.msdn.microsoft.com/cloud_solution_architect/2015/03/10/audit-logs-for-azure-events/).</span></span> <span data-ttu-id="cc941-175">정책 변경은 항상 Azure 감사 로그에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-175">Policy changes are always logged in Azure Audit Logs.</span></span>
> 
> 

### <a name="security-recommendations"></a><span data-ttu-id="cc941-176">보안 권장 사항</span><span class="sxs-lookup"><span data-stu-id="cc941-176">Security recommendations</span></span>
<span data-ttu-id="cc941-177">보안 정책을 구성하기 전에 각각의 [보안 권장 사항](security-center-recommendations.md)을 검토하여 이들 정책이 다양한 구독 및 리소스 그룹에 적합한지 판단합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-177">Before configuring security policies, review each of the [security recommendations](security-center-recommendations.md), and determine whether these policies are appropriate for your various subscriptions and resource groups.</span></span> <span data-ttu-id="cc941-178">[보안 권장 사항](https://docs.microsoft.com/en-us/azure/security-center/security-center-recommendations)을 확인하기 위해 취해야 하는 조치 및 조직에서 새 권장 사항을 모니터링하고 필요한 단계를 수행하는 담당자를 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-178">It is also important to understand what action should be taken to address [Security Recommendations](https://docs.microsoft.com/en-us/azure/security-center/security-center-recommendations) and who in your organization will be responsible for monitoring for new recommendations and taking the needed steps.</span></span>

<span data-ttu-id="cc941-179">Security Center는 Azure 구독에 대한 보안 연락처 세부 정보를 제공하는 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-179">Security Center will recommend that you provide security contact details for your Azure subscription.</span></span> <span data-ttu-id="cc941-180">이 정보는 MSRC(Microsoft 보안 대응 센터)에서 불법적인 또는 권한 없는 당사자가 고객 데이터에 액세스한 것을 발견하는 경우 사용자에게 연락하기 위해 Microsoft에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-180">This information will be used by Microsoft to contact you if the Microsoft Security Response Center (MSRC) discovers that your customer data has been accessed by an unlawful or unauthorized party.</span></span> <span data-ttu-id="cc941-181">이 권장 사항을 사용하는 방법에 대한 자세한 내용은 [Azure Security Center에 보안 연락처 세부 정보 제공](security-center-provide-security-contact-details.md) 을 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="cc941-181">Read [Provide security contact details in Azure Security Center](security-center-provide-security-contact-details.md) for more information on how to enable this recommendation.</span></span>

## <a name="data-collection-and-storage"></a><span data-ttu-id="cc941-182">데이터 수집 및 저장</span><span class="sxs-lookup"><span data-stu-id="cc941-182">Data collection and storage</span></span>
<span data-ttu-id="cc941-183">Azure Security Center는 가상 컴퓨터에서 보안 데이터를 수집하는 데 Microsoft Monitoring Agent를 사용하며 이는 Operations Management Suite 및 Log Analytics 서비스에서 사용하는 동일한 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-183">Azure Security Center uses the Microsoft Monitoring Agent – this is the same agent used by the Operations Management Suite and Log Analytics service – to collect security data from your virtual machines.</span></span> <span data-ttu-id="cc941-184">이 에이전트에서 수집된 데이터는 Log Analytics 작업 영역에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-184">Data collected from this agent will be stored in your Log Analytics workspace(s).</span></span>

### <a name="agent"></a><span data-ttu-id="cc941-185">에이전트</span><span class="sxs-lookup"><span data-stu-id="cc941-185">Agent</span></span>

<span data-ttu-id="cc941-186">데이터 수집이 보안 정책에서 활성화된 후에 Microsoft Monitoring Agent([Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents) 또는 [Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents)용)는 지원되는 모든 Azure VM 및 새로 만들어진 VM에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-186">After data collection is enabled in the security policy, the Microsoft Monitoring Agent (for [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents) or [Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents)) is installed on all supported Azure VMs and any new ones that are created.</span></span>  <span data-ttu-id="cc941-187">VM이 Microsoft Monitoring Agent에 이미 설치된 경우 Azure Security Center는 현재 설치된 에이전트를 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-187">If the VM already has the Microsoft Monitoring Agent installed, Azure Security Center will leverage the current installed agent.</span></span> <span data-ttu-id="cc941-188">에이전트의 프로세스는 사용자 작업에 영향을 미치지 않으며 VM의 성능에도 거의 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-188">The agent’s process is designed to be non-invasive and have very minimal impact on VM performance.</span></span>

<span data-ttu-id="cc941-189">Windows용 Microsoft Monitoring Agent는 TCP 포트 443을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-189">The Microsoft Monitoring Agent for Windows requires use TCP port 443.</span></span> <span data-ttu-id="cc941-190">추가 세부 정보는 [문제 해결 문서](security-center-troubleshooting-guide.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc941-190">See the [Troubleshooting article](security-center-troubleshooting-guide.md) for additional details.</span></span>

<span data-ttu-id="cc941-191">데이터 수집을 사용하지 않으려는 특정 지점의 경우 보안 정책에서 수집을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-191">If at some point you want to disable Data Collection, you can turn it off in the security policy.</span></span> <span data-ttu-id="cc941-192">그러나 다른 Azure Management 및 모니터링 서비스에서 Microsoft Monitoring Agent를 사용할 수 있기 때문에 Security Center에서 데이터 수집을 끄는 경우에도 자동으로 에이전트를 제거하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-192">However, because the Microsoft Monitoring Agent may be used by other Azure management and monitoring services, the agent will not be uninstalled automatically when you turn off data collection in  Security Center.</span></span> <span data-ttu-id="cc941-193">필요한 경우 에이전트를 수동으로 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-193">You can manually uninstall the agent if needed.</span></span>

> [!NOTE]
> <span data-ttu-id="cc941-194">지원되는 VM 목록을 찾아보려면 [Azure Security Center FAQ](security-center-faq.md)를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="cc941-194">To find a list of supported VMs, read the [Azure Security Center frequently asked questions (FAQ)](security-center-faq.md).</span></span>
> 

### <a name="workspace"></a><span data-ttu-id="cc941-195">작업 영역</span><span class="sxs-lookup"><span data-stu-id="cc941-195">Workspace</span></span>

<span data-ttu-id="cc941-196">(Azure Security Center 대신) Microsoft Monitoring Agent에서 수집된 데이터는 VM의 지역을 고려하여 Azure 구독 또는 새 작업 영역에 연결된 기존 Log Analytics 작업 영역 중 하나에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-196">Data collected from the Microsoft Monitoring Agent (on behalf of Azure Security Center) will be stored in either an existing Log Analytics workspace(s) associated with your Azure subscription or a new workspace(s), taking into account the Geo of the VM.</span></span> 

<span data-ttu-id="cc941-197">Azure Portal에서 Azure Security Center에서 만든 항목을 포함하여 Log Analytics 작업 영역 목록을 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-197">In the Azure portal, you can browse to see a list of your Log Analytics workspaces, including any created by Azure Security Center.</span></span> <span data-ttu-id="cc941-198">새 작업 영역에 관련된 리소스 그룹이 만들어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-198">A related resource group will be created for new workspaces.</span></span> <span data-ttu-id="cc941-199">둘 다 다음과 같은 명명 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-199">Both will follow this naming convention:</span></span> 

* <span data-ttu-id="cc941-200">작업 영역: *DefaultWorkspace-[subscription-ID]-[geo]*</span><span class="sxs-lookup"><span data-stu-id="cc941-200">Workspace: *DefaultWorkspace-[subscription-ID]-[geo]*</span></span>
* <span data-ttu-id="cc941-201">리소스 그룹: *DefaultResouceGroup-[geo]*</span><span class="sxs-lookup"><span data-stu-id="cc941-201">Resource Group: *DefaultResouceGroup-[geo]*</span></span>

<span data-ttu-id="cc941-202">Azure Security Center에서 만든 작업 영역의 경우 데이터는 30일 동안 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-202">For workspaces created by Azure Security Center, data is retained for 30 days.</span></span> <span data-ttu-id="cc941-203">기존 작업 영역의 경우 작업 영역 가격 책정 계층에 따라 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-203">For exiting workspaces, retention is based on the workspace pricing tier.</span></span>

> [!NOTE]
> <span data-ttu-id="cc941-204">Microsoft는 이 데이터의 개인 정보 및 보안을 보호하기 위해 노력하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-204">Microsoft make strong commitments to protect the privacy and security of this data.</span></span> <span data-ttu-id="cc941-205">Microsoft는 코딩부터 서비스에 이르기까지 엄격한 규정 준수 및 보안 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-205">Microsoft adheres to strict compliance and security guidelines—from coding to operating a service.</span></span> <span data-ttu-id="cc941-206">데이터 처리 및 개인 정보 보호에 대한 자세한 내용은 [Azure Security Center 데이터 보안](security-center-data-security.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc941-206">For more information about data handling and privacy, read [Azure Security Center Data Security](security-center-data-security.md).</span></span>
> 

## <a name="ongoing-security-monitoring"></a><span data-ttu-id="cc941-207">지속적인 보안 모니터링</span><span class="sxs-lookup"><span data-stu-id="cc941-207">Ongoing security monitoring</span></span>
<span data-ttu-id="cc941-208">보안 센터 권장 사항의 최초 구성과 적용 후에는 보안 센터 운영 프로세스를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-208">After initial configuration and application of Security Center recommendations, the next step is considering Security Center operational processes.</span></span>

<span data-ttu-id="cc941-209">Azure 포털에서 Security Center에 액세스하려면 **찾아보기**를 클릭하고 **필터** 필드에 **Security Center**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-209">To access Security Center from the Azure portal you can click **Browse** and type **Security Center** in the **Filter** field.</span></span> <span data-ttu-id="cc941-210">사용자가 사용하는 보기는 이렇게 적용된 필터에 따라 다릅니다. 아래 예제에서는 많은 문제를 해결해야 하는 환경을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-210">The views that the user gets are according to these applied filters, the example below shows an environment with many issues to be addressed:</span></span>

![dashboard](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig6.png)

> [!NOTE]
> <span data-ttu-id="cc941-212">Security Center는 일반 작동 프로시저를 방해하지 않으면서 배포를 소극적으로 모니터링하고 사용자가 설정한 보안 정책에 따라 권장 사항을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-212">Security Center will not interfere with your normal operational procedures, it will passively monitor your deployments and provide recommendations based on the security policies you enabled.</span></span>

<span data-ttu-id="cc941-213">현재 Azure 환경에 Security Center를 사용하도록 처음으로 설정할 때는 모든 권장 사항을 검토해야 합니다. 이 작업은 **권장 사항** 타일에서 또는 리소스별(**계산**, **네트워킹**, **저장소 및 데이터**, **응용 프로그램**)로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-213">When you first opt in to use Security Center for your current Azure environment, make sure that you review all recommendations, which can be done in the **Recommendations** tile or per resource (**Compute**, **Networking**, **Storage & data**, **Application**).</span></span>

<span data-ttu-id="cc941-214">모든 권장 사항을 해결한 후에는 해결된 모든 리소스에 대해 **방지** 섹션이 녹색이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-214">Once you address all recommendations, the **Prevention** section should be green for all resources that were addressed.</span></span> <span data-ttu-id="cc941-215">이 시점에서는 리소스 보안 상태와 권장 사항 타일에서의 변경 사항을 기준으로 조치를 취하면 되므로 지속적인 모니터링이 더 용이해집니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-215">Ongoing monitoring at this point becomes easier since you will only take actions based on changes in the resource security health and recommendations tiles.</span></span>

<span data-ttu-id="cc941-216">**감지** 섹션은 더 대응적인 부분으로, 지금 발생 중이거나 과거에 발생하여 Security Center 컨트롤과 타사 시스템에서 감지된 문제와 관련한 경고입니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-216">The **Detection** section is more reactive, these are alerts regarding issues that are either taking place now, or occurred in the past and were detected by Security Center controls and 3rd party systems.</span></span> <span data-ttu-id="cc941-217">보안 경고 타일은 매일 확인된 위협 감지의 수를 나타내는 막대 그래프와, 여러 심각도 카테고리(낮음, 중간, 높음) 간의 분포를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-217">The Security Alerts tile will show bar graphs that represent the number of threat detection alerts that were found in each day, and their distribution among the different severity categories (low, medium, high).</span></span> <span data-ttu-id="cc941-218">보안 경고에 대한 자세한 내용은 [Azure Security Center에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md)을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="cc941-218">For more information about Security Alerts, read [Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md).</span></span>

> [!NOTE]
> <span data-ttu-id="cc941-219">Microsoft Power BI를 활용하여 Security Center 데이터를 시각화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-219">You can also leverage Microsoft Power BI to visualize your Security Center data.</span></span> <span data-ttu-id="cc941-220">[Power BI로 Azure Security Center 데이터에서 정보 얻기](security-center-powerbi.md)를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="cc941-220">Read [Get insights from Azure Security Center data with Power BI](security-center-powerbi.md).</span></span>
> 
> 

### <a name="monitoring-for-new-or-changed-resources"></a><span data-ttu-id="cc941-221">새 또는 변경된 리소스 모니터링</span><span class="sxs-lookup"><span data-stu-id="cc941-221">Monitoring for new or changed resources</span></span>
<span data-ttu-id="cc941-222">대부분의 Azure 환경은 동적이며, 새 리소스가 일정 기준, 구성 또는 변경에 따라 확장 및 분리됩니다. Security Center는 이러한 새 리소스의 보안 상태에 대한 정보를 얻는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-222">Most Azure environments are dynamic, with new resources being spun up and down on a regular basis, configurations or changes, etc. Security Center helps ensure that you have visibility into the security state of these new resources.</span></span>

<span data-ttu-id="cc941-223">Azure 환경에 새 리소스(VM, SQL DB)를 추가하면 보안 센터가 자동으로 해당 리소스를 감지하고 보안을 모니터링하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-223">When you add new resources (VMs, SQL DBs) to your Azure Environment, Security Center will automatically discover these resources and begin to monitor their security.</span></span> <span data-ttu-id="cc941-224">또한 PaaS 웹 역할 및 작업자 역할이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-224">This also includes PaaS web roles and worker roles.</span></span> <span data-ttu-id="cc941-225">[보안 정책](security-center-policies.md)에서 데이터 수집을 사용하도록 설정한 경우 가상 컴퓨터에 대해 추가적인 모니터링 기능이 자동으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-225">If Data Collection is enabled in the [Security Policy](security-center-policies.md), additional monitoring capabilities will be enabled automatically for your virtual machines.</span></span>

![주요 영역](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig3-newUI.png)

1. <span data-ttu-id="cc941-227">가상 컴퓨터의 경우 **방지** 섹션에서 **계산**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-227">For virtual machines, click **Compute**, under **Prevention** section.</span></span> <span data-ttu-id="cc941-228">데이터를 사용하도록 설정하는 것과 관련한 문제나 관련 권장 사항은 **개요** 탭 및 **모니터링 권장 사항** 섹션에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-228">Any issues with enabling data or related recommendations will be surfaced in the **Overview** tab, and **Monitoring Recommendations** section.</span></span>
2. <span data-ttu-id="cc941-229">새 리소스에 대한 보안 위협이 있다면 무엇인지를 확인하기 위해 **권장 사항** 을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-229">View the **Recommendations** to see what, if any, security risks were identified for the new resource.</span></span>
3. <span data-ttu-id="cc941-230">새 VM이 환경에 추가되면 운영 체제만 최초로 설치되는 것이 매우 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-230">It is very common that when new VMs are added to your environment, only the operating system is initially installed.</span></span> <span data-ttu-id="cc941-231">리소스 소유자는 이러한 VM에서 사용할 다른 앱을 배포하는 데 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-231">The resource owner might need some time to deploy other apps that will be used by these VMs.</span></span>  <span data-ttu-id="cc941-232">이상적으로는 이 워크로드의 최종 목적을 파악하고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-232">Ideally, you should know the final intent of this workload.</span></span> <span data-ttu-id="cc941-233">응용 프로그램 서버가 됩니까?</span><span class="sxs-lookup"><span data-stu-id="cc941-233">Is it going to be an Application Server?</span></span> <span data-ttu-id="cc941-234">이 새 워크로드의 용도에 맞게 적절한 **보안 정책**을 사용하도록 설정할 수 있으며, 이 워크플로의 세 번째 단계에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-234">Based on what this new workload is going to be, you can enable the appropriate **Security Policy**, which is the third step in this workflow.</span></span>
4. <span data-ttu-id="cc941-235">새 리소스가 Azure 환경에 추가되면 **보안 경고** 타일에 새 경고가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-235">As new resources are added to your Azure environment, it is possible that new alerts appear in the **Security Alerts** tile.</span></span> <span data-ttu-id="cc941-236">항상 이 타일에 새 경고가 있는지 확인하고 보안 센터 권장 사항에 따라 조치를 취합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-236">Always verify if there are new alerts in this tile and take actions according to Security Center recommendations.</span></span>

<span data-ttu-id="cc941-237">또한 기존 리소스 상태를 정기적으로 모니터링하여 보안 위험을 초래하고 권장 기준에 미치지 못하는 구성 변경 내용과 보안 경고를 파악하고자 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-237">You will also want to regularly monitor the state of existing resources to identify configuration changes that have created security risks, drift from recommended baselines, and security alerts.</span></span> <span data-ttu-id="cc941-238">보안 센터 대시보드에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-238">Start at the Security Center dashboard.</span></span> <span data-ttu-id="cc941-239">여기에서는 일관된 기준에 따라 3가지 주요 영역을 검토하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-239">From there you have three major areas to review on a consistent basis.</span></span>

![작업](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig4-newUI.png)

1. <span data-ttu-id="cc941-241">**방지** 섹션 패널은 주요 리소스에 대한 신속한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-241">The **Prevention** section panel provides you quick access to your key resources.</span></span> <span data-ttu-id="cc941-242">이 옵션을 사용하여 계산, 네트워킹, 저장소와 데이터 및 응용 프로그램을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-242">Use this option to monitor Compute, Networking, Storage & data and Applications.</span></span>
2. <span data-ttu-id="cc941-243">**권장 사항** 패널에서 Security Center 권장 사항을 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-243">The **Recommendations** panel enables you to review Security Center recommendations.</span></span> <span data-ttu-id="cc941-244">지속적인 모니터링이 이루어질 때는 매일 권장 사항이 있는 것이 아닙니다. 이것은 최초 Security Center 설정 시 모든 권장 사항을 해결했기 때문에 정상입니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-244">During your ongoing monitoring you may find that you don’t have recommendations on a daily basis, which is normal since you addressed all recommendations on the initial Security Center setup.</span></span> <span data-ttu-id="cc941-245">따라서 매일 이 섹션에 새 정보가 있는 것은 아니며 필요에 따라 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-245">For this reason, you may not have new information in this section every day and will just need to access it as needed.</span></span>
3. <span data-ttu-id="cc941-246">**감지** 섹션은 매우 자주 또는 매우 드물게 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-246">The **Detection** section might change on either a very frequent or very infrequent basis.</span></span> <span data-ttu-id="cc941-247">항상 보안 경고를 검토하고 보안 센터 권장 사항에 따라 조치를 취합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-247">Always review your security alerts and take actions based on Security Center recommendations.</span></span>

## <a name="incident-response"></a><span data-ttu-id="cc941-248">사고 대응</span><span class="sxs-lookup"><span data-stu-id="cc941-248">Incident response</span></span>
<span data-ttu-id="cc941-249">보안 센터는 위협이 발생하면 감지하여 사용자에게 경고합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-249">Security Center detects and alerts you to threats as they occur.</span></span> <span data-ttu-id="cc941-250">조직에서는 새 보안 경고를 모니터링하고 필요에 따라 조치를 통해 추가적인 조사를 수행하거나 공격에 대처해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-250">Organizations should monitor for new security alerts and take action as needed to investigate further or remediate the attack.</span></span> <span data-ttu-id="cc941-251">Security Center 위협 감지 기능이 작동하는 방법에 대한 자세한 내용은 [Azure Security Center 감지 기능](security-center-detection-capabilities.md)을 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="cc941-251">For more information on how Security Center threat detection works, read [Azure Security Center detection capabilities](security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="cc941-252">이 문서가 인시던트 대응 계획을 직접 작성하는 데 도움을 주려는 목적은 아니지만 인시던트 대응 단계에 대한 기반으로 클라우드 수명 주기에 Microsoft Azure 보안 응답을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-252">While this article doesn’t have the intent to assist you creating your own Incident Response plan, we are going to use Microsoft Azure Security Response in the Cloud lifecycle as the foundation for incident response stages.</span></span> <span data-ttu-id="cc941-253">단계는 다음 다이어그램에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-253">The stages are shown in the following diagram:</span></span>

![의심되는 활동](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-1.png)

> [!NOTE]
> <span data-ttu-id="cc941-255">자체 계획을 마련할 때는 NIST(National Institute of Standards and Technology) [컴퓨터 보안 인시던트 처리 가이드](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf) 를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-255">You can use the National Institute of Standards and Technology (NIST) [Computer Security Incident Handling Guide](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf) as a reference to assist you building your own.</span></span>
> 

<span data-ttu-id="cc941-256">다음 단계에서 보안 센터 경고를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-256">You can use Security Center Alerts during the following stages:</span></span>

* <span data-ttu-id="cc941-257">**감지**: 하나 이상의 리소스에서 의심스러운 작업을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-257">**Detect**: identify a suspicious activity in one or more resources.</span></span> 
* <span data-ttu-id="cc941-258">**평가**: 초기 평가를 수행하여 의심스러운 작업에 대한 자세한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-258">**Assess**: perform the initial assessment to obtain more information about the suspicious activity.</span></span>
* <span data-ttu-id="cc941-259">**진단**: 수정 단계를 사용하여 문제를 해결하는 기술 절차를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-259">**Diagnose**: use the remediation steps to conduct the technical procedure to address the issue.</span></span>

<span data-ttu-id="cc941-260">각 보안 경고는 공격의 근원을 더 잘 이해하는 데 도움이 될 수 있는 정보를 제공하며 가능한 해결 방법을 제안합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-260">Each Security Alert provides information that can be used to better understand the nature of the attack and suggest possible mitigations.</span></span> <span data-ttu-id="cc941-261">일부 경고에서는 Azure 내부의 타 정보원이나 다른 추가 정보에 대한 링크를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-261">Some alerts also provide links to either more information or to other sources of information within Azure.</span></span> <span data-ttu-id="cc941-262">완화를 시작하려면 다시 추가 검색에 제공되는 정보를 사용하고 작업 영역에 저장되어 있는 보안 관련 데이터를 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-262">You can use the information provided for further research and to begin mitigation, and you can also search security-related data that is stored in your workspace.</span></span>

<span data-ttu-id="cc941-263">다음 예제에서는 미심쩍은 RDP 활동이 발생하고 있음을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-263">The following example shows a suspicious RDP activity taking place:</span></span>

![의심되는 활동](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-ga.png)

<span data-ttu-id="cc941-265">여기에서 보듯이 이 블레이드는 공격 발생 시간, 소스 호스트 이름, 대상 VM과 관련한 자세한 내용을 표시하며 권장 절차를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-265">As you can see, this blade shows details regarding the time that the attack took place, the source hostname, the target VM and also gives recommendation steps.</span></span> <span data-ttu-id="cc941-266">일부 상황에서는 공격의 소스 정보가 비어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-266">In some circumstances the source information of the attack may be empty.</span></span> <span data-ttu-id="cc941-267">이러한 동작 유형에 대한 자세한 내용은 [Azure Security Center 경고에 누락된 원본 정보](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/25/missing-source-information-in-azure-security-center-alerts/) 를 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="cc941-267">Read [Missing Source Information in Azure Security Center Alerts](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/25/missing-source-information-in-azure-security-center-alerts/) for more information about this type of behavior.</span></span>

<span data-ttu-id="cc941-268">[사고 대응에 대해 Azure Security Center 및 Microsoft Operations Management Suite를 활용하는 방법](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703) 비디오를 통해 각 단계에서 Security Center를 사용할 수 있는 방식을 이해하는 데 도움이 되는 몇 가지 데모를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-268">In the [How to Leverage the Azure Security Center & Microsoft Operations Management Suite for an Incident Response](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703) video you can see some demonstrations that can help you to understand how Security Center can be used in each one of those stages.</span></span>

> [!NOTE]
> <span data-ttu-id="cc941-269">인시던트 대응 프로세스 중에 도움이 될 보안 센터 기능을 사용하는 방법에 대한 자세한 내용은 [인시던트 대응에 Azure Security Center 활용](security-center-incident-response.md) 을 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="cc941-269">Read [Leveraging Azure Security Center for Incident Response](security-center-incident-response.md) for more information on how to use Security Center capabilities to assist you during your Incident Response process.</span></span> 
> 
> 

## <a name="see-also"></a><span data-ttu-id="cc941-270">참고 항목</span><span class="sxs-lookup"><span data-stu-id="cc941-270">See also</span></span>
<span data-ttu-id="cc941-271">이 문서에서는 보안 센터를 도입하도록 계획하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-271">In this document, you learned how to plan for Security Center adoption.</span></span> <span data-ttu-id="cc941-272">보안 센터에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc941-272">To learn more about Security Center, see the following:</span></span>

* [<span data-ttu-id="cc941-273">Azure 보안 센터에서 보안 경고 관리 및 대응</span><span class="sxs-lookup"><span data-stu-id="cc941-273">Managing and responding to security alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* <span data-ttu-id="cc941-274">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) — Azure 리소스의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-274">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="cc941-275">[Azure Security Center를 사용하여 파트너 솔루션 모니터링](security-center-partner-solutions.md) — 파트너 솔루션의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-275">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) — Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="cc941-276">[Azure Security Center FAQ](security-center-faq.md) - 서비스 사용에 관한 질문과 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-276">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="cc941-277">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) - Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="cc941-277">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>

