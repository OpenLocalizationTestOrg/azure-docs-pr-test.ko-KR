---
title: "Azure 네트워크 감시자에서 aaaIntroduction tootopology | Microsoft Docs"
description: "이 페이지 hello 네트워크 감시자 토폴로지의 기능에 대 한 개요를 제공합니다."
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
ms.openlocfilehash: 7fa1c5518e4a25a5db999d898a9ee19fd0121db7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tootopology-in-azure-network-watcher"></a><span data-ttu-id="7f2b6-103">Azure 네트워크 감시자에서 tootopology 소개</span><span class="sxs-lookup"><span data-stu-id="7f2b6-103">Introduction tootopology in Azure Network Watcher</span></span>

<span data-ttu-id="7f2b6-104">토폴로지는 가상 네트워크에서 네트워크 리소스의 그래프를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7f2b6-104">Topology returns a graph of network resources in a virtual network.</span></span> <span data-ttu-id="7f2b6-105">hello 그래프에는 hello 리소스 toorepresent hello 끝 tooend 네트워크 연결 사이의 hello를 상호 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f2b6-105">hello graph depicts hello interconnection between hello resources toorepresent hello end tooend network connectivity.</span></span>

![토폴로지 개요][1]

<span data-ttu-id="7f2b6-107">Hello 포털 토폴로지 hello 리소스 개체에 대 한 반환을 가상 네트워크로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f2b6-107">In hello portal, Topology returns hello resource objects on a per virtual network basis.</span></span> <span data-ttu-id="7f2b6-108">hello 관계에서 hello 리소스 그룹은 표시 되지 않더라도 hello 네트워크 감시자 영역 외부의 리소스 hello 리소스 간의 선으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f2b6-108">hello relationships are depicted by lines between hello resources Resources outside of hello Network Watcher region, even if in hello resource group will not be displayed.</span></span> <span data-ttu-id="7f2b6-109">hello hello 포털 뷰에서 반환 된 리소스가 그래프로 표현 하는 hello 네트워킹 구성의 하위 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="7f2b6-109">hello resources returned in hello portal view are a subset of hello networking components that are graphed.</span></span> <span data-ttu-id="7f2b6-110">사용할 수 있는 네트워킹 리소스의 toosee hello 전체 목록 [PowerShell](network-watcher-topology-powershell.md) 또는 [REST](network-watcher-topology-rest.md)</span><span class="sxs-lookup"><span data-stu-id="7f2b6-110">toosee hello full list of networking resources you can use [PowerShell](network-watcher-topology-powershell.md) or [REST](network-watcher-topology-rest.md)</span></span>

> [!NOTE]
> <span data-ttu-id="7f2b6-111">네트워크 감시자의 인스턴스 toorun 토폴로지에서 원하는 각 지역에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f2b6-111">An instance of Network Watcher is required in each region that you want toorun Topology on.</span></span>

<span data-ttu-id="7f2b6-112">리소스가 서로 hello 연결 반환 되 면 두 개의 관계에서 모델링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f2b6-112">As resources are returned hello connection between them are modeled under two relationships.</span></span>

- <span data-ttu-id="7f2b6-113">**포함** - 예: Virtual Network는 NIC를 포함하는 서브넷을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7f2b6-113">**Containment** - Example: Virtual Network contains a Subnet which contains a NIC</span></span>
- <span data-ttu-id="7f2b6-114">**연결됨** -예제: NIC는 VM과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f2b6-114">**Associated** - Example: A NIC is associated with a VM</span></span>

### <a name="next-steps"></a><span data-ttu-id="7f2b6-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7f2b6-115">Next steps</span></span>

<span data-ttu-id="7f2b6-116">Toouse PowerShell tooretrieve hello 토폴로지를 방문 하 여 보는 방법에 대해 알아봅니다 [powershell 네트워크 감시자 토폴로지](network-watcher-topology-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="7f2b6-116">Learn how toouse PowerShell tooretrieve hello Topology view by visiting [Network Watcher topology with PowerShell](network-watcher-topology-powershell.md)</span></span>

<!--Image references-->

[1]: ./media/network-watcher-topology-overview/topology.png
