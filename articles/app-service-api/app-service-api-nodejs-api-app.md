---
title: "Azure 앱 서비스의 API aaaNode.js 앱 | Microsoft Docs"
description: "자세한 내용은 어떻게 toocreate Node.js RESTful API 및 Azure 앱 서비스의 tooan API 앱을 배포 합니다."
services: app-service\api
documentationcenter: node
author: bradygaster
manager: erikre
editor: 
ms.assetid: a820e400-06af-4852-8627-12b3db4a8e70
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: get-started-article
ms.date: 06/13/2017
ms.author: rachelap
ms.openlocfilehash: 3b3229c1453b6ca4d06bef26f476e92afda4e244
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-restful-api-and-deploy-it-tooan-api-app-in-azure"></a><span data-ttu-id="5fd76-103">Node.js RESTful API를 빌드 및 Azure에서 API tooan 앱 배포</span><span class="sxs-lookup"><span data-stu-id="5fd76-103">Build a Node.js RESTful API and deploy it tooan API app in Azure</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="5fd76-104">이 퀵 스타트의 표시 방법을 toocreate REST API Node.js로 작성 된 [Express](http://expressjs.com/)를 사용 하 여는 [Swagger](http://swagger.io/) 정의 및 배포로 [API 앱](app-service-api-apps-why-best-platform.md) Azure에서.</span><span class="sxs-lookup"><span data-stu-id="5fd76-104">This quickstart shows how toocreate a REST API, written with Node.js [Express](http://expressjs.com/), using a [Swagger](http://swagger.io/) definition and deploying it as an [API app](app-service-api-apps-why-best-platform.md) on Azure.</span></span> <span data-ttu-id="5fd76-105">명령줄 도구를 사용 하 여 hello 앱을 만드는, hello로 리소스를 구성 [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), 및 Git를 사용 하 여 hello 앱을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-105">You create hello app using command-line tools, configure resources with hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and deploy hello app using Git.</span></span>  <span data-ttu-id="5fd76-106">완료하면 Azure에서 실행되는 작업 샘플 REST API를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-106">When you've finished, you have a working sample REST API running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5fd76-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5fd76-107">Prerequisites</span></span>

