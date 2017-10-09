---
title: "aaaPredict 차량 상태 습관-Azure 지원 하 고 | Microsoft Docs"
description: "습관 지원 하 고 차량 상태에 대해 Cortana 인텔리전스 toogain 실시간 및 예측 insights hello 기능을 사용 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 09fad60b-2f48-488b-8a7e-47d1f969ec6f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 54cc890ff39493bc040bb809721388349665720f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a><span data-ttu-id="401ed-103">차량 원격 분석 솔루션 플레이북</span><span class="sxs-lookup"><span data-stu-id="401ed-103">Vehicle telemetry analytics solution playbook</span></span>
<span data-ttu-id="401ed-104">이 **메뉴** toohello 장이 플레이이 북에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="401ed-104">This **menu** links toohello chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a><span data-ttu-id="401ed-105">개요</span><span class="sxs-lookup"><span data-stu-id="401ed-105">Overview</span></span>
<span data-ttu-id="401ed-106">슈퍼 컴퓨터 hello 랩 외부로 이동한 우리의 시설에 주차 이제 됩니다!</span><span class="sxs-lookup"><span data-stu-id="401ed-106">Super computers have moved out of hello lab and are now parked in our garage!</span></span> <span data-ttu-id="401ed-107">이러한 첨단 자동차는 수많은 hello 기능 tootrack 부여 센서, 포함 및 초당 수백만 개의 이벤트를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="401ed-107">These cutting-edge automobiles contain a myriad of sensors, giving them hello ability tootrack and monitor millions of events every second.</span></span> <span data-ttu-id="401ed-108">2020 하 여 대부분의 이러한 자동차 됩니다 되었음을 인터넷 연결된 toohello 라고 생각 됩니다.</span><span class="sxs-lookup"><span data-stu-id="401ed-108">We expect that by 2020, most of these cars will have been connected toohello Internet.</span></span> <span data-ttu-id="401ed-109">이러한 다양 한 데이터 tooprovide 큰 보안, 안정성 및 구동 더 잘 경험을 이용 가정해 보세요!</span><span class="sxs-lookup"><span data-stu-id="401ed-109">Imagine tapping into this wealth of data tooprovide greater safety, reliability and a better driving experience!</span></span> <span data-ttu-id="401ed-110">Microsoft는 Cortana Intelligence를 통해 이 꿈을 현실화했습니다.</span><span class="sxs-lookup"><span data-stu-id="401ed-110">Microsoft has made this dream a reality with Cortana Intelligence.</span></span>

<span data-ttu-id="401ed-111">Microsoft의 Cortana 인텔리전스는 완전히 관리 되는 빅 데이터 및 지능형 동작으로 analytics suite tootransform 수 있는 데이터를 고급 합니다.</span><span class="sxs-lookup"><span data-stu-id="401ed-111">Microsoft’s Cortana Intelligence is a fully managed big data and advanced analytics suite that enables you tootransform your data into intelligent action.</span></span> <span data-ttu-id="401ed-112">Toointroduce 원하는 toohello Cortana Intelligence 차량 원격 분석 분석 솔루션 템플릿을 합니다.</span><span class="sxs-lookup"><span data-stu-id="401ed-112">We want toointroduce you toohello Cortana Intelligence Vehicle Telemetry Analytics Solution Template.</span></span> <span data-ttu-id="401ed-113">이 솔루션은 방법을 보여 주는 딜러 car, automobile 제조업체 및 보험 회사 수 실시간 Cortana 인텔리전스 toogain hello 기능을 사용 하는 차량 상태 및 구동에서 예측 insights 습관입니다.</span><span class="sxs-lookup"><span data-stu-id="401ed-113">This solution demonstrates how car dealerships, automobile manufacturers, and insurance companies can use hello capabilities of Cortana Intelligence toogain real-time and predictive insights on vehicle health and driving habits.</span></span> 

