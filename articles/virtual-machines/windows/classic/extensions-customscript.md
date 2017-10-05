---
title: "Windows VM의 사용자 지정 스크립트 확장 | Microsoft Docs"
description: "사용자 지정 스크립트 확장을 통해 원격 Windows VM에서 PowerShell 스크립트를 실행하여 Azure VM 구성 작업을 자동화합니다."
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
ms.openlocfilehash: 986ab1025dc188cd7fa1cf8b131a9d4b859be8f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="custom-script-extension-for-windows-using-the-classic-deployment-model"></a><span data-ttu-id="02cfe-103">클래식 배포 모델을 사용하는 Windows용 사용자 지정 스크립트 확장</span><span class="sxs-lookup"><span data-stu-id="02cfe-103">Custom Script Extension for Windows using the classic deployment model</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="02cfe-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="02cfe-105">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="02cfe-106">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="02cfe-107">[Resource Manager 모델을 사용하여 이러한 단계를 수행하는](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-107">Learn how to [perform these steps using the Resource Manager model](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="02cfe-108">사용자 지정 스크립트 확장은 Azure 가상 컴퓨터에서 스크립트를 다운로드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-108">The Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="02cfe-109">이 확장은 배포 후 구성, 소프트웨어 설치 또는 기타 구성/관리 작업에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-109">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="02cfe-110">스크립트를 Azure Storage 또는 GitHub에서 다운로드하거나 확장 런타임에서 Azure Portal에 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-110">Scripts can be downloaded from Azure storage or GitHub, or provided to the Azure portal at extension run time.</span></span> <span data-ttu-id="02cfe-111">사용자 지정 스크립트 확장은 Azure Resource Manager 템플릿과 통합되고, Azure CLI, PowerShell, Azure Portal 또는 Azure 가상 컴퓨터 REST API를 사용하여 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-111">The Custom Script extension integrates with Azure Resource Manager templates, and can also be run using the Azure CLI, PowerShell, Azure portal, or the Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="02cfe-112">이 문서에서는 Azure PowerShell 모듈, Azure Resource Manager 템플릿을 사용하는 사용자 지정 스크립트 확장을 사용하는 방법과 Windows 시스템에서 문제 해결 단계를 자세히 설명하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-112">This document details how to use the Custom Script Extension using the Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02cfe-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="02cfe-113">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="02cfe-114">운영 체제</span><span class="sxs-lookup"><span data-stu-id="02cfe-114">Operating System</span></span>

<span data-ttu-id="02cfe-115">Windows용 사용자 지정 스크립트 확장은 Windows Server 2008 R2, 2012, 2012 R2 및 2016 릴리스에 대해 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-115">The Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="02cfe-116">스크립트 위치</span><span class="sxs-lookup"><span data-stu-id="02cfe-116">Script Location</span></span>

<span data-ttu-id="02cfe-117">이 스크립트는 Azure Storage 또는 유효한 URL을 통해 액세스 가능한 기타 위치에 보관해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-117">The script needs to be stored in Azure storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="02cfe-118">인터넷 연결</span><span class="sxs-lookup"><span data-stu-id="02cfe-118">Internet Connectivity</span></span>

<span data-ttu-id="02cfe-119">Windows용 사용자 지정 스크립트 확장은 대상 가상 컴퓨터가 인터넷에 연결되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-119">The Custom Script Extension for Windows requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="02cfe-120">확장 스키마</span><span class="sxs-lookup"><span data-stu-id="02cfe-120">Extension schema</span></span>

<span data-ttu-id="02cfe-121">다음 JSON은 사용자 지정 스크립트 확장에 대한 스키마를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-121">The following JSON shows the schema for the Custom Script Extension.</span></span> <span data-ttu-id="02cfe-122">이 확장은 스크립트 위치(Azure Storage 또는 유효한 URL이 있는 기타 위치)와 실행할 명령이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-122">The extension requires a script location (Azure Storage or other location with valid URL), and a command to execute.</span></span> <span data-ttu-id="02cfe-123">스크립트 원본으로 Azure Storage를 사용하는 경우 Azure Storage 계정 이름 및 계정 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-123">If using Azure Storage as the script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="02cfe-124">이러한 항목은 중요한 데이터로 처리하고 확장으로 보호되는 설정 구성에 지정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-124">These items should be treated as sensitive data and specified in the extensions protected setting configuration.</span></span> <span data-ttu-id="02cfe-125">Azure VM 확장으로 보호되는 설정 데이터는 암호화되어 대상 가상 컴퓨터에서만 해독됩니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-125">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span>

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

### <a name="property-values"></a><span data-ttu-id="02cfe-126">속성 값</span><span class="sxs-lookup"><span data-stu-id="02cfe-126">Property values</span></span>

| <span data-ttu-id="02cfe-127">이름</span><span class="sxs-lookup"><span data-stu-id="02cfe-127">Name</span></span> | <span data-ttu-id="02cfe-128">값/예제</span><span class="sxs-lookup"><span data-stu-id="02cfe-128">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="02cfe-129">apiVersion</span><span class="sxs-lookup"><span data-stu-id="02cfe-129">apiVersion</span></span> | <span data-ttu-id="02cfe-130">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="02cfe-130">2015-06-15</span></span> |
| <span data-ttu-id="02cfe-131">publisher</span><span class="sxs-lookup"><span data-stu-id="02cfe-131">publisher</span></span> | <span data-ttu-id="02cfe-132">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="02cfe-132">Microsoft.Compute</span></span> |
| <span data-ttu-id="02cfe-133">확장</span><span class="sxs-lookup"><span data-stu-id="02cfe-133">extension</span></span> | <span data-ttu-id="02cfe-134">CustomScriptExtension</span><span class="sxs-lookup"><span data-stu-id="02cfe-134">CustomScriptExtension</span></span> |
| <span data-ttu-id="02cfe-135">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="02cfe-135">typeHandlerVersion</span></span> | <span data-ttu-id="02cfe-136">1.8</span><span class="sxs-lookup"><span data-stu-id="02cfe-136">1.8</span></span> |
| <span data-ttu-id="02cfe-137">fileUris(예)</span><span class="sxs-lookup"><span data-stu-id="02cfe-137">fileUris (e.g)</span></span> | <span data-ttu-id="02cfe-138">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="02cfe-138">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="02cfe-139">commandToExecute(예)</span><span class="sxs-lookup"><span data-stu-id="02cfe-139">commandToExecute (e.g)</span></span> | <span data-ttu-id="02cfe-140">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="02cfe-140">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="02cfe-141">템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="02cfe-141">Template deployment</span></span>

<span data-ttu-id="02cfe-142">Azure Resource Manager 템플릿을 사용하여 Azure VM 확장을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-142">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="02cfe-143">이전 섹션에서 자세히 설명되어 있는 JSON 스키마는 Azure Resource Manager 템플릿에서 사용하여 Azure Resource Manager 템플릿 배포 중 사용자 지정 스크립트 확장을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-143">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="02cfe-144">사용자 지정 스크립트 확장이 포함된 샘플 템플릿은 여기 [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-144">A sample template that includes the Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="02cfe-145">PowerShell 배포</span><span class="sxs-lookup"><span data-stu-id="02cfe-145">PowerShell deployment</span></span>

<span data-ttu-id="02cfe-146">`Set-AzureVMCustomScriptExtension` 명령을 사용하여 사용자 지정 스크립트 확장을 기존 가상 컴퓨터에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-146">The `Set-AzureVMCustomScriptExtension` command can be used to add the Custom Script extension to an existing virtual machine.</span></span> <span data-ttu-id="02cfe-147">자세한 내용은 [Set-AzureRmVMCustomScriptExtension](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02cfe-147">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>

```powershell
# create vm object
$vm = Get-AzureVM -Name 2016clas -ServiceName 2016clas1313

# set extension
Set-AzureVMCustomScriptExtension -VM $vm -FileUri myFileUri -Run 'create-file.ps1'

# update vm
$vm | Update-AzureVM
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="02cfe-148">문제 해결 및 지원</span><span class="sxs-lookup"><span data-stu-id="02cfe-148">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="02cfe-149">문제 해결</span><span class="sxs-lookup"><span data-stu-id="02cfe-149">Troubleshoot</span></span>

<span data-ttu-id="02cfe-150">확장 배포 상태에 대한 데이터는 Azure PowerShell 모듈을 사용하여 Azure Portal에서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-150">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="02cfe-151">지정된 VM에 대한 확장의 배포 상태를 보려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-151">To see the deployment state of extensions for a given VM, run the following command.</span></span>

```powershell
Get-AzureVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="02cfe-152">확장 실행 출력은 대상 가상 컴퓨터의 다음 디렉터리에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-152">Extension execution output us logged to files found in the following directory on the target virtual machine.</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="02cfe-153">스크립트 자체는 대상 가상 컴퓨터의 다음 디렉터리에 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-153">The script itself is downloaded into the following directory on the target virtual machine.</span></span>

```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads
```

### <a name="support"></a><span data-ttu-id="02cfe-154">지원</span><span class="sxs-lookup"><span data-stu-id="02cfe-154">Support</span></span>

<span data-ttu-id="02cfe-155">이 문서의 어디에서든 도움이 필요한 경우 [MSDN Azure 및 Stack Overflow 포럼](https://azure.microsoft.com/en-us/support/forums/)에서 Azure 전문가에게 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-155">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="02cfe-156">또는 Azure 기술 지원 인시던트를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-156">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="02cfe-157">[Azure 지원 사이트](https://azure.microsoft.com/en-us/support/options/)로 가서 지원 받기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02cfe-157">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="02cfe-158">Azure 지원을 사용하는 방법에 대한 자세한 내용은 [Microsoft Azure 지원 FAQ](https://azure.microsoft.com/en-us/support/faq/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02cfe-158">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>