---
title: "Linux용 가상 컴퓨터 확장 및 기능 | Microsoft Docs"
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
ms.openlocfilehash: 8a5b39351f665c51ae7d83f755329e54ff3cf786
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="virtual-machine-extensions-and-features-for-linux"></a><span data-ttu-id="169a1-103">Linux용 가상 컴퓨터 확장 및 기능</span><span class="sxs-lookup"><span data-stu-id="169a1-103">Virtual machine extensions and features for Linux</span></span>

<span data-ttu-id="169a1-104">Azure Virtual Machines 확장은 Azure Virtual Machines에서 배포 후 구성 및 Automation 작업을 제공하는 작은 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="169a1-105">예를 들어 가상 컴퓨터에서 소프트웨어가 설치되도록 요구하거나, 바이러스 백신 보호 또는 Docker 구성을 요구하는 경우 VM 확장을 사용하여 이러한 작업을 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used to complete these tasks.</span></span> <span data-ttu-id="169a1-106">Azure CLI, PowerShell, Azure Resource Manager 템플릿 및 Azure Portal을 사용하여 Azure VM 확장을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-106">Azure VM extensions can be run using the Azure CLI, PowerShell, Azure Resource Manager templates, and the Azure portal.</span></span> <span data-ttu-id="169a1-107">확장을 새 가상 컴퓨터 배포와 번들로 제공하거나 기존 시스템에 대해 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-107">Extensions can be bundled with a new virtual machine deployment, or run against any existing system.</span></span>

<span data-ttu-id="169a1-108">이 문서에서는 VM 확장의 개요, Azure VM 확장 사용을 위한 필수 구성 요소, VM 확장을 검색, 관리 및 제거하는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-108">This document provides an overview of VM extensions, prerequisites for using Azure VM extensions, and guidance on how to detect, manage, and remove VM extensions.</span></span> <span data-ttu-id="169a1-109">많은 VM 확장 각각을 고유한 구성으로 사용할 수 있으므로 여기서는 일반적인 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="169a1-110">확장 관련 세부 정보는 개별 확장과 관련된 각 문서에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-110">Extension-specific details can be found in each document specific to the individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="169a1-111">사용 사례 및 샘플</span><span class="sxs-lookup"><span data-stu-id="169a1-111">Use cases and samples</span></span>

<span data-ttu-id="169a1-112">각각 특정 사용 사례가 있는 몇 가지 다른 Azure VM 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-112">Several different Azure VM extensions are available, each with a specific use case.</span></span> <span data-ttu-id="169a1-113">일부 사례:</span><span class="sxs-lookup"><span data-stu-id="169a1-113">Some examples are:</span></span>

