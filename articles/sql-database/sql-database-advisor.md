---
title: "Azure SQL 데이터베이스 aaaPerformance 권장 사항 | Microsoft Docs"
description: "hello Azure SQL 데이터베이스에는 현재 쿼리 성능을 향상 시킬 수 있는 SQL 데이터베이스에 대 한 권장 사항을 제공 합니다."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: 1db441ff-58f5-45da-8d38-b54dc2aa6145
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 77db338a0a395aec78c9e02849ae5ba4f2d01680
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-recommendations"></a>성능 권장 사항

Azure SQL 데이터베이스 및 응용 프로그램에 맞게 변경 알아내면는 SQL 데이터베이스의 toomaximize hello 성능을 사용 하면 사용자 지정 된 권장 사항을 제공 합니다. SQL Database 사용 기록을 분석하여 지속적으로 성능을 평가합니다. 제공 되는 hello 권장 사항 데이터베이스 고유 작업 부하 패턴에 따라 및 성능을 개선 합니다.

> [!NOTE]
> 권장 사항을 사용하는 권장된 방법은 데이터베이스에서 '자동 튜닝'을 사용하는 것입니다. 자세한 내용은 [자동 튜닝](sql-database-automatic-tuning.md)을 참조하세요.
>

## <a name="create-index-recommendations"></a>인덱스 만들기 권장 사항
Azure SQL 데이터베이스는 지속적으로 hello 쿼리가 실행 되 고 모니터링 하 고 hello 성능을 향상 시킬 수 있는 hello 인덱스를 식별 합니다. 특정 인덱스가 없다는 충분한 신뢰도가 빌드되면 새 **인덱스 만들기** 권장 사항이 생성됩니다. 성능 향상 hello 인덱스를 산정 하 여 azure SQL 데이터베이스 빌드 신뢰도 시간까지 상태로 전환 합니다. Hello 예상 성능 향상에 따라 높음, 보통, 낮음으로 권장 사항은 분류 됩니다. 

권장 사항을 사용하여 만든 인덱스는 항상 auto_created 인덱스로 플래그가 지정됩니다. sys.indexes 보기를 확인하여 어떤 인덱스가 auto_created인지를 확인할 수 있습니다. 자동으로 만든 인덱스는 ALTER/RENAME 명령을 차단하지 않습니다. 자동 인덱스 생성 된 toodrop hello 열을 시도 하면 hello 명령 전달 하 고 hello 자동으로 만든 인덱스 hello 명령도 함께 삭제 됩니다. 일반 인덱스는 인덱싱되는 열에 hello ALTER/이름 바꾸기 명령을 중단 됩니다.

Hello 만든 인덱스 권장 사항이 적용 되며, Azure SQL 데이터베이스는 hello 기준 성능 hello 쿼리의 성능을 비교 합니다. 새 인덱스 가져온 hello 성능 향상 된 기능, 권장 사항 성공한 것으로 플래그가 지정 됩니다 및 영향 보고서를 사용할 수 있습니다. Hello 인덱스 hello 혜택이 수반 하지 않은, 하는 경우이 자동으로 되돌립니다. 이러한 방식으로 Azure SQL 데이터베이스를 사용 하면 권장 사항을 사용 하 여 hello 데이터베이스 성능 향상만 됩니다.

모든 **Create index** 권장 사항은 hello 권장 구성을 적용 하 여 hello 데이터베이스나 풀 DTU 사용량 발견 된 경우 80% 이상 마지막 20 분 또는 hello 저장소 사용량의 90% 이상 인지를 허용 하지 않는 정책 백오프입니다. 이 경우 hello 권장 사항 연기 됩니다.

## <a name="drop-index-recommendations"></a>인덱스 삭제 권장 사항
또한 toodetecting Azure SQL 데이터베이스에 지속적으로 누락 된 인덱스를 기존 인덱스의 hello 성능을 분석합니다. 인덱스를 사용하지 않으면 Azure SQL Database에서는 삭제하도록 권장합니다. 다음과 같은 두 가지 경우에는 인덱스를 삭제하는 것이 좋습니다.
* 인덱스가 다른 인덱스의 복제본인 경우(동일하게 인덱스되거나 포함된 열, 파티션 스키마 및 필터)
* 연장된 기간(93) 동안 인덱스를 사용하지 않은 경우

삭제 인덱스 권장 구성이 구현 후 hello 확인도 수행합니다. Hello 성능이 향상 되 hello 영향 보고서 제공 됩니다. 성능 저하가 감지되는 경우 권장 사항이 되돌려집니다.


## <a name="parameterize-queries-recommendations"></a>쿼리 매개 변수화 권장 사항
**쿼리를 매개 변수화** 하나 해야 하거나 더 많은 쿼리는 계속 해 서 다시 컴파일 중 하지만 결국 hello 동일한 쿼리 실행 계획 권장 사항을 표시 합니다. 이 문제는 영업 기회 tooapply 강제 매개 변수화에 toobe 캐시 되 고 향후에 성능을 향상 시키고 리소스 사용이 감소 hello에서 다시 쿼리 계획을 사용 하면 열립니다. 

SQL Server에 대해 처음으로 실행 합니다. 모든 쿼리는 컴파일된 toobe toogenerate 실행 계획을 해야 합니다. 각 생성 된 계획은 toohello 계획 캐시 및 후속 실행 추가 된 hello의 동일한 쿼리를 다시 사용할 수 추가 컴파일 hello 필요성을 제거 하는 hello 캐시에서이 계획 합니다. 

