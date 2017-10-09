---
title: "Azure Cosmos db aaaServer 쪽 JavaScript 프로그래밍 | Microsoft Docs"
description: "어떻게 toouse Azure Cosmos DB toowrite 저장 프로시저, 데이터베이스 트리거 및 사용자 정의 함수 (Udf) javascript에서에 대해 알아봅니다. 데이터베이스 프로그래밍 팁 등을 가져옵니다."
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
ms.openlocfilehash: 5a011d1c4b0b5908d5de73607a1bc328ed1711d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a><span data-ttu-id="af885-105">Azure Cosmos DB 서버 쪽 프로그래밍: 저장 프로시저, 데이터베이스 트리거 및 UDF</span><span class="sxs-lookup"><span data-stu-id="af885-105">Azure Cosmos DB server-side programming: Stored procedures, database triggers, and UDFs</span></span>
<span data-ttu-id="af885-106">Azure Cosmos DB가 언어 통합 트랜잭션 방식으로 JavaScript를 실행하므로 개발자가 기본적으로 [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript로 **저장 프로시저**, **트리거** 및 **UDF(사용자 정의 함수)**를 작성할 수 있는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="af885-106">Learn how Azure Cosmos DB’s language integrated, transactional execution of JavaScript lets developers write **stored procedures**, **triggers** and **user defined functions (UDFs)** natively in an [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span></span> <span data-ttu-id="af885-107">이렇게 하면 toowrite 데이터베이스 프로그램 응용 프로그램 논리를 제공 하 고 hello 데이터베이스 저장소 파티션을에서 직접 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-107">This allows you toowrite database program application logic that can be shipped and executed directly on hello database storage partitions.</span></span> 

<span data-ttu-id="af885-108">권장 가져오기에 의해 시작 시청 hello 다음 비디오, Andrew 무역 ㈜ 간략 한 소개 tooCosmos DB의 서버 쪽 데이터베이스 프로그래밍 모델을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-108">We recommend getting started by watching hello following video, where Andrew Liu provides a brief introduction tooCosmos DB's server-side database programming model.</span></span> 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

<span data-ttu-id="af885-109">에서 반환 toothis 문서 hello 답변 toohello 다음 질문을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="af885-109">Then, return toothis article, where you'll learn hello answers toohello following questions:</span></span>  

* <span data-ttu-id="af885-110">JavaScript를 사용해서 저장 프로시저, 트리거 또는 UDF를 작성하는 방법은 무엇인가?</span><span class="sxs-lookup"><span data-stu-id="af885-110">How do I write a a stored procedure, trigger, or UDF using JavaScript?</span></span>
* <span data-ttu-id="af885-111">Cosmos DB는 ACID를 어떻게 보장하나요?</span><span class="sxs-lookup"><span data-stu-id="af885-111">How does Cosmos DB guarantee ACID?</span></span>
* <span data-ttu-id="af885-112">Cosmos DB에서 트랜잭션이 어떻게 작동하나요?</span><span class="sxs-lookup"><span data-stu-id="af885-112">How do transactions work in Cosmos DB?</span></span>
* <span data-ttu-id="af885-113">사전 트리거 및 사후 트리거는 무엇이고 어떻게 작성하는가?</span><span class="sxs-lookup"><span data-stu-id="af885-113">What are pre-triggers and post-triggers and how do I write one?</span></span>
* <span data-ttu-id="af885-114">HTTP를 사용해서 RESTful 방식으로 저장 프로시저, 트리거 또는 UDF를 등록하고 실행하는 방법은 무엇인가?</span><span class="sxs-lookup"><span data-stu-id="af885-114">How do I register and execute a stored procedure, trigger, or UDF in a RESTful manner by using HTTP?</span></span>
* <span data-ttu-id="af885-115">Cosmos DB Sdk는 사용 가능한 toocreate와 실행 저장 프로시저, 트리거 및 Udf?</span><span class="sxs-lookup"><span data-stu-id="af885-115">What Cosmos DB SDKs are available toocreate and execute stored procedures, triggers, and UDFs?</span></span>

## <a name="introduction-toostored-procedure-and-udf-programming"></a><span data-ttu-id="af885-116">소개 tooStored 프로시저 및 UDF 프로그래밍</span><span class="sxs-lookup"><span data-stu-id="af885-116">Introduction tooStored Procedure and UDF Programming</span></span>
<span data-ttu-id="af885-117">이 접근 방식을 *"는 최신 하루 T-SQL JavaScript"* 형식 시스템 불일치 및 개체-관계형 매핑 기술 hello 복잡성에서 응용 프로그램 개발자를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-117">This approach of *“JavaScript as a modern day T-SQL”* frees application developers from hello complexities of type system mismatches and object-relational mapping technologies.</span></span> <span data-ttu-id="af885-118">또한 여러 과소 toobuild 다양 한 응용 프로그램 일 수 있는 내장 장점에:</span><span class="sxs-lookup"><span data-stu-id="af885-118">It also has a number of intrinsic advantages that can be utilized toobuild rich applications:</span></span>  

* <span data-ttu-id="af885-119">**절차적 논리 없이:** 높은 수준의 프로그래밍 언어로 JavaScript 풍부 하 고 친숙 한 인터페이스 tooexpress 비즈니스 논리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-119">**Procedural Logic:** JavaScript as a high level programming language, provides a rich and familiar interface tooexpress business logic.</span></span> <span data-ttu-id="af885-120">작업 자세히 toohello 데이터의 복잡 한 시퀀스를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-120">You can perform complex sequences of operations closer toohello data.</span></span>
* <span data-ttu-id="af885-121">**원자성 트랜잭션:** Cosmos DB는 단일 저장 프로시저 또는 트리거 내에서 수행되는 데이터베이스 작업의 원자성을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-121">**Atomic Transactions:** Cosmos DB guarantees that database operations performed inside a single stored procedure or trigger are atomic.</span></span> <span data-ttu-id="af885-122">따라서 응용 프로그램이 관련 작업을 단일 배치로 결합하여 모두 성공하거나 모두 실패하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-122">This lets an application combine related operations in a single batch so that either all of them succeed or none of them succeed.</span></span> 
* <span data-ttu-id="af885-123">**성능:** hello 버퍼에서 JSON은 기본적으로 매핑된 toohello Javascript 언어 형식 시스템 및 Cosmos DB에는 저장소의 기본 단위 hello 허용 JSON의 구체화를 지연과 같은 최적화 수 이기도 hello 팩트 문서 풀과 쉽게 사용할 수 있는 주문형 toohello 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-123">**Performance:** hello fact that JSON is intrinsically mapped toohello Javascript language type system and is also hello basic unit of storage in Cosmos DB allows for a number of optimizations like lazy materialization of JSON documents in hello buffer pool and making them available on-demand toohello executing code.</span></span> <span data-ttu-id="af885-124">배송 비즈니스 논리 toohello 데이터베이스와 관련 된 성능 이점이 더 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-124">There are more performance benefits associated with shipping business logic toohello database:</span></span>
  
  * <span data-ttu-id="af885-125">일괄 처리 – 개발자가 삽입 등의 작업을 그룹화하여 대량 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-125">Batching – Developers can group operations like inserts and submit them in bulk.</span></span> <span data-ttu-id="af885-126">hello 네트워크 트래픽 대기 시간이 비용과 hello 저장소 오버 헤드 toocreate 별도 트랜잭션을 크게 감소 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af885-126">hello network traffic latency cost and hello store overhead toocreate separate transactions are reduced significantly.</span></span> 
  * <span data-ttu-id="af885-127">미리 컴파일-저장된 프로시저, 트리거 및 사용자 정의 함수 (Udf) tooavoid 각 호출에 대해 JavaScript 컴파일 비용 Cosmos DB 미리 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-127">Pre-compilation – Cosmos DB precompiles stored procedures, triggers and user defined functions (UDFs) tooavoid JavaScript compilation cost for each invocation.</span></span> <span data-ttu-id="af885-128">hello 오버 헤드의 절차적 논리 없이 hello에 대 한 hello 바이트 코드를 작성 상환 tooa 최소 값입니다.</span><span class="sxs-lookup"><span data-stu-id="af885-128">hello overhead of building hello byte code for hello procedural logic is amortized tooa minimal value.</span></span>
  * <span data-ttu-id="af885-129">시퀀싱 – 보조 저장소 작업을 하나 또는 많이 수행하는 파생 작업("트리거")이 필요한 작업이 많습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-129">Sequencing – Many operations need a side-effect (“trigger”) that potentially involves doing one or many secondary store operations.</span></span> <span data-ttu-id="af885-130">원자성을 외에도이 형식의 성능이 더 우수는 toohello 서버를 이동할 때.</span><span class="sxs-lookup"><span data-stu-id="af885-130">Aside from atomicity, this is more performant when moved toohello server.</span></span> 
* <span data-ttu-id="af885-131">**캡슐화:** 저장 프로시저는 한 곳에 사용 되는 toogroup 비즈니스 논리 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-131">**Encapsulation:** Stored procedures can be used toogroup business logic in one place.</span></span> <span data-ttu-id="af885-132">다음 두 가지 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-132">This has two advantages:</span></span>
  * <span data-ttu-id="af885-133">데이터 설계자 tooevolve hello 데이터에서 독립적으로 응용 프로그램 수 있는 hello 원시 데이터를 기반으로 추상화 계층을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-133">It adds an abstraction layer on top of hello raw data, which enables data architects tooevolve their applications independently from hello data.</span></span> <span data-ttu-id="af885-134">Hello 데이터가 toohello 불안정 가정 toobe hello 응용 프로그램으로 처리 된 데이터와 함께 toodeal 직접 있는 경우 필요할 수 있는 기한 스키마 없는 경우 특히 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-134">This is particularly advantageous when hello data is schema-less, due toohello brittle assumptions that may need toobe baked into hello application if they have toodeal with data directly.</span></span>  
  * <span data-ttu-id="af885-135">이 추상화 hello 스크립트에서 hello 액세스를 간소화 하 여 자신의 데이터 보안을 유지 하는 기업 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-135">This abstraction lets enterprises keep their data secure by streamlining hello access from hello scripts.</span></span>  

<span data-ttu-id="af885-136">hello 데이터베이스 트리거, 저장된 프로시저 및 사용자 지정 쿼리 연산자의 생성 및 실행 통해 지원 됩니다 hello [REST API](/rest/api/documentdb/), [Azure DocumentDB 스튜디오](https://github.com/mingaliu/DocumentDBStudio/releases), 및 [Sdk클라이언트](documentdb-sdk-dotnet.md) .NET, Node.js 및 JavaScript를 포함 하 여 많은 플랫폼에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-136">hello creation and execution of database triggers, stored procedure and custom query operators is supported through hello [REST API](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), and [client SDKs](documentdb-sdk-dotnet.md) in many platforms including .NET, Node.js and JavaScript.</span></span>

<span data-ttu-id="af885-137">이 자습서에서는 hello [Q 프라미스를 통해 Node.js SDK](http://azure.github.io/azure-documentdb-node-q/) tooillustrate 저장된 프로시저, 트리거 및 Udf의 구문 및 사용법입니다.</span><span class="sxs-lookup"><span data-stu-id="af885-137">This tutorial uses hello [Node.js SDK with Q Promises](http://azure.github.io/azure-documentdb-node-q/) tooillustrate syntax and usage of stored procedures, triggers, and UDFs.</span></span>   

## <a name="stored-procedures"></a><span data-ttu-id="af885-138">저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="af885-138">Stored procedures</span></span>
### <a name="example-write-a-simple-stored-procedure"></a><span data-ttu-id="af885-139">예: 간단한 저장 프로시저 작성</span><span class="sxs-lookup"><span data-stu-id="af885-139">Example: Write a simple stored procedure</span></span>
<span data-ttu-id="af885-140">먼저 "Hello World" 응답을 반환하는 단순한 저장 프로시저로 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-140">Let’s start with a simple stored procedure that returns a “Hello World” response.</span></span>

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


<span data-ttu-id="af885-141">저장 프로시저는 컬렉션당 등록되며 해당 컬렉션에 있는 모든 문서 및 첨부 파일에 대해 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-141">Stored procedures are registered per collection, and can operate on any document and attachment present in that collection.</span></span> <span data-ttu-id="af885-142">hello 다음 코드 조각에서는 tooregister hello helloWorld 컬렉션을 사용 하 여 프로시저를 저장 하는 방법을</span><span class="sxs-lookup"><span data-stu-id="af885-142">hello following snippet shows how tooregister hello helloWorld stored procedure with a collection.</span></span> 

    // register hello stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


<span data-ttu-id="af885-143">Hello 저장 프로시저 등록 되 면 hello 컬렉션에 대해 실행 하 고 hello 클라이언트에서 다시 hello 결과 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-143">Once hello stored procedure is registered, we can execute it against hello collection, and read hello results back at hello client.</span></span> 

    // execute hello stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


<span data-ttu-id="af885-144">hello 컨텍스트 개체는 tooall 작업 toohello 요청 및 응답 개체에 액세스할 수 있을 뿐 아니라 Cosmos DB 저장소에서 수행할 수 있는 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-144">hello context object provides access tooall operations that can be performed on Cosmos DB storage, as well as access toohello request and response objects.</span></span> <span data-ttu-id="af885-145">이 경우 보낸 백 toohello 클라이언트 hello 응답의 hello 응답 개체 tooset hello 본문을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-145">In this case, we used hello response object tooset hello body of hello response that was sent back toohello client.</span></span> <span data-ttu-id="af885-146">자세한 내용은 참조 toohello [Azure Cosmos DB JavaScript 서버 SDK 설명서](http://azure.github.io/azure-documentdb-js-server/)합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-146">For more details, refer toohello [Azure Cosmos DB JavaScript server SDK documentation](http://azure.github.io/azure-documentdb-js-server/).</span></span>  

<span data-ttu-id="af885-147">주세요이 예제에서 확장 하 고 그 밖의 관련된 기능 데이터베이스 추가 toohello 저장 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="af885-147">Let us expand on this example and add more database related functionality toohello stored procedure.</span></span> <span data-ttu-id="af885-148">저장된 프로시저 수 만들고, 업데이트, 읽기, 쿼리 하 고 문서와 hello 컬렉션 내 첨부 파일을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-148">Stored procedures can create, update, read, query and delete documents and attachments inside hello collection.</span></span>    

### <a name="example-write-a-stored-procedure-toocreate-a-document"></a><span data-ttu-id="af885-149">예: 저장된 프로시저 toocreate는 문서를 작성</span><span class="sxs-lookup"><span data-stu-id="af885-149">Example: Write a stored procedure toocreate a document</span></span>
<span data-ttu-id="af885-150">다음 코드 조각 hello toouse Cosmos DB 리소스가 있는 상황에 맞는 개체 toointeract hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="af885-150">hello next snippet shows how toouse hello context object toointeract with Cosmos DB resources.</span></span>

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


<span data-ttu-id="af885-151">이 저장된 프로시저는 입력된 documentToCreate, hello 현재 컬렉션에서 만든 문서 toobe hello 본문으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-151">This stored procedure takes as input documentToCreate, hello body of a document toobe created in hello current collection.</span></span> <span data-ttu-id="af885-152">이러한 모든 작업은 비동기이며 JavaScript 함수 콜백에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="af885-152">All such operations are asynchronous and depend on JavaScript function callbacks.</span></span> <span data-ttu-id="af885-153">hello 콜백 함수 hello 작업이 실패 하면이 고 hello에 대 한 개체를 만든 경우 hello error 개체에 대해 하나씩 두 개의 매개 변수를에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-153">hello callback function has two parameters, one for hello error object in case hello operation fails, and one for hello created object.</span></span> <span data-ttu-id="af885-154">Hello 콜백 내부 사용자 hello 예외를 처리 하거나 오류를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-154">Inside hello callback, users can either handle hello exception or throw an error.</span></span> <span data-ttu-id="af885-155">콜백을 제공 하지 않으면이 고 오류가 있으면에 경우 hello Azure Cosmos DB 런타임 오류를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-155">In case a callback is not provided and there is an error, hello Azure Cosmos DB runtime throws an error.</span></span>   

<span data-ttu-id="af885-156">Hello 위의 예에서 hello 콜백 hello 작업이 실패 한 경우 오류를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-156">In hello example above, hello callback throws an error if hello operation failed.</span></span> <span data-ttu-id="af885-157">그렇지 않으면 hello 응답 toohello 클라이언트의 hello 본문으로 문서를 작성 하는 hello의 hello id를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-157">Otherwise, it sets hello id of hello created document as hello body of hello response toohello client.</span></span> <span data-ttu-id="af885-158">다음은 이 저장 프로시저가 입력 매개 변수를 사용하여 실행되는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="af885-158">Here is how this stored procedure is executed with input parameters.</span></span>

    // register hello stored procedure
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', createDocumentStoredProc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;

            // run stored procedure toocreate a document
            var docToCreate = {
                id: "DocFromSproc",
                book: "hello Hitchhiker’s Guide toohello Galaxy",
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


<span data-ttu-id="af885-159">참고가 저장 프로시저는 입력으로 문서 본문의 배열이 수정된 tootake 수 있으며 저장 동일 hello에서 모든 만들 여러 네트워크 대신 프로시저 실행 개별적으로 각 toocreate 그중에서 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-159">Note that this stored procedure can be modified tootake an array of document bodies as input and create them all in hello same stored procedure execution instead of multiple network requests toocreate each of them individually.</span></span> <span data-ttu-id="af885-160">이 사용 되는 tooimplement Cosmos DB (이 자습서의 뒷부분에서 설명)에 대 한 효율적인 대량 가져오기 도구를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-160">This can be used tooimplement an efficient bulk importer for Cosmos DB (discussed later in this tutorial).</span></span>   

<span data-ttu-id="af885-161">설명 된 hello 예제 toouse 프로시저를 저장 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="af885-161">hello example described demonstrated how toouse stored procedures.</span></span> <span data-ttu-id="af885-162">트리거 및 사용자 정의 함수 (Udf) hello 자습서의 뒷부분에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-162">We will cover triggers and user defined functions (UDFs) later in hello tutorial.</span></span>

## <a name="database-program-transactions"></a><span data-ttu-id="af885-163">데이터베이스 프로그램 트랜잭션</span><span class="sxs-lookup"><span data-stu-id="af885-163">Database program transactions</span></span>
<span data-ttu-id="af885-164">일반적인 데이터베이스의 트랜잭션은 하나의 논리적 작업 단위로 수행되는 작업 시퀀스로 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-164">Transaction in a typical database can be defined as a sequence of operations performed as a single logical unit of work.</span></span> <span data-ttu-id="af885-165">각 트랜잭션에서 **ACID 보장**을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-165">Each transaction provides **ACID guarantees**.</span></span> <span data-ttu-id="af885-166">ACID는 원자성, 일관성, 격리 및 내구성의 네 가지 속성을 나타내는 잘 알려진 머리글자어입니다.</span><span class="sxs-lookup"><span data-stu-id="af885-166">ACID is a well-known acronym that stands for four properties -  Atomicity, Consistency, Isolation and Durability.</span></span>  

<span data-ttu-id="af885-167">간단히 말해서 원자성 트랜잭션 내에 수행 된 모든 hello 작업으로 하나의 단위로 처리 됩니다 여기서 중 하나가 해당 내용을 모두 커밋됩니다 또는 none입니다.</span><span class="sxs-lookup"><span data-stu-id="af885-167">Briefly, atomicity guarantees that all hello work done inside a transaction is treated as a single unit where either all of it is committed or none.</span></span> <span data-ttu-id="af885-168">일관성은 hello 데이터를 항상 내부 상태가 정상 트랜잭션에 걸쳐 않았는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-168">Consistency makes sure that hello data is always in a good internal state across transactions.</span></span> <span data-ttu-id="af885-169">격리는 두 개의 트랜잭션이 서로 충돌할 – 일반적으로, 대부분의 상용 시스템 제공 hello 응용 프로그램 요구 사항에 따라 사용할 수 있는 여러 격리 수준을 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-169">Isolation guarantees that no two transactions interfere with each other – generally, most commercial systems provide multiple isolation levels that can be used based on hello application needs.</span></span> <span data-ttu-id="af885-170">내구성은 hello 데이터베이스에서 커밋된 모든 변경 내용이 항상 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-170">Durability ensures that any change that’s committed in hello database will always be present.</span></span>   

<span data-ttu-id="af885-171">Cosmos db에서 JavaScript hello에서 호스팅되는 hello 데이터베이스와 동일한 메모리 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="af885-171">In Cosmos DB, JavaScript is hosted in hello same memory space as hello database.</span></span> <span data-ttu-id="af885-172">따라서 저장된 프로시저 및 트리거 내에서 수행 된 요청의 실행 hello에 동일한 데이터베이스 세션의 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="af885-172">Hence, requests made within stored procedures and triggers execute in hello same scope of a database session.</span></span> <span data-ttu-id="af885-173">이렇게 하면 하나의 저장된 프로시저/트리거의 일부인 모든 작업에 대해 Cosmos DB tooguarantee를 ACID 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-173">This enables Cosmos DB tooguarantee ACID for all operations that are part of a single stored procedure/trigger.</span></span> <span data-ttu-id="af885-174">Hello 다음 사항을 고려 프로시저 정의 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-174">Consider hello following stored procedure definition:</span></span>

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

                    if (documents.length != 1) throw "Unable toofind both names";
                    player1Document = documents[0];

                    var filterQuery2 = 'SELECT * FROM Players p where p.id = "' + playerId2 + '"';
                    var accept2 = collection.queryDocuments(collection.getSelfLink(), filterQuery2, {},
                        function (err2, documents2, responseOptions2) {
                            if (err2) throw new Error("Error" + err2.message);
                            if (documents2.length != 1) throw "Unable toofind both names";
                            player2Document = documents2[0];
                            swapItems(player1Document, player2Document);
                            return;
                        });
                    if (!accept2) throw "Unable tooread player details, abort ";
                });

            if (!accept) throw "Unable tooread player details, abort ";

            // swap hello two players’ items
            function swapItems(player1, player2) {
                var player1ItemSave = player1.item;
                player1.item = player2.item;
                player2.item = player1ItemSave;

                var accept = collection.replaceDocument(player1._self, player1,
                    function (err, docReplaced) {
                        if (err) throw "Unable tooupdate player 1, abort ";

                        var accept2 = collection.replaceDocument(player2._self, player2,
                            function (err2, docReplaced2) {
                                if (err) throw "Unable tooupdate player 2, abort"
                            });

                        if (!accept2) throw "Unable tooupdate player 2, abort";
                    });

                if (!accept) throw "Unable tooupdate player 1, abort";
            }
        }
    }

    // register hello stored procedure in Node.js client
    client.createStoredProcedureAsync(collection._self, exchangeItemsSproc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;
        }
    );

<span data-ttu-id="af885-175">이 저장된 프로시저는 한 번에 두 플레이어 간에 게임 앱 tootrade 항목 내에서 트랜잭션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-175">This stored procedure uses transactions within a gaming app tootrade items between two players in a single operation.</span></span> <span data-ttu-id="af885-176">hello는 프로시저 시도 tooread 두 문서는 인수로 전달 된 각 해당 toohello 플레이어 Id를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-176">hello stored procedure attempts tooread two documents each corresponding toohello player IDs passed in as an argument.</span></span> <span data-ttu-id="af885-177">두 플레이어 문서 발견 되 면 해당 항목을 교체 하 여 hello 문서 업데이트 hello 저장 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="af885-177">If both player documents are found, then hello stored procedure updates hello documents by swapping their items.</span></span> <span data-ttu-id="af885-178">Hello 과정 오류가 발생 하면 암시적으로 hello 트랜잭션을 중단 하는 JavaScript 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-178">If any errors are encountered along hello way, it throws a JavaScript exception that implicitly aborts hello transaction.</span></span>

<span data-ttu-id="af885-179">Hello 컬렉션 hello 저장 프로시저는 등록은 단일 파티션 컬렉션에 대 한 경우 hello 트랜잭션은 hello 컬렉션 내에서 범위 지정 된 tooall hello 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="af885-179">If hello collection hello stored procedure is registered against is a single-partition collection, then hello transaction is scoped tooall hello documents within hello collection.</span></span> <span data-ttu-id="af885-180">Hello 컬렉션 분할 된 경우 저장된 프로시저는 단일 파티션 키의 hello 트랜잭션 범위에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af885-180">If hello collection is partitioned, then stored procedures are executed in hello transaction scope of a single partition key.</span></span> <span data-ttu-id="af885-181">각 저장 프로시저 실행 그런 다음에서 해당 toohello 범위 hello 트랜잭션이 실행 되어야 하는 파티션 키 값을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-181">Each stored procedure execution must then include a partition key value corresponding toohello scope hello transaction must run under.</span></span> <span data-ttu-id="af885-182">자세한 내용은 [Azure Cosmos DB 분할](partition-data.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af885-182">For more details, see [Azure Cosmos DB Partitioning](partition-data.md).</span></span>

### <a name="commit-and-rollback"></a><span data-ttu-id="af885-183">커밋 및 롤백</span><span class="sxs-lookup"><span data-stu-id="af885-183">Commit and rollback</span></span>
<span data-ttu-id="af885-184">트랜잭션은 기본적으로 Cosmos DB의 JavaScript 프로그래밍 모델에 전체 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="af885-184">Transactions are deeply and natively integrated into Cosmos DB’s JavaScript programming model.</span></span> <span data-ttu-id="af885-185">JavaScript 함수 내부에서 모든 작업은 자동으로 단일 트랜잭션 아래에 래핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="af885-185">Inside a JavaScript function, all operations are automatically wrapped under a single transaction.</span></span> <span data-ttu-id="af885-186">Hello JavaScript 완료 된 모든 예외 없이 hello operations toohello 데이터베이스가 커밋됩니다.</span><span class="sxs-lookup"><span data-stu-id="af885-186">If hello JavaScript completes without any exception, hello operations toohello database are committed.</span></span> <span data-ttu-id="af885-187">사실상 관계형 데이터베이스에서 hello "BEGIN TRANSACTION" 및 "트랜잭션 커밋" 명령문은 Cosmos DB에서 암시적입니다.</span><span class="sxs-lookup"><span data-stu-id="af885-187">In effect, hello “BEGIN TRANSACTION” and “COMMIT TRANSACTION” statements in relational databases are implicit in Cosmos DB.</span></span>  

<span data-ttu-id="af885-188">Hello 스크립트에서 전파 되는 모든 예외가 있는 경우 Cosmos DB JavaScript 런타임은 hello 전체 트랜잭션을 롤백합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-188">If there is any exception that’s propagated from hello script, Cosmos DB’s JavaScript runtime will roll back hello whole transaction.</span></span> <span data-ttu-id="af885-189">앞에서 보았듯이 hello에 예제에서는 예외를 throw 효과적으로 동일한 tooa Cosmos db에서 "ROLLBACK TRANSACTION"입니다.</span><span class="sxs-lookup"><span data-stu-id="af885-189">As shown in hello earlier example, throwing an exception is effectively equivalent tooa “ROLLBACK TRANSACTION” in Cosmos DB.</span></span>

### <a name="data-consistency"></a><span data-ttu-id="af885-190">데이터 일관성</span><span class="sxs-lookup"><span data-stu-id="af885-190">Data consistency</span></span>
<span data-ttu-id="af885-191">저장된 프로시저 및 트리거 항상 hello hello Azure Cosmos DB 컨테이너의 주 복제본에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af885-191">Stored procedures and triggers are always executed on hello primary replica of hello Azure Cosmos DB container.</span></span> <span data-ttu-id="af885-192">이렇게 하면 저장 프로시저 내부의 읽기에서 강력한 일관성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-192">This ensures that reads from inside stored procedures offer strong consistency.</span></span> <span data-ttu-id="af885-193">Hello 주 또는 보조 복제본에서 사용자 정의 함수를 사용 하 여 쿼리를 실행할 수 있지만 인지 확인 하는 toomeet hello hello 적절 한 복제본을 선택 하 여 일관성 수준이 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-193">Queries using user defined functions can be executed on hello primary or any secondary replica, but we ensure toomeet hello requested consistency level by choosing hello appropriate replica.</span></span>

## <a name="bounded-execution"></a><span data-ttu-id="af885-194">제한된 예외</span><span class="sxs-lookup"><span data-stu-id="af885-194">Bounded execution</span></span>
<span data-ttu-id="af885-195">지정 된 hello 서버 내에 모든 Cosmos DB 작업이 완료 되어야 요청 시간 제한 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="af885-195">All Cosmos DB operations must complete within hello server specified request timeout duration.</span></span> <span data-ttu-id="af885-196">이 제약 조건에는 tooJavaScript 함수 (저장된 프로시저, 트리거 및 사용자 정의 함수)도 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af885-196">This constraint also applies tooJavaScript functions (stored procedures, triggers and user-defined functions).</span></span> <span data-ttu-id="af885-197">해당 시간 제한 값으로는 작업이 완료 되지 않으면, hello 트랜잭션이 롤백됩니다.</span><span class="sxs-lookup"><span data-stu-id="af885-197">If an operation does not complete with that time limit, hello transaction is rolled back.</span></span> <span data-ttu-id="af885-198">JavaScript 함수 hello 시간 제한 내에 완료 하거나 연속 기반 모델 toobatch/다시 시작 실행을 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-198">JavaScript functions must finish within hello time limit or implement a continuation based model toobatch/resume execution.</span></span>  

<span data-ttu-id="af885-199">저장된 프로시저 및 트리거 toohandle 시간 제한의 순서 toosimplify 개발, 만들기, 읽기, replace 및 문서와 첨부 파일의 삭제) (용 hello 컬렉션 개체에서 모든 함수를 나타내는 부울 값을 반환 하는지 여부를 하는 작업이 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af885-199">In order toosimplify development of stored procedures and triggers toohandle time limits, all functions under hello collection object (for create, read, replace, and delete of documents and attachments) return a Boolean value that represents whether that operation will complete.</span></span> <span data-ttu-id="af885-200">이 값이 false 일 경우는 tooexpire에 대 한 hello 시간 제한 되며 해당 hello 프로시저 실행을 래핑해야 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="af885-200">If this value is false, it is an indication that hello time limit is about tooexpire and that hello procedure must wrap up execution.</span></span>  <span data-ttu-id="af885-201">작업 큐에 대기 중인된 이전 toohello 첫 번째 허용 되지 않은 저장소 작업 toocomplete를 보장 hello 저장 프로시저가 시간 내에 완료 하 고 더 이상 요청을 대기 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-201">Operations queued prior toohello first unaccepted store operation are guaranteed toocomplete if hello stored procedure completes in time and does not queue any more requests.</span></span>  

<span data-ttu-id="af885-202">JavaScript 함수는 리소스 사용에 의해서도 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="af885-202">JavaScript functions are also bounded on resource consumption.</span></span> <span data-ttu-id="af885-203">Cosmos DB 데이터베이스 계정의 사용자를 프로 비전 하는 hello 크기에 따라 컬렉션당 처리량을 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-203">Cosmos DB reserves throughput per collection based on hello provisioned size of a database account.</span></span> <span data-ttu-id="af885-204">처리량은 요청 단위 또는 RU라고 하는 정규화된 CPU, 메모리 및 IO 사용 단위로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="af885-204">Throughput is expressed in terms of a normalized unit of CPU, memory and IO consumption called request units or RUs.</span></span> <span data-ttu-id="af885-205">JavaScript 함수 짧은 시간 동안 RUs의 다 수를 잠재적으로 사용할 수 있으며 hello 컬렉션의 제한에 도달할 경우 속도 제한 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-205">JavaScript functions can potentially use up a large number of RUs within a short time, and might get rate-limited if hello collection’s limit is reached.</span></span> <span data-ttu-id="af885-206">저장된 프로시저를 많이 사용 하는 리소스는 기본 데이터베이스 작업의 격리 된 tooensure 가용성 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-206">Resource intensive stored procedures might also be quarantined tooensure availability of primitive database operations.</span></span>  

### <a name="example-bulk-importing-data-into-a-database-program"></a><span data-ttu-id="af885-207">예: 데이터베이스 프로그램으로 데이터 대량 가져오기</span><span class="sxs-lookup"><span data-stu-id="af885-207">Example: Bulk importing data into a database program</span></span>
<span data-ttu-id="af885-208">다음은 문서 toobulk 가져오기 컬렉션으로 작성 된 저장된 프로시저의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="af885-208">Below is an example of a stored procedure that is written toobulk-import documents into a collection.</span></span> <span data-ttu-id="af885-209">참고 hello 부울 값을 확인 하 여 hello 저장 프로시저 경계가 지정 된 핸들 실행 방법 값의 반환 createDocument를 하 고 사용 하 여 hello hello 저장 프로시저 tootrack 및 다시 시작 진행 상황을 호출할 때마다 일괄 처리에서 삽입 하는 문서 수입니다.</span><span class="sxs-lookup"><span data-stu-id="af885-209">Note how hello stored procedure handles bounded execution by checking hello Boolean return value from createDocument, and then uses hello count of documents inserted in each invocation of hello stored procedure tootrack and resume progress across batches.</span></span>

    function bulkImport(docs) {
        var collection = getContext().getCollection();
        var collectionLink = collection.getSelfLink();

        // hello count of imported docs, also used as current doc index.
        var count = 0;

        // Validate input.
        if (!docs) throw new Error("hello array is undefined or null.");

        var docsLength = docs.length;
        if (docsLength == 0) {
            getContext().getResponse().setBody(0);
        }

        // Call hello create API toocreate a document.
        tryCreate(docs[count], callback);

        // Note that there are 2 exit conditions:
        // 1) hello createDocument request was not accepted. 
        //    In this case hello callback will not be called, we just call setBody and we are done.
        // 2) hello callback was called docs.length times.
        //    In this case all documents were created and we don’t need toocall tryCreate anymore. Just call setBody and we are done.
        function tryCreate(doc, callback) {
            var isAccepted = collection.createDocument(collectionLink, doc, callback);

            // If hello request was accepted, callback will be called.
            // Otherwise report current count back toohello client, 
            // which will call hello script again with remaining set of docs.
            if (!isAccepted) getContext().getResponse().setBody(count);
        }

        // This is called when collection.createDocument is done in order tooprocess hello result.
        function callback(err, doc, options) {
            if (err) throw err;

            // One more document has been inserted, increment hello count.
            count++;

            if (count >= docsLength) {
                // If we created all documents, we are done. Just set hello response.
                getContext().getResponse().setBody(count);
            } else {
                // Create next document.
                tryCreate(docs[count], callback);
            }
        }
    }

## <span data-ttu-id="af885-210"><a id="trigger"></a> 데이터베이스 트리거</span><span class="sxs-lookup"><span data-stu-id="af885-210"><a id="trigger"></a> Database triggers</span></span>
### <a name="database-pre-triggers"></a><span data-ttu-id="af885-211">데이터베이스 사전 트리거</span><span class="sxs-lookup"><span data-stu-id="af885-211">Database pre-triggers</span></span>
<span data-ttu-id="af885-212">Cosmos DB는 문서 작업에 의해 실행되거나 트리거되는 트리거를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-212">Cosmos DB provides triggers that are executed or triggered by an operation on a document.</span></span> <span data-ttu-id="af885-213">예를 들어 hello 문서를 만들기 전에이 사전 트리거가 실행 되도록 한 문서를 만들 경우 사전 트리거를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-213">For example, you can specify a pre-trigger when you are creating a document – this pre-trigger will run before hello document is created.</span></span> <span data-ttu-id="af885-214">hello 다음은 사전 트리거 생성 중인 문서의 사용된 toovalidate hello 속성을 수 있는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="af885-214">hello following is an example of how pre-triggers can be used toovalidate hello properties of a document that is being created:</span></span>

    var validateDocumentContentsTrigger = {
        id: "validateDocumentContents",
        serverScript: function validate() {
            var context = getContext();
            var request = context.getRequest();

            // document toobe created in hello current operation
            var documentToCreate = request.getBody();

            // validate properties
            if (!("timestamp" in documentToCreate)) {
                var ts = new Date();
                documentToCreate["my timestamp"] = ts.getTime();
            }

            // update hello document that will be created
            request.setBody(documentToCreate);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.Create
    }


<span data-ttu-id="af885-215">및 hello 트리거에 Node.js 등록 클라이언트 측 코드에 해당 하는 hello:</span><span class="sxs-lookup"><span data-stu-id="af885-215">And hello corresponding Node.js client-side registration code for hello trigger:</span></span>

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


<span data-ttu-id="af885-216">사전 트리거는 입력 매개 변수를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-216">Pre-triggers cannot have any input parameters.</span></span> <span data-ttu-id="af885-217">hello 요청 개체는 hello 작업과 연결 된 사용된 toomanipulate hello 요청 메시지를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-217">hello request object can be used toomanipulate hello request message associated with hello operation.</span></span> <span data-ttu-id="af885-218">여기서은 문서의 hello 작성 된 hello 사전 트리거 실행 중 이며 JSON 형식으로 만든 hello 문서 toobe hello 요청 메시지 본문에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-218">Here, hello pre-trigger is being run with hello creation of a document, and hello request message body contains hello document toobe created in JSON format.</span></span>   

<span data-ttu-id="af885-219">트리거 등록 되는 경우 사용자로 실행할 수 있는 hello 작업을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-219">When triggers are registered, users can specify hello operations that it can run with.</span></span> <span data-ttu-id="af885-220">이 트리거가 hello 다음은 허용 되지 않습니다 즉 TriggerOperation.Create로 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-220">This trigger was created with TriggerOperation.Create, which means hello following is not permitted.</span></span>

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a><span data-ttu-id="af885-221">데이터베이스 사후 트리거</span><span class="sxs-lookup"><span data-stu-id="af885-221">Database post-triggers</span></span>
<span data-ttu-id="af885-222">사전 트리거와 마찬가지로 사후 트리거는 문서 작업과 연결되며 입력 매개 변수를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-222">Post-triggers, like pre-triggers, are associated with an operation on a document and don’t take any input parameters.</span></span> <span data-ttu-id="af885-223">실행 시 **후** hello 작업이 완료 되 고 toohello 클라이언트 전송 되는 액세스 toohello 응답 메시지가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-223">They run **after** hello operation has completed, and have access toohello response message that is sent toohello client.</span></span>   

<span data-ttu-id="af885-224">다음 예제는 hello 동작의 사후 트리거를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="af885-224">hello following example shows post-triggers in action:</span></span>

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
            if(!accept) throw "Unable tooupdate metadata, abort";

            function updateMetadataCallback(err, documents, responseOptions) {
                if(err) throw new Error("Error" + err.message);
                         if(documents.length != 1) throw 'Unable toofind metadata document';

                         var metadataDocument = documents[0];

                         // update metadata
                         metadataDocument.createdDocuments += 1;
                         metadataDocument.createdNames += " " + createdDocument.id;
                         var accept = collection.replaceDocument(metadataDocument._self,
                               metadataDocument, function(err, docReplaced) {
                                      if(err) throw "Unable tooupdate metadata, abort";
                               });
                         if(!accept) throw "Unable tooupdate metadata, abort";
                         return;                    
            }                                                                                            
        },
        triggerType: TriggerType.Post,
        triggerOperation: TriggerOperation.All
    }


<span data-ttu-id="af885-225">다음 예제는 hello와 같이 hello 트리거를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-225">hello trigger can be registered as shown in hello following sample.</span></span>

    // register post-trigger
    client.createTriggerAsync('dbs/testdb/colls/testColl', updateMetadataTrigger)
        .then(function(createdTrigger) { 
            var docToCreate = { 
                name: "artist_profile_1023",
                artist: "hello Band",
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


<span data-ttu-id="af885-226">이 트리거가 hello 메타 데이터 문서를 쿼리하고 새로 만든 hello 문서에 대 한 세부 정보로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-226">This trigger queries for hello metadata document and updates it with details about hello newly created document.</span></span>  

<span data-ttu-id="af885-227">Toonote는 hello 중요 한 한 가지 **트랜잭션** Cosmos DB에는 트리거를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-227">One thing that is important toonote is hello **transactional** execution of triggers in Cosmos DB.</span></span> <span data-ttu-id="af885-228">이 사후 트리거 hello의 일부분으로 실행 동일한 트랜잭션을 hello 원래 문서 hello 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-228">This post-trigger runs as part of hello same transaction as hello creation of hello original document.</span></span> <span data-ttu-id="af885-229">따라서 면 hello 사후 트리거 (say hello 메타 데이터 문서 수 없습니다 tooupdate 하는 경우)에서 예외를 throw 했습니다 hello 전체 트랜잭션이 실패 하 고 롤백됩니다.</span><span class="sxs-lookup"><span data-stu-id="af885-229">Therefore, if we throw an exception from hello post-trigger (say if we are unable tooupdate hello metadata document), hello whole transaction will fail and be rolled back.</span></span> <span data-ttu-id="af885-230">문서가 만들어지지 않고 예외가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="af885-230">No document will be created, and an exception will be returned.</span></span>  

## <span data-ttu-id="af885-231"><a id="udf"></a>사용자 정의 함수</span><span class="sxs-lookup"><span data-stu-id="af885-231"><a id="udf"></a>User-defined functions</span></span>
<span data-ttu-id="af885-232">사용자 정의 함수 (Udf) 사용 되는 tooextend hello DocumentDB API SQL 쿼리 언어 문법 되 고 사용자 지정 비즈니스 논리를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-232">User-defined functions (UDFs) are used tooextend hello DocumentDB API SQL query language grammar and implement custom business logic.</span></span> <span data-ttu-id="af885-233">UDF는 쿼리 내부에서만 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-233">They can only be called from inside queries.</span></span> <span data-ttu-id="af885-234">이러한 액세스 toohello 컨텍스트 개체를 갖지 않는 하며 toobe 계산 전용 JavaScript로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-234">They do not have access toohello context object and are meant toobe used as compute-only JavaScript.</span></span> <span data-ttu-id="af885-235">따라서 hello Cosmos DB 서비스의 보조 복제본에서 Udf는 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-235">Therefore, UDFs can be run on secondary replicas of hello Cosmos DB service.</span></span>  

<span data-ttu-id="af885-236">hello 다음 샘플 다양 한 수입 대괄호의 비율에 따라 한 UDF toocalculate 수입과 세금 만들고 사용 쿼리 toofind 내 모든 사람 20000 이상 세금에 지불 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-236">hello following sample creates a UDF toocalculate income tax based on rates for various income brackets, and then uses it inside a query toofind all people who paid more than $20,000 in taxes.</span></span>

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


<span data-ttu-id="af885-237">hello UDF는 이후에 hello 다음 예제에서에서와 같은 쿼리에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-237">hello UDF can subsequently be used in queries like in hello following sample:</span></span>

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

## <a name="javascript-language-integrated-query-api"></a><span data-ttu-id="af885-238">JavaScript 언어 통합 쿼리 API</span><span class="sxs-lookup"><span data-stu-id="af885-238">JavaScript language-integrated query API</span></span>
<span data-ttu-id="af885-239">또한 tooissuing 쿼리 DocumentDB의 SQL 문법을 사용 하 여 hello 서버 쪽 SDK 있습니다 sql 지식 없이도 fluent JavaScript 인터페이스를 사용 하 여 최적화 된 tooperform 쿼리를.</span><span class="sxs-lookup"><span data-stu-id="af885-239">In addition tooissuing queries using DocumentDB’s SQL grammar, hello server-side SDK allows you tooperform optimized queries using a fluent JavaScript interface without any knowledge of SQL.</span></span> <span data-ttu-id="af885-240">API 있습니다 tooprogrammatically 빌드 쿼리 조건자 함수 연속 함수에 전달 하 여 hello JavaScript 쿼리는 구문이 친숙 한 tooECMAScript5 배열 기본 제공 항목 및 lodash와 같은 인기 있는 JavaScript 라이브러리와 함께 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-240">hello JavaScript query API allows you tooprogrammatically build queries by passing predicate functions into chainable function calls, with a syntax familiar tooECMAScript5's Array built-ins and popular JavaScript libraries like lodash.</span></span> <span data-ttu-id="af885-241">Hello JavaScript 런타임 toobe Azure Cosmos DB 인덱스를 사용 하 여 효율적으로 실행 하 여 쿼리를 구문 분석 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af885-241">Queries are parsed by hello JavaScript runtime toobe executed efficiently using Azure Cosmos DB’s indices.</span></span>

> [!NOTE]
> <span data-ttu-id="af885-242">`__`(이중 밑줄)이 너무 별칭`getContext().getCollection()`합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-242">`__` (double-underscore) is an alias too`getContext().getCollection()`.</span></span>
> <br/>
> <span data-ttu-id="af885-243">즉, 사용할 수 있습니다 `__` 또는 `getContext().getCollection()` tooaccess hello JavaScript 쿼리 API입니다.</span><span class="sxs-lookup"><span data-stu-id="af885-243">In other words, you can use `__` or `getContext().getCollection()` tooaccess hello JavaScript query API.</span></span>
> 
> 

<span data-ttu-id="af885-244">지원되는 함수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-244">Supported functions include:</span></span>

<ul>
<li><span data-ttu-id="af885-245">
<b>chain() ... .value([callback] [, options])</b>
</span><span class="sxs-lookup"><span data-stu-id="af885-245">
<b>chain() ... .value([callback] [, options])</b>
</span></span><ul>
<li>
<span data-ttu-id="af885-246">value()로 종료되어야 하는 연결된 호출을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-246">Starts a chained call which must be terminated with value().</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="af885-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="af885-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="af885-248">Hello hello 결과 집합으로 순서 toofilter/out 입력된 문서에서에서 true/false를 반환 하는 조건자 함수를 사용 하 여 입력을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-248">Filters hello input using a predicate function which returns true/false in order toofilter in/out input documents into hello resulting set.</span></span> <span data-ttu-id="af885-249">비슷한 tooa 동작 SQL의 WHERE 절.</span><span class="sxs-lookup"><span data-stu-id="af885-249">This behaves similar tooa WHERE clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="af885-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="af885-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="af885-251">각 입력된 항목 tooa JavaScript 개체 또는 값을 매핑하는 변환 함수를 지정 된 투영을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-251">Applies a projection given a transformation function which maps each input item tooa JavaScript object or value.</span></span> <span data-ttu-id="af885-252">SQL에 유사한 tooa SELECT 절 처럼 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-252">This behaves similar tooa SELECT clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="af885-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="af885-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="af885-254">각 입력된 항목에서 hello 단일 속성 값을 추출 하는 지도 대 한 바로 가기입니다.</span><span class="sxs-lookup"><span data-stu-id="af885-254">This is a shortcut for a map which extracts hello value of a single property from each input item.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="af885-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="af885-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="af885-256">평면화 tooa 단일 배열에서 각 입력된 항목의 배열 및 결합 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-256">Combines and flattens arrays from each input item in tooa single array.</span></span> <span data-ttu-id="af885-257">LINQ에서 비슷한 tooSelectMany 처럼 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-257">This behaves similar tooSelectMany in LINQ.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="af885-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="af885-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="af885-259">조건자를 지정 하는 hello를 사용 하 여 오름차순 hello 입력된 문서 스트림에 hello 문서를 정렬 하 여 새 문서 집합을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-259">Produce a new set of documents by sorting hello documents in hello input document stream in ascending order using hello given predicate.</span></span> <span data-ttu-id="af885-260">비슷한 tooa ORDER BY 절 SQL 처럼 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-260">This behaves similar tooa ORDER BY clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="af885-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="af885-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="af885-262">조건자를 지정 하는 hello를 사용 하 여 내림차순으로 hello 입력된 문서 스트림에 hello 문서를 정렬 하 여 새 문서 집합을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-262">Produce a new set of documents by sorting hello documents in hello input document stream in descending order using hello given predicate.</span></span> <span data-ttu-id="af885-263">SQL에 유사한 tooa x DESC ORDER BY 절 처럼 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-263">This behaves similar tooa ORDER BY x DESC clause in SQL.</span></span>
</li>
</ul>
</li>
</ul>


<span data-ttu-id="af885-264">조건자 및/또는 선택기 함수 안에 포함 하는 경우 hello 다음과 같은 JavaScript 구문이 어 자동으로 최적화 된 toorun 직접 Azure Cosmos DB 인덱스:</span><span class="sxs-lookup"><span data-stu-id="af885-264">When included inside predicate and/or selector functions, hello following JavaScript constructs get automatically optimized toorun directly on Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="af885-265">간단한 연산자: = = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span><span class="sxs-lookup"><span data-stu-id="af885-265">Simple operators: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span></span> ~
* <span data-ttu-id="af885-266">리터럴 hello 개체를 포함 한 리터럴: {}</span><span class="sxs-lookup"><span data-stu-id="af885-266">Literals, including hello object literal: {}</span></span>
* <span data-ttu-id="af885-267">var, 반환</span><span class="sxs-lookup"><span data-stu-id="af885-267">var, return</span></span>

<span data-ttu-id="af885-268">다음 JavaScript를 생성 하는 hello Azure Cosmos DB 인덱스에 대 한 최적화 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-268">hello following JavaScript constructs do not get optimized for Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="af885-269">흐름 제어(예: if, for, while)</span><span class="sxs-lookup"><span data-stu-id="af885-269">Control flow (e.g. if, for, while)</span></span>
* <span data-ttu-id="af885-270">함수 호출</span><span class="sxs-lookup"><span data-stu-id="af885-270">Function calls</span></span>

<span data-ttu-id="af885-271">자세한 내용은 [서버 쪽 JSDocs](http://azure.github.io/azure-documentdb-js-server/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af885-271">For more information, please see our [Server-Side JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span></span>

### <a name="example-write-a-stored-procedure-using-hello-javascript-query-api"></a><span data-ttu-id="af885-272">예: hello JavaScript 쿼리 API를 사용 하 여 저장된 프로시저를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-272">Example: Write a stored procedure using hello JavaScript query API</span></span>
<span data-ttu-id="af885-273">아래의 코드 예제는 hello는 저장된 프로시저의 hello 컨텍스트에서 hello JavaScript 쿼리 API를 사용할 수 있는 방법을의 예시입니다.</span><span class="sxs-lookup"><span data-stu-id="af885-273">hello following code sample is an example of how hello JavaScript Query API can be used in hello context of a stored procedure.</span></span> <span data-ttu-id="af885-274">hello 저장된 프로시저는 입력된 매개 변수에서 제공 하 여 문서에 삽입 하 고 업데이트 hello를 사용 하 여 메타 데이터 문서를 `__.filter()` 메서드 minSize, maxSize 및 totalSize hello 입력된 문서 크기 속성을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-274">hello stored procedure inserts a document, given by an input parameter, and updates a metadata document, using hello `__.filter()` method, with minSize, maxSize, and totalSize based upon hello input document's size property.</span></span>

    /**
     * Insert actual doc and update metadata doc: minSize, maxSize, totalSize based on doc.size.
     */
    function insertDocumentAndUpdateMetadata(doc) {
      // HTTP error codes sent tooour callback funciton by DocDB server.
      var ErrorCode = {
        RETRY_WITH: 449,
      }

      var isAccepted = __.createDocument(__.getSelfLink(), doc, {}, function(err, doc, options) {
        if (err) throw err;

        // Check hello doc (ignore docs with invalid/zero size and metaDoc itself) and call updateMetadata.
        if (!doc.isMetadata && doc.size > 0) {
          // Get hello meta document. We keep it in hello same collection. it's hello only doc that has .isMetadata = true.
          var result = __.filter(function(x) {
            return x.isMetadata === true
          }, function(err, feed, options) {
            if (err) throw err;

            // We assume that metadata doc was pre-created and must exist when this script is called.
            if (!feed || !feed.length) throw new Error("Failed toofind hello metadata document.");

            // hello metadata document.
            var metaDoc = feed[0];

            // Update metaDoc.minSize:
            // for 1st document use doc.Size, for all hello rest see if it's less than last min.
            if (metaDoc.minSize == 0) metaDoc.minSize = doc.size;
            else metaDoc.minSize = Math.min(metaDoc.minSize, doc.size);

            // Update metaDoc.maxSize.
            metaDoc.maxSize = Math.max(metaDoc.maxSize, doc.size);

            // Update metaDoc.totalSize.
            metaDoc.totalSize += doc.size;

            // Update/replace hello metadata document in hello store.
            var isAccepted = __.replaceDocument(metaDoc._self, metaDoc, function(err) {
              if (err) throw err;
              // Note: in case concurrent updates causes conflict with ErrorCode.RETRY_WITH, we can't read hello meta again 
              //       and update again because due tooSnapshot isolation we will read same exact version (we are in same transaction).
              //       We have tootake care of that on hello client side.
            });
            if (!isAccepted) throw new Error("replaceDocument(metaDoc) returned false.");
          });
          if (!result.isAccepted) throw new Error("filter for metaDoc returned false.");
        }
      });
      if (!isAccepted) throw new Error("createDocument(actual doc) returned false.");
    }

## <a name="sql-toojavascript-cheat-sheet"></a><span data-ttu-id="af885-275">SQL tooJavascript 치트 시트</span><span class="sxs-lookup"><span data-stu-id="af885-275">SQL tooJavascript cheat sheet</span></span>
<span data-ttu-id="af885-276">hello 다음 표에 표시 다양 한 SQL 쿼리 및 hello 해당 JavaScript 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-276">hello following table presents various SQL queries and hello corresponding JavaScript queries.</span></span>

<span data-ttu-id="af885-277">SQL 쿼리를 사용하는 것과 같이 문서 속성 키(예: `doc.id`)는 소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-277">As with SQL queries, document property keys (e.g. `doc.id`) are case-sensitive.</span></span>

|<span data-ttu-id="af885-278">SQL</span><span class="sxs-lookup"><span data-stu-id="af885-278">SQL</span></span>| <span data-ttu-id="af885-279">JavaScript Query API</span><span class="sxs-lookup"><span data-stu-id="af885-279">JavaScript Query API</span></span>|<span data-ttu-id="af885-280">아래 설명</span><span class="sxs-lookup"><span data-stu-id="af885-280">Description below</span></span>|
|---|---|---|
|<span data-ttu-id="af885-281">SELECT *</span><span class="sxs-lookup"><span data-stu-id="af885-281">SELECT *</span></span><br><span data-ttu-id="af885-282">FROM docs</span><span class="sxs-lookup"><span data-stu-id="af885-282">FROM docs</span></span>| <span data-ttu-id="af885-283">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="af885-283">__.map(function(doc) {</span></span> <br><span data-ttu-id="af885-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span><span class="sxs-lookup"><span data-stu-id="af885-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span></span><br><span data-ttu-id="af885-285">});</span><span class="sxs-lookup"><span data-stu-id="af885-285">});</span></span>|<span data-ttu-id="af885-286">1</span><span class="sxs-lookup"><span data-stu-id="af885-286">1</span></span>|
|<span data-ttu-id="af885-287">SELECT docs.id, docs.message AS msg, docs.actions</span><span class="sxs-lookup"><span data-stu-id="af885-287">SELECT docs.id, docs.message AS msg, docs.actions</span></span> <br><span data-ttu-id="af885-288">FROM docs</span><span class="sxs-lookup"><span data-stu-id="af885-288">FROM docs</span></span>|<span data-ttu-id="af885-289">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="af885-289">__.map(function(doc) {</span></span><br><span data-ttu-id="af885-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="af885-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="af885-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="af885-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="af885-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span><span class="sxs-lookup"><span data-stu-id="af885-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span></span><br><span data-ttu-id="af885-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span><span class="sxs-lookup"><span data-stu-id="af885-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span></span><br><span data-ttu-id="af885-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="af885-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="af885-295">});</span><span class="sxs-lookup"><span data-stu-id="af885-295">});</span></span>|<span data-ttu-id="af885-296">2</span><span class="sxs-lookup"><span data-stu-id="af885-296">2</span></span>|
|<span data-ttu-id="af885-297">SELECT *</span><span class="sxs-lookup"><span data-stu-id="af885-297">SELECT *</span></span><br><span data-ttu-id="af885-298">FROM docs</span><span class="sxs-lookup"><span data-stu-id="af885-298">FROM docs</span></span><br><span data-ttu-id="af885-299">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="af885-299">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="af885-300">__.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="af885-300">__.filter(function(doc) {</span></span><br><span data-ttu-id="af885-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="af885-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="af885-302">});</span><span class="sxs-lookup"><span data-stu-id="af885-302">});</span></span>|<span data-ttu-id="af885-303">3</span><span class="sxs-lookup"><span data-stu-id="af885-303">3</span></span>|
|<span data-ttu-id="af885-304">SELECT *</span><span class="sxs-lookup"><span data-stu-id="af885-304">SELECT *</span></span><br><span data-ttu-id="af885-305">FROM docs</span><span class="sxs-lookup"><span data-stu-id="af885-305">FROM docs</span></span><br><span data-ttu-id="af885-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span><span class="sxs-lookup"><span data-stu-id="af885-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span></span>|<span data-ttu-id="af885-307">__.filter(function(x) {</span><span class="sxs-lookup"><span data-stu-id="af885-307">__.filter(function(x) {</span></span><br><span data-ttu-id="af885-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span><span class="sxs-lookup"><span data-stu-id="af885-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span></span><br><span data-ttu-id="af885-309">});</span><span class="sxs-lookup"><span data-stu-id="af885-309">});</span></span>|<span data-ttu-id="af885-310">4</span><span class="sxs-lookup"><span data-stu-id="af885-310">4</span></span>|
|<span data-ttu-id="af885-311">SELECT docs.id, docs.message AS msg</span><span class="sxs-lookup"><span data-stu-id="af885-311">SELECT docs.id, docs.message AS msg</span></span><br><span data-ttu-id="af885-312">FROM docs</span><span class="sxs-lookup"><span data-stu-id="af885-312">FROM docs</span></span><br><span data-ttu-id="af885-313">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="af885-313">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="af885-314">__.chain()</span><span class="sxs-lookup"><span data-stu-id="af885-314">__.chain()</span></span><br><span data-ttu-id="af885-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="af885-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="af885-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="af885-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="af885-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="af885-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="af885-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="af885-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span></span><br><span data-ttu-id="af885-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="af885-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="af885-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="af885-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="af885-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span><span class="sxs-lookup"><span data-stu-id="af885-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span></span><br><span data-ttu-id="af885-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="af885-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="af885-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="af885-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="af885-324">.value();</span><span class="sxs-lookup"><span data-stu-id="af885-324">.value();</span></span>|<span data-ttu-id="af885-325">5</span><span class="sxs-lookup"><span data-stu-id="af885-325">5</span></span>|
|<span data-ttu-id="af885-326">SELECT VALUE tag</span><span class="sxs-lookup"><span data-stu-id="af885-326">SELECT VALUE tag</span></span><br><span data-ttu-id="af885-327">FROM docs</span><span class="sxs-lookup"><span data-stu-id="af885-327">FROM docs</span></span><br><span data-ttu-id="af885-328">JOIN tag IN docs.Tags</span><span class="sxs-lookup"><span data-stu-id="af885-328">JOIN tag IN docs.Tags</span></span><br><span data-ttu-id="af885-329">ORDER BY docs._ts</span><span class="sxs-lookup"><span data-stu-id="af885-329">ORDER BY docs._ts</span></span>|<span data-ttu-id="af885-330">__.chain()</span><span class="sxs-lookup"><span data-stu-id="af885-330">__.chain()</span></span><br><span data-ttu-id="af885-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="af885-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="af885-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span><span class="sxs-lookup"><span data-stu-id="af885-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span></span><br><span data-ttu-id="af885-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="af885-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="af885-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="af885-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span></span><br><span data-ttu-id="af885-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span><span class="sxs-lookup"><span data-stu-id="af885-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span></span><br><span data-ttu-id="af885-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="af885-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="af885-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span><span class="sxs-lookup"><span data-stu-id="af885-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span></span><br><span data-ttu-id="af885-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span><span class="sxs-lookup"><span data-stu-id="af885-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span></span><br><span data-ttu-id="af885-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span><span class="sxs-lookup"><span data-stu-id="af885-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span></span>|<span data-ttu-id="af885-340">6</span><span class="sxs-lookup"><span data-stu-id="af885-340">6</span></span>|

