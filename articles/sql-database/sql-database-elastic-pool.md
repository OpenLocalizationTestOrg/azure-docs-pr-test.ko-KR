---
title: "aaaWhat 탄력적 풀에는? 여러 SQL Database 관리 - Azure | Microsoft Docs"
description: "탄력적 풀을 사용하여 수백 및 수천 개의 SQL Database를 관리하고 크기를 조정합니다. 필요한 경우 배포할 수는 리소스에 대한 단일 가격"
keywords: "여러 데이터베이스, 데이터베이스 리소스, 데이터베이스 성능"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: b46e7fdc-2238-4b3b-a944-8ab36c5bdb8e
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 07/31/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 2098d7817ebe1277b5c131421f23c00803ec78f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-pools-help-you-manage-and-scale-multiple-sql-databases"></a>탄력적 풀이 여러 SQL Database를 관리하고 크기를 조정하는 데 도움을 주는 방식

SQL Database 탄력적 풀은 사용 요구가 다양하고 예측하기 어려운 여러 데이터베이스를 관리하고 크기를 조정하기 위한 간단하고 비용 효과적인 솔루션입니다. 탄력적 풀의 hello 데이터베이스 단일 Azure SQL 데이터베이스 서버에 있고 집합 다양 한 리소스를 공유 ([탄력적 데이터베이스 트랜잭션 단위](sql-database-what-is-a-dtu.md) (Edtu))에서 집합 가격입니다. Azure SQL 데이터베이스의 탄력적 풀 SaaS 개발자 toooptimize hello 가격 성능을 지원 정해진 예산 데이터베이스 그룹에 대 한 각 데이터베이스에 대 한 성능 탄력성을 제공 하는 동시 합니다.   

> [!NOTE]
> 탄력적 풀은 현재 미리 보기 상태인 인도 서부를 제외한 모든 Azure 지역에서 일반 공급(GA) 상태입니다.  이 영역에서 탄력적 풀의 GA는 가능한 한 빨리 수행될 예정입니다.
>

## <a name="what-are-sql-elastic-pools"></a>SQL 탄력적 풀이란? 

SaaS 개발자는 여러 데이터베이스로 구성된 대규모 데이터 계층에 응용 프로그램을 작성합니다. 일반적인 응용 프로그램 패턴은 각 고객에 대 한 단일 데이터베이스 tooprovision 합니다. 하지만 서로 다른 고객 사용 패턴을 다양 한 및 예측할 수 없는 포함 되며 각 개별 데이터베이스 사용자의 어려운 toopredict hello 리소스 요구 사항을 있습니다. 일반적으로 두 가지 옵션이 있습니다. 

- 최대 사용량에 따른 리소스 오버프로비저닝과 과다 지불 또는
- 아래 프로 비전 toosave 비용, 성능 고객 만족 하는 동안 최대치의 hello 부담 합니다. 

탄력적 풀 데이터베이스 필요할 때 필요한 hello 성능 리소스를 확인 하 여이 문제를 해결 합니다. 예측 가능한 예산 내에서 간단한 리소스 할당 메커니즘을 제공합니다. 탄력적 풀을 사용 하 여 SaaS 응용 프로그램에 대 한 디자인 패턴에 대해 자세히 toolearn 참조 [Azure SQL 데이터베이스를 사용한 다중 테 넌 트 SaaS 응용 프로그램에 대 한 디자인 패턴](sql-database-design-patterns-multi-tenancy-saas-applications.md)합니다.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Elastic-databases-helps-SaaS-developers-tame-explosive-growth/player]
>

탄력적 풀에서는 hello 개발자 toopurchase [탄력적 데이터베이스 트랜잭션 단위](sql-database-what-is-a-dtu.md) (Edtu) 사용의 여러 데이터베이스 tooaccommodate 예측할 수 없는 기간 하 여 개별 데이터베이스에서 공유 풀에 대 한 합니다. 풀에 대 한 hello eDTU 요구 사항은 해당 데이터베이스의 집계 사용률이 hello에 의해 결정 됩니다. 사용 가능한 toohello 풀 Edtu의 hello 수 hello 개발자 예산에 의해 제어 됩니다. hello 개발자 단순히 데이터베이스 toohello 풀을 추가 하 고, hello 최소 및 최대 Edtu hello 데이터베이스에 대 한 설정, 다음 자신의 예산에 따라 hello 풀의 eDTU hello를 설정 합니다. 개발자는 tooseamlessly 증가 자신의 서비스에서 lean 시작 tooa 성숙한 비즈니스에서 풀을 사용할 수 배율 계속 해 서 증가 합니다.

Hello 풀 내에서 개별 데이터베이스 hello 유연성 tooauto 단위 매개 변수 설정 내에서 제공 됩니다. 데이터베이스는 부하가 많은 Edtu toomeet 수요가 사용할 수 있습니다. 낮은 부하량에서 데이터베이스는 적게 사용하고 부하가 없는 데이터베이스는 eDTU를 사용하지 않습니다. 관리 작업을 간소화 hello 전체 풀에 대 한 아닌 단일 데이터베이스에 대 한 리소스를 프로 비전 합니다. 또한 hello 풀에 대 한 예측 가능한 할당 했습니다. 추가 Edtu tooan 기존 풀 중단 시간 없이 데이터베이스를 추가할 수 있습니다, 그리고 tooprovide hello 추가 계산 리소스 hello 새 eDTU 예약을 제외 하 고 hello 데이터베이스 toobe 이동 해야 할 수 있습니다. 마찬가지로, 추가 eDTU가 더 이상 필요하지 않은 경우에는 언제든지 기존 풀에서 제거할 수 있습니다. 및 추가 하거나 데이터베이스 toohello 풀 뺄 수 있습니다. 데이터베이스가 예측 가능한 방식으로 리소스를 사용하는 경우 리소스를 이동합니다.

