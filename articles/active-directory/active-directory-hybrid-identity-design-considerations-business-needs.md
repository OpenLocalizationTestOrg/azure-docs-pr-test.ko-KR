---
title: "Azure Active Directory 하이브리드 ID 디자인 고려 사항 - ID 요구 사항 확인 | Microsoft Docs"
description: "하이브리드 ID 설계에 대한 요구 사항을 정의하도록 하는 회사의 비즈니스 요구를 식별합니다."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: de690978-84ef-41ad-9dfe-785722d343a1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 6503034b3f5a17a2a42338c73329eef0b01f2f27
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="determine-identity-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="b20d5-103">하이브리드 ID 솔루션에 대한 ID 요구 사항 확인</span><span class="sxs-lookup"><span data-stu-id="b20d5-103">Determine identity requirements for your hybrid identity solution</span></span>
<span data-ttu-id="b20d5-104">하이브리드 ID 솔루션을 설계하는 첫 번째 단계는 이 솔루션을 활용하는 비즈니스 조직에 대한 요구 사항을 결정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-104">The first step in designing a hybrid identity solution is to determine the requirements for the business organization that will be leveraging this solution.</span></span>  <span data-ttu-id="b20d5-105">하이브리드 ID는 지원 역할(인증을 제공하여 다른 모든 클라우드 솔루션을 지원)로 시작하고 사용자에 대한 새 워크로드의 잠금을 해제하는 새롭고 흥미로운 기능을 계속하여 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-105">Hybrid identity starts as a supporting role (it supports all other cloud solutions by providing authentication) and goes on to provide new and interesting capabilities that unlock new workloads for users.</span></span>  <span data-ttu-id="b20d5-106">사용자에 대해 채택하려는 이러한 워크로드 또는 서비스는 하이브리드 ID 설계에 대한 요구 사항을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-106">These workloads or services that you wish to adopt for your users will dictate the requirements for the hybrid identity design.</span></span>  <span data-ttu-id="b20d5-107">이러한 서비스와 워크로드는 온-프레미스 및 클라우드에서 하이브리드 ID를 활용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-107">These services and workloads need to leverage hybrid identity both on-premises and in the cloud.</span></span>  

<span data-ttu-id="b20d5-108">현재의 요구 사항 및 미래 회사 계획이 무엇인지 이해하려면 비즈니스의 이러한 주요 측면을 검토해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-108">You need to go over these key aspects of the business to understand what it is a requirement now and what the company plans for the future.</span></span> <span data-ttu-id="b20d5-109">하이브리드 ID 설계에 대한 장기적인 전략을 표시하지 않는다면 비즈니스가 성장하고 변화해야 할 때 솔루션은 확장이 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-109">If you don’t have the visibility of the long term strategy for hybrid identity design, chances are that your solution will not be scalable as the business needs grow and change.</span></span>   <span data-ttu-id="b20d5-110">아래 다이어그램은 사용자에 잠금이 해제된 하이브리드 ID 아키텍처 및 워크로드의 예를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-110">T he diagram below shows an example of a hybrid identity architecture and the workloads that are being unlocked for users.</span></span> <span data-ttu-id="b20d5-111">잠금을 해제하고 견고한 하이브리드 ID 전략을 제공할 수 있는 새로운 가능성의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-111">This is just an example of all the new possibilities that can be unlocked and delivered with a solid hybrid identity strategy.</span></span> 

<span data-ttu-id="b20d5-112">하이브리드 ID 아키텍처의 일부인 구성 요소 일부 ![](./media/hybrid-id-design-considerations/hybrid-identity-architechture.png)</span><span class="sxs-lookup"><span data-stu-id="b20d5-112">Some components that are part of the hybrid identity architecture ![](./media/hybrid-id-design-considerations/hybrid-identity-architechture.png)</span></span>

## <a name="determine-business-needs"></a><span data-ttu-id="b20d5-113">비즈니스 요구 사항 결정</span><span class="sxs-lookup"><span data-stu-id="b20d5-113">Determine business needs</span></span>
<span data-ttu-id="b20d5-114">이러한 회사가 같은 업계의 일부이더라도 실제 비즈니스 요구 사항이 다르기 때문에 각 회사는 서로 다른 요구 사항을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-114">Each company will have different requirements, even if these companies are part of the same industry, the real business requirements might vary.</span></span> <span data-ttu-id="b20d5-115">업계에서 모범 사례를 활용할 수 있지만 궁극적으로 하이브리드 ID 설계에 대한 요구 사항을 정의하도록 하는 것은 회사의 비즈니스 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-115">You can still leverage best practices from the industry, but ultimately it is the company’s business needs that will lead you to define the requirements for the hybrid identity design.</span></span> 

