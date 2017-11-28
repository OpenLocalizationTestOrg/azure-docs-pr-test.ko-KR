---
title: "aaaAzure Active Directory 하이브리드 id 디자인 고려 사항-다단계 인증 요구 사항 결정"
description: "조건부 액세스 제어를 통해 Azure Active Directory hello 사용자를 인증할 때 및 toohello 응용 프로그램 액세스를 허용 하기 전에 선택 hello 특정 상태를 확인 합니다. 이러한 조건이 충족 되 면 hello 사용자가 인증 되 고 toohello 응용 프로그램 액세스를 허용 합니다."
documentationcenter: 
services: active-directory
author: femila
manager: billmath
editor: 
ms.assetid: 9c59fda9-47d0-4c7e-b3e7-3575c29beabe
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 49fa7b43772fb3a2d6664747477c60a34cddde2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-multi-factor-authentication-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="229f0-104">하이브리드 ID 솔루션에 대한 다단계 인증 요구 사항 확인</span><span class="sxs-lookup"><span data-stu-id="229f0-104">Determine multi-factor authentication requirements for your hybrid identity solution</span></span>
<span data-ttu-id="229f0-105">서비스의 데이터와 hello 클라우드 및 모든 장치에서 응용 프로그램에 액세스 하는 사용자와 mobility이 세계에서에서이 정보 보호 꽉 였습니다.</span><span class="sxs-lookup"><span data-stu-id="229f0-105">In this world of mobility, with users accessing data and applications in hello cloud and from any device, securing this information has become paramount.</span></span>  <span data-ttu-id="229f0-106">보안 위반에 관한 뉴스 헤드라인이 매일 바뀌고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="229f0-106">Every day there is a new headline about a security breach.</span></span>  <span data-ttu-id="229f0-107">Multi-factor authentication은 추가적인 계층을 제공 하지만 이러한 위반에 대 한 보장이 없으므로, toohelp 보안 이러한 위반을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="229f0-107">Although, there is no guarantee against such breaches, multi-factor authentication, provides an additional layer of security toohelp prevent these breaches.</span></span>
<span data-ttu-id="229f0-108">Multi-factor authentication에 대해 hello 조직 요구 사항을 평가 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="229f0-108">Start by evaluating hello organizations requirements for multi-factor authentication.</span></span> <span data-ttu-id="229f0-109">즉, hello 조직 동안 toosecure 란 합니다.</span><span class="sxs-lookup"><span data-stu-id="229f0-109">That is, what is hello organization trying toosecure.</span></span>  <span data-ttu-id="229f0-110">이 평가 중요 한 toodefine hello 기술 요구 사항에 설정 및 hello 조직 사용자가 multi-factor authentication을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="229f0-110">This evaluation is important toodefine hello technical requirements for setting up and enabling hello organizations users for multi-factor authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="229f0-111">MFA 및 그 기능에 익숙한 경우이 가장 좋습니다 hello 문서를 읽기 [Azure Multi-factor Authentication 이란?](../multi-factor-authentication/multi-factor-authentication.md) 이전 toocontinue이이 섹션을 읽기입니다.</span><span class="sxs-lookup"><span data-stu-id="229f0-111">If you are not familiar with MFA and what it does, it is strongly recommended that you read hello article [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) prior toocontinue reading this section.</span></span>
> 
> 

<span data-ttu-id="229f0-112">있는지 tooanswer hello 다음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="229f0-112">Make sure tooanswer hello following:</span></span>

* <span data-ttu-id="229f0-113">회사는 toosecure Microsoft 앱 시도?</span><span class="sxs-lookup"><span data-stu-id="229f0-113">Is your company trying toosecure Microsoft apps?</span></span> 
* <span data-ttu-id="229f0-114">이러한 앱은 어떻게 게시되나요?</span><span class="sxs-lookup"><span data-stu-id="229f0-114">How these apps are published?</span></span>
* <span data-ttu-id="229f0-115">회사에서 제공 하는 원격 액세스 tooallow 직원 tooaccess 온-프레미스 앱</span><span class="sxs-lookup"><span data-stu-id="229f0-115">Does your company provide remote access tooallow employees tooaccess on-premises apps?</span></span>

<span data-ttu-id="229f0-116">그렇다면 어떤 유형의 원격 액세스? 이러한 응용 프로그램에 액세스 하는 hello 사용자가 배치할 tooevaluate를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="229f0-116">If yes, what type of remote access?You also need tooevaluate where hello users who are accessing these applications will be located.</span></span> <span data-ttu-id="229f0-117">이 평가 또 다른 중요 한 단계 toodefine hello 적절 한 다단계 인증 전략입니다.</span><span class="sxs-lookup"><span data-stu-id="229f0-117">This evaluation is another important step toodefine hello proper multi-factor authentication strategy.</span></span> <span data-ttu-id="229f0-118">다음 질문 있는지 tooanswer hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="229f0-118">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="229f0-119">Toobe 라인으로 전환 하는 hello 사용자는 어디에 있습니까?</span><span class="sxs-lookup"><span data-stu-id="229f0-119">Where are hello users going toobe located?</span></span>
* <span data-ttu-id="229f0-120">다른 곳으로 배치할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="229f0-120">Can they be located anywhere?</span></span>
* <span data-ttu-id="229f0-121">회사는 toohello 사용자의 위치에 따라 tooestablish 제한 않으려고?</span><span class="sxs-lookup"><span data-stu-id="229f0-121">Does your company want tooestablish restrictions according toohello user’s location?</span></span>

