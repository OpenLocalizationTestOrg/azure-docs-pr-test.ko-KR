---
title: "aaaCreate tooMongoDB 가상 컴퓨터에서 실행을 연결 하는 Azure에서 웹 응용 프로그램"
description: "ASP.NET 응용 프로그램 tooAzure 응용 프로그램 서비스를 연결 하는 toouse Git toodeploy 방법에 대해 설명 하는 자습서는 Azure 가상 컴퓨터에서 tooMongoDB 합니다."
tags: azure-portal
services: app-service\web, virtual-machines
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: adf7a472-ae00-45a8-aec4-06247e21318b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: cephalin
ms.openlocfilehash: 1f5f42c28c3c294d92c9ebf1499374931d47c010
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-azure-that-connects-toomongodb-running-on-a-virtual-machine"></a><span data-ttu-id="da738-103">가상 컴퓨터에서 실행 tooMongoDB 연결 하는 Azure에서 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="da738-103">Create a web app in Azure that connects tooMongoDB running on a virtual machine</span></span>
<span data-ttu-id="da738-104">Git를 사용 하 여 ASP.NET 응용 프로그램 tooAzure 앱 서비스 웹 앱을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da738-104">Using Git, you can deploy an ASP.NET application tooAzure App Service Web Apps.</span></span> <span data-ttu-id="da738-105">이 자습서에서는 간단한 프런트 엔드 ASP.NET MVC Azure의 가상 컴퓨터에서 실행 되는 tooa MongoDB 데이터베이스를 연결 하는 작업 목록 응용 프로그램을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-105">In this tutorial, you will build a simple front-end ASP.NET MVC task list application that connects tooa MongoDB database running on a virtual machine in Azure.</span></span>  <span data-ttu-id="da738-106">[MongoDB][MongoDB]는 인기 있는 고성능 오픈 소스 NoSQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="da738-106">[MongoDB][MongoDB] is a popular open source, high performance NoSQL database.</span></span> <span data-ttu-id="da738-107">테스트 개발 컴퓨터에 hello ASP.NET 응용 프로그램을 실행 한 후 hello 응용 프로그램 tooApp 서비스 웹 앱을 업로드 Git를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-107">After running and testing hello ASP.NET application on your development computer, you will upload hello application tooApp Service Web Apps using Git.</span></span>

> [!NOTE]
> <span data-ttu-id="da738-108">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-108">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="da738-109">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="da738-109">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="background-knowledge"></a><span data-ttu-id="da738-110">배경 지식</span><span class="sxs-lookup"><span data-stu-id="da738-110">Background knowledge</span></span>
<span data-ttu-id="da738-111">Hello 다음에 대 한 지식이 필요 하지 않습니다 이지만이 자습서에서는 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-111">Knowledge of hello following is useful for this tutorial, though not required:</span></span>

