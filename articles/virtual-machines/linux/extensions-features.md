---
title: "aaaVirtual Linux에 대 한 확장 및 기능 기계 | Microsoft Docs"
description: "확장이 제공하거나 개선하는 기능별로 그룹화하여 Azure 가상 컴퓨터에 사용할 수 있는 확장을 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 52f5d0ec-8f75-49e7-9e15-88d46b420e63
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: e0d2ce794c76815ccc6743e8788ee5d9d931e9a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-linux"></a>Linux용 가상 컴퓨터 확장 및 기능

Azure Virtual Machines 확장은 Azure Virtual Machines에서 배포 후 구성 및 Automation 작업을 제공하는 작은 응용 프로그램입니다. 예를 들어 가상 컴퓨터는 소프트웨어 설치, 바이러스 방지 또는 Docker 구성에 필요한 경우 VM 확장 수 toocomplete 사용 되는 이러한 작업을 수 있습니다. Azure VM 확장 hello Azure CLI, PowerShell, Azure 리소스 관리자 템플릿 사용 하 여 실행할 수 있으며 Azure 포털 hello 합니다. 확장을 새 가상 컴퓨터 배포와 번들로 제공하거나 기존 시스템에 대해 실행할 수 있습니다.

이 문서에서는 VM 확장을 Azure VM 확장 및 지침을 사용 하 여 toodetect를 관리 하 고 VM 확장을 제거 하는 방법에 대 한 필수 구성 요소에 대 한 개요를 제공 합니다. 많은 VM 확장 각각을 고유한 구성으로 사용할 수 있으므로 여기서는 일반적인 정보를 제공합니다. 각 문서 특정 toohello 개별 확장에서 확장 관련 세부 정보를 찾을 수 있습니다.

## <a name="use-cases-and-samples"></a>사용 사례 및 샘플

각각 특정 사용 사례가 있는 몇 가지 다른 Azure VM 확장을 사용할 수 있습니다. 일부 사례:

