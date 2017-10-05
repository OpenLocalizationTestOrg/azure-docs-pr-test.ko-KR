---
title: "Azure에서 초대형 앱 빌드 | Microsoft Docs"
description: "Azure에서 ASP.NET 앱의 성능을 최대화하기 위해 서로 다른 Azure 서비스를 사용하는 방법에 알아봅니다."
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
ms.openlocfilehash: eac9c5b0d8d0f7802d88e6f4f27d9d23c406e025
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a><span data-ttu-id="442d4-103">Azure에서 초대형 웹앱 빌드</span><span class="sxs-lookup"><span data-stu-id="442d4-103">Build a hyper-scale web app in Azure</span></span>

<span data-ttu-id="442d4-104">이 자습서에서는 사용자 요청을 최대화하기 위해 Azure에서 ASP.NET 웹앱의 규모를 확장하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-104">This tutorial shows you how to scale out an ASP.NET web app in Azure to maximize user requests.</span></span>

<span data-ttu-id="442d4-105">이 자습서를 시작하기 전에 컴퓨터에 [Azure CLI가 설치되었는지](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-105">Before starting this tutorial, ensure that [the Azure CLI is installed](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span> <span data-ttu-id="442d4-106">또한 샘플 응용 프로그램을 실행하려면 로컬 컴퓨터에 [Visual Studio](https://www.visualstudio.com/vs/)가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-106">In addition, you need [Visual Studio](https://www.visualstudio.com/vs/) on your local machine to run the sample application.</span></span>

## <a name="step-1---get-sample-application"></a><span data-ttu-id="442d4-107">1단계 - 샘플 응용 프로그램 가져오기</span><span class="sxs-lookup"><span data-stu-id="442d4-107">Step 1 - Get sample application</span></span>
<span data-ttu-id="442d4-108">이 단계에서 로컬 ASP.NET 프로젝트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-108">In this step, you set up the local ASP.NET project.</span></span>

### <a name="clone-the-application-repository"></a><span data-ttu-id="442d4-109">응용 프로그램 리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="442d4-109">Clone the application repository</span></span>

<span data-ttu-id="442d4-110">선택한 명령줄 터미널을 열고 작업 디렉터리로 `CD` 합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-110">Open the command-line terminal of your choice and `CD` to a working directory.</span></span> <span data-ttu-id="442d4-111">그런 다음 샘플 응용 프로그램을 복제하기 위해 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-111">Then, run the following commands to clone the sample application.</span></span> 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-the-sample-application-in-visual-studio"></a><span data-ttu-id="442d4-112">Visual Studio에서 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="442d4-112">Run the sample application in Visual Studio</span></span>

<span data-ttu-id="442d4-113">Visual Studio에서 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-113">Open the solution in Visual Studio.</span></span>

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

<span data-ttu-id="442d4-114">`F5`를 입력하여 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-114">Type `F5` to run the application.</span></span>

<span data-ttu-id="442d4-115">이 샘플 ASP.NET 웹 응용 프로그램은 기본 템플릿에서 제공되며 사용자 세션을 유지하고 출력 캐시를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-115">This sample ASP.NET web application comes from the default template, and persists user sessions and uses the output cache.</span></span> <span data-ttu-id="442d4-116">`HighScaleApp\Controllers\HomeController.cs`에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-116">Take a look at `HighScaleApp\Controllers\HomeController.cs`.</span></span> <span data-ttu-id="442d4-117">`Index()` 메서드는 데이터 일부를 세션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-117">The `Index()` method adds a piece of data to the session.</span></span>

```csharp
Session.Add("visited", "true"); 
```

<span data-ttu-id="442d4-118">또한 `About()` 및 `Contact()` 메서드는 해당 출력을 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-118">And the `About()` and `Contact()` methods cache their output.</span></span>

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-to-azure"></a><span data-ttu-id="442d4-119">2단계 - Azure에 배포</span><span class="sxs-lookup"><span data-stu-id="442d4-119">Step 2 - Deploy to Azure</span></span>
<span data-ttu-id="442d4-120">이 단계에서는 Azure 웹앱 만들고 샘플 ASP.NET 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-120">In this step, you create an Azure web app and deploy your sample ASP.NET application to it.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="442d4-121">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="442d4-121">Create a resource group</span></span>   
<span data-ttu-id="442d4-122">[az 그룹 만들기](https://docs.microsoft.com/cli/azure/group#create)를 사용하여 유럽 서부 지역에 [리소스 그룹](../azure-resource-manager/resource-group-overview.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-122">Use [az group create](https://docs.microsoft.com/cli/azure/group#create) to create a [resource group](../azure-resource-manager/resource-group-overview.md) in the West Europe region.</span></span> <span data-ttu-id="442d4-123">리소스 그룹은 웹앱 및 해당 SQL Database 백 엔드와 같이 함께 관리하고자 하는 모든 Azure 리소스를 배치하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-123">A resource group is where you put all the Azure resources that you want to manage together, such as the web app and any SQL Database back end.</span></span>

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

<span data-ttu-id="442d4-124">`---location`에 사용할 수 있는 가능한 값을 보려면 [az appservice list-locations](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-124">To see what possible values you can use for `---location`, use the [az appservice list-locations](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="442d4-125">앱 서비스 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="442d4-125">Create an App Service plan</span></span>
<span data-ttu-id="442d4-126">[az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create)를 사용하여 “B1” [App Service 계획](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-126">Use [az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) to create a "B1" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

<span data-ttu-id="442d4-127">App Service 계획은 동일한 App Service 인프라를 통해 함께 강화 또는 규모 확장하고자 하는 많은 앱을 포함할 수 있는 배율 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-127">An App Service plan is a scale unit, which can include any number of apps that you want to scale up or out together over the same App Service infrastructure.</span></span> <span data-ttu-id="442d4-128">또한 각 계획은 [가격 책정 계층](https://azure.microsoft.com/en-us/pricing/details/app-service/)에 할당되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-128">Each plan is also assigned a [pricing tier](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span></span> <span data-ttu-id="442d4-129">더 높은 계층은 더 많은 규모 확장 인스턴스와 같이 더 향상된 하드웨어와 더 많은 기능을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-129">Higher tiers include better hardware and more features, such as more scale-out instances.</span></span>

<span data-ttu-id="442d4-130">이 자습서에서 B1은 세 개의 인스턴스로 규모 확장이 가능한 최소 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-130">For this tutorial, B1 is the minimum tier that enables scale out to three instances.</span></span> <span data-ttu-id="442d4-131">나중에 [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update)를 실행하여 앱을 가격 책정 계층 위아래로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-131">You can always move your app up or down the pricing tier later by running [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span></span> 

### <a name="create-a-web-app"></a><span data-ttu-id="442d4-132">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="442d4-132">Create a web app</span></span>
<span data-ttu-id="442d4-133">[az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create)를 사용하여 `$appName`에서 고유한 이름을 갖는 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-133">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) to create a web app with a unique name in `$appName`.</span></span>

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a><span data-ttu-id="442d4-134">배포 자격 증명 설정</span><span class="sxs-lookup"><span data-stu-id="442d4-134">Set deployment credentials</span></span>
<span data-ttu-id="442d4-135">[az appservice web deployment user set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set)을 사용하여 App Service에 대한 계정 수준 배포 자격 증명을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-135">Use [az appservice web deployment user set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) to set your account-level deployment credentials for App Service.</span></span>

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a><span data-ttu-id="442d4-136">Git 배포 구성</span><span class="sxs-lookup"><span data-stu-id="442d4-136">Configure Git deployment</span></span>
<span data-ttu-id="442d4-137">[az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git)을 사용하여 로컬 Git 배포를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-137">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) to configure local Git deployment.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

<span data-ttu-id="442d4-138">이 명령은 다음과 같은 출력을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-138">This command gives you an output that looks like the following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="442d4-139">반환된 URL을 사용하여 Git 원격을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-139">Use the returned URL to configure your Git remote.</span></span> <span data-ttu-id="442d4-140">다음 명령은 앞의 출력 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-140">The following command uses the preceding output example.</span></span>

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-the-sample-application"></a><span data-ttu-id="442d4-141">샘플 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="442d4-141">Deploy the sample application</span></span>
<span data-ttu-id="442d4-142">이제 샘플 응용 프로그램을 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-142">You are now ready to deploy your sample application.</span></span> <span data-ttu-id="442d4-143">`git push`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-143">Run `git push`.</span></span>

```powershell
git push azure master
```

<span data-ttu-id="442d4-144">암호를 입력하라는 메시지가 표시되면 `az appservice web deployment user set`을 실행할 때 지정한 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-144">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-azure-web-app"></a><span data-ttu-id="442d4-145">Azure 웹앱 찾아보기</span><span class="sxs-lookup"><span data-stu-id="442d4-145">Browse to Azure web app</span></span>
<span data-ttu-id="442d4-146">[az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse)를 사용하여 Azure에서 실시간으로 실행 중인 앱을 확인하려면 이 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-146">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to see your app running live in Azure, run this command.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-to-redis"></a><span data-ttu-id="442d4-147">3단계 - Redis에 연결</span><span class="sxs-lookup"><span data-stu-id="442d4-147">Step 3 - Connect to Redis</span></span>
<span data-ttu-id="442d4-148">이 단계에서는 Azure Redis Cache를 Azure 웹앱에 공동 배치된 외부 캐시로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-148">In this step, you set up Azure Redis Cache as an external, colocated cache to your Azure web app.</span></span> <span data-ttu-id="442d4-149">Redis를 신속하게 활용하여 페이지 출력을 캐시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-149">You can quickly utilize Redis to cache your page output.</span></span> <span data-ttu-id="442d4-150">또한 나중에 웹앱의 규모를 확장할 때 Redis를 사용하면 사용자 세션을 여러 인스턴스에 걸쳐 안정적으로 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-150">In addition, when you scale out your web apps later, Redis helps you persist user sessions across multiple instances reliably.</span></span>

### <a name="create-an-azure-redis-cache"></a><span data-ttu-id="442d4-151">Azure Redis Cache 만들기</span><span class="sxs-lookup"><span data-stu-id="442d4-151">Create an Azure Redis Cache</span></span>
<span data-ttu-id="442d4-152">[az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create)를 사용하여 Azure Redis Cache를 만들고 JSON 출력을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-152">Use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) to create an Azure Redis Cache and save the JSON output.</span></span> <span data-ttu-id="442d4-153">`$cacheName`에 고유한 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-153">Use a unique name in `$cacheName`.</span></span>

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-the-application-to-use-redis"></a><span data-ttu-id="442d4-154">Redis를 사용하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="442d4-154">Configure the application to use Redis</span></span>
<span data-ttu-id="442d4-155">사용자 캐시에 연결 문자열의 서식을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-155">Format the connection string for your cache.</span></span>

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

<span data-ttu-id="442d4-156">두 번째 줄은 다음과 같은 출력을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-156">The second line should give you an output that looks like this:</span></span>

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

<span data-ttu-id="442d4-157">Visual Studio에서 `redis.config`라는 프로젝트 루트에 웹 구성 파일을 만들고 다음 코드를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-157">In Visual Studio, create a web configuration file in your project root called `redis.config` and paste the following code into it.</span></span> <span data-ttu-id="442d4-158">`value`에서 PowerShell 출력의 연결 문자열을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-158">In `value`, use the connection string from the PowerShell output.</span></span>

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

<span data-ttu-id="442d4-159">Git 리포지토리에 `.gitignore` 파일이 있으면 이 파일이 원본 제어에서 제외되었음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-159">If you look at the `.gitignore` file in your Git repository, you'll see that this file is excluded from source control.</span></span> <span data-ttu-id="442d4-160">이런 방식으로 중요한 정보가 안전하게 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-160">That way your sensitive information is kept safe.</span></span> 

<span data-ttu-id="442d4-161">`Web.config`를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-161">Open `Web.config`.</span></span> <span data-ttu-id="442d4-162">`redis.config`에서 만든 설정을 가져오는 `<appSettings file="redis.config">` 요소에 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="442d4-162">Notice the `<appSettings file="redis.config">` element, which gets the setting you created in `redis.config`.</span></span> 

<span data-ttu-id="442d4-163">`<sessionState>` 및 `<caching>`을 포함하는 주석 처리된 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-163">Find the commented section that includes `<sessionState>` and `<caching>`.</span></span> <span data-ttu-id="442d4-164">이 섹션의 주석 처리를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-164">Uncomment this section.</span></span>

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

<span data-ttu-id="442d4-165">이 코드는 `RedisConnection`에서 정의한 Redis 연결 문자열을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-165">This code looks for the Redis connection string you defined in `RedisConnection`.</span></span> 

<span data-ttu-id="442d4-166">이제 응용 프로그램이 Redis를 사용하여 세션 및 캐싱을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-166">Your application now uses Redis to manage sessions and caching.</span></span> <span data-ttu-id="442d4-167">`F5`를 입력하여 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-167">Type `F5` to run the application.</span></span> <span data-ttu-id="442d4-168">원하는 경우 Redis 관리 클라이언트를 다운로드하면 이제 캐시에 저장된 데이터를 시각화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-168">If you like, you can download a Redis management client to visualize the data that is now saved to the cache.</span></span>

### <a name="configure-the-connection-string-in-azure"></a><span data-ttu-id="442d4-169">Azure에서 연결 문자열 구성</span><span class="sxs-lookup"><span data-stu-id="442d4-169">Configure the connection string in Azure</span></span>

<span data-ttu-id="442d4-170">Azure에서 작동하는 응용 프로그램의 경우 Azure 웹앱에서 동일한 Redis 연결 문자열을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-170">For your application to work in Azure, you need to configure the same Redis connection string in your Azure web app.</span></span> <span data-ttu-id="442d4-171">`redis.config`가 원본 제어에서 유지 관리되지 않으므로 Git 배포를 실행하는 경우 Azure에 배포되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-171">Since `redis.config` is not maintained in source control, it is not deployed to Azure when you run Git deployment.</span></span>

<span data-ttu-id="442d4-172">[az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update)를 사용하여 동일한 이름(`RedisConnection`)의 연결 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-172">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add the connection string with the same name (`RedisConnection`).</span></span>

<span data-ttu-id="442d4-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="442d4-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span></span>

<span data-ttu-id="442d4-174">`$connstring`에는 서식이 지정된 연결 문자열이 포함되어 있음에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="442d4-174">Remember that `$connstring` contains the formatted connection string.</span></span>

### <a name="redeploy-the-application-to-azure"></a><span data-ttu-id="442d4-175">Azure에 응용 프로그램을 다시 배포</span><span class="sxs-lookup"><span data-stu-id="442d4-175">Redeploy the application to Azure</span></span>
<span data-ttu-id="442d4-176">Git 명령을 사용하여 변경 내용을 Azure에 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-176">Use Git commands to push your changes to Azure</span></span>

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

<span data-ttu-id="442d4-177">암호를 입력하라는 메시지가 표시되면 `az appservice web deployment user set`을 실행할 때 지정한 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-177">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="442d4-178">Azure 웹앱 찾아보기</span><span class="sxs-lookup"><span data-stu-id="442d4-178">Browse to the Azure web app</span></span>
<span data-ttu-id="442d4-179">[az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse)를 사용하여 Azure에서 변경 내용을 실시간으로 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-179">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to see the changes live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-to-multiple-instances"></a><span data-ttu-id="442d4-180">4단계 - 여러 인스턴스로 크기 조정</span><span class="sxs-lookup"><span data-stu-id="442d4-180">Step 4 - Scale to multiple instances</span></span>
<span data-ttu-id="442d4-181">App Service 계획은 Azure 웹앱에 대한 배율 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-181">The App Service plan is the scale unit for your Azure web apps.</span></span> <span data-ttu-id="442d4-182">웹앱 규모를 확장하려면 App Service 계획의 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-182">To scale out your web app, you scale the App Service plan.</span></span>

<span data-ttu-id="442d4-183">[az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update)를 사용하여 App Service 계획의 규모를 B1 가격 책정 계층에서 허용하는 최대 수인 세 개의 인스턴스로 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-183">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) to scale out the App Service plan to three instances, which is the maximum number allowed by the B1 pricing tier.</span></span> <span data-ttu-id="442d4-184">B1은 이전에 App Service 계획을 만들 때 선택한 가격 책정 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-184">Remember that B1 is the pricing tier that you chose when you created the App Service plan earlier.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a><span data-ttu-id="442d4-185">5단계 - 지리적으로 크기 조정</span><span class="sxs-lookup"><span data-stu-id="442d4-185">Step 5 - Scale geographically</span></span>
<span data-ttu-id="442d4-186">지리적으로 크기를 조정할 때 Azure 클라우드의 여러 하위 지역에서 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-186">When scaling geographically, you run your app in multiple regions of the Azure cloud.</span></span> <span data-ttu-id="442d4-187">이 설정은 지리에 기반하여 추가로 앱 부하를 분산하며, 앱을 클라이언트 브라우저에 가까이 배치함으로써 반응 시간을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-187">This setup load-balances your app further based on geography and lowers the response time by placing your app closer to client browsers.</span></span>

<span data-ttu-id="442d4-188">이 단계에서 [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/)를 사용하여 ASP.NET 웹앱을 두 번째 하위 지역으로 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-188">In this step, you scale your ASP.NET web app to a second region with [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span></span> <span data-ttu-id="442d4-189">단계 마지막에는 유럽 서부에서 실행되는 웹앱(이미 생성함) 및 동남 아시아에서 실행되는 웹앱(아직 생성하지 않음)이 생기게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-189">At the end of the step, you will have a web app running in West Europe (already created) and a web app running in Southeast Asia (not yet created).</span></span> <span data-ttu-id="442d4-190">두 앱은 동일한 Traffic Manager URL에서 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-190">Both apps will be served from the same Traffic Manager URL.</span></span>

### <a name="scale-up-the-europe-app-to-standard-tier"></a><span data-ttu-id="442d4-191">유럽 앱을 표준 계층으로 강화</span><span class="sxs-lookup"><span data-stu-id="442d4-191">Scale up the Europe app to Standard tier</span></span>
<span data-ttu-id="442d4-192">App Service에서 Azure Traffic Manager와 통합하려면 표준 가격 책정 계층이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-192">In App Service, integration with Azure Traffic Manager requires the Standard pricing tier.</span></span> <span data-ttu-id="442d4-193">[az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update)를 사용하여 App Service 계획을 S1로 강화합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-193">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) to scale up your App Service plan to S1.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="442d4-194">Traffic Manager 프로필 만들기</span><span class="sxs-lookup"><span data-stu-id="442d4-194">Create a Traffic Manager profile</span></span> 
<span data-ttu-id="442d4-195">[az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create)를 사용하여 Traffic Manager 프로필을 만들고 리소스 그룹에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-195">Use [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) to create a Traffic Manager profile and add it to your resource group.</span></span> <span data-ttu-id="442d4-196">$dnsName에 고유한 DNS 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-196">Use a unique DNS name in $dnsName.</span></span>

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> <span data-ttu-id="442d4-197">`--routing-method Performance`는 이 프로필이 [사용자 트래픽을 가장 가까운 끝점으로 라우팅](../traffic-manager/traffic-manager-routing-methods.md)하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-197">`--routing-method Performance` specifies that this profile [routes user traffic to the closest endpoint](../traffic-manager/traffic-manager-routing-methods.md).</span></span>

### <a name="get-the-resource-id-of-the-europe-app"></a><span data-ttu-id="442d4-198">유럽 앱의 리소스 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="442d4-198">Get the resource ID of the Europe app</span></span>
<span data-ttu-id="442d4-199">[az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show)를 사용하여 웹앱의 리소스 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-199">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) to get the resource ID of your web app.</span></span>

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-the-europe-app"></a><span data-ttu-id="442d4-200">유럽 앱에 대한 Traffic Manager 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="442d4-200">Add a Traffic Manager endpoint for the Europe app</span></span>
<span data-ttu-id="442d4-201">[az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create)를 사용하여 끝점을 Traffic Manager 프로필에 추가하고 웹앱의 리소스 ID를 대상으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-201">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) to add an endpoint to your Traffic Manager profile and use the resource ID of your web app as the target.</span></span>

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-the-traffic-manager-endpoint-url"></a><span data-ttu-id="442d4-202">Traffic Manager 끝점 URL 가져오기</span><span class="sxs-lookup"><span data-stu-id="442d4-202">Get the Traffic Manager endpoint URL</span></span>
<span data-ttu-id="442d4-203">이제 Traffic Manager 프로필에 기존 웹앱을 가리키는 끝점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-203">Your Traffic Manager profile now has an endpoint that points to your existing web app.</span></span> <span data-ttu-id="442d4-204">[az network traffic-manager profile show](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show)를 사용하여 해당 URL을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-204">Use [az network traffic-manager profile show](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) to get its URL.</span></span> 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

<span data-ttu-id="442d4-205">브라우저에 출력을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-205">Copy the output into your browser.</span></span> <span data-ttu-id="442d4-206">웹앱을 다시 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-206">You should see your web app again.</span></span>

### <a name="create-an-azure-redis-cache-in-asia"></a><span data-ttu-id="442d4-207">아시아에 Azure Redis Cache 만들기</span><span class="sxs-lookup"><span data-stu-id="442d4-207">Create an Azure Redis Cache in Asia</span></span>
<span data-ttu-id="442d4-208">이제 Azure 웹앱을 동남 아시아 지역으로 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-208">Now, you replicate your Azure web app to the Southeast Asia region.</span></span> <span data-ttu-id="442d4-209">시작하려면 [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create)를 사용하여 동남 아시아에 두 번째는 Azure Redis Cache를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-209">To start, use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) to create a second Azure Redis Cache in Southeast Asia.</span></span> <span data-ttu-id="442d4-210">이 캐시는 아시아의 앱과 공동 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-210">This cache needs to be colocated with your app in Asia.</span></span>

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

<span data-ttu-id="442d4-211">`--name $cacheName-asia`는 캐시에 `-asia` 접미사가 있는 유럽 서부 캐시의 이름을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-211">`--name $cacheName-asia` gives the cache the name of the West Europe cache, with the `-asia` suffix.</span></span>

### <a name="create-an-app-service-plan-in-asia"></a><span data-ttu-id="442d4-212">아시아에 App Service 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="442d4-212">Create an App Service plan in Asia</span></span>
<span data-ttu-id="442d4-213">[az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create)를 사용하여 동남 아시아 지역에 유럽 서부 계획과 동일한 S1 계층을 사용하는 두 번째 App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-213">Use [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) to create a second App Service plan in the Southeast Asia region, using the same S1 tier as the West Europe plan.</span></span>

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a><span data-ttu-id="442d4-214">아시아에 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="442d4-214">Create a web app in Asia</span></span>
<span data-ttu-id="442d4-215">[az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create)를 사용하여 두 번째 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-215">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) to create a second web app.</span></span>

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

<span data-ttu-id="442d4-216">`--name $appName-asia`는 앱에 `-asia` 접미사가 있는 유럽 서부 앱의 이름을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-216">`--name $appName-asia` gives the app the name of the West Europe app, with the `-asia` suffix.</span></span>

### <a name="configure-the-connection-string-for-redis"></a><span data-ttu-id="442d4-217">Redis에 대한 연결 문자열 구성</span><span class="sxs-lookup"><span data-stu-id="442d4-217">Configure the connection string for Redis</span></span>
<span data-ttu-id="442d4-218">[az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update)를 사용하여 웹앱에 동남 아시아 캐시에 대한 연결 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-218">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add to the web app the connection string for the Southeast Asia cache.</span></span>

<span data-ttu-id="442d4-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="442d4-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span></span>

### <a name="configure-git-deployment-for-the-asia-app"></a><span data-ttu-id="442d4-220">아시아 앱에 대한 Git 배포를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-220">Configure Git deployment for the Asia app.</span></span>
<span data-ttu-id="442d4-221">[az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git)을 사용하여 두 번째 웹앱에 대한 로컬 Git 배포를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-221">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) to configure local Git deployment for the second web app.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="442d4-222">이 명령은 다음과 같은 출력을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-222">This command gives you an output that looks like the following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="442d4-223">반환된 URL을 사용하여 로컬 리포지토리에 대한 두 번째 Git 원격을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-223">Use the returned URL to configure a second Git remote for your local repository.</span></span> <span data-ttu-id="442d4-224">다음 명령은 앞의 출력 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-224">The following command uses the preceding output example.</span></span>

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a><span data-ttu-id="442d4-225">샘플 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="442d4-225">Deploy your sample application</span></span>
<span data-ttu-id="442d4-226">`git push`를 실행하여 샘플 응용 프로그램을 두 번째 Git 원격에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-226">Run `git push` to deploy your sample application to the second Git remote.</span></span> 

```bash
git push azure-asia master
```

<span data-ttu-id="442d4-227">암호를 입력하라는 메시지가 표시되면 `az appservice web deployment user set`을 실행할 때 지정한 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-227">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-the-asia-app"></a><span data-ttu-id="442d4-228">아시아 앱 찾아보기</span><span class="sxs-lookup"><span data-stu-id="442d4-228">Browse to the Asia app</span></span>
<span data-ttu-id="442d4-229">[az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse)를 사용하여 Azure에서 실시간으로 실행 중인 앱을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-229">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to verify that your app is running live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-the-resource-id-of-the-asia-app"></a><span data-ttu-id="442d4-230">아시아 앱의 리소스 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="442d4-230">Get the resource ID of the Asia app</span></span>
<span data-ttu-id="442d4-231">[az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show)를 사용하여 동남 아시아의 웹앱 리소스 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-231">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) to get the resource ID of your web app in Southeast Asia.</span></span>

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-the-asia-app"></a><span data-ttu-id="442d4-232">아시아 앱에 대한 Traffic Manager 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="442d4-232">Add a Traffic Manager endpoint for the Asia app</span></span>
<span data-ttu-id="442d4-233">[az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create)를 사용하여 두 번째 끝점을 Traffic Manager 프로필에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-233">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) to add a second endpoint to the Traffic Manager profile.</span></span>

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-to-web-apps"></a><span data-ttu-id="442d4-234">웹앱에 하위 지역 식별자 추가</span><span class="sxs-lookup"><span data-stu-id="442d4-234">Add region identifier to web apps</span></span>
<span data-ttu-id="442d4-235">[az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update)를 사용하여 지역별 환경 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-235">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add a region-specific environment variable.</span></span>

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="442d4-236">응용 프로그램 코드는 이미 이 응용 프로그램 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-236">Your application code already uses this application setting.</span></span> <span data-ttu-id="442d4-237">`HighScaleApp\Views\Home\Index.cshtml`에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-237">Take a look at `HighScaleApp\Views\Home\Index.cshtml`.</span></span>

### <a name="complete"></a><span data-ttu-id="442d4-238">완료!</span><span class="sxs-lookup"><span data-stu-id="442d4-238">Complete!</span></span>

<span data-ttu-id="442d4-239">이제 다른 지리적 하위 지역의 브라우저에서 Traffic Manager 프로필의 URL에 액세스를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-239">Now, try to access the URL of your Traffic Manager profile from browsers in different geographical regions.</span></span> <span data-ttu-id="442d4-240">유럽의 클라이언트 브라우저는 “ASP.NET West Europe”, 아시아의 클라이언트 브라우저는 “ASP.NET Southeast Asia”가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="442d4-240">Client browsers from Europe should show "ASP.NET West Europe", and client browser from Asia should show "ASP.NET Southeast Asia."</span></span>

## <a name="more-resources"></a><span data-ttu-id="442d4-241">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="442d4-241">More resources</span></span>
