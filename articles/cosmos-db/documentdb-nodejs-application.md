---
title: "Node.js 웹 응용 프로그램 Azure Cosmos DB aaaBuild | Microsoft Docs"
description: "이 Node.js 자습서 toouse Microsoft Azure Cosmos DB toostore 데이터에 액세스 하는 Node.js Express 웹 응용 프로그램에서 Azure 웹 사이트에서 호스트 하는 방법을 살펴봅니다."
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
ms.openlocfilehash: 31194dccf37eef69d2219b0d8328a88d434f79b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="d6fcf-104"><a name="_Toc395783175"></a>Azure Cosmos DB를 사용하여 Node.js 웹 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="d6fcf-104"><a name="_Toc395783175"></a>Build a Node.js web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d6fcf-105">.NET</span><span class="sxs-lookup"><span data-stu-id="d6fcf-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="d6fcf-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="d6fcf-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="d6fcf-107">Java</span><span class="sxs-lookup"><span data-stu-id="d6fcf-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="d6fcf-108">Python</span><span class="sxs-lookup"><span data-stu-id="d6fcf-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="d6fcf-109">이 Node.js 자습서에서는 Azure Cosmos DB toouse 및 hello DocumentDB API toostore 데이터에 액세스 하는 Node.js Express 응용 프로그램에서 Azure 웹 사이트에서 호스트 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-109">This Node.js tutorial shows you how toouse Azure Cosmos DB and hello DocumentDB API toostore and access data from a Node.js Express application hosted on Azure Websites.</span></span> <span data-ttu-id="d6fcf-110">작업을 만들고 검색하고 완료할 수 있는 간단한 웹 기반 작업 관리 응용 프로그램인 ToDo 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-110">You build a simple web-based task-management application, a ToDo app, that allows creating, retrieving, and completing tasks.</span></span> <span data-ttu-id="d6fcf-111">hello 작업은 Azure Cosmos DB에서 JSON 문서도 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-111">hello tasks are stored as JSON documents in Azure Cosmos DB.</span></span> <span data-ttu-id="d6fcf-112">이 자습서 hello 앱의 hello 생성 및 배포를 안내 하 고 각 코드 조각에서 일어나는 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-112">This tutorial walks you through hello creation and deployment of hello app and explains what's happening in each snippet.</span></span>

![Hello이 Node.js 자습서에서 만든 내 할 일 목록 응용 프로그램의 스크린 샷](./media/documentdb-nodejs-application/cosmos-db-node-js-mytodo.png)

<span data-ttu-id="d6fcf-114">없습니다 시간 toocomplete hello 자습서 하 고 방금 tooget hello 완벽 한 솔루션을 원합니다?</span><span class="sxs-lookup"><span data-stu-id="d6fcf-114">Don't have time toocomplete hello tutorial and just want tooget hello complete solution?</span></span> <span data-ttu-id="d6fcf-115">아무런 문제가 없습니다 hello 전체 샘플 솔루션을 가져올 수 있습니다 [GitHub][GitHub]합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-115">Not a problem, you can get hello complete sample solution from [GitHub][GitHub].</span></span> <span data-ttu-id="d6fcf-116">Hello 읽어 [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) toorun 앱 hello 하는 방법에 대 한 지침은 파일.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-116">Just read hello [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) file for instructions on how toorun hello app.</span></span>

## <span data-ttu-id="d6fcf-117"><a name="_Toc395783176"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="d6fcf-117"><a name="_Toc395783176"></a>Prerequisites</span></span>
> [!TIP]
> <span data-ttu-id="d6fcf-118">이 Node.js 자습서에서는 Node.js 및 Azure 웹 사이트를 이전에 사용해본 경험이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-118">This Node.js tutorial assumes that you have some prior experience using Node.js and Azure Websites.</span></span>
> 
> 

<span data-ttu-id="d6fcf-119">Hello이이 문서의 지침을 수행 하기 전에 hello 다음 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-119">Before following hello instructions in this article, you should ensure that you have hello following:</span></span>

