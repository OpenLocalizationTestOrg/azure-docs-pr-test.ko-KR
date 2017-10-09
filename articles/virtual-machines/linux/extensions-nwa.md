---
title: "Linux 용 네트워크 감시자 에이전트가 가상 컴퓨터 확장 aaaAzure | Microsoft Docs"
description: "가상 컴퓨터 확장을 사용 하 여 Linux 가상 컴퓨터에서 네트워크 감시자 에이전트 hello를 배포 합니다."
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
ms.openlocfilehash: 84bed132cbda83d0917be490f9a50914578952a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a><span data-ttu-id="6af71-103">Linux용 Network Watcher 에이전트 가상 컴퓨터 확장</span><span class="sxs-lookup"><span data-stu-id="6af71-103">Network Watcher Agent virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="6af71-104">개요</span><span class="sxs-lookup"><span data-stu-id="6af71-104">Overview</span></span>

<span data-ttu-id="6af71-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/)는 Azure 네트워크에 대한 모니터링을 허용하는 네트워크 성능 모니터링, 진단 및 분석 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="6af71-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="6af71-106">네트워크 감시자 에이전트가 가상 컴퓨터 확장 hello hello Azure 가상 컴퓨터 네트워크 감시자 기능 중 일부에 대 한 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="6af71-106">hello Network Watcher Agent virtual machine extension is a requirement for some of hello Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="6af71-107">주문형 네트워크 트래픽을 캡처하는 기능 및 기타 고급 기능이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6af71-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="6af71-108">이 문서 정보 hello Linux 용 hello 네트워크 감시자 에이전트가 가상 컴퓨터 확장에 대 한 플랫폼 및 배포 옵션을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="6af71-108">This document details hello supported platforms and deployment options for hello Network Watcher Agent virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6af71-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6af71-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="6af71-110">운영 체제</span><span class="sxs-lookup"><span data-stu-id="6af71-110">Operating system</span></span>

<span data-ttu-id="6af71-111">네트워크 감시자 에이전트 확장 hello 이러한 Linux 배포에 대해 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6af71-111">hello Network Watcher Agent extension can be run against these Linux distributions:</span></span>

| <span data-ttu-id="6af71-112">배포</span><span class="sxs-lookup"><span data-stu-id="6af71-112">Distribution</span></span> | <span data-ttu-id="6af71-113">버전</span><span class="sxs-lookup"><span data-stu-id="6af71-113">Version</span></span> |
|---|---|
| <span data-ttu-id="6af71-114">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="6af71-114">Ubuntu</span></span> | <span data-ttu-id="6af71-115">16.04 LTS, 14.04 LTS 및 12.04 LTS</span><span class="sxs-lookup"><span data-stu-id="6af71-115">16.04 LTS, 14.04 LTS and 12.04 LTS</span></span> |
| <span data-ttu-id="6af71-116">Debian</span><span class="sxs-lookup"><span data-stu-id="6af71-116">Debian</span></span> | <span data-ttu-id="6af71-117">7 및 8</span><span class="sxs-lookup"><span data-stu-id="6af71-117">7 and 8</span></span> |
| <span data-ttu-id="6af71-118">RedHat</span><span class="sxs-lookup"><span data-stu-id="6af71-118">RedHat</span></span> | <span data-ttu-id="6af71-119">6.x 및 7.x</span><span class="sxs-lookup"><span data-stu-id="6af71-119">6.x and 7.x</span></span> |
| <span data-ttu-id="6af71-120">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="6af71-120">Oracle Linux</span></span> | <span data-ttu-id="6af71-121">7x</span><span class="sxs-lookup"><span data-stu-id="6af71-121">7x</span></span> |
| <span data-ttu-id="6af71-122">Suse</span><span class="sxs-lookup"><span data-stu-id="6af71-122">Suse</span></span> | <span data-ttu-id="6af71-123">11 및 12</span><span class="sxs-lookup"><span data-stu-id="6af71-123">11 and 12</span></span> |
| <span data-ttu-id="6af71-124">OpenSuse</span><span class="sxs-lookup"><span data-stu-id="6af71-124">OpenSuse</span></span> | <span data-ttu-id="6af71-125">7.0</span><span class="sxs-lookup"><span data-stu-id="6af71-125">7.0</span></span> |
| <span data-ttu-id="6af71-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="6af71-126">CentOS</span></span> | <span data-ttu-id="6af71-127">7.0</span><span class="sxs-lookup"><span data-stu-id="6af71-127">7.0</span></span> |

<span data-ttu-id="6af71-128">CoreOS는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6af71-128">Note that CoreOS is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="6af71-129">인터넷 연결</span><span class="sxs-lookup"><span data-stu-id="6af71-129">Internet connectivity</span></span>

<span data-ttu-id="6af71-130">Hello 네트워크 감시자 에이전트 기능 중 일부에서는 해당 hello 대상 가상 컴퓨터 연결된 toohello 인터넷 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6af71-130">Some of hello Network Watcher Agent functionality requires that hello target virtual machine be connected toohello Internet.</span></span> <span data-ttu-id="6af71-131">Hello 기능 tooestablish 나가는 연결 되지 않은 오작동 하거나 사용할 수 없게 될 수 있습니다 hello 네트워크 감시자 에이전트 기능 중 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="6af71-131">Without hello ability tooestablish outgoing connections some of hello Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="6af71-132">자세한 내용은 hello를 참조 하십시오 [네트워크 감시자 설명서](https://review.docs.microsoft.com/en-us/azure/network-watcher/)합니다.</span><span class="sxs-lookup"><span data-stu-id="6af71-132">For more details, please see hello [Network Watcher documentation](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="6af71-133">확장 스키마</span><span class="sxs-lookup"><span data-stu-id="6af71-133">Extension schema</span></span>

