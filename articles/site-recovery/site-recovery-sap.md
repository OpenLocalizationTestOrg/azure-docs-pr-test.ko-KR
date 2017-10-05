---
title: "Azure Site Recovery를 사용하여 다중 SAP NetWeaver 응용 프로그램 배포 보호 | Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery를 사용하여 SAP NetWeaver 응용 프로그램 배포를 보호하는 방법에 대해 설명합니다."
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: manayar
ms.openlocfilehash: 951980eeba61e53c983d5b23c301c81eee9528bd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="protect-a-multi-tier-sap-netweaver-application-deployment-using-azure-site-recovery"></a><span data-ttu-id="6c441-103">Azure Site Recovery를 사용하여 다중 SAP NetWeaver 응용 프로그램 배포 보호 </span><span class="sxs-lookup"><span data-stu-id="6c441-103">Protect a multi-tier SAP NetWeaver application deployment using Azure Site Recovery</span></span>

<span data-ttu-id="6c441-104">대부분의 중대형 SAP 배포에는 어떤 형태의 재해 복구 솔루션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-104">Most large and medium-sized SAP deployments have some form of Disaster Recovery solution.</span></span>  <span data-ttu-id="6c441-105">점점 더 많은 핵심 비즈니스 프로세스가 SAP과 같은 응용 프로그램으로 옮겨가면서 강력하고 테스트 가능한 재해 복구 솔루션이 중요성이 높아지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-105">The importance of robust and testable Disaster Recovery solutions has increased as more core business processes are moved to applications such as SAP.</span></span>  <span data-ttu-id="6c441-106">Azure Site Recovery는 SAP에서 테스트 및 통합되었으며, 경쟁 솔루션보다 총 소유 비용(TCO)은 낮으면서 대부분의 온-프레미스 재해 복구 솔루션 기능을 능가합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-106">Azure Site Recovery has been tested and integrated with SAP applications, and exceeds the capabilities of most on-premises Disaster Recovery solutions, at a lower total cost of ownership (TCO) than competing solutions.</span></span>
<span data-ttu-id="6c441-107">Azure Site Recovery를 통해 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-107">With Azure Site Recovery you can:</span></span>
* <span data-ttu-id="6c441-108">구성 요소를 Azure에 복사하여 온-프레미스로 실행 중인 SAP NetWeaver 및 비-NetWeaver 프로덕션 응용 프로그램 보호를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-108">Enable protection of SAP NetWeaver and non-NetWeaver Production applications running on-premises, by replicating components to Azure.</span></span>
* <span data-ttu-id="6c441-109">구성 요소를 다른 Azure 데이터 센터에 복사하여 Azure를 실행 중인 SAP NetWeaver 및 비-NetWeaver 프로덕션 응용 프로그램 보호를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-109">Enable protection of SAP NetWeaver and non-NetWeaver Production applications running Azure, by replicating components to another Azure datacenter.</span></span>
* <span data-ttu-id="6c441-110">Site Recovery를 사용하여 클라우드 마이그레이션을 간소화하여 Azure에 SAP 배포를 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-110">Simplify cloud migration, by using Site Recovery to migrate your SAP deployment to Azure.</span></span>
* <span data-ttu-id="6c441-111">SAP 응용 프로그램 테스팅을 위해 온디맨드로 프로덕션 클론을 만들어 SAP 프로젝트 업그레이드, 테스트 및 프로토타입 생성을 단순화합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-111">Simplify SAP project upgrades, testing, and prototyping, by creating a production clone on-demand for testing SAP applications.</span></span>

