---
title: "aaaAzure AD 셀프 서비스 암호 재설정 개요 | Microsoft Docs"
description: "Azure AD의 셀프 서비스 암호 재설정이 조직에서 어떤 작업을 수행할 수 있나요?"
services: active-directory
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
ms.openlocfilehash: 0efc291b1eeec0b7ae33ff5a7d9ed38e70c8be6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-self-service-password-reset-for-hello-it-professional"></a><span data-ttu-id="46b83-103">IT 전문가 hello에 대 한 azure AD 셀프 서비스 암호 재설정</span><span class="sxs-lookup"><span data-stu-id="46b83-103">Azure AD self-service password reset for hello IT professional</span></span>

<span data-ttu-id="46b83-104">내에서 throw 주위 많은 IT 부서에서 다양 한 의미를 사용 하는 hello world 용어가 "셀프 서비스"입니다.</span><span class="sxs-lookup"><span data-stu-id="46b83-104">"Self-service" is a buzzword thrown around inside many IT departments across hello world with varying meanings.</span></span> <span data-ttu-id="46b83-105">hello 시장 toomanage 온-프레미스 그룹, 암호 또는 hello 클라우드 또는 온-프레미스에서 사용자 프로필 수 있는 제품과 서비스 장애 유발입니다.</span><span class="sxs-lookup"><span data-stu-id="46b83-105">hello market is flooded with products that allow you toomanage on-premises groups, passwords, or user profiles from hello cloud or on-premises.</span></span>

<span data-ttu-id="46b83-106">Azure Active Directory(Azure AD) SSPR(셀프 서비스 암호 재설정)은 사용 및 배포 편의로부터 분리됩니다.</span><span class="sxs-lookup"><span data-stu-id="46b83-106">Azure Active Directory (Azure AD) self-service password reset (SSPR) sets itself apart with ease of use and deployment.</span></span> <span data-ttu-id="46b83-107">Azure AD 셀프 서비스 암호 재설정은 다음과 같은 일련의 기능을 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="46b83-107">Azure AD self-service password reset combines a set of capabilities that:</span></span>

* <span data-ttu-id="46b83-108">사용자가 toomanage 자신의 암호 허용</span><span class="sxs-lookup"><span data-stu-id="46b83-108">Allow your users toomanage their own password</span></span>
  * <span data-ttu-id="46b83-109">어떤 장치든지</span><span class="sxs-lookup"><span data-stu-id="46b83-109">From any device</span></span>
  * <span data-ttu-id="46b83-110">어디에서든지</span><span class="sxs-lookup"><span data-stu-id="46b83-110">In any location</span></span>
  * <span data-ttu-id="46b83-111">언제든지</span><span class="sxs-lookup"><span data-stu-id="46b83-111">At any time</span></span>
* <span data-ttu-id="46b83-112">관리자 권한으로 정의한 정책을 준수하여 관리할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46b83-112">Maintain compliance with policies you as an administrator define</span></span>

<span data-ttu-id="46b83-113">준비를 마쳤다면 [빠른 시작 설명서](active-directory-passwords-getting-started.md)를 사용하여 Azure AD SSPR을 시작하고 사용자가 자신의 고유한 암호를 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46b83-113">If you are ready, you can get started with Azure AD SSPR using our [quick start guidance](active-directory-passwords-getting-started.md) and quickly have your users resetting their own passwords.</span></span>

## <a name="what-is-possible"></a><span data-ttu-id="46b83-114">가능한 기능</span><span class="sxs-lookup"><span data-stu-id="46b83-114">What is possible</span></span>

