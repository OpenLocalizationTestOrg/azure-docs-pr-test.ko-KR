---
title: "테이블 API를 사용하여 Azure Cosmos DB .NET 응용 프로그램 빌드 | Microsoft Docs"
description: ".NET을 사용하여 Azure Cosmos DB의 Table API 시작"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 66327041-4d5e-4ce6-a394-fee107c18e59
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/22/2017
ms.author: arramac
ms.openlocfilehash: 29e7eebda5177d6e852ef04ad82d9d38a8d30ed8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-the-table-api"></a><span data-ttu-id="478fd-103">Azure Cosmos DB: 테이블 API를 사용하여 .NET 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="478fd-103">Azure Cosmos DB: Build a .NET application using the Table API</span></span>

<span data-ttu-id="478fd-104">Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="478fd-105">Azure Cosmos DB의 핵심인 전역 배포 및 수평적 크기 조정 기능의 이점을 활용하여 문서, 키/값 및 그래프 데이터베이스를 빠르게 만들고 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="478fd-106">이 빠른 시작에서는 Azure Portal을 사용하여 Azure Cosmos DB 계정 및 해당 계정 내에서 테이블을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-106">This quick start demonstrates how to create an Azure Cosmos DB account, and create a table within that account using the Azure portal.</span></span> <span data-ttu-id="478fd-107">그런 다음 엔터티를 삽입, 업데이트 및 삭제하는 코드를 작성하고, NuGet의 새로운 [Microsoft Azure Storage Premium Table](https://aka.ms/premiumtablenuget)(미리 보기) 패키지를 사용하여 일부 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-107">You'll then write code to insert, update, and delete entities, and run some queries using the new [Windows Azure Storage Premium Table](https://aka.ms/premiumtablenuget) (preview) package from NuGet.</span></span> <span data-ttu-id="478fd-108">이 라이브러리는 공용 [Microsoft Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage)와 동일한 클래스 및 메서드 시그니처를 갖추고 있지만 [Table API](table-introduction.md)(미리 보기)를 사용하여 Azure Cosmos DB 계정에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-108">This library has the same classes and method signatures as the public [Windows Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also has the ability to connect to Azure Cosmos DB accounts using the [Table API](table-introduction.md) (preview).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="478fd-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="478fd-109">Prerequisites</span></span>

<span data-ttu-id="478fd-110">Visual Studio 2017이 아직 설치되지 않은 경우 **체험판** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)을 다운로드하고 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-110">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="478fd-111">Visual Studio를 설정하는 동안 **Azure 개발**을 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-111">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="478fd-112">데이터베이스 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="478fd-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)]

## <a name="add-a-table"></a><span data-ttu-id="478fd-113">테이블 추가</span><span class="sxs-lookup"><span data-stu-id="478fd-113">Add a table</span></span>

[!INCLUDE [cosmos-db-create-table](../../includes/cosmos-db-create-table.md)]

## <a name="add-sample-data"></a><span data-ttu-id="478fd-114">샘플 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="478fd-114">Add sample data</span></span>

<span data-ttu-id="478fd-115">이제 데이터 탐색기(미리 보기)를 사용하여 새 테이블에 데이터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-115">You can now add data to your new table using Data Explorer (Preview).</span></span>

1. <span data-ttu-id="478fd-116">데이터 탐색기에서 **sample-table**, **엔터티**를 클릭한 다음 **엔터티 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-116">In Data Explorer, expand **sample-table**, click **Entities**, and then click **Add Entity**.</span></span>

   ![Azure Portal의 데이터 탐색기에서 새 엔터티 만들기](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-document.png)
2. <span data-ttu-id="478fd-118">이제 PartitionKey 값 상자 및 RowKey 값 상자에 데이터를 추가하고 **엔터티 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-118">Now add data to the PartitionKey value box and RowKey value box, and click **Add Entity**.</span></span>

   ![새 엔터티에 대한 분할 키와 행 키 설정](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-entity.png)
  
    <span data-ttu-id="478fd-120">이제 테이블에 더 많은 엔터티를 추가하고 엔터티를 편집하거나 데이터 탐색기에서 데이터를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-120">You can now add more entities to your table, edit your entities, or query your data in Data Explorer.</span></span> <span data-ttu-id="478fd-121">데이터 탐색기에서는 처리량을 확장하고 테이블에 저장된 프로시저, 사용자 정의 함수 및 트리거를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-121">Data Explorer is also where you can scale your throughput and add stored procedures, user defined functions, and triggers to your table.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="478fd-122">샘플 응용 프로그램 복제</span><span class="sxs-lookup"><span data-stu-id="478fd-122">Clone the sample application</span></span>

