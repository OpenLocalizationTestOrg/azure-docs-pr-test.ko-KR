---
title: "aaaAzure Active Directory 하이브리드 id 디자인 고려 사항-액세스 제어 요구 사항을 결정 | Microsoft Docs"
description: "덮개 hello 독특하고 id 및 사용자는 하이브리드 환경에 대 한 리소스에 대 한 액세스 요구 사항 확인 합니다."
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
ms.openlocfilehash: f0c22629f732a4c13ee7a24456651bec7637c387
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-access-control-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="cd347-103">하이브리드 ID 솔루션에 대한 액세스 제어 요구 사항 확인</span><span class="sxs-lookup"><span data-stu-id="cd347-103">Determine access control requirements for your hybrid identity solution</span></span>
<span data-ttu-id="cd347-104">이 기회 tooreview 사용할 수도 있습니다는 하이브리드 id 솔루션 toomake를 계획 하는 hello 리소스에 대 한 요구 사항을 확인 조직을 디자인할 때 사용자에 사용할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd347-104">When an organization is designing their hybrid identity solution they can also use this opportunity tooreview access requirements for hello resources that they are planning toomake it available for users.</span></span> <span data-ttu-id="cd347-105">hello 데이터 액세스는 id의 모든 4 개의 독특하고 간:</span><span class="sxs-lookup"><span data-stu-id="cd347-105">hello data access cross all four pillars of identity, which are:</span></span>

* <span data-ttu-id="cd347-106">관리</span><span class="sxs-lookup"><span data-stu-id="cd347-106">Administration</span></span>
* <span data-ttu-id="cd347-107">인증</span><span class="sxs-lookup"><span data-stu-id="cd347-107">Authentication</span></span>
* <span data-ttu-id="cd347-108">권한 부여</span><span class="sxs-lookup"><span data-stu-id="cd347-108">Authorization</span></span>
* <span data-ttu-id="cd347-109">감사</span><span class="sxs-lookup"><span data-stu-id="cd347-109">Auditing</span></span>

<span data-ttu-id="cd347-110">뒤에 오는 hello 섹션에서는 인증 및 권한 부여 자세히 설명, 관리와 감사 hello 하이브리드 identity lifecycle 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd347-110">hello sections that follows will cover authentication and authorization in more details, administration and auditing are part of hello hybrid identity lifecycle.</span></span> <span data-ttu-id="cd347-111">이러한 기능에 대한 자세한 내용은 [하이브리드 ID 관리 작업 결정](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="cd347-111">Read [Determine hybrid identity management tasks](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) for more information about these capabilities.</span></span>

> [!NOTE]
> <span data-ttu-id="cd347-112">읽기 [hello 4 개의 독특하고의 Identity-hello Age의 하이브리드 IT에서에서 Id 관리](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) 이러한 독특하고의 각 노드에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd347-112">Read [hello Four Pillars of Identity - Identity Management in hello Age of Hybrid IT](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) for more information about each one of those pillars.</span></span>
> 
> 

## <a name="authentication-and-authorization"></a><span data-ttu-id="cd347-113">인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="cd347-113">Authentication and authorization</span></span>
<span data-ttu-id="cd347-114">인증 및 권한 부여에 대 한 다양 한 시나리오는, 이러한 시나리오는 hello 회사는 진행 중인 tooadopt hello 하이브리드 id 솔루션에 의해 충족 해야 하는 특정 요구 사항을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="cd347-114">There are different scenarios for authentication and authorization, these scenarios will have specific requirements that must be fulfilled by hello hybrid identity solution that hello company is going tooadopt.</span></span> <span data-ttu-id="cd347-115">비즈니스 tooBusiness (B2B)를 포함 하는 시나리오 통신 추가할 수 추가 챌린지 IT 관리자에 대 한 이후 hello 조직에서 사용 되는 hello 인증 및 권한 부여 방법 비즈니스 파트너와 통신할 수 있는 tooensure 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd347-115">Scenarios involving Business tooBusiness (B2B) communication can add an extra challenge for IT Admins since they will need tooensure that hello authentication and authorization method used by hello organization can communicate with their business partners.</span></span> <span data-ttu-id="cd347-116">인증 및 권한 부여 요구 사항에 대 한 프로세스를 디자인 하는 hello, 하는 동안 해당 hello 다음 질문에 대 한 답변은 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd347-116">During hello designing process for authentication and authorization requirements, ensure that hello following questions are answered:</span></span>

