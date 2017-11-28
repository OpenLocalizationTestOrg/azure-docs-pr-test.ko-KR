---
title: "Azure Cosmos DB에 대한 서버 쪽 JavaScript 프로그래밍 | Microsoft Docs"
description: "Azure Cosmos DB를 사용하여 JavaScript에서 저장 프로시저, 데이터베이스 트리거 및 UDF(사용자 정의 함수)를 작성하는 방법을 알아봅니다. 데이터베이스 프로그래밍 팁 등을 가져옵니다."
keywords: "데이터베이스 트리거, 저장된 프로시저, 저장된 프로시저, 데이터베이스 프로그램, sproc, documentdb, azure, Microsoft azure"
services: cosmos-db
documentationcenter: 
author: aliuy
manager: jhubbard
editor: mimig
ms.assetid: 0fba7ebd-a4fc-4253-a786-97f1354fbf17
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: andrl
ms.openlocfilehash: 8cddc7a8c9aa677b9c93bee3a7e05c226cc1f655
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a><span data-ttu-id="5df7f-105">Azure Cosmos DB 서버 쪽 프로그래밍: 저장 프로시저, 데이터베이스 트리거 및 UDF</span><span class="sxs-lookup"><span data-stu-id="5df7f-105">Azure Cosmos DB server-side programming: Stored procedures, database triggers, and UDFs</span></span>
<span data-ttu-id="5df7f-106">Azure Cosmos DB가 언어 통합 트랜잭션 방식으로 JavaScript를 실행하므로 개발자가 기본적으로 [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript로 **저장 프로시저**, **트리거** 및 **UDF(사용자 정의 함수)**를 작성할 수 있는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-106">Learn how Azure Cosmos DB’s language integrated, transactional execution of JavaScript lets developers write **stored procedures**, **triggers** and **user defined functions (UDFs)** natively in an [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span></span> <span data-ttu-id="5df7f-107">이 경우 사용자가 데이터베이스 저장소 파티션에 직접 전달되고 실행될 수 있는 데이터베이스 프로그램 응용 프로그램 논리를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-107">This allows you to write database program application logic that can be shipped and executed directly on the database storage partitions.</span></span> 

<span data-ttu-id="5df7f-108">먼저 Andrew Liu가 Cosmos DB의 서버 쪽 데이터베이스 프로그래밍 모델을 간략하게 설명하는 다음 동영상을 보는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-108">We recommend getting started by watching the following video, where Andrew Liu provides a brief introduction to Cosmos DB's server-side database programming model.</span></span> 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

<span data-ttu-id="5df7f-109">그런 다음 이 문서로 돌아와서 다음 내용을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="5df7f-109">Then, return to this article, where you'll learn the answers to the following questions:</span></span>  

* <span data-ttu-id="5df7f-110">JavaScript를 사용해서 저장 프로시저, 트리거 또는 UDF를 작성하는 방법은 무엇인가?</span><span class="sxs-lookup"><span data-stu-id="5df7f-110">How do I write a a stored procedure, trigger, or UDF using JavaScript?</span></span>
* <span data-ttu-id="5df7f-111">Cosmos DB는 ACID를 어떻게 보장하나요?</span><span class="sxs-lookup"><span data-stu-id="5df7f-111">How does Cosmos DB guarantee ACID?</span></span>
* <span data-ttu-id="5df7f-112">Cosmos DB에서 트랜잭션이 어떻게 작동하나요?</span><span class="sxs-lookup"><span data-stu-id="5df7f-112">How do transactions work in Cosmos DB?</span></span>
* <span data-ttu-id="5df7f-113">사전 트리거 및 사후 트리거는 무엇이고 어떻게 작성하는가?</span><span class="sxs-lookup"><span data-stu-id="5df7f-113">What are pre-triggers and post-triggers and how do I write one?</span></span>
* <span data-ttu-id="5df7f-114">HTTP를 사용해서 RESTful 방식으로 저장 프로시저, 트리거 또는 UDF를 등록하고 실행하는 방법은 무엇인가?</span><span class="sxs-lookup"><span data-stu-id="5df7f-114">How do I register and execute a stored procedure, trigger, or UDF in a RESTful manner by using HTTP?</span></span>
* <span data-ttu-id="5df7f-115">저장 프로시저, 트리거 및 UDF를 생성 및 실행하기 위해 사용할 수 있는 Cosmos DB SDK는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="5df7f-115">What Cosmos DB SDKs are available to create and execute stored procedures, triggers, and UDFs?</span></span>

## <a name="introduction-to-stored-procedure-and-udf-programming"></a><span data-ttu-id="5df7f-116">저장 프로시저 및 UDF 프로그래밍 소개</span><span class="sxs-lookup"><span data-stu-id="5df7f-116">Introduction to Stored Procedure and UDF Programming</span></span>
<span data-ttu-id="5df7f-117">이 *"최신 T-SQL로서의 JavaScript"* 접근 방법을 통해 응용 프로그램 개발자는 형식 시스템 불일치 및 개체-관계형 매핑 기술의 복잡성을 벗어날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-117">This approach of *“JavaScript as a modern day T-SQL”* frees application developers from the complexities of type system mismatches and object-relational mapping technologies.</span></span> <span data-ttu-id="5df7f-118">또한 풍부한 응용 프로그램을 작성하기 위해 활용할 수 있는 내재된 많은 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-118">It also has a number of intrinsic advantages that can be utilized to build rich applications:</span></span>  

* <span data-ttu-id="5df7f-119">**절차적 논리:** 고급 프로그래밍 언어인 JavaScript는 비즈니스 논리를 노출하는 풍부하고 익숙한 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-119">**Procedural Logic:** JavaScript as a high level programming language, provides a rich and familiar interface to express business logic.</span></span> <span data-ttu-id="5df7f-120">데이터에 더 가까운 복잡한 작업 시퀀스를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-120">You can perform complex sequences of operations closer to the data.</span></span>
* <span data-ttu-id="5df7f-121">**원자성 트랜잭션:** Cosmos DB는 단일 저장 프로시저 또는 트리거 내에서 수행되는 데이터베이스 작업의 원자성을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-121">**Atomic Transactions:** Cosmos DB guarantees that database operations performed inside a single stored procedure or trigger are atomic.</span></span> <span data-ttu-id="5df7f-122">따라서 응용 프로그램이 관련 작업을 단일 배치로 결합하여 모두 성공하거나 모두 실패하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-122">This lets an application combine related operations in a single batch so that either all of them succeed or none of them succeed.</span></span> 
* <span data-ttu-id="5df7f-123">**성능:** JSON은 본질적으로 Javascript 언어 형식 시스템에 매핑되고 Cosmos DB의 기본 저장소 단위이기도 하므로 버퍼 풀에서 JSON 문서의 지연 구체화와 같은 많은 최적화를 수행할 수 있으며 요청 시 실행 코드에서 JSON 문서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-123">**Performance:** The fact that JSON is intrinsically mapped to the Javascript language type system and is also the basic unit of storage in Cosmos DB allows for a number of optimizations like lazy materialization of JSON documents in the buffer pool and making them available on-demand to the executing code.</span></span> <span data-ttu-id="5df7f-124">데이터베이스에 비즈니스 논리를 전달할 경우 다음과 같은 추가 성능 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-124">There are more performance benefits associated with shipping business logic to the database:</span></span>
  
  * <span data-ttu-id="5df7f-125">일괄 처리 – 개발자가 삽입 등의 작업을 그룹화하여 대량 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-125">Batching – Developers can group operations like inserts and submit them in bulk.</span></span> <span data-ttu-id="5df7f-126">개별 트랜잭션을 만들기 위한 네트워크 트래픽 지연 비용 및 저장소 오버헤드가 크게 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-126">The network traffic latency cost and the store overhead to create separate transactions are reduced significantly.</span></span> 
  * <span data-ttu-id="5df7f-127">사전 컴파일 – Cosmos DB는 각 호출의 JavaScript 컴파일 비용을 방지하기 위해 저장 프로시저, 트리거 및 UDF(사용자 정의 함수)를 사전 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-127">Pre-compilation – Cosmos DB precompiles stored procedures, triggers and user defined functions (UDFs) to avoid JavaScript compilation cost for each invocation.</span></span> <span data-ttu-id="5df7f-128">절차적 논리의 바이트 코드 작성 오버헤드가 최소값으로 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-128">The overhead of building the byte code for the procedural logic is amortized to a minimal value.</span></span>
  * <span data-ttu-id="5df7f-129">시퀀싱 – 보조 저장소 작업을 하나 또는 많이 수행하는 파생 작업("트리거")이 필요한 작업이 많습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-129">Sequencing – Many operations need a side-effect (“trigger”) that potentially involves doing one or many secondary store operations.</span></span> <span data-ttu-id="5df7f-130">원자성뿐 아니라 이 특성도 서버로 이동할 경우 성능이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-130">Aside from atomicity, this is more performant when moved to the server.</span></span> 
* <span data-ttu-id="5df7f-131">**캡슐화:** 저장 프로시저를 사용하여 비즈니스 논리를 단일 장소에 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-131">**Encapsulation:** Stored procedures can be used to group business logic in one place.</span></span> <span data-ttu-id="5df7f-132">다음 두 가지 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-132">This has two advantages:</span></span>
  * <span data-ttu-id="5df7f-133">원시 데이터 위에 추상 계층이 추가되므로 데이터 설계자가 데이터와 독립적으로 응용 프로그램을 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-133">It adds an abstraction layer on top of the raw data, which enables data architects to evolve their applications independently from the data.</span></span> <span data-ttu-id="5df7f-134">데이터를 직접 처리해야 할 경우 응용 프로그램에 포함되어야 할 수 있는 가정으로 인해 데이터에 스키마가 사용되지 않을 경우 이러한 장점은 특히 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-134">This is particularly advantageous when the data is schema-less, due to the brittle assumptions that may need to be baked into the application if they have to deal with data directly.</span></span>  
  * <span data-ttu-id="5df7f-135">이 추상화는 스크립트에서의 액세스를 간소화하여 기업이 데이터 보안을 유지할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-135">This abstraction lets enterprises keep their data secure by streamlining the access from the scripts.</span></span>  

<span data-ttu-id="5df7f-136">데이터베이스 트리거, 저장 프로시저 및 사용자 지정 쿼리 연산자의 만들기 및 실행은 .NET, Node.js 및 JavaScript를 비롯한 많은 플랫폼의 [REST API](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases) 및 [클라이언트 SDK](documentdb-sdk-dotnet.md)를 통해 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-136">The creation and execution of database triggers, stored procedure and custom query operators is supported through the [REST API](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), and [client SDKs](documentdb-sdk-dotnet.md) in many platforms including .NET, Node.js and JavaScript.</span></span>

<span data-ttu-id="5df7f-137">이 자습서에서는 [Q Promise와 함께 Node.js SDK](http://azure.github.io/azure-documentdb-node-q/)를 사용하여 저장 프로시저, 트리거 및 UDF의 구문 및 사용법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-137">This tutorial uses the [Node.js SDK with Q Promises](http://azure.github.io/azure-documentdb-node-q/) to illustrate syntax and usage of stored procedures, triggers, and UDFs.</span></span>   

## <a name="stored-procedures"></a><span data-ttu-id="5df7f-138">저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="5df7f-138">Stored procedures</span></span>
### <a name="example-write-a-simple-stored-procedure"></a><span data-ttu-id="5df7f-139">예: 간단한 저장 프로시저 작성</span><span class="sxs-lookup"><span data-stu-id="5df7f-139">Example: Write a simple stored procedure</span></span>
<span data-ttu-id="5df7f-140">먼저 "Hello World" 응답을 반환하는 단순한 저장 프로시저로 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-140">Let’s start with a simple stored procedure that returns a “Hello World” response.</span></span>

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


<span data-ttu-id="5df7f-141">저장 프로시저는 컬렉션당 등록되며 해당 컬렉션에 있는 모든 문서 및 첨부 파일에 대해 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-141">Stored procedures are registered per collection, and can operate on any document and attachment present in that collection.</span></span> <span data-ttu-id="5df7f-142">다음 조각은 helloWorld 저장 프로시저를 컬렉션에 등록하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-142">The following snippet shows how to register the helloWorld stored procedure with a collection.</span></span> 

    // register the stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


<span data-ttu-id="5df7f-143">저장 프로시저가 등록되면 컬렉션에 대해 실행하고 클라이언트에서 결과를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-143">Once the stored procedure is registered, we can execute it against the collection, and read the results back at the client.</span></span> 

    // execute the stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


<span data-ttu-id="5df7f-144">컨텍스트 개체는 Cosmos DB 저장소에서 수행할 수 있는 모든 작업에 대한 액세스와 요청 및 응답 개체에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-144">The context object provides access to all operations that can be performed on Cosmos DB storage, as well as access to the request and response objects.</span></span> <span data-ttu-id="5df7f-145">여기서는 응답 개체를 사용하여 클라이언트로 전송되는 응답의 본문을 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-145">In this case, we used the response object to set the body of the response that was sent back to the client.</span></span> <span data-ttu-id="5df7f-146">자세한 내용은 [Azure Cosmos DB JavaScript 서버 SDK 설명서](http://azure.github.io/azure-documentdb-js-server/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5df7f-146">For more details, refer to the [Azure Cosmos DB JavaScript server SDK documentation](http://azure.github.io/azure-documentdb-js-server/).</span></span>  

<span data-ttu-id="5df7f-147">이 예제를 확장하여 저장 프로시저에 데이터베이스 관련 기능을 더 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-147">Let us expand on this example and add more database related functionality to the stored procedure.</span></span> <span data-ttu-id="5df7f-148">저장 프로시저는 컬렉션 내의 문서와 첨부 파일을 만들고 업데이트하고 읽고 쿼리 및 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-148">Stored procedures can create, update, read, query and delete documents and attachments inside the collection.</span></span>    

### <a name="example-write-a-stored-procedure-to-create-a-document"></a><span data-ttu-id="5df7f-149">예: 문서 작성을 위한 저장 프로시저 작성</span><span class="sxs-lookup"><span data-stu-id="5df7f-149">Example: Write a stored procedure to create a document</span></span>
<span data-ttu-id="5df7f-150">다음 코드 조각에서는 컨텍스트 개체를 사용하여 Cosmos DB 리소스를 조작하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-150">The next snippet shows how to use the context object to interact with Cosmos DB resources.</span></span>

    var createDocumentStoredProc = {
        id: "createMyDocument",
        serverScript: function createMyDocument(documentToCreate) {
            var context = getContext();
            var collection = context.getCollection();

            var accepted = collection.createDocument(collection.getSelfLink(),
                  documentToCreate,
                  function (err, documentCreated) {
                      if (err) throw new Error('Error' + err.message);
                      context.getResponse().setBody(documentCreated.id)
                  });
            if (!accepted) return;
        }
    }


<span data-ttu-id="5df7f-151">이 저장 프로시저는 현재 컬렉션에 만들 문서의 본문을 입력 documentToCreate로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-151">This stored procedure takes as input documentToCreate, the body of a document to be created in the current collection.</span></span> <span data-ttu-id="5df7f-152">이러한 모든 작업은 비동기이며 JavaScript 함수 콜백에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-152">All such operations are asynchronous and depend on JavaScript function callbacks.</span></span> <span data-ttu-id="5df7f-153">콜백 함수에는 작업이 실패할 경우의 오류 개체 및 만들어진 개체에 각각 사용되는 두 개의 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-153">The callback function has two parameters, one for the error object in case the operation fails, and one for the created object.</span></span> <span data-ttu-id="5df7f-154">콜백 내에서 사용자는 예외를 처리하거나 오류를 throw할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-154">Inside the callback, users can either handle the exception or throw an error.</span></span> <span data-ttu-id="5df7f-155">콜백이 제공되지 않았고 오류가 있는 경우, Azure Cosmos DB 런타임에서 오류를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-155">In case a callback is not provided and there is an error, the Azure Cosmos DB runtime throws an error.</span></span>   

<span data-ttu-id="5df7f-156">위 예제에서 콜백은 작업이 실패한 경우에 오류를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-156">In the example above, the callback throws an error if the operation failed.</span></span> <span data-ttu-id="5df7f-157">그렇지 않으면 만들어진 문서의 ID를 클라이언트에 반환되는 응답의 본문으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-157">Otherwise, it sets the id of the created document as the body of the response to the client.</span></span> <span data-ttu-id="5df7f-158">다음은 이 저장 프로시저가 입력 매개 변수를 사용하여 실행되는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-158">Here is how this stored procedure is executed with input parameters.</span></span>

    // register the stored procedure
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', createDocumentStoredProc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;

            // run stored procedure to create a document
            var docToCreate = {
                id: "DocFromSproc",
                book: "The Hitchhiker’s Guide to the Galaxy",
                author: "Douglas Adams"
            };

            return client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/createMyDocument',
                  docToCreate);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response); // "DocFromSproc"
    }, function (error) {
        console.log("Error", error);
    });


