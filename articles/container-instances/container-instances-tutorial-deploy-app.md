---
title: "Azure Container Instances 자습서 - 앱 배포"
description: "Azure Container Instances 자습서 3/3부 - 응용 프로그램 배포"
services: container-instances
author: seanmck
manager: timlt
ms.service: container-instances
ms.topic: tutorial
ms.date: 01/02/2018
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 471caa1b24dc7017c70782c072b2068f9635244b
ms.sourcegitcommit: 85012dbead7879f1f6c2965daa61302eb78bd366
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/02/2018
---
# <a name="deploy-a-container-to-azure-container-instances"></a>Azure Container Instances에 컨테이너 배포

3부작 시리즈의 마지막 자습서입니다. 시리즈의 앞부분에서는 [컨테이너 이미지를 만들어](container-instances-tutorial-prepare-app.md) [Azure Container Registry에 푸시했습니다](container-instances-tutorial-prepare-acr.md). 이 문서에서는 Azure Container Instances에 컨테이너를 배포하여 이 자습서 시리즈를 완료합니다.

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * Azure CLI를 사용하여 Azure Container Registry의 컨테이너 배포
> * 브라우저에서 응용 프로그램 보기
> * 컨테이너 로그 보기

## <a name="before-you-begin"></a>시작하기 전에

이 자습서의 작업을 수행하려면 Azure CLI 버전 2.0.23 이상을 실행해야 합니다. `az --version`을 실행하여 버전을 찾습니다. 설치하거나 업그레이드해야 하는 경우 [Azure CLI 2.0 설치][azure-cli-install]를 참조하세요.

이 자습서를 완료하려면 로컬에 Docker 개발 환경이 설치되어 있어야 합니다. Docker는 모든 [Mac][docker-mac], [Windows][docker-windows] 또는 [Linux][docker-linux] 시스템에서 쉽게 Docker를 구성하는 패키지를 제공합니다.

Azure Cloud Shell에는 이 자습서의 모든 단계를 완료하는 데 필요한 Docker 구성 요소가 포함되어 있지 않습니다. 이 자습서를 완료하려면 로컬 컴퓨터에 Azure CLI 및 Docker 개발 환경을 설치해야 합니다.

## <a name="deploy-the-container-using-the-azure-cli"></a>Azure CLI를 사용하여 컨테이너 배포

Azure CLI를 통해 단일 명령으로 Azure Container Instances에 컨테이너를 배포할 수 있습니다. 컨테이너 이미지가 개인 Azure Container Registry에 호스트되기 때문에 액세스하는 데 필요한 자격 증명을 포함해야 합니다. 다음 Azure CLI 명령을 사용하여 자격 증명을 얻습니다.

컨테이너 레지스트리 로그인 서버(레지스트리 이름을 업데이트):

```azurecli
az acr show --name <acrName> --query loginServer
```

컨테이너 레지스트리 암호:

```azurecli
az acr credential show --name <acrName> --query "passwords[0].value"
```

1개의 CPU 코어 및 1GB 메모리의 리소스를 요청하는 컨테이너 레지스트리에서 컨테이너 이미지를 배포하려면 다음 명령을 실행합니다. `<acrLoginServer>` 및 `<acrPassword>`를 이전 두 개의 명령에서 얻은 값으로 바꿉니다.

```azurecli
az container create --resource-group myResourceGroup --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-password <acrPassword> --ip-address public --ports 80
```

몇 초 정도 지나면 Azure Resource Manager에서 초기 응답이 수신됩니다. 배포 상태를 확인하려면 [az container show][az-container-show] 명령을 사용합니다.

```azurecli
az container show --resource-group myResourceGroup --name aci-tutorial-app --query instanceView.state
```

상태가 *보류 중*에서 *실행 중*으로 변경될 때까지 [az container show][az-container-show] 명령을 1분 미만으로 반복합니다. 컨테이너가 *실행 중* 상태가 되면 다음 단계를 진행합니다.

## <a name="view-the-application-and-container-logs"></a>응용 프로그램 및 컨테이너 로그 보기

배포에 성공하면 [az container show][az-container-show] 명령을 사용하여 컨테이너의 공용 IP 주소를 표시합니다.

```bash
az container show --resource-group myResourceGroup --name aci-tutorial-app --query ipAddress.ip
```

예제 출력: `"13.88.176.27"`

실행 중인 응용 프로그램을 보려면 원하는 브라우저에서 공용 IP 주소로 이동합니다.

![브라우저의 Hello World 앱][aci-app-browser]

또한 컨테이너의 로그 출력을 볼 수 있습니다.

```azurecli
az container logs --resource-group myResourceGroup --name aci-tutorial-app
```

출력

```bash
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://13.88.176.27/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="clean-up-resources"></a>리소스 정리

더 이상 이 자습서 시리즈에서 만든 리소스가 필요하지 않은 경우 [az group delete][az-group-delete] 명령을 실행하여 리소스 그룹 및 여기에 포함된 모든 리소스를 제거할 수 있습니다. 이 명령은 실행 중인 컨테이너뿐만 아니라 생성한 컨테이너 레지스트리 및 모든 관련 리소스를 삭제합니다.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>다음 단계

이 자습서에서는 Azure Container Instances에 컨테이너를 배포하는 프로세스를 완료했습니다. 다음 단계가 완료되었습니다.

> [!div class="checklist"]
> * Azure CLI를 사용하여 Azure Container Registry의 컨테이너 배포
> * 브라우저에서 응용 프로그램 보기
> * 컨테이너 로그 보기

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png

<!-- LINKS - external -->
[docker-linux]: https://docs.docker.com/engine/installation/#supported-platforms
[docker-login]: https://docs.docker.com/engine/reference/commandline/login/
[docker-mac]: https://docs.docker.com/docker-for-mac/
[docker-push]: https://docs.docker.com/engine/reference/commandline/push/
[docker-tag]: https://docs.docker.com/engine/reference/commandline/tag/
[docker-windows]: https://docs.docker.com/docker-for-windows/

<!-- LINKS - internal -->
[az-container-show]: /cli/azure/container#az_container_show
[az-group-delete]: /cli/azure/group#az_group_delete
[azure-cli-install]: /cli/azure/install-azure-cli
[prepare-app]: ./container-instances-tutorial-prepare-app.md