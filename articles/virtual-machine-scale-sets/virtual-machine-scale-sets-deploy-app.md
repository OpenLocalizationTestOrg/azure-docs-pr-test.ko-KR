---
title: "aaaDeploy 응용 프로그램에 가상 컴퓨터 크기 집합"
description: "Azure 가상 컴퓨터 크기 집합에 확장 toodepoy 응용 프로그램을 사용 합니다."
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
ms.openlocfilehash: 5f3988b9511d80370a8be1fc042c21fee212506e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a><span data-ttu-id="48fb1-103">가상 컴퓨터 확장 집합에 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="48fb1-103">Deploy your application on virtual machine scale sets</span></span>

<span data-ttu-id="48fb1-104">이 문서에서는 다른 hello 시간 hello 배율로 tooinstall 소프트웨어 설정 하는 방법의 프로 비전 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-104">This article describes different ways of how tooinstall software at hello time hello scale set is provisioned.</span></span>

<span data-ttu-id="48fb1-105">Tooreview hello를 할 수 있습니다 [디자인 개요를 설정 하는 눈금](virtual-machine-scale-sets-design-overview.md) 문서도, 가상 컴퓨터 크기 집합으로 부과 된 hello 제한의 일부에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-105">You may want tooreview hello [Scale Set Design Overview](virtual-machine-scale-sets-design-overview.md) article, which describes some of hello limits imposed by virtual machine scale sets.</span></span>

## <a name="capture-and-reuse-an-image"></a><span data-ttu-id="48fb1-106">이미지 캡처 및 재사용</span><span class="sxs-lookup"><span data-stu-id="48fb1-106">Capture and reuse an image</span></span>

<span data-ttu-id="48fb1-107">눈금에 대 한 기본 이미지를 Azure tooprepare에서 설정한 가상 컴퓨터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-107">You can use a virtual machine you have in Azure tooprepare a base-image for your scale set.</span></span> <span data-ttu-id="48fb1-108">이 프로세스는 크기 집합에 대 한 기본 이미지 hello로 참조할 수 있는 저장소 계정에 관리 되는 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-108">This process creates a managed disk in your storage account, which you can reference as hello base image for your scale set.</span></span> 

<span data-ttu-id="48fb1-109">다음 단계 hello 마십시오.</span><span class="sxs-lookup"><span data-stu-id="48fb1-109">Do hello following steps:</span></span>

1. <span data-ttu-id="48fb1-110">Azure 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="48fb1-110">Create an Azure Virtual Machine</span></span>
   * <span data-ttu-id="48fb1-111">[Linux][linux-vm-create]</span><span class="sxs-lookup"><span data-stu-id="48fb1-111">[Linux][linux-vm-create]</span></span>
   * <span data-ttu-id="48fb1-112">[Windows][windows-vm-create]</span><span class="sxs-lookup"><span data-stu-id="48fb1-112">[Windows][windows-vm-create]</span></span>

2. <span data-ttu-id="48fb1-113">원격으로 가상 컴퓨터를 hello 및 hello 시스템 tooyour 원하는 대로 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-113">Remote into hello virtual machine and customize hello system tooyour liking.</span></span>

   <span data-ttu-id="48fb1-114">원한다면 지금 응용 프로그램을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-114">If you want, you can install your application now.</span></span> <span data-ttu-id="48fb1-115">그러나는 이제 응용 프로그램을 설치 하 여 만들 수 있습니다 tooremove 해야 하기 때문에 더욱 복잡 한 응용 프로그램 업그레이드를 알고 그 첫 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-115">However, know that by installing your application now, you may make upgrading your application more complicated because you may need tooremove it first.</span></span> <span data-ttu-id="48fb1-116">대신, 응용 프로그램 같은 특정 런타임 또는 운영 체제 기능 할 수 있는 필수 구성 요소 단계 tooinstall이를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-116">Instead, you can use this step tooinstall any prerequisites your application may need, like a specific runtime or operating system feature.</span></span>

