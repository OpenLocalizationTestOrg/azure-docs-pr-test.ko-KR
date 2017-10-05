---
title: "Azure Active Directory 하이브리드 ID 디자인 고려 사항 - 하이브리드 ID 관리 작업 | Microsoft Docs"
description: "조건부 액세스 제어를 통해 Azure Active Directory는 사용자를 인증할 때 및 응용 프로그램에 대한 액세스를 허용하기 전에 선택한 특정 조건을 확인합니다. 이러한 조건이 충족되면 사용자가 인증되고 응용 프로그램에 대한 액세스가 허용됩니다."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 65f80aea-0426-4072-83e1-faf5b76df034
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 921c8391fc18eca35d10c3ade158a98ae88df397
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="plan-for-hybrid-identity-lifecycle"></a><span data-ttu-id="03ad4-104">하이브리드 ID 수명 주기에 대한 계획</span><span class="sxs-lookup"><span data-stu-id="03ad4-104">Plan for Hybrid Identity Lifecycle</span></span>
<span data-ttu-id="03ad4-105">ID는 엔터프라이즈 이동성 및 응용 프로그램 액세스 전략의 토대 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="03ad4-105">Identity is one of the foundations of your enterprise mobility and application access strategy.</span></span> <span data-ttu-id="03ad4-106">모바일 장치 또는 SaaS 앱에 로그인하는지와 무관하게 ID는 모든 항목에 액세스를 얻는 키입니다.</span><span class="sxs-lookup"><span data-stu-id="03ad4-106">Whether you are signing on to your mobile device or SaaS app, your identity is the key to gaining access to everything.</span></span> <span data-ttu-id="03ad4-107">가장 높은 수준에서 ID 관리 솔루션은 프로비전한 리소스의 프로세스를 자동화하고 중앙 집중화를 포함하는 ID 리포지토리 간의 통합 및 동기화를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="03ad4-107">At its highest level, an identity management solution encompasses unifying and syncing between your identity repositories which includes automating and centralizing the process of provisioning resources.</span></span> <span data-ttu-id="03ad4-108">ID 솔루션은 온-프레미스 및 클라우드 전반에서 중앙 집중화된 ID여야 하며 특정 형태의 ID 페더레이션을 사용하여 중앙 집중된 인증을 유지 관리하고 외부 사용자 및 비즈니스와 안전하게 공유하며 협력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03ad4-108">The identity solution should be a centralized identity across on-premises and cloud and also use some form of identity federation to maintain centralized authentication and securely share and collaborate with external users and businesses.</span></span> <span data-ttu-id="03ad4-109">리소스의 범위는 운영 체제 및 응용 프로그램에서 사용자에 걸쳐 있거나 조직에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03ad4-109">Resources range from operating systems and applications to people in, or affiliated with, an organization.</span></span> <span data-ttu-id="03ad4-110">조직 구조는 프로비전하는 정책 및 절차를 수용하기 위해 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03ad4-110">Organizational structure can be altered to accommodate the provisioning policies and procedures.</span></span>

<span data-ttu-id="03ad4-111">또한 사용자가 생산성을 유지하도록 하기 위해 셀프 서비스 경험을 제공하는 역량을 강화하도록 설계된 ID 솔루션이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03ad4-111">It is also important to have an identity solution geared to empower your users by providing them with self-service experiences to keep them productive.</span></span> <span data-ttu-id="03ad4-112">ID 솔루션이 액세스하는 데 필요한 모든 리소스에 걸쳐 사용자에 대한 Single Sign-On을 사용할 수 있도록 하는 경우 더욱 강력합니다.</span><span class="sxs-lookup"><span data-stu-id="03ad4-112">Your identity solution is more robust if it enables single sign-on for users across all the resources they need access Administrators at all levels can use standardized procedures for managing user credentials.</span></span> <span data-ttu-id="03ad4-113">모든 수준의 관리자는 사용자 자격 증명을 관리하기 위한 표준화된 절차를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03ad4-113">Some levels of administration can be reduced or eliminated, depending on the breadth of the provisioning management solution.</span></span> <span data-ttu-id="03ad4-114">관리의 일부 수준이 프로비전 관리 솔루션의 너비에 따라 감소하거나 제거될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03ad4-114">Furthermore, you can securely distribute administration capabilities, manually or automatically, among various organizations.</span></span> <span data-ttu-id="03ad4-115">또한 수동 또는 자동으로, 다양한 조직 간에 관리 기능을 안전하게 배포할 수 있습니다  예를 들어 도메인 관리자는 해당 도메인의 사용자 및 리소스를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03ad4-115">For example, a domain administrator can serve only the people and resources in that domain.</span></span> <span data-ttu-id="03ad4-116">이 사용자는 관리 및 프로비전 작업을 수행할 수 있지만 워크플로 만들기와 같은 구성 작업을 수행할 수 있는 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="03ad4-116">This user can do administrative and provisioning tasks, but is not authorized to do configuration tasks, such as creating workflows.</span></span>

