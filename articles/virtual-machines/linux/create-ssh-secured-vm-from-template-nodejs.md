---
title: "Azure 템플릿 Azure CLI 1.0과 함께 사용 하 여 Linux VM aaaCreate | Microsoft Docs"
description: "Hello Azure CLI 1.0 및 Azure 리소스 관리자 템플릿을 사용 하 여 Azure에서 Linux VM을 만듭니다."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: v-livech
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b694cc8247a8431b7ef4b24cc7dc2b4cdb9660ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-vm-using-hello-azure-cli-10-an-azure-resource-manager-template"></a>어떻게 사용 하 여 Linux VM a toocreate hello Azure CLI 1.0 Azure 리소스 관리자 템플릿
이 문서에서는 tooquickly hello Azure CLI 1.0 및 Azure 리소스 관리자 템플릿을 사용 하 여 Linux 가상 컴퓨터를 배포 하는 방법을 보여 줍니다. hello 문서에는 다음 사항이 필요합니다.

* Azure 계정([무료 평가판 받기](https://azure.microsoft.com/pricing/free-trial/))
* hello [Azure CLI 1.0](../../cli-install-nodejs.md) 로그인 한 `azure login`합니다.
* hello Azure CLI *에 있어야* Azure Resource Manager 모드 `azure config mode arm`합니다.

Hello를 사용 하 여 Linux VM 템플릿을 신속 하 게 배포할 수 있습니다 [Azure 포털](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 버전 toocomplete hello 작업
Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.

- [Azure CLI 1.0](#quick-command-summary) – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)
- [Azure CLI 2.0](create-ssh-secured-vm-from-template.md) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한

## <a name="quick-command-summary"></a>빠른 명령 요약
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a>자세한 연습
템플릿을 사용 하면 toocreate Vm Azure의 hello 시작, 같은 사용자 이름 및 호스트 이름을 설정 하는 동안 toocustomize 되도록 설정 합니다. 이 문서의 경우 SSH에 오픈된 포트 22를 포함한 NSG(네트워크 보안 그룹)와 함께 Ubuntu VM을 활용하여 Azure 템플릿을 시작합니다.

Azure Resource Manager 템플릿은 이 문서에서와 같이 Ubuntu VM을 시작하는 등 간단한 일회성 작업에 사용할 수 있는 JSON 파일입니다.  Azure 템플릿 전체 환경 테스트, 개발, 또는 프로덕션 배포 스택 처럼 사용 되는 tooconstruct 복잡 한 Azure 구성 될 수도 있습니다.

## <a name="create-hello-linux-vm"></a>Hello Linux VM 만들기
코드 예제에서 보여 주는 방법을 다음 hello toocall `azure group create` toocreate 리소스 그룹화 하 고 hello에는 SSH 보안 Linux VM을 배포할 사용 하 여 동일한 시간 [이 Azure 리소스 관리자 템플릿을](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json)합니다. 고유한 tooyour 환경 있는 toouse 이름이 필요한 예에서 유의 해야 합니다. 이 예에서는 *myResourceGroup* hello 리소스 그룹 이름으로 및 *myVM* hello VM 이름으로 합니다.

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

hello 출력은 출력 블록 뒤 hello 같이 표시 됩니다.

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for hello following parameters
sshKeyData: ssh-rsa AAAAB3Nza<..ssh public key text..>VQgwjNjQ== myAdminUser@myVM
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/<..subid text..>/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

그 예에서 hello를 사용 하는 VM 배포 `--template-uri` 매개 변수입니다.  또한 또는 로컬로 템플릿을 만드는 있으며 hello를 사용 하 여 hello 템플릿을 전달 `--template-file` 매개 변수를 인수로 경로 toohello 템플릿 파일을 사용 합니다. hello Azure CLI 매개 변수를 hello hello 템플릿에 필요 합니다.

## <a name="next-steps"></a>다음 단계
검색 hello [템플릿 갤러리](https://azure.microsoft.com/documentation/templates/) toodiscover 어떤 응용 프로그램 프레임 워크 toodeploy 다음 합니다.

