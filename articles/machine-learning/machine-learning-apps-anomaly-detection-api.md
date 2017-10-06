---
title: "시스템 학습 변칙 검색 API aaaAzure | Microsoft Docs"
description: "이상 감지 API는 Microsoft Azure 기계 학습을 사용하여 빌드한 예로서, 시간 간격이 불균일한 숫자 값이 있는 시계열 데이터에서 이상을 감지합니다."
services: machine-learning
documentationcenter: 
author: alokkirpal
manager: jhubbard
editor: cgronlun
ms.assetid: 52fafe1f-e93d-47df-a8ac-9a9a53b60824
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/05/2017
ms.author: alok;rotimpe
ms.openlocfilehash: ce153689b8ddb36b67a2ad3607d846ea83ebcf61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-anomaly-detection-api"></a>Machine Learning 이상 감지 API
## <a name="overview"></a>개요
[이상 감지 API](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2)는 Azure Machine Learning을 사용하여 빌드한 예로서, 시간 간격이 불균일한 숫자 값이 있는 시계열 데이터에서 이상을 감지합니다.

이 API는 hello 시계열 데이터의 비정상적인 패턴 유형 중 다음을 검색할 수 있습니다.

* **긍정적인 추세 및 부정적인 추세**: 예를 들어, 계산에서 메모리 사용량을 모니터링 할 때, 상향 추세는 메모리 누수를 나타낼 수 있기 때문에 유용할 수 있습니다.
* **Hello 동적 값 범위에 대 한 변경 내용을**: 예를 들어 클라우드 서비스에서 발생 한 hello 예외를 모니터링할 때는 hello 동적 값 범위에 변경 내용을 수 불안정 해 졌음을 나타낼 hello 서비스의 상태를 hello 및
* **스파이크 및 Dip**: 예를 들어 hello 서비스에 로그인 실패 또는 전자 상거래 사이트의 체크 아웃의 수를 모니터링할 때는 스파이크 또는 dip 나타낼 수 비정상적인 동작 합니다.

이러한 기계 학습 감지기는 시간에 따른 값의 변화를 추적하여 해당 값의 계속적인 변화를 이상 점수로 보고합니다. Adhoc 임계값을 조정 하지 않아도 및의 점수 사용된 toocontrol false 양의 비율 일 수 있습니다. hello 변칙 검색 API는 사용 시간에 따른 Kpi를 추적 하 여 모니터링 서비스와 같은 여러 가지 시나리오에서 유용 검색, 수가 한 번의 클릭 수와 같은 메트릭을 통해 모니터링할 성능 카운터 메모리, CPU, 파일 처럼 통해 모니터링 읽기, 시간이 지남에 따라 등입니다.

이상 탐지 제공 hello 시작한 유용한 도구 tooget 함께 제공 됩니다.

