---
title: "Azure의 Kubernertes 자습서 - 클러스터 배포"
description: "AKS 자습서 - 클러스터 배포"
services: container-service
author: neilpeterson
manager: timlt
ms.service: container-service
ms.topic: tutorial
ms.date: 11/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 2c2318d9a5f72800f9cfbd430dca448fd1e5746f
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2017
---
# <a name="deploy-an-azure-container-service-aks-cluster"></a>AKS(Azure Container Service) 클러스터 배포

Kubernetes는 컨테이너화된 응용 프로그램용 분산 플랫폼을 제공합니다. AKS를 통해 프로덕션이 준비된 Kubernetes 클러스터를 간단하고 빠르게 프로비저닝할 수 있습니다. 총 8부 중 3부인 이 자습서에서는 Kubernetes 클러스터가 AKS에 배포됩니다. 완료되는 단계는 다음과 같습니다.

> [!div class="checklist"]
> * Kubernetes AKS 클러스터 배포
> * Kubernetes CLI(kubectl) 설치
> * kubectl 구성

후속 자습서에서는 Azure 투표 응용 프로그램을 클러스터에 배포하고 확장/업데이트하며, Kubernetes 클러스터를 모니터링하도록 Operations Management Suite를 구성합니다.

## <a name="before-you-begin"></a>시작하기 전에

이전 자습서에서는 컨테이너 이미지를 만들어 Azure Container Registry 인스턴스에 업로드했습니다. 이러한 단계를 아직 수행하지 않았으나 수행하려는 경우 [자습서 1 - 컨테이너 이미지 만들기][aks-tutorial-prepare-app]로 돌아갑니다.

## <a name="enabling-aks-preview-for-your-azure-subscription"></a>Azure 구독에 AKS 미리 보기 사용
AKS가 미리 보기 상태인 경우 새 클러스터를 만들려면 구독에서 기능 플래그가 필요합니다. 사용하려는 구독의 수에 관계 없이 이 기능을 요청할 수 있습니다. `az provider register` 명령을 사용하여 AKS 공급자를 등록합니다.

```azurecli-interactive
az provider register -n Microsoft.ContainerService
```

등록하면 이제 AKS를 사용하여 Kubernetes 클러스터를 만들 준비가 되었습니다.

## <a name="create-kubernetes-cluster"></a>Kubernetes 클러스터 만들기

다음 예제에서는 `myResourceGroup` 리소스 그룹에 `myK8sCluster` 클러스터를 만듭니다. 이 리소스 그룹은 [이전 자습서][aks-tutorial-prepare-acr]에서 만든 것입니다.

```azurecli
az aks create --resource-group myResourceGroup --name myK8sCluster --node-count 1 --generate-ssh-keys
```

몇 분 후 배포가 완료되고 json 형식의 AKS 배포 관련 정보가 반환됩니다.

## <a name="install-the-kubectl-cli"></a>kubectl CLI 설치

클라이언트 컴퓨터에서 Kubernetes 클러스터에 연결하려면 Kubernetes 명령줄 클라이언트인 [kubectl][kubectl]을 사용합니다.

Azure Cloud Shell을 사용하는 경우 kubectl이 이미 설치되어 있습니다. 로컬로 설치하려면 다음 명령을 실행합니다.

```azurecli
az aks install-cli
```

## <a name="connect-with-kubectl"></a>Kubectl로 연결

Kubernetes 클러스터에 연결하도록 kubectl을 구성하려면 다음 명령을 실행합니다.

```azurecli
az aks get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

클러스터에 대한 연결을 확인하려면 [kubectl get nodes][kubectl-get] 명령을 실행합니다.

```azurecli
kubectl get nodes
```

출력:

```
NAME                          STATUS    AGE       VERSION
k8s-myk8scluster-36346190-0   Ready     49m       v1.7.7
```

이 자습서를 마치면 AKS 클러스터가 워크로드에 대해 준비됩니다. 이후 자습서에서는 다중 컨테이너 응용 프로그램이 이 클러스터에 배포, 규모 확장, 업데이트 및 모니터링됩니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 Kubernetes 클러스터가 AKS에 배포되었습니다. 다음 단계가 완료되었습니다.

> [!div class="checklist"]
> * Kubernetes AKS 클러스터 배포
> * Kubernetes CLI(kubectl) 설치
> * kubectl 구성

다음 자습서로 이동하여 클러스터에서 응용 프로그램 실행에 대해 알아봅니다.

> [!div class="nextstepaction"]
> [Kubernetes에서 응용 프로그램 배포][aks-tutorial-deploy-app]

<!-- LINKS - external -->
[kubectl]: https://kubernetes.io/docs/user-guide/kubectl/
[kubectl-get]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get

<!-- LINKS - internal -->
[aks-tutorial-deploy-app]: ./tutorial-kubernetes-deploy-application.md
[aks-tutorial-prepare-acr]: ./tutorial-kubernetes-prepare-acr.md
[aks-tutorial-prepare-app]: ./tutorial-kubernetes-prepare-app.md