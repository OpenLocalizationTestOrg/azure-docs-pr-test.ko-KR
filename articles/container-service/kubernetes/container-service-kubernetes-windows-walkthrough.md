---
title: "빠른 시작 - Windows용 Azure Kubernetes 클러스터 | Microsoft Docs"
description: "Azure Container Service에서 Azure CLI를 사용하여 Windows 컨테이너용 Kubernetes 클러스터를 빠르게 만드는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: f9bf4c4094addfa9654e3b99d91add03079ee045
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-kubernetes-cluster-for-windows-containers"></a><span data-ttu-id="22a06-103">Windows 컨테이너용 Kubernetes 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="22a06-103">Deploy Kubernetes cluster for Windows containers</span></span>

<span data-ttu-id="22a06-104">명령줄 또는 스크립트에서 Azure 리소스를 만들고 관리하는 데 Azure CLI가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="22a06-105">이 가이드에서는 Azure CLI를 사용하여 [Azure Container Service](../container-service-intro.md)에서 [Kubernetes](https://kubernetes.io/docs/home/) 클러스터를 배포하는 방법에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-105">This guide details using the Azure CLI to deploy a [Kubernetes](https://kubernetes.io/docs/home/) cluster in [Azure Container Service](../container-service-intro.md).</span></span> <span data-ttu-id="22a06-106">클러스터가 배포되면 Kubernetes `kubectl` 명령줄 도구를 사용하여 해당 클러스터에 연결하고 첫 번째 Windows 컨테이너를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-106">Once the cluster is deployed, you connect to it with the Kubernetes `kubectl` command-line tool, and you deploy your first Windows container.</span></span>

<span data-ttu-id="22a06-107">Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="22a06-108">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 빠른 시작에서 Azure CLI 버전 2.0.4 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-108">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="22a06-109">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="22a06-110">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22a06-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

> [!NOTE]
> <span data-ttu-id="22a06-111">Azure Container Service에서 Kubernetes의 Windows 컨테이너에 대한 지원은 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-111">Support for Windows containers on Kubernetes in Azure Container Service is in preview.</span></span> 
>

## <a name="create-a-resource-group"></a><span data-ttu-id="22a06-112">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="22a06-112">Create a resource group</span></span>

<span data-ttu-id="22a06-113">[az group create](/cli/azure/group#create) 명령을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-113">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="22a06-114">Azure 리소스 그룹은 Azure 리소스가 배포되고 관리되는 논리 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="22a06-115">다음 예제에서는 *eastus* 위치에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-115">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="22a06-116">Kubernetes 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="22a06-116">Create Kubernetes cluster</span></span>
<span data-ttu-id="22a06-117">[az acs create](/cli/azure/acs#create) 명령을 사용하여 Azure Container Service에서 Kubernetes 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-117">Create a Kubernetes cluster in Azure Container Service with the [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="22a06-118">다음 예제에서는 하나의 Linux 마스터 노드와 두 개의 Windows 에이전트 노드가 있는 *myK8sCluster* 클러스터를 만들고,</span><span class="sxs-lookup"><span data-stu-id="22a06-118">The following example creates a cluster named *myK8sCluster* with one Linux master node and two Windows agent nodes.</span></span> <span data-ttu-id="22a06-119">Linux 마스터에 연결하는 데 필요한 SSH 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-119">This example creates SSH keys needed to connect to the Linux master.</span></span> <span data-ttu-id="22a06-120">이 예제에서는 Windows 노드에 대해 관리 사용자 이름으로 *azureuser*, 암호로 *myPassword12*를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-120">This example uses *azureuser* for an administrative user name and *myPassword12* as the password on the Windows nodes.</span></span> <span data-ttu-id="22a06-121">이러한 값을 사용자 환경에 적절한 값으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-121">Update these values to something appropriate to your environment.</span></span> 



```azurecli-interactive 
az acs create --orchestrator-type=kubernetes \
    --resource-group myResourceGroup \
    --name=myK8sCluster \
    --agent-count=2 \
    --generate-ssh-keys \
    --windows --admin-username azureuser \
    --admin-password myPassword12
```

<span data-ttu-id="22a06-122">몇 분 후 명령이 완료되면 배포에 대한 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-122">After several minutes, the command completes, and shows you information about your deployment.</span></span>

## <a name="install-kubectl"></a><span data-ttu-id="22a06-123">kubectl 설치</span><span class="sxs-lookup"><span data-stu-id="22a06-123">Install kubectl</span></span>

<span data-ttu-id="22a06-124">클라이언트 컴퓨터에서 Kubernetes 클러스터에 연결하려면 Kubernetes 명령줄 클라이언트인 [`kubectl`](https://kubernetes.io/docs/user-guide/kubectl/)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-124">To connect to the Kubernetes cluster from your client computer, use [`kubectl`](https://kubernetes.io/docs/user-guide/kubectl/), the Kubernetes command-line client.</span></span> 

<span data-ttu-id="22a06-125">Azure Cloud Shell을 사용하는 경우 `kubectl`이 이미 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-125">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="22a06-126">로컬로 설치하려면 [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) 명령을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-126">If you want to install it locally, you can use the [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="22a06-127">다음 Azure CLI 예제에서는 `kubectl`을 시스템에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-127">The following Azure CLI example installs `kubectl` to your system.</span></span> <span data-ttu-id="22a06-128">Windows에서 이 명령을 관리자 권한으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-128">On Windows, run this command as an administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli
```


## <a name="connect-with-kubectl"></a><span data-ttu-id="22a06-129">Kubectl로 연결</span><span class="sxs-lookup"><span data-stu-id="22a06-129">Connect with kubectl</span></span>

<span data-ttu-id="22a06-130">Kubernetes 클러스터에 연결하도록 `kubectl`을 구성하려면 [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-130">To configure `kubectl` to connect to your Kubernetes cluster, run the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="22a06-131">다음 예제에서는 Kubernetes 클러스터에 대한 클러스터 구성을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-131">The following example downloads the cluster configuration for your Kubernetes cluster.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="22a06-132">시스템에서 클러스터에 대한 연결을 확인하려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-132">To verify the connection to your cluster from your machine, try running:</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="22a06-133">`kubectl`에서 마스터 및 에이전트 노드를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-133">`kubectl` lists the master and agent nodes.</span></span>

```azurecli-interactive
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.5.3
k8s-agent-98dc3136-1    Ready                      5m        v1.5.3
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.5.3

```

## <a name="deploy-a-windows-iis-container"></a><span data-ttu-id="22a06-134">Windows IIS 컨테이너 배포</span><span class="sxs-lookup"><span data-stu-id="22a06-134">Deploy a Windows IIS container</span></span>

<span data-ttu-id="22a06-135">하나 이상의 컨테이너가 포함된 Kubernetes *Pod* 내부에서 Docker 컨테이너를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-135">You can run a Docker container inside a Kubernetes *pod*, which contains one or more containers.</span></span> 

<span data-ttu-id="22a06-136">이 기본 예제에서는 JSON 파일을 사용하여 Microsoft IIS(Internet Information Server) 컨테이너를 지정한 다음 `kubctl apply` 명령을 사용하여 Pod를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-136">This basic example uses a JSON file to specify a Microsoft Internet Information Server (IIS) container, and then creates the pod using the `kubctl apply` command.</span></span> 

<span data-ttu-id="22a06-137">`iis.json`이라는 로컬 파일을 만들고 다음 텍스트를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-137">Create a local file named `iis.json` and copy the following text.</span></span> <span data-ttu-id="22a06-138">이 파일은 Kubernetes에게 [Docker 허브](https://hub.docker.com/r/nanoserver/iis/)의 공용 컨테이너 이미지를 사용하여 Windows Server 2016 Nano Server에서 IIS를 실행하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-138">This file tells Kubernetes to run IIS on Windows Server 2016 Nano Server, using a public container image from [Docker Hub](https://hub.docker.com/r/nanoserver/iis/).</span></span> <span data-ttu-id="22a06-139">컨테이너는 포트 80을 사용하지만, 처음에 클러스터 네트워크 내에서만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-139">The container uses port 80, but initially is only accessible within the cluster network.</span></span>

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

<span data-ttu-id="22a06-140">Pod를 시작하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-140">To start the pod, type:</span></span>
  
```azurecli-interactive
kubectl apply -f iis.json
```  

<span data-ttu-id="22a06-141">배포를 추적하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-141">To track the deployment, type:</span></span>
  
```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="22a06-142">Pod를 배포하는 동안 상태는 `ContainerCreating`입니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-142">While the pod is deploying, the status is `ContainerCreating`.</span></span> <span data-ttu-id="22a06-143">컨테이너가 `Running` 상태가 되는 데 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-143">It can take a few minutes for the container to enter the `Running` state.</span></span>

```azurecli-interactive
NAME     READY        STATUS        RESTARTS    AGE
iis      1/1          Running       0           32s
```

## <a name="view-the-iis-welcome-page"></a><span data-ttu-id="22a06-144">IIS 시작 페이지 보기</span><span class="sxs-lookup"><span data-stu-id="22a06-144">View the IIS welcome page</span></span>

<span data-ttu-id="22a06-145">공용 IP 주소로 Pod를 전 세계에 공개하려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-145">To expose the pod to the world with a public IP address, type the following command:</span></span>

```azurecli-interactive
kubectl expose pods iis --port=80 --type=LoadBalancer
```

<span data-ttu-id="22a06-146">이 명령을 사용하면 Kubernetes에서 해당 공용 IP 주소를 사용하여 서비스 및 [Azure 부하 분산 장치 규칙](container-service-kubernetes-load-balancing.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-146">With this command, Kubernetes creates a service and an [Azure load balancer rule](container-service-kubernetes-load-balancing.md) with a public IP address for the service.</span></span> 

<span data-ttu-id="22a06-147">다음 명령을 실행하여 서비스의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-147">Run the following command to see the status of the service.</span></span>

```azurecli-interactive
kubectl get svc
```

<span data-ttu-id="22a06-148">처음에는 IP 주소가 `pending`으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-148">Initially the IP address appears as `pending`.</span></span> <span data-ttu-id="22a06-149">몇 분 후에 다음과 같이 `iis` Pod의 외부 IP 주소가 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-149">After a few minutes, the external IP address of the `iis` pod is set:</span></span>
  
```azurecli-interactive
NAME         CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE       
kubernetes   10.0.0.1       <none>          443/TCP        21h       
iis          10.0.111.25    13.64.158.233   80/TCP         22m
```

<span data-ttu-id="22a06-150">선택한 웹 브라우저를 사용하여 외부 IP 주소의 기본 IIS 시작 페이지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-150">You can use a web browser of your choice to see the default IIS welcome page at the external IP address:</span></span>

![IIS로 이동하는 이미지](./media/container-service-kubernetes-windows-walkthrough/kubernetes-iis.png)  


## <a name="delete-cluster"></a><span data-ttu-id="22a06-152">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="22a06-152">Delete cluster</span></span>
<span data-ttu-id="22a06-153">클러스터가 더 이상 필요하지 않으면 [az group delete](/cli/azure/group#delete) 명령을 사용하여 리소스 그룹, 컨테이너 서비스 및 모든 관련 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-153">When the cluster is no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a><span data-ttu-id="22a06-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="22a06-154">Next steps</span></span>

<span data-ttu-id="22a06-155">이 빠른 시작에서는 Kubernetes 클러스터를 배포하고, `kubectl`로 연결하고, IIS 컨테이너가 있는 Pod를 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="22a06-155">In this quick start, you deployed a Kubernetes cluster, connected with `kubectl`, and deployed a pod with an IIS container.</span></span> <span data-ttu-id="22a06-156">Azure Container Service에 대해 자세히 알아보려면 Kubernetes 자습서로 계속 진행하세요.</span><span class="sxs-lookup"><span data-stu-id="22a06-156">To learn more about Azure Container Service, continue to the Kubernetes tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="22a06-157">ACS Kubernetes 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="22a06-157">Manage an ACS Kubernetes cluster</span></span>](container-service-tutorial-kubernetes-prepare-app.md)
