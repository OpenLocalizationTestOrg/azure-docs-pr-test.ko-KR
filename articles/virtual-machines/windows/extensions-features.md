---
title: "Azure에서 Windows용 가상 컴퓨터 확장 및 기능 | Microsoft Docs"
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
ms.openlocfilehash: 1ce0eebd2585c9457d7f922898d7f2fa3e7ffad7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="virtual-machine-extensions-and-features-for-windows"></a><span data-ttu-id="d9639-103">Windows용 가상 컴퓨터 확장 및 기능</span><span class="sxs-lookup"><span data-stu-id="d9639-103">Virtual machine extensions and features for Windows</span></span>

<span data-ttu-id="d9639-104">Azure Virtual Machines 확장은 Azure Virtual Machines에서 배포 후 구성 및 Automation 작업을 제공하는 작은 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="d9639-105">예를 들어 가상 컴퓨터에서 소프트웨어가 설치되도록 요구하거나, 바이러스 백신 보호 또는 Docker 구성을 요구하는 경우 VM 확장을 사용하여 이러한 작업을 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used to complete these tasks.</span></span> <span data-ttu-id="d9639-106">Azure CLI, PowerShell, Azure Resource Manager 템플릿 및 Azure Portal을 사용하여 Azure VM 확장을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-106">Azure VM extensions can be run by using the Azure CLI, PowerShell, Azure Resource Manager templates, and the Azure portal.</span></span> <span data-ttu-id="d9639-107">확장을 새 가상 컴퓨터 배포와 번들로 제공하거나 기존 시스템에 대해 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-107">Extensions can be bundled with a new virtual machine deployment or run against any existing system.</span></span>

<span data-ttu-id="d9639-108">이 문서에서는 가상 컴퓨터 확장의 개요, 가상 컴퓨터 확장 사용을 위한 필수 구성 요소, 가상 컴퓨터 확장을 검색, 관리 및 제거하는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-108">This document provides an overview of virtual machine extensions, prerequisites for using virtual machine extensions, and guidance on how to detect, manage, and remove virtual machine extensions.</span></span> <span data-ttu-id="d9639-109">많은 VM 확장 각각을 고유한 구성으로 사용할 수 있으므로 여기서는 일반적인 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="d9639-110">확장 관련 세부 정보는 개별 확장과 관련된 각 문서에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-110">Extension-specific details can be found in each document specific to the individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="d9639-111">사용 사례 및 샘플</span><span class="sxs-lookup"><span data-stu-id="d9639-111">Use cases and samples</span></span>

<span data-ttu-id="d9639-112">각각 특정 사용 사례가 있는 많은 다양한 Azure VM 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-112">There are many different Azure VM extensions available, each with a specific use case.</span></span> <span data-ttu-id="d9639-113">예제 사용 사례:</span><span class="sxs-lookup"><span data-stu-id="d9639-113">Some example use cases are:</span></span>

