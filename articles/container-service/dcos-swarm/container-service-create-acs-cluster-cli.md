---
title: "Docker 컨테이너 클러스터 배포 - Azure CLI | Microsoft Docs"
description: "Azure CLI 2.0을 사용하여 Azure Container Service에 Kubernetes, DC/OS 또는 Docker Swarm 솔루션 배포"
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: azurecli
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: saudas
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: ecac5c255735b588ebb512b183e8a8bbbdcc905f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-the-azure-cli-20"></a><span data-ttu-id="26f6b-103">Azure CLI 2.0을 사용하여 Docker 컨테이너 호스팅 솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="26f6b-103">Deploy a Docker container hosting solution using the Azure CLI 2.0</span></span>

<span data-ttu-id="26f6b-104">Azure CLI 2.0의 `az acs` 명령을 사용하여 Azure Container Service에서 클러스터를 만들고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-104">Use the `az acs` commands in the Azure CLI 2.0 to create and manage clusters in Azure Container Service.</span></span> <span data-ttu-id="26f6b-105">[Azure Portal](container-service-deployment.md) 또는 Azure Container Service API를 사용하여 Azure Container Service 클러스터를 배포할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-105">You can also deploy an Azure Container Service cluster by using the [Azure portal](container-service-deployment.md) or the Azure Container Service APIs.</span></span>

