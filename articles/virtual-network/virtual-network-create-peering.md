---
title: "aaaCreate는 Azure 가상 네트워크 피어 링-리소스 관리자-동일한 구독 | Microsoft Docs"
description: "Toocreate 리소스 관리자를 통해 동일한 hello에 존재 하는 가상 네트워크 간의 가상 네트워크 피어 링 생성 하는 방법을 알아보려면 Azure 구독."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 026bca75-2946-4c03-b4f6-9f3c5809c69a
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: c2d24fdc8103c09c3bfb8e59be12e301d9e9a55a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-same-subscription"></a>가상 네트워크 피어링 만들기 - Resource Manager, 동일한 구독

이 자습서에서는 toocreate 리소스 관리자를 통해 만든 가상 네트워크 간의 피어 링 하는 가상 네트워크를 학습 합니다. Hello에 두 가상 네트워크가 있는 동일한 구독 합니다. Hello에 hello 리소스 것 처럼 동일한 대역폭 및 대기 시간으로 서로 toocommunicate 서로 다른 가상 네트워크의에서 피어 링 두 가상 네트워크 사용 리소스 hello 동일한 가상 네트워크입니다. [가상 네트워크 피어링](virtual-network-peering-overview.md)에 대해 자세히 알아보세요. 

hello 단계 toocreate 피어 링 가상 네트워크는 hello 가상 네트워크는 hello 같거나 다른 데이터 집합, 구독 및 있는에 있는지 여부에 따라 다른 [Azure 배포 모델](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello 가상 네트워크가 만들어집니다. 통해 가상 a toocreate 네트워크 hello 시나리오 hello 다음 표를에서 클릭 하 여 다른 시나리오에서는 피어 링 하는 방법에 대해 알아봅니다.

|Azure 배포 모델  | Azure 구독  |
|--------- |---------|
|[둘 다 Resource Manager](create-peering-different-subscriptions.md) |다름|
|[하나는 Resource Manager, 하나는 클래식](create-peering-different-deployment-models.md) |동일|
|[하나는 Resource Manager, 하나는 클래식](create-peering-different-deployment-models-subscriptions.md) |다름|

Hello 클래식 배포 모델을 통해 배포 된 두 개의 가상 네트워크 간의 피어 링 가상 네트워크를 만들 수 없습니다. 동일한 hello에 존재 하는 두 개의 가상 네트워크 간에 만들 수는 가상 네트워크 피어 링 Azure 지역입니다. Azure를 사용할 수 있는 hello 클래식 배포 모델을 통해 생성 된 또는 서로 다른 Azure 지역에 있는 가상 네트워크 tooconnect 해야 할 경우 [VPN 게이트웨이](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello 가상 네트워크입니다. 

Hello를 사용할 수 있습니다 [Azure 포털](#portal), Azure hello [명령줄 인터페이스](#cli) (CLI) Azure [PowerShell](#powershell), 또는 [Azure리소스관리자템플릿](#template) toocreate 가상 네트워크 피어 링입니다. Toohello 원하는 도구를 사용 하 여 가상 네트워크 피어 링을 만들기 위한 단계를 직접 hello 이전 도구 링크 toogo 중 하나를 클릭 합니다.

## <a name="portal"></a>피어링 만들기 - Azure Portal

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다. 가상 네트워크 피어 링 hello 필요한 권한을 toocreate 사용 하 여 로그인 하는 hello 계정에 있어야 합니다. Hello 참조 [권한을](#permissions) 대 한 자세한 내용은이 문서의 섹션.
2. **+ 새로 만들기**, **네트워킹**, **가상 네트워크**를 차례로 클릭합니다.
3. Hello에 **가상 네트워크 만들기** 블레이드에서 입력 하거나 hello 설정, 다음에 대 한 값을 선택한 다음 클릭 **만들기**:
    - **이름**: *myVnet1*
    - **주소 공간**: *10.0.0.0/16*
    - **서브넷 이름**: *기본값*
    - **서브넷 주소 범위**: *10.0.0.0/24*
    - **구독**: 사용자의 구독을 선택합니다.
    - **리소스 그룹**: **새로 만들기**를 선택하고 *myResourceGroup*을 입력합니다.
    - **위치**: *미국 동부*
4. 단계 2-3 다음 3 단계에서 값에는 hello를 다시 지정을 완료 합니다.
    - **이름**: *myVnet2*
    - **주소 공간**: *10.1.0.0/16*
    - **서브넷 이름**: *기본값*
    - **서브넷 주소 범위**: *10.1.0.0/24*
    - **구독**: 사용자의 구독을 선택합니다.
    - **리소스 그룹**: **기존 항목 사용**을 선택하고 *myResourceGroup*을 선택합니다.
    - **위치**: *미국 동부*
5. Hello에 **리소스 검색** 형식 hello 포털의 hello 상단 상자 *myResourceGroup*합니다. 클릭 **myResourceGroup** hello 검색 결과에 표시 되 면입니다. 블레이드 hello에 대 한 표시 **myresourcegroup** 리소스 그룹입니다. hello 리소스 그룹 이전 단계에서 만든 hello 두 가상 네트워크를 포함 합니다.
6. **myVNet1**을 클릭합니다.
7. Hello에 **myVnet1** 블레이드를 놓고 클릭 **피어 링** hello 세로 hello hello 블레이드의 왼쪽에 옵션 목록에서 합니다.
8. Hello에 **myVnet1-피어 링** 나타나면 블레이드 클릭 **+ 추가**
9. Hello에 **추가 피어 링** 나타나는 블레이드를 입력 하거나 hello 다음 옵션을 선택한 다음 클릭 **확인**:
     - **이름**: *myVnet1ToMyVnet2*
     - **가상 네트워크 배포 모델**: **Resource Manager**를 선택합니다. 
     - **구독**: 사용자의 구독을 선택합니다.
     - **가상 네트워크**: **가상 네트워크 선택**을 클릭한 다음 **myVnet2**를 클릭합니다.
     - **가상 네트워크 액세스 허용:** **사용**이 선택되어 있는지 확인합니다.
    이 자습서에서 다른 설정은 사용되지 않습니다. 모든 피어 링 설정에 대 한 toolearn 읽을 [관리 가상 네트워크 피어 링](virtual-network-manage-peering.md#create-a-peering)합니다.
10. 클릭 한 후 **확인** hello 이전 단계에서 hello **추가 피어 링** 블레이드를 닫고 hello 참조 **myVnet1-피어 링** 블레이드를 다시 합니다. 몇 초 후 사용자가 만든 피어 링 hello hello 블레이드에 나타납니다. **시작** hello에 나열 된 **피어 링 상태** hello에 대 한 열 **myVnet1ToMyVnet2** 만든 피어 링 있습니다. Vnet1 tooVnet2 살펴본 하지만 myVnet2 toomyVnet1 피어 투 피어 해야 이제 합니다. hello 피어 링 만들어야 양방향에서 hello 가상 네트워크 toocommunicate의 tooenable 리소스 서로 합니다.
11. myVnet2에 대해 5~10단계를 다시 완료합니다.  이름 hello 피어 링 *myVnet2ToMyVnet1*합니다.
12. 클릭 한 후 몇 초 **확인** toocreate hello 피어 링 MyVnet2에 대 한 hello **myVnet2ToMyVnet1** 방금 만든 피어 링이 함께 나열 **연결 됨** hello 에서 **피어 링 상태** 열입니다.
13. MyVnet1에 대해 5~7단계를 다시 완료합니다. hello **피어 링 상태** hello에 대 한 **myVnet1ToVNet2** 피어 링는 현재 **연결 됨**합니다. hello 피어 링은 성공적으로 설정 확인 한 후 **연결 됨** hello에 **피어 링 상태** hello 피어 링에서 두 가상 네트워크에 대 한 열입니다.
14. **선택적**: 가상 컴퓨터를 만들어이 자습서에서 다루지 않습니다, 경우에 각 가상 네트워크에서 가상 컴퓨터를 만들 하 고 기타, 하나의 가상 컴퓨터 toohello toovalidate 연결에서에서 연결할 수 있습니다.
15. **선택적**:이 자습서에서 만드는 toodelete hello 리소스 hello에서 단계를 완료 hello [리소스를 삭제](#delete-portal) 이 문서의 섹션.

가상 네트워크 중 하나에서 만드는 모든 Azure 리소스의 IP 주소를 통해 서로 수 toocommunicate 됩니다. Hello 가상 네트워크에 대 한 기본 Azure 이름 확인을 사용 중인 경우 hello hello 가상 네트워크의 리소스가 하지 수 tooresolve 이름을 hello 가상 네트워크를 통해입니다. 피어 링의 가상 네트워크에서 tooresolve 이름을 하려는 경우 자체 DNS 서버를 만들어야 합니다. 자세한 방법을를 tooset [자체 DNS 서버를 사용 하 여 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)합니다.

## <a name="cli"></a>피어링 만들기 - Azure CLI

다음 스크립트는 hello:

- Hello Azure CLI 버전 2.0.4 필요 이상. toofind hello 버전을 실행 hello `az --version` 명령입니다. Tooupgrade 필요한 경우 참조 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.
- Bash 셸에서 작동합니다. Windows 클라이언트에서 Azure CLI 스크립트를 실행 하는 옵션에 대 한 참조 [hello Azure CLI Windows에서 실행 중인](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다. 

CLI hello 및 해당 종속성을 설치 하는 대신 Azure 클라우드 셸 hello를 사용할 수 있습니다. Azure 클라우드 셸 hello hello Azure 포털 내에서 직접 실행할 수 있는 무료 Bash 셸의입니다. Hello Azure CLI 사전 설치 및 toouse 사용자 계정으로 구성 된이 있습니다. Hello 클릭 **실습** 된 Azure 계정 로그는 클라우드 셸을 호출 하는 다음과 같이 tooyour 로그인 할 수 있는 hello 스크립트에서 단추입니다. tooexecute 스크립트 hello를 hello 클릭 **복사** 단추 및 클라우드 Shell에 hello 내용을 붙여 넣습니다.

1. 리소스 그룹 하나와 두 개의 가상 네트워크를 만듭니다.

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
    rgName="myResourceGroup"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network 1.
    az network vnet create \
      --name myVnet1 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Create virtual network 2.
    az network vnet create \
      --name myVnet2 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.1.0.0/16
    ```

2. Hello 두 가상 네트워크 간의 피어 링 가상 네트워크를 만듭니다.
 
    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet1 \
      --query id --out tsv)

    # Get hello id for VNet2.
    vnet2Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet2 \
      --query id \
      --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group $rgName \
      --vnet-name myVnet1 \
      --remote-vnet-id $vnet2Id \
      --allow-vnet-access

    # Peer VNet2 tooVNet1.
    az network vnet peering create \
      --name myVnet2ToMyVnet1 \
      --resource-group $rgName \
      --vnet-name myVnet2 \
      --remote-vnet-id $vnet1Id \
      --allow-vnet-access
    ```

3. Hello 스크립트를 실행 한 후 각 가상 네트워크에 대 한 hello 피어 링을 검토 합니다. 

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    Hello 이전 명령의 다시 실행 하 여 대체 *myVnet1* 와 *myVnet2*합니다. hello 출력 둘 다의 명령을 보여 줍니다 **연결 됨** hello에 **PeeringState** 열입니다.

     가상 네트워크 중 하나에서 만드는 모든 Azure 리소스의 IP 주소를 통해 서로 수 toocommunicate 됩니다. Hello 가상 네트워크에 대 한 기본 Azure 이름 확인을 사용 중인 경우 hello hello 가상 네트워크의 리소스가 하지 수 tooresolve 이름을 hello 가상 네트워크를 통해입니다. 피어 링의 가상 네트워크에서 tooresolve 이름을 하려는 경우 자체 DNS 서버를 만들어야 합니다. 자세한 방법을를 tooset [자체 DNS 서버를 사용 하 여 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)합니다.

4. **선택적**: 가상 컴퓨터를 만들어이 자습서에서 다루지 않습니다, 경우에 각 가상 네트워크에서 가상 컴퓨터를 만들 하 고 기타, 하나의 가상 컴퓨터 toohello toovalidate 연결에서에서 연결할 수 있습니다.
5. **선택적**:이 자습서에서 만드는 toodelete hello 리소스의 단계를 완료 hello [리소스를 삭제](#delete-cli) 이 문서의 내용입니다.


## <a name="powershell"></a>피어링 만들기 - PowerShell

1. Hello hello PowerShell의 최신 버전을 설치 [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 모듈입니다. 새 tooAzure PowerShell 인 경우 참조 [Azure PowerShell 개요](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.
2. PowerShell 세션 toostart 너무 이동**시작**, 입력 **powershell**, 클릭 하 고 **PowerShell**합니다.
3. PowerShell에서 로그인 tooAzure hello를 입력 하 여 `login-azurermaccount` 명령입니다. 가상 네트워크 피어 링 hello 필요한 권한을 toocreate 사용 하 여 로그인 하는 hello 계정에 있어야 합니다. Hello 참조 [권한을](#permissions) 대 한 자세한 내용은이 문서의 섹션.
4. 리소스 그룹 하나와 두 개의 가상 네트워크를 만듭니다. tooexecute hello 스크립트 복사 hello 다음 스크립트, PowerShell에 붙여을 누릅니다 `Enter` hello 마지막 줄 hello 화면에 표시 된 후:

    ```powershell
    # Variables for common values used throughout hello script.
    $rgName='myResourceGroup'
    $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network 1.
    $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location

    # Create virtual network 2.
    $vnet2 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet2' `
      -AddressPrefix '10.1.0.0/16' `
      -Location $location
    ```

5. Hello 두 가상 네트워크 간의 피어 링 가상 네트워크를 만듭니다. 복사 hello 다음 스크립트 tooPowerShell에 붙여 넣고 다음 키를 누릅니다 `Enter` hello 마지막 줄 hello 화면에 표시 된 후:
    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet1ToMyVnet2' `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId $vnet2.Id

    # Peer VNet2 tooVNet1.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet2ToMyVnet1' `
      -VirtualNetwork $vnet2 `
      -RemoteVirtualNetworkId $vnet1.Id
    ```
6. tooreview hello 서브넷 hello 가상 네트워크에 대 한 복사 hello 다음 명령, tooPowerShell, 붙여 및 키를 누릅니다 `Enter`:

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    Hello 이전 명령의 다시 실행 하 여 대체 *myVnet1* 와 *myVnet2*합니다. hello 출력 둘 다의 명령을 보여 줍니다 **연결 됨** hello에 **PeeringState** 열입니다.
7. **선택적**: 가상 컴퓨터를 만들어이 자습서에서 다루지 않습니다, 경우에 각 가상 네트워크에서 가상 컴퓨터를 만들 하 고 기타, 하나의 가상 컴퓨터 toohello toovalidate 연결에서에서 연결할 수 있습니다.
8. **선택적**:이 자습서에서 만드는 toodelete hello 리소스의 단계를 완료 hello [리소스를 삭제](#delete-powershell) 이 문서의 내용입니다.

가상 네트워크 중 하나에서 만드는 모든 Azure 리소스의 IP 주소를 통해 서로 수 toocommunicate 됩니다. Hello 가상 네트워크에 대 한 기본 Azure 이름 확인을 사용 중인 경우 hello hello 가상 네트워크의 리소스가 하지 수 tooresolve 이름을 hello 가상 네트워크를 통해입니다. 피어 링의 가상 네트워크에서 tooresolve 이름을 하려는 경우 자체 DNS 서버를 만들어야 합니다. 자세한 방법을를 tooset [자체 DNS 서버를 사용 하 여 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)합니다.

## <a name="template"></a>피어링 만들기 - Resource Manager 템플릿

1. [가상 네트워크 피어링 만들기](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) Resource Manager 템플릿을 참조합니다. 지침에는 Azure 포털, PowerShell 또는 Azure CLI hello hello를 사용 하 여 hello 서식 파일을 배포 하기 위한 hello 템플릿과 함께 제공 됩니다. 로그에 있는 계정을 사용 하 여 toodeploy hello 템플릿을 선택 하면 toowhichever 도구 가상 네트워크 피어 링 필요한 권한을 toocreate hello 합니다. Hello 참조 [권한을](#permissions) 대 한 자세한 내용은이 문서의 섹션.
2. **선택적**: 가상 컴퓨터를 만들어이 자습서에서 다루지 않습니다, 경우에 각 가상 네트워크에서 가상 컴퓨터를 만들 하 고 기타, 하나의 가상 컴퓨터 toohello toovalidate 연결에서에서 연결할 수 있습니다.
3. **선택적**:이 자습서에서 만드는 toodelete hello 리소스 hello에서 단계를 완료 hello [리소스를 삭제](#delete) 중 하나를 사용 하 여이 문서의 섹션 hello Azure 포털, PowerShell 또는 Azure CLI hello 합니다.

## <a name="permissions"></a>권한

hello 계정 toocreate 가상 네트워크 피어 링을 사용 하 여 hello 필요한 역할 또는 사용 권한이 있어야 합니다. 예를 들어 VNet1 및 VNet2 라는 두 개의 가상 네트워크, 피어 링 된 경우 사용자 계정에 할당 해야 최소 역할 또는 각 가상 네트워크에 대 한 사용 권한을 다음 hello:
    
|가상 네트워크|역할|권한|
|---|---|---|
|VNet1|[네트워크 참여자](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
|VNet2|[네트워크 참여자](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|

에 대 한 자세한 내용은 [기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) 너무 특정 사용 권한을 할당 하 고[사용자 정의 역할](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (리소스 관리자에만 해당).

## <a name="delete"></a>리소스 삭제
이 자습서를 마친 toodelete hello 리소스 사용량에 따른 요금을 발생 하지 않습니다 하므로 hello 자습서에서 만든 할 수 있습니다. 리소스 그룹을 삭제 하면 hello 리소스 그룹에는 모든 리소스를 삭제 합니다.

### <a name="delete-portal"></a>Azure Portal

1. Hello 포털 검색 상자에 입력 **myResourceGroup**합니다. Hello 검색 결과에서 클릭 **myResourceGroup**합니다.
2. Hello에 **myResourceGroup** 블레이드에서 hello 클릭 **삭제** 아이콘입니다.
3. hello에 tooconfirm hello 삭제 **형식 hello 리소스 그룹 이름은** 상자에 입력 **myResourceGroup**, 클릭 하 고 **삭제**합니다.

### <a name="delete-cli"></a>Azure CLI

Hello 다음 명령을 입력 합니다.

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <a name="delete-powershell"></a>PowerShell

Hello 다음 명령을 입력 합니다.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -force
```

## <a name="next-steps"></a>다음 단계

- 프로덕션 환경에 사용하기 위한 가상 네트워크 피어링을 만들기 전에 먼저 중요한 [가상 네트워크 피어링 제약 조건 및 동작](virtual-network-manage-peering.md#requirements-and-constraints)에 철저하게 익숙해집니다.
- 모든 [가상 네트워크 피어링 설정](virtual-network-manage-peering.md#create-a-peering)에 대해 알아봅니다.
- 너무 방법에 대해 알아봅니다[허브를 만들고 네트워크 토폴로지 스포크](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) 가상 네트워크 피어 링을 사용 합니다.