<span data-ttu-id="6c441-112">이 문서에서는 [Azure Site Recovery](site-recovery-overview.md)를 사용하여 SAP NetWeaver 응용 프로그램 배포를 보호하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-112">This article describes how to protect SAP NetWeaver application deployments using [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="6c441-113">이 문서에서는 Azure Site Recovery를 사용하여 다른 Azure 데이터 센터에 복제하여 Azure의 3계층 SAP NetWeaver 배포를 보호하기 위한 모범 사례, 지원되는 시나리오 및 구성과 테스트 장애 조치(재해 복구 훈련) 및 실제 장애 조치 모두를 포함한 장애 조치 수행 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-113">This article covers the best practices for protecting a three-tier SAP NetWeaver deployment on Azure by replicating to another Azure datacenter using Azure Site Recovery, the supported scenarios and configurations, and how to perform failovers, both test failovers (disaster recovery drills) and actual failovers.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="6c441-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6c441-114">Prerequisites</span></span>
<span data-ttu-id="6c441-115">시작하기 전에 다음 항목을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-115">Before you start, make sure you understand the following:</span></span>

1. [<span data-ttu-id="6c441-116">Azure에 가상 컴퓨터 복제</span><span class="sxs-lookup"><span data-stu-id="6c441-116">Replicating a virtual machine to Azure</span></span>](azure-to-azure-walkthrough-enable-replication.md)
2. <span data-ttu-id="6c441-117">방법: [복구 네트워크 디자인](site-recovery-azure-to-azure-networking-guidance.md)</span><span class="sxs-lookup"><span data-stu-id="6c441-117">How to [design a recovery network](site-recovery-azure-to-azure-networking-guidance.md)</span></span>
3. [<span data-ttu-id="6c441-118">Azure로 테스트 장애 조치 수행</span><span class="sxs-lookup"><span data-stu-id="6c441-118">Doing a test failover to Azure</span></span>](azure-to-azure-walkthrough-test-failover.md)
4. [<span data-ttu-id="6c441-119">Azure로 장애 조치 수행</span><span class="sxs-lookup"><span data-stu-id="6c441-119">Doing a failover to Azure</span></span>](site-recovery-failover.md)
5. <span data-ttu-id="6c441-120">방법: [도메인 컨트롤러 복제](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="6c441-120">How to [replicate a domain controller](site-recovery-active-directory.md)</span></span>
6. <span data-ttu-id="6c441-121">방법: [SQL Server 복제](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="6c441-121">How to [replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="6c441-122">지원되는 시나리오</span><span class="sxs-lookup"><span data-stu-id="6c441-122">Supported scenarios</span></span>
<span data-ttu-id="6c441-123">Azure Site Recovery를 통해 다음 시나리오에서의 재해 복구 솔루션을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-123">With Azure Site Recovery you can implement a disaster recovery solution for the following scenarios:</span></span>
* <span data-ttu-id="6c441-124">[여기](https://aka.ms/asr-a2a-architecture)에서 설계한 대로 한 Azure 데이터 센터에서 실행되는 SAP 시스템을 다른 Azure 데이터 센터에 복제(Azure - Azure DR) </span><span class="sxs-lookup"><span data-stu-id="6c441-124">SAP systems running in one Azure datacenter replicating to another Azure datacenter (Azure-to-Azure DR), as architected [here](https://aka.ms/asr-a2a-architecture).</span></span>
* <span data-ttu-id="6c441-125">[여기](https://aka.ms/asr-v2a-architecture)에서 설계한 대로 VMWare(또는 물리적) 서버에서 온-프레미스로 실행 중인 SAP 시스템을 Azure 데이터 센터의 DR 사이트로 복제(VMware-Azure DR). 몇 가지 추가적인 구성 요소 필요</span><span class="sxs-lookup"><span data-stu-id="6c441-125">SAP systems running on VMWare (or Physical) servers on-premises replicating to a DR site in an Azure datacenter (VMware-to-Azure DR), which requires some additional components as architected [here](https://aka.ms/asr-v2a-architecture).</span></span>
* <span data-ttu-id="6c441-126">[여기](https://aka.ms/asr-h2a-architecture)에서 설계한 대로 Hyper-V 온-프레미스로 실행 중인 SAP 시스템을 Azure 데이터 센터의 DR 사이트로 복제(Hyper-V 대 Azure DR). 몇 가지 추가적인 구성 요소 필요</span><span class="sxs-lookup"><span data-stu-id="6c441-126">SAP systems running on Hyper-V on-premises replicating to a DR site in an Azure datacenter (Hyper-V-to-Azure DR), which requires some additional components as architected [here](https://aka.ms/asr-h2a-architecture).</span></span>

<span data-ttu-id="6c441-127">이 문서에서는 Azure Site Recovery의 SAP 재해 복구 기능을 보여 주기 위해 첫 번째 사례인 Azure-t-Azure DR을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-127">This document uses the first case - Azure-to-Azure DR - to demonstrate Azure Site Recovery's SAP disaster recovery capabilities.</span></span> <span data-ttu-id="6c441-128">Azure Site Recovery 복제는 여러 응용 프로그램에 사용되므로 여기서 설명한 프로세스가 다른 시나리오에서도 유효할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-128">As Azure Site Recovery replication is application agnostic, the process described is expected to hold for other scenarios as well.</span></span>

### <a name="required-foundation-services"></a><span data-ttu-id="6c441-129">필요한 기반 서비스</span><span class="sxs-lookup"><span data-stu-id="6c441-129">Required foundation services</span></span>
<span data-ttu-id="6c441-130">이 문서 전체에서는 다음 기본 서비스와 함께 배포되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-130">This documentation scenario all been deployed with the following foundation services deployed:</span></span>
* <span data-ttu-id="6c441-131">ExpressRoute 또는 사이트 간 가상 사설망(VPN)</span><span class="sxs-lookup"><span data-stu-id="6c441-131">ExpressRoute or Site-to-Site Virtual Private Network (VPN)</span></span>
* <span data-ttu-id="6c441-132">Azure에서 하나 이상의 Active Directory 도메인 컨트롤러와 DNS 서버 실행됨</span><span class="sxs-lookup"><span data-stu-id="6c441-132">At least one Active Directory Domain Controller and DNS server running in Azure</span></span>

<span data-ttu-id="6c441-133">Azure Site Recovery를 배포하기 전에 위의 인프라를 구축하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-133">It is recommended that the infrastructure above is established prior to deploying Azure Site Recovery.</span></span>


## <a name="typical-sap-application-deployment"></a><span data-ttu-id="6c441-134">일반 SAP 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="6c441-134">Typical SAP application deployment</span></span>
<span data-ttu-id="6c441-135">일반적으로 대형 SAP 고객은 6~20개의 개별 SAP 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-135">Large SAP customers usually deploy between 6 to 20 individual SAP applications.</span></span>  <span data-ttu-id="6c441-136">이러한 응용 프로그램 대부분은 SAP NetWeaver ABAP 또는 Java 엔진을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-136">Most of these applications are based on the SAP NetWeaver ABAP or Java engines.</span></span>  <span data-ttu-id="6c441-137">이러한 핵심 NetWeaver 응용 프로그램을 지원하는 것은 더 적은 규모의 많은 특정 비 NetWeaver SAP 독립 실행형 엔진이며 보통은 비 SAP 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-137">Supporting these core NetWeaver applications are many smaller specific non-NetWeaver SAP standalone engines and typically some non-SAP applications.</span></span>  

<span data-ttu-id="6c441-138">수평 실행되는 모든 SAP 응용 프로그램을 인벤토리하고 배포 모드(2계층 또는 3계층), 버전, 패치, 크기, 변동 속도, 디스크 지속성 요구 사항을 판단하는 것이 매우 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-138">It is critical to inventory all the SAP applications running in a landscape and to determine the deployment mode (either 2-tier or 3-tier), versions, patches, sizes, churn rates, and disk persistence requirements.</span></span>

![배포 패턴](./media/site-recovery-sap/sap-typical-deployment.png)

<span data-ttu-id="6c441-140">SAP 데이터베이스 지속성 계층은 SQL Server AlwaysOn, Oracle DataGuard 또는 HANA System Replication 등과 같은 기본 DBMS 도구를 통해 보호되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-140">The SAP Database persistence layer should be protected via the native DBMS tools such as SQL Server AlwaysOn, Oracle DataGuard, or HANA System Replication.</span></span> <span data-ttu-id="6c441-141">클라이언트 계층도 Azure Site Recovery로 보호되지는 않지만 DR 데이터 센터에 대한 DNS Propagation 지연, 보안 및 원격 액세스 등과 같이 이 계층에 영향을 미치는 항목을 고려하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-141">The client layer is also not protected by Azure Site Recovery, but it is important to consider topics that impact this layer such as DNS Propagation delay, security and remote access to the DR datacenter.</span></span>

<span data-ttu-id="6c441-142">Azure Site Recovery는 (A)SCS를 포함한 응용 프로그램 계층에 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-142">Azure Site Recovery is the recommended solution for the application layer, including (A)SCS.</span></span> <span data-ttu-id="6c441-143">비 NetWeaver SAP 응용 프로그램 및 비 SAM 응용 프로그램 같은 기타 응용 프로그램은 전체 SAP 배포 환경의 일부를 구성하며 역시 Azure Site Recovery로 보호되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-143">Other applications such as non-NetWeaver SAP applications and non-SAP applications form part of the overall SAP deployment environment and should also be protected with Azure Site Recovery.</span></span>

## <a name="replicate-virtual-machines"></a><span data-ttu-id="6c441-144">가상 컴퓨터 복제</span><span class="sxs-lookup"><span data-stu-id="6c441-144">Replicate virtual machines</span></span>
<span data-ttu-id="6c441-145">[이 지침](azure-to-azure-walkthrough-enable-replication.md)에 따라 모든 SAP 응용 프로그램 가상 컴퓨터를 Azure DR 데이터 센터로 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-145">Follow [this guidance](azure-to-azure-walkthrough-enable-replication.md) to start replicating all the SAP application virtual machines to the Azure DR datacenter.</span></span>

<span data-ttu-id="6c441-146">고정 IP를 사용하는 경우 계산 및 네트워크 설정의 네트워크 인터페이스 카드 섹션에서 가상 컴퓨터가 사용할 IP를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-146">If you are using a static IP, you can specify the IP that you want the virtual machine to take in the Network interface cards section in Compute and Network settings.</span></span>

![대상 IP](./media/site-recovery-sap/sap-static-ip.png)


## <a name="creating-a-recovery-plan"></a><span data-ttu-id="6c441-148">복구 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="6c441-148">Creating a recovery plan</span></span>
<span data-ttu-id="6c441-149">복구 계획을 사용하면 다중 계층 응용 프로그램에서 다양한 계층의 장애 조치를 시퀀싱하여 응용 프로그램의 일관성을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-149">A recovery plan allows sequencing the failover of various tiers in a multi-tier application, hence, maintaining application consistency.</span></span> <span data-ttu-id="6c441-150">다중 계층 웹 응용 프로그램에 대한 복구 계획을 만드는 동안 [여기](site-recovery-create-recovery-plans.md)서 설명한 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-150">Follow the steps described [here](site-recovery-create-recovery-plans.md) while creating a recovery plan for a multi-tier web application.</span></span>

### <a name="adding-scripts-to-the-recovery-plan"></a><span data-ttu-id="6c441-151">복구 계획에 스크립트 추가</span><span class="sxs-lookup"><span data-stu-id="6c441-151">Adding scripts to the recovery plan</span></span>
<span data-ttu-id="6c441-152">장애 조치/테스트 장애 조치 후에 응용 프로그램이 올바르게 작동하도록 Azure 가상 컴퓨터에서 일부 작업을 수행해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-152">You may need to do some operations on the Azure virtual machines post failover/test failover for your applications to function correctly.</span></span> <span data-ttu-id="6c441-153">[이 문서](site-recovery-create-recovery-plans.md#add-scripts)에서 설명한 대로 복구 계획에서 해당 스크립트를 추가하여 DNS 항목 업데이트, 바인딩 및 연결 변경 등과 같은 사후 장애 조치 작업을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-153">You can automate the post failover operation such as updating DNS entry, and changing bindings and connections, by adding corresponding scripts in the recovery plan as described in [this article](site-recovery-create-recovery-plans.md#add-scripts).</span></span>

### <a name="dns-update"></a><span data-ttu-id="6c441-154">DNS 업데이트</span><span class="sxs-lookup"><span data-stu-id="6c441-154">DNS update</span></span>
<span data-ttu-id="6c441-155">DNS가 동적 DNS 업데이트를 위해 구성된 경우 일반적으로 가상 컴퓨터를 시작할 때 새 IP로 DNS를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-155">If the DNS is configured for dynamic DNS update, then virtual machines usually update the DNS with the new IP once they start.</span></span> <span data-ttu-id="6c441-156">가상 컴퓨터의 새 IP로 DNS를 업데이트하는 명시적인 단계를 추가하려면 복구 계획 그룹의 사후 작업으로 [DNS의 IP를 업데이트하는 스크립트](https://aka.ms/asr-dns-update)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-156">If you want to add an explicit step to update DNS with the new IPs of the virtual machines then add this [script to update IP in DNS](https://aka.ms/asr-dns-update) as a post action on recovery plan groups.</span></span>  

## <a name="example-azure-to-azure-deployment"></a><span data-ttu-id="6c441-157">Azure-Azure 배포 예제</span><span class="sxs-lookup"><span data-stu-id="6c441-157">Example Azure-to-Azure deployment</span></span>
<span data-ttu-id="6c441-158">다음 다이어그램에서는 Azure Site Recovery Azure-Azure DR 시나리오를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-158">In the diagram below the Azure Site Recovery Azure-to-Azure DR scenario is depicted:</span></span>
* <span data-ttu-id="6c441-159">기본 데이터 센터는 싱가포르에 있으며(Azure 동남아시아) DR 데이터 센터는 홍콩입니다(Azure 동아시아).</span><span class="sxs-lookup"><span data-stu-id="6c441-159">The Primary Datacenter is in Singapore (Azure South-East Asia) and the DR datacenter is Hong Kong (Azure East Asia).</span></span>  <span data-ttu-id="6c441-160">이 시나리오에서는 싱가포르에서 동기 모드로 SQL Server AlwaysOn을 실행하는 두 VM을 통해 로컬 고가용성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-160">In this scenario, local High Availability is provided by having two VMs running SQL Server AlwaysOn in Synchronous mode in Singapore.</span></span>
* <span data-ttu-id="6c441-161">파일 공유 ASCS를 사용하여 SAP 단일 실패 지점에서 HA를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-161">The File Share ASCS can be used to provide HA for the SAP single points of failure.</span></span> <span data-ttu-id="6c441-162">파일 공유 ASCS에는 클러스터 공유 디스크가 필요하지 않으며 SIOS 같은 응용 프로그램이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-162">File Share ASCS does not require a cluster shared disk, and applications such as SIOS are not required.</span></span>
* <span data-ttu-id="6c441-163">DBMS 계층에 대한 DR 보호는 비동기 복제를 통해 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-163">DR protection for the DBMS layer is achieved using Asynchronous replication.</span></span>
* <span data-ttu-id="6c441-164">이 시나리오에서는 프로덕션의 정확한 복제본인 DR 솔루션을 설명하는 용어인 “대칭 DR”을 나타내므로 DR SQL Server 솔루션에 로컬 고가용성이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-164">This scenario shows “symmetrical DR” – a term used to describe a DR solution that is an exact replica of production, therefore the DR SQL Server solution has local High Availability.</span></span> <span data-ttu-id="6c441-165">데이터베이스 계층에 대칭 DR을 반드시 사용해야 하는 것은 아니며 많은 고객들은 클라우드 배포의 유연성을 활용하여 DR 이벤트 후 신속히 로컬 고가용성 노드를 구축합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-165">The use of symmetrical DR is not mandatory for the Database layer, and many customers leverage the flexibility of cloud deployments to build a local High Availability Node quickly after a DR event.</span></span>
* <span data-ttu-id="6c441-166">이 다이어그램에서는 Azure Site Recovery를 통해 복제된 응용 프로그램 서버 계층과 SAP NetWeaver ASCS를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-166">The diagram depicts the SAP NetWeaver ASCS and Application server layer replicated by Azure Site Recovery.</span></span>

![복제 시나리오](./media/site-recovery-sap/sap-replication-scenario.png)

## <a name="doing-a-test-failover"></a><span data-ttu-id="6c441-168">테스트 장애 조치 수행</span><span class="sxs-lookup"><span data-stu-id="6c441-168">Doing a test failover</span></span>
<span data-ttu-id="6c441-169">[이 지침](azure-to-azure-walkthrough-test-failover.md)에 따라 테스트 장애 조치를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-169">Follow [this guidance](azure-to-azure-walkthrough-test-failover.md) to do a test failover.</span></span>

1.  <span data-ttu-id="6c441-170">Azure Portal로 이동하여 Recovery Services 자격 증명 모음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-170">Go to Azure portal and select your Recovery Services vault.</span></span>
2.  <span data-ttu-id="6c441-171">SAP 응용 프로그램에 대한 복구 계획을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-171">Click on the recovery plan created for SAP applications(s).</span></span>
3.  <span data-ttu-id="6c441-172">'테스트 장애 조치'를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-172">Click on 'Test Failover'.</span></span>
4.  <span data-ttu-id="6c441-173">복구 지점 및 Azure 가상 네트워크를 선택하여 테스트 장애 조치 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-173">Select recovery point and Azure virtual network to start the test failover process.</span></span>
5.  <span data-ttu-id="6c441-174">보조 환경이 가동 중이면 유효성 검사를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-174">Once the secondary environment is up, you can perform your validations.</span></span>
6.  <span data-ttu-id="6c441-175">유효성 검사가 완료되면 '테스트 장애 조치 정리'를 클릭하고 장애 조치 환경을 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-175">Once the validations are complete, click on ‘Cleanup test failover’ and to clean the failover environment.</span></span>

## <a name="doing-a-failover"></a><span data-ttu-id="6c441-176">장애 조치 수행</span><span class="sxs-lookup"><span data-stu-id="6c441-176">Doing a failover</span></span>
<span data-ttu-id="6c441-177">장애 조치를 수행할 때 [이 지침](site-recovery-failover.md)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-177">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

1.  <span data-ttu-id="6c441-178">Azure Portal로 이동하여 Recovery Services 자격 증명 모음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-178">Go to Azure portal and select your Recovery Services vault.</span></span>
2.  <span data-ttu-id="6c441-179">SAP 응용 프로그램에 대해 만든 복구 계획을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-179">Click on the recovery plan created for SAP application(s).</span></span>
3.  <span data-ttu-id="6c441-180">'장애 조치'를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-180">Click on 'Failover'.</span></span>
4.  <span data-ttu-id="6c441-181">복구 지점을 선택하여 장애 조치 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-181">Select recovery point to start the failover process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c441-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6c441-182">Next steps</span></span>
<span data-ttu-id="6c441-183">[이 백서](http://aka.ms/asr-sap)에서는 Azure Site Recovery를 사용한 SAP NetWeaver 배포에서의 재해 복구 솔루션 구축에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-183">Learn more about building a disaster recovery solution for SAP NetWeaver deployments using Azure Site Recovery in [this whitepaper](http://aka.ms/asr-sap).</span></span> <span data-ttu-id="6c441-184">또한 다양한 SAP 아키텍처의 권장 사항에 대해 설명하고, Azure의 SAP에서 지원되는 응용 프로그램 및 VM 유형을 나열하며, 재해 복구 솔루션에서 가능한 테스트 계획에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-184">The whitepaper also discusses recommendations for different SAP architectures, lists supported applications and VM types for SAP on Azure, and describes possible testing plans for your disaster recovery solution.</span></span>

<span data-ttu-id="6c441-185">Site Recovery를 사용하여 [다른 워크로드를 복제](site-recovery-workload.md)하는 것에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6c441-185">Learn more about [replicating other workloads](site-recovery-workload.md) using Site Recovery.</span></span>