<span data-ttu-id="6af71-134">hello 다음 JSON 스키마를 보여 줍니다 hello hello 네트워크 감시자 Agent 확장에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6af71-134">hello following JSON shows hello schema for hello Network Watcher Agent extension.</span></span> <span data-ttu-id="6af71-135">hello 확장명 모두 필요 하거나 사용자가 제공한 설정을이 이번에는 지 원하는 기본 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="6af71-135">hello extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

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

### <a name="property-values"></a><span data-ttu-id="6af71-136">속성 값</span><span class="sxs-lookup"><span data-stu-id="6af71-136">Property values</span></span>

| <span data-ttu-id="6af71-137">이름</span><span class="sxs-lookup"><span data-stu-id="6af71-137">Name</span></span> | <span data-ttu-id="6af71-138">값/예제</span><span class="sxs-lookup"><span data-stu-id="6af71-138">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="6af71-139">apiVersion</span><span class="sxs-lookup"><span data-stu-id="6af71-139">apiVersion</span></span> | <span data-ttu-id="6af71-140">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="6af71-140">2015-06-15</span></span> |
| <span data-ttu-id="6af71-141">publisher</span><span class="sxs-lookup"><span data-stu-id="6af71-141">publisher</span></span> | <span data-ttu-id="6af71-142">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="6af71-142">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="6af71-143">type</span><span class="sxs-lookup"><span data-stu-id="6af71-143">type</span></span> | <span data-ttu-id="6af71-144">NetworkWatcherAgentLinux</span><span class="sxs-lookup"><span data-stu-id="6af71-144">NetworkWatcherAgentLinux</span></span> |
| <span data-ttu-id="6af71-145">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="6af71-145">typeHandlerVersion</span></span> | <span data-ttu-id="6af71-146">1.4</span><span class="sxs-lookup"><span data-stu-id="6af71-146">1.4</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="6af71-147">템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="6af71-147">Template deployment</span></span>

<span data-ttu-id="6af71-148">Azure Resource Manager 템플릿을 사용하여 Azure VM 확장을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6af71-148">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="6af71-149">Azure 리소스 관리자 템플릿 배포 중에 Azure 리소스 관리자 템플릿 toorun hello 네트워크 감시자 Agent 확장 hello 이전 섹션에서 자세히 설명 하는 hello JSON 스키마를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6af71-149">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="azure-cli-deployment"></a><span data-ttu-id="6af71-150">Azure CLI 배포</span><span class="sxs-lookup"><span data-stu-id="6af71-150">Azure CLI deployment</span></span>

<span data-ttu-id="6af71-151">hello Azure CLI 사용된 toodeploy hello 네트워크 감시자의 에이전트 VM 확장 tooan 기존 가상 컴퓨터를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6af71-151">hello Azure CLI can be used toodeploy hello Network Watcher Agent VM extension tooan existing virtual machine.</span></span>

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="6af71-152">문제 해결 및 지원</span><span class="sxs-lookup"><span data-stu-id="6af71-152">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="6af71-153">문제 해결</span><span class="sxs-lookup"><span data-stu-id="6af71-153">Troubleshooting</span></span>

<span data-ttu-id="6af71-154">Hello Azure 포털에서에서 하 고 hello Azure CLI를 사용 하 여 확장 배포의 hello 상태에 대 한 데이터를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6af71-154">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure CLI.</span></span> <span data-ttu-id="6af71-155">hello 명령을 사용 하 여 다음을 실행 하는 특정된 VM에 대 한 확장의 toosee hello 배포 상태 hello Azure CLI 합니다.</span><span class="sxs-lookup"><span data-stu-id="6af71-155">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure CLI.</span></span>

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

<span data-ttu-id="6af71-156">확장 실행은 hello에 기록 된 toofiles 다음 디렉터리를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6af71-156">Extension execution output is logged toofiles found in hello following directory:</span></span>

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a><span data-ttu-id="6af71-157">지원</span><span class="sxs-lookup"><span data-stu-id="6af71-157">Support</span></span>

<span data-ttu-id="6af71-158">Toohello 네트워크 감시자 설명서를 참조 하거나 Azure hello에 게 문의 수를 언제 든 지가이 문서에서 자세한 도움이 필요 하면 경우 전문가의 hello [MSDN Azure 및 스택 오버플로 포럼](https://azure.microsoft.com/en-us/support/forums/)합니다.</span><span class="sxs-lookup"><span data-stu-id="6af71-158">If you need more help at any point in this article, you can refer toohello Network Watcher documentation or contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="6af71-159">또는 Azure 기술 지원 인시던트를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6af71-159">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="6af71-160">Toohello 이동 [Azure 지원 사이트](https://azure.microsoft.com/en-us/support/options/) 지원 받기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6af71-160">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="6af71-161">Azure 지원을 사용 하는 방법에 대 한 내용은 하세요 hello [Microsoft Azure 지원 FAQ](https://azure.microsoft.com/en-us/support/faq/)합니다.</span><span class="sxs-lookup"><span data-stu-id="6af71-161">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
