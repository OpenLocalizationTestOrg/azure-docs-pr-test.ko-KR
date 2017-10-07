---
title: "MongoDB Api toobuild Azure Cosmos DB 앱 aaaUse | Microsoft Docs"
description: "MongoDB에 대 한 hello Azure Cosmos DB Api를 사용 하 여 온라인 데이터베이스를 만드는 자습서입니다."
keywords: "MongoDB 예제"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: fb38bc53-3561-487d-9e03-20f232319a87
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: anhoh
ms.openlocfilehash: 09be4362fe3aac02e0163325f958210be9598383
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-azure-cosmos-db-api-for-mongodb-app-using-nodejs"></a><span data-ttu-id="ee47e-104">Node.js를 사용하여 Azure Cosmos DB: MongoDB API 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="ee47e-104">Build an Azure Cosmos DB: API for MongoDB app using Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ee47e-105">.NET</span><span class="sxs-lookup"><span data-stu-id="ee47e-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="ee47e-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="ee47e-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="ee47e-107">Java</span><span class="sxs-lookup"><span data-stu-id="ee47e-107">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="ee47e-108">MongoDB용 Node.js</span><span class="sxs-lookup"><span data-stu-id="ee47e-108">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="ee47e-109">Node.JS</span><span class="sxs-lookup"><span data-stu-id="ee47e-109">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="ee47e-110">C++</span><span class="sxs-lookup"><span data-stu-id="ee47e-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
>

<span data-ttu-id="ee47e-111">이 예제에서는 Azure Cosmos DB toobuild: Node.js를 사용 하 여 MongoDB 콘솔 응용 프로그램에 대 한 API입니다.</span><span class="sxs-lookup"><span data-stu-id="ee47e-111">This example shows you how toobuild an Azure Cosmos DB: API for MongoDB console app using Node.js.</span></span>

<span data-ttu-id="ee47e-112">toouse이이 예제에서는 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee47e-112">toouse this example, you must:</span></span>

* <span data-ttu-id="ee47e-113">Azure Cosmos DB: MongoDB API 계정을 [만듭니다](create-mongodb-dotnet.md#create-account).</span><span class="sxs-lookup"><span data-stu-id="ee47e-113">[Create](create-mongodb-dotnet.md#create-account) an Azure Cosmos DB: API for MongoDB account.</span></span>
* <span data-ttu-id="ee47e-114">MongoDB [연결 문자열](connect-mongodb-account.md) 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ee47e-114">Retrieve your MongoDB [connection string](connect-mongodb-account.md) information.</span></span>

## <a name="create-hello-app"></a><span data-ttu-id="ee47e-115">Hello 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="ee47e-115">Create hello app</span></span>

1. <span data-ttu-id="ee47e-116">만들기는 *app.js* 파일 및 복사 & 아래 hello 코드를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ee47e-116">Create a *app.js* file and copy & paste hello code below.</span></span>

    ```nodejs
    var MongoClient = require('mongodb').MongoClient;
    var assert = require('assert');
    var ObjectId = require('mongodb').ObjectID;
    var url = 'mongodb://<endpoint>:<password>@<endpoint>.documents.azure.com:10255/?ssl=true';

    var insertDocument = function(db, callback) {
    db.collection('families').insertOne( {
            "id": "AndersenFamily",
            "lastName": "Andersen",
            "parents": [
                { "firstName": "Thomas" },
                { "firstName": "Mary Kay" }
            ],
            "children": [
                { "firstName": "John", "gender": "male", "grade": 7 }
            ],
            "pets": [
                { "givenName": "Fluffy" }
            ],
            "address": { "country": "USA", "state": "WA", "city": "Seattle" }
        }, function(err, result) {
        assert.equal(err, null);
        console.log("Inserted a document into hello families collection.");
        callback();
    });
    };
    
    var findFamilies = function(db, callback) {
    var cursor =db.collection('families').find( );
    cursor.each(function(err, doc) {
        assert.equal(err, null);
        if (doc != null) {
            console.dir(doc);
        } else {
            callback();
        }
    });
    };
    
    var updateFamilies = function(db, callback) {
    db.collection('families').updateOne(
        { "lastName" : "Andersen" },
        {
            $set: { "pets": [
                { "givenName": "Fluffy" },
                { "givenName": "Rocky"}
            ] },
            $currentDate: { "lastModified": true }
        }, function(err, results) {
        console.log(results);
        callback();
    });
    };
    
    var removeFamilies = function(db, callback) {
    db.collection('families').deleteMany(
        { "lastName": "Andersen" },
        function(err, results) {
            console.log(results);
            callback();
        }
    );
    };
    
    MongoClient.connect(url, function(err, db) {
    assert.equal(null, err);
    insertDocument(db, function() {
        findFamilies(db, function() {
        updateFamilies(db, function() {
            removeFamilies(db, function() {
                db.close();
            });
        });
        });
    });
    });
    ```

2. <span data-ttu-id="ee47e-117">Hello에서 변수를 다음 hello 수정 *app.js* 계정 설정에 따라 파일 (학습 방법을 toofind 프로그램 [연결 문자열](connect-mongodb-account.md)):</span><span class="sxs-lookup"><span data-stu-id="ee47e-117">Modify hello following variables in hello *app.js* file per your account settings (Learn how toofind your [connection string](connect-mongodb-account.md)):</span></span>
   
    ```nodejs
    var url = 'mongodb://<endpoint>:<password>@<endpoint>.documents.azure.com:10255/?ssl=true';
    ```
     
3. <span data-ttu-id="ee47e-118">즐겨찾는 터미널을 열고 **npm install mongodb --save**를 설치한 다음 **node app.js**로 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ee47e-118">Open your favorite terminal, run **npm install mongodb --save**, then run your app with **node app.js**</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee47e-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ee47e-119">Next steps</span></span>
* <span data-ttu-id="ee47e-120">너무 방법에 대해 알아봅니다[MongoChef를 사용 하 여](mongodb-mongochef.md) Azure Cosmos DB와 함께: MongoDB 계정에 대 한 API입니다.</span><span class="sxs-lookup"><span data-stu-id="ee47e-120">Learn how too[use MongoChef](mongodb-mongochef.md) with your Azure Cosmos DB: API for MongoDB account.</span></span>
