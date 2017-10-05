---
title: "Linux에서 Azure Web App을 사용한 연속 배포 | Microsoft Docs"
description: "Linux의 Azure Web App에서 연속 배포를 설정하는 방법"
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
ms.openlocfilehash: f8f7d51003f8a55b7f51e8cc2cea838e8e5a6196
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a><span data-ttu-id="e3297-104">Linux에서 Azure Web App을 사용한 연속 배포</span><span class="sxs-lookup"><span data-stu-id="e3297-104">Continuous deployment with Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="e3297-105">이 자습서에서는 관리되는 [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) 리포지토리 또는 [Docker 허브](https://hub.docker.com)에서 사용자 지정 컨테이너 이미지에 대한 연속 배포를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e3297-105">In this tutorial, you configure continuous deployment for a custom container image from Managed [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) repositories or [Docker Hub](https://hub.docker.com).</span></span>

## <a name="step-1---sign-in-to-azure"></a><span data-ttu-id="e3297-106">1단계 - Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="e3297-106">Step 1 - Sign in to Azure</span></span>

<span data-ttu-id="e3297-107">Azure Portal( http://portal.azure.com )에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e3297-107">Sign in to the Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---enable-container-continuous-deployment-feature"></a><span data-ttu-id="e3297-108">2단계 - 컨테이너 연속 배포 기능 사용</span><span class="sxs-lookup"><span data-stu-id="e3297-108">Step 2 - Enable container continuous deployment feature</span></span>

<span data-ttu-id="e3297-109">[Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)를 사용하고 다음 명령을 실행하여 연속 배포 기능을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3297-109">You can enable the continuous deployment feature using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing the following command</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

<span data-ttu-id="e3297-110">**[Azure Portal](https://portal.azure.com/)**에서 페이지 왼쪽의 **App Service** 옵션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e3297-110">In the **[Azure portal](https://portal.azure.com/)**, click the **App Service** option on the left of the page.</span></span>

<span data-ttu-id="e3297-111">Docker 허브 연속 배포를 구성하려는 앱의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e3297-111">Click on the name of your app that you want to configure Docker Hub continuous deployment for.</span></span>

<span data-ttu-id="e3297-112">**앱 설정**에서 `true` 값을 갖는 `DOCKER_ENABLE_CI`라는 앱을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e3297-112">In the **App settings**, add an app setting called `DOCKER_ENABLE_CI` with the value `true`.</span></span>

![앱 설정 이미지 삽입](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a><span data-ttu-id="e3297-114">3단계 - 웹후크 URL 준비</span><span class="sxs-lookup"><span data-stu-id="e3297-114">Step 3 - Prepare Webhook URL</span></span>

<span data-ttu-id="e3297-115">[Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)를 사용하고 다음 명령을 실행하여 웹후크 URL을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3297-115">You can obtain the Webhook URL using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing the following command</span></span>

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

<span data-ttu-id="e3297-116">웹후크 URL에는 끝점 `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e3297-116">For the Webhook URL, you need to have the following endpoint: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span></span>

<span data-ttu-id="e3297-117">Azure Portal에서 웹앱 게시 프로필을 다운로드하여 `publishingusername` 및 `publishingpwd`를 구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3297-117">You can obtain your `publishingusername` and `publishingpwd` by downloading the web app publish profile using the Azure portal.</span></span>

![웹후크 추가 이미지 2 삽입](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a><span data-ttu-id="e3297-119">4단계: 웹후크 추가</span><span class="sxs-lookup"><span data-stu-id="e3297-119">Step 4 - Add a web hook</span></span>

### <a name="azure-container-registry"></a><span data-ttu-id="e3297-120">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="e3297-120">Azure Container Registry</span></span>

<span data-ttu-id="e3297-121">레지스트리 포털 블레이드에서 **웹후크**를 클릭하고 **추가**를 클릭하여 새 웹후크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e3297-121">In your registry portal blade, click **Webhooks**, create a new webhook by clicking **Add**.</span></span> <span data-ttu-id="e3297-122">**웹후크 만들기** 블레이드에서 웹후크에 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e3297-122">In the **Create webhook** blade, give your webhook a name.</span></span> <span data-ttu-id="e3297-123">웹후크 URI에 **3단계**에서 가져온 URL을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3297-123">For the Webhook URI, you need to provide the URL obtained from **Step 3**</span></span>

<span data-ttu-id="e3297-124">범위를 컨테이너 이미지를 포함하는 리포지토리로 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3297-124">Make sure that you define the scope as the repo that contains your container image.</span></span>

![웹후크 이미지 삽입](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

<span data-ttu-id="e3297-126">이미지를 업데이트할 때 자동으로 웹앱이 새 이미지로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3297-126">When the image gets updated, the web app get updated automatically with the new image.</span></span>

### <a name="docker-hub"></a><span data-ttu-id="e3297-127">Docker 허브</span><span class="sxs-lookup"><span data-stu-id="e3297-127">Docker Hub</span></span>

<span data-ttu-id="e3297-128">Docker 허브 페이지에서 **웹후크**를 클릭한 후 **웹후크 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e3297-128">In your Docker Hub page, click **Webhooks**, then **CREATE A WEBHOOK**.</span></span>

![웹후크 추가 이미지 1 삽입](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

<span data-ttu-id="e3297-130">웹후크 URL에 **3단계**에서 가져온 URL을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3297-130">For the Webhook URL, you need to provide the URL obtained from **Step 3**</span></span>

![웹후크 추가 이미지 2 삽입](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

<span data-ttu-id="e3297-132">이미지를 업데이트할 때 자동으로 웹앱이 새 이미지로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3297-132">When the image gets updated, the web app get updated automatically with the new image.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3297-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e3297-133">Next steps</span></span>
* [<span data-ttu-id="e3297-134">Linux에서 Azure Web App이란?</span><span class="sxs-lookup"><span data-stu-id="e3297-134">What is Azure Web App on Linux?</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="e3297-135">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="e3297-135">Azure Container Registry</span></span>](https://azure.microsoft.com/en-us/services/container-registry/)
* [<span data-ttu-id="e3297-136">Linux의 Azure Web App에서 Node.js용 PM2 구성 사용</span><span class="sxs-lookup"><span data-stu-id="e3297-136">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="e3297-137">Linux의 Azure Web App에서 .NET Core 사용</span><span class="sxs-lookup"><span data-stu-id="e3297-137">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="e3297-138">Linux의 Azure Web App에서 Ruby 사용</span><span class="sxs-lookup"><span data-stu-id="e3297-138">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="e3297-139">Linux에서 Azure Web App에 대한 사용자 지정 Docker 이미지를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="e3297-139">How to use a custom Docker image for Azure Web App on Linux</span></span>](./app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="e3297-140">Linux의 Azure App Service Web App에 대한 FAQ</span><span class="sxs-lookup"><span data-stu-id="e3297-140">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md) 
* [<span data-ttu-id="e3297-141">Azure CLI 2.0을 사용하여 Linux에서 웹앱 관리</span><span class="sxs-lookup"><span data-stu-id="e3297-141">Manage Web App on Linux using Azure CLI 2.0</span></span>](./app-service-linux-cli.md)



