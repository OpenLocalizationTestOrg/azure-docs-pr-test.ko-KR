---
title: "VM 확장을 포함 하는 Azure 리소스 그룹 aaaExporting | Microsoft Docs"
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
ms.openlocfilehash: cdbc2030988a19fe68429e8733dc60536c264abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a><span data-ttu-id="b99c1-103">VM 확장을 포함하는 리소스 그룹 내보내기</span><span class="sxs-lookup"><span data-stu-id="b99c1-103">Exporting Resource Groups that contain VM extensions</span></span>

<span data-ttu-id="b99c1-104">Azure 리소스 그룹을 새 Resource Manager 템플릿으로 내보낸 후 다시 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-104">Azure Resource Groups can be exported into a new Resource Manager template that can then be redeployed.</span></span> <span data-ttu-id="b99c1-105">hello 내보내기 프로세스 기존 리소스를 해석 하 고 배포할 때 리소스 관리자 템플릿을 만들고 비슷한 리소스 그룹에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-105">hello export process interprets existing resources, and creates a Resource Manager template that when deployed results in a similar Resource Group.</span></span> <span data-ttu-id="b99c1-106">가상 컴퓨터 확장을 포함 하는 리소스 그룹에 대 한 hello 리소스 그룹 내보내기 옵션을 사용할 경우 몇 가지 항목 필요 toobe 확장 호환성 같은 것으로 간주 하 고 설정을 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-106">When using hello Resource Group export option against a Resource Group containing Virtual Machine extensions, several items need toobe considered such as extension compatibility and protected settings.</span></span>

<span data-ttu-id="b99c1-107">이 문서 정보 hello 리소스 그룹 내보내기 프로세스의 목록이 포함 되는 가상 컴퓨터 확장에 대 한 작동 하는 방법에 확장을 지원 하 고 처리에 대 한 세부 정보 데이터를 보안 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-107">This document details how hello Resource Group export process works regarding virtual machine extensions, including a list of supported extensions, and details on handling secured data.</span></span>

## <a name="supported-virtual-machine-extensions"></a><span data-ttu-id="b99c1-108">지원되는 가상 컴퓨터 확장</span><span class="sxs-lookup"><span data-stu-id="b99c1-108">Supported Virtual Machine Extensions</span></span>

<span data-ttu-id="b99c1-109">여러 가상 컴퓨터 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-109">Many Virtual Machine extensions are available.</span></span> <span data-ttu-id="b99c1-110">모든 확장이 hello "자동화 스크립트" 기능을 사용 하 여 리소스 관리자 템플릿으로 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-110">Not all extensions can be exported into a Resource Manager template using hello “Automation Script” feature.</span></span> <span data-ttu-id="b99c1-111">가상 컴퓨터 확장 지원 되지 않는 경우 수동으로 hello 내보낸된 서식 파일에 다시 배치 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-111">If a virtual machine extension is not supported, it needs toobe manually placed back into hello exported template.</span></span>

<span data-ttu-id="b99c1-112">hello 다음 확장 프로그램 내보낼 수 있습니다 hello 자동화 스크립트 기능.</span><span class="sxs-lookup"><span data-stu-id="b99c1-112">hello following extensions can be exported with hello automation script feature.</span></span>

