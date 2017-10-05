---
title: "Azure Active Directory B2B 공동 작업의 제한 사항 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업의 현재 제한 사항"
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
ms.openlocfilehash: 581e5d1fb5fb08d0dc89ed2c85edcb5f0005650b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a><span data-ttu-id="fdbe2-103">Azure AD B2B 공동 작업의 제한 사항</span><span class="sxs-lookup"><span data-stu-id="fdbe2-103">Limitations of Azure AD B2B collaboration</span></span>
<span data-ttu-id="fdbe2-104">Azure AD(Azure Active Directory) B2B 공동 작업에는 이 문서에 설명된 제한 사항이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fdbe2-104">Azure Active Directory (Azure AD) B2B collaboration is currently subject to the limitations described in this article.</span></span>

## <a name="possible-double-multi-factor-authentication"></a><span data-ttu-id="fdbe2-105">가능한 이중 다단계 인증</span><span class="sxs-lookup"><span data-stu-id="fdbe2-105">Possible double multi-factor authentication</span></span>
<span data-ttu-id="fdbe2-106">Azure AD B2B를 통해 리소스 조직(초대하는 조직)에서 다단계 인증을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdbe2-106">With Azure AD B2B, you can enforce multi-factor authentication at the resource organization (the inviting organization).</span></span> <span data-ttu-id="fdbe2-107">이 방법을 사용하는 이유는 [B2B 공동 작업 사용자에 대한 조건부 액세스](active-directory-b2b-mfa-instructions.md)에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fdbe2-107">The reasons for this approach are detailed in [Conditional access for B2B collaboration users](active-directory-b2b-mfa-instructions.md).</span></span> <span data-ttu-id="fdbe2-108">파트너가 이미 Multi-Factor Authentication을 설정하여 적용 중인 경우 해당 사용자는 소속된 조직에서 인증을 한 번 수행한 후 여러분의 조직에서 다시 한 번 인증을 수행해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdbe2-108">If a partner already has multi-factor authentication set up and enforced, their users might have to perform the authentication once in their home organization and then again in yours.</span></span>

## <a name="instant-on"></a><span data-ttu-id="fdbe2-109">인스턴트 온</span><span class="sxs-lookup"><span data-stu-id="fdbe2-109">Instant-on</span></span>
<span data-ttu-id="fdbe2-110">B2B 공동 작업 흐름에서 해당 디렉터리에 사용자를 추가하고 초대 상환, 앱 할당 등에서 사용자를 동적으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="fdbe2-110">In the B2B collaboration flows, we add users to the directory and dynamically update them during invitation redemption, app assignment, and so on.</span></span> <span data-ttu-id="fdbe2-111">업데이트 및 쓰기는 일반적으로 한 디렉터리 인스턴스에서 발생하며 모든 인스턴스에 걸쳐 복제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdbe2-111">The updates and writes ordinarily happen in one directory instance and must be replicated across all instances.</span></span> <span data-ttu-id="fdbe2-112">모든 인스턴스가 업데이트되면 복제가 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="fdbe2-112">Replication is completed once all instances are updated.</span></span> <span data-ttu-id="fdbe2-113">개체가 한 인스턴스에서 기록 또는 업데이트되고 이 개체를 검색하기 위한 호출이 다른 인스턴스에 대해 수행될 경우 복제 대기 시간이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdbe2-113">Sometimes when the object is written or updated in one instance and the call to retrieve this object is to another instance, replication latencies can occur.</span></span> <span data-ttu-id="fdbe2-114">이 문제가 발생할 경우 새로 고치거나 다시 시도하면 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fdbe2-114">If that happens, refresh or retry to help.</span></span> <span data-ttu-id="fdbe2-115">API를 사용하여 앱을 작성할 경우 백오프를 사용하여 다시 시도하는 것은 이 문제를 완화하기 위한 좋은 방어 사례입니다.</span><span class="sxs-lookup"><span data-stu-id="fdbe2-115">If you are writing an app using our API, then retries with some back-off is a good, defensive practice to alleviate this issue.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fdbe2-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fdbe2-116">Next steps</span></span>

<span data-ttu-id="fdbe2-117">Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:</span><span class="sxs-lookup"><span data-stu-id="fdbe2-117">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="fdbe2-118">Azure AD B2B 공동 작업이란?</span><span class="sxs-lookup"><span data-stu-id="fdbe2-118">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="fdbe2-119">B2B 공동 작업 사용자 속성</span><span class="sxs-lookup"><span data-stu-id="fdbe2-119">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="fdbe2-120">역할에 B2B 공동 작업 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="fdbe2-120">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="fdbe2-121">B2B 공동 작업 초대 위임</span><span class="sxs-lookup"><span data-stu-id="fdbe2-121">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="fdbe2-122">동적 그룹 및 B2B 공동 작업</span><span class="sxs-lookup"><span data-stu-id="fdbe2-122">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="fdbe2-123">B2B 공동 작업 코드 및 PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="fdbe2-123">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="fdbe2-124">B2B 공동 작업을 위한 SaaS 앱 구성</span><span class="sxs-lookup"><span data-stu-id="fdbe2-124">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="fdbe2-125">B2B 공동 작업 사용자 토큰</span><span class="sxs-lookup"><span data-stu-id="fdbe2-125">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="fdbe2-126">B2B 공동 작업 사용자 클레임 매핑</span><span class="sxs-lookup"><span data-stu-id="fdbe2-126">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="fdbe2-127">Office 365 외부 공유</span><span class="sxs-lookup"><span data-stu-id="fdbe2-127">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
