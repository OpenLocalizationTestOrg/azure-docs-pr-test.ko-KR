---
title: "스트림 분석 작업 모니터링 aaaUnderstanding | Microsoft Docs"
description: "Stream Analytics 작업 모니터링 이해"
keywords: "쿼리 모니터"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5f5cc00f-4a7b-491e-89e1-dbafea46d399
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 36819025c7b2ddbf4b9694522f1b4820407ca5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-stream-analytics-job-monitoring-and-how-toomonitor-queries"></a>스트림 분석 작업 모니터링 이해 및 방법을 toomonitor 쿼리

## <a name="introduction-hello-monitor-page"></a>소개: hello 모니터 페이지
Azure 포털 둘 다 화면 쿼리 및 작업 성능 문제를 해결 하 고 사용 하는 toomonitor 수 있는 주요 성능 메트릭을 번호입니다. toosee 이러한 메트릭을 찾아보기 toohello 스트림 분석 작업에 대 한 메트릭을 보기 hello에 관심이 있는 **모니터링** hello 개요 페이지에서 섹션.  

![모니터링 링크](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

hello 창에 표시 된 것 처럼 나타납니다.

![작업 모니터링 대시보드](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a>Stream Analytics에 사용 가능한 메트릭
| 메트릭                 | 정의                               |
| ---------------------- | ---------------------------------------- |
| SU % 사용률       | hello의 hello 사용률이 스트리밍 단위 tooa 작업 hello 작업의 hello 크기 조정 탭에서 할당합니다. 이 표시가 80% 이상에 도달하면 이벤트 처리가 지연되거나 진행을 중단할 가능성이 큽니다. |
| 입력 이벤트           | 이벤트 수의 hello 스트림 분석 작업에서 받은 데이터의 양입니다. 이 이벤트는 toohello 입력된 소스 전송 되 고 사용 하는 toovalidate 수 있습니다. |
| 출력 이벤트          | Hello 스트림 분석 작업 toohello 출력 대상에서 이벤트의 수에 전송 되는 데이터의 양입니다. |
| 순서 비지정 이벤트    | 삭제 했거나 hello 이벤트 순서 정책에 따라는 조정 된 타임 스탬프를 지정 하는 순서가 틀리게 수신 하는 이벤트 수입니다. Hello Out of 순서 허용 시간 설정의 hello 구성에 의해 영향을 줄 수 있습니다. |
| 데이터 변환 오류 | Stream Analytics 작업에 의해 발생하는 데이터 변환 오류 수입니다. |
| 런타임 오류         | hello 스트림 분석 작업을 실행 하는 동안 발생 하는 오류의 총 수입니다. |
| 늦은 입력 이벤트      | Hello 늦게 도착 허용 시간 설정의 hello 이벤트 순서 정책 구성에 따라 하거나 삭제 된 hello 소스 또는 타임 스탬프에서 늦게 도착 하는 이벤트 수가 조정 되었습니다 했습니다. |
| 기능 요청      | 호출 toohello Azure 기계 학습 함수 (있는 경우)의 수입니다. |
| 실패한 기능 요청 | 실패한 Azure Machine Learning 함수 호출(있는 경우) 수입니다. |
| 함수 이벤트        | (있는 경우) toohello Azure 기계 학습 함수를 전송 하는 이벤트의 수입니다. |
| 입력 이벤트 바이트      | 바이트의 hello 스트림 분석 작업에서 받은 데이터의 양입니다. 이 이벤트는 toohello 입력된 소스 전송 되 고 사용 하는 toovalidate 수 있습니다. |


## <a name="customizing-monitoring-in-hello-azure-portal"></a>Hello Azure 포털에서에서 모니터링을 사용자 지정
Hello 종류의 차트를 표시 하는 메트릭 조정할 수 있으며 시간 hello 차트 편집 설정에서 범위 수 있습니다. 자세한 내용은 참조 [어떻게 tooCustomize 모니터링](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md)합니다.

  ![쿼리 모니터 시간 그래프](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a>도움말 보기
추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>다음 단계
* [스트림 분석 소개 tooAzure](stream-analytics-introduction.md)
* [Azure Stream Analytics 사용 시작](stream-analytics-real-time-fraud-detection.md)
* [Azure  Stream Analytics 작업 규모 지정](stream-analytics-scale-jobs.md)
* [Azure  Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)

