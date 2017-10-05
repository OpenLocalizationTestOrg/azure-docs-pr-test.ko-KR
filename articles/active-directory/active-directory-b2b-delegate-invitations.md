---
title: "Azure Active Directory B2B 공동 작업에 대한 초대 위임 | Microsoft Docs"
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
ms.openlocfilehash: 78613cc978b585a98d235245194c02371f7f3849
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="d60d9-103">Azure Active Directory B2B 공동 작업에 대한 초대 위임</span><span class="sxs-lookup"><span data-stu-id="d60d9-103">Delegate invitations for Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="d60d9-104">Azure AD(Azure Active Directory) B2B 공동 작업을 사용하면 전역 관리자가 아니더라도 초대할 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d60d9-104">With Azure Active Directory (Azure AD) business-to-business (B2B) collaboration, you do not have to be a global admin to send invitations.</span></span> <span data-ttu-id="d60d9-105">그 대신 정책을 사용하여 초대를 보낼 수 있는 역할을 가진 사용자에게 초대를 위임할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d60d9-105">Instead, you can use policies and delegate invitations to users whose roles allow them to send invitations.</span></span> <span data-ttu-id="d60d9-106">게스트 사용자 초대를 위임하는 중요한 새 방식은 게스트 초대자 역할을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d60d9-106">An important new way to delegate guest user invitations is through the Guest Inviter role.</span></span>

## <a name="guest-inviter-role"></a><span data-ttu-id="d60d9-107">게스트 초대자 역할</span><span class="sxs-lookup"><span data-stu-id="d60d9-107">Guest Inviter role</span></span>
<span data-ttu-id="d60d9-108">사용자에게 초대를 전송할 수 있는 게스트 초대자 역할에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d60d9-108">We can assign the user to Guest Inviter role to send invitations.</span></span> <span data-ttu-id="d60d9-109">전역 관리자 역할의 구성원이 아니더라도 초대를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d60d9-109">You don't have to be member of the global admin role to send invitations.</span></span> <span data-ttu-id="d60d9-110">기본적으로 전역 관리자가 일반 사용자에게 초대를 사용하지 않도록 설정한 경우가 아니면 일반 사용자도 초대 API를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d60d9-110">By default, regular users can also invoke the invite API unless a global admin disabled invitations for regular users.</span></span> <span data-ttu-id="d60d9-111">Azure Portal 또는 PowerShell을 사용하여 API를 호출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d60d9-111">A user can also invoke the API using the Azure portal or PowerShell.</span></span>

<span data-ttu-id="d60d9-112">다음은 PowerShell을 사용하여 게스트 초대자 역할에 사용자를 추가하는 방법을 보여주는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="d60d9-112">Here's an example that shows how to use PowerShell to add a user to the Guest Inviter role:</span></span>

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a><span data-ttu-id="d60d9-113">초대할 수 있는 사용자 제어</span><span class="sxs-lookup"><span data-stu-id="d60d9-113">Control who can invite</span></span>

![초대 방법 제어](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

<span data-ttu-id="d60d9-115">Azure AD B2B 공동 작업을 사용하면 테넌트 관리자가 다음 초대 정책을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d60d9-115">With Azure AD B2B collaboration, a tenant admin can set the following invitation policies:</span></span>

- <span data-ttu-id="d60d9-116">초대 해제</span><span class="sxs-lookup"><span data-stu-id="d60d9-116">Turn off invitations</span></span>
- <span data-ttu-id="d60d9-117">관리자 및 게스트 초대자 역할의 사용자만 초대 가능</span><span class="sxs-lookup"><span data-stu-id="d60d9-117">Only admins and users in the Guest Inviter role can invite</span></span>
- <span data-ttu-id="d60d9-118">관리자, 게스트 초대자 역할 및 구성원은 초대 가능</span><span class="sxs-lookup"><span data-stu-id="d60d9-118">Admins, the Guest Inviter role, and members can invite</span></span>
- <span data-ttu-id="d60d9-119">게스트를 포함한 모든 사용자가 초대를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d60d9-119">All users, including guests, can invite</span></span>

<span data-ttu-id="d60d9-120">기본적으로 테넌트는 #4로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d60d9-120">By default, tenants are set to #4.</span></span> <span data-ttu-id="d60d9-121">(게스트를 포함한 모든 사용자가 B2B 사용자를 초대할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="d60d9-121">(All users, including guests, can invite B2B users.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d60d9-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d60d9-122">Next steps</span></span>

<span data-ttu-id="d60d9-123">Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:</span><span class="sxs-lookup"><span data-stu-id="d60d9-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="d60d9-124">Azure AD B2B 공동 작업이란?</span><span class="sxs-lookup"><span data-stu-id="d60d9-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="d60d9-125">B2B 공동 작업 사용자 속성</span><span class="sxs-lookup"><span data-stu-id="d60d9-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="d60d9-126">역할에 B2B 공동 작업 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="d60d9-126">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="d60d9-127">동적 그룹 및 B2B 공동 작업</span><span class="sxs-lookup"><span data-stu-id="d60d9-127">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="d60d9-128">B2B 공동 작업 코드 및 PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="d60d9-128">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="d60d9-129">B2B 공동 작업을 위한 SaaS 앱 구성</span><span class="sxs-lookup"><span data-stu-id="d60d9-129">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="d60d9-130">B2B 공동 작업 사용자 토큰</span><span class="sxs-lookup"><span data-stu-id="d60d9-130">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="d60d9-131">B2B 공동 작업 사용자 클레임 매핑</span><span class="sxs-lookup"><span data-stu-id="d60d9-131">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="d60d9-132">Office 365 외부 공유</span><span class="sxs-lookup"><span data-stu-id="d60d9-132">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="d60d9-133">B2B 공동 작업 현재 제한</span><span class="sxs-lookup"><span data-stu-id="d60d9-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
