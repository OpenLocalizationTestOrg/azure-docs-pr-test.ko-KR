---
title: "Linux에서 Azure 웹 앱과 함께 배포 aaaContinuous | Microsoft Docs"
description: "어떻게 toosetup Linux에서 Azure 웹 앱에서 연속 배포 합니다."
keywords: azure app service, linux, oss, acr
services: app-service
documentationcenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: a47fb43a-bbbd-4751-bdc1-cd382eae49f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: f94d837e27605da58428f507ab2b0eb3af3297e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a><span data-ttu-id="2468a-104">Linux에서 Azure Web App을 사용한 연속 배포</span><span class="sxs-lookup"><span data-stu-id="2468a-104">Continuous deployment with Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="2468a-105">이 자습서에서는 관리되는 [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) 리포지토리 또는 [Docker 허브](https://hub.docker.com)에서 사용자 지정 컨테이너 이미지에 대한 연속 배포를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2468a-105">In this tutorial, you configure continuous deployment for a custom container image from Managed [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) repositories or [Docker Hub](https://hub.docker.com).</span></span>

## <a name="step-1---sign-in-tooazure"></a><span data-ttu-id="2468a-106">1 단계-tooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="2468a-106">Step 1 - Sign in tooAzure</span></span>

<span data-ttu-id="2468a-107">Azure 포털에서 http://portal.azure.com toohello에 로그인</span><span class="sxs-lookup"><span data-stu-id="2468a-107">Sign in toohello Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---enable-container-continuous-deployment-feature"></a><span data-ttu-id="2468a-108">2단계 - 컨테이너 연속 배포 기능 사용</span><span class="sxs-lookup"><span data-stu-id="2468a-108">Step 2 - Enable container continuous deployment feature</span></span>

<span data-ttu-id="2468a-109">사용 하 여 hello 연속 배포 기능을 활성화할 수 있습니다 [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) hello 다음 명령을 실행 하 고</span><span class="sxs-lookup"><span data-stu-id="2468a-109">You can enable hello continuous deployment feature using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing hello following command</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

<span data-ttu-id="2468a-110">Hello에  **[Azure 포털](https://portal.azure.com/)**, hello 클릭 **앱 서비스** hello 창의 hello 왼쪽의 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="2468a-110">In hello **[Azure portal](https://portal.azure.com/)**, click hello **App Service** option on hello left of hello page.</span></span>

<span data-ttu-id="2468a-111">Tooconfigure Docker 허브에 대 한 연속 배포 하려는 앱의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2468a-111">Click on hello name of your app that you want tooconfigure Docker Hub continuous deployment for.</span></span>

<span data-ttu-id="2468a-112">Hello에 **앱 설정**, 라고 앱 추가 `DOCKER_ENABLE_CI` hello 값을 가진 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="2468a-112">In hello **App settings**, add an app setting called `DOCKER_ENABLE_CI` with hello value `true`.</span></span>

![앱 설정 이미지 삽입](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a><span data-ttu-id="2468a-114">3단계 - 웹후크 URL 준비</span><span class="sxs-lookup"><span data-stu-id="2468a-114">Step 3 - Prepare Webhook URL</span></span>

<span data-ttu-id="2468a-115">사용 하 여 hello Webhook URL을 가져올 수 있습니다 [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) hello 다음 명령을 실행 하 고</span><span class="sxs-lookup"><span data-stu-id="2468a-115">You can obtain hello Webhook URL using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing hello following command</span></span>

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

<span data-ttu-id="2468a-116">다음 끝점 toohave hello hello Webhook URL에 대 한 필요한: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`합니다.</span><span class="sxs-lookup"><span data-stu-id="2468a-116">For hello Webhook URL, you need toohave hello following endpoint: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span></span>

<span data-ttu-id="2468a-117">가져올 수 있습니다 프로그램 `publishingusername` 및 `publishingpwd` hello 웹 앱을 다운로드 하 여 hello Azure 포털을 사용 하 여 프로필을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2468a-117">You can obtain your `publishingusername` and `publishingpwd` by downloading hello web app publish profile using hello Azure portal.</span></span>

![웹후크 추가 이미지 2 삽입](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a><span data-ttu-id="2468a-119">4단계: 웹후크 추가</span><span class="sxs-lookup"><span data-stu-id="2468a-119">Step 4 - Add a web hook</span></span>

### <a name="azure-container-registry"></a><span data-ttu-id="2468a-120">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="2468a-120">Azure Container Registry</span></span>

<span data-ttu-id="2468a-121">레지스트리 포털 블레이드에서 **웹후크**를 클릭하고 **추가**를 클릭하여 새 웹후크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2468a-121">In your registry portal blade, click **Webhooks**, create a new webhook by clicking **Add**.</span></span> <span data-ttu-id="2468a-122">Hello에 **webhook 만들기** 블레이드에서 프로그램 webhook에 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2468a-122">In hello **Create webhook** blade, give your webhook a name.</span></span> <span data-ttu-id="2468a-123">가져온 tooprovide hello URL hello Webhook URI에 대 한 필요한 **3 단계**</span><span class="sxs-lookup"><span data-stu-id="2468a-123">For hello Webhook URI, you need tooprovide hello URL obtained from **Step 3**</span></span>

<span data-ttu-id="2468a-124">컨테이너 이미지를 포함 하는 리포지토리의 hello으로 hello 범위를 정의 하는 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2468a-124">Make sure that you define hello scope as hello repo that contains your container image.</span></span>

![웹후크 이미지 삽입](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

<span data-ttu-id="2468a-126">Hello 이미지를 업데이트 하는 경우 hello 새 이미지로 hello 웹 응용 프로그램 자동으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2468a-126">When hello image gets updated, hello web app get updated automatically with hello new image.</span></span>

### <a name="docker-hub"></a><span data-ttu-id="2468a-127">Docker 허브</span><span class="sxs-lookup"><span data-stu-id="2468a-127">Docker Hub</span></span>

<span data-ttu-id="2468a-128">Docker 허브 페이지에서 **웹후크**를 클릭한 후 **웹후크 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2468a-128">In your Docker Hub page, click **Webhooks**, then **CREATE A WEBHOOK**.</span></span>

![웹후크 추가 이미지 1 삽입](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

<span data-ttu-id="2468a-130">가져온 tooprovide hello URL hello Webhook URL에 대 한 필요한 **3 단계**</span><span class="sxs-lookup"><span data-stu-id="2468a-130">For hello Webhook URL, you need tooprovide hello URL obtained from **Step 3**</span></span>

![웹후크 추가 이미지 2 삽입](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

<span data-ttu-id="2468a-132">Hello 이미지를 업데이트 하는 경우 hello 새 이미지로 hello 웹 응용 프로그램 자동으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2468a-132">When hello image gets updated, hello web app get updated automatically with hello new image.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2468a-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2468a-133">Next steps</span></span>
* [<span data-ttu-id="2468a-134">Linux에서 Azure Web App이란?</span><span class="sxs-lookup"><span data-stu-id="2468a-134">What is Azure Web App on Linux?</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="2468a-135">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="2468a-135">Azure Container Registry</span></span>](https://azure.microsoft.com/en-us/services/container-registry/)
* [<span data-ttu-id="2468a-136">Linux의 Azure Web App에서 Node.js용 PM2 구성 사용</span><span class="sxs-lookup"><span data-stu-id="2468a-136">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="2468a-137">Linux의 Azure Web App에서 .NET Core 사용</span><span class="sxs-lookup"><span data-stu-id="2468a-137">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="2468a-138">Linux의 Azure Web App에서 Ruby 사용</span><span class="sxs-lookup"><span data-stu-id="2468a-138">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="2468a-139">Linux에서 Azure 웹 앱에 대 한 사용자 지정 Docker toouse 이미지 방법</span><span class="sxs-lookup"><span data-stu-id="2468a-139">How toouse a custom Docker image for Azure Web App on Linux</span></span>](./app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="2468a-140">Linux의 Azure App Service Web App에 대한 FAQ</span><span class="sxs-lookup"><span data-stu-id="2468a-140">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md) 
* [<span data-ttu-id="2468a-141">Azure CLI 2.0을 사용하여 Linux에서 웹앱 관리</span><span class="sxs-lookup"><span data-stu-id="2468a-141">Manage Web App on Linux using Azure CLI 2.0</span></span>](./app-service-linux-cli.md)



