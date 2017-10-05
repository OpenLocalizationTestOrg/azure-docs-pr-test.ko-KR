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
ms.openlocfilehash: 936134bddad19964f809a17f200ebbeed5aa853c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a><span data-ttu-id="f501a-103">Azure AD 셀프 서비스 암호 재설정의 라이선스 요구 사항</span><span class="sxs-lookup"><span data-stu-id="f501a-103">Licensing requirements for Azure AD self-service password reset</span></span>

<span data-ttu-id="f501a-104">Azure AD 암호 재설정의 기능을 작동하려면 **조직에서 할당된 하나 이상의 라이선스가 있어야 합니다**.</span><span class="sxs-lookup"><span data-stu-id="f501a-104">In order for Azure AD Password Reset to function, you **must have at least one license assigned in your organization**.</span></span> <span data-ttu-id="f501a-105">암호 재설정 환경에서 사용자별 라이선스를 적용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f501a-105">We do not enforce per-user licensing on the password reset experience.</span></span> <span data-ttu-id="f501a-106">Microsoft 라이선스 규약을 준수하려면 프리미엄 기능을 사용하는 모든 사용자에게 라이선스를 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f501a-106">To maintain compliance with your Microsoft licensing agreement, you need to assign licenses to any users that use premium features.</span></span>

* <span data-ttu-id="f501a-107">**클라우드 사용자만 해당** - Office 365(O365) 유료 SKU 또는 Azure AD Basic</span><span class="sxs-lookup"><span data-stu-id="f501a-107">**Cloud only users** - Office 365 (O365) any paid SKU, or Azure AD Basic</span></span>
* <span data-ttu-id="f501a-108">**클라우드** 및/또는 **온-프레미스 사용자** - Azure AD Premium P1 또는 P2, EMS(Enterprise Mobility + Security) 또는 SPE(Secure Productive Enterprise)</span><span class="sxs-lookup"><span data-stu-id="f501a-108">**Cloud** and/or **on-premises users** - Azure AD Premium P1 or P2, Enterprise Mobility + Security (EMS), or Secure Productive Enterprise (SPE)</span></span>

## <a name="licenses-required-for-password-writeback"></a><span data-ttu-id="f501a-109">비밀번호 쓰기 저장에 필요한 라이선스</span><span class="sxs-lookup"><span data-stu-id="f501a-109">Licenses required for password writeback</span></span>

<span data-ttu-id="f501a-110">비밀번호 쓰기 저장을 사용하려면 다음 라이선스 중 하나를 테넌트에 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f501a-110">To use password writeback, you must have one of the following licenses assigned in your tenant.</span></span>

* <span data-ttu-id="f501a-111">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="f501a-111">Azure AD Premium P1</span></span>
* <span data-ttu-id="f501a-112">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="f501a-112">Azure AD Premium P2</span></span>
* <span data-ttu-id="f501a-113">Enterprise Mobility + Security E3</span><span class="sxs-lookup"><span data-stu-id="f501a-113">Enterprise Mobility + Security E3</span></span>
* <span data-ttu-id="f501a-114">Enterprise Mobility + Security E5</span><span class="sxs-lookup"><span data-stu-id="f501a-114">Enterprise Mobility + Security E5</span></span>
* <span data-ttu-id="f501a-115">Secure Productive Enterprise E3</span><span class="sxs-lookup"><span data-stu-id="f501a-115">Secure Productive Enterprise E3</span></span>
* <span data-ttu-id="f501a-116">Secure Productive Enterprise E5</span><span class="sxs-lookup"><span data-stu-id="f501a-116">Secure Productive Enterprise E5</span></span>

> [!NOTE]
> <span data-ttu-id="f501a-117">독립 실행형 Office 365 라이선스 계획은 **비밀번호 쓰기 저장을 지원하지 않습니다**. 따라서 이 기능을 작동시키기 위해 이전 계획 중 하나가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f501a-117">Standalone Office 365 licensing plans **do not support password writeback** and require one of the preceding plans for this functionality to work.</span></span>

<span data-ttu-id="f501a-118">다음 페이지에서는 라이선스 비용을 포함한 추가 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f501a-118">Additional licensing info including costs can be found on the following pages</span></span>

