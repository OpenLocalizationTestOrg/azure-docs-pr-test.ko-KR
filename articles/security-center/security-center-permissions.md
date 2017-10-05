---
title: "Azure Security Center의 권한 | Microsoft Docs"
description: "이 문서는 Azure Security Center가 역할 기반 액세스 제어를 사용하여 사용자에게 권한을 할당하는 방법과 각 역할에 대해 허용된 작업을 식별하는 방법에 대해 설명합니다."
services: security-center
cloud: na
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
ms.assetid: 
ms.service: security-center
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: terrylan
ms.openlocfilehash: 0aaa99dda44d2020afd3e841e84020eb4ff87a85
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="permissions-in-azure-security-center"></a><span data-ttu-id="e0b2d-103">Azure Security Center의 권한</span><span class="sxs-lookup"><span data-stu-id="e0b2d-103">Permissions in Azure Security Center</span></span>

<span data-ttu-id="e0b2d-104">Azure Security Center는 Azure에서 사용자, 그룹 및 서비스에 [기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)을 제공하는 [RBAC(역할 기반 액세스 제어)](../active-directory/role-based-access-control-configure.md)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2d-104">Azure Security Center uses [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md), which provides [built-in roles](../active-directory/role-based-access-built-in-roles.md) that can be assigned to users, groups, and services in Azure.</span></span>

<span data-ttu-id="e0b2d-105">Security Center는 리소스 구성을 평가하여 보안 문제 및 취약성을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2d-105">Security Center assesses the configuration of your resources to identify security issues and vulnerabilities.</span></span> <span data-ttu-id="e0b2d-106">Security Center에서는 리소스가 속한 구독이나 리소스 그룹에 대한 소유자, 참가자 또는 독자 역할을 할당 받을 때 리소스와 관련된 항목만 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2d-106">In Security Center, you only see information related to a resource when you are assigned the role of Owner, Contributor, or Reader for the subscription or resource group that a resource belongs to.</span></span>

<span data-ttu-id="e0b2d-107">이러한 역할 외에도 두 개의 특정한 Security Center 역할이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2d-107">In addition to these roles, there are two specific Security Center roles:</span></span>

* <span data-ttu-id="e0b2d-108">**보안 읽기 권한자**: 이 역할에 속하는 사용자는 Security Center에 대한 보기 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2d-108">**Security Reader**: A user that belongs to this role has viewing rights to Security Center.</span></span> <span data-ttu-id="e0b2d-109">사용자가 권장 사항, 경고, 보안 정책 및 보안 상태를 볼 수 있지만 변경할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2d-109">The user can view recommendations, alerts, a security policy, and security states, but cannot make changes.</span></span>
* <span data-ttu-id="e0b2d-110">**보안 관리자**: 이 역할에 속하는 사용자는 보안 읽기 권한자와 동일한 권한이 있으며 보안 정책을 업데이트하고 경고 및 권장 사항을 해제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2d-110">**Security Administrator**: A user that belongs to this role has the same rights as the Security Reader and can also update the security policy and dismiss alerts and recommendations.</span></span>

> [!NOTE]
> <span data-ttu-id="e0b2d-111">보안 역할(보안 읽기 권한자 및 보안 관리자)은 Security Center에만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2d-111">The security roles, Security Reader and Security Administrator, have access only in Security Center.</span></span> <span data-ttu-id="e0b2d-112">보안 역할은 Storage, 웹 및 모바일, 사물 인터넷 등 Azure의 다른 서비스 영역에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2d-112">The security roles do not have access to other service areas of Azure such as Storage, Web & Mobile, or Internet of Things.</span></span>
>
>

## <a name="roles-and-allowed-actions"></a><span data-ttu-id="e0b2d-113">역할 및 허용되는 작업</span><span class="sxs-lookup"><span data-stu-id="e0b2d-113">Roles and allowed actions</span></span>

<span data-ttu-id="e0b2d-114">다음 표는 Security Center의 역할 및 허용되는 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2d-114">The following table displays roles and allowed actions in Security Center.</span></span> <span data-ttu-id="e0b2d-115">X는 작업이 해당 역할에 대해 허용된다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2d-115">An X indicates that the action is allowed for that role.</span></span>

