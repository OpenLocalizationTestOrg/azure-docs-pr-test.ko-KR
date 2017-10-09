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
# <a name="using-hello-azure-custom-script-extension-with-linux-virtual-machines"></a><span data-ttu-id="02dec-103">Linux 가상 컴퓨터와 함께 hello Azure 사용자 지정 스크립트 확장을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="02dec-103">Using hello Azure Custom Script Extension with Linux Virtual Machines</span></span>
<span data-ttu-id="02dec-104">사용자 지정 스크립트 확장 hello 다운로드 하 고 Azure 가상 컴퓨터에서 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-104">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="02dec-105">이 확장은 배포 후 구성, 소프트웨어 설치 또는 기타 구성/관리 작업에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="02dec-106">스크립트는 Azure 저장소 또는 기타 액세스가 가능한 인터넷 위치에서 다운로드 또는 toohello 확장을 런타임에 제공 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-106">Scripts can be downloaded from Azure storage or other accessible internet location, or provided toohello extension run time.</span></span> <span data-ttu-id="02dec-107">사용자 지정 스크립트 확장 hello Azure 리소스 관리자 템플릿 뿐 아니라 통합 하 고 hello Azure CLI, PowerShell, Azure 포털 또는 hello Azure 가상 컴퓨터 REST API를 사용 하 여 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-107">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="02dec-108">이 문서 세부 정보를 어떻게 toouse hello에서 사용자 지정 스크립트 확장 Azure CLI 및 Azure 리소스 관리자 템플릿 및 문제 해결 단계는 Linux 시스템에서 세부 정보 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-108">This document details how toouse hello Custom Script Extension from hello Azure CLI, and an Azure Resource Manager template, and also details troubleshooting steps on Linux systems.</span></span>

## <a name="extension-configuration"></a><span data-ttu-id="02dec-109">확장 구성</span><span class="sxs-lookup"><span data-stu-id="02dec-109">Extension Configuration</span></span>
<span data-ttu-id="02dec-110">hello 사용자 지정 스크립트 확장 구성 스크립트 위치 및 실행 하는 hello 명령 toobe 등으로를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-110">hello Custom Script Extension configuration specifies things like script location and hello command toobe run.</span></span> <span data-ttu-id="02dec-111">이 구성은 Azure 리소스 관리자 템플릿 또는 hello 명령줄에 지정 된 구성 파일에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-111">This configuration can be stored in configuration files, specified on hello command line, or in an Azure Resource Manager template.</span></span> <span data-ttu-id="02dec-112">암호화 되 고 hello 가상 컴퓨터 내의 암호를 해독할 보호 구성에서 중요 한 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-112">Sensitive data can be stored in a protected configuration, which is encrypted and only decrypted inside hello virtual machine.</span></span> <span data-ttu-id="02dec-113">hello 보호 되는 구성 hello 실행 명령을 암호 등의 비밀 정보를 포함 하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-113">hello protected configuration is useful when hello execution command includes secrets such as a password.</span></span>

### <a name="public-configuration"></a><span data-ttu-id="02dec-114">공용 구성</span><span class="sxs-lookup"><span data-stu-id="02dec-114">Public Configuration</span></span>
<span data-ttu-id="02dec-115">스키마:</span><span class="sxs-lookup"><span data-stu-id="02dec-115">Schema:</span></span>

<span data-ttu-id="02dec-116">**참고** - 이러한 속성 이름은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-116">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="02dec-117">배포 문제 tooavoid 아래와 같이 hello 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-117">Use hello names as seen below tooavoid deployment issues.</span></span>

* <span data-ttu-id="02dec-118">**commandToExecute**: (문자열, 필요한) 항목 지점 스크립트 tooexecute hello</span><span class="sxs-lookup"><span data-stu-id="02dec-118">**commandToExecute**: (required, string) hello entry point script tooexecute</span></span>
* <span data-ttu-id="02dec-119">**fileUris**: (선택 사항 문자열 배열) hello Url toobe 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-119">**fileUris**: (optional, string array) hello URLs for files toobe downloaded.</span></span>
* <span data-ttu-id="02dec-120">**타임 스탬프** (선택 사항 정수)이이 필드의 값을 변경 하 여이 필드만 tootrigger hello 스크립트의 다시 실행을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-120">**timestamp** (optional, integer) use this field only tootrigger a rerun of hello script by changing value of this field.</span></span>

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a><span data-ttu-id="02dec-121">보호된 구성</span><span class="sxs-lookup"><span data-stu-id="02dec-121">Protected Configuration</span></span>
<span data-ttu-id="02dec-122">스키마:</span><span class="sxs-lookup"><span data-stu-id="02dec-122">Schema:</span></span>

