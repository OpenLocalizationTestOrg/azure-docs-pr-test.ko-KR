---
title: "Azure Cosmos db aaaDatabase 마이그레이션 도구 | Microsoft Docs"
description: "Toouse hello 소스 Azure Cosmos DB 데이터 마이그레이션 도구 tooimport 데이터 tooAzure Cosmos DB MongoDB, SQL Server, 테이블 저장소, Amazon DynamoDB, CSV 및 JSON 파일을 비롯 한 다양 한 원본의 열 하는 방법에 대해 알아봅니다. CSV tooJSON 변환 합니다."
keywords: "csv toojson, 데이터베이스 마이그레이션 도구, convert csv toojson"
services: cosmos-db
author: andrewhoh
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: d173581d-782a-445c-98d9-5e3c49b00e25
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 997648a31602d854db75bb6ce4e2ecff36fc1069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-data-into-azure-cosmos-db-for-hello-documentdb-api"></a>어떻게 tooimport 데이터에 대 한 Azure Cosmos DB를 DocumentDB API hello?

이 자습서에서 사용 하는 방법은 Azure Cosmos DB hello 제공: JSON 파일을 비롯 한 다양 한 원본의 데이터를 가져올 수 있는 DocumentDB API 데이터 마이그레이션 도구를 CSV 파일, SQL, MongoDB, Amazon DynamoDB 및 Azure Cosmos DB DocumentDB Azure 테이블 저장소 Azure Cosmos DB hello DocumentDB API와 API 컬렉션에 대 한 컬렉션으로 사용합니다. DocumentDB API hello에 대 한 단일 파티션 컬렉션 tooa 다중 파티션 컬렉션에서 마이그레이션할 때 hello 데이터 마이그레이션 도구를 사용할 수도 있습니다.

hello 데이터 마이그레이션 도구에 대 한 Azure Cosmos DB로 데이터를 가져올 hello DocumentDB API를 사용 하는 경우에 작동 합니다. 이 이번에는 hello 테이블 API 또는 Graph API와 함께 사용할 데이터를 가져오는 지원 되지 않습니다. 

hello MongoDB API로 사용 하기 위해 tooimport 데이터 참조 [Azure Cosmos DB: 어떻게 toomigrate 데이터에 대 한 hello MongoDB API?](mongodb-migrate.md)합니다.

이 자습서에서는 hello 다음 작업 방법을 배웁니다.

> [!div class="checklist"]
> * Hello 데이터 마이그레이션 도구 설치
> * 다른 데이터 원본에서 데이터 가져오기
> * Azure Cosmos DB tooJSON에서 내보내기

## <a id="Prerequisites"></a>필수 조건
이 문서의 지침 hello를 수행 하기 전에 hello 다음이 설치 되어 있는지 확인 합니다.

* [Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) 이상

## <a id="Overviewl"></a>Hello 데이터 마이그레이션 도구 개요
hello 데이터 마이그레이션 도구는 다음을 사용 하는 다양 한를 비롯 한 원본에서에서 데이터 tooAzure Cosmos DB 가져오는 오픈 소스 솔루션.

* JSON 파일
* MongoDB
* SQL Server
* CSV 파일
* Azure 테이블 저장소
* Amazon DynamoDB
* HBase
* Azure Cosmos DB 컬렉션

Hello 가져오기 도구 (dtui.exe) 그래픽 사용자 인터페이스를 포함 하는 동안 hello 명령줄 (dt.exe)에서 제어할 수도 있습니다. 실제로 hello UI 통해 가져오기 설정 후 옵션 toooutput hello 관련 명령을 않습니다. 가져오는 동안 계층 관계(하위 문서)를 만들 수 있도록 테이블 형식 원본 데이터(예: SQL Server 또는 CSV 파일)를 변환할 수 있습니다. 대상 옵션 및 보기 결과 가져오기을 각 소스에서 샘플 명령줄 tooimport 원본 옵션에 대 한 자세한 toolearn 읽는 계속 유지 합니다.

