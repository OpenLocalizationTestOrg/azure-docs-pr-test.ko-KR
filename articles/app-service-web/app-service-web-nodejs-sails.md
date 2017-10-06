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
# <a name="deploy-a-sailsjs-web-app-tooazure-app-service"></a>Sails.js 웹 응용 프로그램 tooAzure 앱 서비스 배포
이 자습서에서는 어떻게 toodeploy Sails.js 앱 tooAzure 앱 서비스입니다. Hello 프로세스에서 방법에 대 한 몇 가지 일반적인 지식은 수집 수 tooconfigure 앱 서비스에서 Node.js 응용 프로그램 toorun 프로그램입니다.

여기에서는 다음과 같은 유용한 기술을 배웁니다.

* App Service에서 실행되는 Sails.js 앱을 구성합니다.
* Hello 명령줄에서 응용 프로그램 tooApp 서비스를 배포 합니다.
* Stdout 및 stderr 읽기 tootroubleshoot 배포 문제를 기록 합니다.
* 소스 제어 외부의 환경 변수를 저장합니다.
* 앱에서 Azure 환경 변수에 액세스합니다.
* Tooa 데이터베이스 (MongoDB) 연결 합니다.

Sails.js에 대한 실무 지식이 있어야 합니다. 이 자습서에서는 의도 한 toohelp 일반적 toorunning Sail.js 관련 된 문제는 아닙니다.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 버전 toocomplete hello 작업

Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.

