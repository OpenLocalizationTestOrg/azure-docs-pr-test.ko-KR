---
title: "Service Fabric에 대한 .NET 응용 프로그램 만들기 | Microsoft Docs"
description: "ASP.NET Core 프런트 엔드 및 신뢰할 수 있는 서비스 상태 저장 백 엔드로 응용 프로그램을 만들고 클러스터에 배포하는 방법에 대해 알아봅니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: ef50adf3af19bce494c3256308b443c8eaccdcea
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a><span data-ttu-id="8fbd4-103">ASP.NET Core Web API 프런트 엔드 서비스 및 상태 저장 백 엔드 서비스로 응용 프로그램 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="8fbd4-103">Create and deploy an application with an ASP.NET Core Web API front-end service and a stateful back-end service</span></span>
<span data-ttu-id="8fbd4-104">이 자습서는 시리즈의 1부입니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-104">This tutorial is part one of a series.</span></span>  <span data-ttu-id="8fbd4-105">ASP.NET Core Web API 프런트 엔드 및 상태 저장 백 엔드 서비스에서 Azure Service Fabric 응용 프로그램을 만들어 데이터를 저장하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-105">You will learn how to create an Azure Service Fabric application with an ASP.NET Core Web API front end and a stateful back-end service to store your data.</span></span> <span data-ttu-id="8fbd4-106">완료하면 투표 결과를 클러스터의 상태 저장 백 엔드 서비스에 저장하는 ASP.NET Core 웹 프런트 엔드가 있는 투표 응용 프로그램이 생깁니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-106">When you're finished, you have a voting application with an ASP.NET Core web front-end that saves voting results in a stateful back-end service in the cluster.</span></span> <span data-ttu-id="8fbd4-107">수동으로 투표 응용 프로그램을 만들지 않으려면 완성된 응용 프로그램에서 [소스 코드를 다운로드](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/)하고 [투표 샘플 응용 프로그램을 설명](#walkthrough_anchor)하기 위해 바로 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-107">If you don't want to manually create the voting application, you can [download the source code](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) for the completed application and skip ahead to [Walk through the voting sample application](#walkthrough_anchor).</span></span>