* <span data-ttu-id="46b83-115">**셀프 서비스 암호 변경** 최종 사용자나 관리자가 toochange 관리자의 도움 없이 암호 허용</span><span class="sxs-lookup"><span data-stu-id="46b83-115">**Self-service password change** allows end users or administrators toochange their passwords without administrator assistance</span></span>
* <span data-ttu-id="46b83-116">**셀프 서비스 계정 잠금 해제** 최종 사용자가 toounlock 관리자의 도움 없이 자신의 계정 허용</span><span class="sxs-lookup"><span data-stu-id="46b83-116">**Self-service account unlock** allows end users toounlock their own account without administrator assistance</span></span>
* <span data-ttu-id="46b83-117">**셀프 서비스 암호 재설정** 최종 사용자나 관리자가 tooreset 관리자의 도움 없이 자동으로 해당 암호를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b83-117">**Self-service password reset** allows end users or administrators tooreset their passwords automatically without administrator assistance.</span></span> <span data-ttu-id="46b83-118">셀프 서비스 암호 재설정 기능을 사용하려면 Azure AD Premium 또는 Basic - [Azure Active Directory 버전](active-directory-editions.md)이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="46b83-118">Self-service password reset requires Azure AD Premium or Basic - [Azure Active Directory Editions](active-directory-editions.md).</span></span>
* <span data-ttu-id="46b83-119">**관리자 시작한 암호 재설정** 관리자 tooreset hello 내에서 다른 관리자 또는 최종 사용자의 암호를 사용 하면 [Azure 포털](https://docs.microsoft.com/azure/azure-portal-overview)</span><span class="sxs-lookup"><span data-stu-id="46b83-119">**Administrator-initiated password reset** allows an administrator tooreset an end user’s or another administrator’s password from within hello [Azure portal](https://docs.microsoft.com/azure/azure-portal-overview)</span></span>
* <span data-ttu-id="46b83-120">**암호 관리 작업 보고서**는 조직에서 발생하는 암호 재설정 및 등록 작업에서의 관리자 이해도를 높여줍니다. [관리 보고서](active-directory-passwords-reporting.md)</span><span class="sxs-lookup"><span data-stu-id="46b83-120">**Password management activity reports** give administrators insights into password reset and registration activity occurring in their organization - [Management reports](active-directory-passwords-reporting.md)</span></span>
* <span data-ttu-id="46b83-121">**암호 쓰기 저장** 모든 hello 앞에 있는 by 또는 hello 대신 하 여 시나리오를 수행할 수 있습니다 페더레이션 또는 암호 동기화 사용자가 있으므로 hello 클라우드에서 온-프레미스 암호도 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46b83-121">**Password Writeback** allows management of on-premises passwords from hello cloud so all hello preceeding scenarios can be performed by, or on hello behalf of, federated or password synchronized users.</span></span> <span data-ttu-id="46b83-122">비밀번호 쓰기 저장을 사용하려면 [Azure AD Premium](active-directory-get-started-premium.md)이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="46b83-122">Password Writeback requires [Azure AD Premium](active-directory-get-started-premium.md).</span></span>

## <a name="why-choose-azure-ad-self-service-password-reset"></a><span data-ttu-id="46b83-123">Azure AD 셀프 서비스 암호 재설정을 선택하는 이유</span><span class="sxs-lookup"><span data-stu-id="46b83-123">Why choose Azure AD self-service password reset</span></span>

* <span data-ttu-id="46b83-124">**비용 절감** 기술 지원팀의 지원 기반 암호 재설정은 일반적으로 IT 조직 지출의 20%입니다.</span><span class="sxs-lookup"><span data-stu-id="46b83-124">**Reduce costs** as helpdesk and support assisted password reset is typically 20% of an IT organization’s spend</span></span>
* <span data-ttu-id="46b83-125">**최종 사용자 환경을 개선 하기 위해** 및 **기술 지원팀 량을 줄이는** 제공 하 여 최종 사용자가 hello 전원 tooresolve 자신의 암호 문제가 한 번에 기술 지원팀에 연락 하거나 지원 요청을 열지 않고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b83-125">**Improve end-user experiences** and **reduce helpdesk volume** by giving end users hello power tooresolve their own password issues at once without calling a helpdesk or opening a support request.</span></span>
* <span data-ttu-id="46b83-126">**이동성 공급** - 사용자가 어디에서든 암호를 재설정할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="46b83-126">**Drive mobility** as users can reset their passwords from wherever they are.</span></span>

## <a name="azure-ad-self-service-password-reset-availability"></a><span data-ttu-id="46b83-127">Azure AD 셀프 서비스 암호 재설정 가용성</span><span class="sxs-lookup"><span data-stu-id="46b83-127">Azure AD self-service password reset availability</span></span>

<span data-ttu-id="46b83-128">Azure AD 셀프 서비스 암호 재설정은 구독에 따라 세 가지 계층으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="46b83-128">Azure AD self-service password reset is available in three tiers depending on your subscription.</span></span>

* <span data-ttu-id="46b83-129">**Azure AD Free** - 클라우드 전용 관리자는 해당하는 고유한 암호를 재설정할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="46b83-129">**Azure AD Free** – Cloud-only administrators can reset their own passwords</span></span>
* <span data-ttu-id="46b83-130">**Azure AD 기본** 또는 **유료 Office 365 구독** - 클라우드 전용 사용자 및 클라우드 전용 관리자는 해당하는 고유한 암호를 재설정할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="46b83-130">**Azure AD Basic** or any **Paid Office 365 Subscription** – Cloud-only users and cloud-only administrators can reset their own passwords</span></span>
* <span data-ttu-id="46b83-131">**Azure AD Premium** - 사용자 또는 관리자는 클라우드 전용, 페더레이션된 또는 암호 동기화된 사용자를 포함하여 해당하는 고유한 암호를 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46b83-131">**Azure AD Premium** – Any user or administrator, including cloud-only, federated, or password synchronized users, can reset their own passwords.</span></span> <span data-ttu-id="46b83-132">온-프레미스 암호는 암호 쓰기 저장 toobe 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b83-132">On-premises passwords require password writeback toobe enabled.</span></span>

## <a name="azure-ad-self-service-password-reset-a-sum-of-hello-parts"></a><span data-ttu-id="46b83-133">Azure AD 셀프 서비스 암호 재설정 hello 파트의 합계</span><span class="sxs-lookup"><span data-stu-id="46b83-133">Azure AD self-service password reset, a sum of hello parts</span></span>

<span data-ttu-id="46b83-134">셀프 서비스 암호 재설정 Azure AD에서 다음과 같은 구성 요소가 hello 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46b83-134">Self-service password reset in Azure AD is made up of hello following components:</span></span>

* <span data-ttu-id="46b83-135">**암호 관리 구성 포털** hello Azure 포털을 통해 테 넌 트의 암호를 관리 하는 방법에 대 한 옵션을 제어할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="46b83-135">**Password management configuration portal** where you can control options for how passwords are managed in your tenant via hello Azure portal</span></span>
* <span data-ttu-id="46b83-136">**암호 재설정 등록 포털** 사용자가 암호 재설정을 자동 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46b83-136">**Password reset registration portal** where users can self-register for password reset</span></span>
* <span data-ttu-id="46b83-137">**암호 재설정 포털** 여기서 사용자가 관리자에 게에 정의 된 hello 과제를 사용 하 여 자신의 암호를 재설정할 수 하 고 hello 응답 사용자가 제공한</span><span class="sxs-lookup"><span data-stu-id="46b83-137">**Password reset portal** where users can reset their password using hello challenges defined by hello administrator and hello answers users have provided</span></span>
* <span data-ttu-id="46b83-138">**사용자 암호 변경 포털** 사용자는 이전 암호를 입력하고 새 암호를 제공하여 자신의 암호를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46b83-138">**User password change portal** where users can change their own passwords by entering their old password and providing a new password</span></span>
* <span data-ttu-id="46b83-139">**암호 관리 보고서** hello Azure 포털에서에서 해당 테 넌 트에 대 한 관리자가 보고 하 고 암호 활동 분석할 수 있는 보고서</span><span class="sxs-lookup"><span data-stu-id="46b83-139">**Password management reports** where administrators can view and analyze password activity reports for their tenants in hello Azure portal</span></span>
* <span data-ttu-id="46b83-140">**Azure AD Connect를 사용 하 여 암호 쓰기 저장 tooon 프레미스** 관리할 수 있게 하면 tooenable 온-프레미스와 페더레이션 또는 암호 동기화 사용자가 hello 클라우드에서</span><span class="sxs-lookup"><span data-stu-id="46b83-140">**Password writeback tooon-premises using Azure AD Connect** allows you tooenable management of on-premises, federated, or password synchronized users from hello cloud</span></span>

## <a name="azure-ad-pricing-sla-updates-and-roadmap"></a><span data-ttu-id="46b83-141">Azure AD 가격 책정, SLA, 업데이트 및 로드맵</span><span class="sxs-lookup"><span data-stu-id="46b83-141">Azure AD pricing, SLA, updates, and roadmap</span></span>

<span data-ttu-id="46b83-142">Hello 다음 페이지에서 이러한 항목에 대 한 자세한 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46b83-142">More detail about these topics can be found on hello following pages</span></span>

* [<span data-ttu-id="46b83-143">**Azure AD 가격 책정 정보**</span><span class="sxs-lookup"><span data-stu-id="46b83-143">**Azure AD Pricing Details**</span></span>](https://azure.microsoft.com/pricing/details/active-directory/)
* [<span data-ttu-id="46b83-144">**Office 365 가격 책정**</span><span class="sxs-lookup"><span data-stu-id="46b83-144">**Office 365 Pricing**</span></span>](https://products.office.com/compare-all-microsoft-office-products?tab=2)
* [<span data-ttu-id="46b83-145">**Azure Service Level Agreements(서비스 수준 약정)**</span><span class="sxs-lookup"><span data-stu-id="46b83-145">**Azure Service Level Agreements**</span></span>](https://azure.microsoft.com/support/legal/sla/)
* [<span data-ttu-id="46b83-146">**Microsoft 온라인 서비스에 대한 Service Level Agreements(서비스 수준 약정)**</span><span class="sxs-lookup"><span data-stu-id="46b83-146">**Service Level Agreement for Microsoft Online Services**</span></span>](http://go.microsoft.com/fwlink/?LinkID=272026&clcid=0x409)
* [<span data-ttu-id="46b83-147">**Azure 업데이트**</span><span class="sxs-lookup"><span data-stu-id="46b83-147">**Azure Updates**</span></span>](https://azure.microsoft.com/updates/)
* [<span data-ttu-id="46b83-148">**Azure 로드맵**</span><span class="sxs-lookup"><span data-stu-id="46b83-148">**Azure Roadmap**</span></span>](https://www.microsoft.com/cloud-platform/roadmap-recently-available)

## <a name="next-steps"></a><span data-ttu-id="46b83-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="46b83-149">Next steps</span></span>

<span data-ttu-id="46b83-150">링크를 따라 hello Azure AD를 사용 하 여 다시 설정 하는 암호에 대 한 추가 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b83-150">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="46b83-151">[**빠른 시작**](active-directory-passwords-getting-started.md) - Azure AD 셀프 서비스 암호 관리를 사용하여 운영 시작</span><span class="sxs-lookup"><span data-stu-id="46b83-151">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="46b83-152">[**라이선스**](active-directory-passwords-licensing.md) - Azure AD 라이선스 구성</span><span class="sxs-lookup"><span data-stu-id="46b83-152">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="46b83-153">[**데이터** ](active-directory-passwords-data.md) -hello 필요한 데이터를 이해 하 고 암호 관리에 대 한 사용 방법</span><span class="sxs-lookup"><span data-stu-id="46b83-153">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="46b83-154">[**롤아웃** ](active-directory-passwords-best-practices.md) -계획 및 배포 ´ ֿ ´ hello 지침을 사용 하 여 SSPR tooyour 사용자</span><span class="sxs-lookup"><span data-stu-id="46b83-154">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="46b83-155">[**사용자 지정** ](active-directory-passwords-customize.md) -hello SSPR 귀사에 대 한 경험의 hello 모양과 느낌을 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="46b83-155">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="46b83-156">[**보고**](active-directory-passwords-reporting.md) - 사용자가 SSPR 기능에 액세스하는 조건, 시간 및 위치 탐색</span><span class="sxs-lookup"><span data-stu-id="46b83-156">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="46b83-157">[**기술 심층 분석** ](active-directory-passwords-how-it-works.md) -이동 hello 커튼 toounderstand 뒤 작동 방법</span><span class="sxs-lookup"><span data-stu-id="46b83-157">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="46b83-158">[**질문과 대답**](active-directory-passwords-faq.md) - 어떤 방식으로?</span><span class="sxs-lookup"><span data-stu-id="46b83-158">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="46b83-159">그 이유는</span><span class="sxs-lookup"><span data-stu-id="46b83-159">Why?</span></span> <span data-ttu-id="46b83-160">무엇을?</span><span class="sxs-lookup"><span data-stu-id="46b83-160">What?</span></span> <span data-ttu-id="46b83-161">어디서?</span><span class="sxs-lookup"><span data-stu-id="46b83-161">Where?</span></span> <span data-ttu-id="46b83-162">누가?</span><span class="sxs-lookup"><span data-stu-id="46b83-162">Who?</span></span> <span data-ttu-id="46b83-163">언제?</span><span class="sxs-lookup"><span data-stu-id="46b83-163">When?</span></span> <span data-ttu-id="46b83-164">-Tooask 항상 필요한 tooquestions 답변</span><span class="sxs-lookup"><span data-stu-id="46b83-164">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="46b83-165">[**문제를 해결** ](active-directory-passwords-troubleshoot.md) -SSPR으로 보면 tooresolve 공통을 발급 하는 방법에 대해 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="46b83-165">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>

