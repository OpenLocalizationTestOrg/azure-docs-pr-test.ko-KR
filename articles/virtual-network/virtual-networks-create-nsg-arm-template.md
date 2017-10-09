---
title: "aaaCreate 네트워크 보안 그룹-Azure 리소스 관리자 템플릿을 | Microsoft Docs"
description: "자세한 내용은 방법 toocreate 및 Azure 리소스 관리자 템플릿을 사용 하 여 네트워크 보안 그룹을 배포 합니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: f3e7385d-717c-44ff-be20-f9aa450aa99b
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3750168284fea7b41c8c0f908b0d31a9da5e38ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-an-azure-resource-manager-template"></a>Azure Resource Manager 템플릿을 사용하여 네트워크 보안 그룹 만들기

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

이 문서에서는 hello 리소스 관리자 배포 모델에 설명 합니다. 수도 있습니다 [hello 클래식 배포 모델에서 Nsg를 만들](virtual-networks-create-nsg-classic-ps.md)합니다.

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

## <a name="nsg-resources-in-a-template-file"></a>템플릿 파일의 NSG 리소스
보고 하 고 hello 다운로드 [샘플 템플릿](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json)합니다.

hello 다음 단원에서는 hello의 hello 정의 hello 시나리오에 따라 프런트 엔드 NSG를 합니다.

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Network/networkSecurityGroups",
"name": "[parameters('frontEndNSGName')]",
"location": "[resourceGroup().location]",
"tags": {
  "displayName": "NSG - Front End"
},
"properties": {
  "securityRules": [
    {
      "name": "rdp-rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 100,
        "direction": "Inbound"
      }
    },
    {
      "name": "web-rule",
      "properties": {
        "description": "Allow WEB",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 101,
        "direction": "Inbound"
      }
    }
  ]
}
```
tooassociate hello NSG toohello 프런트 엔드 서브넷에 hello 템플릿과 NSG hello에 대 한 hello 참조 id가 사용 하 여 toochange hello 서브넷 정의 해야합니다.

```json
"subnets": [
  {
    "name": "[parameters('frontEndSubnetName')]",
    "properties": {
      "addressPrefix": "[parameters('frontEndSubnetPrefix')]",
      "networkSecurityGroup": {
      "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('frontEndNSGName'))]"
      }
    }
  }, 
```

Hello 템플릿에서 hello 백 엔드 NSG와 hello 백 엔드 서브넷에 대해 수행 되 고 동일한 hello를 확인 합니다.

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a>Hello ARM 템플릿을 사용 하 여 배포 toodeploy 클릭
hello 공용 저장소에서 사용할 수 있는 hello 샘플 템플릿 hello 기본 사용 되는 값 toogenerate hello 위에서 언급 한 시나리오를 포함 하는 매개 변수 파일을 사용 합니다. toodeploy toodeploy, 클릭 하 여 사용 하 여이 서식 파일에 따라 [이 링크](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), 클릭 **tooAzure 배포**hello 기본 매개 변수 값, 필요한 경우 바꾼 hello 포털의 hello 지침을 따릅니다.

## <a name="deploy-hello-arm-template-by-using-powershell"></a>PowerShell을 사용 하 여 hello ARM 템플릿을 배포합니다
PowerShell을 사용 하 여 다운로드 한 toodeploy hello ARM 템플릿을 다음 hello 단계를 따릅니다.

1. Hello에 hello 지침에 따라 Azure PowerShell을 처음 사용 하는 경우 [어떻게 tooInstall 및 Azure PowerShell 구성](/powershell/azure/overview) tooinstall 하 고 구성 합니다.
2. Hello 실행  **`New-AzureRmResourceGroup`**  사용 하 여 리소스 그룹 cmdlet toocreate hello 템플릿.

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location uswest `
    -TemplateFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' `
    -TemplateParameterFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    예상 출력:

        ResourceGroupName : TestRG
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *                  
   
        Resources         :
                            Name                Type                                     Location
                            ==================  =======================================  ========
                            sqlAvSet            Microsoft.Compute/availabilitySets       westus  
                            webAvSet            Microsoft.Compute/availabilitySets       westus  
                            SQL1                Microsoft.Compute/virtualMachines        westus  
                            SQL2                Microsoft.Compute/virtualMachines        westus  
                            Web1                Microsoft.Compute/virtualMachines        westus  
                            Web2                Microsoft.Compute/virtualMachines        westus  
                            TestNICSQL1         Microsoft.Network/networkInterfaces      westus  
                            TestNICSQL2         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb1         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb2         Microsoft.Network/networkInterfaces      westus  
                            NSG-BackEnd         Microsoft.Network/networkSecurityGroups  westus  
                            NSG-FrontEnd        Microsoft.Network/networkSecurityGroups  westus  
                            TestPIPSQL1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPSQL2         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb2         Microsoft.Network/publicIPAddresses      westus  
                            TestVNet            Microsoft.Network/virtualNetworks        westus  
                            testvnetstorageprm  Microsoft.Storage/storageAccounts        westus  
                            testvnetstoragestd  Microsoft.Storage/storageAccounts        westus  
   
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG

## <a name="deploy-hello-arm-template-by-using-hello-azure-cli"></a>Hello Azure CLI를 사용 하 여 hello ARM 템플릿을 배포합니다
hello Azure CLI를 사용 하 여 toodeploy hello ARM 템플릿을 다음 hello 단계를 따릅니다.

1. Azure CLI 처음 사용 하는 경우 참조 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md) Azure 계정 및 구독을 선택 하면 toohello 포인트 hello 지침을 따릅니다.
2. Hello 실행  **`azure config mode`**  명령 tooswitch tooResource 관리자 모드에서는 다음과 같이 합니다.

    ```azurecli
    azure config mode arm
    ```

    hello 다음 hello 명령에 대 한 hello 예상 출력은입니다.

        info:    New mode is arm

3. Hello 실행  **`azure group deployment create`**  cmdlet toodeploy hello hello 템플릿 및 매개 변수를 사용 하 여 새 VNet이 파일 다운로드 하 고 위에서 수정 합니다. hello 출력 뒤에 표시 된 hello 목록 사용 되는 hello 매개 변수를 설명 합니다.

    ```azurecli
    azure group create -n TestRG -l westus -f 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' -e 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    예상 출력:
   
        info:    Executing command group create
        info:    Getting resource group TestRG
        info:    Creating resource group TestRG
        info:    Created resource group TestRG
        info:    Initializing template configurations and parameters
        info:    Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG
        data:    Name:                TestRG
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:    
        info:    group create command OK
   
   * **-n (or --name)**. 만든 hello 리소스 그룹 toobe의 이름입니다.
   * **-l(또는 --location)**. Azure 지역 hello 리소스 그룹이 만들어집니다.
   * **-f (or --template-file)**. Tooyour ARM 템플릿 파일 경로입니다.
   * **-e(또는 --parameters-file)**. Tooyour ARM 매개 변수 파일 경로입니다.

