---
title: "라이선스: Azure AD SSPR | Microsoft Docs"
description: "Azure AD 셀프 서비스 암호 재설정 라이선스 요구 사항"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 9cecaaac429165346f7082f1965dc8a21063fe7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a><span data-ttu-id="84008-103">Azure AD 셀프 서비스 암호 재설정의 라이선스 요구 사항</span><span class="sxs-lookup"><span data-stu-id="84008-103">Licensing requirements for Azure AD self-service password reset</span></span>

<span data-ttu-id="84008-104">Azure AD 암호 재설정 toofunction 되려면에서 있습니다 **조직에서 할당 된 하나 이상의 라이선스가 있어야**합니다.</span><span class="sxs-lookup"><span data-stu-id="84008-104">In order for Azure AD Password Reset toofunction, you **must have at least one license assigned in your organization**.</span></span> <span data-ttu-id="84008-105">에서는 사용자 단위 hello 암호 재설정 환경에서 라이선스를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84008-105">We do not enforce per-user licensing on hello password reset experience.</span></span> <span data-ttu-id="84008-106">Microsoft 라이선스 계약 toomaintain 규정 준수, 프리미엄 기능을 사용 하는 tooassign 라이선스 tooany 사용자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="84008-106">toomaintain compliance with your Microsoft licensing agreement, you need tooassign licenses tooany users that use premium features.</span></span>

* <span data-ttu-id="84008-107">**클라우드 사용자만 해당** - Office 365(O365) 유료 SKU 또는 Azure AD Basic</span><span class="sxs-lookup"><span data-stu-id="84008-107">**Cloud only users** - Office 365 (O365) any paid SKU, or Azure AD Basic</span></span>
* <span data-ttu-id="84008-108">**클라우드** 및/또는 **온-프레미스 사용자** - Azure AD Premium P1 또는 P2, EMS(Enterprise Mobility + Security) 또는 SPE(Secure Productive Enterprise)</span><span class="sxs-lookup"><span data-stu-id="84008-108">**Cloud** and/or **on-premises users** - Azure AD Premium P1 or P2, Enterprise Mobility + Security (EMS), or Secure Productive Enterprise (SPE)</span></span>

## <a name="licenses-required-for-password-writeback"></a><span data-ttu-id="84008-109">비밀번호 쓰기 저장에 필요한 라이선스</span><span class="sxs-lookup"><span data-stu-id="84008-109">Licenses required for password writeback</span></span>

<span data-ttu-id="84008-110">toouse 암호 쓰기 저장을 있어야 hello 테 넌 트에 할당 된 라이선스를 다음 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="84008-110">toouse password writeback, you must have one of hello following licenses assigned in your tenant.</span></span>

* <span data-ttu-id="84008-111">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="84008-111">Azure AD Premium P1</span></span>
* <span data-ttu-id="84008-112">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="84008-112">Azure AD Premium P2</span></span>
* <span data-ttu-id="84008-113">Enterprise Mobility + Security E3</span><span class="sxs-lookup"><span data-stu-id="84008-113">Enterprise Mobility + Security E3</span></span>
* <span data-ttu-id="84008-114">Enterprise Mobility + Security E5</span><span class="sxs-lookup"><span data-stu-id="84008-114">Enterprise Mobility + Security E5</span></span>
* <span data-ttu-id="84008-115">Secure Productive Enterprise E3</span><span class="sxs-lookup"><span data-stu-id="84008-115">Secure Productive Enterprise E3</span></span>
* <span data-ttu-id="84008-116">Secure Productive Enterprise E5</span><span class="sxs-lookup"><span data-stu-id="84008-116">Secure Productive Enterprise E5</span></span>

> [!NOTE]
> <span data-ttu-id="84008-117">독립 실행형 Office 365 라이선스 계획 **암호 쓰기 저장을 지원 하지 않는** hello 앞에이 기능 toowork에 대 한 계획 중 하나 필요로 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84008-117">Standalone Office 365 licensing plans **do not support password writeback** and require one of hello preceding plans for this functionality toowork.</span></span>

<span data-ttu-id="84008-118">다음 페이지 hello에서 비용을 포함 하는 추가 라이선스 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84008-118">Additional licensing info including costs can be found on hello following pages</span></span>