<span data-ttu-id="b20d5-116">다음 질문에 대답하여 비즈니스 요구를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-116">Make sure to answer the following questions to identify your business needs:</span></span>

* <span data-ttu-id="b20d5-117">회사가 IT 운영 비용 절감을 고민하고 있습니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-117">Is your company looking to cut IT operational cost?</span></span>
* <span data-ttu-id="b20d5-118">회사가 클라우드 자산(SaaS 앱, 인프라)을 보호에 대해 고민하고 있습니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-118">Is your company looking to secure cloud assets (SaaS apps, infrastructure)?</span></span>
* <span data-ttu-id="b20d5-119">회사가 IT를 현대화하기 위해 고민하고 있습니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-119">Is your company looking to modernize your IT?</span></span>
  * <span data-ttu-id="b20d5-120">사용자가 다른 형태의 트래픽이 다른 리소스에 액세스할 수 있도록 DMZ에 예외를 만들기 위해 더 많은 모바일 및 IT를 요구합니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-120">Are your users more mobile and demanding IT to create exceptions into your DMZ to allow different type of traffic to access different resources?</span></span>
  * <span data-ttu-id="b20d5-121">회사에는 이러한 최신 사용자에게 게시하는 데 필요하지만 쉽게 다시 작성하지 않는 레거시 앱이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-121">Does your company have legacy apps that needed to be published to these modern users but are not easy to rewrite?</span></span>
  * <span data-ttu-id="b20d5-122">회사가 이러한 모든 작업을 수행하는 동시에 제어해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-122">Does your company need to accomplish all these tasks and bring it under control at the same time?</span></span>
* <span data-ttu-id="b20d5-123">회사가 Microsoft의 Azure 보안 전문가 온-프레미스의 전문 지식을 활용하는 새로운 도구를 도입하여 사용자 ID를 보호하고 위험을 줄이려고 합니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-123">Is your company looking to secure users’ identities and reduce risk by bringing new tools that leverage the expertise of Microsoft’s Azure security expertise on-premises?</span></span>
* <span data-ttu-id="b20d5-124">회사가 온-프레미스에서 "외부" 계정을 제거하고 온-프레미스 환경 내에서 유휴 위협이 아닌 클라우드로 이동하려 합니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-124">Is your company trying to get rid of the dreaded “external” accounts on premises and move them to the cloud where they are no longer a dormant threat inside your on-premises environment?</span></span>

## <a name="analyze-on-premises-identity-infrastructure"></a><span data-ttu-id="b20d5-125">온-프레미스 ID 인프라 분석</span><span class="sxs-lookup"><span data-stu-id="b20d5-125">Analyze on-premises identity infrastructure</span></span>
<span data-ttu-id="b20d5-126">회사의 비즈니스 요구 사항에 관해 아이디어가 있으므로 온-프레미스 ID 인프라를 평가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-126">Now that you have an idea regarding your company business requirements, you need to evaluate your on-premises identity infrastructure.</span></span> <span data-ttu-id="b20d5-127">이 평가판은 클라우드 ID 관리 시스템에 현재 ID 솔루션을 통합하는 기술 요구 사항을 정의하는 데 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-127">This evaluation is important for defining the technical requirements to integrate your current identity solution to the cloud identity management system.</span></span> <span data-ttu-id="b20d5-128">다음 질문에 답변하세요.</span><span class="sxs-lookup"><span data-stu-id="b20d5-128">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="b20d5-129">회사는 온-프레미스에 어떤 인증 및 권한 부여 솔루션을 사용합니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-129">What authentication and authorization solution does your company use on-premises?</span></span> 
* <span data-ttu-id="b20d5-130">회사에는 현재 온-프레미스 동기화 서비스가 있습니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-130">Does your company currently have any on-premises synchronization services?</span></span>
* <span data-ttu-id="b20d5-131">회사가 타사 ID 공급자(IdP)를 사용합니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-131">Does your company use any third-party Identity Providers (IdP)?</span></span>