* <span data-ttu-id="da738-112">MongoDB에 대 한 C# hello 드라이버입니다.</span><span class="sxs-lookup"><span data-stu-id="da738-112">hello C# driver for MongoDB.</span></span> <span data-ttu-id="da738-113">MongoDB에 대 한 C# 응용 프로그램 개발 방법에 대 한 자세한 내용은 참조 hello MongoDB [CSharp 언어 센터][MongoC#LangCenter]합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-113">For more information on developing C# applications against MongoDB, see hello MongoDB [CSharp Language Center][MongoC#LangCenter].</span></span> 
* <span data-ttu-id="da738-114">hello ASP.NET 웹 응용 프로그램 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="da738-114">hello ASP .NET web application framework.</span></span> <span data-ttu-id="da738-115">Hello에 대해 모든 알 수 있습니다 [ASP.net 웹 사이트][ASP.NET]합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-115">You can learn all about it at hello [ASP.net website][ASP.NET].</span></span>
* <span data-ttu-id="da738-116">hello ASP.NET MVC 웹 응용 프로그램 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="da738-116">hello ASP .NET MVC web application framework.</span></span> <span data-ttu-id="da738-117">Hello에 대해 모든 알 수 있습니다 [ASP.NET MVC 웹 사이트][MVCWebSite]합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-117">You can learn all about it at hello [ASP.NET MVC website][MVCWebSite].</span></span>
* <span data-ttu-id="da738-118">Azure.</span><span class="sxs-lookup"><span data-stu-id="da738-118">Azure.</span></span> <span data-ttu-id="da738-119">[Azure][WindowsAzure]의 내용을 읽어 보고 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da738-119">You can get started reading at [Azure][WindowsAzure].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da738-120">필수 조건</span><span class="sxs-lookup"><span data-stu-id="da738-120">Prerequisites</span></span>
* <span data-ttu-id="da738-121">[Visual Studio Express 2013 for Web][VSEWeb] 또는 [Visual Studio 2013][VSUlt]</span><span class="sxs-lookup"><span data-stu-id="da738-121">[Visual Studio Express 2013 for Web][VSEWeb] or [Visual Studio 2013][VSUlt]</span></span>
* [<span data-ttu-id="da738-122">Azure SDK for .NET</span><span class="sxs-lookup"><span data-stu-id="da738-122">Azure SDK for .NET</span></span>](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* <span data-ttu-id="da738-123">활성 Microsoft Azure 구독</span><span class="sxs-lookup"><span data-stu-id="da738-123">An active Microsoft Azure subscription</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a><span data-ttu-id="da738-124">가상 컴퓨터 만들기 및 MongoDB 설치</span><span class="sxs-lookup"><span data-stu-id="da738-124">Create a virtual machine and install MongoDB</span></span>
<span data-ttu-id="da738-125">이 자습서는 Azure에서 가상 컴퓨터를 만든 적이 있는 개발자를 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-125">This tutorial assumes you have created a virtual machine in Azure.</span></span> <span data-ttu-id="da738-126">Hello 가상 컴퓨터를 만든 후 tooinstall MongoDB hello 가상 컴퓨터에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-126">After creating hello virtual machine you need tooinstall MongoDB on hello virtual machine:</span></span>

* <span data-ttu-id="da738-127">toocreate Windows 가상 컴퓨터와 설치 MongoDB, 참조 [Azure에서 Windows Server를 실행 중인 가상 컴퓨터에 설치 MongoDB][InstallMongoOnWindowsVM]합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-127">toocreate a Windows virtual machine and install MongoDB, see [Install MongoDB on a virtual machine running Windows Server in Azure][InstallMongoOnWindowsVM].</span></span>

<span data-ttu-id="da738-128">Azure의 hello 가상 컴퓨터를 만들어 하면 MongoDB 설치 후 있는지 tooremember hello DNS 이름 이어야 hello 가상 컴퓨터 (예: "testlinuxvm.cloudapp.net")와 hello 외부 포트의 hello 끝점에 지정한 MongoDB에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-128">After you have created hello virtual machine in Azure and installed MongoDB, be sure tooremember hello DNS name of hello virtual machine ("testlinuxvm.cloudapp.net", for example) and hello external port for MongoDB that you specified in hello endpoint.</span></span>  <span data-ttu-id="da738-129">Hello 자습서의 뒷부분에서이 정보가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-129">You will need this information later in hello tutorial.</span></span>

<a id="createapp"></a>

## <a name="create-hello-application"></a><span data-ttu-id="da738-130">Hello 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="da738-130">Create hello application</span></span>
<span data-ttu-id="da738-131">이 섹션에서는 Visual Studio를 사용 하 여 "My 작업 목록" 이라고 하는 ASP.NET 응용 프로그램 만들고 초기 배포 tooAzure 앱 서비스 웹 앱을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-131">In this section you will create an ASP.NET application called "My Task List" by using Visual Studio and perform an initial deployment tooAzure App Service Web Apps.</span></span> <span data-ttu-id="da738-132">Hello 응용 프로그램을 로컬로 실행할 하지만 tooyour 가상 컴퓨터를 Azure에 연결 되며 hello MongoDB 만든 인스턴스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-132">You will run hello application locally, but it will connect tooyour virtual machine on Azure and use hello MongoDB instance that you created there.</span></span>

1. <span data-ttu-id="da738-133">Visual Studio에서 **새 프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-133">In Visual Studio, click **New Project**.</span></span>
   
    ![시작 페이지 새 프로젝트][StartPageNewProject]
2. <span data-ttu-id="da738-135">Hello에 **새 프로젝트** 창의 hello 왼쪽된 창에서 **Visual C#**를 선택한 후 **웹**합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-135">In hello **New Project** window, in hello left pane, select **Visual C#**, and then select **Web**.</span></span> <span data-ttu-id="da738-136">Hello 가운데 창에서 선택 **ASP.NET 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-136">In hello middle pane, select **ASP.NET  Web Application**.</span></span> <span data-ttu-id="da738-137">Hello 맨 아래에 "MyTaskListApp" 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-137">At hello bottom, name your project "MyTaskListApp," and then click **OK**.</span></span>
   
    ![새 프로젝트 대화 상자][NewProjectMyTaskListApp]
3. <span data-ttu-id="da738-139">Hello에 **새 ASP.NET 프로젝트** 대화 상자에서 **MVC**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-139">In hello **New ASP.NET Project** dialog box, select **MVC**, and then click **OK**.</span></span>
   
    ![MVC 템플릿 선택][VS2013SelectMVCTemplate]
4. <span data-ttu-id="da738-141">Microsoft Azure에 로그인 하지 않은 경우에 증명된 toosign 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da738-141">If you aren't already signed into Microsoft Azure, you will be prompted toosign in.</span></span> <span data-ttu-id="da738-142">Azure에 hello 프롬프트 toosign를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="da738-142">Follow hello prompts toosign into Azure.</span></span>
5. <span data-ttu-id="da738-143">로그인한 후 앱 서비스 웹 앱 구성을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da738-143">Once you are signed in, you can start configuring your App Service web app.</span></span> <span data-ttu-id="da738-144">Hello 지정 **웹 응용 프로그램 이름**, **앱 서비스 계획**, **리소스 그룹**, 및 **지역**, 클릭 **만들기**.</span><span class="sxs-lookup"><span data-stu-id="da738-144">Specify hello **Web App name**, **App Service plan**, **Resource group**, and **Region**, then click **Create**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. <span data-ttu-id="da738-145">Hello 프로젝트 생성 되 면 hello 웹 응용 프로그램 toobe hello에 표시 된 대로 Azure 앱 서비스에서 만든 대기 **Azure 앱 서비스 활동** 창.</span><span class="sxs-lookup"><span data-stu-id="da738-145">After hello project creation completes, wait for hello web app toobe created in Azure App Service as indicated in hello **Azure App Service Activity** window.</span></span> <span data-ttu-id="da738-146">클릭 **웹 응용 프로그램 게시 MyTaskListApp toothis을 이제**합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-146">Then, click **Publish MyTaskListApp toothis Web App now**.</span></span>
7. <span data-ttu-id="da738-147">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-147">Click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    <span data-ttu-id="da738-148">기본 ASP.NET 응용 프로그램 게시 tooAzure 앱 서비스 웹 앱 되 면 hello 브라우저에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da738-148">Once your default ASP.NET application is published tooAzure App Service Web Apps, it will be launched in hello browser.</span></span>

## <a name="install-hello-mongodb-c-driver"></a><span data-ttu-id="da738-149">Hello MongoDB C# 드라이버 설치</span><span class="sxs-lookup"><span data-stu-id="da738-149">Install hello MongoDB C# driver</span></span>
<span data-ttu-id="da738-150">MongoDB에 필요한 드라이버를 통해 C# 응용 프로그램에 대 한 클라이언트 쪽 지원을 제공 tooinstall 로컬 개발 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da738-150">MongoDB offers client-side support for C# applications through a driver, which you need tooinstall on your local development computer.</span></span> <span data-ttu-id="da738-151">hello C# 드라이버는 NuGet을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da738-151">hello C# driver is available through NuGet.</span></span>

<span data-ttu-id="da738-152">tooinstall hello MongoDB C# 드라이버:</span><span class="sxs-lookup"><span data-stu-id="da738-152">tooinstall hello MongoDB C# driver:</span></span>

1. <span data-ttu-id="da738-153">**솔루션 탐색기**, 마우스 오른쪽 단추로 클릭 hello **MyTaskListApp** 프로젝트를 마우스 선택 **관리 NuGetPackages**합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-153">In **Solution Explorer**, right-click hello **MyTaskListApp** project and select **Manage NuGetPackages**.</span></span>
   
    ![NuGet 패키지 관리][VS2013ManageNuGetPackages]
2. <span data-ttu-id="da738-155">Hello에 **NuGet 패키지 관리** 창의 hello 왼쪽된 창에서 클릭 **온라인**합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-155">In hello **Manage NuGet Packages** window, in hello left pane, click **Online**.</span></span> <span data-ttu-id="da738-156">Hello에 **온라인 검색** hello 오른쪽에 상자 "mongodb.driver"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-156">In hello **Search Online** box on hello right, type "mongodb.driver".</span></span>  <span data-ttu-id="da738-157">클릭 **설치** tooinstall hello 드라이버입니다.</span><span class="sxs-lookup"><span data-stu-id="da738-157">Click **Install** tooinstall hello driver.</span></span>
   
    ![MongoDB C# 드라이버 검색][SearchforMongoDBCSharpDriver]
3. <span data-ttu-id="da738-159">클릭 **동의** tooaccept hello 10gen, Inc. 사용 조건.</span><span class="sxs-lookup"><span data-stu-id="da738-159">Click **I Accept** tooaccept hello 10gen, Inc. license terms.</span></span>
4. <span data-ttu-id="da738-160">클릭 **닫기** hello 드라이버 설치 후에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da738-160">Click **Close** after hello driver has installed.</span></span>
    <span data-ttu-id="da738-161">![MongoDB C# 드라이버 설치][MongoDBCsharpDriverInstalled]</span><span class="sxs-lookup"><span data-stu-id="da738-161">![MongoDB C# Driver Installed][MongoDBCsharpDriverInstalled]</span></span>

<span data-ttu-id="da738-162">hello MongoDB C# 드라이버가 설치 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="da738-162">hello MongoDB C# driver is now installed.</span></span>  <span data-ttu-id="da738-163">참조 toohello **MongoDB.Bson**, **MongoDB.Driver**, 및 **MongoDB.Driver.Core** 라이브러리 toohello 프로젝트 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="da738-163">References toohello **MongoDB.Bson**, **MongoDB.Driver**, and **MongoDB.Driver.Core**  libraries have been added toohello project.</span></span>

![MongoDB C# 드라이버 참조][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a><span data-ttu-id="da738-165">모델 추가</span><span class="sxs-lookup"><span data-stu-id="da738-165">Add a model</span></span>
<span data-ttu-id="da738-166">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 hello *모델* 폴더 및 **추가** 새 **클래스** 하 고 이름을 *TaskModel.cs* .</span><span class="sxs-lookup"><span data-stu-id="da738-166">In **Solution Explorer**, right-click hello *Models* folder and **Add** a new **Class** and name it *TaskModel.cs*.</span></span>  <span data-ttu-id="da738-167">*TaskModel.cs*, 코드 다음 hello hello 기존 코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="da738-167">In *TaskModel.cs*, replace hello existing code with hello following code:</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MongoDB.Bson.Serialization.Attributes;
    using MongoDB.Bson.Serialization.IdGenerators;
    using MongoDB.Bson;

    namespace MyTaskListApp.Models
    {
        public class MyTask
        {
            [BsonId(IdGenerator = typeof(CombGuidGenerator))]
            public Guid Id { get; set; }

            [BsonElement("Name")]
            public string Name { get; set; }

            [BsonElement("Category")]
            public string Category { get; set; }

            [BsonElement("Date")]
            public DateTime Date { get; set; }

            [BsonElement("CreatedDate")]
            public DateTime CreatedDate { get; set; }

        }
    }

## <a name="add-hello-data-access-layer"></a><span data-ttu-id="da738-168">Hello 데이터 액세스 계층 추가</span><span class="sxs-lookup"><span data-stu-id="da738-168">Add hello data access layer</span></span>
<span data-ttu-id="da738-169">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 hello *MyTaskListApp* 프로젝트 및 **추가** 는 **새 폴더** 라는 *DAL*.</span><span class="sxs-lookup"><span data-stu-id="da738-169">In **Solution Explorer**, right-click hello *MyTaskListApp* project and **Add** a **New Folder** named *DAL*.</span></span>  <span data-ttu-id="da738-170">마우스 오른쪽 단추로 클릭 hello *DAL* 폴더 및 **추가** 새 **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-170">Right-click hello *DAL* folder and **Add** a new **Class**.</span></span> <span data-ttu-id="da738-171">Hello 클래스 파일 이름 *Dal.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-171">Name hello class file *Dal.cs*.</span></span>  <span data-ttu-id="da738-172">*Dal.cs*, 코드 다음 hello hello 기존 코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="da738-172">In *Dal.cs*, replace hello existing code with hello following code:</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MyTaskListApp.Models;
    using MongoDB.Driver;
    using MongoDB.Bson;
    using System.Configuration;


    namespace MyTaskListApp
    {
        public class Dal : IDisposable
        {
            private MongoServer mongoServer = null;
            private bool disposed = false;

            // toodo: update hello connection string with hello DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net"
            private string connectionString = "mongodb://mongodbsrv20151211.cloudapp.net";

            // This sample uses a database named "Tasks" and a 
            //collection named "TasksList".  hello database and collection 
            //will be automatically created if they don't already exist.
            private string dbName = "Tasks";
            private string collectionName = "TasksList";

            // Default constructor.        
            public Dal()
            {
            }

            // Gets all Task items from hello MongoDB server.        
            public List<MyTask> GetAllTasks()
            {
                try
                {
                    var collection = GetTasksCollection();
                    return collection.Find(new BsonDocument()).ToList();
                }
                catch (MongoConnectionException)
                {
                    return new List<MyTask>();
                }
            }

            // Creates a Task and inserts it into hello collection in MongoDB.
            public void CreateTask(MyTask task)
            {
                var collection = GetTasksCollectionForEdit();
                try
                {
                    collection.InsertOne(task);
                }
                catch (MongoCommandException ex)
                {
                    string msg = ex.Message;
                }
            }

            private IMongoCollection<MyTask> GetTasksCollection()
            {
                MongoClient client = new MongoClient(connectionString);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }

            private IMongoCollection<MyTask> GetTasksCollectionForEdit()
            {
                MongoClient client = new MongoClient(connectionString);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }

            # region IDisposable

            public void Dispose()
            {
                this.Dispose(true);
                GC.SuppressFinalize(this);
            }

            protected virtual void Dispose(bool disposing)
            {
                if (!this.disposed)
                {
                    if (disposing)
                    {
                        if (mongoServer != null)
                        {
                            this.mongoServer.Disconnect();
                        }
                    }
                }

                this.disposed = true;
            }

            # endregion
        }
    }

## <a name="add-a-controller"></a><span data-ttu-id="da738-173">컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="da738-173">Add a controller</span></span>
<span data-ttu-id="da738-174">열기 hello *Controllers\HomeController.cs* 파일 **솔루션 탐색기** hello 기존 코드 hello 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="da738-174">Open hello *Controllers\HomeController.cs* file in **Solution Explorer** and replace hello existing code with hello following:</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.Mvc;
    using MyTaskListApp.Models;
    using System.Configuration;

    namespace MyTaskListApp.Controllers
    {
        public class HomeController : Controller, IDisposable
        {
            private Dal dal = new Dal();
            private bool disposed = false;
            //
            // GET: /MyTask/

            public ActionResult Index()
            {
                return View(dal.GetAllTasks());
            }

            //
            // GET: /MyTask/Create

            public ActionResult Create()
            {
                return View();
            }

            //
            // POST: /MyTask/Create

            [HttpPost]
            public ActionResult Create(MyTask task)
            {
                try
                {
                    dal.CreateTask(task);
                    return RedirectToAction("Index");
                }
                catch
                {
                    return View();
                }
            }

            public ActionResult About()
            {
                return View();
            }

            # region IDisposable

            new protected void Dispose()
            {
                this.Dispose(true);
                GC.SuppressFinalize(this);
            }

            new protected virtual void Dispose(bool disposing)
            {
                if (!this.disposed)
                {
                    if (disposing)
                    {
                        this.dal.Dispose();
                    }
                }

                this.disposed = true;
            }

            # endregion

        }
    }

## <a name="set-up-hello-styles"></a><span data-ttu-id="da738-175">Hello 스타일 설정</span><span class="sxs-lookup"><span data-stu-id="da738-175">Set up hello styles</span></span>
<span data-ttu-id="da738-176">페이지 hello open hello hello 위에 toochange hello 제목을 *Views\Shared\\_Layout.cshtml* 파일 **솔루션 탐색기** 바꾸고 "응용 프로그램 이름" hello navbar 헤더에 "내 작업 응용 프로그램을 나열 "다음과 같이 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-176">toochange hello title at hello top of hello page, open hello *Views\Shared\\_Layout.cshtml* file in **Solution Explorer** and replace "Application name" in hello navbar header with "My Task List Application" so that it looks like this:</span></span>

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

<span data-ttu-id="da738-177">순서 tooset hello 작업 목록 메뉴를 열고 hello *\Views\Home\Index.cshtml* 파일 및 코드 다음 hello hello 기존 코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="da738-177">In order tooset up hello Task List menu, open hello *\Views\Home\Index.cshtml* file and replace hello existing code with hello following code:</span></span>

    @model IEnumerable<MyTaskListApp.Models.MyTask>

    @{
        ViewBag.Title = "My Task List";
    }

    <h2>My Task List</h2>

    <table border="1">
        <tr>
            <th>Task</th>
            <th>Category</th>
            <th>Date</th>

        </tr>

    @foreach (var item in Model) {
        <tr>
            <td>
                @Html.DisplayFor(modelItem => item.Name)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Category)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Date)
            </td>

        </tr>
    }

    </table>
    <div>  @Html.Partial("Create", new MyTaskListApp.Models.MyTask())</div>


<span data-ttu-id="da738-178">새 작업을 tooadd hello 기능 toocreate hello를 마우스 오른쪽 단추로 클릭 *Views\Home\\*  폴더 및 **추가** 는 **보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-178">tooadd hello ability toocreate a new task, right-click hello *Views\Home\\* folder and **Add** a **View**.</span></span>  <span data-ttu-id="da738-179">Hello 뷰의 이름을 *만들기*합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-179">Name hello view *Create*.</span></span> <span data-ttu-id="da738-180">Hello 다음과 같이 hello 코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="da738-180">Replace hello code with hello following:</span></span>

    @model MyTaskListApp.Models.MyTask

    <script src="@Url.Content("~/Scripts/jquery-1.10.2.min.js")" type="text/javascript"></script>
    <script src="@Url.Content("~/Scripts/jquery.validate.min.js")" type="text/javascript"></script>
    <script src="@Url.Content("~/Scripts/jquery.validate.unobtrusive.min.js")" type="text/javascript"></script>

    @using (Html.BeginForm("Create", "Home")) {
        @Html.ValidationSummary(true)
        <fieldset>
            <legend>New Task</legend>

            <div class="editor-label">
                @Html.LabelFor(model => model.Name)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Name)
                @Html.ValidationMessageFor(model => model.Name)
            </div>

            <div class="editor-label">
                @Html.LabelFor(model => model.Category)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Category)
                @Html.ValidationMessageFor(model => model.Category)
            </div>

            <div class="editor-label">
                @Html.LabelFor(model => model.Date)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Date)
                @Html.ValidationMessageFor(model => model.Date)
            </div>

            <p>
                <input type="submit" value="Create" />
            </p>
        </fieldset>
    }

