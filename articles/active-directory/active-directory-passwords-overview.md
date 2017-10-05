---
title: "Azure AD 셀프 서비스 암호 재설정 개요 | Microsoft Docs"
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
ms.openlocfilehash: 3903c53b78e61b380bb812a9d3ade694655b5afb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-self-service-password-reset-for-the-it-professional"></a><span data-ttu-id="b5ba3-103">IT 전문가를 위한 Azure AD 셀프 서비스 암호 재설정</span><span class="sxs-lookup"><span data-stu-id="b5ba3-103">Azure AD self-service password reset for the IT professional</span></span>

<span data-ttu-id="b5ba3-104">"셀프 서비스"는 전 세계의 많은 IT 부서 내부에서 throw되는 다양한 의미를 가진 용어입니다.</span><span class="sxs-lookup"><span data-stu-id="b5ba3-104">"Self-service" is a buzzword thrown around inside many IT departments across the world with varying meanings.</span></span> <span data-ttu-id="b5ba3-105">시장은 클라우드 또는 온-프레미스에서 온-프레미스 그룹, 암호 또는 사용자 프로필을 관리할 수 있는 제품으로 넘쳐납니다.</span><span class="sxs-lookup"><span data-stu-id="b5ba3-105">The market is flooded with products that allow you to manage on-premises groups, passwords, or user profiles from the cloud or on-premises.</span></span>

<span data-ttu-id="b5ba3-106">Azure Active Directory(Azure AD) SSPR(셀프 서비스 암호 재설정)은 사용 및 배포 편의로부터 분리됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5ba3-106">Azure Active Directory (Azure AD) self-service password reset (SSPR) sets itself apart with ease of use and deployment.</span></span> <span data-ttu-id="b5ba3-107">Azure AD 셀프 서비스 암호 재설정은 다음과 같은 일련의 기능을 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="b5ba3-107">Azure AD self-service password reset combines a set of capabilities that:</span></span>

* <span data-ttu-id="b5ba3-108">사용자가 자신의 암호를</span><span class="sxs-lookup"><span data-stu-id="b5ba3-108">Allow your users to manage their own password</span></span>
  * <span data-ttu-id="b5ba3-109">어떤 장치든지</span><span class="sxs-lookup"><span data-stu-id="b5ba3-109">From any device</span></span>
  * <span data-ttu-id="b5ba3-110">어디에서든지</span><span class="sxs-lookup"><span data-stu-id="b5ba3-110">In any location</span></span>
  * <span data-ttu-id="b5ba3-111">언제든지</span><span class="sxs-lookup"><span data-stu-id="b5ba3-111">At any time</span></span>
* <span data-ttu-id="b5ba3-112">관리자 권한으로 정의한 정책을 준수하여 관리할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5ba3-112">Maintain compliance with policies you as an administrator define</span></span>

<span data-ttu-id="b5ba3-113">준비를 마쳤다면 [빠른 시작 설명서](active-directory-passwords-getting-started.md)를 사용하여 Azure AD SSPR을 시작하고 사용자가 자신의 고유한 암호를 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5ba3-113">If you are ready, you can get started with Azure AD SSPR using our [quick start guidance](active-directory-passwords-getting-started.md) and quickly have your users resetting their own passwords.</span></span>

## <a name="what-is-possible"></a><span data-ttu-id="b5ba3-114">가능한 기능</span><span class="sxs-lookup"><span data-stu-id="b5ba3-114">What is possible</span></span>

