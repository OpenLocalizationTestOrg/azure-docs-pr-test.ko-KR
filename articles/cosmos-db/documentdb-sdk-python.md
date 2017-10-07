---
title: "aaaAzure Cosmos DB Python API SDK 및 리소스 | Microsoft Docs"
description: "Python API와 SDK 릴리스 날짜, 사용 중지 날짜 및 hello Azure Cosmos DB Python SDK의 각 버전 간의 변경 내용을 포함 하 여 hello에 대 한 모든에 대해 알아봅니다."
services: cosmos-db
documentationcenter: python
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 3ac344a9-b2fa-4a3f-a4cc-02d287e05469
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/24/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1a164b72d2bd819de87df0229357b82e2177af2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a>Azure Cosmos DB Python SDK: 릴리스 정보 및 리소스
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

<tr><td>**SDK 다운로드**</td><td>[PyPI](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td>**API 설명서**</td><td>[Python API 참조 설명서](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td>**SDK 설치 지침**</td><td>[Python SDK 설치 지침](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td>**TooSDK 영향**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td>**시작**</td><td>[Hello Python SDK 시작](documentdb-python-application.md)</td></tr>

<tr><td>**현재 지원되는 플랫폼**</td><td>[Python 2.7](https://www.python.org/downloads/) 및 [Python 3.5](https://www.python.org/downloads/)</td></tr>
</table></br>

## <a name="release-notes"></a>릴리스 정보
### <a name="a-name220220"></a><a name="2.2.0"/>2.2.0
* ConsistentPrefix라는 새로운 일관성 수준에 대한 지원이 추가되었습니다.


### <a name="a-name210210"></a><a name="2.1.0"/>2.1.0
* 집계 쿼리(COUNT, MIN, MAX, SUM 및 AVG)에 대한 지원이 추가되었습니다.
* Cosmos DB 에뮬레이터에 대해 실행하는 경우 SSL 유효성 검사를 비활성화하기 위한 옵션을 추가했습니다.
* 종속 요청 모듈 toobe 정확히 2.10.0 hello 제한을 제거 합니다.
* 10,100 000RU/s too2500 000RU/s에서 분할 된 컬렉션에 대해 최소 처리량을 적어집니다.
* 저장된 프로시저가 실행되는 동안 스크립트 로깅을 사용할 수 있도록 지원이 추가되었습니다.
* REST API 버전 ' 2017 추락 너무-01-19' 이번 릴리스부터 합니다.

### <a name="a-name201201"></a><a name="2.0.1"/>2.0.1
* Toodocumentation 주석 편집 변경 작업을 수행 합니다.

### <a name="a-name200200"></a><a name="2.0.0"/>2.0.0
* Python 3.5에 대한 지원이 추가되었습니다.
* 요청 모듈을 사용하는 연결 풀링에 대한 지원이 추가되었습니다.
* 세션 일관성에 대한 지원이 추가되었습니다.
* 분할된 컬렉션의 TOP/ORDERBY 쿼리에 대한 지원이 추가되었습니다.

### <a name="a-name190190"></a><a name="1.9.0"/>1.9.0
* 제한된 요청에 대한 재시도 정책 지원이 추가되었습니다. (제한된 요청은 오류 코드 429, 요청 속도가 너무 크다는 예외를 수신합니다.) 기본적으로 Azure Cosmos DB 다시 시도 9 번 각 요청에 대 한 오류 코드 429 오류가 발생 하면 hello retryAfter 시간 hello 응답 헤더에 적용 합니다. 고정 된 다시 시도 간격 시간 수 이제 hello RetryOptions 속성의 일부로 개체에 설정 될 hello ConnectionPolicy hello 다시 시도 대기 중 서버에서 반환 된 tooignore hello retryAfter 시간이 필요한 경우. 이제 azure Cosmos DB 최대 (관계 없이 다시 시도 횟수)가 제한 및 오류 코드: 429 hello 응답을 반환 하는 각 요청에 대 한 30 초까지 기다립니다. 이 이번에는 hello RetryOptions ConnectionPolicy 개체 속성에서에서 재정의 된 될 수도 있습니다.
* Cosmos DB 이제 x-ms-스로틀-다시 시도-횟수 및 반환 x-ms-throttle-retry-wait-time-ms hello 응답 헤더의 모든 요청 toodenote hello 스로틀 수 및 hello cummulative hello 요청 대기 시간 hello 재시도 간격을 다시 시도 하십시오.
* 제거 hello RetryPolicy 클래스 및 (retry_policy) 속성을 해당 하는 hello hello document_client 클래스에 노출 되며 대신 hello RetryOptions 클래스의 속성을 ConnectionPolicy toooverride 사용된 될 수 있는 노출 RetryOptions 클래스를 도입 일부 hello 기본 옵션을 다시 시도 하십시오.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* 다중 영역 데이터베이스 계정에 대 한 추가 된 hello 지원 합니다.

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* 추가 된 hello 문서에 대 한 시간 tooLive(TTL) 기능에 대 한 지원.

### <a name="a-name161161"></a><a name="1.6.1"/>1.6.1
* 버그 수정 관련 tooserver 쪽 tooallow partitionkey 경로에서 특수 문자를 분할 합니다.

### <a name="a-name160160"></a><a name="1.6.0"/>1.6.0
* [분할된 컬렉션](partition-data.md) 및 [사용자 정의 성능 수준](performance-levels.md)이 구현되었습니다. 

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* 추가 해시 & 범위 파티션 확인자 tooassist 여러 파티션에서 분할 응용 프로그램입니다.

### <a name="a-name142142"></a><a name="1.4.2"/>1.4.2
* Upsert를 구현합니다. 새 UpsertXXX 메서드가 toosupport Upsert 기능을 추가 합니다.
* ID 기반 라우팅을 구현합니다. 공용 API 변경 없이 모두 내부에서 변경됩니다.

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* 지리 공간 인덱스를 지원합니다.
* 모든 리소스에 대한 ID 속성의 유효성을 검사합니다. 리소스에 대한 ID는 ?, /, #, \, 문자를 포함하거나 공백으로 끝날 수 없습니다.
* 새 헤더 "인덱스 변환 진행 중" tooResourceResponse를 추가합니다.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* V2 인덱싱 정책을 구현합니다.

### <a name="a-name101101"></a><a name="1.0.1"/>1.0.1
* 프록시 연결을 지원합니다

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* GA SDK.

## <a name="release--retirement-dates"></a>릴리스 및 사용 중지 날짜
Microsoft는 알림을 적어도 제공 **12 개월** 순서 toosmooth hello 전환 tooa 지원/최신 버전의 SDK를 사용 중지 전에 합니다.

새로운 기능 및 기능 및 최적화는 toohello 현재만 추가 그렇게 하면 항상 업그레이드 toohello 최신 SDK 버전을 가능한 한 빨리 권장는 SDK입니다. 

모든 요청 tooCosmos 사용 중지 된 SDK를 사용 하 여 DB hello 서비스에서 거부 됩니다.

> [!WARNING]
> 모든 버전의 이전 tooversion Python에 대 한 Azure DocumentDB SDK hello **1.0.0** 에 사용 중지 될 예정 **2016 년 2 월 29 일**합니다. 
> 
> 

<br/>

| 버전 | 릴리스 날짜 | 사용 중지 날짜 |
| --- | --- | --- |
| [2.2.0](#2.2.0) |2017년 5월 10일 |--- |
| [2.1.0](#2.1.0) |2017년 5월 1일 |--- |
| [2.0.1](#2.0.1) |2016년 10월 30일 |--- |
| [2.0.0](#2.0.0) |2016년 9월 29일 |--- |
| [1.9.0](#1.9.0) |2016년 7월 7일 |--- |
| [1.8.0](#1.8.0) |2016년 6월 14일 |--- |
| [1.7.0](#1.7.0) |2016년 4월 26일 |--- |
| [1.6.1](#1.6.1) |2016년 4월 8일 |--- |
| [1.6.0](#1.6.0) |2016년 3월 29일 |--- |
| [1.5.0](#1.5.0) |2016년 1월 3일 |--- |
| [1.4.2](#1.4.2) |2015년 10월 6일 |--- |
| [1.4.1](#1.4.1) |2015년 10월 6일 |--- |
| [1.2.0](#1.2.0) |2015년 8월 6일 |--- |
| [1.1.0](#1.1.0) |2015년 7월 9일 |--- |
| [1.0.1](#1.0.1) |2015년 5월 25일 |--- |
| [1.0.0](#1.0.0) |2015년 4월 7일 |--- |
| 0.9.4-prelease |2015년 1월 14일 |2016년 2월 29일 |
| 0.9.3-prelease |2014년 12월 9일 |2016년 2월 29일 |
| 0.9.2-prelease |2014년 11월 25일 |2016년 2월 29일 |
| 0.9.1-prelease |2014년 9월 23일 |2016년 2월 29일 |
| 0.9.0-prelease |2014년 8월 21일 |2016년 2월 29일 |

## <a name="faq"></a>FAQ
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>참고 항목
Cosmos DB에 대해 자세히 toolearn 참조 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 서비스 페이지. 

