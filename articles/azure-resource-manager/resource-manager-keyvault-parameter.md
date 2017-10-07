---
title: "리소스 관리자 템플릿 사용 하 여 자격 증명 모음 암호 aaaKey | Microsoft Docs"
description: "어떻게 toopass 키에서 암호 자격 증명 모음에 매개 변수로 배포 하는 동안 보여 줍니다."
services: azure-resource-manager,key-vault
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c582c144-4760-49d3-b793-a3e1e89128e2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 0bb7760c95b3b4ef34c9e5cc2e3421be56b5e5e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-key-vault-toopass-secure-parameter-value-during-deployment"></a>배포 중 주요 자격 증명 모음 toopass 보안 매개 변수 값을 사용 합니다.

배포 중 매개 변수로 toopass를 안전한 값 (예: 암호)를 할 때 hello 값을 검색할 수 있습니다는 [Azure 키 자격 증명 모음](../key-vault/key-vault-whatis.md)합니다. Hello 주요 자격 증명 모음 및 암호 매개 변수 파일에 참조 하 여 hello 값을 검색 합니다. hello 값은 주요 자격 증명 모음 ID만 참조 하지 않기 때문에 표시 되지 않으며 않아도 toomanually hello 값 hello 암호에 대 한 때마다 입력 hello 리소스를 배포 합니다. hello 주요 자격 증명 모음에 배포 하는 hello 리소스 그룹 보다는 다른 구독에 있을 수 있습니다. Hello 구독 id입니다. 포함 hello 주요 자격 증명 모음을 참조 하는 경우

Hello 주요 자격 증명 모음을 만들 때 설정 hello *enabledForTemplateDeployment* 속성 너무*true*합니다. 이 값 tootrue를 설정 하 여 배포 하는 동안 리소스 관리자 템플릿에서 대 한 액세스를 허용 합니다.  

## <a name="deploy-a-key-vault-and-secret"></a>키 자격 증명 모음 및 비밀 배포

주요 자격 증명 모음 toocreate 및 암호를 Azure CLI 또는 PowerShell을 사용 합니다. 템플릿 배포에 대 한 해당 hello 키 자격 증명 모음 사용 됨을 확인 합니다. 

Azure CLI의 경우 

```azurecli
vaultname={your-unique-vault-name}
password={password-value}

az group create --name examplegroup --location 'South Central US'
az keyvault create --name $vaultname --resource-group examplegroup --location 'South Central US' --enabled-for-template-deployment true
az keyvault secret set --vault-name $vaultname --name examplesecret --value $password
```

PowerShell의 경우 다음을 사용합니다.

```powershell
$vaultname = "{your-unique-vault-name}"
$password = "{password-value}"

New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmKeyVault -VaultName $vaultname -ResourceGroupName examplegroup -Location "South Central US" -EnabledForTemplateDeployment
$secretvalue = ConvertTo-SecureString $password -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName $vaultname -Name "examplesecret" -SecretValue $secretvalue
```

## <a name="enable-access-toohello-secret"></a>액세스 toohello 암호를 사용 하도록 설정

