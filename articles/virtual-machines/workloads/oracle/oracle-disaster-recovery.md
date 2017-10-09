---
title: "Azure 환경에서 Oracle 재해 복구 시나리오의 aaaOverview | Microsoft Docs"
description: "Azure 환경의 Oracle Database 12c 데이터베이스에 대한 재해 복구 시나리오입니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/2/2017
ms.author: rclaus
ms.openlocfilehash: 1fa69e1ba044b46b27695fec92fd9ca82df796f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-for-an-oracle-database-12c-database-in-an-azure-environment"></a><span data-ttu-id="8e6c7-103">Azure 환경의 Oracle Database 12c 데이터베이스 재해 복구</span><span class="sxs-lookup"><span data-stu-id="8e6c7-103">Disaster recovery for an Oracle Database 12c database in an Azure environment</span></span>

## <a name="assumptions"></a><span data-ttu-id="8e6c7-104">가정</span><span class="sxs-lookup"><span data-stu-id="8e6c7-104">Assumptions</span></span>

- <span data-ttu-id="8e6c7-105">Oracle Data Guard 설계 및 Azure 환경에 대해 이해하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e6c7-105">You have an understanding of Oracle Data Guard design and Azure environments.</span></span>


## <a name="goals"></a><span data-ttu-id="8e6c7-106">목표</span><span class="sxs-lookup"><span data-stu-id="8e6c7-106">Goals</span></span>
- <span data-ttu-id="8e6c7-107">디자인 hello 토폴로지 및 재해 복구 (DR) 요구 사항에 맞게 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e6c7-107">Design hello topology and configuration that meet your disaster recovery (DR) requirements.</span></span>

## <a name="scenario-1-primary-and-dr-sites-on-azure"></a><span data-ttu-id="8e6c7-108">시나리오 1: 기본 사이트 및 DR 사이트가 Azure에 있음</span><span class="sxs-lookup"><span data-stu-id="8e6c7-108">Scenario 1: Primary and DR sites on Azure</span></span>

<span data-ttu-id="8e6c7-109">고객에 게는 Oracle 데이터베이스 설정 hello 기본 사이트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e6c7-109">A customer has an Oracle database set up on hello primary site.</span></span> <span data-ttu-id="8e6c7-110">DR 사이트는 다른 지역에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e6c7-110">A DR site is in a different region.</span></span> <span data-ttu-id="8e6c7-111">hello 고객 Oracle Data Guard를 사용 하 여 이러한 사이트 간의 빠른 복구.</span><span class="sxs-lookup"><span data-stu-id="8e6c7-111">hello customer uses Oracle Data Guard for quick recovery between these sites.</span></span> <span data-ttu-id="8e6c7-112">hello 기본 사이트에는 역시 보고에 대 한 보조 데이터베이스 및 다른 용도로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e6c7-112">hello primary site also has a secondary database for reporting and other uses.</span></span> 

### <a name="topology"></a><span data-ttu-id="8e6c7-113">토폴로지</span><span class="sxs-lookup"><span data-stu-id="8e6c7-113">Topology</span></span>

<span data-ttu-id="8e6c7-114">다음은 hello Azure 설치에 대 한 요약이입니다.</span><span class="sxs-lookup"><span data-stu-id="8e6c7-114">Here is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="8e6c7-115">두 사이트(기본 사이트 및 DR 사이트)</span><span class="sxs-lookup"><span data-stu-id="8e6c7-115">Two sites (a primary site and a DR site)</span></span>
- <span data-ttu-id="8e6c7-116">두 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="8e6c7-116">Two virtual networks</span></span>
- <span data-ttu-id="8e6c7-117">Data Guard가 있는 두 Oracle 데이터베이스(주 및 대기)</span><span class="sxs-lookup"><span data-stu-id="8e6c7-117">Two Oracle databases with Data Guard (primary and standby)</span></span>
- <span data-ttu-id="8e6c7-118">Golden Gate 또는 Data Guard가 있는 두 Oracle 데이터베이스(기본 사이트에만 해당)</span><span class="sxs-lookup"><span data-stu-id="8e6c7-118">Two Oracle databases with Golden Gate or Data Guard (primary site only)</span></span>
- <span data-ttu-id="8e6c7-119">두 개의 응용 프로그램 서비스, 기본 및 hello DR 사이트에</span><span class="sxs-lookup"><span data-stu-id="8e6c7-119">Two application services, one primary and one on hello DR site</span></span>
- <span data-ttu-id="8e6c7-120">*가용성 집합* hello 기본 사이트에서 데이터베이스 및 응용 프로그램 서비스에 사용 되는</span><span class="sxs-lookup"><span data-stu-id="8e6c7-120">An *availability set,* which is used for database and application service on hello primary site</span></span>
- <span data-ttu-id="8e6c7-121">하나의 jumpbox toohello 개인 네트워크 액세스를 제한 하 고 관리자가 한 로그인만 허용 하는 각 사이트에</span><span class="sxs-lookup"><span data-stu-id="8e6c7-121">One jumpbox on each site, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="8e6c7-122">별도의 서브넷에 있는 Jumpbox, 응용 프로그램 서비스, 데이터베이스 및 VPN 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="8e6c7-122">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="8e6c7-123">응용 프로그램 및 데이터베이스 서브넷에 적용되는 NSG</span><span class="sxs-lookup"><span data-stu-id="8e6c7-123">NSG enforced on application and database subnets</span></span>

