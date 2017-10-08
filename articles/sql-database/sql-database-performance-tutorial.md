---
title: "aaaTroubleshoot 성능 문제 및 데이터베이스 최적화 | Microsoft Docs"
description: "성능 권장 사항 tooyour SQL 데이터베이스 뿐만 아니라 하세요 방법에 대 한 통찰력 toogain hello 데이터베이스에 대해 실행 하는 hello 쿼리의 성능을 적용합니다"
metakeywords: azure sql database performance monitoring recommendation
services: sql-database
documentationcenter: 
manager: jhubbard
author: jan-eng
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,monitor & tune
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: janeng
ms.openlocfilehash: e948d30ac74eecf45420d5d77ef55e3c0b6f3f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a>성능 문제 해결 및 데이터베이스 최적화

인덱스 누락 및 최적화되지 않은 쿼리는 데이터베이스 성능을 저하시키는 일반적인 원인입니다. 이 자습서에서는 다음에 대해 알아봅니다.
> [!div class="checklist"]
> * 성능 향상 권장 사항 검토, 적용 및 되돌리기
> * 높은 리소스 사용률을 나타내는 쿼리 찾기
> * 장기 실행 쿼리 찾기

> 예를 들어 tooreceive 권장 인덱스가 없다는 – 성능 문제를 사용 하 여 데이터베이스에 연속 작업을 해야 합니다.
>

## <a name="log-in-toohello-azure-portal"></a>Azure 포털 toohello에 로그인

Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.

## <a name="review-and-apply-a-recommendation"></a>권장 사항 검토 및 적용

데이터베이스에 대 한 hello 시스템에서 이러한 단계 tooapply 권장 사항을 따릅니다.

1. Hello 클릭 **성능 권장 사항** hello 데이터베이스 블레이드에서 메뉴.

    ![성능 권장 사항](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. 권장 구성의 hello 목록에서 활성는 권장 사항을 선택 합니다. 이 예제에서 인덱스를 만듭니다.

    ![권장 사항 선택](./media/sql-database-performance-tutorial/create_index.png)

3. Hello를 클릭 하 여 hello 권장 구성 적용 **적용** 단추입니다. 필요에 따라 hello 권장 사항 세부 정보를 검토 하 고 hello T-SQL 스크립트를 클릭 하 여 실행할 너무 참조 **스크립트 보기** 단추입니다.

    ![권장 사항 적용](./media/sql-database-performance-tutorial/apply.png)

4. [선택 사항] 자동 튜닝 권장 사항 toobe 자동으로 적용에 대 한 사용 하도록 설정 합니다.

    ![자동 조정](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a>권장 사항 되돌리기

hello 데이터베이스 관리자를 구현 하는 모든 권장 사항을 모니터링 합니다. 권장 사항을 hello 작업 부하를 자동으로 되돌릴 수는 향상 되지 않습니다. 수동으로 권장 사항 되돌리기가 가능하지만 대부분의 경우 반드시 그런 것은 아닙니다. toorevert 권장:

1. Toohello 성능 권장 사항 메뉴를 이동 하 고 적용 하는 hello 권장 사항 중 하나를 선택 합니다.

    ![권장 사항 선택](./media/sql-database-performance-tutorial/select.png)

2. Hello 세부 정보 뷰에서 클릭 **Revert**합니다.

    ![권장 사항 되돌리기](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-hello-query-that-consumes-hello-most-resources"></a>대부분의 리소스 hello를 사용 하는 hello 쿼리 찾기

대부분의 리소스 hello를 사용해 이러한 단계 toofind hello 쿼리를 수행 합니다.

1. Hello 클릭 **Query Performance Insight** hello 데이터베이스 블레이드에서 메뉴.

    ![쿼리 인사이트](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. 리소스 종류를 선택합니다.

    ![쿼리 인사이트](./media/sql-database-performance-tutorial/select_resource_type.png)

3. Hello 표에 hello 첫 번째 쿼리를 선택 합니다.

    ![쿼리 인사이트](./media/sql-database-performance-tutorial/select_query.png)

4. Hello 쿼리 세부 정보를 검토 합니다.

    ![쿼리 인사이트](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-hello-longest-running-query"></a>Hello 가장 긴 실행 중인 쿼리 찾기

1. TooQuery Performance Insight를 이동 하 고 hello 선택 **장기 실행 쿼리** 탭 합니다.

    ![쿼리 인사이트](./media/sql-database-performance-tutorial/long_running.png)

3. Hello 표에 hello 첫 번째 쿼리를 선택 합니다.

    ![쿼리 인사이트](./media/sql-database-performance-tutorial/select_first_query.png)

4. Hello 쿼리 세부 정보를 검토 합니다.

    ![쿼리 인사이트](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a>다음 단계 
인덱스 누락 및 최적화되지 않은 쿼리는 데이터베이스 성능을 저하시키는 일반적인 원인입니다. 이 자습서에서는 다음에 대해 알아보았습니다.
> [!div class="checklist"]
> * 성능 향상 권장 사항 검토, 적용 및 되돌리기
> * 높은 리소스 사용률을 나타내는 쿼리 찾기
> * 장기 실행 쿼리 찾기

[SQL 데이터베이스 성능 튜닝 팁](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)
