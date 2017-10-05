---
title: "VM 확장을 포함하는 Azure 리소스 그룹 내보내기 | Microsoft Docs"
description: "가상 컴퓨터 확장을 포함하는 Resource Manager 템플릿을 내보냅니다."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7f4e2ca6-f1c7-4f59-a2cc-8f63132de279
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: nepeters
ms.openlocfilehash: cc3c705f1c9123de75ced016a5b39eb1a86b0f73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a><span data-ttu-id="c41e8-103">VM 확장을 포함하는 리소스 그룹 내보내기</span><span class="sxs-lookup"><span data-stu-id="c41e8-103">Exporting Resource Groups that contain VM extensions</span></span>

<span data-ttu-id="c41e8-104">Azure 리소스 그룹을 새 Resource Manager 템플릿으로 내보낸 후 다시 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-104">Azure Resource Groups can be exported into a new Resource Manager template that can then be redeployed.</span></span> <span data-ttu-id="c41e8-105">내보내기 프로세스 중에 기존 리소스가 해석되고, 배포 시 비슷한 리소스 그룹을 생성하는 Resource Manager 템플릿이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-105">The export process interprets existing resources, and creates a Resource Manager template that when deployed results in a similar Resource Group.</span></span> <span data-ttu-id="c41e8-106">가상 컴퓨터 확장을 포함하는 리소스 그룹에 대해 리소스 그룹 내보내기 옵션을 사용할 경우 확장 호환성 및 보호된 설정과 같은 몇 가지 항목을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-106">When using the Resource Group export option against a Resource Group containing Virtual Machine extensions, several items need to be considered such as extension compatibility and protected settings.</span></span>

<span data-ttu-id="c41e8-107">이 문서에서는 지원되는 확장 목록을 비롯하여 가상 컴퓨터 확장과 관련된 리소스 그룹 내보내기 프로세스의 작동 방식과 보안 데이터 처리에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-107">This document details how the Resource Group export process works regarding virtual machine extensions, including a list of supported extensions, and details on handling secured data.</span></span>

## <a name="supported-virtual-machine-extensions"></a><span data-ttu-id="c41e8-108">지원되는 가상 컴퓨터 확장</span><span class="sxs-lookup"><span data-stu-id="c41e8-108">Supported Virtual Machine Extensions</span></span>

<span data-ttu-id="c41e8-109">여러 가상 컴퓨터 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-109">Many Virtual Machine extensions are available.</span></span> <span data-ttu-id="c41e8-110">모든 확장을 "Automation 스크립트" 기능을 사용하여 Resource Manager 템플릿으로 내보낼 수 있는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-110">Not all extensions can be exported into a Resource Manager template using the “Automation Script” feature.</span></span> <span data-ttu-id="c41e8-111">가상 컴퓨터 확장이 지원되지 않는 경우 내보낸 템플릿에 수동으로 다시 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-111">If a virtual machine extension is not supported, it needs to be manually placed back into the exported template.</span></span>

<span data-ttu-id="c41e8-112">Automation 스크립트 기능을 사용하여 다음 확장을 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-112">The following extensions can be exported with the automation script feature.</span></span>

