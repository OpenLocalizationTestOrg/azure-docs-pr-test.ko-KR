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
# <a name="build-an-azure-cosmos-db-api-for-mongodb-app-using-nodejs"></a>Node.js를 사용하여 Azure Cosmos DB: MongoDB API 앱 빌드
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [MongoDB용 Node.js](mongodb-samples.md)
> * [Node.JS](documentdb-nodejs-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
>

이 예제에서는 Azure Cosmos DB toobuild: Node.js를 사용 하 여 MongoDB 콘솔 응용 프로그램에 대 한 API입니다.

toouse이이 예제에서는 수행 해야 합니다.

* Azure Cosmos DB: MongoDB API 계정을 [만듭니다](create-mongodb-dotnet.md#create-account).
* MongoDB [연결 문자열](connect-mongodb-account.md) 정보를 검색합니다.

## <a name="create-hello-app"></a>Hello 앱 만들기

1. 만들기는 *app.js* 파일 및 복사 & 아래 hello 코드를 붙여 넣습니다.

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

2. Hello에서 변수를 다음 hello 수정 *app.js* 계정 설정에 따라 파일 (학습 방법을 toofind 프로그램 [연결 문자열](connect-mongodb-account.md)):
   
    ```nodejs
    var url = 'mongodb://<endpoint>:<password>@<endpoint>.documents.azure.com:10255/?ssl=true';
    ```
     
3. 즐겨찾는 터미널을 열고 **npm install mongodb --save**를 설치한 다음 **node app.js**로 앱을 실행합니다.

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[MongoChef를 사용 하 여](mongodb-mongochef.md) Azure Cosmos DB와 함께: MongoDB 계정에 대 한 API입니다.
