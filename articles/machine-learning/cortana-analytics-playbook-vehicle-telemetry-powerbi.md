---
title: "차량 상태 및 주행 습관에 대한 Power BI - Azure | Microsoft Docs"
description: "Cortana Intelligence의 기능을 사용하여 차량 상태 및 주행 습관에 대한 예측 가능한 통찰력 및 실시간 정보를 얻습니다."
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
ms.openlocfilehash: f880aceb1657ffdfe909b73f175b9673d9ab02cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a><span data-ttu-id="42f9c-103">차량 원격 분석 솔루션 템플릿 Power BI 대시보드 설정 지침</span><span class="sxs-lookup"><span data-stu-id="42f9c-103">Vehicle telemetry analytics solution template Power BI Dashboard setup instructions</span></span>
<span data-ttu-id="42f9c-104">이 **메뉴** 는 이 플레이북 장에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-104">This **menu** links to the chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="42f9c-105">차량 원격 분석 솔루션에서는 자동차 대리점, 자동차 제조업체 및 보험 회사가 Cortana Intelligence의 기능을 이용하여 고객 경험, 연구 개발 및 마케팅 캠페인 분야의 개선을 추진하기 위해 차량 상태 및 운전 습관에 대한 실시간 및 예측 통찰력을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-105">The Vehicle Telemetry Analytics solution showcases how car dealerships, automobile manufacturers and insurance companies can leverage the capabilities of Cortana Intelligence to gain real-time and predictive insights on vehicle health and driving habits to drive improvements in the area of customer experience, R&D and marketing campaigns.</span></span> <span data-ttu-id="42f9c-106">이 문서는 솔루션을 구독에 배포한 후 Power BI 보고서 및 대시보드를 구성할 수 있는 방법에 관한 단계별 지침을 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-106">This document contains step by step instructions on how you can configure the Power BI reports and dashboard once the solution is deployed in your subscription.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="42f9c-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="42f9c-107">Prerequisites</span></span>
1. <span data-ttu-id="42f9c-108">[원격 분석](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) 솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="42f9c-108">Deploy the [Telemetry Analytics](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) solution</span></span>  
2. [<span data-ttu-id="42f9c-109">Microsoft Power BI 데스크톱 설치</span><span class="sxs-lookup"><span data-stu-id="42f9c-109">Install Microsoft Power BI Desktop</span></span>](http://www.microsoft.com/download/details.aspx?id=45331)
3. <span data-ttu-id="42f9c-110">[Azure 구독](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="42f9c-110">An [Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="42f9c-111">Azure 구독이 없으면 Azure 무료 구독 시작</span><span class="sxs-lookup"><span data-stu-id="42f9c-111">If you don't have an Azure subscription, get started with Azure free subscription</span></span>
4. <span data-ttu-id="42f9c-112">Microsoft Power BI 계정</span><span class="sxs-lookup"><span data-stu-id="42f9c-112">Microsoft Power BI account</span></span>

## <a name="cortana-intelligence-suite-components"></a><span data-ttu-id="42f9c-113">Cortana Intelligence Suite 구성 요소</span><span class="sxs-lookup"><span data-stu-id="42f9c-113">Cortana Intelligence Suite Components</span></span>
<span data-ttu-id="42f9c-114">차량 원격 분석 솔루션 템플릿의 일부로 다음 Cortana Intelligence 서비스가 구독에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-114">As part of the Vehicle Telemetry Analytics solution template, the following Cortana Intelligence services are deployed in your subscription.</span></span>

* <span data-ttu-id="42f9c-115">**이벤트 허브** - 수백만 개의 차량 원격 분석 이벤트를 Azure에 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-115">**Event Hub** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="42f9c-116">**스트림 분석** - 차량 상태에 대한 실시간 통찰력을 얻고 다양한 일괄 처리 분석을 위해 해당 데이터를 장기간용 저장소에 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-116">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="42f9c-117">**기계 학습** - 실시간으로 변칙 검색을 수행하고 일괄 처리하여 예측 가능한 통찰력을 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-117">**Machine Learning** for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="42f9c-118">**HDInsight** - 대규모로 데이터를 변환하는 데 이용됩니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-118">**HDInsight** is leveraged to transform data at scale</span></span>
* <span data-ttu-id="42f9c-119">**Data Factory** - 일괄 처리 파이프라인의 오케스트레이션, 예약, 리소스 관리 및 모니터링을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-119">**Data Factory** handles orchestration, scheduling, resource management and monitoring of the batch processing pipeline.</span></span>

<span data-ttu-id="42f9c-120">**Power BI** - 실시간 데이터 및 예측 분석 시각화를 위해 이 솔루션을 다양한 대시보드에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-120">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="42f9c-121">이 솔루션은 두 개의 서로 다른 데이터 소스: **시뮬레이션된 차량 신호 및 진단 데이터 집합** 및 **차량 카탈로그**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-121">The solution uses two different data sources: **Simulated vehicle signals and diagnostic dataset** and **vehicle catalog**.</span></span>

<span data-ttu-id="42f9c-122">차량 텔레매틱스 시뮬레이터가 이 솔루션의 일부로 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-122">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="42f9c-123">이 기능은 지정된 시기에 차량 상태 및 운전 패턴에 해당하는 신호를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-123">It emits diagnostic information and signals corresponding to the state of the vehicle and driving pattern at a given point in time.</span></span> 

<span data-ttu-id="42f9c-124">차량 카탈로그는 모델 매핑에 대한 VIN이 포함된 참조 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-124">The Vehicle Catalog is a reference dataset containing VIN to model mapping</span></span>

## <a name="power-bi-dashboard-preparation"></a><span data-ttu-id="42f9c-125">Power BI 대시보드 준비</span><span class="sxs-lookup"><span data-stu-id="42f9c-125">Power BI Dashboard Preparation</span></span>
### <a name="setup-power-bi-real-time-dashboard"></a><span data-ttu-id="42f9c-126">Power BI에 대한 실시간 대시보드 설정</span><span class="sxs-lookup"><span data-stu-id="42f9c-126">Setup Power BI Real-Time Dashboard</span></span>

<span data-ttu-id="42f9c-127">**실시간 대시보드 응용 프로그램 시작** 배포가 완료되면 수동 작업 지침을 따라야 합니다</span><span class="sxs-lookup"><span data-stu-id="42f9c-127">**Start the real-time dashboard application** Once the deployment is completed, you should follow the Manual Operation Instructions</span></span>

* <span data-ttu-id="42f9c-128">실시간 대시보드 응용 프로그램 RealtimeDashboardApp.zip을 다운로드한 다음 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-128">Download real-time dashboard application RealtimeDashboardApp.zip, and unzip it.</span></span>
*  <span data-ttu-id="42f9c-129">압축을 푼 폴더에서 앱 구성 파일 'RealtimeDashboardApp.exe.config'를 열고 Eventhub, Blob Storage, ML 서비스 연결의 appSettings를 수동 작업 지침의 값으로 바꾸고 변경 사항을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-129">In the unzipped folder, open app config file 'RealtimeDashboardApp.exe.config', replace appSettings for Eventhub, Blob Storage, and ML service connections with the values in the Manual Operation Instructions, and save your changes.</span></span>
* <span data-ttu-id="42f9c-130">RealtimeDashboardApp.exe 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-130">Run application RealtimeDashboardApp.exe.</span></span> <span data-ttu-id="42f9c-131">로그인 창이 표시되면 유효한 PowerBI 자격 증명을 입력하고 **동의** 버튼을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-131">A login window will pop up, provide your valid PowerBI credentials and click the **Accept** button.</span></span> <span data-ttu-id="42f9c-132">그러면 앱이 실행되기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-132">Then the app will start to run.</span></span>

   ![Power BI에 로그인](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Power BI 대시보드 권한](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* <span data-ttu-id="42f9c-135">PowerBI 웹사이트에 로그인하고 실시간 대시보드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-135">Login to PowerBI website, and create real-time dashboard.</span></span>

<span data-ttu-id="42f9c-136">이제 차량 상태 및 운전 습관에 대한 실시간 및 예측 통찰력을 얻기 위해 시각화 효과가 풍부한 Power BI 대시보드를 구성할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-136">Now, you are ready to configure the Power BI dashboard with rich visualizations to gain real-time and predictive insights on vehicle health and driving habits.</span></span> <span data-ttu-id="42f9c-137">모든 보고서를 만들고 대시보드를 구성하는 데 약 45분에서 한 시간쯤 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-137">It takes about 45 minutes to an hour to create all the reports and configure the dashboard.</span></span> 

### <a name="configure-power-bi-reports"></a><span data-ttu-id="42f9c-138">Power BI 보고서 구성</span><span class="sxs-lookup"><span data-stu-id="42f9c-138">Configure Power BI reports</span></span>
<span data-ttu-id="42f9c-139">실시간 보고서 및 대시보드를 완료하려면 약 30~45분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-139">The real-time reports and the dashboard take about 30-45 minutes to complete.</span></span> <span data-ttu-id="42f9c-140">[http://powerbi.com](http://powerbi.com) 로 이동하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-140">Browse to [http://powerbi.com](http://powerbi.com) and login.</span></span>

![Power BI에 로그인](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

<span data-ttu-id="42f9c-142">새 데이터 집합이 Power BI에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-142">A new dataset is generated in Power BI.</span></span> <span data-ttu-id="42f9c-143">**ConnectedCarsRealtime** 데이터 집합을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-143">Click the **ConnectedCarsRealtime** dataset.</span></span>

![연결된 자동차 실시간 데이터 집합 선택](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

<span data-ttu-id="42f9c-145">**Ctrl + s**를 사용하여 빈 보고서를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-145">Save the blank report using **Ctrl + s**.</span></span>

![빈 보고서 저장](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

<span data-ttu-id="42f9c-147">보고서 이름 *차량 원격 분석 실시간 보고서*를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-147">Provide report name *Vehicle Telemetry Analytics Real-time - Reports*.</span></span>

![보고서 이름 제공](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a><span data-ttu-id="42f9c-149">실시간 보고서</span><span class="sxs-lookup"><span data-stu-id="42f9c-149">Real-time reports</span></span>
<span data-ttu-id="42f9c-150">이 솔루션에는 다음과 같은 세 가지 실시간 보고서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-150">There are three real-time reports in this solution:</span></span>

1. <span data-ttu-id="42f9c-151">운행 중인 차량</span><span class="sxs-lookup"><span data-stu-id="42f9c-151">Vehicles in operation</span></span>
2. <span data-ttu-id="42f9c-152">유지보수가 필요한 차량</span><span class="sxs-lookup"><span data-stu-id="42f9c-152">Vehicles Requiring Maintenance</span></span>
3. <span data-ttu-id="42f9c-153">차량 상태 통계</span><span class="sxs-lookup"><span data-stu-id="42f9c-153">Vehicles Health Statistics</span></span>

<span data-ttu-id="42f9c-154">세 가지 실시간 보고서를 모두 구성하거나 단계를 중지하고 배치 보고서 구성의 다음 섹션으로 이동하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-154">You can choose to configure all the three real-time reports or stop after any stage and proceed to the next section of configuring the batch reports.</span></span> <span data-ttu-id="42f9c-155">솔루션의 실시간 경로 전체 통찰력을 시각화하는 세 가지 보고서를 모두 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-155">We recommend you to create all the three reports to visualize the full insights of the real-time path of the solution.</span></span>  

### <a name="1-vehicles-in-operation"></a><span data-ttu-id="42f9c-156">1. 운행 중인 차량</span><span class="sxs-lookup"><span data-stu-id="42f9c-156">1. Vehicles in operation</span></span>
<span data-ttu-id="42f9c-157">**1페이지**를 두 번 클릭하고 “운행 중인 차량”으로 이름을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-157">Double-click **Page 1** and rename it to “Vehicles in operation”</span></span>  
    <span data-ttu-id="42f9c-158">![연결된 자동차 - 운행 중인 차량](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span><span class="sxs-lookup"><span data-stu-id="42f9c-158">![Connected Cars - Vehicles in operation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span></span>  

<span data-ttu-id="42f9c-159">**필드**에서 **vin**을 선택하고 시각화 형식을 **“카드”**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-159">Select **vin** field from **Fields** and choose visualization type as **“Card”**.</span></span>  

<span data-ttu-id="42f9c-160">카드 시각화는 그림에 나와 있는 것처럼 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-160">Card visualization is created as shown in figure.</span></span>  
    ![연결된 자동차 - vin 선택](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

<span data-ttu-id="42f9c-162">빈 영역을 클릭하여 새 시각화를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-162">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="42f9c-163">필드에서 **시/군/구** 및 **vin**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-163">Select **City** and **vin** from fields.</span></span> <span data-ttu-id="42f9c-164">시각화를 **"맵"**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-164">Change visualization to **“Map”**.</span></span> <span data-ttu-id="42f9c-165">**vin** 을 값 영역으로 끕니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-165">Drag **vin** in values area.</span></span> <span data-ttu-id="42f9c-166">필드에서 **시/군/구**를 **범례** 영역으로 끕니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-166">Drag **city** from fields to **Legend** area.</span></span>   
    <span data-ttu-id="42f9c-167">![연결된 자동차 - 카드 시각화](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span><span class="sxs-lookup"><span data-stu-id="42f9c-167">![Connected Cars - Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span></span>

<span data-ttu-id="42f9c-168">**시각화**에서 **형식** 섹션을 선택하고 **제목**을 클릭한 다음 **텍스트**를 **시/군/구별 운행 중인 차량**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-168">Select **format** section from **Visualizations**, click **Title** and change the **Text** to **“Vehicles in operation by city”**.</span></span>  
    <span data-ttu-id="42f9c-169">![연결된 자동차 - 도시별 운행 중인 차량](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span><span class="sxs-lookup"><span data-stu-id="42f9c-169">![Connected Cars - Vehicles in operation by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span></span>   

<span data-ttu-id="42f9c-170">최종 시각화는 그림과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-170">Final visualization looks as shown in figure.</span></span>    
    ![연결된 자동차 - 최종 시각화](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

<span data-ttu-id="42f9c-172">빈 영역을 클릭하여 새 시각화를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-172">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="42f9c-173">**시/군/구** 및 **vin**을 선택하고 시각화 유형을 **묶은 세로 막대형 차트**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-173">Select **City** and **vin**, change visualization type to **Clustered Column Chart**.</span></span> <span data-ttu-id="42f9c-174">**축 영역**의 **시/군/구** 필드 및 **값 영역**의 **vin** 필드를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-174">Ensure **City** field in **Axis area** and **vin** in **Value area**</span></span>  

<span data-ttu-id="42f9c-175">**“vin 개수”**별로 차트를 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-175">Sort chart by **“Count of vin”**</span></span>  
    <span data-ttu-id="42f9c-176">![연결된 자동차 - vin 개수](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span><span class="sxs-lookup"><span data-stu-id="42f9c-176">![Connected Cars - Count of vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span></span>  

<span data-ttu-id="42f9c-177">차트 **제목**을 **“시/군/구별 운행 중인 차량”**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-177">Change chart **Title** to **“Vehicles in operation by city”**</span></span>  

<span data-ttu-id="42f9c-178">**형식** 섹션을 클릭한 다음 **데이터 색**을 선택하고 **모두 표시**에 대한 **“켜기”**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-178">Click the **Format** section, then select **Data Colors**,  Click the **“On”** to **Show All**</span></span>  
    <span data-ttu-id="42f9c-179">![연결된 자동차 - 모든 데이터 색 표시](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span><span class="sxs-lookup"><span data-stu-id="42f9c-179">![Connected Cars - Show all Data Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span></span>  

<span data-ttu-id="42f9c-180">색 아이콘을 클릭하여 개별 시/군/구의 색을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-180">Change the color of individual city by clicking on color icon.</span></span>  
    ![연결된 자동차 - 색 변경](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

<span data-ttu-id="42f9c-182">빈 영역을 클릭하여 새 시각화를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-182">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="42f9c-183">시각화에서 **묶은 세로 막대형 차트** 시각화를 선택하고 **시/군/구** 필드를 **축** 영역에, **모델**을 **범례** 영역에, **vin**을 **값** 영역으로 끕니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-183">Select **Clustered Column Chart** visualization from visualizations, drag **city** field in **Axis** area, **Model** in **Legend** area and **vin** in **Value** area.</span></span>  
    <span data-ttu-id="42f9c-184">![연결된 자동차 - 묶은 세로 막대형 차트](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span><span class="sxs-lookup"><span data-stu-id="42f9c-184">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span></span>  
    <span data-ttu-id="42f9c-185">![연결된 자동차 - 렌더링](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span><span class="sxs-lookup"><span data-stu-id="42f9c-185">![Connected Cars - Rendering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span></span>

<span data-ttu-id="42f9c-186">이 페이지의 모든 시각화를 페이지에 나와 있는 것처럼 다시 배열합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-186">Rearrange all visualization on this page as shown in figure.</span></span>  
    ![연결된 자동차 - 시각화](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

<span data-ttu-id="42f9c-188">"운행 중인 차량" 실시간 보고서를 성공적으로 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-188">You have successfully configured the “Vehicles in operation” real-time report.</span></span> <span data-ttu-id="42f9c-189">다음 실시간 보고서를 계속 만들거나 여기서 작업을 중지하고 대시보드를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-189">You can proceed to create the next real-time report or stop here and configure the dashboard.</span></span> 

### <a name="2-vehicles-requiring-maintenance"></a><span data-ttu-id="42f9c-190">2. 유지보수가 필요한 차량</span><span class="sxs-lookup"><span data-stu-id="42f9c-190">2. Vehicles Requiring Maintenance</span></span>
<span data-ttu-id="42f9c-191">![추가](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) 을 클릭하여 새 보고서를 추가하고 **“유지보수가 필요한 차량”**</span><span class="sxs-lookup"><span data-stu-id="42f9c-191">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) to add a new report, rename it to **“Vehicles Requiring Maintenance”**</span></span>

![연결된 자동차 - 유지보수가 필요한 차량](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

<span data-ttu-id="42f9c-193">**vin** 필드를 선택하고 시각화 유형을 **카드**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-193">Select **vin** field and change visualization type to **Card**.</span></span>  
    <span data-ttu-id="42f9c-194">![연결된 자동차 - Vin 카드 시각화](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span><span class="sxs-lookup"><span data-stu-id="42f9c-194">![Connected Cars - Vin Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span></span>  

<span data-ttu-id="42f9c-195">데이터 집합에 “MaintenanceLabel”이라는 필드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-195">We have a field named “MaintenanceLabel” In the dataset.</span></span> <span data-ttu-id="42f9c-196">이 할당량 값은 “0” 또는 “1”일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-196">This field can have a value of “0” or “1”.”</span></span> <span data-ttu-id="42f9c-197">솔루션의 일부로 프로비전된 Azure 기계 학습 모델에 의해 설정되고 실시간 경로와 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-197">It is set by the Azure Machine Learning model provisioned as part of solution and integrated with the real-time path.</span></span> <span data-ttu-id="42f9c-198">"1" 값은 유지보수가 필요한 차량을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-198">The value “1” indicates a vehicle requires maintenance.</span></span> 

<span data-ttu-id="42f9c-199">유지보수가 필요한 차량 데이터를 표시하기 위해 **페이지 수준** 필터를 추가하려면:</span><span class="sxs-lookup"><span data-stu-id="42f9c-199">To add a **Page Level** filter for showing vehicles data, which are requiring maintenance:</span></span> 

1. <span data-ttu-id="42f9c-200">**“MaintenanceLabel”** 필드를 **페이지 수준 필터**로 끕니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-200">Drag the **“MaintenanceLabel”** field into **Page Level Filters**.</span></span>  
   <span data-ttu-id="42f9c-201">![연결된 자동차 - 페이지 수준 필터](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span><span class="sxs-lookup"><span data-stu-id="42f9c-201">![Connected Cars - Page Level Filters](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span></span>  
2. <span data-ttu-id="42f9c-202">MaintenanceLabel 페이지 수준 필터 아래쪽에 있는 **기본 필터링** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-202">Click **Basic Filtering** menu present at bottom of MaintenanceLabel Page Level Filter.</span></span>  
   <span data-ttu-id="42f9c-203">![연결된 자동차 - 기본 필터링](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span><span class="sxs-lookup"><span data-stu-id="42f9c-203">![Connected Cars - Basic Filtering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span></span>  
3. <span data-ttu-id="42f9c-204">필터 값을 **"1"**  로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-204">Set its filter value to **“1”**  </span></span>  
   <span data-ttu-id="42f9c-205">![연결된 자동차 - 필터 값](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span><span class="sxs-lookup"><span data-stu-id="42f9c-205">![Connected Cars - Filter Value](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span></span>  

<span data-ttu-id="42f9c-206">빈 영역을 클릭하여 새 시각화를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-206">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="42f9c-207">시각화에서 **묶은 세로 막대형 차트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-207">Select **Clustered Column Chart** from visualizations</span></span>  
<span data-ttu-id="42f9c-208">![연결된 자동차 - Vind 카드 시각화](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span><span class="sxs-lookup"><span data-stu-id="42f9c-208">![Connected Cars - Vind Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span></span>  
<span data-ttu-id="42f9c-209">![연결된 자동차 - 묶은 세로 막대형 차트](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span><span class="sxs-lookup"><span data-stu-id="42f9c-209">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span></span>

<span data-ttu-id="42f9c-210">**모델** 필드를 **축** 영역으로, **Vin**을 **값** 영역으로 끕니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-210">Drag field **Model** into **Axis** area, **Vin** to **Value** area.</span></span> <span data-ttu-id="42f9c-211">그런 다음 시각화를 **vin 개수**별로 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-211">Then sort visualization by **Count of vin**.</span></span>  <span data-ttu-id="42f9c-212">차트 **제목**을 **“모델별 유지보수가 필요한 차량”**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-212">Change chart **Title** to **“Vehicles requiring maintenance by model”**</span></span>  

<span data-ttu-id="42f9c-213">**vin** 필드를 **시각화** 탭의 **필드** ![필드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) 섹션에 있는 **색 채도**로 끕니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-213">Drag **vin** fields into **Color Saturation** present at **Fields** ![Fields](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) section of **Visualization** tab</span></span>  
<span data-ttu-id="42f9c-214">![연결된 자동차 - 색 채도](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span><span class="sxs-lookup"><span data-stu-id="42f9c-214">![Connected Cars - Color Saturation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span></span>  

<span data-ttu-id="42f9c-215">**형식** 섹션의 시각화에서 **데이터 색**을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-215">Change **Data Colors** in visualizations from **Format** section</span></span>  
<span data-ttu-id="42f9c-216">최소 색을 **F2C812**로 변경하고,</span><span class="sxs-lookup"><span data-stu-id="42f9c-216">Change Minimum color to: **F2C812**</span></span>  
<span data-ttu-id="42f9c-217">최대 색을 **FF6300**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-217">Change Maximum color to: **FF6300**</span></span>  
<span data-ttu-id="42f9c-218">![연결된 자동차 - 색 변경](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span><span class="sxs-lookup"><span data-stu-id="42f9c-218">![Connected Cars - Color Changes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span></span>  
<span data-ttu-id="42f9c-219">![연결된 자동차 - 새 시각화 색](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span><span class="sxs-lookup"><span data-stu-id="42f9c-219">![Connected Cars - New Visualization Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span></span>  

<span data-ttu-id="42f9c-220">빈 영역을 클릭하여 새 시각화를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-220">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="42f9c-221">시각화에서 **묶은 세로 막대형 차트**를 선택하고 **vin** 필드를 **값** 영역으로, **시/군/구** 필드를 **축** 영역으로 끕니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-221">Select **Clustered column chart** from visualizations, drag **vin** field into **Value** area, drag **City** field into **Axis** area.</span></span> <span data-ttu-id="42f9c-222">**“vin 개수”**별로 차트를 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-222">Sort chart by **“Count of vin”**.</span></span> <span data-ttu-id="42f9c-223">차트 **제목**을 **“시/군/구별 유지보수가 필요한 차량”** 으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-223">Change chart **Title** to **“Vehicles requiring maintenance by city”** </span></span>  
<span data-ttu-id="42f9c-224">![연결된 자동차 - 도시별 유지보수가 필요한 차량](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span><span class="sxs-lookup"><span data-stu-id="42f9c-224">![Connected Cars - Vehicles requiring maintenance by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span></span>  

<span data-ttu-id="42f9c-225">빈 영역을 클릭하여 새 시각화를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-225">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="42f9c-226">시각화에서 **여러 행 카드** 시각화를 선택하고 **모델** 및 **vin**을 **필드** 영역으로 끕니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-226">Select **Multi-Row Card** visualization from visualizations, drag **Model** and **vin** into the **Fields** area.</span></span>  
<span data-ttu-id="42f9c-227">![연결된 자동차 - 여러 행 카드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span><span class="sxs-lookup"><span data-stu-id="42f9c-227">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span></span>    

<span data-ttu-id="42f9c-228">모든 시각화 요소를 다시 정렬하면 최종 보고서 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-228">Rearranging all of the visualization, the final report looks as follows:</span></span>  
![연결된 자동차 - 여러 행 카드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

<span data-ttu-id="42f9c-230">"유지보수가 필요한 차량" 실시간 보고서를 성공적으로 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-230">You have successfully configured the “Vehicles Requiring Maintenance” real-time report.</span></span> <span data-ttu-id="42f9c-231">다음 실시간 보고서를 계속 만들거나 여기서 작업을 중지하고 대시보드를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-231">You can proceed to create the next real-time report or stop here and configure the dashboard.</span></span> 

### <a name="3-vehicles-health-statistics"></a><span data-ttu-id="42f9c-232">3. 차량 상태 통계</span><span class="sxs-lookup"><span data-stu-id="42f9c-232">3. Vehicles Health Statistics</span></span>
<span data-ttu-id="42f9c-233">![추가](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) 을 클릭하여 새 보고서를 추가하고 **“차량 상태 통계”**</span><span class="sxs-lookup"><span data-stu-id="42f9c-233">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) to add new report, rename it to **“Vehicles Health Statistics”**</span></span>  

<span data-ttu-id="42f9c-234">시각화에서 **계기** 시각화를 선택한 다음 **속도** 필드를 **값, 최소값, 최대값** 영역으로 끕니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-234">Select **Gauge** visualization from visualizations, then drag the **Speed** field into **Value, Minimum Value, Maximum Value** areas.</span></span>  
<span data-ttu-id="42f9c-235">![연결된 자동차 - 여러 행 카드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span><span class="sxs-lookup"><span data-stu-id="42f9c-235">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span></span>  

<span data-ttu-id="42f9c-236">**값 영역**에서 **속도**의 기본 집계를 **평균**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-236">Change the default aggregation of **speed** in **Value area** to **Average**</span></span> 

<span data-ttu-id="42f9c-237">**최소값 영역**에서 **속도**의 기본 집계를 **최소값**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-237">Change the default aggregation of **speed** in **Minimum area** to **Minimum**</span></span>

<span data-ttu-id="42f9c-238">**최대값 영역**에서 **속도**의 기본 집계를 **최대값**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-238">Change the default aggregation of **speed** in **Maximum area** to **Maximum**</span></span>

![연결된 자동차 - 여러 행 카드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

<span data-ttu-id="42f9c-240">**계기 제목**을 **“평균 속도”**로 이름 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-240">Rename the **Gauge Title** to **“Average speed”**</span></span> 

![연결된 자동차 - 계기](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

<span data-ttu-id="42f9c-242">빈 영역을 클릭하여 새 시각화를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-242">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="42f9c-243">마찬가지로 **평균 엔진 오일**, **평균 연료** 및 **평균 엔진 온도**에 대한 **계기**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-243">Similarly add a **Gauge** for **average engine oil**, **average fuel**, and **average engine temperate**.</span></span>  

<span data-ttu-id="42f9c-244">**“평균 속도”** 계기에서 위의 각 단계에 따라 각 계기에서 필드의 기본 집계를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-244">Change the default aggregation of fields in each gauge as per above steps in **“Average speed”** gauge.</span></span>

![연결된 자동차 - 계기](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

<span data-ttu-id="42f9c-246">빈 영역을 클릭하여 새 시각화를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-246">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="42f9c-247">시각화에서 **줄 및 묶은 세로 막대형 차트**를 선택한 다음 **시/군/구** 필드를 **공유 축**으로, **속도**, **타이어 압력 및 엔진 오일 필드**를 **열 값** 영역으로 끌고 해당 집계 형식을 **평균**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-247">Select **Line and Clustered Column Chart** from visualizations, then drag **City** field into **Shared Axis**, drag **speed**, **tirepressure and engineoil fields** into **Column Values** area, change their aggregation type to **Average**.</span></span> 

<span data-ttu-id="42f9c-248">**engineTemperature** 필드를 **줄 값** 영역으로 끌고 집계 유형을 **평균**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-248">Drag the **engineTemperature** field into **Line Values** area, change the  aggregation type to **Average**.</span></span> 

![연결된 자동차 - 시각화 필드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

<span data-ttu-id="42f9c-250">차트 **제목**을 **“평균 속도, 타이어 압력, 엔진 오일 및 엔진 온도”**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-250">Change the chart **Title** to **“Average speed, tire pressure, engine oil and engine temperature”**.</span></span>  

![연결된 자동차 - 시각화 필드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

<span data-ttu-id="42f9c-252">빈 영역을 클릭하여 새 시각화를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-252">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="42f9c-253">시각화에서 **트리맵** 시각화를 선택하고 **모델** 필드를 **그룹** 영역으로, **MaintenanceProbability** 필드를 **값** 영역으로 끕니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-253">Select **Treemap** visualization from visualizations, drag the **Model** field into the **Group** area, and drag the field **MaintenanceProbability** into the **Values** area.</span></span>

<span data-ttu-id="42f9c-254">차트 **제목**을 **“유지보수가 필요한 차량 모델”**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-254">Change the chart **Title** to **“Vehicle models requiring maintenance”**.</span></span>

![연결된 자동차 - 차트 제목 변경](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

<span data-ttu-id="42f9c-256">빈 영역을 클릭하여 새 시각화를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-256">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="42f9c-257">시각화에서 **100% 누적 가로 막대형 차트**를 선택하고 **시/군/구** 필드를 **축** 영역으로, **MaintenanceProbability**, **RecallProbability** 필드를 **값** 영역으로 끌어옵니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-257">Select **100% Stacked Bar Chart** from visualization, drag the **city** field into the **Axis** area, and drag the **MaintenanceProbability**, **RecallProbability** fields into the **Value** area.</span></span>

![연결된 자동차 - 새 시각화 추가](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

<span data-ttu-id="42f9c-259">**형식**을 클릭하고 **데이터 색**을 선택하고 **MaintenanceProbability** 색을 값 **“F2C80F”**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-259">Click **Format**, select **Data Colors**, and set the **MaintenanceProbability** color to the value **“F2C80F”**.</span></span>

<span data-ttu-id="42f9c-260">차트의 **제목**을 **“시/군/구별 차량 유지보수 및 리콜 확률”**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-260">Change the **Title** of the chart to **“Probability of Vehicle Maintenance & Recall by City”**.</span></span>

![연결된 자동차 - 새 시각화 추가](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

<span data-ttu-id="42f9c-262">빈 영역을 클릭하여 새 시각화를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-262">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="42f9c-263">시각화에서 **영역형 차트**를 선택하고 **모델** 필드를 **축** 영역으로, **engineOil, tirepressure, speed 및 MaintenanceProbability** 필드를 **값** 영역으로 끕니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-263">Select **Area Chart** from visualization from visualizations, drag the **Model** field into the **Axis** area, and drag the **engineOil, tirepressure, speed and MaintenanceProbability** fields into the **Values** area.</span></span> <span data-ttu-id="42f9c-264">해당 집계 유형을 **“평균”**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-264">Change their aggregation type to **“Average”**.</span></span> 

![연결된 자동차 - 집계 유형 변경](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

<span data-ttu-id="42f9c-266">차트 제목을 **“모델별 엔진 오일, 타이어 압력, 속도 및 유지보수 확률 평균”**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-266">Change the title of the chart to **“Average engine oil, tire pressure, speed and maintenance probability by model”**.</span></span>

![연결된 자동차 - 차트 제목 변경](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

<span data-ttu-id="42f9c-268">빈 영역을 클릭하여 새 시각화를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-268">Click the blank area to add new visualization:</span></span>

1. <span data-ttu-id="42f9c-269">시각화에서 **분산형 차트** 시각화를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-269">Select **Scatter Chart** visualization from visualizations.</span></span>
2. <span data-ttu-id="42f9c-270">**모델** 필드를 **세부 정보** 및 **범례** 영역으로 끌어옵니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-270">Drag the **Model** field into the **Details** and **Legend** area.</span></span>
3. <span data-ttu-id="42f9c-271">**연료** 필드를 **X 축** 영역으로 끌고 집계를 **평균**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-271">Drag the **fuel** field into the **X-Axis** area, change the aggregation to **Average**.</span></span>
4. <span data-ttu-id="42f9c-272">**engineTemparature**를 **Y 축 영역**으로 끌고 집계를 **평균**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-272">Drag **engineTemparature** into **Y-Axis area**, change the aggregation to **Average**</span></span>
5. <span data-ttu-id="42f9c-273">**vin** 필드를 **크기** 영역으로 끌어옵니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-273">Drag the **vin** field into the **Size** area.</span></span>

![연결된 자동차 - 새 시각화 추가](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

<span data-ttu-id="42f9c-275">차트 **제목**을 **“모델별 연료, 엔진 온도 평균”**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-275">Change the chart **Title** to **“Averages of Fuel, Engine Temperature by Model”**.</span></span>

![연결된 자동차 - 차트 제목 변경](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

<span data-ttu-id="42f9c-277">최종 보고서는 아래와 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-277">The final report will look like as shown below.</span></span>

![연결된 자동차 - 최종 보고서](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-the-reports-to-the-real-time-dashboard"></a><span data-ttu-id="42f9c-279">보고서의 시각화를 실시간 대시보드에 고정</span><span class="sxs-lookup"><span data-stu-id="42f9c-279">Pin visualizations from the reports to the real-time dashboard</span></span>
<span data-ttu-id="42f9c-280">대시보드 옆의 더하기 아이콘을 클릭하여 빈 대시보드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-280">Create a blank dashboard by clicking on the plus icon next to Dashboards.</span></span> <span data-ttu-id="42f9c-281">"차량 원격 분석 대시보드"로 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-281">You can name it “Vehicle Telemetry Analytics Dashboard”</span></span>

![연결된 자동차 - 대시보드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

<span data-ttu-id="42f9c-283">위의 보고서에서 대시보드에 시각화를 고정합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-283">Pin the visualization from the above reports to the dashboard.</span></span> 

![연결된 자동차 - 대시보드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

<span data-ttu-id="42f9c-285">세 가지 보고서를 모두 만들고 해당하는 시각화를 대시보드에 고정할 경우 대시보드는 아래와 같이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-285">The dashboard should look as follows when all the three reports are created and the corresponding visualizations are pinned to the dashboard.</span></span> <span data-ttu-id="42f9c-286">보고서를 모두 만들지 않은 경우 대시보드는 다르게 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-286">If you have not created all the reports, your dashboard could look different.</span></span> 

![연결된 자동차 - 대시보드](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

<span data-ttu-id="42f9c-288">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-288">Congratulations!</span></span> <span data-ttu-id="42f9c-289">실시간 대시보드를 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-289">You have successfully created the real-time dashboard.</span></span> <span data-ttu-id="42f9c-290">CarEventGenerator.exe 및 RealtimeDashboardApp.exe 실행을 계속하면서 라이브 업데이트가 대시보드에 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-290">As you continue to execute CarEventGenerator.exe and RealtimeDashboardApp.exe, you should see live updates on the dashboard.</span></span> <span data-ttu-id="42f9c-291">다음 단계를 완료하려면 약 10-15분 정도가 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-291">It should take about 10 to 15 minutes to complete the following steps.</span></span>

## <a name="setup-power-bi-batch-processing-dashboard"></a><span data-ttu-id="42f9c-292">Power BI 일괄 처리 대시보드 설정</span><span class="sxs-lookup"><span data-stu-id="42f9c-292">Setup Power BI batch processing dashboard</span></span>
> [!NOTE]
> <span data-ttu-id="42f9c-293">파이프라인을 처리하는 종단 간 배치의 경우 (성공적인 배포 완료에서) 실행을 완료하고 일 년 분량의 생성된 데이터를 처리하는 데 약 두 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-293">It takes about two hours (from the successful completion of the deployment) for the end to end batch processing pipeline to finish execution and process a year worth of generated data.</span></span> <span data-ttu-id="42f9c-294">따라서 다음 단계를 계속하기 전에 처리가 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-294">So wait for the processing to finish before proceeding with the next steps.</span></span> 
> 
> 

<span data-ttu-id="42f9c-295">**Power BI Designer 파일 다운로드**</span><span class="sxs-lookup"><span data-stu-id="42f9c-295">**Download the Power BI designer file**</span></span>

* <span data-ttu-id="42f9c-296">미리 구성된 Power BI Designer 파일이 배포 수동 작업 지침의 일부로 포함되어 있습니다</span><span class="sxs-lookup"><span data-stu-id="42f9c-296">A pre-configured Power BI designer file is included as part of the deployment Manual Operation Instructions</span></span>
* <span data-ttu-id="42f9c-297">2를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-297">Look for 2.</span></span> <span data-ttu-id="42f9c-298">PowerBI 배치 프로세싱 대시보드 설정 여기에서 배치 처리 대시보드의 PowerBI 템플릿 **ConnectedCarsPbiReport.pbix**를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-298">Setup PowerBI batch processing dashboard You can download the PowerBI template for batch processing dashboard here called **ConnectedCarsPbiReport.pbix**.</span></span>
* <span data-ttu-id="42f9c-299">• 로컬로 저장</span><span class="sxs-lookup"><span data-stu-id="42f9c-299">Save locally</span></span>

<span data-ttu-id="42f9c-300">**Power BI 보고서 구성**</span><span class="sxs-lookup"><span data-stu-id="42f9c-300">**Configure Power BI reports**</span></span>

* <span data-ttu-id="42f9c-301">Power BI Desktop을 사용하여 디자이너 파일 ‘**ConnectedCarsPbiReport.pbix**’를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-301">Open the designer file ‘**ConnectedCarsPbiReport.pbix**’ using Power BI Desktop.</span></span> <span data-ttu-id="42f9c-302">아직 없는 경우 [Power BI Desktop 설치](http://www.microsoft.com/download/details.aspx?id=45331)에서 Power BI 데스크톱을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-302">If you do not already have, install the Power BI Desktop from [Power BI Desktop install](http://www.microsoft.com/download/details.aspx?id=45331).</span></span> 
* <span data-ttu-id="42f9c-303">**쿼리 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-303">Click the **Edit Queries**.</span></span>

![Power BI 쿼리 편집](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* <span data-ttu-id="42f9c-305">**소스**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-305">Double-click the **Source**.</span></span>

![Power BI 원본 설정](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* <span data-ttu-id="42f9c-307">배포의 일부로 프로비전된 Azure SQL Server를 통해 서버 연결 문자열을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-307">Update Server connection string with the Azure SQL server that got provisioned as part of the deployment.</span></span>  <span data-ttu-id="42f9c-308">수동 작업 지침에서 찾습니다</span><span class="sxs-lookup"><span data-stu-id="42f9c-308">Look in the Manual Operation Instructions under</span></span> 

    4. <span data-ttu-id="42f9c-309">Azure SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="42f9c-309">Azure SQL Database</span></span>
    
    * <span data-ttu-id="42f9c-310">서버: somethingsrv.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="42f9c-310">Server: somethingsrv.database.windows.net</span></span>
    * <span data-ttu-id="42f9c-311">데이터베이스: connectedcar</span><span class="sxs-lookup"><span data-stu-id="42f9c-311">Database: connectedcar</span></span>
    * <span data-ttu-id="42f9c-312">사용자 이름: username</span><span class="sxs-lookup"><span data-stu-id="42f9c-312">Username: username</span></span>
    * <span data-ttu-id="42f9c-313">암호: Azure Portal에서 SQL Server 암호를 관리할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="42f9c-313">Password: You can manage your SQL server password from Azure portal</span></span>

* <span data-ttu-id="42f9c-314">**데이터베이스** 를 *connectedcar*로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-314">Leave **Database** as *connectedcar*.</span></span>

![Power BI 데이터베이스 설정](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* <span data-ttu-id="42f9c-316">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-316">Click **OK**.</span></span>
* <span data-ttu-id="42f9c-317">기본적으로 선택된 **Windows 자격 증명** 탭을 확인하고 오른쪽의 **데이터베이스**를 클릭하여 **데이터베이스 자격 증명**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-317">You will see **Windows credential** tab selected by default, change it to **Database credentials** by clicking on **Database** tab at right.</span></span>
* <span data-ttu-id="42f9c-318">배포 설치 중 지정된 Azure SQL 데이터베이스의 **사용자 이름** 및 **암호**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-318">Provide the **Username** and **Password** of your Azure SQL Database that was specified during its deployment setup.</span></span>

![데이터베이스 자격 증명 제공](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* <span data-ttu-id="42f9c-320">**연결**</span><span class="sxs-lookup"><span data-stu-id="42f9c-320">Click **Connect**</span></span>
* <span data-ttu-id="42f9c-321">오른쪽 창에 있는 남은 쿼리 세 개 각각에 대해 위 단계를 반복하고 데이터 소스 연결 세부 정보를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-321">Repeat the above steps for each of the three remaining queries present at right pane, and then update the data source connection details.</span></span>
* <span data-ttu-id="42f9c-322">**닫기 및 로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-322">Click **Close and Load**.</span></span> <span data-ttu-id="42f9c-323">Power BI 데스크톱 파일 데이터 집합은 SQL Azure 데이터베이스 테이블에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-323">Power BI Desktop file datasets are connected to SQL Azure Database tables.</span></span>
* <span data-ttu-id="42f9c-324">**닫습니다** .</span><span class="sxs-lookup"><span data-stu-id="42f9c-324">**Close** Power BI Desktop file.</span></span>

![Power BI 데스크톱 닫기](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* <span data-ttu-id="42f9c-326">**저장** 단추를 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-326">Click **Save** button to save the changes.</span></span> 

<span data-ttu-id="42f9c-327">이제 솔루션의 배치 처리 경로에 해당하는 모든 보고서를 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-327">You have now configured all the reports corresponding to the batch processing path in the solution.</span></span> 

## <a name="upload-to-powerbicom"></a><span data-ttu-id="42f9c-328">*powerbi.com*</span><span class="sxs-lookup"><span data-stu-id="42f9c-328">Upload to *powerbi.com*</span></span>
1. <span data-ttu-id="42f9c-329">http://powerbi.com에서 Power BI 웹 포털로 이동하고 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-329">Navigate to the Power BI web portal at http://powerbi.com and login.</span></span>
2. <span data-ttu-id="42f9c-330">**데이터 가져오기**</span><span class="sxs-lookup"><span data-stu-id="42f9c-330">Click **Get Data**</span></span>  
3. <span data-ttu-id="42f9c-331">Power BI 데스크톱 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-331">Upload the Power BI Desktop File.</span></span>  
4. <span data-ttu-id="42f9c-332">업로드하려면 **데이터 가져오기 -> 파일 가져오기 -> 로컬 파일**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-332">To upload, click **Get Data -> Files Get -> Local file**</span></span>  
5. <span data-ttu-id="42f9c-333">**“**ConnectedCarsPbiReport.pbix**”**로 이동합니다</span><span class="sxs-lookup"><span data-stu-id="42f9c-333">Navigate to the **“**ConnectedCarsPbiReport.pbix**”**</span></span>  
6. <span data-ttu-id="42f9c-334">파일이 업로드된 후 Power BI 작업 공간으로 다시 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-334">Once the file is uploaded, you will be navigated back to your Power BI work space.</span></span>  

<span data-ttu-id="42f9c-335">데이터 집합, 보고서 및 빈 대시보드가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-335">A dataset, report and a blank dashboard will be created for you.</span></span>  

<span data-ttu-id="42f9c-336">**Power BI**에서 새 대시보드인 **차량 원격 분석 대시보드**에 차트를 고정합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-336">Pin charts to a new dashboard called **Vehicle Telemetry Analytics Dashboard** in **Power BI**.</span></span> <span data-ttu-id="42f9c-337">위에서 만든 빈 대시보드를 클릭한 다음 **보고서** 섹션으로 이동하여 새로 업로드한 보고서를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-337">Click the blank dashboard created above and then navigate to the **Reports** section click the newly uploaded report.</span></span>  

![차량 원격 분석 Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

<span data-ttu-id="42f9c-339">**참고로 보고서에는 6페이지가 있음:**</span><span class="sxs-lookup"><span data-stu-id="42f9c-339">**Note the report has six pages:**</span></span>  
<span data-ttu-id="42f9c-340">1페이지: 차량 밀도</span><span class="sxs-lookup"><span data-stu-id="42f9c-340">Page 1: Vehicle density</span></span>  
<span data-ttu-id="42f9c-341">2페이지: 실시간 차량 상태</span><span class="sxs-lookup"><span data-stu-id="42f9c-341">Page 2: Real-time vehicle health</span></span>  
<span data-ttu-id="42f9c-342">3페이지: 적극적으로 운전한 차량</span><span class="sxs-lookup"><span data-stu-id="42f9c-342">Page 3: Aggressively Driven Vehicles</span></span>   
<span data-ttu-id="42f9c-343">4페이지: 리콜된 차량</span><span class="sxs-lookup"><span data-stu-id="42f9c-343">Page 4: Recalled vehicles</span></span>  
<span data-ttu-id="42f9c-344">5페이지: 연료 효율이 높게 운전한 차량</span><span class="sxs-lookup"><span data-stu-id="42f9c-344">Page 5: Fuel Efficiently Driven Vehicles</span></span>  
<span data-ttu-id="42f9c-345">6페이지: Contoso 로고</span><span class="sxs-lookup"><span data-stu-id="42f9c-345">Page 6: Contoso Logo</span></span>  

![연결된 자동차 Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

<span data-ttu-id="42f9c-347">**3페이지에서**, 다음을 고정:</span><span class="sxs-lookup"><span data-stu-id="42f9c-347">**From Page 3**, pin the following:</span></span>  

1. <span data-ttu-id="42f9c-348">vin 개수</span><span class="sxs-lookup"><span data-stu-id="42f9c-348">Count of VIN</span></span>  
   ![연결된 자동차 Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. <span data-ttu-id="42f9c-350">모델별 적극적으로 운전한 차량 - 폭포 차트 </span><span class="sxs-lookup"><span data-stu-id="42f9c-350">Aggressively driven vehicles by model – Waterfall chart</span></span>  
   ![차량 원격 분석 - 차트 4 고정](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

<span data-ttu-id="42f9c-352">**5페이지에서**, 다음을 고정:</span><span class="sxs-lookup"><span data-stu-id="42f9c-352">**From Page 5**, pin the following:</span></span> 

1. <span data-ttu-id="42f9c-353">vin 개수</span><span class="sxs-lookup"><span data-stu-id="42f9c-353">Count of vin</span></span>    
   ![차량 원격 분석 - 차트 5 고정](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. <span data-ttu-id="42f9c-355">모델별 연료 효율이 좋은 차량: 묶은 세로 막대형 차트 </span><span class="sxs-lookup"><span data-stu-id="42f9c-355">Fuel efficient vehicles by model: Clustered column chart</span></span>  
   ![차량 원격 분석 - 차트 6 고정](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

<span data-ttu-id="42f9c-357">**4페이지에서**, 다음을 고정:</span><span class="sxs-lookup"><span data-stu-id="42f9c-357">**From Page 4**, pin the following:</span></span>  

1. <span data-ttu-id="42f9c-358">vin 개수</span><span class="sxs-lookup"><span data-stu-id="42f9c-358">Count of vin</span></span>  
   ![차량 원격 분석 - 차트 7 고정](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. <span data-ttu-id="42f9c-360">시/군/구, 모델별 리콜된 차량: 트리맵 </span><span class="sxs-lookup"><span data-stu-id="42f9c-360">Recalled vehicles by city, model: Treemap</span></span>  
   ![차량 원격 분석 - 차트 8 고정](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

<span data-ttu-id="42f9c-362">**6페이지에서**, 다음을 고정:</span><span class="sxs-lookup"><span data-stu-id="42f9c-362">**From Page 6**, pin the following:</span></span>  

1. <span data-ttu-id="42f9c-363">Contoso 모터 로고 </span><span class="sxs-lookup"><span data-stu-id="42f9c-363">Contoso Motors logo</span></span>  
   ![차량 원격 분석 - 차트 9 고정](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

<span data-ttu-id="42f9c-365">**대시보드 구성**</span><span class="sxs-lookup"><span data-stu-id="42f9c-365">**Organize the dashboard**</span></span>  

1. <span data-ttu-id="42f9c-366">대시보드로 이동</span><span class="sxs-lookup"><span data-stu-id="42f9c-366">Navigate to the dashboard</span></span>
2. <span data-ttu-id="42f9c-367">각 차트 위를 마우스로 가리키고 아래의 완전한 대시보드 이미지에 제공된 이름에 따라 이름을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-367">Hover over each chart and rename it based on the naming provided in the complete dashboard image below.</span></span> <span data-ttu-id="42f9c-368">또한 아래 대시보드보드와 같이 표시되도록 차트를 이리저리 움직입니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-368">Also move the charts around to look like the dashboard below.</span></span>  
   ![차량 원격 분석 - 대시보드 2 구성](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![차량 원격 분석 Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. <span data-ttu-id="42f9c-371">이 문서에서 설명한 대로 모든 보고서를 만든 경우 최종 완료된 대시보드는 다음 그림처럼 보여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-371">If you have created all the reports as mentioned in this document, the final completed dashboard should look like the following figure.</span></span> 

![차량 원격 분석 - 대시보드 2 구성](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

<span data-ttu-id="42f9c-373">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-373">Congratulations!</span></span> <span data-ttu-id="42f9c-374">차량 상태 및 운전 습관을 실시간으로 예측 가능하며 배치 통찰력을 얻을 수 있는 보고서 및 대시보드를 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="42f9c-374">You have successfully created the reports and the dashboard to gain real-time, predictive and batch insights on vehicle health and driving habits.</span></span>  
