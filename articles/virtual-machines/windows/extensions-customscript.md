---
title: "Windows용 Azure 사용자 지정 스크립트 확장 | Microsoft Azure"
description: "사용자 지정 스크립트 확장을 사용하여 Windows VM 구성 작업 자동화"
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
ms.openlocfilehash: a6f417ea6575b81258998ae3b31c10e9df59b603
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="custom-script-extension-for-windows"></a><span data-ttu-id="9a4ff-103">Windows용 사용자 지정 스크립트 확장</span><span class="sxs-lookup"><span data-stu-id="9a4ff-103">Custom Script Extension for Windows</span></span>

<span data-ttu-id="9a4ff-104">사용자 지정 스크립트 확장은 Azure 가상 컴퓨터에서 스크립트를 다운로드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-104">The Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="9a4ff-105">이 확장은 배포 후 구성, 소프트웨어 설치 또는 기타 구성/관리 작업에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="9a4ff-106">스크립트를 Azure Storage 또는 GitHub에서 다운로드하거나 확장 런타임에서 Azure Portal에 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-106">Scripts can be downloaded from Azure storage or GitHub, or provided to the Azure portal at extension run time.</span></span> <span data-ttu-id="9a4ff-107">사용자 지정 스크립트 확장은 Azure Resource Manager 템플릿과 통합되고, Azure CLI, PowerShell, Azure Portal 또는 Azure 가상 컴퓨터 REST API를 사용하여 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-107">The Custom Script extension integrates with Azure Resource Manager templates, and can also be run using the Azure CLI, PowerShell, Azure portal, or the Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="9a4ff-108">이 문서에서는 Azure PowerShell 모듈, Azure Resource Manager 템플릿을 사용하는 사용자 지정 스크립트 확장을 사용하는 방법과 Windows 시스템에서 문제 해결 단계를 자세히 설명하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-108">This document details how to use the Custom Script Extension using the Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a4ff-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9a4ff-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="9a4ff-110">운영 체제</span><span class="sxs-lookup"><span data-stu-id="9a4ff-110">Operating System</span></span>

<span data-ttu-id="9a4ff-111">Windows용 사용자 지정 스크립트 확장은 Windows Server 2008 R2, 2012, 2012 R2 및 2016 릴리스에 대해 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-111">The Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="9a4ff-112">스크립트 위치</span><span class="sxs-lookup"><span data-stu-id="9a4ff-112">Script Location</span></span>

<span data-ttu-id="9a4ff-113">이 스크립트는 Azure Blob Storage 또는 유효한 URL을 통해 액세스 가능한 기타 위치에 보관해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-113">The script needs to be stored in Azure Blob storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="9a4ff-114">인터넷 연결</span><span class="sxs-lookup"><span data-stu-id="9a4ff-114">Internet Connectivity</span></span>

<span data-ttu-id="9a4ff-115">Windows용 사용자 지정 스크립트 확장은 대상 가상 컴퓨터가 인터넷에 연결되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-115">The Custom Script Extension for Windows requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="9a4ff-116">확장 스키마</span><span class="sxs-lookup"><span data-stu-id="9a4ff-116">Extension schema</span></span>

<span data-ttu-id="9a4ff-117">다음 JSON은 사용자 지정 스크립트 확장에 대한 스키마를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-117">The following JSON shows the schema for the Custom Script Extension.</span></span> <span data-ttu-id="9a4ff-118">이 확장은 스크립트 위치(Azure Storage 또는 유효한 URL이 있는 기타 위치)와 실행할 명령이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-118">The extension requires a script location (Azure Storage or other location with valid URL), and a command to execute.</span></span> <span data-ttu-id="9a4ff-119">스크립트 원본으로 Azure Storage를 사용하는 경우 Azure Storage 계정 이름 및 계정 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-119">If using Azure Storage as the script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="9a4ff-120">이러한 항목은 중요한 데이터로 처리하고 확장으로 보호되는 설정 구성에 지정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-120">These items should be treated as sensitive data and specified in the extensions protected setting configuration.</span></span> <span data-ttu-id="9a4ff-121">Azure VM 확장으로 보호되는 설정 데이터는 암호화되어 대상 가상 컴퓨터에서만 해독됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-121">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span>

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

### <a name="property-values"></a><span data-ttu-id="9a4ff-122">속성 값</span><span class="sxs-lookup"><span data-stu-id="9a4ff-122">Property values</span></span>

