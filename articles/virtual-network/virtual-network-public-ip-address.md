---
title: "aaaCreate, 변경 또는 Azure 공용 IP 주소를 삭제 합니다. | Microsoft Docs"
description: "Toocreate, 변경 또는 공용 IP 주소 삭제 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 0f2578e8661c8f33419b896debcfa0ba1b41fc5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-public-ip-address"></a>공용 IP 주소 만들기, 변경 또는 삭제

공용 IP 주소 및 toocreate, 변경 하 고 하나를 삭제 하는 방법을 알아봅니다. 공용 IP 주소는 자체적으로 구성 가능한 설정을 사용하는 리소스입니다. 공용 IP 주소 tooother Azure 리소스를 할당할 수 있습니다.
- Azure 가상 컴퓨터 (VM), Azure 가상 컴퓨터 크기 집합, Azure VPN 게이트웨이, 응용 프로그램 게이트웨이 및 인터넷 연결 Azure 부하 분산 장치 등의 인바운드 인터넷 연결이 tooresources 합니다. Azure 리소스는 할당 된 공용 IP 주소가 없는 hello 인터넷에서에서 인바운드 통신을 받을 수 없습니다. 일부 Azure 리소스는 기본적으로 공용 IP 주소를 통해 액세스할 수, 다른 리소스 할당 toothem toobe hello 인터넷에서에서 액세스할 수 있는 공용 IP 주소가 있어야 합니다.
- 아웃 바운드 연결 toohello 예측 가능한 IP 주소를 사용 하 여 인터넷 합니다. 예를 들어 가상 컴퓨터에 공용 IP 주소 할당 tooit 없이 아웃 바운드 toohello 인터넷 통신할 수 있지만 해당 주소는 Azure tooan 예측할 수 없는 공용 주소에 의해 번역 네트워크 주소입니다. 공용 IP 주소 tooa 리소스를 지정 tooknow hello 아웃 바운드 연결에 사용 되는 IP 주소 수 있습니다. 예측 가능 하지만 hello 주소 선택한 hello 할당 방법에 따라 달라 집니다. 자세한 내용은 [공용 IP 주소 만들기](#create-a-public-ip-address)를 참조하세요. Azure 리소스를 읽을 hello의 아웃 바운드 연결에 대 한 자세한 toolearn [아웃 바운드 연결 이해](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 문서.

## <a name="before-you-begin"></a>시작하기 전에

이 문서의 섹션의 단계를 완료 하기 전에 작업을 수행 하는 hello를 완료 합니다.

- 검토 hello [Azure 제한](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) 공용 IP 주소에 대 한 제한에 대 한 문서 toolearn 합니다.
- Toohello Azure에에서 로그인 [포털](https://portal.azure.com), Azure 명령줄 인터페이스 (CLI) 또는 Azure 계정으로 Azure PowerShell. 아직 Azure 계정이 없으면 [평가판 계정](https://azure.microsoft.com/free)에 등록합니다.
- 이 문서에서는 toocomplete 작업 명령이 PowerShell을 사용 하는 경우 [Azure PowerShell 설치 및 구성](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다. Hello 가장 최신 버전을 설치 하는 hello Azure PowerShell commandlet의 확인 합니다. 예제를 보려면으로 PowerShell 명령에 대 한 도움말 tooget 입력 `get-help <command> -full`합니다.
- 이 문서에서는 toocomplete 작업 명령을 Azure CLI (명령줄 인터페이스)를 사용 하는 경우 [설치 및 구성 hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다. Hello 최신 버전의 hello Azure CLI 설치 되어 있는지 확인 합니다. CLI 명령에 대 한 도움말 tooget 입력 `az <command> --help`합니다. 설치 hello CLI 및 해당 필수 구성 요소는 대신 Azure 클라우드 셸 hello를 사용할 수 있습니다. Azure 클라우드 셸 hello hello Azure 포털 내에서 직접 실행할 수 있는 무료 Bash 셸의입니다. Hello Azure CLI 사전 설치 및 toouse 사용자 계정으로 구성 된이 있습니다. toouse hello 클라우드 셸 클릭 hello 클라우드 셸 **> _** hello hello 위쪽에 단추 [포털](https://portal.azure.com)합니다.

공용 IP 주소에는 명목 요금이 부과됩니다. hello 읽을 tooview hello 가격 [IP 주소 가격](https://azure.microsoft.com/pricing/details/ip-addresses) 페이지. 

## <a name="create-a-public-ip-address"></a>공용 IP 주소 만들기

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) 계정과 구독에 대 한 hello 네트워크 참가자 역할에 대 한 즉 (최소한) 할당 된 권한입니다. 읽기 hello [Azure 역할 기반 액세스 제어에 대 한 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) tooaccounts 역할 및 사용 권한 할당에 대 한 자세한 문서 toolearn 합니다.
2. Hello 텍스트를 포함 하는 hello 상자에서 *리소스 검색* hello Azure 포털의 hello 위쪽 입력 *공용 ip 주소*합니다. 때 **공용 IP 주소** 나타납니다 hello 검색 결과에를 클릭 합니다.
3. 클릭 **+ 추가** hello에 **공용 IP 주소** 블레이드를 표시 합니다.
4. Hello의 설정에 따라 hello에 대 한 값을 선택 또는 입력 **공용 IP 주소 만들기** 블레이드를 놓고 클릭 한 다음 **만들기**:

    |설정|Required?|세부 정보|
    |---|---|---|
    |이름|예|hello 이름은 선택한 hello 리소스 그룹 내에서 고유 해야 합니다.|
    |IP 버전|예| IPv4 또는 IPv6을 선택합니다. 공용 IPv4 주소가 수는 tooseveral Azure 리소스에 할당 하는 동안 IPv6 공용 IP 주소 수만 할당 될 tooan 인터넷 연결 부하 분산 장치. 부하 분산 장치 hello 균형 IPv6 트래픽 tooAzure 가상 컴퓨터를 로드할 수 있습니다. 에 대 한 자세한 내용은 [부하 분산 IPv6 트래픽을 toovirtual 컴퓨터](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.
    |IP 주소 할당|예|**동적:** tooa NIC tooa VM을 연결 하 고 hello VM 시작 hello에 대 한 처음으로 hello 공용 IP 주소 연결 되 면 동적 주소가 할당 됩니다. 동적 주소는 hello VM hello NIC가 연결 된 toois 중지 하면 변경할 수 (할당 취소 됨). hello 주소 남아 hello 경우 hello VM 다시 부팅 또는 중지 (할당 취소) 동일 합니다. **정적:** hello 공용 IP 주소를 만들 때 고정 주소 할당 됩니다. 고정 주소 변경도 hello VM에에서 저장 됩니다 hello 중지 (할당 취소 됨) 상태를 하지 않습니다. hello NIC 삭제 된 경우에 hello 주소가 해제 됩니다. Hello NIC 만들어지면 hello 할당 메서드를 변경할 수 있습니다. Hello에 대 한 IPv6를 선택 하는 경우 **IP 버전**, hello 할당만 사용할 수 있는 메서드는 **동적**합니다.|
    |유휴 제한 시간(분)|아니요|분 단위로 tookeep 클라이언트가 toosend 연결 유지 메시지에 의존 하지 않고 TCP 또는 HTTP 연결을 엽니다. **IP 버전**으로 IPv6을 선택하는 경우에는 이 값을 변경할 수 없습니다. |
    |DNS 이름 레이블|아니요|Hello에 hello 이름 (모든 구독 및 모든 고객)에서 만들 Azure 위치 내에서 고유 해야 합니다. hello Azure 공용 DNS 서비스가 자동으로 등록 hello 이름 및 IP 주소 hello 이름의 tooa 리소스를 연결할 수 있도록 합니다. Azure 추가 *location.cloudapp.azure.com* toohello 이름 toocreate hello를 완벽 하 게 제공 된 DNS 이름 (여기서 위치는 선택한 hello 위치). Toocreate 두 주소 버전을 선택 하면 hello 동일한 DNS 이름이 지정 됩니다 tooboth hello IPv4 및 IPv6 주소입니다. hello Azure DNS 서비스 IPv4 A 및 AAAA IPv6 모두 이름 레코드를 포함 하며 hello DNS 이름을 조회할 때 두 레코드를 사용 하 여 응답 합니다. hello 클라이언트와 어떤 주소 (IPv4 또는 IPv6) toocommunicate를 선택합니다.|
    |IPv6 주소 만들기 또는 IPv4 주소 만들기|아니요| **IP 버전**으로 선택한 항목에 따라 IPv6 또는 IPv4가 표시됩니다. 예를 들어 **IP 버전**으로 **IPv4**를 선택하면 여기에 **IPv6**이 표시됩니다.
    |이름 (hello를 선택한 경우에 표시 **IPv6 (또는 i p v 4) 주소를 만들어** 확인란)|예, hello를 선택 하는 경우 **IPv6 만들** (또는 IPv4) 확인란을 선택 합니다.|hello 이름은 달라 야 먼저 hello에 대 한 입력 hello 이름 보다 **이름** 이 목록에 있습니다. IPv4 및 IPv6 주소 모두 toocreate를 선택 하면 hello 포털 두 개의 별도 공용 IP 주소 리소스를 tooit 할당 된 각 IP 주소 버전으로 만듭니다.|
    |IP 주소 할당 (hello를 선택한 경우에 표시 **IPv6 (또는 i p v 4) 주소를 만들어** 확인란)|예, hello를 선택 하는 경우 **IPv6 만들** (또는 IPv4) 확인란을 선택 합니다.|표시 hello 확인란을 선택 하는 경우 **IPv4 주소를 만들어**, 할당 방법을 선택할 수 있습니다. 표시 hello 확인란을 선택 하는 경우 **IPv6 주소를 만들어**, 해야 하기 할당 메서드를 선택할 수 없습니다 **동적**합니다.|
    |구독|예|에 존재 해야 hello 동일 [구독](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) hello 리소스로 tooassociate hello 공용 IP 주소를 지정 하려면.|
    |리소스 그룹|예|같거나 다른 데이터 집합, hello에 존재할 수 [리소스 그룹](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group) hello 리소스로 tooassociate hello 공용 IP 주소를 지정 하려면.|
    |위치|예|에 존재 해야 hello 동일 [위치](https://azure.microsoft.com/regions), tooassociate hello 공용 IP 주소를 지정 하려면 hello 리소스로 tooas 영역 라고도 합니다.|

**명령**

Hello 포털은 hello 옵션 toocreate 두 개의 공용 IP 주소 리소스 (IPv4 및 IPv6)을 제공 하지만 hello CLI 및 PowerShell 명령은 다음 리소스를 만듭니다 하나의 IP 버전 또는 hello에 대 한 주소와 다른. 두 개의 공용 IP 주소 리소스, IP 버전 별로 하나씩 하려는 경우 명령을 실행 해야 hello을 두 번 hello 공용 IP 주소 리소스에 대 한 버전 및 서로 다른 이름을 지정 합니다. 

|도구|명령|
|---|---|
|CLI|[az network public-ip create](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)|

## <a name="view-change-settings-for-or-delete-a-public-ip-address"></a>공용 IP 주소 보기, 설정 변경 또는 삭제

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) 계정과 구독에 대 한 hello 네트워크 참가자 역할에 대 한 즉 (최소한) 할당 된 권한입니다. 읽기 hello [Azure 역할 기반 액세스 제어에 대 한 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) tooaccounts 역할 및 사용 권한 할당에 대 한 자세한 문서 toolearn 합니다.
2. Hello 텍스트를 포함 하는 hello 상자에서 *리소스 검색* hello Azure 포털의 hello 위쪽 입력 *공용 ip 주소*합니다. 때 **공용 IP 주소** 나타납니다 hello 검색 결과에를 클릭 합니다.
3. Hello에 **공용 IP 주소** 나타나는 블레이드 hello hello 공용 IP 주소의 이름으로 원하는 tooview에 대 한 설정을 변경 또는 삭제를 클릭 합니다.
4. Hello 블레이드에서 나타나는 hello에 대 한 공용 IP 주소, hello 다음 tooview, 여부에 따라 옵션 중 하나를 수행 삭제 또는 hello 공용 IP 주소를 변경 합니다.
    - **보기**: hello **개요** hello 블레이드 섹션 hello 공용 IP 주소에 대 한 키 설정을 표시, hello 네트워크 인터페이스와 같은 연결 된 너무 (hello 주소 관련된 tooa 네트워크 인터페이스 경우). hello 포털 hello 버전의 hello 주소 (IPv4 또는 IPv6)을 표시 하지 않습니다. tooview hello 버전 정보를 사용 하 여 hello PowerShell 또는 CLI 명령 tooview hello 공용 IP 주소입니다. Hello IP 주소 버전은 i p v 6을 주소를 할당 하는 hello hello 포털, PowerShell 또는 CLI hello로 표시 되지 않습니다. 
    - **삭제**: toodelete hello 공용 IP 주소를 클릭 **삭제** hello에 **개요** hello 블레이드의 섹션입니다. Hello 주소를 현재 연결된 tooan IP 구성을 삭제할 수 없습니다. Hello 주소를 현재 구성에 연결 되어 있으면 클릭 **분리** hello IP 구성에서 toodissociate hello 주소입니다.
    - **변경**: **구성**을 클릭합니다. Hello 정보를 사용 하 여 hello의 4 단계에서 설정을 변경 [공용 IP 주소 만들기](#create-a-public-ip-address) 이 문서의 섹션. 정적 toodynamic에서 IPv4 주소에 대 한 toochange hello 할당을 먼저 hello 공용 IPv4 주소에 연결 하는 hello IP 구성에서 분리 해야 합니다. 그런 다음 hello 할당 메서드 toodynamic 변경 하 고 클릭 수 **연결** tooassociate hello IP 주소 toohello 동일한 IP 구성을, 다른 구성 하거나 있습니다 상태로 남겨둘 수 분리 합니다. hello에 공용 IP 주소를 toodissociate **개요** 섹션에서 클릭 **분리**합니다.

>[!WARNING]
>정적 toodynamic에서 hello 할당 메서드를 변경 하면 toohello 공용 IP 주소가 할당 된 IP 주소를 hello 손실 됩니다. Hello Azure 공용 DNS 서버 간에 매핑을 유지 정적 또는 동적 주소 및 모든 DNS 이름 레이블을 (정의한 하나) 하는 경우, VM hello hello에 (할당 취소) 상태 중지 후 시작 될 때 동적 IP 주소를 변경할 수 있습니다. 변경에서 tooprevent hello 주소는 고정 IP 주소를 할당 합니다.

**명령**

|도구|명령|
|---|---|
|CLI|[az 네트워크 공개 ip 목록](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#list) toolist 공용 IP 주소 [az 네트워크 공개 ip 표시](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#show) tooshow 설정; [az 네트워크 공개 ip 업데이트](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#update) tooupdate; [az 네트워크 공용 ip 삭제](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#delete) toodelete|
|PowerShell|[Get AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress?toc=%2fazure%2fvirtual-network%2ftoc.json) tooretrieve 공용 IP 주소 개체 및 해당 설정을 보려면 [집합 AzureRmPublicIpAddress](/powershell/resourcemanager/azurerm.network/set-azurermpublicipaddress?toc=%2fazure%2fvirtual-network%2ftoc.json) tooupdate 설정; [제거 AzureRmPublicIpAddress](/powershell/module/azurerm.network/remove-azurermpublicipaddress) toodelete|

## <a name="next-steps"></a>다음 단계
Hello 다음 Azure 리소스를 만들 때 공용 IP 주소를 할당 합니다.

- [Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 또는 [Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 가상 컴퓨터
- [인터넷 연결 Azure Load Balancer](../load-balancer/load-balancer-get-started-internet-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Azure 응용 프로그램 게이트웨이](../application-gateway/application-gateway-create-gateway-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Azure VPN Gateway를 사용하여 사이트 간 연결](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Azure Virtual Machine Scale Set](../virtual-machine-scale-sets/virtual-machine-scale-sets-portal-create.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
