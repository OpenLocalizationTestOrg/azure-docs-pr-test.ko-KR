---
title: "Azure 네트워크 인터페이스에 대 한 IP 주소 aaaConfigure | Microsoft Docs"
description: "Tooadd,이 변경 하 고 네트워크 인터페이스에 대 한 개인 및 공용 IP 주소를 제거 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 1e5ea6c65d93be9b1fda5d807500a0823c94c89c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-change-or-remove-ip-addresses-for-an-azure-network-interface"></a>Azure 네트워크 인터페이스용 IP 주소 추가, 변경 또는 제거

Tooadd,이 변경 하 고 네트워크 인터페이스에 대 한 공용 및 개인 IP 주소를 제거 하는 방법에 대해 알아봅니다. Tooa 네트워크 인터페이스에 할당 된 개인 IP 주소는 Azure 가상 네트워크와 연결 된 네트워크의 다른 리소스와 가상 컴퓨터 toocommunicate 사용 하도록 설정 합니다. 또한 개인 IP 주소에 아웃 바운드 통신 toohello를 예측할 수 없는 IP 주소를 사용 하 여 인터넷 수 있습니다. A [공용 IP 주소](virtual-network-public-ip-address.md) tooa 할당 된 네트워크 인터페이스 hello 인터넷에서에서 인바운드 통신 tooa 가상 컴퓨터를 사용 합니다. 또한 hello 주소에 아웃 바운드 통신을 hello 가상 컴퓨터 toohello 예측 가능한 IP 주소를 사용 하 여 인터넷에서에서 수 있습니다. 자세한 내용은 [Azure에서 아웃바운드 연결 이해](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json)를 참조하세요. 

Toocreate 해야 할 경우, 변경 또는 삭제 하는 네트워크 인터페이스 읽기 hello [네트워크 인터페이스를 관리](virtual-network-network-interface.md) 문서. Tooadd 네트워크 인터페이스 tooor 가상 컴퓨터에서 네트워크 인터페이스를 제거 해야 할 경우, hello 읽기 [네트워크 인터페이스를 추가 / 제거](virtual-network-network-interface-vm.md) 문서. 


## <a name="before-you-begin"></a>시작하기 전에

이 문서의 섹션의 단계를 완료 하기 전에 작업을 수행 하는 hello를 완료 합니다.

