---
title: "PHP aaaCreate 웹 앱에 Azure | Microsoft Docs"
description: "몇 분 안에 Azure App Service Web Apps에서 첫 번째 PHP Hello World를 배포합니다."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 07/21/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 8e1022889ca162f8f15ce7435cc9393cc6efef06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-web-app-in-azure"></a>Azure에서 PHP 웹앱 만들기

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다.  이 빠른 시작 자습서에서는 어떻게 toodeploy PHP 응용 프로그램 tooAzure 웹 앱입니다. Hello를 사용 하 여 hello 웹 앱을 만드는 [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) 에 클라우드 셸 및 Git toodeploy 샘플 PHP 코드 toohello 웹 응용 프로그램을 사용할 수 있습니다.

![Azure에서 실행되는 샘플 앱]](media/app-service-web-get-started-php/hello-world-in-browser.png)

Mac, Windows 또는 Linux 컴퓨터를 사용 하 여 아래 hello 단계를 따를 수 있습니다. Hello 필수 구성 요소가 설치 되 면 약 5 분 toocomplete hello 단계가 필요 합니다.

## <a name="prerequisites"></a>필수 조건

toocomplete이 빠른이 시작:

* [Git 설치](https://git-scm.com/)
* [PHP 설치](https://php.net)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample-locally"></a>Hello 샘플 로컬로 다운로드

터미널 창에서 다음 명령을 hello를 실행 합니다. Hello 샘플 응용 프로그램 tooyour 로컬 컴퓨터에 복제 되 고 toohello 디렉터리 포함 hello 샘플 코드를 탐색 합니다.

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-hello-app-locally"></a>Hello 응용 프로그램을 로컬로 실행

터미널 윈도우를 열고 hello를 사용 하 여 hello 응용 프로그램을 로컬로 실행 `php` 명령 toolaunch hello PHP 웹 서버 기본 제공 합니다.

```bash
php -S localhost:8080
```

웹 브라우저를 열고 http://localhost:8080에서 toohello 샘플 응용 프로그램을 이동 합니다.

Hello 참조 **Hello World!** hello 페이지에 표시 되는 hello 샘플 응용 프로그램의 메시지입니다.

![로컬로 실행되는 샘플 앱](media/app-service-web-get-started-php/localhost-hello-world-in-browser.png)

사용자의 터미널 창에서 눌러 **Ctrl + C** tooexit hello 웹 서버.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)]

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)]

![빈 웹앱 페이지](media/app-service-web-get-started-php/app-service-web-service-created.png)

Azure에서 비어 있는 새 웹앱을 만들었습니다.

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 2, done.
Delta compression using up too4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 352 bytes | 0 bytes/s, done.
Total 2 (delta 1), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '25f18051e9'.
remote: Generating deployment script.
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.php'
remote: Ignoring: .git
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
   cc39b1e..25f1805  master -> master
```

## <a name="browse-toohello-app-locally"></a>로컬로 앱 toohello 찾아보기

찾아보기 toohello 웹 브라우저를 사용 하 여 응용 프로그램을 배포 합니다.

```bash
http://<app_name>.azurewebsites.net
```

hello PHP 샘플 코드는 Azure 앱 서비스 웹 앱에서 실행 중입니다.

![Azure에서 실행되는 샘플 앱](media/app-service-web-get-started-php/hello-world-in-browser.png)

**축하합니다.** 배포한 프로그램 첫 번째 PHP 응용 프로그램 tooApp 서비스입니다.

## <a name="update-locally-and-redeploy-hello-code"></a>로컬에서 업데이트 하 고 hello 코드를 다시 배포

Hello를 열고 로컬 텍스트 편집기를 사용 하 여 `index.php` hello PHP 응용 프로그램 내에서 파일을 너무 hello 문자열 내에서 작은 변경 toohello 텍스트를 다음 확인`echo`:

```php
echo "Hello Azure!";
```

Git에서 변경 내용을 커밋하고 hello 코드 변경 내용을 tooAzure 푸시하고 합니다.

```bash
git commit -am "updated output"
git push azure master
```

배포가 완료 되 면 hello에서 열린 백 toohello 브라우저 창을 전환 **찾아보기 toohello 앱** 단계 및 새로 고침 hello 페이지.

![Azure에서 실행되는 업데이트된 샘플 앱](media/app-service-web-get-started-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a>새로운 Azure 웹앱 관리

Toohello 이동 <a href="https://portal.azure.com" target="_blank">Azure 포털</a> 만든 toomanage hello 웹 앱입니다.

Hello 왼쪽된 메뉴에서 클릭 **응용 프로그램 서비스**, Azure 웹 앱의 hello 이름을 클릭 하 고 있습니다.

![포털 탐색 tooAzure 웹 응용 프로그램](./media/app-service-web-get-started-php/php-docs-hello-world-app-service-list.png)

웹앱의 개요 페이지가 표시됩니다. 여기에서 찾아보기, 중지, 시작, 다시 시작, 삭제와 같은 기본 관리 작업을 수행할 수 있습니다.

![Azure Portal의 App Service 블레이드](media/app-service-web-get-started-php/php-docs-hello-world-app-service-detail.png)

왼쪽된 메뉴 hello 응용 프로그램을 구성 하는 서로 다른 페이지를 제공 합니다. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [MySQL을 사용하는 PHP](app-service-web-tutorial-php-mysql.md)
