---
title: "Linux의 Web App에서 .NET Core 사용 | Microsoft Docs"
description: "Linux의 Web App에서 .NET Core를 사용합니다."
keywords: "azure app service, 웹앱, dotnet, core, linux, oss"
services: app-service
documentationCenter: 
authors: michimune, rachelappel
manager: erikre
editor: 
ms.assetid: c02959e6-7220-496a-a417-9b2147638e2e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: aelnably;wesmc;mikono;rachelap
ms.openlocfilehash: 9226dfb90e52ac2cae2cfc4af7c0705a93f56b44
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a><span data-ttu-id="e0170-104">Linux의 Azure Web App에서 .NET Core 사용</span><span class="sxs-lookup"><span data-stu-id="e0170-104">Use .NET Core in an Azure web app on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="e0170-105">Linux의[Web App](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro)은 Linux 운영 체제를 사용하여 확장성이 높은 자동 패치 웹 호스팅 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-105">[Web App](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) on Linux provides a highly scalable, self-patching web hosting service using the Linux operating system.</span></span> <span data-ttu-id="e0170-106">이 자습서에는 Linux의 Azure Web App에서 [.NET Core](https://docs.microsoft.com/aspnet/core/) 앱을 만드는 방법을 보여 주는 단계별 지침이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-106">This tutorial contains step-by-step instructions showing how to create a [.NET Core](https://docs.microsoft.com/aspnet/core/) app on Azure web app on Linux.</span></span> 

![Linux에서 Web App][10]

<span data-ttu-id="e0170-108">Mac, Windows 또는 Linux 컴퓨터를 사용하여 아래 단계를 따르면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0170-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e0170-109">Prerequisites</span></span> ##

<span data-ttu-id="e0170-110">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-110">To complete this tutorial:</span></span> 

* <span data-ttu-id="e0170-111">[.NET Core SDK](https://www.microsoft.com/net/download/core)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-111">Install the [.NET Core SDK](https://www.microsoft.com/net/download/core).</span></span>
* <span data-ttu-id="e0170-112">[Git](https://git-scm.com/downloads)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-112">Install [Git](https://git-scm.com/downloads).</span></span>

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a><span data-ttu-id="e0170-113">로컬 .NET Core 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="e0170-113">Create a local .NET Core application</span></span> ##

<span data-ttu-id="e0170-114">새 터미널 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-114">Start a new terminal session.</span></span> <span data-ttu-id="e0170-115">`hellodotnetcore`라는 디렉터리를 만들고 현재 디렉터리를 이 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-115">Create a directory named `hellodotnetcore`, and change the current directory to it.</span></span> <span data-ttu-id="e0170-116">그런 후에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-116">Then type the following:</span></span> 

```
dotnet new web
``` 

  <span data-ttu-id="e0170-117">이 명령은 현재 디렉터리 아래에 3개의 파일(*hellodotnetcore.csproj*, *Program.cs* 및 *Startup.cs*)과 하나의 빈 폴더(*wwwroot/*)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-117">This command creates three files (*hellodotnetcore.csproj*, *Program.cs*, and *Startup.cs*) and one empty folder (*wwwroot/*) under the current directory.</span></span> <span data-ttu-id="e0170-118">`.csproj` 파일의 내용은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-118">The content of `.csproj` file should look like the following:</span></span> 

```xml
  <!-- Empty lines are omitted. -->

  <Project Sdk="Microsoft.NET.Sdk.Web">
        <PropertyGroup>
        <TargetFramework>netcoreapp1.1</TargetFramework>
        </PropertyGroup>
        <ItemGroup>
        <Folder Include="wwwroot\" />
        </ItemGroup>
        <ItemGroup>
        <PackageReference Include="Microsoft.AspNetCore" Version="1.1.2" />
        </ItemGroup>
  </Project>
```

<span data-ttu-id="e0170-119">이 앱은 웹 응용 프로그램이므로 ASP.NET Core 패키지에 대한 참조가 *hellodotnetcore.csproj* 파일에 자동으로 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-119">Since this app is a web application, a reference to an ASP.NET Core package was automatically added to the *hellodotnetcore.csproj* file.</span></span> <span data-ttu-id="e0170-120">패키지의 버전 번호는 선택한 프레임워크에 따라 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-120">The version number of the package is set according to the chosen framework.</span></span> <span data-ttu-id="e0170-121">.NET Core 1.1이 사용되었으므로 이 예제에서는 ASP.NET Core 버전 1.1.2를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-121">This example is referencing ASP.NET Core version 1.1.2 because .NET Core 1.1 is used.</span></span>

## <a name="build-and-test-the-application-locally"></a><span data-ttu-id="e0170-122">로컬에서 응용 프로그램 빌드 및 테스트</span><span class="sxs-lookup"><span data-stu-id="e0170-122">Build and test the application locally</span></span> ##

<span data-ttu-id="e0170-123">다음과 같이 `dotnet restore` 명령 다음에 `dotnet run` 명령을 사용하여 .NET Core 앱을 빌드하고 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-123">You can build and run your .NET Core app with the `dotnet restore` command followed by the `dotnet run` command, as shown here:</span></span>

```
dotnet restore
dotnet run
```


<span data-ttu-id="e0170-124">응용 프로그램을 시작하면 포트에서 들어오는 요청을 수신 대기 중임을 나타내는 메시지가 이 응용 프로그램에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-124">When the application starts, it displays a message indicating the app is listening to incoming requests at a port.</span></span> 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

<span data-ttu-id="e0170-125">브라우저에서 `http://localhost:5000/`으로 이동하여 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-125">Test it by browsing to `http://localhost:5000/` with your browser.</span></span> <span data-ttu-id="e0170-126">모든 기능이 제대로 작동하는 경우 결과 텍스트로 "Hello World!"가</span><span class="sxs-lookup"><span data-stu-id="e0170-126">If everything works fine, you see "Hello World!"</span></span> <span data-ttu-id="e0170-127">표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-127">as the result text.</span></span>

![브라우저를 통한 테스트][7]

## <a name="create-a-net-core-app-in-the-azure-portal"></a><span data-ttu-id="e0170-129">Azure Portal에서 .NET Core 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="e0170-129">Create a .NET Core app in the Azure Portal</span></span> ##

<span data-ttu-id="e0170-130">먼저 비어 있는 웹앱을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-130">First you need to create an empty web app.</span></span> <span data-ttu-id="e0170-131">[Azure Portal](https://portal.azure.com/)에 로그인하고 [Linux에 새 Web App을 만듭니다](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="e0170-131">Log in to the [Azure portal](https://portal.azure.com/) and create a new [Web App on Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span></span>

![웹앱 만들기][1]

<span data-ttu-id="e0170-133">**만들기** 페이지가 열리면 웹앱에 대한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-133">When the **Create** page opens, provide details about your web app:</span></span>

![.NET Core 런타임 스택 선택][2]

<span data-ttu-id="e0170-135">다음 표를 지침으로 사용하여 **만들기** 페이지를 채운 다음 **확인**과 **만들기**를 선택하여 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-135">Use the following table as a guide to fill out the **Create** page, then select **OK** and **Create** to create the app.</span></span>

| <span data-ttu-id="e0170-136">설정</span><span class="sxs-lookup"><span data-stu-id="e0170-136">Setting</span></span>      | <span data-ttu-id="e0170-137">제안 값</span><span class="sxs-lookup"><span data-stu-id="e0170-137">Suggested value</span></span>  | <span data-ttu-id="e0170-138">설명</span><span class="sxs-lookup"><span data-stu-id="e0170-138">Description</span></span>                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| <span data-ttu-id="e0170-139">앱 이름</span><span class="sxs-lookup"><span data-stu-id="e0170-139">App name</span></span> | <span data-ttu-id="e0170-140">hellodotnetcore</span><span class="sxs-lookup"><span data-stu-id="e0170-140">hellodotnetcore</span></span>  | <span data-ttu-id="e0170-141">앱의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-141">The name of your app.</span></span> <span data-ttu-id="e0170-142">이 이름은 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-142">This name must be unique.</span></span> |
| <span data-ttu-id="e0170-143">구독</span><span class="sxs-lookup"><span data-stu-id="e0170-143">Subscription</span></span> | <span data-ttu-id="e0170-144">기존 구독 선택</span><span class="sxs-lookup"><span data-stu-id="e0170-144">Choose an existing subscription</span></span> | <span data-ttu-id="e0170-145">Azure 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-145">The Azure subscription.</span></span> |
| <span data-ttu-id="e0170-146">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="e0170-146">Resource Group</span></span> | <span data-ttu-id="e0170-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e0170-147">myResourceGroup</span></span> |  <span data-ttu-id="e0170-148">웹앱을 포함할 Azure 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-148">The Azure resource group to contain the web app.</span></span> |
| <span data-ttu-id="e0170-149">앱 서비스 계획</span><span class="sxs-lookup"><span data-stu-id="e0170-149">App Service Plan</span></span> | <span data-ttu-id="e0170-150">기존 App Service 계획 이름</span><span class="sxs-lookup"><span data-stu-id="e0170-150">Existing App Service Plan name</span></span> |  <span data-ttu-id="e0170-151">App Service 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-151">The App Service plan.</span></span>  |
| <span data-ttu-id="e0170-152">컨테이너 구성</span><span class="sxs-lookup"><span data-stu-id="e0170-152">Configure Container</span></span> | <span data-ttu-id="e0170-153">.NET Core 1.1</span><span class="sxs-lookup"><span data-stu-id="e0170-153">.NET Core 1.1</span></span> | <span data-ttu-id="e0170-154">이 웹앱에 대한 컨테이너 형식, 즉 기본 제공, Docker 또는 개인 레지스트리입니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-154">The type of container for this web app: Built-in, Docker, or Private registry.</span></span> |
| <span data-ttu-id="e0170-155">이미지 원본</span><span class="sxs-lookup"><span data-stu-id="e0170-155">Image source</span></span>  | <span data-ttu-id="e0170-156">기본 제공</span><span class="sxs-lookup"><span data-stu-id="e0170-156">Built-in</span></span>  |  <span data-ttu-id="e0170-157">이미지의 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-157">The source of the image.</span></span> |
| <span data-ttu-id="e0170-158">런타임 스택</span><span class="sxs-lookup"><span data-stu-id="e0170-158">Runtime Stack</span></span>  | <span data-ttu-id="e0170-159">.NET Core 1.1</span><span class="sxs-lookup"><span data-stu-id="e0170-159">.NET Core 1.1</span></span>  | <span data-ttu-id="e0170-160">런타임 스택 및 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-160">The runtime stack and version.</span></span>  |

## <a name="deploy-your-application-via-git"></a><span data-ttu-id="e0170-161">Git를 통한 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="e0170-161">Deploy your application via Git</span></span> ##

<span data-ttu-id="e0170-162">Git를 사용하여 .NET Core 응용 프로그램을 Linux의 Azure App Service Web App에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-162">Use Git to deploy the .NET Core application to Azure App Service Web App on Linux.</span></span>

<span data-ttu-id="e0170-163">새 Azure 웹앱에는 이미 Git 배포가 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-163">The new Azure web app already has Git deployment configured.</span></span> <span data-ttu-id="e0170-164">웹앱 이름을 삽입한 후 다음 URL로 이동하여 Git 배포 URL을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-164">You will find the Git deployment URL by navigating to the following URL after inserting your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

<span data-ttu-id="e0170-165">Git URL은 웹앱 이름에 따라 다음과 같은 형식을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-165">The Git URL has the following form based on your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

<span data-ttu-id="e0170-166">다음 명령을 실행하여 Azure 웹앱에 로컬 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-166">Run the following commands to deploy the local application to your Azure web app:</span></span> 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="e0170-167">응용 프로그램의 소스 파일을 Azure로 푸시할 때 응용 프로그램이 클라우드에 빌드되므로 *bin/* 또는 *obj/* 디렉터리 아래에 모든 파일을 푸시할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-167">You don't need to push any files under *bin/* or *obj/* directories because your application is built in the cloud when the application's source files are pushed to Azure.</span></span> <span data-ttu-id="e0170-168">빌드 프로세스가 완료되면 이진 파일이 응용 프로그램 디렉터리 */home/site/wwwroot/*에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-168">After the build process is complete, binary files are copied into the application's directory at */home/site/wwwroot/*.</span></span>

<span data-ttu-id="e0170-169">원격 배포 작업이 성공을 보고하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-169">Confirm that the remote deployment operations report success.</span></span> <span data-ttu-id="e0170-170">패키지 확인 및 빌드 프로세스가 클라우드에서 실행되므로 푸시 작업에 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-170">Push operations may take a while since package resolution and build process run in the cloud.</span></span> <span data-ttu-id="e0170-171">파일이 복사되었음을 포함하여 몇 가지 상태 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-171">You will see several status messages, including ones stating that files have been copied.</span></span> <span data-ttu-id="e0170-172">출력은 다음과 비슷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-172">The output should look similar to the following:</span></span>

```bash
/* some output has been removed for brevity */
remote: Copying file: 'System.Net.Websockets.dll' 
remote: Copying file: 'System.Runtime.CompilerServices.Unsafe.dll' 
remote: Copying file: 'System.Runtime.Serialization.Primitives.dll' 
remote: Copying file: 'System.Text.Encodings.Web.dll' 
remote: Copying file: 'hellodotnetcore.deps.json' 
remote: Copying file: 'hellodotnetcore.dll' 
remote: Omitting next output lines...
remote: Finished successfully.
remote: Running post deployment commands...
remote: Deployment successful.
To https://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

<span data-ttu-id="e0170-173">배포가 완료되면 웹앱을 다시 시작하여 배포를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-173">Once the deployment has completed, restart your web app for the deployment to take effect.</span></span> <span data-ttu-id="e0170-174">이렇게 하려면 Azure Portal로 이동하여 웹앱의 **개요** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-174">To do this, go to the Azure portal and navigate to the **Overview** page of your web app.</span></span> <span data-ttu-id="e0170-175">해당 페이지에서 **다시 시작** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-175">Select the **Restart** button in the page.</span></span> <span data-ttu-id="e0170-176">팝업 창이 표시되면 **예**를 선택하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-176">When a popup window shows up, select **Yes** to confirm.</span></span> <span data-ttu-id="e0170-177">다음과 같이 웹앱을 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0170-177">You can then browse your web app, as shown here:</span></span>

![Linux의 Azure App Service에 배포된 .NET Core 앱 검색][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="e0170-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e0170-179">Next steps</span></span>
* [<span data-ttu-id="e0170-180">Linux의 Azure App Service Web App에 대한 FAQ</span><span class="sxs-lookup"><span data-stu-id="e0170-180">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
