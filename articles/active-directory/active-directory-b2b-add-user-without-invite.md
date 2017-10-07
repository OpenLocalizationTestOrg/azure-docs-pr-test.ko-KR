---
title: "초대 없이 aaaAdd B2B 공동 작업 사용자 tooAzure Active Directory | Microsoft Docs"
description: "게스트 사용자를 Azure Active Directory B2B 공동 작업에 초대를 교환 하지 않고 다른 게스트 사용자 tooyour Azure AD를 추가 하도록 할 수 있습니다."
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
ms.openlocfilehash: 459d99b9f856a35973d1b2cbfabdc23fe40c8f44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-b2b-collaboration-guest-users-without-an-invitation"></a><span data-ttu-id="68b26-103">초대 없이 B2B 공동 작업 게스트 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="68b26-103">Add B2B collaboration guest users without an invitation</span></span>

<span data-ttu-id="68b26-104">교환할 초대 toobe 필요 없이 hello 파트너 tooyour 조직에서 파트너 대표값을 tooadd 사용자 같은 사용자를 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68b26-104">You can allow a user, such as a partner representative, tooadd users from hello partner tooyour organization without needing invitations toobe redeemed.</span></span> <span data-ttu-id="68b26-105">Hello 파트너 조직에 사용할 hello 디렉터리에서 열거형 권한을 해당 사용자에 게 부여 해야 할 모든를</span><span class="sxs-lookup"><span data-stu-id="68b26-105">All you must do is grant that user enumeration privileges in hello directory you're using for hello partner org.</span></span> 

<span data-ttu-id="68b26-106">다음과 같은 경우에 이러한 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="68b26-106">Grant these privileges when:</span></span>

1. <span data-ttu-id="68b26-107">Hello 호스트 조직 (예를 들어 WoodGrove)에 있는 사용자 초대 hello 파트너 조직에서 한 명의 사용자 (예를 들어 Sam@litware.com) 게스트로 합니다.</span><span class="sxs-lookup"><span data-stu-id="68b26-107">A user in hello host organization (for example, WoodGrove) invites one user from hello partner organization (for example, Sam@litware.com) as Guest.</span></span>
2. <span data-ttu-id="68b26-108">hello 호스트 조직에서 admin 님 안녕하세요 Sam tooidentify 허용 하 고 hello 파트너 조직 (Litware) 다른 사용자를 추가 하는 정책을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="68b26-108">hello admin in hello host organization sets up policies that allow Sam tooidentify and add other users from hello partner organization (Litware).</span></span>
3. <span data-ttu-id="68b26-109">이제 Sam 교환할 초대 toobe 필요 없이 Litware toohello WoodGrove 디렉터리, 그룹 또는 응용 프로그램에서 다른 사용자가 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68b26-109">Now Sam can add other users from Litware toohello WoodGrove directory, groups, or applications without needing invitations toobe redeemed.</span></span> <span data-ttu-id="68b26-110">Sam Litware에 hello 열거형 적절 한 권한이 있으면 자동으로 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="68b26-110">If Sam has hello appropriate enumeration privileges in Litware, it happens automatically.</span></span>

### <a name="next-steps"></a><span data-ttu-id="68b26-111">다음 단계</span><span class="sxs-lookup"><span data-stu-id="68b26-111">Next steps</span></span>

<span data-ttu-id="68b26-112">Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:</span><span class="sxs-lookup"><span data-stu-id="68b26-112">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="68b26-113">Azure AD B2B 공동 작업이란?</span><span class="sxs-lookup"><span data-stu-id="68b26-113">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="68b26-114">Azure Active Directory 관리자가 B2B 공동 작업 사용자를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="68b26-114">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="68b26-115">정보 근로자가 B2B 공동 작업 사용자를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="68b26-115">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="68b26-116">hello B2B 공동 작업 초대 메일의 hello 요소</span><span class="sxs-lookup"><span data-stu-id="68b26-116">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="68b26-117">B2B 공동 작업 초대 상환</span><span class="sxs-lookup"><span data-stu-id="68b26-117">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="68b26-118">Azure AD B2B 공동 작업 라이선스</span><span class="sxs-lookup"><span data-stu-id="68b26-118">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="68b26-119">Azure Active Directory B2B 공동 작업 문제 해결</span><span class="sxs-lookup"><span data-stu-id="68b26-119">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="68b26-120">Azure Active Directory B2B 공동 작업 자주 묻는 질문(FAQ)</span><span class="sxs-lookup"><span data-stu-id="68b26-120">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="68b26-121">Azure Active Directory B2B 공동 작업 API 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="68b26-121">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="68b26-122">B2B 공동 작업 사용자에 대한 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="68b26-122">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="68b26-123">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="68b26-123">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)