* <span data-ttu-id="cd347-117">조직이 해당 ID 관리 시스템에 있는 사용자만 인증하고 권한을 부여합니까?</span><span class="sxs-lookup"><span data-stu-id="cd347-117">Will your organization authenticate and authorize only users located at their identity management system?</span></span>
  * <span data-ttu-id="cd347-118">B2B 시나리오에 대한 계획이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="cd347-118">Are there any plans for B2B scenarios?</span></span>
  * <span data-ttu-id="cd347-119">그러한 경우 이미 알 수 있는 프로토콜 (SAML, OAuth, Kerberos, 토큰 또는 인증서)는 두 비즈니스 사용된 tooconnect 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="cd347-119">If yes, do you already know which protocols (SAML, OAuth, Kerberos, Tokens or Certificates) will be used tooconnect both businesses?</span></span>
* <span data-ttu-id="cd347-120">Hello 하이브리드 id 솔루션 tooadopt 하려는 이러한 프로토콜을 지원 합니까?</span><span class="sxs-lookup"><span data-stu-id="cd347-120">Does hello hybrid identity solution that you are going tooadopt support those protocols?</span></span>

<span data-ttu-id="cd347-121">또 다른 중요 한 지점을 tooconsider 이며 사용자 및 파트너에서 사용할 hello 인증 리포지토리 배치 될 위치 hello 관리 모델 toobe 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd347-121">Another important point tooconsider is where hello authentication repository that will be used by users and partners will be located and hello administrative model toobe used.</span></span> <span data-ttu-id="cd347-122">다음 두 가지 핵심 옵션 hello를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd347-122">Consider hello following two core options:</span></span>

* <span data-ttu-id="cd347-123">중앙 집중형:이 모델 hello에 사용자의 자격 증명, 정책 및 관리 될 수 있습니다 중앙 집중식된 온-프레미스 또는 클라우드에서 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd347-123">Centralized: in this model hello user’s credentials, policies and administration can be centralized on-premises or in hello cloud.</span></span>
* <span data-ttu-id="cd347-124">하이브리드:이 모델 hello에 사용자의 자격 증명, 정책 및 관리 됩니다 중앙 집중식된 온-프레미스와 복제 hello 클라우드.</span><span class="sxs-lookup"><span data-stu-id="cd347-124">Hybrid: in this model hello user’s credentials, policies and administration will be centralized on-premises and a replicated in hello cloud.</span></span>

<span data-ttu-id="cd347-125">Tooanswer hello를 질문 tooidentify hello id 관리 시스템은 상주 하 고 관리 모드 toouse hello 다음 보겠습니다 조직 채택 하 게 모델 tootheir 비즈니스 요구에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="cd347-125">Which model your organization will adopt will vary according tootheir business requirements, you want tooanswer hello following questions tooidentify where hello identity management system will reside and hello administrative mode toouse:</span></span>

* <span data-ttu-id="cd347-126">현재 조직에는 ID 관리 온-프레미스가 있습니까?</span><span class="sxs-lookup"><span data-stu-id="cd347-126">Does your organization currently have an identity management on-premises?</span></span>
  * <span data-ttu-id="cd347-127">그렇다면 이러한 계획이 tookeep 것?</span><span class="sxs-lookup"><span data-stu-id="cd347-127">If yes, do they plan tookeep it?</span></span>
  * <span data-ttu-id="cd347-128">조직 따라야 해당 규정 hello id 관리 시스템 상주해 야 규정 또는 준수 요구 사항이 있나요?</span><span class="sxs-lookup"><span data-stu-id="cd347-128">Are there any regulation or compliance requirements that your organization must follow that dictates where hello identity management system should reside?</span></span>
* <span data-ttu-id="cd347-129">조직이 사용 하나요 single sign on 있는 앱 온-프레미스 또는 클라우드에서 hello?</span><span class="sxs-lookup"><span data-stu-id="cd347-129">Does your organization use single sign-on for apps located on-premises or in hello cloud?</span></span>
  * <span data-ttu-id="cd347-130">그러한 경우 하이브리드 id 모델의 hello 채택 영향은이 프로세스?</span><span class="sxs-lookup"><span data-stu-id="cd347-130">If yes, does hello adoption of a hybrid identity model affect this process?</span></span>

