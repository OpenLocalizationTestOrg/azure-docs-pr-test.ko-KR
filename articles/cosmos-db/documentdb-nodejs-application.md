---
title: "Azure Cosmos DB용 Node.js 웹앱 빌드 | Microsoft Docs"
description: "이 Node.js 자습서에서는 Microsoft Azure Cosmos DB를 사용하여 Azure Websites에 호스트된 Node.js Express 웹 응용 프로그램에서 데이터를 저장하고 액세스하는 방법을 설명합니다."
keywords: "응용 프로그램 개발, 데이터베이스 자습서, node.js 알아보기, node.js 자습서"
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 9da9e63b-e76a-434e-96dd-195ce2699ef3
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: mimig
ms.openlocfilehash: 1a98509a98bcd2a5de593eb006f905766fe72966
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <span data-ttu-id="69cfa-104"><a name="_Toc395783175"></a>Azure Cosmos DB를 사용하여 Node.js 웹 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="69cfa-104"><a name="_Toc395783175"></a>Build a Node.js web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="69cfa-105">.NET</span><span class="sxs-lookup"><span data-stu-id="69cfa-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="69cfa-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="69cfa-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="69cfa-107">Java</span><span class="sxs-lookup"><span data-stu-id="69cfa-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="69cfa-108">Python</span><span class="sxs-lookup"><span data-stu-id="69cfa-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="69cfa-109">이 Node.js 자습서에서는 Azure Cosmos DB 및 DocumentDB API를 사용하여 Azure Websites에 호스팅된 Node.js Express 응용 프로그램의 데이터를 저장하고 액세스하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-109">This Node.js tutorial shows you how to use Azure Cosmos DB and the DocumentDB API to store and access data from a Node.js Express application hosted on Azure Websites.</span></span> <span data-ttu-id="69cfa-110">작업을 만들고 검색하고 완료할 수 있는 간단한 웹 기반 작업 관리 응용 프로그램인 ToDo 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-110">You build a simple web-based task-management application, a ToDo app, that allows creating, retrieving, and completing tasks.</span></span> <span data-ttu-id="69cfa-111">작업은 Azure Cosmos DB에 JSON 문서로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-111">The tasks are stored as JSON documents in Azure Cosmos DB.</span></span> <span data-ttu-id="69cfa-112">이 자습서는 앱을 만들고 배포하는 과정을 안내하고 각 코드 조각에서 발생하는 상황에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-112">This tutorial walks you through the creation and deployment of the app and explains what's happening in each snippet.</span></span>

![이 Node.js 자습서에서 만든 My Todo List 응용 프로그램의 스크린샷](./media/documentdb-nodejs-application/cosmos-db-node-js-mytodo.png)

<span data-ttu-id="69cfa-114">자습서를 완료할 시간이 없고 전체 솔루션을 가져오려는 경우</span><span class="sxs-lookup"><span data-stu-id="69cfa-114">Don't have time to complete the tutorial and just want to get the complete solution?</span></span> <span data-ttu-id="69cfa-115">[GitHub][GitHub]에서 전체 샘플 솔루션을 구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-115">Not a problem, you can get the complete sample solution from [GitHub][GitHub].</span></span> <span data-ttu-id="69cfa-116">앱을 실행하는 방법에 대한 지침은 [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) 파일을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69cfa-116">Just read the [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) file for instructions on how to run the app.</span></span>

## <span data-ttu-id="69cfa-117"><a name="_Toc395783176"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="69cfa-117"><a name="_Toc395783176"></a>Prerequisites</span></span>
> [!TIP]
> <span data-ttu-id="69cfa-118">이 Node.js 자습서에서는 Node.js 및 Azure 웹 사이트를 이전에 사용해본 경험이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-118">This Node.js tutorial assumes that you have some prior experience using Node.js and Azure Websites.</span></span>
> 
> 

<span data-ttu-id="69cfa-119">이 문서의 지침을 따르기 전에 다음이 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-119">Before following the instructions in this article, you should ensure that you have the following:</span></span>

* <span data-ttu-id="69cfa-120">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="69cfa-120">An active Azure account.</span></span> <span data-ttu-id="69cfa-121">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="69cfa-122">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69cfa-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

   <span data-ttu-id="69cfa-123">또는</span><span class="sxs-lookup"><span data-stu-id="69cfa-123">OR</span></span>

   <span data-ttu-id="69cfa-124">[Azure Cosmos DB 에뮬레이터](local-emulator.md)의 로컬 설치(Windows만 해당)</span><span class="sxs-lookup"><span data-stu-id="69cfa-124">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md) (Windows only).</span></span>
