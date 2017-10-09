---
title: "Azure 부하 분산 장치에 대 한 ipv6 aaaOverview | Microsoft Docs"
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
ms.openlocfilehash: 5b203f77d86cc1ad455f4ebb297097aef46b658d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-ipv6-for-azure-load-balancer"></a><span data-ttu-id="e22ea-104">Azure Load Balancer의 IPv6에 대한 개요</span><span class="sxs-lookup"><span data-stu-id="e22ea-104">Overview of IPv6 for Azure Load Balancer</span></span>

<span data-ttu-id="e22ea-105">인터넷 연결 부하 분산 장치는 IPv6 주소를 사용해 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-105">Internet-facing load balancers can be deployed with an IPv6 address.</span></span> <span data-ttu-id="e22ea-106">또한 tooIPv4 연결,이 통해 기능을 수행 하는 hello:</span><span class="sxs-lookup"><span data-stu-id="e22ea-106">In addition tooIPv4 connectivity, this enables hello following capabilities:</span></span>

* <span data-ttu-id="e22ea-107">기본 종단 간 IPv6 연결 공용 인터넷 클라이언트와 Azure 가상 컴퓨터 (Vm) 사이의 hello 부하 분산 장치를 통해.</span><span class="sxs-lookup"><span data-stu-id="e22ea-107">Native end-to-end IPv6 connectivity between public Internet clients and Azure Virtual Machines (VMs) through hello load balancer.</span></span>
* <span data-ttu-id="e22ea-108">VM과 공용 인터넷 IPv6 사용 가능 클라이언트 사이의 네이티브 종단 간 IPv6 아웃바운드 연결.</span><span class="sxs-lookup"><span data-stu-id="e22ea-108">Native end-to-end IPv6 outbound connectivity between VMs and public Internet IPv6-enabled clients.</span></span>

<span data-ttu-id="e22ea-109">다음 그림 hello Azure 부하 분산 장치에 대 한 hello IPv6 기능을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-109">hello following picture illustrates hello IPv6 functionality for Azure Load Balancer.</span></span>

![IPv6를 사용하여 Azure Load Balancer](./media/load-balancer-ipv6-overview/load-balancer-ipv6.png)

<span data-ttu-id="e22ea-111">배포 된 후 IPv4 또는 IPv6 가능 인터넷 클라이언트 hello 공용 IPv4 또는 IPv6 주소 (또는 호스트 이름)의 Azure 인터넷 연결 부하 분산 장치 hello와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-111">Once deployed, an IPv4 or IPv6-enabled Internet client can communicate with hello public IPv4 or IPv6 addresses (or hostnames) of hello Azure Internet-facing Load Balancer.</span></span> <span data-ttu-id="e22ea-112">hello 부하 분산 장치 경로 hello hello vm 네트워크 주소 변환 (NAT)를 사용 하 여 IPv6 패킷 toohello 개인 IPv6 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-112">hello load balancer routes hello IPv6 packets toohello private IPv6 addresses of hello VMs using network address translation (NAT).</span></span> <span data-ttu-id="e22ea-113">hello IPv6 인터넷 클라이언트 hello hello Vm의 IPv6 주소와 직접 통신할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-113">hello IPv6 Internet client cannot communicate directly with hello IPv6 address of hello VMs.</span></span>

## <a name="features"></a><span data-ttu-id="e22ea-114">기능</span><span class="sxs-lookup"><span data-stu-id="e22ea-114">Features</span></span>

<span data-ttu-id="e22ea-115">Azure Resource Manager를 통해 배포된 VM에 대한 네이티브 IPv6 지원은 다음을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-115">Native IPv6 support for VMs deployed via Azure Resource Manager provides:</span></span>

