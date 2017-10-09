---
title: "aaaAzure Cosmos DB Node.js API SDK 및 리소스 | Microsoft Docs"
description: "Node.js API와 SDK 릴리스 날짜, 사용 중지 날짜 및 hello Azure Cosmos DB Node.js SDK의 각 버전 간의 변경 내용을 포함 하 여 hello에 대 한 모든에 대해 알아봅니다."
services: cosmos-db
documentationcenter: nodejs
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 9d5621fa-0e11-4619-a28b-a19d872bcf37
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d450b9a9ea7b0f4717ddae8940121fc458ea3744
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a>Azure Cosmos DB Node.js SDK: 릴리스 정보 및 리소스
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

<tr><td>**SDK 다운로드**</td><td>[NPM](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td>**API 설명서**</td><td>[Node.js API 참조 설명서](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td>**SDK 설치 지침**</td><td>[설치 지침](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td>**TooSDK 영향**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td>**샘플**</td><td>[Node.js 코드 샘플](documentdb-nodejs-samples.md)</td></tr>

<tr><td>**시작 자습서**</td><td>[Node.js SDK hello로 시작](documentdb-nodejs-get-started.md)</td></tr>

<tr><td>**웹앱 자습서**</td><td>[Azure Cosmos DB를 사용하여 Node.js 웹 응용 프로그램 빌드](documentdb-nodejs-application.md)</td></tr>

<tr><td>**현재 지원되는 플랫폼**</td><td> 
[Node.js v6.x](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[Node.js v4.2.0](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[Node.js v0.12](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</td></tr>
</table></br>

## <a name="release-notes"></a>릴리스 정보

### <a name="1.12.2"/>1.12.2</a>
*   npm 설명서가 수정되었습니다.

### <a name="1.12.1"/>1.12.1</a>
* 관련된 문서에 특수 유니코드 문자(LS, PS)가 있는 executeStoredProcedure의 버그를 수정했습니다.
* Hello 파티션 키의 유니코드 문자를 사용 하 여 문서를 처리 하는 버그를 수정 합니다.
* Hello 이름 미디어를 사용 하 여 컬렉션을 만들기에 대 한 고정된 지원 합니다. Github 문제 #114.
* 권한 부여 토큰에 대한 지원을 수정했습니다. Github 문제 #178.

### <a name="1.12.0"/>1.12.0</a>
* ConsistentPrefix라고 하는 새로운 [일관성 수준](consistency-levels.md)에 대한 지원이 추가되었습니다.
* UriFactory에 대한 지원이 추가되었습니다.
* 유니코드 지원 버그를 수정했습니다. GitHub 문제 #171.

### <a name="1.11.0"/>1.11.0</a>
* 집계 쿼리 (COUNT, MIN, MAX, SUM 및 AVG)에 대 한 추가 된 hello 지원 합니다.
* 에 대 한 병렬 처리 수준 크로스 파티션 쿼리를 제어 하기 위한 추가 된 hello 옵션입니다.
* Cosmos DB Azure 에뮬레이터에 대해 실행할 때 SSL 유효성 검사를 비활성화 하기 위한 추가 된 hello 옵션입니다.
* 10,100 000RU/s too2500 000RU/s에서 분할 된 컬렉션에 대해 최소 처리량을 적어집니다.
* 단일 파티션 컬렉션에 대 한 고정된 hello 연속 작업의 토큰 버그입니다. Github 문제 #107.
* 단일 매개 변수 형태로 0 처리 고정된 hello executeStoredProcedure 버그입니다. Github 문제 #155.

### <a name="1.10.2"/>1.10.2</a>
* 고정 된 사용자 에이전트 헤더 tooinclude hello SDK 버전입니다.
* 사소한 코드 정리입니다.

### <a name="1.10.1"/>1.10.1</a>
* SDK tootarget hello emulator(hostname=localhost) hello를 사용 하는 경우 SSL 유효성 검사를 사용 하지 않도록 설정 합니다.
* 저장된 프로시저가 실행되는 동안 스크립트 로깅을 사용할 수 있도록 지원이 추가되었습니다.

### <a name="1.10.0"/>1.10.0</a>
* 파티션 간 병렬 쿼리에 대한 지원이 추가되었습니다.
* 분할된 컬렉션의 TOP/ORDER BY 쿼리에 대한 지원이 추가되었습니다.

### <a name="1.9.0"/>1.9.0</a>
* 제한된 요청에 대한 재시도 정책 지원이 추가되었습니다. (제한된 요청은 오류 코드 429, 요청 속도가 너무 크다는 예외를 수신합니다.) 기본적으로 Azure Cosmos DB 다시 시도 9 번 각 요청에 대 한 오류 코드 429 오류가 발생 하면 hello retryAfter 시간 hello 응답 헤더에 적용 합니다. 고정 된 다시 시도 간격 시간 수 이제 hello RetryOptions 속성의 일부로 개체에 설정 될 hello ConnectionPolicy hello 다시 시도 대기 중 서버에서 반환 된 tooignore hello retryAfter 시간이 필요한 경우. 이제 azure Cosmos DB 최대 (관계 없이 다시 시도 횟수)가 제한 및 오류 코드: 429 hello 응답을 반환 하는 각 요청에 대 한 30 초까지 기다립니다. 이 시간 hello RetryOptions ConnectionPolicy 개체 속성에서에서 재정의할 수도 있습니다.
* Cosmos DB 이제 x-ms-스로틀-다시 시도-횟수 및 반환 x-ms-throttle-retry-wait-time-ms hello 응답 헤더의 모든 요청 toodenote hello 스로틀 수 및 hello 누적 hello 요청 대기 시간 hello 재시도 간격을 다시 시도 하십시오.
* hello RetryOptions 속성 노출 hello RetryOptions 클래스 추가 된 hello ConnectionPolicy 클래스 toooverride 사용된 될 수 있는 일부 hello 기본 다시 시도 옵션입니다.

### <a name="1.8.0"/>1.8.0</a>
* 다중 영역 데이터베이스 계정에 대 한 추가 된 hello 지원 합니다.

### <a name="1.7.0"/>1.7.0</a>
* 추가 된 hello 문서에 대 한 시간 tooLive(TTL) 기능에 대 한 지원.

### <a name="1.6.0"/>1.6.0</a>
* [분할된 컬렉션](partition-data.md) 및 [사용자 정의 성능 수준](performance-levels.md)이 구현되었습니다.

### <a name="1.5.6"/>1.5.6</a>
* RangePartitionResolver.resolveForRead 버그 여기서 결과의 잘못 된 concat tooa 인해 링크를 반환 하지 했습니다.

### <a name="1.5.5"/>1.5.5</a>
* hashParitionResolver resolveForRead() 해결: 예외를 throw하는 제공된 파티션 키가 없는 경우 모든 등록된 링크의 목록을 대신 반환합니다.

### <a name="1.5.4"/>1.5.4</a>
* 문제를 해결 [#100](https://github.com/Azure/azure-documentdb-node/issues/100) -HTTPS 에이전트 전용: hello Azure Cosmos DB 목적에 대 한 전역 에이전트 수정 되지 않도록 합니다. 모든 hello lib 요청에 대 한 전용된 에이전트를 사용 합니다.

### <a name="1.5.3"/>1.5.3</a>
* 문제 해결 [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - 미디어 ID에서 대시를 올바르게 처리합니다.

### <a name="1.5.2"/>1.5.2</a>
* 문제 해결 [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter 수신기 누수 경고

### <a name="1.5.1"/>1.5.1</a>
* 문제를 해결 [#92](https://github.com/Azure/azure-documentdb-node/issues/90) -대/소문자 구분 시스템에 대 한 해시 toohash 폴더 이름을 바꿉니다.

### <a name="1.5.0"/>1.5.0</a>
* 해시 및 범위 파티션 해결 프로그램을 추가하여 분할 지원 구현

### <a name="1.4.0"/>1.4.0</a>
* Upsert를 구현합니다. DocumentClient의 새로운 upsertXXX 메서드입니다.

### <a name="1.3.0"/>1.3.0</a>
* 다른 Sdk에 맞게 정렬에서 toobring 버전 번호를 건너뜁니다.

### <a name="1.2.2"/>1.2.2</a>
* 분할 Q 래퍼 toonew 리포지토리를 약속 합니다.
* Npm 레지스트리에 대 한 toopackage 파일을 업데이트 합니다.

### <a name="1.2.1"/>1.2.1</a>
* ID 기반 라우팅을 구현합니다.
* 문제 [#49](https://github.com/Azure/azure-documentdb-node/issues/49) 수정 - 현재 속성이 메서드 current()와 충돌합니다.

### <a name="1.2.0"/>1.2.0</a>
* 지리 공간 인덱스에 대한 지원이 추가되었습니다.
* 모든 리소스에 대한 ID 속성의 유효성을 검사합니다. 리소스의 ID는 ?, /, #, &#47;&#47; 문자를 포함할 수 없으며 공백으로 끝날 수도 없습니다.
* 새 헤더 "인덱스 변환 진행 중" tooResourceResponse를 추가합니다.

### <a name="1.1.0"/>1.1.0</a>
* V2 인덱싱 정책을 구현합니다.

### <a name="1.0.3"/>1.0.3</a>
* 문제 [#40](https://github.com/Azure/azure-documentdb-node/issues/40) -eslint 구현 및 grunt hello 코어에서 구성 하 고 SDK를 약속 합니다.

### <a name="1.0.2"/>1.0.2</a>
* 문제 [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - 프라미스 래퍼에 오류가 있는 헤더가 포함되지 않습니다.

### <a name="1.0.1"/>1.0.1</a>
* ReadConflicts, readConflictAsync, 및 queryConflicts 추가 하 여 충돌에 대 한 기능 tooquery를 구현 합니다.
* API 설명서가 업데이트되었습니다.
* 문제 [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync 오류

### <a name="1.0.0"/>1.0.0</a>
* GA SDK.

## <a name="release--retirement-dates"></a>릴리스 및 사용 중지 날짜
Microsoft는 알림 최소 **12 개월** 순서 toosmooth hello 전환 tooa 지원/최신 버전의 SDK를 사용 중지 전에 합니다.

새로운 기능 및 기능 및 최적화는 toohello 현재만 추가 SDK, 따라서 것이 좋습니다 하면 항상 업그레이드 toohello 최신 SDK 버전 가능한 한 빨리 합니다.

TooCosmos 사용 중지 된 SDK를 사용 하 여 DB에는 모든 요청은 hello 서비스에서 거부 됩니다.

<br/>

| 버전 | 릴리스 날짜 | 사용 중지 날짜 |
| --- | --- | --- |
| [1.12.2](#1.12.2) |2017년 8월 10일 |--- |
| [1.12.1](#1.12.1) |2017년 8월 10일 |--- |
| [1.12.0](#1.12.0) |2017년 5월 10일 |--- |
| [1.11.0](#1.11.0) |2017년 3월 16일 |--- |
| [1.10.2](#1.10.2) |2017년 1월 27일 |--- |
| [1.10.1](#1.10.1) |2016년 12월 22일 |--- |
| [1.10.0](#1.10.0) |2016년 10월 3일 |--- |
| [1.9.0](#1.9.0) |2016년 7월 7일 |--- |
| [1.8.0](#1.8.0) |2016년 6월 14일 |--- |
| [1.7.0](#1.7.0) |2016년 4월 26일 |--- |
| [1.6.0](#1.6.0) |2016년 3월 29일 |--- |
| [1.5.6](#1.5.6) |2016년 3월 8일 |--- |
| [1.5.5](#1.5.5) |2016년 2월 2일 |--- |
| [1.5.4](#1.5.4) |2016년 2월 1일 |--- |
| [1.5.2](#1.5.2) |2016년 1월 26일 |--- |
| [1.5.2](#1.5.2) |2016년 1월 22일 |--- |
| [1.5.1](#1.5.1) |2016년 1월 4일 |--- |
| [1.5.0](#1.5.0) |2015년 12월 31일 |--- |
| [1.4.0](#1.4.0) |2015년 10월 6일 |--- |
| [1.3.0](#1.3.0) |2015년 10월 6일 |--- |
| [1.2.2](#1.2.2) |2015년 9월 10일 |--- |
| [1.2.1](#1.2.1) |2015년 8월 15일 |--- |
| [1.2.0](#1.2.0) |2015년 8월 5일 |--- |
| [1.1.0](#1.1.0) |2015년 7월 9일 |--- |
| [1.0.3](#1.0.3) |2015년 6월 4일 |--- |
| [1.0.2](#1.0.2) |2015년 5월 23일 |--- |
| [1.0.1](#1.0.1) |2015년 5월 15일 |--- |
| [1.0.0](#1.0.0) |2015년 4월 8일 |--- |

## <a name="faq"></a>FAQ
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>참고 항목
Cosmos DB에 대해 자세히 toolearn 참조 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 서비스 페이지.

