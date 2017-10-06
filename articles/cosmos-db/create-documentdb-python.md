---
title: "Azure Cosmos DB: Python 사용 하 여 앱을 빌드하고 DocumentDB API hello | Microsoft Docs"
description: "Tooconnect tooand 쿼리를 사용 하면 Python 코드 샘플은 hello Azure Cosmos DB DocumentDB API를 표시."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 51c11be2-af6d-425f-a86a-39cbfe61da29
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 05/13/2017
ms.author: mimig
ms.openlocfilehash: e66965ab493c6ef693e88a3767a401d39e1bde2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-python-and-hello-azure-portal"></a><span data-ttu-id="7e5a9-103">Azure Cosmos DB: python DocumentDB API 앱을 빌드하고 hello Azure 포털</span><span class="sxs-lookup"><span data-stu-id="7e5a9-103">Azure Cosmos DB: Build a DocumentDB API app with Python and hello Azure portal</span></span>

<span data-ttu-id="7e5a9-104">Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="7e5a9-105">신속 하 게 만들기 및 문서, 키/값 및 hello 글로벌 배포 및 수평 확장이 기능 Cosmos DB Azure의 hello 핵심에에서 활용 중 일부는 그래프 데이터베이스를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="7e5a9-106">이 빠른 시작 toocreate Azure Cosmos DB 계정, 문서 데이터베이스 및 컬렉션 사용 하 여 Azure 포털을 hello 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="7e5a9-107">그런 다음 작성 하 고 hello를 기반으로 하 여 콘솔 응용 프로그램을 실행할 [DocumentDB Python API](documentdb-sdk-python.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-107">You then build and run a console app built on hello [DocumentDB Python API](documentdb-sdk-python.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e5a9-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7e5a9-108">Prerequisites</span></span>

* <span data-ttu-id="7e5a9-109">이 예제를 실행 하려면 먼저 다음 필수 구성 요소는 hello가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
    * <span data-ttu-id="7e5a9-110">[Visual Studio 2015](http://www.visualstudio.com/) 이상.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-110">[Visual Studio 2015](http://www.visualstudio.com/) or higher.</span></span>
    * <span data-ttu-id="7e5a9-111">[GitHub](http://microsoft.github.io/PTVS/)에서 Visual Studio용 Python 도구.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-111">Python Tools for Visual Studio from [GitHub](http://microsoft.github.io/PTVS/).</span></span> <span data-ttu-id="7e5a9-112">이 자습서에서는 Python Tools for VS 2015를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-112">This tutorial uses Python Tools for VS 2015.</span></span>
    * <span data-ttu-id="7e5a9-113">[python.org](https://www.python.org/downloads/release/python-2712/)의 Python 2.7</span><span class="sxs-lookup"><span data-stu-id="7e5a9-113">Python 2.7 from [python.org](https://www.python.org/downloads/release/python-2712/)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="7e5a9-114">데이터베이스 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="7e5a9-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="7e5a9-115">컬렉션 추가</span><span class="sxs-lookup"><span data-stu-id="7e5a9-115">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="7e5a9-116">Hello 샘플 응용 프로그램 복제</span><span class="sxs-lookup"><span data-stu-id="7e5a9-116">Clone hello sample application</span></span>

<span data-ttu-id="7e5a9-117">이제 github에서 복제는 DocumentDB API 앱 hello 연결 문자열을 설정 하 고 실행 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-117">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="7e5a9-118">얼마나 쉬운지 데이터로 toowork 프로그래밍 방식으로 하는 것이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-118">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="7e5a9-119">예: git bash git 터미널 윈도우를 열고 및 `cd` tooa 작업 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-119">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="7e5a9-120">다음 명령은 tooclone hello 샘플 리포지토리 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-120">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-python-getting-started.git
    ```  
## <a name="review-hello-code"></a><span data-ttu-id="7e5a9-121">Hello 코드 검토</span><span class="sxs-lookup"><span data-stu-id="7e5a9-121">Review hello code</span></span>

<span data-ttu-id="7e5a9-122">Hello 앱에서 일어나는 빠르게 검토를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-122">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="7e5a9-123">다음 코드이 줄을 만든다고 hello Azure Cosmos DB 리소스 열기 hello DocumentDBGetStarted.py 파일을 찾을 수입니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-123">Open hello DocumentDBGetStarted.py file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 


* <span data-ttu-id="7e5a9-124">hello DocumentClient 초기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-124">hello DocumentClient is initialized.</span></span>

    ```python
    # Initialize hello Python DocumentDB client
    client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
    ```

* <span data-ttu-id="7e5a9-125">새 데이터베이스가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-125">A new database is created.</span></span>

    ```python
    # Create a database
    db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })
    ```

* <span data-ttu-id="7e5a9-126">새 컬렉션이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-126">A new collection is created.</span></span>

    ```python
    # Create collection options
    options = {
        'offerEnableRUPerMinuteThroughput': True,
        'offerVersion': "V2",
        'offerThroughput': 400
    }

    # Create a collection
    collection = client.CreateCollection(db['_self'], { 'id': config['DOCUMENTDB_COLLECTION'] }, options)
    ```

* <span data-ttu-id="7e5a9-127">일부 문서가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-127">Some documents are created.</span></span>

    ```python
    # Create some documents
    document1 = client.CreateDocument(collection['_self'],
        { 
            'id': 'server1',
            'Web Site': 0,
            'Cloud Service': 0,
            'Virtual Machine': 0,
            'name': 'some' 
        })
    ```

* <span data-ttu-id="7e5a9-128">SQL을 사용하여 쿼리가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-128">A query is performed using SQL</span></span>

    ```python
    # Query them in SQL
    query = { 'query': 'SELECT * FROM server s' }    
            
    options = {} 
    options['enableCrossPartitionQuery'] = True
    options['maxItemCount'] = 2

    result_iterable = client.QueryDocuments(collection['_self'], query, options)
    results = list(result_iterable);

    print(results)
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="7e5a9-129">연결 문자열 업데이트</span><span class="sxs-lookup"><span data-stu-id="7e5a9-129">Update your connection string</span></span>

<span data-ttu-id="7e5a9-130">이제 돌아가서 toohello Azure 포털 tooget 연결 문자열 정보를 hello 앱에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-130">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="7e5a9-131">Hello에 [Azure 포털](http://portal.azure.com/), 프로그램 Azure Cosmos DB에에서 account, 왼쪽 탐색 hello 클릭 **키**, 클릭 하 고 **읽기-쓰기 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-131">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="7e5a9-132">Hello에 hello 화면 toocopy hello URI의 오른쪽 hello와 기본 키에서 hello 복사 단추를 사용 한다고 `DocumentDBGetStarted.py` hello 다음 단계에는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-132">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello `DocumentDBGetStarted.py` file in hello next step.</span></span>

    ![표시 및 hello Azure 포털에에서 액세스 키, 키 블레이드에서 복사](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="7e5a9-134">열린 hello `DocumentDBGetStarted.py` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-134">In Open hello `DocumentDBGetStarted.py` file.</span></span> 

3. <span data-ttu-id="7e5a9-135">Hello 포털 (hello 복사 단추 사용)에서 URI 값을 복사 하 고 쉽게에 hello 끝점 키의 값을 hello `DocumentDBGetStarted.py`합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-135">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in `DocumentDBGetStarted.py`.</span></span> 

    `config.ENDPOINT : "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="7e5a9-136">그런 다음 hello 포털에서 기본 키 값을 복사 하 고 쉽게 hello 값 hello `config.MASTERKEY` 에서 `DocumentDBGetStarted.py`합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-136">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello `config.MASTERKEY` in `DocumentDBGetStarted.py`.</span></span> <span data-ttu-id="7e5a9-137">이제 앱을 업데이트 한 toocommunicate Azure Cosmos DB와 함께 필요한 모든 hello 정보 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-137">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `config.MASTERKEY : "FILLME"`
    
## <a name="run-hello-app"></a><span data-ttu-id="7e5a9-138">Hello 앱 실행</span><span class="sxs-lookup"><span data-stu-id="7e5a9-138">Run hello app</span></span>
1. <span data-ttu-id="7e5a9-139">Visual Studio에서 마우스 오른쪽 단추로 클릭 hello 프로젝트에 대해 **솔루션 탐색기**현재 Python 환경 hello를 선택한 다음 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-139">In Visual Studio, right-click on hello project in **Solution Explorer**, select hello current Python environment, then right click.</span></span>

2. <span data-ttu-id="7e5a9-140">Python 패키지 설치를 선택하고 **pydocumentdb**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-140">Select Install Python Package, then type in **pydocumentdb**</span></span>

3. <span data-ttu-id="7e5a9-141">F5 toorun hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-141">Run F5 toorun hello application.</span></span> <span data-ttu-id="7e5a9-142">앱이 브라우저에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-142">Your app displays in your browser.</span></span> 

<span data-ttu-id="7e5a9-143">이제 다시 tooData 탐색기 및 쿼리를 참조, 수정 돌아가서이 새 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-143">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="7e5a9-144">Sla hello Azure 포털에서에서 검토 하 고</span><span class="sxs-lookup"><span data-stu-id="7e5a9-144">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="7e5a9-145">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="7e5a9-145">Clean up resources</span></span>

<span data-ttu-id="7e5a9-146">것 toocontinue toouse이 응용이 프로그램을 만들이 빠른 시작 하 여 hello Azure 포털에서에서 단계를 수행 하는 hello로 리소스를 모두 삭제:</span><span class="sxs-lookup"><span data-stu-id="7e5a9-146">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="7e5a9-147">Hello Azure 포털에서에서 왼쪽 메뉴 hello에서에서 클릭 **리소스 그룹** 만든 hello 리소스의 hello 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-147">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="7e5a9-148">리소스 그룹 페이지에서 클릭 **삭제**hello 텍스트 상자에 hello 리소스 toodelete의 hello 이름을 입력 한 다음 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-148">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e5a9-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7e5a9-149">Next steps</span></span>

<span data-ttu-id="7e5a9-150">이 빠른 시작에서 Azure Cosmos DB 계정 toocreate hello 데이터 탐색기를 사용 하 여 컬렉션을 만들 하 고 응용 프로그램을 실행 하는 방법 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-150">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="7e5a9-151">이제 tooyour Cosmos DB 계정 추가 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a9-151">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="7e5a9-152">DocumentDB API hello에 대 한 Azure Cosmos DB로 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="7e5a9-152">Import data into Azure Cosmos DB for hello DocumentDB API</span></span>](import-data.md)


