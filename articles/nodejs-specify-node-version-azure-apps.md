---
title: "Node.js 버전 지정"
description: "Azure 웹 사이트 및 클라우드 서비스에서 사용하는 Node.js의 버전을 지정하는 방법에 대해 알아봅니다."
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d0e15278-2ab4-4ec8-8256-913839c6d5ef
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 89627e6a877c9f65a5216c55f58f1c707ea25d44
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a><span data-ttu-id="7591f-103">Azure 응용 프로그램에서 Node.js 버전 지정</span><span class="sxs-lookup"><span data-stu-id="7591f-103">Specifying a Node.js version in an Azure application</span></span>
<span data-ttu-id="7591f-104">Node.js 응용 프로그램을 호스트하는 경우 응용 프로그램에서 특정 버전의 Node.js를 사용하는지 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-104">When hosting a Node.js application, you may want to ensure that your application uses a specific version of Node.js.</span></span> <span data-ttu-id="7591f-105">Azure에 호스트되는 응용 프로그램에 대해 이 작업을 수행하는 여러 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-105">There are several ways to accomplish this for applications hosted on Azure.</span></span>

## <a name="default-versions"></a><span data-ttu-id="7591f-106">기본 버전</span><span class="sxs-lookup"><span data-stu-id="7591f-106">Default versions</span></span>
<span data-ttu-id="7591f-107">Azure에서 제공하는 Node.js 버전은 지속적으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-107">The Node.js versions provided by Azure are constantly updated.</span></span> <span data-ttu-id="7591f-108">별도로 지정하지 않는 한, `WEBSITE_NODE_DEFAULT_VERSION` 환경 변수에 지정된 기본 버전이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-108">Unless otherwise specified, the default version that is specified in the `WEBSITE_NODE_DEFAULT_VERSION` environment variable will be used.</span></span> <span data-ttu-id="7591f-109">기본값을 재정의하려면, 이 문서의 다음 섹션에 나오는 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-109">To override this default value, follow the steps in following sections of this article</span></span>

> [!NOTE]
> <span data-ttu-id="7591f-110">Azure 클라우드 서비스(웹 또는 작업자 역할)에서 응용 프로그램을 호스트하며 응용 프로그램을 처음 배포하는 것이면 Azure는 Azure에서 사용 가능한 기본 버전 중 하나와 일치할 경우 개발 환경에 설치한 것과 동일한 버전의 Node.js를 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-110">If you are hosting your application in an Azure Cloud Service (web or worker role,) and it is the first time you have deployed the application, Azure will attempt to use the same version of Node.js as you have installed on your development environment if it matches one of the default versions available on Azure.</span></span>
>
>

## <a name="versioning-with-packagejson"></a><span data-ttu-id="7591f-111">package.json을 사용하여 버전 관리</span><span class="sxs-lookup"><span data-stu-id="7591f-111">Versioning with package.json</span></span>
<span data-ttu-id="7591f-112">**package.json** 파일에 다음을 추가하여 사용할 Node.js의 버전을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-112">You can specify the version of Node.js to be used by adding the following to your **package.json** file:</span></span>

    "engines":{"node":version}

<span data-ttu-id="7591f-113">여기서 *version* 은 사용할 특정 버전 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-113">Where *version* is the specific version number to use.</span></span> <span data-ttu-id="7591f-114">다음과 같이 버전에 보다 복잡한 조건을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-114">You can specify more complex conditions for version, such as:</span></span>

    "engines":{"node": "0.6.22 || 0.8.x"}

<span data-ttu-id="7591f-115">0.6.22는 호스팅 환경에서 사용 가능한 버전 중 하나가 아니므로 사용 가능한 0.8 시리즈의 가장 높은 버전인 0.8.4가 대신 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-115">Since 0.6.22 is not one of the versions available in the hosting environment, the highest version of the 0.8 series that is available will be used instead - 0.8.4.</span></span>

## <a name="versioning-websites-with-app-settings"></a><span data-ttu-id="7591f-116">앱 설정을 사용하여 웹 사이트 버전 관리</span><span class="sxs-lookup"><span data-stu-id="7591f-116">Versioning Websites with App Settings</span></span>
<span data-ttu-id="7591f-117">웹 사이트에서 응용 프로그램을 호스트하는 경우 환경 변수 **WEBSITE_NODE_DEFAULT_VERSION**을 원하는 버전으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-117">If you are hosting the application in a Website, you can set the environment variable **WEBSITE_NODE_DEFAULT_VERSION** to the desired version.</span></span>

