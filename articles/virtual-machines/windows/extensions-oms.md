---
title: "windows Azure 가상 컴퓨터 확장 aaaOMS | Microsoft Docs"
description: "가상 컴퓨터 확장을 사용 하 여 Windows 가상 컴퓨터에 hello OMS 에이전트를 배포 합니다."
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
ms.openlocfilehash: 3000f66c0acdec1d1fad2125b8c6b72a92b1ec92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-windows"></a><span data-ttu-id="30cdb-103">Windows용 OMS 가상 컴퓨터 확장</span><span class="sxs-lookup"><span data-stu-id="30cdb-103">OMS virtual machine extension for Windows</span></span>

<span data-ttu-id="30cdb-104">OMS(Operations Management Suite)는 클라우드와 온-프레미스 자산에서 모니터링, 경고 및 경고 수정 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-104">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="30cdb-105">Windows 용 OMS 에이전트 가상 컴퓨터 확장 hello 게시 되 고 Microsoft에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-105">hello OMS Agent virtual machine extension for Windows is published and supported by Microsoft.</span></span> <span data-ttu-id="30cdb-106">Azure 가상 컴퓨터에 hello OMS 에이전트를 설치 하 고 기존 OMS 작업 영역에 가상 컴퓨터를 등록 하는 hello 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-106">hello extension installs hello OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="30cdb-107">이 문서 정보 hello windows hello OMS 가상 컴퓨터 확장에 대 한 플랫폼, 구성 및 배포 옵션을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-107">This document details hello supported platforms, configurations, and deployment options for hello OMS virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30cdb-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="30cdb-108">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="30cdb-109">운영 체제</span><span class="sxs-lookup"><span data-stu-id="30cdb-109">Operating system</span></span>
<span data-ttu-id="30cdb-110">OMS 에이전트 확장 hello Windows Server 2008 r 2에 대해 Windows를 실행할 수에 대 한 2016, R2, 2012 및 2012를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-110">hello OMS Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="30cdb-111">인터넷 연결</span><span class="sxs-lookup"><span data-stu-id="30cdb-111">Internet connectivity</span></span>
<span data-ttu-id="30cdb-112">Windows 용 OMS 에이전트 확장 hello hello 대상 가상 컴퓨터는 연결 된 toohello 필요 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-112">hello OMS Agent extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="30cdb-113">확장 스키마</span><span class="sxs-lookup"><span data-stu-id="30cdb-113">Extension schema</span></span>

<span data-ttu-id="30cdb-114">hello 다음 JSON 스키마를 보여 줍니다 hello hello OMS 에이전트 확장에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-114">hello following JSON shows hello schema for hello OMS Agent extension.</span></span> <span data-ttu-id="30cdb-115">hello 확장 해야 hello 대상 OMS 작업 영역에서 hello 작업 영역 Id와 작업 영역 키를 찾을 수 있습니다 hello OMS 포털에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-115">hello extension requires hello workspace Id and workspace key from hello target OMS workspace, these can be found in hello OMS portal.</span></span> <span data-ttu-id="30cdb-116">중요 한 데이터로 처리 되어야 hello 작업 영역 키를 보호 설정 구성에 저장 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-116">Because hello workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="30cdb-117">Azure VM 확장으로 보호 된 데이터를 설정 하는 암호화 되 고 hello 대상 가상 컴퓨터에 암호를 해독할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-117">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span> <span data-ttu-id="30cdb-118">**workspaceId** 및 **workspaceKey**는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-118">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

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
### <a name="property-values"></a><span data-ttu-id="30cdb-119">속성 값</span><span class="sxs-lookup"><span data-stu-id="30cdb-119">Property values</span></span>

| <span data-ttu-id="30cdb-120">이름</span><span class="sxs-lookup"><span data-stu-id="30cdb-120">Name</span></span> | <span data-ttu-id="30cdb-121">값/예제</span><span class="sxs-lookup"><span data-stu-id="30cdb-121">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="30cdb-122">apiVersion</span><span class="sxs-lookup"><span data-stu-id="30cdb-122">apiVersion</span></span> | <span data-ttu-id="30cdb-123">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="30cdb-123">2015-06-15</span></span> |
| <span data-ttu-id="30cdb-124">publisher</span><span class="sxs-lookup"><span data-stu-id="30cdb-124">publisher</span></span> | <span data-ttu-id="30cdb-125">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="30cdb-125">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="30cdb-126">type</span><span class="sxs-lookup"><span data-stu-id="30cdb-126">type</span></span> | <span data-ttu-id="30cdb-127">MicrosoftMonitoringAgent</span><span class="sxs-lookup"><span data-stu-id="30cdb-127">MicrosoftMonitoringAgent</span></span> |
| <span data-ttu-id="30cdb-128">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="30cdb-128">typeHandlerVersion</span></span> | <span data-ttu-id="30cdb-129">1.0</span><span class="sxs-lookup"><span data-stu-id="30cdb-129">1.0</span></span> |
| <span data-ttu-id="30cdb-130">workspaceId(예)</span><span class="sxs-lookup"><span data-stu-id="30cdb-130">workspaceId (e.g)</span></span> | <span data-ttu-id="30cdb-131">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="30cdb-131">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="30cdb-132">workspaceKey(예)</span><span class="sxs-lookup"><span data-stu-id="30cdb-132">workspaceKey (e.g)</span></span> | <span data-ttu-id="30cdb-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span><span class="sxs-lookup"><span data-stu-id="30cdb-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="30cdb-134">템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="30cdb-134">Template deployment</span></span>

