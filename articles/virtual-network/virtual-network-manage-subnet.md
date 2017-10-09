---
title: "aaaAdd, 변경 또는 Azure 가상 네트워크 서브넷을 삭제할 | Microsoft Docs"
description: "Tooadd, 변경 또는 Azure에서 가상 네트워크 서브넷 삭제 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: jdial
ms.openlocfilehash: 0d6d813b7e2fc52a00a87f6c6714ab5b7ca589ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-change-or-delete-a-virtual-network-subnet"></a>가상 네트워크 서브넷 추가, 변경 또는 삭제

Tooadd, 변경 또는 가상 네트워크 서브넷 삭제 방법에 대해 알아봅니다. 

가상 네트워크에 대해 잘 모르는 경우 서브넷을 추가, 변경 또는 삭제하기 전에 [Azure Virtual Network 개요](virtual-networks-overview.md) 및 [가상 네트워크 만들기, 변경 또는 삭제](virtual-network-manage-network.md)를 확인하는 것이 좋습니다. 가상 네트워크에 배포된 모든 Azure 리소스는 가상 네트워크 내의 서브넷에 배포됩니다. 일반적으로 다음을 위해 하나의 가상 네트워크 내에 여러 서브넷이 생성됩니다.
- **서브넷 간의 트래픽 필터링**. 인바운드 및 아웃 바운드 네트워크 보안 그룹 toosubnets toofilter를 적용할 수 네트워크 트래픽을 hello 가상 네트워크에 있는 모든 리소스 (예: 가상 컴퓨터)에 대 한 합니다. 네트워크 보안 그룹 toocreate 확인 하는 방법에 대해 더 알아봅니다을 toolearn [네트워크 보안 그룹을 만들고](virtual-networks-create-nsg-arm-pportal.md)합니다.
- **서브넷 간 라우팅 제어**. 트래픽이 서브넷 간에 자동으로 라우팅되도록 Azure에서 기본 경로를 만듭니다. 사용자 정의 경로를 만들어 Azure 기본 경로를 재정의할 수 있습니다. 사용자 정의 경로 대 한 자세한 정보는 toolearn 참조 [사용자 정의 경로 만듭니다](virtual-network-create-udr-arm-ps.md)합니다. 

이 문서에서는 tooadd, 변경 하 고 hello Azure 리소스 관리자 배포 모델을 사용 하 여 만든 가상 네트워크에 서브넷을 삭제 하는 방법을 설명 합니다.
 
## <a name="before"></a>시작하기 전에

이 문서에서 설명 하는 hello 작업을 시작 하기 전에 다음 필수 구성 요소는 hello를 완료 합니다.

