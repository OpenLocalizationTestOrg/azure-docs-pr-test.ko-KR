---
title: "Azure Active Directory 하이브리드 ID 디자인 고려 사항 - Multi-Factor Authentication 요구 사항 확인"
description: "조건부 액세스 제어를 통해 Azure Active Directory는 사용자를 인증할 때 및 응용 프로그램에 대한 액세스를 허용하기 전에 선택한 특정 조건을 확인합니다. 이러한 조건이 충족되면 사용자가 인증되고 응용 프로그램에 대한 액세스가 허용됩니다."
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
ms.openlocfilehash: 5b3a8ce6e4203dfb3700f324e32687dd910118af
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="determine-multi-factor-authentication-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="0f572-104">하이브리드 ID 솔루션에 대한 다단계 인증 요구 사항 확인</span><span class="sxs-lookup"><span data-stu-id="0f572-104">Determine multi-factor authentication requirements for your hybrid identity solution</span></span>
<span data-ttu-id="0f572-105">모바일 시대에서는 사용자가 모든 장치에서 클라우드에 있는 데이터 및 응용 프로그램에 액세스하므로 정보 보호가 가장 중요한 일이 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0f572-105">In this world of mobility, with users accessing data and applications in the cloud and from any device, securing this information has become paramount.</span></span>  <span data-ttu-id="0f572-106">보안 위반에 관한 뉴스 헤드라인이 매일 바뀌고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f572-106">Every day there is a new headline about a security breach.</span></span>  <span data-ttu-id="0f572-107">보안 위반을 완벽하게 방지하는 대책은 없지만, 다단계 인증을 통해 보안 위반을 방지하는 보안을 강화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f572-107">Although, there is no guarantee against such breaches, multi-factor authentication, provides an additional layer of security to help prevent these breaches.</span></span>
<span data-ttu-id="0f572-108">다단계 인증에 대한 조직 요구 사항을 평가하고 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="0f572-108">Start by evaluating the organizations requirements for multi-factor authentication.</span></span> <span data-ttu-id="0f572-109">즉 조직에서 보호하려고 하는 대상이 무엇인지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="0f572-109">That is, what is the organization trying to secure.</span></span>  <span data-ttu-id="0f572-110">이 평가는 조직의 사용자가 다단계 인증을 설정하고 사용할 수 있도록 하는 기술 요구 사항을 정의하기 위해 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="0f572-110">This evaluation is important to define the technical requirements for setting up and enabling the organizations users for multi-factor authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="0f572-111">MFA 및 그 기능에 대해 잘 모르는 경우 이 섹션을 계속하기 전에 [Azure Multi-Factor Authentication이란?](../multi-factor-authentication/multi-factor-authentication.md) 문서를 읽어보는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0f572-111">If you are not familiar with MFA and what it does, it is strongly recommended that you read the article [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) prior to continue reading this section.</span></span>
> 
> 

<span data-ttu-id="0f572-112">다음 질문에 답변하세요.</span><span class="sxs-lookup"><span data-stu-id="0f572-112">Make sure to answer the following:</span></span>

* <span data-ttu-id="0f572-113">회사가 Microsoft 앱을 보호하려고 하나요?</span><span class="sxs-lookup"><span data-stu-id="0f572-113">Is your company trying to secure Microsoft apps?</span></span> 
* <span data-ttu-id="0f572-114">이러한 앱은 어떻게 게시되나요?</span><span class="sxs-lookup"><span data-stu-id="0f572-114">How these apps are published?</span></span>
* <span data-ttu-id="0f572-115">회사에서 직원들이 온-프레미스 앱에 액세스할 수 있도록 원격 액세스를 제공하나요?</span><span class="sxs-lookup"><span data-stu-id="0f572-115">Does your company provide remote access to allow employees to access on-premises apps?</span></span>

<span data-ttu-id="0f572-116">그렇다면 어떤 유형의 원격 액세스를 제공하나요? 또한 이러한 응용 프로그램에 액세스하는 사용자의 위치를 평가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f572-116">If yes, what type of remote access?You also need to evaluate where the users who are accessing these applications will be located.</span></span> <span data-ttu-id="0f572-117">이 평가는 적절한 다단계 인증 전략을 정의하기 위해 또 다른 중요한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="0f572-117">This evaluation is another important step to define the proper multi-factor authentication strategy.</span></span> <span data-ttu-id="0f572-118">다음 질문에 답변하세요.</span><span class="sxs-lookup"><span data-stu-id="0f572-118">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="0f572-119">사용자가 배치될 위치는 어디인가요?</span><span class="sxs-lookup"><span data-stu-id="0f572-119">Where are the users going to be located?</span></span>
* <span data-ttu-id="0f572-120">다른 곳으로 배치할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="0f572-120">Can they be located anywhere?</span></span>
* <span data-ttu-id="0f572-121">회사에서 사용자의 위치에 따른 제한을 설정하려 하나요?</span><span class="sxs-lookup"><span data-stu-id="0f572-121">Does your company want to establish restrictions according to the user’s location?</span></span>

