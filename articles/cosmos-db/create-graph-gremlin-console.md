---
title: "Azure Cosmos DB 자습서: Apache TinkerPops Gremlin 콘솔에서 만들기, 쿼리하기 및 트래버스 | Microsoft Docs"
description: "Azure Cosmos DB 빠른 시작은 Azure Cosmos DB Graph API를 사용하여 꼭짓점, 에지 및 쿼리를 만듭니다."
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: monicar
ms.assetid: bf08e031-718a-4a2a-89d6-91e12ff8797d
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: terminal
ms.topic: hero-article
ms.date: 07/27/2017
ms.author: denlee
ms.openlocfilehash: fd5cc93ce1ed2a8c7da090666ef539b338ac61c3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-cosmos-db-create-query-and-traverse-a-graph-in-the-gremlin-console"></a><span data-ttu-id="8e311-103">Azure Cosmos DB: Gremlin 콘솔에서 그래프 만들기, 쿼리 및 트래버스</span><span class="sxs-lookup"><span data-stu-id="8e311-103">Azure Cosmos DB: Create, query, and traverse a graph in the Gremlin console</span></span>

<span data-ttu-id="8e311-104">Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="8e311-105">Azure Cosmos DB의 핵심인 전역 배포 및 수평적 크기 조정 기능의 이점을 활용하여 문서, 키/값 및 그래프 데이터베이스를 빠르게 만들고 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="8e311-106">이 빠른 시작에서는 Azure Portal을 사용하여 Azure Cosmos DB 계정, 데이터베이스 및 그래프(컨테이너)를 만들고 [Apache TinkerPop](http://tinkerpop.apache.org)의 [Gremlin 콘솔](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console)을 사용하여 Graph API(미리 보기) 데이터를 사용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-106">This quick start demonstrates how to create an Azure Cosmos DB account, database, and graph (container) using the Azure portal and then use the [Gremlin Console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) from  [Apache TinkerPop](http://tinkerpop.apache.org) to work with Graph API (preview) data.</span></span> <span data-ttu-id="8e311-107">이 자습서에서는 꼭짓점 및 에지를 만들고 쿼리하며, 꼭짓점 속성을 업데이트하고, 꼭짓점을 쿼리하고, 그래프를 트래버스하고, 꼭짓점을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-107">In this tutorial, you create and query vertices and edges, updating a vertex property, query vertices, traverse the graph, and drop a vertex.</span></span>

![Apache Gremlin 콘솔의 Azure Cosmos DB](./media/create-graph-gremlin-console/gremlin-console.png)

<span data-ttu-id="8e311-109">Gremlin 콘솔은 Groovy/Java 기반이며 Linux, Mac 및 Windows에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-109">The Gremlin console is Groovy/Java based and runs on Linux, Mac, and Windows.</span></span> <span data-ttu-id="8e311-110">[Apache TinkerPop 사이트](https://www.apache.org/dyn/closer.lua/tinkerpop/3.2.5/apache-tinkerpop-gremlin-console-3.2.5-bin.zip)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-110">You can download it from the [Apache TinkerPop site](https://www.apache.org/dyn/closer.lua/tinkerpop/3.2.5/apache-tinkerpop-gremlin-console-3.2.5-bin.zip).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e311-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8e311-111">Prerequisites</span></span>

<span data-ttu-id="8e311-112">이 빠른 시작에서 Azure Cosmos DB 계정을 만들려면 Azure 구독이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-112">You need to have an Azure subscription to create an Azure Cosmos DB account for this quickstart.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="8e311-113">또한 [Gremlin 콘솔](http://tinkerpop.apache.org/)을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-113">You also need to install the [Gremlin Console](http://tinkerpop.apache.org/).</span></span> <span data-ttu-id="8e311-114">버전 3.2.5 이상을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-114">Use version 3.2.5 or above.</span></span>

## <a name="create-a-database-account"></a><span data-ttu-id="8e311-115">데이터베이스 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="8e311-115">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="8e311-116">그래프 추가</span><span class="sxs-lookup"><span data-stu-id="8e311-116">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <span data-ttu-id="8e311-117"><a id="ConnectAppService"></a>앱 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="8e311-117"><a id="ConnectAppService"></a>Connect to your app service</span></span>
1. <span data-ttu-id="8e311-118">Gremlin 콘솔을 시작하기 전에 apache-tinkerpop-gremlin-console-3.2.5/conf 디렉터리에서 remote-secure.yaml 구성 파일을 만들거나 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-118">Before starting the Gremlin Console, create or modify the remote-secure.yaml configuration file in the apache-tinkerpop-gremlin-console-3.2.5/conf directory.</span></span>
2. <span data-ttu-id="8e311-119">*호스트*, *포트*, *사용자 이름*, *암호*, *connectionPool* 및 *serializer* 구성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-119">Fill in your *host*, *port*, *username*, *password*, *connectionPool*, and *serializer* configurations:</span></span>

    <span data-ttu-id="8e311-120">설정</span><span class="sxs-lookup"><span data-stu-id="8e311-120">Setting</span></span>|<span data-ttu-id="8e311-121">제안 값</span><span class="sxs-lookup"><span data-stu-id="8e311-121">Suggested value</span></span>|<span data-ttu-id="8e311-122">설명</span><span class="sxs-lookup"><span data-stu-id="8e311-122">Description</span></span>
    ---|---|---
    <span data-ttu-id="8e311-123">호스트</span><span class="sxs-lookup"><span data-stu-id="8e311-123">hosts</span></span>|<span data-ttu-id="8e311-124">[***.graphs.azure.com]</span><span class="sxs-lookup"><span data-stu-id="8e311-124">[***.graphs.azure.com]</span></span>|<span data-ttu-id="8e311-125">아래 스크린샷을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e311-125">See screenshot below.</span></span> <span data-ttu-id="8e311-126">후행 :443/를 제거하고 대괄호로 묶은 Azure Portal의 개요 페이지에서 Gremlin URI 값입니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-126">This is the Gremlin URI value on the Overview page of the Azure portal, in square brackets, with the trailing :443/ removed.</span></span><br><br><span data-ttu-id="8e311-127">https://를 제거하고 문서를 그래프로 변경하고 후행 :443/를 제거하면 URI 값을 사용하여 키 탭에서 이 값을 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-127">This value can also be retrieved from the Keys tab, using the URI value by removing https://, changing documents to graphs, and removing the trailing :443/.</span></span>
    <span data-ttu-id="8e311-128">포트</span><span class="sxs-lookup"><span data-stu-id="8e311-128">port</span></span>|<span data-ttu-id="8e311-129">443</span><span class="sxs-lookup"><span data-stu-id="8e311-129">443</span></span>|<span data-ttu-id="8e311-130">443으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-130">Set to 443.</span></span>
    <span data-ttu-id="8e311-131">username</span><span class="sxs-lookup"><span data-stu-id="8e311-131">username</span></span>|<span data-ttu-id="8e311-132">*사용자 이름*</span><span class="sxs-lookup"><span data-stu-id="8e311-132">*Your username*</span></span>|<span data-ttu-id="8e311-133">`/dbs/<db>/colls/<coll>` 양식의 리소스에서 `<db>`은 데이터베이스 이름이고 `<coll>`은 컬렉션 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-133">The resource of the form `/dbs/<db>/colls/<coll>` where `<db>` is your database name and `<coll>` is your collection name.</span></span>
    <span data-ttu-id="8e311-134">password</span><span class="sxs-lookup"><span data-stu-id="8e311-134">password</span></span>|<span data-ttu-id="8e311-135">*기본 키*</span><span class="sxs-lookup"><span data-stu-id="8e311-135">*Your primary key*</span></span>| <span data-ttu-id="8e311-136">아래에서 두 번째 스크린샷을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e311-136">See second screenshot below.</span></span> <span data-ttu-id="8e311-137">기본 키 상자에 있는 Azure Portal의 키 페이지에서 검색할 수 있는 기본 키입니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-137">This is your primary key, which you can retrieve from the Keys page of the Azure portal, in the Primary Key box.</span></span> <span data-ttu-id="8e311-138">상자의 왼쪽에서 복사 단추를 사용하여 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-138">Use the copy button on the left side of the box to copy the value.</span></span>
    <span data-ttu-id="8e311-139">connectionPool</span><span class="sxs-lookup"><span data-stu-id="8e311-139">connectionPool</span></span>|<span data-ttu-id="8e311-140">{enableSsl: true}</span><span class="sxs-lookup"><span data-stu-id="8e311-140">{enableSsl: true}</span></span>|<span data-ttu-id="8e311-141">SSL에 대한 연결 풀 설정</span><span class="sxs-lookup"><span data-stu-id="8e311-141">Your connection pool setting for SSL.</span></span>
    <span data-ttu-id="8e311-142">직렬 변환기</span><span class="sxs-lookup"><span data-stu-id="8e311-142">serializer</span></span>|<span data-ttu-id="8e311-143">{ className: org.apache.tinkerpop.gremlin.</span><span class="sxs-lookup"><span data-stu-id="8e311-143">{ className: org.apache.tinkerpop.gremlin.</span></span><br><span data-ttu-id="8e311-144">driver.ser.GraphSONMessageSerializerV1d0,</span><span class="sxs-lookup"><span data-stu-id="8e311-144">driver.ser.GraphSONMessageSerializerV1d0,</span></span><br> <span data-ttu-id="8e311-145">config: { serializeResultToString: true }}</span><span class="sxs-lookup"><span data-stu-id="8e311-145">config: { serializeResultToString: true }}</span></span>|<span data-ttu-id="8e311-146">이 값으로 설정하고 값에 붙여 넣을 때 `\n` 줄 바꿈을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-146">Set to this value and delete any `\n` line breaks when pasting in the value.</span></span>

    <span data-ttu-id="8e311-147">호스트 값의 경우 **개요** 페이지의 **Gremlin URI** 값을 복사합니다. ![Azure Portal의 개요 페이지에서 Gremlin URI 값 보기 및 복사](./media/create-graph-gremlin-console/gremlin-uri.png)</span><span class="sxs-lookup"><span data-stu-id="8e311-147">For the hosts value, copy the **Gremlin URI** value from the **Overview** page: ![View and copy the Gremlin URI value on the Overview page in the Azure portal](./media/create-graph-gremlin-console/gremlin-uri.png)</span></span>

    <span data-ttu-id="8e311-148">암호 값의 경우 **키** 페이지의 **기본 키**를 복사합니다. ![Azure Portal의 키 페이지에서 기본 키 보기 및 복사](./media/create-graph-gremlin-console/keys.png)</span><span class="sxs-lookup"><span data-stu-id="8e311-148">For the password value, copy the **Primary key** from the **Keys** page: ![View and copy your primary key in the Azure portal, Keys page](./media/create-graph-gremlin-console/keys.png)</span></span>


3. <span data-ttu-id="8e311-149">터미널에서 `bin/gremlin.bat` 또는 `bin/gremlin.sh`를 실행하여 [Gremlin 콘솔](http://tinkerpop.apache.org/docs/3.2.5/tutorials/getting-started/)을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-149">In your terminal, run `bin/gremlin.bat` or `bin/gremlin.sh` to start the [Gremlin Console](http://tinkerpop.apache.org/docs/3.2.5/tutorials/getting-started/).</span></span>
4. <span data-ttu-id="8e311-150">터미널에서 `:remote connect tinkerpop.server conf/remote-secure.yaml`을 실행하여 앱 서비스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-150">In your terminal, run `:remote connect tinkerpop.server conf/remote-secure.yaml` to connect to your app service.</span></span>

    > [!TIP]
    > <span data-ttu-id="8e311-151">`No appenders could be found for logger` 오류가 발생하면 2단계에 설명된 대로 remote-secure.yaml 파일의 직렬 변환기 값을 업데이트했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-151">If you receive the error `No appenders could be found for logger` ensure that you updated the serializer value in the remote-secure.yaml file as described in step 2.</span></span> 

<span data-ttu-id="8e311-152">잘하셨습니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-152">Great!</span></span> <span data-ttu-id="8e311-153">설정을 완료했으므로 콘솔 명령을 실행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-153">Now that we finished the setup, let's start running some console commands.</span></span>

<span data-ttu-id="8e311-154">간단한 count () 명령을 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-154">Let's try a simple count() command.</span></span> <span data-ttu-id="8e311-155">프롬프트에서 콘솔에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-155">Type the following into the console at the prompt:</span></span>
```
:> g.V().count()
```

> [!TIP]
> <span data-ttu-id="8e311-156">`g.V().count()` 텍스트 앞에 `:>`이 있나요?</span><span class="sxs-lookup"><span data-stu-id="8e311-156">Notice the `:>` that precedes the `g.V().count()` text?</span></span> 
>
> <span data-ttu-id="8e311-157">이는 반드시 입력해야 하는 명령의 일부이며,</span><span class="sxs-lookup"><span data-stu-id="8e311-157">This is part of the command you need to type.</span></span> <span data-ttu-id="8e311-158">Azure Cosmos DB에서 Gremlin 콘솔을 사용할 때 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-158">It is important when using the Gremlin console, with Azure Cosmos DB.</span></span>  
>
> <span data-ttu-id="8e311-159">이 `:>` 접두사를 생략하면 콘솔에서 명령을 로컬로, 종종 메모리 내 그래프에 대해 실행하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-159">Omitting this `:>` prefix instructs the console to execute the command locally, often against an in-memory graph.</span></span>
> <span data-ttu-id="8e311-160">이 `:>`를 사용하면 여기서는 Cosmos DB(localhost 에뮬레이터 또는 > Azure 인스턴스)에 대해 원격 명령을 실행하도록 콘솔에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-160">Using this `:>` tells the console to execute a remote command, in this case against Cosmos DB (either the localhost emulator, or an > Azure instance).</span></span>


## <a name="create-vertices-and-edges"></a><span data-ttu-id="8e311-161">꼭짓점 및 에지 만들기</span><span class="sxs-lookup"><span data-stu-id="8e311-161">Create vertices and edges</span></span>

<span data-ttu-id="8e311-162">*Thomas*, *Mary Kay*, *Robin*, *Ben* 및 *Jack*이라는 5명의 사용자에 대한 꼭짓점을 추가함으로써 시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-162">Let's begin by adding five person vertices for *Thomas*, *Mary Kay*, *Robin*, *Ben*, and *Jack*.</span></span>

<span data-ttu-id="8e311-163">입력(Thomas):</span><span class="sxs-lookup"><span data-stu-id="8e311-163">Input (Thomas):</span></span>

```
:> g.addV('person').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44).property('userid', 1)
```

<span data-ttu-id="8e311-164">출력:</span><span class="sxs-lookup"><span data-stu-id="8e311-164">Output:</span></span>

```
==>[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d,label:person,type:vertex,properties:[firstName:[[id:f02a749f-b67c-4016-850e-910242d68953,value:Thomas]],lastName:[[id:f5fa3126-8818-4fda-88b0-9bb55145ce5c,value:Andersen]],age:[[id:f6390f9c-e563-433e-acbf-25627628016e,value:44]],userid:[[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d|userid,value:1]]]]
```
<span data-ttu-id="8e311-165">입력(Mary Kay):</span><span class="sxs-lookup"><span data-stu-id="8e311-165">Input (Mary Kay):</span></span>

```
:> g.addV('person').property('firstName', 'Mary Kay').property('lastName', 'Andersen').property('age', 39).property('userid', 2)

```

<span data-ttu-id="8e311-166">출력:</span><span class="sxs-lookup"><span data-stu-id="8e311-166">Output:</span></span>

```
==>[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e,label:person,type:vertex,properties:[firstName:[[id:ea0604f8-14ee-4513-a48a-1734a1f28dc0,value:Mary Kay]],lastName:[[id:86d3bba5-fd60-4856-9396-c195ef7d7f4b,value:Andersen]],age:[[id:bc81b78d-30c4-4e03-8f40-50f72eb5f6da,value:39]],userid:[[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e|userid,value:2]]]]

```

<span data-ttu-id="8e311-167">입력(Robin):</span><span class="sxs-lookup"><span data-stu-id="8e311-167">Input (Robin):</span></span>

```
:> g.addV('person').property('firstName', 'Robin').property('lastName', 'Wakefield').property('userid', 3)
```

<span data-ttu-id="8e311-168">출력:</span><span class="sxs-lookup"><span data-stu-id="8e311-168">Output:</span></span>

```
==>[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e,label:person,type:vertex,properties:[firstName:[[id:ec65f078-7a43-4cbe-bc06-e50f2640dc4e,value:Robin]],lastName:[[id:a3937d07-0e88-45d3-a442-26fcdfb042ce,value:Wakefield]],userid:[[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e|userid,value:3]]]]
```

<span data-ttu-id="8e311-169">입력(Ben):</span><span class="sxs-lookup"><span data-stu-id="8e311-169">Input (Ben):</span></span>

```
:> g.addV('person').property('firstName', 'Ben').property('lastName', 'Miller').property('userid', 4)

```

<span data-ttu-id="8e311-170">출력:</span><span class="sxs-lookup"><span data-stu-id="8e311-170">Output:</span></span>

```
==>[id:ee86b670-4d24-4966-9a39-30529284b66f,label:person,type:vertex,properties:[firstName:[[id:a632469b-30fc-4157-840c-b80260871e9a,value:Ben]],lastName:[[id:4a08d307-0719-47c6-84ae-1b0b06630928,value:Miller]],userid:[[id:ee86b670-4d24-4966-9a39-30529284b66f|userid,value:4]]]]
```

<span data-ttu-id="8e311-171">입력(Jack):</span><span class="sxs-lookup"><span data-stu-id="8e311-171">Input (Jack):</span></span>

```
:> g.addV('person').property('firstName', 'Jack').property('lastName', 'Connor').property('userid', 5)
```

<span data-ttu-id="8e311-172">출력:</span><span class="sxs-lookup"><span data-stu-id="8e311-172">Output:</span></span>

```
==>[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469,label:person,type:vertex,properties:[firstName:[[id:4250824e-4b72-417f-af98-8034aa15559f,value:Jack]],lastName:[[id:44c1d5e1-a831-480a-bf94-5167d133549e,value:Connor]],userid:[[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469|userid,value:5]]]]
```


<span data-ttu-id="8e311-173">다음으로, 사용자 간의 관계에 에지를 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-173">Next, let's add edges for relationships between our people.</span></span>

<span data-ttu-id="8e311-174">입력(Thomas -> Mary Kay):</span><span class="sxs-lookup"><span data-stu-id="8e311-174">Input (Thomas -> Mary Kay):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Mary Kay'))
```

<span data-ttu-id="8e311-175">출력:</span><span class="sxs-lookup"><span data-stu-id="8e311-175">Output:</span></span>

```
==>[id:c12bf9fb-96a1-4cb7-a3f8-431e196e702f,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:0d1fa428-780c-49a5-bd3a-a68d96391d5c,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

<span data-ttu-id="8e311-176">입력(Thomas -> Robin):</span><span class="sxs-lookup"><span data-stu-id="8e311-176">Input (Thomas -> Robin):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Robin'))
```

<span data-ttu-id="8e311-177">출력:</span><span class="sxs-lookup"><span data-stu-id="8e311-177">Output:</span></span>

```
==>[id:58319bdd-1d3e-4f17-a106-0ddf18719d15,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:3e324073-ccfc-4ae1-8675-d450858ca116,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

<span data-ttu-id="8e311-178">입력(Robin -> Ben):</span><span class="sxs-lookup"><span data-stu-id="8e311-178">Input (Robin -> Ben):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Robin').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Ben'))
```

<span data-ttu-id="8e311-179">출력:</span><span class="sxs-lookup"><span data-stu-id="8e311-179">Output:</span></span>

```
==>[id:889c4d3c-549e-4d35-bc21-a3d1bfa11e00,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:40fd641d-546e-412a-abcc-58fe53891aab,outV:3e324073-ccfc-4ae1-8675-d450858ca116]
```

## <a name="update-a-vertex"></a><span data-ttu-id="8e311-180">꼭짓점 업데이트</span><span class="sxs-lookup"><span data-stu-id="8e311-180">Update a vertex</span></span>

<span data-ttu-id="8e311-181">*45*세라는 나이로 *Thomas* 꼭짓점을 업데이트하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-181">Let's update the *Thomas* vertex with a new age of *45*.</span></span>

<span data-ttu-id="8e311-182">입력:</span><span class="sxs-lookup"><span data-stu-id="8e311-182">Input:</span></span>
```
:> g.V().hasLabel('person').has('firstName', 'Thomas').property('age', 45)
```
<span data-ttu-id="8e311-183">출력:</span><span class="sxs-lookup"><span data-stu-id="8e311-183">Output:</span></span>

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

## <a name="query-your-graph"></a><span data-ttu-id="8e311-184">그래프 쿼리</span><span class="sxs-lookup"><span data-stu-id="8e311-184">Query your graph</span></span>

<span data-ttu-id="8e311-185">이제 그래프에 대한 다양한 쿼리를 실행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-185">Now, let's run a variety of queries against your graph.</span></span>

<span data-ttu-id="8e311-186">먼저 40세 이상인 사용자만을 반환하는 필터가 포함된 쿼리를 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-186">First, let's try a query with a filter to return only people who are older than 40 years old.</span></span>

<span data-ttu-id="8e311-187">입력(필터 쿼리):</span><span class="sxs-lookup"><span data-stu-id="8e311-187">Input (filter query):</span></span>

```
:> g.V().hasLabel('person').has('age', gt(40))
```

<span data-ttu-id="8e311-188">출력:</span><span class="sxs-lookup"><span data-stu-id="8e311-188">Output:</span></span>

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

<span data-ttu-id="8e311-189">다음으로, 40세 이상인 사용자의 이름을 프로젝트하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-189">Next, let's project the first name for the people who are older than 40 years old.</span></span>

<span data-ttu-id="8e311-190">입력(필터 + 프로젝션 쿼리):</span><span class="sxs-lookup"><span data-stu-id="8e311-190">Input (filter + projection query):</span></span>

```
:> g.V().hasLabel('person').has('age', gt(40)).values('firstName')
```

<span data-ttu-id="8e311-191">출력:</span><span class="sxs-lookup"><span data-stu-id="8e311-191">Output:</span></span>

```
==>Thomas
```

## <a name="traverse-your-graph"></a><span data-ttu-id="8e311-192">그래프 트래버스</span><span class="sxs-lookup"><span data-stu-id="8e311-192">Traverse your graph</span></span>

<span data-ttu-id="8e311-193">Thomas의 친구를 모두 반환하는 그래프를 트래버스하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-193">Let's traverse the graph to return all of Thomas's friends.</span></span>

<span data-ttu-id="8e311-194">입력(Thomas의 친구):</span><span class="sxs-lookup"><span data-stu-id="8e311-194">Input (friends of Thomas):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="8e311-195">출력:</span><span class="sxs-lookup"><span data-stu-id="8e311-195">Output:</span></span> 

```
==>[id:f04bc00b-cb56-46c4-a3bb-a5870c42f7ff,label:person,type:vertex,properties:[firstName:[[id:14feedec-b070-444e-b544-62be15c7167c,value:Mary Kay]],lastName:[[id:107ab421-7208-45d4-b969-bbc54481992a,value:Andersen]],age:[[id:4b08d6e4-58f5-45df-8e69-6b790b692e0a,value:39]]]]
==>[id:91605c63-4988-4b60-9a30-5144719ae326,label:person,type:vertex,properties:[firstName:[[id:f760e0e6-652a-481a-92b0-1767d9bf372e,value:Robin]],lastName:[[id:352a4caa-bad6-47e3-a7dc-90ff342cf870,value:Wakefield]]]]
```

<span data-ttu-id="8e311-196">다음으로 꼭짓점 다음 계층을 가져와 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-196">Next, let's get the next layer of vertices.</span></span> <span data-ttu-id="8e311-197">Thomas의 친구의 친구를 모두 반환하는 그래프를 트래버스합니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-197">Traverse the graph to return all the friends of Thomas's friends.</span></span>

<span data-ttu-id="8e311-198">입력(Thomas의 친구의 친구):</span><span class="sxs-lookup"><span data-stu-id="8e311-198">Input (friends of friends of Thomas):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```
<span data-ttu-id="8e311-199">출력:</span><span class="sxs-lookup"><span data-stu-id="8e311-199">Output:</span></span>

```
==>[id:a801a0cb-ee85-44ee-a502-271685ef212e,label:person,type:vertex,properties:[firstName:[[id:b9489902-d29a-4673-8c09-c2b3fe7f8b94,value:Ben]],lastName:[[id:e084f933-9a4b-4dbc-8273-f0171265cf1d,value:Miller]]]]
```

## <a name="drop-a-vertex"></a><span data-ttu-id="8e311-200">꼭짓점 삭제</span><span class="sxs-lookup"><span data-stu-id="8e311-200">Drop a vertex</span></span>

<span data-ttu-id="8e311-201">이제 그래프 데이터베이스에서 꼭짓점을 삭제하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-201">Let's now delete a vertex from the graph database.</span></span>

<span data-ttu-id="8e311-202">입력(Jack 꼭짓점 삭제):</span><span class="sxs-lookup"><span data-stu-id="8e311-202">Input (drop Jack vertex):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Jack').drop()
```

## <a name="clear-your-graph"></a><span data-ttu-id="8e311-203">그래프 정리</span><span class="sxs-lookup"><span data-stu-id="8e311-203">Clear your graph</span></span>

<span data-ttu-id="8e311-204">마지막으로 모든 꼭짓점 및 에지의 데이터베이스를 정리해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-204">Finally, let's clear the database of all vertices and edges.</span></span>

<span data-ttu-id="8e311-205">입력:</span><span class="sxs-lookup"><span data-stu-id="8e311-205">Input:</span></span>

```
:> g.E().drop()
:> g.V().drop()
```

<span data-ttu-id="8e311-206">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-206">Congratulations!</span></span> <span data-ttu-id="8e311-207">이 Azure Cosmos DB: Graph API 자습서를 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-207">You've completed this Azure Cosmos DB: Graph API tutorial!</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="8e311-208">Azure Portal에서 SLA 검토</span><span class="sxs-lookup"><span data-stu-id="8e311-208">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="8e311-209">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="8e311-209">Clean up resources</span></span>

<span data-ttu-id="8e311-210">이 앱을 계속 사용하지 않으려면 Azure Portal에서 다음 단계에 따라 이 빠른 시작에서 만든 리소스를 모두 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-210">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>  

1. <span data-ttu-id="8e311-211">Azure Portal의 왼쪽 메뉴에서 **리소스 그룹**을 클릭한 다음 만든 리소스의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-211">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="8e311-212">리소스 그룹 페이지에서 **삭제**를 클릭하고 텍스트 상자에서 삭제할 리소스의 이름을 입력한 다음 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-212">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e311-213">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8e311-213">Next steps</span></span>

<span data-ttu-id="8e311-214">이 빠른 시작에서는 Cosmos DB Azure 계정을 만들고, 데이터 탐색기를 사용하여 그래프를 만들고, 꼭짓점과 에지를 만들고, Gremlin 콘솔을 사용하여 그래프를 트래버스하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-214">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a graph using the Data Explorer, create vertices and edges, and traverse your graph using the Gremlin console.</span></span> <span data-ttu-id="8e311-215">이제 Gremlin을 사용하여 더 복잡한 쿼리를 작성하고 강력한 그래프 순회 논리를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e311-215">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="8e311-216">Gremlin을 사용하여 쿼리</span><span class="sxs-lookup"><span data-stu-id="8e311-216">Query using Gremlin</span></span>](tutorial-query-graph.md)
