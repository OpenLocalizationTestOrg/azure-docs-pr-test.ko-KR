---
title: "Azure Active Directory B2B 공동 작업의 aaaLimitations | Microsoft Docs"
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
ms.openlocfilehash: 322081f32fbacfe67ee1300993c7df1870e498bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a><span data-ttu-id="40f33-103">Azure AD B2B 공동 작업의 제한 사항</span><span class="sxs-lookup"><span data-stu-id="40f33-103">Limitations of Azure AD B2B collaboration</span></span>
<span data-ttu-id="40f33-104">Azure Active Directory (Azure AD) B2B 공동 작업은 현재이 문서에서 설명 하는 주체 toohello 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40f33-104">Azure Active Directory (Azure AD) B2B collaboration is currently subject toohello limitations described in this article.</span></span>

## <a name="possible-double-multi-factor-authentication"></a><span data-ttu-id="40f33-105">가능한 이중 다단계 인증</span><span class="sxs-lookup"><span data-stu-id="40f33-105">Possible double multi-factor authentication</span></span>
<span data-ttu-id="40f33-106">Azure AD B2B hello 리소스 조직 (hello 초대 조직)에 multi-factor authentication을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f33-106">With Azure AD B2B, you can enforce multi-factor authentication at hello resource organization (hello inviting organization).</span></span> <span data-ttu-id="40f33-107">이 방법에 대 한 hello 이유에 자세히 설명 되어 [B2B 공동 작업 사용자에 대 한 조건부 액세스](active-directory-b2b-mfa-instructions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="40f33-107">hello reasons for this approach are detailed in [Conditional access for B2B collaboration users](active-directory-b2b-mfa-instructions.md).</span></span> <span data-ttu-id="40f33-108">파트너에 이미 multi-factor authentication을 설정 하 고 적용 하는 경우 사용자에 게 않았기 때문일 수 있습니다 tooperform hello 인증 한 번 홈 조직 및 사용자에 게 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="40f33-108">If a partner already has multi-factor authentication set up and enforced, their users might have tooperform hello authentication once in their home organization and then again in yours.</span></span>

## <a name="instant-on"></a><span data-ttu-id="40f33-109">인스턴트 온</span><span class="sxs-lookup"><span data-stu-id="40f33-109">Instant-on</span></span>
<span data-ttu-id="40f33-110">Hello B2B 공동 작업 흐름에서는 사용자가 toohello 디렉터리를 추가 하 고 초대 상환, 앱 할당 및 등 하는 동안이 동적으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="40f33-110">In hello B2B collaboration flows, we add users toohello directory and dynamically update them during invitation redemption, app assignment, and so on.</span></span> <span data-ttu-id="40f33-111">일반적으로 hello 업데이트 및 쓰기 디렉터리 인스턴스에서 발생 시간과 모든 인 스턴에서 복제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40f33-111">hello updates and writes ordinarily happen in one directory instance and must be replicated across all instances.</span></span> <span data-ttu-id="40f33-112">모든 인스턴스가 업데이트되면 복제가 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="40f33-112">Replication is completed once all instances are updated.</span></span> <span data-ttu-id="40f33-113">경우에 따라 hello 개체가 작성 되거나 업데이트 한 인스턴스에서 시점과 hello 호출 tooretrieve이이 개체 인스턴스가 tooanother, 복제 대기 시간이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f33-113">Sometimes when hello object is written or updated in one instance and hello call tooretrieve this object is tooanother instance, replication latencies can occur.</span></span> <span data-ttu-id="40f33-114">이렇게 되 면 새로 고치거 나 toohelp을 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="40f33-114">If that happens, refresh or retry toohelp.</span></span> <span data-ttu-id="40f33-115">이 API를 다음 다시 시도 횟수를 사용 하 여 일부와 응용 프로그램을 작성 하는 경우 백오프 좋은 방어적 연습 tooalleviate이이 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="40f33-115">If you are writing an app using our API, then retries with some back-off is a good, defensive practice tooalleviate this issue.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40f33-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="40f33-116">Next steps</span></span>

<span data-ttu-id="40f33-117">Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:</span><span class="sxs-lookup"><span data-stu-id="40f33-117">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="40f33-118">Azure AD B2B 공동 작업이란?</span><span class="sxs-lookup"><span data-stu-id="40f33-118">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="40f33-119">B2B 공동 작업 사용자 속성</span><span class="sxs-lookup"><span data-stu-id="40f33-119">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="40f33-120">B2B 공동 작업 사용자 tooa 역할 추가</span><span class="sxs-lookup"><span data-stu-id="40f33-120">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="40f33-121">B2B 공동 작업 초대 위임</span><span class="sxs-lookup"><span data-stu-id="40f33-121">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="40f33-122">동적 그룹 및 B2B 공동 작업</span><span class="sxs-lookup"><span data-stu-id="40f33-122">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="40f33-123">B2B 공동 작업 코드 및 PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="40f33-123">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="40f33-124">B2B 공동 작업을 위한 SaaS 앱 구성</span><span class="sxs-lookup"><span data-stu-id="40f33-124">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="40f33-125">B2B 공동 작업 사용자 토큰</span><span class="sxs-lookup"><span data-stu-id="40f33-125">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="40f33-126">B2B 공동 작업 사용자 클레임 매핑</span><span class="sxs-lookup"><span data-stu-id="40f33-126">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="40f33-127">Office 365 외부 공유</span><span class="sxs-lookup"><span data-stu-id="40f33-127">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