| <span data-ttu-id="b99c1-113">내선 번호</span><span class="sxs-lookup"><span data-stu-id="b99c1-113">Extension</span></span> ||||
|---|---|---|---|
| <span data-ttu-id="b99c1-114">Acronis Backup</span><span class="sxs-lookup"><span data-stu-id="b99c1-114">Acronis Backup</span></span> | <span data-ttu-id="b99c1-115">Datadog Windows Agent</span><span class="sxs-lookup"><span data-stu-id="b99c1-115">Datadog Windows Agent</span></span> | <span data-ttu-id="b99c1-116">OS Patching For Linux</span><span class="sxs-lookup"><span data-stu-id="b99c1-116">OS Patching For Linux</span></span> | <span data-ttu-id="b99c1-117">VM Snapshot Linux</span><span class="sxs-lookup"><span data-stu-id="b99c1-117">VM Snapshot Linux</span></span>
| <span data-ttu-id="b99c1-118">Acronis Backup Linux</span><span class="sxs-lookup"><span data-stu-id="b99c1-118">Acronis Backup Linux</span></span> | <span data-ttu-id="b99c1-119">Docker 확장</span><span class="sxs-lookup"><span data-stu-id="b99c1-119">Docker Extension</span></span> | <span data-ttu-id="b99c1-120">Puppet Agent</span><span class="sxs-lookup"><span data-stu-id="b99c1-120">Puppet Agent</span></span> |
| <span data-ttu-id="b99c1-121">Bg Info</span><span class="sxs-lookup"><span data-stu-id="b99c1-121">Bg Info</span></span> | <span data-ttu-id="b99c1-122">DSC Extension</span><span class="sxs-lookup"><span data-stu-id="b99c1-122">DSC Extension</span></span> | <span data-ttu-id="b99c1-123">Site 24x7 Apm Insight</span><span class="sxs-lookup"><span data-stu-id="b99c1-123">Site 24x7 Apm Insight</span></span> |
| <span data-ttu-id="b99c1-124">BMC CTM Agent Linux</span><span class="sxs-lookup"><span data-stu-id="b99c1-124">BMC CTM Agent Linux</span></span> | <span data-ttu-id="b99c1-125">Dynatrace Linux</span><span class="sxs-lookup"><span data-stu-id="b99c1-125">Dynatrace Linux</span></span> | <span data-ttu-id="b99c1-126">Site 24x7 Linux Server</span><span class="sxs-lookup"><span data-stu-id="b99c1-126">Site 24x7 Linux Server</span></span> |
| <span data-ttu-id="b99c1-127">BMC CTM Agent Windows</span><span class="sxs-lookup"><span data-stu-id="b99c1-127">BMC CTM Agent Windows</span></span> | <span data-ttu-id="b99c1-128">Dynatrace Windows</span><span class="sxs-lookup"><span data-stu-id="b99c1-128">Dynatrace Windows</span></span> | <span data-ttu-id="b99c1-129">Site 24x7 Windows Server</span><span class="sxs-lookup"><span data-stu-id="b99c1-129">Site 24x7 Windows Server</span></span> |
| <span data-ttu-id="b99c1-130">Chef Client</span><span class="sxs-lookup"><span data-stu-id="b99c1-130">Chef Client</span></span> | <span data-ttu-id="b99c1-131">HPE Security Application Defender</span><span class="sxs-lookup"><span data-stu-id="b99c1-131">HPE Security Application Defender</span></span> | <span data-ttu-id="b99c1-132">Trend Micro DSA</span><span class="sxs-lookup"><span data-stu-id="b99c1-132">Trend Micro DSA</span></span> |
| <span data-ttu-id="b99c1-133">Custom Script</span><span class="sxs-lookup"><span data-stu-id="b99c1-133">Custom Script</span></span> | <span data-ttu-id="b99c1-134">IaaS Antimalware</span><span class="sxs-lookup"><span data-stu-id="b99c1-134">IaaS Antimalware</span></span> | <span data-ttu-id="b99c1-135">Trend Micro DSA Linux</span><span class="sxs-lookup"><span data-stu-id="b99c1-135">Trend Micro DSA Linux</span></span> |
| <span data-ttu-id="b99c1-136">사용자 지정 스크립트 확장</span><span class="sxs-lookup"><span data-stu-id="b99c1-136">Custom Script Extension</span></span> | <span data-ttu-id="b99c1-137">IaaS Diagnostics</span><span class="sxs-lookup"><span data-stu-id="b99c1-137">IaaS Diagnostics</span></span> | <span data-ttu-id="b99c1-138">VM Access For Linux</span><span class="sxs-lookup"><span data-stu-id="b99c1-138">VM Access For Linux</span></span> |
| <span data-ttu-id="b99c1-139">Custom Script for Linux</span><span class="sxs-lookup"><span data-stu-id="b99c1-139">Custom Script for Linux</span></span> | <span data-ttu-id="b99c1-140">Linux Chef Client</span><span class="sxs-lookup"><span data-stu-id="b99c1-140">Linux Chef Client</span></span> | <span data-ttu-id="b99c1-141">VM Access For Linux</span><span class="sxs-lookup"><span data-stu-id="b99c1-141">VM Access For Linux</span></span> |
| <span data-ttu-id="b99c1-142">Datadog Linux Agent</span><span class="sxs-lookup"><span data-stu-id="b99c1-142">Datadog Linux Agent</span></span> | <span data-ttu-id="b99c1-143">Linux Diagnostic</span><span class="sxs-lookup"><span data-stu-id="b99c1-143">Linux Diagnostic</span></span> | <span data-ttu-id="b99c1-144">VM Snapshot</span><span class="sxs-lookup"><span data-stu-id="b99c1-144">VM Snapshot</span></span> |