1. <span data-ttu-id="e22ea-116">IPv6 hello 인터넷에 있는 클라이언트에 대 한 IPv6 서비스 부하 분산</span><span class="sxs-lookup"><span data-stu-id="e22ea-116">Load-balanced IPv6 services for IPv6 clients on hello Internet</span></span>
2. <span data-ttu-id="e22ea-117">VM의 네이티브 IPv6 및 IPv4 끝점("이중 스택됨")</span><span class="sxs-lookup"><span data-stu-id="e22ea-117">Native IPv6 and IPv4 endpoints on VMs ("dual stacked")</span></span>
3. <span data-ttu-id="e22ea-118">인바운드 및 아웃바운드 시작 네이티브 IPv6 연결</span><span class="sxs-lookup"><span data-stu-id="e22ea-118">Inbound and outbound-initiated native IPv6 connections</span></span>
4. <span data-ttu-id="e22ea-119">TCP, UDP, HTTP(S)와 같은 지원되는 프로토콜은 서비스 아키텍처의 전체 범위를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-119">Supported protocols such as TCP, UDP, and HTTP(S) enable a full range of service architectures</span></span>

## <a name="benefits"></a><span data-ttu-id="e22ea-120">이점</span><span class="sxs-lookup"><span data-stu-id="e22ea-120">Benefits</span></span>

<span data-ttu-id="e22ea-121">이 기능을 통해 주요 이점은 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="e22ea-121">This functionality enables hello following key benefits:</span></span>

* <span data-ttu-id="e22ea-122">새 응용 프로그램에 액세스할 수 있는 tooIPv6 으로만 이동 가능한 클라이언트 수 없어도 정부 규정을 준수</span><span class="sxs-lookup"><span data-stu-id="e22ea-122">Meet government regulations requiring that new applications be accessible tooIPv6-only clients</span></span>
* <span data-ttu-id="e22ea-123">Enable 모바일 및 IOT (사물) 개발자 toouse 이중 누적 (IPv6 + IPv4) Azure 가상 컴퓨터 tooaddress의 인터넷 hello 증가 모바일 및 IOT 시장</span><span class="sxs-lookup"><span data-stu-id="e22ea-123">Enable mobile and Internet of things (IOT) developers toouse dual-stacked (IPv4+IPv6) Azure Virtual Machines tooaddress hello growing mobile & IOT markets</span></span>

## <a name="details-and-limitations"></a><span data-ttu-id="e22ea-124">세부 사항 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="e22ea-124">Details and limitations</span></span>

<span data-ttu-id="e22ea-125">세부 정보</span><span class="sxs-lookup"><span data-stu-id="e22ea-125">Details</span></span>

* <span data-ttu-id="e22ea-126">hello Azure DNS 서비스 IPv4 A 및 AAAA IPv6 모두 이름 레코드를 포함 하며 hello 부하 분산 장치에 대 한 두 레코드를 사용 하 여 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-126">hello Azure DNS service contains both IPv4 A and IPv6 AAAA name records and responds with both records for hello load balancer.</span></span> <span data-ttu-id="e22ea-127">hello 클라이언트와 어떤 주소 (IPv4 또는 IPv6) toocommunicate를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-127">hello client chooses which address (IPv4 or IPv6) toocommunicate with.</span></span>
* <span data-ttu-id="e22ea-128">VM 시작 연결 tooa 공용 IPv6 인터넷에 연결 된 장치, 네트워크 주소 변환 hello 부하 분산 장치 (NAT) toohello 공용 IPv6 주소 hello VM의 source IPv6 주소는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-128">When a VM initiates a connection tooa public Internet IPv6-connected device, hello VM's source IPv6 address is network address translated (NAT) toohello public IPv6 address of hello load balancer.</span></span>
* <span data-ttu-id="e22ea-129">Hello Linux 운영 체제를 실행 하는 Vm에 구성 된 tooreceive DHCP 통해 IPv6 IP 주소 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-129">VMs running hello Linux operating system must be configured tooreceive an IPv6 IP address via DHCP.</span></span> <span data-ttu-id="e22ea-130">Azure 갤러리는 이미 hello hello Linux 이미지의 많은 toosupport IPv6 수정 하지 않고 구성.</span><span class="sxs-lookup"><span data-stu-id="e22ea-130">Many of hello Linux images in hello Azure Gallery are already configured toosupport IPv6 without modification.</span></span> <span data-ttu-id="e22ea-131">자세한 내용은 [Linux VM에 대한 DHCPv6 구성](load-balancer-ipv6-for-linux.md)</span><span class="sxs-lookup"><span data-stu-id="e22ea-131">For more information, see [Configuring DHCPv6 for Linux VMs](load-balancer-ipv6-for-linux.md)</span></span>
* <span data-ttu-id="e22ea-132">선택 하는 경우 사용자 부하 분산 장치 상태 프로브 toouse IPv4 프로브를 만들고 hello IPv4 및 IPv6 끝점 모두와 함께 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-132">If you choose toouse a health probe with your load balancer, create an IPv4 probe and use it with both hello IPv4 and IPv6 endpoints.</span></span> <span data-ttu-id="e22ea-133">VM에 hello 서비스가 다운 되 면 hello IPv4 및 IPv6 끝점 모두 순환 순서에서 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-133">If hello service on your VM goes down, both hello IPv4 and IPv6 endpoints are taken out of rotation.</span></span>

