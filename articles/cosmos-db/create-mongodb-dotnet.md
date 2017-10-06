---
title: "Azure Cosmos DB:.net 웹 앱을 빌드하고 MongoDB API hello | Microsoft Docs"
description: "Tooconnect tooand 쿼리를 사용 하면.NET 코드 예제는 hello Azure Cosmos DB MongoDB API를 표시."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: c85cc47f772a19aaa7181611b75a8acaedbc4c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-hello-azure-portal"></a><span data-ttu-id="2ea92-103">Azure Cosmos DB:.net MongoDB API 웹 앱을 빌드하고 hello Azure 포털</span><span class="sxs-lookup"><span data-stu-id="2ea92-103">Azure Cosmos DB: Build a MongoDB API web app with .NET and hello Azure portal</span></span>

<span data-ttu-id="2ea92-104">Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="2ea92-105">신속 하 게 만들기 및 문서, 키/값 및 hello 글로벌 배포 및 수평 확장이 기능 Cosmos DB Azure의 hello 핵심에에서 활용 중 일부는 그래프 데이터베이스를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="2ea92-106">이 빠른 시작 toocreate Azure Cosmos DB 계정, 문서 데이터베이스 및 컬렉션 사용 하 여 Azure 포털을 hello 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="2ea92-107">그런 다음 빌드하고 hello에 작성 하는 작업 목록 웹 앱을 배포할 [MongoDB.NET 드라이버](https://docs.mongodb.com/ecosystem/drivers/csharp/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-107">You'll then build and deploy a tasks list web app built on hello [MongoDB .NET driver](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2ea92-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2ea92-108">Prerequisites</span></span>

<span data-ttu-id="2ea92-109">설치 된 Visual Studio 2017 없는 경우 다운로드 하 고 hello를 사용 하 여 수 **무료** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-109">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="2ea92-110">사용할 수 있는지 확인 **Azure 개발** hello Visual Studio 설정 중입니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-110">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="2ea92-111">데이터베이스 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="2ea92-111">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="2ea92-112">Hello 샘플 응용 프로그램 복제</span><span class="sxs-lookup"><span data-stu-id="2ea92-112">Clone hello sample application</span></span>

<span data-ttu-id="2ea92-113">이제 github에서 복제는 MongoDB API 앱 hello 연결 문자열을 설정 하 고 실행 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-113">Now let's clone a MongoDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="2ea92-114">얼마나 쉬운지 데이터로 toowork 프로그래밍 방식으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-114">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="2ea92-115">예: git bash git 터미널 윈도우를 열고 및 `cd` tooa 작업 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-115">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="2ea92-116">다음 명령은 tooclone hello 샘플 리포지토리 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-116">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

3. <span data-ttu-id="2ea92-117">그런 다음 Visual Studio에서 hello 솔루션 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-117">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="2ea92-118">Hello 코드 검토</span><span class="sxs-lookup"><span data-stu-id="2ea92-118">Review hello code</span></span>

<span data-ttu-id="2ea92-119">Hello 앱에서 일어나는 빠르게 검토를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-119">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="2ea92-120">열기 hello **Dal.cs** hello 파일 **DAL** directory를 다음 코드이 줄을 만든다고 hello Azure Cosmos DB 리소스를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-120">Open hello **Dal.cs** file under hello **DAL** directory and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="2ea92-121">Hello Mongo 클라이언트를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-121">Initialize hello Mongo Client.</span></span>

    ```cs
        MongoClientSettings settings = new MongoClientSettings();
        settings.Server = new MongoServerAddress(host, 10255);
        settings.UseSsl = true;
        settings.SslSettings = new SslSettings();
        settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;

        MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
        MongoIdentityEvidence evidence = new PasswordEvidence(password);

        settings.Credentials = new List<MongoCredential>()
        {
            new MongoCredential("SCRAM-SHA-1", identity, evidence)
        };

        MongoClient client = new MongoClient(settings);
    ```

* <span data-ttu-id="2ea92-122">Hello 데이터베이스 및 hello 컬렉션을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-122">Retrieve hello database and hello collection.</span></span>

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* <span data-ttu-id="2ea92-123">모든 문서를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-123">Retrieve all documents.</span></span>

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="2ea92-124">연결 문자열 업데이트</span><span class="sxs-lookup"><span data-stu-id="2ea92-124">Update your connection string</span></span>

<span data-ttu-id="2ea92-125">이제 돌아가서 toohello Azure 포털 tooget 연결 문자열 정보를 hello 앱에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-125">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="2ea92-126">Hello에 [Azure 포털](http://portal.azure.com/), 프로그램 Azure Cosmos DB에에서 account, 왼쪽 탐색 hello 클릭 **연결 문자열**, 클릭 하 고 **읽기-쓰기 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-126">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Connection String**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="2ea92-127">Hello 다음 단계에서 hello Dal.cs 파일로 hello hello 화면 toocopy hello 사용자 이름 오른쪽에 hello 복사 단추, 암호 및 호스트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-127">You'll use hello copy buttons on hello right side of hello screen toocopy hello Username, Password, and Host into hello Dal.cs file in hello next step.</span></span>

2. <span data-ttu-id="2ea92-128">열기 hello **Dal.cs** hello에 대 한 파일 **DAL** 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-128">Open hello **Dal.cs** file in hello **DAL** directory.</span></span> 

3. <span data-ttu-id="2ea92-129">복사 프로그램 **사용자 이름** hello 포털 (hello 복사 단추 사용)에서 값을 하 게 hello 값 hello **사용자 이름** 에 프로그램 **Dal.cs** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-129">Copy your **username** value from hello portal (using hello copy button) and make it hello value of hello **username** in your **Dal.cs** file.</span></span> 

4. <span data-ttu-id="2ea92-130">다음 복사 프로그램 **호스트** hello 포털에서 값을 하 게 hello 값 hello **호스트** 에 프로그램 **Dal.cs** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-130">Then copy your **host** value from hello portal and make it hello value of hello **host** in your **Dal.cs** file.</span></span> 

5. <span data-ttu-id="2ea92-131">마지막 복사 프로그램 **암호** hello 포털에서 값을 하 게 hello 값 hello **암호** 에 프로그램 **Dal.cs** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-131">Finally copy your **password** value from hello portal and make it hello value of hello **password** in your **Dal.cs** file.</span></span> 

<span data-ttu-id="2ea92-132">이제 앱을 업데이트 한 toocommunicate Azure Cosmos DB와 함께 필요한 모든 hello 정보 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-132">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-web-app"></a><span data-ttu-id="2ea92-133">Hello 웹 앱 실행</span><span class="sxs-lookup"><span data-stu-id="2ea92-133">Run hello web app</span></span>

1. <span data-ttu-id="2ea92-134">Visual Studio에서 마우스 오른쪽 단추로 클릭 hello 프로젝트에 대해 **솔루션 탐색기** 클릭 하 고 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-134">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="2ea92-135">Hello NuGet에서에서 **찾아보기** 상자에서 입력 *MongoDB.Driver*합니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-135">In hello NuGet **Browse** box, type *MongoDB.Driver*.</span></span>

3. <span data-ttu-id="2ea92-136">Hello 결과 통해 설치 hello **MongoDB.Driver** 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-136">From hello results, install hello **MongoDB.Driver** library.</span></span> <span data-ttu-id="2ea92-137">Hello MongoDB.Driver 패키지 뿐만 아니라 모든 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-137">This installs hello MongoDB.Driver package as well as all dependencies.</span></span>

4. <span data-ttu-id="2ea92-138">CTRL + f 5를 클릭 toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-138">Click CTRL + F5 toorun hello application.</span></span> <span data-ttu-id="2ea92-139">앱이 브라우저에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-139">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="2ea92-140">클릭 **만들기** 에 브라우저 hello 하 고 작업 목록 앱에서 몇 가지 새 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-140">Click **Create** in hello browser and create a few new tasks in your task list app.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="2ea92-141">Sla hello Azure 포털에서에서 검토 하 고</span><span class="sxs-lookup"><span data-stu-id="2ea92-141">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="2ea92-142">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="2ea92-142">Clean up resources</span></span>

<span data-ttu-id="2ea92-143">것 toocontinue toouse이 응용이 프로그램을 만들이 빠른 시작 하 여 hello Azure 포털에서에서 단계를 수행 하는 hello로 리소스를 모두 삭제:</span><span class="sxs-lookup"><span data-stu-id="2ea92-143">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="2ea92-144">Hello Azure 포털에서에서 왼쪽 메뉴 hello에서에서 클릭 **리소스 그룹** 만든 hello 리소스의 hello 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-144">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="2ea92-145">리소스 그룹 페이지에서 클릭 **삭제**hello 텍스트 상자에 hello 리소스 toodelete의 hello 이름을 입력 한 다음 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-145">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ea92-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2ea92-146">Next steps</span></span>

<span data-ttu-id="2ea92-147">이 퀵 스타트의 어떻게 toocreate Azure Cosmos DB 계정 및 사용 하 여 웹 응용 프로그램 실행 hello API MongoDB에 대 한 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-147">In this quickstart, you've learned how toocreate an Azure Cosmos DB account and run a web app using hello API for MongoDB.</span></span> <span data-ttu-id="2ea92-148">이제 tooyour Cosmos DB 계정 추가 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ea92-148">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="2ea92-149">Hello MongoDB API에 대 한 Azure Cosmos DB로 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="2ea92-149">Import data into Azure Cosmos DB for hello MongoDB API</span></span>](mongodb-migrate.md)