## <a name="versioning-cloud-services-with-powershell"></a><span data-ttu-id="7591f-118">PowerShell을 사용하여 클라우드 서비스 버전 관리</span><span class="sxs-lookup"><span data-stu-id="7591f-118">Versioning Cloud Services with PowerShell</span></span>
<span data-ttu-id="7591f-119">클라우드 서비스에서 응용 프로그램을 호스트하고 Azure PowerShell을 사용하여 응용 프로그램을 배포하는 경우 **Set-AzureServiceProjectRole** PowerShell cmdlet을 사용하여 기본 Node.js 버전을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-119">If you are hosting the application in a Cloud Service, and are deploying the application using Azure PowerShell, you can override the default Node.js version by using the **Set-AzureServiceProjectRole** PowerShell cmdlet.</span></span> <span data-ttu-id="7591f-120">예:</span><span class="sxs-lookup"><span data-stu-id="7591f-120">For example:</span></span>

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

<span data-ttu-id="7591f-121">위의 문에서 매개 변수는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-121">Note the parameters in the above statement are case-sensitive.</span></span>  <span data-ttu-id="7591f-122">역할의 **package.json**에서 **engines** 속성을 검사하여 올바른 버전의 Node.js가 선택되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-122">You can verify the correct version of Node.js has been selected by checking the **engines** property in your role's **package.json**.</span></span>

<span data-ttu-id="7591f-123">**Get-AzureServiceProjectRoleRuntime** 을 사용하여 클라우드 서비스로 호스트된 응용 프로그램에 사용 가능한 Node.js 버전 목록을 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-123">You can also use the **Get-AzureServiceProjectRoleRuntime** to retrieve a list of Node.js versions available for applications hosted as a Cloud Service.</span></span>  <span data-ttu-id="7591f-124">프로젝트에서 사용하는 Node.js 버전이 목록에 있는지 항상 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-124">Always verify the version of Node.js your project depends on is in this list.</span></span>

## <a name="using-a-custom-version-with-azure-websites"></a><span data-ttu-id="7591f-125">Azure 웹 사이트에서 사용자 지정 버전 사용</span><span class="sxs-lookup"><span data-stu-id="7591f-125">Using a custom version with Azure Websites</span></span>
<span data-ttu-id="7591f-126">Azure는 Node.js의 기본 버전을 여러 개 제공하지만 기본적으로 제공되지 않는 버전을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-126">While Azure provides several default versions of Node.js, you may want to use a version that is not provided by default.</span></span> <span data-ttu-id="7591f-127">응용 프로그램이 Azure 웹 사이트로 호스트된 경우 **iisnode.yml** 파일을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-127">If your application is hosted as an Azure Website, you can accomplish this by using the **iisnode.yml** file.</span></span> <span data-ttu-id="7591f-128">다음 단계에서는 Azure 웹 사이트에서 사용자 지정 버전의 Node.Js를 사용하는 프로세스를 단계별로 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-128">The following steps walk through the process of using a custom version of Node.Js with an Azure Website:</span></span>

1. <span data-ttu-id="7591f-129">새 디렉터리를 만든 후 디렉터리 내에 **server.js** 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-129">Create a new directory, and then create a **server.js** file within the directory.</span></span> <span data-ttu-id="7591f-130">**server.js** 파일에는 다음이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-130">The **server.js** file should contain the following:</span></span>

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    <span data-ttu-id="7591f-131">웹 사이트를 검색할 때 사용되는 Node.js 버전이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-131">This will display the Node.js version being used when you browse the website.</span></span>
2. <span data-ttu-id="7591f-132">새로운 웹 사이트를 만들고 사이트 이름을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-132">Create a new Website and note the name of the site.</span></span> <span data-ttu-id="7591f-133">예를 들어 다음 코드는 [Azure 명령줄 도구] 를 사용하여 **mywebsite**라는 새 Azure 웹 사이트를 만든 후 웹 사이트에 Git 리포지토리를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-133">For example, the following uses the [Azure Command-line tools] to create a new Azure Website named **mywebsite**, and then enable a Git repository for the website.</span></span>

        azure site create mywebsite --git
