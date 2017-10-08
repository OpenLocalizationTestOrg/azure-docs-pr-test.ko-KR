---
title: "aaaMigrate 사용자 솔루션 tooSQL 데이터 웨어하우스 | Microsoft Docs"
description: "마이그레이션 지침 tooAzure SQL 데이터 웨어하우스 솔루션 플랫폼으로 전환 합니다."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 198365eb-7451-4222-b99c-d1d9ef687f1b
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/27/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 27b51f15247603f054070f360ede7f24541c0288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-solution-tooazure-sql-data-warehouse"></a>사용자 솔루션 tooAzure SQL 데이터 웨어하우스 마이그레이션
기존 데이터베이스 솔루션 tooAzure SQL 데이터 웨어하우스 마이그레이션 관련 정보를 참조 하십시오. 

## <a name="profile-your-workload"></a>워크로드 프로파일링
를 마이그레이션하기 전에 toobe SQL 데이터 웨어하우스 작업에 대 한 hello 적합 한 솔루션에는 특정 할 수 있습니다. SQL 데이터 웨어하우스는 대규모 데이터에 대해 설계 된 분산된 시스템 tooperform 분석 합니다.  데이터 웨어하우스 마이그레이션 tooSQL 어려운 toounderstand 이지만 일부 시간 tooimplement 걸리는 일부 디자인 변경 해야 합니다. 비즈니스에 필요한 엔터프라이즈 수준의 데이터 웨어하우스, hello 이점 hello 노력 사항이 있습니다. 그러나 SQL 데이터 웨어하우스의 hello 전원 필요 없는 경우 더 많은 비용 효율적인 toouse SQL Server 또는 Azure SQL 데이터베이스입니다.

다음과 같은 경우 SQL Data Warehouse를 사용하는 것이 좋습니다.
- 하나 이상의 테라바이트의 데이터가 있는 경우
- 많은 양의 데이터에 계획 toorun 분석
- Hello 기능 tooscale 계산 및 저장소 필요 
- 필요 하지 않을 때 일시 중지 하 여 toosave 비용 계산 리소스를 선택 합니다.

다음과 같은 작업(OLTP) 워크로드에 SQL Data Warehouse를 사용하지 않습니다.
- 높은 빈도의 읽기 및 쓰기
- 많은 수의 단일 항목 선택
- 많은 양의 단일 행 삽입
- 행 단위 처리 요구 사항
- 호환되지 않는 형식(JSON, XML)


## <a name="plan-hello-migration"></a>Hello 마이그레이션 계획

기존 솔루션 tooSQL 데이터 웨어하우스 toomigrate 계획인 중요 tooplan hello 마이그레이션을 시작 하기 전에 있습니다. 

계획의 단일 목표 tooensure 테이블 스키마를 데이터도 없으며 SQL 데이터 웨어하우스와 호환 되는 코드입니다. 현재 시스템 및 SQL 데이터 웨어하우스 간의 주위 호환성 차이점 toowork 몇 가지 있습니다. 또한 많은 양의 데이터 tooAzure 사용 시간 마이그레이션. 데이터 tooAzure 가져오는 신속히 신중 하 게 계획 합니다. 

계획의 또 다른 목표는 솔루션에서는 SQL 데이터 웨어하우스는 hello 높은 쿼리 성능 활용 조정 tooensure 설계 tooprovide toomake 디자인입니다. 따라서 기존의 접근 방식에서는 없는 가장 hello 경우도 다양 한 디자인 패턴 소개 눈금에 대 한 데이터 웨어하우스를 디자인 합니다. 마이그레이션 후 일부 디자인 조정을 진행할 수 있지만 변경 더 빨리 hello 프로세스에서 나중에 시간을 저장 합니다.

성공적인 마이그레이션 tooperform 해야 toomigrate 테이블 스키마, 코드 및 데이터입니다. 이러한 마이그레이션 항목에 대한 지침은 다음을 참조하세요.

-  [스키마 마이그레이션](sql-data-warehouse-migrate-schema.md)
-  [코드 마이그레이션](sql-data-warehouse-migrate-code.md)
-  [데이터 마이그레이션](sql-data-warehouse-migrate-data.md) 

<!--
## Perform hello migration


## Deploy hello solution


## Validate hello migration

-->

## <a name="next-steps"></a>다음 단계
hello CAT (고객 자문 팀)를 통해 블로그 게시 몇 가지 훌륭한 SQL 데이터 웨어하우스 지침을 있습니다.  해당 문서에 대해 살펴봅니다 [실제로 마이그레이션 데이터 tooAzure SQL 데이터 웨어하우스] [ Migrating data tooAzure SQL Data Warehouse in practice] 마이그레이션에 대 한 추가 지침에 대 한 합니다.

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data tooAzure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
