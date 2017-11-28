---
title: "Azure Cosmos DB: hello.net에서 테이블 API로 개발 | Microsoft Docs"
description: "자세한 방법을 toodevelop.NET을 사용 하 여 Azure Cosmos DB 테이블 api"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 4b22cb49-8ea2-483d-bc95-1172cd009498
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: mvc
ms.openlocfilehash: 70c6985a1dffdbcdb07e377f8ad10355bb97712a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-table-api-in-net"></a><span data-ttu-id="1e476-103">Azure Cosmos DB: hello.net에서 테이블 API를 사용 하 여 개발</span><span class="sxs-lookup"><span data-stu-id="1e476-103">Azure Cosmos DB: Develop with hello Table API in .NET</span></span>

<span data-ttu-id="1e476-104">Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="1e476-105">신속 하 게 만들기 및 문서, 키/값 및 hello 글로벌 배포 및 수평 확장이 기능 Cosmos DB Azure의 hello 핵심에에서 활용 중 일부는 그래프 데이터베이스를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span>

<span data-ttu-id="1e476-106">이 자습서에서는 hello 다음 작업 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-106">This tutorial covers hello following tasks:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="1e476-107">Azure Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="1e476-107">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="1e476-108">Hello app.config 파일에서 기능을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="1e476-108">Enable functionality in hello app.config file</span></span> 
> * <span data-ttu-id="1e476-109">Hello를 사용 하 여 테이블을 만들 [테이블 API](table-introduction.md) (미리 보기)</span><span class="sxs-lookup"><span data-stu-id="1e476-109">Create a table using hello [Table API](table-introduction.md) (preview)</span></span>
> * <span data-ttu-id="1e476-110">엔터티 tooa 테이블 추가</span><span class="sxs-lookup"><span data-stu-id="1e476-110">Add an entity tooa table</span></span> 
> * <span data-ttu-id="1e476-111">엔터티 일괄 삽입</span><span class="sxs-lookup"><span data-stu-id="1e476-111">Insert a batch of entities</span></span> 
> * <span data-ttu-id="1e476-112">단일 엔터티 검색</span><span class="sxs-lookup"><span data-stu-id="1e476-112">Retrieve a single entity</span></span> 
> * <span data-ttu-id="1e476-113">자동 보조 인덱스를 사용하여 엔터티 쿼리</span><span class="sxs-lookup"><span data-stu-id="1e476-113">Query entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="1e476-114">엔터티 바꾸기</span><span class="sxs-lookup"><span data-stu-id="1e476-114">Replace an entity</span></span> 
> * <span data-ttu-id="1e476-115">엔터티 삭제</span><span class="sxs-lookup"><span data-stu-id="1e476-115">Delete an entity</span></span> 
> * <span data-ttu-id="1e476-116">테이블 삭제</span><span class="sxs-lookup"><span data-stu-id="1e476-116">Delete a table</span></span>
 
## <a name="tables-in-azure-cosmos-db"></a><span data-ttu-id="1e476-117">Azure Cosmos DB의 테이블</span><span class="sxs-lookup"><span data-stu-id="1e476-117">Tables in Azure Cosmos DB</span></span> 

<span data-ttu-id="1e476-118">Azure Cosmos DB 제공 hello [테이블 API](table-introduction.md) (미리 보기) 스키마가 지정 되지 않은 디자인에 키-값 저장소를 필요로 하는 응용 프로그램에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-118">Azure Cosmos DB provides hello [Table API](table-introduction.md) (preview) for applications that need a key-value store with a schema-less design.</span></span> <span data-ttu-id="1e476-119">[Azure 테이블 저장소](../storage/common/storage-introduction.md) Sdk 및 REST Api는 Azure Cosmos DB와 함께 사용 되는 toowork 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-119">[Azure Table storage](../storage/common/storage-introduction.md) SDKs and REST APIs can be used toowork with Azure Cosmos DB.</span></span> <span data-ttu-id="1e476-120">처리량이 높은 요구 사항과 Azure Cosmos DB toocreate 테이블을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-120">You can use Azure Cosmos DB toocreate tables with high throughput requirements.</span></span> <span data-ttu-id="1e476-121">Azure Cosmos DB는 현재 공개 미리 보기에서 처리량 액세스에 최적화된 테이블(비공식적으로 "프리미엄 테이블"이라고 함)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-121">Azure Cosmos DB supports throughput-optimized tables (informally called "premium tables"), currently in public preview.</span></span> 

<span data-ttu-id="1e476-122">Toouse 높은 저장소 및 처리량 요구 사항이 낮은 테이블에 대 한 Azure 테이블 저장소를 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-122">You can continue toouse Azure Table storage for tables with high storage and lower throughput requirements.</span></span> <span data-ttu-id="1e476-123">Azure Cosmos DB 향후 업데이트에서 저장소 액세스에 최적화 된 테이블에 대 한 지원을 제공 하 고 기존 및 새 Azure 테이블 저장소 계정으로 원활 하 게 수 tooAzure Cosmos DB 업그레이드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-123">Azure Cosmos DB will introduce support for storage-optimized tables in a future update, and existing and new Azure Table storage accounts will be seamlessly upgraded tooAzure Cosmos DB.</span></span>

<span data-ttu-id="1e476-124">현재 Azure 테이블 저장소를 사용 하는 경우 이점을 hello "프리미엄 table" 미리 보기와 함께 다음 hello를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-124">If you currently use Azure Table storage, you gain hello following benefits with hello "premium table" preview:</span></span>

