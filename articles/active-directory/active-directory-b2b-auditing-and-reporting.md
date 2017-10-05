---
title: "Azure Active Directory B2B 공동 작업 사용자 감사 및 보고 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업에서 구성 가능한 게스트 사용자 속성"
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
ms.date: 04/12/2017
ms.author: sasubram
ms.openlocfilehash: ba782270f3280e52235bc13148d232284b55762a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="auditing-and-reporting-a-b2b-collaboration-user"></a><span data-ttu-id="4bf80-103">B2B 공동 작업 사용자 감사 및 보고</span><span class="sxs-lookup"><span data-stu-id="4bf80-103">Auditing and reporting a B2B collaboration user</span></span>
<span data-ttu-id="4bf80-104">게스트 사용자를 사용하여 구성원 사용자와 유사한 감사 기능을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bf80-104">With guest users, you have auditing capabilities similar to with member users.</span></span> <span data-ttu-id="4bf80-105">다음은 초대한 Sam Oogle의 초대 및 상환 기록에 대한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="4bf80-105">Here's an example of the invitation and redemption history of invitee Sam Oogle:</span></span>

![감사 로그](./media/active-directory-b2b-auditing-and-reporting/audit-log.png)

<span data-ttu-id="4bf80-107">이러한 각 이벤트를 심층 분석하여 자세한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bf80-107">You can dive into each of these events to get the details.</span></span> <span data-ttu-id="4bf80-108">예를 들어 승인 세부 정보를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4bf80-108">For example, let's look at the acceptance details.</span></span>

![활동 세부 정보](./media/active-directory-b2b-auditing-and-reporting/activity-details.png)

<span data-ttu-id="4bf80-110">Azure AD에서 이러한 로그를 내보낸 후 원하는 보고 도구를 사용하여 익숙한 보고서를 얻을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bf80-110">You can also export these logs from Azure AD and use the reporting tool of your choice to get customized reports.</span></span>

### <a name="next-steps"></a><span data-ttu-id="4bf80-111">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4bf80-111">Next steps</span></span>

<span data-ttu-id="4bf80-112">Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:</span><span class="sxs-lookup"><span data-stu-id="4bf80-112">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="4bf80-113">Azure AD B2B 공동 작업이란?</span><span class="sxs-lookup"><span data-stu-id="4bf80-113">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="4bf80-114">B2B 공동 작업 사용자 속성</span><span class="sxs-lookup"><span data-stu-id="4bf80-114">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="4bf80-115">역할에 B2B 공동 작업 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="4bf80-115">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="4bf80-116">B2B 공동 작업 초대 위임</span><span class="sxs-lookup"><span data-stu-id="4bf80-116">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="4bf80-117">동적 그룹 및 B2B 공동 작업</span><span class="sxs-lookup"><span data-stu-id="4bf80-117">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="4bf80-118">B2B 공동 작업 코드 및 PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="4bf80-118">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="4bf80-119">B2B 공동 작업을 위한 SaaS 앱 구성</span><span class="sxs-lookup"><span data-stu-id="4bf80-119">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="4bf80-120">B2B 공동 작업 사용자 토큰</span><span class="sxs-lookup"><span data-stu-id="4bf80-120">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="4bf80-121">B2B 공동 작업 사용자 클레임 매핑</span><span class="sxs-lookup"><span data-stu-id="4bf80-121">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="4bf80-122">Office 365 외부 공유</span><span class="sxs-lookup"><span data-stu-id="4bf80-122">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="4bf80-123">B2B 공동 작업 현재 제한</span><span class="sxs-lookup"><span data-stu-id="4bf80-123">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
