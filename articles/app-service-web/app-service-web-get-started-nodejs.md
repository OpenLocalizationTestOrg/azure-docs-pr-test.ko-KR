---
title: "Azure에서 Node.js 웹 응용 프로그램 aaaCreate | Microsoft Docs"
description: "몇 분 안에 Azure App Service Web Apps에서 첫 번째 Node.js Hello World를 배포합니다."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 582bb3c2-164b-42f5-b081-95bfcb7a502a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/05/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 163edf83b2353755fc9fa2d75aed489038cf7c81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-web-app-in-azure"></a>Azure에서 Node.js 웹앱 만들기

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다.  이 퀵 스타트의 표시 방법을 toodeploy Node.js 앱 tooAzure 웹 앱입니다. Hello를 사용 하 여 hello 웹 앱을 만드는 [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), Git toodeploy 샘플 Node.js 코드 toohello 웹 응용 프로그램을 사용 합니다.

![Azure에서 실행되는 샘플 앱](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

Mac, Windows 또는 Linux 컴퓨터를 사용 하 여 아래 hello 단계를 따를 수 있습니다. Hello 필수 구성 요소가 설치 되 면 약 5 분 toocomplete hello 단계가 필요 합니다.   

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-Node-Developers/Create-a-Nodejs-app-in-Azure-Quickstart/player]   


## <a name="prerequisites"></a>필수 조건

toocomplete이 빠른이 시작:

* [Git 설치](https://git-scm.com/)
* [Node.js 및 NPM 설치](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

## <a name="download-hello-sample"></a>Hello 샘플 다운로드

터미널 창에서 hello 명령 tooclone hello 샘플 응용 프로그램 저장소 tooyour 로컬 컴퓨터에 다음을 실행 합니다.

```bash
git clone https://github.com/Azure-Samples/nodejs-docs-hello-world
```

이 퀵 스타트의이 터미널 윈도우 toorun 모든 hello 명령을 사용합니다.

Hello 샘플 코드를 있는 toohello 디렉터리를 변경 합니다.

```bash
cd nodejs-docs-hello-world
```

## <a name="run-hello-app-locally"></a>Hello 응용 프로그램을 로컬로 실행

터미널 윈도우를 열고 hello를 사용 하 여 hello 응용 프로그램을 로컬로 실행 `npm start` 스크립트 toolaunch hello Node.js HTTP 서버에서 기본적으로 제공 합니다.

```bash
npm start
```

웹 브라우저를 열고 http://localhost:1337에서 toohello 샘플 응용 프로그램을 이동 합니다.

Hello 참조 **Hello World** hello 페이지에 표시 되는 hello 샘플 응용 프로그램에서 메시지입니다.

![로컬로 실행되는 샘플 앱](media/app-service-web-get-started-nodejs-poc/localhost-hello-world-in-browser.png)

사용자의 터미널 창에서 눌러 **Ctrl + C** tooexit hello 웹 서버.

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![빈 웹앱 페이지](media/app-service-web-get-started-php/app-service-web-service-created.png)

Azure에서 비어 있는 새 웹앱을 만들었습니다.

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 23, done.
Delta compression using up too4 threads.
Compressing objects: 100% (21/21), done.
Writing objects: 100% (23/23), 3.71 KiB | 0 bytes/s, done.
Total 23 (delta 8), reused 7 (delta 1)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'bf114df591'.
remote: Generating deployment script.
remote: Generating deployment script for node.js Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling node.js deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.js'
remote: Copying file: 'package.json'
remote: Copying file: 'process.json'
remote: Deleting file: 'hostingstart.html'
remote: Ignoring: .git
remote: Using start-up script index.js from package.json.
remote: Node.js versions available on hello platform are: 4.4.7, 4.5.0, 6.2.2, 6.6.0, 6.9.1.
remote: Selected node.js version 6.9.1. Use package.json file toochoose a different version.
remote: Selected npm version 3.10.8
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net:443/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a>Toohello 응용 프로그램 찾아보기

찾아보기 toohello 웹 브라우저를 사용 하 여 응용 프로그램을 배포 합니다.

```bash
http://<app_name>.azurewebsites.net
```

hello Node.js 샘플 코드는 Azure 앱 서비스 웹 앱에서 실행 중입니다.

![Azure에서 실행되는 샘플 앱](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

**축하합니다.** 배포한 프로그램 첫 번째 Node.js 앱 tooApp 서비스입니다.

## <a name="update-and-redeploy-hello-code"></a>업데이트 하 고 hello 코드를 다시 배포

Hello를 열고 텍스트 편집기를 사용 하 여 `index.js` hello Node.js 응용 프로그램에서 파일을 너무 hello 호출에서 작은 변경 toohello 텍스트 확인`response.end`:

```nodejs
response.end("Hello Azure!");
```

Git에서 변경 내용을 커밋하고 hello 코드 변경 내용을 tooAzure 푸시하고 합니다.

```bash
git commit -am "updated output"
git push azure master
```

배포가 완료 되 면 hello에서 열린 백 toohello 브라우저 창을 전환 **찾아보기 toohello 앱** 단계별로 실행 하며 새로 고침을 누릅니다.

![Azure에서 실행되는 업데이트된 샘플 앱](media/app-service-web-get-started-nodejs-poc/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a>새로운 Azure 웹앱 관리

Toohello 이동 <a href="https://portal.azure.com" target="_blank">Azure 포털</a> 만든 toomanage hello 웹 앱입니다.

Hello 왼쪽된 메뉴에서 클릭 **응용 프로그램 서비스**, Azure 웹 앱의 hello 이름을 클릭 하 고 있습니다.

![포털 탐색 tooAzure 웹 응용 프로그램](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

웹앱의 개요 페이지가 표시됩니다. 여기에서 찾아보기, 중지, 시작, 다시 시작, 삭제와 같은 기본 관리 작업을 수행할 수 있습니다. 

![Azure Portal의 App Service 블레이드](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

왼쪽된 메뉴 hello 응용 프로그램을 구성 하는 서로 다른 페이지를 제공 합니다. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [MongoDB를 사용하는 Node.js](app-service-web-tutorial-nodejs-mongodb-app.md)