| <span data-ttu-id="e0b2d-116">역할</span><span class="sxs-lookup"><span data-stu-id="e0b2d-116">Role</span></span> | <span data-ttu-id="e0b2d-117">보안 정책 편집</span><span class="sxs-lookup"><span data-stu-id="e0b2d-117">Edit security policy</span></span> | <span data-ttu-id="e0b2d-118">리소스에 보안 권장 사항 적용</span><span class="sxs-lookup"><span data-stu-id="e0b2d-118">Apply security recommendations for a resource</span></span> | <span data-ttu-id="e0b2d-119">경고 및 권장 사항 해제</span><span class="sxs-lookup"><span data-stu-id="e0b2d-119">Dismiss alerts and recommendations</span></span> | <span data-ttu-id="e0b2d-120">경고 및 권장 사항 보기</span><span class="sxs-lookup"><span data-stu-id="e0b2d-120">View alerts and recommendations</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="e0b2d-121">구독 소유자</span><span class="sxs-lookup"><span data-stu-id="e0b2d-121">Subscription Owner</span></span> | <span data-ttu-id="e0b2d-122">X</span><span class="sxs-lookup"><span data-stu-id="e0b2d-122">X</span></span> | <span data-ttu-id="e0b2d-123">X</span><span class="sxs-lookup"><span data-stu-id="e0b2d-123">X</span></span> | <span data-ttu-id="e0b2d-124">X</span><span class="sxs-lookup"><span data-stu-id="e0b2d-124">X</span></span> | <span data-ttu-id="e0b2d-125">X</span><span class="sxs-lookup"><span data-stu-id="e0b2d-125">X</span></span> |
| <span data-ttu-id="e0b2d-126">구독 참가자</span><span class="sxs-lookup"><span data-stu-id="e0b2d-126">Subscription Contributor</span></span> | <span data-ttu-id="e0b2d-127">X</span><span class="sxs-lookup"><span data-stu-id="e0b2d-127">X</span></span> | <span data-ttu-id="e0b2d-128">X</span><span class="sxs-lookup"><span data-stu-id="e0b2d-128">X</span></span> | <span data-ttu-id="e0b2d-129">X</span><span class="sxs-lookup"><span data-stu-id="e0b2d-129">X</span></span> | <span data-ttu-id="e0b2d-130">X</span><span class="sxs-lookup"><span data-stu-id="e0b2d-130">X</span></span> |
| <span data-ttu-id="e0b2d-131">리소스 그룹 소유자</span><span class="sxs-lookup"><span data-stu-id="e0b2d-131">Resource Group Owner</span></span> | -- | <span data-ttu-id="e0b2d-132">X</span><span class="sxs-lookup"><span data-stu-id="e0b2d-132">X</span></span> | -- | <span data-ttu-id="e0b2d-133">X</span><span class="sxs-lookup"><span data-stu-id="e0b2d-133">X</span></span> |
| <span data-ttu-id="e0b2d-134">리소스 그룹 참가자</span><span class="sxs-lookup"><span data-stu-id="e0b2d-134">Resource Group Contributor</span></span> | -- | <span data-ttu-id="e0b2d-135">X</span><span class="sxs-lookup"><span data-stu-id="e0b2d-135">X</span></span> | -- | <span data-ttu-id="e0b2d-136">X</span><span class="sxs-lookup"><span data-stu-id="e0b2d-136">X</span></span> |
| <span data-ttu-id="e0b2d-137">판독기</span><span class="sxs-lookup"><span data-stu-id="e0b2d-137">Reader</span></span> | -- | -- | -- | <span data-ttu-id="e0b2d-138">X</span><span class="sxs-lookup"><span data-stu-id="e0b2d-138">X</span></span> |
| <span data-ttu-id="e0b2d-139">보안 관리자</span><span class="sxs-lookup"><span data-stu-id="e0b2d-139">Security Administrator</span></span> | <span data-ttu-id="e0b2d-140">X</span><span class="sxs-lookup"><span data-stu-id="e0b2d-140">X</span></span> | -- | <span data-ttu-id="e0b2d-141">X</span><span class="sxs-lookup"><span data-stu-id="e0b2d-141">X</span></span> | <span data-ttu-id="e0b2d-142">X</span><span class="sxs-lookup"><span data-stu-id="e0b2d-142">X</span></span> |
| <span data-ttu-id="e0b2d-143">보안 판독기</span><span class="sxs-lookup"><span data-stu-id="e0b2d-143">Security Reader</span></span> | -- | -- | -- | <span data-ttu-id="e0b2d-144">X</span><span class="sxs-lookup"><span data-stu-id="e0b2d-144">X</span></span> |

> [!NOTE]
> <span data-ttu-id="e0b2d-145">사용자가 자신의 작업을 완료하는 데 필요한 최소한의 역할을 할당하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2d-145">We recommend that you assign the least permissive role needed for users to complete their tasks.</span></span> <span data-ttu-id="e0b2d-146">예를 들어, 리소스의 보안 상태에 대한 정보를 보기만 하고 권장 사항 적용이나 정책 편집 등의 조치는 취하지 않는 사용자에게 독자 역할을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2d-146">For example, assign the Reader role to users who only need to view information about the security health of a resource but not take action, such as applying recommendations or editing policies.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="e0b2d-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e0b2d-147">Next steps</span></span>
<span data-ttu-id="e0b2d-148">이 문서는 Security Center에서 RBAC를 사용하여 사용자에게 사용 권한을 할당하고 각 역할에 대해 허용된 작업을 식별하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2d-148">This article explained how Security Center uses RBAC to assign permissions to users and identified the allowed actions for each role.</span></span> <span data-ttu-id="e0b2d-149">이제 구독의 보안 상태를 모니터링하고, 보안 정책을 편집하고, 권장 사항을 적용하는 데 필요한 역할 할당에 익숙해졌으므로 다음을 수행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e0b2d-149">Now that you're familiar with the role assignments needed to monitor the security state of your subscription, edit security policies, and apply recommendations, learn how to:</span></span>

- [<span data-ttu-id="e0b2d-150">Security Center에서 보안 정책 설정</span><span class="sxs-lookup"><span data-stu-id="e0b2d-150">Set security policies in Security Center</span></span>](security-center-policies.md)
- [<span data-ttu-id="e0b2d-151">Security Center의 보안 권장 사항 관리</span><span class="sxs-lookup"><span data-stu-id="e0b2d-151">Manage security recommendations in Security Center</span></span>](security-center-recommendations.md)
- [<span data-ttu-id="e0b2d-152">Azure 리소스의 보안 상태 모니터링</span><span class="sxs-lookup"><span data-stu-id="e0b2d-152">Monitor the security health of your Azure resources</span></span>](security-center-monitoring.md)
- [<span data-ttu-id="e0b2d-153">Security Center에서 보안 경고 관리 및 응답</span><span class="sxs-lookup"><span data-stu-id="e0b2d-153">Manage and respond to security alerts in Security Center</span></span>](security-center-managing-and-responding-alerts.md)
- [<span data-ttu-id="e0b2d-154">파트너 보안 솔루션 모니터링</span><span class="sxs-lookup"><span data-stu-id="e0b2d-154">Monitor partner security solutions</span></span>](security-center-partner-solutions.md)