<span data-ttu-id="5df7f-159">문서 본문 배열을 입력으로 사용하고 여러 네트워크 요청을 통해 각각 개별적으로 만드는 대신 동일한 저장 프로시저 실행에서 모두 만들도록 이 저장 프로시저를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-159">Note that this stored procedure can be modified to take an array of document bodies as input and create them all in the same stored procedure execution instead of multiple network requests to create each of them individually.</span></span> <span data-ttu-id="5df7f-160">이 저장 프로시저를 사용하여 Cosmos DB에 대한 효율적인 대량 가져오기를 구현할 수 있습니다(이 자습서의 뒷부분에서 설명).</span><span class="sxs-lookup"><span data-stu-id="5df7f-160">This can be used to implement an efficient bulk importer for Cosmos DB (discussed later in this tutorial).</span></span>   

<span data-ttu-id="5df7f-161">설명한 예제에서는 저장 프로시저를 사용하는 방법을 보여 주었습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-161">The example described demonstrated how to use stored procedures.</span></span> <span data-ttu-id="5df7f-162">트리거와 UDF(사용자 정의 함수)는 자습서의 뒷부분에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-162">We will cover triggers and user defined functions (UDFs) later in the tutorial.</span></span>

## <a name="database-program-transactions"></a><span data-ttu-id="5df7f-163">데이터베이스 프로그램 트랜잭션</span><span class="sxs-lookup"><span data-stu-id="5df7f-163">Database program transactions</span></span>
<span data-ttu-id="5df7f-164">일반적인 데이터베이스의 트랜잭션은 하나의 논리적 작업 단위로 수행되는 작업 시퀀스로 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-164">Transaction in a typical database can be defined as a sequence of operations performed as a single logical unit of work.</span></span> <span data-ttu-id="5df7f-165">각 트랜잭션에서 **ACID 보장**을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-165">Each transaction provides **ACID guarantees**.</span></span> <span data-ttu-id="5df7f-166">ACID는 원자성, 일관성, 격리 및 내구성의 네 가지 속성을 나타내는 잘 알려진 머리글자어입니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-166">ACID is a well-known acronym that stands for four properties -  Atomicity, Consistency, Isolation and Durability.</span></span>  

