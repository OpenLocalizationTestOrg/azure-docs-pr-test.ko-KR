---
title: "SQL 데이터베이스를 사용 하 여 Azure에 ASP.NET 응용 프로그램 aaaBuild | Microsoft Docs"
description: "자세한 방법을 tooget는 ASP.NET 응용 프로그램 연결 tooa SQL 데이터베이스와 Azure에서 작업 합니다."
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
ms.openlocfilehash: d21c2bc404bfe038608c17e5a94d96847153002c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a><span data-ttu-id="116c0-103">SQL Database를 사용하여 Azure에서 ASP.NET 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="116c0-103">Build an ASP.NET app in Azure with SQL Database</span></span>

<span data-ttu-id="116c0-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="116c0-105">이 자습서에서는 toodeploy 데이터 기반 ASP.NET 웹 앱에 Azure 방법과 너무 연결[Azure SQL 데이터베이스](../sql-database/sql-database-technical-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-105">This tutorial shows you how toodeploy a data-driven ASP.NET web app in Azure and connect it too[Azure SQL Database](../sql-database/sql-database-technical-overview.md).</span></span> <span data-ttu-id="116c0-106">실행 중인 ASP.NET 앱이 있는 완료 된 경우 [Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md) tooSQL 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-106">When you're finished, you have a ASP.NET app running in [Azure App Service](../app-service/app-service-value-prop-what-is.md) and connected tooSQL Database.</span></span>

