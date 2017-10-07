---
title: "aaaCompare B2B 공동 작업 및 Azure Active directory에서 B2C | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업 및 Azure AD B2C hello 차이 무엇입니까?"
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
ms.openlocfilehash: 34d88b9a7d023e077568e8df3d5e1610ae05b361
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="compare-b2b-collaboration-and-b2c-in-azure-active-directory"></a><span data-ttu-id="91150-103">Azure Active Directory에서 B2B 공동 작업과 B2C 비교</span><span class="sxs-lookup"><span data-stu-id="91150-103">Compare B2B collaboration and B2C in Azure Active Directory</span></span>

<span data-ttu-id="91150-104">Azure Active Directory (Azure AD) B2B 공동 작업 및 Azure AD B2C 모두 사용 하면 toowork 외부 사용자와 Azure AD에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91150-104">Both Azure Active Directory (Azure AD) B2B collaboration and Azure AD B2C allow you toowork with external users in Azure AD.</span></span> <span data-ttu-id="91150-105">하지만 어떻게 비교할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="91150-105">But how do they compare?</span></span>


<span data-ttu-id="91150-106">B2B 공동 작업 기능</span><span class="sxs-lookup"><span data-stu-id="91150-106">B2B collaboration capabilities</span></span> |     <span data-ttu-id="91150-107">Azure AD B2C 독립 실행형 제품</span><span class="sxs-lookup"><span data-stu-id="91150-107">Azure AD B2C stand-alone offering</span></span>
-------- | --------
<span data-ttu-id="91150-108">위한: toobe 수 tooauthenticate 사용자가 id 공급자에 관계 없이 파트너 조직에서 하려는 조직은 합니다.</span><span class="sxs-lookup"><span data-stu-id="91150-108">Intended for: Organizations that want toobe able tooauthenticate users from a partner organization, regardless of identity provider.</span></span> | <span data-ttu-id="91150-109">대상: 개인이든, 기관이든, 조직이든 상관없이 모바일 및 웹앱 고객을 Azure AD에 초대하려는 사용자</span><span class="sxs-lookup"><span data-stu-id="91150-109">Intended for: Inviting customers of your mobile and web apps, whether individuals, institutional or organizational customers into your Azure AD.</span></span>
<span data-ttu-id="91150-110">지원되는 ID: 회사 또는 학교 계정이 있는 직원, 회사 또는 학교 계정이 있는 파트너 또는 모든 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="91150-110">Identities supported: Employees with work or school accounts, partners with work or school accounts, or any email address.</span></span> <span data-ttu-id="91150-111">곧 toosupport 직접 페더레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="91150-111">Soon toosupport direct federation.</span></span>  | <span data-ttu-id="91150-112">지원되는 ID: 로컬 응용 프로그램 계정(모든 전자 메일 주소 또는 사용자 이름)이 있는 소비자 사용자 또는 직접 페더레이션이 포함된 지원되는 소셜 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="91150-112">Identities supported: Consumer users with local application accounts (any email address or user name) or any supported social identity with direct federation.</span></span>
<span data-ttu-id="91150-113">Hello 파트너 사용자 디렉터리에 있는: hello 외부 조직의 사용자에서 관리 되는 파트너 hello 주석이 추가 된 하지만 직원와 동일한 디렉터리 특별 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="91150-113">Which directory hello partner users are in: Partner users from hello external organization are managed in hello same directory as employees, but annotated specially.</span></span> <span data-ttu-id="91150-114">자격 증명은 관리 hello 동일한 직원으로 방식으로 추가 된 toohello 동일한 그룹 및 수 등</span><span class="sxs-lookup"><span data-stu-id="91150-114">They can be managed hello same way as employees, can be added toohello same groups, and so on</span></span>  | <span data-ttu-id="91150-115">에 디렉터리 hello 고객 사용자 엔터티는 어떤: hello 응용 프로그램 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91150-115">Which directory hello customer user entities are in: In hello application directory.</span></span> <span data-ttu-id="91150-116">Hello 조직의 직원 및 파트너 디렉터리 (해당 되는 경우에서 별도로 관리.</span><span class="sxs-lookup"><span data-stu-id="91150-116">Managed separately from hello organization’s employee and partner directory (if any.</span></span>
<span data-ttu-id="91150-117">Single sign-on (SSO) tooall Azure AD에 연결 된 앱은 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91150-117">Single sign-on (SSO) tooall Azure AD-connected apps is supported.</span></span> <span data-ttu-id="91150-118">예를 들어 액세스 tooOffice 365 또는 온-프레미스 앱 및 Salesforce 또는 Workday 같은 tooother SaaS 앱을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91150-118">For example, you can provide access tooOffice 365 or on-premises apps, and tooother SaaS apps such as Salesforce or Workday.</span></span>  |  <span data-ttu-id="91150-119">SSO toocustomer hello Azure AD B2C 테 넌 트 내에서 앱은 지원 되는 소유 합니다.</span><span class="sxs-lookup"><span data-stu-id="91150-119">SSO toocustomer owned apps within hello Azure AD B2C tenants is supported.</span></span> <span data-ttu-id="91150-120">SSO tooOffice 365 tooother Microsoft 및 타사 SaaS 응용 프로그램 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91150-120">SSO tooOffice 365 or tooother Microsoft and non-Microsoft SaaS apps is not supported.</span></span>
<span data-ttu-id="91150-121">파트너 수명 주기: hello 호스트/초대 조직에서 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="91150-121">Partner lifecycle: Managed by hello host/inviting organization.</span></span>  | <span data-ttu-id="91150-122">고객 수명 주기: 셀프 서비스 또는 hello 응용 프로그램에 의해 관리 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="91150-122">Customer lifecycle: Self-serve or managed by hello application.</span></span>
<span data-ttu-id="91150-123">보안 정책 및 규정 준수: hello 호스트/초대 조직에서 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="91150-123">Security policy and compliance: Managed by hello host/inviting organization.</span></span>  | <span data-ttu-id="91150-124">보안 정책 및 규정 준수: hello 응용 프로그램으로 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="91150-124">Security policy and compliance: Managed by hello application.</span></span>
<span data-ttu-id="91150-125">브랜딩: 호스트/초대한 조직의 브랜드가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="91150-125">Branding: Host/inviting organization’s brand is used.</span></span>  |    <span data-ttu-id="91150-126">브랜딩: 응용 프로그램에 의해 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="91150-126">Branding: Managed by application.</span></span> <span data-ttu-id="91150-127">일반적으로 제품이 나 hello 배경으로 hello 조직 페이드 toobe 제품을 경향이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91150-127">Typically tends toobe product branded, with hello organization fading into hello background.</span></span>
<span data-ttu-id="91150-128">추가 정보: [블로그 게시물](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/01/azure-ad-b2b-new-updates-make-cross-business-collab-easy/), [설명서](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)</span><span class="sxs-lookup"><span data-stu-id="91150-128">More info: [Blog post](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/01/azure-ad-b2b-new-updates-make-cross-business-collab-easy/), [Documentation](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)</span></span>  | <span data-ttu-id="91150-129">추가 정보: [제품 페이지](https://azure.microsoft.com/en-us/services/active-directory-b2c/), [설명서](https://docs.microsoft.com/en-us/azure/active-directory-b2c/)</span><span class="sxs-lookup"><span data-stu-id="91150-129">More info: [Product page](https://azure.microsoft.com/en-us/services/active-directory-b2c/), [Documentation](https://docs.microsoft.com/en-us/azure/active-directory-b2c/)</span></span>


### <a name="next-steps"></a><span data-ttu-id="91150-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="91150-130">Next steps</span></span>

<span data-ttu-id="91150-131">Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:</span><span class="sxs-lookup"><span data-stu-id="91150-131">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="91150-132">Azure AD B2B 공동 작업이란?</span><span class="sxs-lookup"><span data-stu-id="91150-132">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="91150-133">B2B 공동 작업 사용자 속성</span><span class="sxs-lookup"><span data-stu-id="91150-133">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="91150-134">B2B 공동 작업 사용자 tooa 역할 추가</span><span class="sxs-lookup"><span data-stu-id="91150-134">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="91150-135">B2B 공동 작업 초대 위임</span><span class="sxs-lookup"><span data-stu-id="91150-135">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="91150-136">동적 그룹 및 B2B 공동 작업</span><span class="sxs-lookup"><span data-stu-id="91150-136">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="91150-137">B2B 공동 작업용 SaaS 앱 구성</span><span class="sxs-lookup"><span data-stu-id="91150-137">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="91150-138">B2B 공동 작업 사용자 토큰</span><span class="sxs-lookup"><span data-stu-id="91150-138">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="91150-139">B2B 공동 작업 사용자 클레임 매핑</span><span class="sxs-lookup"><span data-stu-id="91150-139">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="91150-140">Office 365 외부 공유</span><span class="sxs-lookup"><span data-stu-id="91150-140">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="91150-141">B2B 공동 작업 현재 제한</span><span class="sxs-lookup"><span data-stu-id="91150-141">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
* [<span data-ttu-id="91150-142">B2B 공동 작업에 대한 지원 받기</span><span class="sxs-lookup"><span data-stu-id="91150-142">Getting support for B2B collaboration</span></span>](active-directory-b2b-support.md)
