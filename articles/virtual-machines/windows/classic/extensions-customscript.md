---
title: "Windows VM에서 스크립트 확장 aaaCustom | Microsoft Docs"
description: "원격 Windows VM에서 hello 사용자 지정 스크립트 확장 toorun PowerShell 스크립트를 사용 하 여 Azure VM 구성 작업을 자동화 합니다."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: ebb7340a-8f61-4d3c-a290-d7bf8de2d0bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: nepeters
ms.openlocfilehash: cf7bb895dd211f07fd010dc03b68cd77df1127b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows-using-hello-classic-deployment-model"></a>사용자 지정 스크립트 확장에 대 한 Windows hello 클래식 배포 모델을 사용 하 여

> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. 너무 방법에 대해 알아봅니다[hello 리소스 관리자 모델을 사용 하 여 이러한 단계를 수행](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

사용자 지정 스크립트 확장 hello 다운로드 하 고 Azure 가상 컴퓨터에서 스크립트를 실행 합니다. 이 확장은 배포 후 구성, 소프트웨어 설치 또는 기타 구성/관리 작업에 유용합니다. 스크립트는 Azure 저장소 또는 GitHub에서 다운로드 또는 toohello Azure 포털 확장 실행 시간에 제공 수 있습니다. 사용자 지정 스크립트 확장 hello Azure 리소스 관리자 템플릿 뿐 아니라 통합 하 고 hello Azure CLI, PowerShell, Azure 포털 또는 hello Azure 가상 컴퓨터 REST API를 사용 하 여 실행할 수도 있습니다.

이 문서는 Azure PowerShell 모듈, Azure 리소스 관리자 템플릿 및 문제 해결 단계는 Windows 시스템에서 세부 정보 어떻게 hello toouse hello 사용자 지정 스크립트 확장을 사용 하 여 자세히 설명 합니다.

## <a name="prerequisites"></a>필수 조건

### <a name="operating-system"></a>운영 체제

사용자 지정 스크립트 확장 hello Windows Server 2008 r 2에 대해 Windows를 실행할 수에 대 한 2016, R2, 2012 및 2012를 해제 합니다.

### <a name="script-location"></a>스크립트 위치

hello 스크립트 toobe Azure 저장소 또는 올바른 URL을 통해 액세스할 수 있는 기타 위치에 저장 해야 합니다.

### <a name="internet-connectivity"></a>인터넷 연결

hello Windows에 대 한 사용자 지정 스크립트 확장에서는 해당 hello 대상 가상 컴퓨터가 연결 된 toohello 인터넷 합니다. 

## <a name="extension-schema"></a>확장 스키마

hello 다음 JSON hello 스키마를 표시 사용자 지정 스크립트 확장이 hello에 대 한 합니다. hello 확장 (Azure 저장소 또는 올바른 URL 사용 하 여 다른 위치) 스크립트 위치 및 명령 tooexecute 필요합니다. Azure 저장소 hello 스크립트 원본으로 사용 하는 경우 Azure 저장소 계정 이름 및 계정 키가 필요 합니다. 이러한 항목으로 중요 한 데이터를 처리 하 고 hello 확장 보호 설정 구성에 지정 해야 합니다. Azure VM 확장으로 보호 된 데이터를 설정 하는 암호화 되 고 hello 대상 가상 컴퓨터에 암호를 해독할 됩니다.

```json
{
    "name": "config-app",
    "type": "Microsoft.ClassicCompute/virtualMachines/extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-01",
    "properties": {
        "publisher": "Microsoft.Compute",
        "extension": "CustomScriptExtension",
        "version": "1.8",
        "parameters": {
            "public": {
                "fileUris": "[myScriptLocation]"
            },
            "private": {
                "commandToExecute": "[myExecutionString]"
            }
        }
    }
}
```

### <a name="property-values"></a>속성 값

| 이름 | 값/예제 |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publisher | Microsoft.Compute |
| 확장 | CustomScriptExtension |
| typeHandlerVersion | 1.8 |
| fileUris(예) | https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1 |
| commandToExecute(예) | powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 |

## <a name="template-deployment"></a>템플릿 배포

Azure Resource Manager 템플릿을 사용하여 Azure VM 확장을 배포할 수 있습니다. Azure 리소스 관리자 템플릿 배포 중에 Azure 리소스 관리자 템플릿 toorun hello 사용자 지정 스크립트 확장 hello 이전 섹션에서 자세히 설명 하는 hello JSON 스키마를 사용할 수 있습니다. 사용자 지정 스크립트 확장을 여기에서 찾을 수 hello를 포함 하는 샘플 템플릿을 [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)합니다.

## <a name="powershell-deployment"></a>PowerShell 배포

hello `Set-AzureVMCustomScriptExtension` 명령을 사용 하는 tooadd hello 사용자 지정 스크립트 확장 tooan 기존 가상 컴퓨터 수 있습니다. 자세한 내용은 [Set-AzureRmVMCustomScriptExtension](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension)을 참조하세요.

```powershell
# create vm object
$vm = Get-AzureVM -Name 2016clas -ServiceName 2016clas1313

# set extension
Set-AzureVMCustomScriptExtension -VM $vm -FileUri myFileUri -Run 'create-file.ps1'

# update vm
$vm | Update-AzureVM
```

## <a name="troubleshoot-and-support"></a>문제 해결 및 지원

### <a name="troubleshoot"></a>문제 해결

Hello Azure 포털에서에서 하 고 hello Azure PowerShell 모듈을 사용 하 여 확장 배포의 hello 상태에 대 한 데이터를 검색할 수 있습니다. hello 배포 상태를 toosee hello 다음 명령을 실행 하는 특정된 VM에 대 한 확장입니다.

```powershell
Get-AzureVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

확장 실행 우리 로깅된 toofiles hello hello 대상 가상 컴퓨터에 디렉터리를 다음에 출력 합니다.

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

hello 스크립트 자체는 hello 나오는 hello 대상 가상 컴퓨터에 디렉터리에 다운로드 됩니다.

```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads
```

### <a name="support"></a>지원

이 문서에서 언제 든 지 자세한 도움말을 보려는 경우 문의할 수 있습니다 Azure 전문가의 hello hello [MSDN Azure 및 스택 오버플로 포럼](https://azure.microsoft.com/en-us/support/forums/)합니다. 또는 Azure 기술 지원 인시던트를 제출할 수 있습니다. Toohello 이동 [Azure 지원 사이트](https://azure.microsoft.com/en-us/support/options/) 지원 받기를 선택 합니다. Azure 지원을 사용 하는 방법에 대 한 내용은 하세요 hello [Microsoft Azure 지원 FAQ](https://azure.microsoft.com/en-us/support/faq/)합니다.
