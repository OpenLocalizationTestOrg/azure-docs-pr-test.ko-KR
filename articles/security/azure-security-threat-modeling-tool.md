---
title: "Microsoft 위협 모델링 도구 - Azure | Microsoft Docs"
description: "도구를 시작하는 정보 및 위협 모델링 프로세스를 포함하는 Microsoft 위협 모델링 도구에 대한 기본 페이지"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 6e26b0af2a16a872c8e02b736e24019b47ed5780
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="microsoft-threat-modeling-tool"></a><span data-ttu-id="4f0e6-103">Microsoft 위협 모델링 도구</span><span class="sxs-lookup"><span data-stu-id="4f0e6-103">Microsoft Threat Modeling Tool</span></span>

<span data-ttu-id="4f0e6-104">위협 모델링 도구는 Microsoft SDL(Security Development Lifecycle)의 핵심 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="4f0e6-104">The Threat Modeling Tool is a core element of the Microsoft Security Development Lifecycle (SDL).</span></span> <span data-ttu-id="4f0e6-105">소프트웨어 설계자는 이 도구를 사용하여 비교적 쉽고 비용 효과적으로 문제를 해결할 수 있는 조기에 잠재적인 보안 문제를 식별하고 완화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f0e6-105">It allows software architects to identify and mitigate potential security issues early, when they are relatively easy and cost-effective to resolve.</span></span> <span data-ttu-id="4f0e6-106">결과적으로 전체 개발 비용이 크게 절감됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f0e6-106">As a result, it greatly reduces the total cost of development.</span></span> <span data-ttu-id="4f0e6-107">또한 보안 전문가가 아닌 사용자를 염두에 두고 개발되었으므로 위협 모델을 만들고 분석하기 위한 정확한 지침을 제공하여 모든 개발자가 쉽게 위협 모델링을 수행할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f0e6-107">Also, we designed the tool with non-security experts in mind, making threat modeling easier for all developers by providing clear guidance on creating and analyzing threat models.</span></span> 

<span data-ttu-id="4f0e6-108">이 도구를 사용하면 누구나 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f0e6-108">The tool enables anyone to:</span></span>

* <span data-ttu-id="4f0e6-109">시스템의 보안 설계에 대한 기본 사항 전달</span><span class="sxs-lookup"><span data-stu-id="4f0e6-109">Communicate about the security design of their systems</span></span>
* <span data-ttu-id="4f0e6-110">입증된 방법을 사용하여 이러한 설계의 잠재적인 보안 문제 분석</span><span class="sxs-lookup"><span data-stu-id="4f0e6-110">Analyze those designs for potential security issues using a proven methodology</span></span>
* <span data-ttu-id="4f0e6-111">보안 문제에 대한 해결 방법 제안 및 관리</span><span class="sxs-lookup"><span data-stu-id="4f0e6-111">Suggest and manage mitigations for security issues</span></span>

<span data-ttu-id="4f0e6-112">일부 도구 기능 및 혁신 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4f0e6-112">Here are some tooling capabilities and innovations, just to name a few:</span></span>

* <span data-ttu-id="4f0e6-113">**자동화:** 모형 그리기에 대한 지침 및 피드백</span><span class="sxs-lookup"><span data-stu-id="4f0e6-113">**Automation:** Guidance and feedback in drawing a model</span></span>
* <span data-ttu-id="4f0e6-114">**요소 기준 STRIDE:** 위협 및 해결 방법에 대한 단계별 분석</span><span class="sxs-lookup"><span data-stu-id="4f0e6-114">**STRIDE per Element:** Guided analysis of threats and mitigations</span></span>
* <span data-ttu-id="4f0e6-115">**보고:** 확인 단계의 보안 작업 및 테스트</span><span class="sxs-lookup"><span data-stu-id="4f0e6-115">**Reporting:** Security activities and testing in the verification phase</span></span>
* <span data-ttu-id="4f0e6-116">**고유한 방법:** 위협을 보다 잘 시각화하고 이해하도록 지원</span><span class="sxs-lookup"><span data-stu-id="4f0e6-116">**Unique Methodology:** Enables users to better visualize and understand threats</span></span>
* <span data-ttu-id="4f0e6-117">**소프트웨어 중심의 개발자를 위한 설계:** 많은 접근 방식이 자산 또는 공격자에 주안점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="4f0e6-117">**Designed for Developers and Centered on Software:** many approaches are centered on assets or attackers.</span></span> <span data-ttu-id="4f0e6-118">Microsoft는 소프트웨어 중심 방식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4f0e6-118">We are centered on software.</span></span> <span data-ttu-id="4f0e6-119">소프트웨어 아키텍처에 대한 그림 그리기와 같이 모든 소프트웨어 개발자와 설계자에게 친숙한 작업을 토대로 기능을 구현하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f0e6-119">We build on activities that all software developers and architects are familiar with -- such as drawing pictures for their software architecture</span></span>
* <span data-ttu-id="4f0e6-120">**설계 분석에 주력:** "위협 모델링"이라는 용어는 요구 사항 또는 설계 분석 기법을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f0e6-120">**Focused on Design Analysis:** The term "threat modeling" can refer to either a requirements or a design analysis technique.</span></span> <span data-ttu-id="4f0e6-121">경우에 따라 두 가지가 복잡하게 혼합된 경우를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="4f0e6-121">Sometimes, it refers to a complex blend of the two.</span></span> <span data-ttu-id="4f0e6-122">Microsoft SDL의 위협 모델링 방법은 설계 분석 기법에 초점을 맞춥니다.</span><span class="sxs-lookup"><span data-stu-id="4f0e6-122">The Microsoft SDL approach to threat modeling is a focused design analysis technique</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f0e6-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4f0e6-123">Next steps</span></span>