![Azure 웹앱의 게시된 ASP.NET 응용 프로그램](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="116c0-108">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="116c0-109">Azure에서 SQL Database 만들기</span><span class="sxs-lookup"><span data-stu-id="116c0-109">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="116c0-110">ASP.NET 응용 프로그램 tooSQL 데이터베이스 연결</span><span class="sxs-lookup"><span data-stu-id="116c0-110">Connect an ASP.NET app tooSQL Database</span></span>
> * <span data-ttu-id="116c0-111">Hello 앱 tooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="116c0-111">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="116c0-112">Hello 데이터 모델을 업데이트 하 고 hello 응용 프로그램을 다시 배포</span><span class="sxs-lookup"><span data-stu-id="116c0-112">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="116c0-113">Azure tooyour 터미널에서 스트림 로그</span><span class="sxs-lookup"><span data-stu-id="116c0-113">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="116c0-114">Hello Azure 포털에서에서 hello 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="116c0-114">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="116c0-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="116c0-115">Prerequisites</span></span>

<span data-ttu-id="116c0-116">toocomplete이이 자습서:</span><span class="sxs-lookup"><span data-stu-id="116c0-116">toocomplete this tutorial:</span></span>

* <span data-ttu-id="116c0-117">설치 [Visual Studio 2017](https://www.visualstudio.com/downloads/) 워크 로드를 수행 하는 hello로:</span><span class="sxs-lookup"><span data-stu-id="116c0-117">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello following workloads:</span></span>
  - <span data-ttu-id="116c0-118">**ASP.NET 및 웹 배포**</span><span class="sxs-lookup"><span data-stu-id="116c0-118">**ASP.NET and web development**</span></span>
  - <span data-ttu-id="116c0-119">**Azure 개발**</span><span class="sxs-lookup"><span data-stu-id="116c0-119">**Azure development**</span></span>

  ![ASP.NET 및 웹 개발 및 Azure 개발(웹 & 클라우드에서)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a><span data-ttu-id="116c0-121">Hello 샘플 다운로드</span><span class="sxs-lookup"><span data-stu-id="116c0-121">Download hello sample</span></span>

<span data-ttu-id="116c0-122">[Hello 샘플 프로젝트를 다운로드](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip)합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-122">[Download hello sample project](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span></span>

<span data-ttu-id="116c0-123">추출 (압축) hello *sqldb 자습서 master.zip dotnet* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-123">Extract (unzip) hello  *dotnet-sqldb-tutorial-master.zip* file.</span></span>

<span data-ttu-id="116c0-124">hello 샘플 프로젝트에는 기본 [ASP.NET MVC](https://www.asp.net/mvc) CRUD (만들기-읽기-업데이트-삭제) 응용 프로그램 사용 하 여 [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application)합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-124">hello sample project contains a basic [ASP.NET MVC](https://www.asp.net/mvc) CRUD (create-read-update-delete) app using [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="run-hello-app"></a><span data-ttu-id="116c0-125">Hello 앱 실행</span><span class="sxs-lookup"><span data-stu-id="116c0-125">Run hello app</span></span>

<span data-ttu-id="116c0-126">열기 hello *dotnet-sqldb-자습서-마스터/DotNetAppSqlDb.sln* Visual Studio에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-126">Open hello *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* file in Visual Studio.</span></span> 

<span data-ttu-id="116c0-127">형식 `Ctrl+F5` 디버깅 하지 않고 toorun hello 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-127">Type `Ctrl+F5` toorun hello app without debugging.</span></span> <span data-ttu-id="116c0-128">hello 앱은 기본 브라우저에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-128">hello app is displayed in your default browser.</span></span> <span data-ttu-id="116c0-129">선택 hello **새로 만들기** 에 연결 하 고 2를 만들어 *할 일* 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-129">Select hello **Create New** link and create a couple *to-do* items.</span></span> 

![새 ASP.NET 프로젝트 대화 상자](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

<span data-ttu-id="116c0-131">테스트 hello **편집**, **세부 정보**, 및 **삭제** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-131">Test hello **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="116c0-132">hello 앱 hello 데이터베이스와 데이터베이스 컨텍스트 tooconnect를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-132">hello app uses a database context tooconnect with hello database.</span></span> <span data-ttu-id="116c0-133">Hello 데이터베이스 컨텍스트를이 샘플에서는 명명 된 연결 문자열을 사용 `MyDbConnection`합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-133">In this sample, hello database context uses a connection string named `MyDbConnection`.</span></span> <span data-ttu-id="116c0-134">연결 문자열 hello hello에 설정 되어 *Web.config* 파일과에 언급 된 hello *Models/MyDatabaseContext.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-134">hello connection string is set in hello *Web.config* file and referenced in hello *Models/MyDatabaseContext.cs* file.</span></span> <span data-ttu-id="116c0-135">hello 자습서 tooconnect hello Azure 웹 앱 tooan Azure SQL 데이터베이스의 뒷부분에 나오는 hello 연결 문자열 이름이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-135">hello connection string name is used later in hello tutorial tooconnect hello Azure web app tooan Azure SQL Database.</span></span> 

## <a name="publish-tooazure-with-sql-database"></a><span data-ttu-id="116c0-136">SQL 데이터베이스와 tooAzure 게시</span><span class="sxs-lookup"><span data-stu-id="116c0-136">Publish tooAzure with SQL Database</span></span>

<span data-ttu-id="116c0-137">Hello에 **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 하면 **DotNetAppSqlDb** 프로젝트를 마우스 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-137">In hello **Solution Explorer**, right-click your **DotNetAppSqlDb** project and select **Publish**.</span></span>

![솔루션 탐색기에서 게시](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

<span data-ttu-id="116c0-139">**Microsoft Azure App Service**를 선택했는지 확인하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-139">Make sure that **Microsoft Azure App Service** is selected and click **Publish**.</span></span>

![프로젝트 개요 페이지에서 게시](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

<span data-ttu-id="116c0-141">게시 열립니다 hello **응용 프로그램 서비스 만들기** 대화 상자에서 만들 모든 해줍니다 hello toorun Azure에서 ASP.NET 웹 앱을 필요한 Azure 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-141">Publishing opens hello **Create App Service** dialog, which helps you create all hello Azure resources you need toorun your ASP.NET web app in Azure.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="116c0-142">TooAzure에 로그인</span><span class="sxs-lookup"><span data-stu-id="116c0-142">Sign in tooAzure</span></span>

<span data-ttu-id="116c0-143">Hello에 **응용 프로그램 서비스 만들기** 대화 상자에서 클릭 **계정 추가**, tooyour Azure 구독에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-143">In hello **Create App Service** dialog, click **Add an account**, and then sign in tooyour Azure subscription.</span></span> <span data-ttu-id="116c0-144">이미 Microsoft 계정에 로그인한 경우 계정에 Azure 구독이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-144">If you're already signed into a Microsoft account, make sure that account holds your Azure subscription.</span></span> <span data-ttu-id="116c0-145">Microsoft 계정 로그인 hello 없는 경우 Azure 구독, tooadd hello에 대 한 올바른 계정을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-145">If hello signed-in Microsoft account doesn't have your Azure subscription, click it tooadd hello correct account.</span></span>
   
![TooAzure에 로그인](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

<span data-ttu-id="116c0-147">로그인 한 후이 대화 상자에 Azure 웹 앱에 필요한 리소스를 모두 hello 준비 toocreate 것입니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-147">Once signed in, you're ready toocreate all hello resources you need for your Azure web app in this dialog.</span></span>

### <a name="configure-hello-web-app-name"></a><span data-ttu-id="116c0-148">Hello 웹 응용 프로그램 이름 구성</span><span class="sxs-lookup"><span data-stu-id="116c0-148">Configure hello web app name</span></span>

<span data-ttu-id="116c0-149">생성 된 hello 웹 응용 프로그램 이름, 유지 하거나 tooanother 고유 이름을 변경할 수 있습니다 (유효한 문자는 `a-z`, `0-9`, 및 `-`).</span><span class="sxs-lookup"><span data-stu-id="116c0-149">You can keep hello generated web app name, or change it tooanother unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="116c0-150">hello 웹 앱 이름은 앱에 대 한 hello 기본 URL의 일부로 사용 됩니다 (`<app_name>.azurewebsites.net`여기서 `<app_name>` 웹 응용 프로그램 이름).</span><span class="sxs-lookup"><span data-stu-id="116c0-150">hello web app name is used as part of hello default URL for your app (`<app_name>.azurewebsites.net`, where `<app_name>` is your web app name).</span></span> <span data-ttu-id="116c0-151">웹 앱 이름은 hello 필요 toobe 고유 Azure에서 모든 앱 간에 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-151">hello web app name needs toobe unique across all apps in Azure.</span></span> 

![앱 서비스 만들기 대화 상자](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a><span data-ttu-id="116c0-153">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="116c0-153">Create a resource group</span></span>

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="116c0-154">다음 너무**리소스 그룹**, 클릭 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-154">Next too**Resource Group**, click **New**.</span></span>

![다음 tooResource 그룹에서 새로 만들기를 클릭 합니다.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

<span data-ttu-id="116c0-156">Hello 리소스 그룹 이름 **myResourceGroup**합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-156">Name hello resource group **myResourceGroup**.</span></span>

> [!NOTE]
> <span data-ttu-id="116c0-157">**만들기**는 클릭하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="116c0-157">Do not click **Create**.</span></span> <span data-ttu-id="116c0-158">먼저 tooset 이후 단계에서 SQL 데이터베이스를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-158">You first need tooset up a SQL Database in a later step.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="116c0-159">App Service 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="116c0-159">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="116c0-160">다음 너무**앱 서비스 계획**, 클릭 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-160">Next too**App Service Plan**, click **New**.</span></span> 

<span data-ttu-id="116c0-161">Hello에 **앱 서비스 계획 구성** 대화 상자에서 다음 설정을 hello로 hello 새 앱 서비스 계획을 구성:</span><span class="sxs-lookup"><span data-stu-id="116c0-161">In hello **Configure App Service Plan** dialog, configure hello new App Service plan with hello following settings:</span></span>

![App Service 계획 만들기](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| <span data-ttu-id="116c0-163">설정</span><span class="sxs-lookup"><span data-stu-id="116c0-163">Setting</span></span>  | <span data-ttu-id="116c0-164">제안 값</span><span class="sxs-lookup"><span data-stu-id="116c0-164">Suggested value</span></span> | <span data-ttu-id="116c0-165">Blob에 대한 자세한 내용은</span><span class="sxs-lookup"><span data-stu-id="116c0-165">For more information</span></span> |
| ----------------- | ------------ | ----|
|<span data-ttu-id="116c0-166">**App Service 계획**</span><span class="sxs-lookup"><span data-stu-id="116c0-166">**App Service Plan**</span></span>| <span data-ttu-id="116c0-167">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="116c0-167">myAppServicePlan</span></span> | [<span data-ttu-id="116c0-168">App Service 계획</span><span class="sxs-lookup"><span data-stu-id="116c0-168">App Service plans</span></span>](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|<span data-ttu-id="116c0-169">**위치**</span><span class="sxs-lookup"><span data-stu-id="116c0-169">**Location**</span></span>| <span data-ttu-id="116c0-170">서유럽</span><span class="sxs-lookup"><span data-stu-id="116c0-170">West Europe</span></span> | [<span data-ttu-id="116c0-171">Azure 지역</span><span class="sxs-lookup"><span data-stu-id="116c0-171">Azure regions</span></span>](https://azure.microsoft.com/regions/) |
|<span data-ttu-id="116c0-172">**크기**</span><span class="sxs-lookup"><span data-stu-id="116c0-172">**Size**</span></span>| <span data-ttu-id="116c0-173">무료</span><span class="sxs-lookup"><span data-stu-id="116c0-173">Free</span></span> | [<span data-ttu-id="116c0-174">가격 책정 계층</span><span class="sxs-lookup"><span data-stu-id="116c0-174">Pricing tiers</span></span>](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a><span data-ttu-id="116c0-175">SQL Server 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="116c0-175">Create a SQL Server instance</span></span>

<span data-ttu-id="116c0-176">먼저 [Azure SQL Database 논리 서버](../sql-database/sql-database-features.md)가 있어야 데이터베이스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-176">Before creating a database, you need an [Azure SQL Database logical server](../sql-database/sql-database-features.md).</span></span> <span data-ttu-id="116c0-177">논리 서버는 그룹으로 관리되는 데이터베이스 그룹을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-177">A logical server contains a group of databases managed as a group.</span></span>

<span data-ttu-id="116c0-178">**추가 Azure 서비스 탐색**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-178">Select **Explore additional Azure services**.</span></span>

![웹앱 이름 구성](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

<span data-ttu-id="116c0-180">Hello에 **서비스** 탭에서 hello  **+**  아이콘 다음 너무**SQL 데이터베이스**합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-180">In hello **Services** tab, click hello **+** icon next too**SQL Database**.</span></span> 

![Hello 서비스 탭 hello + 아이콘을 클릭 다음 tooSQL 데이터베이스입니다.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

<span data-ttu-id="116c0-182">Hello에 **SQL 데이터베이스를 구성** 대화 상자를 클릭 하 여 **새로** 다음 너무**SQL Server**합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-182">In hello **Configure SQL Database** dialog, click **New** next too**SQL Server**.</span></span> 

<span data-ttu-id="116c0-183">고유한 서버 이름이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-183">A unique server name is generated.</span></span> <span data-ttu-id="116c0-184">이 이름은 논리 서버에 대 한 hello 기본 URL의 일부로 사용 됩니다 `<server_name>.database.windows.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-184">This name is used as part of hello default URL for your logical server, `<server_name>.database.windows.net`.</span></span> <span data-ttu-id="116c0-185">Azure의 모든 논리 서버 인스턴스에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-185">It must be unique across all logical server instances in Azure.</span></span> <span data-ttu-id="116c0-186">Hello 서버 이름을 변경할 수 있지만이 자습서에 대 한 hello 생성 된 값을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-186">You can change hello server name, but for this tutorial, keep hello generated value.</span></span>

<span data-ttu-id="116c0-187">관리자 사용자 이름과 암호를 추가한 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-187">Add an administrator username and password, and then select **OK**.</span></span> <span data-ttu-id="116c0-188">암호 복잡성 요구 사항은 [암호 정책](/sql/relational-databases/security/password-policy)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="116c0-188">For password complexity requirements, see [Password Policy](/sql/relational-databases/security/password-policy).</span></span>

<span data-ttu-id="116c0-189">이 사용자 이름과 암호를 기억해 두세요.</span><span class="sxs-lookup"><span data-stu-id="116c0-189">Remember this username and password.</span></span> <span data-ttu-id="116c0-190">Toomanage hello 논리 서버를 필요한 나중 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="116c0-190">You need them toomanage hello logical server instance later.</span></span>

![SQL Server 인스턴스 만들기](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a><span data-ttu-id="116c0-192">SQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="116c0-192">Create a SQL Database</span></span>

<span data-ttu-id="116c0-193">Hello에 **SQL 데이터베이스를 구성** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="116c0-193">In hello **Configure SQL Database** dialog:</span></span> 

* <span data-ttu-id="116c0-194">생성 된 hello 기본 유지 **데이터베이스 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-194">Keep hello default generated **Database Name**.</span></span>
* <span data-ttu-id="116c0-195">**연결 문자열 이름**에 *MyDbConnection*을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-195">In **Connection String Name**, type *MyDbConnection*.</span></span> <span data-ttu-id="116c0-196">이 이름은 hello 연결 문자열에서 참조 되는 같아야 합니다. *Models/MyDatabaseContext.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-196">This name must match hello connection string that is referenced in *Models/MyDatabaseContext.cs*.</span></span>
* <span data-ttu-id="116c0-197">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-197">Select **OK**.</span></span>

![SQL Database 구성](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

<span data-ttu-id="116c0-199">hello **응용 프로그램 서비스 만들기** 대화 상자에 만든 hello 리소스 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-199">hello **Create App Service** dialog shows hello resources you've created.</span></span> <span data-ttu-id="116c0-200">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-200">Click **Create**.</span></span> 

![만든 hello 리소스](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

<span data-ttu-id="116c0-202">Hello 마법사 hello Azure 리소스 만들기를 완료 한 후에 ASP.NET 응용 프로그램 tooAzure 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-202">Once hello wizard finishes creating hello Azure resources, it  publishes your ASP.NET app tooAzure.</span></span> <span data-ttu-id="116c0-203">기본 브라우저 hello URL toohello 배포 응용 프로그램으로 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-203">Your default browser is launched with hello URL toohello deployed app.</span></span> 

<span data-ttu-id="116c0-204">몇 가지 할 일 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-204">Add a few to-do items.</span></span>

![Azure 웹앱의 게시된 ASP.NET 응용 프로그램](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="116c0-206">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-206">Congratulations!</span></span> <span data-ttu-id="116c0-207">데이터 기반 ASP.NET 응용 프로그램이 Azure App Service에서 라이브로 실행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-207">Your data-driven ASP.NET application is running live in Azure App Service.</span></span>

## <a name="access-hello-sql-database-locally"></a><span data-ttu-id="116c0-208">로컬로 hello SQL 데이터베이스에 액세스</span><span class="sxs-lookup"><span data-stu-id="116c0-208">Access hello SQL Database locally</span></span>

<span data-ttu-id="116c0-209">Visual Studio를 사용 하면 탐색 및 hello에서 쉽게 새 SQL 데이터베이스 관리 **SQL Server 개체 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-209">Visual Studio lets you explore and manage your new SQL Database easily in hello **SQL Server Object Explorer**.</span></span>

### <a name="create-a-database-connection"></a><span data-ttu-id="116c0-210">데이터베이스 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="116c0-210">Create a database connection</span></span>

<span data-ttu-id="116c0-211">Hello에서 **보기** 메뉴 선택 **SQL Server 개체 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-211">From hello **View** menu, select **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="116c0-212">Hello 위쪽에 **SQL Server 개체 탐색기**, hello 클릭 **SQL Server 추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-212">At hello top of **SQL Server Object Explorer**, click hello **Add SQL Server** button.</span></span>

### <a name="configure-hello-database-connection"></a><span data-ttu-id="116c0-213">Hello 데이터베이스 연결 구성</span><span class="sxs-lookup"><span data-stu-id="116c0-213">Configure hello database connection</span></span>

<span data-ttu-id="116c0-214">Hello에 **연결** 대화 상자에서 hello 확장 **Azure** 노드.</span><span class="sxs-lookup"><span data-stu-id="116c0-214">In hello **Connect** dialog, expand hello **Azure** node.</span></span> <span data-ttu-id="116c0-215">여기서는 Azure의 모든 SQL Database 인스턴스가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-215">All your SQL Database instances in Azure are listed here.</span></span>

<span data-ttu-id="116c0-216">선택 hello `DotNetAppSqlDb` SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-216">Select hello `DotNetAppSqlDb` SQL Database.</span></span> <span data-ttu-id="116c0-217">앞에서 만든 hello 연결 hello 맨 아래에 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-217">hello connection you created earlier is automatically filled at hello bottom.</span></span>

<span data-ttu-id="116c0-218">앞에서 만든 hello 데이터베이스 관리자 암호를 입력 하 고 클릭 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-218">Type hello database administrator password you created earlier and click **Connect**.</span></span>

![Visual Studio에서 데이터베이스 연결 구성](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a><span data-ttu-id="116c0-220">컴퓨터에서 클라이언트 연결 허용</span><span class="sxs-lookup"><span data-stu-id="116c0-220">Allow client connection from your computer</span></span>

<span data-ttu-id="116c0-221">hello **새 방화벽 규칙 만들기** 대화 상자를 열입니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-221">hello **Create a new firewall rule** dialog is opened.</span></span> <span data-ttu-id="116c0-222">기본적으로 SQL Database 인스턴스는 Azure 웹앱과 같은 Azure 서비스의 연결만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-222">By default, your SQL Database instance only allows connections from Azure services, such as your Azure web app.</span></span> <span data-ttu-id="116c0-223">tooconnect tooyour 데이터베이스, SQL 데이터베이스 인스턴스의 hello 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-223">tooconnect tooyour database, create a firewall rule in hello SQL Database instance.</span></span> <span data-ttu-id="116c0-224">hello 방화벽 규칙에는 로컬 컴퓨터의 공용 IP 주소를 hello 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-224">hello firewall rule allows hello public IP address of your local computer.</span></span>

<span data-ttu-id="116c0-225">hello 대화는 컴퓨터의 공용 IP 주소가 이미 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-225">hello dialog is already filled with your computer's public IP address.</span></span>

<span data-ttu-id="116c0-226">**내 클라이언트 IP 추가**가 선택되어 있는지 확인하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-226">Make sure that **Add my client IP** is selected and click **OK**.</span></span> 

![SQL Database 인스턴스에 대한 방화벽 설정](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

<span data-ttu-id="116c0-228">연결에 표시 SQL 데이터베이스 인스턴스에 대 한 hello 방화벽 설정을 만들어 Visual Studio 완료 되 면 **SQL Server 개체 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-228">Once Visual Studio finishes creating hello firewall setting for your SQL Database instance, your connection shows up in **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="116c0-229">여기에서 수행할 수 있습니다 hello 가장 데이터베이스와 같은 일반적인 작업이 실행된 된 쿼리를 뷰 및 저장된 프로시저를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-229">Here, you can perform hello most common database operations, such as run queries, create views and stored procedures, and more.</span></span> 

<span data-ttu-id="116c0-230">Hello를 마우스 오른쪽 단추로 클릭 `Todoes` 테이블을 선택한 **데이터 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-230">Right-click on hello `Todoes` table and select **View Data**.</span></span> 

![SQL Database 개체 탐색](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a><span data-ttu-id="116c0-232">Code First 마이그레이션으로 앱 업데이트</span><span class="sxs-lookup"><span data-stu-id="116c0-232">Update app with Code First Migrations</span></span>

<span data-ttu-id="116c0-233">Azure의 hello tooupdate Visual Studio의에서 친숙 한 도구 데이터베이스 및 웹 앱을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-233">You can use hello familiar tools in Visual Studio tooupdate your database and web app in Azure.</span></span> <span data-ttu-id="116c0-234">Entity Framework toomake 변경 tooyour 데이터베이스 스키마에서에서 Code First 마이그레이션을 사용 하 여이 단계에서는 tooAzure 게시 하십시오.</span><span class="sxs-lookup"><span data-stu-id="116c0-234">In this step, you use Code First Migrations in Entity Framework toomake a change tooyour database schema and publish it tooAzure.</span></span>

<span data-ttu-id="116c0-235">Entity Framework Code First 마이그레이션 사용에 대한 자세한 내용은 [MVC 5를 사용하여 Entity Framework 6 Code First 시작](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="116c0-235">For more information about using Entity Framework Code First Migrations, see [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="update-your-data-model"></a><span data-ttu-id="116c0-236">데이터 모델 업데이트</span><span class="sxs-lookup"><span data-stu-id="116c0-236">Update your data model</span></span>

<span data-ttu-id="116c0-237">열기 _Models\Todo.cs_ hello 코드 편집기에서.</span><span class="sxs-lookup"><span data-stu-id="116c0-237">Open _Models\Todo.cs_ in hello code editor.</span></span> <span data-ttu-id="116c0-238">다음 속성 toohello hello 추가 `ToDo` 클래스:</span><span class="sxs-lookup"><span data-stu-id="116c0-238">Add hello following property toohello `ToDo` class:</span></span>

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a><span data-ttu-id="116c0-239">Code First 마이그레이션을 로컬에서 실행</span><span class="sxs-lookup"><span data-stu-id="116c0-239">Run Code First Migrations locally</span></span>

<span data-ttu-id="116c0-240">몇 가지 명령을 toomake 업데이트 tooyour 로컬 데이터베이스를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-240">Run a few commands toomake updates tooyour local database.</span></span> 

<span data-ttu-id="116c0-241">Hello에서 **도구** 메뉴를 클릭 하 여 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-241">From hello **Tools** menu, click **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="116c0-242">Hello 패키지 관리자 콘솔 창에서에서 Code First 마이그레이션을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-242">In hello Package Manager Console window, enable Code First Migrations:</span></span>

```PowerShell
Enable-Migrations
```

<span data-ttu-id="116c0-243">마이그레이션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-243">Add a migration:</span></span>

```PowerShell
Add-Migration AddProperty
```

<span data-ttu-id="116c0-244">Hello 로컬 데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-244">Update hello local database:</span></span>

```PowerShell
Update-Database
```

<span data-ttu-id="116c0-245">형식 `Ctrl+F5` toorun hello 앱.</span><span class="sxs-lookup"><span data-stu-id="116c0-245">Type `Ctrl+F5` toorun hello app.</span></span> <span data-ttu-id="116c0-246">테스트 hello 세부 정보를 편집 및 링크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-246">Test hello edit, details, and create links.</span></span>

<span data-ttu-id="116c0-247">Hello 응용 프로그램 오류 없이 로드 됨, Code First 마이그레이션이 성공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-247">If hello application loads without errors, then Code First Migrations has succeeded.</span></span> <span data-ttu-id="116c0-248">그러나 페이지 여전히 찾습니다 hello 응용 프로그램 논리를이 새 속성을 아직 사용 하지 않으므로 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-248">However, your page still looks hello same because your application logic is not using this new property yet.</span></span> 

### <a name="use-hello-new-property"></a><span data-ttu-id="116c0-249">Hello 새 속성을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="116c0-249">Use hello new property</span></span>

<span data-ttu-id="116c0-250">코드 toouse hello에 대 한 일부 변경 `Done` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-250">Make some changes in your code toouse hello `Done` property.</span></span> <span data-ttu-id="116c0-251">이 자습서에서는 간단한 설명을 위해만 거 toochange hello `Index` 및 `Create` 보기 toosee hello 속성을 실행에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-251">For simplicity in this tutorial, you're only going toochange hello `Index` and `Create` views toosee hello property in action.</span></span>

<span data-ttu-id="116c0-252">_Controllers\TodosController.cs_를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-252">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="116c0-253">Hello `Create()` 메서드 추가 `Done` hello 속성 목록이 toohello `Bind` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-253">Find hello `Create()` method and add `Done` toohello list of properties in hello `Bind` attribute.</span></span> <span data-ttu-id="116c0-254">완료 되 면 프로그램 `Create()` 메서드 시그니처 코드 다음 hello 같습니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-254">When you're done, your `Create()` method signature looks like hello following code:</span></span>

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

<span data-ttu-id="116c0-255">_Views\Todos\Create.cshtml_을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-255">Open _Views\Todos\Create.cshtml_.</span></span>

<span data-ttu-id="116c0-256">Hello Razor 코드에에서 표시 됩니다는 `<div class="form-group">` 를 사용 하는 요소 `model.Description`, 다음 또 다른 `<div class="form-group">` 를 사용 하는 요소 `model.CreatedDate`합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-256">In hello Razor code, you should see a `<div class="form-group">` element that uses `model.Description`, and then another `<div class="form-group">` element that uses `model.CreatedDate`.</span></span> <span data-ttu-id="116c0-257">이러한 두 요소 바로 뒤에 `model.Done`을 사용하는 또 다른 `<div class="form-group">` 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-257">Immediately following these two elements, add another `<div class="form-group">` element that uses `model.Done`:</span></span>

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

<span data-ttu-id="116c0-258">_Views\Todos\Index.cshtml_을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-258">Open _Views\Todos\Index.cshtml_.</span></span>

<span data-ttu-id="116c0-259">빈 hello에 대 한 검색 `<th></th>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-259">Search for hello empty `<th></th>` element.</span></span> <span data-ttu-id="116c0-260">이 요소 위에 바로 hello Razor 코드 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-260">Just above this element, add hello following Razor code:</span></span>

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

<span data-ttu-id="116c0-261">Hello `<td>` hello 포함 된 요소 `Html.ActionLink()` 도우미 메서드.</span><span class="sxs-lookup"><span data-stu-id="116c0-261">Find hello `<td>` element that contains hello `Html.ActionLink()` helper methods.</span></span> <span data-ttu-id="116c0-262">이 요소 위에 바로 hello Razor 코드 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-262">Just above this element, add hello following Razor code:</span></span>

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

<span data-ttu-id="116c0-263">Hello toosee hello 변경 하면 이것이 `Index` 및 `Create` 보기.</span><span class="sxs-lookup"><span data-stu-id="116c0-263">That's all you need toosee hello changes in hello `Index` and `Create` views.</span></span> 

<span data-ttu-id="116c0-264">형식 `Ctrl+F5` toorun hello 앱.</span><span class="sxs-lookup"><span data-stu-id="116c0-264">Type `Ctrl+F5` toorun hello app.</span></span>

<span data-ttu-id="116c0-265">이제 할 일 항목을 추가하고 **완료**를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-265">You can now add a to-do item and check **Done**.</span></span> <span data-ttu-id="116c0-266">그러면 홈페이지에 완료된 항목으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-266">Then it should show up in your homepage as a completed item.</span></span> <span data-ttu-id="116c0-267">해당 hello 기억 `Edit` 보기 hello 표시 되지 않는 `Done` hello를 변경 하지 않은 때문에 필드 `Edit` 보기.</span><span class="sxs-lookup"><span data-stu-id="116c0-267">Remember that hello `Edit` view doesn't show hello `Done` field, because you didn't change hello `Edit` view.</span></span>

### <a name="enable-code-first-migrations-in-azure"></a><span data-ttu-id="116c0-268">Azure에서 Code First 마이그레이션 사용</span><span class="sxs-lookup"><span data-stu-id="116c0-268">Enable Code First Migrations in Azure</span></span>

<span data-ttu-id="116c0-269">코드 변경, 데이터베이스 migration을 비롯 한 했으므로 tooyour Azure web app을 게시 하 고 너무 Code First 마이그레이션을 사용 하면 SQL 데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-269">Now that your code change works, including database migration, you publish it tooyour Azure web app and update your SQL Database with Code First Migrations too.</span></span>

<span data-ttu-id="116c0-270">이전과 마찬가지로 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-270">Just like before, right-click your project and select **Publish**.</span></span>

<span data-ttu-id="116c0-271">클릭 **설정을** tooopen hello 게시 마법사.</span><span class="sxs-lookup"><span data-stu-id="116c0-271">Click **Settings** tooopen hello publish wizard.</span></span>

![게시 설정 열기](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

<span data-ttu-id="116c0-273">Hello 마법사에서 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-273">In hello wizard, click **Next**.</span></span>

<span data-ttu-id="116c0-274">하는지 확인 한 hello 연결 문자열을 SQL 데이터베이스에 채워진 **MyDatabaseContext (MyDbConnection)**합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-274">Make sure that hello connection string for your SQL Database is populated in **MyDatabaseContext (MyDbConnection)**.</span></span> <span data-ttu-id="116c0-275">Tooselect hello 야 **myToDoAppDb** hello 드롭다운에서 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="116c0-275">You may need tooselect hello **myToDoAppDb** database from hello dropdown.</span></span> 

<span data-ttu-id="116c0-276">**Execute Code First Migrations (runs on application start)**(Code First 마이그레이션 실행(응용 프로그램 시작 시 실행))를 선택한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-276">Select **Execute Code First Migrations (runs on application start)**, then click **Save**.</span></span>

![Azure 웹앱에서 Code First 마이그레이션 사용](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a><span data-ttu-id="116c0-278">변경 내용 게시</span><span class="sxs-lookup"><span data-stu-id="116c0-278">Publish your changes</span></span>

<span data-ttu-id="116c0-279">이제 Azure 웹앱에서 Code First 마이그레이션을 사용하도록 설정했으므로 코드 변경 내용을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-279">Now that you enabled Code First Migrations in your Azure web app, publish your code changes.</span></span>

<span data-ttu-id="116c0-280">Hello 게시 페이지, 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-280">In hello publish page, click **Publish**.</span></span>

<span data-ttu-id="116c0-281">할 일 항목 추가를 다시 시도하고 **Done**(완료)을 선택합니다. 그러면 홈페이지에 완료된 항목으로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-281">Try adding to-do items again and select **Done**, and they should show up in your homepage as a completed item.</span></span>

![Code First 마이그레이션 후 Azure 웹앱](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

<span data-ttu-id="116c0-283">기존의 모든 할 일 항목이 계속 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-283">All your existing to-do items are still displayed.</span></span> <span data-ttu-id="116c0-284">ASP.NET 응용 프로그램을 다시 게시해도 SQL Database의 기존 데이터가 손실되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-284">When you republish your ASP.NET application, existing data in your SQL Database is not lost.</span></span> <span data-ttu-id="116c0-285">Code First 마이그레이션을 hello 데이터 스키마만 변경 되는 또한 기존 데이터를 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-285">Also, Code First Migrations only changes hello data schema and leaves your existing data intact.</span></span>


## <a name="stream-application-logs"></a><span data-ttu-id="116c0-286">응용 프로그램 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="116c0-286">Stream application logs</span></span>

<span data-ttu-id="116c0-287">Azure 웹 앱 tooVisual Studio에서 직접 추적 메시지를 스트리밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-287">You can stream tracing messages directly from your Azure web app tooVisual Studio.</span></span>

<span data-ttu-id="116c0-288">_Controllers\TodosController.cs_를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-288">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="116c0-289">각 동작은 `Trace.WriteLine()` 메서드로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-289">Each action starts with a `Trace.WriteLine()` method.</span></span> <span data-ttu-id="116c0-290">이 코드가 tooshow 추가 하면 어떻게 tooadd 추적 메시지 tooyour Azure 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-290">This code is added tooshow you how tooadd trace messages tooyour Azure web app.</span></span>

### <a name="open-server-explorer"></a><span data-ttu-id="116c0-291">서버 탐색기 열기</span><span class="sxs-lookup"><span data-stu-id="116c0-291">Open Server Explorer</span></span>

<span data-ttu-id="116c0-292">Hello에서 **보기** 메뉴 선택 **서버 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-292">From hello **View** menu, select **Server Explorer**.</span></span> <span data-ttu-id="116c0-293">**서버 탐색기**에서 Azure 웹앱에 대한 로깅을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-293">You can configure logging for your Azure web app in **Server Explorer**.</span></span> 

### <a name="enable-log-streaming"></a><span data-ttu-id="116c0-294">로그 스트리밍 사용</span><span class="sxs-lookup"><span data-stu-id="116c0-294">Enable log streaming</span></span>

<span data-ttu-id="116c0-295">**서버 탐색기**에서 **Azure** > **App Service**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-295">In **Server Explorer**, expand **Azure** > **App Service**.</span></span>

<span data-ttu-id="116c0-296">Hello 확장 **myResourceGroup** hello Azure 웹 앱을 처음 만들 때 만든 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-296">Expand hello **myResourceGroup** resource group, you created when you first created hello Azure web app.</span></span>

<span data-ttu-id="116c0-297">Azure 웹앱을 마우스 오른쪽 단추로 클릭하고 **스트리밍 로그 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-297">Right-click your Azure web app and select **View Streaming Logs**.</span></span>

![로그 스트리밍 사용](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

<span data-ttu-id="116c0-299">hello 로그 이제 스트리밍되거나 hello에 **출력** 창.</span><span class="sxs-lookup"><span data-stu-id="116c0-299">hello logs are now streamed into hello **Output** window.</span></span> 

![출력 창에서 로그 스트리밍](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

<span data-ttu-id="116c0-301">그러나 표시 되지 않으면 hello 추적 메시지 중 하나가 아직 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-301">However, you don't see any of hello trace messages yet.</span></span> <span data-ttu-id="116c0-302">먼저 선택 하므로 **스트리밍 로그 보기**, Azure 웹 앱 설정 hello 추적 수준이 너무`Error`만 오류 이벤트를 기록 하 (hello로 `Trace.TraceError()` 메서드).</span><span class="sxs-lookup"><span data-stu-id="116c0-302">That's because when you first select **View Streaming Logs**, your Azure web app sets hello trace level too`Error`, which only logs error events (with hello `Trace.TraceError()` method).</span></span>

### <a name="change-trace-levels"></a><span data-ttu-id="116c0-303">추적 수준 변경</span><span class="sxs-lookup"><span data-stu-id="116c0-303">Change trace levels</span></span>

<span data-ttu-id="116c0-304">toochange hello 추적 수준을 toooutput 이동 다른 추적 메시지 다시 너무**서버 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-304">toochange hello trace levels toooutput other trace messages, go back too**Server Explorer**.</span></span>

<span data-ttu-id="116c0-305">Azure 웹앱을 마우스 오른쪽 단추로 다시 클릭하고 **설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-305">Right-click your Azure web app again and select **Settings**.</span></span>

<span data-ttu-id="116c0-306">Hello에 **응용 프로그램 로깅 (파일 시스템)** 드롭다운 **Verbose**합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-306">In hello **Application Logging (File System)** dropdown, select **Verbose**.</span></span> <span data-ttu-id="116c0-307">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-307">Click **Save**.</span></span>

![추적 수준 tooVerbose 변경](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> <span data-ttu-id="116c0-309">각 수준에 대해 표시 되는 메시지 유형을 다양 한 추적 수준 toosee를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-309">You can experiment with different trace levels toosee what types of messages are displayed for each level.</span></span> <span data-ttu-id="116c0-310">예를 들어 hello **정보** 수준에서 만들어진 모든 로그에 포함 됩니다. `Trace.TraceInformation()`, `Trace.TraceWarning()`, 및 `Trace.TraceError()`, 하지만에서 만들어진 로그 하지 `Trace.WriteLine()`합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-310">For example, hello **Information** level includes all logs created by `Trace.TraceInformation()`, `Trace.TraceWarning()`, and `Trace.TraceError()`, but not logs created by `Trace.WriteLine()`.</span></span>
>
>

<span data-ttu-id="116c0-311">브라우저에서 Azure의 hello 할 일 목록 응용 프로그램 주위의 클릭 하십시오.</span><span class="sxs-lookup"><span data-stu-id="116c0-311">In your browser, try clicking around hello to-do list application in Azure.</span></span> <span data-ttu-id="116c0-312">hello 추적 메시지 toohello 스트리밍되거나 이제 **출력** Visual Studio의 창.</span><span class="sxs-lookup"><span data-stu-id="116c0-312">hello trace messages are now streamed toohello **Output** window in Visual Studio.</span></span>

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a><span data-ttu-id="116c0-313">로그 스트리밍 중지</span><span class="sxs-lookup"><span data-stu-id="116c0-313">Stop log streaming</span></span>

<span data-ttu-id="116c0-314">toostop 로그 스트리밍 서비스 hello, hello 클릭 **모니터링을 중지** hello 단추 **출력** 창.</span><span class="sxs-lookup"><span data-stu-id="116c0-314">toostop hello log-streaming service, click hello **Stop monitoring** button in hello **Output** window.</span></span>

![로그 스트리밍 중지](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="116c0-316">Azure Web App 관리</span><span class="sxs-lookup"><span data-stu-id="116c0-316">Manage your Azure web app</span></span>

<span data-ttu-id="116c0-317">Toohello 이동 [Azure 포털](https://portal.azure.com) 만든 toosee hello 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-317">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span> 



<span data-ttu-id="116c0-318">Hello 왼쪽된 메뉴에서 클릭 **앱 서비스**, Azure 웹 앱의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-318">From hello left menu, click **App Service**, then click hello name of your Azure web app.</span></span>

![포털 탐색 tooAzure 웹 응용 프로그램](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

<span data-ttu-id="116c0-320">웹앱 페이지에 연결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-320">You have landed in your web app's page.</span></span> 

<span data-ttu-id="116c0-321">기본적으로 hello 포털 표시 hello **개요** 페이지.</span><span class="sxs-lookup"><span data-stu-id="116c0-321">By default, hello portal shows hello **Overview** page.</span></span> <span data-ttu-id="116c0-322">이 페이지에서는 앱이 어떻게 작동하고 있는지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-322">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="116c0-323">여기에서 찾아보기, 중지, 시작, 다시 시작, 삭제와 같은 기본 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-323">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="116c0-324">hello hello 페이지의 왼쪽에 hello 탭 hello 서로 다른 구성 페이지를 열 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-324">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span> 

![Azure Portal의 App Service 페이지](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="116c0-326">다음 단계</span><span class="sxs-lookup"><span data-stu-id="116c0-326">Next steps</span></span>

<span data-ttu-id="116c0-327">이 자습서에서 학습한 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-327">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="116c0-328">Azure에서 SQL Database 만들기</span><span class="sxs-lookup"><span data-stu-id="116c0-328">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="116c0-329">ASP.NET 응용 프로그램 tooSQL 데이터베이스 연결</span><span class="sxs-lookup"><span data-stu-id="116c0-329">Connect an ASP.NET app tooSQL Database</span></span>
> * <span data-ttu-id="116c0-330">Hello 앱 tooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="116c0-330">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="116c0-331">Hello 데이터 모델을 업데이트 하 고 hello 응용 프로그램을 다시 배포</span><span class="sxs-lookup"><span data-stu-id="116c0-331">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="116c0-332">Azure tooyour 터미널에서 스트림 로그</span><span class="sxs-lookup"><span data-stu-id="116c0-332">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="116c0-333">Hello Azure 포털에서에서 hello 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="116c0-333">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="116c0-334">다음 자습서 toolearn toohello 진행 방법을 사용자 지정 DNS toomap toohello 웹 앱의 이름을 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c0-334">Advance toohello next tutorial toolearn how toomap a custom DNS name toohello web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="116c0-335">지도 기존 사용자 지정 DNS 이름 tooAzure 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="116c0-335">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
