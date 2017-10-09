---
title: "aaaVirtual 확장 및 기능을 Windows azure에서에 대 한 기계 | Microsoft Docs"
description: "확장이 제공하거나 개선하는 기능별로 그룹화하여 Azure 가상 컴퓨터에 사용할 수 있는 확장을 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 999d63ee-890e-432e-9391-25b3fc6cde28
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/06/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 61ccfd696b38e9be1026d836d5796c2346fd650f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-windows"></a>Windows용 가상 컴퓨터 확장 및 기능

Azure Virtual Machines 확장은 Azure Virtual Machines에서 배포 후 구성 및 Automation 작업을 제공하는 작은 응용 프로그램입니다. 예를 들어 가상 컴퓨터는 소프트웨어 설치, 바이러스 방지 또는 Docker 구성에 필요한 경우 VM 확장 수 toocomplete 사용 되는 이러한 작업을 수 있습니다. Azure VM 확장 hello Azure CLI, PowerShell, Azure 리소스 관리자 템플릿 사용 하 여 실행할 수 있으며 Azure 포털 hello 합니다. 확장을 새 가상 컴퓨터 배포와 번들로 제공하거나 기존 시스템에 대해 실행할 수 있습니다.

이 문서에서는 가상 컴퓨터 확장을 가상 컴퓨터 확장 및 지침을 사용 하 여 toodetect를 관리 하 고 가상 컴퓨터 확장을 제거 하는 방법에 대 한 필수 구성 요소에 대 한 개요를 제공 합니다. 많은 VM 확장 각각을 고유한 구성으로 사용할 수 있으므로 여기서는 일반적인 정보를 제공합니다. 각 문서 특정 toohello 개별 확장에서 확장 관련 세부 정보를 찾을 수 있습니다.

## <a name="use-cases-and-samples"></a>사용 사례 및 샘플

각각 특정 사용 사례가 있는 많은 다양한 Azure VM 확장을 사용할 수 있습니다. 예제 사용 사례:

- Windows 용 hello DSC 확장을 사용 하 여 PowerShell 원하는 상태 구성 tooa 가상 컴퓨터를 적용 합니다. 자세한 내용은 [Azure 필요한 상태 구성 확장](extensions-dsc-overview.md)을 참조하세요.
- Hello Microsoft 모니터링 에이전트 VM 확장을 사용 하 여 가상 컴퓨터 모니터링을 구성 합니다. 자세한 내용은 참조 [연결 Azure 가상 컴퓨터 tooLog 분석](../../log-analytics/log-analytics-azure-vm-extension.md)합니다.
- Hello Datadog 확장으로 Azure 인프라의 모니터링을 구성 합니다. 자세한 내용은 참조 hello [Datadog 블로그](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/)합니다.
- Chef를 사용하여 Azure Virtual Machine을 구성합니다. 자세한 내용은 [Chef를 사용하여 Azure 가상 컴퓨터 배포 자동화](chef-automation.md)를 참조하세요.

또한 tooprocess 전용 확장 사용자 지정 스크립트 확장은 Windows와 Linux 가상 컴퓨터에 사용할 수 있습니다. Windows에 대 한 사용자 지정 스크립트 확장 hello 모든 PowerShell 스크립트 toobe를 가상 컴퓨터에서 실행할 수 있습니다. 이 확장은 네이티브 Azure 도구로 제공할 수 있는 것 이상의 구성이 필요한 Azure 배포를 디자인할 때 유용합니다. 자세한 내용은 [Windows VM 사용자 지정 스크립트 확장](extensions-customscript.md)을 참조하세요.


## <a name="prerequisites"></a>필수 조건

각 가상 컴퓨터 확장에는 고유한 필수 구성 요소 집합이 있을 수 있습니다. 예를 들어 hello Docker VM 확장에 지원 되는 Linux 배포판의 필수 구성 요소를 있습니다. 개별 확장의 요구 사항은 hello 확장 프로그램별 설명서에 자세히 설명 합니다.

### <a name="azure-vm-agent"></a>Azure VM 에이전트
hello Azure VM 에이전트는 Azure 가상 컴퓨터와 hello Azure 패브릭 컨트롤러 간의 상호 작용을 관리합니다. hello VM 에이전트는 업무의 다양 한 VM 확장을 실행 하는 포함 하 여 Azure 가상 컴퓨터 배포 및 관리 합니다. hello Azure VM 에이전트는 Azure 마켓플레이스 이미지에 사전 설치 하 고 지원 되는 운영 체제에 설치할 수 있습니다.

지원되는 운영 체제 및 설치 지침에 대한 자세한 내용은 [Azure Virtual Machines 에이전트](agent-user-guide.md)를 참조하세요.

