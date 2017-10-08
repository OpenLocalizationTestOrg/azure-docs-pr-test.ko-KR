---
title: "aaaMicrosoft 위협 모델링 도구-Azure | Microsoft Docs"
description: "Microsoft 위협 모델링 도구를 hello 위협 모델링 프로세스를 포함 하 여 hello 도구로 시작에 대 한 정보가 포함 된 hello에 대 한 기본 페이지"
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
ms.openlocfilehash: 923225a30c592ffdb1d254000451cfaac54a0e68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool"></a><span data-ttu-id="33f82-103">Microsoft 위협 모델링 도구</span><span class="sxs-lookup"><span data-stu-id="33f82-103">Microsoft Threat Modeling Tool</span></span>

<span data-ttu-id="33f82-104">hello 위협 모델링 도구에는 hello Microsoft SDL Security Development Lifecycle ()의 핵심 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="33f82-104">hello Threat Modeling Tool is a core element of hello Microsoft Security Development Lifecycle (SDL).</span></span> <span data-ttu-id="33f82-105">소프트웨어를 통해 tooidentify 만드는 일 및 상대적으로 간편 하 고 비용 효율적인 tooresolve 있을 때 잠재적 보안 문제를 조기에 완화 합니다.</span><span class="sxs-lookup"><span data-stu-id="33f82-105">It allows software architects tooidentify and mitigate potential security issues early, when they are relatively easy and cost-effective tooresolve.</span></span> <span data-ttu-id="33f82-106">결과적으로, 개발의 hello 총 비용이 크게 감소합니다.</span><span class="sxs-lookup"><span data-stu-id="33f82-106">As a result, it greatly reduces hello total cost of development.</span></span> <span data-ttu-id="33f82-107">또한 hello 도구를 보다 쉽게 위협 모델링에 대 한 모든 개발자가 작성 및 위협 모델 분석에 명확한 지침을 제공 하 여을 염두에 비보안 전문가 함께 설계 합니다.</span><span class="sxs-lookup"><span data-stu-id="33f82-107">Also, we designed hello tool with non-security experts in mind, making threat modeling easier for all developers by providing clear guidance on creating and analyzing threat models.</span></span> 

<span data-ttu-id="33f82-108">hello 도구를 사용 하면 다른 사람에 게:</span><span class="sxs-lookup"><span data-stu-id="33f82-108">hello tool enables anyone to:</span></span>

* <span data-ttu-id="33f82-109">시스템의 보안 설계 hello에 대 한 통신</span><span class="sxs-lookup"><span data-stu-id="33f82-109">Communicate about hello security design of their systems</span></span>
* <span data-ttu-id="33f82-110">입증된 방법을 사용하여 이러한 설계의 잠재적인 보안 문제 분석</span><span class="sxs-lookup"><span data-stu-id="33f82-110">Analyze those designs for potential security issues using a proven methodology</span></span>
* <span data-ttu-id="33f82-111">보안 문제에 대한 해결 방법 제안 및 관리</span><span class="sxs-lookup"><span data-stu-id="33f82-111">Suggest and manage mitigations for security issues</span></span>

<span data-ttu-id="33f82-112">다음은 몇 가지 도구 기능과 혁신적인 기술을 정당한 tooname 몇:</span><span class="sxs-lookup"><span data-stu-id="33f82-112">Here are some tooling capabilities and innovations, just tooname a few:</span></span>

* <span data-ttu-id="33f82-113">**자동화:** 모형 그리기에 대한 지침 및 피드백</span><span class="sxs-lookup"><span data-stu-id="33f82-113">**Automation:** Guidance and feedback in drawing a model</span></span>
* <span data-ttu-id="33f82-114">**요소 기준 STRIDE:** 위협 및 해결 방법에 대한 단계별 분석</span><span class="sxs-lookup"><span data-stu-id="33f82-114">**STRIDE per Element:** Guided analysis of threats and mitigations</span></span>
* <span data-ttu-id="33f82-115">**보고:** 보안 활동과 hello 검증 단계에서 테스트</span><span class="sxs-lookup"><span data-stu-id="33f82-115">**Reporting:** Security activities and testing in hello verification phase</span></span>
* <span data-ttu-id="33f82-116">**고유 방법론:** 사용 하면 사용자가 toobetter 파악 하 고 위협 이해</span><span class="sxs-lookup"><span data-stu-id="33f82-116">**Unique Methodology:** Enables users toobetter visualize and understand threats</span></span>
* <span data-ttu-id="33f82-117">**소프트웨어 중심의 개발자를 위한 설계:** 많은 접근 방식이 자산 또는 공격자에 주안점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="33f82-117">**Designed for Developers and Centered on Software:** many approaches are centered on assets or attackers.</span></span> <span data-ttu-id="33f82-118">Microsoft는 소프트웨어 중심 방식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="33f82-118">We are centered on software.</span></span> <span data-ttu-id="33f82-119">소프트웨어 아키텍처에 대한 그림 그리기와 같이 모든 소프트웨어 개발자와 설계자에게 친숙한 작업을 토대로 기능을 구현하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33f82-119">We build on activities that all software developers and architects are familiar with -- such as drawing pictures for their software architecture</span></span>
* <span data-ttu-id="33f82-120">**디자인 분석에 초점을 맞춘:** hello 용어 "위협 모델링"는 요구 사항 또는 디자인 분석 기술 tooeither를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33f82-120">**Focused on Design Analysis:** hello term "threat modeling" can refer tooeither a requirements or a design analysis technique.</span></span> <span data-ttu-id="33f82-121">경우에 따라 두 hello의 복잡 한 혼합 tooa 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="33f82-121">Sometimes, it refers tooa complex blend of hello two.</span></span> <span data-ttu-id="33f82-122">hello Microsoft SDL 접근 방식을 toothreat 모델링은 포커스가 있는 디자인 분석 방법</span><span class="sxs-lookup"><span data-stu-id="33f82-122">hello Microsoft SDL approach toothreat modeling is a focused design analysis technique</span></span>

