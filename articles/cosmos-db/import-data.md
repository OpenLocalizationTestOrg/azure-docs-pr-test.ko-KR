---
title: "Azure Cosmos DB용 데이터베이스 마이그레이션 도구 | Microsoft Docs"
description: "오픈 소스 Azure Cosmos DB 데이터 마이그레이션 도구를 사용하여 MongoDB, SQL Server, 테이블 저장소, Amazon DynamoDB, CSV 및 JSON 파일을 비롯한 다양한 원본에서 Azure Cosmos DB로 데이터를 가져오는 방법을 알아봅니다. CSV에서 JSON로 변환합니다."
keywords: "csv에서 json으로, 데이터베이스 마이그레이션 도구, csv에서 json으로 변환"
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
ms.openlocfilehash: 23a4a82dbdb611f4da90562af936fca28da9b24d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-import-data-into-azure-cosmos-db-for-the-documentdb-api"></a><span data-ttu-id="16b84-105">DocumentDB API용 Azure Cosmos DB로 어떻게 데이터를 가져오나요?</span><span class="sxs-lookup"><span data-stu-id="16b84-105">How to import data into Azure Cosmos DB for the DocumentDB API?</span></span>

<span data-ttu-id="16b84-106">이 자습서에서는 JSON 파일, CSV 파일, SQL, MongoDB, Azure Table Storage, Amazon DynamoDB 및 Azure Cosmos DB DocumentDB API 컬렉션을 비롯한 다양한 원본에서 Azure Cosmos DB 및 DocumentDB API로 데이터를 가져올 수 있는 Azure Cosmos DB: DocumentDB API 데이터 마이그레이션 도구 사용 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-106">This tutorial provides instructions on using the Azure Cosmos DB: DocumentDB API Data Migration tool, which can import data from various sources, including JSON files, CSV files, SQL, MongoDB, Azure Table storage, Amazon DynamoDB and Azure Cosmos DB DocumentDB API collections into collections for use with Azure Cosmos DB and the DocumentDB API.</span></span> <span data-ttu-id="16b84-107">또한 데이터 마이그레이션 도구는 단일 파티션 컬렉션에서 DocumentDB API용 다중 파티션 컬렉션으로 마이그레이션하는 경우에도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-107">The Data Migration tool can also be used when migrating from a single partition collection to a multi-partition collection for the DocumentDB API.</span></span>

<span data-ttu-id="16b84-108">데이터 마이그레이션 도구는 DocumentDB API에서 사용하기 위해 Azure Cosmos DB로 데이터를 가져오는 경우에만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-108">The Data Migration tool only works when importing data into Azure Cosmos DB for use with the DocumentDB API.</span></span> <span data-ttu-id="16b84-109">현재, Table API 또는 Graph API에서 사용하기 위해 데이터 가져오기는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-109">Importing data for use with the Table API or Graph API is not supported at this time.</span></span> 

<span data-ttu-id="16b84-110">MongoDB API에서 사용하기 위해 데이터를 가져오려면 [Azure Cosmos DB: MongoDB API에서 사용할 데이터를 마이그레이션하는 방법](mongodb-migrate.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16b84-110">To import data for use with the MongoDB API, see [Azure Cosmos DB: How to migrate data for the MongoDB API?](mongodb-migrate.md).</span></span>

<span data-ttu-id="16b84-111">이 자습서에서 다루는 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-111">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="16b84-112">데이터 마이그레이션 도구 설치</span><span class="sxs-lookup"><span data-stu-id="16b84-112">Installing the Data Migration tool</span></span>
> * <span data-ttu-id="16b84-113">다른 데이터 원본에서 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="16b84-113">Importing data from different data sources</span></span>
> * <span data-ttu-id="16b84-114">Azure Cosmos DB에서 JSON으로 내보내기</span><span class="sxs-lookup"><span data-stu-id="16b84-114">Exporting from Azure Cosmos DB to JSON</span></span>

## <span data-ttu-id="16b84-115"><a id="Prerequisites"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="16b84-115"><a id="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="16b84-116">이 문서의 지침을 따르기 전에 다음이 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-116">Before following the instructions in this article, ensure that you have the following installed:</span></span>

* <span data-ttu-id="16b84-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) 이상</span><span class="sxs-lookup"><span data-stu-id="16b84-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) or higher.</span></span>

## <span data-ttu-id="16b84-118"><a id="Overviewl"></a>데이터 마이그레이션 도구 개요</span><span class="sxs-lookup"><span data-stu-id="16b84-118"><a id="Overviewl"></a>Overview of the Data Migration tool</span></span>
<span data-ttu-id="16b84-119">데이터 마이그레이션 도구는 다음을 비롯한 다양한 원본에서 Azure Cosmos DB로 데이터를 가져오는 오픈 소스 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-119">The Data Migration tool is an open source solution that imports data to Azure Cosmos DB from a variety of sources, including:</span></span>

* <span data-ttu-id="16b84-120">JSON 파일</span><span class="sxs-lookup"><span data-stu-id="16b84-120">JSON files</span></span>
* <span data-ttu-id="16b84-121">MongoDB</span><span class="sxs-lookup"><span data-stu-id="16b84-121">MongoDB</span></span>
* <span data-ttu-id="16b84-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="16b84-122">SQL Server</span></span>
* <span data-ttu-id="16b84-123">CSV 파일</span><span class="sxs-lookup"><span data-stu-id="16b84-123">CSV files</span></span>
* <span data-ttu-id="16b84-124">Azure 테이블 저장소</span><span class="sxs-lookup"><span data-stu-id="16b84-124">Azure Table storage</span></span>
* <span data-ttu-id="16b84-125">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="16b84-125">Amazon DynamoDB</span></span>
* <span data-ttu-id="16b84-126">HBase</span><span class="sxs-lookup"><span data-stu-id="16b84-126">HBase</span></span>
* <span data-ttu-id="16b84-127">Azure Cosmos DB 컬렉션</span><span class="sxs-lookup"><span data-stu-id="16b84-127">Azure Cosmos DB collections</span></span>

<span data-ttu-id="16b84-128">가져오기 도구는 그래픽 사용자 인터페이스(dtui.exe)를 포함하지만 명령줄(dt.exe)에서 구동할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-128">While the import tool includes a graphical user interface (dtui.exe), it can also be driven from the command line (dt.exe).</span></span> <span data-ttu-id="16b84-129">실제로 UI를 통해 가져오기를 설정한 후 관련 명령을 출력하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-129">In fact, there is an option to output the associated command after setting up an import through the UI.</span></span> <span data-ttu-id="16b84-130">가져오는 동안 계층 관계(하위 문서)를 만들 수 있도록 테이블 형식 원본 데이터(예: SQL Server 또는 CSV 파일)를 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-130">Tabular source data (e.g. SQL Server or CSV files) can be transformed such that hierarchical relationships (subdocuments) can be created during import.</span></span> <span data-ttu-id="16b84-131">원본 옵션, 각 원본에서 가져오는 샘플 명령줄, 대상 옵션 및 가져오기 결과 보기에 대해 자세히 알아보려면 계속 진행하세요.</span><span class="sxs-lookup"><span data-stu-id="16b84-131">Keep reading to learn more about source options, sample command lines to import from each source, target options, and viewing import results.</span></span>