| <span data-ttu-id="c41e8-113">내선 번호</span><span class="sxs-lookup"><span data-stu-id="c41e8-113">Extension</span></span> ||||
|---|---|---|---|
| <span data-ttu-id="c41e8-114">Acronis Backup</span><span class="sxs-lookup"><span data-stu-id="c41e8-114">Acronis Backup</span></span> | <span data-ttu-id="c41e8-115">Datadog Windows Agent</span><span class="sxs-lookup"><span data-stu-id="c41e8-115">Datadog Windows Agent</span></span> | <span data-ttu-id="c41e8-116">OS Patching For Linux</span><span class="sxs-lookup"><span data-stu-id="c41e8-116">OS Patching For Linux</span></span> | <span data-ttu-id="c41e8-117">VM Snapshot Linux</span><span class="sxs-lookup"><span data-stu-id="c41e8-117">VM Snapshot Linux</span></span>
| <span data-ttu-id="c41e8-118">Acronis Backup Linux</span><span class="sxs-lookup"><span data-stu-id="c41e8-118">Acronis Backup Linux</span></span> | <span data-ttu-id="c41e8-119">Docker 확장</span><span class="sxs-lookup"><span data-stu-id="c41e8-119">Docker Extension</span></span> | <span data-ttu-id="c41e8-120">Puppet Agent</span><span class="sxs-lookup"><span data-stu-id="c41e8-120">Puppet Agent</span></span> |
| <span data-ttu-id="c41e8-121">Bg Info</span><span class="sxs-lookup"><span data-stu-id="c41e8-121">Bg Info</span></span> | <span data-ttu-id="c41e8-122">DSC Extension</span><span class="sxs-lookup"><span data-stu-id="c41e8-122">DSC Extension</span></span> | <span data-ttu-id="c41e8-123">Site 24x7 Apm Insight</span><span class="sxs-lookup"><span data-stu-id="c41e8-123">Site 24x7 Apm Insight</span></span> |
| <span data-ttu-id="c41e8-124">BMC CTM Agent Linux</span><span class="sxs-lookup"><span data-stu-id="c41e8-124">BMC CTM Agent Linux</span></span> | <span data-ttu-id="c41e8-125">Dynatrace Linux</span><span class="sxs-lookup"><span data-stu-id="c41e8-125">Dynatrace Linux</span></span> | <span data-ttu-id="c41e8-126">Site 24x7 Linux Server</span><span class="sxs-lookup"><span data-stu-id="c41e8-126">Site 24x7 Linux Server</span></span> |
| <span data-ttu-id="c41e8-127">BMC CTM Agent Windows</span><span class="sxs-lookup"><span data-stu-id="c41e8-127">BMC CTM Agent Windows</span></span> | <span data-ttu-id="c41e8-128">Dynatrace Windows</span><span class="sxs-lookup"><span data-stu-id="c41e8-128">Dynatrace Windows</span></span> | <span data-ttu-id="c41e8-129">Site 24x7 Windows Server</span><span class="sxs-lookup"><span data-stu-id="c41e8-129">Site 24x7 Windows Server</span></span> |
| <span data-ttu-id="c41e8-130">Chef Client</span><span class="sxs-lookup"><span data-stu-id="c41e8-130">Chef Client</span></span> | <span data-ttu-id="c41e8-131">HPE Security Application Defender</span><span class="sxs-lookup"><span data-stu-id="c41e8-131">HPE Security Application Defender</span></span> | <span data-ttu-id="c41e8-132">Trend Micro DSA</span><span class="sxs-lookup"><span data-stu-id="c41e8-132">Trend Micro DSA</span></span> |
| <span data-ttu-id="c41e8-133">Custom Script</span><span class="sxs-lookup"><span data-stu-id="c41e8-133">Custom Script</span></span> | <span data-ttu-id="c41e8-134">IaaS Antimalware</span><span class="sxs-lookup"><span data-stu-id="c41e8-134">IaaS Antimalware</span></span> | <span data-ttu-id="c41e8-135">Trend Micro DSA Linux</span><span class="sxs-lookup"><span data-stu-id="c41e8-135">Trend Micro DSA Linux</span></span> |
| <span data-ttu-id="c41e8-136">사용자 지정 스크립트 확장</span><span class="sxs-lookup"><span data-stu-id="c41e8-136">Custom Script Extension</span></span> | <span data-ttu-id="c41e8-137">IaaS Diagnostics</span><span class="sxs-lookup"><span data-stu-id="c41e8-137">IaaS Diagnostics</span></span> | <span data-ttu-id="c41e8-138">VM Access For Linux</span><span class="sxs-lookup"><span data-stu-id="c41e8-138">VM Access For Linux</span></span> |
| <span data-ttu-id="c41e8-139">Custom Script for Linux</span><span class="sxs-lookup"><span data-stu-id="c41e8-139">Custom Script for Linux</span></span> | <span data-ttu-id="c41e8-140">Linux Chef Client</span><span class="sxs-lookup"><span data-stu-id="c41e8-140">Linux Chef Client</span></span> | <span data-ttu-id="c41e8-141">VM Access For Linux</span><span class="sxs-lookup"><span data-stu-id="c41e8-141">VM Access For Linux</span></span> |
| <span data-ttu-id="c41e8-142">Datadog Linux Agent</span><span class="sxs-lookup"><span data-stu-id="c41e8-142">Datadog Linux Agent</span></span> | <span data-ttu-id="c41e8-143">Linux Diagnostic</span><span class="sxs-lookup"><span data-stu-id="c41e8-143">Linux Diagnostic</span></span> | <span data-ttu-id="c41e8-144">VM Snapshot</span><span class="sxs-lookup"><span data-stu-id="c41e8-144">VM Snapshot</span></span> |

