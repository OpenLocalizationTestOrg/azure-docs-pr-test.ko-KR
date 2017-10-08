---
title: "CLI 샘플 aaaAzure | Microsoft Docs"
description: "Azure CLI 샘플"
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: kumud
ms.openlocfilehash: 8001b7e72480cfd0122325f7fb81c32aaad072d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-networking"></a><span data-ttu-id="7a766-103">네트워킹을 위한 Azure CLI 샘플</span><span class="sxs-lookup"><span data-stu-id="7a766-103">Azure CLI Samples for networking</span></span>

<span data-ttu-id="7a766-104">hello 다음 표는 hello Azure CLI를 사용 하 여 빌드된 링크 toobash 스크립트.</span><span class="sxs-lookup"><span data-stu-id="7a766-104">hello following table includes links toobash scripts built using hello Azure CLI.</span></span>

| | |
|-|-|
|<span data-ttu-id="7a766-105">**Azure 리소스 간 연결**</span><span class="sxs-lookup"><span data-stu-id="7a766-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="7a766-106">다중 계층 응용 프로그램을 위한 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="7a766-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-cli-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="7a766-107">프런트 엔드 및 백 엔드 서브넷이 있는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7a766-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="7a766-108">트래픽 toohello 프런트 엔드 서브넷은 제한 된 tooHTTP 및 SSH, 트래픽 toohello 하는 동안 백 엔드 서브넷은 제한 된 tooMySQL, 3306 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="7a766-108">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> |
| [<span data-ttu-id="7a766-109">2개 가상 네트워크 피어링</span><span class="sxs-lookup"><span data-stu-id="7a766-109">Peer two virtual networks</span></span>](./scripts/virtual-network-cli-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="7a766-110">만들고 hello에 두 개의 가상 네트워크를 연결 합니다. 동일한 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="7a766-110">Creates and connects two virtual networks in hello same region.</span></span> |
| [<span data-ttu-id="7a766-111">네트워크 가상 어플라이언스를 통한 트래픽 라우팅</span><span class="sxs-lookup"><span data-stu-id="7a766-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-cli-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="7a766-112">프런트 엔드 및 백 엔드 서브넷 및 hello 두 서브넷 간의 트래픽 tooroute 수 있는 VM 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7a766-112">Creates a virtual network with front-end and back-end subnets and a VM that is able tooroute traffic between hello two subnets.</span></span> |
| [<span data-ttu-id="7a766-113">인바운드 및 아웃바운드 VM 네트워크 트래픽 필터링</span><span class="sxs-lookup"><span data-stu-id="7a766-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="7a766-114">프런트 엔드 및 백 엔드 서브넷이 있는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7a766-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="7a766-115">인바운드 네트워크 트래픽을 toohello 프런트 엔드 서브넷은 제한 된 tooHTTP SSH 및 HTTPS입니다.</span><span class="sxs-lookup"><span data-stu-id="7a766-115">Inbound network traffic toohello front-end subnet is limited tooHTTP, HTTPS and SSH.</span></span> <span data-ttu-id="7a766-116">아웃 바운드 트래픽을 toohello 인터넷 hello 백 엔드 서브넷에서 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a766-116">Outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="7a766-117">**부하 분산 및 트래픽 방향**</span><span class="sxs-lookup"><span data-stu-id="7a766-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="7a766-118">고가용성을 위한 분산 트래픽 tooVMs 로드</span><span class="sxs-lookup"><span data-stu-id="7a766-118">Load balance traffic tooVMs for high availability</span></span>](./scripts/load-balancer-linux-cli-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="7a766-119">고가용성의 부하가 분산된 구성으로 여러 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7a766-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="7a766-120">VM에서 여러 웹 사이트에 부하 분산</span><span class="sxs-lookup"><span data-stu-id="7a766-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-linux-cli-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="7a766-121">조인 된 tooan Azure 가용성 집합을 통해 Azure 부하 분산 장치는 액세스할 수 있는 여러 IP 구성을 사용 하 여 두 개의 Vm을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7a766-121">Creates two VMs with multiple IP configurations, joined tooan Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="7a766-122">높은 응용 프로그램 가용성을 위해 여러 지역 간에 트래픽 전송</span><span class="sxs-lookup"><span data-stu-id="7a766-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-cli-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="7a766-123">두 개의 App Service 계획, 두 개의 웹앱, Traffic Manager 프로필 및 두 개의 Traffic Manager 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7a766-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |
