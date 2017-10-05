---
title: "Azure Cosmos DB: .NET 및 MongoDB API에서 웹앱 빌드 | Microsoft Docs"
description: "Azure Cosmos DB MongoDB API에 연결 및 쿼리하는 데 사용할 수 있는 .NET 코드 샘플을 제시합니다."
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
ms.openlocfilehash: 2d30bec75d701b1fd55355d1e139350b6d828c9a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-the-azure-portal"></a><span data-ttu-id="1f272-103">Azure Cosmos DB: .NET 및 Azure Portal에서 MongoDB API 웹앱 빌드</span><span class="sxs-lookup"><span data-stu-id="1f272-103">Azure Cosmos DB: Build a MongoDB API web app with .NET and the Azure portal</span></span>

<span data-ttu-id="1f272-104">Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="1f272-105">Azure Cosmos DB의 핵심인 전역 배포 및 수평적 크기 조정 기능의 이점을 활용하여 문서, 키/값 및 그래프 데이터베이스를 빠르게 만들고 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="1f272-106">이 빠른 시작에서는 Azure Portal을 사용하여 Azure Cosmos DB 계정, 문서 데이터베이스 및 컬렉션을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="1f272-107">그런 다음, [MongoDB .NET 드라이버](https://docs.mongodb.com/ecosystem/drivers/csharp/)에서 작성한 작업 목록 웹앱을 빌드 및 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-107">You'll then build and deploy a tasks list web app built on the [MongoDB .NET driver](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="1f272-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1f272-108">Prerequisites</span></span>

<span data-ttu-id="1f272-109">Visual Studio 2017이 아직 설치되지 않은 경우 **체험판** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)을 다운로드하고 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-109">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="1f272-110">Visual Studio를 설정하는 동안 **Azure 개발**을 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-110">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="1f272-111">데이터베이스 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="1f272-111">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="1f272-112">샘플 응용 프로그램 복제</span><span class="sxs-lookup"><span data-stu-id="1f272-112">Clone the sample application</span></span>

<span data-ttu-id="1f272-113">이제 GitHub에서 MongoDB API 앱을 복제하고 연결 문자열을 설정한 다음 실행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-113">Now let's clone a MongoDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="1f272-114">프로그래밍 방식으로 데이터를 사용하여 얼마나 쉽게 작업할 수 있는지 알게 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-114">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="1f272-115">git bash와 같은 git 터미널 창을 열고 `cd`를 수행하여 작업 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-115">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="1f272-116">다음 명령을 실행하여 샘플 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-116">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

3. <span data-ttu-id="1f272-117">그런 다음 Visual Studio에서 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-117">Then open the solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="1f272-118">코드 검토</span><span class="sxs-lookup"><span data-stu-id="1f272-118">Review the code</span></span>

<span data-ttu-id="1f272-119">앱에서 어떤 상황이 발생하고 있는지 빠르게 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-119">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="1f272-120">**DAL** 디렉터리에서 **Dal.cs** 파일을 열어 보면 이들 코드 줄이 Azure Cosmos DB 리소스를 만드는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-120">Open the **Dal.cs** file under the **DAL** directory and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="1f272-121">Mongo 클라이언트를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-121">Initialize the Mongo Client.</span></span>

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

* <span data-ttu-id="1f272-122">데이터베이스 및 컬렉션을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-122">Retrieve the database and the collection.</span></span>

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* <span data-ttu-id="1f272-123">모든 문서를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-123">Retrieve all documents.</span></span>

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="1f272-124">연결 문자열 업데이트</span><span class="sxs-lookup"><span data-stu-id="1f272-124">Update your connection string</span></span>

<span data-ttu-id="1f272-125">이제 Azure Portal로 다시 이동하여 연결 문자열 정보를 가져와서 앱에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-125">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="1f272-126">[Azure Portal](http://portal.azure.com/)의 Azure Cosmos DB 계정에서 왼쪽 탐색 영역의 **연결 문자열**을 클릭한 다음 **읽기-쓰기 키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-126">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Connection String**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="1f272-127">다음 단계에서 화면의 오른쪽에 있는 복사 단추를 사용하여 사용자, 암호 및 호스트를 Dal.cs 파일에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-127">You'll use the copy buttons on the right side of the screen to copy the Username, Password, and Host into the Dal.cs file in the next step.</span></span>

