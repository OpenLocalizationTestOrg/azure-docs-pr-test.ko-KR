---
title: "Azure PowerShell 샘플 | Microsoft Docs"
description: "Azure PowerShell 샘플"
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/24/2017
ms.author: georgewallace
ms.openlocfilehash: 0bca4fb6874bd265f0ae9faeb4219abeb4ffb6d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-powershell-samples-for-networking"></a><span data-ttu-id="9bd45-103">네트워킹에 대한 Azure PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="9bd45-103">Azure PowerShell Samples for networking</span></span>

<span data-ttu-id="9bd45-104">다음 표에는 Azure PowerShell을 사용하여 빌드된 스크립트에 대한 링크가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bd45-104">The following table includes links to scripts built using Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="9bd45-105">**Azure 리소스 간 연결**</span><span class="sxs-lookup"><span data-stu-id="9bd45-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="9bd45-106">다중 계층 응용 프로그램을 위한 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="9bd45-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-powershell-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="9bd45-107">프런트 엔드 및 백 엔드 서브넷이 있는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9bd45-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="9bd45-108">프런트 엔드 서브넷에 대한 트래픽은 HTTP로 제한되며, 백 엔드 서브넷에 대한 트래픽은 SQL, 포트 1433으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="9bd45-108">Traffic to the front-end subnet is limited to HTTP, while traffic to the back-end subnet is limited to SQL, port 1433.</span></span> |
| [<span data-ttu-id="9bd45-109">2개 가상 네트워크 피어링</span><span class="sxs-lookup"><span data-stu-id="9bd45-109">Peer two virtual networks</span></span>](./scripts/virtual-network-powershell-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="9bd45-110">동일한 지역에 2개 가상 네트워크를 만들고 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9bd45-110">Creates and connects two virtual networks in the same region.</span></span> |
| [<span data-ttu-id="9bd45-111">네트워크 가상 어플라이언스를 통한 트래픽 라우팅</span><span class="sxs-lookup"><span data-stu-id="9bd45-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-powershell-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="9bd45-112">프런트 엔드 및 백 엔드 서브넷과 두 서브넷 간에 트래픽을 라우팅할 수 있는 VM이 있는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9bd45-112">Creates a virtual network with front-end and back-end subnets and a VM that is able to route traffic between the two subnets.</span></span> |
| [<span data-ttu-id="9bd45-113">인바운드 및 아웃바운드 VM 네트워크 트래픽 필터링</span><span class="sxs-lookup"><span data-stu-id="9bd45-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-powershell-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="9bd45-114">프런트 엔드 및 백 엔드 서브넷이 있는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9bd45-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="9bd45-115">프런트 엔드 서브넷에 대한 인바운드 네트워크 트래픽은 HTTP 및 HTTPS로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="9bd45-115">Inbound network traffic to the front-end subnet is limited to HTTP and HTTPS..</span></span> <span data-ttu-id="9bd45-116">백 엔드 서브넷에서 인터넷으로의 아웃바운드 트래픽은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9bd45-116">Outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="9bd45-117">**부하 분산 및 트래픽 방향**</span><span class="sxs-lookup"><span data-stu-id="9bd45-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="9bd45-118">고가용성을 위해 VM에 트래픽 부하 분산</span><span class="sxs-lookup"><span data-stu-id="9bd45-118">Load balance traffic to VMs for high availability</span></span>](./scripts/load-balancer-windows-powershell-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="9bd45-119">고가용성의 부하가 분산된 구성으로 여러 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9bd45-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="9bd45-120">VM에서 여러 웹 사이트에 부하 분산</span><span class="sxs-lookup"><span data-stu-id="9bd45-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-windows-powershell-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="9bd45-121">Azure 가용성 집합에 연결되고 Azure 부하 분산 장치를 통해 액세스할 수 있는 2개의 VM을 여러 IP 구성을 사용해서 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9bd45-121">Creates two VMs with multiple IP configurations, joined to an Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="9bd45-122">높은 응용 프로그램 가용성을 위해 여러 지역 간에 트래픽 전송</span><span class="sxs-lookup"><span data-stu-id="9bd45-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-powershell-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="9bd45-123">두 개의 App Service 계획, 두 개의 웹앱, Traffic Manager 프로필 및 두 개의 Traffic Manager 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9bd45-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |
