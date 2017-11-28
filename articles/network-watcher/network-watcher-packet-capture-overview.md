---
title: "Azure 네트워크 감시자에서 aaaIntroduction tooPacket 캡처 | Microsoft Docs"
description: "이 페이지 hello 네트워크 감시자 패킷 캡처 기능에 대 한 개요를 제공합니다."
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
ms.openlocfilehash: 2ce01b391b9c1a1c19aa29c8620628c55586df03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toovariable-packet-capture-in-azure-network-watcher"></a><span data-ttu-id="7df1c-103">Azure 네트워크 감시자에서 소개 toovariable 패킷 캡처</span><span class="sxs-lookup"><span data-stu-id="7df1c-103">Introduction toovariable packet capture in Azure Network Watcher</span></span>

<span data-ttu-id="7df1c-104">네트워크 감시자 변수 패킷 캡처 toocreate 패킷 캡처 세션 tootrack 트래픽 tooand를 가상 컴퓨터를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7df1c-104">Network Watcher variable packet capture allows you toocreate packet capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="7df1c-105">패킷 캡처 프로비저닝하지 toodiagnose 네트워크 비정상 모두 사용 하면 proactivity 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="7df1c-105">Packet capture helps toodiagnose network anomalies both reactively and proactivity.</span></span> <span data-ttu-id="7df1c-106">통신 및 더 많은 네트워크 침입, toodebug 클라이언트-서버에 대 한 정보를 확보 하는 네트워크 통계를 수집 하는 것이 다른 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7df1c-106">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span>

