---
title: "Azure 네트워크 인터페이스 만들기, 변경 또는 삭제 | Microsoft 문서"
description: "네트워크 인터페이스의 정의, 네트워크 인터페이스를 만들고 삭제하는 방법 및 해당 설정을 변경하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 9f1cf113f75bc5a96af8c33d4b83d1bd0f5c6efd
ms.sourcegitcommit: 9292e15fc80cc9df3e62731bafdcb0bb98c256e1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/10/2018
---
# <a name="create-change-or-delete-a-network-interface"></a>네트워크 인터페이스 만들기, 변경 또는 삭제

네트워크 인터페이스를 만들고 삭제하는 방법 및 해당 설정을 변경하는 방법에 대해 알아봅니다. 네트워크 인터페이스를 사용하면 Azure Virtual Machine에서 인터넷, Azure 및 온-프레미스 리소스와 통신할 수 있습니다. Azure Portal을 사용하여 가상 머신을 만들 때 Portal에서는 기본 설정이 포함된 네트워크 인터페이스 하나를 자동으로 만듭니다. 대신 사용자 지정 설정을 사용하여 네트워크 인터페이스를 만들도록 선택할 수 있으며, 가상 컴퓨터를 만들 때 하나 이상의 네트워크 인터페이스를 해당 가상 컴퓨터에 추가할 수 있습니다. 기존 네트워크 인터페이스의 기본 네트워크 인터페이스 설정을 변경할 수도 있습니다. 이 문서에서는 사용자 지정 설정을 사용하여 네트워크 인터페이스를 만들고, 네트워크 필터(네트워크 보안 그룹) 할당/서브넷 할당/DNS 서버 설정/IP 전달 등의 기존 설정을 변경하고, 네트워크 인터페이스를 삭제하는 방법에 대해 설명합니다.

네트워크 인터페이스용 IP 주소를 추가, 변경 또는 제거해야 하는 경우 [IP 주소 관리](virtual-network-network-interface-addresses.md) 문서를 확인하세요. 네트워크 인터페이스를 가상 머신에 추가하거나 가상 머신에서 제거해야 하는 경우에는 [네트워크 인터페이스 추가 또는 제거](virtual-network-network-interface-vm.md) 문서를 확인하세요.


## <a name="before-you-begin"></a>시작하기 전에

이 문서에서 설명하는 섹션의 모든 단계를 수행하려면 다음 작업을 완료해야 합니다.

