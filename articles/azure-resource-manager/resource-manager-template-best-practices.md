---
title: "리소스 관리자 템플릿을 만들기 위한 aaaBest 사례 | Microsoft Docs"
description: "Azure Resource Manager 템플릿 간소화를 위한 지침입니다."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 31b10deb-0183-47ce-a5ba-6d0ff2ae8ab3
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: tomfitz
ms.openlocfilehash: ec9bbe218c4f2c6a92ca44b5e9c9c71029e22151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-azure-resource-manager-templates"></a>Azure Resource Manager 템플릿 생성 모범 사례
이러한 지침을 사용 하면 신뢰할 수 있는 쉽고 toouse 된 Azure 리소스 관리자 템플릿이 만들 수 있습니다. hello 지침만 제안 됩니다. 명시된 경우를 제외하고 필수 사항은 아닙니다. 시나리오 hello 중 하나의 변형 해야 합니다. 다음 접근 방식 또는 예제입니다.

## <a name="resource-names"></a>리소스 이름
일반적으로 Resource Manager에서는 세 가지 유형의 리소스 이름으로 작업합니다.

* 고유해야 하는 리소스 이름
* 되지 않는 리소스 이름이 필요 toobe 고유 하지만, 컨텍스트를 기준으로 리소스를 식별 하는 수 있는 이름이 tooprovide 선택.
* 일반적일 수 있는 리소스 이름

 리소스 이름 제한에 대한 자세한 내용은 [Azure 리소스에 대한 권장 명명 규칙](../guidance/guidance-naming-conventions.md)을 참조하세요.

### <a name="unique-resource-names"></a>고유한 리소스 이름
데이터 액세스 끝점이 있는 모든 리소스 유형에 대해 고유한 리소스 이름을 제공해야 합니다. 고유 이름이 필요한 일반적인 리소스 유형은 다음과 같습니다.

* Azure Storage<sup>1</sup> 
* Azure App Service의 Web Apps 기능
* SQL Server
* Azure 키 자격 증명 모음
* Azure Redis 캐시(영문)
* Azure 배치
* Azure 트래픽 관리자
* Azure 검색
* Azure HDInsight

<sup>1</sup> 저장소 계정 이름은 24자 이내의 소문자여야 하며 하이픈은 포함할 수 없습니다.

