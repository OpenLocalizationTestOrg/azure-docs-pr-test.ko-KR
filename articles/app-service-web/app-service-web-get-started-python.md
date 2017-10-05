---
title: "Azure에서 Python 웹앱 만들기 | Microsoft Docs"
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
ms.openlocfilehash: 119f9770097c010cc360e0e204d06a307a268814
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-python-web-app-in-azure"></a><span data-ttu-id="ec770-103">Azure에서 Python 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="ec770-103">Create a Python web app in Azure</span></span>

<span data-ttu-id="ec770-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="ec770-105">이 빠른 시작에서는 Python 앱을 개발하고 Azure Web Apps에 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-105">This quickstart walks through how to develop and deploy a Python app to Azure Web Apps.</span></span> <span data-ttu-id="ec770-106">[Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)를 사용하여 웹앱을 만들고 Git을 사용하여 웹앱에 샘플 Python 코드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-106">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git to deploy sample Python code to the web app.</span></span>

![Azure에서 실행되는 샘플 앱](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="ec770-108">Mac, Windows 또는 Linux 컴퓨터를 사용하여 아래 단계를 따르면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="ec770-109">필수 구성 요소가 설치된 후 단계를 완료하는 데는 약 5분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-109">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>
## <a name="prerequisites"></a><span data-ttu-id="ec770-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ec770-110">Prerequisites</span></span>

<span data-ttu-id="ec770-111">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-111">To complete this tutorial:</span></span>

1. [<span data-ttu-id="ec770-112">Git 설치</span><span class="sxs-lookup"><span data-stu-id="ec770-112">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="ec770-113">Python 설치</span><span class="sxs-lookup"><span data-stu-id="ec770-113">Install Python</span></span>](https://www.python.org/downloads/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ec770-114">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-114">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ec770-115">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="ec770-116">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec770-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-the-sample"></a><span data-ttu-id="ec770-117">샘플 다운로드</span><span class="sxs-lookup"><span data-stu-id="ec770-117">Download the sample</span></span>

<span data-ttu-id="ec770-118">터미널 창에서 다음 명령을 실행하여 로컬 컴퓨터에 샘플 앱 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-118">In a terminal window, run the following command to clone the sample app repository to your local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
```

<span data-ttu-id="ec770-119">이 터미널 창을 사용하여 이 빠른 시작의 모든 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-119">You use this terminal window to run all the commands in this quickstart.</span></span>

<span data-ttu-id="ec770-120">샘플 코드를 포함하는 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-120">Change to the directory that contains the sample code.</span></span>

```bash
cd Python-docs-hello-world
```

## <a name="run-the-app-locally"></a><span data-ttu-id="ec770-121">로컬에서 앱 실행</span><span class="sxs-lookup"><span data-stu-id="ec770-121">Run the app locally</span></span>

<span data-ttu-id="ec770-122">`pip`를 사용하여 필요한 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-122">Install the required packages using `pip`.</span></span>

```bash
pip install -r requirements.txt
```

<span data-ttu-id="ec770-123">Python 웹 서버에서 기본 제공을 시작하려면 터미널 창을 열고 `Python` 명령을 사용하여 응용 프로그램을 로컬로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-123">Run the application locally by opening a terminal window and using the `Python` command to launch the built-in Python web server.</span></span>

```bash
python main.py
```

<span data-ttu-id="ec770-124">웹 브라우저를 열고 http://localhost:5000 에서 샘플 앱으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-124">Open a web browser, and navigate to the sample app at http://localhost:5000.</span></span>

<span data-ttu-id="ec770-125">이 페이지에 표시된 샘플 앱에서 **Hello World** 메시지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-125">You can see the **Hello World** message from the sample app displayed in the page.</span></span>

![로컬로 실행되는 샘플 앱](media/app-service-web-get-started-python/localhost-hello-world-in-browser.png)

<span data-ttu-id="ec770-127">터미널 창에서 **Ctrl+C**를 눌러 웹 서버를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-127">In your terminal window, press **Ctrl+C** to exit the web server.</span></span>

[!INCLUDE [Log in to Azure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![빈 웹앱 페이지](media/app-service-web-get-started-python/app-service-web-service-created.png)

<span data-ttu-id="ec770-129">Azure에서 비어 있는 새 웹앱을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-129">You’ve created an empty new web app in Azure.</span></span>

## <a name="configure-to-use-python"></a><span data-ttu-id="ec770-130">Python을 사용하도록 구성</span><span class="sxs-lookup"><span data-stu-id="ec770-130">Configure to use Python</span></span>

<span data-ttu-id="ec770-131">[az webapp config set](/cli/azure/webapp/config#set) 명령을 사용하여 Python 버전 `3.4`를 사용하도록 웹앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-131">Use the [az webapp config set](/cli/azure/webapp/config#set) command to configure the web app to use Python version `3.4`.</span></span>

```azurecli-interactive
az webapp config set --python-version 3.4 --name <app_name> --resource-group myResourceGroup
```


<span data-ttu-id="ec770-132">이러한 방식으로 Python 버전을 설정하는 것은 플랫폼에서 제공하는 기본 컨테이너를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-132">Setting the Python version this way uses a default container provided by the platform.</span></span> <span data-ttu-id="ec770-133">자신만의 컨테이너를 사용하려면 [az webapp config container set](/cli/azure/webapp/config/container#set) 명령에 대한 CLI 참조를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec770-133">To use your own container, see the CLI reference for the [az webapp config container set](/cli/azure/webapp/config/container#set) command.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 18, done.
Delta compression using up to 4 threads.
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
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-to-the-app"></a><span data-ttu-id="ec770-134">앱으로 이동</span><span class="sxs-lookup"><span data-stu-id="ec770-134">Browse to the app</span></span>

<span data-ttu-id="ec770-135">웹 브라우저를 사용하여 배포된 응용 프로그램으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-135">Browse to the deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="ec770-136">Python 샘플 코드는 Azure App Service 웹앱에서 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-136">The Python sample code is running in an Azure App Service web app.</span></span>

![Azure에서 실행되는 샘플 앱](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="ec770-138">**축하합니다.**</span><span class="sxs-lookup"><span data-stu-id="ec770-138">**Congratulations!**</span></span> <span data-ttu-id="ec770-139">App Service에 첫 번째 Python 앱을 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-139">You've deployed your first Python app to App Service.</span></span>

## <a name="update-and-redeploy-the-code"></a><span data-ttu-id="ec770-140">코드 업데이트 및 다시 배포</span><span class="sxs-lookup"><span data-stu-id="ec770-140">Update and redeploy the code</span></span>

<span data-ttu-id="ec770-141">로컬 텍스트 편집기를 사용하여 Python 앱에서 `main.py` 파일을 열고 `return` 문 옆의 텍스트를 약간 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-141">Using a local text editor, open the `main.py` file in the Python app, and make a small change to the text next to the `return` statement:</span></span>

```python
return 'Hello, Azure!'
```

<span data-ttu-id="ec770-142">Git에서 변경 내용을 커밋한 다음 Azure에 코드 변경 내용을 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-142">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="ec770-143">배포가 완료되면 [앱으로 이동](#browse-to-the-app) 단계에서 열린 브라우저 창으로 다시 전환하고 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-143">Once deployment has completed, switch back to the browser window that opened in the [Browse to the app](#browse-to-the-app) step, and refresh the page.</span></span>

![Azure에서 실행되는 업데이트된 샘플 앱](media/app-service-web-get-started-python/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="ec770-145">새로운 Azure 웹앱 관리</span><span class="sxs-lookup"><span data-stu-id="ec770-145">Manage your new Azure web app</span></span>

<span data-ttu-id="ec770-146">만든 웹앱을 관리하려면 <a href="https://portal.azure.com" target="_blank">Azure Portal</a>로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-146">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="ec770-147">왼쪽 메뉴에서 **App Services**를 클릭한 다음 Azure 웹앱의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-147">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Azure 웹앱에 대한 포털 탐색](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="ec770-149">웹앱의 개요 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-149">You see your web app's Overview page.</span></span> <span data-ttu-id="ec770-150">여기에서 찾아보기, 중지, 시작, 다시 시작, 삭제와 같은 기본 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-150">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Azure Portal의 App Service 블레이드](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="ec770-152">왼쪽 메뉴는 앱 구성을 위한 서로 다른 페이지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ec770-152">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="ec770-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ec770-153">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ec770-154">PostgreSQL을 사용하는 Python</span><span class="sxs-lookup"><span data-stu-id="ec770-154">Python with PostgreSQL</span></span>](app-service-web-tutorial-docker-python-postgresql-app.md)