- 가상 네트워크와 새 tooworking 인 경우 hello 연습을 검토 하는 것이 좋습니다 [첫 번째 Azure 가상 네트워크를 만든](virtual-network-get-started-vnet-subnet.md)합니다. 이 연습을 통해 가상 네트워크에 친숙해질 수 있습니다.
- 가상 네트워크를 검토에 대 한 제한에 대 한 toolearn [Azure 제한을](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits)합니다.
- Toohello Azure 포털에에서 로그인을 Azure 계정을 사용 하 여 Azure 명령줄 도구 (Azure CLI) 또는 Azure PowerShell hello 합니다. Azure 계정이 없으면 [평가판 계정](https://azure.microsoft.com/free)에 등록합니다.
- 먼저 toouse PowerShell 명령이이 문서에 설명 된 toocomplete hello 작업 하려는 경우 [Azure PowerShell 설치 및 구성](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다. Hello 최신 버전의 Azure PowerShell cmdlet이 설치 된 hello 가졌는지 확인 합니다. hello 예제에서 PowerShell 명령에 대 한 도움말 tooget 입력 `get-help <command> -full`합니다.
- Toouse Azure CLI 명령을이 문서에 설명 된 toocomplete hello 작업 하려는 경우 수행 해야 하거나.
    - [설치 및 구성 hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다. Hello 가장 최신 버전의 Azure CLI를 설치 했는지 확인 합니다.
    - Azure 클라우드 셸 hello를 사용 합니다. CLI hello 및 해당 종속성을 설치 하는 대신 Azure 클라우드 셸 hello를 사용할 수 있습니다. Azure 클라우드 셸 hello hello Azure 포털 내에서 직접 실행할 수 있는 무료 Bash 셸의입니다. Hello Azure CLI 사전 설치 및 toouse 사용자 계정으로 구성 된이 있습니다. toouse hello 클라우드 셸 hello 클라우드 셸 클릭 (**> _**) hello hello Azure 포털 맨 위에 있는 아이콘입니다. 

  Azure CLI 명령 사용 하 여 tooget 도움말 입력 `az <command> --help`합니다.

## <a name="create-subnet"></a>서브넷 추가

tooadd 서브넷:

1. Toohello 로그인 [포털](https://portal.azure.com) 인 계정으로 hello 네트워크 참가자 역할 (최소한) 구독에 대 한 사용 권한이 할당 됩니다. 역할 및 사용 권한 tooaccounts 할당에 대 한 더 toolearn 참조 [Azure 역할 기반 액세스 제어에 대 한 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)합니다.
2. Hello 포털 검색 상자에 입력 **가상 네트워크**합니다. Hello 검색 결과에서 클릭 **가상 네트워크**합니다.
3. Hello에 **가상 네트워크** 블레이드에서 tooadd 서브넷을 원하는 hello 가상 네트워크를 클릭 합니다.
4. Hello 가상 네트워크 블레이드에서 클릭 **서브넷**합니다.
5. **+서브넷**을 클릭합니다.
6. Hello에 **서브넷 추가** 블레이드에서 hello 매개 변수 뒤에 대 한 값을 입력 합니다.
    - **이름**: hello 이름은 hello 가상 네트워크 내에서 고유 해야 합니다.
    - **주소 범위**: hello 범위 hello hello 가상 네트워크 주소 공간 내에서 고유 해야 합니다. hello 범위 hello 가상 네트워크 내에서 다른 서브넷 주소 범위와 겹칠 수 없습니다. 도메인 간 CIDR (Classless Routing) 표기법을 사용 하 여 hello 주소 공간을 지정 해야 합니다. 예를 들어 주소 공간이 10.0.0.0/16인 가상 네트워크에서 서브넷 주소 공간을 10.0.0.0/24로 정의할 수 있습니다. hello 가장 작은 범위를 지정할 수 있습니다 은/29, hello 서브넷에 대 한 8 개의 IP 주소를 제공 하는 합니다. Azure 예약 hello 처음 및 마지막 프로토콜 적합성에 대 한 각 서브넷의 주소입니다. 세 개의 추가 주소가 Azure 서비스를 사용하기 위해 예약되어 있습니다. 결과적으로, / 29 서브넷 정의 범위 결과에 3 개의 사용 가능한 IP 주소가 hello 서브넷의 주소입니다. Tooconnect tooa VPN 게이트웨이 가상 네트워크를 계획 하는 경우 게이트웨이 서브넷을 만들어야 합니다. [게이트웨이 서브넷에 대한 특정 주소 범위 고려 사항](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub)에서 대해 자세히 알아보세요. 특정 조건에서 hello 서브넷 추가 된 후 hello 주소 범위를 변경할 수 있습니다. toochange 서브넷 주소 범위를 확인 하려면 어떻게 해야 toolearn [서브넷 설정 변경](#change-subnet) 이 문서의 내용입니다.
    - **네트워크 보안 그룹**: hello 서브넷 toocontrol와 기존 네트워크 보안 그룹을 연결할 수 필요에 따라 네트워크 트래픽 인바운드 및 아웃 바운드 hello 서브넷에 대 한 필터링 합니다. hello 네트워크 보안 그룹에에서 존재 해야 hello 동일한 구독 및 위치 hello 가상 네트워크와 합니다. 또한 만들어야 하며 hello 리소스 관리자 배포 모델을 사용 하 여 합니다. 네트워크 보안 그룹 toocreate 확인 하는 방법에 대해 더 알아봅니다을 toolearn [네트워크 보안 그룹](virtual-networks-create-nsg-arm-pportal.md)합니다.
    - **경로 테이블**: 필요에 따라 기존 경로 테이블 hello 서브넷 toocontrol 네트워크 트래픽 라우팅을 tooother 네트워크를 연결할 수 있습니다. hello 경로 테이블에에서 존재 해야 hello 동일한 구독 및 위치 hello 가상 네트워크와 합니다. 또한 만들어야 하며 hello 리소스 관리자 배포 모델을 사용 하 여 합니다. toocreate 경로 테이블을 확인 하는 방법에 대해 더 알아봅니다을 toolearn [사용자 정의 경로](virtual-network-create-udr-arm-ps.md)합니다.
    - **사용자가**: 기본 제공 역할 또는 사용자 지정 역할을 사용 하 여 액세스 toohello 서브넷을 제어할 수 있습니다. 역할 및 사용자 tooaccess hello 서브넷 할당에 대 한 더 toolearn 참조 [역할 할당 toomanage 액세스 tooyour Azure를 사용 하 여 리소스](../active-directory/role-based-access-control-configure.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-access)합니다.
7. tooadd hello 서브넷 toohello 가상 네트워크를 선택 하면 클릭 **확인**합니다.

**명령**

|도구|명령|
|---|---|
|Azure CLI|[az network vnet subnet create](/cli/azure/network/vnet/subnet?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json), [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-subnet"></a>서브넷 설정 변경

서브넷에 있는 리소스를 관리 하 여 네트워크 보안 그룹, 경로 테이블 및 사용자 액세스 tooa 서브넷을 변경할 수 있습니다. 이러한 설정에 대 한 toolearn에서 [서브넷을 추가할](#create-subnet), 6 단계를 참조 합니다. 서브넷의 toochange hello 주소 공간을 사용 하도록 하려는 경우 hello 서브넷에 있는 모든 리소스를 먼저 삭제 해야 합니다. hello 단계를 수행 toodelete 리소스 hello 리소스에 따라 달라 집니다. toolearn toodelete 원하는 toodelete 리소스 서브넷의 각 리소스에 대 한 읽기 hello 설명서에 있는 입력 하는 방법입니다. toochange hello 주소는 서브넷에 대 한 범위:

1. Toohello 로그인 [포털](https://portal.azure.com) 인 계정으로 hello 네트워크 참가자 역할 (최소한) 구독에 대 한 사용 권한이 할당 됩니다. 역할 및 사용 권한 tooaccounts 할당에 대 한 더 toolearn 참조 [Azure 역할 기반 액세스 제어에 대 한 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)합니다.
2. Hello 포털 검색 상자에 입력 **가상 네트워크**합니다. Hello 검색 결과에서 클릭 **가상 네트워크**합니다.
3. Hello에 **가상 네트워크** 블레이드에서 toochange 서브넷 주소 범위를 원하는 hello 가상 네트워크를 클릭 합니다.
4. Hello 서브넷 toochange hello 주소 범위를 선택를 클릭 합니다.
5. Hello에 hello 서브넷 블레이드에서 **주소 범위** 상자 hello 새 주소 범위를 입력 합니다. hello 범위는 hello hello 가상 네트워크 주소 공간 내에서 고유 해야 합니다. hello 범위 hello 가상 네트워크 내에서 다른 서브넷 주소 범위와 겹칠 수 없습니다. hello 주소 공간은 CIDR 표기법을 사용 하 여 지정 되어야 합니다. 예를 들어 주소 공간이 10.0.0.0/16인 가상 네트워크에서 서브넷 주소 공간을 10.0.0.0/24로 정의할 수 있습니다. hello 가장 작은 범위를 지정할 수 있습니다 은/29, hello 서브넷에 대 한 8 개의 IP 주소를 제공 하는 합니다. Azure 예약 hello 처음 및 마지막 프로토콜 적합성에 대 한 각 서브넷의 주소입니다. 세 개의 추가 주소가 Azure 서비스를 사용하기 위해 예약되어 있습니다. 결과적으로 주소 범위가 /29인 서브넷에는 사용할 수 있는 3개의 IP 주소가 있습니다. Tooconnect tooa VPN 게이트웨이 가상 네트워크를 계획 하는 경우 게이트웨이 서브넷을 만들어야 합니다. [게이트웨이 서브넷에 대한 특정 주소 범위 고려 사항](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub)에서 대해 자세히 알아보세요. 특정 조건에서 hello 서브넷을 만든 후 hello 주소 범위를 변경할 수 있습니다. toochange 서브넷 주소 범위를 확인 하려면 어떻게 해야 toolearn [서브넷 설정 변경](#change-subnet) 이 문서의 내용입니다.
6. **Save**를 클릭합니다.

**명령**

|도구|명령|
|---|---|
|Azure CLI|[az network vnet subnet update](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="delete-subnet"></a>서브넷 삭제

Hello 서브넷에 리소스가 없는 경우에 서브넷을 삭제할 수 있습니다. Hello 서브넷에 리소스가 있는 경우에 hello 서브넷을 삭제 하기 전에 hello 서브넷에 있는 hello 리소스를 삭제 해야 합니다. hello 단계를 수행 toodelete 리소스 hello 리소스에 따라 달라 집니다. toolearn toodelete 원하는 toodelete 리소스 서브넷의 각 리소스에 대 한 읽기 hello 설명서에 있는 입력 하는 방법입니다. toodelete 서브넷:

1. Toohello 로그인 [포털](https://portal.azure.com) 인 계정으로 hello 네트워크 참가자 역할 (최소한) 구독에 대 한 사용 권한이 할당 됩니다. 역할 및 사용 권한 tooaccounts 할당에 대 한 더 toolearn 참조 [Azure 역할 기반 액세스 제어에 대 한 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)합니다.
2. Hello 포털 검색 상자에 입력 **가상 네트워크**합니다. Hello 검색 결과에서 클릭 **가상 네트워크**합니다.
3. Hello에 **가상 네트워크** 블레이드에서 toodelete에서 서브넷을 원하는 hello 가상 네트워크를 클릭 합니다.
4. 가상 hello에 블레이드에서 아래에서 네트워크 **설정**, 클릭 **서브넷**합니다.
5. Hello 서브넷 블레이드를 마우스 오른쪽 단추로 클릭 hello 서브넷에 표시 되는 서브넷 hello 목록에서 원하는 toodelete, 클릭 **삭제**, 클릭 하 고 **예** toodelete hello 서브넷입니다.

**명령**

|도구|명령|
|---|---|
|Azure CLI|[az network vnet delete](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/remove-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="next-steps"></a>다음 단계

toocreate 가상 컴퓨터는 서브넷에 참조 [hello 서브넷에 Vm을 배포 및 가상 네트워크 만들기](virtual-network-get-started-vnet-subnet.md#create-vms)합니다.
