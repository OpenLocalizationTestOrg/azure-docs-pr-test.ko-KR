---
title: "Office 365 외부 공유 및 Azure Active Directory B2B 공동 작업 | Microsoft Docs"
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
ms.openlocfilehash: cad0ce8f745f3d6ca14436fd714b08c60de0e459
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="1a8e2-103">Office 365 외부 공유 및 Azure Active Directory B2B 공동 작업</span><span class="sxs-lookup"><span data-stu-id="1a8e2-103">Office 365 external sharing and Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="1a8e2-104">Office 365의 외부 공유(OneDrive, SharePoint Online, 통합 그룹 등) 기능과 Azure AD(Azure Active Directory) B2B 공동 작업 기능은 기술적으로 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="1a8e2-104">External sharing in Office 365 (OneDrive, SharePoint Online, Unified Groups, etc.) and Azure Active Directory (Azure AD) B2B collaboration are technically the same thing.</span></span> <span data-ttu-id="1a8e2-105">Office 365 그룹의 게스트를 비롯한 모든 외부 공유(OneDrive/SharePoint Online 제외)는 이미 공유에 Azure AD B2B 공동 작업 초대 API를 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8e2-105">All external sharing (except OneDrive/SharePoint Online), including guests in Office 365 Groups, already uses the Azure AD B2B collaboration invitation APIs for sharing.</span></span>

<span data-ttu-id="1a8e2-106">OneDrive/SharePoint Online에는 별도 초대 관리자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8e2-106">OneDrive/SharePoint Online has a separate invitation manager.</span></span> <span data-ttu-id="1a8e2-107">OneDrive/SharePoint Online의 외부 공유 지원은 Azure AD에서 지원을 개발하기 전에 시작되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8e2-107">Support for external sharing in OneDrive/SharePoint Online started before Azure AD developed its support.</span></span> <span data-ttu-id="1a8e2-108">시간이 지남에 따라 OneDrive/SharePoint Online 외부 공유의 기능도 늘어나고 수많은 사용자들이 이 제품의 기본 제공 공유 패턴을 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8e2-108">Over time, OneDrive/SharePoint Online external sharing has accrued several features and many millions of users who use the product's in-built sharing pattern.</span></span> <span data-ttu-id="1a8e2-109">그렇지만 OneDrive/SharePoint Online 외부 공유의 작동 방식과 Azure AD B2B 공동 작업의 작동 방식 간에 미묘한 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8e2-109">However, there are some subtle differences between how OneDrive/SharePoint Online external sharing works and how Azure AD B2B collaboration works:</span></span>

- <span data-ttu-id="1a8e2-110">사용자가 초대를 교환하면 OneDrive/SharePoint Online은 사용자를 디렉터리에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1a8e2-110">OneDrive/SharePoint Online adds users to the directory after users have redeemed their invitations.</span></span> <span data-ttu-id="1a8e2-111">따라서 교환 전에는 Azure AD 포털에 사용자가 보이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8e2-111">So, before redemption, you don't see the user in Azure AD portal.</span></span> <span data-ttu-id="1a8e2-112">그 사이에 다른 사이트에서 사용자를 초대하면 새 초대가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a8e2-112">If another site invites a user in the meantime, a new invitation is generated.</span></span> <span data-ttu-id="1a8e2-113">그러나 Azure AD B2B 공동 작업을 사용하면 초대와 동시에 사용자가 추가되므로 모든 위치에 사용자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a8e2-113">However, when you use Azure AD B2B collaboration, users are added immediately on invitation so that they show up everywhere.</span></span>

- <span data-ttu-id="1a8e2-114">OneDrive/SharePoint Online의 교환 환경은 Azure AD B2B 공동 작업의 환경과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="1a8e2-114">The redemption experience in OneDrive/SharePoint Online looks different from the experience in Azure AD B2B collaboration.</span></span> <span data-ttu-id="1a8e2-115">사용자가 초대를 교환하면 환경이 비슷하게 보입니다.</span><span class="sxs-lookup"><span data-stu-id="1a8e2-115">After a user redeems an invitation, the experiences look alike.</span></span>

- <span data-ttu-id="1a8e2-116">Azure AD B2B 공동 작업의 초대된 사용자는 OneDrive/SharePoint Online 공유 대화 상자에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8e2-116">Azure AD B2B collaboration invited users can be picked from OneDrive/SharePoint Online sharing dialog boxes.</span></span> <span data-ttu-id="1a8e2-117">OneDrive/SharePoint Online의 초대된 사용자는 초대를 상환한 후 Azure AD에도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a8e2-117">OneDrive/SharePoint Online invited users also show up in Azure AD after they redeem their invitations.</span></span>

- <span data-ttu-id="1a8e2-118">Azure AD B2B 공동 작업 기능으로 OneDrive/SharePoint Online의 외부 공유를 관리하려면 OneDrive/SharePoint Online 외부 공유 설정을 **디렉터리에 이미 있는 외부 사용자와의 공유만 허용**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1a8e2-118">To manage external sharing in OneDrive/SharePoint Online with Azure AD B2B collaboration, set the OneDrive/SharePoint Online external sharing setting to **Only allow sharing with external users already in the directory**.</span></span> <span data-ttu-id="1a8e2-119">사용자는 외부에서 공유되는 사이트로 이동하여 관리자가 추가한 외부 공동 관리자 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8e2-119">Users can go to externally shared sites and pick from external collaborators that the admin has added.</span></span> <span data-ttu-id="1a8e2-120">관리자는 B2B 공동 작업 초대 API를 통해 외부 공동 작업자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8e2-120">The admin can add the external collaborators through the B2B collaboration invitation APIs.</span></span>

![OneDrive/SharePoint Online 외부 공유 설정](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a><span data-ttu-id="1a8e2-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1a8e2-122">Next steps</span></span>

<span data-ttu-id="1a8e2-123">Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:</span><span class="sxs-lookup"><span data-stu-id="1a8e2-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="1a8e2-124">Azure AD B2B 공동 작업이란?</span><span class="sxs-lookup"><span data-stu-id="1a8e2-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="1a8e2-125">B2B 공동 작업 사용자 속성</span><span class="sxs-lookup"><span data-stu-id="1a8e2-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="1a8e2-126">역할에 B2B 공동 작업 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="1a8e2-126">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="1a8e2-127">B2B 공동 작업 초대 위임</span><span class="sxs-lookup"><span data-stu-id="1a8e2-127">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="1a8e2-128">동적 그룹 및 B2B 공동 작업</span><span class="sxs-lookup"><span data-stu-id="1a8e2-128">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="1a8e2-129">B2B 공동 작업 코드 및 PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="1a8e2-129">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="1a8e2-130">B2B 공동 작업을 위한 SaaS 앱 구성</span><span class="sxs-lookup"><span data-stu-id="1a8e2-130">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="1a8e2-131">B2B 공동 작업 사용자 토큰</span><span class="sxs-lookup"><span data-stu-id="1a8e2-131">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="1a8e2-132">B2B 공동 작업 사용자 클레임 매핑</span><span class="sxs-lookup"><span data-stu-id="1a8e2-132">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="1a8e2-133">B2B 공동 작업 현재 제한</span><span class="sxs-lookup"><span data-stu-id="1a8e2-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
