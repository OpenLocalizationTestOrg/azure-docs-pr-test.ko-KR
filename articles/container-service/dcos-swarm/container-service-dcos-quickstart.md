---
title: "Azure Container Service 빠른 시작 - DC/OS 클러스터 배포 | Microsoft Docs"
description: "Azure Container Service 빠른 시작 - DC/OS 클러스터 배포"
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
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: a31170369de9bc1ddcddb97171281b0014af95f9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-dcos-cluster"></a><span data-ttu-id="b28c1-104">DC/OS 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="b28c1-104">Deploy a DC/OS cluster</span></span>

<span data-ttu-id="b28c1-105">DC/OS는 컨테이너화된 최신 응용 프로그램 실행을 위한 분산 플랫폼을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="b28c1-106">Azure Container Service를 통해 프로덕션이 준비된 DC/OS 클러스터를 프로비전하는 작업은 간단하고 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="b28c1-107">이 빠른 시작에서는 DC/OS 클러스터를 배포하고 기본 워크로드를 실행하는 데 필요한 기본 단계를 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-107">This quick start details the basic steps needed to deploy a DC/OS cluster and run basic workload.</span></span>

<span data-ttu-id="b28c1-108">Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="b28c1-109">이 자습서에는 Azure CLI 버전 2.0.4 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-109">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="b28c1-110">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="b28c1-111">업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b28c1-111">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="log-in-to-azure"></a><span data-ttu-id="b28c1-112">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="b28c1-112">Log in to Azure</span></span> 

