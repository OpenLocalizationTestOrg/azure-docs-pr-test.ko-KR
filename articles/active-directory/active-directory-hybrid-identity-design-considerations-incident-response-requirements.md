---
title: "aaaAzure Active Directory 하이브리드 id 디자인 고려 사항-인시던트 rResponse 요구 사항을 결정 | Microsoft Docs"
description: "IT tootake 작업 tooidentify로 이용 될 수 있습니다 및 잠재적인 위협을 완화 하는 hello 하이브리드 id 솔루션에 대 한 모니터링 및 보고 기능을 결정"
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
ms.openlocfilehash: 7084096f318ef461e8331fb6edde1b77d4108466
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-incident-response-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="7b364-103">하이브리드 ID 솔루션에 대한 인시던트 대응 요구 사항 확인</span><span class="sxs-lookup"><span data-stu-id="7b364-103">Determine incident response requirements for your hybrid identity solution</span></span>
<span data-ttu-id="7b364-104">대규모 또는 중간 규모 조직 있을 가능성이 가장 높습니다 됩니다는 [보안 사고 대응](https://technet.microsoft.com/library/cc700825.aspx) 위치 toohelp IT에서에서 작업을 적절 하 게 수행할 인시던트의 toohello 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="7b364-104">Large or medium organizations most likely will have a [security incident response](https://technet.microsoft.com/library/cc700825.aspx) in place toohelp IT take actions accordingly toohello level of incident.</span></span> <span data-ttu-id="7b364-105">hello identity 관리 시스템은 hello 목표에 대해 특정 작업을 수행한 사용자를 식별 하는 사용 되는 toohelp 수 있기 때문에 hello 사고 대응 프로세스에서 중요 한 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="7b364-105">hello identity management system is an important component in hello incident response process because it can be used toohelp identifying who performed a specific action against hello target.</span></span> <span data-ttu-id="7b364-106">hello 하이브리드 id 솔루션 수 tooprovide 모니터링 및 IT tootake 작업 tooidentify로 이용 될 수 하 고 잠재적인 위협을 완화 하는 기능을 보고 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b364-106">hello hybrid identity solution must be able tooprovide monitoring and reporting capabilities that can be leveraged by IT tootake actions tooidentify and mitigate a potential threat.</span></span> <span data-ttu-id="7b364-107">일반적인 사고 대응 계획에 hello hello 계획의 일환으로 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b364-107">In a typical incident response plan you will have hello following phases as part of hello plan:</span></span>

1. <span data-ttu-id="7b364-108">초기 평가.</span><span class="sxs-lookup"><span data-stu-id="7b364-108">Initial assessment.</span></span>
2. <span data-ttu-id="7b364-109">인시던트 통신.</span><span class="sxs-lookup"><span data-stu-id="7b364-109">Incident communication.</span></span>
3. <span data-ttu-id="7b364-110">피해 제어 및 위험 감소.</span><span class="sxs-lookup"><span data-stu-id="7b364-110">Damage control and risk reduction.</span></span>
4. <span data-ttu-id="7b364-111">손상 및 심각도의 식별.</span><span class="sxs-lookup"><span data-stu-id="7b364-111">Identification of what it was compromise and severity.</span></span>
5. <span data-ttu-id="7b364-112">증거 보존.</span><span class="sxs-lookup"><span data-stu-id="7b364-112">Evidence preservation.</span></span>
6. <span data-ttu-id="7b364-113">알림 tooappropriate 당사자입니다.</span><span class="sxs-lookup"><span data-stu-id="7b364-113">Notification tooappropriate parties.</span></span>
7. <span data-ttu-id="7b364-114">시스템 복구.</span><span class="sxs-lookup"><span data-stu-id="7b364-114">System recovery.</span></span>
8. <span data-ttu-id="7b364-115">설명서.</span><span class="sxs-lookup"><span data-stu-id="7b364-115">Documentation.</span></span>
9. <span data-ttu-id="7b364-116">피해 및 비용 평가.</span><span class="sxs-lookup"><span data-stu-id="7b364-116">Damage and cost assessment.</span></span>
10. <span data-ttu-id="7b364-117">프로세스 및 계획 수정.</span><span class="sxs-lookup"><span data-stu-id="7b364-117">Process and plan revision.</span></span>

<span data-ttu-id="7b364-118">어떤 it의 hello 식별 하는 동안 손상 및 심각도 단계를 필요한 tooidentify hello 시스템을 손상 된 파일 액세스 되 고 해당 파일의 hello 중요도 결정 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7b364-118">During hello identification of what it was compromise and severity- phase, it will be necessary tooidentify hello systems that have been compromised, files that have been accessed and determine hello sensitivity of those files.</span></span> <span data-ttu-id="7b364-119">하이브리드 id 시스템과 이러한 요구 사항을 tooassist toofulfill 수 있어야 하면 해당 변경 작업을 수행 하는 hello 사용자 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b364-119">Your hybrid identity system should be able toofulfill these requirements tooassist you identifying hello user that made those changes.</span></span> 

## <a name="monitoring-and-reporting"></a><span data-ttu-id="7b364-120">모니터링 및 보고</span><span class="sxs-lookup"><span data-stu-id="7b364-120">Monitoring and reporting</span></span>
<span data-ttu-id="7b364-121">여러 번 hello id 시스템 hello 시스템의 기본 제공 감사 및 보고 기능을 제공 하는 경우에 주로 초기 평가 단계에서 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b364-121">Many times hello identity system can also help in initial assessment phase mainly if hello system has built in auditing and reporting capabilities.</span></span> <span data-ttu-id="7b364-122">Hello 초기 평가 하는 동안 IT 관리자가 의심 스러운 활동 수 tooidentify 이거나 hello 시스템 미리 구성 된 작업에 따라 자동으로 수 tootrigger 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b364-122">During hello initial assessment, IT Admin must be able tooidentify a suspicious activity, or hello system should be able tootrigger it automatically based on a pre-configured task.</span></span> <span data-ttu-id="7b364-123">다른 경우 시스템이 잘못 구성된 침입 감지 시스템 tooa 수의 거짓 긍정 이어질 수 있지만 많은 활동 공격의 가능성을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b364-123">Many activities could indicate a possible attack, however in other cases, a badly configured system might lead tooa number of false positives in an intrusion detection system.</span></span> 

<span data-ttu-id="7b364-124">hello id 관리 시스템 IT 관리자 tooidentify 지원 하 고 의심 스러운 활동을 보고 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b364-124">hello identity management system should assist IT admins tooidentify and report those suspicious activities.</span></span> <span data-ttu-id="7b364-125">일반적으로 이러한 기술 요구 사항은 모든 시스템을 모니터링하고 잠재적인 위협 요소를 강조 표시할 수 있는 보고 기능에 의해 수행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b364-125">Usually these technical requirements can be fulfilled by monitoring all systems and having a reporting capability that can highlight potential threats.</span></span> <span data-ttu-id="7b364-126">Hello 질문을 사용 하면서 고려 사고 대응 요구 사항으로 하이브리드 id 솔루션을 디자인할 toohelp 아래:</span><span class="sxs-lookup"><span data-stu-id="7b364-126">Use hello questions below toohelp you design your hybrid identity solution while taking into consideration incident response requirements:</span></span>

* <span data-ttu-id="7b364-127">회사는 보안 인시던트 대응에 대비하고 있습니까?</span><span class="sxs-lookup"><span data-stu-id="7b364-127">Does your company has a security incident response in place?</span></span>
  * <span data-ttu-id="7b364-128">예, hello 현재 id 관리 시스템으로 사용 됩니다 hello 프로세스의 일부로?</span><span class="sxs-lookup"><span data-stu-id="7b364-128">If yes, is hello current identity management system used as part of hello process?</span></span>
* <span data-ttu-id="7b364-129">회사 다양 한 장치의 tooidentify 의심 스러운 로그온 시도 사용자 로부터 필요 합니까?</span><span class="sxs-lookup"><span data-stu-id="7b364-129">Does your company need tooidentify suspicious sign-on attempts from users across different devices?</span></span>
* <span data-ttu-id="7b364-130">회사에 toodetect 잠재적인 공격에 노출 된 사용자의 자격 증명이 필요 합니까?</span><span class="sxs-lookup"><span data-stu-id="7b364-130">Does your company need toodetect potential compromised user’s credentials?</span></span>
* <span data-ttu-id="7b364-131">회사는 tooaudit 사용자의 액세스 및 작업에 필요 합니까?</span><span class="sxs-lookup"><span data-stu-id="7b364-131">Does your company need tooaudit user’s access and action?</span></span>
* <span data-ttu-id="7b364-132">사용자 암호를 다시 설정 하는 경우 회사 tooknow에 필요 합니까?</span><span class="sxs-lookup"><span data-stu-id="7b364-132">Does your company need tooknow when a user reset his password?</span></span>

## <a name="policy-enforcement"></a><span data-ttu-id="7b364-133">정책 적용</span><span class="sxs-lookup"><span data-stu-id="7b364-133">Policy enforcement</span></span>
<span data-ttu-id="7b364-134">이 손상 제어 및 위험 감소 단계 동안 tooquickly 공격 hello 실제 및 잠재적 효과가 저하 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b364-134">During damage control and risk reduction-phase, it is important tooquickly reduce hello actual and potential effects of an attack.</span></span> <span data-ttu-id="7b364-135">이 시점에서 수행할 해당 동작 사소한와 심각한 hello 차이 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b364-135">That action that you will take at this point can make hello difference between a minor and a major one.</span></span> <span data-ttu-id="7b364-136">hello 정확한 대응 조직과 hello 공격의의 hello 특성에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="7b364-136">hello exact response will depend on your organization and hello nature of hello attack that you face.</span></span> <span data-ttu-id="7b364-137">Hello 초기 평가 계정을 보안이 손상 된 데이터를 완료 하는 경우이 계정이 tooenforce 정책 tooblock 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b364-137">If hello initial assessment concluded that an account was compromised, you will need tooenforce policy tooblock this account.</span></span> <span data-ttu-id="7b364-138">Hello id 관리 시스템을 활용 하는 예 중 하나일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="7b364-138">That’s just one example where hello identity management system will be leveraged.</span></span> <span data-ttu-id="7b364-139">Tooreact tooan 진행 중인 인시던트 적용 정책 되는 방식을 점을 고려 하는 동안 하이브리드 id 솔루션을 디자인할 toohelp 아래 hello 질문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b364-139">Use hello questions below toohelp you design your hybrid identity solution while taking into consideration how policies will be enforced tooreact tooan ongoing incident:</span></span>

* <span data-ttu-id="7b364-140">회사에에서 한 정책이 있습니까 액세스 hello 네트워크 위치 tooblock 사용자가 필요한 경우?</span><span class="sxs-lookup"><span data-stu-id="7b364-140">Does your company have policies in place tooblock users from access hello network if necessary?</span></span>
  * <span data-ttu-id="7b364-141">그렇다면에 hello 현재 솔루션 통합 hello 하이브리드 id 관리 시스템 하락 tooadopt는?</span><span class="sxs-lookup"><span data-stu-id="7b364-141">If yes, does hello current solution integrate with hello hybrid identity management system that you are going tooadopt?</span></span>
* <span data-ttu-id="7b364-142">회사 격리에 있는 사용자에 대 한 조건부 액세스 tooenforce에 필요 합니까?</span><span class="sxs-lookup"><span data-stu-id="7b364-142">Does your company need tooenforce conditional access for users that are in quarantine?</span></span> 

> [!NOTE]
> <span data-ttu-id="7b364-143">각 응답 tootake 메모 있는지를 확인 하 고 hello 응답 hello 도입한 이유를 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b364-143">Make sure tootake notes of each answer and understand hello rationale behind hello answer.</span></span> <span data-ttu-id="7b364-144">[데이터 보호 전략 정의](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) 에서는 hello 사용 가능한 옵션과 각 옵션의 장단점을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="7b364-144">[Define data protection strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over hello options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="7b364-145">질문에 답변함으로써 비즈니스 요구 사항에 가장 적합한 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b364-145">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="7b364-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7b364-146">Next steps</span></span>
[<span data-ttu-id="7b364-147">데이터 보호 전략 정의</span><span class="sxs-lookup"><span data-stu-id="7b364-147">Define data protection strategy</span></span>](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)

## <a name="see-also"></a><span data-ttu-id="7b364-148">참고 항목</span><span class="sxs-lookup"><span data-stu-id="7b364-148">See Also</span></span>
[<span data-ttu-id="7b364-149">설계 고려 사항 개요</span><span class="sxs-lookup"><span data-stu-id="7b364-149">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

