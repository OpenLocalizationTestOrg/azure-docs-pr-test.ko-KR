---
title: "Linux 용 Azure Kubernetes 클러스터 aaaQuickstart-| Microsoft Docs"
description: "신속 하 게 toocreate hello Azure CLI를 사용 하 여 Azure 컨테이너 서비스의 Linux 컨테이너에 대 한 Kubernetes 클러스터에 알아봅니다."
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 8b0d7a803148c1cbf329f4b76f2e99b4b7e14983
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-linux-containers"></a><span data-ttu-id="9ba89-103">Linux 컨테이너용 Kubernetes 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="9ba89-103">Deploy Kubernetes cluster for Linux containers</span></span>

<span data-ttu-id="9ba89-104">이 빠른 시작에서는 Kubernetes 클러스터 hello Azure CLI를 사용 하 여 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-104">In this quick start, a Kubernetes cluster is deployed using hello Azure CLI.</span></span> <span data-ttu-id="9ba89-105">그런 다음 웹 프런트 엔드 및 Redis 인스턴스로 구성 된 다중 컨테이너 응용 프로그램 배포 하 고 hello 클러스터에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on hello cluster.</span></span> <span data-ttu-id="9ba89-106">Hello 응용 프로그램을 통해 액세스할 수는 완료 되 면 인터넷 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-106">Once completed, hello application is accessible over hello internet.</span></span> 

<span data-ttu-id="9ba89-107">이 문서에 사용 된 예제 응용 프로그램 hello Python로 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-107">hello example application used in this document is written in Python.</span></span> <span data-ttu-id="9ba89-108">hello 개념 및 여기에서 자세히 설명 하는 단계에 사용 되는 toodeploy Kubernetes 클러스터로 컨테이너 이미지 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-108">hello concepts and steps detailed here can be used toodeploy any container image into a Kubernetes cluster.</span></span> <span data-ttu-id="9ba89-109">hello 코드, Dockerfile 및 미리 만들어진된 Kubernetes 매니페스트 파일 관련된 toothis 프로젝트에서 사용할 수 있는 [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git)합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-109">hello code, Dockerfile, and pre-created Kubernetes manifest files related toothis project are available on [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).</span></span>

![투표 tooAzure 검색 이미지](media/container-service-kubernetes-walkthrough/azure-vote.png)

