---
title: "SQL Database를 사용하여 Azure에서 ASP.NET 앱 빌드 | Microsoft Docs"
description: "SQL Database에 연결하여 Azure에서 ASP.NET 앱이 작동하도록 하는 방법에 대해 알아봅니다."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 03c584f1-a93c-4e3d-ac1b-c82b50c75d3e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: csharp
ms.topic: tutorial
ms.date: 06/09/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: c22b8ef4866fe2f1ae32c7cb9158fc7866788b26
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a><span data-ttu-id="89a5a-103">SQL Database를 사용하여 Azure에서 ASP.NET 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="89a5a-103">Build an ASP.NET app in Azure with SQL Database</span></span>

<span data-ttu-id="89a5a-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="89a5a-105">이 자습서에서는 Azure에서 데이터 기반 ASP.NET 웹앱을 개발하고 [Azure SQL Database](../sql-database/sql-database-technical-overview.md)에 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-105">This tutorial shows you how to deploy a data-driven ASP.NET web app in Azure and connect it to [Azure SQL Database](../sql-database/sql-database-technical-overview.md).</span></span> <span data-ttu-id="89a5a-106">완료되면 ASP.NET 앱이 [Azure App Service](../app-service/app-service-value-prop-what-is.md)에서 실행되고 SQL Database에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-106">When you're finished, you have a ASP.NET app running in [Azure App Service](../app-service/app-service-value-prop-what-is.md) and connected to SQL Database.</span></span>

