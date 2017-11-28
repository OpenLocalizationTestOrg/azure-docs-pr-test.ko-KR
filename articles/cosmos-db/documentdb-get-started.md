---
title: "Azure Cosmos DB: DocumentDB API 시작 자습서 | Microsoft Docs"
description: "트 온라인 데이터베이스와 C# 콘솔 응용 프로그램 hello DocumentDB API를 사용 하 여 생성 하는 자습서입니다."
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
ms.openlocfilehash: 65a181f715a670987492ad7815ef2ec94498e84d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-api-getting-started-tutorial"></a><span data-ttu-id="fe012-104">Azure Cosmos DB: DocumentDB API 시작 자습서</span><span class="sxs-lookup"><span data-stu-id="fe012-104">Azure Cosmos DB: DocumentDB API getting started tutorial</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fe012-105">.NET</span><span class="sxs-lookup"><span data-stu-id="fe012-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="fe012-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="fe012-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="fe012-107">MongoDB용 Node.js</span><span class="sxs-lookup"><span data-stu-id="fe012-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="fe012-108">Node.JS</span><span class="sxs-lookup"><span data-stu-id="fe012-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="fe012-109">Java</span><span class="sxs-lookup"><span data-stu-id="fe012-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="fe012-110">C++</span><span class="sxs-lookup"><span data-stu-id="fe012-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="fe012-111">시작 toohello Azure Cosmos DB DocumentDB API 시작 자습서!</span><span class="sxs-lookup"><span data-stu-id="fe012-111">Welcome toohello Azure Cosmos DB DocumentDB API getting started tutorial!</span></span> <span data-ttu-id="fe012-112">이 자습서를 따라 하면 Azure Cosmos DB 리소스를 만들고 쿼리하는 콘솔 응용 프로그램이 생깁니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="fe012-113">다음에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-113">We'll cover:</span></span>

* <span data-ttu-id="fe012-114">만들기 및 tooan Azure Cosmos DB 계정 연결</span><span class="sxs-lookup"><span data-stu-id="fe012-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="fe012-115">Visual Studio 솔루션 구성</span><span class="sxs-lookup"><span data-stu-id="fe012-115">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="fe012-116">온라인 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="fe012-116">Creating an online database</span></span>
* <span data-ttu-id="fe012-117">컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="fe012-117">Creating a collection</span></span>
* <span data-ttu-id="fe012-118">JSON 문서 만들기</span><span class="sxs-lookup"><span data-stu-id="fe012-118">Creating JSON documents</span></span>
* <span data-ttu-id="fe012-119">Hello 컬렉션 쿼리</span><span class="sxs-lookup"><span data-stu-id="fe012-119">Querying hello collection</span></span>
* <span data-ttu-id="fe012-120">문서 바꾸기</span><span class="sxs-lookup"><span data-stu-id="fe012-120">Replacing a document</span></span>
* <span data-ttu-id="fe012-121">문서 삭제</span><span class="sxs-lookup"><span data-stu-id="fe012-121">Deleting a document</span></span>
* <span data-ttu-id="fe012-122">Hello 데이터베이스 삭제</span><span class="sxs-lookup"><span data-stu-id="fe012-122">Deleting hello database</span></span>

