---
title: "aaaCreate는 Azure 가상 네트워크 피어 링-다양 한 배포 모델-서로 다른 구독 | Microsoft Docs"
description: "Toocreate 가상 네트워크 간의 피어 링 가상 네트워크를 만드는 방법을 각기 다른 Azure 구독에 있는 다른 Azure 배포 모델을 통해에 대해 알아봅니다."
services: virtual-network
documentationcenter: 
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
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: 865bdabb5b87523ba943d7b5dcbdc2475b78bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-and-subscriptions"></a>가상 네트워크 피어링 만들기 - 서로 다른 배포 모델 및 구독

이 자습서에서는 toocreate 다양 한 배포 모델을 통해 만든 가상 네트워크 간의 피어 링 하는 가상 네트워크를 학습 합니다. hello 가상 네트워크는 서로 다른 구독에 존재합니다. Hello에 hello 리소스 것 처럼 동일한 대역폭 및 대기 시간으로 서로 toocommunicate 서로 다른 가상 네트워크의에서 피어 링 두 가상 네트워크 사용 리소스 hello 동일한 가상 네트워크입니다. [가상 네트워크 피어링](virtual-network-peering-overview.md)에 대해 자세히 알아보세요. 

hello 단계 toocreate 피어 링 가상 네트워크는 hello 가상 네트워크는 hello 같거나 다른 데이터 집합, 구독 및 있는에 있는지 여부에 따라 다른 [Azure 배포 모델](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello 가상 네트워크가 만들어집니다. 통해 가상 a toocreate 네트워크 hello 시나리오 hello 다음 표를에서 클릭 하 여 다른 시나리오에서는 피어 링 하는 방법에 대해 알아봅니다.

|Azure 배포 모델  | Azure 구독  |
|--------- |---------|
|[둘 다 리소스 관리자](virtual-network-create-peering.md) |동일|
|[둘 다 리소스 관리자](create-peering-different-subscriptions.md) |다름|
|[하나는 Resource Manager, 하나는 클래식](create-peering-different-deployment-models.md) |동일|

Hello 클래식 배포 모델을 통해 배포 된 두 개의 가상 네트워크 간의 피어 링 가상 네트워크를 만들 수 없습니다. 동일한 hello에 존재 하는 두 개의 가상 네트워크 간에 만들 수는 가상 네트워크 피어 링 Azure 지역입니다. Toohello 연결 된 다른 구독을 구독은 둘 다 hello에 존재 하는 가상 네트워크 간의 피어 링 가상 네트워크를 만들 때 동일한 Azure Active Directory 테 넌 트. 아직 Azure Active Directory 테넌트가 없는 경우 신속히 하나 [만들](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch) 수 있습니다. hello 클래식 배포 모델을 통해 생성 된 또는 서로 다른 Azure 지역에 있는 또는 구독에 속해 있는 네트워크 연결 toodifferent Azure Active Directory 테 넌 트를 Azure를사용할수있습니다tooconnect가상필요한경우[VPN 게이트웨이](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello 가상 네트워크입니다. 

> [!WARNING]
> 서로 다른 Azure 구독에 존재하는 동서로 다른 Azure 배포 모델을 통해 만든 가상 네트워크 간의 가상 네트워크 피어링을 만드는 것은 현재 미리 보기 상태입니다. 이 시나리오에서 만든 가상 네트워크 피어 링 없을 수 있습니다 가능성 및 안정성이 피어 링 시나리오에서 일반적 공급 릴리스 가상 네트워크를 만드는 것과 동일한 수준의 hello 합니다. 이 시나리오에서 만든 가상 네트워크 피어링은 지원되지 않으며, 기능상의 제약이 있거나, 일부 Azure 지역에서 사용하지 못할 수 있습니다. 에 대 한 hello 최신 알림을 가능 여부와이 기능의 상태를 확인 hello [Azure 가상 네트워크를 업데이트](https://azure.microsoft.com/updates/?product=virtual-network) 페이지.

Hello를 사용할 수 있습니다 [Azure 포털](#portal), Azure hello [명령줄 인터페이스](#cli) (CLI) 또는 Azure [PowerShell](#powershell) toocreate 가상 네트워크 피어 링입니다. Toohello 원하는 도구를 사용 하 여 가상 네트워크 피어 링을 만들기 위한 단계를 직접 hello 이전 도구 링크 toogo 중 하나를 클릭 합니다.

## <a name="register"></a>Hello 미리 보기에 대 한 등록

hello 미리 보기에 대 한 tooregister, hello 가상 네트워크를 포함 하는 두 구독에 대해 수행 하는 전체 hello 단계 toopeer를 합니다. hello만 도구 tooregister를 사용 하 여 hello 미리 보기에는 PowerShell입니다.

1. Hello hello PowerShell의 최신 버전을 설치 [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 모듈입니다. 새 tooAzure PowerShell 인 경우 참조 [Azure PowerShell 개요](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.
2. PowerShell 세션을 시작 하 고 tooAzure hello를 사용 하 여 로그인 `login-azurermaccount` 명령입니다.
3. Hello 다음 명령을 입력 하 여 hello 미리 보기에 대 한 구독을 등록 합니다.

    ```powershell
    Register-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    
    Register-AzureRmResourceProvider `
      -ProviderNamespace Microsoft.Network
    ```
    Hello 될 때까지이 문서의 hello 포털, Azure CLI 또는 PowerShell 섹션의 hello 단계를 완료 하지 않으면 **RegistrationState** 는 hello 다음 명령을 입력 한 후 수신 출력 **등록 된** 대 한 두 구독:

    ```powershell    
    Get-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    ```

## <a name="portal"></a>피어링 만들기 - Azure Portal

이 자습서에서는 각 구독에 대해 다른 계정을 사용합니다. Tooboth 구독 사용 권한을 가진 계정으로를 사용 하는 모든 단계에 대 한 계정 동일한에서 로그 아웃 hello 포털에 대 한 hello 단계를 건너뛰고 항목과 toohello 가상 네트워크 사용 권한을 다른 사용자를 할당 하기 위한 hello 단계를 건너뛸 hello를 사용할 수 있습니다. Hello 다음 단계를 완료 하기 전에 hello 미리 보기에 등록 해야 합니다. tooregister, hello에서 단계를 완료 하는 hello [hello 미리 보기를 등록할](#register) 이 문서의 섹션. 두 구독 hello 미리 보기에 등록 될 때까지 단계를 남은 hello로 계속 하지 마십시오.
 
1. Toohello 로그인 [Azure 포털](https://portal.azure.com) UserA로 합니다. 가상 네트워크 피어 링 hello 필요한 권한을 toocreate 사용 하 여 로그인 하는 hello 계정에 있어야 합니다. Hello 참조 [권한을](#permissions) 대 한 자세한 내용은이 문서의 섹션.
2. **+ 새로 만들기**, **네트워킹**, **가상 네트워크**를 차례로 클릭합니다.
3. Hello에 **가상 네트워크 만들기** 블레이드에서 입력 하거나 hello 설정, 다음에 대 한 값을 선택한 다음 클릭 **만들기**:
    - **이름**: *myVnetA*
    - **주소 공간**: *10.0.0.0/16*
    - **서브넷 이름**: *기본값*
    - **서브넷 주소 범위**: *10.0.0.0/24*
    - **구독**: 구독 A를 선택합니다.
    - **리소스 그룹**: **새로 만들기**를 선택하고 *myResourceGroupA*를 입력합니다.
    - **위치**: *미국 동부*
4. Hello에 **리소스 검색** 형식 hello 포털의 hello 상단 상자 *myVnetA*합니다. 클릭 **myVnetA** hello 검색 결과에 표시 되 면입니다. 블레이드 hello에 대 한 표시 **myVnetA** 가상 네트워크입니다.
5. Hello에 **myVnetA** 블레이드를 놓고 클릭 **액세스 제어 (IAM)** hello 세로 hello hello 블레이드의 왼쪽에 옵션 목록에서 합니다.
6. Hello에 **myVnetA-액세스 제어 (IAM)** 블레이드를 놓고 클릭 **+ 추가**합니다.
7. Hello에 **사용 권한을 추가** 선택 표시 되 면 블레이드 **네트워크 참가자** hello에 **역할** 상자입니다.
8. Hello에 **선택** 상자 UserB 선택 하거나 입력 한 사용자 b의 전자 메일 주소 toosearch 합니다. hello 표시 된 사용자의 목록은 다음과 같이 hello에서 hello에 대 한 피어 링을 설정 하 고 hello 가상 네트워크와 같은 Azure Active Directory 테 넌 트입니다. Hello 목록에 표시 되 면 UserB를 클릭 합니다.
9. **Save**를 클릭합니다.
10. UserA로 hello 포털에서 기록 한 다음 사용자 b로 로그인 합니다.
11. 클릭 **+ 새로 만들기**, 형식 *가상 네트워크* hello에 **검색 hello 마켓플레이스** 클릭 한 다음 상자 **가상 네트워크** hello 검색 결과에서 .
12. Hello에 **가상 네트워크** 선택 표시 되 면 블레이드 **클래식** hello에 **배포 모델 선택** 클릭 한 다음 상자 **만들기**합니다.
13.   Hello 만들기 가상 네트워크 (클래식) 상자가 표시 되 면 hello 다음 값을 입력 합니다.

    - **이름**: *myVnetB*
    - **주소 공간**: *10.1.0.0/16*
    - **서브넷 이름**: *기본값*
    - **서브넷 주소 범위**: *10.1.0.0/24*
    - **구독**: 구독 B를 선택합니다.
    - **리소스 그룹**: **새로 만들기**를 선택하고 *myResourceGroupB*를 입력합니다.
    - **위치**: *미국 동부*

14. Hello에 **리소스 검색** 형식 hello 포털의 hello 상단 상자 *myVnetB*합니다. 클릭 **myVnetB** hello 검색 결과에 표시 되 면입니다. 블레이드 hello에 대 한 표시 **myVnetB** 가상 네트워크입니다.
15. Hello에 **myVnetB** 블레이드를 놓고 클릭 **속성** hello 세로 hello hello 블레이드의 왼쪽에 옵션 목록에서 합니다. 복사 hello **리소스 ID**, 이후 단계에서 사용 되는 합니다. hello 리소스 ID는 다음 예제와 비슷한 toohello: /subscriptions/<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
16. MyVnetB에 대해 5-9단계를 완료하고 8단계에서 **사용자 A**를 입력합니다.
17. 로그 UserB으로 hello 포털 아웃 한 UserA로 로그인 합니다.
18. Hello에 **리소스 검색** 형식 hello 포털의 hello 상단 상자 *myVnetA*합니다. 클릭 **myVnetA** hello 검색 결과에 표시 되 면입니다. 블레이드 hello에 대 한 표시 **myVnet** 가상 네트워크입니다.
19. **myVnetA**를 클릭합니다.
20. Hello에 **myVnetA** 블레이드를 놓고 클릭 **피어 링** hello 세로 hello hello 블레이드의 왼쪽에 옵션 목록에서 합니다.
21. Hello에 **myVnetA-피어 링** 나타나면 블레이드 클릭 **+ 추가**
22. Hello에 **추가 피어 링** 나타나는 블레이드를 입력 하거나 hello 다음 옵션을 선택한 다음 클릭 **확인**:
     - **이름**: *myVnetAToMyVnetB*
     - **가상 네트워크 배포 모델**: **클래식**을 선택합니다.
     - **리소스 ID를 알고 있음**: 이 확인란을 선택합니다.
     - **리소스 ID**: 15 단계에서 myVnetB의 hello 리소스 ID를 입력 합니다.
     - **가상 네트워크 액세스 허용:** **사용**이 선택되어 있는지 확인합니다.
    이 자습서에서 다른 설정은 사용되지 않습니다. 모든 피어 링 설정에 대 한 toolearn 읽을 [관리 가상 네트워크 피어 링](virtual-network-manage-peering.md#create-a-peering)합니다.
23. 클릭 한 후 **확인** hello 이전 단계에서 hello **추가 피어 링** 블레이드를 닫고 hello 참조 **myVnetA-피어 링** 블레이드를 다시 합니다. 몇 초 후 사용자가 만든 피어 링 hello hello 블레이드에 나타납니다. **연결** hello에 나열 된 **피어 링 상태** hello에 대 한 열 **myVnetAToMyVnetB** 만든 피어 링 있습니다. hello 피어 링 이제 설정 됩니다. 네트워크가 없습니다 필요 toopeer hello 가상 네트워크 (클래식) toohello 가상 (리소스 관리자)입니다.

    가상 네트워크 중 하나에서 만드는 모든 Azure 리소스의 IP 주소를 통해 서로 수 toocommunicate 됩니다. Hello 가상 네트워크에 대 한 기본 Azure 이름 확인을 사용 중인 경우 hello hello 가상 네트워크의 리소스가 하지 수 tooresolve 이름을 hello 가상 네트워크를 통해입니다. 피어 링의 가상 네트워크에서 tooresolve 이름을 하려는 경우 자체 DNS 서버를 만들어야 합니다. 자세한 방법을를 tooset [자체 DNS 서버를 사용 하 여 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)합니다.

24. **선택적**: 가상 컴퓨터를 만들어이 자습서에서 다루지 않습니다, 경우에 각 가상 네트워크에서 가상 컴퓨터를 만들 하 고 기타, 하나의 가상 컴퓨터 toohello toovalidate 연결에서에서 연결할 수 있습니다.
25. **선택적**:이 자습서에서 만드는 toodelete hello 리소스 hello에서 단계를 완료 hello [리소스를 삭제](#delete-portal) 이 문서의 섹션.

## <a name="cli"></a>피어링 만들기 - Azure CLI

이 자습서에서는 각 구독에 대해 다른 계정을 사용합니다. 사용 권한을 tooboth 구독이 있는 계정을 사용 하는 모든 단계에 대 한 계정을 동일한 Azure에서 로깅에 대 한 hello 단계를 건너뛸 및 사용자 역할 할당을 만드는 스크립트의 hello 줄을 제거 하는 hello를 사용할 수 있습니다. 대체 UserA@azure.com 및 UserB@azure.com 의 UserA와 사용자 b에 사용할 hello 사용자 이름 사용 하 여 스크립트를 다음 hello 모든 합니다. 

Hello 다음 단계를 완료 하기 전에 hello 미리 보기에 등록 해야 합니다. tooregister, hello에서 단계를 완료 하는 hello [hello 미리 보기를 등록할](#register) 이 문서의 섹션. 두 구독 hello 미리 보기에 등록 될 때까지 단계를 남은 hello로 계속 하지 마십시오.

1. [설치](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello Azure CLI 1.0 toocreate hello 가상 네트워크 (클래식).
2. CLI 세션을 열고 tooAzure hello를 사용 하 여 사용자 b로 로그인 `azure login` 명령입니다.
3. Hello를 입력 하 여 hello CLI 서비스 관리 모드에서 실행 `azure config mode asm` 명령입니다.
4. Hello 다음 toocreate hello 가상 네트워크 (클래식) 명령을 입력 합니다.
 
    ```azurecli
    azure network vnet create --vnet myVnetB --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```
5. Azure CLI 2.0.4 hello로 bash 셸의 사용 하 여 hello 나머지 단계를 완료 해야 이상 [설치](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json), 또는 Azure 클라우드 셸 hello를 사용 하 여 합니다. Azure 클라우드 셸 hello hello Azure 포털 내에서 직접 실행할 수 있는 무료 Bash 셸의입니다. Hello Azure CLI 사전 설치 및 toouse 사용자 계정으로 구성 된이 있습니다. Hello 클릭 **실습** hello 단추 tooyour Azure 계정이 로그인 하는 클라우드 셸을 엽니다. 나오는 스크립팅 합니다. 옵션 실행 중에 Windows 클라이언트에서 CLI 스크립트를 이용한 적, 참조 [hello Azure CLI Windows에서 실행 중인](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다. 
6. Hello 나오는 스크립트 tooa 텍스트 편집기를 사용자 PC에 복사 합니다. `<SubscriptionB-Id>`는 구독 ID로 바꿉니다. 구독 Id를 모르는 경우 입력 hello `az account show` 명령입니다. 값에 대 한 hello **id** hello 출력은 구독 id입니다. 수정 하는 hello 스크립트 tooyour CLI 2.0 세션에 붙여 복사한 다음 키를 누릅니다 `Enter`합니다. 

    ```azurecli-interactive
    az role assignment create \
      --assignee UserA@azure.com \
      --role "Classic Network Contributor" \
      --scope /subscriptions/<SubscriptionB-Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

    Azure의 hello hello 가상 네트워크를 만든을 만들 때 hello 가상 네트워크 (클래식) 4 단계에서 *기본 네트워킹* 리소스 그룹입니다.
7. Azure와 로그에 도달 하면 UserB UserA로 hello CLI 2.0 로그인 놓습니다.
8. 리소스 그룹 및 가상 네트워크(리소스 관리자)를 만듭니다. 복사 hello 다음 스크립트 tooyour CLI 세션에 붙여 넣고 다음 키를 누릅니다 `Enter`합니다. 

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
    rgName="myResourceGroupA"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network A (Resource Manager).
    az network vnet create \
      --name myVnetA \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Get hello id for myVnetA.
    vNetAId=$(az network vnet show \
      --resource-group $rgName \
      --name myVnetA \
      --query id --out tsv)

    # Assign UserB permissions toomyVnetA.
    az role assignment create \
      --assignee UserB@azure.com \
      --role "Network Contributor" \
      --scope $vNetAId
    ```

9. Hello 다양 한 배포 모델을 통해 만든 hello 두 가상 네트워크 간의 피어 링 가상 네트워크를 만듭니다. Hello 나오는 스크립트 tooa 텍스트 편집기를 사용자 PC에 복사 합니다. `<SubscriptionB-id>`는 구독 ID로 바꿉니다. 구독 Id를 모르는 경우 입력 hello `az account show` 명령입니다. 값에 대 한 hello **id** hello 출력은 구독 id입니다. Azure 명명 된 리소스 그룹의 4 단계에서 만든 가상 hello 네트워크 (클래식)를 만든 *기본 네트워킹*합니다. CLI 세션에서 수정 하는 hello 스크립트를 붙여 넣고 다음 키를 누릅니다 `Enter`합니다.

    ```azurecli-interactive
    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnetAToMyVnetB \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --remote-vnet-id  /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB \
      --allow-vnet-access
    ```

10. Hello 스크립트를 실행 한 후에 hello 가상 네트워크 (리소스 관리자)에 대 한 피어 링 hello를 검토 합니다. 다음 스크립트를 hello 복사한 CLI 세션에 붙여 넣습니다.

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --output table
    ```
    hello 출력 있는지 보여 줍니다 **연결 됨** hello에 **PeeringState** 열입니다.

    가상 네트워크 중 하나에서 만드는 모든 Azure 리소스의 IP 주소를 통해 서로 수 toocommunicate 됩니다. Hello 가상 네트워크에 대 한 기본 Azure 이름 확인을 사용 중인 경우 hello hello 가상 네트워크의 리소스가 하지 수 tooresolve 이름을 hello 가상 네트워크를 통해입니다. 피어 링의 가상 네트워크에서 tooresolve 이름을 하려는 경우 자체 DNS 서버를 만들어야 합니다. 자세한 방법을를 tooset [자체 DNS 서버를 사용 하 여 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)합니다.

11. **선택적**: 가상 컴퓨터를 만들어이 자습서에서 다루지 않습니다, 경우에 각 가상 네트워크에서 가상 컴퓨터를 만들 하 고 기타, 하나의 가상 컴퓨터 toohello toovalidate 연결에서에서 연결할 수 있습니다.
12. **선택적**:이 자습서에서 만드는 toodelete hello 리소스의 단계를 완료 hello [리소스를 삭제](#delete-cli) 이 문서의 내용입니다.

## <a name="powershell"></a>피어링 만들기 - PowerShell

이 자습서에서는 각 구독에 대해 다른 계정을 사용합니다. 사용 권한을 tooboth 구독이 있는 계정을 사용 하는 모든 단계에 대 한 계정을 동일한 Azure에서 로깅에 대 한 hello 단계를 건너뛸 및 사용자 역할 할당을 만드는 스크립트의 hello 줄을 제거 하는 hello를 사용할 수 있습니다. 대체 UserA@azure.com 및 UserB@azure.com 의 UserA와 사용자 b에 사용할 hello 사용자 이름 사용 하 여 스크립트를 다음 hello 모든 합니다. 

Hello 다음 단계를 완료 하기 전에 hello 미리 보기에 등록 해야 합니다. tooregister, hello에서 단계를 완료 하는 hello [hello 미리 보기를 등록할](#register) 이 문서의 섹션. 두 구독 hello 미리 보기에 등록 될 때까지 단계를 남은 hello로 계속 하지 마십시오.

1. Hello hello PowerShell의 최신 버전을 설치 [Azure](https://www.powershellgallery.com/packages/Azure) 및 [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 모듈입니다. 새 tooAzure PowerShell 인 경우 참조 [Azure PowerShell 개요](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.
2. PowerShell 세션을 시작합니다.
3. PowerShell에서 UserB tooUserB의 구독에 입력 하 여 로그인 hello `Add-AzureAccount` 명령입니다.
4. PowerShell 사용 하 여 가상 네트워크 (클래식) toocreate 있습니다 새로 만들거나 수정 해야는 기존 네트워크 구성 파일입니다. 너무 방법에 대해 알아봅니다[내보내기, 업데이트 및 네트워크 구성 파일을 가져올](virtual-networks-using-network-configuration-file.md)합니다. hello 파일에 포함할지 hello 다음 **VirtualNetworkSite** 이 자습서에 사용 된 hello 가상 네트워크에 대 한 요소:

    ```xml
    <VirtualNetworkSite name="myVnetB" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > 변경 된 네트워크 구성 파일을 가져오는 변경 될 수 tooexisting 가상 네트워크 (클래식)를 구독 합니다. 만 hello 이전 가상 네트워크를 추가 하 고 변경 하거나 구독에서 기존 가상 네트워크를 제거 하지 확인 합니다. 

5. Hello를 입력 하 여 UserB toouse 리소스 관리자 명령으로 tooUserB의 구독에 로그인 `login-azurermaccount` 명령입니다.
6. 2. 복사 hello 다음 스크립트 PC에서 tooa 텍스트 편집기 및 바꾸기 할당 UserA 권한 toovirtual 네트워크 `<SubscriptionB-id>` hello 2. 구독 ID로 Hello 구독 Id를 모르는 경우 입력 hello `Get-AzureRmSubscription` 명령 tooview 것입니다. 값에 대 한 hello **Id** hello 반환 출력은 프로그램 구독 id입니다. Azure 명명 된 리소스 그룹의 4 단계에서 만든 가상 hello 네트워크 (클래식)를 만든 *기본 네트워킹*합니다. tooexecute hello 스크립트 복사 hello 수정 된 스크립트 tooPowerShell에 붙여 넣고 다음 키를 누릅니다 `Enter`합니다.
    
    ```powershell 
    New-AzureRmRoleAssignment `
      -SignInName UserA@azure.com `
      -RoleDefinitionName "Classic Network Contributor" `
      -Scope /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

7. UserB으로 Azure에서 로그 아웃 하 고 hello를 입력 하 여 UserA tooUserA의 구독에 로그인 `login-azurermaccount` 명령입니다. 가상 네트워크 피어 링 hello 필요한 권한을 toocreate 사용 하 여 로그인 하는 hello 계정에 있어야 합니다. Hello 참조 [권한을](#permissions) 대 한 자세한 내용은이 문서의 섹션.
8. 다음 스크립트를 tooPowerShell, 한 키를 눌러 다음에 붙여 넣어 hello를 복사 하 여 hello 가상 네트워크 (리소스 관리자)을 만들 `Enter`:

    ```powershell
    # Variables for common values
      $rgName='MyResourceGroupA'
      $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network A.
    $vnetA = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnetA' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location
    ```

9. 사용 권한 toomyVnetA UserB를 할당 합니다. 복사 hello 다음 스크립트 PC에서 tooa 텍스트 편집기 및 바꾸기 `<SubscriptionA-Id>` hello 1. 구독 ID로 Hello 구독 Id를 모르는 경우 입력 hello `Get-AzureRmSubscription` 명령 tooview 것입니다. 값에 대 한 hello **Id** hello 반환 출력은 프로그램 구독 id입니다. PowerShell에서 hello hello 스크립트의 수정된 버전을 붙여 넣고 다음 키를 누릅니다 `Enter` tooexecute 것입니다.

    ```powershell
    New-AzureRmRoleAssignment `
      -SignInName UserB@azure.com `
      -RoleDefinitionName "Network Contributor" `
      -Scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```

10. 복사 hello 다음 스크립트 pc에서는 tooa 텍스트 편집기 및 바꾸기 `<SubscriptionB-id>` 구독 B. toopeer myVnetA toomyVNetB의 hello ID로 수정 hello 스크립트, tooPowerShell에 붙여 복사한 다음 키를 누릅니다 `Enter`합니다.

    ```powershell
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnetAToMyVnetB' `
      -VirtualNetwork $vnetA `
      -RemoteVirtualNetworkId /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

11. 다음 스크립트를 PowerShell 및 키를 눌러에 붙여 넣어 hello를 복사 하 여 myVnetA의 hello 피어 링 상태를 볼 `Enter`합니다.

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName $rgName `
      -VirtualNetworkName myVnetA `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    hello 상태가 **연결 됨**합니다. 너무 변경**연결 됨** hello 피어 링 toomyVnetA myVnetB에서 설정 되 면입니다.

    가상 네트워크 중 하나에서 만드는 모든 Azure 리소스의 IP 주소를 통해 서로 수 toocommunicate 됩니다. Hello 가상 네트워크에 대 한 기본 Azure 이름 확인을 사용 중인 경우 hello hello 가상 네트워크의 리소스가 하지 수 tooresolve 이름을 hello 가상 네트워크를 통해입니다. 피어 링의 가상 네트워크에서 tooresolve 이름을 하려는 경우 자체 DNS 서버를 만들어야 합니다. 자세한 방법을를 tooset [자체 DNS 서버를 사용 하 여 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)합니다.

12. **선택적**: 가상 컴퓨터를 만들어이 자습서에서 다루지 않습니다, 경우에 각 가상 네트워크에서 가상 컴퓨터를 만들 하 고 기타, 하나의 가상 컴퓨터 toohello toovalidate 연결에서에서 연결할 수 있습니다.
13. **선택적**:이 자습서에서 만드는 toodelete hello 리소스의 단계를 완료 hello [리소스를 삭제](#delete-powershell) 이 문서의 내용입니다.

## <a name="permissions"></a>권한

hello 계정 toocreate 가상 네트워크 피어 링을 사용 하 여 hello 필요한 역할 또는 사용 권한이 있어야 합니다. 예를 들어 myVnetA 및 myVnetB 라는 두 개의 가상 네트워크, 피어 링 된 경우 사용자 계정에 할당 해야 최소 역할 또는 각 가상 네트워크에 대 한 사용 권한을 다음 hello:
    
|가상 네트워크|배포 모델|역할|권한|
|---|---|---|---|
|myVnetA|리소스 관리자|[네트워크 참여자](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |클래식|[클래식 네트워크 참여자](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|해당 없음|
|myVnetB|리소스 관리자|[네트워크 참여자](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||클래식|[클래식 네트워크 참여자](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

에 대 한 자세한 내용은 [기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) 너무 특정 사용 권한을 할당 하 고[사용자 정의 역할](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (리소스 관리자에만 해당).

## <a name="delete"></a>리소스 삭제
이 자습서를 마친 toodelete hello 리소스 사용량에 따른 요금을 발생 하지 않습니다 하므로 hello 자습서에서 만든 할 수 있습니다. 리소스 그룹을 삭제 하면 hello 리소스 그룹에는 모든 리소스를 삭제 합니다.

### <a name="delete-portal"></a>Azure Portal

1. Hello 포털 검색 상자에 입력 **myResourceGroupA**합니다. Hello 검색 결과에서 클릭 **myResourceGroupA**합니다.
2. Hello에 **myResourceGroupA** 블레이드에서 hello 클릭 **삭제** 아이콘입니다.
3. hello에 tooconfirm hello 삭제 **형식 hello 리소스 그룹 이름은** 상자에 입력 **myResourceGroupA**, 클릭 하 고 **삭제**합니다.
4. Hello에 **리소스 검색** 형식 hello 포털의 hello 상단 상자 *myVnetB*합니다. 클릭 **myVnetB** hello 검색 결과에 표시 되 면입니다. 블레이드 hello에 대 한 표시 **myVnetB** 가상 네트워크입니다.
5. Hello에 **myVnetB** 블레이드에서 클릭 **삭제**합니다.
6. tooconfirm hello 삭제 클릭 **예** hello에 **가상 네트워크 삭제** 상자입니다.

### <a name="delete-cli"></a>Azure CLI

1. 다음 명령을 hello로 CLI 2.0 toodelete hello 가상 네트워크 (리소스 관리자) tooAzure hello를 사용 하 여에 로그인 합니다.

    ```azurecli-interactive
    az group delete --name myResourceGroupA --yes
    ```

2. 명령 다음 hello로 Azure CLI 1.0 toodelete hello 가상 네트워크 (클래식) tooAzure hello를 사용 하 여에 로그인 합니다.

    ```azurecli
    azure config mode asm 

    azure network vnet delete --vnet myVnetB --quiet
    ```

### <a name="delete-powershell"></a>PowerShell

1. Hello PowerShell 명령 프롬프트에서 다음 명령을 toodelete hello 가상 네트워크 (리소스 관리자) hello를 입력 합니다.

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupA -Force
    ```

2. toodelete hello 가상 네트워크 (클래식) PowerShell과 함께 기존 네트워크 구성 파일을 수정 해야 합니다. 너무 방법에 대해 알아봅니다[내보내기, 업데이트 및 네트워크 구성 파일을 가져올](virtual-networks-using-network-configuration-file.md)합니다. 이 자습서에 사용 된 hello 가상 네트워크에 대 한 VirtualNetworkSite 요소 다음에 오는 hello를 제거 합니다.

    ```xml
    <VirtualNetworkSite name="myVnetB" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > 변경 된 네트워크 구성 파일을 가져오는 변경 될 수 tooexisting 가상 네트워크 (클래식)를 구독 합니다. 만 hello 이전 가상 네트워크를 제거 하 고 변경 하거나 구독에서 다른 기존 가상 네트워크를 제거 하지 확인 합니다. 

## <a name="next-steps"></a>다음 단계

- 프로덕션 환경에 사용하기 위한 가상 네트워크 피어링을 만들기 전에 먼저 중요한 [가상 네트워크 피어링 제약 조건 및 동작](virtual-network-manage-peering.md#requirements-and-constraints)에 철저하게 익숙해집니다.
- 모든 [가상 네트워크 피어링 설정](virtual-network-manage-peering.md#create-a-peering)에 대해 알아봅니다.
- 너무 방법에 대해 알아봅니다[허브를 만들고 네트워크 토폴로지 스포크](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) 가상 네트워크 피어 링을 사용 합니다.
