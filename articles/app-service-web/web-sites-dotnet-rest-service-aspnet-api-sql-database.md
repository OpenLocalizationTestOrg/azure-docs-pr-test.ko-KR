---
title: "ASP.NET 및 SQL DB를 사용 하 여 Azure에서 REST API aaaCreate | Microsoft Docs"
description: "자습서를 참조 하는 방법을 배웁니다 toodeploy 응용 프로그램을 사용 하 여 Visual Studio를 사용 하 여 ASP.NET Web API tooan Azure 웹 앱을 hello 하는 방법을."
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
writer: Rick-Anderson
manager: erikre
editor: 
ms.assetid: f4916fc0-ea08-41f7-846b-73e41bc88149
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: riande
ms.openlocfilehash: 1ef45dd1582bfda367e53c39f863164422ad678b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a><span data-ttu-id="73945-103">Azure 앱 서비스에서 ASP.NET Web API 및 SQL 데이터베이스를 사용하여 REST 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="73945-103">Create a REST service using ASP.NET Web API and SQL Database in Azure App Service</span></span>
<span data-ttu-id="73945-104">이 자습서에서는 어떻게 toodeploy ASP.NET 웹 응용 프로그램 tooan [Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714) Visual Studio 2013 또는 Visual Studio 2013 Community Edition hello 웹 게시 마법사를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-104">This tutorial shows how toodeploy an ASP.NET web app tooan [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by using hello Publish Web wizard in Visual Studio 2013 or Visual Studio 2013 Community Edition.</span></span> 

<span data-ttu-id="73945-105">Azure 계정이 있으세요을 무료, 열 수 있으며 hello SDK Web Express에 대 한 Visual Studio 2013를 자동으로 설치 Visual Studio 2013, 아직 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="73945-105">You can open an Azure account for free, and if you don't already have Visual Studio 2013, hello SDK automatically installs Visual Studio 2013 for Web Express.</span></span> <span data-ttu-id="73945-106">따라서 Azure용 개발을 무료로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73945-106">So you can start developing for Azure entirely for free.</span></span>

<span data-ttu-id="73945-107">이 자습서에서는 이전에 Azure를 사용한 경험이 없다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-107">This tutorial assumes that you have no prior experience using Azure.</span></span> <span data-ttu-id="73945-108">이 자습서를 완료를 단순한 웹 앱 및 hello 클라우드에서 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-108">On completing this tutorial, you'll have a simple web app up and running in hello cloud.</span></span>

<span data-ttu-id="73945-109">다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="73945-109">You'll learn:</span></span>

* <span data-ttu-id="73945-110">어떻게 tooenable 시스템에 설치 하 여 Azure 개발 hello Azure SDK입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-110">How tooenable your machine for Azure development by installing hello Azure SDK.</span></span>
* <span data-ttu-id="73945-111">어떻게 toocreate Visual Studio ASP.NET MVC 5 프로젝트 및 tooan Azure 응용 프로그램을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-111">How toocreate a Visual Studio ASP.NET MVC 5 project and publish it tooan Azure app.</span></span>
* <span data-ttu-id="73945-112">Toouse hello ASP.NET Web API tooenable Restful API 호출 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-112">How toouse hello ASP.NET Web API tooenable Restful API calls.</span></span>
* <span data-ttu-id="73945-113">어떻게 toouse SQL 데이터베이스는 Azure에서 toostore 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-113">How toouse a SQL database toostore data in Azure.</span></span>
* <span data-ttu-id="73945-114">Toopublish 응용 프로그램 tooAzure 업데이트 하는 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-114">How toopublish application updates tooAzure.</span></span>

<span data-ttu-id="73945-115">ASP.NET MVC 5를 기반으로 하는 간단한 대화 상대 목록 웹 응용 프로그램을 빌드하게 됩니다 및 사용 하 여 데이터베이스 액세스를 위해 ADO.NET Entity Framework hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-115">You'll build a simple contact list web application that is built on ASP.NET MVC 5 and uses hello ADO.NET Entity Framework for database access.</span></span> <span data-ttu-id="73945-116">다음 그림에서는 hello hello 완료 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="73945-116">hello following illustration shows hello completed application:</span></span>

