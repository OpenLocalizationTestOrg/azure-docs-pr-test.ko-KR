---
title: "aaaDiagnose 및 문제 해결 | Microsoft Docs"
description: "이 자습서에서는 어떻게 toodiagnose 시간 시계열 Insights 환경에서 문제를 해결 하 고"
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/24/2017
ms.author: venkatja
ms.openlocfilehash: 00893d4bec497f5f8bf7093be5b96f1844446d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-and-solve-problems-in-your-time-series-insights-environment"></a>Time Series Insights 환경에서 문제 진단 및 해결

## <a name="i-dont-see-my-data"></a>내 데이터가 표시되지 않습니다.
이유를 확인할 수 있습니다 데이터 hello 사용자 환경에서 몇 가지 원인은 다음과 같습니다 [Azure 시간 계열 Insights 포털](https://insights.timeseries.azure.com)합니다.

### <a name="your-event-source-doesnt-have-data-in-json-format"></a>이벤트 원본에 JSON 형식의 데이터가 없습니다.
Azure Time Series Insights는 현재 JSON 데이터만 지원합니다. JSON 샘플의 경우 [지원되는 JSON 셰이프](time-series-insights-send-events.md#supported-json-shapes)를 참조하세요.

### <a name="when-you-registered-your-event-source-you-didnt-provide-hello-key-that-has-hello-required-permission"></a>Hello 필요한 권한이 있는 hello 키를 지정 하지 않은 이벤트 원본이 등록
* IoT hub에 있는 tooprovide hello 키가 필요한 **서비스 연결** 권한.

   ![Iot Hub 서비스 연결 사용 권한](media/diagnose-and-solve-problems/iothub-serviceconnect-permissions.png)

   Hello 이미지를 앞에 표시 된 대로 hello 정책 중 하나 **iothubowner** 및 **서비스** 작동할 것 이므로 둘 다 **서비스 연결** 권한.
* 이벤트 허브에 대 한 필요한 tooprovide hello에 **수신** 권한.

   ![이벤트 허브 수신 사용 권한](media/diagnose-and-solve-problems/eventhub-listen-permissions.png)

   Hello 이미지를 앞에 표시 된 대로 hello 정책 중 하나 **읽을** 및 **관리** 둘 다 때문에 작동할 것 **수신** 권한.

### <a name="hello-provided-consumer-group-is-not-exclusive-tootime-series-insights"></a>hello 제공 소비자 그룹이 단독 tooTime 시리즈 Insights 않습니다.
IoT 허브 또는 이벤트 허브에 대 한 등록 하는 동안 해야 데이터를 읽는 데 사용 해야 하는 toospecify hello 소비자 그룹입니다. 이 소비자 그룹은 공유하지 않아야 합니다. 공유 하는 경우 hello 기본 이벤트 허브 자동으로 연결을 끊습니다 hello 판독기 중 하나가 임의로.

## <a name="i-see-my-data-but-theres-a-lag"></a>내 데이터가 표시되지만 시간이 지연됩니다.
Hello 사용자 환경에서 불완전 한 데이터가 표시 될 수는 이유는 이유는 [시간 시계열 Insights 포털](https://insights.timeseries.azure.com)합니다.

### <a name="your-environment-is-getting-throttled"></a>사용자 환경이 제한적입니다.
제한은 hello hello 환경 SKU 형식 및 용량에 따라 적용 됩니다. Hello 환경에서 모든 이벤트 소스가이 용량을 공유합니다. IoT hub 및 이벤트 허브에 대 한 hello 이벤트 소스에 적용 하는 hello 제한 초과 하 여 데이터 푸시합니다, 제한 및 간격 표시 됩니다.

다음 다이어그램 hello S1 SKU와 3의 용량이 있는 시간 시계열 Insights 환경을 보여 줍니다. 하루에 3백만 개의 이벤트를 수신할 수 있습니다.

![환경 SKU 현재 용량](media/diagnose-and-solve-problems/environment-sku-current-capacity.png)

이 환경 hello 수신 속도가 hello 다음 다이어그램에에서 표시 된 이벤트 허브에서 메시지 수집 되는 가정 합니다.

![이벤트 허브에 대한 예제 수신 속도](media/diagnose-and-solve-problems/eventhub-ingress-rate.png)

Hello 다이어그램에 나와 있는 것 처럼 수신 속도 매일 hello ~ 67,000 메시지입니다. 이 속도 변환 대략 too46 메시지 1 분 마다. 각 이벤트 허브 메시지는 일반된 tooa 단일 시간 시계열 Insights 이벤트를 하는 경우이 환경 스로틀이 확인 합니다. 각 이벤트 허브 메시지 일반된 too100 시간 계열 Insights 이벤트 이면 다음 4600 이벤트 해야 수 ingested 1 분 마다. 용량이 3인 S1 SKU 환경은 1분마다 2,100 이벤트만 수신할 수 있습니다(일별 1백만 이벤트 = 3 단위에서 분당 700 이벤트 = 분당 2,100 이벤트). 따라서 간격을 볼 due toothrottling 합니다. 

평면화 논리 작동 방식을 깊이 이해하기 위해서는 [지원되는 JSON 셰이프](time-series-insights-send-events.md#supported-json-shapes)를 참조하세요.

#### <a name="recommended-steps"></a>권장되는 단계
사용자 환경의 SKU 용량 증가 hello toofix hello 지연 합니다. 자세한 내용은 참조 [어떻게 tooscale 시간 시계열 Insights 환경](time-series-insights-how-to-scale-your-environment.md)합니다.

### <a name="youre-pushing-historical-data-and-causing-slow-ingress"></a>기록 데이터를 푸시하고 있어서 수신이 느려지고 있습니다.
기존 이벤트 원본에 연결되어 있는 경우 이미 IoT Hub 또는 이벤트 허브에 데이터가 있을 수 있습니다. 따라서 hello 환경 hello 이벤트 소스 메시지 보존 기간의 hello 시작 부분에서 데이터를 가져올 시작 합니다. 

이 동작은 hello 기본 동작이 며 재정의할 수 없습니다. 제한 하는 의견을 교환 수 및 시간이 걸릴 수 있습니다 toocatch를 기록 데이터를 수집 하는 방법에 있습니다.

#### <a name="recommended-steps"></a>권장되는 단계
단계를 수행 하는 내용이 hello toofix hello 지연:
1. Hello SKU 용량 toohello 최대를 허용 값 (이 경우에는 10)을 늘립니다. Hello 용량을 증가 시켜 훨씬 더 빠르게 잡고 hello 수신 프로세스를 시작 합니다. Hello에 hello 가용성 차트를 통해 잡고 하는 속도 시각화할 수 [시간 시계열 Insights 포털](https://insights.timeseries.azure.com)합니다. 증가 하는 hello 용량에 대 한 요금이 청구 됩니다.
2. Hello 지연 검색은 후 hello SKU 용량 백 tooyour 일반 수신 속도를 줄입니다.

## <a name="my-event-sources-timestamp-property-name-setting-doesnt-work"></a>내 이벤트 원본 *타임 스탬프 속성 이름* 설정이 작동하지 않습니다.
규칙에 따라 toohello hello 이름 및 값을 따르는지 확인 합니다.
* hello 타임 스탬프 속성 이름이 _대/소문자 구분_합니다.
* 이벤트 소스로 JSON 문자열에서 발생 하는 hello 타임 스탬프 속성 값에는 hello 형식 있어야 _yyyy-m M-ddTHH:mm:ss 합니다. FFFFFFFK_합니다. 이러한 문자열의 예는 “2008-04-12T12:53Z”입니다.
