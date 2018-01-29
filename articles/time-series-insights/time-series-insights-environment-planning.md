---
title: "Azure Time Series Insights 환경의 규모 계획 | Microsoft Docs"
description: "이 문서에서는 저장소 용량, 데이터 보존, 수집 용량, 모니터링 모범 사례에 따라 Azure Time Series Insights 환경을 계획하는 방법을 설명합니다."
services: time-series-insights
ms.service: time-series-insights
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: MicrosoftDocs/tsidocs
ms.reviewer: v-mamcge, jasonh, kfile, anshan
ms.devlang: csharp
ms.workload: big-data
ms.topic: article
ms.date: 11/15/2017
ms.openlocfilehash: 5fb158ba162dd199f419f9568de08a7a18c833dd
ms.sourcegitcommit: 9a61faf3463003375a53279e3adce241b5700879
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2017
---
# <a name="plan-your-azure-time-series-insights-environment"></a>Azure Time Series Insights 환경 계획

이 문서에서는 예상되는 수집 속도와 데이터 보존 요구 사항에 따라 Azure Time Series Insights 환경을 계획하는 방법을 설명합니다.

## <a name="best-practices"></a>모범 사례

Time Series Insights를 시작하려면 분당 얼마만큼의 데이터를 수집할지 그리고 데이터를 얼마나 오래 저장해야 하는지 사전에 파악하는 것이 좋습니다.  

두 Time Series Insights SKU의 용량 및 보존에 대한 자세한 내용은 [Time Series Insights 가격](https://azure.microsoft.com/pricing/details/time-series-insights/)을 참조하세요.

장기적인 안목에서 최상의 환경을 계획하려면 다음을 고려해야 합니다. 
- 저장소 용량
- 데이터 보존 기간
- 수집 용량 

## <a name="understand-storage-capacity"></a>저장소 용량의 이해
기본적으로 Time Series Insights는 사용자가 프로비전한 저장소 용량(단위 곱하기 단위당 저장소의 시간)과 수집 용량을 기준으로 데이터를 보존합니다.

## <a name="understand-data-retention"></a>데이터 보존의 이해
Time Series Insights 환경의 **데이터 보존 시간** 설정을 구성하여 최대 400일 동안 보존할 수 있습니다.  Time Series Insights에는 두 가지 모드가 있습니다. 하나는 환경에 최신 데이터가 있도록 최적화하는 것(기본값)이고, 다른 하나는 보존 한도에 맞도록 최적화하는 것입니다. 후자의 경우 환경에서 전체 저장소 용량에 도달하면 수집이 일시 중지됩니다.  Azure Portal의 환경 구성 페이지에서 보존 방법을 조정하고 두 가지 모드 중 하나를 선택할 수 있습니다.

Time Series Insights 환경에서 최대 400일까지 데이터가 보존되도록 구성할 수 있습니다.

## <a name="configure-data-retention"></a>데이터 보존 구성하기

1. [Azure Portal](https://portal.azure.com)에서 Time Series Insights 환경을 선택합니다.

2. **Time Series Insights 환경 페이지**의 **설정** 아래에서 **구성**을 선택합니다. 

3. **데이터 보존 시간(일)** 상자에 1~400 사이의 값을 입력합니다.

   ![보존 구성하기](media/environment-mitigate-latency/configure-retention.png)

## <a name="understand-ingress-capacity"></a>수집 용량의 이해

계획 시 주의해야 할 또 다른 영역은 수집 용량입니다. 수집 용량은 분당 할당의 파생 항목입니다. 

제한 관점에서, 패킷 크기가 32KB인 수신 데이터 패킷은 각각 1KB 크기의 32개 이벤트로 처리됩니다. 최대 허용 이벤트 크기는 32KB입니다. 32KB보다 큰 데이터 패킷은 잘립니다.

다음 표에서 각 SKU의 수집 용량을 확인할 수 있습니다.

|SKU  |단위당 월별 이벤트 개수  |단위당 월별 이벤트 크기  |단위당 분당 이벤트 개수  | 단위당 분당 크기   |
|---------|---------|---------|---------|---------|
|S1     |   3천만     |  30GB     |  700    |  700KB   |
|S2     |   3억    |   300GB   | 7,000   | 7,000KB  |

하나의 환경에서 S1 또는 S2 SKU의 용량을 10개의 단위로 늘릴 수 있습니다. S1 환경을 S2 환경으로 또는 S2 환경을 S1 환경으로 마이그레이션할 수는 없습니다. 

수집 용량의 경우 먼저 매월 필요한 총 수집 용량을 결정합니다. 그런 다음 제한 및 대기 시간이 중요하게 작용하는 분당 용량을 결정합니다.

데이터 수집 용량의 급증이 24시간 미만 지속되는 경우, Time Series Insights가 위에 표시된 속도보다 2배 높은 수집 속도로 이를 따라잡을 수 있습니다. 

예를 들어 하나의 S1 SKU에서 분당 이벤트 700개의 데이터 수집 속도를 갖고 있는데 1시간 미만 동안 시간당 1,400개 이하의 속도로 급증이 발생하는 경우, 환경에서 뚜렷이 감지되는 대기 시간은 없습니다. 그러나 1시간이 넘도록 분당 1,400개 이벤트의 속도가 지속되면 대기 시간을 경험하게 되며, 이는 환경에서 시각화되어 쿼리할 수 있습니다. 

예상되는 데이터 푸시 용량을 사전에 예측하기 어려울 수 있습니다. 이 경우 Azure Portal에서 [Azure IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-metrics) 및 [Azure Event Hubs](https://blogs.msdn.microsoft.com/cloud_solution_architect/2016/05/25/using-the-azure-rest-apis-to-retrieve-event-hub-metrics/)의 데이터 텔레메트리를 찾을 수 있습니다. 텔레메트리를 바탕으로 환경을 어떻게 프로비전해야 할지 판단할 수 있습니다. Azure Portal의 **메트릭** 페이지에서 개별 이벤트 소스의 텔레메트리를 확인할 수 있습니다. 이벤트 소스 메트릭을 파악하면 Time Series Insights 환경을 더 효과적으로 계획하고 프로비전하는 데 도움이 됩니다.

## <a name="calculate-ingress-requirements"></a>수집 요구 사항 계산하기

- 수집 용량이 분당 평균 속도보다 높고, 1시간 미만 동안 용량의 2배에 해당하는 예상 수집 용량을 처리할 만큼 환경의 규모가 커야 합니다.

- 수집 용량 급증이 1시간 미만으로 지속되는 경우, 급증한 속도를 평균값으로 사용하여 급증 속도를 처리할 수 있는 용량으로 환경을 프로비전합니다.
 
## <a name="mitigate-throttling-and-latency"></a>제한 및 대기 시간에 대응하기

제한 및 대기 시간을 방지하는 자세한 방법은 [대기 시간 및 제한 완화](time-series-insights-environment-mitigate-latency.md)를 참조하세요. 

## <a name="next-steps"></a>다음 단계
- [Event Hub 이벤트 소스를 추가하는 방법](time-series-insights-how-to-add-an-event-source-eventhub.md)
- [IoT Hub 이벤트 소스를 추가하는 방법](time-series-insights-how-to-add-an-event-source-iothub.md)
