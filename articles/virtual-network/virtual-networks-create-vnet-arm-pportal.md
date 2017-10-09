---
title: "Azure 가상 네트워크 서브넷이 여러 개를 aaaCreate | Microsoft Docs"
description: "자세한 내용은 방법 toocreate Azure에서 여러 서브넷을 사용 하 여 가상 네트워크입니다."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ad679a4-a959-4e48-a317-d9f5655a442b
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 0f56fa6ac24537d33b8e217f5b03f387826ab487
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-multiple-subnets"></a>여러 서브넷이 있는 가상 네트워크 만들기

이 자습서에서는 toocreate 기본 Azure 가상 네트워크를 가진 공용 및 개인 서브넷을 구분 하는 방법에 대해 알아봅니다. 가상 컴퓨터, App Service Environment, Virtual Machine Scale Sets, Azure HDInsight 및 서브넷의 클라우드 서비스와 같은 Azure 리소스를 만들 수 있습니다. 가상 네트워크의 리소스는 서로 다른 네트워크 연결 된 tooa 가상 네트워크의 리소스와 통신할 수 있습니다.

hello 다음 섹션에서는 단계를 수행할 수 있는 toocreate 가상 네트워크 hello를 사용 하 여 [Azure 포털](#portal), hello Azure 명령줄 인터페이스 ([Azure CLI](#azure-cli)), [Azure PowerShell ](#powershell), 및 [Azure 리소스 관리자 템플릿](#resource-manager-template)합니다. hello 결과 hello에 관계 없이 동일한 toocreate hello 가상 네트워크를 사용 하는 도구입니다. Hello 자습서의 도구 링크 toogo toothat 섹션을 클릭 합니다. 모든 [가상 네트워크](virtual-network-manage-network.md) 및 [서브넷](virtual-network-manage-subnet.md) 설정에 대해 자세히 확인하세요.

이 문서에서는 단계 toocreate hello 리소스 관리자 배포 모델을 사용할 수 있는 새 가상 네트워크를 만들 때 권장 하는 hello 배포 모델을 통해 가상 네트워크를 제공 합니다. 가상 네트워크 (클래식) toocreate 필요한 경우 참조 [가상 네트워크 (클래식)를 만들고](create-virtual-network-classic.md)합니다. Azure 배포 모델에 대해 잘 모르는 경우에는 [Azure 배포 모델 이해](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)을 참조하세요.

## <a name="portal"></a>Azure Portal

1. 인터넷 브라우저를 이동 toohello [Azure 포털](https://portal.azure.com)합니다. [Azure 계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)을 사용하여 로그인합니다. Azure 계정이 없으면 [무료 평가판](https://azure.microsoft.com/offers/ms-azr-0044p)에 등록할 수 있습니다.
2. Hello 포털에서 클릭 **+ 새로 만들기** > **네트워킹** > **가상 네트워크**합니다.
3. Hello에 **가상 네트워크 만들기** 블레이드에서 hello 다음 값을 입력 하 고 클릭 **만들기**:

    |설정|값|
    |---|---|
    |이름|myVnet|
    |주소 공간|10.0.0.0/16|
    |서브넷 이름|공용|
    |서브넷 주소 범위|10.0.0.0/24|
    |리소스 그룹|**새로 만들기**를 선택한 채로 두고 **myResourceGroup**을 입력합니다.|
    |구독 및 위치|구독 및 위치를 선택합니다.

    새 tooAzure 인 경우에 대해 자세히 알아보세요 [리소스 그룹](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [구독](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), 및 [위치](https://azure.microsoft.com/regions) (tooas 라고도 *영역*).
4. Hello 포털에서 가상 네트워크를 만들 때 서브넷이 하나만 만들 수 있습니다. 이 자습서에서는 hello 가상 네트워크를 만든 후 두 번째 서브넷을 만듭니다. 인터넷에서 액세스할 수 있는 리소스 hello 나중에 만들 수 있습니다 **공용** 서브넷입니다. 또한 hello에 hello 인터넷에서에서 액세스할 수 없는 리소스를 만들 수 있습니다 **개인** 서브넷입니다. hello에 toocreate hello 두 번째 서브넷에 **리소스 검색** hello hello 페이지 위쪽에 상자에 입력 **myVnet**합니다. Hello 검색 결과에서 클릭 **myVnet**합니다. 가상 네트워크가 여러 구독에서 이름이 같은 hello, 각 가상 네트워크에 나열 된 hello 리소스 그룹을 확인 있는 경우 합니다. Hello를 클릭 하면 확인 **myVnet** 검색 hello 리소스 그룹이 들어 있는 결과 **myResourceGroup**합니다.
5. Hello에 **myVnet** 블레이드 아래 **설정**, 클릭 **서브넷**합니다.
6. Hello에 **myVnet-서브넷** 블레이드에서 클릭 **+ 서브넷**합니다.
7. Hello에 **서브넷 추가** 블레이드에서 대 한 **이름**, 입력 **개인**합니다. **주소 범위**에 **10.0.1.0/24**를 입력합니다.  **확인**을 클릭합니다.
8. Hello에 **myVnet-서브넷** 블레이드, 검토 hello 서브넷입니다. Hello를 볼 수 있습니다 **공용** 및 **개인** 만든 서브넷입니다.
9. **선택 사항:** 이 자습서에서 만드는 toodelete hello 리소스의 단계를 완료 hello [리소스를 삭제](#delete-portal) 이 문서의 내용입니다.

## <a name="azure-cli"></a>Azure CLI

Azure CLI 명령을 경우 동일 hello Windows, Linux 또는 macOS에서 hello 명령을 실행 하는지 여부 그러나 운영 체제 셸 간에 스크립팅 차이는 있습니다. Bash 셸의 단계를 수행 하는 hello에 hello 스크립트를 실행 합니다. 

1. [설치 및 구성 hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다. Hello 최신 버전의 hello Azure CLI 설치 되어 있는지 확인 합니다. CLI 명령에 대 한 도움말 tooget 입력 `az <command> --help`합니다. 설치 hello CLI 및 해당 필수 구성 요소는 대신 Azure 클라우드 셸 hello를 사용할 수 있습니다. Azure 클라우드 셸 hello hello Azure 포털 내에서 직접 실행할 수 있는 무료 Bash 셸의입니다. 클라우드 셸 hello에 hello Azure CLI 사전 설치 및 toouse 계정으로 구성 되어 있습니다. toouse hello 클라우드 셸 hello 클라우드 셸 클릭 (**> _**) hello hello 위쪽에 단추 [포털](https://portal.azure.com) hello 클릭 또는 *실습* 수행 하는 hello 단계에서 단추입니다. 
2. Hello로 tooAzure hello CLI를 로컬로 실행 하는 경우 로그인 `az login` 명령입니다. 클라우드 셸 hello를 사용 하는 경우 이미 로그인 합니다.
3. 검토 hello 다음 스크립트와 해당 설명 합니다. 브라우저에서 hello 스크립트 복사한 CLI 세션에 붙여 넣습니다.

    ```azurecli-interactive
    #!/bin/bash
    
    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus
    
    # Create a virtual network with one subnet named Public.
    az network vnet create \
      --name myVnet \
      --resource-group myResourceGroup \
      --subnet-name Public
    
    # Create an additional subnet named Private in hello virtual network.
    az network vnet subnet create \
      --name Private \
      --address-prefix 10.0.1.0/24 \
      --vnet-name myVnet \
      --resource-group myResourceGroup
    ```
    
4. Hello 스크립트가 완료 되 면 hello 가상 네트워크에 대 한 hello 서브넷 검토를 실행 합니다. 다음 명령을, hello 복사한 CLI 세션에 붙여 넣습니다.

    ```azurecli
    az network vnet subnet list --resource-group myResourceGroup --vnet-name myVnet --output table
    ```

5. **선택적**:이 자습서에서 만드는 toodelete hello 리소스의 단계를 완료 hello [리소스를 삭제](#delete-cli) 이 문서의 내용입니다.

## <a name="powershell"></a>PowerShell

1. Hello hello PowerShell의 최신 버전을 설치 [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 모듈입니다. 새 tooAzure PowerShell 인 경우 참조 [Azure PowerShell 개요](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.
2. 와 tooAzure PowerShell 세션에서 로그인 하면 [Azure 계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) hello를 사용 하 여 `login-azurermaccount` 명령입니다.

3. 검토 hello 다음 스크립트와 해당 설명 합니다. 브라우저에서 hello 스크립트를 복사 하 여 PowerShell 세션에 붙여 넣습니다.

    ```powershell
    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name myResourceGroup `
      -Location eastus
    
    # Create hello public and private subnets.
    $Subnet1 = New-AzureRmVirtualNetworkSubnetConfig `
      -Name Public `
      -AddressPrefix 10.0.0.0/24
    $Subnet2 = New-AzureRmVirtualNetworkSubnetConfig `
      -Name Private `
      -AddressPrefix 10.0.1.0/24
    
    # Create a virtual network.
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Location eastus `
      -Name myVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet1,$Subnet2
    ```

4. hello 가상 네트워크에 대 한 tooreview hello 서브넷 다음 명령을, hello를 복사 하 여 PowerShell 세션에 붙여 넣습니다.

    ```powershell
    $Vnet.subnets | Format-Table Name, AddressPrefix
    ```

5. **선택적**:이 자습서에서 만드는 toodelete hello 리소스의 단계를 완료 hello [리소스를 삭제](#delete-powershell) 이 문서의 내용입니다.

## <a name="resource-manager-template"></a>Resource Manager 템플릿

Azure Resource Manager 템플릿을 사용하여 가상 네트워크를 배포할 수 있습니다. 서식 파일에 대해 자세히 toolearn 참조 [리소스 관리자란](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#template-deployment)합니다. tooaccess hello 템플릿 및 해당 매개 변수에 대 한 toolearn 참조 hello [두 서브넷과 가상 네트워크 만들기](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) 템플릿. Hello를 사용 하 여 hello 서식 파일을 배포할 수 있습니다 [포털](#template-portal), [Azure CLI](#template-cli), 또는 [PowerShell](#template-powershell)합니다.

**선택 사항:** 이 자습서에서 만드는 toodelete hello 리소스의 모든 하위 섹션에서 단계를 완료 hello [리소스를 삭제](#delete) 이 문서의 내용입니다.

### <a name="template-portal"></a>Azure Portal

1. 브라우저를 열고 hello [템플릿 페이지](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets)합니다.
2. Hello 클릭 **tooAzure 배포** 단추입니다. 표시 된 hello Azure 포털 로그인 화면에 tooAzure에 로그인 되어 있지 하는 경우에 로그인 합니다.
3. 사용 하 여 toohello 포털에 로그인 하면 [Azure 계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)합니다. Azure 계정이 없으면 [무료 평가판](https://azure.microsoft.com/offers/ms-azr-0044p)에 등록할 수 있습니다.
4. Hello 다음 hello 매개 변수에 대 한 값을 입력 합니다.

    |매개 변수|값|
    |---|---|
    |구독|구독 선택|
    |리소스 그룹|myResourceGroup|
    |위치|위치 선택|
    |VNet 이름|myVnet|
    |VNet 주소 접두사|10.0.0.0/16|
    |Subnet1Prefix|10.0.0.0/24|
    |Subnet1Name|공용|
    |Subnet2Prefix|10.0.1.0/24|
    |Subnet2Name|개인|

5. Toohello 사용 약관을 동의 하 고 클릭 **구매** toodeploy hello 가상 네트워크입니다.

### <a name="template-cli"></a>Azure CLI

1. [설치 및 구성 hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다. Hello 최신 버전의 hello Azure CLI 설치 되어 있는지 확인 합니다. CLI 명령에 대 한 도움말 tooget 입력 `az <command> --help`합니다. 설치 hello CLI 및 해당 필수 구성 요소는 대신 Azure 클라우드 셸 hello를 사용할 수 있습니다. Azure 클라우드 셸 hello hello Azure 포털 내에서 직접 실행할 수 있는 무료 Bash 셸의입니다. 클라우드 셸 hello에 hello Azure CLI 사전 설치 및 toouse 계정으로 구성 되어 있습니다. toouse hello 클라우드 셸 클릭 hello 클라우드 셸 **> _** hello hello 위쪽에 단추 [포털](https://portal.azure.com), 또는 hello 클릭할 **실습** 수행 하는 hello 단계에서 단추입니다. 
2. Hello로 tooAzure hello CLI를 로컬로 실행 하는 경우 로그인 `az login` 명령입니다. 클라우드 셸 hello를 사용 하는 경우 이미 로그인 합니다.
3. toocreate hello 가상 네트워크에 대 한 리소스 그룹 복사 hello 다음 명령 및 CLI 세션에 붙여 넣습니다.

    ```azurecli-interactive
    az group create --name myResourceGroup --location eastus
    ```
    
4. Hello 다음 매개 변수 옵션 중 하나를 사용 하 여 hello 서식 파일을 배포할 수 있습니다.
    - **기본 매개 변수 값**. Hello 다음 명령을 입력 합니다.
    
        ```azurecli-interactive
        az group deployment create --resource-group myResourceGroup --name VnetTutorial --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json`
        ```
    - **사용자 지정 매개 변수 값**. 다운로드 하 고 hello 서식 파일을 배포 하기 전에 hello 서식 파일을 수정 합니다. 또한 수 hello 명령줄에서 매개 변수를 사용 하 여 hello 서식 파일을 배포 또는 별도 매개 변수 파일이 있는 hello 서식 파일을 배포 합니다. toodownload hello 템플릿 및 매개 변수 파일을 클릭 하 여 hello **GitHub에서 찾아보기** hello 단추 [두 서브넷과 가상 네트워크 만들기](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) 템플릿 페이지. GitHub에서 클릭 hello **azuredeploy.parameters.json** 또는 **azuredeploy.json** 파일입니다. 클릭 hello **Raw** 단추 toodisplay hello 파일입니다. 브라우저에서 hello 내용 hello 파일을 복사 합니다. Hello 내용을 tooa 파일을 컴퓨터에 저장 합니다. Hello 템플릿의 hello 매개 변수 값을 수정 하거나 별도 매개 변수 파일을 사용 하 여 hello 서식 파일을 배포할 수 있습니다.  

    이러한 메서드를 사용 하 여 toodeploy 템플릿 입력 하는 방법에 대해 더 알아봅니다을 toolearn `az group deployment create --help`합니다.

### <a name="template-powershell"></a>PowerShell

1. Hello hello PowerShell의 최신 버전을 설치 [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 모듈입니다. 새 tooAzure PowerShell 인 경우 참조 [Azure PowerShell 개요](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.
2. PowerShell 세션에서 사용 하 여 toosign 프로그램 [Azure 계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account), 입력 `login-azurermaccount`합니다.
3. hello 가상 네트워크에 대 한 리소스 그룹 toocreate hello 다음 명령을 입력 합니다.

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
    ```
    
4. Hello 다음 매개 변수 옵션 중 하나를 사용 하 여 hello 서식 파일을 배포할 수 있습니다.
    - **기본 매개 변수 값**. Hello 다음 명령을 입력 합니다.
    
        ```powershell
        New-AzureRmResourceGroupDeployment -Name VnetTutorial -ResourceGroupName myResourceGroup -TemplateUri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json
        ```
        
    - **사용자 지정 매개 변수 값**. 다운로드 하 고 배포 하기 전에 hello 서식 파일을 수정 합니다. 또한 수 hello 명령줄에서 매개 변수를 사용 하 여 hello 서식 파일을 배포 또는 별도 매개 변수 파일이 있는 hello 서식 파일을 배포 합니다. toodownload hello 템플릿 및 매개 변수 파일을 클릭 하 여 hello **GitHub에서 찾아보기** hello 단추 [두 서브넷과 가상 네트워크 만들기](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) 템플릿 페이지. GitHub에서 클릭 hello **azuredeploy.parameters.json** 또는 **azuredeploy.json** 파일입니다. 클릭 hello **Raw** 단추 toodisplay hello 파일입니다. 브라우저에서 hello 내용 hello 파일을 복사 합니다. Hello 내용을 tooa 파일을 컴퓨터에 저장 합니다. Hello 템플릿의 hello 매개 변수 값을 수정 하거나 별도 매개 변수 파일을 사용 하 여 hello 서식 파일을 배포할 수 있습니다.  

    이러한 메서드를 사용 하 여 toodeploy 템플릿 입력 하는 방법에 대해 더 알아봅니다을 toolearn `Get-Help New-AzureRmResourceGroupDeployment`합니다. 

## <a name="delete"></a>리소스 삭제

이 자습서를 완료 하면 사용 요금을 발생 하지 않습니다 수 있도록 사용자가 만든 toodelete hello 리소스를 할 수 있습니다. 리소스 그룹을 삭제 하면 hello 리소스 그룹에는 모든 리소스를 삭제 합니다.

### <a name="delete-portal"></a>Azure Portal

1. Hello 포털 검색 상자에 입력 **myResourceGroup**합니다. Hello 검색 결과에서 클릭 **myResourceGroup**합니다.
2. Hello에 **myResourceGroup** 블레이드에서 hello 클릭 **삭제** 아이콘입니다.
3. hello에 tooconfirm hello 삭제 **형식 hello 리소스 그룹 이름은** 상자에 입력 **myResourceGroup**, 클릭 하 고 **삭제**합니다.

### <a name="delete-cli"></a>Azure CLI

CLI 세션 hello 다음 명령을 입력 합니다.

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <a name="delete-powershell"></a>PowerShell

PowerShell 세션에서 다음 명령을 hello를 입력 합니다.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="next-steps"></a>다음 단계

- 모든 가상 네트워크 및 서브넷 설정 하는 방법에 대 한 toolearn 참조 [가상 네트워크를 관리](virtual-network-manage-network.md#view-vnet) 및 [관리 가상 네트워크 서브넷](virtual-network-manage-subnet.md#create-subnet)합니다. 가상 네트워크 및 서브넷을 사용 하 여 프로덕션 환경 toomeet 다른 요구에 대 한 다양 한 옵션이 있습니다.
- 인바운드 및 아웃 바운드 toofilter 서브넷 간의 트래픽은 만들기 및 적용 [네트워크 보안 그룹](virtual-networks-nsg.md) toosubnets 합니다.
- 만들기는 [Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 또는 [Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 가상 컴퓨터를 다음 tooan 기존 가상 네트워크 연결 합니다.
- tooconnect 두 가상 네트워크에서 동일한 Azure 위치 hello 하 만들기는 [가상 네트워크 피어 링](virtual-network-peering-overview.md) hello 가상 네트워크 간의 합니다.
- 사용 하 여 hello 가상 네트워크 tooan 온-프레미스 네트워크에 연결 된 [VPN 게이트웨이](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 또는 [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 회로 합니다.