* [<span data-ttu-id="f501a-119">Azure Active Directory 가격 책정 사이트</span><span class="sxs-lookup"><span data-stu-id="f501a-119">Azure Active Directory Pricing site</span></span>](https://azure.microsoft.com/pricing/details/active-directory/)
* [<span data-ttu-id="f501a-120">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="f501a-120">Enterprise Mobility + Security</span></span>](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [<span data-ttu-id="f501a-121">Secure Productive Enterprise</span><span class="sxs-lookup"><span data-stu-id="f501a-121">Secure Productive Enterprise</span></span>](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

## <a name="enable-group-or-user-based-licensing"></a><span data-ttu-id="f501a-122">그룹 또는 사용자 기반 라이선스 사용</span><span class="sxs-lookup"><span data-stu-id="f501a-122">Enable group or user-based licensing</span></span>

<span data-ttu-id="f501a-123">이제 Azure AD는 관리자가 사용자 그룹에 대량으로 라이선스를 할당하지 않고 한 번에 하나씩 할당하는 그룹 기반 라이선스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f501a-123">Azure AD now supports group-based licensing allowing administrators to assign licenses in bulk to a group of users, rather than assigning them one at a time.</span></span> [<span data-ttu-id="f501a-124">라이선스 할당, 확인 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="f501a-124">Assign, verify, and resolve problems with licenses</span></span>](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)

<span data-ttu-id="f501a-125">일부 Microsoft 서비스는 모든 위치에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f501a-125">Some Microsoft services are not available in all locations.</span></span> <span data-ttu-id="f501a-126">사용자에게 라이선스를 할당하려면 먼저 관리자가 해당 사용자에 대해 “사용 위치” 속성을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f501a-126">Before a license can be assigned to a user, the administrator must specify the “Usage location” property on the user.</span></span> <span data-ttu-id="f501a-127">라이선스의 할당은 Azure Portal의 [사용자 > 프로필 > 설정]에서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f501a-127">Assignment of licenses can be done under User > Profile > Settings section in the Azure portal.</span></span> <span data-ttu-id="f501a-128">**그룹 라이선스 할당을 사용할 때 사용 위치가 지정되지 않은 사용자는 디렉터리의 위치를 상속합니다.**</span><span class="sxs-lookup"><span data-stu-id="f501a-128">**When using group license assignment, any users without a usage location specified inherit the location of the directory.**</span></span>

## <a name="next-steps"></a><span data-ttu-id="f501a-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f501a-129">Next steps</span></span>

<span data-ttu-id="f501a-130">다음 링크는 Azure AD를 사용한 암호 재설정에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f501a-130">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="f501a-131">[**빠른 시작**](active-directory-passwords-getting-started.md) - Azure AD 셀프 서비스 암호 관리를 사용하여 운영 시작</span><span class="sxs-lookup"><span data-stu-id="f501a-131">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="f501a-132">[**데이터**](active-directory-passwords-data.md) - 암호 관리에 필요한 데이터 및 사용 방식을 이해</span><span class="sxs-lookup"><span data-stu-id="f501a-132">[**Data**](active-directory-passwords-data.md) - Understand the data that is required and how it is used for password management</span></span>
* <span data-ttu-id="f501a-133">[**롤아웃**](active-directory-passwords-best-practices.md) - 여기서 제공하는 지침을 사용하여 배포 계획을 세우고 사용자에게 SSPR 배포</span><span class="sxs-lookup"><span data-stu-id="f501a-133">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="f501a-134">[**사용자 지정**](active-directory-passwords-customize.md) - 회사 SSPR 경험의 모양과 느낌을 사용자 지정.</span><span class="sxs-lookup"><span data-stu-id="f501a-134">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="f501a-135">[**보고**](active-directory-passwords-reporting.md) - 사용자가 SSPR 기능에 액세스하는 조건, 시간 및 위치 탐색</span><span class="sxs-lookup"><span data-stu-id="f501a-135">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="f501a-136">[**기술 심층 분석**](active-directory-passwords-how-it-works.md) - 작동 방식을 이해하기 위해 심층 분석</span><span class="sxs-lookup"><span data-stu-id="f501a-136">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="f501a-137">[**질문과 대답**](active-directory-passwords-faq.md) - 어떤 방식으로?</span><span class="sxs-lookup"><span data-stu-id="f501a-137">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="f501a-138">그 이유는</span><span class="sxs-lookup"><span data-stu-id="f501a-138">Why?</span></span> <span data-ttu-id="f501a-139">무엇을?</span><span class="sxs-lookup"><span data-stu-id="f501a-139">What?</span></span> <span data-ttu-id="f501a-140">어디서?</span><span class="sxs-lookup"><span data-stu-id="f501a-140">Where?</span></span> <span data-ttu-id="f501a-141">누가?</span><span class="sxs-lookup"><span data-stu-id="f501a-141">Who?</span></span> <span data-ttu-id="f501a-142">언제?</span><span class="sxs-lookup"><span data-stu-id="f501a-142">When?</span></span> <span data-ttu-id="f501a-143">- 많은 분들이 항상 묻는 질문에 대한 답변입니다.</span><span class="sxs-lookup"><span data-stu-id="f501a-143">- Answers to questions you always wanted to ask</span></span>
* <span data-ttu-id="f501a-144">[**문제 해결**](active-directory-passwords-troubleshoot.md) - SSPR의 일반적인 문제 해결 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="f501a-144">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>

