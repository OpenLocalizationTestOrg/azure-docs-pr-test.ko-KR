---
title: "확장 클라우드 데이터베이스 aaaManaging | Microsoft Docs"
description: "Hello 탄력적 데이터베이스 작업 서비스를 보여 줍니다."
metakeywords: azure sql database elastic databases
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 6fa47cf2-1162-4534-a206-6e2d95b78580
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: b6d330cd712421b8cba781e835830772e6e5b77e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-scaled-out-cloud-databases"></a>규모가 확장된 클라우드 데이터베이스 관리
toomanage 수평 확장 된 분할 된 데이터베이스 hello **탄력적 데이터베이스 작업** 기능 (미리 보기) 사용 하도록 설정 하면 tooreliably 그룹 포함 하 여 데이터베이스에 대 한 TRANSACT-SQL (T-SQL) 스크립트를 실행 합니다.

* 데이터베이스의 사용자 정의 컬렉션(아래 설명)
* [탄력적 풀](sql-database-elastic-pool.md)의 모든 데이터베이스
* 분할된 데이터베이스 집합( [탄력적 데이터베이스 클라이언트 라이브러리](sql-database-elastic-database-client-library.md)를 사용하여 생성) 

## <a name="documentation"></a>설명서
* [Hello 탄력적 데이터베이스 작업 구성 요소를 설치](sql-database-elastic-jobs-service-installation.md)합니다. 
* [탄력적 데이터베이스 작업을 시작합니다](sql-database-elastic-jobs-getting-started.md).
* [PowerShell을 사용하여 작업을 만들고 관리합니다](sql-database-elastic-jobs-powershell.md).
* [규모가 확장된 Azure SQL 데이터베이스 만들기 및 관리](sql-database-elastic-jobs-getting-started.md)

**탄력적 데이터베이스 작업** hello 임시 및 이라고 하는 예약 된 관리 작업을 실행할 수 있습니다 하는 고객 호스팅되지 Azure 클라우드 서비스는 현재 **작업**합니다. 작업을 쉽게 수 고 안정적으로 Transact SQL 스크립트 tooperform 관리 작업을 실행 하 여 Azure SQL 데이터베이스의 대규모 그룹을 관리 합니다. 

![탄력적 데이터베이스 작업 서비스][1]

## <a name="why-use-jobs"></a>작업을 사용하는 이유
**관리**

스키마 변경, 자격 증명 관리, 참조 데이터 업데이트, 성능 데이터 수집 또는 테넌트(고객) 원격 분석 수집 등을 쉽게 수행할 수 있습니다.

**보고서**

Azure SQL 데이터베이스의 컬렉션에서 단일 대상 테이블로 데이터를 집계합니다.

**오버헤드 줄이기**

일반적으로 tooeach 데이터베이스 순서 toorun Transact SQL 문에 독립적으로 연결 하거나 다른 관리 작업을 수행 해야 합니다. 작업 로깅 tooeach 데이터베이스 hello 대상 그룹에서의 hello 작업을 처리 합니다. 또한 정의 유지 관리 및 Azure SQL 데이터베이스의 그룹에 걸쳐 실행 되는 TRANSACT-SQL 스크립트 toobe 유지 합니다.

**계정 관리**

작업에는 각 데이터베이스에 대 한 실행의 hello 스크립트 및 로그 hello 상태를 실행 됩니다. 또한 오류가 발생할 때 자동으로 재시도하도록 합니다.

**유연성**

Azure SQL 데이터베이스의 사용자 지정 그룹을 정의하고 작업 실행을 위한 일정을 정의합니다.

> [!NOTE]
> Hello Azure 포털, 기능 중 일부만 tooSQL 탄력적인 Azure 제한만 풀을 사용할 수 있습니다. Hello PowerShell Api tooaccess hello 현재 기능의 전체 집합을 사용 합니다.
> 
> 