* <span data-ttu-id="69cfa-125">[Node.js][Node.js] 버전 v0.10.29 이상</span><span class="sxs-lookup"><span data-stu-id="69cfa-125">[Node.js][Node.js] version v0.10.29 or higher.</span></span>
* <span data-ttu-id="69cfa-126">[Express 생성기](http://www.expressjs.com/starter/generator.html)(`npm install express-generator -g`를 통해 설치 가능)</span><span class="sxs-lookup"><span data-stu-id="69cfa-126">[Express generator](http://www.expressjs.com/starter/generator.html) (you can install this via `npm install express-generator -g`)</span></span>
* <span data-ttu-id="69cfa-127">[Git][Git].</span><span class="sxs-lookup"><span data-stu-id="69cfa-127">[Git][Git].</span></span>

## <span data-ttu-id="69cfa-128"><a name="_Toc395637761"></a>1단계: Azure Cosmos DB 데이터베이스 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="69cfa-128"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="69cfa-129">Azure Cosmos DB 계정을 만들어 시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-129">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="69cfa-130">계정이 있거나 이 자습서에 Azure Cosmos DB 에뮬레이터를 사용하고 있는 경우 [2단계: 새 Node.js 응용 프로그램 만들기](#_Toc395783178)로 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-130">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create a new Node.js application](#_Toc395783178).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [cosmos-db-keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="69cfa-131"><a name="_Toc395783178"></a>2단계: 새 Node.js 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="69cfa-131"><a name="_Toc395783178"></a>Step 2: Create a new Node.js application</span></span>
<span data-ttu-id="69cfa-132">이제 [Express](http://expressjs.com/) 프레임워크를 사용해서 기본적인 Hello World Node.js 프로젝트를 만드는 방법을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-132">Now let's learn to create a basic Hello World Node.js project using the [Express](http://expressjs.com/) framework.</span></span>

1. <span data-ttu-id="69cfa-133">Node.js 명령 프롬프트와 같이 줄겨찾는 터미널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-133">Open your favorite terminal, such as the Node.js command prompt.</span></span>
2. <span data-ttu-id="69cfa-134">새 응용 프로그램을 저장하려는 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-134">Navigate to the directory in which you'd like to store the new application.</span></span>
3. <span data-ttu-id="69cfa-135">Express 생성기를 사용해서 **todo**라는 새로운 응용 프로그램을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-135">Use the express generator to generate a new application called **todo**.</span></span>
   
        express todo
4. <span data-ttu-id="69cfa-136">새 **todo** 디렉터리를 열고 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-136">Open your new **todo** directory and install dependencies.</span></span>
   
        cd todo
        npm install
5. <span data-ttu-id="69cfa-137">새 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-137">Run your new application.</span></span>
   
        npm start
6. <span data-ttu-id="69cfa-138">브라우저에서 [http://localhost:3000](http://localhost:3000)으로 이동하여 새 응용 프로그램을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-138">You can view your new application by navigating your browser to [http://localhost:3000](http://localhost:3000).</span></span>
   
    ![Node.js 알아보기 - 브라우저 창에 표시된 Hello World 응용 프로그램의 스크린샷](./media/documentdb-nodejs-application/cosmos-db-node-js-express.png)

    <span data-ttu-id="69cfa-140">그런 다음 응용 프로그램을 중지하려면 터미널 창에서 Ctrl+C를 누른 다음 **y**를 클릭하여 배치 작업을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-140">Then, to stop the application, press CTRL+C in the terminal window and then click **y** to terminate the batch job.</span></span>

## <span data-ttu-id="69cfa-141"><a name="_Toc395783179"></a>3단계: 추가 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="69cfa-141"><a name="_Toc395783179"></a>Step 3: Install additional modules</span></span>
<span data-ttu-id="69cfa-142">**package.json** 파일은 프로젝트 루트에 생성되는 파일 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-142">The **package.json** file is one of the files created in the root of the project.</span></span> <span data-ttu-id="69cfa-143">이 파일에는 Node.js 응용 프로그램에 필요한 추가 모듈의 목록이 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-143">This file contains a list of additional modules that are required for your Node.js application.</span></span> <span data-ttu-id="69cfa-144">나중에 이 응용 프로그램을 Azure Websites에 배포할 때, 응용 프로그램을 지원하기 위해 Azure에 설치해야 할 모듈을 결정하는 데 이 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-144">Later, when you deploy this application to Azure Websites, this file is used to determine which modules need to be installed on Azure to support your application.</span></span> <span data-ttu-id="69cfa-145">이 자습서를 위해 패키지 두 개를 더 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-145">We still need to install two more packages for this tutorial.</span></span>

1. <span data-ttu-id="69cfa-146">다시 터미널에서 npm을 통해 **async** 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-146">Back in the terminal, install the **async** module via npm.</span></span>
   
        npm install async --save
2. <span data-ttu-id="69cfa-147">npm을 통해 **documentdb** 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-147">Install the **documentdb** module via npm.</span></span> <span data-ttu-id="69cfa-148">이 모듈에서 중요한 모든 Azure Cosmos DB 기능이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-148">This is the module where all the Azure Cosmos DB magic happens.</span></span>
   
        npm install documentdb --save
3. <span data-ttu-id="69cfa-149">응용 프로그램의 **package.json** 파일에 대해 빠른 검사를 수행하면 추가 모듈이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-149">A quick check of the **package.json** file of the application should show the additional modules.</span></span> <span data-ttu-id="69cfa-150">이 파일은 응용 프로그램 실행 시 다운로드 및 설치할 패키지를 Azure에 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-150">This file will tell Azure which packages to download and install when running your application.</span></span> <span data-ttu-id="69cfa-151">아래 예제와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-151">It should resemble the example below.</span></span>
   
        {
          "name": "todo",
          "version": "0.0.0",
          "private": true,
          "scripts": {
            "start": "node ./bin/www"
          },
          "dependencies": {
            "async": "^2.1.4",
            "body-parser": "~1.15.2",
            "cookie-parser": "~1.4.3",
            "debug": "~2.2.0",
            "documentdb": "^1.10.0",
            "express": "~4.14.0",
            "jade": "~1.11.0",
            "morgan": "~1.7.0",
            "serve-favicon": "~2.3.0"
          }
        }
   
    <span data-ttu-id="69cfa-152">이 파일은 해당 응용 프로그램이 이러한 추가 모듈에 종속된다는 것을 노드(및 나중에 Azure)에 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-152">This tells Node (and Azure later) that your application depends on these additional modules.</span></span>

## <span data-ttu-id="69cfa-153"><a name="_Toc395783180"></a>4단계: 노드 응용 프로그램에서 Azure Cosmos DB 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="69cfa-153"><a name="_Toc395783180"></a>Step 4: Using the Azure Cosmos DB service in a node application</span></span>
<span data-ttu-id="69cfa-154">초기 설정 및 구성이 모두 완료되었으므로 이제 Azure Cosmos DB를 사용하여 일부 코드를 작성하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-154">That takes care of all the initial setup and configuration, now let’s get down to why we’re here, and that’s to write some code using Azure Cosmos DB.</span></span>

### <a name="create-the-model"></a><span data-ttu-id="69cfa-155">모델 만들기</span><span class="sxs-lookup"><span data-stu-id="69cfa-155">Create the model</span></span>
1. <span data-ttu-id="69cfa-156">프로젝트 디렉터리에서 package.json 파일과 동일한 디렉터리에 **models**라는 새 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-156">In the project directory, create a new directory named **models** in the same directory as the package.json file.</span></span>
2. <span data-ttu-id="69cfa-157">**models** 디렉터리에서 **taskDao.js**라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-157">In the **models** directory, create a new file named **taskDao.js**.</span></span> <span data-ttu-id="69cfa-158">이 파일에는 응용 프로그램에서 만든 작업 모델이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-158">This file will contain the model for the tasks created by our application.</span></span>
3. <span data-ttu-id="69cfa-159">동일한 **models** 디렉터리에서 **docdbUtils.js**라는 다른 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-159">In the same **models** directory, create another new file named **docdbUtils.js**.</span></span> <span data-ttu-id="69cfa-160">이 파일에는 응용 프로그램 전체에서 사용할 몇 가지 유용하고, 다시 사용할 수 있는 코드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-160">This file will contain some useful, reusable, code that we will use throughout our application.</span></span> 
4. <span data-ttu-id="69cfa-161">다음 코드를 **docdbUtils.js**</span><span class="sxs-lookup"><span data-stu-id="69cfa-161">Copy the following code in to **docdbUtils.js**</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
   
        var DocDBUtils = {
            getOrCreateDatabase: function (client, databaseId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id= @id',
                    parameters: [{
                        name: '@id',
                        value: databaseId
                    }]
                };
   
                client.queryDatabases(querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        if (results.length === 0) {
                            var databaseSpec = {
                                id: databaseId
                            };
   
                            client.createDatabase(databaseSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            },
   
            getOrCreateCollection: function (client, databaseLink, collectionId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id=@id',
                    parameters: [{
                        name: '@id',
                        value: collectionId
                    }]
                };               
   
                client.queryCollections(databaseLink, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {        
                        if (results.length === 0) {
                            var collectionSpec = {
                                id: collectionId
                            };
   
                            client.createCollection(databaseLink, collectionSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            }
        };
   
        module.exports = DocDBUtils;
   
5. <span data-ttu-id="69cfa-162">**docdbUtils.js** 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-162">Save and close the **docdbUtils.js** file.</span></span>
6. <span data-ttu-id="69cfa-163">**taskDao.js** 파일의 시작 부분에서 위에서 만든 **DocumentDBClient** 및 **docdbUtils.js**를 참조하도록 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-163">At the beginning of the **taskDao.js** file, add the following code to reference the **DocumentDBClient** and the **docdbUtils.js** we created above:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var docdbUtils = require('./docdbUtils');
7. <span data-ttu-id="69cfa-164">그런 다음, Task 개체를 정의하고 내보내는 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-164">Next, you will add code to define and export the Task object.</span></span> <span data-ttu-id="69cfa-165">이 코드는 작업 개체를 초기화하고 사용할 데이터베이스 및 문서 컬렉션을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-165">This is responsible for initializing our Task object and setting up the Database and Document Collection we will use.</span></span>
   
        function TaskDao(documentDBClient, databaseId, collectionId) {
          this.client = documentDBClient;
          this.databaseId = databaseId;
          this.collectionId = collectionId;
   
          this.database = null;
          this.collection = null;
        }
   
        module.exports = TaskDao;
8. <span data-ttu-id="69cfa-166">이제 다음 코드를 추가하여 Task 개체에서 추가 메서드를 정의합니다. 이러한 메서드를 통해 Azure Cosmos DB에 저장된 데이터를 조작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-166">Next, add the following code to define additional methods on the Task object, which allow interactions with data stored in Azure Cosmos DB.</span></span>
   
        TaskDao.prototype = {
            init: function (callback) {
                var self = this;
   
                docdbUtils.getOrCreateDatabase(self.client, self.databaseId, function (err, db) {
                    if (err) {
                        callback(err);
                    } else {
                        self.database = db;
                        docdbUtils.getOrCreateCollection(self.client, self.database._self, self.collectionId, function (err, coll) {
                            if (err) {
                                callback(err);
   
                            } else {
                                self.collection = coll;
                            }
                        });
                    }
                });
            },
   
            find: function (querySpec, callback) {
                var self = this;
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results);
                    }
                });
            },
   
            addItem: function (item, callback) {
                var self = this;
   
                item.date = Date.now();
                item.completed = false;
   
                self.client.createDocument(self.collection._self, item, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, doc);
                    }
                });
            },
   
            updateItem: function (itemId, callback) {
                var self = this;
   
                self.getItem(itemId, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        doc.completed = true;
   
                        self.client.replaceDocument(doc._self, doc, function (err, replaced) {
                            if (err) {
                                callback(err);
   
                            } else {
                                callback(null, replaced);
                            }
                        });
                    }
                });
            },
   
            getItem: function (itemId, callback) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id = @id',
                    parameters: [{
                        name: '@id',
                        value: itemId
                    }]
                };
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results[0]);
                    }
                });
            }
        };