<span data-ttu-id="5df7f-167">간단히 설명하면, 원자성은 트랜잭션 내부에서 수행된 모든 작업이 하나의 단위로 처리되어 모두 커밋되거나 커밋되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-167">Briefly, atomicity guarantees that all the work done inside a transaction is treated as a single unit where either all of it is committed or none.</span></span> <span data-ttu-id="5df7f-168">일관성은 데이터가 트랜잭션 간에 항상 양호한 내부 상태로 유지되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-168">Consistency makes sure that the data is always in a good internal state across transactions.</span></span> <span data-ttu-id="5df7f-169">격리는 두 트랜잭션이 서로를 방해하지 않도록 합니다. 일반적으로 대부분의 상용 시스템은 응용 프로그램 요구에 따라 사용할 수 있는 여러 격리 수준을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-169">Isolation guarantees that no two transactions interfere with each other – generally, most commercial systems provide multiple isolation levels that can be used based on the application needs.</span></span> <span data-ttu-id="5df7f-170">내구성은 데이터베이스에서 커밋된 변경 내용이 항상 유지되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-170">Durability ensures that any change that’s committed in the database will always be present.</span></span>   

<span data-ttu-id="5df7f-171">Cosmos DB에서 JavaScript는 데이터베이스와 동일한 메모리 공간에 호스트됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-171">In Cosmos DB, JavaScript is hosted in the same memory space as the database.</span></span> <span data-ttu-id="5df7f-172">따라서 저장 프로시저 및 트리거 내에서 수행된 요청이 동일한 데이터베이스 세션 범위에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-172">Hence, requests made within stored procedures and triggers execute in the same scope of a database session.</span></span> <span data-ttu-id="5df7f-173">이렇게 하면 Cosmos DB에서 단일 저장 프로시저/트리거에 속하는 모든 작업에 대해 ACID를 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-173">This enables Cosmos DB to guarantee ACID for all operations that are part of a single stored procedure/trigger.</span></span> <span data-ttu-id="5df7f-174">다음 저장 프로시저 정의를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="5df7f-174">Consider the following stored procedure definition:</span></span>

    // JavaScript source code
    var exchangeItemsSproc = {
        id: "exchangeItems",
        serverScript: function (playerId1, playerId2) {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            var player1Document, player2Document;

            // query for players
            var filterQuery = 'SELECT * FROM Players p where p.id  = "' + playerId1 + '"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery, {},
                function (err, documents, responseOptions) {
                    if (err) throw new Error("Error" + err.message);

                    if (documents.length != 1) throw "Unable to find both names";
                    player1Document = documents[0];

                    var filterQuery2 = 'SELECT * FROM Players p where p.id = "' + playerId2 + '"';
                    var accept2 = collection.queryDocuments(collection.getSelfLink(), filterQuery2, {},
                        function (err2, documents2, responseOptions2) {
                            if (err2) throw new Error("Error" + err2.message);
                            if (documents2.length != 1) throw "Unable to find both names";
                            player2Document = documents2[0];
                            swapItems(player1Document, player2Document);
                            return;
                        });
                    if (!accept2) throw "Unable to read player details, abort ";
                });

            if (!accept) throw "Unable to read player details, abort ";

            // swap the two players’ items
            function swapItems(player1, player2) {
                var player1ItemSave = player1.item;
                player1.item = player2.item;
                player2.item = player1ItemSave;

                var accept = collection.replaceDocument(player1._self, player1,
                    function (err, docReplaced) {
                        if (err) throw "Unable to update player 1, abort ";

                        var accept2 = collection.replaceDocument(player2._self, player2,
                            function (err2, docReplaced2) {
                                if (err) throw "Unable to update player 2, abort"
                            });

                        if (!accept2) throw "Unable to update player 2, abort";
                    });

                if (!accept) throw "Unable to update player 1, abort";
            }
        }
    }

    // register the stored procedure in Node.js client
    client.createStoredProcedureAsync(collection._self, exchangeItemsSproc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;
        }
    );

<span data-ttu-id="5df7f-175">이 저장 프로시저는 게임 앱 내의 트랜잭션을 사용하여 단일 작업으로 두 플레이어 간에 항목을 교환합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-175">This stored procedure uses transactions within a gaming app to trade items between two players in a single operation.</span></span> <span data-ttu-id="5df7f-176">저장 프로시저는 각각 인수로 전달된 플레이어 ID에 해당하는 두 개의 문서를 읽으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-176">The stored procedure attempts to read two documents each corresponding to the player IDs passed in as an argument.</span></span> <span data-ttu-id="5df7f-177">두 플레이어 문서가 모두 있으면 저장 프로시저가 항목을 교환하여 문서를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-177">If both player documents are found, then the stored procedure updates the documents by swapping their items.</span></span> <span data-ttu-id="5df7f-178">이 과정에서 오류가 발생할 경우 JavaScript 예외가 발생하여 암시적으로 트랜잭션이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-178">If any errors are encountered along the way, it throws a JavaScript exception that implicitly aborts the transaction.</span></span>

<span data-ttu-id="5df7f-179">저장 프로시저가 등록된 컬렉션이 단일 파티션 컬렉션인 경우 트랜잭션은 해당 컬렉션 내의 모든 문서로 범위가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-179">If the collection the stored procedure is registered against is a single-partition collection, then the transaction is scoped to all the documents within the collection.</span></span> <span data-ttu-id="5df7f-180">컬렉션이 분할된 경우 저장 프로시저는 단일 파티션 키의 트랜잭션 범위에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-180">If the collection is partitioned, then stored procedures are executed in the transaction scope of a single partition key.</span></span> <span data-ttu-id="5df7f-181">이 경우 각 저장 프로시저 실행에는 트랜잭션이 실행되는 범위에 해당하는 파티션 키 값이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-181">Each stored procedure execution must then include a partition key value corresponding to the scope the transaction must run under.</span></span> <span data-ttu-id="5df7f-182">자세한 내용은 [Azure Cosmos DB 분할](partition-data.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5df7f-182">For more details, see [Azure Cosmos DB Partitioning](partition-data.md).</span></span>

### <a name="commit-and-rollback"></a><span data-ttu-id="5df7f-183">커밋 및 롤백</span><span class="sxs-lookup"><span data-stu-id="5df7f-183">Commit and rollback</span></span>
<span data-ttu-id="5df7f-184">트랜잭션은 기본적으로 Cosmos DB의 JavaScript 프로그래밍 모델에 전체 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-184">Transactions are deeply and natively integrated into Cosmos DB’s JavaScript programming model.</span></span> <span data-ttu-id="5df7f-185">JavaScript 함수 내부에서 모든 작업은 자동으로 단일 트랜잭션 아래에 래핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-185">Inside a JavaScript function, all operations are automatically wrapped under a single transaction.</span></span> <span data-ttu-id="5df7f-186">JavaScript가 예외 없이 완료되면 데이터베이스에 대한 작업이 커밋됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-186">If the JavaScript completes without any exception, the operations to the database are committed.</span></span> <span data-ttu-id="5df7f-187">실제로 관계형 데이터베이스의 "BEGIN TRANSACTION" 및 "COMMIT TRANSACTION" 문은 Cosmos DB에서 암시적입니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-187">In effect, the “BEGIN TRANSACTION” and “COMMIT TRANSACTION” statements in relational databases are implicit in Cosmos DB.</span></span>  

<span data-ttu-id="5df7f-188">스크립트에서 전파된 예외가 있을 경우 Cosmos DB의 JavaScript 런타임이 전체 트랜잭션을 롤백합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-188">If there is any exception that’s propagated from the script, Cosmos DB’s JavaScript runtime will roll back the whole transaction.</span></span> <span data-ttu-id="5df7f-189">앞의 예제에 표시된 대로, 예외 throw는 Cosmos DB의 "ROLLBACK TRANSACTION"과 동등합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-189">As shown in the earlier example, throwing an exception is effectively equivalent to a “ROLLBACK TRANSACTION” in Cosmos DB.</span></span>

### <a name="data-consistency"></a><span data-ttu-id="5df7f-190">데이터 일관성</span><span class="sxs-lookup"><span data-stu-id="5df7f-190">Data consistency</span></span>
<span data-ttu-id="5df7f-191">저장 프로시저와 트리거는 항상 Azure Cosmos DB 컨테이너의 주 복제본에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-191">Stored procedures and triggers are always executed on the primary replica of the Azure Cosmos DB container.</span></span> <span data-ttu-id="5df7f-192">이렇게 하면 저장 프로시저 내부의 읽기에서 강력한 일관성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-192">This ensures that reads from inside stored procedures offer strong consistency.</span></span> <span data-ttu-id="5df7f-193">사용자 정의 함수를 사용한 쿼리는 주 복제본이나 모든 보조 복제본에서 실행할 수 있지만 적절한 복제본을 선택하여 요청된 일관성 수준을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-193">Queries using user defined functions can be executed on the primary or any secondary replica, but we ensure to meet the requested consistency level by choosing the appropriate replica.</span></span>

## <a name="bounded-execution"></a><span data-ttu-id="5df7f-194">제한된 예외</span><span class="sxs-lookup"><span data-stu-id="5df7f-194">Bounded execution</span></span>
<span data-ttu-id="5df7f-195">모든 Cosmos DB 작업은 서버에서 지정된 요청 시간 제한 기간 내에 완료되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-195">All Cosmos DB operations must complete within the server specified request timeout duration.</span></span> <span data-ttu-id="5df7f-196">이 제약 조건은 JavaScript 함수(저장 프로시저, 트리거 및 사용자 정의 함수)에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-196">This constraint also applies to JavaScript functions (stored procedures, triggers and user-defined functions).</span></span> <span data-ttu-id="5df7f-197">작업이 시간 제한 내에 완료되지 않으면 트랜잭션이 롤백됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-197">If an operation does not complete with that time limit, the transaction is rolled back.</span></span> <span data-ttu-id="5df7f-198">JavaScript 함수는 시간 제한 내에 완료되거나 실행을 일괄 처리/다시 시작하는 연속 기반 모델을 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-198">JavaScript functions must finish within the time limit or implement a continuation based model to batch/resume execution.</span></span>  

