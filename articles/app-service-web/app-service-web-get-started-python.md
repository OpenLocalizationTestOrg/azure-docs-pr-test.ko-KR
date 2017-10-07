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
# <a name="create-a-python-web-app-in-azure"></a><span data-ttu-id="dfdca-103">Azure에서 Python 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="dfdca-103">Create a Python web app in Azure</span></span>

<span data-ttu-id="dfdca-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="dfdca-105">이 퀵 스타트의 방법을 안내 toodevelop 및 Python 응용 프로그램 tooAzure 웹 앱을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-105">This quickstart walks through how toodevelop and deploy a Python app tooAzure Web Apps.</span></span> <span data-ttu-id="dfdca-106">Hello를 사용 하 여 hello 웹 앱을 만드는 [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), Git toodeploy 샘플 Python 코드가 toohello 웹 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample Python code toohello web app.</span></span>

![Azure에서 실행되는 샘플 앱](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="dfdca-108">Mac, Windows 또는 Linux 컴퓨터를 사용 하 여 아래 hello 단계를 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="dfdca-109">Hello 필수 구성 요소가 설치 되 면 약 5 분 toocomplete hello 단계가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>
## <a name="prerequisites"></a><span data-ttu-id="dfdca-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="dfdca-110">Prerequisites</span></span>

<span data-ttu-id="dfdca-111">toocomplete이이 자습서:</span><span class="sxs-lookup"><span data-stu-id="dfdca-111">toocomplete this tutorial:</span></span>

1. [<span data-ttu-id="dfdca-112">Git 설치</span><span class="sxs-lookup"><span data-stu-id="dfdca-112">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="dfdca-113">Python 설치</span><span class="sxs-lookup"><span data-stu-id="dfdca-113">Install Python</span></span>](https://www.python.org/downloads/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="dfdca-114">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="dfdca-115">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="dfdca-116">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="dfdca-117">Hello 샘플 다운로드</span><span class="sxs-lookup"><span data-stu-id="dfdca-117">Download hello sample</span></span>

<span data-ttu-id="dfdca-118">터미널 창에서 hello 명령 tooclone hello 샘플 응용 프로그램 저장소 tooyour 로컬 컴퓨터에 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-118">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
```

<span data-ttu-id="dfdca-119">이 퀵 스타트의이 터미널 윈도우 toorun 모든 hello 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-119">You use this terminal window toorun all hello commands in this quickstart.</span></span>

<span data-ttu-id="dfdca-120">Hello 샘플 코드를 있는 toohello 디렉터리를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-120">Change toohello directory that contains hello sample code.</span></span>

```bash
cd Python-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="dfdca-121">Hello 응용 프로그램을 로컬로 실행</span><span class="sxs-lookup"><span data-stu-id="dfdca-121">Run hello app locally</span></span>

<span data-ttu-id="dfdca-122">사용 하 여 필요한 hello 패키지 설치 `pip`합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-122">Install hello required packages using `pip`.</span></span>

```bash
pip install -r requirements.txt
```

<span data-ttu-id="dfdca-123">터미널 윈도우를 열고 hello를 사용 하 여 hello 응용 프로그램을 로컬로 실행 `Python` 명령 toolaunch hello Python 웹 서버 기본 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-123">Run hello application locally by opening a terminal window and using hello `Python` command toolaunch hello built-in Python web server.</span></span>

```bash
python main.py
```

<span data-ttu-id="dfdca-124">웹 브라우저를 열고 http://localhost:5000에서 toohello 샘플 응용 프로그램을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-124">Open a web browser, and navigate toohello sample app at http://localhost:5000.</span></span>

<span data-ttu-id="dfdca-125">Hello 나타나면 **Hello World** hello 페이지에 표시 되는 hello 샘플 응용 프로그램에서 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-125">You can see hello **Hello World** message from hello sample app displayed in hello page.</span></span>

![로컬로 실행되는 샘플 앱](media/app-service-web-get-started-python/localhost-hello-world-in-browser.png)

<span data-ttu-id="dfdca-127">사용자의 터미널 창에서 눌러 **Ctrl + C** tooexit hello 웹 서버.</span><span class="sxs-lookup"><span data-stu-id="dfdca-127">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![빈 웹앱 페이지](media/app-service-web-get-started-python/app-service-web-service-created.png)

<span data-ttu-id="dfdca-129">Azure에서 비어 있는 새 웹앱을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-129">You’ve created an empty new web app in Azure.</span></span>

## <a name="configure-toouse-python"></a><span data-ttu-id="dfdca-130">Python toouse 구성</span><span class="sxs-lookup"><span data-stu-id="dfdca-130">Configure toouse Python</span></span>

<span data-ttu-id="dfdca-131">사용 하 여 hello [az webapp 구성 집합](/cli/azure/webapp/config#set) 명령 tooconfigure hello 웹 응용 프로그램 toouse Python 버전 `3.4`합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-131">Use hello [az webapp config set](/cli/azure/webapp/config#set) command tooconfigure hello web app toouse Python version `3.4`.</span></span>

```azurecli-interactive
az webapp config set --python-version 3.4 --name <app_name> --resource-group myResourceGroup
```


<span data-ttu-id="dfdca-132">이러한 방식으로 hello Python 버전 설정 hello 플랫폼에서 제공 하는 기본 컨테이너를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-132">Setting hello Python version this way uses a default container provided by hello platform.</span></span> <span data-ttu-id="dfdca-133">toouse 고유한 컨테이너 참조 hello hello에 대 한 참조를 CLI [az webapp 구성 컨테이너 세트](/cli/azure/webapp/config/container#set) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-133">toouse your own container, see hello CLI reference for hello [az webapp config container set](/cli/azure/webapp/config/container#set) command.</span></span>

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

## <a name="browse-toohello-app"></a><span data-ttu-id="dfdca-134">Toohello 응용 프로그램 찾아보기</span><span class="sxs-lookup"><span data-stu-id="dfdca-134">Browse toohello app</span></span>

<span data-ttu-id="dfdca-135">찾아보기 toohello 웹 브라우저를 사용 하 여 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-135">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="dfdca-136">hello Python 샘플 코드는 Azure 앱 서비스 웹 앱에서 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-136">hello Python sample code is running in an Azure App Service web app.</span></span>

![Azure에서 실행되는 샘플 앱](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="dfdca-138">**축하합니다.**</span><span class="sxs-lookup"><span data-stu-id="dfdca-138">**Congratulations!**</span></span> <span data-ttu-id="dfdca-139">배포한 프로그램 첫 번째 Python 응용 프로그램 tooApp 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-139">You've deployed your first Python app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-code"></a><span data-ttu-id="dfdca-140">업데이트 하 고 hello 코드를 다시 배포</span><span class="sxs-lookup"><span data-stu-id="dfdca-140">Update and redeploy hello code</span></span>

<span data-ttu-id="dfdca-141">Hello를 열고 로컬 텍스트 편집기를 사용 하 여 `main.py` hello Python 응용 프로그램에서 파일을 작은 변경 toohello 텍스트 다음 toohello 확인 `return` 문:</span><span class="sxs-lookup"><span data-stu-id="dfdca-141">Using a local text editor, open hello `main.py` file in hello Python app, and make a small change toohello text next toohello `return` statement:</span></span>

```python
return 'Hello, Azure!'
```

<span data-ttu-id="dfdca-142">Git에서 변경 내용을 커밋하고 hello 코드 변경 내용을 tooAzure 푸시하고 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-142">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="dfdca-143">배포가 완료 되 면 hello에서 열린 백 toohello 브라우저 창을 전환 [찾아보기 toohello 앱](#browse-to-the-app) 단계 및 새로 고침 hello 페이지.</span><span class="sxs-lookup"><span data-stu-id="dfdca-143">Once deployment has completed, switch back toohello browser window that opened in hello [Browse toohello app](#browse-to-the-app) step, and refresh hello page.</span></span>

![Azure에서 실행되는 업데이트된 샘플 앱](media/app-service-web-get-started-python/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="dfdca-145">새로운 Azure 웹앱 관리</span><span class="sxs-lookup"><span data-stu-id="dfdca-145">Manage your new Azure web app</span></span>

<span data-ttu-id="dfdca-146">Toohello 이동 <a href="https://portal.azure.com" target="_blank">Azure 포털</a> 만든 toomanage hello 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-146">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="dfdca-147">Hello 왼쪽된 메뉴에서 클릭 **응용 프로그램 서비스**, Azure 웹 앱의 hello 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-147">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![포털 탐색 tooAzure 웹 응용 프로그램](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="dfdca-149">웹앱의 개요 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-149">You see your web app's Overview page.</span></span> <span data-ttu-id="dfdca-150">여기에서 찾아보기, 중지, 시작, 다시 시작, 삭제와 같은 기본 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-150">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Azure Portal의 App Service 블레이드](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="dfdca-152">왼쪽된 메뉴 hello 응용 프로그램을 구성 하는 서로 다른 페이지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdca-152">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="dfdca-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dfdca-153">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dfdca-154">PostgreSQL을 사용하는 Python</span><span class="sxs-lookup"><span data-stu-id="dfdca-154">Python with PostgreSQL</span></span>](app-service-web-tutorial-docker-python-postgresql-app.md)
