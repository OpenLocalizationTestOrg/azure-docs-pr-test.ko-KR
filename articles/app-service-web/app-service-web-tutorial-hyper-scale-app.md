---
title: "Azure에서 대규모 앱 aaaBuild | Microsoft Docs"
description: "Toouse 서로 다른 Azure 서비스 toomaximize Azure에서 ASP.NET 응용 프로그램의 성능을 hello 하는 방법에 대해 알아봅니다."
services: app-service\web
documentationcenter: dotnet
author: cephalin
manager: erikre
editor: 
ms.assetid: a4d49ac7-0f97-4997-84c5-cdb9c4465757
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 03/23/2017
ms.author: cephalin
ms.openlocfilehash: 7952647b49a82c286c6a737eb41a7f23a13fd75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a><span data-ttu-id="6b441-103">Azure에서 초대형 웹앱 빌드</span><span class="sxs-lookup"><span data-stu-id="6b441-103">Build a hyper-scale web app in Azure</span></span>

<span data-ttu-id="6b441-104">이 자습서는 ASP.NET 웹 앱에 Azure toomaximize 사용자 아웃 tooscale 요청 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-104">This tutorial shows you how tooscale out an ASP.NET web app in Azure toomaximize user requests.</span></span>

<span data-ttu-id="6b441-105">이 자습서를 시작 하기 전에 확인 하는 [hello Azure CLI가 설치 되어](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-105">Before starting this tutorial, ensure that [hello Azure CLI is installed](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span> <span data-ttu-id="6b441-106">또한 필요 [Visual Studio](https://www.visualstudio.com/vs/) 로컬 컴퓨터 toorun hello 예제 응용 프로그램에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-106">In addition, you need [Visual Studio](https://www.visualstudio.com/vs/) on your local machine toorun hello sample application.</span></span>

## <a name="step-1---get-sample-application"></a><span data-ttu-id="6b441-107">1단계 - 샘플 응용 프로그램 가져오기</span><span class="sxs-lookup"><span data-stu-id="6b441-107">Step 1 - Get sample application</span></span>
<span data-ttu-id="6b441-108">이 단계에서는 hello 로컬 ASP.NET 프로젝트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-108">In this step, you set up hello local ASP.NET project.</span></span>

### <a name="clone-hello-application-repository"></a><span data-ttu-id="6b441-109">복제 hello 응용 프로그램 저장소</span><span class="sxs-lookup"><span data-stu-id="6b441-109">Clone hello application repository</span></span>

<span data-ttu-id="6b441-110">사용자가 선택한 열려 hello 명령줄 터미널 및 `CD` tooa 작업 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-110">Open hello command-line terminal of your choice and `CD` tooa working directory.</span></span> <span data-ttu-id="6b441-111">그런 다음 실행된 hello 다음 tooclone hello 샘플 응용 프로그램을 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-111">Then, run hello following commands tooclone hello sample application.</span></span> 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-hello-sample-application-in-visual-studio"></a><span data-ttu-id="6b441-112">Visual Studio에서 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-112">Run hello sample application in Visual Studio</span></span>

<span data-ttu-id="6b441-113">Visual Studio에서 hello 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-113">Open hello solution in Visual Studio.</span></span>

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

<span data-ttu-id="6b441-114">형식 `F5` toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-114">Type `F5` toorun hello application.</span></span>

<span data-ttu-id="6b441-115">이 샘플 ASP.NET 웹 응용 프로그램이 hello 기본 서식 파일에서 제공 하 고 사용자 세션 및 사용 하 여 hello 출력 캐시를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-115">This sample ASP.NET web application comes from hello default template, and persists user sessions and uses hello output cache.</span></span> <span data-ttu-id="6b441-116">`HighScaleApp\Controllers\HomeController.cs`에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-116">Take a look at `HighScaleApp\Controllers\HomeController.cs`.</span></span> <span data-ttu-id="6b441-117">hello `Index()` 데이터 toohello 세션의 일부 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-117">hello `Index()` method adds a piece of data toohello session.</span></span>

```csharp
Session.Add("visited", "true"); 
```

<span data-ttu-id="6b441-118">Hello 및 `About()` 및 `Contact()` 메서드 출력을 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-118">And hello `About()` and `Contact()` methods cache their output.</span></span>

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-tooazure"></a><span data-ttu-id="6b441-119">2 단계-tooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="6b441-119">Step 2 - Deploy tooAzure</span></span>
<span data-ttu-id="6b441-120">이 단계에서는 Azure 웹 앱 만들고 샘플 ASP.NET 응용 프로그램 tooit 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-120">In this step, you create an Azure web app and deploy your sample ASP.NET application tooit.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="6b441-121">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="6b441-121">Create a resource group</span></span>   
<span data-ttu-id="6b441-122">사용 하 여 [az 그룹 만들기](https://docs.microsoft.com/cli/azure/group#create) toocreate는 [리소스 그룹](../azure-resource-manager/resource-group-overview.md) hello 서 부 유럽 지역에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-122">Use [az group create](https://docs.microsoft.com/cli/azure/group#create) toocreate a [resource group](../azure-resource-manager/resource-group-overview.md) in hello West Europe region.</span></span> <span data-ttu-id="6b441-123">리소스 그룹은 모든 정상 상태로 있는 백 엔드 hello 웹 앱 및 모든 SQL 데이터베이스와 같은 Azure 리소스 toomanage 함께 되도록 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-123">A resource group is where you put all hello Azure resources that you want toomanage together, such as hello web app and any SQL Database back end.</span></span>

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

<span data-ttu-id="6b441-124">toosee에 사용할 수 있는 가능한 값은 있습니다 `---location`, hello를 사용 하 여 [위치 나열 az appservice](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-124">toosee what possible values you can use for `---location`, use hello [az appservice list-locations](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="6b441-125">App Service 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="6b441-125">Create an App Service plan</span></span>
<span data-ttu-id="6b441-126">사용 하 여 [az 앱 서비스 계획 만들기](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate "B1" [앱 서비스 계획](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-126">Use [az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate a "B1" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

<span data-ttu-id="6b441-127">앱 서비스 계획은 배율 단위를 tooscale 원하는 또는 함께 over 아웃 동일를 환영 하는 앱을 개수에 관계 없이 포함할 수 있는 응용 프로그램 서비스 인프라입니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-127">An App Service plan is a scale unit, which can include any number of apps that you want tooscale up or out together over hello same App Service infrastructure.</span></span> <span data-ttu-id="6b441-128">또한 각 계획은 [가격 책정 계층](https://azure.microsoft.com/en-us/pricing/details/app-service/)에 할당되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-128">Each plan is also assigned a [pricing tier](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span></span> <span data-ttu-id="6b441-129">더 높은 계층은 더 많은 규모 확장 인스턴스와 같이 더 향상된 하드웨어와 더 많은 기능을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-129">Higher tiers include better hardware and more features, such as more scale-out instances.</span></span>

<span data-ttu-id="6b441-130">이 자습서에 대 한 b 1은 toothree 인스턴스 확장을 사용 하도록 설정 하는 hello 최소 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-130">For this tutorial, B1 is hello minimum tier that enables scale out toothree instances.</span></span> <span data-ttu-id="6b441-131">위로 또는 아래로 hello 가격대 나중에 실행 하 여 항상 응용 프로그램을 이동할 수 있습니다 [az 앱 서비스 계획 업데이트](https://docs.microsoft.com/cli/azure/appservice/plan#update)합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-131">You can always move your app up or down hello pricing tier later by running [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span></span> 

### <a name="create-a-web-app"></a><span data-ttu-id="6b441-132">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="6b441-132">Create a web app</span></span>
<span data-ttu-id="6b441-133">사용 하 여 [az 앱 서비스 웹 만들](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate 고유한 이름의 웹 응용 프로그램에서 `$appName`합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-133">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate a web app with a unique name in `$appName`.</span></span>

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a><span data-ttu-id="6b441-134">배포 자격 증명 설정</span><span class="sxs-lookup"><span data-stu-id="6b441-134">Set deployment credentials</span></span>
<span data-ttu-id="6b441-135">사용 하 여 [az 앱 서비스 웹 설정 된 배포 사용자](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset 응용 프로그램 서비스에 대 한 자격 증명을 계정 수준 배포입니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-135">Use [az appservice web deployment user set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset your account-level deployment credentials for App Service.</span></span>

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a><span data-ttu-id="6b441-136">Git 배포 구성</span><span class="sxs-lookup"><span data-stu-id="6b441-136">Configure Git deployment</span></span>
<span data-ttu-id="6b441-137">사용 하 여 [az 앱 서비스 웹 소스 제어-config-로컬-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure 로컬 Git 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-137">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure local Git deployment.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

<span data-ttu-id="6b441-138">이 명령은 hello 다음과 같은 출력을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-138">This command gives you an output that looks like hello following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="6b441-139">사용 하 여 hello 반환 URL tooconfigure 프로그램 Git 원격.</span><span class="sxs-lookup"><span data-stu-id="6b441-139">Use hello returned URL tooconfigure your Git remote.</span></span> <span data-ttu-id="6b441-140">hello 다음 명령을 사용 하 여 hello 앞에 출력 예입니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-140">hello following command uses hello preceding output example.</span></span>

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-hello-sample-application"></a><span data-ttu-id="6b441-141">Hello 샘플 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="6b441-141">Deploy hello sample application</span></span>
<span data-ttu-id="6b441-142">사용자는 이제 준비 toodeploy 샘플 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-142">You are now ready toodeploy your sample application.</span></span> <span data-ttu-id="6b441-143">`git push`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-143">Run `git push`.</span></span>

```powershell
git push azure master
```

<span data-ttu-id="6b441-144">암호에 대 한 메시지가 표시 되 면 hello 지정한 암호를 실행할 때 사용 하 여 `az appservice web deployment user set`합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-144">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-tooazure-web-app"></a><span data-ttu-id="6b441-145">TooAzure 웹 응용 프로그램 찾아보기</span><span class="sxs-lookup"><span data-stu-id="6b441-145">Browse tooAzure web app</span></span>
<span data-ttu-id="6b441-146">사용 하 여 [az 앱 서비스 웹 찾아보기](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee Azure에서 동시에 실행 되는 앱이이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-146">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee your app running live in Azure, run this command.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-tooredis"></a><span data-ttu-id="6b441-147">3 단계-tooRedis 연결</span><span class="sxs-lookup"><span data-stu-id="6b441-147">Step 3 - Connect tooRedis</span></span>
<span data-ttu-id="6b441-148">이 단계에서는 외부 공동 배치 된 캐시 tooyour Azure 웹 앱으로 Azure Redis Cache를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-148">In this step, you set up Azure Redis Cache as an external, colocated cache tooyour Azure web app.</span></span> <span data-ttu-id="6b441-149">신속 하 게 페이지 출력 Redis toocache를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-149">You can quickly utilize Redis toocache your page output.</span></span> <span data-ttu-id="6b441-150">또한 나중에 웹앱의 규모를 확장할 때 Redis를 사용하면 사용자 세션을 여러 인스턴스에 걸쳐 안정적으로 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-150">In addition, when you scale out your web apps later, Redis helps you persist user sessions across multiple instances reliably.</span></span>

### <a name="create-an-azure-redis-cache"></a><span data-ttu-id="6b441-151">Azure Redis Cache 만들기</span><span class="sxs-lookup"><span data-stu-id="6b441-151">Create an Azure Redis Cache</span></span>
<span data-ttu-id="6b441-152">사용 하 여 [az redis 만들](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate Azure Redis 캐시 하 고 JSON 출력 hello 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-152">Use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate an Azure Redis Cache and save hello JSON output.</span></span> <span data-ttu-id="6b441-153">`$cacheName`에 고유한 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-153">Use a unique name in `$cacheName`.</span></span>

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-hello-application-toouse-redis"></a><span data-ttu-id="6b441-154">Hello 응용 프로그램 toouse Redis 구성</span><span class="sxs-lookup"><span data-stu-id="6b441-154">Configure hello application toouse Redis</span></span>
<span data-ttu-id="6b441-155">캐시에 대 한 hello 연결 문자열의 서식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-155">Format hello connection string for your cache.</span></span>

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

<span data-ttu-id="6b441-156">다음과 같은 출력 hello 두 번째 줄을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-156">hello second line should give you an output that looks like this:</span></span>

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

<span data-ttu-id="6b441-157">Visual Studio에서 라는 프로젝트 루트에 웹 구성 파일을 만드는 `redis.config` 붙여넣기 hello에 코드를 다음 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-157">In Visual Studio, create a web configuration file in your project root called `redis.config` and paste hello following code into it.</span></span> <span data-ttu-id="6b441-158">`value`, hello PowerShell 출력에서에서 hello 연결 문자열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-158">In `value`, use hello connection string from hello PowerShell output.</span></span>

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

<span data-ttu-id="6b441-159">Hello 보면 `.gitignore` 파일에서 Git 리포지토리를 배웁니다이 파일이 소스 제어에서 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-159">If you look at hello `.gitignore` file in your Git repository, you'll see that this file is excluded from source control.</span></span> <span data-ttu-id="6b441-160">이런 방식으로 중요한 정보가 안전하게 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-160">That way your sensitive information is kept safe.</span></span> 

<span data-ttu-id="6b441-161">`Web.config`을(를) 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-161">Open `Web.config`.</span></span> <span data-ttu-id="6b441-162">공지 hello `<appSettings file="redis.config">` 요소에서 만든 hello 설정을 가져오는 `redis.config`합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-162">Notice hello `<appSettings file="redis.config">` element, which gets hello setting you created in `redis.config`.</span></span> 

<span data-ttu-id="6b441-163">Hello 주석 찾기 포함 된 섹션 `<sessionState>` 및 `<caching>`합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-163">Find hello commented section that includes `<sessionState>` and `<caching>`.</span></span> <span data-ttu-id="6b441-164">이 섹션의 주석 처리를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-164">Uncomment this section.</span></span>

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

<span data-ttu-id="6b441-165">이 코드에서 찾는 hello Redis 연결 문자열에 정의한 `RedisConnection`합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-165">This code looks for hello Redis connection string you defined in `RedisConnection`.</span></span> 

<span data-ttu-id="6b441-166">이제 응용 프로그램에 Redis toomanage 세션 및 캐싱을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-166">Your application now uses Redis toomanage sessions and caching.</span></span> <span data-ttu-id="6b441-167">형식 `F5` toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-167">Type `F5` toorun hello application.</span></span> <span data-ttu-id="6b441-168">원하는 경우는 Redis 관리 클라이언트 toovisualize hello 저장 된 데이터는 이제 toohello 캐시를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-168">If you like, you can download a Redis management client toovisualize hello data that is now saved toohello cache.</span></span>

### <a name="configure-hello-connection-string-in-azure"></a><span data-ttu-id="6b441-169">Azure의 hello 연결 문자열을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-169">Configure hello connection string in Azure</span></span>

<span data-ttu-id="6b441-170">Azure에서 응용 프로그램 toowork 프로그램, tooconfigure 필요 hello Azure 웹 앱에서 동일한 Redis 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-170">For your application toowork in Azure, you need tooconfigure hello same Redis connection string in your Azure web app.</span></span> <span data-ttu-id="6b441-171">이후 `redis.config` Git 배포를 실행 하는 경우 배포 된 tooAzure은 소스 제어에서 유지 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-171">Since `redis.config` is not maintained in source control, it is not deployed tooAzure when you run Git deployment.</span></span>

<span data-ttu-id="6b441-172">사용 하 여 [az 앱 서비스 웹 구성 appsettings 업데이트](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) hello로 tooadd hello 연결 문자열이 동일한 이름 (`RedisConnection`).</span><span class="sxs-lookup"><span data-stu-id="6b441-172">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd hello connection string with hello same name (`RedisConnection`).</span></span>

<span data-ttu-id="6b441-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6b441-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span></span>

<span data-ttu-id="6b441-174">에 유의 해야 `$connstring` hello 서식이 지정 된 연결 문자열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-174">Remember that `$connstring` contains hello formatted connection string.</span></span>

### <a name="redeploy-hello-application-tooazure"></a><span data-ttu-id="6b441-175">응용 프로그램 tooAzure hello를 다시 배포</span><span class="sxs-lookup"><span data-stu-id="6b441-175">Redeploy hello application tooAzure</span></span>
<span data-ttu-id="6b441-176">Git 명령 toopush 변경 tooAzure 사용</span><span class="sxs-lookup"><span data-stu-id="6b441-176">Use Git commands toopush your changes tooAzure</span></span>

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

<span data-ttu-id="6b441-177">암호에 대 한 메시지가 표시 되 면 hello 지정한 암호를 실행할 때 사용 하 여 `az appservice web deployment user set`합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-177">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="6b441-178">Toohello Azure 웹 앱을 찾아보기</span><span class="sxs-lookup"><span data-stu-id="6b441-178">Browse toohello Azure web app</span></span>
<span data-ttu-id="6b441-179">사용 하 여 [az 앱 서비스 웹 찾아보기](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee hello 변경 내용을 Azure에 거주 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-179">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee hello changes live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-toomultiple-instances"></a><span data-ttu-id="6b441-180">4 단계-눈금 toomultiple 인스턴스</span><span class="sxs-lookup"><span data-stu-id="6b441-180">Step 4 - Scale toomultiple instances</span></span>
<span data-ttu-id="6b441-181">앱 서비스 계획 hello Azure 웹 앱에 대 한 hello 배율 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-181">hello App Service plan is hello scale unit for your Azure web apps.</span></span> <span data-ttu-id="6b441-182">앱 서비스 계획 hello를 확장할 tooscale 웹 앱, 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-182">tooscale out your web app, you scale hello App Service plan.</span></span>

<span data-ttu-id="6b441-183">사용 하 여 [az 앱 서비스 계획 업데이트](https://docs.microsoft.com/cli/azure/appservice/plan#update) 는 hello 앱 서비스 계획 toothree 인스턴스 tooscale hello hello B1 가격 책정 계층에서 허용 되는 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-183">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale out hello App Service plan toothree instances, which is hello maximum number allowed by hello B1 pricing tier.</span></span> <span data-ttu-id="6b441-184">B1 가격 책정 계층 hello 이전 앱 서비스 계획을 만들 때 선택한 hello 임을 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-184">Remember that B1 is hello pricing tier that you chose when you created hello App Service plan earlier.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a><span data-ttu-id="6b441-185">5단계 - 지리적으로 크기 조정</span><span class="sxs-lookup"><span data-stu-id="6b441-185">Step 5 - Scale geographically</span></span>
<span data-ttu-id="6b441-186">지리적으로 크기 조정 하는 경우의 Azure 클라우드 hello 여러 지역에서 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-186">When scaling geographically, you run your app in multiple regions of hello Azure cloud.</span></span> <span data-ttu-id="6b441-187">이 설치 프로그램 고 부하를 분산 추가로 지리를 기반으로 하는 응용 프로그램 응용 프로그램 자세히 tooclient 브라우저를 배치 하 여 hello 응답 시간을 낮춥니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-187">This setup load-balances your app further based on geography and lowers hello response time by placing your app closer tooclient browsers.</span></span>

<span data-ttu-id="6b441-188">이 단계에서는 해당 ASP.NET 웹 응용 프로그램 tooa 두 번째 지역으로 확장할 있습니다 [Azure 트래픽 관리자](https://docs.microsoft.com/en-us/azure/traffic-manager/)합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-188">In this step, you scale your ASP.NET web app tooa second region with [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span></span> <span data-ttu-id="6b441-189">Hello 단계의 hello 끝 동남 아시아 (아직 만들어지지 않음)에서 실행 되는 웹 응용 프로그램와 웹 앱 (이미 만든)는 서 부 유럽에서 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-189">At hello end of hello step, you will have a web app running in West Europe (already created) and a web app running in Southeast Asia (not yet created).</span></span> <span data-ttu-id="6b441-190">두 앱 모두에서 제공 hello 트래픽 관리자 URL 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-190">Both apps will be served from hello same Traffic Manager URL.</span></span>

### <a name="scale-up-hello-europe-app-toostandard-tier"></a><span data-ttu-id="6b441-191">Hello 유럽 앱 tooStandard 계층 확장</span><span class="sxs-lookup"><span data-stu-id="6b441-191">Scale up hello Europe app tooStandard tier</span></span>
<span data-ttu-id="6b441-192">앱 서비스에서 Azure 트래픽 관리자와의 통합 hello 표준 가격 책정 계층이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-192">In App Service, integration with Azure Traffic Manager requires hello Standard pricing tier.</span></span> <span data-ttu-id="6b441-193">사용 하 여 [az 앱 서비스 계획 업데이트](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale 앱 서비스 계획 tooS1 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-193">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale up your App Service plan tooS1.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="6b441-194">Traffic Manager 프로필 만들기</span><span class="sxs-lookup"><span data-stu-id="6b441-194">Create a Traffic Manager profile</span></span> 
<span data-ttu-id="6b441-195">사용 하 여 [az 네트워크 트래픽 관리자 프로필 만들기](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate 트래픽 관리자 프로필 및 tooyour 리소스 그룹을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-195">Use [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate a Traffic Manager profile and add it tooyour resource group.</span></span> <span data-ttu-id="6b441-196">$dnsName에 고유한 DNS 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-196">Use a unique DNS name in $dnsName.</span></span>

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> <span data-ttu-id="6b441-197">`--routing-method Performance`지정 하는이 프로필 [사용자 트래픽을 가장 가까운 끝점 toohello 라우팅합니다](../traffic-manager/traffic-manager-routing-methods.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-197">`--routing-method Performance` specifies that this profile [routes user traffic toohello closest endpoint](../traffic-manager/traffic-manager-routing-methods.md).</span></span>

### <a name="get-hello-resource-id-of-hello-europe-app"></a><span data-ttu-id="6b441-198">Hello 유럽 응용 프로그램의 hello 리소스 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="6b441-198">Get hello resource ID of hello Europe app</span></span>
<span data-ttu-id="6b441-199">사용 하 여 [az 앱 서비스 웹 쇼](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) 웹 앱의 tooget hello 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-199">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello resource ID of your web app.</span></span>

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-europe-app"></a><span data-ttu-id="6b441-200">Hello 유럽 응용 프로그램에 대 한 트래픽 관리자 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="6b441-200">Add a Traffic Manager endpoint for hello Europe app</span></span>
<span data-ttu-id="6b441-201">사용 하 여 [az 네트워크 트래픽 관리자 끝점 만들기](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd 끝점 tooyour 트래픽 관리자 프로필 및 웹 응용 프로그램을 사용 하 여 hello 리소스 ID hello 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-201">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd an endpoint tooyour Traffic Manager profile and use hello resource ID of your web app as hello target.</span></span>

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-hello-traffic-manager-endpoint-url"></a><span data-ttu-id="6b441-202">Hello 트래픽 관리자 끝점 URL 가져오기</span><span class="sxs-lookup"><span data-stu-id="6b441-202">Get hello Traffic Manager endpoint URL</span></span>
<span data-ttu-id="6b441-203">트래픽 관리자 프로필에 끝점이 해당 지점 tooyour 기존 웹 앱 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-203">Your Traffic Manager profile now has an endpoint that points tooyour existing web app.</span></span> <span data-ttu-id="6b441-204">사용 하 여 [az 네트워크 트래픽 관리자 프로필 표시](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget 해당 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-204">Use [az network traffic-manager profile show](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget its URL.</span></span> 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

<span data-ttu-id="6b441-205">Hello 출력 브라우저에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-205">Copy hello output into your browser.</span></span> <span data-ttu-id="6b441-206">웹앱을 다시 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-206">You should see your web app again.</span></span>

### <a name="create-an-azure-redis-cache-in-asia"></a><span data-ttu-id="6b441-207">아시아에 Azure Redis Cache 만들기</span><span class="sxs-lookup"><span data-stu-id="6b441-207">Create an Azure Redis Cache in Asia</span></span>
<span data-ttu-id="6b441-208">이제 Azure 웹 앱 toohello 동남 아시아 지역을 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-208">Now, you replicate your Azure web app toohello Southeast Asia region.</span></span> <span data-ttu-id="6b441-209">toostart를 사용 하 여 [az redis 만들](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate 동남 아시아에 두 번째 Azure Redis 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-209">toostart, use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate a second Azure Redis Cache in Southeast Asia.</span></span> <span data-ttu-id="6b441-210">이 캐시 toobe 아시아의 응용 프로그램과 함께 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-210">This cache needs toobe colocated with your app in Asia.</span></span>

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

<span data-ttu-id="6b441-211">`--name $cacheName-asia`제공 hello hello로 hello 서 부 유럽 캐시의 캐시 hello 이름을 `-asia` 접미사입니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-211">`--name $cacheName-asia` gives hello cache hello name of hello West Europe cache, with hello `-asia` suffix.</span></span>

### <a name="create-an-app-service-plan-in-asia"></a><span data-ttu-id="6b441-212">아시아에 App Service 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="6b441-212">Create an App Service plan in Asia</span></span>
<span data-ttu-id="6b441-213">사용 하 여 [az 앱 서비스 계획 만들기](https://docs.microsoft.com/cli/azure/appservice/plan#create) hello를 사용 하 여 hello 서 부 유럽 계획으로 계층 동일한 S1, 동남 아시아 지역의 hello toocreate 두 번째 응용 프로그램 서비스 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-213">Use [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate a second App Service plan in hello Southeast Asia region, using hello same S1 tier as hello West Europe plan.</span></span>

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a><span data-ttu-id="6b441-214">아시아에 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="6b441-214">Create a web app in Asia</span></span>
<span data-ttu-id="6b441-215">사용 하 여 [az 앱 서비스 웹 만들](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate 두 번째 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-215">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate a second web app.</span></span>

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

<span data-ttu-id="6b441-216">`--name $appName-asia`제공 hello로 hello 서 부 유럽 응용 프로그램의 응용 프로그램 hello 이름 hello `-asia` 접미사입니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-216">`--name $appName-asia` gives hello app hello name of hello West Europe app, with hello `-asia` suffix.</span></span>

### <a name="configure-hello-connection-string-for-redis"></a><span data-ttu-id="6b441-217">Redis 용 hello 연결 문자열을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-217">Configure hello connection string for Redis</span></span>
<span data-ttu-id="6b441-218">사용 하 여 [az 앱 서비스 웹 구성 appsettings 업데이트](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd toohello 웹 응용 프로그램 hello 연결에 대 한 문자열 hello 동남 아시아 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-218">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd toohello web app hello connection string for hello Southeast Asia cache.</span></span>

<span data-ttu-id="6b441-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6b441-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span></span>

### <a name="configure-git-deployment-for-hello-asia-app"></a><span data-ttu-id="6b441-220">Hello 아시아 앱에 대 한 Git 배포를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-220">Configure Git deployment for hello Asia app.</span></span>
<span data-ttu-id="6b441-221">사용 하 여 [az 앱 서비스 웹 소스 제어-config-로컬-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure hello 두 번째 웹 응용 프로그램에 대 한 로컬 Git 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-221">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure local Git deployment for hello second web app.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="6b441-222">이 명령은 hello 다음과 같은 출력을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-222">This command gives you an output that looks like hello following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="6b441-223">사용 하 여 hello 반환 URL tooconfigure 두 번째 Git 로컬 저장소에 대 한 원격.</span><span class="sxs-lookup"><span data-stu-id="6b441-223">Use hello returned URL tooconfigure a second Git remote for your local repository.</span></span> <span data-ttu-id="6b441-224">hello 다음 명령을 사용 하 여 hello 앞에 출력 예입니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-224">hello following command uses hello preceding output example.</span></span>

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a><span data-ttu-id="6b441-225">샘플 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="6b441-225">Deploy your sample application</span></span>
<span data-ttu-id="6b441-226">실행 `git push` toodeploy 샘플 응용 프로그램 toohello 두 번째 Git 원격입니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-226">Run `git push` toodeploy your sample application toohello second Git remote.</span></span> 

```bash
git push azure-asia master
```

<span data-ttu-id="6b441-227">암호에 대 한 메시지가 표시 되 면 hello 지정한 암호를 실행할 때 사용 하 여 `az appservice web deployment user set`합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-227">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-toohello-asia-app"></a><span data-ttu-id="6b441-228">Toohello 아시아 응용 프로그램 찾아보기</span><span class="sxs-lookup"><span data-stu-id="6b441-228">Browse toohello Asia app</span></span>
<span data-ttu-id="6b441-229">사용 하 여 [az 앱 서비스 웹 찾아보기](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) tooverify 응용 프로그램은 Azure에서 실시간 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-229">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) tooverify that your app is running live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-hello-resource-id-of-hello-asia-app"></a><span data-ttu-id="6b441-230">Hello 아시아 응용 프로그램의 hello 리소스 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="6b441-230">Get hello resource ID of hello Asia app</span></span>
<span data-ttu-id="6b441-231">사용 하 여 [az 앱 서비스 웹 쇼](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) 동남 아시아에서 웹 응용 프로그램의 tooget hello 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-231">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello resource ID of your web app in Southeast Asia.</span></span>

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-asia-app"></a><span data-ttu-id="6b441-232">Hello 아시아 응용 프로그램에 대 한 트래픽 관리자 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="6b441-232">Add a Traffic Manager endpoint for hello Asia app</span></span>
<span data-ttu-id="6b441-233">사용 하 여 [az 네트워크 트래픽 관리자 끝점 만들기](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd 두 번째 끝점 toohello 트래픽 관리자 프로필.</span><span class="sxs-lookup"><span data-stu-id="6b441-233">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd a second endpoint toohello Traffic Manager profile.</span></span>

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-tooweb-apps"></a><span data-ttu-id="6b441-234">지역 식별자 tooweb 앱 추가</span><span class="sxs-lookup"><span data-stu-id="6b441-234">Add region identifier tooweb apps</span></span>
<span data-ttu-id="6b441-235">사용 하 여 [az 앱 서비스 웹 구성 appsettings 업데이트](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd 지역별 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-235">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd a region-specific environment variable.</span></span>

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="6b441-236">응용 프로그램 코드는 이미 이 응용 프로그램 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-236">Your application code already uses this application setting.</span></span> <span data-ttu-id="6b441-237">`HighScaleApp\Views\Home\Index.cshtml`에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-237">Take a look at `HighScaleApp\Views\Home\Index.cshtml`.</span></span>

### <a name="complete"></a><span data-ttu-id="6b441-238">완료!</span><span class="sxs-lookup"><span data-stu-id="6b441-238">Complete!</span></span>

<span data-ttu-id="6b441-239">이제 서로 다른 지리적 지역에 대 한 브라우저에서 트래픽 관리자 프로필의 tooaccess hello URL을 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6b441-239">Now, try tooaccess hello URL of your Traffic Manager profile from browsers in different geographical regions.</span></span> <span data-ttu-id="6b441-240">유럽의 클라이언트 브라우저는 “ASP.NET West Europe”, 아시아의 클라이언트 브라우저는 “ASP.NET Southeast Asia”가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b441-240">Client browsers from Europe should show "ASP.NET West Europe", and client browser from Asia should show "ASP.NET Southeast Asia."</span></span>

## <a name="more-resources"></a><span data-ttu-id="6b441-241">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="6b441-241">More resources</span></span>
