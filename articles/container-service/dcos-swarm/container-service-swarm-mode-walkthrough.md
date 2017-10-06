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
# <a name="deploy-docker-ce-cluster"></a>Docker CE 클러스터 배포

이 빠른 시작에서는 Docker CE 클러스터 hello Azure CLI를 사용 하 여 배포 됩니다. 그런 다음 웹 프런트 엔드 및 Redis 인스턴스로 구성 된 다중 컨테이너 응용 프로그램 배포 하 고 hello 클러스터에서 실행 됩니다. Hello 응용 프로그램을 통해 액세스할 수는 완료 되 면 인터넷 hello 합니다.

Azure Container Service에서 Docker CE는 미리 보기 상태이며 **프로덕션 워크로드에는 사용할 수 없습니다**.

Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.

이 퀵 스타트의 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 필요 tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여 이후 버전입니다. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.

## <a name="create-a-resource-group"></a>리소스 그룹 만들기

Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다. Azure 리소스 그룹은 Azure 리소스가 배포되고 관리되는 논리 그룹입니다.

hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *ukwest* 위치 합니다.

```azurecli-interactive
az group create --name myResourceGroup --location ukwest
```

출력:

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

## <a name="create-docker-swarm-cluster"></a>Docker Swarm 클러스터 만들기

Hello로 Azure 컨테이너 서비스의 Docker CE 클러스터 만들기 [az acs 만들](/cli/azure/acs#create) 명령입니다. 

hello 다음 예제에서는 명명 된 클러스터가 *mySwarmCluster* 와 하나의 Linux 마스터 노드 및 Linux 에이전트 노드를 세 개 있습니다.

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type dockerce --resource-group myResourceGroup --generate-ssh-keys
```

몇 분 후 hello 명령을 완료 하 고 hello 클러스터에 대 한 json 형식 정보를 반환 합니다.

## <a name="connect-toohello-cluster"></a>Toohello 클러스터에 연결

이 빠른 시작 전체에서 hello FQDN hello docker는 Docker Swarm 마스터와 hello Docker 에이전트 풀을 해야합니다. 다음 명령을 tooreturn 둘 다 hello 마스터 및 에이전트 Fqdn hello를 실행 합니다.


```bash
az acs list --resource-group myResourceGroup --query '[*].{Master:masterProfile.fqdn,Agent:agentPoolProfiles[0].fqdn}' -o table
```

출력:

```bash
Master                                                               Agent
-------------------------------------------------------------------  --------------------------------------------------------------------
myswarmcluster-myresourcegroup-d5b9d4mgmt.ukwest.cloudapp.azure.com  myswarmcluster-myresourcegroup-d5b9d4agent.ukwest.cloudapp.azure.com
```

SSH 터널 toohello 웜 마스터를 만듭니다. 대체 `MasterFQDN` hello 웜 마스터의 hello FQDN 주소를 사용 합니다.

```bash
ssh -p 2200 -fNL localhost:2374:/var/run/docker.sock azureuser@MasterFQDN
```

집합 hello `DOCKER_HOST` 환경 변수입니다. 이렇게 하면 있습니다 docker는 Docker Swarm hello에 대해 toorun docker 명령을 hello 호스트의 toospecify hello 이름이 필요 없이.

```bash
export DOCKER_HOST=localhost:2374
```

Docker는 Docker Swarm hello에서 준비 toorun Docker 서비스입니다.


## <a name="run-hello-application"></a>Hello 응용 프로그램 실행

라는 파일을 만들어 `azure-vote.yaml` 고 복사 hello에 콘텐츠를 따릅니다.


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

Hello 실행 [docker 스택 배포](https://docs.docker.com/engine/reference/commandline/stack_deploy/) toocreate hello Azure 투표 서비스 명령입니다.

```bash
docker stack deploy azure-vote --compose-file azure-vote.yaml
```

출력:

```bash
Creating network azure-vote_default
Creating service azure-vote_azure-vote-back
Creating service azure-vote_azure-vote-front
```

사용 하 여 hello [docker 스택 ps](https://docs.docker.com/engine/reference/commandline/stack_ps/) tooreturn hello 응용 프로그램의 배포 상태를 hello 명령입니다.

```bash
docker stack ps azure-vote
```

한 번 hello `CURRENT STATE` 의 각 서비스는 `Running`, hello 응용 프로그램을 준비 합니다.

```bash
ID                  NAME                            IMAGE                                 NODE                               DESIRED STATE       CURRENT STATE                ERROR               PORTS
tnklkv3ogu3i        azure-vote_azure-vote-front.1   microsoft/azure-vote-front:redis-v1   swarmm-agentpool0-66066781000004   Running             Running 5 seconds ago                            
lg99i4hy68r9        azure-vote_azure-vote-back.1    redis:latest                          swarmm-agentpool0-66066781000002   Running             Running about a minute ago
```

## <a name="test-hello-application"></a>Hello 응용 프로그램 테스트

Toohello hello 웜 에이전트 풀 tootest hello Azure 투표 응용 프로그램으로의 FQDN을 찾습니다.

![투표 tooAzure 검색 이미지](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a>클러스터 삭제
Hello hello 클러스터 필요는 더 이상 사용할 수 없습니다 [az 그룹 삭제](/cli/azure/group#delete) tooremove hello 리소스 그룹, 컨테이너 서비스와 관련 된 모든 리소스를 명령입니다.

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a>Hello 코드 가져오기

이 빠른 시작에서 미리 생성된 된 컨테이너 이미지 Docker 서비스가 사용 되는 toocreate 되었습니다. hello 관련 응용 프로그램 코드에서 Dockerfile 되며 Compose 파일 GitHub에서 사용할 수 있습니다.

[https://github.com/Azure-Samples/azure-voting-app-redis](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a>다음 단계

이 빠른 시작에서 docker는 Docker Swarm 클러스터를 배포 및 다중 컨테이너 응용 프로그램 tooit를 배포 합니다.

Docker 웜 Visual Studio Team Services와 통합 하는 방법에 대 한 toolearn toohello docker는 Docker Swarm 및 VSTS CI/CD를 계속 합니다.

> [!div class="nextstepaction"]
> [Docker Swarm 및 VSTS를 사용하는 CI/CD](./container-service-docker-swarm-setup-ci-cd.md)