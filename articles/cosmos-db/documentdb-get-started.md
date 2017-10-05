---
title: "Azure Cosmos DB: DocumentDB API 시작 자습서 | Microsoft Docs"
description: "DocumentDB API를 사용하여 온라인 데이터베이스 및 C# 콘솔 응용 프로그램을 만드는 자습서입니다."
keywords: "NoSQL 자습서, 온라인 데이터베이스, C# 콘솔 응용 프로그램"
services: cosmos-db
documentationcenter: .net
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: bf08e031-718a-4a2a-89d6-91e12ff8797d
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2017
ms.author: anhoh
ms.openlocfilehash: 72f66081a6409f980ec6bca5188f585489245a36
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-documentdb-api-getting-started-tutorial"></a><span data-ttu-id="1f984-104">Azure Cosmos DB: DocumentDB API 시작 자습서</span><span class="sxs-lookup"><span data-stu-id="1f984-104">Azure Cosmos DB: DocumentDB API getting started tutorial</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1f984-105">.NET</span><span class="sxs-lookup"><span data-stu-id="1f984-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="1f984-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="1f984-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="1f984-107">MongoDB용 Node.js</span><span class="sxs-lookup"><span data-stu-id="1f984-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="1f984-108">Node.JS</span><span class="sxs-lookup"><span data-stu-id="1f984-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="1f984-109">Java</span><span class="sxs-lookup"><span data-stu-id="1f984-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="1f984-110">C++</span><span class="sxs-lookup"><span data-stu-id="1f984-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="1f984-111">Azure Cosmos DB DocumentDB API 시작 자습서를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-111">Welcome to the Azure Cosmos DB DocumentDB API getting started tutorial!</span></span> <span data-ttu-id="1f984-112">이 자습서를 따라 하면 Azure Cosmos DB 리소스를 만들고 쿼리하는 콘솔 응용 프로그램이 생깁니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="1f984-113">다음에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-113">We'll cover:</span></span>

* <span data-ttu-id="1f984-114">Azure Cosmos DB 계정 만들기 및 연결</span><span class="sxs-lookup"><span data-stu-id="1f984-114">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="1f984-115">Visual Studio 솔루션 구성</span><span class="sxs-lookup"><span data-stu-id="1f984-115">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="1f984-116">온라인 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="1f984-116">Creating an online database</span></span>
* <span data-ttu-id="1f984-117">컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="1f984-117">Creating a collection</span></span>
* <span data-ttu-id="1f984-118">JSON 문서 만들기</span><span class="sxs-lookup"><span data-stu-id="1f984-118">Creating JSON documents</span></span>
* <span data-ttu-id="1f984-119">컬렉션 쿼리</span><span class="sxs-lookup"><span data-stu-id="1f984-119">Querying the collection</span></span>
* <span data-ttu-id="1f984-120">문서 바꾸기</span><span class="sxs-lookup"><span data-stu-id="1f984-120">Replacing a document</span></span>
* <span data-ttu-id="1f984-121">문서 삭제</span><span class="sxs-lookup"><span data-stu-id="1f984-121">Deleting a document</span></span>
* <span data-ttu-id="1f984-122">데이터베이스 삭제</span><span class="sxs-lookup"><span data-stu-id="1f984-122">Deleting the database</span></span>

<span data-ttu-id="1f984-123">시간이 없으십니까?</span><span class="sxs-lookup"><span data-stu-id="1f984-123">Don't have time?</span></span> <span data-ttu-id="1f984-124">염려하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="1f984-124">Don't worry!</span></span> <span data-ttu-id="1f984-125">[GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started)에서 전체 솔루션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-125">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> <span data-ttu-id="1f984-126">빠른 지침을 보려면 [전체 NoSQL 자습서 솔루션 가져오기 섹션](#GetSolution)으로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="1f984-126">Jump to the [Get the complete NoSQL tutorial solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="1f984-127">나중에 이 페이지 위쪽 또는 아래쪽에 있는 응답 단추를 통해 의견을 보내주세요.</span><span class="sxs-lookup"><span data-stu-id="1f984-127">Afterwards, please use the voting buttons at the top or bottom of this page to give us feedback.</span></span> <span data-ttu-id="1f984-128">직접 연락을 받고 싶은 경우 설명에 메일 주소를 포함하세요.</span><span class="sxs-lookup"><span data-stu-id="1f984-128">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

