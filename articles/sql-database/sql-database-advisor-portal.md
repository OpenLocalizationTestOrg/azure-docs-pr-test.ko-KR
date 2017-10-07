---
title: "aaaApply 성능 권장 사항-Azure SQL 데이터베이스 | Microsoft Docs"
description: "Toocorrect 또는 Azure SQL 데이터베이스의 성능을 최적화할 수 있는 hello Azure 포털 toofind 성능 권장 사항에서는 작업에서 식별 하는 몇 가지 문제입니다."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: cda8a646-0584-4368-b28a-85cdd9b54fcd
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 0b2234840fc3254d235db9e7d18f5bc912851c6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="find-and-apply-performance-recommendations"></a>성능 권장 사항 찾기 및 적용

Toocorrect 또는 Azure SQL 데이터베이스의 성능을 최적화할 수 있는 hello Azure 포털 toofind 성능 권장 사항에서는 작업에서 식별 하는 몇 가지 문제입니다. **성능 권장 사항** Azure 포털에서 페이지에서는 잠재적인 영향에 따라 toofind hello 최상위 권장 수 있습니다. 

## <a name="viewing-recommendations"></a>권장 사항 보기

tooview 올바른 hello 필요 하면 성능 권장 사항 적용 [역할 기반 액세스 제어](../active-directory/role-based-access-control-what-is.md) Azure에서 사용 권한. **판독기**, **SQL DB 참가자** 권한은 필요한 tooview 권장 사항 및 **소유자**, **SQL DB 참가자** 권한은 필요 tooexecute 행위; 만들기 또는 인덱스를 삭제 하 고 인덱스 생성을 취소 합니다.

Hello에 나오는 단계 toofind 성능 권장 사항에 따라 Azure 포털을 사용 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. 너무 이동**더 많은 서비스** > **SQL 데이터베이스**, 해당 데이터베이스를 선택 하 고 있습니다.
3. 너무 이동**성능 권장 사항** tooview hello 선택한 데이터베이스에 사용할 수 있는 권장 합니다.

성능 권장 사항이 hello 다음 그림에 표시 된 하나 hello 테이블 비슷한 toohello shonw:

![권장 사항](./media/sql-database-advisor-portal/recommendations.png)

권장 사항 hello 다음 범주에는 성능에 대 한 잠재적인 영향에 따라 정렬 됩니다.

| 영향 | 설명 |
|:--- |:--- |
| 높음 |높은 영향 권장 사항을 hello 가장 중요 한 성능에 영향을 제공 해야 합니다. |
| 중간 |중간 영향 권장 사항은 성능을 향상시키지만, 크게 향상시키지는 않습니다. |
| 낮음 |낮은 영향 권장 사항은 없는 것보다 나은 성능을 제공하지만, 향상된 기능이 눈에 띄지는 않습니다. |


> [!NOTE]
> Azure SQL 데이터베이스 필요 toomonitor 활동 이상 순서 tooidentify 하루에 몇 가지 권장 합니다. hello Azure SQL 데이터베이스 작업의 임의 연결 상태가 좋지 않은 버스트 수 있습니다에 보다 쉽게 일관 된 쿼리 패턴을 최적화할 수 있습니다. 권장 사항을 corrently 사용할 수 없는 경우 hello **성능 권장 사항** 페이지 이유를 설명 하는 메시지를 제공 합니다.
> 

Hello 기록 작업의 hello 상태를 볼 수 있습니다. 자세한 내용은 권장 사항 또는 상태 toosee를 선택 합니다.

Hello Azure 포털에서에서 "Create index" 권장 구성의 예를 들면 다음과 같습니다.

![인덱스 만들기](./media/sql-database-advisor-portal/sql-database-performance-recommendation.png)

## <a name="applying-recommendations"></a>권장 사항 적용
Azure SQL 데이터베이스는 권장 하는 방법에 대 한 모든 권한을 제공 hello 다음 세 가지 옵션 중 하나를 사용 하 여 활성화 합니다. 

* 개별 권장 구성을 한 번에 하나씩 적용합니다.
* Enable hello 자동 튜닝 tooautomatically 권장 사항을 적용 합니다.
* tooimplement 권장 사항을 수동으로 hello 권장 데이터베이스에 대해 T-SQL 스크립트를 실행 합니다.

