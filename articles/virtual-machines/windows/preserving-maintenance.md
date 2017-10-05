---
title: "Azure에서 Windows VM에 대한 VM 보존 유지 관리 | Microsoft Docs"
description: "메모리 보존 업데이트를 위한 전체 VM 마이그레이션"
services: virtual-machines-windows
documentationcenter: 
author: zivr
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: zivr
ms.openlocfilehash: 8888bafbc3aba24168312b611a9b4fbde25f376d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="vm-preserving-maintenance-with-in-place-vm-migration"></a><span data-ttu-id="56738-103">전체 VM 마이그레이션을 사용한 VM 보존 유지 관리</span><span class="sxs-lookup"><span data-stu-id="56738-103">VM preserving maintenance with In-place VM migration</span></span>

<span data-ttu-id="56738-104">대부분이 업데이트는 호스트된 VM에 영향을 미치지 않지만 구성 요소 또는 서비스에 대한 업데이트가 실행 중인 VM에 최소한의 간섭을 유발하는 경우가 있습니다(가상 컴퓨터의 전체 다시 부팅 없음).</span><span class="sxs-lookup"><span data-stu-id="56738-104">While the majority of updates have no impact to hosted VMs, there are cases where updates to components or services result in minimal interference to running VMs (without a full reboot of the virtual machine).</span></span>

<span data-ttu-id="56738-105">이러한 업데이트는 원위치 실시간 마이그레이션을 가능하게 하는 기술(“메모리 보존 업데이트”)을 통해 완수됩니다.</span><span class="sxs-lookup"><span data-stu-id="56738-105">These updates are accomplished with technology that enables in-place live migration, also called "memory-preserving update".</span></span> <span data-ttu-id="56738-106">호스트 업데이트 시 호스팅 환경(예: 기본 운영 체제)이 필요한 업데이트 및 패치를 적용하는 동안 가상 컴퓨터는 "일시 중지" 상태로 들어가 RAM의 메모리를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="56738-106">When updating the host, the virtual machine is placed into a “paused” state, preserving the memory in RAM, while the hosting environment (e.g. the underlying operating system) applies the necessary updates and patches.</span></span>
<span data-ttu-id="56738-107">그런 후 가상 컴퓨터는 일시 중지 후 30초 내에 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="56738-107">The virtual machine is then resumed within 30 seconds of being paused.</span></span>
<span data-ttu-id="56738-108">다시 시작된 후 가상 컴퓨터의 시계가 자동으로 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="56738-108">After resuming, the clock of the virtual machine is automatically synchronized.</span></span>

<span data-ttu-id="56738-109">이 메커니즘을 사용하여 모든 업데이트를 배포할 수 있는 것은 아니지만 짧은 일시 중지 시간을 지정한 경우 이 방식으로 업데이트를 배포하면 가상 컴퓨터에 미치는 영향을 크게 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56738-109">Not all updates can be deployed by using this mechanism, but given the short pause period, deploying updates in this way greatly reduces impact to virtual machines.</span></span>

<span data-ttu-id="56738-110">다중 인스턴스 업데이트(가용성 집합의 VM)는 한 번에 하나의 업데이트 도메인에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="56738-110">Multi-instance updates (VMs in an availability set) are applied one update domain at a time.</span></span>

<span data-ttu-id="56738-111">일부 응용 프로그램은 이러한 업데이트로 인해 다른 응용 프로그램보다 더 많은 영향을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56738-111">Some applications may be impacted by these updates more than others.</span></span> <span data-ttu-id="56738-112">예를 들어 실시간 이벤트 처리, 미디어 스트리밍 또는 코드 변환, 처리량이 높은 네트워킹 시나리오를 수행하는 응용 프로그램은 30초 일시 중지를 허용할 수 있게 설계되지 않았을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56738-112">Applications that perform real-time event processing, media streaming or transcoding, or high throughput networking scenarios, for example, may not be designed to tolerate a 30 second pause.</span></span> <span data-ttu-id="56738-113">가상 컴퓨터에서 실행 중인 응용 프로그램은 [Azure 메타데이터 서비스](../virtual-machines-instancemetadataservice-overview.md)의 [예약된 이벤트](../virtual-machines-scheduled-events.md) API를 호출하여 예정된 업데이트에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56738-113">Applications running in a virtual machine can learn about upcoming updates by calling the [Scheduled Events](../virtual-machines-scheduled-events.md) API of the [Azure Metadata Service](../virtual-machines-instancemetadataservice-overview.md).</span></span>