* [<span data-ttu-id="5fd76-108">Git</span><span class="sxs-lookup"><span data-stu-id="5fd76-108">Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="5fd76-109">Node.js 및 NPM</span><span class="sxs-lookup"><span data-stu-id="5fd76-109">Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5fd76-110">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-110">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5fd76-111">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-111">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="5fd76-112">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-112">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-your-environment"></a><span data-ttu-id="5fd76-113">환경 준비</span><span class="sxs-lookup"><span data-stu-id="5fd76-113">Prepare your environment</span></span>

1. <span data-ttu-id="5fd76-114">터미널 창에서 hello 명령 tooclone hello 샘플 tooyour 로컬 컴퓨터에 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-114">In a terminal window, run hello following command tooclone hello sample tooyour local machine.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. <span data-ttu-id="5fd76-115">Hello 샘플 코드를 있는 toohello 디렉터리를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-115">Change toohello directory that contains hello sample code.</span></span>

    ```bash
    cd app-service-api-node-contact-list
    ```

3. <span data-ttu-id="5fd76-116">로컬 컴퓨터에 [Swaggerize](https://www.npmjs.com/package/swaggerize-express)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-116">Install [Swaggerize](https://www.npmjs.com/package/swaggerize-express) on your local machine.</span></span> <span data-ttu-id="5fd76-117">Swaggerize는 Swagger 정의에서 REST API에 대한 Node.js 코드를 생성하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-117">Swaggerize is a tool that generates Node.js code for your REST API from a Swagger definition.</span></span>

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a><span data-ttu-id="5fd76-118">Node.js 코드 생성</span><span class="sxs-lookup"><span data-stu-id="5fd76-118">Generate Node.js code</span></span> 

<span data-ttu-id="5fd76-119">Swagger 메타 데이터를 먼저 만들고 해당 tooscaffold를 사용 하는 API 개발 워크플로 모델링 하는 hello 자습서의이 섹션 (자동 생성) hello API에 대 한 서버 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-119">This section of hello tutorial models an API development workflow in which you create Swagger metadata first and use that tooscaffold (auto-generate) server code for hello API.</span></span> 

<span data-ttu-id="5fd76-120">디렉터리 toohello 변경 *시작* 폴더를 다음 실행 `yo swaggerize`합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-120">Change directory toohello *start* folder, then run `yo swaggerize`.</span></span> <span data-ttu-id="5fd76-121">Swaggerize hello Swagger 정의에 API에 대 한 Node.js 프로젝트를 만들 *api.json*합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-121">Swaggerize creates a Node.js project for your API from hello Swagger definition in *api.json*.</span></span>

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

<span data-ttu-id="5fd76-122">Swaggerize가 프로젝트 이름을 물어보면 *ContactList*를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-122">When Swaggerize asks for a project name, use *ContactList*.</span></span>
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like toocall this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-hello-project-code"></a><span data-ttu-id="5fd76-123">Hello 프로젝트 코드를 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="5fd76-123">Customize hello project code</span></span>

1. <span data-ttu-id="5fd76-124">복사 hello *lib* hello 폴더 *ContactList* 으로 만든 폴더 `yo swaggerize`, 다음에 디렉터리를 변경 *ContactList*합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-124">Copy hello *lib* folder into hello *ContactList* folder created by `yo swaggerize`, then change directory into *ContactList*.</span></span>

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. <span data-ttu-id="5fd76-125">Hello 설치 `jsonpath` 및 `swaggerize-ui` NPM 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-125">Install hello `jsonpath` and `swaggerize-ui` NPM modules.</span></span> 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. <span data-ttu-id="5fd76-126">Hello의 hello 코드 *handlers/contacts.js* 코드 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="5fd76-126">Replace hello code in hello *handlers/contacts.js* with hello following code:</span></span> 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    <span data-ttu-id="5fd76-127">이 코드에 저장 된 hello JSON 데이터를 사용 하 여 *lib/contacts.json* 에 의해 처리 *lib/contactRepository.js*합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-127">This code uses hello JSON data stored in *lib/contacts.json* served by *lib/contactRepository.js*.</span></span> <span data-ttu-id="5fd76-128">새 hello *contacts.js* 코드는 JSON 페이로드로 hello 저장소의 모든 연락처를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-128">hello new *contacts.js* code returns all contacts in hello repository as a JSON payload.</span></span> 

4. <span data-ttu-id="5fd76-129">Hello의 hello 코드 **handlers/contacts/{id}.js** 코드 다음 hello로 파일:</span><span class="sxs-lookup"><span data-stu-id="5fd76-129">Replace hello code in hello **handlers/contacts/{id}.js** file with hello following code:</span></span>

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    <span data-ttu-id="5fd76-130">이 코드를 사용 하면 경로 변수 tooreturn만 hello 연락처를 사용 하 여 지정 된 id</span><span class="sxs-lookup"><span data-stu-id="5fd76-130">This code lets you use a path variable tooreturn only hello contact with a given ID.</span></span>

5. <span data-ttu-id="5fd76-131">hello 코드 **server.js** 코드 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="5fd76-131">Replace hello code in **server.js** with hello following code:</span></span>

    ```javascript
    'use strict';

    var port = process.env.PORT || 8000; 

    var http = require('http');
    var express = require('express');
    var bodyParser = require('body-parser');
    var swaggerize = require('swaggerize-express');
    var swaggerUi = require('swaggerize-ui'); 
    var path = require('path');
    var fs = require("fs");
    
    fs.existsSync = fs.existsSync || require('path').existsSync;

    var app = express();

    var server = http.createServer(app);

    app.use(bodyParser.json());

    app.use(swaggerize({
        api: path.resolve('./config/swagger.json'),
        handlers: path.resolve('./handlers'),
        docspath: '/swagger' 
    }));

    // change four
    app.use('/docs', swaggerUi({
        docs: '/swagger'  
    }));

    server.listen(port, function () { 
    });
    ```   

    <span data-ttu-id="5fd76-132">이 코드는 Azure 앱 서비스와 작동 하는 몇 가지 약간 변경 된 toolet 만들고 API에 대 한 대화형 웹 인터페이스를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-132">This code makes some small changes toolet it work with Azure App Service and exposes an interactive web interface for your API.</span></span>

### <a name="test-hello-api-locally"></a><span data-ttu-id="5fd76-133">테스트 hello API 로컬로</span><span class="sxs-lookup"><span data-stu-id="5fd76-133">Test hello API locally</span></span>

1. <span data-ttu-id="5fd76-134">Hello Node.js 응용 프로그램 시작</span><span class="sxs-lookup"><span data-stu-id="5fd76-134">Start up hello Node.js app</span></span>
    ```bash
    npm start
    ```
    
2. <span data-ttu-id="5fd76-135">Toohttp://localhost:8000 찾아보기 / hello 전체 대화 상대 목록에 대 한 JSON tooview hello에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-135">Browse toohttp://localhost:8000/contacts tooview hello JSON for hello entire contact list.</span></span>
   
   ```json
    {
        "id": 1,
        "name": "Barney Poland",
        "email": "barney@contoso.com"
    },
    {
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    },
    {
        "id": 3,
        "name": "Lora Riggs",
        "email": "lora@contoso.com"
    }
   ```

3. <span data-ttu-id="5fd76-136">찾아보기 toohttp://localhost:8000/연락처/2 tooview hello에 대 한 연결이 `id` 두 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-136">Browse toohttp://localhost:8000/contacts/2 tooview hello contact with an `id` of two.</span></span>
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. <span data-ttu-id="5fd76-137">: //Localhost: 8000/docs에 hello Swagger 웹 인터페이스를 사용 하 여 hello API를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-137">Test hello API using hello Swagger web interface at http://localhost:8000/docs.</span></span>
   
    ![Swagger 웹 인터페이스](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <span data-ttu-id="5fd76-139"><a id="createapiapp"></a> API App 만들기</span><span class="sxs-lookup"><span data-stu-id="5fd76-139"><a id="createapiapp"></a> Create an API App</span></span>

<span data-ttu-id="5fd76-140">이 섹션에서는 Azure 앱 서비스에서 Azure CLI 2.0 hello toocreate hello 리소스 toohost hello API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-140">In this section, you use hello Azure CLI 2.0 toocreate hello resources toohost hello API on Azure App Service.</span></span> 

1.  <span data-ttu-id="5fd76-141">Tooyour hello로 Azure 구독에에서 로그인 [az 로그인](/cli/azure/#login) 명령 열고 지시를 따른 hello 화면에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-141">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

    ```azurecli-interactive
    az login
    ```

2. <span data-ttu-id="5fd76-142">여러 Azure 구독이 있는 경우 하나 변경 hello 기본 구독 toohello 원하는입니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-142">If you have multiple Azure subscriptions, change hello default subscription toohello desired one.</span></span>

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-hello-api-with-git"></a><span data-ttu-id="5fd76-143">Git 사용 하 여 hello API를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-143">Deploy hello API with Git</span></span>

<span data-ttu-id="5fd76-144">사용자 로컬 Git 리포지토리 tooAzure 앱 서비스에서에서 커밋을 푸시 하 여 코드 toohello API 앱을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-144">Deploy your code toohello API app by pushing commits from your local Git repository tooAzure App Service.</span></span>

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. <span data-ttu-id="5fd76-145">Hello에서 새 리포지토리를 초기화 *ContactList* 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-145">Initialize a new repo in hello *ContactList* directory.</span></span> 

    ```bash
    git init .
    ```

3. <span data-ttu-id="5fd76-146">Hello 제외 *node_modules* Git에서 hello 자습서의 이전 단계에서 npm에서 만든 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-146">Exclude hello *node_modules* directory created by npm in an earlier step in hello tutorial from Git.</span></span> <span data-ttu-id="5fd76-147">새 `.gitignore` hello 현재 디렉터리에 파일을 hello 텍스트 hello 파일에 새 줄에 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-147">Create a new `.gitignore` file in hello current directory and add hello following text on a new line anywhere in hello file.</span></span>

    ```
    node_modules/
    ```
    <span data-ttu-id="5fd76-148">Hello 확인 `node_modules` 폴더는 무시 되 고 `git status`합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-148">Confirm hello `node_modules` folder is being ignored with  `git status`.</span></span>

4. <span data-ttu-id="5fd76-149">Hello, toohello 리포지토리에 변경 내용을 커밋하십시오.</span><span class="sxs-lookup"><span data-stu-id="5fd76-149">Commit hello changes toohello repo.</span></span>
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push tooAzure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-hello-api--in-azure"></a><span data-ttu-id="5fd76-150">Azure에서 테스트 hello API</span><span class="sxs-lookup"><span data-stu-id="5fd76-150">Test hello API  in Azure</span></span>

1. <span data-ttu-id="5fd76-151">브라우저 toohttp://app_name.azurewebsites.net/contacts를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-151">Open a browser toohttp://app_name.azurewebsites.net/contacts.</span></span> <span data-ttu-id="5fd76-152">Hello 자습서의 앞부분에 나오는 hello 요청을 로컬로 수행 하는 경우 동일한 JSON으로 반환 하는 hello를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-152">You see hello same JSON returned as when you made hello request locally earlier in hello tutorial.</span></span>

   ```json
   {
       "id": 1,
       "name": "Barney Poland",
       "email": "barney@contoso.com"
   },
   {
       "id": 2,
       "name": "Lacy Barrera",
       "email": "lacy@contoso.com"
   },
   {
       "id": 3,
       "name": "Lora Riggs",
       "email": "lora@contoso.com"
   }
   ```

2. <span data-ttu-id="5fd76-153">브라우저에서 이동 toohello `http://app_name.azurewebsites.net/docs` 아웃 끝점 tootry hello Swagger UI Azure에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-153">In a browser, go toohello `http://app_name.azurewebsites.net/docs` endpoint tootry out hello Swagger UI running on Azure.</span></span>

    ![Swagger Ii](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    <span data-ttu-id="5fd76-155">이제 단순히 커밋 toohello Azure Git 리포지토리를 푸시하여 toohello 샘플 API tooAzure 업데이트를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fd76-155">You can now deploy updates toohello sample API tooAzure simply by pushing commits toohello Azure Git repository.</span></span>

## <a name="clean-up"></a><span data-ttu-id="5fd76-156">정리</span><span class="sxs-lookup"><span data-stu-id="5fd76-156">Clean up</span></span>

<span data-ttu-id="5fd76-157">hello 다음 Azure CLI 명령을 실행 합니다.이 퀵 스타트의에서 만든 hello 리소스를 tooclean:</span><span class="sxs-lookup"><span data-stu-id="5fd76-157">tooclean up hello resources created in this quickstart, run hello following Azure CLI command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a><span data-ttu-id="5fd76-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5fd76-158">Next step</span></span> 
> [!div class="nextstepaction"]
> [<span data-ttu-id="5fd76-159">CORS로 JavaScript 클라이언트에서 API 앱 사용</span><span class="sxs-lookup"><span data-stu-id="5fd76-159">Consume API apps from JavaScript clients with CORS</span></span>](app-service-api-cors-consume-javascript.md)

