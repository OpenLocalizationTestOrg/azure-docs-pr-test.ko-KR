---
title: "저장소 테이블 디자인 가이드 aaaAzure | Microsoft Docs"
description: "Azure 테이블 저장소에서 확장형 및 영구 테이블 디자인"
services: storage
documentationcenter: na
author: jasonnewyork
manager: tadb
editor: tysonn
ms.assetid: 8e228b0c-2998-4462-8101-9f16517393ca
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 02/28/2017
ms.author: jahogg
ms.openlocfilehash: bbac5e83fe994c1ba1408dd43367fbcfca6a2148
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-table-design-guide-designing-scalable-and-performant-tables"></a>Azure 저장소 테이블 디자인 가이드: 확장성이 뛰어난 디자인 및 성능이 뛰어난 테이블
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

toodesign 확장성과 성능이 뛰어난 테이블 다양 한 성능, 확장성 및 비용 등의 요소를 고려해 야 합니다. 관계형 데이터베이스에 대 한 스키마를 이전에 디자인에 이러한 고려 사항에 친숙 한 tooyou 됩니다 hello Azure 테이블 서비스 저장소 모델 및 관계형 모델 간의 몇 가지 유사점 상태인 분명 하지만 많은 중요 한 차이입니다. 이러한 차이는 일반적으로 잘못 되었거나 비 직관적인 toosomeone 관계형 데이터베이스에 잘 알고 표시 될 수는 있지만 hello Azure 테이블 서비스와 같은 NoSQL 키/값 저장소를 디자인 하는 경우에 대 한 이해 수행 있는 여러 디자인 toovery 될 있습니다. 테이블 서비스 hello 수십억 개의 엔터티 (행 관계형 데이터베이스 용어에서)의 데이터 또는 매우 높은 지원 해야 하는 데이터 집합에 포함 될 수 있는 디자인 된 toosupport 클라우드 규모 응용 프로그램 된다는 hello 사실에 입각 반영 됩니다 대부분의 디자인 차이점 트랜잭션 볼륨이: 따라서 데이터를 저장 하는 방법에 대 한 다르게 toothink 필요 하며 hello 테이블 서비스의 작동 방식을 이해 합니다. 훨씬 더에 (및 저렴 한 비용)는 잘 설계 된 NoSQL 데이터 저장소 솔루션 tooscale 사용 하도록 설정할 수는 관계형 데이터베이스를 사용 하는 솔루션 보다 합니다. 이 가이드에서는 이러한 항목에 대해 설명합니다.  

## <a name="about-hello-azure-table-service"></a>Hello Azure 테이블 서비스에 대 한
이 섹션을 강조 표시 기능 중 일부 hello 키 hello 테이블 서비스의 성능과 확장성에 대 한 관련 toodesigning 특히는 합니다. 새 tooAzure 저장소 및 테이블 서비스 hello 인 경우 먼저 읽어 [Azure 저장소 소개 tooMicrosoft](storage-introduction.md) 및 [.NET을 사용 하 여 Azure 테이블 저장소 시작](storage-dotnet-how-to-use-tables.md) hello 나머지를 읽기 전에 아티클을 말합니다. 이 가이드의 hello 초점은 hello 테이블 서비스에 있는 경우에 일부 설명은 hello Azure 큐 및 Blob 서비스에 사용 하는 방법으로 hello 솔루션에서 테이블 서비스와 함께 포함 됩니다.  

Hello 테이블 서비스는 무엇입니까? Hello 이름에서 예상과 hello 테이블 서비스는 테이블 형식으로 toostore 데이터를 사용 합니다. Hello 표준 용어 hello 테이블의 각 행 엔터티를 나타내고 hello 열 저장소 hello 해당 엔터티에의 다양 한 속성. 모든 엔터티에 하나만 지정 하는 한 쌍의 키 toouniquely 하 고 테이블 서비스 hello 타임 스탬프 열 hello 엔터티를 마지막으로 수정한 tootrack 사용 (이 자동으로 발생 하 고 임의 값으로 수동으로 hello 타임 스탬프를 덮어쓸 수 없습니다). 테이블 서비스 hello이 마지막 수정 타임 스탬프 (LMT) toomanage 낙관적 동시성을 사용 합니다.  

> [!NOTE]
> hello 테이블 서비스 REST API 작업 반환할는 **ETag** hello 마지막 수정 타임 스탬프 (LMT)에서 파생 되는 값입니다. 사용 하 여이 문서에 hello 조건 ETag 및 LMT 교대로 toohello 참조 하기 때문에 동일한 데이터 원본으로 사용 합니다.  
> 
> 

hello 다음 예제에서는 간단한 테이블 디자인 toostore employee 및 department 엔터티를 표시 합니다. 이 가이드의 뒷부분에 나오는 hello 예 중 대부분은이 간단한 디자인 기반으로 합니다.  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>Timestamp</th>
<th></th>
</tr>
<tr>
<td>Marketing</td>
<td>00001</td>
<td>2014-08-22T00:50:32Z</td>
<td>
<table>
<tr>
<th>FirstName</th>
<th>LastName</th>
<th>Age</th>
<th>Email</th>
</tr>
<tr>
<td>Don</td>
<td>Hall</td>
<td>34</td>
<td>donh@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td>Marketing</td>
<td>00002</td>
<td>2014-08-22T00:50:34Z</td>
<td>
<table>
<tr>
<th>FirstName</th>
<th>LastName</th>
<th>Age</th>
<th>Email</th>
</tr>
<tr>
<td>Jun</td>
<td>Cao</td>
<td>47</td>
<td>junc@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td>Marketing</td>
<td>부서</td>
<td>2014-08-22T00:50:30Z</td>
<td>
<table>
<tr>
<th>DepartmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td>Marketing</td>
<td>153</td>
</tr>
</table>
</td>
</tr>
<tr>
<td>Sales</td>
<td>00010</td>
<td>2014-08-22T00:50:44Z</td>
<td>
<table>
<tr>
<th>FirstName</th>
<th>LastName</th>
<th>Age</th>
<th>Email</th>
</tr>
<tr>
<td>Ken</td>
<td>Kwok</td>
<td>23</td>
<td>kenk@contoso.com</td>
</tr>
</table>
</td>
</tr>
</table>


