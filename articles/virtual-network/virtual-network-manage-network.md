---
title: "aaaCreate, 변경 또는 Azure 가상 네트워크를 삭제 합니다. | Microsoft Docs"
description: "Toocreate, 변경 또는 Azure에서 가상 네트워크 삭제 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 7dfe6632753182eae2a13bb0327f03f75e03d057
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-virtual-network"></a>가상 네트워크 만들기, 변경 또는 삭제

어떻게 toocreate delete 가상 네트워크 및 변경 설정 같은 및 자세한 내용은 DNS 서버 및 IP 주소는 기존 가상 네트워크에 대 한 공간입니다.

가상 네트워크는 hello 클라우드에서 사용자의 네트워크의 표현입니다. 가상 네트워크는 hello 전용된 tooyour Azure 구독이 있는 Azure 클라우드에의 논리적 격리 합니다. 만드는 각 가상 네트워크에 대해 다음을 수행할 수 있습니다.
- 주소 공간 tooassign를 선택 합니다. 주소 공간은 CIDR(Classless Inter-Domain Routing) 표기법(예: 10.0.0.0/16)을 사용하여 정의된 하나 이상의 주소 범위로 구성됩니다.
- Toouse hello Azure 제공 DNS 서버를 선택 하거나 사용자 고유의 DNS 서버를 사용 합니다. 연결 된 toohello 가상 네트워크는 모든 리소스를이 DNS 서버 tooresolve 이름은 hello 가상 네트워크 내에서 할당 됩니다.
- 세그먼트 hello 가상 네트워크 서브넷에 각각 hello 가상 네트워크의 hello 주소 공간 내에서 고유한 주소 범위입니다. toocreate, 변경 및 삭제 서브넷의 참조 toolearn [추가, 변경 또는 삭제 서브넷](virtual-network-manage-subnet.md)합니다.

이 문서에서는 toocreate, 변경 하 고 hello Azure 리소스 관리자 배포 모델을 사용 하 여 가상 네트워크를 삭제 하는 방법을 설명 합니다.

## <a name="before"></a>시작하기 전에

이 문서에서 설명 하는 hello 작업을 시작 하기 전에 다음 필수 구성 요소는 hello를 완료 합니다.