<span data-ttu-id="4f0e6-124">아래 표는 위협 모델링 도구를 시작하는 데 중요한 링크를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4f0e6-124">The table below contains important links to get you started with the Threat Modeling Tool:</span></span>

| <span data-ttu-id="4f0e6-125">단계</span><span class="sxs-lookup"><span data-stu-id="4f0e6-125">Step</span></span>  | <span data-ttu-id="4f0e6-126">설명</span><span class="sxs-lookup"><span data-stu-id="4f0e6-126">Description</span></span>                                                                                   |
| ----- | --------------------------------------------------------------------------------------------- |
| <span data-ttu-id="4f0e6-127">**1**</span><span class="sxs-lookup"><span data-stu-id="4f0e6-127">**1**</span></span> | [<span data-ttu-id="4f0e6-128">위협 모델링 도구 다운로드</span><span class="sxs-lookup"><span data-stu-id="4f0e6-128">Download the Threat Modeling Tool</span></span>](https://aka.ms/tmtpreview)                                |
| <span data-ttu-id="4f0e6-129">**2**</span><span class="sxs-lookup"><span data-stu-id="4f0e6-129">**2**</span></span> | [<span data-ttu-id="4f0e6-130">시작 가이드 읽기</span><span class="sxs-lookup"><span data-stu-id="4f0e6-130">Read Our getting started guide</span></span>](./azure-security-threat-modeling-tool-getting-started.md)    |
| <span data-ttu-id="4f0e6-131">**3**</span><span class="sxs-lookup"><span data-stu-id="4f0e6-131">**3**</span></span> | [<span data-ttu-id="4f0e6-132">기능 익히기</span><span class="sxs-lookup"><span data-stu-id="4f0e6-132">Get familiar with the features</span></span>](./azure-security-threat-modeling-tool-feature-overview.md)   |
| <span data-ttu-id="4f0e6-133">**4**</span><span class="sxs-lookup"><span data-stu-id="4f0e6-133">**4**</span></span> | [<span data-ttu-id="4f0e6-134">생성된 위협 범주에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="4f0e6-134">Learn about generated threat categories</span></span>](./azure-security-threat-modeling-tool-threats.md)   |
| <span data-ttu-id="4f0e6-135">**5**</span><span class="sxs-lookup"><span data-stu-id="4f0e6-135">**5**</span></span> | [<span data-ttu-id="4f0e6-136">생성된 위협에 대한 해결 방법 찾기</span><span class="sxs-lookup"><span data-stu-id="4f0e6-136">Find mitigations to generated threats</span></span>](./azure-security-threat-modeling-tool-mitigations.md) |

## <a name="resources"></a><span data-ttu-id="4f0e6-137">리소스</span><span class="sxs-lookup"><span data-stu-id="4f0e6-137">Resources</span></span>

<span data-ttu-id="4f0e6-138">위협 모델링에 여전히 관련이 있는 몇 가지 이전 문서는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4f0e6-138">Here are a few older articles still relevant to threat modeling today:</span></span>

* [<span data-ttu-id="4f0e6-139">위협 모델링의 중요성에 대한 문서</span><span class="sxs-lookup"><span data-stu-id="4f0e6-139">Article on the Importance of Threat Modeling</span></span>](https://msdn.microsoft.com/magazine/dd347831.aspx)
* [<span data-ttu-id="4f0e6-140">신뢰할 수 있는 컴퓨팅으로 게시된 학습</span><span class="sxs-lookup"><span data-stu-id="4f0e6-140">Training Published by Trustworthy Computing</span></span>](https://www.microsoft.com/download/details.aspx?id=16420)

<span data-ttu-id="4f0e6-141">몇 가지 위협 모델링 도구 전문가가 수행한 작업을 확인해 보세요.</span><span class="sxs-lookup"><span data-stu-id="4f0e6-141">Check out what a few Threat Modeling Tool experts have done:</span></span>

* [<span data-ttu-id="4f0e6-142">위협 관리자</span><span class="sxs-lookup"><span data-stu-id="4f0e6-142">Threats Manager</span></span>](https://simoneonsecurity.com/threatsmanagersetup-v1-5-10/)
* [<span data-ttu-id="4f0e6-143">Simone Curzi 보안 블로그</span><span class="sxs-lookup"><span data-stu-id="4f0e6-143">Simone Curzi Security Blog</span></span>](https://simoneonsecurity.com/)