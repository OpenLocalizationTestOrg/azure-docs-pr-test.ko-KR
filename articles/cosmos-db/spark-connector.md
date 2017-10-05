---
title: "Azure Cosmos DB에 Apache Spark 연결 | Microsoft Docs"
description: "이 자습서에서는 Azure Cosmos DB Spark 커넥터를 통해 Azure Cosmos DB에 Apache Spark를 연결하여 Microsoft에서 클라우드를 위해 설계한 다중 테넌트 전역 분산형 데이터베이스 시스템에서 분산 집계 및 데이터 과학을 수행할 수 있는 방법에 대해 알아봅니다."
keywords: Apache Spark
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: c4f46007-2606-4273-ab16-29d0e15c0736
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: denlee
ms.openlocfilehash: 8ecbb478c81cde25bbd0d1c9ee07ae02b07f8cc7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="accelerate-real-time-big-data-analytics-with-the-spark-to-azure-cosmos-db-connector"></a><span data-ttu-id="7190a-104">Spark-Azure Cosmos DB 커넥터를 사용하여 실시간 빅 데이터 분석 가속화</span><span class="sxs-lookup"><span data-stu-id="7190a-104">Accelerate real-time big-data analytics with the Spark to Azure Cosmos DB connector</span></span>

<span data-ttu-id="7190a-105">Spark-Azure Cosmos DB 커넥터를 사용하면 Azure Cosmos DB가 Apache Spark 작업의 입력 소스 또는 출력 싱크로 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-105">The Spark to Azure Cosmos DB connector enables Azure Cosmos DB to act as an input source or output sink for Apache Spark jobs.</span></span> <span data-ttu-id="7190a-106">[Spark](http://spark.apache.org/)를 [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)에 연결하면 빠르게 움직이는 데이터 과학 문제를 더욱 빠르게 해결할 수 있도록 하므로 Azure Cosmos DB를 사용하여 데이터를 신속하게 저장하고 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-106">Connecting [Spark](http://spark.apache.org/) to [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) accelerates your ability to solve fast-moving data science problems where you can use Azure Cosmos DB to quickly persist and query data.</span></span> <span data-ttu-id="7190a-107">Spark-Azure Cosmos DB 커넥터는 네이티브 Azure Cosmos DB 관리 인덱스를 효율적으로 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-107">The Spark to Azure Cosmos DB connector efficiently utilizes the native Azure Cosmos DB managed indexes.</span></span> <span data-ttu-id="7190a-108">인덱스는 IoT(사물 인터넷)에서 데이터 과학 및 분석 시나리오에 이르기까지 급변하는 전역 분산 데이터에 대한 분석 및 푸시다운 조건자 필터링을 수행할 때 업데이트할 수 있는 열을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-108">The indexes enable updateable columns when you perform analytics and push-down predicate filtering against fast-changing globally distributed data, which range from Internet of Things (IoT) to data science and analytics scenarios.</span></span>

<span data-ttu-id="7190a-109">Spark GraphX 및 Azure Cosmos DB의 Gremlin Graph API로 작업하는 경우 [Spark 및 Apache TinkerPop Gremlin을 사용하여 그래프 분석 수행](spark-connector-graph.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7190a-109">For working with Spark GraphX and the Gremlin graph APIs of Azure Cosmos DB, see [Perform graph analytics using Spark and Apache TinkerPop Gremlin](spark-connector-graph.md).</span></span>

## <a name="download"></a><span data-ttu-id="7190a-110">다운로드</span><span class="sxs-lookup"><span data-stu-id="7190a-110">Download</span></span>

<span data-ttu-id="7190a-111">시작하려면 GitHub의 [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) 리포지토리에서 Spark-Azure Cosmos DB 커넥터(미리 보기)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-111">To get started, download the Spark to Azure Cosmos DB connector (preview) from the [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) repository on GitHub.</span></span>

## <a name="connector-components"></a><span data-ttu-id="7190a-112">커넥터 구성 요소</span><span class="sxs-lookup"><span data-stu-id="7190a-112">Connector components</span></span>

<span data-ttu-id="7190a-113">커넥터는 다음 구성 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-113">The connector utilizes the following components:</span></span>

* <span data-ttu-id="7190a-114">[Azure Cosmos DB](http://documentdb.com)를 사용하면 고객은 여러 지리적 영역에서 처리량과 저장소를 프로비전하고 탄력적으로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-114">[Azure Cosmos DB](http://documentdb.com) enables customers to provision and elastically scale both throughput and storage across any number of geographical regions.</span></span> <span data-ttu-id="7190a-115">서비스에서는 다음을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-115">The service offers:</span></span>
   * <span data-ttu-id="7190a-116">턴키 [전역 배포](distribute-data-globally.md) 및 수평적 확장</span><span class="sxs-lookup"><span data-stu-id="7190a-116">Turn key [global distribution](distribute-data-globally.md) and horizontal scale</span></span>
   * <span data-ttu-id="7190a-117">백분위 99의 1자리 수 대기 시간 보증</span><span class="sxs-lookup"><span data-stu-id="7190a-117">Guaranteed single digit latencies at the 99th percentile</span></span>
   * [<span data-ttu-id="7190a-118">잘 정의된 다중 일관성 모델</span><span class="sxs-lookup"><span data-stu-id="7190a-118">Multiple well-defined consistency models</span></span>](consistency-levels.md)
   * <span data-ttu-id="7190a-119">multi-homing 기능을 통한 고가용성 보장</span><span class="sxs-lookup"><span data-stu-id="7190a-119">Guaranteed high availability with multi-homing capabilities</span></span>
   * <span data-ttu-id="7190a-120">모든 기능이 업계 최고 수준의 포괄적인 SLA([서비스 수준 약정](https://azure.microsoft.com/support/legal/sla/cosmos-db))에 의해 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-120">All features are backed by industry-leading, comprehensive [service level agreements](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLAs).</span></span>

* <span data-ttu-id="7190a-121">[Apache Spark](http://spark.apache.org/)는 속도, 사용 편의성 및 정교한 분석을 기반으로 구축된 강력한 오픈 소스 처리 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-121">[Apache Spark](http://spark.apache.org/) is a powerful open source processing engine that's built around speed, ease of use, and sophisticated analytics.</span></span>

* <span data-ttu-id="7190a-122">[Azure HDInsight에서 Apache Spark](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md)를 사용하면 중요 업무용 배포를 위해 [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/)를 사용하여 클라우드에 Apache Spark를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-122">[Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) so that you can deploy Apache Spark in the cloud for mission-critical deployments by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="7190a-123">공식적으로 지원되는 버전:</span><span class="sxs-lookup"><span data-stu-id="7190a-123">Officially supported versions:</span></span>

| <span data-ttu-id="7190a-124">구성 요소</span><span class="sxs-lookup"><span data-stu-id="7190a-124">Component</span></span> | <span data-ttu-id="7190a-125">버전</span><span class="sxs-lookup"><span data-stu-id="7190a-125">Version</span></span> |
|---------|-------|
|<span data-ttu-id="7190a-126">Apache Spark</span><span class="sxs-lookup"><span data-stu-id="7190a-126">Apache Spark</span></span>|<span data-ttu-id="7190a-127">2.0+</span><span class="sxs-lookup"><span data-stu-id="7190a-127">2.0+</span></span>|
| <span data-ttu-id="7190a-128">스칼라</span><span class="sxs-lookup"><span data-stu-id="7190a-128">Scala</span></span>| <span data-ttu-id="7190a-129">2.11</span><span class="sxs-lookup"><span data-stu-id="7190a-129">2.11</span></span>|
| <span data-ttu-id="7190a-130">Azure DocumentDB Java SDK</span><span class="sxs-lookup"><span data-stu-id="7190a-130">Azure DocumentDB Java SDK</span></span> | <span data-ttu-id="7190a-131">1.10.0</span><span class="sxs-lookup"><span data-stu-id="7190a-131">1.10.0</span></span> |

<span data-ttu-id="7190a-132">이 문서는 Python(pyDocumentDB를 통해)과 Scala 인터페이스를 사용하여 간단한 샘플을 실행하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-132">This article helps you run some simple samples by using Python (via pyDocumentDB) and the Scala interfaces.</span></span>

<span data-ttu-id="7190a-133">Apache Spark와 Azure Cosmos DB를 연결하는 방법에는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-133">There are two approaches to connect Apache Spark and Azure Cosmos DB:</span></span>
- <span data-ttu-id="7190a-134">[Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python)를 통해 pyDocumentDB를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-134">Use pyDocumentDB via the [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python).</span></span>
- <span data-ttu-id="7190a-135">[Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java)를 사용하여 Java 기반 Spark-Azure Cosmos DB 커넥터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-135">Create a Java-based Spark to Azure Cosmos DB connector by utilizing the [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

## <a name="pydocumentdb-implementation"></a><span data-ttu-id="7190a-136">pyDocumentDB 구현</span><span class="sxs-lookup"><span data-stu-id="7190a-136">pyDocumentDB implementation</span></span>
<span data-ttu-id="7190a-137">현재 [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python)를 사용하면 다음 다이어그램과 같이 Spark를 Azure Cosmos DB에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-137">The current [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) enables you to connect Spark to Azure Cosmos DB as shown in the following diagram:</span></span>

![pyDocumentDB DB를 통한 Spark-Azure Cosmos DB 데이터 흐름](./media/spark-connector/spark-pydocumentdb.png)


### <a name="data-flow-of-the-pydocumentdb-implementation"></a><span data-ttu-id="7190a-139">pyDocumentDB 구현의 데이터 흐름</span><span class="sxs-lookup"><span data-stu-id="7190a-139">Data flow of the pyDocumentDB implementation</span></span>

<span data-ttu-id="7190a-140">데이터 흐름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-140">The data flow is as follows:</span></span>

1. <span data-ttu-id="7190a-141">Spark 마스터 노드는 pyDocumentDB를 통해 Azure Cosmos DB 게이트웨이 노드에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-141">The Spark master node connects to the Azure Cosmos DB gateway node via pyDocumentDB.</span></span> <span data-ttu-id="7190a-142">사용자는 Spark 및 Azure Cosmos DB 연결만 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-142">A user specifies only the Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="7190a-143">해당 마스터 및 게이트웨이 노드에 대한 연결은 사용자에게 투명합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-143">Connections to the respective master and gateway nodes are transparent to the user.</span></span>
2. <span data-ttu-id="7190a-144">게이트웨이 노드를 통해 Azure Cosmos DB에 대해 쿼리가 수행되며, 이후에 여기서 데이터 노드의 컬렉션 파티션에 대해 쿼리가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-144">The gateway node makes the query against Azure Cosmos DB where the query subsequently runs against the collection's partitions in the data nodes.</span></span> <span data-ttu-id="7190a-145">이러한 쿼리에 대한 응답은 게이트웨이 노드로 다시 보내지고, 결과 집합은 Spark 마스터 노드로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-145">The response for those queries is sent back to the gateway node, and that result set is returned to the Spark master node.</span></span>
3. <span data-ttu-id="7190a-146">이후의 쿼리(예: Spark DataFrame)는 처리를 위해 Spark 작업자 노드로 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-146">Subsequent queries (for example, against a Spark DataFrame) are sent to the Spark worker nodes for processing.</span></span>

<span data-ttu-id="7190a-147">Spark와 Azure Cosmos DB 간의 통신은 Spark 마스터 노드와 Azure Cosmos DB 게이트웨이 노드로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-147">Communication between Spark and Azure Cosmos DB is limited to the Spark master node and Azure Cosmos DB gateway nodes.</span></span>  <span data-ttu-id="7190a-148">쿼리는 이 두 노드 사이의 전송 계층만큼 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-148">The queries go as fast as the transport layer between these two nodes allows.</span></span>

### <a name="install-pydocumentdb"></a><span data-ttu-id="7190a-149">pyDocumentDB 설치</span><span class="sxs-lookup"><span data-stu-id="7190a-149">Install pyDocumentDB</span></span>
<span data-ttu-id="7190a-150">**pip**를 사용하여 드라이버 노드에 pyDocumentDB를 설치할 수 있습니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-150">You can install pyDocumentDB on your driver node by using **pip**, for example:</span></span>

```
pip install pyDocumentDB
```


### <a name="connect-spark-to-azure-cosmos-db-via-pydocumentdb"></a><span data-ttu-id="7190a-151">pyDocumentDB를 통해 Azure Cosmos DB에 Spark 연결</span><span class="sxs-lookup"><span data-stu-id="7190a-151">Connect Spark to Azure Cosmos DB via pyDocumentDB</span></span>
<span data-ttu-id="7190a-152">통신 전송의 단순성으로 인해 pyDocumentDB를 사용하여 Spark에서 Azure Cosmos DB로 쿼리를 실행하는 것이 비교적 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-152">The simplicity of the communication transport makes execution of a query from Spark to Azure Cosmos DB by using pyDocumentDB relatively simple.</span></span>

<span data-ttu-id="7190a-153">다음 코드 조각에서는 Spark 컨텍스트에서 pyDocumentDB를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-153">The following code snippet shows how to use pyDocumentDB in a Spark context.</span></span>

```
# Import Necessary Libraries
import pydocumentdb
from pydocumentdb import document_client
from pydocumentdb import documents
import datetime

# Configuring the connection policy (allowing for endpoint discovery)
connectionPolicy = documents.ConnectionPolicy()
connectionPolicy.EnableEndpointDiscovery
connectionPolicy.PreferredLocations = ["Central US", "East US 2", "Southeast Asia", "Western Europe","Canada Central"]


# Set keys to connect to Azure Cosmos DB
masterKey = 'le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA=='
host = 'https://doctorwho.documents.azure.com:443/'
client = document_client.DocumentClient(host, {'masterKey': masterKey}, connectionPolicy)
```

<span data-ttu-id="7190a-154">코드 조각에서 설명했듯이</span><span class="sxs-lookup"><span data-stu-id="7190a-154">As noted in the code snippet:</span></span>

* <span data-ttu-id="7190a-155">Azure Cosmos DB Python SDK(`pyDocumentDB`)에는 모든 필수 연결 매개 변수가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-155">The Azure Cosmos DB Python SDK (`pyDocumentDB`) contains the all the necessary connection parameters.</span></span> <span data-ttu-id="7190a-156">예를 들어 기본 위치 매개 변수는 읽기 복제본 및 우선 순위 순서를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-156">For example, the preferred locations parameter chooses the read replica and priority order.</span></span>
*  <span data-ttu-id="7190a-157">필요한 라이브러리를 가져와서 **masterKey** 및 **호스트**를 구성하여 Azure Cosmos DB *클라이언트*(**pydocumentdb.document_client**)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-157">Import the necessary libraries and configure your **masterKey** and **host** to create the Azure Cosmos DB *client* (**pydocumentdb.document_client**).</span></span>


### <a name="execute-spark-queries-via-pydocumentdb"></a><span data-ttu-id="7190a-158">pyDocumentDB를 통해 Spark 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="7190a-158">Execute Spark Queries via pyDocumentDB</span></span>
<span data-ttu-id="7190a-159">다음 예제에서는 지정된 읽기 전용 키를 사용하여 이전 코드 조각에서 만들어진 Azure Cosmos DB 인스턴스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-159">The following examples use the Azure Cosmos DB instance that was created in the previous snippet by using the specified read-only keys.</span></span> <span data-ttu-id="7190a-160">다음 코드 조각은 앞에서 지정한 DoctorWho 계정의 **airports.codes** 컬렉션에 연결하여 워싱턴 주에 있는 공항 도시를 추출하는 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-160">The following code snippet connects to the **airports.codes** collection in the DoctorWho account as specified earlier and runs a query to extract the airport cities in Washington state.</span></span>

```
# Configure Database and Collections
databaseId = 'airports'
collectionId = 'codes'

# Configurations the Azure Cosmos DB client will use to connect to the database and collection
dbLink = 'dbs/' + databaseId
collLink = dbLink + '/colls/' + collectionId

# Set query parameter
querystr = "SELECT c.City FROM c WHERE c.State='WA'"

# Query documents
query = client.QueryDocuments(collLink, querystr, options=None, partition_key=None)

# Query for partitioned collections
# query = client.QueryDocuments(collLink, query, options= { 'enableCrossPartitionQuery': True }, partition_key=None)

# Push into list `elements`
elements = list(query)
```

<span data-ttu-id="7190a-161">쿼리가 **query**를 통해 실행되면 결과는 Python 목록으로 변환된 **query_iterable.QueryIterable**입니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-161">After the query has been executed via **query**, the result is a **query_iterable.QueryIterable** that is converted to a Python list.</span></span> <span data-ttu-id="7190a-162">Python 목록은 다음 코드를 사용하여 Spark DataFrame으로 쉽게 변환될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-162">A Python list can be easily converted to a Spark DataFrame by using the following code:</span></span>

```
# Create `df` Spark DataFrame from `elements` Python list
df = spark.createDataFrame(elements)
```

### <a name="why-use-the-pydocumentdb-to-connect-spark-to-azure-cosmos-db"></a><span data-ttu-id="7190a-163">pyDocumentDB를 사용하여 Azure Cosmos DB에 Spark를 연결하는 이유</span><span class="sxs-lookup"><span data-stu-id="7190a-163">Why use the pyDocumentDB to connect Spark to Azure Cosmos DB?</span></span>
<span data-ttu-id="7190a-164">pyDocumentDB를 사용하여 Azure Cosmos DB에 Spark를 연결하는 시나리오는 일반적으로 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-164">Connecting Spark to Azure Cosmos DB by using pyDocumentDB is typically for scenarios where:</span></span>

* <span data-ttu-id="7190a-165">Python을 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-165">You want to use Python.</span></span>
* <span data-ttu-id="7190a-166">비교적 작은 결과 집합을 Azure Cosmos DB에서 Spark로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-166">You are returning a relatively small result set from Azure Cosmos DB to Spark.</span></span> <span data-ttu-id="7190a-167">Azure Cosmos DB의 기본 데이터 집합은 상당히 클 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-167">Note that the underlying dataset in Azure Cosmos DB can be quite large.</span></span> <span data-ttu-id="7190a-168">Azure Cosmos DB 소스에 대해 필터를 적용 즉, 조건자 필터를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-168">You are applying filters, that is, running predicate filters, against your Azure Cosmos DB source.</span></span>  

## <a name="spark-to-azure-cosmos-db-connector"></a><span data-ttu-id="7190a-169">Spark-Azure Cosmos DB 커넥터</span><span class="sxs-lookup"><span data-stu-id="7190a-169">Spark to Azure Cosmos DB connector</span></span>

<span data-ttu-id="7190a-170">Spark-Azure Cosmos DB 커넥터는 [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java)를 사용하고 다음 다이어그램과 같이 Spark 작업자 노드와 Azure Cosmos DB 간에 데이터를 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-170">The Spark to Azure Cosmos DB connector utilizes the [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java) and moves data between the Spark worker nodes and Azure Cosmos DB as shown in the following diagram:</span></span>

![Spark-Azure Cosmos DB 커넥터의 데이터 흐름](./media/spark-connector/spark-connector.png)

<span data-ttu-id="7190a-172">데이터 흐름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-172">The data flow is as follows:</span></span>

1. <span data-ttu-id="7190a-173">Spark 마스터 노드는 Azure Cosmos DB 게이트웨이 노드에 연결하여 파티션 맵을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-173">The Spark master node connects to the Azure Cosmos DB gateway node to obtain the partition map.</span></span> <span data-ttu-id="7190a-174">사용자는 Spark 및 Azure Cosmos DB 연결만 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-174">A user specifies only the Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="7190a-175">해당 마스터 및 게이트웨이 노드에 대한 연결은 사용자에게 투명합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-175">Connections to the respective master and gateway nodes are transparent to the user.</span></span>
2. <span data-ttu-id="7190a-176">이 정보는 Spark 마스터 노드에 다시 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-176">This information is provided back to the Spark master node.</span></span>  <span data-ttu-id="7190a-177">이 시점에서 쿼리를 구문 분석하여 액세스해야 하는 Azure Cosmos DB의 파티션 및 해당 위치를 확인할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-177">At this point, you should be able to parse the query to determine the partitions and their locations in Azure Cosmos DB that you need to access.</span></span>
3. <span data-ttu-id="7190a-178">이 정보는 Spark 작업자 노드로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-178">This information is transmitted to the Spark worker nodes.</span></span>
4. <span data-ttu-id="7190a-179">Spark 작업자 노드는 Azure Cosmos DB 파티션에 직접 연결하여 데이터를 추출하고 Spark 작업자 노드의 Spark 파티션으로 데이터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-179">The Spark worker nodes connect to the Azure Cosmos DB partitions directly to extract the data and return the data to the Spark partitions in the Spark worker nodes.</span></span>

<span data-ttu-id="7190a-180">Spark 작업자 노드와 Azure Cosmos DB 데이터 노드(파티션) 간에 데이터가 이동하므로 Spark와 Azure Cosmos DB 간의 통신이 훨씬 더 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-180">Communication between Spark and Azure Cosmos DB is significantly faster because the data movement is between the Spark worker nodes and the Azure Cosmos DB data nodes (partitions).</span></span>

### <a name="build-the-spark-to-azure-cosmos-db-connector"></a><span data-ttu-id="7190a-181">Spark-Azure Cosmos DB 커넥터 빌드</span><span class="sxs-lookup"><span data-stu-id="7190a-181">Build the Spark to Azure Cosmos DB connector</span></span>
<span data-ttu-id="7190a-182">현재 커넥터 프로젝트는 maven을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-182">Currently, the connector project uses maven.</span></span> <span data-ttu-id="7190a-183">종속성 없이 커넥터를 빌드하려면 다음을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-183">To build the connector without dependencies, you can run:</span></span>
```
mvn clean package
```
<span data-ttu-id="7190a-184">또한 *releases* 폴더에서 최신 버전의 JAR를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-184">You can also download the latest versions of the JAR from the *releases* folder.</span></span>

### <a name="include-the-azure-cosmos-db-spark-jar"></a><span data-ttu-id="7190a-185">Azure Cosmos DB Spark JAR 포함</span><span class="sxs-lookup"><span data-stu-id="7190a-185">Include the Azure Cosmos DB Spark JAR</span></span>
<span data-ttu-id="7190a-186">코드를 실행하기 전에 먼저 Azure Cosmos DB Spark JAR를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-186">Before you execute any code, you need to include the Azure Cosmos DB Spark JAR.</span></span>  <span data-ttu-id="7190a-187">**spark-shell**을 사용하는 경우 **--jars** 옵션을 사용하여 JAR를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-187">If you are using the **spark-shell**, then you can include the JAR by using the **--jars** option.</span></span>  

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3-jar-with-dependencies.jar
```

<span data-ttu-id="7190a-188">종속성 없이 JAR를 실행하려면 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-188">If you want to execute the JAR without dependencies, use the following code:</span></span>

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3.jar,/$location/azure-documentdb-1.10.0.jar
```

<span data-ttu-id="7190a-189">노트북 서비스(예: Azure HDInsight Jupyter 노트북 서비스)를 사용하는 경우 **spark 매직** 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-189">If you are using a notebook service such as Azure HDInsight Jupyter notebook service, you can use the **spark magic** commands:</span></span>

```
%%configure
{ "jars": ["wasb:///example/jars/azure-documentdb-1.10.0.jar","wasb:///example/jars/azure-cosmosdb-spark-0.0.3.jar"],
  "conf": {
    "spark.jars.excludes": "org.scala-lang:scala-reflect"
   }
}
```

<span data-ttu-id="7190a-190">**jars** 명령을 사용하면 **azure-cosmosdb-spark**(자체 및 Azure DocumentDB Java SDK)에 필요한 두 개의 JAR를 포함하고 **scala-reflect**를 제외할 수 있으므로 Livy 호출을 방해하지 않습니다(Jupyter 노트북 > Livy > Spark).</span><span class="sxs-lookup"><span data-stu-id="7190a-190">The **jars** command enables you to include the two JARs that are needed for **azure-cosmosdb-spark** (itself and the Azure DocumentDB Java SDK) and exclude **scala-reflect** so that it does not interfere with the Livy calls (Jupyter notebook > Livy > Spark).</span></span>

### <a name="connect-spark-to-azure-cosmos-db-using-the-connector"></a><span data-ttu-id="7190a-191">커넥터를 사용하여 Spark를 Azure Cosmos DB에 연결</span><span class="sxs-lookup"><span data-stu-id="7190a-191">Connect Spark to Azure Cosmos DB using the connector</span></span>
<span data-ttu-id="7190a-192">통신 전송이 좀 더 복잡하지만, 커넥터를 사용하여 Spark에서 Azure Cosmos DB로 쿼리를 실행하는 것이 훨씬 더 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-192">Although the communication transport is a little more complicated, executing a query from Spark to Azure Cosmos DB by using the connector is significantly faster.</span></span>

<span data-ttu-id="7190a-193">다음 코드 조각에서는 Spark 컨텍스트에서 커넥터를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-193">The following code snippet shows how to use the connector in a Spark context.</span></span>

```
// Import Necessary Libraries
import org.joda.time._
import org.joda.time.format._
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Configure connection to your collection
val readConfig2 = Config(Map("Endpoint" -> "https://doctorwho.documents.azure.com:443/",
"Masterkey" -> "le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA==",
"Database" -> "DepartureDelays",
"preferredRegions" -> "Central US;East US2;",
"Collection" -> "flights_pcoll",
"SamplingRatio" -> "1.0"))

// Create collection connection
val coll = spark.sqlContext.read.cosmosDB(readConfig2)
coll.createOrReplaceTempView("c")
```

<span data-ttu-id="7190a-194">코드 조각에서 설명했듯이</span><span class="sxs-lookup"><span data-stu-id="7190a-194">As noted in the code snippet:</span></span>

- <span data-ttu-id="7190a-195">**azure-cosmosdb-spark**에는 기본 위치가 포함된 모든 필수 연결 매개 변수가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-195">**azure-cosmosdb-spark** contains the all the necessary connection parameters, which include the preferred locations.</span></span> <span data-ttu-id="7190a-196">예를 들어 읽기 복제본 및 우선 순위 순서를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-196">For example, you can choose the read replica and priority order.</span></span>
- <span data-ttu-id="7190a-197">필요한 라이브러리를 가져와서 masterKey 및 호스트를 구성하여 Azure Cosmos DB 클라이언트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-197">Just import the necessary libraries and configure your masterKey and host to create the Azure Cosmos DB client.</span></span>

### <a name="execute-spark-queries-via-the-connector"></a><span data-ttu-id="7190a-198">커넥터를 통해 Spark 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="7190a-198">Execute Spark queries via the connector</span></span>

<span data-ttu-id="7190a-199">다음 예제에서는 지정된 읽기 전용 키를 사용하여 이전 코드 조각에서 만들어진 Azure Cosmos DB 인스턴스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-199">The following example uses the Azure Cosmos DB instance that was created in the previous snippet by using the specified read-only keys.</span></span> <span data-ttu-id="7190a-200">다음 코드 조각은 DepartureDelays.flights_pcoll 컬렉션(앞에서 지정한 DoctorWho 계정)에 연결하여 시애틀에서 출발하는 항공편의 비행 지연 정보를 추출하는 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-200">The following code snippet connects to the DepartureDelays.flights_pcoll collection (in the DoctorWho account as specified earlier) and runs a query to extract the flight delay information of flights that are departing from Seattle.</span></span>

```
// Queries
var query = "SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'"
val df = spark.sql(query)

// Run DF query (count)
df.count()

// Run DF query (show)
df.show()
```

### <a name="why-use-the-spark-to-azure-cosmos-db-connector-implementation"></a><span data-ttu-id="7190a-201">Spark-Azure Cosmos DB 커넥터 구현을 사용하는 이유</span><span class="sxs-lookup"><span data-stu-id="7190a-201">Why use the Spark to Azure Cosmos DB connector implementation?</span></span>

<span data-ttu-id="7190a-202">커넥터를 사용하여 Azure Cosmos DB에 Spark를 연결하는 시나리오는 일반적으로 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-202">Connecting Spark to Azure Cosmos DB by using the connector is typically for scenarios where:</span></span>

* <span data-ttu-id="7190a-203">Scala를 사용하고 [Issue 3: Add Python wrapper and examples](https://github.com/Azure/azure-cosmosdb-spark/issues/3)(문제 3: Python 래퍼 및 예제 추가)에서 설명한 대로 Python 래퍼를 포함하도록 업데이트하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-203">You want to use Scala and update it to include a Python wrapper as noted in [Issue 3: Add Python wrapper and examples](https://github.com/Azure/azure-cosmosdb-spark/issues/3).</span></span>
* <span data-ttu-id="7190a-204">Apache Spark와 Azure Cosmos DB 간에 많은 양의 데이터를 전송해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-204">You have a large amount of data to transfer between Apache Spark and Azure Cosmos DB.</span></span>

<span data-ttu-id="7190a-205">쿼리 성능 차이에 대한 자세한 내용은 [쿼리 테스트 실행 wiki](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7190a-205">To give you an idea of the query performance difference, see the [Query Test Runs wiki](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span></span>

## <a name="distributed-aggregation-example"></a><span data-ttu-id="7190a-206">분산 집계 예제</span><span class="sxs-lookup"><span data-stu-id="7190a-206">Distributed aggregation example</span></span>
<span data-ttu-id="7190a-207">이 섹션에서는 Apache Spark와 Azure Cosmos DB를 함께 사용하여 분산 집계 및 분석을 수행하는 방법의 몇 가지 예를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-207">This section provides some examples of how you can do distributed aggregations and analytics by using Apache Spark and Azure Cosmos DB together.</span></span> <span data-ttu-id="7190a-208">[Planet scale aggregates with Azure Cosmos DB](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/)(Azure Cosmos DB를 사용한 전 세계적인 규모의 집계) 블로그에 설명된 대로 Azure Cosmos DB는 이미 집계를 지원하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-208">Azure Cosmos DB already supports aggregations, which is discussed in the [Planet scale aggregates with Azure Cosmos DB blog](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/).</span></span> <span data-ttu-id="7190a-209">이러한 방법으로 Apache Spark를 사용하여 다음 단계로 넘어갈 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-209">Here is how you can take it to the next level with Apache Spark.</span></span>

<span data-ttu-id="7190a-210">이러한 집계는 [Spark-Azure Cosmos DB 커넥터 노트북](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb)을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-210">Note that these aggregations are in reference to the [Spark to Azure Cosmos DB Connector notebook](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span></span>

### <a name="connect-to-flights-sample-data"></a><span data-ttu-id="7190a-211">비행 샘플 데이터에 연결</span><span class="sxs-lookup"><span data-stu-id="7190a-211">Connect to flights sample data</span></span>
<span data-ttu-id="7190a-212">이러한 집계 예제에서는 **DoctorWho** Azure Cosmos DB 데이터베이스에 저장된 일부 비행 성능 데이터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-212">These aggregation examples access some flight performance data that's stored in our **DoctorWho** Azure Cosmos DB database.</span></span> <span data-ttu-id="7190a-213">연결하려면 다음 코드 조각을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-213">To connect to it, you need to utilize the following code snippet:</span></span>

```
// Import Spark to Azure Cosmos DB connector
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Connect to Azure Cosmos DB Database
val readConfig2 = Config(Map("Endpoint" -> "https://doctorwho.documents.azure.com:443/",
"Masterkey" -> "le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA==",
"Database" -> "DepartureDelays",
"preferredRegions" -> "Central US;East US 2;",
"Collection" -> "flights_pcoll",
"SamplingRatio" -> "1.0"))

// Create collection connection
val coll = spark.sqlContext.read.cosmosDB(readConfig2)
coll.createOrReplaceTempView("c")
```

<span data-ttu-id="7190a-214">또한 이 코드 조각을 사용하여 필터링된 데이터 집합을 Azure Cosmos DB에서 Spark로 전송하는 기본 쿼리를 실행합니다. Spark는 분산 집계를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-214">With this snippet, we are also going to run a base query that transfers the filtered set of data from Azure Cosmos DB to Spark where the latter can perform distributed aggregates.</span></span> <span data-ttu-id="7190a-215">이 경우 시애틀(SEA)에서 출발하는 항공편을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-215">In this case, we are asking for flights that depart from Seattle (SEA).</span></span>

```
// Run, get row count, and time query
val originSEA = spark.sql("SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'")
originSEA.createOrReplaceTempView("originSEA")
```

<span data-ttu-id="7190a-216">다음 결과는 Jupyter 노트북 서비스에서 쿼리를 실행하여 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-216">The following results were generated by running the queries from the Jupyter notebook service.</span></span>  <span data-ttu-id="7190a-217">모든 코드 조각은 일반적이며 어떤 서비스와도 관련이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-217">Note that all the code snippets are generic and not specific to any service.</span></span>

### <a name="running-limit-and-count-queries"></a><span data-ttu-id="7190a-218">LIMIT 및 COUNT 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="7190a-218">Running LIMIT and COUNT queries</span></span>
<span data-ttu-id="7190a-219">SQL/Spark SQL에서 사용했던 것처럼 **LIMIT** 쿼리로 시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-219">Just like you're used to in SQL/Spark SQL, let's start off with a **LIMIT** query:</span></span>

![Spark LIMIT 쿼리](./media/spark-connector/spark-sql-query.png)

<span data-ttu-id="7190a-221">다음 쿼리는 간단하고 빠른 **COUNT** 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-221">The next query is a simple and fast **COUNT** query:</span></span>

![Spark COUNT 쿼리](./media/spark-connector/spark-count-query.png)

### <a name="group-by-query"></a><span data-ttu-id="7190a-223">GROUP BY 쿼리</span><span class="sxs-lookup"><span data-stu-id="7190a-223">GROUP BY query</span></span>
<span data-ttu-id="7190a-224">다음 집합에서 Azure Cosmos DB 데이터베이스에 대해 **GROUP BY** 쿼리를 쉽게 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-224">In this next set, we can easily run **GROUP BY** queries against our Azure Cosmos DB database:</span></span>

```
select destination, sum(delay) as TotalDelays
from originSEA
group by destination
order by sum(delay) desc limit 10
```

![Spark GROUP BY 쿼리 그래프](./media/spark-connector/group-by-query-graph.png)

### <a name="distinct-order-by-query"></a><span data-ttu-id="7190a-226">DISTINCT, ORDER BY 쿼리</span><span class="sxs-lookup"><span data-stu-id="7190a-226">DISTINCT, ORDER BY query</span></span>
<span data-ttu-id="7190a-227">다음은 **DISTINCT, ORDER BY** 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-227">And here is a **DISTINCT, ORDER BY** query:</span></span>

![Spark GROUP BY 쿼리 그래프](./media/spark-connector/order-by-query.png)

### <a name="continue-the-flight-data-analysis"></a><span data-ttu-id="7190a-229">비행 데이터 분석 계속</span><span class="sxs-lookup"><span data-stu-id="7190a-229">Continue the flight data analysis</span></span>
<span data-ttu-id="7190a-230">다음 예제 쿼리를 사용하여 비행 데이터 분석을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-230">You can use the following example queries to continue analysis of the flight data:</span></span>

#### <a name="top-5-delayed-destinations-cities-departing-from-seattle"></a><span data-ttu-id="7190a-231">시애틀에서 출발하는 상위 5개 지연 대상(도시)</span><span class="sxs-lookup"><span data-stu-id="7190a-231">Top 5 delayed destinations (cities) departing from Seattle</span></span>
```
select destination, sum(delay)
from originSEA
where delay < 0
group by destination
order by sum(delay) limit 5
```
![Spark 상위 지연 그래프](./media/spark-connector/top-delays-graph.png)


#### <a name="calculate-median-delays-by-destination-cities-departing-from-seattle"></a><span data-ttu-id="7190a-233">시애틀에서 출발하는 대상 도시별 지연 중앙값 계산</span><span class="sxs-lookup"><span data-stu-id="7190a-233">Calculate median delays by destination cities departing from Seattle</span></span>
```
select destination, percentile_approx(delay, 0.5) as median_delay
from originSEA
where delay < 0
group by destination
order by percentile_approx(delay, 0.5)
```

![Spark 지연 중앙값 지연 그래프](./media/spark-connector/median-delays-graph.png)

## <a name="next-steps"></a><span data-ttu-id="7190a-235">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7190a-235">Next steps</span></span>

<span data-ttu-id="7190a-236">Cosmos DB와 Spark를 아직 연결하지 않았으면 [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub 리포지토리에서 Spark-Azure Cosmos DB 커넥터를 다운로드하고 다음 리포지토리에서 추가 리소스를 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-236">If you haven't already, download the Spark to Azure Cosmos DB connector from the [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub repository and explore the additional resources in the repo:</span></span>

* <span data-ttu-id="7190a-237">[분산 집계 예제](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples)(영문)</span><span class="sxs-lookup"><span data-stu-id="7190a-237">[Distributed Aggregations Examples](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples)</span></span>
* <span data-ttu-id="7190a-238">[샘플 스크립트 및 노트북](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples)(영문)</span><span class="sxs-lookup"><span data-stu-id="7190a-238">[Sample Scripts and Notebooks](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples)</span></span>

<span data-ttu-id="7190a-239">또한 [Apache Spark SQL, DataFrames, and Datasets Guide](http://spark.apache.org/docs/latest/sql-programming-guide.html)(Apache Spark SQL, DataFrame 및 데이터 집합 가이드) 및 [Azure HDInsight의 Apache Spark](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) 문서를 검토할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7190a-239">You might also want to review the [Apache Spark SQL, DataFrames, and Datasets Guide](http://spark.apache.org/docs/latest/sql-programming-guide.html) and the [Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) article.</span></span>
