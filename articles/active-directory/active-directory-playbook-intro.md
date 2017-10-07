---
title: "Active Directory PoC 플레이 북 소개 aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 655524e9692de46e831fc68e1636e6c20d41958f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-introduction"></a><span data-ttu-id="eca3c-104">Azure Active Directory 개념 증명 플레이 북 구성: 소개</span><span class="sxs-lookup"><span data-stu-id="eca3c-104">Azure Active Directory Proof of Concept Playbook: Introduction</span></span>

<span data-ttu-id="eca3c-105">이 문서의 지침 개념 증명 (PoC) tooexplore 다른 Azure AD 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eca3c-105">This article provides guidelines tooexplore different Azure AD capabilities in a Proof of Concept (PoC).</span></span> <span data-ttu-id="eca3c-106">이 문서의 대상 그룹은 Identity 설계자, IT 전문가 및 시스템 통합자 hello 사용</span><span class="sxs-lookup"><span data-stu-id="eca3c-106">hello intended audience of this document is Identity Architects, IT Professionals, and System Integrators</span></span>

## <a name="how-toouse-this-playbook"></a><span data-ttu-id="eca3c-107">어떻게 toouse이 플레이이 북</span><span class="sxs-lookup"><span data-stu-id="eca3c-107">How toouse this Playbook</span></span>

1. <span data-ttu-id="eca3c-108">사용 하 여 hello [테마](active-directory-playbook-ingredients.md#theme) 섹션 하 고 필요에 따라 원하는 hello 영역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eca3c-108">Use hello [Theme](active-directory-playbook-ingredients.md#theme) section and pick hello area(s) of interest based on your needs.</span></span>  
2. <span data-ttu-id="eca3c-109">비즈니스 목표에 맞춰 hello 시나리오를 선택 하 여 hello PoC 범위.</span><span class="sxs-lookup"><span data-stu-id="eca3c-109">Scope hello PoC by choosing hello scenarios that align with your business goals.</span></span> <span data-ttu-id="eca3c-110">hello 더 짧은 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="eca3c-110">hello shorter hello better.</span></span> <span data-ttu-id="eca3c-111">짧은으로 수행 하는 것이 좋습니다 및 가능한 tooconvey hello 값으로 간결한 최소화 하면서 toohello 관련자 hello 복잡성 toorealize 것입니다.</span><span class="sxs-lookup"><span data-stu-id="eca3c-111">We recommend doing it as short and concise as possible tooconvey hello value toohello stakeholders while minimizing hello complexity toorealize it.</span></span>  
3. <span data-ttu-id="eca3c-112">사용 하 여 hello [구현](active-directory-playbook-implementation.md) 섹션 toounderstand hello 시나리오 및 환경에 대 한 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="eca3c-112">Use hello [Implementation](active-directory-playbook-implementation.md) section toounderstand hello scenarios, and what would they mean for your environment.</span></span> <span data-ttu-id="eca3c-113">각 시나리오에서는 설명 방법을 tooset 설정 (주기 [빌딩 블록](active-directory-playbook-building-blocks.md)), 어떻게 toonavigate hello 시나리오 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="eca3c-113">In each scenario, we describe how tooset it up (what we call [Building Blocks](active-directory-playbook-building-blocks.md)), and how toonavigate hello scenarios.</span></span> 
4. <span data-ttu-id="eca3c-114">필요에 따라 hello 필수 구성 요소 뿐만 아니라 대략적인 시간 toocomplete 각 구성 요소에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="eca3c-114">Each building block explains hello pre-requisites needed, as well as an approximate time toocomplete.</span></span> <span data-ttu-id="eca3c-115">이 프로세스를 계획 하는 hello 중 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eca3c-115">This can help you during hello planning process.</span></span> 
5. <span data-ttu-id="eca3c-116">Hello 정의 위의 1-3에 따라, [환경](active-directory-playbook-ingredients.md#environment) 어떤 tooexecute에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eca3c-116">Based on 1-3 Above, define hello [Environment](active-directory-playbook-ingredients.md#environment) in which tooexecute.</span></span> <span data-ttu-id="eca3c-117">프로덕션 환경 tooget hello 프로그램 사용자 경험 좋은 느낌에 대 한 toostrive를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="eca3c-117">We encourage toostrive for a production environment tooget a good feel of hello experience for your users.</span></span> 
6. <span data-ttu-id="eca3c-118">상충하는 요구 사항이 있을 경우 이 유용한 상쇄 매트릭스를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="eca3c-118">When having conflicting requirements, use this helpful tradeoff matrix</span></span> 
   * <span data-ttu-id="eca3c-119">테마 중심의 값 표시</span><span class="sxs-lookup"><span data-stu-id="eca3c-119">Theme-centric showing of value</span></span>  
   * <span data-ttu-id="eca3c-120">다듬기 tooprepare, up, tooset 및 tooexecute hello 시나리오</span><span class="sxs-lookup"><span data-stu-id="eca3c-120">Smoothness tooprepare, tooset up, and tooexecute hello scenarios</span></span> 
   * <span data-ttu-id="eca3c-121">최소 시간 tooexecute hello 대상 시나리오</span><span class="sxs-lookup"><span data-stu-id="eca3c-121">Minimal time tooexecute hello target scenarios</span></span> 
   * <span data-ttu-id="eca3c-122">제약 조건이 배포 내에서 가능한 닫기 tooproduction으로</span><span class="sxs-lookup"><span data-stu-id="eca3c-122">As close tooproduction as feasible within your constraints</span></span> 

>[!NOTE]
> <span data-ttu-id="eca3c-123">이 문서 전체에서는 편의를 위한 예제로 몇 가지 타사 응용 프로그램 및 제품이 제시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eca3c-123">Throughout this article, you will see some specific third party applications and products mentioned as examples for convenience.</span></span> <span data-ttu-id="eca3c-124">Azure AD의 [응용 프로그램 갤러리](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps)에서는 사용자의 요구 및 환경에 따라 사용할 수 있는 수천 개의 응용 프로그램을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="eca3c-124">Azure AD supports thousands of applications in our [application gallery](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) that you can use based on your needs and environment.</span></span> 



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]