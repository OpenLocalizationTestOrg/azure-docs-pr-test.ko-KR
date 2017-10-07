---
title: "Cosmos DB Gremlin 지원 aaaAzure | Microsoft Docs"
description: "기능 및 단계는 Apache TinkerPop에서 Gremlin 언어 hello에 대 한 자세한 내용은 Azure Cosmos DB에서 사용할 수"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
tags: 
ms.assetid: 6016ccba-0fb9-4218-892e-8f32a1bcc590
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/10/2017
ms.author: denlee
ms.openlocfilehash: f8c2ce50c6946e971f56fe1f3838b0899cb2ad8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-gremlin-graph-support"></a>Azure Cosmos DB Gremlin 그래프 지원
Azure Cosmos DB는 [Apache Tinkerpop](http://tinkerpop.apache.org)의 그래프 통과 언어로서, 그래프 엔터티를 만들고 그래프 쿼리를 수행하기 위한 Graph API인 [Gremlin](http://tinkerpop.apache.org/docs/current/reference/#graph-traversal-steps)을 지원합니다. Hello Gremlin 언어 toocreate 그래프 엔터티 (꼭지점 및 가장자리)를 사용 하 여 해당 엔터티 내에서 속성을 수정 및 쿼리 및 트래버스를 수행 엔터티 삭제 수 있습니다. 

Azure Cosmos DB는 toograph 데이터베이스 엔터프라이즈 지원 기능을 제공합니다. 여기에는 전역 배포, 저장소 및 처리량의 독립적 확장, 예측 가능한 1자리 밀리초 단위 대기 시간, 자동 인덱싱 및 99.99% SLA가 포함됩니다. Azure Cosmos DB TinkerPop/Gremlin를 지원 하므로 toomake 코드를 변경 하지 않고도 다른 그래프 데이터베이스를 사용 하 여 작성 된 응용 프로그램을 쉽게 마이그레이션할 수 있습니다. 또한 Gremlin 지원을 통해, Azure Cosmos DB는 [Apache Spark GraphX](http://spark.apache.org/graphx/)와 같은 TinkerPop 지원 분석 프레임워크와 원활하게 통합됩니다. 

이 문서에서는 Gremlin의 간략 한 설명이 제공 하 고 hello Gremlin 기능 및 Graph API 지원의 hello 미리 보기에서 지원 되는 단계를 열거 합니다.

## <a name="gremlin-by-example"></a>Gremlin 예제
어떻게 Gremlin에서 쿼리를 표현할 수 있는 샘플 그래프 toounderstand을 사용 합니다. hello 다음 그림은 사용자, 관심사에 및 그래프의 hello 형태로 장치에 대 한 데이터를 관리 하는 비즈니스 응용 프로그램.  

![사람, 장치 및 관심 분야를 보여 주는 샘플 데이터베이스](./media/gremlin-support/sample-graph.png) 

이 그래프에 꼭 짓 점 형식 ("레이블" Gremlin에서)를 수행 하는 hello:

- 사람: hello 그래프의 로빈, Thomas, 및 Ben 세 명
- 관심 분야:이 예제에서는 관심을 hello Football의 게임
- 사용자를 사용 하는 장치의 경우: hello 장치
- Hello 장치에서 실행 되는 운영 체제: hello 운영 체제

म 가장자리 유형/레이블 뒤 hello 통해 이러한 엔터티 사이의 hello 관계를 나타냅니다.

- Knows: 예: "Thomas knows Robin"
- 이 그래프에 hello 사람의 예를 들어 "Ben는 데 관심이 Football" 관심된: toorepresent hello 관심사
- 랩톱 RunsOS: hello Windows 운영 체제를 실행
- 용도: toorepresent 개인이 장치를 사용 합니다. 예를 들어 Robin은 일련 번호가 77인 Motorola 휴대폰을 사용합니다.

Hello를 사용 하 여이 그래프에 대해 일부 작업을 실행 해 보겠습니다 [Gremlin 콘솔](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console)합니다. 또한 Gremlin 드라이버를 사용 하 여 사용자가 선택한 (Java, Node.js, Python 또는.NET) hello 플랫폼에서 이러한 작업을 수행할 수 있습니다.  Azure Cosmos DB에서 지원 되는 기능 살펴보기 전에 hello 구문을 사용 하 여 친숙 한 몇 가지 예제 tooget에서 살펴보겠습니다.

먼저 CRUD를 살펴보겠습니다. hello 다음 Gremlin 문은 hello "Thomas" 꼭지점에 삽입 hello 그래프:

```
:> g.addV('person').property('id', 'thomas.1').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44)
```

다음으로 hello Gremlin 문 다음에 Thomas 사이의 로빈 "알고 있는" edge를 삽입 합니다.

```
:> g.V('thomas.1').addE('knows').to(g.V('robin.1'))
```

hello 다음 쿼리 hello "person" 꼭지점 내림차순 반환의 첫 번째 이름:
```
:> g.V().hasLabel('person').order().by('firstName', decr)
```

여기서 그래프 빛은 필요할 때 "어떤 운영 체제 Thomas의 friend 사용 합니까?" 같은 tooanswer 질문 합니다. 이 간단한 Gremlin 순회 tooget 정보 hello 그래프에서 실행할 수 있습니다.

```
:> g.V('thomas.1').out('knows').out('uses').out('runsos').group().by('name').by(count())
```
이제 Azure Cosmos DB에서 Gremlin 개발자에게 제공하는 기능을 살펴보겠습니다.

## <a name="gremlin-features"></a>Gremlin 기능
TinkerPop은 광범위한 그래프 기술을 지원하는 표준입니다. 따라서 있기 표준 용어 toodescribe 그래프 공급자 어떤 기능을 제공 합니다. Azure Cosmos DB는 여러 서버 또는 클러스터에서 분할될 수 있는 지속적이고 높은 동시성을 갖는 쓰기 가능한 그래프 데이터베이스를 제공합니다. 

hello 다음 표에 Azure Cosmos DB에서 구현 되는 hello TinkerPop 기능. 

| Category | Azure Cosmos DB 구현 |  참고 사항 | 
| --- | --- | --- |
| 그래프 기능 | 미리 보기에서 Persistence 및 ConcurrentAccess를 제공합니다. 디자인 된 toosupport 트랜잭션 | Hello Spark 커넥터를 통해 컴퓨터 메서드를 구현할 수 있습니다. |
| 변수 기능 | 부울, 정수, 바이트, Double, Float, Long, 문자열을 지원합니다. | 기본 형식을 지원하고, 데이터 모델을 통해 복잡한 형식과 호환됩니다. |
| 꼭짓점 기능 | RemoveVertices, MetaProperties, AddVertices, MultiProperties, StringIds, UserSuppliedIds, AddProperty, RemoveProperty를 지원합니다.  | 꼭짓점 만들기, 수정 및 삭제를 지원합니다. |
| 꼭짓점 속성 기능 | StringIds, UserSuppliedIds, AddProperty, RemoveProperty, BooleanValues, ByteValues, DoubleValues, FloatValues, IntegerValues, LongValues, StringValues | 꼭짓점 속성 만들기, 수정 및 삭제를 지원합니다. |
| 에지 기능 | AddEges, RemoveEdges, StringIds, UserSuppliedIds, AddProperty, RemoveProperty | 에지 만들기, 수정 및 삭제를 지원합니다. |
| 에지 속성 기능 | Properties, BooleanValues, ByteValues, DoubleValues, FloatValues, IntegerValues, LongValues, StringValues | 에지 속성 만들기, 수정 및 삭제를 지원합니다. |

## <a name="gremlin-wire-format-graphson"></a>Gremlin 통신 형식: GraphSON

Azure Cosmos DB hello를 사용 하 여 [GraphSON 형식](https://github.com/thinkaurelius/faunus/wiki/GraphSON-Format) Gremlin 작업에서 결과 반환할 때. GraphSON는 hello Gremlin 꼭지점, 모서리 및 JSON을 사용 하 여 속성 (단일 및 다중 값 속성)을 나타내기 위한 표준 형식입니다. 

예를 들어 hello 다음 코드 조각 표시 GraphSON 꼭 짓 점 *toohello 클라이언트 반환* Azure Cosmos DB에서 합니다. 

```json
  {
    "id": "a7111ba7-0ea1-43c9-b6b2-efc5e3aea4c0",
    "label": "person",
    "type": "vertex",
    "outE": {
      "knows": [
        {
          "id": "3ee53a60-c561-4c5e-9a9f-9c7924bc9aef",
          "inV": "04779300-1c8e-489d-9493-50fd1325a658"
        },
        {
          "id": "21984248-ee9e-43a8-a7f6-30642bc14609",
          "inV": "a8e3e741-2ef7-4c01-b7c8-199f8e43e3bc"
        }
      ]
    },
    "properties": {
      "firstName": [
        {
          "value": "Thomas"
        }
      ],
      "lastName": [
        {
          "value": "Andersen"
        }
      ],
      "age": [
        {
          "value": 45
        }
      ]
    }
  }
```

꼭 짓 점에 대해 GraphSON에서 사용 하는 hello 속성 hello 다음과 같습니다.

| 속성 | 설명 |
| --- | --- |
| id | hello 꼭 짓 점에 대해 hello ID입니다. (해당 하는 경우 _partition hello 값 조합) 내에서 고유 해야 합니다. |
| label | hello 꼭 짓 점에 hello 레이블입니다. 사용 하는 선택적인 toodescribe hello 엔터티 형식입니다. |
| type | 비 그래프 문서에서 사용 되는 toodistinguish 꼭지점 |
| properties | 꼭 짓 점 hello와 연관 된 사용자 정의 속성 모음에 없습니다. 각 속성에는 값이 여러 개 있을 수 있습니다. |
| _partition(구성 가능) | hello 꼭 짓 점에 hello 파티션 키입니다. 그래프 아웃 사용된 tooscale toomultiple 서버 수 있습니다. |
| outE | 여기에는 꼭짓점의 바깥 에지 목록이 포함됩니다. 꼭지점을 사용 하 여 hello 인접 정보를 저장 하는 작업은 탐색을 신속히 실행할 수 있습니다. 에지는 해당 레이블을 기준으로 그룹화됩니다. |

hello 가장자리 hello hello 그래프의 탐색 tooother 부분과 정보 toohelp 다음을 포함 합니다.

| 속성 | 설명 |
| --- | --- |
| id | hello 가장자리에 대 한 hello ID입니다. (해당 하는 경우 _partition hello 값 조합) 내에서 고유 해야 합니다. |
| label | hello 가장자리의 hello 레이블입니다. 이 속성은 선택 사항이 고 사용 된 toodescribe hello 관계 유형입니다. |
| inV | 여기에는 에지의 모든 꼭지점 목록이 포함됩니다. Hello 가장자리와 hello 인접 정보를 저장 하는 작업은 탐색을 신속히 실행할 수 있습니다. 꼭짓점은 해당 레이블을 기준으로 그룹화됩니다. |
| properties | Hello 가장자리와 연결 된 사용자 지정 속성의 모음입니다. 각 속성에는 값이 여러 개 있을 수 있습니다. |

각 속성은 배열 내에 여러 값을 저장할 수 있습니다. 

| 속성 | 설명 |
| --- | --- |
| 값 | hello hello 속성 값

## <a name="gremlin-partitioning"></a>Gremlin 분할

Azure Cosmos DB에서 그래프는 저장소 및 처리량(정규화된 초당 요청 수로 표현) 측면에서 독립적으로 확장될 수 있는 컨테이너 내에 저장됩니다. 각 컨테이너는 관련 데이터에 대한 논리적 파티션 경계를 결정하는 선택 사항이면서 권장되는 파티션 키 속성을 정의해야 합니다. 모든 꼭짓점/에지에는 해당 파티션 키 값 내의 엔터티에 대해 고유한 `id` 속성이 있어야 합니다. hello 세부 정보에 대해서는 설명 [Azure Cosmos DB에서 분할](partition-data.md)합니다.

Gremlin 작업은 Azure Cosmos DB에서 여러 파티션에 걸쳐 분산된 그래프 데이터에 원활하게 작동합니다. 그러나 일반적으로 쿼리에 필터로 사용 되는 사용자 그래프에 많은 고유 값 및 유사한 주파수의 이러한 값에 액세스를 위해 toochoose 파티션 키를 권장 합니다. 

## <a name="gremlin-steps"></a>Gremlin 단계
이제 살펴보겠습니다 hello Azure Cosmos DB에서 지 원하는 Gremlin 단계입니다. Gremlin에 대한 전체 참조는 [TinkerPop 참조](http://tinkerpop.apache.org/docs/current/reference)를 참조하세요.

| 단계 | 설명 | TinkerPop 3.2 설명서 | 참고 사항 |
| --- | --- | --- | --- |
| `addE` | 두 꼭짓점 사이에 에지를 추가합니다. | [addE 단계](http://tinkerpop.apache.org/docs/current/reference/#addedge-step) | |
| `addV` | 꼭 짓 점 toohello 그래프 추가 | [addV 단계](http://tinkerpop.apache.org/docs/current/reference/#addvertex-step) | |
| `and` | 모든 hello 이동을 값을 반환 하는 Ensurest | [and 단계](http://tinkerpop.apache.org/docs/current/reference/#and-step) | |
| `as` | 단계 변조기 tooassign 단계의 변수 toohello 출력 | [as 단계](http://tinkerpop.apache.org/docs/current/reference/#as-step) | |
| `by` | `group` 및 `order`에서 사용되는 단계 변조기 | [by 단계](http://tinkerpop.apache.org/docs/current/reference/#by-step) | |
| `coalesce` | 결과 반환 하는 hello 첫 번째 순회를 반환 합니다. | [coalesce 단계](http://tinkerpop.apache.org/docs/current/reference/#coalesce-step) | |
| `constant` | 상수 값을 반환합니다. `coalesce`에 사용됩니다.| [constant 단계](http://tinkerpop.apache.org/docs/current/reference/#constant-step) | |
| `count` | Hello 통과에서 hello 개수를 반환합니다. | [count 단계](http://tinkerpop.apache.org/docs/current/reference/#count-step) | |
| `dedup` | 반환 값을 hello 중복 항목을 제거 hello | [dedup 단계](http://tinkerpop.apache.org/docs/current/reference/#dedup-step) | |
| `drop` | 삭제 hello 값 (꼭 짓 점/가장자리에서) | [drop 단계](http://tinkerpop.apache.org/docs/current/reference/#drop-step) | |
| `fold` | 결과의 hello 집계를 계산 하는 장벽으로 작동 하며| [fold 단계](http://tinkerpop.apache.org/docs/current/reference/#fold-step) | |
| `group` | 그룹 hello hello 레이블을 지정에 따라 값| [group 단계](http://tinkerpop.apache.org/docs/current/reference/#group-step) | |
| `has` | Toofilter 속성, 꼭지점 및 가장자리를 사용 합니다. `hasLabel`, `hasId`, `hasNot` 및 `has` 변형을 지원합니다. | [has 단계](http://tinkerpop.apache.org/docs/current/reference/#has-step) | |
| `inject` | 스트림에 값을 삽입합니다.| [inject 단계](http://tinkerpop.apache.org/docs/current/reference/#inject-step) | |
| `is` | Tooperform 부울 식을 사용 하는 필터 사용 | [is 단계](http://tinkerpop.apache.org/docs/current/reference/#is-step) | |
| `limit` | 항목 수가 toolimit hello 탐색에서 사용| [limit 단계](http://tinkerpop.apache.org/docs/current/reference/#limit-step) | |
| `local` | 로컬이 래핑합니다 순회, 비슷한 tooa 하위 쿼리에의 한 섹션 | [local 단계](http://tinkerpop.apache.org/docs/current/reference/#local-step) | |
| `not` | 필터의 tooproduce hello 부정을 사용 | [not 단계](http://tinkerpop.apache.org/docs/current/reference/#not-step) | |
| `optional` | 반환 결과의 지정 된 hello hello 반환 다른 결과 나타낼 경우 통과 hello 호출 하는 요소 | [optional 단계](http://tinkerpop.apache.org/docs/current/reference/#optional-step) | |
| `or` | Hello 순회 중 하나 이상 반환 값 | [or 단계](http://tinkerpop.apache.org/docs/current/reference/#or-step) | |
| `order` | 정렬 순서를 지정 하는 hello에서 결과 반환 | [order 단계](http://tinkerpop.apache.org/docs/current/reference/#order-step) | |
| `path` | Hello 순회 반환 hello 전체 경로 | [path 단계](http://tinkerpop.apache.org/docs/current/reference/#path-step) | |
| `project` | 맵으로 프로젝트 hello 속성 | [project 단계](http://tinkerpop.apache.org/docs/current/reference/#project-step) | |
| `properties` | Hello에 대 한 속성을 반환 hello 레이블 지정 | [properties 단계](http://tinkerpop.apache.org/docs/current/reference/#properties-step) | |
| `range` | 필터 toohello 값의 범위 지정| [range 단계](http://tinkerpop.apache.org/docs/current/reference/#range-step) | |
| `repeat` | Hello에 대 한 hello 단계를 반복 횟수를 지정 합니다. 반복에 사용됩니다. | [repeat 단계](http://tinkerpop.apache.org/docs/current/reference/#repeat-step) | |
| `sample` | Toosample 결과 hello 순회를 사용합니다. | [sample 단계](http://tinkerpop.apache.org/docs/current/reference/#sample-step) | |
| `select` | Tooproject 결과 hello 순회를 사용합니다. |  [select 단계](http://tinkerpop.apache.org/docs/current/reference/#select-step) | |
| `store` | Hello 통과에서 비 블록 킹 집계에 사용 된 | [store 단계](http://tinkerpop.apache.org/docs/current/reference/#store-step) | |
| `tree` | 꼭짓점에서의 경로를 트리로 집계합니다. | [tree 단계](http://tinkerpop.apache.org/docs/current/reference/#tree-step) | |
| `unfold` | 반복기를 단계로 언롤합니다.| [unfold 단계](http://tinkerpop.apache.org/docs/current/reference/#unfold-step) | |
| `union` | 여러 순회의 결과를 병합합니다.| [union 단계](http://tinkerpop.apache.org/docs/current/reference/#union-step) | |
| `V` | Hello 꼭지점 및 가장자리 사이의 탐색 하는 데 필요한 단계 포함 `V`, `E`, `out`, `in`, `both`, `outE`, `inE`, `bothE`, `outV`, `inV`, `bothV`, 및 `otherV` 에 대 한 | [vertex 단계](http://tinkerpop.apache.org/docs/current/reference/#vertex-steps) | |
| `where` | Toofilter 결과 hello 순회를 사용합니다. `eq`, `neq`, `lt`, `lte`, `gt`, `gte` 및 `between` 연산자 지원  | [where 단계](http://tinkerpop.apache.org/docs/current/reference/#where-step) | |

Azure Cosmos DB의 쓰기 최적화 엔진은 기본적으로 꼭짓점 및 에지 내의 모든 속성에 대한 자동 인덱싱을 지원합니다. 따라서 쿼리 범위 쿼리, 정렬, 필터를 사용 하거나 속성에 대해 집계 hello 인덱스에서 처리 되 고 효율적으로 처리 합니다. Azure Cosmos DB에서 인덱싱이 작동하는 방식에 대한 자세한 내용은 [스키마 독립적 인덱싱](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf)을 참조하세요.

## <a name="next-steps"></a>다음 단계
* [SDK를 사용하여](create-graph-dotnet.md) 그래프 응용 프로그램 빌드 시작 
* [Azure Cosmos DB 그래프 지원](graph-introduction.md)에 대해 자세히 알아보기