리소스 이름에 대 한 매개 변수를 지정 하는 경우 hello 리소스를 배포할 때 고유 이름을 제공 해야 합니다. Hello를 사용 하는 변수를 만들 수는 필요에 따라 [uniqueString()](resource-group-template-functions-string.md#uniquestring) toogenerate 이름을 작동 합니다. 

또한 수 원하는 tooadd 접두사 또는 toohello 접미사 **uniqueString** 결과입니다. Hello 고유 이름을 수정 하 고 더욱 쉽게 hello 이름에서 hello 리소스 종류를 식별할 수 유용 합니다. 예를 들어 변수 다음 hello를 사용 하 여 저장소 계정에 대 한 고유 이름을 생성할 수 있습니다.

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a>식별을 위한 리소스 이름
일부 리소스 유형은 이름만 toobe 고유 하지 않은 있지만 tooname를 할 수 있습니다. 이러한 리소스 종류에 대 한 hello 리소스 컨텍스트와 hello 리소스 종류 모두 식별 하는 이름을 제공할 수 있습니다. 리소스 목록에 hello 리소스를 식별 하는 데 도움이 되는 설명이 포함 된 이름을 제공 합니다. 다양 한 배포에 대 한 다른 리소스 이름을 toouse 해야 할 경우에 hello 이름에 대 한 매개 변수를 사용할 수 있습니다.

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "hello name of hello VM toocreate."
        }
    }
}
```

배포 중 이름에 toopass를 필요 하지 않은 경우에 변수를 사용할 수 있습니다. 

```json
"variables": {
    "vmName": "demoLinuxVM"
}
```

하드 코드된 값을 사용할 수도 있습니다.

```json
{
  "type": "Microsoft.Compute/virtualMachines",
  "name": "demoLinuxVM",
  ...
}
```

### <a name="generic-resource-names"></a>일반 리소스 이름
주로 다른 리소스를 통해 액세스 하는 리소스 종류에 대 한 hello 템플릿에 하드 코드 하는 제네릭 이름을 사용할 수 있습니다. 예를 들어 SQL Server에서 방화벽 규칙에 대해 표준 일반 이름을 설정할 수 있습니다.

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="parameters"></a>매개 변수
hello 다음 정보가 유용할 수 매개 변수를 사용 하 여 작업할 때:

* 매개 변수 사용을 최소화합니다. 가능하면 항상, 변수 또는 리터럴 값을 사용합니다. 다음과 같은 시나리오에 대해서만 매개 변수를 사용합니다.
   
   * Tooenvironment (SKU, 크기, 용량)에 따라의 toouse 변형을 지정 하는 설정입니다.
   * 쉽게 식별 하기 위해 toospecify 되도록 하는 리소스 이름입니다.
   * 값을 사용 하는 자주 toocomplete 다른 작업 (예: 관리자 사용자 이름)입니다.
   * 비밀(예: 암호)
   * hello 숫자나 값 toouse 리소스 종류의 여러 인스턴스를 만들 때의 배열입니다.
* 매개 변수 이름에 카멜식 대/소문자를 사용합니다.
* Hello 메타 데이터의 모든 매개 변수에 대 한 설명을 제공 합니다.

   ```json
   "parameters": {
       "storageAccountType": {
           "type": "string",
           "metadata": {
               "description": "hello type of hello new storage account created toostore hello VM disks."
           }
       }
   }
   ```

* 매개 변수의 기본값을 정의합니다(암호 및 SSH 키 제외).
   
   ```json
   "parameters": {
        "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_GRS",
            "metadata": {
                "description": "hello type of hello new storage account created toostore hello VM disks."
            }
        }
   }
   ```

* 모든 암호(password) 및 비밀(secret)에 대해 **SecureString**을 사용합니다. 
   
   ```json
   "parameters": {
       "secretValue": {
           "type": "securestring",
           "metadata": {
               "description": "hello value of hello secret toostore in hello vault."
           }
       }
   }
   ```

* 가능 하면 항상 매개 변수 toospecify 위치를 사용 하지 마십시오. 대신, hello를 사용 하 여 **위치** hello 리소스 그룹의 속성입니다. Hello를 사용 하 여 **resourceGroup ().location** 모든 리소스에 대 한 식, hello 서식 파일의 리소스에 배포 된 hello 같은 hello 리소스 그룹 위치:
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         ...
     }
   ]
   ```
   
   제한 된 수의 위치에서는 리소스 종류는 지원 toospecify hello 서식 파일에서 직접 올바른 위치를 할 수 있습니다. 사용 해야 할 경우는 **위치** 매개 변수를 해당 매개 변수 값을 가능한 한 hello에 가능성이 toobe 않은 리소스와 공유 동일한 위치입니다. 이 사용자에 게 tooprovide 위치 정보를 요청 하는 횟수 hello 만큼을 최소화 합니다.
* 리소스 종류에 대 한 hello API 버전에 대 한 매개 변수 또는 변수를 사용 하지 마십시오. 리소스 속성 및 값은 버전 번호에 따라 달라질 수 있습니다. 코드 편집기의 IntelliSense는 hello API 버전 tooa 매개 변수 또는 변수에 설정 된 경우 hello 올바른 스키마를 확인할 수 없습니다. 대신, 하드 코딩 hello hello 서식 파일에서 API 버전입니다.

## <a name="variables"></a>variables
hello 다음 정보가 유용할 수 변수를 사용 하 여 작업할 때:

