---
title: "확장 클라우드 데이터베이스 간에 데이터 aaaMoving | Microsoft Docs"
description: "Toomanipulate 조각 및 확대/축소를 사용 하 여 자체 호스팅된 서비스를 통해 이동 데이터가 데이터베이스 Api에 설명 합니다."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 204fd902-0397-4185-985a-dea3ed7c7d9f
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 629dee06e22609e9b61edf93ba5c38d997132d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="moving-data-between-scaled-out-cloud-databases"></a>확장된 클라우드 데이터베이스 간 데이터 이동
서비스 개발자는 소프트웨어 응용 프로그램의 엄청난 요청에서 갑자기 경우 tooaccommodate hello 증가 해야 합니다. 따라서 더 많은 데이터베이스(분할 된 데이터베이스)를 추가합니다. Hello 데이터 무결성을 방해 하지 않고 hello 데이터 toohello 새 데이터베이스를 어떻게 재배포할 수 있습니다. 사용 하 여 hello **분할 / 병합 도구** toohello 새 데이터베이스를 데이터베이스 toomove 데이터를 제한 합니다.  

hello 분할 / 병합 도구는 Azure 웹 서비스로 실행 됩니다. 관리자 또는 개발자는 서로 다른 데이터베이스 (분할) 간에 hello 도구 toomove shardlet (분할 영역에서 데이터)를 사용합니다. hello 도구 분할 맵 관리 toomaintain hello 서비스 메타 데이터 데이터베이스를 사용 하 고 일관 된 매핑을 확인 합니다.

![개요][1]

## <a name="download"></a>다운로드
[Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/)

## <a name="documentation"></a>설명서
1. [탄력적 데이터베이스 분할/병합 도구 자습서](sql-database-elastic-scale-configure-deploy-split-and-merge.md)
2. [분할-병합 보안 구성](sql-database-elastic-scale-split-merge-security-configuration.md)
3. [분할-병합 보안 고려 사항](sql-database-elastic-scale-split-merge-security-configuration.md)
4. [분할된 데이터베이스 맵 관리](sql-database-elastic-scale-shard-map-management.md)
5. [기존 데이터베이스 tooscale 아웃 마이그레이션](sql-database-elastic-convert-to-use-elastic-tools.md)
6. [탄력적 데이터베이스 도구](sql-database-elastic-scale-introduction.md)
7. [탄력적 데이터베이스 도구 용어집](sql-database-elastic-scale-glossary.md)

## <a name="why-use-hello-split-merge-tool"></a>Hello 분할 / 병합 도구를 사용 하는 이유는?
**유연성**

응용 프로그램에는 단일 Azure SQL DB 데이터베이스의 hello도 넘어 유연 하 게 toostretch가 필요 합니다. 필요한 toonew 데이터베이스 무결성을 유지 하면서 hello 도구 toomove 데이터를 사용 합니다.

**Toogrow 분합니다** 

전반적인 tooincrease 필요한 용량 toohandle 폭발적 증가 합니다. 따라서 toodo 분할 hello 데이터 및 용량 요구 사항 충족 되는지 될 때까지 점차적으로 더 많은 데이터베이스에 걸쳐 분산 하 여 추가 용량을 만듭니다. Hello 'split' 기능의 전형입니다. 

**Tooshrink 병합**

비즈니스의 toohello 계절별 특성 인해 용량 축소 필요 합니다. hello 도구를 통해 비즈니스의 속도도 느려집니다 때 toofewer 배율 단위를 축소 합니다. hello Elastic Scale 분할 / 병합 서비스에서에서 hello '병합' 기능에는이 요구 사항을 다룹니다. 

**shardlet 이동으로 핫스팟 관리**

데이터베이스 마다 여러 테 넌 트에서 shardlet tooshards의 hello 할당 일부 분할 영역에 toocapacity 병목 현상이 발생할 수 있습니다. 이렇게 하려면 다시 shardlet을 할당 하거나 사용 중인 shardlet toonew 또는 덜 사용 됨된 분할 영역을 이동 합니다. 

## <a name="concepts--key-features"></a>개념 및 주요 기능
**고객 호스트 서비스**

