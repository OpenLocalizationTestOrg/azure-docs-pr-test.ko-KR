---
title: "Azure Cosmos DB: DocumentDB API .NET Core 시작 자습서 | Microsoft Docs"
description: "Azure Cosmos DB DocumentDB API .NET Core SDK를 사용하여 온라인 데이터베이스 및 C# 콘솔 응용 프로그램을 만드는 자습서입니다."
services: cosmos-db
documentationcenter: .net
author: arramac
manager: jhubbard
editor: 
ms.assetid: 9f93e276-9936-4efb-a534-a9889fa7c7d2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 7536978bbb1e41b6484b66fd1b51c900fc3e545d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-getting-started-with-the-documentdb-api-and-net-core"></a><span data-ttu-id="6d958-103">Azure Cosmos DB: DocumentDB API 및 .NET Core 시작</span><span class="sxs-lookup"><span data-stu-id="6d958-103">Azure Cosmos DB: Getting started with the DocumentDB API and .NET Core</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6d958-104">.NET</span><span class="sxs-lookup"><span data-stu-id="6d958-104">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="6d958-105">.NET Core</span><span class="sxs-lookup"><span data-stu-id="6d958-105">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="6d958-106">MongoDB용 Node.js</span><span class="sxs-lookup"><span data-stu-id="6d958-106">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="6d958-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="6d958-107">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="6d958-108">Java</span><span class="sxs-lookup"><span data-stu-id="6d958-108">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="6d958-109">C++</span><span class="sxs-lookup"><span data-stu-id="6d958-109">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="6d958-110">.NET Core 자습서부터 시작하여 Azure Cosmos DB용 DocumentDB API를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-110">Welcome to the DocumentDB API for Azure Cosmos DB getting started with .NET Core tutorial!</span></span> <span data-ttu-id="6d958-111">이 자습서를 따라 하면 Azure Cosmos DB 리소스를 만들고 쿼리하는 콘솔 응용 프로그램이 생깁니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-111">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="6d958-112">다음에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-112">We'll cover:</span></span>

* <span data-ttu-id="6d958-113">Azure Cosmos DB 계정 만들기 및 연결</span><span class="sxs-lookup"><span data-stu-id="6d958-113">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="6d958-114">Visual Studio 솔루션 구성</span><span class="sxs-lookup"><span data-stu-id="6d958-114">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="6d958-115">온라인 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="6d958-115">Creating an online database</span></span>
* <span data-ttu-id="6d958-116">컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="6d958-116">Creating a collection</span></span>
* <span data-ttu-id="6d958-117">JSON 문서 만들기</span><span class="sxs-lookup"><span data-stu-id="6d958-117">Creating JSON documents</span></span>
* <span data-ttu-id="6d958-118">컬렉션 쿼리</span><span class="sxs-lookup"><span data-stu-id="6d958-118">Querying the collection</span></span>
* <span data-ttu-id="6d958-119">문서 바꾸기</span><span class="sxs-lookup"><span data-stu-id="6d958-119">Replacing a document</span></span>
* <span data-ttu-id="6d958-120">문서 삭제</span><span class="sxs-lookup"><span data-stu-id="6d958-120">Deleting a document</span></span>
* <span data-ttu-id="6d958-121">데이터베이스 삭제</span><span class="sxs-lookup"><span data-stu-id="6d958-121">Deleting the database</span></span>

