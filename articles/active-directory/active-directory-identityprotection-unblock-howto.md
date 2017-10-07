---
title: "Active Directory Id 보호-aaaAzure 어떻게 toounblock 사용자 | Microsoft Docs"
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
ms.openlocfilehash: cdda2808822888f76aa75cf46478738c94df51a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection---how-toounblock-users"></a><span data-ttu-id="e8315-104">Azure Active Directory Id 보호-어떻게 toounblock 사용자</span><span class="sxs-lookup"><span data-stu-id="e8315-104">Azure Active Directory Identity Protection - How toounblock users</span></span>
<span data-ttu-id="e8315-105">Azure Active Directory Id 보호 tooblock 사용자 hello 구성 조건을 충족 하는 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8315-105">With Azure Active Directory Identity Protection, you can configure policies tooblock users if hello configured conditions are satisfied.</span></span> <span data-ttu-id="e8315-106">일반적으로 차단 된 사용자 연락처 도움말 센터 toobecome 차단 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8315-106">Typically, a blocked user contacts help desk toobecome unblocked.</span></span> <span data-ttu-id="e8315-107">이 항목 toounblock 차단 된 사용자를 수행할 수 있는 hello 단계를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8315-107">This topics explains hello steps you can perform toounblock a blocked user.</span></span>

## <a name="determine-hello-reason-for-blocking"></a><span data-ttu-id="e8315-108">차단에 대 한 hello 이유를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8315-108">Determine hello reason for blocking</span></span>
<span data-ttu-id="e8315-109">첫 번째 단계 toounblock 사용자,으로 다음 단계에 좌우 되 때문에 hello 사용자 차단 정책 toodetermine hello 형식이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8315-109">As a first step toounblock a user, you need toodetermine hello type of policy that has blocked hello user because your next steps are depending on it.</span></span>
<span data-ttu-id="e8315-110">Azure Active Directory ID보호를 사용하여 로그인 위험 정책 또는 사용자 위험 정책으로 사용자를 차단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8315-110">With Azure Active Directory Identity Protection, a user can be either blocked by a sign-in risk policy or a user risk policy.</span></span>

<span data-ttu-id="e8315-111">Hello 유형의 hello 머리글 toohello 사용자는 로그인 시도 중에 발표 hello 대화 상자에서에서 사용자를 차단 정책 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8315-111">You can get hello type of policy that has blocked a user from hello heading in hello dialog that was presented toohello user during a sign-in attempt:</span></span>

| <span data-ttu-id="e8315-112">정책</span><span class="sxs-lookup"><span data-stu-id="e8315-112">Policy</span></span> | <span data-ttu-id="e8315-113">사용자 대화 상자</span><span class="sxs-lookup"><span data-stu-id="e8315-113">User dialog</span></span> |
| --- | --- |
| <span data-ttu-id="e8315-114">로그인 위험</span><span class="sxs-lookup"><span data-stu-id="e8315-114">Sign-in risk</span></span> |![차단된 로그인](./media/active-directory-identityprotection-unblock-howto/02.png) |
| <span data-ttu-id="e8315-116">사용자 위험</span><span class="sxs-lookup"><span data-stu-id="e8315-116">User risk</span></span> |![차단된 계정](./media/active-directory-identityprotection-unblock-howto/104.png) |

<span data-ttu-id="e8315-118">다음에 의해 차단된 사용자:</span><span class="sxs-lookup"><span data-stu-id="e8315-118">A user that is blocked by:</span></span>

* <span data-ttu-id="e8315-119">로그인 위험 정책은 의심스러운 로그인이라고도 함</span><span class="sxs-lookup"><span data-stu-id="e8315-119">A sign-in risk policy is also known as suspicious sign-in</span></span>
* <span data-ttu-id="e8315-120">사용자 위험 정책은 위험한 계정이라고도 함</span><span class="sxs-lookup"><span data-stu-id="e8315-120">A user risk policy is also known as an account at risk</span></span>

## <a name="unblocking-suspicious-sign-ins"></a><span data-ttu-id="e8315-121">의심스러운 로그인 차단 해제</span><span class="sxs-lookup"><span data-stu-id="e8315-121">Unblocking suspicious sign-ins</span></span>
<span data-ttu-id="e8315-122">의심 스러운 로그인 toounblock, hello 다음 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8315-122">toounblock a suspicious sign-in, you have hello following options:</span></span>