- <span data-ttu-id="1e476-125">멀티 호밍 및 [자동 및 수동 장애 조치](regional-failover.md)와 함께 턴키 방식으로 [전역 배포](distribute-data-globally.md)</span><span class="sxs-lookup"><span data-stu-id="1e476-125">Turn-key [global distribution](distribute-data-globally.md) with multi-homing and [automatic and manual failovers](regional-failover.md)</span></span>
- <span data-ttu-id="1e476-126">모든 속성("보조 인덱스")에 대한 스키마 독립적 자동 인덱싱 및 빠른 쿼리 지원</span><span class="sxs-lookup"><span data-stu-id="1e476-126">Support for automatic schema-agnostic indexing against all properties ("secondary indexes"), and fast queries</span></span> 
- <span data-ttu-id="1e476-127">여러 지역 간에 [독립적인 저장소 및 처리량 크기 조정](partition-data.md) 지원</span><span class="sxs-lookup"><span data-stu-id="1e476-127">Support for [independent scaling of storage and throughput](partition-data.md), across any number of regions</span></span>
- <span data-ttu-id="1e476-128">에 대 한 지원 [테이블당 전용된 처리량](request-units.md) 수백에서 확장할 수 있는 초당 요청 toomillions</span><span class="sxs-lookup"><span data-stu-id="1e476-128">Support for [dedicated throughput per table](request-units.md) that can be scaled from hundreds toomillions of requests per second</span></span>
- <span data-ttu-id="1e476-129">에 대 한 지원 [5 튜닝할 수 있는 일관성 수준](consistency-levels.md) 가용성, 대기 시간 및 일관성 오프 tootrade 응용 프로그램 요구 사항에 따라</span><span class="sxs-lookup"><span data-stu-id="1e476-129">Support for [five tunable consistency levels](consistency-levels.md) tootrade off availability, latency, and consistency based on your application needs</span></span>
- <span data-ttu-id="1e476-130">단일 지역 및 기능 tooadd를 자세한 내에서 99.99% 가용성 높은 가용성을 위한 지역 및 [업계를 주도하 포괄적인 Sla](https://azure.microsoft.com/support/legal/sla/cosmos-db/) 일반 가용성에</span><span class="sxs-lookup"><span data-stu-id="1e476-130">99.99% availability within a single region, and ability tooadd more regions for higher availability, and [industry-leading comprehensive SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db/) on general availability</span></span>
- <span data-ttu-id="1e476-131">Hello 기존 Azure 저장소.NET SDK를 사용 하 고 코드 변경 내용 tooyour 응용 프로그램이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-131">Work with hello existing Azure storage .NET SDK, and no code changes tooyour application</span></span>

<span data-ttu-id="1e476-132">Hello 미리 보기 동안 Azure Cosmos DB 지원 hello.NET SDK를 사용 하 여 테이블 API hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-132">During hello preview, Azure Cosmos DB supports hello Table API using hello .NET SDK.</span></span> <span data-ttu-id="1e476-133">Hello를 다운로드할 수 있습니다 [Azure 저장소 미리 보기 SDK](https://aka.ms/premiumtablenuget) 있는 hello NuGet에서 동일한 클래스와 메서드 시그니처에 hello로 [Azure 저장소 SDK](https://www.nuget.org/packages/WindowsAzure.Storage), 또한 hello를 사용 하 여 tooAzure Cosmos DB 계정을 연결할 수 있지만 테이블 API입니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-133">You can download hello [Azure Storage Preview SDK](https://aka.ms/premiumtablenuget) from NuGet, that has hello same classes and method signatures as hello [Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also can connect tooAzure Cosmos DB accounts using hello Table API.</span></span>

<span data-ttu-id="1e476-134">toolearn 더 복잡 한 Azure 테이블 저장소 작업에 대 한 참조.</span><span class="sxs-lookup"><span data-stu-id="1e476-134">toolearn more about complex Azure Table storage tasks, see:</span></span>

* [<span data-ttu-id="1e476-135">Cosmos DB 소개 tooAzure: 테이블 API</span><span class="sxs-lookup"><span data-stu-id="1e476-135">Introduction tooAzure Cosmos DB: Table API</span></span>](table-introduction.md)
* <span data-ttu-id="1e476-136">사용 가능한 Api에 대 한 자세한 내용은 테이블 서비스 참조 설명서 hello [.NET 참조 용 저장소 클라이언트 라이브러리](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="1e476-136">hello Table service reference documentation for complete details about available APIs [Storage Client Library for .NET reference](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="1e476-137">이 자습서 정보</span><span class="sxs-lookup"><span data-stu-id="1e476-137">About this tutorial</span></span>
<span data-ttu-id="1e476-138">이 자습서 사용 Azure Cosmos DB 개발자에 게 hello SDK, Azure 테이블 저장소에 잘 알고 있으며 toouse hello 프리미엄 기능 사용할 수 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-138">This tutorial is for developers who are familiar with hello Azure Table storage SDK, and would like toouse hello premium features available using Azure Cosmos DB.</span></span> <span data-ttu-id="1e476-139">에 기반 하는 [.NET을 사용 하 여 Azure 테이블 저장소 시작](table-storage-how-to-use-dotnet.md) 및 추가 기능을 활용 tootake 보조 인덱스, 프로 비전 된 처리량 및 멀티 호 밍 등의 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-139">It is based on [Get Started with Azure Table storage using .NET](table-storage-how-to-use-dotnet.md) and shows how tootake advantage of additional capabilities like secondary indexes, provisioned throughput, and multi-homing.</span></span> <span data-ttu-id="1e476-140">어떻게 toouse Azure 포털 toocreate Azure Cosmos DB 계정을 hello 다음 빌드 및 배포 테이블 응용 프로그램을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-140">We cover how toouse hello Azure portal toocreate an Azure Cosmos DB account, and then build and deploy a Table application.</span></span> <span data-ttu-id="1e476-141">또한 테이블을 만들고 삭제하며, 테이블 데이터를 삽입, 업데이트, 삭제 및 쿼리하기 위한 .NET 예제를 단계별로 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-141">We also walk through .NET examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span> 

<span data-ttu-id="1e476-142">설치 된 Visual Studio 2017 없는 경우 다운로드 하 고 hello를 사용 하 여 수 **무료** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-142">If you don't already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="1e476-143">사용할 수 있는지 확인 **Azure 개발** hello Visual Studio 설정 중입니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-143">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="1e476-144">데이터베이스 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="1e476-144">Create a database account</span></span>

<span data-ttu-id="1e476-145">Hello Azure 포털에서에서 Azure Cosmos DB 계정을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-145">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="1e476-146">Azure Cosmos DB 계정이 이미 있나요?</span><span class="sxs-lookup"><span data-stu-id="1e476-146">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="1e476-147">이 경우 건너뛰고 너무[Visual Studio 솔루션 설정](#SetupVS)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-147">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>
> * <span data-ttu-id="1e476-148">Azure DocumentDB 계정이 있나요?</span><span class="sxs-lookup"><span data-stu-id="1e476-148">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="1e476-149">따라서 사용자 계정이 Azure Cosmos DB 계정인 이제 하 고 건너뛰어도 너무[Visual Studio 솔루션 설정](#SetupVS)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-149">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="1e476-150">Hello Azure Cosmos DB 에뮬레이터를 사용 하는 경우 hello 단계에 따르십시오 [Azure Cosmos DB 에뮬레이터](local-emulator.md) toosetup 에뮬레이터 hello 및 너무 건너 뛸[Visual Studio 솔루션 설정](#SetupVS)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-150">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span>
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting tooany location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-hello-sample-application"></a><span data-ttu-id="1e476-151">Hello 샘플 응용 프로그램 복제</span><span class="sxs-lookup"><span data-stu-id="1e476-151">Clone hello sample application</span></span>

<span data-ttu-id="1e476-152">이제 보겠습니다 테이블 앱 github hello 연결 문자열을 설정 하 고 실행을 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-152">Now let's clone a Table app from github, set hello connection string, and run it.</span></span>

1. <span data-ttu-id="1e476-153">예: git bash git 터미널 윈도우를 열고 및 `cd` tooa 작업 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-153">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="1e476-154">다음 명령은 tooclone hello 샘플 리포지토리 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-154">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. <span data-ttu-id="1e476-155">그런 다음 Visual Studio에서 hello 솔루션 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-155">Then open hello solution file in Visual Studio.</span></span>

## <a name="update-your-connection-string"></a><span data-ttu-id="1e476-156">연결 문자열 업데이트</span><span class="sxs-lookup"><span data-stu-id="1e476-156">Update your connection string</span></span>

<span data-ttu-id="1e476-157">이제 돌아가서 toohello Azure 포털 tooget 연결 문자열 정보를 hello 앱에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-157">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="1e476-158">Hello에 [Azure 포털](http://portal.azure.com/), 프로그램 Azure Cosmos DB에에서 account, 왼쪽 탐색 hello 클릭 **키**, 클릭 하 고 **읽기-쓰기 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-158">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="1e476-159">Hello 다음 단계에서 hello app.config 파일에 hello hello 화면 toocopy hello 연결 문자열의 오른쪽에 hello 복사 단추를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-159">You'll use hello copy buttons on hello right side of hello screen toocopy hello connection string into hello app.config file in hello next step.</span></span>

2. <span data-ttu-id="1e476-160">Visual Studio에서 hello app.config 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-160">In Visual Studio, open hello app.config file.</span></span> 

3. <span data-ttu-id="1e476-161">Hello 포털 (hello 복사 단추 사용)에서 URI 값을 복사 하 고 쉽게 hello app.config에 hello 계정 키의 값입니다. App.config의 계정 이름에 대해 이전에 만든 hello 계정 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-161">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello account-key in app.config. Use hello account name created earlier for account-name in app.config.</span></span>
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> <span data-ttu-id="1e476-162">toouse toochange hello 연결 문자열에 필요한 표준 Azure 테이블 저장소로이 응용 프로그램에서는 `app.config file`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-162">toouse this app with standard Azure Table Storage, you need toochange hello connection string in `app.config file`.</span></span> <span data-ttu-id="1e476-163">테이블 계정 이름 및 Azure 저장소 기본 키로 키로 사용 하 여 hello 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-163">Use hello account name as Table-account name and key as Azure Storage Primary key.</span></span> <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-hello-app"></a><span data-ttu-id="1e476-164">빌드 및 hello 앱 배포</span><span class="sxs-lookup"><span data-stu-id="1e476-164">Build and deploy hello app</span></span>
1. <span data-ttu-id="1e476-165">Visual Studio에서 마우스 오른쪽 단추로 클릭 hello 프로젝트에 대해 **솔루션 탐색기** 클릭 하 고 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-165">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="1e476-166">Hello NuGet에서에서 **찾아보기** 상자에서 입력 ***WindowsAzure.Storage PremiumTable***합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-166">In hello NuGet **Browse** box, type ***WindowsAzure.Storage-PremiumTable***.</span></span> <span data-ttu-id="1e476-167">**시험판 버전 포함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-167">Check **Include prerelease versions**.</span></span>

3. <span data-ttu-id="1e476-168">Hello 결과 통해 설치 hello **WindowsAzure.Storage PremiumTable** hello 미리 보기 빌드를 선택 하 고 `0.0.1-preview`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-168">From hello results, install hello **WindowsAzure.Storage-PremiumTable** and choose hello preview build `0.0.1-preview`.</span></span> <span data-ttu-id="1e476-169">이 작업 hello Azure 테이블 저장소 패키지 및 모든 종속성을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-169">This action installs hello Azure Table storage package and all dependencies.</span></span>

4. <span data-ttu-id="1e476-170">CTRL + f 5를 클릭 toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-170">Click CTRL + F5 toorun hello application.</span></span> 

<span data-ttu-id="1e476-171">있습니다 수 이제 tooData 탐색기 돌아가서 및 쿼리 참조, 수정 및이 테이블 데이터와 함께 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-171">You can now go back tooData Explorer and see query, modify, and work with this table data.</span></span> 

> [!NOTE]
> <span data-ttu-id="1e476-172">toouse 정당한 하는 Azure Cosmos DB 에뮬레이터와 함께이 응용 프로그램 toochange hello 연결 문자열에 필요한 `app.config file`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-172">toouse this app with an Azure Cosmos DB Emulator, you just need toochange hello connection string in `app.config file`.</span></span> <span data-ttu-id="1e476-173">에뮬레이터에 대 한 값 보다 작은 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-173">Use hello below value for emulator.</span></span> <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a><span data-ttu-id="1e476-174">Azure DB Cosmos 기능</span><span class="sxs-lookup"><span data-stu-id="1e476-174">Azure Cosmos DB capabilities</span></span>
<span data-ttu-id="1e476-175">Cosmos DB azure의 hello Azure 테이블 저장소 API에서에서 사용할 수 없는 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-175">Azure Cosmos DB supports a number of capabilities that are not available in hello Azure Table storage API.</span></span> <span data-ttu-id="1e476-176">hello 새로운 기능 통해 사용할 수 있습니다 hello 다음 `appSettings` 구성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-176">hello new functionality can be enabled via hello following `appSettings` configuration values.</span></span> <span data-ttu-id="1e476-177">모든 새 서명 또는 오버 로드 toohello 미리 보기 Azure 저장소 SDK 소개 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-177">We did not introduce any new signatures or overloads toohello preview Azure Storage SDK.</span></span> <span data-ttu-id="1e476-178">이렇게 하면 tooconnect tooboth standard 및 premium 테이블, Blob 및 큐와 같은 다른 Azure 저장소 서비스와 작업 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-178">This allows you tooconnect tooboth standard and premium tables, and work with other Azure Storage services like Blobs and Queues.</span></span> 


| <span data-ttu-id="1e476-179">키</span><span class="sxs-lookup"><span data-stu-id="1e476-179">Key</span></span> | <span data-ttu-id="1e476-180">설명</span><span class="sxs-lookup"><span data-stu-id="1e476-180">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1e476-181">TableConnectionMode</span><span class="sxs-lookup"><span data-stu-id="1e476-181">TableConnectionMode</span></span>  | <span data-ttu-id="1e476-182">Azure Cosmos DB는 두 가지 연결 모드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-182">Azure Cosmos DB supports two connectivity modes.</span></span> <span data-ttu-id="1e476-183">`Gateway` 모드에서는 항상 요청은 해당 데이터 파티션에서 toohello 전달 toohello Azure Cosmos DB 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-183">In `Gateway` mode, requests are always made toohello Azure Cosmos DB gateway, which forwards it toohello corresponding data partitions.</span></span> <span data-ttu-id="1e476-184">`Direct` 연결 모드 hello 클라이언트 hello 매핑 테이블 toopartitions의를 가져오고 이러한 데이터 파티션에 대해 직접 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-184">In `Direct` connectivity mode, hello client fetches hello mapping of tables toopartitions, and requests are made directly against data partitions.</span></span> <span data-ttu-id="1e476-185">권장 `Direct`, 기본 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-185">We recommend `Direct`, hello default.</span></span>  |
| <span data-ttu-id="1e476-186">TableConnectionProtocol</span><span class="sxs-lookup"><span data-stu-id="1e476-186">TableConnectionProtocol</span></span> | <span data-ttu-id="1e476-187">Azure Cosmos DB는 두 가지 연결 프로토콜, 즉 `Https`과 `Tcp`를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-187">Azure Cosmos DB supports two connection protocols - `Https` and `Tcp`.</span></span> <span data-ttu-id="1e476-188">`Tcp`hello 기본 템플릿이 고 용량이 있기 때문에 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-188">`Tcp` is hello default, and recommended because it is more lightweight.</span></span> |
| <span data-ttu-id="1e476-189">TablePreferredLocations</span><span class="sxs-lookup"><span data-stu-id="1e476-189">TablePreferredLocations</span></span> | <span data-ttu-id="1e476-190">읽기에 대해 기본 설정된(멀티 홈) 위치를 쉼표로 구분한 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-190">Comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="1e476-191">Azure Cosmos DB 계정은 각각 1-30개 이상의 지역과 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-191">Each Azure Cosmos DB account can be associated with 1-30+ regions.</span></span> <span data-ttu-id="1e476-192">각 클라이언트 인스턴스에 대기 시간이 짧은 읽기에 대 한 hello 기본 설정 순서에 이러한 영역의 하위 집합을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-192">Each client instance can specify a subset of these regions in hello preferred order for low latency reads.</span></span> <span data-ttu-id="1e476-193">사용 하 여 hello 영역 이름은 해당 [표시 이름을](https://msdn.microsoft.com/library/azure/gg441293.aspx), 예를 들어 `West US`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-193">hello regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span> <span data-ttu-id="1e476-194">[멀티 호밍 API](tutorial-global-distribution-table.md)도 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e476-194">Also see [Multi-homing APIs](tutorial-global-distribution-table.md).</span></span>
| <span data-ttu-id="1e476-195">TableConsistencyLevel</span><span class="sxs-lookup"><span data-stu-id="1e476-195">TableConsistencyLevel</span></span> | <span data-ttu-id="1e476-196">잘 정의된 5가지 일관성 수준, 즉 `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix` 및 `Eventual` 중에서 선택하여 대기 시간, 일관성 및 가용성 간에 균형을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-196">You can trade off between latency, consistency, and availability by choosing between five well-defined consistency levels: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, and `Eventual`.</span></span> <span data-ttu-id="1e476-197">기본값은 `Session`입니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-197">Default is `Session`.</span></span> <span data-ttu-id="1e476-198">hello 선택한 일관성 수준에는 다중 지역 한 설정에서 성능이 크게 달라를 집니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-198">hello choice of consistency level makes a significant performance difference in multi-region setups.</span></span> <span data-ttu-id="1e476-199">자세한 내용은 [일관성 수준](consistency-levels.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e476-199">See [Consistency levels](consistency-levels.md) for details.</span></span> |
| <span data-ttu-id="1e476-200">TableThroughput</span><span class="sxs-lookup"><span data-stu-id="1e476-200">TableThroughput</span></span> | <span data-ttu-id="1e476-201">초당 요청 단위 (RU)로 표시 하는 hello 테이블에 대 한 예약 된 처리량입니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-201">Reserved throughput for hello table expressed in request units (RU) per second.</span></span> <span data-ttu-id="1e476-202">테이블당 100-수백만 RU/s를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-202">Single tables can support 100s-millions of RU/s.</span></span> <span data-ttu-id="1e476-203">[요청 단위](request-units.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e476-203">See [Request units](request-units.md).</span></span> <span data-ttu-id="1e476-204">기본값은 `400`입니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-204">Default is `400`</span></span> |
| <span data-ttu-id="1e476-205">TableIndexingPolicy</span><span class="sxs-lookup"><span data-stu-id="1e476-205">TableIndexingPolicy</span></span> | <span data-ttu-id="1e476-206">테이블 내 모든 열에 대해 일관된 자동 보조 인덱싱입니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-206">Consistent and automatic secondary indexing of all columns within tables</span></span> | <span data-ttu-id="1e476-207">JSON 인덱싱 정책을 지정 하는 표준에 맞는 toohello는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-207">JSON string conforming toohello indexing policy specification.</span></span> <span data-ttu-id="1e476-208">참조 [인덱싱 정책](indexing-policies.md) toosee 인덱싱 정책 tooinclude/제외 특정 열을 변경 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-208">See [Indexing Policy](indexing-policies.md) toosee how you can change indexing policy tooinclude/exclude specific columns.</span></span> | <span data-ttu-id="1e476-209">모든 속성의 자동 인덱싱(문자열에 대한 해시 및 숫자에 대한 범위)</span><span class="sxs-lookup"><span data-stu-id="1e476-209">Automatic indexing of all properties (hash for strings, and range for numbers)</span></span> |
| <span data-ttu-id="1e476-210">TableQueryMaxItemCount</span><span class="sxs-lookup"><span data-stu-id="1e476-210">TableQueryMaxItemCount</span></span> | <span data-ttu-id="1e476-211">Hello 단일 왕복에서 테이블 쿼리 당 반환 되는 항목의 최대 수를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-211">Configure hello maximum number of items returned per table query in a single round trip.</span></span> <span data-ttu-id="1e476-212">기본값은 `-1`, Azure Cosmos DB hello 값이 런타임에 동적으로 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-212">Default is `-1`, which lets Azure Cosmos DB dynamically determine hello value at runtime.</span></span> |
| <span data-ttu-id="1e476-213">TableQueryEnableScan</span><span class="sxs-lookup"><span data-stu-id="1e476-213">TableQueryEnableScan</span></span> | <span data-ttu-id="1e476-214">Hello 쿼리를 사용할 수 없는 hello 인덱스 모든 필터에 대 한 다음 실행 그래도 검색을 통해.</span><span class="sxs-lookup"><span data-stu-id="1e476-214">If hello query cannot use hello index for any filter, then run it anyway via a scan.</span></span> <span data-ttu-id="1e476-215">기본값은 `false`입니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-215">Default is `false`.</span></span>|
| <span data-ttu-id="1e476-216">TableQueryMaxDegreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="1e476-216">TableQueryMaxDegreeOfParallelism</span></span> | <span data-ttu-id="1e476-217">hello 수준의 크로스 파티션 쿼리 실행에 대 한 병렬 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-217">hello degree of parallelism for execution of a cross-partition query.</span></span> <span data-ttu-id="1e476-218">`0`없는 미리 인출과, 직렬 `1` 미리 인출과 직렬 이며 증가 hello 속도 병렬 처리 수준 값이 높을수록 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-218">`0` is serial with no pre-fetching, `1` is serial with pre-fetching, and higher values increase hello rate of parallelism.</span></span> <span data-ttu-id="1e476-219">기본값은 `-1`, Azure Cosmos DB hello 값이 런타임에 동적으로 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-219">Default is `-1`, which lets Azure Cosmos DB dynamically determine hello value at runtime.</span></span> |

<span data-ttu-id="1e476-220">toochange hello 기본 값, 열기 hello `app.config` Visual Studio의 솔루션 탐색기에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-220">toochange hello default value, open hello `app.config` file from Solution Explorer in Visual Studio.</span></span> <span data-ttu-id="1e476-221">Hello의 hello 내용을 추가 `<appSettings>` 요소 아래에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-221">Add hello contents of hello `<appSettings>` element shown below.</span></span> <span data-ttu-id="1e476-222">대체 `account-name` hello 저장소 계정의 이름으로 및 `account-key` 와 계정 액세스 키입니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-222">Replace `account-name` with hello name of your storage account, and `account-key` with your account access key.</span></span> 

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
      <!-- Client options -->
      <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key; TableEndpoint=https://account-name.documents.azure.com" />
      <add key="TableConnectionMode" value="Direct"/>
      <add key="TableConnectionProtocol" value="Tcp"/>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>
      <add key="TableConsistencyLevel" value="Eventual"/>

      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
      <add key="TableIndexingPolicy" value="{""indexingMode"": ""Consistent""}"/>

      <!-- Table query options -->
      <add key="TableQueryMaxItemCount" value="-1"/>
      <add key="TableQueryEnableScan" value="false"/>
      <add key="TableQueryMaxDegreeOfParallelism" value="-1"/>
      <add key="TableQueryContinuationTokenLimitInKb" value="16"/>
            
    </appSettings>
</configuration>
```

<span data-ttu-id="1e476-223">Hello 앱에서 일어나는 빠르게 검토를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-223">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="1e476-224">열기 hello `Program.cs` 다음 코드이 줄을 만든다고 hello 테이블 리소스 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-224">Open hello `Program.cs` file and you find that these lines of code create hello Table resources.</span></span> 

## <a name="create-hello-table-client"></a><span data-ttu-id="1e476-225">Hello 테이블 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="1e476-225">Create hello table client</span></span>
<span data-ttu-id="1e476-226">초기화는 `CloudTableClient` tooconnect toohello 테이블 계정.</span><span class="sxs-lookup"><span data-stu-id="1e476-226">You initialize a `CloudTableClient` tooconnect toohello table account.</span></span>

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
<span data-ttu-id="1e476-227">이 클라이언트 hello를 사용 하 여 초기화는 `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, 및 `TablePreferredLocations` hello 응용 프로그램 설정에 지정 된 값을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-227">This client is initialized using hello `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, and `TablePreferredLocations` configuration values if specified in hello app settings.</span></span>
    
## <a name="create-a-table"></a><span data-ttu-id="1e476-228">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="1e476-228">Create a table</span></span>
<span data-ttu-id="1e476-229">그런 다음 `CloudTable`을 사용하여 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-229">Then, you create a table using `CloudTable`.</span></span> <span data-ttu-id="1e476-230">Cosmos db Azure 테이블 저장소와 처리량을 기준으로 독립적으로 확장할 수 있습니다 및 분할 hello 서비스에 의해 자동으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-230">Tables in Azure Cosmos DB can scale independently in terms of storage and throughput, and partitioning is handled automatically by hello service.</span></span> <span data-ttu-id="1e476-231">Azure Cosmos DB는 고정된 크기 및 무제한 테이블을 모두 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-231">Azure Cosmos DB supports both fixed size and unlimited tables.</span></span> <span data-ttu-id="1e476-232">자세한 내용은 [Azure Cosmos DB에서 분할](partition-data.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e476-232">See [Partitioning in Azure Cosmos DB](partition-data.md) for details.</span></span> 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

<span data-ttu-id="1e476-233">테이블을 만드는 방법에는 중요한 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-233">There is an important difference in how tables are created.</span></span> <span data-ttu-id="1e476-234">Azure Cosmos DB는 트랜잭션에 대한 Azure 저장소의 사용량 기반 모델과 달리 처리량을 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-234">Azure Cosmos DB reserves throughput, unlike Azure storage's consumption-based model for transactions.</span></span> <span data-ttu-id="1e476-235">hello 예약 모델에 두 가지 주요 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-235">hello reservation model has two key benefits:</span></span>

* <span data-ttu-id="1e476-236">처리량은 전용/예약되어 있으므로 요청 속도가 프로비전된 처리량 이하인 경우에는 절대로 제한할 수 없습니다</span><span class="sxs-lookup"><span data-stu-id="1e476-236">Your throughput is dedicated/reserved, so you never get throttled if your request rate is at or below your provisioned throughput</span></span>
* <span data-ttu-id="1e476-237">hello 예약 모델은 더 많은 [처리량이 많은 작업에 대 한 비용 효율적인](key-value-store-cost.md)</span><span class="sxs-lookup"><span data-stu-id="1e476-237">hello reservation model is more [cost effective for throughput-heavy workloads](key-value-store-cost.md)</span></span>

<span data-ttu-id="1e476-238">에 대 한 hello 설정을 구성 하 여 hello 기본 처리량을 구성할 수 있습니다 `TableThroughput` 초당 RU (요청 단위)를 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-238">You can configure hello default throughput by configuring hello setting for `TableThroughput` in terms of RU (request units) per second.</span></span> 

<span data-ttu-id="1e476-239">1KB 엔터티 읽기를 1로 정규화 된 RU, 및 기타 작업은 정규화 된 tooa CPU, 메모리 및 IOPS 소비량에 따라 RU 값을 고정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-239">A read of a 1-KB entity is normalized as 1 RU, and other operations are normalized tooa fixed RU value based on their CPU, memory, and IOPS consumption.</span></span> <span data-ttu-id="1e476-240">[Azure Cosmos DB의 요청 단위](request-units.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="1e476-240">Learn more about [Request units in Azure Cosmos DB](request-units.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1e476-241">테이블 저장소 SDK 현재 수정 하 고 처리량을 지원 하지 않는데, 즉각적으로 언제 든 hello Azure 포털 또는 Azure CLI를 사용 하 여 hello 처리량을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-241">While Table storage SDK does not currently support modifying throughput, you can change hello throughput instantaneously at any time using hello Azure portal or Azure CLI.</span></span>

<span data-ttu-id="1e476-242">다음으로 hello 간단한 읽기는 과정을 안내 하 고 hello Azure 테이블 저장소 SDK를 사용 하 여 (CRUD) 작업을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-242">Next, we walk through hello simple read and write (CRUD) operations using hello Azure Table storage SDK.</span></span> <span data-ttu-id="1e476-243">이 자습서에서는 Azure Cosmos DB에서 제공하는 예측 가능한 짧은 대기 시간(한 자리 수의 밀리초) 및 빠른 쿼리를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-243">This tutorial demonstrates predictable low single-digit millisecond latencies and fast queries provided by Azure Cosmos DB.</span></span>

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="1e476-244">엔터티 tooa 테이블 추가</span><span class="sxs-lookup"><span data-stu-id="1e476-244">Add an entity tooa table</span></span>
<span data-ttu-id="1e476-245">Azure 테이블 저장소에서 엔터티의 hello에서 확장 `TableEntity` 클래스 및 있어야 `PartitionKey` 및 `RowKey` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-245">Entities in Azure Table storage extend from hello `TableEntity` class and must have `PartitionKey` and `RowKey` properties.</span></span> <span data-ttu-id="1e476-246">다음은 고객 엔터티에 대한 샘플 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-246">Here's a sample definition for a customer entity.</span></span>

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

<span data-ttu-id="1e476-247">다음 코드 조각 hello tooinsert에서 엔터티를 Azure 저장소 SDK를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-247">hello following snippet shows how tooinsert an entity with hello Azure storage SDK.</span></span> <span data-ttu-id="1e476-248">Azure Cosmos DB hello 전 세계 모든 규모에 짧은 대기 시간을 보장 하도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-248">Azure Cosmos DB is designed for guaranteed low latency at any scale, across hello world.</span></span>

<span data-ttu-id="1e476-249">쓰기 완료 < p99 및 실행 중인 응용 프로그램에 대 한 p50에서 ~ 6 ms 15 밀리초 hello Azure Cosmos DB 계정 hello와 동일한 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-249">Writes complete <15 ms at p99 and ~6 ms at p50 for applications running in hello same region as hello Azure Cosmos DB account.</span></span> <span data-ttu-id="1e476-250">고이 기간 동안 동기적으로 복제, 지 속력 있게 커밋된 모든 콘텐츠가 인덱싱된 후에 기록 하는 hello 팩트에 대 한 계정을 백 toohello 클라이언트 승인 수는 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-250">And this duration accounts for hello fact that writes are acknowledged back toohello client only after they are synchronously replicated, durably committed, and all content is indexed.</span></span>

<span data-ttu-id="1e476-251">hello Cosmos db Azure 테이블 API 미리 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-251">hello Table API for Azure Cosmos DB is in preview.</span></span> <span data-ttu-id="1e476-252">일반 공급 시 hello p99 대기 시간이 보장 다른 Azure Cosmos DB Api와 같이 Sla에 의해 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-252">At general availability, hello p99 latency guarantees are backed by SLAs like other Azure Cosmos DB APIs.</span></span> 

```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="1e476-253">엔터티 일괄 삽입</span><span class="sxs-lookup"><span data-stu-id="1e476-253">Insert a batch of entities</span></span>
<span data-ttu-id="1e476-254">삽입에 동일한 단일 일괄 처리 작업 hello와 azure 테이블 저장소에서는 수 있는 일괄 처리 작업을 API를 업데이트, 삭제를 결합 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-254">Azure Table storage supports a batch operation API, that lets you combine updates, deletes, and inserts in hello same single batch operation.</span></span> <span data-ttu-id="1e476-255">Azure Cosmos DB에는 몇몇 제한 사항이 적용 hello hello 배치 API에서 Azure 테이블 저장소로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-255">Azure Cosmos DB does not have some of hello limitations on hello batch API as Azure Table storage.</span></span> <span data-ttu-id="1e476-256">여러 쓰기 toohello 수행할 수 있습니다, 예를 들어 일괄 처리 내에서 여러 읽기를 수행할 수 있습니다는 일괄 처리 내에서 동일한 엔터티 및 일괄 처리 당 100 개의 작업에는 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-256">For example, you can perform multiple reads within a batch, you can perform multiple writes toohello same entity within a batch, and there is no limit on 100 operations per batch.</span></span> 

```csharp
// Create hello batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it toohello table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it toohello table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities toohello batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute hello batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a><span data-ttu-id="1e476-257">단일 엔터티 검색</span><span class="sxs-lookup"><span data-stu-id="1e476-257">Retrieve a single entity</span></span>
<span data-ttu-id="1e476-258">전체 Azure Cosmos DB에서 가져오거나 검색 < p99와 ~ 1에서 10 밀리초에서 p50에서 ms hello 같은 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-258">Retrieves (GETs) in Azure Cosmos DB complete <10 ms at p99 and ~1 ms at p50 in hello same Azure region.</span></span> <span data-ttu-id="1e476-259">대기 시간이 짧은 읽기에 대 한 개수 만큼 영역 tooyour 계정을 추가 하 고 설정 하 여 ("멀티홈")의 로컬 영역에서 응용 프로그램 tooread를 배포할 수 `TablePreferredLocations`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-259">You can add as many regions tooyour account for low latency reads, and deploy applications tooread from their local region ("multi-homed") by setting `TablePreferredLocations`.</span></span> 

<span data-ttu-id="1e476-260">다음 코드 조각 hello를 사용 하 여 단일 엔터티를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-260">You can retrieve a single entity using hello following snippet:</span></span>

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> <span data-ttu-id="1e476-261">[여러 지역을 사용하여 개발](tutorial-global-distribution-table.md)에서 멀티 호밍 API에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="1e476-261">Learn about multi-homing APIs at [Developing with multiple regions](tutorial-global-distribution-table.md)</span></span>
>

## <a name="query-entities-using-automatic-secondary-indexes"></a><span data-ttu-id="1e476-262">자동 보조 인덱스를 사용하여 엔터티 쿼리</span><span class="sxs-lookup"><span data-stu-id="1e476-262">Query entities using automatic secondary indexes</span></span>
<span data-ttu-id="1e476-263">Hello를 사용 하 여 테이블을 쿼리할 수 `TableQuery` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-263">Tables can be queried using hello `TableQuery` class.</span></span> <span data-ttu-id="1e476-264">Azure Cosmos DB에는 쓰기 액세스에 최적화된 데이터베이스 엔진이 있어 테이블 내의 모든 열을 자동으로 인덱싱합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-264">Azure Cosmos DB has a write-optimized database engine that automatically indexes all columns within your table.</span></span> <span data-ttu-id="1e476-265">인덱스를 만드는 Azure Cosmos DB에서 알 수 없는 tooschema 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-265">Indexing in Azure Cosmos DB is agnostic tooschema.</span></span> <span data-ttu-id="1e476-266">따라서 스키마 행 간에 차이가 있는 경우에 또는 hello 스키마 시간이 지나면서 자동으로 인덱싱.</span><span class="sxs-lookup"><span data-stu-id="1e476-266">Therefore, even if your schema is different between rows, or if hello schema evolves over time, it is automatically indexed.</span></span> <span data-ttu-id="1e476-267">Azure Cosmos DB 자동 보조 인덱스를 지원, 이므로 모든 속성에 대 한 쿼리 hello 인덱스를 사용할 수 하 고 효율적으로 처리할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-267">Since Azure Cosmos DB supports automatic secondary indexes, queries against any property can use hello index and be served efficiently.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");

// Filter against a property that's not partition key or row key
TableQuery<CustomerEntity> emailQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.GenerateFilterCondition("Email", QueryComparisons.Equal, "Ben@contoso.com"));

foreach (CustomerEntity entity in table.ExecuteQuery(emailQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

<span data-ttu-id="1e476-268">미리 보기에서 Azure Cosmos DB 지원 hello 같은 hello 테이블 API에 대 한 Azure 테이블 저장소와 기능을 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-268">In preview, Azure Cosmos DB supports hello same query functionality as Azure Table storage for hello Table API.</span></span> <span data-ttu-id="1e476-269">또한 Azure Cosmos DB는 정렬, 집계, 지리 공간적 쿼리, 계층 구조 및 다양한 기본 제공 함수도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-269">Azure Cosmos DB also supports sorting, aggregates, geospatial query, hierarchy, and a wide range of built-in functions.</span></span> <span data-ttu-id="1e476-270">hello 추가 기능이 이후 서비스 업데이트에 hello 테이블 API에서에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-270">hello additional functionality will be provided in hello Table API in a future service update.</span></span> <span data-ttu-id="1e476-271">이러한 기능에 대한 개요는 [Azure Cosmos DB 쿼리](documentdb-sql-query.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e476-271">See [Azure Cosmos DB query](documentdb-sql-query.md) for an overview of these capabilities.</span></span> 

## <a name="replace-an-entity"></a><span data-ttu-id="1e476-272">엔터티 바꾸기</span><span class="sxs-lookup"><span data-stu-id="1e476-272">Replace an entity</span></span>
<span data-ttu-id="1e476-273">엔터티에 tooupdate hello 테이블 서비스에서 검색, hello 엔터티 개체를 수정 및 다음 hello 변경 내용을 저장할 toohello 테이블 서비스를 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-273">tooupdate an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="1e476-274">hello 다음 코드 기존 고객의 전화 번호를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-274">hello following code changes an existing customer's phone number.</span></span> 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
<span data-ttu-id="1e476-275">마찬가지로 `InsertOrMerge` 또는 `Merge` 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-275">Similarly, you can perform `InsertOrMerge` or `Merge` operations.</span></span>  

## <a name="delete-an-entity"></a><span data-ttu-id="1e476-276">엔터티 삭제</span><span class="sxs-lookup"><span data-stu-id="1e476-276">Delete an entity</span></span>
<span data-ttu-id="1e476-277">Hello를 사용 하 여 검색 한 후에 쉽게 엔터티를 삭제할 수 있습니다 엔터티 업데이트에 대 한 표시 된 같은 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-277">You can easily delete an entity after you have retrieved it by using hello same pattern shown for updating an entity.</span></span> <span data-ttu-id="1e476-278">hello 코드 다음 검색 하 고 고객 엔터티를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-278">hello following code retrieves and deletes a customer entity.</span></span>

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a><span data-ttu-id="1e476-279">테이블 삭제</span><span class="sxs-lookup"><span data-stu-id="1e476-279">Delete a table</span></span>
<span data-ttu-id="1e476-280">마지막으로, 다음 코드 예제는 hello 저장소 계정에서 테이블을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-280">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="1e476-281">Azure Cosmos DB를 사용하여 테이블을 즉시 삭제하고 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-281">You can delete and recreate a table immediately with Azure Cosmos DB.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a><span data-ttu-id="1e476-282">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="1e476-282">Clean up resources</span></span> 

<span data-ttu-id="1e476-283">것 toocontinue toouse이이 앱을 하는 경우 단계 toodelete hello Azure 포털에서에서이 자습서에서 만든 모든 리소스를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-283">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span>   

1. <span data-ttu-id="1e476-284">Hello Azure 포털에서에서 왼쪽 메뉴 hello에서에서 클릭 **리소스 그룹** 만든 hello 리소스의 hello 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-284">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span>  
2. <span data-ttu-id="1e476-285">리소스 그룹 페이지에서 클릭 **삭제**hello 텍스트 상자에 hello 리소스 toodelete의 hello 이름을 입력 한 다음 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-285">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1e476-286">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1e476-286">Next steps</span></span>

<span data-ttu-id="1e476-287">이 자습서에서 다룬 hello 테이블 API가 있는 Azure Cosmos DB를 사용 하 여 tooget을 시작 하는 방법 및 hello 다음 작업을 수행 하면:</span><span class="sxs-lookup"><span data-stu-id="1e476-287">In this tutorial, we covered how tooget started using Azure Cosmos DB with hello Table API, and you've done hello following:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="1e476-288">Azure Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="1e476-288">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="1e476-289">Hello app.config 파일에 제공 된 기능</span><span class="sxs-lookup"><span data-stu-id="1e476-289">Enabled functionality in hello app.config file</span></span> 
> * <span data-ttu-id="1e476-290">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="1e476-290">Created a table</span></span> 
> * <span data-ttu-id="1e476-291">엔터티 tooa 테이블 추가</span><span class="sxs-lookup"><span data-stu-id="1e476-291">Added an entity tooa table</span></span> 
> * <span data-ttu-id="1e476-292">엔터티 일괄 삽입</span><span class="sxs-lookup"><span data-stu-id="1e476-292">Inserted a batch of entities</span></span> 
> * <span data-ttu-id="1e476-293">단일 엔터티 검색</span><span class="sxs-lookup"><span data-stu-id="1e476-293">Retrieved a single entity</span></span> 
> * <span data-ttu-id="1e476-294">자동 보조 인덱스를 사용하여 엔터티 쿼리</span><span class="sxs-lookup"><span data-stu-id="1e476-294">Queried entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="1e476-295">엔터티 바꾸기</span><span class="sxs-lookup"><span data-stu-id="1e476-295">Replaced an entity</span></span> 
> * <span data-ttu-id="1e476-296">엔터티 삭제</span><span class="sxs-lookup"><span data-stu-id="1e476-296">Deleted an entity</span></span> 
> * <span data-ttu-id="1e476-297">테이블 삭제</span><span class="sxs-lookup"><span data-stu-id="1e476-297">Deleted a table</span></span>  

<span data-ttu-id="1e476-298">이제 toohello 다음 자습서를 진행 하 고 테이블 데이터를 쿼리 하는 방법에 대 한 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e476-298">You can now proceed toohello next tutorial and learn more about querying table data.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="1e476-299">Hello 테이블 API가 있는 쿼리</span><span class="sxs-lookup"><span data-stu-id="1e476-299">Query with hello Table API</span></span>](tutorial-query-table.md)
