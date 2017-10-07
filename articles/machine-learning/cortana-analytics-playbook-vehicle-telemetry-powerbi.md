---
title: "자동차를 움직일 상태 및 구동 BI 대시보드에 aaaPower 습관-Azure | Microsoft Docs"
description: "습관 지원 하 고 차량 상태에 대해 Cortana 인텔리전스 toogain 실시간 및 예측 insights hello 기능을 사용 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: aaeb29a5-4a13-4eab-bbf1-885690d86c56
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: bradsev
ms.openlocfilehash: 0bd054d943387ecad7301236eebae22458173aba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a><span data-ttu-id="a3e8f-103">차량 원격 분석 솔루션 템플릿 Power BI 대시보드 설정 지침</span><span class="sxs-lookup"><span data-stu-id="a3e8f-103">Vehicle telemetry analytics solution template Power BI Dashboard setup instructions</span></span>
<span data-ttu-id="a3e8f-104">이 **메뉴** toohello 장이 플레이이 북에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-104">This **menu** links toohello chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="a3e8f-105">hello 차량 원격 분석 분석 솔루션에서는 딜러 car, automobile 제조업체 및 보험 회사 Cortana 인텔리전스 toogain 실시간 및 예측에 대 한 통찰력 차량 상태 및 구동의 hello 기능 활용 방법 R&d 및 마케팅 캠페인 고객의 습관 toodrive 개선 hello 영역에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-105">hello Vehicle Telemetry Analytics solution showcases how car dealerships, automobile manufacturers and insurance companies can leverage hello capabilities of Cortana Intelligence toogain real-time and predictive insights on vehicle health and driving habits toodrive improvements in hello area of customer experience, R&D and marketing campaigns.</span></span> <span data-ttu-id="a3e8f-106">이 문서는 구성 하는 방법을 hello Power BI 보고서와 대시보드 구독에 hello 솔루션을 배포한 후에 대 한 단계별 지침을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-106">This document contains step by step instructions on how you can configure hello Power BI reports and dashboard once hello solution is deployed in your subscription.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a3e8f-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a3e8f-107">Prerequisites</span></span>
1. <span data-ttu-id="a3e8f-108">Hello 배포 [원격 분석 분석](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) 솔루션</span><span class="sxs-lookup"><span data-stu-id="a3e8f-108">Deploy hello [Telemetry Analytics](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) solution</span></span>  
2. [<span data-ttu-id="a3e8f-109">Microsoft Power BI 데스크톱 설치</span><span class="sxs-lookup"><span data-stu-id="a3e8f-109">Install Microsoft Power BI Desktop</span></span>](http://www.microsoft.com/download/details.aspx?id=45331)
3. <span data-ttu-id="a3e8f-110">[Azure 구독](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a3e8f-110">An [Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="a3e8f-111">Azure 구독이 없으면 Azure 무료 구독 시작</span><span class="sxs-lookup"><span data-stu-id="a3e8f-111">If you don't have an Azure subscription, get started with Azure free subscription</span></span>
4. <span data-ttu-id="a3e8f-112">Microsoft Power BI 계정</span><span class="sxs-lookup"><span data-stu-id="a3e8f-112">Microsoft Power BI account</span></span>

## <a name="cortana-intelligence-suite-components"></a><span data-ttu-id="a3e8f-113">Cortana Intelligence Suite 구성 요소</span><span class="sxs-lookup"><span data-stu-id="a3e8f-113">Cortana Intelligence Suite Components</span></span>
<span data-ttu-id="a3e8f-114">Hello 차량 원격 분석 분석 솔루션 서식 파일의 일부로 hello 다음 Cortana Intelligence 서비스 구독에 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-114">As part of hello Vehicle Telemetry Analytics solution template, hello following Cortana Intelligence services are deployed in your subscription.</span></span>

* <span data-ttu-id="a3e8f-115">**이벤트 허브** - 수백만 개의 차량 원격 분석 이벤트를 Azure에 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-115">**Event Hub** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="a3e8f-116">**스트림 분석** - 차량 상태에 대한 실시간 통찰력을 얻고 다양한 일괄 처리 분석을 위해 해당 데이터를 장기간용 저장소에 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-116">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="a3e8f-117">**기계 학습** 실시간 이상 탐지에 대 한 및 일괄 처리 예측 insights toogain 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-117">**Machine Learning** for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="a3e8f-118">**HDInsight** 규모로 tootransform 사용된 데이터는</span><span class="sxs-lookup"><span data-stu-id="a3e8f-118">**HDInsight** is leveraged tootransform data at scale</span></span>
* <span data-ttu-id="a3e8f-119">**Data Factory** 오케스트레이션, 예약, 리소스 관리 및 모니터링 hello 일괄 처리 파이프라인을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-119">**Data Factory** handles orchestration, scheduling, resource management and monitoring of hello batch processing pipeline.</span></span>

<span data-ttu-id="a3e8f-120">**Power BI** - 실시간 데이터 및 예측 분석 시각화를 위해 이 솔루션을 다양한 대시보드에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-120">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="a3e8f-121">hello 솔루션에서는 두 개의 서로 다른 데이터 소스: **차량 신호 및 진단 데이터 집합 시뮬레이션** 및 **차량 카탈로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-121">hello solution uses two different data sources: **Simulated vehicle signals and diagnostic dataset** and **vehicle catalog**.</span></span>

<span data-ttu-id="a3e8f-122">차량 텔레매틱스 시뮬레이터가 이 솔루션의 일부로 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-122">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="a3e8f-123">진단 정보를 내보냅니다 고, 시간에서 hello 차량 및 구동 패턴 지정된 된 지점에서의 해당 toohello 상태를 알립니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-123">It emits diagnostic information and signals corresponding toohello state of hello vehicle and driving pattern at a given point in time.</span></span> 

<span data-ttu-id="a3e8f-124">hello 차량 카탈로그는 참조 데이터 집합 포함 VIN toomodel 매핑을</span><span class="sxs-lookup"><span data-stu-id="a3e8f-124">hello Vehicle Catalog is a reference dataset containing VIN toomodel mapping</span></span>

## <a name="power-bi-dashboard-preparation"></a><span data-ttu-id="a3e8f-125">Power BI 대시보드 준비</span><span class="sxs-lookup"><span data-stu-id="a3e8f-125">Power BI Dashboard Preparation</span></span>
### <a name="setup-power-bi-real-time-dashboard"></a><span data-ttu-id="a3e8f-126">Power BI에 대한 실시간 대시보드 설정</span><span class="sxs-lookup"><span data-stu-id="a3e8f-126">Setup Power BI Real-Time Dashboard</span></span>

<span data-ttu-id="a3e8f-127">**Hello 실시간 대시보드 응용 프로그램을 시작** hello 수동 작업 지침에 따라 해야 hello 배포가 완료 되 면</span><span class="sxs-lookup"><span data-stu-id="a3e8f-127">**Start hello real-time dashboard application** Once hello deployment is completed, you should follow hello Manual Operation Instructions</span></span>

* <span data-ttu-id="a3e8f-128">실시간 대시보드 응용 프로그램 RealtimeDashboardApp.zip을 다운로드한 다음 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-128">Download real-time dashboard application RealtimeDashboardApp.zip, and unzip it.</span></span>
*  <span data-ttu-id="a3e8f-129">Hello 압축 푼된 폴더에서 응용 프로그램 구성 파일 'RealtimeDashboardApp.exe.config' hello 값이 변경 내용을 저장 하 고 수동 작업 지침은 hello에 Eventhub, Blob 저장소 및 ML 서비스 연결에 대 한 대체 appSettings를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-129">In hello unzipped folder, open app config file 'RealtimeDashboardApp.exe.config', replace appSettings for Eventhub, Blob Storage, and ML service connections with hello values in hello Manual Operation Instructions, and save your changes.</span></span>
* <span data-ttu-id="a3e8f-130">RealtimeDashboardApp.exe 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-130">Run application RealtimeDashboardApp.exe.</span></span> <span data-ttu-id="a3e8f-131">로그인 창 팝업, 유효한 PowerBI 자격 증명을 제공 되며 hello 클릭 **Accept** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-131">A login window will pop up, provide your valid PowerBI credentials and click hello **Accept** button.</span></span> <span data-ttu-id="a3e8f-132">그런 다음 hello 앱 toorun을 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-132">Then hello app will start toorun.</span></span>

   ![로그인 tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Power BI 대시보드 권한](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* <span data-ttu-id="a3e8f-135">로그인 tooPowerBI 웹 사이트 및 실시간 대시보드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-135">Login tooPowerBI website, and create real-time dashboard.</span></span>

<span data-ttu-id="a3e8f-136">이제, 사용 중인 다양 한 시각화 기능 toogain 실시간 함께 준비 tooconfigure hello Power BI 대시보드 및 차량 상태 및 구동에서 예측 insights 습관입니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-136">Now, you are ready tooconfigure hello Power BI dashboard with rich visualizations toogain real-time and predictive insights on vehicle health and driving habits.</span></span> <span data-ttu-id="a3e8f-137">보고 하 고 hello 대시보드를 구성 하는 모든 hello tooan 시간 toocreate 약 45 분이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-137">It takes about 45 minutes tooan hour toocreate all hello reports and configure hello dashboard.</span></span> 

### <a name="configure-power-bi-reports"></a><span data-ttu-id="a3e8f-138">Power BI 보고서 구성</span><span class="sxs-lookup"><span data-stu-id="a3e8f-138">Configure Power BI reports</span></span>
<span data-ttu-id="a3e8f-139">hello 실시간 보고서와 hello 대시보드 30 ~ 45 분 toocomplete 약 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-139">hello real-time reports and hello dashboard take about 30-45 minutes toocomplete.</span></span> <span data-ttu-id="a3e8f-140">너무 찾아보기[http://powerbi.com](http://powerbi.com) 및 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-140">Browse too[http://powerbi.com](http://powerbi.com) and login.</span></span>

![로그인 tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

<span data-ttu-id="a3e8f-142">새 데이터 집합이 Power BI에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-142">A new dataset is generated in Power BI.</span></span> <span data-ttu-id="a3e8f-143">Hello 클릭 **ConnectedCarsRealtime** 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-143">Click hello **ConnectedCarsRealtime** dataset.</span></span>

![연결된 자동차 실시간 데이터 집합 선택](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

<span data-ttu-id="a3e8f-145">Hello 빈 보고서를 사용 하 여 저장 **Ctrl + s**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-145">Save hello blank report using **Ctrl + s**.</span></span>

![빈 보고서 저장](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

<span data-ttu-id="a3e8f-147">보고서 이름 *차량 원격 분석 실시간 보고서*를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-147">Provide report name *Vehicle Telemetry Analytics Real-time - Reports*.</span></span>

![보고서 이름 제공](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a><span data-ttu-id="a3e8f-149">실시간 보고서</span><span class="sxs-lookup"><span data-stu-id="a3e8f-149">Real-time reports</span></span>
<span data-ttu-id="a3e8f-150">이 솔루션에는 다음과 같은 세 가지 실시간 보고서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-150">There are three real-time reports in this solution:</span></span>

1. <span data-ttu-id="a3e8f-151">운행 중인 차량</span><span class="sxs-lookup"><span data-stu-id="a3e8f-151">Vehicles in operation</span></span>
2. <span data-ttu-id="a3e8f-152">유지보수가 필요한 차량</span><span class="sxs-lookup"><span data-stu-id="a3e8f-152">Vehicles Requiring Maintenance</span></span>
3. <span data-ttu-id="a3e8f-153">차량 상태 통계</span><span class="sxs-lookup"><span data-stu-id="a3e8f-153">Vehicles Health Statistics</span></span>

<span data-ttu-id="a3e8f-154">선택할 수 tooconfigure 모든 hello 세 개의 실시간 보고서 또는 모든 단계 후에 중지 있으며 toohello hello 일괄 처리 보고서 구성의 다음 섹션을 계속 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-154">You can choose tooconfigure all hello three real-time reports or stop after any stage and proceed toohello next section of configuring hello batch reports.</span></span> <span data-ttu-id="a3e8f-155">모든 toocreate 권장 hello 3 hello 솔루션의 hello 실시간 경로의 toovisualize hello 전체 정보를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-155">We recommend you toocreate all hello three reports toovisualize hello full insights of hello real-time path of hello solution.</span></span>  

### <a name="1-vehicles-in-operation"></a><span data-ttu-id="a3e8f-156">1. 운행 중인 차량</span><span class="sxs-lookup"><span data-stu-id="a3e8f-156">1. Vehicles in operation</span></span>
<span data-ttu-id="a3e8f-157">두 번 클릭 **1 페이지** 너무 이름을 "차량 작업에서"</span><span class="sxs-lookup"><span data-stu-id="a3e8f-157">Double-click **Page 1** and rename it too“Vehicles in operation”</span></span>  
    <span data-ttu-id="a3e8f-158">![연결된 자동차 - 운행 중인 차량](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span><span class="sxs-lookup"><span data-stu-id="a3e8f-158">![Connected Cars - Vehicles in operation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span></span>  

<span data-ttu-id="a3e8f-159">**필드**에서 **vin**을 선택하고 시각화 형식을 **“카드”**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-159">Select **vin** field from **Fields** and choose visualization type as **“Card”**.</span></span>  

<span data-ttu-id="a3e8f-160">카드 시각화는 그림에 나와 있는 것처럼 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-160">Card visualization is created as shown in figure.</span></span>  
    ![연결된 자동차 - vin 선택](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

<span data-ttu-id="a3e8f-162">새 시각화를 tooadd hello 빈 영역을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-162">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="a3e8f-163">필드에서 **시/군/구** 및 **vin**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-163">Select **City** and **vin** from fields.</span></span> <span data-ttu-id="a3e8f-164">시각화에도 변경**"맵"**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-164">Change visualization too**“Map”**.</span></span> <span data-ttu-id="a3e8f-165">**vin** 을 값 영역으로 끕니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-165">Drag **vin** in values area.</span></span> <span data-ttu-id="a3e8f-166">끌기 **도시** 필드에서 너무**범례** 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-166">Drag **city** from fields too**Legend** area.</span></span>   
    <span data-ttu-id="a3e8f-167">![연결된 자동차 - 카드 시각화](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span><span class="sxs-lookup"><span data-stu-id="a3e8f-167">![Connected Cars - Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span></span>

<span data-ttu-id="a3e8f-168">선택 **형식** 섹션에서 **시각화**, 클릭 **제목** hello 변경 **텍스트** 너무**"차량에서 도시별 작업이"**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-168">Select **format** section from **Visualizations**, click **Title** and change hello **Text** too**“Vehicles in operation by city”**.</span></span>  
    <span data-ttu-id="a3e8f-169">![연결된 자동차 - 도시별 운행 중인 차량](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span><span class="sxs-lookup"><span data-stu-id="a3e8f-169">![Connected Cars - Vehicles in operation by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span></span>   

<span data-ttu-id="a3e8f-170">최종 시각화는 그림과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-170">Final visualization looks as shown in figure.</span></span>    
    ![연결된 자동차 - 최종 시각화](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

<span data-ttu-id="a3e8f-172">새 시각화를 tooadd hello 빈 영역을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-172">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="a3e8f-173">선택 **도시** 및 **vin**, 너무 시각화 형식 변경**묶은 세로 막대형 차트**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-173">Select **City** and **vin**, change visualization type too**Clustered Column Chart**.</span></span> <span data-ttu-id="a3e8f-174">**축 영역**의 **시/군/구** 필드 및 **값 영역**의 **vin** 필드를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-174">Ensure **City** field in **Axis area** and **vin** in **Value area**</span></span>  

<span data-ttu-id="a3e8f-175">**“vin 개수”**별로 차트를 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-175">Sort chart by **“Count of vin”**</span></span>  
    <span data-ttu-id="a3e8f-176">![연결된 자동차 - vin 개수](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span><span class="sxs-lookup"><span data-stu-id="a3e8f-176">![Connected Cars - Count of vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span></span>  

<span data-ttu-id="a3e8f-177">변경 차트 **제목** 너무**"차량 도시별 작업에서"**</span><span class="sxs-lookup"><span data-stu-id="a3e8f-177">Change chart **Title** too**“Vehicles in operation by city”**</span></span>  

<span data-ttu-id="a3e8f-178">Hello 클릭 **형식** 섹션을 다음 선택 **데이터 색**, hello 클릭 **"On"** 너무**모두 표시**</span><span class="sxs-lookup"><span data-stu-id="a3e8f-178">Click hello **Format** section, then select **Data Colors**,  Click hello **“On”** too**Show All**</span></span>  
    <span data-ttu-id="a3e8f-179">![연결된 자동차 - 모든 데이터 색 표시](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span><span class="sxs-lookup"><span data-stu-id="a3e8f-179">![Connected Cars - Show all Data Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span></span>  

<span data-ttu-id="a3e8f-180">색 아이콘을 클릭 하 여 개별 도시 hello 색을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-180">Change hello color of individual city by clicking on color icon.</span></span>  
    ![연결된 자동차 - 색 변경](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

<span data-ttu-id="a3e8f-182">새 시각화를 tooadd hello 빈 영역을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-182">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="a3e8f-183">시각화에서 **묶은 세로 막대형 차트** 시각화를 선택하고 **시/군/구** 필드를 **축** 영역에, **모델**을 **범례** 영역에, **vin**을 **값** 영역으로 끕니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-183">Select **Clustered Column Chart** visualization from visualizations, drag **city** field in **Axis** area, **Model** in **Legend** area and **vin** in **Value** area.</span></span>  
    <span data-ttu-id="a3e8f-184">![연결된 자동차 - 묶은 세로 막대형 차트](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span><span class="sxs-lookup"><span data-stu-id="a3e8f-184">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span></span>  
    <span data-ttu-id="a3e8f-185">![연결된 자동차 - 렌더링](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span><span class="sxs-lookup"><span data-stu-id="a3e8f-185">![Connected Cars - Rendering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span></span>

<span data-ttu-id="a3e8f-186">이 페이지의 모든 시각화를 페이지에 나와 있는 것처럼 다시 배열합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-186">Rearrange all visualization on this page as shown in figure.</span></span>  
    ![연결된 자동차 - 시각화](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

<span data-ttu-id="a3e8f-188">Hello "차량 작업에서" 실시간 보고서를 구성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-188">You have successfully configured hello “Vehicles in operation” real-time report.</span></span> <span data-ttu-id="a3e8f-189">Toocreate hello 다음 실시간 보고서를 계속 또는 중지 구성 하는 hello 대시보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-189">You can proceed toocreate hello next real-time report or stop here and configure hello dashboard.</span></span> 

### <a name="2-vehicles-requiring-maintenance"></a><span data-ttu-id="a3e8f-190">2. 유지보수가 필요한 차량</span><span class="sxs-lookup"><span data-stu-id="a3e8f-190">2. Vehicles Requiring Maintenance</span></span>
<span data-ttu-id="a3e8f-191">클릭 ![추가](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd 새 보고서를 이름을 바꾸거나 너무**"유지 관리를 요구 하는 차량"**</span><span class="sxs-lookup"><span data-stu-id="a3e8f-191">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd a new report, rename it too**“Vehicles Requiring Maintenance”**</span></span>

![연결된 자동차 - 유지보수가 필요한 차량](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

<span data-ttu-id="a3e8f-193">선택 **vin** 필드와 시각화 유형 변경**카드**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-193">Select **vin** field and change visualization type too**Card**.</span></span>  
    <span data-ttu-id="a3e8f-194">![연결된 자동차 - Vin 카드 시각화](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span><span class="sxs-lookup"><span data-stu-id="a3e8f-194">![Connected Cars - Vin Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span></span>  

<span data-ttu-id="a3e8f-195">Hello 데이터 집합의 "MaintenanceLabel" 이라는 필드를 만들려고 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-195">We have a field named “MaintenanceLabel” In hello dataset.</span></span> <span data-ttu-id="a3e8f-196">이 할당량 값은 “0” 또는 “1”일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-196">This field can have a value of “0” or “1”.”</span></span> <span data-ttu-id="a3e8f-197">솔루션의 일부로 프로 비전 하 고 실시간 경로 hello와 통합 hello Azure 기계 학습 모델에 의해 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-197">It is set by hello Azure Machine Learning model provisioned as part of solution and integrated with hello real-time path.</span></span> <span data-ttu-id="a3e8f-198">hello 값 "1"는 차량 유지 관리가 필요한 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-198">hello value “1” indicates a vehicle requires maintenance.</span></span> 

<span data-ttu-id="a3e8f-199">tooadd는 **페이지 수준** 유지 관리를 요구 하는 차량 데이터를 표시 하는 것에 대 한 필터:</span><span class="sxs-lookup"><span data-stu-id="a3e8f-199">tooadd a **Page Level** filter for showing vehicles data, which are requiring maintenance:</span></span> 

1. <span data-ttu-id="a3e8f-200">끌어서 hello **"MaintenanceLabel"** 필드 **페이지 수준 필터**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-200">Drag hello **“MaintenanceLabel”** field into **Page Level Filters**.</span></span>  
   <span data-ttu-id="a3e8f-201">![연결된 자동차 - 페이지 수준 필터](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span><span class="sxs-lookup"><span data-stu-id="a3e8f-201">![Connected Cars - Page Level Filters](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span></span>  
2. <span data-ttu-id="a3e8f-202">MaintenanceLabel 페이지 수준 필터 아래쪽에 있는 **기본 필터링** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-202">Click **Basic Filtering** menu present at bottom of MaintenanceLabel Page Level Filter.</span></span>  
   <span data-ttu-id="a3e8f-203">![연결된 자동차 - 기본 필터링](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span><span class="sxs-lookup"><span data-stu-id="a3e8f-203">![Connected Cars - Basic Filtering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span></span>  
3. <span data-ttu-id="a3e8f-204">필터 값을 너무 설정**"1"**  </span><span class="sxs-lookup"><span data-stu-id="a3e8f-204">Set its filter value too**“1”**  </span></span>  
   <span data-ttu-id="a3e8f-205">![연결된 자동차 - 필터 값](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span><span class="sxs-lookup"><span data-stu-id="a3e8f-205">![Connected Cars - Filter Value](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span></span>  

<span data-ttu-id="a3e8f-206">새 시각화를 tooadd hello 빈 영역을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-206">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="a3e8f-207">시각화에서 **묶은 세로 막대형 차트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-207">Select **Clustered Column Chart** from visualizations</span></span>  
<span data-ttu-id="a3e8f-208">![연결된 자동차 - Vind 카드 시각화](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span><span class="sxs-lookup"><span data-stu-id="a3e8f-208">![Connected Cars - Vind Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span></span>  
<span data-ttu-id="a3e8f-209">![연결된 자동차 - 묶은 세로 막대형 차트](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span><span class="sxs-lookup"><span data-stu-id="a3e8f-209">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span></span>

<span data-ttu-id="a3e8f-210">끌어서 필드 **모델** 에 **축** 영역 **Vin** 너무**값** 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-210">Drag field **Model** into **Axis** area, **Vin** too**Value** area.</span></span> <span data-ttu-id="a3e8f-211">그런 다음 시각화를 **vin 개수**별로 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-211">Then sort visualization by **Count of vin**.</span></span>  <span data-ttu-id="a3e8f-212">변경 차트 **제목** 너무**"모델에 의해 유지 관리를 요구 하는 차량"**</span><span class="sxs-lookup"><span data-stu-id="a3e8f-212">Change chart **Title** too**“Vehicles requiring maintenance by model”**</span></span>  

<span data-ttu-id="a3e8f-213">**vin** 필드를 **시각화** 탭의 **필드** ![필드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) 섹션에 있는 **색 채도**로 끕니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-213">Drag **vin** fields into **Color Saturation** present at **Fields** ![Fields](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) section of **Visualization** tab</span></span>  
<span data-ttu-id="a3e8f-214">![연결된 자동차 - 색 채도](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span><span class="sxs-lookup"><span data-stu-id="a3e8f-214">![Connected Cars - Color Saturation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span></span>  

<span data-ttu-id="a3e8f-215">**형식** 섹션의 시각화에서 **데이터 색**을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-215">Change **Data Colors** in visualizations from **Format** section</span></span>  
<span data-ttu-id="a3e8f-216">최소 색을 **F2C812**로 변경하고,</span><span class="sxs-lookup"><span data-stu-id="a3e8f-216">Change Minimum color to: **F2C812**</span></span>  
<span data-ttu-id="a3e8f-217">최대 색을 **FF6300**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-217">Change Maximum color to: **FF6300**</span></span>  
<span data-ttu-id="a3e8f-218">![연결된 자동차 - 색 변경](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span><span class="sxs-lookup"><span data-stu-id="a3e8f-218">![Connected Cars - Color Changes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span></span>  
<span data-ttu-id="a3e8f-219">![연결된 자동차 - 새 시각화 색](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span><span class="sxs-lookup"><span data-stu-id="a3e8f-219">![Connected Cars - New Visualization Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span></span>  

<span data-ttu-id="a3e8f-220">새 시각화를 tooadd hello 빈 영역을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-220">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="a3e8f-221">시각화에서 **묶은 세로 막대형 차트**를 선택하고 **vin** 필드를 **값** 영역으로, **시/군/구** 필드를 **축** 영역으로 끕니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-221">Select **Clustered column chart** from visualizations, drag **vin** field into **Value** area, drag **City** field into **Axis** area.</span></span> <span data-ttu-id="a3e8f-222">**“vin 개수”**별로 차트를 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-222">Sort chart by **“Count of vin”**.</span></span> <span data-ttu-id="a3e8f-223">변경 차트 **제목** 너무**"도시별 유지 관리를 요구 하는 차량"** </span><span class="sxs-lookup"><span data-stu-id="a3e8f-223">Change chart **Title** too**“Vehicles requiring maintenance by city”** </span></span>  
<span data-ttu-id="a3e8f-224">![연결된 자동차 - 도시별 유지보수가 필요한 차량](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span><span class="sxs-lookup"><span data-stu-id="a3e8f-224">![Connected Cars - Vehicles requiring maintenance by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span></span>  

<span data-ttu-id="a3e8f-225">새 시각화를 tooadd hello 빈 영역을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-225">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="a3e8f-226">선택 **다중 행 카드** 시각화에서 시각화를 끌어 **모델** 및 **vin** hello에 **필드** 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-226">Select **Multi-Row Card** visualization from visualizations, drag **Model** and **vin** into hello **Fields** area.</span></span>  
<span data-ttu-id="a3e8f-227">![연결된 자동차 - 여러 행 카드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span><span class="sxs-lookup"><span data-stu-id="a3e8f-227">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span></span>    

<span data-ttu-id="a3e8f-228">Hello 시각화의 모든 재배열 hello 최종 보고서 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-228">Rearranging all of hello visualization, hello final report looks as follows:</span></span>  
![연결된 자동차 - 여러 행 카드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

<span data-ttu-id="a3e8f-230">Hello "유지 관리를 요구 하는 차량" 실시간 보고서를 구성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-230">You have successfully configured hello “Vehicles Requiring Maintenance” real-time report.</span></span> <span data-ttu-id="a3e8f-231">Toocreate hello 다음 실시간 보고서를 계속 또는 중지 구성 하는 hello 대시보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-231">You can proceed toocreate hello next real-time report or stop here and configure hello dashboard.</span></span> 

### <a name="3-vehicles-health-statistics"></a><span data-ttu-id="a3e8f-232">3. 차량 상태 통계</span><span class="sxs-lookup"><span data-stu-id="a3e8f-232">3. Vehicles Health Statistics</span></span>
<span data-ttu-id="a3e8f-233">클릭 ![추가](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd 새 보고서, 너무 이름 바꾸기**"차량 상태 통계"**</span><span class="sxs-lookup"><span data-stu-id="a3e8f-233">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd new report, rename it too**“Vehicles Health Statistics”**</span></span>  

<span data-ttu-id="a3e8f-234">선택 **계기** 시각화에서 시각화를 끌어와서 hello **속도** 필드 **값, 최소값, 최대값** 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-234">Select **Gauge** visualization from visualizations, then drag hello **Speed** field into **Value, Minimum Value, Maximum Value** areas.</span></span>  
<span data-ttu-id="a3e8f-235">![연결된 자동차 - 여러 행 카드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span><span class="sxs-lookup"><span data-stu-id="a3e8f-235">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span></span>  

<span data-ttu-id="a3e8f-236">기본 집계 hello 변경 **속도** 에 **영역 값** 너무**평균**</span><span class="sxs-lookup"><span data-stu-id="a3e8f-236">Change hello default aggregation of **speed** in **Value area** too**Average**</span></span> 

<span data-ttu-id="a3e8f-237">기본 집계 hello 변경 **속도** 에 **최소 영역** 너무**최소**</span><span class="sxs-lookup"><span data-stu-id="a3e8f-237">Change hello default aggregation of **speed** in **Minimum area** too**Minimum**</span></span>

<span data-ttu-id="a3e8f-238">기본 집계 hello 변경 **속도** 에 **최대 영역** 너무**최대**</span><span class="sxs-lookup"><span data-stu-id="a3e8f-238">Change hello default aggregation of **speed** in **Maximum area** too**Maximum**</span></span>

![연결된 자동차 - 여러 행 카드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

<span data-ttu-id="a3e8f-240">Hello 이름 바꾸기 **계기 제목** 너무**"속도 평균"**</span><span class="sxs-lookup"><span data-stu-id="a3e8f-240">Rename hello **Gauge Title** too**“Average speed”**</span></span> 

![연결된 자동차 - 계기](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

<span data-ttu-id="a3e8f-242">새 시각화를 tooadd hello 빈 영역을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-242">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="a3e8f-243">마찬가지로 **평균 엔진 오일**, **평균 연료** 및 **평균 엔진 온도**에 대한 **계기**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-243">Similarly add a **Gauge** for **average engine oil**, **average fuel**, and **average engine temperate**.</span></span>  

<span data-ttu-id="a3e8f-244">단계 위에 기준으로 각 계기에 필드의 기본 집계 hello 변경 **"속도 평균"** 계기입니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-244">Change hello default aggregation of fields in each gauge as per above steps in **“Average speed”** gauge.</span></span>

![연결된 자동차 - 계기](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

<span data-ttu-id="a3e8f-246">새 시각화를 tooadd hello 빈 영역을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-246">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="a3e8f-247">선택 **꺾은선형 및 묶은 세로 막대형 차트** 시각화에서 끌어 **도시** 필드 **Shared Axis**를 끌어 **속도**, **tirepressure 및 engineoil 필드** 에 **열 값** 영역도 해당 집계 유형을 변경**평균**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-247">Select **Line and Clustered Column Chart** from visualizations, then drag **City** field into **Shared Axis**, drag **speed**, **tirepressure and engineoil fields** into **Column Values** area, change their aggregation type too**Average**.</span></span> 

<span data-ttu-id="a3e8f-248">끌어서 hello **engineTemperature** 필드를 **Line Values** 영역도 hello 집계 형식을 변경**평균**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-248">Drag hello **engineTemperature** field into **Line Values** area, change hello  aggregation type too**Average**.</span></span> 

![연결된 자동차 - 시각화 필드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

<span data-ttu-id="a3e8f-250">변경 hello 차트 **제목** 너무**"평균 속도, 타이어 압력, 석유 엔진 및 엔진 온도"**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-250">Change hello chart **Title** too**“Average speed, tire pressure, engine oil and engine temperature”**.</span></span>  

![연결된 자동차 - 시각화 필드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

<span data-ttu-id="a3e8f-252">새 시각화를 tooadd hello 빈 영역을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-252">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="a3e8f-253">선택 **Treemap** 시각화에서 시각화를 끌어 hello **모델** hello 필드 **그룹** 영역과 끌어서 hello 필드  **MaintenanceProbability** hello에 **값** 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-253">Select **Treemap** visualization from visualizations, drag hello **Model** field into hello **Group** area, and drag hello field **MaintenanceProbability** into hello **Values** area.</span></span>

<span data-ttu-id="a3e8f-254">변경 hello 차트 **제목** 너무**"Vehicle 모델 유지 관리 요구"**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-254">Change hello chart **Title** too**“Vehicle models requiring maintenance”**.</span></span>

![연결된 자동차 - 차트 제목 변경](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

<span data-ttu-id="a3e8f-256">새 시각화를 tooadd hello 빈 영역을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-256">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="a3e8f-257">선택 **100% 기준 누적 가로 막대형 차트** 시각화를 끌어 hello **도시** hello 필드 **축** 영역과 끌어서 hello **MaintenanceProbability**, **RecallProbability** hello에 대 한 필드 **값** 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-257">Select **100% Stacked Bar Chart** from visualization, drag hello **city** field into hello **Axis** area, and drag hello **MaintenanceProbability**, **RecallProbability** fields into hello **Value** area.</span></span>

![연결된 자동차 - 새 시각화 추가](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

<span data-ttu-id="a3e8f-259">클릭 **형식**선택, **데이터 색**, 및 집합 hello **MaintenanceProbability** 색 toohello 값 **"F2C80F"**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-259">Click **Format**, select **Data Colors**, and set hello **MaintenanceProbability** color toohello value **“F2C80F”**.</span></span>

<span data-ttu-id="a3e8f-260">변경 hello **제목** hello의 차트 너무**"확률의 자동차를 움직일 유지 관리 및 다시 호출 하 여 도시"**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-260">Change hello **Title** of hello chart too**“Probability of Vehicle Maintenance & Recall by City”**.</span></span>

![연결된 자동차 - 새 시각화 추가](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

<span data-ttu-id="a3e8f-262">새 시각화를 tooadd hello 빈 영역을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-262">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="a3e8f-263">선택 **영역형 차트** 시각화에서 시각화를 끌어 hello **모델** hello 필드 **축** 영역과 끌어서 hello **engineOil, tirepressure, 속도 MaintenanceProbability** hello에 대 한 필드 **값** 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-263">Select **Area Chart** from visualization from visualizations, drag hello **Model** field into hello **Axis** area, and drag hello **engineOil, tirepressure, speed and MaintenanceProbability** fields into hello **Values** area.</span></span> <span data-ttu-id="a3e8f-264">해당 집계 유형을 변경**"평균"**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-264">Change their aggregation type too**“Average”**.</span></span> 

![연결된 자동차 - 집계 유형 변경](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

<span data-ttu-id="a3e8f-266">Hello 차트의 제목을 hello도 변경**"엔진 석유 평균, 모델에 의해 압력, 속도 및 유지 관리 확률 타이어"**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-266">Change hello title of hello chart too**“Average engine oil, tire pressure, speed and maintenance probability by model”**.</span></span>

![연결된 자동차 - 차트 제목 변경](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

<span data-ttu-id="a3e8f-268">Hello 빈 영역 tooadd 새 시각화를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-268">Click hello blank area tooadd new visualization:</span></span>

1. <span data-ttu-id="a3e8f-269">시각화에서 **분산형 차트** 시각화를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-269">Select **Scatter Chart** visualization from visualizations.</span></span>
2. <span data-ttu-id="a3e8f-270">끌어서 hello **모델** hello 필드 **세부 정보** 및 **범례** 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-270">Drag hello **Model** field into hello **Details** and **Legend** area.</span></span>
3. <span data-ttu-id="a3e8f-271">끌어서 hello **연료** hello 필드 **x 축** 영역 hello 집계도 변경**평균**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-271">Drag hello **fuel** field into hello **X-Axis** area, change hello aggregation too**Average**.</span></span>
4. <span data-ttu-id="a3e8f-272">끌기 **engineTemparature** 에 **y 축 영역**, hello 집계도 변경**평균**</span><span class="sxs-lookup"><span data-stu-id="a3e8f-272">Drag **engineTemparature** into **Y-Axis area**, change hello aggregation too**Average**</span></span>
5. <span data-ttu-id="a3e8f-273">끌어서 hello **vin** hello 필드 **크기** 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-273">Drag hello **vin** field into hello **Size** area.</span></span>

![연결된 자동차 - 새 시각화 추가](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

<span data-ttu-id="a3e8f-275">변경 hello 차트 **제목** 너무**"연료의 평균, 모델에 의해 엔진 온도"**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-275">Change hello chart **Title** too**“Averages of Fuel, Engine Temperature by Model”**.</span></span>

![연결된 자동차 - 차트 제목 변경](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

<span data-ttu-id="a3e8f-277">아래와 같이 hello 최종 보고서는 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-277">hello final report will look like as shown below.</span></span>

![연결된 자동차 - 최종 보고서](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-hello-reports-toohello-real-time-dashboard"></a><span data-ttu-id="a3e8f-279">실시간 대시보드를 toohello hello 보고서의 시각화를 고정</span><span class="sxs-lookup"><span data-stu-id="a3e8f-279">Pin visualizations from hello reports toohello real-time dashboard</span></span>
<span data-ttu-id="a3e8f-280">다음 tooDashboards hello 더하기 아이콘을 클릭 하 여 빈 대시보드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-280">Create a blank dashboard by clicking on hello plus icon next tooDashboards.</span></span> <span data-ttu-id="a3e8f-281">"차량 원격 분석 대시보드"로 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-281">You can name it “Vehicle Telemetry Analytics Dashboard”</span></span>

![연결된 자동차 - 대시보드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

<span data-ttu-id="a3e8f-283">보고서 toohello 대시보드 위에 hello의 시각화를 고정 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-283">Pin hello visualization from hello above reports toohello dashboard.</span></span> 

![연결된 자동차 - 대시보드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

<span data-ttu-id="a3e8f-285">모든 세 개의 보고서 만들어집니다 hello 및 시각화에 해당 하는 hello가 고정 된 toohello 대시보드 hello 대시보드 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-285">hello dashboard should look as follows when all hello three reports are created and hello corresponding visualizations are pinned toohello dashboard.</span></span> <span data-ttu-id="a3e8f-286">모든 hello 보고서를 만들지 않은 경우 대시보드를 다른 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-286">If you have not created all hello reports, your dashboard could look different.</span></span> 

![연결된 자동차 - 대시보드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

<span data-ttu-id="a3e8f-288">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-288">Congratulations!</span></span> <span data-ttu-id="a3e8f-289">Hello 실시간 대시보드를 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-289">You have successfully created hello real-time dashboard.</span></span> <span data-ttu-id="a3e8f-290">Tooexecute CarEventGenerator.exe 및 RealtimeDashboardApp.exe을 계속 하면서 실시간 업데이트 hello 대시보드에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-290">As you continue tooexecute CarEventGenerator.exe and RealtimeDashboardApp.exe, you should see live updates on hello dashboard.</span></span> <span data-ttu-id="a3e8f-291">다음 단계는 약 10 개 too15 분 toocomplete hello를 취해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-291">It should take about 10 too15 minutes toocomplete hello following steps.</span></span>

## <a name="setup-power-bi-batch-processing-dashboard"></a><span data-ttu-id="a3e8f-292">Power BI 일괄 처리 대시보드 설정</span><span class="sxs-lookup"><span data-stu-id="a3e8f-292">Setup Power BI batch processing dashboard</span></span>
> [!NOTE]
> <span data-ttu-id="a3e8f-293">2 시간 (에서 성공적으로 완료 hello 배포의 hello) hello 끝 tooend 일괄 처리를 처리 파이프라인 toofinish 실행에 대 한 걸리고 년 분량의 생성 된 데이터를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-293">It takes about two hours (from hello successful completion of hello deployment) for hello end tooend batch processing pipeline toofinish execution and process a year worth of generated data.</span></span> <span data-ttu-id="a3e8f-294">따라서 toofinish hello 다음 단계를 진행 하기 전에 처리 하는 hello를 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-294">So wait for hello processing toofinish before proceeding with hello next steps.</span></span> 
> 
> 

<span data-ttu-id="a3e8f-295">**Hello Power BI designer 파일을 다운로드**</span><span class="sxs-lookup"><span data-stu-id="a3e8f-295">**Download hello Power BI designer file**</span></span>

* <span data-ttu-id="a3e8f-296">미리 구성 된 Power BI designer 파일 수동 작업 지침은 hello 배포의 일부로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-296">A pre-configured Power BI designer file is included as part of hello deployment Manual Operation Instructions</span></span>
* <span data-ttu-id="a3e8f-297">2를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-297">Look for 2.</span></span> <span data-ttu-id="a3e8f-298">설치 프로그램 PowerBI 일괄 처리 대시보드 라는 일괄 처리 대시보드에 대 한 hello PowerBI 템플릿을 다운로드할 수 있습니다 **ConnectedCarsPbiReport.pbix**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-298">Setup PowerBI batch processing dashboard You can download hello PowerBI template for batch processing dashboard here called **ConnectedCarsPbiReport.pbix**.</span></span>
* <span data-ttu-id="a3e8f-299">• 로컬로 저장</span><span class="sxs-lookup"><span data-stu-id="a3e8f-299">Save locally</span></span>

<span data-ttu-id="a3e8f-300">**Power BI 보고서 구성**</span><span class="sxs-lookup"><span data-stu-id="a3e8f-300">**Configure Power BI reports**</span></span>

* <span data-ttu-id="a3e8f-301">디자이너 파일 열기 hello '**ConnectedCarsPbiReport.pbix**' Power BI Desktop을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-301">Open hello designer file ‘**ConnectedCarsPbiReport.pbix**’ using Power BI Desktop.</span></span> <span data-ttu-id="a3e8f-302">설치 하지 않으면 이미 있으면 경우 Power BI Desktop에서 hello [Power BI Desktop 설치](http://www.microsoft.com/download/details.aspx?id=45331)합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-302">If you do not already have, install hello Power BI Desktop from [Power BI Desktop install](http://www.microsoft.com/download/details.aspx?id=45331).</span></span> 
* <span data-ttu-id="a3e8f-303">Hello 클릭 **쿼리 편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-303">Click hello **Edit Queries**.</span></span>

![Power BI 쿼리 편집](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* <span data-ttu-id="a3e8f-305">Hello를 두 번 클릭 **소스**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-305">Double-click hello **Source**.</span></span>

![Power BI 원본 설정](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* <span data-ttu-id="a3e8f-307">Hello 배포의 일환으로 사용자를 프로 비전 가져왔습니다 hello Azure SQL server와 함께 서버 연결 문자열을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-307">Update Server connection string with hello Azure SQL server that got provisioned as part of hello deployment.</span></span>  <span data-ttu-id="a3e8f-308">Hello 수동 작업 지침은 아래에서 찾는 위치</span><span class="sxs-lookup"><span data-stu-id="a3e8f-308">Look in hello Manual Operation Instructions under</span></span> 

    4. <span data-ttu-id="a3e8f-309">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="a3e8f-309">Azure SQL Database</span></span>
    
    * <span data-ttu-id="a3e8f-310">서버: somethingsrv.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="a3e8f-310">Server: somethingsrv.database.windows.net</span></span>
    * <span data-ttu-id="a3e8f-311">데이터베이스: connectedcar</span><span class="sxs-lookup"><span data-stu-id="a3e8f-311">Database: connectedcar</span></span>
    * <span data-ttu-id="a3e8f-312">사용자 이름: username</span><span class="sxs-lookup"><span data-stu-id="a3e8f-312">Username: username</span></span>
    * <span data-ttu-id="a3e8f-313">암호: Azure Portal에서 SQL Server 암호를 관리할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="a3e8f-313">Password: You can manage your SQL server password from Azure portal</span></span>

* <span data-ttu-id="a3e8f-314">**데이터베이스** 를 *connectedcar*로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-314">Leave **Database** as *connectedcar*.</span></span>

![Power BI 데이터베이스 설정](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* <span data-ttu-id="a3e8f-316">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-316">Click **OK**.</span></span>
* <span data-ttu-id="a3e8f-317">나타납니다 **Windows 자격 증명** 도 변경, 탭은 기본적으로 선택**자격 증명을 데이터베이스** 를 클릭 하 여 **데이터베이스** 오른쪽에 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-317">You will see **Windows credential** tab selected by default, change it too**Database credentials** by clicking on **Database** tab at right.</span></span>
* <span data-ttu-id="a3e8f-318">Hello 제공 **Username** 및 **암호** 배포 설치 중 지정 된 Azure SQL 데이터베이스의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-318">Provide hello **Username** and **Password** of your Azure SQL Database that was specified during its deployment setup.</span></span>

![데이터베이스 자격 증명 제공](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* <span data-ttu-id="a3e8f-320">**연결**</span><span class="sxs-lookup"><span data-stu-id="a3e8f-320">Click **Connect**</span></span>
* <span data-ttu-id="a3e8f-321">세 가지 나머지 쿼리 hello 오른쪽 창에는 각각에 대 한 hello 단계를 반복한 다음 hello 데이터 원본 연결 정보를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-321">Repeat hello above steps for each of hello three remaining queries present at right pane, and then update hello data source connection details.</span></span>
* <span data-ttu-id="a3e8f-322">**닫기 및 로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-322">Click **Close and Load**.</span></span> <span data-ttu-id="a3e8f-323">Power BI Desktop 파일 데이터 집합은 연결 된 tooSQL Azure 데이터베이스 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-323">Power BI Desktop file datasets are connected tooSQL Azure Database tables.</span></span>
* <span data-ttu-id="a3e8f-324">**닫습니다** .</span><span class="sxs-lookup"><span data-stu-id="a3e8f-324">**Close** Power BI Desktop file.</span></span>

![Power BI 데스크톱 닫기](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* <span data-ttu-id="a3e8f-326">클릭 **저장** toosave hello 변경 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-326">Click **Save** button toosave hello changes.</span></span> 

<span data-ttu-id="a3e8f-327">이제 hello 솔루션에서 toohello 일괄 처리 경로 해당 하는 모든 hello 보고서를 구성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-327">You have now configured all hello reports corresponding toohello batch processing path in hello solution.</span></span> 

## <a name="upload-toopowerbicom"></a><span data-ttu-id="a3e8f-328">너무 업로드*powerbi.com*</span><span class="sxs-lookup"><span data-stu-id="a3e8f-328">Upload too*powerbi.com*</span></span>
1. <span data-ttu-id="a3e8f-329">Http://powerbi.com 및 로그인에 toohello Power BI 웹 포털을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-329">Navigate toohello Power BI web portal at http://powerbi.com and login.</span></span>
2. <span data-ttu-id="a3e8f-330">**데이터 가져오기**</span><span class="sxs-lookup"><span data-stu-id="a3e8f-330">Click **Get Data**</span></span>  
3. <span data-ttu-id="a3e8f-331">Hello Power BI 데스크톱 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-331">Upload hello Power BI Desktop File.</span></span>  
4. <span data-ttu-id="a3e8f-332">tooupload, 클릭 **데이터 가져오기 파일이->-> 로컬 파일**</span><span class="sxs-lookup"><span data-stu-id="a3e8f-332">tooupload, click **Get Data -> Files Get -> Local file**</span></span>  
5. <span data-ttu-id="a3e8f-333">Toohello 이동 **"**ConnectedCarsPbiReport.pbix**"**</span><span class="sxs-lookup"><span data-stu-id="a3e8f-333">Navigate toohello **“**ConnectedCarsPbiReport.pbix**”**</span></span>  
6. <span data-ttu-id="a3e8f-334">Hello 파일이 업로드 되 면 백 tooyour를 탐색된 하 고 있습니다. Power BI 작업 공간 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-334">Once hello file is uploaded, you will be navigated back tooyour Power BI work space.</span></span>  

<span data-ttu-id="a3e8f-335">데이터 집합, 보고서 및 빈 대시보드가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-335">A dataset, report and a blank dashboard will be created for you.</span></span>  

<span data-ttu-id="a3e8f-336">Pin 호출 tooa 새 대시보드 차트 **차량 원격 분석 분석 대시보드** 에 **Power BI**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-336">Pin charts tooa new dashboard called **Vehicle Telemetry Analytics Dashboard** in **Power BI**.</span></span> <span data-ttu-id="a3e8f-337">위에서 만든 hello 빈 대시보드를 클릭 한 다음 toohello를 탐색 **보고서** 섹션 클릭 hello 새로 보고서를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-337">Click hello blank dashboard created above and then navigate toohello **Reports** section click hello newly uploaded report.</span></span>  

![차량 원격 분석 Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

<span data-ttu-id="a3e8f-339">**참고 hello 보고서에 6 개 페이지가 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="a3e8f-339">**Note hello report has six pages:**</span></span>  
<span data-ttu-id="a3e8f-340">1페이지: 차량 밀도</span><span class="sxs-lookup"><span data-stu-id="a3e8f-340">Page 1: Vehicle density</span></span>  
<span data-ttu-id="a3e8f-341">2페이지: 실시간 차량 상태</span><span class="sxs-lookup"><span data-stu-id="a3e8f-341">Page 2: Real-time vehicle health</span></span>  
<span data-ttu-id="a3e8f-342">3페이지: 적극적으로 운전한 차량</span><span class="sxs-lookup"><span data-stu-id="a3e8f-342">Page 3: Aggressively Driven Vehicles</span></span>   
<span data-ttu-id="a3e8f-343">4페이지: 리콜된 차량</span><span class="sxs-lookup"><span data-stu-id="a3e8f-343">Page 4: Recalled vehicles</span></span>  
<span data-ttu-id="a3e8f-344">5페이지: 연료 효율이 높게 운전한 차량</span><span class="sxs-lookup"><span data-stu-id="a3e8f-344">Page 5: Fuel Efficiently Driven Vehicles</span></span>  
<span data-ttu-id="a3e8f-345">6페이지: Contoso 로고</span><span class="sxs-lookup"><span data-stu-id="a3e8f-345">Page 6: Contoso Logo</span></span>  

![연결된 자동차 Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

<span data-ttu-id="a3e8f-347">**페이지 3 자에서**, hello 다음 고정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-347">**From Page 3**, pin hello following:</span></span>  

1. <span data-ttu-id="a3e8f-348">vin 개수</span><span class="sxs-lookup"><span data-stu-id="a3e8f-348">Count of VIN</span></span>  
   ![연결된 자동차 Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. <span data-ttu-id="a3e8f-350">모델별 적극적으로 운전한 차량 - 폭포 차트 </span><span class="sxs-lookup"><span data-stu-id="a3e8f-350">Aggressively driven vehicles by model – Waterfall chart</span></span>  
   ![차량 원격 분석 - 차트 4 고정](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

<span data-ttu-id="a3e8f-352">**5 페이지에서에서**, hello 다음 고정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-352">**From Page 5**, pin hello following:</span></span> 

1. <span data-ttu-id="a3e8f-353">vin 개수</span><span class="sxs-lookup"><span data-stu-id="a3e8f-353">Count of vin</span></span>    
   ![차량 원격 분석 - 차트 5 고정](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. <span data-ttu-id="a3e8f-355">모델별 연료 효율이 좋은 차량: 묶은 세로 막대형 차트 </span><span class="sxs-lookup"><span data-stu-id="a3e8f-355">Fuel efficient vehicles by model: Clustered column chart</span></span>  
   ![차량 원격 분석 - 차트 6 고정](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

<span data-ttu-id="a3e8f-357">**4 페이지에서에서**, hello 다음 고정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-357">**From Page 4**, pin hello following:</span></span>  

1. <span data-ttu-id="a3e8f-358">vin 개수</span><span class="sxs-lookup"><span data-stu-id="a3e8f-358">Count of vin</span></span>  
   ![차량 원격 분석 - 차트 7 고정](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. <span data-ttu-id="a3e8f-360">시/군/구, 모델별 리콜된 차량: 트리맵 </span><span class="sxs-lookup"><span data-stu-id="a3e8f-360">Recalled vehicles by city, model: Treemap</span></span>  
   ![차량 원격 분석 - 차트 8 고정](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

<span data-ttu-id="a3e8f-362">**6 페이지에서에서**, hello 다음 고정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-362">**From Page 6**, pin hello following:</span></span>  

1. <span data-ttu-id="a3e8f-363">Contoso 모터 로고 </span><span class="sxs-lookup"><span data-stu-id="a3e8f-363">Contoso Motors logo</span></span>  
   ![차량 원격 분석 - 차트 9 고정](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

<span data-ttu-id="a3e8f-365">**Hello 대시보드 구성**</span><span class="sxs-lookup"><span data-stu-id="a3e8f-365">**Organize hello dashboard**</span></span>  

1. <span data-ttu-id="a3e8f-366">Toohello 대시보드를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-366">Navigate toohello dashboard</span></span>
2. <span data-ttu-id="a3e8f-367">각 차트 위에 놓고 hello 전체 대시보드 이미지 아래에 제공 된 hello 이름 지정에 따라 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-367">Hover over each chart and rename it based on hello naming provided in hello complete dashboard image below.</span></span> <span data-ttu-id="a3e8f-368">또한 hello 대시보드 아래와 같은 toolook 주위 hello 차트를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-368">Also move hello charts around toolook like hello dashboard below.</span></span>  
   ![차량 원격 분석 - 대시보드 2 구성](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![차량 원격 분석 Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. <span data-ttu-id="a3e8f-371">이 문서에서 설명한 것 처럼 모든 hello 보고서를 만든 경우 hello 최종 완료 된 대시보드 찾아야 hello 다음 그림 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-371">If you have created all hello reports as mentioned in this document, hello final completed dashboard should look like hello following figure.</span></span> 

![차량 원격 분석 - 대시보드 2 구성](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

<span data-ttu-id="a3e8f-373">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-373">Congratulations!</span></span> <span data-ttu-id="a3e8f-374">성공적으로 만들었음을 hello 보고서 및 대시보드 toogain 실시간으로 예측 hello 및 차량 상태 및 구동에서 일괄 처리 insights 습관입니다.</span><span class="sxs-lookup"><span data-stu-id="a3e8f-374">You have successfully created hello reports and hello dashboard toogain real-time, predictive and batch insights on vehicle health and driving habits.</span></span>  
