---
title: "Azure 가상 네트워크 (클래식)를 여러 서브넷 aaaCreate | Microsoft Docs"
description: "자세한 내용은 방법 toocreate Azure에서 다중 서브넷 가상 네트워크 (클래식)."
services: virtual-network
documentationcenter: 
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
ms.date: 07/31/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: cc7b9ad08d5c26dba09584762bedf614d2847032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a>여러 서브넷이 있는 가상 네트워크(클래식) 만들기

> [!IMPORTANT]
> Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)이라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. Hello 통해 대부분 새 가상 네트워크를 만드는 것이 좋습니다 [리소스 관리자](virtual-networks-create-vnet-arm-pportal.md) 배포 모델입니다.

이 자습서에서는 toocreate 기본 Azure 가상 네트워크 (클래식)가 공용 및 개인 서브넷을 분리 하는 방법에 대해 알아봅니다. Virtual Machines 및 서브넷에 있는 Cloud Services와 같은 Azure 리소스를 만들 수 있습니다. 가상 네트워크 (클래식)에서 생성 된 리소스는 서로 다른 네트워크 연결 된 tooa 가상 네트워크의 리소스와 통신할 수 있습니다.

모든 [가상 네트워크](virtual-network-manage-network.md) 및 [서브넷](virtual-network-manage-subnet.md) 설정에 대해 자세히 확인하세요.

> [!WARNING]
> [구독이 비활성화되는](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit) 경우 Azure에서 가상 네트워크(클래식)가 즉시 삭제됩니다. 가상 네트워크 (클래식) 리소스는 hello 가상 네트워크에 존재 하는지 여부에 관계 없이 삭제 됩니다. 나중에 다시 사용 하면 hello 구독, hello 가상 네트워크에 존재 하는 리소스를 다시 만들어야 합니다.