만들고 hello를 사용 하 여 탄력적 풀을 관리할 수 [Azure 포털](sql-database-elastic-pool-manage-portal.md), [PowerShell](sql-database-elastic-pool-manage-powershell.md), [TRANSACT-SQL](sql-database-elastic-pool-manage-tsql.md), [C#](sql-database-elastic-pool-manage-csharp.md), REST API hello 및 합니다. 

## <a name="when-should-you-consider-a-sql-database-elastic-pool"></a>SQL Database 탄력적 풀은 언제 고려해야 하나요?

풀은 특정 사용 패턴을 사용하여 많은 수의 데이터베이스에 적합합니다. 주어진 데이터 베이스에 대해, 이 패턴은 상대적으로 사용률 급증이 드물고 평균 사용률이 낮음으로 규정됩니다.

hello 더 많은 데이터베이스 추가할 수 있습니다 tooa 풀 hello 큰 절감 효과 됩니다. 응용 프로그램 사용률 패턴을 따라 개만 두 S3 데이터베이스도 가능한 toosee 절약 것합니다.  

hello 다음 섹션에서는 알아야 어떻게 tooassess 경우 데이터베이스의 특정 컬렉션에서 풀의 이점을 얻을 수 있습니다. hello 예제 표준 풀 사용 하지만 hello 동일한 원칙도 적용 tooBasic 및 프리미엄 풀입니다.

### <a name="assessing-database-utilization-patterns"></a>데이터베이스 사용량 패턴 평가

hello 다음 그림은 유휴 시간을 소모 많은 하지만 정기적으로 활동에 급증 하는 데이터베이스의 예제. 다음은 풀에 적합한 사용률 패턴입니다.

   ![풀에 적합한 단일 데이터베이스](./media/sql-database-elastic-pool/one-database.png)

Hello에 대 일 분 기간에 표시 된 것 too90 Dtu DB1 최대치 하지만 전반적인 평균 사용 보다 작거나 5 개 Dtu. 성능 수준이 한 S3 toorun를 단일 데이터베이스에이 작업 필요 하지만,이 리소스의 대부분이 상태로 hello 사용 하지 않는 활동이 적은 기간 동안.

풀을 여러 데이터베이스 간에 공유 사용 하지 않는 Dtu toobe 이러한 있으며 하므로 hello Dtu 필요한 및 전반적인 비용을 줄입니다.

Hello 앞의 예제에서 빌드 추가 포함 된 데이터베이스가 있는 비슷한 사용률 패턴 DB1로 가정 합니다. Hello 아래 다음 두 그림에 4 개의 데이터베이스의 사용률이 hello 및 20 데이터베이스를 계층에 동일한 그래프의 시간에 따라 해당 사용률이 tooillustrate hello 겹치지 않는 특성 hello에:

   ![풀에 적합한 사용 패턴을 가진 네 개의 데이터베이스](./media/sql-database-elastic-pool/four-databases.png)

  ![풀에 적합한 사용 패턴을 가진 20개의 데이터베이스](./media/sql-database-elastic-pool/twenty-databases.png)

모든 20 데이터베이스에 걸쳐 집계 DTU 사용률 hello hello 그림 앞에서 hello 검정 선으로 표시 됩니다. 이것을 보여 줍니다 hello 집계 DTU 사용률 하지 100 Dtu를 초과할 hello 20 데이터베이스가 기간 동안 100 Edtu를 공유할 수 있다는 것을 나타냅니다. 그러면 Dtu는 20 x 감소 하 고는 13 x 가격 비교 감소 tooplacing 각 단일 데이터베이스에 대 한 성능 수준 s 3의에서 hello 데이터베이스.

이 예제는 다음 이유로 hello에 대 한 적합 합니다.

* 최고사용률과 데이터베이스당 평균 사용률간에 큰 차이가 있습니다.  
* 각 데이터베이스에 대 한 hello 최고 사용률 서로 다른 지점에서 시간에 발생합니다.
* eDTU는 많은 데이터베이스 간에 공유됩니다.

풀의 가격 hello는 hello 풀 Edtu의 함수입니다. 풀에 대 한 hello eDTU 단가 1.5 x à ï 단일 데이터베이스에 대 한 hello DTU 단위 가격 보다 큰 동안 **풀 Edtu 많은 데이터베이스에서 공유할 수 있습니다 및 더 적은 총 Edtu 필요한**합니다. 가격 책정 및 eDTU 공유 이러한 차이의 풀을 제공할 수 있는 hello 가격 절약 잠재적인 hello 기반이 됩니다.  

hello 다음 규칙 가장 관련 toodatabase 개수 및 데이터베이스 사용률 도움말 tooensure 풀을 전달 하는 단일 데이터베이스에 toousing 성능 수준에 비해 비용이 감소 합니다.

### <a name="minimum-number-of-databases"></a>데이터베이스의 최소 수

단일 데이터베이스에 대 한 성능 수준의 Dtu hello의 hello 합계 이상 1.5 x à ï hello Edtu hello 풀에 필요한 경우 탄력적 풀 비용 효율적입니다. 사용 가능한 크기에 대해서는 [탄력적 풀 및 탄력적 데이터베이스에 대한 eDTU 및 저장소 제한](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)을 참조하세요.

***예제***<br>
두 개 이상의 S3 데이터베이스 또는 최소 15 S0 데이터베이스에 필요한 100 eDTU 풀 toobe 단일 데이터베이스에 대 한 성능 수준을 사용할 때 보다 더 효율적입니다.

### <a name="maximum-number-of-concurrently-peaking-databases"></a>최대 동시에 최고 데이터베이스

Edtu를 공유 하 여 풀의 일부 데이터베이스가 동시에 사용할 수 Edtu toohello도 사용할 수 있는를 단일 데이터베이스에 대 한 성능 수준을 사용 하는 경우. 피크 동시에 더 적은 데이터베이스 hello, hello 낮은 hello 풀 eDTU 집합과 hello 더 비용 효율적인 hello 풀의 사용이 될 수 있습니다. 일반적으로 되지 보다 더 많은 hello 풀의 hello 데이터베이스의 2/3 (또는 67%) 해야 tootheir eDTU 동시에 최고를 제한 합니다.

***예제***<br>
200 eDTU 풀에 3 개의 S3 데이터베이스에 대 한 tooreduce 비용, 이러한 데이터베이스의 최대 두 개의 동시에 로드가 해당 사용률에서입니다. 그렇지 않은 경우 4 개의 S3 데이터베이스 두 개를 초과할 동시에 최고 hello 풀 Edtu 200 보다 큰 toobe toomore가 있어야 합니다. 더 많은 S3 데이터베이스 추가 toobe 해야 hello 풀 Edtu 200 보다 크기가 조정 된 toomore 이면 단일 데이터베이스에 대 한 성능 수준 보다 낮은 toohello 풀 tookeep 비용입니다.

Note이 예제 hello 풀의 다른 데이터베이스의 사용률을 고려 하지 않습니다. 모든 데이터베이스 데이터베이스의 경우 일부 사용률 특정된 시점에서 시간으로, 다음 2/3 보다 작은 (또는 67%) hello 데이터베이스의 로드가 동시에 합니다.

### <a name="dtu-utilization-per-database"></a>데이터베이스당 DTU 사용률
상당한 차이가 hello와 데이터베이스의 평균 사용률 장시간 사용률이 낮은의 짧은 높은 사용률을 나타냅니다. 이 사용률 패턴은 데이터베이스에서 리소스를 공유 하기에 이상적입니다. 최고 사용률이 평균사용률의 1.5배 이상이 될 때 풀에 대한 데이터베이스를 고려해야 합니다.

***예제***<br>
Too100 Dtu 최대 및 평균 Dtu 67을 사용 하는 S3 데이터베이스 풀의 Edtu를 공유 하는 데 적합 less는 또는 합니다. Too20 Dtu 최대 및 평균 Dtu 13을 사용 하는 S1 데이터베이스 또는 또는 less는 풀에 대 한 적합 합니다.

## <a name="how-do-i-choose-hello-correct-pool-size"></a>Hello 올바른 풀 크기를 선택 하려면 어떻게 해야 합니까?

풀에 대 한 최적의 크기 hello hello 집계 Edtu와 풀 hello에서에서 모든 데이터베이스에 필요한 저장소 리소스에 따라 달라 집니다. 이에서는 hello hello 다음 중 더 큰 숫자를 결정 합니다.

* 최대 Dtu hello 풀의 모든 데이터베이스에서 사용 합니다.
* Hello 풀의 모든 데이터베이스에 사용 되는 최대 저장소 바이트입니다.

사용 가능한 크기에 대해서는 [탄력적 풀 및 탄력적 데이터베이스에 대한 eDTU 및 저장소 제한](#what-are-the-resource-limits-for-elastic-pools)을 참조하세요.

SQL 데이터베이스는 자동으로 기존 SQL 데이터베이스 서버에서 데이터베이스의 hello 기록 리소스 사용량을 평가 하 고 hello Azure 포털에서에서 hello 적절 한 풀 구성을 권장 합니다. 또한 toohello 권장 사항, 기본 제공 경험 hello 서버에 있는 데이터베이스의 사용자 지정 그룹에 대 한 hello eDTU 사용량을 예측합니다. 이렇게 하면 toodo "what-if" 분석 하 여 대화형으로 데이터베이스 toohello 풀을 추가 및 제거 tooget 리소스 사용 현황 분석 및 조언을 변경 내용을 커밋하기 전에 크기 조정. 방법은 [탄력적 풀 모니터링, 관리 및 크기 조정](sql-database-elastic-pool-manage-portal.md)을 참조하세요.

도구를 사용할 수 없는 위치 하는 경우, 단계별 hello 다음 풀 인지 단일 데이터베이스에 비해 더 비용 예측 데 도움이 됩니다.

1. 다음과 같이 hello 풀에 필요한 예상 hello Edtu:

   MAX(<*총 DB 수* X *DB당 평균 DTU 사용률*>,<br>
   <*동시 최고 DB의 수* X *DB당 최고 DTU 사용률*)
2. Hello hello 풀의 모든 hello 데이터베이스에 필요한 바이트 수를 추가 하 여 hello 풀에 필요한 hello 저장 공간을 예측 합니다. 이 저장소의이 크기를 제공 하는 hello eDTU 풀 크기를 결정 합니다. eDTU 풀 크기에 기반한 풀 저장소 한도는 [탄력적 풀 및 탄력적 데이터베이스에 대한 eDTU 및 저장소 제한](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)을 참조하세요.
3. 1 단계 및 2 단계에서 hello hello eDTU 예측 중 더 큰 숫자를 가져옵니다.
4. Hello 참조 [SQL 데이터베이스 가격 책정 페이지](https://azure.microsoft.com/pricing/details/sql-database/) 찾기 hello 작은 eDTU 풀 크기는 3 단계부터에서 hello 예상 보다 크면 합니다.
5. 단일 데이터베이스에 대 한 적절 한 성능 수준 hello를 사용 하 여의 5 단계 toohello 가격에서 hello 풀 가격을 비교 합니다.

### <a name="changing-elastic-pool-resources"></a>탄력적 풀 리소스 변경

Hello 리소스 사용 가능한 tooan 탄력적 풀의 리소스 수요에 따라을 늘리거나 줄일 수 있습니다.

* 5 분 이내에 완료 데이터베이스 마다 데이터베이스 또는 최대 Edtu 당 hello 최소 Edtu를 일반적으로 변경 합니다.
* Hello Edtu 풀 당 변경 hello hello 풀의 모든 데이터베이스에 사용 되는 공간의 총 금액에 따라 달라 집니다. 변경 시간은 100GB당 평균 90분 이하입니다. 예를 들어 hello 총 공간에서 사용 하는 경우 hello 풀의 모든 데이터베이스는 200GB, 다음 hello 필요한 hello 풀 eDTU 풀 당 변경에 대 한 대기 시간은 3 시간 이내입니다.

## <a name="what-are-hello-resource-limits-for-elastic-pools"></a>탄력적 풀에 대 한 hello 리소스 제한 사항은 무엇입니까?

다음 표에서 hello 탄력적 풀의 hello 리소스 제한을 설명 합니다.  참고 hello 리소스 제한을 탄력적 풀의 개별 데이터베이스는 일반적으로 hello Dtu 및 hello 서비스 계층에 따라 풀 외부에서 단일 데이터베이스의 경우와 동일 합니다.  예를 들어 S2 데이터베이스에 대 한 최대 동시 작업자 hello 120 작업자입니다.  따라서 표준 풀에서 데이터베이스에 대 한 최대 동시 작업자 hello 이기도 120 작업자 이면 hello hello 풀 데이터베이스당 최대 DTU (즉, 해당 tooS2) 50 Dtu 합니다.

[!INCLUDE [SQL DB service tiers table for elastic pools](../../includes/sql-database-service-tiers-table-elastic-pools.md)]

탄력적 풀의 모든 Dtu를 사용 하는 hello 풀의 각 데이터베이스는 같은 양의 리소스 tooprocess 쿼리를 받습니다.  SQL 데이터베이스 서비스 hello 공정성 계산 시간의 동일한 분할 영역을 확인 하 여 데이터베이스 간에 공유 되는 리소스를 제공 합니다. 탄력적 풀 리소스 공정성 공유는 또한 tooany의 데이터베이스당 DTU 최소값 hello tooa 0이 아닌 값으로 설정 되어 때 tooeach 데이터베이스 보장 하는 리소스입니다.

### <a name="database-properties-for-pooled-databases"></a>풀링된 데이터베이스에 대한 데이터베이스 속성

다음 표에서 hello 풀링된 데이터베이스에 대 한 hello 속성을 설명 합니다.

| 속성 | 설명 |
|:--- |:--- |
| 데이터베이스당 최대 eDTU |hello hello 풀의 모든 데이터베이스를 사용할 수 있는, 사용 가능한 기반으로 할 경우 사용률 hello 풀의 다른 데이터베이스에서 Edtu의 최대 수입니다.  데이터베이스당 최대 eDTU는 데이터베이스에 대해 리소스를 보장하지 않습니다.  이 설정은 hello 풀의 tooall 데이터베이스 적용 되는 전역 설정이입니다. 데이터베이스 사용에 데이터베이스당 최대 Edtu 충분히 높은 toohandle 최대치를 설정 합니다. 과도 한 커밋의 어느 정도 여야 hello 풀은 일반적으로 데이터베이스에 대 한 핫 및 콜드 사용 패턴 가정 하므로 여기서 모든 데이터베이스는 하지 동시에 데 최고 합니다. 예를 들어 데이터베이스 마다 hello 최대 사용률은 20 Edtu 되며 hello 풀의 hello 100 데이터베이스의 20%만 hello에 대 한 최대 동시 합니다.  데이터베이스당 최대 hello eDTU too20 Edtu 설정 되 면 다음 경우 합리적인 tooovercommit hello 풀 집합 hello Edtu 풀 too400 당 및 5 번입니다. |
| 데이터베이스당 최소 eDTU |hello 최소 Edtu 수 hello 풀의 어떤 데이터베이스도 보장 됩니다.  이 설정은 hello 풀의 tooall 데이터베이스 적용 되는 전역 설정이입니다. 데이터베이스당 hello 최소 eDTU too0를 설정할 수 있습니다 및 hello 기본값 이기도 합니다. 이 속성은 tooanywhere 데이터베이스당 0과 hello 평균 eDTU 사용률 간에 설정 됩니다. hello 곱일 hello 데이터베이스 수에 hello 풀 및 데이터베이스당 hello 최소 Edtu 풀 당 hello Edtu를 초과할 수 없습니다.  예를 들어, 풀에 20 데이터베이스 데이터베이스당 eDTU 최소값 hello too10 Edtu를 설정 하는 경우 다음 hello Edtu 풀 당 해야 200 Edtu 이상이 합니다. |
| 데이터베이스당 최대 데이터 저장소 |최대 저장소 풀에서 데이터베이스에 대 한 hello 합니다. 데이터베이스 저장소는 나머지 풀 저장소 및 데이터베이스당 최대 저장소 중 더 작은 숫자 제한 toohello 풀링된 데이터베이스 풀 저장소를 공유 합니다. 데이터베이스당 최대 저장소 toohello hello 데이터 파일의 최대 크기를 참조 하 고 로그 파일에서 사용 하는 hello 공간은 포함 하지 않습니다. |
|||

## <a name="using-other-sql-database-features-with-elastic-pools"></a>탄력적 풀과 기타 SQL Database 기능 사용

### <a name="elastic-jobs-and-elastic-pools"></a>탄력적 작업 및 탄력적 풀

풀을 통해 **[탄력적 작업](sql-database-elastic-jobs-overview.md)**의 스크립트를 실행하여 관리 작업이 간소화됩니다. 탄력적 작업은 많은 수의 데이터베이스와 관련된 번거로움을 대부분 없애 줍니다. toobegin, 참조 [탄력적 작업 시작](sql-database-elastic-jobs-getting-started.md)합니다.

여러 데이터베이스를 사용하기 위한 다른 데이터베이스 도구에 대한 자세한 내용은 [Azure SQL Database를 사용하여 확장](sql-database-elastic-scale-introduction.md)을 참조합니다.

### <a name="business-continuity-options-for-databases-in-an-elastic-pool"></a>탄력적 풀의 데이터베이스에 대한 비즈니스 연속성 옵션
데이터베이스 풀링된 일반적으로 지원 hello 동일 [비즈니스 연속성 기능](sql-database-business-continuity.md) 는 사용할 수 있는 toosingle 데이터베이스입니다.

- **지정 시간 복원**: 지점--시간 복원 시간에 풀 tooa 특정 시점에 자동으로 데이터베이스 백업을 toorecover 데이터베이스를 사용 합니다. [지정 시간 복원](sql-database-recovery-using-backups.md#point-in-time-restore)

- **지역에서 복원은**: hello 데이터베이스가 호스트 되는 hello 영역의 인시던트 때문에 데이터베이스를 사용할 수 없는 경우 지역 복원 hello 기본 복구 옵션을 제공 합니다. 참조 [Azure SQL 데이터베이스 또는 장애 조치 tooa 보조 복원](sql-database-disaster-recovery.md)

- **활성 지역 복제**: 지역 복원에서 제공하는 것보다 더 까다로운 복구 요구 사항이 있는 응용 프로그램의 경우 [활성 지역 복제](sql-database-geo-replication-overview.md)를 구성합니다.

## <a name="manage-sql-database-elastic-pools-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 SQL 데이터베이스 탄력적 풀 관리

### <a name="creating-a-new-sql-database-elastic-pool-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 새 SQL 데이터베이스 탄력적 풀을 만들려면

두 가지 방법으로 hello Azure 포털에서에서 탄력적 풀을 만들 수 있습니다. Hello 풀 설치 프로그램을 시작 하 든 hello 서비스에서 권장을 알고 있는 경우 처음부터이 수행할 수 있습니다. SQL 데이터베이스에 더 비용 효율적 사용 원격 분석 데이터베이스에 대 한 지난 hello에 근거 하는 경우 탄력적 풀 설치 프로그램을 권장 하는 기본 제공 인텔리전스 있습니다. 

기존 탄력적 풀을 만들어 **서버** hello 포털에서 블레이드는 hello 가장 쉬운 방법은 toomove 기존 데이터베이스를 탄력적 풀으로 합니다. 검색 하 여 탄력적 풀을 만들 수도 있습니다 **SQL 탄력적인 풀** hello에 **마켓플레이스** 클릭 하거나 **+ 추가** hello에 **SQL 탄력적 풀**블레이드를 탐색 합니다. 워크플로 프로 비전 하는이 풀을 통해 기존 또는 새 서버 수 toospecify 됩니다.

> [!NOTE]
> 서버에서 여러 풀을 만들 수 있지만 hello에 서로 다른 서버에서 데이터베이스를 추가할 수 없습니다 동일한 풀입니다.
>  

hello 풀의 가격 책정 계층이 결정 hello hello 그룹 및 hello 최대 수 (최대 eDTU) Edtu 및 저장소 (Gb) 사용 가능한 tooeach 데이터베이스의 사용 가능한 toohello elastics 기능 합니다. 자세한 내용은 [서비스 계층](#edtu-and-storage-limits-for-elastic-pools)을 참조하세요.

hello toochange hello 풀에 대 한 가격 책정 계층을 클릭 **가격 책정 계층**, 가격 책정 계층을 하 고 클릭 hello 클릭 **선택**합니다.

> [!IMPORTANT]
> Hello 가격 책정 계층을 선택 하 고 클릭 하 여 변경 내용을 적용 한 후 **확인** hello 마지막 단계에서 가격 책정 계층 hello 풀의 수 toochange hello 됩니다. toochange hello 기존 탄력적 풀의 가격 책정 계층을 hello 원하는 가격 책정 계층에서 탄력적 풀을 만들거나 hello 데이터베이스 toothis 새 풀을 마이그레이션합니다.
>

사용 하는 hello 데이터베이스 데이터베이스의 기록 사용 만큼 원격 분석이 충분 경우 hello **예상 eDTU 및 GB 사용량** 그래프 및 hello **실제 eDTU 사용량** 가로 막대형 차트 업데이트 toohelp 구성 확인 의사 결정 합니다. 또한 hello 서비스가 제공할 수 있습니다 권장 메시지 toohelp 풀 hello 적정 크기로 있습니다.

hello SQL 데이터베이스 서비스는 사용 현황을 평가 하 고 단일 데이터베이스를 사용 하 여 보다 비용 효율성이 되었을 때 하나 이상의 풀은 것이 좋습니다. 각 권장 사항은 hello 풀에 가장 잘 맞는 hello 서버 데이터베이스의 고유 하위 집합으로 구성 됩니다.

![권장되는 풀](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

hello 풀 권장이 됩니다.

- Hello 풀 (Basic, Standard, Premium 또는 프리미엄 RS)에 대 한 가격 책정 계층
- 적절한 **풀 eDTU** (풀당 최대 eDTU)
- hello **최대 eDTU** 및 **eDTU Min** 데이터베이스당
- hello hello 풀에 대 한 권장된 데이터베이스 목록

> [!IMPORTANT]
> hello 서비스 고려 hello 원격 분석의 지난 30 일 동안 풀 권장할 때 합니다. 탄력적 풀에 대 한 대상으로 간주 하는 데이터베이스 toobe에 대 한 일 이상 있어야 합니다. 이미 탄력적 풀에 있는 데이터베이스는 탄력적 풀 권장 사항에 대한 후보로 간주되지 않습니다.
>

hello 서비스의 리소스 수요를 평가 및 단일 이동 hello의 비용 효율 데이터베이스 각 서비스 계층에서의 hello 풀에 동일한 계층입니다. 예를 들어 서버의 모든 Standard 데이터베이스는 표준 탄력적 풀에 적합한지 평가됩니다. 즉, hello 서비스 계층 간 권장 사항을 표준 데이터베이스는 프리미엄 풀으로 이동 하는 등을 만들지 않습니다.

데이터베이스 toohello 풀을 추가한 다음 권장 사항은 동적으로 생성 되 hello 선택한 hello 데이터베이스의 기존 사용량 기반 합니다. 이러한 권장 hello eDTU 및 GB 사용 현황 차트에서 고 hello hello 맨 위의 권장 사항 배너에 표시 됩니다 **풀 구성** 블레이드입니다. 이러한 권장 사항은 의도 한 tooassist 특정 데이터베이스에 대해 최적화 된 탄력적 풀을 만드는 있습니다.

![동적 권장 사항](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

### <a name="manage-and-monitor-an-elastic-pool"></a>탄력적 풀 관리 및 모니터링

Hello Azure 포털에서에서 탄력적 풀과 해당 풀 내의 hello 데이터베이스의 hello 사용률을 모니터링할 수 있습니다. 변경 내용 집합이 tooyour 탄력적 풀을 확인 하 고 모든 변경 내용을 hello 동일 제출할 수도 있습니다 시간입니다. 이러한 변경 내용에는 데이터베이스 추가 또는 제거, 탄력적 풀 설정 변경, 데이터베이스 설정 변경이 포함됩니다.

다음 그래픽 hello 예제 탄력적 풀을 보여 줍니다. hello 보기에는 다음이 포함 됩니다.

*  Hello 탄력적 풀과 hello 풀에 포함 된 hello 데이터베이스의 리소스 사용 모니터링에 대 한 차트를 제공 해야 합니다.
*  hello **구성** 풀 단추 toomake toohello 탄력적 풀을 변경 합니다.
*  hello **데이터베이스 만들기** 데이터베이스를 만드는 단추 toohello 현재 탄력적 풀을 추가 합니다.
*  목록의 모든 데이터베이스에 대해 Transact SQL 스크립트를 실행하여 많은 데이터베이스를 관리하는 데 도움이 되는 탄력적 작업

![풀 보기](./media/sql-database-elastic-pool-manage-portal/basic.png)

해당 리소스 사용률 tooa 특정 풀 toosee를 이동할 수 있습니다. 기본적으로 hello 풀 지난 1 시간 동안 hello에 대 한 구성된 tooshow 저장소 및 eDTU 사용량은입니다. hello 차트에는 다양 한 시간 창에 대해 구성 된 tooshow 가지 다른 메트릭으로 수 있습니다. Hello 클릭 **리소스 사용률** 아래 차트 **탄력적 풀 모니터링** tooshow hello에 대 한 자세히 보기 hello 지정 된 기간 동안 메트릭을 지정 합니다.

![탄력적 풀 모니터링](./media/sql-database-elastic-pool-manage-portal/basic-2.png)

![메트릭 블레이드](./media/sql-database-elastic-pool-manage-portal/metric.png)

### <a name="toocustomize-hello-chart-display"></a>toocustomize hello 차트 표시

CPU 비율, 데이터 IO 백분율 및 사용 되는 로그 IO 백분율 등 기타 메트릭을 hello 차트 및 hello 메트릭 블레이드 toodisplay 편집할 수 있습니다.

![편집 클릭](./media/sql-database-elastic-pool-manage-portal/edit-metric.png)

Hello에 **차트 편집** 폼 (지난 시간을 오늘 또는 지난 주), 시간 범위를 선택 하거나 클릭 수 **사용자 지정** tooselect 날짜 범위에 속하는 hello 지난 2 주입니다. 가로 막대형 또는 꺾은선형 차트 중에서 선택할 수 있으며 다음 hello 리소스 toomonitor 선택 수 없습니다.

> [!Note]
> 동일한 hello에 hello 동일한 측정 단위는 hello에 표시 될 수 있는 메트릭 차트에 시간입니다. 예를 들어 "eDTU percentage"를 선택 하는 경우 선택할 수 있습니다만 기타 메트릭을 (백분율)으로 hello 측정 단위입니다.
>

[편집 클릭](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

### <a name="manage-and-monitor-databases-in-an-elastic-pool"></a>탄력적 풀의 데이터베이스 관리 및 모니터링

문제 발생 가능성에 대한 개별 데이터베이스를 모니터링할 수도 있습니다. **탄력적 데이터베이스 모니터링**에는 다섯 개의 데이터베이스에 대한 메트릭을 표시하는 차트가 있습니다. 기본적으로 hello 차트 표시 hello 상위 5 데이터베이스 hello 풀의 평균 eDTU 사용량 hello에 의해 지난 시간 합니다. 

![탄력적 풀 모니터링](./media/sql-database-elastic-pool-manage-portal/basic-3.png)

Hello 클릭 **hello 지난 시간에 대 한 데이터베이스에 대 한 eDTU 사용량** 아래 **탄력적 데이터베이스 모니터링**합니다. 그러면 열립니다 **데이터베이스 리소스 사용률** hello 데이터베이스 사용 hello 풀에 대 한 자세히 보기를 제공 합니다. Hello 블레이드의 hello 아래쪽 표에 hello를 사용 하 선택할 수 있습니다 데이터베이스가 hello 풀 toodisplay에 hello 차트 (too5 데이터베이스)를 사용 합니다. Hello 메트릭 및 시간 창을 클릭 하 여 hello 차트에 표시를 사용자 지정할 수도 있습니다 **차트 편집**합니다.

![데이터베이스 리소스 사용률 블레이드](./media/sql-database-elastic-pool-manage-portal/db-utilization.png)

### <a name="toocustomize-hello-view"></a>toocustomize hello 보기

Hello 차트 tooselect (지난 시간 또는 지난 24 시간), 시간 범위를 편집 하거나 클릭 수 **사용자 지정** 지난 2 주 toodisplay hello에 다른 하루 tooselect 합니다.

![차트 편집 클릭](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

![사용자 지정 클릭](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

Hello를 클릭할 수도 있습니다 **하 여 데이터베이스를 비교할** 드롭다운 tooselect 다른 메트릭 toouse 데이터베이스를 비교 하는 경우.

![Hello 차트 편집](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a>tooselect 데이터베이스 toomonitor

Hello에 hello 데이터베이스 목록에서 **데이터베이스 리소스 사용률** 블레이드에서 hello 페이지 hello 목록을 조회 하거나 데이터베이스의 hello 이름에 입력 하 여 특정 데이터베이스를 찾을 수 있습니다. Hello 확인란 tooselect hello 데이터베이스를 사용 합니다.

![데이터베이스 toomonitor 검색](./media/sql-database-elastic-pool-manage-portal/select-dbs.png)


### <a name="add-an-alert-tooan-elastic-pool-resource"></a>경고 tooan 탄력적 풀 리소스 추가

탄력적 풀 hello 설정 하는 사용 임계값에 도달 하면 전자 메일 문자열 tooURL 끝점 toopeople 또는 경고를 전송 하는 규칙 tooan 탄력적 풀을 추가할 수 있습니다.

**tooadd 경고 tooany 리소스:**

1. Hello 클릭 **리소스 사용률** 차트 tooopen hello **메트릭을** 블레이드에서 클릭 **추가 경고**, hello에 hello 정보 입력 **경고를 추가 규칙** 블레이드 (**리소스** 작업할 때 toobe hello 풀을 자동으로 설정 됩니다).
2. 입력 **이름** 및 **설명** hello 경고 tooyou 및 hello 받는 사람을 식별 하 합니다.
3. 선택 된 **메트릭을** tooalert hello 목록에서 원하는 합니다.

    동적으로 hello 차트 메트릭 해당 toohelp에 대 한 리소스 사용률 표시 임계값을 선택 합니다.

4. **조건**(보다 큼, 보다 작음 등) 및 **임계값**을 선택합니다.
5. 선택 된 **기간** 메트릭을 hello 시간의 규칙 hello 경고 트리거 하기 전에 충족 해야 합니다.
6. **확인**을 클릭합니다.

자세한 내용은 [Azure Portal에서 SQL Database 경고 만들기](sql-database-insights-alerts-portal.md)를 참조하세요.

### <a name="move-a-database-into-an-elastic-pool"></a>탄력적 풀로 데이터베이스 이동

기존 풀에서 데이터베이스를 제거하거나 추가할 수 있습니다. hello 데이터베이스가 다른 풀 있을 수 있습니다. 그러나만 추가할 수 있습니다는에 hello 동일 데이터베이스 논리 서버입니다.

 ![풀 구성 클릭](./media/sql-database-elastic-pool-manage-portal/configure-pool.png)

![추가 toopool 클릭](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)

![데이터베이스 tooadd 선택](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

![보류 중인 풀 추가](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

![저장을 클릭합니다.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

### <a name="move-a-database-out-of-an-elastic-pool"></a>탄력적 풀 외부로 데이터베이스 이동

![데이터베이스 나열](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

![데이터베이스 나열](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

![데이터베이스 추가 및 제거 미리 보기](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

![저장을 클릭합니다.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

### <a name="change-performance-settings-of-an-elastic-pool"></a>탄력적 풀의 성능 설정 변경

탄력적 풀의 hello 리소스 사용률을 모니터링 하면서 약간씩 조정 필요한 경우도 있습니다. 아마 hello 풀 hello 성능이 나 저장소 제한 변경을 해야합니다. Hello 풀에서 toochange hello 데이터베이스 설정을 원하는 것 같습니다. 모든 시간 tooget hello 적절 한 성능 및 비용에 hello 풀의 hello 설정을 변경할 수 있습니다. 자세한 내용은 [탄력적 풀을 사용해야 하는 경우](sql-database-elastic-pool.md)를 참조하세요.

toochange hello Edtu 또는 저장소 풀 및 데이터베이스당 Edtu 당 제한 됩니다.

![탄력적 풀 리소스 사용률](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

![탄력적 풀 및 새 월별 비용 업데이트](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="manage-sql-database-elastic-pools-using-powershell"></a>PowerShell을 사용하여 SQL Database 탄력적 풀 관리

toocreate 및 Azure PowerShell과 함께 SQL 데이터베이스 탄력적 풀을 관리, PowerShell cmdlet을 다음 hello를 사용 합니다. PowerShell을 업그레이드 하거나 tooinstall를 필요한 경우 참조 [Azure PowerShell 설치 모듈](/powershell/azure/install-azurerm-ps)합니다. toocreate 데이터베이스, 서버 및 방화벽 규칙 참조를 관리 하 고 [만들기 및 Azure SQL 데이터베이스 서버 및 PowerShell을 사용 하 여 데이터베이스 관리](sql-database-servers-databases.md#manage-azure-sql-servers-databases-and-firewalls-using-powershell)합니다. 

> [!TIP]
> PowerShell 예제 스크립트를 참조 하십시오. [탄력적 풀을 만들고 풀 사이 및 PowerShell을 사용 하 여 풀에서 데이터베이스를 이동](scripts/sql-database-move-database-between-pools-powershell.md) 및 [SQL 탄력적인 풀AzureSQL데이터베이스에서PowerShell사용하여toomonitor및소수](scripts/sql-database-monitor-and-scale-pool-powershell.md).
>

| Cmdlet | 설명 |
| --- | --- |
|[New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool)|논리 SQL Server에서 Elastic Database 풀을 만듭니다.|
|[Get-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/get-azurermsqlelasticpool)|논리 SQL Server에서 탄력적 풀과 해당 속성 값을 가져옵니다.|
|[Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool)|논리 SQL Server에서 Elastic Database 풀의 속성을 수정합니다.|
|[Remove-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/remove-azurermsqlelasticpool)|논리 SQL Server에서 Elastic Database 풀을 삭제합니다.|
|[Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity)|논리 SQL server에서 탄력적 풀에 대 한 작업의 hello 상태를 가져옵니다.|
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|기존 풀 또는 단일 데이터베이스에서 새 데이터베이스를 만듭니다. |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|하나 이상의 데이터베이스를 가져옵니다.|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|데이터베이스의 속성을 설정하거나 기존 데이터베이스와 탄력적 풀 사이를 이동합니다.|
|[Remove-AzureRmSqlDatabase](/powershell/module/azurerm.sql/remove-azurermsqldatabase)|데이터베이스를 제거합니다.|

> [!TIP]
> 탄력적 풀의 많은 데이터베이스 생성 했으면 다음 hello 포털 또는 한 번에 하나의 데이터베이스만 만드는 PowerShell cmdlet을 사용 하 여 시간을 걸릴 수 있습니다. 참조를 탄력적 풀으로 tooautomate 생성 [CreateOrUpdateElasticPoolAndPopulate](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae)합니다.
>

## <a name="manage-sql-database-elastic-pools-using-hello-azure-cli"></a>Hello Azure CLI를 사용 하 여 SQL 데이터베이스 탄력적 풀 관리

toocreate hello로 SQL 데이터베이스 탄력적 풀을 관리 하 고 [Azure CLI](/cli/azure/overview), hello 다음 이름을 사용해 서 [Azure CLI SQL 데이터베이스](/cli/azure/sql/db) 명령입니다. 사용 하 여 hello [클라우드 셸](/azure/cloud-shell/overview) 브라우저에서 toorun hello CLI 또는 [설치](/cli/azure/install-azure-cli) macOS, Linux 또는 Windows에 있습니다. 

> [!TIP]
> Azure CLI 예제 스크립트에 대 한 참조 [SQL 탄력적인 풀에 Azure SQL 데이터베이스 사용 하 여 CLI toomove](scripts/sql-database-move-database-between-pools-cli.md) 및 [Azure SQL 데이터베이스에서 SQL 탄력적 풀을 사용 하 여 Azure CLI tooscale](scripts/sql-database-scale-pool-cli.md)합니다.
>

| Cmdlet | 설명 |
| --- | --- |
|[az sql elastic-pool create](/cli/azure/sql/elastic-pool#create)|탄력적 풀을 만듭니다.|
|[az sql elastic-pool list](/cli/azure/sql/elastic-pool#list)|서버에서 탄력적 풀의 목록을 반환합니다.|
|[az sql elastic-pool list-dbs](/cli/azure/sql/elastic-pool#list-dbs)|탄력적 풀에서 데이터베이스의 목록을 반환합니다.|
|[az sql elastic-pool list-editions](/cli/azure/sql/elastic-pool#list-editions)|사용 가능한 풀 DTU 설정, 저장소 용량 한도 및 데이터베이스별 설정이 포함됩니다. 순서 tooreduce 자세한 정도 추가 저장소 제한 및 데이터베이스당 설정이 기본적으로 숨겨져 있습니다.|
|[az sql elastic-pool update](/cli/azure/sql/elastic-pool#update)|탄력적 풀을 업데이트합니다.|
|[az sql elastic-pool delete](/cli/azure/sql/elastic-pool#delete)|Hello 탄력적 풀을 삭제합니다.|

## <a name="manage-sql-database-elastic-pools-using-transact-sql"></a>Transact-SQL을 사용하여 SQL Database 탄력적 풀 관리

기존 탄력적 풀 또는 TRANSACT-SQL을 사용 하는 SQL 데이터베이스 탄력적인 풀에 대 한 tooreturn 정보 내 toocreate 및 이동 데이터베이스 T-SQL 명령을 수행 하는 hello를 사용 합니다. Hello Azure 포털을 사용 하 여 이러한 명령을 실행할 수 있습니다 [SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio), [Visual Studio Code](https://code.visualstudio.com/docs), 또는 tooan Azure SQL 데이터베이스 서버를 연결 하 고 TRANSACT-SQL 전달할 수 있는 다른 프로그램 명령입니다. toocreate 데이터베이스, 서버 및 방화벽 규칙 참조를 관리 하 고 [만들기 및 Azure SQL 데이터베이스 서버 및 TRANSACT-SQL을 사용 하 여 데이터베이스 관리](sql-database-servers-databases.md#manage-azure-sql-servers-databases-and-firewalls-using-transact-sql)합니다.

> [!IMPORTANT]
> Transact-SQL을 사용하여 Azure SQL Database 탄력적 풀을 만들거나, 업데이트하거나 삭제할 수는 없습니다. 추가 하거나 탄력적 풀에서 데이터베이스를 제거할 수 있으며 기존 탄력적 풀에 대 한 Dmv tooreturn 정보를 사용할 수 있습니다.
>

| 명령 | 설명 |
| --- | --- |
|[CREATE DATABASE(Azure SQL Database)](/sql/t-sql/statements/create-database-azure-sql-database)|기존 풀 또는 단일 데이터베이스에서 새 데이터베이스를 만듭니다. 연결 된 toohello master 데이터베이스 toocreate 새 데이터베이스 여야 합니다.|
| [ALTER DATABASE (Azure SQL Database)](/sql/t-sql/statements/alter-database-azure-sql-database) |탄력적 풀 간에 데이터베이스를 이동합니다.|
|[DROP DATABASE(Transact-SQL)](/sql/t-sql/statements/drop-database-transact-sql)|데이터베이스를 삭제합니다.|
|[sys.elastic_pool_resource_stats (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-elastic-pool-resource-stats-azure-sql-database)|논리 서버에 모든 hello 탄력적 데이터베이스 풀에 대 한 리소스 사용 통계를 반환합니다. 각 Elastic Database 풀의 경우 매 15초 보고 창에 대해 한 행이 있습니다(분당 4개 행). Hello 풀의 모든 데이터베이스에서 CPU, IO, 로그, 저장소 사용량 및 동시 요청/세션 사용률을 포함 합니다.|
|[sys.database_service_objectives(Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|Azure SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스에 대 한 반환 hello edition (서비스 계층), (가격 책정 계층), 서비스 목표 및 탄력적인 풀 이름입니다. Azure SQL 데이터베이스 서버에서 toohello master 데이터베이스에 로그온 하는 경우 모든 데이터베이스에서 정보를 반환 합니다. Azure SQL 데이터 웨어하우스에 대 한 연결 된 toohello master 데이터베이스 여야 합니다.|

## <a name="manage-sql-database-elastic-pools-using-hello-rest-api"></a>Hello REST API를 사용 하 여 SQL 데이터베이스 탄력적 풀 관리

toocreate hello REST API를 사용 하 여 SQL 데이터베이스 탄력적 풀을 관리 하 고, 참조 [Azure SQL 데이터베이스 REST API](/rest/api/sql/)합니다.

## <a name="next-steps"></a>다음 단계

* 비디오는 [Azure SQL Database 탄력적 기능에 대한 Microsoft Virtual Academy 비디오 과정](https://mva.microsoft.com/training-courses/elastic-database-capabilities-with-azure-sql-db-16554)을 참조하세요.
* 탄력적 풀을 사용 하 여 SaaS 응용 프로그램에 대 한 디자인 패턴에 대해 자세히 toolearn 참조 [Azure SQL 데이터베이스를 사용한 다중 테 넌 트 SaaS 응용 프로그램에 대 한 디자인 패턴](sql-database-design-patterns-multi-tenancy-saas-applications.md)합니다.
* 탄력적 풀을 사용 하는 SaaS 자습서를 참조 하십시오. [소개 toohello Wingtip SaaS 응용 프로그램](sql-database-wtp-overview.md)합니다.
