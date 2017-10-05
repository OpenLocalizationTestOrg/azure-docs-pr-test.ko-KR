---
title: "Azure의 Linux VM에서 사용자 지정 스크립트 실행 | Microsoft Docs"
description: "사용자 지정 스크립트 확장을 사용하여 Linux VM 구성 작업 자동화"
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
ms.openlocfilehash: 1dde64aac72c11ccfccf4fdb676279692befaadd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="using-the-azure-custom-script-extension-with-linux-virtual-machines"></a><span data-ttu-id="79a9c-103">Linux 가상 컴퓨터에서 Azure 사용자 지정 스크립트 확장</span><span class="sxs-lookup"><span data-stu-id="79a9c-103">Using the Azure Custom Script Extension with Linux Virtual Machines</span></span>
<span data-ttu-id="79a9c-104">사용자 지정 스크립트 확장은 Azure 가상 컴퓨터에서 스크립트를 다운로드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="79a9c-104">The Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="79a9c-105">이 확장은 배포 후 구성, 소프트웨어 설치 또는 기타 구성/관리 작업에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="79a9c-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="79a9c-106">스크립트를 Azure 저장소 또는 기타 액세스가 가능한 인터넷 위치에서 다운로드하거나 확장 런타임으로 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79a9c-106">Scripts can be downloaded from Azure storage or other accessible internet location, or provided to the extension run time.</span></span> <span data-ttu-id="79a9c-107">사용자 지정 스크립트 확장은 Azure Resource Manager 템플릿과 통합되고, Azure CLI, PowerShell, Azure Portal 또는 Azure 가상 컴퓨터 REST API를 사용하여 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79a9c-107">The Custom Script extension integrates with Azure Resource Manager templates, and can also be run using the Azure CLI, PowerShell, Azure portal, or the Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="79a9c-108">이 문서에서는 Azure CLI 및 Azure Resource Manager 템플릿에서 사용자 지정 스크립트 확장을 사용하는 방법을 자세히 설명하고 Linux 시스템에서의 문제 해결 단계도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="79a9c-108">This document details how to use the Custom Script Extension from the Azure CLI, and an Azure Resource Manager template, and also details troubleshooting steps on Linux systems.</span></span>

## <a name="extension-configuration"></a><span data-ttu-id="79a9c-109">확장 구성</span><span class="sxs-lookup"><span data-stu-id="79a9c-109">Extension Configuration</span></span>
<span data-ttu-id="79a9c-110">사용자 지정 스크립트 확장 구성은 스크립트 위치 및 실행할 명령 등을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="79a9c-110">The Custom Script Extension configuration specifies things like script location and the command to be run.</span></span> <span data-ttu-id="79a9c-111">이 구성은 명령줄 또는 Azure Resource Manager 템플릿에 지정된 구성 파일에 저장될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79a9c-111">This configuration can be stored in configuration files, specified on the command line, or in an Azure Resource Manager template.</span></span> <span data-ttu-id="79a9c-112">중요한 데이터는 보호된 구성에 저장되고 암호화된 후 가상 컴퓨터 내에서만 해독됩니다.</span><span class="sxs-lookup"><span data-stu-id="79a9c-112">Sensitive data can be stored in a protected configuration, which is encrypted and only decrypted inside the virtual machine.</span></span> <span data-ttu-id="79a9c-113">보호된 구성은 실행 명령에 암호와 같은 기밀 정보가 포함될 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="79a9c-113">The protected configuration is useful when the execution command includes secrets such as a password.</span></span>

### <a name="public-configuration"></a><span data-ttu-id="79a9c-114">공용 구성</span><span class="sxs-lookup"><span data-stu-id="79a9c-114">Public Configuration</span></span>
<span data-ttu-id="79a9c-115">스키마:</span><span class="sxs-lookup"><span data-stu-id="79a9c-115">Schema:</span></span>

<span data-ttu-id="79a9c-116">**참고** - 이러한 속성 이름은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="79a9c-116">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="79a9c-117">배포 문제를 방지하려면 아래와 같이 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="79a9c-117">Use the names as seen below to avoid deployment issues.</span></span>