- 검토 hello [Azure 제한](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) 공용 및 개인 IP 주소에 대 한 제한에 대 한 문서 toolearn 합니다.
- Toohello Azure에에서 로그인 [포털](https://portal.azure.com), Azure 명령줄 인터페이스 (CLI) 또는 Azure 계정으로 Azure PowerShell. 아직 Azure 계정이 없으면 [평가판 계정](https://azure.microsoft.com/free)에 등록합니다.
- 이 문서에서는 toocomplete 작업 명령이 PowerShell을 사용 하는 경우 [Azure PowerShell 설치 및 구성](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다. Hello 가장 최신 버전을 설치 하는 hello Azure PowerShell commandlet의 확인 합니다. 예제를 보려면으로 PowerShell 명령에 대 한 도움말 tooget 입력 `get-help <command> -full`합니다.
- 이 문서에서는 toocomplete 작업 명령을 Azure CLI (명령줄 인터페이스)를 사용 하는 경우 [설치 및 구성 hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다. Hello 최신 버전의 hello Azure CLI 설치 되어 있는지 확인 합니다. CLI 명령에 대 한 도움말 tooget 입력 `az <command> --help`합니다. 설치 hello CLI 및 해당 필수 구성 요소는 대신 Azure 클라우드 셸 hello를 사용할 수 있습니다. Azure 클라우드 셸 hello hello Azure 포털 내에서 직접 실행할 수 있는 무료 Bash 셸의입니다. Hello Azure CLI 사전 설치 및 toouse 사용자 계정으로 구성 된이 있습니다. toouse hello 클라우드 셸 클릭 hello 클라우드 셸 **> _** hello hello 위쪽에 단추 [포털](https://portal.azure.com)합니다.

## <a name="add-ip-addresses"></a>IP 주소 추가

만큼 추가할 수 있습니다 [개인](#private) 및 [공용](#public) [IPv4](#ipv4) hello에 나열 된 hello 제한 내에서 필요한 tooa 네트워크 인터페이스로 주소 [Azure 제한 ](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) 문서. (하지만 hello 네트워크 인터페이스를 만들 때 hello 포털 tooadd 개인 IPv6 주소 tooa 네트워크 인터페이스를 사용할 수 있습니다) hello 포털 tooadd IPv6 주소 tooan 기존 네트워크 인터페이스를 사용할 수 없습니다. PowerShell을 사용 하거나 CLI tooadd 개인 IPv6 주소 tooone hello 수 [보조 IP 구성](#secondary) (으로 기존 보조 IP 구성이) 기존 네트워크 인터페이스가 없는 연결 tooa 가상 컴퓨터입니다. 모든 도구 tooadd 공용 IPv6 주소 tooa 네트워크 인터페이스를 사용할 수 없습니다. IPv6 주소 사용에 대한 자세한 내용은 [IPv6](#ipv6)을 참조하세요. 

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) 계정과 구독에 대 한 hello 네트워크 참가자 역할에 대 한 즉 (최소한) 할당 된 권한입니다. 읽기 hello [Azure 역할 기반 액세스 제어에 대 한 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) tooaccounts 역할 및 사용 권한 할당에 대 한 자세한 문서 toolearn 합니다.
2. Hello 텍스트를 포함 하는 hello 상자에서 *리소스 검색* hello Azure 포털의 hello 위쪽 입력 *네트워크 인터페이스*합니다. 때 **네트워크 인터페이스** 나타납니다 hello 검색 결과에를 클릭 합니다.
3. Hello에 **네트워크 인터페이스** 나타나는 블레이드 hello 네트워크 인터페이스에 대 한 tooadd IPv4 주소 지정 하려면 클릭 합니다.
4. 클릭 **IP 구성을** hello에 **설정을** 선택한 hello 네트워크 인터페이스에 대 한 hello 블레이드의 섹션입니다.
5. 클릭 **+ 추가** hello 블레이드에서 열리면 IP 구성에 대 한 합니다.
6. Hello 다음을 지정 하 고 클릭 **확인** tooclose hello **IP 추가 구성** 블레이드:

    |설정|Required?|세부 정보|
    |---|---|---|
    |이름|예|Hello 네트워크 인터페이스에 대 한 고유 해야 합니다.|
    |형식|예|IP 구성 tooan 기존 네트워크 인터페이스를 추가 하 고 각 네트워크 인터페이스 포함 해야 하는 [기본](#primary) IP 구성 하는 수 밖에 **보조**합니다.|
    |개인 IP 주소 할당 방법|예|[**동적** ](#dynamic) hello에 된 (할당 취소) 상태를 중지 한 후 hello 가상 컴퓨터를 다시 시작 하는 경우 주소를 변경할 수 있습니다. Azure 할당 hello 서브넷 hello 네트워크 인터페이스의 hello 주소 공간에서 사용 가능한 주소에 연결 됩니다. [**정적** ](#static) 주소 hello 네트워크 인터페이스 삭제 될 때까지 해제 되지 않습니다. 현재 다른 IP 구성 사용 하 고 있지 않은 hello 서브넷 주소 공간 범위에서 IP 주소를 지정 합니다.|
    |공용 IP 주소|아니요|**사용 안 함:** 없는 공용 IP 주소 리소스는 현재 연결된 toohello IP 구성 합니다. **사용:** 기존 IPv4 공용 IP 주소를 선택하거나 새 공용 IP 주소를 만듭니다. toocreate 공용 IP 주소를 읽는 방법 toolearn hello [공용 IP 주소](virtual-network-public-ip-address.md#create-a-public-ip-address) 문서.|
7. Hello에 hello 지침을 완료 하 여 보조 개인 IP 주소 toohello 가상 컴퓨터 운영 체제를 수동으로 추가 [toovirtual 컴퓨터 운영 체제의 여러 IP 주소를 할당](virtual-network-multiple-ip-addresses-portal.md#os-config) 문서. 참조 [개인](#private) 수동으로 IP 주소 tooa 가상 컴퓨터 운영 체제를 추가 하기 전에 특별 한 고려 사항에 대 한 IP 주소입니다. 모든 공용 IP 주소 toohello 가상 컴퓨터 운영 체제를 추가 하지 마십시오.

**명령**

|도구|명령|
|---|---|
|CLI|[az network nic ip-config create](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Add-AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/add-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-ip-address-settings"></a>IP 주소 설정 변경

변경 hello 고정 IPv4 주소는 IPv4 주소의 toochange hello 할당 메서드를 할 수 있습니다 또는 변경 hello 공용 IP 주소 할당 tooa 네트워크 인터페이스. 가상 컴퓨터에서 보조 네트워크 인터페이스와 연결 된 보조 IP 구성의 hello 개인 IPv4 주소를 변경 하려는 경우 (에 대 한 자세한 내용은 [기본 및 보조 네트워크 인터페이스](virtual-network-network-interface-vm.md#about)), 전체 hello 가상 hello에 컴퓨터가 hello 다음 단계를 완료 하기 전에 (할당 취소) 상태를 중지 합니다. 

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) 계정과 구독에 대 한 hello 네트워크 참가자 역할에 대 한 즉 (최소한) 할당 된 권한입니다. 읽기 hello [Azure 역할 기반 액세스 제어에 대 한 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) tooaccounts 역할 및 사용 권한 할당에 대 한 자세한 문서 toolearn 합니다.
2. Hello 텍스트를 포함 하는 hello 상자에서 *리소스 검색* hello Azure 포털의 hello 위쪽 입력 *네트워크 인터페이스*합니다. 때 **네트워크 인터페이스** 나타납니다 hello 검색 결과에를 클릭 합니다.
3. Hello에 **네트워크 인터페이스** 나타나는 블레이드 hello 네트워크 인터페이스에 대 한 IP 주소 설정을 변경 하거나 tooview를 클릭 합니다.
4. 클릭 **IP 구성을** hello에 **설정을** 선택한 hello 네트워크 인터페이스에 대 한 hello 블레이드의 섹션입니다.
5. Toomodify hello 블레이드에서 열리면 IP 구성에 대 한 hello 목록에서 원하는 hello IP 구성을 클릭 합니다.
6. Hello 설정을 원하는 대로 hello 설정에 대 한 hello 정보를 사용 하 여 hello의 6 단계에서 변경 [IP 구성을 추가](#create-ip-config) 이 문서의 섹션. 클릭 **저장** tooclose hello 블레이드 hello IP 구성 변경에 대 한 합니다.

>[!NOTE]
>Hello 주 네트워크 인터페이스에 여러 IP 구성은 hello hello 기본 IP 구성의 개인 IP 주소를 변경 하는 경우 수동으로 재할당 해야 hello 기본 및 보조 IP 주소 toohello 네트워크 인터페이스 창 내에서 (not 필수 Linux 용). hello 읽을 toomanually 할당는 운영 체제 내에서 IP 주소 tooa 네트워크 인터페이스 [toovirtual 컴퓨터에 여러 IP 주소 할당](virtual-network-multiple-ip-addresses-portal.md#os-config) 문서. 참조 [개인](#private) 수동으로 IP 주소 tooa 가상 컴퓨터 운영 체제를 추가 하기 전에 특별 한 고려 사항에 대 한 IP 주소입니다. 모든 공용 IP 주소 toohello 가상 컴퓨터 운영 체제를 추가 하지 마십시오.

**명령**

|도구|명령|
|---|---|
|CLI|[az network nic ip-config update](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRMNetworkInterfaceIpConfig](/powershell/module/azurerm.network/set-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="remove-ip-addresses"></a>IP 주소 제거

제거할 수 있습니다 [개인](#private) 및 [공용](#public) 네트워크 인터페이스에서 IP 주소 수 있지만 네트워크 인터페이스는 항상 개인 IPv4 주소가 할당 tooit 하나 이상 있어야 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) 계정과 구독에 대 한 hello 네트워크 참가자 역할에 대 한 즉 (최소한) 할당 된 권한입니다. 읽기 hello [Azure 역할 기반 액세스 제어에 대 한 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) tooaccounts 역할 및 사용 권한 할당에 대 한 자세한 문서 toolearn 합니다.
2. Hello 텍스트를 포함 하는 hello 상자에서 *리소스 검색* hello Azure 포털의 hello 위쪽 입력 *네트워크 인터페이스*합니다. 때 **네트워크 인터페이스** 나타납니다 hello 검색 결과에를 클릭 합니다.
3. Hello에 **네트워크 인터페이스** 나타나는 블레이드 hello 네트워크 인터페이스의 tooremove IP 주소를 클릭 합니다.
4. 클릭 **IP 구성을** hello에 **설정을** 선택한 hello 네트워크 인터페이스에 대 한 hello 블레이드의 섹션입니다.
5. 마우스 오른쪽 단추로 클릭 한 [보조](#secondary) IP 구성 (hello를 삭제할 수 없습니다 [기본](#primary) 구성) toodelete 원하는 누릅니다 **삭제**, 클릭 **예**  tooconfirm hello 삭제 합니다. Hello 구성에 공용 IP 주소 리소스 연관 된 tooit, hello 리소스 hello IP 구성에서 분리는 하지만 hello 리소스는 삭제 되지 않습니다.
6. 닫기 hello **IP 구성을** 블레이드입니다.

**명령**

|도구|명령|
|---|---|
|CLI|[az network nic ip-config delete](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/remove-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="ip-configurations"></a>IP 구성

[개인](#private) 및 (옵션) [공용](#public) tooone IP 주소 할당 또는 더 많은 IP 구성 tooa 네트워크 인터페이스를 할당 합니다. IP 구성에는 다음과 같은 두 종류가 있습니다.

### <a name="primary"></a>보조

각 네트워크 인터페이스에는 기본 IP 구성 하나가 할당됩니다. 기본 IP 구성의 특성은 다음과 같습니다.

- 에 [개인](#private) [IPv4](#ipv4) tooit 할당 된 주소입니다. 개인을 할당할 수 없습니다 [IPv6](#ipv6) 주소 tooa 기본 IP 구성 합니다.
- 있을 [공용](#public) IPv4 주소가 할당 tooit 합니다. 공용 IPv6 주소 tooa 기본 또는 보조 IP 구성을 할당할 수 없습니다. 그러나 트래픽 tooa 가상 컴퓨터의 개인 IPv6 주소를 분산 하는 공용 IPv6 tooan Azure 부하 분산 장치를 로드할 수 있는 주소 할당, 수 있습니다. 자세한 내용은 [IPv6 관련 세부 정보 및 제한](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#details-and-limitations)을 참조하세요.

### <a name="secondary"></a>주

또한 기본 IP 구성 tooa 네트워크 인터페이스 있을 0 개 이상의 보조 IP 구성 tooit 할당 합니다. 보조 IP 구성의 특징은 다음과 같습니다.

- 개인 IPv4 또는 IPv6 주소 할당 tooit이 있어야 합니다. Hello 주소가 i p v 6 이면 hello 네트워크 인터페이스에서 하나의 보조 IP 구성을 하나만 사용할 수 있습니다. Hello 주소가 i p v 4 이면 hello 네트워크 인터페이스의 tooit 할당 하는 여러 보조 IP 구성 있을 수 있습니다. toolearn 개수 개인 및 공용 IPv4 주소를 할당할 수 있습니다 tooa 네트워크 인터페이스에 대 한 자세한 참조 hello [Azure 제한](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) 문서.  
- Hello 개인 IP 주소가 i p v 4 이면 공용 IPv4 주소가 할당 tooit을 가질 수도 있습니다. Hello 개인 IP 주소가 i p v 6 이면는 공용 IPv4 또는 IPv6 주소 toohello IP 구성을 할당할 수 없습니다. 특별 한와 같은 여러 IP 주소 tooa 네트워크 인터페이스 할당은 시나리오에 도움이 됩니다.
    - 단일 서버에서 IP 주소와 SSL 인증서를 사용하여 여러 웹 사이트 또는 서비스를 호스트할 수 있습니다.
    - 가상 컴퓨터가 방화벽, 부하 분산 장치 등의 네트워크 가상 어플라이언스로 사용되는 경우
    - hello hello 네트워크 인터페이스 tooan Azure 부하 분산 장치 백 엔드 풀에 대 한 개인 IPv4 주소 입력의 모든 기능 tooadd hello 합니다. Hello 지난에서 hello 기본 IPv4 주소만 hello 주 네트워크 인터페이스에 대 한 백 엔드 풀 tooa 추가할 수 없습니다. toolearn tooload 여러 IPv4 구성을 분산 하는 방법에 대 한 자세한 참조 hello [부하 분산 여러 IP 구성은](../load-balancer/load-balancer-multiple-ip.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 문서. 
    - hello 기능 tooload 하나 이상의 IPv6 주소 할당된 tooa 네트워크 인터페이스를 조정 합니다. toolearn tooload tooa 개인 IPv6 주소를 분산 하는 방법에 대 한 자세한 참조 hello [부하를 분산 IPv6 주소](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 문서.


## <a name="address-types"></a>주소 유형

다음 IP 주소 tooan 유형의으로 hello를 할당할 수 [IP 구성](#ip-configurations):

### <a name="private"></a>개인

개인 [IPv4](#ipv4) 주소 또는 기타 연결 된 네트워크 가상 네트워크의 다른 리소스와 가상 컴퓨터 toocommunicate 사용 하도록 설정 합니다. 가상 컴퓨터, 인바운드 통신 없습니다와 통신할 수 있습니다 hello 가상 컴퓨터는 개인 아웃 바운드 [IPv6](#ipv6) 예외적으로 주소입니다. 가상 컴퓨터는 hello Azure 부하 분산 장치는 IPv6 주소를 사용 하 여 통신할 수 있습니다. 자세한 내용은 [IPv6 관련 세부 정보 및 제한](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#details-and-limitations)을 참조하세요. 

기본적으로 hello Azure DHCP 서버는 hello에 대 한 hello 개인 IPv4 주소가 할당 [기본 IP 구성](#primary) hello 가상 컴퓨터 운영 체제 내에서 hello 네트워크 인터페이스 toohello 네트워크 인터페이스의 합니다. 하지 않으면 필요한 하지 직접 설정 해야 hello 가상 컴퓨터의 운영 체제 내에서 네트워크 인터페이스의 hello IP 주소입니다. 

> [!WARNING]
> 가상 컴퓨터의 운영 체제 내에서 네트워크 인터페이스의 기본 IP 주소 hello 다르면 적이 hello 개인 IPv4 주소가 할당 toohello hello 주 네트워크 인터페이스의 기본 IP 구성으로 설정 하는 IPv4 주소 hello tooa 연결 된 경우 Azure 내에서 가상 컴퓨터를 연결 toohello 가상 컴퓨터는 손실 됩니다.

경우 hello 가상 컴퓨터의 운영 체제 내에서 네트워크 인터페이스의 필요한 toomanually hello IP 주소를 설정 하는 시나리오가 있습니다. 예를 들어 수동으로 설정 해야 hello 기본 및 보조 IP 주소는 Windows 운영 체제의 여러 IP 주소 tooan Azure 가상 컴퓨터를 추가 하는 경우. Linux 가상 컴퓨터에 대 한 toomanually 집합 hello 보조 IP 주소에만 할 수 있습니다. 참조 [추가 IP 주소 tooa VM 운영 체제](virtual-network-multiple-ip-addresses-portal.md#os-config) 대 한 자세한 내용은 합니다. Hello 운영 체제 내에서 hello IP 주소를 수동으로 설치할 때 항상 hello (아닌 정적 동적) 할당 방법을 사용 하 여 네트워크 인터페이스에 대 한 hello 주소 toohello IP 구성을 할당 하는 것이 좋습니다. Hello 정적 메서드를 사용 하 여 hello 주소를 할당 하면 Azure 내에서 hello 주소가 변경 되지 않습니다. 할당 tooan IP 구성을 toochange hello 주소, 필요한 경우는 것이 좋습니다는 있습니다.

1. tooensure hello 가상 컴퓨터는 hello Azure DHCP 서버에서 주소를 수신, hello IP 주소 hello 운영 체제 및 다시 시작 hello 가상 컴퓨터 내에서 뒤로 tooDHCP의 hello 할당을 변경 합니다.
2. 중지 (할당 취소) hello 가상 컴퓨터.
3. Azure 내에서 hello IP 구성에 대 한 hello IP 주소를 변경 합니다.
4. Hello 가상 컴퓨터를 시작 합니다.
5. [수동으로 구성](virtual-network-multiple-ip-addresses-portal.md#os-config) hello 보조 IP hello 운영 체제 (그리고 windows hello 기본 IP 주소) 내의 주소 toomatch Azure 내에서 설정 하는 것입니다.
 
Hello 이전 단계에 따라 개인 IP 주소 할당 toohello 네트워크 인터페이스 및 가상 컴퓨터의 운영 체제 내에서 Azure hello와 남아 hello 동일 합니다. 운영 체제 내에서 IP 주소를 수동으로 설정 하는 구독 내에서 가상 컴퓨터는 Azure를 추가 하십시오 tookeep 트랙 [태그](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags) toohello 가상 컴퓨터. 예를 들어 "IP 주소 할당: 정적" 등을 사용할 수 있습니다. 이러한 방식으로 hello 운영 체제 내에서 hello IP 주소를 수동으로 설정 하는 구독 내에서 hello 가상 컴퓨터를 쉽게 찾을 수 있습니다.

또한 tooenabling hello 동일 하지만, 또는 연결 된 가상 네트워크를 개인 IP 주소도 내에서 다른 리소스와 가상 컴퓨터 toocommunicate 실행 하는 가상 컴퓨터 toocommunicate 아웃 바운드 toohello를 인터넷 수 있습니다. 아웃 바운드 연결은 원본 네트워크 주소 Azure tooan 예측할 수 없는 공용 IP 주소에 의해 변환 됩니다. Azure 아웃 바운드 인터넷이 연결 hello 읽기에 대 한 자세한 toolearn [Azure 아웃 바운드 인터넷 연결](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 문서. Hello 인터넷에서에서 인바운드 tooa 가상 컴퓨터의 개인 IP 주소를 통신할 수 없습니다.

### <a name="public"></a>공용

공용 IP 주소는 hello 인터넷에서에서 인바운드 연결 tooa 가상 컴퓨터를 사용 합니다. 인터넷 아웃 바운드 연결 toohello 예측 가능한 IP 주소를 사용 합니다. 자세한 내용은 [Azure에서 아웃바운드 연결 이해](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json)를 참조하세요. 필요 하지만 공용 IP 주소 tooan IP 구성을 할당할 수 있습니다. 공용 IP 주소 tooa 가상 컴퓨터를 할당 하지 않으면, 해당 개인 IP 주소를 사용 하 여 인터넷 아웃 바운드 toohello 여전히 통신할 수 있습니다. hello를 읽고, 공용 IP 주소에 대 한 자세한 toolearn [공용 IP 주소](virtual-network-public-ip-address.md) 문서.

제한은 toohello 수가 개인 및 tooa를 할당할 수 있는 공용 IP 주소 네트워크 인터페이스. 자세한 내용은 hello 읽을 [Azure 제한](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) 문서.

> [!NOTE]
> Azure 가상 컴퓨터의 개인 IP 주소 tooa 공용 IP 주소를 변환합니다. 결과적으로, hello 운영 체제가 tooit 할당 된 공용 IP 주소를 인식 하지 않는 이므로 없습니다 필요 tooever 수동으로 hello 운영 체제 내에서 공용 IP 주소를 할당 합니다.

## <a name="assignment-methods"></a>할당 방법

할당 메서드를 다음 hello를 사용 하 여 공용 및 개인 IP 주소가 할당 됩니다.

### <a name="dynamic"></a>동적

동적 개인 IPv4 및 IPv6(옵션) 주소는 기본적으로 할당됩니다. Hello에 hello 가상 컴퓨터가 배치 되 면 동적 주소가 변경 되어 중지 (할당 취소) 상태 다음 작업을 시작 합니다. Hello 가상 컴퓨터의 hello 수명에 대 한 IPv4 주소 toochange 않으려면 hello 정적 메서드를 사용 하 여 hello 주소를 할당 합니다. 만 hello 동적 할당 방법을 사용 하 여 개인 IPv6 주소를 할당할 수 있습니다. 공용 IPv6 주소 tooan IP 구성이 두 방법 중 하나를 사용 하 여 할당할 수 없습니다.

### <a name="static"></a>정적

가상 컴퓨터를 삭제할 때까지 hello 정적 메서드를 사용 하 여 할당 된 주소를 변경 하지 마십시오. Hello 서브넷 hello 네트워크 인터페이스에 대 한 개인 IPv4 주소 tooan IP 구성을 hello 주소 공간에서 수동으로 할당 합니다. (선택 사항) 공개 또는 개인 IPv4 주소 tooan IP 구성을 할당할 수 있습니다. 공개 또는 개인 IPv6 주소 tooan IP 구성을 할당할 수 없습니다. Azure 공용 고정 IPv4 주소를 할당 하는 방법에 대 한 자세한 toolearn 참조 hello [공용 IP 주소](virtual-network-public-ip-address.md) 문서.

## <a name="ip-address-versions"></a>IP 주소 버전

Hello 버전 주소를 할당 하는 경우 뒤에 지정할 수 있습니다.

### <a name="ipv4"></a>IPv4

각 네트워크 인터페이스에는 [개인](#private) [IPv4](#ipv4) 주소가 할당된 [기본](#primary) IP 구성 하나가 있어야 합니다. 각각 IPv4 개인 IP 주소와 IPv4 [공용](#public) IP 주소(옵션)를 포함하는 [보조](#secondary) IP 구성을 하나 이상 추가할 수 있습니다.

### <a name="ipv6"></a>IPv6

0 개 또는 1 개인을 할당할 수 있습니다 [IPv6](#ipv6) 네트워크 인터페이스의 주소가 tooone 보조 IP 구성 합니다. hello 네트워크 인터페이스에는 모든 기존 보조 IP 구성을 가질 수 없습니다. Hello 포털을 사용 하 여 IPv6 주소는 IP 구성을 추가할 수 없습니다. PowerShell 또는 CLI tooadd IP 구성 hello를 사용 하 여 개인 IPv6 주소 tooan 기존 네트워크 인터페이스. hello 네트워크 인터페이스 연결된 tooan 기존 VM 수 없습니다.

> [!NOTE]
> Hello 포털을 사용 하 여 IPv6 주소는 네트워크 인터페이스를 만들 수, hello 포털을 사용 하는 기존 네트워크 인터페이스 tooa 새로운 또는 기존 가상 컴퓨터를 추가할 수 없습니다. 개인 IPv6 주소로 PowerShell 또는 hello Azure CLI 2.0 toocreate 네트워크 인터페이스를 사용 하 고 가상 컴퓨터를 만들 때 hello 네트워크 인터페이스를 연결 합니다. Tooit tooan 기존 가상 컴퓨터를 할당 하는 개인 IPv6 주소가 네트워크 인터페이스를 연결할 수 없습니다. (포털, CLI 또는 PowerShell) 다양 한 도구를 사용 하 여 모든 네트워크 인터페이스 연결 tooa 가상 컴퓨터에 대 한 개인 IPv6 주소 tooan IP 구성을 추가할 수 없습니다.

공용 IPv6 주소 tooa 기본 또는 보조 IP 구성을 할당할 수 없습니다.

## <a name="next-steps"></a>다음 단계
toocreate hello 다음 문서를 읽을 다른 IP 구성 사용 하 여 가상 컴퓨터:

|작업|도구|
|---|---|
|여러 NIC를 사용하여 VM 만들기|[CLI](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|여러 IPv4 주소가 있는 단일 NIC VM 만들기|[CLI](virtual-network-multiple-ip-addresses-cli.md), [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|Azure Load Balancer 뒤에 개인 IPv6 주소가 있는 단일 NIC VM 만들기|[CLI](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [Azure Resource Manager 템플릿](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
