---
title: "MongoDB용 Azure Cosmos DB API와 함께 mongoimport 및 mongorestore 사용 | Microsoft Docs"
description: "mongoimport 및 mongorestore를 사용하여 데이터를 MongoDB API 계정으로 가져오는 방법을 알아봅니다."
keywords: mongoimport, mongorestore
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 1555f13c3ea88b61be0ea240b51218b83f6f9724
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-import-mongodb-data"></a><span data-ttu-id="0fa2e-104">Azure Cosmos DB: MongoDB 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="0fa2e-104">Azure Cosmos DB: Import MongoDB data</span></span> 

<span data-ttu-id="0fa2e-105">MongoDB API와 함께 사용하기 위해 MongoDB에서 Azure Cosmos DB 계정으로 데이터를 마이그레이션하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-105">To migrate data from MongoDB to an Azure Cosmos DB account for use with the API for MongoDB, you must:</span></span>

* <span data-ttu-id="0fa2e-106">[MongoDB Download Center](https://www.mongodb.com/download-center)에서 *mongoimport.exe* 또는 *mongorestore.exe*를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-106">Download either *mongoimport.exe* or *mongorestore.exe* from the [MongoDB Download Center](https://www.mongodb.com/download-center).</span></span>
* <span data-ttu-id="0fa2e-107">[MongoDB API 연결 문자열](connect-mongodb-account.md)을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-107">Get your [API for MongoDB connection string](connect-mongodb-account.md).</span></span>

<span data-ttu-id="0fa2e-108">MongoDB에서 데이터를 가져와 Azure Cosmos DB API에 사용하려는 경우 [데이터 마이그레이션 도구](import-data.md)를 사용해서 데이터를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-108">If you are importing data from MongoDB and plan to use it with the Azure Cosmos DB, you should use the [Data Migration tool](import-data.md) to import data.</span></span>

<span data-ttu-id="0fa2e-109">이 자습서에서 다루는 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-109">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0fa2e-110">연결 문자열 검색</span><span class="sxs-lookup"><span data-stu-id="0fa2e-110">Retrieving your connection string</span></span>
> * <span data-ttu-id="0fa2e-111">mongoimport를 사용하여 MongoDB 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="0fa2e-111">Importing MongoDB data by using mongoimport</span></span>
> * <span data-ttu-id="0fa2e-112">mongorestore를 사용하여 MongoDB 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="0fa2e-112">Importing MongoDB data by using mongorestore</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0fa2e-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0fa2e-113">Prerequisites</span></span>

* <span data-ttu-id="0fa2e-114">처리량 늘리기: 데이터 마이그레이션 기간은 컬렉션에 대해 설정한 처리량에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-114">Increase throughput: The duration of your data migration depends on the amount of throughput you set up for your collections.</span></span> <span data-ttu-id="0fa2e-115">대량 데이터 마이그레이션의 경우 처리량을 늘려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-115">Be sure to increase the throughput for larger data migrations.</span></span> <span data-ttu-id="0fa2e-116">마이그레이션을 완료한 후에는 비용을 절약하기 위해 처리량을 줄이세요.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-116">After you've completed the migration, decrease the throughput to save costs.</span></span> <span data-ttu-id="0fa2e-117">[Azure Portal](https://portal.azure.com)에서 처리량을 늘리는 방법에 대한 자세한 내용은 [Azure Cosmos DB의 성능 수준 및 가격 책정 계층](performance-levels.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-117">For more information about increasing throughput in the [Azure portal](https://portal.azure.com), see [Performance levels and pricing tiers in Azure Cosmos DB](performance-levels.md).</span></span>

* <span data-ttu-id="0fa2e-118">SSL 사용: Azure Cosmos DB에는 엄격한 보안 요구 사항과 표준이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-118">Enable SSL: Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="0fa2e-119">계정과 상호 작용하는 경우 SSL을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-119">Be sure to enable SSL when you interact with your account.</span></span> <span data-ttu-id="0fa2e-120">나머지 문서의 절차에서는 mongoimport 및 mongorestore에 대해 SSL을 사용하도록 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-120">The procedures in the rest of the article include how to enable SSL for mongoimport and mongorestore.</span></span>

## <a name="find-your-connection-string-information-host-port-username-and-password"></a><span data-ttu-id="0fa2e-121">연결 문자열 정보(호스트, 포트, 사용자 이름 및 암호) 찾기</span><span class="sxs-lookup"><span data-stu-id="0fa2e-121">Find your connection string information (host, port, username, and password)</span></span>

1. <span data-ttu-id="0fa2e-122">[Azure Portal](https://portal.azure.com)의 왼쪽 창에서 **Azure Cosmos DB** 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-122">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Cosmos DB** entry.</span></span>
2. <span data-ttu-id="0fa2e-123">**구독** 창에서 계정 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-123">In the **Subscriptions** pane, select your account name.</span></span>
3. <span data-ttu-id="0fa2e-124">**연결 문자열** 블레이드에서 **연결 문자열**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-124">In the **Connection String** blade, click **Connection String**.</span></span>  
<span data-ttu-id="0fa2e-125">오른쪽 창에는 계정에 성공적으로 연결하는 데 필요한 모든 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-125">The right pane contains all the information that you need to successfully connect to your account.</span></span>

    ![연결 문자열 블레이드](./media/mongodb-migrate/ConnectionStringBlade.png)

## <a name="import-data-to-the-api-for-mongodb-by-using-mongoimport"></a><span data-ttu-id="0fa2e-127">mongoimport를 사용하여 MongoDB API로 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="0fa2e-127">Import data to the API for MongoDB by using mongoimport</span></span>

<span data-ttu-id="0fa2e-128">데이터를 Azure Cosmos DB 계정으로 가져오려면 다음 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-128">To import data to your Azure Cosmos DB account, use the following template.</span></span> <span data-ttu-id="0fa2e-129">*호스트*, *사용자 이름* 및 *암호*를 계정과 관련된 값으로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-129">Fill in *host*, *username*, and *password* with the values that are specific to your account.</span></span>  

<span data-ttu-id="0fa2e-130">템플릿:</span><span class="sxs-lookup"><span data-stu-id="0fa2e-130">Template:</span></span>

    mongoimport.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file C:\sample.json

<span data-ttu-id="0fa2e-131">예제:</span><span class="sxs-lookup"><span data-stu-id="0fa2e-131">Example:</span></span>  

    mongoimport.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file C:\Users\anhoh\Desktop\*.json

## <a name="import-data-to-the-api-for-mongodb-by-using-mongorestore"></a><span data-ttu-id="0fa2e-132">mongorestore를 사용하여 MongoDB API로 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="0fa2e-132">Import data to the API for MongoDB by using mongorestore</span></span>

<span data-ttu-id="0fa2e-133">데이터를 MongoDB API 계정으로 복원하려면 다음 템플릿을 사용하여 가져오기를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-133">To restore data to your API for MongoDB account, use the following template to execute the import.</span></span> <span data-ttu-id="0fa2e-134">*호스트*, *사용자 이름* 및 *암호*를 계정과 관련된 값으로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-134">Fill in *host*, *username*, and *password* with the values that are specific to your account.</span></span>

<span data-ttu-id="0fa2e-135">템플릿:</span><span class="sxs-lookup"><span data-stu-id="0fa2e-135">Template:</span></span>

    mongorestore.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>

<span data-ttu-id="0fa2e-136">예제:</span><span class="sxs-lookup"><span data-stu-id="0fa2e-136">Example:</span></span>

    mongorestore.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07
    
## <a name="guide-for-a-successful-migration"></a><span data-ttu-id="0fa2e-137">성공적인 마이그레이션 가이드</span><span class="sxs-lookup"><span data-stu-id="0fa2e-137">Guide for a successful migration</span></span>

1. <span data-ttu-id="0fa2e-138">컬렉션을 미리 만들어 크기 조정:</span><span class="sxs-lookup"><span data-stu-id="0fa2e-138">Pre-create and scale your collections:</span></span>
        
    * <span data-ttu-id="0fa2e-139">기본적으로 Azure Cosmos DB는 1,000RU(요청 단위)로 새 MongoDB 컬렉션을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-139">By default, Azure Cosmos DB provisions a new MongoDB collection with 1,000 request units (RUs).</span></span> <span data-ttu-id="0fa2e-140">mongoimport, mongorestore 또는 mongomirror를 사용하여 마이그레이션을 시작하기 전에 [Azure Portal](https://portal.azure.com) 또는 MongoDB 드라이버 및 도구에서 모든 컬렉션을 미리 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-140">Before you start the migration by using mongoimport, mongorestore, or mongomirror, pre-create all your collections from the [Azure portal](https://portal.azure.com) or from MongoDB drivers and tools.</span></span> <span data-ttu-id="0fa2e-141">컬렉션이 10GB보다 큰 경우 적절한 분할 키로 [분할/파티션된 컬렉션](partition-data.md)을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-141">If your collection is greater than 10 GB, make sure to create a [sharded/partitioned collection](partition-data.md) with an appropriate shard key.</span></span>

    * <span data-ttu-id="0fa2e-142">[Azure Portal](https://portal.azure.com)에서 단일 파티션 컬렉션에 대해 1,000RU 및 분할된 컬렉션에 대해 2,500RU부터 컬렉션의 처리량을 증가시킵니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-142">From the [Azure portal](https://portal.azure.com), increase your collections' throughput from 1,000 RUs for a single partition collection and 2,500 RUs for a sharded collection just for the migration.</span></span> <span data-ttu-id="0fa2e-143">처리량이 높을수록 제한을 피하고 마이그레이션 시간을 단축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-143">With the higher throughput, you can avoid throttling and migrate in less time.</span></span> <span data-ttu-id="0fa2e-144">Azure Cosmos DB에서는 시간당 청구되므로 마이그레이션 후 바로 처리량을 줄여 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-144">With hourly billing in Azure Cosmos DB, you can reduce the throughput immediately after the migration to save costs.</span></span>

2. <span data-ttu-id="0fa2e-145">단일 문서 쓰기에 대해 대략적인 RU 요금 계산:</span><span class="sxs-lookup"><span data-stu-id="0fa2e-145">Calculate the approximate RU charge for a single document write:</span></span>

    <span data-ttu-id="0fa2e-146">a.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-146">a.</span></span> <span data-ttu-id="0fa2e-147">MongoDB 셸에서 Azure Cosmos DB MongoDB 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-147">Connect to your Azure Cosmos DB MongoDB database from the MongoDB Shell.</span></span> <span data-ttu-id="0fa2e-148">[Azure Cosmos DB에 MongoDB 응용 프로그램 연결](connect-mongodb-account.md)에서 지침을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-148">You can find instructions in [Connect a MongoDB application to Azure Cosmos DB](connect-mongodb-account.md).</span></span>
    
    <span data-ttu-id="0fa2e-149">b.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-149">b.</span></span> <span data-ttu-id="0fa2e-150">MongoDB 셸에서 샘플 문서 중 하나를 사용하여 샘플 삽입 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-150">Run a sample insert command by using one of your sample documents from the MongoDB Shell:</span></span>
    
        ```db.coll.insert({ "playerId": "a067ff", "hashedid": "bb0091", "countryCode": "hk" })```
        
    <span data-ttu-id="0fa2e-151">c.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-151">c.</span></span> <span data-ttu-id="0fa2e-152">```db.runCommand({getLastRequestStatistics: 1})```를 실행하고 다음과 같은 응답을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-152">Run ```db.runCommand({getLastRequestStatistics: 1})``` and you will receive a response like this one:</span></span>
     
        ```
        globaldb:PRIMARY> db.runCommand({getLastRequestStatistics: 1})
        {
            "_t": "GetRequestStatisticsResponse",
            "ok": 1,
            "CommandName": "insert",
            "RequestCharge": 10,
            "RequestDurationInMilliSeconds": NumberLong(50)
        }
        ```
        
    <span data-ttu-id="0fa2e-153">d.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-153">d.</span></span> <span data-ttu-id="0fa2e-154">요청 요금을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-154">Take note of the request charge.</span></span>
    
3. <span data-ttu-id="0fa2e-155">컴퓨터에서 Azure Cosmos DB 클라우드 서비스까지의 대기 시간을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-155">Determine the latency from your machine to the Azure Cosmos DB cloud service:</span></span>
    
    <span data-ttu-id="0fa2e-156">a.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-156">a.</span></span> <span data-ttu-id="0fa2e-157">다음 명령을 사용하여 MongoDB 셸에서 자세한 로깅 정보를 표시합니다. ```setVerboseShell(true)```</span><span class="sxs-lookup"><span data-stu-id="0fa2e-157">Enable verbose logging from the MongoDB Shell by using this command: ```setVerboseShell(true)```</span></span>
    
    <span data-ttu-id="0fa2e-158">b.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-158">b.</span></span> <span data-ttu-id="0fa2e-159">데이터베이스에 대해 간단한 쿼리를 실행합니다. ```db.coll.find().limit(1)```</span><span class="sxs-lookup"><span data-stu-id="0fa2e-159">Run a simple query against the database: ```db.coll.find().limit(1)```.</span></span> <span data-ttu-id="0fa2e-160">다음과 같은 응답을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-160">You will receive a response like this one:</span></span>

        ```
        Fetched 1 record(s) in 100(ms)
        ```
        
4. <span data-ttu-id="0fa2e-161">마이그레이션 이전에 삽입된 문서를 제거하여 중복된 문서가 없도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-161">Remove the inserted document before the migration to ensure that there are no duplicate documents.</span></span> <span data-ttu-id="0fa2e-162">다음 명령을 사용하여 문서를 제거할 수 있습니다. ```db.coll.remove({})```</span><span class="sxs-lookup"><span data-stu-id="0fa2e-162">You can remove documents by using this command: ```db.coll.remove({})```</span></span>

5. <span data-ttu-id="0fa2e-163">대략적인 *batchSize* 및 *numInsertionWorkers* 값을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-163">Calculate the approximate *batchSize* and *numInsertionWorkers* values:</span></span>

    * <span data-ttu-id="0fa2e-164">*batchSize*에 대해 프로비전된 총 RU를 3단계의 단일 문서 쓰기에서 사용한 RU로 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-164">For *batchSize*, divide the total provisioned RUs by the RUs consumed from your single document write in step 3.</span></span>
    
    * <span data-ttu-id="0fa2e-165">계산된 *batchSize* <= 24이면 이 숫자를 *batchSize* 값으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-165">If the calculated *batchSize* <= 24, use that number as your *batchSize* value.</span></span>
    
    * <span data-ttu-id="0fa2e-166">계산된 *batchSize* > 24이면 *batchSize* 값을 24로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-166">If the calculated *batchSize* > 24, set the *batchSize* value to 24.</span></span>
    
    * <span data-ttu-id="0fa2e-167">*numInsertionWorkers*의 경우 *numInsertionWorkers =  (프로비전된 처리량 * 초 단위 대기 시간)/(배치 크기 * 단일 쓰기에 사용한 RU)* 수식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-167">For *numInsertionWorkers*, use this equation:   *numInsertionWorkers =  (provisioned throughput * latency in seconds) / (batch size * consumed RUs for a single write)*.</span></span>
        
    |<span data-ttu-id="0fa2e-168">속성</span><span class="sxs-lookup"><span data-stu-id="0fa2e-168">Property</span></span>|<span data-ttu-id="0fa2e-169">값</span><span class="sxs-lookup"><span data-stu-id="0fa2e-169">Value</span></span>|
    |--------|-----|
    |<span data-ttu-id="0fa2e-170">batchSize</span><span class="sxs-lookup"><span data-stu-id="0fa2e-170">batchSize</span></span>| <span data-ttu-id="0fa2e-171">24</span><span class="sxs-lookup"><span data-stu-id="0fa2e-171">24</span></span> |
    |<span data-ttu-id="0fa2e-172">프로비전된 RU</span><span class="sxs-lookup"><span data-stu-id="0fa2e-172">RUs provisioned</span></span> | <span data-ttu-id="0fa2e-173">10000</span><span class="sxs-lookup"><span data-stu-id="0fa2e-173">10000</span></span> |
    |<span data-ttu-id="0fa2e-174">대기 시간</span><span class="sxs-lookup"><span data-stu-id="0fa2e-174">Latency</span></span> | <span data-ttu-id="0fa2e-175">0.100s</span><span class="sxs-lookup"><span data-stu-id="0fa2e-175">0.100 s</span></span> |
    |<span data-ttu-id="0fa2e-176">1개 문서 쓰기에 대해 청구된 RU</span><span class="sxs-lookup"><span data-stu-id="0fa2e-176">RU charged for 1 doc write</span></span> | <span data-ttu-id="0fa2e-177">10RU</span><span class="sxs-lookup"><span data-stu-id="0fa2e-177">10 RUs</span></span> |
    |<span data-ttu-id="0fa2e-178">numInsertionWorkers</span><span class="sxs-lookup"><span data-stu-id="0fa2e-178">numInsertionWorkers</span></span> | <span data-ttu-id="0fa2e-179">?</span><span class="sxs-lookup"><span data-stu-id="0fa2e-179">?</span></span> |
    
    <span data-ttu-id="0fa2e-180">*numInsertionWorkers = (10000 RU x 0.1s) / (24 x 10 RU) = 4.1666*</span><span class="sxs-lookup"><span data-stu-id="0fa2e-180">*numInsertionWorkers = (10000 RUs x 0.1 s) / (24 x 10 RUs) = 4.1666*</span></span>

6. <span data-ttu-id="0fa2e-181">최종 마이그레이션 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-181">Run the final migration command:</span></span>

   ```
   mongoimport.exe --host anhoh-mongodb.documents.azure.com:10255 -u anhoh-mongodb -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates --jsonArray --db dabasename --collection collectionName --file "C:\sample.json" --numInsertionWorkers 4 --batchSize 24
   ```

## <a name="next-steps"></a><span data-ttu-id="0fa2e-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0fa2e-182">Next steps</span></span>

<span data-ttu-id="0fa2e-183">다음 자습서로 진행하여 Azure Cosmos DB로 MongoDB 데이터를 쿼리하는 방법을 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fa2e-183">You can proceed to the next tutorial and learn how to query MongoDB data by using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="0fa2e-184">MongoDB 데이터를 쿼리하는 방법</span><span class="sxs-lookup"><span data-stu-id="0fa2e-184">How to query MongoDB data?</span></span>](../cosmos-db/tutorial-query-mongodb.md)