<span data-ttu-id="7df1c-107">패킷 캡처는 Network Watcher를 통해 원격으로 시작되는 가상 컴퓨터 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="7df1c-107">Packet capture is a virtual machine extension that is remotely started through Network Watcher.</span></span> <span data-ttu-id="7df1c-108">이 기능은 중요 한 시간을 절약할 hello 필요한 가상 컴퓨터에서 패킷 캡처를 수동으로 실행의 hello 부담을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7df1c-108">This capability eases hello burden of running a packet capture manually on hello desired virtual machine, which saves valuable time.</span></span> <span data-ttu-id="7df1c-109">Hello 포털, PowerShell, CLI 또는 REST API를 통해 패킷 캡처를 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7df1c-109">Packet capture can be triggered through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="7df1c-110">패킷 캡처를 트리거하는 방식에 대한 한 가지 예는 Virtual Machine 경고를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7df1c-110">One example of how packet capture can be triggered is with Virtual Machine alerts.</span></span> <span data-ttu-id="7df1c-111">필터는 hello 캡처 세션 tooensure toomonitor 원하는 트래픽을 관한 제공.</span><span class="sxs-lookup"><span data-stu-id="7df1c-111">Filters are provided for hello capture session tooensure you capture traffic you want toomonitor.</span></span> <span data-ttu-id="7df1c-112">필터는 5개 튜플(프로토콜, 로컬 IP 주소, 원격 IP 주소, 로컬 포트 및 원격 포트) 정보를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7df1c-112">Filters are based on 5-tuple (protocol, local IP address, remote IP address, local port, and remote port) information.</span></span> <span data-ttu-id="7df1c-113">hello 캡처된 데이터는 hello 로컬 디스크 또는 저장소 blob에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7df1c-113">hello captured data is stored in hello local disk or a storage blob.</span></span> <span data-ttu-id="7df1c-114">구독당 하위 지역별로 패킷 캡처 세션 수가 10개로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="7df1c-114">There is a limit of 10 packet capture sessions per region per subscription.</span></span> <span data-ttu-id="7df1c-115">이 한도 toohello 세션만 적용 하 고 hello VM에서 로컬로 또는 저장소 계정에서 패킷 캡처 파일을 저장 하는 toohello 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7df1c-115">This limit applies only toohello sessions and does not apply toohello saved packet capture files either locally on hello VM or in a storage account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7df1c-116">패킷 캡처에는 가상 컴퓨터 확장 `AzureNetworkWatcherExtension`이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7df1c-116">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="7df1c-117">Windows VM에서 hello 확장을 설치 하는 것에 대 한 방문 [Windows에 대 한 네트워크 감시자 에이전트가 Azure 가상 컴퓨터 확장](../virtual-machines/windows/extensions-nwa.md) 및 방문을 Linux VM에 대 한 [Linux용Azure네트워크감시자에이전트가가상컴퓨터확장](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="7df1c-117">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

<span data-ttu-id="7df1c-118">다음 옵션 hello 패킷 캡처 세션에 사용할 수 있는 원하는 tooonly hello 정보를 캡처하는 tooreduce hello 정보:</span><span class="sxs-lookup"><span data-stu-id="7df1c-118">tooreduce hello information you capture tooonly hello information you want, hello following options are available for a packet capture session:</span></span>

<span data-ttu-id="7df1c-119">**캡처 구성**</span><span class="sxs-lookup"><span data-stu-id="7df1c-119">**Capture configuration**</span></span>

|<span data-ttu-id="7df1c-120">속성</span><span class="sxs-lookup"><span data-stu-id="7df1c-120">Property</span></span>|<span data-ttu-id="7df1c-121">설명</span><span class="sxs-lookup"><span data-stu-id="7df1c-121">Description</span></span>|
|---|---|
|<span data-ttu-id="7df1c-122">**패킷당 최대 바이트(bytes)**</span><span class="sxs-lookup"><span data-stu-id="7df1c-122">**Maximum bytes per packet (bytes)**</span></span> | <span data-ttu-id="7df1c-123">번호 hello 바이트를 모두 비워 두면 캡처되는 각 패킷의 바이트 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="7df1c-123">hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="7df1c-124">번호 hello 바이트를 모두 비워 두면 캡처되는 각 패킷의 바이트 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="7df1c-124">hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="7df1c-125">유일한 hello IPv4 헤더 – 필요한 경우 여기 34를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7df1c-125">If you need only hello IPv4 header – indicate 34 here</span></span> |
|<span data-ttu-id="7df1c-126">**세션당 최대 바이트(bytes)**</span><span class="sxs-lookup"><span data-stu-id="7df1c-126">**Maximum bytes per session (bytes)**</span></span> | <span data-ttu-id="7df1c-127">Hello 값 hello 세션 끝에 도달 하는 바이트의 총이 캡처됩니다.</span><span class="sxs-lookup"><span data-stu-id="7df1c-127">Total number of bytes in that are captured, once hello value is reached hello session ends.</span></span>|
|<span data-ttu-id="7df1c-128">**시간 제한(초)**</span><span class="sxs-lookup"><span data-stu-id="7df1c-128">**Time limit (seconds)**</span></span> | <span data-ttu-id="7df1c-129">집합 hello 패킷에 대 한 시간 제약 세션을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="7df1c-129">Sets a time constraint on hello packet capture session.</span></span> <span data-ttu-id="7df1c-130">hello 기본값은 18000 초 또는 5 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="7df1c-130">hello default value is 18000 seconds or 5 hours.</span></span>|

<span data-ttu-id="7df1c-131">**필터링(선택 사항)**</span><span class="sxs-lookup"><span data-stu-id="7df1c-131">**Filtering (optional)**</span></span>

|<span data-ttu-id="7df1c-132">속성</span><span class="sxs-lookup"><span data-stu-id="7df1c-132">Property</span></span>|<span data-ttu-id="7df1c-133">설명</span><span class="sxs-lookup"><span data-stu-id="7df1c-133">Description</span></span>|
|---|---|
|<span data-ttu-id="7df1c-134">**프로토콜**</span><span class="sxs-lookup"><span data-stu-id="7df1c-134">**Protocol**</span></span> | <span data-ttu-id="7df1c-135">hello 패킷에 대 한 프로토콜 toofilter hello를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="7df1c-135">hello protocol toofilter for hello packet capture.</span></span> <span data-ttu-id="7df1c-136">hello 사용 가능한 값에는 TCP, UDP 및 모든은 합니다.</span><span class="sxs-lookup"><span data-stu-id="7df1c-136">hello available values are TCP, UDP, and All.</span></span>|
|<span data-ttu-id="7df1c-137">**로컬 IP 주소**</span><span class="sxs-lookup"><span data-stu-id="7df1c-137">**Local IP address**</span></span> | <span data-ttu-id="7df1c-138">이 값이 필터 값 hello 로컬 IP 주소와 일치 하는 hello 패킷 캡처 toopackets를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="7df1c-138">This value filters hello packet capture toopackets where hello local IP address matches this filter value.</span></span>|
|<span data-ttu-id="7df1c-139">**로컬 포트**</span><span class="sxs-lookup"><span data-stu-id="7df1c-139">**Local port**</span></span> | <span data-ttu-id="7df1c-140">이 값 필터 hello 패킷 캡처 toopackets hello 로컬 포트가이 필터 값과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7df1c-140">This value filters hello packet capture toopackets where hello local port matches this filter value.</span></span>|
|<span data-ttu-id="7df1c-141">**원격 IP 주소**</span><span class="sxs-lookup"><span data-stu-id="7df1c-141">**Remote IP address**</span></span> | <span data-ttu-id="7df1c-142">이 값 필터 hello 패킷 캡처 toopackets hello 원격 IP가이 필터 값과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7df1c-142">This value filters hello packet capture toopackets where hello remote IP matches this filter value.</span></span>|
|<span data-ttu-id="7df1c-143">**원격 포트**</span><span class="sxs-lookup"><span data-stu-id="7df1c-143">**Remote port**</span></span> | <span data-ttu-id="7df1c-144">이 값 필터 hello 패킷 캡처 toopackets hello 원격 포트가이 필터 값과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7df1c-144">This value filters hello packet capture toopackets where hello remote port matches this filter value.</span></span>|

### <a name="next-steps"></a><span data-ttu-id="7df1c-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7df1c-145">Next steps</span></span>

<span data-ttu-id="7df1c-146">방문 하 여 hello 포털을 통해 패킷 캡처를 관리 하는 방법에 대해 알아봅니다 [hello Azure 포털에에서 대 한 패킷 캡처를 관리](network-watcher-packet-capture-manage-portal.md) 또는 방문 하 여 PowerShell [PowerShell과 함께 패킷 캡처를 관리](network-watcher-packet-capture-manage-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7df1c-146">Learn how you can manage packet captures through hello portal by visiting [Manage packet capture in hello Azure portal](network-watcher-packet-capture-manage-portal.md) or with PowerShell by visiting [Manage Packet Capture with PowerShell](network-watcher-packet-capture-manage-powershell.md).</span></span>

<span data-ttu-id="7df1c-147">방문 하 여 가상 컴퓨터 경고를 기반으로 toocreate 사전 패킷 캡처 방법을 알아보려면 [경고 트리거된 패킷 캡처를 만들려면](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="7df1c-147">Learn how toocreate proactive packet captures based on virtual machine alerts by visiting [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png













