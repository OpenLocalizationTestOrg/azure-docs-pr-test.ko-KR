---
title: "Azure 스트림 분석 및 AzureML 함수와 함께 크기 조정 aaaJob | Microsoft Docs"
description: "Tooproperly 스트림 분석 작업 (분할 SU 수량 등)를 확장 하는 방법을 알아보려면 Azure 기계 학습 함수를 사용 하는 경우."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 47ce7c5e-1de1-41ca-9a26-b5ecce814743
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3fbdfaf7e8e86896c56f1d18bbde3a10bd3dca04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-stream-analytics-job-with-azure-machine-learning-functions"></a>Azure Machine Learning 함수를 사용하여 Stream Analytics 작업의 크기 조정
스트림 분석 작업을 매우 쉽게 tooset 수 있으며 예행 몇 가지 샘플 데이터. 어떻게 해야 하지 toorun 필요한 경우 더 큰 데이터 볼륨 사용 작업이 동일한 hello? 필요 우리 toounderstand 하 게 확장할 수 있도록 tooconfigure hello 스트림 분석 작업 하는 방법. 이 문서에서는 살펴볼 것 hello 크기 조정 스트림 분석의 특별 한 측면에 기계 학습 함수를 사용 하 여 작업입니다. Tooscale 스트림 분석 작업이 hello 문서 일반적 참조 되는 방법에 대 한 내용은 [크기 조정 작업](stream-analytics-scale-jobs.md)합니다.

