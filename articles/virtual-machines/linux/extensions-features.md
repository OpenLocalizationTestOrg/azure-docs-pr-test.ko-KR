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
# <a name="virtual-machine-extensions-and-features-for-linux"></a><span data-ttu-id="7f1c6-103">Linux용 가상 컴퓨터 확장 및 기능</span><span class="sxs-lookup"><span data-stu-id="7f1c6-103">Virtual machine extensions and features for Linux</span></span>

<span data-ttu-id="7f1c6-104">Azure Virtual Machines 확장은 Azure Virtual Machines에서 배포 후 구성 및 Automation 작업을 제공하는 작은 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="7f1c6-105">예를 들어 가상 컴퓨터는 소프트웨어 설치, 바이러스 방지 또는 Docker 구성에 필요한 경우 VM 확장 수 toocomplete 사용 되는 이러한 작업을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used toocomplete these tasks.</span></span> <span data-ttu-id="7f1c6-106">Azure VM 확장 hello Azure CLI, PowerShell, Azure 리소스 관리자 템플릿 사용 하 여 실행할 수 있으며 Azure 포털 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-106">Azure VM extensions can be run using hello Azure CLI, PowerShell, Azure Resource Manager templates, and hello Azure portal.</span></span> <span data-ttu-id="7f1c6-107">확장을 새 가상 컴퓨터 배포와 번들로 제공하거나 기존 시스템에 대해 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-107">Extensions can be bundled with a new virtual machine deployment, or run against any existing system.</span></span>

<span data-ttu-id="7f1c6-108">이 문서에서는 VM 확장을 Azure VM 확장 및 지침을 사용 하 여 toodetect를 관리 하 고 VM 확장을 제거 하는 방법에 대 한 필수 구성 요소에 대 한 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-108">This document provides an overview of VM extensions, prerequisites for using Azure VM extensions, and guidance on how toodetect, manage, and remove VM extensions.</span></span> <span data-ttu-id="7f1c6-109">많은 VM 확장 각각을 고유한 구성으로 사용할 수 있으므로 여기서는 일반적인 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="7f1c6-110">각 문서 특정 toohello 개별 확장에서 확장 관련 세부 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-110">Extension-specific details can be found in each document specific toohello individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="7f1c6-111">사용 사례 및 샘플</span><span class="sxs-lookup"><span data-stu-id="7f1c6-111">Use cases and samples</span></span>

<span data-ttu-id="7f1c6-112">각각 특정 사용 사례가 있는 몇 가지 다른 Azure VM 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-112">Several different Azure VM extensions are available, each with a specific use case.</span></span> <span data-ttu-id="7f1c6-113">일부 사례:</span><span class="sxs-lookup"><span data-stu-id="7f1c6-113">Some examples are:</span></span>

- <span data-ttu-id="7f1c6-114">Linux 용 DSC 확장 hello를 사용 하는 PowerShell 원하는 상태 구성 tooa 가상 컴퓨터를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-114">Apply PowerShell Desired State configurations tooa virtual machine using hello DSC extension for Linux.</span></span> <span data-ttu-id="7f1c6-115">자세한 내용은 [Azure 필요한 상태 구성 확장](https://github.com/Azure/azure-linux-extensions/tree/master/DSC)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-115">For more information, see [Azure Desired State configuration extension](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).</span></span>
- <span data-ttu-id="7f1c6-116">Microsoft 모니터링 에이전트 VM 확장 hello로 가상 컴퓨터의 모니터링을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-116">Configure monitoring of a virtual machine with hello Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="7f1c6-117">자세한 내용은 참조 [어떻게 toomonitor Linux VM](tutorial-monitoring.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-117">For more information, see [How toomonitor a Linux VM](tutorial-monitoring.md).</span></span>
- <span data-ttu-id="7f1c6-118">Hello Datadog 확장으로 Azure 인프라의 모니터링을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-118">Configure monitoring of your Azure infrastructure with hello Datadog extension.</span></span> <span data-ttu-id="7f1c6-119">자세한 내용은 참조 hello [Datadog 블로그](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-119">For more information, see hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="7f1c6-120">Hello Docker VM 확장을 사용 하 여 Azure 가상 컴퓨터에 Docker 호스트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-120">Configure a Docker host on an Azure virtual machine using hello Docker VM extension.</span></span> <span data-ttu-id="7f1c6-121">자세한 내용은 [Docker VM 확장](dockerextension.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-121">For more information, see [Docker VM extension](dockerextension.md).</span></span>

