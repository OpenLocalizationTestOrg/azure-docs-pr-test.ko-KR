---
title: "Azure Active Directory 하이브리드 ID 설계 고려 사항 - 액세스 제어 요구 사항 확인 | Microsoft Docs"
description: "하이브리드 환경에서 ID의 기본 요소 및 사용자의 리소스에 대한 액세스 요구 사항 식별에 대해 설명합니다."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: e3b3b984-0d15-4654-93be-a396324b9f5e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 6404940da460461632616fe49f055d50c2a7aba3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="determine-access-control-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="400f8-103">하이브리드 ID 솔루션에 대한 액세스 제어 요구 사항 확인</span><span class="sxs-lookup"><span data-stu-id="400f8-103">Determine access control requirements for your hybrid identity solution</span></span>
<span data-ttu-id="400f8-104">또한 조직이 해당 하이브리드 ID 솔루션을 설계하는 경우 사용자는 이 기회를 사용하여 사용자가 사용할 수 있게 하려는 리소스에 대한 액세스 요구 사항을 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400f8-104">When an organization is designing their hybrid identity solution they can also use this opportunity to review access requirements for the resources that they are planning to make it available for users.</span></span> <span data-ttu-id="400f8-105">ID의 네 가지 기본 요소에 대한 데이터 액세스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="400f8-105">The data access cross all four pillars of identity, which are:</span></span>

* <span data-ttu-id="400f8-106">관리</span><span class="sxs-lookup"><span data-stu-id="400f8-106">Administration</span></span>
* <span data-ttu-id="400f8-107">인증</span><span class="sxs-lookup"><span data-stu-id="400f8-107">Authentication</span></span>
* <span data-ttu-id="400f8-108">권한 부여</span><span class="sxs-lookup"><span data-stu-id="400f8-108">Authorization</span></span>
* <span data-ttu-id="400f8-109">감사</span><span class="sxs-lookup"><span data-stu-id="400f8-109">Auditing</span></span>

