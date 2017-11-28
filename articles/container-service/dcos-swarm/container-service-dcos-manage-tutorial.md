---
title: "aaaAzure 컨테이너 서비스 자습서-관리 DC/OS | Microsoft Docs"
description: "Azure Container Service 자습서 - DC/OS 관리"
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
ms.date: 07/17/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b91c433bfd7e48ec405cc62be1486d9d4662839d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-service-tutorial---manage-dcos"></a><span data-ttu-id="282d6-104">Azure Container Service 자습서 - DC/OS 관리</span><span class="sxs-lookup"><span data-stu-id="282d6-104">Azure Container Service tutorial - Manage DC/OS</span></span>

<span data-ttu-id="282d6-105">DC/OS는 컨테이너화된 최신 응용 프로그램 실행을 위한 분산 플랫폼을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="282d6-106">Azure Container Service를 통해 프로덕션이 준비된 DC/OS 클러스터를 프로비전하는 작업은 간단하고 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="282d6-107">이 빠른 시작 정보 기본 단계는 DC/OS 클러스터와 기본 실행된 작업 toodeploy 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-107">This quick start details basic steps needed toodeploy a DC/OS cluster and run basic workload.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="282d6-108">ACS DC/OS 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="282d6-108">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="282d6-109">Toohello 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="282d6-109">Connect toohello cluster</span></span>
> * <span data-ttu-id="282d6-110">Hello DC/OS CLI를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-110">Install hello DC/OS CLI</span></span>
> * <span data-ttu-id="282d6-111">응용 프로그램 toohello 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="282d6-111">Deploy an application toohello cluster</span></span>
> * <span data-ttu-id="282d6-112">Hello 클러스터에서 응용 프로그램 크기 조정</span><span class="sxs-lookup"><span data-stu-id="282d6-112">Scale an application on hello cluster</span></span>
> * <span data-ttu-id="282d6-113">Hello DC/OS 클러스터 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-113">Scale hello DC/OS cluster nodes</span></span>
> * <span data-ttu-id="282d6-114">기본 DC/OS 관리</span><span class="sxs-lookup"><span data-stu-id="282d6-114">Basic DC/OS management</span></span>
> * <span data-ttu-id="282d6-115">Hello DC/OS 클러스터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-115">Delete hello DC/OS cluster</span></span>

<span data-ttu-id="282d6-116">이 자습서에서는 Azure CLI 버전 2.0.4 hello 이상.</span><span class="sxs-lookup"><span data-stu-id="282d6-116">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="282d6-117">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-117">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="282d6-118">Tooupgrade 필요한 경우 참조 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-118">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-dcos-cluster"></a><span data-ttu-id="282d6-119">DC/OS 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="282d6-119">Create DC/OS cluster</span></span>

