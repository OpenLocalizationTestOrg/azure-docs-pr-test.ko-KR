---
title: "스트림 분석에서 aaaHow toowrite 쿼리 | Microsoft Docs"
description: "Stream Analytics 및 쿼리 데이터 | 학습 경로 세그먼트에서 쿼리를 작성합니다."
keywords: "toowrite 쿼리, 데이터를 쿼리하거나, 쿼리를 작성 하는 쿼리를 작성 하는 방법"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0e9cdadd-0ee0-4bee-b65b-4a06fb863c95
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: b943c34f10afd2b21789afbd341c471a5f168729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowrite-queries-in-stream-analytics"></a>스트림 분석의 toowrite 쿼리 하는 방법
Azure 스트림 분석에서 논리를 처리 하는 스트림에 대 한 쿼리를 작성 하는 쿼리로"고정" 작업을 시작 하 고 hello 작업에 도달할 때 데이터에서 실행 하기 전에 정의 구현 됩니다. hello 데이터 변환 SQL 방식 쿼리 언어는 단위로 같은 언어 확장을 추가 주로 하위 집합인 T-SQL의 일부와 [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) tooexpress 임시 의미 체계를 사용 합니다.

## <a name="writing-queries"></a>쿼리 작성:
1. 스트림 분석 hello Azure 관리 포털에서 작업을 클릭 **쿼리**합니다.
   
    ![쿼리 선택](./media/stream-analytics-write-queries/1-stream-analytics-write-queries.png)  
   
    Hello Azure 포털에서에서 클릭 **쿼리**합니다.
   
    ![쿼리 선택 미리 보기](./media/stream-analytics-write-queries/query-preview-portal.png)  
2. 새 작업을 시작 하는 쿼리 템플릿 toohelp을 서로 있습니다. 서식 파일 "통과"을 수행 하는 hello 쿼리 프로젝트는 입력된 이벤트의 모든 필드가 hello 출력으로 쿼리 합니다.  
   
   * 작업에 대 한 입력 및 출력을 하나 이상 정의한 경우 hello 자리 표시자 "[YourOutputAlias]" 및 "[YourInputAlias]" 필드의 입력 및 출력 처음 사용 하 여 원하는 hello hello 별칭으로 바꿀 수 있습니다. 또한 여전히 작성 고 hello 작업에서 입력 및 출력을 정의 하지 않고 hello Azure 클래식 포털에서에서 쿼리를 테스트할 수 있습니다.
   * 간단한 통과 보다 더 많은 처리가 tooperform을 원할 경우 hello 쿼리 정의 편집할 수 있습니다. 쿼리를 작성 작업을 시작 하는 tooget 패턴 캡처됩니다 몇 가지 일반적인 쿼리 살펴보세요 [여기](stream-analytics-stream-analytics-query-patterns.md)합니다.  
   
   ![쿼리 데이터 창](./media/stream-analytics-write-queries/2-stream-analytics-write-queries.png)  

## <a name="toovalidate-query-data-is-working"></a>데이터를 쿼리 하는 toovalidate 작동:
쿼리 하나 이상의 로컬 JSON 파일에서 테스트 데이터가 포함 된 hello 브라우저에서 실행 하 여 예상한 대로 작동 하는지 테스트할 수 있습니다. Hello 작업을 시작 되거나 청구를 나타내는 것 되지 됩니다.

> [!NOTE]
> 현재 브라우저에서 쿼리 테스트 hello Azure 포털에서에서 지원 되지 않습니다.  
> 
> 

1. (그렇지 않으면 hello 테스트 단추가 비활성화 됩니다) hello 쿼리에서 오류가 없는지 확인 다음 hello 테스트 단추를 클릭 합니다.  
   
   ![쿼리 데이터 테스트](./media/stream-analytics-write-queries/3-stream-analytics-write-queries.png)  
2. 각 hello 쿼리에서 참조 하는 hello 입력에 대 한 증명된 toospecify 파일 됩니다. 이 예제에서는 hello 템플릿 쿼리 그대로 유지 되므로-이므로, "yourinputalias" 이라는 입력에 사용 하는 hello 대화에서 메시지를 표시 합니다.  
   
   ![테스트 데이터 쿼리](./media/stream-analytics-write-queries/4-stream-analytics-write-queries.png)  
3. Tooa 테스트 파일을 검색 합니다. 몇 가지 샘플 파일에서 사용할 수 있는 [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) 및 hello hello 입력 탭에서 예제 데이터 함수를 통해 사용자 고유의 데이터 스트림 입력에서 샘플 데이터를 검색할 수도 있습니다.  
   
   ![쿼리 입력](./media/stream-analytics-write-queries/5-stream-analytics-write-queries.png)  
4. Hello 대화 상자를 닫은 후에 쿼리 hello 테스트 데이터에 대해 실행 되 고 hello 결과가 hello hello 쿼리 페이지 맨 아래에 표시 됩니다.  
   
   ![쿼리 요약](./media/stream-analytics-write-queries/6-stream-analytics-write-queries.png)  

## <a name="get-help"></a>도움말 보기
추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>다음 단계
* [스트림 분석 소개 tooAzure](stream-analytics-introduction.md)
* [Azure Stream Analytics 사용 시작](stream-analytics-real-time-fraud-detection.md)
* [Azure  Stream Analytics 작업 규모 지정](stream-analytics-scale-jobs.md)
* [Azure  Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)