## <a name="export-hello-resource-group"></a><span data-ttu-id="b99c1-145">내보내기 hello 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="b99c1-145">Export hello Resource Group</span></span>

<span data-ttu-id="b99c1-146">리소스 그룹을 다시 사용할 수 있는 템플릿으로 단계를 수행 하는 전체 hello tooexport:</span><span class="sxs-lookup"><span data-stu-id="b99c1-146">tooexport a Resource Group into a reusable template, complete hello following steps:</span></span>

1. <span data-ttu-id="b99c1-147">Azure 포털 toohello에 로그인</span><span class="sxs-lookup"><span data-stu-id="b99c1-147">Sign in toohello Azure portal</span></span>
2. <span data-ttu-id="b99c1-148">Hello 허브 메뉴에서 리소스 그룹을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-148">On hello Hub Menu, click Resource Groups</span></span>
3. <span data-ttu-id="b99c1-149">Hello 목록에서 hello 대상 리소스 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-149">Select hello target resource group from hello list</span></span>
4. <span data-ttu-id="b99c1-150">Hello 리소스 그룹 블레이드에서 자동화 스크립트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-150">In hello Resource Group blade, click Automation Script</span></span>

![템플릿 내보내기](./media/extensions-export-templates/template-export.png)

<span data-ttu-id="b99c1-152">hello Azure 리소스 관리자 자동화 스크립트는 리소스 관리자 템플릿, 매개 변수 파일 및 PowerShell 및 Azure CLI 같은 몇 가지 예제 배포 스크립트를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-152">hello Azure Resource Manager automations script produces a Resource Manager template, a parameters file, and several sample deployment scripts such as PowerShell and Azure CLI.</span></span> <span data-ttu-id="b99c1-153">이 시점에서 hello 내보낸된 템플릿을 다운로드할 수 있습니다으로 새 템플릿 toohello 템플릿 라이브러리를 추가 하거나 hello를 사용 하 여 다시 배포한 hello 다운로드 단추를 사용 하 여 단추를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-153">At this point, hello exported template can be downloaded using hello download button, added as a new template toohello template library, or redeployed using hello deploy button.</span></span>

## <a name="configure-protected-settings"></a><span data-ttu-id="b99c1-154">보호 설정 구성</span><span class="sxs-lookup"><span data-stu-id="b99c1-154">Configure protected settings</span></span>

<span data-ttu-id="b99c1-155">여러 Azure Virtual Machine 확장에는 자격 증명 및 구성 문자열과 같은 중요한 데이터를 암호화하는 보호 설정 구성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-155">Many Azure virtual machine extensions include a protected settings configuration, that encrypts sensitive data such as credentials and configuration strings.</span></span> <span data-ttu-id="b99c1-156">보호 된 설정 hello 자동화 스크립트와 함께 내보낼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-156">Protected settings are not exported with hello automation script.</span></span> <span data-ttu-id="b99c1-157">필요한, 보호 된 설정을 hello에 다시 삽입할 toobe 필요한 템플릿 기반 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-157">If necessary, protected settings need toobe reinserted into hello exported templated.</span></span>

### <a name="step-1---remove-template-parameter"></a><span data-ttu-id="b99c1-158">1단계 - 템플릿 매개 변수 제거</span><span class="sxs-lookup"><span data-stu-id="b99c1-158">Step 1 - Remove template parameter</span></span>

<span data-ttu-id="b99c1-159">리소스 그룹을 내보내는 hello 단일 템플릿 매개 변수를 만들면 tooprovide 값 toohello 보호 설정을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-159">When hello Resource Group is exported, a single template parameter is created tooprovide a value toohello exported protected settings.</span></span> <span data-ttu-id="b99c1-160">이 매개 변수는 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-160">This parameter can be removed.</span></span> <span data-ttu-id="b99c1-161">tooremove hello 매개 변수를 hello 매개 변수 목록 전체를 검사 하 고 다음과 비슷한 toothis JSON의 예는 hello 매개 변수를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-161">tooremove hello parameter, look through hello parameter list and delete hello parameter that looks similar toothis JSON example.</span></span>

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a><span data-ttu-id="b99c1-162">2단계 - 보호 설정 속성 가져오기</span><span class="sxs-lookup"><span data-stu-id="b99c1-162">Step 2 - Get protected settings properties</span></span>

