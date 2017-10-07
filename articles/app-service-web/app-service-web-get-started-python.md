---
title: "Azure에서 Python 웹 응용 프로그램 aaaCreate | Microsoft Docs"
description: "몇 분 안에 Azure App Service Web Apps에서 첫 번째 Python Hello World를 배포합니다."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 928ee2e5-6143-4c0c-8546-366f5a3d80ce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 03/17/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 42178d490d8aa8eaf93710667aad598794c62c8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-python-web-app-in-azure"></a>Azure에서 Python 웹앱 만들기

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다.  이 퀵 스타트의 방법을 안내 toodevelop 및 Python 응용 프로그램 tooAzure 웹 앱을 배포 합니다. Hello를 사용 하 여 hello 웹 앱을 만드는 [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), Git toodeploy 샘플 Python 코드가 toohello 웹 응용 프로그램을 사용 합니다.

![Azure에서 실행되는 샘플 앱](media/app-service-web-get-started-python/hello-world-in-browser.png)

Mac, Windows 또는 Linux 컴퓨터를 사용 하 여 아래 hello 단계를 따를 수 있습니다. Hello 필수 구성 요소가 설치 되 면 약 5 분 toocomplete hello 단계가 필요 합니다.
## <a name="prerequisites"></a>필수 조건

toocomplete이이 자습서:

1. [Git 설치](https://git-scm.com/)
1. [Python 설치](https://www.python.org/downloads/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

## <a name="download-hello-sample"></a>Hello 샘플 다운로드

터미널 창에서 hello 명령 tooclone hello 샘플 응용 프로그램 저장소 tooyour 로컬 컴퓨터에 다음을 실행 합니다.

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
```

이 퀵 스타트의이 터미널 윈도우 toorun 모든 hello 명령을 사용합니다.

Hello 샘플 코드를 있는 toohello 디렉터리를 변경 합니다.

```bash
cd Python-docs-hello-world
```

## <a name="run-hello-app-locally"></a>Hello 응용 프로그램을 로컬로 실행

사용 하 여 필요한 hello 패키지 설치 `pip`합니다.

```bash
pip install -r requirements.txt
```

터미널 윈도우를 열고 hello를 사용 하 여 hello 응용 프로그램을 로컬로 실행 `Python` 명령 toolaunch hello Python 웹 서버 기본 제공 합니다.

```bash
python main.py
```

웹 브라우저를 열고 http://localhost:5000에서 toohello 샘플 응용 프로그램을 이동 합니다.

Hello 나타나면 **Hello World** hello 페이지에 표시 되는 hello 샘플 응용 프로그램에서 메시지입니다.

![로컬로 실행되는 샘플 앱](media/app-service-web-get-started-python/localhost-hello-world-in-browser.png)

사용자의 터미널 창에서 눌러 **Ctrl + C** tooexit hello 웹 서버.

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![빈 웹앱 페이지](media/app-service-web-get-started-python/app-service-web-service-created.png)

Azure에서 비어 있는 새 웹앱을 만들었습니다.

## <a name="configure-toouse-python"></a>Python toouse 구성

사용 하 여 hello [az webapp 구성 집합](/cli/azure/webapp/config#set) 명령 tooconfigure hello 웹 응용 프로그램 toouse Python 버전 `3.4`합니다.

```azurecli-interactive
az webapp config set --python-version 3.4 --name <app_name> --resource-group myResourceGroup
```


이러한 방식으로 hello Python 버전 설정 hello 플랫폼에서 제공 하는 기본 컨테이너를 사용 합니다. toouse 고유한 컨테이너 참조 hello hello에 대 한 참조를 CLI [az webapp 구성 컨테이너 세트](/cli/azure/webapp/config/container#set) 명령입니다.

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 18, done.
Delta compression using up too4 threads.
Compressing objects: 100% (16/16), done.
Writing objects: 100% (18/18), 4.31 KiB | 0 bytes/s, done.
Total 18 (delta 4), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '44e74fe7dd'.
remote: Generating deployment script.
remote: Generating deployment script for python Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling python deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'main.py'
remote: Copying file: 'README.md'
remote: Copying file: 'requirements.txt'
remote: Copying file: 'virtualenv_proxy.py'
remote: Copying file: 'web.2.7.config'
remote: Copying file: 'web.3.4.config'
remote: Detected requirements.txt.  You can skip Python specific steps with a .skipPythonDeployment file.
remote: Detecting Python runtime from site configuration
remote: Detected python-3.4
remote: Creating python-3.4 virtual environment.
remote: .................................
remote: Pip install requirements.
remote: Successfully installed Flask click itsdangerous Jinja2 Werkzeug MarkupSafe
remote: Cleaning up...
remote: .
remote: Overwriting web.config with web.3.4.config
remote:         1 file(s) copied.
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a>Toohello 응용 프로그램 찾아보기

찾아보기 toohello 웹 브라우저를 사용 하 여 응용 프로그램을 배포 합니다.

```bash
http://<app_name>.azurewebsites.net
```

hello Python 샘플 코드는 Azure 앱 서비스 웹 앱에서 실행 중입니다.

![Azure에서 실행되는 샘플 앱](media/app-service-web-get-started-python/hello-world-in-browser.png)

**축하합니다.** 배포한 프로그램 첫 번째 Python 응용 프로그램 tooApp 서비스입니다.

## <a name="update-and-redeploy-hello-code"></a>업데이트 하 고 hello 코드를 다시 배포

Hello를 열고 로컬 텍스트 편집기를 사용 하 여 `main.py` hello Python 응용 프로그램에서 파일을 작은 변경 toohello 텍스트 다음 toohello 확인 `return` 문:

```python
return 'Hello, Azure!'
```

Git에서 변경 내용을 커밋하고 hello 코드 변경 내용을 tooAzure 푸시하고 합니다.

```bash
git commit -am "updated output"
git push azure master
```

배포가 완료 되 면 hello에서 열린 백 toohello 브라우저 창을 전환 [찾아보기 toohello 앱](#browse-to-the-app) 단계 및 새로 고침 hello 페이지.

![Azure에서 실행되는 업데이트된 샘플 앱](media/app-service-web-get-started-python/hello-azure-in-browser.png)

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
> [PostgreSQL을 사용하는 Python](app-service-web-tutorial-docker-python-postgresql-app.md)
