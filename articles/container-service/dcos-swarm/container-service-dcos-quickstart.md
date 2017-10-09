---
title: "컨테이너 서비스 빠른 시작-aaaAzure DC/OS 클러스터 배포 | Microsoft Docs"
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
ms.openlocfilehash: b961f15bd73deeafda5a3fc25ab53c839195219b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-dcos-cluster"></a><span data-ttu-id="cbed9-104">DC/OS 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="cbed9-104">Deploy a DC/OS cluster</span></span>

<span data-ttu-id="cbed9-105">DC/OS는 컨테이너화된 최신 응용 프로그램 실행을 위한 분산 플랫폼을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="cbed9-106">Azure Container Service를 통해 프로덕션이 준비된 DC/OS 클러스터를 프로비전하는 작업은 간단하고 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="cbed9-107">이 빠른 시작 정보는 기본 단계를 hello DC/OS 클러스터와 기본 실행된 작업 toodeploy 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-107">This quick start details hello basic steps needed toodeploy a DC/OS cluster and run basic workload.</span></span>

<span data-ttu-id="cbed9-108">Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="cbed9-109">이 자습서에서는 Azure CLI 버전 2.0.4 hello 이상.</span><span class="sxs-lookup"><span data-stu-id="cbed9-109">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="cbed9-110">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="cbed9-111">Tooupgrade 필요한 경우 참조 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-111">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="log-in-tooazure"></a><span data-ttu-id="cbed9-112">TooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="cbed9-112">Log in tooAzure</span></span> 