* [<span data-ttu-id="84008-119">Azure Active Directory 가격 책정 사이트</span><span class="sxs-lookup"><span data-stu-id="84008-119">Azure Active Directory Pricing site</span></span>](https://azure.microsoft.com/pricing/details/active-directory/)
* [<span data-ttu-id="84008-120">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="84008-120">Enterprise Mobility + Security</span></span>](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [<span data-ttu-id="84008-121">Secure Productive Enterprise</span><span class="sxs-lookup"><span data-stu-id="84008-121">Secure Productive Enterprise</span></span>](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

## <a name="enable-group-or-user-based-licensing"></a><span data-ttu-id="84008-122">그룹 또는 사용자 기반 라이선스 사용</span><span class="sxs-lookup"><span data-stu-id="84008-122">Enable group or user-based licensing</span></span>

<span data-ttu-id="84008-123">Azure AD는 이제 그룹 기반의 라이선스 수 있도록 관리자 tooassign 라이선스 대량 tooa 사용자 그룹에 보다는 한 번에 하나씩 할당을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="84008-123">Azure AD now supports group-based licensing allowing administrators tooassign licenses in bulk tooa group of users, rather than assigning them one at a time.</span></span> [<span data-ttu-id="84008-124">라이선스 할당, 확인 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="84008-124">Assign, verify, and resolve problems with licenses</span></span>](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)

<span data-ttu-id="84008-125">일부 Microsoft 서비스는 모든 위치에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="84008-125">Some Microsoft services are not available in all locations.</span></span> <span data-ttu-id="84008-126">Tooa 사용자 라이선스를 할당할 수 있습니다, 전에 관리자에 게 hello 사용자에 hello "사용 위치" 속성을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84008-126">Before a license can be assigned tooa user, hello administrator must specify hello “Usage location” property on hello user.</span></span> <span data-ttu-id="84008-127">사용자 라이선스 할당을 수행할 수 있습니다 > 프로필 > hello Azure 포털의에서 설정 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="84008-127">Assignment of licenses can be done under User > Profile > Settings section in hello Azure portal.</span></span> <span data-ttu-id="84008-128">**그룹 라이선스 할당을 사용할 경우 사용 위치를 지정 하지 않고 모든 사용자는 hello 디렉터리의 hello 위치를 상속 합니다.**</span><span class="sxs-lookup"><span data-stu-id="84008-128">**When using group license assignment, any users without a usage location specified inherit hello location of hello directory.**</span></span>

## <a name="next-steps"></a><span data-ttu-id="84008-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="84008-129">Next steps</span></span>

<span data-ttu-id="84008-130">링크를 따라 hello Azure AD를 사용 하 여 다시 설정 하는 암호에 대 한 추가 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="84008-130">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="84008-131">[**빠른 시작**](active-directory-passwords-getting-started.md) - Azure AD 셀프 서비스 암호 관리를 사용하여 운영 시작</span><span class="sxs-lookup"><span data-stu-id="84008-131">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="84008-132">[**데이터** ](active-directory-passwords-data.md) -hello 필요한 데이터를 이해 하 고 암호 관리에 대 한 사용 방법</span><span class="sxs-lookup"><span data-stu-id="84008-132">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="84008-133">[**롤아웃** ](active-directory-passwords-best-practices.md) -계획 및 배포 ´ ֿ ´ hello 지침을 사용 하 여 SSPR tooyour 사용자</span><span class="sxs-lookup"><span data-stu-id="84008-133">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="84008-134">[**사용자 지정** ](active-directory-passwords-customize.md) -hello SSPR 귀사에 대 한 경험의 hello 모양과 느낌을 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="84008-134">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="84008-135">[**보고**](active-directory-passwords-reporting.md) - 사용자가 SSPR 기능에 액세스하는 조건, 시간 및 위치 탐색</span><span class="sxs-lookup"><span data-stu-id="84008-135">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="84008-136">[**기술 심층 분석** ](active-directory-passwords-how-it-works.md) -이동 hello 커튼 toounderstand 뒤 작동 방법</span><span class="sxs-lookup"><span data-stu-id="84008-136">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="84008-137">[**질문과 대답**](active-directory-passwords-faq.md) - 어떤 방식으로?</span><span class="sxs-lookup"><span data-stu-id="84008-137">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="84008-138">그 이유는</span><span class="sxs-lookup"><span data-stu-id="84008-138">Why?</span></span> <span data-ttu-id="84008-139">무엇을?</span><span class="sxs-lookup"><span data-stu-id="84008-139">What?</span></span> <span data-ttu-id="84008-140">어디서?</span><span class="sxs-lookup"><span data-stu-id="84008-140">Where?</span></span> <span data-ttu-id="84008-141">누가?</span><span class="sxs-lookup"><span data-stu-id="84008-141">Who?</span></span> <span data-ttu-id="84008-142">언제?</span><span class="sxs-lookup"><span data-stu-id="84008-142">When?</span></span> <span data-ttu-id="84008-143">-Tooask 항상 필요한 tooquestions 답변</span><span class="sxs-lookup"><span data-stu-id="84008-143">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="84008-144">[**문제를 해결** ](active-directory-passwords-troubleshoot.md) -SSPR으로 보면 tooresolve 공통을 발급 하는 방법에 대해 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="84008-144">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>

