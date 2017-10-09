---
title: "hello Azure CLI 1.0가 있는 완벽 한 Linux 환경 aaaCreate | Microsoft Docs"
description: "Hello Azure CLI 1.0을 사용 하 여 접지 hello 모두에서 저장소, Linux VM, 가상 네트워크 및 서브넷, 부하 분산 장치, NIC를, 공용 IP 및 네트워크 보안 그룹을 만듭니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 7fe00e138704fe9c9a1c9b87a7dd1afd6174e527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-environment-with-hello-azure-cli-10"></a>완벽 한 Linux 환경을 Azure CLI 1.0 hello로 만들기
이 문서에서는 개발 및 간단한 계산에 유용한 부하 분산 장치와 한 쌍의 VM을 사용하여 간단한 네트워크를 빌드해 보겠습니다. 명령에서 명령 hello 과정을 진행, Linux Vm toowhich hello 인터넷에서 임의의 위치에서 연결할 수 있습니다 안전 하 고 구성할 때까지 두 작업을 합니다. 그런 다음 toomore 복잡 한 네트워크와 환경에서 이동할 수 있습니다.

Hello 과정 배웁니다 hello 종속성 계층 구조에 대 한 hello 리소스 관리자 배포 모델을 통해, 및 전력이 얼마나에 대 한 제공 합니다. Hello 시스템 빌드되는 방식을 확인 한 후 다시 작성할 수 있습니다 것 보다 빠르게 사용 하 여 [Azure 리소스 관리자 템플릿을](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. 또한 사용자 환경의 hello 부분 개념이 서로 어떻게를 파악 한 후 템플릿 tooautomate 만드는 해당 쉬워집니다.

hello 환경에 포함 되어 있습니다.

* 가용성 집합에 포함된 두 VM
* 포트 80에서 부하 분산 규칙이 있는 부하 분산 장치
* 네트워크 보안 그룹 (NSG) 규칙은 VM에서 원치 않는 트래픽에 tooprotect 합니다.

toocreate이 사용자 지정 환경을 hello 최신 필요한 [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 리소스 관리자 모드에서 (`azure config mode arm`). JSON 구문 분석 도구도 필요합니다. 이 예제에서는 [jq](https://stedolan.github.io/jq/)를 사용합니다.


## <a name="cli-versions-toocomplete-hello-task"></a>CLI 버전 toocomplete hello 작업
Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.

- [Azure CLI 1.0](#quick-commands) – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)
- [Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한


## <a name="quick-commands"></a>빠른 명령
Tooquickly 해야 할 경우 hello 작업을 수행, 다음 섹션의 세부 정보 hello hello 기본 명령을 tooupload VM tooAzure 합니다. 각 단계는 hello 나머지 시작 하는 hello 문서에서에서 확인할 수 있습니다에 대 한 정보와 컨텍스트 상세 [여기](#detailed-walkthrough)합니다.

확인 했는지 [Azure CLI 1.0 hello](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 에 로그인 하 고 리소스 관리자 모드를 사용 하 여:

```azurecli
azure config mode arm
```

Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다. 예제 매개 변수 이름에 `myResourceGroup`, `mystorageaccount` 및 `myVM`이 포함됩니다.

Hello 리소스 그룹을 만듭니다. hello 다음 예제에서는 명명 된 리소스 그룹 `myResourceGroup` hello에 `westeurope` 위치:

```azurecli
azure group create -n myResourceGroup -l westeurope
```

Hello JSON 파서를 사용 하 여 hello 리소스 그룹을 확인 합니다.

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Hello 저장소 계정을 만듭니다. hello 다음 예제에서는 라는 저장소 계정을 `mystorageaccount`합니다. (사용자 자신의 고유 이름을 제공, 고유 해야 hello 저장소 계정 이름입니다.)

```azurecli
azure storage account create -g myResourceGroup -l westeurope \
  --kind Storage --sku-name GRS mystorageaccount
```

Hello JSON 파서를 사용 하 여 hello 저장소 계정을 확인 합니다.

```azurecli
azure storage account show -g myResourceGroup mystorageaccount --json | jq '.'
```

Hello 가상 네트워크를 만듭니다. hello 다음 예제에서는 가상 네트워크를 만들어 라는 `myVnet`:

```azurecli
azure network vnet create -g myResourceGroup -l westeurope\
  -n myVnet -a 192.168.0.0/16
```

서브넷을 만듭니다. hello 다음 예제에서는 서브넷을 만듭니다. 명명 된 `mySubnet`:

```azurecli
azure network vnet subnet create -g myResourceGroup \
  -e myVnet -n mySubnet -a 192.168.1.0/24
```

Hello JSON 파서를 사용 하 여 hello 가상 네트워크 및 서브넷을 확인 합니다.

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

공용 IP를 만듭니다. hello 다음 예제에서는 명명 된 공용 IP `myPublicIP` 의 hello DNS 이름을 가진 `mypublicdns`합니다. (사용자 자신의 고유 이름을 제공, 고유 해야 hello DNS 이름입니다.)

```azurecli
azure network public-ip create -g myResourceGroup -l westeurope \
  -n myPublicIP  -d mypublicdns -a static -i 4
```

Hello 부하 분산 장치를 만듭니다. hello 다음 예제에서는 명명 된 부하 분산 장치 `myLoadBalancer`:

```azurecli
azure network lb create -g myResourceGroup -l westeurope -n myLoadBalancer
```

Hello 부하 분산 장치에 대 한 프런트 엔드 IP 풀을 만들고 hello 공용 IP를 연결 합니다. hello 다음 예제에서는 명명 된 프런트 엔드 IP 풀을 `mySubnetPool`:

```azurecli
azure network lb frontend-ip create -g myResourceGroup -l myLoadBalancer \
  -i myPublicIP -n myFrontEndPool
```

Hello 부하 분산 장치에 대 한 hello 백 엔드 IP 풀을 만듭니다. hello 다음 예제에서는 명명 된 백 엔드 IP 풀을 `myBackEndPool`:

```azurecli
azure network lb address-pool create -g myResourceGroup -l myLoadBalancer \
  -n myBackEndPool
```

SSH 인바운드 네트워크 hello 부하 분산 장치에 대 한 주소 nat 규칙을 만듭니다. hello 다음 예제에서는 두 가지 부하 분산 장치 규칙 `myLoadBalancerRuleSSH1` 및 `myLoadBalancerRuleSSH2`:

```azurecli
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH1 -p tcp -f 4222 -b 22
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH2 -p tcp -f 4223 -b 22
```

Hello 웹 만들 부하 분산 장치 인바운드 NAT 규칙의 hello에 대 한 합니다. hello 다음 예제에서는 명명 된 부하 분산 장치 규칙 `myLoadBalancerRuleWeb`:

```azurecli
azure network lb rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleWeb -p tcp -f 80 -b 80 \
  -t myFrontEndPool -o myBackEndPool
```

Hello 부하 분산 장치 상태 프로브를 만듭니다. hello 다음 예제에서는 명명 된 TCP 프로브 `myHealthProbe`:

```azurecli
azure network lb probe create -g myResourceGroup -l myLoadBalancer \
  -n myHealthProbe -p "tcp" -i 15 -c 4
```

Hello JSON 파서를 사용 하 여 hello 부하 분산 장치, IP 풀 및 NAT 규칙을 확인 합니다.

```azurecli
azure network lb show -g myResourceGroup -n myLoadBalancer --json | jq '.'
```

Hello 첫 번째 네트워크 인터페이스 카드 (NIC)를 만듭니다. Hello 대체 `#####-###-###` 섹션에서는 사용자 고유의 Azure 구독 id 구독 ID의 hello 출력에서 설명한 **jq** 만들면 hello 리소스를 검사 하는 경우. `azure account list`를 사용하여 구독 ID를 볼 수도 있습니다.

hello 다음 예제에서는 명명 된 NIC `myNic1`:

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic1 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
```

두 번째 NIC. hello 만들기 hello 다음 예제에서는 명명 된 NIC `myNic2`:

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic2 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
```

Hello JSON 파서를 사용 하 여 hello 두 Nic를 확인 합니다.

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
azure network nic show myResourceGroup myNic2 --json | jq '.'
```

Hello 네트워크 보안 그룹을 만듭니다. hello 다음 예제에서는 네트워크 보안 그룹을 만든 라는 `myNetworkSecurityGroup`:

```azurecli
azure network nsg create -g myResourceGroup -l westeurope \
  -n myNetworkSecurityGroup
```

Hello 네트워크 보안 그룹에 대 한 두 가지 인바운드 규칙을 추가 합니다. hello 다음 예제에서는 두 개의 규칙으로 `myNetworkSecurityGroupRuleSSH` 및 `myNetworkSecurityGroupRuleHTTP`:

```azurecli
azure network nsg rule create -p tcp -r inbound -y 1000 -u 22 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleSSH
azure network nsg rule create -p tcp -r inbound -y 1001 -u 80 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleHTTP
```

Hello JSON 파서를 사용 하 여 hello 네트워크 보안 그룹 및 인바운드 규칙을 확인 합니다.

```azurecli
azure network nsg show -g myResourceGroup -n myNetworkSecurityGroup --json | jq '.'
```

바인딩 hello 네트워크 보안 그룹 toohello 두 Nic:

```azurecli
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic1
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic2
```

Hello 가용성 집합을 만듭니다. hello 다음 예제에서는 가용성 명명 된 집합 `myAvailabilitySet`:

```azurecli
azure availset create -g myResourceGroup -l westeurope -n myAvailabilitySet
```

만드는 첫 번째 Linux VM hello 합니다. hello 다음 예제에서는 V `myVM1`:

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM1 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic1 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

Hello 만들기 Linux VM의 두 번째입니다. hello 다음 예제에서는 V `myVM2`:

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM2 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic2 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

모든 항목이 작성 된 JSON 파서 tooverify hello를 사용 합니다.

```azurecli
azure vm show -g myResourceGroup -n myVM1 --json | jq '.'
azure vm show -g myResourceGroup -n myVM2 --json | jq '.'
```

새 환경 tooa 템플릿 tooquickly 다시 만드는 새 인스턴스를 내보냅니다.

```azurecli
azure group export myResourceGroup
```

## <a name="detailed-walkthrough"></a>자세한 연습
hello 수행 하는 자세한 단계 설명 환경으로 빌드하는 동안 각 명령이 수행 하는 작업입니다. 이러한 개념은 개발 또는 프로덕션에 맞는 고유한 사용자 지정 환경을 빌드할 때 도움이 됩니다.

확인 했는지 [Azure CLI 1.0 hello](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 에 로그인 하 고 리소스 관리자 모드를 사용 하 여:

```azurecli
azure config mode arm
```

Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다. 예제 매개 변수 이름에 `myResourceGroup`, `mystorageaccount` 및 `myVM`이 포함됩니다.

## <a name="create-resource-groups-and-choose-deployment-locations"></a>리소스 그룹 만들기 및 배포 위치 선택
Azure 리소스 그룹은 구성 정보 및 메타 데이터 tooenable hello 논리의 관리 리소스 배포를 포함 하는 논리적 배포 엔터티입니다. hello 다음 예제에서는 명명 된 리소스 그룹 `myResourceGroup` hello에 `westeurope` 위치:

```azurecli
azure group create --name myResourceGroup --location westeurope
```

출력:

```azurecli                        
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westeurope
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

## <a name="create-a-storage-account"></a>저장소 계정 만들기
저장소 계정은 모든 추가 데이터 디스크 및 VM 디스크에 대 한 tooadd 되도록 해야 합니다. 리소스 그룹을 만든 후 거의 즉시 저장소 계정을 만들게 됩니다.

Hello 사용 여기 `azure storage account create` 명령, 및 원하는 저장소 지원 hello 유형 제어 hello 리소스 그룹 hello 계정의 hello 위치를 전달 합니다. hello 다음 예제에서는 라는 저장소 계정을 `mystorageaccount`:

```azurecli
azure storage account create \  
  --location westeurope \
  --resource-group myResourceGroup \
  --kind Storage --sku-name GRS \
  mystorageaccount
```

출력:

```azurecli
info:    Executing command storage account create
+ Creating storage account
info:    storage account create command OK
```

hello를 사용 하 여 리소스 그룹 tooexamine `azure group show` 명령에서 hello를 사용 하 여 보겠습니다 [jq](https://stedolan.github.io/jq/) hello와 함께 도구 `--json` Azure CLI 옵션입니다. (사용할 수 있습니다 **jsawk** 또는 tooparse 원하는 모든 언어 라이브러리 JSON을 환영 합니다.)

```azurecli
azure group show myResourceGroup --json | jq '.'
```

출력:

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

hello CLI를 사용 하 여 hello 저장소 계정을 tooinvestigate 먼저 tooset hello 계정 이름과 키입니다. 다음 예에서는 사용자가 선택한 이름으로 hello에 대 한 hello 저장소 계정의 hello 이름을 바꿉니다.

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(azure storage account connectionstring show mystorageaccount --resource-group myResourceGroup --json | jq -r '.string')"
```

그러면 저장소 정보를 쉽게 볼 수 있습니다.

```azurecli
azure storage container list
```

출력:

```azurecli
info:    Executing command storage container list
+ Getting storage containers
data:    Name  Public-Access  Last-Modified
data:    ----  -------------  -----------------------------
data:    vhds  Off            Sun, 27 Sep 2015 19:03:54 GMT
info:    storage container list command OK
```

## <a name="create-a-virtual-network-and-subnet"></a>가상 네트워크 및 서브넷 만들기
그런 다음 거 tooneed toocreate Azure 및 Vm을 만들 수 있는 서브넷에서 실행 되는 가상 네트워크입니다. hello 다음 예제에서는 가상 네트워크를 만들어 명명 된 `myVnet` hello로 `192.168.0.0/16` 주소 접두사:

```azurecli
azure network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefixes 192.168.0.0/16
```

출력:

```azurecli
info:    Executing command network vnet create
+ Looking up virtual network "myVnet"
+ Creating virtual network "myVnet"
+ Loading virtual network state
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet
data:    Name                            : myVnet
data:    Type                            : Microsoft.Network/virtualNetworks
data:    Location                        : westeurope
data:    ProvisioningState               : Succeeded
data:    Address prefixes:
data:      192.168.0.0/16
info:    network vnet create command OK
```

다시 보겠습니다 옵션 사용 하 여 hello-json의 `azure group show` 및 `jq` toosee 우리는를 구축 하 고 어떻게 합니다. 이제 `storageAccounts` 리소스 및 `virtualNetworks` 리소스가 생겼습니다.  

```azurecli
azure group show myResourceGroup --json | jq '.'
```

출력:

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
      "name": "myVnet",
      "type": "virtualNetworks",
      "location": "westeurope",
      "tags": null
    },
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

이제 hello에 서브넷을 만들어 보겠습니다 `myVnet` 는 hello에 Vm이 배포 된 가상 네트워크입니다. Hello 사용 `azure network vnet subnet create` 이미 만들었습니다 hello 리소스와 함께 명령을: hello `myResourceGroup` 리소스 그룹 및 hello `myVnet` 가상 네트워크입니다. 다음 예제는 hello, 라는 hello 서브넷 추가 `mySubnet` hello 서브넷 주소 접두사와 `192.168.1.0/24`:

```azurecli
azure network vnet subnet create --resource-group myResourceGroup \
  --vnet-name myVnet --name mySubnet --address-prefix 192.168.1.0/24
```

출력:

```azurecli
info:    Executing command network vnet subnet create
+ Looking up hello subnet "mySubnet"
+ Creating subnet "mySubnet"
+ Looking up hello subnet "mySubnet"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:    Type                            : Microsoft.Network/virtualNetworks/subnets
data:    ProvisioningState               : Succeeded
data:    Name                            : mySubnet
data:    Address prefix                  : 192.168.1.0/24
data:
info:    network vnet subnet create command OK
```

Hello 서브넷 hello 가상 네트워크 내의 논리적으로 이기 때문에 약간 다른 명령 사용 하 여 hello 서브넷 정보에서는 찾습니다. hello 명령을 사용 하 여 `azure network vnet show`, tooexamine hello JSON 출력 사용 하 여 계속 실행 되지만 `jq`합니다.

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

출력:

```json
{
  "subnets": [
    {
      "ipConfigurations": [],
      "addressPrefix": "192.168.1.0/24",
      "provisioningState": "Succeeded",
      "name": "mySubnet",
      "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
    }
  ],
  "tags": {},
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "provisioningState": "Succeeded",
  "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "name": "myVnet",
  "location": "westeurope"
}
```

## <a name="create-a-public-ip-address"></a>공용 IP 주소 만들기
이제 hello 공용 IP 주소 (PIP) tooyour 부하 분산 장치 할당을 만들어 보겠습니다. 하면 hello 인터넷에서에서 tooconnect tooyour Vm hello를 사용 하 여 `azure network public-ip create` 명령입니다. Hello에 명명 된 DNS 항목을 만듭니다 hello 기본 주소는 동적 **cloudapp.azure.com** hello를 사용 하 여 도메인 `--domain-name-label` 옵션입니다. hello 다음 예제에서는 명명 된 공용 IP `myPublicIP` 의 hello DNS 이름을 가진 `mypublicdns`합니다. Hello DNS 이름은 고유 해야 하기 때문에 고유한 DNS 이름을 제공 합니다.

```azurecli
azure network public-ip create --resource-group myResourceGroup \
  --location westeurope --name myPublicIP --domain-name-label mypublicdns
```

출력:

```azurecli
info:    Executing command network public-ip create
+ Looking up hello public ip "myPublicIP"
+ Creating public ip address "myPublicIP"
+ Looking up hello public ip "myPublicIP"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
data:    Name                            : myPublicIP
data:    Type                            : Microsoft.Network/publicIPAddresses
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Allocation method               : Dynamic
data:    Idle timeout                    : 4
data:    Domain name label               : mypublicdns
data:    FQDN                            : mypublicdns.westeurope.cloudapp.azure.com
info:    network public-ip create command OK
```

hello 공용 IP 주소는 또한 최상위 리소스를 사용 하 여 볼 수 있도록 `azure group show`합니다.

```azurecli
azure group show myResourceGroup --json | jq '.'
```

출력:

```json
{
"tags": {},
"id": "/subscriptions/guid/resourceGroups/myResourceGroup",
"name": "myResourceGroup",
"provisioningState": "Succeeded",
"location": "westeurope",
"properties": {
    "provisioningState": "Succeeded"
},
"resources": [
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "name": "myPublicIP",
    "type": "publicIPAddresses",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
    "name": "myVnet",
    "type": "virtualNetworks",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
    "name": "mystorageaccount",
    "type": "storageAccounts",
    "location": "westeurope",
    "tags": null
    }
],
"permissions": [
    {
    "actions": [
        "*"
    ],
    "notActions": []
    }
]
}
```

전체 hello를 사용 하 여 hello hello 하위 도메인의 정규화 된 도메인 이름 (FQDN)을 포함 하 여 더 많은 리소스 정보를 조사할 수 `azure network public-ip show` 명령입니다. hello 공용 IP 주소 리소스를 논리적으로 할당 하지만 특정 주소 아직 할당 되지 않았습니다. IP 주소 tooobtain tooneed에서는 아직 만들지 않은 부하 분산 장치 거 합니다.

```azurecli
azure network public-ip show myResourceGroup myPublicIP --json | jq '.'
```

출력:

```json
{
"tags": {},
"publicIpAllocationMethod": "Dynamic",
"dnsSettings": {
    "domainNameLabel": "mypublicdns",
    "fqdn": "mypublicdns.westeurope.cloudapp.azure.com"
},
"idleTimeoutInMinutes": 4,
"provisioningState": "Succeeded",
"etag": "W/\"c63154b3-1130-49b9-a887-877d74d5ebc5\"",
"id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
"name": "myPublicIP",
"location": "westeurope"
}
```

## <a name="create-a-load-balancer-and-ip-pools"></a>부하 분산 장치 및 IP 풀 만들기
부하 분산 장치를 만들 때 하면 toodistribute 트래픽을 여러 Vm에서. 또한 toouser 요청 hello 유지 관리 또는 과도 한 로드 이벤트에 응답 하는 여러 Vm을 실행 하 여 중복 tooyour 응용 프로그램을 제공 합니다. hello 다음 예제에서는 명명 된 부하 분산 장치 `myLoadBalancer`:

```azurecli
azure network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer
```

출력:

```azurecli
info:    Executing command network lb create
+ Looking up hello load balancer "myLoadBalancer"
+ Creating load balancer "myLoadBalancer"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer
data:    Name                            : myLoadBalancer
data:    Type                            : Microsoft.Network/loadBalancers
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
info:    network lb create command OK
```

이 부하 분산 장치는 비어 있는 상태이므로 몇 개의 IP 풀을 만들겠습니다. 이 부하 분산 장치, hello 프런트 엔드에 대 한 한 hello 백 엔드에 대 한 IP 풀 toocreate 두 주시기 바랍니다. 프런트 엔드 IP 풀 hello 공개적으로 표시 됩니다. 앞에서 만든 PIP hello 할당 hello 위치 toowhich 이기도 합니다. 다음에 Vm tooconnect를 위해 위치로 hello 백 엔드 풀 사용. 이런 방식으로 hello 트래픽 hello 부하 분산 장치 toohello Vm 통해 전달 될 수 있습니다.

가장 먼저 프런트 엔드 IP 풀을 만들겠습니다. hello 다음 예제에서는 이라는 프런트 엔드 풀 `myFrontEndPool`:

```azurecli
azure network lb frontend-ip create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --public-ip-name myPublicIP \
  --name myFrontEndPool
```

출력:

```azurecli
info:    Executing command network lb frontend-ip create
+ Looking up hello load balancer "myLoadBalancer"
+ Looking up hello public ip "myPublicIP"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myFrontEndPool
data:    Provisioning state              : Succeeded
data:    Private IP allocation method    : Dynamic
data:    Public IP address id            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
info:    network lb mySubnet-ip create command OK
```

Hello 어떻게 사용 참고 `--public-ip-name` hello toopass 전환 `myPublicIP` 앞에서 만든 합니다. 할당 hello 공용 IP 주소 toohello 부하 분산 장치 하면 있습니다 tooreach hello 인터넷을 통해 Vm에 있습니다.

다음으로 백 엔드 트래픽에 사용할 두 번째 IP 풀을 만들겠습니다. hello 다음 예제에서는 명명 된 백 엔드 풀 `myBackEndPool`:

```azurecli
azure network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

출력:

```azurecli
info:    Executing command network lb address-pool create
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myBackEndPool
data:    Provisioning state              : Succeeded
info:    network lb address-pool create command OK
```

이 부하 분산 장치를 검색 하 여 어떻게 진행은 볼 수 있습니다 `azure network lb show` hello JSON 출력을 검토 합니다.

```azurecli
azure network lb show myResourceGroup myLoadBalancer --json | jq '.'
```

출력:

```json
{
  "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [],
  "probes": []
}
```

## <a name="create-load-balancer-nat-rules"></a>부하 분산 장치 NAT 규칙 만들기
이 부하 분산 장치를 통해 흐르는 tooget 트래픽 toocreate 네트워크 주소 변환 (NAT) 규칙 인바운드 또는 아웃 바운드 동작을 지정 해야 합니다. Hello 프로토콜 toouse 지정 다음 필요에 따라 외부 포트 toointernal 포트를 매핑할 수 있습니다. 환경에서는 Vm이 부하 분산 장치 tooour 통해 SSH를 허용 하는 몇 가지 규칙을 만들어 보겠습니다. (나중에 생성)를 통해 Vm에서 TCP 포트 4222 및 4223 toodirect tooTCP 포트 22 설정 합니다. hello 다음 예제는 규칙을 만들고 라는 `myLoadBalancerRuleSSH1` toomap TCP 포트 22 4222 tooport:

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 \
  --protocol tcp --frontend-port 4222 --backend-port 22
```

출력:

```azurecli
info:    Executing command network lb inbound-nat-rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default enable floating ip: false
warn:    Using default idle timeout: 4
warn:    Using default mySubnet IP configuration "myFrontEndPool"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleSSH1
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 4222
data:    Backend port                    : 22
data:    Enable floating IP              : false
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
info:    network lb inbound-nat-rule create command OK
```

SSH에 대 한 두 번째 NAT 규칙에 대 한 hello 절차를 반복 합니다. hello 다음 예제는 규칙을 만들고 라는 `myLoadBalancerRuleSSH2` toomap TCP 포트 22 4223 tooport:

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22
```

보겠습니다도 hello 규칙 tooour IP 풀 연결 되는 웹 트래픽에 대해 TCP 포트 80에 대 한 NAT 규칙을 만듭니다. म 후크 hello 규칙 tooan IP 풀 hello 규칙 tooour Vm 개별적으로 연결 해야 하는 경우 추가 하거나 Vm hello IP 풀에서 제거 수입니다. hello 부하 분산 장치를 자동으로 hello 트래픽 흐름을 조정합니다. hello 다음 예제는 규칙을 만들고 라는 `myLoadBalancerRuleWeb` toomap TCP 포트 80 tooport 80:

```azurecli
azure network lb rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleWeb --protocol tcp \
  --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEndPool \
  --backend-address-pool-name myBackEndPool
```

출력:

```azurecli
info:    Executing command network lb rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default idle timeout: 4
warn:    Using default enable floating ip: false
warn:    Using default load distribution: Default
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleWeb
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 80
data:    Backend port                    : 80
data:    Enable floating IP              : false
data:    Load distribution               : Default
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
data:    Backend address pool id         : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
info:    network lb rule create command OK
```

## <a name="create-a-load-balancer-health-probe"></a>부하 분산 장치 상태 프로브 만들기
상태 프로브 주기적으로 hello 작동 하 고 정의 된 대로 toorequests를 응답에 있는지이 부하 분산 장치 toomake 뒤에 있는 Vm에 대해 검사 합니다. 제거할 not, 사용자가 아닌 되 고 작업을 tooensure toothem을 권고 합니다. 간격 및 시간 제한 값을 함께 hello 상태 검색에 대 한 사용자 지정 검사를 정의할 수 있습니다. 상태 프로브에 대한 자세한 내용은 [부하 분산 장치 프로브](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요. hello 다음 예제에서는 TCP 상태 검색 명명 `myHealthProbe`:

```azurecli
azure network lb probe create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myHealthProbe --protocol "tcp" \
  --interval 15 --count 4
```

출력:

```azurecli
info:    Executing command network lb probe create
warn:    Using default probe port: 80
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myHealthProbe
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    Port                            : 80
data:    Interval in seconds             : 15
data:    Number of probes                : 4
info:    network lb probe create command OK
```

여기서는 상태 검사 간격으로 15초를 지정했습니다. 우리는 최대 4 개 (1 분) 해당 hello 호스트가 더 이상 작동 간주할 hello 부하 분산 장치 프로브 누락 될 수 없습니다.

## <a name="verify-hello-load-balancer"></a>Hello 부하 분산 장치를 확인 합니다.
이제 hello 부하 분산 장치 구성이 수행 됩니다. 수행한 hello 단계는 다음과 같습니다.

1. 부하 분산 장치를 만들었습니다.
2. 프런트 엔드 IP 풀을 만들고 공용 IP tooit 할당 했습니다.
3. VM을 연결할 수 있는 백 엔드 IP 풀을 만들었습니다.
4. 관리 및 웹 앱에 대 한 TCP 포트 80을 허용 하는 규칙에 대 한 SSH toohello Vm을 허용 하는 NAT 규칙을 만들었습니다.
5. 상태 프로브 tooperiodically 검사 hello Vm을 추가 했습니다. 이 상태 프로브를 사용 하면 사용자가 더 이상 작동 또는 콘텐츠를 처리 하는 VM tooaccess를 시도 하지 마십시오.

이제 부하 분산 장치가 어떻게 표시되는지 살펴보겠습니다.

```azurecli
azure network lb show --resource-group myResourceGroup \
  --name myLoadBalancer --json | jq '.'
```

출력:

```json
{
  "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH1",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4222,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    },
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH2",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4223,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    }
  ],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "inboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        },
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleWeb",
      "provisioningState": "Succeeded",
      "enableFloatingIP": false,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "backendAddressPool": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
      },
      "protocol": "Tcp",
      "loadDistribution": "Default",
      "mySubnetPort": 80,
      "backendPort": 80,
      "idleTimeoutInMinutes": 4
    }
  ],
  "probes": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myHealthProbe",
      "provisioningState": "Succeeded",
      "numberOfProbes": 4,
      "intervalInSeconds": 15,
      "port": 80,
      "protocol": "Tcp",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/probes/myHealthProbe"
    }
  ]
}
```

## <a name="create-an-nic-toouse-with-hello-linux-vm"></a>Linux VM hello를 사용 하 여 NIC toouse 만들기
Nic는 tootheir 사용 규칙을 적용할 수 있으므로 프로그래밍 방식으로 사용할 수 있습니다. 2개 이상 있을 수도 있습니다. 다음 예제 hello `azure network nic create` 명령, hello NIC toohello 부하 백 엔드 IP 풀을 연결 하 고 NAT 규칙 toopermit SSH 트래픽 hello와 연결 합니다.

Hello 대체 `#####-###-###` 섹션에서는 사용자 고유의 Azure 구독 id 구독 ID의 hello 출력에서 설명한 `jq` 만들면 hello 리소스를 검사 하는 경우. `azure account list`를 사용하여 구독 ID를 볼 수도 있습니다.

hello 다음 예제에서는 명명 된 NIC `myNic1`:

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic1 \
  --lb-address-pool-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
```

출력:

```azurecli
info:    Executing command network nic create
+ Looking up hello subnet "mySubnet"
+ Looking up hello network interface "myNic1"
+ Creating network interface "myNic1"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1
data:    Name                            : myNic1
data:    Type                            : Microsoft.Network/networkInterfaces
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Enable IP forwarding            : false
data:    IP configurations:
data:      Name                          : Nic-IP-config
data:      Provisioning state            : Succeeded
data:      Private IP address            : 192.168.1.4
data:      Private IP allocation method  : Dynamic
data:      Subnet                        : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:      Load balancer backend address pools:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
data:      Load balancer inbound NAT rules:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
data:
info:    network nic create command OK
```

Hello 리소스를 직접 검사 하 여 hello 세부 정보를 볼 수 있습니다. Hello를 사용 하 여 hello 리소스를 검사할 `azure network nic show` 명령:

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
```

출력:

```json
{
  "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
  "provisioningState": "Succeeded",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1",
  "name": "myNic1",
  "type": "Microsoft.Network/networkInterfaces",
  "location": "westeurope",
  "ipConfigurations": [
    {
      "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1/ipConfigurations/Nic-IP-config",
      "loadBalancerBackendAddressPools": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
        }
      ],
      "loadBalancerInboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        }
      ],
      "privateIPAddress": "192.168.1.4",
      "privateIPAllocationMethod": "Dynamic",
      "subnet": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
      },
      "provisioningState": "Succeeded",
      "name": "Nic-IP-config"
    }
  ],
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": []
  },
  "enableIPForwarding": false,
  "resourceGuid": "a20258b8-6361-45f6-b1b4-27ffed28798c"
}
```

이제 우리 만들 tooour 백 엔드 IP 풀에서 다시 연결 하는 두 번째 NIC hello 합니다. 이 시간 hello 두 번째 NAT 규칙에는 SSH 트래픽을 허용 합니다. hello 다음 예제에서는 명명 된 NIC `myNic2`:

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic2 \
  --lb-address-pool-ids  /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2
```

## <a name="create-a-network-security-group-and-rules"></a>네트워크 보안 그룹 및 규칙 만들기
네트워크 보안 그룹을 생성 하 고 제어 하는 인바운드 규칙 hello 이제 toohello NIC. 액세스 네트워크 보안 그룹에 적용 된 tooa NIC 또는 서브넷 수 있습니다. Vm에 내부 및 외부로 트래픽 규칙 toocontrol hello 흐름을 정의 합니다. hello 다음 예제에서는 네트워크 보안 그룹을 만든 라는 `myNetworkSecurityGroup`:

```azurecli
azure network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

Hello NSG tooallow hello에 대 한 인바운드 규칙을 추가 해 보겠습니다 인바운드 포트 22 (toosupport SSH)에 연결 합니다. hello 다음 예제는 규칙을 만들고 라는 `myNetworkSecurityGroupRuleSSH` tooallow TCP 포트 22에서:

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1000 --destination-port-range 22 --access allow \
  --name myNetworkSecurityGroupRuleSSH
```

이제 hello NSG tooallow hello에 대 한 인바운드 규칙을 추가 해 보겠습니다 인바운드 포트 80 (toosupport 웹 트래픽의 경우)에 연결 합니다. hello 다음 예제는 규칙을 만들고 라는 `myNetworkSecurityGroupRuleHTTP` tooallow 포트 80에 TCP:

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1001 --destination-port-range 80 --access allow \
  --name myNetworkSecurityGroupRuleHTTP
```

> [!NOTE]
> hello 인바운드 규칙은 인바운드 네트워크 연결에 대 한 필터입니다. 이 예제에서는 hello NSG toohello 우리의 VM에서 모든 요청 tooport 22 toohello NIC 통해 전달 되도록 즉 Vm 가상 NIC를 바인딩할 했습니다. 이것은 끝점이 아닌 네트워크 연결에 대한 인바운드 규칙으로, 클래식 배포와 관련이 있습니다. 포트 tooopen hello 남겨 두어야 `--source-port-range` 도 '\*' (hello 기본값) tooaccept 인바운드 요청에서 **모든** 포트를 요청 합니다. 포트는 일반적으로 동적입니다.
>
>

## <a name="bind-toohello-nic"></a>Toohello NIC에 바인딩
Hello NSG toohello Nic에 바인딩하십시오. 필요 tooconnect 우리의 Nic 우리의 네트워크 보안 그룹과 합니다. 두 명령 모두 우리의 Nic toohook를 실행 합니다.

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
  --network-security-group-name myNetworkSecurityGroup
```

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic2 \
  --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-an-availability-set"></a>가용성 집합 만들기
가용성 집합은 장애 도메인 및 업그레이드 도메인에 걸쳐 VM을 분산하는 데 유용합니다. VM의 가용성 집합을 만들겠습니다. hello 다음 예제에서는 가용성 명명 된 집합 `myAvailabilitySet`:

```azurecli
azure availset create --resource-group myResourceGroup --location westeurope
  --name myAvailabilitySet
```

장애 도메인은 공통의 전원 및 네트워크 스위치를 공유하는 가상 컴퓨터 그룹을 정의합니다. 기본적으로 가용성 집합 내에서 구성 된 가상 컴퓨터를 hello toothree 오류 도메인을 걸쳐 분리 되어 있습니다. hello 개념은 이러한 오류 도메인 중 하나에 하드웨어 문제가 있는 응용 프로그램을 실행 하는 모든 VM에 영향을 주지 않습니다. Azure 자동으로 Vm hello 오류 도메인 때 배포 가용성 집합에 배치 합니다.

업그레이드 도메인 hello에서 다시 부팅 해야 하는 기본 실제 하드웨어와 가상 컴퓨터 그룹을 나타내는 동시 합니다. 업그레이드 도메인은 다시 부팅 하는 hello 순서 수 순차적 계획 된 유지 관리 하는 동안 있지만 한 번에 하나의 업그레이드를 다시 부팅 합니다. 또한 Azure는 가용성 집합에 VM을 배치할 때 VM을 업그레이드 도메인에 자동으로 분산합니다.

에 대해 자세히 알아보세요 [Vm의 가용성을 hello 관리](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

## <a name="create-hello-linux-vms"></a>Hello Linux Vm 만들기
저장소 및 네트워크 리소스를 hello toosupport 인터넷에서 액세스할 수 있는 Vm 만들었습니다. 이제 해당 VM을 만들고 암호 없이 SSH 키를 사용하여 VM을 보호하겠습니다. 이 예에서 여기 toocreate Ubuntu VM hello에 따라 가장 최근의 LTS 합니다. [Azure VM 이미지 찾기](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에 설명된 대로 `azure vm image list`를 사용하여 해당 이미지 정보를 찾을 것입니다.

Hello 명령을 사용 하 여 이미지를 선택 했습니다 `azure vm image list westeurope canonical | grep LTS`합니다. 이 경우 `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`을 사용합니다. Hello 마지막 필드에 대 한 전달 `latest` hello 미래에 항상 구했습니다 hello 가장 최근 빌드 수 있도록 합니다. (사용 하 여 hello 문자열은 `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).

다음 단계는 사용자가 만든 이미 친숙 한 tooanyone는 ssh rsa 공개 키와 개인 키 쌍으로 연결 Linux 또는 Mac에서 사용 하 여 **붙여넣으세요-t rsa-b 2048**합니다. `~/.ssh` 디렉터리에 인증서 키 쌍이 없으면 다음과 같이 만들 수 있습니다.

* Hello를 사용 하 여 자동으로 `azure vm create --generate-ssh-keys` 옵션입니다.
* 사용 하 여 수동으로 [hello 지침 toocreate로 직접](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

Hello 또는 사용할 수 있습니다 `--admin-password` 메서드 tooauthenticate hello VM 후 SSH 연결에 만들어집니다. 이 메서드는 일반적으로 보안 수준이 낮습니다.

모든 리소스와 정보를 hello 함께 전환 하 여 hello VM 만듭니다 `azure vm create` 명령:

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM1 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic1 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

출력:

```azurecli
info:    Executing command vm create
+ Looking up hello VM "myVM1"
info:    Verifying hello public key SSH file: /home/ahmet/.ssh/id_rsa.pub
info:    Using hello VM Size "Standard_DS1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Looking up hello storage account mystorageaccount
+ Looking up hello availability set "myAvailabilitySet"
info:    Found an Availability set "myAvailabilitySet"
+ Looking up hello NIC "myNic1"
info:    Found an existing NIC "myNic1"
info:    Found an IP configuration with virtual network subnet id "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet" in hello NIC "myNic1"
info:    This is an NIC without publicIP configured
info:    hello storage URI 'https://mystorageaccount.blob.core.windows.net/' will be used for boot diagnostics settings, and it can be overwritten by hello parameter input of '--boot-diagnostics-storage-uri'.
info:    vm create command OK
```

기본 SSH 키를 사용 하 여 tooyour VM을 즉시 연결할 수 있습니다. Hello 부하 분산 장치를 통해 전달할 것임 이후 hello 적절 한 포트를 지정 하는 있는지 확인 합니다. (이 첫 번째 VM에 대 한 설정 hello NAT 규칙 tooforward 포트 4222 tooour VM.)

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222
```

출력:

```bash
hello authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

Hello에 두 번째 VM을 만들 동일한 방식으로:

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM2 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic2 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

이제 hello를 사용할 수 있습니다 및 `azure vm show myResourceGroup myVM1` 위에서 만든 tooexamine 명령입니다. 이 시점에는 암호가 사용되지 않도록 설정되어 있으므로 Azure의 부하 분산 장치에서 Ubuntu VM을 실행 중이며 보유하고 있는 SSH 키 쌍을 사용하여 로그인할 수 있습니다. 인스턴스를 설치할지 nginx httpd, 웹 앱을 배포 및 hello 트래픽을 볼 hello Vm의 부하 분산 장치 tooboth hello 통해 흐름.

```azurecli
azure vm show --resource-group myResourceGroup --name myVM1
```

출력:

```azurecli
info:    Executing command vm show
+ Looking up hello VM "TestVM1"
+ Looking up hello NIC "myNic1"
data:    Id                              :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Succeeded
data:    Name                            :myVM1
data:    Location                        :westeurope
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :16.04.0-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clib45a8b650f4428a1-os-1471973896525
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/clib45a8b650f4428a1-os-1471973896525.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-24-D4-AA
data:          Provisioning State        :Succeeded
data:          Name                      :LmyNic1
data:          Location                  :westeurope
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://mystorageaccount.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm show command OK

```


## <a name="export-hello-environment-as-a-template"></a>서식 파일로 내보내기 hello 환경
Hello로 추가 개발 환경을 toocreate 싶은 경우이 환경으로 작성 한 했으므로 동일한 매개 변수 또는 일치 하는 프로덕션 환경? 리소스 관리자는 사용자 환경에 대 한 모든 hello 매개 변수를 정의 하는 JSON 템플릿을 사용 합니다. 이 JSON 템플릿을 참조하여 전체 환경을 빌드합니다. 할 수 있습니다 [JSON 서식 파일을 수동으로 빌드할](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 사용자에 대 한 기존 환경 toocreate hello JSON 템플릿 내보내기:

```azurecli
azure group export --name myResourceGroup
```

이 명령은 만듭니다 hello `myResourceGroup.json` 현재 작업 디렉터리에 파일입니다. 이 템플릿에서 환경을 만들 때 hello 부하 분산 장치, 네트워크 인터페이스 또는 Vm에 대 한 hello 이름을 포함 한 모든 hello 리소스 이름을 하 라는 메시지가 표시 됩니다. Hello를 추가 하 여 템플릿 파일에 이러한 이름을 채울 수 있습니다 `-p` 또는 `--includeParameterDefaultValue` 매개 변수 toohello `azure group export` 명령 앞에 나온입니다. JSON 템플릿 toospecify hello 리소스 이름의 편집 또는 [parameters.json 파일을 만들](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) hello 리소스 이름을 지정 하는 합니다.

서식 파일에서 환경 toocreate:

```azurecli
azure group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

Tooread 경우가 [방법에 대 한 자세한 템플릿에서 toodeploy](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. Tooincrementally 업데이트 환경 hello 매개 변수 파일을 사용 하 고 단일 저장소 위치에서 서식 파일에 액세스 하는 방법에 대해 알아봅니다.

## <a name="next-steps"></a>다음 단계
이제 준비 toobegin 여러 네트워킹 구성 요소 및 Vm을 사용 합니다. 여기 도입 hello 핵심 구성 요소를 사용 하 여이 샘플 환경 toobuild 응용 프로그램에 사용할 수 있습니다.
