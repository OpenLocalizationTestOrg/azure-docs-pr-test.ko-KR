---
title: "앱 서비스 Sails.js 웹 응용 프로그램 tooAzure aaaDeploy | Microsoft Docs"
description: "자세한 내용은 방법 toodeploy Azure 앱 서비스는 Node.js 응용 프로그램입니다. 이 자습서에서는 어떻게 toodeploy는 Sails.js 웹 앱입니다."
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
ms.openlocfilehash: f5b2518b9c87c040845f7268763862be8c15e83e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-sailsjs-web-app-tooazure-app-service"></a><span data-ttu-id="5b20b-104">Sails.js 웹 응용 프로그램 tooAzure 앱 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="5b20b-104">Deploy a Sails.js web app tooAzure App Service</span></span>
<span data-ttu-id="5b20b-105">이 자습서에서는 어떻게 toodeploy Sails.js 앱 tooAzure 앱 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-105">This tutorial shows you how toodeploy a Sails.js app tooAzure App Service.</span></span> <span data-ttu-id="5b20b-106">Hello 프로세스에서 방법에 대 한 몇 가지 일반적인 지식은 수집 수 tooconfigure 앱 서비스에서 Node.js 응용 프로그램 toorun 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-106">In hello process, you can glean some general knowledge on how tooconfigure your Node.js app toorun in App Service.</span></span>

<span data-ttu-id="5b20b-107">여기에서는 다음과 같은 유용한 기술을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-107">Here, you will learn useful skills like:</span></span>

* <span data-ttu-id="5b20b-108">App Service에서 실행되는 Sails.js 앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-108">Configure a Sails.js app run in App Service.</span></span>
* <span data-ttu-id="5b20b-109">Hello 명령줄에서 응용 프로그램 tooApp 서비스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-109">Deploy an app tooApp Service from hello command line.</span></span>
* <span data-ttu-id="5b20b-110">Stdout 및 stderr 읽기 tootroubleshoot 배포 문제를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-110">Read stderr and stdout logs tootroubleshoot any deployment issues.</span></span>
* <span data-ttu-id="5b20b-111">소스 제어 외부의 환경 변수를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-111">Store environment variables outside of source control.</span></span>
* <span data-ttu-id="5b20b-112">앱에서 Azure 환경 변수에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-112">Access Azure environment variables from your app.</span></span>
* <span data-ttu-id="5b20b-113">Tooa 데이터베이스 (MongoDB) 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-113">Connect tooa database (MongoDB).</span></span>

