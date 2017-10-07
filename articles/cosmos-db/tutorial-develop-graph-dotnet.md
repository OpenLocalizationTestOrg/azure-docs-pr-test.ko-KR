---
title: "Azure Cosmos DB: hello.NET에서 Graph API를 사용 하 여 개발 | Microsoft Docs"
description: "자세한 방법을 toodevelop.NET을 사용 하 여 Azure Cosmos DB DocumentDB api"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: cc8df0be-672b-493e-95a4-26dd52632261
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.custom: mvc
ms.openlocfilehash: 12e435d8169aeee6e818dac4a3b66c7a0ec5f2d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-graph-api-in-net"></a><span data-ttu-id="f9bd8-103">Azure Cosmos DB: hello.NET에서 Graph API를 사용 하 여 개발</span><span class="sxs-lookup"><span data-stu-id="f9bd8-103">Azure Cosmos DB: Develop with hello Graph API in .NET</span></span>
<span data-ttu-id="f9bd8-104">Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-104">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span></span> <span data-ttu-id="f9bd8-105">신속 하 게 만들기 및 문서, 키/값 및 hello 글로벌 배포 및 수평 확장이 기능 Cosmos DB Azure의 hello 핵심에에서 활용 중 일부는 그래프 데이터베이스를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="f9bd8-106">이 자습서에서는 하 고 사용 하 여 Azure Cosmos DB 계정을 toocreate hello Azure 포털 방법 설명 toocreate 그래프 데이터베이스 및 컨테이너.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-106">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal and how toocreate a graph database and container.</span></span> <span data-ttu-id="f9bd8-107">hello 만듭니다 간단한 소셜 네트워크 hello를 사용 하 여 4 명의 사람과 [Graph API](graph-sdk-dotnet.md) (미리 보기) 트래버스하 고 Gremlin를 사용 하 여 hello 그래프를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-107">hello application then creates a simple social network with four people using hello [Graph API](graph-sdk-dotnet.md) (preview), then traverses and queries hello graph using Gremlin.</span></span>

<span data-ttu-id="f9bd8-108">이 자습서에서는 hello 다음 작업 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-108">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f9bd8-109">Azure Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="f9bd8-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="f9bd8-110">그래프 데이터베이스 및 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="f9bd8-110">Create a graph database and container</span></span>
> * <span data-ttu-id="f9bd8-111">꼭 짓 점 및 가장자리 too.NET 개체 serialize</span><span class="sxs-lookup"><span data-stu-id="f9bd8-111">Serialize vertices and edges too.NET objects</span></span>
> * <span data-ttu-id="f9bd8-112">꼭짓점 및 가장자리 추가</span><span class="sxs-lookup"><span data-stu-id="f9bd8-112">Add vertices and edges</span></span>
> * <span data-ttu-id="f9bd8-113">Gremlin를 사용 하 여 쿼리 hello 그래프</span><span class="sxs-lookup"><span data-stu-id="f9bd8-113">Query hello graph using Gremlin</span></span>