<span data-ttu-id="e22ea-134">제한 사항</span><span class="sxs-lookup"><span data-stu-id="e22ea-134">Limitations</span></span>

* <span data-ttu-id="e22ea-135">Hello Azure 포털에서에서 IPv6 부하 분산 규칙을 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-135">You cannot add IPv6 load balancing rules in hello Azure portal.</span></span> <span data-ttu-id="e22ea-136">hello 규칙 CLI, PowerShell hello 템플릿을 통해만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-136">hello rules can only be created through hello template, CLI, PowerShell.</span></span>
* <span data-ttu-id="e22ea-137">기존 Vm toouse IPv6 주소를 업그레이드 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-137">You may not upgrade existing VMs toouse IPv6 addresses.</span></span> <span data-ttu-id="e22ea-138">새 VM을 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-138">You must deploy new VMs.</span></span>
* <span data-ttu-id="e22ea-139">각 VM에서 tooa 단일 네트워크 인터페이스가 단일 IPv6 주소를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-139">A single IPv6 address can be assigned tooa single network interface in each VM.</span></span>
* <span data-ttu-id="e22ea-140">IPv6 주소를 공개 하는 hello tooa VM을 할당할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-140">hello public IPv6 addresses cannot be assigned tooa VM.</span></span> <span data-ttu-id="e22ea-141">부하 분산 장치 tooa 할당만 하기.</span><span class="sxs-lookup"><span data-stu-id="e22ea-141">They can only be assigned tooa load balancer.</span></span>
* <span data-ttu-id="e22ea-142">공용 IPv6 주소에 대 한 hello 역방향 DNS 조회를 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-142">You cannot configure hello reverse DNS lookup for your public IPv6 addresses.</span></span>
* <span data-ttu-id="e22ea-143">hello IPv6 주소가 포함 된 hello Vm에는 Azure 클라우드 서비스의 구성원 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-143">hello VMs with hello IPv6 addresses cannot be members of an Azure Cloud Service.</span></span> <span data-ttu-id="e22ea-144">연결 된 Azure 가상 네트워크 (VNet) tooan 하 고의 IPv4 주소를 통해 서로 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-144">They can be connected tooan Azure Virtual Network (VNet) and communicate with each other over their IPv4 addresses.</span></span>
* <span data-ttu-id="e22ea-145">개인 IPv6 주소를 리소스 그룹의 개별 VM에 배포할 수 있지만 확장 집합을 통해 리소스 그룹에 배포할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-145">Private IPv6 addresses can be deployed on individual VMs in a resource group but cannot be deployed into a resource group via Scale Sets.</span></span>
* <span data-ttu-id="e22ea-146">Azure Vm은 IPv6 tooother Vm, 다른 Azure 서비스 또는 온-프레미스 장치를 통해 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-146">Azure VMs cannot connect over IPv6 tooother VMs, other Azure services, or on-premises devices.</span></span> <span data-ttu-id="e22ea-147">I p v 6을 통해만 hello Azure 부하 분산 장치와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-147">They can only communicate with hello Azure load balancer over IPv6.</span></span> <span data-ttu-id="e22ea-148">그러나 IPv4를 사용하면 이러한 다른 리소스와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-148">However, they can communicate with these other resources using IPv4.</span></span>
* <span data-ttu-id="e22ea-149">IPv4에 대한 Network Security Group (NSG) 보호는 이중 스택 (IPv6+IPv4) 배포에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-149">Network Security Group (NSG) protection for IPv4 is supported in dual-stack (IPv4+IPv6) deployments.</span></span> <span data-ttu-id="e22ea-150">Nsg은 toohello IPv6 끝점 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-150">NSGs do not apply toohello IPv6 endpoints.</span></span>
* <span data-ttu-id="e22ea-151">IPv6 hello 끝점 VM이 아닌 hello에 직접 노출 toohello 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-151">hello IPv6 endpoint on hello VM is not exposed directly toohello internet.</span></span> <span data-ttu-id="e22ea-152">부하 분산 장치 뒤에.있습니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-152">It is behind a load balancer.</span></span> <span data-ttu-id="e22ea-153">Hello 부하 분산 장치 규칙에 지정 된 hello 포트만 i p v 6을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-153">Only hello ports specified in hello load balancer rules are accessible over IPv6.</span></span>
* <span data-ttu-id="e22ea-154">I p v 6은 IdleTimeout 매개 변수를 hello 변경 **현재 지원 되지 않는**합니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-154">Changing hello IdleTimeout parameter for IPv6 is **currently not supported**.</span></span> <span data-ttu-id="e22ea-155">hello 기본값은 4 분입니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-155">hello default is four minutes.</span></span>
* <span data-ttu-id="e22ea-156">I p v 6은 loadDistributionMethod 매개 변수를 hello 변경 **현재 지원 되지 않는**합니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-156">Changing hello loadDistributionMethod parameter for IPv6 is **currently not supported**.</span></span>
* <span data-ttu-id="e22ea-157">예약된 IPv6 IP(여기서 IPAllocationMethod = static)는 **현재 지원되지 않습니다**.</span><span class="sxs-lookup"><span data-stu-id="e22ea-157">Reserved IPv6 IPs (where IPAllocationMethod = static) are **currently not supported**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e22ea-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e22ea-158">Next steps</span></span>

