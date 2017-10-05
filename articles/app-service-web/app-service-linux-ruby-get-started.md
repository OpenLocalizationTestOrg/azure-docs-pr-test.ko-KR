---
title: "Linux에서 Web Apps를 사용하여 Ruby 앱 만들기 | Microsoft Docs"
description: "Linux에서 Azure 웹앱을 사용하여 Ruby 앱을 만드는 방법을 알아봅니다."
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
ms.openlocfilehash: 17f3f1a2122c508501134a0c43ab6abce412fb44
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a><span data-ttu-id="499eb-104">Linux에서 Web Apps를 사용하여 Ruby 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="499eb-104">Create a Ruby App with Web Apps on Linux</span></span> 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="499eb-105">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-105">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="499eb-106">이 빠른 시작에서는 기본 Ruby on Rails 응용 프로그램을 만든 다음 Linux의 웹앱으로 Azure에 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-106">This quickstart shows you how to create a basic Ruby on Rails application you then deploy it to Azure as a Web App on Linux.</span></span>

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a><span data-ttu-id="499eb-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="499eb-108">Prerequisites</span></span>

* <span data-ttu-id="499eb-109">[Ruby 2.4.1 이상](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller)</span><span class="sxs-lookup"><span data-stu-id="499eb-109">[Ruby 2.4.1 or higher](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span></span>
* <span data-ttu-id="499eb-110">[Git](https://git-scm.com/downloads)</span><span class="sxs-lookup"><span data-stu-id="499eb-110">[Git](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="499eb-111">[활성 Azure 구독](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="499eb-111">An [active Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-the-sample"></a><span data-ttu-id="499eb-112">샘플 다운로드</span><span class="sxs-lookup"><span data-stu-id="499eb-112">Download the sample</span></span>

<span data-ttu-id="499eb-113">터미널 창에서 다음 명령을 실행하여 로컬 컴퓨터에 샘플 앱 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-113">In a terminal window, run the following command to clone the sample app repository to your local machine:</span></span>

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-the-application-locally"></a><span data-ttu-id="499eb-114">로컬에서 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="499eb-114">Run the application locally</span></span>

<span data-ttu-id="499eb-115">응용 프로그램이 작동하도록 레일 서버를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-115">Run the rails server in order for the application to work.</span></span> <span data-ttu-id="499eb-116">*hello-world* 디렉터리로 변경한 후 `rails server` 명령에서 서버를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-116">Change to the *hello-world* directory, and the `rails server` command starts the server.</span></span>

```bash
cd hello-world\bin
rails server
```
    
<span data-ttu-id="499eb-117">웹 브라우저를 사용하여 `http://localhost:3000`으로 이동한 후 앱을 로컬로 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-117">Using your web browser, navigate to `http://localhost:3000` to test the app locally.</span></span>    

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-to-display-welcome-message"></a><span data-ttu-id="499eb-119">앱을 수정하여 환영 메시지 표시</span><span class="sxs-lookup"><span data-stu-id="499eb-119">Modify app to display welcome message</span></span>

<span data-ttu-id="499eb-120">환영 메시지를 표시하도록 응용 프로그램을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-120">Modify the application so it displays a welcome message.</span></span> <span data-ttu-id="499eb-121">브라우저에 HTML로 메시지를 반환하도록 응용 프로그램의 컨트롤러를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-121">Change the application's controller so it returns the message as HTML to the browser.</span></span> 

<span data-ttu-id="499eb-122">편집할 수 있게 *~/workspace/hello-world/app/controllers/application_controller.rb*를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-122">Open *~/workspace/hello-world/app/controllers/application_controller.rb* for editing.</span></span> <span data-ttu-id="499eb-123">다음 코드 샘플과 같이 보이도록 `ApplicationController` 클래스를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-123">Modify the `ApplicationController` class to look like the following code sample:</span></span>

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

<span data-ttu-id="499eb-124">이제 앱이 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-124">Your app is now configured.</span></span> <span data-ttu-id="499eb-125">웹 브라우저를 사용하여 `http://localhost:3000`으로 이동한 후 루트 방문 페이지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-125">Using your web browser, navigate to `http://localhost:3000` to confirm the root landing page.</span></span>

![Hello World가 구성됨](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a><span data-ttu-id="499eb-127">Azure에서 Ruby 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="499eb-127">Create a Ruby web app on Azure</span></span>

<span data-ttu-id="499eb-128">[az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) 명령을 사용하여 웹앱에 대한 앱 서비스 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-128">Use the [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) command to create an app service plan for your web app.</span></span> 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

<span data-ttu-id="499eb-129">다음으로 [az webapp create](https://docs.microsoft.com/cli/azure/webapp) 명령을 실행하여 새로 만든 서비스 계획을 사용하는 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-129">Next, issue the [az webapp create](https://docs.microsoft.com/cli/azure/webapp) command to create the web app that uses the newly created service plan.</span></span> <span data-ttu-id="499eb-130">런타임은 `ruby|2.3`으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-130">Notice that the runtime is set to `ruby|2.3`.</span></span> <span data-ttu-id="499eb-131">`<app name>`을 고유한 앱 이름으로 대체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-131">Don't forget to replace `<app name>` with a unique app name.</span></span>

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

<span data-ttu-id="499eb-132">웹앱을 만든 후 **개요** 페이지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-132">Once the web app is created, an **Overview** page is available to view.</span></span> <span data-ttu-id="499eb-133">해당 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-133">Navigate to it.</span></span> <span data-ttu-id="499eb-134">다음 시작 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-134">The following splash page is displayed:</span></span>

![시작 페이지](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a><span data-ttu-id="499eb-136">응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="499eb-136">Deploy your application</span></span>

<span data-ttu-id="499eb-137">Git를 사용하여 Azure에 Ruby 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-137">Use Git to deploy the Ruby application to Azure.</span></span> <span data-ttu-id="499eb-138">웹앱에는 이미 Git 배포가 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-138">The web app already has a Git deployment configured.</span></span> <span data-ttu-id="499eb-139">[az webapp deployment](https://docs.microsoft.com/cli/azure/webapp/deployment) 명령을 실행하여 배포 URL을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-139">You can retrieve the deployment URL by issuing an [az webapp deployment](https://docs.microsoft.com/cli/azure/webapp/deployment) command.</span></span>  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="499eb-140">Git URL은 웹앱 이름에 따라 다음과 같은 형식을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-140">Notice that the Git URL has the following form based on your web app name:</span></span>

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

<span data-ttu-id="499eb-141">다음 명령을 실행하여 Azure 웹 사이트에 로컬 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-141">Run the following commands to deploy the local application to your Azure website:</span></span>

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="499eb-142">원격 배포 작업이 성공을 보고하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-142">Confirm that the remote deployment operations report success.</span></span> <span data-ttu-id="499eb-143">이 명령은 다음 텍스트와 유사한 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-143">The commands produce output similar to the following text:</span></span>

```bash
remote: Using sass-rails 5.0.6
remote: Updating files in vendor/cache
remote: Bundle gems are installed into ./vendor/bundle
remote: Updating files in vendor/cache
remote: ~site/repository
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
  579ccb....2ca5f31  master -> master
myuser@ubuntu1234:~workspace/<app name>$
```

<span data-ttu-id="499eb-144">배포가 완료되면 여기에 표시된 것처럼 [az webapp restart](https://docs.microsoft.com/cli/azure/webapp#restart) 명령을 사용하여 배포를 적용하도록 웹앱을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-144">Once the deployment has completed, restart your web app for the deployment to take effect by using the [az webapp restart](https://docs.microsoft.com/cli/azure/webapp#restart) command, as shown here:</span></span>

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="499eb-145">사이트로 이동하고 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-145">Navigate to your site and verify the results.</span></span>

```bash
http://<your web app name>.azurewebsites.net
```
![업데이트된 웹앱](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> <span data-ttu-id="499eb-147">앱이 다시 시작되는 동안 사이트로 이동하려고 하면 HTTP 상태 코드 `Error 503 Server unavailable`이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-147">While the app is restarting, attempting to browse the site results in an HTTP status code `Error 503 Server unavailable`.</span></span> <span data-ttu-id="499eb-148">완전하게 다시 시작하는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="499eb-148">It may take a few minutes to fully restart.</span></span>
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a><span data-ttu-id="499eb-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="499eb-149">Next steps</span></span>

[<span data-ttu-id="499eb-150">Linux의 Azure App Service Web App에 대한 FAQ</span><span class="sxs-lookup"><span data-stu-id="499eb-150">Azure App Service Web App on Linux FAQ</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)