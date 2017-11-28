---
title: "Azure Active Directory B2B 공동 작업에 대 한 aaaDelegate 초대장 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업 사용자 속성은 구성 가능합니다."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: c0122d6f60d494c6e251c41d947dc254ea887620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="1586d-103">Azure Active Directory B2B 공동 작업에 대한 초대 위임</span><span class="sxs-lookup"><span data-stu-id="1586d-103">Delegate invitations for Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="1586d-104">Azure Active Directory (Azure AD) 기업 B2B 공동 작업와 없는 toobe 전역 관리자 toosend 초대 합니다.</span><span class="sxs-lookup"><span data-stu-id="1586d-104">With Azure Active Directory (Azure AD) business-to-business (B2B) collaboration, you do not have toobe a global admin toosend invitations.</span></span> <span data-ttu-id="1586d-105">대신, 정책을 사용 하 고 초대 toousers toosend 초대 허용 해당 역할을 위임할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1586d-105">Instead, you can use policies and delegate invitations toousers whose roles allow them toosend invitations.</span></span> <span data-ttu-id="1586d-106">중요 한 새로운 방식으로 toodelegate 게스트 사용자 초대 hello 게스트 초대자 역할을 통해 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="1586d-106">An important new way toodelegate guest user invitations is through hello Guest Inviter role.</span></span>

## <a name="guest-inviter-role"></a><span data-ttu-id="1586d-107">게스트 초대자 역할</span><span class="sxs-lookup"><span data-stu-id="1586d-107">Guest Inviter role</span></span>
<span data-ttu-id="1586d-108">Hello 사용자 tooGuest 초대자 역할 toosend 초대 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1586d-108">We can assign hello user tooGuest Inviter role toosend invitations.</span></span> <span data-ttu-id="1586d-109">Hello 전역 관리자 역할 toosend 초대 toobe 소속이 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1586d-109">You don't have toobe member of hello global admin role toosend invitations.</span></span> <span data-ttu-id="1586d-110">기본적으로 일반 사용자 전역 관리자에 대 한 일반 사용자가 초대장을 해제 하지 않는 한 hello 초대 API를 호출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1586d-110">By default, regular users can also invoke hello invite API unless a global admin disabled invitations for regular users.</span></span> <span data-ttu-id="1586d-111">사용자는 hello Azure 포털 또는 PowerShell을 사용 하 여 hello API를 호출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1586d-111">A user can also invoke hello API using hello Azure portal or PowerShell.</span></span>

<span data-ttu-id="1586d-112">다음은 예제를 보여 주는 방법을 toouse PowerShell tooadd 사용자 toohello 게스트 초대자 역할:</span><span class="sxs-lookup"><span data-stu-id="1586d-112">Here's an example that shows how toouse PowerShell tooadd a user toohello Guest Inviter role:</span></span>

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a><span data-ttu-id="1586d-113">초대할 수 있는 사용자 제어</span><span class="sxs-lookup"><span data-stu-id="1586d-113">Control who can invite</span></span>

![제어 방법을 tooinvite](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

<span data-ttu-id="1586d-115">Azure AD B2B 공동 작업와 테 넌 트 관리자는 다음 초대 정책 hello를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1586d-115">With Azure AD B2B collaboration, a tenant admin can set hello following invitation policies:</span></span>

- <span data-ttu-id="1586d-116">초대 해제</span><span class="sxs-lookup"><span data-stu-id="1586d-116">Turn off invitations</span></span>
- <span data-ttu-id="1586d-117">관리자 및 hello 게스트 초대자 역할의 사용자를 초대할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1586d-117">Only admins and users in hello Guest Inviter role can invite</span></span>
- <span data-ttu-id="1586d-118">Admins, hello 게스트 초대자 역할 및 멤버 초대할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1586d-118">Admins, hello Guest Inviter role, and members can invite</span></span>
- <span data-ttu-id="1586d-119">게스트를 포함한 모든 사용자가 초대를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1586d-119">All users, including guests, can invite</span></span>

<span data-ttu-id="1586d-120">기본적으로 테 넌 트 설정 된 너무 #4입니다.</span><span class="sxs-lookup"><span data-stu-id="1586d-120">By default, tenants are set too#4.</span></span> <span data-ttu-id="1586d-121">(게스트를 포함한 모든 사용자가 B2B 사용자를 초대할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="1586d-121">(All users, including guests, can invite B2B users.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="1586d-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1586d-122">Next steps</span></span>

<span data-ttu-id="1586d-123">Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:</span><span class="sxs-lookup"><span data-stu-id="1586d-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="1586d-124">Azure AD B2B 공동 작업이란?</span><span class="sxs-lookup"><span data-stu-id="1586d-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="1586d-125">B2B 공동 작업 사용자 속성</span><span class="sxs-lookup"><span data-stu-id="1586d-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="1586d-126">B2B 공동 작업 사용자 tooa 역할 추가</span><span class="sxs-lookup"><span data-stu-id="1586d-126">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="1586d-127">동적 그룹 및 B2B 공동 작업</span><span class="sxs-lookup"><span data-stu-id="1586d-127">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="1586d-128">B2B 공동 작업 코드 및 PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="1586d-128">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="1586d-129">B2B 공동 작업을 위한 SaaS 앱 구성</span><span class="sxs-lookup"><span data-stu-id="1586d-129">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="1586d-130">B2B 공동 작업 사용자 토큰</span><span class="sxs-lookup"><span data-stu-id="1586d-130">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="1586d-131">B2B 공동 작업 사용자 클레임 매핑</span><span class="sxs-lookup"><span data-stu-id="1586d-131">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="1586d-132">Office 365 외부 공유</span><span class="sxs-lookup"><span data-stu-id="1586d-132">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="1586d-133">B2B 공동 작업 현재 제한</span><span class="sxs-lookup"><span data-stu-id="1586d-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
