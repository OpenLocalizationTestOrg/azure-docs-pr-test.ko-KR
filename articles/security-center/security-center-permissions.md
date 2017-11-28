---
title: "Azure 보안 센터에서 aaaPermissions | Microsoft Docs"
description: "이 문서에서는 Azure 보안 센터 역할 기반 액세스 제어 tooassign 권한 toousers를 사용 하는 방법에 대해 설명 하 고 hello 허용 되는 각 역할에 대 한 작업을 식별 합니다."
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
ms.openlocfilehash: 03e16132dc3d951ef8ad9e86b9970b9e4d15c76b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-in-azure-security-center"></a><span data-ttu-id="65412-103">Azure Security Center의 권한</span><span class="sxs-lookup"><span data-stu-id="65412-103">Permissions in Azure Security Center</span></span>

<span data-ttu-id="65412-104">Azure 보안 센터를 사용 하 여 [역할 기반 액세스 제어 (RBAC)](../active-directory/role-based-access-control-configure.md)를 제공 하는 [기본 제공 역할](../active-directory/role-based-access-built-in-roles.md) toousers, 그룹 및 Azure 서비스에에서 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65412-104">Azure Security Center uses [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md), which provides [built-in roles](../active-directory/role-based-access-built-in-roles.md) that can be assigned toousers, groups, and services in Azure.</span></span>

<span data-ttu-id="65412-105">보안 센터의 리소스 tooidentify 보안 문제 및 취약점 hello 구성을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="65412-105">Security Center assesses hello configuration of your resources tooidentify security issues and vulnerabilities.</span></span> <span data-ttu-id="65412-106">보안 센터에만 정보를 확인할 때 hello 구독 또는 리소스 그룹에 속한 리소스에 대 한 소유자, 참가자 또는 판독기의 hello 역할이 할당 된 경우 tooa 리소스와 관련 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="65412-106">In Security Center, you only see information related tooa resource when you are assigned hello role of Owner, Contributor, or Reader for hello subscription or resource group that a resource belongs to.</span></span>

<span data-ttu-id="65412-107">또한 toothese 역할에는 두 개의 특정 보안 센터 역할이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65412-107">In addition toothese roles, there are two specific Security Center roles:</span></span>

* <span data-ttu-id="65412-108">**보안 판독기**: toothis 역할에 속하는 사용자에 게 권한 tooSecurity 센터 보기.</span><span class="sxs-lookup"><span data-stu-id="65412-108">**Security Reader**: A user that belongs toothis role has viewing rights tooSecurity Center.</span></span> <span data-ttu-id="65412-109">hello 사용자 권장 사항, 경고, 보안 정책 및 보안 상태를 볼 수 있지만 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="65412-109">hello user can view recommendations, alerts, a security policy, and security states, but cannot make changes.</span></span>
* <span data-ttu-id="65412-110">**보안 관리자**: toothis 역할에 속하는 사용자 hello 보안 판독기로 권한 같은 hello에 hello 보안 정책을 업데이트 하 고 수 경고 및 권장 사항을 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="65412-110">**Security Administrator**: A user that belongs toothis role has hello same rights as hello Security Reader and can also update hello security policy and dismiss alerts and recommendations.</span></span>

> [!NOTE]
> <span data-ttu-id="65412-111">hello 보안 역할, 보안 판독기 및 보안 관리자를 보안 센터에만 액세스할 수 있으며</span><span class="sxs-lookup"><span data-stu-id="65412-111">hello security roles, Security Reader and Security Administrator, have access only in Security Center.</span></span> <span data-ttu-id="65412-112">hello 보안 역할에 Azure 저장소, 웹 및 모바일, 사물 인터넷 등의 액세스 tooother 서비스 분야를 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="65412-112">hello security roles do not have access tooother service areas of Azure such as Storage, Web & Mobile, or Internet of Things.</span></span>
>
>

## <a name="roles-and-allowed-actions"></a><span data-ttu-id="65412-113">역할 및 허용되는 작업</span><span class="sxs-lookup"><span data-stu-id="65412-113">Roles and allowed actions</span></span>

<span data-ttu-id="65412-114">hello 다음 표에서 역할을 표시 하 고 허용 되는 보안 센터에서 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="65412-114">hello following table displays roles and allowed actions in Security Center.</span></span> <span data-ttu-id="65412-115">X가 해당 역할에 대 한 hello 작업 허용 됨을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="65412-115">An X indicates that hello action is allowed for that role.</span></span>