* 된다고 toouse 두 번 이상 서식 파일의 값에 대 한 변수를 사용 합니다. 값을 한 번만 사용 되는 경우 하드 코드 된 값 이면 템플릿을 쉽게 tooread.
* Hello를 사용할 수 없습니다 [참조](resource-group-template-functions-resource.md#reference) 함수 hello에 **변수** hello 서식 파일의 섹션입니다. hello **참조** 함수 hello 리소스의 런타임 상태에서 해당 값을 파생 합니다. 그러나 변수 hello 초기 hello 서식 파일의 구문 분석 하는 동안 확인 됩니다. Hello를 필요로 하는 값을 생성 **참조** hello에서 직접 함수 **리소스** 또는 **출력** hello 서식 파일의 섹션입니다.
* [리소스 이름](#resource-names)에 설명된 대로 고유해야 하는 리소스 이름에 대한 변수를 포함합니다.
* 변수를 복잡한 개체로 그룹화할 수 있습니다. 사용 하 여 hello **variable.subentry** tooreference 복잡 한 개체의 값 형식을 지정 합니다. 변수 그룹화는 관련 변수를 추적하는 데 도움이 됩니다. 또한 hello 서식 파일의 가독성을 개선합니다. 예를 들면 다음과 같습니다.
   
   ```json
   "variables": {
       "storage": {
           "name": "[concat(uniqueString(resourceGroup().id),'storage')]",
           "type": "Standard_LRS"
       }
   },
   "resources": [
     {
         "type": "Microsoft.Storage/storageAccounts",
         "name": "[variables('storage').name]",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "sku": {
             "name": "[variables('storage').type]"
         },
         ...
     }
   ]
   ```
   
   > [!NOTE]
   > 복잡한 개체에는 복잡한 개체의 값을 참조하는 식이 포함될 수 없습니다. 이 목적을 위해서는 별도의 변수를 정의합니다.
   > 
   > 
   
     복잡한 개체를 변수로 사용하는 고급 예제를 보려면 [Azure Resource Manager 템플릿에서 상태 공유](best-practices-resource-manager-state.md)를 참조하세요.

## <a name="resources"></a>리소스
hello 다음 정보가 유용할 수 리소스를 사용 하 여 작업할 때:

* toohelp 다른 참가자 hello 리소스의 hello 목적을 이해, 지정 **주석** hello 서식 파일의 각 리소스에 대해:
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used toostore hello VM disks.",
         ...
     }
   ]
   ```

* 태그 tooadd 메타 데이터 tooresources를 사용할 수 있습니다. 리소스에 대 한 메타 데이터 tooadd 정보를 사용 합니다. 예를 들어 toorecord 메타 데이터는 리소스에 대 한 청구 정보를 추가할 수 있습니다. 자세한 내용은 참조 [를 사용 하 여 Azure 리소스를 tooorganize 태그](resource-group-using-tags.md)합니다.
* 사용 하는 경우는 *공용 끝점* (예: Azure Blob 저장소 공용 끝점), 템플릿에 *하드 코딩 하지 마십시오* hello 네임 스페이스입니다. 사용 하 여 hello **참조** 함수 toodynamically hello 네임 스페이스를 검색 합니다. 이 접근 방식을 toodeploy hello 템플릿 toodifferent 공용 네임 스페이스 환경 hello 템플릿에서 hello 끝점을 수동으로 변경 하지 않고 사용할 수 있습니다. Hello API 버전 toohello 설정 hello 저장소 계정에 대 한 서식 파일에는 사용 하는 동일한 버전:
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   저장소 계정 hello hello에 배포 된 경우 만들고 있는 동일한 템플릿을 않아도 toospecify hello 공급자 네임 스페이스 hello 리소스를 참조 하는 경우. 다음은 hello 간소화 된 구문입니다.
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   다른 값을 서식 파일에 구성 된 toouse 공용 네임 스페이스를 사용 하도록 설정한 경우 이러한 값을 변경 합니다. 동일한 tooreflect hello **참조** 함수입니다. 예를 들어 hello를 설정할 수 있습니다 **storageUri** hello 가상 컴퓨터 진단 프로필의 속성:
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   다른 리소스 그룹에서 기존 저장소 계정을 참조할 수도 있습니다.

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* 응용 프로그램에서 필요로 하는 경우에 공용 IP 주소 tooa 가상 컴퓨터를 할당 합니다. tooconnect tooa 또는 가상 컴퓨터 (VM) 디버깅을 위한 관리 또는 관리 목적을 위한 인바운드 NAT 규칙, 가상 네트워크 게이트웨이 또는 jumpbox 사용 합니다.
   
     Toovirtual 컴퓨터를 연결 하는 방법에 대 한 자세한 내용은 다음을 참조 합니다.
   
   * [Azure에서 N 계층 아키텍처에 대한 VM 실행](../guidance/guidance-compute-n-tier-vm.md)
   * [Azure Resource Manager에서 VM에 대한 WinRM 액세스 설정](../virtual-machines/windows/winrm.md)
   * [외부 액세스 tooyour VM hello Azure 포털을 사용 하 여 허용](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [PowerShell을 사용 하 여 외부 액세스 tooyour VM 허용](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [Azure CLI를 사용 하 여 외부 액세스 tooyour Linux VM 수](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* hello **domainNameLabel** 공용 IP 주소에 대 한 속성은 고유 해야 합니다. hello **domainNameLabel** 값 3-63 자 사이 여야 하며이 정규식으로 지정 된 hello 규칙을 따릅니다: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`합니다. 때문에 hello **uniqueString** 함수는 13 자 hello 하는 문자열을 생성 **dnsPrefixString** 매개 변수는 제한 된 too50 문자:

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "hello DNS label for hello public IP address. It must be lowercase. It should match hello following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* Hello를 사용 하 여 암호 tooa 사용자 지정 스크립트 확장을 추가 하면 **commandToExecute** hello에 대 한 속성 **protectedSettings** 속성:
   
   ```json
   "properties": {
       "publisher": "Microsoft.Azure.Extensions",
       "type": "CustomScript",
       "typeHandlerVersion": "2.0",
       "autoUpgradeMinorVersion": true,
       "settings": {
           "fileUris": [
               "[concat(variables('template').assets, '/lamp-app/install_lamp.sh')]"
           ]
       },
       "protectedSettings": {
           "commandToExecute": "[concat('sh install_lamp.sh ', parameters('mySqlPassword'))]"
       }
   }
   ```
   
   > [!NOTE]
   > 암호는 tooensure tooVMs 매개 변수 및 확장으로 전달 될 때 암호화를 사용 하 여 hello **protectedSettings** hello 관련 확장의 속성입니다.
   > 
   > 

