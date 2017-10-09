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
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a>Azure Cosmos DB 서버 쪽 프로그래밍: 저장 프로시저, 데이터베이스 트리거 및 UDF
Azure Cosmos DB가 언어 통합 트랜잭션 방식으로 JavaScript를 실행하므로 개발자가 기본적으로 [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript로 **저장 프로시저**, **트리거** 및 **UDF(사용자 정의 함수)**를 작성할 수 있는 방법을 알아봅니다. 이렇게 하면 toowrite 데이터베이스 프로그램 응용 프로그램 논리를 제공 하 고 hello 데이터베이스 저장소 파티션을에서 직접 실행할 수 있습니다. 

권장 가져오기에 의해 시작 시청 hello 다음 비디오, Andrew 무역 ㈜ 간략 한 소개 tooCosmos DB의 서버 쪽 데이터베이스 프로그래밍 모델을 제공 합니다. 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

에서 반환 toothis 문서 hello 답변 toohello 다음 질문을 배웁니다.  

* JavaScript를 사용해서 저장 프로시저, 트리거 또는 UDF를 작성하는 방법은 무엇인가?
* Cosmos DB는 ACID를 어떻게 보장하나요?
* Cosmos DB에서 트랜잭션이 어떻게 작동하나요?
* 사전 트리거 및 사후 트리거는 무엇이고 어떻게 작성하는가?
* HTTP를 사용해서 RESTful 방식으로 저장 프로시저, 트리거 또는 UDF를 등록하고 실행하는 방법은 무엇인가?
* Cosmos DB Sdk는 사용 가능한 toocreate와 실행 저장 프로시저, 트리거 및 Udf?

## <a name="introduction-toostored-procedure-and-udf-programming"></a>소개 tooStored 프로시저 및 UDF 프로그래밍
이 접근 방식을 *"는 최신 하루 T-SQL JavaScript"* 형식 시스템 불일치 및 개체-관계형 매핑 기술 hello 복잡성에서 응용 프로그램 개발자를 해제 합니다. 또한 여러 과소 toobuild 다양 한 응용 프로그램 일 수 있는 내장 장점에:  

* **절차적 논리 없이:** 높은 수준의 프로그래밍 언어로 JavaScript 풍부 하 고 친숙 한 인터페이스 tooexpress 비즈니스 논리를 제공 합니다. 작업 자세히 toohello 데이터의 복잡 한 시퀀스를 수행할 수 있습니다.
* **원자성 트랜잭션:** Cosmos DB는 단일 저장 프로시저 또는 트리거 내에서 수행되는 데이터베이스 작업의 원자성을 보장합니다. 따라서 응용 프로그램이 관련 작업을 단일 배치로 결합하여 모두 성공하거나 모두 실패하도록 할 수 있습니다. 
* **성능:** hello 버퍼에서 JSON은 기본적으로 매핑된 toohello Javascript 언어 형식 시스템 및 Cosmos DB에는 저장소의 기본 단위 hello 허용 JSON의 구체화를 지연과 같은 최적화 수 이기도 hello 팩트 문서 풀과 쉽게 사용할 수 있는 주문형 toohello 코드를 실행 합니다. 배송 비즈니스 논리 toohello 데이터베이스와 관련 된 성능 이점이 더 있습니다.
  
  * 일괄 처리 – 개발자가 삽입 등의 작업을 그룹화하여 대량 제출할 수 있습니다. hello 네트워크 트래픽 대기 시간이 비용과 hello 저장소 오버 헤드 toocreate 별도 트랜잭션을 크게 감소 됩니다. 
  * 미리 컴파일-저장된 프로시저, 트리거 및 사용자 정의 함수 (Udf) tooavoid 각 호출에 대해 JavaScript 컴파일 비용 Cosmos DB 미리 컴파일합니다. hello 오버 헤드의 절차적 논리 없이 hello에 대 한 hello 바이트 코드를 작성 상환 tooa 최소 값입니다.
  * 시퀀싱 – 보조 저장소 작업을 하나 또는 많이 수행하는 파생 작업("트리거")이 필요한 작업이 많습니다. 원자성을 외에도이 형식의 성능이 더 우수는 toohello 서버를 이동할 때. 
* **캡슐화:** 저장 프로시저는 한 곳에 사용 되는 toogroup 비즈니스 논리 일 수 있습니다. 다음 두 가지 장점이 있습니다.
  * 데이터 설계자 tooevolve hello 데이터에서 독립적으로 응용 프로그램 수 있는 hello 원시 데이터를 기반으로 추상화 계층을 추가 합니다. Hello 데이터가 toohello 불안정 가정 toobe hello 응용 프로그램으로 처리 된 데이터와 함께 toodeal 직접 있는 경우 필요할 수 있는 기한 스키마 없는 경우 특히 유용 합니다.  
  * 이 추상화 hello 스크립트에서 hello 액세스를 간소화 하 여 자신의 데이터 보안을 유지 하는 기업 수 있습니다.  

hello 데이터베이스 트리거, 저장된 프로시저 및 사용자 지정 쿼리 연산자의 생성 및 실행 통해 지원 됩니다 hello [REST API](/rest/api/documentdb/), [Azure DocumentDB 스튜디오](https://github.com/mingaliu/DocumentDBStudio/releases), 및 [Sdk클라이언트](documentdb-sdk-dotnet.md) .NET, Node.js 및 JavaScript를 포함 하 여 많은 플랫폼에서 합니다.

이 자습서에서는 hello [Q 프라미스를 통해 Node.js SDK](http://azure.github.io/azure-documentdb-node-q/) tooillustrate 저장된 프로시저, 트리거 및 Udf의 구문 및 사용법입니다.   

## <a name="stored-procedures"></a>저장 프로시저
### <a name="example-write-a-simple-stored-procedure"></a>예: 간단한 저장 프로시저 작성
먼저 "Hello World" 응답을 반환하는 단순한 저장 프로시저로 시작하겠습니다.

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


저장 프로시저는 컬렉션당 등록되며 해당 컬렉션에 있는 모든 문서 및 첨부 파일에 대해 작동할 수 있습니다. hello 다음 코드 조각에서는 tooregister hello helloWorld 컬렉션을 사용 하 여 프로시저를 저장 하는 방법을 

    // register hello stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


Hello 저장 프로시저 등록 되 면 hello 컬렉션에 대해 실행 하 고 hello 클라이언트에서 다시 hello 결과 읽을 수 있습니다. 

    // execute hello stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


hello 컨텍스트 개체는 tooall 작업 toohello 요청 및 응답 개체에 액세스할 수 있을 뿐 아니라 Cosmos DB 저장소에서 수행할 수 있는 액세스를 제공 합니다. 이 경우 보낸 백 toohello 클라이언트 hello 응답의 hello 응답 개체 tooset hello 본문을 사용 했습니다. 자세한 내용은 참조 toohello [Azure Cosmos DB JavaScript 서버 SDK 설명서](http://azure.github.io/azure-documentdb-js-server/)합니다.  

주세요이 예제에서 확장 하 고 그 밖의 관련된 기능 데이터베이스 추가 toohello 저장 프로시저입니다. 저장된 프로시저 수 만들고, 업데이트, 읽기, 쿼리 하 고 문서와 hello 컬렉션 내 첨부 파일을 삭제 합니다.    

### <a name="example-write-a-stored-procedure-toocreate-a-document"></a>예: 저장된 프로시저 toocreate는 문서를 작성
다음 코드 조각 hello toouse Cosmos DB 리소스가 있는 상황에 맞는 개체 toointeract hello 하는 방법을 보여 줍니다.

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


이 저장된 프로시저는 입력된 documentToCreate, hello 현재 컬렉션에서 만든 문서 toobe hello 본문으로 사용 합니다. 이러한 모든 작업은 비동기이며 JavaScript 함수 콜백에 따라 달라집니다. hello 콜백 함수 hello 작업이 실패 하면이 고 hello에 대 한 개체를 만든 경우 hello error 개체에 대해 하나씩 두 개의 매개 변수를에 있습니다. Hello 콜백 내부 사용자 hello 예외를 처리 하거나 오류를 throw 합니다. 콜백을 제공 하지 않으면이 고 오류가 있으면에 경우 hello Azure Cosmos DB 런타임 오류를 throw 합니다.   

Hello 위의 예에서 hello 콜백 hello 작업이 실패 한 경우 오류를 throw 합니다. 그렇지 않으면 hello 응답 toohello 클라이언트의 hello 본문으로 문서를 작성 하는 hello의 hello id를 설정 합니다. 다음은 이 저장 프로시저가 입력 매개 변수를 사용하여 실행되는 방법을 보여 줍니다.

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


참고가 저장 프로시저는 입력으로 문서 본문의 배열이 수정된 tootake 수 있으며 저장 동일 hello에서 모든 만들 여러 네트워크 대신 프로시저 실행 개별적으로 각 toocreate 그중에서 요청 합니다. 이 사용 되는 tooimplement Cosmos DB (이 자습서의 뒷부분에서 설명)에 대 한 효율적인 대량 가져오기 도구를 수 있습니다.   

설명 된 hello 예제 toouse 프로시저를 저장 하는 방법을 보여 줍니다. 트리거 및 사용자 정의 함수 (Udf) hello 자습서의 뒷부분에서 설명 합니다.

## <a name="database-program-transactions"></a>데이터베이스 프로그램 트랜잭션
일반적인 데이터베이스의 트랜잭션은 하나의 논리적 작업 단위로 수행되는 작업 시퀀스로 정의할 수 있습니다. 각 트랜잭션에서 **ACID 보장**을 제공합니다. ACID는 원자성, 일관성, 격리 및 내구성의 네 가지 속성을 나타내는 잘 알려진 머리글자어입니다.  

간단히 말해서 원자성 트랜잭션 내에 수행 된 모든 hello 작업으로 하나의 단위로 처리 됩니다 여기서 중 하나가 해당 내용을 모두 커밋됩니다 또는 none입니다. 일관성은 hello 데이터를 항상 내부 상태가 정상 트랜잭션에 걸쳐 않았는지 확인 합니다. 격리는 두 개의 트랜잭션이 서로 충돌할 – 일반적으로, 대부분의 상용 시스템 제공 hello 응용 프로그램 요구 사항에 따라 사용할 수 있는 여러 격리 수준을 보장 합니다. 내구성은 hello 데이터베이스에서 커밋된 모든 변경 내용이 항상 있는지 확인 합니다.   

Cosmos db에서 JavaScript hello에서 호스팅되는 hello 데이터베이스와 동일한 메모리 공간입니다. 따라서 저장된 프로시저 및 트리거 내에서 수행 된 요청의 실행 hello에 동일한 데이터베이스 세션의 범위입니다. 이렇게 하면 하나의 저장된 프로시저/트리거의 일부인 모든 작업에 대해 Cosmos DB tooguarantee를 ACID 수 있습니다. Hello 다음 사항을 고려 프로시저 정의 저장 합니다.

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

이 저장된 프로시저는 한 번에 두 플레이어 간에 게임 앱 tootrade 항목 내에서 트랜잭션을 사용합니다. hello는 프로시저 시도 tooread 두 문서는 인수로 전달 된 각 해당 toohello 플레이어 Id를 저장 합니다. 두 플레이어 문서 발견 되 면 해당 항목을 교체 하 여 hello 문서 업데이트 hello 저장 프로시저입니다. Hello 과정 오류가 발생 하면 암시적으로 hello 트랜잭션을 중단 하는 JavaScript 예외를 throw 합니다.

Hello 컬렉션 hello 저장 프로시저는 등록은 단일 파티션 컬렉션에 대 한 경우 hello 트랜잭션은 hello 컬렉션 내에서 범위 지정 된 tooall hello 문서입니다. Hello 컬렉션 분할 된 경우 저장된 프로시저는 단일 파티션 키의 hello 트랜잭션 범위에서 실행 됩니다. 각 저장 프로시저 실행 그런 다음에서 해당 toohello 범위 hello 트랜잭션이 실행 되어야 하는 파티션 키 값을 포함 해야 합니다. 자세한 내용은 [Azure Cosmos DB 분할](partition-data.md)을 참조하세요.

### <a name="commit-and-rollback"></a>커밋 및 롤백
트랜잭션은 기본적으로 Cosmos DB의 JavaScript 프로그래밍 모델에 전체 통합됩니다. JavaScript 함수 내부에서 모든 작업은 자동으로 단일 트랜잭션 아래에 래핑됩니다. Hello JavaScript 완료 된 모든 예외 없이 hello operations toohello 데이터베이스가 커밋됩니다. 사실상 관계형 데이터베이스에서 hello "BEGIN TRANSACTION" 및 "트랜잭션 커밋" 명령문은 Cosmos DB에서 암시적입니다.  

Hello 스크립트에서 전파 되는 모든 예외가 있는 경우 Cosmos DB JavaScript 런타임은 hello 전체 트랜잭션을 롤백합니다. 앞에서 보았듯이 hello에 예제에서는 예외를 throw 효과적으로 동일한 tooa Cosmos db에서 "ROLLBACK TRANSACTION"입니다.

### <a name="data-consistency"></a>데이터 일관성
저장된 프로시저 및 트리거 항상 hello hello Azure Cosmos DB 컨테이너의 주 복제본에서 실행 됩니다. 이렇게 하면 저장 프로시저 내부의 읽기에서 강력한 일관성을 제공합니다. Hello 주 또는 보조 복제본에서 사용자 정의 함수를 사용 하 여 쿼리를 실행할 수 있지만 인지 확인 하는 toomeet hello hello 적절 한 복제본을 선택 하 여 일관성 수준이 요청 합니다.

## <a name="bounded-execution"></a>제한된 예외
지정 된 hello 서버 내에 모든 Cosmos DB 작업이 완료 되어야 요청 시간 제한 기간입니다. 이 제약 조건에는 tooJavaScript 함수 (저장된 프로시저, 트리거 및 사용자 정의 함수)도 적용 됩니다. 해당 시간 제한 값으로는 작업이 완료 되지 않으면, hello 트랜잭션이 롤백됩니다. JavaScript 함수 hello 시간 제한 내에 완료 하거나 연속 기반 모델 toobatch/다시 시작 실행을 구현 해야 합니다.  

저장된 프로시저 및 트리거 toohandle 시간 제한의 순서 toosimplify 개발, 만들기, 읽기, replace 및 문서와 첨부 파일의 삭제) (용 hello 컬렉션 개체에서 모든 함수를 나타내는 부울 값을 반환 하는지 여부를 하는 작업이 완료 됩니다. 이 값이 false 일 경우는 tooexpire에 대 한 hello 시간 제한 되며 해당 hello 프로시저 실행을 래핑해야 나타냅니다.  작업 큐에 대기 중인된 이전 toohello 첫 번째 허용 되지 않은 저장소 작업 toocomplete를 보장 hello 저장 프로시저가 시간 내에 완료 하 고 더 이상 요청을 대기 하지 않습니다.  

JavaScript 함수는 리소스 사용에 의해서도 제한됩니다. Cosmos DB 데이터베이스 계정의 사용자를 프로 비전 하는 hello 크기에 따라 컬렉션당 처리량을 예약 합니다. 처리량은 요청 단위 또는 RU라고 하는 정규화된 CPU, 메모리 및 IO 사용 단위로 표현됩니다. JavaScript 함수 짧은 시간 동안 RUs의 다 수를 잠재적으로 사용할 수 있으며 hello 컬렉션의 제한에 도달할 경우 속도 제한 될 수 있습니다. 저장된 프로시저를 많이 사용 하는 리소스는 기본 데이터베이스 작업의 격리 된 tooensure 가용성 수도 있습니다.  

### <a name="example-bulk-importing-data-into-a-database-program"></a>예: 데이터베이스 프로그램으로 데이터 대량 가져오기
다음은 문서 toobulk 가져오기 컬렉션으로 작성 된 저장된 프로시저의 예입니다. 참고 hello 부울 값을 확인 하 여 hello 저장 프로시저 경계가 지정 된 핸들 실행 방법 값의 반환 createDocument를 하 고 사용 하 여 hello hello 저장 프로시저 tootrack 및 다시 시작 진행 상황을 호출할 때마다 일괄 처리에서 삽입 하는 문서 수입니다.

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

## <a id="trigger"></a> 데이터베이스 트리거
### <a name="database-pre-triggers"></a>데이터베이스 사전 트리거
Cosmos DB는 문서 작업에 의해 실행되거나 트리거되는 트리거를 제공합니다. 예를 들어 hello 문서를 만들기 전에이 사전 트리거가 실행 되도록 한 문서를 만들 경우 사전 트리거를 지정할 수 있습니다. hello 다음은 사전 트리거 생성 중인 문서의 사용된 toovalidate hello 속성을 수 있는 방법의 예입니다.

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


및 hello 트리거에 Node.js 등록 클라이언트 측 코드에 해당 하는 hello:

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


사전 트리거는 입력 매개 변수를 사용할 수 없습니다. hello 요청 개체는 hello 작업과 연결 된 사용된 toomanipulate hello 요청 메시지를 수 있습니다. 여기서은 문서의 hello 작성 된 hello 사전 트리거 실행 중 이며 JSON 형식으로 만든 hello 문서 toobe hello 요청 메시지 본문에 포함 합니다.   

트리거 등록 되는 경우 사용자로 실행할 수 있는 hello 작업을 지정할 수 있습니다. 이 트리거가 hello 다음은 허용 되지 않습니다 즉 TriggerOperation.Create로 만들어졌습니다.

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a>데이터베이스 사후 트리거
사전 트리거와 마찬가지로 사후 트리거는 문서 작업과 연결되며 입력 매개 변수를 사용하지 않습니다. 실행 시 **후** hello 작업이 완료 되 고 toohello 클라이언트 전송 되는 액세스 toohello 응답 메시지가 있어야 합니다.   

다음 예제는 hello 동작의 사후 트리거를 보여 줍니다.

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


다음 예제는 hello와 같이 hello 트리거를 등록할 수 있습니다.

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


이 트리거가 hello 메타 데이터 문서를 쿼리하고 새로 만든 hello 문서에 대 한 세부 정보로 업데이트 합니다.  

Toonote는 hello 중요 한 한 가지 **트랜잭션** Cosmos DB에는 트리거를 실행 합니다. 이 사후 트리거 hello의 일부분으로 실행 동일한 트랜잭션을 hello 원래 문서 hello 작성 합니다. 따라서 면 hello 사후 트리거 (say hello 메타 데이터 문서 수 없습니다 tooupdate 하는 경우)에서 예외를 throw 했습니다 hello 전체 트랜잭션이 실패 하 고 롤백됩니다. 문서가 만들어지지 않고 예외가 반환됩니다.  

## <a id="udf"></a>사용자 정의 함수
사용자 정의 함수 (Udf) 사용 되는 tooextend hello DocumentDB API SQL 쿼리 언어 문법 되 고 사용자 지정 비즈니스 논리를 구현 합니다. UDF는 쿼리 내부에서만 호출할 수 있습니다. 이러한 액세스 toohello 컨텍스트 개체를 갖지 않는 하며 toobe 계산 전용 JavaScript로 사용 합니다. 따라서 hello Cosmos DB 서비스의 보조 복제본에서 Udf는 실행할 수 있습니다.  

hello 다음 샘플 다양 한 수입 대괄호의 비율에 따라 한 UDF toocalculate 수입과 세금 만들고 사용 쿼리 toofind 내 모든 사람 20000 이상 세금에 지불 합니다.

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


hello UDF는 이후에 hello 다음 예제에서에서와 같은 쿼리에서 사용할 수 있습니다.

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

## <a name="javascript-language-integrated-query-api"></a>JavaScript 언어 통합 쿼리 API
또한 tooissuing 쿼리 DocumentDB의 SQL 문법을 사용 하 여 hello 서버 쪽 SDK 있습니다 sql 지식 없이도 fluent JavaScript 인터페이스를 사용 하 여 최적화 된 tooperform 쿼리를. API 있습니다 tooprogrammatically 빌드 쿼리 조건자 함수 연속 함수에 전달 하 여 hello JavaScript 쿼리는 구문이 친숙 한 tooECMAScript5 배열 기본 제공 항목 및 lodash와 같은 인기 있는 JavaScript 라이브러리와 함께 호출 합니다. Hello JavaScript 런타임 toobe Azure Cosmos DB 인덱스를 사용 하 여 효율적으로 실행 하 여 쿼리를 구문 분석 됩니다.

> [!NOTE]
> `__`(이중 밑줄)이 너무 별칭`getContext().getCollection()`합니다.
> <br/>
> 즉, 사용할 수 있습니다 `__` 또는 `getContext().getCollection()` tooaccess hello JavaScript 쿼리 API입니다.
> 
> 

지원되는 함수는 다음과 같습니다.

<ul>
<li>
<b>chain() ... .value([callback] [, options])</b>
<ul>
<li>
value()로 종료되어야 하는 연결된 호출을 시작합니다.
</li>
</ul>
</li>
<li>
<b>filter(predicateFunction [, options] [, callback])</b>
<ul>
<li>
Hello hello 결과 집합으로 순서 toofilter/out 입력된 문서에서에서 true/false를 반환 하는 조건자 함수를 사용 하 여 입력을 필터링 합니다. 비슷한 tooa 동작 SQL의 WHERE 절.
</li>
</ul>
</li>
<li>
<b>map(transformationFunction [, options] [, callback])</b>
<ul>
<li>
각 입력된 항목 tooa JavaScript 개체 또는 값을 매핑하는 변환 함수를 지정 된 투영을 적용 합니다. SQL에 유사한 tooa SELECT 절 처럼 동작 합니다.
</li>
</ul>
</li>
<li>
<b>pluck([propertyName] [, options] [, callback])</b>
<ul>
<li>
각 입력된 항목에서 hello 단일 속성 값을 추출 하는 지도 대 한 바로 가기입니다.
</li>
</ul>
</li>
<li>
<b>flatten([isShallow] [, options] [, callback])</b>
<ul>
<li>
평면화 tooa 단일 배열에서 각 입력된 항목의 배열 및 결합 합니다. LINQ에서 비슷한 tooSelectMany 처럼 동작 합니다.
</li>
</ul>
</li>
<li>
<b>sortBy([predicate] [, options] [, callback])</b>
<ul>
<li>
조건자를 지정 하는 hello를 사용 하 여 오름차순 hello 입력된 문서 스트림에 hello 문서를 정렬 하 여 새 문서 집합을 생성 합니다. 비슷한 tooa ORDER BY 절 SQL 처럼 동작 합니다.
</li>
</ul>
</li>
<li>
<b>sortByDescending([predicate] [, options] [, callback])</b>
<ul>
<li>
조건자를 지정 하는 hello를 사용 하 여 내림차순으로 hello 입력된 문서 스트림에 hello 문서를 정렬 하 여 새 문서 집합을 생성 합니다. SQL에 유사한 tooa x DESC ORDER BY 절 처럼 동작 합니다.
</li>
</ul>
</li>
</ul>


조건자 및/또는 선택기 함수 안에 포함 하는 경우 hello 다음과 같은 JavaScript 구문이 어 자동으로 최적화 된 toorun 직접 Azure Cosmos DB 인덱스:

* 간단한 연산자: = = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;! ~
* 리터럴 hello 개체를 포함 한 리터럴: {}
* var, 반환

다음 JavaScript를 생성 하는 hello Azure Cosmos DB 인덱스에 대 한 최적화 되지 않습니다.

* 흐름 제어(예: if, for, while)
* 함수 호출

자세한 내용은 [서버 쪽 JSDocs](http://azure.github.io/azure-documentdb-js-server/)를 참조하세요.

### <a name="example-write-a-stored-procedure-using-hello-javascript-query-api"></a>예: hello JavaScript 쿼리 API를 사용 하 여 저장된 프로시저를 작성 합니다.
아래의 코드 예제는 hello는 저장된 프로시저의 hello 컨텍스트에서 hello JavaScript 쿼리 API를 사용할 수 있는 방법을의 예시입니다. hello 저장된 프로시저는 입력된 매개 변수에서 제공 하 여 문서에 삽입 하 고 업데이트 hello를 사용 하 여 메타 데이터 문서를 `__.filter()` 메서드 minSize, maxSize 및 totalSize hello 입력된 문서 크기 속성을 기반으로 합니다.

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

## <a name="sql-toojavascript-cheat-sheet"></a>SQL tooJavascript 치트 시트
hello 다음 표에 표시 다양 한 SQL 쿼리 및 hello 해당 JavaScript 쿼리 합니다.

SQL 쿼리를 사용하는 것과 같이 문서 속성 키(예: `doc.id`)는 소문자를 구분합니다.

|SQL| JavaScript Query API|아래 설명|
|---|---|---|
|SELECT *<br>FROM docs| __.map(function(doc) { <br>&nbsp;&nbsp;&nbsp;&nbsp;return doc;<br>});|1|
|SELECT docs.id, docs.message AS msg, docs.actions <br>FROM docs|__.map(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;return {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions<br>&nbsp;&nbsp;&nbsp;&nbsp;};<br>});|2|
|SELECT *<br>FROM docs<br>WHERE docs.id="X998_Y998"|__.filter(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";<br>});|3|
|SELECT *<br>FROM docs<br>WHERE ARRAY_CONTAINS(docs.Tags, 123)|__.filter(function(x) {<br>&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;<br>});|4|
|SELECT docs.id, docs.message AS msg<br>FROM docs<br>WHERE docs.id="X998_Y998"|__.chain()<br>&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>.value();|5|
|SELECT VALUE tag<br>FROM docs<br>JOIN tag IN docs.Tags<br>ORDER BY docs._ts|__.chain()<br>&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")<br>&nbsp;&nbsp;&nbsp;&nbsp;.flatten()<br>&nbsp;&nbsp;&nbsp;&nbsp;.value()|6|

hello 다음 설명에서는 설명 위의 hello 테이블의 각 쿼리 합니다.
1. 모든 문서(연속 토큰과 함께 페이지가 매겨진)의 결과는 있는 그대로입니다.
2. 프로젝트 hello id, 메시지 (별칭 toomsg) 및 모든 문서에서 작업 합니다.
3. Hello 조건자를 사용 하 여 문서에 대 한 쿼리: id = "X998_Y998"입니다.
4. 태그 속성 및 태그가 있는 문서에 대 한 쿼리는 hello 값 123이 포함 된 배열입니다.
5. 쿼리는 조건자를 사용 하 여 문서에 대 한 id = "X998_Y998" 다음 프로젝트 hello id 및 메시지 (별칭이 지정 toomsg).
6. 배열 속성 태그를 포함 하는 문서에 대 한 필터링 및 hello _ts timestamp 시스템 속성으로 hello 결과 문서를 정렬 하 고 프로젝트 + hello 태그 배열을 평면화합니다


## <a name="runtime-support"></a>런타임 지원
[DocumentDB JavaScript 서버 쪽 API](http://azure.github.io/azure-documentdb-js-server/) hello에 대 한 지원을 제공 대부분 hello의 JavaScript 언어 기능으로 표준화 된 일반 [ECMA 262](http://www.ecma-international.org/publications/standards/Ecma-262.htm)합니다.

### <a name="security"></a>보안
JavaScript 저장 프로시저 및 트리거는 샌드 박싱된 하나의 스크립트의 hello 효과 hello 스냅숏 트랜잭션 격리 hello 데이터베이스 수준에서 수행 하지 않고 다른 toohello 노출 하지 않도록 합니다. hello 런타임 환경 풀링된 있더라도 hello 컨텍스트의 각 실행 후 정리 됩니다. 따라서 toobe 보장 됩니다 서로 모든 의도 하지 않은 부작용의 안전 합니다.

### <a name="pre-compilation"></a>사전 컴파일
저장된 프로시저, 트리거 및 Udf 순서 tooavoid 컴파일 비용에 암시적으로 미리 컴파일된 toohello 바이트 코드 형식 hello 시 각 스크립트 호출 됩니다. 이렇게 하면 저장 프로시저 호출이 빠르며 사용 공간이 적습니다.

## <a name="client-sdk-support"></a>클라이언트 SDK 지원
에 대 한 추가 toohello DocumentDB API에서에서 [Node.js](documentdb-sdk-node.md) 클라이언트, Azure Cosmos DB에 [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [ JavaScript](http://azure.github.io/azure-documentdb-js/), 및 [Python Sdk](documentdb-sdk-python.md) hello DocumentDB API에 대 한 합니다. 이러한 SDK를 사용하여 저장 프로시저, 트리거 및 UDF를 만들고 실행할 수도 있습니다. hello 방법을 예제와 다음 toocreate 고 hello.NET 클라이언트를 사용 하 여 저장된 프로시저를 실행 합니다. 저장 프로시저를 JSON으로 및를 다시 읽고 hello.NET 형식 hello로 전달 되는 방법을 확인 합니다.

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


이 샘플은 어떻게 toouse hello [DocumentDB.NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate 사전 트리거 고 hello 트리거를 사용 된 문서를 만듭니다. 

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


다음 예제는 hello toocreate 사용자 함수 (UDF)을 정의 하는 방법을 보여 줍니다 고에서 사용 하 여 한 [DocumentDB API SQL 쿼리](documentdb-sql-query.md)합니다.

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

## <a name="rest-api"></a>REST API
모든 Azure Cosmos DB 작업은 RESTful 방식으로 수행할 수 있습니다. HTTP POST를 사용하여 저장 프로시저, 트리거 및 사용자 정의 함수를 컬렉션 아래에 등록할 수 있습니다. hello 다음은 방법의 예로 tooregister 저장된 프로시저:

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


hello 저장된 프로시저는 등록 된 hello URI에 대 한 POST 요청을 실행 하 여 dbs/testdb/colls/testColl/저장 프로시저와 hello 본문을 포함 하는 저장된 프로시저 toocreate hello 합니다. 트리거 및 UDF는 각각 /triggers 및 /udfs에 대해 POST를 실행해서 비슷하게 등록할 수 있습니다.
그런 다음 해당 리소스 링크에 대해 POST 요청을 실행해서 이 저장 프로시저를 실행할 수 있습니다.

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of hello Patriarch"}, "Price", 200 ]


여기서 hello 입력된 toohello 저장 프로시저는 hello 요청 본문에 전달 됩니다. Hello 입력 JSON 배열이 입력된 매개 변수로 전달 되는 참고 합니다. 프로시저는 hello에 대 한 첫 번째 입력은 응답 본문 문서로 저장 하는 hello. 수신 하는 hello 응답은 다음과 같습니다.

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


저장 프로시저와 달리 트리거는 직접 실행할 수 없습니다. 대신, 문서 작업의 일부로 실행됩니다. 요청 HTTP 헤더를 사용 하 여 hello 트리거 toorun을 지정할 수 있습니다. hello 요청 toocreate 문서입니다.

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


여기 hello 요청으로 실행 하는 hello 사전 트리거 toobe hello x-ms-documentdb-pre-trigger-include 헤더에 지정 됩니다. 마찬가지로 모든 사후 트리거 hello x-ms-documentdb-post-trigger-include 헤더에 제공 됩니다. 지정된 요청에 사전 트리거와 사후 트리거를 둘 다 지정할 수 있습니다.

## <a name="sample-code"></a>샘플 코드
[GitHub 리포지토리](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples)에서 더 많은 서버 쪽 코드 예제([bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js) 및 [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js) 포함)를 찾을 수 있습니다.

Tooshare 놀라운 저장된 프로시저를 선택 하십시오. 끌어오기 요청을 보내주세요. 

## <a name="next-steps"></a>다음 단계
를 만든 후 하나 이상의 저장된 프로시저, 트리거 및 사용자 정의 함수 생성 로드 하 고 hello 데이터 탐색기를 사용 하 여 Azure 포털에서에서 볼 수 있습니다.

Hello 다음 살펴보면 참조 및 리소스 Azure Cosmos dB 서버 쪽 프로그래밍에 대 한 자세한 경로 toolearn 프로그램에 유용 합니다.

* [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md)
* [DocumentDB 스튜디오](https://github.com/mingaliu/DocumentDBStudio/releases)
* [JSON](http://www.json.org/) 
* [JavaScript ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [안전하고 이식 가능한 데이터베이스 확장성](http://dl.acm.org/citation.cfm?id=276339) 
* [서비스 지향 데이터베이스 아키텍처](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [Microsoft SQL server에 hello.NET 런타임 호스팅](http://dl.acm.org/citation.cfm?id=1007669)

