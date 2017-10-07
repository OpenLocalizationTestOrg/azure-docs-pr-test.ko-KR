---
title: "Windows 용 Azure Kubernetes 클러스터 aaaQuickstart-| Microsoft Docs"
description: "신속 하 게 toocreate hello Azure CLI를 사용 하 여 Azure 컨테이너 서비스의 Windows 컨테이너에 대 한 Kubernetes 클러스터에 알아봅니다."
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 85fe65a46ae8c78797e8a8a097c2a37f06329335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-windows-containers"></a>Windows 컨테이너용 Kubernetes 클러스터 배포

hello Azure CLI 사용된 toocreate 이며 hello 명령줄에서 또는 스크립트에서 Azure 리소스를 관리 합니다. Azure CLI toodeploy hello를 사용 하 여이 가이드 정보는 [Kubernetes](https://kubernetes.io/docs/home/) 에 있는 클러스터 [Azure 컨테이너 서비스](../container-service-intro.md)합니다. Hello Kubernetes로 tooit 연결한 hello 클러스터가 배포 되 면 `kubectl` 명령줄 도구를 첫 번째 Windows 컨테이너를 배포 합니다.

Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

이 퀵 스타트의 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 필요 tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여 이후 버전입니다. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

> [!NOTE]
> Azure Container Service에서 Kubernetes의 Windows 컨테이너에 대한 지원은 미리 보기로 제공됩니다. 
>

## <a name="create-a-resource-group"></a>리소스 그룹 만들기

Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다. Azure 리소스 그룹은 Azure 리소스가 배포되고 관리되는 논리 그룹입니다. 

hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치 합니다.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-kubernetes-cluster"></a>Kubernetes 클러스터 만들기
Azure 컨테이너 서비스의 hello Kubernetes 클러스터 만들기 [az acs 만들](/cli/azure/acs#create) 명령입니다. 

hello 다음 예제에서는 명명 된 클러스터가 *myK8sCluster* 한 Linux로 노드와 두 개의 Windows 에이전트 노드를 마스터 합니다. 이 예에서는 SSH 필요한 tooconnect toohello Linux 마스터 키를 만듭니다. 이 예에서는 *azureuser* 관리 사용자 이름에 대 한 및 *myPassword12* hello Windows 노드에서 hello 암호로 합니다. 이러한 값 toosomething 적절 한 tooyour 환경을 업데이트 합니다. 



```azurecli-interactive 
az acs create --orchestrator-type=kubernetes \
    --resource-group myResourceGroup \
    --name=myK8sCluster \
    --agent-count=2 \
    --generate-ssh-keys \
    --windows --admin-username azureuser \
    --admin-password myPassword12
```

몇 분 후 hello 명령, 완료 하 고 배포 하는 방법에 대 한 정보를 보여 줍니다.

## <a name="install-kubectl"></a>kubectl 설치

사용 하 여 클라이언트 컴퓨터에서 tooconnect toohello Kubernetes 클러스터 [ `kubectl` ](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes 명령줄 클라이언트입니다. 

Azure Cloud Shell을 사용하는 경우 `kubectl`이 이미 설치되어 있습니다. Tooinstall 하려는 경우 로컬로 있습니다 사용할 수 있습니다 hello [az acs kubernetes 설치 cli](/cli/azure/acs/kubernetes#install-cli) 명령입니다.

다음 Azure CLI 예제 설치 hello `kubectl` tooyour 시스템입니다. Windows에서 이 명령을 관리자 권한으로 실행합니다.

```azurecli-interactive 
az acs kubernetes install-cli
```


## <a name="connect-with-kubectl"></a>Kubectl로 연결

tooconfigure `kubectl` hello 실행 tooconnect tooyour Kubernetes 클러스터 [az acs kubernetes get-자격 증명](/cli/azure/acs/kubernetes#get-credentials) 명령입니다. hello 다음 예제에서는 다운로드 Kubernetes 클러스터에 대 한 hello 클러스터 구성.

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

tooverify hello 연결 tooyour에서에서 클러스터 컴퓨터를 실행 해 보십시오.

```azurecli-interactive
kubectl get nodes
```

`kubectl`hello 마스터 및 에이전트 노드를 나열합니다.

```azurecli-interactive
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.5.3
k8s-agent-98dc3136-1    Ready                      5m        v1.5.3
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.5.3

```

## <a name="deploy-a-windows-iis-container"></a>Windows IIS 컨테이너 배포

하나 이상의 컨테이너가 포함된 Kubernetes *Pod* 내부에서 Docker 컨테이너를 실행할 수 있습니다. 

기본 예제에서는 JSON 파일 toospecify Microsoft 인터넷 정보 서버 (IIS) 컨테이너를 사용 하 여 만들고 다음 hello를 사용 하 여 hello pod `kubctl apply` 명령입니다. 

라는 로컬 파일을 만들어 `iis.json` 복사 hello 텍스트에 따라 합니다. 이 파일을 통해 알 Kubernetes toorun IIS에서 Windows Server 2016 Nano 서버에서 공용 컨테이너 이미지를 사용 하 여 [Docker 허브](https://hub.docker.com/r/nanoserver/iis/)합니다. hello 컨테이너 포트 80을 사용 하 여 이지만 처음에 불과합니다 hello 클러스터 네트워크 내에서 액세스할 수 있습니다.

 ```JSON
 {
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "iis",
    "labels": {
      "name": "iis"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "iis",
        "image": "nanoserver/iis",
        "ports": [
          {
          "containerPort": 80
          }
        ]
      }
    ],
    "nodeSelector": {
     "beta.kubernetes.io/os": "windows"
     }
   }
 }
 ```

toostart hello pod, 유형:
  
```azurecli-interactive
kubectl apply -f iis.json
```  

형식 tootrack hello 배포:
  
```azurecli-interactive
kubectl get pods
```

Hello 상태는 hello 포드를 배포 하는 동안 `ContainerCreating`합니다. Hello 컨테이너 tooenter hello에 대 일 분이 지나야 `Running` 상태입니다.

```azurecli-interactive
NAME     READY        STATUS        RESTARTS    AGE
iis      1/1          Running       0           32s
```

## <a name="view-hello-iis-welcome-page"></a>보기 hello IIS 시작 페이지

tooexpose hello pod toohello world 공용 IP 주소, 다음 명령을 형식 hello:

```azurecli-interactive
kubectl expose pods iis --port=80 --type=LoadBalancer
```

Kubernetes이이 명령을 사용 하 여 서비스를 만듭니다와 [Azure 부하 분산 장치 규칙](container-service-kubernetes-load-balancing.md) hello 서비스에 대 한 공용 IP 주소를 사용 합니다. 

Hello hello 서비스의 명령 toosee hello 상태를 다음을 실행 합니다.

```azurecli-interactive
kubectl get svc
```

으로 hello IP 주소가 표시 되는 처음 `pending`합니다. 몇 분 후 hello의 외부 IP 주소를 hello `iis` pod 설정 됩니다.
  
```azurecli-interactive
NAME         CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE       
kubernetes   10.0.0.1       <none>          443/TCP        21h       
iis          10.0.111.25    13.64.158.233   80/TCP         22m
```

Hello 외부 IP 주소에서 choice toosee hello 기본 IIS 시작 페이지의 웹 브라우저를 사용할 수 있습니다.

![TooIIS 검색 이미지](./media/container-service-kubernetes-windows-walkthrough/kubernetes-iis.png)  


## <a name="delete-cluster"></a>클러스터 삭제
Hello hello 클러스터 필요는 더 이상 사용할 수 없습니다 [az 그룹 삭제](/cli/azure/group#delete) tooremove hello 리소스 그룹, 컨테이너 서비스와 관련 된 모든 리소스를 명령입니다.

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a>다음 단계

이 빠른 시작에서는 Kubernetes 클러스터를 배포하고, `kubectl`로 연결하고, IIS 컨테이너가 있는 Pod를 배포했습니다. Azure 컨테이너 서비스에 대해 자세히 toolearn toohello Kubernetes 자습서를 계속 합니다.

> [!div class="nextstepaction"]
> [ACS Kubernetes 클러스터 관리](container-service-tutorial-kubernetes-prepare-app.md)