<span data-ttu-id="5df7f-199">시간 제한을 처리하는 저장 프로시저 및 트리거 개발을 간소화하기 위해 컬렉션 개체 아래의 모든 함수(문서와 첨부 파일 만들기, 읽기, 바꾸기 및 삭제)는 해당 작업이 완료되는지 여부를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-199">In order to simplify development of stored procedures and triggers to handle time limits, all functions under the collection object (for create, read, replace, and delete of documents and attachments) return a Boolean value that represents whether that operation will complete.</span></span> <span data-ttu-id="5df7f-200">이 값이 false이면 시간 제한이 만료되며 프로시저 실행이 종료되어야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-200">If this value is false, it is an indication that the time limit is about to expire and that the procedure must wrap up execution.</span></span>  <span data-ttu-id="5df7f-201">수락되지 않은 첫 번째 저장소 작업 전에 대기된 작업은 저장 프로시저가 제시간에 완료되고 더 이상 요청을 대기열에 추가하지 않을 경우 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-201">Operations queued prior to the first unaccepted store operation are guaranteed to complete if the stored procedure completes in time and does not queue any more requests.</span></span>  

<span data-ttu-id="5df7f-202">JavaScript 함수는 리소스 사용에 의해서도 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-202">JavaScript functions are also bounded on resource consumption.</span></span> <span data-ttu-id="5df7f-203">Cosmos DB는 프로비전된 데이터베이스 계정 크기에 따라 컬렉션당 처리량을 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-203">Cosmos DB reserves throughput per collection based on the provisioned size of a database account.</span></span> <span data-ttu-id="5df7f-204">처리량은 요청 단위 또는 RU라고 하는 정규화된 CPU, 메모리 및 IO 사용 단위로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-204">Throughput is expressed in terms of a normalized unit of CPU, memory and IO consumption called request units or RUs.</span></span> <span data-ttu-id="5df7f-205">JavaScript 함수는 짧은 시간 내에 다수의 RU를 사용할 수 있으며, 컬렉션 한도에 도달할 경우 비율이 제한될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-205">JavaScript functions can potentially use up a large number of RUs within a short time, and might get rate-limited if the collection’s limit is reached.</span></span> <span data-ttu-id="5df7f-206">기본 데이터베이스 작업의 가용성을 위해 리소스를 많이 사용하는 저장 프로시저가 보장될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-206">Resource intensive stored procedures might also be quarantined to ensure availability of primitive database operations.</span></span>  

### <a name="example-bulk-importing-data-into-a-database-program"></a><span data-ttu-id="5df7f-207">예: 데이터베이스 프로그램으로 데이터 대량 가져오기</span><span class="sxs-lookup"><span data-stu-id="5df7f-207">Example: Bulk importing data into a database program</span></span>
<span data-ttu-id="5df7f-208">다음은 문서를 컬렉션으로 대량 가져오기 위해 작성된 저장 프로시저의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-208">Below is an example of a stored procedure that is written to bulk-import documents into a collection.</span></span> <span data-ttu-id="5df7f-209">저장 프로시저가 createDocument의 부울 반환 값을 검사하여 제한된 실행을 처리한 다음 각 저장 프로시저 호출에 삽입된 문서 수를 사용하여 일괄 처리의 진행 상황을 추적하고 다시 시작하는 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-209">Note how the stored procedure handles bounded execution by checking the Boolean return value from createDocument, and then uses the count of documents inserted in each invocation of the stored procedure to track and resume progress across batches.</span></span>

    function bulkImport(docs) {
        var collection = getContext().getCollection();
        var collectionLink = collection.getSelfLink();

        // The count of imported docs, also used as current doc index.
        var count = 0;

        // Validate input.
        if (!docs) throw new Error("The array is undefined or null.");

        var docsLength = docs.length;
        if (docsLength == 0) {
            getContext().getResponse().setBody(0);
        }

        // Call the create API to create a document.
        tryCreate(docs[count], callback);

        // Note that there are 2 exit conditions:
        // 1) The createDocument request was not accepted. 
        //    In this case the callback will not be called, we just call setBody and we are done.
        // 2) The callback was called docs.length times.
        //    In this case all documents were created and we don’t need to call tryCreate anymore. Just call setBody and we are done.
        function tryCreate(doc, callback) {
            var isAccepted = collection.createDocument(collectionLink, doc, callback);

            // If the request was accepted, callback will be called.
            // Otherwise report current count back to the client, 
            // which will call the script again with remaining set of docs.
            if (!isAccepted) getContext().getResponse().setBody(count);
        }

        // This is called when collection.createDocument is done in order to process the result.
        function callback(err, doc, options) {
            if (err) throw err;

            // One more document has been inserted, increment the count.
            count++;

            if (count >= docsLength) {
                // If we created all documents, we are done. Just set the response.
                getContext().getResponse().setBody(count);
            } else {
                // Create next document.
                tryCreate(docs[count], callback);
            }
        }
    }

## <span data-ttu-id="5df7f-210"><a id="trigger"></a> 데이터베이스 트리거</span><span class="sxs-lookup"><span data-stu-id="5df7f-210"><a id="trigger"></a> Database triggers</span></span>
### <a name="database-pre-triggers"></a><span data-ttu-id="5df7f-211">데이터베이스 사전 트리거</span><span class="sxs-lookup"><span data-stu-id="5df7f-211">Database pre-triggers</span></span>
<span data-ttu-id="5df7f-212">Cosmos DB는 문서 작업에 의해 실행되거나 트리거되는 트리거를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-212">Cosmos DB provides triggers that are executed or triggered by an operation on a document.</span></span> <span data-ttu-id="5df7f-213">예를 들어 문서를 만들 때 사전 트리거를 지정할 수 있습니다. 이 사전 트리거는 문서를 만들기 전에 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-213">For example, you can specify a pre-trigger when you are creating a document – this pre-trigger will run before the document is created.</span></span> <span data-ttu-id="5df7f-214">다음은 사전 트리거를 사용하여 만드는 문서의 속성 유효성을 검사할 수 있는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-214">The following is an example of how pre-triggers can be used to validate the properties of a document that is being created:</span></span>

    var validateDocumentContentsTrigger = {
        id: "validateDocumentContents",
        serverScript: function validate() {
            var context = getContext();
            var request = context.getRequest();

            // document to be created in the current operation
            var documentToCreate = request.getBody();

            // validate properties
            if (!("timestamp" in documentToCreate)) {
                var ts = new Date();
                documentToCreate["my timestamp"] = ts.getTime();
            }

            // update the document that will be created
            request.setBody(documentToCreate);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.Create
    }


<span data-ttu-id="5df7f-215">트리거에 해당하는 Node.js 클라이언트 쪽 등록 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-215">And the corresponding Node.js client-side registration code for the trigger:</span></span>

    // register pre-trigger
    client.createTriggerAsync(collection.self, validateDocumentContentsTrigger)
        .then(function (response) {
            console.log("Created", response.resource);
            var docToCreate = {
                id: "DocWithTrigger",
                event: "Error",
                source: "Network outage"
            };

            // run trigger while creating above document 
            var options = { preTriggerInclude: "validateDocumentContents" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response.resource); // document with timestamp property added
    }, function (error) {
        console.log("Error", error);
    });


<span data-ttu-id="5df7f-216">사전 트리거는 입력 매개 변수를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-216">Pre-triggers cannot have any input parameters.</span></span> <span data-ttu-id="5df7f-217">요청 개체를 사용하여 작업과 연결된 요청 메시지를 조작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-217">The request object can be used to manipulate the request message associated with the operation.</span></span> <span data-ttu-id="5df7f-218">여기서는 문서를 만들어 사전 트리거를 실행하며 요청 메시지 본문에 JSON 형식으로 만들 문서가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-218">Here, the pre-trigger is being run with the creation of a document, and the request message body contains the document to be created in JSON format.</span></span>   

<span data-ttu-id="5df7f-219">사용자는 트리거를 등록할 때 트리거 실행에 사용되는 작업을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-219">When triggers are registered, users can specify the operations that it can run with.</span></span> <span data-ttu-id="5df7f-220">이 트리거는 TriggerOperation.Create로 만들어졌으므로 다음이 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-220">This trigger was created with TriggerOperation.Create, which means the following is not permitted.</span></span>

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a><span data-ttu-id="5df7f-221">데이터베이스 사후 트리거</span><span class="sxs-lookup"><span data-stu-id="5df7f-221">Database post-triggers</span></span>
<span data-ttu-id="5df7f-222">사전 트리거와 마찬가지로 사후 트리거는 문서 작업과 연결되며 입력 매개 변수를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-222">Post-triggers, like pre-triggers, are associated with an operation on a document and don’t take any input parameters.</span></span> <span data-ttu-id="5df7f-223">작업이 완료된 **후에** 실행되며 클라이언트에 전송된 응답 메시지에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-223">They run **after** the operation has completed, and have access to the response message that is sent to the client.</span></span>   

<span data-ttu-id="5df7f-224">다음 예제는 사후 트리거 작동을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-224">The following example shows post-triggers in action:</span></span>

    var updateMetadataTrigger = {
        id: "updateMetadata",
        serverScript: function updateMetadata() {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            // document that was created
            var createdDocument = response.getBody();

            // query for metadata document
            var filterQuery = 'SELECT * FROM root r WHERE r.id = "_metadata"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery,
                updateMetadataCallback);
            if(!accept) throw "Unable to update metadata, abort";

            function updateMetadataCallback(err, documents, responseOptions) {
                if(err) throw new Error("Error" + err.message);
                         if(documents.length != 1) throw 'Unable to find metadata document';

                         var metadataDocument = documents[0];

                         // update metadata
                         metadataDocument.createdDocuments += 1;
                         metadataDocument.createdNames += " " + createdDocument.id;
                         var accept = collection.replaceDocument(metadataDocument._self,
                               metadataDocument, function(err, docReplaced) {
                                      if(err) throw "Unable to update metadata, abort";
                               });
                         if(!accept) throw "Unable to update metadata, abort";
                         return;                    
            }                                                                                            
        },
        triggerType: TriggerType.Post,
        triggerOperation: TriggerOperation.All
    }