<span data-ttu-id="282d6-120">Hello로 리소스 그룹을 만들려면 먼저 [az 그룹 만들기](/cli/azure/group#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-120">First, create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="282d6-121">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-121">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="282d6-122">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *westeurope* 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-122">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="282d6-123">다음에 DC/OS 클러스터 hello로 만듭니다 [az acs 만들](/cli/azure/acs#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-123">Next, create a DC/OS cluster with hello [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="282d6-124">hello 다음 예제에서는 명명 된 DC/OS 클러스터가 *myDCOSCluster* 하 고 존재 하지 않을 경우 SSH 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-124">hello following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="282d6-125">toouse 특정 키의 집합, hello를 사용 하 여 `--ssh-key-value` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-125">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="282d6-126">몇 분 후 hello 명령은 완료 되 면 hello 배포에 대 한 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-126">After several minutes, hello command completes, and returns information about hello deployment.</span></span>

## <a name="connect-toodcos-cluster"></a><span data-ttu-id="282d6-127">TooDC/OS 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="282d6-127">Connect tooDC/OS cluster</span></span>

<span data-ttu-id="282d6-128">DC/OS 클러스터를 만들면 SSH 터널을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-128">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="282d6-129">Hello 다음 hello DC/OS 마스터의 명령 tooreturn hello 공용 IP 주소를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-129">Run hello following command tooreturn hello public IP address of hello DC/OS master.</span></span> <span data-ttu-id="282d6-130">이 IP 주소 변수에 저장 되 고 hello 다음 단계에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-130">This IP address is stored in a variable and used in hello next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="282d6-131">toocreate는 SSH 터널 hello, hello 다음 명령을 실행 합니다. 지침을 따릅니다 hello 화면에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-131">toocreate hello SSH tunnel, run hello following command and follow hello on-screen instructions.</span></span> <span data-ttu-id="282d6-132">포트 80 이미 사용 중이면 hello 명령이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-132">If port 80 is already in use, hello command fails.</span></span> <span data-ttu-id="282d6-133">업데이트 hello와 같은, 사용 중이 아닌 포트 tooone 터널링 된 `85:localhost:80`합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-133">Update hello tunneled port tooone not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

## <a name="install-dcos-cli"></a><span data-ttu-id="282d6-134">DC/OS CLI 설치</span><span class="sxs-lookup"><span data-stu-id="282d6-134">Install DC/OS CLI</span></span>

<span data-ttu-id="282d6-135">Hello를 사용 하 여 hello DC/OS cli를 설치 [az acs dcos 설치 cli](/azure/acs/dcos#install-cli) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-135">Install hello DC/OS cli using hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="282d6-136">Azure CloudShell를 사용 하는 hello DC/OS CLI 이미 설치 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-136">If you are using Azure CloudShell, hello DC/OS CLI is already installed.</span></span> <span data-ttu-id="282d6-137">Hello Azure CLI macOS 또는 Linux를 실행 하는 경우에 sudo 사용 하 여 toorun hello 명령을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-137">If you are running hello Azure CLI on macOS or Linux, you might need toorun hello command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="282d6-138">Hello CLI를 사용 하 여 hello 클러스터 수, 하기 전에 구성 된 toouse hello SSH 터널 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-138">Before hello CLI can be used with hello cluster, it must be configured toouse hello SSH tunnel.</span></span> <span data-ttu-id="282d6-139">따라서 toodo 다음 명령을, 필요한 경우 hello 포트 조정 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-139">toodo so, run hello following command, adjusting hello port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="282d6-140">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="282d6-140">Run an application</span></span>

<span data-ttu-id="282d6-141">hello 예약 메커니즘 ACS DC/OS 클러스터에 대 한 기본값이 마라톤입니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-141">hello default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="282d6-142">풀 마라톤은 응용 프로그램을 사용 하는 toostart 고 hello DC/OS 클러스터에서 hello 응용 프로그램의 hello 상태를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-142">Marathon is used toostart an application and manage hello state of hello application on hello DC/OS cluster.</span></span> <span data-ttu-id="282d6-143">풀 마라톤을 통해 응용 프로그램 tooschedule 라는 파일을 만들어 **마라톤 app.json**, 복사 hello를 내용에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-143">tooschedule an application through Marathon, create a file named **marathon-app.json**, and copy hello following contents into it.</span></span> 

```json
{
  "id": "demo-app-private",
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
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

<span data-ttu-id="282d6-144">Hello 명령 tooschedule hello 응용 프로그램 toorun hello DC/OS 클러스터에서 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-144">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="282d6-145">hello 배포 상태를 toosee hello 앱의 경우 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-145">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="282d6-146">Hello 때 **작업** 에서 전환 되는 열 값 *0/1* 너무*1/1*, 응용 프로그램 배포가 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-146">When hello **TASKS** column value switches from *0/1* too*1/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     0/1    ---       ---      False      DOCKER   None
```

## <a name="scale-marathon-application"></a><span data-ttu-id="282d6-147">Marathon 응용 프로그램 크기 조정</span><span class="sxs-lookup"><span data-stu-id="282d6-147">Scale Marathon application</span></span>

<span data-ttu-id="282d6-148">Hello 이전 예제에서는 단일 인스턴스 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-148">In hello previous example, a single instance application was created.</span></span> <span data-ttu-id="282d6-149">이 배포 hello 응용 프로그램의 세 인스턴스를 사용할 수 있도록 개방 hello tooupdate **마라톤 app.json** 파일을 찾아 hello 인스턴스 속성 too3 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-149">tooupdate this deployment so that three instances of hello application are available, open up hello **marathon-app.json** file, and update hello instance property too3.</span></span>

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 3,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

<span data-ttu-id="282d6-150">Hello를 사용 하 여 hello 응용 프로그램 업데이트 `dcos marathon app update` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-150">Update hello application using hello `dcos marathon app update` command.</span></span>

```azurecli
dcos marathon app update demo-app-private < marathon-app.json
```

<span data-ttu-id="282d6-151">hello 배포 상태를 toosee hello 앱의 경우 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-151">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="282d6-152">Hello 때 **작업** 에서 전환 되는 열 값 *1/3* 너무*3/1*, 응용 프로그램 배포가 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-152">When hello **TASKS** column value switches from *1/3* too*3/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/3    ---       ---      False      DOCKER   None
```

## <a name="run-internet-accessible-app"></a><span data-ttu-id="282d6-153">인터넷에 액세스 가능한 앱 실행</span><span class="sxs-lookup"><span data-stu-id="282d6-153">Run internet accessible app</span></span>

<span data-ttu-id="282d6-154">hello ACS DC/OS 클러스터 구성 되어 두 노드 집합에 액세스할 수 있는 공용 인터넷을 hello 및 개인은에 액세스할 수 없는 인터넷 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-154">hello ACS DC/OS cluster consists of two node sets, one public which is accessible on hello internet, and one private which is not accessible on hello internet.</span></span> <span data-ttu-id="282d6-155">hello 기본 집합이 hello 개인 노드 hello 마지막 예제에서는 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-155">hello default set is hello private nodes, which was used in hello last example.</span></span>

<span data-ttu-id="282d6-156">toomake 액세스할 수 있는 응용 프로그램, 인터넷 hello toohello 공용 노드 집합을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-156">toomake an application accessible on hello internet, deploy them toohello public node set.</span></span> <span data-ttu-id="282d6-157">toodo, 하 게 hello `acceptedResourceRoles` 개체의 값 `slave_public`합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-157">toodo so, give hello `acceptedResourceRoles` object a value of `slave_public`.</span></span>

<span data-ttu-id="282d6-158">라는 파일을 만들어 **nginx public.json** 복사 hello를 내용에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-158">Create a file named **nginx-public.json** and copy hello following contents into it.</span></span>

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

<span data-ttu-id="282d6-159">Hello 명령 tooschedule hello 응용 프로그램 toorun hello DC/OS 클러스터에서 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-159">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli 
dcos marathon app add nginx-public.json
```

<span data-ttu-id="282d6-160">Hello hello DC/OS 공용 클러스터 에이전트의 공용 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-160">Get hello public IP address of hello DC/OS public cluster agents.</span></span>

```azurecli 
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="282d6-161">Hello 기본 NGINX 사이트를 반환 toothis 주소를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-161">Browsing toothis address returns hello default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-manage-tutorial/nginx.png)

## <a name="scale-dcos-cluster"></a><span data-ttu-id="282d6-163">DC/OS 클러스터 크기 조정</span><span class="sxs-lookup"><span data-stu-id="282d6-163">Scale DC/OS cluster</span></span>

<span data-ttu-id="282d6-164">Hello 이전 예제에서 응용 프로그램 크기 조정 된 toomultiple 인스턴스 했습니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-164">In hello previous examples, an application was scaled toomultiple instance.</span></span> <span data-ttu-id="282d6-165">hello DC/OS 인프라 많거나 적은 계산 용량 크기 조정 된 tooprovide 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-165">hello DC/OS infrastructure can also be scaled tooprovide more or less compute capacity.</span></span> <span data-ttu-id="282d6-166">Hello로 이렇게 [az acs 확장]() 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-166">This is done with hello [az acs scale]() command.</span></span> 

<span data-ttu-id="282d6-167">hello를 사용 하 여 hello toosee DC/OS 에이전트의 현재 개수 [az acs 표시](/cli/azure/acs#show) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-167">toosee hello current count of DC/OS agents, use hello [az acs show](/cli/azure/acs#show) command.</span></span>

```azurecli
az acs show --resource-group myResourceGroup --name myDCOSCluster --query "agentPoolProfiles[0].count"
```

<span data-ttu-id="282d6-168">tooincrease count too5 hello, hello를 사용 하 여 [az acs 확장](/cli/azure/acs#scale) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-168">tooincrease hello count too5, use hello [az acs scale](/cli/azure/acs#scale) command.</span></span> 

```azurecli
az acs scale --resource-group myResourceGroup --name myDCOSCluster --new-agent-count 5
```

## <a name="delete-dcos-cluster"></a><span data-ttu-id="282d6-169">DC/OS 클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="282d6-169">Delete DC/OS cluster</span></span>

<span data-ttu-id="282d6-170">더 이상 필요 hello를 사용할 수 없습니다 [az 그룹 삭제](/cli/azure/group#delete) tooremove hello 리소스 그룹, DC/OS 클러스터 및 관련 된 모든 리소스를 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-170">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="282d6-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="282d6-171">Next steps</span></span>

<span data-ttu-id="282d6-172">이 자습서에서는 hello 다음을 비롯 한 기본 DC/OS 관리 작업에 대해 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-172">In this tutorial, you have learned about basic DC/OS management task including hello following.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="282d6-173">ACS DC/OS 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="282d6-173">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="282d6-174">Toohello 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="282d6-174">Connect toohello cluster</span></span>
> * <span data-ttu-id="282d6-175">Hello DC/OS CLI를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-175">Install hello DC/OS CLI</span></span>
> * <span data-ttu-id="282d6-176">응용 프로그램 toohello 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="282d6-176">Deploy an application toohello cluster</span></span>
> * <span data-ttu-id="282d6-177">Hello 클러스터에서 응용 프로그램 크기 조정</span><span class="sxs-lookup"><span data-stu-id="282d6-177">Scale an application on hello cluster</span></span>
> * <span data-ttu-id="282d6-178">Hello DC/OS 클러스터 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-178">Scale hello DC/OS cluster nodes</span></span>
> * <span data-ttu-id="282d6-179">Hello DC/OS 클러스터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-179">Delete hello DC/OS cluster</span></span>

<span data-ttu-id="282d6-180">고급 toohello 다음 자습서 toolearn에 대 한 Azure에서 DC/OS 분산 응용 프로그램을 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="282d6-180">Advance toohello next tutorial toolearn about load balancing application in DC/OS on Azure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="282d6-181">부하 분산 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="282d6-181">Load balance applications</span></span>](container-service-load-balancing.md)