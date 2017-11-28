---
title: "Azure Load Balancer의 IPv6에 대한 개요 | Microsoft Docs"
description: "Azure Load Balancer 및 부하 분산된 VM에 대한 IPv6 지원 이해하기."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
keywords: "ipv6, Azure Load Balancer, 이중 스택, 공용 IP, 기본 ipv6, 모바일, iot"
ms.assetid: 6a1d583f-a305-40fd-a94b-fa42e1943bbb
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: kumud
ms.openlocfilehash: 8cca857314ecf37ef51700fd25aef228515ecd0a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-ipv6-for-azure-load-balancer"></a><span data-ttu-id="70d84-104">Azure Load Balancer의 IPv6에 대한 개요</span><span class="sxs-lookup"><span data-stu-id="70d84-104">Overview of IPv6 for Azure Load Balancer</span></span>

<span data-ttu-id="70d84-105">인터넷 연결 부하 분산 장치는 IPv6 주소를 사용해 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-105">Internet-facing load balancers can be deployed with an IPv6 address.</span></span> <span data-ttu-id="70d84-106">IPv4 연결 외에도 다음과 같은 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-106">In addition to IPv4 connectivity, this enables the following capabilities:</span></span>

* <span data-ttu-id="70d84-107">부하 분산 장치를 통한 공용 인터넷 클라이언트와 Azure Virtual Machines(VM) 사이의 네이티브 종단 간 IPv6 연결.</span><span class="sxs-lookup"><span data-stu-id="70d84-107">Native end-to-end IPv6 connectivity between public Internet clients and Azure Virtual Machines (VMs) through the load balancer.</span></span>
* <span data-ttu-id="70d84-108">VM과 공용 인터넷 IPv6 사용 가능 클라이언트 사이의 네이티브 종단 간 IPv6 아웃바운드 연결.</span><span class="sxs-lookup"><span data-stu-id="70d84-108">Native end-to-end IPv6 outbound connectivity between VMs and public Internet IPv6-enabled clients.</span></span>

<span data-ttu-id="70d84-109">다음 그림은 Azure Load Balancer에 대한 IPv6 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-109">The following picture illustrates the IPv6 functionality for Azure Load Balancer.</span></span>

![IPv6를 사용하여 Azure Load Balancer](./media/load-balancer-ipv6-overview/load-balancer-ipv6.png)

<span data-ttu-id="70d84-111">배포된 후 IPv4 또는 IPv6 사용 가능 인터넷 클라이언트는 Azure 인터넷 연결 Load Balancer의 공용 IPv4 또는 IPv6 주소(또는 호스트 이름)와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-111">Once deployed, an IPv4 or IPv6-enabled Internet client can communicate with the public IPv4 or IPv6 addresses (or hostnames) of the Azure Internet-facing Load Balancer.</span></span> <span data-ttu-id="70d84-112">부하 분산 장치는 NAT(네트워크 주소 변환)를 사용하여 VM의 개인 IPv6 주소로 IPv6 패킷을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-112">The load balancer routes the IPv6 packets to the private IPv6 addresses of the VMs using network address translation (NAT).</span></span> <span data-ttu-id="70d84-113">IPv6 인터넷 클라이언트는 VM의 IPv6 주소와 직접 통신할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-113">The IPv6 Internet client cannot communicate directly with the IPv6 address of the VMs.</span></span>

## <a name="features"></a><span data-ttu-id="70d84-114">기능</span><span class="sxs-lookup"><span data-stu-id="70d84-114">Features</span></span>

<span data-ttu-id="70d84-115">Azure Resource Manager를 통해 배포된 VM에 대한 네이티브 IPv6 지원은 다음을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-115">Native IPv6 support for VMs deployed via Azure Resource Manager provides:</span></span>

1. <span data-ttu-id="70d84-116">인터넷에서 IPv6 클라이언트에 대해 부하 분산된 IPv6 서비스</span><span class="sxs-lookup"><span data-stu-id="70d84-116">Load-balanced IPv6 services for IPv6 clients on the Internet</span></span>
2. <span data-ttu-id="70d84-117">VM의 네이티브 IPv6 및 IPv4 끝점("이중 스택됨")</span><span class="sxs-lookup"><span data-stu-id="70d84-117">Native IPv6 and IPv4 endpoints on VMs ("dual stacked")</span></span>
3. <span data-ttu-id="70d84-118">인바운드 및 아웃바운드 시작 네이티브 IPv6 연결</span><span class="sxs-lookup"><span data-stu-id="70d84-118">Inbound and outbound-initiated native IPv6 connections</span></span>
4. <span data-ttu-id="70d84-119">TCP, UDP, HTTP(S)와 같은 지원되는 프로토콜은 서비스 아키텍처의 전체 범위를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-119">Supported protocols such as TCP, UDP, and HTTP(S) enable a full range of service architectures</span></span>

## <a name="benefits"></a><span data-ttu-id="70d84-120">이점</span><span class="sxs-lookup"><span data-stu-id="70d84-120">Benefits</span></span>