- <span data-ttu-id="d9639-114">Windows용 DSC 확장을 사용하여 가상 컴퓨터에 PowerShell의 필요한 상태 구성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-114">Apply PowerShell Desired State configurations to a virtual machine by using the DSC extension for Windows.</span></span> <span data-ttu-id="d9639-115">자세한 내용은 [Azure 필요한 상태 구성 확장](extensions-dsc-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9639-115">For more information, see [Azure Desired State configuration extension](extensions-dsc-overview.md).</span></span>
- <span data-ttu-id="d9639-116">Microsoft Monitoring Agent VM 확장을 사용하여 가상 컴퓨터 모니터링을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-116">Configure virtual machine monitoring by using the Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="d9639-117">자세한 내용은 [Log Analytics에 Azure Virtual Machines 연결](../../log-analytics/log-analytics-azure-vm-extension.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9639-117">For more information, see [Connect Azure virtual machines to Log Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="d9639-118">Datadog 확장으로 Azure 인프라의 모니터링을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-118">Configure monitoring of your Azure infrastructure with the Datadog extension.</span></span> <span data-ttu-id="d9639-119">자세한 내용은 [Datadog 블로그](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9639-119">For more information, see the [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="d9639-120">Chef를 사용하여 Azure Virtual Machine을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-120">Configure an Azure virtual machine by using Chef.</span></span> <span data-ttu-id="d9639-121">자세한 내용은 [Chef를 사용하여 Azure 가상 컴퓨터 배포 자동화](chef-automation.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9639-121">For more information, see [Automating Azure virtual machine deployment with Chef](chef-automation.md).</span></span>

<span data-ttu-id="d9639-122">프로세스 관련 확장 외에도 Windows 및 Linux 가상 컴퓨터에 대해 사용자 지정 스크립트 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-122">In addition to process-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="d9639-123">Windows용 사용자 지정 스크립트 확장을 사용하면 PowerShell 스크립트를 가상 컴퓨터에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-123">The Custom Script extension for Windows allows any PowerShell script to be run on a virtual machine.</span></span> <span data-ttu-id="d9639-124">이 확장은 네이티브 Azure 도구로 제공할 수 있는 것 이상의 구성이 필요한 Azure 배포를 디자인할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-124">This is useful when you're designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="d9639-125">자세한 내용은 [Windows VM 사용자 지정 스크립트 확장](extensions-customscript.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9639-125">For more information, see [Windows VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="d9639-126">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d9639-126">Prerequisites</span></span>

<span data-ttu-id="d9639-127">각 가상 컴퓨터 확장에는 고유한 필수 구성 요소 집합이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-127">Each virtual machine extension may have its own set of prerequisites.</span></span> <span data-ttu-id="d9639-128">예를 들어 Docker VM 확장에는 지원되는 Linux 배포판의 필수 구성 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-128">For instance, the Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="d9639-129">개별 확장의 요구 사항에 대해서는 확장 관련 설명서에 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-129">Requirements of individual extensions are detailed in the extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="d9639-130">Azure VM 에이전트</span><span class="sxs-lookup"><span data-stu-id="d9639-130">Azure VM agent</span></span>
<span data-ttu-id="d9639-131">Azure VM 에이전트는 Azure Virtual Machine과 Azure 패브릭 컨트롤러 간 상호 작용을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-131">The Azure VM agent manages interaction between an Azure virtual machine and the Azure fabric controller.</span></span> <span data-ttu-id="d9639-132">VM 에이전트는 VM 확장 실행을 포함하여 Azure Virtual Machine 배포 및 관리의 다양한 기능적 측면을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-132">The VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="d9639-133">Azure VM 에이전트는 Azure Marketplace 이미지에 미리 설치되며 지원되는 운영 체제에 설치될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-133">The Azure VM agent is preinstalled on Azure Marketplace images and can be installed on supported operating systems.</span></span>

<span data-ttu-id="d9639-134">지원되는 운영 체제 및 설치 지침에 대한 자세한 내용은 [Azure Virtual Machines 에이전트](agent-user-guide.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9639-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](agent-user-guide.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="d9639-135">VM 확장 검색</span><span class="sxs-lookup"><span data-stu-id="d9639-135">Discover VM extensions</span></span>
<span data-ttu-id="d9639-136">Azure Virtual Machine와 함께 여러 다양한 VM 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="d9639-137">전체 목록을 보려면 Azure Resource Manager PowerShell 모듈을 사용하여 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-137">To see a complete list, run the following command with the Azure Resource Manager PowerShell module.</span></span> <span data-ttu-id="d9639-138">이 명령을 실행하는 경우 원하는 위치를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-138">Make sure to specify the desired location when you're running this command.</span></span>

```powershell
Get-AzureRmVmImagePublisher -Location WestUS | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```

## <a name="run-vm-extensions"></a><span data-ttu-id="d9639-139">VM 확장 실행</span><span class="sxs-lookup"><span data-stu-id="d9639-139">Run VM extensions</span></span>

<span data-ttu-id="d9639-140">Azure Virtual Machines 확장은 기존 가상 컴퓨터에서 실행할 수 있습니다. 이러한 기능은 이미 배포한 VM의 구성을 변경하거나 연결을 복구해야 할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-140">Azure virtual machine extensions can be run on existing virtual machines, which is useful when you need to make configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="d9639-141">또한 VM 확장을 Azure Resource Manager 템플릿 배포와 번들로 묶을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-141">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="d9639-142">Resource Manager 템플릿에서 확장을 사용하면 Azure Virtual Machine을 배포하고, 배포 후 개입할 필요 없이 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-142">By using extensions with Resource Manager templates, you can enable Azure virtual machines to be deployed and configured without the need for post-deployment intervention.</span></span>

<span data-ttu-id="d9639-143">다음 방법을 사용하여 기존 가상 컴퓨터에 대해 확장을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-143">The following methods can be used to run an extension against an existing virtual machine.</span></span>

### <a name="powershell"></a><span data-ttu-id="d9639-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9639-144">PowerShell</span></span>

<span data-ttu-id="d9639-145">개별 확장을 실행하기 위한 몇 가지 PowerShell 명령이 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-145">Several PowerShell commands exist for running individual extensions.</span></span> <span data-ttu-id="d9639-146">목록을 보려면 다음 PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-146">To see a list, run the following PowerShell commands.</span></span>

```powershell
get-command Set-AzureRM*Extension* -Module AzureRM.Compute
```

<span data-ttu-id="d9639-147">다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-147">This provides output similar to the following:</span></span>

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

<span data-ttu-id="d9639-148">다음 예제에서는 사용자 지정 스크립트 확장을 사용하여 GitHub 리포지토리에서 대상 가상 컴퓨터에 스크립트를 다운로드한 후 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-148">The following example uses the Custom Script extension to download a script from a GitHub repository onto the target virtual machine and then run the script.</span></span> <span data-ttu-id="d9639-149">사용자 지정 스크립트 확장에 대한 자세한 내용은 [사용자 지정 스크립트 확장 개요](extensions-customscript.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9639-149">For more information on the Custom Script extension, see [Custom Script extension overview](extensions-customscript.md).</span></span>

```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" -Name "myCustomScript" `
    -FileUri "https://raw.githubusercontent.com/neilpeterson/nepeters-azure-templates/master/windows-custom-script-simple/support-scripts/Create-File.ps1" `
    -Run "Create-File.ps1" -Location "West US"
```

<span data-ttu-id="d9639-150">이 예제에서는 Windows 가상 컴퓨터의 관리자 암호를 다시 설정하기 위해 VM 액세스 확장이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-150">In this example, the VM Access extension is used to reset the administrative password of a Windows virtual machine.</span></span> <span data-ttu-id="d9639-151">VM 액세스 확장에 대한 자세한 내용은 [Windows VM에서 원격 데스크톱 서비스 다시 설정](reset-rdp.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9639-151">For more information on the VM Access extension, see [Reset Remote Desktop service in a Windows VM](reset-rdp.md).</span></span>

```powershell
$cred=Get-Credential

Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" -Name "myVMAccess" `
    -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

<span data-ttu-id="d9639-152">`Set-AzureRmVMExtension` 명령을 사용하여 VM 확장을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-152">The `Set-AzureRmVMExtension` command can be used to start any VM extension.</span></span> <span data-ttu-id="d9639-153">자세한 내용은 [Set-AzureRmVMExtension 참조](https://msdn.microsoft.com/en-us/library/mt603745.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9639-153">For more information, see the [Set-AzureRmVMExtension reference](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span></span>


### <a name="azure-portal"></a><span data-ttu-id="d9639-154">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="d9639-154">Azure portal</span></span>

<span data-ttu-id="d9639-155">Azure Portal을 통해 기존 가상 컴퓨터에 VM 확장을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-155">A VM extension can be applied to an existing virtual machine through the Azure portal.</span></span> <span data-ttu-id="d9639-156">이렇게 하려면 사용하려는 가상 컴퓨터를 선택하고 **확장**을 선택한 후 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-156">To do so, select the virtual machine you want to use, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="d9639-157">그러면 사용 가능한 확장 목록이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-157">This provides a list of available extensions.</span></span> <span data-ttu-id="d9639-158">원하는 확장을 선택하고 마법사의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-158">Select the one you want and follow the steps in the wizard.</span></span>

<span data-ttu-id="d9639-159">다음 이미지는 Azure Portal에서 Microsoft 맬웨어 방지 확장을 설치하는 경우를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-159">The following image shows the installation of the Microsoft Antimalware extension from the Azure portal.</span></span>

![Install antimalware extension](./media/extensions-features/installantimalwareextension.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="d9639-161">Azure 리소스 관리자 템플릿</span><span class="sxs-lookup"><span data-stu-id="d9639-161">Azure Resource Manager templates</span></span>

<span data-ttu-id="d9639-162">Azure Resource Manager 템플릿에 VM 확장을 추가하고 템플릿 배포를 통해 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-162">VM extensions can be added to an Azure Resource Manager template and executed with the deployment of the template.</span></span> <span data-ttu-id="d9639-163">템플릿 사용하여 확장을 배포하는 방식은 완전히 구성된 Azure 배포를 만드는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-163">Deploying extensions with a template is useful for creating fully configured Azure deployments.</span></span> <span data-ttu-id="d9639-164">예를 들어 다음 JSON은 부하 분산된 가상 컴퓨터 집합 및 Azure SQL Database를 배포한 후 각 VM에 .NET Core 응용 프로그램을 설치하는 Resource Manager 템플릿에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-164">For example, the following JSON is taken from a Resource Manager template that deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="d9639-165">VM 확장은 소프트웨어 설치를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-165">The VM extension takes care of the software installation.</span></span>

<span data-ttu-id="d9639-166">자세한 내용은 전체 [Resource Manager 템플릿](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9639-166">For more information, see the [full Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

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

<span data-ttu-id="d9639-167">자세한 내용은 [Windows VM 확장을 사용하여 Azure Resource Manager 템플릿 작성](template-description.md#extensions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9639-167">For more information, see [Authoring Azure Resource Manager templates with Windows VM extensions](template-description.md#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="d9639-168">VM 확장 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="d9639-168">Secure VM extension data</span></span>

<span data-ttu-id="d9639-169">VM 확장을 실행하는 경우 자격 증명, 저장소 계정 이름 및 저장소 계정 액세스 키와 같은 중요한 정보를 포함해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-169">When you're running a VM extension, it may be necessary to include sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="d9639-170">많은 VM 확장에는 데이터를 암호화하고 대상 가상 컴퓨터 내에서만 해독하는 보호된 구성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-170">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside the target virtual machine.</span></span> <span data-ttu-id="d9639-171">각 확장에는 보호되는 특정 구성 스키마가 있으며 각각은 확장 관련 설명서에 자세히 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-171">Each extension has a specific protected configuration schema that will be detailed in extension-specific documentation.</span></span>

<span data-ttu-id="d9639-172">다음 예제에서는 Windows용 사용자 지정 스크립트 확장의 인스턴스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-172">The following example shows an instance of the Custom Script extension for Windows.</span></span> <span data-ttu-id="d9639-173">실행할 명령에는 자격 증명 집합이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-173">Notice that the command to execute includes a set of credentials.</span></span> <span data-ttu-id="d9639-174">이 예제에서는 실행할 명령이 암호화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-174">In this example, the command to execute will not be encrypted.</span></span>


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

<span data-ttu-id="d9639-175">**실행할 명령** 속성을 **보호됨** 구성으로 이동하여 실행 문자열을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-175">Secure the execution string by moving the **command to execute** property to the **protected** configuration.</span></span>

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

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="d9639-176">VM 확장 문제 해결</span><span class="sxs-lookup"><span data-stu-id="d9639-176">Troubleshoot VM extensions</span></span>

<span data-ttu-id="d9639-177">각 VM 확장에는 특정 문제 해결 단계가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-177">Each VM extension may have specific troubleshooting steps.</span></span> <span data-ttu-id="d9639-178">예를 들어 사용자 지정 스크립트 확장을 사용하는 경우 확장이 실행된 가상 컴퓨터에서 로컬로 스크립트 실행 세부 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-178">For instance, when you're using the Custom Script extension, script execution details can be found locally on the virtual machine on which the extension was run.</span></span> <span data-ttu-id="d9639-179">확장별 문제 해결 단계는 확장 관련 설명서에 자세히 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-179">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="d9639-180">다음 문제 해결 단계는 모든 가상 컴퓨터 확장에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-180">The following troubleshooting steps apply to all virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="d9639-181">확장 상태 보기</span><span class="sxs-lookup"><span data-stu-id="d9639-181">View extension status</span></span>

<span data-ttu-id="d9639-182">가상 컴퓨터에 대해 가상 컴퓨터 확장을 실행한 후에 다음 PowerShell 명령을 사용하여 확장 상태를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-182">After a virtual machine extension has been run against a virtual machine, use the following PowerShell command to return extension status.</span></span> <span data-ttu-id="d9639-183">매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-183">Replace example parameter names with your own values.</span></span> <span data-ttu-id="d9639-184">`Name` 매개 변수는 실행 시 확장에 지정된 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-184">The `Name` parameter takes the name given to the extension at execution time.</span></span>

```PowerShell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="d9639-185">출력은 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-185">The output looks like the following:</span></span>

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

<span data-ttu-id="d9639-186">Azure Portal에서 확장 실행 상태를 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-186">Extension execution status can also be found in the Azure portal.</span></span> <span data-ttu-id="d9639-187">확장의 상태를 확인하려면 가상 컴퓨터를 선택하고 **확장**을 선택한 후 원하는 확장을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-187">To view the status of an extension, select the virtual machine, choose **Extensions**, and select the desired extension.</span></span>

### <a name="rerun-vm-extensions"></a><span data-ttu-id="d9639-188">VM 확장 다시 실행</span><span class="sxs-lookup"><span data-stu-id="d9639-188">Rerun VM extensions</span></span>

<span data-ttu-id="d9639-189">가상 컴퓨터 확장을 다시 실행해야 하는 경우가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-189">There may be cases in which a virtual machine extension needs to be rerun.</span></span> <span data-ttu-id="d9639-190">이를 위해 확장을 제거한 다음 원하는 실행 방법으로 확장을 다시 실행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-190">You can do this by removing the extension and then rerunning the extension with an execution method of your choice.</span></span> <span data-ttu-id="d9639-191">확장을 제거하려면 Azure PowerShell 모듈을 사용하여 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-191">To remove an extension, run the following command with the Azure PowerShell module.</span></span> <span data-ttu-id="d9639-192">매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-192">Replace example parameter names with your own values.</span></span>

```powershell
Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="d9639-193">Azure Portal을 사용하여 확장을 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-193">An extension can also be removed using the Azure portal.</span></span> <span data-ttu-id="d9639-194">이렇게 하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-194">To do so:</span></span>

1. <span data-ttu-id="d9639-195">가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-195">Select a virtual machine.</span></span>
2. <span data-ttu-id="d9639-196">**확장**을 섡택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-196">Select **Extensions**.</span></span>
3. <span data-ttu-id="d9639-197">원하는 확장을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-197">Choose the desired extension.</span></span>
4. <span data-ttu-id="d9639-198">**제거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9639-198">Select **Uninstall**.</span></span>

## <a name="common-vm-extensions-reference"></a><span data-ttu-id="d9639-199">일반 VM 확장 참조</span><span class="sxs-lookup"><span data-stu-id="d9639-199">Common VM extensions reference</span></span>
| <span data-ttu-id="d9639-200">확장 이름</span><span class="sxs-lookup"><span data-stu-id="d9639-200">Extension name</span></span> | <span data-ttu-id="d9639-201">설명</span><span class="sxs-lookup"><span data-stu-id="d9639-201">Description</span></span> | <span data-ttu-id="d9639-202">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="d9639-202">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d9639-203">Windows용 사용자 지정 스크립트 확장</span><span class="sxs-lookup"><span data-stu-id="d9639-203">Custom Script Extension for Windows</span></span> |<span data-ttu-id="d9639-204">Azure Virtual Machine에 대해 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="d9639-204">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="d9639-205">Windows용 사용자 지정 스크립트 확장</span><span class="sxs-lookup"><span data-stu-id="d9639-205">Custom Script Extension for Windows</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="d9639-206">Windows용 DSC 확장</span><span class="sxs-lookup"><span data-stu-id="d9639-206">DSC Extension for Windows</span></span> |<span data-ttu-id="d9639-207">PowerShell DSC(Desired State Configuration) 확장</span><span class="sxs-lookup"><span data-stu-id="d9639-207">PowerShell DSC (Desired State Configuration) Extension</span></span> |[<span data-ttu-id="d9639-208">Windows용 DSC 확장</span><span class="sxs-lookup"><span data-stu-id="d9639-208">DSC Extension for Windows</span></span>](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="d9639-209">Azure 진단 확장</span><span class="sxs-lookup"><span data-stu-id="d9639-209">Azure Diagnostics Extension</span></span> |<span data-ttu-id="d9639-210">Azure 진단 관리</span><span class="sxs-lookup"><span data-stu-id="d9639-210">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="d9639-211">Azure 진단 확장</span><span class="sxs-lookup"><span data-stu-id="d9639-211">Azure Diagnostics Extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="d9639-212">Azure VM 액세스 확장</span><span class="sxs-lookup"><span data-stu-id="d9639-212">Azure VM Access Extension</span></span> |<span data-ttu-id="d9639-213">사용자 및 자격 증명 관리</span><span class="sxs-lookup"><span data-stu-id="d9639-213">Manage users and credentials</span></span> |[<span data-ttu-id="d9639-214">Linux용 VM 액세스 확장</span><span class="sxs-lookup"><span data-stu-id="d9639-214">VM Access Extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