<span data-ttu-id="cbed9-113">Tooyour hello로 Azure 구독에에서 로그인 [az 로그인](/cli/azure/#login) 명령 열고 지시를 따른 hello 화면에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-113">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

## <a name="create-a-resource-group"></a><span data-ttu-id="cbed9-114">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="cbed9-114">Create a resource group</span></span>

<span data-ttu-id="cbed9-115">Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="cbed9-116">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-116">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="cbed9-117">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-117">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-dcos-cluster"></a><span data-ttu-id="cbed9-118">DC/OS 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="cbed9-118">Create DC/OS cluster</span></span>

<span data-ttu-id="cbed9-119">DC/OS 클러스터 hello로 만들기 [az acs 만들](/cli/azure/acs#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-119">Create a DC/OS cluster with hello [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="cbed9-120">hello 다음 예제에서는 명명 된 DC/OS 클러스터가 *myDCOSCluster* 하 고 존재 하지 않을 경우 SSH 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-120">hello following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="cbed9-121">toouse 특정 키의 집합, hello를 사용 하 여 `--ssh-key-value` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-121">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="cbed9-122">몇 분 후 hello 명령은 완료 되 면 hello 배포에 대 한 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-122">After several minutes, hello command completes, and returns information about hello deployment.</span></span>

## <a name="connect-toodcos-cluster"></a><span data-ttu-id="cbed9-123">TooDC/OS 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="cbed9-123">Connect tooDC/OS cluster</span></span>

<span data-ttu-id="cbed9-124">DC/OS 클러스터를 만들면 SSH 터널을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-124">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="cbed9-125">Hello 다음 hello DC/OS 마스터의 명령 tooreturn hello 공용 IP 주소를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-125">Run hello following command tooreturn hello public IP address of hello DC/OS master.</span></span> <span data-ttu-id="cbed9-126">이 IP 주소 변수에 저장 되 고 hello 다음 단계에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-126">This IP address is stored in a variable and used in hello next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="cbed9-127">toocreate는 SSH 터널 hello, hello 다음 명령을 실행 합니다. 지침을 따릅니다 hello 화면에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-127">toocreate hello SSH tunnel, run hello following command and follow hello on-screen instructions.</span></span> <span data-ttu-id="cbed9-128">포트 80 이미 사용 중이면 hello 명령이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-128">If port 80 is already in use, hello command fails.</span></span> <span data-ttu-id="cbed9-129">업데이트 hello와 같은, 사용 중이 아닌 포트 tooone 터널링 된 `85:localhost:80`합니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-129">Update hello tunneled port tooone not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

<span data-ttu-id="cbed9-130">너무 이동 하 여 hello SSH 터널을 테스트할 수 있습니다`http://localhost`합니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-130">hello SSH tunnel can be tested by browsing too`http://localhost`.</span></span> <span data-ttu-id="cbed9-131">포트가 80 사용 된 다른 hello 위치 toomatch를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-131">If a port other that 80 has been used, adjust hello location toomatch.</span></span> 

<span data-ttu-id="cbed9-132">Hello SSH 터널 성공적으로 만들었습니다 hello DC/OS 포털 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-132">If hello SSH tunnel was successfully created, hello DC/OS portal is returned.</span></span>

![DCOS UI](./media/container-service-dcos-quickstart/dcos-ui.png)

## <a name="install-dcos-cli"></a><span data-ttu-id="cbed9-134">DC/OS CLI 설치</span><span class="sxs-lookup"><span data-stu-id="cbed9-134">Install DC/OS CLI</span></span>

<span data-ttu-id="cbed9-135">hello DC/OS 명령줄 인터페이스에 사용 되는 toomanage hello 명령줄에서 DC/OS 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-135">hello DC/OS command line interface is used toomanage a DC/OS cluster from hello command-line.</span></span> <span data-ttu-id="cbed9-136">Hello를 사용 하 여 hello DC/OS cli를 설치 [az acs dcos 설치 cli](/azure/acs/dcos#install-cli) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-136">Install hello DC/OS cli using hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="cbed9-137">Azure CloudShell를 사용 하는 hello DC/OS CLI 이미 설치 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-137">If you are using Azure CloudShell, hello DC/OS CLI is already installed.</span></span> 

<span data-ttu-id="cbed9-138">Hello Azure CLI macOS 또는 Linux를 실행 하는 경우에 sudo 사용 하 여 toorun hello 명령을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-138">If you are running hello Azure CLI on macOS or Linux, you might need toorun hello command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="cbed9-139">Hello CLI를 사용 하 여 hello 클러스터 수, 하기 전에 구성 된 toouse hello SSH 터널 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-139">Before hello CLI can be used with hello cluster, it must be configured toouse hello SSH tunnel.</span></span> <span data-ttu-id="cbed9-140">따라서 toodo 다음 명령을, 필요한 경우 hello 포트 조정 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-140">toodo so, run hello following command, adjusting hello port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="cbed9-141">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="cbed9-141">Run an application</span></span>

<span data-ttu-id="cbed9-142">hello 예약 메커니즘 ACS DC/OS 클러스터에 대 한 기본값이 마라톤입니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-142">hello default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="cbed9-143">풀 마라톤은 응용 프로그램을 사용 하는 toostart 고 hello DC/OS 클러스터에서 hello 응용 프로그램의 hello 상태를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-143">Marathon is used toostart an application and manage hello state of hello application on hello DC/OS cluster.</span></span> <span data-ttu-id="cbed9-144">풀 마라톤을 통해 응용 프로그램 tooschedule 라는 파일을 만들어 *마라톤 app.json*, 복사 hello를 내용에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-144">tooschedule an application through Marathon, create a file named *marathon-app.json*, and copy hello following contents into it.</span></span> 

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

<span data-ttu-id="cbed9-145">Hello 명령 tooschedule hello 응용 프로그램 toorun hello DC/OS 클러스터에서 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-145">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="cbed9-146">hello 배포 상태를 toosee hello 앱의 경우 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-146">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="cbed9-147">Hello 때 **대기** 에서 전환 되는 열 값 *True* 너무*False*, 응용 프로그램 배포가 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-147">When hello **WAITING** column value switches from *True* too*False*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/1    ---       ---      False      DOCKER   None
```

<span data-ttu-id="cbed9-148">Hello hello DC/OS 클러스터 에이전트의 공용 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-148">Get hello public IP address of hello DC/OS cluster agents.</span></span>

```azurecli
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="cbed9-149">Hello 기본 NGINX 사이트를 반환 toothis 주소를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-149">Browsing toothis address returns hello default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-quickstart/nginx.png)

## <a name="delete-dcos-cluster"></a><span data-ttu-id="cbed9-151">DC/OS 클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="cbed9-151">Delete DC/OS cluster</span></span>

<span data-ttu-id="cbed9-152">더 이상 필요 hello를 사용할 수 없습니다 [az 그룹 삭제](/cli/azure/group#delete) tooremove hello 리소스 그룹, DC/OS 클러스터 및 관련 된 모든 리소스를 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-152">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="cbed9-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cbed9-153">Next steps</span></span>

<span data-ttu-id="cbed9-154">이 빠른 시작에서 DC/OS 클러스터 배포 되었으며을 hello 클러스터에서 간단한 Docker 컨테이너에 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-154">In this quick start, you’ve deployed a DC/OS cluster and have run a simple Docker container on hello cluster.</span></span> <span data-ttu-id="cbed9-155">Azure 컨테이너 서비스에 대해 자세히 toolearn toohello ACS 자습서를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbed9-155">toolearn more about Azure Container Service, continue toohello ACS tutorials.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cbed9-156">ACS DC/OS 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="cbed9-156">Manage an ACS DC/OS Cluster</span></span>](container-service-dcos-manage-tutorial.md)