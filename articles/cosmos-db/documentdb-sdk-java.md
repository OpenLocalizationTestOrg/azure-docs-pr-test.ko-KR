---
title: "Azure Cosmos DB: DocumentDB Java API, SDK 및 리소스 | Microsoft Docs"
description: "Java API와 SDK 릴리스 날짜, 사용 중지 날짜 및 hello Azure Cosmos DB DocumentDB Java SDK의 각 버전 간의 변경 내용을 포함 하 여 hello에 대 한 모든에 대해 알아봅니다."
services: cosmos-db
documentationcenter: java
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 7861cadf-2a05-471a-9925-0fec0599351b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 07/11/2017
ms.author: khdang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8ef43ebeb7ae1bfc55512c4a7489c1b7930122d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-java-sdk-release-notes-and-resources"></a>Azure Cosmos DB: DocumentDB Java SDK 릴리스 정보 및 리소스
> [!div class="op_single_selector"]
> * [.NET](documentdb-sdk-dotnet.md)
> * [.NET 변경 피드](documentdb-sdk-dotnet-changefeed.md)
> * [.NET Core](documentdb-sdk-dotnet-core.md)
> * [Node.JS](documentdb-sdk-node.md)
> * [Java](documentdb-sdk-java.md)
> * [Python](documentdb-sdk-python.md)
> * [REST (영문)](https://docs.microsoft.com/rest/api/documentdb/)
> * [REST 리소스 공급자](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td>**SDK 다운로드**</td><td>[Maven](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td>**API 설명서**</td><td>[Java API 참조 설명서](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td>**TooSDK 영향**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td>**시작**</td><td>[Hello Java SDK 시작](documentdb-java-get-started.md)</td></tr>

<tr><td>**웹앱 자습서**</td><td>[Azure Cosmos DB를 사용한 웹 응용 프로그램 개발](documentdb-java-application.md)</td></tr>

<tr><td>**현재 지원되는 런타임**</td><td>[JDK 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a>릴리스 정보

### <a name="a-name11201120"></a><a name="1.12.0"/>1.12.0
* 파티션 중를 처리 하는 중요 한 버그 수정 toorequest 분할 합니다.
* 강력한 hello 및 BoundedStaleness 일관성 수준 관련 문제를 해결 합니다.

### <a name="a-name11101110"></a><a name="1.11.0"/>1.11.0
* ConsistentPrefix라는 새로운 일관성 수준에 대한 지원이 추가되었습니다.
* 세션 모드에서 컬렉션을 읽을 때 발생하는 버그를 수정했습니다.

### <a name="a-name11001100"></a><a name="1.10.0"/>1.10.0
* 초당 2,500 RU 및 초당 100 RU의 규모 조정 능력을 통해 분할된 컬렉션을 지원합니다.
* 일부 쿼리에서 NullRef 예외가 발생할 수 있는 네이티브 어셈블리 hello에서에서 버그를 수정 합니다.

### <a name="a-name196196"></a><a name="1.9.6"/>1.9.6
* 게이트웨이 모드에서 쿼리에 대 한 예외를 일으킬 수 있는 hello 쿼리 엔진 구성에서 버그를 수정 합니다.
* 컬렉션을 만든 후 즉시 요청에 대 한 "소유자 리소스를 찾을 수 없습니다." 예외를 일으킬 수 있는 hello 세션 컨테이너에 몇 가지 버그도 수정 되었습니다.

### <a name="a-name195195"></a><a name="1.9.5"/>1.9.5
* 집계 쿼리(COUNT, MIN, MAX, SUM 및 AVG)에 대한 지원이 추가되었습니다. [집계 지원](documentdb-sql-query.md#Aggregates)을 참조하세요.
* 변경 피드에 대한 지원이 추가되었습니다.
* RequestOptions.setPopulateQuotaInfo를 통한 컬렉션 할당량 정보에 대한 지원이 추가되었습니다.
* RequestOptions.setScriptLoggingEnabled를 통한 저장 프로시저 스크립트에 대한 지원이 추가되었습니다.
* 제한 오류가 발생할 때 DirectHttps 모드의 쿼리가 중단될 수 있는 버그를 수정했습니다.
* 세션 일관성 모드의 버그를 수정했습니다.
* 요청 속도가 높은 경우 HttpContext에서 NullReferenceException을 유발할 수 있는 버그를 수정했습니다.
* DirectHttps 모드의 성능이 향상되었습니다.

### <a name="a-name194194"></a><a name="1.9.4"/>1.9.4
* ConnectionPolicy.setProxy() API와 함께 샘플 클라이언트 인스턴스 기반 프록시 지원이 추가되었습니다.
* 추가 된 DocumentClient.close() API tooproperly DocumentClient 인스턴스 종료 합니다.
* 쿼리 성능이 향상된 hello 쿼리 계획 hello 게이트웨이 대신 hello 네이티브 어셈블리에서 파생 하 여 직접 연결 모드에 있습니다.
* FAIL_ON_UNKNOWN_PROPERTIES 설정 false = 사용자가 자신의 POJO에 JsonIgnoreProperties toodefine 필요 하지 않습니다.
* 로깅 toouse SLF4J를 리팩터링 합니다.
* 일관성 판독기의 몇 가지 버그를 수정했습니다.

### <a name="a-name193193"></a><a name="1.9.3"/>1.9.3
* 직접 연결 모드에서 hello 연결 관리 tooprevent 연결 누수에서 버그를 수정 합니다.
* NullReferenece 예외가 throw 될 수 있는 hello TOP 쿼리에서 버그를 수정 합니다.
* Hello hello 내부 캐시에 대 한 네트워크 호출 수를 줄이면 성능이 향상 되었습니다.
* DocumentClientException에 상태 코드 ActivityID 및 요청 URI를 추가하여 문제 해결을 개선했습니다.

### <a name="a-name192192"></a><a name="1.9.2"/>1.9.2
* 안정성에 대 한 hello 연결 관리 문제를 해결 합니다.

### <a name="a-name191191"></a><a name="1.9.1"/>1.9.1
* BoundedStaleness 일관성 수준에 대한 지원이 추가되었습니다.
* 분할된 컬렉션의 CRUD 작업에 대한 직접 연결 지원이 추가되었습니다.
* SQL을 사용하여 데이터베이스를 쿼리할 때의 버그가 수정되었습니다.
* 여기서 세션 토큰이 설정 되는 경우 올바르게 hello 세션 캐시에는 버그를 수정 합니다.

### <a name="a-name190190"></a><a name="1.9.0"/>1.9.0
* 파티션 간 병렬 쿼리에 대한 지원이 추가되었습니다.
* 분할된 컬렉션의 TOP/ORDER BY 쿼리에 대한 지원이 추가되었습니다.
* 강력한 일관성에 대한 지원이 추가되었습니다.
* 직접 연결을 사용할 때 이름 기반 요청에 대한 지원이 추가되었습니다.
* 고정된 toomake ActivityId 전체 하 게 유지 일관 된 모든 요청 다시 시도 합니다.
* 버그를 수정 hello 사용 하 여 컬렉션을 다시 만들 때 toohello 세션 캐시와 관련 된 동일한 이름입니다.
* 지역 펜싱 공간 쿼리에 대한 컬렉션 인덱싱 정책을 지정하는 동안 Polygon 및 LineString 데이터 형식이 추가되었습니다.
* Java 1.8용 Java 문서 관련 문제가 해결되었습니다.

### <a name="a-name181181"></a><a name="1.8.1"/>1.8.1
* PartitionKeyDefinitionMap에서 버그를 수정 toocache 단일 파티션 컬렉션 및 추가 만들지 인출 파티션 키를 요청 합니다.
* 잘못 된 파티션 키 값이 제공 하는 경우 버그 toonot 다시 시도 고정 합니다.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* 다중 영역 데이터베이스 계정에 대 한 추가 된 hello 지원 합니다.
* 자동 다시 시도 최대 옵션 toocustomize hello로 제한 된 요청에 대 한 지원 추가 재시도 횟수와 최대 대기 시간을 다시 시도 하십시오.  RetryOptions와 ConnectionPolicy.getRetryOptions()을 참조하세요.
* IPartitionResolver 기반 사용자 지정 파티셔닝 코드의 사용이 중단되었습니다. 보다 큰 저장소 및 처리량에는 파티션된 컬렉션을 사용하세요.

### <a name="a-name171171"></a><a name="1.7.1"/>1.7.1
* 제한에 대한 재시도 정책 지원이 추가되었습니다.  

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* 문서에 대 한 시간 toolive (TTL) 지원이 추가 되었습니다.

### <a name="a-name160160"></a><a name="1.6.0"/>1.6.0
* [분할된 컬렉션](partition-data.md) 및 [사용자 정의 성능 수준](performance-levels.md)이 구현되었습니다.

### <a name="a-name151151"></a><a name="1.5.1"/>1.5.1
* 다른 Sdk와 일치 하는 little endian toobe HashPartitionResolver toogenerate 해시 값에서 버그를 수정 합니다.

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* 추가 해시 & 범위 파티션 확인자 tooassist 여러 파티션에서 분할 응용 프로그램입니다.

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0
* Upsert를 구현합니다. 새 upsertXXX 메서드가 toosupport Upsert 기능을 추가 합니다.
* ID 기반 라우팅을 구현합니다. 공용 API 변경 없이 모두 내부에서 변경됩니다.

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0
* 릴리스 건너뛴 정렬을 다른 Sdk 사용 하 여 toobring 버전 번호

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* 지리 공간 인덱스 지원
* 모든 리소스에 대한 ID 속성의 유효성을 검사합니다. 리소스에 대한 ID는 ?, /, #, \, 문자를 포함하거나 공백으로 끝날 수 없습니다.
* 새 헤더 "인덱스 변환 진행 중" tooResourceResponse를 추가합니다.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* V2 인덱싱 정책 구현

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* GA SDK

## <a name="release--retirement-dates"></a>릴리스 및 사용 중지 날짜
Microsoft는 알림을 적어도 제공 **12 개월** 순서 toosmooth hello 전환 tooa 지원/최신 버전의 SDK를 사용 중지 전에 합니다.

새로운 기능 및 기능 및 최적화는 toohello 현재만 추가 그렇게 하면 항상 업그레이드 toohello 최신 SDK 버전을 가능한 한 빨리 권장는 SDK입니다.

모든 요청 tooCosmos 사용 중지 된 SDK를 사용 하 여 DB hello 서비스에서 거부 됩니다.

> [!WARNING]
> 모든 버전의 Java 이전 tooversion에 대 한 DocumentDB SDK hello **1.0.0** 에 사용 중지 될 예정 **2016 년 2 월 29 일**합니다.
> 
> 

<br/>

| 버전 | 릴리스 날짜 | 사용 중지 날짜 |
| --- | --- | --- |
| [1.12.0](#1.12.0) |2017년 7월 11일 |--- |
| [1.11.0](#1.11.0) |2017년 5월 10일 |--- |
| [1.10.0](#1.10.0) |2017년 3월 11일 |--- |
| [1.9.6](#1.9.6) |2017년 2월 21일 |--- |
| [1.9.5](#1.9.5) |2017년 1월 31일 |--- |
| [1.9.4](#1.9.4) |2016년 11월 24일 |--- |
| [1.9.3](#1.9.3) |2016년 10월 30일 |--- |
| [1.9.2](#1.9.2) |2016년 10월 28일 |--- |
| [1.9.1](#1.9.1) |2016년 10월 26일 |--- |
| [1.9.0](#1.9.0) |2016년 10월 3일 |--- |
| [1.8.1](#1.8.1) |2016년 6월 30일 |--- |
| [1.8.0](#1.8.0) |2016년 6월 14일 |--- |
| [1.7.1](#1.7.1) |2016년 4월 30일 |--- |
| [1.7.0](#1.7.0) |2016년 4월 27일 |--- |
| [1.6.0](#1.6.0) |2016년 3월 29일 |--- |
| [1.5.1](#1.5.1) |2015년 12월 31일 |--- |
| [1.5.0](#1.5.0) |2015년 12월 4일 |--- |
| [1.4.0](#1.4.0) |2015년 10월 5일 |--- |
| [1.3.0](#1.3.0) |2015년 10월 5일 |--- |
| [1.2.0](#1.2.0) |2015년 8월 5일 |--- |
| [1.1.0](#1.1.0) |2015년 7월 9일 |--- |
| [1.0.1](#1.0.1) |2015년 5월 12일 |--- |
| [1.0.0](#1.0.0) |2015년 4월 7일 |--- |
| 0.9.5-prelease |2015년 3월 9일 |2016년 2월 29일 |
| 0.9.4-prelease |2015년 2월 17일 |2016년 2월 29일 |
| 0.9.3-prelease |2015년 1월 13일 |2016년 2월 29일 |
| 0.9.2-prelease |2014년 12월 19일 |2016년 2월 29일 |
| 0.9.1-prelease |2014년 12월 19일 |2016년 2월 29일 |
| 0.9.0-prelease |2014년 12월 10일 |2016년 2월 29일 |

## <a name="faq"></a>FAQ
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>참고 항목
Cosmos DB에 대해 자세히 toolearn 참조 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 서비스 페이지.