<span data-ttu-id="5df7f-225">다음 샘플에 표시된 대로 트리거를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-225">The trigger can be registered as shown in the following sample.</span></span>

    // register post-trigger
    client.createTriggerAsync('dbs/testdb/colls/testColl', updateMetadataTrigger)
        .then(function(createdTrigger) { 
            var docToCreate = { 
                name: "artist_profile_1023",
                artist: "The Band",
                albums: ["Hellujah", "Rotators", "Spinning Top"]
            };

            // run trigger while creating above document 
            var options = { postTriggerInclude: "updateMetadata" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });


<span data-ttu-id="5df7f-226">이 트리거는 메타데이터 문서를 쿼리하고 새로 만든 문서에 대한 세부 정보로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-226">This trigger queries for the metadata document and updates it with details about the newly created document.</span></span>  

<span data-ttu-id="5df7f-227">한 가지 중요한 사항은 Cosmos DB에서 트리거의 **트랜잭션** 실행입니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-227">One thing that is important to note is the **transactional** execution of triggers in Cosmos DB.</span></span> <span data-ttu-id="5df7f-228">이 사후 트리거는 원본 문서 만들기와 동일한 트랜잭션의 일부로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-228">This post-trigger runs as part of the same transaction as the creation of the original document.</span></span> <span data-ttu-id="5df7f-229">따라서 사후 트리거에서 예외가 발생할 경우(가령 메타데이터 문서를 업데이트할 수 없는 경우) 전체 트랜잭션이 실패하고 롤백됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-229">Therefore, if we throw an exception from the post-trigger (say if we are unable to update the metadata document), the whole transaction will fail and be rolled back.</span></span> <span data-ttu-id="5df7f-230">문서가 만들어지지 않고 예외가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-230">No document will be created, and an exception will be returned.</span></span>  

## <span data-ttu-id="5df7f-231"><a id="udf"></a>사용자 정의 함수</span><span class="sxs-lookup"><span data-stu-id="5df7f-231"><a id="udf"></a>User-defined functions</span></span>
<span data-ttu-id="5df7f-232">UDF(사용자 정의 함수)는 DocumentDB API SQL 쿼리 언어 문법을 확장하고 사용자 지정 비즈니스 논리를 구현하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-232">User-defined functions (UDFs) are used to extend the DocumentDB API SQL query language grammar and implement custom business logic.</span></span> <span data-ttu-id="5df7f-233">UDF는 쿼리 내부에서만 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-233">They can only be called from inside queries.</span></span> <span data-ttu-id="5df7f-234">컨텍스트 개체에 액세스할 수 없으며 계산 전용 JavaScript로 사용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-234">They do not have access to the context object and are meant to be used as compute-only JavaScript.</span></span> <span data-ttu-id="5df7f-235">따라서 UDF는 Cosmos DB 서비스의 보조 복제본에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-235">Therefore, UDFs can be run on secondary replicas of the Cosmos DB service.</span></span>  

<span data-ttu-id="5df7f-236">다음 샘플에서는 다양한 수입 브래킷에 대한 비율에 따라 소득세를 계산하는 UDF를 만든 다음 쿼리 내부에서 사용하여 납부한 세금이 $20,000를 초과하는 모든 사람을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-236">The following sample creates a UDF to calculate income tax based on rates for various income brackets, and then uses it inside a query to find all people who paid more than $20,000 in taxes.</span></span>

    var taxUdf = {
        id: "tax",
        serverScript: function tax(income) {

            if(income == undefined) 
                throw 'no input';

            if (income < 1000) 
                return income * 0.1;
            else if (income < 10000) 
                return income * 0.2;
            else
                return income * 0.4;
        }
    }


<span data-ttu-id="5df7f-237">이후에 다음 샘플과 같이 쿼리에 UDF를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-237">The UDF can subsequently be used in queries like in the following sample:</span></span>

    // register UDF
    client.createUserDefinedFunctionAsync('dbs/testdb/colls/testColl', taxUdf)
        .then(function(response) { 
            console.log("Created", response.resource);

            var query = 'SELECT * FROM TaxPayers t WHERE udf.tax(t.income) > 20000'; 
            return client.queryDocuments('dbs/testdb/colls/testColl',
                   query).toArrayAsync();
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        var documents = response.feed;
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });

## <a name="javascript-language-integrated-query-api"></a><span data-ttu-id="5df7f-238">JavaScript 언어 통합 쿼리 API</span><span class="sxs-lookup"><span data-stu-id="5df7f-238">JavaScript language-integrated query API</span></span>
<span data-ttu-id="5df7f-239">DocumentDB의 SQL 문법을 사용하여 쿼리를 발급하는 것 외에도 서버 쪽 SDK를 사용하면 SQL의 지식 없이도 흐름 JavaScript 인터페이스를 사용하여 최적화된 쿼리를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-239">In addition to issuing queries using DocumentDB’s SQL grammar, the server-side SDK allows you to perform optimized queries using a fluent JavaScript interface without any knowledge of SQL.</span></span> <span data-ttu-id="5df7f-240">JavaScript 쿼리 API를 사용하면 조건자 함수를 ECMAScript5의 배열 기본 제공 항목과 익숙한 구문 및 lodash와 같은 인기 있는 JavaScript 라이브러리가 포함된 연결 가능한 함수 호출에 전달하여 쿼리를 프로그래밍 방식으로 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-240">The JavaScript query API allows you to programmatically build queries by passing predicate functions into chainable function calls, with a syntax familiar to ECMAScript5's Array built-ins and popular JavaScript libraries like lodash.</span></span> <span data-ttu-id="5df7f-241">쿼리는 Azure Cosmos DB의 인덱스를 사용하여 효율적으로 실행되도록 JavaScript 런타임으로 구문 분석됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-241">Queries are parsed by the JavaScript runtime to be executed efficiently using Azure Cosmos DB’s indices.</span></span>

> [!NOTE]
> <span data-ttu-id="5df7f-242">`__`(이중 밑줄)은 `getContext().getCollection()`에 대한 별칭입니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-242">`__` (double-underscore) is an alias to `getContext().getCollection()`.</span></span>
> <br/>
> <span data-ttu-id="5df7f-243">즉, `__` 또는 `getContext().getCollection()`을 사용하여 JavaScript 쿼리 API에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-243">In other words, you can use `__` or `getContext().getCollection()` to access the JavaScript query API.</span></span>
> 
> 

<span data-ttu-id="5df7f-244">지원되는 함수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-244">Supported functions include:</span></span>

<ul>
<li><span data-ttu-id="5df7f-245">
<b>chain() ... .value([callback] [, options])</b>
</span><span class="sxs-lookup"><span data-stu-id="5df7f-245">
<b>chain() ... .value([callback] [, options])</b>
</span></span><ul>
<li>
<span data-ttu-id="5df7f-246">value()로 종료되어야 하는 연결된 호출을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-246">Starts a chained call which must be terminated with value().</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="5df7f-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="5df7f-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="5df7f-248">출력 문서를 결과 집합으로 필터링하기 위해 true/false를 반환하는 조건자 함수를 사용하여 입력을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-248">Filters the input using a predicate function which returns true/false in order to filter in/out input documents into the resulting set.</span></span> <span data-ttu-id="5df7f-249">이 동작은 SQL의 WHERE 절과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-249">This behaves similar to a WHERE clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="5df7f-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="5df7f-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="5df7f-251">각 입력 항목을 JavaScript 개체 또는 값에 매핑하는 변환 함수에 대해 프로젝션을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-251">Applies a projection given a transformation function which maps each input item to a JavaScript object or value.</span></span> <span data-ttu-id="5df7f-252">이 동작은 SQL의 SELECT 절과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-252">This behaves similar to a SELECT clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="5df7f-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="5df7f-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="5df7f-254">이 각 입력 항목에서 단일 속성의 값을 추출하는 맵에 대한 바로 가기입니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-254">This is a shortcut for a map which extracts the value of a single property from each input item.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="5df7f-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="5df7f-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="5df7f-256">각 입력 항목의 배열을 단일 배열로 결합하고 평면화합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-256">Combines and flattens arrays from each input item in to a single array.</span></span> <span data-ttu-id="5df7f-257">이 동작은 LINQ의 SelectMany와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-257">This behaves similar to SelectMany in LINQ.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="5df7f-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="5df7f-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="5df7f-259">주어진 조건자를 사용하여 입력 문서 스트림의 문서를 오름차순으로 정렬하여 새 문서 집합을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-259">Produce a new set of documents by sorting the documents in the input document stream in ascending order using the given predicate.</span></span> <span data-ttu-id="5df7f-260">이 동작은 SQL의 ORDER BY 절과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-260">This behaves similar to a ORDER BY clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="5df7f-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="5df7f-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="5df7f-262">주어진 조건자를 사용하여 입력 문서 스트림의 문서를 내림차순으로 정렬하여 새 문서 집합을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-262">Produce a new set of documents by sorting the documents in the input document stream in descending order using the given predicate.</span></span> <span data-ttu-id="5df7f-263">이 동작은 SQL의 ORDER BY x DESC 절과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-263">This behaves similar to a ORDER BY x DESC clause in SQL.</span></span>
</li>
</ul>
</li>
</ul>


<span data-ttu-id="5df7f-264">조건자 및/또는 선택기 함수 안에 포함된 경우 다음과 같은 JavaScript 구문이 Azure Cosmos DB 인덱스에서 직접 실행하도록 자동으로 최적화됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-264">When included inside predicate and/or selector functions, the following JavaScript constructs get automatically optimized to run directly on Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="5df7f-265">간단한 연산자: = = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span><span class="sxs-lookup"><span data-stu-id="5df7f-265">Simple operators: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span></span> ~
* <span data-ttu-id="5df7f-266">개체 리터럴을 포함하는 리터럴: {}</span><span class="sxs-lookup"><span data-stu-id="5df7f-266">Literals, including the object literal: {}</span></span>
* <span data-ttu-id="5df7f-267">var, 반환</span><span class="sxs-lookup"><span data-stu-id="5df7f-267">var, return</span></span>

<span data-ttu-id="5df7f-268">다음 JavaScript 구문은 Azure Cosmos DB 인덱스에 대해 최적화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-268">The following JavaScript constructs do not get optimized for Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="5df7f-269">흐름 제어(예: if, for, while)</span><span class="sxs-lookup"><span data-stu-id="5df7f-269">Control flow (e.g. if, for, while)</span></span>
* <span data-ttu-id="5df7f-270">함수 호출</span><span class="sxs-lookup"><span data-stu-id="5df7f-270">Function calls</span></span>

<span data-ttu-id="5df7f-271">자세한 내용은 [서버 쪽 JSDocs](http://azure.github.io/azure-documentdb-js-server/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5df7f-271">For more information, please see our [Server-Side JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span></span>

### <a name="example-write-a-stored-procedure-using-the-javascript-query-api"></a><span data-ttu-id="5df7f-272">예: JavaScript 쿼리 API를 사용하여 저장된 프로시저 작성</span><span class="sxs-lookup"><span data-stu-id="5df7f-272">Example: Write a stored procedure using the JavaScript query API</span></span>
<span data-ttu-id="5df7f-273">다음 코드 샘플은 저장된 프로시저의 컨텍스트에서 JavaScript 쿼리 API를 사용할 수 있는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-273">The following code sample is an example of how the JavaScript Query API can be used in the context of a stored procedure.</span></span> <span data-ttu-id="5df7f-274">저장된 프로시저는 입력된 매개 변수로 지정된 문서를 삽입하고 입력된 문서의 크기 속성을 기반으로 하는 minSize, maxSize 및 totalSize가 있는 `__.filter()` 메서드를 사용하여 메타데이터 문서를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-274">The stored procedure inserts a document, given by an input parameter, and updates a metadata document, using the `__.filter()` method, with minSize, maxSize, and totalSize based upon the input document's size property.</span></span>

    /**
     * Insert actual doc and update metadata doc: minSize, maxSize, totalSize based on doc.size.
     */
    function insertDocumentAndUpdateMetadata(doc) {
      // HTTP error codes sent to our callback funciton by DocDB server.
      var ErrorCode = {
        RETRY_WITH: 449,
      }

      var isAccepted = __.createDocument(__.getSelfLink(), doc, {}, function(err, doc, options) {
        if (err) throw err;

        // Check the doc (ignore docs with invalid/zero size and metaDoc itself) and call updateMetadata.
        if (!doc.isMetadata && doc.size > 0) {
          // Get the meta document. We keep it in the same collection. it's the only doc that has .isMetadata = true.
          var result = __.filter(function(x) {
            return x.isMetadata === true
          }, function(err, feed, options) {
            if (err) throw err;

            // We assume that metadata doc was pre-created and must exist when this script is called.
            if (!feed || !feed.length) throw new Error("Failed to find the metadata document.");

            // The metadata document.
            var metaDoc = feed[0];

            // Update metaDoc.minSize:
            // for 1st document use doc.Size, for all the rest see if it's less than last min.
            if (metaDoc.minSize == 0) metaDoc.minSize = doc.size;
            else metaDoc.minSize = Math.min(metaDoc.minSize, doc.size);

            // Update metaDoc.maxSize.
            metaDoc.maxSize = Math.max(metaDoc.maxSize, doc.size);

            // Update metaDoc.totalSize.
            metaDoc.totalSize += doc.size;

            // Update/replace the metadata document in the store.
            var isAccepted = __.replaceDocument(metaDoc._self, metaDoc, function(err) {
              if (err) throw err;
              // Note: in case concurrent updates causes conflict with ErrorCode.RETRY_WITH, we can't read the meta again 
              //       and update again because due to Snapshot isolation we will read same exact version (we are in same transaction).
              //       We have to take care of that on the client side.
            });
            if (!isAccepted) throw new Error("replaceDocument(metaDoc) returned false.");
          });
          if (!result.isAccepted) throw new Error("filter for metaDoc returned false.");
        }
      });
      if (!isAccepted) throw new Error("createDocument(actual doc) returned false.");
    }

## <a name="sql-to-javascript-cheat-sheet"></a><span data-ttu-id="5df7f-275">SQL-Javascript 치트 시트</span><span class="sxs-lookup"><span data-stu-id="5df7f-275">SQL to Javascript cheat sheet</span></span>
<span data-ttu-id="5df7f-276">다음 표에서 다양한 SQL 쿼리 및 해당 JavaScript 쿼리를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-276">The following table presents various SQL queries and the corresponding JavaScript queries.</span></span>

<span data-ttu-id="5df7f-277">SQL 쿼리를 사용하는 것과 같이 문서 속성 키(예: `doc.id`)는 소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-277">As with SQL queries, document property keys (e.g. `doc.id`) are case-sensitive.</span></span>

|<span data-ttu-id="5df7f-278">SQL</span><span class="sxs-lookup"><span data-stu-id="5df7f-278">SQL</span></span>| <span data-ttu-id="5df7f-279">JavaScript Query API</span><span class="sxs-lookup"><span data-stu-id="5df7f-279">JavaScript Query API</span></span>|<span data-ttu-id="5df7f-280">아래 설명</span><span class="sxs-lookup"><span data-stu-id="5df7f-280">Description below</span></span>|
|---|---|---|
|<span data-ttu-id="5df7f-281">SELECT *</span><span class="sxs-lookup"><span data-stu-id="5df7f-281">SELECT *</span></span><br><span data-ttu-id="5df7f-282">FROM docs</span><span class="sxs-lookup"><span data-stu-id="5df7f-282">FROM docs</span></span>| <span data-ttu-id="5df7f-283">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="5df7f-283">__.map(function(doc) {</span></span> <br><span data-ttu-id="5df7f-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span><span class="sxs-lookup"><span data-stu-id="5df7f-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span></span><br><span data-ttu-id="5df7f-285">});</span><span class="sxs-lookup"><span data-stu-id="5df7f-285">});</span></span>|<span data-ttu-id="5df7f-286">1</span><span class="sxs-lookup"><span data-stu-id="5df7f-286">1</span></span>|
|<span data-ttu-id="5df7f-287">SELECT docs.id, docs.message AS msg, docs.actions</span><span class="sxs-lookup"><span data-stu-id="5df7f-287">SELECT docs.id, docs.message AS msg, docs.actions</span></span> <br><span data-ttu-id="5df7f-288">FROM docs</span><span class="sxs-lookup"><span data-stu-id="5df7f-288">FROM docs</span></span>|<span data-ttu-id="5df7f-289">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="5df7f-289">__.map(function(doc) {</span></span><br><span data-ttu-id="5df7f-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="5df7f-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="5df7f-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="5df7f-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="5df7f-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span><span class="sxs-lookup"><span data-stu-id="5df7f-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span></span><br><span data-ttu-id="5df7f-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span><span class="sxs-lookup"><span data-stu-id="5df7f-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span></span><br><span data-ttu-id="5df7f-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="5df7f-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="5df7f-295">});</span><span class="sxs-lookup"><span data-stu-id="5df7f-295">});</span></span>|<span data-ttu-id="5df7f-296">2</span><span class="sxs-lookup"><span data-stu-id="5df7f-296">2</span></span>|
|<span data-ttu-id="5df7f-297">SELECT *</span><span class="sxs-lookup"><span data-stu-id="5df7f-297">SELECT *</span></span><br><span data-ttu-id="5df7f-298">FROM docs</span><span class="sxs-lookup"><span data-stu-id="5df7f-298">FROM docs</span></span><br><span data-ttu-id="5df7f-299">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="5df7f-299">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="5df7f-300">__.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="5df7f-300">__.filter(function(doc) {</span></span><br><span data-ttu-id="5df7f-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="5df7f-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="5df7f-302">});</span><span class="sxs-lookup"><span data-stu-id="5df7f-302">});</span></span>|<span data-ttu-id="5df7f-303">3</span><span class="sxs-lookup"><span data-stu-id="5df7f-303">3</span></span>|
|<span data-ttu-id="5df7f-304">SELECT *</span><span class="sxs-lookup"><span data-stu-id="5df7f-304">SELECT *</span></span><br><span data-ttu-id="5df7f-305">FROM docs</span><span class="sxs-lookup"><span data-stu-id="5df7f-305">FROM docs</span></span><br><span data-ttu-id="5df7f-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span><span class="sxs-lookup"><span data-stu-id="5df7f-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span></span>|<span data-ttu-id="5df7f-307">__.filter(function(x) {</span><span class="sxs-lookup"><span data-stu-id="5df7f-307">__.filter(function(x) {</span></span><br><span data-ttu-id="5df7f-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span><span class="sxs-lookup"><span data-stu-id="5df7f-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span></span><br><span data-ttu-id="5df7f-309">});</span><span class="sxs-lookup"><span data-stu-id="5df7f-309">});</span></span>|<span data-ttu-id="5df7f-310">4</span><span class="sxs-lookup"><span data-stu-id="5df7f-310">4</span></span>|
|<span data-ttu-id="5df7f-311">SELECT docs.id, docs.message AS msg</span><span class="sxs-lookup"><span data-stu-id="5df7f-311">SELECT docs.id, docs.message AS msg</span></span><br><span data-ttu-id="5df7f-312">FROM docs</span><span class="sxs-lookup"><span data-stu-id="5df7f-312">FROM docs</span></span><br><span data-ttu-id="5df7f-313">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="5df7f-313">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="5df7f-314">__.chain()</span><span class="sxs-lookup"><span data-stu-id="5df7f-314">__.chain()</span></span><br><span data-ttu-id="5df7f-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="5df7f-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="5df7f-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="5df7f-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="5df7f-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="5df7f-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="5df7f-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="5df7f-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span></span><br><span data-ttu-id="5df7f-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="5df7f-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="5df7f-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="5df7f-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="5df7f-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span><span class="sxs-lookup"><span data-stu-id="5df7f-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span></span><br><span data-ttu-id="5df7f-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="5df7f-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="5df7f-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="5df7f-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="5df7f-324">.value();</span><span class="sxs-lookup"><span data-stu-id="5df7f-324">.value();</span></span>|<span data-ttu-id="5df7f-325">5</span><span class="sxs-lookup"><span data-stu-id="5df7f-325">5</span></span>|
|<span data-ttu-id="5df7f-326">SELECT VALUE tag</span><span class="sxs-lookup"><span data-stu-id="5df7f-326">SELECT VALUE tag</span></span><br><span data-ttu-id="5df7f-327">FROM docs</span><span class="sxs-lookup"><span data-stu-id="5df7f-327">FROM docs</span></span><br><span data-ttu-id="5df7f-328">JOIN tag IN docs.Tags</span><span class="sxs-lookup"><span data-stu-id="5df7f-328">JOIN tag IN docs.Tags</span></span><br><span data-ttu-id="5df7f-329">ORDER BY docs._ts</span><span class="sxs-lookup"><span data-stu-id="5df7f-329">ORDER BY docs._ts</span></span>|<span data-ttu-id="5df7f-330">__.chain()</span><span class="sxs-lookup"><span data-stu-id="5df7f-330">__.chain()</span></span><br><span data-ttu-id="5df7f-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="5df7f-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="5df7f-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span><span class="sxs-lookup"><span data-stu-id="5df7f-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span></span><br><span data-ttu-id="5df7f-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="5df7f-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="5df7f-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="5df7f-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span></span><br><span data-ttu-id="5df7f-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span><span class="sxs-lookup"><span data-stu-id="5df7f-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span></span><br><span data-ttu-id="5df7f-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="5df7f-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="5df7f-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span><span class="sxs-lookup"><span data-stu-id="5df7f-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span></span><br><span data-ttu-id="5df7f-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span><span class="sxs-lookup"><span data-stu-id="5df7f-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span></span><br><span data-ttu-id="5df7f-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span><span class="sxs-lookup"><span data-stu-id="5df7f-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span></span>|<span data-ttu-id="5df7f-340">6</span><span class="sxs-lookup"><span data-stu-id="5df7f-340">6</span></span>|