| <span data-ttu-id="9a4ff-123">이름</span><span class="sxs-lookup"><span data-stu-id="9a4ff-123">Name</span></span> | <span data-ttu-id="9a4ff-124">값/예제</span><span class="sxs-lookup"><span data-stu-id="9a4ff-124">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="9a4ff-125">apiVersion</span><span class="sxs-lookup"><span data-stu-id="9a4ff-125">apiVersion</span></span> | <span data-ttu-id="9a4ff-126">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="9a4ff-126">2015-06-15</span></span> |
| <span data-ttu-id="9a4ff-127">publisher</span><span class="sxs-lookup"><span data-stu-id="9a4ff-127">publisher</span></span> | <span data-ttu-id="9a4ff-128">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="9a4ff-128">Microsoft.Compute</span></span> |
| <span data-ttu-id="9a4ff-129">type</span><span class="sxs-lookup"><span data-stu-id="9a4ff-129">type</span></span> | <span data-ttu-id="9a4ff-130">확장</span><span class="sxs-lookup"><span data-stu-id="9a4ff-130">extensions</span></span> |
| <span data-ttu-id="9a4ff-131">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="9a4ff-131">typeHandlerVersion</span></span> | <span data-ttu-id="9a4ff-132">1.9</span><span class="sxs-lookup"><span data-stu-id="9a4ff-132">1.9</span></span> |
| <span data-ttu-id="9a4ff-133">fileUris(예)</span><span class="sxs-lookup"><span data-stu-id="9a4ff-133">fileUris (e.g)</span></span> | <span data-ttu-id="9a4ff-134">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="9a4ff-134">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="9a4ff-135">commandToExecute(예)</span><span class="sxs-lookup"><span data-stu-id="9a4ff-135">commandToExecute (e.g)</span></span> | <span data-ttu-id="9a4ff-136">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="9a4ff-136">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |
| <span data-ttu-id="9a4ff-137">storageAccountName(예)</span><span class="sxs-lookup"><span data-stu-id="9a4ff-137">storageAccountName (e.g)</span></span> | <span data-ttu-id="9a4ff-138">examplestorageacct</span><span class="sxs-lookup"><span data-stu-id="9a4ff-138">examplestorageacct</span></span> |
| <span data-ttu-id="9a4ff-139">storageAccountKey(예)</span><span class="sxs-lookup"><span data-stu-id="9a4ff-139">storageAccountKey (e.g)</span></span> | <span data-ttu-id="9a4ff-140">TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg==</span><span class="sxs-lookup"><span data-stu-id="9a4ff-140">TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg==</span></span> |

<span data-ttu-id="9a4ff-141">**참고** - 이러한 속성 이름은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-141">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="9a4ff-142">배포 문제를 방지하려면 위와 같이 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-142">Use the names as seen above to avoid deployment issues.</span></span>

## <a name="template-deployment"></a><span data-ttu-id="9a4ff-143">템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="9a4ff-143">Template deployment</span></span>

