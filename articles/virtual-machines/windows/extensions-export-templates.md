---
title: "VM 확장을 포함 하는 Azure 리소스 그룹 aaaExporting | Microsoft Docs"
description: "가상 컴퓨터 확장을 포함하는 Resource Manager 템플릿을 내보냅니다."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7f4e2ca6-f1c7-4f59-a2cc-8f63132de279
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: nepeters
ms.openlocfilehash: cdbc2030988a19fe68429e8733dc60536c264abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a>VM 확장을 포함하는 리소스 그룹 내보내기

Azure 리소스 그룹을 새 Resource Manager 템플릿으로 내보낸 후 다시 배포할 수 있습니다. hello 내보내기 프로세스 기존 리소스를 해석 하 고 배포할 때 리소스 관리자 템플릿을 만들고 비슷한 리소스 그룹에서 발생 합니다. 가상 컴퓨터 확장을 포함 하는 리소스 그룹에 대 한 hello 리소스 그룹 내보내기 옵션을 사용할 경우 몇 가지 항목 필요 toobe 확장 호환성 같은 것으로 간주 하 고 설정을 보호 합니다.

이 문서 정보 hello 리소스 그룹 내보내기 프로세스의 목록이 포함 되는 가상 컴퓨터 확장에 대 한 작동 하는 방법에 확장을 지원 하 고 처리에 대 한 세부 정보 데이터를 보안 키를 누릅니다.

## <a name="supported-virtual-machine-extensions"></a>지원되는 가상 컴퓨터 확장

여러 가상 컴퓨터 확장을 사용할 수 있습니다. 모든 확장이 hello "자동화 스크립트" 기능을 사용 하 여 리소스 관리자 템플릿으로 내보낼 수 있습니다. 가상 컴퓨터 확장 지원 되지 않는 경우 수동으로 hello 내보낸된 서식 파일에 다시 배치 toobe가 필요 합니다.

hello 다음 확장 프로그램 내보낼 수 있습니다 hello 자동화 스크립트 기능.

| 내선 번호 ||||
|---|---|---|---|
| Acronis Backup | Datadog Windows Agent | OS Patching For Linux | VM Snapshot Linux
| Acronis Backup Linux | Docker 확장 | Puppet Agent |
| Bg Info | DSC Extension | Site 24x7 Apm Insight |
| BMC CTM Agent Linux | Dynatrace Linux | Site 24x7 Linux Server |
| BMC CTM Agent Windows | Dynatrace Windows | Site 24x7 Windows Server |
| Chef Client | HPE Security Application Defender | Trend Micro DSA |
| Custom Script | IaaS Antimalware | Trend Micro DSA Linux |
| 사용자 지정 스크립트 확장 | IaaS Diagnostics | VM Access For Linux |
| Custom Script for Linux | Linux Chef Client | VM Access For Linux |
| Datadog Linux Agent | Linux Diagnostic | VM Snapshot |

## <a name="export-hello-resource-group"></a>내보내기 hello 리소스 그룹

리소스 그룹을 다시 사용할 수 있는 템플릿으로 단계를 수행 하는 전체 hello tooexport:

1. Azure 포털 toohello에 로그인
2. Hello 허브 메뉴에서 리소스 그룹을 클릭 합니다.
3. Hello 목록에서 hello 대상 리소스 그룹을 선택 합니다.
4. Hello 리소스 그룹 블레이드에서 자동화 스크립트를 클릭 합니다.

![템플릿 내보내기](./media/extensions-export-templates/template-export.png)

hello Azure 리소스 관리자 자동화 스크립트는 리소스 관리자 템플릿, 매개 변수 파일 및 PowerShell 및 Azure CLI 같은 몇 가지 예제 배포 스크립트를 생성합니다. 이 시점에서 hello 내보낸된 템플릿을 다운로드할 수 있습니다으로 새 템플릿 toohello 템플릿 라이브러리를 추가 하거나 hello를 사용 하 여 다시 배포한 hello 다운로드 단추를 사용 하 여 단추를 배포 합니다.

## <a name="configure-protected-settings"></a>보호 설정 구성

