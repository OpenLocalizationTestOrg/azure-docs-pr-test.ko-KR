---
title: "Windows 용 사용자 지정 스크립트 확장 aaaAzure | Microsoft Docs"
description: "Hello 사용자 지정 스크립트 확장을 사용 하 여 Windows VM 구성 작업을 자동화 합니다."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f4181fee-7a9d-4a1c-b517-52956f5b7fa1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/16/2017
ms.author: nepeters
ms.openlocfilehash: 97e065242e9fed116ee20b074f4e302a0cd10585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows"></a>Windows용 사용자 지정 스크립트 확장

사용자 지정 스크립트 확장 hello 다운로드 하 고 Azure 가상 컴퓨터에서 스크립트를 실행 합니다. 이 확장은 배포 후 구성, 소프트웨어 설치 또는 기타 구성/관리 작업에 유용합니다. 스크립트는 Azure 저장소 또는 GitHub에서 다운로드 또는 toohello Azure 포털 확장 실행 시간에 제공 수 있습니다. 사용자 지정 스크립트 확장 hello Azure 리소스 관리자 템플릿 뿐 아니라 통합 하 고 hello Azure CLI, PowerShell, Azure 포털 또는 hello Azure 가상 컴퓨터 REST API를 사용 하 여 실행할 수도 있습니다.

이 문서는 Azure PowerShell 모듈, Azure 리소스 관리자 템플릿 및 문제 해결 단계는 Windows 시스템에서 세부 정보 어떻게 hello toouse hello 사용자 지정 스크립트 확장을 사용 하 여 자세히 설명 합니다.

## <a name="prerequisites"></a>필수 조건

### <a name="operating-system"></a>운영 체제

사용자 지정 스크립트 확장 hello Windows Server 2008 r 2에 대해 Windows를 실행할 수에 대 한 2016, R2, 2012 및 2012를 해제 합니다.

### <a name="script-location"></a>스크립트 위치

hello 스크립트 toobe Azure Blob 저장소 또는 올바른 URL을 통해 액세스할 수 있는 기타 위치에 저장 해야 합니다.

### <a name="internet-connectivity"></a>인터넷 연결

hello Windows에 대 한 사용자 지정 스크립트 확장에서는 해당 hello 대상 가상 컴퓨터가 연결 된 toohello 인터넷 합니다. 

## <a name="extension-schema"></a>확장 스키마

hello 다음 JSON hello 스키마를 표시 사용자 지정 스크립트 확장이 hello에 대 한 합니다. hello 확장 (Azure 저장소 또는 올바른 URL 사용 하 여 다른 위치) 스크립트 위치 및 명령 tooexecute 필요합니다. Azure 저장소 hello 스크립트 원본으로 사용 하는 경우 Azure 저장소 계정 이름 및 계정 키가 필요 합니다. 이러한 항목으로 중요 한 데이터를 처리 하 고 hello 확장 보호 설정 구성에 지정 해야 합니다. Azure VM 확장으로 보호 된 데이터를 설정 하는 암호화 되 고 hello 대상 가상 컴퓨터에 암호를 해독할 됩니다.

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
        "[variables('musicstoresqlName')]"
    ],
    "tags": {
        "displayName": "config-app"
    },
    "properties": {
        "publisher": "Microsoft.Compute",
        "type": "CustomScriptExtension",
        "typeHandlerVersion": "1.9",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "fileUris": [
                "script location"
            ]
        },
        "protectedSettings": {
            "commandToExecute": "myExecutionCommand",
            "storageAccountName": "myStorageAccountName",
            "storageAccountKey": "myStorageAccountKey"
        }
    }
}
```

### <a name="property-values"></a>속성 값

| 이름 | 값/예제 |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publisher | Microsoft.Compute |
| type | 확장 |
| typeHandlerVersion | 1.9 |
| fileUris(예) | https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1 |
| commandToExecute(예) | powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 |
| storageAccountName(예) | examplestorageacct |
| storageAccountKey(예) | TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg== |

**참고** - 이러한 속성 이름은 대/소문자를 구분합니다. 배포 문제 tooavoid 위의 예제와 같이 hello 이름을 사용 합니다.

## <a name="template-deployment"></a>템플릿 배포

Azure Resource Manager 템플릿을 사용하여 Azure VM 확장을 배포할 수 있습니다. Azure 리소스 관리자 템플릿 배포 중에 Azure 리소스 관리자 템플릿 toorun hello 사용자 지정 스크립트 확장 hello 이전 섹션에서 자세히 설명 하는 hello JSON 스키마를 사용할 수 있습니다. 사용자 지정 스크립트 확장을 여기에서 찾을 수 hello를 포함 하는 샘플 템플릿을 [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)합니다.

## <a name="powershell-deployment"></a>PowerShell 배포

hello `Set-AzureRmVMCustomScriptExtension` 명령을 사용 하는 tooadd hello 사용자 지정 스크립트 확장 tooan 기존 가상 컴퓨터 수 있습니다. 자세한 내용은 [Set-AzureRmVMCustomScriptExtension](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension)을 참조하세요.
```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName myResourceGroup `
    -VMName myVM `
    -Location myLocation `
    -FileUri myURL `
    -Run 'myScript.ps1' `
    -Name DemoScriptExtension
```