| <span data-ttu-id="65412-116">역할</span><span class="sxs-lookup"><span data-stu-id="65412-116">Role</span></span> | <span data-ttu-id="65412-117">보안 정책 편집</span><span class="sxs-lookup"><span data-stu-id="65412-117">Edit security policy</span></span> | <span data-ttu-id="65412-118">리소스에 보안 권장 사항 적용</span><span class="sxs-lookup"><span data-stu-id="65412-118">Apply security recommendations for a resource</span></span> | <span data-ttu-id="65412-119">경고 및 권장 사항 해제</span><span class="sxs-lookup"><span data-stu-id="65412-119">Dismiss alerts and recommendations</span></span> | <span data-ttu-id="65412-120">경고 및 권장 사항 보기</span><span class="sxs-lookup"><span data-stu-id="65412-120">View alerts and recommendations</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="65412-121">구독 소유자</span><span class="sxs-lookup"><span data-stu-id="65412-121">Subscription Owner</span></span> | <span data-ttu-id="65412-122">X</span><span class="sxs-lookup"><span data-stu-id="65412-122">X</span></span> | <span data-ttu-id="65412-123">X</span><span class="sxs-lookup"><span data-stu-id="65412-123">X</span></span> | <span data-ttu-id="65412-124">X</span><span class="sxs-lookup"><span data-stu-id="65412-124">X</span></span> | <span data-ttu-id="65412-125">X</span><span class="sxs-lookup"><span data-stu-id="65412-125">X</span></span> |
| <span data-ttu-id="65412-126">구독 참가자</span><span class="sxs-lookup"><span data-stu-id="65412-126">Subscription Contributor</span></span> | <span data-ttu-id="65412-127">X</span><span class="sxs-lookup"><span data-stu-id="65412-127">X</span></span> | <span data-ttu-id="65412-128">X</span><span class="sxs-lookup"><span data-stu-id="65412-128">X</span></span> | <span data-ttu-id="65412-129">X</span><span class="sxs-lookup"><span data-stu-id="65412-129">X</span></span> | <span data-ttu-id="65412-130">X</span><span class="sxs-lookup"><span data-stu-id="65412-130">X</span></span> |
| <span data-ttu-id="65412-131">리소스 그룹 소유자</span><span class="sxs-lookup"><span data-stu-id="65412-131">Resource Group Owner</span></span> | -- | <span data-ttu-id="65412-132">X</span><span class="sxs-lookup"><span data-stu-id="65412-132">X</span></span> | -- | <span data-ttu-id="65412-133">X</span><span class="sxs-lookup"><span data-stu-id="65412-133">X</span></span> |
| <span data-ttu-id="65412-134">리소스 그룹 참가자</span><span class="sxs-lookup"><span data-stu-id="65412-134">Resource Group Contributor</span></span> | -- | <span data-ttu-id="65412-135">X</span><span class="sxs-lookup"><span data-stu-id="65412-135">X</span></span> | -- | <span data-ttu-id="65412-136">X</span><span class="sxs-lookup"><span data-stu-id="65412-136">X</span></span> |
| <span data-ttu-id="65412-137">판독기</span><span class="sxs-lookup"><span data-stu-id="65412-137">Reader</span></span> | -- | -- | -- | <span data-ttu-id="65412-138">X</span><span class="sxs-lookup"><span data-stu-id="65412-138">X</span></span> |
| <span data-ttu-id="65412-139">보안 관리자</span><span class="sxs-lookup"><span data-stu-id="65412-139">Security Administrator</span></span> | <span data-ttu-id="65412-140">X</span><span class="sxs-lookup"><span data-stu-id="65412-140">X</span></span> | -- | <span data-ttu-id="65412-141">X</span><span class="sxs-lookup"><span data-stu-id="65412-141">X</span></span> | <span data-ttu-id="65412-142">X</span><span class="sxs-lookup"><span data-stu-id="65412-142">X</span></span> |
| <span data-ttu-id="65412-143">보안 판독기</span><span class="sxs-lookup"><span data-stu-id="65412-143">Security Reader</span></span> | -- | -- | -- | <span data-ttu-id="65412-144">X</span><span class="sxs-lookup"><span data-stu-id="65412-144">X</span></span> |

> [!NOTE]
> <span data-ttu-id="65412-145">Hello를 할당 하는 것이 좋습니다 사이의 역할 작업 사용자 toocomplete에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="65412-145">We recommend that you assign hello least permissive role needed for users toocomplete their tasks.</span></span> <span data-ttu-id="65412-146">예를 들어 권장 사항을 적용 하거나 정책 편집 등의 작업을 사용 하지는 않지만 hello 보안 상태에 대 한 리소스의 tooview 정보 하기만 hello 판독기 역할 toousers를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="65412-146">For example, assign hello Reader role toousers who only need tooview information about hello security health of a resource but not take action, such as applying recommendations or editing policies.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="65412-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="65412-147">Next steps</span></span>
<span data-ttu-id="65412-148">이 문서는 보안 센터 tooassign 권한 toousers RBAC를 사용 하는 방법을 설명 하 고 hello 허용 되는 각 역할에 대 한 작업을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="65412-148">This article explained how Security Center uses RBAC tooassign permissions toousers and identified hello allowed actions for each role.</span></span> <span data-ttu-id="65412-149">익숙한 hello 역할 할당이 필요 toomonitor hello 구독의 보안 상태, 했으므로 보안 정책을 편집 하며 권장 구성 적용, 자세한 내용은 방법:</span><span class="sxs-lookup"><span data-stu-id="65412-149">Now that you're familiar with hello role assignments needed toomonitor hello security state of your subscription, edit security policies, and apply recommendations, learn how to:</span></span>

- [<span data-ttu-id="65412-150">Security Center에서 보안 정책 설정</span><span class="sxs-lookup"><span data-stu-id="65412-150">Set security policies in Security Center</span></span>](security-center-policies.md)
- [<span data-ttu-id="65412-151">Security Center의 보안 권장 사항 관리</span><span class="sxs-lookup"><span data-stu-id="65412-151">Manage security recommendations in Security Center</span></span>](security-center-recommendations.md)
- [<span data-ttu-id="65412-152">Azure 리소스의 hello 보안 상태를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="65412-152">Monitor hello security health of your Azure resources</span></span>](security-center-monitoring.md)
- [<span data-ttu-id="65412-153">관리 및 보안 센터에서 toosecurity 경고에 응답</span><span class="sxs-lookup"><span data-stu-id="65412-153">Manage and respond toosecurity alerts in Security Center</span></span>](security-center-managing-and-responding-alerts.md)
- [<span data-ttu-id="65412-154">파트너 보안 솔루션 모니터링</span><span class="sxs-lookup"><span data-stu-id="65412-154">Monitor partner security solutions</span></span>](security-center-partner-solutions.md)
