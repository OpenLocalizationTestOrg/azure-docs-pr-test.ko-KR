---
title: aaaConnecting Apache Spark tooAzure Cosmos DB | Microsoft Docs
description: "이 자습서 toolearn tooconnect Apache Spark tooAzure Cosmos DB distributed tooperform 집계 및 Microsoft에서 hello 다중 테 넌 트 전 세계적으로 분산된 데이터베이스 시스템에서 데이터 과학 수 있는 hello Azure Cosmos DB Spark 커넥터에 대 한 사용 hello 클라우드 위해 설계 되었습니다."
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
ms.openlocfilehash: 70b496fc5ca8f65675f0224e749637f5d533c346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="accelerate-real-time-big-data-analytics-with-hello-spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="b78c7-104">Hello Spark tooAzure Cosmos DB 커넥터와 함께 실시간 빅 데이터 분석을 가속화</span><span class="sxs-lookup"><span data-stu-id="b78c7-104">Accelerate real-time big-data analytics with hello Spark tooAzure Cosmos DB connector</span></span>

<span data-ttu-id="b78c7-105">hello Spark tooAzure Cosmos DB 커넥터를 사용 하면 입력된 소스 또는 Apache Spark 작업에 대 한 출력 싱크 Azure Cosmos DB tooact 합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-105">hello Spark tooAzure Cosmos DB connector enables Azure Cosmos DB tooact as an input source or output sink for Apache Spark jobs.</span></span> <span data-ttu-id="b78c7-106">연결 [스파크](http://spark.apache.org/) 너무[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 프로그램 기능 toosolve 빠르게 변화 데이터 과학 Azure Cosmos DB tooquickly를 사용할 수 있는 문제를 유지 하 고 데이터를 쿼리할 가속화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-106">Connecting [Spark](http://spark.apache.org/) too[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) accelerates your ability toosolve fast-moving data science problems where you can use Azure Cosmos DB tooquickly persist and query data.</span></span> <span data-ttu-id="b78c7-107">hello Spark tooAzure Cosmos DB 커넥터 hello 네이티브 Azure Cosmos DB 관리 되는 인덱스를 효율적으로 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-107">hello Spark tooAzure Cosmos DB connector efficiently utilizes hello native Azure Cosmos DB managed indexes.</span></span> <span data-ttu-id="b78c7-108">hello 인덱스 필터링 빠르게 변경 전역에 대 한 푸시 다운 조건자 분산 인터넷 IoT (사물) toodata 과학 및 분석 시나리오에서 범위는 데이터 및 분석을 수행 해야 하는 경우 업데이트 가능한 열의 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-108">hello indexes enable updateable columns when you perform analytics and push-down predicate filtering against fast-changing globally distributed data, which range from Internet of Things (IoT) toodata science and analytics scenarios.</span></span>

<span data-ttu-id="b78c7-109">Spark GraphX 및 hello Gremlin 그래프 Azure Cosmos DB Api를 사용 하기 위한 참조 [Spark 및 Apache TinkerPop Gremlin 사용 하 여 그래프 분석 수행](spark-connector-graph.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-109">For working with Spark GraphX and hello Gremlin graph APIs of Azure Cosmos DB, see [Perform graph analytics using Spark and Apache TinkerPop Gremlin](spark-connector-graph.md).</span></span>

## <a name="download"></a><span data-ttu-id="b78c7-110">다운로드</span><span class="sxs-lookup"><span data-stu-id="b78c7-110">Download</span></span>

<span data-ttu-id="b78c7-111">tooget 시작을 hello에서 hello Spark tooAzure Cosmos DB 커넥터 (preview)를 다운로드 하 여 [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) GitHub의 리포지토리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-111">tooget started, download hello Spark tooAzure Cosmos DB connector (preview) from hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) repository on GitHub.</span></span>

## <a name="connector-components"></a><span data-ttu-id="b78c7-112">커넥터 구성 요소</span><span class="sxs-lookup"><span data-stu-id="b78c7-112">Connector components</span></span>

<span data-ttu-id="b78c7-113">hello 커넥터는 hello 다음과 같은 구성 요소가 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="b78c7-113">hello connector utilizes hello following components:</span></span>

* <span data-ttu-id="b78c7-114">[Azure Cosmos DB](http://documentdb.com) 고객 tooprovision 있으며 특정 처리량과 저장소 지리적 영역을 개수에 관계 없이 탄력적으로 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-114">[Azure Cosmos DB](http://documentdb.com) enables customers tooprovision and elastically scale both throughput and storage across any number of geographical regions.</span></span> <span data-ttu-id="b78c7-115">hello 서비스 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-115">hello service offers:</span></span>
   * <span data-ttu-id="b78c7-116">턴키 [전역 배포](distribute-data-globally.md) 및 수평적 확장</span><span class="sxs-lookup"><span data-stu-id="b78c7-116">Turn key [global distribution](distribute-data-globally.md) and horizontal scale</span></span>
   * <span data-ttu-id="b78c7-117">단일 숫자 대기 hello 99 번째 백분위 수를 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-117">Guaranteed single digit latencies at hello 99th percentile</span></span>
   * [<span data-ttu-id="b78c7-118">잘 정의된 다중 일관성 모델</span><span class="sxs-lookup"><span data-stu-id="b78c7-118">Multiple well-defined consistency models</span></span>](consistency-levels.md)
   * <span data-ttu-id="b78c7-119">multi-homing 기능을 통한 고가용성 보장</span><span class="sxs-lookup"><span data-stu-id="b78c7-119">Guaranteed high availability with multi-homing capabilities</span></span>
   * <span data-ttu-id="b78c7-120">모든 기능이 업계 최고 수준의 포괄적인 SLA([서비스 수준 약정](https://azure.microsoft.com/support/legal/sla/cosmos-db))에 의해 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-120">All features are backed by industry-leading, comprehensive [service level agreements](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLAs).</span></span>

* <span data-ttu-id="b78c7-121">[Apache Spark](http://spark.apache.org/)는 속도, 사용 편의성 및 정교한 분석을 기반으로 구축된 강력한 오픈 소스 처리 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-121">[Apache Spark](http://spark.apache.org/) is a powerful open source processing engine that's built around speed, ease of use, and sophisticated analytics.</span></span>

* <span data-ttu-id="b78c7-122">[Azure HDInsight의 Apache Spark](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) 를 사용 하 여 업무상 중요 한 배포에 대 한 hello 클라우드에서 Apache Spark를 배포할 수 있도록 [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-122">[Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) so that you can deploy Apache Spark in hello cloud for mission-critical deployments by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="b78c7-123">공식적으로 지원되는 버전:</span><span class="sxs-lookup"><span data-stu-id="b78c7-123">Officially supported versions:</span></span>

| <span data-ttu-id="b78c7-124">구성 요소</span><span class="sxs-lookup"><span data-stu-id="b78c7-124">Component</span></span> | <span data-ttu-id="b78c7-125">버전</span><span class="sxs-lookup"><span data-stu-id="b78c7-125">Version</span></span> |
|---------|-------|
|<span data-ttu-id="b78c7-126">Apache Spark</span><span class="sxs-lookup"><span data-stu-id="b78c7-126">Apache Spark</span></span>|<span data-ttu-id="b78c7-127">2.0+</span><span class="sxs-lookup"><span data-stu-id="b78c7-127">2.0+</span></span>|
| <span data-ttu-id="b78c7-128">스칼라</span><span class="sxs-lookup"><span data-stu-id="b78c7-128">Scala</span></span>| <span data-ttu-id="b78c7-129">2.11</span><span class="sxs-lookup"><span data-stu-id="b78c7-129">2.11</span></span>|
| <span data-ttu-id="b78c7-130">Azure DocumentDB Java SDK</span><span class="sxs-lookup"><span data-stu-id="b78c7-130">Azure DocumentDB Java SDK</span></span> | <span data-ttu-id="b78c7-131">1.10.0</span><span class="sxs-lookup"><span data-stu-id="b78c7-131">1.10.0</span></span> |

<span data-ttu-id="b78c7-132">이 문서를 사용 하면 (pyDocumentDB)를 통해 Python을 사용 하 여 몇 가지 간단한 예제를 실행 하 고 Scala 인터페이스 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-132">This article helps you run some simple samples by using Python (via pyDocumentDB) and hello Scala interfaces.</span></span>

<span data-ttu-id="b78c7-133">두 가지 방법 tooconnect Apache Spark와 Azure Cosmos DB 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-133">There are two approaches tooconnect Apache Spark and Azure Cosmos DB:</span></span>
- <span data-ttu-id="b78c7-134">Hello 통해 pyDocumentDB를 사용 하 여 [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python)합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-134">Use pyDocumentDB via hello [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python).</span></span>
- <span data-ttu-id="b78c7-135">Hello를 활용 하 여 Java 기반 Spark tooAzure Cosmos DB 커넥터 만들기 [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java)합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-135">Create a Java-based Spark tooAzure Cosmos DB connector by utilizing hello [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

## <a name="pydocumentdb-implementation"></a><span data-ttu-id="b78c7-136">pyDocumentDB 구현</span><span class="sxs-lookup"><span data-stu-id="b78c7-136">pyDocumentDB implementation</span></span>
<span data-ttu-id="b78c7-137">현재 hello [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) hello 다음 다이어그램에에서 표시 된 대로 tooconnect Spark tooAzure Cosmos DB를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-137">hello current [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) enables you tooconnect Spark tooAzure Cosmos DB as shown in hello following diagram:</span></span>

![Spark tooAzure pyDocumentDB DB 통해 데이터 흐름 Cosmos DB](./media/spark-connector/spark-pydocumentdb.png)


### <a name="data-flow-of-hello-pydocumentdb-implementation"></a><span data-ttu-id="b78c7-139">Hello pyDocumentDB 구현의 데이터 흐름</span><span class="sxs-lookup"><span data-stu-id="b78c7-139">Data flow of hello pyDocumentDB implementation</span></span>

<span data-ttu-id="b78c7-140">hello 데이터 흐름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-140">hello data flow is as follows:</span></span>

1. <span data-ttu-id="b78c7-141">hello Spark 마스터 노드 pyDocumentDB 통해 toohello Azure Cosmos DB 게이트웨이 노드를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-141">hello Spark master node connects toohello Azure Cosmos DB gateway node via pyDocumentDB.</span></span> <span data-ttu-id="b78c7-142">사용자만 hello Spark 및 Azure Cosmos DB 연결을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-142">A user specifies only hello Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="b78c7-143">연결 toohello 해당 마스터 및 게이트웨이 노드는 투명 toohello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-143">Connections toohello respective master and gateway nodes are transparent toohello user.</span></span>
2. <span data-ttu-id="b78c7-144">hello 게이트웨이 노드는 hello 쿼리가 이후에 hello 데이터 노드에 hello 컬렉션의 파티션에 대해 실행 하는 Azure Cosmos DB에 대 한 hello 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-144">hello gateway node makes hello query against Azure Cosmos DB where hello query subsequently runs against hello collection's partitions in hello data nodes.</span></span> <span data-ttu-id="b78c7-145">해당 쿼리에 대해 hello 응답 toohello 게이트웨이 노드 및 해당 결과 집합은 toohello Spark 마스터 노드를 반환 하는 다시 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-145">hello response for those queries is sent back toohello gateway node, and that result set is returned toohello Spark master node.</span></span>
3. <span data-ttu-id="b78c7-146">(예를 들어 스파크 데이터 프레임)에 대해 후속 쿼리 toohello Spark 작업자 노드 처리를 위해 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-146">Subsequent queries (for example, against a Spark DataFrame) are sent toohello Spark worker nodes for processing.</span></span>

<span data-ttu-id="b78c7-147">Spark와 Azure Cosmos DB 간 통신이 제한 toohello Spark 마스터 노드 및 Azure Cosmos DB 게이트웨이 노드 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-147">Communication between Spark and Azure Cosmos DB is limited toohello Spark master node and Azure Cosmos DB gateway nodes.</span></span>  <span data-ttu-id="b78c7-148">hello 쿼리는 두 노드 사이의 hello 전송 계층에서 허용 하는 만큼 빠르게 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-148">hello queries go as fast as hello transport layer between these two nodes allows.</span></span>

### <a name="install-pydocumentdb"></a><span data-ttu-id="b78c7-149">pyDocumentDB 설치</span><span class="sxs-lookup"><span data-stu-id="b78c7-149">Install pyDocumentDB</span></span>
<span data-ttu-id="b78c7-150">**pip**를 사용하여 드라이버 노드에 pyDocumentDB를 설치할 수 있습니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-150">You can install pyDocumentDB on your driver node by using **pip**, for example:</span></span>

```
pip install pyDocumentDB
```


### <a name="connect-spark-tooazure-cosmos-db-via-pydocumentdb"></a><span data-ttu-id="b78c7-151">Spark tooAzure Cosmos DB pyDocumentDB 통해 연결</span><span class="sxs-lookup"><span data-stu-id="b78c7-151">Connect Spark tooAzure Cosmos DB via pyDocumentDB</span></span>
<span data-ttu-id="b78c7-152">hello 통신 전송의 hello 단순성에서는 비교적 간단한 pyDocumentDB를 사용 하 여 Spark tooAzure Cosmos DB에서에서 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-152">hello simplicity of hello communication transport makes execution of a query from Spark tooAzure Cosmos DB by using pyDocumentDB relatively simple.</span></span>

<span data-ttu-id="b78c7-153">다음 코드 조각에 나와 있는 어떻게 hello Spark 컨텍스트에서 toouse pyDocumentDB 합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-153">hello following code snippet shows how toouse pyDocumentDB in a Spark context.</span></span>

```
# Import Necessary Libraries
import pydocumentdb
from pydocumentdb import document_client
from pydocumentdb import documents
import datetime

# Configuring hello connection policy (allowing for endpoint discovery)
connectionPolicy = documents.ConnectionPolicy()
connectionPolicy.EnableEndpointDiscovery
connectionPolicy.PreferredLocations = ["Central US", "East US 2", "Southeast Asia", "Western Europe","Canada Central"]


# Set keys tooconnect tooAzure Cosmos DB
masterKey = 'le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA=='
host = 'https://doctorwho.documents.azure.com:443/'
client = document_client.DocumentClient(host, {'masterKey': masterKey}, connectionPolicy)
```

<span data-ttu-id="b78c7-154">Hello 코드 조각에서 설명한 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="b78c7-154">As noted in hello code snippet:</span></span>

* <span data-ttu-id="b78c7-155">hello Azure Cosmos DB Python SDK (`pyDocumentDB`) hello가 포함 되어 모든 hello 필요한 연결 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-155">hello Azure Cosmos DB Python SDK (`pyDocumentDB`) contains hello all hello necessary connection parameters.</span></span> <span data-ttu-id="b78c7-156">예를 들어 hello 기본 위치 매개 변수 hello 읽을 복제 데이터베이스 및 우선 순위 순서를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-156">For example, hello preferred locations parameter chooses hello read replica and priority order.</span></span>
*  <span data-ttu-id="b78c7-157">Hello 필요한 라이브러리를 가져오고 구성 하 여 **masterKey** 및 **호스트** toocreate hello Azure Cosmos DB *클라이언트* (**pydocumentdb.document_ 클라이언트**).</span><span class="sxs-lookup"><span data-stu-id="b78c7-157">Import hello necessary libraries and configure your **masterKey** and **host** toocreate hello Azure Cosmos DB *client* (**pydocumentdb.document_client**).</span></span>


### <a name="execute-spark-queries-via-pydocumentdb"></a><span data-ttu-id="b78c7-158">pyDocumentDB를 통해 Spark 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="b78c7-158">Execute Spark Queries via pyDocumentDB</span></span>
<span data-ttu-id="b78c7-159">다음 예에서는 사용 하 여 hello Azure Cosmos DB 인스턴스 hello를 사용 하 여 hello 이전 코드 조각에서 만든 hello 읽기 전용 키를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-159">hello following examples use hello Azure Cosmos DB instance that was created in hello previous snippet by using hello specified read-only keys.</span></span> <span data-ttu-id="b78c7-160">hello 다음 코드 조각 연결 toohello **airports.codes** 와 hello DoctorWho 계정에 이전에 지정한 컬렉션과 워싱턴 주에 있는 쿼리 tooextract hello 공항 도시를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-160">hello following code snippet connects toohello **airports.codes** collection in hello DoctorWho account as specified earlier and runs a query tooextract hello airport cities in Washington state.</span></span>

```
# Configure Database and Collections
databaseId = 'airports'
collectionId = 'codes'

# Configurations hello Azure Cosmos DB client will use tooconnect toohello database and collection
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

<span data-ttu-id="b78c7-161">Hello 쿼리를 통해 실행 된 후 **쿼리**, hello 결과는 **query_iterable 합니다. QueryIterable** 즉 변환 된 tooa Python 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-161">After hello query has been executed via **query**, hello result is a **query_iterable.QueryIterable** that is converted tooa Python list.</span></span> <span data-ttu-id="b78c7-162">Python 목록 코드 다음 hello를 사용 하 여 쉽게 변환 된 tooa Spark 데이터 프레임을 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-162">A Python list can be easily converted tooa Spark DataFrame by using hello following code:</span></span>

```
# Create `df` Spark DataFrame from `elements` Python list
df = spark.createDataFrame(elements)
```

### <a name="why-use-hello-pydocumentdb-tooconnect-spark-tooazure-cosmos-db"></a><span data-ttu-id="b78c7-163">Hello pyDocumentDB tooconnect Spark tooAzure Cosmos DB를 사용 하는 이유는?</span><span class="sxs-lookup"><span data-stu-id="b78c7-163">Why use hello pyDocumentDB tooconnect Spark tooAzure Cosmos DB?</span></span>
<span data-ttu-id="b78c7-164">Spark tooAzure pyDocumentDB를 사용 하 여 Cosmos DB는 일반적으로 시나리오에 대 한 연결 위치:</span><span class="sxs-lookup"><span data-stu-id="b78c7-164">Connecting Spark tooAzure Cosmos DB by using pyDocumentDB is typically for scenarios where:</span></span>

* <span data-ttu-id="b78c7-165">Toouse Python 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-165">You want toouse Python.</span></span>
* <span data-ttu-id="b78c7-166">상대적으로 작은 결과 집합 Azure Cosmos DB tooSpark에서 반환 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-166">You are returning a relatively small result set from Azure Cosmos DB tooSpark.</span></span> <span data-ttu-id="b78c7-167">Azure Cosmos DB에서 기본 데이터 집합을 hello는 매우 클 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-167">Note that hello underlying dataset in Azure Cosmos DB can be quite large.</span></span> <span data-ttu-id="b78c7-168">Azure Cosmos DB 소스에 대해 필터를 적용 즉, 조건자 필터를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-168">You are applying filters, that is, running predicate filters, against your Azure Cosmos DB source.</span></span>  

## <a name="spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="b78c7-169">Spark tooAzure Cosmos DB 커넥터</span><span class="sxs-lookup"><span data-stu-id="b78c7-169">Spark tooAzure Cosmos DB connector</span></span>

<span data-ttu-id="b78c7-170">hello Spark tooAzure Cosmos DB 커넥터 활용 hello [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java) hello 다음 다이어그램에에서 표시 된 대로 hello Spark 작업자 노드 및 Azure Cosmos DB 사이의 데이터를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-170">hello Spark tooAzure Cosmos DB connector utilizes hello [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java) and moves data between hello Spark worker nodes and Azure Cosmos DB as shown in hello following diagram:</span></span>

![Hello Spark tooAzure Cosmos DB 커넥터의 데이터 흐름](./media/spark-connector/spark-connector.png)

<span data-ttu-id="b78c7-172">hello 데이터 흐름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-172">hello data flow is as follows:</span></span>

1. <span data-ttu-id="b78c7-173">hello Spark 마스터 노드 toohello Azure Cosmos DB 게이트웨이 노드 tooobtain hello 파티션 맵이 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-173">hello Spark master node connects toohello Azure Cosmos DB gateway node tooobtain hello partition map.</span></span> <span data-ttu-id="b78c7-174">사용자만 hello Spark 및 Azure Cosmos DB 연결을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-174">A user specifies only hello Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="b78c7-175">연결 toohello 해당 마스터 및 게이트웨이 노드는 투명 toohello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-175">Connections toohello respective master and gateway nodes are transparent toohello user.</span></span>
2. <span data-ttu-id="b78c7-176">이 정보는 뒤로 toohello Spark 마스터 노드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-176">This information is provided back toohello Spark master node.</span></span>  <span data-ttu-id="b78c7-177">이 시점에서 수 tooparse hello 쿼리 toodetermine hello 파티션 및 tooaccess 해야 하는 Azure Cosmos DB에 위치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-177">At this point, you should be able tooparse hello query toodetermine hello partitions and their locations in Azure Cosmos DB that you need tooaccess.</span></span>
3. <span data-ttu-id="b78c7-178">이 정보는 전송 된 toohello Spark 작업자 노드.</span><span class="sxs-lookup"><span data-stu-id="b78c7-178">This information is transmitted toohello Spark worker nodes.</span></span>
4. <span data-ttu-id="b78c7-179">hello Spark 작업자 노드 tooextract 데이터 hello 다음 다시 돌아와 hello 데이터 toohello Spark 파티션을 hello Spark 작업자 노드에서 직접 toohello Azure Cosmos DB 파티션에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-179">hello Spark worker nodes connect toohello Azure Cosmos DB partitions directly tooextract hello data and return hello data toohello Spark partitions in hello Spark worker nodes.</span></span>

<span data-ttu-id="b78c7-180">Spark와 Azure Cosmos DB 간의 통신 훨씬 더 빠릅니다 hello 데이터 이동은 hello Spark 작업자 노드 및 hello Azure Cosmos DB 데이터 노드 (파티션) 사이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-180">Communication between Spark and Azure Cosmos DB is significantly faster because hello data movement is between hello Spark worker nodes and hello Azure Cosmos DB data nodes (partitions).</span></span>

### <a name="build-hello-spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="b78c7-181">빌드 hello Spark tooAzure Cosmos DB 커넥터</span><span class="sxs-lookup"><span data-stu-id="b78c7-181">Build hello Spark tooAzure Cosmos DB connector</span></span>
<span data-ttu-id="b78c7-182">현재, hello 커넥터 프로젝트 maven을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-182">Currently, hello connector project uses maven.</span></span> <span data-ttu-id="b78c7-183">종속성이 없는 toobuild hello 커넥터를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-183">toobuild hello connector without dependencies, you can run:</span></span>
```
mvn clean package
```
<span data-ttu-id="b78c7-184">Hello에서 hello hello JAR의 최신 버전을 다운로드할 수도 있습니다 *해제* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-184">You can also download hello latest versions of hello JAR from hello *releases* folder.</span></span>

### <a name="include-hello-azure-cosmos-db-spark-jar"></a><span data-ttu-id="b78c7-185">Azure Cosmos DB Spark JAR hello를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-185">Include hello Azure Cosmos DB Spark JAR</span></span>
<span data-ttu-id="b78c7-186">모든 코드를 실행 하기 전에 Azure Cosmos DB Spark JAR tooinclude hello를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-186">Before you execute any code, you need tooinclude hello Azure Cosmos DB Spark JAR.</span></span>  <span data-ttu-id="b78c7-187">Hello를 사용 하는 경우 **spark 셸**, hello를 사용 하 여 hello JAR를 포함할 수 있습니다 다음 **-jar** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-187">If you are using hello **spark-shell**, then you can include hello JAR by using hello **--jars** option.</span></span>  

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3-jar-with-dependencies.jar
```

<span data-ttu-id="b78c7-188">종속성이 없는 tooexecute hello JAR hello 코드 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-188">If you want tooexecute hello JAR without dependencies, use hello following code:</span></span>

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3.jar,/$location/azure-documentdb-1.10.0.jar
```

<span data-ttu-id="b78c7-189">Azure HDInsight Jupyter 노트북 서비스와 같은 전자 필기장 서비스를 사용 하는 경우에 hello을 사용할 수 있습니다 **매직 멤버** 명령:</span><span class="sxs-lookup"><span data-stu-id="b78c7-189">If you are using a notebook service such as Azure HDInsight Jupyter notebook service, you can use hello **spark magic** commands:</span></span>

```
%%configure
{ "jars": ["wasb:///example/jars/azure-documentdb-1.10.0.jar","wasb:///example/jars/azure-cosmosdb-spark-0.0.3.jar"],
  "conf": {
    "spark.jars.excludes": "org.scala-lang:scala-reflect"
   }
}
```

<span data-ttu-id="b78c7-190">hello **jar** 있습니다 tooinclude hello 두 개 사용 하는 단지 명령에 필요한 **azure-cosmosdb-spark** (자체 및 Azure DocumentDB Java SDK hello)를 제외 하 고 **scala-반영** hello 리비 호출로 간섭 하지 않도록 (Jupyter 노트북 > 리비 > Spark).</span><span class="sxs-lookup"><span data-stu-id="b78c7-190">hello **jars** command enables you tooinclude hello two JARs that are needed for **azure-cosmosdb-spark** (itself and hello Azure DocumentDB Java SDK) and exclude **scala-reflect** so that it does not interfere with hello Livy calls (Jupyter notebook > Livy > Spark).</span></span>

### <a name="connect-spark-tooazure-cosmos-db-using-hello-connector"></a><span data-ttu-id="b78c7-191">연결 Spark 커넥터 hello tooAzure Cosmos DB를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="b78c7-191">Connect Spark tooAzure Cosmos DB using hello connector</span></span>
<span data-ttu-id="b78c7-192">Hello 통신 전송을 좀 더 복잡 한 경우에 Spark tooAzure에서 쿼리를 실행 Cosmos DB hello 커넥터를 사용 하 여 훨씬 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-192">Although hello communication transport is a little more complicated, executing a query from Spark tooAzure Cosmos DB by using hello connector is significantly faster.</span></span>

<span data-ttu-id="b78c7-193">다음 코드 조각 hello toouse Spark 컨텍스트에서 커넥터 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-193">hello following code snippet shows how toouse hello connector in a Spark context.</span></span>

```
// Import Necessary Libraries
import org.joda.time._
import org.joda.time.format._
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Configure connection tooyour collection
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

<span data-ttu-id="b78c7-194">Hello 코드 조각에서 설명한 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="b78c7-194">As noted in hello code snippet:</span></span>

- <span data-ttu-id="b78c7-195">**azure-cosmosdb-spark** hello가 포함 되어 모든 hello hello 기본 위치를 포함 하는 데 필요한 연결 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-195">**azure-cosmosdb-spark** contains hello all hello necessary connection parameters, which include hello preferred locations.</span></span> <span data-ttu-id="b78c7-196">예를 들어 hello 읽을 복제 데이터베이스 및 우선 순위 순서를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-196">For example, you can choose hello read replica and priority order.</span></span>
- <span data-ttu-id="b78c7-197">Hello 필요한 라이브러리를 가져오고 masterKey 및 호스트 toocreate hello Azure Cosmos DB 클라이언트 구성만 합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-197">Just import hello necessary libraries and configure your masterKey and host toocreate hello Azure Cosmos DB client.</span></span>

### <a name="execute-spark-queries-via-hello-connector"></a><span data-ttu-id="b78c7-198">Hello 커넥터를 통해 Spark 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="b78c7-198">Execute Spark queries via hello connector</span></span>

<span data-ttu-id="b78c7-199">다음 예에 사용 하 여 hello Azure Cosmos DB 인스턴스에 hello를 사용 하 여 hello 이전 코드 조각에서 만든 hello 읽기 전용 키를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-199">hello following example uses hello Azure Cosmos DB instance that was created in hello previous snippet by using hello specified read-only keys.</span></span> <span data-ttu-id="b78c7-200">hello 다음 코드 조각 연결 toohello DepartureDelays.flights_pcoll 컬렉션 (이전에 지정 된 DoctorWho 계정 hello)을 실행 한 쿼리 tooextract hello 비행 지연 정보 시애틀에서 달라진 다는 냅니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-200">hello following code snippet connects toohello DepartureDelays.flights_pcoll collection (in hello DoctorWho account as specified earlier) and runs a query tooextract hello flight delay information of flights that are departing from Seattle.</span></span>

```
// Queries
var query = "SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'"
val df = spark.sql(query)

// Run DF query (count)
df.count()

// Run DF query (show)
df.show()
```

### <a name="why-use-hello-spark-tooazure-cosmos-db-connector-implementation"></a><span data-ttu-id="b78c7-201">Hello Spark tooAzure Cosmos DB 커넥터 구현을 사용 하는 이유</span><span class="sxs-lookup"><span data-stu-id="b78c7-201">Why use hello Spark tooAzure Cosmos DB connector implementation?</span></span>

<span data-ttu-id="b78c7-202">Cosmos DB hello 커넥터를 사용 하는 시나리오에 대 한 일반적으로 스파크 tooAzure 연결 위치:</span><span class="sxs-lookup"><span data-stu-id="b78c7-202">Connecting Spark tooAzure Cosmos DB by using hello connector is typically for scenarios where:</span></span>

* <span data-ttu-id="b78c7-203">Toouse Scala을 tooinclude Python 래퍼에 설명 된 대로 업데이트 [문제 3: 추가 Python 래퍼 및 예제](https://github.com/Azure/azure-cosmosdb-spark/issues/3)합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-203">You want toouse Scala and update it tooinclude a Python wrapper as noted in [Issue 3: Add Python wrapper and examples](https://github.com/Azure/azure-cosmosdb-spark/issues/3).</span></span>
* <span data-ttu-id="b78c7-204">많은 양의 데이터 tootransfer Apache Spark와 Azure Cosmos DB 간의 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-204">You have a large amount of data tootransfer between Apache Spark and Azure Cosmos DB.</span></span>

<span data-ttu-id="b78c7-205">toogive hello 참조을 hello 쿼리 성능 차이 이해할 수 [쿼리 테스트 실행 wiki](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs)합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-205">toogive you an idea of hello query performance difference, see hello [Query Test Runs wiki](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span></span>

## <a name="distributed-aggregation-example"></a><span data-ttu-id="b78c7-206">분산 집계 예제</span><span class="sxs-lookup"><span data-stu-id="b78c7-206">Distributed aggregation example</span></span>
<span data-ttu-id="b78c7-207">이 섹션에서는 Apache Spark와 Azure Cosmos DB를 함께 사용하여 분산 집계 및 분석을 수행하는 방법의 몇 가지 예를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-207">This section provides some examples of how you can do distributed aggregations and analytics by using Apache Spark and Azure Cosmos DB together.</span></span> <span data-ttu-id="b78c7-208">Azure Cosmos DB 이미 지원 하 고 집계를 hello에 설명 된 대로 [Azure Cosmos DB 블로그를 사용 하 여 지구 눈금 집계](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-208">Azure Cosmos DB already supports aggregations, which is discussed in hello [Planet scale aggregates with Azure Cosmos DB blog](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/).</span></span> <span data-ttu-id="b78c7-209">다음 방법을 사용할 수 있으며 toohello 다음은 Apache Spark와 함께 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-209">Here is how you can take it toohello next level with Apache Spark.</span></span>

<span data-ttu-id="b78c7-210">이러한 집계에 참조 toohello 서로 [Spark tooAzure Cosmos DB 커넥터 노트북](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb)합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-210">Note that these aggregations are in reference toohello [Spark tooAzure Cosmos DB Connector notebook](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span></span>

### <a name="connect-tooflights-sample-data"></a><span data-ttu-id="b78c7-211">Tooflights 샘플 데이터에 연결</span><span class="sxs-lookup"><span data-stu-id="b78c7-211">Connect tooflights sample data</span></span>
<span data-ttu-id="b78c7-212">이러한 집계 예제에서는 **DoctorWho** Azure Cosmos DB 데이터베이스에 저장된 일부 비행 성능 데이터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-212">These aggregation examples access some flight performance data that's stored in our **DoctorWho** Azure Cosmos DB database.</span></span> <span data-ttu-id="b78c7-213">tooconnect tooit 다음 코드 조각 tooutilize hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-213">tooconnect tooit, you need tooutilize hello following code snippet:</span></span>

```
// Import Spark tooAzure Cosmos DB connector
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Connect tooAzure Cosmos DB Database
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

<span data-ttu-id="b78c7-214">이 조각을 사용 하는 또한 지속적인 toorun 전송 필터링 된 데이터의 집합에서 Azure Cosmos DB tooSpark hello를 기본 쿼리 hello 후자 분산된 집계를 수행할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-214">With this snippet, we are also going toorun a base query that transfers hello filtered set of data from Azure Cosmos DB tooSpark where hello latter can perform distributed aggregates.</span></span> <span data-ttu-id="b78c7-215">이 경우 시애틀(SEA)에서 출발하는 항공편을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-215">In this case, we are asking for flights that depart from Seattle (SEA).</span></span>

```
// Run, get row count, and time query
val originSEA = spark.sql("SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'")
originSEA.createOrReplaceTempView("originSEA")
```

<span data-ttu-id="b78c7-216">hello 다음과 같은 결과가 생성 된 hello Jupyter 노트북 서비스에서에서 hello 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-216">hello following results were generated by running hello queries from hello Jupyter notebook service.</span></span>  <span data-ttu-id="b78c7-217">모든 hello 코드 조각은 일반적이 고 구체적인 하지 tooany 서비스 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-217">Note that all hello code snippets are generic and not specific tooany service.</span></span>

### <a name="running-limit-and-count-queries"></a><span data-ttu-id="b78c7-218">LIMIT 및 COUNT 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="b78c7-218">Running LIMIT and COUNT queries</span></span>
<span data-ttu-id="b78c7-219">같은 정당한 사용 되는 SQL/Spark SQL tooin 보겠습니다으로 시작 한 **제한** 쿼리:</span><span class="sxs-lookup"><span data-stu-id="b78c7-219">Just like you're used tooin SQL/Spark SQL, let's start off with a **LIMIT** query:</span></span>

![Spark LIMIT 쿼리](./media/spark-connector/spark-sql-query.png)

<span data-ttu-id="b78c7-221">hello 다음 쿼리는 단순 하 고, 신속한 **COUNT** 쿼리:</span><span class="sxs-lookup"><span data-stu-id="b78c7-221">hello next query is a simple and fast **COUNT** query:</span></span>

![Spark COUNT 쿼리](./media/spark-connector/spark-count-query.png)

### <a name="group-by-query"></a><span data-ttu-id="b78c7-223">GROUP BY 쿼리</span><span class="sxs-lookup"><span data-stu-id="b78c7-223">GROUP BY query</span></span>
<span data-ttu-id="b78c7-224">다음 집합에서 Azure Cosmos DB 데이터베이스에 대해 **GROUP BY** 쿼리를 쉽게 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-224">In this next set, we can easily run **GROUP BY** queries against our Azure Cosmos DB database:</span></span>

```
select destination, sum(delay) as TotalDelays
from originSEA
group by destination
order by sum(delay) desc limit 10
```

![Spark GROUP BY 쿼리 그래프](./media/spark-connector/group-by-query-graph.png)

### <a name="distinct-order-by-query"></a><span data-ttu-id="b78c7-226">DISTINCT, ORDER BY 쿼리</span><span class="sxs-lookup"><span data-stu-id="b78c7-226">DISTINCT, ORDER BY query</span></span>
<span data-ttu-id="b78c7-227">다음은 **DISTINCT, ORDER BY** 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-227">And here is a **DISTINCT, ORDER BY** query:</span></span>

![Spark GROUP BY 쿼리 그래프](./media/spark-connector/order-by-query.png)

### <a name="continue-hello-flight-data-analysis"></a><span data-ttu-id="b78c7-229">Hello 비행 데이터 분석을 계속</span><span class="sxs-lookup"><span data-stu-id="b78c7-229">Continue hello flight data analysis</span></span>
<span data-ttu-id="b78c7-230">Hello 비행 데이터의 분석 하는 예제 쿼리 toocontinue hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b78c7-230">You can use hello following example queries toocontinue analysis of hello flight data:</span></span>

#### <a name="top-5-delayed-destinations-cities-departing-from-seattle"></a><span data-ttu-id="b78c7-231">시애틀에서 출발하는 상위 5개 지연 대상(도시)</span><span class="sxs-lookup"><span data-stu-id="b78c7-231">Top 5 delayed destinations (cities) departing from Seattle</span></span>
```
select destination, sum(delay)
from originSEA
where delay < 0
group by destination
order by sum(delay) limit 5
```
![Spark 상위 지연 그래프](./media/spark-connector/top-delays-graph.png)


#### <a name="calculate-median-delays-by-destination-cities-departing-from-seattle"></a><span data-ttu-id="b78c7-233">시애틀에서 출발하는 대상 도시별 지연 중앙값 계산</span><span class="sxs-lookup"><span data-stu-id="b78c7-233">Calculate median delays by destination cities departing from Seattle</span></span>
```
select destination, percentile_approx(delay, 0.5) as median_delay
from originSEA
where delay < 0
group by destination
order by percentile_approx(delay, 0.5)
```

![Spark 지연 중앙값 지연 그래프](./media/spark-connector/median-delays-graph.png)

## <a name="next-steps"></a><span data-ttu-id="b78c7-235">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b78c7-235">Next steps</span></span>

<span data-ttu-id="b78c7-236">아직 하지 않는 경우 hello에서 hello Spark tooAzure Cosmos DB 커넥터 다운로드 [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub 리포지토리 hello hello 리포지토리에 있는 추가 리소스를 탐색 및:</span><span class="sxs-lookup"><span data-stu-id="b78c7-236">If you haven't already, download hello Spark tooAzure Cosmos DB connector from hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub repository and explore hello additional resources in hello repo:</span></span>

* <span data-ttu-id="b78c7-237">[분산 집계 예제](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples)(영문)</span><span class="sxs-lookup"><span data-stu-id="b78c7-237">[Distributed Aggregations Examples](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples)</span></span>
* <span data-ttu-id="b78c7-238">[샘플 스크립트 및 노트북](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples)(영문)</span><span class="sxs-lookup"><span data-stu-id="b78c7-238">[Sample Scripts and Notebooks](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples)</span></span>

<span data-ttu-id="b78c7-239">Tooreview hello 수도 [Apache Spark SQL, 프레임, 및 데이터 집합 가이드](http://spark.apache.org/docs/latest/sql-programming-guide.html) 및 hello [Azure HDInsight의 Apache Spark](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="b78c7-239">You might also want tooreview hello [Apache Spark SQL, DataFrames, and Datasets Guide](http://spark.apache.org/docs/latest/sql-programming-guide.html) and hello [Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) article.</span></span>