## <a name="troubleshoot-and-support"></a>문제 해결 및 지원

### <a name="troubleshoot"></a>문제 해결

Hello Azure 포털에서에서 하 고 hello Azure PowerShell 모듈을 사용 하 여 확장 배포의 hello 상태에 대 한 데이터를 검색할 수 있습니다. hello 배포 상태를 toosee hello 다음 명령을 실행 하는 특정된 VM에 대 한 확장입니다.

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

확장 실행 기록된 toofiles hello 아래 팔 로우 디렉터리 hello 대상 가상 컴퓨터에 출력 합니다.
```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

hello는 hello hello 대상 가상 컴퓨터에 디렉터리를 다음으로 다운로드 되는 파일을 지정 합니다.
```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads\<n>
```
여기서 `<n>` hello 확장의 실행 간에 변경 될 수 있는 10 진수 정수.  hello `1.*` hello 실제, 현재 값이 일치 `typeHandlerVersion` hello 확장의 값입니다.  예를 들어, hello 실제 디렉터리 일 수 `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`합니다.  

Hello를 실행할 때 `commandToExecute` 명령,이 디렉터리 hello 확장 설정 됩니다 (예: `...\Downloads\2`) hello 현재 작업 디렉터리로 합니다. 상대 경로 toolocate hello 파일을 사용 하면 hello 사용이 hello를 통해 다운로드 `fileURIs` 속성입니다. 예제를 보려면 아래 hello 표를 참조 하십시오.

시간이 지남에 따라 다를 수 있습니다 hello 절대 다운로드 경로 이므로 hello 상대 스크립트/파일 경로 대 한 더 나은 tooopt `commandToExecute` 가능 하면 문자열입니다. 예:
```json
    "commandToExecute": "powershell.exe . . . -File './scripts/myscript.ps1'"
```

Hello를 통해 경로 정보 파일 hello 첫 번째 URI 세그먼트를 유지 한 후 다운로드 `fileUris` 속성 목록입니다.  다운로드 한 파일 다운로드의 hello tooreflect hello 구조 하위 디렉터리에 매핑된 hello 테이블 아래에 나와 있는 것 처럼 `fileUris` 값입니다.  

#### <a name="examples-of-downloaded-files"></a>다운로드된 파일의 예

| fileUris의 URI | 다운로드된 상대 위치 | 다운로드된 절대 위치* |
| ---- | ------- |:--- |
| `https://someAcct.blob.core.windows.net/aContainer/scripts/myscript.ps1` | `./scripts/myscript.ps1` |`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\scripts\myscript.ps1`  |
| `https://someAcct.blob.core.windows.net/aContainer/topLevel.ps1` | `./topLevel.ps1` | `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\topLevel.ps1` |

\*으로 hello CustomScript 확장의 단일 실행 내부가 아니라 hello VM의 hello 수명 주기 동안 위에서 hello 절대 디렉터리 경로 변경 합니다.

### <a name="support"></a>지원

이 문서에서 언제 든 지 자세한 도움말을 보려는 경우 문의할 수 있습니다 [MSDN Azure 및 스택 오버플로 포럼] hello에 Azure 전문가 hello (https://azure.microsoft.com/en-us/support/forums/). 또는 Azure 기술 지원 인시던트를 제출할 수 있습니다. Toohello 이동 [Azure 지원 사이트](https://azure.microsoft.com/en-us/support/options/) 지원 받기를 선택 합니다. Azure 지원을 사용 하는 방법에 대 한 내용은 하세요 hello [Microsoft Azure 지원 FAQ](https://azure.microsoft.com/en-us/support/faq/)합니다.