지금까지이 매우 유사한 tooa 테이블 관계형 데이터베이스의 필수 열 hello 되 hello 주요 차이점이 모양과 hello 기능 toostore 여러 엔터티 형식을 hello에 동일한 테이블입니다. 또한 각 hello 사용자 정의 속성와 같은 **FirstName** 또는 **Age** 에 정수 또는 문자열 정당한 같은 관계형 데이터베이스의 열 같은 데이터 형식입니다. 와 달리 관계형 데이터베이스의 테이블 서비스 속성을 가질 필요가 있다는 hello의 스키마가 지정 되지 않은 특성 hello hello 동일 하지만 각 엔터티에 대해 데이터 형식입니다. 단일 속성에 toostore 복잡 한 데이터 형식, 예: JSON 또는 XML serialize 된 형식을 사용 해야 합니다. Hello 테이블 서비스와 같은 지원 데이터 형식, 지원 되는 날짜 범위, 명명 규칙 및 크기 제약 조건에 대 한 자세한 내용은 참조 [테이블 서비스 데이터 모델 이해 hello](http://msdn.microsoft.com/library/azure/dd179338.aspx)합니다.

살펴보게 되겠지만, 사용자가 선택한 **PartitionKey** 및 **RowKey** 기본 toogood 테이블 디자인 됩니다. 테이블에 저장된 모든 엔터티에는 고유하게 조합된 **PartitionKey**와 **RowKey**가 있어야 합니다. 관계형 데이터베이스 테이블의 키와 마찬가지로 hello **PartitionKey** 및 **RowKey** 값은 인덱싱된 toocreate 빠른 조회를 사용 하도록 설정 된 클러스터형된 인덱스가 있어 합니다; 그러나 테이블 서비스 hello 생성 되지 않습니다 보조 인덱스 hello 들은 두 개의 파일 인덱싱된 속성 (뒷부분에서 설명 하는 hello 패턴의 일부 표시이 명백한 제한을 해결할 수는 방법).  

테이블은 하나 이상의 파티션을 구성 하 고 다양 한 hello 디자인는 적절 한 선택 주위 결정 하는 대로 **PartitionKey** 및 **RowKey** toooptimize 솔루션입니다. 솔루션은 파티션으로 구성된 모든 엔터티를 포함하는 단일 테이블로 구성될 수 있지만 일반적으로 솔루션에는 여러 테이블이 있습니다. 표 수 toologically 엔터티를 구성 하 고, 사용 하 여 액세스 toohello 데이터를 관리할 수 있게 액세스 제어 목록, 단일 저장소 작업을 사용 하 여 전체 테이블을 삭제할 수 있습니다.  

### <a name="table-partitions"></a>테이블 파티션
hello 계정 이름, 테이블 이름 및 **PartitionKey** 함께 hello 테이블 서비스는 hello 엔터티를 저장 하는 hello 저장소 서비스 내에서 파티션 hello를 식별 합니다. 주소 지정 체계 엔터티에 대 한 hello의 일부분인, 뿐만 아니라 파티션 트랜잭션에 대 한 범위를 정의 (참조 [엔터티 그룹 트랜잭션을](#entity-group-transactions) 아래), 및 hello 테이블 서비스 확장 하는 방법의 양식 hello 기반 합니다. 파티션에 대한 자세한 내용은 [Azure 저장소 확장성 및 성능 목표](storage-scalability-targets.md)를 참조하세요.  

테이블 서비스 hello에서 개별 노드 하나 서비스 또는 파티션을 완료 및 동적으로 부하 분산 하 여 서비스 눈금 hello 노드 간에 파티션이 합니다. Hello 테이블 서비스의 수는 노드가 부하 상태에서 경우 *분할* hello 파티션 범위에 해당 노드를 서로 다른 노드에로 서비스; hello 서비스 수 트래픽 subsides 때 *병합* hello 파티션을에서 범위 단일 노드로 다시 quiet 노드입니다.  

Hello에 대 한 자세한 내용은 내부 hello 테이블 서비스를 하 고 세부적인 특히 hello 서비스에서 파티션을 관리 하는 방법 참조 hello 용지 [Microsoft Azure 저장소: A 항상 사용 가능한 클라우드 저장소 서비스 강력한 일관성](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).  

### <a name="entity-group-transactions"></a>EGT(엔터티 그룹 트랜잭션)
Hello 테이블 서비스에서에서 엔터티 그룹 트랜잭션 (EGTs)은 여러 엔터티 간에 자동 업데이트를 수행 하기 위한 hello만 기본 제공 메커니즘입니다. EGTs 참조 tooas 사항도 *트랜잭션 일괄 처리* 일부 설명서에서는 합니다. EGTs hello에 저장 된 엔터티 에서만 작동할 수 있습니다 동일한 파티션 (공유 hello 지정된 된 테이블에서 동일한 파티션 키) 이므로 해당 엔터티가 서로 hello에 tooensure 필요한 여러 엔터티에서 원자성 트랜잭션 동작 언제 든 지 동일한 파티션에 합니다. 종종 hello 동일 테이블 (및 파티션)의 여러 엔터티 형식을 유지 하 고 서로 다른 엔터티 형식에 대 한 여러 테이블을 사용 하지에 대 한 이유입니다. 단일 EGT는 최대 100개의 엔터티에서 작동할 수 있습니다.  처리 중요 tooensure에 대 한 여러 개의 동시 EGTs 제출 하는 경우 이러한 EGTs 그렇지 않으면 처리 지연 될 수 있습니다 EGTs 걸쳐 공통 되는 엔터티에 대해 작동 하지 마십시오.

EGTs tooevaluate 디자인에 대 한 잠재적인 영향에 대해서도 소개: 많은 파티션을 사용 하 여 늘어납니다 hello 확장성 응용 프로그램을 Azure의 부하 분산 요청 노드에서 기회가 늘어나기 때문이 hello로 제한 될 수 있습니다 응용 프로그램 tooperform 원자성 트랜잭션의 기능 및 데이터에 대 한 강력한 일관성을 유지 관리 합니다. 또한 hello 트랜잭션 처리량을 단일 노드에 대해 예상할 수를 제한할 수 있는 파티션의 hello 수준에서 특정 확장성 목표 발생 되어: Azure 저장소 계정과 hello 테이블에 대 한 hello 확장성 목표에 대 한 자세한 내용은 서비스 참조, [Azure 저장소 확장성 및 성능 목표](storage-scalability-targets.md)합니다. 이 가이드의 뒷부분에 나오는 섹션에 설명 다양 한 디자인 전략 데 도움이 되는이 샘플과 같이 장단점을 관리 하 고 최상의 방법을 toochoose 파티션 키 기반 클라이언트 응용 프로그램의 hello 특정 요구 사항에 설명 합니다.  

### <a name="capacity-considerations"></a>용량 고려 사항
hello 다음 표에서 일부의 hello 키 값 toobe 테이블 서비스 솔루션을 디자인 하는 경우 인식 나타냅니다.  

| Azure 저장소 계정의 총 용량 | 500TB |
| --- | --- |
| Azure 저장소 계정에서 테이블의 수 |Hello 저장소 계정의 용량 hello로만 제한 |
| 테이블에 있는 파티션 수 |Hello 저장소 계정의 용량 hello로만 제한 |
| 파티션의 엔터티 수 |Hello 저장소 계정의 용량 hello로만 제한 |
| 개별 엔터티의 크기 |최대 255 개의 속성을 최대 too1 MB (hello를 포함 하 여 **PartitionKey**, **RowKey**, 및 **타임 스탬프**) |
| Hello 크기인 **PartitionKey** |크기가 too1 KB 문자열 |
| Hello 크기인 **RowKey** |크기가 too1 KB 문자열 |
| 엔터티 그룹 트랜잭션의 크기 |트랜잭션이 최대 100 개의 엔터티가 포함 될 수 있습니다 및 hello 페이로드 크기는 4MB 미만 이어야 합니다. EGT는 한 번에 하나의 엔터티만 업데이트할 수 있음 |

자세한 내용은 참조 [테이블 서비스 데이터 모델 이해 hello](http://msdn.microsoft.com/library/azure/dd179338.aspx)합니다.  

### <a name="cost-considerations"></a>비용 고려 사항
테이블 저장소 상대적으로 비용이 많이 들지 않습니다. 하지만 hello 테이블 서비스를 사용 하는 솔루션의 평가판의 일부로 트랜잭션의 두 용량 사용량 및 hello 수량에 대 한 예상 비용을 포함 해야 합니다. 그러나 순서 tooimprove hello에 정규화 되지 않은 또는 중복 데이터를 저장 하는 많은 시나리오에서 성능이 나 확장성을 솔루션의는 올바른 방법은 tootake. 가격 책정에 대한 자세한 내용은 [Azure 저장소 가격 책정](https://azure.microsoft.com/pricing/details/storage/)을 참조하세요.  

## <a name="guidelines-for-table-design"></a>테이블 디자인 지침
이러한 목록 요약 테이블을 디자인할 때 염두에서 유지 해야 하는 hello 핵심 지침 몇 가지 하 고이 가이드 뒷부분에서 자세히 모두에서 설명 합니다. 이러한 지침은 hello 지침을 수행 해야 하는 일반적으로 관계형 데이터베이스 디자인에 대 한 매우 다릅니다.  

사용자 테이블 서비스 솔루션 toobe 디자인 *읽을* 효율적인:

* ***읽기 작업이 많은 응용 프로그램의 쿼리를 위해 디자인합니다.*** 실행할 hello 쿼리 (특히 hello 대기 시간이 중요 한 것)에 대해 생각 하는 테이블을 디자인 하는 경우 먼저 엔터티를 업데이트할 것 방법에 대 한 생각 합니다. 이는 일반적으로 솔루션의 효율성 및 성능에 영향을 줍니다.  
* ***쿼리에서 PartitionKey와 RowKey 둘 다 지정합니다.*** *쿼리를 가리키고* hello 가장 효율적인 테이블 서비스 쿼리는 같은 합니다.  
* ***엔터티의 중복 복사본을 저장하는 것이 좋습니다.*** 테이블 저장소는 비용이 적게 드는 것이 좋습니다 동일한 엔터티를 여러 번 (다른 키를 가진) hello 저장 tooenable 더 효율적인 쿼리 합니다.  
* ***데이터를 비정규화하는 것이 좋습니다.*** 테이블 저장소는 저렴하기 때문에 데이터를 비정규화하는 것이 좋습니다. 예를 들어 데이터 집계에 대 한 쿼리 하기만 tooaccess 단일 엔터티 있도록 요약 엔터티를 저장 합니다.  
* ***복합 키 값을 사용하는 것이 좋습니다.*** hello 있는 키만이 **PartitionKey** 및 **RowKey**합니다. 예를 들어 tooenable 대체 키가 지정 된 액세스 경로 tooentities 복합 키 값을 사용 합니다.  
* ***쿼리 프로젝션을 사용합니다.*** Hello 방금 hello 필요한 필드를 선택 하는 쿼리를 사용 하 여 hello 네트워크를 통해 전송 하는 데이터 양을 줄일 수 있습니다.  

사용자 테이블 서비스 솔루션 toobe 디자인 *쓰기* 효율적인:  

* ***핫 파티션을 만들지 마세요.*** 시간의 언제 든 지 여러 파티션에서 키 toospread 수 있도록 하는 사용자의 요청을 선택 합니다.  
* ***트래픽 급증을 방지합니다.*** Hello 트래픽을 적절 한 기간을 통해 매끄럽게 한 트래픽 급증을 방지 합니다.
* ***각 엔터티 유형에 대한 별도의 테이블을 만들 필요가 없습니다.*** 엔터티 형식 간에 원자성 트랜잭션을 요구 하면 저장할 수 있습니다 이러한 여러 엔터티 형식을 hello 파티션에 동일한 hello 같은 테이블입니다.
* ***Hello 최대 처리량을 조정 해야 것이 좋습니다.*** Hello 테이블 서비스에 대 한 확장성 목표 hello 알고 있어야 하며 디자인에서 되지 않도록 하면 tooexceed 확인 해당 합니다.  

이 가이드에서는 이 모든 원칙을 실습해 볼 수 있는 예제를 제공합니다.  

## <a name="design-for-querying"></a>쿼리를 위한 디자인
많이 사용, 쓰기 중심 또는 두 hello 혼합 하 여 테이블 서비스 솔루션을 읽을 수 있습니다. 이 섹션으로 읽기 작업을 효율적으로 하 여 테이블 서비스 toosupport 디자인할 때 고려에서 사항 toobear hello 집중 합니다. 일반적으로 읽기 작업을 효율적으로 지원하는 디자인은 쓰기 작업에도 효율적입니다. 그러나 가지 추가 고려 사항 toobear 염두에서 디자인 toosupport 쓰기 작업을 hello 다음 섹션에서 설명 하는 경우 [데이터 수정 위한 디자인](#design-for-data-modification)합니다.

테이블 서비스 솔루션 tooenable 프로그램을 디자인 하기 위한 좋은 출발점 tooread 데이터 효율적으로 tooask "하는 쿼리는 hello 테이블 서비스에서에서 필요한 응용 프로그램 요구 tooexecute tooretrieve hello 데이터가?"  

> [!NOTE]
> 테이블 서비스 hello로는 것이 중요 tooget hello 디자인 올바른 들겠지만 많은 시간과 비용이 많이 드는 toochange 있기 때문에 나중에 해당 합니다. 예를 들어 tooan 기존 데이터베이스 인덱스를 추가 하 여 가능한 tooaddress 성능 문제는 종종 관계형 데이터베이스에서:이 hello 테이블 서비스를 사용 하는 옵션입니다.  
> 
> 

이 섹션을 쿼리 하기 위한 테이블을 디자인할 때 고려해 야 할 주요 문제를 hello에 중점을 둡니다. 이 섹션에서 다루는 hello 항목은 다음과 같습니다.

* [PartitionKey 및 RowKey 선택이 쿼리 성능에 미치는 영향](#how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance)
* [적절한 PartitionKey 선택](#choosing-an-appropriate-partitionkey)
* [Hello 테이블 서비스에 대 한 쿼리 최적화](#optimizing-queries-for-the-table-service)
* [Hello 테이블 서비스의에서 데이터 정렬](#sorting-data-in-the-table-service)

### <a name="how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance"></a>PartitionKey 및 RowKey 선택이 쿼리 성능에 미치는 영향
hello 다음 예제에서는 가정 hello 테이블 서비스에서 다음 구조 hello로 employee 엔터티를 저장 하는 (대부분의 hello 예제 생략 hello **타임 스탬프** 명확성에 대 한 속성):  

| *열 이름* | *데이터 형식* |
| --- | --- |
| **PartitionKey** (부서 이름) |String |
| **RowKey** (직원 Id) |String |
| **FirstName** |String |
| **LastName** |String |
| **Age** |Integer |
| **EmailAddress** |문자열 |

이전 섹션 hello [Azure 테이블 서비스 개요](#overview) hello 주요 기능 hello Azure 테이블 서비스의 쿼리에 대 한 디자인에 직접적인 영향을 주지 않은의 일부에 대해 설명 합니다. 이렇게 하면 테이블 서비스 쿼리를 디자인 하기 위한 일반적인 지침을 따르는 hello 합니다. 테이블 서비스 REST API 참조 항목에 대 한 hello에서에서 hello 필터 구문 아래 hello 예제에서 사용 되는 [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx)합니다.  

* A ***지점 쿼리*** hello 가장 효율적인 조회 toouse 이며 toobe 대용량 조회 또는 가장 짧은 대기 시간을 요구 하는 조회에 사용 되는 것이 좋습니다. 이러한 쿼리 צ ְ ײ hello 인덱스 toolocate 개별 엔터티에 매우 효율적으로 hello 둘 다 지정 하 여 **PartitionKey** 및 **RowKey** 값입니다. 예: $filter=(PartitionKey eq 'Sales') and (RowKey eq '2')  
* 가 두 번째로 가장는 ***범위 쿼리*** hello를 사용 하 여 **PartitionKey** 및 범위에 대 한 필터 **RowKey** tooreturn 둘 이상의 엔터티 값입니다. hello **PartitionKey** 값을 특정 파티션 및 hello 식별 **RowKey** 해당 파티션의 hello 엔터티 하위 집합을 식별 하는 값입니다. 예: $filter=PartitionKey eq 'Sales' and RowKey ge 'S' and RowKey lt 'T'  
* 세 번째 최고는 ***파티션 검색*** hello를 사용 하 여 **PartitionKey** 있고 다른 키가 아닌 속성에 대 한 필터는 둘 이상의 엔터티를 반환할 수 있습니다. hello **PartitionKey** hello 속성 값을 해당 파티션의 hello 엔터티 하위 집합에 대 한 select 및 특정 파티션을 식별 하는 값입니다. 예: $filter=PartitionKey eq 'Sales' and LastName eq 'Smith'  
* A ***Table Scan*** hello는 **PartitionKey** 검색의 모든 테이블에 일치 하는 모든 항목에 대 한 다시 구성 하는 hello 파티션을 하므로 효율적이 지 않습니다. 필터 hello를 사용 하는 여부에 관계 없이 테이블 검색이 수행 **RowKey**합니다. 예: $filter=LastName eq 'Jones'  
* 여러 엔터티를 반환하는 쿼리는 **PartitionKey**와 **RowKey** 순으로 정렬된 엔터티를 반환합니다. tooavoid 앞선 hello 엔터티 hello 클라이언트에서 선택 된 **RowKey** hello 가장 일반적인 정렬 순서를 정의 하는 합니다.  

사용는 "**또는**" 필터에 따라 toospecify **RowKey** 파티션 검색의 결과 값을 범위 쿼리로 처리 되지 않습니다. 따라서 다음과 같은 필터를 사용하는 쿼리는 피해야 합니다. $filter=PartitionKey eq 'Sales' and (RowKey eq '121' or RowKey eq '322')  

Hello 저장소 클라이언트 라이브러리 tooexecute 효율적인 쿼리를 사용 하 여 클라이언트 쪽 코드 예제 참조.  

* [Hello 저장소 클라이언트 라이브러리를 사용 하 여 지점 쿼리를 실행 합니다.](#executing-a-point-query-using-the-storage-client-library)
* [LINQ를 사용하여 여러 엔터티 검색](#retrieving-multiple-entities-using-linq)
* [서버 쪽 프로젝션](#server-side-projection)  

여러 엔터티를 처리할 수 있는 클라이언트 쪽 코드의 예에 대 한 형식에에서 저장 된 hello 동일 테이블 참조 하십시오.  

* [유형이 다른 엔터티 유형 작업](#working-with-heterogeneous-entity-types)  

### <a name="choosing-an-appropriate-partitionkey"></a>적절한 PartitionKey 선택
사용자가 선택한 **PartitionKey** 간의 균형 EGTs (tooensure 일관성) hello 필요 tooenables hello 사용 요구 사항이 toodistribute hello에 대 한 엔터티를 여러 파티션에 (tooensure 확장성이 뛰어난 솔루션).  

최대에서는 단일 파티션의 모든 엔터티를 저장할 수 있지만이 솔루션의 hello 확장성이 제한 될 수 있습니다 이며 hello 테이블 서비스 요청 수 tooload 분산할 수 없도록 방지 합니다. 다른 한편으로는 hello에 확장성이 높은 것 및 hello 테이블 서비스 tooload 잔액 요청을 할 수 있게 하지만으로 인해 엔터티 그룹 트랜잭션을 사용 하 여 파티션당 하나의 엔터티가 저장할 수 있습니다.  

이상적 **PartitionKey** toouse 효율적인 쿼리를 수 있는 되며 충분 한 파티션을 tooensure 솔루션은 확장 가능 합니다. 일반적으로 엔터티에는 충분한 파티션으로 엔터티를 분산하는 적절한 속성이 있습니다.

> [!NOTE]
> 예를 들어 사용자 또는 직원에 대한 정보를 저장하는 시스템에서는 UserID가 적절한 PartitionKey일 수 있습니다. Hello 파티션 키로 지정 된 사용자 Id를 사용 하는 몇 개의 엔터티를 할 수 있습니다. 사용자에 대한 데이터를 저장하는 각 엔터티는 단일 파티션으로 그룹화되므로 이러한 엔터티는 높은 확장성을 유지하면서 엔터티 그룹 트랜잭션을 통해 액세스할 수 있습니다.
> 
> 

선택한에서 추가 고려 사항 사항이 **PartitionKey** 삽입, 업데이트 및 엔터티를 삭제 합니다 toohow 관련 된: hello 섹션을 참조 [데이터 수정 위한 디자인](#design-for-data-modification) 아래 합니다.  

### <a name="optimizing-queries-for-hello-table-service"></a>Hello 테이블 서비스에 대 한 쿼리 최적화
테이블 서비스 hello hello를 사용 하 여 엔터티를 자동으로 인덱싱됩니다 **PartitionKey** 및 **RowKey** 단일 클러스터형된 인덱스의 값에 따라서 이유 지점 쿼리가 가장 효율적인 toouse를 hello는 hello . 그러나 여러 가지 hello hello에서 클러스터형된 인덱스에는 다른 인덱스가 없는 **PartitionKey** 및 **RowKey**합니다.

대부분의 디자인 여러 조건을 기반으로 하는 엔터티의 tooenable 조회 요구 사항을 충족 해야 합니다. 예를 들어 전자 메일, 직원 ID 또는 성을 기반으로 직원 엔터티를 찾을 수 있어야 합니다. 패턴 hello 섹션의 다음 hello [테이블 디자인 패턴](#table-design-patterns) 이러한 유형의 요구 사항 해결 하 고 hello 테이블 서비스 보조 인덱스를 제공 하지 않습니다 hello 팩트 해결 방법에 설명 합니다.  

* [파티션 내 보조 인덱스 패턴](#intra-partition-secondary-index-pattern) -복사본을 여러 개 사용 하 여 각 엔터티 다른 저장 **RowKey** 값 (hello에 같은 파티션) tooenable 신속 하 고 효율적인 조회 및 대체 정렬 순서를 사용 하 여 다른 **RowKey** 값입니다.  
* [보조 인덱스 간 파티션 패턴](#inter-partition-secondary-index-pattern) -각 사용 하 여 엔터티 RowKey 값이 다른 별도 파티션을 또는 별도 테이블 tooenable 빠른의 여러 복사본을 저장 하 고 다른 를사용하여효율적인조회및대체정렬순서**RowKey** 값입니다.  
* [인덱스 엔터티 패턴](#index-entities-pattern) -인덱스 엔터티 tooenable 효율적인 검색 엔터티 목록을 반환 하는 유지 관리 합니다.  

### <a name="sorting-data-in-hello-table-service"></a>Hello 테이블 서비스의에서 데이터 정렬
hello 테이블 서비스에 따라 내림차순으로 정렬 하는 엔터티를 반환 합니다. **PartitionKey** 한 다음 **RowKey**합니다. 이러한 키가 문자열 값 및 숫자 값이 올바르게 정렬 tooensure tooa 고정 길이 변환 하 고 0은 사용이 채울 해야 합니다. 예를 들어 경우 hello 직원 id 값으로 사용할 있습니다 hello **RowKey** 는 정수 값, 직원 id를 변환 해야 **123** 너무**00000123**합니다.  

많은 응용 프로그램의 순서가 다른 toouse 데이터가 정렬 요구 사항이: 예를 들어, 이름별 또는 날짜를 조인 하 여 직원을 정렬 합니다. 패턴 hello 섹션의 다음 hello [테이블 디자인 패턴](#table-design-patterns) 엔터티에 대 한 tooalternate 정렬 순서 하는 방법을 주소:  

* [파티션 내 보조 인덱스 패턴](#intra-partition-secondary-index-pattern) -다른 RowKey 값을 사용 하 여 각 엔터티의 여러 복사본을 저장 (hello에 같은 파티션) 다른 RowKey 값을 사용 하 여 tooenable 신속 하 고 효율적인 조회 및 대체 정렬 순서입니다.  
* [보조 인덱스 간 파티션 패턴](#inter-partition-secondary-index-pattern) -tooenable 별도 테이블에서에서 별도 파티션의 빠르게 RowKey 값이 다른를 사용 하 여 각 엔터티의 여러 복사본을 저장 하 고 다른 RowKey를 사용 하 여 효율적인 조회 및 대체 정렬 순서 값입니다.
* [비상 로그 패턴](#log-tail-pattern) -검색 hello  *n*  엔터티 가장 최근에 추가 된 tooa 파티션을 사용 하 여 한 **RowKey** 역방향 날짜와 시간 순서에 정렬 하는 값입니다.  

## <a name="design-for-data-modification"></a>데이터 수정을 위한 디자인
이 섹션 삽입, 업데이트를 최적화 하기 위한 hello 디자인 고려 사항에 중점적으로 설명 하 고 삭제 합니다. 일부 경우에서와 마찬가지로 관계형 데이터베이스에 대 한 디자인에 (hello 기술을 관리 하기 위한 디자인 hello 하지만 데이터 수정에 대 한 최적화 하는 디자인에 대 한 쿼리를 최적화 하는 설계 간 절충 값 tooevaluate hello 해야 합니다. 상충 관계에서 서로 관계형 데이터베이스). 섹션 hello [테이블 디자인 패턴](#table-design-patterns) hello 테이블 서비스에 대 한 몇 가지 세부 디자인 패턴을 설명 하 고 몇 이러한 장단점에 설명 합니다. 실제로 엔터티 쿼리에 최적화된 디자인은 대부분 엔터티를 수정하는 데에도 효율적입니다.  

### <a name="optimizing-hello-performance-of-insert-update-and-delete-operations"></a>Hello 성능 최적화의 삽입, 업데이트 및 삭제 작업
tooupdate 또는 엔터티를 삭제, 수 tooidentify 있어야 hello를 사용 하 여 **PartitionKey** 및 **RowKey** 값입니다. 사용자가 선택한 이러한 점에서 **PartitionKey** 및 **RowKey** 따라야 엔터티 수정 유사한 조건 tooyour 선택 toosupport 가리킨 쿼리 tooidentify 엔터티를 것 이므로 최대한 효율적으로 합니다. Toouse는 비효율적인 파티션 또는 테이블 스캔 toolocate 순서 toodiscover hello에 엔터티를 원하지 않는 **PartitionKey** 및 **RowKey** 값 tooupdate 필요 하거나 삭제 합니다.  

패턴 hello 섹션의 다음 hello [테이블 디자인 패턴](#table-design-patterns) 주소 hello 성능 최적화 또는 삽입, 업데이트 및 삭제 작업:  

* [패턴을 삭제 하는 정보의 양이](#high-volume-delete-pattern) -Enable hello 삭제는 대량의 동시 삭제에 대 한 모든 hello 엔터티는 각각의 별도 테이블에 저장 하 여 엔터티; hello 테이블을 삭제 하 여 hello 엔터티를 삭제 합니다.  
* [데이터 계열 패턴](#data-series-pattern) -저장소 전체 데이터 계열에는 단일 엔터티 toominimize hello 수가 요청 합니다.  
* [넓은 엔터티 패턴](#wide-entities-pattern) -이상 252 속성을 가진 여러 개의 물리적 엔터티 toostore 논리적 엔터티를 사용 합니다.  
* [큰 엔터티 패턴](#large-entities-pattern) -blob 저장소 toostore 큰 속성 값 사용.  

### <a name="ensuring-consistency-in-your-stored-entities"></a>저장된 엔터티의 일관성 유지
데이터 수정 최적화를 선택 하는 키 영향을 주는 다른 중요 한 요소 hello 어떻게 원자성 트랜잭션을 사용 하 여 tooensure 일관성. EGT toooperate hello에 저장 된 엔터티 에서만 사용할 수 있습니다 같은 파티션에 합니다.  

패턴 hello 섹션의 다음 hello [테이블 디자인 패턴](#table-design-patterns) 일관성을 관리 하는 주소:  

* [파티션 내 보조 인덱스 패턴](#intra-partition-secondary-index-pattern) -복사본을 여러 개 사용 하 여 각 엔터티 다른 저장 **RowKey** 값 (hello에 같은 파티션) tooenable 신속 하 고 효율적인 조회 및 대체 정렬 순서를 사용 하 여 다른 **RowKey** 값입니다.  
* [보조 인덱스 간 파티션 패턴](#inter-partition-secondary-index-pattern) -각 사용 하 여 엔터티 RowKey 값이 다른 별도 파티션을 또는 별도 테이블 tooenable 빠른의 여러 복사본을 저장 하 고 다른 를사용하여효율적인조회및대체정렬순서**RowKey** 값입니다.  
* [결과적으로 일관성 있는 트랜잭션 패턴](#eventually-consistent-transactions-pattern) - Azure 큐를 사용하여 파티션 경계 또는 저장소 시스템 경계 간에 결과적으로 일관성 있는 동작을 지원합니다.
* [인덱스 엔터티 패턴](#index-entities-pattern) -인덱스 엔터티 tooenable 효율적인 검색 엔터티 목록을 반환 하는 유지 관리 합니다.  
* [비 정규화 패턴](#denormalization-pattern) -결합 되어 감사가 만들어집니다 관련 데이터를 함께 단일 엔터티 tooenable에 tooretrieve 모든 hello 필요한 데이터를 단일 지점 쿼리를 사용 합니다.  
* [데이터 계열 패턴](#data-series-pattern) -저장소 전체 데이터 계열에는 단일 엔터티 toominimize hello 수가 요청 합니다.  

엔터티 그룹 트랜잭션에 대 한 정보를 hello 섹션을 참조 하십시오. [엔터티 그룹 트랜잭션을](#entity-group-transactions)합니다.  

### <a name="ensuring-your-design-for-efficient-modifications-facilitates-efficient-queries"></a>효율적인 수정을 위한 디자인이 효율적인 쿼리에도 유용
대부분의 경우 특정 시나리오에 대 한 hello 대/소문자 인지 여부를 항상 효율적인 수정 작업에 효율적으로 쿼리 결과 대 한 디자인 평가 해야 합니다. 일부 hello 섹션의 hello 패턴 [테이블 디자인 패턴](#table-design-patterns) 명시적으로 쿼리 및 수정 엔터티 간의 장단점을 평가 하 고 각 유형의 작업이의 계정 hello 번호를 항상 고려해 야 합니다.  

패턴 hello 섹션의 다음 hello [테이블 디자인 패턴](#table-design-patterns) 효율적인 쿼리를 위해 디자인 하 고 효율적인 데이터 수정을 위한 디자인 간의 장단점 주소:  

* [복합 키 패턴](#compound-key-pattern) -사용 하 여 복합 **RowKey** 값 tooenable 클라이언트 toolookup 관련 데이터는 단일 지점에서 쿼리를 사용 합니다.  
* [비상 로그 패턴](#log-tail-pattern) -검색 hello  *n*  엔터티 가장 최근에 추가 된 tooa 파티션을 사용 하 여 한 **RowKey** 역방향 날짜와 시간 순서에 정렬 하는 값입니다.  

## <a name="encrypting-table-data"></a>테이블 데이터의 암호화
삽입에 대 한 문자열 엔터티 속성의.NET Azure 저장소 클라이언트 라이브러리 지원 암호화 hello 및 교체 작업 합니다. 이진 속성으로 암호화 하는 hello 문자열 hello 서비스에 저장 됩니다 및 암호 해독 한 후 뒤로 toostrings 변환 됩니다.    

테이블의 경우 또한 toohello 암호화 정책 사용자 지정 해야 hello 속성 toobe 암호화 합니다. 이것은 특성(TableEntity에서 파생 되는 POCO 엔터티)을 지정[EncryptProperty]하거나 암호화 해결 프로그램 요청 옵션에서 수행할 수 있습니다.  암호화 해결 프로그램은 파티션 키, 행 키, 그리고 속성 이름 및 암호화 여부 속성을 나타내는  Bool방식을 반환하는 대표자입니다. 암호화 하는 동안 toohello 통신에 쓰는 동안 속성을 암호화 해야 하는지 여부를 hello 클라이언트 라이브러리 정보 toodecide이를 사용 합니다. 또한 hello 대리자 hello 가능성은 속성이 암호화 주위 논리를 제공 합니다. (예를 들어 X의 경우, A 속성을 암호화하고 그렇지 않은 경우 A와 B 속성을 암호화) 한다는 확인은 필요 하지 않은 tooprovide 읽기 또는 엔터티를 쿼리 하는 동안이 정보입니다.

병합은 현재 지원되지 않습니다. 속성 하위 집합 암호화 된 다른 키를 사용 하 여 이전에, 이후 hello 새 속성을 병합 하 고 hello 메타 데이터를 업데이트 하기만 하면 데이터가 손실 됩니다. Hello 서비스에서 tooread hello 기존 엔터티를 호출 추가 서비스를 만드는 또는 속성 당 새 키를 사용 하는 적합 하지 않은 성능상의 이유로 필요 하거나 병합 합니다.     

테이블 데이터를 암호화에 대한 정보는 [클라이언트측 암호화 및 Microsoft Azure 저장소에 대한 Azure 키 자격 증명 모음](storage-client-side-encryption.md)을 참조하십시오.  

## <a name="modelling-relationships"></a>관계 모델링
도메인 모델을 작성은 복잡 한 시스템의 hello 디자인에 중요 한 단계입니다. 일반적으로 프로세스 tooidentify 엔터티를 모델링 하는 hello를 사용 하 고 hello 관계도 방식으로 toounderstand로 비즈니스 도메인 hello 및 시스템의 hello 디자인에 게 알립니다. 이 ½ º å 어떻게 hello 테이블 서비스에 대 한 도메인 모델 toodesigns에 hello 일반적인 관계 유형 중 일부 번역할 수 있습니다. 논리적 데이터 모델 tooa 물리적 기반 NoSQL 데이터 모델에서 매핑의 hello 프로세스는 관계형 데이터베이스를 디자인할 때 사용 되는 매우 다릅니다. 일반적으로 관계형 데이터베이스 디자인 중복 – 및 요약에 hello 데이터베이스의 작동 원리의 구현 방법을 hello 선언적 쿼리 기능을 최소화 하기 위한 액세스에 최적화 된 데이터 정규화 프로세스를 가정 합니다.  

### <a name="one-to-many-relationships"></a>일대다 관계
비즈니스 도메인 개체 간의 일대다 관계는 매우 빈번하게 발생합니다. 예를 들어 하나의 부서에 여러 직원이 있는 경우가 여기에 해당합니다. 테이블 서비스 각 장점 및 단점 관련 toohello 특정 시나리오를 될 수 있는 hello에는 몇 가지 방법으로 tooimplement 대 다 관계가 있습니다.  

Hello 예제를 다국적 대기업의 수만 부서 및 employee 엔터티 여기서 모든 부서는 직원 및 각 직원 한 특정 부서와 관련 된 것이 좋습니다. 한 가지 방법은 이러한 employee 엔터티 toostore 별도 부서입니다.  

![][1]

이 예에서는 hello에 따라 hello 형식 간의 암시적 대 다 관계가 **PartitionKey** 값입니다. 각 부서에는 여러 직원이 있을 수 있습니다.  

해당 직원 관련된 엔터티를 같은 파티션 hello 및이 예제에서는 또한 department 엔터티를 보여 줍니다. Toouse 다른 파티션, 테이블 또는 심지어 hello 서로 다른 엔터티 형식에 대 한 저장소 계정을 선택할 수 있습니다.  

다른 접근 방식은 hello 다음 예제와 같이 toodenormalize 정규화 되지 않은 부서 데이터와 사용자 데이터 및 스토어만 employee 엔터티입니다. 에서는이 특정 시나리오에서 정규화 되지 않은이 방법은 아닐 수 있습니다 hello 최상의 부서 관리자의 요구 사항 toobe 수 toochange hello 정보 때문에 있는 경우 toodo이 tooupdate hello 부서의 모든 직원을 필요 합니다.  

![][2]

자세한 내용은 참조 hello [비 정규화 패턴](#denormalization-pattern) 이 가이드의 뒷부분에 나오는 합니다.  

hello 다음 표에 요약 되어 hello 장점 및 단점을 employee 및 department 엔터티 대 다 관계가 있는 저장 하기 위해 위에서 설명한 hello 방법 중 한 가지입니다. 예상 되는 빈도 tooperform 다양 한 작업을 고려해 야: 허용 toohave 해당 작업 으로만 자주 발생 하는 경우 비용이 많이 드는 작업이 포함 된 디자인 수도 있습니다.  

<table>
<tr>
<th>접근 방식</th>
<th>장점</th>
<th>단점</th>
</tr>
<tr>
<td>별도의 엔터티 유형, 동일한 파티션, 동일한 테이블</td>
<td>
<ul>
<li>단일 작업으로 부서 엔터티를 업데이트할 수 있습니다.</li>
<li>요구 사항 toomodify department 엔터티를 설정한 경우 EGT toomaintain 일관성을 사용할 수 있습니다 때마다 있습니다 업데이트/삽입/삭제 employee 엔터티. 예를 들어 각 부서의 직원 수를 유지 관리하는 경우가 여기에 해당됩니다.</li>
</ul>
</td>
<td>
<ul>
<li>일부 클라이언트 작업에 대 한 tooretrieve는 employee 및 department 엔터티 둘 다 할 수 있습니다.</li>
<li>Hello에 저장소 작업이 수행 동일한 파티션 합니다. 대용량 트랜잭션의 경우 핫스폿이 발생할 수 있습니다.</li>
<li>EGT를 사용 하 여 직원 tooa 새 부서를 이동할 수 없습니다.</li>
</ul>
</td>
</tr>
<tr>
<td>별도의 엔터티 유형, 서로 다른 파티션, 테이블 또는 저장소 계정</td>
<td>
<ul>
<li>단일 작업으로 부서 엔터티 또는 직원 엔터티를 업데이트할 수 있습니다.</li>
<li>많은 트랜잭션 볼륨에 도움이 될 수 있습니다이 더 많은 파티션 간에 확산 hello 로드 합니다.</li>
</ul>
</td>
<td>
<ul>
<li>일부 클라이언트 작업에 대 한 tooretrieve는 employee 및 department 엔터티 둘 다 할 수 있습니다.</li>
<li>EGTs toomaintain 일관성을 사용할 수 없는 때 하면 업데이트/삽입/삭제는 직원 및 부서 업데이트 합니다. 예를 들어 부서 엔터티의 직원 수를 업데이트하는 경우가 여기에 해당합니다.</li>
<li>EGT를 사용 하 여 직원 tooa 새 부서를 이동할 수 없습니다.</li>
</ul>
</td>
</tr>
<tr>
<td>단일 엔터티 유형으로 비정규화</td>
<td>
<ul>
<li>단일 요청으로 필요한 모든 hello 정보를 검색할 수 있습니다.</li>
</ul>
</td>
<td>
<ul>
<li>(이 위해서는 있습니다 tooupdate 부서에 모든 hello 직원) tooupdate 부서 정보가 필요한 경우 비용이 많이 드는 toomaintain 일관성 수도 있습니다.</li>
</ul>
</td>
</tr>
</table>

이러한 옵션 중 hello 전문가 사이의 선택 방법과 관련 하 여 아래의 가장 중요 한 특정 응용 프로그램 시나리오에 따라 다릅니다. 예를 들어 얼마나 자주 수행 하면 부서 엔터티 수정; 모든 직원 쿼리 hello 추가 부서별 정보; 필요가 얼마나 비슷한지를? 파티션 또는 저장소 계정에서 toohello 확장성 제한  

### <a name="one-to-one-relationships"></a>일대일 관계
도메인 모델은 엔터티 간의 일대일 관계를 포함할 수 있습니다. Hello 테이블 서비스에에서 한 일 관계 tooimplement 해야 할 경우 필요할 때 tooretrieve 모두 두 개의 관련된 엔터티 toolink hello 하는 방법을 선택 해야 합니다. 이 링크 암시적, hello 키 값에 규칙에 따라 또는 가능 명시적 hello 형태의에 대 한 링크를 저장 하 여 **PartitionKey** 및 **RowKey** 각 엔터티 tooits 값 관련 엔터티. 관련 엔터티 hello를 저장 해야 하는지 여부에 미치는 같은 파티션에 hello 하 hello 섹션을 참조 [대 다 관계](#one-to-many-relationships)합니다.  

구현 고려 사항 이어질 수 있는 있습니다 tooimplement 한 일 관계 hello 테이블 서비스에도 지 note:  

* 큰 엔터티 처리(자세한 내용은 [큰 엔터티 패턴](#large-entities-pattern)참조)  
* 액세스 제어 구현(자세한 내용은 [공유 액세스 서명을 사용하여 액세스 제어](#controlling-access-with-shared-access-signatures)참조)  

### <a name="join-in-hello-client"></a>클라이언트 hello에 가입
테이블 서비스 hello 방법 toomodel 관계 있지만 있습니다 해야 잊지 hello hello 테이블 서비스를 사용 하기 위한 두 가지 주요 이유는 확장성 및 성능. 솔루션의 hello 성능 및 확장성을 손상 시킬 수 있는 많은 관계를 모델링 하는 경우 고려해 야 할 모든 hello 데이터 관계 테이블 디자인에 필요한 toobuild 경우. 수 toosimplify hello 디자인 하 고 필요한 모든 조인을 수행 하는 클라이언트 응용 프로그램을 사용 하는 경우 솔루션의 hello 확장성과 성능을 향상 시킬 수 있습니다.  

예를 들어 매우 자주 변경 되지 않는 데이터가 포함 된 작은 테이블의 경우 다음이 데이터를 한 번에 검색할 수 있고 hello 클라이언트에 캐시 합니다. 이 반복된 왕복을 방지할 수 tooretrieve hello 같은 데이터입니다. 이 가이드에서 살펴본 hello 예제에서 hello 부서 중소기업에서의 집합이 작은 가능성이 toobe 및 자주 있으므로 적합 한 클라이언트 응용 프로그램에 한 번만 다운로드할 수 있는 데이터 및 캐시 데이터를 모양으로 변경 합니다.  

### <a name="inheritance-relationships"></a>상속 관계
클라이언트 응용 프로그램의 클래스는 상속 관계 toorepresent 비즈니스 엔터티의 일부를 구성 하는 집합을 사용 하는 경우 hello 테이블 서비스에서에서 해당 엔터티를 쉽게 유지할 수 있습니다. 예를 들어 클라이언트 응용 프로그램에 정의 된 클래스 집합을 추적 하는 hello 해야할 여기서 **사람** 클래스는 추상 클래스입니다.

![][3]

Hello hello에는 다음과 같은 엔터티를 사용 하 여 단일 Person 테이블을 사용 하 여 테이블 서비스에 두 개의 구체적 클래스의 인스턴스를 유지할 수 있습니다.  

![][4]

Hello 클라이언트 코드에서 동일한 테이블로의 엔터티 형식에 여러 작업에 대 한 자세한 내용은 hello 섹션을 참조 하십시오. [유형이 다른 엔터티 형식 작업](#working-with-heterogeneous-entity-types) 이 가이드의 뒷부분에 나오는 합니다. Toorecognize 클라이언트 코드의 엔터티 형식을 hello 하는 방법의 예를 제공 합니다.  

## <a name="table-design-patterns"></a>테이블 디자인 패턴
이전 섹션에서 toooptimize 테이블와 디자인 방법 모두 엔터티 데이터를 검색할 쿼리를 사용 하 여에 대 한 삽입, 업데이트, 및 엔터티 데이터를 삭제 하는 방법에 대 한 자세한 내용은 일부에 대해 알아보았습니다. 이 섹션에서는 테이블 서비스 솔루션에서 사용하기에 적합한 몇 가지 패턴에 대해 알아봅니다. 또한 어떻게 해결할 수 있습니다 거의 hello 문제와 장단점이이 가이드에서 이전에 발생 하는 중 일부에 대해 표시 됩니다. hello 다음 다이어그램에서는 요약 hello 다양 한 패턴 간에 hello 관계 합니다.  

![][5]

위의 hello 패턴 지도 패턴 (파란색),이 가이드에 설명 되어 있는 바이러스 패턴 (주황) 간에 관계를 강조 표시 합니다. 물론 고려할 만한 다른 많은 패턴도 있습니다. 예를 들어 hello 테이블 서비스에 대 한 주요 시나리오 중 하나는 toouse hello [구체화 된 뷰 패턴](https://msdn.microsoft.com/library/azure/dn589782.aspx) hello에서 [명령 쿼리 책임 분리 (CQRS)](https://msdn.microsoft.com/library/azure/jj554200.aspx) 패턴입니다.  

### <a name="intra-partition-secondary-index-pattern"></a>파티션 간 보조 인덱스 패턴
복사본을 여러 개 사용 하 여 각 엔터티 다른 저장 **RowKey** 값 (hello에 같은 파티션) 다른을 사용 하 여 tooenable 신속 하 고 효율적인 조회 및 대체 정렬 순서 **RowKey** 값입니다. EGT를 사용하여 복사본 간의 업데이트를 일관성 있게 유지할 수 있습니다.  

#### <a name="context-and-problem"></a>컨텍스트 및 문제점
테이블 서비스 hello hello를 사용 하 여 엔터티를 자동으로 인덱싱됩니다 **PartitionKey** 및 **RowKey** 값입니다. 이렇게 하면 클라이언트 응용 프로그램 tooretrieve 효율적으로 이러한 값을 사용 하는 엔터티. 예를 들어, 아래에 표시 된 hello 테이블 구조를 사용 하는 클라이언트 응용 프로그램 צ ְ ײ 지점 쿼리 tooretrieve 개별 employee 엔터티 hello 부서 이름 및 hello 직원 id를 사용 하 여 (hello **PartitionKey** 및  **RowKey** 값). 또한 클라이언트는 각 부서 내에서 직원 ID별로 정렬된 엔터티를 검색할 수 있습니다.

![][6]

또한 toobe 수 toofind 전자 메일 주소 등의 다른 속성의 hello 값에 따라 employee 엔터티를 원하는 경우 효율성이 떨어지는 파티션 검색 toofind 일치 하는 항목을 사용 해야 합니다. Hello 테이블 서비스에서 보조 인덱스를 제공 하지 않기 때문입니다. 또한 없는 없습니다 옵션 toorequest 보다 다른 순서로 정렬 하는 직원의 목록이 **RowKey** 순서입니다.  

#### <a name="solution"></a>해결 방법
보조 인덱스의 부족 hello 주위 toowork, 각 엔터티와 다른를 사용 하 여 각 복사본의 여러 복사본을 저장할 수 있습니다 **RowKey** 값입니다. Hello 구조 아래에 표시 된 엔터티를 저장 하는 경우 전자 메일 주소 또는 직원 id에 따라 employee 엔터티를 효율적으로 검색할 수 있습니다. hello에 대 한 접두사 값 hello **RowKey**, "empid_" 및 "email_" 사용 하면 tooquery는 한 명의 직원과 또는 직원의 범위에 대 한 전자 메일 주소 또는 직원 id 범위를 사용 하 여 합니다.  

![][7]

지점 쿼리를 지정 둘 다 두 필터 조건 (하나를 조회 직원 id와 전자 메일 주소를 조회 하나)를 수행 하는 hello:  

* $filter=(PartitionKey eq 'Sales') and (RowKey eq 'empid_000223')  
* $filter=(PartitionKey eq 'Sales') and (RowKey eq 'email_jonesj@contoso.com')  

직원 id 순으로 정렬 된 범위 또는 hello hello에 적절 한 접두사가 포함 된 엔터티에 대 한 쿼리를 통해 전자 메일 주소 순서로 정렬 된 범위를 지정할 수 employee 엔터티 범위에 대 한 쿼리 하는 경우 **RowKey**합니다.  

* toofind hello 범위 000100 too000199의 직원 id와 hello 영업 부서에 모든 hello 직원 사용: $filter = (PartitionKey eq '판매') 및 (RowKey ge 'empid_000100') 및 (RowKey le 'empid_000199')  
* hello 영업 부서의 직원 hello로 시작 하는 전자 메일 주소와 hello 모든 toofind 문자 'a' 사용: $filter = (PartitionKey eq '판매') 및 (RowKey ge 'email_a') 및 (RowKey lt 'email_b')  
  
  위의 hello 예에 사용 되는 hello 필터 구문에 대 한 자세한 내용은 참조 하십시오 hello 테이블 서비스 REST API에서에서는 [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx)합니다.  

#### <a name="issues-and-considerations"></a>문제 및 고려 사항
Hello 지점을 결정할 때 다음 고려 어떻게 tooimplement이이 패턴:  

* 테이블 저장소 상대적으로 경제적인 toouse 이므로 중복 데이터를 저장할 경우의 오버 헤드 비용 hello 중요 한 문제가 되지 않습니다. 그러나 항상 예상 되는 저장소 요구 사항에 따라 디자인의 hello 비용을 평가 하 고만 중복 항목 toosupport hello 쿼리 실행 됩니다 클라이언트 응용 프로그램을 추가 해야 합니다.  
* Hello 보조 인덱스 엔터티 hello 원래 엔터티로 분할 동일 hello에 저장 되므로 개별 파티션에 대 한 hello 확장성 목표를 초과 하지 않는지 확인 해야 합니다.  
* 원자적으로 hello 엔터티의 EGTs tooupdate hello 두 복사본을 사용 하 여 중복 된 엔터티를 서로 일치 유지할 수 있습니다. 이 인해 hello에 엔터티의 모든 복사본 저장 해야 하는 동일한 파티션 합니다. 자세한 내용은 hello 섹션을 참조 하십시오. [엔터티 그룹 트랜잭션을 사용 하 여](#entity-group-transactions)합니다.  
* hello에 사용 되는 값을 hello **RowKey** 각 엔터티에 대해 고유 해야 합니다. 복합 키 값을 사용하는 것이 좋습니다.  
* 안쪽 여백 hello에 숫자 값 **RowKey** (예: hello 직원 id 000223) 하면 정렬 및 하한값과 상한값에 따라 필터링을 해결 합니다.  
* 반드시 불필요 tooduplicate 엔터티의 모든 hello 속성입니다. 예를 들어 경우 hello 쿼리 해당 hello를 사용 하 여 조회 hello 엔터티 전자 메일 주소를 hello에 **RowKey** 필요 hello 직원의 나이, 이러한 엔터티는 다음 구조 hello 있을 수 있습니다.

![][8]

* 일반적으로 더 나은 toostore 중복 데이터 사용 되며 모든 hello 필요한 데이터를 단일 쿼리를 검색할 수 있습니다, 엔터티 및 다른 toolookup hello 필요한 데이터 toouse 하나의 쿼리 toolocate 보다 있는지 확인 합니다.  

#### <a name="when-toouse-this-pattern"></a>때 toouse이이 패턴
이 패턴을 사용 하 여 클라이언트 응용 프로그램 클라이언트 tooretrieve 엔터티가 서로 다른 정렬 순서에 필요한 경우에 다양 한 서로 다른 키를 사용 하 여 tooretrieve 엔터티 있고 다양 한 고유 값을 사용 하 여 각 엔터티를 식별할 수 있습니다. 그러나 해야 다른 hello를 사용 하 여 엔터티 조회를 수행 하는 경우 hello 파티션 확장성 제한 초과 하지 않는 **RowKey** 값입니다.  

#### <a name="related-patterns-and-guidance"></a>관련 패턴 및 지침
hello 다음 패턴 및 지침은 수도 관련이 패턴을 구현 하는 경우.  

* [파티션 내 보조 인덱스 패턴](#inter-partition-secondary-index-pattern)
* [복합 키 패턴](#compound-key-pattern)
* [엔터티 그룹 트랜잭션](#entity-group-transactions)
* [유형이 다른 엔터티 유형 작업](#working-with-heterogeneous-entity-types)

### <a name="inter-partition-secondary-index-pattern"></a>파티션 간 보조 인덱스 패턴
복사본을 여러 개 사용 하 여 각 엔터티 다른 저장 **RowKey** 별도 파티션을 또는 별도 테이블 tooenable 신속 하 고 효율적인 조회 및 다른을 사용 하 여 대체 정렬 순서 값 **RowKey**값입니다.  

#### <a name="context-and-problem"></a>컨텍스트 및 문제점
테이블 서비스 hello hello를 사용 하 여 엔터티를 자동으로 인덱싱됩니다 **PartitionKey** 및 **RowKey** 값입니다. 이렇게 하면 클라이언트 응용 프로그램 tooretrieve 효율적으로 이러한 값을 사용 하는 엔터티. 예를 들어, 아래에 표시 된 hello 테이블 구조를 사용 하는 클라이언트 응용 프로그램 צ ְ ײ 지점 쿼리 tooretrieve 개별 employee 엔터티 hello 부서 이름 및 hello 직원 id를 사용 하 여 (hello **PartitionKey** 및  **RowKey** 값). 또한 클라이언트는 각 부서 내에서 직원 ID별로 정렬된 엔터티를 검색할 수 있습니다.  

![][9]

또한 toobe 수 toofind 전자 메일 주소 등의 다른 속성의 hello 값에 따라 employee 엔터티를 원하는 경우 효율성이 떨어지는 파티션 검색 toofind 일치 하는 항목을 사용 해야 합니다. Hello 테이블 서비스에서 보조 인덱스를 제공 하지 않기 때문입니다. 또한 없는 없습니다 옵션 toorequest 보다 다른 순서로 정렬 하는 직원의 목록이 **RowKey** 순서입니다.  

이러한 엔터티에 대 한 트랜잭션 매우 큰 용량의 예측은 때 toominimize hello 위험이 hello 테이블 서비스 클라이언트를 제한 합니다.  

#### <a name="solution"></a>해결 방법
보조 인덱스의 부족 hello 주위 toowork, 복사본을 여러 개 사용 하 여 각 복사본에 있는 각 엔터티를 다른 저장할 수 있습니다 **PartitionKey** 및 **RowKey** 값입니다. Hello 구조 아래에 표시 된 엔터티를 저장 하는 경우 전자 메일 주소 또는 직원 id에 따라 employee 엔터티를 효율적으로 검색할 수 있습니다. hello에 대 한 접두사 값 hello **PartitionKey**, "empid_" 및 "email_"를 사용 하면 인덱싱할 있습니다 tooidentify 쿼리에 대 한 toouse 원하는 합니다.  

![][10]

지점 쿼리를 지정 둘 다 두 필터 조건 (하나를 조회 직원 id와 전자 메일 주소를 조회 하나)를 수행 하는 hello:  

* $filter=(PartitionKey eq 'empid_Sales') and (RowKey eq '000223')
* $filter=(PartitionKey eq 'email_Sales') and (RowKey eq 'jonesj@contoso.com')  

직원 id 순으로 정렬 된 범위 또는 hello hello에 적절 한 접두사가 포함 된 엔터티에 대 한 쿼리를 통해 전자 메일 주소 순서로 정렬 된 범위를 지정할 수 employee 엔터티 범위에 대 한 쿼리 하는 경우 **RowKey**합니다.  

* 모든 hello에 직원 toofind hello 영업부 hello 범위의 직원 id와 **000100** 너무**000199** 직원 id 순서 사용에서 정렬: $filter = (PartitionKey eq ' empid_Sales') 및 (RowKey ge ' 000100') 및 (RowKey le '000199')  
* toofind에 정렬 된 'a'로 시작 하는 메일 주소로 hello 영업 부서에 모든 hello 직원 전자 메일 주소 순서 사용: $filter = (PartitionKey eq ' email_Sales') 및 (RowKey ge 'a') 및 (RowKey lt 'b')  

위의 hello 예에 사용 되는 hello 필터 구문에 대 한 자세한 내용은 참조 하십시오 hello 테이블 서비스 REST API에서에서는 [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx)합니다.  

#### <a name="issues-and-considerations"></a>문제 및 고려 사항
Hello 지점을 결정할 때 다음 고려 어떻게 tooimplement이이 패턴:  

* 유지할 수 있습니다 중복 엔터티가 서로 일치 결국 hello를 사용 하 여 [결국 일관 된 트랜잭션 패턴](#eventually-consistent-transactions-pattern) toomaintain hello 기본 및 보조 인덱스 엔터티.  
* 테이블 저장소 상대적으로 경제적인 toouse 이므로 중복 데이터를 저장할 경우의 오버 헤드 비용 hello 중요 한 문제가 되지 않습니다. 그러나 항상 예상 되는 저장소 요구 사항에 따라 디자인의 hello 비용을 평가 하 고만 중복 항목 toosupport hello 쿼리 실행 됩니다 클라이언트 응용 프로그램을 추가 해야 합니다.  
* hello에 사용 되는 값을 hello **RowKey** 각 엔터티에 대해 고유 해야 합니다. 복합 키 값을 사용하는 것이 좋습니다.  
* 안쪽 여백 hello에 숫자 값 **RowKey** (예: hello 직원 id 000223) 하면 정렬 및 하한값과 상한값에 따라 필터링을 해결 합니다.  
* 반드시 불필요 tooduplicate 엔터티의 모든 hello 속성입니다. 예를 들어 경우 hello 쿼리 해당 hello를 사용 하 여 조회 hello 엔터티 전자 메일 주소를 hello에 **RowKey** 필요 hello 직원의 나이, 이러한 엔터티는 다음 구조 hello 있을 수 있습니다.
  
  ![][11]
* 일반적으로 toostore 중복 데이터를 보다 잘 하 고 사용 하 여 엔터티 toouse 하나의 쿼리 toolocate hello 보조 인덱스 보다는 단일 쿼리로 필요한 모든 hello 데이터를 검색할 수 있는 확인 및 다른 toolookup hello hello 기본 인덱스에 필요한 데이터.  

#### <a name="when-toouse-this-pattern"></a>때 toouse이이 패턴
이 패턴을 사용 하 여 클라이언트 응용 프로그램 클라이언트 tooretrieve 엔터티가 서로 다른 정렬 순서에 필요한 경우에 다양 한 서로 다른 키를 사용 하 여 tooretrieve 엔터티 있고 다양 한 고유 값을 사용 하 여 각 엔터티를 식별할 수 있습니다. 다른 hello를 사용 하 여 엔터티 조회를 수행 하는 경우 hello 파티션 확장성 제한을 초과 tooavoid 하려는 경우이 패턴을 사용 하 여 **RowKey** 값입니다.  

#### <a name="related-patterns-and-guidance"></a>관련 패턴 및 지침
hello 다음 패턴 및 지침은 수도 관련이 패턴을 구현 하는 경우.  

* [결과적으로 일관성 있는 트랜잭션 패턴](#eventually-consistent-transactions-pattern)  
* [파티션 간 보조 인덱스 패턴](#intra-partition-secondary-index-pattern)  
* [복합 키 패턴](#compound-key-pattern)  
* [엔터티 그룹 트랜잭션](#entity-group-transactions)  
* [유형이 다른 엔터티 유형 작업](#working-with-heterogeneous-entity-types)  

### <a name="eventually-consistent-transactions-pattern"></a>결과적으로 일관성 있는 트랜잭션 패턴
Azure 큐를 사용하여 파티션 경계 또는 저장소 시스템 경계 간에 결과적으로 일관성 있는 동작을 지원합니다.  

#### <a name="context-and-problem"></a>컨텍스트 및 문제점
EGTs hello를 공유 하는 여러 엔터티 간에 원자성 트랜잭션을 사용 동일한 파티션 키입니다. 성능 및 확장성 때문에 대 한 별도 파티션을 또는 별도 저장소 시스템 일관성 요구 사항이 있는 toostore 엔터티를 결정할 수 있습니다: 이러한 시나리오에서는 EGTs toomaintain 일관성을 사용할 수 없습니다. 예를 들어 간의 요구 사항 toomaintain 결과적 일관성을 할 수 있습니다.  

* 동일한 테이블을 서로 다른 테이블의 다른 저장소 계정에서 hello에 두 개의 서로 다른 파티션에 저장 된 엔터티.  
* Hello 테이블 서비스에에서 저장 된 엔터티 및 hello Blob 서비스에에서 저장 된 blob입니다.  
* 파일 시스템의 hello 테이블 서비스 및 파일에 저장 하는 엔터티.  
* 엔터티는 hello 테이블 서비스에에서 저장 하면서 hello Azure 검색 서비스를 사용 하 여 인덱싱됩니다.  

#### <a name="solution"></a>해결 방법
Azure 큐를 사용하면 둘 이상의 파티션 또는 저장소 시스템 간에 결과적 일관성을 유지하는 솔루션을 구현할 수 있습니다.
tooillustrate 접근이 요구 사항 toobe 수 tooarchive 이전 employee 엔터티를 있다고 가정 합니다. 이전 직원 엔터티는 거의 쿼리되지 않으므로 현재 직원을 다루는 활동에서 제외해야 합니다. tooimplement hello에 근무 중인 직원을 저장 하는이 요구 사항을 **현재** 테이블과 hello에 오래 된 직원 **보관** 테이블입니다. 직원을 보관 해야 toodelete hello 엔터티로서 hello **현재** 테이블 및 엔터티 toohello hello 추가 **보관** 수 있지만 테이블을 사용할 수 없습니다 EGT tooperform 두 가지 동작 합니다. 오류가 모두 또는 두 테이블에 엔터티 tooappear를 하면 tooavoid hello 위험 hello 보관 작업 결국 일치 해야 합니다. hello 시퀀스 다이어그램을 다음 단계를 간략하게 설명 hello이이 작업에 있습니다. 자세한 내용은 예외 경로 hello 텍스트 다음에 대해 제공 됩니다.  

![][12]

클라이언트에서이 예제에서는 tooarchive 직원 #456 Azure 큐에서 메시지를 배치 하 여 hello 보관 작업을 시작 합니다. 작업자 역할 새 메시지;에 대 한 hello 큐를 폴링합니다. 를 찾으면 hello 메시지 읽고 hello 큐에서 숨겨진된 복사본을 전송 합니다. hello 작업자 역할 hello에서 hello 엔터티의 복사본을 다음 인출 **현재** hello에 복사본을 삽입, 테이블 **보관** 테이블 및 hello에서 원래 삭제 hello **현재**테이블입니다. 마지막으로, hello 이전 단계에서 오류가 발생 하지 인 경우 hello 작업자 역할 hello 큐에서 숨겨진된 hello 메시지를 삭제 합니다.  

이 예제에서는 4 단계 삽입 hello 직원 hello **보관** 테이블입니다. 파일 시스템에 hello Blob 서비스에에서 hello 직원 tooa blob 또는 파일을 표시할 수 있습니다.  

#### <a name="recovering-from-failures"></a>오류 복구
것이 중요 단계에서 작업 하는 hello **4** 및 **5** 해야 *idempotent* hello 작업자 역할 toorestart hello 보관 작업에 필요한 경우. 단계에 대 한 hello 테이블 서비스를 사용 하는 경우 **4** "삽입 또는 교체" 작업을 사용 해야; 단계에 대 한 **5** 사용할지는 "경우 삭제 존재" 작업을 사용 하는 hello 클라이언트 라이브러리에서. 다른 저장소 시스템을 사용하는 경우에는 적절한 idempotent 작업을 사용해야 합니다.  

Hello 작업자 역할 절대 단계를 완료 하는 경우 **6**, 후 시간 초과 hello 메시지 hello 큐에 다시 나타납니다. 후 작업자 역할 tootry tooreprocess hello에 대 한 해 준비 합니다. hello 작업자 역할 hello 큐에 메시지를 읽은 횟수를 확인할 수 있습니다 및 플래그 tooa 전송 하 여 조사를 위해 "포이즌" 메시지를은 큐 구분 필요한 경우. 큐에서 제거한 횟수 큐의 메시지를 읽고 hello를 검사 하는 방법에 대 한 자세한 내용은 참조 하십시오. [Get 메시지](https://msdn.microsoft.com/library/azure/dd179474.aspx)합니다.  

Hello 테이블 및 큐 서비스에서 일부 오류는 일시적인 오류 및 클라이언트 응용 프로그램에 적합 한 다시 시도 논리 toohandle 포함 되어야 하 합니다.  

#### <a name="issues-and-considerations"></a>문제 및 고려 사항
Hello 지점을 결정할 때 다음 고려 어떻게 tooimplement이이 패턴:  

* 이 솔루션은 트랜잭션 격리를 제공하지 않습니다. 클라이언트 hello를 읽을 수는 예를 들어 **현재** 및 **보관** hello 작업자 역할이 단계 사이의 되었을 때 테이블 **4** 및 **5**, 참조 및 프로그램 hello 데이터의 일관성 없는 뷰. Hello 데이터가 될 것 이라는 일관 된 결국 참고 합니다.  
* 4-5 단계에서 순서 tooensure 결과적 일관성 idempotent 인지 확인 해야 합니다.  
* 여러 큐 및 작업자 역할 인스턴스를 사용 하 여 hello 솔루션을 확장할 수 있습니다.  

#### <a name="when-toouse-this-pattern"></a>때 toouse이이 패턴
여러 파티션 또는 테이블에 존재 하는 엔터티 간의 결과적 일관성 tooguarantee 하려는 경우이 패턴을 사용 합니다. Hello 테이블 서비스 및 hello Blob 서비스 및 기타 비 Azure 저장소 데이터 원본 데이터베이스 또는 hello 파일 시스템 등에서 작업에 대 한이 패턴 tooensure 결과적 일관성을 확장할 수 있습니다.  

#### <a name="related-patterns-and-guidance"></a>관련 패턴 및 지침
hello 다음 패턴 및 지침은 수도 관련이 패턴을 구현 하는 경우.  

* [엔터티 그룹 트랜잭션](#entity-group-transactions)  
* [병합 또는 바꾸기](#merge-or-replace)  

> [!NOTE]
> 트랜잭션 격리는 중요 한 tooyour 솔루션을 하는 경우 테이블 tooenable 다시 디자인 고려해 야 toouse EGTs 있습니다.  
> 
> 

### <a name="index-entities-pattern"></a>인덱스 엔터티 패턴
인덱스 엔터티 tooenable 효율적인 검색 엔터티 목록을 반환 하는 유지 관리 합니다.  

#### <a name="context-and-problem"></a>컨텍스트 및 문제점
테이블 서비스 hello hello를 사용 하 여 엔터티를 자동으로 인덱싱됩니다 **PartitionKey** 및 **RowKey** 값입니다. 이렇게 하면 클라이언트 응용 프로그램 tooretrieve를 효율적으로 지점 쿼리를 사용 하는 엔터티 수 있습니다. 예를 들어 아래에 표시 된 hello 테이블 구조를 사용 하 여 클라이언트 응용 프로그램이 효율적으로 검색할 수 개별 employee 엔터티 hello 부서 이름 및 hello 직원 id를 사용 하 여 (hello **PartitionKey** 및 **RowKey** ).  

![][13]

싶다면의 employee 엔터티 목록을 성, 등의 다른 고유 하지 않은 속성의 hello 값에 따라 toobe 수 tooretrieve 효율성이 떨어지는 파티션을 사용 해야 인덱스 toolook를 사용 하지 않고 스캔 toofind 일치 항목을 직접 위로 합니다. Hello 테이블 서비스에서 보조 인덱스를 제공 하지 않기 때문입니다.  

#### <a name="solution"></a>해결 방법
위에 표시 된 직원 id 목록을 유지 관리 해야 하는 hello 엔터티 구조와 성 기준으로 tooenable 조회 합니다. Jones, 같은 특정 마지막 이름의 tooretrieve hello employee 엔터티를 원하는 경우에 먼저 성,으로 jones 이면 특정 인 직원에 대 한 hello 목록을 직원 id를 찾을 하 고 employee 엔터티를 검색 해야 합니다. Hello 목록이 직원 id 저장 하기 위한 세 가지 옵션에는  

* Blob 저장소 사용  
* 동일한 hello employee 엔터티를 분할 하는 hello에 인덱스 엔터티를 만듭니다.  
* 별도의 파티션 또는 테이블에 인덱스 엔터티 만들기  

<u>옵션 #1: Blob 저장소 사용</u>  

Hello 첫 번째 옵션에 대 한 모든 고유한 성 및 각 blob 저장소에 blob 목록을 만들면의 hello **PartitionKey** (부서) 및 **RowKey** 된 마지막는 직원에 대 한 값 (직원 id) 이름입니다. 추가 하거나 해당 직원을 삭제할 때 hello 관련 blob의 hello 콘텐츠가 결국 hello employee 엔터티와 일치 하는지 확인 해야 합니다.  

<u>옵션 2:</u> 에서 Create index 엔터티 hello 같은 파티션  

Hello 두 번째 옵션에 대 한 hello 다음 데이터를 저장 하는 인덱스 엔터티를 사용 합니다.  

![][14]

hello **EmployeeIDs** 속성 hello 성 hello에 저장 된 직원에 대 한 직원 id 목록이 포함 **RowKey**합니다.  

hello 다음 단계에 간략하게 설명 hello 프로세스 hello 두 번째 옵션을 사용 하는 경우 새 직원을 추가 하는 경우 따라야 합니다. 이 예제에서는 Id 000152 및 성 jones 이면 특정 hello 영업 부서의 직원을 추가 됩니다.  

1. Hello 인덱스 엔터티를 검색 한 **PartitionKey** 값 "Sales" 및 hello **RowKey** "Jones" 값 2 단계에서 hello이 엔터티 toouse의 ETag를 저장 합니다.  
2. Hello 새 employee 엔터티를 삽입 하는 엔터티 그룹 트랜잭션은 (즉, 일괄 처리 작업)을 만듭니다 (**PartitionKey** "Sales" 값 및 **RowKey** "000152" 값), 업데이트 인덱스 엔터티 (hello및 **PartitionKey** "Sales" 값 및 **RowKey** "jones 이면 특정" 값) hello 새 직원 id toohello 목록 hello EmployeeIDs 필드에 추가 하 여 합니다. 엔터티 그룹 트랜잭션에 대한 자세한 내용은 [엔터티 그룹 트랜잭션](#entity-group-transactions)을 참조하세요.  
3. (다른 사용자가 방금 수정한 hello 인덱스 엔터티)는 낙관적 동시성 오류 때문에 실패 하면 hello 엔터티 그룹 트랜잭션은 해야 toostart 통해 1 단계부터 다시.  

Hello 두 번째 옵션을 사용 하는 경우 비슷한 접근 방식을 toodeleting 직원을 사용할 수 있습니다. 직원의 성을 변경은 세 개의 엔터티를 업데이트 하는 엔터티 그룹 트랜잭션은 tooexecute 필요 하므로 약간 더 복잡 한: hello employee 엔터티, 이전 마지막 이름 hello에 대 한 hello 인덱스 엔터티 및 hello 새 마지막 이름에 대 한 hello 인덱스 엔터티. 그런 다음 낙관적 동시성을 사용 하 여 tooperform hello 업데이트를 사용할 수 있는 tooretrieve hello ETag 값 순서로 변경 하기 전에 각 엔터티를 검색 해야 합니다.  

hello 다음 단계에 간략하게 설명 hello 프로세스 hello 두 번째 옵션을 사용 하는 경우 toolook 부서에서 특정된 성 가진 모든 직원으로 hello 해야 하는 경우 따라야 합니다. 이 예제에서는 hello 영업부에서 jones 이면 특정 이름 가진 모든 직원으로 hello 찾고:  

1. Hello 인덱스 엔터티를 검색 한 **PartitionKey** 값 "Sales" 및 hello **RowKey** "Jones" 값  
2. Hello 목록이 직원 hello EmployeeIDs 필드의 Id 구문 분석 합니다.  
3. (예:가 전자 메일 주소) 이러한 직원 들의 각각에 대 한 추가 정보를 검색 hello employee 엔터티를 사용 하 여 각 **PartitionKey** "Sales" 값 및 **RowKey** 에서 값 2 단계에서 얻은 직원의 hello 목록입니다.  

<u>옵션 3:</u> 별도의 파티션 또는 테이블에 인덱스 엔터티 만들기  

Hello 세 번째 옵션에 대 한 hello 다음 데이터를 저장 하는 인덱스 엔터티를 사용 합니다.  

![][15]

hello **EmployeeIDs** 속성 hello 성 hello에 저장 된 직원에 대 한 직원 id 목록이 포함 **RowKey**합니다.  

Hello 세 번째 옵션을 사용 하므로 hello employee 엔터티를를 별도 파티션으로 hello 인덱스 엔터티는 EGTs toomaintain 일관성을 사용할 수 없습니다. Hello 인덱스 엔터티는 결국 hello employee 엔터티와 일치 해야 합니다.  

#### <a name="issues-and-considerations"></a>문제 및 고려 사항
Hello 지점을 결정할 때 다음 고려 어떻게 tooimplement이이 패턴:  

* 이 솔루션에 필요한 엔터티를 일치 하는 두 개 이상의 쿼리 tooretrieve: tooquery hello 인덱스 엔터티 tooobtain hello 목록은 한 **RowKey** 값, 및 다음 tooretrieve hello 목록에서 각 엔터티를 쿼리 합니다.  
* 개별 엔터티에 최대 크기는 1MB 옵션 #2 개이고 옵션 #3 hello 솔루션의 가정 해당 hello 목록이 있다고 지정된 성에 대 한 직원 id 되지 보다 큰 경우 1MB 직원 id 목록은 hello 가능성이 toobe 크기가 1MB 보다 클 경우 #1 옵션을 사용 하 고 blob 저장소에 hello 인덱스 데이터를 저장 합니다.  
* 옵션 2를 사용 하는 경우 (EGTs toohandle 추가 하 고 직원, 삭제와 직원의 성을 변경 사용) 해야 지 평가할 수 트랜잭션 양이 hello는 지정한 파티션에서 hello 확장성 제한에 가까워집니다. Hello 대/소문자 이면 큐 toohandle hello 업데이트를 사용 하는 결국 일관 된 솔루션 (#1 옵션이 나 옵션 3) 요청 하 고 있습니다 toostore hello employee 엔터티를를 별도 파티션으로 인덱스 엔터티 수를 고려해 야 합니다.  
* 이 솔루션에서는 옵션 #2 한다고 가정 toolook를는 부서 내 성을 기준으로: tooretrieve hello 판매 부서의 성이 jones 이면 특정 직원의 목록을 원하는 예를 들어 있습니다. 성 jones 이면 특정 hello 전체 조직 전체에서 가진 모든 직원으로 hello toobe 수 toolook #1 옵션이 나 옵션 # 3을 사용 합니다.
* 결과적 일관성을 제공 하는 큐 기반 솔루션을 구현할 수 있습니다 (hello 참조 [결국 일관 된 트랜잭션 패턴](#eventually-consistent-transactions-pattern) 자세한 세부 정보에 대 한).  

#### <a name="when-toouse-this-pattern"></a>때 toouse이이 패턴
Toolookup hello 성 jones 이면 특정 가진 모든 직원 등 공통 속성 값을 공유 하는 엔터티 집합을 원하는 경우이 패턴을 사용 합니다.  

#### <a name="related-patterns-and-guidance"></a>관련 패턴 및 지침
hello 다음 패턴 및 지침은 수도 관련이 패턴을 구현 하는 경우.  

* [복합 키 패턴](#compound-key-pattern)  
* [결과적으로 일관성 있는 트랜잭션 패턴](#eventually-consistent-transactions-pattern)  
* [엔터티 그룹 트랜잭션](#entity-group-transactions)  
* [유형이 다른 엔터티 유형 작업](#working-with-heterogeneous-entity-types)  

### <a name="denormalization-pattern"></a>비정규화 패턴
단일 엔터티 tooenable에서 함께 관련된 데이터를 결합 tooretrieve 모든 hello 필요한 데이터를 단일 지점 쿼리를 사용 합니다.  

#### <a name="context-and-problem"></a>컨텍스트 및 문제점
관계형 데이터베이스에 일반적으로 데이터 tooremove 중복 여러 테이블에서 데이터를 검색 하는 쿼리에서 결과 정규화 합니다. Azure 테이블에 데이터를 표준화 하는 경우에 관련된 데이터를 여러 번 왕복 hello 클라이언트 toohello 서버 tooretrieve에서 확인 해야 합니다. 예를 들어 아래 표시 된 hello 테이블 구조와 필요한 두 라운드 트립을 tooretrieve hello 세부 정보는 부서에 대 한: 직원에 hello 관리자의 id와 다른 요청 toofetch hello 관리자의 세부 정보를 포함 하는 하나의 toofetch hello department 엔터티 엔터티입니다.  

![][16]

#### <a name="solution"></a>해결 방법
두 개의 개별 엔터티인에 hello 데이터를 저장 하는 대신 hello 데이터를 비 정규화 하 고 hello 부서 엔터티에 hello 관리자의 세부 정보의 복사본을 보관 합니다. 예:  

![][17]

이러한 속성으로 저장 된 부서 엔터티에 이제 지점 쿼리를 사용 하 여 부서에 대해 필요한 모든 hello 세부 정보를 검색할 수 있습니다.  

#### <a name="issues-and-considerations"></a>문제 및 고려 사항
Hello 지점을 결정할 때 다음 고려 어떻게 tooimplement이이 패턴:  

* 일부 데이터를 두 번 저장하는 것과 관련된 약간의 비용 오버헤드가 있습니다. hello 성능 (더 적은 요청 toohello 저장소 서비스에서 발생 함) 일반적으로 능가 이점이 hello 한계 저장소 비용이 증가 (이 비용은 부분적으로 오프셋 되 고 hello 트랜잭션 수가 감소 하 여 필요한 toofetch hello 세부 정보 부서).  
* 관리자에 대 한 정보를 저장 하는 두 개의 엔터티를 hello hello 일관성을 유지 해야 합니다. 단일 원자성 트랜잭션 내에서 여러 엔터티 EGTs tooupdate를 사용 하 여 hello 일관성 문제를 처리할 수 있습니다: hello department 엔터티 및 hello 부서 관리자에 대 한 hello employee 엔터티에 hello에 저장 됩니다는 경우 같은 파티션 합니다.  

#### <a name="when-toouse-this-pattern"></a>때 toouse이이 패턴
관련된 정보를 toolook를 자주 할 경우이 패턴을 사용 합니다. 이 패턴 hello 클라이언트에 필요한 tooretrieve hello 데이터를 확인 해야 하는 쿼리 수를 줄입니다.  

#### <a name="related-patterns-and-guidance"></a>관련 패턴 및 지침
hello 다음 패턴 및 지침은 수도 관련이 패턴을 구현 하는 경우.  

* [복합 키 패턴](#compound-key-pattern)  
* [엔터티 그룹 트랜잭션](#entity-group-transactions)  
* [유형이 다른 엔터티 유형 작업](#working-with-heterogeneous-entity-types)

### <a name="compound-key-pattern"></a>복합 키 패턴
사용 하 여 복합 **RowKey** 값 tooenable 클라이언트 toolookup 관련 데이터는 단일 지점에서 쿼리를 사용 합니다.  

#### <a name="context-and-problem"></a>컨텍스트 및 문제점
쿼리에서 매우 체계적 toouse 조인은 것이 관계형 데이터베이스 tooreturn 관련 단일 쿼리에서 데이터 toohello 클라이언트의 부분입니다. 예를 들어 hello 직원 id toolook 성능 포함 및 해당 직원에 대 한 데이터를 검토 하는 관련 엔터티 그룹을 사용할 수 있습니다.  

Employee 엔터티를 저장 하는 구조를 다음 hello를 사용 하 여 hello 테이블 서비스에 있다고 가정 합니다.  

![][18]

Tooreviews 관련 toostore 기록 데이터를 제공 해야 하 고 조직에 대 한 각 연도의 hello 직원에 대 한 성능 한 적이 toobe 수 tooaccess 연도별이 정보가 필요 합니다. 한 가지 옵션은 toocreate 구조를 다음 hello로 엔터티를 저장 하는 다른 테이블:  

![][19]

이 방법에 tooduplicate hello 새 엔터티 tooenable의 일부 정보 (예: 이름 및 성) 결정할 수 있습니다 tooretrieve 단일 요청으로 데이터입니다. 그러나 원자 단위로 EGT tooupdate hello 두 엔터티를 사용할 수 없으므로 강력한 일관성을 유지할 수 없습니다.  

#### <a name="solution"></a>해결 방법
새 엔터티 형식이 구조를 다음 hello로 엔터티를 사용 하 여 원본 테이블에 저장:  

![][20]

Hello 어떻게 확인 **RowKey** 이제의 복합 키 이루어져 hello 직원 id와 수 있는 hello 검토 데이터의 hello 연도 tooretrieve 직원의 성과 hello 및 단일 엔터티에 대 한 단일 요청으로 데이터를 검토 합니다.  

다음 예제는 hello (예: 000123 hello 영업 부서의 직원) 특정 직원에 대 한 모든 hello 검토 데이터를 검색 하는 방법을 설명 합니다.  

$filter=(PartitionKey eq 'Sales') and (RowKey ge 'empid_000123') and (RowKey lt 'empid_000124')&$select=RowKey,Manager Rating,Peer Rating,Comments  

#### <a name="issues-and-considerations"></a>문제 및 고려 사항
Hello 지점을 결정할 때 다음 고려 어떻게 tooimplement이이 패턴:  

* 쉽게 tooparse hello 있는 적합 한 구분 기호를 사용 해야 **RowKey** 값: 예를 들어 **000123_2012**합니다.  
* Hello에 대 한 관련된 데이터를 포함 하는 다른 엔터티로 분할 동일 hello에이 엔터티를 저장할도 동일한 직원 이기 EGTs toomaintain 강력한 일관성을 사용할 수 있습니다.
* 이 패턴 적절 한지 여부를 hello 데이터 toodetermine을 쿼리 하는 빈도 고려해 야 합니다.  예를 들어 액세스 하는 경우 자주 검토 데이터 hello 및 hello 주 직원 데이터 종종 별도 엔터티로 유지 해야 합니다.  

#### <a name="when-toouse-this-pattern"></a>때 toouse이이 패턴
이 패턴을 사용 하 여 하나 toostore 하거나 이상의 관련 엔터티 쿼리 하는 경우가 많습니다.  

#### <a name="related-patterns-and-guidance"></a>관련 패턴 및 지침
hello 다음 패턴 및 지침은 수도 관련이 패턴을 구현 하는 경우.  

* [엔터티 그룹 트랜잭션](#entity-group-transactions)  
* [유형이 다른 엔터티 유형 작업](#working-with-heterogeneous-entity-types)  
* [결과적으로 일관성 있는 트랜잭션 패턴](#eventually-consistent-transactions-pattern)  

### <a name="log-tail-pattern"></a>로그 테일 패턴
Hello 검색  *n*  엔터티 가장 최근에 추가 된 tooa 파티션을 사용 하 여 한 **RowKey** 역방향 날짜와 시간 순서에 정렬 하는 값입니다.  

#### <a name="context-and-problem"></a>컨텍스트 및 문제점
일반적인 요구 사항은 엔터티일 수 tooretrieve 가장 최근에 만든 hello, 예를 들어 hello 10 개의 가장 최근 비용 청구서 직원 제출한입니다. 테이블 쿼리 지원은 **$top** 작업 tooreturn hello를 먼저 쿼리  *n*  집합에서 엔터티에: 없는 해당 하는 쿼리 작업 tooreturn hello 마지막 n 개 엔터티 집합에는 합니다.  

#### <a name="solution"></a>해결 방법
사용 하 여 저장소 hello 엔터티는 **RowKey** 는 자연스럽 게 반대 방향으로 정렬 합니다. 날짜/시간 순서 있으므로 hello 가장 최근 항목은 항상 hello를 사용 하 여 hello 테이블의 첫 번째입니다.  

예를 들어 toobe 수 tooretrieve hello 직원 제출한 10 개의 가장 최근 비용 청구서, 현재 날짜/시간 hello에서 파생 된 역방향 눈금 값을 사용할 수 있습니다. hello 다음 C# 보여 주는 코드 예제는 한 가지 방법은 toocreate에 대 한 적합 한 "틱 반전" 값은 **RowKey** 가장 오래 된 가장 최근 toohello hello에서에서 정렬 하 합니다.  

`string invertedTicks = string.Format("{0:D19}", DateTime.MaxValue.Ticks - DateTime.UtcNow.Ticks);`  

Toohello 날짜/시간 값 코드 다음 hello를 사용 하 여 다시 가져올 수 있습니다.  

`DateTime dt = new DateTime(DateTime.MaxValue.Ticks - Int64.Parse(invertedTicks));`  

hello 테이블 쿼리는 다음과 같습니다.  

`https://myaccount.table.core.windows.net/EmployeeExpense(PartitionKey='empid')?$top=10`  

#### <a name="issues-and-considerations"></a>문제 및 고려 사항
Hello 지점을 결정할 때 다음 고려 어떻게 tooimplement이이 패턴:  

* Hello 역방향 틱 값 앞에 오는 0으로 채움 해야 예상 대로 tooensure hello 문자열 값을 정렬 합니다.  
* Hello 확장성 목표는 파티션의 hello 수준에서 인식 해야 합니다. 핫스폿 파티션을 만들지 않도록 주의하세요.  

#### <a name="when-toouse-this-pattern"></a>때 toouse이이 패턴
역방향 날짜/시간 순서로 tooaccess 엔터티 필요 하거나 최근에 tooaccess hello 사용 해야 하는 경우이 패턴을 사용 하 여 엔터티를 추가 합니다.  

#### <a name="related-patterns-and-guidance"></a>관련 패턴 및 지침
hello 다음 패턴 및 지침은 수도 관련이 패턴을 구현 하는 경우.  

* [앞/뒤에 추가된 안티패턴](#prepend-append-anti-pattern)  
* [엔터티 검색](#retrieving-entities)  

### <a name="high-volume-delete-pattern"></a>대용량 삭제 패턴
동시 삭제에 대 한 모든 hello 엔터티 자체 별도 테이블에 저장 하 여 많은 양의 엔터티 hello 삭제 사용 hello 테이블을 삭제 하 여 hello 엔터티를 삭제 합니다.  

#### <a name="context-and-problem"></a>컨텍스트 및 문제점
많은 응용 프로그램이 더 이상 필요 없는 toobe tooa 사용할 수 있는 클라이언트 응용 프로그램에는 기존 데이터를 삭제 하거나 해당 hello 응용 프로그램은 tooanother 저장 미디어를 보관 합니다. 일반적으로 날짜까지 이러한 데이터를 식별: 예를 들어 60 일 이상 있는 모든 로그인 요청이의 요구 사항 toodelete 레코드 해야 합니다.  

Toouse hello 날짜 및 시간 hello 로그인 요청 hello에 대 한 가능한 디자인은 **RowKey**:  

![][21]

이 방법은 hello 응용 프로그램을 삽입 및 삭제를 별도 파티션으로 각 사용자에 대 한 로그인 엔터티 때문에 파티션 핫스폿에 방지할 수 있습니다. 그러나이 방법은 많이 사용 될 수 있습니다 및 tooperform 먼저 때문에 많은 수의 엔터티가 있는 경우 시간이 오래 걸릴 table scan 순서 tooidentify에 모든 hello 엔터티 toodelete 않으며 각 이전 엔터티를 삭제 해야 합니다. 참고 EGTs에 여러 개의 삭제 요청을 일괄 처리 하 여 hello 왕복 toohello 필요한 서버 toodelete hello 이전 엔터티 수를 줄일 수 있습니다.  

#### <a name="solution"></a>해결 방법
각 로그인 시도 날짜에 별도의 테이블을 사용합니다. 엔터티를 삽입 하는 고 단순히 매일 한 테이블을 삭제할 경우의 질문은 기존 엔터티를 삭제 하는 경우 tooavoid 핫스폿에 위에 hello 엔터티 디자인을 사용할 수 있습니다 (단일 저장소 작업) 대신 찾기 및 수많은 삭제 개별 로그인 엔터티 매일입니다.  

#### <a name="issues-and-considerations"></a>문제 및 고려 사항
Hello 지점을 결정할 때 다음 고려 어떻게 tooimplement이이 패턴:  

* 디자인에 응용 프로그램은 특정 엔터티를 다른 데이터 또는 생성 한 집계 정보를 사용 하 여 링크를 검색 하는 등 hello 데이터를 사용 하 여 다른 방법을 지원 합니까?  
* 디자인이 새 엔터티를 삽입할 때 핫스폿을 방지하나요?  
* 동일한 tooreuse를 원하는 경우 지연 hello 예상 삭제 한 후 테이블 이름입니다. 것이 더 나은 tooalways 고유한 테이블 이름을 사용 합니다.  
* Hello 테이블 서비스는 hello 액세스 패턴 및 노드에 hello 파티션을 배포 하는 동안 새 테이블을 처음 사용할 때의 몇 가지 제한 있기만 하면 됩니다. Toocreate 새 테이블이 필요 얼마나 자주 하는 것이 좋습니다.  

#### <a name="when-toouse-this-pattern"></a>때 toouse이이 패턴
많은 양의 hello에서 삭제 해야 하는 엔터티 있는 경우이 패턴을 사용 같은 시간입니다.  

#### <a name="related-patterns-and-guidance"></a>관련 패턴 및 지침
hello 다음 패턴 및 지침은 수도 관련이 패턴을 구현 하는 경우.  

* [엔터티 그룹 트랜잭션](#entity-group-transactions)
* [엔터티 수정](#modifying-entities)  

### <a name="data-series-pattern"></a>데이터 계열 패턴
저장소 전체 데이터 계열에는 단일 엔터티 toominimize hello 수가 요청 합니다.  

#### <a name="context-and-problem"></a>컨텍스트 및 문제점
응용 프로그램 toostore 일련의 데이터는 일반적으로 필요 tooretrieve 한 번에 모두 일반적인 시나리오가입니다. 예를 들어 응용 프로그램에 각 직원 1 시간 마다 보냅니다 IM 메시지의 수를 기록 하 고 각 사용자로 보낸 메시지 수 hello 이전 24 시간 동안 정보 tooplot이를 사용 하 여 될 수 있습니다. 하나의 디자인에는 각 직원에 대 한 toostore 24 엔터티 수 있습니다.  

![][22]

이 디자인에서는 있습니다 수를 쉽게 찾고 hello 응용 프로그램 tooupdate hello 메시지 개수 값 필요할 때마다 hello 엔터티 tooupdate 각 직원에 대 한 업데이트 합니다. 그러나 tooretrieve hello 정보 tooplot 차트 hello에 대 한 활동 hello 이전 24 시간, 24 엔터티를 검색 해야 합니다.  

#### <a name="solution"></a>해결 방법
디자인을 별도 속성 toostore hello 메시지 수와 각 시간에 대해 다음 hello를 사용 합니다.  

![][23]

이 디자인에서는 특정 시간에 대 한 직원에 대 한 병합 작업 tooupdate hello 메시지 수를 사용할 수 있습니다. 이제 tooplot hello 차트 단일 엔터티에 대 한 요청을 사용 하 여 필요한 모든 hello 정보를 검색할 수 있습니다.  

#### <a name="issues-and-considerations"></a>문제 및 고려 사항
Hello 지점을 결정할 때 다음 고려 어떻게 tooimplement이이 패턴:  

* 전체 데이터 계열에는 단일 엔터티 (too252 속성을 있을 수 있는 엔터티)에 맞지 않는 경우 blob와 같은 대체 데이터 저장소를 사용 합니다.  
* 여러 클라이언트가 동시에 엔터티를 업데이트 하면 toouse hello **ETag** tooimplement 낙관적 동시성 합니다. 여러 클라이언트가 있는 경우 높은 경합이 발생할 수 있습니다.  

#### <a name="when-toouse-this-pattern"></a>때 toouse이이 패턴
Tooupdate 필요 하 고 개별 엔터티와 연결 된 데이터 계열을 검색 하는 경우이 패턴을 사용 합니다.  

#### <a name="related-patterns-and-guidance"></a>관련 패턴 및 지침
hello 다음 패턴 및 지침은 수도 관련이 패턴을 구현 하는 경우.  

* [큰 엔터티 패턴](#large-entities-pattern)  
* [병합 또는 바꾸기](#merge-or-replace)  
* [결국 일관 된 트랜잭션 패턴](#eventually-consistent-transactions-pattern) (하는 경우를 저장 하는 hello 데이터 계열 blob)  

### <a name="wide-entities-pattern"></a>넓은 엔터티 패턴
개 이상의 252 속성을 가진 여러 물리적 엔터티 toostore 논리적 엔터티를 사용 합니다.  

#### <a name="context-and-problem"></a>컨텍스트 및 문제점
개별 엔터티에 (hello 필수 시스템 속성은 제외) 252 개 이하의 속성이 있을 수 있습니다 및 총에서 1MB 이상 데이터를 저장할 수 없습니다. 관계형 데이터베이스에 일반적으로 얻게 hello 행 크기에 제한이 라운드 새 테이블을 추가 하 고 이들 간에 한 일 관계를 적용할 합니다.  

#### <a name="solution"></a>해결 방법
Hello 테이블 서비스를 사용 하 여 여러 엔터티 toorepresent 이상 252 속성을 가진 단일 큰 비즈니스 개체를 저장할 수 있습니다. 예를 들어 toostore hello IM 보낸 메시지 수 hello에 대 한 각 직원이 최근 365 일간의 수를 원하는 경우 스키마가 서로 다른 두 개의 엔터티를 사용 하 여 디자인 hello를 사용할 수 있습니다.  

![][24]

Toomake 서로 동기화 하는 두 엔터티 tookeep를 업데이트 해야 하는 변경 해야 할 경우에 EGT를 사용할 수 있습니다. 그렇지 않으면 특정 한 날에 대 한 단일 병합 작업 tooupdate hello 메시지 수를 사용할 수 있습니다. 데이터를 함께 사용 하는 두 개의 효율적인 요청과 함께 수행할 수 있는 두 엔터티를 검색 해야 하는 개별 직원에 대 한 hello 모든 tooretrieve는 **PartitionKey** 및 **RowKey** 값입니다.  

#### <a name="issues-and-considerations"></a>문제 및 고려 사항
Hello 지점을 결정할 때 다음 고려 어떻게 tooimplement이이 패턴:  

* 두 개 이상의 저장소 트랜잭션 관련 완료 하는 논리적 엔터티를 검색: 하나의 tooretrieve 실제 엔터티입니다.  

#### <a name="when-toouse-this-pattern"></a>때 toouse이이 패턴
테이블 서비스 필요 toostore 엔터티 크기 또는 다양 한 속성이 있는 hello에 개별 엔터티에 대해 hello 제한을 초과 하는 경우이 패턴을 사용 합니다.  

#### <a name="related-patterns-and-guidance"></a>관련 패턴 및 지침
hello 다음 패턴 및 지침은 수도 관련이 패턴을 구현 하는 경우.  

* [엔터티 그룹 트랜잭션](#entity-group-transactions)
* [병합 또는 바꾸기](#merge-or-replace)

### <a name="large-entities-pattern"></a>큰 엔터티 패턴
Blob 저장소 toostore 큰 속성 값을 사용 합니다.  

#### <a name="context-and-problem"></a>컨텍스트 및 문제점
개별 엔터티는 총 1MB가 넘는 데이터를 저장할 수 없습니다. 사용자 속성 중 하나 또는 여러 hello 엔터티 tooexceed의 총 크기가이 값을 발생 시킨 값을 저장, hello 테이블 서비스에에서 hello 전체 엔터티를 저장할 수 없습니다.  

#### <a name="solution"></a>해결 방법
많은 양의 데이터를 포함 하는 하나 이상의 속성 때문에 크기가 1MB를 초과 하는 엔터티를 하는 경우에 hello Blob 서비스에에서 데이터를 저장 및 다음 hello 엔터티 속성에 hello blob의 hello 주소를 저장할 수 있습니다. 직원의 hello 사진 blob 저장소에 저장 하 고 링크 toohello 사진 hello에 저장할 수 예를 들어 **사진** employee 엔터티의 속성:  

![][25]

#### <a name="issues-and-considerations"></a>문제 및 고려 사항
Hello 지점을 결정할 때 다음 고려 어떻게 tooimplement이이 패턴:  

* Blob 서비스 hello hello 데이터와 hello 테이블 서비스의에서 hello 엔터티 간에 toomaintain 결과적 일관성 hello를 사용 하 여 [결국 일관 된 트랜잭션 패턴](#eventually-consistent-transactions-pattern) toomaintain 사용자 엔터티.
* 두 개 이상의 저장소 트랜잭션 포함를 전체 엔터티에 검색: 하나의 tooretrieve hello 엔터티와 하나의 tooretrieve hello blob 데이터입니다.  

#### <a name="when-toouse-this-pattern"></a>때 toouse이이 패턴
Toostore 엔터티 필요에 따라 크기가 hello 테이블 서비스에 개별 엔터티에 대해 hello 제한을 초과 해야 하는 경우이 패턴을 사용 합니다.  

#### <a name="related-patterns-and-guidance"></a>관련 패턴 및 지침
hello 다음 패턴 및 지침은 수도 관련이 패턴을 구현 하는 경우.  

* [결과적으로 일관성 있는 트랜잭션 패턴](#eventually-consistent-transactions-pattern)  
* [넓은 엔터티 패턴](#wide-entities-pattern)

<a name="prepend-append-anti-pattern"></a>

### <a name="prependappend-anti-pattern"></a>앞에 추가/뒤에 추가 안티패턴
여러 파티션에서 hello 삽입 분배 하 여 많은 양의 삽입이 있는 경우 확장성 향상.  

#### <a name="context-and-problem"></a>컨텍스트 및 문제점
먼저 새 엔터티 toohello을 추가 하는 hello 응용 프로그램으로 인해 일반적으로 엔터티 tooyour 저장 된 엔터티를 추가 또는 앞에 추가 되거나 파티션을 파티션 시퀀스의 마지막 합니다. 이 경우 언제 든 지 hello 삽입의 모든 hello 테이블 서비스 부하 분산 되지 않도록 하 한 핫스폿을 생성 하는 동일한 파티션을 여러 노드에서 삽입 hello에서 수행 되며 사용자 응용 프로그램 toohit hello 확장성을 일으킬 수 있는 파티션에 대 한 대상으로 합니다. 예를 들어 될 수 있는 엔터티 구조 아래와 같이 다음 직원이, 로그 네트워크 및 리소스에 액세스 하는 응용 프로그램이 있는 경우 hello 트랜잭션 양이 hello에 대 한 hello 확장성 목표에 도달 하면 핫스폿 되 고 현재 시간 파티션 개별 파티션:  

![][26]

#### <a name="solution"></a>해결 방법
hello 다음과 같은 대체 엔터티 구조 방지 특정 파티션의에서 핫스폿을 hello 응용 프로그램 로그 이벤트로 합니다.  

![][27]

확인이 예제와 둘 다 hello **PartitionKey** 및 **RowKey** 복합 키가 있습니다. hello **PartitionKey** 여러 파티션에서 hello 부서 및 직원 id toodistribute hello 로깅을 모두 사용 합니다.  

#### <a name="issues-and-considerations"></a>문제 및 고려 사항
Hello 지점을 결정할 때 다음 고려 어떻게 tooimplement이이 패턴:  

* hello 대체 키 구조 쿼리를 만드는 핫 파티션을 insert에 효율적으로 지원 hello 방지 하는 클라이언트 응용 프로그램에서는?  
* 트랜잭션의 예상된 볼륨 가능성이 tooreach 개별 파티션에 대 한 hello 확장성 목표는 hello 저장소 서비스에 의해 스로틀 된 것을 의미 합니까?  

#### <a name="when-toouse-this-pattern"></a>때 toouse이이 패턴
트랜잭션 볼륨 가능성이 tooresult 핫 파티션을 액세스할 때 hello 저장소 서비스에 의해 제한 되 면 hello 앞에 추가 하 고 추가 안티패턴을 하지 마십시오.  

#### <a name="related-patterns-and-guidance"></a>관련 패턴 및 지침
hello 다음 패턴 및 지침은 수도 관련이 패턴을 구현 하는 경우.  

* [복합 키 패턴](#compound-key-pattern)  
* [로그 테일 패턴](#log-tail-pattern)  
* [엔터티 수정](#modifying-entities)  

### <a name="log-data-anti-pattern"></a>로그 데이터 안티패턴
일반적으로 hello 테이블 서비스 toostore 로그 데이터 대신 hello Blob 서비스를 사용 해야 합니다.  

#### <a name="context-and-problem"></a>컨텍스트 및 문제점
로그 데이터는 tooretrieve 특정 날짜/시간 범위에 대 한 로그 항목의 선택에 대 한 일반적인 사용 사례: 응용 프로그램 로그 15시 04분 및 15:06 특정 날짜에 시작 하는 중요 한 메시지와 오류 hello 모든 toofind 원하는 예를 들어 있습니다. Toouse hello 날짜 및 시간 파티션의 hello 로그 메시지 toodetermine hello에 로그 항목을 저장 하지 않을:는 핫 분할에 대 한 결과 모든 hello 로그 엔터티 어느 시점에 공유 하 게 되므로 hello 동일 **PartitionKey** 값 (hello 섹션을 참조 [Prepend/추가 안티패턴](#prepend-append-anti-pattern)). 예를 들어 hello 응용 프로그램 toohello 파티션 hello 현재 날짜 및 시간에 대 한 모든 로그 메시지를 기록 하기 때문에 로그 메시지에 대 한 엔터티 스키마를 따르는 hello 핫 분할에 발생 합니다.  

![][28]

이 예제에서는 hello **RowKey** 날짜/시간 순서 대로 정렬 된 로그 메시지를 저장 하는 hello 로그 메시지 tooensure의 hello 날짜 및 시간을 포함 하 고 여러 로그 메시지 hello 동일한 날짜 및 시간을 공유 하는 경우 메시지 id를 포함 합니다.  

또 다른 방법은 toouse는 **PartitionKey** 검색이 설정 되어 hello 응용 프로그램 파티션의 범위 전체에서 메시지를 기록 합니다. 예를 들어 hello 소스 hello 로그 메시지의 여러 파티션에서 방법을 toodistribute 메시지를 제공, 엔터티 스키마를 따르는 hello를 사용할 수 있습니다.  

![][29]

그러나 hello 문제가이 스키마는 로그 메시지는 특정 시간 범위를 검색 해야 hello 모든 해당 tooretrieve hello 테이블의 모든 파티션에 합니다.

#### <a name="solution"></a>해결 방법
hello 이전 섹션 강조 표시 된 hello 문제 toouse 시도의 hello 테이블 서비스 toostore 로그 항목 두 불만족 제안, 디자인 합니다. 로그 메시지를 작성 하는 성능 저하의 hello 위험을이 어 졌는 한 가지 해결 tooa 핫 파티션 hello 다른 솔루션으로 인해 쿼리 성능 저하 hello 요구 사항 tooscan 때문에 특정 시간 범위에 대 한 hello tooretrieve 로그 메시지를 테이블에서 모든 파티션 되었습니다. Blob 저장소 이러한 종류의 시나리오에 대 한 더 나은 솔루션 소개 하며이 어떻게 Azure Storage Analytics hello 로그 데이터를 저장을 수집 합니다.  

이 섹션에서는 Storage Analytics 저장 하는 방법을 로그 데이터를 blob 저장소에 이러한 접근 방식 toostoring 데이터 범위 내에서 일반적으로 쿼리 하는 그림으로 설명 합니다.  

Storage Analytics는 로그 메시지를 구분 기호로 분리된 형식으로 여러 Blob에 저장합니다. hello 구분 기호로 분리 된 형식을 사용 하면 쉽게 클라이언트에 대 한 응용 프로그램 tooparse hello 데이터 hello 로그 메시지에서 합니다.  

Storage Analytics는 검색 하려는 hello 로그 메시지를 포함 하는 toolocate hello blob (또는 blob) 사용 하면 blob에 대 한 명명 규칙을 사용 합니다. 예를 들어 "queue/2014/07/31/1800/000001.log" 라는 blob는 2014 년 7 월 31 일 18시 시작 하는 hello 시간에 대 한 toohello 큐 서비스와 관련 된 로그 메시지를 포함 합니다. "000001" hello이이 기간에 대 한 hello 첫 번째 로그 파일 임을 나타냅니다. 저장소 분석 또한 hello의 hello 타임 스탬프를 먼저 기록 및 마지막 hello blob의 메타 데이터의 일부로 hello 파일에 저장 된 메시지를 로그 합니다. blob 저장소 이름 접두사에 따라 컨테이너에서 blob를 찾을 수 있습니다에 대 한 API hello: toolocate 큐를 포함 하는 모든 hello blob 데이터 18시 시작 하는 hello 시간에 대 한 로그, hello 접두사 "큐/2014/07/31/1800."를 사용할 수 있습니다  

저장소 분석 로그 메시지를 내부적으로 버퍼링 하 고 hello 적절 한 blob를 정기적으로 업데이트 하거나 로그 항목의 최신 배치 hello로 새 레코드를 만듭니다. Hello 수를 줄일 수이 쓰기 toohello blob 서비스 수행 해야 합니다.  

Toomanage 안정성 (발생 하는 대로 모든 로그 항목 tooblob 저장소 쓰기) 및 비용 및 확장성 사이의 절충 값 hello 하는 방법을 고려해 야 사용자 응용 프로그램에서 유사한 솔루션을 구현 하는 경우 (응용 프로그램에서 업데이트를 버퍼링 하 고 tooblob 저장소에에서 작성 일괄 처리).  

#### <a name="issues-and-considerations"></a>문제 및 고려 사항
Hello 포인트 toostore 데이터를 기록 하는 방법을 결정할 때 다음을 고려 합니다.  

* 잠재적 핫 파티션을 방지하는 테이블 디자인을 만든 경우 로그 데이터에 효율적으로 액세스할 수 없는 경우가 있을 수 있습니다.  
* tooprocess 로그 데이터, 클라이언트 종종 필요한 tooload 레코드 수입니다.  
* 로그 데이터는 구조화된 경우가 많지만 Blob 저장소가 더 나은 솔루션일 수 있습니다.  

### <a name="implementation-considerations"></a>구현 고려 사항
이 섹션 hello 이전 섹션에 설명 된 hello 패턴을 구현할 때 설명 염두에서 hello 고려 사항 toobear 중 일부입니다. 이 섹션의 대부분 hello 저장소 클라이언트 라이브러리 (버전 4.3.0 hello 작성 시점에)를 사용 하는 C#으로 작성 된 예제를 사용 합니다.  

### <a name="retrieving-entities"></a>엔터티 검색
Hello 섹션에서 설명한 대로 [를 쿼리 하기 위한 디자인](#design-for-querying), hello 가장 효율적인 쿼리는 지점 쿼리 합니다. 그러나 일부 시나리오에서 할 수 있습니다 tooretrieve 여러 엔터티. 이 섹션에서는 hello 저장소 클라이언트 라이브러리를 사용 하 여 몇 가지 일반적인 접근 방식을 tooretrieving 엔터티를 설명 합니다.  

#### <a name="executing-a-point-query-using-hello-storage-client-library"></a>Hello 저장소 클라이언트 라이브러리를 사용 하 여 지점 쿼리를 실행 합니다.
hello 가장 쉬운 방법은 tooexecute 지점 쿼리는 toouse hello **검색** 로 엔터티를 검색 하는 hello 다음 C# 코드 조각에에서 나와 있는 것 처럼 작업 테이블을 **PartitionKey** 값 "Sales"와  **RowKey** "212" 값의:  

```csharp
TableOperation retrieveOperation = TableOperation.Retrieve<EmployeeEntity>("Sales", "212");
var retrieveResult = employeeTable.Execute(retrieveOperation);
if (retrieveResult.Result != null)
{
    EmployeeEntity employee = (EmployeeEntity)retrieveResult.Result;
    ...
}  
```

이 예제에서는 hello 엔터티를 예상 하는 방법을 확인 형식의 toobe 검색 **EmployeeEntity**합니다.  

#### <a name="retrieving-multiple-entities-using-linq"></a>LINQ를 사용하여 여러 엔터티 검색
저장소 클라이언트 라이브러리와 함께 LINQ를 사용하고 **where** 절이 있는 쿼리를 지정하여 여러 엔터티를 검색할 수 있습니다. 테이블 검색 tooavoid 항상 포함 해야 hello **PartitionKey** hello에 대 한 값 여기서 절, 가능한 경우 hello 및 **RowKey** tooavoid 테이블 및 파티션 검색 값입니다. hello 테이블 서비스에서는 제한 된 비교 연산자 (보다 큼, 보다 큰 또는 같음, 보다 작음, 작거나 또는, 같음, 같고 같지 않음) toouse 집합이 hello 여기서 절. hello 다음 C# 코드 조각은 직원을 찾습니다 모든 hello "B" 인 마지막 이름은 시작 (해당 hello 가정 **RowKey** 저장소 hello 성) hello 영업 부서의 (hello 가정 **PartitionKey** 저장소 hello 부서 이름):  

```csharp
TableQuery<EmployeeEntity> employeeQuery = employeeTable.CreateQuery<EmployeeEntity>();
var query = (from employee in employeeQuery
            where employee.PartitionKey == "Sales" &&
            employee.RowKey.CompareTo("B") >= 0 &&
            employee.RowKey.CompareTo("C") < 0
            select employee).AsTableQuery();
var employees = query.Execute();  
```

Hello 쿼리 둘 다 지정 방법을 **RowKey** 및 **PartitionKey** tooensure 성능을 향상 합니다.  

hello 다음 보여 주는 코드 예제 hello fluent API를 사용 하 여 해당 하는 기능 (fluent Api에 대 한 자세한 내용은 참조 일반적으로 [Fluent API를 디자인 하기 위한 모범 사례](http://visualstudiomagazine.com/articles/2013/12/01/best-practices-for-designing-a-fluent-api.aspx)):  

```csharp
TableQuery<EmployeeEntity> employeeQuery = new TableQuery<EmployeeEntity>().Where(
    TableQuery.CombineFilters(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition(
    "PartitionKey", QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.GenerateFilterCondition(
    "RowKey", QueryComparisons.GreaterThanOrEqual, "B")
),
TableOperators.And,
TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "C")
    )
);
var employees = employeeTable.ExecuteQuery(employeeQuery);  
```

> [!NOTE]
> hello 샘플 중첩 여러 **CombineFilters** 메서드 tooinclude hello 세 개의 필터 조건을 합니다.  
> 
> 

#### <a name="retrieving-large-numbers-of-entities-from-a-query"></a>쿼리에서 여러 엔터티 검색
최적의 쿼리는 **PartitionKey** 값과 **RowKey** 값을 기반으로 개별 엔터티를 반환합니다. 그러나 일부 시나리오에서 할 수 있습니다 요구 사항 tooreturn 파티션 같거나 여러 파티션을 포함 하 여 hello에서 많은 엔터티.  

이러한 시나리오에서는 응용 프로그램의 성능을 hello를 항상 완벽 하 게 테스트 해야 합니다.  

Hello 테이블 서비스에 대 한 쿼리 1,000 엔터티 최대 한 번에 반환할 수 있으며 최대 5 초 동안 실행 될 수 있습니다. 연속 토큰 tooenable 클라이언트 응용 프로그램 toorequest hello hello hello 결과 집합에 포함 된 1, 000 개 엔터티, hello 쿼리가 5 초 안에 완료 되지 않은 논리값이 hello 쿼리 hello 파티션 경계를 교차 하는 경우 hello 테이블 서비스 다음 엔터티 집합입니다. 연속 토큰의 작동 방식에 대한 자세한 내용은 [쿼리 제한 시간 및 페이지 번호 매김](http://msdn.microsoft.com/library/azure/dd135718.aspx)을 참조하세요.  

Hello 저장소 클라이언트 라이브러리를 사용 하는 경우 자동으로 처리할 수 연속 토큰 드립니다 hello 테이블 서비스에서에서 엔터티를 반환 합니다. hello 다음 C# 코드 샘플 hello 저장소 클라이언트 라이브러리를 자동으로 사용 하 여 연속 토큰 처리 hello 테이블 서비스는 응답에 반환 하는 경우:  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

var employees = employeeTable.ExecuteQuery(employeeQuery);
foreach (var emp in employees)
{
        ...
}  
```

C# 코드 다음 hello 연속 토큰을 명시적으로 처리 합니다.  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

TableContinuationToken continuationToken = null;

do
{
        var employees = employeeTable.ExecuteQuerySegmented(
        employeeQuery, continuationToken);
    foreach (var emp in employees)
    {
    ...
    }
    continuationToken = employees.ContinuationToken;
} while (continuationToken != null);  
```

연속 토큰을 명시적으로 사용 하 여 응용 프로그램 데이터의 다음 세그먼트 hello를 검색 하는 시기를 제어할 수 있습니다. 예를 들어 테이블에 저장 된 hello 엔터티를 통해 사용자가 toopage를 사용 하는 클라이언트 응용 프로그램, 경우 사용자 결정할 수 있도록 응용 프로그램에 사용 연속 토큰 tooretrieve hello 다음 hello 쿼리로 검색 된 모든 hello 엔터티를 통해 toopage 하지 hello 사용자 hello 현재 세그먼트에 있는 모든 hello 엔터티 집합에 대해 페이징을 완료 되 면 세그먼트입니다. 이 접근 방식에는 몇 가지 이점이 있습니다.  

* 하면 toolimit hello hello 테이블 서비스에서에서 데이터 tooretrieve 양과 hello 네트워크를 통해 이동 하는.  
* 있습니다 tooperform 비동기 IO를.net에서 수 있습니다.  
* 하면 tooserialize hello 연속 토큰 toopersistent 저장소 응용 프로그램 크래시가의 hello 이벤트에서 계속 수행할 수 있습니다.  

> [!NOTE]
> 일반적으로 연속 토큰은 1,000개(이보다 적을 수도 있음)의 엔터티가 포함된 세그먼트를 반환합니다. 이것은 hello 경우에도 hello를 사용 하 여 쿼리에서 반환 하는 항목 수를 제한 하는 경우 **걸릴** tooreturn hello 처음 n 개 엔터티 조회 조건과 일치 하는: hello 테이블 서비스와 함께 n 개 엔터티를 보다 적으면를 포함 하는 세그먼트를 반환할 수 있습니다 연속 토큰 tooenable와 있습니다 tooretrieve 나머지 엔터티 hello 합니다.  
> 
> 

hello 다음 C# 코드를 보여 줍니다 세그먼트 내 반환 되는 엔터티의 toomodify hello 수 있습니다:  

```csharp
employeeQuery.TakeCount = 50;  
```

#### <a name="server-side-projection"></a>서버 쪽 프로젝션
단일 엔터티 too255 속성을 있고 too1 MB 단위로 크기를 수 있습니다. 모든 hello 속성이 필요 하지 않을 hello 테이블을 쿼리 하 고 엔터티를 검색할 때 및 데이터를 불필요 하 게 전송 하는 되지 않도록 (toohelp 대기 시간 및 비용을 감소 하는 데 사용). 필요한 서버 쪽 프로젝션 tootransfer 정당한 hello 속성을 사용할 수 있습니다. hello 다음 예제는 검색만 hello **전자 메일** 속성 (함께 **PartitionKey**, **RowKey**, **타임 스탬프**, 및  **ETag**) hello 엔터티에서 hello 쿼리에서 선택 합니다.  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
List<string> columns = new List<string>() { "Email" };
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter).Select(columns);

var entities = employeeTable.ExecuteQuery(employeeQuery);
foreach (var e in entities)
{
        Console.WriteLine("RowKey: {0}, EmployeeEmail: {1}", e.RowKey, e.Email);
}  
```

Hello 어떻게 확인 **RowKey** 속성 tooretrieve hello 목록에 포함 되지 않은 경우에 값을 사용할 수 있습니다.  

### <a name="modifying-entities"></a>엔터티 수정
저장소 클라이언트 라이브러리 hello toomodify를 삽입, 삭제 및 업데이트 엔터티 여 hello 테이블 서비스에 저장 된 엔터티 수 있습니다. 여러 삽입, 업데이트 및 삭제 작업 함께 tooreduce hello 수의 왕복 필요 하 고 솔루션의 hello 성능 향상 EGTs toobatch를 사용할 수 있습니다.  

참고 hello 저장소 클라이언트 라이브러리는 EGT를 일반적으로 실행 될 때 발생 한 예외 hello 일괄 처리 toofail 발생 시킨 hello 엔터티의 hello 인덱스를 포함 합니다. 이는 EGT를 사용하는 코드를 디버그할 때 유용합니다.  

디자인이 클라이언트 응용 프로그램에서 동시성 및 업데이트 작업을 처리하는 방법에 어떤 영향을 미치는지도 고려해야 합니다.  

#### <a name="managing-concurrency"></a>동시성 관리
기본적으로 hello 테이블 서비스는 낙관적 동시성 검사에 대 한 개별 엔터티 hello 수준에서 구현 **삽입**, **병합**, 및 **삭제** 작업 클라이언트 tooforce hello 테이블 서비스 toobypass 이러한 검사에 대 한 것이 가능 하지만 합니다. Hello 테이블 서비스 동시성을 관리 하는 방법에 대 한 자세한 내용은 참조 [Microsoft Azure 저장소에 대 한 동시성 관리](storage-concurrency.md)합니다.  

#### <a name="merge-or-replace"></a>병합 또는 바꾸기
hello **대체** hello 방식의 **TableOperation** 클래스에는 항상 hello hello 테이블 서비스에서에서 전체 엔터티 대체 합니다. Hello 저장 된 엔터티의 해당 속성이 존재 하는 경우 속성 hello 요청에 포함 되지 않은 경우 hello 요청 엔터티 hello에서 속성에 저장 되도록를 제거 합니다. Tooremove 저장 엔터티에서 명시적으로 속성을 사용 하려는 경우가 아니면 hello 요청에서 모든 속성을 포함 해야 합니다.  

Hello를 사용할 수 있습니다 **병합** hello 방식의 **TableOperation** 보내는 toohello 테이블 서비스 tooupdate 하려는 경우 엔터티 데이터 양을 tooreduce hello 클래스입니다. hello **병합** 메서드 hello 요청에 포함 된 hello 엔터티에서 속성 값으로 저장 하는 hello 엔터티의 모든 속성을 대체 하지만 leaves 그대로 hello에서 속성을 hello 요청에 포함 되지 않은 엔터티를 저장 합니다. 큰 엔터티를 있고만 tooupdate 적은 수의 요청에서 속성을 필요한 경우에 유용 합니다.  

> [!NOTE]
> hello **대체** 및 **병합** hello 엔터티가 존재 하지 않는 경우 메서드가 실패 합니다. 사용 하 여 hello **InsertOrReplace** 및 **InsertOrMerge** 존재 하지 않는 경우 새 엔터티를 만드는 메서드를 합니다.  
> 
> 

### <a name="working-with-heterogeneous-entity-types"></a>유형이 다른 엔터티 유형 작업
hello 테이블 서비스는는 *스키마 없음* 테이블 저장소를 단일 테이블 디자인에 뛰어난 유연성을 제공 하는 여러 형식의 엔터티를 저장할 수 있다는 것을 의미 합니다. hello 다음 예제에서는 employee 및 department 엔터티 둘 다를 저장 하는 테이블 수행 합니다.  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>타임 스탬프</th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>FirstName</th>
<th>LastName</th>
<th>Age</th>
<th>Email</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>FirstName</th>
<th>LastName</th>
<th>Age</th>
<th>Email</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>DepartmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>FirstName</th>
<th>LastName</th>
<th>Age</th>
<th>Email</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

각 엔터티에 여전히 **PartitionKey**, **RowKey** 및 **Timestamp** 값이 있어야 하지만 다른 속성 집합은 원하는 대로 포함할 수 있습니다. 또한 없는 toostore 어딘가에 해당 정보를 선택 하지 않으면 엔터티 tooindicate hello 입력 됩니다. Hello 엔터티 유형을 식별 하는 방법은 두 가지가 있습니다.  

* Hello 엔터티 형식 toohello 앞 **RowKey** (또는 가능 환영 **PartitionKey**). **RowKey** 값을 예로 들어 **EMPLOYEE_000123** 또는 **DEPARTMENT_SALES**하십시오.  
* Hello 테이블 아래에 나와 있는 것 처럼 별도 속성 toorecord hello 엔터티 형식을 사용 합니다.  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>타임 스탬프</th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>FirstName</th>
<th>LastName</th>
<th>Age</th>
<th>Email</th>
</tr>
<tr>
<td>Employee</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>FirstName</th>
<th>LastName</th>
<th>Age</th>
<th>Email</th>
</tr>
<tr>
<td>Employee</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>DepartmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td>department</td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>FirstName</th>
<th>LastName</th>
<th>Age</th>
<th>Email</th>
</tr>
<tr>
<td>Employee</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

hello 엔터티 형식 toohello 앞에 추가 하는 hello 첫 번째 옵션을 **RowKey**, 동일한 키 값 형식이 다른 두 개의 엔터티를 들 수 hello 가능성이 경우 유용 합니다. 또한 형식 함께 hello 파티션 동일 hello의 엔터티를 그룹화 합니다.  

hello이 섹션에 설명 된 기술을 특별히 관련 된 toohello 토론 [상속 관계](#inheritance-relationships) hello 섹션에이 가이드 앞부분에 있는 [관계를 모델링](#modelling-relationships)합니다.  

> [!NOTE]
> Hello 엔터티 형식 값 tooenable 클라이언트 응용 프로그램 tooevolve POCO 개체의 버전 번호를 포함 하는 것이 좋습니다. 하 고 다른 버전을 사용 해야 합니다.  
> 
> 

hello이 섹션의 나머지 부분에 설명 hello 저장소 클라이언트 라이브러리의에서 작업을 쉽고 hello의 엔터티 형식에 여러 개의 동일한 hello 기능 중 일부 테이블입니다.  

#### <a name="retrieving-heterogeneous-entity-types"></a>서로 다른 엔터티 유형 검색
Hello 저장소 클라이언트 라이브러리를 사용 하는 경우 여러 엔터티 형식을 사용 하기 위한 세 가지 옵션이 있습니다.  

특정와 함께 저장 하는 hello 엔터티의 hello 형식을 알고 있는 경우 **RowKey** 및 **PartitionKey** 값 hello 이전 두 예와 같이 hello 엔터티를 검색 하는 경우 hello 엔터티 형식을 지정할 수 있습니다 형식의 엔터티를 검색 하는 **EmployeeEntity**: [hello 저장소 클라이언트 라이브러리를 사용 하 여 지점 쿼리를 실행](#executing-a-point-query-using-the-storage-client-library) 및 [LINQ를사용하여여러엔터티를검색](#retrieving-multiple-entities-using-linq).  

hello 두 번째 옵션은 toouse hello **DynamicTableEntity** 구체적인 POCO 엔터티 형식이 아닌 형식 (예: 속성 모음) (이 옵션 수 없는 필요 tooserialize 없기 때문에 성능이 향상 및 너무 hello 엔터티를 deserialize 합니다. NET 형식)입니다. C# 코드를 잠재적으로 다음 hello hello 테이블에서 다른 유형의 여러 항목을 검색 하지만로 모든 엔터티를 반환 **DynamicTableEntity** 인스턴스. Hello 사용 하 여 다음 **EntityType** 각 엔터티의 속성 toodetermine hello 유형:  

```csharp
string filter = TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("PartitionKey",
    QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("RowKey",
                    QueryComparisons.GreaterThanOrEqual, "B"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey",
        QueryComparisons.LessThan, "F")
    )
);
TableQuery<DynamicTableEntity> entityQuery =
    new TableQuery<DynamicTableEntity>().Where(filter);
var employees = employeeTable.ExecuteQuery(entityQuery);

IEnumerable<DynamicTableEntity> entities = employeeTable.ExecuteQuery(entityQuery);
foreach (var e in entities)
{
EntityProperty entityTypeProperty;
if (e.Properties.TryGetValue("EntityType", out entityTypeProperty))
{
    if (entityTypeProperty.StringValue == "Employee")
    {
        // Use entityTypeProperty, RowKey, PartitionKey, Etag, and Timestamp
        }
    }
}  
```

해당 tooretrieve hello를 사용 해야 하는 다른 속성을 확인 **TryGetValue** 메서드 hello **속성** hello 속성 **DynamicTableEntity** 클래스입니다.  

세 번째 방법은 hello를 사용 하 여 toocombine **DynamicTableEntity** 유형 및 **EntityResolver** 인스턴스. 이렇게 하면 hello에 tooresolve toomultiple POCO 형식을 동일한 쿼리 합니다. 이 예제에서는 hello **EntityResolver** 대리자 hello를 사용 하는 **EntityType** hello 쿼리에서 반환 하는 엔터티의 hello 두 형식 간의 toodistinguish 속성입니다. hello **해결** 방법은 hello를 사용 하 여 **확인자** tooresolve 위임 **DynamicTableEntity** 너무 인스턴스**TableEntity** 인스턴스.  

```csharp
EntityResolver<TableEntity> resolver = (pk, rk, ts, props, etag) =>
{

        TableEntity resolvedEntity = null;
        if (props["EntityType"].StringValue == "Department")
        {
        resolvedEntity = new DepartmentEntity();
        }
        else if (props["EntityType"].StringValue == "Employee")
        {
        resolvedEntity = new EmployeeEntity();
        }
        else throw new ArgumentException("Unrecognized entity", "props");

        resolvedEntity.PartitionKey = pk;
        resolvedEntity.RowKey = rk;
        resolvedEntity.Timestamp = ts;
        resolvedEntity.ETag = etag;
        resolvedEntity.ReadEntity(props, null);
        return resolvedEntity;
};

string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<DynamicTableEntity> entityQuery =
        new TableQuery<DynamicTableEntity>().Where(filter);

var entities = employeeTable.ExecuteQuery(entityQuery, resolver);
foreach (var e in entities)
{
        if (e is DepartmentEntity)
        {
    ...
        }
        if (e is EmployeeEntity)
        {
    ...
        }
}  
```

#### <a name="modifying-heterogeneous-entity-types"></a>서로 다른 엔터티 유형 수정
및를 알려 항상 hello 엔터티 형식을 삽입 하면 tooknow hello 유형의 엔터티 toodelete 않아도 됩니다. 사용할 수 있습니다 **DynamicTableEntity** 해당 형식을 모르는 및 POCO 엔터티 클래스를 사용 하지 않고 tooupdate 엔터티를 입력 합니다. hello 다음 코드 예제는 단일 엔터티를 검색 하 고 hello 확인 **EmployeeCount** 업데이트 하기 전에 속성이 존재 합니다.  

```csharp
TableResult result =
        employeeTable.Execute(TableOperation.Retrieve(partitionKey, rowKey));
DynamicTableEntity department = (DynamicTableEntity)result.Result;

EntityProperty countProperty;

if (!department.Properties.TryGetValue("EmployeeCount", out countProperty))
{
        throw new
        InvalidOperationException("Invalid entity, EmployeeCount property not found.");
}
countProperty.Int32Value += 1;
employeeTable.Execute(TableOperation.Merge(department));  
```

### <a name="controlling-access-with-shared-access-signatures"></a>공유 액세스 서명을 사용하여 액세스 제어
공유 액세스 서명 (SAS) 토큰 tooenable 클라이언트 응용 프로그램 toomodify를 사용 하 여 (및 쿼리할 수 있습니다) hello 테이블 서비스와 직접 hello 필요 tooauthenticate 하지 않고 직접 테이블 엔터티. 일반적으로, 응용 프로그램에서 세 가지 주요 이점을 toousing SAS입니다.  

* Toodistribute 불필요 저장소 계정 키 tooan 안전 하지 않은 플랫폼 (예: 모바일 장치)에 순서 tooallow 해당 장치 tooaccess 및 hello 테이블 서비스의에서 엔터티를 수정 합니다.  
* 오프 로드할 수 있습니다 hello 작업의 일부 해당 웹 및 작업자 역할 최종 사용자 컴퓨터와 같은 엔터티 tooclient 장치 및 모바일 장치 관리를 수행 합니다.  
* 에 제한 된 할당할 수 있으며 시간 제한 된 사용 권한 tooa 클라이언트 (예: toospecific 리소스 읽기 전용 액세스를 허용) 집합입니다.  

테이블 서비스 hello로 SAS 토큰을 사용 하는 방법에 대 한 자세한 내용은 참조 [공유 액세스 서명 (SAS)를 사용 하 여](storage-dotnet-shared-access-signature-part-1.md)합니다.  

그러나 클라이언트 응용 프로그램 toohello 엔터티 hello 테이블 서비스에 권한을 부여 하는 hello SAS 토큰 여전히 생성 해야 합니다: 액세스 tooyour 저장소 계정 키를 보안에 환경에서이 작업을 수행 해야 합니다. 일반적으로 웹 또는 작업자 역할 toogenerate hello SAS 토큰 및 tooyour 엔터티 액세스 해야 하는 toohello 클라이언트 응용 프로그램에 전달할를 사용 합니다. 가 여전히 오버 헤드를 생성 하 고 SAS 토큰 tooclients 배달에 관련 된 최선의 방법 tooreduce 대량 시나리오에서 특히이 오버 헤드를 고려해 야 합니다.  

가능한 toogenerate tooa hello 테이블의에서 엔터티 집합이 있는 액세스 권한을 부여 하는 SAS 토큰은 기본적으로 전체 테이블에 대 한 SAS 토큰 만들지만 이기도 가능한 toospecify의 범위는 해당 hello SAS 토큰 권한 부여 액세스 tooeither **PartitionKey** 값 또는 범위 **PartitionKey** 및  **RowKey** 값입니다. 선택할 수 있습니다 toogenerate 시스템의 개별 사용자에 대 한 SAS 토큰 각 사용자의 SAS 토큰에 대 한 액세스만 허용 되도록 tootheir hello의 고유한 엔터티 테이블 서비스입니다.  

### <a name="asynchronous-and-parallel-operations"></a>비동기 및 병렬 작업
여러 파티션에 요청을 분산하는 경우 비동기 또는 병렬 쿼리를 사용하여 처리량 및 클라이언트 응답성을 향상시킬 수 있습니다.
예를 들어 둘 이상의 작업자 역할 인스턴스에서 테이블에 병렬로 액세스하는 경우가 있을 수 있습니다. 파티션의 특정 집합에 대 한 책임 개별 작업자 역할을 설치 하거나 여러 작업자 역할 인스턴스, 각 수 tooaccess 하기만 수도 있습니다는 테이블에서 파티션의 hello 모든 합니다.  

클라이언트 인스턴스 내에서 저장소 작업을 비동기식으로 실행하여 처리량을 향상시킬 수 있습니다. hello 저장소 클라이언트 라이브러리를 사용 하면 쉽게 toowrite 비동기 쿼리 및 수정 합니다. 예를 들어 hello C# 코드 다음에 표시 된 대로 파티션의 모든 hello 엔터티를 검색 하는 hello 동기 메서드를 시작할 수 있습니다.  

```csharp
private static void ManyEntitiesQuery(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

        TableContinuationToken continuationToken = null;

        do
        {
        var employees = employeeTable.ExecuteQuerySegmented(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
    {
        ...
    }
        continuationToken = employees.ContinuationToken;
        } while (continuationToken != null);
}  
```

Hello를 쿼리 하는 다음과 같이 비동기적으로 실행 되도록이 코드를 쉽게 수정할 수 있습니다.  

```csharp
private static async Task ManyEntitiesQueryAsync(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);
        TableContinuationToken continuationToken = null;

        do
        {
        var employees = await employeeTable.ExecuteQuerySegmentedAsync(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
        {
            ...
        }
        continuationToken = employees.ContinuationToken;
            } while (continuationToken != null);
}  
```

이 예에서 비동기 hello 다음과 같이 hello 동기 버전에서 변경 확인할 수 있습니다.  

* hello 메서드 시그니처에 이제 hello 포함 **비동기** 한정자 및 반환 된 **작업** 인스턴스.  
* 호출 hello 대신 **ExecuteSegmented** 메서드 tooretrieve 결과, hello 메서드 이제 호출 hello **ExecuteSegmentedAsync** 메서드 및 사용 하 여 hello **await** 한정자 tooretrieve는 비동기적으로 발생합니다.  

hello 클라이언트 응용 프로그램이이 메서드가 여러 번 호출할 수 있습니다 (hello에 대 한 값이 서로 다른 **부서** 매개 변수), 각 쿼리에 별도 스레드에서 실행 됩니다.  

가 없는 비동기 버전의 hello **Execute** hello에 대 한 메서드 **TableQuery** 클래스 하므로 hello **a b l e** 인터페이스는 비동기 지원 열거형입니다.  

엔터티를 비동기식으로 삽입, 업데이트 및 삭제할 수도 있습니다. 다음 C# 예제는 hello 간단 하 고 동기 메서드 tooinsert 표시 하거나 employee 엔터티를 바꿉니다.  

```csharp
private static void SimpleEmployeeUpsert(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = employeeTable
        .Execute(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

Hello 업데이트 다음과 같이 비동기적으로 실행 되도록이 코드를 쉽게 수정할 수 있습니다.  

```csharp
private static async Task SimpleEmployeeUpsertAsync(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = await employeeTable
        .ExecuteAsync(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

이 예에서 비동기 hello 다음과 같이 hello 동기 버전에서 변경 확인할 수 있습니다.  

* hello 메서드 시그니처에 이제 hello 포함 **비동기** 한정자 및 반환 된 **작업** 인스턴스.  
* 호출 hello 대신 **Execute** 메서드 tooupdate hello 엔터티, hello 메서드 이제 호출 hello **ExecuteAsync** 메서드 및 사용 하 여 hello **await** 한정자 tooretrieve 비동기적으로 발생합니다.  

hello 클라이언트 응용 프로그램에서 이와 같은 여러 비동기 메서드를 호출할 수 및 각 메서드 호출 마다 별도 스레드에서 실행 됩니다.  

### <a name="credits"></a>크레딧
Hello 기여도 대 한 Azure 팀의 멤버가 따르는 toothank hello 같은: Dominic Betts, Jason Hogg, 장 Ghanem, Jai Haridas, Jeff Irwin, Vamshidhar Kommineni, Vinay 샤 및 Serdar Ozler로 Microsoft DX에서 Tom 적입니다. 

또한 toothank hello 검토 주기 동안 Microsoft mvp 인 고객의 의견에 대 한 다음 같은: Igor Papirov 및 Edward Bakker 합니다.

[1]: ./media/storage-table-design-guide/storage-table-design-IMAGE01.png
[2]: ./media/storage-table-design-guide/storage-table-design-IMAGE02.png
[3]: ./media/storage-table-design-guide/storage-table-design-IMAGE03.png
[4]: ./media/storage-table-design-guide/storage-table-design-IMAGE04.png
[5]: ./media/storage-table-design-guide/storage-table-design-IMAGE05.png
[6]: ./media/storage-table-design-guide/storage-table-design-IMAGE06.png
[7]: ./media/storage-table-design-guide/storage-table-design-IMAGE07.png
[8]: ./media/storage-table-design-guide/storage-table-design-IMAGE08.png
[9]: ./media/storage-table-design-guide/storage-table-design-IMAGE09.png
[10]: ./media/storage-table-design-guide/storage-table-design-IMAGE10.png
[11]: ./media/storage-table-design-guide/storage-table-design-IMAGE11.png
[12]: ./media/storage-table-design-guide/storage-table-design-IMAGE12.png
[13]: ./media/storage-table-design-guide/storage-table-design-IMAGE13.png
[14]: ./media/storage-table-design-guide/storage-table-design-IMAGE14.png
[15]: ./media/storage-table-design-guide/storage-table-design-IMAGE15.png
[16]: ./media/storage-table-design-guide/storage-table-design-IMAGE16.png
[17]: ./media/storage-table-design-guide/storage-table-design-IMAGE17.png
[18]: ./media/storage-table-design-guide/storage-table-design-IMAGE18.png
[19]: ./media/storage-table-design-guide/storage-table-design-IMAGE19.png
[20]: ./media/storage-table-design-guide/storage-table-design-IMAGE20.png
[21]: ./media/storage-table-design-guide/storage-table-design-IMAGE21.png
[22]: ./media/storage-table-design-guide/storage-table-design-IMAGE22.png
[23]: ./media/storage-table-design-guide/storage-table-design-IMAGE23.png
[24]: ./media/storage-table-design-guide/storage-table-design-IMAGE24.png
[25]: ./media/storage-table-design-guide/storage-table-design-IMAGE25.png
[26]: ./media/storage-table-design-guide/storage-table-design-IMAGE26.png
[27]: ./media/storage-table-design-guide/storage-table-design-IMAGE27.png
[28]: ./media/storage-table-design-guide/storage-table-design-IMAGE28.png
[29]: ./media/storage-table-design-guide/storage-table-design-IMAGE29.png