## <a name="outputs"></a>outputs
서식 파일 toocreate 공용 IP 주소를 사용 하 여는 **출력** hello IP 주소와 hello 정규화 된 도메인 이름 (FQDN)의 세부 정보를 반환 하는 섹션입니다. 배포 후 공용 IP 주소와 Fqdn에 대 한 출력 값 tooeasily 검색 정보를 사용할 수 있습니다. Hello 리소스를 참조 하는 경우 toocreate를 사용 하 여 hello API 버전을 사용 하기: 

```json
"outputs": {
    "fqdn": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').dnsSettings.fqdn]",
        "type": "string"
    },
    "ipaddress": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').ipAddress]",
        "type": "string"
    }
}
```

## <a name="single-template-vs-nested-templates"></a>단일 템플릿 또는 중첩된 템플릿
toodeploy 솔루션에 여러 개의 중첩 된 템플릿으로 단일 템플릿 또는 기본 서식 파일을 사용할 수 있습니다. 중첩된 템플릿은 좀 더 수준 높은 시나리오에서 일반적입니다. 다음 이점을 hello 중첩 된 템플릿 제공을 사용 하 여:

* 솔루션을 대상 구성 요소로 세분화할 수 있습니다.
* 중첩된 템플릿은 다른 주 템플릿에서 다시 사용할 수 있습니다.

중첩 toouse 서식 파일을 선택 하면 표준화 템플릿 디자인 지침에 따라 hello 수 있습니다. 이러한 지침은 [Azure Resource Manager 템플릿 디자인 패턴](best-practices-resource-manager-design-templates.md)을 기준으로 합니다. 다음 템플릿 hello 있는 디자인을 사용 하는 것이 좋습니다.

