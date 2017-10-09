---
title: "aaaCreate, 변경 또는 Azure 가상 네트워크 피어 링 삭제 | Microsoft Docs"
description: "Toocreate, 변경 또는 가상 네트워크 피어 링 삭제 방법에 대해 알아봅니다."
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
ms.date: 07/26/2017
ms.author: jdial
ms.openlocfilehash: 70f85364ab23e23533ad276aeec0156cebe89be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-virtual-network-peering"></a>가상 네트워크 피어링 만들기, 변경 또는 삭제

Toocreate, 변경 또는 가상 네트워크 피어 링 삭제 방법에 대해 알아봅니다. 가상 네트워크 피어 링 수 있도록 하면 tooconnect 2에서 가상 네트워크를 통해 동일한 Azure 위치 hello hello Azure 백본 네트워크입니다. 겹치기, 되 면 hello 두 가상 네트워크는 여전히 별도 리소스 그룹으로 관리 됩니다. 동일한 hello와 각 가상 네트워크의 리소스 통신 hello 리소스 모두에 존재 하는 경우 hello 동일 대기 시간 및 대역폭 가상 네트워크입니다. 가상 네트워크 피어 링이 모르는 경우 hello를 읽는 것이 좋습니다 [가상 네트워크 피어 링 개요](virtual-network-peering-overview.md) hello를 완료 하 고 [만들 가상 네트워크 피어 링 자습서](virtual-network-create-peering.md)를 완료 하기 전에 이 문서의 hello 작업입니다.

## <a name="before-you-begin"></a>시작하기 전에

이 문서의 섹션의 단계를 완료 하기 전에 작업을 수행 하는 hello를 완료 합니다.

