---
title: "스트림 분석 이벤트 처리를 사용 하 여 처리 시간 aaaReal 이벤트 | Microsoft Docs"
description: "실시간 이벤트 처리 및 분석을 구현하기 위해 Azure 서비스가 어떻게 상호 운용되는지 알아보세요."
keywords: "실시간 처리, 이벤트 처리, 참조 아키텍처"
services: stream-analytics,event-hubs,storage,sql-database
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: 
ms.assetid: 11af48bc-313c-4527-8c80-91088dc9f3c6
ms.service: stream-analytics
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: jeffstok
ms.openlocfilehash: a43c503d709609ba61e9932822d30bc2208906ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reference-architecture-real-time-event-processing-with-microsoft-azure-stream-analytics"></a><span data-ttu-id="1fa91-104">참조 아키텍처: Microsoft Azure Stream Analytics으로 실시간 이벤트 처리</span><span class="sxs-lookup"><span data-stu-id="1fa91-104">Reference architecture: Real-time event processing with Microsoft Azure Stream Analytics</span></span>
<span data-ttu-id="1fa91-105">Azure 스트림 분석을 사용 하 여 처리 하는 실시간 이벤트에 대 한 hello 참조 아키텍처에는 의도 한 tooprovide 실시간 플랫폼으로 Microsoft Azure 서비스 (PaaS) 스트림 처리 솔루션으로 배포 하기 위한 일반 청사진입니다.</span><span class="sxs-lookup"><span data-stu-id="1fa91-105">hello reference architecture for real-time event processing with Azure Stream Analytics is intended tooprovide a generic blueprint for deploying a real-time platform as a service (PaaS) stream-processing solution with Microsoft Azure.</span></span>

## <a name="summary"></a><span data-ttu-id="1fa91-106">요약</span><span class="sxs-lookup"><span data-stu-id="1fa91-106">Summary</span></span>
<span data-ttu-id="1fa91-107">일반적으로 분석 솔루션 토대로 데이터 웨어하우징, ETL (extract, transform, load) 등의 기능 데이터를 이전 tooanalysis 저장된 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fa91-107">Traditionally, analytics solutions have been based on capabilities such as ETL (extract, transform, load) and data warehousing, where data is stored prior tooanalysis.</span></span> <span data-ttu-id="1fa91-108">이 기존 모델 toohello 제한을 강제로 신속 하 게 도착 더 많은 데이터를 포함 하 여 변경 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1fa91-108">Changing requirements, including more rapidly arriving data, are pushing this existing model toohello limit.</span></span> <span data-ttu-id="1fa91-109">hello 기능 tooanalyze 데이터 이동, 이전 toostorage 스트림 내에서 하나의 솔루션 이며 새로운 기능으로는 없지만 hello 접근 방식에 널리 채택 되지는 모든 업계 직종에서.</span><span class="sxs-lookup"><span data-stu-id="1fa91-109">hello ability tooanalyze data within moving streams prior toostorage is one solution, and while it is not a new capability, hello approach has not been widely adopted across all industry verticals.</span></span> 

<span data-ttu-id="1fa91-110">Microsoft Azure는 여러 솔루션 시나리오 및 요구 사항을 지원할 수 있는 광범위한 분석 기술 카탈로그를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1fa91-110">Microsoft Azure provides an extensive catalog of analytics technologies that are capable of supporting an array of different solution scenarios and requirements.</span></span> <span data-ttu-id="1fa91-111">Azure 서비스 toodeploy 종단 간 솔루션에 대 한 제품의 hello 너비 이와 수를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fa91-111">Selecting which Azure services toodeploy for an end-to-end solution can be a challenge given hello breadth of offerings.</span></span> <span data-ttu-id="1fa91-112">이 백서는 디자인 된 toodescribe hello 기능 및 간의 상호 운용을 hello 이벤트 스트리밍 솔루션을 지 원하는 다양 한 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="1fa91-112">This paper is designed toodescribe hello capabilities and interoperation of hello various Azure services that support an event-streaming solution.</span></span> <span data-ttu-id="1fa91-113">또한이 유형의 방법에서 고객 혜택 수 있는 hello 시나리오 중 일부를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fa91-113">It also explains some of hello scenarios in which customers can benefit from this type of approach.</span></span>

