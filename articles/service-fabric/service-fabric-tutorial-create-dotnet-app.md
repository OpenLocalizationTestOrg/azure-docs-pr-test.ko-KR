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
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a>ASP.NET Core Web API 프런트 엔드 서비스 및 상태 저장 백 엔드 서비스로 응용 프로그램 만들기 및 배포
이 자습서는 시리즈의 1부입니다.  배웁니다 어떤 toocreate ASP.NET Core 웹 API 앞으로 Azure 서비스 패브릭 응용 프로그램을 시작 하 고 상태 저장 서비스의 백 엔드 toostore 데이터. 완료 되 면 hello 클러스터에서 상태 저장 백 엔드 서비스의 응답 결과 저장 하는 프런트 엔드는 ASP.NET Core 웹 응용 프로그램을 응답 해야 합니다. Toomanually 않으려면 hello 투표 응용 프로그램 만들기, 할 수 있습니다 [hello 소스 코드 다운로드](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) hello에 대 한 응용 프로그램을 완료 하 고 너무 건너 뛸[hello 샘플 응용 프로그램 투표 하는 과정을 안내](#walkthrough_anchor)합니다.

![응용 프로그램 다이어그램](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

Hello 시리즈의 1 부에서는 학습 하는 방법:

> [!div class="checklist"]
> * ASP.NET Core Web API 서비스를 상태 저장 Reliable Service로 만들기
> * ASP.NET Core Web 응용 프로그램 서비스를 상태 비저장 웹 서비스로 만들기
> * Hello 역방향 프록시 toocommunicate hello 상태 저장 서비스와 함께 사용

이 자습서 시리즈에서는 다음 방법에 대해 알아봅니다.
> [!div class="checklist"]
> * .NET Service Fabric 응용 프로그램 빌드
> * [Hello 응용 프로그램 tooa 원격 클러스터 배포](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * [Visual Studio Team Services를 사용하여 CI/CD 구성](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a>필수 조건
이 자습서를 시작하기 전에:
- Azure 구독이 없는 경우 [평가판 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만듭니다.
- [Visual Studio 2017 설치](https://www.visualstudio.com/) hello를 설치 하 고 **Azure 개발** 및 **ASP.NET 및 웹 개발** 작업 합니다.
- [Hello 서비스 패브릭 SDK 설치](service-fabric-get-started.md)

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a>ASP.NET Web API 서비스를 신뢰할 수 있는 서비스로 만들기
Hello 웹을 프런트 엔드 ASP.NET Core를 사용 하 여 응용 프로그램 투표 hello를 먼저 만듭니다. ASP.NET Core는 플랫폼 간 경량 웹 개발 프레임 워크 toocreate 최신 웹 UI를 사용할 수 있으며 웹 Api입니다. 서비스 패브릭 ASP.NET Core 통합 하는 방법을 완전히 이해 tooget 권장 hello를 읽는 [서비스 패브릭 신뢰할 수 있는 서비스에서 ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) 문서. 지금은이 자습서에 신속 하 게 시작 tooget을 따를 수 있습니다. ASP.NET Core에 대 한 자세한 toolearn 참조 hello [ASP.NET Core 설명서](https://docs.microsoft.com/aspnet/core/)합니다.

> [!NOTE]
> 이 자습서는 hello 기반 [ASP.NET Core l Visual Studio 2017 용 도구](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc)합니다. Visual Studio 2015 용 hello.NET Core 도구는 더 이상 업데이트 중입니다.

1. **관리자** 권한으로 Visual Studio를 시작합니다.

2. **파일**->**새로 만들기**->**프로젝트**로 프로젝트를 만듭니다.

3. Hello에 **새 프로젝트** 대화 상자에서 선택 **클라우드 > 서비스 패브릭 응용 프로그램**합니다.

4. Hello 응용 프로그램 이름을 **응답** 누릅니다 **확인**합니다.

   ![Visual Studio의 새 프로젝트 대화 상자](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. Hello에 **새 서비스 패브릭 서비스** 페이지에서 선택 **상태 비저장 ASP.NET Core**, 서비스 이름 지정 및 **VotingWeb**합니다.
   
   ![Hello 새 서비스 대화 상자에서 ASP.NET 웹 서비스를 선택합니다.](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. hello 다음 페이지는 ASP.NET Core 집합이 프로젝트 템플릿을 제공합니다. 이 자습서에서는 **웹 응용 프로그램**을 선택합니다. 
   
   ![ASP.NET 프로젝트 형식 선택](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   Visual Studio는 응용 프로그램 및 서비스 프로젝트를 만들고 솔루션 탐색기에 표시합니다.

   ![ASP.NET core Web API 서비스를 사용하여 응용 프로그램 만들기를 수행하는 솔루션 탐색기]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-toohello-votingweb-service"></a>AngularJS toohello VotingWeb 서비스 추가
추가 [AngularJS](http://angularjs.org/) 기본 제공 hello를 사용 하 여 tooyour 서비스 [지원 Bower](/aspnet/core/client-side/bower)합니다. *bower.json*을 열고 각도 및 각도 부트스트랩에 항목을 추가한 후 변경 내용을 저장합니다.

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
Hello 저장 시 *bower.json* 파일을 각 프로젝트에 설치 되어 *wwwroot/lib* 폴더입니다. 또한 hello 내 나열 *종속성/Bower* 폴더입니다.

### <a name="update-hello-sitejs-file"></a>Hello site.js 파일 업데이트
열기 hello *wwwroot/js/site.js* 파일입니다.  해당 내용을 hello hello 홈 보기에서 사용 하는 JavaScript로 바꿉니다.

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

### <a name="update-hello-indexcshtml-file"></a>Hello Index.cshtml 파일 업데이트
열기 hello *Views/Home/Index.cshtml* 파일, hello 보기 특정 toohello 홈 컨트롤러입니다.  해당 내용을 hello 다음 코드로 바꿉니다 다음 변경 내용을 저장 합니다.

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

### <a name="update-hello-layoutcshtml-file"></a>Hello _Layout.cshtml 파일 업데이트
열기 hello *Views/Shared/_Layout.cshtml* 파일, hello ASP.NET 응용 프로그램에 대 한 hello 기본 레이아웃 합니다.  해당 내용을 hello 다음 코드로 바꿉니다 다음 변경 내용을 저장 합니다.

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

### <a name="update-hello-votingwebcs-file"></a>Hello VotingWeb.cs 파일 업데이트
열기 hello *VotingWeb.cs* 파일 hello WebListener 웹 서버를 사용 하 여 hello 상태 비저장 서비스 내부 hello ASP.NET Core 웹 호스트를 만듭니다.  Hello 추가 `using System.Net.Http;` hello 파일의 지시문 toohello 맨 위로 이동 합니다.  Hello 대체 `CreateServiceInstanceListeners()` hello 다음과 같이 작동 한 다음 변경 내용을 저장 합니다.

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

### <a name="add-hello-votescontrollercs-file"></a>Hello VotesController.cs 파일 추가
투표 작업을 정의하는 컨트롤러를 추가합니다. Hello를 마우스 오른쪽 단추로 클릭 **컨트롤러** 폴더를 선택 합니다 **추가-새로 만들기 > 항목 클래스->**합니다.  "VotesController.cs" hello 파일 이름을 지정 하 고 클릭 **추가**합니다.  Hello 파일 내용을 hello 다음으로 바꾸는 다음 변경 내용을 저장 합니다.  뒷부분에 나오는 [업데이트 hello VotesController.cs 파일](#updatevotecontroller_anchor),이 파일 수정된 tooread 되며 hello 백 엔드 서비스에서 응답 데이터를 기록 합니다.  지금은 hello 컨트롤러 데이터 toohello 뷰의 정적 문자열을 반환합니다.

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



### <a name="deploy-and-run-hello-application-locally"></a>배포 하 고 hello 응용 프로그램을 로컬로 실행
이제 계속 진행 하 고 hello 응용 프로그램을 실행할 수 있습니다. 키를 눌러 Visual Studio에서 `F5` toodeploy hello 응용 프로그램을 디버깅 합니다. **관리자** 권한으로 Visual Studio를 이전에 열지 않은 경우 `F5` 키가 실패합니다.

> [!NOTE]
> hello 처음으로 실행 하 고 hello 응용 프로그램 배포를 로컬로 Visual Studio 디버깅에 대 한 로컬 클러스터를 만듭니다.  클러스터 생성에는 다소 시간이 걸릴 수 있습니다. hello 클러스터 만들기 상태 hello Visual Studio 출력 창에 표시 됩니다.

이 시점에서 웹앱은 다음과 같이 표시됩니다.

![ASP.NET Core 프런트 엔드](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

hello 응용 프로그램을 디버깅 toostop tooVisual Studio 누릅니다 돌아가서 **Shift + f 5**합니다.

## <a name="add-a-stateful-back-end-service-tooyour-application"></a>상태 저장 서비스의 백 엔드 tooyour 응용 프로그램 추가
응용 프로그램에서 실행 되는 ASP.NET Web API 서비스를 만들었으므로 이제 해당 응용 프로그램의 상태 저장 서비스의 신뢰할 수 있는 toostore 일부 데이터를 추가 해 보겠습니다.

서비스 패브릭 tooconsistently 있으며 안정적으로 신뢰할 수 있는 컬렉션을 사용 하 여 내부 서비스에 직접 데이터를 저장 합니다. 신뢰할 수 있는 컬렉션은 컬렉션 C# 사용 경험이 친숙 한 tooanyone 있는 항상 사용 가능 하 고 신뢰할 수 있는 컬렉션 클래스의 집합입니다.

이 자습서에서는 신뢰할 수 있는 컬렉션에 카운터 값을 저장하는 서비스를 만듭니다.

1. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 **서비스** 내 응용 프로그램 프로젝트 hello 및 선택 **추가 > 새 서비스 패브릭 서비스**합니다.
   
    ![새 서비스 tooan 기존 응용 프로그램 추가](./media/service-fabric-tutorial-create-dotnet-app/vs-add-new-service.png)

2. Hello에 **새 서비스 패브릭 서비스** 대화 상자에서 선택 **Stateful ASP.NET Core**, 및 이름 hello 서비스 **VotingData** 누릅니다 **확인**합니다.

    ![Visual Studio의 새 서비스 대화 상자](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    서비스 프로젝트를 만들었으면 응용 프로그램에 두 개의 서비스가 있을 것입니다. Hello에 더 많은 서비스를 추가할 수 toobuild 응용 프로그램을 계속 하면서 동일한 방식으로 합니다. 각 서비스를 독립적으로 버전 지정 및 업그레이드할 수 있습니다.

3. hello 다음 페이지는 ASP.NET Core 집합이 프로젝트 템플릿을 제공합니다. 이 자습서에서는 **Web API**를 선택합니다.

    ![ASP.NET 프로젝트 형식 선택](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    Visual Studio는 서비스 프로젝트를 만들고 솔루션 탐색기에 표시합니다.

    ![솔루션 탐색기](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-hello-votedatacontrollercs-file"></a>Hello VoteDataController.cs 파일 추가

Hello에 **VotingData** 마우스 오른쪽 단추로 클릭 hello 프로젝트 **컨트롤러** 폴더를 선택 합니다 **추가-새로 만들기 > 항목 클래스->**합니다. "VoteDataController.cs" hello 파일 이름을 지정 하 고 클릭 **추가**합니다. Hello 파일 내용을 hello 다음으로 바꾸는 다음 변경 내용을 저장 합니다.

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


## <a name="connect-hello-services"></a>Hello 서비스 연결
다음이 단계에서는 hello 두 서비스를 연결 하 고 hello 프런트 엔드 웹 응용 프로그램을 가져오고 설정 투표 hello 백 엔드 서비스에서 정보를 확인 합니다.

서비스 패브릭은 신뢰할 수 있는 서비스와 유연하게 통신할 수 있는 방법을 제공합니다. 단일 응용 프로그램 내에는 TCP를 통해 액세스할 수 있는 서비스가 있을 수 있습니다. HTTP REST API 및 다른 서비스를 통해 액세스할 수 있는 기타 서비스는 웹 소켓을 통해 액세스할 수 있습니다. 참조에 대 한 배경 사용할 수 있는 hello 옵션 및 hello 보완, [서비스와 통신](service-fabric-connect-and-communicate-with-services.md)합니다.

이 자습서에서 [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md)를 사용합니다.

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-hello-votescontrollercs-file"></a>Hello VotesController.cs 파일 업데이트
Hello에 **VotingWeb** 프로젝트, 열기 hello *Controllers/VotesController.cs* 파일입니다.  Hello 대체 `VotesController` hello 다음과 같이 정의 내용을 클래스 다음 변경 내용을 저장 합니다.

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

## <a name="walk-through-hello-voting-sample-application"></a>샘플 응용 프로그램 투표 hello 안내
두 서비스의 응용 프로그램 투표 hello 구성 됩니다.
- 웹 프런트 엔드 서비스 (VotingWeb)-An ASP.NET Core 웹 hello 웹 페이지를 사용 되는 프런트 엔드 서비스 및 노출 웹 Api toocommunicate hello 백 엔드 서비스와 함께 합니다.
- 백 엔드 서비스 (VotingData)-노출 API toostore hello 투표를 신뢰할 수 있는 사전으로 인해 디스크에 저장 되는 ASP.NET Core 웹 서비스입니다.

![응용 프로그램 다이어그램](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

다음 hello 응용 프로그램 hello에 투표 이벤트가 발생 합니다.
1. JavaScript은 hello 웹 프런트 엔드 서비스 hello 투표 요청 toohello web을 API HTTP PUT 요청으로 보냅니다.

2. hello 웹 프런트 엔드 서비스 프록시 toolocate를 사용 하 여 하 고는 HTTP PUT 요청 toohello 백 엔드 서비스에 전달 합니다.

3. hello 백 엔드 서비스는 hello 들어오는 요청을 사용 하 고 저장소 hello hello 클러스터 내에서 복제 된 toomultiple 노드를 가져오고 디스크에 저장 하는 신뢰할 수 있는 사전에서 결과 업데이트 합니다. 모든 hello 응용 프로그램의 데이터는 데이터베이스가 필요 하므로 hello 클러스터에 저장 됩니다.

## <a name="debug-in-visual-studio"></a>Visual Studio에서 디버그
Visual Studio에서 응용 프로그램을 디버깅할 때 로컬 Service Fabric 개발 클러스터를 사용합니다. Hello 옵션 tooadjust 디버깅 환경을 tooyour 시나리오를 해야합니다. 이 응용 프로그램에서는 신뢰할 수 있는 사전을 사용하여 데이터를 백 엔드 서비스에 저장합니다. Visual Studio hello 디버거를 중지 하는 경우 기본 당 hello 응용 프로그램을 제거 합니다. Hello 백 엔드에 hello 데이터 hello 응용 프로그램을 제거 하면 서비스 tooalso 제거할 수 있습니다. 디버깅 세션 간에 toopersist hello 데이터를 hello 변경할 수 있습니다 **응용 프로그램 디버그 모드** hello 속성으로 **응답** Visual Studio에서 프로젝트.

hello 코드에서는 다음 단계 완료 hello toolook에 어떤 상황이 발생 합니다.
1. 열기 hello **VotesController.cs** hello 웹 API에에서 중단점을 설정 하 고 파일 **배치** 메서드 (47 선)-hello Visual Studio의 솔루션 탐색기에서에서 hello 파일을 검색할 수 있습니다.

2. 열기 hello **VoteDataController.cs** 파일을 웹 API이 중단점을 설정할 **배치** 메서드 (라인 50).

3. Toohello 브라우저 돌아가서 투표 옵션을 클릭 하거나 새 응답 옵션을 추가 합니다. Hello hello 웹 프런트 엔드에서 api 컨트롤러의 첫 번째 중단점을 누르면 있습니다.
    
    1. 이 hello 브라우저에서 JavaScript hello hello 프런트 엔드 서비스에 요청 toohello web API 컨트롤러를 보냅니다.
    
    ![투표 프런트 엔드 서비스 추가](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. 백 엔드 서비스에 대 한 hello URL toohello ReverseProxy 생성 먼저 **(1)**합니다.
    3. म ध hello HTTP PUT 요청 toohello ReverseProxy 다음 **(2)**합니다.
    4. 마지막으로 hello 반환 hello 응답 hello 백 엔드 서비스 toohello 클라이언트로부터 **(3)**합니다.

4. 키를 눌러 **F5** toocontinue
    1. 현재 위치는 hello 중단점의 hello 백 엔드 서비스입니다.
    
    ![투표 백 엔드 서비스 추가](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. Hello hello 메서드 첫 번째 줄에 **(1)** hello 사용 하 여 `StateManager` tooget 라는 신뢰할 수 있는 사전 추가 또는 `counts`합니다.
    3. 신뢰할 수 있는 사전에 있는 값과의 모든 상호 작용에는 트랜잭션이 필요하며 using 문**(2)**으로 트랜잭션이 만들어집니다.
    4. Hello 트랜잭션에서 다음 업데이트 옵션 투표 hello에 대 한 hello 관련 키의 hello 값 및 커밋 작업 hello **(3)**합니다. Hello 커밋하면 메서드가 반환 hello 데이터 hello 사전에서 업데이트 되 고 tooother hello 클러스터 노드를 복제 합니다. 이제 hello 데이터는 hello 클러스터에 안전 하 게 저장 하 고 hello 백 엔드 서비스 데 계속 사용할 수 있는 hello 데이터 tooother 노드를 장애 조치할 수 있습니다.
5. 키를 눌러 **F5** toocontinue

세션 키를 눌러 디버깅 toostop hello **Shift + f 5**합니다.


## <a name="next-steps"></a>다음 단계
Hello 자습서의이 단계에서는 알아보았습니다 하는 방법:

> [!div class="checklist"]
> * ASP.NET Core Web API 서비스를 상태 저장 Reliable Service로 만들기
> * ASP.NET Core Web 응용 프로그램 서비스를 상태 비저장 웹 서비스로 만들기
> * Hello 역방향 프록시 toocommunicate hello 상태 저장 서비스와 함께 사용

고급 toohello 다음 자습서:
> [!div class="nextstepaction"]
> [Hello 응용 프로그램 tooAzure 배포](service-fabric-tutorial-deploy-app-to-party-cluster.md)
