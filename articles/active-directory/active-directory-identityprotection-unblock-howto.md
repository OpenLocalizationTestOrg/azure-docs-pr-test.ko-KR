---
title: "Azure Active Directory ID 보호 - 사용자를 차단 해제하는 방법 | Microsoft Docs"
description: "Azure Active Directory ID 보호 정책에 의해 차단된 사용자를 차단 해제하는 방법을 알아봅니다."
services: active-directory
keywords: "Azure Active Directory ID 보호, 사용자 차단 해제"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: a953d425-a3ef-41f8-a55d-0202c3f250a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ce6b2805e7281dff7752a73ada86be11d7e01fc3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection---how-to-unblock-users"></a><span data-ttu-id="12661-104">Azure Active Directory ID 보호 - 사용자를 차단 해제하는 방법</span><span class="sxs-lookup"><span data-stu-id="12661-104">Azure Active Directory Identity Protection - How to unblock users</span></span>
<span data-ttu-id="12661-105">Azure Active Directory ID 보호를 사용하여 구성된 조건을 만족하는 경우에 사용자를 차단하는 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12661-105">With Azure Active Directory Identity Protection, you can configure policies to block users if the configured conditions are satisfied.</span></span> <span data-ttu-id="12661-106">일반적으로 차단된 사용자 연락처는 데스크가 차단 해제되도록 돕습니다.</span><span class="sxs-lookup"><span data-stu-id="12661-106">Typically, a blocked user contacts help desk to become unblocked.</span></span> <span data-ttu-id="12661-107">이 항목은 차단된 사용자를 해제하기 위해 수행할 수 있는 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="12661-107">This topics explains the steps you can perform to unblock a blocked user.</span></span>

## <a name="determine-the-reason-for-blocking"></a><span data-ttu-id="12661-108">차단 이유를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="12661-108">Determine the reason for blocking</span></span>
<span data-ttu-id="12661-109">사용자를 차단 해제하는 첫 번째 단계로 다음 단계가 좌우되는 사용자를 차단한 정책의 유형을 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12661-109">As a first step to unblock a user, you need to determine the type of policy that has blocked the user because your next steps are depending on it.</span></span>
<span data-ttu-id="12661-110">Azure Active Directory ID보호를 사용하여 로그인 위험 정책 또는 사용자 위험 정책으로 사용자를 차단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12661-110">With Azure Active Directory Identity Protection, a user can be either blocked by a sign-in risk policy or a user risk policy.</span></span>

<span data-ttu-id="12661-111">로그인을 시도하는 동안 사용자에게 표시된 대화 상자의 제목에서 사용자를 차단한 정책 유형을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12661-111">You can get the type of policy that has blocked a user from the heading in the dialog that was presented to the user during a sign-in attempt:</span></span>

| <span data-ttu-id="12661-112">정책</span><span class="sxs-lookup"><span data-stu-id="12661-112">Policy</span></span> | <span data-ttu-id="12661-113">사용자 대화 상자</span><span class="sxs-lookup"><span data-stu-id="12661-113">User dialog</span></span> |
| --- | --- |
| <span data-ttu-id="12661-114">로그인 위험</span><span class="sxs-lookup"><span data-stu-id="12661-114">Sign-in risk</span></span> |![차단된 로그인](./media/active-directory-identityprotection-unblock-howto/02.png) |
| <span data-ttu-id="12661-116">사용자 위험</span><span class="sxs-lookup"><span data-stu-id="12661-116">User risk</span></span> |![차단된 계정](./media/active-directory-identityprotection-unblock-howto/104.png) |

<span data-ttu-id="12661-118">다음에 의해 차단된 사용자:</span><span class="sxs-lookup"><span data-stu-id="12661-118">A user that is blocked by:</span></span>

* <span data-ttu-id="12661-119">로그인 위험 정책은 의심스러운 로그인이라고도 함</span><span class="sxs-lookup"><span data-stu-id="12661-119">A sign-in risk policy is also known as suspicious sign-in</span></span>
* <span data-ttu-id="12661-120">사용자 위험 정책은 위험한 계정이라고도 함</span><span class="sxs-lookup"><span data-stu-id="12661-120">A user risk policy is also known as an account at risk</span></span>

## <a name="unblocking-suspicious-sign-ins"></a><span data-ttu-id="12661-121">의심스러운 로그인 차단 해제</span><span class="sxs-lookup"><span data-stu-id="12661-121">Unblocking suspicious sign-ins</span></span>
<span data-ttu-id="12661-122">의심스러운 로그인을 차단 해제하기 위해 다음 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12661-122">To unblock a suspicious sign-in, you have the following options:</span></span>

