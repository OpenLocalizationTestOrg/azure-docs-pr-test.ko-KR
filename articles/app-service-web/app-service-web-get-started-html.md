---
title: "Azure에서 웹 앱을 정적 HTML aaaCreate | Microsoft Docs"
description: "방법: 정적 HTML을 배포 하 여 Azure 앱 서비스에서 toorun 웹 앱 샘플 앱에 알아봅니다."
services: app-service\web
documentationcenter: 
author: rick-anderson
manager: wpickett
editor: 
ms.assetid: 60495cc5-6963-4bf0-8174-52786d226c26
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/26/2017
ms.author: riande
ms.custom: mvc
ms.openlocfilehash: efd8c8189a3aa1ac35602b688eeb31bff6f5a373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-static-html-web-app-in-azure"></a>Azure에서 정적 HTML 웹앱 만들기

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다.  이 퀵 스타트의 toodeploy 기본 HTML + CSS tooAzure 웹 앱 사이트 하는 방법을 보여 줍니다. Hello를 사용 하 여 hello 웹 앱을 만드는 [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), Git toodeploy 샘플 HTML 콘텐츠 toohello 웹 응용 프로그램을 사용 합니다.

![샘플 앱의 홈 페이지](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

Mac, Windows 또는 Linux 컴퓨터를 사용 하 여 아래 hello 단계를 따를 수 있습니다. Hello 필수 구성 요소가 설치 되 면 약 5 분 toocomplete hello 단계가 필요 합니다.

## <a name="prerequisites"></a>필수 조건

toocomplete이 빠른이 시작:

- [Git 설치](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

## <a name="download-hello-sample"></a>Hello 샘플 다운로드

터미널 창에서 hello 명령 tooclone hello 샘플 응용 프로그램 저장소 tooyour 로컬 컴퓨터에 다음을 실행 합니다.

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

이 퀵 스타트의이 터미널 윈도우 toorun 모든 hello 명령을 사용합니다.

## <a name="view-hello-html"></a>HTML 보기 hello

Hello 샘플 HTML 있는 toohello 디렉터리를 이동 합니다. 열기 hello *index.html* 브라우저에서 파일입니다.

![샘플 앱 홈 페이지](media/app-service-web-get-started-html/hello-world-in-browser.png)

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![빈 웹앱 페이지](media/app-service-web-get-started-html/app-service-web-service-created.png)

Azure에서 비어 있는 새 웹앱을 만들었습니다.

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 13, done.
Delta compression using up too4 threads.
Compressing objects: 100% (11/11), done.
Writing objects: 100% (13/13), 2.07 KiB | 0 bytes/s, done.
Total 13 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'cc39b1e4cb'.
remote: Generating deployment script.
remote: Generating deployment script for Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a>Toohello 응용 프로그램 찾아보기

브라우저에서 toohello Azure 웹 앱 URL을 이동 합니다.

```
http://<app_name>.azurewebsites.net
```

Azure 앱 서비스 웹 앱으로 hello 페이지 실행 중입니다.

![샘플 앱 홈 페이지](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

**축하합니다.** 배포한 프로그램 첫 번째 HTML 응용 프로그램 tooApp 서비스입니다.

## <a name="update-and-redeploy-hello-app"></a>업데이트 하 고 hello 응용 프로그램을 다시 배포

열기 hello *index.html* 텍스트 편집기에서 파일을 변경 toohello 태그를 확인 합니다. 예를 들어, "Azure 앱 서비스-샘플 정적 HTML 사이트" toojust에서 hello H1 제목을 변경 "Azure 앱 서비스 '.

Git에서 변경 내용을 커밋하고 hello 코드 변경 내용을 tooAzure 푸시하고 합니다.

```bash
git commit -am "updated HTML"
git push azure master
```

배포가 완료 되 면 브라우저 toosee hello 변경을 내용을 새로 고칩니다.

![업데이트된 샘플 앱 홈 페이지](media/app-service-web-get-started-html/hello-azure-in-browser-az.png)

## <a name="manage-your-new-azure-web-app"></a>새로운 Azure 웹앱 관리

Toohello 이동 <a href="https://portal.azure.com" target="_blank">Azure 포털</a> 만든 toomanage hello 웹 앱입니다.

Hello 왼쪽된 메뉴에서 클릭 **응용 프로그램 서비스**, Azure 웹 앱의 hello 이름을 클릭 하 고 있습니다.

![포털 탐색 tooAzure 웹 응용 프로그램](./media/app-service-web-get-started-html/portal1.png)

웹앱의 개요 페이지가 표시됩니다. 여기에서 찾아보기, 중지, 시작, 다시 시작, 삭제와 같은 기본 관리 작업을 수행할 수 있습니다. 

![Azure Portal의 App Service 블레이드](./media/app-service-web-get-started-html/portal2.png)

왼쪽된 메뉴 hello 응용 프로그램을 구성 하는 서로 다른 페이지를 제공 합니다. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [사용자 지정 도메인 매핑](app-service-web-tutorial-custom-domain.md)
