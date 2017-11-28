---
title: "Azure 네트워크 감시자 IP 흐름을 사용 하 여 aaaVerify 트래픽을 확인-Azure 포털 | Microsoft Docs"
description: "이 문서에서는 설명 방법을 toocheck 가상 컴퓨터에서 트래픽 tooor 허용 또는 거부 하는 경우"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e0e3e9a8-70eb-409a-a744-0ce9deb27148
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: abf639f36d32f3416dd927e66b635267b746e62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="cd1cb-103">트래픽은 허용 되거나 Azure 네트워크 감시자의 구성 요소는 VM과 IP 확인 흐름에서 tooor을 거부 하는 경우를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd1cb-103">Check if traffic is allowed or denied tooor from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="cd1cb-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="cd1cb-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="cd1cb-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cd1cb-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="cd1cb-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="cd1cb-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="cd1cb-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="cd1cb-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="cd1cb-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="cd1cb-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="cd1cb-109">IP 흐름은 tooor 가상 컴퓨터에서 트래픽을 허용 하는 경우 tooverify 수 있는 네트워크 감시자의 기능을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd1cb-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="cd1cb-110">들어오거나 나가는 트래픽에 대 한 hello 유효성 검사를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd1cb-110">hello validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="cd1cb-111">이 시나리오는 유용한 tooget tooan 외부 리소스 또는 다른 리소스가 가상 컴퓨터를 서로 연결할 수 있는지 여부의 현재 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="cd1cb-111">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or another resource.</span></span> <span data-ttu-id="cd1cb-112">IP 흐름 보안 그룹 NSG (네트워크) 규칙에 올바르게 구성 되어 NSG 규칙에 의해 차단 되는 흐름 문제를 해결 하는 경우 사용 되는 tooverify 수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd1cb-112">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="cd1cb-113">IP를 사용 하는 또 다른 이유 흐름 tooensure 트래픽이 차단 되도록 제대로 hello NSG 차단 하 고이 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd1cb-113">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="cd1cb-114">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="cd1cb-114">Before you begin</span></span>

<span data-ttu-id="cd1cb-115">이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 네트워크 감시자의 기존 인스턴스가 또는 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd1cb-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="cd1cb-116">hello 시나리오는 또한 적합 한 가상 컴퓨터가 리소스 그룹 사용 toobe 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd1cb-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="cd1cb-117">시나리오</span><span class="sxs-lookup"><span data-stu-id="cd1cb-117">Scenario</span></span>

<span data-ttu-id="cd1cb-118">이 시나리오에서는 가상 컴퓨터 포트 443 통해 tooanother 컴퓨터 수와 통신 하는 경우 tooverify IP 확인 흐름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd1cb-118">This scenario uses IP Flow Verify tooverify if a virtual machine can talk tooanother machine over port 443.</span></span> <span data-ttu-id="cd1cb-119">Hello 트래픽이 거부 되 면 해당 트래픽을 거부 하는 hello 보안 규칙을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd1cb-119">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="cd1cb-120">IP 확인 흐름에 대 한 자세한 toolearn 방문 [IP 흐름 확인 개요](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="cd1cb-120">toolearn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

### <a name="run-ip-flow-verify"></a><span data-ttu-id="cd1cb-121">IP 흐름 확인 실행</span><span class="sxs-lookup"><span data-stu-id="cd1cb-121">Run IP flow verify</span></span>

<span data-ttu-id="cd1cb-122">네트워크 감시자 tooyour 이동한 클릭 **IP 흐름 확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd1cb-122">Navigate tooyour Network Watcher and click **IP flow verify**.</span></span> <span data-ttu-id="cd1cb-123">Tooverify 트래픽만 원하는 hello 가상 컴퓨터와 네트워크 인터페이스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd1cb-123">Select hello virtual machine and network interface you want tooverify traffic from.</span></span> <span data-ttu-id="cd1cb-124">추가 필터링 정보를 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd1cb-124">Enter any additional filtering information and click **Check**.</span></span>

<span data-ttu-id="cd1cb-125">클릭 한 후 **확인**, 사용자가 제공한 hello 기준에 따라 hello 흐름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd1cb-125">Once you click **Check**, hello flow based on hello criteria you provided is checked.</span></span> <span data-ttu-id="cd1cb-126">hello 결과 중 하나는 **액세스 허용** 또는 **액세스가 거부 되었습니다**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd1cb-126">hello result is either **Access allowed** or **Access denied**.</span></span> <span data-ttu-id="cd1cb-127">액세스를 거부 한 경우 보안 그룹 NSG (네트워크) hello 및 트래픽을 차단 하는 보안 규칙 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd1cb-127">If access is denied, hello Network Security Group (NSG) and security rule that block traffic is provided.</span></span> <span data-ttu-id="cd1cb-128">트래픽의 hello 거부는 예상 된 동작을 hello 규칙 성공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="cd1cb-128">If hello denial of traffic is expected behavior, then hello rule was successful.</span></span>

> [!NOTE]
> <span data-ttu-id="cd1cb-129">IP 흐름 확인 hello VM 리소스 할당 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd1cb-129">IP flow verify requires that hello VM resource is allocated.</span></span>

<span data-ttu-id="cd1cb-130">다음 이미지는 hello 알 수 있듯이 hello 아웃 바운드 HTTPS 트래픽을 허용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cd1cb-130">As you can see from hello following image, hello outbound HTTPS traffic was allowed.</span></span>

![IP 흐름 확인 개요][1]

<span data-ttu-id="cd1cb-132">트래픽 변경 hello 다음 이미지와 같이 tooinbound 및 hello 인바운드 too123 포트를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd1cb-132">As seen in hello following image, traffic is changed tooinbound and hello inbound port changed too123.</span></span> <span data-ttu-id="cd1cb-133">트래픽 이제 거부 되 면 hello 메시지 "액세스가 거부 되었습니다" hello 네트워크 보안 그룹 및 보안 규칙 hello 트래픽을 거부 하는 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd1cb-133">Traffic is now denied, hello message "Access denied" is provided along with hello network security group and security rule that deny hello traffic.</span></span>

![IP 흐름 결과][2]

## <a name="next-steps"></a><span data-ttu-id="cd1cb-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cd1cb-135">Next steps</span></span>

<span data-ttu-id="cd1cb-136">트래픽을 차단 하지 않아야 하는 경우 참조 [네트워크 보안 그룹 관리](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hello 네트워크 보안 그룹 및 보안 정의 된 규칙을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd1cb-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