![웹 사이트의 스크린샷][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-hello-project"></a><span data-ttu-id="73945-118">Hello 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="73945-118">Create hello project</span></span>
1. <span data-ttu-id="73945-119">Visual Studio 2013을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-119">Start Visual Studio 2013.</span></span>
2. <span data-ttu-id="73945-120">Hello에서 **파일** 메뉴 클릭 **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-120">From hello **File** menu click **New Project**.</span></span>
3. <span data-ttu-id="73945-121">Hello에 **새 프로젝트** 대화 상자에서 **Visual C#** 선택 **웹** 선택한 후 **ASP.NET 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-121">In hello **New Project** dialog box, expand **Visual C#** and select **Web**  and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="73945-122">Hello 응용 프로그램 이름을 **ContactManager** 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-122">Name hello application **ContactManager** and click **OK**.</span></span>
   
    ![새 프로젝트 대화 상자](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. <span data-ttu-id="73945-124">Hello에 **새 ASP.NET 프로젝트** 대화 상자, 선택 hello **MVC** 서식 파일을 검사 **웹 API** 클릭 하 고 **인증 변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-124">In hello **New ASP.NET Project** dialog box, select hello **MVC** template, check **Web API** and then click **Change Authentication**.</span></span>
5. <span data-ttu-id="73945-125">Hello에 **인증 변경** 대화 상자를 클릭 **인증 안 함**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-125">In hello **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span>
   
    ![인증 없음](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    <span data-ttu-id="73945-127">만드는 hello 샘플 응용 프로그램에서 사용자가 toolog 요구 하는 기능 없을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73945-127">hello sample application you're creating won't have features that require users toolog in.</span></span> <span data-ttu-id="73945-128">방법에 대 한 내용은 tooimplement 인증 및 권한 부여 기능 참조 hello [다음 단계](#nextsteps) hello 끝이 자습서에는 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-128">For information about how tooimplement authentication and authorization features, see hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span> 
6. <span data-ttu-id="73945-129">Hello에 **새 ASP.NET 프로젝트** 대화 상자에서 확인 되었는지 hello **호스트 클라우드 hello에** 선택 되 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-129">In hello **New ASP.NET Project** dialog box, make sure hello **Host in hello Cloud** is checked and click **OK**.</span></span>

<span data-ttu-id="73945-130">이전에 tooAzure에 등록 하지 않은 경우에 증명된 toosign 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73945-130">If you have not previously signed in tooAzure, you will be prompted toosign in.</span></span>

1. <span data-ttu-id="73945-131">hello 구성 마법사는 기반으로 고유 이름을 제안 *ContactManager* (hello 이미지 아래 참조).</span><span class="sxs-lookup"><span data-stu-id="73945-131">hello configuration wizard will suggest a unique name based on *ContactManager* (see hello image below).</span></span> <span data-ttu-id="73945-132">근처에 있는 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-132">Select a region near you.</span></span> <span data-ttu-id="73945-133">사용할 수 있습니다 [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") toofind hello 가장 낮은 대기 시간 데이터 센터입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-133">You can use [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") toofind hello lowest latency data center.</span></span> 
2. <span data-ttu-id="73945-134">기존에 만든 데이터베이스 서버가 없으면 **새 서버 만들기**를 선택하고 데이터베이스 사용자 이름과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-134">If you haven't created a database server before, select **Create new server**, enter a database user name and password.</span></span>
   
    ![Azure 웹 사이트 구성](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

<span data-ttu-id="73945-136">데이터베이스 서버를 설정한 경우 해당 toocreate 새 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-136">If you have a database server, use that toocreate a new database.</span></span> <span data-ttu-id="73945-137">일반적으로 원하는 toocreate hello에 있는 여러 데이터베이스 및 데이터베이스 서버는 소중한 리소스를 테스트 및 개발 아닌 데이터베이스 마다 데이터베이스 서버를 만드는 동일한 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-137">Database servers are a precious resource, and you generally want toocreate multiple databases on hello same server for testing and development rather than creating a database server per database.</span></span> <span data-ttu-id="73945-138">웹 사이트 및 데이터베이스에에서 있어야 hello 동일한 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-138">Make sure your web site and database are in hello same region.</span></span>

![Azure 웹 사이트 구성](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-hello-page-header-and-footer"></a><span data-ttu-id="73945-140">Hello 페이지 머리글 및 바닥글을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-140">Set hello page header and footer</span></span>
1. <span data-ttu-id="73945-141">**솔루션 탐색기**, hello 확장 *Views\Shared* 폴더를 열고 hello *_Layout.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-141">In **Solution Explorer**, expand hello *Views\Shared* folder and open hello *_Layout.cshtml* file.</span></span>
   
    ![솔루션 탐색기의 _Layout.cshtml][newapp004]
2. <span data-ttu-id="73945-143">Hello hello 내용 바꾸기 *Views\Shared_Layout.cshtml* 코드 다음 hello로 파일:</span><span class="sxs-lookup"><span data-stu-id="73945-143">Replace hello contents of hello *Views\Shared_Layout.cshtml* file with hello following code:</span></span>

        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="utf-8" />
            <title>@ViewBag.Title - Contact Manager</title>
            <link href="~/favicon.ico" rel="shortcut icon" type="image/x-icon" />
            <meta name="viewport" content="width=device-width" />
            @Styles.Render("~/Content/css")
            @Scripts.Render("~/bundles/modernizr")
        </head>
        <body>
            <header>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p class="site-title">@Html.ActionLink("Contact Manager", "Index", "Home")</p>
                    </div>
                </div>
            </header>
            <div id="body">
                @RenderSection("featured", required: false)
                <section class="content-wrapper main-content clear-fix">
                    @RenderBody()
                </section>
            </div>
            <footer>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p>&copy; @DateTime.Now.Year - Contact Manager</p>
                    </div>
                </div>
            </footer>
            @Scripts.Render("~/bundles/jquery")
            @RenderSection("scripts", required: false)
        </body>
        </html>

<span data-ttu-id="73945-144">hello 태그 "내 ASP.NET 응용 프로그램"에서 변경 내용 hello 응용 프로그램 이름 위에 너무 "Contact Manager" 및 해당 링크를 제거 hello 너무**홈**, **에 대 한** 및 **연락처**합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-144">hello markup above changes hello app name from "My ASP.NET App" too"Contact Manager", and it removes hello links too**Home**, **About** and **Contact**.</span></span>

### <a name="run-hello-application-locally"></a><span data-ttu-id="73945-145">Hello 응용 프로그램을 로컬로 실행</span><span class="sxs-lookup"><span data-stu-id="73945-145">Run hello application locally</span></span>
1. <span data-ttu-id="73945-146">CTRL + f 5 toorun hello 응용 프로그램 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="73945-146">Press CTRL+F5 toorun hello application.</span></span>
   <span data-ttu-id="73945-147">hello 응용 프로그램 홈 페이지 hello 기본 브라우저에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="73945-147">hello application home page appears in hello default browser.</span></span>
    <span data-ttu-id="73945-148">![tooDo 목록 홈 페이지](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span><span class="sxs-lookup"><span data-stu-id="73945-148">![tooDo List home page](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span></span>

<span data-ttu-id="73945-149">이 하기만 하면 toodo 지금은 toocreate hello 응용 프로그램 tooAzure를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-149">This is all you need toodo for now toocreate hello application that you'll deploy tooAzure.</span></span> <span data-ttu-id="73945-150">나중에 데이터베이스 기능을 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="73945-150">Later you'll add database functionality.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="73945-151">Hello 응용 프로그램 tooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="73945-151">Deploy hello application tooAzure</span></span>
1. <span data-ttu-id="73945-152">Visual Studio에서의 hello 프로젝트를 마우스 오른쪽 단추로 **솔루션 탐색기** 선택 **게시** hello 상황에 맞는 메뉴에서입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-152">In Visual Studio, right-click hello project in **Solution Explorer** and select **Publish** from hello context menu.</span></span>
   
    ![프로젝트 상황에 맞는 메뉴의 게시][PublishVSSolution]
   
    <span data-ttu-id="73945-154">hello **웹 게시** 마법사가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="73945-154">hello **Publish Web** wizard opens.</span></span>
2. <span data-ttu-id="73945-155">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-155">Click **Publish**.</span></span>

![설정 탭](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

<span data-ttu-id="73945-157">Visual Studio hello 복사 프로세스를 hello 파일 toohello Azure 서버를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-157">Visual Studio begins hello process of copying hello files toohello Azure server.</span></span> <span data-ttu-id="73945-158">hello **출력** 창 수행 된 배포 작업을 표시 하 고 hello 배포를 성공적으로 완료를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-158">hello **Output** window shows what deployment actions were taken and reports successful completion of hello deployment.</span></span>

1. <span data-ttu-id="73945-159">hello 기본 브라우저 toohello 사이트의 URL을 배포 하는 hello 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="73945-159">hello default browser automatically opens toohello URL of hello deployed site.</span></span>
   
   <span data-ttu-id="73945-160">hello 응용 프로그램을 만든 hello 클라우드에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73945-160">hello application you created is now running in hello cloud.</span></span>
   
   ![Azure에서 실행 되 고 tooDo 목록 홈 페이지][rxz2]

## <a name="add-a-database-toohello-application"></a><span data-ttu-id="73945-162">데이터베이스 toohello 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="73945-162">Add a database toohello application</span></span>
<span data-ttu-id="73945-163">다음으로 hello MVC 응용 프로그램 tooadd hello 기능 toodisplay 업데이트 및 연락처를 업데이트 하 hello 데이터는 데이터베이스에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-163">Next, you'll update hello MVC application tooadd hello ability toodisplay and update contacts and store hello data in a database.</span></span> <span data-ttu-id="73945-164">hello 응용 프로그램이 hello Entity Framework toocreate hello 데이터베이스와 tooread를 사용 하 고 hello 데이터베이스에서 데이터를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-164">hello application will use hello Entity Framework toocreate hello database and tooread and update data in hello database.</span></span>

### <a name="add-data-model-classes-for-hello-contacts"></a><span data-ttu-id="73945-165">Hello 연락처에 대 한 데이터 모델 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-165">Add data model classes for hello contacts</span></span>
<span data-ttu-id="73945-166">먼저 코드로 간단한 데이터 모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73945-166">You begin by creating a simple data model in code.</span></span>

1. <span data-ttu-id="73945-167">**솔루션 탐색기**hello 모델 폴더를 마우스 오른쪽 단추로 클릭 하 여 **추가**, 차례로 **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-167">In **Solution Explorer**, right-click hello Models folder, click **Add**, and then **Class**.</span></span>
   
    ![모델 폴더 상황에 맞는 메뉴의 클래스 추가][adddb001]
2. <span data-ttu-id="73945-169">Hello에 **새 항목 추가** 대화 상자, 이름 hello 새 클래스 파일 *Contact.cs*, 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-169">In hello **Add New Item** dialog box, name hello new class file *Contact.cs*, and then click **Add**.</span></span>
   
    ![새 항목 추가 대화 상자][adddb002]
3. <span data-ttu-id="73945-171">Hello Contacts.cs 파일의 내용을 hello 코드 다음 hello로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-171">Replace hello contents of hello Contacts.cs file with hello following code.</span></span>
   
        using System.Globalization;
        namespace ContactManager.Models
        {
            public class Contact
               {
                public int ContactId { get; set; }
                public string Name { get; set; }
                public string Address { get; set; }
                public string City { get; set; }
                public string State { get; set; }
                public string Zip { get; set; }
                public string Email { get; set; }
                public string Twitter { get; set; }
                public string Self
                {
                    get { return string.Format(CultureInfo.CurrentCulture,
                         "api/contacts/{0}", this.ContactId); }
                    set { }
                }
            }
        }

<span data-ttu-id="73945-172">hello **문의** 각 연락처와 ContactID hello 데이터베이스에 필요한 기본 키를 저장 하는 hello 데이터 클래스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-172">hello **Contact** class defines hello data that you will store for each contact, plus a primary key, ContactID, that is needed by hello database.</span></span> <span data-ttu-id="73945-173">Hello에 데이터 모델에 대 한 자세한 정보를 얻을 수 [다음 단계](#nextsteps) hello 끝이 자습서에는 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-173">You can get more information about data models in hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span>

### <a name="create-web-pages-that-enable-app-users-toowork-with-hello-contacts"></a><span data-ttu-id="73945-174">Hello 연락처가 있는 응용 프로그램 사용자 toowork 수 있도록 하는 웹 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="73945-174">Create web pages that enable app users toowork with hello contacts</span></span>
<span data-ttu-id="73945-175">hello ASP.NET MVC hello 스 캐 폴딩 기능은 자동으로 생성할 수 수행 하는 코드 생성, 읽기, 업데이트 및 삭제 (CRUD) 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-175">hello ASP.NET MVC hello scaffolding feature can automatically generate code that performs create, read, update, and delete (CRUD) actions.</span></span>

## <a name="add-a-controller-and-a-view-for-hello-data"></a><span data-ttu-id="73945-176">컨트롤러와 hello 데이터에 대 한 보기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-176">Add a Controller and a view for hello data</span></span>
1. <span data-ttu-id="73945-177">**솔루션 탐색기**, 안녕하세요 Controllers 폴더를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-177">In **Solution Explorer**, expand hello Controllers folder.</span></span>
2. <span data-ttu-id="73945-178">Hello 프로젝트 빌드 **(Ctrl + Shift + B)**합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-178">Build hello project **(Ctrl+Shift+B)**.</span></span> <span data-ttu-id="73945-179">(스 캐 폴딩 메커니즘을 사용 하기 전에 hello 프로젝트를 빌드합니다 해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="73945-179">(You must build hello project before using scaffolding mechanism.)</span></span> 
3. <span data-ttu-id="73945-180">안녕하세요 Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 클릭 **추가**, 클릭 하 고 **컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-180">Right-click hello Controllers folder and click **Add**, and then click **Controller**.</span></span>
   
    ![컨트롤러 폴더 상황에 맞는 메뉴의 컨트롤러 추가][addcode001]
4. <span data-ttu-id="73945-182">Hello에 **추가 스 캐 폴드** 대화 상자에서 **Entity Framework를 사용 하 여 뷰를 포함 된 MVC 컨트롤러** 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-182">In hello **Add Scaffold** dialog box, select **MVC Controller with views, using Entity Framework** and click **Add**.</span></span>
   
   ![컨트롤러 추가](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. <span data-ttu-id="73945-184">Hello 컨트롤러 이름을 너무 설정**HomeController**합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-184">Set hello controller name too**HomeController**.</span></span> <span data-ttu-id="73945-185">모델 클래스로 **Contact** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-185">Select **Contact** as your model class.</span></span> <span data-ttu-id="73945-186">Hello 클릭 **새 데이터 컨텍스트에** hello에 대 한 hello 기본값 "ContactManager.Models.ContactManagerContext" क र च 단추 **새 데이터 컨텍스트 형식**합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-186">Click hello **New data context** button and accept hello default "ContactManager.Models.ContactManagerContext" for hello **New data context type**.</span></span> <span data-ttu-id="73945-187">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-187">Click **Add**.</span></span>

    <span data-ttu-id="73945-188">묻는 대화 상자가: "hello 이름 가진 파일이 HomeController 이미 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73945-188">A dialog box will prompt you: "A file with hello name HomeController already exits.</span></span> <span data-ttu-id="73945-189">Tooreplace 원하는 것? "입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-189">Do you want tooreplace it?".</span></span> <span data-ttu-id="73945-190">**예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-190">Click **Yes**.</span></span> <span data-ttu-id="73945-191">Hello hello 새 프로젝트를 사용 하 여 만든 홈 컨트롤러를 덮어쓰는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-191">We are overwriting hello Home Controller that was created with hello new project.</span></span> <span data-ttu-id="73945-192">사용 합니다 hello 새 홈 컨트롤러에 대 한 연락처 목록.</span><span class="sxs-lookup"><span data-stu-id="73945-192">We will use hello new Home Controller for our contact list.</span></span>

    <span data-ttu-id="73945-193">Visual Studio에서 **Contact** 개체에 대한 CRUD 데이터베이스 작업의 컨트롤러 메서드와 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73945-193">Visual Studio creates controller methods and views for CRUD database operations for **Contact** objects.</span></span>

## <a name="enable-migrations-create-hello-database-add-sample-data-and-a-data-initializer"></a><span data-ttu-id="73945-194">마이그레이션을 사용 하도록 설정, hello 데이터베이스 만들기, 샘플 데이터와 데이터 이니셜라이저를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-194">Enable Migrations, create hello database, add sample data and a data initializer</span></span>
<span data-ttu-id="73945-195">hello 다음 작업은 tooenable hello [Code First 마이그레이션을](http://curah.microsoft.com/55220) 만든 hello 데이터 모델을 기반으로 하는 주문 toocreate hello 데이터베이스의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-195">hello next task is tooenable hello [Code First Migrations](http://curah.microsoft.com/55220) feature in order toocreate hello database based on hello data model you created.</span></span>

1. <span data-ttu-id="73945-196">Hello에 **도구** 메뉴 선택 **라이브러리 패키지 관리자** 차례로 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-196">In hello **Tools** menu, select **Library Package Manager** and then **Package Manager Console**.</span></span>
   
    ![도구 메뉴의 패키지 관리자 콘솔][addcode008]
2. <span data-ttu-id="73945-198">Hello에 **패키지 관리자 콘솔** 창의 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-198">In hello **Package Manager Console** window, enter hello following command:</span></span>
   
        enable-migrations 
   
    <span data-ttu-id="73945-199">hello **사용 마이그레이션** 명령은 만듭니다는 *마이그레이션* 폴더 이므로 해당 폴더에 넣습니다는 *Configuration.cs* 파일 tooconfigure 마이그레이션을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73945-199">hello **enable-migrations** command creates a *Migrations* folder and it puts in that folder a *Configuration.cs* file that you can edit tooconfigure Migrations.</span></span> 
3. <span data-ttu-id="73945-200">Hello에 **패키지 관리자 콘솔** 창의 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-200">In hello **Package Manager Console** window, enter hello following command:</span></span>
   
        add-migration Initial
   
    <span data-ttu-id="73945-201">hello **추가 마이그레이션 초기** 라는 클래스를 생성 하는 명령  **&lt;date_stamp&gt;초기** hello 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73945-201">hello **add-migration Initial** command generates a class named **&lt;date_stamp&gt;Initial** that creates hello database.</span></span> <span data-ttu-id="73945-202">첫 번째 매개 변수를 hello ( *초기* ) 되 고 사용 된 임의의 toocreate hello hello 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-202">hello first parameter ( *Initial* ) is arbitrary and used toocreate hello name of hello file.</span></span> <span data-ttu-id="73945-203">Hello에서 새 클래스 파일을 볼 수 **솔루션 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-203">You can see hello new class files in **Solution Explorer**.</span></span>
   
    <span data-ttu-id="73945-204">Hello에 **초기** 클래스 hello **를** 메서드 hello Contacts 테이블와 hello 만듭니다 **아래로** 메서드 (tooreturn toohello 이전 상태로 하려는 경우 사용) 하 여 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-204">In hello **Initial** class, hello **Up** method creates hello Contacts table, and hello **Down** method (used when you want tooreturn toohello previous state) drops it.</span></span>
4. <span data-ttu-id="73945-205">열기 hello *Migrations\Configuration.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-205">Open hello *Migrations\Configuration.cs* file.</span></span> 
5. <span data-ttu-id="73945-206">Hello 다음 네임 스페이스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-206">Add hello following namespaces.</span></span> 
   
         using ContactManager.Models;
6. <span data-ttu-id="73945-207">Hello 대체 *시드* 메서드 코드 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="73945-207">Replace hello *Seed* method with hello following code:</span></span>
   
        protected override void Seed(ContactManager.Models.ContactManagerContext context)
        {
            context.Contacts.AddOrUpdate(p => p.Name,
               new Contact
               {
                   Name = "Debra Garcia",
                   Address = "1234 Main St",
                   City = "Redmond",
                   State = "WA",
                   Zip = "10999",
                   Email = "debra@example.com",
                   Twitter = "debra_example"
               },
                new Contact
                {
                    Name = "Thorsten Weinrich",
                    Address = "5678 1st Ave W",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "thorsten@example.com",
                    Twitter = "thorsten_example"
                },
                new Contact
                {
                    Name = "Yuhong Li",
                    Address = "9012 State st",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "yuhong@example.com",
                    Twitter = "yuhong_example"
                },
                new Contact
                {
                    Name = "Jon Orton",
                    Address = "3456 Maple St",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "jon@example.com",
                    Twitter = "jon_example"
                },
                new Contact
                {
                    Name = "Diliana Alexieva-Bosseva",
                    Address = "7890 2nd Ave E",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "diliana@example.com",
                    Twitter = "diliana_example"
                }
                );
        }
   
    <span data-ttu-id="73945-208">위의이 코드를이 hello 연락처 정보를 사용 하 여 hello 데이터베이스를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-208">This code above will initialize hello database with hello contact information.</span></span> <span data-ttu-id="73945-209">시드 hello 데이터베이스에 대 한 자세한 내용은 참조 하십시오. [디버깅 Entity Framework (EF) Db](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-209">For more information on seeding hello database, see [Debugging Entity Framework (EF) DBs](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span></span>
7. <span data-ttu-id="73945-210">Hello에 **패키지 관리자 콘솔** hello 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-210">In hello **Package Manager Console** enter hello command:</span></span>
   
        update-database
   
    ![패키지 관리자 콘솔 명령][addcode009]
   
    <span data-ttu-id="73945-212">hello **데이터베이스 업데이트** 실행 hello hello 데이터베이스를 만드는 첫 번째 마이그레이션.</span><span class="sxs-lookup"><span data-stu-id="73945-212">hello **update-database** runs hello first migration which creates hello database.</span></span> <span data-ttu-id="73945-213">기본적으로 SQL Server Express LocalDB 데이터베이스 서 hello 데이터베이스가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73945-213">By default, hello database is created as a SQL Server Express LocalDB database.</span></span>
8. <span data-ttu-id="73945-214">CTRL + f 5 toorun hello 응용 프로그램 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="73945-214">Press CTRL+F5 toorun hello application.</span></span> 

<span data-ttu-id="73945-215">hello 응용 프로그램 hello 시드 데이터를 표시 하 고 편집, 내용 및 삭제 링크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-215">hello application shows hello seed data and provides edit, details and delete links.</span></span>

![MVC 데이터 뷰][rxz3]

## <a name="edit-hello-view"></a><span data-ttu-id="73945-217">Hello 보기 편집</span><span class="sxs-lookup"><span data-stu-id="73945-217">Edit hello View</span></span>
1. <span data-ttu-id="73945-218">열기 hello *Views\Home\Index.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-218">Open hello *Views\Home\Index.cshtml* file.</span></span> <span data-ttu-id="73945-219">Hello 다음 단계에서 사용 하는 코드로 생성 된 hello 태그 바꿉니다 됩니다 [jQuery](http://jquery.com/) 및 [Knockout.js](http://knockoutjs.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-219">In hello next step, we will replace hello generated markup with code that uses [jQuery](http://jquery.com/) and [Knockout.js](http://knockoutjs.com/).</span></span> <span data-ttu-id="73945-220">이 새 코드 웹 API를 사용 하 여에서 연락처 목록을 hello를 검색 하 고 JSON 및 바인딩 hello 문의 데이터 toohello UI knockout.js를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-220">This new code retrieves hello list of contacts from using web API and JSON and then binds hello contact data toohello UI using knockout.js.</span></span> <span data-ttu-id="73945-221">자세한 내용은 참조 hello [다음 단계](#nextsteps) hello 끝이 자습서에는 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-221">For more information, see hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span> 
2. <span data-ttu-id="73945-222">Hello 파일의 내용을 hello 코드 다음 hello로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-222">Replace hello contents of hello file with hello following code.</span></span>
   
        @model IEnumerable<ContactManager.Models.Contact>
        @{
            ViewBag.Title = "Home";
        }
        @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                function ContactsViewModel() {
                    var self = this;
                    self.contacts = ko.observableArray([]);
                    self.addContact = function () {
                        $.post("api/contacts",
                            $("#addContact").serialize(),
                            function (value) {
                                self.contacts.push(value);
                            },
                            "json");
                    }
                    self.removeContact = function (contact) {
                        $.ajax({
                            type: "DELETE",
                            url: contact.Self,
                            success: function () {
                                self.contacts.remove(contact);
                            }
                        });
                    }
   
                    $.getJSON("api/contacts", function (data) {
                        self.contacts(data);
                    });
                }
                ko.applyBindings(new ContactsViewModel());    
        </script>
        }
        <ul id="contacts" data-bind="foreach: contacts">
            <li class="ui-widget-content ui-corner-all">
                <h1 data-bind="text: Name" class="ui-widget-header"></h1>
                <div><span data-bind="text: $data.Address || 'Address?'"></span></div>
                <div>
                    <span data-bind="text: $data.City || 'City?'"></span>,
                    <span data-bind="text: $data.State || 'State?'"></span>
                    <span data-bind="text: $data.Zip || 'Zip?'"></span>
                </div>
                <div data-bind="if: $data.Email"><a data-bind="attr: { href: 'mailto:' + Email }, text: Email"></a></div>
                <div data-bind="ifnot: $data.Email"><span>Email?</span></div>
                <div data-bind="if: $data.Twitter"><a data-bind="attr: { href: 'http://twitter.com/' + Twitter }, text: '@@' + Twitter"></a></div>
                <div data-bind="ifnot: $data.Twitter"><span>Twitter?</span></div>
                <p><a data-bind="attr: { href: Self }, click: $root.removeContact" class="removeContact ui-state-default ui-corner-all">Remove</a></p>
            </li>
        </ul>
        <form id="addContact" data-bind="submit: addContact">
            <fieldset>
                <legend>Add New Contact</legend>
                <ol>
                    <li>
                        <label for="Name">Name</label>
                        <input type="text" name="Name" />
                    </li>
                    <li>
                        <label for="Address">Address</label>
                        <input type="text" name="Address" >
                    </li>
                    <li>
                        <label for="City">City</label>
                        <input type="text" name="City" />
                    </li>
                    <li>
                        <label for="State">State</label>
                        <input type="text" name="State" />
                    </li>
                    <li>
                        <label for="Zip">Zip</label>
                        <input type="text" name="Zip" />
                    </li>
                    <li>
                        <label for="Email">E-mail</label>
                        <input type="text" name="Email" />
                    </li>
                    <li>
                        <label for="Twitter">Twitter</label>
                        <input type="text" name="Twitter" />
                    </li>
                </ol>
                <input type="submit" value="Add" />
            </fieldset>
        </form>
3. <span data-ttu-id="73945-223">Hello 콘텐츠 폴더를 마우스 오른쪽 단추로 클릭 하 고 클릭 **추가**, 클릭 하 고 **새 항목...** .</span><span class="sxs-lookup"><span data-stu-id="73945-223">Right-click hello Content folder and click **Add**, and then click **New Item...**.</span></span>
   
    ![Content 폴더의 상황에 맞는 메뉴에서 스타일시트 추가][addcode005]
4. <span data-ttu-id="73945-225">Hello에 **새 항목 추가** 대화 상자에 입력 **스타일** 에 hello 위쪽 오른쪽 검색 상자를 클릭 한 **스타일 시트**합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-225">In hello **Add New Item** dialog box, enter **Style** in hello upper right search box and then select **Style Sheet**.</span></span>
    <span data-ttu-id="73945-226">![새 항목 추가 대화 상자][rxStyle]</span><span class="sxs-lookup"><span data-stu-id="73945-226">![Add New Item dialog box][rxStyle]</span></span>
5. <span data-ttu-id="73945-227">이름 hello 파일 *Contacts.css* 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-227">Name hello file *Contacts.css* and click **Add**.</span></span> <span data-ttu-id="73945-228">Hello 파일의 내용을 hello 코드 다음 hello로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-228">Replace hello contents of hello file with hello following code.</span></span>
   
        .column {
            float: left;
            width: 50%;
            padding: 0;
            margin: 5px 0;
        }
        form ol {
            list-style-type: none;
            padding: 0;
            margin: 0;
        }
        form li {
            padding: 1px;
            margin: 3px;
        }
        form input[type="text"] {
            width: 100%;
        }
        #addContact {
            width: 300px;
            float: left;
            width:30%;
        }
        #contacts {
            list-style-type: none;
            margin: 0;
            padding: 0;
            float:left;
            width: 70%;
        }
        #contacts li {
            margin: 3px 3px 3px 0;
            padding: 1px;
            float: left;
            width: 300px;
            text-align: center;
            background-image: none;
            background-color: #F5F5F5;
        }
        #contacts li h1
        {
            padding: 0;
            margin: 0;
            background-image: none;
            background-color: Orange;
            color: White;
            font-family: Trebuchet MS, Tahoma, Verdana, Arial, sans-serif;
        }
        .removeContact, .viewImage
        {
            padding: 3px;
            text-decoration: none;
        }
   
    <span data-ttu-id="73945-229">이 스타일 시트 hello 레이아웃, 색 및 hello 연락처 관리자 앱에서 사용 되는 스타일에 대 한 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-229">We will use this style sheet for hello layout, colors and styles used in hello contact manager app.</span></span>
6. <span data-ttu-id="73945-230">열기 hello *App_Start\BundleConfig.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-230">Open hello *App_Start\BundleConfig.cs* file.</span></span>
7. <span data-ttu-id="73945-231">다음 코드 tooregister hello hello 추가 [Knockout](http://knockoutjs.com/index.html "KO") 플러그 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-231">Add hello following code tooregister hello [Knockout](http://knockoutjs.com/index.html "KO") plugin.</span></span>
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    <span data-ttu-id="73945-232">Knockout toosimplify 동적 JavaScript 코드를 hello 화면 템플릿을 처리를 사용 하 여이 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-232">This sample using knockout toosimplify dynamic JavaScript code that handles hello screen templates.</span></span>
8. <span data-ttu-id="73945-233">Hello 내용을/css 항목 tooregister hello 수정 *contacts.css* 스타일 시트입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-233">Modify hello contents/css entry tooregister hello *contacts.css* style sheet.</span></span> <span data-ttu-id="73945-234">Hello 다음 줄을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-234">Change hello following line:</span></span>
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   <span data-ttu-id="73945-235">아래와 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-235">To:</span></span>
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. <span data-ttu-id="73945-236">Hello 패키지 관리자 콘솔에서에서 다음 명령을 tooinstall Knockout hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-236">In hello Package Manager Console, run hello following command tooinstall Knockout.</span></span>
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-hello-web-api-restful-interface"></a><span data-ttu-id="73945-237">Hello 웹 API Restful 인터페이스에 대 한 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="73945-237">Add a controller for hello Web API Restful interface</span></span>
1. <span data-ttu-id="73945-238">**솔루션 탐색기**에서 컨트롤러를 마우스 오른쪽 단추로 클릭하고 **추가**를 클릭한 후 **컨트롤러...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-238">In **Solution Explorer**, right-click Controllers and click **Add** and then **Controller....**</span></span> 
2. <span data-ttu-id="73945-239">Hello에 **추가 스 캐 폴드** 대화 상자에 입력 **Entity Framework를 사용 하 여 작업을 포함 된 Web API 2 컨트롤러** 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-239">In hello **Add Scaffold** dialog box, enter **Web API 2 Controller with actions, using Entity Framework** and then click **Add**.</span></span>
   
    ![API 컨트롤러 추가](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. <span data-ttu-id="73945-241">Hello에 **컨트롤러 추가** 대화 상자에 컨트롤러 이름으로 "ContactsController"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-241">In hello **Add Controller** dialog box, enter "ContactsController" as your controller name.</span></span> <span data-ttu-id="73945-242">Hello에 대 한 "Contact (ContactManager.Models)"를 선택 **모델 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-242">Select "Contact (ContactManager.Models)" for hello **Model class**.</span></span>  <span data-ttu-id="73945-243">Hello에 대 한 hello 기본값 유지 **데이터 컨텍스트 클래스가**합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-243">Keep hello default value for hello **Data context class**.</span></span> 
4. <span data-ttu-id="73945-244">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-244">Click **Add**.</span></span>

### <a name="run-hello-application-locally"></a><span data-ttu-id="73945-245">Hello 응용 프로그램을 로컬로 실행</span><span class="sxs-lookup"><span data-stu-id="73945-245">Run hello application locally</span></span>
1. <span data-ttu-id="73945-246">CTRL + f 5 toorun hello 응용 프로그램 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="73945-246">Press CTRL+F5 toorun hello application.</span></span>
   
    ![인덱스 페이지][intro001]
2. <span data-ttu-id="73945-248">연락처를 입력하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-248">Enter a contact and click **Add**.</span></span> <span data-ttu-id="73945-249">hello 앱 toohello 홈 페이지를 반환 하 고 입력 한 hello 연락처를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-249">hello app returns toohello home page and displays hello contact you entered.</span></span>
   
    ![할 일 모음 항목이 있는 인덱스 페이지][addwebapi004]
3. <span data-ttu-id="73945-251">Hello 브라우저에서 추가 **/api/연락처** toohello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-251">In hello browser, append **/api/contacts** toohello URL.</span></span>
   
    <span data-ttu-id="73945-252">hello 결과 URL http://localhost:1234/api/연락처와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-252">hello resulting URL will resemble http://localhost:1234/api/contacts.</span></span> <span data-ttu-id="73945-253">hello RESTful 웹 API 추가한 저장 hello 연락처를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-253">hello RESTful web API you added returns hello stored contacts.</span></span> <span data-ttu-id="73945-254">Firefox 및 Chrome은 XML 형식의 hello 데이터를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73945-254">Firefox and Chrome will display hello data in XML format.</span></span>
   
    ![할 일 모음 항목이 있는 인덱스 페이지][rxFFchrome]

    <span data-ttu-id="73945-256">IE는 tooopen 라는 메시지가 표시 되거나 hello 연락처 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73945-256">IE will prompt you tooopen or save hello contacts.</span></span>

    ![Web API 저장 대화 상자][addwebapi006]


    <span data-ttu-id="73945-258">메모장 이나 브라우저에서 연락처를 반환 하는 hello를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73945-258">You can open hello returned contacts in notepad or a browser.</span></span>

    <span data-ttu-id="73945-259">이 출력은 모바일 웹 페이지나 모바일 응용 프로그램 같은 다른 응용 프로그램에서 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73945-259">This output can be consumed by another application such as mobile web page or application.</span></span>

    ![Web API 저장 대화 상자][addwebapi007]

    <span data-ttu-id="73945-261">**보안 경고**:이 시점에서 응용 프로그램은 안전 하지 않은 및 취약 한 tooCSRF 방식의 공격입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-261">**Security Warning**: At this point, your application is insecure and vulnerable tooCSRF attack.</span></span> <span data-ttu-id="73945-262">Hello 자습서의 뒷부분에 나오는 이러한 취약성을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-262">Later in hello tutorial we will remove this vulnerability.</span></span> <span data-ttu-id="73945-263">자세한 내용은 [CSRF(교차 사이트 요청 위조) 공격 예방][prevent-csrf-attacks]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73945-263">For more information see [Preventing Cross-Site Request Forgery (CSRF) Attacks][prevent-csrf-attacks].</span></span>
## <a name="add-xsrf-protection"></a><span data-ttu-id="73945-264">XSRF 보호 추가</span><span class="sxs-lookup"><span data-stu-id="73945-264">Add XSRF Protection</span></span>
<span data-ttu-id="73945-265">교차 사이트 요청 위조 (XSRF 또는 CSRF 라고도 함)은 악성 웹 사이트 클라이언트 브라우저와 해당 브라우저에서 신뢰할 수 있는 웹 사이트 간의 상호 작용 hello 영향을 줄 수는 그에 따라 웹 호스팅 응용 프로그램에 대 한 공격입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-265">Cross-site request forgery (also known as XSRF or CSRF) is an attack against web-hosted applications whereby a malicious website can influence hello interaction between a client browser and a website trusted by that browser.</span></span> <span data-ttu-id="73945-266">이러한 공격은 웹 브라우저에서 자동으로 모든 요청 tooa 웹 사이트와 함께 인증 토큰을 보냅니다 때문에 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-266">These attacks are made possible because web browsers will send authentication tokens automatically with every request tooa website.</span></span> <span data-ttu-id="73945-267">hello 정식 예는 예: ASP는 인증 쿠키입니다. NET의 폼 인증 티켓입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-267">hello canonical example is an authentication cookie, such as ASP.NET's Forms Authentication ticket.</span></span> <span data-ttu-id="73945-268">하지만 Windows 인증, 기본 인증 등 영구적 인증 메커니즘을 사용하는 웹 사이트가 이러한 공격의 대상이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73945-268">However, websites which use any persistent authentication mechanism (such as Windows Authentication, Basic, and so forth) can be targeted by these attacks.</span></span>

<span data-ttu-id="73945-269">XSRF 공격은 피싱 공격과는 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="73945-269">An XSRF attack is distinct from a phishing attack.</span></span> <span data-ttu-id="73945-270">피싱 공격 hello 교착 상태가 발생에서 상호 작용을 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-270">Phishing attacks require interaction from hello victim.</span></span> <span data-ttu-id="73945-271">피싱 공격에서는 악의적인 웹 사이트를 hello 대상 웹 사이트를 모방 합니다 및 hello 교착 상태가 발생 toohello 공격자가 중요 한 정보를 제공 하도록 속일 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73945-271">In a phishing attack, a malicious website will mimic hello target website, and hello victim is fooled into providing sensitive information toohello attacker.</span></span> <span data-ttu-id="73945-272">XSRF 공격에서 종종 hello 교착 상태가 발생에서 필요한 조작은 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="73945-272">In an XSRF attack, there is often no interaction necessary from hello victim.</span></span> <span data-ttu-id="73945-273">대신, hello 공격자가 모든 관련 쿠키 toohello 대상 웹 사이트를 자동으로 보낼 hello 브라우저에 의존 하므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-273">Rather, hello attacker is relying on hello browser automatically sending all relevant cookies toohello destination website.</span></span>

<span data-ttu-id="73945-274">자세한 내용은 참조 hello [웹 응용 프로그램 보안 프로젝트 열기](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\))합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-274">For more information, see hello [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span></span>

1. <span data-ttu-id="73945-275">**솔루션 탐색기**에서 **ContactManager** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**를 클릭한 후 **클래스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-275">In **Solution Explorer**, right **ContactManager** project and click **Add** and then click **Class**.</span></span>
2. <span data-ttu-id="73945-276">이름 hello 파일 *ValidateHttpAntiForgeryTokenAttribute.cs* hello 코드 다음에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-276">Name hello file *ValidateHttpAntiForgeryTokenAttribute.cs* and add hello following code:</span></span>
   
        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Helpers;
        using System.Web.Http.Controllers;
        using System.Web.Http.Filters;
        using System.Web.Mvc;
        namespace ContactManager.Filters
        {
            public class ValidateHttpAntiForgeryTokenAttribute : AuthorizationFilterAttribute
            {
                public override void OnAuthorization(HttpActionContext actionContext)
                {
                    HttpRequestMessage request = actionContext.ControllerContext.Request;
                    try
                    {
                        if (IsAjaxRequest(request))
                        {
                            ValidateRequestHeader(request);
                        }
                        else
                        {
                            AntiForgery.Validate();
                        }
                    }
                    catch (HttpAntiForgeryException e)
                    {
                        actionContext.Response = request.CreateErrorResponse(HttpStatusCode.Forbidden, e);
                    }
                }
                private bool IsAjaxRequest(HttpRequestMessage request)
                {
                    IEnumerable<string> xRequestedWithHeaders;
                    if (request.Headers.TryGetValues("X-Requested-With", out xRequestedWithHeaders))
                    {
                        string headerValue = xRequestedWithHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(headerValue))
                        {
                            return String.Equals(headerValue, "XMLHttpRequest", StringComparison.OrdinalIgnoreCase);
                        }
                    }
                    return false;
                }
                private void ValidateRequestHeader(HttpRequestMessage request)
                {
                    string cookieToken = String.Empty;
                    string formToken = String.Empty;
                    IEnumerable<string> tokenHeaders;
                    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
                    {
                        string tokenValue = tokenHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(tokenValue))
                        {
                            string[] tokens = tokenValue.Split(':');
                            if (tokens.Length == 2)
                            {
                                cookieToken = tokens[0].Trim();
                                formToken = tokens[1].Trim();
                            }
                        }
                    }
                    AntiForgery.Validate(cookieToken, formToken);
                }
            }
        }
3. <span data-ttu-id="73945-277">Hello 다음 추가 *를 사용 하 여* 액세스 toohello 해야 하므로 문을 toohello 계약 컨트롤러 **[ValidateHttpAntiForgeryToken]** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-277">Add hello following *using* statement toohello contracts controller so you have access toohello **[ValidateHttpAntiForgeryToken]** attribute.</span></span>
   
        using ContactManager.Filters;
4. <span data-ttu-id="73945-278">Hello 추가 **[ValidateHttpAntiForgeryToken]** hello의 toohello Post 메서드 특성 **ContactsController** tooprotect XSRF 위협 옵니다.</span><span class="sxs-lookup"><span data-stu-id="73945-278">Add hello **[ValidateHttpAntiForgeryToken]** attribute toohello Post methods of hello **ContactsController** tooprotect it from XSRF threats.</span></span> <span data-ttu-id="73945-279">Toohello "PutContact", "PostContact" 추가 합니다 및 **DeleteContact** 작업 메서드.</span><span class="sxs-lookup"><span data-stu-id="73945-279">You will add it toohello "PutContact",  "PostContact" and **DeleteContact** action methods.</span></span>
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. <span data-ttu-id="73945-280">업데이트 hello *스크립트* hello 섹션 *Views\Home\Index.cshtml* tooinclude 코드 tooget hello XSRF 토큰 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-280">Update hello *Scripts* section of hello *Views\Home\Index.cshtml* file tooinclude code tooget hello XSRF tokens.</span></span>
   
         @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                @functions{
                   public string TokenHeaderValue()
                   {
                      string cookieToken, formToken;
                      AntiForgery.GetTokens(null, out cookieToken, out formToken);
                      return cookieToken + ":" + formToken;                
                   }
                }
   
               function ContactsViewModel() {
                  var self = this;
                  self.contacts = ko.observableArray([]);
                  self.addContact = function () {
   
                     $.ajax({
                        type: "post",
                        url: "api/contacts",
                        data: $("#addContact").serialize(),
                        dataType: "json",
                        success: function (value) {
                           self.contacts.push(value);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
                     });
   
                  }
                  self.removeContact = function (contact) {
                     $.ajax({
                        type: "DELETE",
                        url: contact.Self,
                        success: function () {
                           self.contacts.remove(contact);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
   
                     });
                  }
   
                  $.getJSON("api/contacts", function (data) {
                     self.contacts(data);
                  });
               }
               ko.applyBindings(new ContactsViewModel());
            </script>
         }

## <a name="publish-hello-application-update-tooazure-and-sql-database"></a><span data-ttu-id="73945-281">응용 프로그램 업데이트 tooAzure hello 및 SQL 데이터베이스를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-281">Publish hello application update tooAzure and SQL Database</span></span>
<span data-ttu-id="73945-282">toopublish hello 응용 프로그램을 이전에 따른 hello 절차를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-282">toopublish hello application, you repeat hello procedure you followed earlier.</span></span>

1. <span data-ttu-id="73945-283">**솔루션 탐색기**hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-283">In **Solution Explorer**, right click hello project and select **Publish**.</span></span>
   
    ![게시][rxP]
2. <span data-ttu-id="73945-285">Hello 클릭 **설정을** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-285">Click hello **Settings** tab.</span></span>
3. <span data-ttu-id="73945-286">아래 **ContactsManagerContext(ContactsManagerContext)**, hello 클릭 **v** 아이콘 toochange *원격 연결 문자열* hello 연락처에 대 한 toohello 연결 문자열 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-286">Under **ContactsManagerContext(ContactsManagerContext)**, click hello **v** icon toochange *Remote connection string* toohello connection string for hello contact database.</span></span> <span data-ttu-id="73945-287">**ContactDB**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-287">Click **ContactDB**.</span></span>
   
    ![설정](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. <span data-ttu-id="73945-289">에 대 한 hello 확인란 **실행 Code First 마이그레이션을 (응용 프로그램 시작 시 실행)**합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-289">Check hello box for **Execute Code First Migrations (runs on application start)**.</span></span>
5. <span data-ttu-id="73945-290">**다음**을 클릭한 후 **미리 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-290">Click **Next** and then click **Preview**.</span></span> <span data-ttu-id="73945-291">Visual Studio에 추가 하거나 업데이트할 수 있는 hello 파일의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73945-291">Visual Studio displays a list of hello files that will be added or updated.</span></span>
6. <span data-ttu-id="73945-292">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-292">Click **Publish**.</span></span>
   <span data-ttu-id="73945-293">Hello 배포가 완료 된 후 hello 브라우저 hello 응용 프로그램의 toohello 홈 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="73945-293">After hello deployment completes, hello browser opens toohello home page of hello application.</span></span>
   
    ![연락처가 없는 인덱스 페이지][intro001]
   
    <span data-ttu-id="73945-295">배포 된 hello에 hello 연결 문자열을 자동으로 구성 하는 프로세스를 게시 하는 hello Visual Studio *Web.config* toopoint toohello SQL 데이터베이스 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-295">hello Visual Studio publish process automatically configured hello connection string in hello deployed *Web.config* file toopoint toohello SQL database.</span></span> <span data-ttu-id="73945-296">또한 Code First 마이그레이션을 tooautomatically 업그레이드 hello 데이터베이스 toohello 최신 버전 hello 첫 번째 시간 hello 응용 프로그램 배포 후 hello 데이터베이스에 액세스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-296">It also configured Code First Migrations tooautomatically upgrade hello database toohello latest version hello first time hello application accesses hello database after deployment.</span></span>
   
    <span data-ttu-id="73945-297">이 구성으로 인해 코드 첫 번째 데이터베이스를 만들었습니다 hello hello에 hello 코드를 실행 하 여 **초기** 앞에서 만든 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-297">As a result of this configuration, Code First created hello database by running hello code in hello **Initial** class that you created earlier.</span></span> <span data-ttu-id="73945-298">배포 후이 hello 첫 번째 시간 hello 응용 프로그램 시도 tooaccess hello 데이터베이스에서 수행한 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-298">It did this hello first time hello application tried tooaccess hello database after deployment.</span></span>
7. <span data-ttu-id="73945-299">Hello 응용 프로그램을 로컬로 설치에 데이터베이스 배포 성공 tooverify 실행 되었을 때 수행한 대로 연락처를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-299">Enter a contact as you did when you ran hello app locally, tooverify that database deployment succeeded.</span></span>

<span data-ttu-id="73945-300">입력 하면 해당 hello 항목이 저장 되 고 hello 연락처 관리자 페이지에 표시를 보면 hello 데이터베이스에 저장 되어 있는 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73945-300">When you see that hello item you enter is saved and appears on hello contact manager page, you know that it has been stored in hello database.</span></span>

![연락처가 있는 인덱스 페이지][addwebapi004]

<span data-ttu-id="73945-302">hello 응용 프로그램은 이제 클라우드에서 실행 중인 hello, toostore SQL 데이터베이스를 사용 하 여 해당 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="73945-302">hello application is now running in hello cloud, using SQL Database toostore its data.</span></span> <span data-ttu-id="73945-303">Azure의 hello 응용 프로그램 테스트를 마친 후 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-303">After you finish testing hello application in Azure, delete it.</span></span> <span data-ttu-id="73945-304">hello 응용 프로그램은 공용 및 메커니즘 toolimit 액세스할 수 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-304">hello application is public and doesn't have a mechanism toolimit access.</span></span>

> [!NOTE]
> <span data-ttu-id="73945-305">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-305">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="73945-306">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="73945-306">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="73945-307">다음 단계</span><span class="sxs-lookup"><span data-stu-id="73945-307">Next Steps</span></span>
<span data-ttu-id="73945-308">Azure 응용 프로그램에서 다른 방식으로 toostore 데이터 toouse Azure 저장소 blob 및 테이블 hello 형태로 비관계형 데이터 저장소를 제공 하는 경우</span><span class="sxs-lookup"><span data-stu-id="73945-308">Another way toostore data in an Azure application is toouse Azure storage, which provide non-relational data storage in hello form of blobs and tables.</span></span> <span data-ttu-id="73945-309">링크를 따라 hello 웹 API, ASP.NET MVC 및 Window Azure에서 자세한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="73945-309">hello following links provide more information on Web API, ASP.NET MVC and Window Azure.</span></span>

* <span data-ttu-id="73945-310">[MVC를 사용하여 Entity Framework 시작][EFCodeFirstMVCTutorial]</span><span class="sxs-lookup"><span data-stu-id="73945-310">[Getting Started with Entity Framework using MVC][EFCodeFirstMVCTutorial]</span></span>
* [<span data-ttu-id="73945-311">소개 tooASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="73945-311">Intro tooASP.NET MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="73945-312">최초 ASP.NET 앱 API</span><span class="sxs-lookup"><span data-stu-id="73945-312">Your First ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [<span data-ttu-id="73945-313">WAWS 디버그</span><span class="sxs-lookup"><span data-stu-id="73945-313">Debugging WAWS</span></span>](web-sites-dotnet-troubleshoot-visual-studio.md)

<span data-ttu-id="73945-314">이 자습서와 hello 샘플 응용 프로그램에 의해 작성 되었으므로 [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [ @RickAndMSFT ](https://twitter.com/RickAndMSFT)) Tom Dykstra 및 Barry Dorrans의 도움을 받아 (Twitter [ @blowdart ](https://twitter.com/blowdart)).</span><span class="sxs-lookup"><span data-stu-id="73945-314">This tutorial and hello sample application was written by [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) with assistance from Tom Dykstra and Barry Dorrans (Twitter [@blowdart](https://twitter.com/blowdart)).</span></span> 

<span data-ttu-id="73945-315">좋아 있습니다 또는 원하는 toosee 자체 hello 자습서 정보 뿐만 아니라 코드를 보여 줍니다 hello 제품에 대 한 향상 된 사용자 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="73945-315">Please leave feedback on what you liked or what you would like toosee improved, not only about hello tutorial itself but also about hello products that it demonstrates.</span></span> <span data-ttu-id="73945-316">사용자 의견은 개선 사항의 우선 순위를 지정하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73945-316">Your feedback will help us prioritize improvements.</span></span> <span data-ttu-id="73945-317">하는 hello 프로세스에 대 한 많은 자동화 구성 하 고 hello 멤버 자격 데이터베이스 배포에 얼마나 많은 관심 있는 인지 찾기에 특히 관심이 많습니다.</span><span class="sxs-lookup"><span data-stu-id="73945-317">We are especially interested in finding out how much interest there is in more automation for hello process of configuring and deploying hello membership database.</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="73945-318">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="73945-318">What's changed</span></span>
* <span data-ttu-id="73945-319">웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="73945-319">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- bookmarks -->
[Add an OAuth Provider]: #addOauth
[Add Roles toohello Membership Database]:#mbrDB
[Create a Data Deployment Script]:#ppd
[Update hello Membership Database]:#ppd2
[setupdbenv]: #bkmk_setupdevenv
[setupwindowsazureenv]: #bkmk_setupwindowsazure
[createapplication]: #bkmk_createmvc4app
[deployapp1]: #bkmk_deploytowindowsazure1
[adddb]: #bkmk_addadatabase
[addcontroller]: #bkmk_addcontroller
[addwebapi]: #bkmk_addwebapi
[deploy2]: #bkmk_deploydatabaseupdate

<!-- links -->
[EFCodeFirstMVCTutorial]: http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
[dbcontext-link]: http://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx


<!-- images-->
[rxE]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxE.png
[rxP]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxP.png
[rx22]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/
[rxb2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxb2.png
[rxz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz.png
[rxzz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxzz.png
[rxz2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz2.png
[rxz3]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz3.png
[rxStyle]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxStyle.png
[rxz4]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz4.png
[rxz44]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz44.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxPrevDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPrevDB.png
[rxOverwrite]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxOverwrite.png
[rxPWS]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPWS.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxAddApiController]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxAddApiController.png
[rxFFchrome]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxFFchrome.png
[intro001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobil-intro-finished-web-app.png
[rxCreateWSwithDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxCreateWSwithDB.png
[setup007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-setup-azure-site-004.png
[setup009]: ../Media/dntutmobile-setup-azure-site-006.png
[newapp002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-002.png
[newapp004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-004.png
[firsdeploy007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-005.png
[firsdeploy009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-007.png
[adddb001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-001.png
[adddb002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-002.png
[addcode001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-context-menu.png
[addcode002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-controller-dialog.png
[addcode004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-index-context.png
[addcode005]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-contents-context-menu.png
[addcode007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-bundleconfig-context.png
[addcode008]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-menu.png
[addcode009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-console.png
[addwebapi004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-added-contact.png
[addwebapi006]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-save-returned-contacts.png
[addwebapi007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-contacts-in-notepad.png
[Add XSRF Protection]: #xsrf
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[Add XSRF Protection]: #xsrf
[ImportPublishSettings]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishSettings.png
[ImportPublishProfile]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishProfile.png
[PublishVSSolution]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/PublishVSSolution.png
[ValidateConnection]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ValidateConnection.png
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[prevent-csrf-attacks]: http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-(csrf)-attacks

