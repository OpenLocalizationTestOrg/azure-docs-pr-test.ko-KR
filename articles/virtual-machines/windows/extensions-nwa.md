---
title: "Windows에 대 한 네트워크 감시자 에이전트가 가상 컴퓨터 확장 aaaAzure | Microsoft Docs"
description: "가상 컴퓨터 확장을 사용 하 여 Windows 가상 컴퓨터에서 네트워크 감시자 에이전트 hello를 배포 합니다."
services: virtual-machines-windows
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 27e46af7-2150-45e8-b084-ba33de8c5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 21298706e462ff32c4d314f9a1ad127074ddf481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-windows"></a><span data-ttu-id="08a25-103">Windows용 Network Watcher 에이전트 가상 컴퓨터 확장</span><span class="sxs-lookup"><span data-stu-id="08a25-103">Network Watcher Agent virtual machine extension for Windows</span></span>

## <a name="overview"></a><span data-ttu-id="08a25-104">개요</span><span class="sxs-lookup"><span data-stu-id="08a25-104">Overview</span></span>

<span data-ttu-id="08a25-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/)는 Azure 네트워크에 대한 모니터링을 허용하는 네트워크 성능 모니터링, 진단 및 분석 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="08a25-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="08a25-106">네트워크 감시자 에이전트가 가상 컴퓨터 확장 hello hello Azure 가상 컴퓨터 네트워크 감시자 기능 중 일부에 대 한 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="08a25-106">hello Network Watcher Agent virtual machine extension is a requirement for some of hello Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="08a25-107">주문형 네트워크 트래픽을 캡처하는 기능 및 기타 고급 기능이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="08a25-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="08a25-108">이 문서 정보 hello windows hello 네트워크 감시자 에이전트가 가상 컴퓨터 확장에 대 한 플랫폼 및 배포 옵션을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a25-108">This document details hello supported platforms and deployment options for hello Network Watcher Agent virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08a25-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="08a25-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="08a25-110">운영 체제</span><span class="sxs-lookup"><span data-stu-id="08a25-110">Operating system</span></span>

<span data-ttu-id="08a25-111">네트워크 감시자 Agent 확장 hello Windows Server 2008 r 2에 대해 Windows를 실행할 수에 대 한 2016, R2, 2012 및 2012를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a25-111">hello Network Watcher Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span> <span data-ttu-id="08a25-112">이 이번에는 Nano Server hello는 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="08a25-112">Note that hello Nano Server is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="08a25-113">인터넷 연결</span><span class="sxs-lookup"><span data-stu-id="08a25-113">Internet connectivity</span></span>

<span data-ttu-id="08a25-114">Hello 네트워크 감시자 에이전트 기능 중 일부에서는 해당 hello 대상 가상 컴퓨터 연결된 toohello 인터넷 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a25-114">Some of hello Network Watcher Agent functionality requires that hello target virtual machine be connected toohello Internet.</span></span> <span data-ttu-id="08a25-115">Hello 기능 tooestablish 나가는 연결 되지 않은 오작동 하거나 사용할 수 없게 될 수 있습니다 hello 네트워크 감시자 에이전트 기능 중 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="08a25-115">Without hello ability tooestablish outgoing connections some of hello Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="08a25-116">자세한 내용은 hello를 참조 하십시오 [네트워크 감시자 설명서](../../network-watcher/network-watcher-monitoring-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="08a25-116">For more details, please see hello [Network Watcher documentation](../../network-watcher/network-watcher-monitoring-overview.md).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="08a25-117">확장 스키마</span><span class="sxs-lookup"><span data-stu-id="08a25-117">Extension schema</span></span>

<span data-ttu-id="08a25-118">hello 다음 JSON 스키마를 보여 줍니다 hello hello 네트워크 감시자 Agent 확장에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a25-118">hello following JSON shows hello schema for hello Network Watcher Agent extension.</span></span> <span data-ttu-id="08a25-119">hello 확장명 모두 필요 하거나 사용자가 제공한 설정을이 이번에는 지 원하는 기본 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="08a25-119">hello extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

