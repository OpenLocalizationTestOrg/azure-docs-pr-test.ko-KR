---
title: "hello Azure Cosmos DB에 대 한 DocumentDB API에 대 한 aaaNode.js 자습서 | Microsoft Docs"
description: "Node.js 하는 자습서는 Cosmos DB hello DocumentDB API를 사용 하 여 만듭니다."
keywords: "node.js 자습서, 노드 데이터베이스"
services: cosmos-db
documentationcenter: node.js
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: 14d52110-1dce-4ac0-9dd9-f936afccd550
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: node
ms.topic: article
ms.date: 08/14/2017
ms.author: anhoh
ms.openlocfilehash: fce244c6a5f321608e82ca51a2c987e84b98bffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-tutorial-use-hello-documentdb-api-in-azure-cosmos-db-toocreate-a-nodejs-console-application"></a>Node.js 자습서: Azure Cosmos DB toocreate Node.js 콘솔 응용 프로그램에에서 사용 하 여 hello DocumentDB API
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [MongoDB용 Node.js](mongodb-samples.md)
> * [Node.JS](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Hello Azure Cosmos DB Node.js SDK에 대 한 toohello Node.js 자습서를 시작! 이 자습서를 따라 하면 Azure Cosmos DB 리소스를 만들고 쿼리하는 콘솔 응용 프로그램이 생깁니다.

다음에 대해 설명합니다.

* 만들기 및 tooan Azure Cosmos DB 계정 연결
* 응용 프로그램 설정
* 노드 데이터베이스 만들기
* 컬렉션 만들기
* JSON 문서 만들기
* Hello 컬렉션 쿼리
* 문서 바꾸기
* 문서 삭제
* Hello 노드 데이터베이스 삭제

시간이 없으십니까? 염려하지 마십시오. hello 완벽 한 솔루션에 있는 [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started)합니다. 참조 [hello 완벽 한 솔루션을 가져올](#GetSolution) 빠른 지침에 대 한 합니다.

Hello Node.js 자습서를 완료 한 후 하십시오 사용 하 여 hello 투표 하는 단추 hello의 위쪽과 아래쪽 페이지 toogive이에서 us 피드백. 받을지 경우 toocontact를 직접 생각 될 전자 메일 주소 가능한 tooinclude 메모에 있습니다.

이제 시작하겠습니다.

## <a name="prerequisites-for-hello-nodejs-tutorial"></a>Hello Node.js 자습서에 대 한 필수 구성 요소
Hello 다음 항목이 있는지 확인 하십시오.

* 활성 Azure 계정. 아직 구독하지 않은 경우 [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.
    * Hello 또는 사용할 수 있습니다 [Azure Cosmos DB 에뮬레이터](local-emulator.md) 이 자습서에 대 한 합니다.
* [Node.js](https://nodejs.org/) 버전 v0.10.29 이상

## <a name="step-1-create-an-azure-cosmos-db-account"></a>1단계: Azure Cosmos DB 계정 만들기
Azure Cosmos DB 계정을 만들어 보겠습니다. Toouse 원하는 계정을 이미 있는 경우 건너뛰어도 너무[Node.js 응용 프로그램 설정](#SetupNode)합니다. Hello Azure Cosmos DB 에뮬레이터를 사용 하는 경우 hello 단계에 따르십시오 [Azure Cosmos DB 에뮬레이터](local-emulator.md) toosetup 에뮬레이터 hello 및 너무 건너 뛸[Node.js 응용 프로그램 설정](#SetupNode)합니다.

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupNode"></a>2단계: Node.js 응용 프로그램 설치
1. 자주 사용하는 터미널을 엽니다.
2. Node.js 응용을 프로그램 hello 폴더 또는 디렉터리 toosave 하려는 위치를 찾습니다.
3. 다음 명령을 hello로 두 개의 빈 JavaScript 파일을 만듭니다.
   * Windows:
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * Linux/OS X:
     * ```touch app.js```
     * ```touch config.js```
4. Npm 통해 hello documentdb 모듈을 설치 합니다. 다음 명령을 사용 하 여 hello:
   * ```npm install documentdb --save```

잘하셨습니다. 설치를 완료했으므로 코드를 작성해 보겠습니다.

## <a id="Config"></a>3단계: 앱의 구성 설정
원하는 텍스트 편집기에서 ```config.js```을 엽니다.

그런 다음, 복사 및 붙여넣기 hello 아래 코드 조각 및 속성 설정 ```config.endpoint``` 및 ```config.primaryKey``` tooyour Azure Cosmos DB 끝점 uri 및 기본 키입니다. 이러한 두 구성을 모두 hello에서 확인할 수 있습니다 [Azure 포털](https://portal.azure.com)합니다.

![Node.js 자습서-hello Azure Cosmos DB 계정을 활성 허브 hello 표시 하는 Azure 포털의 스크린 샷을 강조 표시 된 hello에 강조 표시 된 hello Azure Cosmos DB 계정 블레이드 및 hello URI, 기본 키와 보조 키 값에 강조 표시 된 hello 키 단추 키 블레이드에서-노드 데이터베이스][keys]

    // ADD THIS PART tooYOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

복사 및 붙여넣기 hello ```database id```, ```collection id```, 및 ```JSON documents``` tooyour ```config``` 설정 하면 개체 아래에 ```config.endpoint``` 및 ```config.authKey``` 속성입니다. 원하는 toostore 데이터베이스의 데이터를 이미 있는 경우 Azure Cosmos DB를 사용할 수 있습니다 [데이터 마이그레이션 도구](import-data.md) hello 문서 정의 추가 하는 대신 합니다.

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

    // ADD THIS PART tooYOUR CODE
    config.database = {
        "id": "FamilyDB"
    };

    config.collection = {
        "id": "FamilyColl"
    };

    config.documents = {
        "Andersen": {
            "id": "Anderson.1",
            "lastName": "Andersen",
            "parents": [{
                "firstName": "Thomas"
            }, {
                    "firstName": "Mary Kay"
                }],
            "children": [{
                "firstName": "Henriette Thaulow",
                "gender": "female",
                "grade": 5,
                "pets": [{
                    "givenName": "Fluffy"
                }]
            }],
            "address": {
                "state": "WA",
                "county": "King",
                "city": "Seattle"
            }
        },
        "Wakefield": {
            "id": "Wakefield.7",
            "parents": [{
                "familyName": "Wakefield",
                "firstName": "Robin"
            }, {
                    "familyName": "Miller",
                    "firstName": "Ben"
                }],
            "children": [{
                "familyName": "Merriam",
                "firstName": "Jesse",
                "gender": "female",
                "grade": 8,
                "pets": [{
                    "givenName": "Goofy"
                }, {
                        "givenName": "Shadow"
                    }]
            }, {
                    "familyName": "Miller",
                    "firstName": "Lisa",
                    "gender": "female",
                    "grade": 1
                }],
            "address": {
                "state": "NY",
                "county": "Manhattan",
                "city": "NY"
            },
            "isRegistered": false
        }
    };


hello 데이터베이스, 컬렉션 및 문서 정의 역할을 Azure Cosmos DB ```database id```, ```collection id```, 및 문서의 데이터입니다.

마지막으로 내보내기 프로그램 ```config``` hello 내에서 참조할 수 있도록 개체 ```app.js``` 파일입니다.

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART tooYOUR CODE
    module.exports = config;

## <a id="Connect"></a>4 단계: tooan Cosmos DB Azure 계정을 연결 하세요.
에 비어 있지 엽니다 ```app.js``` hello 텍스트 편집기에서 파일입니다. 복사 및 붙여넣기 tooimport hello 아래 hello 코드 ```documentdb``` 모듈과 새로 만든 ```config``` 모듈입니다.

    // ADD THIS PART tooYOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

복사 및 붙여넣기 이전에 저장 하는 hello 코드 toouse hello ```config.endpoint``` 및 ```config.primaryKey``` toocreate 새 DocumentClient 합니다.

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART tooYOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

Hello 코드 tooinitialize hello Azure Cosmos DB 클라이언트를가지고 살펴보겠습니다는 Azure Cosmos DB 리소스를 사용 합니다.

## <a name="step-5-create-a-node-database"></a>5단계: 노드 데이터베이스 만들기
복사한 찾을 수 없습니다, hello 데이터베이스 url 및 hello 컬렉션 url에 대 한 HTTP 상태 tooset hello 아래 hello 코드를 붙여 넣습니다. 이러한 url은 찾으려면 어떻게 해야 hello Azure Cosmos DB 클라이언트는 hello 오른쪽 데이터베이스 및 컬렉션입니다.

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART tooYOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

A [데이터베이스](documentdb-resources.md#databases) hello를 사용 하 여 만들 수 [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) 함수 hello의 **DocumentClient** 클래스입니다. 데이터베이스는 컬렉션에 분할 된 문서 저장소의 hello 논리적 컨테이너입니다.

복사 및 붙여넣기 hello **getDatabase** 함수 hello로 hello app.js 파일에서 새 데이터베이스를 만들기 위한 ```id``` hello에 지정 된 ```config``` 개체입니다. hello 함수는 확인 hello로 hello 데이터베이스 동일 ```FamilyRegistry``` id 이미 존재 하지 않습니다. 파일이 존재하는 경우 새로 만드는 대신 해당 데이터베이스를 반환합니다.

    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

    // ADD THIS PART tooYOUR CODE
    function getDatabase() {
        console.log(`Getting database:\n${config.database.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDatabase(databaseUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDatabase(config.database, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

복사 및 붙여넣기 아래 hello 코드 hello 설정한 **getDatabase** tooadd hello 도우미 함수를 작동 **종료** 하는 hello 종료 메시지와 인쇄 hello 호출 너무**getDatabase** 함수입니다.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function exit(message) {
        console.log(message);
        console.log('Press any key tooexit');
        process.stdin.setRawMode(true);
        process.stdin.resume();
        process.stdin.on('data', process.exit.bind(process, 0));
    }

    getDatabase()
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

터미널을 찾습니다 프로그램 ```app.js``` 파일을 hello 명령을 실행 합니다.```node app.js```

축하합니다. Azure Cosmos DB 데이터베이스를 성공적으로 만들었습니다.

## <a id="CreateColl"></a>6단계: 컬렉션 만들기
> [!WARNING]
> **CreateDocumentCollectionAsync** 는 가격 책정 의미가 포함된 새 컬렉션을 만듭니다. 자세한 내용은 [가격 페이지](https://azure.microsoft.com/pricing/details/cosmos-db/)를 참조하세요.
> 
> 

A [컬렉션](documentdb-resources.md#collections) hello를 사용 하 여 만들 수 [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) 함수 hello의 **DocumentClient** 클래스입니다. 컬렉션은 JSON 문서 및 관련 JavaScript 응용 프로그램 논리의 컨테이너입니다.

복사 및 붙여넣기 hello **getCollection** 함수 hello 아래 **getDatabase** hello app.js 파일 toocreate 함수 hello 사용 하 여 새 사용자 컬렉션 ```id``` hello에지정된```config```개체입니다. Toomake 확인 다시 사용 하 여 컬렉션 동일 hello 있는지 ```FamilyCollection``` id 이미 존재 하지 않습니다. 파일이 존재하는 경우 새로 만드는 대신 해당 컬렉션을 반환합니다.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getCollection() {
        console.log(`Getting collection:\n${config.collection.id}\n`);

        return new Promise((resolve, reject) => {
            client.readCollection(collectionUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

복사 및 붙여넣기 hello 호출 아래 hello 코드를 너무**getDatabase** tooexecute hello **getCollection** 함수입니다.

    getDatabase()

    // ADD THIS PART tooYOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

터미널을 찾습니다 프로그램 ```app.js``` 파일을 hello 명령을 실행 합니다.```node app.js```

축하합니다. Azure Cosmos DB 컬렉션을 성공적으로 만들었습니다.

## <a id="CreateDoc"></a>7단계: 문서 만들기
A [문서](documentdb-resources.md#documents) hello를 사용 하 여 만들 수 [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) 함수 hello의 **DocumentClient** 클래스입니다. 문서는 사용자 정의(임의) JSON 콘텐츠입니다. 이제 Azure Cosmos DB에 문서를 삽입할 수 있습니다.

복사 및 붙여넣기 hello **getFamilyDocument** 함수 hello 아래 **getCollection** 함수 hello에 저장 된 hello JSON 데이터를 포함 하는 hello 문서를 만들기 위한 ```config``` 개체입니다. 다시 확인 toomake 있는지 동일한 id가 아직 없는 hello로 문서.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Getting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDocument(documentUrl, { partitionKey: document.district }, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDocument(collectionUrl, document, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    };

복사 및 붙여넣기 hello 호출 아래 hello 코드를 너무**getCollection** tooexecute hello **getFamilyDocument** 함수입니다.

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

터미널을 찾습니다 프로그램 ```app.js``` 파일을 hello 명령을 실행 합니다.```node app.js```

축하합니다. Azure Cosmos DB 문서를 성공적으로 만들었습니다.

![Node.js 자습서-hello hello 계정과 hello 데이터베이스, hello 컬렉션 hello 문서 간의 계층 관계를 보여 주는 다이어그램-노드 데이터베이스](./media/documentdb-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <a id="Query"></a>8단계: Azure Cosmos DB 리소스 쿼리
Azure Cosmos DB는 각 컬렉션에 저장된 JSON 문서에 대해 [다양한 쿼리](documentdb-sql-query.md)를 지원합니다. hello 다음 샘플 코드는 쿼리를 보여 줍니다 컬렉션에 hello 문서에 대해 실행할 수 있습니다.

복사 및 붙여넣기 hello **queryCollection** 함수 hello 아래 **getFamilyDocument** hello app.js 파일에는 함수입니다. Azure Cosmos DB는 아래와 같이 SQL과 비슷한 쿼리를 지원합니다. 복잡 한 쿼리 작성에 대 한 자세한 내용은 체크 아웃 hello [Query Playground](https://www.documentdb.com/sql/demo) 및 hello [설명서 쿼리](documentdb-sql-query.md)합니다.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function queryCollection() {
        console.log(`Querying collection through index:\n${config.collection.id}`);

        return new Promise((resolve, reject) => {
            client.queryDocuments(
                collectionUrl,
                'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
            ).toArray((err, results) => {
                if (err) reject(err)
                else {
                    for (var queryResult of results) {
                        let resultString = JSON.stringify(queryResult);
                        console.log(`\tQuery returned ${resultString}`);
                    }
                    console.log();
                    resolve(results);
                }
            });
        });
    };


다음 다이어그램 hello 구문 hello 컬렉션에 대해 호출 되는 hello Azure Cosmos DB SQL 쿼리를 만든 방법 보여 줍니다.

![Node.js 자습서-다이어그램 hello 범위를 표현 하 고 hello 쿼리의 의미-노드 데이터베이스](./media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

hello [FROM](documentdb-sql-query.md#FromClause) Azure Cosmos DB 쿼리 범위 지정 된 tooa 단일 컬렉션에 이미 있으므로 키워드는 hello 쿼리에서 선택 사항입니다. 따라서 "FROM Families f"를 "FROM root r" 또는 선택한 다른 변수 이름으로 교체할 수 있습니다. Cosmos DB azure는 제품군, 루트 또는 hello 변수 이름을 선택한, 기본적으로 참조 hello 현재 컬렉션을 유추 합니다.

복사 및 붙여넣기 hello 호출 아래 hello 코드를 너무**getFamilyDocument** tooexecute hello **queryCollection** 함수입니다.

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART tooYOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

터미널을 찾습니다 프로그램 ```app.js``` 파일을 hello 명령을 실행 합니다.```node app.js```

축하합니다. 쿼리된 Azure Cosmos DB 문서를 성공적으로 만들었습니다.

## <a id="ReplaceDocument"></a>9단계: 문서 바꾸기
Azure Cosmos DB는 JSON 문서 바꾸기를 지원합니다.

복사 및 붙여넣기 hello **replaceFamilyDocument** 함수 hello 아래 **queryCollection** hello app.js 파일에는 함수입니다.

                    }
                    console.log();
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function replaceFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Replacing document:\n${document.id}\n`);
        document.children[0].grade = 6;

        return new Promise((resolve, reject) => {
            client.replaceDocument(documentUrl, document, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

복사 및 붙여넣기 hello 호출 아래 hello 코드를 너무**queryCollection** tooexecute hello **replaceDocument** 함수입니다. 또한 hello 코드 toocall 추가 **queryCollection** 다시 tooverify hello 문서가 성공적으로 변경 합니다.

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

터미널을 찾습니다 프로그램 ```app.js``` 파일을 hello 명령을 실행 합니다.```node app.js```

축하합니다. Azure Cosmos DB 문서를 성공적으로 대체했습니다.

## <a id="DeleteDocument"></a>10단계: 문서 삭제
Azure Cosmos DB는 JSON 문서 삭제를 지원합니다.

복사 및 붙여넣기 hello **deleteFamilyDocument** 함수 hello 아래 **replaceFamilyDocument** 함수입니다.

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function deleteFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Deleting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.deleteDocument(documentUrl, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

복사 및 붙여넣기 hello 호출 toohello 아래 hello 코드를 두 번째로 **queryCollection** tooexecute hello **deleteDocument** 함수입니다.

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

터미널을 찾습니다 프로그램 ```app.js``` 파일을 hello 명령을 실행 합니다.```node app.js```

축하합니다. Azure Cosmos DB 문서를 성공적으로 삭제했습니다.

## <a id="DeleteDatabase"></a>11 단계: hello 노드 데이터베이스를 삭제 합니다.
데이터베이스를 만들었습니다. 삭제 hello hello 데이터베이스와 모든 자식 리소스 (컬렉션, 문서 등)를 제거 합니다.

복사 및 붙여넣기 hello **정리** 함수 hello 아래 **deleteFamilyDocument** tooremove hello 데이터베이스 및 모든 hello 자식 리소스가 작동 합니다.

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function cleanup() {
        console.log(`Cleaning up by deleting database ${config.database.id}`);

        return new Promise((resolve, reject) => {
            client.deleteDatabase(databaseUrl, (err) => {
                if (err) reject(err)
                else resolve(null);
            });
        });
    }

복사 및 붙여넣기 hello 호출 아래 hello 코드를 너무**deleteFamilyDocument** tooexecute hello **정리** 함수입니다.

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART tooYOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <a id="Run"></a>12단계: Node.js 응용 프로그램 모두 함께 실행
맵 함수 호출에 대 한 hello 시퀀스는 다음과 같이 표시 됩니다.

    getDatabase()
    .then(() => getCollection())
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    .then(() => cleanup())
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

터미널을 찾습니다 프로그램 ```app.js``` 파일을 hello 명령을 실행 합니다.```node app.js```

Get 시작된 응용 프로그램의 hello 출력을 표시 되어야 합니다. hello 출력 hello 아래 예제에서는 텍스트를 일치 해야 합니다.

    Getting database:
    FamilyDB

    Getting collection:
    FamilyColl

    Getting document:
    Anderson.1

    Getting document:
    Wakefield.7

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":5,"pets":[{"givenName":"Fluffy"}]}]

    Replacing document:
    Anderson.1

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":6,"pets":[{"givenName":"Fluffy"}]}]

    Deleting document:
    Anderson.1

    Cleaning up by deleting database FamilyDB
    Completed successfully
    Press any key tooexit

축하합니다. 하면 만든 첫 번째 Azure Cosmos DB 콘솔 응용 프로그램을 있고 hello Node.js 자습서를 완료 했습니다!

## <a id="GetSolution"></a>Hello 완료 Node.js 자습서 솔루션 가져오기
이 자습서의 단계를 hello 강조 하거나 toodownload hello 코드 시간 toocomplete 없는에서 가져올 수 있습니다 [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started)합니다.

이 문서에서 모든 hello 예제가 포함 된 toorun hello GetStarted 솔루션 hello 다음이 필요 합니다.

* [Azure Cosmos DB 계정][create-account].
* hello [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) 솔루션 GitHub에서 사용할 수 있습니다.

Hello 설치 **documentdb** npm 통해 모듈입니다. 다음 명령을 사용 하 여 hello:

* ```npm install documentdb --save```

다음으로 hello ```config.js``` 파일을 업데이트 hello config.endpoint 및 config.authKey 값에 설명 된 대로 [3 단계: 응용 프로그램의 구성 설정](#Config)합니다. 

다음 프로그램 터미널을 찾습니다 프로그램 ```app.js``` hello 명령을 실행 하 고 파일: ```node app.js```합니다.

정말 간단하죠? 빌드하고 원하는 대로 진행하세요! 

## <a name="next-steps"></a>다음 단계
* 더 복잡한 Node.js 샘플을 찾으십니까? [Azure Cosmos DB를 사용하여 Node.js 웹 응용 프로그램 빌드](documentdb-nodejs-application.md)를 참조하세요.
* 너무 방법에 대해 알아봅니다[Azure Cosmos DB 계정을 모니터링](monitor-accounts.md)합니다.
* Hello에 우리의 샘플 데이터 집합에 대해 쿼리 실행 [Query Playground](https://www.documentdb.com/sql/demo)합니다.
* Hello hello의 개발 섹션에서에서 hello 프로그래밍 모델에 대 한 자세한 [Azure Cosmos DB 설명서 페이지](https://azure.microsoft.com/documentation/services/documentdb/)합니다.

[create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-nodejs-get-started/node-js-tutorial-keys.png
