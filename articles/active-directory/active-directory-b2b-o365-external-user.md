---
title: "aaaOffice 365 외부 공유 및 Azure Active Directory B2B 공동 작업 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업에 대한 클레임 매핑 참조"
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
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 60452b27b328453eda729bd839c982b479cb6f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="b652d-103">Office 365 외부 공유 및 Azure Active Directory B2B 공동 작업</span><span class="sxs-lookup"><span data-stu-id="b652d-103">Office 365 external sharing and Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="b652d-104">Office 365 (OneDrive, SharePoint Online, 그룹 통합, 등) 및 Azure Active Directory (Azure AD) B2B 공동 작업은 기술적으로 공유 하 고 외부 hello 동일한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b652d-104">External sharing in Office 365 (OneDrive, SharePoint Online, Unified Groups, etc.) and Azure Active Directory (Azure AD) B2B collaboration are technically hello same thing.</span></span> <span data-ttu-id="b652d-105">이미 hello Azure AD B2B 공동 작업 초대 Api를 사용 하 여 공유 하는 데을 Office 365 그룹에 게스트를 비롯 한 모든 외부 공유 (OneDrive/SharePoint Online) 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="b652d-105">All external sharing (except OneDrive/SharePoint Online), including guests in Office 365 Groups, already uses hello Azure AD B2B collaboration invitation APIs for sharing.</span></span>

<span data-ttu-id="b652d-106">OneDrive/SharePoint Online에는 별도 초대 관리자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b652d-106">OneDrive/SharePoint Online has a separate invitation manager.</span></span> <span data-ttu-id="b652d-107">OneDrive/SharePoint Online의 외부 공유 지원은 Azure AD에서 지원을 개발하기 전에 시작되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b652d-107">Support for external sharing in OneDrive/SharePoint Online started before Azure AD developed its support.</span></span> <span data-ttu-id="b652d-108">시간이 지남에 따라 몇 가지 기능을 계산에 OneDrive/SharePoint Online 외부 공유 하 고 수백만 hello 제품을 사용 하는 사용자의 기본 제공 패턴을 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="b652d-108">Over time, OneDrive/SharePoint Online external sharing has accrued several features and many millions of users who use hello product's in-built sharing pattern.</span></span> <span data-ttu-id="b652d-109">그렇지만 OneDrive/SharePoint Online 외부 공유의 작동 방식과 Azure AD B2B 공동 작업의 작동 방식 간에 미묘한 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b652d-109">However, there are some subtle differences between how OneDrive/SharePoint Online external sharing works and how Azure AD B2B collaboration works:</span></span>

- <span data-ttu-id="b652d-110">OneDrive/SharePoint Online 사용자 toohello 디렉터리 사용자가 초대를 회수 된 후 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b652d-110">OneDrive/SharePoint Online adds users toohello directory after users have redeemed their invitations.</span></span> <span data-ttu-id="b652d-111">따라서 상환 하기 전에 hello 사용자 Azure AD 포털에 표시 되지 않으면 합니다.</span><span class="sxs-lookup"><span data-stu-id="b652d-111">So, before redemption, you don't see hello user in Azure AD portal.</span></span> <span data-ttu-id="b652d-112">다른 사이트, 그 동안 hello의 사용자 초대 합니다. 새 초대 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652d-112">If another site invites a user in hello meantime, a new invitation is generated.</span></span> <span data-ttu-id="b652d-113">그러나 Azure AD B2B 공동 작업을 사용하면 초대와 동시에 사용자가 추가되므로 모든 위치에 사용자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652d-113">However, when you use Azure AD B2B collaboration, users are added immediately on invitation so that they show up everywhere.</span></span>

- <span data-ttu-id="b652d-114">hello 상환 경험 OneDrive/SharePoint Online에서 Azure AD B2B 공동 작업에서 환경을 hello 다르게 보입니다.</span><span class="sxs-lookup"><span data-stu-id="b652d-114">hello redemption experience in OneDrive/SharePoint Online looks different from hello experience in Azure AD B2B collaboration.</span></span> <span data-ttu-id="b652d-115">사용자 초대 교환, 후 hello 경험 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="b652d-115">After a user redeems an invitation, hello experiences look alike.</span></span>

- <span data-ttu-id="b652d-116">Azure AD B2B 공동 작업의 초대된 사용자는 OneDrive/SharePoint Online 공유 대화 상자에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b652d-116">Azure AD B2B collaboration invited users can be picked from OneDrive/SharePoint Online sharing dialog boxes.</span></span> <span data-ttu-id="b652d-117">OneDrive/SharePoint Online의 초대된 사용자는 초대를 상환한 후 Azure AD에도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652d-117">OneDrive/SharePoint Online invited users also show up in Azure AD after they redeem their invitations.</span></span>

- <span data-ttu-id="b652d-118">외부 toomanage 외부 너무 설정 공유 hello OneDrive/SharePoint Online을 설정 OneDrive/SharePoint Online에서 Azure AD B2B 공동 작업와 공유**만 hello 디렉터리에 이미 외부 사용자와 공유할 수 있도록**합니다.</span><span class="sxs-lookup"><span data-stu-id="b652d-118">toomanage external sharing in OneDrive/SharePoint Online with Azure AD B2B collaboration, set hello OneDrive/SharePoint Online external sharing setting too**Only allow sharing with external users already in hello directory**.</span></span> <span data-ttu-id="b652d-119">사용자가 공유 tooexternally 사이트 이동 수 및 hello 관리 하는 외부 공동 작업자에서 선택이 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b652d-119">Users can go tooexternally shared sites and pick from external collaborators that hello admin has added.</span></span> <span data-ttu-id="b652d-120">admin 님 안녕하세요 hello hello B2B 공동 작업 초대 Api 통해 외부 공동 작업자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b652d-120">hello admin can add hello external collaborators through hello B2B collaboration invitation APIs.</span></span>

![hello OneDrive/SharePoint Online 외부 공유 설정](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a><span data-ttu-id="b652d-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b652d-122">Next steps</span></span>

<span data-ttu-id="b652d-123">Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:</span><span class="sxs-lookup"><span data-stu-id="b652d-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="b652d-124">Azure AD B2B 공동 작업이란?</span><span class="sxs-lookup"><span data-stu-id="b652d-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="b652d-125">B2B 공동 작업 사용자 속성</span><span class="sxs-lookup"><span data-stu-id="b652d-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="b652d-126">B2B 공동 작업 사용자 tooa 역할 추가</span><span class="sxs-lookup"><span data-stu-id="b652d-126">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="b652d-127">B2B 공동 작업 초대 위임</span><span class="sxs-lookup"><span data-stu-id="b652d-127">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="b652d-128">동적 그룹 및 B2B 공동 작업</span><span class="sxs-lookup"><span data-stu-id="b652d-128">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="b652d-129">B2B 공동 작업 코드 및 PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="b652d-129">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="b652d-130">B2B 공동 작업을 위한 SaaS 앱 구성</span><span class="sxs-lookup"><span data-stu-id="b652d-130">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="b652d-131">B2B 공동 작업 사용자 토큰</span><span class="sxs-lookup"><span data-stu-id="b652d-131">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="b652d-132">B2B 공동 작업 사용자 클레임 매핑</span><span class="sxs-lookup"><span data-stu-id="b652d-132">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="b652d-133">B2B 공동 작업 현재 제한</span><span class="sxs-lookup"><span data-stu-id="b652d-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
