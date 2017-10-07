---
title: "aaaAdd Azure Active Directory B2B 공동 작업 사용자 tooa 역할 | Microsoft Docs"
description: "Azure Active Directory에서 게스트 사용자 tooa 역할 추가"
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
ms.date: 03/15/2017
ms.author: sasubram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ccc58a0c8ecc73f8e79a8d827efdc0ff93846a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="grant-permissions-toousers-from-partner-organizations-in-your-azure-active-directory-tenant"></a><span data-ttu-id="4d998-103">Azure Active Directory 테 넌 트의 파트너 조직에서 toousers 사용 권한 부여</span><span class="sxs-lookup"><span data-stu-id="4d998-103">Grant permissions toousers from partner organizations in your Azure Active Directory tenant</span></span>

<span data-ttu-id="4d998-104">Azure Active Directory (Azure AD) B2B 공동 작업 사용자는 추가 게스트 사용자 toohello 디렉터리로 및 게스트 사용 권한 hello 디렉터리에 기본적으로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d998-104">Azure Active Directory (Azure AD) B2B collaboration users are added as guest users toohello directory, and guest permissions in hello directory are restricted by default.</span></span> <span data-ttu-id="4d998-105">비즈니스 조직에서 일부 게스트 사용자 toofill 높은 권한이 역할을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d998-105">Your business may need some guest users toofill higher-privilege roles in your organization.</span></span> <span data-ttu-id="4d998-106">높은 권한이 역할 정의 toosupport 게스트 사용자 조직의 요구에 따라 원하는 추가 된 tooany 역할이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d998-106">toosupport defining higher-privilege roles, guest users can be added tooany roles you desire, based on your organization's needs.</span></span>

## <a name="default-role"></a><span data-ttu-id="4d998-107">기본 역할</span><span class="sxs-lookup"><span data-stu-id="4d998-107">Default role</span></span>

![기본 역할](./media/active-directory-b2b-add-guest-to-role/default-role.png)

## <a name="global-administrator-role"></a><span data-ttu-id="4d998-109">전역 관리자 역할</span><span class="sxs-lookup"><span data-stu-id="4d998-109">Global Administrator Role</span></span>

![전역 관리자 역할](./media/active-directory-b2b-add-guest-to-role/global-admin-role.png)

## <a name="limited-administrator-role"></a><span data-ttu-id="4d998-111">제한된 관리자 역할</span><span class="sxs-lookup"><span data-stu-id="4d998-111">Limited Administrator Role</span></span>

![제한된 관리자 역할](./media/active-directory-b2b-add-guest-to-role/limited-admin-role.png)

## <a name="next-steps"></a><span data-ttu-id="4d998-113">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4d998-113">Next steps</span></span>

<span data-ttu-id="4d998-114">Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:</span><span class="sxs-lookup"><span data-stu-id="4d998-114">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="4d998-115">Azure AD B2B 공동 작업이란?</span><span class="sxs-lookup"><span data-stu-id="4d998-115">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="4d998-116">B2B 공동 작업 사용자 속성</span><span class="sxs-lookup"><span data-stu-id="4d998-116">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="4d998-117">B2bB 공동 작업 초대 위임</span><span class="sxs-lookup"><span data-stu-id="4d998-117">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="4d998-118">동적 그룹 및 B2B 공동 작업</span><span class="sxs-lookup"><span data-stu-id="4d998-118">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="4d998-119">B2B 공동 작업 코드 및 PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="4d998-119">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="4d998-120">B2B 공동 작업을 위한 SaaS 앱 구성</span><span class="sxs-lookup"><span data-stu-id="4d998-120">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="4d998-121">B2B 공동 작업 사용자 토큰</span><span class="sxs-lookup"><span data-stu-id="4d998-121">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="4d998-122">B2B 공동 작업 사용자 클레임 매핑</span><span class="sxs-lookup"><span data-stu-id="4d998-122">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="4d998-123">Office 365 외부 공유</span><span class="sxs-lookup"><span data-stu-id="4d998-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="4d998-124">B2B 공동 작업 현재 제한</span><span class="sxs-lookup"><span data-stu-id="4d998-124">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