<span data-ttu-id="7f1c6-122">또한 tooprocess 전용 확장 사용자 지정 스크립트 확장은 Windows와 Linux 가상 컴퓨터에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-122">In addition tooprocess-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="7f1c6-123">Linux 용 사용자 지정 스크립트 확장 hello 모든 Bash 스크립트 toobe를 가상 컴퓨터에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-123">hello Custom Script extension for Linux allows any Bash script toobe run on a virtual machine.</span></span> <span data-ttu-id="7f1c6-124">사용자 지정 스크립트는 네이티브 Azure 도구로 제공할 수 있는 것 이상의 구성이 필요한 Azure 배포를 디자인할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-124">Custom scripts are useful for designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="7f1c6-125">자세한 내용은 [Linux VM 사용자 지정 스크립트 확장](extensions-customscript.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-125">For more information, see [Linux VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="7f1c6-126">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7f1c6-126">Prerequisites</span></span>

<span data-ttu-id="7f1c6-127">각 가상 컴퓨터 확장에는 고유한 필수 구성 요소 집합이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-127">Each virtual machine extension might have its own set of prerequisites.</span></span> <span data-ttu-id="7f1c6-128">예를 들어 hello Docker VM 확장에 지원 되는 Linux 배포판의 필수 구성 요소를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-128">For instance, hello Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="7f1c6-129">개별 확장의 요구 사항은 hello 확장 프로그램별 설명서에 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-129">Requirements of individual extensions are detailed in hello extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="7f1c6-130">Azure VM 에이전트</span><span class="sxs-lookup"><span data-stu-id="7f1c6-130">Azure VM agent</span></span>

<span data-ttu-id="7f1c6-131">hello Azure VM 에이전트는 Azure 가상 컴퓨터와 hello Azure 패브릭 컨트롤러 간의 상호 작용을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-131">hello Azure VM agent manages interactions between an Azure virtual machine and hello Azure fabric controller.</span></span> <span data-ttu-id="7f1c6-132">hello VM 에이전트는 업무의 다양 한 VM 확장을 실행 하는 포함 하 여 Azure 가상 컴퓨터 배포 및 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-132">hello VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="7f1c6-133">hello Azure VM 에이전트는 Azure 마켓플레이스 이미지에 사전 설치 하 고 지원 되는 운영 체제에 수동으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-133">hello Azure VM agent is preinstalled on Azure Marketplace images and can be installed manually on supported operating systems.</span></span>

<span data-ttu-id="7f1c6-134">지원되는 운영 체제 및 설치 지침에 대한 자세한 내용은 [Azure Virtual Machines 에이전트](../windows/classic/agents-and-extensions.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](../windows/classic/agents-and-extensions.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="7f1c6-135">VM 확장 검색</span><span class="sxs-lookup"><span data-stu-id="7f1c6-135">Discover VM extensions</span></span>

<span data-ttu-id="7f1c6-136">Azure Virtual Machine와 함께 여러 다양한 VM 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="7f1c6-137">toosee 전체 목록 보려면 다음 명령을 hello Azure CLI로, 사용자가 선택한 hello 위치와 hello 예제 위치 대체 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-137">toosee a complete list, run hello following command with hello Azure CLI, replacing hello example location with hello location of your choice.</span></span>

```azurecli
az vm extension image list --location westus -o table
```

## <a name="run-vm-extensions"></a><span data-ttu-id="7f1c6-138">VM 확장 실행</span><span class="sxs-lookup"><span data-stu-id="7f1c6-138">Run VM extensions</span></span>

<span data-ttu-id="7f1c6-139">toomake 구성 변경 내용이 필요 하거나 이미 배포 된 VM에서 연결을 복구 하는 경우에 유용 하는 기존 가상 컴퓨터에 azure 가상 컴퓨터 확장을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-139">Azure virtual machine extensions can be run on existing virtual machines, which are useful when you need toomake configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="7f1c6-140">또한 VM 확장을 Azure Resource Manager 템플릿 배포와 번들로 묶을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-140">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="7f1c6-141">Resource Manager 템플릿에서 확장을 사용하면 Azure Virtual Machine을 배포하고, 배포 후 개입 없이 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-141">By using extensions with Resource Manager templates, Azure virtual machines can be deployed and configured without post-deployment intervention.</span></span>

<span data-ttu-id="7f1c6-142">메서드를 다음 hello 사용된 toorun 기존 가상 컴퓨터에 대해 확장 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-142">hello following methods can be used toorun an extension against an existing virtual machine.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="7f1c6-143">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7f1c6-143">Azure CLI</span></span>

<span data-ttu-id="7f1c6-144">Azure 가상 컴퓨터 확장 hello를 사용 하 여 기존 가상 컴퓨터에 대해 실행할 수 `az vm extension set` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-144">Azure virtual machine extensions can be run against an existing virtual machine by using hello `az vm extension set` command.</span></span> <span data-ttu-id="7f1c6-145">이 예제에서는 가상 컴퓨터에 대 한 hello 사용자 지정 스크립트 확장을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-145">This example runs hello custom script extension against a virtual machine.</span></span>

```azurecli
az vm extension set `
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

<span data-ttu-id="7f1c6-146">스크립트 생성 출력 유사한 toohello 텍스트 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="7f1c6-146">hello script produces output similar toohello following text:</span></span>

```azurecli
info:    Executing command vm extension set
+ Looking up hello VM "myVM"
+ Installing extension "CustomScript", VM: "mvVM"
info:    vm extension set command OK
```

### <a name="azure-portal"></a><span data-ttu-id="7f1c6-147">Azure portal</span><span class="sxs-lookup"><span data-stu-id="7f1c6-147">Azure portal</span></span>

<span data-ttu-id="7f1c6-148">VM 확장 hello Azure 포털을 통해 적용 된 tooan 기존 가상 컴퓨터를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-148">VM extensions can be applied tooan existing virtual machine through hello Azure portal.</span></span> <span data-ttu-id="7f1c6-149">toodo hello 가상 컴퓨터를를 따라서 선택 선택 **확장**를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-149">toodo so, select hello virtual machine, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="7f1c6-150">Hello 사용 가능한 확장 목록에서 원하는 및 hello 마법사 지시에에서 따라 hello hello 확장을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-150">Select hello extension you want from hello list of available extensions and follow hello instructions in hello wizard.</span></span>

<span data-ttu-id="7f1c6-151">hello 다음 이미지에서는 hello 설치 hello hello Azure 포털에서에서 Linux 사용자 지정 스크립트 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-151">hello following image shows hello installation of hello Linux Custom Script extension from hello Azure portal.</span></span>

![Install custom script extension](./media/extensions-features/installscriptextensionlinux.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="7f1c6-153">Azure 리소스 관리자 템플릿</span><span class="sxs-lookup"><span data-stu-id="7f1c6-153">Azure Resource Manager templates</span></span>

<span data-ttu-id="7f1c6-154">VM 확장 추가 tooan Azure 리소스 관리자 템플릿 수 및 hello 템플릿의 hello 배포를 사용 하 여 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-154">VM extensions can be added tooan Azure Resource Manager template and executed with hello deployment of hello template.</span></span> <span data-ttu-id="7f1c6-155">템플릿을 사용하여 확장을 배포할 때 완전히 구성된 Azure 배포를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-155">When you deploy an extension with a template, you can create fully configured Azure deployments.</span></span> <span data-ttu-id="7f1c6-156">예를 들어 다음 JSON hello은 리소스 관리자 템플릿을에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-156">For example, hello following JSON is taken from a Resource Manager template.</span></span> <span data-ttu-id="7f1c6-157">hello 템플릿 집합을 부하 분산 된 가상 컴퓨터와 Azure SQL 데이터베이스를 배포 하 고 각 VM에서.NET Core 응용 프로그램을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-157">hello template deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="7f1c6-158">VM 확장 hello hello 소프트웨어 설치 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-158">hello VM extension takes care of hello software installation.</span></span>

<span data-ttu-id="7f1c6-159">자세한 내용은 참조 hello 전체 [리소스 관리자 템플릿](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-159">For more information, see hello full [Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

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

<span data-ttu-id="7f1c6-160">자세한 내용은 [Azure Resource Manager 템플릿 작성](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-160">For more information, see [Authoring Azure Resource Manager templates](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="7f1c6-161">VM 확장 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="7f1c6-161">Secure VM extension data</span></span>

<span data-ttu-id="7f1c6-162">VM 확장을 실행 하는 경우 자격 증명, 저장소 계정 이름과 저장소 계정 액세스 키와 같은 중요 한 정보가 필요한 tooinclude 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-162">When you're running a VM extension, it may be necessary tooinclude sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="7f1c6-163">많은 VM 확장 데이터를 암호화 하 고만 hello 대상 가상 컴퓨터 내 해독 하는 보호 된 구성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-163">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside hello target virtual machine.</span></span> <span data-ttu-id="7f1c6-164">각 확장에는 보호되는 특정 구성 스키마가 있으며 각각은 확장 관련 설명서에 자세히 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-164">Each extension has a specific protected configuration schema, and each is detailed in extension-specific documentation.</span></span>

<span data-ttu-id="7f1c6-165">다음 예제는 hello Linux에 대 한 사용자 지정 스크립트 확장 hello의 인스턴스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-165">hello following example shows an instance of hello Custom Script extension for Linux.</span></span> <span data-ttu-id="7f1c6-166">Hello 명령 tooexecute 해당 자격 증명 집합이 포함 되어 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-166">Notice that hello command tooexecute includes a set of credentials.</span></span> <span data-ttu-id="7f1c6-167">이 예제에서는 hello 명령 tooexecute 암호화 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-167">In this example, hello command tooexecute will not be encrypted.</span></span>


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

<span data-ttu-id="7f1c6-168">이동 hello **명령 tooexecute** 속성 toohello **보호** 구성 hello 실행 문자열을 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-168">Moving hello **command tooexecute** property toohello **protected** configuration secures hello execution string.</span></span>

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

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="7f1c6-169">VM 확장 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7f1c6-169">Troubleshoot VM extensions</span></span>

<span data-ttu-id="7f1c6-170">각 VM 확장 단계 특정 toohello 확장 문제 해결 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-170">Each VM extension may have troubleshooting steps specific toohello extension.</span></span> <span data-ttu-id="7f1c6-171">예를 들어 hello 사용자 지정 스크립트 확장을 사용 하는 경우 스크립트 실행 세부 사항은 있습니다 로컬로 hello 확장 실행 된 hello 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-171">For example, when you're using hello Custom Script extension, script execution details can be found locally on hello virtual machine on which hello extension was run.</span></span> <span data-ttu-id="7f1c6-172">확장별 문제 해결 단계는 확장 관련 설명서에 자세히 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-172">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="7f1c6-173">문제 해결 단계를 수행 하는 hello tooall 가상 컴퓨터 확장을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-173">hello following troubleshooting steps apply tooall virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="7f1c6-174">확장 상태 보기</span><span class="sxs-lookup"><span data-stu-id="7f1c6-174">View extension status</span></span>

<span data-ttu-id="7f1c6-175">가상 컴퓨터 확장을 가상 컴퓨터에 대해 실행 한 후 다음 Azure CLI 명령을 tooreturn 확장 상태 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-175">After a virtual machine extension has been run against a virtual machine, use hello following Azure CLI command tooreturn extension status.</span></span> <span data-ttu-id="7f1c6-176">매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-176">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="7f1c6-177">hello 출력 텍스트 다음 hello와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-177">hello output looks like hello following text:</span></span>

```azurecli
AutoUpgradeMinorVersion    Location    Name          ProvisioningState    Publisher                   ResourceGroup      TypeHandlerVersion  VirtualMachineExtensionType
-------------------------  ----------  ------------  -------------------  --------------------------  ---------------  --------------------  -----------------------------
True                       westus      customScript  Succeeded            Microsoft.Azure.Extensions  exttest                             2  customScript
```

<span data-ttu-id="7f1c6-178">Hello Azure 포털에서에서 확장 실행 상태를 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-178">Extension execution status can also be found in hello Azure portal.</span></span> <span data-ttu-id="7f1c6-179">확장을 선택 하는 hello 가상 컴퓨터의 tooview hello 상태 선택 **확장**, 선택 hello 원하는 확장 프로그램 및입니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-179">tooview hello status of an extension, select hello virtual machine, choose **Extensions**, and select hello desired extension.</span></span>

### <a name="rerun-a-vm-extension"></a><span data-ttu-id="7f1c6-180">VM 확장 다시 실행</span><span class="sxs-lookup"><span data-stu-id="7f1c6-180">Rerun a VM extension</span></span>

<span data-ttu-id="7f1c6-181">가상 컴퓨터 확장 toobe 해야 하는 경우 있을 수 있습니다를 다시 실행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-181">There may be cases in which a virtual machine extension needs toobe rerun.</span></span> <span data-ttu-id="7f1c6-182">제거한 다음 원하는 실행 메서드에 hello 확장을 다시 실행 하 여 확장을 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-182">You can rerun an extension by removing it, and then rerunning hello extension with an execution method of your choice.</span></span> <span data-ttu-id="7f1c6-183">tooremove 확장을 hello 다음 Azure CLI hello로 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-183">tooremove an extension, run hello following command with hello Azure CLI.</span></span> <span data-ttu-id="7f1c6-184">매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-184">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension delete --name customScript --resource-group myResourceGroup --vm-name myVM
```

<span data-ttu-id="7f1c6-185">Hello Azure 포털의에서 단계를 실행 하는 hello를 사용 하 여 확장을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-185">You can remove an extension by using hello following steps in hello Azure portal:</span></span>

1. <span data-ttu-id="7f1c6-186">가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-186">Select a virtual machine.</span></span>
2. <span data-ttu-id="7f1c6-187">**확장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-187">Choose **Extensions**.</span></span>
3. <span data-ttu-id="7f1c6-188">Hello 필요한 확장을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-188">Select hello desired extension.</span></span>
4. <span data-ttu-id="7f1c6-189">**제거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-189">Choose **Uninstall**.</span></span>

## <a name="common-vm-extension-reference"></a><span data-ttu-id="7f1c6-190">일반적인 VM 확장 참조</span><span class="sxs-lookup"><span data-stu-id="7f1c6-190">Common VM extension reference</span></span>
| <span data-ttu-id="7f1c6-191">확장 이름</span><span class="sxs-lookup"><span data-stu-id="7f1c6-191">Extension name</span></span> | <span data-ttu-id="7f1c6-192">설명</span><span class="sxs-lookup"><span data-stu-id="7f1c6-192">Description</span></span> | <span data-ttu-id="7f1c6-193">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="7f1c6-193">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7f1c6-194">Linux용 사용자 지정 스크립트 확장</span><span class="sxs-lookup"><span data-stu-id="7f1c6-194">Custom Script extension for Linux</span></span> |<span data-ttu-id="7f1c6-195">Azure Virtual Machine에 대해 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="7f1c6-195">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="7f1c6-196">Linux용 사용자 지정 스크립트 확장</span><span class="sxs-lookup"><span data-stu-id="7f1c6-196">Custom Script extension for Linux</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="7f1c6-197">Docker 확장</span><span class="sxs-lookup"><span data-stu-id="7f1c6-197">Docker extension</span></span> |<span data-ttu-id="7f1c6-198">Hello Docker 디먼 toosupport 원격 Docker 명령을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1c6-198">Install hello Docker daemon toosupport remote Docker commands.</span></span> |[<span data-ttu-id="7f1c6-199">Docker VM 확장</span><span class="sxs-lookup"><span data-stu-id="7f1c6-199">Docker VM extension</span></span>](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="7f1c6-200">VM 액세스 확장</span><span class="sxs-lookup"><span data-stu-id="7f1c6-200">VM Access extension</span></span> |<span data-ttu-id="7f1c6-201">액세스 tooan Azure 가상 컴퓨터를 다시 가져오기</span><span class="sxs-lookup"><span data-stu-id="7f1c6-201">Regain access tooan Azure virtual machine</span></span> |[<span data-ttu-id="7f1c6-202">VM 액세스 확장</span><span class="sxs-lookup"><span data-stu-id="7f1c6-202">VM Access extension</span></span>](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) |
| <span data-ttu-id="7f1c6-203">Azure 진단 확장</span><span class="sxs-lookup"><span data-stu-id="7f1c6-203">Azure Diagnostics extension</span></span> |<span data-ttu-id="7f1c6-204">Azure 진단 관리</span><span class="sxs-lookup"><span data-stu-id="7f1c6-204">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="7f1c6-205">Azure 진단 확장</span><span class="sxs-lookup"><span data-stu-id="7f1c6-205">Azure Diagnostics extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="7f1c6-206">Azure VM 액세스 확장</span><span class="sxs-lookup"><span data-stu-id="7f1c6-206">Azure VM Access extension</span></span> |<span data-ttu-id="7f1c6-207">사용자 및 자격 증명 관리</span><span class="sxs-lookup"><span data-stu-id="7f1c6-207">Manage users and credentials</span></span> |[<span data-ttu-id="7f1c6-208">Linux용 VM 액세스 확장</span><span class="sxs-lookup"><span data-stu-id="7f1c6-208">VM Access extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
