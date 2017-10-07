---
title: "Azure에서 Linux VM aaaDifferent 방법 toocreate | Microsoft Azure"
description: "Hello 다양 한 방법 toocreate 링크 tootools 등 각 방법에 대 한 자습서는 Azure에서 Linux 가상 컴퓨터에 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 250e92c063c87a8c1279097dc2264777d95478d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-linux-vm"></a>다양 한 방법 toocreate Linux VM
에 유연성이 있습니다 hello Azure toocreate 능숙 tooyou 도구 및 워크플로 사용 하 여 Linux 가상 컴퓨터 (VM). 이 문서에는 이러한 차이점과 hello Azure CLI 2.0을 포함 하 여 Linux Vm을 만들기 위한 예제가 요약 되어 있습니다. Hello를 포함 하 여 만들기 옵션을 볼 수 있습니다 [Azure CLI 1.0](creation-choices-nodejs.md)합니다.

hello [Azure CLI 2.0](/cli/azure/install-az-cli2) npm 패키지, 패키지, distro 제공 또는 Docker 컨테이너를 통해 플랫폼에서 제공 됩니다. 사용자 환경에 대 한 hello 가장 적합 한 빌드를 설치 하 고 tooan Azure 계정을 사용 하 여 로그인 [az 로그인](/cli/azure/#login)

* [Hello Azure CLI 2.0 여 Linux VM 만들기](quick-create-cli.md)
  
  * *myResourceGroup*이라는 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다. 
   
    ```azurecli
    az group create --name myResourceGroup --location eastus
    ```
    
  * 사용 하 여 VM 만들기 [az vm 만들기](/cli/azure/vm#create) 라는 *myVM* 최신 hello를 사용 하 여 *UbuntuLTS* 이미지에 이미 존재 하지 않는 경우 SSH 키를 생성 및 *~/.ssh*:

    ```azurecli
    az vm create \
        --resource-group myResourceGroup \
        --name myVM \
        --image UbuntuLTS \
        --generate-ssh-keys
    ```

* [Azure 템플릿을 사용하여 Linux VM 만들기](create-ssh-secured-vm-from-template.md)
  
  * hello 다음 예제에서는 [az 그룹 배포 만들기](/cli/azure/group/deployment#create) toocreate GitHub에 저장 된 템플릿에서 VM:
    
    ```azurecli
    az group deployment create --resource-group myResourceGroup \ 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
      --parameters @myparameters.json
    ```
* [Linux VM을 만들고 cloud-init를 사용하여 사용자 지정](tutorial-automate-vm-deployment.md)

* [여러 Linux VM에서 부하가 분산된 고가용성 응용 프로그램 만들기](tutorial-load-balancer.md)


## <a name="azure-portal"></a>Azure portal
hello [Azure 포털](https://portal.azure.com) 있습니다 tooquickly 없기 때문에 VM을 만들 tooinstall 시스템에 있습니다. Hello Azure 포털 toocreate hello VM을 사용 합니다.

* [Hello Azure 포털을 사용 하 여 Linux VM 만들기](quick-create-portal.md) 


## <a name="operating-system-and-image-choices"></a>운영 체제 및 이미지 선택
VM을 만들 때 운영 체제 toorun 원하는 hello를 기반으로 이미지를 선택 합니다. Azure 및 해당 파트너는 미리 설치된 응용 프로그램 및 도구를 포함하는 여러 이미지를 제공합니다. 또는 사용자 고유의 이미지 중 하나를 업로드 (참조 [섹션 다음 hello](#use-your-own-image)).

### <a name="azure-images"></a>Azure 이미지
사용 하 여 hello [az vm 이미지](/cli/azure/vm/image) 게시자, distro 릴리스 및 빌드에 따라 사용 가능한 란 toosee 명령입니다.

사용 가능한 게시자 나열:

```azurecli
az vm image list-publishers --location eastus
```

지정된 게시자에 사용 가능한 제품(제품) 나열:

```azurecli
az vm image list-offers --publisher Canonical --location eastus
```

지정된 제품 중 사용 가능한 SKU(배포판 릴리스) 나열:

```azurecli
az vm image list-skus --publisher Canonical --offer UbuntuServer --location eastus
```

지정된 릴리스에 사용 가능한 모든 이미지 나열:

```azurecli
az vm image list --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS --location eastus
```

검색 및 사용 가능한 이미지를 사용 하 여 더 많은 예제를 참조 하십시오. [탐색 하 고 hello Azure CLI를 사용 하 여 Azure 가상 컴퓨터 이미지 선택](cli-ps-findimage.md)합니다.

hello [az vm 만들기](/cli/azure/vm#create) 명령 tooquickly 액세스를 사용 하 여 별칭에는 일반적인 배포판 및 최신 버전의 hello 합니다. 별칭을 사용 하 여 hello 게시자, 제품, SKU 및 버전을 지정 하는 VM을 만들 때 보다 신속 하 게 관리가:

| Alias | 게시자 | 제안 | SKU | 버전 |
|:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |Centos |7.2 |최신 |
| CoreOS |CoreOS |CoreOS |Stable |최신 |
| Debian |credativ |Debian |8 |최신 |
| openSUSE |SUSE |openSUSE |13.2 |최신 |
| RHEL |Redhat |RHEL |7.2 |최신 |
| SLES |SLES |SLES |12-SP1 |최신 |
| UbuntuLTS |Canonical |UbuntuServer |14.04.4-LTS |최신 |

### <a name="use-your-own-image"></a>사용자 고유의 이미지 사용
특정 사용자 지정이 필요한 경우 해당 VM을 캡처하여 기존 Azure VM을 기반으로 하는 이미지를 사용할 수 있습니다. 이미지로 만든 온-프레미스를 업로드할 수도 있습니다. 지원 되는 배포판에 대 한 자세한 내용은 toouse 사용자 고유의 이미지를 확인 하려면 어떻게 해야 하 고 문서 다음 hello:

* [Azure 인증 배포](endorsed-distros.md)
* [보증되지 않는 배포에 대한 정보](create-upload-generic.md)
* [어떻게 toocreate 기존 Azure VM에서 이미지](tutorial-custom-images.md)합니다.
  
  * 빠른 시작 예제에서는 기존 Azure VM에서 이미지 toocreate 명령:
    
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm generalize --resource-group myResourceGroup --name myVM
    az vm image create --resource-group myResourceGroup --source myVM --name myImage
    ```

## <a name="next-steps"></a>다음 단계
* Hello로 Linux VM을 만들 [CLI](quick-create-cli.md), hello에서 [포털](quick-create-portal.md), 또는 사용 하는 [Azure 리소스 관리자 템플릿](../windows/cli-deploy-templates.md)합니다.
* Linux VM을 만든 후 [Azure 디스크 및 저장소에 대해 알아봅니다](tutorial-manage-disks.md).
* 빠른 단계 너무[암호 또는 SSH 키를 다시 설정 하 고 사용자 관리](using-vmaccess-extension.md)합니다.
