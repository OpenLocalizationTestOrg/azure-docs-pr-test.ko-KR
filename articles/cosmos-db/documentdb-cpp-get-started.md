---
title: "Azure Cosmos DB에 대 한 aaaC + + 자습서 | Microsoft Docs"
description: "C++용 Azure Cosmos DB 인증 SDK를 사용하여 C++ 데이터베이스 및 콘솔 응용 프로그램을 만드는 C++ 자습서입니다. Azure Cosmos DB는 전 세계적인 규모의 데이터베이스 서비스입니다."
services: cosmos-db
documentationcenter: cpp
author: asthana86
manager: jhubbard
editor: 
ms.assetid: b8756b60-8d41-4231-ba4f-6cfcfe3b4bab
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 12/25/2016
ms.author: aasthan
ms.openlocfilehash: 2d5eeff349b7753e39936b7eb77557ad30c5830a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-c-console-application-tutorial-for-hello-documentdb-api"></a><span data-ttu-id="79a82-104">DocumentDB API hello에 대 한 azure Cosmos DB: c + + 콘솔 응용 프로그램 자습서</span><span class="sxs-lookup"><span data-stu-id="79a82-104">Azure Cosmos DB: C++ console application tutorial for hello DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="79a82-105">.NET</span><span class="sxs-lookup"><span data-stu-id="79a82-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="79a82-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="79a82-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="79a82-107">MongoDB용 Node.js</span><span class="sxs-lookup"><span data-stu-id="79a82-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="79a82-108">Node.JS</span><span class="sxs-lookup"><span data-stu-id="79a82-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="79a82-109">Java</span><span class="sxs-lookup"><span data-stu-id="79a82-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="79a82-110">C++</span><span class="sxs-lookup"><span data-stu-id="79a82-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 
 

<span data-ttu-id="79a82-111">C + +에 대 한 SDK를 지지 하는 hello Azure Cosmos DB DocumentDB API에 대 한 c + + 자습서 toohello를 시작!</span><span class="sxs-lookup"><span data-stu-id="79a82-111">Welcome toohello C++ tutorial for hello Azure Cosmos DB DocumentDB API endorsed SDK for C++!</span></span> <span data-ttu-id="79a82-112">이 자습서를 따라 하면 C++ 데이터베이스를 포함하여 Azure Cosmos DB 리소스를 만들고 쿼리하는 콘솔 응용 프로그램이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources, including a C++ database.</span></span>

<span data-ttu-id="79a82-113">다음에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-113">We'll cover:</span></span>

* <span data-ttu-id="79a82-114">만들기 및 tooan Azure Cosmos DB 계정 연결</span><span class="sxs-lookup"><span data-stu-id="79a82-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="79a82-115">응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="79a82-115">Setting up your application</span></span>
* <span data-ttu-id="79a82-116">C++ Azure Cosmos DB 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="79a82-116">Creating a C++ Azure Cosmos DB database</span></span>
* <span data-ttu-id="79a82-117">컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="79a82-117">Creating a collection</span></span>
* <span data-ttu-id="79a82-118">JSON 문서 만들기</span><span class="sxs-lookup"><span data-stu-id="79a82-118">Creating JSON documents</span></span>
* <span data-ttu-id="79a82-119">Hello 컬렉션 쿼리</span><span class="sxs-lookup"><span data-stu-id="79a82-119">Querying hello collection</span></span>
* <span data-ttu-id="79a82-120">문서 바꾸기</span><span class="sxs-lookup"><span data-stu-id="79a82-120">Replacing a document</span></span>
* <span data-ttu-id="79a82-121">문서 삭제</span><span class="sxs-lookup"><span data-stu-id="79a82-121">Deleting a document</span></span>
* <span data-ttu-id="79a82-122">Hello c + + Azure Cosmos DB 데이터베이스 삭제</span><span class="sxs-lookup"><span data-stu-id="79a82-122">Deleting hello C++ Azure Cosmos DB database</span></span>

