---
title: "Azure Network Watcher에서 IP 흐름 확인 소개 | Microsoft Docs"
description: "이 페이지는 Network Watcher IP 흐름 확인 기능에 대한 개요를 제공합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: d352fb2d-4b4f-4ac4-9c2e-1cfccf0e7e03
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 9c0dfc449b3d93d8aa4551ce16476c8313d731fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-ip-flow-verify-in-azure-network-watcher"></a><span data-ttu-id="5c62f-103">Azure Network Watcher에서 IP 흐름 확인 소개</span><span class="sxs-lookup"><span data-stu-id="5c62f-103">Introduction to IP flow verify in Azure Network Watcher</span></span>

<span data-ttu-id="5c62f-104">IP 흐름 확인은 5개 튜플 정보에 따라 가상 컴퓨터 간 패킷이 허용되거나 거부되는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c62f-104">IP flow verify checks if a packet is allowed or denied to or from a virtual machine based on 5-tuple information.</span></span> <span data-ttu-id="5c62f-105">이 정보는 방향, 프로토콜, 로컬 IP, 원격 IP, 로컬 포트 및 원격 포트로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c62f-105">This information consists of direction, protocol, local IP, remote IP, local port, and remote port.</span></span> <span data-ttu-id="5c62f-106">보안 그룹에서 패킷을 거부하면 해당 패킷을 거부한 규칙의 이름이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c62f-106">If the packet is denied by a security group, the name of the rule that denied the packet is returned.</span></span> <span data-ttu-id="5c62f-107">모든 원본 또는 대상 IP를 선택할 수 있는 동안 이 기능을 통해 관리자는 인터넷 간 및 온-프레미스 환경 간 연결 문제를 신속하게 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c62f-107">While any source or destination IP can be chosen, this feature helps administrators quickly diagnose connectivity issues from or to the internet and from or to the on-premises environment.</span></span>

<span data-ttu-id="5c62f-108">IP 흐름 확인은 가상 컴퓨터의 네트워크 인터페이스를 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c62f-108">IP flow verify targets a network interface of a virtual machine.</span></span> <span data-ttu-id="5c62f-109">그런 다음 해당 네트워크 인터페이스 간에서 구성된 설정에 따라 트래픽 흐름이 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c62f-109">Traffic flow is then verified based on the configured settings to or from that network interface.</span></span> <span data-ttu-id="5c62f-110">이 기능은 네트워크 보안 그룹에서 규칙이 가상 컴퓨터 간의 수신 또는 송신 트래픽을 차단하는 경우를 확인하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="5c62f-110">This capability is useful in confirming if a rule in a Network Security Group is blocking ingress or egress traffic to or from a virtual machine.</span></span>

<span data-ttu-id="5c62f-111">Network Watcher의 인스턴스는 IP 흐름을 실행하려는 모든 지역에서 만들어져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c62f-111">An instance of Network Watcher needs to be created in all regions that you plan to run IP flow verify.</span></span> <span data-ttu-id="5c62f-112">Network Watcher는 지역 서비스이며 동일한 지역의 리소스에 대해서만 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c62f-112">Network Watcher is a regional service and can only be ran against resources in the same region.</span></span> <span data-ttu-id="5c62f-113">NIC와 연결된 경로는 여전히 반환되므로 IP 흐름 확인의 결과에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5c62f-113">This does not affect the results of IP flow verify as the route associated with the NIC will still be returned.</span></span>

![1][1]

## <a name="next-steps"></a><span data-ttu-id="5c62f-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5c62f-115">Next steps</span></span>

<span data-ttu-id="5c62f-116">다음 문서를 참조하여 포털을 통해 특정 가상 컴퓨터에 대해 패킷이 허용되거나 거부되는 경우를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5c62f-116">Visit the following article to learn if a packet is allowed or denied for a specific virtual machine through the portal.</span></span> [<span data-ttu-id="5c62f-117">포털을 사용하여 IP 흐름 확인으로 VM에서 트래픽이 허용되는지 확인</span><span class="sxs-lookup"><span data-stu-id="5c62f-117">Check if traffic is allowed on a VM with IP Flow Verify using the portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png