## <a name="discover-vm-extensions"></a>VM 확장 검색
Azure Virtual Machine와 함께 여러 다양한 VM 확장을 사용할 수 있습니다. toosee 전체 목록 보려면 다음 명령을 hello Azure 리소스 관리자 PowerShell 모듈과 함께 hello를 실행 합니다. 이 명령을 실행 하는 경우 있는지 toospecify hello 원하는 위치를 확인 합니다.

```powershell
Get-AzureRmVmImagePublisher -Location WestUS | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```

## <a name="run-vm-extensions"></a>VM 확장 실행

Azure 가상 컴퓨터 확장 toomake 구성 변경 내용이 필요 하거나 이미 배포 된 VM에서 연결을 복구 하는 경우 유용 기존 가상 컴퓨터에서 실행할 수 있습니다. 또한 VM 확장을 Azure Resource Manager 템플릿 배포와 번들로 묶을 수도 있습니다. 확장을 리소스 관리자 템플릿으로 사용 하 여 배포 하 고 hello 배포 후가 개입할 필요 없이 구성 된 Azure 가상 컴퓨터 toobe를 사용할 수 있습니다.

메서드를 다음 hello 사용된 toorun 기존 가상 컴퓨터에 대해 확장 될 수 있습니다.

### <a name="powershell"></a>PowerShell

개별 확장을 실행하기 위한 몇 가지 PowerShell 명령이 존재합니다. toosee 목록 hello 다음 PowerShell 명령을 실행 합니다.

```powershell
get-command Set-AzureRM*Extension* -Module AzureRM.Compute
```

이 출력 유사한 toohello 다음을 제공합니다.

```powershell
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Set-AzureRmVMAccessExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMADDomainExtension                     2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMAEMExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBackupExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBginfoExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMChefExtension                         2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMCustomScriptExtension                 2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiagnosticsExtension                  2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiskEncryptionExtension               2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDscExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMExtension                             2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMSqlServerExtension                    2.2.0      AzureRM.Compute
```

hello 다음 예제에서는 hello 사용자 지정 스크립트 확장 toodownload 스크립트를 사용 하 여 hello 대상 가상 컴퓨터에 GitHub 리포지토리 및 hello 스크립트를 실행 합니다. 사용자 지정 스크립트 확장 hello에 대 한 자세한 내용은 참조 하십시오. [사용자 지정 스크립트 확장 개요](extensions-customscript.md)합니다.

```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" -Name "myCustomScript" `
    -FileUri "https://raw.githubusercontent.com/neilpeterson/nepeters-azure-templates/master/windows-custom-script-simple/support-scripts/Create-File.ps1" `
    -Run "Create-File.ps1" -Location "West US"
```

이 예제에서는 hello VM 액세스 확장에는 Windows 가상 컴퓨터의 사용 되는 tooreset hello 관리자 암호입니다. VM 액세스 확장 hello에 대 한 자세한 내용은 참조 하십시오. [Windows VM의 다시 설정 원격 데스크톱 서비스](reset-rdp.md)합니다.

```powershell
$cred=Get-Credential

Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" -Name "myVMAccess" `
    -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

