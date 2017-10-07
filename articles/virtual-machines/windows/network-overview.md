---
title: "aaaVirtual 네트워크와 Azure의 Windows 가상 컴퓨터 | Microsoft Docs"
description: "Azure에서 Windows 가상 컴퓨터를 만드는 기본적인 toohello와 관련 네트워킹에 대해 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 5493e9f7-7d45-4e98-be9a-657a53708746
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: e28a4782f9f6c69f6101e45dbb560ccd694a1e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-networks-and-windows-virtual-machines-in-azure"></a>Azure의 가상 네트워크 및 Windows 가상 컴퓨터 

Azure VM(가상 컴퓨터)을 만들 때 [VNet(가상 네트워크)](../../virtual-network/virtual-networks-overview.md)을 만들거나 기존 VNet을 사용해야 합니다. Vm에 의도 한 toobe hello VNet에서 액세스 하는 방법을 toodecide를 해야 합니다. 반드시 너무[리소스를 만들기 전에 계획](../../virtual-network/virtual-network-vnet-plan-design-arm.md) hello를 이해 하 고 [네트워킹 리소스의 한계](../../azure-subscription-service-limits.md#networking-limits)합니다.

다음 그림 hello, Vm은 웹 서버 및 데이터베이스 서버로 표현 됩니다. 각 Vm 집합 tooseparate hello VNet 서브넷에 할당 됩니다.

![Azure 가상 네트워크](./media/network-overview/vnetoverview.png)

VM을 만들 때 hello VNet을 만들 수 있습니다를 VM을 만들기 전에 하거나 VNet을 만들 수 있습니다. VNet은 직접 만들거나 VM을 만들 때 만들어집니다.

이러한 리소스 만들어야 toosupport 통신은 VM으로:

- 네트워크 인터페이스
- IP 주소
- 가상 네트워크 및 서브넷

또한 toothose 기본 리소스를 선택적 이러한 리소스를 고려해 야 하면:

- 네트워크 보안 그룹
- 부하 분산 장치 

## <a name="network-interfaces"></a>네트워크 인터페이스

A [네트워크 인터페이스 (NIC)](../../virtual-network/virtual-network-network-interface.md) VM 및 가상 네트워크 (VNet) 간의 hello를 상호 연결 됩니다. VM 하나 이상 NIC 하지만 둘 이상 hello 만드는 VM의 hello 크기에 따라 있을 수 있습니다. [Azure의 가상 컴퓨터 크기](sizes.md)에서 각 VM 크기가 지원하는 NIC 수에 대해 알아봅니다. 

둘 이상의 NIC 사용 하 여 VM toocreate 원하는 hello VM 두 개 이상 있는 만들어야 합니다.  만든 후 다른 Nic hello VM 크기에서 지원 되는 toohello 번호를 추가할 수 있습니다 하지만 추가 Nic tooa만 하나를 사용 하 여 만든 VM을 추가할 수 없습니다, 그리고 Nic 개수에 관계 없이 hello v M 크기를 지원 합니다. 

Hello VM tooan 가용성 집합에 추가 되 면 하나 또는 여러 개의 Nic hello 가용성 집합 내에서 모든 Vm에 있어야 합니다. 둘 이상의 NIC 아닌 함께 Vm toohave hello Nic의 동일한 개수가 되지만 모든 적어도 두 개 필요 합니다.

VM에 있어야 합니다. 각 연결 된 NIC tooa hello VM으로 동일한 위치 및 구독 hello 합니다. 각 NIC 연결된 tooa VNet에에서 있는 hello 동일 해야 합니다. Azure 위치와 NIC. hello 구독 NIC를 만든 후에, 연결 된 hello 서브넷을 변경할 수 있지만 hello VNet에 연결 되어 변경할 수 없습니다.  각 NIC tooa VM hello VM 삭제 될 때까지 변경 되지 않는 MAC 주소 할당을 연결 합니다.

이 표에서 toocreate 네트워크 인터페이스를 사용할 수 있는 hello 메서드를 보여 줍니다.

| 메서드 | 설명 |
| ------ | ----------- |
| Azure portal | Hello Azure 포털에서에서 VM을 만들 때 네트워크 인터페이스 (별도로 만들 NIC를 사용할 수 없음)를 자동으로 만들어집니다. hello 포털 하나만 NIC.를 사용 하 여 VM을 만듭니다. Toocreate 둘 이상의 NIC 사용 하 여 VM을 하려는 경우 다른 방법으로 만들어야 합니다. |
| [Azure PowerShell](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) | 사용 하 여 [새로 AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) hello로 **-PublicIpAddressId** 매개 변수 tooprovide hello 식별자 이전에 만든 hello 공용 IP 주소입니다. |
| [Azure CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md) | tooprovide hello 식별자의 hello 공용 IP 주소에 사용 하 여 이전에 만든된 [az 네트워크 nic 만들](https://docs.microsoft.com/cli/azure/network/nic#create) hello로 **-공용 ip 주소** 매개 변수입니다. |
| [템플릿](../../virtual-network/virtual-network-deploy-multinic-arm-template.md) | 템플릿을 사용하여 네트워크 인터페이스를 배포하기 위한 지침으로 [공용 IP 주소를 사용하는 Virtual Network의 네트워크 인터페이스](https://github.com/Azure/azure-quickstart-templates/tree/master/101-nic-publicip-dns-vnet)를 사용합니다. |

## <a name="ip-addresses"></a>IP 주소 

이러한 유형의 할당할 수 [IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) tooa Azure에서 NIC:

- **공용 IP 주소** -toocommunicate 인바운드 및 아웃 바운드 NAT 네트워크 주소 변환 ()) (없이 사용 되는 hello로 인터넷와 다른 Azure 리소스로 연결 되지 않은 tooa VNet입니다. 공용 IP 주소 tooa 할당 NIC은 선택 사항입니다. 공용 IP 주소에는 명목 상의 요금이 부과되며 구독당 사용할 수 있는 최대 개수가 있습니다.
- **개인 IP 주소** -VNet, 온-프레미스 네트워크 및 인터넷 (NAT)을 hello 내에서 통신에 사용 합니다. 하나 이상의 개인 IP 주소 tooa VM을 할당 해야 합니다. azure에서는 NAT에 대해 자세히 toolearn 읽을 [Azure의 아웃 바운드 연결 이해](../../load-balancer/load-balancer-outbound-connections.md)합니다.

공용 IP 주소 tooVMs 또는 인터넷 연결 부하 분산 장치를 할당할 수 있습니다. 개인 IP 주소 tooVMs 및 내부 부하 분산 장치를 할당할 수 있습니다. IP 주소 tooa 네트워크 인터페이스를 사용 하 여 VM을 할당 합니다.

IP 주소는 동적 또는 정적 tooa 리소스-을 할당 하는 데는 두 가지가 있습니다. hello 기본 할당 방법을 만들어질 때 IP 주소 할당 되지 않은 경우에 동적으로 합니다. 대신, VM을 만들거나 중지 된 VM을 시작할 때 hello IP 주소가 할당 됩니다. 중지 하거나 VM hello를 삭제할 때 hello IP 주소가 해제 됩니다. 

VM 상태를 유지 하는 hello에 대 한 tooensure hello IP 주소 같은 hello hello 할당 메서드를 명시적으로 설정할 수 있습니다, toostatic 합니다. 이 경우 IP 주소는 즉시 할당되며, 놓을 때 hello VM을 삭제 하거나 해당 할당 메서드 toodynamic를 변경 하는 경우에 합니다.
    
이 표에서 toocreate IP 주소를 사용할 수 있는 hello 메서드를 보여 줍니다.

| 메서드 | 설명 |
| ------ | ----------- |
| [Azure 포털](../../virtual-network/virtual-network-deploy-static-pip-arm-portal.md) | 기본적으로 공용 IP 주소는 동적 이며 hello 연결 된 주소 toothem hello VM은 중지 되거나 삭제 될 때 변경 될 수 있습니다. 사용 하 여 VM을 항상 hello tooguarantee hello 동일한 공용 IP 주소를 고정 공용 IP 주소를 만듭니다. 기본적으로 VM을 만들 때 hello 포털은 동적 개인 IP 주소 tooa NIC를 할당 합니다. 이 toostatic hello VM이 생성 후 변경할 수 있습니다.|
| [Azure PowerShell](../../virtual-network/virtual-network-deploy-static-pip-arm-ps.md) | 사용 하면 [새로 AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) hello로 **-AllocationMethod** 동적 또는 정적으로 매개 변수입니다. |
| [Azure CLI](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md) | 사용 하면 [az 네트워크 공용 ip 만들기](https://docs.microsoft.com/cli/azure/network/public-ip#create) hello로 **-할당 방법** 동적 또는 정적으로 매개 변수입니다. |
| [템플릿](../../virtual-network/virtual-network-deploy-static-pip-arm-template.md) | 템플릿을 사용하여 공용 IP 주소를 배포하기 위한 지침으로 [공용 IP 주소를 사용하는 Virtual Network의 네트워크 인터페이스](https://github.com/Azure/azure-quickstart-templates/tree/master/101-nic-publicip-dns-vnet)를 사용합니다. |

공용 IP 주소를 만든 후 연결할 수 있습니다 하는 VM으로 tooa NIC. 할당 하 여

## <a name="virtual-network-and-subnets"></a>가상 네트워크 및 서브넷

서브넷은 hello VNet에에서 범위의 IP 주소입니다. 조직 및 보안을 위해 VNet을 여러 서브넷으로 나눌 수 있습니다. 각 NIC는 VM에서 하나의 VNet에 연결 된 tooone 서브넷입니다. Nic 연결된 toosubnets (같거나 다른) VNet 내에서 추가 구성 없이 서로 통신할 수 있습니다.

VNet을 설정할 때 hello 사용 가능한 주소 공간 및 서브넷을 포함 하 여 hello 토폴로지를 지정 합니다. Hello VNet 이면 연결 된 toobe tooother Vnet 또는 온-프레미스 네트워크와 겹치지 않는 주소 범위를 선택 해야 합니다. hello IP 주소는 개인 및 hello 10.0.0.0/8, 172.16.0.0/12, 또는 192.168.0.0/16 같은 hello routeable IP 주소에 대해서만 true가 인터넷에서에서 액세스할 수 없습니다. 이제 Azure hello 개인 VNet IP 주소 공간 내 hello VNet, 상호 연결 된 Vnet 내 및 온-프레미스 위치에서 연결할 수 있는의 일환으로 임의의 주소 범위를 처리 합니다. 

다른 사람이 hello 내부 네트워크에 대 한 책임은 조직 내에서 작업 하는 경우에 주소 공간을 선택 하기 전에 toothat 사람을 문의 해야 합니다. 겹치지 있는지 확인 하 고 toouse hello 공간 알 수 있도록 toouse hello 동일한 IP 주소 범위를 시도 하지 않습니다. 

기본적으로,는 없는 보안 경계, 서브넷 이러한 각 서브넷에 Vm tooone 대화를 나눌 수 있으므로 다른 합니다. 그러나 서브넷에서 toocontrol hello 트래픽 흐름 tooand 및 Vm에서 tooand 수 있게 하는 네트워크 보안 그룹 (Nsg)을 설정할 수 있습니다. 

이 표에 hello 메서드 toocreate VNet 및 서브넷을 사용할 수 있습니다.   

| 메서드 | 설명 |
| ------ | ----------- |
| [Azure 포털](../../virtual-network/virtual-networks-create-vnet-arm-pportal.md) | Hello 이름 hello VNet을 포함 하는 hello 리소스 그룹 이름 결합 한 것를 Azure VM을 만들 때 VNet을 만들 수 있도록 하는 경우 및 **vnet**합니다. hello 주소 공간은 10.0.0.0/24, hello 필요한 서브넷 이름이 **기본**, hello 서브넷 주소 범위는 10.0.0.0/24 및 합니다. |
| [Azure PowerShell](../../virtual-network/virtual-networks-create-vnet-arm-ps.md) | 사용 하면 [새로 AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmVirtualNetworkSubnetConfig) 및 [새로 AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmVirtualNetwork) 서브넷 및 VNet toocreate 합니다. 사용할 수도 있습니다 [추가 AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig) tooadd 서브넷 tooan 기존 VNet입니다. |
| [Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md) | hello 서브넷과 hello VNet에서 만들어진 hello 동일한 시간입니다. 제공 된 **-서브넷 이름** 매개 변수 너무[az 네트워크 vnet 만들기](https://docs.microsoft.com/cli/azure/network/vnet#create) hello 서브넷 이름의 합니다. |
| [템플릿](../../virtual-network/virtual-networks-create-vnet-arm-template-click.md) | 가장 쉬운 방법은 toocreate VNet hello 및 서브넷은 toodownload 기존 서식 파일을 같은 [두 서브넷을 사용 하 여 가상 네트워크](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets), 요구에 맞게 수정 합니다. |

## <a name="network-security-groups"></a>네트워크 보안 그룹

A [네트워크 보안 그룹 (NSG)](../../virtual-network/virtual-networks-nsg.md) 허용 하거나 네트워크 트래픽 toosubnets, Nic, 또는 둘 다 거부 하는 액세스 제어 목록 (ACL) 규칙의 목록을 포함 합니다. Nsg를 서브넷 또는 개별 Nic 연결 된 tooa 서브넷와 연결할 수 있습니다. NSG를 서브넷과 연결 되는 경우 해당 서브넷에 대 한 Vm tooall hello hello ACL 규칙이 적용 됩니다. 또한 NSG를 연결 하 여 개별 NIC 제한 될 수 있습니다 tooan 트래픽 tooa NIC. 직접

NSG에는 인바운드 및 아웃바운드의 두 가지 규칙 집합이 포함되어 있습니다. hello 우선 순위 규칙에 대 한 각 집합 내에서 고유 해야 합니다. 각 규칙에는 프로토콜, 원본 및 대상 포트 범위, 주소 접두사, 트래픽 방향, 우선 순위 및 액세스 유형에 관한 속성이 있습니다. 

모든 NSG에는 기본 규칙 집합이 포함됩니다. hello 기본 규칙은 삭제할 수 있지만 여 hello 만드는 규칙을 재정의할 수 hello 가장 낮은 우선 순위를 할당 되었으므로 있습니다. 

Hello NSG의에서 hello 네트워크 액세스 규칙이 적용 된 유일한 toothat NIC.은 NSG tooa NIC에 연결 하면 NSG가 적용 된 tooa 경우 단일 NIC에 다중 NIC VM을 그대로 트래픽 toohello 다른 Nic 합니다. 다른 Nsg tooa NIC (또는 hello 배포 모델에 따라 VM)를 연결 하 고 hello에 바인딩된 NIC 또는 VM 서브넷 수 있습니다. 트래픽 hello 방향에 우선 순위를 기준으로 제공 됩니다.

반드시 너무[계획](../../virtual-network/virtual-networks-nsg.md#planning) 여 Nsg를 Vm과 VNet를 계획 하는 경우.

이 표에서 toocreate 네트워크 보안 그룹을 사용할 수 있는 hello 메서드를 보여 줍니다.

| 메서드 | 설명 |
| ------ | ----------- |
| [Azure 포털](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md) | Hello Azure 포털에서에서 VM을 만들 때 NSG 자동으로 만들어지고 연결된 toohello NIC hello 포털을 만듭니다. hello NSG의 hello 이름이 hello VM의 hello 이름의 조합 및 **-nsg**합니다. 이 NSG의 우선 순위가 1000, 서비스 집합 tooRDP, hello 프로토콜 집합 tooTCP 인바운드 규칙을 하나 포함, 포트 too3389를 설정 하 고 작업이 tooAllow를 설정 합니다. 모든 다른 인바운드 트래픽을 toohello VM tooallow을 원하는 경우에 추가 규칙 toohello NSG를 추가 해야 합니다. |
| [Azure PowerShell](../../virtual-network/virtual-networks-create-nsg-arm-ps.md) | 사용 하 여 [새로 AzureRmNetworkSecurityRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmNetworkSecurityRuleConfig) hello 필요한 규칙 정보를 제공 합니다. 사용 하 여 [새로 AzureRmNetworkSecurityGroup](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmNetworkSecurityGroup) toocreate hello NSG 합니다. 사용 하 여 [집합 AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/Set-AzureRmVirtualNetworkSubnetConfig) tooconfigure hello NSG hello 서브넷에 대 한 합니다. 사용 하 여 [집합 AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) tooadd hello NSG toohello VNet입니다. |
| [Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md) | 사용 하 여 [az 네트워크 nsg 만들기](https://docs.microsoft.com/cli/azure/network/nsg#create) tooinitially hello NSG를 만듭니다. 사용 하 여 [az 네트워크 nsg 규칙 만들기](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) tooadd toohello NSG 규칙입니다. 사용 하 여 [az 네트워크 vnet 서브넷 업데이트](https://docs.microsoft.com/en-us/cli/azure/network/vnet/subnet#update) tooadd hello NSG toohello 서브넷입니다. |
| [템플릿](../../virtual-network/virtual-networks-create-nsg-arm-template.md) | 템플릿을 사용하여 네트워크 보안 그룹을 배포하기 위한 지침으로 [네트워크 보안 그룹 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/101-security-group-create)를 사용합니다. |

## <a name="load-balancers"></a>부하 분산 장치

[Azure 부하 분산 장치](../../load-balancer/load-balancer-overview.md) 높은 가용성 및 네트워크 성능을 tooyour 응용 프로그램을 제공 합니다. 부하 분산 장치를 너무 구성할 수 있습니다[들어오는 인터넷 트래픽 균등화](../../load-balancer/load-balancer-internet-overview.md) tooVMs 또는 [VNet에서 Vm 간의 트래픽을 분산](../../load-balancer/load-balancer-internal-overview.md)합니다. 부하 분산 장치가 외부 트래픽 전달 tooa 또는 크로스-프레미스 네트워크에서 온-프레미스 컴퓨터와 Vm 간의 트래픽을 균형을 조정할 수도 수 특정 VM입니다.

hello 부하 분산 장치 지도 들어오고 나가는 트래픽을 사이 공용 IP 주소 및 포트에 hello 부하 분산 장치 및 hello 개인 IP 주소 및 hello VM의 포트 hello 합니다.

부하 분산 장치를 만들 때는 다음 구성 요소도 고려해야 합니다.

- **프런트 엔드 IP 구성** - 부하 분산 장치는 VIP(가상 IP)라고도 하는 프런트 엔드 IP 주소를 하나 이상 포함할 수 있습니다. 이러한 IP 주소는 hello 트래픽에 대 한 수신으로 사용 됩니다.
- **백 엔드 주소 풀** – hello NIC toowhich 부하와 관련 된 IP 주소에 배포 됩니다.
- **NAT 규칙** -방법을 인바운드 트래픽을 정의 hello 프런트 엔드 IP와 분산된 toohello 백 엔드 IP를 통해 이동 합니다.
- **부하 분산 장치 규칙** -지정 된 프런트 엔드 IP와 포트 조합이 tooa 일련의 백 엔드 IP 주소 및 포트 조합에 매핑합니다. 부하 분산 장치 하나에 여러 부하 분산 규칙이 포함될 수 있습니다. 각 규칙은 VM과 연결된 백 엔드 IP와 포트 및 프런트 엔드 IP와 포트의 조합입니다.
- **[프로브](../../load-balancer/load-balancer-custom-probe-overview.md)**  -모니터 hello Vm의 상태입니다. Hello 부하 분산 장치는 새 연결 toohello 전송을 중지 하는 검색에 실패 하면 toorespond 비정상 VM입니다. hello 기존 연결에 영향을 받지 않습니다 및 새 연결 toohealthy Vm 전송 됩니다.

이 표에서 toocreate에서 인터넷 연결 부하 분산 장치를 사용할 수 있는 hello 메서드를 보여 줍니다.

| 메서드 | 설명 |
| ------ | ----------- |
| Azure portal | 현재 hello Azure 포털을 사용 하 여에서 인터넷 연결 부하 분산 장치를 만들 수 없습니다. |
| [Azure PowerShell](../../load-balancer/load-balancer-get-started-internet-arm-ps.md) | tooprovide hello 식별자의 hello 공용 IP 주소에 사용 하 여 이전에 만든된 [새로 AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerFrontendIpConfig) hello로 **-PublicIpAddress** 매개 변수입니다. 사용 하 여 [새로 AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerBackendAddressPoolConfig) hello 백 엔드 주소 풀의 toocreate hello 구성 합니다. 사용 하 여 [새로 AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerInboundNatRuleConfig) toocreate 인바운드 NAT 규칙 만든 hello 프런트 엔드 IP 구성과 관련 된 합니다. 사용 하 여 [새로 AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerProbeConfig) toocreate hello 조사 해야 합니다. 사용 하 여 [새로 AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerRuleConfig) toocreate hello 부하 분산 장치 구성 합니다. 사용 하 여 [새로 AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer) toocreate hello에 대 한 부하 분산 장치입니다.|
| [Azure CLI](../../load-balancer/load-balancer-get-started-internet-arm-cli.md) | 사용 하 여 [az 네트워크 lb 만들](https://docs.microsoft.com/cli/azure/network/lb#create) toocreate hello 초기 부하 분산 장치 구성 합니다. 사용 하 여 [az 네트워크 lb 프런트 엔드-ip 만들기](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) tooadd hello 공용 IP 주소를 이전에 만든 합니다. 사용 하 여 [az 네트워크 lb 주소 풀 만들기](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) hello 백 엔드 주소 풀의 tooadd hello 구성 합니다. 사용 하 여 [az 네트워크 lb 인바운드-nat-규칙 만들기](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) tooadd NAT 규칙입니다. 사용 하 여 [az 네트워크 lb 규칙 만들기](https://docs.microsoft.com/cli/azure/network/lb/rule#create) tooadd hello 부하 분산 장치 규칙입니다. 사용 하 여 [az 네트워크 lb 프로브 만들기](https://docs.microsoft.com/cli/azure/network/lb/probe#create) tooadd hello 프로브 합니다. |
| [템플릿](../../load-balancer/load-balancer-get-started-internet-arm-template.md) | 사용 하 여 [부하 분산 장치에 2 개의 Vm hello LB에서 NAT 규칙을 구성 하 고](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-natrules) 템플릿을 사용 하 여 부하 분산 장치를 배포 하기 위한 기준으로 합니다. |
    
이 표에서 toocreate는 내부 부하 분산 장치를 사용할 수 있는 hello 메서드를 보여 줍니다.

| 메서드 | 설명 |
| ------ | ----------- |
| Azure portal | 현재 hello Azure 포털을 사용 하는 내부 부하 분산 장치를 만들 수 없습니다. |
| [Azure PowerShell](../../load-balancer/load-balancer-get-started-ilb-arm-ps.md) | tooprovide hello 네트워크 서브넷에서 사용 하 여 개인 IP 주소를 [새로 AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerFrontendIpConfig) hello로 **-PrivateIpAddress** 매개 변수입니다. 사용 하 여 [새로 AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerBackendAddressPoolConfig) hello 백 엔드 주소 풀의 toocreate hello 구성 합니다. 사용 하 여 [새로 AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerInboundNatRuleConfig) toocreate 인바운드 NAT 규칙 만든 hello 프런트 엔드 IP 구성과 관련 된 합니다. 사용 하 여 [새로 AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerProbeConfig) toocreate hello 조사 해야 합니다. 사용 하 여 [새로 AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerRuleConfig) toocreate hello 부하 분산 장치 구성 합니다. 사용 하 여 [새로 AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer) toocreate hello에 대 한 부하 분산 장치입니다.|
| [Azure CLI](../../load-balancer/load-balancer-get-started-ilb-arm-cli.md) | 사용 하 여 hello [az 네트워크 lb 만들](https://docs.microsoft.com/cli/azure/network/lb#create) 명령 toocreate hello 초기 부하 분산 장치 구성 합니다. toodefine hello 개인 IP 주소를 사용 하 여 [az 네트워크 lb 프런트 엔드-ip 만들기](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) hello로 **-개인 ip 주소** 매개 변수입니다. 사용 하 여 [az 네트워크 lb 주소 풀 만들기](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) hello 백 엔드 주소 풀의 tooadd hello 구성 합니다. 사용 하 여 [az 네트워크 lb 인바운드-nat-규칙 만들기](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) tooadd NAT 규칙입니다. 사용 하 여 [az 네트워크 lb 규칙 만들기](https://docs.microsoft.com/cli/azure/network/lb/rule#create) tooadd hello 부하 분산 장치 규칙입니다. 사용 하 여 [az 네트워크 lb 프로브 만들기](https://docs.microsoft.com/cli/azure/network/lb/probe#create) tooadd hello 프로브 합니다.|
| [템플릿](../../load-balancer/load-balancer-get-started-ilb-arm-template.md) | 사용 하 여 [부하 분산 장치에 2 개의 Vm hello LB에서 NAT 규칙을 구성 하 고](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer) 템플릿을 사용 하 여 부하 분산 장치를 배포 하기 위한 기준으로 합니다. |

## <a name="vms"></a>VM

Vm에서에서 만들 수 있습니다 hello 동일한 VNet 있으며 다른 tooeach 연결할 수 개인 IP 주소를 사용할 합니다. Hello 필요 tooconfigure 없이 서로 다른 서브넷의 게이트웨이 인지 공용 IP 주소를 사용 하는 경우에 연결할 수 있습니다. hello VNet을 만들 tooput VNet에 Vm을 다음 각 VM을 만들 때 있습니다 지정 toohello VNet 서브넷입니다. VM은 배포 또는 시작 중에 네트워크 설정을 가져옵니다.  

VM을 배포할 때 IP 주소가 해당 VM에 할당됩니다. 여러 VM을 VNet 또는 서브넷에 배포하는 경우 부팅할 때 IP 주소가 할당됩니다. 동적 IP 주소 (DIP)는 VM와 관련 된 hello 내부 IP 주소. 정적 DIP tooa VM을 할당할 수 있습니다. 고정 DIP를 할당 하는 경우 실수로 다른 VM에 대 한 고정 DIP를 다시 사용 하는 특정 서브넷 tooavoid 사용을 고려해 야 합니다.  

VM을 만들고 나중에 toomigrate를 원하는 경우이 VNet 안으로 없는 간단한 구성을 변경 합니다. Hello VNet에 VM hello를 다시 배포 해야 합니다. 가장 쉬운 방법은 tooredeploy hello는 toodelete hello VM을 내보내지 디스크가 연결 tooit, 있고 hello VNet의에서 원래 디스크 hello 한 다음 다시 hello VM 사용 하 여 작성 합니다. 

이 표에서 hello 메서드 toocreate VM을 VNet에 사용할 수 있습니다.

| 메서드 | 설명 |
| ------ | ----------- |
| [Azure 포털](../virtual-machines-windows-hero-tutorial.md) | 사용 하 여 hello 기본 네트워크 설정이 이전에 있던 언급 toocreate 단일 NIC VM 여러 Nic 사용 하 여 VM toocreate 다른 방법을 사용 해야 합니다. |
| [Azure PowerShell](../virtual-machines-windows-ps-create.md) | hello 사용을 포함 [추가 AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) tooadd hello toohello VM 구성 이전에 만든 NIC 합니다. |
| [템플릿](ps-template.md) | 템플릿을 사용하여 VM을 배포하기 위한 지침으로 [매우 간단한 Windows VM 배포](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)(영문)를 사용합니다. |

## <a name="next-steps"></a>다음 단계

- 자세한 내용은 방법 tooconfigure [사용자 정의 경로 및 IP 전달](../../virtual-network/virtual-networks-udr-overview.md)합니다. 
- 자세한 내용은 방법 tooconfigure [tooVNet vnet 대 VNet 연결](../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)합니다.
- 너무 방법에 대해 알아봅니다[경로 문제를 해결](../../virtual-network/virtual-network-routes-troubleshoot-portal.md)합니다.
