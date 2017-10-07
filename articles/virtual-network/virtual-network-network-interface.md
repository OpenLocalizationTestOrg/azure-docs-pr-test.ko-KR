---
title: "aaaCreate, 변경 또는 삭제 된 Azure 네트워크 인터페이스 | Microsoft Docs"
description: "알아보려면 네트워크 인터페이스는 및 toocreate,에 대 한 설정을 변경 하 고 하나를 삭제 하는 방법입니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: jdial
ms.openlocfilehash: dcb6cdbd73bc0d0ca4efb9d972d370cf2d54abb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-network-interface"></a>네트워크 인네트워크 인터페이스 만들기, 변경 또는 삭제

Toocreate,이 설정을 변경 하 고 네트워크 인터페이스를 삭제 하는 방법에 대해 알아봅니다. 네트워크 인터페이스에는 인터넷, Azure, 온-프레미스 리소스와는 Azure 가상 컴퓨터 toocommunicate를 수 있습니다. Hello Azure 포털을 사용 하 여 가상 컴퓨터를 만들 때 hello 포털 사용자에 대 한 기본 설정을 사용 하 여 하나 이상의 네트워크 인터페이스를 만듭니다. 대신 toocreate 사용자 지정 설정 사용 하 여 네트워크 인터페이스를 선택 하 고 만들 때 하나 이상의 네트워크 인터페이스 tooa 가상 컴퓨터를 추가할 수 있습니다. 기존 네트워크 인터페이스에 대 한 기본 네트워크 인터페이스 설정은 toochange 할 수 있습니다. 이 문서에서는 사용자 지정 설정 사용 하 여 네트워크 인터페이스 toocreate이 네트워크 필터 (네트워크 보안 그룹) 할당, 서브넷 할당, DNS 서버 설정 및 IP 전달 등의 기존 설정을 변경 하 고 네트워크 인터페이스를 삭제 하는 방법을 설명 합니다.

변경 또는 제거 하는 네트워크 인터페이스에 대 한 IP 주소 tooadd 해야 할 경우 읽기 hello [관리 IP 주소](virtual-network-network-interface-addresses.md) 문서. 를 tooadd 네트워크 인터페이스가 필요 하거나 가상 컴퓨터에서 네트워크 인터페이스를 제거 하는 경우 읽기 hello [네트워크 인터페이스를 추가 / 제거](virtual-network-network-interface-vm.md) 문서.


## <a name="before-you-begin"></a>시작하기 전에

이 문서의 섹션의 단계를 완료 하기 전에 작업을 수행 하는 hello를 완료 합니다.