<span data-ttu-id="229f0-122">이러한 요구 사항을 이해 하면 유용 tooalso 다단계 인증에 대 한 hello 사용자의 요구 사항을 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="229f0-122">Once you understand these requirements, it is important tooalso evaluate hello user’s requirements for multi-factor authentication.</span></span> <span data-ttu-id="229f0-123">Multi-factor authentication이 출시에 대 한 hello 요구 사항 정의이 평가 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="229f0-123">This evaluation is important because it will define hello requirements for rolling out multi-factor authentication.</span></span> <span data-ttu-id="229f0-124">다음 질문 있는지 tooanswer hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="229f0-124">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="229f0-125">익숙한 hello 사용자가 multi-factor authentication?</span><span class="sxs-lookup"><span data-stu-id="229f0-125">Are hello users familiar with multi-factor authentication?</span></span>
* <span data-ttu-id="229f0-126">몇 가지 사용 필요한 tooprovide 추가 인증 됩니까?</span><span class="sxs-lookup"><span data-stu-id="229f0-126">Will some uses be required tooprovide additional authentication?</span></span>  
  * <span data-ttu-id="229f0-127">그러한 경우 모든 hello 시간, 외부 네트워크 또는 특정 응용 프로그램에 액세스, 또는 다른 조건 하면?</span><span class="sxs-lookup"><span data-stu-id="229f0-127">If yes, all hello time, when coming from external networks, or accessing specific applications, or under other conditions?</span></span>
* <span data-ttu-id="229f0-128">Hello 사용자가 방법에 대 한 학습 해야 toosetup 및 구현 multi-factor authentication?</span><span class="sxs-lookup"><span data-stu-id="229f0-128">Will hello users require training on how toosetup and implement multi-factor authentication?</span></span>
* <span data-ttu-id="229f0-129">Hello 주요 시나리오에 사는 사용자에 게 tooenable multi-factor authentication 이란?</span><span class="sxs-lookup"><span data-stu-id="229f0-129">What are hello key scenarios that your company wants tooenable multi-factor authentication for their users?</span></span>

<span data-ttu-id="229f0-130">Hello 위의 질문에 답변 한 후 multi-factor authentication이 이미 구현 되어 온-프레미스에 있는 경우 수 toounderstand 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="229f0-130">After answering hello previous questions, you will be able toounderstand if there are multi-factor authentication already implemented on-premises.</span></span> <span data-ttu-id="229f0-131">이 평가 중요 한 toodefine hello 기술 요구 사항에 설정 및 hello 조직 사용자가 multi-factor authentication을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="229f0-131">This evaluation is important toodefine hello technical requirements for setting up and enabling hello organizations users for multi-factor authentication.</span></span> <span data-ttu-id="229f0-132">다음 질문 있는지 tooanswer hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="229f0-132">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="229f0-133">Mfa tooprotect 특권 계정 회사에 필요 합니까?</span><span class="sxs-lookup"><span data-stu-id="229f0-133">Does your company need tooprotect privileged accounts with MFA?</span></span>
* <span data-ttu-id="229f0-134">회사에 필요 합니까 tooenable MFA 특정 응용 프로그램 규정 준수 상의 이유로?</span><span class="sxs-lookup"><span data-stu-id="229f0-134">Does your company need tooenable MFA for certain application for compliance reasons?</span></span>
* <span data-ttu-id="229f0-135">회사의 이러한 응용 프로그램 또는 관리자만 적합 한 모든 사용자에 대 한 MFA tooenable에 필요 합니까?</span><span class="sxs-lookup"><span data-stu-id="229f0-135">Does your company need tooenable MFA for all eligible users of these application or only administrators?</span></span>
* <span data-ttu-id="229f0-136">필요한 MFA 항상 사용 하도록 설정 또는 있습니까 hello 사용자가 회사 네트워크 외부에 기록 되는 경우에?</span><span class="sxs-lookup"><span data-stu-id="229f0-136">Do you need have MFA always enabled or only when hello users are logged outside of your corporate network?</span></span>

## <a name="next-steps"></a><span data-ttu-id="229f0-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="229f0-137">Next steps</span></span>
[<span data-ttu-id="229f0-138">하이브리드 ID 채택 전략 정의</span><span class="sxs-lookup"><span data-stu-id="229f0-138">Define a hybrid identity adoption strategy</span></span>](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)

## <a name="see-also"></a><span data-ttu-id="229f0-139">참고 항목</span><span class="sxs-lookup"><span data-stu-id="229f0-139">See also</span></span>
[<span data-ttu-id="229f0-140">디자인 고려 사항 개요</span><span class="sxs-lookup"><span data-stu-id="229f0-140">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

