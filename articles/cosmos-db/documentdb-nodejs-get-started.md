---
title: "Azure Cosmos DB용 DocumentDB API에 대한 Node.js 자습서 | Microsoft Docs"
description: "DocumentDB API를 사용하여 Cosmos DB를 만드는 Node.js 자습서입니다."
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
ms.openlocfilehash: 6510e0270bb2efa252a2b2ad40014c5d26b74a81
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="nodejs-tutorial-use-the-documentdb-api-in-azure-cosmos-db-to-create-a-nodejs-console-application"></a><span data-ttu-id="79bbc-104">Node.js 자습서: Azure Cosmos DB에서 DocumentDB API를 사용하여 Node.js 콘솔 응용 프로그램을 만들기</span><span class="sxs-lookup"><span data-stu-id="79bbc-104">Node.js tutorial: Use the DocumentDB API in Azure Cosmos DB to create a Node.js console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="79bbc-105">.NET</span><span class="sxs-lookup"><span data-stu-id="79bbc-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="79bbc-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="79bbc-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="79bbc-107">MongoDB용 Node.js</span><span class="sxs-lookup"><span data-stu-id="79bbc-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="79bbc-108">Node.JS</span><span class="sxs-lookup"><span data-stu-id="79bbc-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="79bbc-109">Java</span><span class="sxs-lookup"><span data-stu-id="79bbc-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="79bbc-110">C++</span><span class="sxs-lookup"><span data-stu-id="79bbc-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="79bbc-111">Azure Cosmos DB Node.js SDK용 Node.js 자습서를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-111">Welcome to the Node.js tutorial for the Azure Cosmos DB Node.js SDK!</span></span> <span data-ttu-id="79bbc-112">이 자습서를 따라 하면 Azure Cosmos DB 리소스를 만들고 쿼리하는 콘솔 응용 프로그램이 생깁니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="79bbc-113">다음에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-113">We'll cover:</span></span>

* <span data-ttu-id="79bbc-114">Azure Cosmos DB 계정 만들기 및 연결</span><span class="sxs-lookup"><span data-stu-id="79bbc-114">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="79bbc-115">응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="79bbc-115">Setting up your application</span></span>
* <span data-ttu-id="79bbc-116">노드 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="79bbc-116">Creating a node database</span></span>
* <span data-ttu-id="79bbc-117">컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="79bbc-117">Creating a collection</span></span>
* <span data-ttu-id="79bbc-118">JSON 문서 만들기</span><span class="sxs-lookup"><span data-stu-id="79bbc-118">Creating JSON documents</span></span>
* <span data-ttu-id="79bbc-119">컬렉션 쿼리</span><span class="sxs-lookup"><span data-stu-id="79bbc-119">Querying the collection</span></span>
* <span data-ttu-id="79bbc-120">문서 바꾸기</span><span class="sxs-lookup"><span data-stu-id="79bbc-120">Replacing a document</span></span>
* <span data-ttu-id="79bbc-121">문서 삭제</span><span class="sxs-lookup"><span data-stu-id="79bbc-121">Deleting a document</span></span>
* <span data-ttu-id="79bbc-122">노드 데이터베이스 삭제</span><span class="sxs-lookup"><span data-stu-id="79bbc-122">Deleting the node database</span></span>

<span data-ttu-id="79bbc-123">시간이 없으십니까?</span><span class="sxs-lookup"><span data-stu-id="79bbc-123">Don't have time?</span></span> <span data-ttu-id="79bbc-124">염려하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="79bbc-124">Don't worry!</span></span> <span data-ttu-id="79bbc-125">[GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started)에서 전체 솔루션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-125">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span> <span data-ttu-id="79bbc-126">빠른 지침은 [전체 솔루션 다운로드](#GetSolution) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="79bbc-126">See [Get the complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="79bbc-127">Node.js 자습서를 완료한 후에 이 페이지 위쪽 및 아래쪽에 있는 응답 단추를 통해 의견을 보내주세요.</span><span class="sxs-lookup"><span data-stu-id="79bbc-127">After you've completed the Node.js tutorial, please use the voting buttons at the top and bottom of this page to give us feedback.</span></span> <span data-ttu-id="79bbc-128">직접 연락을 받고 싶은 경우 설명에 메일 주소를 포함하세요.</span><span class="sxs-lookup"><span data-stu-id="79bbc-128">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