- <span data-ttu-id="169a1-114">Linux용 DSC 확장을 사용하여 가상 컴퓨터에 PowerShell의 필요한 상태 구성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-114">Apply PowerShell Desired State configurations to a virtual machine using the DSC extension for Linux.</span></span> <span data-ttu-id="169a1-115">자세한 내용은 [Azure 필요한 상태 구성 확장](https://github.com/Azure/azure-linux-extensions/tree/master/DSC)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="169a1-115">For more information, see [Azure Desired State configuration extension](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).</span></span>
- <span data-ttu-id="169a1-116">Microsoft Monitoring Agent VM 확장을 사용하여 가상 컴퓨터의 모니터링을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-116">Configure monitoring of a virtual machine with the Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="169a1-117">자세한 내용은 [Linux VM을 모니터링하는 방법](tutorial-monitoring.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="169a1-117">For more information, see [How to monitor a Linux VM](tutorial-monitoring.md).</span></span>
- <span data-ttu-id="169a1-118">Datadog 확장으로 Azure 인프라의 모니터링을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-118">Configure monitoring of your Azure infrastructure with the Datadog extension.</span></span> <span data-ttu-id="169a1-119">자세한 내용은 [Datadog 블로그](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="169a1-119">For more information, see the [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="169a1-120">Docker VM 확장을 사용하여 Azure Virtual Machine에서 Docker 호스트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-120">Configure a Docker host on an Azure virtual machine using the Docker VM extension.</span></span> <span data-ttu-id="169a1-121">자세한 내용은 [Docker VM 확장](dockerextension.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="169a1-121">For more information, see [Docker VM extension](dockerextension.md).</span></span>

<span data-ttu-id="169a1-122">프로세스 관련 확장 외에도 Windows 및 Linux 가상 컴퓨터에 대해 사용자 지정 스크립트 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-122">In addition to process-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="169a1-123">Linux용 사용자 지정 스크립트 확장을 사용하면 Bash 스크립트를 가상 컴퓨터에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-123">The Custom Script extension for Linux allows any Bash script to be run on a virtual machine.</span></span> <span data-ttu-id="169a1-124">사용자 지정 스크립트는 네이티브 Azure 도구로 제공할 수 있는 것 이상의 구성이 필요한 Azure 배포를 디자인할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-124">Custom scripts are useful for designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="169a1-125">자세한 내용은 [Linux VM 사용자 지정 스크립트 확장](extensions-customscript.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="169a1-125">For more information, see [Linux VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="169a1-126">필수 조건</span><span class="sxs-lookup"><span data-stu-id="169a1-126">Prerequisites</span></span>

<span data-ttu-id="169a1-127">각 가상 컴퓨터 확장에는 고유한 필수 구성 요소 집합이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-127">Each virtual machine extension might have its own set of prerequisites.</span></span> <span data-ttu-id="169a1-128">예를 들어 Docker VM 확장에는 지원되는 Linux 배포판의 필수 구성 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-128">For instance, the Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="169a1-129">개별 확장의 요구 사항에 대해서는 확장 관련 설명서에 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-129">Requirements of individual extensions are detailed in the extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="169a1-130">Azure VM 에이전트</span><span class="sxs-lookup"><span data-stu-id="169a1-130">Azure VM agent</span></span>

<span data-ttu-id="169a1-131">Azure VM 에이전트는 Azure Virtual Machine과 Azure 패브릭 컨트롤러 간 상호 작용을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-131">The Azure VM agent manages interactions between an Azure virtual machine and the Azure fabric controller.</span></span> <span data-ttu-id="169a1-132">VM 에이전트는 VM 확장 실행을 포함하여 Azure Virtual Machine 배포 및 관리의 다양한 기능적 측면을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-132">The VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="169a1-133">Azure VM 에이전트는 Azure Marketplace 이미지에 미리 설치되며 지원되는 운영 체제에 수동으로 설치될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-133">The Azure VM agent is preinstalled on Azure Marketplace images and can be installed manually on supported operating systems.</span></span>

<span data-ttu-id="169a1-134">지원되는 운영 체제 및 설치 지침에 대한 자세한 내용은 [Azure Virtual Machines 에이전트](../windows/classic/agents-and-extensions.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="169a1-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](../windows/classic/agents-and-extensions.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="169a1-135">VM 확장 검색</span><span class="sxs-lookup"><span data-stu-id="169a1-135">Discover VM extensions</span></span>

<span data-ttu-id="169a1-136">Azure Virtual Machine와 함께 여러 다양한 VM 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="169a1-137">전체 목록을 보려면 Azure CLI와 함께 다음 명령을 실행하고 해당 예제 위치를 선택한 위치로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-137">To see a complete list, run the following command with the Azure CLI, replacing the example location with the location of your choice.</span></span>

```azurecli
az vm extension image list --location westus -o table
```

## <a name="run-vm-extensions"></a><span data-ttu-id="169a1-138">VM 확장 실행</span><span class="sxs-lookup"><span data-stu-id="169a1-138">Run VM extensions</span></span>

<span data-ttu-id="169a1-139">Azure 가상 컴퓨터 확장은 기존 가상 컴퓨터에서 실행할 수 있습니다. 이러한 기능은 이미 배포한 VM의 구성을 변경하거나 연결을 복구해야 할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-139">Azure virtual machine extensions can be run on existing virtual machines, which are useful when you need to make configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="169a1-140">또한 VM 확장을 Azure Resource Manager 템플릿 배포와 번들로 묶을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-140">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="169a1-141">Resource Manager 템플릿에서 확장을 사용하면 Azure Virtual Machine을 배포하고, 배포 후 개입 없이 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-141">By using extensions with Resource Manager templates, Azure virtual machines can be deployed and configured without post-deployment intervention.</span></span>

<span data-ttu-id="169a1-142">다음 방법을 사용하여 기존 가상 컴퓨터에 대해 확장을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-142">The following methods can be used to run an extension against an existing virtual machine.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="169a1-143">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="169a1-143">Azure CLI</span></span>

<span data-ttu-id="169a1-144">`az vm extension set` 명령을 사용하여 기존 가상 컴퓨터에 대해 Azure Virtual Machine 확장을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-144">Azure virtual machine extensions can be run against an existing virtual machine by using the `az vm extension set` command.</span></span> <span data-ttu-id="169a1-145">이 예제에서는 가상 컴퓨터에 대한 사용자 지정 스크립트 확장을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-145">This example runs the custom script extension against a virtual machine.</span></span>

```azurecli
az vm extension set `
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

<span data-ttu-id="169a1-146">이 스크립트는 다음 텍스트와 유사한 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-146">The script produces output similar to the following text:</span></span>

```azurecli
info:    Executing command vm extension set
+ Looking up the VM "myVM"
+ Installing extension "CustomScript", VM: "mvVM"
info:    vm extension set command OK
```

### <a name="azure-portal"></a><span data-ttu-id="169a1-147">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="169a1-147">Azure portal</span></span>

<span data-ttu-id="169a1-148">Azure Portal을 통해 기존 가상 컴퓨터에 VM 확장을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-148">VM extensions can be applied to an existing virtual machine through the Azure portal.</span></span> <span data-ttu-id="169a1-149">이렇게 하려면 가상 컴퓨터를 선택하고 **확장**을 선택한 후 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-149">To do so, select the virtual machine, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="169a1-150">사용 가능한 확장 목록에서 원하는 확장을 선택하고 마법사의 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-150">Select the extension you want from the list of available extensions and follow the instructions in the wizard.</span></span>

<span data-ttu-id="169a1-151">다음 이미지는 Azure Portal에서 Linux 사용자 지정 스크립트 확장을 설치하는 경우를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-151">The following image shows the installation of the Linux Custom Script extension from the Azure portal.</span></span>

![Install custom script extension](./media/extensions-features/installscriptextensionlinux.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="169a1-153">Azure 리소스 관리자 템플릿</span><span class="sxs-lookup"><span data-stu-id="169a1-153">Azure Resource Manager templates</span></span>

<span data-ttu-id="169a1-154">Azure Resource Manager 템플릿에 VM 확장을 추가하고 템플릿 배포를 통해 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-154">VM extensions can be added to an Azure Resource Manager template and executed with the deployment of the template.</span></span> <span data-ttu-id="169a1-155">템플릿을 사용하여 확장을 배포할 때 완전히 구성된 Azure 배포를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-155">When you deploy an extension with a template, you can create fully configured Azure deployments.</span></span> <span data-ttu-id="169a1-156">예를 들어 다음 JSON은 Resource Manager 템플릿에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-156">For example, the following JSON is taken from a Resource Manager template.</span></span> <span data-ttu-id="169a1-157">이 템플릿은 부하 분산된 가상 컴퓨터 집합 및 Azure SQL Database를 배포한 후 각 VM에 .NET Core 응용 프로그램을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-157">The template deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="169a1-158">VM 확장은 소프트웨어 설치를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-158">The VM extension takes care of the software installation.</span></span>

<span data-ttu-id="169a1-159">자세한 내용은 전체 [Resource Manager 템플릿](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="169a1-159">For more information, see the full [Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

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

<span data-ttu-id="169a1-160">자세한 내용은 [Azure Resource Manager 템플릿 작성](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="169a1-160">For more information, see [Authoring Azure Resource Manager templates](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="169a1-161">VM 확장 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="169a1-161">Secure VM extension data</span></span>

<span data-ttu-id="169a1-162">VM 확장을 실행하는 경우 자격 증명, 저장소 계정 이름 및 저장소 계정 액세스 키와 같은 중요한 정보를 포함해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-162">When you're running a VM extension, it may be necessary to include sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="169a1-163">많은 VM 확장에는 데이터를 암호화하고 대상 가상 컴퓨터 내에서만 해독하는 보호된 구성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-163">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside the target virtual machine.</span></span> <span data-ttu-id="169a1-164">각 확장에는 보호되는 특정 구성 스키마가 있으며 각각은 확장 관련 설명서에 자세히 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-164">Each extension has a specific protected configuration schema, and each is detailed in extension-specific documentation.</span></span>

<span data-ttu-id="169a1-165">다음 예제에서는 Linux용 사용자 지정 스크립트 확장의 인스턴스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-165">The following example shows an instance of the Custom Script extension for Linux.</span></span> <span data-ttu-id="169a1-166">실행할 명령에는 자격 증명 집합이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-166">Notice that the command to execute includes a set of credentials.</span></span> <span data-ttu-id="169a1-167">이 예제에서는 실행할 명령이 암호화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-167">In this example, the command to execute will not be encrypted.</span></span>


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

<span data-ttu-id="169a1-168">**실행할 명령** 속성을 **보호됨** 구성으로 이동하면 실행 문자열이 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-168">Moving the **command to execute** property to the **protected** configuration secures the execution string.</span></span>

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

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="169a1-169">VM 확장 문제 해결</span><span class="sxs-lookup"><span data-stu-id="169a1-169">Troubleshoot VM extensions</span></span>

<span data-ttu-id="169a1-170">각 VM 확장에는 확장 관련 문제 해결 단계가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-170">Each VM extension may have troubleshooting steps specific to the extension.</span></span> <span data-ttu-id="169a1-171">예를 들어 사용자 지정 스크립트 확장을 사용하는 경우 확장이 실행된 가상 컴퓨터에서 로컬로 스크립트 실행 세부 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-171">For example, when you're using the Custom Script extension, script execution details can be found locally on the virtual machine on which the extension was run.</span></span> <span data-ttu-id="169a1-172">확장별 문제 해결 단계는 확장 관련 설명서에 자세히 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-172">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="169a1-173">다음 문제 해결 단계는 모든 가상 컴퓨터 확장에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-173">The following troubleshooting steps apply to all virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="169a1-174">확장 상태 보기</span><span class="sxs-lookup"><span data-stu-id="169a1-174">View extension status</span></span>

<span data-ttu-id="169a1-175">가상 컴퓨터에 대해 가상 컴퓨터 확장을 실행한 후에 다음 Azure CLI 명령을 사용하여 확장 상태를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-175">After a virtual machine extension has been run against a virtual machine, use the following Azure CLI command to return extension status.</span></span> <span data-ttu-id="169a1-176">매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-176">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="169a1-177">출력은 다음 텍스트와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-177">The output looks like the following text:</span></span>

```azurecli
AutoUpgradeMinorVersion    Location    Name          ProvisioningState    Publisher                   ResourceGroup      TypeHandlerVersion  VirtualMachineExtensionType
-------------------------  ----------  ------------  -------------------  --------------------------  ---------------  --------------------  -----------------------------
True                       westus      customScript  Succeeded            Microsoft.Azure.Extensions  exttest                             2  customScript
```

<span data-ttu-id="169a1-178">Azure Portal에서 확장 실행 상태를 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-178">Extension execution status can also be found in the Azure portal.</span></span> <span data-ttu-id="169a1-179">확장의 상태를 확인하려면 가상 컴퓨터를 선택하고 **확장**을 선택한 후 원하는 확장을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-179">To view the status of an extension, select the virtual machine, choose **Extensions**, and select the desired extension.</span></span>

### <a name="rerun-a-vm-extension"></a><span data-ttu-id="169a1-180">VM 확장 다시 실행</span><span class="sxs-lookup"><span data-stu-id="169a1-180">Rerun a VM extension</span></span>

<span data-ttu-id="169a1-181">가상 컴퓨터 확장을 다시 실행해야 하는 경우가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-181">There may be cases in which a virtual machine extension needs to be rerun.</span></span> <span data-ttu-id="169a1-182">확장을 다시 실행하려면 확장을 제거한 다음 원하는 실행 방법으로 확장을 다시 실행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-182">You can rerun an extension by removing it, and then rerunning the extension with an execution method of your choice.</span></span> <span data-ttu-id="169a1-183">확장을 제거하려면 Azure CLI를 사용하여 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-183">To remove an extension, run the following command with the Azure CLI.</span></span> <span data-ttu-id="169a1-184">매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-184">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension delete --name customScript --resource-group myResourceGroup --vm-name myVM
```

<span data-ttu-id="169a1-185">Azure Portal에서 다음 단계에 사용하여 확장을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-185">You can remove an extension by using the following steps in the Azure portal:</span></span>

1. <span data-ttu-id="169a1-186">가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-186">Select a virtual machine.</span></span>
2. <span data-ttu-id="169a1-187">**확장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-187">Choose **Extensions**.</span></span>
3. <span data-ttu-id="169a1-188">원하는 확장을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-188">Select the desired extension.</span></span>
4. <span data-ttu-id="169a1-189">**제거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-189">Choose **Uninstall**.</span></span>

## <a name="common-vm-extension-reference"></a><span data-ttu-id="169a1-190">일반적인 VM 확장 참조</span><span class="sxs-lookup"><span data-stu-id="169a1-190">Common VM extension reference</span></span>
| <span data-ttu-id="169a1-191">확장 이름</span><span class="sxs-lookup"><span data-stu-id="169a1-191">Extension name</span></span> | <span data-ttu-id="169a1-192">설명</span><span class="sxs-lookup"><span data-stu-id="169a1-192">Description</span></span> | <span data-ttu-id="169a1-193">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="169a1-193">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="169a1-194">Linux용 사용자 지정 스크립트 확장</span><span class="sxs-lookup"><span data-stu-id="169a1-194">Custom Script extension for Linux</span></span> |<span data-ttu-id="169a1-195">Azure Virtual Machine에 대해 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="169a1-195">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="169a1-196">Linux용 사용자 지정 스크립트 확장</span><span class="sxs-lookup"><span data-stu-id="169a1-196">Custom Script extension for Linux</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="169a1-197">Docker 확장</span><span class="sxs-lookup"><span data-stu-id="169a1-197">Docker extension</span></span> |<span data-ttu-id="169a1-198">원격 Docker 명령을 지원하기 위해 Docker 데몬을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="169a1-198">Install the Docker daemon to support remote Docker commands.</span></span> |[<span data-ttu-id="169a1-199">Docker VM 확장</span><span class="sxs-lookup"><span data-stu-id="169a1-199">Docker VM extension</span></span>](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="169a1-200">VM 액세스 확장</span><span class="sxs-lookup"><span data-stu-id="169a1-200">VM Access extension</span></span> |<span data-ttu-id="169a1-201">Azure Virtual Machine에 대한 액세스 권한 복구</span><span class="sxs-lookup"><span data-stu-id="169a1-201">Regain access to an Azure virtual machine</span></span> |[<span data-ttu-id="169a1-202">VM 액세스 확장</span><span class="sxs-lookup"><span data-stu-id="169a1-202">VM Access extension</span></span>](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) |
| <span data-ttu-id="169a1-203">Azure 진단 확장</span><span class="sxs-lookup"><span data-stu-id="169a1-203">Azure Diagnostics extension</span></span> |<span data-ttu-id="169a1-204">Azure 진단 관리</span><span class="sxs-lookup"><span data-stu-id="169a1-204">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="169a1-205">Azure 진단 확장</span><span class="sxs-lookup"><span data-stu-id="169a1-205">Azure Diagnostics extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="169a1-206">Azure VM 액세스 확장</span><span class="sxs-lookup"><span data-stu-id="169a1-206">Azure VM Access extension</span></span> |<span data-ttu-id="169a1-207">사용자 및 자격 증명 관리</span><span class="sxs-lookup"><span data-stu-id="169a1-207">Manage users and credentials</span></span> |[<span data-ttu-id="169a1-208">Linux용 VM 액세스 확장</span><span class="sxs-lookup"><span data-stu-id="169a1-208">VM Access extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