모든 권장 사항 tooview 세부 정보를 선택한 다음 클릭 **스크립트를 보려면** tooreview hello hello 권장 구성을 만드는 방법에 대 한 자세한 내용은 합니다.

hello 권장 구성이 적용 되는 등의 데이터베이스를 오프 라인 성능 권장 또는 자동 튜닝 하지를 사용 하는 동안 hello 데이터베이스가 온라인 상태로 유지 합니다.

### <a name="apply-an-individual-recommendation"></a>개별 권장 구성 적용
권장 구성을 한 번에 하나씩 검토하고 수락할 수 있습니다.

1. Hello에 **권장 사항을** 블레이드의 권장 구성 선택 합니다.
2. Hello에 **세부 정보** 블레이드 클릭 **적용** 단추입니다.
   
    ![권장 구성 적용](./media/sql-database-advisor-portal/apply.png)

선택한 권장 hello 데이터베이스에 적용 됩니다.

### <a name="removing-recommendations-from-hello-list"></a>Hello 목록에서 제거 하는 권장 사항
권장 사항 목록에 항목이 tooremove hello 목록에서 원하는 경우 hello 권장 사항을 무시 될 수 있습니다.

1. hello 목록에서 권장 구성을 선택 **권장 사항을** tooopen hello 세부 정보입니다.
2. 클릭 **취소** hello에 **세부 정보** 블레이드입니다.

원하는 경우 삭제 된 항목을 toohello 다시 추가할 수 있습니다 **권장 사항을** 목록:

1. Hello에 **권장 사항을** 블레이드 클릭 **보기 삭제**합니다.
2. 세부 정보 목록 tooview hello에서에서 삭제 한 항목을 선택 합니다.
3. 필요에 따라 **삭제 취소** tooadd hello 인덱스 백 toohello 기본 목록 **권장 사항을**합니다.


### <a name="enable-automatic-tuning"></a>자동 조정 사용
Hello Azure SQL 데이터베이스 tooimplement 권장 사항을 자동으로 설정할 수 있습니다. 권장 구성은 사용할 수 있을 때 자동으로 적용됩니다. 으로 hello에서 관리 하는 모든 권장 사항이 포함 된 경우 성능에 미치는 영향 hello 음수 hello 권장 사항은 서비스가 되돌립니다.

1. Hello에 **권장 사항을** 블레이드에서 클릭 **자동화**:
   
    ![관리자 설정](./media/sql-database-advisor-portal/settings.png)
2. 작업 선택 tooautomate:
   
    ![권장된 인덱스](./media/sql-database-advisor-portal/automation.png)

### <a name="manually-run-hello-recommended-t-sql-script"></a>T-SQL 스크립트를 권장 하는 hello를 수동으로 실행
권장 사항을 선택한 다음 **스크립트 보기**를 클릭합니다. 데이터베이스에 대해이 스크립트를 실행 toomanually hello 권장 구성을 적용 합니다.