## <a name="export-the-resource-group"></a><span data-ttu-id="c41e8-145">리소스 그룹 내보내기</span><span class="sxs-lookup"><span data-stu-id="c41e8-145">Export the Resource Group</span></span>

<span data-ttu-id="c41e8-146">리소스 그룹을 다시 사용할 수 있는 템플릿으로 내보내려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-146">To export a Resource Group into a reusable template, complete the following steps:</span></span>

1. <span data-ttu-id="c41e8-147">Azure 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-147">Sign in to the Azure portal</span></span>
2. <span data-ttu-id="c41e8-148">허브 메뉴에서 리소스 그룹 클릭</span><span class="sxs-lookup"><span data-stu-id="c41e8-148">On the Hub Menu, click Resource Groups</span></span>
3. <span data-ttu-id="c41e8-149">목록에서 대상 리소스 그룹 선택</span><span class="sxs-lookup"><span data-stu-id="c41e8-149">Select the target resource group from the list</span></span>
4. <span data-ttu-id="c41e8-150">리소스 그룹 블레이드에서 Automation 스크립트 클릭</span><span class="sxs-lookup"><span data-stu-id="c41e8-150">In the Resource Group blade, click Automation Script</span></span>

![템플릿 내보내기](./media/extensions-export-templates/template-export.png)

<span data-ttu-id="c41e8-152">Azure Resource Manager Automation 스크립트는 Resource Manager 템플릿, 매개 변수 파일, PowerShell 및 Azure CLI와 같은 몇 가지 샘플 배포 스크립트를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-152">The Azure Resource Manager automations script produces a Resource Manager template, a parameters file, and several sample deployment scripts such as PowerShell and Azure CLI.</span></span> <span data-ttu-id="c41e8-153">이제 내보낸 템플릿을 다운로드 단추를 사용하여 다운로드하거나, 템플릿 라이브러리에 새 템플릿으로 추가하거나, 배포 단추를 사용하여 다시 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-153">At this point, the exported template can be downloaded using the download button, added as a new template to the template library, or redeployed using the deploy button.</span></span>

## <a name="configure-protected-settings"></a><span data-ttu-id="c41e8-154">보호 설정 구성</span><span class="sxs-lookup"><span data-stu-id="c41e8-154">Configure protected settings</span></span>

<span data-ttu-id="c41e8-155">여러 Azure Virtual Machine 확장에는 자격 증명 및 구성 문자열과 같은 중요한 데이터를 암호화하는 보호 설정 구성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-155">Many Azure virtual machine extensions include a protected settings configuration, that encrypts sensitive data such as credentials and configuration strings.</span></span> <span data-ttu-id="c41e8-156">보호 설정은 Automation 스크립트를 사용하여 내보낼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-156">Protected settings are not exported with the automation script.</span></span> <span data-ttu-id="c41e8-157">필요하면 보호 설정을 내보낸 템플릿에 다시 삽입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-157">If necessary, protected settings need to be reinserted into the exported templated.</span></span>

### <a name="step-1---remove-template-parameter"></a><span data-ttu-id="c41e8-158">1단계 - 템플릿 매개 변수 제거</span><span class="sxs-lookup"><span data-stu-id="c41e8-158">Step 1 - Remove template parameter</span></span>

<span data-ttu-id="c41e8-159">리소스 그룹을 내보낼 때 내보낸 보호 설정에 값을 제공하는 단일 템플릿 매개 변수가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-159">When the Resource Group is exported, a single template parameter is created to provide a value to the exported protected settings.</span></span> <span data-ttu-id="c41e8-160">이 매개 변수는 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-160">This parameter can be removed.</span></span> <span data-ttu-id="c41e8-161">이 매개 변수를 제거하려면 매개 변수 목록을 확인하고 이 JSON 예제와 유사한 매개 변수를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-161">To remove the parameter, look through the parameter list and delete the parameter that looks similar to this JSON example.</span></span>

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a><span data-ttu-id="c41e8-162">2단계 - 보호 설정 속성 가져오기</span><span class="sxs-lookup"><span data-stu-id="c41e8-162">Step 2 - Get protected settings properties</span></span>

