---
title: "앱 서비스에서 지 원하는 aaaCORS | Microsoft Docs"
description: "Azure Azure 앱 서비스의 CORS toouse를 지 원하는 방법에 대해 알아봅니다."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 4f980a97-b9f5-4d1d-87ab-82b60bb96e1c
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/27/2016
ms.author: alkarche
ms.openlocfilehash: c229378b75840bc0f7b2eefc3df3031233f9b494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-api-app-from-javascript-using-cors"></a><span data-ttu-id="88983-103">CORS를 사용하여 JavaScript에서 API 앱 사용</span><span class="sxs-lookup"><span data-stu-id="88983-103">Consume an API app from JavaScript using CORS</span></span>
<span data-ttu-id="88983-104">앱 서비스 제공에 대 한 기본 제공 지원 [교차 원본 자원 공유 (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), tooAPIs API 앱에서 호스트 되는 호출 JavaScript 클라이언트 toomake 도메인 간 할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-104">App Service offers built-in support for [Cross Origin Resource Sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), which enables JavaScript clients toomake cross-domain calls tooAPIs that are hosted in API apps.</span></span> <span data-ttu-id="88983-105">앱 서비스 API에는 모든 코드를 작성 하지 않고도 CORS 액세스 tooyour API를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88983-105">App Service lets you configure CORS access tooyour API without writing any code in your API.</span></span>

<span data-ttu-id="88983-106">이 문서에는 다음과 같은 두 섹션이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88983-106">This article contains two sections:</span></span>

* <span data-ttu-id="88983-107">hello [어떻게 tooconfigure CORS](#corsconfig) 섹션에서는 일반적인 방법에 설명 모든 API 앱, 웹 응용 프로그램 또는 모바일 앱에 대 한 CORS tooconfigure 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-107">hello [How tooconfigure CORS](#corsconfig) section explains in general how tooconfigure CORS for any API app, web app, or mobile app.</span></span> <span data-ttu-id="88983-108">응용 프로그램 서비스,.NET, Node.js, Java 등에서 지원 되는 tooall 프레임 워크 똑같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-108">It applies equally tooall frameworks that are supported by App Service, including .NET, Node.js, and Java.</span></span> 
* <span data-ttu-id="88983-109">Hello로 시작 [hello.NET 시작 하기 자습서를 계속](#tutorialstart) 섹션 hello 문서는 CORS 지원에서 수행한 작업에 구축 하 여 보여 주는 자습서 [hello 첫 번째 API 앱 시작된 자습서 ](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="88983-109">Starting with hello [Continuing hello .NET getting-started tutorials](#tutorialstart) section, hello article is a tutorial that demonstrates CORS support by building on what you did in [hello first API Apps getting started tutorial](app-service-api-dotnet-get-started.md).</span></span> 

## <span data-ttu-id="88983-110"><a id="corsconfig"></a>어떻게 tooconfigure Azure 앱 서비스의 CORS</span><span class="sxs-lookup"><span data-stu-id="88983-110"><a id="corsconfig"></a> How tooconfigure CORS in Azure App Service</span></span>
<span data-ttu-id="88983-111">Hello Azure 포털에서에서 또는 사용 하 여 CORS를 구성할 수 있습니다 [Azure 리소스 관리자](../azure-resource-manager/resource-group-overview.md) 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="88983-111">You can configure CORS in hello Azure portal or by using [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) tools.</span></span>

#### <a name="configure-cors-in-hello-azure-portal"></a><span data-ttu-id="88983-112">Hello Azure 포털에서에서 CORS를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-112">Configure CORS in hello Azure portal</span></span>
1. <span data-ttu-id="88983-113">브라우저에서 toohello 이동 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-113">In a browser go toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="88983-114">클릭 **응용 프로그램 서비스**, 다음 API 앱의 hello 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88983-114">Click **App Services**, and then click hello name of your API app.</span></span>
   
    ![포털에서 API 앱 선택](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="88983-116">Hello에 **설정** hello toohello 오른쪽에 열리는 블레이드 **API 앱** 블레이드, 찾기 hello **API** 섹션을 선택한 다음 클릭 **CORS**합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-116">In hello **Settings** blade that opens toohello right of hello **API app** blade, find hello **API** section, and then click **CORS**.</span></span>
   
   ![설정 블레이드에서 CORS 선택](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="88983-118">Hello 텍스트 상자에 hello tooallow JavaScript 호출 toocome에서 원하는 Url 또는 URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-118">In hello text box enter hello URL or URLs that you want tooallow JavaScript calls toocome from.</span></span>

    <span data-ttu-id="88983-119">예를 들어 todolistangular 명명 된 JavaScript 응용 프로그램 tooa 웹 앱을 배포한 경우 "https://todolistangular.azurewebsites.net"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-119">For example, if you deployed your JavaScript application tooa web app named todolistangular, enter "https://todolistangular.azurewebsites.net".</span></span> <span data-ttu-id="88983-120">대신 모든 원본 도메인이 허용 되는 별표 (*) toospecify를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88983-120">As an alternative, you can enter an asterisk (*) toospecify that all origin domains are accepted.</span></span>


1. <span data-ttu-id="88983-121">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-121">Click **Save**.</span></span>
   
   ![저장을 클릭합니다.](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="88983-123">클릭 한 후 **저장**, hello API 앱에는 JavaScript 수락할 호출 hello에서 Url을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-123">After you click **Save**, hello API app will accept JavaScript calls from hello specified URLs.</span></span>

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a><span data-ttu-id="88983-124">Azure 리소스 관리자 도구를 사용하여 CORS 구성</span><span class="sxs-lookup"><span data-stu-id="88983-124">Configure CORS by using Azure Resource Manager tools</span></span>
<span data-ttu-id="88983-125">사용 하 여 API 앱에 대 한 CORS를 구성할 수도 있습니다 [Azure 리소스 관리자 템플릿을](../azure-resource-manager/resource-group-authoring-templates.md) 와 같은 명령줄 도구에서 [Azure PowerShell](/powershell/azureps-cmdlets-docs) 및 hello [Azure CLI](../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-125">You can also configure CORS for an API app by using [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) in command line tools such as [Azure PowerShell](/powershell/azureps-cmdlets-docs) and hello [Azure CLI](../cli-install-nodejs.md).</span></span> 

<span data-ttu-id="88983-126">Hello CORS 속성을 설정 하는 Azure 리소스 관리자 템플릿의 예제를 열고 hello [이 자습서에서는 샘플 응용 프로그램에 대 한 hello 리포지토리에 azuredeploy.json 파일](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-126">For an example of an Azure Resource Manager template that sets hello CORS property, open hello [azuredeploy.json file in hello repository for this tutorial's sample application](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span></span> <span data-ttu-id="88983-127">다음 예제는 hello 같은 hello 템플릿의 hello 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="88983-127">Find hello section of hello template that looks like hello following example:</span></span>

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <span data-ttu-id="88983-128"><a id="tutorialstart"></a>Hello.NET-시작 자습서를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-128"><a id="tutorialstart"></a> Continuing hello .NET getting-started tutorial</span></span>
<span data-ttu-id="88983-129">Hello Node.js 또는 Java 시작 시리즈 API 앱에 대 한를 따르는 경우 완료 된 hello 시작된 시리즈 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-129">If you are following hello Node.js or Java getting-started series for API apps, you have completed hello getting started series.</span></span> <span data-ttu-id="88983-130">Toohello 건너뛸 [다음 단계](#next-steps) 추가 API 앱에 대 한 학습을 위한 toofind 제안을 섹션.</span><span class="sxs-lookup"><span data-stu-id="88983-130">Skip toohello [Next steps](#next-steps) section toofind suggestions for further learning about API Apps.</span></span>

<span data-ttu-id="88983-131">hello이 문서의 나머지 부분에서는 연속 된 hello.NET 시작 시리즈 및 성공적으로 완료 했다고 가정 [hello 첫 번째 자습서](app-service-api-dotnet-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-131">hello remainder of this article is a continuation of hello .NET getting-started series and assumes that you successfully completed [hello first tutorial](app-service-api-dotnet-get-started.md).</span></span>

## <a name="deploy-hello-todolistangular-project-tooa-new-web-app"></a><span data-ttu-id="88983-132">Hello ToDoListAngular 프로젝트 tooa 새 웹 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="88983-132">Deploy hello ToDoListAngular project tooa new web app</span></span>
<span data-ttu-id="88983-133">[hello 첫 번째 자습서](app-service-api-dotnet-get-started.md), 중간 계층 API 앱 및 데이터 계층 API 앱을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-133">In [hello first tutorial](app-service-api-dotnet-get-started.md), you created a middle tier API app and a data tier API app.</span></span> <span data-ttu-id="88983-134">이 자습서는 단일 페이지 응용 프로그램 (SPA) 웹 응용 프로그램 호출 hello 중간 계층 API 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="88983-134">In this tutorial you create a single-page application (SPA) web app that calls hello middle tier API app.</span></span> <span data-ttu-id="88983-135">Hello SPA toowork hello 중간 계층 API 앱에서 CORS tooenable를 구조가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88983-135">For hello SPA toowork you have tooenable CORS on hello middle tier API app.</span></span> 

<span data-ttu-id="88983-136">Hello에 [ToDoList 샘플 응용 프로그램](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), hello ToDoListAngular 프로젝트는 hello 중간 계층 ToDoListAPI 웹 API 프로젝트를 호출 하는 간단한 AngularJS 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="88983-136">In hello [ToDoList sample application](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), hello ToDoListAngular project is a simple AngularJS client that calls hello middle tier ToDoListAPI Web API project.</span></span> <span data-ttu-id="88983-137">hello에서 JavaScript 코드를 hello *app/scripts/todoListSvc.js* hello AngularJS HTTP 공급자를 사용 하 여 hello API를 호출 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="88983-137">hello JavaScript code in hello *app/scripts/todoListSvc.js* file calls hello API by using hello AngularJS HTTP provider.</span></span> 

        angular.module('todoApp')
        .factory('todoListSvc', ['$http', function ($http) {

            $http.defaults.useXDomain = true;
            delete $http.defaults.headers.common['X-Requested-With']; 

            return {
                getItems : function(){
                    return $http.get(apiEndpoint + '/api/TodoList');
                },

                /* Get by ID, Put, and Delete methods not shown */

                postItem : function(item){
                    return $http.post(apiEndpoint + '/api/TodoList', item);
                }
            };
        }]);

### <a name="create-a-new-web-app-for-hello-todolistangular-project"></a><span data-ttu-id="88983-138">Hello ToDoListAngular 프로젝트에 대 한 새 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="88983-138">Create a new web app for hello ToDoListAngular project</span></span>
<span data-ttu-id="88983-139">hello 프로시저 toocreate 새 앱 서비스 웹 앱 및 프로젝트 배포 tooit는 언급 했 듯이 대 한 유사한 toowhat [만들고 hello이이 시리즈의 첫 번째 자습서에서 API 앱을 배포](app-service-api-dotnet-get-started.md#createapiapp)합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-139">hello procedure toocreate a new App Service web app and deploy a project tooit is similar toowhat you saw for [creating and deploying an API app in hello first tutorial in this series](app-service-api-dotnet-get-started.md#createapiapp).</span></span> <span data-ttu-id="88983-140">hello 차이점은 해당 hello 앱 형식에만 **웹 앱** 대신 **API 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-140">hello only difference is that hello app type is **Web App** instead of **API App**.</span></span>  <span data-ttu-id="88983-141">Hello 대화의 스크린 샷을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="88983-141">For screen shots of hello dialogs, see</span></span> 

1. <span data-ttu-id="88983-142">**솔루션 탐색기**hello ToDoListAngular 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-142">In **Solution Explorer**, right-click hello ToDoListAngular project, and then click **Publish**.</span></span>
2. <span data-ttu-id="88983-143">Hello에 **프로필** hello 탭 **웹 게시** 마법사를 클릭 하 여 **Microsoft Azure 앱 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-143">In hello **Profile** tab of hello **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="88983-144">Hello에 **앱 서비스** 대화 상자를 클릭 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-144">In hello **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="88983-145">Hello에 **호스팅** hello 탭 **응용 프로그램 서비스 만들기** 대화 상자에 입력 한 **웹 앱 이름은** hello에 고유 *azurewebsites.net* 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="88983-145">In hello **Hosting** tab of hello **Create App Service** dialog box, enter a **Web App Name** that is unique in hello *azurewebsites.net* domain.</span></span> 
5. <span data-ttu-id="88983-146">Azure hello 선택 **구독** toowork와 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-146">Choose hello Azure **Subscription** you want toowork with.</span></span>
6. <span data-ttu-id="88983-147">Hello에 **리소스 그룹** 드롭 다운 목록에서 선택 hello 앞에서 만든 동일한 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="88983-147">In hello **Resource Group** drop-down list, choose hello same resource group you created earlier.</span></span>
7. <span data-ttu-id="88983-148">Hello에 **앱 서비스 계획** 드롭 다운 목록에서 선택 hello 앞에서 만든 동일한 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-148">In hello **App Service Plan** drop-down list, choose hello same plan you created earlier.</span></span> 
8. <span data-ttu-id="88983-149">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-149">Click **Create**.</span></span>
   
    <span data-ttu-id="88983-150">Visual Studio hello 웹 응용 프로그램, 게시 프로필을 만드는 만들고 표시 hello **연결** hello 단계의 **웹 게시** 마법사.</span><span class="sxs-lookup"><span data-stu-id="88983-150">Visual Studio creates hello web app, creates a publish profile for it, and displays hello **Connection** step of hello **Publish Web** wizard.</span></span>
   
    <span data-ttu-id="88983-151">**게시** 를 아직 클릭하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="88983-151">Don't click **Publish** yet.</span></span> <span data-ttu-id="88983-152">Hello 섹션 뒤, hello 새 웹 응용 프로그램 toocall hello 중간 계층 API 앱을 앱 서비스에서 실행 되 고 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-152">In hello following section, you configure hello new web app toocall hello middle tier API app that is running in App Service.</span></span> 

### <a name="set-hello-middle-tier-url-in-web-app-settings"></a><span data-ttu-id="88983-153">웹 앱 설정의 hello 중간 계층 URL 설정</span><span class="sxs-lookup"><span data-stu-id="88983-153">Set hello middle tier URL in web app settings</span></span>
1. <span data-ttu-id="88983-154">Toohello 이동 [Azure 포털](https://portal.azure.com/)를 이동한 후 toohello **웹 응용 프로그램** 블레이드 toohost hello TodoListAngular (프런트 엔드) 프로젝트를 만든 hello 웹 앱에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-154">Go toohello [Azure portal](https://portal.azure.com/), and then navigate toohello **Web App** blade for hello web app that you created toohost hello TodoListAngular (front end) project.</span></span>
2. <span data-ttu-id="88983-155">**설정 > 응용 프로그램 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-155">Click **Settings > Application Settings**.</span></span>
3. <span data-ttu-id="88983-156">Hello에 **앱 설정** 섹션에서 hello 다음 추가 키 / 값:</span><span class="sxs-lookup"><span data-stu-id="88983-156">In hello **App settings** section, add hello following key and value:</span></span>
   
   | <span data-ttu-id="88983-157">키</span><span class="sxs-lookup"><span data-stu-id="88983-157">Key</span></span> | <span data-ttu-id="88983-158">값</span><span class="sxs-lookup"><span data-stu-id="88983-158">Value</span></span> | <span data-ttu-id="88983-159">예</span><span class="sxs-lookup"><span data-stu-id="88983-159">Example</span></span> |
   | --- | --- | --- |
   | <span data-ttu-id="88983-160">toDoListAPIURL</span><span class="sxs-lookup"><span data-stu-id="88983-160">toDoListAPIURL</span></span> |<span data-ttu-id="88983-161">https://{중간 계층 API 앱 이름}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="88983-161">https://{your middle tier API app name}.azurewebsites.net</span></span> |<span data-ttu-id="88983-162">https://todolistapi0121.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="88983-162">https://todolistapi0121.azurewebsites.net</span></span> |
4. <span data-ttu-id="88983-163">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-163">Click **Save**.</span></span>
   
    <span data-ttu-id="88983-164">Azure의 hello 코드가 실행 되 면이 값 재정의 hello에 있는 hello localhost URL *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="88983-164">When hello code runs in Azure, this value overrides hello localhost URL that is in hello *Web.config* file.</span></span> 
   
    <span data-ttu-id="88983-165">값을 설정 하는 hello 가져오는 hello 코드는 *index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="88983-165">hello code that gets hello setting value is in *index.cshtml*:</span></span>
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    <span data-ttu-id="88983-166">코드 hello *todoListSvc.js* hello 설정을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="88983-166">hello code in *todoListSvc.js* uses hello setting:</span></span>
   
        return {
            getItems : function(){
                return $http.get(apiEndpoint + '/api/TodoList');
            },
            getItem : function(id){
                return $http.get(apiEndpoint + '/api/TodoList/' + id);
            },
            postItem : function(item){
                return $http.post(apiEndpoint + '/api/TodoList', item);
            },
            putItem : function(item){
                return $http.put(apiEndpoint + '/api/TodoList/', item);
            },
            deleteItem : function(id){
                return $http({
                    method: 'DELETE',
                    url: apiEndpoint + '/api/TodoList/' + id
                });
            }
        };

### <a name="deploy-hello-todolistangular-web-project-toohello-new-web-app"></a><span data-ttu-id="88983-167">Hello ToDoListAngular 웹 프로젝트 toohello 새 웹 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="88983-167">Deploy hello ToDoListAngular web project toohello new web app</span></span>
* <span data-ttu-id="88983-168">Hello에 Visual Studio에서 **연결** hello 단계의 **웹 게시** 마법사를 클릭 하 여 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-168">In Visual Studio, in hello **Connection** step of hello **Publish Web** wizard, click **Publish**.</span></span>
  
   <span data-ttu-id="88983-169">Visual Studio는 hello ToDoListAngular 프로젝트 toohello 새 웹 앱을 배포 하 고 브라우저 toohello hello 웹 앱의 URL을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="88983-169">Visual Studio deploys hello ToDoListAngular project toohello new web app and opens a browser toohello URL of hello web app.</span></span> 

### <a name="test-hello-application-without-cors-enabled"></a><span data-ttu-id="88983-170">CORS를 사용 하도록 설정 하지 않고 hello 응용 프로그램을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-170">Test hello application without CORS enabled</span></span>
1. <span data-ttu-id="88983-171">브라우저 개발자 도구에서에서 hello 콘솔 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="88983-171">In your browser Developer Tools, open hello Console window.</span></span>
2. <span data-ttu-id="88983-172">Hello AngularJS UI를 표시 하는 hello 브라우저 창에서 클릭 hello **tooDo 목록** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-172">In hello browser window that displays hello AngularJS UI, click hello **tooDo List** link.</span></span>
   
    <span data-ttu-id="88983-173">JavaScript 코드 hello toocall hello 중간 계층 API 앱 하지만 hello 프런트 엔드 끝 hello 다시 아닌 다른 도메인에서 실행 중인 hello 호출이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-173">hello JavaScript code tries toocall hello middle tier API app, but hello call fails because hello front end is running in a different domain than hello back end.</span></span> <span data-ttu-id="88983-174">hello 브라우저의 개발자 도구 콘솔 창에 크로스-원본 오류 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-174">hello browser's Developer Tools Console window shows a cross-origin error message.</span></span>
   
    ![교차 원본 오류 메시지](./media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-hello-middle-tier-api-app"></a><span data-ttu-id="88983-176">CORS hello 중간 계층 API 앱에 대 한 구성</span><span class="sxs-lookup"><span data-stu-id="88983-176">Configure CORS for hello middle tier API app</span></span>
<span data-ttu-id="88983-177">이 섹션에서는 hello 중간 계층 ToDoListAPI API 앱에 대 한 Azure의 hello CORS 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88983-177">In this section, you configure hello CORS setting in Azure for hello middle tier ToDoListAPI API app.</span></span> <span data-ttu-id="88983-178">이 설정을 hello 중간 계층 응용 프로그램 tooreceive JavaScript에서에서 API 호출 hello ToDoListAngular 프로젝트에 대해 만든 hello 웹 앱을 통해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88983-178">This setting will allow hello middle tier API app tooreceive JavaScript calls from hello web app that you created for hello ToDoListAngular project.</span></span>

1. <span data-ttu-id="88983-179">브라우저에서 toohello 이동 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-179">In a browser, go toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="88983-180">클릭 **응용 프로그램 서비스**, 다음 hello ToDoListAPI (중간 계층) API 앱을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-180">Click **App Services**, and then click hello ToDoListAPI (middle tier) API app.</span></span>
   
    ![포털에서 API 앱 선택](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="88983-182">Hello에 **설정** hello toohello 오른쪽에 열리는 블레이드 **API 앱** 블레이드, 찾기 hello **API** 섹션을 선택한 다음 클릭 **CORS**합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-182">In hello **Settings** blade that opens toohello right of hello **API app** blade, find hello **API** section, and then click **CORS**.</span></span>
   
   ![포털에서 CORS 선택](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="88983-184">Hello 텍스트 상자에 hello ToDoListAngular (프런트 엔드) 웹 앱에 대 한 hello URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-184">In hello text box, enter hello URL for hello ToDoListAngular (front end) web app.</span></span> <span data-ttu-id="88983-185">Todolistangular0121 라는 hello ToDoListAngular 프로젝트 tooa 웹 앱을 배포한 경우 예를 들어 hello URL에서 호출을 허용 `https://todolistangular0121.azurewebsites.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-185">For example, if you deployed hello ToDoListAngular project tooa web app named todolistangular0121, allow calls from hello URL `https://todolistangular0121.azurewebsites.net`.</span></span>
   
   <span data-ttu-id="88983-186">대신 모든 원본 도메인이 허용 되는 별표 (*) toospecify를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88983-186">As an alternative, you can enter an asterisk (*) toospecify that all origin domains are accepted.</span></span>
5. <span data-ttu-id="88983-187">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-187">Click **Save**.</span></span>
   
   ![저장을 클릭합니다.](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="88983-189">클릭 한 후 **저장**, hello API 앱에는 JavaScript 수락할 호출 hello에서 URL을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-189">After you click **Save**, hello API app will accept JavaScript calls from hello specified URL.</span></span> <span data-ttu-id="88983-190">이 스크린 샷 hello ToDoListAPI0223 API 앱은 hello ToDoListAngular 웹 앱에서 JavaScript 클라이언트 호출을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-190">In this screen shot, hello ToDoListAPI0223 API app will accept JavaScript client calls from hello ToDoListAngular web app.</span></span>

### <a name="test-hello-application-with-cors-enabled"></a><span data-ttu-id="88983-191">CORS를 사용 하도록 설정 된 hello 응용 프로그램을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-191">Test hello application with CORS enabled</span></span>
* <span data-ttu-id="88983-192">브라우저 toohello hello 웹 앱의 HTTPS URL을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="88983-192">Open a browser toohello HTTPS URL of hello web app.</span></span> 
  
    <span data-ttu-id="88983-193">이 시간 hello 응용 프로그램을 사용 하 여 보고, 추가, 편집 및 할 일 항목을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88983-193">This time hello application lets you view, add, edit, and delete to-do items.</span></span> 
  
    ![샘플 응용 프로그램의 tooDo 목록 페이지](./media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a><span data-ttu-id="88983-195">앱 서비스 CORS와 Web API CORS</span><span class="sxs-lookup"><span data-stu-id="88983-195">App Service CORS versus Web API CORS</span></span>
<span data-ttu-id="88983-196">웹 API 프로젝트 hello를 설치할 수 있습니다 [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) API 수락할 수 있는 도메인에서 호출 된 JavaScript 코드에서 NuGet 패키지 toospecify 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-196">In a Web API project, you can install hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package toospecify in code which domains your API will accept JavaScript calls from.</span></span>

<span data-ttu-id="88983-197">Web API CORS 지원은 앱 서비스 CORS 지원보다 유연성이 뛰어납니다.</span><span class="sxs-lookup"><span data-stu-id="88983-197">Web API CORS support is more flexible than App Service CORS support.</span></span> <span data-ttu-id="88983-198">예를 들어 코드에서 다른 작업 메서드에 대해 다른 허용된 원본을 지정할 수 있는 반면 앱 서비스 CORS의 경우 모든 API 앱의 메서드에 대해 허용된 원본 집합을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-198">For example, in code you can specify different accepted origins for different action methods, while for App Service CORS you specify one set of accepted origins for all of an API app's methods.</span></span>

> [!NOTE]
> <span data-ttu-id="88983-199">Toouse 마세요 Web API CORS와 하나의 API 앱에 응용 프로그램 서비스 CORS 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-199">Don't try toouse both Web API CORS and App Service CORS in one API app.</span></span> <span data-ttu-id="88983-200">앱 서비스 CORS가 우선적으로 적용되며 Web API CORS는 아무 효과가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="88983-200">App Service CORS will take precedence and Web API CORS will have no effect.</span></span> <span data-ttu-id="88983-201">예를 들어, 앱 서비스에서 하나의 원본 도메인을 사용 하도록 설정 하 고 웹 API 코드에서 모든 원본 도메인을 사용 하도록 설정 하는 경우 Azure API 앱 에서만 수락 Azure에서 지정 된 hello 도메인에서 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-201">For example, if you enable one origin domain in App Service, and enable all origin domains in your Web API code, your Azure API app will only accept calls from hello domain you specified in Azure.</span></span>
> 
> 

### <a name="how-tooenable-cors-in-web-api-code"></a><span data-ttu-id="88983-202">어떻게 tooenable CORS 웹 API 코드에서</span><span class="sxs-lookup"><span data-stu-id="88983-202">How tooenable CORS in Web API code</span></span>
<span data-ttu-id="88983-203">단계를 수행 하는 hello Web API CORS 지원을 사용 하도록 설정 하는 것에 대 한 hello 프로세스를 요약 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-203">hello following steps summarize hello process for enabling Web API CORS support.</span></span> <span data-ttu-id="88983-204">자세한 내용은 [ASP.NET Web API 2에서 크로스-원본 리소스 요청 사용](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="88983-204">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span></span>

1. <span data-ttu-id="88983-205">웹 API 프로젝트에 설치 hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-205">In a Web API project, install hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package.</span></span>
2. <span data-ttu-id="88983-206">포함 한 `config.EnableCors()` hello 코드 줄 **등록** hello 방식의 **경우 WebApiConfig** hello 다음 예제와 같이 클래스를 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-206">Include a `config.EnableCors()` line of code in hello **Register** method of hello **WebApiConfig** class, as in hello following example.</span></span> 
   
        public static class WebApiConfig
        {
            public static void Register(HttpConfiguration config)
            {
                // Web API configuration and services
   
                // hello following line enables you toocontrol CORS by using Web API code
                config.EnableCors();
   
                // Web API routes
                config.MapHttpAttributeRoutes();
   
                config.Routes.MapHttpRoute(
                    name: "DefaultApi",
                    routeTemplate: "api/{controller}/{id}",
                    defaults: new { id = RouteParameter.Optional }
                );
            }
        }
3. <span data-ttu-id="88983-207">프로그램 Web API 컨트롤러에 추가 `using` hello에 대 한 문을 `System.Web.Http.Cors` 네임 스페이스, hello 추가 `EnableCors` toohello 컨트롤러 클래스 또는 tooindividual 작업 메서드에 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="88983-207">In your Web API controller, add a `using` statement for hello `System.Web.Http.Cors` namespace, and add hello `EnableCors` attribute toohello controller class or tooindividual action methods.</span></span> <span data-ttu-id="88983-208">다음 예제는 hello, CORS 지원 toohello 전체 컨트롤러를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-208">In hello following example, CORS support applies toohello entire controller.</span></span>
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a><span data-ttu-id="88983-209">API 앱으로 Azure API 관리 사용</span><span class="sxs-lookup"><span data-stu-id="88983-209">Using Azure API Management with API Apps</span></span>
<span data-ttu-id="88983-210">API 앱과 Azure API 관리를 사용 하는 경우 hello API 앱에서 CORS 대신 API 관리에서 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-210">If you use Azure API Management with an API app, configure CORS in API Management instead of in hello API app.</span></span> <span data-ttu-id="88983-211">자세한 내용은 다음 리소스는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="88983-211">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="88983-212">Azure API 관리 개요(비디오: CORS는 12:10부터 시작)</span><span class="sxs-lookup"><span data-stu-id="88983-212">Azure API Management Overview (video: CORS starts at 12:10)</span></span>](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/)
* [<span data-ttu-id="88983-213">도메인 정책 간 API 관리</span><span class="sxs-lookup"><span data-stu-id="88983-213">API Management cross domain policies</span></span>](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a><span data-ttu-id="88983-214">문제 해결</span><span class="sxs-lookup"><span data-stu-id="88983-214">Troubleshooting</span></span>
<span data-ttu-id="88983-215">다음은 이 자습서를 수행하는 동안 문제가 발생하는 경우에 사용할 몇 가지 문제 해결 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="88983-215">In case you run into a problem while going through this tutorial, here are some troubleshooting ideas.</span></span>

* <span data-ttu-id="88983-216">최신 버전의 hello hello를 사용 하는 확인 [Azure SDK for Visual Studio 2015에 대 한.NET](http://go.microsoft.com/fwlink/?linkid=518003)합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-216">Make sure that you're using hello latest version of hello [Azure SDK for .NET for Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="88983-217">입력 했는지 확인 `https` 에 CORS 설정을 hello을 만들고 사용 하는 경우 `https` toorun hello에 대 한 프런트 엔드 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="88983-217">Make sure that you entered `https` in hello CORS setting, and make sure that you're using `https` toorun hello front-end web app.</span></span>
* <span data-ttu-id="88983-218">Hello 프런트 엔드 웹 응용 프로그램 아니라 hello 중간 계층 API 앱에서 CORS 설정을 hello를 입력 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-218">Make sure that you entered hello CORS setting in hello middle tier API app, not in hello front-end web app.</span></span>
* <span data-ttu-id="88983-219">응용 프로그램 코드 및 Azure 앱 서비스의 CORS를 구성한 경우 note 응용 프로그램 코드에서 수행할 무엇이 든 hello 응용 프로그램 서비스 CORS 설정을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-219">If you're configuring CORS in both application code and Azure App Service, note that hello App Service CORS setting will override whatever you're doing in application code.</span></span> 

<span data-ttu-id="88983-220">문제 해결을 간소화 하는 Visual Studio 기능에 대해 자세히 toolearn 참조 [Visual Studio에서 문제 해결 Azure 앱 서비스 앱](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="88983-220">toolearn more about Visual Studio features that simplify troubleshooting, see [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="88983-221">다음 단계</span><span class="sxs-lookup"><span data-stu-id="88983-221">Next steps</span></span>
<span data-ttu-id="88983-222">이 문서에서는 앱 서비스 CORS tooenable 클라이언트 JavaScript 코드 다른 도메인에 있는 API를 호출할 수 있도록 지 원하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="88983-222">In this article, you saw how tooenable App Service CORS support so that client JavaScript code can call an API in a different domain.</span></span> <span data-ttu-id="88983-223">toolearn hello 읽기 API 앱에 대 한 자세한 [소개 tooauthentication 앱 서비스에서](../app-service/app-service-authentication-overview.md), toohello 넘어갑니다 [API 앱에 대 한 사용자 인증](app-service-api-dotnet-user-principal-auth.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="88983-223">toolearn more about API apps, read hello [introduction tooauthentication in App Service](../app-service/app-service-authentication-overview.md), and then go toohello [user authentication for API apps](app-service-api-dotnet-user-principal-auth.md) tutorial.</span></span>