## <a name="applications"></a>응용 프로그램
* 새 스키마 배포와 같은 관리 작업을 수행합니다.
* 모든 데이터베이스에서 공통적인 제품 정보와 같은 참조 데이터를 업데이트합니다. 평일 근무 외 시간에 자동 업데이트를 예약합니다.
* 인덱스 tooimprove 쿼리 성능 다시 작성 합니다. hello를 다시 작성 될 수 있습니다 tooexecute 구성 된 컬렉션에서 정기적으로 데이터베이스의와 같은 사용량이 적은 시간입니다.
* 지속적으로 데이터베이스 집합에서 중앙 테이블로 쿼리 결과 수집 성능 쿼리 지속적으로 실행 될 수 있으며 tootrigger 추가 작업 toobe 실행을 구성 합니다.
* 다양 한 데이터베이스에서 오래 실행 되는 데이터 처리 쿼리를 실행, 예를 들어 고객 원격 분석의 컬렉션을 hello 합니다. 추가 분석을 위해 결과가 단일 대상 테이블에 수집됩니다.

## <a name="elastic-database-jobs-end-to-end"></a>탄력적 데이터베이스 작업: 종단 간
1. Hello 설치 **탄력적 데이터베이스 작업** 구성 요소입니다. 자세한 내용은 [탄력적 데이터베이스 작업 설치](sql-database-elastic-jobs-service-installation.md)를 참조하세요. Hello 설치가 실패할 경우 참조 [어떻게 toouninstall](sql-database-elastic-jobs-uninstall.md)합니다.
2. 더 많은 기능을 사용자 정의 데이터베이스 컬렉션, 일정을 추가 및/또는 결과 집합을 수집을 만드는 예를 들어 PowerShell Api tooaccess hello를 사용 합니다. 간단한 설치 및 작업의 생성/모니터링에 사용 하 여 hello 포털 제한에 대해 tooexecution는 **탄력적 풀**합니다. 
3. 작업 실행을 위해 암호화 된 자격 증명 만들기 및 [hello 사용자 (또는 역할) tooeach 데이터베이스 hello 그룹에 추가](sql-database-security-overview.md)합니다.
4. idempotent hello 그룹의 모든 데이터베이스에 대해 실행할 수 있는 T-SQL 스크립트를 만듭니다. 
5. Hello Azure 포털을 사용 하 여 이러한 단계 toocreate 작업 수행: [만들고 탄력적 데이터베이스 작업 관리](sql-database-elastic-jobs-create-and-manage.md)합니다. 
6. 또는 PowerShell 스크립트를 사용하여 [PowerShell로 SQL 데이터베이스 탄력적 데이터베이스 작업을 만들고 관리(미리 보기)](sql-database-elastic-jobs-powershell.md)합니다.

