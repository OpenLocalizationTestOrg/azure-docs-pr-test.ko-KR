---
title: "Azure CDN 규칙 엔진 조건식 | Microsoft Docs"
description: "Azure CDN 규칙 엔진 일치 조건 및 기능에 대한 참조 설명서"
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 57e56c38e003cb83dcf44f455c4451d159db8a59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cdn-rules-engine-conditional-expressions"></a><span data-ttu-id="f8efc-103">Azure CDN 규칙 엔진 조건식</span><span class="sxs-lookup"><span data-stu-id="f8efc-103">Azure CDN rules engine conditional expressions</span></span>
<span data-ttu-id="f8efc-104">이 항목에서는 Azure CDN(Content Delivery Network) [규칙 엔진](cdn-rules-engine.md)에 대한 조건식에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f8efc-104">This topic lists detailed descriptions of the Conditional Expressions for Azure Content Delivery Network (CDN) [Rules Engine](cdn-rules-engine.md).</span></span>

<span data-ttu-id="f8efc-105">규칙의 첫 번째 부분은 조건식입니다.</span><span class="sxs-lookup"><span data-stu-id="f8efc-105">The first part of a rule is the Conditional Expression.</span></span>

<span data-ttu-id="f8efc-106">조건식</span><span class="sxs-lookup"><span data-stu-id="f8efc-106">Conditional Expression</span></span> | <span data-ttu-id="f8efc-107">설명</span><span class="sxs-lookup"><span data-stu-id="f8efc-107">Description</span></span>
-----------------------|-------------
<span data-ttu-id="f8efc-108">IF</span><span class="sxs-lookup"><span data-stu-id="f8efc-108">IF</span></span> | <span data-ttu-id="f8efc-109">IF 식은 항상 규칙의 첫 번째 문의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="f8efc-109">An IF expression is always a part of the first statement in a rule.</span></span> <span data-ttu-id="f8efc-110">다른 모든 조건식과 마찬가지로 이 IF 문은 일치와 관련이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8efc-110">Like all other conditional expressions, this IF statement must be associated with a match.</span></span> <span data-ttu-id="f8efc-111">추가 조건식이 정의되지 않은 경우 이 일치는 기능 집합이 요청에 적용되기 전에 충족되어야 하는 기준을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8efc-111">If no additional conditional expressions are defined, then this match determines the criterion that must be met before a set of features may be applied to a request.</span></span>
<span data-ttu-id="f8efc-112">AND IF</span><span class="sxs-lookup"><span data-stu-id="f8efc-112">AND IF</span></span> | <span data-ttu-id="f8efc-113">AND IF 식은 IF, AND IF 형식의 조건식 뒤에만 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8efc-113">An AND IF expression may only be added after the following types of conditional expressions:IF,AND IF.</span></span> <span data-ttu-id="f8efc-114">초기 IF 문에 대해 충족되어야 하는 다른 조건이 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f8efc-114">It indicates that there is another condition that must be met for the initial IF statement.</span></span>
<span data-ttu-id="f8efc-115">ELSE IF</span><span class="sxs-lookup"><span data-stu-id="f8efc-115">ELSE IF</span></span>| <span data-ttu-id="f8efc-116">ELSE IF 식은 이 ELSE IF 문과 관련된 기능 집합이 수행되기 전에 충족되어야 하는 대체 조건을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8efc-116">An ELSE IF expression specifies an alternative condition that must be met before a set of features specific to this ELSE IF statement takes place.</span></span> <span data-ttu-id="f8efc-117">ELSE IF 문이 있으면 이전 문의 끝을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f8efc-117">The presence of an ELSE IF statement indicates the end of the previous statement.</span></span> <span data-ttu-id="f8efc-118">ELSE IF 문 다음에 올 수 있는 유일한 조건식은 다른 ELSE IF 문입니다.</span><span class="sxs-lookup"><span data-stu-id="f8efc-118">The only conditional expression that may be placed after an ELSE IF statement is another ELSE IF statement.</span></span> <span data-ttu-id="f8efc-119">즉, ELSE IF 문은 충족해야 하는 단일 추가 조건을 지정하는 데에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8efc-119">This means that an ELSE IF statement may only be used to specify a single additional condition that has to be met.</span></span>

<span data-ttu-id="f8efc-120">**예**: ![CDN 일치 조건](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span><span class="sxs-lookup"><span data-stu-id="f8efc-120">**Example**: ![CDN match condition](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span></span>

 > [!TIP]
   > <span data-ttu-id="f8efc-121">후속 규칙은 이전 규칙에서 지정된 동작을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8efc-121">A subsequent rule may override the actions specified by a previous rule.</span></span> <span data-ttu-id="f8efc-122">예: catch-all 규칙은 토큰 기반 인증을 통해 모든 요청을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="f8efc-122">Example: A catch-all rule secures all requests via Token-Based Authentication.</span></span> <span data-ttu-id="f8efc-123">특정 요청 형식에 대한 예외를 만들기 위해 다른 규칙을 바로 아래에 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8efc-123">Another rule may be created directly below it to make an exception for certain types of requests.</span></span>

### <a name="next-steps"></a><span data-ttu-id="f8efc-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f8efc-124">Next steps</span></span>
* [<span data-ttu-id="f8efc-125">Azure CDN 개요</span><span class="sxs-lookup"><span data-stu-id="f8efc-125">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="f8efc-126">규칙 엔진 참조</span><span class="sxs-lookup"><span data-stu-id="f8efc-126">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="f8efc-127">규칙 엔진 일치 조건</span><span class="sxs-lookup"><span data-stu-id="f8efc-127">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="f8efc-128">규칙 엔진 기능</span><span class="sxs-lookup"><span data-stu-id="f8efc-128">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="f8efc-129">규칙 엔진을 사용하여 기본 HTTP 동작 재정의</span><span class="sxs-lookup"><span data-stu-id="f8efc-129">Overriding default HTTP behavior using the rules engine</span></span>](cdn-rules-engine.md)
