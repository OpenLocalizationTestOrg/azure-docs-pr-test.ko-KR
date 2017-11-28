---
title: "첫 번째 Azure Container Instances 컨테이너 만들기 | Azure Docs"
description: "Azure Container Instances 배포 및 시작"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 905f69e5e1e237a31d9bb1e326969ec83292c244
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-your-first-container-in-azure-container-instances"></a><span data-ttu-id="110ac-103">Azure Container Instances에서 첫 번째 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="110ac-103">Create your first container in Azure Container Instances</span></span>

<span data-ttu-id="110ac-104">Azure Container Instances를 통해 Azure에서 컨테이너를 쉽게 만들고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="110ac-104">Azure Container Instances makes it easy to create and manage containers in Azure.</span></span> <span data-ttu-id="110ac-105">이 빠른 시작에서는 Azure에서 컨테이너를 만들고 공용 IP 주소를 사용하여 인터넷에 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="110ac-105">In this quick start, you will create a container in Azure and expose it to the internet with a public IP address.</span></span> <span data-ttu-id="110ac-106">이 작업은 단일 명령으로 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="110ac-106">This operation is completed in a single command.</span></span> <span data-ttu-id="110ac-107">몇 초 내에 브라우저에 이 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="110ac-107">Within just a few seconds, you will see this in your browser:</span></span>

![Azure Container Instances를 사용하여 배포된 앱이 브라우저에 표시됨][aci-app-browser]

<span data-ttu-id="110ac-109">Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="110ac-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="110ac-110">CLI를 로컬로 설치하여 사용하도록 선택하는 경우 이 빠른 시작에서 Azure CLI 버전 2.0.12 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="110ac-110">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.12 or later.</span></span> <span data-ttu-id="110ac-111">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="110ac-111">Run `az --version` to find the version.</span></span> <span data-ttu-id="110ac-112">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="110ac-112">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="110ac-113">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="110ac-113">Create a resource group</span></span>

<span data-ttu-id="110ac-114">Azure Container Instances는 Azure 리소스이며 Azure 리소스 그룹, Azure 리소스가 배포 및 관리되는 논리적 컬렉션에 배치되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="110ac-114">Azure Container Instances are Azure resources and must be placed in an Azure resource group, a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="110ac-115">[az group create](/cli/azure/group#create) 명령을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="110ac-115">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="110ac-116">다음 예제에서는 *eastus* 위치에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="110ac-116">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a><span data-ttu-id="110ac-117">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="110ac-117">Create a container</span></span>

<span data-ttu-id="110ac-118">이름, Docker 이미지 및 Azure 리소스 그룹을 제공하여 컨테이너를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="110ac-118">You can create a container by providing a name, a Docker image, and an Azure resource group.</span></span> <span data-ttu-id="110ac-119">선택적으로 공용 IP 주소로 컨테이너를 인터넷에 공개할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="110ac-119">You can optionally expose the container to the internet with a public IP address.</span></span> <span data-ttu-id="110ac-120">이 경우 [Node.js](http://nodejs.org)에 작성된 매우 간단한 웹앱을 호스트하는 컨테이너를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="110ac-120">In this case, we'll use a container that hosts a very simple web app written in [Node.js](http://nodejs.org).</span></span>

```azurecli-interactive
az container create --name mycontainer --image microsoft/aci-helloworld --resource-group myResourceGroup --ip-address public 
```

<span data-ttu-id="110ac-121">몇 초 안에 요청에 대한 응답을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="110ac-121">Within a few seconds, you should get a response to your request.</span></span> <span data-ttu-id="110ac-122">처음에는 컨테이너가 **만드는 중** 상태가 되지만 몇 초 이내 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="110ac-122">Initially, the container will be in a **Creating** state, but it should start within a few seconds.</span></span> <span data-ttu-id="110ac-123">`show` 명령을 사용하여 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="110ac-123">You can check the status using the `show` command:</span></span>

```azurecli-interactive
az container show --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="110ac-124">출력 맨 아래에 컨테이너의 프로비전 상태와 해당 IP 주소가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="110ac-124">At the bottom of the output, you will see the container's provisioning state and its IP address:</span></span>

```json
...
"ipAddress": {
      "ip": "13.88.8.148",
      "ports": [
        {
          "port": 80,
          "protocol": "TCP"
        }
      ]
    },
    "osType": "Linux",
    "provisioningState": "Succeeded"
...
```

<span data-ttu-id="110ac-125">컨테이너가 **성공함** 상태로 전환되면 제공된 IP 주소를 사용하여 브라우저에 도달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="110ac-125">Once the container moves to the **Succeeded** state, you can reach it in the browser using the IP address provided.</span></span> 

![Azure Container Instances를 사용하여 배포된 앱이 브라우저에 표시됨][aci-app-browser]

## <a name="pull-the-container-logs"></a><span data-ttu-id="110ac-127">컨테이너 로그 끌어오기</span><span class="sxs-lookup"><span data-stu-id="110ac-127">Pull the container logs</span></span>

<span data-ttu-id="110ac-128">`logs` 명령을 사용하여 만든 컨테이너의 로그를 끌어올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="110ac-128">You can pull the logs for the container you created using the `logs` command:</span></span>

```azurecli-interactive
az container logs --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="110ac-129">출력:</span><span class="sxs-lookup"><span data-stu-id="110ac-129">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://104.210.39.122/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="delete-the-container"></a><span data-ttu-id="110ac-130">컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="110ac-130">Delete the container</span></span>

<span data-ttu-id="110ac-131">컨테이너 작업을 완료했으면 `delete` 명령을 사용하여 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="110ac-131">When you are done with the container, you can remove it using the `delete` command:</span></span>

```azurecli-interactive
az container delete --name mycontainer --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="110ac-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="110ac-132">Next steps</span></span>

<span data-ttu-id="110ac-133">이 빠른 시작에 사용된 컨테이너의 모든 코드는 Dockerfile과 함께 [GitHub][app-github-repo]에서 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="110ac-133">All of the code for the container used in this quick start is available [on GitHub][app-github-repo], along with its Dockerfile.</span></span> <span data-ttu-id="110ac-134">직접 빌드하고 Azure Container Registry를 사용하여 Azure Container Instances에 배포하려면 Azure Container Instances 자습서를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="110ac-134">If you'd like to try building it yourself and deploying it to Azure Container Instances using the Azure Container Registry, continue to the Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="110ac-135">Azure Container Instances 자습서</span><span class="sxs-lookup"><span data-stu-id="110ac-135">Azure Container Instances tutorials</span></span>](./container-instances-tutorial-prepare-app.md)


<!-- LINKS -->
[app-github-repo]: https://github.com/Azure-Samples/aci-helloworld.git

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png