## <a name="next-steps"></a><span data-ttu-id="33f82-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="33f82-123">Next steps</span></span>

<span data-ttu-id="33f82-124">hello 아래 표에서 중요 링크 tooget hello 위협 모델링 도구를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="33f82-124">hello table below contains important links tooget you started with hello Threat Modeling Tool:</span></span>

| <span data-ttu-id="33f82-125">단계</span><span class="sxs-lookup"><span data-stu-id="33f82-125">Step</span></span>  | <span data-ttu-id="33f82-126">설명</span><span class="sxs-lookup"><span data-stu-id="33f82-126">Description</span></span>                                                                                   |
| ----- | --------------------------------------------------------------------------------------------- |
| <span data-ttu-id="33f82-127">**1**</span><span class="sxs-lookup"><span data-stu-id="33f82-127">**1**</span></span> | [<span data-ttu-id="33f82-128">Hello 위협 모델링 도구를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="33f82-128">Download hello Threat Modeling Tool</span></span>](https://aka.ms/tmtpreview)                                |
| <span data-ttu-id="33f82-129">**2**</span><span class="sxs-lookup"><span data-stu-id="33f82-129">**2**</span></span> | [<span data-ttu-id="33f82-130">시작 가이드 읽기</span><span class="sxs-lookup"><span data-stu-id="33f82-130">Read Our getting started guide</span></span>](./azure-security-threat-modeling-tool-getting-started.md)    |
| <span data-ttu-id="33f82-131">**3**</span><span class="sxs-lookup"><span data-stu-id="33f82-131">**3**</span></span> | [<span data-ttu-id="33f82-132">Hello 기능에 알아보세요</span><span class="sxs-lookup"><span data-stu-id="33f82-132">Get familiar with hello features</span></span>](./azure-security-threat-modeling-tool-feature-overview.md)   |
| <span data-ttu-id="33f82-133">**4**</span><span class="sxs-lookup"><span data-stu-id="33f82-133">**4**</span></span> | [<span data-ttu-id="33f82-134">생성된 위협 범주에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="33f82-134">Learn about generated threat categories</span></span>](./azure-security-threat-modeling-tool-threats.md)   |
| <span data-ttu-id="33f82-135">**5**</span><span class="sxs-lookup"><span data-stu-id="33f82-135">**5**</span></span> | [<span data-ttu-id="33f82-136">Toogenerated 위협 완화 찾기</span><span class="sxs-lookup"><span data-stu-id="33f82-136">Find mitigations toogenerated threats</span></span>](./azure-security-threat-modeling-tool-mitigations.md) |

## <a name="resources"></a><span data-ttu-id="33f82-137">리소스</span><span class="sxs-lookup"><span data-stu-id="33f82-137">Resources</span></span>

<span data-ttu-id="33f82-138">다음은 몇 가지 이전 문서 //www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio toothreat 모델링 오늘입니다.</span><span class="sxs-lookup"><span data-stu-id="33f82-138">Here are a few older articles still relevant toothreat modeling today:</span></span>

* [<span data-ttu-id="33f82-139">중요성의 위협 모델링 hello에 대 한 기사</span><span class="sxs-lookup"><span data-stu-id="33f82-139">Article on hello Importance of Threat Modeling</span></span>](https://msdn.microsoft.com/magazine/dd347831.aspx)
* [<span data-ttu-id="33f82-140">신뢰할 수 있는 컴퓨팅으로 게시된 학습</span><span class="sxs-lookup"><span data-stu-id="33f82-140">Training Published by Trustworthy Computing</span></span>](https://www.microsoft.com/download/details.aspx?id=16420)

<span data-ttu-id="33f82-141">몇 가지 위협 모델링 도구 전문가가 수행한 작업을 확인해 보세요.</span><span class="sxs-lookup"><span data-stu-id="33f82-141">Check out what a few Threat Modeling Tool experts have done:</span></span>

* [<span data-ttu-id="33f82-142">위협 관리자</span><span class="sxs-lookup"><span data-stu-id="33f82-142">Threats Manager</span></span>](https://simoneonsecurity.com/threatsmanagersetup-v1-5-10/)
* [<span data-ttu-id="33f82-143">Simone Curzi 보안 블로그</span><span class="sxs-lookup"><span data-stu-id="33f82-143">Simone Curzi Security Blog</span></span>](https://simoneonsecurity.com/)