## <span data-ttu-id="16b84-132"><a id="Install"></a>데이터 마이그레이션 도구 설치</span><span class="sxs-lookup"><span data-stu-id="16b84-132"><a id="Install"></a>Install the Data Migration tool</span></span>
<span data-ttu-id="16b84-133">마이그레이션 도구 소스 코드는 GitHub의 [이 리포지토리](https://github.com/azure/azure-documentdb-datamigrationtool)에서 사용할 수 있으며, 컴파일된 버전은 [Microsoft 다운로드 센터](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-133">The migration tool source code is available on GitHub in [this repository](https://github.com/azure/azure-documentdb-datamigrationtool) and a compiled version is available from [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span></span> <span data-ttu-id="16b84-134">솔루션을 컴파일하거나, 컴파일된 버전을 다운로드하고 선택한 디렉터리에 압축을 풀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-134">You may either compile the solution or simply download and extract the compiled version to a directory of your choice.</span></span> <span data-ttu-id="16b84-135">다음 중 하나를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-135">Then run either:</span></span>

* <span data-ttu-id="16b84-136">**Dtui.exe**: 도구의 그래픽 인터페이스 버전</span><span class="sxs-lookup"><span data-stu-id="16b84-136">**Dtui.exe**: Graphical interface version of the tool</span></span>
* <span data-ttu-id="16b84-137">**Dt.exe**: 도구의 명령줄 버전</span><span class="sxs-lookup"><span data-stu-id="16b84-137">**Dt.exe**: Command-line version of the tool</span></span>

## <a name="import-data"></a><span data-ttu-id="16b84-138">데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="16b84-138">Import data</span></span>

<span data-ttu-id="16b84-139">이 도구를 설치하면 이제 데이터를 가져올 차례입니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-139">Once you've installed the tool, it's time to import your data.</span></span> <span data-ttu-id="16b84-140">어떤 종류의 데이터를 가져오시겠어요?</span><span class="sxs-lookup"><span data-stu-id="16b84-140">What kind of data do you want to import?</span></span>

* [<span data-ttu-id="16b84-141">JSON 파일</span><span class="sxs-lookup"><span data-stu-id="16b84-141">JSON files</span></span>](#JSON)
* [<span data-ttu-id="16b84-142">MongoDB</span><span class="sxs-lookup"><span data-stu-id="16b84-142">MongoDB</span></span>](#MongoDB)
* [<span data-ttu-id="16b84-143">MongoDB 내보내기 파일</span><span class="sxs-lookup"><span data-stu-id="16b84-143">MongoDB Export files</span></span>](#MongoDBExport)
* [<span data-ttu-id="16b84-144">SQL Server</span><span class="sxs-lookup"><span data-stu-id="16b84-144">SQL Server</span></span>](#SQL)
* [<span data-ttu-id="16b84-145">CSV 파일</span><span class="sxs-lookup"><span data-stu-id="16b84-145">CSV files</span></span>](#CSV)
* [<span data-ttu-id="16b84-146">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="16b84-146">Azure Table storage</span></span>](#AzureTableSource)
* [<span data-ttu-id="16b84-147">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="16b84-147">Amazon DynamoDB</span></span>](#DynamoDBSource)
* [<span data-ttu-id="16b84-148">Blob</span><span class="sxs-lookup"><span data-stu-id="16b84-148">Blob</span></span>](#BlobImport)
* [<span data-ttu-id="16b84-149">Azure Cosmos DB 컬렉션</span><span class="sxs-lookup"><span data-stu-id="16b84-149">Azure Cosmos DB collections</span></span>](#DocumentDBSource)
* [<span data-ttu-id="16b84-150">HBase</span><span class="sxs-lookup"><span data-stu-id="16b84-150">HBase</span></span>](#HBaseSource)
* [<span data-ttu-id="16b84-151">Azure Cosmos DB 대량 가져오기</span><span class="sxs-lookup"><span data-stu-id="16b84-151">Azure Cosmos DB bulk import</span></span>](#DocumentDBBulkImport)
* [<span data-ttu-id="16b84-152">Azure Cosmos DB 순차 레코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="16b84-152">Azure Cosmos DB sequential record import</span></span>](#DocumentDSeqTarget)


## <span data-ttu-id="16b84-153"><a id="JSON"></a>JSON 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="16b84-153"><a id="JSON"></a>To import JSON files</span></span>
<span data-ttu-id="16b84-154">JSON 파일 원본 가져오기 옵션을 사용하면 단일 문서 JSON 파일이나 각각 JSON 문서 배열을 포함하는 JSON 파일을 하나 이상 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-154">The JSON file source importer option allows you to import one or more single document JSON files or JSON files that each contain an array of JSON documents.</span></span> <span data-ttu-id="16b84-155">가져올 JSON 파일을 포함하는 폴더를 추가하면, 하위 폴더에서 재귀적으로 파일을 검색하는 옵션도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-155">When adding folders that contain JSON files to import, you have the option of recursively searching for files in subfolders.</span></span>

![JSON 파일 원본 옵션의 스크린샷 - 데이터베이스 마이그레이션 도구](./media/import-data/jsonsource.png)

<span data-ttu-id="16b84-157">JSON 파일을 가져오는 몇 가지 명령줄 샘플은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-157">Here are some command line samples to import JSON files:</span></span>

    #Import a single JSON file
    dt.exe /s:JsonFile /s.Files:.\Sessions.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory of JSON files
    dt.exe /s:JsonFile /s.Files:C:\TESessions\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory (including sub-directories) of JSON files
    dt.exe /s:JsonFile /s.Files:C:\LastFMMusic\**\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Music /t.CollectionThroughput:2500

    #Import a directory (single), directory (recursive), and individual JSON files
    dt.exe /s:JsonFile /s.Files:C:\Tweets\*.*;C:\LargeDocs\**\*.*;C:\TESessions\Session48172.json;C:\TESessions\Session48173.json;C:\TESessions\Session48174.json;C:\TESessions\Session48175.json;C:\TESessions\Session48177.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:subs /t.CollectionThroughput:2500

    #Import a single JSON file and partition the data across 4 collections
    dt.exe /s:JsonFile /s.Files:D:\\CompanyData\\Companies.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:comp[1-4] /t.PartitionKey:name /t.CollectionThroughput:2500

## <span data-ttu-id="16b84-158"><a id="MongoDB"></a>MongoDB에서 가져오기</span><span class="sxs-lookup"><span data-stu-id="16b84-158"><a id="MongoDB"></a>To import from MongoDB</span></span>

> [!IMPORTANT]
> <span data-ttu-id="16b84-159">MongoDB에 대한 지원을 포함한 Azure Cosmos DB 계정을 가져오는 경우 다음 [지침](mongodb-migrate.md)을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-159">If you are importing to an Azure Cosmos DB account with Support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="16b84-160">MongoDB 원본 가져오기 옵션을 사용하면 개별 MongoDB 컬렉션에서 가져오고 필요에 따라 쿼리를 사용하여 문서를 필터링하거나 프로젝션을 사용하여 문서 구조를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-160">The MongoDB source importer option allows you to import from an individual MongoDB collection and optionally filter documents using a query and/or modify the document structure by using a projection.</span></span>  

![MongoDB 원본 옵션의 스크린샷](./media/import-data/mongodbsource.png)

<span data-ttu-id="16b84-162">연결 문자열은 표준 MongoDB 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-162">The connection string is in the standard MongoDB format:</span></span>

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> <span data-ttu-id="16b84-163">Verify 명령을 사용하여 연결 문자열 필드에 지정된 MongoDB 인스턴스를 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-163">Use the Verify command to ensure that the MongoDB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="16b84-164">데이터를 가져올 컬렉션의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-164">Enter the name of the collection from which data will be imported.</span></span> <span data-ttu-id="16b84-165">필요에 따라 쿼리(예: {pop: {$gt: 5000}}) 및/또는 프로젝션(예: {loc:0})에 대한 파일을 제공하여 가져올 데이터를 필터링하고 형식을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-165">You may optionally specify or provide a file for a query (e.g. {pop: {$gt:5000}} ) and/or projection (e.g. {loc:0} ) to both filter and shape the data to be imported.</span></span>

<span data-ttu-id="16b84-166">MongoDB에서 가져오는 몇 가지 명령줄 샘플은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-166">Here are some command line samples to import from MongoDB:</span></span>

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match the query and exclude the loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <span data-ttu-id="16b84-167"><a id="MongoDBExport"></a>MongoDB 내보내기 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="16b84-167"><a id="MongoDBExport"></a>To import MongoDB export files</span></span>

> [!IMPORTANT]
> <span data-ttu-id="16b84-168">MongoDB에 대한 지원을 포함한 Azure Cosmos DB 계정을 가져오는 경우 다음 [지침](mongodb-migrate.md)을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-168">If you are importing to an Azure Cosmos DB account with support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="16b84-169">MongoDB 내보내기 JSON 파일 원본 가져오기 옵션을 사용하면 mongoexport 유틸리티에서 생성된 JSON 파일을 하나 이상 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-169">The MongoDB export JSON file source importer option allows you to import one or more JSON files produced from the mongoexport utility.</span></span>  

![MongoDB 내보내기 원본 옵션의 스크린샷](./media/import-data/mongodbexportsource.png)

<span data-ttu-id="16b84-171">가져올 MongoDB 내보내기 JSON 파일이 포함된 폴더를 추가할 때 하위 폴더의 파일을 재귀적으로 검색하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-171">When adding folders that contain MongoDB export JSON files for import, you have the option of recursively searching for files in subfolders.</span></span>

<span data-ttu-id="16b84-172">MongoDB 내보내기 JSON 파일에서 가져오는 명령줄 샘플은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-172">Here is a command line sample to import from MongoDB export JSON files:</span></span>

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <span data-ttu-id="16b84-173"><a id="SQL"></a>SQL Server에서 가져오기</span><span class="sxs-lookup"><span data-stu-id="16b84-173"><a id="SQL"></a>To import from SQL Server</span></span>
<span data-ttu-id="16b84-174">SQL 원본 가져오기 옵션을 사용하면 개별 SQL Server 데이터베이스에서 가져오고 필요에 따라 쿼리를 사용하여 가져올 레코드를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-174">The SQL source importer option allows you to import from an individual SQL Server database and optionally filter the records to be imported using a query.</span></span> <span data-ttu-id="16b84-175">또한 중첩 구분 기호를 지정하여 문서 구조를 수정할 수 있습니다(추가 정보 제공 예정).</span><span class="sxs-lookup"><span data-stu-id="16b84-175">In addition, you can modify the document structure by specifying a nesting separator (more on that in a moment).</span></span>  

![SQL 원본 옵션의 스크린샷 - 데이터베이스 마이그레이션 도구](./media/import-data/sqlexportsource.png)

<span data-ttu-id="16b84-177">연결 문자열의 형식은 표준 SQL 연결 문자열 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-177">The format of the connection string is the standard SQL connection string format.</span></span>

> [!NOTE]
> <span data-ttu-id="16b84-178">Verify 명령을 사용하여 연결 문자열 필드에 지정된 SQL Server 인스턴스를 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-178">Use the Verify command to ensure that the SQL Server instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="16b84-179">중첩 구분 기호 속성을 사용하여 가져오는 동안 계층 관계(하위 문서)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-179">The nesting separator property is used to create hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="16b84-180">다음과 같은 SQL 쿼리를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="16b84-180">Consider the following SQL query:</span></span>

<span data-ttu-id="16b84-181">*CAST(BusinessEntityID AS varchar)를 ID, Name으로, AddressType을 [Address.AddressType]으로, AddressLine1을 [Address.AddressLine1]로, City를 [Address.Location.City]로, StateProvinceName을 [Address.Location.StateProvinceName]으로, PostalCode를 [Address.PostalCode]로, CountryRegionName을 AddressType='Main Office'인 Sales.vStoreWithAddresses에서 [Address.CountryRegionName]으로 선택합니다.*</span><span class="sxs-lookup"><span data-stu-id="16b84-181">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span></span>

<span data-ttu-id="16b84-182">다음과 같은 (부분) 결과가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-182">Which returns the following (partial) results:</span></span>

![SQL 쿼리 결과의 스크린샷](./media/import-data/sqlqueryresults.png)

<span data-ttu-id="16b84-184">Address.AddressType 및 Address.Location.StateProvinceName과 같은 별칭을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-184">Note the aliases such as Address.AddressType and Address.Location.StateProvinceName.</span></span> <span data-ttu-id="16b84-185">중첩 구분 기호 '.'을 지정하면 가져오기 도구가 가져오는 동안 Address 및 Address.Location 하위 문서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-185">By specifying a nesting separator of ‘.’, the import tool creates Address and Address.Location subdocuments during the import.</span></span> <span data-ttu-id="16b84-186">Azure Cosmos DB의 결과 문서 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-186">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="16b84-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span><span class="sxs-lookup"><span data-stu-id="16b84-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span></span>

<span data-ttu-id="16b84-188">SQL Server에서 가져오는 몇 가지 명령줄 샘플은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-188">Here are some command line samples to import from SQL Server:</span></span>

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <span data-ttu-id="16b84-189"><a id="CSV"></a>CSV 파일을 가져와 CSV를 JSON으로 변환</span><span class="sxs-lookup"><span data-stu-id="16b84-189"><a id="CSV"></a>To import CSV files and convert CSV to JSON</span></span>
<span data-ttu-id="16b84-190">CSV 파일 원본 가져오기 옵션을 사용하면 하나 이상의 CSV 파일을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-190">The CSV file source importer option enables you to import one or more CSV files.</span></span> <span data-ttu-id="16b84-191">가져올 CSV 파일이 포함된 폴더를 추가하면, 하위 폴더에서 재귀적으로 파일을 검색하는 옵션도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-191">When adding folders that contain CSV files for import, you have the option of recursively searching for files in subfolders.</span></span>

![CSV 원본 옵션의 스크린샷 - CSV에서 JSON으로](media/import-data/csvsource.png)

<span data-ttu-id="16b84-193">SQL 원본과 마찬가지로, 중첩 구분 기호 속성을 사용하여 가져오는 동안 계층 관계(하위 문서)를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-193">Similar to the SQL source, the nesting separator property may be used to create hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="16b84-194">다음과 같은 CSV 머리글 행과 데이터 행을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="16b84-194">Consider the following CSV header row and data rows:</span></span>

![CSV 샘플 레코드의 스크린샷 - CSV에서 JSON으로](./media/import-data/csvsample.png)

<span data-ttu-id="16b84-196">DomainInfo.Domain_Name 및 RedirectInfo.Redirecting과 같은 별칭을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="16b84-196">Note the aliases such as DomainInfo.Domain_Name and RedirectInfo.Redirecting.</span></span> <span data-ttu-id="16b84-197">중첩 구분 기호 '.'을 지정하면 가져오기 도구가 가져오는 동안 DomainInfo 및 RedirectInfo 하위 문서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-197">By specifying a nesting separator of ‘.’, the import tool will create DomainInfo and RedirectInfo subdocuments during the import.</span></span> <span data-ttu-id="16b84-198">Azure Cosmos DB의 결과 문서 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-198">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="16b84-199">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of the United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span><span class="sxs-lookup"><span data-stu-id="16b84-199">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of the United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span></span>

<span data-ttu-id="16b84-200">가져오기 도구는 CSV 파일의 따옴표가 없는 값에 대한 형식 정보를 유추하려고 합니다(따옴표로 묶인 값은 항상 문자열로 처리됨).</span><span class="sxs-lookup"><span data-stu-id="16b84-200">The import tool will attempt to infer type information for unquoted values in CSV files (quoted values are always treated as strings).</span></span>  <span data-ttu-id="16b84-201">숫자, 날짜/시간, 부울 순서로 형식이 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-201">Types are identified in the following order: number, datetime, boolean.</span></span>  

<span data-ttu-id="16b84-202">CSV 가져오기에 대해 다른 두 가지 사항을 기억해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-202">There are two other things to note about CSV import:</span></span>

1. <span data-ttu-id="16b84-203">기본적으로 따옴표가 없는 값이 항상 잘리지만, 따옴표로 묶인 값은 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-203">By default, unquoted values are always trimmed for tabs and spaces, while quoted values are preserved as-is.</span></span> <span data-ttu-id="16b84-204">Trim 따옴표로 묶인 값 확인란을 선택 또는 /s.TrimQuoted 명령줄 옵션으로 이 동작을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-204">This behavior can be overridden with the Trim quoted values checkbox or the /s.TrimQuoted command line option.</span></span>
2. <span data-ttu-id="16b84-205">기본적으로는 따옴표가 없는 null은 null 값으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-205">By default, an unquoted null is treated as a null value.</span></span> <span data-ttu-id="16b84-206">따옴표가 없는 NULL을 문자열 확인란이나 /s.NoUnquotedNulls 명령줄 옵션으로 이 동작을 재정의할 수 있습니다(예: "null" 문자열로 따옴표가 없는 null 처리).</span><span class="sxs-lookup"><span data-stu-id="16b84-206">This behavior can be overridden (i.e. treat an unquoted null as a “null” string) with the Treat unquoted NULL as string checkbox or the /s.NoUnquotedNulls command line option.</span></span>

<span data-ttu-id="16b84-207">CSV 가져오기에 대한 명령줄 샘플은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-207">Here is a command line sample for CSV import:</span></span>

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <span data-ttu-id="16b84-208"><a id="AzureTableSource"></a>Azure Table Storage에서 가져오기</span><span class="sxs-lookup"><span data-stu-id="16b84-208"><a id="AzureTableSource"></a>To import from Azure Table storage</span></span>
<span data-ttu-id="16b84-209">Azure 테이블 저장소 원본 가져오기 옵션을 사용하면 개별 Azure 테이블 저장소 테이블에서 가져오고 필요에 따라 가져올 테이블 엔터티를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-209">The Azure Table storage source importer option allows you to import from an individual Azure Table storage table and optionally filter the table entities to be imported.</span></span> <span data-ttu-id="16b84-210">Table API에 사용하기 위해 Azure Table Storage 데이터를 Azure Cosmos DB로 가져오는 데에는 이 데이터 마이그레이션 도구를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-210">Note that you cannot use the Data Migration tool to import Azure Table storage data into Azure Cosmos DB for use with the Table API.</span></span> <span data-ttu-id="16b84-211">현재, DocumentDB API에 사용하기 위해 Azure Cosmos DB로 가져오기만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-211">Only importing to Azure Cosmos DB for use with the DocumentDB API is supported at this time.</span></span>

![Azure 테이블 저장소 원본 옵션의 스크린샷](./media/import-data/azuretablesource.png)

<span data-ttu-id="16b84-213">Azure 테이블 저장소 연결 문자열의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-213">The format of the Azure Table storage connection string is:</span></span>

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> <span data-ttu-id="16b84-214">Verify 명령을 사용하여 연결 문자열 필드에 지정된 Azure 테이블 저장소 인스턴스를 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-214">Use the Verify command to ensure that the Azure Table storage instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="16b84-215">데이터를 가져올 Azure 테이블의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-215">Enter the name of the Azure table from which data will be imported.</span></span> <span data-ttu-id="16b84-216">필요에 따라 [필터](https://msdn.microsoft.com/library/azure/ff683669.aspx)를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-216">You may optionally specify a [filter](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span></span>

<span data-ttu-id="16b84-217">Azure 테이블 저장소 원본 가져오기 옵션에는 다음과 같은 추가 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-217">The Azure Table storage source importer option has the following additional options:</span></span>

1. <span data-ttu-id="16b84-218">내부 필드 포함</span><span class="sxs-lookup"><span data-stu-id="16b84-218">Include Internal Fields</span></span>
   1. <span data-ttu-id="16b84-219">모두 - 모든 내부 필드 포함(PartitionKey, RowKey 및 Timestamp)</span><span class="sxs-lookup"><span data-stu-id="16b84-219">All - Include all internal fields (PartitionKey, RowKey, and Timestamp)</span></span>
   2. <span data-ttu-id="16b84-220">없음 - 모든 내부 필드 제외</span><span class="sxs-lookup"><span data-stu-id="16b84-220">None - Exclude all internal fields</span></span>
   3. <span data-ttu-id="16b84-221">RowKey - RowKey 필드만 포함</span><span class="sxs-lookup"><span data-stu-id="16b84-221">RowKey - Only include the RowKey field</span></span>
2. <span data-ttu-id="16b84-222">열 선택</span><span class="sxs-lookup"><span data-stu-id="16b84-222">Select Columns</span></span>
   1. <span data-ttu-id="16b84-223">Azure 테이블 저장소 필터는 프로젝션을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-223">Azure Table storage filters do not support projections.</span></span> <span data-ttu-id="16b84-224">특정 Azure 테이블 엔터티 속성만 가져오려는 경우 열 선택 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-224">If you want to only import specific Azure Table entity properties, add them to the Select Columns list.</span></span> <span data-ttu-id="16b84-225">다른 모든 엔터티 속성은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-225">All other entity properties will be ignored.</span></span>

<span data-ttu-id="16b84-226">Azure 테이블 저장소에서 가져오는 명령줄 샘플은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-226">Here is a command line sample to import from Azure Table storage:</span></span>

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <span data-ttu-id="16b84-227"><a id="DynamoDBSource"></a>Amazon DynamoDB에서 가져오기</span><span class="sxs-lookup"><span data-stu-id="16b84-227"><a id="DynamoDBSource"></a>To import from Amazon DynamoDB</span></span>
<span data-ttu-id="16b84-228">Amazon DynamoDB 원본 가져오기 옵션을 사용하면 개별 Amazon DynamoDB 테이블에서 가져오고 필요에 따라 가져올 엔터티를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-228">The Amazon DynamoDB source importer option allows you to import from an individual Amazon DynamoDB table and optionally filter the entities to be imported.</span></span> <span data-ttu-id="16b84-229">여러 템플릿이 제공되므로 가져오기를 최대한 쉽게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-229">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Amazon DynamoDB 원본 옵션의 스크린샷 - 데이터베이스 마이그레이션 도구](./media/import-data/dynamodbsource1.png)

![Amazon DynamoDB 원본 옵션의 스크린샷 - 데이터베이스 마이그레이션 도구](./media/import-data/dynamodbsource2.png)

<span data-ttu-id="16b84-232">Amazon DynamoDB 연결 문자열의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-232">The format of the Amazon DynamoDB connection string is:</span></span>

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> <span data-ttu-id="16b84-233">Verify 명령을 사용하여 연결 문자열 필드에 지정된 Amazon DynamoDB 인스턴스를 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-233">Use the Verify command to ensure that the Amazon DynamoDB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="16b84-234">Amazon DynamoDB에서 가져오는 명령줄 샘플은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-234">Here is a command line sample to import from Amazon DynamoDB:</span></span>

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <span data-ttu-id="16b84-235"><a id="BlobImport"></a>Azure Blob Storage에서 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="16b84-235"><a id="BlobImport"></a>To import files from Azure Blob storage</span></span>
<span data-ttu-id="16b84-236">JSON 파일, MongoDB 내보내기 파일 및 CSV 파일 원본 가져오기 옵션을 통해 Azure Blob 저장소에서 하나 이상의 파일을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-236">The JSON file, MongoDB export file, and CSV file source importer options allow you to import one or more files from Azure Blob storage.</span></span> <span data-ttu-id="16b84-237">Blob 컨테이너 URL 및 계정 키를 지정한 후에 가져올 파일을 선택하는 정규식을 제공하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-237">After specifying a Blob container URL and Account Key, simply provide a regular expression to select the file(s) to import.</span></span>

![Blob 파일 원본 옵션의 스크린샷](./media/import-data/blobsource.png)

<span data-ttu-id="16b84-239">Azure Blob 저장소에서 JSON 파일을 가져오려면 명령줄 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-239">Here is command line sample to import JSON files from Azure Blob storage:</span></span>

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <span data-ttu-id="16b84-240"><a id="DocumentDBSource"></a>Azure Cosmos DB DocumentDB API 컬렉션에서 가져오려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-240"><a id="DocumentDBSource"></a>To import from an Azure Cosmos DB DocumentDB API collection</span></span>
<span data-ttu-id="16b84-241">Azure Cosmos DB 원본 가져오기 옵션을 사용하면 필요에 따라 쿼리를 사용하여 문서를 필터링하고 하나 이상의 Azure Cosmos DB 컬렉션에서 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-241">The Azure Cosmos DB source importer option allows you to import data from one or more Azure Cosmos DB collections and optionally filter documents using a query.</span></span>  

![Azure Cosmos DB 원본 옵션의 스크린샷](./media/import-data/documentdbsource.png)

<span data-ttu-id="16b84-243">Azure Cosmos DB 연결 문자열의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-243">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="16b84-244">[Azure Cosmos DB 계정을 관리하는 방법](manage-account.md)에 설명된 대로 Azure Cosmos DB 계정 연결 문자열은 Azure Portal의 키 블레이드에서 검색할 수 있지만 데이터베이스의 이름은 다음 형식으로 연결 문자열에 추가되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-244">The Azure Cosmos DB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="16b84-245">Verify 명령을 사용하여 연결 문자열 필드에 지정된 Azure Cosmos DB 인스턴스를 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-245">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="16b84-246">단일 Azure Cosmos DB 컬렉션에서 가져오려면 데이터를 가져올 컬렉션의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-246">To import from a single Azure Cosmos DB collection, enter the name of the collection from which data will be imported.</span></span> <span data-ttu-id="16b84-247">여러 Azure Cosmos DB 컬렉션에서 가져오려면 하나 이상의 컬렉션 이름과 일치하는 정규식을 제공합니다(예: collection01 | collection02 | collection03).</span><span class="sxs-lookup"><span data-stu-id="16b84-247">To import from multiple Azure Cosmos DB collections, provide a regular expression to match one or more collection names (e.g. collection01 | collection02 | collection03).</span></span> <span data-ttu-id="16b84-248">필요에 따라 쿼리를 지정하거나 쿼리에 대한 파일을 제공하여 가져올 데이터를 필터링하고 형식을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-248">You may optionally specify, or provide a file for, a query to both filter and shape the data to be imported.</span></span>

> [!NOTE]
> <span data-ttu-id="16b84-249">컬렉션 필드 이름이 정규식 문자를 포함하므로 이름에 정규식 문자를 포함한 단일 컬렉션에서 가져오는 경우 해당 문자는 이스케이프되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-249">Since the collection field accepts regular expressions, if you are importing from a single collection whose name contains regular expression characters, then those characters must be escaped accordingly.</span></span>
> 
> 

<span data-ttu-id="16b84-250">Azure Cosmos DB 원본 가져오기 옵션에는 다음과 같은 고급 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-250">The Azure Cosmos DB source importer option has the following advanced options:</span></span>

1. <span data-ttu-id="16b84-251">내부 필드 포함: 내보내기에 Azure Cosmos DB 문서 시스템 속성(예: _rid, _ts)을 포함할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-251">Include Internal Fields: Specifies whether or not to include Azure Cosmos DB document system properties in the export (e.g. _rid, _ts).</span></span>
2. <span data-ttu-id="16b84-252">실패 시 다시 시도 횟수: 일시적 오류(예: 네트워크 연결 중단)의 경우 Azure Cosmos DB에 대한 연결을 다시 시도할 횟수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-252">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
3. <span data-ttu-id="16b84-253">다시 시도 간격: 일시적 오류(예: 네트워크 연결 중단)의 경우 Azure Cosmos DB에 대한 연결을 다시 시도하는 간격을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-253">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
4. <span data-ttu-id="16b84-254">연결 모드: Azure Cosmos DB에 사용할 연결 모드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-254">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="16b84-255">사용 가능한 선택 사항은 DirectTcp, DirectHttps 및 게이트웨이입니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-255">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="16b84-256">직접 연결 모드는 더 빠르고, 게이트웨이 모드는 포트 443만 사용하므로 더 방화벽 친화적입니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-256">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Azure Cosmos DB 원본 고급 옵션의 스크린샷](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> <span data-ttu-id="16b84-258">가져오기 도구는 기본적으로 DirectTcp 연결 모드로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-258">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="16b84-259">방화벽 문제가 발생하는 경우 포트 443만 요구하는 게이트웨이 연결 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-259">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

<span data-ttu-id="16b84-260">Azure Cosmos DB에서 가져오는 몇 가지 명령줄 샘플은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-260">Here are some command line samples to import from Azure Cosmos DB:</span></span>

    #Migrate data from one Azure Cosmos DB collection to another Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections to a single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection to a JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> <span data-ttu-id="16b84-261">또한 Azure Cosmos DB 데이터 가져오기 도구는 [Azure Cosmos DB 에뮬레이터](local-emulator.md)에서 데이터를 가져오도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-261">The Azure Cosmos DB Data Import Tool also supports import of data from the [Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="16b84-262">로컬 에뮬레이터에서 데이터를 가져올 때 끝점을 `https://localhost:<port>`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-262">When importing data from a local emulator, set the endpoint to `https://localhost:<port>`.</span></span> 
> 
> 

## <span data-ttu-id="16b84-263"><a id="HBaseSource"></a>HBase에서 가져오기</span><span class="sxs-lookup"><span data-stu-id="16b84-263"><a id="HBaseSource"></a>To import from HBase</span></span>
<span data-ttu-id="16b84-264">HBase 원본 가져오기 옵션을 사용하면 HBase 테이블에서 데이터를 가져오고 필요에 따라 데이터를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-264">The HBase source importer option allows you to import data from an HBase table and optionally filter the data.</span></span> <span data-ttu-id="16b84-265">여러 템플릿이 제공되므로 가져오기를 최대한 쉽게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-265">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![HBase 원본 옵션의 스크린샷](./media/import-data/hbasesource1.png)

![HBase 원본 옵션의 스크린샷](./media/import-data/hbasesource2.png)

<span data-ttu-id="16b84-268">HBase Stargate 연결 문자열의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-268">The format of the HBase Stargate connection string is:</span></span>

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> <span data-ttu-id="16b84-269">Verify 명령을 사용하여 연결 문자열 필드에 지정된 HBase 인스턴스를 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-269">Use the Verify command to ensure that the HBase instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="16b84-270">HBase에서 가져오는 명령줄 샘플은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-270">Here is a command line sample to import from HBase:</span></span>

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <span data-ttu-id="16b84-271"><a id="DocumentDBBulkTarget"></a>DocumentDB API로 가져오려면(대량 가져오기) 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-271"><a id="DocumentDBBulkTarget"></a>To import to the DocumentDB API (Bulk Import)</span></span>
<span data-ttu-id="16b84-272">Azure Cosmos DB 대량 가져오기를 사용하면 효율성을 위해 Azure Cosmos DB 저장 프로시저를 통해 사용 가능한 모든 원본 옵션에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-272">The Azure Cosmos DB Bulk importer allows you to import from any of the available source options, using an Azure Cosmos DB stored procedure for efficiency.</span></span> <span data-ttu-id="16b84-273">이 도구는 하나의 단일 분할된 Azure Cosmos DB 컬렉션 및 여러 단일 분할된 Azure Cosmos DB 컬렉션 간에 데이터를 분할하는 분할된 데이터베이스 가져오기도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-273">The tool supports import to one single-partitioned Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partitioned Azure Cosmos DB collections.</span></span> <span data-ttu-id="16b84-274">데이터를 분할하는 방법에 대한 자세한 내용은 [Azure Cosmos DB에서 분할 및 크기 조정](partition-data.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16b84-274">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span> <span data-ttu-id="16b84-275">이 도구는 대상 컬렉션에서 저장 프로시저를 만들고 실행한 다음 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-275">The tool will create, execute, and then delete the stored procedure from the target collection(s).</span></span>  

![Azure Cosmos DB 대량 옵션의 스크린샷](./media/import-data/documentdbbulk.png)

<span data-ttu-id="16b84-277">Azure Cosmos DB 연결 문자열의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-277">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="16b84-278">[Azure Cosmos DB 계정을 관리하는 방법](manage-account.md)에 설명된 대로 Azure Cosmos DB 계정 연결 문자열은 Azure Portal의 키 블레이드에서 검색할 수 있지만 데이터베이스의 이름은 다음 형식으로 연결 문자열에 추가되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-278">The Azure Cosmos DB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="16b84-279">Verify 명령을 사용하여 연결 문자열 필드에 지정된 Azure Cosmos DB 인스턴스를 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-279">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="16b84-280">단일 컬렉션으로 가져오려면, 데이터를 가져올 컬렉션의 이름을 입력하고 추가 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-280">To import to a single collection, enter the name of the collection to which data will be imported and click the Add button.</span></span> <span data-ttu-id="16b84-281">여러 컬렉션을 가져오려면 개별적으로 각 컬렉션 이름을 입력하거나 여러 컬렉션을 지정하려면 다음 구문을 사용합니다. *collection_prefix*[start index - end index].</span><span class="sxs-lookup"><span data-stu-id="16b84-281">To import to multiple collections, either enter each collection name individually or use the following syntax to specify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="16b84-282">앞서 언급한 구문을 통해 여러 컬렉션을 지정할 때 다음 사항에 유의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-282">When specifying multiple collections via the aforementioned syntax, keep the following in mind:</span></span>

1. <span data-ttu-id="16b84-283">정수 범위 이름 패턴만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-283">Only integer range name patterns are supported.</span></span> <span data-ttu-id="16b84-284">예를 들어, 컬렉션 [0-3]을 지정하면 collection0, collection1, collection2, collection3 컬렉션을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-284">For example, specifying collection[0-3] will produce the following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="16b84-285">축약된 구문을 사용할 수 있습니다. [3] 컬렉션은 1단계에서 설명한 동일한 집합을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-285">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="16b84-286">둘 이상의 대체를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-286">More than one substitution can be provided.</span></span> <span data-ttu-id="16b84-287">예를 들어, 컬렉션 [0-1] [0-9]는 0이 이름 앞에 오는 20개의 컬렉션을 생성합니다(collection01,... 02... 03).</span><span class="sxs-lookup"><span data-stu-id="16b84-287">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="16b84-288">컬렉션 이름이 지정되면 원하는 컬렉션 처리량을 선택합니다(400RU~10,000RU).</span><span class="sxs-lookup"><span data-stu-id="16b84-288">Once the collection name(s) have been specified, choose the desired throughput of the collection(s) (400 RUs to 10,000 RUs).</span></span> <span data-ttu-id="16b84-289">가져오기 성능을 최적화하려면 더 높은 처리량을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-289">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="16b84-290">성능 수준에 대한 자세한 내용은 [Azure Cosmos DB의 성능 수준](performance-levels.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16b84-290">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span>

> [!NOTE]
> <span data-ttu-id="16b84-291">성능 처리량 설정은 컬렉션 생성에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-291">The performance throughput setting only applies to collection creation.</span></span> <span data-ttu-id="16b84-292">지정된 컬렉션이 이미 있는 경우 해당 처리량은 수정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-292">If the specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="16b84-293">여러 컬렉션을 가져올 때 가져오기 도구는 해시 기반 분할을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-293">When importing to multiple collections, the import tool supports hash based sharding.</span></span> <span data-ttu-id="16b84-294">이 시나리오에서는 파티션 키로 사용하려는 문서 속성을 지정합니다(파티션 키에 정보를 입력하지 않으면 문서는 대상 컬렉션에서 임의로 분할됨).</span><span class="sxs-lookup"><span data-stu-id="16b84-294">In this scenario, specify the document property you wish to use as the Partition Key (if Partition Key is left blank, documents will be sharded randomly across the target collections).</span></span>

<span data-ttu-id="16b84-295">필요에 따라 가져오는 동안 Azure Cosmos DB 문서 ID 속성으로 사용할 가져오기 원본의 필드를 지정할 수 있습니다(문서에 이 속성이 없는 경우 가져오기 도구에서 GUID를 ID 속성 값으로 생성함).</span><span class="sxs-lookup"><span data-stu-id="16b84-295">You may optionally specify which field in the import source should be used as the Azure Cosmos DB document id property during the import (note that if documents do not contain this property, then the import tool will generate a GUID as the id property value).</span></span>

<span data-ttu-id="16b84-296">가져오는 동안 사용할 수 있는 다양한 고급 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-296">There are a number of advanced options available during import.</span></span> <span data-ttu-id="16b84-297">먼저, 도구에 기본 대량 가져오기 저장 프로시저(BulkInsert.js)가 포함되어 있지만 사용자 고유의 가져오기 저장 프로시저를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-297">First, while the tool includes a default bulk import stored procedure (BulkInsert.js), you may choose to specify your own import stored procedure:</span></span>

 ![Azure Cosmos DB 대량 삽입 저장 프로시저 옵션의 스크린샷](./media/import-data/bulkinsertsp.png)

<span data-ttu-id="16b84-299">또한 SQL Server 또는 MongoDB 등에서 날짜 형식을 가져오는 경우 다음 3개의 가져오기 옵션 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-299">Additionally, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Azure Cosmos DB 날짜/시간 가져오기 옵션의 스크린샷](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="16b84-301">문자열: 문자열 값으로 유지</span><span class="sxs-lookup"><span data-stu-id="16b84-301">String: Persist as a string value</span></span>
* <span data-ttu-id="16b84-302">Epoch: Epoch 숫자 값으로 유지</span><span class="sxs-lookup"><span data-stu-id="16b84-302">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="16b84-303">둘 다: 문자열 및 Epoch 숫자 값으로 유지.</span><span class="sxs-lookup"><span data-stu-id="16b84-303">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="16b84-304">이 옵션은 하위 문서를 만듭니다(예: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }).</span><span class="sxs-lookup"><span data-stu-id="16b84-304">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="16b84-305">Azure Cosmos DB 대량 가져오기에는 다음과 같은 추가 고급 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-305">The Azure Cosmos DB Bulk importer has the following additional advanced options:</span></span>

1. <span data-ttu-id="16b84-306">배치 크기: 기본적으로 도구의 배치 크기는 50으로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-306">Batch Size: The tool defaults to a batch size of 50.</span></span>  <span data-ttu-id="16b84-307">가져올 문서가 크면 배치 크기를 줄이는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-307">If the documents to be imported are large, consider lowering the batch size.</span></span> <span data-ttu-id="16b84-308">반대로, 가져올 문서가 작으면 배치 크기를 늘리는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-308">Conversely, if the documents to be imported are small, consider raising the batch size.</span></span>
2. <span data-ttu-id="16b84-309">최대 스크립트 크기(바이트): 기본적으로 도구의 최대 스크립트 크기는 512KB로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-309">Max Script Size (bytes): The tool defaults to a max script size of 512KB</span></span>
3. <span data-ttu-id="16b84-310">자동 ID 생성 사용 안 함: 가져올 모든 문서에 ID 필드가 포함되어 있는 경우 이 옵션을 선택하면 성능을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-310">Disable Automatic Id Generation: If every document to be imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="16b84-311">고유 ID 필드가 없는 문서는 가져오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-311">Documents missing a unique id field will not be imported.</span></span>
4. <span data-ttu-id="16b84-312">기존 문서 업데이트: 이 도구는 기본적으로 기존 문서를 충돌하는 ID로 대체하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-312">Update Existing Documents: The tool defaults to not replacing existing documents with id conflicts.</span></span> <span data-ttu-id="16b84-313">이 옵션을 선택하면 기존 문서를 일치하는 ID로 덮어쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-313">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="16b84-314">이 기능은 기존 문서를 업데이트하는 예약된 데이터 마이그레이션에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-314">This feature is useful for scheduled data migrations that update existing documents.</span></span>
5. <span data-ttu-id="16b84-315">실패 시 다시 시도 횟수: 일시적 오류(예: 네트워크 연결 중단)의 경우 Azure Cosmos DB에 대한 연결을 다시 시도할 횟수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-315">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="16b84-316">다시 시도 간격: 일시적 오류(예: 네트워크 연결 중단)의 경우 Azure Cosmos DB에 대한 연결을 다시 시도하는 간격을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-316">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
7. <span data-ttu-id="16b84-317">연결 모드: Azure Cosmos DB에 사용할 연결 모드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-317">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="16b84-318">사용 가능한 선택 사항은 DirectTcp, DirectHttps 및 게이트웨이입니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-318">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="16b84-319">직접 연결 모드는 더 빠르고, 게이트웨이 모드는 포트 443만 사용하므로 더 방화벽 친화적입니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-319">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Azure Cosmos DB 대량 가져오기 고급 옵션의 스크린샷](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> <span data-ttu-id="16b84-321">가져오기 도구는 기본적으로 DirectTcp 연결 모드로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-321">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="16b84-322">방화벽 문제가 발생하는 경우 포트 443만 요구하는 게이트웨이 연결 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-322">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="16b84-323"><a id="DocumentDBSeqTarget"></a>DocumentDB API로 가져오려면(순차 레코드 가져오기) 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-323"><a id="DocumentDBSeqTarget"></a>To import to the DocumentDB API (Sequential Record Import)</span></span>
<span data-ttu-id="16b84-324">Azure Cosmos DB 순차 레코드 가져오기를 사용하면 레코드 단위로 사용 가능한 모든 원본 옵션에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-324">The Azure Cosmos DB sequential record importer allows you to import from any of the available source options on a record by record basis.</span></span> <span data-ttu-id="16b84-325">저장 프로시저의 할당량에 도달한 기존 컬렉션으로 가져오는 경우 이 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-325">You might choose this option if you’re importing to an existing collection that has reached its quota of stored procedures.</span></span> <span data-ttu-id="16b84-326">이 도구는 단일(단일 파티션 및 다중 파티션 모두) Azure Cosmos DB 컬렉션 및 여러 단일 파티션 및/또는 다중 파티션 Azure Cosmos DB 컬렉션 간에 데이터를 분할하는 분할된 데이터베이스 가져오기도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-326">The tool supports import to a single (both single-partition and multi-partition) Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partition and/or multi-partition Azure Cosmos DB collections.</span></span> <span data-ttu-id="16b84-327">데이터를 분할하는 방법에 대한 자세한 내용은 [Azure Cosmos DB에서 분할 및 크기 조정](partition-data.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16b84-327">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span>

![Azure Cosmos DB 순차 레코드 가져오기 옵션의 스크린샷](./media/import-data/documentdbsequential.png)

<span data-ttu-id="16b84-329">Azure Cosmos DB 연결 문자열의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-329">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="16b84-330">[Azure Cosmos DB 계정을 관리하는 방법](manage-account.md)에 설명된 대로 Azure Cosmos DB 계정 연결 문자열은 Azure Portal의 키 블레이드에서 검색할 수 있지만 데이터베이스의 이름은 다음 형식으로 연결 문자열에 추가되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-330">The Azure Cosmos DB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> <span data-ttu-id="16b84-331">Verify 명령을 사용하여 연결 문자열 필드에 지정된 Azure Cosmos DB 인스턴스를 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-331">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="16b84-332">단일 컬렉션으로 가져오려면, 데이터를 가져올 컬렉션의 이름을 입력하고 추가 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-332">To import to a single collection, enter the name of the collection to which data will be imported and click the Add button.</span></span> <span data-ttu-id="16b84-333">여러 컬렉션을 가져오려면 개별적으로 각 컬렉션 이름을 입력하거나 여러 컬렉션을 지정하려면 다음 구문을 사용합니다. *collection_prefix*[start index - end index].</span><span class="sxs-lookup"><span data-stu-id="16b84-333">To import to multiple collections, either enter each collection name individually or use the following syntax to specify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="16b84-334">앞서 언급한 구문을 통해 여러 컬렉션을 지정할 때 다음 사항에 유의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-334">When specifying multiple collections via the aforementioned syntax, keep the following in mind:</span></span>

1. <span data-ttu-id="16b84-335">정수 범위 이름 패턴만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-335">Only integer range name patterns are supported.</span></span> <span data-ttu-id="16b84-336">예를 들어, 컬렉션 [0-3]을 지정하면 collection0, collection1, collection2, collection3 컬렉션을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-336">For example, specifying collection[0-3] will produce the following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="16b84-337">축약된 구문을 사용할 수 있습니다. [3] 컬렉션은 1단계에서 설명한 동일한 집합을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-337">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="16b84-338">둘 이상의 대체를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-338">More than one substitution can be provided.</span></span> <span data-ttu-id="16b84-339">예를 들어, 컬렉션 [0-1] [0-9]는 0이 이름 앞에 오는 20개의 컬렉션을 생성합니다(collection01,... 02... 03).</span><span class="sxs-lookup"><span data-stu-id="16b84-339">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="16b84-340">컬렉션 이름이 지정되면 원하는 컬렉션 처리량을 선택합니다(400RU~250,000RU).</span><span class="sxs-lookup"><span data-stu-id="16b84-340">Once the collection name(s) have been specified, choose the desired throughput of the collection(s) (400 RUs to 250,000 RUs).</span></span> <span data-ttu-id="16b84-341">가져오기 성능을 최적화하려면 더 높은 처리량을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-341">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="16b84-342">성능 수준에 대한 자세한 내용은 [Azure Cosmos DB의 성능 수준](performance-levels.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16b84-342">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span> <span data-ttu-id="16b84-343">처리량 >10,000RU로 컬렉션에 가져오기는 파티션 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-343">Any import to collections with throughput >10,000 RUs will require a partition key.</span></span> <span data-ttu-id="16b84-344">250,000RU 이상을 보유하도록 선택한 경우에는 계정을 늘리도록 포털에 요청을 접수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-344">If you choose to have more than 250,000 RUs, you will need to file a request in the portal to have your account increased.</span></span>

> [!NOTE]
> <span data-ttu-id="16b84-345">처리량 설정은 컬렉션 생성에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-345">The throughput setting only applies to collection creation.</span></span> <span data-ttu-id="16b84-346">지정된 컬렉션이 이미 있는 경우 해당 처리량은 수정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-346">If the specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="16b84-347">여러 컬렉션을 가져올 때 가져오기 도구는 해시 기반 분할을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-347">When importing to multiple collections, the import tool supports hash based sharding.</span></span> <span data-ttu-id="16b84-348">이 시나리오에서는 파티션 키로 사용하려는 문서 속성을 지정합니다(파티션 키에 정보를 입력하지 않으면 문서는 대상 컬렉션에서 임의로 분할됨).</span><span class="sxs-lookup"><span data-stu-id="16b84-348">In this scenario, specify the document property you wish to use as the Partition Key (if Partition Key is left blank, documents will be sharded randomly across the target collections).</span></span>

<span data-ttu-id="16b84-349">필요에 따라 가져오는 동안 Azure Cosmos DB 문서 ID 속성으로 사용할 가져오기 원본의 필드를 지정할 수 있습니다(문서에 이 속성이 없는 경우 가져오기 도구에서 GUID를 ID 속성 값으로 생성함).</span><span class="sxs-lookup"><span data-stu-id="16b84-349">You may optionally specify which field in the import source should be used as the Azure Cosmos DB document id property during the import (note that if documents do not contain this property, then the import tool will generate a GUID as the id property value).</span></span>

<span data-ttu-id="16b84-350">가져오는 동안 사용할 수 있는 다양한 고급 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-350">There are a number of advanced options available during import.</span></span> <span data-ttu-id="16b84-351">먼저, SQL Server 또는 MongoDB 등에서 날짜 형식을 가져오는 경우 다음 3개의 가져오기 옵션 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-351">First, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Azure Cosmos DB 날짜/시간 가져오기 옵션의 스크린샷](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="16b84-353">문자열: 문자열 값으로 유지</span><span class="sxs-lookup"><span data-stu-id="16b84-353">String: Persist as a string value</span></span>
* <span data-ttu-id="16b84-354">Epoch: Epoch 숫자 값으로 유지</span><span class="sxs-lookup"><span data-stu-id="16b84-354">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="16b84-355">둘 다: 문자열 및 Epoch 숫자 값으로 유지.</span><span class="sxs-lookup"><span data-stu-id="16b84-355">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="16b84-356">이 옵션은 하위 문서를 만듭니다(예: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }).</span><span class="sxs-lookup"><span data-stu-id="16b84-356">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="16b84-357">Azure Cosmos DB - 순차 레코드 가져오기에는 다음과 같은 추가 고급 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-357">The Azure Cosmos DB - Sequential record importer has the following additional advanced options:</span></span>

1. <span data-ttu-id="16b84-358">병렬 요청 수: 기본적으로 도구의 병렬 요청 수는 2개로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-358">Number of Parallel Requests: The tool defaults to 2 parallel requests.</span></span> <span data-ttu-id="16b84-359">가져올 문서가 작으면 병렬 요청 수를 늘리는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-359">If the documents to be imported are small, consider raising the number of parallel requests.</span></span> <span data-ttu-id="16b84-360">이 개수를 너무 많이 늘리면 가져오기 시 제한이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-360">Note that if this number is raised too much, the import may experience throttling.</span></span>
2. <span data-ttu-id="16b84-361">자동 ID 생성 사용 안 함: 가져올 모든 문서에 ID 필드가 포함되어 있는 경우 이 옵션을 선택하면 성능을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-361">Disable Automatic Id Generation: If every document to be imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="16b84-362">고유 ID 필드가 없는 문서는 가져오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-362">Documents missing a unique id field will not be imported.</span></span>
3. <span data-ttu-id="16b84-363">기존 문서 업데이트: 이 도구는 기본적으로 기존 문서를 충돌하는 ID로 대체하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-363">Update Existing Documents: The tool defaults to not replacing existing documents with id conflicts.</span></span> <span data-ttu-id="16b84-364">이 옵션을 선택하면 기존 문서를 일치하는 ID로 덮어쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-364">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="16b84-365">이 기능은 기존 문서를 업데이트하는 예약된 데이터 마이그레이션에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-365">This feature is useful for scheduled data migrations that update existing documents.</span></span>
4. <span data-ttu-id="16b84-366">실패 시 다시 시도 횟수: 일시적 오류(예: 네트워크 연결 중단)의 경우 Azure Cosmos DB에 대한 연결을 다시 시도할 횟수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-366">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
5. <span data-ttu-id="16b84-367">다시 시도 간격: 일시적 오류(예: 네트워크 연결 중단)의 경우 Azure Cosmos DB에 대한 연결을 다시 시도하는 간격을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-367">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="16b84-368">연결 모드: Azure Cosmos DB에 사용할 연결 모드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-368">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="16b84-369">사용 가능한 선택 사항은 DirectTcp, DirectHttps 및 게이트웨이입니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-369">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="16b84-370">직접 연결 모드는 더 빠르고, 게이트웨이 모드는 포트 443만 사용하므로 더 방화벽 친화적입니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-370">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Azure Cosmos DB 순차 레코드 가져오기 고급 옵션의 스크린샷](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> <span data-ttu-id="16b84-372">가져오기 도구는 기본적으로 DirectTcp 연결 모드로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-372">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="16b84-373">방화벽 문제가 발생하는 경우 포트 443만 요구하는 게이트웨이 연결 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-373">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="16b84-374"><a id="IndexingPolicy"></a>Azure Cosmos DB 컬렉션을 만들 때 인덱싱 정책 지정</span><span class="sxs-lookup"><span data-stu-id="16b84-374"><a id="IndexingPolicy"></a>Specify an indexing policy when creating Azure Cosmos DB collections</span></span>
<span data-ttu-id="16b84-375">가져오는 동안 컬렉션을 만들 수 있도록 마이그레이션 도구를 허용하는 경우 컬렉션의 인덱싱 정책을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-375">When you allow the migration tool to create collections during import, you can specify the indexing policy of the collections.</span></span> <span data-ttu-id="16b84-376">Azure Cosmos DB 대량 가져오기의 고급 옵션 섹션 및 Azure Cosmos DB 순차 레코드 옵션에서 인덱싱 정책 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-376">In the advanced options section of the Azure Cosmos DB Bulk import and Azure Cosmos DB Sequential record options, navigate to the Indexing Policy section.</span></span>

![Azure Cosmos DB 인덱싱 정책 고급 옵션의 스크린샷](./media/import-data/indexingpolicy1.png)

<span data-ttu-id="16b84-378">인덱싱 정책 고급 옵션을 사용하여 인덱싱 정책 파일을 선택하고 인덱싱 정책을 수동으로 입력하거나 일련의 기본 템플릿에서 선택할 수 있습니다(인덱싱 정책 텍스트 상자를 마우스 오른쪽 단추로 클릭).</span><span class="sxs-lookup"><span data-stu-id="16b84-378">Using the Indexing Policy advanced option, you can select an indexing policy file, manually enter an indexing policy, or select from a set of default templates (by right clicking in the indexing policy textbox).</span></span>

<span data-ttu-id="16b84-379">도구가 제공하는 정책 템플릿은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-379">The policy templates the tool provides are:</span></span>

* <span data-ttu-id="16b84-380">기본값</span><span class="sxs-lookup"><span data-stu-id="16b84-380">Default.</span></span> <span data-ttu-id="16b84-381">이 정책은 문자열에 대해 같음 쿼리를 수행하고 숫자에 대해 ORDER BY, 범위 및 같음 쿼리를 사용할 때 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-381">This policy is best when you’re performing equality queries against strings and using ORDER BY, range, and equality queries for numbers.</span></span> <span data-ttu-id="16b84-382">이 정책에는 범위보다 더 낮은 인덱스 저장소 오버헤드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-382">This policy has a lower index storage overhead than Range.</span></span>
* <span data-ttu-id="16b84-383">범위입니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-383">Range.</span></span> <span data-ttu-id="16b84-384">이 정책은 숫자와 문자열 모두에 ORDER BY, 범위 및 같음 쿼리를 사용할 때 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-384">This policy is best you’re using ORDER BY, range and equality queries on both numbers and strings.</span></span> <span data-ttu-id="16b84-385">이 정책에는 기본값 또는 해시보다 더 높은 인덱스 저장소 오버헤드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-385">This policy has a higher index storage overhead than Default or Hash.</span></span>

![Azure Cosmos DB 인덱싱 정책 고급 옵션의 스크린샷](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> <span data-ttu-id="16b84-387">인덱싱 정책을 지정하지 않으면 기본 정책이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-387">If you do not specify an indexing policy, then the default policy will be applied.</span></span> <span data-ttu-id="16b84-388">인덱싱 정책에 대한 자세한 내용은 [Azure Cosmos DB 인덱싱 정책](indexing-policies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16b84-388">For more information about indexing policies, see [Azure Cosmos DB indexing policies](indexing-policies.md).</span></span>
> 
> 

## <a name="export-to-json-file"></a><span data-ttu-id="16b84-389">JSON 파일로 내보내기</span><span class="sxs-lookup"><span data-stu-id="16b84-389">Export to JSON file</span></span>
<span data-ttu-id="16b84-390">Azure Cosmos DB JSON 내보내기를 사용하면 사용 가능한 모든 원본 옵션을 JSON 문서 배열이 포함된 JSON 파일로 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-390">The Azure Cosmos DB JSON exporter allows you to export any of the available source options to a JSON file that contains an array of JSON documents.</span></span> <span data-ttu-id="16b84-391">도구에서 자동으로 내보내기를 처리하거나, 결과 마이그레이션 명령을 보고 직접 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-391">The tool will handle the export for you, or you can choose to view the resulting migration command and run the command yourself.</span></span> <span data-ttu-id="16b84-392">결과 JSON 파일은 로컬로 또는 Azure Blob 저장소에 저장될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-392">The resulting JSON file may be stored locally or in Azure Blob storage.</span></span>

![Azure Cosmos DB JSON 로컬 파일 내보내기 옵션의 스크린샷](./media/import-data/jsontarget.png)

![Azure Cosmos DB JSON Azure Blob Storage 내보내기 옵션의 스크린샷](./media/import-data/jsontarget2.png)

<span data-ttu-id="16b84-395">필요에 따라 결과 JSON을 꾸밀 수 있으며, 이 경우 콘텐츠의 가독성은 향상되지만 결과 문서의 크기가 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-395">You may optionally choose to prettify the resulting JSON, which will increase the size of the resulting document while making the contents more human readable.</span></span>

    Standard JSON export
    [{"id":"Sample","Title":"About Paris","Language":{"Name":"English"},"Author":{"Name":"Don","Location":{"City":"Paris","Country":"France"}},"Content":"Don's document in Azure Cosmos DB is a valid JSON document as defined by the JSON spec.","PageViews":10000,"Topics":[{"Title":"History of Paris"},{"Title":"Places to see in Paris"}]}]

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
    "Content": "Don's document in Azure Cosmos DB is a valid JSON document as defined by the JSON spec.",
    "PageViews": 10000,
    "Topics": [
      {
        "Title": "History of Paris"
      },
      {
        "Title": "Places to see in Paris"
      }
    ]
    }]

## <a name="advanced-configuration"></a><span data-ttu-id="16b84-396">고급 구성</span><span class="sxs-lookup"><span data-stu-id="16b84-396">Advanced configuration</span></span>
<span data-ttu-id="16b84-397">고급 구성 화면에서 원하는 모든 오류가 기록된 로그 파일의 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-397">In the Advanced configuration screen, specify the location of the log file to which you would like any errors written.</span></span> <span data-ttu-id="16b84-398">이 페이지에는 다음 규칙이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-398">The following rules apply to this page:</span></span>

1. <span data-ttu-id="16b84-399">파일 이름을 제공하지 않으면, 모든 오류는 결과 페이지에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-399">If a file name is not provided, then all errors will be returned on the Results page.</span></span>
2. <span data-ttu-id="16b84-400">파일 이름에서 디렉터리가 없는 경우 파일은 현재 환경 디렉터리에 만들어지거나 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-400">If a file name is provided without a directory, then the file will be created (or overwritten) in the current environment directory.</span></span>
3. <span data-ttu-id="16b84-401">기존 파일을 선택하는 경우 파일을 덮어쓰며 추가 옵션은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-401">If you select an existing file, then the file will be overwritten, there is no append option.</span></span>

<span data-ttu-id="16b84-402">그런 다음 모든 메시지를 기록할지, 중요한 메시지를 기록할지 또는 오류 없음 메시지를 기록할지 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-402">Then, choose whether to log all, critical, or no error messages.</span></span> <span data-ttu-id="16b84-403">마지막으로, 화면 전송 메시지를 해당 진행률과 함께 업데이트할 빈도를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-403">Finally, decide how frequently the on screen transfer message will be updated with its progress.</span></span>

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a><span data-ttu-id="16b84-404">가져오기 설정 확인 및 명령줄 보기</span><span class="sxs-lookup"><span data-stu-id="16b84-404">Confirm import settings and view command line</span></span>
1. <span data-ttu-id="16b84-405">원본 정보, 대상 정보 및 고급 구성을 지정한 후, 마이그레이션 요약을 검토하고, 필요에 따라 결과 마이그레이션 명령을 확인/복사합니다(명령 복사는 가져오기 작업을 자동화하는 데 유용함).</span><span class="sxs-lookup"><span data-stu-id="16b84-405">After specifying source information, target information, and advanced configuration, review the migration summary and, optionally, view/copy the resulting migration command (copying the command is useful to automate import operations):</span></span>
   
    ![요약 화면의 스크린샷](./media/import-data/summary.png)
   
    ![요약 화면의 스크린샷](./media/import-data/summarycommand.png)
2. <span data-ttu-id="16b84-408">원본 및 대상 옵션이 적절하면 **가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-408">Once you’re satisfied with your source and target options, click **Import**.</span></span> <span data-ttu-id="16b84-409">가져오기가 처리되는 동안 경과 시간, 전송 횟수 및 실패 정보가 업데이트됩니다(고급 구성에서 파일 이름을 지정하지 않은 경우).</span><span class="sxs-lookup"><span data-stu-id="16b84-409">The elapsed time, transferred count, and failure information (if you didn't provide a file name in the Advanced configuration) will update as the import is in process.</span></span> <span data-ttu-id="16b84-410">완료되면 결과를 내보낼 수 있습니다(예: 가져오기 오류를 처리하기 위해).</span><span class="sxs-lookup"><span data-stu-id="16b84-410">Once complete, you can export the results (e.g. to deal with any import failures).</span></span>
   
    ![Azure Cosmos DB JSON 내보내기 옵션의 스크린샷](./media/import-data/viewresults.png)
3. <span data-ttu-id="16b84-412">기존 설정(예: 연결 문자열 정보, 원본 및 대상 선택 등)을 유지하거나 모든 값을 다시 설정하여 새 가져오기를 시작할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-412">You may also start a new import, either keeping the existing settings (e.g. connection string information, source and target choice, etc.) or resetting all values.</span></span>
   
    ![Azure Cosmos DB JSON 내보내기 옵션의 스크린샷](./media/import-data/newimport.png)

## <a name="next-steps"></a><span data-ttu-id="16b84-414">다음 단계</span><span class="sxs-lookup"><span data-stu-id="16b84-414">Next steps</span></span>

<span data-ttu-id="16b84-415">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-415">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="16b84-416">데이터 마이그레이션 도구 설치</span><span class="sxs-lookup"><span data-stu-id="16b84-416">Installed the Data Migration tool</span></span>
> * <span data-ttu-id="16b84-417">여러 데이터 원본에서 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="16b84-417">Imported data from different data sources</span></span>
> * <span data-ttu-id="16b84-418">Azure Cosmos DB에서 JSON으로 내보내기</span><span class="sxs-lookup"><span data-stu-id="16b84-418">Exported from Azure Cosmos DB to JSON</span></span>

<span data-ttu-id="16b84-419">이제 다음 자습서로 진행하여 Azure Cosmos DB를 사용하여 데이터를 쿼리하는 방법을 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b84-419">You can now proceed to the next tutorial and learn how to query data using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="16b84-420">데이터는 어떻게 쿼리하나요?</span><span class="sxs-lookup"><span data-stu-id="16b84-420">How to query data?</span></span>](../cosmos-db/tutorial-query-documentdb.md)