<span data-ttu-id="70d84-121">이 기능을 통해 다음과 같은 주요 이점을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-121">This functionality enables the following key benefits:</span></span>

* <span data-ttu-id="70d84-122">새 응용 프로그램이 IPv6 전용 클라이언트에 액세스할 수 있도록 한 정부 규정을 충족합니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-122">Meet government regulations requiring that new applications be accessible to IPv6-only clients</span></span>
* <span data-ttu-id="70d84-123">모바일 및 IoT(사물 인터넷) 개발자가 성장하는 모바일 및 IoT 시장에 대처하기 위해 이중 스택된(IPv6+IPv4) Azure Virtual Machines를 사용할 수 있도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-123">Enable mobile and Internet of things (IOT) developers to use dual-stacked (IPv4+IPv6) Azure Virtual Machines to address the growing mobile & IOT markets</span></span>

## <a name="details-and-limitations"></a><span data-ttu-id="70d84-124">세부 사항 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="70d84-124">Details and limitations</span></span>

<span data-ttu-id="70d84-125">세부 정보</span><span class="sxs-lookup"><span data-stu-id="70d84-125">Details</span></span>

* <span data-ttu-id="70d84-126">Azure DNS 서비스는 IPv4 및 IPv6 AAAA 이름 레코드를 모두 포함하며 부하 분산 장치에 대해 두 레코드와 반응합니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-126">The Azure DNS service contains both IPv4 A and IPv6 AAAA name records and responds with both records for the load balancer.</span></span> <span data-ttu-id="70d84-127">클라이언트는 어떤 주소(IPv4 또는 IPv6)와 통신할지 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-127">The client chooses which address (IPv4 or IPv6) to communicate with.</span></span>
* <span data-ttu-id="70d84-128">VM이 공용 인터넷 IPv6 연결 장치에 연결을 시작할 경우 VM의 원본 IPv6 주소는 부하 분산 장치의 공용 IPv6 주소에 대한 NAT(네트워크 주소 변환)입니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-128">When a VM initiates a connection to a public Internet IPv6-connected device, the VM's source IPv6 address is network address translated (NAT) to the public IPv6 address of the load balancer.</span></span>
* <span data-ttu-id="70d84-129">Linux 운영 체제를 실행하는 VM은 DHCP 통해 IPv6 IP 주소를 수신하도록 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-129">VMs running the Linux operating system must be configured to receive an IPv6 IP address via DHCP.</span></span> <span data-ttu-id="70d84-130">Azure Gallery의 대부분 Linux 이미지는 수정하지 않고 IPv6를 지원하도록 이미 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-130">Many of the Linux images in the Azure Gallery are already configured to support IPv6 without modification.</span></span> <span data-ttu-id="70d84-131">자세한 내용은 [Linux VM에 대한 DHCPv6 구성](load-balancer-ipv6-for-linux.md)</span><span class="sxs-lookup"><span data-stu-id="70d84-131">For more information, see [Configuring DHCPv6 for Linux VMs](load-balancer-ipv6-for-linux.md)</span></span>
* <span data-ttu-id="70d84-132">부하 분산 장치에 상태 프로브를 사용하기로 선택한 경우 IPv4 프로브 만들어 IPv4 및 IPv6 끝점 모두에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-132">If you choose to use a health probe with your load balancer, create an IPv4 probe and use it with both the IPv4 and IPv6 endpoints.</span></span> <span data-ttu-id="70d84-133">VM에서 서비스가 중단될 경우 IPv4 및 IPv6 끝점은 모두 회전 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-133">If the service on your VM goes down, both the IPv4 and IPv6 endpoints are taken out of rotation.</span></span>

<span data-ttu-id="70d84-134">제한 사항</span><span class="sxs-lookup"><span data-stu-id="70d84-134">Limitations</span></span>