*수동으로 실행 하는 인덱스는 하지 모니터링 하 고 hello 서비스 성능에 미치는 영향에 대 한 유효성을 검사* 하므로 생성 tooverify 후 이러한 인덱스를 모니터링 하는 것이 좋습니다 제공 성능 향상 및 조정 하거나 경우 삭제 필요 합니다. 인덱스 만들기에 대한 세부 정보는 [CREATE INDEX (TRANSACT-SQL)](https://msdn.microsoft.com/library/ms188783.aspx)를 참조하세요.

### <a name="canceling-recommendations"></a>권장 사항 취소
**보류 중**, **확인 중** 또는 **성공** 상태에 있는 권장 사항은 취소할 수 있습니다. **실행 중** 상태의 권장 사항은 취소할 수 없습니다.

1. Hello에 권장 사항을 선택 **튜닝 기록** 영역 tooopen hello **권장 사항 세부 정보** 블레이드입니다.
2. 클릭 **취소** tooabort hello 과정 hello 권장 구성을 적용 합니다.

## <a name="monitoring-operations"></a>모니터링 작업
권장 구성을 적용해도 즉각적으로 일어나지 않을 수 있습니다. hello 포털 권장 구성의 hello 상태에 관한 세부 정보를 제공합니다. hello 다음은 인덱스에 저장할 수 있는 가능한 상태입니다.

| 가동 상태 | 설명 |
|:--- |:--- |
| Pending |권장 사항 적용 명령을 수신했고 실행이 예약됩니다. |
| 실행 중 |hello 권장 구성이 적용 되 고 있습니다. |
| 확인 중 |권장 사항이 성공적으로 적용 하 고 hello 서비스는 hello 혜택을 측정 합니다. |
| 성공 |권장 사항이 성공적으로 적용되면 성능을 측정합니다. |
| 오류 |Hello 과정 hello 권장 구성을 적용 하는 동안 오류가 발생 했습니다. 이 일시적인 문제 또는 스키마 변경 toohello 테이블 수 및 hello 스크립트는 더 이상 유효 합니다. |
| 되돌리기 |hello 권장 구성이 적용 된 비 고성능 판단 되는 있고 자동으로 되돌리고 합니다. |
| 되돌림 |hello 권장 되돌려. |

자세한 내용은 in-process에 권장 사항을 hello 목록 toosee에서를 클릭 합니다.

![권장된 인덱스](./media/sql-database-advisor-portal/operations.png)

### <a name="reverting-a-recommendation"></a>권장 사항 되돌리기
Hello 성능 권장 사항 tooapply hello 권장 사항을 사용 하는 경우 (수동으로 hello T-SQL 스크립트를 실행 하지 않은 것을 의미) 자동으로 되돌려집니다 것 찾으면 hello 성능 영향 toobe 음수입니다. 어떤 이유로 든 원할 toorevert 권장 할 수 있습니다 hello 다음:

1. Hello에 성공적으로 적용 된 권장 사항을 선택 **기록 튜닝** 영역입니다.
2. 클릭 **Revert** hello에 **권장 사항 세부 정보** 블레이드입니다.

![권장된 인덱스](./media/sql-database-advisor-portal/details.png)

## <a name="monitoring-performance-impact-of-index-recommendations"></a>인덱스 권장 구성의 성능 영향 모니터링
권장 사항을 성공적으로 구현 된 후 (현재 작업 인덱스 및 쿼리 권장 구성의 경우에 매개 변수화) 클릭할 수 있는 **쿼리 Insights** hello 권장 사항 세부 정보 블레이드에서 tooopen에 [쿼리 Performance Insight](sql-database-query-performance.md) hello 상위 쿼리의 성능에 영향을 확인 합니다.

![성능에 미치는 영향을 모니터링합니다.](./media/sql-database-advisor-portal/query-insights.png)

## <a name="summary"></a>요약
Azure SQL Database는 SQL Database 성능을 향상하기 위한 권장 사항을 제공합니다. T-SQL 스크립트를 개별적인 완전 자동으로 제공하여 데이터베이스를 최적화하고 궁극적으로 쿼리 성능을 향상시키도록 지원합니다.

## <a name="next-steps"></a>다음 단계
하면 권장 사항을 모니터링 하 고 tooapply 계속 해당 toorefine 성능입니다. 데이터베이스 워크로드는 동적 이며 지속적으로 변경합니다. Azure SQL 데이터베이스는 toomonitor 계속 되 고 데이터베이스의 성능을 향상 시킬 수 있는 권장 사항을 제공 합니다. 

* 참조 [자동 튜닝](sql-database-automatic-tuning.md) toolearn에 더 알아봅니다 hello Azure SQL 데이터베이스에서 자동으로 조정 합니다.
* Azure SQL Database 성능 권장 사항에 대한 개요는 [성능 권장 사항](sql-database-advisor.md)을 참조하세요.
* 참조 [Query Performance Insight](sql-database-query-performance.md) toolearn hello 상위 쿼리의 성능에 영향을 확인 하는 방법에 대 한 합니다.

## <a name="additional-resources"></a>추가 리소스
* [쿼리 저장소](https://msdn.microsoft.com/library/dn817826.aspx)
* [CREATE INDEX](https://msdn.microsoft.com/library/ms188783.aspx)
* [역할 기반 액세스 제어](../active-directory/role-based-access-control-what-is.md)

