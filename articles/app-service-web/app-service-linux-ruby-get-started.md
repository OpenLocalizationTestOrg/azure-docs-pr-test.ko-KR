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
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a><span data-ttu-id="384ac-104">Linux에서 Web Apps를 사용하여 Ruby 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="384ac-104">Create a Ruby App with Web Apps on Linux</span></span> 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="384ac-105">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="384ac-105">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="384ac-106">이 퀵 스타트를 보면 어떻게 toocreate 레일 응용 프로그램에 기본 Ruby 배포 tooAzure Linux에서 웹 앱으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="384ac-106">This quickstart shows you how toocreate a basic Ruby on Rails application you then deploy it tooAzure as a Web App on Linux.</span></span>

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a><span data-ttu-id="384ac-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="384ac-108">Prerequisites</span></span>

* <span data-ttu-id="384ac-109">[Ruby 2.4.1 이상](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller)</span><span class="sxs-lookup"><span data-stu-id="384ac-109">[Ruby 2.4.1 or higher](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span></span>
* <span data-ttu-id="384ac-110">[Git](https://git-scm.com/downloads)</span><span class="sxs-lookup"><span data-stu-id="384ac-110">[Git](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="384ac-111">[활성 Azure 구독](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="384ac-111">An [active Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a><span data-ttu-id="384ac-112">Hello 샘플 다운로드</span><span class="sxs-lookup"><span data-stu-id="384ac-112">Download hello sample</span></span>

<span data-ttu-id="384ac-113">터미널 창에서 hello 명령 tooclone hello 샘플 응용 프로그램 저장소 tooyour 로컬 컴퓨터에 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="384ac-113">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine:</span></span>

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-hello-application-locally"></a><span data-ttu-id="384ac-114">Hello 응용 프로그램을 로컬로 실행</span><span class="sxs-lookup"><span data-stu-id="384ac-114">Run hello application locally</span></span>

<span data-ttu-id="384ac-115">Hello 레일 서버 응용 프로그램 toowork hello에 대 한 순서를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="384ac-115">Run hello rails server in order for hello application toowork.</span></span> <span data-ttu-id="384ac-116">Toohello 변경 *hello world* 디렉터리 및 hello `rails server` 시작 서버 hello 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="384ac-116">Change toohello *hello-world* directory, and hello `rails server` command starts hello server.</span></span>

```bash
cd hello-world\bin
rails server
```
    
<span data-ttu-id="384ac-117">웹 브라우저를 사용 하 여 이동 너무`http://localhost:3000` 로컬로 tootest hello 앱.</span><span class="sxs-lookup"><span data-stu-id="384ac-117">Using your web browser, navigate too`http://localhost:3000` tootest hello app locally.</span></span>  

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-toodisplay-welcome-message"></a><span data-ttu-id="384ac-119">응용 프로그램 toodisplay 환영 메시지를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="384ac-119">Modify app toodisplay welcome message</span></span>

<span data-ttu-id="384ac-120">환영 메시지를 표시 하므로 hello 응용 프로그램을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="384ac-120">Modify hello application so it displays a welcome message.</span></span> <span data-ttu-id="384ac-121">HTML toohello 브라우저로 hello 메시지를 반환 하도록 hello 응용 프로그램의 컨트롤러를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="384ac-121">Change hello application's controller so it returns hello message as HTML toohello browser.</span></span> 

<span data-ttu-id="384ac-122">편집할 수 있게 *~/workspace/hello-world/app/controllers/application_controller.rb*를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="384ac-122">Open *~/workspace/hello-world/app/controllers/application_controller.rb* for editing.</span></span> <span data-ttu-id="384ac-123">Hello 수정 `ApplicationController` 아래의 코드 예제는 hello와 같은 클래스 toolook:</span><span class="sxs-lookup"><span data-stu-id="384ac-123">Modify hello `ApplicationController` class toolook like hello following code sample:</span></span>

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

<span data-ttu-id="384ac-124">이제 앱이 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="384ac-124">Your app is now configured.</span></span> <span data-ttu-id="384ac-125">웹 브라우저를 사용 하 여 이동 너무`http://localhost:3000` tooconfirm hello 루트 방문 페이지.</span><span class="sxs-lookup"><span data-stu-id="384ac-125">Using your web browser, navigate too`http://localhost:3000` tooconfirm hello root landing page.</span></span>

![Hello World가 구성됨](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a><span data-ttu-id="384ac-127">Azure에서 Ruby 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="384ac-127">Create a Ruby web app on Azure</span></span>

<span data-ttu-id="384ac-128">사용 하 여 hello [az 앱 서비스 계획 만들기](https://docs.microsoft.com/cli/azure/appservice/plan#create) 명령 toocreate 웹 앱에 대 한 앱 서비스 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="384ac-128">Use hello [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) command toocreate an app service plan for your web app.</span></span> 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

<span data-ttu-id="384ac-129">다음으로 hello를 발급 [az webapp 만들기](https://docs.microsoft.com/cli/azure/webapp) hello 새로 만든 서비스 계획을 사용 하는 명령 toocreate hello 웹 앱.</span><span class="sxs-lookup"><span data-stu-id="384ac-129">Next, issue hello [az webapp create](https://docs.microsoft.com/cli/azure/webapp) command toocreate hello web app that uses hello newly created service plan.</span></span> <span data-ttu-id="384ac-130">해당 hello 런타임 너무 설정 되어`ruby|2.3`입니다.</span><span class="sxs-lookup"><span data-stu-id="384ac-130">Notice that hello runtime is set too`ruby|2.3`.</span></span> <span data-ttu-id="384ac-131">Tooreplace 반드시 `<app name>` 고유한 응용 프로그램 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="384ac-131">Don't forget tooreplace `<app name>` with a unique app name.</span></span>

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

<span data-ttu-id="384ac-132">Hello 웹 응용 프로그램을 만든 후는 **개요** 페이지는 사용 가능한 tooview 합니다.</span><span class="sxs-lookup"><span data-stu-id="384ac-132">Once hello web app is created, an **Overview** page is available tooview.</span></span> <span data-ttu-id="384ac-133">Tooit을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="384ac-133">Navigate tooit.</span></span> <span data-ttu-id="384ac-134">hello 다음 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="384ac-134">hello following splash page is displayed:</span></span>

![시작 페이지](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a><span data-ttu-id="384ac-136">응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="384ac-136">Deploy your application</span></span>

<span data-ttu-id="384ac-137">Git toodeploy hello Ruby 응용 프로그램 tooAzure를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="384ac-137">Use Git toodeploy hello Ruby application tooAzure.</span></span> <span data-ttu-id="384ac-138">hello 웹 응용 프로그램으로 구성 된 Git 배포를 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="384ac-138">hello web app already has a Git deployment configured.</span></span> <span data-ttu-id="384ac-139">실행 하 여 hello 배포 URL를 검색할 수는 [az webapp 배포](https://docs.microsoft.com/cli/azure/webapp/deployment) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="384ac-139">You can retrieve hello deployment URL by issuing an [az webapp deployment](https://docs.microsoft.com/cli/azure/webapp/deployment) command.</span></span>  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="384ac-140">Git URL hello는 양식 기반 웹 응용 프로그램 이름으로 다음 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="384ac-140">Notice that hello Git URL has hello following form based on your web app name:</span></span>

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

<span data-ttu-id="384ac-141">Hello 명령을 toodeploy hello 로컬 응용 프로그램 tooyour Azure 웹 사이트의 다음 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="384ac-141">Run hello following commands toodeploy hello local application tooyour Azure website:</span></span>

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="384ac-142">Hello 원격 배포 작업에 성공 했음을 보고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="384ac-142">Confirm that hello remote deployment operations report success.</span></span> <span data-ttu-id="384ac-143">hello 명령을 생성 텍스트 다음 유사한 toohello를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="384ac-143">hello commands produce output similar toohello following text:</span></span>

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

<span data-ttu-id="384ac-144">Hello 배포 완료 되 면 hello를 사용 하 여 hello 배포 tootake 효과 대 한 웹 앱을 다시 [az webapp 다시 시작](https://docs.microsoft.com/cli/azure/webapp#restart) 다음과 같이 명령:</span><span class="sxs-lookup"><span data-stu-id="384ac-144">Once hello deployment has completed, restart your web app for hello deployment tootake effect by using hello [az webapp restart](https://docs.microsoft.com/cli/azure/webapp#restart) command, as shown here:</span></span>

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="384ac-145">Tooyour 사이트를 탐색 하 고 hello 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="384ac-145">Navigate tooyour site and verify hello results.</span></span>

```bash
http://<your web app name>.azurewebsites.net
```
![업데이트된 웹앱](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> <span data-ttu-id="384ac-147">Hello 앱을 다시 시작 하는 동안에 HTTP 상태 코드에 toobrowse hello 사이트 결과 시도 `Error 503 Server unavailable`합니다.</span><span class="sxs-lookup"><span data-stu-id="384ac-147">While hello app is restarting, attempting toobrowse hello site results in an HTTP status code `Error 503 Server unavailable`.</span></span> <span data-ttu-id="384ac-148">몇 분 정도 걸릴 수 있습니다 toofully 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="384ac-148">It may take a few minutes toofully restart.</span></span>
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a><span data-ttu-id="384ac-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="384ac-149">Next steps</span></span>

[<span data-ttu-id="384ac-150">Linux의 Azure App Service Web App에 대한 FAQ</span><span class="sxs-lookup"><span data-stu-id="384ac-150">Azure App Service Web App on Linux FAQ</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)