여러 Azure Virtual Machine 확장에는 자격 증명 및 구성 문자열과 같은 중요한 데이터를 암호화하는 보호 설정 구성이 포함됩니다. 보호 된 설정 hello 자동화 스크립트와 함께 내보낼 수 없습니다. 필요한, 보호 된 설정을 hello에 다시 삽입할 toobe 필요한 템플릿 기반 내보내집니다.

### <a name="step-1---remove-template-parameter"></a>1단계 - 템플릿 매개 변수 제거

리소스 그룹을 내보내는 hello 단일 템플릿 매개 변수를 만들면 tooprovide 값 toohello 보호 설정을 내보냅니다. 이 매개 변수는 제거할 수 있습니다. tooremove hello 매개 변수를 hello 매개 변수 목록 전체를 검사 하 고 다음과 비슷한 toothis JSON의 예는 hello 매개 변수를 삭제 합니다.

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a>2단계 - 보호 설정 속성 가져오기

각 보호 설정을 필수 속성의 집합을 사용 하므로 이러한 속성 목록은 수집 toobe가 필요 합니다. Hello에 hello 보호 설정 구성의 각 매개 변수에 있습니다 [GitHub의 Azure 리소스 관리자 스키마](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json)합니다. 이 스키마는이 문서의 hello 개요 섹션에 나열 된 hello 확장에 대 한 hello 매개 변수 집합을 포함 합니다. 

Hello 스키마 리포지토리 내에서 검색할이 예제에 대 한 원하는 hello 확장 `IaaSDiagnostics`합니다. 한 번 확장 hello `protectedSettings` 개체 찾았습니다, 각 매개 변수를 기록 합니다. Hello의 hello 예제에서 `IaasDiagnostic` 확장 프로그램, hello 필요한 매개 변수는 `storageAccountName`, `storageAccountKey`, 및 `storageAccountEndPoint`합니다.

```json
"protectedSettings": {
    "type": "object",
    "properties": {
        "storageAccountName": {
            "type": "string"
        },
        "storageAccountKey": {
            "type": "string"
        },
        "storageAccountEndPoint": {
            "type": "string"
        }
    },
    "required": [
        "storageAccountName",
        "storageAccountKey",
        "storageAccountEndPoint"
    ]
}
```

### <a name="step-3---re-create-hello-protected-configuration"></a>3 단계-hello 보호 구성 다시 만들기

내보낸된 템플릿 hello, 검색할 `protectedSettings` 개체를 내보낸된 보호 설정 하는 hello hello 필요한 확장 프로그램 매개 변수 및 각각에 대 한 값을 포함 하는 새 항목으로 바꿉니다.

Hello의 hello 예제에서 `IaasDiagnostic` 확장명 hello 새 보호 설정 구성 같습니다. 다음 예제는 hello:

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

hello 최종 확장을 리소스에는 다음 JSON 예제와 비슷한 toohello 표시 됩니다.

```json
{
    "name": "Microsoft.Insights.VMDiagnosticsSettings",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "[variables('apiVersion')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "tags": {
        "displayName": "AzureDiagnostics"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
            "storageAccountName": "[parameters('storageAccountName')]",
            "storageAccountKey": "[parameters('storageAccountKey')]",
            "storageAccountEndPoint": "https://core.windows.net"
        }
    }
}
```

템플릿 매개 변수 tooprovide 속성 값을 사용 하는 경우 이러한 만든 toobe가 필요 합니다. 템플릿 매개 변수 값을 설정 하는 보호 된를 만들 때 확인 되었는지 toouse hello `SecureString` 매개 변수를 입력 하 여 중요 한 값 보안이 유지 됩니다. 매개 변수 사용에 대한 자세한 내용은 [Azure Resource Manager 템플릿 작성](../../resource-group-authoring-templates.md)을 참조하세요.

Hello의 hello 예제에서 `IaasDiagnostic` 확장명 hello 매개 변수 뒤에 만들어짐 hello 리소스 관리자 템플릿의 hello 매개 변수 섹션.

```json
"storageAccountName": {
    "defaultValue": null,
    "type": "SecureString"
},
"storageAccountKey": {
    "defaultValue": null,
    "type": "SecureString"
}
```

이 시점에서 hello 템플릿에 템플릿 배포 방법을 사용 하 여 배포할 수 있습니다.
