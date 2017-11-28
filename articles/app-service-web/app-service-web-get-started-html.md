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
# <a name="create-a-static-html-web-app-in-azure"></a><span data-ttu-id="d2b49-103">Azure에서 정적 HTML 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="d2b49-103">Create a static HTML web app in Azure</span></span>

<span data-ttu-id="d2b49-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b49-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="d2b49-105">이 퀵 스타트의 toodeploy 기본 HTML + CSS tooAzure 웹 앱 사이트 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2b49-105">This quickstart shows how toodeploy a basic HTML+CSS site tooAzure Web Apps.</span></span> <span data-ttu-id="d2b49-106">Hello를 사용 하 여 hello 웹 앱을 만드는 [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), Git toodeploy 샘플 HTML 콘텐츠 toohello 웹 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b49-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample HTML content toohello web app.</span></span>

![샘플 앱의 홈 페이지](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="d2b49-108">Mac, Windows 또는 Linux 컴퓨터를 사용 하 여 아래 hello 단계를 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2b49-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="d2b49-109">Hello 필수 구성 요소가 설치 되 면 약 5 분 toocomplete hello 단계가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b49-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2b49-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d2b49-110">Prerequisites</span></span>

<span data-ttu-id="d2b49-111">toocomplete이 빠른이 시작:</span><span class="sxs-lookup"><span data-stu-id="d2b49-111">toocomplete this quickstart:</span></span>

- <span data-ttu-id="d2b49-112">[Git 설치](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span><span class="sxs-lookup"><span data-stu-id="d2b49-112">[Install Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d2b49-113">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b49-113">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d2b49-114">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b49-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="d2b49-115">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b49-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="d2b49-116">Hello 샘플 다운로드</span><span class="sxs-lookup"><span data-stu-id="d2b49-116">Download hello sample</span></span>

<span data-ttu-id="d2b49-117">터미널 창에서 hello 명령 tooclone hello 샘플 응용 프로그램 저장소 tooyour 로컬 컴퓨터에 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b49-117">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

<span data-ttu-id="d2b49-118">이 퀵 스타트의이 터미널 윈도우 toorun 모든 hello 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b49-118">You use this terminal window toorun all hello commands in this quickstart.</span></span>

## <a name="view-hello-html"></a><span data-ttu-id="d2b49-119">HTML 보기 hello</span><span class="sxs-lookup"><span data-stu-id="d2b49-119">View hello HTML</span></span>

<span data-ttu-id="d2b49-120">Hello 샘플 HTML 있는 toohello 디렉터리를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b49-120">Navigate toohello directory that contains hello sample HTML.</span></span> <span data-ttu-id="d2b49-121">열기 hello *index.html* 브라우저에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b49-121">Open hello *index.html* file in your browser.</span></span>

![샘플 앱 홈 페이지](media/app-service-web-get-started-html/hello-world-in-browser.png)

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![빈 웹앱 페이지](media/app-service-web-get-started-html/app-service-web-service-created.png)

<span data-ttu-id="d2b49-124">Azure에서 비어 있는 새 웹앱을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="d2b49-124">You’ve created an empty new web app in Azure.</span></span>

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

## <a name="browse-toohello-app"></a><span data-ttu-id="d2b49-125">Toohello 응용 프로그램 찾아보기</span><span class="sxs-lookup"><span data-stu-id="d2b49-125">Browse toohello app</span></span>

<span data-ttu-id="d2b49-126">브라우저에서 toohello Azure 웹 앱 URL을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b49-126">In a browser, go toohello Azure web app URL:</span></span>

```
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="d2b49-127">Azure 앱 서비스 웹 앱으로 hello 페이지 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b49-127">hello page is running as an Azure App Service web app.</span></span>

![샘플 앱 홈 페이지](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="d2b49-129">**축하합니다.**</span><span class="sxs-lookup"><span data-stu-id="d2b49-129">**Congratulations!**</span></span> <span data-ttu-id="d2b49-130">배포한 프로그램 첫 번째 HTML 응용 프로그램 tooApp 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b49-130">You've deployed your first HTML app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-app"></a><span data-ttu-id="d2b49-131">업데이트 하 고 hello 응용 프로그램을 다시 배포</span><span class="sxs-lookup"><span data-stu-id="d2b49-131">Update and redeploy hello app</span></span>

<span data-ttu-id="d2b49-132">열기 hello *index.html* 텍스트 편집기에서 파일을 변경 toohello 태그를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b49-132">Open hello *index.html* file in a text editor, and make a change toohello markup.</span></span> <span data-ttu-id="d2b49-133">예를 들어, "Azure 앱 서비스-샘플 정적 HTML 사이트" toojust에서 hello H1 제목을 변경 "Azure 앱 서비스 '.</span><span class="sxs-lookup"><span data-stu-id="d2b49-133">For example, change hello H1 heading from "Azure App Service - Sample Static HTML Site" toojust "Azure App Service\`.</span></span>

<span data-ttu-id="d2b49-134">Git에서 변경 내용을 커밋하고 hello 코드 변경 내용을 tooAzure 푸시하고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b49-134">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated HTML"
git push azure master
```

<span data-ttu-id="d2b49-135">배포가 완료 되 면 브라우저 toosee hello 변경을 내용을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="d2b49-135">Once deployment has completed, refresh your browser toosee hello changes.</span></span>

![업데이트된 샘플 앱 홈 페이지](media/app-service-web-get-started-html/hello-azure-in-browser-az.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="d2b49-137">새로운 Azure 웹앱 관리</span><span class="sxs-lookup"><span data-stu-id="d2b49-137">Manage your new Azure web app</span></span>

<span data-ttu-id="d2b49-138">Toohello 이동 <a href="https://portal.azure.com" target="_blank">Azure 포털</a> 만든 toomanage hello 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b49-138">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="d2b49-139">Hello 왼쪽된 메뉴에서 클릭 **응용 프로그램 서비스**, Azure 웹 앱의 hello 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2b49-139">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![포털 탐색 tooAzure 웹 응용 프로그램](./media/app-service-web-get-started-html/portal1.png)

<span data-ttu-id="d2b49-141">웹앱의 개요 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2b49-141">You see your web app's Overview page.</span></span> <span data-ttu-id="d2b49-142">여기에서 찾아보기, 중지, 시작, 다시 시작, 삭제와 같은 기본 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2b49-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Azure Portal의 App Service 블레이드](./media/app-service-web-get-started-html/portal2.png)

<span data-ttu-id="d2b49-144">왼쪽된 메뉴 hello 응용 프로그램을 구성 하는 서로 다른 페이지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b49-144">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="d2b49-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d2b49-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d2b49-146">사용자 지정 도메인 매핑</span><span class="sxs-lookup"><span data-stu-id="d2b49-146">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
