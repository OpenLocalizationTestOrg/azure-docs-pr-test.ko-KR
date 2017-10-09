---
title: "고정 공용 IP 주소-Azure 리소스 관리자 템플릿 사용 하 여 VM aaaCreate | Microsoft Docs"
description: "Azure 리소스 관리자 템플릿을 사용 하 여 toocreate 고정 공용 IP 사용 하 여 VM을 해결 하는 방법을 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d551085a-c7ed-4ec6-b4c3-e9e1cebb774c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6a8640ed4fad06b0e09820e6114fd6789db73847
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-an-azure-resource-manager-template"></a>Azure Resource Manager 템플릿을 사용하여 고정 공용 IP 주소를 사용하는 VM 만들기

> [!div class="op_single_selector"]
> * [Azure Portal](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Azure CLI](virtual-network-deploy-static-pip-arm-cli.md)
> * [템플릿](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell(클래식)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다. 이 문서에서는 Microsoft hello 클래식 배포 모델 대신 대부분의 새 배포에 권장 하는 hello 리소스 관리자 배포 모델을 사용 하 여 설명 합니다.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="public-ip-address-resources-in-a-template-file"></a>템플릿 파일의 공용 IP 주소 리소스
보고 하 고 hello 다운로드 [샘플 템플릿](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json)합니다.

hello 다음 단원에서는 hello 공용 IP 리소스에 위의 hello 시나리오에 따라의 hello 정의:

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('webVMSetting').pipName]",
  "location": "[variables('location')]",
  "properties": {
    "publicIPAllocationMethod": "Static"
  },
  "tags": {
    "displayName": "PublicIPAddress - Web"
  }
},
```

공지 hello **publicIPAllocationMethod** 너무 설정 된 속성*정적*합니다. 이 속성은 *동적*(기본값) 또는 *고정*이 될 수 있습니다. 할당 hello 공용 IP 주소가 변경 되지 않을 것임 toostatic 보장 설정 합니다.

hello 다음 단원에서는 hello 공용 IP 주소는 네트워크 인터페이스와 hello 연결:

```json
  {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('webVMSetting').nicName]",
    "location": "[variables('location')]",
    "tags": {
    "displayName": "NetworkInterface - Web"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/publicIPAddresses/', variables('webVMSetting').pipName)]",
      "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
    ],
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
          "privateIPAllocationMethod": "Static",
          "privateIPAddress": "[variables('webVMSetting').ipAddress]",
          "publicIPAddress": {
          "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('webVMSetting').pipName)]"
          },
          "subnet": {
            "id": "[variables('frontEndSubnetRef')]"
          }
        }
      }
    ]
  }
},
```

공지 hello **publicIPAddress** toohello 가리키는 속성 **Id** 명명 된 리소스의 **variables('webVMSetting').pipName**합니다. 위에 표시 된 hello 공용 IP 리소스의 hello 이름입니다.

위의 hello 네트워크 인터페이스 hello에 나열 된 마지막으로, **networkProfile** hello 만들려는 VM의 속성입니다.

```json
      "networkProfile": {
        "networkInterfaces": [
          {
            "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('webVMSetting').nicName)]"
          }
        ]
      }
