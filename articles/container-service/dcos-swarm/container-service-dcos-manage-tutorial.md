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
# <a name="azure-container-service-tutorial---manage-dcos"></a>Azure Container Service 자습서 - DC/OS 관리

DC/OS는 컨테이너화된 최신 응용 프로그램 실행을 위한 분산 플랫폼을 제공합니다. Azure Container Service를 통해 프로덕션이 준비된 DC/OS 클러스터를 프로비전하는 작업은 간단하고 빠릅니다. 이 빠른 시작 정보 기본 단계는 DC/OS 클러스터와 기본 실행된 작업 toodeploy 필요합니다.

> [!div class="checklist"]
> * ACS DC/OS 클러스터 만들기
> * Toohello 클러스터에 연결
> * Hello DC/OS CLI를 설치 합니다.
> * 응용 프로그램 toohello 클러스터 배포
> * Hello 클러스터에서 응용 프로그램 크기 조정
> * Hello DC/OS 클러스터 노드를 확장 합니다.
> * 기본 DC/OS 관리
> * Hello DC/OS 클러스터를 삭제 합니다.

이 자습서에서는 Azure CLI 버전 2.0.4 hello 이상. 실행 `az --version` toofind hello 버전입니다. Tooupgrade 필요한 경우 참조 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

## <a name="create-dcos-cluster"></a>DC/OS 클러스터 만들기

