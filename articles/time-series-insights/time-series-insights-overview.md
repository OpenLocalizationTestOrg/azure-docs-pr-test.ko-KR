---
title: "Azure Time Series Insights 개요 | Microsoft Docs"
description: "시계열 데이터 분석 및 IoT 솔루션을 위한 새로운 서비스인 Azure Time Series Insights를 소개합니다."
keywords: 
services: tsi
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: 
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: omravi
ms.openlocfilehash: abd66208ab7ac30831f3f1eddb2891ed7bcd3995
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-azure-time-series-insights"></a><span data-ttu-id="66153-103">Azure Time Series Insights란?</span><span class="sxs-lookup"><span data-stu-id="66153-103">What is Azure Time Series Insights</span></span>

<span data-ttu-id="66153-104">Azure Time Series Insights는 수십억 개의 이벤트를 동시에 쉽게 수집, 저장, 탐색, 분석할 수 있는 저장소, 분석 및 시각화 구성 요소를 갖춘 관리되는 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="66153-104">Azure Time Series Insights is a managed cloud service with storage, analytics, and visualization components that make it easy to ingest, store, explore and analyze billions of events simultaneously.</span></span> <span data-ttu-id="66153-105">Time Series Insights는 데이터의 전체 보기를 제공하여 IoT 솔루션의 유효성을 빠르게 검사할 수 있으며, 숨겨진 추세와 비정상을 검색하고 거의 실시간으로 근본 원인 분석을 수행할 수 있도록 하여 비용이 많이 드는 장치 가동 중지를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66153-105">Time Series Insights gives you a global view of your data, letting you quickly validate your IoT Solutions, and avoid costly device downtime, by helping you discover hidden trends and anomalies, and conduct root-cause analyses in near real-time.</span></span> <span data-ttu-id="66153-106">Time Series Insights는 이벤트 브로커(예: IoT Hub 또는 Event Hubs)에서 시계열 데이터를 수집하고, 데이터를 인덱싱하고, 구성 가능한 보존 정책에 따라 데이터를 폐기합니다.</span><span class="sxs-lookup"><span data-stu-id="66153-106">Time Series Insights ingests time-series data from event-brokers (e.g. IoT Hubs or Event Hubs), indexes the data, and retires data based on a configurable retention policy.</span></span> <span data-ttu-id="66153-107">사용자는 직관적인 UX 또는 REST 쿼리 API를 통해 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="66153-107">Users consume the data either through an intuitive UX or REST Query APIs.</span></span>

![Time Series Insight 개요](media/overview/time-series-insights-overview-flow.png)

## <a name="primary-scenarios"></a><span data-ttu-id="66153-109">기본 시나리오</span><span class="sxs-lookup"><span data-stu-id="66153-109">Primary scenarios</span></span>

* <span data-ttu-id="66153-110">수분 내에 IoT 솔루션을 모니터링하고 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="66153-110">Monitor and validate IoT solutions in minutes.</span></span>
* <span data-ttu-id="66153-111">대용량 IoT 데이터를 시각화하고 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="66153-111">Visualize and analyze IoT data at scale.</span></span>
* <span data-ttu-id="66153-112">근본 원인 분석 및 변칙 검색을 빠르게 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="66153-112">Expedite root-cause analysis and anomaly detection.</span></span>
* <span data-ttu-id="66153-113">여러 장치, 장비 및 데이터의 전체 보기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="66153-113">Create a global view of multiple devices, plants, and data.</span></span>

## <a name="capabilities-and-benefits"></a><span data-ttu-id="66153-114">기능 및 이점</span><span class="sxs-lookup"><span data-stu-id="66153-114">Capabilities and benefits</span></span>

* <span data-ttu-id="66153-115">**쉬운 시작**: Azure Time Series Insights는 데이터를 미리 준비할 필요가 없으며 매우 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="66153-115">**Easy to get started**: Azure Time Series Insights requires no up-front data preparation and is incredibly fast.</span></span> <span data-ttu-id="66153-116">수분 내에 Azure IoT Hub 또는 Event Hub에서 수십억 개의 이벤트에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="66153-116">Connect to billions of events in your Azure IoT Hub or Event Hub in minutes.</span></span> <span data-ttu-id="66153-117">연결이 되면 수초 내에 센서 데이터를 시각화하고 상호 작용하여 IoT 솔루션의 유효성을 빠르게 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66153-117">Once connected, visualize and interact with sensor data in seconds to quickly validate your IoT solutions.</span></span> <span data-ttu-id="66153-118">Time Series Insights는 한 줄의 코드도 작성하지 않고 데이터와 상호 작용할 수 있으므로 사용하기가 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="66153-118">Time Series Insights is easy to use; you can interact with your data without writing a single line of code.</span></span>  <span data-ttu-id="66153-119">또한 고급 사용자에게는 세분화된 자유 텍스트 쿼리 화면을 제공하고, 모든 사용자에게는 가리킨 다음 클릭 탐색 기능을 제공하므로 새로 익혀야 할 언어가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="66153-119">There is no new language to learn; Time Series Insights provides a granular, free-text query surface for advanced users, and point and click exploration for all.</span></span>