Hello를 사용 하 여 가상 네트워크 (클래식)를 만들 수 있습니다 [Azure 포털](#portal), hello [Azure CLI (명령줄 인터페이스) 1.0](#azure-cli), 또는 [PowerShell](#powershell)합니다.

## <a name="portal"></a>포털

1. 인터넷 브라우저를 이동 toohello [Azure 포털](https://portal.azure.com)합니다. [Azure 계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)을 사용하여 로그인합니다. Azure 계정이 없으면 [무료 평가판](https://azure.microsoft.com/offers/ms-azr-0044p)에 등록할 수 있습니다.
2. 클릭 **+ 새로 만들기** hello 포털에서입니다.
3. 입력 *가상 네트워크* hello에 **검색 hello 마켓플레이스** hello의 hello 상단 상자 **새로 만들기** 블레이드를 표시 합니다.  클릭 **가상 네트워크** hello 검색 결과에 표시 되 면입니다.
4. 선택 **클래식** hello에 **배포 모델 선택** 상자 hello에 **가상 네트워크** 블레이드를 놓고 클릭 한 다음 **만들기**합니다. 
5. 입력 값에 나오는 hello에 hello **가상 네트워크 만들기 (클래식)** 블레이드에 대 한 클릭 **만들기**:

    |설정|값|
    |---|---|
    |이름|myVnet|
    |주소 공간|10.0.0.0/16|
    |서브넷 이름|공용|
    |서브넷 주소 범위|10.0.0.0/24|
    |리소스 그룹|**새로 만들기**를 선택한 채로 두고 **myResourceGroup**을 입력합니다.|
    |구독 및 위치|구독 및 위치를 선택합니다.

    새 tooAzure 인 경우에 대해 자세히 알아보세요 [리소스 그룹](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [구독](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), 및 [위치](https://azure.microsoft.com/regions) (tooas 라고도 *영역*).
4. Hello 포털에서 가상 네트워크를 만들 때 서브넷이 하나만 만들 수 있습니다. 이 자습서에서는 hello 가상 네트워크를 만든 후 두 번째 서브넷을 만듭니다. 인터넷에서 액세스할 수 있는 리소스 hello 나중에 만들 수 있습니다 **공용** 서브넷입니다. 또한 hello에 hello 인터넷에서에서 액세스할 수 없는 리소스를 만들 수 있습니다 **개인** 서브넷입니다. toocreate hello 두 번째 서브넷을 입력 **myVnet** hello에 **리소스 검색** hello hello 페이지 위쪽에 상자입니다. 클릭 **myVnet** hello 검색 결과에 표시 되 면입니다.
5. 클릭 **서브넷** (hello에 **설정** 섹션) hello에 **가상 네트워크 만들기 (클래식)** 블레이드를 표시 합니다.
6. 클릭 **+ 추가** hello에 **myVnet-서브넷** 블레이드를 표시 합니다.
7. 입력 **개인** 에 대 한 **이름** hello에 **서브넷 추가** 블레이드입니다. **주소 범위**에 **10.0.1.0/24**를 입력합니다.  **확인**을 클릭합니다.
8. Hello에 **myVnet-서브넷** 블레이드에서 hello를 볼 수 있습니다 **공용** 및 **개인** 만든 서브넷입니다.
9. **선택적**:이 자습서를 완료 하면 사용 요금을 발생 하지 않습니다 수 있도록 사용자가 만든 toodelete hello 리소스 할 수 있습니다.
    - 클릭 **개요** hello에 **myVnet** 블레이드입니다.
    - Hello 클릭 **삭제** hello에 아이콘 **myVnet** 블레이드입니다.
    - tooconfirm hello 삭제 클릭 **예** hello에 **가상 네트워크 삭제** 상자입니다.

## <a name="azure-cli"></a>Azure CLI

1. 유지할 수 있습니다 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), 하거나 hello Azure 클라우드 셸 내에서 CLI hello를 사용 합니다. Azure 클라우드 셸 hello hello Azure 포털 내에서 직접 실행할 수 있는 무료 Bash 셸의입니다. Hello Azure CLI 사전 설치 및 toouse 사용자 계정으로 구성 된이 있습니다. CLI 명령에 대 한 도움말 tooget 입력 `azure <command> --help`합니다. 
2. CLI 세션에서 tooAzure 뒤에 오는 hello 명령 사용 하 여 로그인 합니다. 클릭 하면 **실습** hello 상자 아래에 클라우드 셸 열립니다. Hello 다음 명령을 입력 하지 않고 tooyour Azure 구독에 로그인 할 수 있습니다.

    ```azurecli-interactive
    azure login
    ```

3. 서비스 관리 모드에서 CLI는 tooensure hello hello 다음 명령을 입력 합니다.

    ```azurecli-interactive
    azure config mode asm
    ```

4. 개인 서브넷을 사용하는 가상 네트워크를 만듭니다.

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. Hello 가상 네트워크 내에 있는 공용 서브넷을 만듭니다.

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. Hello 가상 네트워크 및 서브넷을 검토 합니다.

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. **선택적**: toodelete hello 리소스 사용량에 따른 요금을 발생 하지 않습니다 있도록이 자습서를 완료 하면 만든를 할 수 있습니다.

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> Azure 리소스 그룹에 hello 가상 네트워크를 만듭니다 hello CLI를 사용 하 여 리소스 그룹 toocreate 가상 네트워크 (클래식)를 지정할 수 없습니다, 있지만 *기본 네트워킹*합니다.

## <a name="powershell"></a>PowerShell

1. Hello hello PowerShell의 최신 버전을 설치 [Azure](https://www.powershellgallery.com/packages/Azure) 모듈입니다. 새 tooAzure PowerShell 인 경우 참조 [Azure PowerShell 개요](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.
2. PowerShell 세션을 시작합니다.
3. PowerShell에서 로그인 tooAzure hello를 입력 하 여 `Add-AzureAccount` 명령입니다.
4. 변경 hello 다음 경로 파일 이름을 적절 하 게는 다음 기존 네트워크 구성 파일을 내보냅니다.

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. toocreate 공용 및 개인 서브넷과 가상 네트워크를 사용 하 여 모든 텍스트 편집기 tooadd hello **VirtualNetworkSite** toohello 네트워크 구성 파일에 나타나는 요소입니다.

    ```xml
    <VirtualNetworkSite name="myVnet" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Private">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Public">
            <AddressPrefix>10.0.1.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    ```

    전체 검토 hello [네트워크 구성 파일 스키마](https://msdn.microsoft.com/library/azure/jj157100.aspx)합니다.

6. Hello 네트워크 구성 파일을 가져옵니다.

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > 변경 된 네트워크 구성 파일을 가져오는 변경 될 수 tooexisting 가상 네트워크 (클래식)를 구독 합니다. 만 hello 이전 가상 네트워크를 추가 하 고 변경 하거나 구독에서 기존 가상 네트워크를 제거 하지 확인 합니다. 

7. Hello 가상 네트워크 및 서브넷을 검토 합니다.

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. **선택적**: toodelete hello 리소스 사용량에 따른 요금을 발생 하지 않습니다 있도록이 자습서를 완료 하면 만든를 할 수 있습니다. toodelete hello 가상 네트워크를 전체 4-6 단계를 다시이 시간 제거 hello **VirtualNetworkSite** 5 단계에서 추가 된 요소입니다.
 
> [!NOTE]
> Azure 리소스 그룹에 hello 가상 네트워크를 만듭니다 PowerShell을 사용 하 여 리소스 그룹 toocreate 가상 네트워크 (클래식)를 지정할 수 없습니다, 있지만 *기본 네트워킹*합니다.

---

## <a name="next-steps"></a>다음 단계

- 모든 가상 네트워크 및 서브넷 설정 하는 방법에 대 한 toolearn 참조 [가상 네트워크를 관리](virtual-network-manage-network.md) 및 [관리 가상 네트워크 서브넷](virtual-network-manage-subnet.md)합니다. 가상 네트워크 및 서브넷을 사용 하 여 프로덕션 환경 toomeet 다른 요구에 대 한 다양 한 옵션이 있습니다.
- 인바운드 및 아웃 바운드 toofilter 서브넷 간의 트래픽은 만들기 및 적용 [네트워크 보안 그룹](virtual-networks-nsg.md) toosubnets 합니다.
- 만들기는 [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 또는 [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 가상 컴퓨터를 다음 tooan 기존 가상 네트워크 연결 합니다.
- tooconnect 두 가상 네트워크에서 동일한 Azure 위치 hello 하 만들기는 [가상 네트워크 피어 링](create-peering-different-deployment-models.md) hello 가상 네트워크 간의 합니다. 가상 네트워크 (리소스 관리자) tooa 가상 네트워크 (클래식) 피어 링 할 수 있지만 두 가상 네트워크 (클래식) 간의 피어 링을 만들 수 없습니다.
- 사용 하 여 hello 가상 네트워크 tooan 온-프레미스 네트워크에 연결 된 [VPN 게이트웨이](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 또는 [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 회로 합니다.
