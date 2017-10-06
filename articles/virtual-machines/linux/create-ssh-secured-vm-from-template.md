---
title: "Azure에서 Linux VM 템플릿에서 aaaCreate | Microsoft Docs"
description: "어떻게 toouse hello Azure CLI 2.0 toocreate 리소스 관리자 템플릿으로 Linux VM"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 721b8378-9e47-411e-842c-ec3276d3256a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f4b8c4103cccbae13c679ff2a2cac928a0e8e809
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-with-azure-resource-manager-templates"></a>어떻게 toocreate Azure 리소스 관리자 템플릿으로 Linux 가상 컴퓨터
이 문서에서는 tooquickly hello Azure CLI 2.0 및 Azure 리소스 관리자 템플릿을 사용 하 여 Linux 가상 컴퓨터 (VM)를 배포 하는 방법을 보여 줍니다. Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md)합니다.


## <a name="templates-overview"></a>템플릿 개요
Azure 리소스 관리자 템플릿은 hello 인프라 및 Azure 솔루션의 구성을 정의 하는 JSON 파일입니다. 템플릿을 사용하여 수명 주기 내내 솔루션을 반복적으로 배포하고 안심하고 일관된 상태로 리소스를 배포할 수 있습니다. hello 형식의 hello 템플릿과 작성 하는 방법에 대해 자세히 toolearn 참조 [첫 번째 Azure 리소스 관리자 서식 파일 만들기](../../azure-resource-manager/resource-manager-create-first-template.md)합니다. tooview hello 리소스 형식에 대 한 JSON 구문을 참조 [Azure 리소스 관리자 템플릿을에 리소스를 정의](/azure/templates/)합니다.


## <a name="create-resource-group"></a>리소스 그룹 만들기
Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다. 가상 컴퓨터보다 먼저 리소스 그룹을 만들어야 합니다. hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroupVM* hello에 *eastus* 영역:

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>가상 컴퓨터 만들기
hello 다음 예제에서는에서 VM [이 Azure 리소스 관리자 템플릿을](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) 와 [az 그룹 배포 만들기](/cli/azure/group/deployment#create)합니다. 사용자 고유의 SSH 공개 키를 hello 내용의 등의 hello 값을 제공 *~/.ssh/id_rsa.pub*합니다. SSH 키 쌍 toocreate 필요한 경우 참조 [어떻게 toocreate 및 사용 된 SSH 키 쌍 Azure에서 Linux Vm에 대 한](mac-create-ssh-keys.md)합니다.

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

이 예제에서는 GitHub에 저장된 템플릿을 지정했습니다. 있습니다 수 또한 다운로드 또는 템플릿을 만들고 hello로 hello 로컬 경로 지정 합니다. 동일한 `--template-file` 매개 변수입니다.

tooSSH tooyour VM을 hello와 공용 IP 주소를 가져올 [az 네트워크 공개 ip 표시](/cli/azure/network/public-ip#show):

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

그런 다음 SSH tooyour VM 정상적으로 수행할 수 있습니다.

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a>다음 단계
이 예제에서는 기본 Linux VM을 만들었습니다. 응용 프로그램 프레임 워크를 포함 하거나 더 복잡 한 환경을 만들 수 있는 더 많은 리소스 관리자 템플릿에 대 한 찾아보기 hello [Azure 빠른 시작 템플릿 갤러리](https://azure.microsoft.com/documentation/templates/)합니다.