<span data-ttu-id="400f8-110">다음 섹션에서는 인증 및 권한 부여를 자세히 살펴봅니다. 관리 및 감사는 하이브리드 ID 수명 주기의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="400f8-110">The sections that follows will cover authentication and authorization in more details, administration and auditing are part of the hybrid identity lifecycle.</span></span> <span data-ttu-id="400f8-111">이러한 기능에 대한 자세한 내용은 [하이브리드 ID 관리 작업 결정](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="400f8-111">Read [Determine hybrid identity management tasks](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) for more information about these capabilities.</span></span>

> [!NOTE]
> <span data-ttu-id="400f8-112">이러한 기본 요소 각각에 대한 자세한 내용은 [ID의 네 가지 기본 요소 - 하이브리드 IT 시대에서 ID 관리](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) 를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="400f8-112">Read [The Four Pillars of Identity - Identity Management in the Age of Hybrid IT](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) for more information about each one of those pillars.</span></span>
> 
> 

## <a name="authentication-and-authorization"></a><span data-ttu-id="400f8-113">인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="400f8-113">Authentication and authorization</span></span>
<span data-ttu-id="400f8-114">인증 및 권한 부여에 대한 여러 시나리오가 있으며 이러한 시나리오에는 회사가 도입할 하이브리드 ID 솔루션에서 충족시켜야 하는 특정 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400f8-114">There are different scenarios for authentication and authorization, these scenarios will have specific requirements that must be fulfilled by the hybrid identity solution that the company is going to adopt.</span></span> <span data-ttu-id="400f8-115">기업간(B2B) 통신을 포함하는 시나리오는 조직에서 사용하는 인증 및 권한 부여 방법이 비즈니스 파트너와 통신할 수 있는지 확인해야 하므로 IT 관리자에게 추가적인 도전을 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400f8-115">Scenarios involving Business to Business (B2B) communication can add an extra challenge for IT Admins since they will need to ensure that the authentication and authorization method used by the organization can communicate with their business partners.</span></span> <span data-ttu-id="400f8-116">인증 및 권한 부여 요구 사항에 대한 설계 프로세스 동안 응답된 다음 질문을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="400f8-116">During the designing process for authentication and authorization requirements, ensure that the following questions are answered:</span></span>

* <span data-ttu-id="400f8-117">조직이 해당 ID 관리 시스템에 있는 사용자만 인증하고 권한을 부여합니까?</span><span class="sxs-lookup"><span data-stu-id="400f8-117">Will your organization authenticate and authorize only users located at their identity management system?</span></span>
  * <span data-ttu-id="400f8-118">B2B 시나리오에 대한 계획이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="400f8-118">Are there any plans for B2B scenarios?</span></span>
  * <span data-ttu-id="400f8-119">있다면 어떤 프로토콜(SAML, OAuth, Kerberos, 토큰 또는 인증서)이 양쪽 비즈니스를 연결하는 데 사용할 수 있는지 알고 계십니까?</span><span class="sxs-lookup"><span data-stu-id="400f8-119">If yes, do you already know which protocols (SAML, OAuth, Kerberos, Tokens or Certificates) will be used to connect both businesses?</span></span>
* <span data-ttu-id="400f8-120">채택하려는 하이브리드 ID 솔루션이 해당 프로토콜을 지원합니까?</span><span class="sxs-lookup"><span data-stu-id="400f8-120">Does the hybrid identity solution that you are going to adopt support those protocols?</span></span>

<span data-ttu-id="400f8-121">고려해야 할 다른 중요한 사항은 사용자 및 파트너가 사용할 인증 리포지토리가 배치될 위치 및 사용할 관리 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="400f8-121">Another important point to consider is where the authentication repository that will be used by users and partners will be located and the administrative model to be used.</span></span> <span data-ttu-id="400f8-122">다음 두 가지 핵심 옵션을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="400f8-122">Consider the following two core options:</span></span>

* <span data-ttu-id="400f8-123">중앙 집중화됨: 이 모델에서 사용자의 자격 증명, 정책 및 관리는 온-프레미스 또는 클라우드에서 중앙 집중화될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400f8-123">Centralized: in this model the user’s credentials, policies and administration can be centralized on-premises or in the cloud.</span></span>
* <span data-ttu-id="400f8-124">하이브리드: 이 모델에서 사용자의 자격 증명, 정책 및 관리는 온-프레미스에서 중앙 집중화되고 클라우드에서 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="400f8-124">Hybrid: in this model the user’s credentials, policies and administration will be centralized on-premises and a replicated in the cloud.</span></span>

<span data-ttu-id="400f8-125">조직이 어떤 모델을 도입할지는 비즈니스 요구 사항에 따라 달라집니다. 다음 질문에 응답하여 ID 관리 시스템의 위치 및 사용할 관리 모드를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="400f8-125">Which model your organization will adopt will vary according to their business requirements, you want to answer the following questions to identify where the identity management system will reside and the administrative mode to use:</span></span>

* <span data-ttu-id="400f8-126">현재 조직에는 ID 관리 온-프레미스가 있습니까?</span><span class="sxs-lookup"><span data-stu-id="400f8-126">Does your organization currently have an identity management on-premises?</span></span>
  * <span data-ttu-id="400f8-127">있다면 유지할 계획입니까?</span><span class="sxs-lookup"><span data-stu-id="400f8-127">If yes, do they plan to keep it?</span></span>
  * <span data-ttu-id="400f8-128">조직이 따라야 하고 ID 관리 시스템이 위치해야 할 규정 또는 준수 요구 사항이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="400f8-128">Are there any regulation or compliance requirements that your organization must follow that dictates where the identity management system should reside?</span></span>
* <span data-ttu-id="400f8-129">조직은 온-프레미스 나 클라우드에 위치한 앱에 Single Sign-On을 사용합니까?</span><span class="sxs-lookup"><span data-stu-id="400f8-129">Does your organization use single sign-on for apps located on-premises or in the cloud?</span></span>
  * <span data-ttu-id="400f8-130">사용한다면 하이브리드 ID 모델의 도입은 이 프로세스에 영향을 줍니까?</span><span class="sxs-lookup"><span data-stu-id="400f8-130">If yes, does the adoption of a hybrid identity model affect this process?</span></span>

## <a name="access-control"></a><span data-ttu-id="400f8-131">액세스 제어</span><span class="sxs-lookup"><span data-stu-id="400f8-131">Access Control</span></span>
<span data-ttu-id="400f8-132">인증 및 권한 부여는 사용자의 유효성 검사를 통해 회사 데이터에 액세스할 수 있도록 하는 핵심 요소이며 또한 관리 중인 리소스를 통해 이러한 사용자가 가질 액세스 수준 및 관리자가 가질 액세스 수준을 제어하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="400f8-132">While authentication and authorization are core elements to enable access to corporate data through user’s validation, it is also important to control the level of access that these users will have and the level of access administrators will have over the resources that they are managing.</span></span> <span data-ttu-id="400f8-133">하이브리드 ID 솔루션은 리소스, 위임 및 역할 기반 액세스 제어에 대한 세부적인 액세스를 제공할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="400f8-133">Your hybrid identity solution must be able to provide granular access to resources, delegation and role base access control.</span></span> <span data-ttu-id="400f8-134">액세스 제어에 관하여 다음과 같은 질문에 응답해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="400f8-134">Ensure that the following question are answered regarding access control:</span></span>

* <span data-ttu-id="400f8-135">회사에는 상승된 권한이 있는 둘 이상의 사용자가 있어서 ID 시스템을 관리합니까?</span><span class="sxs-lookup"><span data-stu-id="400f8-135">Does your company have more than one user with elevated privilege to manage your identity system?</span></span>
  * <span data-ttu-id="400f8-136">그렇다면 각 사용자는 동일한 수준의 액세스 권한이 필요합니까?</span><span class="sxs-lookup"><span data-stu-id="400f8-136">If yes, does each user need the same access level?</span></span>
* <span data-ttu-id="400f8-137">회사가 사용자에게 액세스 권한을 위임하여 특정 리소스를 관리해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="400f8-137">Would your company need to delegate access to users to manage specific resources?</span></span>
  * <span data-ttu-id="400f8-138">그렇다면 얼마나 자주 발생합니까?</span><span class="sxs-lookup"><span data-stu-id="400f8-138">If yes, how frequently this happens?</span></span>
* <span data-ttu-id="400f8-139">회사가 온-프레미스와 클라우드 리소스 사이에 액세스 제어 기능을 통합해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="400f8-139">Would your company need to integrate access control capabilities between on-premises and cloud resources?</span></span>
* <span data-ttu-id="400f8-140">회사가 일부 조건에 따라 리소스에 대한 액세스를 제한해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="400f8-140">Would your company need to limit access to resources according to some conditions?</span></span>
* <span data-ttu-id="400f8-141">회사에는 일부 리소스에 사용자 지정 제어 액세스가 필요한 응용 프로그램이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="400f8-141">Would your company have any application that needs custom control access to some resources?</span></span>
  * <span data-ttu-id="400f8-142">그렇다면 해당 앱은 어디에 위치합니까(온-프레미스 또는 클라우드)?</span><span class="sxs-lookup"><span data-stu-id="400f8-142">If yes, where are those apps located (on-premises or in the cloud)?</span></span>
  * <span data-ttu-id="400f8-143">그렇다면 해당 대상 리소스는 어디에 위치합니까(온-프레미스 또는 클라우드)?</span><span class="sxs-lookup"><span data-stu-id="400f8-143">If yes, where are those target resources located (on-premises or in the cloud)?</span></span>

> [!NOTE]
> <span data-ttu-id="400f8-144">각 답변을 주목하고 답변 이유를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="400f8-144">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="400f8-145">[데이터 보호 전략 정의](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) 에서는 사용할 수 있는 옵션과 각 옵션의 장점/단점을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="400f8-145">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over the options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="400f8-146">질문에 답변하여 비즈니스 요구 사항에 가장 적합한 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="400f8-146">By answering those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="400f8-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="400f8-147">Next steps</span></span>
[<span data-ttu-id="400f8-148">사고 대응 요구 사항 결정</span><span class="sxs-lookup"><span data-stu-id="400f8-148">Determine incident response requirements</span></span>](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="see-also"></a><span data-ttu-id="400f8-149">참고 항목</span><span class="sxs-lookup"><span data-stu-id="400f8-149">See Also</span></span>
[<span data-ttu-id="400f8-150">설계 고려 사항 개요</span><span class="sxs-lookup"><span data-stu-id="400f8-150">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

