---
title: "Azure DC/OS 클러스터의 aaaLoad 균형 컨테이너 | Microsoft Docs"
description: "Azure Container Service DC/OS 클러스터에 있는 여러 컨테이너에 대해 부하를 분산합니다."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "컨테이너, 마이크로 서비스, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 2249cb06880cdb7e9a3aa94c0750c6a27316d349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a>Azure Container Service DC/OS 클러스터에서 컨테이너 부하 분산
이 문서에서는 toocreate DC/OS에는 내부 부하 분산 장치 풀 마라톤 LB를 사용 하 여 Azure 컨테이너 서비스를 관리 하는 방법을 탐색 합니다. 이 구성을 통해 tooscale 하면 응용 프로그램 가로로 있습니다. 또한 있습니다 tootake 활용을 hello 공용 및 개인 에이전트 클러스터 hello 공용 클러스터와 사용자 응용 프로그램 컨테이너에서 hello 개인 클러스터에 부하 분산을 배치 하 여 합니다. 이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * Marathon Load Balancer 구성
> * Hello 부하 분산 장치를 사용 하 여 응용 프로그램 배포
> * Azure Load Balancer 구성

ACS DC/OS 클러스터 toocomplete hello이이 자습서의 단계를 해야 합니다. 필요한 경우 [이 스크립트 샘플](./../kubernetes/scripts/container-service-cli-deploy-dcos.md)을 사용하여 클러스터를 만들 수 있습니다.

이 자습서에서는 Azure CLI 버전 2.0.4 hello 이상. 실행 `az --version` toofind hello 버전입니다. Tooupgrade 필요한 경우 참조 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a>부하 분산 개요

Azure Container Service DC/OS 클러스터에는 두 개의 부하 분산 계층이 있습니다. 

**Azure 부하 분산 장치** 공용 진입점 (최종 사용자가 해당 항목에 액세스 하는 hello)를 제공 합니다. Azure LB Azure 컨테이너 서비스에 의해 자동으로 제공 되며, 기본적으로 구성 된 tooexpose 포트 80, 443 및 8080 있습니다.

**hello 마라톤 부하 분산 장치 (마라톤 파운드)** 경로 인바운드 요청 toocontainer 이러한 요청을 서비스 인스턴스입니다. 웹 서비스를 제공 하는 hello 컨테이너의 크기를 조정 했습니다 hello 마라톤 lb 동적으로 반응 합니다. 이 부하 분산 장치의 기본 컨테이너 서비스에 의해 제공 되지 않습니다 이지만 쉽게 tooinstall 합니다.

## <a name="configure-marathon-load-balancer"></a>Marathon Load Balancer 구성

부하 분산 장치 풀 마라톤 배포한 hello 컨테이너를 기준으로 자체에 동적으로 재구성 합니다. 이 발생 Apache Mesos hello 컨테이너를 다른 곳에서 다시 시작 하 고 마라톤 lb 조정 탄력적 toohello 손실 컨테이너 또는 에이전트-이기도 합니다.

Hello 명령 tooinstall hello 마라톤 부하 분산 장치 hello 공용 에이전트의 클러스터에서 다음을 실행 합니다.

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a>부하 분산된 응용 프로그램 배포

Hello 마라톤 lb 패키지를 만들었으므로 이제 해당 했는데도 tooload 분산 하는 응용 프로그램 컨테이너를 배포할 수 있습니다. 

먼저, hello를 공개적으로 노출 하는 hello 에이전트의 FQDN을 가져옵니다.

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

다음으로 파일을 만듭니다 *hello web.json* 내용에 따라 hello에 복사 합니다. hello `HAPROXY_0_VHOST` 레이블 toobe hello hello DC/OS 에이전트의 FQDN으로 업데이트 해야 합니다. 

```json
{
  "id": "web",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "yeasy/simple-web",
      "network": "BRIDGE",
      "portMappings": [
        { "hostPort": 0, "containerPort": 80, "servicePort": 10000 }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "labels":{
    "HAPROXY_GROUP":"external",
    "HAPROXY_0_VHOST":"YOUR FQDN",
    "HAPROXY_0_MODE":"http"
  }
}
```

Hello DC/OS CLI toorun hello 응용 프로그램을 사용 합니다. 기본적으로 풀 마라톤 hello toohello 개인 클러스터 hello 응용 프로그램을 배포합니다. 이 즉 배포 위에 hello는 부하 분산 장치를 통해 액세스할 수 있는는 일반적으로 필요한 hello 동작 합니다.

```azurecli-interactive
dcos marathon app add hello-web.json
```

Hello 응용 프로그램을 배포한 후에 toohello FQDN hello 에이전트 클러스터 tooview 부하 분산 된 응용 프로그램을 이동 합니다.

![부하 분산된 응용 프로그램의 이미지](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a>Azure Load Balancer 구성

Azure Load Balancer는 기본적으로 포트 80, 8080 및 443을 노출합니다. 사용 중인 경우이 세 가지 중 하나 (같이 hello 위 예제) 포트를 다음 toodo 필요 없습니다. 수 toohit 있어야 에이전트 부하 분산 장치의 FQDN 및 새로 고칠 때마다 합니다 적중할 라운드 로빈 방식으로 세 개의 웹 서버 중 하나입니다. 

다른 포트를 사용 하는 경우 사용한 hello 포트에 대 한 라운드 로빈 tooadd 규칙 및 hello 부하 분산 장치 프로브 필요 합니다. Hello에서 이렇게 하려면 [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), hello 명령을 사용 하 여 `azure network lb rule create` 및 `azure network lb probe create`합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 hello 마라톤와 Azure 부하 분산 장치 포함 하 여 작업을 다음 hello ACS에서 부하 분산에 대 한 알아보았습니다.

> [!div class="checklist"]
> * Marathon Load Balancer 구성
> * Hello 부하 분산 장치를 사용 하 여 응용 프로그램 배포
> * Azure Load Balancer 구성

Azure에서 DC/OS와 Azure 저장소 통합 하는 방법에 대 한 다음 자습서 toolearn toohello를 진행 합니다.

> [!div class="nextstepaction"]
> [DC/OS 클러스터에 Azure File Share 탑재](container-service-dcos-fileshare.md)