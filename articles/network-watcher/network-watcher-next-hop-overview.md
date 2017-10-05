---
title: "Azure Network Watcher에서 다음 홉 소개 | Microsoft Docs"
description: "이 페이지는 Network Watcher 다음 홉 기능에 대한 개요를 제공합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: febf7bca-e0b7-41d5-838f-a5a40ebc5aac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5dd65d2418cae206965a13013dd990b916ad0733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-next-hop-in-azure-network-watcher"></a><span data-ttu-id="341ba-103">Azure Network Watcher에서 다음 홉 소개</span><span class="sxs-lookup"><span data-stu-id="341ba-103">Introduction to next hop in Azure Network Watcher</span></span>

<span data-ttu-id="341ba-104">VM의 트래픽은 NIC와 연결된 유효 경로에 따라 대상에 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="341ba-104">Traffic from a VM is sent to a destination based on the effective routes associated with a NIC.</span></span> <span data-ttu-id="341ba-105">다음 홉은 특정 가상 컴퓨터 및 NIC에서 다음 홉 유형 및 패킷의 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="341ba-105">Next hop gets the next hop type and IP address of a packet from a specific virtual machine and NIC.</span></span> <span data-ttu-id="341ba-106">이를 통해 패킷이 대상으로 연결되거나 블랙홀이 되는 트래픽인 경우를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="341ba-106">This helps to determine if the packet is being directed to the destination or is the traffic being black holed.</span></span> <span data-ttu-id="341ba-107">사용자에 의한 부적절한 경로의 구성으로 연결 문제가 발생할 수 있습니다. 여기서 트래픽은 온-프레미스 위치 또는 가상 어플라이언스로 향합니다.</span><span class="sxs-lookup"><span data-stu-id="341ba-107">An improper configuration of routes by the user, where a traffic is directed to an on-premises location or a virtual appliance, can lead to connectivity issues.</span></span> <span data-ttu-id="341ba-108">또한 다음 홉은 다음 홉과 연결된 경로 테이블을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="341ba-108">Next hop also returns the route table associated with the next hop.</span></span> <span data-ttu-id="341ba-109">다음 홉을 쿼리할 때 경로가 사용자 정의 경로로 정의된 경우 해당 경로가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="341ba-109">When querying a next hop if the route is defined as a user-defined route, that route will be returned.</span></span> <span data-ttu-id="341ba-110">그렇지 않은 경우 다음 홉은 "시스템 경로"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="341ba-110">Otherwise Next hop returns "System Route".</span></span>

![다음 홉 개요][1]

<span data-ttu-id="341ba-112">다음은 다음 홉을 쿼리할 때 반환될 수 있는 다음 홉 형식의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="341ba-112">The following is a list of the next hop types that can be returned when querying Next hop.</span></span>

* <span data-ttu-id="341ba-113">인터넷</span><span class="sxs-lookup"><span data-stu-id="341ba-113">Internet</span></span>
* <span data-ttu-id="341ba-114">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="341ba-114">VirtualAppliance</span></span>
* <span data-ttu-id="341ba-115">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="341ba-115">VirtualNetworkGateway</span></span>
* <span data-ttu-id="341ba-116">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="341ba-116">VnetLocal</span></span>
* <span data-ttu-id="341ba-117">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="341ba-117">HyperNetGateway</span></span>
* <span data-ttu-id="341ba-118">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="341ba-118">VnetPeering</span></span>
* <span data-ttu-id="341ba-119">없음</span><span class="sxs-lookup"><span data-stu-id="341ba-119">None</span></span>

### <a name="next-steps"></a><span data-ttu-id="341ba-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="341ba-120">Next steps</span></span>

<span data-ttu-id="341ba-121">[VM에서 다음 홉 확인](network-watcher-check-next-hop-portal.md)을 방문하여 다음 홉을 사용하여 네트워크 연결 문제를 찾는 방법에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="341ba-121">Learn how to use next hop to find issues with network connectivity by visiting [Check the next hop on a VM](network-watcher-check-next-hop-portal.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













