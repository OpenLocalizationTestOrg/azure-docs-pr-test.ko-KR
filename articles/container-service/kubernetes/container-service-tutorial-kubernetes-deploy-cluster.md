---
title: "aaaAzure 컨테이너 서비스 자습서-클러스터 배포 | Microsoft Docs"
description: "Azure Container Service 자습서 - 클러스터 배포"
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
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c4c8cc95c88d9c2077d0322f57e5d3159e2dd0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a>Azure Container Service에서 Kubernetes 클러스터 배포

Kubernetes는 컨테이너화된 응용 프로그램용 분산 플랫폼을 제공합니다. Azure Container Service를 통해 프로덕션이 준비된 Kubernetes 클러스터를 프로비전하는 작업은 간단하고 빠릅니다. 이 자습서(전체 7부 중 3부)에서는 Azure Container Service Kubernetes 클러스터를 배포했습니다. 완료되는 단계는 다음과 같습니다.

> [!div class="checklist"]
> * Kubernetes ACS 클러스터 배포
> * Hello Kubernetes CLI (kubectl) 설치
> * kubectl 구성

후속 자습서에서는 응용 프로그램은 Azure 투표의 배율 조정 toohello 클러스터를 배포 하는 hello 업데이트 하 고 Operations Management Suite가 구성 된 toomonitor hello Kubernetes 클러스터.

## <a name="before-you-begin"></a>시작하기 전에

이전 자습서에서 컨테이너 이미지 생성 하 고 tooan Azure 컨테이너 레지스트리 인스턴스에 업로드 합니다. 다음이 단계를 수행 하지 않은 toofollow을 따라 하려는 경우 너무 반환[자습서 1-컨테이너 이미지 만들기](./container-service-tutorial-kubernetes-prepare-app.md)합니다.

## <a name="create-kubernetes-cluster"></a>Kubernetes 클러스터 만들기

Hello에 [이전 자습서](./container-service-tutorial-kubernetes-prepare-acr.md), 명명 된 리소스 그룹 *myResourceGroup* 만들었습니다. 만들지 않은 경우 지금 이 리소스 그룹을 만듭니다.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

Azure 컨테이너 서비스의 hello Kubernetes 클러스터 만들기 [az acs 만들](/cli/azure/acs#create) 명령입니다. 

hello 다음 예제에서는 명명 된 클러스터가 *myK8sCluster* 와 하나의 Linux 마스터 노드 및 Linux 에이전트 노드를 세 개 있습니다.

```azurecli-interactive 
az acs create --orchestrator-type=kubernetes --resource-group myResourceGroup --name=myK8SCluster --generate-ssh-keys 
```

몇 분 후 hello 명령이 완료 되 면 및 json 반환 서식이 hello ACS 배포에 대 한 정보를 지정 합니다.

## <a name="install-hello-kubectl-cli"></a>Hello kubectl CLI를 설치 합니다.

사용 하 여 클라이언트 컴퓨터에서 tooconnect toohello Kubernetes 클러스터 [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes 명령줄 클라이언트입니다. 

Azure Cloud Shell을 사용하는 경우 `kubectl`이 이미 설치되어 있습니다. Tooinstall 하려는 경우 hello 사용 하 여 로컬로 [az acs kubernetes 설치 cli](/cli/azure/acs/kubernetes#install-cli) 명령입니다.

Linux 또는 macOS에서를 실행 하는 경우에 sudo와 toorun을 할 수 있습니다. Windows에서는 셸이 관리자 권한으로 실행되었는지 확인합니다.

```azurecli-interactive 
az acs kubernetes install-cli 
```

Windows에서는 hello 기본 설치가 *c:\program files (x86)\kubectl.exe*합니다. 이 파일 toohello Windows 경로 tooadd를 할 수 있습니다. 

## <a name="connect-with-kubectl"></a>Kubectl로 연결

tooconfigure `kubectl` hello 실행 tooconnect tooyour Kubernetes 클러스터 [az acs kubernetes get-자격 증명](/cli/azure/acs/kubernetes#get-credentials) 명령입니다.

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8SCluster
```

tooverify hello 연결 tooyour 클러스터 hello 실행 [kubectl 노드 가져오기](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) 명령입니다.

```azurecli-interactive
kubectl get nodes
```

출력:

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.6.2
k8s-agent-98dc3136-1    Ready                      5m        v1.6.2
k8s-agent-98dc3136-2    Ready                      5m        v1.6.2
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.6.2
```

이 자습서를 마치면 ACS Kubernetes 클러스터가 워크로드에 대해 준비됩니다. 후속 자습서에서는 다중 컨테이너 응용 프로그램은 배포 된 toothis 클러스터, 확장, 업데이트 및 모니터링 있습니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 Azure Container Service Kubernetes 클러스터를 배포했습니다. 단계를 수행 하는 hello 완료 되었습니다.

> [!div class="checklist"]
> * Kubernetes ACS 클러스터 배포
> * 설치 된 hello Kubernetes CLI (kubectl)
> * kubectl 구성

Hello 클러스터에서 응용 프로그램을 실행 하는 방법에 대 한 다음 자습서 toolearn toohello를 진행 합니다.

> [!div class="nextstepaction"]
> [Kubernetes에서 응용 프로그램 배포](./container-service-tutorial-kubernetes-deploy-application.md)