<span data-ttu-id="da738-181">**솔루션 탐색기** 가 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="da738-181">**Solution Explorer** should look like this:</span></span>

![솔루션 탐색기][SolutionExplorerMyTaskListApp]

## <a name="set-hello-mongodb-connection-string"></a><span data-ttu-id="da738-183">Hello MongoDB 연결 문자열 설정</span><span class="sxs-lookup"><span data-stu-id="da738-183">Set hello MongoDB connection string</span></span>
<span data-ttu-id="da738-184">**솔루션 탐색기**개방형 hello *DAL/Dal.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="da738-184">In **Solution Explorer**, open hello *DAL/Dal.cs* file.</span></span> <span data-ttu-id="da738-185">다음 코드 줄을 hello를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="da738-185">Find hello following line of code:</span></span>

    private string connectionString = "mongodb://<vm-dns-name>";

<span data-ttu-id="da738-186">대체 `<vm-dns-name>` hello에서 만든 MongoDB를 실행 하는 hello 가상 컴퓨터의 hello DNS 이름을 가진 [가상 컴퓨터를 만들고 설치 MongoDB] [ Create a virtual machine and install MongoDB] 이 자습서의 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="da738-186">Replace `<vm-dns-name>` with hello DNS name of hello virtual machine running MongoDB you created in hello [Create a virtual machine and install MongoDB][Create a virtual machine and install MongoDB] step of this tutorial.</span></span>  <span data-ttu-id="da738-187">가상 컴퓨터의 toofind hello DNS 이름을 toohello Azure 포털에서 선택 이동 **가상 컴퓨터**, 했는데 **DNS 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-187">toofind hello DNS name of your virtual machine, go toohello Azure Portal, select **Virtual Machines**, and find **DNS Name**.</span></span>

