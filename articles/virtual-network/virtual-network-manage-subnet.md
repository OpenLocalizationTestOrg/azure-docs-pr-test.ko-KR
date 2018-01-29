---
title: "Azure Virtual Network 서브넷 추가, 변경 또는 삭제 | Microsoft 문서"
description: "Azure에서 가상 네트워크 서브넷을 추가, 변경 또는 삭제하는 방법을 알아봅니다."
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
ms.openlocfilehash: 85ba6ef3e51c339a77eb9b4198c4f87e2a64cf09
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="add-change-or-delete-a-virtual-network-subnet"></a>가상 네트워크 서브넷 추가, 변경 또는 삭제

가상 네트워크 서브넷을 추가, 변경 또는 삭제하는 방법을 알아봅니다. 

가상 네트워크에 대해 잘 모르는 경우 서브넷을 추가, 변경 또는 삭제하기 전에 [Azure Virtual Network 개요](virtual-networks-overview.md) 및 [가상 네트워크 만들기, 변경 또는 삭제](virtual-network-manage-network.md)를 확인하는 것이 좋습니다. 가상 네트워크에 배포된 모든 Azure 리소스는 가상 네트워크 내의 서브넷에 배포됩니다. 일반적으로 다음을 위해 하나의 가상 네트워크 내에 여러 서브넷이 생성됩니다.
- **서브넷 간의 트래픽 필터링**. 서브넷에 네트워크 보안 그룹을 적용하여 가상 네트워크에 있는 모든 리소스(예: 가상 컴퓨터)에 대한 인바운드 및 아웃바운드 네트워크 트래픽을 필터링할 수 있습니다. 네트워크 보안 그룹을 만드는 방법에 대한 자세한 내용은 [네트워크 보안 그룹 만들기](virtual-networks-create-nsg-arm-pportal.md)를 참조하세요.
- **서브넷 간 라우팅 제어**. 트래픽이 서브넷 간에 자동으로 라우팅되도록 Azure에서 기본 경로를 만듭니다. 사용자 정의 경로를 만들어 Azure 기본 경로를 재정의할 수 있습니다. 사용자 정의 경로에 대한 자세한 내용은 [사용자 정의 경로 만들기](virtual-network-create-udr-arm-ps.md)를 참조하세요. 

이 문서에서는 Azure Resource Manager 배포 모델을 사용하여 만든 가상 네트워크에 대한 서브넷을 추가, 변경 및 삭제하는 방법을 설명합니다.
 
## <a name="before"></a>시작하기 전에

이 문서에 설명된 작업을 시작하기 전에 다음 전제 조건을 완료합니다.

