---
title: "aaaAzure 가상 네트워크와 Linux 가상 컴퓨터 | Microsoft Docs"
description: "자습서-hello Azure CLI를 사용 하 여 Azure 가상 네트워크와 Linux 가상 컴퓨터 관리"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 57e6bd4de16f0e31d53dc67bf50dc5730d43712b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-linux-virtual-machines-with-hello-azure-cli"></a>Hello Azure CLI를 사용 하 여 Azure 가상 네트워크와 Linux 가상 컴퓨터 관리

Azure 가상 컴퓨터는 내부 및 외부 네트워크 통신에서 Azure 네트워킹을 사용합니다. 이 자습서에서는 두 개의 가상 컴퓨터를 배포하고 이러한 VM에 Azure 네트워킹을 구성하기 위해 단계별로 안내합니다. 이 자습서에서는 hello 예제 응용 프로그램 hello 자습서에서 배포 되지 않은 있지만 hello Vm으로 데이터베이스 백 엔드, 웹 응용 프로그램을 호스팅하는 가정 합니다. 이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * 가상 네트워크 배포
> * 가상 네트워크 내에 서브넷 만들기
> * 가상 컴퓨터 tooa 서브넷 연결
> * 가상 컴퓨터 공용 IP 주소 관리
> * 들어오는 인터넷 트래픽 보호
> * VM tooVM 트래픽을 보호합니다


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 자습서를 사용 하려면 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

## <a name="vm-networking-overview"></a>VM 네트워킹 개요

Azure 가상 네트워크는 가상 컴퓨터 간에 안전한 네트워크 연결을 설정, 인터넷 및 Azure SQL 데이터베이스와 같은 다른 Azure 서비스 hello 합니다. 가상 네트워크는 서브넷이라는 논리적 세그먼트로 구분됩니다. 서브넷에서 사용 되 toocontrol 네트워크 흐름 및 보안 경계로 합니다. VM을 배포할 때는 일반적으로 연결 된 tooa 서브넷이 가상 네트워크 인터페이스를 포함 합니다.

## <a name="deploy-virtual-network"></a>가상 네트워크 배포

이 자습서에서는 두 개의 서브넷이 있는 단일 가상 네트워크를 만듭니다. 서브넷 하나는 웹 응용 프로그램을 호스트하기 위한 프런트 엔드 서브넷이고 다른 하나는 데이터베이스 서버를 호스트하기 위한 백 엔드 서브넷입니다.

가상 네트워크를 만들려면 먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다. hello 다음 예제에서는 명명 된 리소스 그룹 *myRGNetwork* hello eastus 위치에 있습니다.

```azurecli-interactive 
az group create --name myRGNetwork --location eastus
```

### <a name="create-virtual-network"></a>가상 네트워크 만들기

