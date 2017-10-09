---
title: "aaaUse VM에 대 한 내부 DNS 이름 확인 Azure CLI 2.0 hello로 | Microsoft Docs"
description: "Toocreate 가상 네트워크 인터페이스 카드 하 고 Azure CLI 2.0 hello로 Azure에서 VM 이름 확인에 대 한 내부 DNS를 사용 하는 방법"
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
ms.devlang: azurecli
ms.topic: article
ms.date: 02/16/2017
ms.author: v-livech
ms.openlocfilehash: b3c4bfd3ab698f7b25d763ba9e60dd7984f6269d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-virtual-network-interface-cards-and-use-internal-dns-for-vm-name-resolution-on-azure"></a>가상 네트워크 인터페이스 카드 만들기 및 Azure에서 VM 이름 확인을 위해 내부 DNS 사용
이 문서 tooset 정적 내부 DNS 이름을 사용 하 여 가상 Linux Vm에 대 한 네트워크 인터페이스 카드 (vNics) 및 Azure CLI 2.0 hello로 DNS 레이블 이름의 방법을 보여 줍니다. Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. 정적 DNS 이름은 이 문서에서 사용되는 Jenkins 빌드 서버 또는 Git 서버와 같은 영구 인프라 서비스에 사용됩니다.

hello 요구 사항은 같습니다.

