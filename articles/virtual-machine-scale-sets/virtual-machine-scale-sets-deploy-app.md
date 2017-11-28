---
title: "가상 컴퓨터 확장 집합에 앱 배포"
description: "확장을 사용하여 Azure 가상 컴퓨터 확장 집합에 앱을 배포합니다."
services: virtual-machine-scale-sets
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8892199-f2e2-4b82-988a-28ca8a7fd1eb
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: fa7d9d3bef4cb326844ede76171e8c566e87116b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a><span data-ttu-id="45d51-103">가상 컴퓨터 확장 집합에 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="45d51-103">Deploy your application on virtual machine scale sets</span></span>

<span data-ttu-id="45d51-104">이 문서에서는 확장 집합을 프로비전할 때 소프트웨어를 설치하는 여러 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-104">This article describes different ways of how to install software at the time the scale set is provisioned.</span></span>

<span data-ttu-id="45d51-105">가상 컴퓨터 확장 집합에 적용되는 일부 제한에 대해 설명하는 [확장 집합 디자인 개요](virtual-machine-scale-sets-design-overview.md)도 읽어 보시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-105">You may want to review the [Scale Set Design Overview](virtual-machine-scale-sets-design-overview.md) article, which describes some of the limits imposed by virtual machine scale sets.</span></span>

## <a name="capture-and-reuse-an-image"></a><span data-ttu-id="45d51-106">이미지 캡처 및 재사용</span><span class="sxs-lookup"><span data-stu-id="45d51-106">Capture and reuse an image</span></span>

<span data-ttu-id="45d51-107">Azure에 갖고 있는 가상 컴퓨터를 사용하여 확장 집합에 사용할 기본 이미지를 준비할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-107">You can use a virtual machine you have in Azure to prepare a base-image for your scale set.</span></span> <span data-ttu-id="45d51-108">이 프로세스는 저장소 계정에 관리되는 디스크를 만듭니다. 만들어진 디스크는 확장 집합의 기본 이미지로 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-108">This process creates a managed disk in your storage account, which you can reference as the base image for your scale set.</span></span> 

<span data-ttu-id="45d51-109">다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-109">Do the following steps:</span></span>

1. <span data-ttu-id="45d51-110">Azure 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="45d51-110">Create an Azure Virtual Machine</span></span>
   * <span data-ttu-id="45d51-111">[Linux][linux-vm-create]</span><span class="sxs-lookup"><span data-stu-id="45d51-111">[Linux][linux-vm-create]</span></span>
   * <span data-ttu-id="45d51-112">[Windows][windows-vm-create]</span><span class="sxs-lookup"><span data-stu-id="45d51-112">[Windows][windows-vm-create]</span></span>

2. <span data-ttu-id="45d51-113">가상 컴퓨터에 원격으로 연결하고 시스템을 연결에 맞게 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-113">Remote into the virtual machine and customize the system to your liking.</span></span>

   <span data-ttu-id="45d51-114">원한다면 지금 응용 프로그램을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-114">If you want, you can install your application now.</span></span> <span data-ttu-id="45d51-115">그러나 지금 응용 프로그램을 설치하면 응용 프로그램 업그레이드가 더 복잡해질 수 있습니다. 가장 먼저 응용 프로그램을 제거해야 할 수도 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-115">However, know that by installing your application now, you may make upgrading your application more complicated because you may need to remove it first.</span></span> <span data-ttu-id="45d51-116">그 대신 이 단계에 따라 특정 런타임이나 운영 체제 기능처럼 응용 프로그램에 꼭 필요한 필수 구성 요소를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-116">Instead, you can use this step to install any prerequisites your application may need, like a specific runtime or operating system feature.</span></span>

3. <span data-ttu-id="45d51-117">[Linux][linux-vm-capture] 또는 [Windows][windows-vm-capture]에 대한 "컴퓨터 캡처" 자습서의 내용을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="45d51-117">Follow the "capture a machine" tutorial for either [Linux][linux-vm-capture] or [Windows][windows-vm-capture].</span></span>