3. <span data-ttu-id="48fb1-117">에 대 한 hello "컴퓨터를 캡처" 자습서에 따라 [Linux] [ linux-vm-capture] 또는 [Windows][windows-vm-capture]합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-117">Follow hello "capture a machine" tutorial for either [Linux][linux-vm-capture] or [Windows][windows-vm-capture].</span></span>

4. <span data-ttu-id="48fb1-118">만들기는 [가상 컴퓨터 크기 집합] [ vmss-create] hello로 URI hello 이전 단계에서 캡처된 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-118">Create a [Virtual Machine Scale Set][vmss-create] with hello image URI you captured in hello previous step.</span></span>

<span data-ttu-id="48fb1-119">디스크에 대한 자세한 내용은 [Managed Disks 개요](../virtual-machines/windows/managed-disks-overview.md) 및 [연결된 데이터 디스크 사용](virtual-machine-scale-sets-attached-disks.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="48fb1-119">For more information about disks, see [Managed Disks Overview](../virtual-machines/windows/managed-disks-overview.md) and [Use Attached Data Disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

## <a name="install-when-hello-scale-set-is-provisioned"></a><span data-ttu-id="48fb1-120">Hello 크기 집합 프로 비전 될 때 설치</span><span class="sxs-lookup"><span data-stu-id="48fb1-120">Install when hello scale set is provisioned</span></span>

<span data-ttu-id="48fb1-121">가상 컴퓨터 확장 될 수 있습니다 tooa 가상 컴퓨터 크기 집합을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-121">Virtual machine extensions can be applied tooa virtual machine scale set.</span></span> <span data-ttu-id="48fb1-122">가상 컴퓨터 확장 hello 가상 컴퓨터 크기 집합으로 전체 그룹에에서 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-122">With a virtual machine extension, you can customize hello virtual machines in a scale set as a whole group.</span></span> <span data-ttu-id="48fb1-123">확장에 대한 자세한 내용은 [가상 컴퓨터 확장](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="48fb1-123">For more information about extensions, see [Virtual Machine Extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="48fb1-124">운영 체제가 Linux 기반인지 아니면 Windows 기반인지에 따라 세 가지 주요 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-124">There are three main extensions you can use, depending on if your operating system is Linux-based or Windows-based.</span></span>

### <a name="windows"></a><span data-ttu-id="48fb1-125">Windows</span><span class="sxs-lookup"><span data-stu-id="48fb1-125">Windows</span></span>

<span data-ttu-id="48fb1-126">Windows 기반 운영 체제에 대 한 hello 중 하나를 사용 하 여 **사용자 정의 스크립트 v1.8** 확장명 또는 hello **PowerShell DSC** 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-126">For a Windows-based operating system, use either hello **Custom Script v1.8** extension, or hello **PowerShell DSC** extension.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="48fb1-127">Custom Script</span><span class="sxs-lookup"><span data-stu-id="48fb1-127">Custom Script</span></span>

<span data-ttu-id="48fb1-128">사용자 지정 스크립트 확장 hello hello 크기 집합의 각 가상 컴퓨터 인스턴스에서 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-128">hello Custom Script extension runs a script on each virtual machine instance in hello scale set.</span></span> <span data-ttu-id="48fb1-129">구성 파일 또는 변수는 파일을 다운로드 한 toohello 가상 컴퓨터를 한 다음 명령을 실행을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-129">A config file or variable indicates which files are downloaded toohello virtual machine, and then what command runs.</span></span> <span data-ttu-id="48fb1-130">예를 들어이 toorun 설치 관리자, 스크립트, 배치 파일에서 모든 실행 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-130">You could use this toorun an installer, a script, a batch file, any executable for example.</span></span>

<span data-ttu-id="48fb1-131">PowerShell은 hello 설정에 대 한 해시 테이블을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-131">PowerShell uses a hashtable for hello settings.</span></span> <span data-ttu-id="48fb1-132">이 예제에서는 hello 사용자 지정 스크립트 확장 toorun IIS를 설치 하는 PowerShell 스크립트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-132">This example configures hello custom script extension toorun a PowerShell script that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="48fb1-133">사용 하 여 hello `-ProtectedSetting` 중요 한 정보가 포함 된 모든 설정에 대 한 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-133">Use hello `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

---------


<span data-ttu-id="48fb1-134">Azure CLI hello 설정에 대 한 json 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-134">Azure CLI uses a json file for hello settings.</span></span> <span data-ttu-id="48fb1-135">이 예제에서는 hello 사용자 지정 스크립트 확장 toorun IIS를 설치 하는 PowerShell 스크립트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-135">This example configures hello custom script extension toorun a PowerShell script that installs IIS.</span></span> <span data-ttu-id="48fb1-136">다음으로 json 파일 hello 저장 _settings.json_합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-136">Save hello following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

<span data-ttu-id="48fb1-137">그런 다음 이 Azure CLI 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-137">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="48fb1-138">사용 하 여 hello `--protected-settings` 중요 한 정보가 포함 된 모든 설정에 대 한 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-138">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="powershell-dsc"></a><span data-ttu-id="48fb1-139">PowerShell DSC</span><span class="sxs-lookup"><span data-stu-id="48fb1-139">PowerShell DSC</span></span>

<span data-ttu-id="48fb1-140">PowerShell DSC toocustomize hello 눈금 집합 vm 인스턴스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-140">You can use PowerShell DSC toocustomize hello scale set vm instances.</span></span> <span data-ttu-id="48fb1-141">hello **DSC** 확장 공개한 **Microsoft.Powershell** 배포 하 고 각 가상 컴퓨터 인스턴스에서 제공 하는 hello DSC 구성을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-141">hello **DSC** extension published by **Microsoft.Powershell** deploys and runs hello provided DSC configuration on each virtual machine instance.</span></span> <span data-ttu-id="48fb1-142">구성 파일 또는 변수 hello 확장을 알려 줍니다 여기서 *.zip* 패키지는 이며 _스크립트 함수_ 조합 toorun 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-142">A config file or variable tells hello extension where *.zip* package is, and which _script-function_ combination toorun.</span></span>

<span data-ttu-id="48fb1-143">PowerShell은 hello 설정에 대 한 해시 테이블을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-143">PowerShell uses a hashtable for hello settings.</span></span> <span data-ttu-id="48fb1-144">이 예제에서는 IIS를 설치하는 DSC 패키지를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-144">This example deploys a DSC package that installs IIS.</span></span>

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

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="48fb1-145">사용 하 여 hello `-ProtectedSetting` 중요 한 정보가 포함 된 모든 설정에 대 한 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-145">Use hello `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

-----------

<span data-ttu-id="48fb1-146">Azure CLI hello 설정에 대 한 json을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-146">Azure CLI uses a json for hello settings.</span></span> <span data-ttu-id="48fb1-147">이 예제에서는 IIS를 설치하는 DSC 패키지를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-147">This example deploys a DSC package that installs IIS.</span></span> <span data-ttu-id="48fb1-148">다음으로 json 파일 hello 저장 _settings.json_합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-148">Save hello following json file as _settings.json_.</span></span>

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

<span data-ttu-id="48fb1-149">그런 다음 이 Azure CLI 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-149">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="48fb1-150">사용 하 여 hello `--protected-settings` 중요 한 정보가 포함 된 모든 설정에 대 한 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-150">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="linux"></a><span data-ttu-id="48fb1-151">Linux</span><span class="sxs-lookup"><span data-stu-id="48fb1-151">Linux</span></span>

<span data-ttu-id="48fb1-152">Linux 어느 hello צ ְ ײ **사용자 정의 스크립트 v2.0** 확장 또는 사용 하 여 **클라우드 init** 를 만드는 동안 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-152">Linux can use either hello **Custom Script v2.0** extension or use **cloud-init** during creation.</span></span>

<span data-ttu-id="48fb1-153">사용자 지정 스크립트는 파일 toohello 가상 컴퓨터 인스턴스를 다운로드 하 고 명령을 실행 하는 간단한 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-153">Custom script is a simple extension that downloads files toohello virtual machine instances, and runs a command.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="48fb1-154">Custom Script</span><span class="sxs-lookup"><span data-stu-id="48fb1-154">Custom Script</span></span>

<span data-ttu-id="48fb1-155">다음으로 json 파일 hello 저장 _settings.json_합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-155">Save hello following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

<span data-ttu-id="48fb1-156">기존 가상 컴퓨터 크기 집합 확장 tooan이 Azure CLI tooadd hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-156">Use hello Azure CLI tooadd this extension tooan existing virtual machine scale set.</span></span> <span data-ttu-id="48fb1-157">Hello 규모에 맞게 각 가상 컴퓨터 실행 hello 확장명이 자동으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-157">Each virtual machine in hello scale set automatically runs hello extension.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="48fb1-158">사용 하 여 hello `--protected-settings` 중요 한 정보가 포함 된 모든 설정에 대 한 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-158">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

#### <a name="cloud-init"></a><span data-ttu-id="48fb1-159">Cloud-Init</span><span class="sxs-lookup"><span data-stu-id="48fb1-159">Cloud-Init</span></span>

<span data-ttu-id="48fb1-160">클라우드 Init hello 눈금 세트를 만들 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-160">Cloud-Init is used when hello scale set is created.</span></span> <span data-ttu-id="48fb1-161">첫째, 명명 된 로컬 파일을 만들 _클라우드 init.txt_ 구성 tooit 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-161">First, create a local file named _cloud-init.txt_ and add your configuration tooit.</span></span> <span data-ttu-id="48fb1-162">예제는 [이 gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="48fb1-162">For example, see [this gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span></span>

<span data-ttu-id="48fb1-163">사용 하 여 hello Azure CLI toocreate 소수 자릿수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-163">Use hello Azure CLI toocreate a scale set.</span></span> <span data-ttu-id="48fb1-164">hello `--custom-data` 필드에서 클라우드 초기화 스크립트의 hello 파일 이름을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-164">hello `--custom-data` field accepts hello file name of a cloud-init script.</span></span>

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

## <a name="how-do-i-manage-application-updates"></a><span data-ttu-id="48fb1-165">응용 프로그램 업데이트를 관리하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="48fb1-165">How do I manage application updates?</span></span>

<span data-ttu-id="48fb1-166">확장을 통해 응용 프로그램을 배포한 경우 어떤 방식으로든에서 hello 확장 정의 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-166">If you deployed your application through an extension, alter hello extension definition in some way.</span></span> <span data-ttu-id="48fb1-167">이러한 변경으로 인해 hello 확장 재배포 toobe tooall 가상 컴퓨터 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="48fb1-167">This change causes hello extension toobe redeployed tooall virtual machine instances.</span></span> <span data-ttu-id="48fb1-168">무언가 **해야** Azure가 확장 hello 표시 하지 않으려면 변경, 참조 된 파일 이름 바꾸기와 같은 hello 확장에 대 한 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-168">Something **must** be changed about hello extension, such as renaming a referenced file, otherwise, Azure does not see that hello extension has changed.</span></span>

<span data-ttu-id="48fb1-169">사용자 고유의 운영 체제 이미지에 hello 응용 프로그램을 반영 하는 경우 응용 프로그램 업데이트에 대 한 자동화 된 배포 파이프라인을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-169">If you baked hello application into your own operating system image, use an automated deployment pipeline for application updates.</span></span> <span data-ttu-id="48fb1-170">프로덕션 환경으로 설정 하는 준비 된 눈금으로 교체 신속한 아키텍처 toofacilitate 프로그램을 디자인 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-170">Design your architecture toofacilitate rapid swapping of a staged scale set into production.</span></span> <span data-ttu-id="48fb1-171">이 방법의 좋은 예는 hello [Azure Spinnaker 드라이버 작업](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/)합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-171">A good example of this approach is hello [Azure Spinnaker driver work](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span></span>

<span data-ttu-id="48fb1-172">[Packer](https://www.packer.io/) 및 [Terraform](https://www.terraform.io/) 지원 Azure 리소스 관리자도 "code" 다른 이름으로 이미지를 정의 하 고 Azure에서 빌드할 수 있도록 hello VHD 크기 집합의 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-172">[Packer](https://www.packer.io/) and [Terraform](https://www.terraform.io/) support Azure Resource Manager, so you can also define your images "as code" and build them in Azure, then use hello VHD in your scale set.</span></span> <span data-ttu-id="48fb1-173">그러나 사용자가 Marketplace에서 직접 조작하지 않으므로 확장/사용자 지정 스크립트가 좀 더 중요한 경우 이렇게 하면 Marketplace 이미지에 문제가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-173">However, doing so would become problematic for marketplace images, where extensions/custom scripts become more important since you don’t directly manipulate bits from marketplace.</span></span>

## <a name="what-happens-when-a-scale-set-scales-out"></a><span data-ttu-id="48fb1-174">확장 집합이 확장되면 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="48fb1-174">What happens when a scale set scales out?</span></span>
<span data-ttu-id="48fb1-175">하나 이상의 가상 컴퓨터 tooa 크기 집합에 추가 하면 hello 응용 프로그램은 자동으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-175">When you add one or more virtual machines tooa scale set, hello application is automatically installed.</span></span> <span data-ttu-id="48fb1-176">예제 hello 크기 조정 설정에 정의 된 확장에 대 한 실행 새 가상 컴퓨터에 생성 될 때마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-176">For example if hello scale set has extensions defined, they run on a new virtual machine each time it is created.</span></span> <span data-ttu-id="48fb1-177">Hello 크기 집합 사용자 지정 이미지를 기반 하는 경우 모든 새 가상 컴퓨터는 hello 원본 사용자 지정 이미지의 복사본을입니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-177">If hello scale set is based on a custom image, any new virtual machine is a copy of hello source custom image.</span></span> <span data-ttu-id="48fb1-178">Hello 눈금 집합 가상 컴퓨터는 컨테이너 호스트를 시작 코드 tooload hello 컨테이너를 사용자 지정 스크립트 확장에서 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-178">If hello scale set virtual machines are container hosts, then you might have startup code tooload hello containers in a Custom Script Extension.</span></span> <span data-ttu-id="48fb1-179">또는 확장이 클러스터 조정자에 등록하는 Azure Container Service 같은 에이전트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-179">Or, an extension might install an agent that registers with a cluster orchestrator, such as Azure Container Service.</span></span>


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a><span data-ttu-id="48fb1-180">업데이트 도메인 간에 OS 업데이트를 롤아웃하려면 어떻게 해야 할까요?</span><span class="sxs-lookup"><span data-stu-id="48fb1-180">How do you roll out an OS update across update domains?</span></span>
<span data-ttu-id="48fb1-181">Tooupdate 한다고 가정 hello 가상 컴퓨터 크기를 유지 하면서 OS 이미지는 실행을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-181">Suppose you want tooupdate your OS image while keeping hello virtual machine scale set running.</span></span> <span data-ttu-id="48fb1-182">PowerShell 및 Azure CLI hello hello 가상 컴퓨터 이미지를 한 번에 하나의 가상 컴퓨터를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-182">PowerShell and hello Azure CLI can update hello virtual machine images, one virtual machine at a time.</span></span> <span data-ttu-id="48fb1-183">hello [가상 컴퓨터 크기 집합 업그레이드](./virtual-machine-scale-sets-upgrade-scale-set.md) 도 문서에 있는 가상 컴퓨터 크기 집합에서 운영 체제를 업그레이드 하는 사용 가능한 tooperform 옵션과 각 옵션의 추가 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-183">hello [Upgrade a Virtual Machine Scale Set](./virtual-machine-scale-sets-upgrade-scale-set.md) article also provides further information on what options are available tooperform an operating system upgrade across a virtual machine scale set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48fb1-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="48fb1-184">Next steps</span></span>

* [<span data-ttu-id="48fb1-185">PowerShell toomanage를 사용 하 여 크기 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="48fb1-185">Use PowerShell toomanage your scale set.</span></span>](virtual-machine-scale-sets-windows-manage.md)
* [<span data-ttu-id="48fb1-186">확장 집합 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="48fb1-186">Create a scale set template.</span></span>](virtual-machine-scale-sets-mvss-start.md)


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