- [Azure 제한](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) 문서를 검토하여 네트워크 인터페이스에 대한 제한 사항을 알아봅니다.
- Azure 계정으로 Azure [Portal](https://portal.azure.com), Azure CLI(명령줄 인터페이스) 또는 Azure PowerShell에 로그인합니다. 아직 Azure 계정이 없으면 [평가판 계정](https://azure.microsoft.com/free)에 등록합니다.
- PowerShell 명령을 사용하여 이 문서의 작업을 완료하는 경우 [Azure PowerShell을 설치 및 구성](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다. 최신 버전의 Azure PowerShell commandlet을 설치했는지 확인합니다. 예제와 함께 PowerShell 명령에 대한 도움말을 보려면 `get-help <command> -full`을 입력합니다.
- Azure CLI(명령줄 인터페이스) 명령을 사용하여 이 문서의 작업을 완료하는 경우 [Azure CLI를 설치 및 구성](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다. 최신 버전의 Azure CLI를 설치했는지 확인합니다. CLI 명령에 대한 도움말을 보려면 `az <command> --help`를 입력합니다. CLI 및 해당 필수 구성 요소를 설치하는 대신 Azure Cloud Shell을 사용할 수 있습니다. Azure Cloud Shell은 Azure Portal에서 직접 실행할 수 있는 평가판 Bash 셸입니다. Azure CLI가 사전 설치되어 계정에서 사용하도록 구성되어 있습니다. Cloud Shell을 사용하려면 [Portal](https://portal.azure.com) 위쪽의 Cloud Shell **>_** 단추를 클릭합니다.

## <a name="create-a-network-interface"></a>네트워크 인터페이스 만들기

Azure Portal을 사용하여 가상 머신을 만들 때 Portal에서는 기본 설정이 포함된 네트워크 인터페이스 하나를 자동으로 만듭니다. 모든 네트워크 인터페이스 설정을 지정하려는 경우 사용자 지정 설정으로 네트워크 인터페이스를 만든 다음, PowerShell 또는 Azure CLI를 사용하여 가상 머신을 만들 때 해당 네트워크 인터페이스를 가상 머신에 연결하면 됩니다. 네트워크 인터페이스를 만든 다음 PowerShell 또는 Azure CLI를 사용하여 기존 가상 컴퓨터에 추가할 수도 있습니다. 기존 네트워크 인터페이스를 사용하여 가상 머신을 만들거나 네트워크 인터페이스를 가상 머신에 추가하는 방법 또는 기존 가상 머신에서 네트워크 인터페이스를 제거하는 방법에 대해 알아보려면 [네트워크 인터페이스 추가 또는 제거](virtual-network-network-interface-vm.md) 문서를 확인하세요. 네트워크 인터페이스를 만들려면 네트워크 인터페이스를 만들려는 동일 위치 및 구독에 기존 [가상 네트워크](virtual-networks-create-vnet-arm-pportal.md)가 있어야 합니다.

1. 구독에 대한 네트워크 참가자 역할에 권한(최소)이 할당된 계정으로 [Azure Portal](https://portal.azure.com)에 로그인합니다. 계정에 역할 및 권한을 할당하는 방법에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어의 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) 문서를 참조하세요.
2. Azure Portal 위쪽의 *리소스 검색* 텍스트가 있는 상자에서 *네트워크 인터페이스*를 입력합니다. 검색 결과에 표시된 **네트워크 인터페이스**를 클릭합니다.
3. **네트워크 인터페이스** 블레이드가 표시되면 **+ 추가**를 클릭합니다.
4. 표시되는 **네트워크 인터페이스 만들기** 블레이드에서 다음 설정에 대한 값을 입력하거나 선택한 다음 **만들기**를 클릭합니다.

    |설정|Required?|세부 정보|
    |---|---|---|
    |이름|적용|이름은 선택한 리소스 그룹 내에서 고유해야 합니다. 시간이 지남에 따라 Azure 구독에는 여러 개의 네트워크 인터페이스가 추가될 가능성이 많습니다. 여러 네트워크 인터페이스를 더 쉽게 관리할 수 있도록 명명 규칙을 만들 때 적용 가능한 권장 사항은 [명명 규칙](/azure/architecture/best-practices/naming-conventions?toc=%2fazure%2fvirtual-network%2ftoc.json#naming-rules-and-restrictions) 문서를 참조하세요. 네트워크 인터페이스를 만든 후에는 이름을 변경할 수 없습니다.|
    |가상 네트워크|적용|네트워크 인터페이스용 가상 네트워크를 선택합니다. 네트워크 인터페이스와 같은 구독 및 위치에 있는 가상 네트워크에만 네트워크 인터페이스를 할당할 수 있습니다. 네트워크 인터페이스를 만든 후에는 해당 인터페이스가 할당된 가상 네트워크를 변경할 수 없습니다. 네트워크 인터페이스에 추가하는 가상 머신은 네트워크 인터페이스와 같은 위치 및 구독에도 있어야 합니다.|
    |서브넷|적용|선택한 가상 네트워크 내의 서브넷을 선택합니다. 네트워크 인터페이스를 만든 후에 해당 인터페이스가 할당된 서브넷을 변경할 수 있습니다.|
    |개인 IP 주소 할당|적용| 이 설정에서는 IPv4 주소의 할당 방법을 선택합니다. 다음 할당 방법 중에서 선택합니다. **동적:** 이 옵션을 선택하면 선택한 서브넷의 주소 공간에서 사용 가능한 다음 주소가 자동으로 할당됩니다. **고정:** 이 옵션을 선택하면 선택한 서브넷의 주소 공간에서 사용 가능한 IP 주소를 수동으로 할당해야 합니다. 고정 및 동적 주소는 변경하거나 네트워크 인터페이스를 삭제할 때까지 변경되지 않습니다. 네트워크 인터페이스를 만든 후에 할당 방법을 변경할 수 있습니다. Azure DHCP 서버는 이 주소를 가상 머신 운영 체제 내의 네트워크 인터페이스에 할당합니다.|
    |네트워크 보안 그룹|아니요| **없음**으로 설정된 상태로 두거나 기존 [네트워크 보안 그룹](virtual-networks-nsg.md)을 선택하거나 [네트워크 보안 그룹을 만듭니다](virtual-networks-create-nsg-arm-pportal.md). 네트워크 보안 그룹을 사용하면 네트워크 인터페이스 내/외부 네트워크 트래픽을 필터링할 수 있습니다. 네트워크 인터페이스에 네트워크 보안 그룹을 적용하지 않거나 하나를 적용할 수 있습니다. 네트워크 인터페이스가 할당된 서브넷에도 네트워크 보안 그룹을 적용하지 않거나 하나를 적용할 수 있습니다. 네트워크 인터페이스와 네트워크 인터페이스가 할당된 서브넷에 네트워크 보안 그룹을 적용하면 예기치 않은 결과가 발생하는 경우도 있습니다. 네트워크 인터페이스 및 서브넷에 적용된 네트워크 보안 그룹의 문제를 해결하려면 [네트워크 보안 그룹 문제 해결](virtual-network-nsg-troubleshoot-portal.md#nsg) 문서를 확인하세요.|
    |구독|적용|Azure [구독](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) 중 하나를 선택합니다. 네트워크 인터페이스를 연결하는 가상 머신과 네트워크 인터페이스에 연결되는 가상 네트워크가 같은 구독에 있어야 합니다.|
    |개인 IP 주소(IPv6)|아니요| 이 확인란을 선택하면 네트워크 인터페이스에 할당된 IPv4 주소 외에 IPv6 주소가 네트워크 인터페이스에 할당됩니다. 네트워크 인터페이스에서 IPv6을 사용하는 경우와 관련된 중요한 정보는 이 문서의 [IPv6](#IPv6) 섹션을 참조하세요. IPv6 주소에 대해서는 할당 방법을 선택할 수 없습니다. IPv6 주소를 할당하도록 선택하면 주소는 동적 방법으로 할당됩니다.
    |IPv6 이름(**개인 IP 주소(IPv6)** 확인란을 선택해야 표시됨) |예 - **개인 IP 주소(IPv6)** 확인란을 선택하는 경우| 이 이름은 네트워크 인터페이스의 보조 IP 구성에 할당됩니다. IP 구성에 대해 자세히 알아보려면 이 문서의 [네트워크 인터페이스 설정 확인](#view-network-interface-settings) 섹션을 참조하세요.|
    |리소스 그룹|적용|기존 [리소스 그룹](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group)을 선택하거나 리소스 그룹을 만듭니다. 네트워크 인터페이스는 연결하는 가상 머신이나 연결된 가상 네트워크와 같은 리소스 그룹에 있을 수도 있고 다른 리소스 그룹에 있을 수도 있습니다.|
    |위치|적용|네트워크 인터페이스를 연결하는 가상 컴퓨터와 네트워크 인터페이스에 연결되는 가상 네트워크가 같은 [위치](https://azure.microsoft.com/regions)(지역이라고도 함)에 있어야 합니다.|

Portal에서는 네트워크 인터페이스를 만들 때 공용 IP 주소를 네트워크 인터페이스에 할당하는 옵션을 제공하지 않습니다. 하지만 Portal을 사용하여 가상 머신을 만들 때는 공용 IP 주소가 작성되어 네트워크 인터페이스에 할당됩니다. 네트워크 인터페이스를 만든 후 공용 IP 주소를 추가하는 방법을 자세히 알아보려면 [IP 주소 관리](virtual-network-network-interface-addresses.md) 문서를 확인하세요. 공용 IP 주소가 있는 네트워크 인터페이스를 만들려면 CLI 또는 PowerShell을 사용하여 네트워크 인터페이스를 만들어야 합니다.

>[!Note]
> Azure에서는 네트워크 인터페이스가 가상 머신에 연결되고 가상 머신이 처음으로 시작된 후에만 MAC 주소를 네트워크 인터페이스에 할당합니다. Azure에서 네트워크 인터페이스에 할당하는 MAC 주소를 지정할 수는 없습니다. 네트워크 인터페이스를 삭제하거나 기본 네트워크 인터페이스의 기본 IP 구성에 할당된 개인 IP 주소를 변경할 때까지 MAC 주소는 네트워크 인터페이스에 할당된 상태로 유지됩니다. IP 주소 및 IP 구성에 대해 자세히 알아보려면 [IP 주소 관리](virtual-network-network-interface-addresses.md) 문서를 확인하세요.

**명령**

|도구|명령|
|---|---|
|CLI|[az network nic create](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[새-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|

## <a name="view-network-interface-settings"></a>네트워크 인터페이스 설정 확인

네트워크 인터페이스를 만든 후에는 대부분의 설정을 확인하고 변경할 수 있습니다.

1. 구독에 대한 네트워크 참가자 역할에 권한(최소)이 할당된 계정으로 [Azure Portal](https://portal.azure.com)에 로그인합니다. 계정에 역할 및 권한을 할당하는 방법에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어의 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) 문서를 참조하세요.
2. Azure Portal 위쪽의 *리소스 검색* 텍스트가 있는 상자에서 *네트워크 인터페이스*를 입력합니다. 검색 결과에 표시된 **네트워크 인터페이스**를 클릭합니다.
3. 표시되는 **네트워크 인터페이스** 블레이드에서 설정을 보거나 변경하려는 네트워크 인터페이스를 클릭합니다.
4. 선택한 네트워크 인터페이스에 대해 표시되는 블레이드에서 다음 설정이 나열됩니다.
    - **개요:** 네트워크 인터페이스에 할당된 IP 주소, 네트워크 인터페이스가 할당된 가상 네트워크/서브넷, 네트워크 인터페이스가 연결된 가상 머신(가상 머신에 연결되어 있는 경우)와 같은 네트워크 인터페이스 관련 정보를 제공합니다. 다음 그림에서는 **mywebserver256**이라는 네트워크 인터페이스에 대한 개요 설정을 보여 줍니다. ![네트워크 인터페이스 개요](./media/virtual-network-network-interface/nic-overview.png) **리소스 그룹** 또는 **구독 이름** 옆에 있는 (**변경**)을 클릭하여 네트워크 인터페이스를 다른 리소스 그룹 또는 구독으로 이동할 수 있습니다. 네트워크 인터페이스를 이동하는 경우에는 해당 네트워크 인터페이스와 관련된 모든 리소스도 함께 이동해야 합니다. 예를 들어 네트워크 인터페이스가 가상 머신에 연결되어 있는 경우에는 가상 머신 및 기타 가상 머신 관련 리소스도 이동해야 합니다. 네트워크 인터페이스를 이동하려면 [새 리소스 그룹 또는 구독으로 리소스 이동](../azure-resource-manager/resource-group-move-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json#use-portal) 문서를 확인하세요. 필수 조건과 Azure Portal, PowerShell 및 Azure CLI를 사용하여 리소스를 이동하는 방법을 나열하고 있습니다.
    - **IP 구성:** IP 구성에 할당된 공용 및 개인 IPv4/IPv6 주소가 여기에 나열됩니다. IP 구성에 할당된 IPv6 주소는 표시되지 않습니다. IP 구성 및 IP 주소를 추가하고 제거하는 방법에 대해 자세히 알아보려면 [Azure 네트워크 인터페이스용 IP 주소 구성](virtual-network-network-interface-addresses.md) 문서를 참조하세요. 또한 IP 전달 및 서브넷 할당도 이 섹션에서 구성합니다. 이러한 설정에 대해 자세히 알아보려면 이 문서의 [IP 전달 사용/사용 안 함](#enable-or-disable-ip-forwarding) 및 [서브넷 할당 변경](#change-subnet-assignment) 섹션을 참조하세요.
    - **DNS 서버:** Azure DHCP 서버에서 네트워크 인터페이스를 할당하는 DNS 서버를 지정할 수 있습니다. 네트워크 인터페이스는 할당되어 있는 가상 네트워크의 설정을 상속할 수도 있고, 할당되어 있는 가상 네트워크의 설정을 재정의하는 사용자 지정 설정을 포함할 수도 있습니다. 표시되는 항목을 수정하려면 이 문서의 [DNS 서버 변경](#change-dns-servers) 섹션에서 설명하는 단계를 수행합니다.
    - **NSG(네트워크 보안 그룹):** 네트워크 인터페이스에 연결된 NSG를 표시합니다(있는 경우). NSG에는 네트워크 인터페이스의 네트워크 트래픽을 필터링하기 위한 인바운드 및 아웃바운드 규칙이 포함되어 있습니다. NSG가 네트워크 인터페이스에 연결되어 있으면 연결된 NSG의 이름이 표시됩니다. 표시되는 이름을 수정하려면 [네트워크 보안 그룹 연결 관리](virtual-network-manage-nsg-arm-portal.md#manage-associations) 문서의 단계를 완료하세요.
    - **속성:** 네트워크 인터페이스의 MAC 주소(네트워크 인터페이스가 가상 머신에 연결되어 있지 않으면 비어 있음)와 해당 네트워크 인터페이스가 있는 구독을 비롯하여 네트워크 인터페이스에 대한 주요 설정이 표시됩니다.
    - **효과적인 보안 규칙:** 네트워크 인터페이스가 실행 중인 가상 머신에 연결되어 있고 네트워크 인터페이스, 네트워크 인터페이스가 할당된 서브넷 또는 둘 다에 NSG가 연결되어 있으면 보안 규칙이 나열됩니다. 표시되는 항목에 대한 자세한 내용은 [네트워크 보안 그룹 문제 해결](virtual-network-nsg-troubleshoot-portal.md#nsg) 문서를 참조하세요. NSG에 대한 자세한 내용은 [네트워크 보안 그룹](virtual-networks-nsg.md) 문서를 참조하세요.
    - **유효 경로:** 네트워크 인터페이스가 실행 중인 가상 컴퓨터에 연결되어 있으면 경로가 나열됩니다. 경로는 Azure 기본 경로, UDR(사용자 정의 경로) 및 네트워크 인터페이스가 할당된 서브넷에 있을 수 있는 BGP 경로의 조합입니다. 표시되는 항목에 대한 자세한 내용은 [경로 문제 해결](virtual-network-routes-troubleshoot-portal.md#view-effective-routes-for-a-network-interface) 문서를 참조하세요. Azure 기본 경로 및 UDR에 대한 자세한 내용은 [사용자 정의 경로](virtual-networks-udr-overview.md) 문서를 참조하세요.
    - **일반적인 Azure Resource Manager 설정:** 일반적인 Azure Resource Manager 설정에 대한 자세한 내용은 [활동 로그](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#activity-logs), [Access Control(IAM)](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#access-control), [태그](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags), [잠금](../azure-resource-manager/resource-group-lock-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 및 [Automation 스크립트](../azure-resource-manager/resource-manager-export-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json#export-the-template-from-resource-group) 문서를 참조하세요.

**명령**

IPv6 주소가 네트워크 인터페이스에 할당되어 있으면 PowerShell 출력에서는 주소가 할당되어 있다는 정보만 반환되며 할당된 주소는 반환되지 않습니다. 마찬가지로 CLI도 주소가 할당되어 있다는 정보는 반환하지만 주소에 대해서는 출력에 *null*이 반환됩니다.

|도구|명령|
|---|---|
|CLI|구독의 네트워크 인터페이스를 확인하려면 [az network nic list](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#list)를 실행하고, 네트워크 인터페이스의 설정을 확인하려면 [az network nic show](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#show)를 실행합니다.|
|PowerShell|구독의 네트워크 인터페이스를 확인하거나 네트워크 인터페이스의 설정을 확인하려면 [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)를 실행합니다.|

## <a name="change-dns-servers"></a>DNS 서버 변경

DNS 서버는 Azure DHCP 서버에 의해 가상 머신 운영 체제 내의 네트워크 인터페이스에 할당됩니다. 네트워크 인터페이스의 DNS 서버 설정에 지정되어 있는 DNS 서버가 할당됩니다. 네트워크 인터페이스의 이름 확인 설정에 대한 자세한 내용은 [가상 머신의 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md) 문서를 참조하세요. 네트워크 인터페이스는 가상 네트워크에서 설정을 상속할 수도 있고, 가상 네트워크의 설정을 재정의하는 고유한 설정을 사용할 수도 있습니다.

1. 구독에 대한 네트워크 참가자 역할에 권한(최소)이 할당된 계정으로 [Azure Portal](https://portal.azure.com)에 로그인합니다. 계정에 역할 및 권한을 할당하는 방법에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어의 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) 문서를 참조하세요.
2. Azure Portal 위쪽의 *리소스 검색* 텍스트가 있는 상자에서 *네트워크 인터페이스*를 입력합니다. 검색 결과에 표시된 **네트워크 인터페이스**를 클릭합니다.
3. 표시되는 **네트워크 인터페이스** 블레이드에서 설정을 보거나 변경하려는 네트워크 인터페이스를 클릭합니다.
4. 선택한 네트워크 인터페이스에 대한 블레이드의 **설정** 아래에서 **DNS 서버**를 클릭합니다.
5. 다음 중 하나를 클릭합니다:
    - **가상 네트워크에서 상속(기본값)**: 이 옵션을 선택하면 네트워크 인터페이스가 할당되어 있는 가상 네트워크에 대해 정의된 DNS 서버 설정을 상속합니다. 가상 네트워크 수준에서는 사용자 지정 DNS 서버 또는 Azure 제공 DNS 서버가 정의됩니다. Azure에서 제공한 DNS 서버는 동일한 가상 네트워크에 할당된 리소스에 대한 호스트 이름을 확인할 수 있습니다. FQDN을 사용하여 서로 다른 가상 네트워크에 할당된 리소스를 확인해야 합니다.
    - **사용자 지정**: 여러 가상 네트워크에서 이름을 확인하도록 사용자 고유의 DNS 서버를 구성할 수 있습니다. DNS 서버로 사용하려는 서버의 IP 주소를 입력합니다. 여기서 지정하는 DNS 서버 주소는 이 네트워크 인터페이스에만 할당되며, 네트워크 인터페이스가 할당된 가상 네트워크의 모든 DNS 설정을 재정의합니다.
6. **저장**을 클릭합니다.

**명령**

|도구|명령|
|---|---|
|CLI|[az network nic update](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterface](/powershell/module/azurerm.network/set-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="enable-or-disable-ip-forwarding"></a>IP 전달을 사용하거나 사용하지 않도록 설정

IP 전달을 통해 네트워크 인터페이스가 연결된 가상 머신에서 다음 작업을 수행할 수 있습니다.
- 네트워크 인터페이스에 할당된 IP 구성에 할당되어 있는 IP 주소 중 하나를 대상으로 하지 않는 네트워크 트래픽을 받습니다.
- 네트워크 인터페이스의 IP 구성 중 하나에 할당된 것과 소스 IP 주소가 다른 네트워크 트래픽을 보냅니다.

가상 머신에 연결되어 있으며 가상 머신이 전달해야 하는 트래픽을 받는 모든 네트워크 인터페이스에 대해 설정을 활성화해야 합니다. 가상 머신은 네트워크 인터페이스가 하나만 연결되어 있든, 여러 개 연결되어 있든 관계없이 트래픽을 전달할 수 있습니다. IP 전달은 Azure 설정이지만 가상 머신은 방화벽, WAN 최적화 및 부하 분산 응용 프로그램과 같이 트래픽을 전달할 수 있는 응용 프로그램도 실행해야 합니다. 네트워크 응용 프로그램을 실행하는 가상 머신은 네트워크 가상 어플라이언스라고도 합니다. [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances)에서 즉시 배포 가능한 네트워크 가상 어플라이언스 목록을 확인할 수 있습니다. IP 전달은 일반적으로 사용자 정의 경로와 함께 사용됩니다. 사용자 정의 경로에 대해 자세히 알아보려면 [사용자 정의 경로](virtual-networks-udr-overview.md) 문서를 참조하세요.

1. 구독에 대한 네트워크 참가자 역할에 권한(최소)이 할당된 계정으로 [Azure Portal](https://portal.azure.com)에 로그인합니다. 계정에 역할 및 권한을 할당하는 방법에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어의 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) 문서를 참조하세요.
2. Azure Portal 위쪽의 *리소스 검색* 텍스트가 있는 상자에서 *네트워크 인터페이스*를 입력합니다. 검색 결과에 표시된 **네트워크 인터페이스**를 클릭합니다.
3. 표시되는 **네트워크 인터페이스** 블레이드에서 IP 전달을 사용하거나 사용하지 않도록 설정하려는 네트워크 인터페이스를 클릭합니다.
4. 선택한 네트워크 인터페이스에 대한 블레이드의 **설정** 섹션에서 **IP 구성**을 클릭합니다.
5. **사용** 또는 **사용 안 함**(기본 설정)을 클릭하여 설정을 변경합니다.
6. **저장**을 클릭합니다.

**명령**

|도구|명령|
|---|---|
|CLI|[az network nic update](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterface](/powershell/module/azurerm.network/set-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-subnet-assignment"></a>서브넷 할당 변경

네트워크 인터페이스가 할당된 가상 네트워크는 변경할 수 없지만 서브넷은 변경할 수 있습니다.

1. 구독에 대한 네트워크 참가자 역할에 권한(최소)이 할당된 계정으로 [Azure Portal](https://portal.azure.com)에 로그인합니다. 계정에 역할 및 권한을 할당하는 방법에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어의 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) 문서를 참조하세요.
2. Azure Portal 위쪽의 *리소스 검색* 텍스트가 있는 상자에서 *네트워크 인터페이스*를 입력합니다. 검색 결과에 표시된 **네트워크 인터페이스**를 클릭합니다.
3. 표시되는 **네트워크 인터페이스** 블레이드에서 설정을 보거나 변경하려는 네트워크 인터페이스를 클릭합니다.
4. 선택한 네트워크 인터페이스에 대한 블레이드의 **설정** 아래에서 **IP 구성**을 클릭합니다. 나열된 모든 IP 구성의 개인 IP 주소 옆에 **(고정)**이 있으면 다음 단계를 수행하여 IP 주소 할당 방법을 동적으로 변경해야 합니다. 네트워크 인터페이스에 대한 서브넷 할당을 변경하려면 동적 할당 방법을 사용하여 모든 개인 IP 주소를 할당해야 합니다. 주소가 동적 방법으로 할당되면 5단계로 진행합니다. 고정 할당 방법으로 할당된 IPv4 주소가 있으면 다음 단계를 수행하여 할당 방법을 동적으로 변경합니다.
    - IP 구성 목록에서 IPv4 주소 할당 방법을 변경하려는 IP 구성을 클릭합니다.
    - IP 구성에 대해 표시되는 블레이드에서 **할당** 방법으로 **동적**을 클릭합니다. 정적 할당 방법으로 IPv6 주소를 할당할 수는 없습니다.
    - **저장**을 클릭합니다.
5. **서브넷** 드롭다운 목록에서 네트워크 인터페이스를 연결하려는 서브넷을 선택합니다.
6. **저장**을 클릭합니다. 새 동적 주소는 새 서브넷의 서브넷 주소 범위에서 할당됩니다. 네트워크 인터페이스를 새 서브넷에 할당한 후에는 원하는 경우 새 서브넷 주소 범위에서 고정 IPv4 주소를 할당할 수 있습니다. 네트워크 인터페이스용 IP 주소 추가, 변경 및 제거에 대해 자세히 알아보려면 [IP 주소 관리](virtual-network-network-interface-addresses.md) 문서를 확인하세요.

**명령**

|도구|명령|
|---|---|
|CLI|[az network nic ip-config update](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/set-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="delete-a-network-interface"></a>네트워크 인터페이스 삭제

가상 머신에 연결되지 않은 네트워크 인터페이스는 삭제할 수 있습니다. 네트워크 인터페이스가 가상 머신에 연결되어 있는 경우에는 먼저 가상 머신을 중지됨(할당 취소됨) 상태로 설정한 다음 가상 머신에서 네트워크 인터페이스를 분리합니다. 그런 후에 네트워크 인터페이스를 삭제할 수 있습니다. 가상 머신에서 네트워크 인터페이스를 분리하려면 [네트워크 인터페이스 추가 또는 제거](virtual-network-network-interface-vm.md) 문서 [가상 머신에서 네트워크 인터페이스 분리](virtual-network-network-interface-vm.md#vm-remove-nic) 섹션의 단계를 완료합니다. 가상 머신을 삭제하면 해당 가상 머신에 연결된 모든 네트워크 인터페이스가 분리되지만 삭제되지는 않습니다.

1. 구독에 대한 네트워크 참가자 역할에 권한(최소)이 할당된 계정으로 [Azure Portal](https://portal.azure.com)에 로그인합니다. 계정에 역할 및 권한을 할당하는 방법에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어의 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) 문서를 참조하세요.
2. Azure Portal 위쪽의 *리소스 검색* 텍스트가 있는 상자에서 *네트워크 인터페이스*를 입력합니다. 검색 결과에 표시된 **네트워크 인터페이스**를 클릭합니다.
3. 삭제하려는 네트워크 인터페이스를 마우스 오른쪽 단추로 클릭하고 **삭제**를 클릭합니다.
4. **예**를 클릭하여 네트워크 인터페이스 삭제를 확인합니다.

네트워크 인터페이스를 삭제하면 해당 네트워크 인터페이스에 할당된 모든 MAC 또는 IP 주소가 해제됩니다.

**명령**

|도구|명령|
|---|---|
|CLI|[az network nic delete](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmNetworkInterface](/powershell/module/azurerm.network/remove-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="next-steps"></a>다음 단계
여러 네트워크 인터페이스 또는 IP 주소가 있는 가상 머신을 만들려면 다음 문서를 참조하세요.

**명령**

|Task|도구|
|---|---|
|여러 NIC를 사용하여 VM 만들기|[CLI](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|여러 IPv4 주소가 있는 단일 NIC VM 만들기|[CLI](virtual-network-multiple-ip-addresses-cli.md), [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|Azure Load Balancer 뒤에 개인 IPv6 주소가 있는 단일 NIC VM 만들기|[CLI](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [Azure Resource Manager 템플릿](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