<span data-ttu-id="79a82-123">시간이 없으십니까?</span><span class="sxs-lookup"><span data-stu-id="79a82-123">Don't have time?</span></span> <span data-ttu-id="79a82-124">염려하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="79a82-124">Don't worry!</span></span> <span data-ttu-id="79a82-125">hello 완벽 한 솔루션에 있는 [GitHub](https://github.com/stalker314314/DocumentDBCpp)합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-125">hello complete solution is available on [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span></span> <span data-ttu-id="79a82-126">참조 [hello 완벽 한 솔루션을 가져올](#GetSolution) 빠른 지침에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-126">See [Get hello complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="79a82-127">Hello c + + 자습서를 완료 한 후 하십시오 사용 하 여 hello 투표 하는 단추 hello 페이지 toogive이 맨 아래에 us 피드백.</span><span class="sxs-lookup"><span data-stu-id="79a82-127">After you've completed hello C++ tutorial, please use hello voting buttons at hello bottom of this page toogive us feedback.</span></span> 

<span data-ttu-id="79a82-128">받을지 경우 toocontact를 직접 생각 될 전자 메일 주소 가능한 tooinclude 메모에 또는 [toous 여기 교류할](https://www.research.net/r/8BKRJ3Z)합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments or [reach out toous here](https://www.research.net/r/8BKRJ3Z).</span></span> 

<span data-ttu-id="79a82-129">이제 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-129">Now let's get started!</span></span>

## <a name="prerequisites-for-hello-c-tutorial"></a><span data-ttu-id="79a82-130">Hello c + + 자습서에 대 한 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="79a82-130">Prerequisites for hello C++ tutorial</span></span>
<span data-ttu-id="79a82-131">Hello 다음 항목이 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="79a82-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="79a82-132">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="79a82-132">An active Azure account.</span></span> <span data-ttu-id="79a82-133">아직 구독하지 않은 경우 [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="79a82-134">[Visual Studio](https://www.visualstudio.com/downloads/), hello c + + 언어 구성 요소가 설치 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-134">[Visual Studio](https://www.visualstudio.com/downloads/), with hello C++ language components installed.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="79a82-135">1단계: Azure Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="79a82-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="79a82-136">Azure Cosmos DB 계정을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="79a82-137">Toouse 원하는 계정을 이미 있는 경우 건너뛰어도 너무[c + + 응용 프로그램 설치](#SetupNode)합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-137">If you already have an account you want toouse, you can skip ahead too[Setup your C++ application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="79a82-138"><a id="SetupC++"></a>2단계: C++ 응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="79a82-138"><a id="SetupC++"></a>Step 2: Set up your C++ application</span></span>
1. <span data-ttu-id="79a82-139">Visual Studio를 열고 hello에서 **파일** 메뉴를 클릭 **새로**, 클릭 하 고 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-139">Open Visual Studio, and then on hello **File** menu, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="79a82-140">Hello에 **새 프로젝트** 창의 hello **설치 됨** 창 확장 **Visual c + +**, 클릭 **Win32**, 클릭 하 고  **Win32 콘솔 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-140">In hello **New Project** window, in hello **Installed** pane, expand **Visual C++**, click **Win32**, and then click **Win32 Console Application**.</span></span> <span data-ttu-id="79a82-141">Hello 프로젝트 hellodocumentdb 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-141">Name hello project hellodocumentdb and then click **OK**.</span></span> 
   
    ![Hello 새 프로젝트 마법사의 스크린 샷](media/documentdb-cpp-get-started/hello.png)
3. <span data-ttu-id="79a82-143">Hello Win32 응용 프로그램 마법사가 시작 되 면 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-143">When hello Win32 Application Wizard starts, click **Finish**.</span></span>
4. <span data-ttu-id="79a82-144">Hello 프로젝트를 만든 후 hello를 마우스 오른쪽 단추로 클릭 하 여 hello NuGet 패키지 관리자를 열고 **hellodocumentdb** 프로젝트에서 **솔루션 탐색기** 클릭 하 고 **NuGet패키지관리**.</span><span class="sxs-lookup"><span data-stu-id="79a82-144">Once hello project has been created, open hello NuGet package manager by right-clicking hello **hellodocumentdb** project in **Solution Explorer** and clicking **Manage NuGet Packages**.</span></span> 
   
    ![Hello 프로젝트 메뉴에서 NuGet 패키지 관리를 보여 주는 스크린샷](media/documentdb-cpp-get-started/nuget.png)
5. <span data-ttu-id="79a82-146">Hello에 **NuGet: hellodocumentdb** 탭을 클릭 **찾아보기**, 검색할 *documentdbcpp*합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-146">In hello **NuGet: hellodocumentdb** tab, click **Browse**, and then search for *documentdbcpp*.</span></span> <span data-ttu-id="79a82-147">Hello 결과에 스크린 샷 다음 hello와 같이 DocumentDbCPP을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-147">In hello results, select DocumentDbCPP, as shown in hello following screenshot.</span></span> <span data-ttu-id="79a82-148">이 패키지 설치 참조 tooC + + REST SDK DocumentDbCPP hello에 대 한 종속성 합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-148">This package installs references tooC++ REST SDK, which is a dependency for hello DocumentDbCPP.</span></span>  
   
    ![강조 표시 된 hello DocumentDbCpp 패키지를 보여 주는 스크린샷](media/documentdb-cpp-get-started/cpp.png)
   
    <span data-ttu-id="79a82-150">Hello 패키지 tooyour 프로젝트를 추가한 후 모든 집합 toostart 코드를 작성 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-150">Once hello packages have been added tooyour project, we are all set toostart writing some code.</span></span>   

## <span data-ttu-id="79a82-151"><a id="Config"></a>3단계: Azure Cosmos DB 데이터베이스에 대한 Azure Portal의 연결 세부 정보 복사</span><span class="sxs-lookup"><span data-stu-id="79a82-151"><a id="Config"></a>Step 3: Copy connection details from Azure portal for your Azure Cosmos DB database</span></span>
<span data-ttu-id="79a82-152">(를) 실행 [Azure 포털](https://portal.azure.com) 만든 toohello Azure Cosmos DB 데이터베이스 계정을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-152">Bring up [Azure portal](https://portal.azure.com) and traverse toohello Azure Cosmos DB database account you created.</span></span> <span data-ttu-id="79a82-153">C + + 코드 조각의 우리의 hello URI 및 hello 다음 단계 tooestablish 연결에서에서 Azure 포털에서 기본 키 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-153">We will need hello URI and hello primary key from Azure portal in hello next step tooestablish a connection from our C++ code snippet.</span></span> 

![Azure Cosmos DB URI 및 키 hello Azure 포털에](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <span data-ttu-id="79a82-155"><a id="Connect"></a>4 단계: tooan Cosmos DB Azure 계정을 연결 하세요.</span><span class="sxs-lookup"><span data-stu-id="79a82-155"><a id="Connect"></a>Step 4: Connect tooan Azure Cosmos DB account</span></span>
1. <span data-ttu-id="79a82-156">추가 후 헤더 및 네임 스페이스 tooyour 소스 코드를 다음 hello `#include "stdafx.h"`합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-156">Add hello following headers and namespaces tooyour source code, after `#include "stdafx.h"`.</span></span>
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. <span data-ttu-id="79a82-157">다음 추가 hello 다음 tooyour main 함수를 코드로 바꾸고 hello 계정 구성 및 기본 키 toomatch 3 단계에서 Azure Cosmos DB 설정을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-157">Next add hello following code tooyour main function and replace hello account configuration and primary key toomatch your Azure Cosmos DB settings from step 3.</span></span> 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    <span data-ttu-id="79a82-158">Hello 코드 tooinitialize hello documentdb 클라이언트를가지고 살펴보겠습니다는 Azure Cosmos DB 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-158">Now that you have hello code tooinitialize hello documentdb client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <span data-ttu-id="79a82-159"><a id="CreateDBColl"></a>5단계: C++ 데이터베이스 및 컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="79a82-159"><a id="CreateDBColl"></a>Step 5: Create a C++ database and collection</span></span>
<span data-ttu-id="79a82-160">이 단계를 수행 하기 전에 새 tooAzure Cosmos DB 인 경우에 데이터베이스, 컬렉션 및 문서 상호 작용 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-160">Before we perform this step, let's go over how a database, collection and documents interact for those of you who are new tooAzure Cosmos DB.</span></span> <span data-ttu-id="79a82-161">[데이터베이스](documentdb-resources.md#databases)는 여러 컬렉션으로 분할된 문서 저장소의 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-161">A [database](documentdb-resources.md#databases) is a logical container of document storage portioned across collections.</span></span> <span data-ttu-id="79a82-162">A [컬렉션](documentdb-resources.md#collections) 는 JSON 문서의 컨테이너 및 hello 관련 JavaScript 응용 프로그램 논리입니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-162">A [collection](documentdb-resources.md#collections) is a container of JSON documents and hello associated JavaScript application logic.</span></span> <span data-ttu-id="79a82-163">Hello Azure Cosmos DB 계층적 리소스 모델 및 개념에 대 한 자세한 정보 학습할 수 있는 [Azure Cosmos DB 계층적 리소스 모델 및 개념](documentdb-resources.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-163">You can learn more about hello Azure Cosmos DB hierarchical resource model and concepts in [Azure Cosmos DB hierarchical resource model and concepts](documentdb-resources.md).</span></span>

<span data-ttu-id="79a82-164">toocreate 데이터베이스 및 해당 컬렉션 hello 코드 toohello의 끝 다음 main 함수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-164">toocreate a database and a corresponding collection add hello following code toohello end of your main function.</span></span> <span data-ttu-id="79a82-165">'FamilyRegistry' 및 'FamilyCollection' hello 이전 단계에서 선언 된 hello 클라이언트 구성을 사용 하 여 라는 컬렉션 라는 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-165">This creates a database called 'FamilyRegistry’ and a collection called ‘FamilyCollection’ using hello client configuration you declared in hello previous step.</span></span>

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <span data-ttu-id="79a82-166"><a id="CreateDoc"></a>6단계: 문서 만들기</span><span class="sxs-lookup"><span data-stu-id="79a82-166"><a id="CreateDoc"></a>Step 6: Create a document</span></span>
<span data-ttu-id="79a82-167">[문서](documentdb-resources.md#documents)는 사용자 정의(임의) JSON 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-167">[Documents](documentdb-resources.md#documents) are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="79a82-168">이제 Azure Cosmos DB에 문서를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-168">You can now insert a document into Azure Cosmos DB.</span></span> <span data-ttu-id="79a82-169">Hello hello main 함수 hello 끝에 코드를 다음 복사 하 여 문서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-169">You can create a document by copying hello following code into hello end of hello main function.</span></span> 

    try {
      value document_family;
      document_family[L"id"] = value::string(L"AndersenFamily");
      document_family[L"FirstName"] = value::string(L"Thomas");
      document_family[L"LastName"] = value::string(L"Andersen");
      shared_ptr<Document> doc = coll->CreateDocumentAsync(document_family).get();

      document_family[L"id"] = value::string(L"WakefieldFamily");
      document_family[L"FirstName"] = value::string(L"Lucy");
      document_family[L"LastName"] = value::string(L"Wakefield");
      doc = coll->CreateDocumentAsync(document_family).get();
    } catch (ResourceAlreadyExistsException ex) {
      wcout << ex.message();
    }

<span data-ttu-id="79a82-170">toosummarize,이 코드는 Azure Cosmos DB 데이터베이스, 컬렉션 및 Azure 포털의 문서 탐색기에서 쿼리할 수 있는 문서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-170">toosummarize, this code creates an Azure Cosmos DB database, collection, and documents, which you can query in Document Explorer in Azure portal.</span></span> 

![C + + 자습서-hello hello 계정과 hello 데이터베이스, hello 컬렉션 hello 문서 간의 계층 관계를 보여 주는 다이어그램](media/documentdb-cpp-get-started/docs.png)

## <span data-ttu-id="79a82-172"><a id="QueryDB"></a>7단계: Azure Cosmos DB 리소스 쿼리</span><span class="sxs-lookup"><span data-stu-id="79a82-172"><a id="QueryDB"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="79a82-173">Azure Cosmos DB는 각 컬렉션에 저장된 JSON 문서에 대해 [다양한 쿼리](documentdb-sql-query.md)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-173">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="79a82-174">hello 다음 샘플 코드에서는 hello 이전 단계에서 만든으로 hello 문서에 대해 실행할 수 있는 SQL 구문을 사용 하 여 수행 되는 쿼리</span><span class="sxs-lookup"><span data-stu-id="79a82-174">hello following sample code shows a query made using SQL syntax that you can run against hello documents we created in hello previous step.</span></span>

<span data-ttu-id="79a82-175">hello 함수 인수 hello 고유 식별자 또는 hello 데이터베이스와 함께 hello 문서 클라이언트 hello 컬렉션에 대 한 리소스 id에 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-175">hello function takes in as arguments hello unique identifier or resource id for hello database and hello collection along with hello document client.</span></span> <span data-ttu-id="79a82-176">main 함수 앞에 이 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-176">Add this code before main function.</span></span>

    void executesimplequery(const DocumentClient &client,
                            const wstring dbresourceid,
                            const wstring collresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        wstring coll_name = coll->id();
        shared_ptr<DocumentIterator> iter =
            coll->QueryDocumentsAsync(wstring(L"SELECT * FROM " + coll_name)).get();
        wcout << "\n\nQuerying collection:";
        while (iter->HasMore()) {
          shared_ptr<Document> doc = iter->Next();
          wstring doc_name = doc->id();
          wcout << "\n\t" << doc_name << "\n";
          wcout << "\t"
                << "[{\"FirstName\":"
                << doc->payload().at(U("FirstName")).as_string()
                << ",\"LastName\":" << doc->payload().at(U("LastName")).as_string()
                << "}]";
        }
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="79a82-177"><a id="Replace"></a>8단계: 문서 바꾸기</span><span class="sxs-lookup"><span data-stu-id="79a82-177"><a id="Replace"></a>Step 8: Replace a document</span></span>
<span data-ttu-id="79a82-178">Azure Cosmos DB hello 코드 다음에 표시 된 대로 교체 JSON 문서를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-178">Azure Cosmos DB supports replacing JSON documents, as demonstrated in hello following code.</span></span> <span data-ttu-id="79a82-179">Hello executesimplequery 함수 뒤에이 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-179">Add this code after hello executesimplequery function.</span></span>

    void replacedocument(const DocumentClient &client, const wstring dbresourceid,
                         const wstring collresourceid,
                         const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        value newdoc;
        newdoc[L"id"] = value::string(L"WakefieldFamily");
        newdoc[L"FirstName"] = value::string(L"Lucy");
        newdoc[L"LastName"] = value::string(L"Smith Wakefield");
        coll->ReplaceDocument(docresourceid, newdoc);
      } catch (DocumentDBRuntimeException ex) {
        throw;
      }
    }

## <span data-ttu-id="79a82-180"><a id="Delete"></a>9단계: 문서 삭제</span><span class="sxs-lookup"><span data-stu-id="79a82-180"><a id="Delete"></a>Step 9: Delete a document</span></span>
<span data-ttu-id="79a82-181">Azure Cosmos DB JSON 문서 삭제를 지원 하면 복사 및 붙여넣기 hello hello replacedocument 함수 뒤에 코드를 다음으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-181">Azure Cosmos DB supports deleting JSON documents, you can do so by copy and pasting hello following code after hello replacedocument function.</span></span> 

    void deletedocument(const DocumentClient &client, const wstring dbresourceid,
                        const wstring collresourceid, const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        coll->DeleteDocumentAsync(docresourceid).get();
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="79a82-182"><a id="DeleteDB"></a>10단계: 데이터베이스 삭제</span><span class="sxs-lookup"><span data-stu-id="79a82-182"><a id="DeleteDB"></a>Step 10: Delete a database</span></span>
<span data-ttu-id="79a82-183">삭제 만든 hello 데이터베이스 hello 데이터베이스와 모든 자식 리소스 (컬렉션, 문서 등)를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-183">Deleting hello created database removes hello database and all child resources (collections, documents, etc.).</span></span>

<span data-ttu-id="79a82-184">복사한 후 hello deletedocument 함수 tooremove hello 데이터베이스와 모든 hello 자식 리소스 코드 조각 (함수 정리)를 수행 하는 hello를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-184">Copy and paste hello following code snippet (function cleanup) after hello deletedocument function tooremove hello database and all hello child resources.</span></span>

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="79a82-185"><a id="Run"></a>11단계: C# 응용 프로그램 모두 함께 실행</span><span class="sxs-lookup"><span data-stu-id="79a82-185"><a id="Run"></a>Step 11: Run your C++ application all together!</span></span>
<span data-ttu-id="79a82-186">म 코드 toocreate 이제 추가한 쿼리, 수정 하 고 다른 Azure Cosmos DB 리소스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-186">We have now added code toocreate, query, modify, and delete different Azure Cosmos DB resources.</span></span>  <span data-ttu-id="79a82-187">주세요 이제이를 연결 hellodocumentdb.cpp 일부 진단 메시지와 함께에서 주 함수에서 호출 toothese 다양 한 기능을 추가 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-187">Let us now wire this up by adding calls toothese different functions from our main function in hellodocumentdb.cpp along with some diagnostic messages.</span></span>

<span data-ttu-id="79a82-188">응용 프로그램의 main 함수 hello 코드 다음 hello로 대체 하 여 그렇게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-188">You can do so by replacing hello main function of your application with hello following code.</span></span> <span data-ttu-id="79a82-189">이 쓰기 hello account_configuration_uri 및 primary_key 3 단계에서에서 hello 코드에 복사 하므로에서 해당 줄 또는 복사 된 hello 값 다시 저장 hello 포털에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-189">This writes over hello account_configuration_uri and primary_key you copied into hello code in Step 3, so save that line or copy hello values in again from hello portal.</span></span> 

    int main() {
        try {
            // Start by defining your account's configuration
            DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
            // Create your client
            DocumentClient client(conf);
            // Create a new database
            try {
                shared_ptr<Database> db = client.CreateDatabase(L"FamilyDB");
                wcout << "\nCreating database:\n" << db->id();
                // Create a collection inside database
                shared_ptr<Collection> coll = db->CreateCollection(L"FamilyColl");
                wcout << "\n\nCreating collection:\n" << coll->id();
                value document_family;
                document_family[L"id"] = value::string(L"AndersenFamily");
                document_family[L"FirstName"] = value::string(L"Thomas");
                document_family[L"LastName"] = value::string(L"Andersen");
                shared_ptr<Document> doc =
                    coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                document_family[L"id"] = value::string(L"WakefieldFamily");
                document_family[L"FirstName"] = value::string(L"Lucy");
                document_family[L"LastName"] = value::string(L"Wakefield");
                doc = coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                replacedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nReplaced document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                deletedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nDeleted document:\n" << doc->id();
                deletedb(client, db->resource_id());
                wcout << "\n\nDeleted db:\n" << db->id();
                cin.get();
            }
            catch (ResourceAlreadyExistsException ex) {
                wcout << ex.message();
            }
        }
        catch (DocumentDBRuntimeException ex) {
            wcout << ex.message();
        }
        cin.get();
    }

<span data-ttu-id="79a82-190">해야 이제 수 toobuild 수와 Visual Studio에서 f5 키를 눌러 코드를 실행할 또는 또는 hello 응용 프로그램을 찾아 실행 하 여 hello 터미널 창에서 실행를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-190">You should now be able toobuild and run your code in Visual Studio by pressing F5 or alternatively in hello terminal window by locating hello application and running hello executable.</span></span> 

<span data-ttu-id="79a82-191">Get 시작된 응용 프로그램의 hello 출력을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-191">You should see hello output of your get started app.</span></span> <span data-ttu-id="79a82-192">hello 출력 스크린 샷 다음 hello를 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-192">hello output should match hello following screenshot.</span></span>

![Azure Cosmos DB C++ 응용 프로그램 출력](media/documentdb-cpp-get-started/console.png)

<span data-ttu-id="79a82-194">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-194">Congratulations!</span></span> <span data-ttu-id="79a82-195">첫 번째 Azure Cosmos DB 콘솔 응용 프로그램 있고 hello c + + 자습서!</span><span class="sxs-lookup"><span data-stu-id="79a82-195">You've completed hello C++ tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="79a82-196"><a id="GetSolution"></a>Hello 전체 c + + 자습서 솔루션 가져오기</span><span class="sxs-lookup"><span data-stu-id="79a82-196"><a id="GetSolution"></a>Get hello complete C++ tutorial solution</span></span>
<span data-ttu-id="79a82-197">이 문서에서 모든 hello 예제가 포함 된 toobuild hello GetStarted 솔루션 hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-197">toobuild hello GetStarted solution that contains all hello samples in this article, you need hello following:</span></span>

* <span data-ttu-id="79a82-198">[Azure Cosmos DB 계정][create-account].</span><span class="sxs-lookup"><span data-stu-id="79a82-198">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="79a82-199">hello [GetStarted](https://github.com/stalker314314/DocumentDBCpp) 솔루션 GitHub에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-199">hello [GetStarted](https://github.com/stalker314314/DocumentDBCpp) solution available on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79a82-200">다음 단계</span><span class="sxs-lookup"><span data-stu-id="79a82-200">Next steps</span></span>
* <span data-ttu-id="79a82-201">너무 방법에 대해 알아봅니다[Azure Cosmos DB 계정을 모니터링](monitor-accounts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-201">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="79a82-202">Hello에 우리의 샘플 데이터 집합에 대해 쿼리 실행 [Query Playground](https://www.documentdb.com/sql/demo)합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-202">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="79a82-203">Hello hello의 개발 섹션에서에서 hello 프로그래밍 모델에 대 한 자세한 [Azure Cosmos DB 설명서 페이지](https://azure.microsoft.com/documentation/services/documentdb/)합니다.</span><span class="sxs-lookup"><span data-stu-id="79a82-203">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account


