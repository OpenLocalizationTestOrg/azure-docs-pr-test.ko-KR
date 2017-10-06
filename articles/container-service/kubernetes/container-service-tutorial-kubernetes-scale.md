---
title: "aaaAzure 컨테이너 서비스 자습서-규모의 응용 프로그램 | Microsoft Docs"
description: "Azure Container Service 자습서 - 응용 프로그램 크기 조정"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Kubernetes, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 29571eef0fd91bd6b40f00d8c018539f320179bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-kubernetes-pods-and-kubernetes-infrastructure"></a>Kubernetes Pod 및 Kubernetes 인프라 크기 조정

Hello 자습서 수행 했다면, 하는 경우 작업 Kubernetes 클러스터에 Azure 컨테이너 서비스 있고 hello Azure 투표 앱을 배포 합니다. 

이 자습서에서는, 7 5 부분 hello 포드 hello 응용 프로그램에서 확장 고 pod 자동 크기 조정을 시도 하십시오. 또한 Azure VM 에이전트 노드 toochange tooscale hello 수의 워크 로드를 호스트에 대 한 클러스터의 용량 hello 방법을 알아봅니다. 완료된 작업은 다음과 같습니다.

> [!div class="checklist"]
> * 수동으로 Kubernetes Pod 크기 조정
> * Hello 응용 프로그램에 대 한 프런트 엔드를 실행 하는 자동 크기 조정 포드를 구성 합니다.
> * Hello Kubernetes Azure 에이전트 노드를 확장 합니다.

후속 자습서에서는 hello Azure 투표 응용 프로그램 업데이트 되 고 Operations Management Suite toomonitor hello Kubernetes 클러스터를 구성 합니다.

## <a name="before-you-begin"></a>시작하기 전에

이전 자습서에서 컨테이너 이미지에 패키지 된 응용 프로그램, 컨테이너 레지스트리 tooAzure 및 만들어진 Kubernetes 클러스터가이 이미지를 업로드 합니다. 그런 다음 hello 응용 프로그램 hello Kubernetes 클러스터에서 실행 합니다. 다음이 단계를 수행 하지 않은 toofollow을 따라 하려는 경우 반환 toohello [자습서 1-컨테이너 이미지 만들기](./container-service-tutorial-kubernetes-prepare-app.md)합니다. 

최소한 이 자습서에는 실행 중인 응용 프로그램이 있는 Kubernetes 클러스터가 필요합니다.

## <a name="manually-scale-pods"></a>수동으로 Pod 크기 조정

지금까지 hello Azure 투표 프런트 엔드 및 Redis 인스턴스 배포 됨에 따라 각각 단일 복제본입니다. hello 실행 tooverify [kubectl 가져오기](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) 명령입니다.

```azurecli-interactive
kubectl get pods
```

출력:

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2549686872-4d2r5   1/1       Running   0          31m
azure-vote-front-848767080-tf34m   1/1       Running   0          31m
```

Hello에 포드 hello 수를 수동으로 변경 `azure-vote-front` hello를 사용 하 여 배포 [kubectl 배율](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) 명령입니다. 이 예에서는 숫자 too5 hello 증가합니다.

```azurecli-interactive
kubectl scale --replicas=5 deployment/azure-vote-front
```

실행 [kubectl 가져오기 포드](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify Kubernetes hello 포드를 만드는 것입니다. 1 분 정도 지난 후 hello 추가 포드 실행 중입니다.

```azurecli-interactive
kubectl get pods
```

출력:

```bash
NAME                                READY     STATUS    RESTARTS   AGE
azure-vote-back-2606967446-nmpcf    1/1       Running   0          15m
azure-vote-front-3309479140-2hfh0   1/1       Running   0          3m
azure-vote-front-3309479140-bzt05   1/1       Running   0          3m
azure-vote-front-3309479140-fvcvm   1/1       Running   0          3m
azure-vote-front-3309479140-hrbf2   1/1       Running   0          15m
azure-vote-front-3309479140-qphz8   1/1       Running   0          3m
```

## <a name="autoscale-pods"></a>Pod 자동 크기 조정

Kubernetes 지원 [수평 포드 자동 크기 조정](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) tooadjust hello 수가 포드 CPU 사용률 또는 기타에 따라 배포에서 메트릭을 선택 합니다. 

toouse hello autoscaler CPU 요청 및 제한을 정의 하면 포드 있어야 합니다. Hello에 `azure-vote-front` 배포에서는 프런트 엔드 컨테이너 요청 0.25 CPU 0.5의 제한으로 hello CPU. hello 설정은 다음과 같습니다.

```YAML
resources:
  requests:
     cpu: 250m
  limits:
     cpu: 500m
```

hello 다음 예제에서는 hello [kubectl 자동 크기 조정](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) tooautoscale hello 수가 hello에 포드 명령 `azure-vote-front` 배포 합니다. 여기에서 50%를 초과 하는 CPU 사용률, hello autoscaler hello 포드 tooa 최대를 10 늘리십시오.


```azurecli-interactive
kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10
```

hello 다음 명령을 실행 하는 hello autoscaler toosee hello 상태:

```azurecli-interactive
kubectl get hpa
```

출력:

```bash
NAME               REFERENCE                     TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
azure-vote-front   Deployment/azure-vote-front   0% / 50%   3         10        3          2m
```

Hello Azure 투표 응용 프로그램에 대 한 최소한의 부하를 몇 분 후 hello pod 복제본 수가 too3 자동으로 감소합니다.

## <a name="scale-hello-agents"></a>배율 hello 에이전트

Hello 이전 자습서에서 기본 명령을 사용 하 여 Kubernetes 클러스터를 만든 경우에 세 개의 에이전트 노드에 있습니다. 클러스터에 더 많거나 적은 컨테이너 작업을 계획 하는 경우 에이전트의 hello 수를 수동으로 조정할 수 있습니다. 사용 하 여 hello [az acs 확장](/cli/azure/acs#scale) 명령을 실행 하 고 에이전트의 hello 번호 hello 지정 `--new-agent-count` 매개 변수입니다.

hello 다음 예제에서는 hello 수가 증가 라는 hello Kubernetes 클러스터의 에이전트 노드 too4 *myK8sCluster*합니다. hello 명령 작업은 몇 분 toocomplete입니다.

```azurecli-interactive
az acs scale --resource-group=myResourceGroup --name=myK8SCluster --new-agent-count 4
```

hello 명령 출력 에이전트의 hello 번호에서에서 노드 표시의 hello 값 `agentPoolProfiles:count`:

```azurecli
{
  "agentPoolProfiles": [
    {
      "count": 4,
      "dnsPrefix": "myK8SCluster-myK8SCluster-e44f25-k8s-agents",
      "fqdn": "",
      "name": "agentpools",
      "vmSize": "Standard_D2_v2"
    }
  ],
...

```

## <a name="next-steps"></a>다음 단계

이 자습서에서는 Kubernetes 클러스터의 다양한 크기 조정 기능을 사용했습니다. 설명한 작업은 다음과 같습니다.

> [!div class="checklist"]
> * 수동으로 Kubernetes Pod 크기 조정
> * Hello 응용 프로그램에 대 한 프런트 엔드를 실행 하는 자동 크기 조정 포드를 구성 합니다.
> * Hello Kubernetes Azure 에이전트 노드를 확장 합니다.

Kubernetes에서 응용 프로그램을 업데이트 하는 방법에 대 한 다음 자습서 toolearn toohello를 진행 합니다.

> [!div class="nextstepaction"]
> [Kubernetes에서 응용 프로그램 업데이트](./container-service-tutorial-kubernetes-app-update.md)