<span data-ttu-id="9ba89-111">이 빠른 시작에 Kubernetes 개념에 대 한 기본 지식이 있다고 가정, 참조 hello에 대 한 자세한 내용은 Kubernetes [Kubernetes 설명서]( https://kubernetes.io/docs/home/)합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-111">This quick start assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see hello [Kubernetes documentation]( https://kubernetes.io/docs/home/).</span></span>

<span data-ttu-id="9ba89-112">Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9ba89-113">이 퀵 스타트의 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 필요 tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여 이후 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-113">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="9ba89-114">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="9ba89-115">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="9ba89-116">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="9ba89-116">Create a resource group</span></span>

<span data-ttu-id="9ba89-117">Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-117">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="9ba89-118">Azure 리소스 그룹은 Azure 리소스가 배포되고 관리되는 논리 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-118">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="9ba89-119">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *westeurope* 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-119">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="9ba89-120">출력:</span><span class="sxs-lookup"><span data-stu-id="9ba89-120">Output:</span></span>

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westeurope",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="9ba89-121">Kubernetes 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="9ba89-121">Create Kubernetes cluster</span></span>

<span data-ttu-id="9ba89-122">Azure 컨테이너 서비스의 hello Kubernetes 클러스터 만들기 [az acs 만들](/cli/azure/acs#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-122">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> <span data-ttu-id="9ba89-123">hello 다음 예제에서는 명명 된 클러스터가 *myK8sCluster* 와 하나의 Linux 마스터 노드 및 Linux 에이전트 노드를 세 개 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-123">hello following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type kubernetes --resource-group myResourceGroup --name myK8sCluster --generate-ssh-keys 
```

<span data-ttu-id="9ba89-124">몇 분 후 hello 명령을 완료 하 고 hello 클러스터에 대 한 json 형식 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-124">After several minutes, hello command completes and returns json formatted information about hello cluster.</span></span> 

## <a name="connect-toohello-cluster"></a><span data-ttu-id="9ba89-125">Toohello 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="9ba89-125">Connect toohello cluster</span></span>

<span data-ttu-id="9ba89-126">toomanage Kubernetes 클러스터를 사용 하 여 [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes 명령줄 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-126">toomanage a Kubernetes cluster, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="9ba89-127">Azure Cloud Shell을 사용하는 경우 kubectl이 이미 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-127">If you're using Azure CloudShell, kubectl is already installed.</span></span> <span data-ttu-id="9ba89-128">Tooinstall 하려는 경우 로컬로 있습니다 사용할 수 있습니다 hello [az acs kubernetes 설치 cli](/cli/azure/acs/kubernetes#install-cli) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-128">If you want tooinstall it locally, you can use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="9ba89-129">tooconfigure kubectl tooconnect tooyour Kubernetes 클러스터 hello 실행 [az acs kubernetes get-자격 증명](/cli/azure/acs/kubernetes#get-credentials) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-129">tooconfigure kubectl tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="9ba89-130">이 단계는 자격 증명을 다운로드 하 고 hello Kubernetes CLI toouse 구성으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-130">This step downloads credentials and configures hello Kubernetes CLI toouse them.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="9ba89-131">tooverify hello 연결 tooyour 클러스터를 사용 하 여 hello [kubectl 가져오기](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) 명령 tooreturn hello 클러스터 노드의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-131">tooverify hello connection tooyour cluster, use hello [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command tooreturn a list of hello cluster nodes.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="9ba89-132">출력:</span><span class="sxs-lookup"><span data-stu-id="9ba89-132">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-14ad53a1-0    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-1    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-2    Ready                      10m       v1.6.6
k8s-master-14ad53a1-0   Ready,SchedulingDisabled   10m       v1.6.6
```

## <a name="run-hello-application"></a><span data-ttu-id="9ba89-133">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="9ba89-133">Run hello application</span></span>

<span data-ttu-id="9ba89-134">Kubernetes 매니페스트 파일 내용을 컨테이너 이미지를 실행 해야 하는 포함 하 여 hello 클러스터에 대 한 원하는 상태를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-134">A Kubernetes manifest file defines a desired state for hello cluster, including what container images should be running.</span></span> <span data-ttu-id="9ba89-135">예를 들어 매니페스트는 사용 되는 toocreate 모든 필요한 toorun hello Azure 투표 응용 프로그램 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-135">For this example, a manifest is used toocreate all objects needed toorun hello Azure Vote application.</span></span> 

<span data-ttu-id="9ba89-136">라는 파일을 만들어 `azure-vote.yml` 및 복사에 YAML 다음 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-136">Create a file named `azure-vote.yml` and copy into it hello following YAML.</span></span> <span data-ttu-id="9ba89-137">Azure Cloud Shell에서 작업하고 있는 경우 이 파일은 가상 또는 실제 시스템에서 작업하고 있는 것처럼 vi 또는 Nano를 사용하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-137">If you are working in Azure Cloud Shell, this file can be created using vi or Nano as if working on a virtual or physical system.</span></span>

```yaml
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-back
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-back
    spec:
      containers:
      - name: azure-vote-back
        image: redis
        ports:
        - containerPort: 6379
          name: redis
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-back
spec:
  ports:
  - port: 6379
  selector:
    app: azure-vote-back
---
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-front
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-front
    spec:
      containers:
      - name: azure-vote-front
        image: microsoft/azure-vote-front:redis-v1
        ports:
        - containerPort: 80
        env:
        - name: REDIS
          value: "azure-vote-back"
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-front
spec:
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    app: azure-vote-front
```

<span data-ttu-id="9ba89-138">사용 하 여 hello [kubectl 만들](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) toorun hello 응용 프로그램 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-138">Use hello [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) command toorun hello application.</span></span>

```azurecli-interactive
kubectl create -f azure-vote.yml
```

<span data-ttu-id="9ba89-139">출력:</span><span class="sxs-lookup"><span data-stu-id="9ba89-139">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-hello-application"></a><span data-ttu-id="9ba89-140">Hello 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="9ba89-140">Test hello application</span></span>

<span data-ttu-id="9ba89-141">Hello 응용 프로그램을 실행 한 [Kubernetes 서비스](https://kubernetes.io/docs/concepts/services-networking/service/) 노출 응용 프로그램 프런트 엔드 toohello hello는 만들어집니다 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-141">As hello application is run, a [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created that exposes hello application front end toohello internet.</span></span> <span data-ttu-id="9ba89-142">이 프로세스는 몇 분 toocomplete를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-142">This process can take a few minutes toocomplete.</span></span> 

<span data-ttu-id="9ba89-143">toomonitor 진행 상황을 사용 하 여 hello [kubectl 서비스를 가져올](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) hello로 명령을 `--watch` 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-143">toomonitor progress, use hello [kubectl get service](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command with hello `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="9ba89-144">처음 hello **외부 IP** hello에 대 한 *azure 투표 프런트* 으로 서비스 나타납니다 *보류 중인*합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-144">Initially hello **EXTERNAL-IP** for hello *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="9ba89-145">hello 외부 IP 주소가 변경 되 면 *보류 중인* tooan *IP 주소*를 사용 하 여 `CTRL-C` toostop hello kubectl 조사식 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-145">Once hello EXTERNAL-IP address has changed from *pending* tooan *IP address*, use `CTRL-C` toostop hello kubectl watch process.</span></span> 
  
```bash
azure-vote-front   10.0.34.242   <pending>     80:30676/TCP   7s
azure-vote-front   10.0.34.242   52.179.23.131   80:30676/TCP   2m
```

<span data-ttu-id="9ba89-146">이제 toohello 외부 IP 주소 toosee hello Azure 투표 앱을 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-146">You can now browse toohello external IP address toosee hello Azure Vote App.</span></span>

![투표 tooAzure 검색 이미지](media/container-service-kubernetes-walkthrough/azure-vote.png)  

## <a name="delete-cluster"></a><span data-ttu-id="9ba89-148">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="9ba89-148">Delete cluster</span></span>
<span data-ttu-id="9ba89-149">Hello hello 클러스터 필요는 더 이상 사용할 수 없습니다 [az 그룹 삭제](/cli/azure/group#delete) tooremove hello 리소스 그룹, 컨테이너 서비스와 관련 된 모든 리소스를 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-149">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a><span data-ttu-id="9ba89-150">Hello 코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="9ba89-150">Get hello code</span></span>

<span data-ttu-id="9ba89-151">이 빠른 시작에서 미리 생성된 된 컨테이너 이미지에 사용 되는 toocreate Kubernetes 배포 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-151">In this quick start, pre-created container images have been used toocreate a Kubernetes deployment.</span></span> <span data-ttu-id="9ba89-152">hello 관련 응용 프로그램 코드에서 Dockerfile을 되며 Kubernetes 매니페스트 파일 GitHub에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-152">hello related application code, Dockerfile, and Kubernetes manifest file are available on GitHub.</span></span>

[<span data-ttu-id="9ba89-153">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="9ba89-153">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="9ba89-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9ba89-154">Next steps</span></span>

<span data-ttu-id="9ba89-155">이 빠른 시작 Kubernetes 클러스터를 배포 하 고 여러 컨테이너 응용 프로그램 tooit 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-155">In this quick start, you deployed a Kubernetes cluster and deployed a multi-container application tooit.</span></span> 

<span data-ttu-id="9ba89-156">Azure 컨테이너 서비스 및 전체 코드 toodeployment 예제를 통해 워크에 대해 자세히 toolearn toohello Kubernetes 클러스터 자습서를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba89-156">toolearn more about Azure Container Service, and walk through a complete code toodeployment example, continue toohello Kubernetes cluster tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9ba89-157">ACS Kubernetes 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="9ba89-157">Manage an ACS Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-prepare-app.md)