<span data-ttu-id="79bbc-129">이제 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-129">Now let's get started!</span></span>

## <a name="prerequisites-for-the-nodejs-tutorial"></a><span data-ttu-id="79bbc-130">Node.js 자습서의 필수 조건</span><span class="sxs-lookup"><span data-stu-id="79bbc-130">Prerequisites for the Node.js tutorial</span></span>
<span data-ttu-id="79bbc-131">다음 항목이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-131">Please make sure you have the following:</span></span>

* <span data-ttu-id="79bbc-132">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="79bbc-132">An active Azure account.</span></span> <span data-ttu-id="79bbc-133">아직 구독하지 않은 경우 [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
    * <span data-ttu-id="79bbc-134">또는 이 자습서에 [Azure Cosmos DB 에뮬레이터](local-emulator.md)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-134">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="79bbc-135">[Node.js](https://nodejs.org/) 버전 v0.10.29 이상</span><span class="sxs-lookup"><span data-stu-id="79bbc-135">[Node.js](https://nodejs.org/) version v0.10.29 or higher.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="79bbc-136">1단계: Azure Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="79bbc-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="79bbc-137">Azure Cosmos DB 계정을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="79bbc-138">사용하려는 계정이 이미 있는 경우 [Node.js 응용 프로그램 설치](#SetupNode)로 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-138">If you already have an account you want to use, you can skip ahead to [Set up your Node.js application](#SetupNode).</span></span> <span data-ttu-id="79bbc-139">Azure Cosmos DB 에뮬레이터를 사용하는 경우 [Azure Cosmos DB 에뮬레이터](local-emulator.md)의 단계에 따라 에뮬레이터를 설치하고 [Node.js 응용 프로그램 설치](#SetupNode)로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-139">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Node.js application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="79bbc-140"><a id="SetupNode"></a>2단계: Node.js 응용 프로그램 설치</span><span class="sxs-lookup"><span data-stu-id="79bbc-140"><a id="SetupNode"></a>Step 2: Set up your Node.js application</span></span>
1. <span data-ttu-id="79bbc-141">자주 사용하는 터미널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-141">Open your favorite terminal.</span></span>
2. <span data-ttu-id="79bbc-142">Node.js 응용 프로그램을 저장하려는 폴더 또는 디렉터리를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-142">Locate the folder or directory where you'd like to save your Node.js application.</span></span>
3. <span data-ttu-id="79bbc-143">다음 명령을 사용하여 두 개의 빈 JavaScript 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-143">Create two empty JavaScript files with the following commands:</span></span>
   * <span data-ttu-id="79bbc-144">Windows:</span><span class="sxs-lookup"><span data-stu-id="79bbc-144">Windows:</span></span>
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * <span data-ttu-id="79bbc-145">Linux/OS X:</span><span class="sxs-lookup"><span data-stu-id="79bbc-145">Linux/OS X:</span></span>
     * ```touch app.js```
     * ```touch config.js```
4. <span data-ttu-id="79bbc-146">npm을 통해 documentdb 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-146">Install the documentdb module via npm.</span></span> <span data-ttu-id="79bbc-147">다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-147">Use the following command:</span></span>
   * ```npm install documentdb --save```

<span data-ttu-id="79bbc-148">잘하셨습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-148">Great!</span></span> <span data-ttu-id="79bbc-149">설치를 완료했으므로 코드를 작성해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-149">Now that you've finished setting up, let's start writing some code.</span></span>

## <span data-ttu-id="79bbc-150"><a id="Config"></a>3단계: 앱의 구성 설정</span><span class="sxs-lookup"><span data-stu-id="79bbc-150"><a id="Config"></a>Step 3: Set your app's configurations</span></span>
<span data-ttu-id="79bbc-151">원하는 텍스트 편집기에서 ```config.js```을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-151">Open ```config.js``` in your favorite text editor.</span></span>

<span data-ttu-id="79bbc-152">그런 다음 아래 코드 조각을 복사하고 붙여넣은 다음 속성 ```config.endpoint``` 및 ```config.primaryKey```를 Azure Cosmos DB 끝점 URI 및 기본 키로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-152">Then, copy and paste the code snippet below and set properties ```config.endpoint``` and ```config.primaryKey``` to your Azure Cosmos DB endpoint uri and primary key.</span></span> <span data-ttu-id="79bbc-153">이러한 구성은 모두 [Azure Portal](https://portal.azure.com)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-153">Both these configurations can be found in the [Azure portal](https://portal.azure.com).</span></span>

![Node.js 자습서 - 액티브 허브, Azure Cosmos DB 계정 블레이드의 키 단추 및 키 블레이드의 URI, 기본 키 및 보조 키 값이 강조 표시된 Azure Cosmos DB 계정을 보여 주는 Azure Portal의 스크린샷 - 노드 데이터베이스][keys]

    // ADD THIS PART TO YOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

<span data-ttu-id="79bbc-155">```database id```, ```collection id``` 및 ```JSON documents```을 ```config.endpoint``` 및 ```config.authKey``` 속성을 설정한 아래의 ```config``` 개체로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-155">Copy and paste the ```database id```, ```collection id```, and ```JSON documents``` to your ```config``` object below where you set your ```config.endpoint``` and ```config.authKey``` properties.</span></span> <span data-ttu-id="79bbc-156">데이터베이스에 저장하려는 데이터가 이미 있다면 문서 정의를 추가하는 대신 Azure Cosmos DB의 [데이터 마이그레이션 도구](import-data.md)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-156">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) rather than adding the document definitions.</span></span>

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

    // ADD THIS PART TO YOUR CODE
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


<span data-ttu-id="79bbc-157">데이터베이스, 컬렉션 및 문서 정의는 Azure Cosmos DB ```database id```, ```collection id``` 및 문서 데이터의 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-157">The database, collection, and document definitions will act as your Azure Cosmos DB ```database id```, ```collection id```, and documents' data.</span></span>

<span data-ttu-id="79bbc-158">마지막으로 ```config``` 개체를 내보내므로 ```app.js``` 파일 내에서 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-158">Finally, export your ```config``` object, so that you can reference it within the ```app.js``` file.</span></span>

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART TO YOUR CODE
    module.exports = config;

## <span data-ttu-id="79bbc-159"><a id="Connect"></a>4단계: Azure Cosmos DB 계정에 연결</span><span class="sxs-lookup"><span data-stu-id="79bbc-159"><a id="Connect"></a> Step 4: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="79bbc-160">텍스트 편집기에서 빈 ```app.js``` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-160">Open your empty ```app.js``` file in the text editor.</span></span> <span data-ttu-id="79bbc-161">다음 코드를 복사하고 붙여넣어서 ```documentdb``` 모듈 및 새로 만든 ```config``` 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-161">Copy and paste the code below to import the ```documentdb``` module and your newly created ```config``` module.</span></span>

    // ADD THIS PART TO YOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

<span data-ttu-id="79bbc-162">이전에 저장된 ```config.endpoint``` 및 ```config.primaryKey```를 사용하는 코드를 복사하고 붙여넣어서 새 DocumentClient를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-162">Copy and paste the code to use the previously saved ```config.endpoint``` and ```config.primaryKey``` to create a new DocumentClient.</span></span>

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART TO YOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

<span data-ttu-id="79bbc-163">Azure Cosmos DB 클라이언트를 시작하는 코드가 있다면 Azure Cosmos DB 리소스와 함께 작동하는지 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-163">Now that you have the code to initialize the Azure Cosmos DB client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <a name="step-5-create-a-node-database"></a><span data-ttu-id="79bbc-164">5단계: 노드 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="79bbc-164">Step 5: Create a Node database</span></span>
<span data-ttu-id="79bbc-165">다음 코드를 복사하고 붙여넣어서 찾을 수 없음, 데이터베이스 URL 및 컬렉션 URL에 대한 HTTP 상태를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-165">Copy and paste the code below to set the HTTP status for Not Found, the database url, and the collection url.</span></span> <span data-ttu-id="79bbc-166">이러한 URL을 통해 Azure Cosmos DB 클라이언트가 올바른 데이터베이스 및 컬렉션을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-166">These urls are how the Azure Cosmos DB client will find the right database and collection.</span></span>

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART TO YOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

<span data-ttu-id="79bbc-167">**DocumentClient** 클래스의 [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) 함수를 사용하여 [데이터베이스](documentdb-resources.md#databases)를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-167">A [database](documentdb-resources.md#databases) can be created by using the [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of the **DocumentClient** class.</span></span> <span data-ttu-id="79bbc-168">데이터베이스는 여러 컬렉션으로 분할된 문서 저장소의 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-168">A database is the logical container of document storage partitioned across collections.</span></span>

<span data-ttu-id="79bbc-169">```config``` 개체에 지정된 ```id```를 사용하여 app.js 파일에서 새 데이터베이스를 만들기 위해 **getDatabase** 함수를 복사하고 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-169">Copy and paste the **getDatabase** function for creating your new database in the app.js file with the ```id``` specified in the ```config``` object.</span></span> <span data-ttu-id="79bbc-170">함수는 동일한 ```FamilyRegistry``` ID를 가진 데이터베이스가 이미 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-170">The function will check if the database with the same ```FamilyRegistry``` id does not already exist.</span></span> <span data-ttu-id="79bbc-171">파일이 존재하는 경우 새로 만드는 대신 해당 데이터베이스를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-171">If it does exist, we'll return that database instead of creating a new one.</span></span>

    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="79bbc-172">**getDatabase** 함수를 설정한 아래 코드를 복사하고 붙여넣어서 종료 메시지를 인쇄하고 **getDatabase** 함수를 호출하는 도우미 함수 **종료**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-172">Copy and paste the code below where you set the **getDatabase** function to add the helper function **exit** that will print the exit message and the call to **getDatabase** function.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
    function exit(message) {
        console.log(message);
        console.log('Press any key to exit');
        process.stdin.setRawMode(true);
        process.stdin.resume();
        process.stdin.on('data', process.exit.bind(process, 0));
    }

    getDatabase()
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="79bbc-173">터미널에서 ```app.js``` 파일을 찾고 다음 명령을 실행합니다. ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="79bbc-173">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="79bbc-174">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-174">Congratulations!</span></span> <span data-ttu-id="79bbc-175">Azure Cosmos DB 데이터베이스를 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-175">You have successfully created an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="79bbc-176"><a id="CreateColl"></a>6단계: 컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="79bbc-176"><a id="CreateColl"></a>Step 6: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="79bbc-177">**CreateDocumentCollectionAsync** 는 가격 책정 의미가 포함된 새 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-177">**CreateDocumentCollectionAsync** will create a new collection, which has pricing implications.</span></span> <span data-ttu-id="79bbc-178">자세한 내용은 [가격 페이지](https://azure.microsoft.com/pricing/details/cosmos-db/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="79bbc-178">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="79bbc-179">**DocumentClient** 클래스의 [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) 함수를 사용하여 [컬렉션](documentdb-resources.md#collections)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-179">A [collection](documentdb-resources.md#collections) can be created by using the [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of the **DocumentClient** class.</span></span> <span data-ttu-id="79bbc-180">컬렉션은 JSON 문서 및 관련 JavaScript 응용 프로그램 논리의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-180">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="79bbc-181">**getCollection** 함수를 복사하여 app.js 파일의 **getDatabase** 함수 아래에 붙여넣어 ```config``` 개체에 지정된 ```id```를 포함한 새 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-181">Copy and paste the **getCollection** function underneath the **getDatabase** function in the app.js file to create your new collection with the ```id``` specified in the ```config``` object.</span></span> <span data-ttu-id="79bbc-182">다시 동일한 ```FamilyCollection``` ID를 가진 컬렉션이 이미 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-182">Again, we'll check to make sure a collection with the same ```FamilyCollection``` id does not already exist.</span></span> <span data-ttu-id="79bbc-183">파일이 존재하는 경우 새로 만드는 대신 해당 컬렉션을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-183">If it does exist, we'll return that collection instead of creating a new one.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="79bbc-184">**getDatabase**에 대한 호출 아래에 코드를 복사하고 붙여넣어서 **getCollection** 함수를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-184">Copy and paste the code below the call to **getDatabase** to execute the **getCollection** function.</span></span>

    getDatabase()

    // ADD THIS PART TO YOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="79bbc-185">터미널에서 ```app.js``` 파일을 찾고 다음 명령을 실행합니다. ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="79bbc-185">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="79bbc-186">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-186">Congratulations!</span></span> <span data-ttu-id="79bbc-187">Azure Cosmos DB 컬렉션을 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-187">You have successfully created an Azure Cosmos DB collection.</span></span>

## <span data-ttu-id="79bbc-188"><a id="CreateDoc"></a>7단계: 문서 만들기</span><span class="sxs-lookup"><span data-stu-id="79bbc-188"><a id="CreateDoc"></a>Step 7: Create a document</span></span>
<span data-ttu-id="79bbc-189">**DocumentClient** 클래스의 [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) 함수를 사용하여 [문서](documentdb-resources.md#documents)를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-189">A [document](documentdb-resources.md#documents) can be created by using the [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of the **DocumentClient** class.</span></span> <span data-ttu-id="79bbc-190">문서는 사용자 정의(임의) JSON 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-190">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="79bbc-191">이제 Azure Cosmos DB에 문서를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-191">You can now insert a document into Azure Cosmos DB.</span></span>

<span data-ttu-id="79bbc-192">```config``` 체에 저장된 JSON 데이터를 포함하는 문서를 만들기 위해 **getCollection** 함수 아래에 있는 **getFamilyDocument** 함수를 복사하고 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-192">Copy and paste the **getFamilyDocument** function underneath the **getCollection** function for creating the documents containing the JSON data saved in the ```config``` object.</span></span> <span data-ttu-id="79bbc-193">다시 동일한 ID를 가진 문서가 이미 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-193">Again, we'll check to make sure a document with the same id does not already exist.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="79bbc-194">**getCollection**에 대한 호출 아래에 코드를 복사하고 붙여넣어서 **getFamilyDocument** 함수를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-194">Copy and paste the code below the call to **getCollection** to execute the **getFamilyDocument** function.</span></span>

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART TO YOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="79bbc-195">터미널에서 ```app.js``` 파일을 찾고 다음 명령을 실행합니다. ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="79bbc-195">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="79bbc-196">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-196">Congratulations!</span></span> <span data-ttu-id="79bbc-197">Azure Cosmos DB 문서를 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-197">You have successfully created an Azure Cosmos DB document.</span></span>

![Node.js 자습서 - 계정, 데이터베이스, 컬렉션 및 문서 간의 계층 관계를 보여 주는 다이어그램 - 노드 데이터베이스](./media/documentdb-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <span data-ttu-id="79bbc-199"><a id="Query"></a>8단계: Azure Cosmos DB 리소스 쿼리</span><span class="sxs-lookup"><span data-stu-id="79bbc-199"><a id="Query"></a>Step 8: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="79bbc-200">Azure Cosmos DB는 각 컬렉션에 저장된 JSON 문서에 대해 [다양한 쿼리](documentdb-sql-query.md)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-200">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="79bbc-201">다음 샘플 코드에서는 컬렉션에는 문서에 대해 실행할 수 있는 쿼리를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-201">The following sample code shows a query that you can run against the documents in your collection.</span></span>

<span data-ttu-id="79bbc-202">**queryCollection** 함수를 복사하여 app.js 파일의 **getFamilyDocument** 함수 아래에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-202">Copy and paste the **queryCollection** function underneath the **getFamilyDocument** function in the app.js file.</span></span> <span data-ttu-id="79bbc-203">Azure Cosmos DB는 아래와 같이 SQL과 비슷한 쿼리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-203">Azure Cosmos DB supports SQL-like queries as shown below.</span></span> <span data-ttu-id="79bbc-204">복잡한 쿼리 작성에 대한 자세한 내용은 [쿼리 실습](https://www.documentdb.com/sql/demo) 및 [쿼리 설명서](documentdb-sql-query.md)를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-204">For more information on building complex queries, check out the [Query Playground](https://www.documentdb.com/sql/demo) and the [query documentation](documentdb-sql-query.md).</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
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


<span data-ttu-id="79bbc-205">다음 다이어그램에서는 만든 컬렉션에 대해 Azure Cosmos DB SQL 쿼리 구문을 호출하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-205">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created.</span></span>

![Node.js 자습서 - 쿼리의 의미와 범위를 보여 주는 다이어그램 - 노드 데이터베이스](./media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

<span data-ttu-id="79bbc-207">Azure Cosmos DB 쿼리는 이미 단일 컬렉션으로 범위가 지정되었기 때문에 [FROM](documentdb-sql-query.md#FromClause) 키워드는 쿼리에서 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-207">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span></span> <span data-ttu-id="79bbc-208">따라서 "FROM Families f"를 "FROM root r" 또는 선택한 다른 변수 이름으로 교체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-208">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="79bbc-209">Azure Cosmos DB는 패밀리, 루트 또는 선택한 변수 이름이 기본적으로 현재 컬렉션을 참조하는 것으로 유추합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-209">Azure Cosmos DB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

<span data-ttu-id="79bbc-210">**getFamilyDocument**에 대한 호출 아래에 코드를 복사하고 붙여넣어서 **queryCollection** 함수를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-210">Copy and paste the code below the call to **getFamilyDocument** to execute the **queryCollection** function.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART TO YOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="79bbc-211">터미널에서 ```app.js``` 파일을 찾고 다음 명령을 실행합니다. ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="79bbc-211">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="79bbc-212">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-212">Congratulations!</span></span> <span data-ttu-id="79bbc-213">쿼리된 Azure Cosmos DB 문서를 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-213">You have successfully queried Azure Cosmos DB documents.</span></span>

## <span data-ttu-id="79bbc-214"><a id="ReplaceDocument"></a>9단계: 문서 바꾸기</span><span class="sxs-lookup"><span data-stu-id="79bbc-214"><a id="ReplaceDocument"></a>Step 9: Replace a document</span></span>
<span data-ttu-id="79bbc-215">Azure Cosmos DB는 JSON 문서 바꾸기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-215">Azure Cosmos DB supports replacing JSON documents.</span></span>

<span data-ttu-id="79bbc-216">**replaceFamilyDocument** 함수를 복사하여 app.js 파일의 **queryCollection** 함수 아래에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-216">Copy and paste the **replaceFamilyDocument** function underneath the **queryCollection** function in the app.js file.</span></span>

                    }
                    console.log();
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="79bbc-217">**queryCollection**에 대한 호출 아래에 코드를 복사하고 붙여넣어서 **replaceDocument** 함수를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-217">Copy and paste the code below the call to **queryCollection** to execute the **replaceDocument** function.</span></span> <span data-ttu-id="79bbc-218">또한 **queryCollection** 을 다시 호출하는 코드를 추가하여 문서가 성공적으로 변경되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-218">Also, add the code to call **queryCollection** again to verify that the document had successfully changed.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART TO YOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="79bbc-219">터미널에서 ```app.js``` 파일을 찾고 다음 명령을 실행합니다. ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="79bbc-219">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="79bbc-220">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-220">Congratulations!</span></span> <span data-ttu-id="79bbc-221">Azure Cosmos DB 문서를 성공적으로 대체했습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-221">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="79bbc-222"><a id="DeleteDocument"></a>10단계: 문서 삭제</span><span class="sxs-lookup"><span data-stu-id="79bbc-222"><a id="DeleteDocument"></a>Step 10: Delete a document</span></span>
<span data-ttu-id="79bbc-223">Azure Cosmos DB는 JSON 문서 삭제를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-223">Azure Cosmos DB supports deleting JSON documents.</span></span>

<span data-ttu-id="79bbc-224">**deleteFamilyDocument** 함수를 복사하여 **replaceFamilyDocument** 함수 아래에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-224">Copy and paste the **deleteFamilyDocument** function underneath the **replaceFamilyDocument** function.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="79bbc-225">두 번째 **queryCollection**에 대한 호출 아래에 코드를 복사하고 붙여넣어서 **deleteDocument** 함수를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-225">Copy and paste the code below the call to the second **queryCollection** to execute the **deleteDocument** function.</span></span>

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART TO YOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="79bbc-226">터미널에서 ```app.js``` 파일을 찾고 다음 명령을 실행합니다. ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="79bbc-226">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="79bbc-227">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-227">Congratulations!</span></span> <span data-ttu-id="79bbc-228">Azure Cosmos DB 문서를 성공적으로 삭제했습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-228">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="79bbc-229"><a id="DeleteDatabase"></a>11단계: 노드 데이터베이스 삭제</span><span class="sxs-lookup"><span data-stu-id="79bbc-229"><a id="DeleteDatabase"></a>Step 11: Delete the Node database</span></span>
<span data-ttu-id="79bbc-230">만든 데이터베이스를 삭제하면 데이터베이스와 모든 자식 리소스(컬렉션, 문서 등)가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-230">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="79bbc-231">**cleanup** 함수를 복사하여 **deleteFamilyDocument** 함수 아래에 붙여넣어 데이터베이스와 모든 자식 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-231">Copy and paste the **cleanup** function underneath the **deleteFamilyDocument** function to remove the database and all the children resources.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART TO YOUR CODE
    function cleanup() {
        console.log(`Cleaning up by deleting database ${config.database.id}`);

        return new Promise((resolve, reject) => {
            client.deleteDatabase(databaseUrl, (err) => {
                if (err) reject(err)
                else resolve(null);
            });
        });
    }

<span data-ttu-id="79bbc-232">**deleteFamilyDocument**에 대한 호출 아래의 코드를 복사하여 붙여넣어 **cleanup** 함수를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-232">Copy and paste the code below the call to **deleteFamilyDocument** to execute the **cleanup** function.</span></span>

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART TO YOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <span data-ttu-id="79bbc-233"><a id="Run"></a>12단계: Node.js 응용 프로그램 모두 함께 실행</span><span class="sxs-lookup"><span data-stu-id="79bbc-233"><a id="Run"></a>Step 12: Run your Node.js application all together!</span></span>
<span data-ttu-id="79bbc-234">함수를 호출는 시퀀스는 모두 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-234">Altogether, the sequence for calling your functions should look like this:</span></span>

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

<span data-ttu-id="79bbc-235">터미널에서 ```app.js``` 파일을 찾고 다음 명령을 실행합니다. ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="79bbc-235">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="79bbc-236">시작한 앱의 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-236">You should see the output of your get started app.</span></span> <span data-ttu-id="79bbc-237">출력은 아래의 예제 텍스트와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-237">The output should match the example text below.</span></span>

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
    Press any key to exit

<span data-ttu-id="79bbc-238">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-238">Congratulations!</span></span> <span data-ttu-id="79bbc-239">Node.js 자습서를 만들고 완료했으며 첫 번째 Azure Cosmos DB 콘솔 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-239">You've created you've completed the Node.js tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="79bbc-240"><a id="GetSolution"></a>전체 Node.js 자습서 솔루션 다운로드</span><span class="sxs-lookup"><span data-stu-id="79bbc-240"><a id="GetSolution"></a>Get the complete Node.js tutorial solution</span></span>
<span data-ttu-id="79bbc-241">이 자습서의 단계를 완료할 시간이 없거나 코드를 다운로드하려는 경우 [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started)에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-241">If you didn't have time to complete the steps in this tutorial, or just want to download the code, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span>

<span data-ttu-id="79bbc-242">이 문서의 모든 샘플을 포함하는 GetStarted 솔루션을 실행하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-242">To run the GetStarted solution that contains all the samples in this article, you will need the following:</span></span>

* <span data-ttu-id="79bbc-243">[Azure Cosmos DB 계정][create-account].</span><span class="sxs-lookup"><span data-stu-id="79bbc-243">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="79bbc-244">GitHub에서 제공하는 [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) 솔루션</span><span class="sxs-lookup"><span data-stu-id="79bbc-244">The [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="79bbc-245">npm을 통해 **documentdb** 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-245">Install the **documentdb** module via npm.</span></span> <span data-ttu-id="79bbc-246">다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-246">Use the following command:</span></span>

* ```npm install documentdb --save```

<span data-ttu-id="79bbc-247">다음으로 ```config.js``` 파일에서 [3단계: 앱의 구성 설정](#Config)에 설명한 대로 config.endpoint 및 config.authKey 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-247">Next, in the ```config.js``` file, update the config.endpoint and config.authKey values as described in [Step 3: Set your app's configurations](#Config).</span></span> 

<span data-ttu-id="79bbc-248">그런 다음 터미널에서 ```app.js``` 파일을 찾고 ```node app.js``` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-248">Then in your terminal, locate your ```app.js``` file and run the command: ```node app.js```.</span></span>

<span data-ttu-id="79bbc-249">정말 간단하죠? 빌드하고 원하는 대로 진행하세요!</span><span class="sxs-lookup"><span data-stu-id="79bbc-249">That's it, build it and you're on your way!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="79bbc-250">다음 단계</span><span class="sxs-lookup"><span data-stu-id="79bbc-250">Next steps</span></span>
* <span data-ttu-id="79bbc-251">더 복잡한 Node.js 샘플을 찾으십니까?</span><span class="sxs-lookup"><span data-stu-id="79bbc-251">Want a more complex Node.js sample?</span></span> <span data-ttu-id="79bbc-252">[Azure Cosmos DB를 사용하여 Node.js 웹 응용 프로그램 빌드](documentdb-nodejs-application.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="79bbc-252">See [Build a Node.js web application using Azure Cosmos DB](documentdb-nodejs-application.md).</span></span>
* <span data-ttu-id="79bbc-253">[Azure Cosmos DB 계정 모니터링](monitor-accounts.md) 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="79bbc-253">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="79bbc-254">[쿼리 실습](https://www.documentdb.com/sql/demo)의 샘플 데이터 집합에 대해 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-254">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="79bbc-255">[Azure Cosmos DB 설명서](https://azure.microsoft.com/documentation/services/documentdb/) 페이지의 개발 섹션에서 프로그래밍 모델에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="79bbc-255">Learn more about the programming model in the Develop section of the [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-nodejs-get-started/node-js-tutorial-keys.png