## <a name="determine-hybrid-identity-management-tasks"></a><span data-ttu-id="03ad4-117">하이브리드 ID 관리 작업 결정</span><span class="sxs-lookup"><span data-stu-id="03ad4-117">Determine Hybrid Identity Management Tasks</span></span>
<span data-ttu-id="03ad4-118">조직에서 관리 작업을 배포하면 관리의 정확성 및 효율성이 향상되고 조직의 워크로드 균형을 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="03ad4-118">Distributing administrative tasks in your organization improves the accuracy and effectiveness of administration and improves the balance of the workload of an organization.</span></span> <span data-ttu-id="03ad4-119">다음은 강력한 ID 관리 시스템을 정의하는 피벗입니다.</span><span class="sxs-lookup"><span data-stu-id="03ad4-119">Following are the pivots that define a robust identity management system.</span></span>

 ![](./media/hybrid-id-design-considerations/Identity_management_considerations.png)

<span data-ttu-id="03ad4-120">하이브리드 ID 관리 작업을 정의하려면 하이브리드 ID를 채택하는 조직의 필수 특징 일부를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03ad4-120">To define hybrid identity management tasks, you must understand some essential characteristics of the organization that will be adopting hybrid identity.</span></span> <span data-ttu-id="03ad4-121">ID 원본에 사용되는 현재 리포지토리를 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="03ad4-121">It is important to understand the current repositories being used for identity sources.</span></span> <span data-ttu-id="03ad4-122">이러한 핵심 요소를 파악하여 기본적인 요구 사항을 얻고 이를 기반으로 ID 솔루션에 대한 더 나은 설계를 결정하게 할 수 있는 보다 세부적인 질문을 던져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03ad4-122">By knowing those core elements, you will have the foundational requirements and based on that you will need to ask more granular questions that will lead you to a better design decision for your Identity solution.</span></span>  

<span data-ttu-id="03ad4-123">이러한 요구 사항을 정의하는 동안 적어도 다음 질문에 대답하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="03ad4-123">While defining those requirements, ensure that at least the following questions are answered</span></span>

* <span data-ttu-id="03ad4-124">프로비전 옵션:</span><span class="sxs-lookup"><span data-stu-id="03ad4-124">Provisioning options:</span></span> 
  
  * <span data-ttu-id="03ad4-125">하이브리드 ID 솔루션이 강력한 계정 액세스 관리 및 프로비전 시스템을 지원합니까?</span><span class="sxs-lookup"><span data-stu-id="03ad4-125">Does the hybrid identity solution support a robust account access management and provisioning system?</span></span>
  * <span data-ttu-id="03ad4-126">사용자, 그룹 및 암호를 관리하는 방법은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="03ad4-126">How are users, groups, and passwords going to be managed?</span></span>
  * <span data-ttu-id="03ad4-127">ID 수명 주기 관리는 응답 속도가 빠릅니까?</span><span class="sxs-lookup"><span data-stu-id="03ad4-127">Is the identity lifecycle management responsive?</span></span> 
    * <span data-ttu-id="03ad4-128">암호 업데이트 계정을 일시 중단하는 데 시간이 얼마나 걸립니까?</span><span class="sxs-lookup"><span data-stu-id="03ad4-128">How long does password updates account suspension take?</span></span>
* <span data-ttu-id="03ad4-129">라이선스 관리:</span><span class="sxs-lookup"><span data-stu-id="03ad4-129">License management:</span></span> 
  
  * <span data-ttu-id="03ad4-130">하이브리드 ID 솔루션은 라이선스 관리를 처리합니까?</span><span class="sxs-lookup"><span data-stu-id="03ad4-130">Does the hybrid identity solution handles license management?</span></span>
    * <span data-ttu-id="03ad4-131">그렇다면 어떤 기능을 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="03ad4-131">If yes, what capabilities are available?</span></span>
* <span data-ttu-id="03ad4-132">솔루션은 그룹 기반 라이선스 관리를 처리합니까?</span><span class="sxs-lookup"><span data-stu-id="03ad4-132">Does the solution handle group-based license management?</span></span> 
  
      - <span data-ttu-id="03ad4-133">그렇다면 보안 그룹을 할당할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="03ad4-133">If yes, is it possible to assign a security group to it?</span></span> 
       - <span data-ttu-id="03ad4-134">그렇다면 클라우드 디렉터리가 자동으로 그룹의 모든 멤버에게 라이선스를 할당합니까?</span><span class="sxs-lookup"><span data-stu-id="03ad4-134">If yes, will the cloud directory automatically assign licenses to all the members of the group?</span></span> 
        - <span data-ttu-id="03ad4-135">사용자가 이후에 추가되거나 그룹에서 제거되는 경우 어떻게 됩니까, 라이선스가 자동으로 할당되거나 적절하게 제거됩니까?</span><span class="sxs-lookup"><span data-stu-id="03ad4-135">What happens if a user is subsequently added to, or removed from the group, will a license be automatically assigned or removed as appropriate?</span></span> 