- [Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – hello 클래식 및 리소스 관리 배포 모델에 대 한 우리의 CLI
- [Azure CLI 2.0](app-service-web-nodejs-sails.md) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한

## <a name="prerequisites"></a>필수 조건
* [Node.JS](https://nodejs.org/)
* [Sails.js](http://sailsjs.org/get-started)
* [Git](http://www.git-scm.com/downloads)
* [Azure CLI 2.0](/cli/azure/install-az-cli2)
* Microsoft Azure 계정. 계정이 없는 경우 [무료 평가판을 등록](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)하거나 [Visual Studio 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)할 수 있습니다.

> [!NOTE]
> Azure 계정 없이 [App Service를 체험](https://azure.microsoft.com/try/app-service/)할 수 있습니다. 시작 응용 프로그램 만들기 및 신용 카드가 필요 없는, 없음의 노력과 헌신 함께 tooan 시간-를 재생 합니다.
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a>1단계: 로컬로 Sails.js 앱 만들기 및 구성
먼저 다음 단계를 수행하여 개발 환경에서 기본 Sails.js 앱을 신속하게 만듭니다.

1. 사용자가 선택한 열려 hello 명령줄 터미널 및 `CD` tooa 작업 디렉터리입니다.
2. Sails.js 앱을 만들고 실행합니다.

        sails new <app_name>
        cd <app_name>
        sails lift

    Http://localhost:1377에 toohello 기본 홈 페이지를 탐색할 수 있는지 확인 합니다.

1. 다음으로 Azure에 대한 로깅을 사용하도록 설정합니다. 루트 디렉터리에 파일을 만들 `iisnode.yml` hello 다음 두 줄을 추가 합니다.

        loggingEnabled: true
        logDirectory: iisnode

    로깅 hello आ त ा [iisnode](https://github.com/tjanczuk/iisnode) Azure 앱 서비스 toorun Node.js 앱을 사용 하는 서버입니다. 
    이 작동 하는 방법에 대 한 자세한 내용은 참조 하십시오. [어떻게 toodebug는 Node.js 웹 Azure 앱 서비스의 앱](web-sites-nodejs-debug.md)합니다.

2. 다음으로 hello Sails.js 앱 toouse Azure 환경 변수를 구성 합니다. Config/env/production.js tooconfigure 프로덕션 환경의 열고 설정 `port` 및 `hookTimeout`:

        module.exports = {

            // Use process.env.port toohandle web requests toohello default HTTP port
            port: process.env.port,
            // Increase hooks timout too30 seconds
            // This avoids hello Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    이러한 구성 설정에 대한 설명서는 [Sails.js 설명서](http://sailsjs.org/documentation/reference/configuration/sails-config)에서 찾을 수 있습니다.

4. 다음으로 하드 코드 hello Node.js 버전 toouse 원하는입니다. Package.json에서 hello 다음 추가 `engines` 속성 tooset hello Node.js 버전 tooone 우리가 원하는 합니다.

        "engines": {
            "node": "6.9.1"
        },

5. 마지막으로 Git 저장소를 초기화하고 파일을 커밋합니다. Hello 응용 프로그램 루트에서 (여기서 package.json는) Git 명령을 다음 실행된 hello:

        git init
        git add .
        git commit -m "<your commit message>"

사용자 코드는 배포 준비 toobe입니다. 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a>2단계: Azure 앱 만들기 및 Sails.js 배포

Azure의 hello 앱 서비스 리소스를 만들어 다음에 Sails.js 앱 tooit를 배포 합니다.

1. 같은 tooAzure 로그인 됩니다.

        az login

    Azure 구독을 보유 하는 Microsoft 계정 사용 하 여 브라우저에서 hello 프롬프트 toocontinue hello 로그인을 수행 합니다.

3. 응용 프로그램 서비스에 대 한 hello 배포 사용자를 설정 합니다. 나중에 이러한 자격 증명을 사용하여 코드를 배포합니다.
   
        az appservice web deployment user set --user-name <username> --password <password>

3. [리소스 그룹](../azure-resource-manager/resource-group-overview.md)을 만들고 이름을 지정합니다. 이 Node.js 자습서 없이 tooknow 무엇 인지 합니다.

        az group create --location "<location>" --name my-sailsjs-app-group

    toosee에 사용할 수 있는 가능한 값은 있습니다 `<location>`, hello를 사용 하 여 `az appservice list-locations` CLI 명령입니다.

3. "무료" [App Service 계획](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)을 만들고 이름을 지정합니다. 이 Node.js 자습서에서는 이 계획에서 웹앱에 대한 요금이 부과되지 않습니다.

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. `<app_name>`에 고유한 이름이 있는 새 웹앱을 만듭니다.

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a>3단계: Sails.js 앱 구성 및 배포

1. 다음 명령을 hello로 새로운 웹 응용 프로그램에 대 한 로컬 Git 배포를 구성 합니다.

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    해당 hello 원격 Git 리포지토리 구성 즉, 다음과 같이 JSON 출력을 얻게 됩니다.

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. 로컬 저장소에 대 한 원격 Git으로 hello URL hello JSON에서에서 추가 (호출 `azure` 편의상).

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. 샘플 코드 toohello 배포 `azure` Git 원격입니다. 메시지가 표시 되 면 이전에 구성한 hello 배포 자격 증명을 사용 합니다.

        git push azure master

7. 마지막으로, hello 브라우저에서 Azure 라이브 앱만 실행 합니다.

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    이제 hello 동일한 Sails.js 홈 페이지입니다.

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a>배포 문제 해결
앱 서비스에서 어떤 이유로 Sails.js 응용 프로그램이 실패 하면 hello stderr 로그 파일을 찾을 toohelp 문제를 해결 합니다.
자세한 내용은 참조 [어떻게 toodebug는 Node.js 웹 Azure 앱 서비스의 앱](web-sites-nodejs-debug.md)합니다.
Hello 앱이 성공적으로 시작 하는 경우 hello stdout 로그 표시 해야 hello 친숙 한 메시지:

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

Hello에 있는 hello stdout 로그의 세분성을 제어할 수 있습니다 [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) 파일입니다.

## <a name="connect-tooa-database-in-azure"></a>Azure에서 tooa 데이터베이스 연결
tooconnect tooa 데이터베이스, Azure의 hello 데이터베이스 사용자가 선택한 Azure SQL 데이터베이스, MySQL, MongoDB, Azure (Redis) 캐시 등 등 Azure에서 만들고 사용 하 hello 해당 [데이터 저장소 어댑터](https://github.com/balderdashy/sails#compatibility) tooconnect tooit 합니다. hello이 섹션의 단계 방법을 보여 줍니다를 사용 하 여 tooconnect tooMongoDB는 [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) MongoDB 클라이언트 연결을 지원할 수 있는 데이터베이스입니다.

1. [MongoDB 프로토콜 지원을 사용하는 Cosmos DB 계정을 만듭니다](../documentdb/documentdb-create-mongodb-account.md).
2. [Cosmos DB 컬렉션 및 데이터베이스를 만듭니다](../documentdb/documentdb-create-collection.md). hello 컬렉션의 hello 이름 문제가 되지 않지만 Sails.js에서 연결할 때 hello 데이터베이스의 hello 이름이 필요 합니다.
3. [Cosmos DB 데이터베이스에 대 한 연결 정보 hello](../cosmos-db/connect-mongodb-account.md#GetCustomConnection)합니다.
2. 프로그램 명령줄 터미널에서 hello MongoDB 어댑터 설치:

        npm install sails-mongo --save

3. Config/connections.js 열고 hello 연결 개체 toohello 목록 다음을 추가 합니다.

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
    > hello `ssl: true` 옵션은 중요 하기 때문에 [Cosmos DB에 필요한](../cosmos-db/connect-mongodb-account.md#connection-string-requirements)합니다. 
    >
    >

4. 각 환경 변수에 대 한 (`process.env.*`), tooset 필요한 앱 서비스에서 합니다. toodo이, 실행된 hello 터미널에서 명령을 수행 합니다. Cosmos DB에 대 한 hello 연결 정보를 사용 합니다.

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    Azure 앱 설정에 설정 내용을 적용하면 중요한 데이터의 소스를 제어할 수 없게 됩니다(Git). 다음으로 구성한 사용자가 개발 환경 toouse hello 동일한 연결 정보입니다.
5. Config/local.js 열고 hello 다음 연결 개체를 추가 합니다.

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    이 구성은 hello 로컬 환경에 대 한 config/connections.js 파일의 hello 설정을 재정의합니다. 이 파일은 Git에서 저장 되지 것입니다 하므로 프로젝트의 hello 기본값.gitignore로 제외 됩니다. 이제 Azure 웹 앱에서와 로컬 개발 환경에서 모두 수 tooconnect tooyour Cosmos DB (MongoDB) 데이터베이스 됩니다.
6. Config/env/production.js tooconfigure 프로덕션 환경을 열고 hello 다음 추가 `models` 개체:

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. Config/env/development.js tooconfigure 개발 환경을 열고 hello 다음 추가 `models` 개체:

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    `migrate: 'alter'`데이터베이스 마이그레이션 기능 toocreate를 사용 하 고 데이터베이스 컬렉션 또는 테이블을 쉽게 업데이트할 수 있습니다. 그러나 `migrate: 'safe'` Sails.js에서 toouse 허용 하지 않으므로 Azure 프로덕션 환경에 대 한 사용 `migrate: 'alter'` 프로덕션 환경에서 (참조 [Sails.js 설명서](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).
8. , 터미널 hello [생성](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) 는 Sails.js [API 세부 계획](http://sailsjs.org/documentation/concepts/blueprints) 일반적으로 적절 하 게 한 다음 실행 하는 같은 `sails lift` Sails.js 데이터베이스 마이그레이션을 사용 하 여 hello 데이터베이스를 만들려고 합니다. 예:

         sails generate api mywidget
         sails lift

    hello `mywidget` 이 명령에 의해 생성 된 모델 비어 있지만 tooshow 데이터베이스 연결이 있는지를 사용할 수 있습니다.
    실행 하는 경우 `sails lift`, hello 누락 된 컬렉션을 만듭니다 및 hello에 대 한 테이블에 응용 프로그램 사용을 모델링 합니다.
9. Hello 브라우저에서 방금 만든 액세스 hello 청사진 API입니다. 예:

        http://localhost:1337/mywidget/create

    hello API 컬렉션을 성공적으로 만들어졌는지 즉 hello 브라우저 창에서 만든 hello 항목 백 tooyou를 반환 해야 합니다.

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. 이제 프로그램 변경 내용을 tooAzure 푸시를 여전히 작동 하는지 tooyour 앱 toomake를 이동 합니다.

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. Azure 웹 앱의 액세스 hello 청사진 API입니다. 예:

         http://<appname>.azurewebsites.net/mywidget/create

     Hello API 또 다른 새 행을 반환 하는 경우 Azure 웹 앱 란 tooyour Cosmos DB (MongoDB) 데이터베이스를 동작입니다.

## <a name="more-resources"></a>추가 리소스
* [Azure 앱 서비스에서 Node.js 웹앱 시작](app-service-web-get-started-nodejs.md)
* [Azure 응용 프로그램에 Node.js 모듈 사용](../nodejs-use-node-modules-azure-apps.md)