<span data-ttu-id="26f6b-106">`az acs` 명령에 대한 도움말은 `-h` 매개 변수를 명령에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-106">For help on `az acs` commands, pass the `-h` parameter to any command.</span></span> <span data-ttu-id="26f6b-107">예: `az acs create -h`</span><span class="sxs-lookup"><span data-stu-id="26f6b-107">For example: `az acs create -h`.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="26f6b-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="26f6b-108">Prerequisites</span></span>
<span data-ttu-id="26f6b-109">Azure CLI 2.0을 사용하여 Azure Container Service 클러스터를 만들려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-109">To create an Azure Container Service cluster using the Azure CLI 2.0, you must:</span></span>
* <span data-ttu-id="26f6b-110">Azure 계정([무료 평가판 받기](https://azure.microsoft.com/pricing/free-trial/))이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-110">have an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/))</span></span>
* <span data-ttu-id="26f6b-111">[Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치하고 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-111">have installed and set up the [Azure CLI 2.0](/cli/azure/install-az-cli2)</span></span>

## <a name="get-started"></a><span data-ttu-id="26f6b-112">시작</span><span class="sxs-lookup"><span data-stu-id="26f6b-112">Get started</span></span> 
### <a name="log-in-to-your-account"></a><span data-ttu-id="26f6b-113">계정에 로그인</span><span class="sxs-lookup"><span data-stu-id="26f6b-113">Log in to your account</span></span>
```azurecli
az login 
```

<span data-ttu-id="26f6b-114">프롬프트를 따라 대화형으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-114">Follow the prompts to log in interactively.</span></span> <span data-ttu-id="26f6b-115">로그인을 위한 다른 메서드는 [Azure CLI 2.0 시작](/cli/azure/get-started-with-az-cli2)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26f6b-115">For other methods to log in, see [Get started with Azure CLI 2.0](/cli/azure/get-started-with-az-cli2).</span></span>

### <a name="set-your-azure-subscription"></a><span data-ttu-id="26f6b-116">Azure 구독 설정</span><span class="sxs-lookup"><span data-stu-id="26f6b-116">Set your Azure subscription</span></span>

<span data-ttu-id="26f6b-117">Azure 구독이 두 개 이상인 경우 기본 구독을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-117">If you have more than one Azure subscription, set the default subscription.</span></span> <span data-ttu-id="26f6b-118">예:</span><span class="sxs-lookup"><span data-stu-id="26f6b-118">For example:</span></span>

```
az account set --subscription "f66xxxxx-xxxx-xxxx-xxx-zgxxxx33cha5"
```


### <a name="create-a-resource-group"></a><span data-ttu-id="26f6b-119">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="26f6b-119">Create a resource group</span></span>
<span data-ttu-id="26f6b-120">모든 클러스터에 대한 리소스 그룹을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-120">We recommend that you create a resource group for every cluster.</span></span> <span data-ttu-id="26f6b-121">Azure Container Service가 [사용 가능](https://azure.microsoft.com/en-us/regions/services/)한 Azure 지역을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-121">Specify an Azure region in which Azure Container Service is [available](https://azure.microsoft.com/en-us/regions/services/).</span></span> <span data-ttu-id="26f6b-122">예:</span><span class="sxs-lookup"><span data-stu-id="26f6b-122">For example:</span></span>

```azurecli
az group create -n acsrg1 -l "westus"
```
<span data-ttu-id="26f6b-123">다음과 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-123">Output is similar to the following:</span></span>

![리소스 그룹 만들기](./media/container-service-create-acs-cluster-cli/rg-create.png)


## <a name="create-an-azure-container-service-cluster"></a><span data-ttu-id="26f6b-125">Azure Container Service 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="26f6b-125">Create an Azure Container Service cluster</span></span>

<span data-ttu-id="26f6b-126">클러스터를 만들려면 `az acs create`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-126">To create a cluster, use `az acs create`.</span></span>
<span data-ttu-id="26f6b-127">컨테이너의 이름, 이전 단계에서 만든 리소스 그룹의 이름은 필수 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-127">A name for the cluster and the name of the resource group created in the previous step are mandatory parameters.</span></span> 

<span data-ttu-id="26f6b-128">해당 스위치를 사용하여 덮어쓰지 않는 한, 다른 입력은 기본값으로 설정됩니다(다음 화면 참조).</span><span class="sxs-lookup"><span data-stu-id="26f6b-128">Other inputs are set to default values (see the following screen) unless overwritten using their respective switches.</span></span> <span data-ttu-id="26f6b-129">예를 들어 orchestrator는 기본으로 DC/OS로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-129">For example, the orchestrator is set by default to DC/OS.</span></span> <span data-ttu-id="26f6b-130">지정하지 않는 경우 DNS 이름 접두사는 클러스터 이름에 따라 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-130">And if you don't specify one, a DNS name prefix is created based on the cluster name.</span></span>

![az acs create 사용](./media/container-service-create-acs-cluster-cli/create-help.png)


### <a name="quick-acs-create-using-defaults"></a><span data-ttu-id="26f6b-132">기본값을 사용하는 빠른 `acs create`</span><span class="sxs-lookup"><span data-stu-id="26f6b-132">Quick `acs create` using defaults</span></span>
<span data-ttu-id="26f6b-133">기본 위치에 SSH RSA 공개 키 파일 `id_rsa.pub`가 있는 경우(또는 [OS X 및 Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) 또는 [Windows](../../virtual-machines/linux/ssh-from-windows.md)용으로 만든 경우) 다음과 같은 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-133">If you have an SSH RSA public key file `id_rsa.pub` in the default location (or created one for [OS X and Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../../virtual-machines/linux/ssh-from-windows.md)), use a command like the following:</span></span>

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789
```
<span data-ttu-id="26f6b-134">SSH 공용 키가 없는 경우 다음 두 번째 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-134">If you don't have an SSH public key, use this second command.</span></span> <span data-ttu-id="26f6b-135">`--generate-ssh-keys` 스위치가 있는 이 명령은 SSH 공용 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-135">This command with the `--generate-ssh-keys` switch creates one for you.</span></span>

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789 --generate-ssh-keys
```

<span data-ttu-id="26f6b-136">명령을 입력한 후 클러스터가 만들어질 때까지 10분 정도 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-136">After you enter the command, wait for about 10 minutes for the cluster to be created.</span></span> <span data-ttu-id="26f6b-137">명령 출력은 마스터의 FQDN(정규화된 도메인 이름) 및 에이전트 노드 및 첫 번째 마스터에 연결하기 위한 SSH 명령을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-137">The command output includes fully qualified domain names (FQDNs) of the master and agent nodes and an SSH command to connect to the first master.</span></span> <span data-ttu-id="26f6b-138">다음은 축약된 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-138">Here is abbreviated output:</span></span>

![이미지 ACS create](./media/container-service-create-acs-cluster-cli/cluster-create.png)

> [!TIP]
> <span data-ttu-id="26f6b-140">[Kubernetes 연습](../kubernetes/container-service-kubernetes-walkthrough.md)은 Kubernetes 클러스터를 만드는 기본값으로 `az acs create`를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-140">The [Kubernetes walkthrough](../kubernetes/container-service-kubernetes-walkthrough.md) shows how to use `az acs create` with default values to create a Kubernetes cluster.</span></span>
>

## <a name="manage-acs-clusters"></a><span data-ttu-id="26f6b-141">ACS 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="26f6b-141">Manage ACS clusters</span></span>

<span data-ttu-id="26f6b-142">추가 `az acs` 명령을 사용하여 클러스터를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-142">Use additional `az acs` commands to manage your cluster.</span></span> <span data-ttu-id="26f6b-143">다음은 몇 가지 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-143">Here are some examples.</span></span>

### <a name="list-clusters-under-a-subscription"></a><span data-ttu-id="26f6b-144">구독 아래에 클러스터 나열</span><span class="sxs-lookup"><span data-stu-id="26f6b-144">List clusters under a subscription</span></span>

```azurecli
az acs list --output table
```

### <a name="list-clusters-in-a-resource-group"></a><span data-ttu-id="26f6b-145">리소스 그룹의 클러스터 나열</span><span class="sxs-lookup"><span data-stu-id="26f6b-145">List clusters in a resource group</span></span>

```azurecli
az acs list -g acsrg1 --output table
```

![acs 목록](./media/container-service-create-acs-cluster-cli/acs-list.png)


### <a name="display-details-of-a-container-service-cluster"></a><span data-ttu-id="26f6b-147">컨테이너 서비스 클러스터 세부 정보 표시</span><span class="sxs-lookup"><span data-stu-id="26f6b-147">Display details of a container service cluster</span></span>

```azurecli
az acs show -g acsrg1 -n acs-cluster --output list
```

![acs 표시](./media/container-service-create-acs-cluster-cli/acs-show.png)


### <a name="scale-the-cluster"></a><span data-ttu-id="26f6b-149">클러스터 크기 조정</span><span class="sxs-lookup"><span data-stu-id="26f6b-149">Scale the cluster</span></span>
<span data-ttu-id="26f6b-150">에이전트 노드의 확장 및 축소가 모두 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-150">Both scaling in and scaling out of agent nodes are allowed.</span></span> <span data-ttu-id="26f6b-151">`new-agent-count` 매개 변수는 ACS 클러스터의 새 에이전트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-151">The parameter `new-agent-count` is the new number of agents in the ACS cluster.</span></span>

```azurecli
az acs scale -g acsrg1 -n acs-cluster --new-agent-count 4
```

![acs scale](./media/container-service-create-acs-cluster-cli/acs-scale.png)

## <a name="delete-a-container-service-cluster"></a><span data-ttu-id="26f6b-153">컨테이너 서비스 클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="26f6b-153">Delete a container service cluster</span></span>
```azurecli
az acs delete -g acsrg1 -n acs-cluster 
```
<span data-ttu-id="26f6b-154">이 명령은 컨테이너 서비스를 만드는 동안 만들어진 모든 리소스(네트워크 및 저장소)를 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-154">This command does not delete all resources (network and storage) created while creating the container service.</span></span> <span data-ttu-id="26f6b-155">모든 리소스를 쉽게 삭제하려면 고유한 리소스 그룹에 각 클러스터를 배포하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-155">To delete all resources easily, it is recommended you deploy each cluster in a distinct resource group.</span></span> <span data-ttu-id="26f6b-156">그런 다음 클러스터가 더 이상 필요하지 않을 때 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="26f6b-156">Then, delete the resource group when the cluster is no longer required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26f6b-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="26f6b-157">Next steps</span></span>
<span data-ttu-id="26f6b-158">이제 클러스터가 작동하기 시작했으니 연결 및 관리 정보는 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26f6b-158">Now that you have a functioning cluster, see these documents for connection and management details:</span></span>

* [<span data-ttu-id="26f6b-159">Azure 컨테이너 서비스 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="26f6b-159">Connect to an Azure Container Service cluster</span></span>](../container-service-connect.md)
* [<span data-ttu-id="26f6b-160">Azure 컨테이너 서비스 및 DC/OS로 작업</span><span class="sxs-lookup"><span data-stu-id="26f6b-160">Work with Azure Container Service and DC/OS</span></span>](container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="26f6b-161">Azure 컨테이너 서비스 및 Docker Swarm으로 작업</span><span class="sxs-lookup"><span data-stu-id="26f6b-161">Work with Azure Container Service and Docker Swarm</span></span>](container-service-docker-swarm.md)
* [<span data-ttu-id="26f6b-162">Azure Container Service 및 Kubernetes로 작업</span><span class="sxs-lookup"><span data-stu-id="26f6b-162">Work with Azure Container Service and Kubernetes</span></span>](../kubernetes/container-service-kubernetes-walkthrough.md)