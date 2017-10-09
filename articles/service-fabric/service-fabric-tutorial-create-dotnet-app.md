---
title: "서비스 패브릭 용.NET 응용 프로그램 aaaCreate | Microsoft Docs"
description: "Toocreate 프런트 엔드는 ASP.NET Core 및는 신뢰할 수 있는 응용 프로그램을 상태 저장 백 엔드 서비스 방법과 hello 응용 프로그램 tooa 클러스터 배포에 대해 알아봅니다."
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
ms.openlocfilehash: bab331b9f8616c50a2794b6c048aace15579c8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a><span data-ttu-id="9cbce-103">ASP.NET Core Web API 프런트 엔드 서비스 및 상태 저장 백 엔드 서비스로 응용 프로그램 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="9cbce-103">Create and deploy an application with an ASP.NET Core Web API front-end service and a stateful back-end service</span></span>
<span data-ttu-id="9cbce-104">이 자습서는 시리즈의 1부입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-104">This tutorial is part one of a series.</span></span>  <span data-ttu-id="9cbce-105">배웁니다 어떤 toocreate ASP.NET Core 웹 API 앞으로 Azure 서비스 패브릭 응용 프로그램을 시작 하 고 상태 저장 서비스의 백 엔드 toostore 데이터.</span><span class="sxs-lookup"><span data-stu-id="9cbce-105">You will learn how toocreate an Azure Service Fabric application with an ASP.NET Core Web API front end and a stateful back-end service toostore your data.</span></span> <span data-ttu-id="9cbce-106">완료 되 면 hello 클러스터에서 상태 저장 백 엔드 서비스의 응답 결과 저장 하는 프런트 엔드는 ASP.NET Core 웹 응용 프로그램을 응답 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-106">When you're finished, you have a voting application with an ASP.NET Core web front-end that saves voting results in a stateful back-end service in hello cluster.</span></span> <span data-ttu-id="9cbce-107">Toomanually 않으려면 hello 투표 응용 프로그램 만들기, 할 수 있습니다 [hello 소스 코드 다운로드](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) hello에 대 한 응용 프로그램을 완료 하 고 너무 건너 뛸[hello 샘플 응용 프로그램 투표 하는 과정을 안내](#walkthrough_anchor)합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-107">If you don't want toomanually create hello voting application, you can [download hello source code](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) for hello completed application and skip ahead too[Walk through hello voting sample application](#walkthrough_anchor).</span></span>

![응용 프로그램 다이어그램](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="9cbce-109">Hello 시리즈의 1 부에서는 학습 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="9cbce-109">In part one of hello series, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9cbce-110">ASP.NET Core Web API 서비스를 상태 저장 Reliable Service로 만들기</span><span class="sxs-lookup"><span data-stu-id="9cbce-110">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="9cbce-111">ASP.NET Core Web 응용 프로그램 서비스를 상태 비저장 웹 서비스로 만들기</span><span class="sxs-lookup"><span data-stu-id="9cbce-111">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="9cbce-112">Hello 역방향 프록시 toocommunicate hello 상태 저장 서비스와 함께 사용</span><span class="sxs-lookup"><span data-stu-id="9cbce-112">Use hello reverse proxy toocommunicate with hello stateful service</span></span>

<span data-ttu-id="9cbce-113">이 자습서 시리즈에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-113">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="9cbce-114">.NET Service Fabric 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="9cbce-114">Build a .NET Service Fabric application</span></span>
> * [<span data-ttu-id="9cbce-115">Hello 응용 프로그램 tooa 원격 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="9cbce-115">Deploy hello application tooa remote cluster</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * [<span data-ttu-id="9cbce-116">Visual Studio Team Services를 사용하여 CI/CD 구성</span><span class="sxs-lookup"><span data-stu-id="9cbce-116">Configure CI/CD using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a><span data-ttu-id="9cbce-117">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9cbce-117">Prerequisites</span></span>
<span data-ttu-id="9cbce-118">이 자습서를 시작하기 전에:</span><span class="sxs-lookup"><span data-stu-id="9cbce-118">Before you begin this tutorial:</span></span>
- <span data-ttu-id="9cbce-119">Azure 구독이 없는 경우 [평가판 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-119">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="9cbce-120">[Visual Studio 2017 설치](https://www.visualstudio.com/) hello를 설치 하 고 **Azure 개발** 및 **ASP.NET 및 웹 개발** 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-120">[Install Visual Studio 2017](https://www.visualstudio.com/) and install hello **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="9cbce-121">Hello 서비스 패브릭 SDK 설치</span><span class="sxs-lookup"><span data-stu-id="9cbce-121">Install hello Service Fabric SDK</span></span>](service-fabric-get-started.md)

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a><span data-ttu-id="9cbce-122">ASP.NET Web API 서비스를 신뢰할 수 있는 서비스로 만들기</span><span class="sxs-lookup"><span data-stu-id="9cbce-122">Create an ASP.NET Web API service as a reliable service</span></span>
<span data-ttu-id="9cbce-123">Hello 웹을 프런트 엔드 ASP.NET Core를 사용 하 여 응용 프로그램 투표 hello를 먼저 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-123">First, create hello web front-end of hello voting application using ASP.NET Core.</span></span> <span data-ttu-id="9cbce-124">ASP.NET Core는 플랫폼 간 경량 웹 개발 프레임 워크 toocreate 최신 웹 UI를 사용할 수 있으며 웹 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-124">ASP.NET Core is a lightweight, cross-platform web development framework that you can use toocreate modern web UI and web APIs.</span></span> <span data-ttu-id="9cbce-125">서비스 패브릭 ASP.NET Core 통합 하는 방법을 완전히 이해 tooget 권장 hello를 읽는 [서비스 패브릭 신뢰할 수 있는 서비스에서 ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="9cbce-125">tooget a complete understanding of how ASP.NET Core integrates with Service Fabric, we strongly recommend reading through hello [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) article.</span></span> <span data-ttu-id="9cbce-126">지금은이 자습서에 신속 하 게 시작 tooget을 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-126">For now, you can follow this tutorial tooget started quickly.</span></span> <span data-ttu-id="9cbce-127">ASP.NET Core에 대 한 자세한 toolearn 참조 hello [ASP.NET Core 설명서](https://docs.microsoft.com/aspnet/core/)합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-127">toolearn more about ASP.NET Core, see hello [ASP.NET Core Documentation](https://docs.microsoft.com/aspnet/core/).</span></span>

> [!NOTE]
> <span data-ttu-id="9cbce-128">이 자습서는 hello 기반 [ASP.NET Core l Visual Studio 2017 용 도구](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc)합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-128">This tutorial is based on hello [ASP.NET Core tools for Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span></span> <span data-ttu-id="9cbce-129">Visual Studio 2015 용 hello.NET Core 도구는 더 이상 업데이트 중입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-129">hello .NET Core tools for Visual Studio 2015 are no longer being updated.</span></span>

1. <span data-ttu-id="9cbce-130">**관리자** 권한으로 Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-130">Launch Visual Studio as an **administrator**.</span></span>

2. <span data-ttu-id="9cbce-131">**파일**->**새로 만들기**->**프로젝트**로 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-131">Create a project with **File**->**New**->**Project**</span></span>

3. <span data-ttu-id="9cbce-132">Hello에 **새 프로젝트** 대화 상자에서 선택 **클라우드 > 서비스 패브릭 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-132">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

4. <span data-ttu-id="9cbce-133">Hello 응용 프로그램 이름을 **응답** 누릅니다 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-133">Name hello application **Voting** and press **OK**.</span></span>

   ![Visual Studio의 새 프로젝트 대화 상자](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. <span data-ttu-id="9cbce-135">Hello에 **새 서비스 패브릭 서비스** 페이지에서 선택 **상태 비저장 ASP.NET Core**, 서비스 이름 지정 및 **VotingWeb**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-135">On hello **New Service Fabric Service** page, choose **Stateless ASP.NET Core**, and name your service **VotingWeb**.</span></span>
   
   ![Hello 새 서비스 대화 상자에서 ASP.NET 웹 서비스를 선택합니다.](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. <span data-ttu-id="9cbce-137">hello 다음 페이지는 ASP.NET Core 집합이 프로젝트 템플릿을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-137">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="9cbce-138">이 자습서에서는 **웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-138">For this tutorial, choose **Web Application**.</span></span> 
   
   ![ASP.NET 프로젝트 형식 선택](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   <span data-ttu-id="9cbce-140">Visual Studio는 응용 프로그램 및 서비스 프로젝트를 만들고 솔루션 탐색기에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-140">Visual Studio creates an application and a service project and displays them in Solution Explorer.</span></span>

   ![ASP.NET core Web API 서비스를 사용하여 응용 프로그램 만들기를 수행하는 솔루션 탐색기]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-toohello-votingweb-service"></a><span data-ttu-id="9cbce-142">AngularJS toohello VotingWeb 서비스 추가</span><span class="sxs-lookup"><span data-stu-id="9cbce-142">Add AngularJS toohello VotingWeb service</span></span>
<span data-ttu-id="9cbce-143">추가 [AngularJS](http://angularjs.org/) 기본 제공 hello를 사용 하 여 tooyour 서비스 [지원 Bower](/aspnet/core/client-side/bower)합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-143">Add [AngularJS](http://angularjs.org/) tooyour service using hello built-in [Bower support](/aspnet/core/client-side/bower).</span></span> <span data-ttu-id="9cbce-144">*bower.json*을 열고 각도 및 각도 부트스트랩에 항목을 추가한 후 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-144">Open *bower.json* and add entries for angular and angular-bootstrap, then save your changes.</span></span>

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
<span data-ttu-id="9cbce-145">Hello 저장 시 *bower.json* 파일을 각 프로젝트에 설치 되어 *wwwroot/lib* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-145">Upon saving hello *bower.json* file, Angular is installed in your project's *wwwroot/lib* folder.</span></span> <span data-ttu-id="9cbce-146">또한 hello 내 나열 *종속성/Bower* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-146">Additionally, it is listed within hello *Dependencies/Bower* folder.</span></span>

### <a name="update-hello-sitejs-file"></a><span data-ttu-id="9cbce-147">Hello site.js 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="9cbce-147">Update hello site.js file</span></span>
<span data-ttu-id="9cbce-148">열기 hello *wwwroot/js/site.js* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-148">Open hello *wwwroot/js/site.js* file.</span></span>  <span data-ttu-id="9cbce-149">해당 내용을 hello hello 홈 보기에서 사용 하는 JavaScript로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-149">Replace its contents with hello JavaScript used by hello Home views:</span></span>

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

### <a name="update-hello-indexcshtml-file"></a><span data-ttu-id="9cbce-150">Hello Index.cshtml 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="9cbce-150">Update hello Index.cshtml file</span></span>
<span data-ttu-id="9cbce-151">열기 hello *Views/Home/Index.cshtml* 파일, hello 보기 특정 toohello 홈 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-151">Open hello *Views/Home/Index.cshtml* file, hello view specific toohello Home controller.</span></span>  <span data-ttu-id="9cbce-152">해당 내용을 hello 다음 코드로 바꿉니다 다음 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-152">Replace its contents with hello following, then save your changes.</span></span>

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
                        Click toovote
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

### <a name="update-hello-layoutcshtml-file"></a><span data-ttu-id="9cbce-153">Hello _Layout.cshtml 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="9cbce-153">Update hello _Layout.cshtml file</span></span>
<span data-ttu-id="9cbce-154">열기 hello *Views/Shared/_Layout.cshtml* 파일, hello ASP.NET 응용 프로그램에 대 한 hello 기본 레이아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-154">Open hello *Views/Shared/_Layout.cshtml* file, hello default layout for hello ASP.NET app.</span></span>  <span data-ttu-id="9cbce-155">해당 내용을 hello 다음 코드로 바꿉니다 다음 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-155">Replace its contents with hello following, then save your changes.</span></span>

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

### <a name="update-hello-votingwebcs-file"></a><span data-ttu-id="9cbce-156">Hello VotingWeb.cs 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="9cbce-156">Update hello VotingWeb.cs file</span></span>
<span data-ttu-id="9cbce-157">열기 hello *VotingWeb.cs* 파일 hello WebListener 웹 서버를 사용 하 여 hello 상태 비저장 서비스 내부 hello ASP.NET Core 웹 호스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-157">Open hello *VotingWeb.cs* file, which creates hello ASP.NET Core WebHost inside hello stateless service using hello WebListener web server.</span></span>  <span data-ttu-id="9cbce-158">Hello 추가 `using System.Net.Http;` hello 파일의 지시문 toohello 맨 위로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-158">Add hello `using System.Net.Http;` directive toohello top of hello file.</span></span>  <span data-ttu-id="9cbce-159">Hello 대체 `CreateServiceInstanceListeners()` hello 다음과 같이 작동 한 다음 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-159">Replace hello `CreateServiceInstanceListeners()` function with hello following, then save your changes.</span></span>

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

### <a name="add-hello-votescontrollercs-file"></a><span data-ttu-id="9cbce-160">Hello VotesController.cs 파일 추가</span><span class="sxs-lookup"><span data-stu-id="9cbce-160">Add hello VotesController.cs file</span></span>
<span data-ttu-id="9cbce-161">투표 작업을 정의하는 컨트롤러를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-161">Add a controller which defines voting actions.</span></span> <span data-ttu-id="9cbce-162">Hello를 마우스 오른쪽 단추로 클릭 **컨트롤러** 폴더를 선택 합니다 **추가-새로 만들기 > 항목 클래스->**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-162">Right-click on hello **Controllers** folder, then select **Add->New item->Class**.</span></span>  <span data-ttu-id="9cbce-163">"VotesController.cs" hello 파일 이름을 지정 하 고 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-163">Name hello file "VotesController.cs" and click **Add**.</span></span>  <span data-ttu-id="9cbce-164">Hello 파일 내용을 hello 다음으로 바꾸는 다음 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-164">Replace hello file contents with hello following, then save your changes.</span></span>  <span data-ttu-id="9cbce-165">뒷부분에 나오는 [업데이트 hello VotesController.cs 파일](#updatevotecontroller_anchor),이 파일 수정된 tooread 되며 hello 백 엔드 서비스에서 응답 데이터를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-165">Later, in [Update hello VotesController.cs file](#updatevotecontroller_anchor), this file will be modified tooread and write voting data from hello back-end service.</span></span>  <span data-ttu-id="9cbce-166">지금은 hello 컨트롤러 데이터 toohello 뷰의 정적 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-166">For now, hello controller returns static string data toohello view.</span></span>

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



### <a name="deploy-and-run-hello-application-locally"></a><span data-ttu-id="9cbce-167">배포 하 고 hello 응용 프로그램을 로컬로 실행</span><span class="sxs-lookup"><span data-stu-id="9cbce-167">Deploy and run hello application locally</span></span>
<span data-ttu-id="9cbce-168">이제 계속 진행 하 고 hello 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-168">You can now go ahead and run hello application.</span></span> <span data-ttu-id="9cbce-169">키를 눌러 Visual Studio에서 `F5` toodeploy hello 응용 프로그램을 디버깅 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-169">In Visual Studio, press `F5` toodeploy hello application for debugging.</span></span> <span data-ttu-id="9cbce-170">**관리자** 권한으로 Visual Studio를 이전에 열지 않은 경우 `F5` 키가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-170">`F5` fails if you didn't previously open Visual Studio as **administrator**.</span></span>

> [!NOTE]
> <span data-ttu-id="9cbce-171">hello 처음으로 실행 하 고 hello 응용 프로그램 배포를 로컬로 Visual Studio 디버깅에 대 한 로컬 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-171">hello first time you run and deploy hello application locally, Visual Studio creates a local cluster for debugging.</span></span>  <span data-ttu-id="9cbce-172">클러스터 생성에는 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-172">Cluster creation may take some time.</span></span> <span data-ttu-id="9cbce-173">hello 클러스터 만들기 상태 hello Visual Studio 출력 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-173">hello cluster creation status is displayed in hello Visual Studio output window.</span></span>

<span data-ttu-id="9cbce-174">이 시점에서 웹앱은 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-174">At this point, your web app should look like this:</span></span>

![ASP.NET Core 프런트 엔드](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

<span data-ttu-id="9cbce-176">hello 응용 프로그램을 디버깅 toostop tooVisual Studio 누릅니다 돌아가서 **Shift + f 5**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-176">toostop debugging hello application, go back tooVisual Studio and press **Shift+F5**.</span></span>

## <a name="add-a-stateful-back-end-service-tooyour-application"></a><span data-ttu-id="9cbce-177">상태 저장 서비스의 백 엔드 tooyour 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="9cbce-177">Add a stateful back-end service tooyour application</span></span>
<span data-ttu-id="9cbce-178">응용 프로그램에서 실행 되는 ASP.NET Web API 서비스를 만들었으므로 이제 해당 응용 프로그램의 상태 저장 서비스의 신뢰할 수 있는 toostore 일부 데이터를 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-178">Now that we have an ASP.NET Web API service running in our application, let's go ahead and add a stateful reliable service toostore some data in our application.</span></span>

<span data-ttu-id="9cbce-179">서비스 패브릭 tooconsistently 있으며 안정적으로 신뢰할 수 있는 컬렉션을 사용 하 여 내부 서비스에 직접 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-179">Service Fabric allows you tooconsistently and reliably store your data right inside your service by using reliable collections.</span></span> <span data-ttu-id="9cbce-180">신뢰할 수 있는 컬렉션은 컬렉션 C# 사용 경험이 친숙 한 tooanyone 있는 항상 사용 가능 하 고 신뢰할 수 있는 컬렉션 클래스의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-180">Reliable collections are a set of highly available and reliable collection classes that are familiar tooanyone who has used C# collections.</span></span>

<span data-ttu-id="9cbce-181">이 자습서에서는 신뢰할 수 있는 컬렉션에 카운터 값을 저장하는 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-181">In this tutorial, you create a service which stores a counter value in a reliable collection.</span></span>

1. <span data-ttu-id="9cbce-182">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 **서비스** 내 응용 프로그램 프로젝트 hello 및 선택 **추가 > 새 서비스 패브릭 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-182">In Solution Explorer, right-click **Services** within hello application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![새 서비스 tooan 기존 응용 프로그램 추가](./media/service-fabric-tutorial-create-dotnet-app/vs-add-new-service.png)

2. <span data-ttu-id="9cbce-184">Hello에 **새 서비스 패브릭 서비스** 대화 상자에서 선택 **Stateful ASP.NET Core**, 및 이름 hello 서비스 **VotingData** 누릅니다 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-184">In hello **New Service Fabric Service** dialog, choose **Stateful ASP.NET Core**, and name hello service **VotingData** and press **OK**.</span></span>

    ![Visual Studio의 새 서비스 대화 상자](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    <span data-ttu-id="9cbce-186">서비스 프로젝트를 만들었으면 응용 프로그램에 두 개의 서비스가 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-186">Once your service project is created, you have two services in your application.</span></span> <span data-ttu-id="9cbce-187">Hello에 더 많은 서비스를 추가할 수 toobuild 응용 프로그램을 계속 하면서 동일한 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-187">As you continue toobuild your application, you can add more services in hello same way.</span></span> <span data-ttu-id="9cbce-188">각 서비스를 독립적으로 버전 지정 및 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-188">Each can be independently versioned and upgraded.</span></span>

3. <span data-ttu-id="9cbce-189">hello 다음 페이지는 ASP.NET Core 집합이 프로젝트 템플릿을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-189">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="9cbce-190">이 자습서에서는 **Web API**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-190">For this tutorial, choose **Web API**.</span></span>

    ![ASP.NET 프로젝트 형식 선택](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    <span data-ttu-id="9cbce-192">Visual Studio는 서비스 프로젝트를 만들고 솔루션 탐색기에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-192">Visual Studio creates a service project and displays them in Solution Explorer.</span></span>

    ![솔루션 탐색기](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-hello-votedatacontrollercs-file"></a><span data-ttu-id="9cbce-194">Hello VoteDataController.cs 파일 추가</span><span class="sxs-lookup"><span data-stu-id="9cbce-194">Add hello VoteDataController.cs file</span></span>

<span data-ttu-id="9cbce-195">Hello에 **VotingData** 마우스 오른쪽 단추로 클릭 hello 프로젝트 **컨트롤러** 폴더를 선택 합니다 **추가-새로 만들기 > 항목 클래스->**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-195">In hello **VotingData** project right-click on hello **Controllers** folder, then select **Add->New item->Class**.</span></span> <span data-ttu-id="9cbce-196">"VoteDataController.cs" hello 파일 이름을 지정 하 고 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-196">Name hello file "VoteDataController.cs" and click **Add**.</span></span> <span data-ttu-id="9cbce-197">Hello 파일 내용을 hello 다음으로 바꾸는 다음 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-197">Replace hello file contents with hello following, then save your changes.</span></span>

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


## <a name="connect-hello-services"></a><span data-ttu-id="9cbce-198">Hello 서비스 연결</span><span class="sxs-lookup"><span data-stu-id="9cbce-198">Connect hello services</span></span>
<span data-ttu-id="9cbce-199">다음이 단계에서는 hello 두 서비스를 연결 하 고 hello 프런트 엔드 웹 응용 프로그램을 가져오고 설정 투표 hello 백 엔드 서비스에서 정보를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-199">In this next step, we will connect hello two services and make hello front-end Web application get and set voting information from hello back-end service.</span></span>

<span data-ttu-id="9cbce-200">서비스 패브릭은 신뢰할 수 있는 서비스와 유연하게 통신할 수 있는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-200">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="9cbce-201">단일 응용 프로그램 내에는 TCP를 통해 액세스할 수 있는 서비스가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-201">Within a single application, you might have services that are accessible via TCP.</span></span> <span data-ttu-id="9cbce-202">HTTP REST API 및 다른 서비스를 통해 액세스할 수 있는 기타 서비스는 웹 소켓을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-202">Other services that might be accessible via an HTTP REST API and still other services could be accessible via web sockets.</span></span> <span data-ttu-id="9cbce-203">참조에 대 한 배경 사용할 수 있는 hello 옵션 및 hello 보완, [서비스와 통신](service-fabric-connect-and-communicate-with-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-203">For background on hello options available and hello tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

<span data-ttu-id="9cbce-204">이 자습서에서 [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-204">In this tutorial, we are using [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-hello-votescontrollercs-file"></a><span data-ttu-id="9cbce-205">Hello VotesController.cs 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="9cbce-205">Update hello VotesController.cs file</span></span>
<span data-ttu-id="9cbce-206">Hello에 **VotingWeb** 프로젝트, 열기 hello *Controllers/VotesController.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-206">In hello **VotingWeb** project, open hello *Controllers/VotesController.cs* file.</span></span>  <span data-ttu-id="9cbce-207">Hello 대체 `VotesController` hello 다음과 같이 정의 내용을 클래스 다음 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-207">Replace hello `VotesController` class definition contents with hello following, then save your changes.</span></span>

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

## <a name="walk-through-hello-voting-sample-application"></a><span data-ttu-id="9cbce-208">샘플 응용 프로그램 투표 hello 안내</span><span class="sxs-lookup"><span data-stu-id="9cbce-208">Walk through hello voting sample application</span></span>
<span data-ttu-id="9cbce-209">두 서비스의 응용 프로그램 투표 hello 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-209">hello voting application consists of two services:</span></span>
- <span data-ttu-id="9cbce-210">웹 프런트 엔드 서비스 (VotingWeb)-An ASP.NET Core 웹 hello 웹 페이지를 사용 되는 프런트 엔드 서비스 및 노출 웹 Api toocommunicate hello 백 엔드 서비스와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-210">Web front-end service (VotingWeb)- An ASP.NET Core web front-end service, which serves hello web page and exposes web APIs toocommunicate with hello backend service.</span></span>
- <span data-ttu-id="9cbce-211">백 엔드 서비스 (VotingData)-노출 API toostore hello 투표를 신뢰할 수 있는 사전으로 인해 디스크에 저장 되는 ASP.NET Core 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-211">Back-end service (VotingData)- An ASP.NET Core web service, which exposes an API toostore hello vote results in a reliable dictionary persisted on disk.</span></span>

![응용 프로그램 다이어그램](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="9cbce-213">다음 hello 응용 프로그램 hello에 투표 이벤트가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-213">When you vote in hello application hello following events occur:</span></span>
1. <span data-ttu-id="9cbce-214">JavaScript은 hello 웹 프런트 엔드 서비스 hello 투표 요청 toohello web을 API HTTP PUT 요청으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-214">A JavaScript sends hello vote request toohello web API in hello web front-end service as an HTTP PUT request.</span></span>

2. <span data-ttu-id="9cbce-215">hello 웹 프런트 엔드 서비스 프록시 toolocate를 사용 하 여 하 고는 HTTP PUT 요청 toohello 백 엔드 서비스에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-215">hello web front-end service uses a proxy toolocate and forward an HTTP PUT request toohello back-end service.</span></span>

3. <span data-ttu-id="9cbce-216">hello 백 엔드 서비스는 hello 들어오는 요청을 사용 하 고 저장소 hello hello 클러스터 내에서 복제 된 toomultiple 노드를 가져오고 디스크에 저장 하는 신뢰할 수 있는 사전에서 결과 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-216">hello back-end service takes hello incoming request, and stores hello updated result in a reliable dictionary, which gets replicated toomultiple nodes within hello cluster and persisted on disk.</span></span> <span data-ttu-id="9cbce-217">모든 hello 응용 프로그램의 데이터는 데이터베이스가 필요 하므로 hello 클러스터에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-217">All hello application's data is stored in hello cluster, so no database is needed.</span></span>

## <a name="debug-in-visual-studio"></a><span data-ttu-id="9cbce-218">Visual Studio에서 디버그</span><span class="sxs-lookup"><span data-stu-id="9cbce-218">Debug in Visual Studio</span></span>
<span data-ttu-id="9cbce-219">Visual Studio에서 응용 프로그램을 디버깅할 때 로컬 Service Fabric 개발 클러스터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-219">When debugging application in Visual Studio, you are using a local Service Fabric development cluster.</span></span> <span data-ttu-id="9cbce-220">Hello 옵션 tooadjust 디버깅 환경을 tooyour 시나리오를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-220">You have hello option tooadjust your debugging experience tooyour scenario.</span></span> <span data-ttu-id="9cbce-221">이 응용 프로그램에서는 신뢰할 수 있는 사전을 사용하여 데이터를 백 엔드 서비스에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-221">In this application, we store data in our back-end service, using a reliable dictionary.</span></span> <span data-ttu-id="9cbce-222">Visual Studio hello 디버거를 중지 하는 경우 기본 당 hello 응용 프로그램을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-222">Visual Studio removes hello application per default when you stop hello debugger.</span></span> <span data-ttu-id="9cbce-223">Hello 백 엔드에 hello 데이터 hello 응용 프로그램을 제거 하면 서비스 tooalso 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-223">Removing hello application causes hello data in hello back-end service tooalso be removed.</span></span> <span data-ttu-id="9cbce-224">디버깅 세션 간에 toopersist hello 데이터를 hello 변경할 수 있습니다 **응용 프로그램 디버그 모드** hello 속성으로 **응답** Visual Studio에서 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="9cbce-224">toopersist hello data between debugging sessions, you can change hello **Application Debug Mode** as a property on hello **Voting** project in Visual Studio.</span></span>

<span data-ttu-id="9cbce-225">hello 코드에서는 다음 단계 완료 hello toolook에 어떤 상황이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-225">toolook at what happens in hello code, complete hello following steps:</span></span>
1. <span data-ttu-id="9cbce-226">열기 hello **VotesController.cs** hello 웹 API에에서 중단점을 설정 하 고 파일 **배치** 메서드 (47 선)-hello Visual Studio의 솔루션 탐색기에서에서 hello 파일을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-226">Open hello **VotesController.cs** file and set a breakpoint in hello web API's **Put** method (line 47) - You can search for hello file in hello Solution Explorer in Visual Studio.</span></span>

2. <span data-ttu-id="9cbce-227">열기 hello **VoteDataController.cs** 파일을 웹 API이 중단점을 설정할 **배치** 메서드 (라인 50).</span><span class="sxs-lookup"><span data-stu-id="9cbce-227">Open hello **VoteDataController.cs** file and set a breakpoint in this web API's **Put** method (line 50).</span></span>

3. <span data-ttu-id="9cbce-228">Toohello 브라우저 돌아가서 투표 옵션을 클릭 하거나 새 응답 옵션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-228">Go back toohello browser and click a voting option or add a new voting option.</span></span> <span data-ttu-id="9cbce-229">Hello hello 웹 프런트 엔드에서 api 컨트롤러의 첫 번째 중단점을 누르면 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-229">You hit hello first breakpoint in hello web front-end's api controller.</span></span>
    
    1. <span data-ttu-id="9cbce-230">이 hello 브라우저에서 JavaScript hello hello 프런트 엔드 서비스에 요청 toohello web API 컨트롤러를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-230">This is where hello JavaScript in hello browser sends a request toohello web API controller in hello front-end service.</span></span>
    
    ![투표 프런트 엔드 서비스 추가](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. <span data-ttu-id="9cbce-232">백 엔드 서비스에 대 한 hello URL toohello ReverseProxy 생성 먼저 **(1)**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-232">First we construct hello URL toohello ReverseProxy for our back-end service **(1)**.</span></span>
    3. <span data-ttu-id="9cbce-233">म ध hello HTTP PUT 요청 toohello ReverseProxy 다음 **(2)**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-233">Then we send hello HTTP PUT Request toohello ReverseProxy **(2)**.</span></span>
    4. <span data-ttu-id="9cbce-234">마지막으로 hello 반환 hello 응답 hello 백 엔드 서비스 toohello 클라이언트로부터 **(3)**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-234">Finally hello we return hello response from hello back-end service toohello client **(3)**.</span></span>

4. <span data-ttu-id="9cbce-235">키를 눌러 **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="9cbce-235">Press **F5** toocontinue</span></span>
    1. <span data-ttu-id="9cbce-236">현재 위치는 hello 중단점의 hello 백 엔드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-236">You are now at hello break point in hello back-end service.</span></span>
    
    ![투표 백 엔드 서비스 추가](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. <span data-ttu-id="9cbce-238">Hello hello 메서드 첫 번째 줄에 **(1)** hello 사용 하 여 `StateManager` tooget 라는 신뢰할 수 있는 사전 추가 또는 `counts`합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-238">In hello first line in hello method **(1)** we are using hello `StateManager` tooget or add a reliable dictionary called `counts`.</span></span>
    3. <span data-ttu-id="9cbce-239">신뢰할 수 있는 사전에 있는 값과의 모든 상호 작용에는 트랜잭션이 필요하며 using 문**(2)**으로 트랜잭션이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-239">All interactions with values in a reliable dictionary require a transaction, this using statement **(2)** creates that transaction.</span></span>
    4. <span data-ttu-id="9cbce-240">Hello 트랜잭션에서 다음 업데이트 옵션 투표 hello에 대 한 hello 관련 키의 hello 값 및 커밋 작업 hello **(3)**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-240">In hello transaction, we then update hello value of hello relevant key for hello voting option and commits hello operation **(3)**.</span></span> <span data-ttu-id="9cbce-241">Hello 커밋하면 메서드가 반환 hello 데이터 hello 사전에서 업데이트 되 고 tooother hello 클러스터 노드를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-241">Once hello commit method returns, hello data is updated in hello dictionary and replicated tooother nodes in hello cluster.</span></span> <span data-ttu-id="9cbce-242">이제 hello 데이터는 hello 클러스터에 안전 하 게 저장 하 고 hello 백 엔드 서비스 데 계속 사용할 수 있는 hello 데이터 tooother 노드를 장애 조치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-242">hello data is now safely stored in hello cluster, and hello back-end service can fail over tooother nodes, still having hello data available.</span></span>
5. <span data-ttu-id="9cbce-243">키를 눌러 **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="9cbce-243">Press **F5** toocontinue</span></span>

<span data-ttu-id="9cbce-244">세션 키를 눌러 디버깅 toostop hello **Shift + f 5**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbce-244">toostop hello debugging session, press **Shift+F5**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9cbce-245">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9cbce-245">Next steps</span></span>
<span data-ttu-id="9cbce-246">Hello 자습서의이 단계에서는 알아보았습니다 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="9cbce-246">In this part of hello tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9cbce-247">ASP.NET Core Web API 서비스를 상태 저장 Reliable Service로 만들기</span><span class="sxs-lookup"><span data-stu-id="9cbce-247">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="9cbce-248">ASP.NET Core Web 응용 프로그램 서비스를 상태 비저장 웹 서비스로 만들기</span><span class="sxs-lookup"><span data-stu-id="9cbce-248">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="9cbce-249">Hello 역방향 프록시 toocommunicate hello 상태 저장 서비스와 함께 사용</span><span class="sxs-lookup"><span data-stu-id="9cbce-249">Use hello reverse proxy toocommunicate with hello stateful service</span></span>

<span data-ttu-id="9cbce-250">고급 toohello 다음 자습서:</span><span class="sxs-lookup"><span data-stu-id="9cbce-250">Advance toohello next tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="9cbce-251">Hello 응용 프로그램 tooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="9cbce-251">Deploy hello application tooAzure</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