4. <span data-ttu-id="45d51-118">이전 단계에서 캡처한 이미지 URI를 사용하여 [가상 컴퓨터 확장 집합][vmss-create]을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-118">Create a [Virtual Machine Scale Set][vmss-create] with the image URI you captured in the previous step.</span></span>

<span data-ttu-id="45d51-119">디스크에 대한 자세한 내용은 [Managed Disks 개요](../virtual-machines/windows/managed-disks-overview.md) 및 [연결된 데이터 디스크 사용](virtual-machine-scale-sets-attached-disks.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45d51-119">For more information about disks, see [Managed Disks Overview](../virtual-machines/windows/managed-disks-overview.md) and [Use Attached Data Disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

## <a name="install-when-the-scale-set-is-provisioned"></a><span data-ttu-id="45d51-120">확장 집합이 프로비전되면 설치</span><span class="sxs-lookup"><span data-stu-id="45d51-120">Install when the scale set is provisioned</span></span>

<span data-ttu-id="45d51-121">가상 컴퓨터 확장 집합에 가상 컴퓨터 확장을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-121">Virtual machine extensions can be applied to a virtual machine scale set.</span></span> <span data-ttu-id="45d51-122">가상 컴퓨터 확장을 사용하여 확장 집합의 가상 컴퓨터를 하나의 전체 그룹으로 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-122">With a virtual machine extension, you can customize the virtual machines in a scale set as a whole group.</span></span> <span data-ttu-id="45d51-123">확장에 대한 자세한 내용은 [가상 컴퓨터 확장](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45d51-123">For more information about extensions, see [Virtual Machine Extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="45d51-124">운영 체제가 Linux 기반인지 아니면 Windows 기반인지에 따라 세 가지 주요 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-124">There are three main extensions you can use, depending on if your operating system is Linux-based or Windows-based.</span></span>

### <a name="windows"></a><span data-ttu-id="45d51-125">Windows</span><span class="sxs-lookup"><span data-stu-id="45d51-125">Windows</span></span>

<span data-ttu-id="45d51-126">Windows 기반 운영 체제의 경우 **사용자 지정 스크립트 v1.8** 확장 또는 **PowerShell DSC** 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-126">For a Windows-based operating system, use either the **Custom Script v1.8** extension, or the **PowerShell DSC** extension.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="45d51-127">Custom Script</span><span class="sxs-lookup"><span data-stu-id="45d51-127">Custom Script</span></span>

<span data-ttu-id="45d51-128">사용자 지정 스크립트 확장은 확장 집합의 각 가상 컴퓨터 인스턴스에서 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-128">The Custom Script extension runs a script on each virtual machine instance in the scale set.</span></span> <span data-ttu-id="45d51-129">구성 파일 또는 변수는 어떤 파일이 가상 컴퓨터에 다운로드된 후 어떤 명령이 실행되는지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-129">A config file or variable indicates which files are downloaded to the virtual machine, and then what command runs.</span></span> <span data-ttu-id="45d51-130">예를 들어 이것을 사용하여 설치 프로그램, 스크립트, 일괄 처리 파일 및 모든 실행 파일을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-130">You could use this to run an installer, a script, a batch file, any executable for example.</span></span>

<span data-ttu-id="45d51-131">PowerShell은 설정에 해시 테이블을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-131">PowerShell uses a hashtable for the settings.</span></span> <span data-ttu-id="45d51-132">이 예제에서는 IIS를 설치하는 PowerShell 스크립트를 실행하는 사용자 지정 스크립트 확장을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-132">This example configures the custom script extension to run a PowerShell script that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add the extension to the config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send the new config to Azure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="45d51-133">민감한 정보가 포함될 수 있는 설정에는 `-ProtectedSetting` 스위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-133">Use the `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

---------


<span data-ttu-id="45d51-134">Azure CLI는 설정에 json 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-134">Azure CLI uses a json file for the settings.</span></span> <span data-ttu-id="45d51-135">이 예제에서는 IIS를 설치하는 PowerShell 스크립트를 실행하는 사용자 지정 스크립트 확장을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-135">This example configures the custom script extension to run a PowerShell script that installs IIS.</span></span> <span data-ttu-id="45d51-136">다음 json 파일을 _settings.json_으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-136">Save the following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

<span data-ttu-id="45d51-137">그런 다음 이 Azure CLI 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-137">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="45d51-138">민감한 정보가 포함될 수 있는 설정에는 `--protected-settings` 스위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-138">Use the `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="powershell-dsc"></a><span data-ttu-id="45d51-139">PowerShell DSC</span><span class="sxs-lookup"><span data-stu-id="45d51-139">PowerShell DSC</span></span>

<span data-ttu-id="45d51-140">PowerShell DSC를 사용하여 확장 집합 vm 인스턴스를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-140">You can use PowerShell DSC to customize the scale set vm instances.</span></span> <span data-ttu-id="45d51-141">**Microsoft.Powershell**을 통해 게시된 **DSC**는 제공된 DSC 구성을 각 가상 컴퓨터 인스턴스에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-141">The **DSC** extension published by **Microsoft.Powershell** deploys and runs the provided DSC configuration on each virtual machine instance.</span></span> <span data-ttu-id="45d51-142">구성 파일 또는 변수는 확장에 *.zip* 패키지의 위치 및 실행할 _스크립트-함수_ 조합을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-142">A config file or variable tells the extension where *.zip* package is, and which _script-function_ combination to run.</span></span>

<span data-ttu-id="45d51-143">PowerShell은 설정에 해시 테이블을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-143">PowerShell uses a hashtable for the settings.</span></span> <span data-ttu-id="45d51-144">이 예제에서는 IIS를 설치하는 DSC 패키지를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-144">This example deploys a DSC package that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$dscConfig = @{
  "wmfVersion" = "latest";
  "configuration" = @{
    "url" = "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip";
    "script" = "configure-http.ps1";
    "function" = "WebsiteTest";
  };
}

# Add the extension to the config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send the new config to Azure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="45d51-145">민감한 정보가 포함될 수 있는 설정에는 `-ProtectedSetting` 스위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-145">Use the `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

-----------

<span data-ttu-id="45d51-146">Azure CLI는 설정에 json을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-146">Azure CLI uses a json for the settings.</span></span> <span data-ttu-id="45d51-147">이 예제에서는 IIS를 설치하는 DSC 패키지를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-147">This example deploys a DSC package that installs IIS.</span></span> <span data-ttu-id="45d51-148">다음 json 파일을 _settings.json_으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-148">Save the following json file as _settings.json_.</span></span>

```json
{
  "wmfVersion": "latest",
  "configuration": {
    "url": "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip",
    "script": "configure-http.ps1",
    "function": "WebsiteTest"
  }
}
```

<span data-ttu-id="45d51-149">그런 다음 이 Azure CLI 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-149">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="45d51-150">민감한 정보가 포함될 수 있는 설정에는 `--protected-settings` 스위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-150">Use the `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="linux"></a><span data-ttu-id="45d51-151">Linux</span><span class="sxs-lookup"><span data-stu-id="45d51-151">Linux</span></span>

<span data-ttu-id="45d51-152">Linux는 **사용자 지정 스크립트 v2.0**을 사용하거나 만드는 동안 **cloud-init**을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-152">Linux can use either the **Custom Script v2.0** extension or use **cloud-init** during creation.</span></span>

<span data-ttu-id="45d51-153">사용자 지정 스크립트는 가상 컴퓨터 인스턴스에 파일을 다운로드하고 명령을 실행하는 간단한 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-153">Custom script is a simple extension that downloads files to the virtual machine instances, and runs a command.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="45d51-154">Custom Script</span><span class="sxs-lookup"><span data-stu-id="45d51-154">Custom Script</span></span>

<span data-ttu-id="45d51-155">다음 json 파일을 _settings.json_으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-155">Save the following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

<span data-ttu-id="45d51-156">Azure CLI를 사용하여 기존 가상 컴퓨터 확장 집합에 이 확장을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-156">Use the Azure CLI to add this extension to an existing virtual machine scale set.</span></span> <span data-ttu-id="45d51-157">확장 집합의 각 가상 컴퓨터는 자동으로 확장을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-157">Each virtual machine in the scale set automatically runs the extension.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="45d51-158">민감한 정보가 포함될 수 있는 설정에는 `--protected-settings` 스위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-158">Use the `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

#### <a name="cloud-init"></a><span data-ttu-id="45d51-159">Cloud-Init</span><span class="sxs-lookup"><span data-stu-id="45d51-159">Cloud-Init</span></span>

<span data-ttu-id="45d51-160">Cloud-Init은 확장 집합을 만들 때 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-160">Cloud-Init is used when the scale set is created.</span></span> <span data-ttu-id="45d51-161">먼저 _cloud-init.txt_라는 로컬 파일을 만들고 이 파일에 구성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-161">First, create a local file named _cloud-init.txt_ and add your configuration to it.</span></span> <span data-ttu-id="45d51-162">예제는 [이 gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45d51-162">For example, see [this gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span></span>

<span data-ttu-id="45d51-163">Azure CLI를 사용하여 확장 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-163">Use the Azure CLI to create a scale set.</span></span> <span data-ttu-id="45d51-164">`--custom-data` 필드는 cloud-init 스크립트의 파일 이름을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-164">The `--custom-data` field accepts the file name of a cloud-init script.</span></span>

```azurecli
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image Canonical:UbuntuServer:14.04.4-LTS:latest \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

## <a name="how-do-i-manage-application-updates"></a><span data-ttu-id="45d51-165">응용 프로그램 업데이트를 관리하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="45d51-165">How do I manage application updates?</span></span>

<span data-ttu-id="45d51-166">확장을 통해 응용 프로그램을 배포한 경우 어떤 방식으로든 확장 정의를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-166">If you deployed your application through an extension, alter the extension definition in some way.</span></span> <span data-ttu-id="45d51-167">이렇게 변경하면 모든 가상 컴퓨터 인스턴스에 확장이 다시 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-167">This change causes the extension to be redeployed to all virtual machine instances.</span></span> <span data-ttu-id="45d51-168">확장에 대한 무언가를 **반드시** 변경해야 합니다. 예를 들어 참조 파일의 이름을 변경합니다. 그렇지 않으면 Azure는 확장이 변경된 것으로 인식하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-168">Something **must** be changed about the extension, such as renaming a referenced file, otherwise, Azure does not see that the extension has changed.</span></span>

<span data-ttu-id="45d51-169">응용 프로그램을 사용자 고유의 운영 체제 이미지에 직접 포함한 경우 응용 프로그램 업데이트에 자동 배포 파이프라인을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-169">If you baked the application into your own operating system image, use an automated deployment pipeline for application updates.</span></span> <span data-ttu-id="45d51-170">미리 구성된 확장 집합을 용이하게 프로덕션으로 빠르게 교체할 수 있도록 아키텍처를 디자인합니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-170">Design your architecture to facilitate rapid swapping of a staged scale set into production.</span></span> <span data-ttu-id="45d51-171">이 방법의 예로 [Azure Spinnaker 드라이버 작업](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-171">A good example of this approach is the [Azure Spinnaker driver work](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span></span>

<span data-ttu-id="45d51-172">[Packer](https://www.packer.io/) 및 [Terraform](https://www.terraform.io/)은 Azure Resource Manager를 지원하므로, 이미지를 "코드로" 정의하고 Azure에서 빌드한 다음 해당 VHD를 확장 집합에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-172">[Packer](https://www.packer.io/) and [Terraform](https://www.terraform.io/) support Azure Resource Manager, so you can also define your images "as code" and build them in Azure, then use the VHD in your scale set.</span></span> <span data-ttu-id="45d51-173">그러나 사용자가 Marketplace에서 직접 조작하지 않으므로 확장/사용자 지정 스크립트가 좀 더 중요한 경우 이렇게 하면 Marketplace 이미지에 문제가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-173">However, doing so would become problematic for marketplace images, where extensions/custom scripts become more important since you don’t directly manipulate bits from marketplace.</span></span>

## <a name="what-happens-when-a-scale-set-scales-out"></a><span data-ttu-id="45d51-174">확장 집합이 확장되면 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="45d51-174">What happens when a scale set scales out?</span></span>
<span data-ttu-id="45d51-175">확장 집합에 하나 이상의 가상 컴퓨터를 추가하면 응용 프로그램이 자동으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-175">When you add one or more virtual machines to a scale set, the application is automatically installed.</span></span> <span data-ttu-id="45d51-176">예를 들어 확장 집합에 확장이 정의되면 가상 컴퓨터가 만들어질 때마다 새 가상 컴퓨터에서 해당 확장이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-176">For example if the scale set has extensions defined, they run on a new virtual machine each time it is created.</span></span> <span data-ttu-id="45d51-177">확장 집합이 사용자 지정 이미지를 기반으로 하는 경우 새 가상 컴퓨터는 원본 사용자 지정 이미지의 복사본이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-177">If the scale set is based on a custom image, any new virtual machine is a copy of the source custom image.</span></span> <span data-ttu-id="45d51-178">확장 집합 가상 컴퓨터가 컨테이너 호스트인 경우 사용자 지정 스크립트 확장의 컨테이너를 로드하는 시작 코드가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-178">If the scale set virtual machines are container hosts, then you might have startup code to load the containers in a Custom Script Extension.</span></span> <span data-ttu-id="45d51-179">또는 확장이 클러스터 조정자에 등록하는 Azure Container Service 같은 에이전트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-179">Or, an extension might install an agent that registers with a cluster orchestrator, such as Azure Container Service.</span></span>


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a><span data-ttu-id="45d51-180">업데이트 도메인 간에 OS 업데이트를 롤아웃하려면 어떻게 해야 할까요?</span><span class="sxs-lookup"><span data-stu-id="45d51-180">How do you roll out an OS update across update domains?</span></span>
<span data-ttu-id="45d51-181">가상 컴퓨터 확장 집합을 계속 실행하면서 OS 이미지를 업데이트하려 한다고 가정해 봅시다.</span><span class="sxs-lookup"><span data-stu-id="45d51-181">Suppose you want to update your OS image while keeping the virtual machine scale set running.</span></span> <span data-ttu-id="45d51-182">PowerShell 및 Azure CLI는 한 번에 하나의 가상 컴퓨터에서 가상 컴퓨터 이미지를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-182">PowerShell and the Azure CLI can update the virtual machine images, one virtual machine at a time.</span></span> <span data-ttu-id="45d51-183">또한 가상 컴퓨터 확장 집합에서 운영 체제 업그레이드를 수행하는 데 사용할 수 있는 옵션에 대한 자세한 내용은 [가상 컴퓨터 확장 집합 업그레이드](./virtual-machine-scale-sets-upgrade-scale-set.md) 문서에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d51-183">The [Upgrade a Virtual Machine Scale Set](./virtual-machine-scale-sets-upgrade-scale-set.md) article also provides further information on what options are available to perform an operating system upgrade across a virtual machine scale set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45d51-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="45d51-184">Next steps</span></span>

* [<span data-ttu-id="45d51-185">PowerShell을 사용하여 확장 집합 관리</span><span class="sxs-lookup"><span data-stu-id="45d51-185">Use PowerShell to manage your scale set.</span></span>](virtual-machine-scale-sets-windows-manage.md)
* [<span data-ttu-id="45d51-186">확장 집합 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="45d51-186">Create a scale set template.</span></span>](virtual-machine-scale-sets-mvss-start.md)


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

