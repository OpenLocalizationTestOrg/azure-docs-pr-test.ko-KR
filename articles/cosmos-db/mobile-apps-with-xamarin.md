---
title: "Xamarin과 Azure Cosmos DB aaaBuild 모바일 응용 프로그램 | Microsoft Docs"
description: "Azure Cosmos DB를 사용하여 Xamarin iOS, Android 또는 Forms 응용 프로그램을 만드는 방법에 대한 자습서입니다. Azure Cosmos DB는 속도가 빠른 세계적 규모의 모바일 앱용 클라우드 데이터베이스입니다."
services: cosmos-db
documentationcenter: .net
author: arramac
manager: monicar
editor: 
ms.assetid: ff97881a-b41a-499d-b7ab-4f394df0e153
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: arramac
ms.openlocfilehash: 362a0e239a61e1309e1cf720c23151760952cf69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-mobile-applications-with-xamarin-and-azure-cosmos-db"></a>Xamarin 및 Azure Cosmos DB를 사용하여 모바일 응용 프로그램 빌드
대부분의 모바일 앱 hello 클라우드에서 toostore 데이터가 필요 하 고 Azure Cosmos DB는 모바일 앱에 대 한 클라우드 데이터베이스. 이 기능에는 모바일 개발자에게 필요한 모든 항목이 있습니다. 필요에 따라 규모를 조정할 수 있는 Database as a Service입니다. Hello 전 세계 사용자에 게 있는 경우 항상 투명 하 게 데이터 tooyour 응용 프로그램을 가져올 수 있습니다 것입니다. Hello를 사용 하 여 [Azure Cosmos DB.NET Core SDK](documentdb-sdk-dotnet-core.md), 중간 계층 없이 Azure Cosmos DB를 사용 하 여 직접 모바일 앱 toointeract Xamarin을 사용 하도록 설정할 수 있습니다.

이 문서에서는 Xamarin 및 Azure Cosmos DB를 사용하여 모바일 앱을 빌드하는 자습서를 제공합니다. hello 자습서에 대 한 hello 전체 소스 코드를 찾을 수 있습니다 [Xamarin 및 GitHub의 Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin), 방법을 비롯 하 여 toomanage 사용자 및 사용 권한.

## <a name="azure-cosmos-db-capabilities-for-mobile-apps"></a>모바일 앱용 Azure Cosmos DB 기능
Cosmos DB azure 모바일 앱 개발자를 위한 주요 기능을 수행 하는 hello를 제공 합니다.

![모바일 앱용 Azure Cosmos DB 기능](media/mobile-apps-with-xamarin/documentdb-for-mobile.png)