<span data-ttu-id="fe012-123">시간이 없으십니까?</span><span class="sxs-lookup"><span data-stu-id="fe012-123">Don't have time?</span></span> <span data-ttu-id="fe012-124">염려하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="fe012-124">Don't worry!</span></span> <span data-ttu-id="fe012-125">hello 완벽 한 솔루션에 있는 [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started)합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-125">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> <span data-ttu-id="fe012-126">Toohello 점프 [hello 전체 NoSQL 자습서 솔루션 섹션 가져오기](#GetSolution) 빠른 지침에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-126">Jump toohello [Get hello complete NoSQL tutorial solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="fe012-127">이후에 하십시오 사용 하 여 hello 투표 하는 단추 hello 위쪽 또는 아래쪽에이 페이지 toogive us 피드백.</span><span class="sxs-lookup"><span data-stu-id="fe012-127">Afterwards, please use hello voting buttons at hello top or bottom of this page toogive us feedback.</span></span> <span data-ttu-id="fe012-128">받을지 경우 toocontact를 직접 생각 될 전자 메일 주소 가능한 tooinclude 메모에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="fe012-129">이제 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-129">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe012-130">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fe012-130">Prerequisites</span></span>
<span data-ttu-id="fe012-131">Hello 다음 항목이 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="fe012-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="fe012-132">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="fe012-132">An active Azure account.</span></span> <span data-ttu-id="fe012-133">계정이 없는 경우 [무료 계정](https://azure.microsoft.com/free/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-133">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="fe012-134">Hello 또는 사용할 수 있습니다 [Azure Cosmos DB 에뮬레이터](local-emulator.md) 이 자습서에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-134">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="fe012-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="fe012-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="fe012-136">1단계: Azure Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="fe012-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="fe012-137">Azure Cosmos DB 계정을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="fe012-138">Toouse 원하는 계정을 이미 있는 경우 건너뛰어도 너무[Visual Studio 솔루션에 설치](#SetupVS)합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-138">If you already have an account you want toouse, you can skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="fe012-139">Hello Azure Cosmos DB 에뮬레이터를 사용 하는 경우 hello 단계에 따르십시오 [Azure Cosmos DB 에뮬레이터](local-emulator.md) toosetup 에뮬레이터 hello 및 너무 건너 뛸[Visual Studio 솔루션에 설치](#SetupVS)합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-139">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="fe012-140"><a id="SetupVS"></a>2단계: Visual Studio 솔루션 설치</span><span class="sxs-lookup"><span data-stu-id="fe012-140"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="fe012-141">컴퓨터에서 **Visual Studio 2017**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-141">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="fe012-142">Hello에 **파일** 메뉴 선택 **새로**를 선택한 후 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-142">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="fe012-143">Hello에 **새 프로젝트** 대화 상자에서 **템플릿** / **Visual C#** / **콘솔 응용 프로그램**, 이름 프로젝트 및 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-143">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console Application**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="fe012-144">![새 프로젝트 창 hello 스크린 샷](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="fe012-144">![Screen shot of hello New Project window](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span></span>
4. <span data-ttu-id="fe012-145">Hello에 **솔루션 탐색기**을 Visual Studio 솔루션에서 사용 중인 새 콘솔 응용 프로그램을 마우스 오른쪽 단추로 클릭 하 고 클릭 **NuGet 패키지 관리...**</span><span class="sxs-lookup"><span data-stu-id="fe012-145">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Hello 오른쪽 hello 프로젝트에 대 한 Clicked 메뉴를 스크린샷](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="fe012-147">Hello에 **Nuget** 탭을 클릭 **찾아보기**, 유형과 **azure documentdb** hello 검색 상자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-147">In hello **Nuget** tab, click **Browse**, and type **azure documentdb** in hello search box.</span></span>
6. <span data-ttu-id="fe012-148">Hello 결과 내 찾을 **Microsoft.Azure.DocumentDB** 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-148">Within hello results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="fe012-149">hello Azure Cosmos DB DocumentDB API 클라이언트 라이브러리에 대 한 hello 패키지 ID가 [Microsoft Azure DocumentDB 클라이언트 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/)합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-149">hello package ID for hello Azure Cosmos DB DocumentDB API Client Library is [Microsoft Azure DocumentDB Client Library](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span></span>
   <span data-ttu-id="fe012-150">![Azure Cosmos DB 클라이언트 SDK를 찾기 위한 hello Nuget 메뉴의 스크린 샷](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="fe012-150">![Screen shot of hello Nuget Menu for finding Azure Cosmos DB Client SDK](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="fe012-151">변경 내용을 toohello 솔루션을 검토 하는 방법에 대 한 메시지를 발생 하는 경우 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-151">If you get a messages about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="fe012-152">라이선스 승인에 관한 메시지가 표시되면 **동의합니다.**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-152">If you get a message about license acceptance, click **I accept**.</span></span>

<span data-ttu-id="fe012-153">잘하셨습니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-153">Great!</span></span> <span data-ttu-id="fe012-154">Hello 설치를 완료 했으므로 일부 코드 작성 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-154">Now that we finished hello setup, let's start writing some code.</span></span> <span data-ttu-id="fe012-155">[GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs)에서 이 자습서의 완성된 코드 프로젝트를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-155">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span></span>

## <span data-ttu-id="fe012-156"><a id="Connect"></a>3 단계: tooan Cosmos DB Azure 계정을 연결 하세요.</span><span class="sxs-lookup"><span data-stu-id="fe012-156"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="fe012-157">먼저,이 추가 응용 프로그램의 C# hello Program.cs 파일에 toohello 시작 부분을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-157">First, add these references toohello beginning of your C# application, in hello Program.cs file:</span></span>

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART tooYOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> <span data-ttu-id="fe012-158">순서 toocomplete hello 자습서에서는 위의 hello 종속성을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-158">In order toocomplete hello tutorial, make sure you add hello dependencies above.</span></span>
> 
> 

<span data-ttu-id="fe012-159">이제, 두 가지 상수와 *클라이언트* 변수를 공용 클래스 *프로그램* 아래에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-159">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

    public class Program
    {
        // ADD THIS PART tooYOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

<span data-ttu-id="fe012-160">Toohello 돌아가 다음으로, [Azure 포털](https://portal.azure.com) tooretrieve 끝점 URL 및 기본 키입니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-160">Next, head back toohello [Azure Portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="fe012-161">hello 끝점 URL 및 기본 키가 응용 프로그램 toounderstand에 필요한 위치 tooconnect 되며, Azure Cosmos DB tootrust에 대 한 응용 프로그램의 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-161">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="fe012-162">에 Azure 포털 hello, tooyour Azure Cosmos DB 계정을 탐색 한 다음 클릭 **키**합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-162">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="fe012-163">Hello 포털에서 hello URI를 복사 하 고 붙여 넣습니다 `<your endpoint URL>` hello program.cs 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-163">Copy hello URI from hello portal and paste it into `<your endpoint URL>` in hello program.cs file.</span></span> <span data-ttu-id="fe012-164">그러면 복사본 hello 포털에서 기본 키를 hello에 붙여 넣습니다 `<your primary key>`합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-164">Then copy hello PRIMARY KEY from hello portal and paste it into `<your primary key>`.</span></span>

![Azure 포털 hello NoSQL 자습서 toocreate C# 콘솔 응용 프로그램에서 사용 하는 hello 스크린 샷][keys]

<span data-ttu-id="fe012-167">다음으로 hello 응용 프로그램 hello의 새 인스턴스를 만들어 시작 합니다 **DocumentClient**합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-167">Next, we'll start hello application by creating a new instance of hello **DocumentClient**.</span></span>

<span data-ttu-id="fe012-168">Hello 아래 **Main** 메서드를이 비동기 작업 호출 추가 **GetStartedDemo**는 새 우리의 인스턴스화하고 **DocumentClient**합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-168">Below hello **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

    static void Main(string[] args)
    {
    }

    // ADD THIS PART tooYOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

<span data-ttu-id="fe012-169">Hello 다음 코드 toorun에서 해당 비동기 작업을 추가 하면 **Main** 메서드.</span><span class="sxs-lookup"><span data-stu-id="fe012-169">Add hello following code toorun your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="fe012-170">hello **Main** 메서드 예외를 catch 하 고 toohello 콘솔에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-170">hello **Main** method will catch exceptions and write them toohello console.</span></span>

    static void Main(string[] args)
    {
            // ADD THIS PART tooYOUR CODE
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
                    Console.WriteLine("End of demo, press any key tooexit.");
                    Console.ReadKey();
            }

<span data-ttu-id="fe012-171">키를 눌러 **F5** toorun 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-171">Press **F5** toorun your application.</span></span> <span data-ttu-id="fe012-172">hello 메시지를 표시 하는 hello 콘솔 창 출력 `End of demo, press any key tooexit.` hello 연결이 생성 된 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-172">hello console window output displays hello message `End of demo, press any key tooexit.` confirming that hello connection was made.</span></span>  <span data-ttu-id="fe012-173">그런 다음 hello 콘솔 창을 닫을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-173">You can then close hello console window.</span></span> 

<span data-ttu-id="fe012-174">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-174">Congratulations!</span></span> <span data-ttu-id="fe012-175">Tooan Azure Cosmos DB 계정을 성공적으로 연결한, 이제 살펴보겠습니다는 Azure Cosmos DB 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-175">You have successfully connected tooan Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="fe012-176">4단계: 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="fe012-176">Step 4: Create a database</span></span>
<span data-ttu-id="fe012-177">데이터베이스를 만들기 위한 hello 코드를 추가 하기 전에 toohello 콘솔 작성 하기 위한 도우미 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-177">Before you add hello code for creating a database, add a helper method for writing toohello console.</span></span>

<span data-ttu-id="fe012-178">복사 및 붙여넣기 hello **WriteToConsoleAndPromptToContinue** 메서드 hello 후 **GetStartedDemo** 메서드.</span><span class="sxs-lookup"><span data-stu-id="fe012-178">Copy and paste hello **WriteToConsoleAndPromptToContinue** method after hello **GetStartedDemo** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

<span data-ttu-id="fe012-179">Azure Cosmos DB [데이터베이스](documentdb-resources.md#databases) hello를 사용 하 여 만들 수 [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) hello 방식의 **DocumentClient** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-179">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="fe012-180">데이터베이스는 컬렉션에 분할 된 JSON 문서 저장소의 hello 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-180">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="fe012-181">복사 및 붙여넣기 hello 다음 코드 tooyour **GetStartedDemo** hello 클라이언트를 만든 후 메서드.</span><span class="sxs-lookup"><span data-stu-id="fe012-181">Copy and paste hello following code tooyour **GetStartedDemo** method after hello client creation.</span></span> <span data-ttu-id="fe012-182">*FamilyDB*라는 데이터베이스가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-182">This will create a database named *FamilyDB*.</span></span>

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART tooYOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

<span data-ttu-id="fe012-183">키를 눌러 **F5** toorun 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-183">Press **F5** toorun your application.</span></span>

<span data-ttu-id="fe012-184">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-184">Congratulations!</span></span> <span data-ttu-id="fe012-185">Azure Cosmos DB 데이터베이스를 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-185">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="fe012-186"><a id="CreateColl"></a>5단계: 컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="fe012-186"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="fe012-187">**CreateDocumentCollectionIfNotExistsAsync**는 가격 책정 의미가 포함된 예약된 처리량이 있는 새 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-187">**CreateDocumentCollectionIfNotExistsAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="fe012-188">자세한 내용은 [가격 페이지](https://azure.microsoft.com/pricing/details/cosmos-db/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe012-188">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="fe012-189">A [컬렉션](documentdb-resources.md#collections) hello를 사용 하 여 만들 수 [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) hello 방식의 **DocumentClient** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-189">A [collection](documentdb-resources.md#collections) can be created by using hello [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="fe012-190">컬렉션은 JSON 문서 및 관련 JavaScript 응용 프로그램 논리의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-190">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="fe012-191">복사 및 붙여넣기 hello 다음 코드 tooyour **GetStartedDemo** hello 데이터베이스 생성 후 메서드.</span><span class="sxs-lookup"><span data-stu-id="fe012-191">Copy and paste hello following code tooyour **GetStartedDemo** method after hello database creation.</span></span> <span data-ttu-id="fe012-192">*FamilyCollection*이라는 문서 컬렉션이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-192">This will create a document collection named *FamilyCollection*.</span></span>

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART tooYOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

<span data-ttu-id="fe012-193">키를 눌러 **F5** toorun 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-193">Press **F5** toorun your application.</span></span>

<span data-ttu-id="fe012-194">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-194">Congratulations!</span></span> <span data-ttu-id="fe012-195">Azure Cosmos DB 데이터베이스 컬렉션을 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-195">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="fe012-196"><a id="CreateDoc"></a>6단계: JSON 문서 만들기</span><span class="sxs-lookup"><span data-stu-id="fe012-196"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="fe012-197">A [문서](documentdb-resources.md#documents) hello를 사용 하 여 만들 수 [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) hello 방식의 **DocumentClient** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-197">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="fe012-198">문서는 사용자 정의(임의) JSON 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-198">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="fe012-199">이제 하나 이상의 문서를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-199">We can now insert one or more documents.</span></span> <span data-ttu-id="fe012-200">이미 원하는 toostore 데이터베이스에 데이터가 있으면 hello Azure Cosmos DB를 사용할 수 있습니다 [데이터 마이그레이션 도구](import-data.md) tooimport hello 데이터를 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-200">If you already have data you'd like toostore in your database, you can use hello Azure Cosmos DB [Data Migration tool](import-data.md) tooimport hello data into a database.</span></span>

<span data-ttu-id="fe012-201">먼저 toocreate는 **제품군** 이 샘플에서 Azure Cosmos DB 내에 저장 하는 개체를 나타내는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-201">First, we need toocreate a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="fe012-202">또한 **가족** 내에서 사용되는 **부모**, **자식**, **애완 동물**, **주소** 하위 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-202">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="fe012-203">문서에는 JSON에서 **ID**로 직렬화된 **ID** 속성이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-203">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="fe012-204">Hello 내부 하위 클래스 hello 후 다음을 추가 하 여 이러한 클래스를 만들 **GetStartedDemo** 메서드.</span><span class="sxs-lookup"><span data-stu-id="fe012-204">Create these classes by adding hello following internal sub-classes after hello **GetStartedDemo** method.</span></span>

<span data-ttu-id="fe012-205">복사 및 붙여넣기 hello **제품군**, **부모**, **자식**, **애완 동물**, 및 **주소** hello 후 클래스 **WriteToConsoleAndPromptToContinue** 메서드.</span><span class="sxs-lookup"><span data-stu-id="fe012-205">Copy and paste hello **Family**, **Parent**, **Child**, **Pet**, and **Address** classes after hello **WriteToConsoleAndPromptToContinue** method.</span></span>

    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
    }

    // ADD THIS PART tooYOUR CODE
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

<span data-ttu-id="fe012-206">복사 및 붙여넣기 hello **CreateFamilyDocumentIfNotExists** 아래 메서드 여 **주소** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-206">Copy and paste hello **CreateFamilyDocumentIfNotExists** method underneath your **Address** class.</span></span>

    // ADD THIS PART tooYOUR CODE
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

<span data-ttu-id="fe012-207">두 문서, 각 hello Andersen 제품군 및 제품군 Wakefield hello를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-207">And insert two documents, one each for hello Andersen Family and hello Wakefield Family.</span></span>

<span data-ttu-id="fe012-208">복사 및 붙여넣기 hello 다음 코드 tooyour **GetStartedDemo** hello 문서 컬렉션을 만든 후 메서드.</span><span class="sxs-lookup"><span data-stu-id="fe012-208">Copy and paste hello following code tooyour **GetStartedDemo** method after hello document collection creation.</span></span>

    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });
    
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });


    // ADD THIS PART tooYOUR CODE
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

<span data-ttu-id="fe012-209">키를 눌러 **F5** toorun 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-209">Press **F5** toorun your application.</span></span>

<span data-ttu-id="fe012-210">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-210">Congratulations!</span></span> <span data-ttu-id="fe012-211">두 개의 Azure Cosmos DB 문서를 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-211">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Hello 계정과 hello 온라인 데이터베이스, hello 컬렉션 hello NoSQL 자습서 toocreate C# 콘솔 응용 프로그램에서 사용 하는 hello 문서 간의 hello 계층 관계를 보여 주는 다이어그램](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="fe012-213"><a id="Query"></a>7단계: Azure Cosmos DB 리소스 쿼리</span><span class="sxs-lookup"><span data-stu-id="fe012-213"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="fe012-214">Azure Cosmos DB는 각 컬렉션에 저장된 JSON 문서에 대해 [다양한 쿼리](documentdb-sql-query.md)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-214">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="fe012-215">hello 다음 샘플 코드를 보여 줍니다 다양 한 쿼리-두 Azure Cosmos DB SQL을 사용 하 여 것에 대해 실행할 수 있는 LINQ-뿐 아니라 구문 hello 문서 hello 이전 단계에서 삽입 했습니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-215">hello following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against hello documents we inserted in hello previous step.</span></span>

<span data-ttu-id="fe012-216">복사 및 붙여넣기 hello **ExecuteSimpleQuery** 메서드 후 프로그램 **CreateFamilyDocumentIfNotExists** 메서드.</span><span class="sxs-lookup"><span data-stu-id="fe012-216">Copy and paste hello **ExecuteSimpleQuery** method after your **CreateFamilyDocumentIfNotExists** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private void ExecuteSimpleQuery(string databaseName, string collectionName)
    {
        // Set some common query options
        FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

            // Here we find hello Andersen family via its LastName
            IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                    .Where(f => f.LastName == "Andersen");

            // hello query is executed synchronously here, but can also be executed asynchronously via hello IDocumentQuery<T> interface
            Console.WriteLine("Running LINQ query...");
            foreach (Family family in familyQuery)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            // Now execute hello same query via direct SQL
            IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                    "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                    queryOptions);

            Console.WriteLine("Running direct SQL query...");
            foreach (Family family in familyQueryInSql)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

<span data-ttu-id="fe012-217">복사 및 붙여넣기 hello 다음 코드 tooyour **GetStartedDemo** hello 두 번째 문서를 만든 후 메서드.</span><span class="sxs-lookup"><span data-stu-id="fe012-217">Copy and paste hello following code tooyour **GetStartedDemo** method after hello second document creation.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART tooYOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="fe012-218">키를 눌러 **F5** toorun 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-218">Press **F5** toorun your application.</span></span>

<span data-ttu-id="fe012-219">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-219">Congratulations!</span></span> <span data-ttu-id="fe012-220">Azure Cosmos DB 컬렉션에 대한 쿼리가 성공적으로 수행되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-220">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="fe012-221">hello 다음 다이어그램에서는 구문 hello 컬렉션에 대해 호출 되는 hello Azure Cosmos DB SQL 쿼리를 만든 방법, 고 hello 동일한 논리 적용 toohello LINQ 쿼리도 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-221">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created, and hello same logic applies toohello LINQ query as well.</span></span>

![다이어그램 hello 범위를 표현 하 고 hello 쿼리의 의미에서 사용 하는 hello NoSQL 자습서 toocreate C# 콘솔 응용 프로그램](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="fe012-223">hello [FROM](documentdb-sql-query.md#FromClause) Azure Cosmos DB 쿼리 범위 지정 된 tooa 단일 컬렉션에 이미 있으므로 키워드는 hello 쿼리에서 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-223">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="fe012-224">따라서 "FROM Families f"를 "FROM root r" 또는 선택한 다른 변수 이름으로 교체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-224">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="fe012-225">Cosmos DB azure는 제품군, 루트 또는 hello 변수 이름을 선택한, 기본적으로 참조 hello 현재 컬렉션을 유추 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-225">Azure Cosmos DB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

## <span data-ttu-id="fe012-226"><a id="ReplaceDocument"></a>8단계: JSON 문서 바꾸기</span><span class="sxs-lookup"><span data-stu-id="fe012-226"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="fe012-227">Azure Cosmos DB는 JSON 문서 바꾸기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-227">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="fe012-228">복사 및 붙여넣기 hello **ReplaceFamilyDocument** 메서드 후 프로그램 **ExecuteSimpleQuery** 메서드.</span><span class="sxs-lookup"><span data-stu-id="fe012-228">Copy and paste hello **ReplaceFamilyDocument** method after your **ExecuteSimpleQuery** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

<span data-ttu-id="fe012-229">복사 및 붙여넣기 hello 다음 코드 tooyour **GetStartedDemo** hello 메서드 hello 끝나기 전에 hello 쿼리 실행 후 메서드.</span><span class="sxs-lookup"><span data-stu-id="fe012-229">Copy and paste hello following code tooyour **GetStartedDemo** method after hello query execution, at hello end of hello method.</span></span> <span data-ttu-id="fe012-230">Hello 문서를 바꾼 후가 실행 되어 hello 동일 tooview 변경 hello 문서 다시 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-230">After replacing hello document, this will run hello same query again tooview hello changed document.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART tooYOUR CODE
    // Update hello Grade of hello Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="fe012-231">키를 눌러 **F5** toorun 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-231">Press **F5** toorun your application.</span></span>

<span data-ttu-id="fe012-232">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-232">Congratulations!</span></span> <span data-ttu-id="fe012-233">Azure Cosmos DB 문서를 성공적으로 대체했습니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-233">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="fe012-234"><a id="DeleteDocument"></a>9단계: JSON 문서 삭제</span><span class="sxs-lookup"><span data-stu-id="fe012-234"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="fe012-235">Azure Cosmos DB는 JSON 문서 삭제를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-235">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="fe012-236">복사 및 붙여넣기 hello **DeleteFamilyDocument** 메서드 후 프로그램 **ReplaceFamilyDocument** 메서드.</span><span class="sxs-lookup"><span data-stu-id="fe012-236">Copy and paste hello **DeleteFamilyDocument** method after your **ReplaceFamilyDocument** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

<span data-ttu-id="fe012-237">복사 및 붙여넣기 hello 다음 코드 tooyour **GetStartedDemo** hello 두 번째 쿼리 실행 후 hello 메서드의 hello 끝 메서드.</span><span class="sxs-lookup"><span data-stu-id="fe012-237">Copy and paste hello following code tooyour **GetStartedDemo** method after hello second query execution, at hello end of hello method.</span></span>

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART tooCODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

<span data-ttu-id="fe012-238">키를 눌러 **F5** toorun 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-238">Press **F5** toorun your application.</span></span>

<span data-ttu-id="fe012-239">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-239">Congratulations!</span></span> <span data-ttu-id="fe012-240">Azure Cosmos DB 문서를 성공적으로 삭제했습니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-240">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="fe012-241"><a id="DeleteDatabase"></a>10 단계: hello 데이터베이스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-241"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="fe012-242">데이터베이스를 만들었습니다. 삭제 hello hello 데이터베이스와 모든 자식 리소스 (컬렉션, 문서 등)를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-242">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="fe012-243">복사 및 붙여넣기 hello 다음 코드 tooyour **GetStartedDemo** 메서드 hello 문서 후 toodelete hello에 대 한 전체 데이터베이스 및 모든 자식 리소스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-243">Copy and paste hello following code tooyour **GetStartedDemo** method after hello document delete toodelete hello entire database and all children resources.</span></span>

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART tooCODE
    // Clean up/delete hello database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

<span data-ttu-id="fe012-244">키를 눌러 **F5** toorun 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-244">Press **F5** toorun your application.</span></span>

<span data-ttu-id="fe012-245">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-245">Congratulations!</span></span> <span data-ttu-id="fe012-246">Azure Cosmos DB 데이터베이스를 성공적으로 삭제했습니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-246">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="fe012-247"><a id="Run"></a>11단계: C# 콘솔 응용 프로그램 모두 함께 실행</span><span class="sxs-lookup"><span data-stu-id="fe012-247"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="fe012-248">디버그 모드에서 Visual Studio toobuild hello 응용 프로그램에서 f5 키를 누르면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-248">Hit F5 in Visual Studio toobuild hello application in debug mode.</span></span>

<span data-ttu-id="fe012-249">콘솔 창에 get 시작된 응용 프로그램의 hello 출력을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-249">You should see hello output of your get started app in a console window.</span></span> <span data-ttu-id="fe012-250">hello 출력 hello hello 결과 보기는 쿼리를 추가 하 고 아래 예제에서는 텍스트 hello와 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-250">hello output will show hello results of hello queries we added and should match hello example text below.</span></span>

    Created FamilyDB
    Press any key toocontinue ...
    Created FamilyCollection
    Press any key toocontinue ...
    Created Family Andersen.1
    Press any key toocontinue ...
    Created Family Wakefield.7
    Press any key toocontinue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Replaced Family Andersen.1
    Press any key toocontinue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Deleted Family Andersen.1
    End of demo, press any key tooexit.

<span data-ttu-id="fe012-251">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-251">Congratulations!</span></span> <span data-ttu-id="fe012-252">Hello 자습서를 완료 하 고 C# 콘솔 응용 프로그램!</span><span class="sxs-lookup"><span data-stu-id="fe012-252">You've completed hello tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="fe012-253"><a id="GetSolution"></a>Hello 완료 자습서 솔루션 가져오기</span><span class="sxs-lookup"><span data-stu-id="fe012-253"><a id="GetSolution"></a> Get hello complete tutorial solution</span></span>
<span data-ttu-id="fe012-254">이 자습서에서는 또는 원하는 toodownload hello 코드 샘플만의 toocomplete hello 단계 하는 데 시간이 하지 않은 경우에서 가져올 수 있습니다 [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started)합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-254">If you didn't have time toocomplete hello steps in this tutorial, or just want toodownload hello code samples, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> 

<span data-ttu-id="fe012-255">toobuild hello GetStarted 솔루션 hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-255">toobuild hello GetStarted solution, you will need hello following:</span></span>

* <span data-ttu-id="fe012-256">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="fe012-256">An active Azure account.</span></span> <span data-ttu-id="fe012-257">계정이 없는 경우 [무료 계정](https://azure.microsoft.com/free/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-257">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="fe012-258">[Azure Cosmos DB 계정][cosmos-db-create-account].</span><span class="sxs-lookup"><span data-stu-id="fe012-258">An [Azure Cosmos DB account][cosmos-db-create-account].</span></span>
* <span data-ttu-id="fe012-259">hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) 솔루션 GitHub에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-259">hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="fe012-260">Visual Studio에서 Azure Cosmos DB.NET SDK toorestore hello 참조 toohello hello를 마우스 오른쪽 단추로 클릭 **GetStarted** 클릭 한 다음 솔루션 탐색기에서 솔루션 **NuGet 패키지 복원을 사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-260">toorestore hello references toohello Azure Cosmos DB .NET SDK in Visual Studio, right-click hello **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="fe012-261">다음으로 hello App.config 파일에서 값을 업데이트 hello EndpointUrl 및 AuthorizationKey에 설명 된 대로 [tooan Cosmos DB Azure 계정을 연결](#Connect)합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-261">Next, in hello App.config file, update hello EndpointUrl and AuthorizationKey values as described in [Connect tooan Azure Cosmos DB account](#Connect).</span></span>

<span data-ttu-id="fe012-262">정말 간단하죠? 빌드하고 원하는 대로 진행하세요!</span><span class="sxs-lookup"><span data-stu-id="fe012-262">That's it, build it and you're on your way!</span></span>


## <a name="next-steps"></a><span data-ttu-id="fe012-263">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fe012-263">Next steps</span></span>
* <span data-ttu-id="fe012-264">보다 복잡한 ASP.NET MVC 자습서가 필요하신가요?</span><span class="sxs-lookup"><span data-stu-id="fe012-264">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="fe012-265">[ASP.NET MVC 자습서: Azure Cosmos DB를 사용한 웹 응용 프로그램 개발](documentdb-dotnet-application.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe012-265">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="fe012-266">Tooperform 확장 및 성능 Azure Cosmos DB를 사용 하 여 테스트를 선택 하십시오.</span><span class="sxs-lookup"><span data-stu-id="fe012-266">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="fe012-267">[Azure Cosmos DB를 사용한 성능 및 규모 테스트](performance-testing.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe012-267">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="fe012-268">너무 방법에 대해 알아봅니다[Azure Cosmos DB 요청, 사용 및 저장소 모니터링](monitor-accounts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-268">Learn how too[monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="fe012-269">Hello에 우리의 샘플 데이터 집합에 대해 쿼리 실행 [Query Playground](https://www.documentdb.com/sql/demo)합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-269">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="fe012-270">Azure Cosmos DB에 대해 자세히 toolearn 참조 [tooAzure Cosmos DB 시작](https://docs.microsoft.com/azure/cosmos-db/introduction)합니다.</span><span class="sxs-lookup"><span data-stu-id="fe012-270">toolearn more about Azure Cosmos DB, see [Welcome tooAzure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-documentdb-dotnet.md#create-account