<span data-ttu-id="1f984-129">이제 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-129">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f984-130">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1f984-130">Prerequisites</span></span>
<span data-ttu-id="1f984-131">다음 항목이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-131">Please make sure you have the following:</span></span>

* <span data-ttu-id="1f984-132">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="1f984-132">An active Azure account.</span></span> <span data-ttu-id="1f984-133">계정이 없는 경우 [무료 계정](https://azure.microsoft.com/free/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-133">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="1f984-134">또는 이 자습서에 [Azure Cosmos DB 에뮬레이터](local-emulator.md)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-134">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="1f984-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="1f984-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="1f984-136">1단계: Azure Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="1f984-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="1f984-137">Azure Cosmos DB 계정을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="1f984-138">계정이 이미 있는 경우 [Visual Studio 솔루션 설치](#SetupVS)로 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-138">If you already have an account you want to use, you can skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="1f984-139">Azure Cosmos DB 에뮬레이터를 사용하는 경우 [Azure Cosmos DB 에뮬레이터](local-emulator.md)의 단계에 따라 에뮬레이터를 설치하고 [Visual Studio 솔루션 설치](#SetupVS)로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-139">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="1f984-140"><a id="SetupVS"></a>2단계: Visual Studio 솔루션 설치</span><span class="sxs-lookup"><span data-stu-id="1f984-140"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="1f984-141">컴퓨터에서 **Visual Studio 2017**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-141">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="1f984-142">**파일** 메뉴에서 **새로 만들기**와 **프로젝트**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-142">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="1f984-143">**새 프로젝트** 대화 상자에서 **템플릿** / **Visual C#** / **콘솔 응용 프로그램**을 선택하고 프로젝트 이름을 지정한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-143">In the **New Project** dialog, select **Templates** / **Visual C#** / **Console Application**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="1f984-144">![새 프로젝트 창의 스크린샷](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="1f984-144">![Screen shot of the New Project window](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span></span>
4. <span data-ttu-id="1f984-145">**솔루션 탐색기**에서 Visual Studio 솔루션 아래에 있는 새 콘솔 응용 프로그램을 마우스 오른쪽 단추로 클릭한 다음 **NuGet 패키지 관리...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-145">In the **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![프로젝트의 마우스 오른쪽 단추 클릭 메뉴의 스크린샷](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="1f984-147">**Nuget** 탭에서 **찾아보기**를 클릭하고 검색 상자에 **azure documentdb**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-147">In the **Nuget** tab, click **Browse**, and type **azure documentdb** in the search box.</span></span>
6. <span data-ttu-id="1f984-148">결과 내에서 **Microsoft.Azure.DocumentDB**를 찾아 **설치l**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-148">Within the results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="1f984-149">Azure Cosmos DB DocumentDB API 클라이언트 라이브러리의 패키지 ID는 [Microsoft Azure DocumentDB Client Library](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/)입니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-149">The package ID for the Azure Cosmos DB DocumentDB API Client Library is [Microsoft Azure DocumentDB Client Library](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span></span>
   <span data-ttu-id="1f984-150">![Azure Cosmos DB 클라이언트 SDK를 찾기 위한 Nuget 메뉴의 스크린샷](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="1f984-150">![Screen shot of the Nuget Menu for finding Azure Cosmos DB Client SDK](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="1f984-151">솔루션 변경 사항 검토에 관한 메시지가 표시되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-151">If you get a messages about reviewing changes to the solution, click **OK**.</span></span> <span data-ttu-id="1f984-152">라이선스 승인에 관한 메시지가 표시되면 **동의합니다.**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-152">If you get a message about license acceptance, click **I accept**.</span></span>

<span data-ttu-id="1f984-153">잘하셨습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-153">Great!</span></span> <span data-ttu-id="1f984-154">설치를 완료했으므로 코드를 작성해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-154">Now that we finished the setup, let's start writing some code.</span></span> <span data-ttu-id="1f984-155">[GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs)에서 이 자습서의 완성된 코드 프로젝트를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-155">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span></span>

## <span data-ttu-id="1f984-156"><a id="Connect"></a>3단계: Azure Cosmos DB 계정에 연결</span><span class="sxs-lookup"><span data-stu-id="1f984-156"><a id="Connect"></a>Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="1f984-157">먼저 Program.cs에서 C# 응용 프로그램의 시작 부분에 다음 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-157">First, add these references to the beginning of your C# application, in the Program.cs file:</span></span>

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART TO YOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> <span data-ttu-id="1f984-158">이 자습서를 완료하려면 위의 종속성을 추가했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-158">In order to complete the tutorial, make sure you add the dependencies above.</span></span>
> 
> 

<span data-ttu-id="1f984-159">이제, 두 가지 상수와 *클라이언트* 변수를 공용 클래스 *프로그램* 아래에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-159">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

    public class Program
    {
        // ADD THIS PART TO YOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

<span data-ttu-id="1f984-160">다음으로 [Azure Portal](https://portal.azure.com)로 다시 이동하여 끝점 URL과 기본 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-160">Next, head back to the [Azure Portal](https://portal.azure.com) to retrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="1f984-161">끝점 URL과 기본 키는 응용 프로그램에서 연결할 위치를 식별하고 Azure Cosmos DB에서 응용 프로그램의 연결을 신뢰하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-161">The endpoint URL and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="1f984-162">Azure Portal에서 Azure Cosmos DB 계정으로 이동한 다음 **키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-162">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="1f984-163">포털에서 URI를 복사하고 program.cs 파일의 `<your endpoint URL>` 에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-163">Copy the URI from the portal and paste it into `<your endpoint URL>` in the program.cs file.</span></span> <span data-ttu-id="1f984-164">그런 다음 포털에서 기본 키를 복사하고 `<your primary key>`에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-164">Then copy the PRIMARY KEY from the portal and paste it into `<your primary key>`.</span></span>

![C# 콘솔 응용 프로그램을 만들기 위해 NoSQL 자습서에서 사용하는 Azure Portal의 스크린샷][keys]

<span data-ttu-id="1f984-167">다음으로 **DocumentClient**의 새 인스턴스를 만들어 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-167">Next, we'll start the application by creating a new instance of the **DocumentClient**.</span></span>

<span data-ttu-id="1f984-168">**Main** 메서드 아래에 **GetStartedDemo**라는 이름의 새 비동기 작업을 추가하면, 새 **DocumentClient**가 인스턴스화됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-168">Below the **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

    static void Main(string[] args)
    {
    }

    // ADD THIS PART TO YOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

<span data-ttu-id="1f984-169">다음 코드를 추가하여 **Main** 메서드에서 비동기 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-169">Add the following code to run your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="1f984-170">**Main** 메서드가 예외를 catch하여 콘솔에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-170">The **Main** method will catch exceptions and write them to the console.</span></span>

    static void Main(string[] args)
    {
            // ADD THIS PART TO YOUR CODE
            try
            {
                    Program p = new Program();
                    p.GetStartedDemo().Wait();
            }
            catch (DocumentClientException de)
            {
                    Exception baseException = de.GetBaseException();
                    Console.WriteLine("{0} error occurred: {1}, Message: {2}", de.StatusCode, de.Message, baseException.Message);
            }
            catch (Exception e)
            {
                    Exception baseException = e.GetBaseException();
                    Console.WriteLine("Error: {0}, Message: {1}", e.Message, baseException.Message);
            }
            finally
            {
                    Console.WriteLine("End of demo, press any key to exit.");
                    Console.ReadKey();
            }

<span data-ttu-id="1f984-171">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-171">Press **F5** to run your application.</span></span> <span data-ttu-id="1f984-172">콘솔 창 출력에서는 연결되었음을 확인하는 `End of demo, press any key to exit.` 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-172">The console window output displays the message `End of demo, press any key to exit.` confirming that the connection was made.</span></span>  <span data-ttu-id="1f984-173">그런 다음 콘솔 창을 닫을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-173">You can then close the console window.</span></span> 

<span data-ttu-id="1f984-174">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-174">Congratulations!</span></span> <span data-ttu-id="1f984-175">Azure Cosmos DB 계정에 성공적으로 연결되었으므로 Azure Cosmos DB 리소스 작업에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-175">You have successfully connected to an Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="1f984-176">4단계: 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="1f984-176">Step 4: Create a database</span></span>
<span data-ttu-id="1f984-177">데이터베이스 생성을 위한 코드를 추가하기 전에, 콘솔에 쓰기 위한 도우미 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-177">Before you add the code for creating a database, add a helper method for writing to the console.</span></span>

<span data-ttu-id="1f984-178">**WriteToConsoleAndPromptToContinue** 메서드를 복사하여 **GetStartedDemo** 메서드 다음에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-178">Copy and paste the **WriteToConsoleAndPromptToContinue** method after the **GetStartedDemo** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }

<span data-ttu-id="1f984-179">**DocumentClient** 클래스의 [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) 메서드를 사용하여 Azure Cosmos DB [데이터베이스](documentdb-resources.md#databases)를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-179">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using the [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="1f984-180">데이터베이스는 여러 컬렉션으로 분할된 JSON 문서 저장소의 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-180">A database is the logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="1f984-181">클라이언트를 만든 후 다음 코드를 복사하여 **GetStartedDemo** 메서드에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-181">Copy and paste the following code to your **GetStartedDemo** method after the client creation.</span></span> <span data-ttu-id="1f984-182">*FamilyDB*라는 데이터베이스가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-182">This will create a database named *FamilyDB*.</span></span>

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART TO YOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

<span data-ttu-id="1f984-183">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-183">Press **F5** to run your application.</span></span>

<span data-ttu-id="1f984-184">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-184">Congratulations!</span></span> <span data-ttu-id="1f984-185">Azure Cosmos DB 데이터베이스를 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-185">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="1f984-186"><a id="CreateColl"></a>5단계: 컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="1f984-186"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="1f984-187">**CreateDocumentCollectionIfNotExistsAsync**는 가격 책정 의미가 포함된 예약된 처리량이 있는 새 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-187">**CreateDocumentCollectionIfNotExistsAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="1f984-188">자세한 내용은 [가격 페이지](https://azure.microsoft.com/pricing/details/cosmos-db/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f984-188">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="1f984-189">**DocumentClient** 클래스의 [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) 메서드를 사용하여 [컬렉션](documentdb-resources.md#collections)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-189">A [collection](documentdb-resources.md#collections) can be created by using the [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="1f984-190">컬렉션은 JSON 문서 및 관련 JavaScript 응용 프로그램 논리의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-190">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="1f984-191">데이터베이스를 만든 후 다음 코드를 복사하여 **GetStartedDemo** 메서드에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-191">Copy and paste the following code to your **GetStartedDemo** method after the database creation.</span></span> <span data-ttu-id="1f984-192">*FamilyCollection*이라는 문서 컬렉션이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-192">This will create a document collection named *FamilyCollection*.</span></span>

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART TO YOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

<span data-ttu-id="1f984-193">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-193">Press **F5** to run your application.</span></span>

<span data-ttu-id="1f984-194">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-194">Congratulations!</span></span> <span data-ttu-id="1f984-195">Azure Cosmos DB 데이터베이스 컬렉션을 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-195">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="1f984-196"><a id="CreateDoc"></a>6단계: JSON 문서 만들기</span><span class="sxs-lookup"><span data-stu-id="1f984-196"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="1f984-197">**DocumentClient** 클래스의 [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) 메서드를 사용하여 [문서](documentdb-resources.md#documents)를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-197">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="1f984-198">문서는 사용자 정의(임의) JSON 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-198">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="1f984-199">이제 하나 이상의 문서를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-199">We can now insert one or more documents.</span></span> <span data-ttu-id="1f984-200">데이터베이스에 저장하려는 데이터가 이미 있는 경우 Azure Cosmos DB의 [데이터 마이그레이션 도구](import-data.md)를 사용하여 데이터를 데이터베이스로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-200">If you already have data you'd like to store in your database, you can use the Azure Cosmos DB [Data Migration tool](import-data.md) to import the data into a database.</span></span>

<span data-ttu-id="1f984-201">먼저 이 샘플에서는 Azure Cosmos DB 내에 저장된 개체를 나타내는 **가족** 클래스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-201">First, we need to create a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="1f984-202">또한 **가족** 내에서 사용되는 **부모**, **자식**, **애완 동물**, **주소** 하위 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-202">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="1f984-203">문서에는 JSON에서 **ID**로 직렬화된 **ID** 속성이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-203">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="1f984-204">**GetStartedDemo** 메서드 다음에 다음 내부 하위 클래스를 추가하여 이러한 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-204">Create these classes by adding the following internal sub-classes after the **GetStartedDemo** method.</span></span>

<span data-ttu-id="1f984-205">**가족**, **부모**, **자식**, **애완 동물** 및 **주소** 클래스를 복사하여 **WriteToConsoleAndPromptToContinue** 메서드 다음에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-205">Copy and paste the **Family**, **Parent**, **Child**, **Pet**, and **Address** classes after the **WriteToConsoleAndPromptToContinue** method.</span></span>

    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
    }

    // ADD THIS PART TO YOUR CODE
    public class Family
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        public string LastName { get; set; }
        public Parent[] Parents { get; set; }
        public Child[] Children { get; set; }
        public Address Address { get; set; }
        public bool IsRegistered { get; set; }
        public override string ToString()
        {
            return JsonConvert.SerializeObject(this);
        }
    }

    public class Parent
    {
        public string FamilyName { get; set; }
        public string FirstName { get; set; }
    }

    public class Child
    {
        public string FamilyName { get; set; }
        public string FirstName { get; set; }
        public string Gender { get; set; }
        public int Grade { get; set; }
        public Pet[] Pets { get; set; }
    }

    public class Pet
    {
        public string GivenName { get; set; }
    }

    public class Address
    {
        public string State { get; set; }
        public string County { get; set; }
        public string City { get; set; }
    }

<span data-ttu-id="1f984-206">**Address** 클래스 아래에 **CreateFamilyDocumentIfNotExists** 메서드를 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-206">Copy and paste the **CreateFamilyDocumentIfNotExists** method underneath your **Address** class.</span></span>

    // ADD THIS PART TO YOUR CODE
    private async Task CreateFamilyDocumentIfNotExists(string databaseName, string collectionName, Family family)
    {
        try
        {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, family.Id));
            this.WriteToConsoleAndPromptToContinue("Found {0}", family.Id);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), family);
                this.WriteToConsoleAndPromptToContinue("Created Family {0}", family.Id);
            }
            else
            {
                throw;
            }
        }
    }

<span data-ttu-id="1f984-207">그리고 Andersen Family와 Wakefield Family의 문서 하나씩 두 개의 문서를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-207">And insert two documents, one each for the Andersen Family and the Wakefield Family.</span></span>

<span data-ttu-id="1f984-208">문서 컬렉션을 만든 후 다음 코드를 복사하여 **GetStartedDemo** 메서드에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-208">Copy and paste the following code to your **GetStartedDemo** method after the document collection creation.</span></span>

    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });
    
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });


    // ADD THIS PART TO YOUR CODE
    Family andersenFamily = new Family
    {
            Id = "Andersen.1",
            LastName = "Andersen",
            Parents = new Parent[]
            {
                    new Parent { FirstName = "Thomas" },
                    new Parent { FirstName = "Mary Kay" }
            },
            Children = new Child[]
            {
                    new Child
                    {
                            FirstName = "Henriette Thaulow",
                            Gender = "female",
                            Grade = 5,
                            Pets = new Pet[]
                            {
                                    new Pet { GivenName = "Fluffy" }
                            }
                    }
            },
            Address = new Address { State = "WA", County = "King", City = "Seattle" },
            IsRegistered = true
    };

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", andersenFamily);

    Family wakefieldFamily = new Family
    {
            Id = "Wakefield.7",
            LastName = "Wakefield",
            Parents = new Parent[]
            {
                    new Parent { FamilyName = "Wakefield", FirstName = "Robin" },
                    new Parent { FamilyName = "Miller", FirstName = "Ben" }
            },
            Children = new Child[]
            {
                    new Child
                    {
                            FamilyName = "Merriam",
                            FirstName = "Jesse",
                            Gender = "female",
                            Grade = 8,
                            Pets = new Pet[]
                            {
                                    new Pet { GivenName = "Goofy" },
                                    new Pet { GivenName = "Shadow" }
                            }
                    },
                    new Child
                    {
                            FamilyName = "Miller",
                            FirstName = "Lisa",
                            Gender = "female",
                            Grade = 1
                    }
            },
            Address = new Address { State = "NY", County = "Manhattan", City = "NY" },
            IsRegistered = false
    };

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

