---
title: "Azure App Service에 Sails.js 웹앱 배포 | Microsoft Docs"
description: "Azure 앱 서비스에서 Node.js 응용 프로그램을 배포하는 방법을 알아봅니다. 이 자습서에서는 Sails.js 웹앱을 배포하는 방법을 보여 줍니다."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 8877ddc8-1476-45ae-9e7f-3c75917b4564
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: e36fc5f5273f98c3cca91973db9910f32443ec7c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-a-sailsjs-web-app-to-azure-app-service"></a><span data-ttu-id="7603a-104">Azure 앱 서비스에 Sails.js 웹앱을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-104">Deploy a Sails.js web app to Azure App Service</span></span>
<span data-ttu-id="7603a-105">이 자습서에서는 Azure 앱 서비스에 Sails.js 앱을 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-105">This tutorial shows you how to deploy a Sails.js app to Azure App Service.</span></span> <span data-ttu-id="7603a-106">프로세스를 통해 앱 서비스에서 실행할 Node.js 앱 구성 방법에 대한 일반적인 지식을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-106">In the process, you can glean some general knowledge on how to configure your Node.js app to run in App Service.</span></span>

<span data-ttu-id="7603a-107">여기에서는 다음과 같은 유용한 기술을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-107">Here, you will learn useful skills like:</span></span>

* <span data-ttu-id="7603a-108">App Service에서 실행되는 Sails.js 앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-108">Configure a Sails.js app run in App Service.</span></span>
* <span data-ttu-id="7603a-109">명령줄에서 App Service에 앱을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-109">Deploy an app to App Service from the command line.</span></span>
* <span data-ttu-id="7603a-110">배포 문제를 해결하기 위해 stderr 및 stdout 로그를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-110">Read stderr and stdout logs to troubleshoot any deployment issues.</span></span>
* <span data-ttu-id="7603a-111">소스 제어 외부의 환경 변수를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-111">Store environment variables outside of source control.</span></span>
* <span data-ttu-id="7603a-112">앱에서 Azure 환경 변수에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-112">Access Azure environment variables from your app.</span></span>
* <span data-ttu-id="7603a-113">데이터베이스에 연결합니다(MongoDB).</span><span class="sxs-lookup"><span data-stu-id="7603a-113">Connect to a database (MongoDB).</span></span>

<span data-ttu-id="7603a-114">Sails.js에 대한 실무 지식이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-114">You should have working knowledge of Sails.js.</span></span> <span data-ttu-id="7603a-115">이 자습서는 일반적으로 Sail.js의 실행과 관련된 문제를 해결하는 데 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-115">This tutorial is not intended to help you with issues related to running Sail.js in general.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="7603a-116">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="7603a-116">CLI versions to complete the task</span></span>

