---
title: "여러 Nic-Azure 리소스 관리자 템플릿 사용 하 여 VM aaaCreate | Microsoft Docs"
description: "Azure Resource Manager 템플릿을 사용하여 다중 NIC이 있는 개인 VM을 만듭니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 486f7dd5-cf2f-434c-85d1-b3e85c427def
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5d9ffcbd40c72dc18ae6de38e739eb5e45bf669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-a-template"></a>템플릿을 사용하여 다중 NIC이 있는 VM 만들기
[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.  사용 하 여이 문서에서는 Microsoft hello 대신 대부분의 새 배포에 권장 하는 hello 리소스 관리자 배포 모델 [클래식 배포 모델](virtual-network-deploy-multinic-classic-ps.md)합니다.
> 

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

hello 다음 단계 사용 하 여 명명 된 리소스 그룹 *IaaSStory* hello 웹 서버 및 리소스 그룹에 대 한 명명 된 *IaaSStory 백 엔드* hello DB 서버에 대 한 합니다.

## <a name="prerequisites"></a>필수 조건
Hello DB 서버를 만들려면 먼저 toocreate hello *IaaSStory* 이 시나리오에 대 한 모든 hello 필요한 리소스의 리소스 그룹입니다. 이러한 리소스를 완료 하는 toocreate hello 다음 단계:

1. 너무 이동[hello 템플릿 페이지](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC)합니다.
2. Hello 템플릿 페이지의 오른쪽 toohello **부모 리소스 그룹**, 클릭 **tooAzure 배포**합니다.
3. 필요한 경우 hello 매개 변수 값을를 변경한 다음 hello Azure preview 포털 toodeploy hello 리소스 그룹의 hello 단계를 수행 합니다.

> [!IMPORTANT]
> 저장소 계정 이름이 고유한지 확인합니다. Azure에서 중복된 저장소 계정 이름을 사용할 수 없습니다.
> 

## <a name="understand-hello-deployment-template"></a>Hello 배포 서식 파일 이해
이 설명서와 함께 제공 되는 hello 서식 파일을 배포 하기 전에 역할 알고 있어야 합니다. 단계를 수행 하는 hello hello 템플릿에 대 한 개요를 제공 합니다.

1. 너무 이동[hello 템플릿 페이지](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC)합니다.
2. 클릭 **azuredeploy.json** tooopen hello 템플릿 파일입니다.
3. 공지 hello *osType* 아래에 나열 된 매개 변수입니다. 이 매개 변수는 사용 되는 tooselect 어떤 VM 이미지 toouse 여러 운영 체제와 함께 hello 데이터베이스 서버에 대 한 관련 설정을 지정 합니다.

    ```json
    "osType": {
      "type": "string",
      "defaultValue": "Windows",
      "allowedValues": [
        "Windows",
        "Ubuntu"
      ],
      "metadata": {
      "description": "Type of OS toouse for VMs: Windows or Ubuntu."
      }
    },
    ```

4. 변수 toohello 목록 아래로 스크롤하여 hello에 대 한 hello 정의 확인 **dbVMSetting** 아래에 나열 된 변수입니다. Hello에 포함 된 hello 배열 요소 중 하나를 수신한 **dbVMSettings** 변수입니다. 소프트웨어 개발 용어에 익숙한 경우에 hello을 볼 수 있습니다 **dbVMSettings** 변수 해시 테이블을 사용 하거나 사전으로 합니다.

    ```json
    "dbVMSetting": "[variables('dbVMSettings')[parameters('osType')]]"
    ```

5. Hello 백 엔드에 SQL을 실행 하는 Windows Vm toodeploy 결정 했다고 가정 하겠습니다. 다음에 대 한 값을 hello **osType** 것 *Windows*, 및 hello **dbVMSetting** 변수는 hello hello의 첫 번째 값을 나타내는 hello 요소 아래에 나열 된 포함 **dbVMSettings** 변수입니다.

    ```json
    "Windows": {
      "vmSize": "Standard_DS3",
      "publisher": "MicrosoftSQLServer",
      "offer": "SQL2014SP1-WS2012R2",
      "sku": "Standard",
      "version": "latest",
      "vmName": "DB",
      "osdisk": "osdiskdb",
      "datadisk": "datadiskdb",
      "nicName": "NICDB",
      "ipAddress": "192.168.2.",
      "extensionDeployment": "",
      "avsetName": "ASDB",
      "remotePort": 3389,
      "dbPort": 1433
    },
    ```

6. 공지 hello **vmSize** hello 값이 포함 된 *Standard_DS3*합니다. 여러 Nic의 hello 사용에 대 한 특정 VM 크기에만 허용합니다. VM 크기는 hello를 참조 하 여 여러 Nic를 지 원하는 것을 확인할 수 있습니다 [Windows VM 크기](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 및 [Linux VM 크기](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 문서입니다.

7. 너무 아래로 스크롤하여**리소스** 및 통지 hello 첫 번째 요소입니다. 여기에는 저장소 계정이 설명되어 있습니다. 이 저장소 계정에 사용 되는 toomaintain hello 데이터 디스크를 VM 각 데이터베이스에서 사용 됩니다. 이 시나리오의 각 데이터베이스 VM에는 일반 저장소에 OS 디스크가 있고 SSD(프리미엄) 저장소에 두 개의 데이터 디스크가 저장되어 있습니다.

    ```json
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[parameters('prmStorageName')]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "Storage Account - Premium"
      },
      "properties": {
      "accountType": "[parameters('prmStorageType')]"
      }
    },
    ```

8. 아래와 같이 toohello 다음 리소스를 아래로 스크롤하십시오. 이 리소스는 NIC VM 각 데이터베이스에서 데이터베이스 액세스에 사용 되는 hello를 나타냅니다. 공지 hello 사용 hello **복사** 이 리소스의 함수입니다. hello 템플릿을 사용 하 여 toodeploy로 hello에 따라 원하는 만큼 많은 Vm **dbCount** 매개 변수입니다. 따라서 toocreate 해야 각 VM에 대 한 데이터베이스 액세스를 위한 Nic 같은 양의 hello 합니다.

    ```json
    {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[concat(variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
    "location": "[variables('location')]",
    "tags": {
      "displayName": "NetworkInterfaces - DB DA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "privateIPAllocationMethod": "Static",
            "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(4))]",
            "subnet": {
              "id": "[variables('backEndSubnetRef')]"
            }
          }
         }
       ] 
     }
    },
    ```

9. 아래와 같이 toohello 다음 리소스를 아래로 스크롤하십시오. 이 리소스는 NIC VM 각 데이터베이스 관리에 사용 되는 hello를 나타냅니다. 각 데이터베이스 VM에 대해 이 NIC 중 하나가 필요합니다. 공지 hello **networkSecurityGroup** 요소를 액세스 tooRDP/SSH toothis NIC만 허용 된 NSG를 연결 합니다.

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[concat(variables('dbVMSetting').nicName, '-RA-',copyindex(1))]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "NetworkInterfaces - DB RA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "networkSecurityGroup": {
             "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('remoteAccessNSGName'))]"
             },
             "privateIPAllocationMethod": "Static",
             "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(54))]",
             "subnet": {
              "id": "[variables('backEndSubnetRef')]"
             }
           }
          }
        ]
      }
    },
