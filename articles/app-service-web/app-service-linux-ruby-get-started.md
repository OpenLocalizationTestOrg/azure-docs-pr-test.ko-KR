---
title: "Linux에서 웹 앱과 Ruby 앱 aaaCreate | Microsoft Docs"
description: "Ruby toocreate 자세한 내용은 Azure 웹 wpp linux를 사용 하 여 앱입니다."
keywords: azure app service, linux, oss, ruby
services: app-service
documentationcenter: 
author: wesmc7777
manager: erikre
editor: 
ms.assetid: 6d00c73c-13cb-446f-8926-923db4101afa
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: wesmc;rachelap
ms.openlocfilehash: 99ce3b5ee16703a147787387bb02973defce8190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a>Linux에서 Web Apps를 사용하여 Ruby 앱 만들기 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다. 이 퀵 스타트를 보면 어떻게 toocreate 레일 응용 프로그램에 기본 Ruby 배포 tooAzure Linux에서 웹 앱으로 합니다.

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a>필수 조건

* [Ruby 2.4.1 이상](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller)
* [Git](https://git-scm.com/downloads)
* [활성 Azure 구독](https://azure.microsoft.com/pricing/free-trial/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a>Hello 샘플 다운로드

터미널 창에서 hello 명령 tooclone hello 샘플 응용 프로그램 저장소 tooyour 로컬 컴퓨터에 다음을 실행 합니다.

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-hello-application-locally"></a>Hello 응용 프로그램을 로컬로 실행

Hello 레일 서버 응용 프로그램 toowork hello에 대 한 순서를 실행 합니다. Toohello 변경 *hello world* 디렉터리 및 hello `rails server` 시작 서버 hello 명령입니다.

```bash
cd hello-world\bin
rails server
```
    
웹 브라우저를 사용 하 여 이동 너무`http://localhost:3000` 로컬로 tootest hello 앱.  

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-toodisplay-welcome-message"></a>응용 프로그램 toodisplay 환영 메시지를 수정 합니다.

환영 메시지를 표시 하므로 hello 응용 프로그램을 수정 합니다. HTML toohello 브라우저로 hello 메시지를 반환 하도록 hello 응용 프로그램의 컨트롤러를 변경 합니다. 

편집할 수 있게 *~/workspace/hello-world/app/controllers/application_controller.rb*를 엽니다. Hello 수정 `ApplicationController` 아래의 코드 예제는 hello와 같은 클래스 toolook:

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

이제 앱이 구성되었습니다. 웹 브라우저를 사용 하 여 이동 너무`http://localhost:3000` tooconfirm hello 루트 방문 페이지.

![Hello World가 구성됨](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a>Azure에서 Ruby 웹앱 만들기

사용 하 여 hello [az 앱 서비스 계획 만들기](https://docs.microsoft.com/cli/azure/appservice/plan#create) 명령 toocreate 웹 앱에 대 한 앱 서비스 계획 합니다. 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

다음으로 hello를 발급 [az webapp 만들기](https://docs.microsoft.com/cli/azure/webapp) hello 새로 만든 서비스 계획을 사용 하는 명령 toocreate hello 웹 앱. 해당 hello 런타임 너무 설정 되어`ruby|2.3`입니다. Tooreplace 반드시 `<app name>` 고유한 응용 프로그램 이름으로 합니다.

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

Hello 웹 응용 프로그램을 만든 후는 **개요** 페이지는 사용 가능한 tooview 합니다. Tooit을 이동 합니다. hello 다음 페이지가 표시 됩니다.

![시작 페이지](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a>응용 프로그램 배포

Git toodeploy hello Ruby 응용 프로그램 tooAzure를 사용 합니다. hello 웹 응용 프로그램으로 구성 된 Git 배포를 이미 있습니다. 실행 하 여 hello 배포 URL를 검색할 수는 [az webapp 배포](https://docs.microsoft.com/cli/azure/webapp/deployment) 명령입니다.  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

Git URL hello는 양식 기반 웹 응용 프로그램 이름으로 다음 hello에 있습니다.

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

Hello 명령을 toodeploy hello 로컬 응용 프로그램 tooyour Azure 웹 사이트의 다음 실행 합니다.

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

Hello 원격 배포 작업에 성공 했음을 보고 있는지 확인 합니다. hello 명령을 생성 텍스트 다음 유사한 toohello를 출력 합니다.

```bash
remote: Using sass-rails 5.0.6
remote: Updating files in vendor/cache
remote: Bundle gems are installed into ./vendor/bundle
remote: Updating files in vendor/cache
remote: ~site/repository
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<your web app name>.scm.azurewebsites.net/<your web app name>.git
  579ccb....2ca5f31  master -> master
myuser@ubuntu1234:~workspace/<app name>$
```

Hello 배포 완료 되 면 hello를 사용 하 여 hello 배포 tootake 효과 대 한 웹 앱을 다시 [az webapp 다시 시작](https://docs.microsoft.com/cli/azure/webapp#restart) 다음과 같이 명령:

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

Tooyour 사이트를 탐색 하 고 hello 결과 확인 합니다.

```bash
http://<your web app name>.azurewebsites.net
```
![업데이트된 웹앱](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> Hello 앱을 다시 시작 하는 동안에 HTTP 상태 코드에 toobrowse hello 사이트 결과 시도 `Error 503 Server unavailable`합니다. 몇 분 정도 걸릴 수 있습니다 toofully 다시 시작 합니다.
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a>다음 단계

[Linux의 Azure App Service Web App에 대한 FAQ](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)