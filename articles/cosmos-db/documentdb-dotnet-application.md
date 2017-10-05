---
title: "Azure Cosmos DB용 ASP.NET MVC 자습서: 웹 응용 프로그램 개발 | Microsoft Docs"
description: "Azure Cosmos DB를 사용하여 MVC 웹 응용 프로그램을 만드는 ASP.NET MVC 자습서 JSON을 저장하고 Azure Websites - ASP NET MVC 단계별 자습서에서 호스팅하는 todo 앱에서 데이터에 액세스합니다."
keywords: "ASP.NET MVC 자습서, 웹 응용 프로그램 개발, MVC 웹 응용 프로그램, ASP NET MVC 단계별 자습서"
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 52532d89-a40e-4fdf-9b38-aadb3a4cccbc
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: mimig
ms.openlocfilehash: 3f2950fe25feb8f3ee81cc0a79bf624f0ee33bd5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <span data-ttu-id="3f071-105"><a name="_Toc395809351"></a>ASP.NET MVC 자습서: Azure Cosmos DB를 사용한 웹 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="3f071-105"><a name="_Toc395809351"></a>ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3f071-106">.NET</span><span class="sxs-lookup"><span data-stu-id="3f071-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="3f071-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="3f071-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="3f071-108">Java</span><span class="sxs-lookup"><span data-stu-id="3f071-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="3f071-109">Python</span><span class="sxs-lookup"><span data-stu-id="3f071-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="3f071-110">Azure Cosmos DB를 효율적으로 활용하여 JSON 문서를 저장 및 쿼리할 수 있는 방법을 강조하기 위해 이 문서에서는 Azure Cosmos DB를 사용하여 todo 앱을 빌드하는 방법을 보여 주는 종합적인 연습을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-110">To highlight how you can efficiently leverage Azure Cosmos DB to store and query JSON documents, this article provides an end-to-end walk-through showing you how to build a todo app using Azure Cosmos DB.</span></span> <span data-ttu-id="3f071-111">작업은 Azure Cosmos DB에 JSON 문서로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-111">The tasks will be stored as JSON documents in Azure Cosmos DB.</span></span>