Hello로 리소스 그룹을 만들려면 먼저 [az 그룹 만들기](/cli/azure/group#create) 명령입니다. Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다. 

hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *westeurope* 위치 합니다.

```azurecli
az group create --name myResourceGroup --location westeurope
```

다음에 DC/OS 클러스터 hello로 만듭니다 [az acs 만들](/cli/azure/acs#create) 명령입니다.

hello 다음 예제에서는 명명 된 DC/OS 클러스터가 *myDCOSCluster* 하 고 존재 하지 않을 경우 SSH 키를 만듭니다. toouse 특정 키의 집합, hello를 사용 하 여 `--ssh-key-value` 옵션입니다.  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

몇 분 후 hello 명령은 완료 되 면 hello 배포에 대 한 정보를 반환 합니다.

## <a name="connect-toodcos-cluster"></a>TooDC/OS 클러스터에 연결

DC/OS 클러스터를 만들면 SSH 터널을 통해 액세스할 수 있습니다. Hello 다음 hello DC/OS 마스터의 명령 tooreturn hello 공용 IP 주소를 실행 합니다. 이 IP 주소 변수에 저장 되 고 hello 다음 단계에서 사용 합니다.

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

toocreate는 SSH 터널 hello, hello 다음 명령을 실행 합니다. 지침을 따릅니다 hello 화면에 표시 합니다. 포트 80 이미 사용 중이면 hello 명령이 실패 합니다. 업데이트 hello와 같은, 사용 중이 아닌 포트 tooone 터널링 된 `85:localhost:80`합니다. 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

## <a name="install-dcos-cli"></a>DC/OS CLI 설치

Hello를 사용 하 여 hello DC/OS cli를 설치 [az acs dcos 설치 cli](/azure/acs/dcos#install-cli) 명령입니다. Azure CloudShell를 사용 하는 hello DC/OS CLI 이미 설치 되었습니다. Hello Azure CLI macOS 또는 Linux를 실행 하는 경우에 sudo 사용 하 여 toorun hello 명령을 할 수 있습니다.

```azurecli
az acs dcos install-cli
```

Hello CLI를 사용 하 여 hello 클러스터 수, 하기 전에 구성 된 toouse hello SSH 터널 해야 합니다. 따라서 toodo 다음 명령을, 필요한 경우 hello 포트 조정 hello를 실행 합니다.

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a>응용 프로그램 실행

hello 예약 메커니즘 ACS DC/OS 클러스터에 대 한 기본값이 마라톤입니다. 풀 마라톤은 응용 프로그램을 사용 하는 toostart 고 hello DC/OS 클러스터에서 hello 응용 프로그램의 hello 상태를 관리 합니다. 풀 마라톤을 통해 응용 프로그램 tooschedule 라는 파일을 만들어 **마라톤 app.json**, 복사 hello를 내용에 따라 합니다. 

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

Hello 명령 tooschedule hello 응용 프로그램 toorun hello DC/OS 클러스터에서 다음을 실행 합니다.

```azurecli
dcos marathon app add marathon-app.json
```

hello 배포 상태를 toosee hello 앱의 경우 hello 다음 명령을 실행 합니다.

```azurecli
dcos marathon app list
```

Hello 때 **작업** 에서 전환 되는 열 값 *0/1* 너무*1/1*, 응용 프로그램 배포가 완료 합니다.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     0/1    ---       ---      False      DOCKER   None
```

## <a name="scale-marathon-application"></a>Marathon 응용 프로그램 크기 조정

Hello 이전 예제에서는 단일 인스턴스 응용 프로그램을 만들었습니다. 이 배포 hello 응용 프로그램의 세 인스턴스를 사용할 수 있도록 개방 hello tooupdate **마라톤 app.json** 파일을 찾아 hello 인스턴스 속성 too3 업데이트 합니다.

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

Hello를 사용 하 여 hello 응용 프로그램 업데이트 `dcos marathon app update` 명령입니다.

```azurecli
dcos marathon app update demo-app-private < marathon-app.json
```

hello 배포 상태를 toosee hello 앱의 경우 hello 다음 명령을 실행 합니다.

```azurecli
dcos marathon app list
```

Hello 때 **작업** 에서 전환 되는 열 값 *1/3* 너무*3/1*, 응용 프로그램 배포가 완료 합니다.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/3    ---       ---      False      DOCKER   None
```

## <a name="run-internet-accessible-app"></a>인터넷에 액세스 가능한 앱 실행

hello ACS DC/OS 클러스터 구성 되어 두 노드 집합에 액세스할 수 있는 공용 인터넷을 hello 및 개인은에 액세스할 수 없는 인터넷 hello 합니다. hello 기본 집합이 hello 개인 노드 hello 마지막 예제에서는 사용 합니다.

toomake 액세스할 수 있는 응용 프로그램, 인터넷 hello toohello 공용 노드 집합을 배포 합니다. toodo, 하 게 hello `acceptedResourceRoles` 개체의 값 `slave_public`합니다.

라는 파일을 만들어 **nginx public.json** 복사 hello를 내용에 따라 합니다.

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

Hello 명령 tooschedule hello 응용 프로그램 toorun hello DC/OS 클러스터에서 다음을 실행 합니다.

```azurecli 
dcos marathon app add nginx-public.json
```

Hello hello DC/OS 공용 클러스터 에이전트의 공용 IP 주소를 가져옵니다.

```azurecli 
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

Hello 기본 NGINX 사이트를 반환 toothis 주소를 검색 합니다.

![NGINX](./media/container-service-dcos-manage-tutorial/nginx.png)

## <a name="scale-dcos-cluster"></a>DC/OS 클러스터 크기 조정

Hello 이전 예제에서 응용 프로그램 크기 조정 된 toomultiple 인스턴스 했습니다. hello DC/OS 인프라 많거나 적은 계산 용량 크기 조정 된 tooprovide 될 수도 있습니다. Hello로 이렇게 [az acs 확장]() 명령입니다. 

hello를 사용 하 여 hello toosee DC/OS 에이전트의 현재 개수 [az acs 표시](/cli/azure/acs#show) 명령입니다.

```azurecli
az acs show --resource-group myResourceGroup --name myDCOSCluster --query "agentPoolProfiles[0].count"
```

tooincrease count too5 hello, hello를 사용 하 여 [az acs 확장](/cli/azure/acs#scale) 명령입니다. 

```azurecli
az acs scale --resource-group myResourceGroup --name myDCOSCluster --new-agent-count 5
```

## <a name="delete-dcos-cluster"></a>DC/OS 클러스터 삭제

더 이상 필요 hello를 사용할 수 없습니다 [az 그룹 삭제](/cli/azure/group#delete) tooremove hello 리소스 그룹, DC/OS 클러스터 및 관련 된 모든 리소스를 명령입니다.

```azurecli 
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a>다음 단계

이 자습서에서는 hello 다음을 비롯 한 기본 DC/OS 관리 작업에 대해 배웠습니다. 

> [!div class="checklist"]
> * ACS DC/OS 클러스터 만들기
> * Toohello 클러스터에 연결
> * Hello DC/OS CLI를 설치 합니다.
> * 응용 프로그램 toohello 클러스터 배포
> * Hello 클러스터에서 응용 프로그램 크기 조정
> * Hello DC/OS 클러스터 노드를 확장 합니다.
> * Hello DC/OS 클러스터를 삭제 합니다.

고급 toohello 다음 자습서 toolearn에 대 한 Azure에서 DC/OS 분산 응용 프로그램을 로드 합니다. 

> [!div class="nextstepaction"]
> [부하 분산 응용 프로그램](container-service-load-balancing.md)