![Azure 웹앱의 게시된 ASP.NET 응용 프로그램](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="89a5a-108">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="89a5a-109">Azure에서 SQL Database 만들기</span><span class="sxs-lookup"><span data-stu-id="89a5a-109">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="89a5a-110">SQL Database에 ASP.NET 앱 연결</span><span class="sxs-lookup"><span data-stu-id="89a5a-110">Connect an ASP.NET app to SQL Database</span></span>
> * <span data-ttu-id="89a5a-111">Azure에 앱 배포</span><span class="sxs-lookup"><span data-stu-id="89a5a-111">Deploy the app to Azure</span></span>
> * <span data-ttu-id="89a5a-112">데이터 모델 업데이트 및 앱 다시 배포</span><span class="sxs-lookup"><span data-stu-id="89a5a-112">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="89a5a-113">Azure에서 터미널로 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="89a5a-113">Stream logs from Azure to your terminal</span></span>
> * <span data-ttu-id="89a5a-114">Azure Portal에서 앱 관리</span><span class="sxs-lookup"><span data-stu-id="89a5a-114">Manage the app in the Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89a5a-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="89a5a-115">Prerequisites</span></span>

<span data-ttu-id="89a5a-116">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-116">To complete this tutorial:</span></span>

* <span data-ttu-id="89a5a-117">다음 워크로드와 함께 [Visual Studio 2017](https://www.visualstudio.com/downloads/)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-117">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the following workloads:</span></span>
  - <span data-ttu-id="89a5a-118">**ASP.NET 및 웹 배포**</span><span class="sxs-lookup"><span data-stu-id="89a5a-118">**ASP.NET and web development**</span></span>
  - <span data-ttu-id="89a5a-119">**Azure 개발**</span><span class="sxs-lookup"><span data-stu-id="89a5a-119">**Azure development**</span></span>

  ![ASP.NET 및 웹 개발 및 Azure 개발(웹 & 클라우드에서)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-the-sample"></a><span data-ttu-id="89a5a-121">샘플 다운로드</span><span class="sxs-lookup"><span data-stu-id="89a5a-121">Download the sample</span></span>

<span data-ttu-id="89a5a-122">[샘플 프로젝트를 다운로드합니다](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="89a5a-122">[Download the sample project](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span></span>

<span data-ttu-id="89a5a-123">*dotnet-sqldb-tutorial-master.zip* 파일을 추출(압축 해제)합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-123">Extract (unzip) the  *dotnet-sqldb-tutorial-master.zip* file.</span></span>

<span data-ttu-id="89a5a-124">샘플 프로젝트에는 [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application)를 사용하는 기본 [ASP.NET MVC](https://www.asp.net/mvc) CRUD(Create-Read-Update-Delete) 앱이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-124">The sample project contains a basic [ASP.NET MVC](https://www.asp.net/mvc) CRUD (create-read-update-delete) app using [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="run-the-app"></a><span data-ttu-id="89a5a-125">앱 실행</span><span class="sxs-lookup"><span data-stu-id="89a5a-125">Run the app</span></span>

<span data-ttu-id="89a5a-126">Visual Studio에서 *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-126">Open the *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* file in Visual Studio.</span></span> 

<span data-ttu-id="89a5a-127">디버깅 없이 앱을 실행하려면 `Ctrl+F5`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-127">Type `Ctrl+F5` to run the app without debugging.</span></span> <span data-ttu-id="89a5a-128">앱이 기본 브라우저에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-128">The app is displayed in your default browser.</span></span> <span data-ttu-id="89a5a-129">**새로 만들기** 링크를 선택하고 두 개의 *할 일* 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-129">Select the **Create New** link and create a couple *to-do* items.</span></span> 

![새 ASP.NET 프로젝트 대화 상자](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

<span data-ttu-id="89a5a-131">**편집**, **세부 정보** 및 **삭제** 링크를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-131">Test the **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="89a5a-132">앱은 데이터베이스 컨텍스트를 사용하여 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-132">The app uses a database context to connect with the database.</span></span> <span data-ttu-id="89a5a-133">이 샘플의 데이터베이스 컨텍스트에는 `MyDbConnection`이라는 연결 문자열이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-133">In this sample, the database context uses a connection string named `MyDbConnection`.</span></span> <span data-ttu-id="89a5a-134">연결 문자열은 *Web.config* 파일에서 설정되고 *Models\MyDatabaseContext.cs* 파일에서 참조됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-134">The connection string is set in the *Web.config* file and referenced in the *Models/MyDatabaseContext.cs* file.</span></span> <span data-ttu-id="89a5a-135">연결 문자열 이름은 이 자습서의 뒷부분에서 Azure 웹앱을 Azure SQL Database에 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-135">The connection string name is used later in the tutorial to connect the Azure web app to an Azure SQL Database.</span></span> 

## <a name="publish-to-azure-with-sql-database"></a><span data-ttu-id="89a5a-136">SQL Database를 사용하여 Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="89a5a-136">Publish to Azure with SQL Database</span></span>

<span data-ttu-id="89a5a-137">**솔루션 탐색기**에서 **DotNetAppSqlDb** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-137">In the **Solution Explorer**, right-click your **DotNetAppSqlDb** project and select **Publish**.</span></span>

![솔루션 탐색기에서 게시](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

<span data-ttu-id="89a5a-139">**Microsoft Azure App Service**를 선택했는지 확인하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-139">Make sure that **Microsoft Azure App Service** is selected and click **Publish**.</span></span>

![프로젝트 개요 페이지에서 게시](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

<span data-ttu-id="89a5a-141">게시하는 경우 Azure에서 ASP.NET 웹앱을 실행하는 데 필요한 모든 Azure 리소스를 만들 수 있는 유용한 **App Service 만들기** 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-141">Publishing opens the **Create App Service** dialog, which helps you create all the Azure resources you need to run your ASP.NET web app in Azure.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="89a5a-142">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="89a5a-142">Sign in to Azure</span></span>

<span data-ttu-id="89a5a-143">**App Service 만들기** 대화 상자에서 **계정 추가**를 클릭한 다음 Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-143">In the **Create App Service** dialog, click **Add an account**, and then sign in to your Azure subscription.</span></span> <span data-ttu-id="89a5a-144">이미 Microsoft 계정에 로그인한 경우 계정에 Azure 구독이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-144">If you're already signed into a Microsoft account, make sure that account holds your Azure subscription.</span></span> <span data-ttu-id="89a5a-145">로그인된 Microsoft 계정에 Azure 구독이 없는 경우 클릭하여 올바른 계정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-145">If the signed-in Microsoft account doesn't have your Azure subscription, click it to add the correct account.</span></span>
   
![Azure에 로그인](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

<span data-ttu-id="89a5a-147">일단 로그인되면 이 대화 상자에서 Azure 웹앱에 필요한 모든 리소스를 만들 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-147">Once signed in, you're ready to create all the resources you need for your Azure web app in this dialog.</span></span>

### <a name="configure-the-web-app-name"></a><span data-ttu-id="89a5a-148">웹앱 이름 구성</span><span class="sxs-lookup"><span data-stu-id="89a5a-148">Configure the web app name</span></span>

<span data-ttu-id="89a5a-149">생성된 웹앱 이름을 유지하거나 다른 고유한 이름으로 변경할 수 있습니다(유효한 문자: `a-z`, `0-9` 및 `-`).</span><span class="sxs-lookup"><span data-stu-id="89a5a-149">You can keep the generated web app name, or change it to another unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="89a5a-150">웹앱 이름은 앱의 기본 URL(`<app_name>.azurewebsites.net`, 여기서 `<app_name>`는 웹앱 이름)의 일부로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-150">The web app name is used as part of the default URL for your app (`<app_name>.azurewebsites.net`, where `<app_name>` is your web app name).</span></span> <span data-ttu-id="89a5a-151">웹앱 이름은 Azure의 모든 앱에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-151">The web app name needs to be unique across all apps in Azure.</span></span> 

![앱 서비스 만들기 대화 상자](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a><span data-ttu-id="89a5a-153">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="89a5a-153">Create a resource group</span></span>

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="89a5a-154">**리소스 그룹** 옆에 있는 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-154">Next to **Resource Group**, click **New**.</span></span>

![[리소스 그룹] 옆에 있는 [새로 만들기]를 클릭합니다.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

<span data-ttu-id="89a5a-156">리소스 그룹 이름을 **myResourceGroup**으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-156">Name the resource group **myResourceGroup**.</span></span>

> [!NOTE]
> <span data-ttu-id="89a5a-157">**만들기**는 클릭하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="89a5a-157">Do not click **Create**.</span></span> <span data-ttu-id="89a5a-158">먼저 나중의 단계에서 SQL Database를 설정해야 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-158">You first need to set up a SQL Database in a later step.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="89a5a-159">App Service 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="89a5a-159">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="89a5a-160">**App Service 계획** 옆에 있는 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-160">Next to **App Service Plan**, click **New**.</span></span> 

<span data-ttu-id="89a5a-161">**App Service 계획 구성** 대화 상자에서 다음 설정을 사용하여 새 App Service 계획을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-161">In the **Configure App Service Plan** dialog, configure the new App Service plan with the following settings:</span></span>

![앱 서비스 계획 만들기](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| <span data-ttu-id="89a5a-163">설정</span><span class="sxs-lookup"><span data-stu-id="89a5a-163">Setting</span></span>  | <span data-ttu-id="89a5a-164">제안 값</span><span class="sxs-lookup"><span data-stu-id="89a5a-164">Suggested value</span></span> | <span data-ttu-id="89a5a-165">Blob에 대한 자세한 내용은</span><span class="sxs-lookup"><span data-stu-id="89a5a-165">For more information</span></span> |
| ----------------- | ------------ | ----|
|<span data-ttu-id="89a5a-166">**App Service 계획**</span><span class="sxs-lookup"><span data-stu-id="89a5a-166">**App Service Plan**</span></span>| <span data-ttu-id="89a5a-167">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="89a5a-167">myAppServicePlan</span></span> | [<span data-ttu-id="89a5a-168">App Service 계획</span><span class="sxs-lookup"><span data-stu-id="89a5a-168">App Service plans</span></span>](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|<span data-ttu-id="89a5a-169">**위치**</span><span class="sxs-lookup"><span data-stu-id="89a5a-169">**Location**</span></span>| <span data-ttu-id="89a5a-170">서유럽</span><span class="sxs-lookup"><span data-stu-id="89a5a-170">West Europe</span></span> | [<span data-ttu-id="89a5a-171">Azure 지역</span><span class="sxs-lookup"><span data-stu-id="89a5a-171">Azure regions</span></span>](https://azure.microsoft.com/regions/) |
|<span data-ttu-id="89a5a-172">**크기**</span><span class="sxs-lookup"><span data-stu-id="89a5a-172">**Size**</span></span>| <span data-ttu-id="89a5a-173">무료</span><span class="sxs-lookup"><span data-stu-id="89a5a-173">Free</span></span> | [<span data-ttu-id="89a5a-174">가격 책정 계층</span><span class="sxs-lookup"><span data-stu-id="89a5a-174">Pricing tiers</span></span>](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a><span data-ttu-id="89a5a-175">SQL Server 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="89a5a-175">Create a SQL Server instance</span></span>

<span data-ttu-id="89a5a-176">먼저 [Azure SQL Database 논리 서버](../sql-database/sql-database-features.md)가 있어야 데이터베이스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-176">Before creating a database, you need an [Azure SQL Database logical server](../sql-database/sql-database-features.md).</span></span> <span data-ttu-id="89a5a-177">논리 서버는 그룹으로 관리되는 데이터베이스 그룹을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-177">A logical server contains a group of databases managed as a group.</span></span>

<span data-ttu-id="89a5a-178">**추가 Azure 서비스 탐색**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-178">Select **Explore additional Azure services**.</span></span>

![웹앱 이름 구성](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

<span data-ttu-id="89a5a-180">**서비스** 탭에서 **SQL Database** 옆에 있는 **+**  아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-180">In the **Services** tab, click the **+** icon next to **SQL Database**.</span></span> 

![[서비스] 탭에서 [SQL Database] 옆에 있는 + 아이콘을 클릭합니다.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

<span data-ttu-id="89a5a-182">**SQL Database 구성** 대화 상자에서 **SQL Server** 옆에 있는 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-182">In the **Configure SQL Database** dialog, click **New** next to **SQL Server**.</span></span> 

<span data-ttu-id="89a5a-183">고유한 서버 이름이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-183">A unique server name is generated.</span></span> <span data-ttu-id="89a5a-184">이 이름은 논리 서버에 대한 기본 URL(`<server_name>.database.windows.net`)의 일부로 사용되며,</span><span class="sxs-lookup"><span data-stu-id="89a5a-184">This name is used as part of the default URL for your logical server, `<server_name>.database.windows.net`.</span></span> <span data-ttu-id="89a5a-185">Azure의 모든 논리 서버 인스턴스에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-185">It must be unique across all logical server instances in Azure.</span></span> <span data-ttu-id="89a5a-186">서버 이름은 변경할 수 있지만 이 자습서에서는 생성된 값을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-186">You can change the server name, but for this tutorial, keep the generated value.</span></span>

<span data-ttu-id="89a5a-187">관리자 사용자 이름과 암호를 추가한 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-187">Add an administrator username and password, and then select **OK**.</span></span> <span data-ttu-id="89a5a-188">암호 복잡성 요구 사항은 [암호 정책](/sql/relational-databases/security/password-policy)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89a5a-188">For password complexity requirements, see [Password Policy](/sql/relational-databases/security/password-policy).</span></span>

<span data-ttu-id="89a5a-189">이 사용자 이름과 암호를 기억해 두세요.</span><span class="sxs-lookup"><span data-stu-id="89a5a-189">Remember this username and password.</span></span> <span data-ttu-id="89a5a-190">나중에 논리 서버 인스턴스를 관리하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-190">You need them to manage the logical server instance later.</span></span>

![SQL Server 인스턴스 만들기](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a><span data-ttu-id="89a5a-192">SQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="89a5a-192">Create a SQL Database</span></span>

<span data-ttu-id="89a5a-193">**SQL Database 구성** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-193">In the **Configure SQL Database** dialog:</span></span> 

* <span data-ttu-id="89a5a-194">생성된 기본 **데이터베이스 이름**을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-194">Keep the default generated **Database Name**.</span></span>
* <span data-ttu-id="89a5a-195">**연결 문자열 이름**에 *MyDbConnection*을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-195">In **Connection String Name**, type *MyDbConnection*.</span></span> <span data-ttu-id="89a5a-196">이 이름은 *Models\MyDatabaseContext.cs*에서 참조되는 연결 문자열과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-196">This name must match the connection string that is referenced in *Models/MyDatabaseContext.cs*.</span></span>
* <span data-ttu-id="89a5a-197">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-197">Select **OK**.</span></span>

![SQL Database 구성](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

<span data-ttu-id="89a5a-199">**App Service 만들기** 대화 상자에서 만든 리소스를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-199">The **Create App Service** dialog shows the resources you've created.</span></span> <span data-ttu-id="89a5a-200">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-200">Click **Create**.</span></span> 

![만든 리소스](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

<span data-ttu-id="89a5a-202">마법사에서 Azure 리소스 만들기를 완료하면 ASP.NET 응용 프로그램을 Azure에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-202">Once the wizard finishes creating the Azure resources, it  publishes your ASP.NET app to Azure.</span></span> <span data-ttu-id="89a5a-203">기본 브라우저가 배포된 앱에 대한 URL로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-203">Your default browser is launched with the URL to the deployed app.</span></span> 

<span data-ttu-id="89a5a-204">몇 가지 할 일 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-204">Add a few to-do items.</span></span>

![Azure 웹앱의 게시된 ASP.NET 응용 프로그램](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="89a5a-206">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-206">Congratulations!</span></span> <span data-ttu-id="89a5a-207">데이터 기반 ASP.NET 응용 프로그램이 Azure App Service에서 라이브로 실행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-207">Your data-driven ASP.NET application is running live in Azure App Service.</span></span>

## <a name="access-the-sql-database-locally"></a><span data-ttu-id="89a5a-208">로컬에서 SQL Database에 액세스</span><span class="sxs-lookup"><span data-stu-id="89a5a-208">Access the SQL Database locally</span></span>

<span data-ttu-id="89a5a-209">Visual Studio를 사용하면 **SQL Server 개체 탐색기**에서 새 SQL Database를 쉽게 탐색하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-209">Visual Studio lets you explore and manage your new SQL Database easily in the **SQL Server Object Explorer**.</span></span>

### <a name="create-a-database-connection"></a><span data-ttu-id="89a5a-210">데이터베이스 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="89a5a-210">Create a database connection</span></span>

<span data-ttu-id="89a5a-211">**보기** 메뉴에서 **SQL Server 개체 탐색기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-211">From the **View** menu, select **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="89a5a-212">**SQL Server 개체 탐색기** 맨 위에 있는 **SQL Server 추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-212">At the top of **SQL Server Object Explorer**, click the **Add SQL Server** button.</span></span>

### <a name="configure-the-database-connection"></a><span data-ttu-id="89a5a-213">데이터베이스 연결 구성</span><span class="sxs-lookup"><span data-stu-id="89a5a-213">Configure the database connection</span></span>

<span data-ttu-id="89a5a-214">**연결** 대화 상자에서 **Azure** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-214">In the **Connect** dialog, expand the **Azure** node.</span></span> <span data-ttu-id="89a5a-215">여기서는 Azure의 모든 SQL Database 인스턴스가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-215">All your SQL Database instances in Azure are listed here.</span></span>

<span data-ttu-id="89a5a-216">`DotNetAppSqlDb` SQL Database를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-216">Select the `DotNetAppSqlDb` SQL Database.</span></span> <span data-ttu-id="89a5a-217">앞에서 만든 연결이 맨 아래쪽에 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-217">The connection you created earlier is automatically filled at the bottom.</span></span>

<span data-ttu-id="89a5a-218">이전에 사용한 데이터베이스 관리자 암호를 입력하고 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-218">Type the database administrator password you created earlier and click **Connect**.</span></span>

![Visual Studio에서 데이터베이스 연결 구성](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a><span data-ttu-id="89a5a-220">컴퓨터에서 클라이언트 연결 허용</span><span class="sxs-lookup"><span data-stu-id="89a5a-220">Allow client connection from your computer</span></span>

<span data-ttu-id="89a5a-221">**새 방화벽 규칙 만들기** 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-221">The **Create a new firewall rule** dialog is opened.</span></span> <span data-ttu-id="89a5a-222">기본적으로 SQL Database 인스턴스는 Azure 웹앱과 같은 Azure 서비스의 연결만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-222">By default, your SQL Database instance only allows connections from Azure services, such as your Azure web app.</span></span> <span data-ttu-id="89a5a-223">데이터베이스에 연결하려면 SQL Database 인스턴스에 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-223">To connect to your database, create a firewall rule in the SQL Database instance.</span></span> <span data-ttu-id="89a5a-224">방화벽 규칙에는 로컬 컴퓨터의 공용 IP 주소가 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-224">The firewall rule allows the public IP address of your local computer.</span></span>

<span data-ttu-id="89a5a-225">대화 상자가 컴퓨터의 공용 IP 주소로 이미 채워져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-225">The dialog is already filled with your computer's public IP address.</span></span>

<span data-ttu-id="89a5a-226">**내 클라이언트 IP 추가**가 선택되어 있는지 확인하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-226">Make sure that **Add my client IP** is selected and click **OK**.</span></span> 

![SQL Database 인스턴스에 대한 방화벽 설정](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

<span data-ttu-id="89a5a-228">Visual Studio에서 SQL Database 인스턴스에 대한 방화벽 설정을 만든 후에 **SQL Server 개체 탐색기**에 연결이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-228">Once Visual Studio finishes creating the firewall setting for your SQL Database instance, your connection shows up in **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="89a5a-229">여기에서 쿼리 실행, 뷰 및 저장 프로시저 만들기 등의 가장 일반적이 데이터베이스 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-229">Here, you can perform the most common database operations, such as run queries, create views and stored procedures, and more.</span></span> 

<span data-ttu-id="89a5a-230">`Todoes` 테이블을 마우스 오른쪽 단추로 클릭하고 **데이터 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-230">Right-click on the `Todoes` table and select **View Data**.</span></span> 

![SQL Database 개체 탐색](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a><span data-ttu-id="89a5a-232">Code First 마이그레이션으로 앱 업데이트</span><span class="sxs-lookup"><span data-stu-id="89a5a-232">Update app with Code First Migrations</span></span>

<span data-ttu-id="89a5a-233">Visual Studio의 친숙한 도구를 사용하여 Azure에서 데이터베이스 및 웹앱을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-233">You can use the familiar tools in Visual Studio to update your database and web app in Azure.</span></span> <span data-ttu-id="89a5a-234">이 단계에서는 Entity Framework에서 Code First 마이그레이션을 사용하여 데이터베이스 스키마를 변경하고 Azure에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-234">In this step, you use Code First Migrations in Entity Framework to make a change to your database schema and publish it to Azure.</span></span>

<span data-ttu-id="89a5a-235">Entity Framework Code First 마이그레이션 사용에 대한 자세한 내용은 [MVC 5를 사용하여 Entity Framework 6 Code First 시작](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89a5a-235">For more information about using Entity Framework Code First Migrations, see [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="update-your-data-model"></a><span data-ttu-id="89a5a-236">데이터 모델 업데이트</span><span class="sxs-lookup"><span data-stu-id="89a5a-236">Update your data model</span></span>

<span data-ttu-id="89a5a-237">코드 편집기에서 _Models\Todo.cs_를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-237">Open _Models\Todo.cs_ in the code editor.</span></span> <span data-ttu-id="89a5a-238">다음 속성을 `ToDo` 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-238">Add the following property to the `ToDo` class:</span></span>

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a><span data-ttu-id="89a5a-239">Code First 마이그레이션을 로컬에서 실행</span><span class="sxs-lookup"><span data-stu-id="89a5a-239">Run Code First Migrations locally</span></span>

<span data-ttu-id="89a5a-240">몇 가지 명령을 실행하여 로컬 데이터베이스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-240">Run a few commands to make updates to your local database.</span></span> 

<span data-ttu-id="89a5a-241">**도구** 메뉴에서 **NuGet 패키지 관리** > **패키지 관리자 콘솔**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-241">From the **Tools** menu, click **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="89a5a-242">[패키지 관리자 콘솔] 창에서 Code First 마이그레이션을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-242">In the Package Manager Console window, enable Code First Migrations:</span></span>

```PowerShell
Enable-Migrations
```

<span data-ttu-id="89a5a-243">마이그레이션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-243">Add a migration:</span></span>

```PowerShell
Add-Migration AddProperty
```

<span data-ttu-id="89a5a-244">로컬 데이터베이스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-244">Update the local database:</span></span>

```PowerShell
Update-Database
```

<span data-ttu-id="89a5a-245">`Ctrl+F5`를 입력하여 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-245">Type `Ctrl+F5` to run the app.</span></span> <span data-ttu-id="89a5a-246">편집, 세부 정보 및 만들기 링크를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-246">Test the edit, details, and create links.</span></span>

<span data-ttu-id="89a5a-247">응용 프로그램이 오류 없이 로드되면 Code First 마이그레이션이 성공한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-247">If the application loads without errors, then Code First Migrations has succeeded.</span></span> <span data-ttu-id="89a5a-248">그러나 응용 프로그램 논리에서 이 새로운 속성을 아직 사용하지 않기 때문에 페이지가 여전히 동일하게 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-248">However, your page still looks the same because your application logic is not using this new property yet.</span></span> 

### <a name="use-the-new-property"></a><span data-ttu-id="89a5a-249">새 속성 사용</span><span class="sxs-lookup"><span data-stu-id="89a5a-249">Use the new property</span></span>

<span data-ttu-id="89a5a-250">`Done` 속성을 사용하도록 코드를 약간 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-250">Make some changes in your code to use the `Done` property.</span></span> <span data-ttu-id="89a5a-251">이 자습서에서는 간단하게 `Index` 및 `Create` 보기만 변경하여 속성의 실제 작동을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-251">For simplicity in this tutorial, you're only going to change the `Index` and `Create` views to see the property in action.</span></span>

<span data-ttu-id="89a5a-252">_Controllers\TodosController.cs_를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-252">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="89a5a-253">`Create()` 메서드를 찾고 `Done`을 `Bind` 특성의 속성 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-253">Find the `Create()` method and add `Done` to the list of properties in the `Bind` attribute.</span></span> <span data-ttu-id="89a5a-254">완료되면 `Create()` 메서드 시그니처가 다음 코드와 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-254">When you're done, your `Create()` method signature looks like the following code:</span></span>

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

<span data-ttu-id="89a5a-255">_Views\Todos\Create.cshtml_을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-255">Open _Views\Todos\Create.cshtml_.</span></span>

<span data-ttu-id="89a5a-256">Razor 코드에서 `model.Description`을 사용하는 `<div class="form-group">` 요소가 표시된 다음 `model.CreatedDate`를 사용하는 또 다른 `<div class="form-group">` 요소가 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-256">In the Razor code, you should see a `<div class="form-group">` element that uses `model.Description`, and then another `<div class="form-group">` element that uses `model.CreatedDate`.</span></span> <span data-ttu-id="89a5a-257">이러한 두 요소 바로 뒤에 `model.Done`을 사용하는 또 다른 `<div class="form-group">` 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-257">Immediately following these two elements, add another `<div class="form-group">` element that uses `model.Done`:</span></span>

```csharp
<div class="form-group">
    @Html.LabelFor(model => model.Done, htmlAttributes: new { @class = "control-label col-md-2" })
    <div class="col-md-10">
        <div class="checkbox">
            @Html.EditorFor(model => model.Done)
            @Html.ValidationMessageFor(model => model.Done, "", new { @class = "text-danger" })
        </div>
    </div>
</div>
```

<span data-ttu-id="89a5a-258">_Views\Todos\Index.cshtml_을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-258">Open _Views\Todos\Index.cshtml_.</span></span>

<span data-ttu-id="89a5a-259">빈 `<th></th>` 요소를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-259">Search for the empty `<th></th>` element.</span></span> <span data-ttu-id="89a5a-260">이 요소 바로 위에 다음 Razor 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-260">Just above this element, add the following Razor code:</span></span>

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

<span data-ttu-id="89a5a-261">`Html.ActionLink()` 도우미 메서드가 포함된 `<td>` 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-261">Find the `<td>` element that contains the `Html.ActionLink()` helper methods.</span></span> <span data-ttu-id="89a5a-262">이 요소 바로 위에 다음 Razor 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-262">Just above this element, add the following Razor code:</span></span>

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

<span data-ttu-id="89a5a-263">`Index` 및 `Create` 보기에서 변경 내용을 확인하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-263">That's all you need to see the changes in the `Index` and `Create` views.</span></span> 

<span data-ttu-id="89a5a-264">`Ctrl+F5`를 입력하여 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-264">Type `Ctrl+F5` to run the app.</span></span>

<span data-ttu-id="89a5a-265">이제 할 일 항목을 추가하고 **완료**를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-265">You can now add a to-do item and check **Done**.</span></span> <span data-ttu-id="89a5a-266">그러면 홈페이지에 완료된 항목으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-266">Then it should show up in your homepage as a completed item.</span></span> <span data-ttu-id="89a5a-267">`Edit` 보기를 변경하지 않았으므로 `Edit` 보기에서 `Done` 필드가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-267">Remember that the `Edit` view doesn't show the `Done` field, because you didn't change the `Edit` view.</span></span>

### <a name="enable-code-first-migrations-in-azure"></a><span data-ttu-id="89a5a-268">Azure에서 Code First 마이그레이션 사용</span><span class="sxs-lookup"><span data-stu-id="89a5a-268">Enable Code First Migrations in Azure</span></span>

<span data-ttu-id="89a5a-269">데이터베이스 마이그레이션을 비롯하여 코드 변경이 수행되었으므로 Azure 웹앱에 게시하고 Code First 마이그레이션을 사용하여 SQL Database도 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-269">Now that your code change works, including database migration, you publish it to your Azure web app and update your SQL Database with Code First Migrations too.</span></span>

<span data-ttu-id="89a5a-270">이전과 마찬가지로 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-270">Just like before, right-click your project and select **Publish**.</span></span>

<span data-ttu-id="89a5a-271">**설정**을 클릭하여 게시 마법사를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-271">Click **Settings** to open the publish wizard.</span></span>

![게시 설정 열기](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

<span data-ttu-id="89a5a-273">마법사에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-273">In the wizard, click **Next**.</span></span>

<span data-ttu-id="89a5a-274">SQL Database에 대한 연결 문자열이 **MyDatabaseContext (MyDbConnection)**로 채워졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-274">Make sure that the connection string for your SQL Database is populated in **MyDatabaseContext (MyDbConnection)**.</span></span> <span data-ttu-id="89a5a-275">드롭다운에서 **myToDoAppDb** 데이터베이스를 선택해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-275">You may need to select the **myToDoAppDb** database from the dropdown.</span></span> 

<span data-ttu-id="89a5a-276">**Execute Code First Migrations (runs on application start)**(Code First 마이그레이션 실행(응용 프로그램 시작 시 실행))를 선택한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-276">Select **Execute Code First Migrations (runs on application start)**, then click **Save**.</span></span>

![Azure 웹앱에서 Code First 마이그레이션 사용](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a><span data-ttu-id="89a5a-278">변경 내용 게시</span><span class="sxs-lookup"><span data-stu-id="89a5a-278">Publish your changes</span></span>

<span data-ttu-id="89a5a-279">이제 Azure 웹앱에서 Code First 마이그레이션을 사용하도록 설정했으므로 코드 변경 내용을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-279">Now that you enabled Code First Migrations in your Azure web app, publish your code changes.</span></span>

<span data-ttu-id="89a5a-280">게시 페이지에서 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-280">In the publish page, click **Publish**.</span></span>

<span data-ttu-id="89a5a-281">할 일 항목 추가를 다시 시도하고 **Done**(완료)을 선택합니다. 그러면 홈페이지에 완료된 항목으로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-281">Try adding to-do items again and select **Done**, and they should show up in your homepage as a completed item.</span></span>

![Code First 마이그레이션 후 Azure 웹앱](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

<span data-ttu-id="89a5a-283">기존의 모든 할 일 항목이 계속 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-283">All your existing to-do items are still displayed.</span></span> <span data-ttu-id="89a5a-284">ASP.NET 응용 프로그램을 다시 게시해도 SQL Database의 기존 데이터가 손실되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-284">When you republish your ASP.NET application, existing data in your SQL Database is not lost.</span></span> <span data-ttu-id="89a5a-285">또한 Code First 마이그레이션은 데이터 스키마만 변경하고 기존 데이터는 그대로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-285">Also, Code First Migrations only changes the data schema and leaves your existing data intact.</span></span>


## <a name="stream-application-logs"></a><span data-ttu-id="89a5a-286">응용 프로그램 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="89a5a-286">Stream application logs</span></span>

<span data-ttu-id="89a5a-287">Azure 웹앱에서 직접 Visual Studio로 추적 메시지를 스트림할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-287">You can stream tracing messages directly from your Azure web app to Visual Studio.</span></span>

<span data-ttu-id="89a5a-288">_Controllers\TodosController.cs_를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-288">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="89a5a-289">각 동작은 `Trace.WriteLine()` 메서드로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-289">Each action starts with a `Trace.WriteLine()` method.</span></span> <span data-ttu-id="89a5a-290">이 코드는 Azure 웹앱에 추적 메시지를 추가하는 방법을 보여 주기 위해 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-290">This code is added to show you how to add trace messages to your Azure web app.</span></span>

### <a name="open-server-explorer"></a><span data-ttu-id="89a5a-291">서버 탐색기 열기</span><span class="sxs-lookup"><span data-stu-id="89a5a-291">Open Server Explorer</span></span>

<span data-ttu-id="89a5a-292">**보기** 메뉴에서 **서버 탐색기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-292">From the **View** menu, select **Server Explorer**.</span></span> <span data-ttu-id="89a5a-293">**서버 탐색기**에서 Azure 웹앱에 대한 로깅을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-293">You can configure logging for your Azure web app in **Server Explorer**.</span></span> 

### <a name="enable-log-streaming"></a><span data-ttu-id="89a5a-294">로그 스트리밍 사용</span><span class="sxs-lookup"><span data-stu-id="89a5a-294">Enable log streaming</span></span>

<span data-ttu-id="89a5a-295">**서버 탐색기**에서 **Azure** > **App Service**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-295">In **Server Explorer**, expand **Azure** > **App Service**.</span></span>

<span data-ttu-id="89a5a-296">Azure 웹앱을 처음 만들 때 만든 **myResourceGroup** 리소스 그룹을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-296">Expand the **myResourceGroup** resource group, you created when you first created the Azure web app.</span></span>

<span data-ttu-id="89a5a-297">Azure 웹앱을 마우스 오른쪽 단추로 클릭하고 **스트리밍 로그 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-297">Right-click your Azure web app and select **View Streaming Logs**.</span></span>

![로그 스트리밍 사용](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

<span data-ttu-id="89a5a-299">이제 로그가 **출력** 창으로 스트리밍됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-299">The logs are now streamed into the **Output** window.</span></span> 

![출력 창에서 로그 스트리밍](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

<span data-ttu-id="89a5a-301">그러나 추적 메시지가 아직 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-301">However, you don't see any of the trace messages yet.</span></span> <span data-ttu-id="89a5a-302">**스트리밍 로그 보기**를 먼저 선택하면 Azure 웹앱에서 추적 수준을 `Error`로 설정하여 `Trace.TraceError()` 메서드로 생성된 오류 이벤트만 로깅하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-302">That's because when you first select **View Streaming Logs**, your Azure web app sets the trace level to `Error`, which only logs error events (with the `Trace.TraceError()` method).</span></span>

### <a name="change-trace-levels"></a><span data-ttu-id="89a5a-303">추적 수준 변경</span><span class="sxs-lookup"><span data-stu-id="89a5a-303">Change trace levels</span></span>

<span data-ttu-id="89a5a-304">다른 추적 메시지를 출력하도록 추적 수준을 변경하려면 **서버 탐색기**로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-304">To change the trace levels to output other trace messages, go back to **Server Explorer**.</span></span>

<span data-ttu-id="89a5a-305">Azure 웹앱을 마우스 오른쪽 단추로 다시 클릭하고 **설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-305">Right-click your Azure web app again and select **Settings**.</span></span>

<span data-ttu-id="89a5a-306">**응용 프로그램 로깅(파일 시스템)** 드롭다운에서 **자세한 정보 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-306">In the **Application Logging (File System)** dropdown, select **Verbose**.</span></span> <span data-ttu-id="89a5a-307">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-307">Click **Save**.</span></span>

![추적 수준을 자세한 정보 표시로 설정](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> <span data-ttu-id="89a5a-309">다양한 추적 수준을 사용하여 각 수준에서 표시되는 메시지 종류를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-309">You can experiment with different trace levels to see what types of messages are displayed for each level.</span></span> <span data-ttu-id="89a5a-310">예를 들어 **정보** 수준에는 `Trace.TraceInformation()`, `Trace.TraceWarning()` 및 `Trace.TraceError()`로 생성된 모든 로그가 포함되지만 `Trace.WriteLine()`으로 생성된 로그는 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-310">For example, the **Information** level includes all logs created by `Trace.TraceInformation()`, `Trace.TraceWarning()`, and `Trace.TraceError()`, but not logs created by `Trace.WriteLine()`.</span></span>
>
>

<span data-ttu-id="89a5a-311">브라우저에서 Azure의 할 일 목록 응용 프로그램을 클릭해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-311">In your browser, try clicking around the to-do list application in Azure.</span></span> <span data-ttu-id="89a5a-312">추적 메시지가 Visual Studio의 **출력** 창으로 스트리밍됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-312">The trace messages are now streamed to the **Output** window in Visual Studio.</span></span>

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a><span data-ttu-id="89a5a-313">로그 스트리밍 중지</span><span class="sxs-lookup"><span data-stu-id="89a5a-313">Stop log streaming</span></span>

<span data-ttu-id="89a5a-314">로그 스트리밍 서비스를 중지하려면 **출력** 창에서 **모니터링 중지** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-314">To stop the log-streaming service, click the **Stop monitoring** button in the **Output** window.</span></span>

![로그 스트리밍 중지](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="89a5a-316">Azure Web App 관리</span><span class="sxs-lookup"><span data-stu-id="89a5a-316">Manage your Azure web app</span></span>

<span data-ttu-id="89a5a-317">[Azure Portal](https://portal.azure.com)로 이동하여 만든 웹앱을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-317">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span> 



<span data-ttu-id="89a5a-318">왼쪽 메뉴에서 **App Service**를 클릭한 다음 Azure 웹앱의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-318">From the left menu, click **App Service**, then click the name of your Azure web app.</span></span>

![Azure 웹앱에 대한 포털 탐색](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

<span data-ttu-id="89a5a-320">웹앱 페이지에 연결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-320">You have landed in your web app's page.</span></span> 

<span data-ttu-id="89a5a-321">기본적으로 포털에서 **개요** 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-321">By default, the portal shows the **Overview** page.</span></span> <span data-ttu-id="89a5a-322">이 페이지에서는 앱이 어떻게 작동하고 있는지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-322">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="89a5a-323">여기에서 찾아보기, 중지, 시작, 다시 시작, 삭제와 같은 기본 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-323">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="89a5a-324">페이지의 왼쪽에 있는 탭에서는 열 수 있는 여러 구성 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-324">The tabs on the left side of the page show the different configuration pages you can open.</span></span> 

![Azure Portal의 App Service 페이지](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="89a5a-326">다음 단계</span><span class="sxs-lookup"><span data-stu-id="89a5a-326">Next steps</span></span>

<span data-ttu-id="89a5a-327">이 자습서에서 학습한 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-327">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="89a5a-328">Azure에서 SQL Database 만들기</span><span class="sxs-lookup"><span data-stu-id="89a5a-328">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="89a5a-329">SQL Database에 ASP.NET 앱 연결</span><span class="sxs-lookup"><span data-stu-id="89a5a-329">Connect an ASP.NET app to SQL Database</span></span>
> * <span data-ttu-id="89a5a-330">Azure에 앱 배포</span><span class="sxs-lookup"><span data-stu-id="89a5a-330">Deploy the app to Azure</span></span>
> * <span data-ttu-id="89a5a-331">데이터 모델 업데이트 및 앱 다시 배포</span><span class="sxs-lookup"><span data-stu-id="89a5a-331">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="89a5a-332">Azure에서 터미널로 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="89a5a-332">Stream logs from Azure to your terminal</span></span>
> * <span data-ttu-id="89a5a-333">Azure Portal에서 앱 관리</span><span class="sxs-lookup"><span data-stu-id="89a5a-333">Manage the app in the Azure portal</span></span>

<span data-ttu-id="89a5a-334">다음 자습서로 이동하여 사용자 지정 DNS 이름을 웹앱에 매핑하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="89a5a-334">Advance to the next tutorial to learn how to map a custom DNS name to the web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="89a5a-335">Azure Web Apps에 기존 사용자 지정 DNS 이름 매핑</span><span class="sxs-lookup"><span data-stu-id="89a5a-335">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