<span data-ttu-id="af885-341">hello 다음 설명에서는 설명 위의 hello 테이블의 각 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-341">hello following descriptions explain each query in hello table above.</span></span>
1. <span data-ttu-id="af885-342">모든 문서(연속 토큰과 함께 페이지가 매겨진)의 결과는 있는 그대로입니다.</span><span class="sxs-lookup"><span data-stu-id="af885-342">Results in all documents (paginated with continuation token) as is.</span></span>
2. <span data-ttu-id="af885-343">프로젝트 hello id, 메시지 (별칭 toomsg) 및 모든 문서에서 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-343">Projects hello id, message (aliased toomsg), and action from all documents.</span></span>
3. <span data-ttu-id="af885-344">Hello 조건자를 사용 하 여 문서에 대 한 쿼리: id = "X998_Y998"입니다.</span><span class="sxs-lookup"><span data-stu-id="af885-344">Queries for documents with hello predicate: id = "X998_Y998".</span></span>
4. <span data-ttu-id="af885-345">태그 속성 및 태그가 있는 문서에 대 한 쿼리는 hello 값 123이 포함 된 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="af885-345">Queries for documents that have a Tags property and Tags is an array containing hello value 123.</span></span>
5. <span data-ttu-id="af885-346">쿼리는 조건자를 사용 하 여 문서에 대 한 id = "X998_Y998" 다음 프로젝트 hello id 및 메시지 (별칭이 지정 toomsg).</span><span class="sxs-lookup"><span data-stu-id="af885-346">Queries for documents with a predicate, id = "X998_Y998", and then projects hello id and message (aliased toomsg).</span></span>
6. <span data-ttu-id="af885-347">배열 속성 태그를 포함 하는 문서에 대 한 필터링 및 hello _ts timestamp 시스템 속성으로 hello 결과 문서를 정렬 하 고 프로젝트 + hello 태그 배열을 평면화합니다</span><span class="sxs-lookup"><span data-stu-id="af885-347">Filters for documents which have an array property, Tags, and sorts hello resulting documents by hello _ts timestamp system property, and then projects + flattens hello Tags array.</span></span>