1. <span data-ttu-id="e8315-123">**친숙한 위치 또는 장치에서 로그인** - 차단된 의심스러운 로그인에 대한 일반적인 이유는 알 수 없는 위치 또는 장치에서의 로그인 시도입니다.</span><span class="sxs-lookup"><span data-stu-id="e8315-123">**Sign-in from a familiar location or device** - A common reason for blocked suspicious sign-ins are sign-in attempts from unfamiliar locations or devices.</span></span> <span data-ttu-id="e8315-124">사용자가 친숙 한 위치 또는 장치에서 toosign에서 시도 하 여 이유를 차단 하는 hello 인지 여부를 빠르게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8315-124">Your users can quickly determine whether this is hello blocking reason by trying toosign-in from a familiar location or device.</span></span>
2. <span data-ttu-id="e8315-125">**정책에서 제외** hello 정책에 로그인의 현재 구성을 특정 사용자에 대 한 문제를 일으키는지, 여기에서 hello 사용자가 제외할 수 있다고 생각 되 면-합니다.</span><span class="sxs-lookup"><span data-stu-id="e8315-125">**Exclude from policy** - If you think that hello current configuration of your sign-in policy is causing issues for specific users, you can exclude hello users from it.</span></span> <span data-ttu-id="e8315-126">자세한 내용은 [Azure Active Directory ID 보호](active-directory-identityprotection.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8315-126">See [Azure Active Directory Identity Protection](active-directory-identityprotection.md) for more details.</span></span>
3. <span data-ttu-id="e8315-127">**정책을 사용 하지 않도록** 정책 구성이 모든 사용자에 대 한 문제를 일으키는지, hello 정책을 해제할 수 있다고 생각 되 면-합니다.</span><span class="sxs-lookup"><span data-stu-id="e8315-127">**Disable policy** - If you think that your policy configuration is causing issues for all your users, you can disable hello policy.</span></span> <span data-ttu-id="e8315-128">자세한 내용은 [Azure Active Directory ID 보호](active-directory-identityprotection.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8315-128">See [Azure Active Directory Identity Protection](active-directory-identityprotection.md) for more details.</span></span>

## <a name="unblocking-accounts-at-risk"></a><span data-ttu-id="e8315-129">위험한 계정 차단 해제</span><span class="sxs-lookup"><span data-stu-id="e8315-129">Unblocking accounts at risk</span></span>
<span data-ttu-id="e8315-130">hello 다음 옵션을 사용할 수 있는 위험에 노출 하는 계정 toounblock, 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8315-130">toounblock an account at risk, you have hello following options:</span></span>

1. <span data-ttu-id="e8315-131">**암호 재설정** -hello 사용자의 암호를 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8315-131">**Reset password** - You can reset hello user's password.</span></span> <span data-ttu-id="e8315-132">자세한 내용은 [수동으로 안전한 암호 다시 설정](active-directory-identityprotection.md#manual-secure-password-reset) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8315-132">See [manual secure password reset](active-directory-identityprotection.md#manual-secure-password-reset) for more details.</span></span>
2. <span data-ttu-id="e8315-133">**위험 이벤트를 모두 해제** -hello 사용자 위험 정책 액세스를 차단 하는 것에 대 한 구성 hello 사용자 위험 수준에 도달 하면 사용자를 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8315-133">**Dismiss all risk events** - hello user risk policy blocks a user if hello configured user risk level for blocking access has been reached.</span></span> <span data-ttu-id="e8315-134">수동으로 보고된 위험 이벤트를 닫아서 사용자의 위험 수준을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8315-134">You can reduce a user's risk level by manually closing reported risk events.</span></span> <span data-ttu-id="e8315-135">자세한 내용은 [수동으로 위험 이벤트 닫기](active-directory-identityprotection.md#closing-risk-events-manually)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8315-135">For more details, see [closing risk events manually](active-directory-identityprotection.md#closing-risk-events-manually).</span></span>
3. <span data-ttu-id="e8315-136">**정책에서 제외** hello 정책에 로그인의 현재 구성을 특정 사용자에 대 한 문제를 일으키는지, 여기에서 hello 사용자가 제외할 수 있다고 생각 되 면-합니다.</span><span class="sxs-lookup"><span data-stu-id="e8315-136">**Exclude from policy** - If you think that hello current configuration of your sign-in policy is causing issues for specific users, you can exclude hello users from it.</span></span> <span data-ttu-id="e8315-137">자세한 내용은 [Azure Active Directory ID 보호](active-directory-identityprotection.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8315-137">See [Azure Active Directory Identity Protection](active-directory-identityprotection.md) for more details.</span></span>
4. <span data-ttu-id="e8315-138">**정책을 사용 하지 않도록** 정책 구성이 모든 사용자에 대 한 문제를 일으키는지, hello 정책을 해제할 수 있다고 생각 되 면-합니다.</span><span class="sxs-lookup"><span data-stu-id="e8315-138">**Disable policy** - If you think that your policy configuration is causing issues for all your users, you can disable hello policy.</span></span> <span data-ttu-id="e8315-139">자세한 내용은 [Azure Active Directory ID 보호](active-directory-identityprotection.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8315-139">See [Azure Active Directory Identity Protection](active-directory-identityprotection.md) for more details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8315-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e8315-140">Next steps</span></span>
 <span data-ttu-id="e8315-141">Azure AD Identity Protection에 대 한 자세한 tooknow 하 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="e8315-141">Do you want tooknow more about Azure AD Identity Protection?</span></span> <span data-ttu-id="e8315-142">[Azure Active Directory ID 보호](active-directory-identityprotection.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="e8315-142">Check out [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>