* **주 템플릿** (azuredeploy.json). Hello 입력된 매개 변수를 사용 합니다.
* **공유 리소스 템플릿**. 사용 하 여 toodeploy 공유 된 다른 모든 리소스를 사용 하는 리소스 (예를 들어 가상 네트워크 및 가용성 집합). 사용 하 여 hello **dependsOn** 이 템플릿은 다른 템플릿에 하기 전에 배포 된 식 tooensure 합니다.
* **선택적 리소스 템플릿**. 사용 하 여 tooconditionally 매개 변수 (예를 들어 jumpbox)에 따라 리소스를 배포 합니다.
* **멤버 리소스 템플릿**. 응용 프로그램 계층 내의 각 인스턴스 형식은 자체 구성을 가집니다. 계층 내에서 서로 다른 인스턴스 형식을 정의할 수 있습니다. (예를 들어 hello 첫 번째 인스턴스는 클러스터를 만들고 및 인스턴스가 더 toohello 기존 클러스터에 추가 됩니다.) 각 인스턴스 형식에는 고유한 배포 템플릿이 있습니다.
* **스크립트**. 폭 넓게 재사용할 수 있는 스크립트를 각 인스턴스 형식에 적용할 수 있습니다(예: 추가 디스크 초기화 및 포맷). 특정 사용자 지정 목적을 위해 생성 된 사용자 지정 스크립트는 hello 인스턴스 형식에 따라 다릅니다.

![중첩된 템플릿](./media/resource-manager-template-best-practices/nestedTemplateDesign.png)

자세한 내용은 [Azure Resource Manager에서 연결된 템플릿 사용](resource-group-linked-templates.md)을 참조하세요.

## <a name="conditionally-link-toonested-templates"></a>조건에 따라 toonested 템플릿 연결
매개 변수 tooconditionally 링크 toonested 템플릿을 사용할 수 있습니다. hello 매개 변수를 사용 하면 hello 서식 파일에 대 한 hello URI의 일부가:

```json
"parameters": {
    "newOrExisting": {
        "type": "String",
        "allowedValues": [
            "new",
            "existing"
        ]
    }
},
"variables": {
    "templatelink": "[concat('https://raw.githubusercontent.com/Contoso/Templates/master/',parameters('newOrExisting'),'StorageAccount.json')]"
},
"resources": [
    {
        "apiVersion": "2015-01-01",
        "name": "nestedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
            "mode": "incremental",
            "templateLink": {
                "uri": "[variables('templatelink')]",
                "contentVersion": "1.0.0.0"
            },
            "parameters": {
            }
        }
    }
]
```

## <a name="template-format"></a>템플릿 형식
것이 좋습니다 toopass JSON 유효성 검사기를 통해 서식 파일에 있습니다. 유효성 검사기를 통해 불필요한 쉼표, 괄호 및 배포 중에 오류를 유발할 수 있는 대괄호를 제거할 수 있습니다. 자주 사용하는 편집 환경을 위해 [JSONLint](http://jsonlint.com/) 또는 linter 패키지를 사용합니다(Visual Studio Code, Atom, Sublime Text, Visual Studio 등).

좋습니다 tooformat 이기도 가독성을 높이기 위해, JSON입니다. 로컬 편집기에 대한 JSON 포맷터 패키지를 사용할 수 있습니다. 키를 눌러 Visual studio에서는 tooformat hello 문서 **Ctrl + K, Ctrl + D**합니다. Visual Studio Code에서 **Alt+Shift+F**를 누릅니다. 로컬 편집기 hello 문서의 서식을 지정 하지 않습니다, 하는 경우 사용할 수 있습니다는 [온라인 포맷터](https://www.bing.com/search?q=json+formatter)합니다.

## <a name="next-steps"></a>다음 단계
* 가상 컴퓨터를 위한 솔루션 설계에 대한 자세한 내용은 [Azure에서 Windows VM 실행](../guidance/guidance-compute-single-vm.md) 및 [Azure에서 Linux VM 실행](../guidance/guidance-compute-single-vm-linux.md)을 참조하세요.
* 저장소 계정 설정에 대한 자세한 내용은 [Azure Storage 성능 및 확장성 검사 목록](../storage/common/storage-performance-checklist.md)을 참조하세요.
* toolearn 엔터프라이즈 tooeffectively 리소스 관리자를 사용 하는 방법에 대 한 구독 관리, 참조 [Azure enterprise 스 캐 폴딩: 규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.