<span data-ttu-id="b20d5-132">또한 회사에 있을 수도 있는 클라우드 서비스를 인식해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-132">You also need to be aware of the cloud services that your company might have.</span></span> <span data-ttu-id="b20d5-133">사용자 환경에서 SaaS IaaS, PaaS 모델을 사용하는 현재 통합을 이해하도록 평가를 수행하는 것이 매우 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-133">Performing an assessment to understand the current integration with SaaS, IaaS or PaaS models in your environment is very important.</span></span> <span data-ttu-id="b20d5-134">이 평가를 진행하는 동안 다음 질문에 답변하세요.</span><span class="sxs-lookup"><span data-stu-id="b20d5-134">Make sure to answer the following questions during this assessment:</span></span>

* <span data-ttu-id="b20d5-135">귀사가 클라우드 서비스 공급자와 통합된 부분이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-135">Does your company have any integration with a cloud service provider?</span></span>
* <span data-ttu-id="b20d5-136">만약 그렇다면 어떤 서비스를 사용하십니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-136">If yes, which services are being used?</span></span>
* <span data-ttu-id="b20d5-137">이 통합이 현재 운영 중입니까 아니면 파일럿입니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-137">Is this integration currently in production or is it a pilot?</span></span>

> [!NOTE]
> <span data-ttu-id="b20d5-138">모든 앱 및 클라우드 서비스의 정확한 매핑이 되지 않은 경우 클라우드 앱 검색 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-138">If you don’t have an accurate mapping of all your apps and cloud services, you can use the Cloud App Discovery tool.</span></span> <span data-ttu-id="b20d5-139">이 도구는 조직의 모든 비즈니스 및 소비자 클라우드 앱에 가시성이 있는 IT 부서를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-139">This tool can provide your IT department with visibility into all your organization’s business and consumer cloud apps.</span></span> <span data-ttu-id="b20d5-140">따라서 사용 패턴 및 클라우드 응용 프로그램에 액세스하는 사용자에 대한 세부 정보를 포함하여 조직의 섀도 IT를 더 쉽게 발견할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-140">That makes it easier than ever to discover shadow IT in your organization, including details on usage patterns and any users accessing your cloud applications.</span></span> <span data-ttu-id="b20d5-141">시작하려면 [클라우드 앱 검색](active-directory-cloudappdiscovery-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b20d5-141">To get started see [Cloud app discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>
> 
> 

## <a name="evaluate-identity-integration-requirements"></a><span data-ttu-id="b20d5-142">ID 통합 요구 사항 평가</span><span class="sxs-lookup"><span data-stu-id="b20d5-142">Evaluate identity integration requirements</span></span>
<span data-ttu-id="b20d5-143">다음으로 ID 통합 요구 사항을 평가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-143">Next, you need to evaluate the identity integration requirements.</span></span> <span data-ttu-id="b20d5-144">이 평가는 사용자가 인증하는 방법, 조직의 우선 순위가 클라우드에서 보이는 방법, 조직이 권한을 부여하는 방법 및 사용자 환경이 변할 모습에 대한 기술 요구 사항을 정의하는 데 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-144">This evaluation is important to define the technical requirements for how users will authenticate, how the organization’s presence will look in the cloud, how the organization will allow authorization and what the user experience is going to be.</span></span> <span data-ttu-id="b20d5-145">다음 질문에 답변하세요.</span><span class="sxs-lookup"><span data-stu-id="b20d5-145">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="b20d5-146">조직이 페더레이션, 표준 인증 또는 둘 모두를 사용합니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-146">Will your organization be using federation, standard authentication or both?</span></span>
* <span data-ttu-id="b20d5-147">페더레이션 요구 사항입니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-147">Is federation a requirement?</span></span>  <span data-ttu-id="b20d5-148">다음 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-148">Because of the following:</span></span>
  * <span data-ttu-id="b20d5-149">Kerberos 기반 SSO</span><span class="sxs-lookup"><span data-stu-id="b20d5-149">Kerberos-based SSO</span></span>
  * <span data-ttu-id="b20d5-150">회사에는 SAML 또는 유사한 페더레이션 기능을 사용하는 온-프레미스 응용 프로그램이 있습니다.(기본 제공 또는 타사 제공 중 하나)</span><span class="sxs-lookup"><span data-stu-id="b20d5-150">Your company has an on-premises applications (either built in-house or 3rd party) that uses SAML or similar federation capabilities.</span></span>
  * <span data-ttu-id="b20d5-151">스마트 카드를 통한 MFA.</span><span class="sxs-lookup"><span data-stu-id="b20d5-151">MFA via Smart Cards.</span></span> <span data-ttu-id="b20d5-152">RSA SecurID 등.</span><span class="sxs-lookup"><span data-stu-id="b20d5-152">RSA SecurID, etc.</span></span>
  * <span data-ttu-id="b20d5-153">아래 질문을 해결하는 클라이언트 액세스 규칙:</span><span class="sxs-lookup"><span data-stu-id="b20d5-153">Client access rules that address the questions below:</span></span>
    1. <span data-ttu-id="b20d5-154">클라이언트의 IP 주소에 기반하여 Office 365에 대한 모든 외부 액세스를 차단할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-154">Can I block all external access to Office 365 based on the IP address of the client?</span></span>
    2. <span data-ttu-id="b20d5-155">Exchange ActiveSync를 제외하고 Office 365에 대한 모든 외부 액세스를 차단할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-155">Can I block all external access to Office 365, except Exchange ActiveSync?</span></span>
    3. <span data-ttu-id="b20d5-156">브라우저 기반 앱(OWA, SPO)을 제외한 Office 365에 모든 외부 액세스를 차단할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-156">Can I block all external access to Office 365, except for browser-based apps (OWA, SPO)</span></span>
    4. <span data-ttu-id="b20d5-157">지정된 AD 그룹의 멤버에 대한 Office 365의 모든 외부 액세스를 차단할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-157">Can I block all external access to Office 365 for members of designated AD groups</span></span>
* <span data-ttu-id="b20d5-158">보안/감사 문제</span><span class="sxs-lookup"><span data-stu-id="b20d5-158">Security/auditing concerns</span></span>
* <span data-ttu-id="b20d5-159">페더레이션된 인증에서 기존 투자</span><span class="sxs-lookup"><span data-stu-id="b20d5-159">Already existing investment in federated authentication</span></span>
* <span data-ttu-id="b20d5-160">회사는 클라우드의 도메인에 어떤 이름을 사용합니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-160">What name will our organization use for our domain in the cloud?</span></span>
* <span data-ttu-id="b20d5-161">조직에는 사용자 지정 도메인이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-161">Does the organization have a custom domain?</span></span>
  1. <span data-ttu-id="b20d5-162">해당 도메인이 공용이고 DNS를 통해 쉽게 확인할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-162">Is that domain public and easily verifiable via DNS?</span></span>
  2. <span data-ttu-id="b20d5-163">그렇지 않다면 대체 UPN를 AD에 등록하는데 사용할 수 있는 공용 도메인이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-163">If it is not, then do you have a public domain that can be used to register an alternate UPN in AD?</span></span>
* <span data-ttu-id="b20d5-164">사용자 식별자가 클라우드 표현에 대해 일관됩니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-164">Are the user identifiers consistent for cloud representation?</span></span> 
* <span data-ttu-id="b20d5-165">조직에는 클라우드 서비스와 통합을 필요로 하는 앱이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-165">Does the organization have apps that require integration with cloud services?</span></span>
* <span data-ttu-id="b20d5-166">조직이 여러 도메인을 가지고 표준 또는 페더레이션된 인증을 모두 사용합니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-166">Does the organization have multiple domains and will they all use standard or federated authentication?</span></span>

## <a name="evaluate-applications-that-run-in-your-environment"></a><span data-ttu-id="b20d5-167">사용자 환경에서 실행하는 응용 프로그램 평가</span><span class="sxs-lookup"><span data-stu-id="b20d5-167">Evaluate applications that run in your environment</span></span>
<span data-ttu-id="b20d5-168">온-프레미스 및 클라우드 인프라에 관한 아이디어가 있으므로 이러한 환경에서 실행되는 응용 프로그램을 평가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-168">Now that you have an idea regarding your on-premises and cloud infrastructure, you need to evaluate the applications that run in these environments.</span></span> <span data-ttu-id="b20d5-169">이 평가판은 클라우드 ID 관리 시스템에 이러한 응용 프로그램을 통합하는 기술 요구 사항을 정의하는 데 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-169">This evaluation is important to define the technical requirements to integrate these applications to the cloud identity management system.</span></span> <span data-ttu-id="b20d5-170">다음 질문에 답변하세요.</span><span class="sxs-lookup"><span data-stu-id="b20d5-170">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="b20d5-171">응용 프로그램은 어디에 있습니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-171">Where will our applications live?</span></span>
* <span data-ttu-id="b20d5-172">사용자는 온-프레미스 응용 프로그램에 액세스합니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-172">Will users be accessing on-premises applications?</span></span>  <span data-ttu-id="b20d5-173">클라우드에서?</span><span class="sxs-lookup"><span data-stu-id="b20d5-173">In the cloud?</span></span> <span data-ttu-id="b20d5-174">또는 둘 모두?</span><span class="sxs-lookup"><span data-stu-id="b20d5-174">Or both?</span></span>
* <span data-ttu-id="b20d5-175">기존 응용 프로그램 워크로드를 클라우드로 이동할 계획이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-175">Are there plans to take the existing application workloads and move them to the cloud?</span></span>
* <span data-ttu-id="b20d5-176">클라우드 인증을 사용하는 온-프레미스 또는 클라우드에 위치하는 새 응용 프로그램을 개발할 계획이 있습니까 ?</span><span class="sxs-lookup"><span data-stu-id="b20d5-176">Are there plans to develop new applications that will reside either on-premises or in the cloud that will use cloud authentication?</span></span>

## <a name="evaluate-user-requirements"></a><span data-ttu-id="b20d5-177">사용자 요구 사항 평가</span><span class="sxs-lookup"><span data-stu-id="b20d5-177">Evaluate user requirements</span></span>
<span data-ttu-id="b20d5-178">또한 사용자 요구 사항을 평가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-178">You also have to evaluate the user requirements.</span></span> <span data-ttu-id="b20d5-179">이 평가판은 사용자가 클라우드에 전환할 때 사용자를 등록 및 지원하기 위해 필요한 단계를 정의하는 데 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-179">This evaluation is important to define the steps that will be needed for on-boarding and assisting users as they transition to the cloud.</span></span> <span data-ttu-id="b20d5-180">다음 질문에 답변하세요.</span><span class="sxs-lookup"><span data-stu-id="b20d5-180">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="b20d5-181">사용자는 응용 프로그램 온-프레미스에 액세스합니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-181">Will users be accessing applications on-premises?</span></span>
* <span data-ttu-id="b20d5-182">사용자는 클라우드에서 응용 프로그램에 액세스합니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-182">Will users be accessing applications in the cloud?</span></span>
* <span data-ttu-id="b20d5-183">일반적으로 사용자는 해당 온-프레미스 환경에 어떻게 로그인합니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-183">How do users typically login to their on-premises environment?</span></span>
* <span data-ttu-id="b20d5-184">사용자가 클라우드에 어떻게 로그인합니까?</span><span class="sxs-lookup"><span data-stu-id="b20d5-184">How will users sign-in to the cloud?</span></span>

> [!NOTE]
> <span data-ttu-id="b20d5-185">각 답변을 주목하고 답변 이유를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-185">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="b20d5-186">[사고 대응 요구 사항 결정](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) 은 사용할 수 있는 옵션 및 각 옵션의 장단점을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-186">[Determine incident response requirements](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) will go over the options available and pros/cons of each option.</span></span>  <span data-ttu-id="b20d5-187">질문에 답변함으로써 비즈니스 요구 사항에 가장 적합한 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b20d5-187">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b20d5-188">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b20d5-188">Next steps</span></span>
[<span data-ttu-id="b20d5-189">디렉터리 동기화 요구 사항 결정</span><span class="sxs-lookup"><span data-stu-id="b20d5-189">Determine directory synchronization requirements</span></span>](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)

## <a name="see-also"></a><span data-ttu-id="b20d5-190">참고 항목</span><span class="sxs-lookup"><span data-stu-id="b20d5-190">See also</span></span>
[<span data-ttu-id="b20d5-191">디자인 고려 사항 개요</span><span class="sxs-lookup"><span data-stu-id="b20d5-191">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