Hello us [az 네트워크 vnet 만들기](/cli/azure/network/vnet#create) 명령 toocreate 가상 네트워크입니다. 이 예제에서는 hello 네트워크 이름은 *mvVnet* 의 주소 접두사를 지정 하 고 *10.0.0.0/16*합니다. 또한 서브넷은 *mySubnetFrontEnd* 이름과 *10.0.1.0/24* 접두사로 만들어집니다. 이 자습서의 뒷부분에 나오는 프런트 엔드 VM에 연결 된 toothis 서브넷은 합니다. 

```azurecli-interactive 
az network vnet create \
  --resource-group myRGNetwork \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnetFrontEnd \
  --subnet-prefix 10.0.1.0/24
```

### <a name="create-subnet"></a>서브넷 만들기

새 서브넷 hello를 사용 하 여 toohello 가상 네트워크 추가 [az 네트워크 vnet 서브넷 만들기](/cli/azure/network/vnet/subnet#create) 명령입니다. 이 예제에서는 hello 서브넷 이름이 *mySubnetBackEnd* 의 주소 접두사를 지정 하 고 *10.0.2.0/24*합니다. 이 서브넷은 모든 백 엔드 서비스에서 사용됩니다.

```azurecli-interactive 
az network vnet subnet create \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --address-prefix 10.0.2.0/24
```

이 시점에서 네트워크가 만들어져 하나는 프론트 엔드 서비스를, 다른 하나는 백 엔드 서비스를 위한 두 개의 서브넷으로 분할되었습니다. Hello 다음 섹션에서 가상 컴퓨터 생성 되 고 연결 된 toothese 서브넷.

## <a name="understand-public-ip-address"></a>공용 IP 주소 이해

공용 IP 주소 허용 toobe Azure 리소스에 액세스할 수 있는 인터넷 hello 합니다. Hello 자습서의이 섹션에서는 VM에 공용 IP로 toowork 해결 하는 방법을 toodemonstrate를 만들어집니다.

### <a name="allocation-method"></a>할당 방법

공용 IP 주소는 동적 또는 정적으로 할당할 수 있습니다. 기본적으로 공용 IP 주소는 동적으로 할당됩니다. VM 할당을 취소하는 경우 동적 IP 주소도 해제됩니다. 이 동작은 hello IP 주소 toochange VM 할당 취소를 포함 하는 작업 중.

hello 할당 방법 toostatic를 설정할 수 tooa VM에 할당 된 내용이 hello IP 주소 상태를 유지 하는 할당 취소 된 상태 중에 있습니다. 정적으로 할당 된 IP 주소를 사용 하는 경우에 자체 hello IP 주소를 지정할 수 없습니다. 대신 사용 가능한 주소 풀에서 할당됩니다.

### <a name="dynamic-allocation"></a>동적 할당

Hello로 VM을 만들 때 [az vm 만들기](/cli/azure/vm#create) 명령, hello 기본 공용 IP 주소 할당 방법은 동적입니다. 다음 예제는 hello, VM 동적 IP 주소로 만들어집니다. 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myFrontEndVM \
  --vnet-name myVnet \
  --subnet mySubnetFrontEnd \
  --nsg myNSGFrontEnd \
  --public-ip-address myFrontEndIP \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="static-allocation"></a>정적 할당

Hello를 사용 하 여 가상 컴퓨터를 만들 때 [az vm 만들기](/cli/azure/vm#create) 명령에서 hello 포함 `--public-ip-address-allocation static` 인수 tooassign 고정 공용 IP 주소입니다. 그러나이 작업은이 자습서에서는 제공 되지 않습니다 hello 다음 섹션에 동적으로 할당 된 IP 주소에는 변경 된 tooa 정적으로 할당 된 주소입니다. 

### <a name="change-allocation-method"></a>할당 방법 변경

hello IP 주소 할당 방법은 hello를 사용 하 여 변경할 수 있습니다 [az 네트워크 공개 ip 업데이트](/cli/azure/network/public-ip#update) 명령입니다. 이 예제에서는 hello 프런트 엔드 VM 변경 된의 IP 주소 할당 방법은 hello toostatic 합니다.

첫째, hello VM 할당이 취소 되었습니다.

```azurecli-interactive 
az vm deallocate --resource-group myRGNetwork --name myFrontEndVM
```

사용 하 여 hello [az 네트워크 공개 ip 업데이트가](/cli/azure/network/public-ip#update) tooupdate hello 할당 방법 명령입니다. 이 경우 hello `--allocation-method` 너무 설정 되어*정적*합니다.

```azurecli-interactive 
az network public-ip update --resource-group myRGNetwork --name myFrontEndIP --allocation-method static
```

Hello VM을 시작 합니다.

```azurecli-interactive 
az vm start --resource-group myRGNetwork --name myFrontEndVM --no-wait
```

### <a name="no-public-ip-address"></a>공용 IP 주소 없음

종종 VM 하지 않아도 toobe로 액세스할 수 있는 인터넷 hello 합니다. 공용 IP 주소를 사용 하 여 hello 없이 VM toocreate `--public-ip-address ""` 인수 빈 집합이 큰따옴표를 사용 합니다. 이 구성은 이 자습서의 뒷부분에서 설명합니다.

## <a name="secure-network-traffic"></a>네트워크 트래픽 보안

네트워크 보안 그룹 NSG ()를 허용 하거나 거부할 네트워크 트래픽 tooresources tooAzure 가상 네트워크 (VNet) 연결 하는 보안 규칙 목록이 포함 되어 있습니다. Nsg 연결된 toosubnets 또는 개별 네트워크 인터페이스 수 있습니다. NSG는 네트워크 인터페이스와 연결 되 면 hello 관련 VM에만 적용 됩니다. NSG 연결된 tooa 서브넷 이면 tooall 리소스 연결 된 toohello 서브넷 hello 규칙에 적용 됩니다. 

### <a name="network-security-group-rules"></a>네트워크 보안 그룹 규칙

NSG 규칙은 트래픽이 허용되거나 거부되는 네트워킹 포트를 정의합니다. 특정 시스템 또는 서브넷 간의 트래픽 제어가 되도록 hello 규칙에서 원본 및 대상 IP 주소 범위를 포함할 수 있습니다. NSG 규칙에는 우선 순위(1-4096 사이)도 포함됩니다. 규칙의 우선 순위 hello 순서로 평가 됩니다. 우선 순위가 100인 규칙은 우선 순위가 200인 규칙보다 먼저 평가됩니다.

모든 NSG에는 기본 규칙 집합이 포함됩니다. hello 기본 규칙은 삭제할 수 있지만 여 hello 만드는 규칙을 재정의할 수 hello 가장 낮은 우선 순위를 할당 되었으므로 있습니다.

- **가상 네트워크:** 가상 네트워크에서 시작하고 끝나는 트래픽은 인바운드와 아웃바운드 방향 둘 다에서 허용됩니다.
- **인터넷:** 아웃바운드 트래픽은 허용되지만 인바운드 트래픽은 차단됩니다.
- **부하 분산 장치** -의 Vm 및 역할 인스턴스 수 있도록 Azure의 부하 분산 장치 tooprobe hello 상태입니다. 부하 분산된 집합을 사용하지 않는 경우 이 규칙을 재정의할 수 있습니다.

### <a name="create-network-security-groups"></a>네트워크 보안 그룹 만들기

네트워크 보안 그룹에서 만들 수 hello 동일 hello를 사용 하는 VM으로 시간 [az vm 만들기](/cli/azure/vm#create) 명령입니다. 이렇게 할 경우 hello NSG hello Vm 네트워크 인터페이스와 연결 되며 NSG 규칙은 포트에서 자동으로 만들어진 tooallow 트래픽을 *22* 소스의 합니다. 이 자습서의 앞부분에 나오는 프런트 엔드 NSG를 사용 하 여 자동 만든 hello 프런트 엔드 VM hello 합니다. 22 포트에 대한 NSG 규칙도 자동으로 만들어졌습니다. 

일부 경우에는 것이 유용한 toopre-때 기본 SSH 규칙을 만들지 때 hello NSG 연결된 tooa 서브넷 해야 등 NSG를 만듭니다. 

사용 하 여 hello [az 네트워크 nsg 만들기](/cli/azure/network/nsg#create) 명령 toocreate 네트워크 보안 그룹입니다.

```azurecli-interactive 
az network nsg create --resource-group myRGNetwork --name myNSGBackEnd
```

Hello NSG tooa 네트워크 인터페이스를 연결 하는 대신 서브넷과 연결 됩니다. 이 구성에서는 VM에 연결 된 toohello 서브넷 hello NSG 규칙을 상속 합니다.

명명 된 hello 기존 서브넷 업데이트 *mySubnetBackEnd* 와 새 NSG hello 합니다.

```azurecli-interactive 
az network vnet subnet update \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --network-security-group myNSGBackEnd
```

이제 연결 된 toohello 가상 컴퓨터를 만들 *mySubnetBackEnd*합니다. 해당 hello 확인 `--nsg` 인수에 빈 큰따옴표의 값입니다. NSG는 VM hello를 사용 하 여 만든 toobe가 필요 하지 않습니다. hello VM 백 엔드 NSG를 미리 만들어 hello로 보호 되는 연결 된 toohello 백 엔드 서브넷입니다. 이 NSG toohello VM 적용 됩니다. 또한 해당 hello 여기 확인 `--public-ip-address` 인수에 빈 큰따옴표의 값입니다. 이 구성은 공용 IP 주소 없이 VM을 만듭니다. 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myBackEndVM \
  --vnet-name myVnet \
  --subnet mySubnetBackEnd \
  --public-ip-address "" \
  --nsg "" \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="secure-incoming-traffic"></a>들어오는 트래픽 보호

Hello 프런트 엔드 VM을 만들 때 NSG 규칙이 포트 22에서 들어오는 트래픽은 tooallow를 만들었습니다. 이 규칙은 SSH 연결 toohello VM 허용 합니다. 이 예제에서 트래픽은 *80* 포트에서도 허용되어야 합니다. 이 구성은 hello VM에 액세스 하는 웹 응용 프로그램 toobe를 허용 합니다.

사용 하 여 hello [az 네트워크 nsg 규칙 만들기](/cli/azure/network/nsg/rule#create) 명령 toocreate 포트에 대 한 규칙 *80*합니다.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGFrontEnd \
  --name http \
  --access allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range 80
```

hello 프런트 엔드 VM이 이제만 액세스할 수 있는 포트에서 *22* 및 포트 *80*합니다. Hello 네트워크 보안 그룹에서 다른 들어오는 트래픽은 모두 차단 됩니다. 유용한 toovisualize hello NSG 규칙 구성을 수도 있습니다. Hello로 반환 hello NSG 규칙 구성을 [az 네트워크 규칙 목록](/cli/azure/network/nsg/rule#list) 명령입니다. 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGFrontEnd --output table
```

출력:

```azurecli-interactive 
Access    DestinationAddressPrefix      DestinationPortRange  Direction    Name                 Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -----------------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                                               22  Inbound      default-allow-ssh        1000  Tcp         Succeeded            myRGNetwork      *                      *
Allow     *                                               80  Inbound      http                      200  Tcp         Succeeded            myRGNetwork      *                      *
```

### <a name="secure-vm-toovm-traffic"></a>VM tooVM 트래픽을 보호합니다

네트워크 보안 그룹 규칙은 VM 간에도 적용할 수 있습니다. 이 예제에 대 한 프런트 엔드 VM으로 toocommunicate 필요한 hello hello 포트에서 백 엔드 VM *22* 및 *3306*합니다. 이 구성은 SSH 연결을 허용 프런트 엔드 VM hello 고도 백엔드로 MySQL 데이터베이스와 프런트 엔드 VM toocommunicate hello에 응용 프로그램을 허용 합니다. 기타 모든 트래픽에 hello 프런트 엔드 및 백 엔드 가상 컴퓨터 간에 차단 해야 합니다.

사용 하 여 hello [az 네트워크 nsg 규칙 만들기](/cli/azure/network/nsg/rule#create) 명령 toocreate 포트 22에 대 한 규칙입니다. 해당 hello 확인 `--source-address-prefix` 의 값을 지정 하는 인수 *10.0.1.0/24*합니다. 이 구성을 통해 hello 프런트 엔드 서브넷의 트래픽만 hello NSG 통해 허용 됩니다.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name SSH \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 100 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "22"
```

이제 3306 포트에서 MySQL 트래픽에 대한 규칙을 추가합니다.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name MySQL \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "3306"
```

마지막으로, Nsg 허용 하는 기본 규칙 때문에 간의 모든 트래픽이 Vm hello에 동일한 VNet 규칙을 만들 수 있습니다 백 엔드 Nsg tooblock hello에 대 한 모든 트래픽이 합니다. 확인 여기 해당 hello `--priority` 의 값이 지정 되 *300*, MySQL 및 NSG 규칙을 hello 둘 다 낮은 합니다. 이 구성을 통해 SSH 및 MySQL 트래픽이 hello NSG 통해 여전히 허용 됩니다.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name denyAll \
  --access Deny \
  --protocol Tcp \
  --direction Inbound \
  --priority 300 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "*"
```

hello 백 엔드 VM이 이제만 액세스할 수 있는 포트에서 *22* 및 포트 *3306* hello 프런트 엔드 서브넷에서. Hello 네트워크 보안 그룹에서 다른 들어오는 트래픽은 모두 차단 됩니다. 유용한 toovisualize hello NSG 규칙 구성을 수도 있습니다. Hello로 반환 hello NSG 규칙 구성을 [az 네트워크 규칙 목록](/cli/azure/network/nsg/rule#list) 명령입니다. 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGBackEnd --output table
```

출력:

```azurecli-interactive 
Access    DestinationAddressPrefix    DestinationPortRange    Direction    Name       Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                           22                      Inbound      SSH             100  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Allow     *                           3306                    Inbound      MySQL           200  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Deny      *                           *                       Inbound      denyAll         300  Tcp         Succeeded            myRGNetwork      *                      *
```

## <a name="next-steps"></a>다음 단계

이 자습서에서 만든 및 보안 관련된 toovirtual 컴퓨터와 Azure 네트워크입니다. 다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * 가상 네트워크 배포
> * 가상 네트워크 내에 서브넷 만들기
> * 가상 컴퓨터 tooa 서브넷 연결
> * 가상 컴퓨터 공용 IP 주소 관리
> * 들어오는 인터넷 트래픽 보호
> * VM tooVM 트래픽을 보호합니다

Azure 백업을 사용 하 여 가상 컴퓨터에서 데이터를 보호 하는 방법에 대 한 다음 자습서 toolearn toohello를 진행 합니다. 

> [!div class="nextstepaction"]
> [Azure에서 Linux 가상 컴퓨터 백업](./tutorial-backup-vms.md)