```

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>Hello 템플릿을 사용 하 여 배포 toodeploy 클릭

hello 공용 저장소에서 사용할 수 있는 hello 샘플 템플릿 hello 기본 사용 되는 값 toogenerate hello 위에서 언급 한 시나리오를 포함 하는 매개 변수 파일을 사용 합니다. toodeploy toodeploy를 클릭 하 여 사용 하 여이 템플릿을 클릭 **tooAzure 배포** hello에 대 한 hello Readme.md 파일에 [정적 PIP 사용 하 여 VM](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) 템플릿. 원하는 경우 hello 기본 매개 변수 값을 대체 하 고 hello 빈 매개 변수에 대 한 값을 입력 합니다.  Hello 포털 toocreate 고정 공용 IP 주소를 사용 하는 가상 컴퓨터의에서 hello 지침을 따릅니다.

## <a name="deploy-hello-template-by-using-powershell"></a>PowerShell을 사용 하 여 hello 서식 파일을 배포 합니다.

PowerShell을 사용 하 여 다운로드 한 toodeploy hello 템플릿을 다음 hello 단계를 따릅니다.

1. Azure PowerShell을 처음 사용 하는 경우 전체 hello hello의 단계를 [어떻게 tooInstall 및 Azure PowerShell 구성](/powershell/azure/overview) 문서.
2. PowerShell 콘솔에서 실행 hello `New-AzureRmResourceGroup` cmdlet toocreate 필요한 경우 새 리소스 그룹입니다. 만든 리소스 그룹을 이미 있는 경우에 3 toostep을 이동 합니다.

    ```powershell
    New-AzureRmResourceGroup -Name PIPTEST -Location westus
    ```

    예상 출력:
   
        ResourceGroupName : PIPTEST
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/StaticPublicIP

3. PowerShell 콘솔에서 실행 hello `New-AzureRmResourceGroupDeployment` cmdlet toodeploy hello 템플릿.

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployVM -ResourceGroupName PIPTEST `
        -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json
    ```

    예상 출력:
   
        DeploymentName    : DeployVM
        ResourceGroupName : PIPTEST
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
                            Uri            : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/mas
                            ter/IaaS-Story/03-Static-public-IP/azuredeploy.json
                            ContentVersion : 1.0.0.0
   
        Parameters        :
                            Name                      Type                       Value     
                            ========================  =========================  ==========
                            vnetName                  String                     WTestVNet
                            vnetPrefix                String                     192.168.0.0/16
                            frontEndSubnetName        String                     FrontEnd  
                            frontEndSubnetPrefix      String                     192.168.1.0/24
                            storageAccountNamePrefix  String                     iaasestd  
                            stdStorageType            String                     Standard_LRS
                            osType                    String                     Windows   
                            adminUsername             String                     adminUser
                            adminPassword             SecureString                         
   
        Outputs           :

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Hello Azure CLI를 사용 하 여 hello 서식 파일을 배포 합니다.
toodeploy hello Azure CLI, 단계를 수행 하는 전체 hello 사용 하 여 서식 파일을 hello:

1. Azure CLI 처음 사용 하는 경우에서 다음과 같이 hello hello [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md) tooinstall 문서를 구성 합니다.
2. Hello 실행 `azure config mode` 명령 tooswitch tooResource 관리자 모드에서는 다음과 같이 합니다.

    ```azurecli
    azure config mode arm
    ```

    hello 예상 위의 hello 명령에 대 한 출력:

        info:    New mode is arm

3. 열기 hello [매개 변수 파일](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), 해당 콘텐츠를 선택 하 고 컴퓨터에 tooa 파일을 저장 합니다. 예를 들어 hello 매개 변수가 라는 tooa 파일이 저장 되 *parameters.json*합니다. Hello 매개 변수 값을 원하는 경우 hello 파일 내에서 변경 있지만 여기에 최소한 것이 좋습니다 hello hello는 adminPassword 매개 변수 tooa 고유, 복잡 한 암호 값을 변경 합니다.
4. Hello 실행 `azure group deployment create` cmd toodeploy hello hello 템플릿 및 매개 변수를 사용 하 여 새 VNet이 파일 다운로드 하 고 위에서 수정 합니다. Hello 명령 아래에서 <path> hello 경로로 hello 파일을 저장 합니다. 

    ```azurecli
    azure group create -n PIPTEST2 -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json -e <path>\parameters.json
    ```

    예상 출력(사용한 매개 변수 값 나열):

        info:    Executing command group create
        + Getting resource group PIPTEST2
        + Creating resource group PIPTEST2
        info:    Created resource group PIPTEST2
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/PIPTEST2
        data:    Name:                PIPTEST2
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

