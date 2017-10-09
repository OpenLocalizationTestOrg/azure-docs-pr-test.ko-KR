---
title: "SELECT INTO를 사용 하 여 aaaDebug Azure 스트림 분석 쿼리 | Microsoft Docs"
description: "Stream Analytics에서 SELECT INTO 문을 사용한 샘플 데이터 중간 쿼리"
keywords: 
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 27e41af1a6ea06b4509d07a3a67087490d0ec1fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a>SELECT INTO 문을 사용하여 쿼리 디버그

실시간 데이터 처리에 hello 데이터를 알 같습니다. hello의 hello 중간 쿼리 유용할 수 있습니다. Azure Stream Analytics 작업의 입력 또는 단계를 여러 번 읽을 수 있기 때문에 추가 SELECT INTO 문을 작성할 수 있습니다. 이렇게 중간 데이터 저장소에 출력 되 고 마찬가지로 hello 데이터의 hello 정확성을 검사할 수 있습니다 *변수를 조사할* 않습니다를 디버그할 때 프로그램입니다.

## <a name="use-select-into-toocheck-hello-data-stream"></a>Toocheck hello 데이터 스트림을 SELECT INTO 사용

hello Azure Stream Analytics 작업에서 다음 예제 쿼리에서 하나의 스트림 입력, 두 개의 참조 데이터 입력 및 출력 tooAzure 테이블 저장소 합니다. hello 이벤트 허브 및 두 개의 참조는 blob tooget hello 이름 및 범주 정보 데이터를 조인 하는 hello 쿼리:

![SELECT INTO 쿼리 예제](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

Note hello 작업이 실행 되 고 있지만 hello 출력에서 생성 되는 이벤트가 없습니다. Hello에 **모니터링** hello 입력 데이터를 생성 하지만 hello의 단계를 알 수 없는 볼 수는 여기에 표시 된 타일 **조인** 삭제 이벤트 toobe hello 모두 발생 합니다.

![hello 모니터링 타일](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
이 경우 몇 가지 추가 SELECT INTO 문의 너무 "로그인" hello 중간 조인 결과 hello 입력에서 읽은 hello 데이터를 추가할 수 있습니다.

이 예제에서는 두 개의 새로운 “임시 출력”을 추가했습니다. 사용자가 원하는 어떠한 싱크도 될 수 있습니다. 여기서는 Azure Storage를 예로 사용합니다.

![추가 SELECT INTO 문 추가](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

그런 다음 다음과 같은 hello 쿼리를 다시 작성할 수 있습니다.

![SELECT INTO 쿼리 다시 작성](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

이제 hello 작업을 다시 시작 하 고 몇 분 동안 실행 되도록 합니다. 다음 표에서 Visual Studio 클라우드 탐색기 tooproduce hello로 temp1 및 temp2을 쿼리 한 다음:

**temp1 테이블**
![SELECT INTO temp1 테이블](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)

**temp2 테이블**
![SELECT INTO temp2 테이블](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)

볼 수 있듯이 temp1 및 temp2 데이터가 있고 고 hello 이름 열에서 temp2 올바르게 채워집니다. 그러나 여전히 출력에 데이터가 없기 때문에 문제가 있습니다.

![데이터가 없는 SELECT INTO output1 테이블](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

Hello 데이터를 샘플링 하 여 제어할 수 있습니다 거의 hello로 hello 문제 인지 조인의 두 번째입니다. Hello blob에서 hello 참조 데이터를 다운로드 하 고 볼 수 있습니다.

![SELECT INTO 참조 테이블](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

볼 수 있듯이 hello이 참조 데이터에 hello GUID 형식이 hello 형식의 [temp2의 열에서] hello와 다릅니다. 바로 이러한 이유로 예상 대로 hello 데이터 output1에 도착 하지 않았습니다.

Hello 데이터 형식을 수정 지정, tooreference blob을 업로드 및 다시 시도 하십시오.

![SELECT INTO 임시 테이블](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

이 시간 hello의에서 데이터가 hello 출력 형식이 지정 되어 예상 대로 채워집니다.

![SELECT INTO 최종 테이블](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a>도움말 보기

추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.

## <a name="next-steps"></a>다음 단계

* [스트림 분석 소개 tooAzure](stream-analytics-introduction.md)
* [Azure Stream Analytics 사용 시작](stream-analytics-real-time-fraud-detection.md)
* [Azure  Stream Analytics 작업 규모 지정](stream-analytics-scale-jobs.md)
* [Azure  Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)