9. <span data-ttu-id="69cfa-167">**taskDao.js** 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-167">Save and close the **taskDao.js** file.</span></span> 

### <a name="create-the-controller"></a><span data-ttu-id="69cfa-168">컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="69cfa-168">Create the controller</span></span>
1. <span data-ttu-id="69cfa-169">프로젝트의 **routes** 디렉터리에서 **tasklist.js**라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-169">In the **routes** directory of your project, create a new file named **tasklist.js**.</span></span> 
2. <span data-ttu-id="69cfa-170">아래 코드를 **tasklist.js**에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-170">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="69cfa-171">이 코드는 **tasklist.js**에서 사용되는 DocumentDBClient 및 async 모듈을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-171">This loads the DocumentDBClient and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="69cfa-172">또한 앞에서 정의한 **Task** 개체의 인스턴스가 전달되는 **TaskList** 함수도 정의되었습니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-172">This also defined the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var async = require('async');
   
        function TaskList(taskDao) {
          this.taskDao = taskDao;
        }
   
        module.exports = TaskList;
3. <span data-ttu-id="69cfa-173">**showTasks, addTask** 및 **completeTasks**에 사용된 메서드를 추가하여 **tasklist.js** 파일에 계속 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-173">Continue adding to the **tasklist.js** file by adding the methods used to **showTasks, addTask**, and **completeTasks**:</span></span>
   
        TaskList.prototype = {
            showTasks: function (req, res) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.completed=@completed',
                    parameters: [{
                        name: '@completed',
                        value: false
                    }]
                };
   
                self.taskDao.find(querySpec, function (err, items) {
                    if (err) {
                        throw (err);
                    }
   
                    res.render('index', {
                        title: 'My ToDo List ',
                        tasks: items
                    });
                });
            },
   
            addTask: function (req, res) {
                var self = this;
                var item = req.body;
   
                self.taskDao.addItem(item, function (err) {
                    if (err) {
                        throw (err);
                    }
   
                    res.redirect('/');
                });
            },
   
            completeTask: function (req, res) {
                var self = this;
                var completedTasks = Object.keys(req.body);
   
                async.forEach(completedTasks, function taskIterator(completedTask, callback) {
                    self.taskDao.updateItem(completedTask, function (err) {
                        if (err) {
                            callback(err);
                        } else {
                            callback(null);
                        }
                    });
                }, function goHome(err) {
                    if (err) {
                        throw err;
                    } else {
                        res.redirect('/');
                    }
                });
            }
        };