- 검토 hello [Azure 제한](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) 피어 링에 대 한 제한에 대 한 문서 toolearn 합니다.
- Azure 계정으로 toohello Azure 포털, Azure 명령줄 인터페이스 (CLI) 또는 Azure PowerShell에 로그인 합니다. 아직 Azure 계정이 없으면 [평가판 계정](https://azure.microsoft.com/free)에 등록합니다.
- 이 문서에서는 toocomplete 작업 명령이 PowerShell을 사용 하는 경우 [Azure PowerShell 설치 및 구성](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다. Hello 가장 최신 버전의 hello Azure PowerShell cmdlet이 설치 되어 있는지 확인 합니다. 예제를 보려면으로 PowerShell 명령에 대 한 도움말 tooget 입력 `get-help <command> -full`합니다.
- 이 문서에서는 toocomplete 작업 명령을 Azure CLI (명령줄 인터페이스)를 사용 하는 경우 [설치 및 구성 hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다. Hello 최신 버전의 hello Azure CLI 설치 되어 있는지 확인 합니다. CLI 명령에 대 한 도움말 tooget 입력 `az <command> --help`합니다. 설치 hello CLI 및 해당 필수 구성 요소는 대신 Azure 클라우드 셸 hello를 사용할 수 있습니다. Azure 클라우드 셸 hello hello Azure 포털 내에서 직접 실행할 수 있는 무료 Bash 셸의입니다. 클라우드 셸 hello에 hello Azure CLI 사전 설치 및 toouse 계정으로 구성 되어 있습니다. toouse hello 클라우드 셸 클릭 hello 클라우드 셸 **> _** hello hello 위쪽에 단추 [포털](https://portal.azure.com)합니다. 

## <a name="create-a-peering"></a>피어링 만들기

>[!NOTE]
>제약 조건, 몇 가지 요구 사항이 있으며 고려 사항 toosuccessfully 피어 링 가상 네트워크를 만듭니다. 피어 링을 만들기 전에 확인 하면 한 익숙해지면 hello [요구 사항 및 제약 조건](#requirements-and-constraints) 및 [필요한 권한](#permissions)합니다.
>

1. Toohello 로그인 [포털](https://portal.azure.com) hello 필요한 할당 된 계정으로 [역할 또는 권한](#permissions)합니다.
2. Hello 텍스트를 포함 하는 hello 상자에서 *리소스 검색* hello Azure 포털의 hello 위쪽 입력 *가상 네트워크*합니다. 때 **가상 네트워크** 나타납니다 hello 검색 결과에를 클릭 합니다. 선택 하지 않으면 **가상 네트워크 (클래식)** 경우 나타나는 hello 목록의 hello 클래식 배포 모델을 통해 배포 된 가상 네트워크에서 피어 링을 만들 수 없습니다.
3. Hello에 **가상 네트워크** 나타나는 블레이드 hello 가상 네트워크에 대 한 피어 링 toocreate 하려면 클릭 합니다.
4. 선택한 hello 가상 네트워크에 대해 표시 되는 hello 창에서 클릭 **피어 링** hello에 **설정을** 섹션.
5. **+ 추가**를 클릭합니다. 
6. <a name="add-peering"></a>Hello에 **피어 링 추가** 블레이드를 입력 하거나 다음 설정을 hello에 대 한 값을 선택 합니다.
    - **이름:** hello 피어 링에 대 한 hello 이름은 hello 가상 네트워크 내에서 고유 해야 합니다.
    - **가상 네트워크 배포 모델:** toopeer를 통해 배포 된 원하는 하는 어떤 배포 모델 hello 가상 네트워크를 선택 합니다.
    - **내 리소스 ID 확인:** 읽기 액세스 toohello 가상 네트워크와 toopeer 원하는 설정한 경우 선택이 확인란을이 선택 합니다. 읽기 액세스 toohello 가상 네트워크 또는와 toopeer 구독 없는 경우이 확인란을 선택 합니다. Hello에 toopeer와 원하는 hello 가상 네트워크의 hello 전체 리소스 ID를 입력 **리소스 ID** hello 상자를 선택 하면 때 나타나는 상자. 에 있는 가상 네트워크에 대 한 ID 입력 해야 하는 hello 리소스 동일한 Azure hello [위치](https://azure.microsoft.com/regions) 이 가상 네트워크와 합니다. hello 전체 리소스 ID 찾는 유사한너무/구독/<Id>/resourceGroups/ < 리소스 그룹 이름 > /providers/Microsoft.Network/virtualNetworks/ < 가상 네트워크-이름 >. 가상 네트워크에 대 한 hello 속성을 확인 하 여 가상 네트워크에 대 한 hello 리소스 ID를 얻을 수 있습니다. 가상 네트워크에 대 한 tooview hello 속성 참조 toolearn [가상 네트워크를 관리](virtual-network-manage-network.md#view-vnet)합니다.
    - **구독:** 선택 hello [구독](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) 와 toopeer hello 가상 네트워크의 원하는 합니다. 계정이 읽기 권한이 있는 구독 수에 따라 하나 이상의 구독이 나열됩니다. Hello를 선택 하는 경우 **리소스 ID** 확인란,이 설정을 사용할 수 없습니다. 두 가상 네트워크가 Resource Manager를 통해 만들어졌기만 하면 다른 구독에 있는 가상 네트워크를 피어링할 수 있습니다. 다양 한 배포 모델을 통해 만든 구독 전반에 걸쳐 hello 기능 toopeer 미리 보기 릴리스에서입니다. 서로 다른 구독에 존재 하는 다양 한 배포 모델을 통해 배포 된 가상 네트워크 간의 피어 링을 만들기 전에 hello 미리 보기에 등록 하십시오. 에 대 한 자세한 방법에 대 한 tooregister hello 미리 보기에 대 한 및 [서로 다른 구독에 대 한 다양 한 배포 모델을 통해 만든 가상 네트워크 피어](create-peering-different-deployment-models-subscriptions.md)합니다.
    - **가상 네트워크:** 선택 hello와 toopeer 원하는 가상 네트워크입니다. 두 Azure 배포 모델을 통해 만든 가상 네트워크를 선택할 수 있습니다 하지만 hello 가상 네트워크를 시작 하는 hello 가상 네트워크와 동일한 위치에서 피어 링 hello hello에 있어야 합니다. 읽기 있어야 액세스 toohello 가상 네트워크에 대 한 toobe hello 목록에 표시 합니다. Hello 가상 네트워크에 대 한 hello 주소 공간은이 가상 네트워크에 대 한 hello 주소 공간과 겹칩니다. out, 회색으로 표시 되지만 가상 네트워크 나열 되 면 수 있습니다. 가상 네트워크 주소 공간이 겹치면 피어링할 수 없습니다. Hello를 선택 하는 경우 **리소스 ID** 확인란,이 설정을 사용할 수 없습니다.
    - **가상 네트워크 액세스 허용:** 선택 **Enabled** hello 두 가상 네트워크 간의 tooenable 통신 하려는 경우 (기본값). 리소스 연결 된 가상 네트워크 간의 통신을 사용 하면 마치 toohello 연결 된 것 처럼 동일한 대역폭 및 대기 시간으로 서로 tooeither 가상 네트워크 toocommunicate hello 동일한 가상 네트워크입니다. Hello 두 가상 네트워크의 리소스 간의 모든 통신이 hello Azure 개인 네트워크 끝났습니다. hello **VirtualNetwork** hello 가상 네트워크와 가상 네트워크 겹치기 네트워크 보안 그룹에 대 한 기본 태그를 포함 합니다. hello 읽기에 대해 더 알아봅니다 toolearn 네트워크 보안 그룹 기본 태그 [네트워크 보안 그룹을 개요](virtual-networks-nsg.md#default-tags) 문서.  선택 **비활성화** tooflow toohello 트래픽 가상 네트워크를 겹치기 않도록 합니다. 선택할 수 있습니다 **비활성화** 다른 가상 네트워크와 가상 네트워크를 겹치기 했습니다 하지만 hello 두 가상 네트워크 간의 트래픽 흐름 toodisable를 원하는 경우도 있습니다. 피어링을 삭제하고 다시 만드는 것보다 사용/사용 안 함을 설정하는 것이 더 편리함을 알 수 있습니다. 간의 트래픽 흐름 하지 않는이 설정을 비활성화 되 면 hello 겹치기 가상 네트워크입니다.
    - **전달 된 트래픽을 허용:** 상자 tooallow 트래픽 전달 toohello이 가상 네트워크 (하지 hello 겹치기 가상 네트워크에서 시작 되는 트래픽을) 겹치기 확인 tooflow toothis 가상 네트워크입니다. 트래픽 전달이 hello와 피어 링 하 고 사용자 정의 경로 tooforward 트래픽 hello 네트워크 가상 어플라이언스를 통해 만든 가상 네트워크의 네트워크 가상 어플라이언스를 구축 하면 때 일반적입니다. 이 상자 선택 취소 되어 있음된 (기본값)를 두면 hello 겹치기 가상 네트워크에서 전달 하는 트래픽은 toothis 가상 네트워크를 이동 하지 못합니다. Hello 피어 링을 통해 트래픽을 전달 하는 hello에서는이 기능을 사용 하도록 설정 하는 동안 하거나 하지 않는 모든 사용자 정의 경로 만들 네트워크 가상 어플라이언스 합니다. 사용자 정의 경로와 네트워크 가상 어플라이언스는 개별적으로 만들어집니다. [사용자 정의 경로](virtual-networks-udr-overview.md)에 대해 자세히 알아보세요.
    - **게이트웨이 전송 허용:** 보유 한 가상 네트워크 게이트웨이 연결 된 toothis 가상 네트워크 및 원하는 tooallow 트래픽만 hello 겹치기 hello 게이트웨이 통해 가상 네트워크 tooflow이이 상자를 선택 합니다. 예를 들어이 가상 네트워크는 가상 네트워크 게이트웨이 통해 연결 된 tooan 온-프레미스 네트워크를 수 있습니다. Hello 게이트웨이 toothis 연결 된 가상 네트워크를 통해 가상 네트워크 tooflow를 겹치기 확인이 상자 hello에서의 트래픽을 허용 하는 중입니다. 이 확인란을 선택 하면 hello 겹치기 가상 네트워크 구성 된 게이트웨이 사용할 수 없습니다. hello 겹치기 가상 네트워크에는 hello를 사용 해야 합니다. **원격 게이트웨이 사용** 확인란을 선택 하면 다른 가상 네트워크 toothis 가상 네트워크를 hello hello에서 피어 링 설정 합니다. 이 상자 선택 취소 되어 있음된 (기본값)를 두면 hello 겹치기 가상 네트워크에서 트래픽을 여전히 toothis 가상 네트워크를 이동 하지만 가상 네트워크 게이트웨이 연결 된 toothis 가상 네트워크를 통해 전달할 수 없습니다. [가상 네트워크 게이트웨이](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#s2smulti)에 대해 자세히 알아보세요. 
    
    가상 네트워크(Resource Manager)를 가상 네트워크(클래식)와 피어링하는 경우 이 옵션을 사용하도록 설정할 수 없습니다. Hello 두 가상 네트워크 간 hello 트래픽 흐름을 하지만 hello 가상 네트워크 (클래식) 트래픽을 네트워크 게이트웨이가 연결 된 toohello 가상 네트워크 (리소스 관리자)를 통해 전달할 수 없습니다.
    - **원격 게이트웨이 사용 하 여:** 이 상자 tooallow 트래픽만 가상 네트워크 게이트웨이 연결 된 toohello 가상 네트워크와 피어 링 하는 통해이 가상 네트워크 tooflow 확인 합니다. 예를 들어 hello와 피어 링 하는 가상 네트워크에 연결 된 VPN 게이트웨이 통신 tooan 온-프레미스 네트워크를 사용 하도록 설정 하는 있습니다.  이 가상 네트워크 tooflow hello VPN 게이트웨이 연결 된 toohello 겹치기 가상 네트워크를 통해 트래픽을 허용이 확인란을 선택 합니다. 이 상자를 선택 하는 경우 hello 겹치기 가상 네트워크 가상 네트워크 게이트웨이 연결 tooit 있어야 하며이 hello 있어야 하는 **게이트웨이 전송 허용** checkbox 선택 합니다. Hello 겹치기 가상 네트워크에서 트래픽을 가상 toothis를 여전히 전달 될 수 있습니다이 상자 선택 취소 되어 있음된 (기본값)를 두면 네트워크에 있지만 가상 네트워크 게이트웨이 연결 된 toothis 가상 네트워크를 통해 전달할 수 없습니다. 
    
    가상 네트워크(Resource Manager)를 가상 네트워크(클래식)와 피어링하는 경우 이 옵션을 사용하도록 설정할 수 없습니다. Hello 트래픽을 두 가상 네트워크 hello 사이 이동, 경우에 hello (리소스 관리자) 가상 네트워크 트래픽이 네트워크 게이트웨이가 연결 된 toohello 가상 네트워크 (클래식)를 통해 전달할 수 없습니다.
7. Hello 클릭 **확인** 단추 tooadd hello 서브넷 toohello 가상 네트워크 선택 합니다.

### <a name="commands"></a>명령

|도구|명령|
|---|---|
|CLI|[az network vnet peering create](/cli/azure/network/vnet/peering#create?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Add-AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json)|


### <a name="scenarios"></a>시나리오

동일 hello를 통해 만든 가상 네트워크 간에 만들어진 가상 네트워크 피어 링 하거나 다양 한 배포 모델에 존재 하는 hello 같거나 다른 데이터 집합 구독 합니다. Hello 다음 시나리오 중 하나에 대 한 단계별 자습서를 완료 합니다.
 
|Azure 배포 모델  | 구독  |
|---------|---------|
|둘 다 Resource Manager |[동일](virtual-network-create-peering.md)|
| |[다름](create-peering-different-subscriptions.md)|
|하나는 Resource Manager, 다른 하나는 클래식     |[동일](create-peering-different-deployment-models.md)|
| |[다름](create-peering-different-deployment-models-subscriptions.md)|

## <a name="view-or-change-peering-settings"></a>피어링 설정 보기 또는 변경

1. Toohello 로그인 [포털](https://portal.azure.com) hello 필요한 할당 된 계정으로 [역할 또는 권한](#permissions)합니다.
2. Hello 텍스트를 포함 하는 hello 상자에서 *리소스 검색* hello Azure 포털의 hello 위쪽 입력 *가상 네트워크*합니다. 때 **가상 네트워크** 나타납니다 hello 검색 결과에를 클릭 합니다.
3. Hello에 **가상 네트워크** 나타나는 블레이드 hello 가상 네트워크에 대 한 피어 링 toocreate 하려면 클릭 합니다.
4. 선택한 hello 가상 네트워크에 대해 표시 되는 hello 창에서 클릭 **피어 링** hello에 **설정을** 섹션.
5. Hello 피어 링 클릭 tooview 하거나에 대 한 설정을 변경 합니다.
6. Hello 적절 한 설정을 변경 합니다. 각 설정에 대 한 hello 옵션에 대해 알아보세요 [6 단계](#add-peering) 의 hello이 문서의 피어 링 섹션을 만듭니다. 

    >[!NOTE]
    >제약 조건, 몇 가지 요구 사항이 있으며 고려 사항 toosuccessfully 피어 링 가상 네트워크를 만듭니다. 피어 링을 만들기 전에 확인 하면 한 익숙해지면 hello [요구 사항 및 제약 조건](#requirements-and-constraints) 및 [필요한 권한](#permissions)합니다.
    >

7. **Save**를 클릭합니다.

**명령**

|도구|명령|
|---|---|
|CLI|[az 네트워크 vnet 피어 링 목록](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#list) 가상 네트워크에 대 한 피어 링 toolist [az 네트워크 vnet 피어 링 표시](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#show) tooshow 특정 피어 링, 설정 및 [az 네트워크 vnet 피어 링 업데이트](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#update) toochange 피어 링 설정입니다.|
|PowerShell|[Get AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/get-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json) tooretrieve 피어 링 설정을 확인 하 고 [집합 AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/set-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json) toochange 설정 합니다.|

## <a name="delete-a-peering"></a>피어링 삭제
피어 링이 삭제 되 면 가상 네트워크에서 트래픽을 toohello 겹치기 가상 네트워크를 더 이상 이동 합니다. 리소스 관리자를 통해 배포 된 가상 네트워크 겹치기는 경우 각 가상 네트워크에 피어 링 toohello 다른 가상 네트워크 경우에 하나의 가상 네트워크에서 피어 링 hello 삭제 hello 간의 통신이 해제 hello 가상 네트워크를 삭제 하지는 않습니다 hello에서 피어 링 hello 다른 가상 네트워크입니다. hello에 존재 하는 피어 링 hello에 대 한 피어 링 상태 hello 다른 가상 네트워크는 **Disconnected**합니다. Hello 첫 번째 가상 네트워크에 피어 링 hello 다시 만드는 가상 모두에 대 한 피어 링 상태 hello 네트워크 변경 내용을 너무 될 때까지 hello 피어 링 다시 만들 수 없습니다*연결 됨*합니다. 

경우에 따라 가상 네트워크 toocommunicate 사용 하려는 경우 항상 피어 링을 삭제 하는 대신 설정할 수 있습니다 hello **가상 네트워크 액세스 허용** 너무 설정**비활성화** 대신 합니다. toolearn hello의 6 단계를 읽는 방법, [피어 링 만들기](#create-peering) 이 문서의 섹션. 피어링을 삭제하고 다시 만드는 것보다 네트워크 액세스를 사용 안 함/사용 설정하는 것이 더 쉬움을 알 수 있습니다.

1. Toohello 로그인 [포털](https://portal.azure.com) hello 필요한 할당 된 계정으로 [역할 또는 권한](#permissions)합니다.
2. Hello 텍스트를 포함 하는 hello 상자에서 *리소스 검색* hello Azure 포털의 hello 위쪽 입력 *가상 네트워크*합니다. 때 **가상 네트워크** 나타납니다 hello 검색 결과에를 클릭 합니다.
3. Hello에 **가상 네트워크** 나타나는 블레이드에서 피어 링 toodelete 원하는 hello 가상 네트워크를 클릭 합니다.
4. Hello 블레이드에서 나타나는 선택한 hello 가상 네트워크에 대 한 클릭 **피어 링** 아래 **설정을**합니다.
5. 원하는 toodelete hello 피어 링 블레이드에서 마우스 오른쪽 단추로 클릭 hello 있습니다 피어 링에 표시 되는 피어 링의 hello 목록에서 클릭 **삭제**, 다음 **예** hello 첫 번째 가상 네트워크에서 피어 링 toodelete hello 합니다.
6. 전체 hello 이전 단계 toodelete hello에서 피어 링 hello hello 피어 링에 다른 가상 네트워크입니다.

**명령**

|도구|명령|
|---|---|
|CLI|[az network vnet peering delete](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/remove-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="requirements-and-constraints"></a>요구 사항 및 제약 조건 

- hello 가상 네트워크 피어 링 있습니다 겹치지 않는 IP 주소 공간이 있어야 합니다.
- 가상 네트워크가 다른 가상 네트워크와 피어링되면 가상 네트워크에 주소 공간을 추가하거나 가상 네트워크에서 주소 공간을 삭제할 수 없습니다. tooadd / 제거 주소 공간 delete hello 피어 링을 추가 또는 hello 주소 공간을 제거 후 다시 hello 피어 링을 만듭니다. tooadd 주소 공간, 또는 가상 네트워크에서 주소 공간을 제거 읽기 hello [만들기, 변경 또는 삭제 가상 네트워크](virtual-network-manage-network.md#add-address-spaces) 문서. 
- 리소스 관리자 또는 hello 클래식 배포 모델을 통해 배포 된 가상 네트워크와 리소스 관리자를 통해 배포 된 가상 네트워크를 통해 배포 되는 두 개의 가상 네트워크 피어 링 할 수 있습니다. Hello 클래식 배포 모델을 통해 생성 된 가상 네트워크에서 두 피어 링 수 없습니다. Azure 배포 모델을 잘 모르는 경우 읽기 hello [이해 Azure 배포 모델](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 문서. 사용할 수는 [VPN 게이트웨이](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) hello 클래식 배포 모델을 통해 만든 tooconnect 두 가상 네트워크입니다.
- 리소스 관리자를 통해 생성 된 가상 네트워크에서 두 개의 피어 링을 피어 링 hello 피어 링에 각 가상 네트워크에 대해 구성 해야 합니다. Hello 첫 번째 가상 네트워크에서 hello 피어 링 toohello 두 번째 가상 네트워크를 만들 때 hello 피어 링 상태가 *시작 되었습니다.*합니다.  Hello 두 번째 가상 네트워크 toohello 첫 번째 가상 네트워크에서 피어 링 hello를 만들면 피어 링 상태가 *연결 됨*합니다. 상태가 변경에서 hello 첫 번째 가상 네트워크에 대 한 hello 피어 링 상태를 확인 하는 경우 표시 *시작 되었습니다.* 너무*연결 됨*합니다. hello 피어 링은 설정 되지 않으면 두 가상 네트워크 피어 링에 대 한 피어 링 상태가 hello *연결 됨*합니다. 
- Hello 클래식 배포 모델을 통해 만든 가상 네트워크를 사용 하 여 리소스 관리자를 통해 만든 가상 네트워크 피어 링을 때만 구성한 리소스 관리자를 통해 배포 된 hello 가상 네트워크에 대 한 피어 링입니다. Hello 클래식 배포 모델을 통해 배포 된 두 개의 가상 네트워크 간 또는 가상 네트워크 (클래식)에 대 한 피어 링을 구성할 수 없습니다. Hello hello 가상 네트워크 (리소스 관리자) toohello 가상 네트워크 (클래식)에서 피어 링을 만들 때 hello 피어 링 상태가 *업데이트*, 다음 너무 변경 곧*연결 됨*합니다.   
- 두 가상 네트워크 간에 피어링이 설정됩니다. 피어링은 전이적이지 않습니다. 다음 사이에 피어링을 만들면:
    - VirtualNetwork1 및 VirtualNetwork2
    - VirtualNetwork2 및 VirtualNetwork3

  VirtualNetwork2를 통한 VirtualNetwork1과 VirtualNetwork3 사이의 피어링은 없습니다. 가상 네트워크 VirtualNetwork1 VirtualNetwork3 사이의 피어 링 toocreate 원하는 있으면 toocreate VirtualNetwork1 VirtualNetwork3 사이의 피어 링입니다.
- 기본 Azure 이름 확인을 사용하여 피어링된 가상 네트워크에서 이름을 확인할 수 없습니다. 다른 가상 네트워크에서 tooresolve 이름, 사용자 지정 DNS 서버를 사용 해야 합니다. 사용자 고유의 DNS 서버를 tooset 읽으려면 어떻게 toolearn hello [자체 DNS 서버를 사용 하 여 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) 문서.
- Hello 피어 링에서 두 가상 네트워크의 리소스와 통신할 수 서로 hello로 동일에서 듯 hello 동일 대역폭 및 대기 시간 가상 네트워크입니다. 그러나 각 가상 컴퓨터 크기에는 고유한 최대 네트워크 대역폭이 있습니다. hello를 읽고, 다른 가상 컴퓨터 크기에 대 한 최대 네트워크 대역폭에 대 한 자세한 toolearn [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 또는 [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 가상 컴퓨터의 문서 크기를 조정 합니다.
- 에 hello 동일 하는 리소스 관리자를 통해 배포 된 가상 네트워크 피어 링 할 수 또는 서로 다른 구독 합니다.
- 에 hello 동일 다양 한 배포 모델을 통해 배포 된 가상 네트워크 피어 링 할 수 또는 서로 다른 구독 (미리 보기). 
- hello 구독에 있는 두 가상 네트워크가 있어야 관련된 toohello 동일한 Azure Active Directory 테 넌 트입니다. 아직 AD 테넌트가 없는 경우 빠르게 [만들](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch) 수 있습니다. 사용할 수는 [VPN 게이트웨이](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect 두 개의 서로 다른 구독에 있는 가상 네트워크 toodifferent Active Directory 테 넌 트에 연결 합니다.
- 가상 네트워크 겹치기 tooanother 가상 네트워크 되며도 Azure 가상 네트워크 게이트웨이 사용 하 여 연결 된 tooanother 가상 네트워크를 사용할 수 있습니다. 가상 네트워크 피어 링 및 게이트웨이 통해 연결 되 면 hello 가상 네트워크 간에 트래픽을 hello 게이트웨이 보다 hello 피어 링 구성을 통해 전송 됩니다.
- 가상 네트워크 피어링을 활용하는 수신 및 송신 트래픽에 대한 명목 요금이 부과됩니다. 자세한 내용은 참조 hello [가격 책정 페이지](https://azure.microsoft.com/pricing/details/virtual-network)합니다.


## <a name="permissions"></a>권한

hello 계정 toocreate 가상 네트워크 피어 링을 사용 하 여 hello 필요한 역할 또는 사용 권한이 있어야 합니다. 예를 들어 myVnetA 및 myVnetB 라는 두 개의 가상 네트워크, 피어 링 된 경우 사용자 계정에 할당 해야 최소 역할 또는 각 가상 네트워크에 대 한 사용 권한을 다음 hello:
    
|가상 네트워크|배포 모델|역할|권한|
|---|---|---|---|
|myVnetA|리소스 관리자|[네트워크 참여자](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |클래식|[클래식 네트워크 참여자](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|해당 없음|
|myVnetB|리소스 관리자|[네트워크 참여자](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||클래식|[클래식 네트워크 참여자](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

에 대 한 자세한 내용은 [기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) 너무 특정 사용 권한을 할당 하 고[사용자 정의 역할](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (리소스 관리자에만 해당).

## <a name="next-steps"></a>다음 단계

자세한 내용은 방법 toocreate는 [허브 및 스포크 네트워크 토폴로지](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) 