3. <span data-ttu-id="7591f-134">**server.js** 파일이 포함된 디렉터리의 자식으로 **bin** 디렉터리를 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-134">Create a new directory named **bin** as a child of the directory containing the **server.js** file.</span></span>
4. <span data-ttu-id="7591f-135">응용 프로그램과 함께 사용할 특정 버전의 **node.exe** (Windows 버전)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-135">Download the specific version of **node.exe** (the Windows version) that you wish to use with your application.</span></span> <span data-ttu-id="7591f-136">예를 들어 다음 코드는 **curl** 을 사용하여 버전 0.8.1을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-136">For example, the following uses **curl** to download version 0.8.1:</span></span>

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    <span data-ttu-id="7591f-137">이전에 만든 **bin** 폴더에 **node.exe** 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-137">Save the **node.exe** file into the **bin** folder created previously.</span></span>
5. <span data-ttu-id="7591f-138">**server.js** 파일과 동일한 디렉터리에 **iisnode.yml** 파일을 만든 후 **iisnode.yml** 파일에 다음 콘텐츠를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-138">Create an **iisnode.yml** file in the same directory as the **server.js** file, and then add the following content to the **iisnode.yml** file:</span></span>

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    <span data-ttu-id="7591f-139">이 경로는 Azure 웹 사이트에 응용 프로그램을 게시한 후 프로젝트 내의 **node.exe** 파일이 있는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-139">This path is where the **node.exe** file within your project will be located once you have published your application to the Azure Website.</span></span>
6. <span data-ttu-id="7591f-140">응용 프로그램을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-140">Publish your application.</span></span> <span data-ttu-id="7591f-141">예를 들어 이전에 --git 매개 변수를 사용하여 새로운 웹 사이트를 만들었으므로 다음 명령은 로컬 Git 리포지토리에 응용 프로그램 파일을 추가한 후 웹 사이트 리포지토리에 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-141">For example, since I created a new website with the --git parameter earlier, the following commands will add the application files to my local Git repository, and then push them to the website repository:</span></span>

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    <span data-ttu-id="7591f-142">응용 프로그램이 게시된 후 브라우저에서 웹 사이트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-142">After the application has published, open the website in a browser.</span></span> <span data-ttu-id="7591f-143">"Hello from Azure running node version: v0.8.1"이라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-143">You should see a message stating "Hello from Azure running node version: v0.8.1".</span></span>

## <a name="next-steps"></a><span data-ttu-id="7591f-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7591f-144">Next Steps</span></span>
<span data-ttu-id="7591f-145">지금까지 응용 프로그램에서 사용되는 Node.js 버전을 지정하는 방법을 배웠습니다. 이제 [모듈 작업] 방법, [Node.js 웹 사이트 빌드 및 배포](app-service-web/app-service-web-get-started-nodejs.md) 방법, [Mac 및 Linux에서 Azure 명령줄 도구를 사용하는 방법]을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7591f-145">Now that you understand how to specify the version of Node.js used by your application, learn how to [work with modules], [build and deploy a Node.js Web Site](app-service-web/app-service-web-get-started-nodejs.md), and [How to use the Azure Command-Line Tools for Mac and Linux].</span></span>

<span data-ttu-id="7591f-146">자세한 내용은 [Node.js 개발자 센터](https://azure.microsoft.com/develop/nodejs/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7591f-146">For more information, see the [Node.js Developer Center](https://azure.microsoft.com/develop/nodejs/).</span></span>

<span data-ttu-id="7591f-147">[Mac 및 Linux에서 Azure 명령줄 도구를 사용하는 방법]:cli-install-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="7591f-147">[How to use the Azure Command-Line Tools for Mac and Linux]:cli-install-nodejs.md</span></span>
<span data-ttu-id="7591f-148">[Azure 명령줄 도구]:cli-install-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="7591f-148">[Azure Command-line tools]:cli-install-nodejs.md</span></span>
<span data-ttu-id="7591f-149">[모듈 작업]: nodejs-use-node-modules-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="7591f-149">[work with modules]: nodejs-use-node-modules-azure-apps.md</span></span>
[build and deploy a Node.js Web Site]: app-service-web/app-service-web-get-started-nodejs.md