<span data-ttu-id="478fd-123">이제 github에서 Table 앱을 복제하고 연결 문자열을 설정한 다음 실행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-123">Now let's clone a Table app from github, set the connection string, and run it.</span></span> <span data-ttu-id="478fd-124">프로그래밍 방식으로 데이터를 사용하여 얼마나 쉽게 작업할 수 있는지 알게 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-124">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="478fd-125">git bash와 같은 git 터미널 창을 열고 `cd`를 수행하여 작업 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-125">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="478fd-126">다음 명령을 실행하여 샘플 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-126">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started.git
    ```

3. <span data-ttu-id="478fd-127">그런 다음 Visual Studio에서 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-127">Then open the solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="478fd-128">코드 검토</span><span class="sxs-lookup"><span data-stu-id="478fd-128">Review the code</span></span>

<span data-ttu-id="478fd-129">앱에서 어떤 상황이 발생하고 있는지 빠르게 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-129">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="478fd-130">Program.cs 파일을 열어 보면 이러한 코드 줄에서 Azure Cosmos DB 리소스를 만드는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-130">Open the Program.cs file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="478fd-131">CloudTableClient가 초기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-131">The CloudTableClient is initialized.</span></span>

    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); 
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

* <span data-ttu-id="478fd-132">새 테이블이 존재하지 않는 경우 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-132">A new table is created if it does not exist.</span></span>

    ```csharp
    CloudTable table = tableClient.GetTableReference("people");
    table.CreateIfNotExists();
    ```

* <span data-ttu-id="478fd-133">새 테이블 컨테이너가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-133">A new Table container is created.</span></span> <span data-ttu-id="478fd-134">이 코드는 일반적인 Azure Table Storage SDK와 매우 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-134">You will notice this code very similar to regular Azure Table storage SDK.</span></span> 

    ```csharp
    CustomerEntity item = new CustomerEntity()
                {
                    PartitionKey = Guid.NewGuid().ToString(),
                    RowKey = Guid.NewGuid().ToString(),
                    Email = $"{GetRandomString(6)}@contoso.com",
                    PhoneNumber = "425-555-0102",
                    Bio = GetRandomString(1000)
                };
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="478fd-135">연결 문자열 업데이트</span><span class="sxs-lookup"><span data-stu-id="478fd-135">Update your connection string</span></span>

<span data-ttu-id="478fd-136">이제 연결 문자열 정보를 업데이트하면 앱이 Azure Cosmos DB과 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-136">Now we'll update the connection string information so your app can talk to Azure Cosmos DB.</span></span> 

1. <span data-ttu-id="478fd-137">Visual Studio에서 app.config 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-137">In Visual Studio, open the app.config file.</span></span> 