## <a name="runtime-support"></a><span data-ttu-id="af885-348">런타임 지원</span><span class="sxs-lookup"><span data-stu-id="af885-348">Runtime support</span></span>
<span data-ttu-id="af885-349">[DocumentDB JavaScript 서버 쪽 API](http://azure.github.io/azure-documentdb-js-server/) hello에 대 한 지원을 제공 대부분 hello의 JavaScript 언어 기능으로 표준화 된 일반 [ECMA 262](http://www.ecma-international.org/publications/standards/Ecma-262.htm)합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-349">[DocumentDB JavaScript server side API](http://azure.github.io/azure-documentdb-js-server/) provides support for hello most of hello mainstream JavaScript language features as standardized by [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span></span>

### <a name="security"></a><span data-ttu-id="af885-350">보안</span><span class="sxs-lookup"><span data-stu-id="af885-350">Security</span></span>
<span data-ttu-id="af885-351">JavaScript 저장 프로시저 및 트리거는 샌드 박싱된 하나의 스크립트의 hello 효과 hello 스냅숏 트랜잭션 격리 hello 데이터베이스 수준에서 수행 하지 않고 다른 toohello 노출 하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-351">JavaScript stored procedures and triggers are sandboxed so that hello effects of one script do not leak toohello other without going through hello snapshot transaction isolation at hello database level.</span></span> <span data-ttu-id="af885-352">hello 런타임 환경 풀링된 있더라도 hello 컨텍스트의 각 실행 후 정리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af885-352">hello runtime environments are pooled but cleaned of hello context after each run.</span></span> <span data-ttu-id="af885-353">따라서 toobe 보장 됩니다 서로 모든 의도 하지 않은 부작용의 안전 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-353">Hence they are guaranteed toobe safe of any unintended side effects from each other.</span></span>

### <a name="pre-compilation"></a><span data-ttu-id="af885-354">사전 컴파일</span><span class="sxs-lookup"><span data-stu-id="af885-354">Pre-compilation</span></span>
<span data-ttu-id="af885-355">저장된 프로시저, 트리거 및 Udf 순서 tooavoid 컴파일 비용에 암시적으로 미리 컴파일된 toohello 바이트 코드 형식 hello 시 각 스크립트 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af885-355">Stored procedures, triggers and UDFs are implicitly precompiled toohello byte code format in order tooavoid compilation cost at hello time of each script invocation.</span></span> <span data-ttu-id="af885-356">이렇게 하면 저장 프로시저 호출이 빠르며 사용 공간이 적습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-356">This ensures invocations of stored procedures are fast and have a low footprint.</span></span>

## <a name="client-sdk-support"></a><span data-ttu-id="af885-357">클라이언트 SDK 지원</span><span class="sxs-lookup"><span data-stu-id="af885-357">Client SDK support</span></span>
<span data-ttu-id="af885-358">에 대 한 추가 toohello DocumentDB API에서에서 [Node.js](documentdb-sdk-node.md) 클라이언트, Azure Cosmos DB에 [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [ JavaScript](http://azure.github.io/azure-documentdb-js/), 및 [Python Sdk](documentdb-sdk-python.md) hello DocumentDB API에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-358">In addition toohello DocumentDB API for [Node.js](documentdb-sdk-node.md) client, Azure Cosmos DB has [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/), and [Python SDKs](documentdb-sdk-python.md) for hello DocumentDB API.</span></span> <span data-ttu-id="af885-359">이러한 SDK를 사용하여 저장 프로시저, 트리거 및 UDF를 만들고 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-359">Stored procedures, triggers and UDFs can be created and executed using any of these SDKs as well.</span></span> <span data-ttu-id="af885-360">hello 방법을 예제와 다음 toocreate 고 hello.NET 클라이언트를 사용 하 여 저장된 프로시저를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-360">hello following example shows how toocreate and execute a stored procedure using hello .NET client.</span></span> <span data-ttu-id="af885-361">저장 프로시저를 JSON으로 및를 다시 읽고 hello.NET 형식 hello로 전달 되는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-361">Note how hello .NET types are passed into hello stored procedure as JSON and read back.</span></span>

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


<span data-ttu-id="af885-362">이 샘플은 어떻게 toouse hello [DocumentDB.NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate 사전 트리거 고 hello 트리거를 사용 된 문서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af885-362">This sample shows how toouse hello [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate a pre-trigger and create a document with hello trigger enabled.</span></span> 

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


<span data-ttu-id="af885-363">다음 예제는 hello toocreate 사용자 함수 (UDF)을 정의 하는 방법을 보여 줍니다 고에서 사용 하 여 한 [DocumentDB API SQL 쿼리](documentdb-sql-query.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-363">And hello following example shows how toocreate a user defined function (UDF) and use it in a [DocumentDB API SQL query](documentdb-sql-query.md).</span></span>

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

## <a name="rest-api"></a><span data-ttu-id="af885-364">REST API</span><span class="sxs-lookup"><span data-stu-id="af885-364">REST API</span></span>
<span data-ttu-id="af885-365">모든 Azure Cosmos DB 작업은 RESTful 방식으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-365">All Azure Cosmos DB operations can be performed in a RESTful manner.</span></span> <span data-ttu-id="af885-366">HTTP POST를 사용하여 저장 프로시저, 트리거 및 사용자 정의 함수를 컬렉션 아래에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-366">Stored procedures, triggers and user-defined functions can be registered under a collection by using HTTP POST.</span></span> <span data-ttu-id="af885-367">hello 다음은 방법의 예로 tooregister 저장된 프로시저:</span><span class="sxs-lookup"><span data-stu-id="af885-367">hello following is an example of how tooregister a stored procedure:</span></span>

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


<span data-ttu-id="af885-368">hello 저장된 프로시저는 등록 된 hello URI에 대 한 POST 요청을 실행 하 여 dbs/testdb/colls/testColl/저장 프로시저와 hello 본문을 포함 하는 저장된 프로시저 toocreate hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-368">hello stored procedure is registered by executing a POST request against hello URI dbs/testdb/colls/testColl/sprocs with hello body containing hello stored procedure toocreate.</span></span> <span data-ttu-id="af885-369">트리거 및 UDF는 각각 /triggers 및 /udfs에 대해 POST를 실행해서 비슷하게 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-369">Triggers and UDFs can be registered similarly by issuing a POST against /triggers and /udfs respectively.</span></span>
<span data-ttu-id="af885-370">그런 다음 해당 리소스 링크에 대해 POST 요청을 실행해서 이 저장 프로시저를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-370">This stored procedure can then be executed by issuing a POST request against its resource link:</span></span>

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of hello Patriarch"}, "Price", 200 ]


<span data-ttu-id="af885-371">여기서 hello 입력된 toohello 저장 프로시저는 hello 요청 본문에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af885-371">Here, hello input toohello stored procedure is passed in hello request body.</span></span> <span data-ttu-id="af885-372">Hello 입력 JSON 배열이 입력된 매개 변수로 전달 되는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-372">Note that hello input is passed as a JSON array of input parameters.</span></span> <span data-ttu-id="af885-373">프로시저는 hello에 대 한 첫 번째 입력은 응답 본문 문서로 저장 하는 hello.</span><span class="sxs-lookup"><span data-stu-id="af885-373">hello stored procedure takes hello first input as a document that is a response body.</span></span> <span data-ttu-id="af885-374">수신 하는 hello 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-374">hello response we receive is as follows:</span></span>

    HTTP/1.1 200 OK

    { 
      name: 'TestDocument',
      book: ‘Autumn of hello Patriarch’,
      id: ‘V7tQANV3rAkDAAAAAAAAAA==‘,
      ts: 1407830727,
      self: ‘dbs/V7tQAA==/colls/V7tQANV3rAk=/docs/V7tQANV3rAkDAAAAAAAAAA==/’,
      etag: ‘6c006596-0000-0000-0000-53e9cac70000’,
      attachments: ‘attachments/’,
      Price: 200
    }


<span data-ttu-id="af885-375">저장 프로시저와 달리 트리거는 직접 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-375">Triggers, unlike stored procedures, cannot be executed directly.</span></span> <span data-ttu-id="af885-376">대신, 문서 작업의 일부로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="af885-376">Instead they are executed as part of an operation on a document.</span></span> <span data-ttu-id="af885-377">요청 HTTP 헤더를 사용 하 여 hello 트리거 toorun을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-377">We can specify hello triggers toorun with a request using HTTP headers.</span></span> <span data-ttu-id="af885-378">hello 요청 toocreate 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="af885-378">hello following is request toocreate a document.</span></span>

    POST https://<url>/docs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT
    x-ms-documentdb-pre-trigger-include: validateDocumentContents 
    x-ms-documentdb-post-trigger-include: bookCreationPostTrigger


    {
       "name": "newDocument",
       “title”: “hello Wizard of Oz”,
       “author”: “Frank Baum”,
       “pages”: 92
    }


<span data-ttu-id="af885-379">여기 hello 요청으로 실행 하는 hello 사전 트리거 toobe hello x-ms-documentdb-pre-trigger-include 헤더에 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af885-379">Here hello pre-trigger toobe run with hello request is specified in hello x-ms-documentdb-pre-trigger-include header.</span></span> <span data-ttu-id="af885-380">마찬가지로 모든 사후 트리거 hello x-ms-documentdb-post-trigger-include 헤더에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af885-380">Correspondingly, any post-triggers are given in hello x-ms-documentdb-post-trigger-include header.</span></span> <span data-ttu-id="af885-381">지정된 요청에 사전 트리거와 사후 트리거를 둘 다 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-381">Note that both pre- and post-triggers can be specified for a given request.</span></span>

## <a name="sample-code"></a><span data-ttu-id="af885-382">샘플 코드</span><span class="sxs-lookup"><span data-stu-id="af885-382">Sample code</span></span>
<span data-ttu-id="af885-383">[GitHub 리포지토리](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples)에서 더 많은 서버 쪽 코드 예제([bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js) 및 [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js) 포함)를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-383">You can find more server-side code examples (including [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), and [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) on our [GitHub repository](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span></span>

<span data-ttu-id="af885-384">Tooshare 놀라운 저장된 프로시저를 선택 하십시오.</span><span class="sxs-lookup"><span data-stu-id="af885-384">Want tooshare your awesome stored procedure?</span></span> <span data-ttu-id="af885-385">끌어오기 요청을 보내주세요.</span><span class="sxs-lookup"><span data-stu-id="af885-385">Please, send us a pull-request!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="af885-386">다음 단계</span><span class="sxs-lookup"><span data-stu-id="af885-386">Next steps</span></span>
<span data-ttu-id="af885-387">를 만든 후 하나 이상의 저장된 프로시저, 트리거 및 사용자 정의 함수 생성 로드 하 고 hello 데이터 탐색기를 사용 하 여 Azure 포털에서에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af885-387">Once you have one or more stored procedures, triggers, and user-defined functions created, you can load them and view them in hello Azure portal using Data Explorer.</span></span>

<span data-ttu-id="af885-388">Hello 다음 살펴보면 참조 및 리소스 Azure Cosmos dB 서버 쪽 프로그래밍에 대 한 자세한 경로 toolearn 프로그램에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="af885-388">You may also find hello following references and resources useful in your path toolearn more about Azure Cosmos dB server-side programming:</span></span>

* [<span data-ttu-id="af885-389">Azure Cosmos DB SDK</span><span class="sxs-lookup"><span data-stu-id="af885-389">Azure Cosmos DB SDKs</span></span>](documentdb-sdk-dotnet.md)
* [<span data-ttu-id="af885-390">DocumentDB 스튜디오</span><span class="sxs-lookup"><span data-stu-id="af885-390">DocumentDB Studio</span></span>](https://github.com/mingaliu/DocumentDBStudio/releases)
* [<span data-ttu-id="af885-391">JSON</span><span class="sxs-lookup"><span data-stu-id="af885-391">JSON</span></span>](http://www.json.org/) 
* [<span data-ttu-id="af885-392">JavaScript ECMA-262</span><span class="sxs-lookup"><span data-stu-id="af885-392">JavaScript ECMA-262</span></span>](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [<span data-ttu-id="af885-393">안전하고 이식 가능한 데이터베이스 확장성</span><span class="sxs-lookup"><span data-stu-id="af885-393">Secure and Portable Database Extensibility</span></span>](http://dl.acm.org/citation.cfm?id=276339) 
* [<span data-ttu-id="af885-394">서비스 지향 데이터베이스 아키텍처</span><span class="sxs-lookup"><span data-stu-id="af885-394">Service Oriented Database Architecture</span></span>](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [<span data-ttu-id="af885-395">Microsoft SQL server에 hello.NET 런타임 호스팅</span><span class="sxs-lookup"><span data-stu-id="af885-395">Hosting hello .NET Runtime in Microsoft SQL server</span></span>](http://dl.acm.org/citation.cfm?id=1007669)

