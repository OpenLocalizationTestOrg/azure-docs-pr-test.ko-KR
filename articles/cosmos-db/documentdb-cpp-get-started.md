---
title: "Azure Cosmos DB에 대한 C++ 자습서 | Microsoft Docs"
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
ms.openlocfilehash: 7d8de973765830ccd7983182bc1bb19b1e01e505
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-c-console-application-tutorial-for-the-documentdb-api"></a><span data-ttu-id="993f3-104">Azure Cosmos DB: DocumentDB API에 대한 C++ 콘솔 응용 프로그램 자습서</span><span class="sxs-lookup"><span data-stu-id="993f3-104">Azure Cosmos DB: C++ console application tutorial for the DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="993f3-105">.NET</span><span class="sxs-lookup"><span data-stu-id="993f3-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="993f3-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="993f3-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="993f3-107">MongoDB용 Node.js</span><span class="sxs-lookup"><span data-stu-id="993f3-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="993f3-108">Node.JS</span><span class="sxs-lookup"><span data-stu-id="993f3-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="993f3-109">Java</span><span class="sxs-lookup"><span data-stu-id="993f3-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="993f3-110">C++</span><span class="sxs-lookup"><span data-stu-id="993f3-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 
 

<span data-ttu-id="993f3-111">C++용 Azure Cosmos DB DocumentDB API 인증 SDK에 대한 C++ 자습서를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-111">Welcome to the C++ tutorial for the Azure Cosmos DB DocumentDB API endorsed SDK for C++!</span></span> <span data-ttu-id="993f3-112">이 자습서를 따라 하면 C++ 데이터베이스를 포함하여 Azure Cosmos DB 리소스를 만들고 쿼리하는 콘솔 응용 프로그램이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources, including a C++ database.</span></span>

<span data-ttu-id="993f3-113">다음에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-113">We'll cover:</span></span>

* <span data-ttu-id="993f3-114">Azure Cosmos DB 계정 만들기 및 연결</span><span class="sxs-lookup"><span data-stu-id="993f3-114">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="993f3-115">응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="993f3-115">Setting up your application</span></span>
* <span data-ttu-id="993f3-116">C++ Azure Cosmos DB 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="993f3-116">Creating a C++ Azure Cosmos DB database</span></span>
* <span data-ttu-id="993f3-117">컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="993f3-117">Creating a collection</span></span>
* <span data-ttu-id="993f3-118">JSON 문서 만들기</span><span class="sxs-lookup"><span data-stu-id="993f3-118">Creating JSON documents</span></span>
* <span data-ttu-id="993f3-119">컬렉션 쿼리</span><span class="sxs-lookup"><span data-stu-id="993f3-119">Querying the collection</span></span>
* <span data-ttu-id="993f3-120">문서 바꾸기</span><span class="sxs-lookup"><span data-stu-id="993f3-120">Replacing a document</span></span>
* <span data-ttu-id="993f3-121">문서 삭제</span><span class="sxs-lookup"><span data-stu-id="993f3-121">Deleting a document</span></span>
* <span data-ttu-id="993f3-122">C++ Azure Cosmos DB 데이터베이스 삭제</span><span class="sxs-lookup"><span data-stu-id="993f3-122">Deleting the C++ Azure Cosmos DB database</span></span>