<span data-ttu-id="30cdb-135">Azure Resource Manager 템플릿을 사용하여 Azure VM 확장을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-135">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="30cdb-136">Azure 리소스 관리자 템플릿 배포 중에 Azure 리소스 관리자 템플릿 toorun hello OMS 에이전트 확장 hello 이전 섹션에서 자세히 설명 하는 hello JSON 스키마를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-136">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello OMS Agent extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="30cdb-137">Hello에 hello OMS 에이전트 VM 확장을 포함 하는 샘플 템플릿이 있습니다 [Azure 빠른 시작 갤러리](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm)합니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-137">A sample template that includes hello OMS Agent VM extension can be found on hello [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span></span> 

<span data-ttu-id="30cdb-138">가상 컴퓨터 확장에 대 한 JSON hello hello 가상 컴퓨터 리소스 내에 중첩 된 또는 hello 루트 또는 리소스 관리자 JSON 서식 파일의 최상위 수준에 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-138">hello JSON for a virtual machine extension can be nested inside hello virtual machine resource, or placed at hello root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="30cdb-139">hello JSON의 hello 배치 hello hello 리소스 이름 및 형식의 값을 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-139">hello placement of hello JSON affects hello value of hello resource name and type.</span></span> <span data-ttu-id="30cdb-140">자세한 내용은 [자식 리소스의 이름 및 형식 설정](../../azure-resource-manager/resource-manager-template-child-resource.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30cdb-140">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="30cdb-141">hello 다음 예에서는 가정 hello OMS 확장 hello 가상 컴퓨터 리소스 내에 중첩 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-141">hello following example assumes hello OMS extension is nested inside hello virtual machine resource.</span></span> <span data-ttu-id="30cdb-142">Hello JSON hello에 위치한 hello 확장을 리소스를 중첩할 때 `"resources": []` hello 가상 컴퓨터의 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-142">When nesting hello extension resource, hello JSON is placed in hello `"resources": []` object of hello virtual machine.</span></span>


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

<span data-ttu-id="30cdb-143">Hello 서식 파일의 루트 hello에 hello 확장 JSON를 배치할 때 참조 toohello 부모 가상 컴퓨터를 포함 하는 hello 리소스 이름 및 hello 유형은 hello 중첩 된 구성에 반영 합니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-143">When placing hello extension JSON at hello root of hello template, hello resource name includes a reference toohello parent virtual machine, and hello type reflects hello nested configuration.</span></span> 

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

## <a name="powershell-deployment"></a><span data-ttu-id="30cdb-144">PowerShell 배포</span><span class="sxs-lookup"><span data-stu-id="30cdb-144">PowerShell deployment</span></span>

<span data-ttu-id="30cdb-145">hello `Set-AzureRmVMExtension` 명령을 사용 하는 toodeploy hello OMS 에이전트 가상 컴퓨터 확장 tooan 기존 가상 컴퓨터 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-145">hello `Set-AzureRmVMExtension` command can be used toodeploy hello OMS Agent virtual machine extension tooan existing virtual machine.</span></span> <span data-ttu-id="30cdb-146">Hello 명령을 실행 하기 전에 hello 공용 및 개인 구성 PowerShell 해시 테이블에 저장 된 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-146">Before running hello command, hello public and private configurations need toobe stored in a PowerShell hash table.</span></span> 

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

## <a name="troubleshoot-and-support"></a><span data-ttu-id="30cdb-147">문제 해결 및 지원</span><span class="sxs-lookup"><span data-stu-id="30cdb-147">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="30cdb-148">문제 해결</span><span class="sxs-lookup"><span data-stu-id="30cdb-148">Troubleshoot</span></span>

<span data-ttu-id="30cdb-149">Hello Azure 포털에서에서 하 고 hello Azure PowerShell 모듈을 사용 하 여 확장 배포의 hello 상태에 대 한 데이터를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-149">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="30cdb-150">지정 된 VM 사용 하 여 명령을 다음 실행된 hello에 대 한 확장의 toosee hello 배포 상태 hello Azure PowerShell 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-150">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="30cdb-151">확장 실행은 hello에 기록 된 toofiles 다음 디렉터리를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-151">Extension execution output is logged toofiles found in hello following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\
```

### <a name="support"></a><span data-ttu-id="30cdb-152">지원</span><span class="sxs-lookup"><span data-stu-id="30cdb-152">Support</span></span>

<span data-ttu-id="30cdb-153">이 문서에서 언제 든 지 자세한 도움말을 보려는 경우 문의할 수 있습니다 Azure 전문가의 hello hello [MSDN Azure 및 스택 오버플로 포럼](https://azure.microsoft.com/en-us/support/forums/)합니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-153">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="30cdb-154">또는 Azure 기술 지원 인시던트를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-154">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="30cdb-155">Toohello 이동 [Azure 지원 사이트](https://azure.microsoft.com/en-us/support/options/) 지원 받기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-155">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="30cdb-156">Azure 지원을 사용 하는 방법에 대 한 내용은 하세요 hello [Microsoft Azure 지원 FAQ](https://azure.microsoft.com/en-us/support/faq/)합니다.</span><span class="sxs-lookup"><span data-stu-id="30cdb-156">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