![이 자습서에서 만든 할 일 모음 MVC 웹 응용 프로그램의 스크린샷 - ASP NET MVC 단계별 자습서](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

<span data-ttu-id="3f071-113">이 연습에서는 Azure Cosmos DB 서비스를 사용하여 Azure에서 호스트되는 ASP.NET MVC 웹 응용 프로그램의 데이터를 저장하고 액세스하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-113">This walk-through shows you how to use the Azure Cosmos DB service to store and access data from an ASP.NET MVC web application hosted on Azure.</span></span> <span data-ttu-id="3f071-114">ASP.NET MVC 구성 요소가 아닌 Azure Cosmos DB에만 집중하는 자습서를 찾는 경우 [Azure Cosmos DB C# 콘솔 응용 프로그램 빌드](documentdb-get-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f071-114">If you're looking for a tutorial that focuses only on Azure Cosmos DB, and not the ASP.NET MVC components, see [Build an Azure Cosmos DB C# console application](documentdb-get-started.md).</span></span>

> [!TIP]
> <span data-ttu-id="3f071-115">이 자습서에서는 이전에 ASP.NET MVC 및 Azure Websites를 사용해 본 경험이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-115">This tutorial assumes that you have prior experience using ASP.NET MVC and Azure Websites.</span></span> <span data-ttu-id="3f071-116">ASP.NET 또는 [필수 도구](#_Toc395637760)를 처음 사용하는 경우 [GitHub][GitHub]에서 전체 샘플 프로젝트를 다운로드하고 이 샘플의 지침을 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-116">If you are new to ASP.NET or the [prerequisite tools](#_Toc395637760), we recommend downloading the complete sample project from [GitHub][GitHub] and following the instructions in this sample.</span></span> <span data-ttu-id="3f071-117">프로젝트를 빌드하고 나면 이 문서를 검토하여 프로젝트의 컨텍스트에서 코드를 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-117">Once you have it built, you can review this article to gain insight on the code in the context of the project.</span></span>
> 
> 

## <span data-ttu-id="3f071-118"><a name="_Toc395637760"></a>이 데이터베이스 자습서의 필수 조건</span><span class="sxs-lookup"><span data-stu-id="3f071-118"><a name="_Toc395637760"></a>Prerequisites for this database tutorial</span></span>
<span data-ttu-id="3f071-119">이 문서의 지침을 따르기 전에 다음이 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-119">Before following the instructions in this article, you should ensure that you have the following:</span></span>

* <span data-ttu-id="3f071-120">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="3f071-120">An active Azure account.</span></span> <span data-ttu-id="3f071-121">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="3f071-122">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f071-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

    <span data-ttu-id="3f071-123">또는</span><span class="sxs-lookup"><span data-stu-id="3f071-123">OR</span></span>

    <span data-ttu-id="3f071-124">[Azure Cosmos DB 에뮬레이터](local-emulator.md)의 로컬 설치</span><span class="sxs-lookup"><span data-stu-id="3f071-124">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="3f071-125">[Visual Studio 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="3f071-125">[Visual Studio 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="3f071-126">Microsoft Azure SDK for .NET for Visual Studio 2017, Visual Studio 설치 관리자를 통해 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-126">Microsoft Azure SDK for .NET for Visual Studio 2017, available through the Visual Studio Installer.</span></span>

<span data-ttu-id="3f071-127">이 문서의 모든 스크린 샷은 Microsoft Visual Studio Community 2017을 사용하여 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-127">All the screen shots in this article have been taken using Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="3f071-128">시스템이 다른 버전으로 구성된 경우 화면과 옵션이 일부 달라질 수 있지만 위의 필수 구성 요소를 충족하면 솔루션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-128">If your system is configured with a different version it is possible that your screens and options won't match entirely, but if you meet the above prerequisites this solution should work.</span></span>

## <span data-ttu-id="3f071-129"><a name="_Toc395637761"></a>1단계: Azure Cosmos DB 데이터베이스 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="3f071-129"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="3f071-130">Azure Cosmos DB 계정을 만들어 시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-130">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="3f071-131">Azure Cosmos DB용 SQL(DocumentDB) 계정이 이미 있거나 이 자습서에 Azure Cosmos DB 에뮬레이터를 사용하고 있는 경우 [새 ASP.NET MVC 응용 프로그램 만들기](#_Toc395637762)로 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-131">If you already have a SQL (DocumentDB) account for Azure Cosmos DB or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Create a new ASP.NET MVC application](#_Toc395637762).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
<span data-ttu-id="3f071-132">이제 새 ASP.NET MVC 응용 프로그램을 처음부터 만드는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-132">We will now walk through how to create a new ASP.NET MVC application from the ground-up.</span></span> 

## <span data-ttu-id="3f071-133"><a name="_Toc395637762"></a>2단계: 새 ASP.NET MVC 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="3f071-133"><a name="_Toc395637762"></a>Step 2: Create a new ASP.NET MVC application</span></span>

1. <span data-ttu-id="3f071-134">Visual Studio의 **파일** 메뉴에서 **새로 만들기**를 가리킨 후 **프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-134">In Visual Studio, on the **File** menu, point to **New**, and then click **Project**.</span></span> <span data-ttu-id="3f071-135">**새 프로젝트** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-135">The **New Project** dialog box appears.</span></span>

2. <span data-ttu-id="3f071-136">**프로젝트 형식** 창에서 **템플릿**, **Visual C#**, **웹**을 확장한 후 **ASP.NET 웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-136">In the **Project types** pane, expand **Templates**, **Visual C#**, **Web**, and then select **ASP.NET Web Application**.</span></span>

      ![ASP.NET 웹 응용 프로그램 프로젝트 유형이 강조 표시된 새 프로젝트 대화 상자의 스크린샷](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. <span data-ttu-id="3f071-138">**이름** 상자에 프로젝트의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-138">In the **Name** box, type the name of the project.</span></span> <span data-ttu-id="3f071-139">이 자습서에서는 "todo"라는 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-139">This tutorial uses the name "todo".</span></span> <span data-ttu-id="3f071-140">다른 이름을 사용하도록 선택한 경우에는 이 자습서에서 todo 네임스페이스를 지칭할 때마다 지정한 응용 프로그램 이름을 사용하도록 제공된 코드 샘플을 조정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-140">If you choose to use something other than this, then wherever this tutorial talks about the todo namespace, you need to adjust the provided code samples to use whatever you named your application.</span></span> 
4. <span data-ttu-id="3f071-141">**찾아보기**를 클릭하여 프로젝트를 만들 폴더로 이동한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-141">Click **Browse** to navigate to the folder where you would like to create the project, and then click **OK**.</span></span>
   
      <span data-ttu-id="3f071-142">**새 ASP.NET 웹 응용 프로그램** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-142">The **New ASP.NET Web Application** dialog box appears.</span></span>
   
    ![새 ASP.NET 웹 응용 프로그램 대화 상자 스크린샷(MVC 응용 프로그램 템플릿이 강조 표시됨)](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. <span data-ttu-id="3f071-144">템플릿 창에서 **MVC**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-144">In the templates pane, select **MVC**.</span></span>

6. <span data-ttu-id="3f071-145">**확인** 을 클릭하면 Visual Studio에서 빈 ASP.NET MVC 템플릿을 스캐폴딩합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-145">Click **OK** and let Visual Studio do its thing around scaffolding the empty ASP.NET MVC template.</span></span> 

          
7. <span data-ttu-id="3f071-146">Visual Studio에서 상용구 MVC 응용 프로그램을 만들면 로컬에서 실행할 수 있는 빈 ASP.NET 응용 프로그램을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-146">Once Visual Studio has finished creating the boilerplate MVC application you have an empty ASP.NET application that you can run locally.</span></span>
   
    <span data-ttu-id="3f071-147">모두 ASP.NET "Hello World" 응용 프로그램을 본 적이 있다고 확신하므로 프로젝트 로컬 실행은 건너뛰겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-147">We'll skip running the project locally because I'm sure we've all seen the ASP.NET "Hello World" application.</span></span> <span data-ttu-id="3f071-148">바로 이 프로젝트에 Azure Cosmos DB를 추가하고 응용 프로그램을 작성하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-148">Let's go straight to adding Azure Cosmos DB to this project and building our application.</span></span>

## <span data-ttu-id="3f071-149"><a name="_Toc395637767"></a>3단계: MVC 웹 응용 프로그램 프로젝트에 Azure Cosmos DB 추가</span><span class="sxs-lookup"><span data-stu-id="3f071-149"><a name="_Toc395637767"></a>Step 3: Add Azure Cosmos DB to your MVC web application project</span></span>
<span data-ttu-id="3f071-150">이 솔루션에 필요한 대부분의 ASP.NET MVC 배관을 만들었으므로 이제 이 자습서의 실제 목적으로 돌아가 MVC 웹 응용 프로그램에 Azure Cosmos DB를 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-150">Now that we have most of the ASP.NET MVC plumbing that we need for this solution, let's get to the real purpose of this tutorial, adding Azure Cosmos DB to our MVC web application.</span></span>

1. <span data-ttu-id="3f071-151">Azure Cosmos DB .NET SDK는 패키지되어 NuGet 패키지로 배포되며,</span><span class="sxs-lookup"><span data-stu-id="3f071-151">The Azure Cosmos DB .NET SDK is packaged and distributed as a NuGet package.</span></span> <span data-ttu-id="3f071-152">Visual Studio에서 NuGet 패키지를 다운로드하려면 **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭한 후 **NuGet 패키지 관리**를 클릭하여 Visual Studio에서 NuGet 패키지 관리자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-152">To get the NuGet package in Visual Studio, use the NuGet package manager in Visual Studio by right-clicking on the project in **Solution Explorer** and then clicking **Manage NuGet Packages**.</span></span>
   
    ![NuGet 패키지 관리가 강조 표시된 솔루션 탐색기 내 웹 응용 프로그램 프로젝트에 대한 마우스 오른쪽 클릭 옵션의 스크린샷](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    <span data-ttu-id="3f071-154">**NuGet 패키지 관리** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-154">The **Manage NuGet Packages** dialog box appears.</span></span>
2. <span data-ttu-id="3f071-155">NuGet **찾아보기** 상자에 ***Azure DocumentDB***를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-155">In the NuGet **Browse** box, type ***Azure DocumentDB***.</span></span> <span data-ttu-id="3f071-156">(패키지 이름은 Azure Cosmos DB로 업데이트되지 않았습니다.)</span><span class="sxs-lookup"><span data-stu-id="3f071-156">(The package name has not been updated to Azure Cosmos DB.)</span></span>
   
    <span data-ttu-id="3f071-157">결과에서 **Microsoft.Azure.DocumentDB by Microsoft** 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-157">From the results, install the **Microsoft.Azure.DocumentDB by Microsoft** package.</span></span> <span data-ttu-id="3f071-158">그러면 Azure Cosmos DB 패키지 및 모든 종속성(예: Newtonsoft.Json)이 다운로드되어 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-158">This will download and install the Azure Cosmos DB package as well as all dependencies, such as Newtonsoft.Json.</span></span> <span data-ttu-id="3f071-159">**미리 보기** 창에서 **확인**을 클릭하고 **라이선스 승인** 창에서 **동의**를 클릭하여 설치를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-159">Click **OK** in the **Preview** window, and **I Accept** in the **License Acceptance** window to complete the install.</span></span>
   
    ![Microsoft Azure DocumentDB Client Library가 강조 표시된 NuGet 패키지 관리 창의 스크린샷](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      <span data-ttu-id="3f071-161">또는 패키지 관리자 콘솔을 사용하여 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-161">Alternatively you can use the Package Manager Console to install the package.</span></span> <span data-ttu-id="3f071-162">이렇게 하려면 **도구** 메뉴에서 **NuGet 패키지 관리자**, **패키지 관리자 콘솔**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-162">To do so, on the **Tools** menu, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span> <span data-ttu-id="3f071-163">프롬프트에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-163">At the prompt, type the following.</span></span>
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. <span data-ttu-id="3f071-164">패키지가 설치되고 나면 Visual Studio 솔루션은 Microsoft.Azure.Documents.Client 및 Newtonsoft.Json이라는 두 개의 새 참조가 추가된 상태로 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-164">Once the package is installed, your Visual Studio solution should resemble the following with two new references added, Microsoft.Azure.Documents.Client and Newtonsoft.Json.</span></span>
   
    ![솔루션 탐색기에서 JSON 데이터 프로젝트에 추가된 두 참조의 스크린샷](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <span data-ttu-id="3f071-166"><a name="_Toc395637763"></a>4단계: ASP.NET MVC 응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="3f071-166"><a name="_Toc395637763"></a>Step 4: Set up the ASP.NET MVC application</span></span>
<span data-ttu-id="3f071-167">이제 이 MVC 응용 프로그램에 모델, 뷰 및 컨트롤러를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-167">Now let's add the models, views, and controllers to this MVC application:</span></span>

* <span data-ttu-id="3f071-168">[모델 추가](#_Toc395637764).</span><span class="sxs-lookup"><span data-stu-id="3f071-168">[Add a model](#_Toc395637764).</span></span>
* <span data-ttu-id="3f071-169">[컨트롤러 추가](#_Toc395637765).</span><span class="sxs-lookup"><span data-stu-id="3f071-169">[Add a controller](#_Toc395637765).</span></span>
* <span data-ttu-id="3f071-170">[뷰 추가](#_Toc395637766).</span><span class="sxs-lookup"><span data-stu-id="3f071-170">[Add views](#_Toc395637766).</span></span>

### <span data-ttu-id="3f071-171"><a name="_Toc395637764"></a>JSON 데이터 모델 추가</span><span class="sxs-lookup"><span data-stu-id="3f071-171"><a name="_Toc395637764"></a>Add a JSON data model</span></span>
<span data-ttu-id="3f071-172">먼저 MVC의 **M** 인 모델을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-172">Let's begin by creating the **M** in MVC, the model.</span></span> 

1. <span data-ttu-id="3f071-173">**솔루션 탐색기**에서 **Models** 폴더를 마우스 오른쪽 단추로 클릭한 후 **추가**, **클래스**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-173">In **Solution Explorer**, right-click the **Models** folder, click **Add**, and then click **Class**.</span></span>
   
      <span data-ttu-id="3f071-174">**새 항목 추가** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-174">The **Add New Item** dialog box appears.</span></span>
2. <span data-ttu-id="3f071-175">새 클래스의 이름을 **Item.cs**로 지정하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-175">Name your new class **Item.cs** and click **Add**.</span></span> 
3. <span data-ttu-id="3f071-176">이 새 **Item.cs** 파일에서 마지막 *using 문*뒤에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-176">In this new **Item.cs** file, add the following after the last *using statement*.</span></span>
   
        using Newtonsoft.Json;
4. <span data-ttu-id="3f071-177">이제 이 코드를</span><span class="sxs-lookup"><span data-stu-id="3f071-177">Now replace this code</span></span> 
   
        public class Item
        {
        }
   
    <span data-ttu-id="3f071-178">다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-178">with the following code.</span></span>
   
        public class Item
        {
            [JsonProperty(PropertyName = "id")]
            public string Id { get; set; }
   
            [JsonProperty(PropertyName = "name")]
            public string Name { get; set; }
   
            [JsonProperty(PropertyName = "description")]
            public string Description { get; set; }
   
            [JsonProperty(PropertyName = "isComplete")]
            public bool Completed { get; set; }
        }
   
    <span data-ttu-id="3f071-179">Azure Cosmos DB의 모든 데이터가 네트워크를 통해 전달되고 JSON으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-179">All data in Azure Cosmos DB is passed over the wire and stored as JSON.</span></span> <span data-ttu-id="3f071-180">JSON.NET에서 개체를 직렬화/역직렬화하는 방식을 제어하기 위해 방금 만든 **Item** 클래스에서 본 것처럼 **JsonProperty** 특성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-180">To control the way your objects are serialized/deserialized by JSON.NET you can use the **JsonProperty** attribute as demonstrated in the **Item** class we just created.</span></span> <span data-ttu-id="3f071-181">꼭 **필요한** 과정은 아니지만 저는 제가 만든 속성이 JSON camelCase 명명 규칙을 따르는지 확인하고 싶습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-181">You don't **have** to do this but I want to ensure that my properties follow the JSON camelCase naming conventions.</span></span> 
   
    <span data-ttu-id="3f071-182">JSON의 경우 속성 이름 형식을 제어할 수 있을 뿐만 아니라, **Description** 속성에 대해 했던 것처럼 .NET 속성의 이름을 완전히 다시 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-182">Not only can you control the format of the property name when it goes into JSON, but you can entirely rename your .NET properties like I did with the **Description** property.</span></span> 

### <span data-ttu-id="3f071-183"><a name="_Toc395637765"></a>컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="3f071-183"><a name="_Toc395637765"></a>Add a controller</span></span>
<span data-ttu-id="3f071-184">**M** 작업을 마쳤으므로 이제 MVC의 **C**인 컨트롤러 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-184">That takes care of the **M**, now let's create the **C** in MVC, a controller class.</span></span>

1. <span data-ttu-id="3f071-185">**솔루션 탐색기**에서 **Controllers** 폴더를 마우스 오른쪽 단추로 클릭한 후 **추가**, **컨트롤러**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-185">In **Solution Explorer**, right-click the **Controllers** folder, click **Add**, and then click **Controller**.</span></span>
   
    <span data-ttu-id="3f071-186">**스캐폴드 추가** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-186">The **Add Scaffold** dialog box appears.</span></span>
2. <span data-ttu-id="3f071-187">**MVC 5 컨트롤러 - 비어 있음**을 선택한 후 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-187">Select **MVC 5 Controller - Empty** and then click **Add**.</span></span>
   
    ![MVC 5 컨트롤러 - 비어 있음 옵션이 강조 표시된 스캐폴드 추가 대화 상자의 스크린샷](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. <span data-ttu-id="3f071-189">새 컨트롤러의 이름을 **ItemController**</span><span class="sxs-lookup"><span data-stu-id="3f071-189">Name your new Controller, **ItemController.**</span></span>
   
    ![컨트롤러 추가 대화 상자의 스크린샷](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    <span data-ttu-id="3f071-191">파일을 만들고 나면 Visual Studio 솔루션은 **솔루션 탐색기**에 새 ItemController.cs 파일이 있는 상태로 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-191">Once the file is created, your Visual Studio solution should resemble the following with the new ItemController.cs file in **Solution Explorer**.</span></span> <span data-ttu-id="3f071-192">이전에 만든 새 Item.cs 파일도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-192">The new Item.cs file created earlier is also shown.</span></span>
   
    ![Visual Studio 솔루션의 스크린샷 - 새 ItemController.cs 파일 및 Item.cs 파일이 강조 표시된 솔루션 탐색기](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    <span data-ttu-id="3f071-194">나중에 돌아올 것이므로 ItemController.cs를 닫아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-194">You can close ItemController.cs, we'll come back to it later.</span></span> 

### <span data-ttu-id="3f071-195"><a name="_Toc395637766"></a>뷰 추가</span><span class="sxs-lookup"><span data-stu-id="3f071-195"><a name="_Toc395637766"></a>Add views</span></span>
<span data-ttu-id="3f071-196">이제 MVC의 **V** 인 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-196">Now, let's create the **V** in MVC, the views:</span></span>

* <span data-ttu-id="3f071-197">[항목 인덱스 뷰 추가](#AddItemIndexView).</span><span class="sxs-lookup"><span data-stu-id="3f071-197">[Add an Item Index view](#AddItemIndexView).</span></span>
* <span data-ttu-id="3f071-198">[새 항목 뷰 추가](#AddNewIndexView).</span><span class="sxs-lookup"><span data-stu-id="3f071-198">[Add a New Item view](#AddNewIndexView).</span></span>
* <span data-ttu-id="3f071-199">[항목 편집 뷰 추가](#_Toc395888515).</span><span class="sxs-lookup"><span data-stu-id="3f071-199">[Add an Edit Item view](#_Toc395888515).</span></span>

#### <span data-ttu-id="3f071-200"><a name="AddItemIndexView"></a>항목 인덱스 뷰 추가</span><span class="sxs-lookup"><span data-stu-id="3f071-200"><a name="AddItemIndexView"></a>Add an Item Index view</span></span>
1. <span data-ttu-id="3f071-201">**솔루션 탐색기**에서 **Views** 폴더를 확장하고 앞에서 **ItemController**를 추가할 때 Visual Studio에서 만들어진 빈 **Item** 폴더를 마우스 오른쪽 단추로 클릭하고 **추가**, **보기**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-201">In **Solution Explorer**, expand the **Views**  folder, right-click the empty **Item** folder that Visual Studio created for you when you added the **ItemController** earlier, click **Add**, and then click **View**.</span></span>
   
    ![뷰 추가 명령이 강조 표시된 Visual Studio에서 만든 항목 폴더를 보여 주는 솔루션 탐색기의 스크린샷](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. <span data-ttu-id="3f071-203">**뷰 추가** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-203">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="3f071-204">**뷰 이름** 상자에 ***인덱스***를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-204">In the **View name** box, type ***Index***.</span></span>
   * <span data-ttu-id="3f071-205">**템플릿** 상자에서 ***목록***을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-205">In the **Template** box, select ***List***.</span></span>
   * <span data-ttu-id="3f071-206">**모델 클래스** 상자에서 ***항목(todo.Models)***을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-206">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="3f071-207">레이아웃 페이지 상자에 ***~/Views/Shared/_Layout.cshtml***을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-207">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
     
   ![뷰 추가 대화 상자를 보여주는 스크린샷](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. <span data-ttu-id="3f071-209">이러한 값이 모두 설정된 후 **추가** 를 클릭하면 Visual Studio에서 새 템플릿 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-209">Once all these values are set, click **Add** and let Visual Studio create a new template view.</span></span> <span data-ttu-id="3f071-210">완료되면 만들어진 cshtml 파일이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-210">Once it is done, it will open the cshtml file  that was created.</span></span> <span data-ttu-id="3f071-211">나중에 돌아올 것이므로 Visual Studio에서 해당 파일을 닫아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-211">We can close that file in Visual Studio as we will come back to it later.</span></span>

#### <span data-ttu-id="3f071-212"><a name="AddNewIndexView"></a>새 항목 뷰 추가</span><span class="sxs-lookup"><span data-stu-id="3f071-212"><a name="AddNewIndexView"></a>Add a New Item view</span></span>
<span data-ttu-id="3f071-213">**항목 인덱스** 뷰를 만든 방법과 유사하게 이제 새 **항목**을 만들기 위한 새 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-213">Similar to how we created an **Item Index** view, we will now create a new view for creating new **Items**.</span></span>

1. <span data-ttu-id="3f071-214">**솔루션 탐색기**에서 **Item** 폴더를 마우스 오른쪽 단추로 클릭한 후 **추가**, **보기**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-214">In **Solution Explorer**, right-click the **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="3f071-215">**뷰 추가** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-215">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="3f071-216">**뷰 이름** 상자에 ***Create***를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-216">In the **View name** box, type ***Create***.</span></span>
   * <span data-ttu-id="3f071-217">**템플릿** 상자에서 ***Create***를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-217">In the **Template** box, select ***Create***.</span></span>
   * <span data-ttu-id="3f071-218">**모델 클래스** 상자에서 ***항목(todo.Models)***을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-218">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="3f071-219">레이아웃 페이지 상자에 ***~/Views/Shared/_Layout.cshtml***을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-219">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="3f071-220">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-220">Click **Add**.</span></span>
   
#### <span data-ttu-id="3f071-221"><a name="_Toc395888515"></a>항목 편집 뷰 추가</span><span class="sxs-lookup"><span data-stu-id="3f071-221"><a name="_Toc395888515"></a>Add an Edit Item view</span></span>
<span data-ttu-id="3f071-222">마지막으로, 이전과 동일한 방식으로 **항목** 을 편집하기 위한 최종 뷰를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-222">And finally, add one last view for editing an **Item** in the same way as before.</span></span>

1. <span data-ttu-id="3f071-223">**솔루션 탐색기**에서 **Item** 폴더를 마우스 오른쪽 단추로 클릭한 후 **추가**, **보기**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-223">In **Solution Explorer**, right-click the **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="3f071-224">**뷰 추가** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-224">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="3f071-225">**뷰 이름** 상자에 ***Edit***를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-225">In the **View name** box, type ***Edit***.</span></span>
   * <span data-ttu-id="3f071-226">**템플릿** 상자에서 ***Edit***를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-226">In the **Template** box, select ***Edit***.</span></span>
   * <span data-ttu-id="3f071-227">**모델 클래스** 상자에서 ***항목(todo.Models)***을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-227">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="3f071-228">레이아웃 페이지 상자에 ***~/Views/Shared/_Layout.cshtml***을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-228">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="3f071-229">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-229">Click **Add**.</span></span>

<span data-ttu-id="3f071-230">이 작업이 완료되면 나중에 이러한 뷰로 돌아올 것이므로 Visual Studio에서 모든 cshtml 문서를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-230">Once this is done, close all the cshtml documents in Visual Studio as we will return to these views later.</span></span>

## <span data-ttu-id="3f071-231"><a name="_Toc395637769"></a>5단계: Azure Cosmos DB 연결</span><span class="sxs-lookup"><span data-stu-id="3f071-231"><a name="_Toc395637769"></a>Step 5: Wiring up Azure Cosmos DB</span></span>
<span data-ttu-id="3f071-232">표준 MVC를 처리했으므로 이제 Azure Cosmos DB에 대한 코드를 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-232">Now that the standard MVC stuff is taken care of, let's turn to adding the code for Azure Cosmos DB.</span></span> 

<span data-ttu-id="3f071-233">이 섹션에서는 다음을 처리하기 위한 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-233">In this section, we'll add code to handle the following:</span></span>

* <span data-ttu-id="3f071-234">[완료되지 않은 항목 나열](#_Toc395637770).</span><span class="sxs-lookup"><span data-stu-id="3f071-234">[Listing incomplete Items](#_Toc395637770).</span></span>
* <span data-ttu-id="3f071-235">[항목 추가](#_Toc395637771).</span><span class="sxs-lookup"><span data-stu-id="3f071-235">[Adding Items](#_Toc395637771).</span></span>
* <span data-ttu-id="3f071-236">[항목 편집](#_Toc395637772).</span><span class="sxs-lookup"><span data-stu-id="3f071-236">[Editing Items](#_Toc395637772).</span></span>

### <span data-ttu-id="3f071-237"><a name="_Toc395637770"></a>MVC 웹 응용 프로그램에서 완료되지 않은 항목 나열</span><span class="sxs-lookup"><span data-stu-id="3f071-237"><a name="_Toc395637770"></a>Listing incomplete Items in your MVC web application</span></span>
<span data-ttu-id="3f071-238">먼저 Azure Cosmos DB에 연결하고 이를 사용할 모든 논리가 포함된 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-238">The first thing to do here is add a class that contains all the logic to connect to and use Azure Cosmos DB.</span></span> <span data-ttu-id="3f071-239">이 자습서에서는 이 모든 논리를 DocumentDBRepository라는 리포지토리 클래스로 캡슐화합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-239">For this tutorial we'll encapsulate all this logic in to a repository class called DocumentDBRepository.</span></span> 

1. <span data-ttu-id="3f071-240">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**, **클래스**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-240">In **Solution Explorer**, right-click on the project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="3f071-241">새 클래스의 이름을 **DocumentDBRepository**로 지정하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-241">Name the new class **DocumentDBRepository** and click **Add**.</span></span>
2. <span data-ttu-id="3f071-242">새로 만든 **DocumentDBRepository** 클래스에서 *네임스페이스* 선언 위에 다음 *using 문*을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-242">In the newly created **DocumentDBRepository** class and add the following *using statements* above the *namespace* declaration</span></span>
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    <span data-ttu-id="3f071-243">이제 이 코드를</span><span class="sxs-lookup"><span data-stu-id="3f071-243">Now replace this code</span></span> 
   
        public class DocumentDBRepository
        {
        }
   
    <span data-ttu-id="3f071-244">다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-244">with the following code.</span></span>
   
        public static class DocumentDBRepository<T> where T : class
        {
            private static readonly string DatabaseId = ConfigurationManager.AppSettings["database"];
            private static readonly string CollectionId = ConfigurationManager.AppSettings["collection"];
            private static DocumentClient client;
   
            public static void Initialize()
            {
                client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);
                CreateDatabaseIfNotExistsAsync().Wait();
                CreateCollectionIfNotExistsAsync().Wait();
            }
   
            private static async Task CreateDatabaseIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDatabaseAsync(UriFactory.CreateDatabaseUri(DatabaseId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
   
            private static async Task CreateCollectionIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDocumentCollectionAsync(
                            UriFactory.CreateDatabaseUri(DatabaseId),
                            new DocumentCollection { Id = CollectionId },
                            new RequestOptions { OfferThroughput = 1000 });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
        }
   
    
3. <span data-ttu-id="3f071-245">구성에서 일부 값을 읽어올 것이므로 응용 프로그램의 **Web.config** 파일을 열고 `<AppSettings>` 섹션 아래에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-245">We're reading some values from configuration, so open the **Web.config** file of your application and add the following lines under the `<AppSettings>` section.</span></span>
   
        <add key="endpoint" value="enter the URI from the Keys blade of the Azure Portal"/>
        <add key="authKey" value="enter the PRIMARY KEY, or the SECONDARY KEY, from the Keys blade of the Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. <span data-ttu-id="3f071-246">이제 Azure Portal의 키 블레이드를 사용하여 *끝점* 및 *authKey* 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-246">Now, update the values for *endpoint* and *authKey* using the Keys blade of the Azure Portal.</span></span> <span data-ttu-id="3f071-247">키 블레이드의 **URI**를 끝점 설정 값으로 사용하고 키 블레이드의 **기본 키** 또는 **보조 키**를 authKey 설정 값으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-247">Use the **URI** from the Keys blade as the value of the endpoint setting, and use the **PRIMARY KEY**, or **SECONDARY KEY** from the Keys blade as the value of the authKey setting.</span></span>

    <span data-ttu-id="3f071-248">Azure Cosmos DB 리포지토리의 연결을 완료했으므로 이제 응용 프로그램 논리를 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-248">That takes care of wiring up the Azure Cosmos DB repository, now let's add our application logic.</span></span>

1. <span data-ttu-id="3f071-249">todo 모음 응용 프로그램으로 가장 먼저 할 일은 완료되지 않은 항목을 표시하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-249">The first thing we want to be able to do with a todo list application is to display the incomplete items.</span></span>  <span data-ttu-id="3f071-250">다음 코드 조각을 **DocumentDBRepository** 클래스 내의 아무 곳에나 복사하여 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-250">Copy and paste the following code snippet anywhere within the **DocumentDBRepository** class.</span></span>
   
        public static async Task<IEnumerable<T>> GetItemsAsync(Expression<Func<T, bool>> predicate)
        {
            IDocumentQuery<T> query = client.CreateDocumentQuery<T>(
                UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId))
                .Where(predicate)
                .AsDocumentQuery();
   
            List<T> results = new List<T>();
            while (query.HasMoreResults)
            {
                results.AddRange(await query.ExecuteNextAsync<T>());
            }
   
            return results;
        }
2. <span data-ttu-id="3f071-251">앞에서 추가한 **ItemController** 를 열고 네임스페이스 선언 위에 다음 *using 문* 을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-251">Open the **ItemController** we added earlier and add the following *using statements* above the namespace declaration.</span></span>
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    <span data-ttu-id="3f071-252">프로젝트 이름이 "todo"가 아닌 경우 프로젝트 이름을 반영하기 위해 "todo.Models";를 사용하여 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-252">If your project is not named "todo", then you need to update using "todo.Models"; to reflect the name of your project.</span></span>
   
    <span data-ttu-id="3f071-253">이제 이 코드를</span><span class="sxs-lookup"><span data-stu-id="3f071-253">Now replace this code</span></span>
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    <span data-ttu-id="3f071-254">다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-254">with the following code.</span></span>
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. <span data-ttu-id="3f071-255">**Global.asax.cs**를 열고 **Application_Start** 메서드에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-255">Open **Global.asax.cs** and add the following line to the **Application_Start** method</span></span> 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

<span data-ttu-id="3f071-256">이때 오류 없이 솔루션을 작성할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-256">At this point your solution should be able to build without any errors.</span></span>

<span data-ttu-id="3f071-257">지금 응용 프로그램을 실행하면 **HomeController** 및 해당 컨트롤러의 **인덱스** 뷰로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-257">If you ran the application now, you would go to the **HomeController** and the **Index** view of that controller.</span></span> <span data-ttu-id="3f071-258">이것은 시작할 때 선택한 MVC 템플릿 프로젝트에 대한 기본 동작이지만 여기서는 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-258">This is the default behavior for the MVC template project we chose at the start but we don't want that!</span></span> <span data-ttu-id="3f071-259">이 동작을 변경하기 위해 이 MVC 응용 프로그램의 라우팅을 변경하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-259">Let's change the routing on this MVC application to alter this behavior.</span></span>

<span data-ttu-id="3f071-260">***App\_Start\RouteConfig.cs***를 열고 "defaults:"로 시작하는 줄을 찾은 후 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-260">Open ***App\_Start\RouteConfig.cs*** and locate the line starting with "defaults:" and change it to resemble the following.</span></span>

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

<span data-ttu-id="3f071-261">이 구문은 이제 ASP.NET MVC에 라우팅 동작을 제어하기 위한 URL에 값이 지정되지 않은 경우 **홈** 대신 **항목**을 컨트롤러로 사용하고 사용자 **인덱스**를 뷰로 사용하라고 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-261">This now tells ASP.NET MVC that if you have not specified a value in the URL to control the routing behavior that instead of **Home**, use **Item** as the controller and user **Index** as the view.</span></span>

<span data-ttu-id="3f071-262">이제 응용 프로그램을 실행하면 응용 프로그램에서 리포지토리 클래스를 호출하는 **ItemController**를 호출하며 GetItems 메서드를 사용하여 완료되지 않은 모든 항목을 **Views**\\**Item**\\**Index** 뷰로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-262">Now if you run the application, it will call into your **ItemController** which will call in to the repository class and use the GetItems method to return all the incomplete items to the **Views**\\**Item**\\**Index** view.</span></span> 

<span data-ttu-id="3f071-263">이 프로젝트를 지금 빌드하여 실행하면 이제 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-263">If you build and run this project now, you should now see something that looks this.</span></span>    

![이 데이터베이스 자습서에서 만든 할 일 모음 웹 응용 프로그램의 스크린샷](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <span data-ttu-id="3f071-265"><a name="_Toc395637771"></a>항목 추가</span><span class="sxs-lookup"><span data-stu-id="3f071-265"><a name="_Toc395637771"></a>Adding Items</span></span>
<span data-ttu-id="3f071-266">빈 그리드 외에 확인할 항목이 있도록 데이터베이스에 일부 항목을 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-266">Let's put some items into our database so we have something more than an empty grid to look at.</span></span>

<span data-ttu-id="3f071-267">Azure Cosmos DB에 레코드를 저장하기 위해 Azure Cosmos DBRepository 및 ItemController에 일부 코드를 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-267">Let's add some code to  Azure Cosmos DBRepository and ItemController to persist the record in Azure Cosmos DB.</span></span>

1. <span data-ttu-id="3f071-268">다음 메서드를 **DocumentDBRepository** 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-268">Add the following method to your **DocumentDBRepository** class.</span></span>
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   <span data-ttu-id="3f071-269">이 메서드는 단순히 전달된 개체를 받아서 Azure Cosmos DB에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-269">This method simply takes an object passed to it and persists it in Azure Cosmos DB.</span></span>
2. <span data-ttu-id="3f071-270">ItemController.cs 파일을 열고 클래스 내에 다음 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-270">Open the ItemController.cs file and add the following code snippet within the class.</span></span> <span data-ttu-id="3f071-271">이를 통해 ASP.NET MVC에서 **Create** 작업을 위해 수행할 작업을 인식할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-271">This is how ASP.NET MVC knows what to do for the **Create** action.</span></span> <span data-ttu-id="3f071-272">이 경우 앞에서 만든 관련 Create.cshtml 뷰를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-272">In this case just render the associated Create.cshtml view created earlier.</span></span>
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    <span data-ttu-id="3f071-273">이제 **만들기** 뷰의 제출을 수락하는 코드를 이 컨트롤러에 더 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-273">We now need some more code in this controller that will accept the submission from the **Create** view.</span></span>
3. <span data-ttu-id="3f071-274">이 컨트롤러에 대한 폼 POST의 처리 방법을 ASP.NET MVC에 알리는 다음 코드 블록을 ItemController.cs 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-274">Add the next block of code to the ItemController.cs class that tells ASP.NET MVC what to do with a form POST for this controller.</span></span>
   
        [HttpPost]
        [ActionName("Create")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> CreateAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.CreateItemAsync(item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
    <span data-ttu-id="3f071-275">이 코드는 DocumentDBRepository를 호출하고 CreateItemAsync 메서드를 사용하여 새로운 todo 항목을 데이터베이스에 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-275">This code calls in to the DocumentDBRepository and uses the CreateItemAsync method to persist the new todo item to the database.</span></span> 
   
    <span data-ttu-id="3f071-276">**보안 정보**: **ValidateAntiForgeryToken** 특성은 여기서 교차 사이트 요청 위조 공격으로부터 이 응용 프로그램을 보호하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-276">**Security Note**: The **ValidateAntiForgeryToken** attribute is used here to help protect this application against cross-site request forgery attacks.</span></span> <span data-ttu-id="3f071-277">이 특성을 추가하는 것 외에 뷰가 이 위조 방지 토큰과 작동하도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-277">There is more to it than just adding this attribute, your views need to work with this anti-forgery token as well.</span></span> <span data-ttu-id="3f071-278">이 주제에 대한 자세한 내용과 이를 올바르게 구현하는 방법의 예는 [교차 사이트 요청 위조 방지(영문)][Preventing Cross-Site Request Forgery]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f071-278">For more on the subject, and examples of how to implement this correctly, please see [Preventing Cross-Site Request Forgery][Preventing Cross-Site Request Forgery].</span></span> <span data-ttu-id="3f071-279">[GitHub][GitHub]에서 제공하는 소스 코드에는 완벽하게 구현되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-279">The source code provided on [GitHub][GitHub] has the full implementation in place.</span></span>
   
    <span data-ttu-id="3f071-280">**보안 정보**: 또한 메서드 매개 변수에 **Bind** 특성을 사용하여 과도한 게시 공격으로부터 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-280">**Security Note**: We also use the **Bind** attribute on the method parameter to help protect against over-posting attacks.</span></span> <span data-ttu-id="3f071-281">자세한 내용은 [ASP.NET MVC의 기본 CRUD 작업(영문)][Basic CRUD Operations in ASP.NET MVC]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f071-281">For more details please see [Basic CRUD Operations in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span></span>

<span data-ttu-id="3f071-282">데이터베이스에 새 항목을 추가하는 데 필요한 코드가 완성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-282">This concludes the code required to add new Items to our database.</span></span>

### <span data-ttu-id="3f071-283"><a name="_Toc395637772"></a>항목 편집</span><span class="sxs-lookup"><span data-stu-id="3f071-283"><a name="_Toc395637772"></a>Editing Items</span></span>
<span data-ttu-id="3f071-284">마지막으로 수행할 작업은 데이터베이스에서 **항목** 을 편집하고 완료로 표시하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-284">There is one last thing for us to do, and that is to add the ability to edit **Items** in the database and to mark them as complete.</span></span> <span data-ttu-id="3f071-285">편집용 뷰는 이미 프로젝트에 추가되었으므로 다시 컨트롤러와 **DocumentDBRepository** 클래스에 일부 코드를 추가하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-285">The view for editing was already added to the project, so we just need to add some code to our controller and to the **DocumentDBRepository** class again.</span></span>

1. <span data-ttu-id="3f071-286">**DocumentDBRepository** 클래스에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-286">Add the following to the **DocumentDBRepository** class.</span></span>
   
        public static async Task<Document> UpdateItemAsync(string id, T item)
        {
            return await client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id), item);
        }
   
        public static async Task<T> GetItemAsync(string id)
        {
            try
            {
                Document document = await client.ReadDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id));
                return (T)(dynamic)document;
            }
            catch (DocumentClientException e)
            {
                if (e.StatusCode == HttpStatusCode.NotFound)
                {
                    return null;
                }
                else
                {
                    throw;
                }
            }
        }
   
    <span data-ttu-id="3f071-287">이러한 메서드 중 첫 번째 메서드인 **GetItem**은 Azure Cosmos DB에서 항목을 가져오며, 이 항목이 다시 **ItemController** 및 **편집** 뷰로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-287">The first of these methods, **GetItem** fetches an Item from Azure Cosmos DB which is passed back to the **ItemController** and then on to the **Edit** view.</span></span>
   
    <span data-ttu-id="3f071-288">방금 추가한 메서드 중 두 번째 메서드는 Cosmos DB의 **문서**를 **ItemController**에서 전달된 **문서** 버전으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-288">The second of the methods we just added replaces the **Document** in Azure Cosmos DB with the version of the **Document** passed in from the **ItemController**.</span></span>
2. <span data-ttu-id="3f071-289">**ItemController** 클래스에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-289">Add the following to the **ItemController** class.</span></span>
   
        [HttpPost]
        [ActionName("Edit")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> EditAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.UpdateItemAsync(item.Id, item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
        [ActionName("Edit")]
        public async Task<ActionResult> EditAsync(string id)
        {
            if (id == null)
            {
                return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
            }
   
            Item item = await DocumentDBRepository<Item>.GetItemAsync(id);
            if (item == null)
            {
                return HttpNotFound();
            }
   
            return View(item);
        }
   
    <span data-ttu-id="3f071-290">첫 번째 메서드는 사용자가 **인덱스** 뷰에서 **편집** 링크를 클릭할 때 발생하는 Http Get을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-290">The first method handles the Http GET that happens when the user clicks on the **Edit** link from the **Index** view.</span></span> <span data-ttu-id="3f071-291">이 메서드는 Azure Cosmos DB에서 [**문서**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx)를 가져와 **편집** 뷰에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-291">This method fetches a [**Document**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) from Azure Cosmos DB and passes it to the **Edit** view.</span></span>
   
    <span data-ttu-id="3f071-292">그런 다음 **편집** 뷰는 **IndexController**에 Http Post를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-292">The **Edit** view will then do an Http POST to the **IndexController**.</span></span> 
   
    <span data-ttu-id="3f071-293">추가한 두 번째 메서드는 데이터베이스에 저장되도록 업데이트된 개체를 Azure Cosmos DB에 전달하는 작업을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-293">The second method we added handles passing the updated object to Azure Cosmos DB to be persisted in the database.</span></span>

<span data-ttu-id="3f071-294">응용 프로그램을 실행하는 데 필요한 모든 작업(완료되지 않은 **항목** 나열, 새 **항목** 추가 및 **항목** 편집)이 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-294">That's it, that is everything we need to run our application, list incomplete **Items**, add new **Items**, and edit **Items**.</span></span>

## <span data-ttu-id="3f071-295"><a name="_Toc395637773"></a>6단계: 로컬에서 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="3f071-295"><a name="_Toc395637773"></a>Step 6: Run the application locally</span></span>
<span data-ttu-id="3f071-296">로컬 컴퓨터에서 응용 프로그램을 테스트하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-296">To test the application on your local machine, do the following:</span></span>

1. <span data-ttu-id="3f071-297">디버그 모드에서 응용 프로그램을 빌드하려면 Visual Studio에서 F5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-297">Hit F5 in Visual Studio to build the application in debug mode.</span></span> <span data-ttu-id="3f071-298">응용 프로그램이 빌드되고 앞에서 본 것처럼 빈 그리드 페이지가 포함된 상태로 브라우저가 시작되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-298">It should build the application and launch a browser with the empty grid page we saw before:</span></span>
   
    ![이 데이터베이스 자습서에서 만든 할 일 모음 웹 응용 프로그램의 스크린샷](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. <span data-ttu-id="3f071-300">**새로 만들기** 링크를 클릭하고 **이름** 및 **설명** 필드에 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-300">Click the **Create New** link and add values to the **Name** and **Description** fields.</span></span> <span data-ttu-id="3f071-301">**완료** 확인란을 선택 취소된 상태로 둡니다. 그렇지 않으면 새 **항목**이 완료 상태로 추가되며 초기 목록에 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-301">Leave the **Completed** check box unselected otherwise the new **Item** will be added in a completed state and will not appear on the initial list.</span></span>
   
    ![만들기 뷰의 스크린샷](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. <span data-ttu-id="3f071-303">**만들기**를 클릭하면 **인덱스** 뷰로 다시 리디렉션되고 **항목**이 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-303">Click **Create** and you are redirected back to the **Index** view and your **Item** appears in the list.</span></span>
   
    ![인덱스 뷰의 스크린샷](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    <span data-ttu-id="3f071-305">Todo 목록에 **항목** 을 더 추가해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-305">Feel free to add a few more **Items** to your todo list.</span></span>
    
4. <span data-ttu-id="3f071-306">목록에서 **항목** 옆의 **편집**을 클릭합니다. **편집** 뷰로 이동되며, 여기서 **완료** 플래그를 비롯한 개체 속성을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-306">Click **Edit** next to an **Item** on the list and you are taken to the **Edit** view where you can update any property of your object, including the **Completed** flag.</span></span> <span data-ttu-id="3f071-307">**완료** 플래그를 표시하고 **저장**을 클릭하면 **항목**이 완료되지 않은 작업 목록에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-307">If you mark the **Complete** flag and click **Save**, the **Item** is removed from the list of incomplete tasks.</span></span>
   
    ![완료 상자가 선택된 인덱스 뷰의 스크린샷](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. <span data-ttu-id="3f071-309">앱을 테스트하고 나면 Ctrl+F5를 눌러 앱 디버깅을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-309">Once you've tested the app, press Ctrl+F5 to stop debugging the app.</span></span> <span data-ttu-id="3f071-310">배포할 준비가 되었습니다!</span><span class="sxs-lookup"><span data-stu-id="3f071-310">You're ready to deploy!</span></span>

## <span data-ttu-id="3f071-311"><a name="_Toc395637774"></a>7단계: Azure App Service에 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="3f071-311"><a name="_Toc395637774"></a>Step 7: Deploy the application to Azure App Service</span></span> 
<span data-ttu-id="3f071-312">이제 전체 응용 프로그램이 Azure Cosmos DB와 올바르게 작동하므로 Azure App Service에 이 웹앱을 배포하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-312">Now that you have the complete application working correctly with Azure Cosmos DB we're going to deploy this web app to Azure App Service.</span></span>  

1. <span data-ttu-id="3f071-313">이 응용 프로그램을 게시하기 위해 할 일은 **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 클릭하는 것뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-313">To publish this application all you need to do is right-click on the project in **Solution Explorer** and click **Publish**.</span></span>
   
    ![솔루션 탐색기 내 게시 옵션의 스크린샷](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. <span data-ttu-id="3f071-315">**게시** 대화 상자에서 **Microsoft Azure App Service**를 클릭한 다음 **새로 만들기**를 선택하여 App Service 프로필을 만들거나 **기존 항목 선택**을 클릭하여 기존 프로필을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-315">In the **Publish** dialog box, click **Microsoft Azure App Service**, then select **Create New** to create an App Service profile, or click **Select Existing** to use an existing profile.</span></span>

    ![Visual Studio에서 대화 상자 게시](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. <span data-ttu-id="3f071-317">기존 Azure App Service 프로필이 있는 경우 구독 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-317">If you have an existing Azure App Service profile, enter your subscription name.</span></span> <span data-ttu-id="3f071-318">**보기** 필터를 사용하여 리소스 그룹 또는 리소스 종류별로 정렬한 다음 Azure App Service를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-318">Use the **View** filter to sort by resource group or resource type, then select your Azure App Service.</span></span> 
   
    ![Visual Studio의 App Service 대화 상자](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. <span data-ttu-id="3f071-320">새 Azure App Service 프로필을 만들려면 **게시** 대화 상자에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-320">To create a new Azure App Service profile, click **Create New** in the **Publish** dialog box.</span></span> <span data-ttu-id="3f071-321">**앱 서비스 만들기** 대화 상자에서 웹앱 이름 및 적절한 구독, 리소스 그룹 및 App Service 계획을 입력하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-321">In the **Create App Service** dialog, enter your Web App name and appropriate subscription, resource group, and App Service plan, then click **Create**.</span></span>

    ![Visual Studio의 앱 서비스 만들기 대화 상자](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

<span data-ttu-id="3f071-323">몇 초 후에 Visual Studio에서 웹 응용 프로그램 게시를 완료하고 브라우저를 시작하며, Azure에서 실행되는 작업 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-323">In a few seconds, Visual Studio will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>



## <span data-ttu-id="3f071-324"><a name="_Toc395637775"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="3f071-324"><a name="_Toc395637775"></a>Next steps</span></span>
<span data-ttu-id="3f071-325">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-325">Congratulations!</span></span> <span data-ttu-id="3f071-326">지금까지 Azure Cosmos DB를 사용하여 첫 ASP.NET MVC 웹 응용 프로그램을 빌드하고 Azure에 게시했습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-326">You just built your first ASP.NET MVC web application using Azure Cosmos DB and published it to Azure.</span></span> <span data-ttu-id="3f071-327">이 자습서에 포함되지 않은 세부 정보 및 삭제 기능을 비롯한 전체 응용 프로그램 소스 코드는 [GitHub][GitHub]에서 다운로드하거나 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-327">The source code for the complete application, including the detail and delete functionality that were not included in this tutorial can be downloaded or cloned from [GitHub][GitHub].</span></span> <span data-ttu-id="3f071-328">따라서 이 내용을 앱에 추가하려는 경우 코드를 끌어와서 이 앱에 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f071-328">So if you're interested in adding that to your app, grab the code and add it to this app.</span></span>

<span data-ttu-id="3f071-329">응용 프로그램에 기능을 더 추가하려면 [Azure Cosmos DB .NET 라이브러리](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)에서 사용 가능한 API를 검토하고 [GitHub][GitHub]의 Azure Cosmos DB .NET 라이브러리에 자유롭게 기여하세요.</span><span class="sxs-lookup"><span data-stu-id="3f071-329">To add additional functionality to your application, review the APIs available in the [Azure Cosmos DB .NET Library](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) and feel free to contribute to the Azure Cosmos DB .NET Library on [GitHub][GitHub].</span></span> 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
