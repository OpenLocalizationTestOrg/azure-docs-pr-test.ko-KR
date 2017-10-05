---
title: "Linux용 Azure Network Watcher 에이전트 가상 컴퓨터 확장 | Microsoft Docs"
description: "가상 컴퓨터 확장을 사용하여 Linux 가상 컴퓨터에 Network Watcher를 배포합니다."
services: virtual-machines-linux
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 5c81e94c-e127-4dd2-ae83-a236c4512345
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: eaadd531b9e05a54446e61f98584ae9d75470a5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a><span data-ttu-id="4dbf7-103">Linux용 Network Watcher 에이전트 가상 컴퓨터 확장</span><span class="sxs-lookup"><span data-stu-id="4dbf7-103">Network Watcher Agent virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="4dbf7-104">개요</span><span class="sxs-lookup"><span data-stu-id="4dbf7-104">Overview</span></span>

<span data-ttu-id="4dbf7-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/)는 Azure 네트워크에 대한 모니터링을 허용하는 네트워크 성능 모니터링, 진단 및 분석 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="4dbf7-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="4dbf7-106">Azure Virtual Machines의 Network Watcher 기능 중 일부에는 Azure Network Watcher 에이전트 가상 컴퓨터 확장이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4dbf7-106">The Network Watcher Agent virtual machine extension is a requirement for some of the Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="4dbf7-107">주문형 네트워크 트래픽을 캡처하는 기능 및 기타 고급 기능이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dbf7-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="4dbf7-108">이 문서에서는 Linux용 Network Watcher 에이전트 가상 컴퓨터 확장에 대해 지원되는 플랫폼 및 배포 옵션을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4dbf7-108">This document details the supported platforms and deployment options for the Network Watcher Agent virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4dbf7-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4dbf7-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="4dbf7-110">운영 체제</span><span class="sxs-lookup"><span data-stu-id="4dbf7-110">Operating system</span></span>

<span data-ttu-id="4dbf7-111">Network Watcher 에이전트 확장은 다음 Linux 배포판에 대해 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbf7-111">The Network Watcher Agent extension can be run against these Linux distributions:</span></span>

| <span data-ttu-id="4dbf7-112">배포</span><span class="sxs-lookup"><span data-stu-id="4dbf7-112">Distribution</span></span> | <span data-ttu-id="4dbf7-113">버전</span><span class="sxs-lookup"><span data-stu-id="4dbf7-113">Version</span></span> |
|---|---|
| <span data-ttu-id="4dbf7-114">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="4dbf7-114">Ubuntu</span></span> | <span data-ttu-id="4dbf7-115">16.04 LTS, 14.04 LTS 및 12.04 LTS</span><span class="sxs-lookup"><span data-stu-id="4dbf7-115">16.04 LTS, 14.04 LTS and 12.04 LTS</span></span> |
| <span data-ttu-id="4dbf7-116">Debian</span><span class="sxs-lookup"><span data-stu-id="4dbf7-116">Debian</span></span> | <span data-ttu-id="4dbf7-117">7 및 8</span><span class="sxs-lookup"><span data-stu-id="4dbf7-117">7 and 8</span></span> |
| <span data-ttu-id="4dbf7-118">RedHat</span><span class="sxs-lookup"><span data-stu-id="4dbf7-118">RedHat</span></span> | <span data-ttu-id="4dbf7-119">6.x 및 7.x</span><span class="sxs-lookup"><span data-stu-id="4dbf7-119">6.x and 7.x</span></span> |
| <span data-ttu-id="4dbf7-120">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="4dbf7-120">Oracle Linux</span></span> | <span data-ttu-id="4dbf7-121">7x</span><span class="sxs-lookup"><span data-stu-id="4dbf7-121">7x</span></span> |
| <span data-ttu-id="4dbf7-122">Suse</span><span class="sxs-lookup"><span data-stu-id="4dbf7-122">Suse</span></span> | <span data-ttu-id="4dbf7-123">11 및 12</span><span class="sxs-lookup"><span data-stu-id="4dbf7-123">11 and 12</span></span> |
| <span data-ttu-id="4dbf7-124">OpenSuse</span><span class="sxs-lookup"><span data-stu-id="4dbf7-124">OpenSuse</span></span> | <span data-ttu-id="4dbf7-125">7.0</span><span class="sxs-lookup"><span data-stu-id="4dbf7-125">7.0</span></span> |
| <span data-ttu-id="4dbf7-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="4dbf7-126">CentOS</span></span> | <span data-ttu-id="4dbf7-127">7.0</span><span class="sxs-lookup"><span data-stu-id="4dbf7-127">7.0</span></span> |

<span data-ttu-id="4dbf7-128">CoreOS는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbf7-128">Note that CoreOS is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="4dbf7-129">인터넷 연결</span><span class="sxs-lookup"><span data-stu-id="4dbf7-129">Internet connectivity</span></span>

