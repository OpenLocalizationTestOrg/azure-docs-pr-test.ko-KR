---
title: "Azure Active Directory B2B 공동 작업을 위한 셀프 서비스 등록 포털 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업은 비즈니스 파트너가 선택적으로 회사 응용 프로그램에 액세스할 수 있게 함으로써 회사 간 관계를 지원합니다."
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
ms.openlocfilehash: 307373c75bbb87cec683f7a3097f8f159c9d5e61
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="self-service-portal-for-azure-ad-b2b-collaboration-sign-up"></a><span data-ttu-id="6993d-103">Azure AD B2B 공동 작업 등록을 위한 셀프 서비스 포털</span><span class="sxs-lookup"><span data-stu-id="6993d-103">Self-service portal for Azure AD B2B collaboration sign-up</span></span>

<span data-ttu-id="6993d-104">고객은 최종 사용자를 위한 IT 관리 [Azure Portal](https://portal.azure.com) 및 [응용 프로그램 액세스 패널](https://myapps.microsoft.com)을 통해 제공되는 기본 제공 기능으로 많은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6993d-104">Customers can do a lot with the built-in features that are exposed through our IT admin [Azure portal](https://portal.azure.com) and our [Application Access Panel](https://myapps.microsoft.com) for end users.</span></span> <span data-ttu-id="6993d-105">그렇지만 기업에서는 조직의 요구에 맞게 B2B 사용자에 대한 온보딩 워크플로를 사용자 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6993d-105">But we are also aware that businesses need to customize the onboarding workflow for B2B users to fit their organization’s needs.</span></span> <span data-ttu-id="6993d-106">이러한 작업은 [API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)를 통해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6993d-106">They can do that with [our API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).</span></span>

<span data-ttu-id="6993d-107">고객들과 이러한 점을 논의하면서 일반적인 요구가 있다는 것을 알게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6993d-107">In discussions with our customers, we see one common need rise up above all others.</span></span> <span data-ttu-id="6993d-108">초대하는 조직이 리소스에 액세스할 필요가 있는 개별 외부 공동 작업자가 누구인지를 미리 알지 못할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6993d-108">The inviting organization may not know ahead of time who the individual external collaborators are who need access to their resources.</span></span> <span data-ttu-id="6993d-109">고객들은 파트너 회사의 사용자가 초대하는 조직이 제어하는 정책 집합으로 자체 등록할 수 있는 방식을 원했습니다.</span><span class="sxs-lookup"><span data-stu-id="6993d-109">They wanted a way for users from partner companies to  sign themselves up with a set of policies that the inviting organization controls.</span></span> <span data-ttu-id="6993d-110">이 시나리오는 API를 통해 구현될 수 있습니다. 따라서 이러한 작업을 수행하는 [샘플 Github 프로젝트](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web)를 GItHub에 게시했습니다.</span><span class="sxs-lookup"><span data-stu-id="6993d-110">This scenario is possible through our APIs,  so we published a project on Github that did just that: [sample Github project](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span></span>

<span data-ttu-id="6993d-111">Github 프로젝트는 조직이 API를 사용하고, 액세스해야 하는 앱을 결정하는 규칙을 통해 신뢰할 수 있는 파트너에게 정책 기반의 셀프 서비스 등록 기능을 제공하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6993d-111">Our Github project demonstrates how organizations can use our APIs, and provide a policy-based, self-service sign-up capability for their trusted partners, with rules that determine the apps they can access.</span></span> <span data-ttu-id="6993d-112">초대하는 조직이 수동으로 온보딩할 필요 없이 파트너 사용자는 필요할 때 안전하게 적절한 리소스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6993d-112">Partner users can get access to resources when they need them, securely, without requiring the inviting organization to manually onboard them.</span></span> <span data-ttu-id="6993d-113">사용자가 선택한 Azure 구독에 프로젝트를 쉽게 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6993d-113">You can easily deploy the project into an Azure subscription of your choice.</span></span>

## <a name="as-is-code"></a><span data-ttu-id="6993d-114">원본 코드</span><span class="sxs-lookup"><span data-stu-id="6993d-114">As-is code</span></span>

<span data-ttu-id="6993d-115">이 코드는 Azure Active Directory B2B 초대 API의 사용법을 보여 주기 위해 샘플로 사용할 수 있게 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6993d-115">Remember that this code is made available as a sample to demonstrate usage of the Azure Active Directory B2B invitation API.</span></span> <span data-ttu-id="6993d-116">따라서 개발 팀 또는 파트너가 코드를 사용자 지정해야 하고 프로덕션 시나리오에서 배포하기 전에 검토해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6993d-116">It should be customized by your dev team or a partner, and should be reviewed before being deployed in a production scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6993d-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6993d-117">Next steps</span></span>

<span data-ttu-id="6993d-118">Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:</span><span class="sxs-lookup"><span data-stu-id="6993d-118">Browse our other articles on Azure AD B2B collaboration:</span></span>
* [<span data-ttu-id="6993d-119">Azure AD B2B 공동 작업이란?</span><span class="sxs-lookup"><span data-stu-id="6993d-119">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="6993d-120">Azure Active Directory 관리자가 B2B 공동 작업 사용자를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="6993d-120">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="6993d-121">정보 근로자가 B2B 공동 작업 사용자를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="6993d-121">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="6993d-122">B2B 공동 작업 초대 전자 메일의 요소</span><span class="sxs-lookup"><span data-stu-id="6993d-122">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="6993d-123">B2B 공동 작업 초대 상환</span><span class="sxs-lookup"><span data-stu-id="6993d-123">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="6993d-124">Azure AD B2B 공동 작업 라이선스</span><span class="sxs-lookup"><span data-stu-id="6993d-124">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="6993d-125">Azure Active Directory B2B 공동 작업 문제 해결</span><span class="sxs-lookup"><span data-stu-id="6993d-125">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="6993d-126">Azure Active Directory B2B 공동 작업 자주 묻는 질문(FAQ)</span><span class="sxs-lookup"><span data-stu-id="6993d-126">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="6993d-127">B2B 공동 작업 사용자에 대한 다단계 인증</span><span class="sxs-lookup"><span data-stu-id="6993d-127">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="6993d-128">초대 없이 B2B 공동 작업 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="6993d-128">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="6993d-129">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="6993d-129">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)