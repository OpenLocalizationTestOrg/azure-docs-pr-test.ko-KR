---
title: "Azure Network Watcher에서 패킷 캡처 소개 | Microsoft Docs"
description: "이 페이지는 Network Watcher 패킷 캡처 기능에 대한 개요를 제공합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3a81afaa-ecd9-4004-b68e-69ab56913356
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4fdd007c2cfad7b42f26ab2cacfba06d95c8dad3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-variable-packet-capture-in-azure-network-watcher"></a><span data-ttu-id="31a1f-103">Azure Network Watcher에서 변수 패킷 캡처 소개</span><span class="sxs-lookup"><span data-stu-id="31a1f-103">Introduction to variable packet capture in Azure Network Watcher</span></span>

<span data-ttu-id="31a1f-104">Network Watcher 변수 패킷을 사용하면 가상 컴퓨터 간에 트래픽을 추적하는 패킷 캡처 세션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31a1f-104">Network Watcher variable packet capture allows you to create packet capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="31a1f-105">패킷 캡처를 통해 사후 및 사전 대응적으로 네트워크 예외를 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31a1f-105">Packet capture helps to diagnose network anomalies both reactively and proactivity.</span></span> <span data-ttu-id="31a1f-106">또한 네트워크 침입에 대한 정보를 가져오는 네트워크 통계를 수집하는 것을 포함하여 클라이언트 서버 간 통신을 디버깅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31a1f-106">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span>

<span data-ttu-id="31a1f-107">패킷 캡처는 Network Watcher를 통해 원격으로 시작되는 가상 컴퓨터 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="31a1f-107">Packet capture is a virtual machine extension that is remotely started through Network Watcher.</span></span> <span data-ttu-id="31a1f-108">이 기능은 원하는 가상 컴퓨터에서 수동으로 패킷 캡처를 실행하는 부담을 줄이고 시간을 단축합니다.</span><span class="sxs-lookup"><span data-stu-id="31a1f-108">This capability eases the burden of running a packet capture manually on the desired virtual machine, which saves valuable time.</span></span> <span data-ttu-id="31a1f-109">포털, PowerShell, CLI 또는 REST API를 통해 패킷 캡처를 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31a1f-109">Packet capture can be triggered through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="31a1f-110">패킷 캡처를 트리거하는 방식에 대한 한 가지 예는 Virtual Machine 경고를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="31a1f-110">One example of how packet capture can be triggered is with Virtual Machine alerts.</span></span> <span data-ttu-id="31a1f-111">모니터링할 트래픽을 캡처할 수 있도록 캡처 세션에 대한 필터가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="31a1f-111">Filters are provided for the capture session to ensure you capture traffic you want to monitor.</span></span> <span data-ttu-id="31a1f-112">필터는 5개 튜플(프로토콜, 로컬 IP 주소, 원격 IP 주소, 로컬 포트 및 원격 포트) 정보를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="31a1f-112">Filters are based on 5-tuple (protocol, local IP address, remote IP address, local port, and remote port) information.</span></span> <span data-ttu-id="31a1f-113">캡처된 데이터는 로컬 디스크 또는 저장소 BLOB에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="31a1f-113">The captured data is stored in the local disk or a storage blob.</span></span> <span data-ttu-id="31a1f-114">구독당 하위 지역별로 패킷 캡처 세션 수가 10개로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="31a1f-114">There is a limit of 10 packet capture sessions per region per subscription.</span></span> <span data-ttu-id="31a1f-115">이 제한은 세션에만 적용되며 VM에 로컬로 또는 저장소 계정에 저장된 패킷 캡처 파일에는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="31a1f-115">This limit applies only to the sessions and does not apply to the saved packet capture files either locally on the VM or in a storage account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31a1f-116">패킷 캡처에는 가상 컴퓨터 확장 `AzureNetworkWatcherExtension`이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="31a1f-116">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="31a1f-117">Windows VM에서 확장을 설치하려면 [Windows용 Azure Network Watcher 에이전트 가상 컴퓨터 확장](../virtual-machines/windows/extensions-nwa.md)을 방문하고 Linux VM인 경우 [Linux용 Azure Network Watcher 에이전트 가상 컴퓨터 확장](../virtual-machines/linux/extensions-nwa.md)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="31a1f-117">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

<span data-ttu-id="31a1f-118">캡처할 정보를 원하는 정보로 한정하기 위해 패킷 캡처 세션에 대해 다음 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="31a1f-118">To reduce the information you capture to only the information you want, the following options are available for a packet capture session:</span></span>

<span data-ttu-id="31a1f-119">**캡처 구성**</span><span class="sxs-lookup"><span data-stu-id="31a1f-119">**Capture configuration**</span></span>

