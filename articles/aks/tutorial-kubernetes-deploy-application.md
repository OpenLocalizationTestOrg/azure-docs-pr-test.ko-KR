---
title: "Azure의 Kubernertes 자습서 - 응용 프로그램 배포"
description: "AKS 자습서 - 응용 프로그램 배포"
services: container-service
author: neilpeterson
manager: timlt
ms.service: container-service
ms.topic: tutorial
ms.date: 10/24/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 4468424a96b4949161218d495dd21f24285430fd
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/18/2017
---
# <a name="run-applications-in-azure-container-service-aks"></a>AKS(Azure Container Service)에서 응용 프로그램 실행

총 8부 중 4부인 이 자습서에서는 응용 프로그램 예제를 Kubernetes 클러스터에 배포합니다. 완료되는 단계는 다음과 같습니다.

> [!div class="checklist"]
> * Kubernetes 매니페스트 파일 업데이트
> * Kubernetes에서 응용 프로그램 실행
> * 응용 프로그램 테스트

후속 자습서에서는 이 응용 프로그램을 스케일 아웃하고 업데이트하며, Kubernetes 클러스터를 모니터링하도록 Operations Management Suite를 구성합니다.

이 자습서에서는 Kubernetes 개념에 대한 기본적인 이해가 있다고 가정하며 Kubernetes에 대한 자세한 내용은 [Kubernetes 설명서][kubernetes-documentation]를 참조하세요.

## <a name="before-you-begin"></a>시작하기 전에

이전 자습서에서는 응용 프로그램을 컨테이너 이미지에 패키지하고, Azure Container Registry에 이러한 이미지를 업로드하고, Kubernetes 클러스터를 만들었습니다. 

이 자습서를 완료하려면 미리 작성된 `azure-vote-all-in-one-redis.yaml` Kubernetes 매니페스트 파일이 필요합니다. 이전 자습서에서 응용 프로그램 소스 코드와 함께 이 파일을 다운로드했습니다. 리포지토리를 복제했으며 디렉터리를 복제된 리포지토리로 변경했는지 확인하세요.

이러한 단계를 아직 수행하지 않았으나 수행하려는 경우 [자습서 1 - 컨테이너 이미지 만들기][aks-tutorial-prepare-app]로 돌아갑니다.

## <a name="update-manifest-file"></a>매니페스트 파일 업데이트

이 자습서에서는 ACR(Azure Container Registry)을 사용하여 컨테이너 이미지를 저장했습니다. 응용 프로그램을 실행하기 전에 Kubernetes 매니페스트 파일에서 ACR 로그인 서버 이름을 업데이트해야 합니다.

[az acr list][az-acr-list] 명령을 사용하여 ACR 로그인 서버 이름을 가져옵니다.

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

매니페스트 파일은 로그인 서버 이름 `microsoft`를 사용하여 미리 작성되었습니다. 원하는 텍스트 편집기에서 파일을 엽니다. 이 예제에서는 `vi`를 사용하여 파일을 엽니다.

```console
vi azure-vote-all-in-one-redis.yaml
```

`microsoft`는 ACR 로그인 서버 이름으로 바꿉니다. 이 값은 매니페스트 파일의 줄 **47**에 있습니다.

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

파일을 저장하고 닫습니다.

## <a name="deploy-application"></a>응용 프로그램 배포

응용 프로그램을 실행하려면 [kubectl create][kubectl-create] 명령을 사용합니다. 이 명령은 매니페스트 파일을 구문 분석하고 정의된 Kubernetes 개체를 만듭니다.

```azurecli
kubectl create -f azure-vote-all-in-one-redis.yaml
```

출력

```
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a>응용 프로그램 테스트

인터넷에 응용 프로그램을 노출하는 [Kubernetes 서비스][kubernetes-service]가 생성됩니다. 이 프로세스는 몇 분 정도 걸릴 수 있습니다. 

진행 상황을 모니터링하려면 `--watch` 인수와 함께 [kubectl get service][kubectl-get] 명령을 사용합니다.

```azurecli
kubectl get service azure-vote-front --watch
```

처음에는 *azure-vote-front* 서비스에 대한 *EXTERNAL-IP*가 *보류 중*으로 표시됩니다.
  
```
azure-vote-front   10.0.34.242   <pending>     80:30676/TCP   7s
```

*EXTERNAL-IP* 주소가 *보류 중*에서 *IP 주소*로 변경되면 `CTRL-C`를 사용하여 kubectl 조사식 프로세스를 중지합니다. 

```
azure-vote-front   10.0.34.242   52.179.23.131   80:30676/TCP   2m
```

응용 프로그램을 보려면 외부 IP 주소로 이동합니다.

![Azure의 Kubernetes 클러스터 이미지](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a>다음 단계

이 자습서에서는 Azure Vote 응용 프로그램이 AKS의 Kubernetes 클러스터에 배포되었습니다. 완료된 작업은 다음과 같습니다.  

> [!div class="checklist"]
> * Kubernetes 매니페스트 파일 다운로드
> * Kubernetes에서 응용 프로그램 실행
> * 응용 프로그램 테스트

다음 자습서로 이동하여 Kubernetes 응용 프로그램과 기본 Kubernetes 인프라를 모두 크기 조정하는 방법에 대해 알아봅니다. 

> [!div class="nextstepaction"]
> [Kubernetes 응용 프로그램 및 인프라 크기 조정][aks-tutorial-scale]

<!-- LINKS - external -->
[kubectl-create]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create
[kubectl-get]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get
[kubernetes-documentation]: https://kubernetes.io/docs/home/
[kubernetes-service]: https://kubernetes.io/docs/concepts/services-networking/service/

<!-- LINKS - internal -->
[aks-tutorial-prepare-app]: ./tutorial-kubernetes-prepare-app.md
[aks-tutorial-scale]: ./tutorial-kubernetes-scale.md
[az-acr-list]: /cli/azure/acr#list
