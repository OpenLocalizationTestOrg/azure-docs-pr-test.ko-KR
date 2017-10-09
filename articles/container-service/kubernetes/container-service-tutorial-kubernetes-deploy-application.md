---
title: "aaaAzure 컨테이너 서비스 자습서-응용 프로그램 배포 | Microsoft Docs"
description: "Azure Container Service 자습서 - 응용 프로그램 배포"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7e2fa06d359caf83e684df3966624a6e9a8e7efa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-applications-in-kubernetes"></a>Kubernetes에서 응용 프로그램 실행

7개 중 4단계인 이 자습서에서는 응용 프로그램 예제를 Kubernetes 클러스터에 배포합니다. 완료되는 단계는 다음과 같습니다.

> [!div class="checklist"]
> * Kubernetes 매니페스트 파일 다운로드
> * Kubernetes에서 응용 프로그램 실행
> * Hello 응용 프로그램 테스트

이후 자습서에서이 응용 프로그램은 확장 업데이트 하 고 Operations Management Suite toomonitor hello Kubernetes 클러스터 구성.

이 자습서에 Kubernetes 개념에 대 한 기본 지식이 있다고 가정, 참조 hello에 대 한 자세한 내용은 Kubernetes [Kubernetes 설명서](https://kubernetes.io/docs/home/)합니다.

## <a name="before-you-begin"></a>시작하기 전에

이전 자습서에서 컨테이너 이미지에 패키지 된 응용 프로그램 하 고이 이미지는 업로드 컨테이너 레지스트리 tooAzure Kubernetes 클러스터를 만들 합니다. 다음이 단계를 수행 하지 않은 toofollow을 따라 하려는 경우 너무 반환[자습서 1-컨테이너 이미지 만들기](./container-service-tutorial-kubernetes-prepare-app.md)합니다. 

최소한 이 자습서에는 Kubernetes 클러스터가 필요합니다.

## <a name="get-manifest-file"></a>매니페스트 파일 가져오기

이 자습서에서는 Kubernetes 매니페스트를 사용하여 [Kubernetes 개체](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/)를 배포합니다. Kubernetes 매니페스트는 Kubernetes 개체 배포 및 구성 지침이 포함된 YAML 또는 JSON 형식이 지정된 파일입니다.

이 자습서에 대 한 hello 응용 프로그램 매니페스트 파일은 이전 자습서에서 복제 된 hello Azure 투표 응용 프로그램 리포지토리를 제공 됩니다. 이미 수행 하는 경우 다음 명령을 hello로 hello 리포지토리를 복제: 

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

hello 매니페스트 파일은 복제 hello 리포지토리의 디렉터리를 다음 hello 있습니다.

```bash
/azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

## <a name="update-manifest-file"></a>매니페스트 파일 업데이트

Azure 컨테이너 레지스트리 toostore hello 컨테이너 이미지를 사용 하는 경우 hello 매니페스트 요구 toobe hello ACR loginServer 이름으로 업데이트 합니다.

Hello로 hello ACR 로그인 서버 이름을 가져오는 [az acr 목록](/cli/azure/acr#list) 명령입니다.

```azurecli-interactive
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

hello 샘플 매니페스트 미리 만들었습니다 리포지토리 이름이 *microsoft*합니다. 임의의 텍스트 편집기로 hello 파일을 열고 및 hello 바꾸기 *microsoft* hello ACR 인스턴스 로그인 서버 이름 사용 하 여 값입니다.

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

## <a name="deploy-application"></a>응용 프로그램 배포

사용 하 여 hello [kubectl 만들](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) toorun hello 응용 프로그램 명령입니다. 이 명령 구문 분석 하 여 hello 매니페스트 파일을 정의 된 hello Kubernetes 개체를 만듭니다.

```azurecli-interactive
kubectl create -f ./azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

출력:

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a>응용 프로그램 테스트

A [Kubernetes 서비스](https://kubernetes.io/docs/concepts/services-networking/service/) hello 응용 프로그램 toohello를 노출 하는 만들어집니다 인터넷 합니다. 이 프로세스는 몇 분 정도 걸릴 수 있습니다. 

toomonitor 진행 상황을 사용 하 여 hello [kubectl 서비스를 가져올](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) hello로 명령을 `--watch` 인수입니다.

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

처음에 hello **외부 IP** hello에 대 한 *azure 투표 프런트* 으로 서비스 나타납니다 *보류 중인*합니다. hello 외부 IP 주소가 변경 되 면 *보류 중인* tooan *IP 주소*를 사용 하 여 `CTRL-C` toostop hello kubectl 조사식 프로세스입니다.

```bash
NAME               CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   10.0.42.158   <pending>     80:31873/TCP   1m
azure-vote-front   10.0.42.158   52.179.23.131 80:31873/TCP   2m
```

toosee hello 응용 프로그램, 찾아보기 toohello 외부 IP 주소입니다.

![Azure의 Kubernetes 클러스터 이미지](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a>다음 단계

이 자습서에서는 Azure 투표 응용 프로그램 hello tooan 배포 된 Azure 컨테이너 서비스 Kubernetes 클러스터 했습니다. 완료된 작업은 다음과 같습니다.  

> [!div class="checklist"]
> * Kubernetes 매니페스트 파일 다운로드
> * Kubernetes에 hello 응용 프로그램을 실행 합니다.
> * 테스트 된 hello 응용 프로그램

Kubernetes 응용 프로그램과 hello Kubernetes 인프라 내부 크기 조정 하는 방법에 대 한 다음 자습서 toolearn toohello를 진행 합니다. 

> [!div class="nextstepaction"]
> [Kubernetes 응용 프로그램 및 인프라 크기 조정](./container-service-tutorial-kubernetes-scale.md)