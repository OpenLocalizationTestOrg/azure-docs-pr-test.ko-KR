---
title: "Azure 네트워크 감시자에서 aaaIntroduction tooIP 흐름 확인 | Microsoft Docs"
description: "이 페이지에서는 소개 흐름 hello 네트워크 감시자 IP의 기능을 확인"
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
ms.openlocfilehash: b648a4816a7ffdc6ca54462944b574e2395e8298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooip-flow-verify-in-azure-network-watcher"></a><span data-ttu-id="6198e-103">Azure 네트워크 감시자에서 소개 tooIP 흐름 확인</span><span class="sxs-lookup"><span data-stu-id="6198e-103">Introduction tooIP flow verify in Azure Network Watcher</span></span>

<span data-ttu-id="6198e-104">IP 흐름 패킷을 허용 또는 tooor 5-튜플 정보에 따라 가상 컴퓨터를 거부 하는 경우 검사를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198e-104">IP flow verify checks if a packet is allowed or denied tooor from a virtual machine based on 5-tuple information.</span></span> <span data-ttu-id="6198e-105">이 정보는 방향, 프로토콜, 로컬 IP, 원격 IP, 로컬 포트 및 원격 포트로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6198e-105">This information consists of direction, protocol, local IP, remote IP, local port, and remote port.</span></span> <span data-ttu-id="6198e-106">Hello 패킷 보안 그룹에 의해 거부 되 면 hello 패킷을 거부 하는 hello 규칙의 hello 이름이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6198e-106">If hello packet is denied by a security group, hello name of hello rule that denied hello packet is returned.</span></span> <span data-ttu-id="6198e-107">모든 소스 또는 대상 IP를 선택한이 기능 하는 데 도움이에서 연결 문제 또는 toohello 신속 하 게 진단 하는 관리자가 인터넷에서 또는 toohello 온-프레미스 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="6198e-107">While any source or destination IP can be chosen, this feature helps administrators quickly diagnose connectivity issues from or toohello internet and from or toohello on-premises environment.</span></span>

<span data-ttu-id="6198e-108">IP 흐름 확인은 가상 컴퓨터의 네트워크 인터페이스를 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198e-108">IP flow verify targets a network interface of a virtual machine.</span></span> <span data-ttu-id="6198e-109">트래픽 흐름에서 해당 네트워크 인터페이스 설정 tooor hello 구성에 따라 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6198e-109">Traffic flow is then verified based on hello configured settings tooor from that network interface.</span></span> <span data-ttu-id="6198e-110">이 기능은 네트워크 보안 그룹의 규칙은 가상 컴퓨터에서 수신 또는 송신 트래픽 tooor를 차단 하 고 하는 경우를 확인 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198e-110">This capability is useful in confirming if a rule in a Network Security Group is blocking ingress or egress traffic tooor from a virtual machine.</span></span>

<span data-ttu-id="6198e-111">네트워크 감시자 요구 toobe toorun IP 흐름을 계획 해야 하는 모든 지역에서 만든의 인스턴스를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198e-111">An instance of Network Watcher needs toobe created in all regions that you plan toorun IP flow verify.</span></span> <span data-ttu-id="6198e-112">네트워크 감시자 지역 서비스 이며 hello에 대 한 리소스에 대 한 실행만 수 동일한 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="6198e-112">Network Watcher is a regional service and can only be ran against resources in hello same region.</span></span> <span data-ttu-id="6198e-113">Hello NIC 여전히 반환 될 hello와 관련 된 hello 경로로 확인 IP 흐름의 결과는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6198e-113">This does not affect hello results of IP flow verify as hello route associated with hello NIC will still be returned.</span></span>

![1][1]

## <a name="next-steps"></a><span data-ttu-id="6198e-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6198e-115">Next steps</span></span>

<span data-ttu-id="6198e-116">Hello 패킷을 허용 또는 거부할지 hello 포털을 통해 특정 가상 컴퓨터에 대 한 경우 문서 toolearn 다음을 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198e-116">Visit hello following article toolearn if a packet is allowed or denied for a specific virtual machine through hello portal.</span></span> [<span data-ttu-id="6198e-117">트래픽이 허용 됩니다 IP 확인 흐름의 VM에 hello 포털을 사용 하 여 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198e-117">Check if traffic is allowed on a VM with IP Flow Verify using hello portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png