<span data-ttu-id="401ed-114">hello 솔루션으로 구현 하는 [람다 아키텍처 패턴](https://en.wikipedia.org/wiki/Lambda_architecture) hello에 대 한 hello Cortana Intelligence 플랫폼에 잠재력을 보여 주는 실시간 및 일괄 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="401ed-114">hello solution is implemented as a [lambda architecture pattern](https://en.wikipedia.org/wiki/Lambda_architecture) showing hello full potential of hello Cortana Intelligence platform for real-time and batch processing.</span></span> <span data-ttu-id="401ed-115">hello 해결 방법:</span><span class="sxs-lookup"><span data-stu-id="401ed-115">hello solution:</span></span> 

* <span data-ttu-id="401ed-116">Vehicle Telematics 시뮬레이터 제공</span><span class="sxs-lookup"><span data-stu-id="401ed-116">provides a Vehicle Telematics simulator</span></span>
* <span data-ttu-id="401ed-117">이벤트 허브를 이용하여 수백만 개의 차량 원격 분석 이벤트를 Azure에 수집</span><span class="sxs-lookup"><span data-stu-id="401ed-117">leverages Event Hubs for ingesting millions of simulated vehicle telemetry events into Azure</span></span> 
* <span data-ttu-id="401ed-118">스트림 분석 toogain 실시간 정보를 사용 하 여 차량 상태에 대해</span><span class="sxs-lookup"><span data-stu-id="401ed-118">uses Stream Analytics toogain real-time insights on vehicle health</span></span>
* <span data-ttu-id="401ed-119">일괄 처리의 다양 한 분석에 대 한 장기 저장소에 hello 데이터를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="401ed-119">persists hello data into long-term storage for richer batch analytics.</span></span> 
* <span data-ttu-id="401ed-120">활용 기계 학습에서 비정상 검색에 대 한 실시간 및 처리 toogain 예측 insights 일괄 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="401ed-120">takes advantage of Machine Learning for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="401ed-121">크기 조정 및 Data Factory toohandle 오케스트레이션, 예약, 리소스 관리 및 모니터링 hello 일괄 처리 파이프라인의에서 HDInsight tootransform 데이터를 활용 하 여</span><span class="sxs-lookup"><span data-stu-id="401ed-121">leverages HDInsight tootransform data at scale and Data Factory toohandle orchestration, scheduling, resource management, and monitoring of hello batch processing pipeline</span></span> 
* <span data-ttu-id="401ed-122">Power BI를 사용하여 실시간 데이터 및 예측 분석 시각화를 위해 이 솔루션을 다양한 대시보드에 제공</span><span class="sxs-lookup"><span data-stu-id="401ed-122">gives this solution a rich dashboard for real-time data and predictive analytics visualizations using Power BI</span></span>

## <a name="architecture"></a><span data-ttu-id="401ed-123">아키텍처</span><span class="sxs-lookup"><span data-stu-id="401ed-123">Architecture</span></span>
<span data-ttu-id="401ed-124">![솔루션 아키텍처 다이어그램](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*그림 1 - 차량 원격 분석 솔루션 아키텍처*</span><span class="sxs-lookup"><span data-stu-id="401ed-124">![Solution architecture diagram](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figure 1 – Vehicle Telemetry Analytics Solution Architecture*</span></span>

<span data-ttu-id="401ed-125">이 솔루션에 hello 다음과 같은 **Cortana Intelligence 구성 요소** 의 최종 tooend 통합에서는 및:</span><span class="sxs-lookup"><span data-stu-id="401ed-125">This solution includes hello following **Cortana Intelligence components** and showcases their end tooend integration:</span></span>

* <span data-ttu-id="401ed-126">**이벤트 허브** - 수백만 개의 차량 원격 분석 이벤트를 Azure에 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="401ed-126">**Event Hubs** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="401ed-127">**스트림 분석** - 차량 상태에 대한 실시간 통찰력을 얻고 다양한 일괄 처리 분석을 위해 해당 데이터를 장기간용 저장소에 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="401ed-127">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="401ed-128">**기계 학습** 실시간 이상 탐지에 대 한 및 일괄 처리 예측 insights toogain 합니다.</span><span class="sxs-lookup"><span data-stu-id="401ed-128">**Machine Learning** for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="401ed-129">**HDInsight** 규모로 tootransform 사용된 데이터는</span><span class="sxs-lookup"><span data-stu-id="401ed-129">**HDInsight** is leveraged tootransform data at scale</span></span>
* <span data-ttu-id="401ed-130">**Data Factory** 오케스트레이션, 예약, 리소스 관리 및 모니터링 hello 일괄 처리 파이프라인을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="401ed-130">**Data Factory** handles orchestration, scheduling, resource management and monitoring of hello batch processing pipeline.</span></span>
* <span data-ttu-id="401ed-131">**Power BI** - 실시간 데이터 및 예측 분석 시각화를 위해 이 솔루션을 다양한 대시보드에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="401ed-131">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span>

<span data-ttu-id="401ed-132">이 솔루션은 서로 다른 두 개의 **데이터 원본**에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="401ed-132">This solution accesses two different **data sources**:</span></span> 

* <span data-ttu-id="401ed-133">**자동차를 움직일 신호 및 진단 시뮬레이션**: 차량 전자 통신 정보 시뮬레이터 진단 정보 및 해당 하는 hello 차량와 시간에서 지정된 된 지점에서 패턴을 구동 하는 hello toohello 상태는 신호를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="401ed-133">**Simulated vehicle signals and diagnostics**: A vehicle telematics simulator emits diagnostic information and signals that correspond toohello state of hello vehicle and hello driving pattern at a given point in time.</span></span> 
* <span data-ttu-id="401ed-134">**자동차를 움직일 카탈로그**: VIN toomodel 매핑을 포함 하는 참조 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="401ed-134">**Vehicle catalog**: A reference dataset containing a VIN toomodel mapping.</span></span>