- 검토 hello [Azure 제한](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) 네트워크 인터페이스에 대 한 제한에 대 한 문서 toolearn 합니다.
- Toohello Azure에에서 로그인 [포털](https://portal.azure.com), Azure 명령줄 인터페이스 (CLI) 또는 Azure 계정으로 Azure PowerShell. 아직 Azure 계정이 없으면 [평가판 계정](https://azure.microsoft.com/free)에 등록합니다.
- 이 문서에서는 toocomplete 작업 명령이 PowerShell을 사용 하는 경우 [Azure PowerShell 설치 및 구성](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다. Hello 가장 최신 버전을 설치 하는 hello Azure PowerShell commandlet의 확인 합니다. 예제를 보려면으로 PowerShell 명령에 대 한 도움말 tooget 입력 `get-help <command> -full`합니다.
- 이 문서에서는 toocomplete 작업 명령을 Azure CLI (명령줄 인터페이스)를 사용 하는 경우 [설치 및 구성 hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다. Hello 최신 버전의 hello Azure CLI 설치 되어 있는지 확인 합니다. CLI 명령에 대 한 도움말 tooget 입력 `az <command> --help`합니다. 설치 hello CLI 및 해당 필수 구성 요소는 대신 Azure 클라우드 셸 hello를 사용할 수 있습니다. Azure 클라우드 셸 hello hello Azure 포털 내에서 직접 실행할 수 있는 무료 Bash 셸의입니다. Hello Azure CLI 사전 설치 및 toouse 사용자 계정으로 구성 된이 있습니다. toouse hello 클라우드 셸 클릭 hello 클라우드 셸 **> _** hello hello 위쪽에 단추 [포털](https://portal.azure.com)합니다.

## <a name="create-a-network-interface"></a>네트워크 인터페이스 만들기

Hello Azure 포털을 사용 하 여 가상 컴퓨터를 만들 때 hello 포털 사용자에 대 한 기본 설정을 사용 하 여 네트워크 인터페이스를 만듭니다. 대신 모든 네트워크 인터페이스 설정을 지정, 사용자 지정 설정을 사용 하 여 네트워크 인터페이스를 만들고 (hello Azure CLI 또는 PowerShell을 사용 하 여) hello 가상 컴퓨터를 만들 때 hello 네트워크 인터페이스 tooa 가상 컴퓨터를 연결할 수 있습니다. 네트워크 인터페이스를 만들고 tooan (hello Azure CLI 또는 PowerShell 사용)는 기존 가상 컴퓨터를 추가할 수도 있습니다. toolearn toocreate 된 기존 가상 컴퓨터 네트워크 인터페이스 또는 tooadd, 또는 기존 가상 컴퓨터에서 네트워크 인터페이스를 제거 하는 방법을 읽고 hello [네트워크 인터페이스를 추가 / 제거](virtual-network-network-interface-vm.md) 문서. 네트워크 인터페이스를 만들기 전에 있어야 기존 [가상 네트워크](virtual-networks-create-vnet-arm-pportal.md) 에서 네트워크 인터페이스에 만들어야 하는 동일한 위치 형식 및 구독 hello 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) 계정과 구독에 대 한 hello 네트워크 참가자 역할에 대 한 즉 (최소한) 할당 된 권한입니다. 읽기 hello [Azure 역할 기반 액세스 제어에 대 한 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) tooaccounts 역할 및 사용 권한 할당에 대 한 자세한 문서 toolearn 합니다.
2. Hello 텍스트를 포함 하는 hello 상자에서 *리소스 검색* hello Azure 포털의 hello 위쪽 입력 *네트워크 인터페이스*합니다. 때 **네트워크 인터페이스** 나타납니다 hello 검색 결과에를 클릭 합니다.
3. Hello에 **네트워크 인터페이스** 블레이드를 놓고 클릭 **+ 추가**합니다.
4. Hello에 **만들기 네트워크 인터페이스** 나타나는 블레이드를 입력 하거나 hello 설정, 다음에 대 한 값을 선택한 다음 클릭 **만들기**:

    |설정|Required?|세부 정보|
    |---|---|---|
    |이름|예|hello 이름은 선택한 hello 리소스 그룹 내에서 고유 해야 합니다. 시간이 지남에 따라 Azure 구독에는 여러 개의 네트워크 인터페이스가 추가될 가능성이 많습니다. 읽기 hello [명명 규칙](/azure/architecture/best-practices/naming-conventions?toc=%2fazure%2fvirtual-network%2ftoc.json#naming-rules-and-restrictions) 제안 여러 관리 명명 규칙 toomake를 만들 때 네트워크 인터페이스를 더 쉽게에 대 한 문서입니다. hello 네트워크 인터페이스를 만든 후에 hello 이름을 변경할 수 없습니다.|
    |가상 네트워크|예|Hello hello 네트워크 인터페이스에 대 한 가상 네트워크를 선택 합니다. 네트워크 인터페이스 tooa 가상 네트워크에에서 있는 hello 동일만 할당할 수 구독 및 hello 네트워크 인터페이스로 위치입니다. 네트워크 인터페이스를 만든 후에 할당 된 hello 가상 네트워크를 변경할 수 없습니다. hello hello 네트워크 인터페이스 toomust를 추가 하는 가상 컴퓨터에에서도 존재 hello 동일한 위치 및 hello 네트워크 인터페이스로 구독 합니다.|
    |서브넷|예|선택한 hello 가상 네트워크 내에서 서브넷을 선택 합니다. Hello 서브넷을 변경할 수 있습니다 만들어질 tooafter hello 네트워크 인터페이스에 할당 됩니다.|
    |개인 IP 주소 할당|예| 이 설정에 hello IPv4 주소에 대 한 hello 할당 방법을 선택 합니다. Hello 할당 메서드를 다음 중에서 선택할: **동적:** Azure 선택한 hello 서브넷의 hello 주소 공간에서 사용 가능한 주소를 자동으로 할당이 옵션을 선택 하면 됩니다. Azure는 hello에 된 (할당 취소) 상태를 중지 한 후에 hello 가상 컴퓨터를 시작할 때 다른 주소 tooa 네트워크 인터페이스를 할당할 수 있습니다. hello 주소 남아 hello hello에 된 (할당 취소) 상태를 중지 하지 않고 hello 가상 컴퓨터를 다시 시작 하는 경우 동일 합니다. **정적:** 이 옵션을 선택 하면 수동으로 선택한 hello 서브넷의 hello 주소 공간 내에서 사용 가능한 IP 주소를 할당 해야 합니다. 변경 하는 또는 hello 네트워크 인터페이스는 삭제 될 때까지 고정 주소를 변경 하지 마십시오. Hello 네트워크 인터페이스를 만든 후 hello 할당 메서드를 변경할 수 있습니다. hello Azure DHCP 서버 hello 가상 컴퓨터의 hello 운영 체제 내에서이 주소 toohello 네트워크 인터페이스에 할당합니다.|
    |네트워크 보안 그룹|아니요| 너무 설정 된 상태로 둡니다**None**, 기존 선택 [네트워크 보안 그룹](virtual-networks-nsg.md), 또는 [네트워크 보안 그룹 만들기](virtual-networks-create-nsg-arm-pportal.md)합니다. 네트워크 보안 그룹을 사용 하면 네트워크 인터페이스 내부 및 외부로 toofilter 네트워크 트래픽이 있습니다. 0 개 또는 한 네트워크 보안 그룹 tooa 네트워크 인터페이스를 적용할 수 있습니다. 0 개 또는 한 네트워크 보안 그룹도 적용 될 수 toohello 서브넷 hello 네트워크 인터페이스에 할당 됩니다. 적용 된 tooa 네트워크 인터페이스와 hello 서브넷 hello 네트워크 인터페이스 네트워크 보안 그룹의 경우 할당 된 경우에 따라 예기치 않은 결과가 발생할 합니다. hello 읽을 tootroubleshoot 네트워크 보안 그룹 축소할된 toonetwork 인터페이스 및 서브넷을 [네트워크 보안 그룹 문제 해결](virtual-network-nsg-troubleshoot-portal.md#nsg) 문서.|
    |구독|예|Azure [구독](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) 중 하나를 선택합니다. hello 가상 컴퓨터를 연결 하 여 네트워크 인터페이스 tooand hello 가상 네트워크를 연결한 hello에 toomust 존재 동일 구독 합니다.|
    |개인 IP 주소(IPv6)|아니요| 이 확인란을 선택 하면 IPv6 주소는 할당 된 toohello 네트워크 인터페이스, 또한 toohello IPv4 주소 toohello 네트워크 인터페이스에 할당 합니다. Hello 참조 [IPv6](#IPv6) 와 네트워크 인터페이스가 i p v 6의 사용에 대 한 중요 한 정보에 대 한이 문서의 섹션. Hello IPv6 주소에 대 한 할당 메서드를 선택할 수 없습니다. Tooassign IPv6 주소를 선택 하면 hello 동적 방법으로 할당 됩니다.
    |IPv6 이름 (때 hello만 표시 **개인 IP 주소 (IPv6)** 확인란이 선택 되어) |예, 경우 hello **개인 IP 주소 (IPv6)** 확인란이 선택 되어 있습니다.| 이 이름은 tooa hello 네트워크 인터페이스에 대 한 보조 IP 구성에 할당 됩니다. Hello에 IP 구성에 대 한 자세한 정보 [네트워크 인터페이스 설정을 보고](#view-network-interface-settings) 이 문서의 섹션.|
    |리소스 그룹|예|기존 [리소스 그룹](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group)을 선택하거나 리소스 그룹을 만듭니다. 네트워크 인터페이스 수에 hello 동일 없거나, 연결 하는 hello 가상 컴퓨터와 다른 리소스 그룹 또는 hello 가상 네트워크에 연결 합니다.|
    |위치|예|hello 가상 컴퓨터를 연결 하 여 네트워크 인터페이스 tooand hello 가상 네트워크를 연결한 동일 hello에 toomust 존재 [위치](https://azure.microsoft.com/regions), 영역 tooas 라고도 합니다.|

만들 때, hello 포털은 공용 IP 주소를 만들고 할당 tooa 네트워크 인터페이스 hello 포털을 사용 하 여 가상 컴퓨터를 만들 때 있지만 hello 포털 공용 IP 주소 toohello 네트워크 인터페이스 hello 옵션 tooassign 제공 하지 않습니다. toolearn을 만든 후 tooadd 공용 IP 주소 toohello 네트워크 인터페이스 하는 방법을 읽고 hello [관리 IP 주소](virtual-network-network-interface-addresses.md) 문서. Toocreate 공용 IP 주소와 네트워크 인터페이스를 사용 하도록 하려는 경우에 hello CLI 또는 PowerShell toocreate hello 네트워크 인터페이스를 사용 해야 합니다.

>[!Note]
> 연결 된 tooa 가상 컴퓨터와 가상 컴퓨터 hello hello 네트워크 인터페이스는 후에 MAC 주소 toohello 네트워크 인터페이스를 azure 할당은 처음으로 hello를 시작 합니다. Azure toohello 네트워크 인터페이스를 매기는 hello MAC 주소를 지정할 수 없습니다. hello 네트워크 인터페이스 삭제 될 때까지 MAC 주소 할당은 유지 toohello 네트워크 인터페이스 hello 또는 hello 개인 IP 주소가 할당 toohello hello 주 네트워크 인터페이스의 기본 IP 구성을 변경 합니다. IP 주소 및 IP 구성이, hello 읽기에 대 한 자세한 toolearn [관리 IP 주소](virtual-network-network-interface-addresses.md) 문서.

**명령**

|도구|명령|
|---|---|
|CLI|[az network nic create](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[새-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|

## <a name="view-network-interface-settings"></a>네트워크 인터페이스 설정 확인

네트워크 인터페이스를 만든 후에는 대부분의 설정을 확인하고 변경할 수 있습니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) 계정과 구독에 대 한 hello 네트워크 참가자 역할에 대 한 즉 (최소한) 할당 된 권한입니다. 읽기 hello [Azure 역할 기반 액세스 제어에 대 한 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) tooaccounts 역할 및 사용 권한 할당에 대 한 자세한 문서 toolearn 합니다.
2. Hello 텍스트를 포함 하는 hello 상자에서 *리소스 검색* hello Azure 포털의 hello 위쪽 입력 *네트워크 인터페이스*합니다. 때 **네트워크 인터페이스** 나타납니다 hello 검색 결과에를 클릭 합니다.
3. Hello에 **네트워크 인터페이스** 나타나는 블레이드 hello 네트워크 인터페이스에 대 한 설정을 변경 하거나 tooview를 클릭 합니다.
4. hello 다음에 설정이 정리 되어 선택한 hello 네트워크 인터페이스에 대해 나타나는 hello 블레이드:
    - **개요:** hello IP 주소 할당 tooit, hello 가상 네트워크/서브넷 hello 네트워크 인터페이스에 할당 되 고 hello 가상 컴퓨터 hello 네트워크 인터페이스가 너무 연결 된 같은 hello 네트워크 인터페이스에 대 한 정보를 제공 (선택 된 경우 연결 된 tooone). hello 다음 그림에 나와 명명 된 네트워크 인터페이스에 대 한 hello 개요 설정을 **mywebserver256**: ![네트워크 인터페이스 개요](./media/virtual-network-network-interface/nic-overview.png) 네트워크 인터페이스 tooa 다른 리소스 그룹을 이동할 수 있습니다 또는 클릭 하 여 구독 (**변경**) 다음 toohello **리소스 그룹** 또는 **구독 이름**합니다. Hello 네트워크 인터페이스를 이동 하면 함께 모든 관련된 toohello 네트워크 인터페이스 리소스를 이동 해야 합니다. Hello 네트워크 인터페이스 연결된 tooa 가상 컴퓨터인 경우 예를 들어 이동 해야 hello 가상 컴퓨터 및 기타 가상 컴퓨터 관련 리소스입니다. toomove 네트워크 인터페이스 hello 읽을 [리소스 tooa 새 리소스 그룹이 나 구독 이동](../azure-resource-manager/resource-group-move-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json#use-portal) 문서. hello 문서는 사전 요구 사항 및 사용 하 여 toomove 리소스 hello Azure 포털, PowerShell 및 Azure CLI hello 방법을 나열 합니다.
    - **IP 구성:** tooIP 구성을 할당 된 공용 및 개인 IPv4 및 IPv6 주소는 다음과 같습니다. IPv6 주소는 tooan IP 구성에 할당 된 hello 주소가 표시 되지 않습니다. IP 구성 하 고 hello에 tooadd 및 제거 하는 IP 주소 하는 방법에 대 한 자세한 [구성할 IP 주소는 Azure 네트워크 인터페이스에 대 한](virtual-network-network-interface-addresses.md) 문서. 또한 IP 전달 및 서브넷 할당도 이 섹션에서 구성합니다. toolearn hello 읽을 이러한 설정에 대 한 자세한 [IP 전달을 사용할지](#enable-or-disable-ip-forwarding) 및 [서브넷 할당을 변경](#change-subnet-assignment) 이 문서의 섹션.
    - **DNS 서버:** 어떤 DNS 서버는 네트워크 인터페이스에 의해 할당 된 hello Azure DHCP 서버를 지정할 수 있습니다. hello 네트워크 인터페이스 수 hello 설정을 상속 hello에서 가상 네트워크 hello 네트워크 인터페이스, 할당 또는에 할당 된 hello 가상 네트워크에 대 한 hello 설정을 재정의 하는 사용자 지정 설정이 있습니다. 표시 되는 내용 toomodify, hello의 단계를 완료 hello [변경 DNS 서버](#change-dns-servers) 이 문서의 섹션.
    - **네트워크 보안 그룹 (NSG):** (있는 경우) toohello 네트워크 인터페이스를 연결 된 NSG는 표시 합니다. NSG에는 hello 네트워크 인터페이스에 대 한 인바운드 및 아웃 바운드 규칙 toofilter 네트워크 트래픽이 포함 됩니다. NSG 연결된 toohello 네트워크 인터페이스 이면 hello hello NSG를 연결된 표시의 이름입니다. 표시 되는 내용 toomodify, hello의 단계를 완료 hello [네트워크 보안 그룹 연결 관리](virtual-network-manage-nsg-arm-portal.md#manage-associations) 문서.
    - **속성:** 키 (비어 있음 hello 네트워크 인터페이스 연결 된 tooa 가상 컴퓨터가 없는 경우), MAC 주소를 포함 하 여 hello 네트워크 인터페이스에 대 한 설정 및 구독에 있는 hello 표시 됩니다.
    - **효과적인 보안 규칙:** hello 네트워크 인터페이스는 가상 컴퓨터를 실행 하는 연결 된 tooa 이며 NSG 연결된 toohello 네트워크 인터페이스, 할당 된 hello 서브넷 또는 둘 다 하는 경우 보안 규칙 나열 됩니다. 표시 내용에 대해 자세히 toolearn 읽을 hello [네트워크 보안 그룹 문제 해결](virtual-network-nsg-troubleshoot-portal.md#nsg) 문서. hello 읽을 Nsg에 대 한 자세한 toolearn [네트워크 보안 그룹](virtual-networks-nsg.md) 문서.
    - **유효 경로:** hello 네트워크 인터페이스는 연결 된 tooa 실행 중인 가상 컴퓨터 경로가 나열 됩니다. hello 경로 hello Azure 기본 경로, 모든 사용자 정의 경로 (UDR) 및 hello 서브넷 hello 네트워크 인터페이스에 할당 된에 대 한 있을 수 있는 BGP 경로 모두의 조합입니다. 표시 내용에 대해 자세히 toolearn 읽을 hello [경로 문제를 해결](virtual-network-routes-troubleshoot-portal.md#view-effective-routes-for-a-network-interface) 문서. Azure 기본 및 hello 읽을 UDRs에 대 한 자세한 toolearn [사용자 정의 경로](virtual-networks-udr-overview.md) 문서.
    - **일반적인 Azure 리소스 관리자 설정:** toolearn hello 읽을 일반적인 Azure 리소스 관리자 설정에 대 한 자세한 [활동 로그](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#activity-logs), [액세스 제어 (IAM)](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#access-control), [태그 ](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags), [잠급니다](../azure-resource-manager/resource-group-lock-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json), 및 [자동화 스크립트](../azure-resource-manager/resource-manager-export-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json#export-the-template-from-resource-group) 문서입니다.

**명령**

IPv6 주소는 tooa 네트워크 인터페이스에 할당 된 hello 주소를 할당 하지만 hello 할당 된 주소 반환 되지 않는 hello 사실 hello PowerShell 출력을 반환 합니다. CLI 반환 주소 hello hello 팩트 할당 되지만 반환 하는 hello 마찬가지로, *null* hello 주소에 대 한 출력에 있습니다.

|도구|명령|
|---|---|
|CLI|[az 네트워크 nic 목록](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#list) hello 구독의; tooview 네트워크 인터페이스 [az 네트워크 nic 표시](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#show) 네트워크 인터페이스에 대 한 tooview 설정|
|PowerShell|[Get AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) tooview 네트워크 인터페이스는 네트워크 인터페이스에 대 한 hello 구독 또는 뷰 설정|

## <a name="change-dns-servers"></a>DNS 서버 변경

hello DNS 서버 hello 가상 컴퓨터 운영 체제 내에서 hello Azure DHCP 서버 toohello 네트워크 인터페이스에 의해 할당 됩니다. hello DNS 서버가 할당은 hello DNS 서버 설정이 모든 네트워크 인터페이스에 대 한 합니다. 네트워크 인터페이스에 대 한 이름 확인 설정에 대해 자세히 toolearn 참조 [가상 컴퓨터에 대 한 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md)합니다. hello 네트워크 인터페이스 hello 가상 네트워크에서 hello 설정을 상속 하거나 hello 가상 네트워크에 대 한 hello 설정을 재정의 하는 고유한 고유한 설정을 사용할 수 있습니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) 계정과 구독에 대 한 hello 네트워크 참가자 역할에 대 한 즉 (최소한) 할당 된 권한입니다. 읽기 hello [Azure 역할 기반 액세스 제어에 대 한 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) tooaccounts 역할 및 사용 권한 할당에 대 한 자세한 문서 toolearn 합니다.
2. Hello 텍스트를 포함 하는 hello 상자에서 *리소스 검색* hello Azure 포털의 hello 위쪽 입력 *네트워크 인터페이스*합니다. 때 **네트워크 인터페이스** 나타납니다 hello 검색 결과에를 클릭 합니다.
3. Hello에 **네트워크 인터페이스** 나타나는 블레이드 hello 네트워크 인터페이스에 대 한 설정을 변경 하거나 tooview를 클릭 합니다.
4. 선택한 hello 네트워크 인터페이스에 대 한 hello 블레이드에서 클릭 **DNS 서버** 아래 **설정을**합니다.
5. 다음 중 하나를 클릭합니다:
    - **가상 네트워크 (기본값)에서 상속**: hello 가상 네트워크 hello 네트워크 인터페이스에 할당 된에 대해 정의 된 옵션 tooinherit hello DNS 서버 설정 선택 합니다. Hello 가상 네트워크 수준에서 사용자 지정 DNS 서버 또는 hello Azure 제공 DNS 서버 정의 됩니다. hello Azure 제공 DNS 서버를 해결할 수 toohello 할당 된 리소스에 대 한 호스트 이름이 동일한 가상 네트워크입니다. FQDN은 toodifferent 가상 네트워크에 할당 된 리소스에 대 한 사용된 tooresolve 수 있어야 합니다.
    - **사용자 지정**: 여러 가상 네트워크에서 고유한 DNS 서버 tooresolve 이름을 구성할 수 있습니다. Hello IP 주소를 입력 하려는 DNS 서버로 toouse hello 서버의 합니다. toothis 네트워크 인터페이스 및 재정의에 할당 된 hello 가상 네트워크 hello 네트워크 인터페이스에 대 한 DNS 설정을 지정 하는 hello DNS 서버 주소 할당 됩니다.
6. **Save**를 클릭합니다.

**명령**

|도구|명령|
|---|---|
|CLI|[az network nic update](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterface](/powershell/module/azurerm.network/set-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="enable-or-disable-ip-forwarding"></a>IP 전달을 사용하거나 사용하지 않도록 설정

IP 전달을 사용 hello 가상 컴퓨터 네트워크 인터페이스에 연결 되어 있습니다.
- 보내지지 tooany toohello 네트워크 인터페이스를 할당 된 hello IP 구성의 할당 된 hello IP 주소 중 하나에 대 한 네트워크 트래픽을 수신 합니다.
- 네트워크 인터페이스의 IP 구성의 한 할당 된 tooone hello 보다 다른 원본 IP 주소와 네트워크 트래픽을 전송 합니다.

hello 설정은 toohello 연결 된 가상 컴퓨터가 가상 컴퓨터 요구 tooforward hello 트래픽을 수신 하는 모든 네트워크 인터페이스에 대해 활성화 되어야 합니다. 가상 컴퓨터에 여러 네트워크 인터페이스 또는 단일 네트워크 인터페이스 연결 tooit 여부 트래픽을 전달할 수 있습니다. IP 전달을 Azure 설정 이지만, hello 가상 컴퓨터에는 방화벽, WAN 최적화 및 부하 분산 응용 프로그램 등의 응용 프로그램 수 tooforward hello 트래픽에도 실행 해야 합니다. 가상 컴퓨터가 실행 되는 네트워크 응용 프로그램, hello 가상 컴퓨터는 참조 된 tooas 네트워크 가상 어플라이언스 경우가 많습니다. Hello에 준비 toodeploy 네트워크 가상 어플라이언스의 목록을 볼 수 있습니다 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances)합니다. IP 전달은 일반적으로 사용자 정의 경로와 함께 사용됩니다. hello 읽기 사용자 정의 경로 대 한 자세한 toolearn [사용자 정의 경로](virtual-networks-udr-overview.md) 문서.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) 계정과 구독에 대 한 hello 네트워크 참가자 역할에 대 한 즉 (최소한) 할당 된 권한입니다. 읽기 hello [Azure 역할 기반 액세스 제어에 대 한 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) tooaccounts 역할 및 사용 권한 할당에 대 한 자세한 문서 toolearn 합니다.
2. Hello 텍스트를 포함 하는 hello 상자에서 *리소스 검색* hello Azure 포털의 hello 위쪽 입력 *네트워크 인터페이스*합니다. 때 **네트워크 인터페이스** 나타납니다 hello 검색 결과에를 클릭 합니다.
3. Hello에 **네트워크 인터페이스** 나타나는 블레이드 hello 네트워크 인터페이스에 대 한 전달 IP를 사용 하지 않도록 설정 하거나 tooenable를 클릭 합니다.
4. 선택한 hello 네트워크 인터페이스에 대 한 hello 블레이드에서 클릭 **IP 구성을** hello에 **설정을** 섹션.
5. 클릭 **Enabled** 또는 **비활성화** toochange hello 설정 (기본 설정).
6. **Save**를 클릭합니다.

**명령**

|도구|명령|
|---|---|
|CLI|[az network nic update](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterface](/powershell/module/azurerm.network/set-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-subnet-assignment"></a>서브넷 할당 변경

Hello 서브넷 하지만 hello 가상 네트워크가 아니라, 네트워크 인터페이스에 할당 된 변경할 수 있습니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) 계정과 구독에 대 한 hello 네트워크 참가자 역할에 대 한 즉 (최소한) 할당 된 권한입니다. 읽기 hello [Azure 역할 기반 액세스 제어에 대 한 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) tooaccounts 역할 및 사용 권한 할당에 대 한 자세한 문서 toolearn 합니다.
2. Hello 텍스트를 포함 하는 hello 상자에서 *리소스 검색* hello Azure 포털의 hello 위쪽 입력 *네트워크 인터페이스*합니다. 때 **네트워크 인터페이스** 나타납니다 hello 검색 결과에를 클릭 합니다.
3. Hello에 **네트워크 인터페이스** 나타나는 블레이드 hello 네트워크 인터페이스에 대 한 설정을 변경 하거나 tooview를 클릭 합니다.
4. 클릭 **IP 구성을** 아래 **설정을** 선택한 hello 네트워크 인터페이스에 대 한 hello 블레이드에서 합니다. 모든 IP 구성에 대 한 모든 개인 IP 주소 목록에 없으면 **(정적)** 다음 toothem hello 다음 단계를 완료 하 여 hello IP 주소 할당 메서드 toodynamic를 변경 해야 합니다. 모든 개인 IP 주소 할당이 지정 된 hello 동적 할당 메서드 toochange hello 서브넷 hello 네트워크 인터페이스에 대 한 할당 되어야 합니다. Hello 주소 hello 동적 메서드가 할당 되어 있으면 toostep 5를 계속 합니다. 모든 IPv4 주소 hello 정적 할당 메서드에 할당 되어 있으면 다음 단계 toochange hello 할당 메서드 toodynamic hello를 완료 합니다.
    - Hello IP 구성을 toochange hello IP 구성의 hello 목록에서 IPv4 주소 할당 방법에 대 한를 클릭 합니다.
    - Hello 블레이드에서 나타나는 hello IP 구성에 대 한 클릭 **동적** hello에 대 한 **할당** 메서드. Hello 정적 할당 방법으로 IPv6 주소를 할당할 수 없습니다.
    - **Save**를 클릭합니다.
5. 원하는 tooconnect hello 네트워크 인터페이스 toofrom hello hello 서브넷을 선택 **서브넷** 드롭 다운 목록입니다.
6. **Save**를 클릭합니다. 새 동적 주소는 hello 새 서브넷에 대 한 hello 서브넷 주소 범위에서 할당 됩니다. Hello 네트워크 인터페이스 tooa 새 서브넷에 할당 하면 hello 새 서브넷 주소 범위에서 고정 IPv4 주소를 할당할 수 있습니다. 추가, 변경 및 hello 읽기는 네트워크 인터페이스에 대 한 IP 주소를 제거 하는 방법에 대 한 자세한 toolearn [관리 IP 주소](virtual-network-network-interface-addresses.md) 문서.

**명령**

|도구|명령|
|---|---|
|CLI|[az network nic ip-config update](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/set-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="delete-a-network-interface"></a>네트워크 인터페이스 삭제

네트워크 인터페이스 연결된 tooa 가상 컴퓨터가 없으면으로 삭제할 수 있습니다. 첫 번째 위치 hello (할당 취소 됨) 가상 컴퓨터를 중지 하는 hello에 상태 연결된 tooa 가상 컴퓨터인 경우 해야 합니다, 그리고 hello 네트워크 인터페이스를 삭제 하려면 먼저 다음 hello 가상 컴퓨터에서 hello 네트워크 인터페이스를 분리 합니다. 가상 컴퓨터에서 네트워크 인터페이스 toodetach hello에서 단계를 완료 hello [가상 컴퓨터에서 네트워크 인터페이스 분리](virtual-network-network-interface-vm.md#vm-remove-nic) hello 섹션 [네트워크 인터페이스를 추가 / 제거](virtual-network-network-interface-vm.md) 문서. 가상 컴퓨터를 삭제 하는 모든 네트워크 인터페이스 연결 된 tooit, 분리 하지만 hello 네트워크 인터페이스를 삭제 하지 않습니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) 계정과 구독에 대 한 hello 네트워크 참가자 역할에 대 한 즉 (최소한) 할당 된 권한입니다. 읽기 hello [Azure 역할 기반 액세스 제어에 대 한 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) tooaccounts 역할 및 사용 권한 할당에 대 한 자세한 문서 toolearn 합니다.
2. Hello 텍스트를 포함 하는 hello 상자에서 *리소스 검색* hello Azure 포털의 hello 위쪽 입력 *네트워크 인터페이스*합니다. 때 **네트워크 인터페이스** 나타납니다 hello 검색 결과에를 클릭 합니다.
3. 마우스 오른쪽 단추로 클릭 hello 네트워크 인터페이스 누르고 toodelete 원하는 **삭제**합니다.
4. 클릭 **예** hello 네트워크 인터페이스의 tooconfirm 삭제 합니다.

모든 MAC 하는 네트워크 인터페이스를 삭제 하거나 IP 주소 할당 tooit 때 해제 됩니다.

**명령**

|도구|명령|
|---|---|
|CLI|[az network nic delete](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmNetworkInterface](/powershell/module/azurerm.network/remove-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="next-steps"></a>다음 단계
hello 다음 문서를 읽을 toocreate 가상 컴퓨터를 여러 개의 네트워크 인터페이스 또는 IP 주소:

**명령**

|작업|도구|
|---|---|
|여러 NIC를 사용하여 VM 만들기|[CLI](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|여러 IPv4 주소가 있는 단일 NIC VM 만들기|[CLI](virtual-network-multiple-ip-addresses-cli.md), [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|Azure Load Balancer 뒤에 개인 IPv6 주소가 있는 단일 NIC VM 만들기|[CLI](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [Azure Resource Manager 템플릿](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