<span data-ttu-id="c41e8-163">각 보호 설정에는 필수 속성 집합이 있으므로 이러한 속성의 목록을 수집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-163">Because each protected setting has a set of required properties, a list of these properties need to be gathered.</span></span> <span data-ttu-id="c41e8-164">보호 설정 구성의 각 매개 변수는 [GitHub의 Azure Resource Manager 스키마](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-164">Each parameter of the protected settings configuration can be found in the [Azure Resource Manager schema on GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span></span> <span data-ttu-id="c41e8-165">이 스키마는 이 문서의 개요 섹션에 나열된 확장에 대한 매개 변수 집합만 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-165">This schema only includes the parameter sets for the extensions listed in the overview section of this document.</span></span> 

<span data-ttu-id="c41e8-166">스키마 리포지토리 내에서 원하는 확장(이 예제에서는 `IaaSDiagnostics`)을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-166">From within the schema repository, search for the desired extension, for this example `IaaSDiagnostics`.</span></span> <span data-ttu-id="c41e8-167">확장 `protectedSettings` 개체를 찾으면 각 매개 변수를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-167">Once the extensions `protectedSettings` object has been located, take note of each parameter.</span></span> <span data-ttu-id="c41e8-168">`IaasDiagnostic` 확장 예제에서는 `storageAccountName`, `storageAccountKey` 및 `storageAccountEndPoint` 매개 변수가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-168">In the example of the `IaasDiagnostic` extension, the require parameters are `storageAccountName`, `storageAccountKey`, and `storageAccountEndPoint`.</span></span>

```json
"protectedSettings": {
    "type": "object",
    "properties": {
        "storageAccountName": {
            "type": "string"
        },
        "storageAccountKey": {
            "type": "string"
        },
        "storageAccountEndPoint": {
            "type": "string"
        }
    },
    "required": [
        "storageAccountName",
        "storageAccountKey",
        "storageAccountEndPoint"
    ]
}
```

### <a name="step-3---re-create-the-protected-configuration"></a><span data-ttu-id="c41e8-169">3단계 - 보호되는 구성 다시 만들기</span><span class="sxs-lookup"><span data-stu-id="c41e8-169">Step 3 - Re-create the protected configuration</span></span>

<span data-ttu-id="c41e8-170">내보낸 템플릿에서 `protectedSettings`를 검색하고 내보낸된 보호 설정 개체를 필수 확장 매개 변수 및 각 매개 변수의 값을 포함하는 새 개체로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-170">On the exported template, search for `protectedSettings` and replace the exported protected setting object with a new one that includes the required extension parameters and a value for each one.</span></span>

<span data-ttu-id="c41e8-171">`IaasDiagnostic` 확장 예제에서 새로운 보호 설정 구성은 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-171">In the example of the `IaasDiagnostic` extension, the new protected setting configuration would look like the following example:</span></span>

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

<span data-ttu-id="c41e8-172">최종 확장 리소스는 다음 JSON 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-172">The final extension resource looks similar to the following JSON example:</span></span>

```json
{
    "name": "Microsoft.Insights.VMDiagnosticsSettings",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "[variables('apiVersion')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "tags": {
        "displayName": "AzureDiagnostics"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
            "storageAccountName": "[parameters('storageAccountName')]",
            "storageAccountKey": "[parameters('storageAccountKey')]",
            "storageAccountEndPoint": "https://core.windows.net"
        }
    }
}
```

<span data-ttu-id="c41e8-173">템플릿 매개 변수를 사용하여 속성 값을 제공하려면 이러한 항목을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-173">If using template parameters to provide property values, these need to be created.</span></span> <span data-ttu-id="c41e8-174">보호 설정 값에 대해 템플릿 매개 변수를 만들 경우 중요한 값이 보호되도록 `SecureString` 매개 변수 형식을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-174">When creating template parameters for protected setting values, make sure to use the `SecureString` parameter type so that sensitive values are secured.</span></span> <span data-ttu-id="c41e8-175">매개 변수 사용에 대한 자세한 내용은 [Azure Resource Manager 템플릿 작성](../../resource-group-authoring-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c41e8-175">For more information on using parameters, see [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="c41e8-176">`IaasDiagnostic` 확장 예제에서는 Resource Manager 템플릿의 매개 변수 섹션에서 다음 매개 변수가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-176">In the example of the `IaasDiagnostic` extension, the following parameters would be created in the parameters section of the Resource Manager template.</span></span>

```json
"storageAccountName": {
    "defaultValue": null,
    "type": "SecureString"
},
"storageAccountKey": {
    "defaultValue": null,
    "type": "SecureString"
}
```

<span data-ttu-id="c41e8-177">이제 템플릿 배포 방법을 사용하여 템플릿을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c41e8-177">At this point, the template can be deployed using any template deployment method.</span></span>
