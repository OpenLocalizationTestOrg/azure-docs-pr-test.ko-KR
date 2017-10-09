---
title: "Azure에서 Linux Vm에서 사용자 지정 스크립트 aaaRun | Microsoft Docs"
description: "사용자 지정 스크립트 확장 hello를 사용 하 여 Linux VM 구성 작업을 자동화 합니다."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cf17ab2b-8d7e-4078-b6df-955c6d5071c2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: f2c273a5fbd4cd1695aea48fa4bd08e691511e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-custom-script-extension-with-linux-virtual-machines"></a>Linux 가상 컴퓨터와 함께 hello Azure 사용자 지정 스크립트 확장을 사용 하 여
사용자 지정 스크립트 확장 hello 다운로드 하 고 Azure 가상 컴퓨터에서 스크립트를 실행 합니다. 이 확장은 배포 후 구성, 소프트웨어 설치 또는 기타 구성/관리 작업에 유용합니다. 스크립트는 Azure 저장소 또는 기타 액세스가 가능한 인터넷 위치에서 다운로드 또는 toohello 확장을 런타임에 제공 수 있습니다. 사용자 지정 스크립트 확장 hello Azure 리소스 관리자 템플릿 뿐 아니라 통합 하 고 hello Azure CLI, PowerShell, Azure 포털 또는 hello Azure 가상 컴퓨터 REST API를 사용 하 여 실행할 수도 있습니다.

이 문서 세부 정보를 어떻게 toouse hello에서 사용자 지정 스크립트 확장 Azure CLI 및 Azure 리소스 관리자 템플릿 및 문제 해결 단계는 Linux 시스템에서 세부 정보 hello 합니다.

## <a name="extension-configuration"></a>확장 구성
hello 사용자 지정 스크립트 확장 구성 스크립트 위치 및 실행 하는 hello 명령 toobe 등으로를 지정 합니다. 이 구성은 Azure 리소스 관리자 템플릿 또는 hello 명령줄에 지정 된 구성 파일에 저장할 수 있습니다. 암호화 되 고 hello 가상 컴퓨터 내의 암호를 해독할 보호 구성에서 중요 한 데이터를 저장할 수 있습니다. hello 보호 되는 구성 hello 실행 명령을 암호 등의 비밀 정보를 포함 하는 경우에 유용 합니다.

### <a name="public-configuration"></a>공용 구성
스키마:

**참고** - 이러한 속성 이름은 대/소문자를 구분합니다. 배포 문제 tooavoid 아래와 같이 hello 이름을 사용 합니다.

* **commandToExecute**: (문자열, 필요한) 항목 지점 스크립트 tooexecute hello
* **fileUris**: (선택 사항 문자열 배열) hello Url toobe 파일을 다운로드 합니다.
* **타임 스탬프** (선택 사항 정수)이이 필드의 값을 변경 하 여이 필드만 tootrigger hello 스크립트의 다시 실행을 사용 합니다.

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a>보호된 구성
스키마:

**참고** - 이러한 속성 이름은 대/소문자를 구분합니다. 배포 문제 tooavoid 아래와 같이 hello 이름을 사용 합니다.

* **commandToExecute**: (선택 사항, string) 항목 지점 스크립트 tooexecute hello 합니다. 명령에 암호와 같은 기밀 정보가 포함되는 경우 이 필드를 대신 사용합니다.
* **storageAccountName**: (선택 사항, string) hello 저장소 계정의 이름입니다. 저장소 자격 증명을 지정하는 경우 모든 fileUris는 Azure Blob에 대한 URL이어야 합니다.
* **storageAccountKey**: (선택 사항, string) hello 선택 키의 저장소 계정입니다.

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a>Azure CLI
Hello Azure CLI toorun hello 사용자 지정 스크립트 확장을 사용할 경우에 구성 파일 또는 최소 hello 파일 uri 및 hello 스크립트 실행 명령을 포함 하는 파일을 만듭니다.

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

필요에 따라 JSON 형식 문자열로 hello 설정은 hello 명령에 지정할 수 있습니다. 따라서 별도 구성 파일 없이도 실행 하는 동안 지정 된 hello 구성 toobe를 수 있습니다.

```azurecli
az vm extension set '
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],"commandToExecute": "./test.sh"}'
```

### <a name="azure-cli-examples"></a>Azure CLI 예제

**예제 1** - 스크립트 파일이 있는 공용 구성.

```json
{
  "fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],
  "commandToExecute": "./test.sh"
}
```

Azure CLI 명령:

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

**예제 2** - 스크립트 파일이 없는 공용 구성.

```json
{
  "commandToExecute": "apt-get -y update && apt-get install -y apache2"
}
```

Azure CLI 명령:

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

**예제 3** -공용 구성 파일이 사용 되는 toospecify hello 스크립트 파일 URI 및 보호 되는 구성 파일을 사용 하는 toospecify hello 명령 toobe 실행 합니다.

공용 구성 파일:

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"]
}
```

보호된 구성 파일:  

```json
{
  "commandToExecute": "./hello.sh <password>"
}
```

Azure CLI 명령:

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json --protected-settings ./protected-config.json
```

## <a name="resource-manager-template"></a>Resource Manager 템플릿
hello Azure 사용자 지정 스크립트 확장을 리소스 관리자 템플릿을 사용 하 여 가상 컴퓨터 배포 시간에 실행할 수 있습니다. toodo는, 적절 한 형식의 JSON toohello 배포 템플릿을 추가 합니다.

### <a name="resource-manager-examples"></a>Resource Manager 예제
**예제 1** - 공용 구성

```json
{
    "name": "scriptextensiondemo",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-15",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', parameters('scriptextensiondemoName'))]"
    ],
    "tags": {
        "displayName": "scriptextensiondemo"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Extensions",
        "type": "CustomScript",
        "typeHandlerVersion": "2.0",
        "autoUpgradeMinorVersion": true,
      "settings": {
        "fileUris": [
          "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
        ],
        "commandToExecute": "sh hello.sh"
      }
    }
}
```

**예제 2** - 보호된 구성의 실행 명령.

```json
{
  "name": "config-app",
  "type": "extensions",
  "location": "[resourceGroup().location]",
  "apiVersion": "2015-06-15",
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
        "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
      ]              
    },
    "protectedSettings": {
      "commandToExecute": "sh hello.sh <password>"
    }
  }
}
```

Hello.Net Core Music Store 참조는 전체 예제-데모 [음악 스토어 데모](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db)합니다.

## <a name="troubleshooting"></a>문제 해결
Hello 사용자 지정 스크립트 확장이 실행 되 면 hello 스크립트를 만들거나 다음 예제에서는 디렉터리 비슷한 toohello에 다운로드 합니다. hello 명령 출력에서이 디렉터리에도 저장 `stdout` 및 `stderr` 파일입니다.

```bash
/var/lib/waagent/custom-script/download/0/
```

hello Azure 스크립트 확장을 찾아볼 수 있는 로그를 생성 합니다.

```bash
/var/log/azure/custom-script/handler.log
```

hello Azure CLI로 hello 사용자 지정 스크립트 확장의 hello 실행 상태를 검색할 수도 있습니다.

```azurecli
az vm extension list -g myResourceGroup --vm-name myVM
```

hello 출력 텍스트 다음 hello와 같습니다.

```azurecli
info:    Executing command vm extension get
+ Looking up hello VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a>다음 단계
다른 VM 스크립트 확장에 대한 자세한 내용은 [Linux용 Azure 스크립트 확장 개요](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.