```json
{
    "type": "extensions",
    "name": "Microsoft.Azure.NetworkWatcher",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.NetworkWatcher",
        "type": "NetworkWatcherAgentWindows",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a><span data-ttu-id="08a25-120">속성 값</span><span class="sxs-lookup"><span data-stu-id="08a25-120">Property values</span></span>

| <span data-ttu-id="08a25-121">이름</span><span class="sxs-lookup"><span data-stu-id="08a25-121">Name</span></span> | <span data-ttu-id="08a25-122">값/예제</span><span class="sxs-lookup"><span data-stu-id="08a25-122">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="08a25-123">apiVersion</span><span class="sxs-lookup"><span data-stu-id="08a25-123">apiVersion</span></span> | <span data-ttu-id="08a25-124">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="08a25-124">2015-06-15</span></span> |
| <span data-ttu-id="08a25-125">publisher</span><span class="sxs-lookup"><span data-stu-id="08a25-125">publisher</span></span> | <span data-ttu-id="08a25-126">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="08a25-126">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="08a25-127">type</span><span class="sxs-lookup"><span data-stu-id="08a25-127">type</span></span> | <span data-ttu-id="08a25-128">NetworkWatcherAgentWindows</span><span class="sxs-lookup"><span data-stu-id="08a25-128">NetworkWatcherAgentWindows</span></span> |
| <span data-ttu-id="08a25-129">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="08a25-129">typeHandlerVersion</span></span> | <span data-ttu-id="08a25-130">1.4</span><span class="sxs-lookup"><span data-stu-id="08a25-130">1.4</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="08a25-131">템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="08a25-131">Template deployment</span></span>

<span data-ttu-id="08a25-132">Azure Resource Manager 템플릿을 사용하여 Azure VM 확장을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a25-132">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="08a25-133">Azure 리소스 관리자 템플릿 배포 중에 Azure 리소스 관리자 템플릿 toorun hello 네트워크 감시자 Agent 확장 hello 이전 섹션에서 자세히 설명 하는 hello JSON 스키마를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a25-133">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="08a25-134">PowerShell 배포</span><span class="sxs-lookup"><span data-stu-id="08a25-134">PowerShell deployment</span></span>

<span data-ttu-id="08a25-135">hello `Set-AzureRmVMExtension` 명령을 사용 하는 toodeploy hello 네트워크 감시자 에이전트가 가상 컴퓨터 확장 tooan 기존 가상 컴퓨터 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a25-135">hello `Set-AzureRmVMExtension` command can be used toodeploy hello Network Watcher Agent virtual machine extension tooan existing virtual machine.</span></span>

```powershell
Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup1" `
                       -Location "WestUS" `
                       -VMName "myVM1" `
                       -Name "networkWatcherAgent" `
                       -Publisher "Microsoft.Azure.NetworkWatcher" `
                       -Type "NetworkWatcherAgentWindows" `
                       -TypeHandlerVersion "1.4"
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="08a25-136">문제 해결 및 지원</span><span class="sxs-lookup"><span data-stu-id="08a25-136">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="08a25-137">문제 해결</span><span class="sxs-lookup"><span data-stu-id="08a25-137">Troubleshooting</span></span>

<span data-ttu-id="08a25-138">Hello Azure 포털에서에서 하 고 hello Azure PowerShell 모듈을 사용 하 여 확장 배포의 hello 상태에 대 한 데이터를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a25-138">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="08a25-139">지정 된 VM 사용 하 여 명령을 다음 실행된 hello에 대 한 확장의 toosee hello 배포 상태 hello Azure PowerShell 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="08a25-139">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup1 -VMName myVM1 -Name networkWatcherAgent
```

<span data-ttu-id="08a25-140">확장 실행은 hello에 기록 된 toofiles 다음 디렉터리를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a25-140">Extension execution output is logged toofiles found in hello following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentWindows\
```

### <a name="support"></a><span data-ttu-id="08a25-141">지원</span><span class="sxs-lookup"><span data-stu-id="08a25-141">Support</span></span>

<span data-ttu-id="08a25-142">Toohello 네트워크 감시자 사용자 가이드 문서를 참조 하십시오 하거나 Azure hello 문의 수를 언제 든 지가이 문서에서 자세한 도움이 필요 하면 경우 전문가의 hello [MSDN Azure 및 스택 오버플로 포럼](https://azure.microsoft.com/en-us/support/forums/)합니다.</span><span class="sxs-lookup"><span data-stu-id="08a25-142">If you need more help at any point in this article, you can refer toohello Network Watcher User Guide documentation or contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="08a25-143">또는 Azure 기술 지원 인시던트를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a25-143">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="08a25-144">Toohello 이동 [Azure 지원 사이트](https://azure.microsoft.com/en-us/support/options/) 지원 받기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a25-144">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="08a25-145">Azure 지원을 사용 하는 방법에 대 한 내용은 하세요 hello [Microsoft Azure 지원 FAQ](https://azure.microsoft.com/en-us/support/faq/)합니다.</span><span class="sxs-lookup"><span data-stu-id="08a25-145">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
