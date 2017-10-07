---
title: "스트림 분석에서 작업 스트리밍 aaaHow toostart | Microsoft Docs"
description: "Azure Stream Analytics에서 스트리밍 작업을 실행 하는 방법 | 학습 경로 세그먼트"
keywords: "스트리밍 작업"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9d46950f-2b69-49ce-a567-df558c5dd820
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 67aa14860c38cbd0535d0ec4f23729445d0185c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-streaming-job-in-azure-stream-analytics"></a>스트리밍 toorun Azure 스트림 분석에서 작업 하는 방법
작업 입력 될 때 쿼리 및 출력 모두 지정 된 hello 스트림 분석 작업을 시작할 수 있습니다.

toostart 작업:

1. Hello 작업 대시보드에서 hello Azure 클래식 포털에서 클릭 **시작** hello hello 페이지 맨 아래에 있습니다.
   
   ![작업 시작 단추](./media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   Hello Azure 포털에서에서 클릭 **시작** hello 작업 페이지 위쪽에 있습니다.
   
   ![Azure Portal 작업 시작 단추](./media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. 지정 된 **시작 출력** 값 toodetermine 때이 작업의 출력을 생성이 시작 됩니다. hello 이전에 시작 되지 않은 작업에 대 한 기본 설정값은 **작업 시작 시간**, 즉 hello 작업이 데이터를 처리 즉시 시작 됩니다. 지정할 수 있습니다는 **사용자 지정** hello에 시간이 과거 (소비에 대 한 기록 데이터) 또는 향후 hello (toodelay 이후의 시간이 될 때까지 처리). 작업에 이전에 시작 / 중지 하는 경우 사례 hello 옵션에 대 한 **마지막으로 중지 된 시간** hello 마지막 출력 시간에서에서 tooresume hello 작업 순서에서에서 사용할 수 있으며 데이터가 손실 되지 않도록 합니다.  
   
   ![스트리밍 작업 시작 시간](./media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Azure Portal 스트리밍 작업 시작 시간](./media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. 선택을 확인합니다. 작업 상태 hello도 변경 됩니다*시작* 너무 곧 들어왔다 및*실행* hello 작업이 시작 되 면입니다. Hello의 hello 진행률을 모니터링할 수 있습니다 **시작** hello에 대 한 작업 **알림 허브**:
   
   ![스트림 작업 진행률](./media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![Azure Portal 스트리밍 작업 진행률](./media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a>도움말 보기
추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>다음 단계
* [스트림 분석 소개 tooAzure](stream-analytics-introduction.md)
* [Azure Stream Analytics 사용 시작](stream-analytics-real-time-fraud-detection.md)
* [Azure  Stream Analytics 작업 규모 지정](stream-analytics-scale-jobs.md)
* [Azure  Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)