* <span data-ttu-id="66153-120">**거의 실시간에 가까운 정보**: Time Series Insights는 1분 대기 시간으로 하루에 수억 개의 센서 이벤트를 수집할 수 있으므로 변화에 빠르게 대응할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66153-120">**Near Real-time insights**: Time Series Insights can ingest hundreds of millions of sensor events per day, with one minute latency, so you can react to changes quickly.</span></span> <span data-ttu-id="66153-121">Time Series Insights는 추세와 비정상을 빠르게 찾아내고, 복잡한 근본 원인을 분석하며, 비용이 많이 드는 가동 중지를 방지할 수 있게 함으로써 센서 데이터에 대한 심층적인 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66153-121">Time Series Insights helps you gain deep insights into your sensor data by helping you spot trends and anomalies quickly, conduct complex root-cause analyses, and avoid costly downtime.</span></span> <span data-ttu-id="66153-122">Time Series Insights는 실시간 데이터와 기록 데이터 간의 상호 상관 관계를 사용하여 데이터에 숨겨진 추세를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66153-122">By enabling cross-correlation between real-time and historical data, Time Series Insights helps you unlock hidden trends in the data.</span></span>

* <span data-ttu-id="66153-123">**사용자 지정 솔루션 빌드**: Azure Time Series Insights 데이터를 기존 응용 프로그램에 포함하거나 Time Series Insights REST API를 사용하여 새로운 사용자 지정 솔루션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66153-123">**Build custom solutions**: Embed Azure Time Series Insights data into your existing applications, or create new custom solutions with Time Series Insights REST APIs.</span></span> <span data-ttu-id="66153-124">다른 사용자가 검색 결과를 공유하여 탐색할 수 있는 개인 설정 보기를 만들고 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="66153-124">Creating and sharing personalized views you can share for others to explore your discoveries.</span></span>

* <span data-ttu-id="66153-125">**확장성**: Time Series Insights는 대용량 IoT를 지원하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="66153-125">**Scalability**: Time Series Insights is designed to support IoT at scale.</span></span> <span data-ttu-id="66153-126">미리 보기에서 기본 보존 기간을 31일로 설정하면 하루에 1백만 ~ 1억 개의 이벤트를 수신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66153-126">In Preview, it can ingress from 1 million to 100 million events per day, with a default retention span of 31 days.</span></span> <span data-ttu-id="66153-127">방대한 양의 기록 데이터와 함께 라이브 데이터 스트림을 거의 실시간으로 시각화하고 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66153-127">You can visualize and analyze live data streams in near real-time, alongside vast amounts of historical data.</span></span> <span data-ttu-id="66153-128">계속 진화하는 엔터프라이즈 규모를 수용할 수 있도록 전달, 수신 및 고객 보유율이 향상될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="66153-128">Moving forward, ingress and retention rates will increase to accommodate an ever evolving enterprise scale.</span></span>

## <a name="time-series-insights-glossary"></a><span data-ttu-id="66153-129">Time Series Insights 용어</span><span class="sxs-lookup"><span data-stu-id="66153-129">Time Series Insights glossary</span></span>

* <span data-ttu-id="66153-130">**환경**: 환경은 수신 및 저장 용량이 있는 Azure 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="66153-130">**Environment**: An environment is an Azure resource with ingress and storage capacity.</span></span>  <span data-ttu-id="66153-131">고객은 필요한 용량을 갖춘 Azure Portal을 통해 환경을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="66153-131">Customers provision environments through the Azure portal with their required capacity.</span></span>
* <span data-ttu-id="66153-132">**이벤트 원본**: 이벤트 원본은 Azure Event Hubs 같은 이벤트 브로커에서 파생됩니다.</span><span class="sxs-lookup"><span data-stu-id="66153-132">**Event Source**: An Event Source is derived from an event broker, like Azure Event Hubs.</span></span>  <span data-ttu-id="66153-133">Time Series Insights는 이벤트 원본에 직접 연결하여 코드를 작성하지 않고 데이터 스트림을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="66153-133">Time Series Insights connects directly to Event Sources, ingesting the data stream without writing any code.</span></span> <span data-ttu-id="66153-134">현재 Time Series Insights는 Azure Event Hubs 및 Azure IoT Hubs를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="66153-134">Currently, Time Series Insights supports Azure Event Hubs and Azure IoT Hubs.</span></span>
* <span data-ttu-id="66153-135">**참조 데이터**: Time Series Insights는 사용자에게 시계열 데이터를 참조 데이터와 조인하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="66153-135">**Reference data**: Time Series Insights provides users the ability to join time series data with reference data.</span></span>  <span data-ttu-id="66153-136">참조 데이터는 장치에 대한 메타데이터 또는 비교적 자주 변경되지 않는 다른 정적 데이터를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66153-136">Reference data can include metadata about devices, or other static data that changes relatively infrequently.</span></span> <span data-ttu-id="66153-137">Time Series Insights는 사용자가 데이터를 거의 실시간으로 시각화하고 분석할 수 있도록 참조 데이터를 데이터 스트림과 조인합니다.</span><span class="sxs-lookup"><span data-stu-id="66153-137">Time Series Insights joins the reference data with data streams, allowing users to visualize and analyze this data in near real-time.</span></span>
