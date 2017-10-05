---
title: "Azure Active Directory PoC 플레이 북 소개 | Microsoft Docs"
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
ms.openlocfilehash: 567f3373594bc53435e8c0bd0a3445dd318af1cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-introduction"></a><span data-ttu-id="6167b-104">Azure Active Directory 개념 증명 플레이 북 구성: 소개</span><span class="sxs-lookup"><span data-stu-id="6167b-104">Azure Active Directory Proof of Concept Playbook: Introduction</span></span>

<span data-ttu-id="6167b-105">이 문서에서는 PoC(개념 증명)에서 다른 Azure 기능을 탐색하기 위한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6167b-105">This article provides guidelines to explore different Azure AD capabilities in a Proof of Concept (PoC).</span></span> <span data-ttu-id="6167b-106">이 문서의 예상 사용자는 ID 설계자, IT 전문가 및 시스템 통합 업체입니다.</span><span class="sxs-lookup"><span data-stu-id="6167b-106">The intended audience of this document is Identity Architects, IT Professionals, and System Integrators</span></span>

## <a name="how-to-use-this-playbook"></a><span data-ttu-id="6167b-107">이 플레이 북을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="6167b-107">How to use this Playbook</span></span>

1. <span data-ttu-id="6167b-108">[테마](active-directory-playbook-ingredients.md#theme) 섹션을 사용하고 필요에 따라 관심 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6167b-108">Use the [Theme](active-directory-playbook-ingredients.md#theme) section and pick the area(s) of interest based on your needs.</span></span>  
2. <span data-ttu-id="6167b-109">비즈니스 목표에 맞는 시나리오를 선택하여 PoC 범위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6167b-109">Scope the PoC by choosing the scenarios that align with your business goals.</span></span> <span data-ttu-id="6167b-110">짧을수록 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6167b-110">The shorter the better.</span></span> <span data-ttu-id="6167b-111">구현하는 데 필요한 복잡성을 최소화하면서 이해 관계자에게 값을 전달할 수 있도록 가능한 한 짧고 간단하게 유지하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6167b-111">We recommend doing it as short and concise as possible to convey the value to the stakeholders while minimizing the complexity to realize it.</span></span>  
3. <span data-ttu-id="6167b-112">[구현](active-directory-playbook-implementation.md) 섹션을 사용하여 이러한 시나리오와 각 시나리오가 사용자 환경에 어떤 의미를 갖는지 이해하세요.</span><span class="sxs-lookup"><span data-stu-id="6167b-112">Use the [Implementation](active-directory-playbook-implementation.md) section to understand the scenarios, and what would they mean for your environment.</span></span> <span data-ttu-id="6167b-113">각 시나리오에서 설정 방법([구성 요소](active-directory-playbook-building-blocks.md)) 및 시나리오 탐색 방법이 설명됩니다.</span><span class="sxs-lookup"><span data-stu-id="6167b-113">In each scenario, we describe how to set it up (what we call [Building Blocks](active-directory-playbook-building-blocks.md)), and how to navigate the scenarios.</span></span> 
4. <span data-ttu-id="6167b-114">각 구성 요소는 완료하는 데 드는 대략적인 시간 뿐만 아니라 필수 전제 조건도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6167b-114">Each building block explains the pre-requisites needed, as well as an approximate time to complete.</span></span> <span data-ttu-id="6167b-115">이를 통해 계획하는 데 도움을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6167b-115">This can help you during the planning process.</span></span> 
5. <span data-ttu-id="6167b-116">위의 1-3에 따라 실행할 [환경](active-directory-playbook-ingredients.md#environment)을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6167b-116">Based on 1-3 Above, define the [Environment](active-directory-playbook-ingredients.md#environment) in which to execute.</span></span> <span data-ttu-id="6167b-117">사용자가 환경에 대해 좋은 평가를 내릴 수 있도록 적절한 프로덕션 환경을 제공하기 위해 노력하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6167b-117">We encourage to strive for a production environment to get a good feel of the experience for your users.</span></span> 
6. <span data-ttu-id="6167b-118">상충하는 요구 사항이 있을 경우 이 유용한 상쇄 매트릭스를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="6167b-118">When having conflicting requirements, use this helpful tradeoff matrix</span></span> 
   * <span data-ttu-id="6167b-119">테마 중심의 값 표시</span><span class="sxs-lookup"><span data-stu-id="6167b-119">Theme-centric showing of value</span></span>  
   * <span data-ttu-id="6167b-120">원활하게 시나리오를 준비, 설정 및 실행할 수 있는 효율성</span><span class="sxs-lookup"><span data-stu-id="6167b-120">Smoothness to prepare, to set up, and to execute the scenarios</span></span> 
   * <span data-ttu-id="6167b-121">대상 시나리오를 실행하는 데 소요되는 최소 시간</span><span class="sxs-lookup"><span data-stu-id="6167b-121">Minimal time to execute the target scenarios</span></span> 
   * <span data-ttu-id="6167b-122">제약 조건에도 불구하고 최대한 프로덕션에 가깝게 구현</span><span class="sxs-lookup"><span data-stu-id="6167b-122">As close to production as feasible within your constraints</span></span> 

>[!NOTE]
> <span data-ttu-id="6167b-123">이 문서 전체에서는 편의를 위한 예제로 몇 가지 타사 응용 프로그램 및 제품이 제시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6167b-123">Throughout this article, you will see some specific third party applications and products mentioned as examples for convenience.</span></span> <span data-ttu-id="6167b-124">Azure AD의 [응용 프로그램 갤러리](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps)에서는 사용자의 요구 및 환경에 따라 사용할 수 있는 수천 개의 응용 프로그램을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6167b-124">Azure AD supports thousands of applications in our [application gallery](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) that you can use based on your needs and environment.</span></span> 



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]