1. <span data-ttu-id="12661-123">**친숙한 위치 또는 장치에서 로그인** - 차단된 의심스러운 로그인에 대한 일반적인 이유는 알 수 없는 위치 또는 장치에서의 로그인 시도입니다.</span><span class="sxs-lookup"><span data-stu-id="12661-123">**Sign-in from a familiar location or device** - A common reason for blocked suspicious sign-ins are sign-in attempts from unfamiliar locations or devices.</span></span> <span data-ttu-id="12661-124">사용자는 친숙한 위치 또는 장치에서 로그인을 시도하여 차단 이유인지 여부를 빠르게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12661-124">Your users can quickly determine whether this is the blocking reason by trying to sign-in from a familiar location or device.</span></span>
2. <span data-ttu-id="12661-125">**정책에서 제외** - 로그인 정책의 현재 구성이 특정 사용자에 대해 문제를 일으킨다고 생각하는 경우 여기에서 사용자를 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12661-125">**Exclude from policy** - If you think that the current configuration of your sign-in policy is causing issues for specific users, you can exclude the users from it.</span></span> <span data-ttu-id="12661-126">자세한 내용은 [Azure Active Directory ID 보호](active-directory-identityprotection.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12661-126">See [Azure Active Directory Identity Protection](active-directory-identityprotection.md) for more details.</span></span>
3. <span data-ttu-id="12661-127">**정책 비활성화** - 정책 구성이 모든 사용자에 대해 문제를 일으킨다고 생각하는 경우 정책을 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12661-127">**Disable policy** - If you think that your policy configuration is causing issues for all your users, you can disable the policy.</span></span> <span data-ttu-id="12661-128">자세한 내용은 [Azure Active Directory ID 보호](active-directory-identityprotection.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12661-128">See [Azure Active Directory Identity Protection](active-directory-identityprotection.md) for more details.</span></span>

## <a name="unblocking-accounts-at-risk"></a><span data-ttu-id="12661-129">위험한 계정 차단 해제</span><span class="sxs-lookup"><span data-stu-id="12661-129">Unblocking accounts at risk</span></span>
<span data-ttu-id="12661-130">위험한 계정을 차단 해제하기 위해 다음 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12661-130">To unblock an account at risk, you have the following options:</span></span>

1. <span data-ttu-id="12661-131">**암호 재설정** - 사용자의 암호를 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12661-131">**Reset password** - You can reset the user's password.</span></span> <span data-ttu-id="12661-132">자세한 내용은 [수동으로 안전한 암호 다시 설정](active-directory-identityprotection.md#manual-secure-password-reset) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12661-132">See [manual secure password reset](active-directory-identityprotection.md#manual-secure-password-reset) for more details.</span></span>
2. <span data-ttu-id="12661-133">**모든 위험 이벤트 해제** - 액세스 차단에 대해 구성된 사용자 위험 수준에 도달한 경우 사용자 위험 정책은 사용자를 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="12661-133">**Dismiss all risk events** - The user risk policy blocks a user if the configured user risk level for blocking access has been reached.</span></span> <span data-ttu-id="12661-134">수동으로 보고된 위험 이벤트를 닫아서 사용자의 위험 수준을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12661-134">You can reduce a user's risk level by manually closing reported risk events.</span></span> <span data-ttu-id="12661-135">자세한 내용은 [수동으로 위험 이벤트 닫기](active-directory-identityprotection.md#closing-risk-events-manually)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12661-135">For more details, see [closing risk events manually](active-directory-identityprotection.md#closing-risk-events-manually).</span></span>
3. <span data-ttu-id="12661-136">**정책에서 제외** - 로그인 정책의 현재 구성이 특정 사용자에 대해 문제를 일으킨다고 생각하는 경우 여기에서 사용자를 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12661-136">**Exclude from policy** - If you think that the current configuration of your sign-in policy is causing issues for specific users, you can exclude the users from it.</span></span> <span data-ttu-id="12661-137">자세한 내용은 [Azure Active Directory ID 보호](active-directory-identityprotection.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12661-137">See [Azure Active Directory Identity Protection](active-directory-identityprotection.md) for more details.</span></span>
4. <span data-ttu-id="12661-138">**정책 비활성화** - 정책 구성이 모든 사용자에 대해 문제를 일으킨다고 생각하는 경우 정책을 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12661-138">**Disable policy** - If you think that your policy configuration is causing issues for all your users, you can disable the policy.</span></span> <span data-ttu-id="12661-139">자세한 내용은 [Azure Active Directory ID 보호](active-directory-identityprotection.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12661-139">See [Azure Active Directory Identity Protection](active-directory-identityprotection.md) for more details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12661-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="12661-140">Next steps</span></span>
 <span data-ttu-id="12661-141">Azure AD ID 보호에 대해 자세히 살펴보시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="12661-141">Do you want to know more about Azure AD Identity Protection?</span></span> <span data-ttu-id="12661-142">[Azure Active Directory ID 보호](active-directory-identityprotection.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="12661-142">Check out [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>