2. <span data-ttu-id="478fd-138">[Azure Portal](http://portal.azure.com/)에서 Azure Cosmos DB 왼쪽 탐색 메뉴에 있는 **연결 문자열**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-138">In the [Azure portal](http://portal.azure.com/), in the Azure Cosmos DB left navigation menu, click **Connection String**.</span></span> <span data-ttu-id="478fd-139">그런 다음 새 창에서 연결 문자열에 대한 복사 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-139">Then in the new pane click the copy button for the connection string.</span></span> 

    ![연결 문자열 창에서 끝점 및 계정 키 보기 및 복사](./media/create-table-dotnet/keys.png)

3. <span data-ttu-id="478fd-141">app.config 파일에 값을 PremiumStorageConnectionString의 값으로 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-141">Paste the value into the app.config file as the value of the PremiumStorageConnectionString.</span></span> 

    `<add key="PremiumStorageConnectionString" 
        value="DefaultEndpointsProtocol=https;AccountName=MYSTORAGEACCOUNT;AccountKey=AUTHKEY;TableEndpoint=https://COSMOSDB.documents.azure.com" />`    

    <span data-ttu-id="478fd-142">StandardStorageConnectionString은 그대로 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-142">You can leave the StandardStorageConnectionString as is.</span></span>

<span data-ttu-id="478fd-143">이제 Azure Cosmos DB와 통신하는 데 필요한 모든 정보로 앱이 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-143">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

## <a name="run-the-web-app"></a><span data-ttu-id="478fd-144">웹앱 실행</span><span class="sxs-lookup"><span data-stu-id="478fd-144">Run the web app</span></span>

1. <span data-ttu-id="478fd-145">Visual Studio의 **솔루션 탐색기**에서 **PremiumTableGetStarted** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-145">In Visual Studio, right-click on the **PremiumTableGetStarted** project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="478fd-146">NuGet **찾아보기** 상자에서 *WindowsAzure.Storage-PremiumTable*을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-146">In the NuGet **Browse** box, type *WindowsAzure.Storage-PremiumTable*.</span></span>

3. <span data-ttu-id="478fd-147">**시험판 포함** 상자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-147">Check the **Include prerelease** box.</span></span> 

4. <span data-ttu-id="478fd-148">결과에서 **WindowsAzure.Storage-PremiumTable** 라이브러리를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-148">From the results, install the **WindowsAzure.Storage-PremiumTable** library.</span></span> <span data-ttu-id="478fd-149">그러면 Azure Cosmos DB 테이블 API 미리 보기 패키지 뿐만 아니라 모든 종속성도 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-149">This installs the preview Azure Cosmos DB Table API package as well as all dependencies.</span></span> <span data-ttu-id="478fd-150">이는 Azure 테이블 저장소에서 사용되는 Microsoft Azure Storage 패키지와 다른 NuGet 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-150">Note that this is a different NuGet package than the Windows Azure Storage package used by Azure Table storage.</span></span> 

5. <span data-ttu-id="478fd-151">CTRL+F5를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-151">Click CTRL + F5 to run the application.</span></span>

    <span data-ttu-id="478fd-152">콘솔 창은 추가되고, 검색되고, 쿼리되고, 교체되고, 테이블에서 삭제되는 데이터를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-152">The console window displays the data being added, retrieved, queried, replaced and deleted from the table.</span></span> <span data-ttu-id="478fd-153">스크립트가 완료되면 아무 키를 눌러 콘솔 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-153">When the script completes, press any key to close the console window.</span></span> 
    
    ![빠른 시작의 콘솔 출력](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-console-output.png)

6. <span data-ttu-id="478fd-155">데이터 탐색기에서 새 엔터티를 보려면 삭제되지 않도록 program.cs의 188-208 줄에 주석으로 처리한 다음 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-155">If you want to see the new entities in Data Explorer, just comment out lines 188-208 in program.cs so they aren't deleted, then run the sample again.</span></span> 

    <span data-ttu-id="478fd-156">이제 데이터 탐색기로 돌아와서 **새로 고침**을 클릭하고 **사람** 테이블을 확장하고 **엔터티**를 클릭하면, 이 새 데이터로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-156">You can now go back to Data Explorer, click **Refresh**, expand the **people** table and click **Entities**, and then work with this new data.</span></span> 

    ![데이터 탐색기의 새 엔터티](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-data-explorer.png)

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="478fd-158">Azure Portal에서 SLA 검토</span><span class="sxs-lookup"><span data-stu-id="478fd-158">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="478fd-159">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="478fd-159">Clean up resources</span></span>

<span data-ttu-id="478fd-160">이 앱을 계속 사용하지 않으려면 Azure Portal에서 다음 단계에 따라 이 빠른 시작에서 만든 리소스를 모두 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-160">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span> 

1. <span data-ttu-id="478fd-161">Azure Portal의 왼쪽 메뉴에서 **리소스 그룹**을 클릭한 다음 만든 리소스의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-161">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="478fd-162">리소스 그룹 페이지에서 **삭제**를 클릭하고 텍스트 상자에서 삭제할 리소스의 이름을 입력한 다음 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-162">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="478fd-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="478fd-163">Next steps</span></span>

<span data-ttu-id="478fd-164">이 빠른 시작에서, Azure Cosmos DB 계정을 만들고, 데이터 탐색기를 사용하여 테이블을 만들고, 앱을 실행하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-164">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a table using the Data Explorer, and run an app.</span></span>  <span data-ttu-id="478fd-165">이제 테이블 API를 사용하여 데이터를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="478fd-165">Now you can query your data using the Table API.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="478fd-166">테이블 API를 사용하여 쿼리</span><span class="sxs-lookup"><span data-stu-id="478fd-166">Query using the Table API</span></span>](tutorial-query-table.md)