## <a name="graphs-in-azure-cosmos-db"></a><span data-ttu-id="f9bd8-114">Azure Cosmos DB의 그래프</span><span class="sxs-lookup"><span data-stu-id="f9bd8-114">Graphs in Azure Cosmos DB</span></span>
<span data-ttu-id="f9bd8-115">Azure Cosmos DB toocreate, 업데이트 및 hello를 사용 하 여 쿼리 그래프를 사용할 수 있습니다 [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-115">You can use Azure Cosmos DB toocreate, update, and query graphs using hello [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) library.</span></span> <span data-ttu-id="f9bd8-116">단일 확장 메서드를 제공 하는 hello Microsoft.Azure.Graph 라이브러리 `CreateGremlinQuery<T>` hello 위에 `DocumentClient` tooexecute Gremlin 쿼리 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-116">hello Microsoft.Azure.Graph library provides a single extension method `CreateGremlinQuery<T>` on top of hello `DocumentClient` class tooexecute Gremlin queries.</span></span>

<span data-ttu-id="f9bd8-117">Gremlin은 쓰기 작업(DML)과 쿼리 및 순회 작업을 지원하는 함수형 프로그래밍 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-117">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="f9bd8-118">이 문서 tooget에 몇 가지 예가 Gremlin와 시작 프로그램 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-118">We cover a few examples in this article tooget your started with Gremlin.</span></span> <span data-ttu-id="f9bd8-119">Azure Cosmos DB에서 사용할 수 있는 Gremlin 기능에 대한 자세한 연습은 [Gremlin 쿼리](gremlin-support.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-119">See [Gremlin queries](gremlin-support.md) for a detailed walkthrough of Gremlin capabilities available in Azure Cosmos DB.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f9bd8-120">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f9bd8-120">Prerequisites</span></span>
<span data-ttu-id="f9bd8-121">Hello 다음 항목이 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-121">Please make sure you have hello following:</span></span>

* <span data-ttu-id="f9bd8-122">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-122">An active Azure account.</span></span> <span data-ttu-id="f9bd8-123">계정이 없는 경우 [무료 계정](https://azure.microsoft.com/free/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-123">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="f9bd8-124">Hello 또는 사용할 수 있습니다 [Azure DocumentDB 에뮬레이터](local-emulator.md) 이 자습서에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-124">Alternatively, you can use hello [Azure DocumentDB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="f9bd8-125">[Visual Studio](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="f9bd8-125">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-database-account"></a><span data-ttu-id="f9bd8-126">데이터베이스 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="f9bd8-126">Create database account</span></span>

<span data-ttu-id="f9bd8-127">Hello Azure 포털에서에서 Azure Cosmos DB 계정을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-127">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="f9bd8-128">Azure Cosmos DB 계정이 이미 있나요?</span><span class="sxs-lookup"><span data-stu-id="f9bd8-128">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="f9bd8-129">이 경우 건너뛰고 너무[Visual Studio 솔루션 설정](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="f9bd8-129">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="f9bd8-130">Azure DocumentDB 계정이 있나요?</span><span class="sxs-lookup"><span data-stu-id="f9bd8-130">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="f9bd8-131">따라서 사용자 계정이 Azure Cosmos DB 계정인 이제 하 고 건너뛰어도 너무[Visual Studio 솔루션 설정](#SetupVS)합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-131">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="f9bd8-132">Hello Azure Cosmos DB 에뮬레이터를 사용 하는 경우 hello 단계에 따르십시오 [Azure Cosmos DB 에뮬레이터](local-emulator.md) toosetup 에뮬레이터 hello 및 너무 건너 뛸[Visual Studio 솔루션 설정](#SetupVS)합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-132">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
> 

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <span data-ttu-id="f9bd8-133"><a id="SetupVS"></a>Visual Studio 솔루션 설치</span><span class="sxs-lookup"><span data-stu-id="f9bd8-133"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="f9bd8-134">컴퓨터에서 **Visual Studio**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-134">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="f9bd8-135">Hello에 **파일** 메뉴 선택 **새로**를 선택한 후 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-135">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="f9bd8-136">Hello에 **새 프로젝트** 대화 상자에서 **템플릿** / **Visual C#** / **콘솔 응용 프로그램 (.NET Framework)**프로젝트 이름을 지정 하 고 클릭 한 다음, **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-136">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
4. <span data-ttu-id="f9bd8-137">Hello에 **솔루션 탐색기**을 Visual Studio 솔루션에서 사용 중인 새 콘솔 응용 프로그램을 마우스 오른쪽 단추로 클릭 하 고 클릭 **NuGet 패키지 관리...**</span><span class="sxs-lookup"><span data-stu-id="f9bd8-137">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
5. <span data-ttu-id="f9bd8-138">Hello에 **NuGet** 탭을 클릭 **찾아보기**, 유형과 **Microsoft.Azure.Graphs** hello 검색 상자 및 확인란 hello **시험판 버전포함**.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-138">In hello **NuGet** tab, click **Browse**, and type **Microsoft.Azure.Graphs** in hello search box, and check hello **Include prerelease versions**.</span></span>
6. <span data-ttu-id="f9bd8-139">Hello 결과 내 찾을 **Microsoft.Azure.Graphs** 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-139">Within hello results, find **Microsoft.Azure.Graphs** and click **Install**.</span></span>
   
   <span data-ttu-id="f9bd8-140">클릭 하 여 변경 내용을 toohello 솔루션을 검토 하는 방법에 대 한 메시지를 가져오면 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-140">If you get a message about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="f9bd8-141">라이선스 승인에 관한 메시지가 표시되면 **동의합니다.**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-141">If you get a message about license acceptance, click **I accept**.</span></span>
   
    <span data-ttu-id="f9bd8-142">hello `Microsoft.Azure.Graphs` 단일 확장 메서드를 제공 하는 라이브러리 `CreateGremlinQuery<T>` Gremlin 작업을 실행 하기 위한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-142">hello `Microsoft.Azure.Graphs` library provides a single extension method `CreateGremlinQuery<T>` for executing Gremlin operations.</span></span> <span data-ttu-id="f9bd8-143">Gremlin은 쓰기 작업(DML)과 쿼리 및 순회 작업을 지원하는 함수형 프로그래밍 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-143">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="f9bd8-144">이 문서 tooget에 몇 가지 예가 Gremlin와 시작 프로그램 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-144">We cover a few examples in this article tooget your started with Gremlin.</span></span> <span data-ttu-id="f9bd8-145">[Gremlin 쿼리](gremlin-support.md)에는 Azure Cosmos DB의 Gremlin 기능에 대한 자세한 연습이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-145">[Gremlin queries](gremlin-support.md) has a detailed walkthrough of Gremlin capabilities in Azure Cosmos DB.</span></span>

## <span data-ttu-id="f9bd8-146"><a id="add-references"></a>앱 연결</span><span class="sxs-lookup"><span data-stu-id="f9bd8-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="f9bd8-147">응용 프로그램에 이 두 상수와 *client* 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-147">Add these two constants and your *client* variable in your application.</span></span> 

```csharp
string endpoint = ConfigurationManager.AppSettings["Endpoint"]; 
string authKey = ConfigurationManager.AppSettings["AuthKey"]; 
``` 
<span data-ttu-id="f9bd8-148">Toohello 돌아가 다음으로, [Azure 포털](https://portal.azure.com) tooretrieve 끝점 URL 및 기본 키입니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-148">Next, head back toohello [Azure portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="f9bd8-149">hello 끝점 URL 및 기본 키가 응용 프로그램 toounderstand에 필요한 위치 tooconnect 되며, Azure Cosmos DB tootrust에 대 한 응용 프로그램의 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-149">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span> 

<span data-ttu-id="f9bd8-150">에 Azure 포털 hello, tooyour Azure Cosmos DB 계정 탐색, 클릭 **키**, 클릭 하 고 **읽기-쓰기 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-150">In hello Azure portal, navigate tooyour Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span> 

<span data-ttu-id="f9bd8-151">Hello 포털에서 hello URI를 복사 하 고 붙여넣어 `Endpoint` 위의 hello 끝점 속성에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-151">Copy hello URI from hello portal and paste it over `Endpoint` in hello endpoint property above.</span></span> <span data-ttu-id="f9bd8-152">그런 다음 복사본 hello 포털에서 기본 키를 hello 및 hello에 붙여 `AuthKey` 위의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-152">Then copy hello PRIMARY KEY from hello portal and paste it into hello `AuthKey` property above.</span></span> 

<span data-ttu-id="f9bd8-153">! [Hello Azure 포털의 스크린 샷 hello 자습서 toocreate 하 여 C# 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-153">![Screen shot of hello Azure portal used by hello tutorial toocreate a C# application.</span></span> <span data-ttu-id="f9bd8-154">키 단추에 강조 표시 된 hello Azure Cosmos DB 탐색 및 hello URI 및 기본 키 값에 강조 표시 된 hello 키 블레이드에서 Azure Cosmos DB 계정 hello 표시] [키]</span><span class="sxs-lookup"><span data-stu-id="f9bd8-154">Shows an Azure Cosmos DB account hello KEYS button highlighted on hello Azure Cosmos DB navigation , and hello URI and PRIMARY KEY values highlighted on hello Keys blade][keys]</span></span> 
 
## <span data-ttu-id="f9bd8-155"><a id="instantiate"></a>Hello DocumentClient 인스턴스화합니다</span><span class="sxs-lookup"><span data-stu-id="f9bd8-155"><a id="instantiate"></a>Instantiate hello DocumentClient</span></span> 
<span data-ttu-id="f9bd8-156">다음으로 hello의 새 인스턴스를 만듭니다 **DocumentClient**합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-156">Next, create a new instance of hello **DocumentClient**.</span></span>  

```csharp 
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey); 
``` 

## <span data-ttu-id="f9bd8-157"><a id="create-database"></a>데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="f9bd8-157"><a id="create-database"></a>Create a database</span></span> 

<span data-ttu-id="f9bd8-158">이제 Azure Cosmos DB 만들 [데이터베이스](documentdb-resources.md#databases) hello를 사용 하 여 [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) 메서드 또는 [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) hello 방식의  **DocumentClient** hello에서 클래스 [DocumentDB.NET SDK](documentdb-sdk-dotnet.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-158">Now, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class from hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span>  

```csharp 
Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" }); 
``` 
 
## <a name="create-a-graph"></a><span data-ttu-id="f9bd8-159">그래프 만들기</span><span class="sxs-lookup"><span data-stu-id="f9bd8-159">Create a graph</span></span> 

<span data-ttu-id="f9bd8-160">다음으로 hello를 사용 하 여 hello를 사용 하 여 그래프의 컨테이너를 만들 [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) 메서드 또는 [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) hello 방식의 **DocumentClient**  클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-160">Next, create a graph container by using hello using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="f9bd8-161">컬렉션은 그래프 엔터티의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-161">A collection is a container of graph entities.</span></span> 

```csharp 
DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync( 
    UriFactory.CreateDatabaseUri("graphdb"), 
    new DocumentCollection { Id = "graphcollz" }, 
    new RequestOptions { OfferThroughput = 1000 }); 
``` 

## <span data-ttu-id="f9bd8-162"><a id="serializing"></a>꼭 짓 점 및 가장자리 too.NET 개체 serialize</span><span class="sxs-lookup"><span data-stu-id="f9bd8-162"><a id="serializing"></a>Serialize vertices and edges too.NET objects</span></span>
<span data-ttu-id="f9bd8-163">Azure Cosmos DB hello를 사용 하 여 [GraphSON 통신 형식](gremlin-support.md), 꼭 짓 점, 모서리 및 속성에 대 한 JSON 스키마를 정의 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-163">Azure Cosmos DB uses hello [GraphSON wire format](gremlin-support.md), which defines a JSON schema for vertices, edges, and properties.</span></span> <span data-ttu-id="f9bd8-164">이렇게 하면 코드에서 작업할 수 있습니다 있는.NET 개체로 GraphSON tooserialize/역직렬화 및 hello Cosmos DB AZURE.NET SDK를 종속성으로 JSON.NET 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-164">hello Azure Cosmos DB .NET SDK includes JSON.NET as a dependency, and this allows us tooserialize/deserialize GraphSON into .NET objects that we can work with in code.</span></span>

<span data-ttu-id="f9bd8-165">예를 들어 4명의 사람으로 구성된 포함된 간단한 소셜 네트워크로 작업해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-165">As an example, let's work with a simple social network with four people.</span></span> <span data-ttu-id="f9bd8-166">방법을 살펴볼 toocreate `Person` 꼭지점 추가 `Knows` 다음 사이의 관계를 쿼리하고 hello 그래프 toofind "친한 친구의 친구" 관계를 트래버스 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-166">We look at how toocreate `Person` vertices, add `Knows` relationships between them, then query and traverse hello graph toofind "friend of friend" relationships.</span></span> 

<span data-ttu-id="f9bd8-167">hello `Microsoft.Azure.Graphs.Elements` 네임 스페이스를 제공 `Vertex`, `Edge`, `Property` 및 `VertexProperty` GraphSON 응답 toowell 정의.NET 개체를 역직렬화 하는 동안에 대 한 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-167">hello `Microsoft.Azure.Graphs.Elements` namespace provides `Vertex`, `Edge`, `Property` and `VertexProperty` classes for deserializing GraphSON responses toowell-defined .NET objects.</span></span>

## <a name="run-gremlin-using-creategremlinquery"></a><span data-ttu-id="f9bd8-168">CreateGremlinQuery를 사용하여 Gremlin 실행</span><span class="sxs-lookup"><span data-stu-id="f9bd8-168">Run Gremlin using CreateGremlinQuery</span></span>
<span data-ttu-id="f9bd8-169">Gremlin은 SQL과 마찬가지로 읽기, 쓰기 및 쿼리 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-169">Gremlin, like SQL, supports read, write, and query operations.</span></span> <span data-ttu-id="f9bd8-170">예를 들어 hello 다음 코드 조각에서는 toocreate 꼭지점, 가장자리를 사용 하 여 몇 가지 샘플 쿼리를 수행 하는 방법 `CreateGremlinQuery<T>`, 비동기적으로 사용 하 여 이러한 결과 반복 하 고 `ExecuteNextAsync` 및 ' HasMoreResults 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-170">For example, hello following snippet shows how toocreate vertices, edges, perform some sample queries using `CreateGremlinQuery<T>`, and asynchronously iterate through these results using `ExecuteNextAsync` and \`HasMoreResults.</span></span>

```cs
Dictionary<string, string> gremlinQueries = new Dictionary<string, string>
{
    { "Cleanup",        "g.V().drop()" },
    { "AddVertex 1",    "g.addV('person').property('id', 'thomas').property('firstName', 'Thomas').property('age', 44)" },
    { "AddVertex 2",    "g.addV('person').property('id', 'mary').property('firstName', 'Mary').property('lastName', 'Andersen').property('age', 39)" },
    { "AddVertex 3",    "g.addV('person').property('id', 'ben').property('firstName', 'Ben').property('lastName', 'Miller')" },
    { "AddVertex 4",    "g.addV('person').property('id', 'robin').property('firstName', 'Robin').property('lastName', 'Wakefield')" },
    { "AddEdge 1",      "g.V('thomas').addE('knows').to(g.V('mary'))" },
    { "AddEdge 2",      "g.V('thomas').addE('knows').to(g.V('ben'))" },
    { "AddEdge 3",      "g.V('ben').addE('knows').to(g.V('robin'))" },
    { "UpdateVertex",   "g.V('thomas').property('age', 44)" },
    { "CountVertices",  "g.V().count()" },
    { "Filter Range",   "g.V().hasLabel('person').has('age', gt(40))" },
    { "Project",        "g.V().hasLabel('person').values('firstName')" },
    { "Sort",           "g.V().hasLabel('person').order().by('firstName', decr)" },
    { "Traverse",       "g.V('thomas').outE('knows').inV().hasLabel('person')" },
    { "Traverse 2x",    "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')" },
    { "Loop",           "g.V('thomas').repeat(out()).until(has('id', 'robin')).path()" },
    { "DropEdge",       "g.V('thomas').outE('knows').where(inV().has('id', 'mary')).drop()" },
    { "CountEdges",     "g.E().count()" },
    { "DropVertex",     "g.V('thomas').drop()" },
};

foreach (KeyValuePair<string, string> gremlinQuery in gremlinQueries)
{
    Console.WriteLine($"Running {gremlinQuery.Key}: {gremlinQuery.Value}");

    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, gremlinQuery.Value);
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    Console.WriteLine();
}
```

## <a name="add-vertices-and-edges"></a><span data-ttu-id="f9bd8-171">꼭짓점 및 가장자리 추가</span><span class="sxs-lookup"><span data-stu-id="f9bd8-171">Add vertices and edges</span></span>

<span data-ttu-id="f9bd8-172">Hello Gremlin 문을 자세히 hello 섹션 앞에 표시 된 것을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-172">Let's look at hello Gremlin statements shown in hello preceding section more detail.</span></span> <span data-ttu-id="f9bd8-173">먼저 Gremlin의 `addV` 메서드를 사용하는 몇 가지 꼭짓점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-173">First we some vertices using Gremlin's `addV` method.</span></span> <span data-ttu-id="f9bd8-174">예를 들어 hello 다음 조각에서는 "Person" 형식의 "Thomas Andersen" 꼭지점 이름, 성, 이름 및 보존 기간에 대 한 속성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-174">For example, hello following snippet creates a "Thomas Andersen" vertex of type "Person", with properties for first name, last name, and age.</span></span>

```cs
// Create a vertex
IDocumentQuery<Vertex> createVertexQuery = client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.addV('person').property('firstName', 'Thomas')");

while (createVertexQuery.HasMoreResults)
{
    Vertex thomas = (await create.ExecuteNextAsync<Vertex>()).First();
}
```

<span data-ttu-id="f9bd8-175">그런 다음 Gremlin의 `addE` 메서드를 사용하여 이 꼭짓점 사이에 몇 개의 가장자리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-175">Then we create some edges between these vertices using Gremlin's `addE` method.</span></span> 

```cs
// Add a "knows" edge
IDocumentQuery<Edge> createEdgeQuery = client.CreateGremlinQuery<Edge>(
    graphCollection, 
    "g.V('thomas').addE('knows').to(g.V('mary'))");

while (create.HasMoreResults)
{
    Edge thomasKnowsMaryEdge = (await create.ExecuteNextAsync<Edge>()).First();
}
```

<span data-ttu-id="f9bd8-176">Gremlin의 `properties` 단계를 사용하여 기존 꼭짓점을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-176">We can update an existing vertex by using `properties` step in Gremlin.</span></span> <span data-ttu-id="f9bd8-177">Hello 호출 tooexecute hello를 통해 쿼리를 건너뛰고 `HasMoreResults` 및 `ExecuteNextAsync` hello 나머지 hello 예제에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-177">We skip hello call tooexecute hello query via `HasMoreResults` and `ExecuteNextAsync` for hello rest of hello examples.</span></span>

```cs
// Update a vertex
client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.V('thomas').property('age', 45)");
```

<span data-ttu-id="f9bd8-178">Gremlin의 `drop` 단계를 사용하여 가장자리와 꼭짓점을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-178">You can drop edges and vertices using Gremlin's `drop` step.</span></span> <span data-ttu-id="f9bd8-179">다음은 조각 보여 주는 방법을 toodelete 꼭 짓 점 및 가장자리입니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-179">Here's a snippet that shows how toodelete a vertex and an edge.</span></span> <span data-ttu-id="f9bd8-180">참고의 hello 모두 삭제를 수행 하는 꼭 짓 점 삭제 가장자리에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-180">Note that dropping a vertex performs a cascading delete of hello associated edges.</span></span>

```cs
// Drop an edge
client.CreateGremlinQuery(graphCollection, "g.E('thomasKnowsRobin').drop()");

// Drop a vertex
client.CreateGremlinQuery(graphCollection, "g.V('robin').drop()");
```

## <a name="query-hello-graph"></a><span data-ttu-id="f9bd8-181">쿼리 hello 그래프</span><span class="sxs-lookup"><span data-stu-id="f9bd8-181">Query hello graph</span></span>

<span data-ttu-id="f9bd8-182">Gremlin을 사용하여 쿼리와 순회도 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-182">You can perform queries and traversals also using Gremlin.</span></span> <span data-ttu-id="f9bd8-183">예를 들어 다음 코드 조각 hello toocount hello 그래프에 꼭 짓 점 수가 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-183">For example, hello following snippet shows how toocount hello number of vertices in hello graph:</span></span>

```cs
// Run a query toocount vertices
IDocumentQuery<int> countQuery = client.CreateGremlinQuery<int>(graphCollection, "g.V().count()");
```
<span data-ttu-id="f9bd8-184">Gremlin의를 사용 하 여 필터를 수행할 수 있습니다 `has` 및 `hasLabel` 둘을 결합 하 여 단계를 사용 하 여 `and`, `or`, 및 `not` toobuild 보다 복잡 한 필터:</span><span class="sxs-lookup"><span data-stu-id="f9bd8-184">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` toobuild more complex filters:</span></span>

```cs
// Run a query with filter
IDocumentQuery<Vertex> personsByAge = client.CreateGremlinQuery<Vertex>(
  graphCollection, 
  "g.V().hasLabel('person').has('age', gt(40))");
```

<span data-ttu-id="f9bd8-185">Hello를 사용 하 여 hello 쿼리 결과에서 특정 속성을 프로젝션 할 수 `values` 단계:</span><span class="sxs-lookup"><span data-stu-id="f9bd8-185">You can project certain properties in hello query results using hello `values` step:</span></span>

```cs
// Run a query with projection
IDocumentQuery<string> firstNames = client.CreateGremlinQuery<string>(
  graphCollection, 
  $"g.V().hasLabel('person').values('firstName')");
```

<span data-ttu-id="f9bd8-186">지금까지 모든 데이터베이스에서 작동하는 쿼리 연산자만 보았습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-186">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="f9bd8-187">Toonavigate toorelated 가장자리과 꼭지점 필요한 경우 그래프를 신속 하 고 통과 작업에 대 한 효율적인 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-187">Graphs are fast and efficient for traversal operations when you need toonavigate toorelated edges and vertices.</span></span> <span data-ttu-id="f9bd8-188">Thomas의 친구들을 모두 찾아 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-188">Let's find all friends of Thomas.</span></span> <span data-ttu-id="f9bd8-189">Gremlin의를 사용 하 여 수행 `outE` Thomas에서 모든 hello 송신 가장자리 toofind 시작한 다음 Gremlin의를 사용 하 여 해당 가장자리부터 꼭지점에 toohello 통과 `inV` 단계:</span><span class="sxs-lookup"><span data-stu-id="f9bd8-189">We do this by using Gremlin's `outE` step toofind all hello out-edges from Thomas, then traversing toohello in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
// Run a traversal (find friends of Thomas)
IDocumentQuery<Vertex> friendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="f9bd8-190">hello 다음 쿼리는 두 가지 홉 toofind 수행 Thomas' "친구의 친구"를 호출 하 여 모든 `outE` 및 `inV` 두 배입니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-190">hello next query performs two hops toofind all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
// Run a traversal (find friends of friends of Thomas)
IDocumentQuery<Vertex> friendsOfFriendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="f9bd8-191">더 복잡 한 쿼리를 작성 하 고 Gremlin를 비롯 한 혼합 필터를 사용 하 여 반복을 수행 하는 식, hello를 사용 하 여 강력한 그래프 순회 논리 구현 `loop` 단계 및 hello를 사용 하 여 구현 조건부 탐색 `choose` 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-191">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using hello `loop` step, and implementing conditional navigation using hello `choose` step.</span></span> <span data-ttu-id="f9bd8-192">[Gremlin 지원](gremlin-support.md)에서 수행할 수 있는 작업에 대해 자세히 알아보세요!</span><span class="sxs-lookup"><span data-stu-id="f9bd8-192">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

<span data-ttu-id="f9bd8-193">이것으로 끝이며, 이 Azure Cosmos DB 자습서를 완료했습니다!</span><span class="sxs-lookup"><span data-stu-id="f9bd8-193">That's it, this Azure Cosmos DB tutorial is complete!</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="f9bd8-194">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="f9bd8-194">Clean up resources</span></span>

<span data-ttu-id="f9bd8-195">것 toocontinue toouse이이 앱을 하는 경우 단계 toodelete hello Azure 포털에서에서이 자습서에서 만든 모든 리소스를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-195">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span>  

1. <span data-ttu-id="f9bd8-196">Hello Azure 포털에서에서 왼쪽 메뉴 hello에서에서 클릭 **리소스 그룹** 만든 hello 리소스의 hello 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-196">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="f9bd8-197">리소스 그룹 페이지에서 클릭 **삭제**hello 텍스트 상자에 hello 리소스 toodelete의 hello 이름을 입력 한 다음 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-197">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9bd8-198">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f9bd8-198">Next Steps</span></span>

<span data-ttu-id="f9bd8-199">이 자습서에서는 hello 다음 작업을 수행 하면:</span><span class="sxs-lookup"><span data-stu-id="f9bd8-199">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f9bd8-200">Azure Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="f9bd8-200">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="f9bd8-201">그래프 데이터베이스 및 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="f9bd8-201">Created a graph database and container</span></span>
> * <span data-ttu-id="f9bd8-202">직렬화 된 꼭 짓 점 및 가장자리 too.NET 개체</span><span class="sxs-lookup"><span data-stu-id="f9bd8-202">Serialized vertices and edges too.NET objects</span></span>
> * <span data-ttu-id="f9bd8-203">꼭짓점 및 가장자리 추가</span><span class="sxs-lookup"><span data-stu-id="f9bd8-203">Added vertices and edges</span></span>
> * <span data-ttu-id="f9bd8-204">Gremlin를 사용 하 여 쿼리 된 hello 그래프</span><span class="sxs-lookup"><span data-stu-id="f9bd8-204">Queried hello graph using Gremlin</span></span>

<span data-ttu-id="f9bd8-205">이제 Gremlin을 사용하여 더 복잡한 쿼리를 작성하고 강력한 그래프 순회 논리를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bd8-205">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="f9bd8-206">Gremlin을 사용하여 쿼리</span><span class="sxs-lookup"><span data-stu-id="f9bd8-206">Query using Gremlin</span></span>](tutorial-query-graph.md)