<span data-ttu-id="7603a-117">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-117">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="7603a-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) - 클래식 및 리소스 관리 배포 모델용 CLI</span><span class="sxs-lookup"><span data-stu-id="7603a-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span>
- <span data-ttu-id="7603a-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) - 리소스 관리 배포 모델용 차세대 CLI</span><span class="sxs-lookup"><span data-stu-id="7603a-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7603a-120">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7603a-120">Prerequisites</span></span>
* [<span data-ttu-id="7603a-121">Node.JS</span><span class="sxs-lookup"><span data-stu-id="7603a-121">Node.js</span></span>](https://nodejs.org/)
* [<span data-ttu-id="7603a-122">Sails.js</span><span class="sxs-lookup"><span data-stu-id="7603a-122">Sails.js</span></span>](http://sailsjs.org/get-started)
* [<span data-ttu-id="7603a-123">Git</span><span class="sxs-lookup"><span data-stu-id="7603a-123">Git</span></span>](http://www.git-scm.com/downloads)
* [<span data-ttu-id="7603a-124">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7603a-124">Azure CLI 2.0</span></span>](/cli/azure/install-az-cli2)
* <span data-ttu-id="7603a-125">Microsoft Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="7603a-125">A Microsoft Azure account.</span></span> <span data-ttu-id="7603a-126">계정이 없는 경우 [무료 평가판을 등록](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)하거나 [Visual Studio 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-126">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="7603a-127">Azure 계정 없이 [App Service를 체험](https://azure.microsoft.com/try/app-service/)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-127">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="7603a-128">시작 앱을 만들고 최대 한 시간 동안 해당 앱을 사용하여 재생합니다. -- 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-128">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a><span data-ttu-id="7603a-129">1단계: 로컬로 Sails.js 앱 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="7603a-129">Step 1: Create and configure a Sails.js app locally</span></span>
<span data-ttu-id="7603a-130">먼저 다음 단계를 수행하여 개발 환경에서 기본 Sails.js 앱을 신속하게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-130">First, quickly create a default Sails.js app in your development environment by following these steps:</span></span>

1. <span data-ttu-id="7603a-131">선택한 명령줄 터미널을 열고 작업 디렉터리로 `CD` 합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-131">Open the command-line terminal of your choice and `CD` to a working directory.</span></span>
2. <span data-ttu-id="7603a-132">Sails.js 앱을 만들고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-132">Create a Sails.js app and run it:</span></span>

        sails new <app_name>
        cd <app_name>
        sails lift

    <span data-ttu-id="7603a-133">기본 홈 페이지 http://localhost:1377 로 이동할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-133">Make sure you can navigate to the default home page at http://localhost:1377.</span></span>

1. <span data-ttu-id="7603a-134">다음으로 Azure에 대한 로깅을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-134">Next, enable logging for Azure.</span></span> <span data-ttu-id="7603a-135">루트 디렉터리에서 `iisnode.yml`이라는 파일을 만들고 다음 두 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-135">In your root directory, create a file called `iisnode.yml` and add the following two lines:</span></span>

        loggingEnabled: true
        logDirectory: iisnode

    <span data-ttu-id="7603a-136">이제 Azure App Service가 Node.js 앱을 실행하는 데 사용하는 [iisnode](https://github.com/tjanczuk/iisnode) 서버에 대한 로깅이 사용하도록 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-136">Logging is now enabled for the [iisnode](https://github.com/tjanczuk/iisnode) server that Azure App Service uses to run Node.js apps.</span></span> 
    <span data-ttu-id="7603a-137">작동 방식에 대한 자세한 내용은 [Azure App Service에서 Node.js 웹앱을 디버그하는 방법](web-sites-nodejs-debug.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7603a-137">For more information on how this works, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

2. <span data-ttu-id="7603a-138">다음으로 Azure 환경 변수를 사용하도록 Sails.js 앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-138">Next, configure the Sails.js app to use Azure environment variables.</span></span> <span data-ttu-id="7603a-139">프로덕션 환경을 구성하기 위해 config/env/production.js를 열고 `port` 및 `hookTimeout`을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-139">Open config/env/production.js to configure your production environment, and set `port` and `hookTimeout`:</span></span>

        module.exports = {

            // Use process.env.port to handle web requests to the default HTTP port
            port: process.env.port,
            // Increase hooks timout to 30 seconds
            // This avoids the Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    <span data-ttu-id="7603a-140">이러한 구성 설정에 대한 설명서는 [Sails.js 설명서](http://sailsjs.org/documentation/reference/configuration/sails-config)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-140">You can find documentation for these configuration settings in the  [Sails.js Documentation](http://sailsjs.org/documentation/reference/configuration/sails-config).</span></span>

4. <span data-ttu-id="7603a-141">다음으로 사용할 Node.js 버전을 하드 코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-141">Next, hardcode the Node.js version you want to use.</span></span> <span data-ttu-id="7603a-142">package.json에서 다음 `engines` 속성을 추가하여 Node.js를 원하는 버전으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-142">In package.json, add the following `engines` property to set the Node.js version to one that we want.</span></span>

        "engines": {
            "node": "6.9.1"
        },

5. <span data-ttu-id="7603a-143">마지막으로 Git 저장소를 초기화하고 파일을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-143">Finally, initialize a Git repository and commit your files.</span></span> <span data-ttu-id="7603a-144">응용 프로그램 루트(package.json 위치)에서 다음 Git 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-144">In the application root (where package.json is), run the following Git commands:</span></span>

        git init
        git add .
        git commit -m "<your commit message>"

<span data-ttu-id="7603a-145">코드를 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-145">Your code is ready to be deployed.</span></span> 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a><span data-ttu-id="7603a-146">2단계: Azure 앱 만들기 및 Sails.js 배포</span><span class="sxs-lookup"><span data-stu-id="7603a-146">Step 2: Create an Azure app and deploy Sails.js</span></span>

<span data-ttu-id="7603a-147">다음으로 Azure에 App Service 리소스를 만들고 Sails.js 앱을 해당 리소스에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-147">Next, create the App Service resource in Azure and deploy your Sails.js app to it.</span></span>

1. <span data-ttu-id="7603a-148">다음과 같이 Azure에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-148">log in to Azure like so:</span></span>

        az login

    <span data-ttu-id="7603a-149">프롬프트를 따라 Azure 구독을 보유하고 있는 Microsoft 계정을 사용하여 브라우저에 로그인을 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-149">Follow the prompt to continue the login in a browser with a Microsoft account that has your Azure subscription.</span></span>

3. <span data-ttu-id="7603a-150">App Service의 배포 사용자를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-150">Set the deployment user for App Service.</span></span> <span data-ttu-id="7603a-151">나중에 이러한 자격 증명을 사용하여 코드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-151">You will deploy code using these credentials later.</span></span>
   
        az appservice web deployment user set --user-name <username> --password <password>

3. <span data-ttu-id="7603a-152">[리소스 그룹](../azure-resource-manager/resource-group-overview.md)을 만들고 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-152">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with a name.</span></span> <span data-ttu-id="7603a-153">이 Node.js 자습서에서는 실제로 무엇인지 알 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-153">For this Node.js tutorial, you don't really need to know what it is.</span></span>

        az group create --location "<location>" --name my-sailsjs-app-group

    <span data-ttu-id="7603a-154">`<location>`에 사용할 수 있는 가능한 값을 보려면 `az appservice list-locations` CLI 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-154">To see what possible values you can use for `<location>`, use the `az appservice list-locations` CLI command.</span></span>

3. <span data-ttu-id="7603a-155">"무료" [App Service 계획](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)을 만들고 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-155">Create a "FREE" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) with a name.</span></span> <span data-ttu-id="7603a-156">이 Node.js 자습서에서는 이 계획에서 웹앱에 대한 요금이 부과되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-156">For this Node.js tutorial, just know that you won't be charged for web apps in this plan.</span></span>

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. <span data-ttu-id="7603a-157">`<app_name>`에 고유한 이름이 있는 새 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-157">Create a new web app with a unique name in `<app_name>`.</span></span>

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a><span data-ttu-id="7603a-158">3단계: Sails.js 앱 구성 및 배포</span><span class="sxs-lookup"><span data-stu-id="7603a-158">Step 3: Configure and deploy your Sails.js app</span></span>

1. <span data-ttu-id="7603a-159">다음 명령을 사용하여 새 웹앱에 대한 로컬 Git 배포를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-159">Configure local Git deployment for your new web app with the following command:</span></span>

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="7603a-160">다음과 같은 JSON 출력을 받으며, 이는 원격 Git 리포지토리가 구성되었음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-160">You will get a JSON output like this, which means that the remote Git repository is configured:</span></span>

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. <span data-ttu-id="7603a-161">JSON의 URL을 로컬 리포지토리의 Git 원격으로 추가합니다(간단히 `azure`라고 함).</span><span class="sxs-lookup"><span data-stu-id="7603a-161">Add the URL in the JSON as a Git remote for your local repository (called `azure` for simplicity).</span></span>

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. <span data-ttu-id="7603a-162">샘플 코드를 `azure` Git 원격에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-162">Deploy your sample code to the `azure` Git remote.</span></span> <span data-ttu-id="7603a-163">메시지가 표시되면 이전에 구성한 배포 자격 증명을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-163">When prompted, use the deployment credentials you configured earlier.</span></span>

        git push azure master

7. <span data-ttu-id="7603a-164">마지막으로 브라우저에서 라이브 Azure 앱을 실행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-164">Finally, just launch your live Azure app in the browser:</span></span>

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="7603a-165">이제 동일한 Sails.js 홈페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-165">You should now see the same Sails.js home page.</span></span>

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a><span data-ttu-id="7603a-166">배포 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7603a-166">Troubleshoot your deployment</span></span>
<span data-ttu-id="7603a-167">Sails.js 응용 프로그램이 앱 서비스에서 어떤 이유로 실패하면 문제 해결을 위해 stderr 로그를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-167">If your Sails.js application fails for some reason in App Service, find the stderr logs to help troubleshoot it.</span></span>
<span data-ttu-id="7603a-168">자세한 내용은 [Azure App Service에서 Node.js 웹앱을 디버그하는 방법](web-sites-nodejs-debug.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7603a-168">For more information, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>
<span data-ttu-id="7603a-169">앱이 성공적으로 시작된 경우 stdout 로그에 익숙한 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-169">If the app has started successfully, the stdout log should show you the familiar message:</span></span>

                   .-..-.
    
       Sails              <|    .-..-.
       v0.12.11            |\
                          /|.\
                         / || \
                       ,'  |'  \
                    .-'.-==|/_--'
                    `--'-------' 
       __---___--___---___--___---___--___
     ____---___--___---___--___---___--___-__

    Server lifted in `D:\home\site\wwwroot`
    To see your app, visit http://localhost:\\.\pipe\c775303c-0ebc-4854-8ddd-2e280aabccac
    To shut down Sails, press <CTRL> + C at any time.

<span data-ttu-id="7603a-170">[config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) 파일에서 stdout 로그의 세분화 수준을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-170">You can control granularity of the stdout logs in the [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) file.</span></span>

## <a name="connect-to-a-database-in-azure"></a><span data-ttu-id="7603a-171">Azure의 데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="7603a-171">Connect to a database in Azure</span></span>
<span data-ttu-id="7603a-172">Azure 데이터베이스에 연결하려면 Azure에 Azure SQL Database, MySQL, MongoDB, Azure (Redis) Cache 등 원하는 데이터베이스를 만들고 해당하는 [데이터 저장소 어댑터](https://github.com/balderdashy/sails#compatibility) 를 사용하여 이 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-172">To connect to a database in Azure, you create the database of your choice in Azure, such as Azure SQL Database, MySQL, MongoDB, Azure (Redis) Cache, etc., and use the corresponding [datastore adapter](https://github.com/balderdashy/sails#compatibility) to connect to it.</span></span> <span data-ttu-id="7603a-173">이 섹션의 단계에서는 MongoDB 클라이언트 연결을 지원할 수 있는 [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) 데이터베이스를 사용하여 MongoDB에 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-173">The steps in this section show you how to connect to MongoDB by using an [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) database, which can support MongoDB client connections.</span></span>

1. <span data-ttu-id="7603a-174">[MongoDB 프로토콜 지원을 사용하는 Cosmos DB 계정을 만듭니다](../documentdb/documentdb-create-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="7603a-174">[Create a Cosmos DB account with MongoDB protocol support](../documentdb/documentdb-create-mongodb-account.md).</span></span>
2. <span data-ttu-id="7603a-175">[Cosmos DB 컬렉션 및 데이터베이스를 만듭니다](../documentdb/documentdb-create-collection.md).</span><span class="sxs-lookup"><span data-stu-id="7603a-175">[Create a Cosmos DB collection and database](../documentdb/documentdb-create-collection.md).</span></span> <span data-ttu-id="7603a-176">컬렉션의 이름은 중요하지 않지만 Sails.js에서 연결할 때 데이터베이스의 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-176">The name of the collection doesn't matter, but you need the name of the database when you connect from Sails.js.</span></span>
3. <span data-ttu-id="7603a-177">[Cosmos DB 데이터베이스에 대한 연결 정보를 찾습니다](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="7603a-177">[Find the connection information for your Cosmos DB database](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span></span>
2. <span data-ttu-id="7603a-178">명령줄 터미널에서 MongoDB 어댑터를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-178">From your command-line terminal, install the MongoDB adapter:</span></span>

        npm install sails-mongo --save

3. <span data-ttu-id="7603a-179">config/connections.js를 열고 목록에 다음 연결 개체를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-179">Open config/connections.js and add the following connection object to the list:</span></span>

        docDbMongo: {
            adapter: 'sails-mongo',
            user: process.env.dbuser,
            password: process.env.dbpassword,
            host: process.env.dbhost,
            port: process.env.dbport,
            database: process.env.dbname,
            ssl: true
        },

    > [!NOTE] 
    > <span data-ttu-id="7603a-180">`ssl: true` 옵션은 [Cosmos DB에서 필요](../cosmos-db/connect-mongodb-account.md#connection-string-requirements)하기 때문에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-180">The `ssl: true` option is important because [Cosmos DB requires it](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 
    >
    >

4. <span data-ttu-id="7603a-181">각 환경 변수(`process.env.*`)의 경우 App Service에서 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-181">For each environment variable (`process.env.*`), you need to set it in App Service.</span></span> <span data-ttu-id="7603a-182">이렇게 하려면 터미널에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-182">To do this, run the following commands from your terminal.</span></span> <span data-ttu-id="7603a-183">Cosmos DB에 대한 연결 정보를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-183">Use the connection information for your Cosmos DB.</span></span>

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="7603a-184">Azure 앱 설정에 설정 내용을 적용하면 중요한 데이터의 소스를 제어할 수 없게 됩니다(Git).</span><span class="sxs-lookup"><span data-stu-id="7603a-184">Putting your settings in Azure app settings keeps sensitive data out of your source control (Git).</span></span> <span data-ttu-id="7603a-185">다음으로, 동일한 연결 정보를 사용하도록 개발 환경을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-185">Next, you will configure your development environment to use the same connection information.</span></span>
5. <span data-ttu-id="7603a-186">config/local.js를 열고 다음 연결 개체를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-186">Open config/local.js and add the following connections object:</span></span>

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    <span data-ttu-id="7603a-187">이 구성은 config/connections.js 파일에서 로컬 환경에 대한 설정을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-187">This configuration overrides the settings in your config/connections.js file for the local environment.</span></span> <span data-ttu-id="7603a-188">이 파일은 프로젝트에서 기본 .gitignore에 의해 제외되므로 Git에 저장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-188">This file is excluded by the default .gitignore in your project, so it will not be stored in Git.</span></span> <span data-ttu-id="7603a-189">이제 Azure Web App 및 로컬 개발 환경 둘 다에서 Cosmos DB(MongoDB) 데이터베이스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-189">Now, you are able to connect to your Cosmos DB (MongoDB) database both from your Azure web app and from your local development environment.</span></span>
6. <span data-ttu-id="7603a-190">config/env/production.js를 열어 프로덕션 환경을 구성하고 다음 `models` 개체를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-190">Open config/env/production.js to configure your production environment, and add the following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. <span data-ttu-id="7603a-191">config/env/development.js를 열어 개발 환경을 구성하고 다음 `models` 개체를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-191">Open config/env/development.js to configure your development environment, and add the following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    <span data-ttu-id="7603a-192">`migrate: 'alter'`를 통해 데이터베이스 마이그레이션 기능을 사용하여 데이터베이스 컬렉션 또는 테이블을 쉽게 만들고 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-192">`migrate: 'alter'` lets you use database migration features to create and update database collections or tables easily.</span></span> <span data-ttu-id="7603a-193">그러나 Sails.js에서는 프로덕션 환경에서 `migrate: 'alter'` 사용을 허용하지 않으므로 Azure(프로덕션) 환경에 `migrate: 'safe'`가 사용됩니다([Sails.js 설명서](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings) 참조).</span><span class="sxs-lookup"><span data-stu-id="7603a-193">However, `migrate: 'safe'` is used for your Azure (production) environment because Sails.js does not allow you to use `migrate: 'alter'` in a production environment (see [Sails.js Documentation](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span></span>
8. <span data-ttu-id="7603a-194">터미널에서 평소처럼 Sails.js [청사진 AP](http://sailsjs.org/documentation/concepts/blueprints)I를 [생성](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate)한 다음 `sails lift`을(를) 실행하여 Sails.js 데이터베이스 마이그레이션을 통해 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-194">From the terminal, [generate](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) a Sails.js [blueprint API](http://sailsjs.org/documentation/concepts/blueprints) like you normally would, then run `sails lift` to create the database with Sails.js database migration.</span></span> <span data-ttu-id="7603a-195">예:</span><span class="sxs-lookup"><span data-stu-id="7603a-195">For example:</span></span>

         sails generate api mywidget
         sails lift

    <span data-ttu-id="7603a-196">이 명령에 의해 생성된 `mywidget` 모델은 비어 있으나 이 모델을 사용하여 데이터베이스에 연결되어 있다는 사실을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-196">The `mywidget` model generated by this command is empty, but we can use it to show that we have database connectivity.</span></span>
    <span data-ttu-id="7603a-197">`sails lift`를 실행하면 앱이 사용하는 모델에 대해 누락된 컬렉션 및 테이블이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-197">When you run `sails lift`, it creates the missing collections and tables for the models your app uses.</span></span>
9. <span data-ttu-id="7603a-198">브라우저에서 방금 만든 청사진 API에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-198">Access the blueprint API you just created in the browser.</span></span> <span data-ttu-id="7603a-199">예:</span><span class="sxs-lookup"><span data-stu-id="7603a-199">For example:</span></span>

        http://localhost:1337/mywidget/create

    <span data-ttu-id="7603a-200">API가 만든 항목을 브라우저 창에 다시 반환합니다. 이것은 컬렉션이 정상적으로 만들어졌다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-200">The API should return the created entry back to you in the browser window, which means that your collection is created  successfully.</span></span>

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. <span data-ttu-id="7603a-201">이제 변경 내용을 Azure에 푸시하고, 앱으로 이동하여 계속 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-201">Now, push your changes to Azure, and browse to your app to make sure it still works.</span></span>

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. <span data-ttu-id="7603a-202">Azure 웹앱의 청사진 API에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-202">Access the blueprint API of your Azure web app.</span></span> <span data-ttu-id="7603a-203">예:</span><span class="sxs-lookup"><span data-stu-id="7603a-203">For example:</span></span>

         http://<appname>.azurewebsites.net/mywidget/create

     <span data-ttu-id="7603a-204">API가 다른 새 항목을 반환하는 경우 Azure Web App은 Cosmos DB(MongoDB) 데이터베이스에 그 사실을 알립니다.</span><span class="sxs-lookup"><span data-stu-id="7603a-204">If the API returns another new entry, then your Azure web app is talking to your Cosmos DB (MongoDB) database.</span></span>

## <a name="more-resources"></a><span data-ttu-id="7603a-205">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="7603a-205">More resources</span></span>
* [<span data-ttu-id="7603a-206">Azure 앱 서비스에서 Node.js 웹앱 시작</span><span class="sxs-lookup"><span data-stu-id="7603a-206">Get started with Node.js web apps in Azure App Service</span></span>](app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="7603a-207">Azure 응용 프로그램에 Node.js 모듈 사용</span><span class="sxs-lookup"><span data-stu-id="7603a-207">Using Node.js Modules with Azure applications</span></span>](../nodejs-use-node-modules-azure-apps.md)
