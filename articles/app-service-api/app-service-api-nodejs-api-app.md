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
# <a name="build-a-nodejs-restful-api-and-deploy-it-tooan-api-app-in-azure"></a>Node.js RESTful API를 빌드 및 Azure에서 API tooan 앱 배포
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

이 퀵 스타트의 표시 방법을 toocreate REST API Node.js로 작성 된 [Express](http://expressjs.com/)를 사용 하 여는 [Swagger](http://swagger.io/) 정의 및 배포로 [API 앱](app-service-api-apps-why-best-platform.md) Azure에서. 명령줄 도구를 사용 하 여 hello 앱을 만드는, hello로 리소스를 구성 [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), 및 Git를 사용 하 여 hello 앱을 배포 합니다.  완료하면 Azure에서 실행되는 작업 샘플 REST API를 갖습니다.

## <a name="prerequisites"></a>필수 조건

* [Git](https://git-scm.com/)
* [Node.js 및 NPM](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

## <a name="prepare-your-environment"></a>환경 준비

1. 터미널 창에서 hello 명령 tooclone hello 샘플 tooyour 로컬 컴퓨터에 다음을 실행 합니다.

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. Hello 샘플 코드를 있는 toohello 디렉터리를 변경 합니다.

    ```bash
    cd app-service-api-node-contact-list
    ```

3. 로컬 컴퓨터에 [Swaggerize](https://www.npmjs.com/package/swaggerize-express)를 설치합니다. Swaggerize는 Swagger 정의에서 REST API에 대한 Node.js 코드를 생성하는 도구입니다.

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a>Node.js 코드 생성 

Swagger 메타 데이터를 먼저 만들고 해당 tooscaffold를 사용 하는 API 개발 워크플로 모델링 하는 hello 자습서의이 섹션 (자동 생성) hello API에 대 한 서버 코드입니다. 

디렉터리 toohello 변경 *시작* 폴더를 다음 실행 `yo swaggerize`합니다. Swaggerize hello Swagger 정의에 API에 대 한 Node.js 프로젝트를 만들 *api.json*합니다.

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

Swaggerize가 프로젝트 이름을 물어보면 *ContactList*를 사용합니다.
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like toocall this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-hello-project-code"></a>Hello 프로젝트 코드를 사용자 지정

1. 복사 hello *lib* hello 폴더 *ContactList* 으로 만든 폴더 `yo swaggerize`, 다음에 디렉터리를 변경 *ContactList*합니다.

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. Hello 설치 `jsonpath` 및 `swaggerize-ui` NPM 모듈입니다. 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. Hello의 hello 코드 *handlers/contacts.js* 코드 다음 hello로: 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    이 코드에 저장 된 hello JSON 데이터를 사용 하 여 *lib/contacts.json* 에 의해 처리 *lib/contactRepository.js*합니다. 새 hello *contacts.js* 코드는 JSON 페이로드로 hello 저장소의 모든 연락처를 반환 합니다. 

4. Hello의 hello 코드 **handlers/contacts/{id}.js** 코드 다음 hello로 파일:

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    이 코드를 사용 하면 경로 변수 tooreturn만 hello 연락처를 사용 하 여 지정 된 id

5. hello 코드 **server.js** 코드 다음 hello로:

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

    이 코드는 Azure 앱 서비스와 작동 하는 몇 가지 약간 변경 된 toolet 만들고 API에 대 한 대화형 웹 인터페이스를 노출 합니다.

### <a name="test-hello-api-locally"></a>테스트 hello API 로컬로

1. Hello Node.js 응용 프로그램 시작
    ```bash
    npm start
    ```
    
2. Toohttp://localhost:8000 찾아보기 / hello 전체 대화 상대 목록에 대 한 JSON tooview hello에 연결 합니다.
   
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

3. 찾아보기 toohttp://localhost:8000/연락처/2 tooview hello에 대 한 연결이 `id` 두 합니다.
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. : //Localhost: 8000/docs에 hello Swagger 웹 인터페이스를 사용 하 여 hello API를 테스트 합니다.
   
    ![Swagger 웹 인터페이스](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <a id="createapiapp"></a> API App 만들기

이 섹션에서는 Azure 앱 서비스에서 Azure CLI 2.0 hello toocreate hello 리소스 toohost hello API를 사용합니다. 

1.  Tooyour hello로 Azure 구독에에서 로그인 [az 로그인](/cli/azure/#login) 명령 열고 지시를 따른 hello 화면에 표시 합니다.

    ```azurecli-interactive
    az login
    ```

2. 여러 Azure 구독이 있는 경우 하나 변경 hello 기본 구독 toohello 원하는입니다.

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-hello-api-with-git"></a>Git 사용 하 여 hello API를 배포 합니다.

사용자 로컬 Git 리포지토리 tooAzure 앱 서비스에서에서 커밋을 푸시 하 여 코드 toohello API 앱을 배포 합니다.

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. Hello에서 새 리포지토리를 초기화 *ContactList* 디렉터리입니다. 

    ```bash
    git init .
    ```

3. Hello 제외 *node_modules* Git에서 hello 자습서의 이전 단계에서 npm에서 만든 디렉터리입니다. 새 `.gitignore` hello 현재 디렉터리에 파일을 hello 텍스트 hello 파일에 새 줄에 다음을 추가 합니다.

    ```
    node_modules/
    ```
    Hello 확인 `node_modules` 폴더는 무시 되 고 `git status`합니다.

4. Hello, toohello 리포지토리에 변경 내용을 커밋하십시오.
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push tooAzure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-hello-api--in-azure"></a>Azure에서 테스트 hello API

1. 브라우저 toohttp://app_name.azurewebsites.net/contacts를 엽니다. Hello 자습서의 앞부분에 나오는 hello 요청을 로컬로 수행 하는 경우 동일한 JSON으로 반환 하는 hello를 표시 됩니다.

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

2. 브라우저에서 이동 toohello `http://app_name.azurewebsites.net/docs` 아웃 끝점 tootry hello Swagger UI Azure에서 실행 합니다.

    ![Swagger Ii](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    이제 단순히 커밋 toohello Azure Git 리포지토리를 푸시하여 toohello 샘플 API tooAzure 업데이트를 배포할 수 있습니다.

## <a name="clean-up"></a>정리

hello 다음 Azure CLI 명령을 실행 합니다.이 퀵 스타트의에서 만든 hello 리소스를 tooclean:

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a>다음 단계 
> [!div class="nextstepaction"]
> [CORS로 JavaScript 클라이언트에서 API 앱 사용](app-service-api-cors-consume-javascript.md)

