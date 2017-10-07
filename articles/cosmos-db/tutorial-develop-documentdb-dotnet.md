---
title: "Azure Cosmos DB: hello.net에서 DocumentDB API로 개발 | Microsoft Docs"
description: "자세한 방법을 toodevelop.NET을 사용 하 여 Azure Cosmos DB DocumentDB api"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: 0d3d17afa782054c8fdf3cbac421e5a5d0a6800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmosdb-develop-with-hello-documentdb-api-in-net"></a><span data-ttu-id="4fe97-103">Azure CosmosDB: hello.net에서 DocumentDB API를 사용 하 여 개발</span><span class="sxs-lookup"><span data-stu-id="4fe97-103">Azure CosmosDB: Develop with hello DocumentDB API in .NET</span></span>

<span data-ttu-id="4fe97-104">Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="4fe97-105">신속 하 게 만들기 및 문서, 키/값 및 hello 글로벌 배포 및 수평 확장이 기능 Cosmos DB Azure의 hello 핵심에에서 활용 중 일부는 그래프 데이터베이스를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="4fe97-106">이 자습서는 방법을 보여 주는 사용 하 여 Azure Cosmos DB 계정을 toocreate hello Azure 포털에서 다음 문서 데이터베이스 및 컬렉션을 만듭니다는 [파티션 키](documentdb-partition-data.md#partition-keys) hello를 사용 하 여 [DocumentDB.NET API](documentdb-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-106">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal, and then create a document database and collection with a [partition key](documentdb-partition-data.md#partition-keys) using hello [DocumentDB .NET API](documentdb-introduction.md).</span></span> <span data-ttu-id="4fe97-107">컬렉션을 만들 때 파티션 키를 정의 하 여 응용 프로그램은 준비 tooscale 손쉽게 데이터 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-107">By defining a partition key when you create a collection, your application is prepared tooscale effortlessly as your data grows.</span></span> 

<span data-ttu-id="4fe97-108">이 자습서에서는 hello 다음 hello를 사용 하 여 작업 [DocumentDB.NET API](documentdb-sdk-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="4fe97-108">This tutorial covers hello following tasks by using hello [DocumentDB .NET API](documentdb-sdk-dotnet.md):</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4fe97-109">Azure Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="4fe97-109">Create an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="4fe97-110">파티션 키가 있는 데이터베이스 및 컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="4fe97-110">Create a database and collection with a partition key</span></span>
> * <span data-ttu-id="4fe97-111">JSON 문서 만들기</span><span class="sxs-lookup"><span data-stu-id="4fe97-111">Create JSON documents</span></span>
> * <span data-ttu-id="4fe97-112">문서 업데이트</span><span class="sxs-lookup"><span data-stu-id="4fe97-112">Update a document</span></span>
> * <span data-ttu-id="4fe97-113">분할된 컬렉션 쿼리</span><span class="sxs-lookup"><span data-stu-id="4fe97-113">Query partitioned collections</span></span>
> * <span data-ttu-id="4fe97-114">저장 프로시저 실행</span><span class="sxs-lookup"><span data-stu-id="4fe97-114">Run stored procedures</span></span>
> * <span data-ttu-id="4fe97-115">문서 삭제</span><span class="sxs-lookup"><span data-stu-id="4fe97-115">Delete a document</span></span>
> * <span data-ttu-id="4fe97-116">데이터베이스 삭제</span><span class="sxs-lookup"><span data-stu-id="4fe97-116">Delete a database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4fe97-117">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4fe97-117">Prerequisites</span></span>
<span data-ttu-id="4fe97-118">Hello 다음 항목이 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4fe97-118">Please make sure you have hello following:</span></span>

* <span data-ttu-id="4fe97-119">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="4fe97-119">An active Azure account.</span></span> <span data-ttu-id="4fe97-120">계정이 없는 경우 [무료 계정](https://azure.microsoft.com/free/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-120">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="4fe97-121">Hello 또는 사용할 수 있습니다 [Azure Cosmos DB 에뮬레이터](local-emulator.md) toouse hello Azure DocumentDB 서비스를 개발 목적으로 에뮬레이트하는 로컬 환경을 원하는 경우이 자습서에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-121">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial if you'd like toouse a local environment that emulates hello Azure DocumentDB service for development purposes.</span></span>
* <span data-ttu-id="4fe97-122">[Visual Studio](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="4fe97-122">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="4fe97-123">Azure Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="4fe97-123">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="4fe97-124">Hello Azure 포털에서에서 Azure Cosmos DB 계정을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-124">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>

> [!TIP]
> * <span data-ttu-id="4fe97-125">Azure Cosmos DB 계정이 이미 있나요?</span><span class="sxs-lookup"><span data-stu-id="4fe97-125">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="4fe97-126">이 경우 건너뛰고 너무[Visual Studio 솔루션 설정](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="4fe97-126">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="4fe97-127">Azure DocumentDB 계정이 있나요?</span><span class="sxs-lookup"><span data-stu-id="4fe97-127">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="4fe97-128">따라서 사용자 계정이 Azure Cosmos DB 계정인 이제 하 고 건너뛰어도 너무[Visual Studio 솔루션 설정](#SetupVS)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-128">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="4fe97-129">Hello Azure Cosmos DB 에뮬레이터를 사용 하는 경우 hello 단계에 따르십시오 [Azure Cosmos DB 에뮬레이터](local-emulator.md) toosetup 에뮬레이터 hello 및 너무 건너 뛸[Visual Studio 솔루션 설정](#SetupVS)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-129">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="4fe97-130"><a id="SetupVS"></a>Visual Studio 솔루션 설치</span><span class="sxs-lookup"><span data-stu-id="4fe97-130"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="4fe97-131">컴퓨터에서 **Visual Studio**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-131">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="4fe97-132">Hello에 **파일** 메뉴 선택 **새로**를 선택한 후 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-132">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="4fe97-133">Hello에 **새 프로젝트** 대화 상자에서 **템플릿** / **Visual C#** / **콘솔 응용 프로그램 (.NET Framework)**프로젝트 이름을 지정 하 고 클릭 한 다음, **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-133">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="4fe97-134">![새 프로젝트 창 hello 스크린 샷](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="4fe97-134">![Screen shot of hello New Project window](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span></span>

4. <span data-ttu-id="4fe97-135">Hello에 **솔루션 탐색기**을 Visual Studio 솔루션에서 사용 중인 새 콘솔 응용 프로그램을 마우스 오른쪽 단추로 클릭 하 고 클릭 **NuGet 패키지 관리...**</span><span class="sxs-lookup"><span data-stu-id="4fe97-135">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Hello 오른쪽 hello 프로젝트에 대 한 Clicked 메뉴를 스크린샷](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="4fe97-137">Hello에 **NuGet** 탭을 클릭 **찾아보기**, 유형과 **documentdb** hello 검색 상자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-137">In hello **NuGet** tab, click **Browse**, and type **documentdb** in hello search box.</span></span>
<!---stopped here--->
6. <span data-ttu-id="4fe97-138">Hello 결과 내 찾을 **Microsoft.Azure.DocumentDB** 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-138">Within hello results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="4fe97-139">hello Azure Cosmos DB 클라이언트 라이브러리에 대 한 hello 패키지 ID가 [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-139">hello package ID for hello Azure Cosmos DB Client Library is [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span></span>
   <span data-ttu-id="4fe97-140">![Azure Cosmos DB 클라이언트 SDK를 찾기 위한 hello NuGet 메뉴의 스크린 샷](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="4fe97-140">![Screen shot of hello NuGet Menu for finding Azure Cosmos DB Client SDK](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="4fe97-141">클릭 하 여 변경 내용을 toohello 솔루션을 검토 하는 방법에 대 한 메시지를 가져오면 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-141">If you get a message about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="4fe97-142">라이선스 승인에 관한 메시지가 표시되면 **동의합니다.**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-142">If you get a message about license acceptance, click **I accept**.</span></span>

## <span data-ttu-id="4fe97-143"><a id="Connect"></a>참조 tooyour 프로젝트 추가</span><span class="sxs-lookup"><span data-stu-id="4fe97-143"><a id="Connect"></a>Add references tooyour project</span></span>
<span data-ttu-id="4fe97-144">이 자습서를 제공 hello DocumentDB API 코드 조각 필요한 toocreate 및 update Azure Cosmos DB 프로젝트의 리소스에서 남은 hello 단계 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-144">hello remaining steps in this tutorial provide hello DocumentDB API code snippets required toocreate and update Azure Cosmos DB resources in your project.</span></span>

<span data-ttu-id="4fe97-145">첫째, 이러한 참조 tooyour 응용 프로그램을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-145">First, add these references tooyour application.</span></span>
<!---These aren't added by default when you install hello pkg?--->

```csharp
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

## <span data-ttu-id="4fe97-146"><a id="add-references"></a>앱 연결</span><span class="sxs-lookup"><span data-stu-id="4fe97-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="4fe97-147">다음으로 응용 프로그램에 이 두 상수와 *client* 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-147">Next, add these two constants and your *client* variable in your application.</span></span>

```csharp
private const string EndpointUrl = "<your endpoint URL>";
private const string PrimaryKey = "<your primary key>";
private DocumentClient client;
```

<span data-ttu-id="4fe97-148">다음, h e a d 다시 toohello [Azure 포털](https://portal.azure.com) tooretrieve 끝점 URL 및 기본 키입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-148">Then, head back toohello [Azure portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="4fe97-149">hello 끝점 URL 및 기본 키가 응용 프로그램 toounderstand에 필요한 위치 tooconnect 되며, Azure Cosmos DB tootrust에 대 한 응용 프로그램의 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-149">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="4fe97-150">에 Azure 포털 hello, tooyour Azure Cosmos DB 계정 탐색, 클릭 **키**, 클릭 하 고 **읽기-쓰기 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-150">In hello Azure portal, navigate tooyour Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span>

<span data-ttu-id="4fe97-151">Hello 포털에서 hello URI를 복사 하 고 붙여넣어 `<your endpoint URL>` hello program.cs 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-151">Copy hello URI from hello portal and paste it over `<your endpoint URL>` in hello program.cs file.</span></span> <span data-ttu-id="4fe97-152">복사 hello 포털에서 기본 키를 hello 고 하 고 붙여넣어 `<your primary key>`합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-152">Then copy hello PRIMARY KEY from hello portal and paste it over `<your primary key>`.</span></span> <span data-ttu-id="4fe97-153">수 있는지 tooremove hello `<` 및 `>` 값에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-153">Be sure tooremove hello `<` and `>` from your values.</span></span>

![C# 콘솔 응용 프로그램 hello NoSQL 자습서 toocreate hello Azure 포털의 스크린 샷을 사용합니다.](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-keys.png)

## <span data-ttu-id="4fe97-156"><a id="instantiate"></a>Hello DocumentClient 인스턴스화합니다</span><span class="sxs-lookup"><span data-stu-id="4fe97-156"><a id="instantiate"></a>Instantiate hello DocumentClient</span></span>

<span data-ttu-id="4fe97-157">이제 hello의 새 인스턴스를 만들 **DocumentClient**합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-157">Now, create a new instance of hello **DocumentClient**.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
```

## <span data-ttu-id="4fe97-158"><a id="create-database"></a>데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="4fe97-158"><a id="create-database"></a>Create a database</span></span>

<span data-ttu-id="4fe97-159">다음으로 Azure Cosmos DB 만듭니다 [데이터베이스](documentdb-resources.md#databases) hello를 사용 하 여 [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) 메서드 또는 [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) hello 방식의  **DocumentClient** hello에서 클래스 [DocumentDB.NET SDK](documentdb-sdk-dotnet.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-159">Next, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class from hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="4fe97-160">데이터베이스는 컬렉션에 분할 된 JSON 문서 저장소의 hello 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-160">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

```csharp
await client.CreateDatabaseAsync(new Database { Id = "db" });
```
## <a name="decide-on-a-partition-key"></a><span data-ttu-id="4fe97-161">파티션 키 결정</span><span class="sxs-lookup"><span data-stu-id="4fe97-161">Decide on a partition key</span></span> 

<span data-ttu-id="4fe97-162">컬렉션은 문서를 저장하기 위한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-162">Collections are containers for storing documents.</span></span> <span data-ttu-id="4fe97-163">논리적인 리소스이며 [하나 이상의 물리적 파티션](partition-data.md)에 걸쳐 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-163">They are logical resources and can [span one or more physical partitions](partition-data.md).</span></span> <span data-ttu-id="4fe97-164">A [파티션 키](documentdb-partition-data.md) 내인지 속성 (또는 경로) 프로그램은 문서에 사용 되는 toodistribute hello 서버 또는 파티션 간에 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-164">A [partition key](documentdb-partition-data.md) is a property (or path) within your documents that is used toodistribute your data among hello servers or partitions.</span></span> <span data-ttu-id="4fe97-165">Hello 동일한 파티션 키에 저장 되어 있는 모든 문서를 동일한 파티션에 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-165">All documents with hello same partition key are stored in hello same partition.</span></span> 

<span data-ttu-id="4fe97-166">컬렉션을 만들기 전에 중요 한 결정 사항 toomake를는 파티션 키를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-166">Determining a partition key is an important decision toomake before you create a collection.</span></span> <span data-ttu-id="4fe97-167">파티션 키는 속성 (또는 경로) 될 수 있는 문서 내에서 여러 서버 또는 파티션 간에 데이터를 Azure Cosmos DB toodistribute에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-167">Partition keys are a property (or path) within your documents that can be used by Azure Cosmos DB toodistribute your data among multiple servers or partitions.</span></span> <span data-ttu-id="4fe97-168">Cosmos DB hello 파티션 키 값을 해시 하 고 toostore hello 문서에 해시 된 hello 결과 toodetermine hello 파티션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-168">Cosmos DB hashes hello partition key value and uses hello hashed result toodetermine hello partition in which toostore hello document.</span></span> <span data-ttu-id="4fe97-169">Hello 동일한 파티션 키에 저장 되어 있는 모든 문서를 동일한 파티션에 hello 및는 컬렉션을 만든 후에 파티션 키를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-169">All documents with hello same partition key are stored in hello same partition, and partition keys cannot be changed once a collection is created.</span></span> 

<span data-ttu-id="4fe97-170">이 자습서에서는 여기 tooset hello 파티션 키 너무`/deviceId` 단일 장치 단일 파티션에 저장에 대 한 모든 hello 데이터 hello 하는 하므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-170">For this tutorial, we're going tooset hello partition key too`/deviceId` so that hello all hello data for a single device is stored in a single partition.</span></span> <span data-ttu-id="4fe97-171">많은 수의 값을 각각 사용 되는 파티션 키 toochoose 원하는에 hello에 대 한 동일한 주파수 tooensure Cosmos DB 부하를 분산할 수 데이터 증가 하 고 hello hello 컬렉션의 전체 처리량을 달성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-171">You want toochoose a partition key that has a large number of values, each of which are used at about hello same frequency tooensure Cosmos DB can load balance as your data grows and achieve hello full throughput of hello collection.</span></span> 

<span data-ttu-id="4fe97-172">분할에 대 한 자세한 내용은 참조 [어떻게 toopartition 및 Azure Cosmos DB에서 소수?](partition-data.md)</span><span class="sxs-lookup"><span data-stu-id="4fe97-172">For more information about partitioning, see [How toopartition and scale in Azure Cosmos DB?](partition-data.md)</span></span> 

## <span data-ttu-id="4fe97-173"><a id="CreateColl"></a>컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="4fe97-173"><a id="CreateColl"></a>Create a collection</span></span> 

<span data-ttu-id="4fe97-174">이 파티션 키를 알았으므로 `/deviceId`를 만들 수 있습니다. 한 [컬렉션](documentdb-resources.md#collections) hello를 사용 하 여 [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) 메서드 또는 [ CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) hello 방식의 **DocumentClient** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-174">Now that we know our partition key, `/deviceId`, lets create a [collection](documentdb-resources.md#collections) by using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="4fe97-175">컬렉션은 JSON 문서 및 관련된 모든 JavaScript 응용 프로그램 논리의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-175">A collection is a container of JSON documents and any associated JavaScript application logic.</span></span> 

> [!WARNING]
> <span data-ttu-id="4fe97-176">컬렉션을 만드는 영향을 줍니다 가격의 Azure Cosmos DB와 함께 응용 프로그램 toocommunicate hello에 대 한 처리량을 예약 하는.</span><span class="sxs-lookup"><span data-stu-id="4fe97-176">Creating a collection has pricing implications, as you are reserving throughput for hello application toocommunicate with Azure Cosmos DB.</span></span> <span data-ttu-id="4fe97-177">자세한 내용은 [가격 페이지](https://azure.microsoft.com/pricing/details/cosmos-db/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4fe97-177">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

```csharp
// Collection for device telemetry. Here hello JSON property deviceId is used  
// as hello partition key toospread across partitions. Configured for 2500 RU/s  
// throughput and an indexing policy that supports sorting against any  
// number or string property. .
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 2500 });
```

<span data-ttu-id="4fe97-178">이 메서드는 REST API tooAzure Cosmos DB 호출 및 hello 서비스 제공 hello 요청된 처리량에 기반 하는 파티션의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-178">This method makes a REST API call tooAzure Cosmos DB, and hello service provisions a number of partitions based on hello requested throughput.</span></span> <span data-ttu-id="4fe97-179">성능을 요구 사항이 발전 hello SDK 또는 hello를 사용 하 여 컬렉션의 hello 처리량을 변경할 수 있습니다 [Azure 포털](set-throughput.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-179">You can change hello throughput of a collection as your performance needs evolve using hello SDK or hello [Azure portal](set-throughput.md).</span></span>

## <span data-ttu-id="4fe97-180"><a id="CreateDoc"></a>JSON 문서 만들기</span><span class="sxs-lookup"><span data-stu-id="4fe97-180"><a id="CreateDoc"></a>Create JSON documents</span></span>
<span data-ttu-id="4fe97-181">Azure Cosmos DB에 일부 JSON 문서를 삽입해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-181">Let's insert some JSON documents into Azure Cosmos DB.</span></span> <span data-ttu-id="4fe97-182">A [문서](documentdb-resources.md#documents) hello를 사용 하 여 만들 수 [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) hello 방식의 **DocumentClient** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-182">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="4fe97-183">문서는 사용자 정의(임의) JSON 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-183">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="4fe97-184">이 샘플 클래스 컬렉션으로 읽어 새 장치는 장치 읽기 및 호출 tooCreateDocumentAsync tooinsert 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-184">This sample class contains a device reading, and a call tooCreateDocumentAsync tooinsert a new device reading into a collection.</span></span>

```csharp
public class DeviceReading
{
    [JsonProperty("id")]
    public string Id;

    [JsonProperty("deviceId")]
    public string DeviceId;

    [JsonConverter(typeof(IsoDateTimeConverter))]
    [JsonProperty("readingTime")]
    public DateTime ReadingTime;

    [JsonProperty("metricType")]
    public string MetricType;

    [JsonProperty("unit")]
    public string Unit;

    [JsonProperty("metricValue")]
    public double MetricValue;
  }

// Create a document. Here hello partition key is extracted 
// as "XMS-0001" based on hello collection definition
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "coll"),
    new DeviceReading
    {
        Id = "XMS-001-FE24C",
        DeviceId = "XMS-0001",
        MetricType = "Temperature",
        MetricValue = 105.00,
        Unit = "Fahrenheit",
        ReadingTime = DateTime.UtcNow
    });
```
## <a name="read-data"></a><span data-ttu-id="4fe97-185">데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="4fe97-185">Read data</span></span>

<span data-ttu-id="4fe97-186">파티션 키 및 hello ReadDocumentAsync 메서드를 사용 하 여 Id 사용 하 여 hello 문서를 읽을 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-186">Let's read hello document by its partition key and Id using hello ReadDocumentAsync method.</span></span> <span data-ttu-id="4fe97-187">Hello 읽기 PartitionKey 값에 포함 (해당 toohello `x-ms-documentdb-partitionkey` hello REST API에서에서 요청 헤더).</span><span class="sxs-lookup"><span data-stu-id="4fe97-187">Note that hello reads include a PartitionKey value (corresponding toohello `x-ms-documentdb-partitionkey` request header in hello REST API).</span></span>

```csharp
// Read document. Needs hello partition key and hello Id toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;
```

## <a name="update-data"></a><span data-ttu-id="4fe97-188">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="4fe97-188">Update data</span></span>

<span data-ttu-id="4fe97-189">이제 hello ReplaceDocumentAsync 메서드를 사용 하 여 일부 데이터를 업데이트 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-189">Now let's update some data using hello ReplaceDocumentAsync method.</span></span>

```csharp
// Update hello document. Partition key is not required, again extracted from hello document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);
```

## <a name="delete-data"></a><span data-ttu-id="4fe97-190">데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="4fe97-190">Delete data</span></span>

<span data-ttu-id="4fe97-191">이제 hello DeleteDocumentAsync 메서드를 사용 하 여 파티션 키로 문서 및 id를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-191">Now lets delete a document by partition key and id by using hello DeleteDocumentAsync method.</span></span>

```csharp
// Delete a document. hello partition key is required.
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```
## <a name="query-partitioned-collections"></a><span data-ttu-id="4fe97-192">분할된 컬렉션 쿼리</span><span class="sxs-lookup"><span data-stu-id="4fe97-192">Query partitioned collections</span></span>

<span data-ttu-id="4fe97-193">Azure Cosmos DB 분할 된 컬렉션에서 데이터를 자동으로 쿼리할 때 경로 (있는 경우) hello 필터에 지정 된 toohello 파티션 키 값에 해당 하는 쿼리 toohello 파티션이 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-193">When you query data in partitioned collections, Azure Cosmos DB automatically routes hello query toohello partitions corresponding toohello partition key values specified in hello filter (if there are any).</span></span> <span data-ttu-id="4fe97-194">예를 들어이 쿼리는 라우트된 toojust hello 파티션 포함 hello 파티션 키 "x m S-0001"입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-194">For example, this query is routed toojust hello partition containing hello partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="4fe97-195">hello 다음 쿼리는 필터 hello 파티션 키 (DeviceId)에 없으며 hello 파티션 인덱스에 대해 실행 되는 tooall 파티션 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-195">hello following query does not have a filter on hello partition key (DeviceId) and is fanned out tooall partitions where it is executed against hello partition's index.</span></span> <span data-ttu-id="4fe97-196">Toospecify hello EnableCrossPartitionQuery가 (`x-ms-documentdb-query-enablecrosspartition` hello REST API에에서) toohave hello SDK tooexecute 파티션에서 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-196">Note that you have toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in hello REST API) toohave hello SDK tooexecute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

## <a name="parallel-query-execution"></a><span data-ttu-id="4fe97-197">병렬 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="4fe97-197">Parallel query execution</span></span>
<span data-ttu-id="4fe97-198">hello Azure Cosmos DB DocumentDB Sdk 1.9.0 지원 위에 tooperform 짧은 대기 시간 수 있게 하는 병렬 쿼리 실행 옵션에 대해 쿼리를 분할 된 컬렉션 tootouch 필요한 경우에 많은 수의 파티션 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-198">hello Azure Cosmos DB DocumentDB SDKs 1.9.0 and above support parallel query execution options, which allow you tooperform low latency queries against partitioned collections, even when they need tootouch a large number of partitions.</span></span> <span data-ttu-id="4fe97-199">예를 들어 다음 쿼리는 hello 여러 파티션에 병렬로 구성된 toorun입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-199">For example, hello following query is configured toorun in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="4fe97-200">Hello 매개 변수 뒤를 튜닝 하 여 병렬 쿼리 실행을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-200">You can manage parallel query execution by tuning hello following parameters:</span></span>

* <span data-ttu-id="4fe97-201">설정 하 여 `MaxDegreeOfParallelism`를 병렬 처리 수준, 즉 hello 최대 동시 네트워크 연결 toohello 컬렉션 파티션 수 정도 hello 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-201">By setting `MaxDegreeOfParallelism`, you can control hello degree of parallelism i.e., hello maximum number of simultaneous network connections toohello collection's partitions.</span></span> <span data-ttu-id="4fe97-202">로 설정 하면이-1 너무 hello 병렬 처리 수준은 hello SDK에서 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-202">If you set this too-1, hello degree of parallelism is managed by hello SDK.</span></span> <span data-ttu-id="4fe97-203">경우 hello `MaxDegreeOfParallelism` 지정 하지 않거나 too0는 hello 기본값을 설정 하지는 단일 네트워크 연결 toohello 컬렉션의 파티션이 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-203">If hello `MaxDegreeOfParallelism` is not specified or set too0, which is hello default value, there will be a single network connection toohello collection's partitions.</span></span>
* <span data-ttu-id="4fe97-204">`MaxBufferedItemCount`를 설정하여 쿼리 대기 시간과 클라이언트 쪽 메모리 사용률 간에 균형을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-204">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="4fe97-205">이 매개 변수를 생략 하거나이-1 너무 설정 hello SDK hello 개수의 병렬 쿼리 실행 중에 버퍼링 하는 항목을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-205">If you omit this parameter or set this too-1, hello number of items buffered during parallel query execution is managed by hello SDK.</span></span>

<span data-ttu-id="4fe97-206">Hello 제공 hello 컬렉션의 동일한 상태 병렬 쿼리의 직렬 실행에서와 같이 주문 동일 hello에 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-206">Given hello same state of hello collection, a parallel query will return results in hello same order as in serial execution.</span></span> <span data-ttu-id="4fe97-207">정렬 (ORDER BY 및 TOP)을 포함 하는 분할 간 쿼리를 수행할 때는 hello DocumentDB SDK는 여러 파티션에 병렬로 hello 쿼리를 발급 하 고 hello 클라이언트 쪽 tooproduce 전체적으로 순서가 지정 된 결과에서 부분적으로 저장 된 결과 병합 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-207">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), hello DocumentDB SDK issues hello query in parallel across partitions and merges partially sorted results in hello client side tooproduce globally ordered results.</span></span>

## <a name="execute-stored-procedures"></a><span data-ttu-id="4fe97-208">저장 프로시저 실행</span><span class="sxs-lookup"><span data-stu-id="4fe97-208">Execute stored procedures</span></span>
<span data-ttu-id="4fe97-209">원자성 트랜잭션을 사용 하 여 문서에 대해 실행할 수 있습니다는 마지막으로, 동일한 장치 ID, 예를 들어 hello 집계를 관리 하 고 또는 hello tooyour 프로젝트 코드를 다음을 추가 하 여 단일 문서에서 장치의 최신 상태를 환영 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="4fe97-209">Lastly, you can execute atomic transactions against documents with hello same device ID, e.g. if you're maintaining aggregates or hello latest state of a device in a single document by adding hello following code tooyour project.</span></span>

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```

<span data-ttu-id="4fe97-210">이것으로 끝입니다!</span><span class="sxs-lookup"><span data-stu-id="4fe97-210">And that's it!</span></span> <span data-ttu-id="4fe97-211">hello 파티션에서 파티션 키 tooefficiently 배율 데이터 분포를 사용 하는 Azure Cosmos DB 응용 프로그램의 주요 구성 요소 모두입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-211">those are hello main components of an Azure Cosmos DB application that uses a partition key tooefficiently scale data distribution across partitions.</span></span>  

## <a name="clean-up-resources"></a><span data-ttu-id="4fe97-212">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="4fe97-212">Clean up resources</span></span>

<span data-ttu-id="4fe97-213">것 toocontinue toouse이 응용이 프로그램, 경우에이 자습서에서 만든 hello Azure 포털 단계를 수행 하는 hello로 리소스를 모두 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-213">If you're not going toocontinue toouse this app, delete all resources created by this tutorial in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="4fe97-214">Hello Azure 포털에서에서 왼쪽 메뉴 hello에서에서 클릭 **리소스 그룹** hello 만든 hello 리소스의 고유 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-214">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello unique name of hello resource you created.</span></span> 
2. <span data-ttu-id="4fe97-215">리소스 그룹 페이지에서 클릭 **삭제**hello 텍스트 상자에 hello 리소스 toodelete의 hello 이름을 입력 한 다음 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-215">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fe97-216">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4fe97-216">Next steps</span></span>

<span data-ttu-id="4fe97-217">이 자습서에서는 hello 다음 작업을 수행 하면:</span><span class="sxs-lookup"><span data-stu-id="4fe97-217">In this tutorial, you've done hello following:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="4fe97-218">Azure Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="4fe97-218">Created an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="4fe97-219">파티션 키가 있는 데이터베이스 및 컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="4fe97-219">Created a database and collection with a partition key</span></span>
> * <span data-ttu-id="4fe97-220">JSON 문서 만들기</span><span class="sxs-lookup"><span data-stu-id="4fe97-220">Created JSON documents</span></span>
> * <span data-ttu-id="4fe97-221">문서 업데이트</span><span class="sxs-lookup"><span data-stu-id="4fe97-221">Updated a document</span></span>
> * <span data-ttu-id="4fe97-222">분할된 컬렉션 쿼리</span><span class="sxs-lookup"><span data-stu-id="4fe97-222">Queried partitioned collections</span></span>
> * <span data-ttu-id="4fe97-223">저장 프로시저 실행</span><span class="sxs-lookup"><span data-stu-id="4fe97-223">Ran a stored procedure</span></span>
> * <span data-ttu-id="4fe97-224">문서 삭제</span><span class="sxs-lookup"><span data-stu-id="4fe97-224">Deleted a document</span></span>
> * <span data-ttu-id="4fe97-225">데이터베이스 삭제</span><span class="sxs-lookup"><span data-stu-id="4fe97-225">Deleted a database</span></span>

<span data-ttu-id="4fe97-226">이제 toohello 다음 자습서를 진행 한 tooyour Cosmos DB 계정 추가 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe97-226">You can now proceed toohello next tutorial and import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="4fe97-227">Azure Cosmos DB로 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="4fe97-227">Import data into Azure Cosmos DB</span></span>](import-data.md)