## <a id="Install"></a>Hello 데이터 마이그레이션 도구 설치
hello 마이그레이션 도구 소스 코드의 GitHub에서 사용할 수는 [이 리포지토리](https://github.com/azure/azure-documentdb-datamigrationtool) 고 컴파일된 버전에서 사용할 수 있는 [Microsoft 다운로드 센터](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d)합니다. Hello 솔루션 컴파일 중 하나 단순히를 다운로드 하 고 선택한 hello 컴파일된 버전 tooa 디렉터리 압축 될 수 있습니다. 다음 중 하나를 실행합니다.

* **Dtui.exe**: hello 도구의 그래픽 인터페이스 버전
* **Dt.exe**: hello 도구의 명령줄 버전

## <a name="import-data"></a>데이터 가져오기

시간 tooimport는 hello 도구를 설치한 후 데이터입니다. 어떤 종류의 데이터 시겠습니까 tooimport?

* [JSON 파일](#JSON)
* [MongoDB](#MongoDB)
* [MongoDB 내보내기 파일](#MongoDBExport)
* [SQL Server](#SQL)
* [CSV 파일](#CSV)
* [Azure Table Storage](#AzureTableSource)
* [Amazon DynamoDB](#DynamoDBSource)
* [Blob](#BlobImport)
* [Azure Cosmos DB 컬렉션](#DocumentDBSource)
* [HBase](#HBaseSource)
* [Azure Cosmos DB 대량 가져오기](#DocumentDBBulkImport)
* [Azure Cosmos DB 순차 레코드 가져오기](#DocumentDSeqTarget)


## <a id="JSON"></a>tooimport JSON 파일
hello JSON 파일 소스 가져오기 옵션을 사용 하면 tooimport 하나 이상의 단일 문서 JSON 파일 또는 JSON 문서의 배열을 포함 된 JSON 파일이 있습니다. JSON 파일 tooimport를 포함 하는 폴더를 추가할 때의 하위 폴더에 파일을 검색 하는 재귀적 hello 선택할을 수 있습니다.

![JSON 파일 원본 옵션의 스크린샷 - 데이터베이스 마이그레이션 도구](./media/import-data/jsonsource.png)

다음은 몇 가지 명령줄 샘플 tooimport JSON 파일입니다.

    #Import a single JSON file
    dt.exe /s:JsonFile /s.Files:.\Sessions.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory of JSON files
    dt.exe /s:JsonFile /s.Files:C:\TESessions\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory (including sub-directories) of JSON files
    dt.exe /s:JsonFile /s.Files:C:\LastFMMusic\**\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Music /t.CollectionThroughput:2500

    #Import a directory (single), directory (recursive), and individual JSON files
    dt.exe /s:JsonFile /s.Files:C:\Tweets\*.*;C:\LargeDocs\**\*.*;C:\TESessions\Session48172.json;C:\TESessions\Session48173.json;C:\TESessions\Session48174.json;C:\TESessions\Session48175.json;C:\TESessions\Session48177.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:subs /t.CollectionThroughput:2500

    #Import a single JSON file and partition hello data across 4 collections
    dt.exe /s:JsonFile /s.Files:D:\\CompanyData\\Companies.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:comp[1-4] /t.PartitionKey:name /t.CollectionThroughput:2500

## <a id="MongoDB"></a>MongoDB에서 tooimport

> [!IMPORTANT]
> MongoDB에 대 한 지원과 함께 tooan Azure Cosmos DB 계정을 가져오는 경우 다음을 수행 [지침](mongodb-migrate.md)합니다.
> 
> 

hello MongoDB 소스 가져오기 옵션 tooimport 개별 MongoDB 컬렉션에서 사용 하면 및 필요에 따라 쿼리를 사용 하 여 문서를 필터링 및/또는 예측을 사용 하 여 hello 문서 구조를 수정 합니다.  

![MongoDB 원본 옵션의 스크린샷](./media/import-data/mongodbsource.png)

hello 연결 문자열은 hello 표준 MongoDB 형식:

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> Hello 연결 문자열 필드에 지정 된 MongoDB 인스턴스 hello를 사용 하 여 hello Verify 명령 tooensure 액세스할 수 있습니다.
> 
> 

데이터를 가져올 hello 컬렉션의 hello 이름을 입력 합니다. 선택적으로 지정 하거나 쿼리에 대 한 파일을 제공 될 수 있습니다 (예: {pop: {$gt: 5000}}) 및/또는 프로젝션 (예: {loc:0}) tooboth 필터 및 모양 hello 데이터 toobe 가져온 합니다.

다음은 몇 가지 명령줄 샘플 tooimport MongoDB에서입니다.

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match hello query and exclude hello loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <a id="MongoDBExport"></a>tooimport MongoDB 내보내기 파일

> [!IMPORTANT]
> MongoDB에 대 한 지원과 함께 tooan Azure Cosmos DB 계정을 가져오는 경우 다음을 수행 [지침](mongodb-migrate.md)합니다.
> 
> 

hello MongoDB 내보내기 JSON 파일 소스 가져오기 옵션 있습니다 하나 tooimport 또는 hello mongoexport 유틸리티에서 생성 된 JSON 파일.  

![MongoDB 내보내기 원본 옵션의 스크린샷](./media/import-data/mongodbexportsource.png)

가져오기에 대 한 MongoDB 내보내기 JSON 파일을 포함 하는 폴더를 추가할 때의 하위 폴더에 파일을 검색 하는 재귀적 hello 선택할을 수 있습니다.

다음 MongoDB 내보내기에서 명령줄 샘플 tooimport JSON 파일은:

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <a id="SQL"></a>SQL Server에서 tooimport
hello SQL 소스 가져오기 옵션 개별 SQL Server 데이터베이스에서 tooimport 있으며 필요에 따라 쿼리를 사용 하 여 가져올 hello 레코드 toobe를 필터링 합니다. 또한 중첩 (에 자세히 설명 잠시 후에) 구분 기호를 지정 하 여 hello 문서 구조를 수정할 수 있습니다.  

![SQL 원본 옵션의 스크린샷 - 데이터베이스 마이그레이션 도구](./media/import-data/sqlexportsource.png)

hello 연결 문자열의 형식이 hello hello 표준 SQL 연결 문자열 형식이입니다.

> [!NOTE]
> Hello hello 연결 문자열 필드에 지정 된 SQL Server 인스턴스를 사용 하 여 hello Verify 명령 tooensure 액세스할 수 있습니다.
> 
> 

hello 중첩 구분 기호 속성을 가져오는 동안 사용 되는 toocreate 계층 관계 (하위 문서)입니다. Hello 다음 SQL 쿼리를 고려 합니다.

*CAST(BusinessEntityID AS varchar)를 ID, Name으로, AddressType을 [Address.AddressType]으로, AddressLine1을 [Address.AddressLine1]로, City를 [Address.Location.City]로, StateProvinceName을 [Address.Location.StateProvinceName]으로, PostalCode를 [Address.PostalCode]로, CountryRegionName을 AddressType='Main Office'인 Sales.vStoreWithAddresses에서 [Address.CountryRegionName]으로 선택합니다.*

반환 (부분) 결과 다음 hello 됩니다.

![SQL 쿼리 결과의 스크린샷](./media/import-data/sqlqueryresults.png)

Note Address.AddressType 등 Address.Location.StateProvinceName hello 별칭입니다. 중첩 구분 기호를 지정 하 여 '.', hello 가져오기 도구는 주소를 만들고 hello 중 Address.Location 하위 문서 가져오기. Azure Cosmos DB의 결과 문서 예는 다음과 같습니다.

*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*

SQL Server에서 몇 가지 명령줄 샘플 tooimport 다음과 같습니다.

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <a id="CSV"></a>tooimport CSV 파일 및 CSV tooJSON 변환
CSV 파일 소스 가져오기 옵션 hello tooimport 있습니다 하나 이상의 CSV 파일을 수 있습니다. 가져올 CSV 파일을 포함 하는 폴더를 추가할 때의 하위 폴더에 파일을 검색 하는 재귀적 hello 선택할을 수 있습니다.

![CSV tooJSON-CSV 스크린샷 소스 옵션](media/import-data/csvsource.png)

유사한 toohello SQL 원본, 구분 기호 속성을 중첩 하는 hello 가져오기 중 사용 되는 toocreate 계층 관계 (하위 문서)을 수 있습니다. Hello CSV 머리글 행과 데이터 행을 고려해 야 합니다.

![CSV 스크린샷 샘플 레코드-CSV tooJSON](./media/import-data/csvsample.png)

Note DomainInfo.Domain_Name 등 RedirectInfo.Redirecting hello 별칭입니다. 중첩 구분 기호를 지정 하 여 '.', hello 가져오기 도구는 DomainInfo 만들고 hello 중 RedirectInfo 하위 문서 가져옵니다. Azure Cosmos DB의 결과 문서 예는 다음과 같습니다.

*{"DomainInfo": {"Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www. ACUS.GOV"}," Federal 에이전시 ":"미국 hello의 관리 회의","RedirectInfo": {"리디렉션":"0","Redirect_Destination":" "},"id":"9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d "을 (를)*

hello 가져오기 도구 (따옴표로 묶인된 값은 항상 처리 문자열로) CSV 파일의 따옴표가 없는 값에 대 한 tooinfer 형식 정보를 시도 합니다.  종류 순서에 따라 hello에 알 수: 숫자, datetime, boolean입니다.  

CSV 가져오기에 대 한 다른 작업이 toonote 두 가지가 있습니다.

1. 기본적으로 따옴표가 없는 값이 항상 잘리지만, 따옴표로 묶인 값은 그대로 유지됩니다. 이 동작은 Trim 값 확인란을 선택 또는 hello /s.TrimQuoted 명령줄 옵션은 따옴표로 묶을 hello로 재정의할 수 있습니다.
2. 기본적으로는 따옴표가 없는 null은 null 값으로 처리됩니다. 이 동작을 재정의할 수 있습니다 (예: "null" 문자열로 따옴표로 표시 되지 않은 null 처리) hello NULL 문자열 hello 또는 확인란 /s.NoUnquotedNulls 명령줄 옵션으로 따옴표가 없는 Treat로 합니다.

CSV 가져오기에 대한 명령줄 샘플은 다음과 같습니다.

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <a id="AzureTableSource"></a>Azure 테이블 저장소에서 tooimport
hello Azure 테이블 저장소 소스 가져오기 옵션 개별 Azure 테이블 저장소 테이블에서 tooimport 있으며 필요에 따라 가져온 hello 테이블 엔터티 toobe를 필터링 합니다. Hello 테이블 API와 함께 사용할 hello 데이터 마이그레이션 도구 tooimport Azure 테이블 저장소 데이터를 사용할 Azure Cosmos DB에 수 없다는 note 합니다. 이 이번에만 hello DocumentDB API와 함께 사용할 Cosmos DB tooAzure를 가져오기는 지원 됩니다.

![Azure 테이블 저장소 원본 옵션의 스크린샷](./media/import-data/azuretablesource.png)

hello hello Azure 테이블 저장소 연결 문자열의 형식은 다음과 같습니다.

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> Hello 연결 문자열 필드에 지정 된 Azure 테이블 저장소 인스턴스 hello를 사용 하 여 hello Verify 명령 tooensure 액세스할 수 있습니다.
> 
> 

Hello Azure의 hello 이름을 입력 테이블 데이터를 가져옵니다. 필요에 따라 [필터](https://msdn.microsoft.com/library/azure/ff683669.aspx)를 지정할 수 있습니다.

hello Azure 테이블 저장소 소스 가져오기 옵션에는 다음 추가 옵션 hello에 있습니다.

1. 내부 필드 포함
   1. 모두 - 모든 내부 필드 포함(PartitionKey, RowKey 및 Timestamp)
   2. 없음 - 모든 내부 필드 제외
   3. RowKey-만 hello RowKey 필드를 포함 합니다.
2. 열 선택
   1. Azure 테이블 저장소 필터는 프로젝션을 지원하지 않습니다. Tooonly 가져오기 특정 Azure 테이블 엔터티 속성을 사용 하도록 하려는 경우 해당 toohello 열 선택 목록을 추가 합니다. 다른 모든 엔터티 속성은 무시됩니다.

Azure 테이블 저장소에서 명령줄 샘플 tooimport 다음과 같습니다.

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <a id="DynamoDBSource"></a>Amazon DynamoDB에서 tooimport
hello Amazon DynamoDB 소스 가져오기 옵션 개별 Amazon DynamoDB 테이블에서 tooimport 있으며 필요에 따라 가져온 hello 엔터티 toobe를 필터링 합니다. 여러 템플릿이 제공되므로 가져오기를 최대한 쉽게 설정할 수 있습니다.

![Amazon DynamoDB 원본 옵션의 스크린샷 - 데이터베이스 마이그레이션 도구](./media/import-data/dynamodbsource1.png)

![Amazon DynamoDB 원본 옵션의 스크린샷 - 데이터베이스 마이그레이션 도구](./media/import-data/dynamodbsource2.png)

hello hello Amazon DynamoDB 연결 문자열의 형식은 다음과 같습니다.

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> Hello 연결 문자열 필드에 지정 된 Amazon DynamoDB 인스턴스에 hello를 사용 하 여 hello Verify 명령 tooensure 액세스할 수 있습니다.
> 
> 

Amazon DynamoDB에서 명령줄 샘플 tooimport 다음과 같습니다.

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <a id="BlobImport"></a>Azure Blob 저장소에서 tooimport 파일
hello JSON 파일, MongoDB 내보내기 파일 및 CSV 파일 소스 가져오기 옵션을 사용 하면 tooimport Azure Blob 저장소에서 하나 이상의 파일입니다. Blob 컨테이너 URL 및 계정 키를 지정한 후 정규식 tooselect hello 파일 tooimport를 제공 합니다.

![Blob 파일 원본 옵션의 스크린샷](./media/import-data/blobsource.png)

다음은 Azure Blob 저장소에서 명령줄 예제 tooimport JSON 파일입니다.

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <a id="DocumentDBSource"></a>Azure Cosmos DB DocumentDB API 컬렉션에서 tooimport
hello Azure Cosmos DB 소스 가져오기 옵션 tooimport 데이터를 Azure Cosmos DB 컬렉션 하나 이상 있으며 필요에 따라 쿼리를 사용 하 여 문서를 필터링 합니다.  

![Azure Cosmos DB 원본 옵션의 스크린샷](./media/import-data/documentdbsource.png)

hello hello Azure Cosmos DB 연결 문자열의 형식은 다음과 같습니다.

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

에 설명 된 대로 hello Azure 포털의 hello 키 블레이드에서에서 hello Azure Cosmos DB 계정 연결 문자열을 검색할 수 있습니다 [어떻게 toomanage Azure Cosmos DB 계정](manage-account.md)hello 데이터베이스의 이름을 hello 필요한 추가 toobe toohello 있지만, 형식에 따라 hello에 대 한 연결 문자열:

    Database=<CosmosDB Database>;

> [!NOTE]
> Hello 연결 문자열 필드에 지정 된 Azure Cosmos DB 인스턴스에 hello를 사용 하 여 hello Verify 명령 tooensure 액세스할 수 있습니다.
> 
> 

단일 Azure Cosmos DB 컬렉션에서 tooimport hello 컬렉션 데이터를 가져올 hello 이름을 입력 하십시오. 여러 Azure Cosmos DB 컬렉션에서 tooimport 제공 정규식 toomatch 하나 이상의 컬렉션 이름 (예: collection01 | collection02 | collection03). 수 필요에 따라 지정, 또는 쿼리 tooboth 필터에 대 한 파일을 제공 하 고 가져올 hello 데이터 toobe 셰이프.

> [!NOTE]
> Hello 컬렉션 필드 이름에 정규식 문자가 단일 컬렉션에서 가져오는 경우 정규식, 허용, 이후 다음 해당 문자가 이스케이프 되어야 합니다 적절 하 게 합니다.
> 
> 

hello Azure Cosmos DB 소스 가져오기 옵션 hello 다음과 같은 고급 옵션에 있습니다.

1. 내부 필드를 포함 하 hello에서 tooinclude Azure Cosmos DB 문서 시스템 속성 (예:: _rid, _ts) 내보내기 여부를 지정 합니다.
2. 실패 시 다시 시도 횟수: hello tooretry hello 일시적 오류 (예: 네트워크 연결 중단)의 경우 연결 tooAzure Cosmos DB 시간 수를 지정 합니다.
3. 다시 시도 간격: 일시적인 오류 (예: 네트워크 연결 중단)의 경우 hello 연결 tooAzure Cosmos DB를 다시 시도 사이의 시간 toowait를 지정 합니다.
4. 연결 모드: Azure Cosmos DB와 함께 hello 연결 모드 toouse를 지정합니다. hello 사용 가능한 선택 항목은 DirectTcp, DirectHttps, 및 게이트웨이입니다. hello 직접 연결 모드는 보다 빠르게 hello 게이트웨이 모드는 더 많은 방화벽 포트 443만 사용 하므로 합니다.

![Azure Cosmos DB 원본 고급 옵션의 스크린샷](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> hello는 DirectTcp 도구 기본값 tooconnection 모드를 가져옵니다. 방화벽 문제를 발생 하는 경우 포트 443만 해야 하므로 tooconnection 모드 게이트웨이 전환 합니다.
> 
> 

다음은 Azure Cosmos DB에서 일부 명령줄 샘플 tooimport가입니다.

    #Migrate data from one Azure Cosmos DB collection tooanother Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections tooa single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection tooa JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> hello Azure Cosmos DB 데이터 가져오기 도구는 또한 hello에서 데이터를 가져오도록 지원 [Azure Cosmos DB 에뮬레이터](local-emulator.md)합니다. 로컬 에뮬레이터에서 데이터를 가져올 때 설정 hello 끝점 너무`https://localhost:<port>`합니다. 
> 
> 

## <a id="HBaseSource"></a>HBase에서 tooimport
hello HBase 소스 가져오기 옵션 tooimport HBase 테이블을 데이터로 있으며 필요에 따라 hello 데이터를 필터링 합니다. 여러 템플릿이 제공되므로 가져오기를 최대한 쉽게 설정할 수 있습니다.

![HBase 원본 옵션의 스크린샷](./media/import-data/hbasesource1.png)

![HBase 원본 옵션의 스크린샷](./media/import-data/hbasesource2.png)

hello hello HBase Stargate 연결 문자열의 형식은 다음과 같습니다.

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> Hello 연결 문자열 필드에 지정 된 HBase 인스턴스 hello를 사용 하 여 hello Verify 명령 tooensure 액세스할 수 있습니다.
> 
> 

HBase에서 명령줄 샘플 tooimport 다음과 같습니다.

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <a id="DocumentDBBulkTarget"></a>tooimport toohello DocumentDB API (대량 가져오기)
hello Azure Cosmos DB 대량 가져오기를 사용 하면 효율성을 위해 Azure Cosmos DB 저장 프로시저를 사용 하 여 hello 사용 가능한 대상 옵션 중 하나에서 tooimport 있습니다. hello 도구 가져오기 tooone 단일 분할 Azure Cosmos DB 컬렉션 뿐만 아니라 여러 단일 분할 Azure Cosmos DB 컬렉션 간에 데이터를 분할 하는 그에 따라 분할 가져오기를 지원 합니다. 데이터를 분할하는 방법에 대한 자세한 내용은 [Azure Cosmos DB에서 분할 및 크기 조정](partition-data.md)을 참조하세요. hello 도구, 실행을 만들고 hello 대상 커넥터가 컬렉션에서 hello 저장 프로시저를 삭제 합니다.  

![Azure Cosmos DB 대량 옵션의 스크린샷](./media/import-data/documentdbbulk.png)

hello hello Azure Cosmos DB 연결 문자열의 형식은 다음과 같습니다.

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

에 설명 된 대로 hello Azure 포털의 hello 키 블레이드에서에서 hello Azure Cosmos DB 계정 연결 문자열을 검색할 수 있습니다 [어떻게 toomanage Azure Cosmos DB 계정](manage-account.md)hello 데이터베이스의 이름을 hello 필요한 추가 toobe toohello 있지만, 형식에 따라 hello에 대 한 연결 문자열:

    Database=<CosmosDB Database>;

> [!NOTE]
> Hello 연결 문자열 필드에 지정 된 Azure Cosmos DB 인스턴스에 hello를 사용 하 여 hello Verify 명령 tooensure 액세스할 수 있습니다.
> 
> 

tooimport tooa 컬렉션을 단일, hello 컬렉션 toowhich hello 추가 단추를 클릭을 가져와서 데이터의 hello 이름을 입력 합니다. tooimport toomultiple 컬렉션, 개별적으로 각 컬렉션 이름을 입력 하거나 여러 컬렉션 구문 toospecify 다음 hello를 사용 하 여: *collection_prefix*[시작 인덱스-끝 인덱스]. Hello 앞에서 언급 한 구문을 통해 여러 컬렉션을 지정할 때는 hello 다음 염두에서에 둬야 합니다.

1. 정수 범위 이름 패턴만 지원됩니다. 예를 들어 컬렉션 [0-3]을 지정 하는 # 컬렉션 다음 hello: collection0, collection1, collection2, collection3 합니다.
2. 축약된 구문을 사용할 수 있습니다. [3] 컬렉션은 1단계에서 설명한 동일한 집합을 내보냅니다.
3. 둘 이상의 대체를 제공할 수 있습니다. 예를 들어, 컬렉션 [0-1] [0-9]는 0이 이름 앞에 오는 20개의 컬렉션을 생성합니다(collection01,... 02... 03).

Hello 컬렉션 이름 지정 된, 일단 hello 커넥터가 컬렉션 (400 RUs too10, 000 RUs)의 hello 원하는 처리량을 선택 합니다. 가져오기 성능을 최적화하려면 더 높은 처리량을 선택합니다. 성능 수준에 대한 자세한 내용은 [Azure Cosmos DB의 성능 수준](performance-levels.md)을 참조하세요.

> [!NOTE]
> hello 성능 처리량 설정은 toocollection 만들기만을 적용 됩니다. Hello를 지정 된 컬렉션에 이미 있는, 해당 처리량 수정 되지 않습니다.
> 
> 

Toomultiple 컬렉션을 가져올 때 hello 가져오기 도구 해시 기반 분할을 지원 합니다. 이 시나리오에서는 파티션 키 hello 처럼 원하는 toouse hello 문서 속성을 지정 (파티션 키에 정보를 입력 하지 않으면 문서 수는 분할 임의로 hello 대상 컬렉션 마다).

필요에 따라 hello 가져오기 원본의 어떤 필드로 hello Azure Cosmos DB 문서 id 속성으로 hello 가져오기 (참고 하는 경우 문서에는이 속성이 포함 되지 않은, hello 가져오기 도구 생성 합니다 hello id 속성 값으로 GUID) 하는 동안 사용 해야 지정할 수 있습니다.

가져오는 동안 사용할 수 있는 다양한 고급 옵션이 있습니다. 첫째, hello 도구에 포함 되어 있는 동안 기본 대량 가져오기 (BulkInsert.js) 저장된 프로시저, toospecify 가져오기 저장 프로시저를 직접 선택할 수 있습니다.

 ![Azure Cosmos DB 대량 삽입 저장 프로시저 옵션의 스크린샷](./media/import-data/bulkinsertsp.png)

또한 SQL Server 또는 MongoDB 등에서 날짜 형식을 가져오는 경우 다음 3개의 가져오기 옵션 중에서 선택할 수 있습니다.

 ![Azure Cosmos DB 날짜/시간 가져오기 옵션의 스크린샷](./media/import-data/datetimeoptions.png)

* 문자열: 문자열 값으로 유지
* Epoch: Epoch 숫자 값으로 유지
* 둘 다: 문자열 및 Epoch 숫자 값으로 유지. 이 옵션은 하위 문서를 만듭니다(예: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }).

hello Azure Cosmos DB 대량 가져오기 hello 다음을 추가 고급 옵션에 있습니다.

1. 일괄 처리 크기: hello 도구 기본값 tooa 일괄 처리 크기 50입니다.  가져온 hello 문서 toobe 큰 경우 hello 일괄 처리 크기를 낮추는 것을 고려 합니다. 반대로, 가져온 hello 문서 toobe 작은 경우에 hello 일괄 처리 크기를 발생 하는 것이 좋습니다.
2. 최대 스크립트 크기 (바이트): hello 도구 기본값 tooa 최대 스크립트 크기는 512KB
3. 자동 Id 생성을 사용 안 함: 가져온 모든 문서 toobe 들어 id 필드는 다음이 옵션을 선택 하면 성능을 향상 시킬 수입니다. 고유 ID 필드가 없는 문서는 가져오지 않습니다.
4. 기존 문서를 업데이트: hello 도구 기본값 toonot id가 충돌할 기존 문서를 바꿉니다. 이 옵션을 선택하면 기존 문서를 일치하는 ID로 덮어쓸 수 있습니다. 이 기능은 기존 문서를 업데이트하는 예약된 데이터 마이그레이션에 유용합니다.
5. 실패 시 다시 시도 횟수: hello tooretry hello 일시적 오류 (예: 네트워크 연결 중단)의 경우 연결 tooAzure Cosmos DB 시간 수를 지정 합니다.
6. 다시 시도 간격: 일시적인 오류 (예: 네트워크 연결 중단)의 경우 hello 연결 tooAzure Cosmos DB를 다시 시도 사이의 시간 toowait를 지정 합니다.
7. 연결 모드: Azure Cosmos DB와 함께 hello 연결 모드 toouse를 지정합니다. hello 사용 가능한 선택 항목은 DirectTcp, DirectHttps, 및 게이트웨이입니다. hello 직접 연결 모드는 보다 빠르게 hello 게이트웨이 모드는 더 많은 방화벽 포트 443만 사용 하므로 합니다.

![Azure Cosmos DB 대량 가져오기 고급 옵션의 스크린샷](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> hello는 DirectTcp 도구 기본값 tooconnection 모드를 가져옵니다. 방화벽 문제를 발생 하는 경우 포트 443만 해야 하므로 tooconnection 모드 게이트웨이 전환 합니다.
> 
> 

## <a id="DocumentDBSeqTarget"></a>tooimport toohello DocumentDB API (순차적 레코드 가져오기)
hello Azure Cosmos DB 순차적 레코드 가져오기 레코드 별로 hello 사용 가능한 대상 옵션 중 하나에서 tooimport가 있습니다. 저장된 프로시저의 할당량에 도달한 tooan 기존 컬렉션을 가져오는 경우이 옵션을 선택할 수 있습니다. hello 도구 지원 가져오기 tooa (단일 파티션 및 다중 파티션) Azure Cosmos DB 컬렉션 뿐만 아니라 여러 단일 파티션 및/또는 다중 파티션 Azure Cosmos DB 컬렉션 간에 데이터를 분할 하는 그에 따라 분할 가져오기 단일. 데이터를 분할하는 방법에 대한 자세한 내용은 [Azure Cosmos DB에서 분할 및 크기 조정](partition-data.md)을 참조하세요.

![Azure Cosmos DB 순차 레코드 가져오기 옵션의 스크린샷](./media/import-data/documentdbsequential.png)

hello hello Azure Cosmos DB 연결 문자열의 형식은 다음과 같습니다.

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

에 설명 된 대로 hello Azure 포털의 hello 키 블레이드에서에서 hello Azure Cosmos DB 계정 연결 문자열을 검색할 수 있습니다 [어떻게 toomanage Azure Cosmos DB 계정](manage-account.md)hello 데이터베이스의 이름을 hello 필요한 추가 toobe toohello 있지만, 형식에 따라 hello에 대 한 연결 문자열:

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> Hello 연결 문자열 필드에 지정 된 Azure Cosmos DB 인스턴스에 hello를 사용 하 여 hello Verify 명령 tooensure 액세스할 수 있습니다.
> 
> 

tooimport tooa 컬렉션을 단일, hello 컬렉션 toowhich hello 추가 단추를 클릭을 가져와서 데이터의 hello 이름을 입력 합니다. tooimport toomultiple 컬렉션, 개별적으로 각 컬렉션 이름을 입력 하거나 여러 컬렉션 구문 toospecify 다음 hello를 사용 하 여: *collection_prefix*[시작 인덱스-끝 인덱스]. Hello 앞에서 언급 한 구문을 통해 여러 컬렉션을 지정할 때는 hello 다음 염두에서에 둬야 합니다.

1. 정수 범위 이름 패턴만 지원됩니다. 예를 들어 컬렉션 [0-3]을 지정 하는 # 컬렉션 다음 hello: collection0, collection1, collection2, collection3 합니다.
2. 축약된 구문을 사용할 수 있습니다. [3] 컬렉션은 1단계에서 설명한 동일한 집합을 내보냅니다.
3. 둘 이상의 대체를 제공할 수 있습니다. 예를 들어, 컬렉션 [0-1] [0-9]는 0이 이름 앞에 오는 20개의 컬렉션을 생성합니다(collection01,... 02... 03).

Hello 컬렉션 이름 지정 된, 일단 hello 커넥터가 컬렉션 (400 RUs too250, 000 RUs)의 hello 원하는 처리량을 선택 합니다. 가져오기 성능을 최적화하려면 더 높은 처리량을 선택합니다. 성능 수준에 대한 자세한 내용은 [Azure Cosmos DB의 성능 수준](performance-levels.md)을 참조하세요. 처리량 toocollections import가 있으면 > 10, 000 RUs 파티션 키가 필요 합니다. Toohave 250, 000 개 이상의 RUs를 선택 하면 toofile 계정 증가 hello 포털 toohave에서 요청 해야 합니다.

> [!NOTE]
> hello 처리량 설정은 toocollection 만들기만을 적용 됩니다. Hello를 지정 된 컬렉션에 이미 있는, 해당 처리량 수정 되지 않습니다.
> 
> 

Toomultiple 컬렉션을 가져올 때 hello 가져오기 도구 해시 기반 분할을 지원 합니다. 이 시나리오에서는 파티션 키 hello 처럼 원하는 toouse hello 문서 속성을 지정 (파티션 키에 정보를 입력 하지 않으면 문서 수는 분할 임의로 hello 대상 컬렉션 마다).

필요에 따라 hello 가져오기 원본의 어떤 필드로 hello Azure Cosmos DB 문서 id 속성으로 hello 가져오기 (참고 하는 경우 문서에는이 속성이 포함 되지 않은, hello 가져오기 도구 생성 합니다 hello id 속성 값으로 GUID) 하는 동안 사용 해야 지정할 수 있습니다.

가져오는 동안 사용할 수 있는 다양한 고급 옵션이 있습니다. 먼저, SQL Server 또는 MongoDB 등에서 날짜 형식을 가져오는 경우 다음 3개의 가져오기 옵션 중에서 선택할 수 있습니다.

 ![Azure Cosmos DB 날짜/시간 가져오기 옵션의 스크린샷](./media/import-data/datetimeoptions.png)

* 문자열: 문자열 값으로 유지
* Epoch: Epoch 숫자 값으로 유지
* 둘 다: 문자열 및 Epoch 숫자 값으로 유지. 이 옵션은 하위 문서를 만듭니다(예: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }).

hello Azure Cosmos DB-순차적 레코드 가져오기에 hello 다음의 추가 고급 옵션:

1. 병렬 요청 수: hello 도구 기본값 too2 병렬 요청 합니다. 가져온 hello 문서 toobe 작은 경우에 병렬 요청의 hello 수 발생 하는 것이 좋습니다. 이 번호를 너무 많이 발생 하는 경우 hello 가져오기는 조정이 발생할 수 있습니다.
2. 자동 Id 생성을 사용 안 함: 가져온 모든 문서 toobe 들어 id 필드는 다음이 옵션을 선택 하면 성능을 향상 시킬 수입니다. 고유 ID 필드가 없는 문서는 가져오지 않습니다.
3. 기존 문서를 업데이트: hello 도구 기본값 toonot id가 충돌할 기존 문서를 바꿉니다. 이 옵션을 선택하면 기존 문서를 일치하는 ID로 덮어쓸 수 있습니다. 이 기능은 기존 문서를 업데이트하는 예약된 데이터 마이그레이션에 유용합니다.
4. 실패 시 다시 시도 횟수: hello tooretry hello 일시적 오류 (예: 네트워크 연결 중단)의 경우 연결 tooAzure Cosmos DB 시간 수를 지정 합니다.
5. 다시 시도 간격: 일시적인 오류 (예: 네트워크 연결 중단)의 경우 hello 연결 tooAzure Cosmos DB를 다시 시도 사이의 시간 toowait를 지정 합니다.
6. 연결 모드: Azure Cosmos DB와 함께 hello 연결 모드 toouse를 지정합니다. hello 사용 가능한 선택 항목은 DirectTcp, DirectHttps, 및 게이트웨이입니다. hello 직접 연결 모드는 보다 빠르게 hello 게이트웨이 모드는 더 많은 방화벽 포트 443만 사용 하므로 합니다.

![Azure Cosmos DB 순차 레코드 가져오기 고급 옵션의 스크린샷](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> hello는 DirectTcp 도구 기본값 tooconnection 모드를 가져옵니다. 방화벽 문제를 발생 하는 경우 포트 443만 해야 하므로 tooconnection 모드 게이트웨이 전환 합니다.
> 
> 

## <a id="IndexingPolicy"></a>Azure Cosmos DB 컬렉션을 만들 때 인덱싱 정책 지정
가져오는 동안 도구 toocreate 컬렉션 hello 마이그레이션을 허용 하는 경우에 hello 컬렉션의 hello 인덱싱 정책을 지정할 수 있습니다. 고급 옵션 섹션 hello Azure Cosmos DB 대량 가져오기 및 Azure Cosmos 순차적 DB 기록 옵션 hello, toohello 인덱싱 정책 섹션을 찾습니다.

![Azure Cosmos DB 인덱싱 정책 고급 옵션의 스크린샷](./media/import-data/indexingpolicy1.png)

Hello 인덱싱 정책 고급 옵션을 사용 하 여 있습니다 수 인덱싱 정책 파일 선택, 수동으로 입력 한 인덱싱 정책을 하거나 (hello 인덱싱 정책 텍스트 상자에서에서 마우스 오른쪽 단추로 클릭)에서 기본 템플릿 중 집합에서 선택 합니다.

hello 도구를 제공 하는 hello 정책 템플릿은 다음과 같습니다.

* 기본값 이 정책은 문자열에 대해 같음 쿼리를 수행하고 숫자에 대해 ORDER BY, 범위 및 같음 쿼리를 사용할 때 가장 좋습니다. 이 정책에는 범위보다 더 낮은 인덱스 저장소 오버헤드가 있습니다.
* 범위입니다. 이 정책은 숫자와 문자열 모두에 ORDER BY, 범위 및 같음 쿼리를 사용할 때 가장 좋습니다. 이 정책에는 기본값 또는 해시보다 더 높은 인덱스 저장소 오버헤드가 있습니다.

![Azure Cosmos DB 인덱싱 정책 고급 옵션의 스크린샷](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> 인덱싱 정책을 지정 하지 않으면 hello 기본 정책이 적용 됩니다. 인덱싱 정책에 대한 자세한 내용은 [Azure Cosmos DB 인덱싱 정책](indexing-policies.md)을 참조하세요.
> 
> 

## <a name="export-toojson-file"></a>내보내기 tooJSON 파일
hello Azure Cosmos DB JSON 내보내기 허용 tooexport hello 사용 가능한 원본 옵션 tooa 포함 된 JSON 파일의 JSON 문서 배열 중 하나입니다. hello 내보내기,를 처리 하는 hello 도구 또는 tooview hello 결과 마이그레이션 명령을 선택 하 고 hello 명령을 직접 실행할 수 있습니다. hello 결과 JSON 파일은 로컬로 또는 Azure Blob 저장소에 저장 될 수 있습니다.

![Azure Cosmos DB JSON 로컬 파일 내보내기 옵션의 스크린샷](./media/import-data/jsontarget.png)

![Azure Cosmos DB JSON Azure Blob Storage 내보내기 옵션의 스크린샷](./media/import-data/jsontarget2.png)

필요에 따라 더 많은 사람이 읽을 수 있는 내용을 hello를 만드는 동안 hello 결과 문서의 hello 크기가 늘어납니다 JSON 결과 tooprettify hello를 선택할 수 있습니다.

    Standard JSON export
    [{"id":"Sample","Title":"About Paris","Language":{"Name":"English"},"Author":{"Name":"Don","Location":{"City":"Paris","Country":"France"}},"Content":"Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.","PageViews":10000,"Topics":[{"Title":"History of Paris"},{"Title":"Places toosee in Paris"}]}]

    Prettified JSON export
    [
     {
    "id": "Sample",
    "Title": "About Paris",
    "Language": {
      "Name": "English"
    },
    "Author": {
      "Name": "Don",
      "Location": {
        "City": "Paris",
        "Country": "France"
      }
    },
    "Content": "Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.",
    "PageViews": 10000,
    "Topics": [
      {
        "Title": "History of Paris"
      },
      {
        "Title": "Places toosee in Paris"
      }
    ]
    }]

## <a name="advanced-configuration"></a>고급 구성
Hello 고급 구성 화면에서 작성 된 모든 오류 원하는 hello 로그 파일 toowhich의 hello 위치를 지정 합니다. 규칙에 따라 hello toothis 페이지를 적용 됩니다.

1. 파일 이름을 제공 하지 않으면, 모든 오류는 hello 결과 페이지에 반환 됩니다.
2. 디렉터리가 없는 파일 이름이 제공 하는 경우 다음 hello 파일 됩니다 (만들거나 덮어쓸) hello 현재 환경 디렉터리에 있습니다.
3. 기존 선택 하는 경우 파일을 다음 hello 파일을 덮어쓰게 됩니다, 그리고 추가 옵션이 없습니다.

그런 다음 선택 여부를 toolog 모든 중요, 또는 오류 메시지가 없습니다. 마지막으로, hello 화면 전송 메시지에는 진행 중으로 업데이트 됩니다 빈도 결정 합니다.

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a>가져오기 설정 확인 및 명령줄 보기
1. 원본 정보, 대상 정보 및 고급 구성을 지정한 후 hello 마이그레이션 요약을 검토 하 고, 필요에 따라 보기/복사 (복사 hello 명령 유용 tooautomate 가져오기 작업을는) 마이그레이션 명령으로 인해 발생 하는 hello:
   
    ![요약 화면의 스크린샷](./media/import-data/summary.png)
   
    ![요약 화면의 스크린샷](./media/import-data/summarycommand.png)
2. 원본 및 대상 옵션이 적절하면 **가져오기**를 클릭합니다. hello 가져오기 진행 중인 hello 경과 시간, 전송 된 개수 및 오류 정보 (hello 고급 구성에서 파일 이름을 제공 하지 않은) 하는 경우 업데이트 됩니다. 완료 되 면 (예: 모든 가져오기 실패와 toodeal) hello 결과 내보낼 수 있습니다.
   
    ![Azure Cosmos DB JSON 내보내기 옵션의 스크린샷](./media/import-data/viewresults.png)
3. (예: 연결 문자열 정보, 소스 및 대상 선택 등) hello 기존 설정을 유지 하거나 모든 값을 다시 설정 하면 새 가져오기를 시작할 수도 있습니다.
   
    ![Azure Cosmos DB JSON 내보내기 옵션의 스크린샷](./media/import-data/newimport.png)

## <a name="next-steps"></a>다음 단계

이 자습서에서는 hello 다음 작업을 수행 하면:

> [!div class="checklist"]
> * Hello 데이터 마이그레이션 도구 설치
> * 여러 데이터 원본에서 데이터 가져오기
> * Azure Cosmos DB tooJSON에서 내보낸

이제 toohello 다음 자습서를 진행 하 고 알아볼 수 있습니다 어떻게 Azure Cosmos DB를 사용 하 여 tooquery 데이터입니다. 

> [!div class="nextstepaction"]
>[어떻게 tooquery 데이터?](../cosmos-db/tutorial-query-documentdb.md)
