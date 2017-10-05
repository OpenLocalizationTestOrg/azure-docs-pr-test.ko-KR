---
title: "Windows용 OMS Azure Virtual Machine 확장 | Microsoft Docs"
description: "가상 컴퓨터 확장을 사용하여 Windows 가상 컴퓨터에 OMS 에이전트를 배포합니다."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: feae6176-2373-4034-b5d9-a32c6b4e1f10
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: nepeters
ms.openlocfilehash: d933f488fdda0c1d37892be65f2712cf0eb5694e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="oms-virtual-machine-extension-for-windows"></a><span data-ttu-id="76a2a-103">Windows용 OMS 가상 컴퓨터 확장</span><span class="sxs-lookup"><span data-stu-id="76a2a-103">OMS virtual machine extension for Windows</span></span>

<span data-ttu-id="76a2a-104">OMS(Operations Management Suite)는 클라우드와 온-프레미스 자산에서 모니터링, 경고 및 경고 수정 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="76a2a-104">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="76a2a-105">Windows용 OMS 에이전트 가상 컴퓨터 확장은 Microsoft에서 게시 및 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="76a2a-105">The OMS Agent virtual machine extension for Windows is published and supported by Microsoft.</span></span> <span data-ttu-id="76a2a-106">확장 버전은 Azure Virtual Machines에 OMS 에이전트를 설치하고 기존 OMS 작업 영역에 Virtual Machines를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="76a2a-106">The extension installs the OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="76a2a-107">이 문서에서는 지원되는 플랫폼, 구성 및 Windows용 OMS 가상 컴퓨터 확장에 대한 배포 옵션을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="76a2a-107">This document details the supported platforms, configurations, and deployment options for the OMS virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76a2a-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="76a2a-108">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="76a2a-109">운영 체제</span><span class="sxs-lookup"><span data-stu-id="76a2a-109">Operating system</span></span>
<span data-ttu-id="76a2a-110">Windows용 OMS 에이전트 확장은 Windows Server 2008 R2, 2012, 2012 R2 및 2016 릴리스에 대해 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76a2a-110">The OMS Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="76a2a-111">인터넷 연결</span><span class="sxs-lookup"><span data-stu-id="76a2a-111">Internet connectivity</span></span>
<span data-ttu-id="76a2a-112">Windows용 OMS 에이전트 확장은 대상 가상 컴퓨터가 인터넷에 연결되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a2a-112">The OMS Agent extension for Windows requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="76a2a-113">확장 스키마</span><span class="sxs-lookup"><span data-stu-id="76a2a-113">Extension schema</span></span>

<span data-ttu-id="76a2a-114">다음 JSON은 OMS 에이전트 확장에 대한 스키마를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="76a2a-114">The following JSON shows the schema for the OMS Agent extension.</span></span> <span data-ttu-id="76a2a-115">이 확장은 대상 OMS 작업 영역에서 작업 영역 ID와 작업 영역 키가 필요하며, OMS 포털에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76a2a-115">The extension requires the workspace Id and workspace key from the target OMS workspace, these can be found in the OMS portal.</span></span> <span data-ttu-id="76a2a-116">작업 영역 키는 중요한 데이터로 처리되므로 보호되는 설정에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a2a-116">Because the workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="76a2a-117">Azure VM 확장으로 보호되는 설정 데이터는 암호화되어 대상 가상 컴퓨터에서만 해독됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a2a-117">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span> <span data-ttu-id="76a2a-118">**workspaceId** 및 **workspaceKey**는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="76a2a-118">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```
### <a name="property-values"></a><span data-ttu-id="76a2a-119">속성 값</span><span class="sxs-lookup"><span data-stu-id="76a2a-119">Property values</span></span>

| <span data-ttu-id="76a2a-120">이름</span><span class="sxs-lookup"><span data-stu-id="76a2a-120">Name</span></span> | <span data-ttu-id="76a2a-121">값/예제</span><span class="sxs-lookup"><span data-stu-id="76a2a-121">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="76a2a-122">apiVersion</span><span class="sxs-lookup"><span data-stu-id="76a2a-122">apiVersion</span></span> | <span data-ttu-id="76a2a-123">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="76a2a-123">2015-06-15</span></span> |
| <span data-ttu-id="76a2a-124">publisher</span><span class="sxs-lookup"><span data-stu-id="76a2a-124">publisher</span></span> | <span data-ttu-id="76a2a-125">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="76a2a-125">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="76a2a-126">type</span><span class="sxs-lookup"><span data-stu-id="76a2a-126">type</span></span> | <span data-ttu-id="76a2a-127">MicrosoftMonitoringAgent</span><span class="sxs-lookup"><span data-stu-id="76a2a-127">MicrosoftMonitoringAgent</span></span> |
| <span data-ttu-id="76a2a-128">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="76a2a-128">typeHandlerVersion</span></span> | <span data-ttu-id="76a2a-129">1.0</span><span class="sxs-lookup"><span data-stu-id="76a2a-129">1.0</span></span> |
| <span data-ttu-id="76a2a-130">workspaceId(예)</span><span class="sxs-lookup"><span data-stu-id="76a2a-130">workspaceId (e.g)</span></span> | <span data-ttu-id="76a2a-131">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="76a2a-131">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="76a2a-132">workspaceKey(예)</span><span class="sxs-lookup"><span data-stu-id="76a2a-132">workspaceKey (e.g)</span></span> | <span data-ttu-id="76a2a-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span><span class="sxs-lookup"><span data-stu-id="76a2a-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="76a2a-134">템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="76a2a-134">Template deployment</span></span>

