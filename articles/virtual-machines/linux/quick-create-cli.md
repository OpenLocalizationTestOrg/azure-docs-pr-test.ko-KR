---
title: "빠른 시작-aaaAzure VM CLI 만들기 | Microsoft Docs"
description: "Hello Azure CLI로 toocreate 가상 컴퓨터를 신속 하 게 알아봅니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 0d9c686e2f4c7339b29b8c43cd1dd9ee56d7dc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-cli"></a>Hello Azure CLI로 Linux 가상 컴퓨터 만들기

hello Azure CLI 사용된 toocreate 이며 hello 명령줄에서 또는 스크립트에서 Azure 리소스를 관리 합니다. Ubuntu server를 실행 하는 가상 컴퓨터 Azure CLI toodeploy hello를 사용 하 여이 가이드 정보입니다. Hello 서버 배포 되 면 SSH 연결을 만들고 및는 NGINX 웹 서버에 설치 됩니다.

Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

이 퀵 스타트의 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 필요 tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여 이후 버전입니다. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

## <a name="create-a-resource-group"></a>리소스 그룹 만들기

Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다. Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다. 

hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치 합니다.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>가상 컴퓨터 만들기

Hello로 VM을 만들 [az vm 만들기](/cli/azure/vm#create) 명령입니다. 

hello 다음 예제에서는 V *myVM* 하 고 기본 키 위치에 이미 존재 하지 않는 경우 SSH 키를 만듭니다. toouse 특정 키의 집합, hello를 사용 하 여 `--ssh-key-value` 옵션입니다.  

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS --generate-ssh-keys
```

Hello VM을 만든 hello Azure CLI 정보 비슷한 toohello 다음 예제에 표시 됩니다. Hello를 메모해 `publicIpAddress`합니다. 이 주소는 사용 되는 tooaccess hello VM입니다.

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a>웹 트래픽에 대해 포트 80 열기 

기본적으로 Azure에 배포된 Linux 가상 컴퓨터에는 SSH 연결만이 가능합니다. 이 VM은 toobe 웹 서버에서 한 걸음 경우 hello 인터넷에서에서 tooopen 포트 80 해야 합니다. 사용 하 여 hello [az vm-포트를 열](/cli/azure/vm#open-port) 명령 tooopen hello 원하는 포트입니다.  
 
 ```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="ssh-into-your-vm"></a>VM에 SSH 수행

사용 하 여 hello 다음 명령은 toocreate hello 가상 컴퓨터와의 SSH 세션입니다. 있는지 tooreplace 확인  *<publicIpAddress>*  hello로 가상 컴퓨터의 공용 IP 주소를 수정 합니다.  예제에서 IP 주소는 *40.68.254.142*입니다.

```bash 
ssh <publicIpAddress>
```

## <a name="install-nginx"></a>NGINX 설치

사용 하 여 hello 다음 스크립트 tooupdate 패키지 소스를 이용한 적 하 고 hello 최신 NGINX 패키지를 설치 합니다. 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-nginx-welcome-page"></a>Hello NGINX 시작 페이지 보기

설치 NGINX 및 포트 80이 이제 열려 hello-인터넷에서에서 VM에 사용 하 여 선택한 tooview hello 기본 NGINX 시작 페이지의 웹 브라우저를 사용할 수 있습니다. 수 있는지 toouse hello *publicIpAddress* toovisit hello 기본 페이지의 위쪽 문서화 합니다. 

![NGINX 기본 사이트](./media/quick-create-cli/nginx.png) 


## <a name="clean-up-resources"></a>리소스 정리

더 이상 필요 hello를 사용할 수 없습니다 [az 그룹 삭제](/cli/azure/group#delete) tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 명령입니다.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>다음 단계

이 빠른 시작에서 간단한 가상 컴퓨터, 네트워크 보안 그룹 규칙을 배포했으며 웹 서버를 설치했습니다. Azure 가상 컴퓨터에 대해 자세히 toolearn Linux Vm에 대 한 toohello 자습서를 계속 합니다.


> [!div class="nextstepaction"]
> [Azure Linux 가상 컴퓨터 자습서](./tutorial-manage-vm.md)