- 가상 네트워크에서 처음 작업하는 경우 [첫 번째 Azure Virtual Network 만들기](virtual-network-get-started-vnet-subnet.md)의 연습을 검토하는 것이 좋습니다. 이 연습을 통해 가상 네트워크에 친숙해질 수 있습니다.
- 가상 네트워크에 대한 제한 사항은 [Azure 제한](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits)을 참조하세요.
- Azure 계정을 사용하여 Azure Portal, Azure CLI(명령줄 도구) 또는 Azure PowerShell에 로그인합니다. Azure 계정이 없으면 [평가판 계정](https://azure.microsoft.com/free)에 등록합니다.
- PowerShell 명령을 사용하여 이 문서의 작업을 수행하려면 먼저 [Azure PowerShell을 설치 및 구성](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json)해야 합니다. 최신 버전의 Azure PowerShell cmdlet을 설치했는지 확인합니다. 예제에서 PowerShell 명령에 대한 도움말을 보려면 `get-help <command> -full`을 입력합니다.
- Azure CLI 명령을 사용하여 이 문서에서 설명하는 작업을 완료하려면 다음 중 하나를 수행해야 합니다.
    - [Azure CLI를 설치 및 구성합니다](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). 최신 버전의 Azure CLI를 설치했는지 확인합니다.
    - Azure Cloud Shell을 사용합니다. CLI 및 해당 종속성을 설치하는 대신 Azure Cloud Shell을 사용할 수 있습니다. Azure Cloud Shell은 Azure Portal에서 직접 실행할 수 있는 평가판 Bash 셸입니다. Azure CLI가 사전 설치되어 계정에서 사용하도록 구성되어 있습니다. Cloud Shell을 사용하려면 Azure Portal 위쪽의 Cloud Shell(**>_**) 아이콘을 클릭합니다. 

  Azure CLI 명령에 대한 도움말을 보려면 `az <command> --help`를 입력합니다.

## <a name="create-subnet"></a>서브넷 추가

서브넷을 추가하려면 다음을 수행합니다.

1. 구독에 대한 네트워크 참가자 역할에 권한(최소)이 할당된 계정으로 [포털](https://portal.azure.com)에 로그인합니다. 계정에 역할 및 권한을 할당하는 방법에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어의 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)을 참조하세요.
2. 포털 검색 상자에 **가상 네트워크**를 입력합니다. 검색 결과에서 **가상 네트워크**를 클릭합니다.
3. **가상 네트워크** 블레이드에서 서브넷을 추가하려는 가상 네트워크를 클릭합니다.
4. 가상 네트워크 블레이드에서 **서브넷**을 클릭합니다.
5. **+서브넷**을 클릭합니다.
6. **서브넷 추가** 블레이드에서 다음 매개 변수에 대한 값을 입력합니다.
    - **이름:** 가상 네트워크 내에서 고유해야 합니다.
    - **주소 범위:** 범위는 가상 네트워크의 주소 공간 내에서 고유해야 합니다. 범위는 가상 네트워크 내에서 다른 서브넷 주소 범위와 겹칠 수 없습니다. CIDR(Classless Inter-Domain Routing) 표기법을 사용하여 주소 공간을 지정해야 합니다. 예를 들어 주소 공간이 10.0.0.0/16인 가상 네트워크에서 서브넷 주소 공간을 10.0.0.0/24로 정의할 수 있습니다. 지정할 수 있는 최소 범위는 /29이며, 서브넷에 대해 8개의 IP 주소를 제공합니다. Azure는 프로토콜 준수를 위해 각 서브넷의 첫 번째 및 마지막 주소를 예약합니다. 세 개의 추가 주소가 Azure 서비스를 사용하기 위해 예약되어 있습니다. 결과적으로 주소 범위가 /29인 서브넷을 정의하면 서브넷에 사용할 수 있는 3개의 IP 주소가 만들어집니다. 가상 네트워크를 VPN Gateway에 연결하려면 게이트웨이 서브넷을 만들어야 합니다. [게이트웨이 서브넷에 대한 특정 주소 범위 고려 사항](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub)에서 대해 자세히 알아보세요. 특정 조건에서는 서브넷을 추가한 후에 주소 범위를 변경할 수 있습니다. 서브넷 주소 범위를 변경하는 방법에 대한 자세한 내용은 이 문서에서 [서브넷 설정 변경](#change-subnet)을 참조하세요.
    - **네트워크 보안 그룹:** 필요한 경우 기존 네트워크 보안 그룹을 서브넷에 연결하여 서브넷에 대한 인바운드 및 아웃바운드 네트워크 트래픽 필터링을 제어할 수 있습니다. 네트워크 보안 그룹은 가상 네트워크와 동일한 구독 및 위치에 있어야 합니다. 또한 Resource Manager 배포 모델을 사용하여 만들어야 합니다. 네트워크 보안 그룹을 만드는 방법에 대한 자세한 내용은 [네트워크 보안 그룹](virtual-networks-create-nsg-arm-pportal.md)을 참조하세요.
    - **경로 테이블:** 필요한 경우 기존 네트워크 경로 테이블을 서브넷에 연결하여 다른 네트워크에 대한 네트워크 트래픽 라우팅을 제어할 수 있습니다. 경로 테이블은 가상 네트워크와 동일한 구독 및 위치에 있어야 합니다. 또한 Resource Manager 배포 모델을 사용하여 만들어야 합니다. 경로 테이블을 만드는 방법에 대한 자세한 내용은 [사용자 정의 경로](virtual-network-create-udr-arm-ps.md)를 참조하세요.
    - **사용자**: 기본 제공 역할 또는 사용자 지정 역할을 사용하여 서브넷에 대한 액세스를 제어할 수 있습니다. 역할과 사용자를 할당하여 서브넷에 액세스하는 방법에 대한 자세한 내용은 [역할 할당을 사용하여 Azure 리소스에 대한 액세스 관리](../active-directory/role-based-access-control-configure.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-access)를 참조하세요.
7. 선택한 가상 네트워크에 서브넷을 추가하려면 **확인**을 클릭합니다.

**명령**

|도구|명령|
|---|---|
|Azure CLI|[az network vnet subnet create](/cli/azure/network/vnet/subnet?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json), [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-subnet"></a>서브넷 설정 변경

서브넷에 있는 리소스를 관리하여 서브넷에 대한 사용자 액세스, 경로 테이블 및 네트워크 보안 그룹을 변경할 수 있습니다. 이러한 설정에 대해 알아보려면 [서브넷 추가](#create-subnet)에서 6단계를 참조하세요. 서브넷의 주소 공간을 변경하려면 먼저 서브넷에 있는 모든 리소스를 삭제해야 합니다. 리소스 삭제를 수행하는 단계는 리소스에 따라 다릅니다. 서브넷에 있는 리소스를 삭제하는 방법에 대해 알아보려면 삭제하려는 각 리소스 종류의 설명서를 참조하세요. 서브넷의 주소 범위를 변경하려면

1. 구독에 대한 네트워크 참가자 역할에 권한(최소)이 할당된 계정으로 [포털](https://portal.azure.com)에 로그인합니다. 계정에 역할 및 권한을 할당하는 방법에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어의 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)을 참조하세요.
2. 포털 검색 상자에 **가상 네트워크**를 입력합니다. 검색 결과에서 **가상 네트워크**를 클릭합니다.
3. **가상 네트워크** 블레이드에서 서브넷 주소 범위를 변경할 가상 네트워크를 클릭합니다.
4. 주소 범위를 변경할 서브넷을 클릭합니다.
5. 서브넷 블레이드에서 **주소 범위** 상자에 새 주소 범위를 입력합니다. 범위는 가상 네트워크의 주소 공간 내에서 고유해야 합니다. 범위는 가상 네트워크 내에서 다른 서브넷 주소 범위와 겹칠 수 없습니다. CIDR 표기법을 사용하여 주소 공간을 지정해야 합니다. 예를 들어 주소 공간이 10.0.0.0/16인 가상 네트워크에서 서브넷 주소 공간을 10.0.0.0/24로 정의할 수 있습니다. 지정할 수 있는 최소 범위는 /29이며, 서브넷에 대해 8개의 IP 주소를 제공합니다. Azure는 프로토콜 준수를 위해 각 서브넷의 첫 번째 및 마지막 주소를 예약합니다. 세 개의 추가 주소가 Azure 서비스를 사용하기 위해 예약되어 있습니다. 결과적으로 주소 범위가 /29인 서브넷에는 사용할 수 있는 3개의 IP 주소가 있습니다. 가상 네트워크를 VPN Gateway에 연결하려면 게이트웨이 서브넷을 만들어야 합니다. [게이트웨이 서브넷에 대한 특정 주소 범위 고려 사항](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub)에서 대해 자세히 알아보세요. 특정 조건에서 서브넷을 만든 후에 주소 범위를 변경할 수 있습니다. 서브넷 주소 범위를 변경하는 방법에 대한 자세한 내용은 이 문서에서 [서브넷 설정 변경](#change-subnet)을 참조하세요.
6. **Save**를 클릭합니다.

**명령**

|도구|명령|
|---|---|
|Azure CLI|[az network vnet subnet update](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="delete-subnet"></a>서브넷 삭제

서브넷에 리소스가 없는 경우에만 해당 서브넷을 삭제할 수 있습니다. 서브넷에 리소스가 있으면 서브넷을 삭제하기 전에 먼저 서브넷에 있는 리소스를 삭제해야 합니다. 리소스 삭제를 수행하는 단계는 리소스에 따라 다릅니다. 서브넷에 있는 리소스를 삭제하는 방법에 대해 알아보려면 삭제하려는 각 리소스 종류의 설명서를 참조하세요. 서브넷을 삭제하려면

1. 구독에 대한 네트워크 참가자 역할에 권한(최소)이 할당된 계정으로 [포털](https://portal.azure.com)에 로그인합니다. 계정에 역할 및 권한을 할당하는 방법에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어의 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)을 참조하세요.
2. 포털 검색 상자에 **가상 네트워크**를 입력합니다. 검색 결과에서 **가상 네트워크**를 클릭합니다.
3. **가상 네트워크** 블레이드에서 서브넷을 삭제하려는 가상 네트워크를 클릭합니다.
4. 가상 네트워크 블레이드의 **설정**에서 **서브넷**을 클릭합니다.
5. 서브넷 블레이드에 표시되는 서브넷 목록에서 삭제하려는 서브넷을 마우스 오른쪽 단추로 클릭하고 **삭제**를 클릭한 다음 **예**를 클릭하여 해당 서브넷을 삭제합니다.

**명령**

|도구|명령|
|---|---|
|Azure CLI|[az network vnet delete](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/remove-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="next-steps"></a>다음 단계

서브넷에서 가상 컴퓨터를 만들려면 [가상 네트워크 만들기 및 서브넷에서 VM 배포](virtual-network-get-started-vnet-subnet.md#create-vms)를 참조하세요.