- 가상 네트워크와 새 tooworking 인 경우 hello 연습을 검토 하는 것이 좋습니다 [첫 번째 Azure 가상 네트워크를 만든](virtual-network-get-started-vnet-subnet.md)합니다. 이 연습을 통해 가상 네트워크에 친숙해질 수 있습니다.
- 가상 네트워크를 검토에 대 한 제한에 대 한 toolearn [Azure 제한을](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits)합니다.
- Toohello Azure 포털에에서 로그인을 Azure 계정을 사용 하 여 Azure 명령줄 도구 (Azure CLI) 또는 Azure PowerShell hello 합니다. Azure 계정이 없으면 [평가판 계정](https://azure.microsoft.com/free)에 등록합니다.
- 먼저 toouse PowerShell 명령이이 문서에 설명 된 toocomplete hello 작업 하려는 경우 [Azure PowerShell 설치 및 구성](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다. Hello 최신 버전의 Azure PowerShell cmdlet이 설치 된 hello 가졌는지 확인 합니다. hello 예제에서 PowerShell 명령에 대 한 도움말 tooget 입력 `get-help <command> -full`합니다.
- 먼저 toouse Azure CLI 명령을이 문서에 설명 된 toocomplete hello 작업 하려는 경우 [설치 및 구성 Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다. Hello 가장 최신 버전의 Azure CLI를 설치 했는지 확인 합니다. Azure CLI 명령 사용 하 여 tooget 도움말 입력 `az <command> --help`합니다.


## <a name="create-vnet"></a>가상 네트워크 만들기

toocreate 가상 네트워크:

1. Toohello 로그인 [포털](https://portal.azure.com) 인 계정으로 hello 네트워크 참가자 역할 (최소한) 구독에 대 한 사용 권한이 할당 됩니다. 역할 및 사용 권한 tooaccounts 할당에 대 한 더 toolearn 참조 [Azure 역할 기반 액세스 제어에 대 한 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)합니다.
2. **새로 만들기** > **네트워킹** > **가상 네트워크**를 클릭합니다.
3. Hello에 **가상 네트워크** 블레이드 hello **배포 모델 선택** 둡니다 **리소스 관리자** 을 선택한 다음 클릭 **만들기**.
4. Hello에 **가상 네트워크 만들기** 블레이드를 입력 하거나 다음 설정을 hello에 대 한 값을 선택한 다음 클릭 **만들기**:
    - **이름**: hello 이름은 hello에서 고유 해야 합니다. [리소스 그룹](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group) toocreate hello에 있는 가상 네트워크를 선택 합니다. Hello 가상 네트워크를 만든 후 hello 이름을 변경할 수 없습니다. 시간이 지남에 따라 여러 가상 네트워크를 만들 수 있습니다. 명명 제안에 대해서는 [명명 규칙](/azure/architecture/best-practices/naming-conventions.md?toc=%2fazure%2fvirtual-network%2ftoc.json#naming-rules-and-restrictions)을 참조하세요. 보다 쉽게 toomanage 있도록 도와 명명 규칙에 따라 여러 개의 가상 네트워크입니다.
    - **주소 공간**: hello 주소 공간 CIDR 표기법으로 지정 합니다. 공용 또는 개인 (RFC 1918) hello 주소 공간을 정의할 수 있습니다. 공용 또는 개인으로 hello 주소 공간을 정의 하는지 여부를 hello 주소 공간은 hello 가상 네트워크, toohello 가상 네트워크를 연결 하는 모든 온-프레미스 네트워크와 연결 된 가상 네트워크에서 내 에서만 연결할 수입니다. 주소 공간을 다음 hello를 추가할 수 없습니다.
        - 224.0.0.0/4(멀티캐스트)
        - 255.255.255.255/32(브로드캐스트)
        - 127.0.0.0/8(루프백)
        - 169.254.0.0/16(링크-로컬)
        - 168.63.129.16/32(내부 DNS)

      Hello 가상 네트워크를 만들 때 하나의 주소 공간을 정의할 수 있지만 hello 가상 네트워크를 만든 후 더 많은 주소 공간을 추가할 수 있습니다. toolearn tooadd 주소 공간 tooan 기존 가상 네트워크를 참조 [추가 / 제거 주소 공간](#add-address-spaces) 이 문서의 내용입니다.

      >[!WARNING]
      >가상 네트워크의 다른 가상 네트워크 또는 온-프레미스 네트워크와 겹치는 주소 공간, 경우에 hello 두 네트워크를 연결할 수 없습니다. 주소 공간을 정의 하기 전에 수 사용할지 tooconnect hello 가상 네트워크 tooother 가상 네트워크 또는 온-프레미스 네트워크 hello에 이후 하는 것이 좋습니다.
      >
      >

    - **서브넷 이름**: hello 서브넷 이름은 hello 가상 네트워크 내에서 고유 해야 합니다. Hello 서브넷을 만든 후 서브넷 이름 hello를 변경할 수 없습니다. hello 포털 정의 하는 서브넷 1 개 가상 네트워크를 만들 때 가상 네트워크 필요 toohave 없는 경우에 모든 서브넷에 필요 합니다. Hello 포털에서 가상 네트워크를 만들 때 서브넷이 하나만 정의할 수 있습니다. Hello 가상 네트워크를 만든 후 더 많은 서브넷 toohello 가상 네트워크를 나중에 추가할 수 있습니다. 서브넷 tooa 가상 네트워크 tooadd 참조 [서브넷을 만든](virtual-network-manage-subnet.md#create-subnet) 에 [만들기, 변경 또는 삭제 서브넷](virtual-network-manage-subnet.md)합니다. Azure CLI 또는 PowerShell을 사용하여 여러 서브넷이 있는 가상 네트워크를 만들 수 있습니다.

      >[!TIP]
      >경우에 따라 관리자 hello 서브넷 간의 라우팅 toofilter 또는 제어 트래픽 서로 다른 서브넷을 만듭니다. 서브넷을 정의 하기 전에 toofilter 원하는 하 고 서브넷 간에 트래픽을 라우팅할 수 있는 방법을 고려 합니다. 서브넷 간의 트래픽 필터링에 대 한 더 toolearn 참조 [네트워크 보안 그룹](virtual-networks-nsg.md)합니다. Azure에서는 서브넷 간에 트래픽을 자동으로 라우팅하지만 Azure 기본 경로를 재정의할 수 있습니다. toolearn toooverride Azure 서브넷 트래픽 라우팅을 기본 참조 [사용자 정의 경로](virtual-networks-udr-overview.md)합니다.
      >

    - **서브넷 주소 범위**: hello 범위 hello 가상 네트워크에 대해 입력 한 hello 주소 공간 내에서 동일 해야 합니다. hello 가장 작은 범위를 지정할 수 있습니다 은/29, hello 서브넷에 대 한 8 개의 IP 주소를 제공 하는 합니다. Azure 예약 hello 처음 및 마지막 프로토콜 적합성에 대 한 각 서브넷의 주소입니다. 세 개의 추가 주소가 Azure 서비스를 사용하기 위해 예약되어 있습니다. 결과적으로 서브넷 주소 범위가 /29인 가상 네트워크에는 세 개의 IP 주소만 사용할 수 있습니다. Tooconnect tooa VPN 게이트웨이 가상 네트워크를 계획 하는 경우 게이트웨이 서브넷을 만들어야 합니다. [게이트웨이 서브넷에 대한 특정 주소 범위 고려 사항](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub)에서 대해 자세히 알아보세요. 특정 조건에서 hello 서브넷을 만든 후 hello 주소 범위를 변경할 수 있습니다. toochange 서브넷 주소 범위를 확인 하려면 어떻게 해야 toolearn [서브넷 설정을 변경](#change-subnet) 에 [추가, 변경 또는 삭제 서브넷](virtual-network-manage-subnet.md)합니다.
    - **구독**: [구독](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription)을 선택합니다. Hello를 사용할 수 없는 동일한 가상 네트워크에 하나 이상의 Azure 구독. 그러나 다른 구독에서 하나의 구독 toovirtual 네트워크에서 가상 네트워크를 연결할 수 있습니다. 다른 구독의 tooconnect 가상 네트워크는 Azure VPN 게이트웨이 또는 가상 네트워크 피어 링을 사용 합니다. Hello에 toohello 가상 네트워크를 연결 하는 모든 Azure 리소스 있어야 hello 가상 네트워크와 동일한 구독 합니다.
    - **리소스 그룹**: 기존 [리소스 그룹](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-groups)을 선택하거나 새 리소스 그룹을 만듭니다. Hello에 Azure 리소스 toohello 가상 네트워크를 연결할 수 있는 다른 리소스 그룹 또는 hello 가상 네트워크와 동일한 리소스 그룹입니다.
    - **위치:** 지역이라고도 하는 Azure [위치](https://azure.microsoft.com/regions/)를 선택합니다. 가상 네트워크는 하나의 Azure 위치에만 있을 수 있습니다. 그러나 다른 위치에 있는 하나의 위치 tooa 가상 네트워크에서 가상 네트워크 VPN 게이트웨이 사용 하 여 연결할 수 있습니다. Hello에 toohello 가상 네트워크를 연결 하는 모든 Azure 리소스 있어야 hello 가상 네트워크와 동일한 위치입니다.

**명령**

|도구|명령|
|---|---|
|Azure CLI|[az network vnet create](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[새-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name = "view-vnet"></a>가상 네트워크 및 설정 보기

tooview 가상 네트워크 및 설정:

1. Toohello 로그인 [포털](https://portal.azure.com) 인 계정으로 hello 네트워크 참가자 역할 (최소한) 구독에 대 한 사용 권한이 할당 됩니다. 역할 및 사용 권한 tooaccounts 할당에 대 한 더 toolearn 참조 [Azure 역할 기반 액세스 제어에 대 한 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)합니다.
2. Hello 포털 검색 상자에 입력 **가상 네트워크**합니다. Hello 검색 결과에서 클릭 **가상 네트워크**합니다.
3. Hello에 **가상 네트워크** 블레이드에서 hello 가상 네트워크에 대 한 tooview 설정을 클릭 합니다.
4. hello 다음 설정이 정리 되어 선택한 hello 가상 네트워크에 대 한 hello 블레이드에서:
    - **개요**: hello 가상 네트워크의 주소 공간 및 DNS 서버를 포함 하는 방법에 대 한 정보를 제공 합니다. hello 다음 스크린샷은 이라는 가상 네트워크에 대 한 hello 개요 설정을 **MyVNet**:

        ![네트워크 인터페이스 개요](./media/virtual-network-manage-network/vnet-overview.png)

      Hello에 **개요** 블레이드를 가상 네트워크 tooa 다른 구독 또는 리소스 그룹을 이동할 수 있습니다. toomove 가상 네트워크를 확인 하려면 어떻게 toolearn [구독 또는 리소스 tooa 다른 리소스 그룹 이동](../azure-resource-manager/resource-group-move-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다. hello 문서는 사전 요구 사항 및 Azure 포털, PowerShell 및 Azure CLI toomove 리소스를 사용 하 여 hello 하는 방법을 나열 합니다. Hello 가상 네트워크와 연결 된 toohello 가상 네트워크는 모든 리소스를 이동 해야 합니다.
    - **주소 공간**: toohello 가상 네트워크에 할당 된 hello 주소 공간 나열 됩니다. toolearn tooadd 및 주소 공간을 제거 하는 완료 하는 방법의 단계를 hello [추가 / 제거 주소 공간](#address-spaces) 이 문서의 내용입니다.
    - **연결 된 장치**: 모든 리소스를 연결 된 toohello 가상 네트워크 나열 됩니다. Hello 앞에 스크린 샷, 3 개의 네트워크 인터페이스와 부하 분산 장치가 하나은 연결 된 toohello 가상 네트워크입니다. 새 리소스를 만들고 toohello 가상 네트워크에 연결 하는 나열 됩니다. 연결 된 toohello 가상 네트워크에 있던 리소스를 삭제 하면 더 이상 hello 목록에 나타납니다.
    - **서브넷**: hello 가상 네트워크 내에 존재 하는 서브넷의 목록이 표시 됩니다. tooadd 및 제거 하는 서브넷의 참조 toolearn [서브넷을 만든](virtual-network-manage-subnet.md#create-subnet) 및 [서브넷 삭제](virtual-network-manage-subnet.md#delete-subnet) 에 [추가, 변경 또는 삭제 서브넷](virtual-network-manage-subnet.md)합니다.
    - **DNS 서버**: 제공 하는지 여부를 hello Azure 내부 DNS 서버 또는 사용자 지정 DNS 서버 이름 확인은 연결 된 toohello 가상 네트워크 장치에 대 한를 지정할 수 있습니다. Hello Azure 포털을 사용 하 여 가상 네트워크를 만들 때 기본적으로 DNS 서버를 Azure의 가상 네트워크 내에서 이름 확인을 위해 사용 됩니다. toomodify hello DNS 서버에서 단계를 완료 하는 hello [추가, 변경 또는 제거 하는 DNS 서버](#dns-servers) 이 문서의 내용입니다.
    - **피어 링**: 여기 나열 됩니다 hello 구독에 기존 피어 링이 있는 경우. 기존 피어링에 대한 설정을 보거나, 피어링을 만들거나 변경하거나 삭제할 수 있습니다. toolearn, 피어 링에 대 한 자세한 참조 [가상 네트워크 피어 링](virtual-network-peering-overview.md)합니다.
    - **속성**: hello 가상 네트워크를 hello 가상 네트워크의 리소스 ID를 포함 하 고 Azure 구독에 hello에 대 한 설정을 표시 합니다.
    - **다이어그램**: hello 다이어그램에는 모든 장치에 연결 된 toohello 가상 네트워크의 시각적 표현을 제공 합니다. hello 다이어그램에 hello 장치에 대 한 몇 가지 주요 정보가 있습니다. hello 다이어그램에이 뷰에서 장치 toomanage hello 장치를 클릭 합니다.
    - **일반적인 Azure 설정을**: 일반적인 Azure 설정에 대해 자세히 toolearn hello 다음 정보를 참조 하세요.
        *   [활동 로그](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#activity-logs)
        *   [액세스 제어(IAM)](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#access-control)
        *   [태그](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags)
        *   [잠금](../azure-resource-manager/resource-group-lock-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
        *   [자동화 스크립트](../azure-resource-manager/resource-manager-export-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json#export-the-template-from-resource-group)

**명령**

|도구|명령|
|---|---|
|Azure CLI|[az network vnet show](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#show)|
|PowerShell|[Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork/?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="add-address-spaces"></a>주소 공간 추가 또는 제거

가상 네트워크에 대한 주소 공간을 추가 및 제거할 수 있습니다. 주소 공간 CIDR 표기법으로 지정 해야 하며 겹칠 수 없습니다 hello 내에서 다른 주소 공간과 동일한 가상 네트워크입니다. 공용 또는 개인 (RFC 1918) hello 주소 공간을 정의할 수 있습니다. 공용 또는 개인으로 hello 주소 공간을 정의 하는지 여부를 hello 주소 공간은 hello 가상 네트워크, toohello 가상 네트워크를 연결 하는 모든 온-프레미스 네트워크와 연결 된 가상 네트워크에서 내 에서만 연결할 수입니다. 주소 공간을 다음 hello를 추가할 수 없습니다.

- 224.0.0.0/4(멀티캐스트)
- 255.255.255.255/32(브로드캐스트)
- 127.0.0.0/8(루프백)
- 169.254.0.0/16(링크-로컬)
- 168.63.129.16/32(내부 DNS)

tooadd / 제거 주소 공간:

1. Toohello 로그인 [포털](https://portal.azure.com) 인 계정으로 hello 네트워크 참가자 역할 (최소한) 구독에 대 한 사용 권한이 할당 됩니다. 역할 및 사용 권한 tooaccounts 할당에 대 한 더 toolearn 참조 [Azure 역할 기반 액세스 제어에 대 한 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)합니다.
2. Hello 포털 검색 상자에 입력 **가상 네트워크**합니다. Hello 검색 결과에서 선택 **가상 네트워크**합니다.
3. Hello에 **가상 네트워크** 블레이드에서 hello tooadd 원하는 하거나 주소 공간을 제거 하는 가상 네트워크를 클릭 합니다.
4. 가상 hello에 블레이드에서 아래에서 네트워크 **설정**, 클릭 **주소 공간**합니다.
5. Hello 주소 공간에 대 한 hello 블레이드에서 hello 다음 옵션 중 하나를 완료 합니다.
    - **주소 공간 추가**: hello 새 주소 공간을 입력 합니다. hello 주소 공간 hello 가상 네트워크에 대해 정의 된 기존 주소 공간과 겹칠 수 없습니다.
    - **주소 공간 제거:** 주소 공간을 마우스 오른쪽 단추로 클릭한 다음 **제거**를 클릭합니다. Hello 주소 공간에 서브넷이 있으면 hello 주소 공간을 제거할 수 없습니다. tooremove 주소 공간을 먼저 삭제 해야 어떤 서브넷 (및 모든 리소스를 연결 된 toohello 서브넷) hello 주소 공간에 존재 합니다.
6. **Save**를 클릭합니다.

**명령**

|도구|명령|
|---|---|
|Azure CLI|리소스 관리자에만 해당|[az network vnet update](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="dns-servers"></a>DNS 서버 추가, 변경 또는 제거

모든 Vm을 가상 네트워크에 연결 된 toohello hello 가상 네트워크에 대해 지정 하는 hello DNS 서버를 등록 합니다. 지정 된 hello도 사용 이름 확인에 DNS 서버입니다. VM의 각 NIC(네트워크 인터페이스)에는 자체의 DNS 서버 설정이 있을 수 있습니다. NIC는 자체 DNS 서버 설정을 있으면 hello 가상 네트워크에 대 한 hello DNS 서버 설정이 재정의 됩니다. NIC DNS 설정에 대해 자세히 toolearn 참조 [네트워크 인터페이스 작업 및 설정을](virtual-network-network-interface.md#change-dns-servers)합니다. Vm 및 Azure 클라우드 서비스에서 역할 인스턴스에 대 한 이름 확인에 대해 자세히 toolearn 참조 [Vm 및 역할 인스턴스에 대 한 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md)합니다. tooadd, 변경 또는 DNS 서버를 제거 합니다.

1. Toohello 로그인 [포털](https://portal.azure.com) 인 계정으로 hello 네트워크 참가자 역할 (최소한) 구독에 대 한 사용 권한이 할당 됩니다. 역할 및 사용 권한 tooaccounts 할당에 대 한 더 toolearn 참조 [Azure 역할 기반 액세스 제어에 대 한 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)합니다.
2. Hello 포털 검색 상자에 입력 **가상 네트워크**합니다. Hello 검색 결과에서 선택 **가상 네트워크**합니다.
3. Hello에 **가상 네트워크** 블레이드에서 대 한 DNS 설정을 toochange hello 가상 네트워크를 클릭 합니다.
4. 가상 hello에 블레이드에서 아래에서 네트워크 **설정**, 클릭 **DNS 서버**합니다.
5. Hello 다음 DNS 서버를 나열 하는 hello 블레이드에서 옵션 중 하나를 선택 합니다.
    - **기본 (Azure 제공)**: 모든 리소스 이름 및 개인 IP 주소는 자동으로 등록 된 toohello Azure DNS 서버입니다. 모든 리소스를 연결 된 toohello 간의 이름을 확인할 수 있습니다 동일한 가상 네트워크입니다. 가상 네트워크를 통해이 옵션 tooresolve 이름은 사용할 수 없습니다. 가상 네트워크를 통해 tooresolve 이름, 사용자 지정 DNS 서버를 사용 해야 합니다.
    - **사용자 지정**: toohello Azure 가상 네트워크에 대 한 제한에 하나 이상의 서버를 추가할 수 있습니다. DNS 서버도 대 한 자세한 정보는 toolearn 참조 [Azure 제한을](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#virtual-networking-limits-classic)합니다. Hello 다음 옵션을 사용할 수 있습니다.
        - **주소 추가**: hello 서버 tooyour 가상 네트워크 DNS 서버 목록을 추가 합니다. 또한이 옵션으로 Azure hello DNS 서버를 등록합니다. Azure DNS 서버를 이미 등록 한 경우에 hello 목록에서 해당 DNS 서버를 선택할 수 있습니다.
        - **주소 제거**: tooremove를 지정 하는 다음 toohello 서버 클릭 **X**합니다. 이 가상 네트워크 목록 에서만에서 hello 서버를 제거 하는 hello 서버를 삭제 합니다. hello DNS 서버에 다른 가상 네트워크 toouse 프로그램에 대 한 Azure에 등록 된 상태로 유지 됩니다.
        - **DNS 서버 주소를 다시 정렬**:이 tooverify hello에 DNS 서버를 나열 하는 올바른 순서 환경에 대 한 중요 합니다. 지정 된 hello 순서로 DNS 서버 목록이 사용 됩니다. 라운드 로빈 설정으로 작동하지 않습니다. Hello hello 목록에서 첫 번째 DNS 서버에 연결할 수 있는 경우 hello 클라이언트 hello DNS 서버가 올바르게 작동 하는지 여부에 관계 없이 해당 DNS 서버를 사용 합니다. 나열 된 hello DNS 서버를 모두 제거 하 고 원하는 hello 순서로 다시 추가 합니다.
        - **주소 변경**: hello DNS 서버 hello 목록에서 강조 표시 한 다음 hello 새 이름을 입력 합니다.
6. **Save**를 클릭합니다.
7. Hello 새 DNS 서버 설정을 할당 되므로 toohello 연결 된 가상 네트워크에 있는 hello Vm을 다시 시작 합니다. Vm 다시 시작 될 때까지 현재 DNS 설정 toouse를 계속 합니다.

**명령**

|도구|명령|
|---|---|
|Azure CLI|[az network vnet update](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="delete-vnet"></a>가상 네트워크 삭제

리소스 연결 된 tooit 없는 경우에 가상 네트워크를 삭제할 수 있습니다. Hello 가상 네트워크 내에서 리소스 연결 된 tooany 서브넷에 있는 경우 hello 리소스 hello 가상 네트워크 내에서 연결 된 tooall 서브넷을 먼저 삭제 해야 합니다. hello 단계를 수행 toodelete 리소스 hello 리소스에 따라 달라 집니다. toodelete 리소스 연결된 toosubnets를 읽는 방법 toolearn hello 설명서 원하는 toodelete 각 리소스 유형에 대 한 합니다. toodelete 가상 네트워크:

1. Toohello 로그인 [포털](https://portal.azure.com) 계정과 즉 (최소한) 할당 된 사용 권한은 구독에 대 한 hello 네트워크 참가자 역할에 대 한 합니다. 역할 및 사용 권한 tooaccounts 할당에 대 한 더 toolearn 참조 [Azure 역할 기반 액세스 제어에 대 한 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)합니다.
2. Hello 포털 검색 상자에 입력 **가상 네트워크**합니다. Hello 검색 결과에서 클릭 **가상 네트워크**합니다.
3. Hello에 **가상 네트워크** 블레이드, toodelete 원하는 선택 hello 가상 네트워크입니다.
4. 장치가 없는 tooconfirm hello 가상 네트워크 블레이드에서 toohello 가상 네트워크에서 연결 **설정**, 클릭 **연결 된 장치**합니다. 연결 된 장치가 없을 경우 hello 가상 네트워크를 삭제 하려면 먼저 삭제 해야 합니다. 연결된 장치가 없으면 **개요**를 클릭합니다.
5. Hello 블레이드의 hello 위쪽 hello 클릭 **삭제** 아이콘입니다.
6. hello 가상 네트워크의 tooconfirm hello 삭제 클릭 **예**합니다.


**명령**

|도구|명령|
|---|---|
|Azure CLI|[azure network vnet delete](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmVirtualNetwork](/powershell/module/azurerm.network/remove-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="next-steps"></a>다음 단계

- VM toocreate tooa 가상 네트워크 연결을 참조 하세요 [가상 네트워크를 만들고 Vm 연결](virtual-network-get-started-vnet-subnet.md#create-vms)합니다.
- 가상 네트워크 내의 서브넷 간의 네트워크 트래픽을 toofilter 참조 [네트워크 보안 그룹을 만들고](virtual-networks-create-nsg-arm-pportal.md)합니다.
- 가상 네트워크 tooanother 가상 네트워크 toopeer 참조 [피어 링 가상 네트워크 만들기](virtual-network-create-peering.md#portal)합니다.
- 가상 네트워크 tooan 온-프레미스 네트워크를 연결 하기 위한 옵션에 대 한 toolearn 참조 [에 대 한 VPN 게이트웨이](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#diagrams)합니다.
