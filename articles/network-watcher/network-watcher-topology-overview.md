---
title: "Azure Network Watcher에서 토폴로지 소개 | Microsoft Docs"
description: "이 페이지는 Network Watcher 토폴로지 기능에 대한 개요를 제공합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e753a435-38e0-482b-846b-121cb547555c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 42443f614b76b8180ac163b9889163021adbf048
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-topology-in-azure-network-watcher"></a><span data-ttu-id="24194-103">Azure Network Watcher에서 토폴로지 소개</span><span class="sxs-lookup"><span data-stu-id="24194-103">Introduction to topology in Azure Network Watcher</span></span>

<span data-ttu-id="24194-104">토폴로지는 가상 네트워크에서 네트워크 리소스의 그래프를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="24194-104">Topology returns a graph of network resources in a virtual network.</span></span> <span data-ttu-id="24194-105">이 그래프는 리소스 간 상호 연결을 보여 주고 종단 간 네트워크 연결을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="24194-105">The graph depicts the interconnection between the resources to represent the end to end network connectivity.</span></span>

![토폴로지 개요][1]

<span data-ttu-id="24194-107">포털에서 토폴로지는 가상 네트워크를 기반으로 리소스 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="24194-107">In the portal, Topology returns the resource objects on a per virtual network basis.</span></span> <span data-ttu-id="24194-108">관계는 Network Watcher 지역 외부에 있는 리소스로 리소스 그룹에 표시되지 않더라도 리소스 간에 선으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="24194-108">The relationships are depicted by lines between the resources Resources outside of the Network Watcher region, even if in the resource group will not be displayed.</span></span> <span data-ttu-id="24194-109">포털 보기에서 반환된 리소스는 그래프 표시된 네트워킹 구성 요소의 하위 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="24194-109">The resources returned in the portal view are a subset of the networking components that are graphed.</span></span> <span data-ttu-id="24194-110">전체 네트워킹 리소스 목록을 보려면 [PowerShell](network-watcher-topology-powershell.md) 또는 [REST](network-watcher-topology-rest.md)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24194-110">To see the full list of networking resources you can use [PowerShell](network-watcher-topology-powershell.md) or [REST](network-watcher-topology-rest.md)</span></span>

> [!NOTE]
> <span data-ttu-id="24194-111">토폴로지를 실행할 각 지역에 Network Watcher의 인스턴스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="24194-111">An instance of Network Watcher is required in each region that you want to run Topology on.</span></span>

<span data-ttu-id="24194-112">리소스가 반환되면 리소스 간 연결은 두 관계로 모델링됩니다.</span><span class="sxs-lookup"><span data-stu-id="24194-112">As resources are returned the connection between them are modeled under two relationships.</span></span>

- <span data-ttu-id="24194-113">**포함** - 예: Virtual Network는 NIC를 포함하는 서브넷을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="24194-113">**Containment** - Example: Virtual Network contains a Subnet which contains a NIC</span></span>
- <span data-ttu-id="24194-114">**연결됨** -예제: NIC는 VM과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="24194-114">**Associated** - Example: A NIC is associated with a VM</span></span>

### <a name="next-steps"></a><span data-ttu-id="24194-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="24194-115">Next steps</span></span>

<span data-ttu-id="24194-116">[PowerShell에서 Network Watcher 토폴로지](network-watcher-topology-powershell.md)에서 PowerShell을 사용하여 토폴로지 보기를 검색하는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="24194-116">Learn how to use PowerShell to retrieve the Topology view by visiting [Network Watcher topology with PowerShell](network-watcher-topology-powershell.md)</span></span>

<!--Image references-->

[1]: ./media/network-watcher-topology-overview/topology.png
