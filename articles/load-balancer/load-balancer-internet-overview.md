---
title: "부하 분산 장치 개요 직면 aaaInternet | Microsoft Docs"
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
ms.openlocfilehash: 3514f945d69ec576ed256cdd01069491e3e43936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="internet-facing-load-balancer-overview"></a><span data-ttu-id="ed7b9-104">인터넷 연결 부하 분산 장치 개요</span><span class="sxs-lookup"><span data-stu-id="ed7b9-104">Internet facing load balancer overview</span></span>

<span data-ttu-id="ed7b9-105">Hello 공용 IP 주소와 포트 번호를 들어오는 트래픽 toohello 개인 IP 주소와 포트 번호의 hello 가상 컴퓨터의 그 반대의 hello 가상 컴퓨터의 응답 트래픽은 hello에 대 한 azure 부하 분산 장치에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="ed7b9-105">Azure load balancer maps hello public IP address and port number of incoming traffic toohello private IP address and port number of hello virtual machine and vice versa for hello response traffic from hello virtual machine.</span></span> <span data-ttu-id="ed7b9-106">부하 분산 규칙을 사용 하면 특정 유형의 여러 가상 컴퓨터나 서비스 간에 트래픽을 toodistribute 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed7b9-106">Load balancing rules allow you toodistribute specific types of traffic between multiple virtual machines or services.</span></span> <span data-ttu-id="ed7b9-107">예를 들어 여러 웹 서버 또는 웹 역할에서 웹 요청 트래픽의 hello 부하를 분배할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed7b9-107">For example, you can spread hello load of web request traffic across multiple web servers or web roles.</span></span>

<span data-ttu-id="ed7b9-108">웹 역할 또는 작업자 역할 인스턴스를 포함 하는 클라우드 서비스에 대 한 hello 서비스 정의 (.csdef) 파일에서 공용 끝점을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed7b9-108">For a cloud service that contains instances of web roles or worker roles, you can define a public endpoint in hello service definition (.csdef) file.</span></span>

<span data-ttu-id="ed7b9-109">hello *servicedefinition.csdef* 파일 hello 끝점 구성을 포함 하 고 hello 부하 분산 장치에 대 한 설치 프로그램을 됩니다 웹 또는 작업자 역할 배포에 대 한 역할 인스턴스가 여러 개 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="ed7b9-109">hello *servicedefinition.csdef* file contains hello endpoint configuration and when you have multiple role instances for a web or worker role deployment, hello load balancer will be setup for it.</span></span> <span data-ttu-id="ed7b9-110">hello 방식으로 tooadd 인스턴스 tooyour 클라우드 배포는 hello 서비스 구성 파일 (.csfg)에 hello 인스턴스 수를 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed7b9-110">hello way tooadd instances tooyour cloud deployment is changing hello instance count on hello service configuration file (.csfg).</span></span>

<span data-ttu-id="ed7b9-111">hello 다음 그림은 hello 공용 및 개인 TCP 포트 80에 대 한 세 개의 가상 컴퓨터 간에 공유 되는 웹 트래픽에 대 한 부하 분산 된 끝점.</span><span class="sxs-lookup"><span data-stu-id="ed7b9-111">hello following figure shows a load-balanced endpoint for web traffic that is shared among three virtual machines for hello public and private TCP port of 80.</span></span> <span data-ttu-id="ed7b9-112">이 세 대의 가상 컴퓨터는 부하 분산 집합에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="ed7b9-112">These three virtual machines are in a load-balanced set.</span></span>

![공용 부하 분산 장치 예](./media/load-balancer-internet-overview/IC727496.png)

<span data-ttu-id="ed7b9-114">그림 1 - 웹 트래픽에 대한 부하 분산 끝점</span><span class="sxs-lookup"><span data-stu-id="ed7b9-114">Figure 1 - Load-balanced endpoint for web traffic</span></span>

<span data-ttu-id="ed7b9-115">인터넷 클라이언트가 TCP 포트 80에서 웹 페이지 요청 hello 클라우드 서비스의 공용 IP 주소 toohello 보내면, hello 부하 분산 된 집합에 3 개의 가상 컴퓨터가 hello 사이의 hello 요청 hello Azure 부하 분산 장치에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed7b9-115">When Internet clients send web page requests toohello public IP address of hello cloud service on TCP port 80, hello Azure Load Balancer distributes hello requests between hello three virtual machines in hello load-balanced set.</span></span> <span data-ttu-id="ed7b9-116">부하 분산 알고리즘에 대 한 자세한 내용은 참조 hello [부하 분산 장치 개요 페이지](load-balancer-overview.md#load-balancer-features)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed7b9-116">For more information about load balancer algorithms, see hello [load balancer overview page](load-balancer-overview.md#load-balancer-features).</span></span>

<span data-ttu-id="ed7b9-117">기본적으로 Azure Load Balancer는 네트워크 트래픽을 여러 가상 컴퓨터 인스턴스에 고르게 분산시킵니다.</span><span class="sxs-lookup"><span data-stu-id="ed7b9-117">By default, Azure Load Balancer distributes network traffic equally among multiple virtual machine instances.</span></span> <span data-ttu-id="ed7b9-118">세션 선호도도 구성할 수 있습니다. 자세한 내용은 [부하 분산 장치 배포 모드](load-balancer-distribution-mode.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed7b9-118">You can also configure session affinity, For more information, see [load balancer distribution mode](load-balancer-distribution-mode.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed7b9-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ed7b9-119">Next steps</span></span>

<span data-ttu-id="ed7b9-120">에 대 한 자세한 내용은 [내부 부하 분산 장치](load-balancer-internal-overview.md) toobetter 이해는 부하 분산 장치는 클라우드 배포에 대 한 더 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed7b9-120">Learn about [Internal load balancer](load-balancer-internal-overview.md) toobetter understand which load balancer is a better fit for your cloud deployment.</span></span>

<span data-ttu-id="ed7b9-121">[인터넷 연결 부하 분산 장치를 시작](load-balancer-get-started-internet-arm-ps.md)하고 특정 부하 분산 장치 네트워크 트래픽 동작에 대한 [배포 모드](load-balancer-distribution-mode.md) 유형을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed7b9-121">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for an specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="ed7b9-122">경우 응용 프로그램 서버 부하 분산 장치 뒤에 대 한 연결 유지 tookeep 연결에 필요한를 이해할 수 있습니다 더에 대 한 [부하 분산 장치에 대 한 TCP 시간 제한 설정을 유휴](load-balancer-tcp-idle-timeout.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed7b9-122">If your application needs tookeep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="ed7b9-123">유휴 연결 동작에 대 한 toolearn Azure 부하 분산 장치를 사용 하는 경우 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed7b9-123">It will help toolearn about idle connection behavior when you are using Azure Load Balancer.</span></span>