hello 분할 / 병합을 고객 호스팅 서비스로 배달 됩니다. 배포 하 고 Microsoft Azure 구독에 hello 서비스를 호스트 해야 합니다. NuGet에서 다운로드 하는 hello 패키지에는 특정 배포에 대 한 hello 정보로 구성 템플릿 toocomplete 포함 되어 있습니다. Hello 참조 [분할 / 병합 자습서](sql-database-elastic-scale-configure-deploy-split-and-merge.md) 대 한 자세한 내용은 합니다. Hello 서비스가 Azure 구독에서 실행 되는 이후 제어 하 고 hello 서비스의 대부분 보안 측면을 구성할 수 있습니다. hello 옵션 tooconfigure SSL, 인증서 기반 클라이언트 인증, 저장 된 자격 증명, DoS 보호 및 IP 제한에 대 한 암호화 hello 기본 서식 파일에 포함 되어 있습니다. Hello 문서 뒤에서 hello에 대 한 자세한 내용은 보안 측면을 찾을 수 있습니다 [분할 / 병합 보안 구성](sql-database-elastic-scale-split-merge-security-configuration.md)합니다.

hello 기본 배포 하나의 작업자와 단일 웹 역할 서비스를 실행 합니다. 각각 hello A1 v M 크기를 사용 하 여 Azure 클라우드 서비스에서입니다. Hello 패키지를 배포할 때 이러한 설정을 수정할 수는 없지만, (Azure 포털 hello)를 통해 클라우드 서비스를 실행 하는 hello에 배포 된 후 변경할 수 있습니다. 해당 hello 작업자 역할 구성 하지 않아야 단일 인스턴스 보다 기술적인 이유로 note 합니다. 

**분할된 데이터베이스 맵 통합**

hello 분할 / 병합 서비스는 hello 분할 맵을 hello 응용 프로그램의 상호 작용합니다. 분할 영역 간에 분할 / 병합 서비스 toosplit hello 또는 병합 범위 또는 toomove shardlet을 사용 하는 경우 hello 서비스 hello 분할 맵은 toodate 자동으로 유지 합니다. toodo hello 서비스 hello 응용 프로그램의 toohello shard map manager 데이터베이스를 연결 하 고 진행 상황을 분할/병합/이동 요청 범위 및 매핑을 유지 관리 하는 등입니다. 이렇게 하면 해당 hello 분할 맵을 표시 합니다. 항상 최신 보기 분할 / 병합 작업이 진행 되는 경우. 분할 범위 병합 및 shardlet 이동 작업 hello 원본 shard toohello 대상 분할 영역에서 shardlet의 일괄 처리를 이동 하 여 구현 됩니다. Hello shardlet 이동 작업 hello shardlet 주체 toohello 현재 일괄 처리 하는 동안 표시 된 hello 분할 맵을 오프 라인으로 및 hello를 사용 하 여 데이터 종속 라우팅 연결에 사용할 수 없는 **OpenConnectionForKey** API입니다. 

**일관된 Shardlet 연결 수**

Shardlet의 새 일괄 처리에 대 한 데이터 이동 시작 되 면 모든 제공 된 분할 맵을 데이터 종속 라우팅 연결 toohello 분할 저장 hello shardlet 연결이 중지 되 고 후속 hello 분할 맵에서 Api toohello이 shardlet이 차단 되는 동안 hello 데이터 이동 순서 tooavoid 불일치가 진행 중입니다. 동일한 분할 영역에는 또한 가져오기 중단 되지만 다시 성공 hello에 tooother shardlet 연결 다시 시도에 즉시 합니다. Hello 일괄 처리를 이동 hello shardlet은 hello 대상 분할 영역에 대 한 다시 온라인으로 표시 하 고 hello 원본 데이터 hello 원본 분할 영역에서 제거 됩니다. hello 서비스는 모든 shardlet 이동 될 때까지 모든 일괄 처리에 대해 다음이 단계를 거칩니다. 분할/병합/이동 작업을 완료 하는 hello hello 과정 tooseveral 연결 kill 작업 일으킵니다.  

**Shardlet 가용성 관리**