4. <span data-ttu-id="69cfa-174">**tasklist.js** 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-174">Save and close the **tasklist.js** file.</span></span>

### <a name="add-configjs"></a><span data-ttu-id="69cfa-175">config.js 추가</span><span class="sxs-lookup"><span data-stu-id="69cfa-175">Add config.js</span></span>
1. <span data-ttu-id="69cfa-176">프로젝트 디렉터리에서 **config.js**라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-176">In your project directory create a new file named **config.js**.</span></span>
2. <span data-ttu-id="69cfa-177">다음을 **config.js**에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-177">Add the following to **config.js**.</span></span> <span data-ttu-id="69cfa-178">이 파일은 응용 프로그램에 필요한 구성 설정 및 값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-178">This defines configuration settings and values needed for our application.</span></span>
   
        var config = {}
   
        config.host = process.env.HOST || "[the URI value from the Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.authKey = process.env.AUTH_KEY || "[the PRIMARY KEY value from the Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.databaseId = "ToDoList";
        config.collectionId = "Items";
   
        module.exports = config;
3. <span data-ttu-id="69cfa-179">**config.js** 파일에서 [Microsoft Azure Portal](https://portal.azure.com)에 있는 Azure Cosmos DB 계정의 [키] 블레이드에 있는 값을 사용하여 HOST 및 AUTH_KEY 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-179">In the **config.js** file, update the values of HOST and AUTH_KEY using the values found in the Keys blade of your Azure Cosmos DB account on the [Microsoft Azure portal](https://portal.azure.com).</span></span>
4. <span data-ttu-id="69cfa-180">**config.js** 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-180">Save and close the **config.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="69cfa-181">app.js 수정</span><span class="sxs-lookup"><span data-stu-id="69cfa-181">Modify app.js</span></span>
1. <span data-ttu-id="69cfa-182">프로젝트 디렉터리에서 **app.js** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-182">In the project directory, open the **app.js** file.</span></span> <span data-ttu-id="69cfa-183">이 파일은 이전에 Express 웹 응용 프로그램을 만들 때 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-183">This file was created earlier when the Express web application was created.</span></span>
2. <span data-ttu-id="69cfa-184">다음 코드를 **app.js**</span><span class="sxs-lookup"><span data-stu-id="69cfa-184">Add the following code to the top of **app.js**</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var config = require('./config');
        var TaskList = require('./routes/tasklist');
        var TaskDao = require('./models/taskDao');
3. <span data-ttu-id="69cfa-185">이 코드는 사용할 구성 파일을 정의하고, 이 파일의 값을 곧 사용할 몇 가지 변수로 읽어들입니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-185">This code defines the config file to be used, and proceeds to read values out of this file into some variables we will use soon.</span></span>
4. <span data-ttu-id="69cfa-186">**app.js** 파일에서 다음 두 줄을</span><span class="sxs-lookup"><span data-stu-id="69cfa-186">Replace the following two lines in **app.js** file:</span></span>
   
        app.use('/', index);
        app.use('/users', users); 
   
      <span data-ttu-id="69cfa-187">다음 코드 조각으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-187">with the following snippet:</span></span>
   
        var docDbClient = new DocumentDBClient(config.host, {
            masterKey: config.authKey
        });
        var taskDao = new TaskDao(docDbClient, config.databaseId, config.collectionId);
        var taskList = new TaskList(taskDao);
        taskDao.init();
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
        app.set('view engine', 'jade');
5. <span data-ttu-id="69cfa-188">이러한 줄은 Azure Cosmos DB에 대한 새로운 연결을 사용해서 **TaskDao** 개체의 새 인스턴스를 정의하고(**config.js**에서 읽은 값 사용), 작업 개체를 초기화한 후 폼 작업을 **TaskList** 컨트롤러의 메서드에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-188">These lines define a new instance of our **TaskDao** object, with a new connection to Azure Cosmos DB (using the values read from the **config.js**), initialize the task object and then bind form actions to methods on our **TaskList** controller.</span></span> 
6. <span data-ttu-id="69cfa-189">끝으로, **app.js** 파일을 저장하고 닫으면 작업이 거의 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-189">Finally, save and close the **app.js** file, we're just about done.</span></span>

## <span data-ttu-id="69cfa-190"><a name="_Toc395783181"></a>5단계: 사용자 인터페이스 작성</span><span class="sxs-lookup"><span data-stu-id="69cfa-190"><a name="_Toc395783181"></a>Step 5: Build a user interface</span></span>
<span data-ttu-id="69cfa-191">이제 사용자가 실제로 응용 프로그램을 조작할 수 있도록 사용자 인터페이스를 작성하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-191">Now let’s turn our attention to building the user interface so a user can actually interact with our application.</span></span> <span data-ttu-id="69cfa-192">만든 Express 응용 프로그램은 **Jade** 를 뷰 엔진으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-192">The Express application we created uses **Jade** as the view engine.</span></span> <span data-ttu-id="69cfa-193">Jade에 대한 자세한 내용은 [http://jade-lang.com/](http://jade-lang.com/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69cfa-193">For more information on Jade please refer to [http://jade-lang.com/](http://jade-lang.com/).</span></span>

1. <span data-ttu-id="69cfa-194">**views** 디렉터리의 **layout.jade** 파일은 다른 **.jade** 파일에 대한 전역 템플릿으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-194">The **layout.jade** file in the **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="69cfa-195">이 단계에서는 멋진 모습의 웹 사이트를 쉽게 디자인할 수 있게 해주는 도구 키트인 [Twitter Bootstrap](https://github.com/twbs/bootstrap)을 사용하도록 이 파일을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-195">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking website.</span></span> 
2. <span data-ttu-id="69cfa-196">**views** 폴더에 있는 **layout.jade** 파일을 열고 파일 내용을 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-196">Open the **layout.jade** file found in the **views** folder and replace the contents with the following:</span></span>

    ```
    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body
        nav.navbar.navbar-inverse.navbar-fixed-top
          div.navbar-header
            a.navbar-brand(href='#') My Tasks
        block content
        script(src='//ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js')
        script(src='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js')
    ```

    <span data-ttu-id="69cfa-197">이렇게 하면 응용 프로그램에 대한 일부 HTML을 렌더링하고 콘텐츠 페이지의 레이아웃을 제공할 수 있는 **콘텐츠**라는 **블록**을 만들도록 **Jade** 엔진에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-197">This effectively tells the **Jade** engine to render some HTML for our application and creates a **block** called **content** where we can supply the layout for our content pages.</span></span>

    <span data-ttu-id="69cfa-198">이 **layout.jade** 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-198">Save and close this **layout.jade** file.</span></span>

3. <span data-ttu-id="69cfa-199">이제 응용 프로그램에 사용되는 뷰인 **index.jade** 파일을 열고 파일 내용을 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-199">Now open the **index.jade** file, the view that will be used by our application, and replace the content of the file with the following:</span></span>
   
        extends layout
        block content
           h1 #{title}
           br
        
           form(action="/completetask", method="post")
             table.table.table-striped.table-bordered
               tr
                 td Name
                 td Category
                 td Date
                 td Complete
               if (typeof tasks === "undefined")
                 tr
                   td
               else
                 each task in tasks
                   tr
                     td #{task.name}
                     td #{task.category}
                     - var date  = new Date(task.date);
                     - var day   = date.getDate();
                     - var month = date.getMonth() + 1;
                     - var year  = date.getFullYear();
                     td #{month + "/" + day + "/" + year}
                     td
                       input(type="checkbox", name="#{task.id}", value="#{!task.completed}", checked=task.completed)
             button.btn.btn-primary(type="submit") Update tasks
           hr
           form.well(action="/addtask", method="post")
             .form-group
               label(for="name") Item Name:
               input.form-control(name="name", type="textbox")
             .form-group
               label(for="category") Item Category:
               input.form-control(name="category", type="textbox")
             br
             button.btn(type="submit") Add item
   

<span data-ttu-id="69cfa-200">이렇게 하면 레이아웃이 확장되고 앞에서 **layout.jade** 파일에 있던 **content** 자리 표시자의 콘텐츠가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-200">This extends layout, and provides content for the **content** placeholder we saw in the **layout.jade** file earlier.</span></span>
   
<span data-ttu-id="69cfa-201">이 레이아웃에서 HTML 폼 두 개를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-201">In this layout we created two HTML forms.</span></span>

<span data-ttu-id="69cfa-202">첫 번째 폼에는 데이터에 대한 테이블 및 컨트롤러의 **/completetask** 메서드에 게시하여 항목을 업데이트할 수 있게 해주는 단추 및 데이터 테이블이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-202">The first form contains a table for our data and a button that allows us to update items by posting to **/completetask** method of our controller.</span></span>
    
<span data-ttu-id="69cfa-203">두 번째 폼에는 컨트롤러의 **/addtask** 메서드에 게시하여 새 항목을 만들 수 있게 해주는 단추와 2개의 입력 필드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-203">The second form contains two input fields and a button that allows us to create a new item by posting to **/addtask** method of our controller.</span></span>

<span data-ttu-id="69cfa-204">응용 프로그램이 작동하는 데 필요한 모든 작업이 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-204">This should be all that we need for our application to work.</span></span>

## <span data-ttu-id="69cfa-205"><a name="_Toc395783181"></a>6단계: 로컬에서 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="69cfa-205"><a name="_Toc395783181"></a>Step 6: Run your application locally</span></span>
1. <span data-ttu-id="69cfa-206">로컬 컴퓨터에서 응용 프로그램을 테스트하려면 터미널에서 `npm start`를 실행하여 응용 프로그램을 시작한 다음 [http://localhost:3000](http://localhost:3000) 브라우저 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-206">To test the application on your local machine, run `npm start` in the terminal to start your application, then refresh your [http://localhost:3000](http://localhost:3000) browser page.</span></span> <span data-ttu-id="69cfa-207">이제 페이지가 아래 이미지처럼 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-207">The page should now look like the image below:</span></span>
   
    ![브라우저 창에 표시된 MyTodo List 응용 프로그램의 스크린샷](./media/documentdb-nodejs-application/cosmos-db-node-js-localhost.png)

    > [!TIP]
    > <span data-ttu-id="69cfa-209">layout.jade 파일이나 index.jade 파일에서 들여쓰기에 대한 오류가 발생하면 두 파일의 처음 두 줄을 공백 없이 왼쪽에 맞춥니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-209">If you receive an error about the indent in the layout.jade file or the index.jade file, ensure that the first two lines in both files is left justified, with no spaces.</span></span> <span data-ttu-id="69cfa-210">처음 두 줄 앞에 공백이 있으면 제거하고 두 파일을 모두 저장한 다음 브라우저 창을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-210">If there are spaces before the first two lines, remove them, save both files, then refresh your browser window.</span></span> 

2. <span data-ttu-id="69cfa-211">[항목], [항목 이름] 및 [범주] 필드를 사용하여 새 작업을 입력한 다음 **항목 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-211">Use the Item, Item Name and Category fields to enter a new task and then click **Add Item**.</span></span> <span data-ttu-id="69cfa-212">그러면 이러한 속성을 포함한 문서를 Azure Cosmos DB에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-212">This creates a document in Azure Cosmos DB with those properties.</span></span> 
3. <span data-ttu-id="69cfa-213">페이지가 업데이트되어 새로 만든 항목을 ToDo 목록에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-213">The page should update to display the newly created item in the ToDo list.</span></span>
   
    ![할 일 모음에 새 항목이 포함된 응용 프로그램의 스크린샷](./media/documentdb-nodejs-application/cosmos-db-node-js-added-task.png)
4. <span data-ttu-id="69cfa-215">작업을 완료하려면 완료 열의 확인란을 선택한 후 **작업 업데이트**를 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-215">To complete a task, simply check the checkbox in the Complete column, and then click **Update tasks**.</span></span> <span data-ttu-id="69cfa-216">그러면 이미 만든 문서를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-216">This updates the document you already created.</span></span>

5. <span data-ttu-id="69cfa-217">응용 프로그램을 중지하려면 터미널 창에서 Ctrl+C를 누른 다음 **Y**를 클릭하여 배치 작업을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-217">To stop the application, press CTRL+C in the terminal window and then click **Y** to terminate the batch job.</span></span>

## <span data-ttu-id="69cfa-218"><a name="_Toc395783182"></a>7단계: Azure 웹 사이트에 응용 프로그램 개발 프로젝트 배포</span><span class="sxs-lookup"><span data-stu-id="69cfa-218"><a name="_Toc395783182"></a>Step 7: Deploy your application development project to Azure Websites</span></span>
1. <span data-ttu-id="69cfa-219">아직 Azure 웹 사이트에 대해 git 리포지토리를 사용하도록 설정하지 않은 경우 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-219">If you haven't already, enable a git repository for your Azure Website.</span></span> <span data-ttu-id="69cfa-220">[Azure App Service에 로컬 Git 배포](../app-service-web/app-service-deploy-local-git.md) 항목에서 이 작업을 수행하는 방법에 대한 지침을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-220">You can find instructions on how to do this in the [Local Git Deployment to Azure App Service](../app-service-web/app-service-deploy-local-git.md) topic.</span></span>
2. <span data-ttu-id="69cfa-221">Azure 웹 사이트를 git 원격으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-221">Add your Azure Website as a git remote.</span></span>
   
        git remote add azure https://username@your-azure-website.scm.azurewebsites.net:443/your-azure-website.git
3. <span data-ttu-id="69cfa-222">원격 푸시로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-222">Deploy by pushing to the remote.</span></span>
   
        git push azure master
4. <span data-ttu-id="69cfa-223">몇 초 후에 git이 웹 응용 프로그램 게시를 완료하고 Azure에서 실행 중인 작업을 볼 수 있는 브라우저가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-223">In a few seconds, git will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>

    <span data-ttu-id="69cfa-224">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-224">Congratulations!</span></span> <span data-ttu-id="69cfa-225">지금까지 Azure Cosmos DB를 사용하여 첫 Node.js Express 웹 응용 프로그램을 작성하고 Azure Websites에 게시했습니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-225">You have just built your first Node.js Express Web Application using Azure Cosmos DB and published it to Azure Websites.</span></span>

    <span data-ttu-id="69cfa-226">이 자습서의 참조 응용 프로그램 전체를 다운로드하거나 참조하려면 [GitHub][GitHub]에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-226">If you want to download or refer to the complete reference application for this tutorial, it can be downloaded from [GitHub][GitHub].</span></span>

## <span data-ttu-id="69cfa-227"><a name="_Toc395637775"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="69cfa-227"><a name="_Toc395637775"></a>Next steps</span></span>

* <span data-ttu-id="69cfa-228">Azure Cosmos DB를 사용하여 규모 및 성능 테스트를 수행하고 싶으신가요?</span><span class="sxs-lookup"><span data-stu-id="69cfa-228">Want to perform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="69cfa-229">[Azure Cosmos DB를 사용한 성능 및 규모 테스트](performance-testing.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69cfa-229">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="69cfa-230">[Azure Cosmos DB 계정 모니터링](monitor-accounts.md) 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="69cfa-230">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="69cfa-231">[쿼리 실습](https://www.documentdb.com/sql/demo)의 샘플 데이터 집합에 대해 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-231">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="69cfa-232">[Azure Cosmos DB 설명서](https://docs.microsoft.com/azure/documentdb/)를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="69cfa-232">Explore the [Azure Cosmos DB documentation](https://docs.microsoft.com/azure/documentdb/).</span></span>

[Node.js]: http://nodejs.org/
[Git]: http://git-scm.com/
[GitHub]: https://github.com/Azure-Samples/documentdb-node-todo-app