<span data-ttu-id="6d958-122">시간이 없으십니까?</span><span class="sxs-lookup"><span data-stu-id="6d958-122">Don't have time?</span></span> <span data-ttu-id="6d958-123">염려하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="6d958-123">Don't worry!</span></span> <span data-ttu-id="6d958-124">[GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started)에서 전체 솔루션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-124">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span> <span data-ttu-id="6d958-125">빠른 지침을 보려면 [전체 솔루션 다운로드 섹션](#GetSolution) 으로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="6d958-125">Jump to the [Get the complete solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="6d958-126">DocumentDB API 및 .NET Core SDK를 사용하여 Xamarin iOS, Android 또는 Forms 응용 프로그램을 빌드하시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="6d958-126">Want to build a Xamarin iOS, Android, or Forms application using the DocumentDB API and .NET Core SDK?</span></span> <span data-ttu-id="6d958-127">[Xamarin 및 Azure Cosmos DB를 사용하여 모바일 응용 프로그램 빌드](mobile-apps-with-xamarin.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d958-127">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6d958-128">이 자습서에서 사용되는 Azure Cosmos DB .NET Core SDK는 UWP(유니버설 Windows 플랫폼) 앱과 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-128">The Azure Cosmos DB .NET Core SDK used in this tutorial is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="6d958-129">UWP 앱을 지원하는 .NET Core SDK의 미리 보기 버전은 [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com)(으)로 전자 메일을 보내세요.</span><span class="sxs-lookup"><span data-stu-id="6d958-129">For a preview version of the .NET Core SDK that does support UWP apps, send email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

<span data-ttu-id="6d958-130">이제 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-130">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d958-131">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6d958-131">Prerequisites</span></span>
<span data-ttu-id="6d958-132">다음 항목이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-132">Please make sure you have the following:</span></span>

