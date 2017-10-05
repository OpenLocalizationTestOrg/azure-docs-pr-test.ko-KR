---
title: "Azure 공용 IP 주소 만들기, 변경 또는 삭제 | Microsoft 문서"
description: "공용 IP 주소를 만들거나 변경하거나 삭제하는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bb71abaf-b2d9-4147-b607-38067a10caf6
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: jdial
ms.openlocfilehash: 9a51cd703266e330550a2a2f4e6a4d46722fec09
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-change-or-delete-a-public-ip-address"></a>공용 IP 주소 만들기, 변경 또는 삭제

공용 IP 주소 및 해당 IP 주소를 생성, 변경 및 삭제하는 방법에 대해 알아봅니다. 공용 IP 주소는 자체적으로 구성 가능한 설정을 사용하는 리소스입니다. 공용 IP 주소를 다른 Azure 리소스에 할당하면 다음을 수행할 수 있습니다.
- Azure VM(가상 컴퓨터), Azure Virtual Machine Scale Sets, Azure VPN Gateway, 응용 프로그램 게이트웨이 및 인터넷 연결 Azure Load Balancer와 같은 리소스에 대한 인바운드 인터넷 연결. 할당된 공용 IP 주소가 없으면 Azure 리소스는 인터넷에서 인바운드 통신을 수신할 수 없습니다. 공용 IP 주소를 통해 기본적으로 액세스 가능한 Azure 리소스도 있지만, 그 외의 리소스에는 공용 IP 주소가 할당되어 있어야 인터넷에서 액세스할 수 있습니다.
- 예측 가능한 IP 주소를 사용하는 인터넷으로의 아웃바운드 연결. 예를 들어 공용 IP 주소가 할당되지 않은 가상 컴퓨터도 인터넷으로의 아웃바운드 통신을 수행할 수는 있지만, 이 가상 컴퓨터의 주소는 Azure에서 예측할 수 없는 공용 주소로 변환한 네트워크 주소입니다. 공용 IP 주소를 리소스에 할당하면 아웃바운드 연결에 사용되는 IP 주소를 확인할 수 있습니다. 이 주소는 예측은 가능하지만 선택한 할당 방법에 따라 변경될 수 있습니다. 자세한 내용은 [공용 IP 주소 만들기](#create-a-public-ip-address)를 참조하세요. Azure 리소스의 아웃바운드 연결에 대한 자세한 내용은 [아웃바운드 연결 이해](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 문서를 참조하세요.

## <a name="before-you-begin"></a>시작하기 전에

이 문서에서 설명하는 섹션의 모든 단계를 수행하려면 다음 작업을 완료해야 합니다.

- [Azure 한도](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) 문서를 검토하여 공용 IP 주소에 대한 한도 사항을 알아봅니다.
- Azure 계정으로 Azure [Portal](https://portal.azure.com), Azure CLI(명령줄 인터페이스) 또는 Azure PowerShell에 로그인합니다. 아직 Azure 계정이 없으면 [평가판 계정](https://azure.microsoft.com/free)에 등록합니다.
- PowerShell 명령을 사용하여 이 문서의 작업을 완료하는 경우 [Azure PowerShell을 설치 및 구성](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다. 최신 버전의 Azure PowerShell commandlet을 설치했는지 확인합니다. 예제와 함께 PowerShell 명령에 대한 도움말을 보려면 `get-help <command> -full`을 입력합니다.
- Azure CLI(명령줄 인터페이스) 명령을 사용하여 이 문서의 작업을 완료하는 경우 [Azure CLI를 설치 및 구성](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다. 최신 버전의 Azure CLI를 설치했는지 확인합니다. CLI 명령에 대한 도움말을 보려면 `az <command> --help`를 입력합니다. CLI 및 해당 필수 구성 요소를 설치하는 대신 Azure Cloud Shell을 사용할 수 있습니다. Azure Cloud Shell은 Azure Portal에서 직접 실행할 수 있는 평가판 Bash 셸입니다. Azure CLI가 사전 설치되어 계정에서 사용하도록 구성되어 있습니다. Cloud Shell을 사용하려면 [Portal](https://portal.azure.com) 위쪽의 Cloud Shell **>_** 단추를 클릭합니다.

공용 IP 주소에는 명목 요금이 부과됩니다. 가격을 보려면 [IP 주소 가격](https://azure.microsoft.com/pricing/details/ip-addresses) 페이지를 참조하세요. 

## <a name="create-a-public-ip-address"></a>공용 IP 주소 만들기

1. 구독에 대한 네트워크 참가자 역할에 권한(최소)이 할당된 계정으로 [Azure Portal](https://portal.azure.com)에 로그인합니다. 계정에 역할 및 권한을 할당하는 방법에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어의 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) 문서를 참조하세요.
2. Azure Portal 위쪽의 *리소스 검색* 텍스트가 있는 상자에서 *공용 IP 주소*를 입력합니다. 검색 결과에 표시된 **공용 IP 주소**를 클릭합니다.
3. 표시되는 **공용 IP 주소** 블레이드에서 **+ 추가**를 클릭합니다.
4. 표시되는 **공용 IP 주소 만들기** 블레이드에서 다음 설정 값을 입력하거나 선택한 다음 **만들기**를 클릭합니다.

    |설정|Required?|세부 정보|
    |---|---|---|
    |이름|예|이름은 선택한 리소스 그룹 내에서 고유해야 합니다.|
    |IP 버전|예| IPv4 또는 IPv6을 선택합니다. 공용 IPv4 주소는 여러 Azure 리소스에 할당할 수 있는 반면 IPv6 공용 IP 주소는 인터넷 연결 부하 분산 장치에만 할당할 수 있습니다. 부하 분산 장치는 Azure 가상 컴퓨터로 IPv6 트래픽을 부하 분산할 수 있습니다. 자세한 내용은 [가상 컴퓨터로 IPv6 트래픽 부하 분산](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json)을 참조하세요.
    |IP 주소 할당|예|**동적:** 동적 주소는 VM에 연결된 NIC에 공용 IP 주소를 연결하고 VM을 처음 시작한 후에만 할당됩니다. NIC가 연결된 VM이 중지(할당 취소)되면 동적 주소가 변경될 수 있습니다. VM을 다시 부팅하거나 중지하는 경우(하지만 할당 취소하지 않은 경우) 주소가 동일하게 유지됩니다. **고정:** 고정 IP 주소를 만들면 고정 주소가 할당됩니다. VM이 중지(할당 취소)된 상태에 있더라도 고정 주소는 변경되지 않습니다. 이 주소는 NIC를 삭제할 때만 해제됩니다. NIC를 만든 후에는 할당 방법을 변경할 수 있습니다. **IP 버전**으로 IPv6을 선택하는 경우에는 **동적** 할당 방법만 사용할 수 있습니다.|
    |유휴 제한 시간(분)|아니요|연결 유지 메시지를 보내는 데 클라이언트를 사용하지 않고 TCP 또는 HTTP 연결을 유지하는 데 걸리는 시간(분)입니다. **IP 버전**으로 IPv6을 선택하는 경우에는 이 값을 변경할 수 없습니다. |
    |DNS 이름 레이블|아니요|이름을 만드는 Azure 위치 내에서(모든 구독 및 모든 고객에서) 고유해야 합니다. Azure 공용 DNS 서비스는 이름과 IP 주소를 자동으로 등록하므로 해당 이름을 사용하는 리소스에 연결할 수 있습니다. Azure에서는 정규화된 DNS 이름을 만드는 데 제공하는 이름에 *location.cloudapp.azure.com*(여기서 location은 선택한 위치임)을 추가합니다. 두 주소 버전을 모두 만드는 경우 IPv4 및 IPv6 주소 둘 다에 같은 DNS 이름이 할당됩니다. Azure DNS 서비스는 IPv4 A 및 IPv6 AAAA 이름 레코드를 모두 포함하며, DNS 이름을 조회할 때 응답으로 두 레코드를 모두 전송합니다. 클라이언트는 어떤 주소(IPv4 또는 IPv6)와 통신할지 선택합니다.|
    |IPv6 주소 만들기 또는 IPv4 주소 만들기|아니요| **IP 버전**으로 선택한 항목에 따라 IPv6 또는 IPv4가 표시됩니다. 예를 들어 **IP 버전**으로 **IPv4**를 선택하면 여기에 **IPv6**이 표시됩니다.
    |이름(**IPv6 주소 만들기 또는 IPv4 주소 만들기** 확인란을 선택한 경우에만 표시됨)|예 - **IPv6 주소 만들기** 또는 IPv4 주소 만들기 확인란을 선택하는 경우|이름은 이 목록의 첫 번째 **이름**으로 입력하는 이름과 달라야 합니다. IPv4 주소와 IPv6 주소를 모두 만들도록 선택하면 Portal에서는 각 IP 주소 버전이 할당된 개별 공용 IP 주소 리소스 두 개를 만듭니다.|
    |IP 주소 할당(**IPv6 주소 만들기 또는 IPv4 주소 만들기** 확인란을 선택한 경우에만 표시됨)|예 - **IPv6 주소 만들기** 또는 IPv4 주소 만들기 확인란을 선택하는 경우|**IPv4 주소 만들기** 확인란이 표시되는 경우 할당 방법을 선택할 수 있습니다. **IPv6 주소 만들기** 확인란이 표시되는 경우에는 **동적** 할당 방법만 사용해야 하므로 할당 방법을 선택할 수 없습니다.|
    |구독|예|공용 IP 주소를 연결하려는 리소스와 동일한 [구독](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription)에 있어야 합니다.|
    |리소스 그룹|예|공용 IP 주소를 연결하려는 리소스와 동일하거나 다른 [리소스 그룹](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group)에 있을 수 있습니다.|
    |위치|예|공용 IP 주소를 연결하려는 리소스와 동일한 [위치](https://azure.microsoft.com/regions)(하위 지역이라고도 함)에 있어야 합니다.|

**명령**

Portal에서는 IPv4와 IPv6용으로 하나씩 두 개의 공용 IP 주소 리소스를 만드는 옵션을 제공하지만, 다음 CLI 및 PowerShell 명령은 두 IP 버전 중 하나의 주소가 포함된 리소스 하나를 만듭니다. 각 IP 버전용으로 하나씩 두 개의 공용 IP 주소 리소스를 사용하려는 경우에는 공용 IP 주소 리소스에 대해 각기 다른 이름과 버전을 지정하여 명령을 두 번 실행해야 합니다. 

|도구|명령|
|---|---|
|CLI|[az network public-ip create](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)|

## <a name="view-change-settings-for-or-delete-a-public-ip-address"></a>공용 IP 주소 보기, 설정 변경 또는 삭제

1. 구독에 대한 네트워크 참가자 역할에 권한(최소)이 할당된 계정으로 [Azure Portal](https://portal.azure.com)에 로그인합니다. 계정에 역할 및 권한을 할당하는 방법에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어의 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) 문서를 참조하세요.
2. Azure Portal 위쪽의 *리소스 검색* 텍스트가 있는 상자에서 *공용 IP 주소*를 입력합니다. 검색 결과에 표시된 **공용 IP 주소**를 클릭합니다.
3. 나타나는 **공용 IP 주소** 블레이드에서 보고 설정을 변경하거나 삭제하려는 공용 IP 주소의 이름을 클릭합니다.
4. 공용 IP 주소에 대해 표시되는 블레이드에서 공용 IP 주소에 대해 수행하려는 작업(보기/삭제/변경)에 따라 다음 옵션 중 하나를 수행합니다.
    - **보기**: 블레이드의 **개요** 섹션에는 공용 IP 주소에 대한 주요 설정(예: 공용 IP 주소가 네트워크 인터페이스에 연결된 경우 주소가 연결된 네트워크 인터페이스)이 표시됩니다. Portal에는 주소(IPv4 또는 IPv6)의 버전이 표시되지 않습니다. 버전 정보를 보려면 PowerShell 또는 CLI를 사용하여 공용 IP 주소를 확인합니다. IP 주소 버전이 IPv6이면 할당된 주소가 Portal, PowerShell 또는 CLI 사용 시 표시되지 않습니다. 
    - **삭제**: 공용 IP 주소를 삭제하려면 블레이드의 **개요** 섹션에서 **삭제**를 클릭합니다. 주소가 현재 IP 구성과 연결되어 있으면 삭제할 수 없습니다. 주소가 현재 구성과 연결되어 있으면 **분리**를 클릭하여 IP 구성에서 주소를 분리합니다.
    - **변경**: **구성**을 클릭합니다. 이 문서의 [공용 IP 주소 만들기](#create-a-public-ip-address) 섹션의 4단계 정보를 사용하여 설정을 변경합니다. IPv4 주소 할당 방식을 정적에서 동적으로 변경하려면 먼저 공용 IPv4 주소가 연결된 IP 구성에서 주소를 분리해야 합니다. 그런 다음 할당 방법을 동적으로 변경하고 **연결**을 클릭하여 동일한 IP 구성이나 다른 구성으로 해당 IP 주소를 연결하거나 분리할 수 있습니다. 공용 IP 주소를 분리하려면 **개요** 섹션에서 **분리**를 클릭합니다.

>[!WARNING]
>할당 방법을 고정에서 동적으로 변경하면 공용 IP 주소에 할당된 IP 주소가 손실됩니다. Azure 공용 DNS 서버는 고정 또는 동적 주소와 모든 DNS 이름 레이블(사용자가 정의한 경우) 간의 매핑을 유지하지만, VM을 중지(할당 취소)된 상태에서 시작할 때 동적 IP 주소가 변경될 수 있습니다. 주소가 변경되지 않도록 하려면 고정 IP 주소를 할당합니다.

**명령**

|도구|명령|
|---|---|
|CLI|[az network public-ip-list](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#list): 공용 IP 주소를 나열함, [az network public-ip-show](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#show): 설정을 표시함, [az network public-ip update](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#update): 업데이트함, [az network public-ip delete](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#delete): 삭제함|
|PowerShell|[Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress?toc=%2fazure%2fvirtual-network%2ftoc.json): 공용 IP 주소 개체를 검색하고 해당 설정을 확인함, [Set-AzureRmPublicIpAddress](/powershell/resourcemanager/azurerm.network/set-azurermpublicipaddress?toc=%2fazure%2fvirtual-network%2ftoc.json): 설정을 업데이트함, [Remove-AzureRmPublicIpAddress](/powershell/module/azurerm.network/remove-azurermpublicipaddress): 삭제함|

## <a name="next-steps"></a>다음 단계
다음 Azure 리소스를 만들 때 공용 IP 주소를 할당합니다.

- [Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 또는 [Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 가상 컴퓨터
- [인터넷 연결 Azure Load Balancer](../load-balancer/load-balancer-get-started-internet-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Azure 응용 프로그램 게이트웨이](../application-gateway/application-gateway-create-gateway-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Azure VPN Gateway를 사용하여 사이트 간 연결](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Azure Virtual Machine Scale Set](../virtual-machine-scale-sets/virtual-machine-scale-sets-portal-create.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
