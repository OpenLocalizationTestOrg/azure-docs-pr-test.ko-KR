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
# <a name="deploy-a-dcos-cluster"></a>DC/OS 클러스터 배포

DC/OS는 컨테이너화된 최신 응용 프로그램 실행을 위한 분산 플랫폼을 제공합니다. Azure Container Service를 통해 프로덕션이 준비된 DC/OS 클러스터를 프로비전하는 작업은 간단하고 빠릅니다. 이 빠른 시작 정보는 기본 단계를 hello DC/OS 클러스터와 기본 실행된 작업 toodeploy 필요합니다.

Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.

이 자습서에서는 Azure CLI 버전 2.0.4 hello 이상. 실행 `az --version` toofind hello 버전입니다. Tooupgrade 필요한 경우 참조 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

## <a name="log-in-tooazure"></a>TooAzure 로그인 

Tooyour hello로 Azure 구독에에서 로그인 [az 로그인](/cli/azure/#login) 명령 열고 지시를 따른 hello 화면에 표시 합니다.

```azurecli
az login
```

## <a name="create-a-resource-group"></a>리소스 그룹 만들기

Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다. Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다. 

hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치 합니다.

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-dcos-cluster"></a>DC/OS 클러스터 만들기

DC/OS 클러스터 hello로 만들기 [az acs 만들](/cli/azure/acs#create) 명령입니다.

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

너무 이동 하 여 hello SSH 터널을 테스트할 수 있습니다`http://localhost`합니다. 포트가 80 사용 된 다른 hello 위치 toomatch를 조정 합니다. 

Hello SSH 터널 성공적으로 만들었습니다 hello DC/OS 포털 반환 됩니다.

![DCOS UI](./media/container-service-dcos-quickstart/dcos-ui.png)

## <a name="install-dcos-cli"></a>DC/OS CLI 설치

hello DC/OS 명령줄 인터페이스에 사용 되는 toomanage hello 명령줄에서 DC/OS 클러스터입니다. Hello를 사용 하 여 hello DC/OS cli를 설치 [az acs dcos 설치 cli](/azure/acs/dcos#install-cli) 명령입니다. Azure CloudShell를 사용 하는 hello DC/OS CLI 이미 설치 되었습니다. 

Hello Azure CLI macOS 또는 Linux를 실행 하는 경우에 sudo 사용 하 여 toorun hello 명령을 할 수 있습니다.

```azurecli
az acs dcos install-cli
```

Hello CLI를 사용 하 여 hello 클러스터 수, 하기 전에 구성 된 toouse hello SSH 터널 해야 합니다. 따라서 toodo 다음 명령을, 필요한 경우 hello 포트 조정 hello를 실행 합니다.

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a>응용 프로그램 실행

hello 예약 메커니즘 ACS DC/OS 클러스터에 대 한 기본값이 마라톤입니다. 풀 마라톤은 응용 프로그램을 사용 하는 toostart 고 hello DC/OS 클러스터에서 hello 응용 프로그램의 hello 상태를 관리 합니다. 풀 마라톤을 통해 응용 프로그램 tooschedule 라는 파일을 만들어 *마라톤 app.json*, 복사 hello를 내용에 따라 합니다. 

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
dcos marathon app add marathon-app.json
```

hello 배포 상태를 toosee hello 앱의 경우 hello 다음 명령을 실행 합니다.

```azurecli
dcos marathon app list
```

Hello 때 **대기** 에서 전환 되는 열 값 *True* 너무*False*, 응용 프로그램 배포가 완료 합니다.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/1    ---       ---      False      DOCKER   None
```

Hello hello DC/OS 클러스터 에이전트의 공용 IP 주소를 가져옵니다.

```azurecli
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

Hello 기본 NGINX 사이트를 반환 toothis 주소를 검색 합니다.

![NGINX](./media/container-service-dcos-quickstart/nginx.png)

## <a name="delete-dcos-cluster"></a>DC/OS 클러스터 삭제

더 이상 필요 hello를 사용할 수 없습니다 [az 그룹 삭제](/cli/azure/group#delete) tooremove hello 리소스 그룹, DC/OS 클러스터 및 관련 된 모든 리소스를 명령입니다.

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a>다음 단계

이 빠른 시작에서 DC/OS 클러스터 배포 되었으며을 hello 클러스터에서 간단한 Docker 컨테이너에 실행 합니다. Azure 컨테이너 서비스에 대해 자세히 toolearn toohello ACS 자습서를 계속 합니다.

> [!div class="nextstepaction"]
> [ACS DC/OS 클러스터 관리](container-service-dcos-manage-tutorial.md)