hello `Set-AzureRmVMExtension` 명령을 사용 하는 toostart 서비스나 VM 확장 될 수 있습니다. 자세한 내용은 참조 hello [집합 AzureRmVMExtension 참조](https://msdn.microsoft.com/en-us/library/mt603745.aspx)합니다.


### <a name="azure-portal"></a>Azure portal

VM 확장 hello Azure 포털을 통해 적용 된 tooan 기존 가상 컴퓨터를 수 있습니다. toodo hello 가상 컴퓨터를 선택, toouse 원하는 선택 **확장**를 클릭 하 고 **추가**합니다. 그러면 사용 가능한 확장 목록이 제공됩니다. Hello 및 hello 마법사에서 hello 단계에 따라 하나를 선택 합니다.

hello 다음 이미지에서는 hello 설치 hello hello Azure 포털에서에서 Microsoft 맬웨어 방지 확장 합니다.

![Install antimalware extension](./media/extensions-features/installantimalwareextension.png)

### <a name="azure-resource-manager-templates"></a>Azure 리소스 관리자 템플릿

VM 확장 추가 tooan Azure 리소스 관리자 템플릿 수 및 hello 템플릿의 hello 배포를 사용 하 여 실행 합니다. 템플릿 사용하여 확장을 배포하는 방식은 완전히 구성된 Azure 배포를 만드는 데 유용합니다. 다음 JSON에서 부하 분산 된 가상 컴퓨터 및 Azure SQL 데이터베이스의 집합을 배포 하 고 다음 각 VM에는.NET Core 응용 프로그램을 설치 하는 리소스 관리자 템플릿을 가져옵니다 hello 예를 들어 있습니다. VM 확장 hello hello 소프트웨어 설치 처리합니다.

자세한 내용은 참조 hello [전체 리소스 관리자 템플릿](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)합니다.

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
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

자세한 내용은 [Windows VM 확장을 사용하여 Azure Resource Manager 템플릿 작성](template-description.md#extensions)을 참조하세요.

## <a name="secure-vm-extension-data"></a>VM 확장 데이터 보호

VM 확장을 실행 하는 경우 자격 증명, 저장소 계정 이름과 저장소 계정 액세스 키와 같은 중요 한 정보가 필요한 tooinclude 수 있습니다. 많은 VM 확장 데이터를 암호화 하 고만 hello 대상 가상 컴퓨터 내 해독 하는 보호 된 구성을 포함 합니다. 각 확장에는 보호되는 특정 구성 스키마가 있으며 각각은 확장 관련 설명서에 자세히 나와 있습니다.

다음 예제는 hello Windows hello 사용자 지정 스크립트 확장의 인스턴스를 보여 줍니다. Hello 명령 tooexecute 해당 자격 증명 집합이 포함 되어 확인 합니다. 이 예제에서는 hello 명령 tooexecute 암호화 되지 않습니다.


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
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ],
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

보안 hello 실행 문자열 hello를 이동 하 여 **명령 tooexecute** 속성 toohello **보호** 구성 합니다.

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
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

## <a name="troubleshoot-vm-extensions"></a>VM 확장 문제 해결

각 VM 확장에는 특정 문제 해결 단계가 있을 수 있습니다. 예를 들어 hello 사용자 지정 스크립트 확장을 사용 하는 경우 스크립트 실행 세부 사항은 있습니다 로컬로 hello 확장 실행 된 hello 가상 컴퓨터. 확장별 문제 해결 단계는 확장 관련 설명서에 자세히 나와 있습니다.

문제 해결 단계를 수행 하는 hello tooall 가상 컴퓨터 확장을 적용 합니다.

### <a name="view-extension-status"></a>확장 상태 보기

가상 컴퓨터 확장을 가상 컴퓨터에 대해 실행 한 후 다음 PowerShell 명령을 tooreturn 확장 상태 hello를 사용 합니다. 매개 변수 이름을 고유한 값으로 바꿉니다. hello `Name` 매개 변수는 실행 시 toohello 확장을 지정 하는 hello 이름입니다.

```PowerShell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

hello 출력 hello 다음과 같습니다.

```json
ResourceGroupName       : myResourceGroup
VMName                  : myVM
Name                    : myExtensionName
Location                : westus
Etag                    : null
Publisher               : Microsoft.Azure.Extensions
ExtensionType           : DockerExtension
TypeHandlerVersion      : 1.0
Id                      : /subscriptions/mySubscriptionIS/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM/extensions/myExtensionName
PublicSettings          :
ProtectedSettings       :
ProvisioningState       : Succeeded
Statuses                :
SubStatuses             :
AutoUpgradeMinorVersion : False
ForceUpdateTag          :
```

Hello Azure 포털에서에서 확장 실행 상태를 찾을 수도 있습니다. 확장을 선택 하는 hello 가상 컴퓨터의 tooview hello 상태 선택 **확장**, 선택 hello 원하는 확장 프로그램 및입니다.

### <a name="rerun-vm-extensions"></a>VM 확장 다시 실행

가상 컴퓨터 확장 toobe 해야 하는 경우 있을 수 있습니다를 다시 실행 하십시오. Hello 확장을 제거한 다음 원하는 실행 메서드에 hello 확장을 다시 실행 하 여이 수행할 수 있습니다. tooremove 확장을 hello 다음 hello Azure PowerShell 모듈을 사용 하 여 명령을 실행 합니다. 매개 변수 이름을 고유한 값으로 바꿉니다.

```powershell
Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

확장은 hello Azure 포털을 사용 하 여 제거할 수 있습니다. toodo 하므로:

1. 가상 컴퓨터를 선택합니다.
2. **확장**을 섡택합니다.
3. Hello 필요한 확장 프로그램을 선택 합니다.
4. **제거**를 선택합니다.

## <a name="common-vm-extensions-reference"></a>일반 VM 확장 참조
| 확장 이름 | 설명 | 자세한 정보 |
| --- | --- | --- |
| Windows용 사용자 지정 스크립트 확장 |Azure Virtual Machine에 대해 스크립트 실행 |[Windows용 사용자 지정 스크립트 확장](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Windows용 DSC 확장 |PowerShell DSC(Desired State Configuration) 확장 |[Windows용 DSC 확장](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Azure 진단 확장 |Azure 진단 관리 |[Azure 진단 확장](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| Azure VM 액세스 확장 |사용자 및 자격 증명 관리 |[Linux용 VM 액세스 확장](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