* <span data-ttu-id="d6fcf-120">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-120">An active Azure account.</span></span> <span data-ttu-id="d6fcf-121">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d6fcf-122">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

   <span data-ttu-id="d6fcf-123">또는</span><span class="sxs-lookup"><span data-stu-id="d6fcf-123">OR</span></span>

   <span data-ttu-id="d6fcf-124">Hello의 로컬 설치 [Azure Cosmos DB 에뮬레이터](local-emulator.md) (Windows에만 해당).</span><span class="sxs-lookup"><span data-stu-id="d6fcf-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md) (Windows only).</span></span>
* <span data-ttu-id="d6fcf-125">[Node.js][Node.js] 버전 v0.10.29 이상</span><span class="sxs-lookup"><span data-stu-id="d6fcf-125">[Node.js][Node.js] version v0.10.29 or higher.</span></span>
* <span data-ttu-id="d6fcf-126">[Express 생성기](http://www.expressjs.com/starter/generator.html)(`npm install express-generator -g`를 통해 설치 가능)</span><span class="sxs-lookup"><span data-stu-id="d6fcf-126">[Express generator](http://www.expressjs.com/starter/generator.html) (you can install this via `npm install express-generator -g`)</span></span>
* <span data-ttu-id="d6fcf-127">[Git][Git].</span><span class="sxs-lookup"><span data-stu-id="d6fcf-127">[Git][Git].</span></span>

## <span data-ttu-id="d6fcf-128"><a name="_Toc395637761"></a>1단계: Azure Cosmos DB 데이터베이스 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="d6fcf-128"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="d6fcf-129">Azure Cosmos DB 계정을 만들어 시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-129">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="d6fcf-130">계정이 이미 없거나 사용 중인 경우이 자습서에 대 한 Azure Cosmos DB 에뮬레이터 hello 건너뛰어도 너무[2 단계: 새 Node.js 응용 프로그램 만들기](#_Toc395783178)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-130">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create a new Node.js application](#_Toc395783178).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [cosmos-db-keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="d6fcf-131"><a name="_Toc395783178"></a>2단계: 새 Node.js 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="d6fcf-131"><a name="_Toc395783178"></a>Step 2: Create a new Node.js application</span></span>
<span data-ttu-id="d6fcf-132">이제 알아보겠습니다 toocreate hello를 사용 하 여 기본 Hello World Node.js 프로젝트 [Express](http://expressjs.com/) 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-132">Now let's learn toocreate a basic Hello World Node.js project using hello [Express](http://expressjs.com/) framework.</span></span>

1. <span data-ttu-id="d6fcf-133">Hello Node.js 명령 프롬프트와 같은 즐겨 찾는 터미널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-133">Open your favorite terminal, such as hello Node.js command prompt.</span></span>
2. <span data-ttu-id="d6fcf-134">Toohello 디렉터리를 원하는 toostore hello 새 응용 프로그램을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-134">Navigate toohello directory in which you'd like toostore hello new application.</span></span>
3. <span data-ttu-id="d6fcf-135">새 응용 프로그램을 호출 하는 hello express 생성기 toogenerate를 사용 하 여 **todo**합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-135">Use hello express generator toogenerate a new application called **todo**.</span></span>
   
        express todo
4. <span data-ttu-id="d6fcf-136">새 **todo** 디렉터리를 열고 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-136">Open your new **todo** directory and install dependencies.</span></span>
   
        cd todo
        npm install
5. <span data-ttu-id="d6fcf-137">새 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-137">Run your new application.</span></span>
   
        npm start
6. <span data-ttu-id="d6fcf-138">브라우저를 너무 이동 하 여 새 응용 프로그램을 볼 수 있습니다[http://localhost:3000](http://localhost:3000)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-138">You can view your new application by navigating your browser too[http://localhost:3000](http://localhost:3000).</span></span>
   
    ![자세한 Node.js-hello 브라우저 창에서 Hello World 응용 프로그램의 스크린 샷](./media/documentdb-nodejs-application/cosmos-db-node-js-express.png)

    <span data-ttu-id="d6fcf-140">그런 다음 응용 프로그램 hello을 hello 터미널 창에서 CTRL + C를 눌러 다음 클릭 toostop **y** tooterminate hello 일괄 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-140">Then, toostop hello application, press CTRL+C in hello terminal window and then click **y** tooterminate hello batch job.</span></span>

## <span data-ttu-id="d6fcf-141"><a name="_Toc395783179"></a>3단계: 추가 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="d6fcf-141"><a name="_Toc395783179"></a>Step 3: Install additional modules</span></span>
<span data-ttu-id="d6fcf-142">hello **package.json** 파일 hello 프로젝트의 hello 루트에서 생성 하는 hello 파일 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-142">hello **package.json** file is one of hello files created in hello root of hello project.</span></span> <span data-ttu-id="d6fcf-143">이 파일에는 Node.js 응용 프로그램에 필요한 추가 모듈의 목록이 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-143">This file contains a list of additional modules that are required for your Node.js application.</span></span> <span data-ttu-id="d6fcf-144">이상 버전에서는이 응용 프로그램 tooAzure 웹 사이트를 배포할 때이 파일은 응용 프로그램이 Azure toosupport에 설치 되어 있는 모듈 필요 toobe 사용된 toodetermine 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-144">Later, when you deploy this application tooAzure Websites, this file is used toodetermine which modules need toobe installed on Azure toosupport your application.</span></span> <span data-ttu-id="d6fcf-145">여전히 필요 tooinstall 두 개 더 많은 패키지가이 자습서에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-145">We still need tooinstall two more packages for this tutorial.</span></span>

1. <span data-ttu-id="d6fcf-146">Hello 터미널에 다시 설치 hello **비동기** npm 통해 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-146">Back in hello terminal, install hello **async** module via npm.</span></span>
   
        npm install async --save
2. <span data-ttu-id="d6fcf-147">Hello 설치 **documentdb** npm 통해 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-147">Install hello **documentdb** module via npm.</span></span> <span data-ttu-id="d6fcf-148">이 모든 hello Azure Cosmos DB 매직 문제가 발생 하는 hello 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-148">This is hello module where all hello Azure Cosmos DB magic happens.</span></span>
   
        npm install documentdb --save
3. <span data-ttu-id="d6fcf-149">Hello 신속 하 게 확인 **package.json** hello 응용 프로그램의 파일 hello 추가 모듈 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-149">A quick check of hello **package.json** file of hello application should show hello additional modules.</span></span> <span data-ttu-id="d6fcf-150">이 파일은 Azure는 패키지 toodownload 지시 하 고 응용 프로그램을 실행 하는 경우를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-150">This file will tell Azure which packages toodownload and install when running your application.</span></span> <span data-ttu-id="d6fcf-151">아래 hello 예제와 비슷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-151">It should resemble hello example below.</span></span>
   
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
   
    <span data-ttu-id="d6fcf-152">이 파일은 해당 응용 프로그램이 이러한 추가 모듈에 종속된다는 것을 노드(및 나중에 Azure)에 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-152">This tells Node (and Azure later) that your application depends on these additional modules.</span></span>

## <span data-ttu-id="d6fcf-153"><a name="_Toc395783180"></a>4 단계: hello Azure Cosmos DB 서비스를 사용 하 여 노드 응용 프로그램에서</span><span class="sxs-lookup"><span data-stu-id="d6fcf-153"><a name="_Toc395783180"></a>Step 4: Using hello Azure Cosmos DB service in a node application</span></span>
<span data-ttu-id="d6fcf-154">담당 모든 hello 초기 설치 및 구성, 이제 보겠습니다 get toowhy 아래로 드리겠습니다, 있고 Azure Cosmos DB를 사용 하는 코드 일부 toowrite입니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-154">That takes care of all hello initial setup and configuration, now let’s get down toowhy we’re here, and that’s toowrite some code using Azure Cosmos DB.</span></span>

### <a name="create-hello-model"></a><span data-ttu-id="d6fcf-155">Hello 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="d6fcf-155">Create hello model</span></span>
1. <span data-ttu-id="d6fcf-156">Hello 프로젝트 디렉터리에 라는 새 디렉터리를 만듭니다 **모델** hello에 hello package.json 파일과 동일한 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-156">In hello project directory, create a new directory named **models** in hello same directory as hello package.json file.</span></span>
2. <span data-ttu-id="d6fcf-157">Hello에 **모델** 디렉터리 라는 새 파일을 만들어 **taskDao.js**합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-157">In hello **models** directory, create a new file named **taskDao.js**.</span></span> <span data-ttu-id="d6fcf-158">이 파일에는 응용 프로그램에서 만든 hello 작업에 대 한 hello 모델을 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-158">This file will contain hello model for hello tasks created by our application.</span></span>
3. <span data-ttu-id="d6fcf-159">동일한 hello **모델** 디렉터리 라는 또 다른 새 파일을 만들어 **docdbUtils.js**합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-159">In hello same **models** directory, create another new file named **docdbUtils.js**.</span></span> <span data-ttu-id="d6fcf-160">이 파일에는 응용 프로그램 전체에서 사용할 몇 가지 유용하고, 다시 사용할 수 있는 코드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-160">This file will contain some useful, reusable, code that we will use throughout our application.</span></span> 
4. <span data-ttu-id="d6fcf-161">복사 hello 다음 코드에서는 너무**docdbUtils.js**</span><span class="sxs-lookup"><span data-stu-id="d6fcf-161">Copy hello following code in too**docdbUtils.js**</span></span>
   
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
   
5. <span data-ttu-id="d6fcf-162">저장 후 닫기 hello **docdbUtils.js** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-162">Save and close hello **docdbUtils.js** file.</span></span>
6. <span data-ttu-id="d6fcf-163">Hello hello 시작 시 **taskDao.js** 파일, 코드 tooreference hello 다음 hello 추가 **DocumentDBClient** 및 hello **docdbUtils.js** 위에서 만든:</span><span class="sxs-lookup"><span data-stu-id="d6fcf-163">At hello beginning of hello **taskDao.js** file, add hello following code tooreference hello **DocumentDBClient** and hello **docdbUtils.js** we created above:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var docdbUtils = require('./docdbUtils');
7. <span data-ttu-id="d6fcf-164">다음으로 코드 toodefine를 추가 하 고 hello (Task) 개체를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-164">Next, you will add code toodefine and export hello Task object.</span></span> <span data-ttu-id="d6fcf-165">이이 작업 개체를 초기화 하 고 데이터베이스 및 문서 컬렉션을 사용 하 여 hello을 설정 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-165">This is responsible for initializing our Task object and setting up hello Database and Document Collection we will use.</span></span>
   
        function TaskDao(documentDBClient, databaseId, collectionId) {
          this.client = documentDBClient;
          this.databaseId = databaseId;
          this.collectionId = collectionId;
   
          this.database = null;
          this.collection = null;
        }
   
        module.exports = TaskDao;
8. <span data-ttu-id="d6fcf-166">다음으로 추가 나오는 코드 toodefine 추가 방법 hello 작업 개체에 hello Azure Cosmos DB에 저장 된 데이터와의 상호 작용을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-166">Next, add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in Azure Cosmos DB.</span></span>
   
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
9. <span data-ttu-id="d6fcf-167">저장 후 닫기 hello **taskDao.js** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-167">Save and close hello **taskDao.js** file.</span></span> 

### <a name="create-hello-controller"></a><span data-ttu-id="d6fcf-168">Hello 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="d6fcf-168">Create hello controller</span></span>
1. <span data-ttu-id="d6fcf-169">Hello에 **경로** 프로젝트의 디렉터리 라는 새 파일을 만들어 **tasklist.js**합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-169">In hello **routes** directory of your project, create a new file named **tasklist.js**.</span></span> 
2. <span data-ttu-id="d6fcf-170">추가 코드를 너무 다음 hello**tasklist.js**합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-170">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="d6fcf-171">사용 되는 hello DocumentDBClient 및 비동기 모듈 로드 **tasklist.js**합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-171">This loads hello DocumentDBClient and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="d6fcf-172">Hello 정의 **TaskList \ / s** hello의 인스턴스를 전달 되는 함수 **작업** 앞에서 정의한 개체:</span><span class="sxs-lookup"><span data-stu-id="d6fcf-172">This also defined hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var async = require('async');
   
        function TaskList(taskDao) {
          this.taskDao = taskDao;
        }
   
        module.exports = TaskList;
3. <span data-ttu-id="d6fcf-173">계속 해 서 추가 toohello **tasklist.js** 너무 hello 메서드를 추가 하 여 파일**showTasks, addTask**, 및 **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="d6fcf-173">Continue adding toohello **tasklist.js** file by adding hello methods used too**showTasks, addTask**, and **completeTasks**:</span></span>
   
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
4. <span data-ttu-id="d6fcf-174">저장 후 닫기 hello **tasklist.js** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-174">Save and close hello **tasklist.js** file.</span></span>

### <a name="add-configjs"></a><span data-ttu-id="d6fcf-175">config.js 추가</span><span class="sxs-lookup"><span data-stu-id="d6fcf-175">Add config.js</span></span>
1. <span data-ttu-id="d6fcf-176">프로젝트 디렉터리에서 **config.js**라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-176">In your project directory create a new file named **config.js**.</span></span>
2. <span data-ttu-id="d6fcf-177">Hello 너무 다음 추가**config.js**합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-177">Add hello following too**config.js**.</span></span> <span data-ttu-id="d6fcf-178">이 파일은 응용 프로그램에 필요한 구성 설정 및 값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-178">This defines configuration settings and values needed for our application.</span></span>
   
        var config = {}
   
        config.host = process.env.HOST || "[hello URI value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.authKey = process.env.AUTH_KEY || "[hello PRIMARY KEY value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.databaseId = "ToDoList";
        config.collectionId = "Items";
   
        module.exports = config;
3. <span data-ttu-id="d6fcf-179">Hello에 **config.js** 파일, 호스트 및 AUTH_KEY hello 키 블레이드에서 hello에 Azure Cosmos DB 계정에서 찾은 hello 값을 사용 하 여 hello 값 업데이트 [Microsoft Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-179">In hello **config.js** file, update hello values of HOST and AUTH_KEY using hello values found in hello Keys blade of your Azure Cosmos DB account on hello [Microsoft Azure portal](https://portal.azure.com).</span></span>
4. <span data-ttu-id="d6fcf-180">저장 후 닫기 hello **config.js** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-180">Save and close hello **config.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="d6fcf-181">app.js 수정</span><span class="sxs-lookup"><span data-stu-id="d6fcf-181">Modify app.js</span></span>
1. <span data-ttu-id="d6fcf-182">Hello 프로젝트 디렉터리에서 엽니다 hello **app.js** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-182">In hello project directory, open hello **app.js** file.</span></span> <span data-ttu-id="d6fcf-183">Hello Express 웹 응용 프로그램을 만들 때이 파일은 이전 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-183">This file was created earlier when hello Express web application was created.</span></span>
2. <span data-ttu-id="d6fcf-184">추가 코드 toohello 맨 뒤 hello **app.js**</span><span class="sxs-lookup"><span data-stu-id="d6fcf-184">Add hello following code toohello top of **app.js**</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var config = require('./config');
        var TaskList = require('./routes/tasklist');
        var TaskDao = require('./models/taskDao');
3. <span data-ttu-id="d6fcf-185">이 코드는을 사용 하는 hello config 파일 toobe를 정의 하 고 tooread 값이이 파일을 사용 하 여 곧 일부 변수에 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-185">This code defines hello config file toobe used, and proceeds tooread values out of this file into some variables we will use soon.</span></span>
4. <span data-ttu-id="d6fcf-186">두 줄을 다음 hello 대체 **app.js** 파일:</span><span class="sxs-lookup"><span data-stu-id="d6fcf-186">Replace hello following two lines in **app.js** file:</span></span>
   
        app.use('/', index);
        app.use('/users', users); 
   
      <span data-ttu-id="d6fcf-187">다음 코드 조각 hello로:</span><span class="sxs-lookup"><span data-stu-id="d6fcf-187">with hello following snippet:</span></span>
   
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
5. <span data-ttu-id="d6fcf-188">이 줄의 새 인스턴스를 정의 우리의 **TaskDao** 개체와 새 연결 tooAzure Cosmos DB (hello에서 읽은 hello 값을 사용 하 여 **config.js**) hello (task) 개체를 초기화 하 고 양식 동작을 바인딩할 toomethods 우리의 **TaskList \ / s** 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-188">These lines define a new instance of our **TaskDao** object, with a new connection tooAzure Cosmos DB (using hello values read from hello **config.js**), initialize hello task object and then bind form actions toomethods on our **TaskList** controller.</span></span> 
6. <span data-ttu-id="d6fcf-189">마지막으로 저장 하 고 hello 닫습니다 **app.js** 파일에 대 한 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-189">Finally, save and close hello **app.js** file, we're just about done.</span></span>

## <span data-ttu-id="d6fcf-190"><a name="_Toc395783181"></a>5단계: 사용자 인터페이스 작성</span><span class="sxs-lookup"><span data-stu-id="d6fcf-190"><a name="_Toc395783181"></a>Step 5: Build a user interface</span></span>
<span data-ttu-id="d6fcf-191">이제 사용자 응용 프로그램와 실제로 상호 작용할 수 있도록 주의 기울여야 toobuilding hello 사용자 인터페이스를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-191">Now let’s turn our attention toobuilding hello user interface so a user can actually interact with our application.</span></span> <span data-ttu-id="d6fcf-192">빠른 응용 프로그램을 사용 하 여 만든 hello **Jade** hello 뷰 엔진으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-192">hello Express application we created uses **Jade** as hello view engine.</span></span> <span data-ttu-id="d6fcf-193">Jade 대 한 자세한 내용은 참조 하십시오 너무[http://jade-lang.com/](http://jade-lang.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-193">For more information on Jade please refer too[http://jade-lang.com/](http://jade-lang.com/).</span></span>

1. <span data-ttu-id="d6fcf-194">hello **layout.jade** hello에 대 한 파일 **뷰** 디렉터리는 기본 서식 파일의 다른 사용 **.jade** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-194">hello **layout.jade** file in hello **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="d6fcf-195">이 단계에서 수정 toouse [Twitter 부트스트랩](https://github.com/twbs/bootstrap)는 쉽게 toodesign 좋은 찾고 웹 사이트를 사용 하면 하는 도구 키트입니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-195">In this step you will modify it toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking website.</span></span> 
2. <span data-ttu-id="d6fcf-196">열기 hello **layout.jade** hello에서 파일을 찾을 **뷰** hello 다음을 사용 하 여 폴더 및 바꾸기 hello 콘텐츠:</span><span class="sxs-lookup"><span data-stu-id="d6fcf-196">Open hello **layout.jade** file found in hello **views** folder and replace hello contents with hello following:</span></span>

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

    <span data-ttu-id="d6fcf-197">Hello를 효과적으로 그러면 **Jade** toorender 응용 프로그램에 대 한 일부 HTML 엔진을 사용 하며 만듭니다는 **블록** 호출 **콘텐츠** 우리의 콘텐츠에 대 한 hello 레이아웃을 제공할 수 있습니다 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-197">This effectively tells hello **Jade** engine toorender some HTML for our application and creates a **block** called **content** where we can supply hello layout for our content pages.</span></span>

    <span data-ttu-id="d6fcf-198">이 **layout.jade** 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-198">Save and close this **layout.jade** file.</span></span>

3. <span data-ttu-id="d6fcf-199">이제 hello 열 **index.jade** 파일, hello 보기를이 응용 프로그램에서 사용 되 고 hello 파일의 내용을 hello hello 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-199">Now open hello **index.jade** file, hello view that will be used by our application, and replace hello content of hello file with hello following:</span></span>
   
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
   

<span data-ttu-id="d6fcf-200">이 레이아웃을 확장 하 고 hello에 대 한 콘텐츠를 제공 **콘텐츠** hello에서 살펴본 자리 표시자 **layout.jade** 이전 파일.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-200">This extends layout, and provides content for hello **content** placeholder we saw in hello **layout.jade** file earlier.</span></span>
   
<span data-ttu-id="d6fcf-201">이 레이아웃에서 HTML 폼 두 개를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-201">In this layout we created two HTML forms.</span></span>

<span data-ttu-id="d6fcf-202">데이터 및 너무 게시 하 여 tooupdate 항목 수 있는 단추에 대 한 테이블을 포함 하는 첫 번째 형태 hello**/completetask** controller 메서드.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-202">hello first form contains a table for our data and a button that allows us tooupdate items by posting too**/completetask** method of our controller.</span></span>
    
<span data-ttu-id="d6fcf-203">hello 두 번째 형태는 두 개의 입력된 필드와 너무 게시 하 여 새 항목 toocreate 수 있는 단추가 포함**/addtask** controller 메서드.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-203">hello second form contains two input fields and a button that allows us toocreate a new item by posting too**/addtask** method of our controller.</span></span>

<span data-ttu-id="d6fcf-204">이 응용 프로그램 toowork 취급에 대 한 모든 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-204">This should be all that we need for our application toowork.</span></span>

## <span data-ttu-id="d6fcf-205"><a name="_Toc395783181"></a>6단계: 로컬에서 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="d6fcf-205"><a name="_Toc395783181"></a>Step 6: Run your application locally</span></span>
1. <span data-ttu-id="d6fcf-206">로컬 컴퓨터의 tootest hello 응용 프로그램 실행 `npm start` 에서 응용 프로그램을 터미널 toostart hello 다음 새로 고침 프로그램 [http://localhost:3000](http://localhost:3000) 브라우저 페이지.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-206">tootest hello application on your local machine, run `npm start` in hello terminal toostart your application, then refresh your [http://localhost:3000](http://localhost:3000) browser page.</span></span> <span data-ttu-id="d6fcf-207">hello 페이지 이제 hello 이미지 아래와 같이 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-207">hello page should now look like hello image below:</span></span>
   
    ![Hello 브라우저 창에서 MyTodo 목록 응용 프로그램의 스크린 샷](./media/documentdb-nodejs-application/cosmos-db-node-js-localhost.png)

    > [!TIP]
    > <span data-ttu-id="d6fcf-209">Hello layout.jade 파일 또는 hello index.jade 파일에서 hello 들여쓰기에 대 한 오류를 수신 하는 경우에 hello 두 파일의 처음 두 줄은 왼쪽에 맞추고, 공백 없이 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-209">If you receive an error about hello indent in hello layout.jade file or hello index.jade file, ensure that hello first two lines in both files is left justified, with no spaces.</span></span> <span data-ttu-id="d6fcf-210">Hello 처음 두 줄 앞에 공백이 있으면 해당 구성 요소 제거를 두 파일을 저장한 다음 브라우저 창을 새로 고쳐야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-210">If there are spaces before hello first two lines, remove them, save both files, then refresh your browser window.</span></span> 

2. <span data-ttu-id="d6fcf-211">Hello 항목, 항목 이름 및 범주 필드 tooenter 새 작업을 선택한 다음 클릭 **항목 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-211">Use hello Item, Item Name and Category fields tooenter a new task and then click **Add Item**.</span></span> <span data-ttu-id="d6fcf-212">그러면 이러한 속성을 포함한 문서를 Azure Cosmos DB에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-212">This creates a document in Azure Cosmos DB with those properties.</span></span> 
3. <span data-ttu-id="d6fcf-213">hello 페이지 hello 할 일 목록에서 항목을 새로 만들 toodisplay hello를 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-213">hello page should update toodisplay hello newly created item in hello ToDo list.</span></span>
   
    ![Hello 할 일 목록에 새 항목으로 hello 응용 프로그램의 스크린 샷](./media/documentdb-nodejs-application/cosmos-db-node-js-added-task.png)
4. <span data-ttu-id="d6fcf-215">toocomplete 작업을 단순히 hello 전체 열에 hello 확인란을 확인 하 고 클릭 **작업 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-215">toocomplete a task, simply check hello checkbox in hello Complete column, and then click **Update tasks**.</span></span> <span data-ttu-id="d6fcf-216">이미 만든 hello 문서를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-216">This updates hello document you already created.</span></span>

5. <span data-ttu-id="d6fcf-217">toostop hello 응용 프로그램 hello 터미널 창에서 CTRL + C를 누르고 클릭 **Y** tooterminate hello 일괄 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-217">toostop hello application, press CTRL+C in hello terminal window and then click **Y** tooterminate hello batch job.</span></span>

## <span data-ttu-id="d6fcf-218"><a name="_Toc395783182"></a>7 단계: 응용 프로그램 개발 프로젝트 tooAzure 웹 사이트를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-218"><a name="_Toc395783182"></a>Step 7: Deploy your application development project tooAzure Websites</span></span>
1. <span data-ttu-id="d6fcf-219">아직 Azure 웹 사이트에 대해 git 리포지토리를 사용하도록 설정하지 않은 경우 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-219">If you haven't already, enable a git repository for your Azure Website.</span></span> <span data-ttu-id="d6fcf-220">방법에 지침을 찾을 수 toodo hello에이 [로컬 Git 배포 tooAzure 앱 서비스](../app-service-web/app-service-deploy-local-git.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-220">You can find instructions on how toodo this in hello [Local Git Deployment tooAzure App Service](../app-service-web/app-service-deploy-local-git.md) topic.</span></span>
2. <span data-ttu-id="d6fcf-221">Azure 웹 사이트를 git 원격으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-221">Add your Azure Website as a git remote.</span></span>
   
        git remote add azure https://username@your-azure-website.scm.azurewebsites.net:443/your-azure-website.git
3. <span data-ttu-id="d6fcf-222">Toohello 원격 푸시하여 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-222">Deploy by pushing toohello remote.</span></span>
   
        git push azure master
4. <span data-ttu-id="d6fcf-223">몇 초 후에 git이 웹 응용 프로그램 게시를 완료하고 Azure에서 실행 중인 작업을 볼 수 있는 브라우저가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-223">In a few seconds, git will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>

    <span data-ttu-id="d6fcf-224">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-224">Congratulations!</span></span> <span data-ttu-id="d6fcf-225">방금 첫 번째 Node.js Express 웹 응용 프로그램 Azure Cosmos DB를 사용 하 여 빌드된 서 tooAzure 웹 사이트를 게시 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-225">You have just built your first Node.js Express Web Application using Azure Cosmos DB and published it tooAzure Websites.</span></span>

    <span data-ttu-id="d6fcf-226">Toodownload를 싶거나 toohello 전체 참조를 응용 프로그램을이 자습서에 대 한 참조에서 다운로드할 수 있습니다 [GitHub][GitHub]합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-226">If you want toodownload or refer toohello complete reference application for this tutorial, it can be downloaded from [GitHub][GitHub].</span></span>

## <span data-ttu-id="d6fcf-227"><a name="_Toc395637775"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="d6fcf-227"><a name="_Toc395637775"></a>Next steps</span></span>

* <span data-ttu-id="d6fcf-228">Tooperform 확장 및 성능 Azure Cosmos DB를 사용 하 여 테스트를 선택 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-228">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="d6fcf-229">[Azure Cosmos DB를 사용한 성능 및 규모 테스트](performance-testing.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-229">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="d6fcf-230">너무 방법에 대해 알아봅니다[Azure Cosmos DB 계정을 모니터링](monitor-accounts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-230">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="d6fcf-231">Hello에 우리의 샘플 데이터 집합에 대해 쿼리 실행 [Query Playground](https://www.documentdb.com/sql/demo)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-231">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="d6fcf-232">Hello 탐색 [Azure Cosmos DB 설명서](https://docs.microsoft.com/azure/documentdb/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6fcf-232">Explore hello [Azure Cosmos DB documentation](https://docs.microsoft.com/azure/documentdb/).</span></span>

[Node.js]: http://nodejs.org/
[Git]: http://git-scm.com/
[GitHub]: https://github.com/Azure-Samples/documentdb-node-todo-app