* <span data-ttu-id="79a9c-118">**commandToExecute**: (필수, 문자열) 실행할 진입점 스크립트</span><span class="sxs-lookup"><span data-stu-id="79a9c-118">**commandToExecute**: (required, string) the entry point script to execute</span></span>
* <span data-ttu-id="79a9c-119">**fileUris**: (옵션, 문자열 배열) 파일을 다운로드할 URL</span><span class="sxs-lookup"><span data-stu-id="79a9c-119">**fileUris**: (optional, string array) the URLs for files to be downloaded.</span></span>
* <span data-ttu-id="79a9c-120">**timestamp** : (옵션, 정수) 이 필드는 이 필드의 값을 변경하여 스크립트의 다시 실행을 트리거하는 데만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="79a9c-120">**timestamp** (optional, integer) use this field only to trigger a rerun of the script by changing value of this field.</span></span>

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a><span data-ttu-id="79a9c-121">보호된 구성</span><span class="sxs-lookup"><span data-stu-id="79a9c-121">Protected Configuration</span></span>
<span data-ttu-id="79a9c-122">스키마:</span><span class="sxs-lookup"><span data-stu-id="79a9c-122">Schema:</span></span>

<span data-ttu-id="79a9c-123">**참고** - 이러한 속성 이름은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="79a9c-123">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="79a9c-124">배포 문제를 방지하려면 아래와 같이 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="79a9c-124">Use the names as seen below to avoid deployment issues.</span></span>

* <span data-ttu-id="79a9c-125">**commandToExecute**: (옵션, 문자열) 실행할 진입점 스크립트.</span><span class="sxs-lookup"><span data-stu-id="79a9c-125">**commandToExecute**: (optional, string) the entry point script to execute.</span></span> <span data-ttu-id="79a9c-126">명령에 암호와 같은 기밀 정보가 포함되는 경우 이 필드를 대신 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="79a9c-126">Use this field instead if your command contains secrets such as passwords.</span></span>
* <span data-ttu-id="79a9c-127">**storageAccountName**: (옵션, 문자열) 저장소 계정의 이름.</span><span class="sxs-lookup"><span data-stu-id="79a9c-127">**storageAccountName**: (optional, string) the name of storage account.</span></span> <span data-ttu-id="79a9c-128">저장소 자격 증명을 지정하는 경우 모든 fileUris는 Azure Blob에 대한 URL이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79a9c-128">If you specify storage credentials, all fileUris must be URLs for Azure Blobs.</span></span>
* <span data-ttu-id="79a9c-129">**storageAccountName**: (옵션, 문자열) 저장소 계정의 액세스 키</span><span class="sxs-lookup"><span data-stu-id="79a9c-129">**storageAccountKey**: (optional, string) the access key of storage account.</span></span>

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a><span data-ttu-id="79a9c-130">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="79a9c-130">Azure CLI</span></span>
<span data-ttu-id="79a9c-131">Azure CLI를 사용하여 사용자 지정 스크립트 확장을 실행할 때 최소한 파일 URI 및 스크립트 실행 명령을 포함하는 구성 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="79a9c-131">When using the Azure CLI to run the Custom Script Extension, create a configuration file or files containing at minimum the file uri, and the script execution command.</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="79a9c-132">필요에 따라 설정을 JSON 형식 문자열로 명령에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79a9c-132">Optionally the settings can be specified in the command as a JSON formatted string.</span></span> <span data-ttu-id="79a9c-133">이렇게 하면 실행 중에 별도 구성 파일 없이 구성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79a9c-133">This allows the configuration to be specified during execution and without a separate configuration file.</span></span>

```azurecli
az vm extension set '
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],"commandToExecute": "./test.sh"}'
```

### <a name="azure-cli-examples"></a><span data-ttu-id="79a9c-134">Azure CLI 예제</span><span class="sxs-lookup"><span data-stu-id="79a9c-134">Azure CLI Examples</span></span>

<span data-ttu-id="79a9c-135">**예제 1** - 스크립트 파일이 있는 공용 구성.</span><span class="sxs-lookup"><span data-stu-id="79a9c-135">**Example 1** - Public configuration with script file.</span></span>

```json
{
  "fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],
  "commandToExecute": "./test.sh"
}
```

<span data-ttu-id="79a9c-136">Azure CLI 명령:</span><span class="sxs-lookup"><span data-stu-id="79a9c-136">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="79a9c-137">**예제 2** - 스크립트 파일이 없는 공용 구성.</span><span class="sxs-lookup"><span data-stu-id="79a9c-137">**Example 2** - Public configuration with no script file.</span></span>

```json
{
  "commandToExecute": "apt-get -y update && apt-get install -y apache2"
}
```