## <a name="idempotent-scripts"></a>Idempotent 스크립트
hello 스크립트 여야 [idempotent](https://en.wikipedia.org/wiki/Idempotence)합니다. 간단히 말해서 "idempotent" hello 스크립트 성공 하는 경우 다시 실행 되어 hello 동일한 결과가 발생 함을 의미 합니다. 스크립트는 tootransient 네트워크 문제로 인해 실패할 수 있습니다. 이 경우 hello 작업이 자동으로 다시 hello 스크립트 desisting 하기 전에 미리 설정 된 횟수를 실행 합니다. Idempotent 스크립트 성공적으로 실행 되었으며 두 번 하는 경우에 같은 결과 hello에 있습니다. 

간단한 방법은 tootest 만들기 전에 개체의 존재를 hello에 대 한입니다.  

    IF NOT EXIST (some_object)
    -- Create hello object 
    -- If it exists, drop hello object before recreating it.

마찬가지로, 스크립트 있어야 수 tooexecute 성공적으로 논리적으로 테스트 하 여 하며 찾은 모든 조건을 대처 합니다.

## <a name="failures-and-logs"></a>오류 및 로그
스크립트를 여러 번 시도한 후 실패 하면 hello 작업 hello 오류를 기록 하 고 계속 합니다. 작업 종료 된 후 (hello 그룹의 모든 데이터베이스에 대해 실행 되는 의미) 확인할 수 있습니다 실패 한 시도의 목록. hello 로그 toodebug 결함이 있는 스크립트 세부 정보를 제공합니다. 

## <a name="group-types-and-creation"></a>그룹 유형 및 만들기
두 종류의 그룹이 있습니다. 

1. 분할된 데이터베이스 집합
2. 사용자 지정 그룹

Hello를 사용 하 여 분할 집합 그룹을 만들어 [탄력적 데이터베이스 도구](sql-database-elastic-scale-introduction.md)합니다. 분할 집합 그룹을 만들 때 데이터베이스 추가 또는 hello 그룹에서 자동으로 제거 합니다. 예를 들어 새 분할은 자동으로 그룹에 포함 될 hello toohello 분할 맵을 추가할 때. Hello 그룹에 대해 작업을 실행할 수 있습니다.

사용자 지정 그룹을 다른 손 hello, 엄격 하 게 정의 됩니다. 사용자 지정 그룹에서 데이터베이스를 명시적으로 추가하거나 제거해야 합니다. Hello 그룹에서 데이터베이스를 삭제 하면 hello 작업이 최종 실패로 인해 hello 데이터베이스에 대해 toorun hello 스크립트를 시도 됩니다. 현재 hello Azure 포털을 사용 하 여 만든 그룹은 사용자 지정 그룹. 

## <a name="components-and-pricing"></a>구성 요소 및 가격
hello 다음 구성 요소가 함께 작동 toocreate는 Azure 클라우드 서비스 관리 작업의 임시 실행입니다. hello 구성 요소 설치 되 고 구독에서 설치 하는 동안 자동으로 구성 됩니다. 자동 생성 된 동일한 hello가 모두 대로 hello 서비스를 식별할 수 이름입니다. hello 이름이 고유한 지 고 hello 접두사 "edj" 21 임의로 생성 된 문자로 이어지는 구성 합니다.

* **Azure 클라우드 서비스**: 탄력적 데이터베이스 작업 (미리 보기)은 고객에서 호스팅되는 Azure 클라우드도 제공 hello의 서비스 tooperform 실행 작업을 요청 합니다. Hello 포털에서 hello 서비스는 배포 하 고 Microsoft Azure 구독에서 호스팅됩니다. hello 기본 배포 서비스의 고가용성을 위해 두 작업자 역할 hello 최소한으로 실행 됩니다. 각 작업자 역할 (ElasticDatabaseJobWorker)의 기본 크기는 hello A0 인스턴스에서 실행 합니다. 가격에 대한 내용은 [클라우드 서비스 가격](https://azure.microsoft.com/pricing/details/cloud-services/)을 참조하세요. 
* **Azure SQL 데이터베이스**: hello 서비스 hello 라고 하는 Azure SQL 데이터베이스를 사용 하 여 **제어 데이터베이스** toostore 모든 hello 작업 메타 데이터입니다. hello 기본 서비스 계층에는 s 0입니다. 가격에 대한 내용은 [SQL 데이터베이스 가격](https://azure.microsoft.com/pricing/details/sql-database/)을 참조하세요.
* **Azure 서비스 버스**: hello Azure 클라우드 서비스 내에서 hello 작업을 조정 하기 위해는 Azure 서비스 버스는 합니다. [서비스 버스 가격](https://azure.microsoft.com/pricing/details/service-bus/)을 참조하세요.
* **Azure 저장소**:는 Azure 저장소 계정이 사용 toostore 진단 출력에서 추가 디버깅 취해야 하는 문제가 hello 이벤트 로깅 (참조 [Azure 클라우드 서비스 및 가상 컴퓨터에서 진단 사용](../cloud-services/cloud-services-dotnet-diagnostics.md)). 가격에 대한 내용은 [Azure 저장소 가격](https://azure.microsoft.com/pricing/details/storage/)을 참조하세요.

## <a name="how-elastic-database-jobs-work"></a>탄력적 데이터베이스 작업의 작동 방식
1. Azure SQL 데이터베이스는 모든 메타데이터 및 상태 데이터를 저장하는 **제어 데이터베이스** 로 지정됩니다.
2. hello hello 제어 데이터베이스에 액세스 **작업 서비스** toolaunch 및 추적 작업 tooexecute 합니다.
3. 두 가지 역할 hello 제어 데이터베이스와 통신합니다. 
   * 컨트롤러: 작업을 수행 하는 새 작업을 만들어 작업과 실패 한 작업을 다시 시도 요청 하는 작업 tooperform hello 필요 여부를 확인 합니다.
   * 작업 작업 실행: hello 수행 하는 작업을 수행합니다.

### <a name="job-task-types"></a>작업 태스크 유형
작업을 실행하는 여러 유형의 작업 태스크가 있습니다.

* ShardMapRefresh: 쿼리 hello 분할 맵 toodetermine 분할 된 데이터베이스로 모든 hello 데이터베이스 사용
* ScriptSplit: hello 스크립트에 대해 '이동 문을 일괄 처리로 균등 분산
* ExpandJob: 데이터베이스 그룹을 대상으로 하는 작업에서 각 데이터베이스에 대한 자식 작업을 만듭니다.
* ScriptExecution: 정의된 자격 증명을 사용하여 특정 데이터베이스에 대해 스크립트를 실행합니다.
* Dacpac: 특정 자격 증명을 사용 하 여 DACPAC tooa 특정 데이터베이스를 적용 됩니다.

## <a name="end-to-end-job-execution-work-flow"></a>종단 간 작업 실행 워크플로
1. Hello 포털 또는 PowerShell API hello를 사용 하 여, 작업 삽입 된 hello **제어 데이터베이스**합니다. hello 작업 그룹 특정 자격 증명을 사용 하 여 데이터베이스에 대해 TRANSACT-SQL 스크립트의 실행을 요청 합니다.
2. hello 컨트롤러 hello 새 작업을 식별합니다. 작업 실행 태스크가 실행 된 toosplit hello 스크립트 및 toorefresh hello 그룹의 데이터베이스 및 만들어집니다. 마지막으로, 새 작업 및 tooexpand hello 작업 실행 만들어지고 새 자식 여기서 각 자식 작업은 지정 된 tooexecute hello hello 그룹에서 개별 데이터베이스에 대 한 TRANSACT-SQL 스크립트 작업을 만듭니다.
3. hello 컨트롤러 hello 만든 자식 작업을 식별 합니다. 각 작업에 대 한 hello 컨트롤러 만들고 데이터베이스에 대해 작업 tooexecute hello 스크립트 작업을 트리거합니다. 
4. 모든 작업 실행 태스크가 완료 된 후 hello 컨트롤러 hello 작업 tooa 완료 상태를 업데이트 합니다. 
   작업 실행 중 언제 든 hello PowerShell API 사용된 tooview 수 hello 작업 실행의 현재 상태입니다. 모든 시간은 반환 hello PowerShell Api utc로 표시 됩니다. 원하는 경우 취소 요청이 시작 된 toostop 작업 될 수 있습니다. 

## <a name="next-steps"></a>다음 단계
[Hello 구성 요소를 설치](sql-database-elastic-jobs-service-installation.md), 다음 [만들고 tooeach hello 그룹 데이터베이스의 데이터베이스에 로그를 추가](sql-database-manage-logins.md)합니다. toofurther 작업 만들기 및 관리를 이해, 참조 [만들고 탄력적 데이터베이스 작업을 관리](sql-database-elastic-jobs-create-and-manage.md)합니다. [탄력적 데이터베이스 작업 시작](sql-database-elastic-jobs-getting-started.md)도 참조하세요.

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-overview/elastic-jobs.png
<!--anchors-->