```

10. 아래와 같이 toohello 다음 리소스를 아래로 스크롤하십시오. 이 리소스는 모든 데이터베이스 Vm에서 공유 하는 가용성 집합 toobe를 나타냅니다. 이런 방식으로 항상 것 하나의 VM에 유지 관리 하는 동안 실행을 설정 하는 hello 보장 합니다.

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/availabilitySets",
      "name": "[variables('dbVMSetting').avsetName]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "AvailabilitySet - DB"
      }
    },
    ```

11. 다음 리소스에 toohello 아래로 스크롤하십시오. 이 리소스와 같이 hello 처음 몇 줄 아래에 나열 된 hello 데이터베이스를 Vm을 나타냅니다. 공지 hello 사용 hello **복사** 다시 함수, hello에 따라 여러 Vm 만들어졌는지 확인 **dbCount** 매개 변수입니다. 또한 hello 확인 **dependsOn** 컬렉션입니다. Hello hello 가용성 집합 및 hello 저장소 계정을 함께 VM을 배포 하기 전에 필요한 toobe 되 고 두 개의 Nic를 나열 합니다.

    ```json
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('dbVMSetting').vmName,copyindex(1))]",
    "location": "[variables('location')]",
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-RA-', copyindex(1))]",
      "[concat('Microsoft.Compute/availabilitySets/', variables('dbVMSetting').avsetName)]",
      "[concat('Microsoft.Storage/storageAccounts/', parameters('prmStorageName'))]"
    ],
    "tags": {
      "displayName": "VMs - DB"
    },
    "copy": {
      "name": "dbvmcount",
      "count": "[parameters('dbCount')]"
    },
    ```