- Linux 용 DSC 확장 hello를 사용 하는 PowerShell 원하는 상태 구성 tooa 가상 컴퓨터를 적용 합니다. 자세한 내용은 [Azure 필요한 상태 구성 확장](https://github.com/Azure/azure-linux-extensions/tree/master/DSC)을 참조하세요.
- Microsoft 모니터링 에이전트 VM 확장 hello로 가상 컴퓨터의 모니터링을 구성 합니다. 자세한 내용은 참조 [어떻게 toomonitor Linux VM](tutorial-monitoring.md)합니다.
- Hello Datadog 확장으로 Azure 인프라의 모니터링을 구성 합니다. 자세한 내용은 참조 hello [Datadog 블로그](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/)합니다.
- Hello Docker VM 확장을 사용 하 여 Azure 가상 컴퓨터에 Docker 호스트를 구성 합니다. 자세한 내용은 [Docker VM 확장](dockerextension.md)을 참조하세요.

또한 tooprocess 전용 확장 사용자 지정 스크립트 확장은 Windows와 Linux 가상 컴퓨터에 사용할 수 있습니다. Linux 용 사용자 지정 스크립트 확장 hello 모든 Bash 스크립트 toobe를 가상 컴퓨터에서 실행할 수 있습니다. 사용자 지정 스크립트는 네이티브 Azure 도구로 제공할 수 있는 것 이상의 구성이 필요한 Azure 배포를 디자인할 때 유용합니다. 자세한 내용은 [Linux VM 사용자 지정 스크립트 확장](extensions-customscript.md)을 참조하세요.


## <a name="prerequisites"></a>필수 조건

각 가상 컴퓨터 확장에는 고유한 필수 구성 요소 집합이 있을 수 있습니다. 예를 들어 hello Docker VM 확장에 지원 되는 Linux 배포판의 필수 구성 요소를 있습니다. 개별 확장의 요구 사항은 hello 확장 프로그램별 설명서에 자세히 설명 합니다.

### <a name="azure-vm-agent"></a>Azure VM 에이전트

hello Azure VM 에이전트는 Azure 가상 컴퓨터와 hello Azure 패브릭 컨트롤러 간의 상호 작용을 관리 합니다. hello VM 에이전트는 업무의 다양 한 VM 확장을 실행 하는 포함 하 여 Azure 가상 컴퓨터 배포 및 관리 합니다. hello Azure VM 에이전트는 Azure 마켓플레이스 이미지에 사전 설치 하 고 지원 되는 운영 체제에 수동으로 설치할 수 있습니다.

지원되는 운영 체제 및 설치 지침에 대한 자세한 내용은 [Azure Virtual Machines 에이전트](../windows/classic/agents-and-extensions.md)를 참조하세요.

## <a name="discover-vm-extensions"></a>VM 확장 검색

Azure Virtual Machine와 함께 여러 다양한 VM 확장을 사용할 수 있습니다. toosee 전체 목록 보려면 다음 명령을 hello Azure CLI로, 사용자가 선택한 hello 위치와 hello 예제 위치 대체 hello를 실행 합니다.

```azurecli
az vm extension image list --location westus -o table
```

## <a name="run-vm-extensions"></a>VM 확장 실행

toomake 구성 변경 내용이 필요 하거나 이미 배포 된 VM에서 연결을 복구 하는 경우에 유용 하는 기존 가상 컴퓨터에 azure 가상 컴퓨터 확장을 실행할 수 있습니다. 또한 VM 확장을 Azure Resource Manager 템플릿 배포와 번들로 묶을 수도 있습니다. Resource Manager 템플릿에서 확장을 사용하면 Azure Virtual Machine을 배포하고, 배포 후 개입 없이 구성할 수 있습니다.

메서드를 다음 hello 사용된 toorun 기존 가상 컴퓨터에 대해 확장 될 수 있습니다.

### <a name="azure-cli"></a>Azure CLI

Azure 가상 컴퓨터 확장 hello를 사용 하 여 기존 가상 컴퓨터에 대해 실행할 수 `az vm extension set` 명령입니다. 이 예제에서는 가상 컴퓨터에 대 한 hello 사용자 지정 스크립트 확장을 실행 합니다.

```azurecli
az vm extension set `
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

스크립트 생성 출력 유사한 toohello 텍스트 다음 hello:

```azurecli
info:    Executing command vm extension set
+ Looking up hello VM "myVM"
+ Installing extension "CustomScript", VM: "mvVM"
info:    vm extension set command OK
```

### <a name="azure-portal"></a>Azure portal

VM 확장 hello Azure 포털을 통해 적용 된 tooan 기존 가상 컴퓨터를 수 있습니다. toodo hello 가상 컴퓨터를를 따라서 선택 선택 **확장**를 클릭 하 고 **추가**합니다. Hello 사용 가능한 확장 목록에서 원하는 및 hello 마법사 지시에에서 따라 hello hello 확장을 선택 합니다.

hello 다음 이미지에서는 hello 설치 hello hello Azure 포털에서에서 Linux 사용자 지정 스크립트 확장 합니다.

![Install custom script extension](./media/extensions-features/installscriptextensionlinux.png)

### <a name="azure-resource-manager-templates"></a>Azure 리소스 관리자 템플릿

VM 확장 추가 tooan Azure 리소스 관리자 템플릿 수 및 hello 템플릿의 hello 배포를 사용 하 여 실행 합니다. 템플릿을 사용하여 확장을 배포할 때 완전히 구성된 Azure 배포를 만들 수 있습니다. 예를 들어 다음 JSON hello은 리소스 관리자 템플릿을에서 가져옵니다. hello 템플릿 집합을 부하 분산 된 가상 컴퓨터와 Azure SQL 데이터베이스를 배포 하 고 각 VM에서.NET Core 응용 프로그램을 설치 합니다. VM 확장 hello hello 소프트웨어 설치 처리합니다.

자세한 내용은 참조 hello 전체 [리소스 관리자 템플릿](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux)합니다.

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
    }
}
```

자세한 내용은 [Azure Resource Manager 템플릿 작성](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions)을 참조하세요.

## <a name="secure-vm-extension-data"></a>VM 확장 데이터 보호

VM 확장을 실행 하는 경우 자격 증명, 저장소 계정 이름과 저장소 계정 액세스 키와 같은 중요 한 정보가 필요한 tooinclude 수 있습니다. 많은 VM 확장 데이터를 암호화 하 고만 hello 대상 가상 컴퓨터 내 해독 하는 보호 된 구성을 포함 합니다. 각 확장에는 보호되는 특정 구성 스키마가 있으며 각각은 확장 관련 설명서에 자세히 나와 있습니다.

다음 예제는 hello Linux에 대 한 사용자 지정 스크립트 확장 hello의 인스턴스를 보여 줍니다. Hello 명령 tooexecute 해당 자격 증명 집합이 포함 되어 확인 합니다. 이 예제에서는 hello 명령 tooexecute 암호화 되지 않습니다.


```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ],
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

