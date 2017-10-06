---
title: "Linux 용 Azure Docker CE 클러스터 aaaQuickstart-| Microsoft Docs"
description: "신속 하 게 toocreate hello Azure CLI를 사용 하 여 Azure 컨테이너 서비스의 Linux 컨테이너에 대 한 Docker CE 클러스터에 알아봅니다."
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, Docker, Swarm
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nepeters
ms.custom: 
ms.openlocfilehash: 6c26c12ed085ec379c3486095a5fa51379afc5a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-docker-ce-cluster"></a><span data-ttu-id="901ce-103">Docker CE 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="901ce-103">Deploy Docker CE cluster</span></span>

<span data-ttu-id="901ce-104">이 빠른 시작에서는 Docker CE 클러스터 hello Azure CLI를 사용 하 여 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-104">In this quick start, a Docker CE cluster is deployed using hello Azure CLI.</span></span> <span data-ttu-id="901ce-105">그런 다음 웹 프런트 엔드 및 Redis 인스턴스로 구성 된 다중 컨테이너 응용 프로그램 배포 하 고 hello 클러스터에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on hello cluster.</span></span> <span data-ttu-id="901ce-106">Hello 응용 프로그램을 통해 액세스할 수는 완료 되 면 인터넷 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-106">Once completed, hello application is accessible over hello internet.</span></span>

<span data-ttu-id="901ce-107">Azure Container Service에서 Docker CE는 미리 보기 상태이며 **프로덕션 워크로드에는 사용할 수 없습니다**.</span><span class="sxs-lookup"><span data-stu-id="901ce-107">Docker CE on Azure Container Service is in preview and **should not be used for production workloads**.</span></span>

<span data-ttu-id="901ce-108">Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="901ce-109">이 퀵 스타트의 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 필요 tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여 이후 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-109">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="901ce-110">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="901ce-111">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-111">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="901ce-112">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="901ce-112">Create a resource group</span></span>

<span data-ttu-id="901ce-113">Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-113">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="901ce-114">Azure 리소스 그룹은 Azure 리소스가 배포되고 관리되는 논리 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="901ce-115">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *ukwest* 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-115">hello following example creates a resource group named *myResourceGroup* in hello *ukwest* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location ukwest
```

<span data-ttu-id="901ce-116">출력:</span><span class="sxs-lookup"><span data-stu-id="901ce-116">Output:</span></span>

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westcentralus",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-docker-swarm-cluster"></a><span data-ttu-id="901ce-117">Docker Swarm 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="901ce-117">Create Docker Swarm cluster</span></span>

<span data-ttu-id="901ce-118">Hello로 Azure 컨테이너 서비스의 Docker CE 클러스터 만들기 [az acs 만들](/cli/azure/acs#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-118">Create a Docker CE cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="901ce-119">hello 다음 예제에서는 명명 된 클러스터가 *mySwarmCluster* 와 하나의 Linux 마스터 노드 및 Linux 에이전트 노드를 세 개 있습니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-119">hello following example creates a cluster named *mySwarmCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type dockerce --resource-group myResourceGroup --generate-ssh-keys
```

<span data-ttu-id="901ce-120">몇 분 후 hello 명령을 완료 하 고 hello 클러스터에 대 한 json 형식 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-120">After several minutes, hello command completes and returns json formatted information about hello cluster.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="901ce-121">Toohello 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="901ce-121">Connect toohello cluster</span></span>

<span data-ttu-id="901ce-122">이 빠른 시작 전체에서 hello FQDN hello docker는 Docker Swarm 마스터와 hello Docker 에이전트 풀을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-122">Throughout this quick start, you need hello FQDN of both hello Docker Swarm master and hello Docker agent pool.</span></span> <span data-ttu-id="901ce-123">다음 명령을 tooreturn 둘 다 hello 마스터 및 에이전트 Fqdn hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-123">Run hello following command tooreturn both hello master and agent FQDNs.</span></span>


```bash
az acs list --resource-group myResourceGroup --query '[*].{Master:masterProfile.fqdn,Agent:agentPoolProfiles[0].fqdn}' -o table
```

<span data-ttu-id="901ce-124">출력:</span><span class="sxs-lookup"><span data-stu-id="901ce-124">Output:</span></span>

```bash
Master                                                               Agent
-------------------------------------------------------------------  --------------------------------------------------------------------
myswarmcluster-myresourcegroup-d5b9d4mgmt.ukwest.cloudapp.azure.com  myswarmcluster-myresourcegroup-d5b9d4agent.ukwest.cloudapp.azure.com
```

<span data-ttu-id="901ce-125">SSH 터널 toohello 웜 마스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-125">Create an SSH tunnel toohello Swarm master.</span></span> <span data-ttu-id="901ce-126">대체 `MasterFQDN` hello 웜 마스터의 hello FQDN 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-126">Replace `MasterFQDN` with hello FQDN address of hello Swarm master.</span></span>

```bash
ssh -p 2200 -fNL localhost:2374:/var/run/docker.sock azureuser@MasterFQDN
```