<span data-ttu-id="e22ea-159">자세한 내용은 방법 toodeploy i p v 6는 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="e22ea-159">Learn how toodeploy a load balancer with IPv6.</span></span>

* [<span data-ttu-id="e22ea-160">지역별 IPv6 가용성</span><span class="sxs-lookup"><span data-stu-id="e22ea-160">Availability of IPv6 by region</span></span>](https://go.microsoft.com/fwlink/?linkid=828357)
* [<span data-ttu-id="e22ea-161">템플릿을 사용하여 IPv6와 함께 부하 분산 장치 배포하기</span><span class="sxs-lookup"><span data-stu-id="e22ea-161">Deploy a load balancer with IPv6 using a template</span></span>](load-balancer-ipv6-internet-template.md)
* [<span data-ttu-id="e22ea-162">Azure PowerShell을 사용하여 IPv6와 함께 부하 분산 장치 배포하기</span><span class="sxs-lookup"><span data-stu-id="e22ea-162">Deploy a load balancer with IPv6 using Azure PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
* [<span data-ttu-id="e22ea-163">Azure CLI를 사용하여 IPv6와 함께 부하 분산 장치 배포하기</span><span class="sxs-lookup"><span data-stu-id="e22ea-163">Deploy a load balancer with IPv6 using Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