<span data-ttu-id="79a9c-138">Azure CLI 명령:</span><span class="sxs-lookup"><span data-stu-id="79a9c-138">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="79a9c-139">**예제 3** - 공용 구성 파일은 스크립트 파일 URI를 지정하는 데 사용되고, 보호된 구성 파일은 실행할 명령을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="79a9c-139">**Example 3** - A public configuration file is used to specify the script file URI, and a protected configuration file is used to specify the command to be executed.</span></span>

<span data-ttu-id="79a9c-140">공용 구성 파일:</span><span class="sxs-lookup"><span data-stu-id="79a9c-140">Public configuration file:</span></span>

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"]
}
```

<span data-ttu-id="79a9c-141">보호된 구성 파일:</span><span class="sxs-lookup"><span data-stu-id="79a9c-141">Protected configuration file:</span></span>  

```json
{
  "commandToExecute": "./hello.sh <password>"
}
```

<span data-ttu-id="79a9c-142">Azure CLI 명령:</span><span class="sxs-lookup"><span data-stu-id="79a9c-142">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json --protected-settings ./protected-config.json
```

## <a name="resource-manager-template"></a><span data-ttu-id="79a9c-143">Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="79a9c-143">Resource Manager Template</span></span>
<span data-ttu-id="79a9c-144">Azure 사용자 지정 스크립트 확장은 Resource Manager 템플릿을 사용하여 가상 컴퓨터 배포 시에 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79a9c-144">The Azure Custom Script Extension can be run at Virtual Machine deployment time using a Resource Manager template.</span></span> <span data-ttu-id="79a9c-145">이렇게 하려면 올바른 형식의 JSON을 배포 템플릿에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="79a9c-145">To do so, add properly formatted JSON to the deployment template.</span></span>

### <a name="resource-manager-examples"></a><span data-ttu-id="79a9c-146">Resource Manager 예제</span><span class="sxs-lookup"><span data-stu-id="79a9c-146">Resource Manager Examples</span></span>
<span data-ttu-id="79a9c-147">**예제 1** - 공용 구성</span><span class="sxs-lookup"><span data-stu-id="79a9c-147">**Example 1** - public configuration.</span></span>

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

<span data-ttu-id="79a9c-148">**예제 2** - 보호된 구성의 실행 명령.</span><span class="sxs-lookup"><span data-stu-id="79a9c-148">**Example 2** - execution command in protected configuration.</span></span>

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

<span data-ttu-id="79a9c-149">전체 예제에 대해서는 .NET Core Music Store 데모 참조 [Music Store 데모](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="79a9c-149">See the .Net Core Music Store Demo for a complete example - [Music Store Demo](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="79a9c-150">문제 해결</span><span class="sxs-lookup"><span data-stu-id="79a9c-150">Troubleshooting</span></span>
<span data-ttu-id="79a9c-151">사용자 지정 스크립트 확장이 실행되면 스크립트 생성되거나 다음 예제와 비슷한 디렉터리에 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="79a9c-151">When the Custom Script Extension runs, the script is created or downloaded into a directory similar to the following example.</span></span> <span data-ttu-id="79a9c-152">또한 명령 출력은 이 디렉터리의 `stdout` 및 `stderr` 파일에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="79a9c-152">The command output is also saved into this directory in `stdout` and `stderr` file.</span></span>

```bash
/var/lib/waagent/custom-script/download/0/
```

<span data-ttu-id="79a9c-153">Azure 스크립트 확장은 여기에서 찾을 수 있는 로그를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="79a9c-153">The Azure Script Extension produces a log, which can be found here.</span></span>

```bash
/var/log/azure/custom-script/handler.log
```

<span data-ttu-id="79a9c-154">사용자 지정 스크립트 확장의 실행 상태를 Azure CLI를 사용하여 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79a9c-154">The execution state of the Custom Script Extension can also be retrieved with the Azure CLI.</span></span>

```azurecli
az vm extension list -g myResourceGroup --vm-name myVM
```

<span data-ttu-id="79a9c-155">출력은 다음 텍스트와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="79a9c-155">The output looks like the following text:</span></span>

```azurecli
info:    Executing command vm extension get
+ Looking up the VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a><span data-ttu-id="79a9c-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="79a9c-156">Next Steps</span></span>
<span data-ttu-id="79a9c-157">다른 VM 스크립트 확장에 대한 자세한 내용은 [Linux용 Azure 스크립트 확장 개요](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="79a9c-157">For information on other VM Script Extensions, see [Azure Script Extension overview for Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