|<span data-ttu-id="31a1f-120">속성</span><span class="sxs-lookup"><span data-stu-id="31a1f-120">Property</span></span>|<span data-ttu-id="31a1f-121">설명</span><span class="sxs-lookup"><span data-stu-id="31a1f-121">Description</span></span>|
|---|---|
|<span data-ttu-id="31a1f-122">**패킷당 최대 바이트(bytes)**</span><span class="sxs-lookup"><span data-stu-id="31a1f-122">**Maximum bytes per packet (bytes)**</span></span> | <span data-ttu-id="31a1f-123">캡처된 각 패킷의 바이트 수이며 비어 있으면 모든 바이트가 캡처됩니다.</span><span class="sxs-lookup"><span data-stu-id="31a1f-123">The number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="31a1f-124">캡처된 각 패킷의 바이트 수이며 비어 있으면 모든 바이트가 캡처됩니다.</span><span class="sxs-lookup"><span data-stu-id="31a1f-124">The number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="31a1f-125">IPv4 헤더만 필요한 경우 여기서 34를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="31a1f-125">If you need only the IPv4 header – indicate 34 here</span></span> |
|<span data-ttu-id="31a1f-126">**세션당 최대 바이트(bytes)**</span><span class="sxs-lookup"><span data-stu-id="31a1f-126">**Maximum bytes per session (bytes)**</span></span> | <span data-ttu-id="31a1f-127">값이 세션 끝에 도달할 때까지 캡처된 총 바이트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="31a1f-127">Total number of bytes in that are captured, once the value is reached the session ends.</span></span>|
|<span data-ttu-id="31a1f-128">**시간 제한(초)**</span><span class="sxs-lookup"><span data-stu-id="31a1f-128">**Time limit (seconds)**</span></span> | <span data-ttu-id="31a1f-129">패킷 캡처 세션에서 시간 제약 조건을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="31a1f-129">Sets a time constraint on the packet capture session.</span></span> <span data-ttu-id="31a1f-130">기본값은 18000초 또는 5시간입니다.</span><span class="sxs-lookup"><span data-stu-id="31a1f-130">The default value is 18000 seconds or 5 hours.</span></span>|

<span data-ttu-id="31a1f-131">**필터링(선택 사항)**</span><span class="sxs-lookup"><span data-stu-id="31a1f-131">**Filtering (optional)**</span></span>

|<span data-ttu-id="31a1f-132">속성</span><span class="sxs-lookup"><span data-stu-id="31a1f-132">Property</span></span>|<span data-ttu-id="31a1f-133">설명</span><span class="sxs-lookup"><span data-stu-id="31a1f-133">Description</span></span>|
|---|---|
|<span data-ttu-id="31a1f-134">**프로토콜**</span><span class="sxs-lookup"><span data-stu-id="31a1f-134">**Protocol**</span></span> | <span data-ttu-id="31a1f-135">패킷 캡처에 대해 필터링할 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="31a1f-135">The protocol to filter for the packet capture.</span></span> <span data-ttu-id="31a1f-136">사용 가능한 값은 TCP, UDP 및 모두입니다.</span><span class="sxs-lookup"><span data-stu-id="31a1f-136">The available values are TCP, UDP, and All.</span></span>|
|<span data-ttu-id="31a1f-137">**로컬 IP 주소**</span><span class="sxs-lookup"><span data-stu-id="31a1f-137">**Local IP address**</span></span> | <span data-ttu-id="31a1f-138">이 값은 패킷 캡처를 로컬 IP 주소가 이 필터 값과 일치하는 패킷으로 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="31a1f-138">This value filters the packet capture to packets where the local IP address matches this filter value.</span></span>|
|<span data-ttu-id="31a1f-139">**로컬 포트**</span><span class="sxs-lookup"><span data-stu-id="31a1f-139">**Local port**</span></span> | <span data-ttu-id="31a1f-140">이 값은 패킷 캡처를 로컬 포트가 이 필터 값과 일치하는 패킷으로 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="31a1f-140">This value filters the packet capture to packets where the local port matches this filter value.</span></span>|
|<span data-ttu-id="31a1f-141">**원격 IP 주소**</span><span class="sxs-lookup"><span data-stu-id="31a1f-141">**Remote IP address**</span></span> | <span data-ttu-id="31a1f-142">이 값은 패킷 캡처를 원격 IP가 이 필터 값과 일치하는 패킷으로 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="31a1f-142">This value filters the packet capture to packets where the remote IP matches this filter value.</span></span>|
|<span data-ttu-id="31a1f-143">**원격 포트**</span><span class="sxs-lookup"><span data-stu-id="31a1f-143">**Remote port**</span></span> | <span data-ttu-id="31a1f-144">이 값은 패킷 캡처를 원격 포트가 이 필터 값과 일치하는 패킷으로 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="31a1f-144">This value filters the packet capture to packets where the remote port matches this filter value.</span></span>|

### <a name="next-steps"></a><span data-ttu-id="31a1f-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="31a1f-145">Next steps</span></span>

<span data-ttu-id="31a1f-146">[Azure Portal에서 패킷 캡처 관리](network-watcher-packet-capture-manage-portal.md)를 참조하여 포털을 통해 패킷 캡처를 관리하거나 [PowerShell에서 패킷 캡처 관리](network-watcher-packet-capture-manage-powershell.md)를 참조하여 PowerShell로 패킷 캡처를 관리하는 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="31a1f-146">Learn how you can manage packet captures through the portal by visiting [Manage packet capture in the Azure portal](network-watcher-packet-capture-manage-portal.md) or with PowerShell by visiting [Manage Packet Capture with PowerShell](network-watcher-packet-capture-manage-powershell.md).</span></span>

<span data-ttu-id="31a1f-147">[경고로 트리거된 패킷 캡처 만들기](network-watcher-alert-triggered-packet-capture.md)를 확인하여 가상 컴퓨터 경고를 기반으로 사전 패킷 캡처를 만드는 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="31a1f-147">Learn how to create proactive packet captures based on virtual machine alerts by visiting [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png