## <a name="access-control"></a><span data-ttu-id="cd347-131">액세스 제어</span><span class="sxs-lookup"><span data-stu-id="cd347-131">Access Control</span></span>
<span data-ttu-id="cd347-132">인증 및 권한 부여는 사용자의 유효성 검사를 통해 핵심 요소 tooenable 액세스 toocorporate 데이터는 것도 중요 한 toocontrol hello 수준의 액세스는 이러한 사용자는 및 hello 보다 hello 수준의 관리자 액세스를 갖습니다. 관리 하 고 있는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="cd347-132">While authentication and authorization are core elements tooenable access toocorporate data through user’s validation, it is also important toocontrol hello level of access that these users will have and hello level of access administrators will have over hello resources that they are managing.</span></span> <span data-ttu-id="cd347-133">하이브리드 id 솔루션 수 tooprovide 세부적인 액세스 tooresources, 위임 및 역할 기본 액세스를 제어 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd347-133">Your hybrid identity solution must be able tooprovide granular access tooresources, delegation and role base access control.</span></span> <span data-ttu-id="cd347-134">액세스 제어에 관한 질문 뒤 해당 hello 응답을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd347-134">Ensure that hello following question are answered regarding access control:</span></span>

* <span data-ttu-id="cd347-135">회사에는 높은 권한 toomanage 가진 둘 이상의 사용자 id 시스템과?</span><span class="sxs-lookup"><span data-stu-id="cd347-135">Does your company have more than one user with elevated privilege toomanage your identity system?</span></span>
  * <span data-ttu-id="cd347-136">예, 각 사용자 하나요 hello 동일한 액세스 수준?</span><span class="sxs-lookup"><span data-stu-id="cd347-136">If yes, does each user need hello same access level?</span></span>
* <span data-ttu-id="cd347-137">회사 요구 toodelegate 액세스 toousers toomanage 특정 리소스는?</span><span class="sxs-lookup"><span data-stu-id="cd347-137">Would your company need toodelegate access toousers toomanage specific resources?</span></span>
  * <span data-ttu-id="cd347-138">그렇다면 얼마나 자주 발생합니까?</span><span class="sxs-lookup"><span data-stu-id="cd347-138">If yes, how frequently this happens?</span></span>
* <span data-ttu-id="cd347-139">온-프레미스와 클라우드 간 액세스 제어 기능 toointegrate 해야 회사 리소스?</span><span class="sxs-lookup"><span data-stu-id="cd347-139">Would your company need toointegrate access control capabilities between on-premises and cloud resources?</span></span>
* <span data-ttu-id="cd347-140">회사는 toolimit 액세스 tooresources toosome 조건에 따라 필요?</span><span class="sxs-lookup"><span data-stu-id="cd347-140">Would your company need toolimit access tooresources according toosome conditions?</span></span>
* <span data-ttu-id="cd347-141">회사에 사용자 지정 컨트롤 toosome 리소스에 액세스 해야 하는 모든 응용 프로그램에는?</span><span class="sxs-lookup"><span data-stu-id="cd347-141">Would your company have any application that needs custom control access toosome resources?</span></span>
  * <span data-ttu-id="cd347-142">그러한 경우 해당 앱 위치 (온-프레미스 또는 클라우드에서 hello)?</span><span class="sxs-lookup"><span data-stu-id="cd347-142">If yes, where are those apps located (on-premises or in hello cloud)?</span></span>
  * <span data-ttu-id="cd347-143">예, 여기서는 해당 대상으로 배치 된 리소스 (온-프레미스 또는 클라우드에서 hello)?</span><span class="sxs-lookup"><span data-stu-id="cd347-143">If yes, where are those target resources located (on-premises or in hello cloud)?</span></span>

> [!NOTE]
> <span data-ttu-id="cd347-144">각 응답 tootake 메모 있는지를 확인 하 고 hello 응답 hello 도입한 이유를 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd347-144">Make sure tootake notes of each answer and understand hello rationale behind hello answer.</span></span> <span data-ttu-id="cd347-145">[데이터 보호 전략 정의](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) 에서는 hello 사용 가능한 옵션과 각 옵션의 장단점을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="cd347-145">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over hello options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="cd347-146">질문에 답변하여 비즈니스 요구 사항에 가장 적합한 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd347-146">By answering those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="cd347-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cd347-147">Next steps</span></span>
[<span data-ttu-id="cd347-148">사고 대응 요구 사항 결정</span><span class="sxs-lookup"><span data-stu-id="cd347-148">Determine incident response requirements</span></span>](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="see-also"></a><span data-ttu-id="cd347-149">참고 항목</span><span class="sxs-lookup"><span data-stu-id="cd347-149">See Also</span></span>
[<span data-ttu-id="cd347-150">설계 고려 사항 개요</span><span class="sxs-lookup"><span data-stu-id="cd347-150">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

