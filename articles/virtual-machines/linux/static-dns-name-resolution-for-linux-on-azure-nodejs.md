---
title: "aaaUsing VM에 대 한 내부 DNS 이름 확인을 Azure에서 | Microsoft Docs"
description: "Azure에서 VM 이름 확인을 위해 내부 DNS 사용"
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
ms.date: 12/05/2016
ms.author: v-livech
ms.openlocfilehash: 94fd6577aa51ce5db4dc26649b415ddeeb410eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-internal-dns-for-vm-name-resolution-on-azure"></a>Azure에서 VM 이름 확인을 위해 내부 DNS 사용

이 문서에서는 어떻게 tooset 정적 내부 DNS 이름을 지정 Linux Vm에 대 한 가상 NIC 카드 (VNic) 및 DNS 레이블 이름을 사용 하 여 합니다. 정적 DNS 이름은 이 문서에서 사용되는 Jenkins 빌드 서버 또는 Git 서버와 같은 영구 인프라 서비스에 사용됩니다.

hello 요구 사항은 같습니다.

* [Azure 계정](https://azure.microsoft.com/pricing/free-trial/)
* [SSH 공용 및 개인 키 파일](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="cli-versions-toocomplete-hello-task"></a>CLI 버전 toocomplete hello 작업
Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.

- [Azure CLI 1.0](#quick-commands) – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)
- [Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한


## <a name="quick-commands"></a>빠른 명령

Hello 작업을 수행를 tooquickly가 필요한 경우 다음 단원을 hello 필요한 hello 명령에 자세히 설명 합니다. 각 단계를 찾을 수 있습니다 hello 나머지 hello 문서에 대 한 정보와 컨텍스트 상세 [여기 시작](#detailed-walkthrough)합니다.  

사전 요구 사항: SSH 인바운드를 사용하는 NSG, 리소스 그룹, VNet, 서브넷입니다.

### <a name="create-a-vnic-with-a-static-internal-dns-name"></a>정적 내부 DNS 이름으로 VNic 만들기

hello `-r` cli 플래그는 hello VNic hello에 대 한 정적 DNS 이름을 제공 하는 설정 hello DNS 레이블에 대 한 합니다.

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

### <a name="deploy-hello-vm-into-hello-vnet-nsg-and-connect-hello-vnic"></a>Hello VNet NSG VM hello를 배포 하 고 hello VNic 연결

hello `-N` hello VNic toohello 연결 hello 배포 tooAzure 하는 동안 새 VM입니다.

```azurecli
azure vm create jenkins \
-g myResourceGroup \
-l westus \
-y linux \
-Q Debian \
-o myStorageAcct \
-u myAdminUser \
-M ~/.ssh/id_rsa.pub \
-F myVNet \
-j mySubnet \
-N jenkinsVNic
```

## <a name="detailed-walkthrough"></a>자세한 연습

전체 연속 통합 및 연속 배포 (CiCd) 인프라를 Azure에서 특정 서버 toobe 정적 또는 수명이 긴 서버가 필요 합니다.  Hello 가상 네트워크 (Vnet) 및 네트워크 보안 그룹 (Nsg)와 같은 Azure 자산 정적 이어야 하 고 거의 배포 되는 리소스를 수명이 긴 것이 좋습니다.  VNet에 배포한 후에 부정적인 영향을 줌 toohello 인프라 없이 새 배포 재사용할 수 있습니다.  추가 toothis 정적 네트워크는 Git 리포지토리 서버 및 Jenkins 자동화 서버 배달 CiCd tooyour 개발 또는 테스트 환경 합니다.  

내부 DNS 이름은 Azure Virtual Network 내에서만 확인할 수 있습니다.  Hello DNS 이름은 내부에 있으므로 추가 보안 toohello 인프라를 제공 하는 인터넷 외부 확인할 toohello 않습니다.

_모든 예제를 고유한 이름으로 바꿉니다._

## <a name="create-hello-resource-group"></a>Hello 리소스 그룹 만들기

리소스 그룹 필요한 tooorganize을에서는이 연습에서 만드는 모든 항목입니다.  Azure 리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.

```azurecli
azure group create myResourceGroup \
--location westus
```

## <a name="create-hello-vnet"></a>Hello VNet 만들기

hello 첫 번째 단계는 VNet toolaunch hello에 대 한 Vm toobuild입니다.  hello VNet이 연습에서는 한 서브넷을 포함합니다.  Azure Vnet에 대 한 자세한 내용은 참조 하세요. [hello Azure CLI를 사용 하 여 가상 네트워크 만들기](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure network vnet create myVNet \
--resource-group myResourceGroup \
--address-prefixes 10.10.0.0/24 \
--location westus
```

## <a name="create-hello-nsg"></a>Hello NSG 만들기

hello 서브넷 기존 네트워크 보안 그룹 뒤에 있는 기본 제공 되므로 hello 서브넷 하기 전에 hello NSG를 만들었습니다.  Azure Nsg는 hello 네트워크 계층에서 해당 tooa 방화벽.  Azure Nsg에 대 한 자세한 내용은 참조 하십시오. [toocreate Nsg에 Azure CLI hello 하는 방법](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure network nsg create myNSG \
--resource-group myResourceGroup \
--location westus
```

## <a name="add-an-inbound-ssh-allow-rule"></a>인바운드 SSH 허용 규칙 추가

Linux VM hello hello 필요한 hello Linux VM에서 인바운드 포트 22 트래픽 toobe 허용 하는 규칙 hello 네트워크 tooport 22 전달 하도록 인터넷에서에서 액세스를 해야 합니다.

```azurecli
azure network nsg rule create inboundSSH \
--resource-group myResourceGroup \
--nsg-name myNSG \
--access Allow \
--protocol Tcp \
--direction Inbound \
--priority 100 \
--source-address-prefix * \
--source-port-range * \
--destination-address-prefix 10.10.0.0/24 \
--destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a>서브넷 toohello VNet 추가

Hello VNet 내에서 Vm 서브넷에 있어야 합니다.  각 VNet에는 여러 개의 서브넷이 있을 수 있습니다.  Hello 서브넷을 만들고 hello 서브넷 hello NSG tooadd 방화벽 toohello 서브넷을 연결 합니다.

```azurecli
azure network vnet subnet create mySubNet \
--resource-group myResourceGroup \
--vnet-name myVNet \
--address-prefix 10.10.0.0/26 \
--network-security-group-name myNSG
```

이제 hello 서브넷 hello VNet 내 추가 되 고 연결 된 NSG hello 및 hello NSG 규칙입니다.

## <a name="creating-static-dns-names"></a>정적 DNS 이름 만들기

Azure는 매우 유연한 방법 이지만 toocreate로 가상 네트워크 카드 (VNics)에 레이블을 지정 하는 DNS를 사용 하 여 필요한 Vm 이름 확인에 대 한 DNS 이름을 toouse 합니다.  VNics은 다시 사용할 수 있습니다에 연결 하 여 toodifferent Vm hello Vm 임시 수 있지만 정적 리소스로 hello VNic 되므로 중요 합니다.  Hello VNic에 레이블을 지정 하는 DNS를 사용 하 여 hello VNet의에서 다른 Vm에서 간단한 이름 확인을 tooenable 수 있습니다.  Hello DNS 이름으로 다른 Vm tooaccess hello 자동화 서버를 사용 하면 확인할 수 있는 이름을 사용 하 여 `Jenkins` 또는 Git 서버 hello `gitrepo`합니다.  VNic 만들고 서브넷 hello 이전 단계에서 만든 hello와 연결 합니다.

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Hello VNet에 VM hello 및 NSG를 배포 합니다.

해당 VNet 및 역할을 하는 방화벽 tooprotect 우리의 서브넷 SSH에 대 한 포트 22 제외한 모든 인바운드 트래픽 차단 하 여 NSG 내부 서브넷 VNet 했습니다.  이제이 기존 네트워크 인프라 내 hello VM을 배포할 수 있습니다.

Hello Azure CLI 및 hello를 사용 하 여 `azure vm create` hello Linux VM은 Azure 리소스 그룹, VNet, 서브넷 및 VNic 기존 배포 toohello 명령입니다.  Hello CLI toodeploy 전체 VM 사용에 대 한 자세한 내용은 참조 하세요. [hello Azure CLI를 사용 하 여 완벽 한 Linux 환경을 만들](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure vm create jenkins \
--resource-group myResourceGroup myVM \
--location westus \
--os-type linux \
--image-urn Debian \
--storage-account-name mystorageaccount \
--admin-username myAdminUser \
--ssh-publickey-file ~/.ssh/id_rsa.pub \
--vnet-name myVNet \
--vnet-subnet-name mySubnet \
--nic-name jenkinsVNic
```

CLI 플래그는 hello를 사용 하 여 기존 리소스를 toocall hello 기존 네트워크 내부 Azure toodeploy hello VM 하도록 지시 합니다.  tooreiterate, VNet 및 서브넷에 배포 된 후 있습니다 수로 유지 되 Azure 지역이 내부 정적 지, 영구적인 리소스입니다.  

## <a name="next-steps"></a>다음 단계
* [Azure CLI 명령을 직접 사용하여 Linux VM에 대한 고유한 사용자 지정 환경 만들기](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [템플릿을 사용하여 Azure에서 Linux VM 만들기](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
