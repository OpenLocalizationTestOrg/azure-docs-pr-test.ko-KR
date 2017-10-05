---
title: "Azure Active Directory PoC 플레이 북 구성 | Microsoft Docs"
description: "ID 및 액세스 관리 시나리오를 탐색하고 신속하게 구현"
services: active-directory
keywords: "Azure Active Directory, 플레이 북, 개념 증명, PoC"
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: d2a0fe280f143d390f5e4ba40e0ebe92d8a4a837
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a><span data-ttu-id="fac1e-104">Azure Active Directory 개념 증명 플레이 북 구성</span><span class="sxs-lookup"><span data-stu-id="fac1e-104">Azure Active Directory Proof of Concept Playbook Ingredients</span></span> 

## <a name="theme"></a><span data-ttu-id="fac1e-105">테마</span><span class="sxs-lookup"><span data-stu-id="fac1e-105">Theme</span></span>
<span data-ttu-id="fac1e-106">Azure AD는 기업의 여러 영역에서 ID 및 액세스 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fac1e-106">Azure AD provides identity and access solutions across multiple areas in the enterprise.</span></span> <span data-ttu-id="fac1e-107">해당 시나리오를 다음 영역으로 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fac1e-107">We classify the scenarios in the following areas:</span></span> 

* [<span data-ttu-id="fac1e-108">다수의 앱, 하나의 ID</span><span class="sxs-lookup"><span data-stu-id="fac1e-108">Lots of apps, one identity</span></span>](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [<span data-ttu-id="fac1e-109">보안 향상</span><span class="sxs-lookup"><span data-stu-id="fac1e-109">Increase your security</span></span>](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [<span data-ttu-id="fac1e-110">셀프 서비스에 맞게 크기 조정</span><span class="sxs-lookup"><span data-stu-id="fac1e-110">Scale with Self Service</span></span>](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

<span data-ttu-id="fac1e-111">PoC를 규정하는 테마를 정의하면 비즈니스 목표에 맞게 노력을 집중하도록 하는 데 도움이 되며, 처음부터 개념 증명에 관심이 생길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fac1e-111">Defining a theme to frame the PoC helps to focus the efforts that resonates with business goals, which oftentimes are the triggers of the interest in a proof of concept in the first place.</span></span> 

## <a name="environment"></a><span data-ttu-id="fac1e-112">Environment</span><span class="sxs-lookup"><span data-stu-id="fac1e-112">Environment</span></span>

<span data-ttu-id="fac1e-113">PoC를 전달하는 환경의 세부 정보를 확인하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="fac1e-113">It is important to determine the details of the environment where you will deliver the PoC.</span></span> <span data-ttu-id="fac1e-114">이상적으로는 PoC가 완료된 후에 환경을 구축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fac1e-114">Ideally you can build upon it after the PoC is completed.</span></span> <span data-ttu-id="fac1e-115">목표 환경은 중요하며, 가능한 한 실제와 같이 유지하면서도 제약이나 추가 고려 사항에 따른 오버헤드를 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac1e-115">The target environment is crucial and you should find the right balance between making it as real as possible and the overhead of constraints or extra considerations.</span></span> <span data-ttu-id="fac1e-116">PoC에 대한 일반적인 환경은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fac1e-116">The typical environments for PoCs are:</span></span>
* <span data-ttu-id="fac1e-117">**프로덕션:** 시나리오가 라이브 환경에서 구현되며, 이미 Microsoft 클라우드 서비스(프로덕션 AD, Office 365, Azure AD 테넌트/SSO 솔루션)가 배포되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fac1e-117">**Production:** The scenarios will be implemented in your live environment and already deployed Microsoft Cloud services (production AD, Office 365, Azure AD tenant/SSO solution).</span></span> 
* <span data-ttu-id="fac1e-118">**UAT(사용자 수용 테스트)/개발 환경:** 프로덕션과 유사한 테스트 데이터를 포함하는 테스트 인프라(병렬 AD 및 잠재적으로 Azure AD 테넌트/SSO 솔루션)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fac1e-118">**User Acceptance Test (UAT)/Dev environment:** You have test infrastructure (parallel AD and potentially Azure AD tenant/SSO solution) with test data that resembles production.</span></span> <span data-ttu-id="fac1e-119">일반적으로 테스트 환경은 엔터프라이즈의 여러 프로젝트 간에 공유됩니다.</span><span class="sxs-lookup"><span data-stu-id="fac1e-119">Typically, the test environment is shared across multiple projects in the enterprise.</span></span>

<span data-ttu-id="fac1e-120">이 가이드의 시나리오 대부분은 기본적으로 추가가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="fac1e-120">Most scenarios in this guide are additive in nature.</span></span> <span data-ttu-id="fac1e-121">따라서 PoC 외부 사용자에게 영향을 주지 않으면서 프로덕션 테넌트에 배포될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fac1e-121">As a result, they can be deployed in the production tenant without affecting users outside the PoC.</span></span> <span data-ttu-id="fac1e-122">이 문서 전체에서는 테넌트 차원에서 영향을 미치는 시나리오를 살펴볼 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fac1e-122">Throughout this document, we will be calling out which scenarios would have tenant-wide effect.</span></span> <span data-ttu-id="fac1e-123">이러한 경우 프로덕션이 아닌 환경을 고려하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fac1e-123">In those cases, you might want to consider a non-production environment.</span></span> 


## <a name="target-users"></a><span data-ttu-id="fac1e-124">대상 사용자</span><span class="sxs-lookup"><span data-stu-id="fac1e-124">Target Users</span></span>

<span data-ttu-id="fac1e-125">시나리오를 연습할 대상 사용자 집합을 결정하는 것이 중요합니다. 이 작업은 환경이 프로덕션 또는 테스트 환경일 때 특히 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="fac1e-125">It is important to determine the target set of users that will exercise the scenarios, especially when the environment is production or test.</span></span> <span data-ttu-id="fac1e-126">PoC에 대한 대상 사용자 범주는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fac1e-126">The categories of target users for PoC are:</span></span>
* <span data-ttu-id="fac1e-127">**파일럿 사용자:** 당일 작업을 수행하기 위해 해당 하루 동안 사용하는 계정으로 솔루션을 사용하게 되는 환경의 실제 사용자</span><span class="sxs-lookup"><span data-stu-id="fac1e-127">**Pilot Users:** Real users in the environment that will be using the solution with the account they use for their day to day job functions</span></span>
* <span data-ttu-id="fac1e-128">**테스트 사용자:** 환경에서 생성된 테스트 계정</span><span class="sxs-lookup"><span data-stu-id="fac1e-128">**Test Users:** Test accounts created in the environment</span></span> 

<span data-ttu-id="fac1e-129">이 가이드의 시나리오 대부분은 파일럿 사용자가 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fac1e-129">Most scenarios in this guide can be exercised by pilot users.</span></span> <span data-ttu-id="fac1e-130">이 문서 전체에서는 필요할 때 대상 사용자 고려 사항을 언급합니다.</span><span class="sxs-lookup"><span data-stu-id="fac1e-130">Throughout this document, we will be calling out target user considerations if needed.</span></span>


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]