<span data-ttu-id="993f3-123">시간이 없으십니까?</span><span class="sxs-lookup"><span data-stu-id="993f3-123">Don't have time?</span></span> <span data-ttu-id="993f3-124">염려하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="993f3-124">Don't worry!</span></span> <span data-ttu-id="993f3-125">[GitHub](https://github.com/stalker314314/DocumentDBCpp)에서 전체 솔루션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-125">The complete solution is available on [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span></span> <span data-ttu-id="993f3-126">빠른 지침은 [전체 솔루션 다운로드](#GetSolution) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="993f3-126">See [Get the complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="993f3-127">C++ 자습서를 완료한 후에 이 페이지의 아래쪽에 있는 응답 단추를 통해 의견을 보내주세요.</span><span class="sxs-lookup"><span data-stu-id="993f3-127">After you've completed the C++ tutorial, please use the voting buttons at the bottom of this page to give us feedback.</span></span> 

<span data-ttu-id="993f3-128">직접 연락을 받고 싶은 경우 코멘트에 메일 주소를 적거나 [여기에 알려주세요](https://www.research.net/r/8BKRJ3Z).</span><span class="sxs-lookup"><span data-stu-id="993f3-128">If you'd like us to contact you directly, feel free to include your email address in your comments or [reach out to us here](https://www.research.net/r/8BKRJ3Z).</span></span> 

<span data-ttu-id="993f3-129">이제 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-129">Now let's get started!</span></span>

## <a name="prerequisites-for-the-c-tutorial"></a><span data-ttu-id="993f3-130">C++ 자습서의 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="993f3-130">Prerequisites for the C++ tutorial</span></span>
<span data-ttu-id="993f3-131">다음 항목이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-131">Please make sure you have the following:</span></span>

* <span data-ttu-id="993f3-132">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="993f3-132">An active Azure account.</span></span> <span data-ttu-id="993f3-133">아직 구독하지 않은 경우 [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="993f3-134">C++ 언어 구성 요소가 설치된 [Visual Studio](https://www.visualstudio.com/downloads/)입니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-134">[Visual Studio](https://www.visualstudio.com/downloads/), with the C++ language components installed.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="993f3-135">1단계: Azure Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="993f3-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="993f3-136">Azure Cosmos DB 계정을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="993f3-137">계정이 이미 있는 경우 [C++ 응용 프로그램 설치](#SetupNode)로 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-137">If you already have an account you want to use, you can skip ahead to [Setup your C++ application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="993f3-138"><a id="SetupC++"></a>2단계: C++ 응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="993f3-138"><a id="SetupC++"></a>Step 2: Set up your C++ application</span></span>
1. <span data-ttu-id="993f3-139">Visual Studio를 열고 **파일** 메뉴에서 **새로 만들기**를 클릭한 다음 **프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-139">Open Visual Studio, and then on the **File** menu, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="993f3-140">**새 프로젝트** 창의 **설치됨** 창에서 **Visual C++**를 확장하고 **Win32**, **Win32 콘솔 응용 프로그램**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-140">In the **New Project** window, in the **Installed** pane, expand **Visual C++**, click **Win32**, and then click **Win32 Console Application**.</span></span> <span data-ttu-id="993f3-141">프로젝트 이름을 hellodocumentdb로 지정한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-141">Name the project hellodocumentdb and then click **OK**.</span></span> 
   
    ![새 프로젝트 마법사의 스크린샷](media/documentdb-cpp-get-started/hello.png)
3. <span data-ttu-id="993f3-143">Win32 응용 프로그램 마법사가 시작되면 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-143">When the Win32 Application Wizard starts, click **Finish**.</span></span>
4. <span data-ttu-id="993f3-144">프로젝트를 만들면 **솔루션 탐색기**에서 **hellodocumentdb** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 클릭하여 NuGet 패키지 관리자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-144">Once the project has been created, open the NuGet package manager by right-clicking the **hellodocumentdb** project in **Solution Explorer** and clicking **Manage NuGet Packages**.</span></span> 
   
    ![프로젝트 메뉴에서 NuGet 패키지 관리를 보여 주는 스크린샷](media/documentdb-cpp-get-started/nuget.png)
5. <span data-ttu-id="993f3-146">**NuGet: hellodocumentdb** 탭에서 **찾아보기**를 클릭한 다음 *documentdbcpp*를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-146">In the **NuGet: hellodocumentdb** tab, click **Browse**, and then search for *documentdbcpp*.</span></span> <span data-ttu-id="993f3-147">결과에서 다음 스크린샷에 표시된 것처럼 DocumentDbCPP를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-147">In the results, select DocumentDbCPP, as shown in the following screenshot.</span></span> <span data-ttu-id="993f3-148">이 패키지에서는 DocumentDbCPP에 대한 종속성이 있는 C++ REST SDK에 대한 참조를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-148">This package installs references to C++ REST SDK, which is a dependency for the DocumentDbCPP.</span></span>  
   
    ![DocumentDbCpp 패키지를 강조 표시하는 스크린샷](media/documentdb-cpp-get-started/cpp.png)
   
    <span data-ttu-id="993f3-150">패키지가 프로젝트에 추가되면 코드 작성을 시작하는 설정이 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-150">Once the packages have been added to your project, we are all set to start writing some code.</span></span>   

## <span data-ttu-id="993f3-151"><a id="Config"></a>3단계: Azure Cosmos DB 데이터베이스에 대한 Azure Portal의 연결 세부 정보 복사</span><span class="sxs-lookup"><span data-stu-id="993f3-151"><a id="Config"></a>Step 3: Copy connection details from Azure portal for your Azure Cosmos DB database</span></span>
<span data-ttu-id="993f3-152">[Azure Portal](https://portal.azure.com)을 불러와서, 만든 Azure Cosmos DB 데이터베이스 계정에 트래버스합니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-152">Bring up [Azure portal](https://portal.azure.com) and traverse to the Azure Cosmos DB database account you created.</span></span> <span data-ttu-id="993f3-153">다음 단계에서는 C++ 코드 조각에서 연결을 설정하기 위해 Azure Portal의 URI 및 기본 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-153">We will need the URI and the primary key from Azure portal in the next step to establish a connection from our C++ code snippet.</span></span> 

![Azure Portal에서 Azure Cosmos DB URI 및 키](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <span data-ttu-id="993f3-155"><a id="Connect"></a>4단계: Azure Cosmos DB 계정에 연결</span><span class="sxs-lookup"><span data-stu-id="993f3-155"><a id="Connect"></a>Step 4: Connect to an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="993f3-156">`#include "stdafx.h"` 뒤의 소스 코드에 다음 헤더 및 네임스페이스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-156">Add the following headers and namespaces to your source code, after `#include "stdafx.h"`.</span></span>
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. <span data-ttu-id="993f3-157">그런 다음 main 함수에 다음 코드를 추가하고 계정 구성 및 기본 키를 바꾸어 3단계의 Azure Cosmos DB 설정과 일치시킵니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-157">Next add the following code to your main function and replace the account configuration and primary key to match your Azure Cosmos DB settings from step 3.</span></span> 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    <span data-ttu-id="993f3-158">documentdb 계정을 시작하는 코드가 있다면 Azure Cosmos DB 리소스와 함께 작동하는지 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-158">Now that you have the code to initialize the documentdb client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <span data-ttu-id="993f3-159"><a id="CreateDBColl"></a>5단계: C++ 데이터베이스 및 컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="993f3-159"><a id="CreateDBColl"></a>Step 5: Create a C++ database and collection</span></span>
<span data-ttu-id="993f3-160">이 단계를 수행하기 전에 Azure Cosmos DB를 처음 접하는 경우 데이터베이스, 컬렉션 및 문서가 상호 작용하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-160">Before we perform this step, let's go over how a database, collection and documents interact for those of you who are new to Azure Cosmos DB.</span></span> <span data-ttu-id="993f3-161">[데이터베이스](documentdb-resources.md#databases)는 여러 컬렉션으로 분할된 문서 저장소의 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-161">A [database](documentdb-resources.md#databases) is a logical container of document storage portioned across collections.</span></span> <span data-ttu-id="993f3-162">[컬렉션](documentdb-resources.md#collections)은 JSON 문서 및 관련 JavaScript 응용 프로그램 논리의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-162">A [collection](documentdb-resources.md#collections) is a container of JSON documents and the associated JavaScript application logic.</span></span> <span data-ttu-id="993f3-163">[Azure Cosmos DB 계층적 리소스 모델 및 개념](documentdb-resources.md)에서 Azure Cosmos DB 계층적 리소스 모델 및 개념에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-163">You can learn more about the Azure Cosmos DB hierarchical resource model and concepts in [Azure Cosmos DB hierarchical resource model and concepts](documentdb-resources.md).</span></span>

<span data-ttu-id="993f3-164">데이터베이스와 해당 컬렉션을 만들려면 main 함수 끝에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-164">To create a database and a corresponding collection add the following code to the end of your main function.</span></span> <span data-ttu-id="993f3-165">이전 단계에서 선언한 클라이언트 구성을 사용하여 'FamilyRegistry'라는 데이터베이스 및 'FamilyCollection'라는 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-165">This creates a database called 'FamilyRegistry’ and a collection called ‘FamilyCollection’ using the client configuration you declared in the previous step.</span></span>

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <span data-ttu-id="993f3-166"><a id="CreateDoc"></a>6단계: 문서 만들기</span><span class="sxs-lookup"><span data-stu-id="993f3-166"><a id="CreateDoc"></a>Step 6: Create a document</span></span>
<span data-ttu-id="993f3-167">[문서](documentdb-resources.md#documents)는 사용자 정의(임의) JSON 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-167">[Documents](documentdb-resources.md#documents) are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="993f3-168">이제 Azure Cosmos DB에 문서를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-168">You can now insert a document into Azure Cosmos DB.</span></span> <span data-ttu-id="993f3-169">main 함수의 끝에 다음 코드를 복사하여 문서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-169">You can create a document by copying the following code into the end of the main function.</span></span> 

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

<span data-ttu-id="993f3-170">요약하자면 이 코드는 Azure Portal의 문서 탐색기에서 쿼리할 수 있는 Azure Cosmos DB 데이터베이스, 컬렉션 및 문서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-170">To summarize, this code creates an Azure Cosmos DB database, collection, and documents, which you can query in Document Explorer in Azure portal.</span></span> 

![C++ 자습서 - 계정, 데이터베이스, 컬렉션 및 문서 간의 계층 관계를 보여 주는 다이어그램](media/documentdb-cpp-get-started/docs.png)

## <span data-ttu-id="993f3-172"><a id="QueryDB"></a>7단계: Azure Cosmos DB 리소스 쿼리</span><span class="sxs-lookup"><span data-stu-id="993f3-172"><a id="QueryDB"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="993f3-173">Azure Cosmos DB는 각 컬렉션에 저장된 JSON 문서에 대해 [다양한 쿼리](documentdb-sql-query.md)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-173">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="993f3-174">다음 샘플 코드는 SQL 구문을 사용해서 만든 다양한 쿼리를 보여 줍니다. 이러한 쿼리는 이전 단계에서 만든 문서에 대해 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-174">The following sample code shows a query made using SQL syntax that you can run against the documents we created in the previous step.</span></span>

<span data-ttu-id="993f3-175">함수는 문서 클라이언트와 함께 데이터베이스 및 컬렉션에 대한 고유한 식별자 또는 리소스 ID를 인수로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-175">The function takes in as arguments the unique identifier or resource id for the database and the collection along with the document client.</span></span> <span data-ttu-id="993f3-176">main 함수 앞에 이 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-176">Add this code before main function.</span></span>

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

## <span data-ttu-id="993f3-177"><a id="Replace"></a>8단계: 문서 바꾸기</span><span class="sxs-lookup"><span data-stu-id="993f3-177"><a id="Replace"></a>Step 8: Replace a document</span></span>
<span data-ttu-id="993f3-178">Azure Cosmos DB는 다음 코드에서와 같이 JSON 문서를 바꾸도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-178">Azure Cosmos DB supports replacing JSON documents, as demonstrated in the following code.</span></span> <span data-ttu-id="993f3-179">executesimplequery 함수 뒤에 이 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-179">Add this code after the executesimplequery function.</span></span>

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

## <span data-ttu-id="993f3-180"><a id="Delete"></a>9단계: 문서 삭제</span><span class="sxs-lookup"><span data-stu-id="993f3-180"><a id="Delete"></a>Step 9: Delete a document</span></span>
<span data-ttu-id="993f3-181">Azure Cosmos DB는 JSON 문서를 삭제하도록 지원합니다. replacedocument 함수 뒤에 다음 코드를 복사하고 붙여 넣는 방법으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-181">Azure Cosmos DB supports deleting JSON documents, you can do so by copy and pasting the following code after the replacedocument function.</span></span> 

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

## <span data-ttu-id="993f3-182"><a id="DeleteDB"></a>10단계: 데이터베이스 삭제</span><span class="sxs-lookup"><span data-stu-id="993f3-182"><a id="DeleteDB"></a>Step 10: Delete a database</span></span>
<span data-ttu-id="993f3-183">만든 데이터베이스를 삭제하면 데이터베이스와 모든 자식 리소스(컬렉션, 문서 등)가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-183">Deleting the created database removes the database and all child resources (collections, documents, etc.).</span></span>

<span data-ttu-id="993f3-184">deletedocument 함수 뒤에 다음 코드 조각(함수 정리)을 복사하고 붙여넣어서 데이터베이스와 모든 하위 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-184">Copy and paste the following code snippet (function cleanup) after the deletedocument function to remove the database and all the child resources.</span></span>

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="993f3-185"><a id="Run"></a>11단계: C# 응용 프로그램 모두 함께 실행</span><span class="sxs-lookup"><span data-stu-id="993f3-185"><a id="Run"></a>Step 11: Run your C++ application all together!</span></span>
<span data-ttu-id="993f3-186">이제 다른 Azure Cosmos DB 리소스를 만들기, 쿼리, 수정 및 삭제하는 코드를 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-186">We have now added code to create, query, modify, and delete different Azure Cosmos DB resources.</span></span>  <span data-ttu-id="993f3-187">이제 몇몇 진단 메시지와 함께 hellodocumentdb.cpp에서 main 함수의 이러한 다양한 기능에 대한 호출을 추가하여 마무리합니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-187">Let us now wire this up by adding calls to these different functions from our main function in hellodocumentdb.cpp along with some diagnostic messages.</span></span>

<span data-ttu-id="993f3-188">다음 코드로 응용 프로그램의 main 함수를 대체하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-188">You can do so by replacing the main function of your application with the following code.</span></span> <span data-ttu-id="993f3-189">3단계에서 코드에 복사한 account_configuration_uri 및 primary_key를 덮어 쓰기 때문에 해당 줄을 저장하거나 포털에서의 값을 다시 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-189">This writes over the account_configuration_uri and primary_key you copied into the code in Step 3, so save that line or copy the values in again from the portal.</span></span> 

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

<span data-ttu-id="993f3-190">이제 Visual Studio에서 F5 키를 누르거나 터미널 창에서 응용 프로그램을 찾고 실행 파일을 실행하여 코드를 빌드하고 실행할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-190">You should now be able to build and run your code in Visual Studio by pressing F5 or alternatively in the terminal window by locating the application and running the executable.</span></span> 

<span data-ttu-id="993f3-191">시작한 앱의 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-191">You should see the output of your get started app.</span></span> <span data-ttu-id="993f3-192">축력은 다음 스크린샷과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-192">The output should match the following screenshot.</span></span>

![Azure Cosmos DB C++ 응용 프로그램 출력](media/documentdb-cpp-get-started/console.png)

<span data-ttu-id="993f3-194">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-194">Congratulations!</span></span> <span data-ttu-id="993f3-195">C++ 자습서를 완료했으며 첫 번째 Azure Cosmos DB 콘솔 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-195">You've completed the C++ tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="993f3-196"><a id="GetSolution"></a> 전체 C++ 자습서 솔루션 가져오기</span><span class="sxs-lookup"><span data-stu-id="993f3-196"><a id="GetSolution"></a>Get the complete C++ tutorial solution</span></span>
<span data-ttu-id="993f3-197">이 문서의 모든 샘플을 포함하는 GetStarted 솔루션을 빌드하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-197">To build the GetStarted solution that contains all the samples in this article, you need the following:</span></span>

* <span data-ttu-id="993f3-198">[Azure Cosmos DB 계정][create-account].</span><span class="sxs-lookup"><span data-stu-id="993f3-198">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="993f3-199">GitHub에서 제공하는 [GetStarted](https://github.com/stalker314314/DocumentDBCpp) 솔루션</span><span class="sxs-lookup"><span data-stu-id="993f3-199">The [GetStarted](https://github.com/stalker314314/DocumentDBCpp) solution available on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="993f3-200">다음 단계</span><span class="sxs-lookup"><span data-stu-id="993f3-200">Next steps</span></span>
* <span data-ttu-id="993f3-201">[Azure Cosmos DB 계정 모니터링](monitor-accounts.md) 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="993f3-201">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="993f3-202">[쿼리 실습](https://www.documentdb.com/sql/demo)의 샘플 데이터 집합에 대해 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-202">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="993f3-203">[Azure Cosmos DB 설명서](https://azure.microsoft.com/documentation/services/documentdb/) 페이지의 개발 섹션에서 프로그래밍 모델에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="993f3-203">Learn more about the programming model in the Develop section of the [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account