<span data-ttu-id="02dec-123">**참고** - 이러한 속성 이름은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-123">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="02dec-124">배포 문제 tooavoid 아래와 같이 hello 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-124">Use hello names as seen below tooavoid deployment issues.</span></span>

* <span data-ttu-id="02dec-125">**commandToExecute**: (선택 사항, string) 항목 지점 스크립트 tooexecute hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-125">**commandToExecute**: (optional, string) hello entry point script tooexecute.</span></span> <span data-ttu-id="02dec-126">명령에 암호와 같은 기밀 정보가 포함되는 경우 이 필드를 대신 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-126">Use this field instead if your command contains secrets such as passwords.</span></span>
* <span data-ttu-id="02dec-127">**storageAccountName**: (선택 사항, string) hello 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-127">**storageAccountName**: (optional, string) hello name of storage account.</span></span> <span data-ttu-id="02dec-128">저장소 자격 증명을 지정하는 경우 모든 fileUris는 Azure Blob에 대한 URL이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-128">If you specify storage credentials, all fileUris must be URLs for Azure Blobs.</span></span>
* <span data-ttu-id="02dec-129">**storageAccountKey**: (선택 사항, string) hello 선택 키의 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-129">**storageAccountKey**: (optional, string) hello access key of storage account.</span></span>

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a><span data-ttu-id="02dec-130">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="02dec-130">Azure CLI</span></span>
<span data-ttu-id="02dec-131">Hello Azure CLI toorun hello 사용자 지정 스크립트 확장을 사용할 경우에 구성 파일 또는 최소 hello 파일 uri 및 hello 스크립트 실행 명령을 포함 하는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-131">When using hello Azure CLI toorun hello Custom Script Extension, create a configuration file or files containing at minimum hello file uri, and hello script execution command.</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="02dec-132">필요에 따라 JSON 형식 문자열로 hello 설정은 hello 명령에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-132">Optionally hello settings can be specified in hello command as a JSON formatted string.</span></span> <span data-ttu-id="02dec-133">따라서 별도 구성 파일 없이도 실행 하는 동안 지정 된 hello 구성 toobe를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-133">This allows hello configuration toobe specified during execution and without a separate configuration file.</span></span>

```azurecli
az vm extension set '
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],"commandToExecute": "./test.sh"}'
```

### <a name="azure-cli-examples"></a><span data-ttu-id="02dec-134">Azure CLI 예제</span><span class="sxs-lookup"><span data-stu-id="02dec-134">Azure CLI Examples</span></span>

<span data-ttu-id="02dec-135">**예제 1** - 스크립트 파일이 있는 공용 구성.</span><span class="sxs-lookup"><span data-stu-id="02dec-135">**Example 1** - Public configuration with script file.</span></span>

```json
{
  "fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],
  "commandToExecute": "./test.sh"
}
```

<span data-ttu-id="02dec-136">Azure CLI 명령:</span><span class="sxs-lookup"><span data-stu-id="02dec-136">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="02dec-137">**예제 2** - 스크립트 파일이 없는 공용 구성.</span><span class="sxs-lookup"><span data-stu-id="02dec-137">**Example 2** - Public configuration with no script file.</span></span>

```json
{
  "commandToExecute": "apt-get -y update && apt-get install -y apache2"
}
```

<span data-ttu-id="02dec-138">Azure CLI 명령:</span><span class="sxs-lookup"><span data-stu-id="02dec-138">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="02dec-139">**예제 3** -공용 구성 파일이 사용 되는 toospecify hello 스크립트 파일 URI 및 보호 되는 구성 파일을 사용 하는 toospecify hello 명령 toobe 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-139">**Example 3** - A public configuration file is used toospecify hello script file URI, and a protected configuration file is used toospecify hello command toobe executed.</span></span>