매개 변수가 없는 값이 포함 되는 쿼리를 전송 하는 응용 프로그램에 있는 다른 매개 변수 값으로 이러한 모든 쿼리에 대해 hello 실행 계획이 컴파일되거나 다시 tooa 성능 오버 헤드가 발생할 수 있습니다. 대부분의 경우 hello에서 동일한 쿼리 값을 생성 하는 다른 매개 변수를 동일한 실행 계획을 hello 하지만 이러한 계획 toohello 계획 캐시를 여전히 별도로 추가 됩니다. 재컴파일을 실행 계획에는 데이터베이스 리소스를 사용 하 여, hello 쿼리 기간 시간과 오버플로 hello 계획 toobe hello 캐시에서 제거 계획 캐시를 일으키는 증가 합니다. Hello 데이터베이스의 parameterization 옵션이 forced hello를 설정 하 여 SQL Server의 이러한 동작을 변경할 수 있습니다. 

이 권장 구성의 hello 영향 예측 toohelp, 있습니다는 제공와 비교 하 여 hello 실제 CPU 사용량 및 hello 프로젝션 CPU 사용량 (처럼 hello 권장 구성이 적용 된 경우). 또한 tooCPU 절감 쿼리 기간 감소 컴파일에 소요 된 hello 시간에 대 한 합니다. 사용 해야 하는 오버 헤드가 훨씬 덜 계획 캐시, 허용 대부분의 hello toostay 캐시에서 계획 하 고 다시 사용할 수 있습니다. 적용할 수 있습니다이 권장 사항을 신속 하 고 쉽게 hello를 클릭 하 여 **적용** 명령입니다. 

이 권장 사항을 적용 한 후 데이터베이스에서 분 이내에 강제 매개 변수화를 활성화 및 hello 모니터링 약 24 시간 동안 지속 되는 프로세스를 시작 합니다. 이 기간이 지나면 전 24 시간 동안 데이터베이스의 CPU 사용량을 보여 주는 수 toosee hello 유효성 검사 보고서 수 및 hello 권장 구성이 적용 된 후 됩니다. SQL 데이터베이스 관리자에 성능 저하를 감지 하는 경우 적용 hello 권장 사항을 자동으로 전환 하는 보안 메커니즘이 있습니다.

## <a name="fix-schema-issues-recommendations"></a>스키마 문제 해결 권장 사항
**스키마 문제를 해결** 권장 사항을 나타난다 hello SQL 데이터베이스 서비스는 Azure SQL 데이터베이스에서 발생 하는 스키마와 관련 된 SQL 오류 hello 수의 특이 확인 합니다. 이 권장 사항은 데이터베이스에서 한 시간 내에 여러 스키마 관련 오류(잘못된 열 이름, 잘못된 개체 이름 등...)를 발견한 경우에 일반적으로 나타납니다.

"스키마 문제"는 hello SQL 쿼리의 hello 정의와 hello 데이터베이스 스키마의 hello 정의 정렬 되지 않은 경우 발생 하는 SQL Server의 구문 오류의 클래스입니다. 예를 들어 hello 쿼리에서 예상 hello 열 중 하나가 없을 수 있습니다 hello 대상 테이블 또는 그 반대의 경우도 마찬가지입니다. 

권장 사항 "스키마 문제 해결" Azure SQL 데이터베이스 서비스는 Azure SQL 데이터베이스에서 발생 하는 스키마와 관련 된 SQL 오류 hello 수의 특이 확인 하는 경우 표시 됩니다. 다음 관련된 tooschema 문제가 테이블 표시 hello 오류 hello:

| SQL 오류 코드 | Message |
| --- | --- |
| 201 |프로시저 또는 함수 '*'에서 매개 변수 '*'이(가) 필요하지만 제공되지 않았습니다. |
| 207 |잘못된 열 이름: '*'. |
| 208 |잘못된 개체 이름: '*'. |
| 213 |제공된 값의 개수나 열 이름이 테이블 정의와 일치하지 않습니다. |
| 2812 |저장 프로시저를 찾을 수 없습니다. '*'. |
| 8144 |프로시저 또는 함수 *에 너무 많은 인수가 지정되었습니다. |

## <a name="next-steps"></a>다음 단계
하면 권장 사항을 모니터링 하 고 tooapply 계속 해당 toorefine 성능입니다. 데이터베이스 워크로드는 동적 이며 지속적으로 변경합니다. SQL 데이터베이스 관리자는 toomonitor 계속 하 고 데이터베이스의 성능을 향상 시킬 수 있는 권장 사항을 제공 합니다. 

* 참조 [hello Azure 포털의에서 성능 권장 사항](sql-database-advisor-portal.md) toouse 성능 권장 사항에 Azure 포털을 hello 하는 방법에 대 한 단계입니다.
* 참조 [Query Performance Insight](sql-database-query-performance.md) 상위 쿼리의 성능에 영향을 hello에 대 한 toolearn 및 보기.

## <a name="additional-resources"></a>추가 리소스
* [쿼리 저장소](https://msdn.microsoft.com/library/dn817826.aspx)
* [CREATE INDEX](https://msdn.microsoft.com/library/ms188783.aspx)
* [역할 기반 액세스 제어](../active-directory/role-based-access-control-what-is.md)