<span data-ttu-id="b99c1-163">각 보호 설정을 필수 속성의 집합을 사용 하므로 이러한 속성 목록은 수집 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-163">Because each protected setting has a set of required properties, a list of these properties need toobe gathered.</span></span> <span data-ttu-id="b99c1-164">Hello에 hello 보호 설정 구성의 각 매개 변수에 있습니다 [GitHub의 Azure 리소스 관리자 스키마](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-164">Each parameter of hello protected settings configuration can be found in hello [Azure Resource Manager schema on GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span></span> <span data-ttu-id="b99c1-165">이 스키마는이 문서의 hello 개요 섹션에 나열 된 hello 확장에 대 한 hello 매개 변수 집합을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-165">This schema only includes hello parameter sets for hello extensions listed in hello overview section of this document.</span></span> 

<span data-ttu-id="b99c1-166">Hello 스키마 리포지토리 내에서 검색할이 예제에 대 한 원하는 hello 확장 `IaaSDiagnostics`합니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-166">From within hello schema repository, search for hello desired extension, for this example `IaaSDiagnostics`.</span></span> <span data-ttu-id="b99c1-167">한 번 확장 hello `protectedSettings` 개체 찾았습니다, 각 매개 변수를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-167">Once hello extensions `protectedSettings` object has been located, take note of each parameter.</span></span> <span data-ttu-id="b99c1-168">Hello의 hello 예제에서 `IaasDiagnostic` 확장 프로그램, hello 필요한 매개 변수는 `storageAccountName`, `storageAccountKey`, 및 `storageAccountEndPoint`합니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-168">In hello example of hello `IaasDiagnostic` extension, hello require parameters are `storageAccountName`, `storageAccountKey`, and `storageAccountEndPoint`.</span></span>

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

### <a name="step-3---re-create-hello-protected-configuration"></a><span data-ttu-id="b99c1-169">3 단계-hello 보호 구성 다시 만들기</span><span class="sxs-lookup"><span data-stu-id="b99c1-169">Step 3 - Re-create hello protected configuration</span></span>

<span data-ttu-id="b99c1-170">내보낸된 템플릿 hello, 검색할 `protectedSettings` 개체를 내보낸된 보호 설정 하는 hello hello 필요한 확장 프로그램 매개 변수 및 각각에 대 한 값을 포함 하는 새 항목으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-170">On hello exported template, search for `protectedSettings` and replace hello exported protected setting object with a new one that includes hello required extension parameters and a value for each one.</span></span>

<span data-ttu-id="b99c1-171">Hello의 hello 예제에서 `IaasDiagnostic` 확장명 hello 새 보호 설정 구성 같습니다. 다음 예제는 hello:</span><span class="sxs-lookup"><span data-stu-id="b99c1-171">In hello example of hello `IaasDiagnostic` extension, hello new protected setting configuration would look like hello following example:</span></span>

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

<span data-ttu-id="b99c1-172">hello 최종 확장을 리소스에는 다음 JSON 예제와 비슷한 toohello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-172">hello final extension resource looks similar toohello following JSON example:</span></span>

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

<span data-ttu-id="b99c1-173">템플릿 매개 변수 tooprovide 속성 값을 사용 하는 경우 이러한 만든 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-173">If using template parameters tooprovide property values, these need toobe created.</span></span> <span data-ttu-id="b99c1-174">템플릿 매개 변수 값을 설정 하는 보호 된를 만들 때 확인 되었는지 toouse hello `SecureString` 매개 변수를 입력 하 여 중요 한 값 보안이 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-174">When creating template parameters for protected setting values, make sure toouse hello `SecureString` parameter type so that sensitive values are secured.</span></span> <span data-ttu-id="b99c1-175">매개 변수 사용에 대한 자세한 내용은 [Azure Resource Manager 템플릿 작성](../../resource-group-authoring-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b99c1-175">For more information on using parameters, see [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="b99c1-176">Hello의 hello 예제에서 `IaasDiagnostic` 확장명 hello 매개 변수 뒤에 만들어짐 hello 리소스 관리자 템플릿의 hello 매개 변수 섹션.</span><span class="sxs-lookup"><span data-stu-id="b99c1-176">In hello example of hello `IaasDiagnostic` extension, hello following parameters would be created in hello parameters section of hello Resource Manager template.</span></span>

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

<span data-ttu-id="b99c1-177">이 시점에서 hello 템플릿에 템플릿 배포 방법을 사용 하 여 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b99c1-177">At this point, hello template can be deployed using any template deployment method.</span></span>