<span data-ttu-id="5df7f-341">다음 설명에서는 위의 테이블에 있는 각 쿼리를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-341">The following descriptions explain each query in the table above.</span></span>
1. <span data-ttu-id="5df7f-342">모든 문서(연속 토큰과 함께 페이지가 매겨진)의 결과는 있는 그대로입니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-342">Results in all documents (paginated with continuation token) as is.</span></span>
2. <span data-ttu-id="5df7f-343">모든 문서에서 id, message(msg로 별칭이 지정됨) 및 action을 프로젝션합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-343">Projects the id, message (aliased to msg), and action from all documents.</span></span>
3. <span data-ttu-id="5df7f-344">조건자: id = "X998\_Y998"을 사용하여 문서를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-344">Queries for documents with the predicate: id = "X998_Y998".</span></span>
4. <span data-ttu-id="5df7f-345">Tags 속성이 있는 문서를 쿼리합니다. Tags는 123 값을 포함하는 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-345">Queries for documents that have a Tags property and Tags is an array containing the value 123.</span></span>
5. <span data-ttu-id="5df7f-346">조건자 id = "X998_Y998"을 사용하여 문서를 쿼리한 다음 id와 message(msg로 별칭이 지정됨)를 프로젝션합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-346">Queries for documents with a predicate, id = "X998_Y998", and then projects the id and message (aliased to msg).</span></span>
6. <span data-ttu-id="5df7f-347">array 속성 Tags가 있는 문서를 필터링하고 _ts timestamp system 속성으로 결과 문서를 정렬한 다음 Tags 배열을 프로젝션 및 평면화합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-347">Filters for documents which have an array property, Tags, and sorts the resulting documents by the _ts timestamp system property, and then projects + flattens the Tags array.</span></span>