위에서 설명한 것 처럼 shardlet의 toohello 현재 일괄 처리를 종료 하는 hello 연결을 제한 한 번에 shardlet의 사용 불가 tooone 일괄 처리의 hello 범위를 제한 합니다. 이것이 기본 접근 방식을 통해 여기서 hello 완료 분할 된 데이터베이스는 오프 라인으로 유지 모든 shardlet에 대 한 hello 진행 되는 분할 또는 병합 작업 동안입니다. 한 번에 고유한 shardlet toomove hello 수로 정의 되는 일괄 처리의 hello 크기에는 구성 매개 변수입니다. Hello 응용 프로그램의 가용성 및 성능 요구에 따라 각 분할 및 병합 작업에 대해 정의할 수 있습니다. Hello shard map의 잠금 중인 hello 범위 지정 된 hello 일괄 처리 크기 보다 클 수 있습니다는 참고 사항 즉, hello 서비스 hello 실제 hello 데이터에서 분할 키 값 수에는 약 hello 일괄 처리 크기와 일치 되도록 hello 범위 크기를 선택 합니다. 이 중요 한 tooremember 특히 근거가 분할 키입니다. 

**메타데이터 저장소**

hello 분할 / 병합 서비스 요청을 처리 하는 동안 로그의 상태와 tookeep 데이터베이스 toomaintain를 사용 합니다. hello 사용자 자신의 구독에이 데이터베이스를 만듭니다 고 hello 서비스 배포에 대 한 hello 구성 파일에서 연결 문자열 hello 제공 합니다. Hello 사용자의 조직에서 관리자 toothis 연결할 수 있으며 데이터베이스 tooreview 요청 진행 상황과 tooinvestigate 발생할 수 있는 오류에 대 한 정보를 자세히 설명 합니다.

**분할 인식**

hello 분할 / 병합 서비스 (1) 분할 된 테이블, (2) 참조 테이블 및 (3) 일반 테이블을 구분합니다. 분할/병합/이동 작업의 hello 의미 체계 hello 유형의 hello 테이블 사용에 따라 다르며 다음과 같이 정의 됩니다. 

* **분할 된 테이블**: 분할, 병합 및 이동 작업 소스 tootarget 분할 된 데이터베이스에서 shardlet을 이동 합니다. Hello 성공적으로 완료 한 후 전체 요청을 해당 shardlet hello 원본에 존재 하지 않는 합니다. 참고 hello 대상 테이블 tooexist hello 대상 분할 영역에 필요 하 고 hello 대상 범위 hello 작업의 이전 tooprocessing의 데이터를 포함 해야 합니다. 
* **테이블 참조**: hello 분할 참조 테이블, 병합 및 hello 원본 toohello 대상 분할 영역에서 hello 데이터를 복사 하는 작업을 이동 합니다. 그러나 Note, 변경 없이 지정된 된 테이블에 대 한 hello 대상 분할 영역에 행 hello 대상에서이 테이블에 이미 있으면 발생 합니다. hello 테이블에 toobe 처리 된 모든 참조 테이블 복사본 작업 tooget에 대해 비어 있습니다.
* **다른 테이블**: hello 원본 또는 분할 및 병합 작업의 hello 대상에 있는 다른 테이블 있을 수 있습니다. hello 분할 / 병합 서비스는 모든 데이터를 이동 또는 복사 작업에 이러한 테이블을 무시합니다. 단, 제약 조건이 있는 경우에는 이와 같은 작업이 정상적으로 수행되지 않을 수 있습니다.

hello에 분할 된 테이블 및 참조 정보 hello **SchemaInfo** hello 분할 맵에 Api입니다. 다음 예제는 hello 이러한 Api에 주어진된 shard map manager 개체 smm hello 사용을 보여 줍니다. 

    // Create hello schema annotations 
    SchemaInfo schemaInfo = new SchemaInfo(); 

    // Reference tables 
    schemaInfo.Add(new ReferenceTableInfo("dbo", "region")); 
    schemaInfo.Add(new ReferenceTableInfo("dbo", "nation")); 

    // Sharded tables 
    schemaInfo.Add(new ShardedTableInfo("dbo", "customer", "C_CUSTKEY")); 
    schemaInfo.Add(new ShardedTableInfo("dbo", "orders", "O_CUSTKEY")); 

    // Publish 
    smm.GetSchemaInfoCollection().Add(Configuration.ShardMapName, schemaInfo); 

지역' hello 테이블' 및 '사막이 남 지역' 참조 테이블으로 정의 되 고 분할/병합/이동 작업에 복사 됩니다. 그런 다음 'customer' 및 'orders'는 분할된 테이블로 정의됩니다. C_CUSTKEY 및 O_CUSTKEY hello 분할 키로 사용 합니다. 

**참조 무결성**

