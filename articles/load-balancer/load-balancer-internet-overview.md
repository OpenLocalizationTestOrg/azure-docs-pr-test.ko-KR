---
title: "인터넷 연결 부하 분산 장치 개요 | Microsoft Docs"
description: "인터넷 연결 부하 분산 장치 및 해당 기능에 대한 개요입니다. 가상 컴퓨터 및 클라우드 서비스를 사용하여 부하 분산 장치가 Azure에 대해 작동하는 방식입니다."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 529b37aa-a45c-41d1-8877-fee8cc1fa375
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: c420b38fbe8054bc4b701f89ebc417677ca47a27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="internet-facing-load-balancer-overview"></a><span data-ttu-id="beaff-104">인터넷 연결 부하 분산 장치 개요</span><span class="sxs-lookup"><span data-stu-id="beaff-104">Internet facing load balancer overview</span></span>

<span data-ttu-id="beaff-105">Azure 부하 분산 장치는 들어오는 트래픽의 공용 IP 주소 및 포트 번호를 가상 컴퓨터의 개인 IP 주소 및 포트 번호로 매핑하고 가상 컴퓨터에서 오는 응답 트래픽의 경우 반대 방향으로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="beaff-105">Azure load balancer maps the public IP address and port number of incoming traffic to the private IP address and port number of the virtual machine and vice versa for the response traffic from the virtual machine.</span></span> <span data-ttu-id="beaff-106">부하 분산 규칙을 사용하면 여러 가상 컴퓨터나 서비스 간에 특정 유형의 트래픽을 분산시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beaff-106">Load balancing rules allow you to distribute specific types of traffic between multiple virtual machines or services.</span></span> <span data-ttu-id="beaff-107">예를 들어 웹 요청 트래픽의 부하를 여러 웹 서버 또는 웹 역할에 분배할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beaff-107">For example, you can spread the load of web request traffic across multiple web servers or web roles.</span></span>

<span data-ttu-id="beaff-108">웹 역할 또는 작업자 역할 인스턴스를 포함하는 클라우드 서비스의 경우 서비스 정의(.csdef) 파일에 공용 끝점을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beaff-108">For a cloud service that contains instances of web roles or worker roles, you can define a public endpoint in the service definition (.csdef) file.</span></span>

<span data-ttu-id="beaff-109">*servicedefinition.csdef* 파일은 끝점 구성을 포함하며, 웹 역할 또는 작업자 역할 배포에 대한 역할 인스턴스가 여러 개 있는 경우 부하 분산 장치가 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="beaff-109">The *servicedefinition.csdef* file contains the endpoint configuration and when you have multiple role instances for a web or worker role deployment, the load balancer will be setup for it.</span></span> <span data-ttu-id="beaff-110">클라우드 배포에 인스턴스를 추가하는 방법은 서비스 구성 파일(.csfg)에서 인스턴스 개수를 변경하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="beaff-110">The way to add instances to your cloud deployment is changing the instance count on the service configuration file (.csfg).</span></span>

<span data-ttu-id="beaff-111">다음 그림에서는 공용 및 개인 TCP 포트 80에 대해 3개의 가상 컴퓨터 간에 공유되는 웹 트래픽의 부하가 분산된 끝점을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="beaff-111">The following figure shows a load-balanced endpoint for web traffic that is shared among three virtual machines for the public and private TCP port of 80.</span></span> <span data-ttu-id="beaff-112">이 세 대의 가상 컴퓨터는 부하 분산 집합에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="beaff-112">These three virtual machines are in a load-balanced set.</span></span>

![공용 부하 분산 장치 예](./media/load-balancer-internet-overview/IC727496.png)

<span data-ttu-id="beaff-114">그림 1 - 웹 트래픽에 대한 부하 분산 끝점</span><span class="sxs-lookup"><span data-stu-id="beaff-114">Figure 1 - Load-balanced endpoint for web traffic</span></span>

<span data-ttu-id="beaff-115">인터넷 클라이언트가 80 TCP 포트에서 클라우드 서비스의 공용 IP 주소로 웹 페이지 요청을 보내면 Azure Load Balancer에서 부하 분산 집합에 있는 3개의 가상 컴퓨터 간에 요청을 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="beaff-115">When Internet clients send web page requests to the public IP address of the cloud service on TCP port 80, the Azure Load Balancer distributes the requests between the three virtual machines in the load-balanced set.</span></span> <span data-ttu-id="beaff-116">부하 분산 알고리즘에 대한 자세한 내용은 [부하 분산 장치 개요 페이지](load-balancer-overview.md#load-balancer-features)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="beaff-116">For more information about load balancer algorithms, see the [load balancer overview page](load-balancer-overview.md#load-balancer-features).</span></span>

<span data-ttu-id="beaff-117">기본적으로 Azure Load Balancer는 네트워크 트래픽을 여러 가상 컴퓨터 인스턴스에 고르게 분산시킵니다.</span><span class="sxs-lookup"><span data-stu-id="beaff-117">By default, Azure Load Balancer distributes network traffic equally among multiple virtual machine instances.</span></span> <span data-ttu-id="beaff-118">세션 선호도도 구성할 수 있습니다. 자세한 내용은 [부하 분산 장치 배포 모드](load-balancer-distribution-mode.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="beaff-118">You can also configure session affinity, For more information, see [load balancer distribution mode](load-balancer-distribution-mode.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="beaff-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="beaff-119">Next steps</span></span>

<span data-ttu-id="beaff-120">[내부 부하 분산 장치](load-balancer-internal-overview.md)에서 클라우드 배포에 적합한 부하 분산 장치를 보다 명확하게 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beaff-120">Learn about [Internal load balancer](load-balancer-internal-overview.md) to better understand which load balancer is a better fit for your cloud deployment.</span></span>

<span data-ttu-id="beaff-121">[인터넷 연결 부하 분산 장치를 시작](load-balancer-get-started-internet-arm-ps.md)하고 특정 부하 분산 장치 네트워크 트래픽 동작에 대한 [배포 모드](load-balancer-distribution-mode.md) 유형을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beaff-121">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for an specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="beaff-122">응용 프로그램이 부하 분산 장치 뒤의 서버에 대한 연결을 유지해야 하는 경우 [부하 분산 장치에 대한 유휴 TCP 시간 제한 설정](load-balancer-tcp-idle-timeout.md)에 대해 자세히 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beaff-122">If your application needs to keep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="beaff-123">Azure 부하 분산 장치를 사용하는 경우 유휴 연결 동작에 대해 알아보는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="beaff-123">It will help to learn about idle connection behavior when you are using Azure Load Balancer.</span></span>
