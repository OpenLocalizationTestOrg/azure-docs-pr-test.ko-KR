---
title: "Azure SQL 데이터베이스에 아웃 aaaScaling | Microsoft Docs"
description: "Saas () 개발자는 소프트웨어를 탄력적 쉽게 만들 수, 확장 가능한 데이터베이스 hello에 이러한 도구를 사용 하 여 클라우드"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: d15a2e3f-5adf-41f0-95fa-4b945448e184
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: 82a561e07389d8619727a540fa9424248c087eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-out-with-azure-sql-database"></a>Azure SQL 데이터베이스를 사용하여 규모 확장
Hello를 사용 하 여 Azure SQL 데이터베이스를 쉽게 확장할 수 있습니다 **탄력적 데이터베이스** 도구입니다. 이러한 도구와 기능을 통해 거의 무제한 hello를 사용 하 여 데이터베이스의 리소스 **Azure SQL 데이터베이스** Saas () 응용 프로그램으로 트랜잭션 워크 로드와 특히 소프트웨어에 대 한 toocreate 솔루션입니다. 탄력적 데이터베이스 기능 hello 다음 구성 되어 있습니다.

* [탄력적 데이터베이스 클라이언트 라이브러리](sql-database-elastic-database-client-library.md): hello 클라이언트 라이브러리는 toocreate 있으며 분할 된 데이터베이스 유지 관리 하는 기능입니다.  [탄력적 데이터베이스 도구 시작하기](sql-database-elastic-scale-get-started.md)를 참조하세요.
* [탄력적 데이터베이스 분할-병합 도구](sql-database-elastic-scale-overview-split-and-merge.md): 분할된 데이터베이스 간에 데이터를 이동합니다. 다중 테 넌 트 데이터베이스 tooa 단일 테 넌 트 데이터베이스 (또는 그 반대로)에서 데이터를 이동할 때 유용 합니다. [탄력적 데이터베이스 분할-병합 도구 자습서](sql-database-elastic-scale-configure-deploy-split-and-merge.md)를 참조하세요.
* [탄력적 데이터베이스 작업](sql-database-elastic-jobs-overview.md) (미리 보기): 사용 하 여 Azure SQL 데이터베이스의 많은 toomanage 작업 합니다. 작업을 사용하여 스키마 변경, 자격 증명 관리, 참조 데이터 업데이트, 성능 데이터 수집 또는 테넌트(고객) 원격 분석 수집 등의 관리 작업을 쉽게 수행합니다.
* [탄력적 데이터베이스 쿼리](sql-database-elastic-query-overview.md) (미리 보기): 여러 데이터베이스에 걸쳐 있는 toorun Transact SQL 쿼리를 사용 하면 됩니다. 이 Excel, PowerBI, Tableau 등과 같은 연결 tooreporting 도구를 사용 합니다.
* [탄력적 트랜잭션을](sql-database-elastic-transactions-overview.md):이 기능을 통해 Azure SQL 데이터베이스에서 여러 데이터베이스에 걸쳐 있는 toorun 트랜잭션 있습니다. 탄력적 데이터베이스 트랜잭션 ADO.NET을 사용 하 여.NET 응용 프로그램에 사용할 수 있으며 hello를 사용 하 여 hello 친숙 한 프로그래밍 환경에 통합 [리스트 클래스](https://msdn.microsoft.com/library/system.transactions.aspx)합니다.

아래 hello 그래픽 hello를 포함 하는 아키텍처를 보여 줍니다. **탄력적 데이터베이스 기능** 데이터베이스 관계 tooa 컬렉션에 있습니다.

이 그래픽 hello 데이터베이스의 스키마를 나타냅니다. 데이터베이스 hello로 색과 같은 공유 hello 동일한 스키마입니다.

1. **Azure SQL 데이터베이스** 집합은 분할 아키텍처를 사용하여 Azure에서 호스트됩니다.
2. hello **탄력적 데이터베이스 클라이언트 라이브러리** 사용 되는 toomanage 분할 영역이 설정 되어 있습니다.
3. Hello 데이터베이스의 하위 집합에 포함 된 **탄력적 풀**합니다. ( [풀이란?](sql-database-elastic-pool.md)참조).
4. **탄력적 데이터베이스 작업** 은 모든 데이터베이스에 대해 예약된 또는 임시 T-SQL 스크립트를 실행합니다.
5. hello **분할 / 병합 도구** 하나의 분할 tooanother에서 사용 되는 toomove 데이터입니다.
6. hello **탄력적 데이터베이스 쿼리** toowrite hello 분할 집합의 모든 데이터베이스에 걸쳐 있는 쿼리일 수 있습니다.
7. **탄력적 트랜잭션을** toorun 트랜잭션이 여러 데이터베이스에 걸쳐 있습니다. 

![탄력적 데이터베이스 도구][1]

## <a name="why-use-hello-tools"></a>Hello 도구를 사용 하는 이유는?
클라우드 응용 프로그램에 대한 탄력성 및 규모 달성은 VM 및 Blob 저장소에 대해 복잡하지 않습니다. 단순히 단위를 더하거나 빼고 거듭제곱 수를 늘립니다. 하지만 관계형 데이터베이스의 상태 저장 데이터 처리는 과제로 남아 있습니다. 이러한 시나리오에서 발생하는 문제:

* 관계형 hello에 대 한 용량 확장 및 축소 데이터베이스 작업의 일부입니다.
* 데이터의 특정 하위 집합에 영향을 발생시킬 수 있는 핫스팟 관리 - 예: 특히 바쁜 최종 고객(테넌트)

일반적으로 시나리오 이와 같은 더 큰 규모의 데이터베이스 서버 toosupport hello 응용 프로그램에 투자 하 여 해결 되었습니다. 그러나이 옵션은 미리 정의 된 상용 하드웨어에서 모든 처리가 발생 하는 hello 클라우드에서 제한 됩니다. 대신, 데이터 배포와 동일 하 게 구조화 된 많은 데이터베이스에서 처리 ("분할" 라고 하는 확장 패턴)는 대체 tootraditional 수직 방식으로 비용 및 탄력성 측면에서 모두.

## <a name="horizontal-and-vertical-scaling"></a>수평 및 수직적 크기 조정
아래 hello 그림 hello hello 기본적인 방법을 hello 탄력적 데이터베이스를 확장할 수 있는 크기 조정의 가로 및 세로 크기를 보여 줍니다.

![수평 규모 확장과 수직 규모 확장 비교][2]

가로 배율 순서 tooadjust 용량 또는 전반적인 성능 tooadding 또는 제거 데이터베이스 참조합니다. “확장"이라고도 합니다. 컬렉션에서 동일 하 게 구조화 된 데이터베이스의 데이터가 분할 하는 분할은 일반적인 방식으로 tooimplement 가로 크기 조정 합니다.  

세로 크기 조정은 tooincreasing 또는 개별 데이터베이스의 성능 수준을 hello 감소-"를 확장 합니다."로 알려져도

대부분의 클라우드 규모 데이터베이스 응용 프로그램에 이러한 두 전략의 조합을 사용 합니다. 예를 들어, 서비스 응용 프로그램으로 소프트웨어 가로 크기 조정 tooprovision 새 최종 고객 및 세로 배율 tooallow 각 최종 사용자의 데이터베이스 toogrow 또는 축소 리소스 hello 작업별 필요에 따라 사용할 수 있습니다.

* Hello를 사용 하 여 관리는 수평적 확장 [탄력적 데이터베이스 클라이언트 라이브러리](sql-database-elastic-database-client-library.md)합니다.
* Azure PowerShell cmdlet toochange hello 서비스 계층을 사용 하 여 수행은 세로 크기 조정 탄력적 풀의 데이터베이스를 배치 하 여 합니다.

## <a name="sharding"></a>분할
*분할* 기술을 toodistribute를 동일 하 게 구조화 된 데이터의 양이 많은 독립적인 데이터베이스 수에서 합니다. 특히 최종 고객 또는 비즈니스에 대한 SAAS(Software as a Service) 제품을 만드는 클라우드 개발자가 이 기법을 많이 사용합니다. 이러한 최종 고객 참조 tooas "테 넌 트" 경우가 많습니다. 분할은 다음과 같은 여러 가지 이유로 필요할 수 있습니다.  

* hello 총 데이터 양이 너무 커서 toofit 단일 데이터베이스의 hello 제약 조건 내에서
* hello 트랜잭션 처리량의 hello 전반적인 작업 부하는 단일 데이터베이스의 hello 기능을 초과 하
* 테넌트는 물리적으로 서로 격리되어야 할 수 있으므로 각 테넌트에는 별도의 데이터베이스가 필요합니다.
* 데이터베이스의 다양 한 섹션 규정 준수, 성능 또는 지정 학적 상의 이유로 여러 지역에서 tooreside가 필요할 수 있습니다.

분산된 장치에서 데이터 수집 등의 다른 시나리오에서 분할에 사용 되는 toofill 일시적으로 구성 되는 데이터베이스 집합이 될 수 있습니다. 예를 들어 tooeach 하루 또는 한 주 별도 데이터베이스에 전용 될 수 있습니다. 이 경우 hello 분할 키에는 정수 나타내는 hello 날짜 (hello 분할 된 테이블의 모든 행에 있는) 될 수 있습니다 및 hello 범위를 포함 하는 데이터베이스의 hello 응용 프로그램 toohello 하위 집합으로 라우팅되어야 하며 날짜 범위에 대 한 정보를 검색 하는 쿼리 질문입니다.

분할 응용 프로그램에서 모든 트랜잭션이 제한 tooa 수에 가장 적합 단일 분할 키의 값입니다. 모든 트랜잭션을 로컬 tooa 특정 데이터베이스 된다는 것 검색이 설정 되어 있습니다.

## <a name="multi-tenant-and-single-tenant"></a>다중 테넌트 및 단일 테넌트
일부 응용 프로그램에서는 각 테 넌 트에 대 한 별도 데이터베이스를 만드는 가장 간단한 방법은 hello를 사용 합니다. 이 hello **단일 테 넌 트 분할 패턴** 격리, 백업/복원 기능 및 hello 테 넌 트의 hello 세분성에서 크기 조정 하는 리소스를 제공 하는 합니다. 단일 테 넌 트 분할 각 데이터베이스 특정 테 넌 트 ID 값 (또는 고객의 키 값), 연결 되지만 키가 필요 하지 hello 데이터 자체에 존재 합니다. 응용 프로그램의 책임 tooroute 각 요청 toohello 적절 한 데이터베이스-hello은 및 hello 클라이언트 라이브러리 간소화할 수 있습니다.

![다중 테넌트 대 단일 테넌트][4]

다른 시나리오에서는 여러 테넌트를 개별 데이터베이스로 격리하지 않고 함께 데이터베이스에 포함합니다. 이것은 일반적인 **다중 테 넌 트 분할 패턴** -및 많은 수의 매우 작은 테 넌 트 응용 프로그램을 관리 하는 hello 팩트에서 구동 될 수 있습니다. 다중 테 넌 트 분할 hello 데이터베이스 테이블의 hello 행 toocarry hello 테 넌 트 ID 또는 분할 키를 식별 하는 키 설계 됩니다. 다시 라우팅 테 넌 트의 요청 toohello 적절 한 데이터베이스에 대 한 hello 응용 프로그램 계층은 고 hello 탄력적 데이터베이스 클라이언트 라이브러리에서 지원할 수 있습니다. 또한 행 수준 보안이 사용 되는 toofilter 각 테 넌 트에 액세스할 수-자세한 내용은 행 참조 수 [탄력적 데이터베이스 도구와 행 수준 보안 다중 테 넌 트 응용 프로그램](sql-database-elastic-tools-multi-tenant-row-level-security.md)합니다. 데이터베이스 간에 데이터를 재배포 hello 다중 테 넌 트 분할 패턴으로 필요 하며 이것은 hello 탄력적 데이터베이스 분할 / 병합 도구를 통해 지원 됩니다. 탄력적 풀을 사용 하 여 SaaS 응용 프로그램에 대 한 디자인 패턴에 대해 자세히 toolearn 참조 [Azure SQL 데이터베이스를 사용한 다중 테 넌 트 SaaS 응용 프로그램에 대 한 디자인 패턴](sql-database-design-patterns-multi-tenancy-saas-applications.md)합니다.

### <a name="move-data-from-multiple-toosingle-tenancy-databases"></a>여러 toosingle 테 넌 트 데이터베이스에서 데이터를 이동 합니다.
SaaS 응용 프로그램을 만들 때 일반적인 toooffer 잠재 고객의 평가판 소프트웨어 hello 합니다. 이 경우,이 비용 효율적인 toouse hello 데이터에 대 한 다중 테 넌 트 데이터베이스입니다. 그러나 잠재 고객이 고객이 되면 단일 테넌트 데이터베이스가 더 나은 성능을 제공하므로 단일 테넌트 데이터베이스가 더 좋습니다. Hello를 사용 하 여 hello 고객 hello 평가 기간 중 데이터 만들, [분할 / 병합 도구](sql-database-elastic-scale-overview-split-and-merge.md) hello 다중 테 넌 트 toohello 새 단일 테 넌 트 데이터베이스에서 toomove hello 데이터입니다.

## <a name="next-steps"></a>다음 단계
Hello 클라이언트 라이브러리를 보여 주는 샘플 응용 프로그램을 참조 하십시오. [탄력적 데이터베이스 도구 시작](sql-database-elastic-scale-get-started.md)합니다.

toouse hello 도구 데이터베이스 tooconvert 기존, 참조 [tooscale 아웃 데이터베이스 마이그레이션 기존](sql-database-elastic-convert-to-use-elastic-tools.md)합니다.

hello 탄력적 풀의 toosee hello 세부 사항 참조 [탄력적 풀의 가격 및 성능 고려 사항은](sql-database-elastic-pool.md), 새 풀을 만들거나 [탄력적 풀](sql-database-elastic-pool-manage-portal.md)합니다.  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-scale-introduction/tools.png
[2]:./media/sql-database-elastic-scale-introduction/h_versus_vert.png
[3]:./media/sql-database-elastic-scale-introduction/overview.png
[4]:./media/sql-database-elastic-scale-introduction/single_v_multi_tenant.png

