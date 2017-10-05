---
title: "Azure Active Directory에서 B2B 공동 작업과 B2C 비교 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업과 Azure AD B2C 간의 차이는 무엇인가요?"
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
ms.openlocfilehash: 44cbbc149787a2d6cf2e0e8750b98d33b52f6136
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="compare-b2b-collaboration-and-b2c-in-azure-active-directory"></a><span data-ttu-id="c809d-103">Azure Active Directory에서 B2B 공동 작업과 B2C 비교</span><span class="sxs-lookup"><span data-stu-id="c809d-103">Compare B2B collaboration and B2C in Azure Active Directory</span></span>

<span data-ttu-id="c809d-104">Azure Active Directory(Azure AD) B2B 공동 작업 및 Azure AD B2C 모두를 사용하여 Azure AD에서 외부 사용자와 함께 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c809d-104">Both Azure Active Directory (Azure AD) B2B collaboration and Azure AD B2C allow you to work with external users in Azure AD.</span></span> <span data-ttu-id="c809d-105">하지만 어떻게 비교할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="c809d-105">But how do they compare?</span></span>


<span data-ttu-id="c809d-106">B2B 공동 작업 기능</span><span class="sxs-lookup"><span data-stu-id="c809d-106">B2B collaboration capabilities</span></span> |     <span data-ttu-id="c809d-107">Azure AD B2C 독립 실행형 제품</span><span class="sxs-lookup"><span data-stu-id="c809d-107">Azure AD B2C stand-alone offering</span></span>
-------- | --------
<span data-ttu-id="c809d-108">대상: ID 공급자에 관계없이 파트너 조직의 사용자를 인증할 수 있기를 원하는 조직</span><span class="sxs-lookup"><span data-stu-id="c809d-108">Intended for: Organizations that want to be able to authenticate users from a partner organization, regardless of identity provider.</span></span> | <span data-ttu-id="c809d-109">대상: 개인이든, 기관이든, 조직이든 상관없이 모바일 및 웹앱 고객을 Azure AD에 초대하려는 사용자</span><span class="sxs-lookup"><span data-stu-id="c809d-109">Intended for: Inviting customers of your mobile and web apps, whether individuals, institutional or organizational customers into your Azure AD.</span></span>
<span data-ttu-id="c809d-110">지원되는 ID: 회사 또는 학교 계정이 있는 직원, 회사 또는 학교 계정이 있는 파트너 또는 모든 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="c809d-110">Identities supported: Employees with work or school accounts, partners with work or school accounts, or any email address.</span></span> <span data-ttu-id="c809d-111">직접 페더레이션 기능을 곧 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c809d-111">Soon to support direct federation.</span></span>  | <span data-ttu-id="c809d-112">지원되는 ID: 로컬 응용 프로그램 계정(모든 전자 메일 주소 또는 사용자 이름)이 있는 소비자 사용자 또는 직접 페더레이션이 포함된 지원되는 소셜 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="c809d-112">Identities supported: Consumer users with local application accounts (any email address or user name) or any supported social identity with direct federation.</span></span>
<span data-ttu-id="c809d-113">파트너 사용자가 위치한 디렉터리: 외부 조직의 파트너 사용자는 직원과 같은 디렉터리에서 관리되지만 특별하게 주석 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="c809d-113">Which directory the partner users are in: Partner users from the external organization are managed in the same directory as employees, but annotated specially.</span></span> <span data-ttu-id="c809d-114">이들은 직원과 같은 방식으로 관리하고 동일한 그룹에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c809d-114">They can be managed the same way as employees, can be added to the same groups, and so on</span></span>  | <span data-ttu-id="c809d-115">고객 사용자 엔터티가 위치한 디렉터리: 응용 프로그램 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c809d-115">Which directory the customer user entities are in: In the application directory.</span></span> <span data-ttu-id="c809d-116">조직의 직원 및 파트너 디렉터리(있는 경우)에서 별도로 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="c809d-116">Managed separately from the organization’s employee and partner directory (if any.</span></span>
<span data-ttu-id="c809d-117">모든 Azure AD 연결 앱에 대한 SSO(Single Sign-On)가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c809d-117">Single sign-on (SSO) to all Azure AD-connected apps is supported.</span></span> <span data-ttu-id="c809d-118">예를 들어 Office 365 또는 온-프레미스 앱 및 다른 SaaS 앱(예: Salesforce 또는 Workday)에 대한 액세스를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c809d-118">For example, you can provide access to Office 365 or on-premises apps, and to other SaaS apps such as Salesforce or Workday.</span></span>  |  <span data-ttu-id="c809d-119">Azure AD B2C 테넌트 내의 고객 소유 앱에 대한 SSO가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c809d-119">SSO to customer owned apps within the Azure AD B2C tenants is supported.</span></span> <span data-ttu-id="c809d-120">Office 365 또는 다른 Microsoft 앱 및 타사 SaaS 앱에 대한 SSO가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c809d-120">SSO to Office 365 or to other Microsoft and non-Microsoft SaaS apps is not supported.</span></span>
<span data-ttu-id="c809d-121">파트너 수명 주기: 호스트/초대한 조직에 의해 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="c809d-121">Partner lifecycle: Managed by the host/inviting organization.</span></span>  | <span data-ttu-id="c809d-122">고객 수명 주기: 셀프 서비스 또는 응용 프로그램에 의해 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="c809d-122">Customer lifecycle: Self-serve or managed by the application.</span></span>
<span data-ttu-id="c809d-123">보안 정책 및 규정 준수: 호스트/초대한 조직에 의해 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="c809d-123">Security policy and compliance: Managed by the host/inviting organization.</span></span>  | <span data-ttu-id="c809d-124">보안 정책 및 규정 준수: 응용 프로그램에 의해 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="c809d-124">Security policy and compliance: Managed by the application.</span></span>
<span data-ttu-id="c809d-125">브랜딩: 호스트/초대한 조직의 브랜드가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c809d-125">Branding: Host/inviting organization’s brand is used.</span></span>  |    <span data-ttu-id="c809d-126">브랜딩: 응용 프로그램에 의해 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="c809d-126">Branding: Managed by application.</span></span> <span data-ttu-id="c809d-127">일반적으로 조직의 존재가 희미해지고 제품 브랜드가 되는 경향이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c809d-127">Typically tends to be product branded, with the organization fading into the background.</span></span>
<span data-ttu-id="c809d-128">추가 정보: [블로그 게시물](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/01/azure-ad-b2b-new-updates-make-cross-business-collab-easy/), [설명서](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)</span><span class="sxs-lookup"><span data-stu-id="c809d-128">More info: [Blog post](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/01/azure-ad-b2b-new-updates-make-cross-business-collab-easy/), [Documentation](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)</span></span>  | <span data-ttu-id="c809d-129">추가 정보: [제품 페이지](https://azure.microsoft.com/en-us/services/active-directory-b2c/), [설명서](https://docs.microsoft.com/en-us/azure/active-directory-b2c/)</span><span class="sxs-lookup"><span data-stu-id="c809d-129">More info: [Product page](https://azure.microsoft.com/en-us/services/active-directory-b2c/), [Documentation](https://docs.microsoft.com/en-us/azure/active-directory-b2c/)</span></span>


### <a name="next-steps"></a><span data-ttu-id="c809d-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c809d-130">Next steps</span></span>

<span data-ttu-id="c809d-131">Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:</span><span class="sxs-lookup"><span data-stu-id="c809d-131">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="c809d-132">Azure AD B2B 공동 작업이란?</span><span class="sxs-lookup"><span data-stu-id="c809d-132">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="c809d-133">B2B 공동 작업 사용자 속성</span><span class="sxs-lookup"><span data-stu-id="c809d-133">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="c809d-134">역할에 B2B 공동 작업 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="c809d-134">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="c809d-135">B2B 공동 작업 초대 위임</span><span class="sxs-lookup"><span data-stu-id="c809d-135">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="c809d-136">동적 그룹 및 B2B 공동 작업</span><span class="sxs-lookup"><span data-stu-id="c809d-136">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="c809d-137">B2B 공동 작업용 SaaS 앱 구성</span><span class="sxs-lookup"><span data-stu-id="c809d-137">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="c809d-138">B2B 공동 작업 사용자 토큰</span><span class="sxs-lookup"><span data-stu-id="c809d-138">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="c809d-139">B2B 공동 작업 사용자 클레임 매핑</span><span class="sxs-lookup"><span data-stu-id="c809d-139">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="c809d-140">Office 365 외부 공유</span><span class="sxs-lookup"><span data-stu-id="c809d-140">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="c809d-141">B2B 공동 작업 현재 제한</span><span class="sxs-lookup"><span data-stu-id="c809d-141">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
* [<span data-ttu-id="c809d-142">B2B 공동 작업에 대한 지원 받기</span><span class="sxs-lookup"><span data-stu-id="c809d-142">Getting support for B2B collaboration</span></span>](active-directory-b2b-support.md)
