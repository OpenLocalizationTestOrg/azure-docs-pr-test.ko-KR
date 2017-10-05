---
title: "Azure Container Instances 자습서 - 앱 배포 | Microsoft Docs"
description: "Azure Container Instances 자습서 - 앱 배포"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 54151a5c1850ab7120fe666a46dc5dc99c0f5157
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-container-to-azure-container-instances"></a><span data-ttu-id="57fa3-103">Azure Container Instances에 컨테이너 배포</span><span class="sxs-lookup"><span data-stu-id="57fa3-103">Deploy a container to Azure Container Instances</span></span>

<span data-ttu-id="57fa3-104">세 부분으로 이루어진 자습서의 마지막 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="57fa3-104">This is the last of a three-part tutorial.</span></span> <span data-ttu-id="57fa3-105">이전 섹션에서는 [컨테이너 이미지를 만들어](container-instances-tutorial-prepare-app.md) [Azure Container Registry에 푸시했습니다](container-instances-tutorial-prepare-acr.md).</span><span class="sxs-lookup"><span data-stu-id="57fa3-105">In previous sections, [a container image was created](container-instances-tutorial-prepare-app.md) and [pushed to an Azure Container Registry](container-instances-tutorial-prepare-acr.md).</span></span> <span data-ttu-id="57fa3-106">이 섹션에서는 Azure Container Instances에 컨테이너를 배포하여 이 자습서를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="57fa3-106">This section completes the tutorial by deploying the container to Azure Container Instances.</span></span> <span data-ttu-id="57fa3-107">완료되는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="57fa3-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="57fa3-108">Azure Resource Manager 템플릿을 사용하여 컨테이너 그룹 정의</span><span class="sxs-lookup"><span data-stu-id="57fa3-108">Defining a container group using an Azure Resource Manager template</span></span>
> * <span data-ttu-id="57fa3-109">Azure CLI를 사용하여 컨테이너 그룹 배포</span><span class="sxs-lookup"><span data-stu-id="57fa3-109">Deploying the container group using the Azure CLI</span></span>
> * <span data-ttu-id="57fa3-110">컨테이너 로그 보기</span><span class="sxs-lookup"><span data-stu-id="57fa3-110">Viewing container logs</span></span>

## <a name="deploy-the-container-using-the-azure-cli"></a><span data-ttu-id="57fa3-111">Azure CLI를 사용하여 컨테이너 배포</span><span class="sxs-lookup"><span data-stu-id="57fa3-111">Deploy the container using the Azure CLI</span></span>

<span data-ttu-id="57fa3-112">Azure CLI를 통해 단일 명령으로 Azure Container Instances에 컨테이너를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57fa3-112">The Azure CLI enables deployment of a container to Azure Container Instances in a single command.</span></span> <span data-ttu-id="57fa3-113">컨테이너 이미지가 개인 Azure Container Registry에 호스트되기 때문에 액세스하는 데 필요한 자격 증명을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57fa3-113">Since the container image is hosted in the private Azure Container Registry, you must include the credentials required to access it.</span></span> <span data-ttu-id="57fa3-114">필요한 경우 아래와 같이 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57fa3-114">If necessary, you can query them as shown below.</span></span>

<span data-ttu-id="57fa3-115">컨테이너 레지스트리 로그인 서버(레지스트리 이름을 업데이트):</span><span class="sxs-lookup"><span data-stu-id="57fa3-115">Container registry login server (update with your registry name):</span></span>

```azurecli-interactive
az acr show --name <acrName> --query loginServer
```

<span data-ttu-id="57fa3-116">컨테이너 레지스트리 암호:</span><span class="sxs-lookup"><span data-stu-id="57fa3-116">Container registry password:</span></span>

```azurecli-interactive
az acr credential show --name <acrName> --query "passwords[0].value"
```

<span data-ttu-id="57fa3-117">1개의 CPU 코어 및 1GB 메모리의 리소스를 요청하는 컨테이너 레지스트리에서 컨테이너 이미지를 배포하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="57fa3-117">To deploy your container image from the container registry with a resource request of 1 CPU core and 1GB of memory, run the following command:</span></span>

```azurecli-interactive
az container create --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-password <acrPassword> --ip-address public -g myResourceGroup
```

<span data-ttu-id="57fa3-118">몇 초 정도 지나면 Azure Resource Manager에서 초기 응답이 수신됩니다.</span><span class="sxs-lookup"><span data-stu-id="57fa3-118">Within a few seconds, you will receive an initial response from Azure Resource Manager.</span></span> <span data-ttu-id="57fa3-119">배포 상태를 확인하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="57fa3-119">To view the state of the deployment, use:</span></span>

```azurecli-interactive
az container show --name aci-tutorial-app --resource-group myResourceGroup --query state
```

<span data-ttu-id="57fa3-120">상태가 *보류 중*에서 *실행 중*으로 변경될 때까지 이 명령을 계속 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57fa3-120">We can continue running this command until the state changes from *pending* to *running*.</span></span> <span data-ttu-id="57fa3-121">그런 다음, 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57fa3-121">Then we can proceed.</span></span>

## <a name="view-the-application-and-container-logs"></a><span data-ttu-id="57fa3-122">응용 프로그램 및 컨테이너 로그 보기</span><span class="sxs-lookup"><span data-stu-id="57fa3-122">View the application and container logs</span></span>

<span data-ttu-id="57fa3-123">배포에 성공하면 브라우저를 다음 명령의 출력에 표시되는 IP 주소로 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57fa3-123">Once the deployment succeeds, open your browser to the IP address shown in the output of the following command:</span></span>

```bash
az container show --name aci-tutorial-app --resource-group myResourceGroup --query ipAddress.ip
```

```json
"13.88.176.27"
```

![브라우저의 Hello World 앱][aci-app-browser]

<span data-ttu-id="57fa3-125">또한 컨테이너의 로그 출력을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57fa3-125">You can also view the log output of the container:</span></span>

```azurecli-interactive
az container logs --name aci-tutorial-app -g myResourceGroup
```

<span data-ttu-id="57fa3-126">출력:</span><span class="sxs-lookup"><span data-stu-id="57fa3-126">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://13.88.176.27/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="next-steps"></a><span data-ttu-id="57fa3-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="57fa3-127">Next steps</span></span>

<span data-ttu-id="57fa3-128">이 자습서에서는 Azure Container Instances에 컨테이너를 배포하는 프로세스를 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="57fa3-128">In this tutorial, you completed the process of deploying your containers to Azure Container Instances.</span></span> <span data-ttu-id="57fa3-129">다음 단계가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="57fa3-129">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="57fa3-130">Azure CLI를 사용하여 Azure Container Registry의 컨테이너 배포</span><span class="sxs-lookup"><span data-stu-id="57fa3-130">Deploying the container from the Azure Container Registry using the Azure CLI</span></span>
> * <span data-ttu-id="57fa3-131">브라우저에서 응용 프로그램 보기</span><span class="sxs-lookup"><span data-stu-id="57fa3-131">Viewing the application in the browser</span></span>
> * <span data-ttu-id="57fa3-132">컨테이너 로그 보기</span><span class="sxs-lookup"><span data-stu-id="57fa3-132">Viewing the container logs</span></span>

<!-- LINKS -->
[prepare-app]: ./container-instances-tutorial-prepare-app.md

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png