<span data-ttu-id="0f572-122">이러한 요구 사항을 이해했다면 다단계 인증에 대한 사용자의 요구 사항을 평가하는 것도 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="0f572-122">Once you understand these requirements, it is important to also evaluate the user’s requirements for multi-factor authentication.</span></span> <span data-ttu-id="0f572-123">이 평가는 다단계 인증을 롤아웃하기 위한 요구 사항을 정의하므로 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="0f572-123">This evaluation is important because it will define the requirements for rolling out multi-factor authentication.</span></span> <span data-ttu-id="0f572-124">다음 질문에 답변하세요.</span><span class="sxs-lookup"><span data-stu-id="0f572-124">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="0f572-125">사용자가 다단계 인증에 대해 잘 알고 있나요?</span><span class="sxs-lookup"><span data-stu-id="0f572-125">Are the users familiar with multi-factor authentication?</span></span>
* <span data-ttu-id="0f572-126">일부 사용자는 추가 인증을 제공해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="0f572-126">Will some uses be required to provide additional authentication?</span></span>  
  * <span data-ttu-id="0f572-127">그렇다면 외부 네트워크에서 액세스하거나 특정 응용 프로그램에서 액세스하거나 기타 조건에서 액세스하는 경우는 언제인가요?</span><span class="sxs-lookup"><span data-stu-id="0f572-127">If yes, all the time, when coming from external networks, or accessing specific applications, or under other conditions?</span></span>
* <span data-ttu-id="0f572-128">사용자가 다단계 인증 설정 및 구현 방법에 대한 교육을 받아야 하나요?</span><span class="sxs-lookup"><span data-stu-id="0f572-128">Will the users require training on how to setup and implement multi-factor authentication?</span></span>
* <span data-ttu-id="0f572-129">회사에서 사용자가 다단계 인증을 사용할 수 있도록 하려는 주요 시나리오는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="0f572-129">What are the key scenarios that your company wants to enable multi-factor authentication for their users?</span></span>

<span data-ttu-id="0f572-130">이전 질문에 답변한 후 온-프레미스에 다단계 인증이 이미 구현되어 있는지 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f572-130">After answering the previous questions, you will be able to understand if there are multi-factor authentication already implemented on-premises.</span></span> <span data-ttu-id="0f572-131">이 평가는 조직의 사용자가 다단계 인증을 설정하고 사용할 수 있도록 하는 기술 요구 사항을 정의하기 위해 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="0f572-131">This evaluation is important to define the technical requirements for setting up and enabling the organizations users for multi-factor authentication.</span></span> <span data-ttu-id="0f572-132">다음 질문에 답변하세요.</span><span class="sxs-lookup"><span data-stu-id="0f572-132">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="0f572-133">회사에서 MFA로 권한 있는 계정을 보호해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="0f572-133">Does your company need to protect privileged accounts with MFA?</span></span>
* <span data-ttu-id="0f572-134">회사가 규정 준수 상의 이유로 특정 응용 프로그램에 대해 MFA를 사용하도록 설정해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="0f572-134">Does your company need to enable MFA for certain application for compliance reasons?</span></span>
* <span data-ttu-id="0f572-135">회사가 이러한 응용 프로그램에 대해 자격이 있는 모든 사용자에 대해 MFA를 사용하도록 설정해야 하나요, 아니면 관리자에 대해서만 MFA를 사용하도록 설정해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="0f572-135">Does your company need to enable MFA for all eligible users of these application or only administrators?</span></span>
* <span data-ttu-id="0f572-136">MFA를 항상 사용하도록 설정해야 하나요, 아니면 사용자가 회사 네트워크 외부에서 로그인하는 경우에만 사용하도록 설정해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="0f572-136">Do you need have MFA always enabled or only when the users are logged outside of your corporate network?</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f572-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0f572-137">Next steps</span></span>
[<span data-ttu-id="0f572-138">하이브리드 ID 채택 전략 정의</span><span class="sxs-lookup"><span data-stu-id="0f572-138">Define a hybrid identity adoption strategy</span></span>](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)

## <a name="see-also"></a><span data-ttu-id="0f572-139">참고 항목</span><span class="sxs-lookup"><span data-stu-id="0f572-139">See also</span></span>
[<span data-ttu-id="0f572-140">디자인 고려 사항 개요</span><span class="sxs-lookup"><span data-stu-id="0f572-140">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