* <span data-ttu-id="03ad4-136">다른 타사 ID 공급자와 통합:</span><span class="sxs-lookup"><span data-stu-id="03ad4-136">Integration with other third-party identity providers:</span></span>
* <span data-ttu-id="03ad4-137">이 하이브리드 솔루션은 타사 ID 공급자와 통합되어 Single Sign-On을 구현할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="03ad4-137">Can this hybrid solution be integrated with third-party identity providers to implement single sign-on?</span></span>
* <span data-ttu-id="03ad4-138">다른 ID 공급자를 모두 통합된 ID 시스템에 통합할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="03ad4-138">Is it possible to unify all the different identity providers into a cohesive identity system?</span></span>
* <span data-ttu-id="03ad4-139">그렇다면 공급자의 종류 및 상태는 어떠하며 어떤 기능을 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="03ad4-139">If yes, how and which are they and what capabilities are available?</span></span>

## <a name="synchronization-management"></a><span data-ttu-id="03ad4-140">동기화 관리</span><span class="sxs-lookup"><span data-stu-id="03ad4-140">Synchronization Management</span></span>
<span data-ttu-id="03ad4-141">ID 관리자의 목표 중 하나는 모든 ID 공급자를 가져오고 동기화 상태를 유지할 수 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="03ad4-141">One of the goals of an identity manager, to be able to bring all the identity providers and keep them synchronized.</span></span> <span data-ttu-id="03ad4-142">권한이 있는 마스터 ID 공급자에 기반하여 데이터 동기화를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="03ad4-142">You keep the data synchronized based on an authoritative master identity provider.</span></span> <span data-ttu-id="03ad4-143">동기화된 관리 모델을 사용하는 하이브리드 ID 시나리오에서 온-프레미스 서버에 있는 모든 사용자 및 장치 ID를 관리하고 계정 및 필요에 따라 암호를 클라우드로 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="03ad4-143">In a hybrid identity scenario, with a synchronized management model, you manage all user and device identities in an on-premises server and synchronize the accounts and, optionally, passwords to the cloud.</span></span> <span data-ttu-id="03ad4-144">로그인에서 사용자는 클라우드에서 입력한 동일한 온-프레미스 암호를 입력하고 암호는 ID 솔루션에서 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="03ad4-144">The user enters the same password on-premises as he or she does in the cloud, and at sign-in, the password is verified by the identity solution.</span></span> <span data-ttu-id="03ad4-145">이 모델은 디렉터리 동기화 도구를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="03ad4-145">This model uses a directory synchronization tool.</span></span>

<span data-ttu-id="03ad4-146">![](./media/hybrid-id-design-considerations/Directory_synchronization.png) 하이브리드 ID 솔루션의 동기화를 적절히 설계하려면 다음 질문에 대답하도록 합니다. • 하이브리드 ID 솔루션에 사용할 수 있는 동기화 솔루션은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="03ad4-146">![](./media/hybrid-id-design-considerations/Directory_synchronization.png) To proper design the synchronization of your hybrid identity solution ensure that the following questions are answered: •    What are the sync solutions available for the hybrid identity solution?</span></span>
<span data-ttu-id="03ad4-147">• 사용할 수는 Single sign-on 기능은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="03ad4-147">•    What are the single sign on capabilities available?</span></span>
<span data-ttu-id="03ad4-148">• B2B 및 B2C 간의 ID 페더레이션에 대한 옵션은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="03ad4-148">•    What are the options for identity federation between B2B and B2C?</span></span>

## <a name="next-steps"></a><span data-ttu-id="03ad4-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="03ad4-149">Next steps</span></span>
[<span data-ttu-id="03ad4-150">하이브리드 ID 관리 채택 전략 결정</span><span class="sxs-lookup"><span data-stu-id="03ad4-150">Determine hybrid identity management adoption strategy</span></span>](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md)

## <a name="see-also"></a><span data-ttu-id="03ad4-151">참고 항목</span><span class="sxs-lookup"><span data-stu-id="03ad4-151">See Also</span></span>
[<span data-ttu-id="03ad4-152">설계 고려 사항 개요</span><span class="sxs-lookup"><span data-stu-id="03ad4-152">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