## <a name="contents"></a><span data-ttu-id="1fa91-114">목차</span><span class="sxs-lookup"><span data-stu-id="1fa91-114">Contents</span></span>
* <span data-ttu-id="1fa91-115">요약</span><span class="sxs-lookup"><span data-stu-id="1fa91-115">Executive Summary</span></span>
* <span data-ttu-id="1fa91-116">소개 tooReal 시간 분석</span><span class="sxs-lookup"><span data-stu-id="1fa91-116">Introduction tooReal-Time Analytics</span></span>
* <span data-ttu-id="1fa91-117">Azure에서 실시간 데이터의 가치 제안</span><span class="sxs-lookup"><span data-stu-id="1fa91-117">Value Proposition of Real-Time Data in Azure</span></span>
* <span data-ttu-id="1fa91-118">실시간 분석의 일반적인 시나리오</span><span class="sxs-lookup"><span data-stu-id="1fa91-118">Common Scenarios for Real-Time Analytics</span></span>
* <span data-ttu-id="1fa91-119">아키텍처 및 구성 요소</span><span class="sxs-lookup"><span data-stu-id="1fa91-119">Architecture and Components</span></span>
  * <span data-ttu-id="1fa91-120">데이터 원본</span><span class="sxs-lookup"><span data-stu-id="1fa91-120">Data Sources</span></span>
  * <span data-ttu-id="1fa91-121">데이터 통합 계층</span><span class="sxs-lookup"><span data-stu-id="1fa91-121">Data-Integration Layer</span></span>
  * <span data-ttu-id="1fa91-122">실시간 분석 계층</span><span class="sxs-lookup"><span data-stu-id="1fa91-122">Real-time Analytics Layer</span></span>
  * <span data-ttu-id="1fa91-123">데이터 저장소 계층</span><span class="sxs-lookup"><span data-stu-id="1fa91-123">Data Storage Layer</span></span>
  * <span data-ttu-id="1fa91-124">프레젠테이션/소비 계층</span><span class="sxs-lookup"><span data-stu-id="1fa91-124">Presentation / Consumption Layer</span></span>
* <span data-ttu-id="1fa91-125">결론</span><span class="sxs-lookup"><span data-stu-id="1fa91-125">Conclusion</span></span>

<span data-ttu-id="1fa91-126">**작성자:** Charles Feddersen - Microsoft Corporation, Data Insights Center of Excellence, 솔루션 설계자</span><span class="sxs-lookup"><span data-stu-id="1fa91-126">**Author:** Charles Feddersen, Solution Architect, Data Insights Center of Excellence, Microsoft Corporation</span></span>

<span data-ttu-id="1fa91-127">**게시:** 2015년 1월</span><span class="sxs-lookup"><span data-stu-id="1fa91-127">**Published:** January 2015</span></span>

<span data-ttu-id="1fa91-128">**수정 버전:** 1.0</span><span class="sxs-lookup"><span data-stu-id="1fa91-128">**Revision:** 1.0</span></span>

<span data-ttu-id="1fa91-129">**다운로드:** [Microsoft Azure Stream Analytics과 실시간 이벤트 처리](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span><span class="sxs-lookup"><span data-stu-id="1fa91-129">**Download:** [Real-Time Event Processing with Microsoft Azure Stream Analytics](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span></span>

## <a name="get-help"></a><span data-ttu-id="1fa91-130">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="1fa91-130">Get help</span></span>
<span data-ttu-id="1fa91-131">추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="1fa91-131">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="1fa91-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1fa91-132">Next steps</span></span>
* [<span data-ttu-id="1fa91-133">스트림 분석 소개 tooAzure</span><span class="sxs-lookup"><span data-stu-id="1fa91-133">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="1fa91-134">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="1fa91-134">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="1fa91-135">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="1fa91-135">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="1fa91-136">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="1fa91-136">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="1fa91-137">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="1fa91-137">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