hello 분할 / 병합 서비스 테이블 간의 종속성을 분석 하 고 참조 테이블 및 shardlet을 이동 하는 것에 대 한 외래 키 기본 키 관계 toostage hello 작업을 사용 합니다. 일반적으로 참조 테이블이 종속성 순서에 따라 먼저 복사된 다음 shardlet이 각 배치 내에서 해당 종속성의 순서에 따라 복사됩니다. 이 소프트웨어는 hello 새로운 데이터 유입 대로 hello 대상 분할 영역에 PK 외래 키 제약 조건을 적용를 필요 합니다. 

**분할된 데이터베이스 맵 일관성 및 최종 완료**

오류의 hello 상태에서 hello 분할 / 병합 서비스는 모든 중단 후 작업을 다시 시작 하 고 진행 중인 요청에 아무 toocomplete 목표로 합니다. 그러나 있을 수 있습니다 복구할 수 없는 경우, 예: hello 대상 분할 된 데이터베이스를 분실 하거나 복구할 수 없을 정도로 손상 될 경우. 이러한 상황에서 toobe 이동 었어야 일부 shardlet hello 원본 분할 영역을 tooreside를 계속할 수 있습니다. hello 서비스는 hello 필요한 데이터를 성공적으로 복사한 toohello 대상 된 후 shardlet 매핑만 업데이트 되도록 합니다. Shardlet은 toohello 대상 된 해당 데이터를 모두 복사 하 고 hello 해당 매핑을 업데이트 되었습니다에 hello 소스에서 삭제 됩니다. hello 삭제 작업 동안 hello 범위는 hello 대상 분할 영역에 이미 온라인 hello 백그라운드에서 발생 합니다. hello 분할 / 병합 서비스는 항상 hello shard map에 저장 된 hello 매핑의 정확성을 보장 합니다.

## <a name="hello-split-merge-user-interface"></a>hello 분할 / 병합 사용자 인터페이스
웹 역할과 작업자 역할 hello 분할 / 병합 서비스 패키지에 포함 되어 있습니다. hello 웹 역할에서 대화식으로 사용 되는 toosubmit 분할 / 병합 요청은입니다. hello hello 사용자 인터페이스의 주요 구성 요소는 다음과 같습니다.

* 작업 유형: hello 작업 유형에이 요청에 대 한 hello 서비스에서 수행 하는 작업의 hello 종류를 제어 하는 라디오 단추입니다. Hello 분할 중에서 선택할 병합 한 시나리오를 이동할 수 있습니다. 이전에 제출된 작업을 취소할 수도 있습니다. 범위 분할된 데이터베이스 맵에 분할, 병합 및 이동 요청을 사용할 수 있습니다. 목록 분할된 데이터베이스 맵은 이동 작업만 지원합니다.
* 분할 맵은: hello 분할 맵 및 hello 데이터베이스 분할 맵을 호스팅에 대 한 요청 매개 변수 커버 정보의 다음 섹션을 hello 합니다. 특히 hello Azure SQL 데이터베이스 서버 및 데이터베이스 호스팅 hello shardmap tooprovide hello 이름이 필요, 자격 증명 tooconnect toohello 분할 데이터베이스 매핑한 마지막으로 hello 분할 맵의 이름을 hello 합니다. 현재 hello 작업이 하나의 자격 증명 집합만을 허용합니다. 이러한 자격 증명 toohave 충분 한 권한이 필요 tooperform toohello 분할 맵을 한 hello 분할 영역에 toohello 사용자 데이터를 변경 합니다.
* Source Range (split and merge): 분할 및 병합 작업은 해당 하위 키 및 상위 키를 사용하여 범위를 처리합니다. toospecify unbounded 높은 키 값이 인 검사 작업 확인란 "높은 키가 max" hello 및 hello 높은 키 필드를 비워 두십시오. 매핑과 shard map의 경계 필요 tooprecisely 일치 하지 않을 하는 사용자가 지정한 hello 범위 키 값입니다. 모든 범위 경계를 전혀 지정 하지 않으면 hello 서비스는 자동으로 hello 가장 가까운 범위를 유추할 합니다. 에 지정 된 분할 맵을 hello GetMappings.ps1 PowerShell 스크립트 tooretrieve hello 현재 매핑을 사용할 수 있습니다.
* 분할 소스 동작 (나누기): 분할 작업에 대 한 hello 지점 toosplit hello 소스 범위를 정의 합니다. 저장할 hello 분할 toooccur hello 분할 키를 제공 하 여이 작업을 수행 합니다. Hello 라디오 단추를 사용 하 여 hello 위쪽 toomove (hello 분할 키 포함)를 변경할지 아니면 hello 범위 (제외 키 분할 hello) toomove의 아래 부분 hello 것인지 지정 합니다.
* Shardlet 이동 (이동)을 원본: 이동 작업은 다른 분할 또는 병합 작업으로 범위 toodescribe hello 소스 필요 하지 않습니다. 이동에 대 한 소스는 hello 분할 키 값으로 식별 단순히 toomove을 계획 해야 합니다.
* 분할 된 데이터베이스 (분할) 대상으로: hello 데이터 toobe tooby 제공 hello Azure SQL Db 서버 및 데이터베이스 이름을 hello 대상에 대 한 복사 하려는 toodefine split 작업의 hello 원본 hello 정보를 제공한 후 필요 합니다.
* 대상 범위 (병합): 병합 작업 shardlet tooan 기존 분할 영역을 이동 합니다. Hello 기존 범위와 toomerge 원하는의 hello 범위 경계를 제공 하 여 hello 기존 분할 영역을 식별 합니다.
* 일괄 처리 크기: hello 일괄 처리 크기 컨트롤이 hello hello 데이터 이동 하는 동안 한 번에 오프 라인으로 전송 되는 shardlet 수가 있습니다. 중요 한 toolong shardlet의 작동 중단 기간 때 더 작은 값을 사용할 수 있는 정수 값입니다. 값이 클수록 hello 시간을 지정된 된 shardlet을 증가 합니다 오프 라인 상태 이지만 성능이 향상 될 수 있습니다.
* 작업 Id (취소): 진행 중인 작업은 더 이상 필요 하지를 설정한 경우이 필드에서 해당 작업 ID를 제공 하 여 hello 작업을 취소할 수 없습니다. Hello 요청 상태 테이블에서 hello 작업 ID를 검색할 수 있습니다 (8.1 섹션 참조) 또는 hello 요청을 보내는 위치 hello 웹 브라우저에서 hello 출력 합니다.