<span data-ttu-id="b28c1-113">[az login](/cli/azure/#login) 명령으로 Azure 구독에 로그인하고 화면의 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-113">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli
az login
```

## <a name="create-a-resource-group"></a><span data-ttu-id="b28c1-114">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="b28c1-114">Create a resource group</span></span>

<span data-ttu-id="b28c1-115">[az group create](/cli/azure/group#create) 명령을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-115">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="b28c1-116">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-116">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="b28c1-117">다음 예제에서는 *eastus* 위치에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-117">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-dcos-cluster"></a><span data-ttu-id="b28c1-118">DC/OS 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="b28c1-118">Create DC/OS cluster</span></span>

<span data-ttu-id="b28c1-119">[az acs create](/cli/azure/acs#create) 명령을 사용하여 DC/OS 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-119">Create a DC/OS cluster with the [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="b28c1-120">다음 예제에서는 *myDCOSCluster*라는 DC/OS 클러스터를 만들고 SSH 키가 없는 경우 이 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-120">The following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="b28c1-121">특정 키 집합을 사용하려면 `--ssh-key-value` 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-121">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="b28c1-122">몇 분 후 명령이 완료되고 배포에 대한 정보가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-122">After several minutes, the command completes, and returns information about the deployment.</span></span>

## <a name="connect-to-dcos-cluster"></a><span data-ttu-id="b28c1-123">DC/OS 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="b28c1-123">Connect to DC/OS cluster</span></span>

<span data-ttu-id="b28c1-124">DC/OS 클러스터를 만들면 SSH 터널을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-124">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="b28c1-125">다음 명령을 실행하여 DC/OS 마스터의 공용 IP 주소를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-125">Run the following command to return the public IP address of the DC/OS master.</span></span> <span data-ttu-id="b28c1-126">이 IP 주소는 변수에 저장되어 다음 단계에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-126">This IP address is stored in a variable and used in the next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="b28c1-127">SSH 터널을 만들려면 다음 명령을 실행하고 화면에 나타나는 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="b28c1-127">To create the SSH tunnel, run the following command and follow the on-screen instructions.</span></span> <span data-ttu-id="b28c1-128">포트 80이 이미 사용 중인 경우 명령이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-128">If port 80 is already in use, the command fails.</span></span> <span data-ttu-id="b28c1-129">터널링된 포트를 `85:localhost:80`과 같이 사용하지 않는 포트로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-129">Update the tunneled port to one not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

<span data-ttu-id="b28c1-130">`http://localhost`로 이동하여 SSH 터널을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-130">The SSH tunnel can be tested by browsing to `http://localhost`.</span></span> <span data-ttu-id="b28c1-131">80이 아닌 포트를 사용한 경우 위치를 일치하도록 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-131">If a port other that 80 has been used, adjust the location to match.</span></span> 

<span data-ttu-id="b28c1-132">SSH 터널이 성공적으로 만들어진 경우 DC/OS 포털이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-132">If the SSH tunnel was successfully created, the DC/OS portal is returned.</span></span>

![DCOS UI](./media/container-service-dcos-quickstart/dcos-ui.png)

## <a name="install-dcos-cli"></a><span data-ttu-id="b28c1-134">DC/OS CLI 설치</span><span class="sxs-lookup"><span data-stu-id="b28c1-134">Install DC/OS CLI</span></span>

<span data-ttu-id="b28c1-135">명령줄에서 DC/OS 클러스터를 관리하는 데 DC/OS 명령줄 인터페이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-135">The DC/OS command line interface is used to manage a DC/OS cluster from the command-line.</span></span> <span data-ttu-id="b28c1-136">[az acs dcos install-cli](/azure/acs/dcos#install-cli) 명령을 사용하여 DC/OS 클라이언트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-136">Install the DC/OS cli using the [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="b28c1-137">Azure Cloud Shell을 사용하는 경우 DC/OS CLI가 이미 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-137">If you are using Azure CloudShell, the DC/OS CLI is already installed.</span></span> 

<span data-ttu-id="b28c1-138">macOS 또는 Linux에서 Azure CLI를 실행하는 경우 sudo를 사용하여 이 명령을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-138">If you are running the Azure CLI on macOS or Linux, you might need to run the command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="b28c1-139">CLI를 클러스터 함께 사용하기 전에 SSH 터널을 사용하도록 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-139">Before the CLI can be used with the cluster, it must be configured to use the SSH tunnel.</span></span> <span data-ttu-id="b28c1-140">이렇게 하려면 필요한 경우 포트를 조정하여 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-140">To do so, run the following command, adjusting the port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="b28c1-141">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="b28c1-141">Run an application</span></span>

<span data-ttu-id="b28c1-142">ACS DC/OS 클러스터의 기본 예약 메커니즘은 Marathon입니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-142">The default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="b28c1-143">Marathon은 응용 프로그램을 시작하고 DC/OS 클러스터에서 응용 프로그램의 상태를 관리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-143">Marathon is used to start an application and manage the state of the application on the DC/OS cluster.</span></span> <span data-ttu-id="b28c1-144">Marathon을 통해 응용 프로그램을 예약하려면 *marathon-app.json*이라는 파일을 만들고 여기에 다음과 같은 내용을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-144">To schedule an application through Marathon, create a file named *marathon-app.json*, and copy the following contents into it.</span></span> 

```json
{
  "id": "demo-app",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  },
  "acceptedResourceRoles": [
    "slave_public"
  ]
}
```

<span data-ttu-id="b28c1-145">DC/OS 클러스터에서 실행되도록 응용 프로그램을 예약하는 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-145">Run the following command to schedule the application to run on the DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="b28c1-146">앱의 배포 상태를 보려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-146">To see the deployment status for the app, run the following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="b28c1-147">**대기** 열 값이 *True*에서 *False*로 전환되는 경우 응용 프로그램 배포가 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-147">When the **WAITING** column value switches from *True* to *False*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/1    ---       ---      False      DOCKER   None
```

<span data-ttu-id="b28c1-148">DC/OS 클러스터 에이전트의 공용 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-148">Get the public IP address of the DC/OS cluster agents.</span></span>

```azurecli
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="b28c1-149">이 주소를 찾아 NGINX 기본 사이트를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-149">Browsing to this address returns the default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-quickstart/nginx.png)

## <a name="delete-dcos-cluster"></a><span data-ttu-id="b28c1-151">DC/OS 클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="b28c1-151">Delete DC/OS cluster</span></span>

<span data-ttu-id="b28c1-152">더 이상 필요하지 않은 경우 [az group delete](/cli/azure/group#delete) 명령을 사용하여 리소스 그룹, DC/OS 클러스터 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-152">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="b28c1-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b28c1-153">Next steps</span></span>

<span data-ttu-id="b28c1-154">이 빠른 시작에서는 DC/OS 클러스터를 배포하고 클러스터에서 간단한 Docker 컨테이너를 실행했습니다.</span><span class="sxs-lookup"><span data-stu-id="b28c1-154">In this quick start, you’ve deployed a DC/OS cluster and have run a simple Docker container on the cluster.</span></span> <span data-ttu-id="b28c1-155">Azure Container Service에 대해 자세히 알아보려면 ACS 자습서로 계속 진행하세요.</span><span class="sxs-lookup"><span data-stu-id="b28c1-155">To learn more about Azure Container Service, continue to the ACS tutorials.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b28c1-156">ACS DC/OS 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="b28c1-156">Manage an ACS DC/OS Cluster</span></span>](container-service-dcos-manage-tutorial.md)