---
title: "aaaCreate 첫 번째 Azure 컨테이너 인스턴스 컨테이너 | Azure 문서"
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
ms.openlocfilehash: b57c52714933bd3b28c44d33f9af7cd1f23fb951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-container-in-azure-container-instances"></a><span data-ttu-id="09bb0-103">Azure Container Instances에서 첫 번째 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="09bb0-103">Create your first container in Azure Container Instances</span></span>

<span data-ttu-id="09bb0-104">Azure 컨테이너 인스턴스를 쉽게 toocreate 있고 Azure에서 컨테이너를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="09bb0-104">Azure Container Instances makes it easy toocreate and manage containers in Azure.</span></span> <span data-ttu-id="09bb0-105">이 빠른 시작에서 컨테이너를 Azure에서 만들고 toohello 노출 공용 IP 주소를 사용 하 여 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="09bb0-105">In this quick start, you will create a container in Azure and expose it toohello internet with a public IP address.</span></span> <span data-ttu-id="09bb0-106">이 작업은 단일 명령으로 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="09bb0-106">This operation is completed in a single command.</span></span> <span data-ttu-id="09bb0-107">몇 초 내에 브라우저에 이 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="09bb0-107">Within just a few seconds, you will see this in your browser:</span></span>

![Azure Container Instances를 사용하여 배포된 앱이 브라우저에 표시됨][aci-app-browser]

<span data-ttu-id="09bb0-109">Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09bb0-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="09bb0-110">이 퀵 스타트의 2.0.12 hello Azure CLI 버전을 실행 되 고 있는지 필요 tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여 이후 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="09bb0-110">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.12 or later.</span></span> <span data-ttu-id="09bb0-111">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="09bb0-111">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="09bb0-112">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="09bb0-112">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="09bb0-113">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="09bb0-113">Create a resource group</span></span>

<span data-ttu-id="09bb0-114">Azure Container Instances는 Azure 리소스이며 Azure 리소스 그룹, Azure 리소스가 배포 및 관리되는 논리적 컬렉션에 배치되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09bb0-114">Azure Container Instances are Azure resources and must be placed in an Azure resource group, a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="09bb0-115">Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="09bb0-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="09bb0-116">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="09bb0-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a><span data-ttu-id="09bb0-117">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="09bb0-117">Create a container</span></span>

<span data-ttu-id="09bb0-118">이름, Docker 이미지 및 Azure 리소스 그룹을 제공하여 컨테이너를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09bb0-118">You can create a container by providing a name, a Docker image, and an Azure resource group.</span></span> <span data-ttu-id="09bb0-119">Hello 컨테이너 toohello를 선택적으로 노출할 공용 IP 주소를 사용 하 여 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="09bb0-119">You can optionally expose hello container toohello internet with a public IP address.</span></span> <span data-ttu-id="09bb0-120">이 경우 [Node.js](http://nodejs.org)에 작성된 매우 간단한 웹앱을 호스트하는 컨테이너를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="09bb0-120">In this case, we'll use a container that hosts a very simple web app written in [Node.js](http://nodejs.org).</span></span>

```azurecli-interactive
az container create --name mycontainer --image microsoft/aci-helloworld --resource-group myResourceGroup --ip-address public 
```

<span data-ttu-id="09bb0-121">몇 초 안에 응답 tooyour 요청을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09bb0-121">Within a few seconds, you should get a response tooyour request.</span></span> <span data-ttu-id="09bb0-122">처음에 hello 컨테이너 수는 **만들기** 상태로 설정 되지만 몇 초 이내에 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09bb0-122">Initially, hello container will be in a **Creating** state, but it should start within a few seconds.</span></span> <span data-ttu-id="09bb0-123">Hello를 사용 하 여 hello 상태를 확인할 수 있습니다 `show` 명령:</span><span class="sxs-lookup"><span data-stu-id="09bb0-123">You can check hello status using hello `show` command:</span></span>

```azurecli-interactive
az container show --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="09bb0-124">Hello 출력의 hello 아래쪽 hello 컨테이너의 프로 비전 상태 및 해당 IP 주소 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09bb0-124">At hello bottom of hello output, you will see hello container's provisioning state and its IP address:</span></span>

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

<span data-ttu-id="09bb0-125">Hello 컨테이너 toohello 이동 되 면 **Succeeded** 상태 이면 hello 제공 되는 IP 주소를 사용 하 여 hello 브라우저에 도달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09bb0-125">Once hello container moves toohello **Succeeded** state, you can reach it in hello browser using hello IP address provided.</span></span> 

![Azure Container Instances를 사용하여 배포된 앱이 브라우저에 표시됨][aci-app-browser]

## <a name="pull-hello-container-logs"></a><span data-ttu-id="09bb0-127">Hello 컨테이너 로그 가져오기</span><span class="sxs-lookup"><span data-stu-id="09bb0-127">Pull hello container logs</span></span>

<span data-ttu-id="09bb0-128">Hello를 사용 하 여 만든 hello 컨테이너에 대 한 hello 로그를 끌어올 수 `logs` 명령:</span><span class="sxs-lookup"><span data-stu-id="09bb0-128">You can pull hello logs for hello container you created using hello `logs` command:</span></span>

```azurecli-interactive
az container logs --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="09bb0-129">출력:</span><span class="sxs-lookup"><span data-stu-id="09bb0-129">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://104.210.39.122/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="delete-hello-container"></a><span data-ttu-id="09bb0-130">Hello 컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="09bb0-130">Delete hello container</span></span>

<span data-ttu-id="09bb0-131">Hello 컨테이너를 완료 하는 hello를 사용 하 여 제거할 수 있습니다 `delete` 명령:</span><span class="sxs-lookup"><span data-stu-id="09bb0-131">When you are done with hello container, you can remove it using hello `delete` command:</span></span>

```azurecli-interactive
az container delete --name mycontainer --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="09bb0-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="09bb0-132">Next steps</span></span>

<span data-ttu-id="09bb0-133">이 빠른 시작에 사용 되는 hello 컨테이너를 사용할 수 없으면 hello의 모든 코드 [github][app-github-repo], 해당 Dockerfile 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="09bb0-133">All of hello code for hello container used in this quick start is available [on GitHub][app-github-repo], along with its Dockerfile.</span></span> <span data-ttu-id="09bb0-134">Tootry 직접 작성 하 고 hello Azure 컨테이너 레지스트리를 사용 하 여 tooAzure 컨테이너 인스턴스를 배포 하기를 원하는 경우 toohello Azure 컨테이너 인스턴스 자습서를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="09bb0-134">If you'd like tootry building it yourself and deploying it tooAzure Container Instances using hello Azure Container Registry, continue toohello Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="09bb0-135">Azure Container Instances 자습서</span><span class="sxs-lookup"><span data-stu-id="09bb0-135">Azure Container Instances tutorials</span></span>](./container-instances-tutorial-prepare-app.md)


<!-- LINKS -->
[app-github-repo]: https://github.com/Azure-Samples/aci-helloworld.git

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png