## <a name="requirements-and-limitations"></a>요구 사항 및 제한 사항
hello 분할 / 병합 서비스의 현재 구현 hello 주체 toohello는 다음 요구 사항 및 제한 사항: 

* hello 분할 된 데이터베이스 tooexist 필요 하 고 이러한 분할 된이 데이터베이스에서 분할 / 병합 작업을 수행 하려면 먼저 hello 분할 맵은에 등록 되어야 합니다. 
* 테이블 또는 해당 작업의 일부로 자동으로 다른 데이터베이스 개체에 hello 서비스 만들지 않습니다. 이 즉, 모든 분할 된 테이블에 대 한 스키마를 hello 및 참조 테이블 tooexist hello 대상 분할 이전 tooany 분할/병합/이동 작업에 필요 합니다. 분할 된 테이블에는 특히 hello 범위에서 새 shardlet toobe 분할/병합/이동 작업에 의해 추가 된 빈 필요한 toobe은 합니다. 그렇지 않으면 hello 작업이 hello 대상 분할 영역에 대해 hello 초기 일관성 확인을 실패 합니다. 또한 참고 hello 참조 테이블이 비어 있는 경우 참조 데이터 복사만 되 고 없는 일관성 없는 관계 tooother 동시 쓰기 작업 hello 참조 테이블에서 보장 합니다. 이 제품을 추천: 분할/병합 작업을 실행할 때 다른 쓰기 작업이 없습니다 변경할 toohello 참조 테이블입니다.
* hello 서비스는 hello 분할 키 tooimprove 성능 및 대규모 shardlet에 대 한 안정성을 포함 하는 키 또는 고유 인덱스에 의해 설정 된 행 id를 사용 합니다. 이렇게 하면 방금 hello 분할 키 값 보다 훨씬 더 세밀 한 세분성에서 hello 서비스 toomove 데이터입니다. 이렇게 하면 tooreduce hello 최대한의 로그 공간 및 잠금 hello 작업 중 필요한에 있습니다. 분할/병합/이동 요청이 포함 된 고유 인덱스 또는 기본 키를 포함 하 여 지정된 된 테이블에서 분할 키 hello toouse 해당 테이블을 만드는 것이 좋습니다. 성능상의 이유로 hello 키 또는 hello 인덱스의 선행 열 hello hello 분할 키가 있어야 합니다.
* 요청 처리의 hello 동안 일부 shardlet 데이터는 모두 hello 원본과 hello 대상 분할 영역에 존재할 수 있습니다. 오류에 대 한 필요한 tooprotect hello shardlet 이동입니다. hello hello 분할 맵 사용 하 여 분할 / 병합의 통합을 사용 하면는 hello 데이터 종속 라우팅 Api를 사용 하 여를 통한 연결 hello **OpenConnectionForKey** hello 분할 맵의 메서드에서 일치 하지 않는 중간 상태에 나타나지 않습니다. 그러나 때 연결 toohello 소스 또는 hello 대상 분할 영역 hello를 사용 하지 않고 **OpenConnectionForKey** 메서드를 분할/병합/이동 요청은 진행 하는 경우 일치 하지 않는 중간 상태 표시 될 수 있습니다. 이러한 연결은 hello 타이밍 또는 hello 분할 기본 hello 연결에 따라 중복 또는 부분 결과 표시할 수 있습니다. 현재이 제한을 Elastic Scale 다중-Shard-쿼리에 의해 수행 하는 hello 연결을 포함 합니다.
* hello 분할 / 병합 서비스에 대 한 hello 메타 데이터 데이터베이스를 다른 역할 간에 공유 되어야 합니다. 예를 들어 준비 hello 프로덕션 역할 보다 요구 toopoint tooa 다른 메타 데이터 데이터베이스에서 실행 되는 hello 분할 / 병합 서비스의 역할입니다.

