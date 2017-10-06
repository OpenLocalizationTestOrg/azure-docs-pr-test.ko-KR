---
title: "Azure 네트워크 감시자에서 aaaIntroduction toonext 홉 | Microsoft Docs"
description: "이 페이지에서는 다음 홉 기능 hello 네트워크 감시자의 개요를 제공"
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
ms.openlocfilehash: 916af736d0d52abadeafed746f0f8a0173b11033
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonext-hop-in-azure-network-watcher"></a><span data-ttu-id="98deb-103">Azure 네트워크 감시자에서 toonext 홉 소개</span><span class="sxs-lookup"><span data-stu-id="98deb-103">Introduction toonext hop in Azure Network Watcher</span></span>

<span data-ttu-id="98deb-104">트래픽이 VM에서 NIC와 관련 된 hello 유효 경로에 따라 tooa 대상 전송</span><span class="sxs-lookup"><span data-stu-id="98deb-104">Traffic from a VM is sent tooa destination based on hello effective routes associated with a NIC.</span></span> <span data-ttu-id="98deb-105">다음 홉에서 특정 가상 컴퓨터 및 NIC. hello 다음 홉 형식이 및 패킷의 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="98deb-105">Next hop gets hello next hop type and IP address of a packet from a specific virtual machine and NIC.</span></span> <span data-ttu-id="98deb-106">이렇게 하면 hello 패킷 되 toohello 방향이 지정 된 대상 또는 black 되 고 hello 트래픽 숨어 경우 toodetermine 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98deb-106">This helps toodetermine if hello packet is being directed toohello destination or is hello traffic being black holed.</span></span> <span data-ttu-id="98deb-107">여기서 트래픽이 방향이 지정 된 tooan 온-프레미스 위치 또는 가상 어플라이언스, hello 사용자별 경로의 됨으로써 구성이 tooconnectivity 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98deb-107">An improper configuration of routes by hello user, where a traffic is directed tooan on-premises location or a virtual appliance, can lead tooconnectivity issues.</span></span> <span data-ttu-id="98deb-108">또한 다음 홉 hello 다음 홉와 관련 된 hello 경로 테이블을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="98deb-108">Next hop also returns hello route table associated with hello next hop.</span></span> <span data-ttu-id="98deb-109">다음 홉을 hello 경로 사용자 정의 경로로 정의 된 경우 쿼리할 때 해당 경로 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98deb-109">When querying a next hop if hello route is defined as a user-defined route, that route will be returned.</span></span> <span data-ttu-id="98deb-110">그렇지 않은 경우 다음 홉은 "시스템 경로"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="98deb-110">Otherwise Next hop returns "System Route".</span></span>

![다음 홉 개요][1]

<span data-ttu-id="98deb-112">hello 다음은 목록 다음 홉을 쿼리할 때 반환 될 수 있는 hello 다음 홉 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="98deb-112">hello following is a list of hello next hop types that can be returned when querying Next hop.</span></span>

* <span data-ttu-id="98deb-113">인터넷</span><span class="sxs-lookup"><span data-stu-id="98deb-113">Internet</span></span>
* <span data-ttu-id="98deb-114">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="98deb-114">VirtualAppliance</span></span>
* <span data-ttu-id="98deb-115">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="98deb-115">VirtualNetworkGateway</span></span>
* <span data-ttu-id="98deb-116">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="98deb-116">VnetLocal</span></span>
* <span data-ttu-id="98deb-117">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="98deb-117">HyperNetGateway</span></span>
* <span data-ttu-id="98deb-118">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="98deb-118">VnetPeering</span></span>
* <span data-ttu-id="98deb-119">없음</span><span class="sxs-lookup"><span data-stu-id="98deb-119">None</span></span>

### <a name="next-steps"></a><span data-ttu-id="98deb-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="98deb-120">Next steps</span></span>

<span data-ttu-id="98deb-121">다음 홉 toofind toouse 네트워크 연결에 방문 하 여 발급 하는 방법에 대해 알아봅니다 [검사 hello 다음 홉 VM에서](network-watcher-check-next-hop-portal.md)</span><span class="sxs-lookup"><span data-stu-id="98deb-121">Learn how toouse next hop toofind issues with network connectivity by visiting [Check hello next hop on a VM](network-watcher-check-next-hop-portal.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