<span data-ttu-id="901ce-127">집합 hello `DOCKER_HOST` 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-127">Set hello `DOCKER_HOST` environment variable.</span></span> <span data-ttu-id="901ce-128">이렇게 하면 있습니다 docker는 Docker Swarm hello에 대해 toorun docker 명령을 hello 호스트의 toospecify hello 이름이 필요 없이.</span><span class="sxs-lookup"><span data-stu-id="901ce-128">This allows you toorun docker commands against hello Docker Swarm without having toospecify hello name of hello host.</span></span>

```bash
export DOCKER_HOST=localhost:2374
```

<span data-ttu-id="901ce-129">Docker는 Docker Swarm hello에서 준비 toorun Docker 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-129">You are now ready toorun Docker services on hello Docker Swarm.</span></span>


## <a name="run-hello-application"></a><span data-ttu-id="901ce-130">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="901ce-130">Run hello application</span></span>

<span data-ttu-id="901ce-131">라는 파일을 만들어 `azure-vote.yaml` 고 복사 hello에 콘텐츠를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-131">Create a file named `azure-vote.yaml` and copy hello following content into it.</span></span>


```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:redis-v1
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

<span data-ttu-id="901ce-132">Hello 실행 [docker 스택 배포](https://docs.docker.com/engine/reference/commandline/stack_deploy/) toocreate hello Azure 투표 서비스 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-132">Run hello [docker stack deploy](https://docs.docker.com/engine/reference/commandline/stack_deploy/) command toocreate hello Azure Vote service.</span></span>

```bash
docker stack deploy azure-vote --compose-file azure-vote.yaml
```

<span data-ttu-id="901ce-133">출력:</span><span class="sxs-lookup"><span data-stu-id="901ce-133">Output:</span></span>

```bash
Creating network azure-vote_default
Creating service azure-vote_azure-vote-back
Creating service azure-vote_azure-vote-front
```

<span data-ttu-id="901ce-134">사용 하 여 hello [docker 스택 ps](https://docs.docker.com/engine/reference/commandline/stack_ps/) tooreturn hello 응용 프로그램의 배포 상태를 hello 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-134">Use hello [docker stack ps](https://docs.docker.com/engine/reference/commandline/stack_ps/) command tooreturn hello deployment status of hello application.</span></span>

```bash
docker stack ps azure-vote
```

<span data-ttu-id="901ce-135">한 번 hello `CURRENT STATE` 의 각 서비스는 `Running`, hello 응용 프로그램을 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-135">Once hello `CURRENT STATE` of each service is `Running`, hello application is ready.</span></span>

```bash
ID                  NAME                            IMAGE                                 NODE                               DESIRED STATE       CURRENT STATE                ERROR               PORTS
tnklkv3ogu3i        azure-vote_azure-vote-front.1   microsoft/azure-vote-front:redis-v1   swarmm-agentpool0-66066781000004   Running             Running 5 seconds ago                            
lg99i4hy68r9        azure-vote_azure-vote-back.1    redis:latest                          swarmm-agentpool0-66066781000002   Running             Running about a minute ago
```

## <a name="test-hello-application"></a><span data-ttu-id="901ce-136">Hello 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="901ce-136">Test hello application</span></span>

<span data-ttu-id="901ce-137">Toohello hello 웜 에이전트 풀 tootest hello Azure 투표 응용 프로그램으로의 FQDN을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-137">Browse toohello FQDN of hello Swarm agent pool tootest out hello Azure Vote application.</span></span>

![투표 tooAzure 검색 이미지](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a><span data-ttu-id="901ce-139">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="901ce-139">Delete cluster</span></span>
<span data-ttu-id="901ce-140">Hello hello 클러스터 필요는 더 이상 사용할 수 없습니다 [az 그룹 삭제](/cli/azure/group#delete) tooremove hello 리소스 그룹, 컨테이너 서비스와 관련 된 모든 리소스를 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-140">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a><span data-ttu-id="901ce-141">Hello 코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="901ce-141">Get hello code</span></span>

<span data-ttu-id="901ce-142">이 빠른 시작에서 미리 생성된 된 컨테이너 이미지 Docker 서비스가 사용 되는 toocreate 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-142">In this quick start, pre-created container images have been used toocreate a Docker service.</span></span> <span data-ttu-id="901ce-143">hello 관련 응용 프로그램 코드에서 Dockerfile 되며 Compose 파일 GitHub에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-143">hello related application code, Dockerfile, and Compose file are available on GitHub.</span></span>

[<span data-ttu-id="901ce-144">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="901ce-144">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="901ce-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="901ce-145">Next steps</span></span>

<span data-ttu-id="901ce-146">이 빠른 시작에서 docker는 Docker Swarm 클러스터를 배포 및 다중 컨테이너 응용 프로그램 tooit를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-146">In this quick start, you deployed a Docker Swarm cluster and deployed a multi-container application tooit.</span></span>

<span data-ttu-id="901ce-147">Docker 웜 Visual Studio Team Services와 통합 하는 방법에 대 한 toolearn toohello docker는 Docker Swarm 및 VSTS CI/CD를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="901ce-147">toolearn about integrating Docker warm with Visual Studio Team Services, continue toohello CI/CD with Docker Swarm and VSTS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="901ce-148">Docker Swarm 및 VSTS를 사용하는 CI/CD</span><span class="sxs-lookup"><span data-stu-id="901ce-148">CI/CD with Docker Swarm and VSTS</span></span>](./container-service-docker-swarm-setup-ci-cd.md)