* <span data-ttu-id="b5ba3-115">**셀프 서비스 암호 변경**을 사용하면 최종 사용자나 관리자가 관리자의 도움 없이 자신의 암호를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5ba3-115">**Self-service password change** allows end users or administrators to change their passwords without administrator assistance</span></span>
* <span data-ttu-id="b5ba3-116">**셀프 서비스 계정 잠금 해제**를 사용하면 최종 사용자가 관리자의 도움 없이 자신의 계정의 잠금을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5ba3-116">**Self-service account unlock** allows end users to unlock their own account without administrator assistance</span></span>
* <span data-ttu-id="b5ba3-117">**셀프 서비스 암호 재설정**을 사용하면 최종 사용자나 관리자는 관리자의 도움 없이 자신의 암호를 자동으로 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5ba3-117">**Self-service password reset** allows end users or administrators to reset their passwords automatically without administrator assistance.</span></span> <span data-ttu-id="b5ba3-118">셀프 서비스 암호 재설정 기능을 사용하려면 Azure AD Premium 또는 Basic - [Azure Active Directory 버전](active-directory-editions.md)이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b5ba3-118">Self-service password reset requires Azure AD Premium or Basic - [Azure Active Directory Editions](active-directory-editions.md).</span></span>
* <span data-ttu-id="b5ba3-119">**관리자가 시작한 암호 재설정** 기능을 사용하여 관리자는 [Azure Portal](https://docs.microsoft.com/azure/azure-portal-overview) 내에서 최종 사용자나 다른 관리자의 암호를 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5ba3-119">**Administrator-initiated password reset** allows an administrator to reset an end user’s or another administrator’s password from within the [Azure portal](https://docs.microsoft.com/azure/azure-portal-overview)</span></span>
* <span data-ttu-id="b5ba3-120">**암호 관리 작업 보고서**는 조직에서 발생하는 암호 재설정 및 등록 작업에서의 관리자 이해도를 높여줍니다. [관리 보고서](active-directory-passwords-reporting.md)</span><span class="sxs-lookup"><span data-stu-id="b5ba3-120">**Password management activity reports** give administrators insights into password reset and registration activity occurring in their organization - [Management reports](active-directory-passwords-reporting.md)</span></span>
* <span data-ttu-id="b5ba3-121">**비밀번호 쓰기 저장**을 사용하면 클라우드에서 온-프레미스 암호를 관리할 수 있으므로 이전의 모든 시나리오에서 수행되거나 페더레이션 및 암호가 동기화된 사용자가 대신 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5ba3-121">**Password Writeback** allows management of on-premises passwords from the cloud so all the preceeding scenarios can be performed by, or on the behalf of, federated or password synchronized users.</span></span> <span data-ttu-id="b5ba3-122">비밀번호 쓰기 저장을 사용하려면 [Azure AD Premium](active-directory-get-started-premium.md)이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b5ba3-122">Password Writeback requires [Azure AD Premium](active-directory-get-started-premium.md).</span></span>

## <a name="why-choose-azure-ad-self-service-password-reset"></a><span data-ttu-id="b5ba3-123">Azure AD 셀프 서비스 암호 재설정을 선택하는 이유</span><span class="sxs-lookup"><span data-stu-id="b5ba3-123">Why choose Azure AD self-service password reset</span></span>

* <span data-ttu-id="b5ba3-124">**비용 절감** 기술 지원팀의 지원 기반 암호 재설정은 일반적으로 IT 조직 지출의 20%입니다.</span><span class="sxs-lookup"><span data-stu-id="b5ba3-124">**Reduce costs** as helpdesk and support assisted password reset is typically 20% of an IT organization’s spend</span></span>
* <span data-ttu-id="b5ba3-125">**최종 사용자 환경 개선** 및 **기술 지원팀 볼륨 감소** 기술 지원팀에 연락하거나 지원을 요청하지 않고 한 번에 고유한 암호 문제를 해결하기 위해 최종 사용자에게 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="b5ba3-125">**Improve end-user experiences** and **reduce helpdesk volume** by giving end users the power to resolve their own password issues at once without calling a helpdesk or opening a support request.</span></span>
* <span data-ttu-id="b5ba3-126">**이동성 공급** - 사용자가 어디에서든 암호를 재설정할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="b5ba3-126">**Drive mobility** as users can reset their passwords from wherever they are.</span></span>

## <a name="azure-ad-self-service-password-reset-availability"></a><span data-ttu-id="b5ba3-127">Azure AD 셀프 서비스 암호 재설정 가용성</span><span class="sxs-lookup"><span data-stu-id="b5ba3-127">Azure AD self-service password reset availability</span></span>

<span data-ttu-id="b5ba3-128">Azure AD 셀프 서비스 암호 재설정은 구독에 따라 세 가지 계층으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5ba3-128">Azure AD self-service password reset is available in three tiers depending on your subscription.</span></span>

* <span data-ttu-id="b5ba3-129">**Azure AD Free** - 클라우드 전용 관리자는 해당하는 고유한 암호를 재설정할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="b5ba3-129">**Azure AD Free** – Cloud-only administrators can reset their own passwords</span></span>
* <span data-ttu-id="b5ba3-130">**Azure AD 기본** 또는 **유료 Office 365 구독** - 클라우드 전용 사용자 및 클라우드 전용 관리자는 해당하는 고유한 암호를 재설정할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="b5ba3-130">**Azure AD Basic** or any **Paid Office 365 Subscription** – Cloud-only users and cloud-only administrators can reset their own passwords</span></span>
* <span data-ttu-id="b5ba3-131">**Azure AD Premium** - 사용자 또는 관리자는 클라우드 전용, 페더레이션된 또는 암호 동기화된 사용자를 포함하여 해당하는 고유한 암호를 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5ba3-131">**Azure AD Premium** – Any user or administrator, including cloud-only, federated, or password synchronized users, can reset their own passwords.</span></span> <span data-ttu-id="b5ba3-132">온-프레미스 암호는 비밀번호 쓰기 저장을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5ba3-132">On-premises passwords require password writeback to be enabled.</span></span>

## <a name="azure-ad-self-service-password-reset-a-sum-of-the-parts"></a><span data-ttu-id="b5ba3-133">Azure AD 셀프 서비스 암호 재설정, 부분의 합</span><span class="sxs-lookup"><span data-stu-id="b5ba3-133">Azure AD self-service password reset, a sum of the parts</span></span>

<span data-ttu-id="b5ba3-134">Azure AD의 셀프 서비스 암호 재설정은 다음 구성 요소로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5ba3-134">Self-service password reset in Azure AD is made up of the following components:</span></span>

* <span data-ttu-id="b5ba3-135">**암호 관리 구성 포털** Azure Portal을 통해 테넌트에서 암호를 관리하는 방법에 대한 옵션을 제어할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="b5ba3-135">**Password management configuration portal** where you can control options for how passwords are managed in your tenant via the Azure portal</span></span>
* <span data-ttu-id="b5ba3-136">**암호 재설정 등록 포털** 사용자가 암호 재설정을 자동 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5ba3-136">**Password reset registration portal** where users can self-register for password reset</span></span>
* <span data-ttu-id="b5ba3-137">**암호 재설정 포털** 관리자가 정의한 과제 및 사용자가 제공한 답변을 사용하여 사용자는 자신의 암호를 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5ba3-137">**Password reset portal** where users can reset their password using the challenges defined by the administrator and the answers users have provided</span></span>
* <span data-ttu-id="b5ba3-138">**사용자 암호 변경 포털** 사용자는 이전 암호를 입력하고 새 암호를 제공하여 자신의 암호를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5ba3-138">**User password change portal** where users can change their own passwords by entering their old password and providing a new password</span></span>
* <span data-ttu-id="b5ba3-139">**암호 관리 보고서** 관리자는 Azure Portal에서 해당 테넌트에 대한 암호 작업 보고서를 보고 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5ba3-139">**Password management reports** where administrators can view and analyze password activity reports for their tenants in the Azure portal</span></span>
* <span data-ttu-id="b5ba3-140">**Azure AD Connect를 사용하여 온-프레미스에 비밀번호 쓰기 저장**을 사용하면 클라우드에서 온-프레미스, 페더레이션 또는 암호 동기화 사용자를 관리할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="b5ba3-140">**Password writeback to on-premises using Azure AD Connect** allows you to enable management of on-premises, federated, or password synchronized users from the cloud</span></span>

## <a name="azure-ad-pricing-sla-updates-and-roadmap"></a><span data-ttu-id="b5ba3-141">Azure AD 가격 책정, SLA, 업데이트 및 로드맵</span><span class="sxs-lookup"><span data-stu-id="b5ba3-141">Azure AD pricing, SLA, updates, and roadmap</span></span>

<span data-ttu-id="b5ba3-142">다음 페이지에서 이러한 항목에 대한 자세한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5ba3-142">More detail about these topics can be found on the following pages</span></span>

* [<span data-ttu-id="b5ba3-143">**Azure AD 가격 책정 정보**</span><span class="sxs-lookup"><span data-stu-id="b5ba3-143">**Azure AD Pricing Details**</span></span>](https://azure.microsoft.com/pricing/details/active-directory/)
* [<span data-ttu-id="b5ba3-144">**Office 365 가격 책정**</span><span class="sxs-lookup"><span data-stu-id="b5ba3-144">**Office 365 Pricing**</span></span>](https://products.office.com/compare-all-microsoft-office-products?tab=2)
* [<span data-ttu-id="b5ba3-145">**Azure Service Level Agreements(서비스 수준 약정)**</span><span class="sxs-lookup"><span data-stu-id="b5ba3-145">**Azure Service Level Agreements**</span></span>](https://azure.microsoft.com/support/legal/sla/)
* [<span data-ttu-id="b5ba3-146">**Microsoft 온라인 서비스에 대한 Service Level Agreements(서비스 수준 약정)**</span><span class="sxs-lookup"><span data-stu-id="b5ba3-146">**Service Level Agreement for Microsoft Online Services**</span></span>](http://go.microsoft.com/fwlink/?LinkID=272026&clcid=0x409)
* [<span data-ttu-id="b5ba3-147">**Azure 업데이트**</span><span class="sxs-lookup"><span data-stu-id="b5ba3-147">**Azure Updates**</span></span>](https://azure.microsoft.com/updates/)
* [<span data-ttu-id="b5ba3-148">**Azure 로드맵**</span><span class="sxs-lookup"><span data-stu-id="b5ba3-148">**Azure Roadmap**</span></span>](https://www.microsoft.com/cloud-platform/roadmap-recently-available)

## <a name="next-steps"></a><span data-ttu-id="b5ba3-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b5ba3-149">Next steps</span></span>

<span data-ttu-id="b5ba3-150">다음 링크는 Azure AD를 사용한 암호 재설정에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b5ba3-150">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="b5ba3-151">[**빠른 시작**](active-directory-passwords-getting-started.md) - Azure AD 셀프 서비스 암호 관리를 사용하여 운영 시작</span><span class="sxs-lookup"><span data-stu-id="b5ba3-151">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="b5ba3-152">[**라이선스**](active-directory-passwords-licensing.md) - Azure AD 라이선스 구성</span><span class="sxs-lookup"><span data-stu-id="b5ba3-152">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="b5ba3-153">[**데이터**](active-directory-passwords-data.md) - 암호 관리에 필요한 데이터 및 사용 방식을 이해</span><span class="sxs-lookup"><span data-stu-id="b5ba3-153">[**Data**](active-directory-passwords-data.md) - Understand the data that is required and how it is used for password management</span></span>
* <span data-ttu-id="b5ba3-154">[**롤아웃**](active-directory-passwords-best-practices.md) - 여기서 제공하는 지침을 사용하여 배포 계획을 세우고 사용자에게 SSPR 배포</span><span class="sxs-lookup"><span data-stu-id="b5ba3-154">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="b5ba3-155">[**사용자 지정**](active-directory-passwords-customize.md) - 회사 SSPR 경험의 모양과 느낌을 사용자 지정.</span><span class="sxs-lookup"><span data-stu-id="b5ba3-155">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="b5ba3-156">[**보고**](active-directory-passwords-reporting.md) - 사용자가 SSPR 기능에 액세스하는 조건, 시간 및 위치 탐색</span><span class="sxs-lookup"><span data-stu-id="b5ba3-156">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="b5ba3-157">[**기술 심층 분석**](active-directory-passwords-how-it-works.md) - 작동 방식을 이해하기 위해 심층 분석</span><span class="sxs-lookup"><span data-stu-id="b5ba3-157">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="b5ba3-158">[**질문과 대답**](active-directory-passwords-faq.md) - 어떤 방식으로?</span><span class="sxs-lookup"><span data-stu-id="b5ba3-158">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="b5ba3-159">그 이유는</span><span class="sxs-lookup"><span data-stu-id="b5ba3-159">Why?</span></span> <span data-ttu-id="b5ba3-160">무엇을?</span><span class="sxs-lookup"><span data-stu-id="b5ba3-160">What?</span></span> <span data-ttu-id="b5ba3-161">어디서?</span><span class="sxs-lookup"><span data-stu-id="b5ba3-161">Where?</span></span> <span data-ttu-id="b5ba3-162">누가?</span><span class="sxs-lookup"><span data-stu-id="b5ba3-162">Who?</span></span> <span data-ttu-id="b5ba3-163">언제?</span><span class="sxs-lookup"><span data-stu-id="b5ba3-163">When?</span></span> <span data-ttu-id="b5ba3-164">- 많은 분들이 항상 묻는 질문에 대한 답변입니다.</span><span class="sxs-lookup"><span data-stu-id="b5ba3-164">- Answers to questions you always wanted to ask</span></span>
* <span data-ttu-id="b5ba3-165">[**문제 해결**](active-directory-passwords-troubleshoot.md) - SSPR의 일반적인 문제 해결 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="b5ba3-165">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>

