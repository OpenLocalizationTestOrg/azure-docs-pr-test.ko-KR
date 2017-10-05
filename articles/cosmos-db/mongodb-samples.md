---
title: "MongoDB API를 사용하여 Azure Cosmos DB 앱 빌드 | Microsoft Docs"
description: "이 문서는 MongoDB용 Azure Cosmos DB API를 사용하여 온라인 데이터베이스를 만드는 자습서입니다."
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
ms.openlocfilehash: 433d2e585c884a10e7e923a0b27c179a95410d01
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="build-an-azure-cosmos-db-api-for-mongodb-app-using-nodejs"></a><span data-ttu-id="d9880-104">Node.js를 사용하여 Azure Cosmos DB: MongoDB API 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="d9880-104">Build an Azure Cosmos DB: API for MongoDB app using Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d9880-105">.NET</span><span class="sxs-lookup"><span data-stu-id="d9880-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="d9880-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="d9880-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="d9880-107">Java</span><span class="sxs-lookup"><span data-stu-id="d9880-107">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="d9880-108">MongoDB용 Node.js</span><span class="sxs-lookup"><span data-stu-id="d9880-108">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="d9880-109">Node.JS</span><span class="sxs-lookup"><span data-stu-id="d9880-109">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="d9880-110">C++</span><span class="sxs-lookup"><span data-stu-id="d9880-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
>

<span data-ttu-id="d9880-111">이 예제에서는 Node.js를 사용하여 Azure Cosmos DB: MongoDB API 콘솔 앱을 빌드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d9880-111">This example shows you how to build an Azure Cosmos DB: API for MongoDB console app using Node.js.</span></span>

<span data-ttu-id="d9880-112">이 예제를 사용하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9880-112">To use this example, you must:</span></span>

* <span data-ttu-id="d9880-113">Azure Cosmos DB: MongoDB API 계정을 [만듭니다](create-mongodb-dotnet.md#create-account).</span><span class="sxs-lookup"><span data-stu-id="d9880-113">[Create](create-mongodb-dotnet.md#create-account) an Azure Cosmos DB: API for MongoDB account.</span></span>
* <span data-ttu-id="d9880-114">MongoDB [연결 문자열](connect-mongodb-account.md) 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d9880-114">Retrieve your MongoDB [connection string](connect-mongodb-account.md) information.</span></span>

## <a name="create-the-app"></a><span data-ttu-id="d9880-115">앱 만들기</span><span class="sxs-lookup"><span data-stu-id="d9880-115">Create the app</span></span>

1. <span data-ttu-id="d9880-116">*app.js* 파일을 만들고 아래 코드를 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d9880-116">Create a *app.js* file and copy & paste the code below.</span></span>

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
        console.log("Inserted a document into the families collection.");
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

2. <span data-ttu-id="d9880-117">계정 설정에 따라 *app.js* 파일에서 다음 변수를 수정합니다([연결 문자열](connect-mongodb-account.md)을 찾는 방법 자세히 알아보기).</span><span class="sxs-lookup"><span data-stu-id="d9880-117">Modify the following variables in the *app.js* file per your account settings (Learn how to find your [connection string](connect-mongodb-account.md)):</span></span>
   
    ```nodejs
    var url = 'mongodb://<endpoint>:<password>@<endpoint>.documents.azure.com:10255/?ssl=true';
    ```
     
3. <span data-ttu-id="d9880-118">즐겨찾는 터미널을 열고 **npm install mongodb --save**를 설치한 다음 **node app.js**로 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d9880-118">Open your favorite terminal, run **npm install mongodb --save**, then run your app with **node app.js**</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9880-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d9880-119">Next steps</span></span>
* <span data-ttu-id="d9880-120">Azure Cosmos DB: MongoDB API 계정으로 [MongoChef를 사용](mongodb-mongochef.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d9880-120">Learn how to [use MongoChef](mongodb-mongochef.md) with your Azure Cosmos DB: API for MongoDB account.</span></span>