<span data-ttu-id="da738-188">Hello 가상 컴퓨터의 DNS 이름을 hello "testlinuxvm.cloudapp.net" 이며 MongoDB 27017 hello 기본 포트에서 수신 대기 하는 경우 코드의 연결 문자열 줄 hello 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da738-188">If hello DNS name of hello virtual machine is "testlinuxvm.cloudapp.net" and MongoDB is listening on hello default port 27017, hello connection string line of code will look like:</span></span>

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

<span data-ttu-id="da738-189">MongoDB에 대 한 다른 외부 포트를 지정 하는 hello 가상 컴퓨터 끝점을 hello 연결 문자열의 hello 포트 지정을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da738-189">If hello virtual machine endpoint specifies a different external port for MongoDB, you can specifiy hello port in hello connection string:</span></span>

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

<span data-ttu-id="da738-190">MongoDB 연결 문자열에 대한 자세한 내용은 [연결][MongoConnectionStrings](영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da738-190">For more information on MongoDB connection strings, see [Connections][MongoConnectionStrings].</span></span>

## <a name="test-hello-local-deployment"></a><span data-ttu-id="da738-191">Hello 로컬 배포를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-191">Test hello local deployment</span></span>
<span data-ttu-id="da738-192">toorun 개발 컴퓨터에 응용 프로그램 선택 **디버깅 시작** hello에서 **디버그** 메뉴 또는 적중 **F5**합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-192">toorun your application on your development computer, select **Start Debugging** from hello **Debug** menu or hit **F5**.</span></span> <span data-ttu-id="da738-193">IIS Express를 시작 하 고 브라우저를 열고 hello 응용 프로그램의 홈 페이지를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-193">IIS Express starts and a browser opens and launches hello application's home page.</span></span>  <span data-ttu-id="da738-194">Azure에서 가상 컴퓨터에서 실행 되는 toohello MongoDB 데이터베이스 추가 되는 새 작업을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da738-194">You can add a new task, which will be added toohello MongoDB database running on your virtual machine in Azure.</span></span>

![My Task List 응용 프로그램][TaskListAppBlank]

## <a name="publish-tooazure-app-service-web-apps"></a><span data-ttu-id="da738-196">TooAzure 앱 서비스 웹 앱 게시</span><span class="sxs-lookup"><span data-stu-id="da738-196">Publish tooAzure App Service Web Apps</span></span>
<span data-ttu-id="da738-197">이 섹션에 변경 내용을 tooAzure 앱 서비스 웹 앱을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-197">In this section you will publish your changes tooAzure App Service Web Apps.</span></span>

1. <span data-ttu-id="da738-198">솔루션 탐색기에서 **MyTaskListApp**을 마우스 오른쪽 단추로 클릭하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-198">In Solution Explorer, right-click **MyTaskListApp** again and click **Publish**.</span></span>
2. <span data-ttu-id="da738-199">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-199">Click **Publish**.</span></span>
   
    <span data-ttu-id="da738-200">Azure 앱 서비스에서 실행 되 고 Azure 가상 컴퓨터의 hello MongoDB 데이터베이스에 액세스 하 여 웹 응용 프로그램을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da738-200">You should now see your web app running in Azure App Service and accessing hello MongoDB database in Azure Virtual Machines.</span></span>

## <a name="summary"></a><span data-ttu-id="da738-201">요약</span><span class="sxs-lookup"><span data-stu-id="da738-201">Summary</span></span>
<span data-ttu-id="da738-202">이제 ASP.NET 응용 프로그램 tooAzure 앱 서비스 웹 앱 성공적으로 배포 했습니다.</span><span class="sxs-lookup"><span data-stu-id="da738-202">You have now successfully deployed your ASP.NET application tooAzure App Service Web Apps.</span></span> <span data-ttu-id="da738-203">tooview hello 웹 앱:</span><span class="sxs-lookup"><span data-stu-id="da738-203">tooview hello web app:</span></span>

1. <span data-ttu-id="da738-204">Hello Azure 포털에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-204">Log into hello Azure Portal.</span></span>
2. <span data-ttu-id="da738-205">**웹 앱**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da738-205">Click **Web apps**.</span></span> 
3. <span data-ttu-id="da738-206">Hello에서 웹 앱 선택 **웹 앱** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="da738-206">Select your web app in hello **Web Apps** list.</span></span>

<span data-ttu-id="da738-207">MongoDB에 대한 C# 응용 프로그램 개발에 대한 자세한 내용은 [CSharp 언어 센터][MongoC#LangCenter](영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da738-207">For more information on developing C# applications against MongoDB, see [CSharp Language Center][MongoC#LangCenter].</span></span> 

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- HYPERLINKS -->

[AzurePortal]: http://manage.windowsazure.com
[WindowsAzure]: http://www.windowsazure.com
[MongoC#LangCenter]: http://docs.mongodb.org/ecosystem/drivers/csharp/
[MVCWebSite]: http://www.asp.net/mvc
[ASP.NET]: http://www.asp.net/
[MongoConnectionStrings]: http://www.mongodb.org/display/DOCS/Connections
[MongoDB]: http://www.mongodb.org
[InstallMongoOnWindowsVM]:../virtual-machines/windows/classic/install-mongodb.md
[VSEWeb]: http://www.microsoft.com/visualstudio/eng/2013-downloads#d-2013-express
[VSUlt]: http://www.microsoft.com/visualstudio/eng/2013-downloads

<!-- IMAGES -->


[StartPageNewProject]: ./media/web-sites-dotnet-store-data-mongodb-vm/NewProject.png
[NewProjectMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/NewProjectMyTaskListApp.png
[VS2013SelectMVCTemplate]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013SelectMVCTemplate.png
[VS2013DefaultMVCApplication]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013DefaultMVCApplication.png
[VS2013ManageNuGetPackages]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013ManageNuGetPackages.png
[SearchforMongoDBCSharpDriver]: ./media/web-sites-dotnet-store-data-mongodb-vm/SearchforMongoDBCSharpDriver.png
[MongoDBCsharpDriverInstalled]: ./media/web-sites-dotnet-store-data-mongodb-vm/MongoDBCsharpDriverInstalled.png
[MongoDBCSharpDriverReferences]: ./media/web-sites-dotnet-store-data-mongodb-vm/MongoDBCSharpDriverReferences.png
[SolutionExplorerMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/SolutionExplorerMyTaskListApp.png
[TaskListAppBlank]: ./media/web-sites-dotnet-store-data-mongodb-vm/TaskListAppBlank.png
[WAWSCreateWebSite]: ./media/web-sites-dotnet-store-data-mongodb-vm/WAWSCreateWebSite.png
[WAWSDashboardMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/WAWSDashboardMyTaskListApp.png
[Image9]: ./media/web-sites-dotnet-store-data-mongodb-vm/RepoReady.png
[Image10]: ./media/web-sites-dotnet-store-data-mongodb-vm/GitInstructions.png
[Image11]: ./media/web-sites-dotnet-store-data-mongodb-vm/GitDeploymentComplete.png

<!-- TOC BOOKMARKS -->
[Create a virtual machine and install MongoDB]: #virtualmachine
[Create and run hello My Task List ASP.NET application on your development computer]: #createapp
[Create an Azure web site]: #createwebsite
[Deploy hello ASP.NET application toohello web site using Git]: #deployapp