![응용 프로그램 다이어그램](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="8fbd4-109">시리즈 1부에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-109">In part one of the series, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8fbd4-110">ASP.NET Core Web API 서비스를 상태 저장 Reliable Service로 만들기</span><span class="sxs-lookup"><span data-stu-id="8fbd4-110">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="8fbd4-111">ASP.NET Core Web 응용 프로그램 서비스를 상태 비저장 웹 서비스로 만들기</span><span class="sxs-lookup"><span data-stu-id="8fbd4-111">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="8fbd4-112">역방향 프록시를 사용하여 상태 저장 서비스와 통신</span><span class="sxs-lookup"><span data-stu-id="8fbd4-112">Use the reverse proxy to communicate with the stateful service</span></span>

<span data-ttu-id="8fbd4-113">이 자습서 시리즈에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-113">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="8fbd4-114">.NET Service Fabric 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="8fbd4-114">Build a .NET Service Fabric application</span></span>
> * [<span data-ttu-id="8fbd4-115">응용 프로그램을 원격 클러스터에 배포</span><span class="sxs-lookup"><span data-stu-id="8fbd4-115">Deploy the application to a remote cluster</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * [<span data-ttu-id="8fbd4-116">Visual Studio Team Services를 사용하여 CI/CD 구성</span><span class="sxs-lookup"><span data-stu-id="8fbd4-116">Configure CI/CD using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a><span data-ttu-id="8fbd4-117">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8fbd4-117">Prerequisites</span></span>
<span data-ttu-id="8fbd4-118">이 자습서를 시작하기 전에:</span><span class="sxs-lookup"><span data-stu-id="8fbd4-118">Before you begin this tutorial:</span></span>
- <span data-ttu-id="8fbd4-119">Azure 구독이 없는 경우 [평가판 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-119">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="8fbd4-120">[Visual Studio 2017을 설치](https://www.visualstudio.com/)하고 **Azure 개발**과 **ASP.NET 및 웹 개발** 워크로드를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-120">[Install Visual Studio 2017](https://www.visualstudio.com/) and install the **Azure development** and **ASP.NET and web development** workloads.</span></span>
- <span data-ttu-id="8fbd4-121">[Service Fabric SDK를 설치](service-fabric-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-121">[Install the Service Fabric SDK](service-fabric-get-started.md)</span></span>

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a><span data-ttu-id="8fbd4-122">ASP.NET Web API 서비스를 신뢰할 수 있는 서비스로 만들기</span><span class="sxs-lookup"><span data-stu-id="8fbd4-122">Create an ASP.NET Web API service as a reliable service</span></span>
<span data-ttu-id="8fbd4-123">먼저 ASP.NET Core를 사용하여 투표 응용 프로그램의 웹 프런트 엔드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-123">First, create the web front-end of the voting application using ASP.NET Core.</span></span> <span data-ttu-id="8fbd4-124">ASP.NET Core는 최신 웹 UI 및 Web API를 만드는 데 사용할 수 있는 가벼운 크로스 플랫폼 웹 개발 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-124">ASP.NET Core is a lightweight, cross-platform web development framework that you can use to create modern web UI and web APIs.</span></span> <span data-ttu-id="8fbd4-125">ASP.NET Core가 Service Fabric과 통합되는 방식을 완전히 이해하려면 [Service Fabric Reliable Services의 ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) 문서를 읽어보는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-125">To get a complete understanding of how ASP.NET Core integrates with Service Fabric, we strongly recommend reading through the [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) article.</span></span> <span data-ttu-id="8fbd4-126">지금은 이 가이드를 따라 작업하여 빠르게 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-126">For now, you can follow this tutorial to get started quickly.</span></span> <span data-ttu-id="8fbd4-127">ASP.NET Core에 대한 자세한 내용은 [ASP.NET Core 설명서](https://docs.microsoft.com/aspnet/core/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-127">To learn more about ASP.NET Core, see the [ASP.NET Core Documentation](https://docs.microsoft.com/aspnet/core/).</span></span>

> [!NOTE]
> <span data-ttu-id="8fbd4-128">이 자습서는 [Visual Studio 2017용 ASP.NET Core 도구](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc)를 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-128">This tutorial is based on the [ASP.NET Core tools for Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span></span> <span data-ttu-id="8fbd4-129">Visual Studio 2015용 .NET Core 도구는 더 이상 업데이트되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-129">The .NET Core tools for Visual Studio 2015 are no longer being updated.</span></span>

1. <span data-ttu-id="8fbd4-130">**관리자** 권한으로 Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-130">Launch Visual Studio as an **administrator**.</span></span>

2. <span data-ttu-id="8fbd4-131">**파일**->**새로 만들기**->**프로젝트**로 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-131">Create a project with **File**->**New**->**Project**</span></span>

3. <span data-ttu-id="8fbd4-132">**새 프로젝트** 대화 상자에서 **클라우드 > Service Fabric 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-132">In the **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

4. <span data-ttu-id="8fbd4-133">응용 프로그램의 이름을 **Voting**으로 지정하고 **확인**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-133">Name the application **Voting** and press **OK**.</span></span>

   ![Visual Studio의 새 프로젝트 대화 상자](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. <span data-ttu-id="8fbd4-135">**새 Service Fabric 서비스** 페이지에서 **상태 비저장 ASP.NET Core**를 선택하고 서비스 이름을 **VotingWeb**으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-135">On the **New Service Fabric Service** page, choose **Stateless ASP.NET Core**, and name your service **VotingWeb**.</span></span>
   
   ![새 서비스 대화 상자에서 ASP.NET 웹 서비스 선택](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. <span data-ttu-id="8fbd4-137">다음 페이지에서는 ASP.NET Core 프로젝트 템플릿 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-137">The next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="8fbd4-138">이 자습서에서는 **웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-138">For this tutorial, choose **Web Application**.</span></span> 
   
   ![ASP.NET 프로젝트 형식 선택](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   <span data-ttu-id="8fbd4-140">Visual Studio는 응용 프로그램 및 서비스 프로젝트를 만들고 솔루션 탐색기에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-140">Visual Studio creates an application and a service project and displays them in Solution Explorer.</span></span>

   ![ASP.NET core Web API 서비스를 사용하여 응용 프로그램 만들기를 수행하는 솔루션 탐색기]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-to-the-votingweb-service"></a><span data-ttu-id="8fbd4-142">VotingWeb 서비스에 AngularJS 추가</span><span class="sxs-lookup"><span data-stu-id="8fbd4-142">Add AngularJS to the VotingWeb service</span></span>
<span data-ttu-id="8fbd4-143">기본 제공 [브라우저 지원](/aspnet/core/client-side/bower)을 사용하여 서비스에 [AngularJS](http://angularjs.org/)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-143">Add [AngularJS](http://angularjs.org/) to your service using the built-in [Bower support](/aspnet/core/client-side/bower).</span></span> <span data-ttu-id="8fbd4-144">*bower.json*을 열고 각도 및 각도 부트스트랩에 항목을 추가한 후 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-144">Open *bower.json* and add entries for angular and angular-bootstrap, then save your changes.</span></span>

```json
{
  "name": "asp.net",
  "private": true,
  "dependencies": {
    "bootstrap": "3.3.7",
    "jquery": "2.2.0",
    "jquery-validation": "1.14.0",
    "jquery-validation-unobtrusive": "3.2.6",
    "angular": "v1.6.5",
    "angular-bootstrap": "v1.1.0"
  }
}
```
<span data-ttu-id="8fbd4-145">*bower.json* 파일을 저장한 다음 각도가 프로젝트의 *wwwroot/lib* 폴더에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-145">Upon saving the *bower.json* file, Angular is installed in your project's *wwwroot/lib* folder.</span></span> <span data-ttu-id="8fbd4-146">또한 *Dependencies/Bower* 폴더 내에서 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-146">Additionally, it is listed within the *Dependencies/Bower* folder.</span></span>

### <a name="update-the-sitejs-file"></a><span data-ttu-id="8fbd4-147">site.js 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="8fbd4-147">Update the site.js file</span></span>
<span data-ttu-id="8fbd4-148">*wwwroot/js/site.js* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-148">Open the *wwwroot/js/site.js* file.</span></span>  <span data-ttu-id="8fbd4-149">홈 보기에서 사용한 JavaScript로 해당 내용을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-149">Replace its contents with the JavaScript used by the Home views:</span></span>

```javascript
var app = angular.module('VotingApp', ['ui.bootstrap']);
app.run(function () { });

app.controller('VotingAppController', ['$rootScope', '$scope', '$http', '$timeout', function ($rootScope, $scope, $http, $timeout) {

    $scope.refresh = function () {
        $http.get('api/Votes?c=' + new Date().getTime())
            .then(function (data, status) {
                $scope.votes = data;
            }, function (data, status) {
                $scope.votes = undefined;
            });
    };

    $scope.remove = function (item) {
        $http.delete('api/Votes/' + item)
            .then(function (data, status) {
                $scope.refresh();
            })
    };

    $scope.add = function (item) {
        var fd = new FormData();
        fd.append('item', item);
        $http.put('api/Votes/' + item, fd, {
            transformRequest: angular.identity,
            headers: { 'Content-Type': undefined }
        })
            .then(function (data, status) {
                $scope.refresh();
                $scope.item = undefined;
            })
    };
}]);
```

### <a name="update-the-indexcshtml-file"></a><span data-ttu-id="8fbd4-150">Index.cshtml 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="8fbd4-150">Update the Index.cshtml file</span></span>
<span data-ttu-id="8fbd4-151">홈 컨트롤러에 특정된 보기인 *Views/Home/Index.cshtml* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-151">Open the *Views/Home/Index.cshtml* file, the view specific to the Home controller.</span></span>  <span data-ttu-id="8fbd4-152">해당 내용을 다음으로 바꾸고 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-152">Replace its contents with the following, then save your changes.</span></span>

```html
@{
    ViewData["Title"] = "Service Fabric Voting Sample";
}

<div ng-controller="VotingAppController" ng-init="refresh()">
    <div class="container-fluid">
        <div class="row">
            <div class="col-xs-8 col-xs-offset-2 text-center">
                <h2>Service Fabric Voting Sample</h2>
            </div>
        </div>

        <div class="row">
            <div class="col-xs-8 col-xs-offset-2">
                <form class="col-xs-12 center-block">
                    <div class="col-xs-6 form-group">
                        <input id="txtAdd" type="text" class="form-control" placeholder="Add voting option" ng-model="item" />
                    </div>
                    <button id="btnAdd" class="btn btn-default" ng-click="add(item)">
                        <span class="glyphicon glyphicon-plus" aria-hidden="true"></span>
                        Add
                    </button>
                </form>
            </div>
        </div>

        <hr />

        <div class="row">
            <div class="col-xs-8 col-xs-offset-2">
                <div class="row">
                    <div class="col-xs-4">
                        Click to vote
                    </div>
                </div>
                <div class="row top-buffer" ng-repeat="vote in votes.data">
                    <div class="col-xs-8">
                        <button class="btn btn-success text-left btn-block" ng-click="add(vote.key)">
                            <span class="pull-left">
                                {{vote.key}}
                            </span>
                            <span class="badge pull-right">
                                {{vote.value}} Votes
                            </span>
                        </button>
                    </div>
                    <div class="col-xs-4">
                        <button class="btn btn-danger pull-right btn-block" ng-click="remove(vote.key)">
                            <span class="glyphicon glyphicon-remove" aria-hidden="true"></span>
                            Remove
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
```

### <a name="update-the-layoutcshtml-file"></a><span data-ttu-id="8fbd4-153">_Layout.cshtml 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="8fbd4-153">Update the _Layout.cshtml file</span></span>
<span data-ttu-id="8fbd4-154">ASP.NET 앱에 대한 기본 레이아웃인 *Views/Shared/_Layout.cshtml* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-154">Open the *Views/Shared/_Layout.cshtml* file, the default layout for the ASP.NET app.</span></span>  <span data-ttu-id="8fbd4-155">해당 내용을 다음으로 바꾸고 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-155">Replace its contents with the following, then save your changes.</span></span>

```html
<!DOCTYPE html>
<html ng-app="VotingApp" xmlns:ng="http://angularjs.org">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>@ViewData["Title"]</title>

    <link href="~/lib/bootstrap/dist/css/bootstrap.min.css" rel="stylesheet" />
    <link href="~/css/site.css" rel="stylesheet" />

</head>
<body>
    <div class="container body-content">
        @RenderBody()
    </div>

    <script src="~/lib/jquery/dist/jquery.js"></script>
    <script src="~/lib/bootstrap/dist/js/bootstrap.js"></script>
    <script src="~/lib/angular/angular.js"></script>
    <script src="~/lib/angular-bootstrap/ui-bootstrap-tpls.js"></script>
    <script src="~/js/site.js"></script>

    @RenderSection("Scripts", required: false)
</body>
</html>
```

### <a name="update-the-votingwebcs-file"></a><span data-ttu-id="8fbd4-156">VotingWeb.cs 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="8fbd4-156">Update the VotingWeb.cs file</span></span>
<span data-ttu-id="8fbd4-157">WebListener 웹 서버를 사용하여 상태 비저장 서비스 내에 ASP.NET Core 웹 호스트를 만드는 *VotingWeb.cs* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-157">Open the *VotingWeb.cs* file, which creates the ASP.NET Core WebHost inside the stateless service using the WebListener web server.</span></span>  <span data-ttu-id="8fbd4-158">파일 맨 위에 `using System.Net.Http;` 지시문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-158">Add the `using System.Net.Http;` directive to the top of the file.</span></span>  <span data-ttu-id="8fbd4-159">`CreateServiceInstanceListeners()` 함수를 다음으로 바꾸고 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-159">Replace the `CreateServiceInstanceListeners()` function with the following, then save your changes.</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
            {
                ServiceEventSource.Current.ServiceMessage(serviceContext, $"Starting WebListener on {url}");

                return new WebHostBuilder().UseWebListener()
                            .ConfigureServices(
                                services => services
                                    .AddSingleton<StatelessServiceContext>(serviceContext)
                                    .AddSingleton<HttpClient>())
                            .UseContentRoot(Directory.GetCurrentDirectory())
                            .UseStartup<Startup>()
                            .UseApplicationInsights()
                            .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                            .UseUrls(url)
                            .Build();
            }))
    };
}
```

### <a name="add-the-votescontrollercs-file"></a><span data-ttu-id="8fbd4-160">VotesController.cs 파일 추가</span><span class="sxs-lookup"><span data-stu-id="8fbd4-160">Add the VotesController.cs file</span></span>
<span data-ttu-id="8fbd4-161">투표 작업을 정의하는 컨트롤러를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-161">Add a controller which defines voting actions.</span></span> <span data-ttu-id="8fbd4-162">**Controllers** 폴더를 마우스 오른쪽 단추로 클릭하고 **추가->새 항목->클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-162">Right-click on the **Controllers** folder, then select **Add->New item->Class**.</span></span>  <span data-ttu-id="8fbd4-163">파일 이름을 "VotesController.cs"로 지정하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-163">Name the file "VotesController.cs" and click **Add**.</span></span>  <span data-ttu-id="8fbd4-164">파일 내용을 다음으로 바꾸고 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-164">Replace the file contents with the following, then save your changes.</span></span>  <span data-ttu-id="8fbd4-165">뒷부분의 [VotesController.cs 파일 업데이트](#updatevotecontroller_anchor)에서 백 엔드 서비스의 투표 데이터를 읽고 쓰도록 이 파일을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-165">Later, in [Update the VotesController.cs file](#updatevotecontroller_anchor), this file will be modified to read and write voting data from the back-end service.</span></span>  <span data-ttu-id="8fbd4-166">지금은 컨트롤러가 보기에 고정 문자열 데이터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-166">For now, the controller returns static string data to the view.</span></span>

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using System.Collections.Generic;
using Newtonsoft.Json;
using System.Text;
using System.Net.Http;
using System.Net.Http.Headers;

namespace VotingWeb.Controllers
{
    [Produces("application/json")]
    [Route("api/Votes")]
    public class VotesController : Controller
    {
        private readonly HttpClient httpClient;

        public VotesController(HttpClient httpClient)
        {
            this.httpClient = httpClient;
        }

        // GET: api/Votes
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            List<KeyValuePair<string, int>> votes= new List<KeyValuePair<string, int>>();
            votes.Add(new KeyValuePair<string, int>("Pizza", 3));
            votes.Add(new KeyValuePair<string, int>("Ice cream", 4));

            return Json(votes);
        }
     }
}
```



### <a name="deploy-and-run-the-application-locally"></a><span data-ttu-id="8fbd4-167">로컬로 응용 프로그램 배포 및 실행</span><span class="sxs-lookup"><span data-stu-id="8fbd4-167">Deploy and run the application locally</span></span>
<span data-ttu-id="8fbd4-168">이제 진행하여 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-168">You can now go ahead and run the application.</span></span> <span data-ttu-id="8fbd4-169">Visual Studio에서 `F5`를 눌러 응용 프로그램을 디버깅하기 위해 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-169">In Visual Studio, press `F5` to deploy the application for debugging.</span></span> <span data-ttu-id="8fbd4-170">**관리자** 권한으로 Visual Studio를 이전에 열지 않은 경우 `F5` 키가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-170">`F5` fails if you didn't previously open Visual Studio as **administrator**.</span></span>

> [!NOTE]
> <span data-ttu-id="8fbd4-171">로컬에서 처음으로 응용 프로그램을 실행하고 배포할 때 Visual Studio는 디버깅을 위해 로컬 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-171">The first time you run and deploy the application locally, Visual Studio creates a local cluster for debugging.</span></span>  <span data-ttu-id="8fbd4-172">클러스터 생성에는 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-172">Cluster creation may take some time.</span></span> <span data-ttu-id="8fbd4-173">Visual Studio 출력 창에 클러스터 생성 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-173">The cluster creation status is displayed in the Visual Studio output window.</span></span>

<span data-ttu-id="8fbd4-174">이 시점에서 웹앱은 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-174">At this point, your web app should look like this:</span></span>

![ASP.NET Core 프런트 엔드](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

<span data-ttu-id="8fbd4-176">응용 프로그램 디버깅을 중지하려면 Visual Studio로 돌아가 **Shift+F5** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-176">To stop debugging the application, go back to Visual Studio and press **Shift+F5**.</span></span>

## <a name="add-a-stateful-back-end-service-to-your-application"></a><span data-ttu-id="8fbd4-177">상태 저장 백 엔드 서비스를 응용 프로그램에 추가</span><span class="sxs-lookup"><span data-stu-id="8fbd4-177">Add a stateful back-end service to your application</span></span>
<span data-ttu-id="8fbd4-178">이제 응용 프로그램에서 실행되는 ASP.NET Web API 서비스가 있으므로 계속해서 상태 저장 신뢰할 수 있는 서비스 추가하여 응용 프로그램에 일부 데이터를 저장해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-178">Now that we have an ASP.NET Web API service running in our application, let's go ahead and add a stateful reliable service to store some data in our application.</span></span>

<span data-ttu-id="8fbd4-179">Service Fabric을 통해 신뢰할 수 있는 컬렉션을 사용하여 일관되고 안정적으로 서비스 내에 데이터를 바로 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-179">Service Fabric allows you to consistently and reliably store your data right inside your service by using reliable collections.</span></span> <span data-ttu-id="8fbd4-180">신뢰할 수 있는 컬렉션은 C# 컬렉션을 사용해본 적이 있는 사람에게 친숙한 신뢰할 수 있는 고가용성 컬렉션 클래스의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-180">Reliable collections are a set of highly available and reliable collection classes that are familiar to anyone who has used C# collections.</span></span>

<span data-ttu-id="8fbd4-181">이 자습서에서는 신뢰할 수 있는 컬렉션에 카운터 값을 저장하는 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-181">In this tutorial, you create a service which stores a counter value in a reliable collection.</span></span>

1. <span data-ttu-id="8fbd4-182">솔루션 탐색기에서 응용 프로그램 프로젝트 내의 **서비스**를 마우스 오른쪽 단추로 클릭하고 **추가 > 새 Service Fabric 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-182">In Solution Explorer, right-click **Services** within the application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![기존 응용 프로그램에 새 서비스 추가](./media/service-fabric-tutorial-create-dotnet-app/vs-add-new-service.png)

2. <span data-ttu-id="8fbd4-184">**새 Service Fabric 서비스** 대화 상자에서 **상태 저장 ASP.NET Core**를 선택하고 서비스 이름을 **VotingData**로 지정하고 **확인**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-184">In the **New Service Fabric Service** dialog, choose **Stateful ASP.NET Core**, and name the service **VotingData** and press **OK**.</span></span>

    ![Visual Studio의 새 서비스 대화 상자](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    <span data-ttu-id="8fbd4-186">서비스 프로젝트를 만들었으면 응용 프로그램에 두 개의 서비스가 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-186">Once your service project is created, you have two services in your application.</span></span> <span data-ttu-id="8fbd4-187">계속해서 응용 프로그램을 빌드하는 동안 같은 방법으로 더 많은 서비스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-187">As you continue to build your application, you can add more services in the same way.</span></span> <span data-ttu-id="8fbd4-188">각 서비스를 독립적으로 버전 지정 및 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-188">Each can be independently versioned and upgraded.</span></span>

3. <span data-ttu-id="8fbd4-189">다음 페이지에서는 ASP.NET Core 프로젝트 템플릿 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-189">The next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="8fbd4-190">이 자습서에서는 **Web API**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-190">For this tutorial, choose **Web API**.</span></span>

    ![ASP.NET 프로젝트 형식 선택](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    <span data-ttu-id="8fbd4-192">Visual Studio는 서비스 프로젝트를 만들고 솔루션 탐색기에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-192">Visual Studio creates a service project and displays them in Solution Explorer.</span></span>

    ![솔루션 탐색기](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-the-votedatacontrollercs-file"></a><span data-ttu-id="8fbd4-194">VoteDataController.cs 파일 추가</span><span class="sxs-lookup"><span data-stu-id="8fbd4-194">Add the VoteDataController.cs file</span></span>

<span data-ttu-id="8fbd4-195">**VotingData** 프로젝트에서 **Controllers** 폴더를 마우스 오른쪽 단추로 클릭하고 **추가->새 항목->클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-195">In the **VotingData** project right-click on the **Controllers** folder, then select **Add->New item->Class**.</span></span> <span data-ttu-id="8fbd4-196">파일 이름을 "VoteDataController.cs"로 지정하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-196">Name the file "VoteDataController.cs" and click **Add**.</span></span> <span data-ttu-id="8fbd4-197">파일 내용을 다음으로 바꾸고 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-197">Replace the file contents with the following, then save your changes.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using Microsoft.ServiceFabric.Data;
using System.Threading;
using Microsoft.ServiceFabric.Data.Collections;

namespace VotingData.Controllers
{
    [Route("api/[controller]")]
    public class VoteDataController : Controller
    {
        private readonly IReliableStateManager stateManager;

        public VoteDataController(IReliableStateManager stateManager)
        {
            this.stateManager = stateManager;
        }

        // GET api/VoteData
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            var ct = new CancellationToken();

            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                var list = await votesDictionary.CreateEnumerableAsync(tx);

                var enumerator = list.GetAsyncEnumerator();

                var result = new List<KeyValuePair<string, int>>();

                while (await enumerator.MoveNextAsync(ct))
                {
                    result.Add(enumerator.Current);
                }

                return Json(result);
            }
        }

        // PUT api/VoteData/name
        [HttpPut("{name}")]
        public async Task<IActionResult> Put(string name)
        {
            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                await votesDictionary.AddOrUpdateAsync(tx, name, 1, (key, oldvalue) => oldvalue + 1);
                await tx.CommitAsync();
            }

            return new OkResult();
        }

        // DELETE api/VoteData/name
        [HttpDelete("{name}")]
        public async Task<IActionResult> Delete(string name)
        {
            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                if (await votesDictionary.ContainsKeyAsync(tx, name))
                {
                    await votesDictionary.TryRemoveAsync(tx, name);
                    await tx.CommitAsync();
                    return new OkResult();
                }
                else
                {
                    return new NotFoundResult();
                }
            }
        }
    }
}
```


## <a name="connect-the-services"></a><span data-ttu-id="8fbd4-198">서비스 연결</span><span class="sxs-lookup"><span data-stu-id="8fbd4-198">Connect the services</span></span>
<span data-ttu-id="8fbd4-199">다음 단계에서는 두 서비스를 연결하고 프런트 엔드 웹 응용 프로그램이 백 엔드 서비스에서 투표 정보를 가져오고 설정하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-199">In this next step, we will connect the two services and make the front-end Web application get and set voting information from the back-end service.</span></span>

<span data-ttu-id="8fbd4-200">서비스 패브릭은 신뢰할 수 있는 서비스와 유연하게 통신할 수 있는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-200">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="8fbd4-201">단일 응용 프로그램 내에는 TCP를 통해 액세스할 수 있는 서비스가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-201">Within a single application, you might have services that are accessible via TCP.</span></span> <span data-ttu-id="8fbd4-202">HTTP REST API 및 다른 서비스를 통해 액세스할 수 있는 기타 서비스는 웹 소켓을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-202">Other services that might be accessible via an HTTP REST API and still other services could be accessible via web sockets.</span></span> <span data-ttu-id="8fbd4-203">제공되는 옵션 및 관련 장단점에 대한 배경 정보는 [서비스와의 통신](service-fabric-connect-and-communicate-with-services.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-203">For background on the options available and the tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

<span data-ttu-id="8fbd4-204">이 자습서에서 [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-204">In this tutorial, we are using [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-the-votescontrollercs-file"></a><span data-ttu-id="8fbd4-205">VotesController.cs 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="8fbd4-205">Update the VotesController.cs file</span></span>
<span data-ttu-id="8fbd4-206">**VotingWeb** 프로젝트에서 *Controllers/VotesController.cs* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-206">In the **VotingWeb** project, open the *Controllers/VotesController.cs* file.</span></span>  <span data-ttu-id="8fbd4-207">`VotesController` 클래스 정의 내용을 다음으로 바꾸고 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-207">Replace the `VotesController` class definition contents with the following, then save your changes.</span></span>

```csharp
    public class VotesController : Controller
    {
        private readonly HttpClient httpClient;
        string serviceProxyUrl = "http://localhost:19081/Voting/VotingData/api/VoteData";
        string partitionKind = "Int64Range";
        string partitionKey = "0";

        public VotesController(HttpClient httpClient)
        {
            this.httpClient = httpClient;
        }

        // GET: api/Votes
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            IEnumerable<KeyValuePair<string, int>> votes;

            HttpResponseMessage response = await this.httpClient.GetAsync($"{serviceProxyUrl}?PartitionKind={partitionKind}&PartitionKey={partitionKey}");

            if (response.StatusCode != System.Net.HttpStatusCode.OK)
            {
                return this.StatusCode((int)response.StatusCode);
            }

            votes = JsonConvert.DeserializeObject<List<KeyValuePair<string, int>>>(await response.Content.ReadAsStringAsync());

            return Json(votes);
        }

        // PUT: api/Votes/name
        [HttpPut("{name}")]
        public async Task<IActionResult> Put(string name)
        {
            string payload = $"{{ 'name' : '{name}' }}";
            StringContent putContent = new StringContent(payload, Encoding.UTF8, "application/json");
            putContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");

            string proxyUrl = $"{serviceProxyUrl}/{name}?PartitionKind={partitionKind}&PartitionKey={partitionKey}";

            HttpResponseMessage response = await this.httpClient.PutAsync(proxyUrl, putContent);

            return new ContentResult()
            {
                StatusCode = (int)response.StatusCode,
                Content = await response.Content.ReadAsStringAsync()
            };
        }

        // DELETE: api/Votes/name
        [HttpDelete("{name}")]
        public async Task<IActionResult> Delete(string name)
        {
            HttpResponseMessage response = await this.httpClient.DeleteAsync($"{serviceProxyUrl}/{name}?PartitionKind={partitionKind}&PartitionKey={partitionKey}");

            if (response.StatusCode != System.Net.HttpStatusCode.OK)
            {
                return this.StatusCode((int)response.StatusCode);
            }

            return new OkResult();

        }
    }
```
<a id="walkthrough" name="walkthrough_anchor"></a>

## <a name="walk-through-the-voting-sample-application"></a><span data-ttu-id="8fbd4-208">투표 응용 프로그램 예제 연습</span><span class="sxs-lookup"><span data-stu-id="8fbd4-208">Walk through the voting sample application</span></span>
<span data-ttu-id="8fbd4-209">투표 응용 프로그램은 두 가지 서비스로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-209">The voting application consists of two services:</span></span>
- <span data-ttu-id="8fbd4-210">웹 프런트 엔드 서비스(VotingWeb) - ASP.NET Core 웹 프런트 엔드 서비스로, 웹 페이지를 제공하며 백 엔드 서비스와 통신하기 위한 Web API를 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-210">Web front-end service (VotingWeb)- An ASP.NET Core web front-end service, which serves the web page and exposes web APIs to communicate with the backend service.</span></span>
- <span data-ttu-id="8fbd4-211">백 엔드 서비스(VotingData) - ASP.NET Core 웹 서비스로, 투표 결과를 디스크에 보관된 신뢰할 수 있는 사전에 저장하기 위한 API를 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-211">Back-end service (VotingData)- An ASP.NET Core web service, which exposes an API to store the vote results in a reliable dictionary persisted on disk.</span></span>

![응용 프로그램 다이어그램](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="8fbd4-213">응용 프로그램에 투표하는 경우 다음 이벤트가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-213">When you vote in the application the following events occur:</span></span>
1. <span data-ttu-id="8fbd4-214">JavaScript가 투표 요청을 웹 프런트 엔드 서비스의 Web API에 HTTP PUT 요청으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-214">A JavaScript sends the vote request to the web API in the web front-end service as an HTTP PUT request.</span></span>

2. <span data-ttu-id="8fbd4-215">웹 프런트 엔드 서비스는 프록시를 사용하여 HTTP PUT 요청을 찾아 백 엔드 서비스에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-215">The web front-end service uses a proxy to locate and forward an HTTP PUT request to the back-end service.</span></span>

3. <span data-ttu-id="8fbd4-216">백 엔드 서비스는 들어오는 요청을 받고 업데이트된 결과를, 클러스터 내의 여러 노드에 복제되고 디스크에 보관된 신뢰할 수 있는 사전에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-216">The back-end service takes the incoming request, and stores the updated result in a reliable dictionary, which gets replicated to multiple nodes within the cluster and persisted on disk.</span></span> <span data-ttu-id="8fbd4-217">응용 프로그램의 모든 데이터가 클러스터에 저장되므로 데이터베이스가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-217">All the application's data is stored in the cluster, so no database is needed.</span></span>

## <a name="debug-in-visual-studio"></a><span data-ttu-id="8fbd4-218">Visual Studio에서 디버그</span><span class="sxs-lookup"><span data-stu-id="8fbd4-218">Debug in Visual Studio</span></span>
<span data-ttu-id="8fbd4-219">Visual Studio에서 응용 프로그램을 디버깅할 때 로컬 Service Fabric 개발 클러스터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-219">When debugging application in Visual Studio, you are using a local Service Fabric development cluster.</span></span> <span data-ttu-id="8fbd4-220">사용자 시나리오에 대해 디버깅 환경을 조정하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-220">You have the option to adjust your debugging experience to your scenario.</span></span> <span data-ttu-id="8fbd4-221">이 응용 프로그램에서는 신뢰할 수 있는 사전을 사용하여 데이터를 백 엔드 서비스에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-221">In this application, we store data in our back-end service, using a reliable dictionary.</span></span> <span data-ttu-id="8fbd4-222">Visual Studio는 디버거를 중지하는 경우 기본값에 대해 응용 프로그램을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-222">Visual Studio removes the application per default when you stop the debugger.</span></span> <span data-ttu-id="8fbd4-223">응용 프로그램을 제거하면 백 엔드 서비스의 데이터도 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-223">Removing the application causes the data in the back-end service to also be removed.</span></span> <span data-ttu-id="8fbd4-224">디버깅 세션 간에 데이터를 유지하려면 **응용 프로그램 디버그 모드**를 Visual Studio에서 **Voting** 프로젝트의 속성으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-224">To persist the data between debugging sessions, you can change the **Application Debug Mode** as a property on the **Voting** project in Visual Studio.</span></span>

<span data-ttu-id="8fbd4-225">코드에서 수행되는 작업을 살펴보려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-225">To look at what happens in the code, complete the following steps:</span></span>
1. <span data-ttu-id="8fbd4-226">**VotesController.cs** 파일을 열고 Web API의 **Put** 메서드(47줄)에서 중단점을 설정합니다. Visual Studio의 솔루션 탐색기에서 파일을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-226">Open the **VotesController.cs** file and set a breakpoint in the web API's **Put** method (line 47) - You can search for the file in the Solution Explorer in Visual Studio.</span></span>

2. <span data-ttu-id="8fbd4-227">**VoteDataController.cs** 파일을 열고 이 Web API의 **Put** 메서드(50줄)에서 중단점을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-227">Open the **VoteDataController.cs** file and set a breakpoint in this web API's **Put** method (line 50).</span></span>

3. <span data-ttu-id="8fbd4-228">브라우저로 돌아가서 투표 옵션을 클릭하거나 새 투표 옵션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-228">Go back to the browser and click a voting option or add a new voting option.</span></span> <span data-ttu-id="8fbd4-229">웹 프런트 엔드의 api 컨트롤러에서 첫 번째 중단점에 도달합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-229">You hit the first breakpoint in the web front-end's api controller.</span></span>
    
    1. <span data-ttu-id="8fbd4-230">여기서 브라우저의 JavaScript가 프런트 엔드 서비스의 Web API 컨트롤러에 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-230">This is where the JavaScript in the browser sends a request to the web API controller in the front-end service.</span></span>
    
    ![투표 프런트 엔드 서비스 추가](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. <span data-ttu-id="8fbd4-232">먼저 백 엔드 서비스 **(1)**에 대해 ReverseProxy에 대한 URL을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-232">First we construct the URL to the ReverseProxy for our back-end service **(1)**.</span></span>
    3. <span data-ttu-id="8fbd4-233">그런 다음 ReverseProxy **(2)**에 HTTP PUT 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-233">Then we send the HTTP PUT Request to the ReverseProxy **(2)**.</span></span>
    4. <span data-ttu-id="8fbd4-234">마지막으로로 백 엔드 서비스로부터 클라이언트 **(3)**에 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-234">Finally the we return the response from the back-end service to the client **(3)**.</span></span>

4. <span data-ttu-id="8fbd4-235">계속하려면 **F5** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-235">Press **F5** to continue</span></span>
    1. <span data-ttu-id="8fbd4-236">이제 백 엔드 서비스의 중단점에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-236">You are now at the break point in the back-end service.</span></span>
    
    ![투표 백 엔드 서비스 추가](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. <span data-ttu-id="8fbd4-238">메서드의 첫 번째 줄**(1)**에서는 신뢰할 수 있는 사전 `counts`를 가져오거나 추가하기 위해 `StateManager`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-238">In the first line in the method **(1)** we are using the `StateManager` to get or add a reliable dictionary called `counts`.</span></span>
    3. <span data-ttu-id="8fbd4-239">신뢰할 수 있는 사전에 있는 값과의 모든 상호 작용에는 트랜잭션이 필요하며 using 문**(2)**으로 트랜잭션이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-239">All interactions with values in a reliable dictionary require a transaction, this using statement **(2)** creates that transaction.</span></span>
    4. <span data-ttu-id="8fbd4-240">트랜잭션에서는 투표 옵션에 대한 관련 키 값을 업데이트하고 작업을 커밋합니다**(3)**.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-240">In the transaction, we then update the value of the relevant key for the voting option and commits the operation **(3)**.</span></span> <span data-ttu-id="8fbd4-241">커밋 메서드가 반환되면 사전에 데이터가 업데이트되고 클러스터의 다른 노드에 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-241">Once the commit method returns, the data is updated in the dictionary and replicated to other nodes in the cluster.</span></span> <span data-ttu-id="8fbd4-242">이제 데이터는 클러스터에 안전하게 저장되며 백 엔드 서비스는 데이터를 계속 제공하면서 다른 노드로 장애 조치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-242">The data is now safely stored in the cluster, and the back-end service can fail over to other nodes, still having the data available.</span></span>
5. <span data-ttu-id="8fbd4-243">계속하려면 **F5** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-243">Press **F5** to continue</span></span>

<span data-ttu-id="8fbd4-244">디버깅 세션을 중지하려면 **Shift+F5** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-244">To stop the debugging session, press **Shift+F5**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8fbd4-245">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8fbd4-245">Next steps</span></span>
<span data-ttu-id="8fbd4-246">자습서의 이 부분에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-246">In this part of the tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8fbd4-247">ASP.NET Core Web API 서비스를 상태 저장 Reliable Service로 만들기</span><span class="sxs-lookup"><span data-stu-id="8fbd4-247">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="8fbd4-248">ASP.NET Core Web 응용 프로그램 서비스를 상태 비저장 웹 서비스로 만들기</span><span class="sxs-lookup"><span data-stu-id="8fbd4-248">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="8fbd4-249">역방향 프록시를 사용하여 상태 저장 서비스와 통신</span><span class="sxs-lookup"><span data-stu-id="8fbd4-249">Use the reverse proxy to communicate with the stateful service</span></span>

<span data-ttu-id="8fbd4-250">다음 자습서를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbd4-250">Advance to the next tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="8fbd4-251">Azure에 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="8fbd4-251">Deploy the application to Azure</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)