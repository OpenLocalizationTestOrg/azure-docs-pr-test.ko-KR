---
title: "aaaAzure Cosmos DB.NET Core API SDK 및 리소스 | Microsoft Docs"
description: ".NET Core API 및 SDK 릴리스 날짜, 사용 중지 날짜 및 hello Azure Cosmos DB.NET Core SDK의 각 버전 간의 변경 내용을 포함 하 여 hello에 대 한 모든에 대해 알아봅니다."
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: f899b314-26ac-4ddb-86b2-bfdf05c2abf2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1269cafe0ea1caaa871404d507b12632dbb3ed82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-net-core-sdk-release-notes-and-resources"></a>Azure Cosmos DB .NET Core SDK: 릴리스 정보 및 리소스
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

<tr><td>**SDK 다운로드**</td><td>[NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td>**API 설명서**</td><td>[.NET API 참조 설명서](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td>**샘플**</td><td>[.NET 코드 샘플](documentdb-dotnet-samples.md)</td></tr>

<tr><td>**시작**</td><td>[Hello Azure Cosmos DB.NET Core SDK 시작](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td>**웹앱 자습서**</td><td>[Azure Cosmos DB를 사용한 웹 응용 프로그램 개발](documentdb-dotnet-application.md)</td></tr>

<tr><td>**현재 지원되는 프레임워크**</td><td>[.NET Standard 1.6 및 .NET Standard 1.5](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a>릴리스 정보

hello Azure Cosmos DB.NET Core SDK에 기능 패리티를 최신 버전의 hello hello [Cosmos DB AZURE.NET SDK](documentdb-sdk-dotnet.md)합니다.

> [!NOTE] 
> hello Azure Cosmos DB.NET Core SDK 유니버설 Windows 플랫폼 (UWP) 앱과 호환 되지 않습니다. UWP 앱에서는.NET Core SDK hello에 관심이 있는 경우 전자 메일 보내기 너무[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com)합니다.

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0 

* 쿼리 결과 tooa 특정 파티션 키 범위 값의 범위를 지정 하는 것에 대 한 FeedOption으로 PartitionKeyRangeId에 대 한 지원이 추가 되었습니다. 
* 해당 시간 이후에 hello 변경 내용 검색 ChangeFeedOption toostart로 StartTime에 대 한 지원이 추가 되었습니다. 

### <a name="a-name141141"></a><a name="1.4.1"/>1.4.1

*   Hello 스택 오버플로 예외를 일으킬 수 있는 JsonSerializable 클래스에에서는 문제가 해결 되었습니다.

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0

*   [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) 인스턴스를 인스턴스화하는 동안 사용자 지정 JsonSerializerSettings를 지정하기 위한 지원을 추가하였습니다.

### <a name="a-name132132"></a><a name="1.3.2"/>1.3.2

*   Hello 대상 프레임 워크 중 하나로.NET 표준 1.5를 지원 합니다.

### <a name="a-name131131"></a><a name="1.3.1"/>1.3.1

*   SSE4 명령을 지원하지 않고 Azure Cosmos DB 쿼리를 실행할 때 SEHException을 throw하는 X64 컴퓨터에 영향을 준 문제가 해결되었습니다.

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0

*   ConsistentPrefix라는 새로운 일관성 수준에 대한 지원이 추가되었습니다.
*   개별 파티션의 쿼리 메트릭에 대한 지원이 추가되었습니다.
*   쿼리에 대 한 hello 연속 토큰의 hello 크기 제한에 대 한 지원이 추가 되었습니다.
*   실패한 요청의 자세한 추적에 대한 지원이 추가되었습니다.
*   Hello SDK 일부 성능 향상이 되었습니다.

### <a name="a-name122122"></a><a name="1.2.2"/>1.2.2

* 집계 쿼리에 대 한 FeedOptions에 제공 된 hello PartitionKey 값을 무시 하는 문제가 해결 되었습니다.
* 플라이트 중간의 파티션 간 Order By 쿼리를 실행하는 동안 파티션 관리의 투명한 처리 문제를 해결했습니다.

### <a name="a-name121121"></a><a name="1.2.1"/>1.2.1

* Hello 비동기 ASP.NET 컨텍스트 내에서 사용 하는 경우 Api의 일부에서 교착 상태를 일으킨 문제가 해결 되었습니다.

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0

* SDK toomake 더 해결 특정 조건에서 탄력적인 tooautomatic 장애 조치 합니다.

### <a name="a-name112112"></a><a name="1.1.2"/>1.1.2

* 경우에 따라 WebException을 야기 하는 문제에 대 한 수정: hello 원격 이름을 확인할 수 없습니다.
* 추가 된 hello 직접 새 오버 로드 tooReadDocumentAsync API를 추가 하 여 형식화 된 문서를 읽기 위한 지원 합니다.

### <a name="a-name111111"></a><a name="1.1.1"/>1.1.1

* 집계 쿼리(COUNT, MIN, MAX, SUM 및 AVG)에 대한 LINQ 지원이 추가되었습니다.
* 용 hello 이벤트 처리기를 사용 하 여 발생 하는 hello ConnectionPolicy 개체에 대 한 메모리 누수 문제를 수정 합니다.
* ETag를 사용할 때 UpsertAttachmentAsync가 작동하지 않는 문제를 해결합니다.
* 문자열 필드를 정렬할 때 파티션 간 order-by 쿼리 연속 작업이 작동하지 않는 문제를 해결합니다.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0

* 집계 쿼리(COUNT, MIN, MAX, SUM 및 AVG)에 대한 지원이 추가되었습니다. [집계 지원](documentdb-sql-query.md#Aggregates)을 참조하세요.
* 10,100 000RU/s too2500 000RU/s에서 분할 된 컬렉션에 대해 최소 처리량을 적어집니다.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0

hello Azure Cosmos DB.NET Core SDK를 사용 하면 toobuild 빠름, 플랫폼 간 [ASP.NET Core](https://www.asp.net/core) 및 [.NET Core](https://www.microsoft.com/net/core#windows) Windows, Mac 및 Linux에서 앱 toorun 합니다. hello hello Azure Cosmos DB.NET Core SDK의 최신 릴리스는 완벽 하 게 [Xamarin](https://www.xamarin.com) 호환 iOS, Android 및 모노 (Linux)을 대상으로 하는 응용 프로그램에서 사용 되는 toobuild 이어야 하 고 있습니다.  

### <a name="a-name010-preview010-preview"></a><a name="0.1.0-preview"/>0.1.0-preview

hello Azure Cosmos DB.NET Core 미리 보기 SDK를 사용 하면 toobuild 빠름, 플랫폼 간 [ASP.NET Core](https://www.asp.net/core) 및 [.NET Core](https://www.microsoft.com/net/core#windows) Windows, Mac 및 Linux에서 앱 toorun 합니다.

hello Azure Cosmos DB.NET Core 미리 보기 SDK에 기능 패리티를 최신 버전의 hello hello [Cosmos DB AZURE.NET SDK](documentdb-sdk-dotnet.md) hello 다음과 같은 지원 및:
* 모든 [연결 모드](performance-tips.md#networking): 게이트웨이 모드, Direct TCP 및 Direct HTTP 
* 모든 [일관성 수준](consistency-levels.md): 강함, 세션, 제한된 부실, 최종
* [분할된 컬렉션](partition-data.md) 
* [다중 하위 지역 데이터베이스 계정 및 지역에서 복제](distribute-data-globally.md)

질문 관련된 toothis SDK를 사용 하도록 설정한 경우 너무 게시[StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), hello에 문제를 제출 또는 [github 리포지토리](https://github.com/Azure/azure-documentdb-dotnet/issues)합니다. 

## <a name="release--retirement-dates"></a>릴리스 및 사용 중지 날짜

| 버전 | 릴리스 날짜 | 사용 중지 날짜 |
| --- | --- | --- |
| [1.5.0](#1.5.0) |2017년 8월 10일 |--- | 
| [1.4.1](#1.4.1) |2017년 8월 7일 |--- |
| [1.4.0](#1.4.0) |2017년 8월 2일 |--- |
| [1.3.2](#1.3.2) |2017년 6월 12일 |--- |
| [1.3.1](#1.3.1) |2017년 5월 23일 |--- |
| [1.3.0](#1.3.0) |2017년 5월 10일 |--- |
| [1.2.2](#1.2.2) |2017년 4월 19일 |--- |
| [1.2.1](#1.2.1) |2017년 3월 29일 |--- |
| [1.2.0](#1.2.0) |2017년 3월 25일 |--- |
| [1.1.2](#1.1.2) |2017년 3월 20일 |--- |
| [1.1.1](#1.1.1) |2017년 3월 14일 |--- |
| [1.1.0](#1.1.0) |2017년 2월 16일 |--- |
| [1.0.0](#1.0.0) |2016년 12월 21일 |--- |
| [0.1.0-preview](#0.1.0-preview) |2016년 11월 15일 |2015년 12월 31일 |

## <a name="see-also"></a>참고 항목
Cosmos DB에 대해 자세히 toolearn 참조 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 서비스 페이지. 