2. <span data-ttu-id="1f272-128">**DAL** 디렉터리에서 **Dal.cs** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-128">Open the **Dal.cs** file in the **DAL** directory.</span></span> 

3. <span data-ttu-id="1f272-129">포털에서 복사 단추를 사용하여 **사용자 이름** 값을 복사하고 **Dal.cs** 파일의 **사용자 이름** 값으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-129">Copy your **username** value from the portal (using the copy button) and make it the value of the **username** in your **Dal.cs** file.</span></span> 

4. <span data-ttu-id="1f272-130">그 다음, 포털에서 사용자의 **호스트** 값을 복사하고 **Dal.cs** 파일의 **호스트** 값으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-130">Then copy your **host** value from the portal and make it the value of the **host** in your **Dal.cs** file.</span></span> 

5. <span data-ttu-id="1f272-131">마지막으로, 포털에서 사용자의 **암호** 값을 복사하고 **Dal.cs** 파일의 **암호** 값으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-131">Finally copy your **password** value from the portal and make it the value of the **password** in your **Dal.cs** file.</span></span> 

<span data-ttu-id="1f272-132">이제 Azure Cosmos DB와 통신하는 데 필요한 모든 정보로 앱이 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-132">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-the-web-app"></a><span data-ttu-id="1f272-133">웹앱 실행</span><span class="sxs-lookup"><span data-stu-id="1f272-133">Run the web app</span></span>

1. <span data-ttu-id="1f272-134">Visual Studio의 **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-134">In Visual Studio, right-click on the project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="1f272-135">NuGet **찾아보기** 상자에 *MongoDB.Driver*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-135">In the NuGet **Browse** box, type *MongoDB.Driver*.</span></span>

3. <span data-ttu-id="1f272-136">결과에서 **MongoDB.Driver** 라이브러리를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-136">From the results, install the **MongoDB.Driver** library.</span></span> <span data-ttu-id="1f272-137">그러면 MongoDB.Driver 패키지 뿐만 아니라 모든 종속성도 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-137">This installs the MongoDB.Driver package as well as all dependencies.</span></span>

4. <span data-ttu-id="1f272-138">CTRL+F5를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-138">Click CTRL + F5 to run the application.</span></span> <span data-ttu-id="1f272-139">앱이 브라우저에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-139">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="1f272-140">브라우저에서 **만들기**를 클릭하고 작업 목록 앱에서 몇 가지 새 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-140">Click **Create** in the browser and create a few new tasks in your task list app.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="1f272-141">Azure Portal에서 SLA 검토</span><span class="sxs-lookup"><span data-stu-id="1f272-141">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="1f272-142">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="1f272-142">Clean up resources</span></span>

<span data-ttu-id="1f272-143">이 앱을 계속 사용하지 않으려면 Azure Portal에서 다음 단계에 따라 이 빠른 시작에서 만든 리소스를 모두 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-143">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="1f272-144">Azure Portal의 왼쪽 메뉴에서 **리소스 그룹**을 클릭한 다음 만든 리소스의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-144">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="1f272-145">리소스 그룹 페이지에서 **삭제**를 클릭하고 텍스트 상자에서 삭제할 리소스의 이름을 입력한 다음 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-145">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f272-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1f272-146">Next steps</span></span>

<span data-ttu-id="1f272-147">이 빠른 시작에서 Azure Cosmos DB 계정을 만들고, MongoDB의 API를 사용하여 웹앱을 실행하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-147">In this quickstart, you've learned how to create an Azure Cosmos DB account and run a web app using the API for MongoDB.</span></span> <span data-ttu-id="1f272-148">이제 사용자의 Cosmos DB 계정에 추가 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f272-148">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="1f272-149">MongoDB API용 Azure Cosmos DB로 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="1f272-149">Import data into Azure Cosmos DB for the MongoDB API</span></span>](mongodb-migrate.md)