<span data-ttu-id="76a2a-135">Azure Resource Manager 템플릿을 사용하여 Azure VM 확장을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76a2a-135">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="76a2a-136">이전 섹션에서 자세히 설명되어 있는 JSON 스키마는 Azure Resource Manager 템플릿에서 사용하여 Azure Resource Manager 템플릿 배포 중 OMS 에이전트 확장을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76a2a-136">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the OMS Agent extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="76a2a-137">OMS 에이전트 VM 확장을 포함하는 샘플 템플릿은 [Azure 빠른 시작 갤러리](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76a2a-137">A sample template that includes the OMS Agent VM extension can be found on the [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span></span> 

<span data-ttu-id="76a2a-138">가상 컴퓨터 확장에 대한 JSON은 가상 컴퓨터 리소스 내에 중첩되거나 루트 또는 최상위 수준의 Resource Manager JSON 템플릿에 배치될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76a2a-138">The JSON for a virtual machine extension can be nested inside the virtual machine resource, or placed at the root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="76a2a-139">JSON의 배치는 리소스 이름 및 형식 값에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="76a2a-139">The placement of the JSON affects the value of the resource name and type.</span></span> <span data-ttu-id="76a2a-140">자세한 내용은 [자식 리소스의 이름 및 형식 설정](../../azure-resource-manager/resource-manager-template-child-resource.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="76a2a-140">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="76a2a-141">다음 예제에서는 OMS 확장이 가상 컴퓨터 리소스 내에 중첩되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="76a2a-141">The following example assumes the OMS extension is nested inside the virtual machine resource.</span></span> <span data-ttu-id="76a2a-142">확장 리소스를 중첩하는 경우 JSON은 가상 컴퓨터의 `"resources": []` 개체에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a2a-142">When nesting the extension resource, the JSON is placed in the `"resources": []` object of the virtual machine.</span></span>


```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

<span data-ttu-id="76a2a-143">템플릿의 루트에 JSON 확장을 배치하면 리소스 이름에 부모 가상 컴퓨터에 대한 참조가 포함되며 형식은 중첩된 구성을 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="76a2a-143">When placing the extension JSON at the root of the template, the resource name includes a reference to the parent virtual machine, and the type reflects the nested configuration.</span></span> 

```json
{
    "type": "Microsoft.Compute/virtualMachines/extensions",
    "name": "<parentVmResource>/OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

## <a name="powershell-deployment"></a><span data-ttu-id="76a2a-144">PowerShell 배포</span><span class="sxs-lookup"><span data-stu-id="76a2a-144">PowerShell deployment</span></span>

<span data-ttu-id="76a2a-145">`Set-AzureRmVMExtension` 명령을 사용하여 OMS 에이전트 가상 컴퓨터 확장을 기존 가상 컴퓨터에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76a2a-145">The `Set-AzureRmVMExtension` command can be used to deploy the OMS Agent virtual machine extension to an existing virtual machine.</span></span> <span data-ttu-id="76a2a-146">명령을 실행하기 전에 공용 및 개인 구성을 PowerShell 해시 테이블에 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a2a-146">Before running the command, the public and private configurations need to be stored in a PowerShell hash table.</span></span> 

```powershell
$PublicSettings = @{"workspaceId" = "myWorkspaceId"}
$ProtectedSettings = @{"workspaceKey" = "myWorkspaceKey"}

Set-AzureRmVMExtension -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
    -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" `
    -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
    -ExtensionType "MicrosoftMonitoringAgent" `
    -TypeHandlerVersion 1.0 `
    -Settings $PublicSettings `
    -ProtectedSettings $ProtectedSettings `
    -Location WestUS ` 
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="76a2a-147">문제 해결 및 지원</span><span class="sxs-lookup"><span data-stu-id="76a2a-147">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="76a2a-148">문제 해결</span><span class="sxs-lookup"><span data-stu-id="76a2a-148">Troubleshoot</span></span>

<span data-ttu-id="76a2a-149">확장 배포 상태에 대한 데이터는 Azure PowerShell 모듈을 사용하여 Azure Portal에서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76a2a-149">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="76a2a-150">지정된 VM에 대한 확장의 배포 상태를 보려면 Azure PowerShell 모듈을 사용하여 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="76a2a-150">To see the deployment state of extensions for a given VM, run the following command using the Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="76a2a-151">확장 실행 출력은 다음 디렉터리에 있는 파일에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a2a-151">Extension execution output is logged to files found in the following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\
```

### <a name="support"></a><span data-ttu-id="76a2a-152">지원</span><span class="sxs-lookup"><span data-stu-id="76a2a-152">Support</span></span>

<span data-ttu-id="76a2a-153">이 문서의 어디에서든 도움이 필요한 경우 [MSDN Azure 및 Stack Overflow 포럼](https://azure.microsoft.com/en-us/support/forums/)에서 Azure 전문가에게 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76a2a-153">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="76a2a-154">또는 Azure 기술 지원 인시던트를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76a2a-154">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="76a2a-155">[Azure 지원 사이트](https://azure.microsoft.com/en-us/support/options/)로 가서 지원 받기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76a2a-155">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="76a2a-156">Azure 지원을 사용하는 방법에 대한 자세한 내용은 [Microsoft Azure 지원 FAQ](https://azure.microsoft.com/en-us/support/faq/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="76a2a-156">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