* <span data-ttu-id="70d84-135">Azure Portal에 IPv6 부하 분산 규칙을 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-135">You cannot add IPv6 load balancing rules in the Azure portal.</span></span> <span data-ttu-id="70d84-136">규칙은 CLI PowerShell 템플릿을 통해서만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-136">The rules can only be created through the template, CLI, PowerShell.</span></span>
* <span data-ttu-id="70d84-137">IPv6 주소를 사용하도록 기존 VM을 업그레이드 하지 못할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-137">You may not upgrade existing VMs to use IPv6 addresses.</span></span> <span data-ttu-id="70d84-138">새 VM을 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-138">You must deploy new VMs.</span></span>
* <span data-ttu-id="70d84-139">각 VM에서 단일 네트워크 인터페이스에 단일 IPv6 주소를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-139">A single IPv6 address can be assigned to a single network interface in each VM.</span></span>
* <span data-ttu-id="70d84-140">공용 IPv6 주소는 VM에 할당할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-140">The public IPv6 addresses cannot be assigned to a VM.</span></span> <span data-ttu-id="70d84-141">부하 분산 장치에만 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-141">They can only be assigned to a load balancer.</span></span>
* <span data-ttu-id="70d84-142">공용 IPv6 주소에 대해 역방향 DNS 조회를 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-142">You cannot configure the reverse DNS lookup for your public IPv6 addresses.</span></span>
* <span data-ttu-id="70d84-143">IPv6 주소를 사용하는 VM은 Azure Cloud Service의 멤버가 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-143">The VMs with the IPv6 addresses cannot be members of an Azure Cloud Service.</span></span> <span data-ttu-id="70d84-144">Azure Virtual Network (VNet)에 연결될 수 있으며 IPv4 주소를 통해 서로 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-144">They can be connected to an Azure Virtual Network (VNet) and communicate with each other over their IPv4 addresses.</span></span>
* <span data-ttu-id="70d84-145">개인 IPv6 주소를 리소스 그룹의 개별 VM에 배포할 수 있지만 확장 집합을 통해 리소스 그룹에 배포할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-145">Private IPv6 addresses can be deployed on individual VMs in a resource group but cannot be deployed into a resource group via Scale Sets.</span></span>
* <span data-ttu-id="70d84-146">Azure VM은 IPv6를 통해 다른 VM, 다른 Azure 서비스 또는 온-프레미스 장치에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-146">Azure VMs cannot connect over IPv6 to other VMs, other Azure services, or on-premises devices.</span></span> <span data-ttu-id="70d84-147">단지 IPv6를 통해 Azure Load Balancer와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-147">They can only communicate with the Azure load balancer over IPv6.</span></span> <span data-ttu-id="70d84-148">그러나 IPv4를 사용하면 이러한 다른 리소스와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-148">However, they can communicate with these other resources using IPv4.</span></span>
* <span data-ttu-id="70d84-149">IPv4에 대한 Network Security Group (NSG) 보호는 이중 스택 (IPv6+IPv4) 배포에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-149">Network Security Group (NSG) protection for IPv4 is supported in dual-stack (IPv4+IPv6) deployments.</span></span> <span data-ttu-id="70d84-150">NSG는 IPv6 끝점에 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-150">NSGs do not apply to the IPv6 endpoints.</span></span>
* <span data-ttu-id="70d84-151">VM의 IPv6 끝점은 인터넷에 직접 노출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-151">The IPv6 endpoint on the VM is not exposed directly to the internet.</span></span> <span data-ttu-id="70d84-152">부하 분산 장치 뒤에.있습니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-152">It is behind a load balancer.</span></span> <span data-ttu-id="70d84-153">부하 분산 장치 규칙에 지정된 포트만 IPv6를 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-153">Only the ports specified in the load balancer rules are accessible over IPv6.</span></span>
* <span data-ttu-id="70d84-154">IPv6에 대한 IdleTimeout 매개 변수 변경은 **현재 지원되지 않습니다**.</span><span class="sxs-lookup"><span data-stu-id="70d84-154">Changing the IdleTimeout parameter for IPv6 is **currently not supported**.</span></span> <span data-ttu-id="70d84-155">기본 값은 4분입니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-155">The default is four minutes.</span></span>
* <span data-ttu-id="70d84-156">IPv6에 대한 loadDistributionMethod 매개 변수 변경은 **현재 지원되지 않습니다**.</span><span class="sxs-lookup"><span data-stu-id="70d84-156">Changing the loadDistributionMethod parameter for IPv6 is **currently not supported**.</span></span>
* <span data-ttu-id="70d84-157">예약된 IPv6 IP(여기서 IPAllocationMethod = static)는 **현재 지원되지 않습니다**.</span><span class="sxs-lookup"><span data-stu-id="70d84-157">Reserved IPv6 IPs (where IPAllocationMethod = static) are **currently not supported**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70d84-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="70d84-158">Next steps</span></span>

<span data-ttu-id="70d84-159">IPv6를 사용하여 부하 분산 장치를 배포하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="70d84-159">Learn how to deploy a load balancer with IPv6.</span></span>

* [<span data-ttu-id="70d84-160">지역별 IPv6 가용성</span><span class="sxs-lookup"><span data-stu-id="70d84-160">Availability of IPv6 by region</span></span>](https://go.microsoft.com/fwlink/?linkid=828357)
* [<span data-ttu-id="70d84-161">템플릿을 사용하여 IPv6와 함께 부하 분산 장치 배포하기</span><span class="sxs-lookup"><span data-stu-id="70d84-161">Deploy a load balancer with IPv6 using a template</span></span>](load-balancer-ipv6-internet-template.md)
* [<span data-ttu-id="70d84-162">Azure PowerShell을 사용하여 IPv6와 함께 부하 분산 장치 배포하기</span><span class="sxs-lookup"><span data-stu-id="70d84-162">Deploy a load balancer with IPv6 using Azure PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
* [<span data-ttu-id="70d84-163">Azure CLI를 사용하여 IPv6와 함께 부하 분산 장치 배포하기</span><span class="sxs-lookup"><span data-stu-id="70d84-163">Deploy a load balancer with IPv6 using Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