<span data-ttu-id="5b20b-114">Sails.js에 대한 실무 지식이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-114">You should have working knowledge of Sails.js.</span></span> <span data-ttu-id="5b20b-115">이 자습서에서는 의도 한 toohelp 일반적 toorunning Sail.js 관련 된 문제는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-115">This tutorial is not intended toohelp you with issues related toorunning Sail.js in general.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="5b20b-116">CLI 버전 toocomplete hello 작업</span><span class="sxs-lookup"><span data-stu-id="5b20b-116">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="5b20b-117">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-117">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="5b20b-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – hello 클래식 및 리소스 관리 배포 모델에 대 한 우리의 CLI</span><span class="sxs-lookup"><span data-stu-id="5b20b-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span>
- <span data-ttu-id="5b20b-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한</span><span class="sxs-lookup"><span data-stu-id="5b20b-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b20b-120">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5b20b-120">Prerequisites</span></span>
* [<span data-ttu-id="5b20b-121">Node.JS</span><span class="sxs-lookup"><span data-stu-id="5b20b-121">Node.js</span></span>](https://nodejs.org/)
* [<span data-ttu-id="5b20b-122">Sails.js</span><span class="sxs-lookup"><span data-stu-id="5b20b-122">Sails.js</span></span>](http://sailsjs.org/get-started)
* [<span data-ttu-id="5b20b-123">Git</span><span class="sxs-lookup"><span data-stu-id="5b20b-123">Git</span></span>](http://www.git-scm.com/downloads)
* [<span data-ttu-id="5b20b-124">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5b20b-124">Azure CLI 2.0</span></span>](/cli/azure/install-az-cli2)
* <span data-ttu-id="5b20b-125">Microsoft Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="5b20b-125">A Microsoft Azure account.</span></span> <span data-ttu-id="5b20b-126">계정이 없는 경우 [무료 평가판을 등록](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)하거나 [Visual Studio 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-126">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="5b20b-127">Azure 계정 없이 [App Service를 체험](https://azure.microsoft.com/try/app-service/)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-127">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="5b20b-128">시작 응용 프로그램 만들기 및 신용 카드가 필요 없는, 없음의 노력과 헌신 함께 tooan 시간-를 재생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-128">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a><span data-ttu-id="5b20b-129">1단계: 로컬로 Sails.js 앱 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="5b20b-129">Step 1: Create and configure a Sails.js app locally</span></span>
<span data-ttu-id="5b20b-130">먼저 다음 단계를 수행하여 개발 환경에서 기본 Sails.js 앱을 신속하게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-130">First, quickly create a default Sails.js app in your development environment by following these steps:</span></span>

1. <span data-ttu-id="5b20b-131">사용자가 선택한 열려 hello 명령줄 터미널 및 `CD` tooa 작업 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-131">Open hello command-line terminal of your choice and `CD` tooa working directory.</span></span>
2. <span data-ttu-id="5b20b-132">Sails.js 앱을 만들고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-132">Create a Sails.js app and run it:</span></span>

        sails new <app_name>
        cd <app_name>
        sails lift

    <span data-ttu-id="5b20b-133">Http://localhost:1377에 toohello 기본 홈 페이지를 탐색할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-133">Make sure you can navigate toohello default home page at http://localhost:1377.</span></span>

1. <span data-ttu-id="5b20b-134">다음으로 Azure에 대한 로깅을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-134">Next, enable logging for Azure.</span></span> <span data-ttu-id="5b20b-135">루트 디렉터리에 파일을 만들 `iisnode.yml` hello 다음 두 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-135">In your root directory, create a file called `iisnode.yml` and add hello following two lines:</span></span>

        loggingEnabled: true
        logDirectory: iisnode

    <span data-ttu-id="5b20b-136">로깅 hello आ त ा [iisnode](https://github.com/tjanczuk/iisnode) Azure 앱 서비스 toorun Node.js 앱을 사용 하는 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-136">Logging is now enabled for hello [iisnode](https://github.com/tjanczuk/iisnode) server that Azure App Service uses toorun Node.js apps.</span></span> 
    <span data-ttu-id="5b20b-137">이 작동 하는 방법에 대 한 자세한 내용은 참조 하십시오. [어떻게 toodebug는 Node.js 웹 Azure 앱 서비스의 앱](web-sites-nodejs-debug.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-137">For more information on how this works, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

2. <span data-ttu-id="5b20b-138">다음으로 hello Sails.js 앱 toouse Azure 환경 변수를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-138">Next, configure hello Sails.js app toouse Azure environment variables.</span></span> <span data-ttu-id="5b20b-139">Config/env/production.js tooconfigure 프로덕션 환경의 열고 설정 `port` 및 `hookTimeout`:</span><span class="sxs-lookup"><span data-stu-id="5b20b-139">Open config/env/production.js tooconfigure your production environment, and set `port` and `hookTimeout`:</span></span>

        module.exports = {

            // Use process.env.port toohandle web requests toohello default HTTP port
            port: process.env.port,
            // Increase hooks timout too30 seconds
            // This avoids hello Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    <span data-ttu-id="5b20b-140">이러한 구성 설정에 대한 설명서는 [Sails.js 설명서](http://sailsjs.org/documentation/reference/configuration/sails-config)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-140">You can find documentation for these configuration settings in the  [Sails.js Documentation](http://sailsjs.org/documentation/reference/configuration/sails-config).</span></span>

4. <span data-ttu-id="5b20b-141">다음으로 하드 코드 hello Node.js 버전 toouse 원하는입니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-141">Next, hardcode hello Node.js version you want toouse.</span></span> <span data-ttu-id="5b20b-142">Package.json에서 hello 다음 추가 `engines` 속성 tooset hello Node.js 버전 tooone 우리가 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-142">In package.json, add hello following `engines` property tooset hello Node.js version tooone that we want.</span></span>

        "engines": {
            "node": "6.9.1"
        },

5. <span data-ttu-id="5b20b-143">마지막으로 Git 저장소를 초기화하고 파일을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-143">Finally, initialize a Git repository and commit your files.</span></span> <span data-ttu-id="5b20b-144">Hello 응용 프로그램 루트에서 (여기서 package.json는) Git 명령을 다음 실행된 hello:</span><span class="sxs-lookup"><span data-stu-id="5b20b-144">In hello application root (where package.json is), run hello following Git commands:</span></span>

        git init
        git add .
        git commit -m "<your commit message>"

<span data-ttu-id="5b20b-145">사용자 코드는 배포 준비 toobe입니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-145">Your code is ready toobe deployed.</span></span> 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a><span data-ttu-id="5b20b-146">2단계: Azure 앱 만들기 및 Sails.js 배포</span><span class="sxs-lookup"><span data-stu-id="5b20b-146">Step 2: Create an Azure app and deploy Sails.js</span></span>

<span data-ttu-id="5b20b-147">Azure의 hello 앱 서비스 리소스를 만들어 다음에 Sails.js 앱 tooit를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-147">Next, create hello App Service resource in Azure and deploy your Sails.js app tooit.</span></span>

1. <span data-ttu-id="5b20b-148">같은 tooAzure 로그인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-148">log in tooAzure like so:</span></span>

        az login

    <span data-ttu-id="5b20b-149">Azure 구독을 보유 하는 Microsoft 계정 사용 하 여 브라우저에서 hello 프롬프트 toocontinue hello 로그인을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-149">Follow hello prompt toocontinue hello login in a browser with a Microsoft account that has your Azure subscription.</span></span>

3. <span data-ttu-id="5b20b-150">응용 프로그램 서비스에 대 한 hello 배포 사용자를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-150">Set hello deployment user for App Service.</span></span> <span data-ttu-id="5b20b-151">나중에 이러한 자격 증명을 사용하여 코드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-151">You will deploy code using these credentials later.</span></span>
   
        az appservice web deployment user set --user-name <username> --password <password>

3. <span data-ttu-id="5b20b-152">[리소스 그룹](../azure-resource-manager/resource-group-overview.md)을 만들고 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-152">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with a name.</span></span> <span data-ttu-id="5b20b-153">이 Node.js 자습서 없이 tooknow 무엇 인지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-153">For this Node.js tutorial, you don't really need tooknow what it is.</span></span>

        az group create --location "<location>" --name my-sailsjs-app-group

    <span data-ttu-id="5b20b-154">toosee에 사용할 수 있는 가능한 값은 있습니다 `<location>`, hello를 사용 하 여 `az appservice list-locations` CLI 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-154">toosee what possible values you can use for `<location>`, use hello `az appservice list-locations` CLI command.</span></span>

3. <span data-ttu-id="5b20b-155">"무료" [App Service 계획](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)을 만들고 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-155">Create a "FREE" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) with a name.</span></span> <span data-ttu-id="5b20b-156">이 Node.js 자습서에서는 이 계획에서 웹앱에 대한 요금이 부과되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-156">For this Node.js tutorial, just know that you won't be charged for web apps in this plan.</span></span>

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. <span data-ttu-id="5b20b-157">`<app_name>`에 고유한 이름이 있는 새 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-157">Create a new web app with a unique name in `<app_name>`.</span></span>

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a><span data-ttu-id="5b20b-158">3단계: Sails.js 앱 구성 및 배포</span><span class="sxs-lookup"><span data-stu-id="5b20b-158">Step 3: Configure and deploy your Sails.js app</span></span>

1. <span data-ttu-id="5b20b-159">다음 명령을 hello로 새로운 웹 응용 프로그램에 대 한 로컬 Git 배포를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-159">Configure local Git deployment for your new web app with hello following command:</span></span>

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="5b20b-160">해당 hello 원격 Git 리포지토리 구성 즉, 다음과 같이 JSON 출력을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-160">You will get a JSON output like this, which means that hello remote Git repository is configured:</span></span>

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. <span data-ttu-id="5b20b-161">로컬 저장소에 대 한 원격 Git으로 hello URL hello JSON에서에서 추가 (호출 `azure` 편의상).</span><span class="sxs-lookup"><span data-stu-id="5b20b-161">Add hello URL in hello JSON as a Git remote for your local repository (called `azure` for simplicity).</span></span>

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. <span data-ttu-id="5b20b-162">샘플 코드 toohello 배포 `azure` Git 원격입니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-162">Deploy your sample code toohello `azure` Git remote.</span></span> <span data-ttu-id="5b20b-163">메시지가 표시 되 면 이전에 구성한 hello 배포 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-163">When prompted, use hello deployment credentials you configured earlier.</span></span>

        git push azure master

7. <span data-ttu-id="5b20b-164">마지막으로, hello 브라우저에서 Azure 라이브 앱만 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-164">Finally, just launch your live Azure app in hello browser:</span></span>

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="5b20b-165">이제 hello 동일한 Sails.js 홈 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-165">You should now see hello same Sails.js home page.</span></span>

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a><span data-ttu-id="5b20b-166">배포 문제 해결</span><span class="sxs-lookup"><span data-stu-id="5b20b-166">Troubleshoot your deployment</span></span>
<span data-ttu-id="5b20b-167">앱 서비스에서 어떤 이유로 Sails.js 응용 프로그램이 실패 하면 hello stderr 로그 파일을 찾을 toohelp 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-167">If your Sails.js application fails for some reason in App Service, find hello stderr logs toohelp troubleshoot it.</span></span>
<span data-ttu-id="5b20b-168">자세한 내용은 참조 [어떻게 toodebug는 Node.js 웹 Azure 앱 서비스의 앱](web-sites-nodejs-debug.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-168">For more information, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>
<span data-ttu-id="5b20b-169">Hello 앱이 성공적으로 시작 하는 경우 hello stdout 로그 표시 해야 hello 친숙 한 메시지:</span><span class="sxs-lookup"><span data-stu-id="5b20b-169">If hello app has started successfully, hello stdout log should show you hello familiar message:</span></span>

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
    toosee your app, visit http://localhost:\\.\pipe\c775303c-0ebc-4854-8ddd-2e280aabccac
    tooshut down Sails, press <CTRL> + C at any time.

<span data-ttu-id="5b20b-170">Hello에 있는 hello stdout 로그의 세분성을 제어할 수 있습니다 [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-170">You can control granularity of hello stdout logs in hello [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) file.</span></span>

## <a name="connect-tooa-database-in-azure"></a><span data-ttu-id="5b20b-171">Azure에서 tooa 데이터베이스 연결</span><span class="sxs-lookup"><span data-stu-id="5b20b-171">Connect tooa database in Azure</span></span>
<span data-ttu-id="5b20b-172">tooconnect tooa 데이터베이스, Azure의 hello 데이터베이스 사용자가 선택한 Azure SQL 데이터베이스, MySQL, MongoDB, Azure (Redis) 캐시 등 등 Azure에서 만들고 사용 하 hello 해당 [데이터 저장소 어댑터](https://github.com/balderdashy/sails#compatibility) tooconnect tooit 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-172">tooconnect tooa database in Azure, you create hello database of your choice in Azure, such as Azure SQL Database, MySQL, MongoDB, Azure (Redis) Cache, etc., and use hello corresponding [datastore adapter](https://github.com/balderdashy/sails#compatibility) tooconnect tooit.</span></span> <span data-ttu-id="5b20b-173">hello이 섹션의 단계 방법을 보여 줍니다를 사용 하 여 tooconnect tooMongoDB는 [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) MongoDB 클라이언트 연결을 지원할 수 있는 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-173">hello steps in this section show you how tooconnect tooMongoDB by using an [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) database, which can support MongoDB client connections.</span></span>

1. <span data-ttu-id="5b20b-174">[MongoDB 프로토콜 지원을 사용하는 Cosmos DB 계정을 만듭니다](../documentdb/documentdb-create-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="5b20b-174">[Create a Cosmos DB account with MongoDB protocol support](../documentdb/documentdb-create-mongodb-account.md).</span></span>
2. <span data-ttu-id="5b20b-175">[Cosmos DB 컬렉션 및 데이터베이스를 만듭니다](../documentdb/documentdb-create-collection.md).</span><span class="sxs-lookup"><span data-stu-id="5b20b-175">[Create a Cosmos DB collection and database](../documentdb/documentdb-create-collection.md).</span></span> <span data-ttu-id="5b20b-176">hello 컬렉션의 hello 이름 문제가 되지 않지만 Sails.js에서 연결할 때 hello 데이터베이스의 hello 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-176">hello name of hello collection doesn't matter, but you need hello name of hello database when you connect from Sails.js.</span></span>
3. <span data-ttu-id="5b20b-177">[Cosmos DB 데이터베이스에 대 한 연결 정보 hello](../cosmos-db/connect-mongodb-account.md#GetCustomConnection)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-177">[Find hello connection information for your Cosmos DB database](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span></span>
2. <span data-ttu-id="5b20b-178">프로그램 명령줄 터미널에서 hello MongoDB 어댑터 설치:</span><span class="sxs-lookup"><span data-stu-id="5b20b-178">From your command-line terminal, install hello MongoDB adapter:</span></span>

        npm install sails-mongo --save

3. <span data-ttu-id="5b20b-179">Config/connections.js 열고 hello 연결 개체 toohello 목록 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-179">Open config/connections.js and add hello following connection object toohello list:</span></span>

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
    > <span data-ttu-id="5b20b-180">hello `ssl: true` 옵션은 중요 하기 때문에 [Cosmos DB에 필요한](../cosmos-db/connect-mongodb-account.md#connection-string-requirements)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-180">hello `ssl: true` option is important because [Cosmos DB requires it](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 
    >
    >

4. <span data-ttu-id="5b20b-181">각 환경 변수에 대 한 (`process.env.*`), tooset 필요한 앱 서비스에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-181">For each environment variable (`process.env.*`), you need tooset it in App Service.</span></span> <span data-ttu-id="5b20b-182">toodo이, 실행된 hello 터미널에서 명령을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-182">toodo this, run hello following commands from your terminal.</span></span> <span data-ttu-id="5b20b-183">Cosmos DB에 대 한 hello 연결 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-183">Use hello connection information for your Cosmos DB.</span></span>

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="5b20b-184">Azure 앱 설정에 설정 내용을 적용하면 중요한 데이터의 소스를 제어할 수 없게 됩니다(Git).</span><span class="sxs-lookup"><span data-stu-id="5b20b-184">Putting your settings in Azure app settings keeps sensitive data out of your source control (Git).</span></span> <span data-ttu-id="5b20b-185">다음으로 구성한 사용자가 개발 환경 toouse hello 동일한 연결 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-185">Next, you will configure your development environment toouse hello same connection information.</span></span>
5. <span data-ttu-id="5b20b-186">Config/local.js 열고 hello 다음 연결 개체를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-186">Open config/local.js and add hello following connections object:</span></span>

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    <span data-ttu-id="5b20b-187">이 구성은 hello 로컬 환경에 대 한 config/connections.js 파일의 hello 설정을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-187">This configuration overrides hello settings in your config/connections.js file for hello local environment.</span></span> <span data-ttu-id="5b20b-188">이 파일은 Git에서 저장 되지 것입니다 하므로 프로젝트의 hello 기본값.gitignore로 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-188">This file is excluded by hello default .gitignore in your project, so it will not be stored in Git.</span></span> <span data-ttu-id="5b20b-189">이제 Azure 웹 앱에서와 로컬 개발 환경에서 모두 수 tooconnect tooyour Cosmos DB (MongoDB) 데이터베이스 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-189">Now, you are able tooconnect tooyour Cosmos DB (MongoDB) database both from your Azure web app and from your local development environment.</span></span>
6. <span data-ttu-id="5b20b-190">Config/env/production.js tooconfigure 프로덕션 환경을 열고 hello 다음 추가 `models` 개체:</span><span class="sxs-lookup"><span data-stu-id="5b20b-190">Open config/env/production.js tooconfigure your production environment, and add hello following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. <span data-ttu-id="5b20b-191">Config/env/development.js tooconfigure 개발 환경을 열고 hello 다음 추가 `models` 개체:</span><span class="sxs-lookup"><span data-stu-id="5b20b-191">Open config/env/development.js tooconfigure your development environment, and add hello following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    <span data-ttu-id="5b20b-192">`migrate: 'alter'`데이터베이스 마이그레이션 기능 toocreate를 사용 하 고 데이터베이스 컬렉션 또는 테이블을 쉽게 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-192">`migrate: 'alter'` lets you use database migration features toocreate and update database collections or tables easily.</span></span> <span data-ttu-id="5b20b-193">그러나 `migrate: 'safe'` Sails.js에서 toouse 허용 하지 않으므로 Azure 프로덕션 환경에 대 한 사용 `migrate: 'alter'` 프로덕션 환경에서 (참조 [Sails.js 설명서](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span><span class="sxs-lookup"><span data-stu-id="5b20b-193">However, `migrate: 'safe'` is used for your Azure (production) environment because Sails.js does not allow you toouse `migrate: 'alter'` in a production environment (see [Sails.js Documentation](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span></span>
8. <span data-ttu-id="5b20b-194">, 터미널 hello [생성](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) 는 Sails.js [API 세부 계획](http://sailsjs.org/documentation/concepts/blueprints) 일반적으로 적절 하 게 한 다음 실행 하는 같은 `sails lift` Sails.js 데이터베이스 마이그레이션을 사용 하 여 hello 데이터베이스를 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-194">From hello terminal, [generate](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) a Sails.js [blueprint API](http://sailsjs.org/documentation/concepts/blueprints) like you normally would, then run `sails lift` to create hello database with Sails.js database migration.</span></span> <span data-ttu-id="5b20b-195">예:</span><span class="sxs-lookup"><span data-stu-id="5b20b-195">For example:</span></span>

         sails generate api mywidget
         sails lift

    <span data-ttu-id="5b20b-196">hello `mywidget` 이 명령에 의해 생성 된 모델 비어 있지만 tooshow 데이터베이스 연결이 있는지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-196">hello `mywidget` model generated by this command is empty, but we can use it tooshow that we have database connectivity.</span></span>
    <span data-ttu-id="5b20b-197">실행 하는 경우 `sails lift`, hello 누락 된 컬렉션을 만듭니다 및 hello에 대 한 테이블에 응용 프로그램 사용을 모델링 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-197">When you run `sails lift`, it creates hello missing collections and tables for hello models your app uses.</span></span>
9. <span data-ttu-id="5b20b-198">Hello 브라우저에서 방금 만든 액세스 hello 청사진 API입니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-198">Access hello blueprint API you just created in hello browser.</span></span> <span data-ttu-id="5b20b-199">예:</span><span class="sxs-lookup"><span data-stu-id="5b20b-199">For example:</span></span>

        http://localhost:1337/mywidget/create

    <span data-ttu-id="5b20b-200">hello API 컬렉션을 성공적으로 만들어졌는지 즉 hello 브라우저 창에서 만든 hello 항목 백 tooyou를 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-200">hello API should return hello created entry back tooyou in hello browser window, which means that your collection is created  successfully.</span></span>

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. <span data-ttu-id="5b20b-201">이제 프로그램 변경 내용을 tooAzure 푸시를 여전히 작동 하는지 tooyour 앱 toomake를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-201">Now, push your changes tooAzure, and browse tooyour app toomake sure it still works.</span></span>

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. <span data-ttu-id="5b20b-202">Azure 웹 앱의 액세스 hello 청사진 API입니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-202">Access hello blueprint API of your Azure web app.</span></span> <span data-ttu-id="5b20b-203">예:</span><span class="sxs-lookup"><span data-stu-id="5b20b-203">For example:</span></span>

         http://<appname>.azurewebsites.net/mywidget/create

     <span data-ttu-id="5b20b-204">Hello API 또 다른 새 행을 반환 하는 경우 Azure 웹 앱 란 tooyour Cosmos DB (MongoDB) 데이터베이스를 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="5b20b-204">If hello API returns another new entry, then your Azure web app is talking tooyour Cosmos DB (MongoDB) database.</span></span>

## <a name="more-resources"></a><span data-ttu-id="5b20b-205">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="5b20b-205">More resources</span></span>
* [<span data-ttu-id="5b20b-206">Azure 앱 서비스에서 Node.js 웹앱 시작</span><span class="sxs-lookup"><span data-stu-id="5b20b-206">Get started with Node.js web apps in Azure App Service</span></span>](app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="5b20b-207">Azure 응용 프로그램에 Node.js 모듈 사용</span><span class="sxs-lookup"><span data-stu-id="5b20b-207">Using Node.js Modules with Azure applications</span></span>](../nodejs-use-node-modules-azure-apps.md)
