---
title: "Azure Active Directory 하이브리드 ID 설계 고려 사항 - 인시던트 응답 요구 사항 확인 | Microsoft Docs"
description: "IT에서 활용할 수 있는 하이브리드 ID 솔루션에 대한 모니터링 및 보고 기능을 확인하여 잠재적인 위협을 식별하고 완화하는 작업을 수행합니다."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: a3d2a459-599b-4b67-8e51-7369ee25082d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 536071ec61d093af243bfd42faa6bb404172fb8e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="determine-incident-response-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="4d843-103">하이브리드 ID 솔루션에 대한 인시던트 대응 요구 사항 확인</span><span class="sxs-lookup"><span data-stu-id="4d843-103">Determine incident response requirements for your hybrid identity solution</span></span>
<span data-ttu-id="4d843-104">대규모 또는 중간 규모 조직에서는 대개 [보안 인시던트 대응](https://technet.microsoft.com/library/cc700825.aspx) 을 준비하여 IT가 인시던트의 수준에 따라 동작을 취합니다.</span><span class="sxs-lookup"><span data-stu-id="4d843-104">Large or medium organizations most likely will have a [security incident response](https://technet.microsoft.com/library/cc700825.aspx) in place to help IT take actions accordingly to the level of incident.</span></span> <span data-ttu-id="4d843-105">ID 관리 시스템은 대상에 대해 특정 동작을 수행한 사용자를 식별하는 데 사용될 수 있기 때문에 인시던트 대응 프로세스에서 중요한 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="4d843-105">The identity management system is an important component in the incident response process because it can be used to help identifying who performed a specific action against the target.</span></span> <span data-ttu-id="4d843-106">하이브리드 ID 솔루션은 IT에서 활용할 수 있는 모니터링 및 보고 기능을 제공하여 잠재적인 위협을 식별하고 완화하는 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d843-106">The hybrid identity solution must be able to provide monitoring and reporting capabilities that can be leveraged by IT to take actions to identify and mitigate a potential threat.</span></span> <span data-ttu-id="4d843-107">일반적인 인시던트 대응 계획에서 계획의 일부를 다음과 같은 단계로 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d843-107">In a typical incident response plan you will have the following phases as part of the plan:</span></span>

1. <span data-ttu-id="4d843-108">초기 평가.</span><span class="sxs-lookup"><span data-stu-id="4d843-108">Initial assessment.</span></span>
2. <span data-ttu-id="4d843-109">인시던트 통신.</span><span class="sxs-lookup"><span data-stu-id="4d843-109">Incident communication.</span></span>
3. <span data-ttu-id="4d843-110">피해 제어 및 위험 감소.</span><span class="sxs-lookup"><span data-stu-id="4d843-110">Damage control and risk reduction.</span></span>
4. <span data-ttu-id="4d843-111">손상 및 심각도의 식별.</span><span class="sxs-lookup"><span data-stu-id="4d843-111">Identification of what it was compromise and severity.</span></span>
5. <span data-ttu-id="4d843-112">증거 보존.</span><span class="sxs-lookup"><span data-stu-id="4d843-112">Evidence preservation.</span></span>
6. <span data-ttu-id="4d843-113">적절한 당사자에 알림.</span><span class="sxs-lookup"><span data-stu-id="4d843-113">Notification to appropriate parties.</span></span>
7. <span data-ttu-id="4d843-114">시스템 복구.</span><span class="sxs-lookup"><span data-stu-id="4d843-114">System recovery.</span></span>
8. <span data-ttu-id="4d843-115">설명서.</span><span class="sxs-lookup"><span data-stu-id="4d843-115">Documentation.</span></span>
9. <span data-ttu-id="4d843-116">피해 및 비용 평가.</span><span class="sxs-lookup"><span data-stu-id="4d843-116">Damage and cost assessment.</span></span>
10. <span data-ttu-id="4d843-117">프로세스 및 계획 수정.</span><span class="sxs-lookup"><span data-stu-id="4d843-117">Process and plan revision.</span></span>

<span data-ttu-id="4d843-118">손상 및 심각도의 식별 단계 중에 손상된 시스템, 액세스된 파일을 식별하고 해당 파일의 중요도를 결정할 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d843-118">During the identification of what it was compromise and severity- phase, it will be necessary to identify the systems that have been compromised, files that have been accessed and determine the sensitivity of those files.</span></span> <span data-ttu-id="4d843-119">하이브리드 ID 시스템은 이러한 요구 사항을 충족하여 해당 변경을 수행한 사용자를 식별하는 데 도움이 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d843-119">Your hybrid identity system should be able to fulfill these requirements to assist you identifying the user that made those changes.</span></span> 

## <a name="monitoring-and-reporting"></a><span data-ttu-id="4d843-120">모니터링 및 보고</span><span class="sxs-lookup"><span data-stu-id="4d843-120">Monitoring and reporting</span></span>
<span data-ttu-id="4d843-121">또한 시스템이 기본 제공 감사 및 보고 기능을 제공하는 경우 ID 시스템은 주로 초기 평가 단계에서 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d843-121">Many times the identity system can also help in initial assessment phase mainly if the system has built in auditing and reporting capabilities.</span></span> <span data-ttu-id="4d843-122">초기 평가 중에 IT 관리자가 의심스러운 활동을 식별할 수 있거나 시스템이 미리 구성된 작업에 기초하여 자동으로 트리거할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d843-122">During the initial assessment, IT Admin must be able to identify a suspicious activity, or the system should be able to trigger it automatically based on a pre-configured task.</span></span> <span data-ttu-id="4d843-123">작업이 많다는 점은 공격의 가능성을 나타낼 수 있지만 다른 경우에 잘못 구성된 시스템 때문에 침입 감지 시스템에서 거짓 긍정을 이끌어낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d843-123">Many activities could indicate a possible attack, however in other cases, a badly configured system might lead to a number of false positives in an intrusion detection system.</span></span> 

<span data-ttu-id="4d843-124">ID서 관리 시스템은 IT 관리자를 도와 해당하는 의심스러운 활동을 식별하고 보고해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d843-124">The identity management system should assist IT admins to identify and report those suspicious activities.</span></span> <span data-ttu-id="4d843-125">일반적으로 이러한 기술 요구 사항은 모든 시스템을 모니터링하고 잠재적인 위협 요소를 강조 표시할 수 있는 보고 기능에 의해 수행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d843-125">Usually these technical requirements can be fulfilled by monitoring all systems and having a reporting capability that can highlight potential threats.</span></span> <span data-ttu-id="4d843-126">인시던트 대응 요구 사항을 고려하는 동안 아래의 질문을 사용하여 하이브리드 ID 솔루션을 설계하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d843-126">Use the questions below to help you design your hybrid identity solution while taking into consideration incident response requirements:</span></span>

* <span data-ttu-id="4d843-127">회사는 보안 인시던트 대응에 대비하고 있습니까?</span><span class="sxs-lookup"><span data-stu-id="4d843-127">Does your company has a security incident response in place?</span></span>
  * <span data-ttu-id="4d843-128">그렇다면 현재 ID 관리 시스템이 프로세스의 일부로 사용됩니까?</span><span class="sxs-lookup"><span data-stu-id="4d843-128">If yes, is the current identity management system used as part of the process?</span></span>
* <span data-ttu-id="4d843-129">회사가 다른 장치에서 사용자의 의심스러운 로그인 시도를 식별해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="4d843-129">Does your company need to identify suspicious sign-on attempts from users across different devices?</span></span>
* <span data-ttu-id="4d843-130">회사가 잠재적으로 공격에 노출된 사용자의 자격 증명을 검색해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="4d843-130">Does your company need to detect potential compromised user’s credentials?</span></span>
* <span data-ttu-id="4d843-131">회사가 사용자의 액세스 및 동작을 감사해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="4d843-131">Does your company need to audit user’s access and action?</span></span>
* <span data-ttu-id="4d843-132">사용자가 자신의 암호를 재설정하는 경우 회사가 알아야 합니까?</span><span class="sxs-lookup"><span data-stu-id="4d843-132">Does your company need to know when a user reset his password?</span></span>

## <a name="policy-enforcement"></a><span data-ttu-id="4d843-133">정책 적용</span><span class="sxs-lookup"><span data-stu-id="4d843-133">Policy enforcement</span></span>
<span data-ttu-id="4d843-134">손상 제어 및 위험 감소 단계 동안 잠재적 공격의 실제 및 잠재적인 영향을 신속하게 줄이는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="4d843-134">During damage control and risk reduction-phase, it is important to quickly reduce the actual and potential effects of an attack.</span></span> <span data-ttu-id="4d843-135">이 시점에서 수행할 동작은 주 및 부 동작 간의 차이를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d843-135">That action that you will take at this point can make the difference between a minor and a major one.</span></span> <span data-ttu-id="4d843-136">정확한 대응은 조직 및 직면하는 공격의 특성에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="4d843-136">The exact response will depend on your organization and the nature of the attack that you face.</span></span> <span data-ttu-id="4d843-137">초기 평가에서 계정이 손상되었다고 결론을 얻은 경우 이 계정을 차단하는 정책을 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d843-137">If the initial assessment concluded that an account was compromised, you will need to enforce policy to block this account.</span></span> <span data-ttu-id="4d843-138">ID 관리 시스템이 활용되는 하나의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="4d843-138">That’s just one example where the identity management system will be leveraged.</span></span> <span data-ttu-id="4d843-139">진행 중인 인시던트에 반응하기 위해 정책이 어떻게 적용될지를 고려하는 동안 아래의 질문을 사용하여 하이브리드 ID 솔루션을 설계하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d843-139">Use the questions below to help you design your hybrid identity solution while taking into consideration how policies will be enforced to react to an ongoing incident:</span></span>

* <span data-ttu-id="4d843-140">필요한 경우 회사가 네트워크 액세스에서 사용자를 블록하는 정책이 준비되어 있습니까?</span><span class="sxs-lookup"><span data-stu-id="4d843-140">Does your company have policies in place to block users from access the network if necessary?</span></span>
  * <span data-ttu-id="4d843-141">그렇다면 현재 솔루션이 채택하려는 하이브리드 ID 관리 시스템과 통합됩니까?</span><span class="sxs-lookup"><span data-stu-id="4d843-141">If yes, does the current solution integrate with the hybrid identity management system that you are going to adopt?</span></span>
* <span data-ttu-id="4d843-142">회사가 격리된 사용자에 대해 조건부 액세스를 적용해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="4d843-142">Does your company need to enforce conditional access for users that are in quarantine?</span></span> 

> [!NOTE]
> <span data-ttu-id="4d843-143">각 답변을 주목하고 답변 이유를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d843-143">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="4d843-144">[데이터 보호 전략 정의](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) 에서는 사용할 수 있는 옵션과 각 옵션의 장점/단점을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="4d843-144">[Define data protection strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over the options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="4d843-145">질문에 답변함으로써 비즈니스 요구 사항에 가장 적합한 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d843-145">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4d843-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4d843-146">Next steps</span></span>
[<span data-ttu-id="4d843-147">데이터 보호 전략 정의</span><span class="sxs-lookup"><span data-stu-id="4d843-147">Define data protection strategy</span></span>](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)

## <a name="see-also"></a><span data-ttu-id="4d843-148">참고 항목</span><span class="sxs-lookup"><span data-stu-id="4d843-148">See Also</span></span>
[<span data-ttu-id="4d843-149">설계 고려 사항 개요</span><span class="sxs-lookup"><span data-stu-id="4d843-149">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

