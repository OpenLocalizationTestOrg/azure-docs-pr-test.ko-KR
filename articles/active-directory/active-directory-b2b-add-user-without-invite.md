---
title: "초대 없이 Azure Active Directory에 B2B 공동 작업 사용자 추가 | Microsoft Docs"
description: "게스트 사용자가 Azure Active Directory B2B 공동 작업에서 초대를 사용하지 않고 Azure AD에 다른 게스트 사용자를 추가하도록 할 수 있습니다."
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
ms.openlocfilehash: 91b9477cdb679851e7d8d2942c06999a05f64e46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="add-b2b-collaboration-guest-users-without-an-invitation"></a><span data-ttu-id="3506c-103">초대 없이 B2B 공동 작업 게스트 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="3506c-103">Add B2B collaboration guest users without an invitation</span></span>

<span data-ttu-id="3506c-104">파트너 담당자와 같은 사용자가 초대를 사용하지 않고 파트너의 사용자를 조직에 추가하도록 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3506c-104">You can allow a user, such as a partner representative, to add users from the partner to your organization without needing invitations to be redeemed.</span></span> <span data-ttu-id="3506c-105">파트너 조직에 사용 중인 디렉터리에서 해당 사용자에게 열거형 권한을 부여하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3506c-105">All you must do is grant that user enumeration privileges in the directory you're using for the partner org.</span></span> 

<span data-ttu-id="3506c-106">다음과 같은 경우에 이러한 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="3506c-106">Grant these privileges when:</span></span>

1. <span data-ttu-id="3506c-107">호스트 조직(예: WoodGrove)의 한 사용자가 파트너 조직(예: Sam@litware.com)의 한 사용자를 게스트로 초대합니다.</span><span class="sxs-lookup"><span data-stu-id="3506c-107">A user in the host organization (for example, WoodGrove) invites one user from the partner organization (for example, Sam@litware.com) as Guest.</span></span>
2. <span data-ttu-id="3506c-108">호스트 조직의 관리자는 Sam이 파트너 조직(Litware)의 다른 사용자를 식별하고 추가할 수 있도록 하는 정책을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3506c-108">The admin in the host organization sets up policies that allow Sam to identify and add other users from the partner organization (Litware).</span></span>
3. <span data-ttu-id="3506c-109">이제 Sam은 초대를 돌려받지 않아도 Litware의 다른 사용자를 WoodGrove 디렉터리, 그룹 또는 응용 프로그램에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3506c-109">Now Sam can add other users from Litware to the WoodGrove directory, groups, or applications without needing invitations to be redeemed.</span></span> <span data-ttu-id="3506c-110">Sam에게 Litware의 적절한 열거 권한이 있으면 이러한 작업이 자동으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="3506c-110">If Sam has the appropriate enumeration privileges in Litware, it happens automatically.</span></span>

### <a name="next-steps"></a><span data-ttu-id="3506c-111">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3506c-111">Next steps</span></span>

<span data-ttu-id="3506c-112">Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:</span><span class="sxs-lookup"><span data-stu-id="3506c-112">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="3506c-113">Azure AD B2B 공동 작업이란?</span><span class="sxs-lookup"><span data-stu-id="3506c-113">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="3506c-114">Azure Active Directory 관리자가 B2B 공동 작업 사용자를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="3506c-114">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="3506c-115">정보 근로자가 B2B 공동 작업 사용자를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="3506c-115">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="3506c-116">B2B 공동 작업 초대 전자 메일의 요소</span><span class="sxs-lookup"><span data-stu-id="3506c-116">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="3506c-117">B2B 공동 작업 초대 상환</span><span class="sxs-lookup"><span data-stu-id="3506c-117">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="3506c-118">Azure AD B2B 공동 작업 라이선스</span><span class="sxs-lookup"><span data-stu-id="3506c-118">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="3506c-119">Azure Active Directory B2B 공동 작업 문제 해결</span><span class="sxs-lookup"><span data-stu-id="3506c-119">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="3506c-120">Azure Active Directory B2B 공동 작업 자주 묻는 질문(FAQ)</span><span class="sxs-lookup"><span data-stu-id="3506c-120">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="3506c-121">Azure Active Directory B2B 공동 작업 API 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="3506c-121">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="3506c-122">B2B 공동 작업 사용자에 대한 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="3506c-122">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="3506c-123">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="3506c-123">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)