* 스키마 없는 데이터에 대한 풍부한 쿼리 Azure Cosmos DB는 데이터를 유형이 다른 컬렉션에 스키마 없는 JSON 문서로 저장합니다. 제공 [풍부 하 고 빠른 쿼리](documentdb-sql-query.md) hello tooworry 스키마 또는 인덱스에 대 한 필요 합니다.
* 빠른 처리량. 몇 밀리초 동안만 Azure Cosmos DB를 사용 하 여 tooread 및 쓰기 문서가 필요합니다. 개발자가 필요한 hello 처리량을 지정할 수 및 Azure Cosmos DB 99.99 %sla가 적용 된 인식 합니다.
* 규모가 무제한입니다. Azure Cosmos DB 컬렉션은 [앱이 증가함에 따라 증가합니다](partition-data.md). 처음에는 소규모 데이터와 초당 요청 처리량 수백 개로 시작할 수 있습니다. 사용자 컬렉션에는 수백만 개의 초당 요청 수가 수백 개인 데이터와 임의의 큰 처리량 toopetabytes를 증가할 수 있습니다.
* 전역적으로 분산됩니다. Hello는 사용자가 모바일 앱 hello 전 세계 자주 이동 합니다. Azure Cosmos DB는 [전역적으로 분산되는 데이터베이스](distribute-data-globally.md)입니다. 사용자가 데이터 액세스할 수 있는 tooyour hello 맵 toomake를 클릭 합니다.
* 풍부한 권한이 기본 제공됩니다. Azure Cosmos DB를 사용하면 복잡한 사용자 지정 권한 부여 코드 없이 [사용자별 데이터](https://aka.ms/documentdb-xamarin-todouser)와 같은 인기 있는 패턴 또는 다중 사용자 공유 데이터를 쉽게 구현할 수 있습니다.
* 지리 공간적 쿼리. 현재 대부분의 모바일 앱은 지역 상황별 환경을 제공합니다. 첫 번째 클래스를 지 원하는 [지리 공간 형식](geospatial.md), 이러한 환경을 쉽게 tooaccomplish 만드는 Azure Cosmos DB 만듭니다.
* 이진 첨부 파일입니다. 앱 데이터는 종종 이진 Blob을 포함합니다. 첨부 파일에 대 한 기본 지원을 통해 응용 프로그램 데이터에 대 한 원스톱 상점으로 보다 쉽게 toouse Azure Cosmos DB 있습니다.

## <a name="azure-cosmos-db-and-xamarin-tutorial"></a>Azure Cosmos DB 및 Xamarin 자습서
자습서에서는 방법을 따르는 hello toobuild Xamarin과 Azure Cosmos DB를 사용 하 여 모바일 응용 프로그램입니다. hello 자습서에 대 한 hello 전체 소스 코드를 찾을 수 있습니다 [Xamarin 및 GitHub의 Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin)합니다.

### <a name="get-started"></a>시작
되기 쉬운 tooget Azure Cosmos DB 시작. Azure 포털 toohello 이동한 새 Azure Cosmos DB 계정을 만듭니다. Hello 클릭 **퀵 스타트** 탭 합니다. 다운로드 hello Xamarin Forms 할 일 목록 예제 이미 있는 tooyour Cosmos DB Azure 계정을 연결 합니다. 

![모바일 앱의 Azure Cosmos DB 빠른 시작](media/mobile-apps-with-xamarin/cosmos-db-quickstart.png)

기존 Xamarin 앱이 있는 경우에 hello을 추가할 수 있습니다 또는 [Azure Cosmos DB NuGet 패키지](documentdb-sdk-dotnet-core.md)합니다. Azure Cosmos DB는 Xamarin.IOS, Xamarin.Android 및 Xamarin Forms 공유 라이브러리를 지원합니다.

### <a name="work-with-data"></a>데이터 작업
데이터 레코드는 유형이 다른 컬렉션에서 스키마 없는 JSON 문서로 Azure Cosmos DB에 저장됩니다. Hello에 서로 다른 구조를 사용 하 여 문서를 저장할 수 있습니다 동일한 컬렉션:

```cs
    var result = await client.CreateDocumentAsync(collectionLink, todoItem);
```

Xamarin 프로젝트에서 스키마 없는 데이터에 언어가 통합된 쿼리를 사용할 수 있습니다.

```cs
    var query = await client.CreateDocumentQuery<ToDoItem>(collectionLink)
                    .Where(todoItem => todoItem.Complete == false)
                    .AsDocumentQuery();

    Items = new List<TodoItem>();
    while (query.HasMoreResults) {
        Items.AddRange(await query.ExecuteNextAsync<TodoItem>());
    }
```
### <a name="add-users"></a>사용자 추가
시작된 샘플을 받으려면 많은 처럼 hello Azure Cosmos DB 샘플을 다운로드 한 hello 응용 프로그램의 코드에서 마스터 키 하드 코드를 사용 하 여 toohello 서비스를 인증 합니다. 이 기본값은 하지 로컬 에뮬레이터에서 아무 곳 이나 제외한 toorun 하려는 응용 프로그램에 대 한는 것이 좋습니다. 경우 hello 마스터 키를 가져올 권한이 없는 사용자를 Azure Cosmos DB 계정에서 모든 hello 데이터 손상 될 수 있습니다. 대신, 응용 프로그램 tooaccess hello 로그인 한 사용자에 대 한 레코드를 hello만 하는 것이 좋습니다. Azure Cosmos DB를 사용 하면 개발자가 toogrant 응용 프로그램 읽기 또는 읽기/쓰기 권한 tooa 컬렉션, 파티션 키로 그룹화 된 문서 또는 특정 문서 집합입니다. 

이러한 단계 toomodify hello 할 일 목록 응용 프로그램 tooa 다중 사용자 할 일 목록 응용 프로그램을 수행 합니다. 

  1. Facebook, Active Directory 또는 다른 공급자를 사용 하 여 로그인 tooyour 응용 프로그램을 추가 합니다.

  2. 사용 하 여 Azure Cosmos DB UserItems 컬렉션 만들기 **/userId** hello 파티션 키로 합니다. 지정 하면 컬렉션에 대 한 파티션 키 hello 하면 Azure Cosmos DB tooscale 무한히 응용 프로그램 사용자의 hello 수치로, 증가 속도 toooffer 빠른 쿼리를 계속 합니다.

  3. Azure Cosmos DB 리소스 토큰 브로커를 추가합니다. 이 간단한 웹 API 사용자를 인증 않으며 수명이 짧은 토큰 toosigned 기능 사용자에 게 액세스 권한이 있는 해당 파티션 내에서 toohello 문서만 합니다. 이 예에서 리소스 토큰 broker는 App Service에 호스팅됩니다.

  4. Hello 앱 tooauthenticate tooResource를 Facebook에 토큰 브로커를 수정 하 고 Facebook 사용자 로그인 hello에 대 한 hello 리소스 토큰을 요청 합니다. Hello UserItems 컬렉션에서에서 데이터를 액세스할 수 있습니다.  

[GitHub의 리소스 토큰 broker](http://aka.ms/documentdb-xamarin-todouser)에서 이 패턴의 전체 코드 샘플을 찾을 수 있습니다. 이 다이어그램에서는 hello 솔루션을 보여 줍니다.

![Azure Cosmos DB 사용자 및 사용 권한 브로커](media/mobile-apps-with-xamarin/documentdb-resource-token-broker.png)

두 개의 사용자 toohave 액세스 toohello 하려는 경우 동일한 할 일 목록에 리소스 토큰 브로커의 추가 사용 권한을 toohello 액세스 토큰을 추가할 수 있습니다.

### <a name="scale-on-demand"></a>주문형 확장
Azure Cosmos DB는 관리되는 Database as a Service입니다. 사용자 수가 늘어나면 tooworry Vm을 프로 비전 또는 코어 증가 하는 방법에 대 한 필요는 없습니다. 앱에서 필요한 작업의 수 / 초 (처리량) tootell Azure Cosmos DB 하면 됩니다. Hello 통해 hello 처리량을 지정할 수 있습니다 **배율** 초당 요청 단위 (RUs)를 호출 하는 처리량 측정 한 값을 사용 하 여 탭 합니다. 예를 들어 1KB 문서의 읽기 작업에는 1RU가 필요합니다. 경고 toohello를 추가할 수도 있습니다 **처리량** 메트릭 toomonitor hello 트래픽 증가 하 고 경고를 실행 하는 대로 hello 처리량을 프로그래밍 방식으로 변경 합니다.

![주문형 Azure Cosmos DB 크기 조정 처리량](media/mobile-apps-with-xamarin/cosmos-db-xamarin-scale.png)

### <a name="go-planet-scale"></a>세계적 규모로 확장
앱 향상 인기도 프로그램으로 hello 전세계 사용자가 얻을 수 있습니다. 또는 toobe 예기치 못한 이벤트에 대 한 준비를 할 수도 있습니다. Azure 포털 toohello 이동한 다음 Azure Cosmos DB 계정을 열고 합니다. Hello world hello 맵 toomake 영역의 사용자 데이터 지속적으로 복제 tooany 번호를 클릭 합니다. 이 기능을 사용하면 사용자가 어디서나 데이터 사용할 수 있습니다. 장애 조치 정책을 toobe 만일의 대비책이 대 한 준비를 추가할 수 있습니다.

![지리적 지역에 Azure Cosmos DB 크기 조정](media/mobile-apps-with-xamarin/cosmos-db-xamarin-replicate.png)

축하합니다. Hello 솔루션 완료 했으며 Xamarin과 Azure Cosmos DB으로 모바일 앱 Azure Cosmos DB REST Api를 사용 하 여 hello Azure Cosmos DB JavaScript SDK 및 네이티브 iOS/Android 앱을 사용 하 여 비슷한 단계 toobuild Cordova 앱을 따릅니다.

## <a name="next-steps"></a>다음 단계
* Hello 소스 코드를 보려면 [Xamarin 및 GitHub의 Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin)합니다.
* Hello 다운로드 [Azure Cosmos DB.NET Core SDK](documentdb-sdk-dotnet-core.md)합니다.
* [.NET 응용 프로그램](documentdb-dotnet-samples.md)에 대한 추가 코드 샘플을 찾습니다.
* [Azure Cosmos DB의 다양한 쿼리 기능](documentdb-sql-query.md)에 대해 알아봅니다.
* [Azure Cosmos DB의 지리 공간적 지원](geospatial.md)에 대해 알아봅니다.