확인 하는지 여부를 새 키 자격 증명 모음 또는 기존 파일을 사용 하는 hello 서식 파일을 배포 하는 hello 사용자 hello 암호에 액세스할 수 있습니다. 암호를 참조 하는 서식 파일을 배포 하는 hello 사용자 hello 있어야 합니다. `Microsoft.KeyVault/vaults/deploy/action` hello 주요 자격 증명 모음에 대 한 권한이 있습니다. hello [소유자](../active-directory/role-based-access-built-in-roles.md#owner) 및 [참가자](../active-directory/role-based-access-built-in-roles.md#contributor) 역할을 모두이 액세스 권한을 부여 합니다. 만들 수도 있습니다는 [사용자 지정 역할](../active-directory/role-based-access-control-custom-roles.md) 이 사용 권한을 부여 하 고 hello 사용자 toothat 역할을 추가 합니다. 사용자 tooa 역할을 추가 하는 방법에 대 한 정보를 참조 하십시오. [Azure Active Directory에서 tooadministrator 역할에 사용자 지정](../active-directory/active-directory-users-assign-role-azure-portal.md)합니다.


## <a name="reference-a-secret-with-static-id"></a>정적 ID로 비밀 참조

키 자격 증명 모음 암호를 수신 하는 hello 템플릿을 다른 서식 파일과 비슷합니다. 때문 **hello 키 자격 증명 모음 hello 매개 변수 파일을 하지 hello 서식 파일을 참조 합니다.** 예를 들어 다음 템플릿을 hello 관리자 암호를 포함 하는 SQL 데이터베이스를 배포 합니다. hello password 매개 변수는 tooa 보안 문자열로 설정 됩니다. 하지만 hello 서식 파일에서 해당 값을 제공 하는 위치를 지정 하지 않습니다.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "administratorLogin": {
            "type": "string"
        },
        "administratorLoginPassword": {
            "type": "securestring"
        },
        "collation": {
            "type": "string"
        },
        "databaseName": {
            "type": "string"
        },
        "edition": {
            "type": "string"
        },
        "requestedServiceObjectiveId": {
            "type": "string"
        },
        "location": {
            "type": "string"
        },
        "maxSizeBytes": {
            "type": "string"
        },
        "serverName": {
            "type": "string"
        },
        "sampleName": {
            "type": "string",
            "defaultValue": ""
        }
    },
    "resources": [
        {
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "name": "[parameters('serverName')]",
            "properties": {
                "administratorLogin": "[parameters('administratorLogin')]",
                "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
                "version": "12.0"
            },
            "resources": [
                {
                    "apiVersion": "2014-04-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Sql/servers/', parameters('serverName'))]"
                    ],
                    "location": "[parameters('location')]",
                    "name": "[parameters('databaseName')]",
                    "properties": {
                        "collation": "[parameters('collation')]",
                        "edition": "[parameters('edition')]",
                        "maxSizeBytes": "[parameters('maxSizeBytes')]",
                        "requestedServiceObjectiveId": "[parameters('requestedServiceObjectiveId')]",
                        "sampleName": "[parameters('sampleName')]"
                    },
                    "type": "databases"
                },
                {
                    "apiVersion": "2014-04-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Sql/servers/', parameters('serverName'))]"
                    ],
                    "location": "[parameters('location')]",
                    "name": "AllowAllWindowsAzureIps",
                    "properties": {
                        "endIpAddress": "0.0.0.0",
                        "startIpAddress": "0.0.0.0"
                    },
                    "type": "firewallrules"
                }
            ],
            "type": "Microsoft.Sql/servers"
        }
    ]
}
```

이제 hello 앞에 서식 파일에 대 한 매개 변수 파일을 만듭니다. Hello 매개 변수 파일에서 hello 서식 파일에서 hello 매개 변수가 hello 이름과 일치 하는 매개 변수를 지정 합니다. Hello 매개 변수 값에 대 한 hello hello 키 자격 증명 모음에서 암호를 참조 합니다. Hello 키 자격 증명 모음의 hello 리소스 식별자 및 hello 암호의 hello 이름을 전달 하 여 hello 비밀을 참조 합니다. 다음 예제는 hello에서 hello 키 자격 증명 모음 암호 이미 있어야 하며, 리소스 ID에 대 한 정적 값을 제공

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "administratorLogin": {
            "value": "exampleadmin"
        },
        "administratorLoginPassword": {
            "reference": {
              "keyVault": {
                "id": "/subscriptions/{guid}/resourceGroups/examplegroup/providers/Microsoft.KeyVault/vaults/{vault-name}"
              },
              "secretName": "examplesecret"
            }
        },
        "collation": {
            "value": "SQL_Latin1_General_CP1_CI_AS"
        },
        "databaseName": {
            "value": "exampledb"
        },
        "edition": {
            "value": "Standard"
        },
        "location": {
            "value": "southcentralus"
        },
        "maxSizeBytes": {
            "value": "268435456000"
        },
        "requestedServiceObjectiveId": {
            "value": "455330e1-00cd-488b-b5fa-177c226f28b7"
        },
        "sampleName": {
            "value": ""
        },
        "serverName": {
            "value": "exampleserver"
        }
    }
}
```

## <a name="reference-a-secret-with-dynamic-id"></a>동적 ID로 비밀 참조

정적 리소스 ID toopass hello 키에 대 한 보안 자격 증명 모음에 어떻게 hello 이전 섹션에 살펴보았습니다. 그러나 일부 시나리오에서는 tooreference hello 현재 배포에 따라 달라 지는 주요 자격 증명 모음 암호 해야 합니다. 이 경우 리소스 ID를 hello 매개 변수 파일에 하드 코드 hello 수 없습니다. 안타깝게도, 생성할 수 없습니다 동적으로 hello 리소스 ID hello 매개 변수 파일에 있으므로 hello 매개 변수 파일에 템플릿 식이 허용 되지 않습니다.

toodynamically 생성 되는 주요 자격 증명 모음 암호에 대 한 hello 리소스 ID, 중첩 된 템플릿으로 hello 암호를 필요로 하는 hello 리소스를 이동 해야 합니다. 마스터 서식 파일에서 hello 중첩 된 템플릿 추가 하 고이 동적으로 생성 된 hello 리소스 ID를 포함 하는 매개 변수 전달

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "vaultName": {
        "type": "string"
      },
      "secretName": {
        "type": "string"
      }
    },
    "resources": [
    {
      "apiVersion": "2015-01-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newVM.json",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "reference": {
              "keyVault": {
                "id": "[concat(resourceGroup().id, '/providers/Microsoft.KeyVault/vaults/', parameters('vaultName'))]"
              },
              "secretName": "[parameters('secretName')]"
            }
          }
        }
      }
    }],
    "outputs": {}
}
```

## <a name="next-steps"></a>다음 단계
* 키 자격 증명 모음에 대한 일반 정보는 [Azure Key Vault 시작](../key-vault/key-vault-get-started.md)을 참조하세요.
* 키 비밀을 참조하는 전체 예제는 [키 자격 증명 모음 예제](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples)를 참조하세요.