## <a name="billing"></a>결제
hello 분할 / 병합 서비스는 Microsoft Azure 구독에서 클라우드 서비스로 실행 됩니다. 따라서 클라우드 서비스에 대 한 청구가 hello 서비스의 tooyour 인스턴스에 적용 됩니다. 분할/병합/이동 작업을 자주 수행하지 않는 한 분할/병합 클라우드 서비스를 삭제하는 것이 좋습니다. 그렇게 하면 실행 중이거나 배포된 클라우드 서비스 인스턴스의 비용이 절감됩니다. 다시 배포 하 고 tooperform 필요할 때마다 즉시 실행 가능한 구성을 시작할 수 있습니다 분할 또는 병합 작업 합니다. 

## <a name="monitoring"></a>모니터링
### <a name="status-tables"></a>상태 테이블
hello 분할 / 병합 서비스 제공 hello **RequestStatus** 완료 된 작업과 진행 중인 요청을 모니터링 하기 위한 hello 메타 데이터 저장소 데이터베이스의 테이블입니다. hello 표에서 hello 분할 / 병합 서비스에 제출 된 toothis 인스턴스의 된 각 분할 / 병합 요청에 대 한 행을 보여 줍니다. Hello 다음 각 요청에 대 한 정보를 제공 합니다.

* **타임 스탬프**: hello hello 요청이 시작 되었을 때 날짜와 시간입니다.
* **OperationId**: hello 요청을 고유 하 게 식별 하는 GUID입니다. 여전히 진행 중인 동안이 요청에 사용 되는 toocancel hello 작업이 될 수도 있습니다.
* **상태**: hello hello 요청의 현재 상태입니다. 진행 중인 요청에 대 한 또한 나열 hello는 hello 요청은 현재 단계입니다.
* **CancelRequest**: hello 요청이 취소 되었는지 여부를 나타내는 플래그입니다.
* **진행률**: hello 작업에 대 한 백분율 예상 합니다. 값이 50 hello 작업이 약 50% 완료 되었음을 나타냅니다.
* **세부 정보**: 더 자세한 진행률 보고서를 제공하는 XML 값입니다. 행 집합이 소스 tootarget에서 복사 된 hello 진행률 보고서 주기적으로 업데이트 됩니다. 이 열에는 오류 또는 예외 발생 시 hello 실패에 대 한 자세한 내용은 포함 됩니다.