<span data-ttu-id="1f984-209">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-209">Press **F5** to run your application.</span></span>

<span data-ttu-id="1f984-210">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-210">Congratulations!</span></span> <span data-ttu-id="1f984-211">두 개의 Azure Cosmos DB 문서를 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-211">You have successfully created two Azure Cosmos DB documents.</span></span>  

![NoSQL에서 C# 콘솔 응용 프로그램을 만들기 위해 사용한 계정, 데이터베이스, 컬렉션 및 문서 간의 계층 관계를 보여 주는 다이어그램](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="1f984-213"><a id="Query"></a>7단계: Azure Cosmos DB 리소스 쿼리</span><span class="sxs-lookup"><span data-stu-id="1f984-213"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="1f984-214">Azure Cosmos DB는 각 컬렉션에 저장된 JSON 문서에 대해 [다양한 쿼리](documentdb-sql-query.md)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-214">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="1f984-215">다음 샘플 코드는 Azure Cosmos DB SQL 구문뿐 아니라 LINQ를 사용하는 다양한 쿼리를 보여 줍니다. 이러한 쿼리는 이전 단계에서 삽입한 문서에 대해 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-215">The following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against the documents we inserted in the previous step.</span></span>

<span data-ttu-id="1f984-216">**ExecuteSimpleQuery** 메서드를 복사하여 **CreateFamilyDocumentIfNotExists** 메서드 다음에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-216">Copy and paste the **ExecuteSimpleQuery** method after your **CreateFamilyDocumentIfNotExists** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private void ExecuteSimpleQuery(string databaseName, string collectionName)
    {
        // Set some common query options
        FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

            // Here we find the Andersen family via its LastName
            IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                    .Where(f => f.LastName == "Andersen");

            // The query is executed synchronously here, but can also be executed asynchronously via the IDocumentQuery<T> interface
            Console.WriteLine("Running LINQ query...");
            foreach (Family family in familyQuery)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            // Now execute the same query via direct SQL
            IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                    "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                    queryOptions);

            Console.WriteLine("Running direct SQL query...");
            foreach (Family family in familyQueryInSql)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }

<span data-ttu-id="1f984-217">두 번째 문서를 만든 후 다음 코드를 복사하여 **GetStartedDemo** 메서드에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-217">Copy and paste the following code to your **GetStartedDemo** method after the second document creation.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART TO YOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="1f984-218">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-218">Press **F5** to run your application.</span></span>

<span data-ttu-id="1f984-219">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-219">Congratulations!</span></span> <span data-ttu-id="1f984-220">Azure Cosmos DB 컬렉션에 대한 쿼리가 성공적으로 수행되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-220">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="1f984-221">다음 다이어그램에서는 만든 컬렉션에 대해 Azure Cosmos DB SQL 쿼리 구문을 호출하는 방법을 보여 주며, 마찬가지로 동일한 논리가 LINQ 쿼리에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-221">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created, and the same logic applies to the LINQ query as well.</span></span>

![NoSQL에서 C# 콘솔 응용 프로그램을 만들기 위해 사용한 쿼리의 의미와 범위를 보여 주는 다이어그램](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="1f984-223">Azure Cosmos DB 쿼리는 이미 단일 컬렉션으로 범위가 지정되었기 때문에 [FROM](documentdb-sql-query.md#FromClause) 키워드는 쿼리에서 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-223">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span></span> <span data-ttu-id="1f984-224">따라서 "FROM Families f"를 "FROM root r" 또는 선택한 다른 변수 이름으로 교체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-224">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="1f984-225">Azure Cosmos DB는 패밀리, 루트 또는 선택한 변수 이름이 기본적으로 현재 컬렉션을 참조하는 것으로 유추합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-225">Azure Cosmos DB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

## <span data-ttu-id="1f984-226"><a id="ReplaceDocument"></a>8단계: JSON 문서 바꾸기</span><span class="sxs-lookup"><span data-stu-id="1f984-226"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="1f984-227">Azure Cosmos DB는 JSON 문서 바꾸기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-227">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="1f984-228">**ReplaceFamilyDocument** 메서드를 복사하여 **ExecuteSimpleQuery** 메서드 다음에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-228">Copy and paste the **ReplaceFamilyDocument** method after your **ExecuteSimpleQuery** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

<span data-ttu-id="1f984-229">메서드 끝에서 쿼리를 실행한 후 다음 코드를 복사하여 **GetStartedDemo** 메서드에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-229">Copy and paste the following code to your **GetStartedDemo** method after the query execution, at the end of the method.</span></span> <span data-ttu-id="1f984-230">문서를 바꾼 후에, 변경된 문서를 표시하도록 같은 쿼리가 다시 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-230">After replacing the document, this will run the same query again to view the changed document.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART TO YOUR CODE
    // Update the Grade of the Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="1f984-231">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-231">Press **F5** to run your application.</span></span>

<span data-ttu-id="1f984-232">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-232">Congratulations!</span></span> <span data-ttu-id="1f984-233">Azure Cosmos DB 문서를 성공적으로 대체했습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-233">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="1f984-234"><a id="DeleteDocument"></a>9단계: JSON 문서 삭제</span><span class="sxs-lookup"><span data-stu-id="1f984-234"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="1f984-235">Azure Cosmos DB는 JSON 문서 삭제를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-235">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="1f984-236">**DeleteFamilyDocument** 메서드를 복사하여 **ReplaceFamilyDocument** 메서드 다음에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-236">Copy and paste the **DeleteFamilyDocument** method after your **ReplaceFamilyDocument** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

<span data-ttu-id="1f984-237">메서드 끝에서 두 번째 쿼리를 실행한 후 다음 코드를 복사하여 **GetStartedDemo** 메서드에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-237">Copy and paste the following code to your **GetStartedDemo** method after the second query execution, at the end of the method.</span></span>

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART TO CODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

<span data-ttu-id="1f984-238">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-238">Press **F5** to run your application.</span></span>

<span data-ttu-id="1f984-239">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-239">Congratulations!</span></span> <span data-ttu-id="1f984-240">Azure Cosmos DB 문서를 성공적으로 삭제했습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-240">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="1f984-241"><a id="DeleteDatabase"></a>10단계: 데이터베이스 삭제</span><span class="sxs-lookup"><span data-stu-id="1f984-241"><a id="DeleteDatabase"></a>Step 10: Delete the database</span></span>
<span data-ttu-id="1f984-242">만든 데이터베이스를 삭제하면 데이터베이스와 모든 자식 리소스(컬렉션, 문서 등)가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-242">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="1f984-243">문서를 삭제한 후 다음 코드를 복사하여 **GetStartedDemo** 메서드에 붙여넣어 전체 데이터베이스 및 모든 자식 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-243">Copy and paste the following code to your **GetStartedDemo** method after the document delete to delete the entire database and all children resources.</span></span>

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART TO CODE
    // Clean up/delete the database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

<span data-ttu-id="1f984-244">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-244">Press **F5** to run your application.</span></span>

<span data-ttu-id="1f984-245">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-245">Congratulations!</span></span> <span data-ttu-id="1f984-246">Azure Cosmos DB 데이터베이스를 성공적으로 삭제했습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-246">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="1f984-247"><a id="Run"></a>11단계: C# 콘솔 응용 프로그램 모두 함께 실행</span><span class="sxs-lookup"><span data-stu-id="1f984-247"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="1f984-248">디버그 모드에서 응용 프로그램을 빌드하려면 Visual Studio에서 F5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-248">Hit F5 in Visual Studio to build the application in debug mode.</span></span>

<span data-ttu-id="1f984-249">시작한 앱의 출력이 콘솔 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-249">You should see the output of your get started app in a console window.</span></span> <span data-ttu-id="1f984-250">출력은 추가한 쿼리 결과를 보여 주며, 아래 예제 텍스트와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-250">The output will show the results of the queries we added and should match the example text below.</span></span>

    Created FamilyDB
    Press any key to continue ...
    Created FamilyCollection
    Press any key to continue ...
    Created Family Andersen.1
    Press any key to continue ...
    Created Family Wakefield.7
    Press any key to continue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Replaced Family Andersen.1
    Press any key to continue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Deleted Family Andersen.1
    End of demo, press any key to exit.

<span data-ttu-id="1f984-251">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-251">Congratulations!</span></span> <span data-ttu-id="1f984-252">이 자습서를 완료했으며 실행되는 C# 콘솔 응용 프로그램이 생겼습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-252">You've completed the tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="1f984-253"><a id="GetSolution"></a> 전체 자습서 솔루션 가져오기</span><span class="sxs-lookup"><span data-stu-id="1f984-253"><a id="GetSolution"></a> Get the complete tutorial solution</span></span>
<span data-ttu-id="1f984-254">이 자습서의 단계를 완료할 시간이 없거나 코드 샘플만 다운로드하려는 경우 [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started)에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-254">If you didn't have time to complete the steps in this tutorial, or just want to download the code samples, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> 

<span data-ttu-id="1f984-255">GetStarted 솔루션을 빌드하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-255">To build the GetStarted solution, you will need the following:</span></span>

* <span data-ttu-id="1f984-256">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="1f984-256">An active Azure account.</span></span> <span data-ttu-id="1f984-257">계정이 없는 경우 [무료 계정](https://azure.microsoft.com/free/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-257">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="1f984-258">[Azure Cosmos DB 계정][cosmos-db-create-account].</span><span class="sxs-lookup"><span data-stu-id="1f984-258">An [Azure Cosmos DB account][cosmos-db-create-account].</span></span>
* <span data-ttu-id="1f984-259">GitHub에서 제공하는 [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) 솔루션</span><span class="sxs-lookup"><span data-stu-id="1f984-259">The [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="1f984-260">Visual Studio에서 Azure Cosmos DB .NET SDK에 대한 참조를 복원하려면 솔루션 탐색기에서 **GetStarted** 솔루션을 마우스 오른쪽 단추로 클릭한 다음 **NuGet 패키지 복원 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-260">To restore the references to the Azure Cosmos DB .NET SDK in Visual Studio, right-click the **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="1f984-261">다음으로, App.config 파일에서 EndpointUrl 및 AuthorizationKey 값을 [Azure Cosmos DB 계정에 연결](#Connect)에 설명된 대로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-261">Next, in the App.config file, update the EndpointUrl and AuthorizationKey values as described in [Connect to an Azure Cosmos DB account](#Connect).</span></span>

<span data-ttu-id="1f984-262">정말 간단하죠? 빌드하고 원하는 대로 진행하세요!</span><span class="sxs-lookup"><span data-stu-id="1f984-262">That's it, build it and you're on your way!</span></span>


## <a name="next-steps"></a><span data-ttu-id="1f984-263">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1f984-263">Next steps</span></span>
* <span data-ttu-id="1f984-264">보다 복잡한 ASP.NET MVC 자습서가 필요하신가요?</span><span class="sxs-lookup"><span data-stu-id="1f984-264">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="1f984-265">[ASP.NET MVC 자습서: Azure Cosmos DB를 사용한 웹 응용 프로그램 개발](documentdb-dotnet-application.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f984-265">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="1f984-266">Azure Cosmos DB를 사용하여 규모 및 성능 테스트를 수행하고 싶으신가요?</span><span class="sxs-lookup"><span data-stu-id="1f984-266">Want to perform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="1f984-267">[Azure Cosmos DB를 사용한 성능 및 규모 테스트](performance-testing.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f984-267">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="1f984-268">[Azure Cosmos DB 요청, 사용 및 저장소 모니터링](monitor-accounts.md) 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="1f984-268">Learn how to [monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="1f984-269">[쿼리 실습](https://www.documentdb.com/sql/demo)의 샘플 데이터 집합에 대해 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f984-269">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="1f984-270">Azure Cosmos DB에 대한 자세한 내용은 [Azure Cosmos DB 시작](https://docs.microsoft.com/azure/cosmos-db/introduction)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f984-270">To learn more about Azure Cosmos DB, see [Welcome to Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-documentdb-dotnet.md#create-account
