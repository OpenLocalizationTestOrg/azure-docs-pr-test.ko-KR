---
title: "Azure Cosmos DB: hello.net에서 테이블 API로 개발 | Microsoft Docs"
description: "자세한 방법을 toodevelop.NET을 사용 하 여 Azure Cosmos DB 테이블 api"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 4b22cb49-8ea2-483d-bc95-1172cd009498
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: mvc
ms.openlocfilehash: 70c6985a1dffdbcdb07e377f8ad10355bb97712a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-table-api-in-net"></a>Azure Cosmos DB: hello.net에서 테이블 API를 사용 하 여 개발

Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다. 신속 하 게 만들기 및 문서, 키/값 및 hello 글로벌 배포 및 수평 확장이 기능 Cosmos DB Azure의 hello 핵심에에서 활용 중 일부는 그래프 데이터베이스를 쿼리할 수 있습니다.

이 자습서에서는 hello 다음 작업 방법을 배웁니다. 

> [!div class="checklist"] 
> * Azure Cosmos DB 계정 만들기 
> * Hello app.config 파일에서 기능을 사용 하도록 설정 
> * Hello를 사용 하 여 테이블을 만들 [테이블 API](table-introduction.md) (미리 보기)
> * 엔터티 tooa 테이블 추가 
> * 엔터티 일괄 삽입 
> * 단일 엔터티 검색 
> * 자동 보조 인덱스를 사용하여 엔터티 쿼리 
> * 엔터티 바꾸기 
> * 엔터티 삭제 
> * 테이블 삭제
 
## <a name="tables-in-azure-cosmos-db"></a>Azure Cosmos DB의 테이블 

Azure Cosmos DB 제공 hello [테이블 API](table-introduction.md) (미리 보기) 스키마가 지정 되지 않은 디자인에 키-값 저장소를 필요로 하는 응용 프로그램에 대 한 합니다. [Azure 테이블 저장소](../storage/common/storage-introduction.md) Sdk 및 REST Api는 Azure Cosmos DB와 함께 사용 되는 toowork 될 수 있습니다. 처리량이 높은 요구 사항과 Azure Cosmos DB toocreate 테이블을 사용할 수 있습니다. Azure Cosmos DB는 현재 공개 미리 보기에서 처리량 액세스에 최적화된 테이블(비공식적으로 "프리미엄 테이블"이라고 함)을 지원합니다. 

Toouse 높은 저장소 및 처리량 요구 사항이 낮은 테이블에 대 한 Azure 테이블 저장소를 계속할 수 있습니다. Azure Cosmos DB 향후 업데이트에서 저장소 액세스에 최적화 된 테이블에 대 한 지원을 제공 하 고 기존 및 새 Azure 테이블 저장소 계정으로 원활 하 게 수 tooAzure Cosmos DB 업그레이드 됩니다.

현재 Azure 테이블 저장소를 사용 하는 경우 이점을 hello "프리미엄 table" 미리 보기와 함께 다음 hello를 얻을 수 있습니다.