### <a name="azure-diagnostics"></a>Azure 진단
hello 분할 / 병합 서비스 모니터링 및 진단에 대 한 Azure SDK 2.5에 따라 Azure 진단을 사용 합니다. 여기에서 설명한 대로 hello 진단 구성 제어: [Azure 클라우드 서비스 및 가상 컴퓨터에서 진단 사용](../cloud-services/cloud-services-dotnet-diagnostics.md)합니다. hello 다운로드 패키지에 두 개의 진단 구성-hello 웹 역할 및 작업자 역할 hello에 대 한 하나 있습니다. Hello 서비스에 대 한 이러한 진단 구성에서 hello 지침에 따라 [Microsoft Azure에서 클라우드 서비스 기본 사항](https://code.msdn.microsoft.com/windowsazure/Cloud-Service-Fundamentals-4ca72649)합니다. Hello 정의 toolog 성능 카운터, IIS 로그, Windows 이벤트 로그 및 분할 / 병합 응용 프로그램 이벤트 로그를 포함합니다. 

## <a name="deploy-diagnostics"></a>진단 배포 
tooenable 모니터링 및 진단 정보를 사용 하 여 hello NuGet 패키지를 hello 다음 Azure PowerShell을 사용 하 여 명령을 실행 하 여 제공 된 hello 웹 및 작업자 역할에 대 한 진단 구성을 hello: 

    $storage_name = "<YourAzureStorageAccount>" 

    $key = "<YourAzureStorageAccountKey" 

    $storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key  


    $config_path = "<YourFilePath>\SplitMergeWebContent.diagnostics.xml" 

    $service_name = "<YourCloudServiceName>" 

    Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Production -Role "SplitMergeWeb" 


    $config_path = "<YourFilePath>\SplitMergeWorkerContent.diagnostics.xml" 

    $service_name = "<YourCloudServiceName>" 

    Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Production -Role "SplitMergeWorker" 

방법에 자세한 정보를 찾을 수 tooconfigure 여기에서 진단 설정을 배포 하 고: [Azure 클라우드 서비스 및 가상 컴퓨터에서 진단 사용](../cloud-services/cloud-services-dotnet-diagnostics.md)합니다. 

## <a name="retrieve-diagnostics"></a>진단 검색
Hello hello 서버 탐색기 트리의 Azure 부분에에서 hello Visual Studio 서버 탐색기에서에서 진단 프로그램을 쉽게 액세스할 수 있습니다. Visual Studio 인스턴스를 열고 hello 메뉴 모음에서 서버 탐색기 및 보기를 클릭 합니다. Hello Azure 아이콘 tooconnect tooyour Azure 구독을 클릭 합니다. 다음 탐색 tooAzure 저장소->-> <your storage account> -> 테이블 WADLogsTable-> 합니다. 자세한 내용은 [서버 탐색기로 저장소 리소스 찾아보기](http://msdn.microsoft.com/library/azure/ff683677.aspx)를 참조하세요. 

![WADLogsTable][2]

위의 hello 그림에 강조 표시 하는 WADLogsTable hello hello가 포함 되어 hello 분할 / 병합 서비스의 응용 프로그램 로그에서 이벤트를 자세히 설명 합니다. 참고 hello 다운로드의 hello 기본 구성은 해당 패키지는 프로덕션 배포도 소개 합니다. 따라서 hello 간격을 로그 및 카운터에서에서 끌어 오지 않습니다 hello 서비스 인스턴스는 큰 (5 분)입니다. 테스트 및 개발에 대 한 hello 웹 또는 작업자 역할 tooyour hello hello 진단 설정을 조정 하 여 낮은 hello 간격 필요 합니다. Hello 역할 hello Visual Studio 서버 탐색기 (위 참조)에 단추로 클릭 하 고 hello 진단 구성 설정에 대 한 hello 대화 상자에서 hello 전송 기간을 조정 합니다. 

![구성][3]

## <a name="performance"></a>성능
일반적으로 더 나은 성능을 toobe Azure SQL 데이터베이스에서 더 많은 성능이 서비스 계층, 더 높은 hello에서 예상 되는 합니다. Hello 더 높은 서비스 계층에 대 한 높은 IO, CPU 및 메모리 할당 hello 대량 복사를 활용 하 고 hello 분할 / 병합 서비스에 사용 하는 작업을 삭제 합니다. 이런 이유로 시간이 정의 되 고 제한 된 기간에 대 한 해당 데이터베이스에 대 한 hello 서비스 계층을 늘립니다.

또한 hello 서비스의 정상 작업의 일환으로 유효성 검사 쿼리를 수행합니다. 이러한 유효성 검사 쿼리에 예기치 않은 데이터 hello 대상 범위에 있는지 확인 하 고 일관 된 상태에서 모든 분할/병합/이동 작업 시작 됨을 확인 하십시오. 이러한 쿼리 모든 hello 작업과 hello 요청 정의의 일부로 제공 된 hello 일괄 처리 크기의 hello 범위에 의해 정의 된 분할 키 범위를 통해서도 있습니다. 이러한 쿼리 인덱스는 hello 선행 열 처럼 hello 분할 키가 있는 경우 최상의 성능을 발휘할 합니다. 

또한 hello 선행 열으로 hello 분할 키를 사용 하 여 고유성 속성 hello 서비스 toouse 로그 공간 및 메모리 관련 리소스 소비량을 제한 하는 최적화 된 방법을 허용 됩니다. 고유성 속성 (일반적으로 1GB) 위 필요한 toomove 큰 데이터 크기입니다. 

## <a name="how-tooupgrade"></a>어떻게 tooupgrade
1. Hello 단계에 따라 [분할 / 병합 서비스 배포](sql-database-elastic-scale-configure-deploy-split-and-merge.md)합니다.
2. 클라우드 서비스 구성 파일에 대 한 분할 / 병합 배포 tooreflect hello 새 구성 매개 변수를 변경 합니다. 새 필수 매개 변수는 암호화에 사용 되는 hello 인증서에 대 한 hello 정보입니다. 쉽게 toodo toocompare hello 새 구성 템플릿 파일에서 기존 구성에 대 한 hello 다운로드입니다. hello 웹 및 작업자 역할 hello에 대 한 "DataEncryptionPrimaryCertificateThumbprint" 및 "DataEncryptionPrimary"에 대 한 hello 설정을 추가 해야 합니다.
3. Hello 업데이트 tooAzure를 배포 하기 전에 모든 분할 / 병합 현재 실행 중인 작업이 완료 될를 확인 합니다. 진행 중인 요청에 대 한 hello 분할 / 병합 메타 데이터 데이터베이스의 hello RequestStatus 및 PendingWorkflows 테이블을 쿼리하여 쉽게 수행할 수 있습니다.
4. 분할 / 병합 hello 새 패키지로 Azure 구독 및 업데이트 된 서비스 구성 파일에 대 한 기존 클라우드 서비스 배포를 업데이트 합니다.

분할 / 병합 tooupgrade에 대 한 새 메타 데이터 데이터베이스 tooprovision이 필요가 없습니다. hello 새 버전에는 기존 메타 데이터 데이터베이스 toohello 새 버전 자동 업그레이드 됩니다. 

## <a name="best-practices--troubleshooting"></a>모범 사례, 문제 해결:
* 테스트 테 넌 트를 정의 하 고 여러 분할 영역 간에 hello 테스트 테 넌 트와 가장 중요 한 분할/병합/이동 작업을 실행 합니다. 모든 메타 데이터 분할 맵을에 올바르게 정의 되어 있으며 hello 작업 제약 조건 또는 외래 키 위반 하지 않는지 확인 합니다.
* 유지 hello 테스트 테 넌 트 데이터 크기가 데이터 크기 발생 하지 않는지 tooensure 관련 문제를 가장 큰 테 넌 트의 hello 최대 데이터 크기를 초과 합니다. Hello 시간이 toomove 주위 단일 테 넌 트에 상한 값을 비교할 수 있습니다. 
* 스키마 삭제를 허용 하는지 확인합니다. hello 분할 / 병합 서비스는 hello 데이터 복사 성공 toohello 대상 되 면 hello 기능 tooremove 데이터 원본 shard hello에서 필요 합니다. 예를 들어 **delete 트리거를** hello 서비스 hello 소스에 hello 데이터를 삭제 하지 못할 수 있습니다 및 작업 toofail 발생할 수 있습니다.
* hello 분할 키는 기본 키 또는 고유 인덱스가 정의 hello 선행 열 이어야 합니다. 유효성 검사 쿼리를 분할 또는 병합 hello에 대 한 최상의 성능을 hello 되도록 하 고 hello 실제 데이터 이동 및 삭제 작업에는 분할 키 범위에서 항상 수행 합니다.
* 사용자 데이터베이스가 있는 hello 지역 및 데이터 센터에서 분할 / 병합 서비스를 배치 합니다. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-scale-overview-split-and-merge/split-merge-overview.png
[2]:./media/sql-database-elastic-scale-overview-split-and-merge/diagnostics.png
[3]:./media/sql-database-elastic-scale-overview-split-and-merge/diagnostics-config.png