![Hello DR 토폴로지에 페이지의 스크린샷](./media/oracle-disaster-recovery/oracle_topology_01.png)

## <a name="scenario-2-primary-site-on-premises-and-dr-site-on-azure"></a><span data-ttu-id="8e6c7-125">시나리오 2: 기본 사이트는 온-프레미스에 있고, DR 사이트는 Azure에 있음</span><span class="sxs-lookup"><span data-stu-id="8e6c7-125">Scenario 2: Primary site on-premises and DR site on Azure</span></span>

<span data-ttu-id="8e6c7-126">고객이 온-프레미스에 Oracle 데이터베이스를 설치했습니다(기본 사이트).</span><span class="sxs-lookup"><span data-stu-id="8e6c7-126">A customer has an on-premises Oracle database setup (primary site).</span></span> <span data-ttu-id="8e6c7-127">DR 사이트는 Azure에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e6c7-127">A DR site is on Azure.</span></span> <span data-ttu-id="8e6c7-128">Oracle Data Guard는 이러한 사이트 간의 빠른 복구에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e6c7-128">Oracle Data Guard is used for quick recovery between these sites.</span></span> <span data-ttu-id="8e6c7-129">hello 기본 사이트에는 역시 보고에 대 한 보조 데이터베이스 및 다른 용도로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e6c7-129">hello primary site also has a secondary database for reporting and other uses.</span></span> 

<span data-ttu-id="8e6c7-130">이 설치에 대한 접근 방법은 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e6c7-130">There are two approaches for this setup.</span></span>

### <a name="approach-1-direct-connections-between-on-premises-and-azure-requiring-open-tcp-ports-on-hello-firewall"></a><span data-ttu-id="8e6c7-131">온-프레미스와 Azure hello 방화벽에서 열려 있는 TCP 포트 요구 간 접근 방식 1: 직접 연결</span><span class="sxs-lookup"><span data-stu-id="8e6c7-131">Approach 1: Direct connections between on-premises and Azure, requiring open TCP ports on hello firewall</span></span> 

<span data-ttu-id="8e6c7-132">외부 세계 hello TCP 포트 toohello 노출 하기 때문에 직접 연결 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e6c7-132">We don't recommend direct connections because they expose hello TCP ports toohello outside world.</span></span>

#### <a name="topology"></a><span data-ttu-id="8e6c7-133">토폴로지</span><span class="sxs-lookup"><span data-stu-id="8e6c7-133">Topology</span></span>

<span data-ttu-id="8e6c7-134">다음은 hello Azure 설치에 대 한 요약입니다.</span><span class="sxs-lookup"><span data-stu-id="8e6c7-134">Following is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="8e6c7-135">하나의 DR 사이트</span><span class="sxs-lookup"><span data-stu-id="8e6c7-135">One DR site</span></span> 
- <span data-ttu-id="8e6c7-136">가상 네트워크 1개</span><span class="sxs-lookup"><span data-stu-id="8e6c7-136">One virtual network</span></span>
- <span data-ttu-id="8e6c7-137">Data Guard가 있는 하나의 Oracle 데이터베이스(활성)</span><span class="sxs-lookup"><span data-stu-id="8e6c7-137">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="8e6c7-138">Hello DR 사이트에서 하나의 응용 프로그램 서비스</span><span class="sxs-lookup"><span data-stu-id="8e6c7-138">One application service on hello DR site</span></span>
- <span data-ttu-id="8e6c7-139">Toohello 개인 네트워크 액세스를 제한 하 고 관리자가 한 로그인만 허용 하는 하나의 jumpbox</span><span class="sxs-lookup"><span data-stu-id="8e6c7-139">One jumpbox, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="8e6c7-140">별도의 서브넷에 있는 Jumpbox, 응용 프로그램 서비스, 데이터베이스 및 VPN 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="8e6c7-140">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="8e6c7-141">응용 프로그램 및 데이터베이스 서브넷에 적용되는 NSG</span><span class="sxs-lookup"><span data-stu-id="8e6c7-141">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="8e6c7-142">NSG 정책/규칙 tooallow 인바운드 TCP 포트 1521 (또는 사용자 지정 포트)</span><span class="sxs-lookup"><span data-stu-id="8e6c7-142">An NSG policy/rule tooallow inbound TCP port 1521 (or a user-defined port)</span></span>
- <span data-ttu-id="8e6c7-143">NSG 정책/규칙 toorestrict 유일한 hello IP 주소/온-프레미스 (DB 또는 응용 프로그램) tooaccess hello에 대 한 가상 네트워크 주소</span><span class="sxs-lookup"><span data-stu-id="8e6c7-143">An NSG policy/rule toorestrict only hello IP address/addresses on-premises (DB or application) tooaccess hello virtual network</span></span>

