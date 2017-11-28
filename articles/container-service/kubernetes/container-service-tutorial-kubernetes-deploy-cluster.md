---
title: "Azure Container Service 자습서 - 클러스터 배포 | Microsoft Docs"
description: "Azure Container Service 자습서 - 클러스터 배포"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 472697c1f0c18859087d7b448e1786d85c27aca0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="17853-104">Azure Container Service에서 Kubernetes 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="17853-104">Deploy a Kubernetes cluster in Azure Container Service</span></span>

<span data-ttu-id="17853-105">Kubernetes는 컨테이너화된 응용 프로그램용 분산 플랫폼을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="17853-105">Kubernetes provides a distributed platform for containerized applications.</span></span> <span data-ttu-id="17853-106">Azure Container Service를 통해 프로덕션이 준비된 Kubernetes 클러스터를 프로비전하는 작업은 간단하고 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="17853-106">With Azure Container Service, provisioning of a production ready Kubernetes cluster is simple and quick.</span></span> <span data-ttu-id="17853-107">이 자습서(전체 7부 중 3부)에서는 Azure Container Service Kubernetes 클러스터를 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="17853-107">In this tutorial, part 3 of 7, an Azure Container Service Kubernetes cluster is deployed.</span></span> <span data-ttu-id="17853-108">완료되는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="17853-108">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="17853-109">Kubernetes ACS 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="17853-109">Deploying a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="17853-110">Kubernetes CLI(kubectl) 설치</span><span class="sxs-lookup"><span data-stu-id="17853-110">Installation of the Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="17853-111">kubectl 구성</span><span class="sxs-lookup"><span data-stu-id="17853-111">Configuration of kubectl</span></span>

<span data-ttu-id="17853-112">후속 자습서에서는 Azure 투표 응용 프로그램을 클러스터에 배포하고 확장/업데이트하며, Kubernetes 클러스터를 모니터링하도록 Operations Management Suite를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="17853-112">In subsequent tutorials, the Azure Vote application is deployed to the cluster, scaled, updated, and Operations Management Suite is configured to monitor the Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="17853-113">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="17853-113">Before you begin</span></span>

<span data-ttu-id="17853-114">이전 자습서에서는 컨테이너 이미지를 만들어 Azure Container Registry 인스턴스에 업로드했습니다.</span><span class="sxs-lookup"><span data-stu-id="17853-114">In previous tutorials, a container image was created and uploaded to an Azure Container Registry instance.</span></span> <span data-ttu-id="17853-115">이러한 단계를 수행하지 않은 경우 수행하려면 [자습서 1 - 컨테이너 이미지 만들기](./container-service-tutorial-kubernetes-prepare-app.md)로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="17853-115">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span>

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="17853-116">Kubernetes 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="17853-116">Create Kubernetes cluster</span></span>