- 멀티 호밍 및 [자동 및 수동 장애 조치](regional-failover.md)와 함께 턴키 방식으로 [전역 배포](distribute-data-globally.md)
- 모든 속성("보조 인덱스")에 대한 스키마 독립적 자동 인덱싱 및 빠른 쿼리 지원 
- 여러 지역 간에 [독립적인 저장소 및 처리량 크기 조정](partition-data.md) 지원
- 에 대 한 지원 [테이블당 전용된 처리량](request-units.md) 수백에서 확장할 수 있는 초당 요청 toomillions
- 에 대 한 지원 [5 튜닝할 수 있는 일관성 수준](consistency-levels.md) 가용성, 대기 시간 및 일관성 오프 tootrade 응용 프로그램 요구 사항에 따라
- 단일 지역 및 기능 tooadd를 자세한 내에서 99.99% 가용성 높은 가용성을 위한 지역 및 [업계를 주도하 포괄적인 Sla](https://azure.microsoft.com/support/legal/sla/cosmos-db/) 일반 가용성에
- Hello 기존 Azure 저장소.NET SDK를 사용 하 고 코드 변경 내용 tooyour 응용 프로그램이 없습니다.

Hello 미리 보기 동안 Azure Cosmos DB 지원 hello.NET SDK를 사용 하 여 테이블 API hello 합니다. Hello를 다운로드할 수 있습니다 [Azure 저장소 미리 보기 SDK](https://aka.ms/premiumtablenuget) 있는 hello NuGet에서 동일한 클래스와 메서드 시그니처에 hello로 [Azure 저장소 SDK](https://www.nuget.org/packages/WindowsAzure.Storage), 또한 hello를 사용 하 여 tooAzure Cosmos DB 계정을 연결할 수 있지만 테이블 API입니다.

toolearn 더 복잡 한 Azure 테이블 저장소 작업에 대 한 참조.

* [Cosmos DB 소개 tooAzure: 테이블 API](table-introduction.md)
* 사용 가능한 Api에 대 한 자세한 내용은 테이블 서비스 참조 설명서 hello [.NET 참조 용 저장소 클라이언트 라이브러리](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)

### <a name="about-this-tutorial"></a>이 자습서 정보
이 자습서 사용 Azure Cosmos DB 개발자에 게 hello SDK, Azure 테이블 저장소에 잘 알고 있으며 toouse hello 프리미엄 기능 사용할 수 있을 것입니다. 에 기반 하는 [.NET을 사용 하 여 Azure 테이블 저장소 시작](table-storage-how-to-use-dotnet.md) 및 추가 기능을 활용 tootake 보조 인덱스, 프로 비전 된 처리량 및 멀티 호 밍 등의 방법을 보여 줍니다. 어떻게 toouse Azure 포털 toocreate Azure Cosmos DB 계정을 hello 다음 빌드 및 배포 테이블 응용 프로그램을 다룹니다. 또한 테이블을 만들고 삭제하며, 테이블 데이터를 삽입, 업데이트, 삭제 및 쿼리하기 위한 .NET 예제를 단계별로 안내합니다. 

설치 된 Visual Studio 2017 없는 경우 다운로드 하 고 hello를 사용 하 여 수 **무료** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)합니다. 사용할 수 있는지 확인 **Azure 개발** hello Visual Studio 설정 중입니다.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>데이터베이스 계정 만들기

Hello Azure 포털에서에서 Azure Cosmos DB 계정을 만들어 보겠습니다.  

> [!TIP]
> * Azure Cosmos DB 계정이 이미 있나요? 이 경우 건너뛰고 너무[Visual Studio 솔루션 설정](#SetupVS)합니다.
> * Azure DocumentDB 계정이 있나요? 따라서 사용자 계정이 Azure Cosmos DB 계정인 이제 하 고 건너뛰어도 너무[Visual Studio 솔루션 설정](#SetupVS)합니다.  
> * Hello Azure Cosmos DB 에뮬레이터를 사용 하는 경우 hello 단계에 따르십시오 [Azure Cosmos DB 에뮬레이터](local-emulator.md) toosetup 에뮬레이터 hello 및 너무 건너 뛸[Visual Studio 솔루션 설정](#SetupVS)합니다.
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting tooany location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-hello-sample-application"></a>Hello 샘플 응용 프로그램 복제

이제 보겠습니다 테이블 앱 github hello 연결 문자열을 설정 하 고 실행을 복제 합니다.

1. 예: git bash git 터미널 윈도우를 열고 및 `cd` tooa 작업 디렉터리입니다.  

2. 다음 명령은 tooclone hello 샘플 리포지토리 hello를 실행 합니다. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. 그런 다음 Visual Studio에서 hello 솔루션 파일을 엽니다.

## <a name="update-your-connection-string"></a>연결 문자열 업데이트

이제 돌아가서 toohello Azure 포털 tooget 연결 문자열 정보를 hello 앱에 복사 합니다.

1. Hello에 [Azure 포털](http://portal.azure.com/), 프로그램 Azure Cosmos DB에에서 account, 왼쪽 탐색 hello 클릭 **키**, 클릭 하 고 **읽기-쓰기 키**합니다. Hello 다음 단계에서 hello app.config 파일에 hello hello 화면 toocopy hello 연결 문자열의 오른쪽에 hello 복사 단추를 사용 합니다.

2. Visual Studio에서 hello app.config 파일을 엽니다. 

3. Hello 포털 (hello 복사 단추 사용)에서 URI 값을 복사 하 고 쉽게 hello app.config에 hello 계정 키의 값입니다. App.config의 계정 이름에 대해 이전에 만든 hello 계정 이름을 사용 합니다.
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> toouse toochange hello 연결 문자열에 필요한 표준 Azure 테이블 저장소로이 응용 프로그램에서는 `app.config file`합니다. 테이블 계정 이름 및 Azure 저장소 기본 키로 키로 사용 하 여 hello 계정 이름입니다. <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-hello-app"></a>빌드 및 hello 앱 배포
1. Visual Studio에서 마우스 오른쪽 단추로 클릭 hello 프로젝트에 대해 **솔루션 탐색기** 클릭 하 고 **NuGet 패키지 관리**합니다. 

2. Hello NuGet에서에서 **찾아보기** 상자에서 입력 ***WindowsAzure.Storage PremiumTable***합니다. **시험판 버전 포함**을 선택합니다.

3. Hello 결과 통해 설치 hello **WindowsAzure.Storage PremiumTable** hello 미리 보기 빌드를 선택 하 고 `0.0.1-preview`합니다. 이 작업 hello Azure 테이블 저장소 패키지 및 모든 종속성을 설치 합니다.

4. CTRL + f 5를 클릭 toorun hello 응용 프로그램입니다. 

있습니다 수 이제 tooData 탐색기 돌아가서 및 쿼리 참조, 수정 및이 테이블 데이터와 함께 작동 합니다. 

> [!NOTE]
> toouse 정당한 하는 Azure Cosmos DB 에뮬레이터와 함께이 응용 프로그램 toochange hello 연결 문자열에 필요한 `app.config file`합니다. 에뮬레이터에 대 한 값 보다 작은 hello를 사용 합니다. <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a>Azure DB Cosmos 기능
Cosmos DB azure의 hello Azure 테이블 저장소 API에서에서 사용할 수 없는 기능을 지원 합니다. hello 새로운 기능 통해 사용할 수 있습니다 hello 다음 `appSettings` 구성 값입니다. 모든 새 서명 또는 오버 로드 toohello 미리 보기 Azure 저장소 SDK 소개 하지 않았습니다. 이렇게 하면 tooconnect tooboth standard 및 premium 테이블, Blob 및 큐와 같은 다른 Azure 저장소 서비스와 작업 있습니다. 


| 키 | 설명 |
| --- | --- |
| TableConnectionMode  | Azure Cosmos DB는 두 가지 연결 모드를 지원합니다. `Gateway` 모드에서는 항상 요청은 해당 데이터 파티션에서 toohello 전달 toohello Azure Cosmos DB 게이트웨이 합니다. `Direct` 연결 모드 hello 클라이언트 hello 매핑 테이블 toopartitions의를 가져오고 이러한 데이터 파티션에 대해 직접 요청 합니다. 권장 `Direct`, 기본 hello 합니다.  |
| TableConnectionProtocol | Azure Cosmos DB는 두 가지 연결 프로토콜, 즉 `Https`과 `Tcp`를 지원합니다. `Tcp`hello 기본 템플릿이 고 용량이 있기 때문에 권장 됩니다. |
| TablePreferredLocations | 읽기에 대해 기본 설정된(멀티 홈) 위치를 쉼표로 구분한 목록입니다. Azure Cosmos DB 계정은 각각 1-30개 이상의 지역과 연결할 수 있습니다. 각 클라이언트 인스턴스에 대기 시간이 짧은 읽기에 대 한 hello 기본 설정 순서에 이러한 영역의 하위 집합을 지정할 수 있습니다. 사용 하 여 hello 영역 이름은 해당 [표시 이름을](https://msdn.microsoft.com/library/azure/gg441293.aspx), 예를 들어 `West US`합니다. [멀티 호밍 API](tutorial-global-distribution-table.md)도 참조하세요.
| TableConsistencyLevel | 잘 정의된 5가지 일관성 수준, 즉 `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix` 및 `Eventual` 중에서 선택하여 대기 시간, 일관성 및 가용성 간에 균형을 유지할 수 있습니다. 기본값은 `Session`입니다. hello 선택한 일관성 수준에는 다중 지역 한 설정에서 성능이 크게 달라를 집니다. 자세한 내용은 [일관성 수준](consistency-levels.md)을 참조하세요. |
| TableThroughput | 초당 요청 단위 (RU)로 표시 하는 hello 테이블에 대 한 예약 된 처리량입니다. 테이블당 100-수백만 RU/s를 지원할 수 있습니다. [요청 단위](request-units.md)를 참조하세요. 기본값은 `400`입니다. |
| TableIndexingPolicy | 테이블 내 모든 열에 대해 일관된 자동 보조 인덱싱입니다. | JSON 인덱싱 정책을 지정 하는 표준에 맞는 toohello는 문자열입니다. 참조 [인덱싱 정책](indexing-policies.md) toosee 인덱싱 정책 tooinclude/제외 특정 열을 변경 하는 방법입니다. | 모든 속성의 자동 인덱싱(문자열에 대한 해시 및 숫자에 대한 범위) |
| TableQueryMaxItemCount | Hello 단일 왕복에서 테이블 쿼리 당 반환 되는 항목의 최대 수를 구성 합니다. 기본값은 `-1`, Azure Cosmos DB hello 값이 런타임에 동적으로 결정할 수 있습니다. |
| TableQueryEnableScan | Hello 쿼리를 사용할 수 없는 hello 인덱스 모든 필터에 대 한 다음 실행 그래도 검색을 통해. 기본값은 `false`입니다.|
| TableQueryMaxDegreeOfParallelism | hello 수준의 크로스 파티션 쿼리 실행에 대 한 병렬 처리 합니다. `0`없는 미리 인출과, 직렬 `1` 미리 인출과 직렬 이며 증가 hello 속도 병렬 처리 수준 값이 높을수록 더 합니다. 기본값은 `-1`, Azure Cosmos DB hello 값이 런타임에 동적으로 결정할 수 있습니다. |

toochange hello 기본 값, 열기 hello `app.config` Visual Studio의 솔루션 탐색기에서 파일입니다. Hello의 hello 내용을 추가 `<appSettings>` 요소 아래에 표시 합니다. 대체 `account-name` hello 저장소 계정의 이름으로 및 `account-key` 와 계정 액세스 키입니다. 

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
      <!-- Client options -->
      <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key; TableEndpoint=https://account-name.documents.azure.com" />
      <add key="TableConnectionMode" value="Direct"/>
      <add key="TableConnectionProtocol" value="Tcp"/>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>
      <add key="TableConsistencyLevel" value="Eventual"/>

      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
      <add key="TableIndexingPolicy" value="{""indexingMode"": ""Consistent""}"/>

      <!-- Table query options -->
      <add key="TableQueryMaxItemCount" value="-1"/>
      <add key="TableQueryEnableScan" value="false"/>
      <add key="TableQueryMaxDegreeOfParallelism" value="-1"/>
      <add key="TableQueryContinuationTokenLimitInKb" value="16"/>
            
    </appSettings>
</configuration>
```

Hello 앱에서 일어나는 빠르게 검토를 만들어 보겠습니다. 열기 hello `Program.cs` 다음 코드이 줄을 만든다고 hello 테이블 리소스 파일을 찾습니다. 

## <a name="create-hello-table-client"></a>Hello 테이블 클라이언트 만들기
초기화는 `CloudTableClient` tooconnect toohello 테이블 계정.

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
이 클라이언트 hello를 사용 하 여 초기화는 `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, 및 `TablePreferredLocations` hello 응용 프로그램 설정에 지정 된 값을 구성 합니다.
    
## <a name="create-a-table"></a>테이블 만들기
그런 다음 `CloudTable`을 사용하여 테이블을 만듭니다. Cosmos db Azure 테이블 저장소와 처리량을 기준으로 독립적으로 확장할 수 있습니다 및 분할 hello 서비스에 의해 자동으로 처리 됩니다. Azure Cosmos DB는 고정된 크기 및 무제한 테이블을 모두 지원합니다. 자세한 내용은 [Azure Cosmos DB에서 분할](partition-data.md)을 참조하세요. 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

테이블을 만드는 방법에는 중요한 차이가 있습니다. Azure Cosmos DB는 트랜잭션에 대한 Azure 저장소의 사용량 기반 모델과 달리 처리량을 예약합니다. hello 예약 모델에 두 가지 주요 이점이 있습니다.

* 처리량은 전용/예약되어 있으므로 요청 속도가 프로비전된 처리량 이하인 경우에는 절대로 제한할 수 없습니다
* hello 예약 모델은 더 많은 [처리량이 많은 작업에 대 한 비용 효율적인](key-value-store-cost.md)

에 대 한 hello 설정을 구성 하 여 hello 기본 처리량을 구성할 수 있습니다 `TableThroughput` 초당 RU (요청 단위)를 기준으로 합니다. 

1KB 엔터티 읽기를 1로 정규화 된 RU, 및 기타 작업은 정규화 된 tooa CPU, 메모리 및 IOPS 소비량에 따라 RU 값을 고정 합니다. [Azure Cosmos DB의 요청 단위](request-units.md)에 대해 자세히 알아보세요.

> [!NOTE]
> 테이블 저장소 SDK 현재 수정 하 고 처리량을 지원 하지 않는데, 즉각적으로 언제 든 hello Azure 포털 또는 Azure CLI를 사용 하 여 hello 처리량을 변경할 수 있습니다.

다음으로 hello 간단한 읽기는 과정을 안내 하 고 hello Azure 테이블 저장소 SDK를 사용 하 여 (CRUD) 작업을 작성 합니다. 이 자습서에서는 Azure Cosmos DB에서 제공하는 예측 가능한 짧은 대기 시간(한 자리 수의 밀리초) 및 빠른 쿼리를 보여 줍니다.

## <a name="add-an-entity-tooa-table"></a>엔터티 tooa 테이블 추가
Azure 테이블 저장소에서 엔터티의 hello에서 확장 `TableEntity` 클래스 및 있어야 `PartitionKey` 및 `RowKey` 속성입니다. 다음은 고객 엔터티에 대한 샘플 정의입니다.

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

다음 코드 조각 hello tooinsert에서 엔터티를 Azure 저장소 SDK를 hello 하는 방법을 보여 줍니다. Azure Cosmos DB hello 전 세계 모든 규모에 짧은 대기 시간을 보장 하도록 설계 되었습니다.

쓰기 완료 < p99 및 실행 중인 응용 프로그램에 대 한 p50에서 ~ 6 ms 15 밀리초 hello Azure Cosmos DB 계정 hello와 동일한 영역입니다. 고이 기간 동안 동기적으로 복제, 지 속력 있게 커밋된 모든 콘텐츠가 인덱싱된 후에 기록 하는 hello 팩트에 대 한 계정을 백 toohello 클라이언트 승인 수는 했습니다.

hello Cosmos db Azure 테이블 API 미리 보기입니다. 일반 공급 시 hello p99 대기 시간이 보장 다른 Azure Cosmos DB Api와 같이 Sla에 의해 지원 됩니다. 

```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a>엔터티 일괄 삽입
삽입에 동일한 단일 일괄 처리 작업 hello와 azure 테이블 저장소에서는 수 있는 일괄 처리 작업을 API를 업데이트, 삭제를 결합 합니다. Azure Cosmos DB에는 몇몇 제한 사항이 적용 hello hello 배치 API에서 Azure 테이블 저장소로 합니다. 여러 쓰기 toohello 수행할 수 있습니다, 예를 들어 일괄 처리 내에서 여러 읽기를 수행할 수 있습니다는 일괄 처리 내에서 동일한 엔터티 및 일괄 처리 당 100 개의 작업에는 제한이 없습니다. 

```csharp
// Create hello batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it toohello table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it toohello table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities toohello batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute hello batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a>단일 엔터티 검색
전체 Azure Cosmos DB에서 가져오거나 검색 < p99와 ~ 1에서 10 밀리초에서 p50에서 ms hello 같은 Azure 지역입니다. 대기 시간이 짧은 읽기에 대 한 개수 만큼 영역 tooyour 계정을 추가 하 고 설정 하 여 ("멀티홈")의 로컬 영역에서 응용 프로그램 tooread를 배포할 수 `TablePreferredLocations`합니다. 

다음 코드 조각 hello를 사용 하 여 단일 엔터티를 검색할 수 있습니다.

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> [여러 지역을 사용하여 개발](tutorial-global-distribution-table.md)에서 멀티 호밍 API에 대해 알아보세요.
>

## <a name="query-entities-using-automatic-secondary-indexes"></a>자동 보조 인덱스를 사용하여 엔터티 쿼리
Hello를 사용 하 여 테이블을 쿼리할 수 `TableQuery` 클래스입니다. Azure Cosmos DB에는 쓰기 액세스에 최적화된 데이터베이스 엔진이 있어 테이블 내의 모든 열을 자동으로 인덱싱합니다. 인덱스를 만드는 Azure Cosmos DB에서 알 수 없는 tooschema 것입니다. 따라서 스키마 행 간에 차이가 있는 경우에 또는 hello 스키마 시간이 지나면서 자동으로 인덱싱. Azure Cosmos DB 자동 보조 인덱스를 지원, 이므로 모든 속성에 대 한 쿼리 hello 인덱스를 사용할 수 하 고 효율적으로 처리할 수입니다.

```csharp
CloudTable table = tableClient.GetTableReference("people");

// Filter against a property that's not partition key or row key
TableQuery<CustomerEntity> emailQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.GenerateFilterCondition("Email", QueryComparisons.Equal, "Ben@contoso.com"));

foreach (CustomerEntity entity in table.ExecuteQuery(emailQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

미리 보기에서 Azure Cosmos DB 지원 hello 같은 hello 테이블 API에 대 한 Azure 테이블 저장소와 기능을 쿼리 합니다. 또한 Azure Cosmos DB는 정렬, 집계, 지리 공간적 쿼리, 계층 구조 및 다양한 기본 제공 함수도 지원합니다. hello 추가 기능이 이후 서비스 업데이트에 hello 테이블 API에서에서 제공 됩니다. 이러한 기능에 대한 개요는 [Azure Cosmos DB 쿼리](documentdb-sql-query.md)를 참조하세요. 

## <a name="replace-an-entity"></a>엔터티 바꾸기
엔터티에 tooupdate hello 테이블 서비스에서 검색, hello 엔터티 개체를 수정 및 다음 hello 변경 내용을 저장할 toohello 테이블 서비스를 다시 합니다. hello 다음 코드 기존 고객의 전화 번호를 변경합니다. 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
마찬가지로 `InsertOrMerge` 또는 `Merge` 작업을 수행할 수 있습니다.  

## <a name="delete-an-entity"></a>엔터티 삭제
Hello를 사용 하 여 검색 한 후에 쉽게 엔터티를 삭제할 수 있습니다 엔터티 업데이트에 대 한 표시 된 같은 패턴입니다. hello 코드 다음 검색 하 고 고객 엔터티를 삭제 합니다.

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a>테이블 삭제
마지막으로, 다음 코드 예제는 hello 저장소 계정에서 테이블을 삭제 합니다. Azure Cosmos DB를 사용하여 테이블을 즉시 삭제하고 다시 만들 수 있습니다.

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a>리소스 정리 

것 toocontinue toouse이이 앱을 하는 경우 단계 toodelete hello Azure 포털에서에서이 자습서에서 만든 모든 리소스를 수행 하는 hello를 사용 합니다.   

1. Hello Azure 포털에서에서 왼쪽 메뉴 hello에서에서 클릭 **리소스 그룹** 만든 hello 리소스의 hello 이름을 클릭 하 고 있습니다.  
2. 리소스 그룹 페이지에서 클릭 **삭제**hello 텍스트 상자에 hello 리소스 toodelete의 hello 이름을 입력 한 다음 클릭 **삭제**합니다. 

## <a name="next-steps"></a>다음 단계

이 자습서에서 다룬 hello 테이블 API가 있는 Azure Cosmos DB를 사용 하 여 tooget을 시작 하는 방법 및 hello 다음 작업을 수행 하면: 

> [!div class="checklist"] 
> * Azure Cosmos DB 계정 만들기 
> * Hello app.config 파일에 제공 된 기능 
> * 테이블 만들기 
> * 엔터티 tooa 테이블 추가 
> * 엔터티 일괄 삽입 
> * 단일 엔터티 검색 
> * 자동 보조 인덱스를 사용하여 엔터티 쿼리 
> * 엔터티 바꾸기 
> * 엔터티 삭제 
> * 테이블 삭제  

이제 toohello 다음 자습서를 진행 하 고 테이블 데이터를 쿼리 하는 방법에 대 한 자세히 알아볼 수 있습니다. 

> [!div class="nextstepaction"]
> [Hello 테이블 API가 있는 쿼리](tutorial-query-table.md)
