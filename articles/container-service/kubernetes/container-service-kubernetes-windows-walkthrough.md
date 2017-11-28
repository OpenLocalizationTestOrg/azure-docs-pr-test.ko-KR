---
title: "Windows 용 Azure Kubernetes 클러스터 aaaQuickstart-| Microsoft Docs"
description: "신속 하 게 toocreate hello Azure CLI를 사용 하 여 Azure 컨테이너 서비스의 Windows 컨테이너에 대 한 Kubernetes 클러스터에 알아봅니다."
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 85fe65a46ae8c78797e8a8a097c2a37f06329335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-windows-containers"></a><span data-ttu-id="3b5d4-103">Windows 컨테이너용 Kubernetes 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="3b5d4-103">Deploy Kubernetes cluster for Windows containers</span></span>

<span data-ttu-id="3b5d4-104">hello Azure CLI 사용된 toocreate 이며 hello 명령줄에서 또는 스크립트에서 Azure 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="3b5d4-105">Azure CLI toodeploy hello를 사용 하 여이 가이드 정보는 [Kubernetes](https://kubernetes.io/docs/home/) 에 있는 클러스터 [Azure 컨테이너 서비스](../container-service-intro.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-105">This guide details using hello Azure CLI toodeploy a [Kubernetes](https://kubernetes.io/docs/home/) cluster in [Azure Container Service](../container-service-intro.md).</span></span> <span data-ttu-id="3b5d4-106">Hello Kubernetes로 tooit 연결한 hello 클러스터가 배포 되 면 `kubectl` 명령줄 도구를 첫 번째 Windows 컨테이너를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-106">Once hello cluster is deployed, you connect tooit with hello Kubernetes `kubectl` command-line tool, and you deploy your first Windows container.</span></span>

<span data-ttu-id="3b5d4-107">Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3b5d4-108">이 퀵 스타트의 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 필요 tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여 이후 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-108">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="3b5d4-109">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="3b5d4-110">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

> [!NOTE]
> <span data-ttu-id="3b5d4-111">Azure Container Service에서 Kubernetes의 Windows 컨테이너에 대한 지원은 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-111">Support for Windows containers on Kubernetes in Azure Container Service is in preview.</span></span> 
>

## <a name="create-a-resource-group"></a><span data-ttu-id="3b5d4-112">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="3b5d4-112">Create a resource group</span></span>

<span data-ttu-id="3b5d4-113">Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-113">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="3b5d4-114">Azure 리소스 그룹은 Azure 리소스가 배포되고 관리되는 논리 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="3b5d4-115">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-115">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="3b5d4-116">Kubernetes 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="3b5d4-116">Create Kubernetes cluster</span></span>
<span data-ttu-id="3b5d4-117">Azure 컨테이너 서비스의 hello Kubernetes 클러스터 만들기 [az acs 만들](/cli/azure/acs#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-117">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="3b5d4-118">hello 다음 예제에서는 명명 된 클러스터가 *myK8sCluster* 한 Linux로 노드와 두 개의 Windows 에이전트 노드를 마스터 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-118">hello following example creates a cluster named *myK8sCluster* with one Linux master node and two Windows agent nodes.</span></span> <span data-ttu-id="3b5d4-119">이 예에서는 SSH 필요한 tooconnect toohello Linux 마스터 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-119">This example creates SSH keys needed tooconnect toohello Linux master.</span></span> <span data-ttu-id="3b5d4-120">이 예에서는 *azureuser* 관리 사용자 이름에 대 한 및 *myPassword12* hello Windows 노드에서 hello 암호로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-120">This example uses *azureuser* for an administrative user name and *myPassword12* as hello password on hello Windows nodes.</span></span> <span data-ttu-id="3b5d4-121">이러한 값 toosomething 적절 한 tooyour 환경을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-121">Update these values toosomething appropriate tooyour environment.</span></span> 



```azurecli-interactive 
az acs create --orchestrator-type=kubernetes \
    --resource-group myResourceGroup \
    --name=myK8sCluster \
    --agent-count=2 \
    --generate-ssh-keys \
    --windows --admin-username azureuser \
    --admin-password myPassword12
```

<span data-ttu-id="3b5d4-122">몇 분 후 hello 명령, 완료 하 고 배포 하는 방법에 대 한 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-122">After several minutes, hello command completes, and shows you information about your deployment.</span></span>

## <a name="install-kubectl"></a><span data-ttu-id="3b5d4-123">kubectl 설치</span><span class="sxs-lookup"><span data-stu-id="3b5d4-123">Install kubectl</span></span>

<span data-ttu-id="3b5d4-124">사용 하 여 클라이언트 컴퓨터에서 tooconnect toohello Kubernetes 클러스터 [ `kubectl` ](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes 명령줄 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-124">tooconnect toohello Kubernetes cluster from your client computer, use [`kubectl`](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="3b5d4-125">Azure Cloud Shell을 사용하는 경우 `kubectl`이 이미 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-125">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="3b5d4-126">Tooinstall 하려는 경우 로컬로 있습니다 사용할 수 있습니다 hello [az acs kubernetes 설치 cli](/cli/azure/acs/kubernetes#install-cli) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-126">If you want tooinstall it locally, you can use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="3b5d4-127">다음 Azure CLI 예제 설치 hello `kubectl` tooyour 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-127">hello following Azure CLI example installs `kubectl` tooyour system.</span></span> <span data-ttu-id="3b5d4-128">Windows에서 이 명령을 관리자 권한으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-128">On Windows, run this command as an administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli
```


## <a name="connect-with-kubectl"></a><span data-ttu-id="3b5d4-129">Kubectl로 연결</span><span class="sxs-lookup"><span data-stu-id="3b5d4-129">Connect with kubectl</span></span>

<span data-ttu-id="3b5d4-130">tooconfigure `kubectl` hello 실행 tooconnect tooyour Kubernetes 클러스터 [az acs kubernetes get-자격 증명](/cli/azure/acs/kubernetes#get-credentials) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-130">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="3b5d4-131">hello 다음 예제에서는 다운로드 Kubernetes 클러스터에 대 한 hello 클러스터 구성.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-131">hello following example downloads hello cluster configuration for your Kubernetes cluster.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="3b5d4-132">tooverify hello 연결 tooyour에서에서 클러스터 컴퓨터를 실행 해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-132">tooverify hello connection tooyour cluster from your machine, try running:</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="3b5d4-133">`kubectl`hello 마스터 및 에이전트 노드를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-133">`kubectl` lists hello master and agent nodes.</span></span>

```azurecli-interactive
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.5.3
k8s-agent-98dc3136-1    Ready                      5m        v1.5.3
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.5.3

```

## <a name="deploy-a-windows-iis-container"></a><span data-ttu-id="3b5d4-134">Windows IIS 컨테이너 배포</span><span class="sxs-lookup"><span data-stu-id="3b5d4-134">Deploy a Windows IIS container</span></span>

<span data-ttu-id="3b5d4-135">하나 이상의 컨테이너가 포함된 Kubernetes *Pod* 내부에서 Docker 컨테이너를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-135">You can run a Docker container inside a Kubernetes *pod*, which contains one or more containers.</span></span> 

<span data-ttu-id="3b5d4-136">기본 예제에서는 JSON 파일 toospecify Microsoft 인터넷 정보 서버 (IIS) 컨테이너를 사용 하 여 만들고 다음 hello를 사용 하 여 hello pod `kubctl apply` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-136">This basic example uses a JSON file toospecify a Microsoft Internet Information Server (IIS) container, and then creates hello pod using hello `kubctl apply` command.</span></span> 

<span data-ttu-id="3b5d4-137">라는 로컬 파일을 만들어 `iis.json` 복사 hello 텍스트에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-137">Create a local file named `iis.json` and copy hello following text.</span></span> <span data-ttu-id="3b5d4-138">이 파일을 통해 알 Kubernetes toorun IIS에서 Windows Server 2016 Nano 서버에서 공용 컨테이너 이미지를 사용 하 여 [Docker 허브](https://hub.docker.com/r/nanoserver/iis/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-138">This file tells Kubernetes toorun IIS on Windows Server 2016 Nano Server, using a public container image from [Docker Hub](https://hub.docker.com/r/nanoserver/iis/).</span></span> <span data-ttu-id="3b5d4-139">hello 컨테이너 포트 80을 사용 하 여 이지만 처음에 불과합니다 hello 클러스터 네트워크 내에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-139">hello container uses port 80, but initially is only accessible within hello cluster network.</span></span>

 ```JSON
 {
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "iis",
    "labels": {
      "name": "iis"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "iis",
        "image": "nanoserver/iis",
        "ports": [
          {
          "containerPort": 80
          }
        ]
      }
    ],
    "nodeSelector": {
     "beta.kubernetes.io/os": "windows"
     }
   }
 }
 ```

<span data-ttu-id="3b5d4-140">toostart hello pod, 유형:</span><span class="sxs-lookup"><span data-stu-id="3b5d4-140">toostart hello pod, type:</span></span>
  
```azurecli-interactive
kubectl apply -f iis.json
```  

<span data-ttu-id="3b5d4-141">형식 tootrack hello 배포:</span><span class="sxs-lookup"><span data-stu-id="3b5d4-141">tootrack hello deployment, type:</span></span>
  
```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="3b5d4-142">Hello 상태는 hello 포드를 배포 하는 동안 `ContainerCreating`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-142">While hello pod is deploying, hello status is `ContainerCreating`.</span></span> <span data-ttu-id="3b5d4-143">Hello 컨테이너 tooenter hello에 대 일 분이 지나야 `Running` 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-143">It can take a few minutes for hello container tooenter hello `Running` state.</span></span>

```azurecli-interactive
NAME     READY        STATUS        RESTARTS    AGE
iis      1/1          Running       0           32s
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="3b5d4-144">보기 hello IIS 시작 페이지</span><span class="sxs-lookup"><span data-stu-id="3b5d4-144">View hello IIS welcome page</span></span>

<span data-ttu-id="3b5d4-145">tooexpose hello pod toohello world 공용 IP 주소, 다음 명령을 형식 hello:</span><span class="sxs-lookup"><span data-stu-id="3b5d4-145">tooexpose hello pod toohello world with a public IP address, type hello following command:</span></span>

```azurecli-interactive
kubectl expose pods iis --port=80 --type=LoadBalancer
```

<span data-ttu-id="3b5d4-146">Kubernetes이이 명령을 사용 하 여 서비스를 만듭니다와 [Azure 부하 분산 장치 규칙](container-service-kubernetes-load-balancing.md) hello 서비스에 대 한 공용 IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-146">With this command, Kubernetes creates a service and an [Azure load balancer rule](container-service-kubernetes-load-balancing.md) with a public IP address for hello service.</span></span> 

<span data-ttu-id="3b5d4-147">Hello hello 서비스의 명령 toosee hello 상태를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-147">Run hello following command toosee hello status of hello service.</span></span>

```azurecli-interactive
kubectl get svc
```

<span data-ttu-id="3b5d4-148">으로 hello IP 주소가 표시 되는 처음 `pending`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-148">Initially hello IP address appears as `pending`.</span></span> <span data-ttu-id="3b5d4-149">몇 분 후 hello의 외부 IP 주소를 hello `iis` pod 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-149">After a few minutes, hello external IP address of hello `iis` pod is set:</span></span>
  
```azurecli-interactive
NAME         CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE       
kubernetes   10.0.0.1       <none>          443/TCP        21h       
iis          10.0.111.25    13.64.158.233   80/TCP         22m
```

<span data-ttu-id="3b5d4-150">Hello 외부 IP 주소에서 choice toosee hello 기본 IIS 시작 페이지의 웹 브라우저를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-150">You can use a web browser of your choice toosee hello default IIS welcome page at hello external IP address:</span></span>

![TooIIS 검색 이미지](./media/container-service-kubernetes-windows-walkthrough/kubernetes-iis.png)  


## <a name="delete-cluster"></a><span data-ttu-id="3b5d4-152">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="3b5d4-152">Delete cluster</span></span>
<span data-ttu-id="3b5d4-153">Hello hello 클러스터 필요는 더 이상 사용할 수 없습니다 [az 그룹 삭제](/cli/azure/group#delete) tooremove hello 리소스 그룹, 컨테이너 서비스와 관련 된 모든 리소스를 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-153">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a><span data-ttu-id="3b5d4-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3b5d4-154">Next steps</span></span>

<span data-ttu-id="3b5d4-155">이 빠른 시작에서는 Kubernetes 클러스터를 배포하고, `kubectl`로 연결하고, IIS 컨테이너가 있는 Pod를 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-155">In this quick start, you deployed a Kubernetes cluster, connected with `kubectl`, and deployed a pod with an IIS container.</span></span> <span data-ttu-id="3b5d4-156">Azure 컨테이너 서비스에 대해 자세히 toolearn toohello Kubernetes 자습서를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b5d4-156">toolearn more about Azure Container Service, continue toohello Kubernetes tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3b5d4-157">ACS Kubernetes 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="3b5d4-157">Manage an ACS Kubernetes cluster</span></span>](container-service-tutorial-kubernetes-prepare-app.md)