<span data-ttu-id="17853-117">[이전 자습서](./container-service-tutorial-kubernetes-prepare-acr.md)에서 *myResourceGroup*이라는 리소스 그룹을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="17853-117">In the [previous tutorial](./container-service-tutorial-kubernetes-prepare-acr.md), a resource group named *myResourceGroup* was created.</span></span> <span data-ttu-id="17853-118">만들지 않은 경우 지금 이 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17853-118">If you have not done so, create this resource group now.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="17853-119">[az acs create](/cli/azure/acs#create) 명령을 사용하여 Azure Container Service에서 Kubernetes 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17853-119">Create a Kubernetes cluster in Azure Container Service with the [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="17853-120">다음 예제에서는 하나의 Linux 마스터 노드와 세 개의 Linux 에이전트 노드가 있는 *myK8sCluster*라는 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17853-120">The following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type=kubernetes --resource-group myResourceGroup --name=myK8SCluster --generate-ssh-keys 
```

<span data-ttu-id="17853-121">몇 분 후 명령이 완료되고 ACS 배포에 대해 json으로 형식화된 정보가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="17853-121">After several minutes, the command completes, and returns json formatted information about the ACS deployment.</span></span>

## <a name="install-the-kubectl-cli"></a><span data-ttu-id="17853-122">kubectl CLI 설치</span><span class="sxs-lookup"><span data-stu-id="17853-122">Install the kubectl CLI</span></span>

<span data-ttu-id="17853-123">클라이언트 컴퓨터에서 Kubernetes 클러스터에 연결하려면 Kubernetes 명령줄 클라이언트인 [kubectl](https://kubernetes.io/docs/user-guide/kubectl/)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="17853-123">To connect to the Kubernetes cluster from your client computer, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), the Kubernetes command-line client.</span></span> 

<span data-ttu-id="17853-124">Azure Cloud Shell을 사용하는 경우 `kubectl`이 이미 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17853-124">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="17853-125">로컬로 설치하려면 [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="17853-125">If you want to install it locally, use the [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="17853-126">Linux 또는 macOS에서 실행하는 경우 sudo를 사용하여 실행해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17853-126">If running in Linux or macOS, you may need to run with sudo.</span></span> <span data-ttu-id="17853-127">Windows에서는 셸이 관리자 권한으로 실행되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="17853-127">On Windows, ensure your shell has been run as administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli 
```

<span data-ttu-id="17853-128">Windows에서 기본 설치는 *c:\program files (x86)\kubectl.exe*입니다.</span><span class="sxs-lookup"><span data-stu-id="17853-128">On Windows, the default installation is *c:\program files (x86)\kubectl.exe*.</span></span> <span data-ttu-id="17853-129">Windows 경로에 이 파일을 추가해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17853-129">You may need to add this file to the Windows path.</span></span> 

## <a name="connect-with-kubectl"></a><span data-ttu-id="17853-130">Kubectl로 연결</span><span class="sxs-lookup"><span data-stu-id="17853-130">Connect with kubectl</span></span>

<span data-ttu-id="17853-131">Kubernetes 클러스터에 연결하도록 `kubectl`을 구성하려면 [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="17853-131">To configure `kubectl` to connect to your Kubernetes cluster, run the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8SCluster
```

<span data-ttu-id="17853-132">클러스터에 대한 연결을 확인하려면 [kubectl get nodes](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="17853-132">To verify the connection to your cluster, run the [kubectl get nodes](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="17853-133">출력:</span><span class="sxs-lookup"><span data-stu-id="17853-133">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.6.2
k8s-agent-98dc3136-1    Ready                      5m        v1.6.2
k8s-agent-98dc3136-2    Ready                      5m        v1.6.2
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.6.2
```

<span data-ttu-id="17853-134">이 자습서를 마치면 ACS Kubernetes 클러스터가 워크로드에 대해 준비됩니다.</span><span class="sxs-lookup"><span data-stu-id="17853-134">At tutorial completion, you have an ACS Kubernetes cluster ready for workloads.</span></span> <span data-ttu-id="17853-135">이후 자습서에서는 다중 컨테이너 응용 프로그램이 이 클러스터에 배포, 규모 확장, 업데이트 및 모니터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="17853-135">In subsequent tutorials, a multi-container application is deployed to this cluster, scaled out, updated, and monitored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="17853-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="17853-136">Next steps</span></span>

<span data-ttu-id="17853-137">이 자습서에서는 Azure Container Service Kubernetes 클러스터를 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="17853-137">In this tutorial, an Azure Container Service Kubernetes cluster was deployed.</span></span> <span data-ttu-id="17853-138">다음 단계가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="17853-138">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="17853-139">Kubernetes ACS 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="17853-139">Deployed a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="17853-140">Kubernetes CLI(kubectl) 설치</span><span class="sxs-lookup"><span data-stu-id="17853-140">Installed the Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="17853-141">kubectl 구성</span><span class="sxs-lookup"><span data-stu-id="17853-141">Configured kubectl</span></span>

<span data-ttu-id="17853-142">다음 자습서로 이동하여 클러스터에서 응용 프로그램 실행에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="17853-142">Advance to the next tutorial to learn about running application on the cluster.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="17853-143">Kubernetes에서 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="17853-143">Deploy application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-deploy-application.md)