## <a name="what-is-an-azure-machine-learning-function-in-stream-analytics"></a>Stream Analytics의 Azure Machine Learning 함수란 무엇입니까?
스트림 분석에는 기계 학습 함수 hello 스트림 분석 쿼리 언어에에서는 일반 함수 호출 처럼 사용할 수 있습니다. 그러나 hello 함수 호출 뒤에 hello 장면 실제로 Azure 기계 학습 웹 서비스 요청이 포함 됩니다. 컴퓨터 학습 웹 서비스 최소 일괄 처리 라고 함 지원 "일괄 처리" 여러 행, 동일한 웹 서비스 API 호출, tooimprove hello에 전체 처리량입니다. 자세한 내용은;에 대 한 아티클을 다음 hello를 참조 하세요 [스트림 분석의 azure 기계 학습 함수](https://blogs.technet.microsoft.com/machinelearning/2015/12/10/azure-ml-now-available-as-a-function-in-azure-stream-analytics/) 및 [Azure 컴퓨터 학습 웹 서비스](../machine-learning/machine-learning-consume-web-services.md)합니다.

## <a name="configure-a-stream-analytics-job-with-machine-learning-functions"></a>Machine Learning 함수를 사용하여 Stream Analytics 작업 구성
스트림 분석 작업에 대 한 기계 학습 함수를 구성할 때는 커넥터가 있으며 두 개의 매개 변수 tooconsider hello 기계 학습 함수 호출 및 스트리밍 단위 (SUs) hello 스트림 분석 작업에 대 한 사용자를 프로 비전 하는 hello hello 일괄 처리 크기입니다. 이러한 toodetermine hello의 적절 한 값을 먼저는 내려야 합니다 사이의 대기 시간 및 처리량, 즉, hello 스트림 분석 작업의 대기 시간 및 각 SU의 처리량입니다. SUs 항상 추가할 수 있습니다 올바르게 분할 스트림 분석 쿼리 tooa 작업 tooincrease 처리량 추가 SUs을 사용 하면 실행 중인 hello 작업의 hello 비용.

따라서 변수는 중요 한 toodetermine hello *허용 오차* 스트림 분석 작업에 대 한 대기 시간입니다. Azure 기계 학습 서비스 요청을 실행 중에서 추가 대기 시간 hello 스트림 분석 작업의 대기 시간 hello 복합는 일괄 처리 크기를 자연스럽 게 늘어납니다. Hello 반면, 일괄 처리 크기를 늘리면 허용 hello 스트림 분석 작업 tooprocess * hello로 더 많은 이벤트 *같은 번호* 기계 학습의 웹 서비스 요청 합니다. 기계 학습 웹 서비스 대기 시간 증가 종종 hello은 특정된 상황에서는 기계 학습 웹 서비스에 대 한 중요 한 tooconsider hello 가장 비용 효율적인 일괄 처리 크기 없으므로 일괄 처리 크기의 선형적 toohello 증가 합니다. hello 웹 서비스에 대 한 hello 기본 일괄 처리 크기는 1000 및 hello를 사용 하 여 수정할 수 있습니다 요청 [스트림 분석 REST API](https://msdn.microsoft.com/library/mt653706.aspx "스트림 분석 REST API") 또는 hello [PowerShell 클라이언트 스트림 분석에 대 한](stream-analytics-monitor-and-manage-jobs-use-powershell.md "스트림 분석에 대 한 PowerShell 클라이언트")합니다.

일괄 처리 크기가 결정 되 면 hello 양을 스트리밍 단위 (SUs) 결정 될 수 있습니다 수에 따라 hello 이벤트를 hello 함수 초당 tooprocess를 해야 하는 합니다. 스트리밍 단위에 대한 자세한 내용은 [Stream Analytics 크기 조정 작업](stream-analytics-scale-jobs.md)을 참조하세요.

일반적으로 연결이 20 동시 toohello 기계 학습 웹 서비스에 대 한 모든 6 SUs 제외 하 고 1 SU 작업과 3 SU 작업이 받아볼 20 개의 동시 연결도 있습니다.  예를 들어 hello 입력된 데이터 속도가 초당 200, 000 이벤트 고 hello 일괄 처리 크기는 남아 toohello 1000 hello 결과 웹 서비스 대기 시간 1000 이벤트 최소 일괄 처리의 기본값이 200ms입니다. 이 모든 연결 요청을 수행할 수 5 toohello 기계 학습 웹 서비스에서 초당 것을 의미 합니다. 20 개의 연결 된 hello 스트림 분석 작업이 200ms에 20, 000 이벤트 및 10만 개 이벤트를 따라서 1 초 동안에서 처리할 수 있습니다. 초당 200, 000 tooprocess 이벤트, hello 스트림 분석 작업 필요한 등 40 동시 연결 될 too12 SUs 합니다. hello 다이어그램 아래 hello 스트림 분석 작업 toohello 기계 학습 웹 서비스 끝점의 hello 요청을 보여 줍니다.-모든 6 SUs가 최대 20 동시 연결 tooMachine 학습 웹 서비스를 포함 합니다.

![Machine Learning 함수 2 작업 예제를 사용한 Stream Analytics 크기 조정](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-00.png "Machine Learning 함수 2 작업 예제를 사용한 Stream Analytics 크기 조정")

일반적으로 ***B*** 일괄 처리 크기에 대 한 ***L*** hello 웹 서비스 대기 시간 (밀리초) 일괄 처리 크기 B에서를 사용 하는 스트림 분석 작업의 처리량을 hello ***N*** SUs는:

![Machine Learning 함수 수식을 사용한 Stream Analytics 크기 조정](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-02.png "Machine Learning 함수 수식을 사용한 Stream Analytics 크기 조정")

분석도 고려해 야 hello '최대 동시 호출' hello 기계 학습 웹 서비스 쪽에서을 것이 좋습니다 tooset이 toohello 최 댓 값 (200 현재).

이 설정에 대 한 자세한 내용은 hello를 검토 하십시오 [컴퓨터 학습 웹 서비스에 대 한 조정이 문서의](../machine-learning/machine-learning-scaling-webservice.md)합니다.

## <a name="example--sentiment-analysis"></a>예 – 정서 분석
hello 다음 예제에서는 포함 hello 감성 분석 기계 학습 함수를 사용 하는 스트림 분석 작업 hello에 설명 된 대로 [스트림 분석 기계 학습 통합 자습서](stream-analytics-machine-learning-integration-tutorial.md)합니다.

hello 쿼리는 hello 뒤 간단한 완벽 하 게 분할 된 쿼리 **감성** 아래와 같이 작동 합니다.

    WITH subquery AS (
        SELECT text, sentiment(text) as result from input
    )

    Select text, result.[Score]
    Into output
    From subquery

Hello를; 시나리오를 따르는 것이 좋습니다 초당 10, 000 트 윗의 처리량으로 스트림 분석 작업 tooperform 감성 분석 hello 트 윗 (이벤트)을 만들어야 합니다. 1 SU를 사용 하 여이 스트림 분석 작업 수 수 toohandle hello 트래픽? 1000 hello 작업의 hello 기본 일괄 처리 크기를 사용 하 여 있어야 수 tookeep를 hello 입력을 사용 합니다. 추가 hello 추가 기계 학습 함수 hello 일반 기본적으로 대기 시간 hello 감성 분석 기계 학습 웹 서비스 (1000의 기본 일괄 처리 크기) 인 대기 시간의 초 보다 더 이상 생성 해야 합니다. hello 스트림 분석 작업 **전반적인** 또는 종단 간 대기 시간이 몇 초 정도 대체로 됩니다. 이 스트림 분석 작업에 대해 보다 자세한 고려 *특히* hello 기계 학습 함수를 호출 합니다. 1000으로 hello 일괄 처리 크기를 having, 10, 000 이벤트의 처리량이 걸립니다 약 10 개 요청 tooweb 서비스. 1 SU 된 경우에는 동시 연결 tooaccommodate 충분 한 트래픽을이 입력 합니다.

하지만 경우에 어떻게 hello 입력된 이벤트 속도 100 배로 증가 하 고 hello 스트림 분석 작업에서 초당 tooprocess 1000000 트 윗을 요구 하는 이제? 두 가지 옵션이 있습니다.

1. Hello 일괄 처리 크기를 늘리고 또는
2. 병렬에서 파티션 hello 입력된 스트림 tooprocess hello 이벤트

Hello 첫 번째 옵션을 사용 하면 작업 hello **대기 시간** 증가 합니다.

Hello 두 번째 옵션을 사용 하면 더 많은 SUs toobe 프로 비전 해야 하 고 따라서 더 많은 동시 기계 학습 웹 서비스 요청을 생성 게 됩니다. 즉, hello 작업 **비용** 증가 합니다.

Hello 감성 분석 기계 학습 웹 서비스의 hello 대기 시간은 200ms 1000 이벤트 일괄 처리에 대 한 이하일 증가가 5,000 이벤트 일괄 처리의 경우 10, 000 이벤트 일괄 처리에 대 한 300ms 또는 500ms 25000 이벤트 일괄 처리에 대 한 가정 합니다.

1. Hello 첫 번째 옵션을 사용 하 여 (**하지** 자세한 SUs 프로 비전), hello 일괄 처리 크기를 너무 늘릴 수 없습니다**25000**합니다. 그러면 그러면 hello 작업 tooprocess 20 개의 동시 연결 toohello 기계 학습 웹 서비스와 함께 1000000 이벤트 (호출당 500 밀리초의 대기 시간)으로 있습니다. 따라서 기계 학습 웹 서비스 요청에서 증가 하므로 hello에 대 한 toohello 감성 함수 요청 인해 hello 스트림 분석 작업의 대기 시간이 추가 hello **200ms** 너무**500ms**합니다. 그러나 해당 일괄 처리 크기를 기록 **없습니다** 무한히 hello 기계 학습 웹 서비스에 필요한 만큼 요청 hello 페이로드 크기 증가 4mb 또는 더 작은 작업의 100 초 후 서비스 요청 제한 시간을 웹 합니다.
2. Hello 두 번째 옵션을 사용 하 여 hello 일괄 처리 크기에 그대로 유지 됩니다 1000, 200ms 웹 서비스에 대 한 대기 시간과 함께 이면 모든 20 개의 동시 연결 toohello 웹 서비스는 수 tooprocess 5 * 20 * 1000 이벤트 = 초당 100, 000입니다. 따라서 두 번째, hello 작업당 tooprocess 1000000 이벤트 60 SUs 필요 합니다. 비교 toohello 첫 번째 옵션을 스트림 분석 작업이 더 많은 서비스 일괄 처리 요청을 다시 웹 하 게 만드는 증가 비용을 생성 합니다.

다음 다른 SUs 및 일괄 처리 크기 (초당 이벤트 수)에 대 한 hello 스트림 분석 작업의 처리량 hello에 대 한 테이블은입니다.

| 배치 크기(ML 대기 시간) | 500(200ms) | 1,000(200ms) | 5,000(250ms) | 10,000(300ms) | 25,000(500ms) |
| --- | --- | --- | --- | --- | --- |
| **1SU** |2,500 |5,000 |20,000 |30,000 |50,000 |
| **3SU** |2,500 |5,000 |20,000 |30,000 |50,000 |
| **6SU** |2,500 |5,000 |20,000 |30,000 |50,000 |
| **12SU** |5,000 |10,000 |40,000 |60,000 |100,000 |
| **18SU** |7,500 |15,000 |60,000 |90,000 |150,000 |
| **24SU** |10,000 |20,000 |80,000 |120,000 |200,000 |
| **…** |… |… |… |… |… |
| **60SU** |25,000 |50,000 |200,000 |300,000 |500,000 |

이제 Stream Analytics 작업에서 Machine Learning 함수가 어떻게 작동하는지 충분히 이해하셨을 것입니다. 가능성이 또한 알려 각 "끌어오기" 데이터 원본에서 데이터를 "끌어온" 일괄 처리에 대 한 이벤트를 반환 하는 스트림 분석 작업 스트림 분석 작업 tooprocess hello 하 합니다. 이 끌어오기 모델 hello 기계 학습 웹 서비스 요청에 주는 영향가?

일반적으로 기계 학습 함수에 대 한 설정 hello 일괄 처리 크기 정확 하 게 hello "끌어오기" 각 스트림 분석 작업에 의해 반환 되는 이벤트 수로 나눌 수 없습니다. 이 경우 "부분" 일괄 처리와 hello 기계 학습 웹 서비스 호출 됩니다. 이 작업은 수행 toonot 추가 작업 대기 시간 끌어오기 toopull의 이벤트를 결합에 오버 헤드를 유발 합니다.

## <a name="new-function-related-monitoring-metrics"></a>새 함수 관련 모니터링 메트릭
스트림 분석 작업의 모니터 영역 hello, 세 개의 추가 기능 관련 메트릭을 추가 되었습니다. 서로 함수 요청, 함수 이벤트 및 실패 한 함수 요청 hello 그래픽 아래에 나와 있는 것 처럼입니다.

![Machine Learning 함수 메트릭을 사용한 Stream Analytics 크기 조정](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-01.png "Machine Learning 함수 메트릭을 사용한 Stream Analytics 크기 조정")

hello ´ ï ´ ù.

**함수 요청**: hello 함수 요청 수입니다.

**함수 이벤트**: hello의 hello 번호 이벤트 함수 요청 합니다.

**실패 한 함수 요청**: hello 실패 한 함수별 요청 수입니다.

## <a name="key-takeaways"></a>핵심 내용
toosummarize hello 주요 데이터 요소 순서 tooscale 기계 학습 함수를 사용 하는 스트림 분석 작업 hello 다음과 같은 항목이 고려해 야 합니다.

1. hello 입력된 이벤트 율
2. hello 트랜잭션당 스트림 분석 작업을 실행 하는 hello에 대 한 대기 시간 (및 따라서 hello 일괄 처리 크기 hello 기계 학습 웹 서비스의 요청)
3. 스트림 분석 SUs 및 기계 학습 웹 서비스 요청 (hello 추가 기능 관련 된 비용) hello 수 hello를 프로 비전

이 예에서는 완전하게 분할된 Stream Analytics 쿼리가 사용되었습니다. 더 복잡 한 쿼리 필요 하지 않으면 hello [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) hello 스트림 분석 팀의 추가 도움말에 대 한 중요 한 리소스입니다.

## <a name="next-steps"></a>다음 단계
스트림 분석에 대해 자세히 toolearn 참조:

* [Azure Stream Analytics 사용 시작](stream-analytics-real-time-fraud-detection.md)
* [Azure  Stream Analytics 작업 규모 지정](stream-analytics-scale-jobs.md)
* [Azure  Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)