<span data-ttu-id="9a4ff-144">Azure Resource Manager 템플릿을 사용하여 Azure VM 확장을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-144">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="9a4ff-145">이전 섹션에서 자세히 설명되어 있는 JSON 스키마는 Azure Resource Manager 템플릿에서 사용하여 Azure Resource Manager 템플릿 배포 중 사용자 지정 스크립트 확장을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-145">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="9a4ff-146">사용자 지정 스크립트 확장이 포함된 샘플 템플릿은 여기 [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-146">A sample template that includes the Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="9a4ff-147">PowerShell 배포</span><span class="sxs-lookup"><span data-stu-id="9a4ff-147">PowerShell deployment</span></span>

<span data-ttu-id="9a4ff-148">`Set-AzureRmVMCustomScriptExtension` 명령을 사용하여 사용자 지정 스크립트 확장을 기존 가상 컴퓨터에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-148">The `Set-AzureRmVMCustomScriptExtension` command can be used to add the Custom Script extension to an existing virtual machine.</span></span> <span data-ttu-id="9a4ff-149">자세한 내용은 [Set-AzureRmVMCustomScriptExtension](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-149">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>
```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName myResourceGroup `
    -VMName myVM `
    -Location myLocation `
    -FileUri myURL `
    -Run 'myScript.ps1' `
    -Name DemoScriptExtension
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="9a4ff-150">문제 해결 및 지원</span><span class="sxs-lookup"><span data-stu-id="9a4ff-150">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="9a4ff-151">문제 해결</span><span class="sxs-lookup"><span data-stu-id="9a4ff-151">Troubleshoot</span></span>

<span data-ttu-id="9a4ff-152">확장 배포 상태에 대한 데이터는 Azure PowerShell 모듈을 사용하여 Azure Portal에서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-152">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="9a4ff-153">지정된 VM에 대한 확장의 배포 상태를 보려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-153">To see the deployment state of extensions for a given VM, run the following command.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="9a4ff-154">확장 실행 출력은 대상 가상 컴퓨터의 다음 디렉터리 아래에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-154">Extension execution output is logged to files found under the following directory on the target virtual machine.</span></span>
```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="9a4ff-155">지정된 파일은 대상 가상 컴퓨터의 다음 디렉터리에 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-155">The specified files are downloaded into the following directory on the target virtual machine.</span></span>
```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads\<n>
```
<span data-ttu-id="9a4ff-156">여기서 `<n>`은 확장의 실행 간에 변경될 수 있는 10진수 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-156">where `<n>` is a decimal integer which may change between executions of the extension.</span></span>  <span data-ttu-id="9a4ff-157">`1.*` 값은 확장의 현재 실제 `typeHandlerVersion` 값과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-157">The `1.*` value matches the actual, current `typeHandlerVersion` value of the extension.</span></span>  <span data-ttu-id="9a4ff-158">예를 들어, 실제 디렉터리는 `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-158">For example, the actual directory could be `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span></span>  

<span data-ttu-id="9a4ff-159">`commandToExecute` 명령을 실행할 경우 확장은 현재 작업 디렉터리처럼 이 디렉터리를 설정합니다(예: `...\Downloads\2`).</span><span class="sxs-lookup"><span data-stu-id="9a4ff-159">When executing the `commandToExecute` command, the extension will have set this directory (e.g., `...\Downloads\2`) as the current working directory.</span></span> <span data-ttu-id="9a4ff-160">그러면 `fileURIs` 속성을 통해 다운로드된 파일을 배치하는 상대 경로를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-160">This enables the use of relative paths to locate the files downloaded via the `fileURIs` property.</span></span> <span data-ttu-id="9a4ff-161">예제는 아래 테이블을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-161">See the table below for examples.</span></span>

<span data-ttu-id="9a4ff-162">시간이 지남에 따라 절대 다운로드 경로가 달라질 수 있으므로 가능한 경우 `commandToExecute` 문자열에서 상대 스크립트/파일 경로를 옵트인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-162">Since the absolute download path may vary over time, it is better to opt for relative script/file paths in the `commandToExecute` string, whenever possible.</span></span> <span data-ttu-id="9a4ff-163">예:</span><span class="sxs-lookup"><span data-stu-id="9a4ff-163">For example:</span></span>
```json
    "commandToExecute": "powershell.exe . . . -File './scripts/myscript.ps1'"
```

<span data-ttu-id="9a4ff-164">첫 번째 URI 세그먼트 뒤의 경로 정보는 `fileUris` 속성 목록을 통해 다운로드된 파일에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-164">Path information after the first URI segment is retained for files downloaded via the `fileUris` property list.</span></span>  <span data-ttu-id="9a4ff-165">아래 테이블에 표시된 대로 다운로드된 파일은 다운로드 하위 디렉터리에 매핑되어 `fileUris` 값의 구조를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-165">As shown in the table below, downloaded files are mapped into download subdirectories to reflect the structure of the `fileUris` values.</span></span>  

#### <a name="examples-of-downloaded-files"></a><span data-ttu-id="9a4ff-166">다운로드된 파일의 예</span><span class="sxs-lookup"><span data-stu-id="9a4ff-166">Examples of Downloaded Files</span></span>

| <span data-ttu-id="9a4ff-167">fileUris의 URI</span><span class="sxs-lookup"><span data-stu-id="9a4ff-167">URI in fileUris</span></span> | <span data-ttu-id="9a4ff-168">다운로드된 상대 위치</span><span class="sxs-lookup"><span data-stu-id="9a4ff-168">Relative downloaded location</span></span> | <span data-ttu-id="9a4ff-169">다운로드된 절대 위치*</span><span class="sxs-lookup"><span data-stu-id="9a4ff-169">Absolute downloaded location *</span></span> |
| ---- | ------- |:--- |
| `https://someAcct.blob.core.windows.net/aContainer/scripts/myscript.ps1` | `./scripts/myscript.ps1` |`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\scripts\myscript.ps1`  |
| `https://someAcct.blob.core.windows.net/aContainer/topLevel.ps1` | `./topLevel.ps1` | `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\topLevel.ps1` |

<span data-ttu-id="9a4ff-170">\* 위와 같이 CustomScript 확장의 단일 실행 이내가 아닌 VM의 수명 동안 절대 디렉터리 경로가 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-170">\* As above, the absolute directory paths will change over the lifetime of the VM, but not within a single execution of the CustomScript extension.</span></span>

### <a name="support"></a><span data-ttu-id="9a4ff-171">지원</span><span class="sxs-lookup"><span data-stu-id="9a4ff-171">Support</span></span>

<span data-ttu-id="9a4ff-172">이 문서의 어디에서든 도움이 필요한 경우 [MSDN Azure 및 Stack Overflow 포럼](https://azure.microsoft.com/en-us/support/forums/)에서 Azure 전문가에게 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-172">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums] (https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="9a4ff-173">또는 Azure 기술 지원 인시던트를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-173">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="9a4ff-174">[Azure 지원 사이트](https://azure.microsoft.com/en-us/support/options/)로 가서 지원 받기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-174">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="9a4ff-175">Azure 지원을 사용하는 방법에 대한 자세한 내용은 [Microsoft Azure 지원 FAQ](https://azure.microsoft.com/en-us/support/faq/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a4ff-175">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
