---
title: "Azure 스트림 분석에 대 한 aaaTroubleshooting 가이드 | Microsoft Docs"
description: "어떻게 tootroubleshoot 스트림 분석 작업"
keywords: "문제 해결 가이드"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 4add48054e06a7d8eb617a08595c1be4555c59d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-azure-stream-analytics"></a>Azure Stream Analytics 문제 해결 가이드

Azure 스트림 분석 문제 해결 toobe 복잡 한 노력 얼핏 보기에 나타날 수 있습니다. 여러 사용자가 있는 작업을 한 후이 가이드 toohelp 약식 hello 프로세스 만든 우리 고 입력, 출력, 쿼리 및 함수에 대 한 hello 추측을 제거 합니다.

## <a name="troubleshoot-your-stream-analytics-job"></a>Stream Analytics 작업 문제 해결

스트림 분석 작업 문제 해결에 대 한 최상의 결과 지침을 따르는 hello를 사용 합니다.

1.  연결을 테스트합니다.
    - Hello를 사용 하 여 연결 tooinputs 및 출력을 확인 **연결 테스트** 각 입력 및 출력에 대 한 단추가 있습니다.

2.  입력된 데이터를 검사합니다.
    - 입력 데이터 tooverify 이벤트 허브로 전달 되는지, 사용 하 여 [서비스 버스 탐색기](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a) tooconnect tooAzure (이벤트 허브 입력이 사용 됨) 하는 경우 이벤트 허브입니다.  
    - 사용 하 여 hello [ **예제 데이터** ](stream-analytics-sample-data-input.md) 각 입력에 대 한 단추 및 hello 입력된 샘플 데이터를 다운로드 합니다.
    - Hello 데이터 hello 샘플 데이터 toounderstand hello 형식 검사: 스키마와 hello hello [데이터 형식](https://msdn.microsoft.com/library/azure/dn835065.aspx)합니다.

3.  쿼리를 테스트합니다.
    - Hello에 **쿼리** 탭에서 hello를 사용 하 여 **테스트** tootest hello 쿼리 단추를 선택한 너무 hello 다운로드 한 샘플 데이터를 사용 하 여[hello 쿼리 테스트](stream-analytics-test-query.md)합니다. 모든 오류를 검토 하 고 toocorrect 시도 해당 합니다.
    - 사용 하는 경우 [ **Timestamp By**](https://msdn.microsoft.com/library/azure/mt573293.aspx), hello 이벤트 hello 보다 큰 타임 스탬프가 있는지 확인 해야 [작업 시작 시간](stream-analytics-out-of-order-and-late-events.md)합니다.

4.  쿼리를 디버그합니다.
    - 단순 select 문 toomore 복잡 한 집계에서 점진적으로 hello 쿼리 단계를 사용 하 여 다시 작성 합니다. toobuild 단계별로 hello 쿼리 논리를 사용 하 여 [WITH](https://msdn.microsoft.com/library/azure/dn835049.aspx) 절.
    - 사용 하 여 [SELECT INTO](stream-analytics-select-into.md) toodebug 쿼리 단계입니다.

5.  다음과 같은 공통 문제를 제거합니다.
    - A [ **여기서** ](https://msdn.microsoft.com/library/azure/dn835048.aspx) hello 쿼리 절 어떠한 출력도 생성 되지 방지 하는 모든 이벤트를 필터링 합니다.
    - 창 함수를 사용할 때까지 기다린 hello 창의 전체 기간 toosee hello 쿼리에서 출력.
    - 이벤트에 대 한 타임 스탬프 hello hello 작업 시작 시간을 앞에 오고, 따라서 이벤트 손실 되는 합니다.

6.  이벤트 순서를 사용합니다.
    - 모든 이전 단계는 작동 hello, toohello 이동 **설정** 블레이드에 대 한 선택 [ **이벤트 순서가**](stream-analytics-out-of-order-and-late-events.md)합니다. 이 정책이 사용자 시나리오에 적합하게 구성되어 있는지 확인합니다. hello 정책이 *하지* hello를 사용할 때 적용 **테스트** 단추 tootest hello 쿼리 합니다. 이 결과 프로덕션 환경에서 hello 작업을 실행 하는 비교는 브라우저에서 테스트 간의 차이점 중 하나입니다.

7.  메트릭을 사용하여 디버그합니다.
    - Hello 예상 기간 (쿼리를 기반으로 hello) 후 없는 출력을 가져올 경우 hello 다음을 시도해 보십시오.
        - 살펴보고 [ **모니터링 메트릭에** ](stream-analytics-monitoring.md) hello에 **모니터** 탭 합니다. Hello 값이 집계 되기 때문에 hello 메트릭 몇 분 정도 지연 됩니다.
            - 하는 경우 입력 이벤트 > 0 hello 작업은 수 tooread 입력된 데이터입니다. 입력 이벤트가 0보다 크지 않으면 다음을 수행합니다.
                - toosee hello 데이터 원본에 유효한 데이터가 있는지 여부를 확인 하기를 사용 하 여 [서비스 버스 탐색기](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a)합니다. 이 검사는 hello 작업 입력으로 이벤트 허브를 사용 하는 경우 적용 됩니다.
                - Toosee를 예상 대로 hello 데이터 serialization 형식 및 데이터 인코딩 되는지 여부를 확인 합니다.
                - Hello 메시지의 본문 hello 인지 hello 작업 이벤트 허브를 사용 하는 경우 확인 toosee *Null*합니다.
            - 하는 경우 데이터 변환 오류 > 0 및 오르기 hello 다음 문제가 발생할 수 있습니다.
                - hello 작업 수 있습니다 수 toode-hello 이벤트를 직렬화 합니다.
                - hello 이벤트 스키마와 일치 하지 않는 hello 정의 된 또는 hello 쿼리에서 hello 이벤트 스키마 필요 합니다.
                - 일부 hello 이벤트의 hello 필드의 데이터 형식이 hello 기대와 다릅니다.
            - 경우 런타임 오류가 해당 hello 작업 hello 데이터를 받을 수는 있지만 hello 쿼리를 처리 하는 동안 오류를 생성 하는 의미 > 0입니다.
                - toofind hello 오류 이동 toohello [감사 로그](../azure-resource-manager/resource-group-audit.md) 찾아서 활성 *실패* 상태입니다.
            - 경우 InputEvents > 0과 OutputEvents = 0, hello 다음 중 하나가 충족 될 것을 의미 합니다.
                - 쿼리 처리로 제로 출력 이벤트가 발생했습니다.
                - 이벤트 또는 그 필드가 잘못되어 쿼리 처리 후 제로 출력이 발생할 수 있습니다.
                - hello 작업은 없습니다 toopush 데이터 toohello [출력 싱크](stream-analytics-select-into.md) 연결 또는 인증 이유로 합니다.
        - 모든 hello에 앞서 언급 한 작업 (발생 하는 작업 포함)에 추가 세부 정보를 설명 하는 로그 메시지의 오류 경우 hello 쿼리 논리 모든 이벤트를 필터링 하는 경우에서를 제외 하 고 있습니다. 여러 이벤트의 hello 처리에서 오류가 발생 하면 스트림 분석 로그 hello tooOperations 10 분 내에서 동일한 형식 hello의 처음 세 개의 오류 메시지를 기록 합니다. 그런 다음 “오류가 너무 빠르게 발생하고 억제되고 있습니다”라는 메시지로 동일한 추가 오류를 표시하지 않습니다.

8. 감사 및 진단 로그를 사용하여 디버그합니다.
    - 사용 하 여 [감사 로그](../azure-resource-manager/resource-group-audit.md), 필터 tooidentify 및 디버그 오류입니다.
    - 사용 하 여 [작업 진단 로그](stream-analytics-job-diagnostic-logs.md) 오류 tooidentify 및 디버그 합니다.

9. Hello 출력을 검토 합니다.
    - Hello 작업 상태는 때 *실행*hello 싱크 데이터 원본에 대 한 hello 출력을 볼 수 있습니다 hello 쿼리에서 명시한는 hello 기간에 따라 합니다.
    - 출력 tooa 특정 출력 형식이는 표시 되지 않는 경우 Azure Blob와 같은 덜 복잡 한 않은 tooan 출력 형식이 리디렉션하십시오. 저장소 탐색기를 사용 하 여 toosee hello 출력을 볼 수 있는지 여부를 확인 합니다. 또한 스로틀 한계 hello 출력에서 데이터를 수신 하지 못합니다 방지는 여부를 확인 합니다.

10. 작업 다이어그램 메트릭을 통해 데이터 흐름 분석을 사용합니다.
    - tooanalyze 데이터 흐름 및 문제를 사용 하 여 hello 식별 [메트릭 사용 하 여 작업 다이어그램](stream-analytics-job-diagram-with-metrics.md)합니다.

11. 지원 사례를 엽니다.
    - 마지막으로, 모든 작업이 실패 하면 작업을 포함 하는 SubscriptionID hello를 사용 하 여 Microsoft 지원 케이스를 엽니다.

## <a name="get-help"></a>도움말 보기

추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.

## <a name="next-steps"></a>다음 단계

* [스트림 분석 소개 tooAzure](stream-analytics-introduction.md)
* [Azure Stream Analytics 사용 시작](stream-analytics-real-time-fraud-detection.md)
* [Azure  Stream Analytics 작업 규모 지정](stream-analytics-scale-jobs.md)
* [Azure  Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)