<span data-ttu-id="02dec-140">공용 구성 파일:</span><span class="sxs-lookup"><span data-stu-id="02dec-140">Public configuration file:</span></span>

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"]
}
```

<span data-ttu-id="02dec-141">보호된 구성 파일:</span><span class="sxs-lookup"><span data-stu-id="02dec-141">Protected configuration file:</span></span>  

```json
{
  "commandToExecute": "./hello.sh <password>"
}
```

<span data-ttu-id="02dec-142">Azure CLI 명령:</span><span class="sxs-lookup"><span data-stu-id="02dec-142">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json --protected-settings ./protected-config.json
```

## <a name="resource-manager-template"></a><span data-ttu-id="02dec-143">Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="02dec-143">Resource Manager Template</span></span>
<span data-ttu-id="02dec-144">hello Azure 사용자 지정 스크립트 확장을 리소스 관리자 템플릿을 사용 하 여 가상 컴퓨터 배포 시간에 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-144">hello Azure Custom Script Extension can be run at Virtual Machine deployment time using a Resource Manager template.</span></span> <span data-ttu-id="02dec-145">toodo는, 적절 한 형식의 JSON toohello 배포 템플릿을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-145">toodo so, add properly formatted JSON toohello deployment template.</span></span>

### <a name="resource-manager-examples"></a><span data-ttu-id="02dec-146">Resource Manager 예제</span><span class="sxs-lookup"><span data-stu-id="02dec-146">Resource Manager Examples</span></span>
<span data-ttu-id="02dec-147">**예제 1** - 공용 구성</span><span class="sxs-lookup"><span data-stu-id="02dec-147">**Example 1** - public configuration.</span></span>

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

<span data-ttu-id="02dec-148">**예제 2** - 보호된 구성의 실행 명령.</span><span class="sxs-lookup"><span data-stu-id="02dec-148">**Example 2** - execution command in protected configuration.</span></span>

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

<span data-ttu-id="02dec-149">Hello.Net Core Music Store 참조는 전체 예제-데모 [음악 스토어 데모](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db)합니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-149">See hello .Net Core Music Store Demo for a complete example - [Music Store Demo](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="02dec-150">문제 해결</span><span class="sxs-lookup"><span data-stu-id="02dec-150">Troubleshooting</span></span>
<span data-ttu-id="02dec-151">Hello 사용자 지정 스크립트 확장이 실행 되 면 hello 스크립트를 만들거나 다음 예제에서는 디렉터리 비슷한 toohello에 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-151">When hello Custom Script Extension runs, hello script is created or downloaded into a directory similar toohello following example.</span></span> <span data-ttu-id="02dec-152">hello 명령 출력에서이 디렉터리에도 저장 `stdout` 및 `stderr` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-152">hello command output is also saved into this directory in `stdout` and `stderr` file.</span></span>

```bash
/var/lib/waagent/custom-script/download/0/
```

<span data-ttu-id="02dec-153">hello Azure 스크립트 확장을 찾아볼 수 있는 로그를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-153">hello Azure Script Extension produces a log, which can be found here.</span></span>

```bash
/var/log/azure/custom-script/handler.log
```

<span data-ttu-id="02dec-154">hello Azure CLI로 hello 사용자 지정 스크립트 확장의 hello 실행 상태를 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-154">hello execution state of hello Custom Script Extension can also be retrieved with hello Azure CLI.</span></span>

```azurecli
az vm extension list -g myResourceGroup --vm-name myVM
```

<span data-ttu-id="02dec-155">hello 출력 텍스트 다음 hello와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="02dec-155">hello output looks like hello following text:</span></span>

```azurecli
info:    Executing command vm extension get
+ Looking up hello VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a><span data-ttu-id="02dec-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="02dec-156">Next Steps</span></span>
<span data-ttu-id="02dec-157">다른 VM 스크립트 확장에 대한 자세한 내용은 [Linux용 Azure 스크립트 확장 개요](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02dec-157">For information on other VM Script Extensions, see [Azure Script Extension overview for Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

