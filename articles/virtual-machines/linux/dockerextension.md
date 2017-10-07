---
title: "aaaUse hello Azure Docker VM 확장 | Microsoft Docs"
description: "Toouse Docker VM 확장 tooquickly hello와 안전 하 게 리소스 관리자 템플릿을 사용 하 여 Azure에서 Docker 환경을 배포 방법과 hello Azure CLI 2.0에 알아봅니다"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 936d67d7-6921-4275-bf11-1e0115e66b7f
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 8e43adc594192773466ccd2d3e455105f14c1a61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension"></a>Hello Docker VM 확장을 사용 하 여 Azure에서 Docker 환경 만들기
Docker는 인기 있는 컨테이너 관리와 이미징 플랫폼 linux 컨테이너와 tooquickly 작업을 허용 하는 합니다. Azure에서 다양 한 방법으로 Docker tooyour 요구에 따라 배포할 수 있습니다. 이 문서에서는 Azure CLI 2.0 hello hello Docker VM 확장 및 Azure 리소스 관리자 템플릿을 사용 합니다. Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](dockerextension-nodejs.md)합니다.

## <a name="azure-docker-vm-extension-overview"></a>Azure Docker VM 확장 개요
hello Azure Docker VM 확장을 설치 하 고 Linux 가상 컴퓨터 (VM)에서 hello Docker 디먼을, Docker 클라이언트 및 Docker Compose를 구성 합니다. Hello Azure Docker VM 확장을 사용 하 여 더 많은 제어 및 기능 보다 간단히 Docker 컴퓨터를 사용 하 여 hello Docker 호스트를 직접 만드는 것이 해야 합니다. 등의 이러한 추가 기능은 [Docker Compose](https://docs.docker.com/compose/overview/), 더욱 강력한 개발자 또는 프로덕션 환경에 적합 한 hello Azure Docker VM 확장을 확인 합니다.

Docker 컴퓨터 및 Azure 컨테이너 서비스를 사용 하는 등 hello 다양 한 배포 방법에 대 한 자세한 내용은 다음 문서는 hello 참조:

* tooquickly 프로토타입 응용 프로그램을 사용 하 여 단일 Docker 호스트를 만들 수 있습니다 [Docker 컴퓨터](docker-machine.md)합니다.
* 배포할 수 있습니다 toobuild 즉시 사용, 확장 가능한 환경 추가 일정 예약 및 관리 도구를 제공 하는 한 [Azure 컨테이너 서비스에서 클러스터 docker는 Docker Swarm](../../container-service/dcos-swarm/container-service-deployment.md)합니다.

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a>Azure Docker VM 확장 hello로 템플릿을 배포합니다
보겠습니다 기존 퀵 스타트 템플릿 toocreate hello Azure Docker VM 확장 tooinstall를 사용 하는 Ubuntu VM을 사용 하 고 hello Docker 호스트를 구성 합니다. 여기에 hello 서식 파일을 볼 수 있습니다: [Docker가 있는 Ubuntu VM의 간단한 배포](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)합니다. 최신 hello 필요한 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 사용 하 여 Azure 계정 tooan [az 로그인](/cli/azure/#login)합니다.

먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다. hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *westus* 위치:

```azurecli
az group create --name myResourceGroup --location westus
```

다음에 사용 하 여 VM을 배포 [az 그룹 배포 만들기](/cli/azure/group/deployment#create) hello Azure Docker VM 확장을 포함 하는 [GitHub에서이 Azure 리소스 관리자 템플릿을](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)합니다. 다음과 같이 *newStorageAccountName*, *adminUsername*, *adminPassword* 및 *dnsNameForPublicIP*에 대한 고유한 값을 제공합니다.

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

배포 toofinish hello에 대 한 몇 가지 분 걸립니다. 응용 프로그램이 완료 되 면 hello 배포 [toonext 단계 이동](#deploy-your-first-nginx-container) tooSSH tooyour VM입니다. 

필요에 따라 hello 추가 tooinstead 반환 컨트롤 toohello 확인 및 let hello 배포 hello 백그라운드에서 계속 `--no-wait` toohello 명령 앞에 플래그를 지정 합니다. 이 프로세스 tooperform 수 있습니다. 몇 분 동안 계속 hello 배포 하는 동안 CLI hello에서 다른 작업입니다. 

와 hello Docker 호스트 상태에 대 한 세부 정보를 볼 수 있습니다 [az vm 표시](/cli/azure/vm#show)합니다. hello 다음 예제에서는 hello의 상태를 검사 hello 라는 VM *myDockerVM* (hello hello 서식 파일에서 기본 이름-이 이름은 변경 하지 않는) 이라는 hello 리소스 그룹에 *myResourceGroup*:

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

이 명령은 반환 하는 경우 *Succeeded*, hello 배포가 완료 되 고 단계 다음에 나오는 hello에 SSH toohello VM을 할 수 있습니다.

## <a name="deploy-your-first-nginx-container"></a>첫 번째 nginx 컨테이너 배포
VM 포함 하 여 hello DNS 이름의 tooview 세부 정보를 사용 하 여 `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`합니다. SSH tooyour 새 Docker 호스트 로컬 컴퓨터에서 다음과 같이:

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

로그인 한 toohello Docker 호스트 nginx 컨테이너를 실행 해 보겠습니다.

```bash
sudo docker run -d -p 80:80 nginx
```

hello 출력은 hello nginx 이미지 다운로드는 다음 예제와 비슷한 toohello 및 시작 하는 컨테이너입니다.

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

다음과 같이 Docker 호스트에서 실행 되는 hello 컨테이너의 hello 상태를 확인 합니다.

```bash
sudo docker ps
```

hello 출력은 다음 예제와 비슷한 toohello, 실행 중 이며 TCP 포트 80 및 443 및 전달 되 고 해당 hello nginx 컨테이너를 보여 주는 있습니다.

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

toosee 컨테이너 작업에서 열 웹 브라우저를 및 Docker 호스트의 hello DNS 이름을 입력 합니다.

![ngnix 컨테이너 실행](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a>Azure Docker VM 확장 템플릿 참조
hello 이전 예제에서는 기존 퀵 스타트 서식 파일을 사용 합니다. 사용자 리소스 관리자 템플릿을 hello Azure Docker VM 확장을 배포할 수도 있습니다. toodo hello tooyour 리소스 관리자 템플릿을 다음, hello 정의 추가, `vmName` vm 적절 하 게 합니다.

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "[concat(variables('vmName'), '/DockerExtension'))]",
  "apiVersion": "2015-05-01-preview",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
  ],
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "DockerExtension",
    "typeHandlerVersion": "1.*",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

Resource Manager 템플릿 사용에 대한 자세한 연습은 [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계
너무 수도[hello Docker 디먼이 TCP 포트 구성](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), 이해 [Docker 보안](https://docs.docker.com/engine/security/security/), 컨테이너를 사용 하 여 배포 또는 [Docker Compose](https://docs.docker.com/compose/overview/)합니다. 자체 Azure Docker VM 확장 hello에 대 한 자세한 내용은 참조 hello [GitHub 프로젝트](https://github.com/Azure/azure-docker-extension/)합니다.

Azure의 hello 추가 Docker 배포 옵션에 대 한 자세한 정보를 읽어 보십시오.

* [Azure 드라이버 hello로 사용 하 여 Docker 컴퓨터](docker-machine.md)  
* [Docker로 시작 하 고 toodefine를 작성 하 고, Azure 가상 컴퓨터에서 여러 컨테이너 응용 프로그램 실행](docker-compose-quickstart.md)합니다.
* [Azure 컨테이너 서비스 클러스터 배포](../../container-service/dcos-swarm/container-service-deployment.md)