* [Azure 계정](https://azure.microsoft.com/pricing/free-trial/)
* [SSH 공용 및 개인 키 파일](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a>빠른 명령
Hello 작업을 수행를 tooquickly가 필요한 경우 다음 단원을 hello 필요한 hello 명령에 자세히 설명 합니다. 각 단계는 hello 나머지 hello 문서에서에서 확인할 수 있습니다에 대 한 정보와 컨텍스트 상세 [여기 시작](#detailed-walkthrough)합니다. 이 단계는 tooperform, 필요한 hello 최신 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 tooan Azure 계정을 사용 하 여 로그인 [az 로그인](/cli/azure/#login)합니다.

사전 요구 사항: 리소스 그룹, 가상 네트워크 및 서브넷, SSH 인바운드가 있는 네트워크 보안 그룹.

### <a name="create-a-virtual-network-interface-card-with-a-static-internal-dns-name"></a>정적 내부 DNS 이름을 가진 가상 네트워크 인터페이스 카드 만들기
만들기와 hello vNic [az 네트워크 nic 만들](/cli/azure/network/nic#create)합니다. hello `--internal-dns-name` CLI 플래그는 hello hello 가상 네트워크 인터페이스 카드 (vNic)에 대 한 정적 DNS 이름을 제공 하는 설정 hello DNS 레이블에 대 한 합니다. hello 다음 예제에서는 명명 된 vNic `myNic`, toohello 연결 `myVnet` 가상 네트워크를 호출 하는 내부 DNS 이름 레코드를 만듭니다 `jenkins`:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

### <a name="deploy-a-vm-and-connect-hello-vnic"></a>VM을 배포 하 고 hello vNic 연결
[az vm create](/cli/azure/vm#create)로 VM을 만듭니다. hello `--nics` hello 배포 tooAzure 중 hello vNic toohello VM을 연결 하는 플래그입니다. hello 다음 예제에서는 V `myVM` Azure 관리 되는 디스크와 연결 합니다. hello vNic 라는 `myNic` hello 앞 단계에서에서:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="detailed-walkthrough"></a>자세한 연습

전체 연속 통합 및 연속 배포 (CiCd) 인프라를 Azure에서 특정 서버 toobe 정적 또는 수명이 긴 서버가 필요 합니다. 가상 네트워크 및 네트워크 보안 그룹 hello와 같은 Azure 자산 정적 이며 거의 배포 되는 리소스를 수명이 긴 것이 좋습니다. 가상 네트워크에 배포한 후에 부정적인 영향을 줌 toohello 인프라 없이 새 배포 재사용할 수 있습니다. Git 리포지토리 서버를 나중에 추가할 수 있습니다 또는 Jenkins 자동화 서버 CiCd toothis 개발 또는 테스트 환경에 대 한 가상 네트워크를 제공 합니다.  

내부 DNS 이름은 Azure Virtual Network 내에서만 확인할 수 있습니다. Hello DNS 이름은 내부에 있으므로 추가 보안 toohello 인프라를 제공 하는 인터넷 외부 확인할 toohello 않습니다.

Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다. 예제 매개 변수 이름에 `myResourceGroup`, `myNic` 및 `myVM`이 포함됩니다.

## <a name="create-hello-resource-group"></a>Hello 리소스 그룹 만들기
Hello 리소스 그룹을 먼저 만듭니다 [az 그룹 만들기](/cli/azure/group#create)합니다. hello 다음 예제에서는 명명 된 리소스 그룹 `myResourceGroup` hello에 `westus` 위치:

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-hello-virtual-network"></a>Hello 가상 네트워크 만들기

hello 다음 단계에는 가상 네트워크 toolaunch hello에 대 한 Vm toobuild입니다. 이 연습에서는 한 서브넷을 포함 하는 hello 가상 네트워크입니다. Azure 가상 네트워크에 대 한 자세한 내용은 참조 하십시오. [hello Azure CLI를 사용 하 여 가상 네트워크를 만들](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. 

Hello 가상 네트워크를 만듭니다 [az 네트워크 vnet 만들기](/cli/azure/network/vnet#create)합니다. hello 다음 예제에서는 가상 네트워크를 만들어 명명 된 `myVnet` 와 명명 된 서브넷 `mySubnet`:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

## <a name="create-hello-network-security-group"></a>Hello 네트워크 보안 그룹 만들기
Azure 네트워크 보안 그룹은 hello 네트워크 계층에서 해당 tooa 방화벽입니다. 네트워크 보안 그룹에 대 한 자세한 내용은 참조 [어떻게 toocreate Nsg에 hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. 

Hello 네트워크 보안 그룹을 만들 [az 네트워크 nsg 만들기](/cli/azure/network/nsg#create)합니다. hello 다음 예제에서는 네트워크 보안 그룹을 만든 라는 `myNetworkSecurityGroup`:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-rule-tooallow-ssh"></a>SSH는 인바운드 규칙 tooallow 추가
네트워크 보안 그룹을 hello에 대 한 인바운드 규칙 추가 [az 네트워크 nsg 규칙 만들기](/cli/azure/network/nsg/rule#create)합니다. hello 다음 예제는 규칙을 만들고 라는 `myRuleAllowSSH`:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myRuleAllowSSH \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --source-address-prefix '*' \
    --source-port-range '*' \
    --destination-address-prefix '*' \
    --destination-port-range 22 \
    --access allow
```

## <a name="associate-hello-subnet-with-hello-network-security-group"></a>Hello 서브넷 hello 네트워크 보안 그룹을 연결
tooassociate hello 서브넷 hello 네트워크 보안 그룹을 사용 하 여 [az 네트워크 vnet 서브넷 업데이트](/cli/azure/network/vnet/subnet#update)합니다. hello 다음 예제에서는 연결 hello 서브넷 이름 `mySubnet` 네트워크 보안 그룹 이라는 hello로 `myNetworkSecurityGroup`:

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```


## <a name="create-hello-virtual-network-interface-card-and-static-dns-names"></a>Hello 가상 네트워크 인터페이스 카드를 만들고 정적 DNS 이름
Azure는 매우 유연한 방법 이지만 toocreate 가상 네트워크 인터페이스 카드 (vNics) DNS 레이블을 포함 하는 필요한 VM 이름 확인에 대 한 DNS 이름을 toouse 합니다. vNics는 다시 사용할 수 있습니다에 연결 하 여 toodifferent Vm hello 인프라가 수명 주기에 대 때 중요 합니다. 이 방법은 hello Vm 말할 수 하는 동안 정적 리소스로 hello vNic를 유지 합니다. Hello vNic에 레이블을 지정 하는 DNS를 사용 하 여 hello VNet의에서 다른 Vm에서 간단한 이름 확인을 tooenable 수 있습니다. Hello DNS 이름으로 다른 Vm tooaccess hello 자동화 서버를 사용 하면 확인할 수 있는 이름을 사용 하 여 `Jenkins` 또는 Git 서버 hello `gitrepo`합니다.  

만들기와 hello vNic [az 네트워크 nic 만들](/cli/azure/network/nic#create)합니다. hello 다음 예제에서는 명명 된 vNic `myNic`, toohello 연결 `myVnet` 이라는 가상 네트워크 `myVnet`를 호출 하는 내부 DNS 이름 레코드를 만듭니다 `jenkins`:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Hello VM hello 가상 네트워크 인프라에 배포
했습니다 가상 네트워크 및 서브넷에 역할을 하는 방화벽 tooprotect 우리의 서브넷 SSH, 및 vNic에 대 한 포트 22 제외한 모든 인바운드 트래픽 차단 하 여 네트워크 보안 그룹입니다. 이제 이 기존 네트워크 인프라 내에 VM을 배포할 수 있습니다.

[az vm create](/cli/azure/vm#create)로 VM을 만듭니다. hello 다음 예제에서는 V `myVM` Azure 관리 되는 디스크와 연결 합니다. hello vNic 라는 `myNic` hello 앞 단계에서에서:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

CLI 플래그는 hello를 사용 하 여 기존 리소스를 toocall hello 기존 네트워크 내부 Azure toodeploy hello VM 하도록 지시 합니다. tooreiterate, VNet 및 서브넷에 배포 된 후 있습니다 수로 유지 되 Azure 지역이 내부 정적 지, 영구적인 리소스입니다.  

## <a name="next-steps"></a>다음 단계
* [Azure CLI 명령을 직접 사용하여 Linux VM에 대한 고유한 사용자 지정 환경 만들기](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [템플릿을 사용하여 Azure에서 Linux VM 만들기](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
