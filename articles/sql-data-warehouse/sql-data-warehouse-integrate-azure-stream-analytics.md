---
title: "SQL 데이터 웨어하우스에 Azure 스트림 분석 aaaUse | Microsoft Docs"
description: "솔루션 개발을 위한 Azure SQL 데이터 웨어하우스와 함께 Azure 스트림 분석 사용을 위한 팁"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 8aeb2247-20c5-4a29-b327-30a8ce09dfdc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 1278197a6764864124fd92fc672de00b83ec343f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a>SQL 데이터 웨어하우스와 함께 Azure 스트림 분석 사용
Azure Stream Analytics는 스트리밍 데이터 hello 클라우드에 대해 낮은 대기 시간, 고가용성, 확장 가능한 복합 이벤트 처리를 제공 하는 완전히 관리 되는 서비스. 참조 하 여 hello 기본 사항을 배울 [스트림 분석 소개 tooAzure][Introduction tooAzure Stream Analytics]합니다. 학습할 수 있는 다음 방법을 수행 하 여 스트림 분석에는 종단 간 솔루션 toocreate hello [Azure 스트림 분석을 사용 하 여 시작] [ Get started using Azure Stream Analytics] 자습서입니다.

이 문서에서는 toouse 하 여 Azure SQL 데이터 웨어하우스 데이터베이스 방법 스트림을 분석 작업에 대 한 출력 싱크로 배웁니다.

## <a name="prerequisites"></a>필수 조건
먼저 hello 단계를 수행 하는 hello 예행 [Azure 스트림 분석을 사용 하 여 시작] [ Get started using Azure Stream Analytics] 자습서입니다.  

1. 이벤트 허브 입력 만들기
2. 이벤트 생성기 응용 프로그램 구성 및 시작
3. 스트림 분석 작업 프로비전
4. 작업 입력 및 쿼리 지정

그런 다음 SQL 데이터 웨어하우스 데이터베이스를 만듭니다.

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a>작업 출력 지정: Azure SQL 데이터 웨어하우스 데이터베이스
### <a name="step-1"></a>1단계
Stream Analytics 작업에서 클릭 **출력** hello 페이지 한 후 hello 위에서 **출력 추가**합니다.

### <a name="step-2"></a>2단계
SQL 데이터베이스를 선택하고 다음을 클릭합니다.

![][add-output]

### <a name="step-3"></a>3단계
Hello hello 다음 페이지에서 다음 값을 입력 합니다.

* *출력 별칭*: 이 작업 출력의 이름을 입력합니다.
* *구독*:
  * SQL 데이터 웨어하우스 데이터베이스 hello에 있으면 hello 스트림 분석 작업으로 동일한 구독 현재 구독에서 사용 하 여 SQL 데이터베이스를 선택 합니다.
  * 데이터베이스가 다른 구독에 있는 경우 다른 구독에서 SQL 데이터베이스 사용을 선택합니다.
* *데이터베이스*: 대상 데이터베이스의 hello 이름을 지정 합니다.
* *서버 이름*: 방금 지정한 hello 데이터베이스에 대 한 hello 서버 이름을 지정 합니다. Azure 클래식 포털 toofind hello에이 사용할 수 있습니다.

![][server-name]

* *사용자 이름*: hello 데이터베이스에 대 한 쓰기 권한이 있는 계정의 hello 사용자 이름을 지정 합니다.
* *암호*: 제공 hello에 대 한 hello 암호가 사용자 계정을 지정 합니다.
* *테이블*: hello 데이터베이스에 hello 대상 테이블의 hello 이름을 지정 합니다.

![][add-database]

### <a name="step-4"></a>4단계
이 작업 출력 및 스트림 분석 toohello 데이터베이스에 연결할 수 있는지 tooverify hello 확인 단추 tooadd를 클릭 합니다.

![][test-connection]

Hello, toohello 데이터베이스 연결에 성공 하면 hello hello 포털 맨 아래에 알림이 표시 됩니다. Hello 아래쪽 tootest hello 연결 toohello 데이터베이스에서 연결 테스트를 클릭 수 있습니다.

## <a name="next-steps"></a>다음 단계
통합 개요는 [SQL Data Warehouse 통합 개요][SQL Data Warehouse integration overview]를 참조하세요.

더 많은 개발 팁은 [SQL Data Warehouse 개발 개요][SQL Data Warehouse development overview]를 참조하세요.

<!--Image references-->

[add-output]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction tooAzure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-real-time-fraud-detection.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/