* <span data-ttu-id="6d958-133">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="6d958-133">An active Azure account.</span></span> <span data-ttu-id="6d958-134">계정이 없는 경우 [무료 계정](https://azure.microsoft.com/free/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-134">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="6d958-135">또는 이 자습서에 [Azure Cosmos DB 에뮬레이터](local-emulator.md)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-135">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="6d958-136">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="6d958-136">Visual Studio 2017</span></span>](https://www.visualstudio.com/vs/) 
    * <span data-ttu-id="6d958-137">MacOS 또는 Linux에서 작업하는 경우 원하는 플랫폼에 대한 [.NET Core SDK](https://www.microsoft.com/net/core#macos)를 설치하여 명령줄에서 .NET Core 앱을 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-137">If you're working on MacOS or Linux, you can develop .NET Core apps from the command-line by installing the [.NET Core SDK](https://www.microsoft.com/net/core#macos) for the platform of your choice.</span></span> 
    * <span data-ttu-id="6d958-138">Windows에서 작업하는 경우 [.NET Core SDK](https://www.microsoft.com/net/core#windows)를 설치하여 명령줄에서 .NET Core 앱을 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-138">If you're working on Windows, you can develop .NET Core apps from the command-line by installing the [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span></span> 
    * <span data-ttu-id="6d958-139">자체 편집기를 사용하거나 Windows, Linux, MacOS에서 작동하는 무료 [Visual Studio Code](https://code.visualstudio.com/)를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-139">You can use your own editor, or download [Visual Studio Code](https://code.visualstudio.com/) which is free and works on Windows, Linux, and MacOS.</span></span> 

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="6d958-140">1단계: Azure Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="6d958-140">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="6d958-141">Azure Cosmos DB 계정을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-141">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="6d958-142">계정이 이미 있는 경우 [Visual Studio 솔루션 설치](#SetupVS)로 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-142">If you already have an account you want to use, you can skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="6d958-143">Azure Cosmos DB 에뮬레이터를 사용하는 경우 [Azure Cosmos DB 에뮬레이터](local-emulator.md)의 단계에 따라 에뮬레이터를 설치하고 [Visual Studio 솔루션 설치](#SetupVS)로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-143">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="6d958-144"><a id="SetupVS"></a>2단계: Visual Studio 솔루션 설치</span><span class="sxs-lookup"><span data-stu-id="6d958-144"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="6d958-145">컴퓨터에서 **Visual Studio 2017**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-145">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="6d958-146">**파일** 메뉴에서 **새로 만들기**와 **프로젝트**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-146">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="6d958-147">**새 프로젝트** 대화 상자에서 **템플릿** / **Visual C#** / **.NET Core**/**콘솔 응용 프로그램(.NET Core)**을 선택하고 프로젝트 이름을 **DocumentDBGettingStarted**라고 지정한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-147">In the **New Project** dialog, select **Templates** / **Visual C#** / **.NET Core**/**Console Application (.NET Core)**, name your project **DocumentDBGettingStarted**, and then click **OK**.</span></span>

   ![새 프로젝트 창의 스크린샷](./media/documentdb-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. <span data-ttu-id="6d958-149">**솔루션 탐색기**에서 **DocumentDBGettingStarted**를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-149">In the **Solution Explorer**, right click on **DocumentDBGettingStarted**.</span></span>
5. <span data-ttu-id="6d958-150">그런 다음 메뉴를 벗어나지 않은 상태에서 **NuGet 패키지 관리...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-150">Then without leaving the menu, click on **Manage NuGet Packages...**.</span></span>

   ![프로젝트의 마우스 오른쪽 단추 클릭 메뉴의 스크린샷](./media/documentdb-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. <span data-ttu-id="6d958-152">**NuGet** 탭에서 창의 맨 위에 있는 **찾아보기**를 클릭하고 검색 상자에 **azure documentdb**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-152">In the **NuGet** tab, click **Browse** at the top of the window, and type **azure documentdb** in the search box.</span></span>
7. <span data-ttu-id="6d958-153">결과 내에서 **Microsoft.Azure.DocumentDB.Core**를 찾아 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-153">Within the results, find **Microsoft.Azure.DocumentDB.Core** and click **Install**.</span></span>
   <span data-ttu-id="6d958-154">.NET Core용 DocumentDB 클라이언트 라이브러리의 패키지 ID는 [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core)입니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-154">The package ID for the DocumentDB Client Library for .NET Core is [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span></span> <span data-ttu-id="6d958-155">이 .NET Core NuGet 패키지에서 지원되지 않는 .NET Framework 버전(예: net461)을 대상으로 하는 경우 .NET Framework 4.5 이후의 모든 .NET Framework 버전을 지원하는 [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-155">If you are targeting a .NET Framework version (like net461) that is not supported by this .NET Core NuGet package, then use [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) that supports all .NET Framework versions starting .NET Framework 4.5.</span></span>
8. <span data-ttu-id="6d958-156">프롬프트가 표시되면 NuGet 패키지 설치를 수락하고 사용권 계약에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-156">At the prompts, accept the NuGet package installations and the license agreement.</span></span>

<span data-ttu-id="6d958-157">잘하셨습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-157">Great!</span></span> <span data-ttu-id="6d958-158">설치를 완료했으므로 코드를 작성해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-158">Now that we finished the setup, let's start writing some code.</span></span> <span data-ttu-id="6d958-159">[GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started)에서 이 자습서의 완성된 코드 프로젝트를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-159">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span>

## <span data-ttu-id="6d958-160"><a id="Connect"></a>3단계: Azure Cosmos DB 계정에 연결</span><span class="sxs-lookup"><span data-stu-id="6d958-160"><a id="Connect"></a>Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="6d958-161">먼저 Program.cs에서 C# 응용 프로그램의 시작 부분에 다음 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-161">First, add these references to the beginning of your C# application, in the Program.cs file:</span></span>

```csharp
using System;

// ADD THIS PART TO YOUR CODE
using System.Linq;
using System.Threading.Tasks;
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

> [!IMPORTANT]
> <span data-ttu-id="6d958-162">이 자습서를 완료하려면 위의 종속성을 추가했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-162">In order to complete this tutorial, make sure you add the dependencies above.</span></span>

<span data-ttu-id="6d958-163">이제, 두 가지 상수와 *클라이언트* 변수를 공용 클래스 *프로그램* 아래에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-163">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

```csharp
class Program
{
    // ADD THIS PART TO YOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

<span data-ttu-id="6d958-164">다음으로 [Azure Portal](https://portal.azure.com)로 이동하여 URI 및 기본 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-164">Next, head to the [Azure Portal](https://portal.azure.com) to retrieve your URI and primary key.</span></span> <span data-ttu-id="6d958-165">Azure Cosmos DB URI와 기본 키는 응용 프로그램에서 연결할 위치를 식별하고 Azure Cosmos DB에서 응용 프로그램의 연결을 신뢰하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-165">The Azure Cosmos DB URI and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="6d958-166">Azure Portal에서 Azure Cosmos DB 계정으로 이동한 다음 **키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-166">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="6d958-167">포털에서 URI를 복사하고 program.cs 파일의 `<your endpoint URI>` 에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-167">Copy the URI from the portal and paste it into `<your endpoint URI>` in the program.cs file.</span></span> <span data-ttu-id="6d958-168">그런 다음 포털에서 기본 키를 복사하고 `<your key>`에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-168">Then copy the PRIMARY KEY from the portal and paste it into `<your key>`.</span></span> <span data-ttu-id="6d958-169">Azure Cosmos DB 에뮬레이터를 사용하는 경우 끝점으로 `https://localhost:8081`과, [Azure Cosmos DB 에뮬레이터를 사용한 개발 방법](local-emulator.md)에서 잘 정의된 권한 부여 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-169">If you are using the Azure Cosmos DB Emulator, use `https://localhost:8081` as the endpoint, and the well-defined authorization key from [How to develop using the Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="6d958-170">< 및 >를 반드시 제거하고 끝점 및 키를 묶은 큰따옴표는 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-170">Make sure to remove the < and > but leave the double quotes around your endpoint and key.</span></span>

![C# 콘솔 응용 프로그램을 만들기 위해 NoSQL 자습서에서 사용하는 Azure Portal의 스크린샷][keys]

<span data-ttu-id="6d958-173">**DocumentClient**의 새 인스턴스를 만드는 것으로 시작 응용 프로그램을 시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-173">We'll start the getting started application by creating a new instance of the **DocumentClient**.</span></span>

<span data-ttu-id="6d958-174">**Main** 메서드 아래에 **GetStartedDemo**라는 이름의 새 비동기 작업을 추가하면, 새 **DocumentClient**가 인스턴스화됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-174">Below the **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

```csharp
static void Main(string[] args)
{
}

// ADD THIS PART TO YOUR CODE
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);
}
```

<span data-ttu-id="6d958-175">다음 코드를 추가하여 **Main** 메서드에서 비동기 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-175">Add the following code to run your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="6d958-176">**Main** 메서드가 예외를 catch하여 콘솔에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-176">The **Main** method will catch exceptions and write them to the console.</span></span>

```csharp
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
```

<span data-ttu-id="6d958-177">**DocumentDBGettingStarted** 단추를 클릭하여 응용 프로그램을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-177">Press the **DocumentDBGettingStarted** button to build and run the application.</span></span>

<span data-ttu-id="6d958-178">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-178">Congratulations!</span></span> <span data-ttu-id="6d958-179">Azure Cosmos DB 계정에 성공적으로 연결되었으므로 Azure Cosmos DB 리소스 작업에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-179">You have successfully connected to an Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="6d958-180">4단계: 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="6d958-180">Step 4: Create a database</span></span>
<span data-ttu-id="6d958-181">데이터베이스 생성을 위한 코드를 추가하기 전에, 콘솔에 쓰기 위한 도우미 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-181">Before you add the code for creating a database, add a helper method for writing to the console.</span></span>

<span data-ttu-id="6d958-182">**GetStartedDemo** 메서드에 **WriteToConsoleAndPromptToContinue** 메서드를 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-182">Copy and paste the **WriteToConsoleAndPromptToContinue** method underneath the **GetStartedDemo** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
}
```

<span data-ttu-id="6d958-183">**DocumentClient** 클래스의 [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) 메서드를 사용하여 Azure Cosmos DB [데이터베이스](documentdb-resources.md#databases)를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-183">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using the [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="6d958-184">데이터베이스는 여러 컬렉션으로 분할된 JSON 문서 저장소의 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-184">A database is the logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="6d958-185">클라이언트 생성의 **GetStartedDemo** 메서드에 다음 코드를 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-185">Copy and paste the following code to your **GetStartedDemo** method underneath the client creation.</span></span> <span data-ttu-id="6d958-186">*FamilyDB*라는 데이터베이스가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-186">This will create a database named *FamilyDB*.</span></span>

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART TO YOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

<span data-ttu-id="6d958-187">**DocumentDBGettingStarted** 단추를 클릭하여 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-187">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="6d958-188">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-188">Congratulations!</span></span> <span data-ttu-id="6d958-189">Azure Cosmos DB 데이터베이스를 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-189">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="6d958-190"><a id="CreateColl"></a>5단계: 컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="6d958-190"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="6d958-191">**CreateDocumentCollectionAsync** 는 가격 책정 의미가 포함된 예약된 처리량이 있는 새 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-191">**CreateDocumentCollectionAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="6d958-192">자세한 내용은 [가격 페이지](https://azure.microsoft.com/pricing/details/cosmos-db/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d958-192">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>

<span data-ttu-id="6d958-193">**DocumentClient** 클래스의 [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) 메서드를 사용하여 [컬렉션](documentdb-resources.md#collections)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-193">A [collection](documentdb-resources.md#collections) can be created by using the [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="6d958-194">컬렉션은 JSON 문서 및 관련 JavaScript 응용 프로그램 논리의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-194">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="6d958-195">데이터베이스 생성의 **GetStartedDemo** 메서드에 다음 코드를 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-195">Copy and paste the following code to your **GetStartedDemo** method underneath the database creation.</span></span> <span data-ttu-id="6d958-196">*FamilyCollection_oa*라는 문서 컬렉션이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-196">This will create a document collection named *FamilyCollection_oa*.</span></span>

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART TO YOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

<span data-ttu-id="6d958-197">**DocumentDBGettingStarted** 단추를 클릭하여 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-197">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="6d958-198">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-198">Congratulations!</span></span> <span data-ttu-id="6d958-199">Azure Cosmos DB 데이터베이스 컬렉션을 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-199">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="6d958-200"><a id="CreateDoc"></a>6단계: JSON 문서 만들기</span><span class="sxs-lookup"><span data-stu-id="6d958-200"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="6d958-201">**DocumentClient** 클래스의 [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) 메서드를 사용하여 [문서](documentdb-resources.md#documents)를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-201">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="6d958-202">문서는 사용자 정의(임의) JSON 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-202">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="6d958-203">이제 하나 이상의 문서를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-203">We can now insert one or more documents.</span></span> <span data-ttu-id="6d958-204">데이터베이스에 저장하려는 데이터가 이미 있다면 Azure Cosmos DB의 [데이터 마이그레이션 도구](import-data.md)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-204">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md).</span></span>

<span data-ttu-id="6d958-205">먼저 이 샘플에서는 Azure Cosmos DB 내에 저장된 개체를 나타내는 **가족** 클래스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-205">First, we need to create a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="6d958-206">또한 **가족** 내에서 사용되는 **부모**, **자식**, **애완 동물**, **주소** 하위 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-206">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="6d958-207">문서에는 JSON에서 **ID**로 직렬화된 **ID** 속성이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-207">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="6d958-208">**GetStartedDemo** 메서드 다음에 다음 내부 하위 클래스를 추가하여 이러한 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-208">Create these classes by adding the following internal sub-classes after the **GetStartedDemo** method.</span></span>

<span data-ttu-id="6d958-209">**WriteToConsoleAndPromptToContinue** 메서드에 **가족**, **부모**, **자식**, **애완 동물** 및 **주소** 클래스를 복사하여 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-209">Copy and paste the **Family**, **Parent**, **Child**, **Pet**, and **Address** classes underneath the **WriteToConsoleAndPromptToContinue** method.</span></span>

```csharp
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
```

<span data-ttu-id="6d958-210">**CreateDocumentCollectionIfNotExists** 메서드에 **CreateFamilyDocumentIfNotExists** 메서드를 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-210">Copy and paste the **CreateFamilyDocumentIfNotExists** method underneath your **CreateDocumentCollectionIfNotExists** method.</span></span>

```csharp
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
```

<span data-ttu-id="6d958-211">그리고 Andersen Family와 Wakefield Family의 문서 하나씩 두 개의 문서를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-211">And insert two documents, one each for the Andersen Family and the Wakefield Family.</span></span>

<span data-ttu-id="6d958-212">문서 컬렉션 생성 아래에서 **GetStartedDemo** 메서드에 `// ADD THIS PART TO YOUR CODE` 다음에 코드를 복사하고 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-212">Copy and paste the code that follows `// ADD THIS PART TO YOUR CODE` to your **GetStartedDemo** method underneath the document collection creation.</span></span>

```csharp
await this.CreateDatabaseIfNotExists("FamilyDB_oa");

await this.CreateDocumentCollectionIfNotExists("FamilyDB_oa", "FamilyCollection_oa");

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

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", andersenFamily);

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

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);
```

<span data-ttu-id="6d958-213">**DocumentDBGettingStarted** 단추를 클릭하여 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-213">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="6d958-214">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-214">Congratulations!</span></span> <span data-ttu-id="6d958-215">두 개의 Azure Cosmos DB 문서를 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-215">You have successfully created two Azure Cosmos DB documents.</span></span>  

![NoSQL에서 C# 콘솔 응용 프로그램을 만들기 위해 사용한 계정, 데이터베이스, 컬렉션 및 문서 간의 계층 관계를 보여 주는 다이어그램](./media/documentdb-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="6d958-217"><a id="Query"></a>7단계: Azure Cosmos DB 리소스 쿼리</span><span class="sxs-lookup"><span data-stu-id="6d958-217"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="6d958-218">Azure Cosmos DB는 각 컬렉션에 저장된 JSON 문서에 대해 [다양한 쿼리](documentdb-sql-query.md)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-218">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="6d958-219">다음 샘플 코드는 Azure Cosmos DB SQL 구문뿐 아니라 LINQ를 사용하는 다양한 쿼리를 보여 줍니다. 이러한 쿼리는 이전 단계에서 삽입한 문서에 대해 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-219">The following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against the documents we inserted in the previous step.</span></span>

<span data-ttu-id="6d958-220">**CreateFamilyDocumentIfNotExists** 메서드에 **ExecuteSimpleQuery** 메서드를 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-220">Copy and paste the **ExecuteSimpleQuery** method underneath your **CreateFamilyDocumentIfNotExists** method.</span></span>

```csharp
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
```

<span data-ttu-id="6d958-221">두 번째 문서 생성의 **GetStartedDemo** 메서드에 다음 코드를 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-221">Copy and paste the following code to your **GetStartedDemo** method underneath the second document creation.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART TO YOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="6d958-222">**DocumentDBGettingStarted** 단추를 클릭하여 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-222">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="6d958-223">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-223">Congratulations!</span></span> <span data-ttu-id="6d958-224">Azure Cosmos DB 컬렉션에 대한 쿼리가 성공적으로 수행되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-224">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="6d958-225">다음 다이어그램에서는 만든 컬렉션에 대해 Azure Cosmos DB SQL 쿼리 구문을 호출하는 방법을 보여 주며, 마찬가지로 동일한 논리가 LINQ 쿼리에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-225">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created, and the same logic applies to the LINQ query as well.</span></span>

![NoSQL에서 C# 콘솔 응용 프로그램을 만들기 위해 사용한 쿼리의 의미와 범위를 보여 주는 다이어그램](./media/documentdb-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="6d958-227">Azure Cosmos DB 쿼리는 이미 단일 컬렉션으로 범위가 지정되었기 때문에 [FROM](documentdb-sql-query.md#FromClause) 키워드는 쿼리에서 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-227">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span></span> <span data-ttu-id="6d958-228">따라서 "FROM Families f"를 "FROM root r" 또는 선택한 다른 변수 이름으로 교체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-228">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="6d958-229">DocumentDB는 패밀리, 루트 또는 선택한 변수 이름이 기본적으로 현재 컬렉션을 참조하는 것으로 유추합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-229">DocumentDB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

## <span data-ttu-id="6d958-230"><a id="ReplaceDocument"></a>8단계: JSON 문서 바꾸기</span><span class="sxs-lookup"><span data-stu-id="6d958-230"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="6d958-231">Azure Cosmos DB는 JSON 문서 바꾸기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-231">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="6d958-232">**ExecuteSimpleQuery** 메서드에 **ReplaceFamilyDocument** 메서드를 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-232">Copy and paste the **ReplaceFamilyDocument** method underneath your **ExecuteSimpleQuery** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
{
    try
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
        this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

<span data-ttu-id="6d958-233">쿼리 실행의 **GetStartedDemo** 메서드에 다음 코드를 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-233">Copy and paste the following code to your **GetStartedDemo** method underneath the query execution.</span></span> <span data-ttu-id="6d958-234">문서를 바꾼 후에, 변경된 문서를 표시하도록 같은 쿼리가 다시 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-234">After replacing the document, this will run the same query again to view the changed document.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO YOUR CODE
// Update the Grade of the Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="6d958-235">**DocumentDBGettingStarted** 단추를 클릭하여 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-235">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="6d958-236">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-236">Congratulations!</span></span> <span data-ttu-id="6d958-237">Azure Cosmos DB 문서를 성공적으로 대체했습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-237">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="6d958-238"><a id="DeleteDocument"></a>9단계: JSON 문서 삭제</span><span class="sxs-lookup"><span data-stu-id="6d958-238"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="6d958-239">Azure Cosmos DB는 JSON 문서 삭제를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-239">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="6d958-240">**ReplaceFamilyDocument** 메서드에 **DeleteFamilyDocument** 메서드를 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-240">Copy and paste the **DeleteFamilyDocument** method underneath your **ReplaceFamilyDocument** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
{
    try
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
        Console.WriteLine("Deleted Family {0}", documentName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

<span data-ttu-id="6d958-241">두 번째 쿼리 실행의 **GetStartedDemo** 메서드에 다음 코드를 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-241">Copy and paste the following code to your **GetStartedDemo** method underneath the second query execution.</span></span>

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO CODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

<span data-ttu-id="6d958-242">**DocumentDBGettingStarted** 단추를 클릭하여 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-242">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="6d958-243">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-243">Congratulations!</span></span> <span data-ttu-id="6d958-244">Azure Cosmos DB 문서를 성공적으로 삭제했습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-244">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="6d958-245"><a id="DeleteDatabase"></a>10단계: 데이터베이스 삭제</span><span class="sxs-lookup"><span data-stu-id="6d958-245"><a id="DeleteDatabase"></a>Step 10: Delete the database</span></span>
<span data-ttu-id="6d958-246">만든 데이터베이스를 삭제하면 데이터베이스와 모든 자식 리소스(컬렉션, 문서 등)가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-246">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="6d958-247">전체 데이터베이스와 모든 자식 리소스를 삭제하기 위해 문서 삭제의 **GetStartedDemo** 메서드에 다음 코드를 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-247">Copy and paste the following code to your **GetStartedDemo** method underneath the document delete to delete the entire database and all children resources.</span></span>

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART TO CODE
// Clean up/delete the database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

<span data-ttu-id="6d958-248">**DocumentDBGettingStarted** 단추를 클릭하여 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-248">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="6d958-249">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-249">Congratulations!</span></span> <span data-ttu-id="6d958-250">Azure Cosmos DB 데이터베이스를 성공적으로 삭제했습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-250">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="6d958-251"><a id="Run"></a>11단계: C# 콘솔 응용 프로그램 모두 함께 실행</span><span class="sxs-lookup"><span data-stu-id="6d958-251"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="6d958-252">Visual Studio에서 **DocumentDBGettingStarted** 단추를 클릭하여 디버그 모드에서 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-252">Press the **DocumentDBGettingStarted** button in Visual Studio to build the application in debug mode.</span></span>

<span data-ttu-id="6d958-253">시작한 앱의 출력이 콘솔 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-253">You should see the output of your get started app in the console window.</span></span> <span data-ttu-id="6d958-254">출력은 추가한 쿼리 결과를 보여 주며, 아래 예제 텍스트와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-254">The output will show the results of the queries we added and should match the example text below.</span></span>

```
Created FamilyDB_oa
Press any key to continue ...
Created FamilyCollection_oa
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
```

<span data-ttu-id="6d958-255">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-255">Congratulations!</span></span> <span data-ttu-id="6d958-256">이 자습서를 완료했으며 실행되는 C# 콘솔 응용 프로그램이 생겼습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-256">You've completed the tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="6d958-257"><a id="GetSolution"></a> 전체 자습서 솔루션 가져오기</span><span class="sxs-lookup"><span data-stu-id="6d958-257"><a id="GetSolution"></a> Get the complete tutorial solution</span></span>
<span data-ttu-id="6d958-258">이 문서의 모든 샘플을 포함하는 GetStarted 솔루션을 빌드하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-258">To build the GetStarted solution that contains all the samples in this article, you will need the following:</span></span>

* <span data-ttu-id="6d958-259">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="6d958-259">An active Azure account.</span></span> <span data-ttu-id="6d958-260">계정이 없는 경우 [무료 계정](https://azure.microsoft.com/free/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-260">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="6d958-261">[Azure Cosmos DB 계정][create-documentdb-dotnet.md#create-account].</span><span class="sxs-lookup"><span data-stu-id="6d958-261">An [Azure Cosmos DB account][create-documentdb-dotnet.md#create-account].</span></span>
* <span data-ttu-id="6d958-262">GitHub에서 제공하는 [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) 솔루션</span><span class="sxs-lookup"><span data-stu-id="6d958-262">The [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="6d958-263">Visual Studio에서 Azure Cosmos DB .NET Core SDK용 DocumentDB API 참조를 복원하려면 솔루션 탐색기에서 **GetStarted** 솔루션을 마우스 오른쪽 단추로 클릭한 다음 **NuGet 패키지 복원 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-263">To restore the references to the DocumentDB API for Azure Cosmos DB .NET Core SDK in Visual Studio, right-click the **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="6d958-264">다음으로, Program.cs 파일에서 EndpointUrl 및 AuthorizationKey 값을 [Azure Cosmos DB 계정에 연결](#Connect)에 설명된 대로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-264">Next, in the Program.cs file, update the EndpointUrl and AuthorizationKey values as described in [Connect to an Azure Cosmos DB account](#Connect).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d958-265">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6d958-265">Next steps</span></span>
* <span data-ttu-id="6d958-266">보다 복잡한 ASP.NET MVC 자습서가 필요하신가요?</span><span class="sxs-lookup"><span data-stu-id="6d958-266">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="6d958-267">[ASP.NET MVC 자습서: Azure Cosmos DB를 사용한 웹 응용 프로그램 개발](documentdb-dotnet-application.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d958-267">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="6d958-268">Azure Cosmos DB .NET Core SDK용 DocumentDB API를 사용하여 Xamarin iOS, Android 또는 Forms 응용 프로그램을 개발하시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="6d958-268">Want to develop a Xamarin iOS, Android, or Forms application using the DocumentDB API for Azure Cosmos DB .NET Core SDK?</span></span> <span data-ttu-id="6d958-269">[Xamarin 및 Azure Cosmos DB를 사용하여 모바일 응용 프로그램 빌드](mobile-apps-with-xamarin.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d958-269">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>
* <span data-ttu-id="6d958-270">Azure Cosmos DB를 사용하여 규모 및 성능 테스트를 수행하고 싶으신가요?</span><span class="sxs-lookup"><span data-stu-id="6d958-270">Want to perform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="6d958-271">[Azure Cosmos DB를 사용한 성능 및 규모 테스트](performance-testing.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d958-271">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="6d958-272">[Azure Cosmos DB 요청, 사용 및 저장소 모니터링](monitor-accounts.md) 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="6d958-272">Learn how to [Monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="6d958-273">[쿼리 실습](https://www.documentdb.com/sql/demo)의 샘플 데이터 집합에 대해 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d958-273">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="6d958-274">프로그래밍 모델에 대한 자세히 알아보려면 [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d958-274">To learn more about the programming model, see [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

[create-documentdb-dotnet.md#create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-dotnetcore-get-started/nosql-tutorial-keys.png