12. Hello VM 리소스 toohello에서 아래로 스크롤하여 **networkProfile** 요소 아래에 나와 있습니다. 각 VM의 참조가 되는 두 개의 NIC가 있습니다. Hello를 설정 해야 합니다는 VM에 대 한 여러 Nic를 만들 때 **기본** hello Nic 중 하나의 속성을 너무*true*, 너무 rest hello 및*false*합니다.

    ```json
    "networkProfile": {
      "networkInterfaces": [
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-DA-',copyindex(1)))]",
          "properties": { "primary": true }
        },
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-RA-',copyindex(1)))]",
          "properties": { "primary": false }
        }
      ]
    }
    ```

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a>Hello ARM 템플릿을 사용 하 여 배포 toodeploy 클릭

> [!IMPORTANT]
> Hello를 따르도록 [필수 구성 요소](#Pre-requisites) 아래 hello 지침을 수행 하기 전에 단계입니다.
> 

hello 공용 저장소에서 사용할 수 있는 hello 샘플 템플릿 hello 기본 사용 되는 값 toogenerate hello 위에서 언급 한 시나리오를 포함 하는 매개 변수 파일을 사용 합니다. toodeploy toodeploy, 클릭 하 여 사용 하 여이 서식 파일에 따라 [이 링크](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC)의 오른쪽 toohello **백 엔드 리소스 그룹 (설명서 참조)** 클릭 **tooAzure 배포**, 대체 hello 필요한 경우 기본 매개 변수 값 및 hello 포털의 hello 지침을 따릅니다.

아래 hello 그림에는 배포 후 hello 새 리소스 그룹의 hello 내용을 보여 줍니다.

![백 엔드 리소스 그룹](./media/virtual-network-deploy-multinic-arm-template/Figure2.png)

## <a name="deploy-hello-template-by-using-powershell"></a>PowerShell을 사용 하 여 hello 서식 파일을 배포 합니다.
PowerShell을 사용 하 여 다운로드 한 toodeploy hello 템플릿을 PowerShell 설치 및 구성 hello의 hello 단계를 완료 하 여 [PowerShell 설치 및 구성](/powershell/azure/overview) 문서 및 다음 단계를 수행 하는 hello를 완료 합니다.

Hello 실행  **`New-AzureRmResourceGroup`**  사용 하 여 리소스 그룹 cmdlet toocreate hello 템플릿.

```powershell
New-AzureRmResourceGroup -Name IaaSStory-Backend -Location uswest `
TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json' `
-TemplateParameterFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json'
```

예상 출력:

    ResourceGroupName : IaaSStory-Backend
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    Permissions       :
                        Actions  NotActions
                        =======  ==========
                        *
        Resources         :
                        Name                 Type                                 Location
                        ===================  ===================================  ========
                        ASDB                 Microsoft.Compute/availabilitySets   westus  
                        DB1                  Microsoft.Compute/virtualMachines    westus  
                        DB2                  Microsoft.Compute/virtualMachines    westus  
                        NICDB-DA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-DA-2           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-2           Microsoft.Network/networkInterfaces  westus  
                        wtestvnetstorageprm  Microsoft.Storage/storageAccounts    westus  
    ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Hello Azure CLI를 사용 하 여 hello 서식 파일을 배포 합니다.
hello Azure CLI를 사용 하 여 toodeploy hello 템플릿을 다음 hello 단계를 따릅니다.

1. Azure CLI 처음 사용 하는 경우 참조 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md) Azure 계정 및 구독을 선택 하면 toohello 포인트 hello 지침을 따릅니다.
2. Hello 실행  **`azure config mode`**  명령 tooswitch tooResource 관리자 모드에서는 다음과 같이 합니다.

    ```azurecli
    azure config mode arm
    ```

    hello 예상 출력 다음과:

        info:    New mode is arm

3. 열기 hello [매개 변수 파일](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), 해당 콘텐츠를 선택 하 고 컴퓨터에 tooa 파일을 저장 합니다. 이 예에서는 저장 hello 매개 변수 파일 너무*parameters.json*합니다.
4. Hello 실행  **`azure group deployment create`**  cmdlet toodeploy hello hello 템플릿 및 매개 변수를 사용 하 여 새 VNet이 파일 다운로드 하 고 위에서 수정 합니다. hello 출력 뒤에 표시 된 hello 목록 사용 되는 hello 매개 변수를 설명 합니다.

    ```azurecli
    azure group create -n IaaSStory-Backend -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json -e parameters.json
    ```

    예상 출력:
   
        info:    Executing command group create
        + Getting resource group IaaSStory-Backend
        + Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