## <a name="runtime-support"></a><span data-ttu-id="5df7f-348">런타임 지원</span><span class="sxs-lookup"><span data-stu-id="5df7f-348">Runtime support</span></span>
<span data-ttu-id="5df7f-349">[DocumentDB JavaScript 서버 쪽 API](http://azure.github.io/azure-documentdb-js-server/)는 [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm)에서 표준화된 일반 JavaScript 언어 기능을 대부분 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-349">[DocumentDB JavaScript server side API](http://azure.github.io/azure-documentdb-js-server/) provides support for the most of the mainstream JavaScript language features as standardized by [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span></span>

### <a name="security"></a><span data-ttu-id="5df7f-350">보안</span><span class="sxs-lookup"><span data-stu-id="5df7f-350">Security</span></span>
<span data-ttu-id="5df7f-351">JavaScript 저장 프로시저와 트리거는 한 스크립트의 결과가 데이터베이스 수준의 스냅숏 트랜잭션 격리를 통과하지 않고 다른 스크립트로 누출되지 않도록 샌드박스됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-351">JavaScript stored procedures and triggers are sandboxed so that the effects of one script do not leak to the other without going through the snapshot transaction isolation at the database level.</span></span> <span data-ttu-id="5df7f-352">런타임 환경은 풀링되지만 각 실행 후에 컨텍스트가 정리됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-352">The runtime environments are pooled but cleaned of the context after each run.</span></span> <span data-ttu-id="5df7f-353">따라서 서로 간의 의도치 않은 파생 작업으로부터 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-353">Hence they are guaranteed to be safe of any unintended side effects from each other.</span></span>

### <a name="pre-compilation"></a><span data-ttu-id="5df7f-354">사전 컴파일</span><span class="sxs-lookup"><span data-stu-id="5df7f-354">Pre-compilation</span></span>
<span data-ttu-id="5df7f-355">저장 프로시저, 트리거 및 UDF는 각 스크립트 호출 시 컴파일 비용을 방지하기 위해 암시적으로 바이트 코드 형식으로 사전 컴파일됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-355">Stored procedures, triggers and UDFs are implicitly precompiled to the byte code format in order to avoid compilation cost at the time of each script invocation.</span></span> <span data-ttu-id="5df7f-356">이렇게 하면 저장 프로시저 호출이 빠르며 사용 공간이 적습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-356">This ensures invocations of stored procedures are fast and have a low footprint.</span></span>

## <a name="client-sdk-support"></a><span data-ttu-id="5df7f-357">클라이언트 SDK 지원</span><span class="sxs-lookup"><span data-stu-id="5df7f-357">Client SDK support</span></span>
<span data-ttu-id="5df7f-358">[Node.js](documentdb-sdk-node.md) 클라이언트용 DocumentDB API뿐 아니라 Azure Cosmos DB에는 DocumentDB API용 [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/) 및 [Python SDK](documentdb-sdk-python.md)도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-358">In addition to the DocumentDB API for [Node.js](documentdb-sdk-node.md) client, Azure Cosmos DB has [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/), and [Python SDKs](documentdb-sdk-python.md) for the DocumentDB API.</span></span> <span data-ttu-id="5df7f-359">이러한 SDK를 사용하여 저장 프로시저, 트리거 및 UDF를 만들고 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-359">Stored procedures, triggers and UDFs can be created and executed using any of these SDKs as well.</span></span> <span data-ttu-id="5df7f-360">다음 예제에서는 .NET 클라이언트를 사용하여 저장 프로시저를 만들고 실행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-360">The following example shows how to create and execute a stored procedure using the .NET client.</span></span> <span data-ttu-id="5df7f-361">.NET 유형을 저장 프로시저에 JSON으로 전달하고 다시 읽는 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-361">Note how the .NET types are passed into the stored procedure as JSON and read back.</span></span>

    var markAntiquesSproc = new StoredProcedure
    {
        Id = "ValidateDocumentAge",
        Body = @"
                function(docToCreate, antiqueYear) {
                    var collection = getContext().getCollection();    
                    var response = getContext().getResponse();    

                    if(docToCreate.Year != undefined && docToCreate.Year < antiqueYear){
                        docToCreate.antique = true;
                    }

                    collection.createDocument(collection.getSelfLink(), docToCreate, {}, 
                        function(err, docCreated, options) { 
                            if(err) throw new Error('Error while creating document: ' + err.message);                              
                            if(options.maxCollectionSizeInMb == 0) throw 'max collection size not found'; 
                            response.setBody(docCreated);
                    });
             }"
    };

    // register stored procedure
    StoredProcedure createdStoredProcedure = await client.CreateStoredProcedureAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), markAntiquesSproc);
    dynamic document = new Document() { Id = "Borges_112" };
    document.Title = "Aleph";
    document.Year = 1949;

    // execute stored procedure
    Document createdDocument = await client.ExecuteStoredProcedureAsync<Document>(UriFactory.CreateStoredProcedureUri("db", "coll", "sproc"), document, 1920);