![Hello DR 토폴로지에 페이지의 스크린샷](./media/oracle-disaster-recovery/oracle_topology_02.png)

### <a name="approach-2-site-to-site-vpn"></a><span data-ttu-id="8e6c7-145">방법 2: 사이트 간 VPN</span><span class="sxs-lookup"><span data-stu-id="8e6c7-145">Approach 2: Site-to-site VPN</span></span>
<span data-ttu-id="8e6c7-146">사이트 간 VPN이 더 나은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="8e6c7-146">Site-to-site VPN is a better approach.</span></span> <span data-ttu-id="8e6c7-147">VPN 설정에 대한 자세한 내용은 [CLI를 사용하여 사이트 간 VPN 연결로 가상 네트워크 만들기](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e6c7-147">For more information about setting up a VPN, see [Create a virtual network with a Site-to-Site VPN connection using CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span>

#### <a name="topology"></a><span data-ttu-id="8e6c7-148">토폴로지</span><span class="sxs-lookup"><span data-stu-id="8e6c7-148">Topology</span></span>

<span data-ttu-id="8e6c7-149">다음은 hello Azure 설치에 대 한 요약입니다.</span><span class="sxs-lookup"><span data-stu-id="8e6c7-149">Following is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="8e6c7-150">하나의 DR 사이트</span><span class="sxs-lookup"><span data-stu-id="8e6c7-150">One DR site</span></span> 
- <span data-ttu-id="8e6c7-151">가상 네트워크 1개</span><span class="sxs-lookup"><span data-stu-id="8e6c7-151">One virtual network</span></span> 
- <span data-ttu-id="8e6c7-152">Data Guard가 있는 하나의 Oracle 데이터베이스(활성)</span><span class="sxs-lookup"><span data-stu-id="8e6c7-152">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="8e6c7-153">Hello DR 사이트에서 하나의 응용 프로그램 서비스</span><span class="sxs-lookup"><span data-stu-id="8e6c7-153">One application service on hello DR site</span></span>
- <span data-ttu-id="8e6c7-154">Toohello 개인 네트워크 액세스를 제한 하 고 관리자가 한 로그인만 허용 하는 하나의 jumpbox</span><span class="sxs-lookup"><span data-stu-id="8e6c7-154">One jumpbox, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="8e6c7-155">별도의 서브넷에 있는 Jumpbox, 응용 프로그램 서비스, 데이터베이스 및 VPN 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="8e6c7-155">A jumpbox, application service, database, and VPN gateway are on separate subnets</span></span>
- <span data-ttu-id="8e6c7-156">응용 프로그램 및 데이터베이스 서브넷에 적용되는 NSG</span><span class="sxs-lookup"><span data-stu-id="8e6c7-156">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="8e6c7-157">온-프레미스와 Azure 간의 사이트 간 VPN 연결</span><span class="sxs-lookup"><span data-stu-id="8e6c7-157">Site-to-site VPN connection between on-premises and Azure</span></span>

![Hello DR 토폴로지에 페이지의 스크린샷](./media/oracle-disaster-recovery/oracle_topology_03.png)

## <a name="additional-reading"></a><span data-ttu-id="8e6c7-159">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="8e6c7-159">Additional reading</span></span>

- [<span data-ttu-id="8e6c7-160">Azure에서 Oracle 데이터베이스 설계 및 구현</span><span class="sxs-lookup"><span data-stu-id="8e6c7-160">Design and implement an Oracle database on Azure</span></span>](oracle-design.md)
- [<span data-ttu-id="8e6c7-161">Oracle Data Guard 구성</span><span class="sxs-lookup"><span data-stu-id="8e6c7-161">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="8e6c7-162">Oracle Golden Gate 구성</span><span class="sxs-lookup"><span data-stu-id="8e6c7-162">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="8e6c7-163">Oracle 백업 및 복구</span><span class="sxs-lookup"><span data-stu-id="8e6c7-163">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)


## <a name="next-steps"></a><span data-ttu-id="8e6c7-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8e6c7-164">Next steps</span></span>

- [<span data-ttu-id="8e6c7-165">자습서: 고가용성 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="8e6c7-165">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)
- [<span data-ttu-id="8e6c7-166">VM 배포 Azure CLI 샘플 탐색</span><span class="sxs-lookup"><span data-stu-id="8e6c7-166">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