* hello [웹 응용 프로그램](http://anomalydetection-aml.azurewebsites.net/) 평가 하 고 데이터에 대해 비정상 검색 Api의 hello 결과 시각화 하는 데 도움이 됩니다.

> [!NOTE]
> [이 API](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2)에서 제공되는 **IT Anomaly Insights 솔루션**을 사용해 봅니다.
> 
> tooget이 최종 tooend 솔루션 배포 tooyour Azure 구독 <a href="https://gallery.cortanaintelligence.com/Solution/Anomaly-Detection-Pre-Configured-Solution-1" target="_blank"> **여기서 시작 >**</a>
> 
>

## <a name="api-deployment"></a>API 배포
순서 toouse hello API에 배포 해야 tooyour Azure 구독으로 Azure 기계 학습 웹 서비스에 호스트 됩니다.  Hello에서 이렇게 하려면 [Cortana 인텔리전스 갤러리](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2)합니다.  두 AzureML 웹 서비스 (및 해당 관련된 리소스)을 배포 합니다 tooyour Azure 구독-계절성 검색 된 이상 탐지에 대 한 및 계절성 검색 하지 않고 있습니다.  Hello 배포 완료 되 면 사용할 수 없게 toomanage에서 Api hello [AzureML 웹 서비스](https://services.azureml.net/webservices/) 페이지.  이 페이지에서는 있습니다 됩니다 수 수 toofind API 키 위치를 끝점으로 hello API를 호출 하는 것에 대 한 코드 샘플.  더 자세한 지침은 [여기](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-manage-new-webservice)에 있습니다.

## <a name="scaling-hello-api"></a>크기 조정 hello API
기본적으로 배포에는 1,000 트랜잭션/월 및 2 계산 시간/월을 포함하는 무료 개발/테스트 청구 계획이 있습니다.  필요에 따라 tooanother 계획을 업그레이드할 수 있습니다.  다양 한 계획의 가격 책정 hello에 대 한 세부 정보를 사용할 수 있는 [여기](https://azure.microsoft.com/en-us/pricing/details/machine-learning/) "프로덕션 웹 API 가격" 아래에서 합니다.

## <a name="managing-aml-plans"></a>AML 관리 계획 
[여기](https://services.azureml.net/plans/)서 청구 계획을 관리할 수 있습니다.  hello 계획 이름은 hello API를 배포 하는 경우 선택한 hello 리소스 그룹 이름을 비롯 한 고유 tooyour 구독 하는 문자열에 따라 달라 집니다.  어떻게 tooupgrade 계획에 사용할 수 있는 지침은 [여기](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-manage-new-webservice) hello "청구 계획 관리" 섹션.

## <a name="api-definition"></a>API 정의
hello 웹 서비스를 제공 하는 REST 기반 API는 웹 또는 R, Python, Excel, 모바일 응용 프로그램을 비롯 한 다양 한 방식으로 사용할 수 있는 HTTPS를 통해 등입니다.  시간 시계열 데이터 toothis 서비스 REST API 호출을 통해 보내고 hello 세 가지 예외 형식 아래에 설명 된 조합을 실행 합니다.

## <a name="calling-hello-api"></a>Hello API 호출
순서 toocall hello API에서 tooknow hello 끝점 위치와 API 키가 필요 합니다.  Hello에서 사용할 수 있는 hello API를 호출 하는 것에 대 한 샘플 코드와 함께 이러한 둘 다 [AzureML 웹 서비스](https://services.azureml.net/webservices/) 페이지.  원하는 toohello API 이동한 다음 클릭 hello "사용" 탭 toofind 해당 합니다.  Swagger API로 hello API를 호출할 수 있습니다 (hello URL 매개 변수와 함께, 즉 `format=swagger`) 또는으로 비-Swagger API를 (즉, hello 없이 `format` URL 매개 변수).  hello 샘플 코드는 hello Swagger 형식을 사용합니다.  아래는 Swagger가 아닌 형식의 예제 요청 및 응답입니다.  이러한 예제는 toohello 계절성 끝점.  hello 비 계절성 끝점은 유사 합니다.

### <a name="sample-request-body"></a>샘플 요청 본문
두 개체를 포함 하는 hello 요청: `Inputs` 및 `GlobalParameters`합니다.  Hello 예제 요청 아래에 일부 매개 변수는 명시적으로 하는 동안 전송 되지 않습니다 (전체 목록은 각 끝점에 대 한 매개 변수 아래로 스크롤하여).  Hello 요청에 명시적으로 전송 되지 않습니다는 매개 변수는 아래에 지정 된 hello 기본값을 사용 합니다.

    {
                "Inputs": {
                        "input1": {
                                "ColumnNames": ["Time", "Data"],
                                "Values": [
                                        ["5/30/2010 18:07:00", "1"],
                                        ["5/30/2010 18:08:00", "1.4"],
                                        ["5/30/2010 18:09:00", "1.1"]
                                ]
                        }
                },
        "GlobalParameters": {
            "tspikedetector.sensitivity": "3",
            "zspikedetector.sensitivity": "3",
            "bileveldetector.sensitivity": "3.25",
            "detectors.spikesdips": "Both"
        }
    }

### <a name="sample-response"></a>샘플 응답
이때 순서 toosee hello에 `ColumnNames` 포함 해야 필드 `details=true` 요청에 URL 매개 변수입니다.  이러한 각 필드에 있으며 hello 의미에 대 한 아래 hello 테이블을 참조 하십시오.

    {
        "Results": {
            "output1": {
                "type": "table",
                "value": {
                    "Values": [
                        ["5/30/2010 6:07:00 PM", "1", "1", "0", "0", "-0.687952590518378", "0", "-0.687952590518378", "0", "-0.687952590518378", "0"],
                        ["5/30/2010 6:08:00 PM", "1.4", "1.4", "0", "0", "-1.07030497733224", "0", "-0.884548154298423", "0", "-1.07030497733224", "0"],
                        ["5/30/2010 6:09:00 PM", "1.1", "1.1", "0", "0", "-1.30229513613974", "0", "-1.173800281031", "0", "-1.30229513613974", "0"]
                    ],
                    "ColumnNames": ["Time", "OriginalData", "ProcessedData", "TSpike", "ZSpike", "BiLevelChangeScore", "BiLevelChangeAlert", "PosTrendScore", "PosTrendAlert", "NegTrendScore", "NegTrendAlert"],
                    "ColumnTypes": ["DateTime", "Double", "Double", "Double", "Double", "Double", "Int32", "Double", "Int32", "Double", "Int32"]
                }
            }
        }
    }


## <a name="score-api"></a>Score API
hello 점수 API 없는 seasonal 시계열 데이터에서 변칙 검색을 실행 하는 데 사용 됩니다. hello API hello 데이터에 대해 다양 한 비정상 검색기를 실행 하 고의 비정상 점수를 반환 합니다. hello 아래 그림은 예 예외의 해당 hello 점수 API 감지할 수 있습니다. 이 시계열에는 두 개의 뚜렷한 수준 변화와 세 개의 급증이 있습니다. hello 빨간색 점은 hello에서 수준 변경이 감지 되 면 hello 검정 점 검색 hello 스파이크를 표시 하는 동안 hello 시간을 표시 합니다.
![점수 매기기 API][1]

### <a name="detectors"></a>감지기
hello 이상 탐지 API 3 광범위 한 범주에서 검색기를 지원합니다. 다음 표에 hello에 특정 입력된 매개 변수 및 각 탐지기에 대 한 출력에 대 한 세부 정보를 찾을 수 있습니다.

| 감지기 범주 | 감지기 | 설명 | 입력 매개 변수 | 출력 |
| --- | --- | --- | --- | --- |
| 급증 감지기 |TSpike 감지기 |스파이크 및 값은 첫 번째 및 세 번째 변 위치에서 먼 hello에 따라 dip를 검색 합니다. |*tspikedetector.sensitivity:* hello 범위의 정수 값 1-10, 기본 사용: 3; 값이 높을수록 더 많은 극단적인 값 있기 때문 덜 중요 한 catch |TSpike: 이진 값 – 급증/급락이 감지되면 ‘1’, 그 외 경우는 ‘0’ |
| 급증 감지기 | ZSpike 감지기 |평균에서을 스파이크 및 dip 얼마나 hello 데이터 요소에 따라 검색 |*zspikedetector.sensitivity:* hello 범위의 정수 값 1-10, 기본 사용: 3; 값이 높을수록 덜 중요 하므로 더 많은 극단적인 값을 catch 합니다. |ZSpike: 이진 값 – 급증/급락이 감지되면 ‘1’, 그 외 경우는 ‘0’ | |
| 느린 추세 감지기 |느린 추세 감지기 |Hello 집합 민감도 따라 느린 긍정적인 추세를 검색 합니다. |*trenddetector.sensitivity:* 탐지기 점수에 대 한 임계값 (기본값:, 3.25 3.25-5는 적당 한 범위 tooselect에서이; 구분 보다 더 높은 hello hello) |tscore: 추세에 대한 이상 점수를 나타내는 부동 소수점 숫자 |
| 수준 변화 감지기 | 양방향 수준 변화 감지기 |Hello 집합 민감도 따라 상향 및 하향 수준 변경 내용을 검색합니다 |*bileveldetector.sensitivity:* 탐지기 점수에 대 한 임계값 (기본값:, 3.25 3.25-5는 적당 한 범위 tooselect에서이; 구분 보다 더 높은 hello hello) |rpscore: 상향 및 하향 수준 변화에 대한 이상 점수를 나타내는 부동 소수점 숫자 | |

### <a name="parameters"></a>매개 변수
이러한 입력된 매개 변수에 대 한 자세한 내용은 아래 hello 표에 나열 됩니다.

| 입력 매개 변수 | 설명 | 기본 설정 | 형식 | 유효 범위 | 제안 범위 |
| --- | --- | --- | --- | --- | --- |
| detectors.historyWindow |이상 점수 계산에 사용된 내역(데이터 요소 수) |500 |정수 |10-2000 |시계열에 종속 |
| detectors.spikesdips | Toodetect만 급증 여부, 유일한 dip 또는 둘 다 |둘 다 |열거형 |Both, Spikes, Dips |둘 다 |
| bileveldetector.sensitivity |양방향 수준 변화 감지기에 대한 민감도. |3.25 |double |없음 |3.25-5(값이 낮을수록 높은 민감도) |
| trenddetector.sensitivity |긍정적인 추세 감지에 대한 민감도. |3.25 |double |없음 |3.25-5(값이 낮을수록 높은 민감도) |
| tspikedetector.sensitivity |TSpike 감지기의 민감도 |3 |정수 |1-10 |3-5(값이 낮을수록 높은 민감도) |
| zspikedetector.sensitivity |ZSpike 감지기의 민감도 |3 |정수 |1-10 |3-5(값이 낮을수록 높은 민감도) |
| postprocess.tailRows |Hello 최신 데이터 요소 수의 toobe hello 결과 출력에 유지 |0 |정수 |0 (모든 데이터 요소 유지), 하거나 결과에 tookeep 포인트의 수를 지정 합니다. |해당 없음 |

### <a name="output"></a>출력
hello API 프로그램 시계열 데이터에서 모든 검색기를 실행 하 고 시간에서 비정상 점수와 각 지점에 대 한 이진 스파이크 표시기를 반환 합니다. hello 아래 표에 hello API에서에서 출력 합니다. 

| outputs | 설명 |
| --- | --- |
| Time |원시 데이터의 타임스탬프 또는 집계 (및/또는) 누락 데이터 대체가 적용되는 경우 집계 (및/또는) 대체된 데이터 |
| Data |원시 데이터의 값 또는 집계 (및/또는) 누락 데이터 대체가 적용되는 경우 집계 (및/또는) 대체된 데이터 |
| Tspike |이진 표시기 tooindicate 스파이크가 TSpike 탐지기에서 인식 되는지 여부 |
| ZSpike |이진 표시기 tooindicate 스파이크가 ZSpike 탐지기에서 인식 되는지 여부 |
| rpscore |양방향 수준 변화에 대한 이상 점수를 나타내는 부동 소수점 숫자 |
| rpalert |양방향 수준을 나타내는 값이 1/0 비정상 hello 입력된 민감도에 따라 변경 |
| tscore |긍정적인 추세에 대한 이상 점수를 나타내는 부동 소수점 숫자 |
| talert |값이 나타내는 1/0은 hello 입력된 민감도에 따라 긍정적인 추세 비정상 |

## <a name="scorewithseasonality-api"></a>ScoreWithSeasonality API
hello ScoreWithSeasonality API 주기적인 패턴을 사용할 수 있는 시계열에서 변칙 검색을 실행 하는 데 사용 됩니다. 이 API는 주기적인 패턴에서 유용한 toodetect 편차.  
hello 다음 그림의 예가 나와 계절별 시계열에서 발견 되는 예외입니다. hello 시계열 하나의 스파이크 (hello 1 검은색 점), (2 일 검정색 점이 hello 및 hello 끝에 하나씩), 두 개의 dip 및 하나의 수준 변경 (빨간 점)에 있습니다. Hello 시계열 및 hello 수준 변경의 hello 중간에서 dip를 hello 둘 다는 확연히 계절 관련 구성 요소는 hello 계열에서 제거 됩니다.
![계절성 API][2]

### <a name="detectors"></a>감지기
hello 탐지기 hello 계절성 끝점에는 hello 비 계절성 끝점에 이지만 약간 다른 매개 변수 이름 (아래 참조)와 비슷한 toohello 것입니다.

### <a name="parameters"></a>매개 변수

이러한 입력된 매개 변수에 대 한 자세한 내용은 아래 hello 표에 나열 됩니다.

| 입력 매개 변수 | 설명 | 기본 설정 | 형식 | 유효 범위 | 제안 범위 |
| --- | --- | --- | --- | --- | --- |
| preprocess.aggregationInterval |입력 시계열 집계에 대한 초 단위 집계 간격 |0(집계가 수행되지 않음) |정수 |0: 집계 건너뜀, > 0 기타 |시계열 종속 too1 하루 5 분 |
| preprocess.aggregationFunc |Hello에 데이터를 집계에 사용 되는 함수 AggregationInterval 지정 |평균 |열거형 |평균, 합계, 길이 |해당 없음 |
| preprocess.replaceMissing |Tooimpute 누락 된 데이터를 사용 하는 값 |lkv(마지막으로 알려진 값) |열거형 |0, lkv, 평균 |해당 없음 |
| detectors.historyWindow |이상 점수 계산에 사용된 내역(데이터 요소 수) |500 |정수 |10-2000 |시계열에 종속 |
| detectors.spikesdips | Toodetect만 급증 여부, 유일한 dip 또는 둘 다 |둘 다 |열거형 |Both, Spikes, Dips |둘 다 |
| bileveldetector.sensitivity |양방향 수준 변화 감지기에 대한 민감도. |3.25 |double |없음 |3.25-5(값이 낮을수록 높은 민감도) |
| postrenddetector.sensitivity |긍정적인 추세 감지에 대한 민감도. |3.25 |double |없음 |3.25-5(값이 낮을수록 높은 민감도) |
| negtrenddetector.sensitivity |부정적인 추세 감지기에 대한 민감도 |3.25 |double |없음 |3.25-5(값이 낮을수록 높은 민감도) |
| tspikedetector.sensitivity |TSpike 감지기의 민감도 |3 |정수 |1-10 |3-5(값이 낮을수록 높은 민감도) |
| zspikedetector.sensitivity |ZSpike 감지기의 민감도 |3 |정수 |1-10 |3-5(값이 낮을수록 높은 민감도) |
| seasonality.enable |계절성 분석 toobe 인지 수행 |true |부울 |true, false |시계열에 종속 |
| seasonality.numSeasonality |최대 검색 주기 주기 toobe 수 |1 |정수 |1, 2 |1-2 |
| seasonality.transform |이상 감지를 적용하기 전에 계절성 (및) 추세 구성 요소가 제거될지 여부 |deseason |열거형 |none, deseason, deseasontrend |해당 없음 |
| postprocess.tailRows |Hello 최신 데이터 요소 수의 toobe hello 결과 출력에 유지 |0 |정수 |0 (모든 데이터 요소 유지), 하거나 결과에 tookeep 포인트의 수를 지정 합니다. |해당 없음 |

### <a name="output"></a>출력
hello API 프로그램 시계열 데이터에서 모든 검색기를 실행 하 고 시간에서 비정상 점수와 각 지점에 대 한 이진 스파이크 표시기를 반환 합니다. hello 아래 표에 hello API에서에서 출력 합니다. 

| outputs | 설명 |
| --- | --- |
| Time |원시 데이터의 타임스탬프 또는 집계 (및/또는) 누락 데이터 대체가 적용되는 경우 집계 (및/또는) 대체된 데이터 |
| OriginalData |원시 데이터의 값 또는 집계 (및/또는) 누락 데이터 대체가 적용되는 경우 집계 (및/또는) 대체된 데이터 |
| ProcessedData |Hello 다음 중 하나: <ul><li>명확한 계절성이 감지되고 deseason 옵션이 선택된 경우 계절에 따라 조정된 시계열</li><li>명확한 계절성이 감지되고 deseasontrend 옵션이 선택된 경우 계절에 따라 조정되고 추세가 제거된 시계열</li><li>그렇지 않은 경우이 hello OriginalData와 동일</li> |
| Tspike |이진 표시기 tooindicate 스파이크가 TSpike 탐지기에서 인식 되는지 여부 |
| ZSpike |이진 표시기 tooindicate 스파이크가 ZSpike 탐지기에서 인식 되는지 여부 |
| BiLevelChangeScore |수준 변화에 대한 이상 점수를 나타내는 부동 소수점 숫자 |
| BiLevelChangeAlert |hello 입력된 민감도에 따라 수준 변경이 비정상 상태는 1/0 값을 나타내는 있습니다. |
| PosTrendScore |긍정적인 추세에 대한 이상 점수를 나타내는 부동 소수점 숫자 |
| PosTrendAlert |값이 나타내는 1/0은 hello 입력된 민감도에 따라 긍정적인 추세 비정상 |
| NegTrendScore |부정적인 추세에 대한 이상 점수를 나타내는 부동 소수점 숫자 |
| NegTrendAlert |값이 나타내는 1/0은 hello 입력된 민감도에 따라 부정적인 추세 비정상 |

[1]: ./media/machine-learning-apps-anomaly-detection-api/anomaly-detection-score.png
[2]: ./media/machine-learning-apps-anomaly-detection-api/anomaly-detection-seasonal.png