<span data-ttu-id="5df7f-362">이 샘플에서는 [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)를 사용하여 사전 트리거를 만들고 트리거를 사용하도록 설정하여 문서를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-362">This sample shows how to use the [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) to create a pre-trigger and create a document with the trigger enabled.</span></span> 

    Trigger preTrigger = new Trigger()
    {
        Id = "CapitalizeName",
        Body = @"function() {
            var item = getContext().getRequest().getBody();
            item.id = item.id.toUpperCase();
            getContext().getRequest().setBody(item);
        }",
        TriggerOperation = TriggerOperation.Create,
        TriggerType = TriggerType.Pre
    };

    Document createdItem = await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), new Document { Id = "documentdb" },
        new RequestOptions
        {
            PreTriggerInclude = new List<string> { "CapitalizeName" },
        });


<span data-ttu-id="5df7f-363">다음 예제에서는 UDF(사용자 정의 함수)를 만들고 [DocumentDB API SQL 쿼리](documentdb-sql-query.md)에 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-363">And the following example shows how to create a user defined function (UDF) and use it in a [DocumentDB API SQL query](documentdb-sql-query.md).</span></span>

    UserDefinedFunction function = new UserDefinedFunction()
    {
        Id = "LOWER",
        Body = @"function(input) 
        {
            return input.toLowerCase();
        }"
    };

    foreach (Book book in client.CreateDocumentQuery(UriFactory.CreateDocumentCollectionUri("db", "coll"),
        "SELECT * FROM Books b WHERE udf.LOWER(b.Title) = 'war and peace'"))
    {
        Console.WriteLine("Read {0} from query", book);
    }

## <a name="rest-api"></a><span data-ttu-id="5df7f-364">REST API</span><span class="sxs-lookup"><span data-stu-id="5df7f-364">REST API</span></span>
<span data-ttu-id="5df7f-365">모든 Azure Cosmos DB 작업은 RESTful 방식으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-365">All Azure Cosmos DB operations can be performed in a RESTful manner.</span></span> <span data-ttu-id="5df7f-366">HTTP POST를 사용하여 저장 프로시저, 트리거 및 사용자 정의 함수를 컬렉션 아래에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-366">Stored procedures, triggers and user-defined functions can be registered under a collection by using HTTP POST.</span></span> <span data-ttu-id="5df7f-367">다음은 저장 프로시저를 등록하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-367">The following is an example of how to register a stored procedure:</span></span>

    POST https://<url>/sprocs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT


    var x = {
      "name": "createAndAddProperty",
      "body": function (docToCreate, addedPropertyName, addedPropertyValue) {
                var collectionManager = getContext().getCollection();
                collectionManager.createDocument(
                    collectionManager.getSelfLink(),
                    docToCreate,
                    function(err, docCreated) {
                      if(err) throw new Error('Error:  ' + err.message);
                      docCreated[addedPropertyName] = addedPropertyValue;
                      getContext().getResponse().setBody(docCreated);
                    });
            }
    }


<span data-ttu-id="5df7f-368">만들려는 저장 프로시저를 본문에 포함하여 URI dbs/testdb/colls/testColl/sprocs에 대해 POST 요청을 실행하면 저장 프로시저가 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-368">The stored procedure is registered by executing a POST request against the URI dbs/testdb/colls/testColl/sprocs with the body containing the stored procedure to create.</span></span> <span data-ttu-id="5df7f-369">트리거 및 UDF는 각각 /triggers 및 /udfs에 대해 POST를 실행해서 비슷하게 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-369">Triggers and UDFs can be registered similarly by issuing a POST against /triggers and /udfs respectively.</span></span>
<span data-ttu-id="5df7f-370">그런 다음 해당 리소스 링크에 대해 POST 요청을 실행해서 이 저장 프로시저를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-370">This stored procedure can then be executed by issuing a POST request against its resource link:</span></span>

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of the Patriarch"}, "Price", 200 ]


<span data-ttu-id="5df7f-371">여기서는 저장 프로시저에 대한 입력이 요청 본문에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-371">Here, the input to the stored procedure is passed in the request body.</span></span> <span data-ttu-id="5df7f-372">입력은 입력 매개 변수의 JSON 배열로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-372">Note that the input is passed as a JSON array of input parameters.</span></span> <span data-ttu-id="5df7f-373">저장 프로시저는 첫 번째 입력을 응답 본문인 문서로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-373">The stored procedure takes the first input as a document that is a response body.</span></span> <span data-ttu-id="5df7f-374">수신하는 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-374">The response we receive is as follows:</span></span>

    HTTP/1.1 200 OK

    { 
      name: 'TestDocument',
      book: ‘Autumn of the Patriarch’,
      id: ‘V7tQANV3rAkDAAAAAAAAAA==‘,
      ts: 1407830727,
      self: ‘dbs/V7tQAA==/colls/V7tQANV3rAk=/docs/V7tQANV3rAkDAAAAAAAAAA==/’,
      etag: ‘6c006596-0000-0000-0000-53e9cac70000’,
      attachments: ‘attachments/’,
      Price: 200
    }


<span data-ttu-id="5df7f-375">저장 프로시저와 달리 트리거는 직접 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-375">Triggers, unlike stored procedures, cannot be executed directly.</span></span> <span data-ttu-id="5df7f-376">대신, 문서 작업의 일부로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-376">Instead they are executed as part of an operation on a document.</span></span> <span data-ttu-id="5df7f-377">HTTP 헤더를 사용하여 요청과 함께 실행할 트리거를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-377">We can specify the triggers to run with a request using HTTP headers.</span></span> <span data-ttu-id="5df7f-378">다음은 문서 만들기 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-378">The following is request to create a document.</span></span>

    POST https://<url>/docs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT
    x-ms-documentdb-pre-trigger-include: validateDocumentContents 
    x-ms-documentdb-post-trigger-include: bookCreationPostTrigger


    {
       "name": "newDocument",
       “title”: “The Wizard of Oz”,
       “author”: “Frank Baum”,
       “pages”: 92
    }


<span data-ttu-id="5df7f-379">여기서는 요청과 함께 실행할 사전 트리거가 x-ms-documentdb-pre-trigger-include 헤더에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-379">Here the pre-trigger to be run with the request is specified in the x-ms-documentdb-pre-trigger-include header.</span></span> <span data-ttu-id="5df7f-380">마찬가지로, 모든 사후 트리거는 x-ms-documentdb-post-trigger-include 헤더에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-380">Correspondingly, any post-triggers are given in the x-ms-documentdb-post-trigger-include header.</span></span> <span data-ttu-id="5df7f-381">지정된 요청에 사전 트리거와 사후 트리거를 둘 다 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-381">Note that both pre- and post-triggers can be specified for a given request.</span></span>

## <a name="sample-code"></a><span data-ttu-id="5df7f-382">샘플 코드</span><span class="sxs-lookup"><span data-stu-id="5df7f-382">Sample code</span></span>
<span data-ttu-id="5df7f-383">[GitHub 리포지토리](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples)에서 더 많은 서버 쪽 코드 예제([bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js) 및 [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js) 포함)를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-383">You can find more server-side code examples (including [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), and [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) on our [GitHub repository](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span></span>

<span data-ttu-id="5df7f-384">저장된 프로시저를 공유하시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="5df7f-384">Want to share your awesome stored procedure?</span></span> <span data-ttu-id="5df7f-385">끌어오기 요청을 보내주세요.</span><span class="sxs-lookup"><span data-stu-id="5df7f-385">Please, send us a pull-request!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5df7f-386">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5df7f-386">Next steps</span></span>
<span data-ttu-id="5df7f-387">하나 이상의 저장된 프로시저, 트리거 및 생성된 사용자 정의 함수가 있다면 데이터 탐색기를 사용하여 Azure Portal에서 해당 함수를 로드하고 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-387">Once you have one or more stored procedures, triggers, and user-defined functions created, you can load them and view them in the Azure portal using Data Explorer.</span></span>

<span data-ttu-id="5df7f-388">또한 Azure Cosmos DB 서버 쪽 프로그래밍에 대한 자세한 내용을 보려면 경로에서 다음의 참조 자료 및 리소스가 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="5df7f-388">You may also find the following references and resources useful in your path to learn more about Azure Cosmos dB server-side programming:</span></span>

* [<span data-ttu-id="5df7f-389">Azure Cosmos DB SDK</span><span class="sxs-lookup"><span data-stu-id="5df7f-389">Azure Cosmos DB SDKs</span></span>](documentdb-sdk-dotnet.md)
* [<span data-ttu-id="5df7f-390">DocumentDB 스튜디오</span><span class="sxs-lookup"><span data-stu-id="5df7f-390">DocumentDB Studio</span></span>](https://github.com/mingaliu/DocumentDBStudio/releases)
* [<span data-ttu-id="5df7f-391">JSON</span><span class="sxs-lookup"><span data-stu-id="5df7f-391">JSON</span></span>](http://www.json.org/) 
* [<span data-ttu-id="5df7f-392">JavaScript ECMA-262</span><span class="sxs-lookup"><span data-stu-id="5df7f-392">JavaScript ECMA-262</span></span>](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [<span data-ttu-id="5df7f-393">안전하고 이식 가능한 데이터베이스 확장성</span><span class="sxs-lookup"><span data-stu-id="5df7f-393">Secure and Portable Database Extensibility</span></span>](http://dl.acm.org/citation.cfm?id=276339) 
* [<span data-ttu-id="5df7f-394">서비스 지향 데이터베이스 아키텍처</span><span class="sxs-lookup"><span data-stu-id="5df7f-394">Service Oriented Database Architecture</span></span>](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [<span data-ttu-id="5df7f-395">Microsoft SQL server에서 .NET 런타임 호스팅</span><span class="sxs-lookup"><span data-stu-id="5df7f-395">Hosting the .NET Runtime in Microsoft SQL server</span></span>](http://dl.acm.org/citation.cfm?id=1007669)