<span data-ttu-id="4dbf7-130">일부 Network Watcher 에이전트 기능에서는 대상 가상 컴퓨터를 인터넷에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dbf7-130">Some of the Network Watcher Agent functionality requires that the target virtual machine be connected to the Internet.</span></span> <span data-ttu-id="4dbf7-131">일부 Network Watcher 에이전트 기능에 나가는 연결을 설정하는 기능이 없는 경우 오작동하거나 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dbf7-131">Without the ability to establish outgoing connections some of the Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="4dbf7-132">자세한 내용은 [Network Watcher 설명서](https://review.docs.microsoft.com/en-us/azure/network-watcher/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4dbf7-132">For more details, please see the [Network Watcher documentation](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="4dbf7-133">확장 스키마</span><span class="sxs-lookup"><span data-stu-id="4dbf7-133">Extension schema</span></span>

<span data-ttu-id="4dbf7-134">다음 JSON은 Network Watcher 에이전트 확장에 대한 스키마를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4dbf7-134">The following JSON shows the schema for the Network Watcher Agent extension.</span></span> <span data-ttu-id="4dbf7-135">현재 확장은 사용자 제공 설정을 필요로 하거나 지원하지 않고 기본 구성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4dbf7-135">The extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

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
        "type": "NetworkWatcherAgentLinux",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a><span data-ttu-id="4dbf7-136">속성 값</span><span class="sxs-lookup"><span data-stu-id="4dbf7-136">Property values</span></span>

| <span data-ttu-id="4dbf7-137">이름</span><span class="sxs-lookup"><span data-stu-id="4dbf7-137">Name</span></span> | <span data-ttu-id="4dbf7-138">값/예제</span><span class="sxs-lookup"><span data-stu-id="4dbf7-138">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="4dbf7-139">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4dbf7-139">apiVersion</span></span> | <span data-ttu-id="4dbf7-140">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="4dbf7-140">2015-06-15</span></span> |
| <span data-ttu-id="4dbf7-141">publisher</span><span class="sxs-lookup"><span data-stu-id="4dbf7-141">publisher</span></span> | <span data-ttu-id="4dbf7-142">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="4dbf7-142">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="4dbf7-143">type</span><span class="sxs-lookup"><span data-stu-id="4dbf7-143">type</span></span> | <span data-ttu-id="4dbf7-144">NetworkWatcherAgentLinux</span><span class="sxs-lookup"><span data-stu-id="4dbf7-144">NetworkWatcherAgentLinux</span></span> |
| <span data-ttu-id="4dbf7-145">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="4dbf7-145">typeHandlerVersion</span></span> | <span data-ttu-id="4dbf7-146">1.4</span><span class="sxs-lookup"><span data-stu-id="4dbf7-146">1.4</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="4dbf7-147">템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="4dbf7-147">Template deployment</span></span>

<span data-ttu-id="4dbf7-148">Azure Resource Manager 템플릿을 사용하여 Azure VM 확장을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbf7-148">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="4dbf7-149">이전 섹션에서 자세히 설명한 JSON 스키마를 Azure Resource Manager 템플릿에서 사용하여 Azure Resource Manager 템플릿 배포 중 Network Watcher 에이전트 확장을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbf7-149">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="azure-cli-deployment"></a><span data-ttu-id="4dbf7-150">Azure CLI 배포</span><span class="sxs-lookup"><span data-stu-id="4dbf7-150">Azure CLI deployment</span></span>

<span data-ttu-id="4dbf7-151">Azure CLI를 사용하여 Network Watcher 에이전트 VM 확장을 기존 가상 컴퓨터에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbf7-151">The Azure CLI can be used to deploy the Network Watcher Agent VM extension to an existing virtual machine.</span></span>

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="4dbf7-152">문제 해결 및 지원</span><span class="sxs-lookup"><span data-stu-id="4dbf7-152">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="4dbf7-153">문제 해결</span><span class="sxs-lookup"><span data-stu-id="4dbf7-153">Troubleshooting</span></span>

<span data-ttu-id="4dbf7-154">확장 배포 상태에 대한 데이터는 Azure CLI를 사용하여 Azure Portal에서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbf7-154">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure CLI.</span></span> <span data-ttu-id="4dbf7-155">지정된 VM에 대한 확장의 배포 상태를 보려면 Azure CLI를 사용하여 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4dbf7-155">To see the deployment state of extensions for a given VM, run the following command using the Azure CLI.</span></span>

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

<span data-ttu-id="4dbf7-156">확장 실행 출력은 다음 디렉터리에 있는 파일에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dbf7-156">Extension execution output is logged to files found in the following directory:</span></span>

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a><span data-ttu-id="4dbf7-157">지원</span><span class="sxs-lookup"><span data-stu-id="4dbf7-157">Support</span></span>

<span data-ttu-id="4dbf7-158">이 문서의 어디에서든 도움이 필요한 경우 Network Watcher 설명서를 참조하거나 [MSDN Azure 및 Stack Overflow 포럼](https://azure.microsoft.com/en-us/support/forums/)에서 Azure 전문가에게 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbf7-158">If you need more help at any point in this article, you can refer to the Network Watcher documentation or contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="4dbf7-159">또는 Azure 기술 지원 인시던트를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbf7-159">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="4dbf7-160">[Azure 지원 사이트](https://azure.microsoft.com/en-us/support/options/)로 가서 지원 받기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4dbf7-160">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="4dbf7-161">Azure 지원을 사용하는 방법에 대한 자세한 내용은 [Microsoft Azure 지원 FAQ](https://azure.microsoft.com/en-us/support/faq/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4dbf7-161">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