이동 hello **명령 tooexecute** 속성 toohello **보호** 구성 hello 실행 문자열을 보호 합니다.

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

## <a name="troubleshoot-vm-extensions"></a>VM 확장 문제 해결

각 VM 확장 단계 특정 toohello 확장 문제 해결 있을 수 있습니다. 예를 들어 hello 사용자 지정 스크립트 확장을 사용 하는 경우 스크립트 실행 세부 사항은 있습니다 로컬로 hello 확장 실행 된 hello 가상 컴퓨터. 확장별 문제 해결 단계는 확장 관련 설명서에 자세히 나와 있습니다.

문제 해결 단계를 수행 하는 hello tooall 가상 컴퓨터 확장을 적용 합니다.

### <a name="view-extension-status"></a>확장 상태 보기

가상 컴퓨터 확장을 가상 컴퓨터에 대해 실행 한 후 다음 Azure CLI 명령을 tooreturn 확장 상태 hello를 사용 합니다. 매개 변수 이름을 고유한 값으로 바꿉니다.

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

hello 출력 텍스트 다음 hello와 같습니다.

```azurecli
AutoUpgradeMinorVersion    Location    Name          ProvisioningState    Publisher                   ResourceGroup      TypeHandlerVersion  VirtualMachineExtensionType
-------------------------  ----------  ------------  -------------------  --------------------------  ---------------  --------------------  -----------------------------
True                       westus      customScript  Succeeded            Microsoft.Azure.Extensions  exttest                             2  customScript
```

Hello Azure 포털에서에서 확장 실행 상태를 찾을 수도 있습니다. 확장을 선택 하는 hello 가상 컴퓨터의 tooview hello 상태 선택 **확장**, 선택 hello 원하는 확장 프로그램 및입니다.

### <a name="rerun-a-vm-extension"></a>VM 확장 다시 실행

가상 컴퓨터 확장 toobe 해야 하는 경우 있을 수 있습니다를 다시 실행 하십시오. 제거한 다음 원하는 실행 메서드에 hello 확장을 다시 실행 하 여 확장을 다시 실행할 수 있습니다. tooremove 확장을 hello 다음 Azure CLI hello로 명령을 실행 합니다. 매개 변수 이름을 고유한 값으로 바꿉니다.

```azurecli
az vm extension delete --name customScript --resource-group myResourceGroup --vm-name myVM
```

Hello Azure 포털의에서 단계를 실행 하는 hello를 사용 하 여 확장을 제거할 수 있습니다.

1. 가상 컴퓨터를 선택합니다.
2. **확장**을 선택합니다.
3. Hello 필요한 확장을 선택 합니다.
4. **제거**를 선택합니다.

## <a name="common-vm-extension-reference"></a>일반적인 VM 확장 참조
| 확장 이름 | 설명 | 자세한 정보 |
| --- | --- | --- |
| Linux용 사용자 지정 스크립트 확장 |Azure Virtual Machine에 대해 스크립트 실행 |[Linux용 사용자 지정 스크립트 확장](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| Docker 확장 |Hello Docker 디먼 toosupport 원격 Docker 명령을 설치 합니다. |[Docker VM 확장](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| VM 액세스 확장 |액세스 tooan Azure 가상 컴퓨터를 다시 가져오기 |[VM 액세스 확장](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) |
| Azure 진단 확장 |Azure 진단 관리 |[Azure 진단 확장](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| Azure VM 액세스 확장 |사용자 및 자격 증명 관리 |[Linux용 VM 액세스 확장](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
