---
title: "(대형 인스턴스) Azure에서 SAP HANA의 aaaHigh 고가용성 및 재해 복구 | Microsoft Docs"
description: "Azure(큰 인스턴스)의 SAP HANA에 대한 고가용성을 달성하고 및 재해 복구를 계획합니다."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0c0967f54cf29bbb275eb7cda9d36608488add9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-high-availability-and-disaster-recovery-on-azure"></a><span data-ttu-id="9320c-103">Azure(큰 인스턴스)의 SAP HANA 고가용성 및 재해 복구</span><span class="sxs-lookup"><span data-stu-id="9320c-103">SAP HANA (large instances) high availability and disaster recovery on Azure</span></span> 

<span data-ttu-id="9320c-104">Azure(큰 인스턴스) 서버에서 업무상 중요한 SAP HANA를 실행할 때 고가용성 및 재해 복구는 중요한 측면입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-104">High availability and disaster recovery are important aspects of running your mission-critical SAP HANA on Azure (large instances) servers.</span></span> <span data-ttu-id="9320c-105">중요 한 toowork sap, 시스템 통합 업체 또는 Microsoft tooproperly 설계자와 구현 hello 오른쪽 우선-가용성/재해 복구 전략입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-105">It's important toowork with SAP, your system integrator, or Microsoft tooproperly architect and implement hello right high-availability/disaster-recovery strategy.</span></span> <span data-ttu-id="9320c-106">중요 한 tooconsider hello 복구 지점 목표 및 복구 시간 목표를 특정 tooyour 환경 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-106">It is also important tooconsider hello recovery point objective and recovery time objective, which are specific tooyour environment.</span></span>

## <a name="high-availability"></a><span data-ttu-id="9320c-107">고가용성</span><span class="sxs-lookup"><span data-stu-id="9320c-107">High availability</span></span>

<span data-ttu-id="9320c-108">Microsoft는 포함 하는 SAP HANA 고가용성 방법을 "hello 상자 부족"를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-108">Microsoft supports SAP HANA high-availability methods "out of hello box," which include:</span></span>

- <span data-ttu-id="9320c-109">**저장소 복제:** hello 기능 tooreplicate 저장소 시스템의 모든 데이터 tooanother 위치 (내에서 또는 별도의 hello 동일한 데이터 센터).</span><span class="sxs-lookup"><span data-stu-id="9320c-109">**Storage replication:** hello storage system's ability tooreplicate all data tooanother location (within, or separate from, hello same datacenter).</span></span> <span data-ttu-id="9320c-110">SAP HANA는 이 메서드와 독립적으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-110">SAP HANA operates independently of this method.</span></span>
- <span data-ttu-id="9320c-111">**HANA 시스템 복제:** SAP HANA tooa 별도 SAP HANA 시스템의 모든 데이터의 복제 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-111">**HANA system replication:** hello replication of all data in SAP HANA tooa separate SAP HANA system.</span></span> <span data-ttu-id="9320c-112">hello 복구 시간 목표는 정기적으로 데이터 복제를 통해 최소화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-112">hello recovery time objective is minimized through data replication at regular intervals.</span></span> <span data-ttu-id="9320c-113">비동기, 동기 메모리 내 및 동기 모드를 지원 하는 SAP HANA (SAP HANA에만 권장 시스템 내에 있는 동일한 데이터 센터 또는 보다 작거나 100 KM 떨어져 있는 hello).</span><span class="sxs-lookup"><span data-stu-id="9320c-113">SAP HANA supports asynchronous, synchronous in-memory, and synchronous modes (recommended only for SAP HANA systems that are within hello same datacenter or less than 100 KM apart).</span></span> <span data-ttu-id="9320c-114">현재 디자인 HANA 큰 인스턴스 스탬프의 hello에서는 고가용성만 HANA 시스템 복제를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-114">In hello current design of HANA large-instance stamps, HANA system replication can be used for high availability only.</span></span>
- <span data-ttu-id="9320c-115">**자동 장애 조치 호스트:** 대체 toosystem 복제로 로컬 오류 복구 솔루션 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-115">**Host auto-failover:** A local fault-recovery solution toouse as an alternative toosystem replication.</span></span> <span data-ttu-id="9320c-116">Hello 마스터 노드를 사용할 수 없을 때 SAP HANA tooanother 노드를 통해 자동으로 장애 및 하나 이상의 대기 SAP HANA 노드 확장 모드에서 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-116">When hello master node becomes unavailable, one or more standby SAP HANA nodes are configured in scale-out mode and SAP HANA automatically fails over tooanother node.</span></span>

<span data-ttu-id="9320c-117">SAP HANA 고가용성에 대 한 자세한 내용은 다음 SAP 정보 hello를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="9320c-117">For more information on SAP HANA high availability, see hello following SAP information:</span></span>

- [<span data-ttu-id="9320c-118">SAP HANA 고가용성 백서</span><span class="sxs-lookup"><span data-stu-id="9320c-118">SAP HANA High-Availability Whitepaper</span></span>](http://go.sap.com/documents/2016/05/f8e5eeba-737c-0010-82c7-eda71af511fa.html)
- [<span data-ttu-id="9320c-119">SAP HANA 관리 가이드</span><span class="sxs-lookup"><span data-stu-id="9320c-119">SAP HANA Administration Guide</span></span>](http://help.sap.com/hana/SAP_HANA_Administration_Guide_en.pdf)
- [<span data-ttu-id="9320c-120">SAP HANA 시스템 복제에 대한 SAP Academy 비디오</span><span class="sxs-lookup"><span data-stu-id="9320c-120">SAP Academy Video on SAP HANA System Replication</span></span>](http://scn.sap.com/community/hana-in-memory/blog/2015/05/19/sap-hana-system-replication)
- [<span data-ttu-id="9320c-121">SAP 지원 참고 사항 #1999880 – SAP HANA 시스템 복제에 대한 FAQ</span><span class="sxs-lookup"><span data-stu-id="9320c-121">SAP Support Note #1999880 – FAQ on SAP HANA System Replication</span></span>](https://bcs.wdf.sap.corp/sap/support/notes/1999880)
- <span data-ttu-id="9320c-122">[SAP 지원 참고 사항 #2165547 – SAP HANA 시스템 복제 환경 내의 SAP HANA 백업 및 복원](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3231363535343726)</span><span class="sxs-lookup"><span data-stu-id="9320c-122">[SAP Support Note #2165547 – SAP HANA Backup and Restore within SAP HANA System Replication Environment](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3231363535343726)</span></span>
- <span data-ttu-id="9320c-123">[SAP 지원 참고 사항 #1984882 – 가동 중지 시간이 최소/없는 하드웨어 Exchange에 대한 SAP HANA 시스템 복제 사용](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3139383438383226)</span><span class="sxs-lookup"><span data-stu-id="9320c-123">[SAP Support Note #1984882 – Using SAP HANA System Replication for Hardware Exchange with Minimum/Zero Downtime](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3139383438383226)</span></span>

## <a name="disaster-recovery"></a><span data-ttu-id="9320c-124">재해 복구</span><span class="sxs-lookup"><span data-stu-id="9320c-124">Disaster recovery</span></span>

<span data-ttu-id="9320c-125">Azure(큰 인스턴스)의 SAP HANA가 지역 정책 지역에 있는 여러 Azure 지역에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-125">SAP HANA on Azure (large instances) is offered in two Azure regions in a geopolitical region.</span></span> <span data-ttu-id="9320c-126">두 개의 서로 다른 지역에 대 한 두 개의 큰 인스턴스 스탬프 hello 사이 재해 복구 시 데이터를 복제에 대 한 네트워크에 직접 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-126">Between hello two large-instance stamps of two different regions is a direct network connectivity for replicating data during disaster recovery.</span></span> <span data-ttu-id="9320c-127">hello 데이터의 hello 복제는 저장소 인프라를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-127">hello replication of hello data is storage-infrastructure based.</span></span> <span data-ttu-id="9320c-128">기본적으로 hello 복제 수행 되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-128">hello replication is not done by default.</span></span> <span data-ttu-id="9320c-129">Hello 재해 복구를 정렬 하는 hello 고객 구성에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-129">It is done for hello customer configurations that ordered hello disaster recovery.</span></span> <span data-ttu-id="9320c-130">Hello 현재 디자인 재해 복구를 위해 HANA 시스템 복제를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-130">In hello current design, HANA system replication can't be used for disaster recovery.</span></span>

<span data-ttu-id="9320c-131">그러나 tootake 이점은 toostart toodesign hello 네트워크 연결 toohello 두 개의 서로 다른 Azure 지역 hello 재해 복구 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-131">However, tootake advantage of hello disaster recovery, you need toostart toodesign hello network connectivity toohello two different Azure regions.</span></span> <span data-ttu-id="9320c-132">toodo, 주요 Azure 지역이 및 온-프레미스 tooyour 재해 복구 지역에서 다른 회로 연결에 온-프레미스에서 Azure express 경로 회로 연결을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-132">toodo so, you need an Azure ExpressRoute circuit connection from on-premises in your main Azure region and another circuit connection from on-premises tooyour disaster-recovery region.</span></span> <span data-ttu-id="9320c-133">이러한 측정값은 MSEE(Microsoft Enterprise Edge 라우터) 위치를 포함하는 전체 Azure 지역에 문제가 발생한 상황에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-133">This measure would cover a situation in which a complete Azure region, including a Microsoft enterprise edge router (MSEE) location, has an issue.</span></span>

<span data-ttu-id="9320c-134">두 번째 측정값으로 이러한 ExpressRoute 회로의 hello 영역 tooboth 중 하나에 tooSAP HANA Azure (대형 인스턴스)에 연결 하는 모든 Azure 가상 네트워크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-134">As a second measure, you can connect all Azure virtual networks that connect tooSAP HANA on Azure (large instances) in one of hello regions tooboth of those ExpressRoute circuits.</span></span> <span data-ttu-id="9320c-135">사용 안 함 흐름 방향은 하나만 hello MSEE 위치 Azure와 온-프레미스 위치를 연결 하는 경우가이 측정값을 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-135">This measure addresses a case where only one of hello MSEE locations that connects your on-premises location with Azure goes off duty.</span></span>

<span data-ttu-id="9320c-136">hello 다음 그림과 hello 재해 복구를 위한 최적의 구성:</span><span class="sxs-lookup"><span data-stu-id="9320c-136">hello following figure shows hello optimal configuration for disaster recovery:</span></span>

![재해 복구에 대한 최적의 구성](./media/hana-overview-high-availability-disaster-recovery/image1-optimal-configuration.png)

<span data-ttu-id="9320c-138">hello 최적의 사례 hello 네트워크의 재해 복구 구성에 대 한는 온-프레미스 toohello 두 개의 서로 다른 Azure 지역에서 두 개의 ExpressRoute 회로 toohave입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-138">hello optimal case for a disaster-recovery configuration of hello network is toohave two ExpressRoute circuits from on-premises toohello two different Azure regions.</span></span> <span data-ttu-id="9320c-139">하나의 회로 이동 tooregion #1 프로덕션 인스턴스를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-139">One circuit goes tooregion #1, running a production instance.</span></span> <span data-ttu-id="9320c-140">ExpressRoute 회로 두 번째 hello tooregion # 2를 실행 중인 일부 비-프로덕션 HANA 인스턴스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-140">hello second ExpressRoute circuit goes tooregion #2, running some non-production HANA instances.</span></span> <span data-ttu-id="9320c-141">(이 hello 눈금 MSEE hello 및 큰 인스턴스 스탬프를 포함 하는 전체 Azure 지역 중 중요 합니다.)</span><span class="sxs-lookup"><span data-stu-id="9320c-141">(This is important if an entire Azure region, including hello MSEE and large-instance stamp, goes off hello grid.)</span></span>

<span data-ttu-id="9320c-142">두 번째 측정값으로 hello 다양 한 가상 네트워크는 연결 된 toohello 연결된 tooSAP HANA Azure (대형 인스턴스)에 있는 다양 한 express 경로 회로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-142">As a second measure, hello various virtual networks are connected toohello various ExpressRoute circuits that are connected tooSAP HANA on Azure (large instances).</span></span> <span data-ttu-id="9320c-143">나중에 설명 된 대로 MSEE, 실패 또는 재해 복구에 대 한 hello 복구 지점 목표를 낮출 수 hello 위치를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-143">You can bypass hello location where an MSEE is failing, or you can lower hello recovery point objective for disaster recovery, as we discuss later.</span></span>

<span data-ttu-id="9320c-144">에 재해 복구 설치에 대 한 hello 다음 요구 사항:</span><span class="sxs-lookup"><span data-stu-id="9320c-144">hello next requirements for a disaster-recovery setup are:</span></span>

- <span data-ttu-id="9320c-145">hello Sku 프로덕션으로 크기를 동일 하 고 hello 재해 복구 지역에 배포 합니다 (대형 인스턴스) Azure Sku에서 SAP HANA를 주문 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-145">You must order SAP HANA on Azure (large instances) SKUs of hello same size as your production SKUs and deploy them in hello disaster-recovery region.</span></span> <span data-ttu-id="9320c-146">이러한 인스턴스를 사용 하는 toorun 테스트, 샌드박스 또는 QA HANA 인스턴스 수입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-146">These instances can be used toorun test, sandbox, or QA HANA instances.</span></span>
- <span data-ttu-id="9320c-147">순서 지정 해야 재해 복구 프로필 각각의 Sku (대형 인스턴스) Azure에서 SAP HANA 프로그램에 대 한 원하는 toorecover hello 재해 복구 사이트에서 필요한 경우.</span><span class="sxs-lookup"><span data-stu-id="9320c-147">You must order a disaster-recovery profile for each of your SAP HANA on Azure (large instances) SKUs that you want toorecover in hello disaster-recovery site, if necessary.</span></span> <span data-ttu-id="9320c-148">이 동작으로 인해 다시 toohello hello 재해 복구 영역에 프로덕션 지역에서 저장소 복제 hello의 hello 대상 저장소 볼륨을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-148">This action leads toohello allocation of storage volumes, which are hello target of hello storage replication from your production region into hello disaster-recovery region.</span></span>

<span data-ttu-id="9320c-149">Hello 앞에 요구 사항을 충족 시키면 책임 toostart hello 저장소 복제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-149">After you meet hello preceding requirements, it is your responsibility toostart hello storage replication.</span></span> <span data-ttu-id="9320c-150">Hello 저장소 인프라 (대형 인스턴스) Azure에서 SAP HANA에 사용 되는 저장소 복제의 hello 기반 저장소 스냅숏을입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-150">In hello storage infrastructure used for SAP HANA on Azure (large instances), hello basis of storage replication is storage snapshots.</span></span> <span data-ttu-id="9320c-151">toostart hello 재해 복구 복제 tooperform이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-151">toostart hello disaster-recovery replication, you need tooperform:</span></span>

- <span data-ttu-id="9320c-152">앞서 설명한 대로 부팅 LUN의 스냅숏</span><span class="sxs-lookup"><span data-stu-id="9320c-152">A snapshot of your boot LUN, as described earlier.</span></span>
- <span data-ttu-id="9320c-153">앞서 설명한 대로 HANA 관련 볼륨의 스냅숏</span><span class="sxs-lookup"><span data-stu-id="9320c-153">A snapshot of your HANA-related volumes, as described earlier.</span></span>

<span data-ttu-id="9320c-154">이러한 스냅숏을 실행 하 고 나면 hello 볼륨의 초기 복제본 hello 재해 복구 지역에서 재해 복구 프로필 연관 된 hello 볼륨에 마련 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-154">After you execute these snapshots, an initial replica of hello volumes is seeded on hello volumes that are associated with your disaster-recovery profile in hello disaster-recovery region.</span></span>

<span data-ttu-id="9320c-155">Hello 가장 최근의 저장소 스냅숏이 1 시간 마다 사용 이후에 tooreplicate hello 델타 hello 저장소 볼륨을 개발 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-155">Subsequently, hello most recent storage snapshot is used every hour tooreplicate hello deltas that develop on hello storage volumes.</span></span>

<span data-ttu-id="9320c-156">이 구성을 지원 hello 복구 지점 목표 60 too90 분에서입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-156">hello recovery point objective that's achieved with this configuration is from 60 too90 minutes.</span></span> <span data-ttu-id="9320c-157">tooachieve 더 빠른 복구 지점 목표 hello 재해 복구 경우 복사 hello HANA에서 트랜잭션 로그 백업에서 SAP HANA toohello Azure (대형 인스턴스)를 다른 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-157">tooachieve a better recovery point objective in hello disaster-recovery case, copy hello HANA transaction log backups from SAP HANA on Azure (large instances) toohello other Azure region.</span></span> <span data-ttu-id="9320c-158">tooachieve이 복구 지점 목표를 사용 하 여 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-158">tooachieve this recovery point objective, do hello following:</span></span>

1. <span data-ttu-id="9320c-159">Hello HANA 트랜잭션 로그를 백업 자주 가능한 너무/hana/로그/백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-159">Back up hello HANA transaction log as frequently as possible too/hana/log/backup.</span></span>
2. <span data-ttu-id="9320c-160">완성 된 tooan toohello SAP HANA (대형 인스턴스) Azure 서버에 연결 된 가상 네트워크에 있는 Azure 가상 컴퓨터 (VM) 될 때 hello 트랜잭션 로그 백업을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-160">Copy hello transaction log backups when they are finished tooan Azure virtual machine (VM), which is in a virtual network that's connected toohello SAP HANA on Azure (large instances) server.</span></span>
3. <span data-ttu-id="9320c-161">해당 VM에서 hello 백업 tooa hello 재해 복구 지역에서 가상 네트워크에 있는 VM을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-161">From that VM, copy hello backup tooa VM that's in a virtual network in hello disaster-recovery region.</span></span>
4. <span data-ttu-id="9320c-162">Hello VM에서에서 해당 지역에서 hello 트랜잭션 로그 백업을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-162">Keep hello transaction log backups in that region in hello VM.</span></span>

<span data-ttu-id="9320c-163">재해가 발생할 경우 재해 복구 프로필 hello 실제 서버에 배포한 후 hello 트랜잭션 로그 백업을 복사 hello VM toohello Azure (대형 인스턴스)는 이제 hello hello 재해 복구 영역에 주 서버에서 SAP HANA에서에서 및 이러한 백업을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-163">In case of disaster, after hello disaster-recovery profile has been deployed on an actual server, copy hello transaction log backups from hello VM toohello SAP HANA on Azure (large instances) that is now hello primary server in hello disaster-recovery region, and restore those backups.</span></span> <span data-ttu-id="9320c-164">이 복구가 없기 때문에 hello HANA hello 재해 복구 디스크 상태가 HANA 스냅숏 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-164">This recovery is possible because hello state of HANA on hello disaster-recovery disks is that of a HANA snapshot.</span></span> <span data-ttu-id="9320c-165">추가 트랜잭션 로그 백업 복원에 대 한 hello 오프셋된 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-165">This is hello offset point for further restorations of transaction log backups.</span></span>

## <a name="backup-and-restore"></a><span data-ttu-id="9320c-166">백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="9320c-166">Backup and restore</span></span>

<span data-ttu-id="9320c-167">Hello 가장 중요 한 측면 toooperating 데이터베이스 중 하나 있는지 확인 하에서 다양 한 치명적인 이벤트 hello 데이터베이스를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-167">One of hello most important aspects toooperating databases is making sure hello database can be protected from various catastrophic events.</span></span> <span data-ttu-id="9320c-168">자연 재해 toosimple 사용자 오류 로부터 이러한 이벤트는 아무것도 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-168">These events can be caused by anything from natural disasters toosimple user errors.</span></span>

<span data-ttu-id="9320c-169">데이터베이스 데이터베이스 hello 기능 toorestore 것 tooany 지점에서에서 백업 시간 (같은 누군가가 중요 한 데이터를 삭제 하기 전에), 허용 가능한 toohello 방식으로 hello 중단이 발생 한 하기 전의 가까운 복원 tooa 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-169">Backing up a database, with hello ability toorestore it tooany point in time (such as before somebody deleted critical data), allows restoration tooa state that is as close as possible toohello way it was before hello disruption occurred.</span></span>

<span data-ttu-id="9320c-170">최상의 결과를 위해 두 가지 백업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-170">Two types of backups must be performed for best results:</span></span>

- <span data-ttu-id="9320c-171">데이터베이스 백업</span><span class="sxs-lookup"><span data-stu-id="9320c-171">Database backups</span></span>
- <span data-ttu-id="9320c-172">트랜잭션 로그 백업</span><span class="sxs-lookup"><span data-stu-id="9320c-172">Transaction log backups</span></span>

<span data-ttu-id="9320c-173">또한 응용 프로그램 수준에서 수행 toofull 데이터베이스 백업과 할 수 있습니다 더욱 철저 한 저장소 스냅숏과 함께 백업을 수행 하 여.</span><span class="sxs-lookup"><span data-stu-id="9320c-173">In addition toofull database backups performed at an application-level, you can be even more thorough by performing backups with storage snapshots.</span></span> <span data-ttu-id="9320c-174">로그 백업을 수행 hello 데이터베이스 (및 이미 커밋된 트랜잭션에서 tooempty hello 로그) 복원을 위해 중요 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-174">Performing log backups is also important for restoring hello database (and tooempty hello logs from already committed transactions).</span></span>

<span data-ttu-id="9320c-175">Azure(큰 인스턴스)의 SAP HANA는 다음과 같은 두 개의 백업과 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-175">SAP HANA on Azure (large instances) offers two backup and restore options:</span></span>

- <span data-ttu-id="9320c-176">DIY(Do It Yourself)</span><span class="sxs-lookup"><span data-stu-id="9320c-176">Do it yourself (DIY).</span></span> <span data-ttu-id="9320c-177">Tooensure 충분 한 디스크 공간을 계산한 후 디스크 백업 방법 (toothose 디스크)를 사용 하 여 전체 데이터베이스 및 로그 백업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-177">After you calculate tooensure enough disk space, perform full database and log backups by using disk backup methods (toothose disks).</span></span> <span data-ttu-id="9320c-178">시간이 지남에 따라 hello 백업은 복사한 tooan Azure 저장소 계정 (설정한 후 거의 무제한 저장을 사용 하는 Azure 기반 파일 서버) 또는 Azure 백업 자격 증명 모음 또는 Azure 콜드 저장소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-178">Over time, hello backups are copied tooan Azure storage account (after you set up an Azure-based file server with virtually unlimited storage), or use an Azure Backup vault or Azure cold storage.</span></span> <span data-ttu-id="9320c-179">다른 방법은 Commvault, toostore hello 백업을 한 후 복사 tooa 저장소 계정 등 toouse 제 3 자 데이터 보호 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-179">Another option is toouse a third-party data protection tool, such as Commvault, toostore hello backups after they are copied tooa storage account.</span></span> <span data-ttu-id="9320c-180">백업 옵션 DIY hello toobe 준수 및 감사 목적에 대 한 장기간 저장 해야 하는 데이터에 필요한 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-180">hello DIY backup option might also be necessary for data that needs toobe stored for longer periods for compliancy and auditing purposes.</span></span>
- <span data-ttu-id="9320c-181">Hello 백업을 사용 하 고 복원 hello (대형 인스턴스) Azure에서 SAP HANA의 기본 인프라 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-181">Use hello backup and restore functionality that hello underlying infrastructure of SAP HANA on Azure (large instances) provides.</span></span> <span data-ttu-id="9320c-182">이 옵션 백업에 대 한 hello 요구를 충족 하 고 수동 백업을 (여기서 데이터 백업을 규정 준수를 위해 필요한)를 제외한 거의 사용 되지 않는입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-182">This option fulfills hello need for backups, and it makes manual backups nearly obsolete (except where data backups are required for compliance purposes).</span></span> <span data-ttu-id="9320c-183">이 섹션에서는 나머지 hello 백업 hello 및 HANA (대형 인스턴스)를 제공 하는 기능을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-183">hello rest of this section addresses hello backup and restore functionality that's offered with HANA (large instances).</span></span>

> [!NOTE]
> <span data-ttu-id="9320c-184">hello 스냅숏 기술 hello HANA (대형 인스턴스)의 기본 인프라에서 사용 되는 SAP HANA 스냅숏에 대 한 종속성을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-184">hello snapshot technology that is used by hello underlying infrastructure of HANA (large instances) has a dependency on SAP HANA snapshots.</span></span> <span data-ttu-id="9320c-185">SAP HANA 스냅숏은 SAP HANA 다중 테넌트 데이터베이스 컨테이너와 함께 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-185">SAP HANA snapshots do not work in conjunction with SAP HANA Multitenant Database Containers.</span></span> <span data-ttu-id="9320c-186">결과적으로, 이러한 방식의 백업 사용 하는 toodeploy SAP HANA 다중 테 넌 트 데이터베이스 컨테이너 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-186">As a result, this method of backup cannot be used toodeploy SAP HANA Multitenant Database Containers.</span></span>

### <a name="using-storage-snapshots-of-sap-hana-on-azure-large-instances"></a><span data-ttu-id="9320c-187">Azure(큰 인스턴스)의 SAP HANA 저장소 스냅숏 사용</span><span class="sxs-lookup"><span data-stu-id="9320c-187">Using storage snapshots of SAP HANA on Azure (large instances)</span></span>

<span data-ttu-id="9320c-188">hello 저장소 인프라 (대형 인스턴스) Azure에서 SAP HANA를 기본 볼륨의 저장소 스냅숏의 hello 개념을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-188">hello storage infrastructure underlying SAP HANA on Azure (large instances) supports hello notion of a storage snapshot of volumes.</span></span> <span data-ttu-id="9320c-189">다음 고려 사항 hello로 백업 및 특정 볼륨의 복원은 모두 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-189">Both backup and restoration of a particular volume are supported, with hello following considerations:</span></span>

- <span data-ttu-id="9320c-190">데이터베이스 백업 대신 저장소 볼륨 스냅숏을 자주 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-190">Instead of database backups, storage volume snapshots are taken on a frequent basis.</span></span>
- <span data-ttu-id="9320c-191">hello 저장소 스냅숏을 실행 하기 전에 hello 저장소 스냅숏 SAP HANA 스냅숏을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-191">hello storage snapshot initiates an SAP HANA snapshot before it executes hello storage snapshot.</span></span> <span data-ttu-id="9320c-192">이 SAP HANA 스냅숏에 hello 저장소 스냅숏의 복구 후 최종 로그 복원에 대 한 hello 설치 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-192">This SAP HANA snapshot is hello setup point for eventual log restorations after recovery of hello storage snapshot.</span></span>
- <span data-ttu-id="9320c-193">Hello 저장소 스냅숏이 성공적으로 실행 된 hello 지점에 hello SAP HANA 스냅숏이 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-193">At hello point where hello storage snapshot is executed successfully, hello SAP HANA snapshot is deleted.</span></span>
- <span data-ttu-id="9320c-194">로그 백업은 자주 수행 되며 Azure의 hello 로그 백업 볼륨에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-194">Log backups are taken frequently and stored in hello log backup volume or in Azure.</span></span>
- <span data-ttu-id="9320c-195">Hello 데이터베이스를 복원 해야 하는 경우 tooa 특정 지정 시간, 요청이 있는 Azure 서비스 관리 toorestore tooa tooMicrosoft Azure 지원 (프로덕션 작동 중단) 또는 SAP HANA 특정 저장소 (예를 들어 계획 된 복원 샌드박스 시스템의 스냅숏 tooits 원래 상태)입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-195">If hello database must be restored tooa certain point in time, a request is made tooMicrosoft Azure Support (production outage) or SAP HANA on Azure Service Management toorestore tooa certain storage snapshot (for example, a planned restoration of a sandbox system tooits original state).</span></span>
- <span data-ttu-id="9320c-196">hello SAP HANA hello 저장소 스냅숏에 포함 된 스냅숏이 실행 되 고 hello 저장소 스냅숏을 만든 후 저장 된 로그 백업 적용에 대 한 오프셋된 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-196">hello SAP HANA snapshot that's included in hello storage snapshot is an offset point for applying log backups that have been executed and stored after hello storage snapshot was taken.</span></span>
- <span data-ttu-id="9320c-197">이러한 로그 백업 하는 toorestore hello 데이터베이스 백 tooa 특정 지정 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-197">These log backups are taken toorestore hello database back tooa certain point in time.</span></span>

<span data-ttu-id="9320c-198">지정 하 여 hello 백업\_이름 hello 다음 볼륨의 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-198">Specifying hello backup\_name creates a snapshot of hello following volumes:</span></span>

- <span data-ttu-id="9320c-199">hana/data</span><span class="sxs-lookup"><span data-stu-id="9320c-199">hana/data</span></span>
- <span data-ttu-id="9320c-200">hana/log</span><span class="sxs-lookup"><span data-stu-id="9320c-200">hana/log</span></span>
- <span data-ttu-id="9320c-201">hana/log\_backup(hana/log에 백업으로 탑재됨)</span><span class="sxs-lookup"><span data-stu-id="9320c-201">hana/log\_backup (mounted as backup into hana/log)</span></span>
- <span data-ttu-id="9320c-202">hana/shared</span><span class="sxs-lookup"><span data-stu-id="9320c-202">hana/shared</span></span>

### <a name="storage-snapshot-considerations"></a><span data-ttu-id="9320c-203">저장소 스냅숏 고려 사항</span><span class="sxs-lookup"><span data-stu-id="9320c-203">Storage snapshot considerations</span></span>

>[!NOTE]
><span data-ttu-id="9320c-204">추가 저장소 공간이 할당되어야 하기 때문에 저장소 스냅숏은 무료로 제공되지 _않습니다_.</span><span class="sxs-lookup"><span data-stu-id="9320c-204">Storage snapshots are _not_ provided free of charge, because additional storage space must be allocated.</span></span>

<span data-ttu-id="9320c-205">저장소에 대 한 스냅숏 (대형 인스턴스) Azure에서 SAP HANA hello 특정 메커니즘은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-205">hello specific mechanics of storage snapshots for SAP HANA on Azure (large instances) include:</span></span>

- <span data-ttu-id="9320c-206">(시점 hello에서 제외 될 때) 특정 저장소 스냅숏 매우 작은 저장소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-206">A specific storage snapshot (at hello point in time when it is taken) consumes very little storage.</span></span>
- <span data-ttu-id="9320c-207">데이터 변경 내용이 및 SAP HANA 데이터 hello 저장소 볼륨에서 파일 변경의 hello 콘텐츠에 hello 스냅숏 toostore hello 원래 블록 콘텐츠가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-207">As data content changes and hello content in SAP HANA data files change on hello storage volume, hello snapshot needs toostore hello original block content.</span></span>
- <span data-ttu-id="9320c-208">hello 저장소 스냅숏 크기가 늘어납니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-208">hello storage snapshot increases in size.</span></span> <span data-ttu-id="9320c-209">hello 긴 hello 스냅숏이 있는, hello 큰 hello 저장소 스냅숏 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-209">hello longer hello snapshot exists, hello larger hello storage snapshot becomes.</span></span>
- <span data-ttu-id="9320c-210">더 많은 변경 내용을 toohello SAP HANA 데이터베이스 볼륨의 저장소 스냅숏 hello 수명 주기 동안 hello, hello 저장소 스냅숏의 hello 큰 hello 공간 소비 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-210">hello more changes made toohello SAP HANA database volume over hello lifetime of a storage snapshot, hello larger hello space consumption of hello storage snapshot becomes.</span></span>

<span data-ttu-id="9320c-211">(대형 인스턴스) Azure에서 SAP HANA hello SAP HANA 데이터 및 로그 볼륨에 대 한 고정된 볼륨 크기 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-211">SAP HANA on Azure (large instances) comes with fixed volume sizes for hello SAP HANA data and log volume.</span></span> <span data-ttu-id="9320c-212">이러한 볼륨의 스냅숏을 수행를 볼륨 공간으로 무시 (내에서 SAP HANA [큰 인스턴스] Azure 프로세스에 hello)는 책임 tooschedule storage 스냅숏이 되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-212">Performing snapshots of those volumes eats into your volume space, so it is your responsibility tooschedule storage snapshots (within hello SAP HANA on Azure [large instances] process).</span></span>

<span data-ttu-id="9320c-213">hello 다음 섹션에서는 제공 일반적인 권장 사항을 비롯 한 이러한 스냅숏을 수행 하기 위한 정보:</span><span class="sxs-lookup"><span data-stu-id="9320c-213">hello following sections provide information for performing these snapshots, including general recommendations:</span></span>

- <span data-ttu-id="9320c-214">Hello 하드웨어 볼륨당 255 스냅숏을 유지할 수 있습니다, 경우에이 번호 보다 유지 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-214">Though hello hardware can sustain 255 snapshots per volume, we highly recommend that you stay well below this number.</span></span>
- <span data-ttu-id="9320c-215">스냅숏 저장소를 수행하기 전에 여유 공간을 모니터링하고 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-215">Before you perform storage snapshots, monitor and keep track of free space.</span></span>
- <span data-ttu-id="9320c-216">사용 가능한 공간에 따라 저장소 스냅숏 낮은 hello 수.</span><span class="sxs-lookup"><span data-stu-id="9320c-216">Lower hello number of storage snapshots based on free space.</span></span> <span data-ttu-id="9320c-217">를 유지 하는 스냅숏 toolower hello 수 하거나 tooextend hello 볼륨을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-217">You might need toolower hello number of snapshots that you keep, or you might need tooextend hello volumes.</span></span> <span data-ttu-id="9320c-218">(추가 저장소를 1TB 단위로 주문할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="9320c-218">(You can order additional storage in 1-TB units.)</span></span>
- <span data-ttu-id="9320c-219">시스템 마이그레이션 도구(R3load 또는 백업에서 SAP HANA 데이터베이스 복원)를 사용하여 SAP HANA에 데이터를 이동하는 것과 같은 작업 중에 저장소 스냅숏을 수행하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-219">During activities such as moving data into SAP HANA with system migration tools (with R3load, or by restoring SAP HANA databases from backups), we highly recommended that you not perform any storage snapshots.</span></span> <span data-ttu-id="9320c-220">(시스템 마이그레이션 새 SAP HANA 시스템에서 수행 중인 경우 저장소 스냅숏을 필요 하지 toobe 수행 합니다.)</span><span class="sxs-lookup"><span data-stu-id="9320c-220">(If a system migration is being done on a new SAP HANA system, storage snapshots would not need toobe performed.)</span></span>
- <span data-ttu-id="9320c-221">SAP HANA 테이블을 크게 재구성하는 동안 저장소 스냅숏을 가능하면 사용하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-221">During larger reorganizations of SAP HANA tables, storage snapshots should be avoided if possible.</span></span>
- <span data-ttu-id="9320c-222">저장소 스냅숏은 (대형 인스턴스) Azure에서 SAP HANA의 필수 구성 요소 tooengaging hello 재해 복구 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-222">Storage snapshots are a prerequisite tooengaging hello disaster-recovery capabilities of SAP HANA on Azure (large instances).</span></span>

### <a name="setting-up-storage-snapshots"></a><span data-ttu-id="9320c-223">저장소 스냅숏 설정</span><span class="sxs-lookup"><span data-stu-id="9320c-223">Setting up storage snapshots</span></span>

1. <span data-ttu-id="9320c-224">Perl hello HANA (대형 인스턴스) 서버의 hello Linux 운영 체제에 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-224">Make sure that Perl is installed in hello Linux operating system on hello HANA (large instances) server.</span></span>
2. <span data-ttu-id="9320c-225">수정/등/ssh/ssh\_config tooadd hello 줄 _Mac hmac sha1_합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-225">Modify /etc/ssh/ssh\_config tooadd hello line _MACs hmac-sha1_.</span></span>
3. <span data-ttu-id="9320c-226">SAP HANA 인스턴스마다 (있는 경우)를 실행 하는 hello 마스터 노드에서 SAP HANA backup 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-226">Create an SAP HANA backup user account on hello master node for each SAP HANA instance you are running (if applicable).</span></span>
4. <span data-ttu-id="9320c-227">SAP HANA HDB 클라이언트 hello 모든 SAP HANA (대형 인스턴스) 서버에 설치 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-227">hello SAP HANA HDB client must be installed on all SAP HANA (large instances) servers.</span></span>
5. <span data-ttu-id="9320c-228">Hello 첫 번째 SAP HANA (대형 인스턴스) 서버에서 각 영역의 공개 키 tooaccess hello 스냅숏 생성을 제어 하는 저장소 인프라를 기본 생성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-228">On hello first SAP HANA (large instances) server of each region, a public key must be created tooaccess hello underlying storage infrastructure that controls snapshot creation.</span></span>
6. <span data-ttu-id="9320c-229">Azure hello 스크립트 복사\_hana\_의 /scripts toohello 위치에서 backup.pl **hdbsql** 의 hello SAP HANA 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-229">Copy hello script azure\_hana\_backup.pl from /scripts toohello location of **hdbsql** of hello SAP HANA installation.</span></span>
7. <span data-ttu-id="9320c-230">동일한 /scripts toohello에서 복사 hello HANABackupDetails.txt 파일 Perl 스크립트 hello 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-230">Copy hello HANABackupDetails.txt file from /scripts toohello same location as hello Perl script.</span></span>
8. <span data-ttu-id="9320c-231">Hello 적절 한 고객 사양에 대 한 필요에 따라 hello HANABackupDetails.txt 파일을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-231">Modify hello HANABackupDetails.txt file as necessary for hello appropriate customer specifications.</span></span>

### <a name="step-1-install-sap-hana-hdbclient"></a><span data-ttu-id="9320c-232">1단계: SAP HANA HDBClient 설치</span><span class="sxs-lookup"><span data-stu-id="9320c-232">Step 1: Install SAP HANA HDBClient</span></span>

<span data-ttu-id="9320c-233">hello (대형 인스턴스) Azure에서 SAP HANA에 설치 된 Linux hello 폴더를 포함 및 백업 및 재해 복구를 위해 필요한 tooexecute SAP HANA storage 스냅숏의 스크립팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-233">hello Linux installed on SAP HANA on Azure (large instances) includes hello folders and scripts necessary tooexecute SAP HANA storage snapshots for backup and disaster-recovery purposes.</span></span> <span data-ttu-id="9320c-234">그러나 SAP HANA를 설치 하는 동안 프로그램 책임 tooinstall SAP HANA HDBclient 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-234">However, it is your responsibility tooinstall SAP HANA HDBclient while you are installing SAP HANA.</span></span> <span data-ttu-id="9320c-235">(Microsoft hello HDBclient 아니고 SAP HANA 설치합니다.)</span><span class="sxs-lookup"><span data-stu-id="9320c-235">(Microsoft installs neither hello HDBclient nor SAP HANA.)</span></span>

### <a name="step-2-change-etcsshsshconfig"></a><span data-ttu-id="9320c-236">2단계: /etc/ssh/ssh\_config 변경</span><span class="sxs-lookup"><span data-stu-id="9320c-236">Step 2: Change /etc/ssh/ssh\_config</span></span>

<span data-ttu-id="9320c-237">여기에 표시된 _MACs hmac-sha1_ 줄을 추가하여 /etc/ssh/ssh\_config를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-237">Change /etc/ssh/ssh\_config by adding _MACs hmac-sha1_ line as shown here:</span></span>
```
#   RhostsRSAAuthentication no
#   RSAAuthentication yes
#   PasswordAuthentication yes
#   HostbasedAuthentication no
#   GSSAPIAuthentication no
#   GSSAPIDelegateCredentials no
#   GSSAPIKeyExchange no
#   GSSAPITrustDNS no
#   BatchMode no
#   CheckHostIP yes
#   AddressFamily any
#   ConnectTimeout 0
#   StrictHostKeyChecking ask
#   IdentityFile ~/.ssh/identity
#   IdentityFile ~/.ssh/id_rsa
#   IdentityFile ~/.ssh/id_dsa
#   Port 22
Protocol 2
#   Cipher 3des
#   Ciphers aes128-ctr,aes192-ctr,aes256-ctr,arcfour256,arcfour128,aes128-cbc,3des-cbc
#   MACs hmac-md5,hmac-sha1,umac-64@openssh.com,hmac-ripemd160
MACs hmac-sha1
#   EscapeChar ~
#   Tunnel no
#   TunnelDevice any:any
#   PermitLocalCommand no
#   VisualHostKey no
#   ProxyCommand ssh -q -W %h:%p gateway.example.com
```

### <a name="step-3-create-a-public-key"></a><span data-ttu-id="9320c-238">3단계: 공개 키 만들기</span><span class="sxs-lookup"><span data-stu-id="9320c-238">Step 3: Create a public key</span></span>

<span data-ttu-id="9320c-239">Hello에 각 Azure 지역에서 Azure (대형 인스턴스) 서버에서 첫 번째 SAP HANA 스냅샷을 만들 수 있도록 사용 되는 공개 키 toobe tooaccess hello 저장소 인프라를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-239">On hello first SAP HANA on Azure (large instances) server in each Azure region, create a public key toobe used tooaccess hello storage infrastructure so that you can create snapshots.</span></span> <span data-ttu-id="9320c-240">hello 공개 키 암호 toohello 저장소에 필요한 toosign를 하면 암호 자격 증명이 유지 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-240">hello public key ensures that a password is not required toosign in toohello storage and that password credentials are not maintained.</span></span> <span data-ttu-id="9320c-241">Hello SAP HANA (대형 인스턴스) 서버에 Linux에서 다음 명령을 toogenerate hello에 대 한 공개 키 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-241">In Linux on hello SAP HANA (large instances) server, execute hello following command toogenerate hello public key:</span></span>
```
  ssh-keygen –t dsa –b 1024
```
<span data-ttu-id="9320c-242">hello 새 위치는 _/root/.ssh/id\_dsa.pub 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-242">hello new location is _/root/.ssh/id\_dsa.pub.</span></span> <span data-ttu-id="9320c-243">실제 암호를 입력 하지 마십시오. 그렇지 않으면 됩니다 필요 tooenter hello 암호에 로그인 할 때마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-243">Do not enter an actual passphrase, or else you will be required tooenter hello passphrase each time you sign in.</span></span> <span data-ttu-id="9320c-244">을 여러 번 **Enter** tooremove hello 두 번 입력 로그인에 대 한 암호 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-244">Instead, press **Enter** twice tooremove hello enter passphrase requirement for signing in.</span></span>

<span data-ttu-id="9320c-245">Toomake 고쳐지도록 해당 hello 공개 키가 too/root/.ssh/ 폴더를 변경 하 고 hello 다음 실행 하 여 예상 대로 확인 **ls** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-245">Check toomake sure that hello public key was corrected as expected by changing folders too/root/.ssh/ and then executing hello **ls** command.</span></span> <span data-ttu-id="9320c-246">Hello 키가 있는 경우에 hello 다음 명령을 실행 하 여 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-246">If hello key is present, you can copy it by running hello following command:</span></span>

![이 명령을 실행하여 공개 키를 복사합니다.](./media/hana-overview-high-availability-disaster-recovery/image2-public-key.png)

<span data-ttu-id="9320c-248">이 시점에서 Azure 서비스 관리에서 SAP HANA에 게 문의 하 고 hello 키를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-248">At this point, contact SAP HANA on Azure Service Management and provide hello key.</span></span> <span data-ttu-id="9320c-249">hello 서비스 담당자에 게 사용 하 여 hello 공개 키 tooregister hello 저장소 인프라를 내부에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-249">hello service representative uses hello public key tooregister it in hello underlying storage infrastructure.</span></span>

### <a name="step-4-create-an-sap-hana-user-account"></a><span data-ttu-id="9320c-250">4단계: SAP HANA 사용자 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="9320c-250">Step 4: Create an SAP HANA user account</span></span>

<span data-ttu-id="9320c-251">백업을 목적으로 SAP HANA Studio 내에서 SAP HANA 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-251">Create an SAP HANA user account within SAP HANA Studio for backup purposes.</span></span> <span data-ttu-id="9320c-252">이 계정에는 hello 다음 권한이 있어야 합니다.: _백업 관리자_ 및 _카탈로그 읽기_합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-252">This account must have hello following privileges: _Backup Admin_ and _Catalog Read_.</span></span> <span data-ttu-id="9320c-253">이 예제에서는 hello username SCADMIN 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-253">In this example, hello username SCADMIN is created.</span></span>

![HANA Studio에서 사용자 만들기](./media/hana-overview-high-availability-disaster-recovery/image3-creating-user.png)

### <a name="step-5-authorize-hello-sap-hana-user-account"></a><span data-ttu-id="9320c-255">5 단계: hello SAP HANA 사용자 계정에 권한을 부여합니다</span><span class="sxs-lookup"><span data-stu-id="9320c-255">Step 5: Authorize hello SAP HANA user account</span></span>

<span data-ttu-id="9320c-256">Hello SAP HANA 사용자 계정 (toobe hello 스크립트를 실행할 때마다 권한 부여를 요구 하지 않고 hello 스크립트에서 사용)에 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-256">Authorize hello SAP HANA user account (toobe used by hello scripts without requiring authorization every time hello script is run).</span></span> <span data-ttu-id="9320c-257">SAP HANA 명령 hello `hdbuserstore` hello 하나 이상의 SAP HANA 노드에 저장 되는 SAP HANA 사용자 키를 만들기를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-257">hello SAP HANA command `hdbuserstore` allows hello creation of an SAP HANA user key, which is stored on one or more SAP HANA nodes.</span></span> <span data-ttu-id="9320c-258">hello 사용자 키 hello 스크립팅 나중에 설명 하는 프로세스 내에서 toomanage 암호 필요 없이 hello 사용자 tooaccess를 SAP HANA를 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-258">hello user key also allows hello user tooaccess SAP HANA without having toomanage passwords from within hello scripting process that's discussed later.</span></span>

>[!IMPORTANT]
><span data-ttu-id="9320c-259">실행 hello 다음으로 명령을 `_root_`합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-259">Run hello following command as `_root_`.</span></span> <span data-ttu-id="9320c-260">그렇지 않으면 hello 스크립트는 제대로 작동 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-260">Otherwise, hello script cannot work properly.</span></span>

<span data-ttu-id="9320c-261">Hello 입력 `hdbuserstore` 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-261">Enter hello `hdbuserstore` command as follows:</span></span>

![Hello hdbuserstore 명령을 입력 합니다.](./media/hana-overview-high-availability-disaster-recovery/image4-hdbuserstore-command.png)

<span data-ttu-id="9320c-263">다음 예에서는 여기서 hello 사용자 SCADMIN01 이며 hello 호스트 이름이 lhanad01 hello hello 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-263">In hello following example, where hello user is SCADMIN01 and hello hostname is lhanad01, hello command is:</span></span>
```
hdbuserstore set SCADMIN01 lhanad01:30115 <backup username> <password>
```
<span data-ttu-id="9320c-264">확장 HANA 인스턴스의 단일 서버에서 모든 스크립트를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-264">Manage all scripting from a single server for scale-out HANA instances.</span></span> <span data-ttu-id="9320c-265">이 예에서 각 호스트는 키 관련된 toohello hello 호스트를 반영 하는 방식에 대해 SCADMIN01 hello SAP HANA 키를 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-265">In this example, hello SAP HANA key SCADMIN01 must be altered for each host in a way that reflects hello host that is related toohello key.</span></span> <span data-ttu-id="9320c-266">Hello HANA DB의 hello 인스턴스 번호를 사용 하 여 hello SAP HANA 백업 계정이 수정 하는, 즉 **lhanad**합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-266">That is, hello SAP HANA backup account is amended with hello instance number of hello HANA DB, **lhanad**.</span></span> <span data-ttu-id="9320c-267">hello 키 할당 된 hello 호스트에서 관리자 권한이 있어야 하 고 hello 확장에 대 한 백업 사용자 액세스 권한 tooall SAP HANA 인스턴스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-267">hello key must have administrative privileges on hello host it is assigned to, and hello backup user for scale-out must have access rights tooall SAP HANA instances.</span></span>
```
hdbuserstore set SCADMIN01 lhanad:30015 SCADMIN <password>
hdbuserstore set SCADMIN02 lhanad:30115 SCADMIN <password>
hdbuserstore set SCADMIN03 lhanad:30215 SCADMIN <password>
```

### <a name="step-6-copy-items-from-hello-scripts-folder"></a><span data-ttu-id="9320c-268">6 단계: hello /scripts 폴더에서 항목 복사</span><span class="sxs-lookup"><span data-stu-id="9320c-268">Step 6: Copy items from hello /scripts folder</span></span>

<span data-ttu-id="9320c-269">복사 hello 다음 hello에서 항목 을/폴더 (hello 설치의 hello 골드 이미지에 포함 됨) toohello 작업 디렉터리에 대 한 스크립트 **hdbsql**합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-269">Copy hello following items from hello /scripts folder (included on hello gold image of hello installation) toohello working directory for **hdbsql**.</span></span> <span data-ttu-id="9320c-270">현재 HANA 설치의 경우 이 디렉터리는 /hana/shared/D01/exe/linuxx86\_64/hdb입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-270">For current HANA installations, this directory is /hana/shared/D01/exe/linuxx86\_64/hdb.</span></span>
```
azure\_hana\_backup.pl
testHANAConnection.pl
testStorageSnapshotConnection.pl
removeTestStorageSnapshot.pl
HANABackupCustomerDetails.txt
```
<span data-ttu-id="9320c-271">OLAP 또는 hello 확장 실행 하는 경우 다음 항목을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-271">Copy hello following items if they are running scale-out or OLAP:</span></span>
```
azure\_hana\_backup\_bw.pl
testHANAConnectionBW.pl
testStorageSnapshotConnectionBW.pl
removeTestStorageSnapshotBW.pl
HANABackupCustomerDetailsBW.txt
```
<span data-ttu-id="9320c-272">hello HANABackupCustomerDetails.txt 파일이 확장 배포에 대 한 다음과 같이 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-272">hello HANABackupCustomerDetails.txt file is modifiable as follows for a scale-up deployment.</span></span> <span data-ttu-id="9320c-273">Hello storage 스냅숏을 실행 하는 hello 스크립트에 대 한 hello 컨트롤 및 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-273">It is hello control and configuration file for hello script that runs hello storage snapshots.</span></span> <span data-ttu-id="9320c-274">받았을 것 hello _저장소 백업 이름_ 및 _저장소 IP 주소_ 인스턴스에 배포 된 경우 Azure 서비스 관리에서 SAP HANA에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-274">You should have received hello _Storage Backup Name_ and _Storage IP Address_ from SAP HANA on Azure Service Management when your instances were deployed.</span></span> <span data-ttu-id="9320c-275">순서 지정 hello 시퀀스 수정할 수 없습니다 또는 hello 변수나 hello 스크립트의 모든 간격 제대로 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-275">You cannot modify hello sequence, ordering, or spacing of any of hello variables, or hello script does not run properly.</span></span>

<span data-ttu-id="9320c-276">확장 배포에 대 한 hello 구성 파일은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-276">For a scale-up deployment, hello configuration file would look like:</span></span>
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Created by customer using hdbuserstore
HANA Backup Name: SCADMIND01
```
<span data-ttu-id="9320c-277">확장 구성에 대 한 hello HANABackupCustomerDetailsBW.txt 파일은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-277">For a scale-out configuration, hello HANABackupCustomerDetailsBW.txt file would look like:</span></span>
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Node IP addresses, instance numbers, and HANA backup name
#provided by customer.  HANA backup name created using
#hdbuserstore utility.
Node 1 IP Address: 10.254.15.21
Node 1 HANA instance number: 01
Node 1 HANA Backup Name: SCADMIN01
Node 2 IP Address: 10.254.15.22
Node 2 HANA instance number: 02
Node 2 HANA Backup Name: SCADMIN02
Node 3 IP Address: 10.254.15.23
Node 3 HANA instance number: 03
Node 3 HANA Backup Name: SCADMIN03
Node 4 IP Address: 10.254.15.24
Node 4 HANA instance number: 04
Node 4 HANA Backup Name: SCADMIN04
Node 5 IP Address: 10.254.15.25
Node 5 HANA instance number: 05
Node 5 HANA Backup Name: SCADMIN05
Node 6 IP Address: 10.254.15.26
Node 6 HANA instance number: 06
Node 6 HANA Backup Name: SCADMIN06
Node 7 IP Address: 10.254.15.27
Node 7 HANA instance number: 07
Node 7 HANA Backup Name: SCADMIN07
Node 8 IP Address: 10.254.15.28
Node 8 HANA instance number: 08
Node 8 HANA Backup Name: SCADMIN08
```
>[!NOTE]
><span data-ttu-id="9320c-278">현재 노드 1 세부 정보만 hello 실제 HANA 저장소 스냅숏 스크립트에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-278">Currently, only Node 1 details are used in hello actual HANA storage snapshot script.</span></span> <span data-ttu-id="9320c-279">즉, hello 마스터 백업 노드로 변경 되는 경우 이미 확인 했는 다른 노드 대신할 수의 노드 1 hello 세부 정보를 수정 하 여 모든 HANA 노드에서 액세스 tooor를 테스트 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-279">We recommend that you test access tooor from all HANA nodes so that, if hello master backup node ever changes, you have already ensured that any other node can take its place by modifying hello details in Node 1.</span></span>

<span data-ttu-id="9320c-280">toocheck hello 구성 파일 또는 적절 한 연결 toohello HANA 인스턴스에 hello 올바른 구성에 대 한 hello 스크립트를 다음 중 하나를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-280">toocheck for hello correct configurations in hello configuration file or proper connectivity toohello HANA instances, run either of hello following scripts:</span></span>
- <span data-ttu-id="9320c-281">강화 구성의 경우(SAP 워크로드에 독립적임):</span><span class="sxs-lookup"><span data-stu-id="9320c-281">For a scale-up configuration (independent on SAP workload):</span></span>

 ```
testHANAConnection.pl
```
- <span data-ttu-id="9320c-282">확장 구성의 경우:</span><span class="sxs-lookup"><span data-stu-id="9320c-282">For a scale-out configuration:</span></span>

 ```
testHANAConnectionBW.pl
```

<span data-ttu-id="9320c-283">해당 hello 마스터 HANA 인스턴스에 액세스 필요한 tooall HANA 서버를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-283">Ensure that hello master HANA instance has access tooall required HANA servers.</span></span> <span data-ttu-id="9320c-284">매개 변수 toohello 스크립트가 없습니다 있지만 끝내십시오 적절 한 HANABackupCustomerDetails hello / HANABackupCustomerDetailsBW 제대로 스크립트 toorun hello에 대 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-284">There are no parameters toohello script, but you must complete hello appropriate HANABackupCustomerDetails/ HANABackupCustomerDetailsBW file for hello script toorun properly.</span></span> <span data-ttu-id="9320c-285">만 hello 셸 명령 오류 코드 반환 되므로 수 없으면 hello 스크립트 tooerror 검사 모든 인스턴스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-285">Because only hello shell command error codes are returned, it is not possible for hello script tooerror-check every instance.</span></span> <span data-ttu-id="9320c-286">그럼에도 hello 스크립트는 몇 가지 유용한 설명이 있습니다 toodouble 확인을 위해 제공.</span><span class="sxs-lookup"><span data-stu-id="9320c-286">Even so, hello script does provide some helpful comments for you toodouble-check.</span></span>

<span data-ttu-id="9320c-287">toorun hello 스크립트:</span><span class="sxs-lookup"><span data-stu-id="9320c-287">toorun hello script:</span></span>
```
 ./testHANAConnection.pl
```
 <span data-ttu-id="9320c-288">Hello 스크립트 hello hello HANA 인스턴스 상태를 얻고 성공적으로 hello HANA 연결 성공 했다는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-288">If hello script successfully obtains hello status of hello HANA instance, it displays a message that hello HANA connection was successful.</span></span>

<span data-ttu-id="9320c-289">또한 된 형식이 두 번째 스크립트의 toocheck hello 마스터 HANA 인스턴스 서버 기능 toosign toohello 저장소에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-289">Additionally, there is a second type of script you can use toocheck hello master HANA instance server's ability toosign in toohello storage.</span></span> <span data-ttu-id="9320c-290">Hello azure를 실행 하기 전에\_hana\_백업 (\_bw).pl 스크립트 hello 다음 스크립트를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-290">Before you execute hello azure\_hana\_backup(\_bw).pl script, you must execute hello next script.</span></span> <span data-ttu-id="9320c-291">볼륨 스냅숏이 없습니다 있으면가 불가능 한 toodetermine hello 볼륨 단순히 비어 있거나는 ssh 오류 tooobtain hello 스냅숏 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-291">If a volume contains no snapshots, it is impossible toodetermine whether hello volume is simply empty or there is an ssh failure tooobtain hello snapshot details.</span></span> <span data-ttu-id="9320c-292">이러한 이유로 hello 스크립트는 두 단계를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-292">For this reason, hello script executes two steps:</span></span>

- <span data-ttu-id="9320c-293">해당 hello 저장소 콘솔은 액세스할 수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-293">It verifies that hello storage console is accessible.</span></span>
- <span data-ttu-id="9320c-294">HANA 인스턴스에서 각 볼륨의 테스트, 더미 또는 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-294">It creates a test, or dummy, snapshot for each volume by HANA instance.</span></span>

<span data-ttu-id="9320c-295">이러한 이유로 hello HANA 인스턴스에 대 한 인수로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-295">For this reason, hello HANA instance is included as an argument.</span></span> <span data-ttu-id="9320c-296">다시, 가능한 tooprovide 오류 hello 저장소 연결에 대 한 검사는 없지만 hello 스크립트 hello 실행이 실패 하면 유용한 힌트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-296">Again, it is not possible tooprovide error checking for hello storage connection, but hello script provides helpful hints if hello execution fails.</span></span>

<span data-ttu-id="9320c-297">hello 스크립트는으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-297">hello script is run as:</span></span>
```
 ./testStorageSnapshotConnection.pl <hana instance>
```
<span data-ttu-id="9320c-298">또는 다음의 경우 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-298">Or it is run as:</span></span>
```
./testStorageSnapshotConnectionBW.pl <hana instance>
```
<span data-ttu-id="9320c-299">hello 스크립트에는 적절 하 게 배포 tooyour 저장소 테 넌 트에서 주위 hello 논리 단위 번호 (Lun)을 소유 하는 hello 서버 인스턴스에서 사용 되는 구성 된 수 toosign 있는 없다는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-299">hello script also displays a message that you are able toosign in appropriately tooyour deployed storage tenant, which is organized around hello logical unit numbers (LUNs) that are used by hello server instances you own.</span></span>

<span data-ttu-id="9320c-300">첫 번째 저장소 스냅숏 기반 백업을 hello를 실행 하기 전에 hello 다음 스크립트 toomake 해당 hello 구성이 올바른지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-300">Before you execute hello first storage snapshot-based backups, run hello next scripts toomake sure that hello configuration is correct.</span></span>

<span data-ttu-id="9320c-301">이러한 스크립트를 실행 한 후 실행 하 여 hello 스냅숏을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-301">After running these scripts, you can delete hello snapshots by executing:</span></span>
```
./removeTestStorageSnapshot.pl <hana instance>
```
<span data-ttu-id="9320c-302">또는</span><span class="sxs-lookup"><span data-stu-id="9320c-302">Or</span></span>
```
./removeTestStorageSnapshot.pl <hana instance>
```

### <a name="step-7-perform-on-demand-snapshots"></a><span data-ttu-id="9320c-303">7단계: 주문형 스냅숏 수행</span><span class="sxs-lookup"><span data-stu-id="9320c-303">Step 7: Perform on-demand snapshots</span></span>

<span data-ttu-id="9320c-304">여기에서 설명한 대로 주문형 스냅숏을 수행할 뿐만 아니라 cron를 사용하여 일반 스냅숏을 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-304">Perform on-demand snapshots (as well as schedule regular snapshots by using cron) as described here.</span></span>

<span data-ttu-id="9320c-305">확장 구성에 대 한 hello 다음 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-305">For scale-up configurations, execute hello following script:</span></span>
```
./azure_hana_backup.pl lhanad01 customer 20
```
<span data-ttu-id="9320c-306">확장 구성에 대 한 hello 다음 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-306">For scale-out configurations, execute hello following script:</span></span>
```
./azure_hana_backup_bw.pl lhanad01 customer 20
```
<span data-ttu-id="9320c-307">hello 확장 스크립트는 몇 가지 추가 검사 toomake 시키고 모든 HANA 서버에 액세스할 수 있는 모든 HANA 인스턴스 SAP HANA 또는 저장소 스냅숏 만들기를 계속 하기 전에 hello 인스턴스의 적절 한 상태를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-307">hello scale-out script does some additional checking toomake sure that all HANA servers can be accessed, and all HANA instances return appropriate status of hello instance before proceeding with creating SAP HANA or storage snapshots.</span></span>

<span data-ttu-id="9320c-308">다음 인수 hello 요소가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-308">hello following arguments are required:</span></span>

- <span data-ttu-id="9320c-309">hello HANA 인스턴스 필요한 백업입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-309">hello HANA instance requiring backup.</span></span>
- <span data-ttu-id="9320c-310">hello hello 저장소 스냅숏에 대 한 스냅숏 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-310">hello snapshot prefix for hello storage snapshot.</span></span>
- <span data-ttu-id="9320c-311">스냅숏 toobe hello 특정 접두사에 대 한 보관 hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-311">hello number of snapshots toobe kept for hello specific prefix.</span></span>

```
./azure_hana_backup.pl lhanad01 customer 20
```

<span data-ttu-id="9320c-312">hello 스크립트 실행의 hello 이러한 세 가지 단계로 hello 저장소 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-312">hello execution of hello script creates hello storage snapshot in these three distinct phases:</span></span>

- <span data-ttu-id="9320c-313">HANA 스냅숏을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-313">Execute a HANA snapshot.</span></span>
- <span data-ttu-id="9320c-314">저장소 스냅숏을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-314">Execute a storage snapshot.</span></span>
- <span data-ttu-id="9320c-315">Hello HANA 스냅숏을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-315">Remove hello HANA snapshot.</span></span>

<span data-ttu-id="9320c-316">에 복사 했던 hello HDB 실행 폴더에서 호출 하 여 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-316">Execute hello script by calling it from hello HDB executable folder that it was copied to.</span></span> <span data-ttu-id="9320c-317">그 다음 볼륨을 백업 이상 hello 하지만 또한 안녕하세요 명시적 SAP HANA 인스턴스 이름을 hello 볼륨 이름에 있는 모든 볼륨을 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-317">It backs up at least hello following volumes, but it also backs up any volume that has hello explicit SAP HANA instance name in hello volume name.</span></span>
```
hana_data_<hana instance>_prod_t020_vol
hana_log_<hana instance>_prod_t020_vol
hana_log_backup_<hana instance>_prod_t020_vol
hana_shared_<hana instance>_prod_t020_vol
```
<span data-ttu-id="9320c-318">(예: 20, 앞에 나온) hello 스크립트를 실행할 때 매개 변수로 제출 스냅숏의 hello 번호로, hello 보존 기간 관리 엄격 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-318">hello retention period is strictly administered, with hello number of snapshots submitted as a parameter when you execute hello script (such as 20, shown previously).</span></span> <span data-ttu-id="9320c-319">따라서 hello 기간 실행 및 hello hello 스크립트의 hello 호출에는 스냅숏 수의 hello 기간의 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-319">So hello amount of time is a function of hello period of execution and hello number of snapshots in hello call of hello script.</span></span> <span data-ttu-id="9320c-320">Hello 유지 되는 스냅숏의 개수 hello 스크립트의 hello 호출에서 매개 변수로 명명 된 hello 수를 초과 하면 가장 오래 된 저장소 스냅숏이이 레이블의 hello (이전 여기서에서 _사용자 지정_)는 새 스냅숏이 전에 삭제 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-320">If hello number of snapshots that are kept exceeds hello number that are named as a parameter in hello call of hello script, hello oldest storage snapshot of this label (in our previous case, _custom_) is deleted before a new snapshot is executed.</span></span> <span data-ttu-id="9320c-321">즉, hello 번호 hello hello 호출의 마지막 매개 변수는 hello 번호 toocontrol hello 스냅숏 수를 사용할 수 있습니다 하는 대로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-321">This means hello number you give as hello last parameter of hello call is hello number you can use toocontrol hello number of snapshots.</span></span>

>[!NOTE]
><span data-ttu-id="9320c-322">Hello 레이블을 변경 하는 즉시 다시 시작 hello 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-322">As soon as you change hello label, hello counting starts again.</span></span>

<span data-ttu-id="9320c-323">제공 하는 Azure 서비스 관리에서 SAP HANA를 인수로 multi-node 환경에서 스냅숏을 만들고 있는 경우 tooinclude hello HANA 인스턴스 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-323">You need tooinclude hello HANA instance name that's provided by SAP HANA on Azure Service Management as an argument if they are creating snapshots in multi-node environments.</span></span> <span data-ttu-id="9320c-324">단일 노드 환경에서 Azure (대형 인스턴스) 단위에 SAP HANA hello의 hello 이름 만으로는 있지만 hello HANA 인스턴스 이름을 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-324">In single-node environments, hello name of hello SAP HANA on Azure (large instances) unit is sufficient, but hello HANA instance name is still recommended.</span></span>

<span data-ttu-id="9320c-325">또한 있습니다 수를 사용 하 여 부팅 volumes\LUNs 백업 hello 동일 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-325">Additionally, you can back up boot volumes\LUNs by using hello same script.</span></span> <span data-ttu-id="9320c-326">처음 HANA를 실행하는 경우 한 번 이상 부팅 볼륨을 백업해야 합니다. 하지만 cron의 부팅에 대해 주간 또는 야간 백업 일정을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-326">You must back up your boot volume at least once when you first run HANA, although we recommend a weekly or nightly backup schedule for booting in cron.</span></span> <span data-ttu-id="9320c-327">SAP HANA 인스턴스 이름을 추가, 보다 삽입 하는 대신 _부팅_ hello 스크립트에 인수를 다음과 같이 hello 대로:</span><span class="sxs-lookup"><span data-stu-id="9320c-327">Rather than add an SAP HANA instance name, insert _boot_ as hello argument into hello script as follows:</span></span>
```
./azure_hana_backup boot customer 20
```
<span data-ttu-id="9320c-328">hello 동일한 보존 정책을 제공 되어 toohello 부팅 볼륨도 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-328">hello same retention policy is afforded toohello boot volume as well.</span></span> <span data-ttu-id="9320c-329">설명 된 대로 특수 한 경우에만에 이전에 같은 SAP 향상 된 기능, 패키지 (EHP)으로 업그레이드 하는 동안 하거나 toocreate 고유 저장소 스냅숏을 해야 할 때 주문형으로 스냅숏을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-329">Use on-demand snapshots, as described previously, for special cases only, such as during an SAP enhancement package (EHP) upgrade, or when you need toocreate a distinct storage snapshot.</span></span>

<span data-ttu-id="9320c-330">Cron를 사용 하 여 예약 된 tooperform 저장소 스냅샷 좋습니다 하 고 모든 백업 및 재해 복구 요구 사항 (수정 하 고 hello 스크립트 입력 toomatch hello 백업 시간을 요청한 다양 한)에 동일한 스크립트 hello를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-330">We encourage you tooperform scheduled storage snapshots using cron, and we recommend that you use hello same script for all backups and disaster-recovery needs (modifying hello script inputs toomatch hello various requested backup times).</span></span> <span data-ttu-id="9320c-331">해당 실행 시간(매시간, 12시간, 매일 또는 매주)에 따라 cron에서 모두 다르게 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-331">These are all scheduled differently in cron depending on their execution time: hourly, 12-hour, daily, or weekly.</span></span> <span data-ttu-id="9320c-332">hello cron 일정은 위에 설명 된 hello 장기 오프 사이트 백업에 대 한 보존 레이블 지정과 일치 하는 디자인 된 toocreate 저장소 스냅숏입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-332">hello cron schedule is designed toocreate storage snapshots that match hello previously discussed retention labeling for long-term off-site backup.</span></span> <span data-ttu-id="9320c-333">hello 명령 tooback (데이터 및 로그 파일이 백업 시간별, hello 부팅 볼륨은 매일 백업 하는 반면)가 요청 된 빈도 따라 모든 프로덕션 볼륨을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-333">hello script includes commands tooback up all production volumes, depending on their requested frequency (data and log files are backed up hourly, whereas hello boot volume is backed up daily).</span></span>

<span data-ttu-id="9320c-334">hello 항목 hello cron 스크립트 다음에 실행 매시간 hello에 10 분, 10 분 단위 hello 및 hello 10 분 단위에서 매일 12 시간 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-334">hello entries in hello following cron script run every hour at hello tenth minute, every 12 hours at hello tenth minute, and daily at hello tenth minute.</span></span> <span data-ttu-id="9320c-335">hello cron 작업 하는 방식에 만들어집니다. 해당 하나만 SAP HANA 저장소 스냅숏을 수행 특정 시간에 하므로 hello 시간 및 일별 백업에서 발생 하지 않는 hello 동일한 시간 (오전 12시 10분).</span><span class="sxs-lookup"><span data-stu-id="9320c-335">hello cron jobs are created in such a way that only one SAP HANA storage snapshot takes place during any particular hour, so that hello hourly and daily backups do not occur at hello same time (12:10 AM).</span></span> <span data-ttu-id="9320c-336">스냅숏 만들기 및 복제 toohelp 최적화, Azure 서비스 관리에서 SAP HANA hello 권장 toorun 있습니다에 대 한 시간 백업을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-336">toohelp optimize your snapshot creation and replication, SAP HANA on Azure Service Management provides hello recommended time for you toorun your backups.</span></span>

<span data-ttu-id="9320c-337">hello 기본 cron /etc/crontab의 일정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-337">hello default cron scheduling in /etc/crontab is as follows:</span></span>
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 14
```
<span data-ttu-id="9320c-338">이전 cron 지침 hello (하지 않고 부팅 볼륨) hello HANA 볼륨 hello 레이블로 스냅숏 시간별을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-338">In hello previous cron instructions, hello HANA volumes (without boot volume) get an hourly snapshot with hello label.</span></span> <span data-ttu-id="9320c-339">이러한 66개의 스냅숏이 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-339">Of these snapshots, 66 are retained.</span></span> <span data-ttu-id="9320c-340">또한 hello 12 시간 레이블이 있는 14 스냅숏은 보존 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-340">Additionally, 14 snapshots with hello 12-hour label are retained.</span></span> <span data-ttu-id="9320c-341">잠재적으로 3일 간의 매시간 스냅숏에 추가로 4일 간의 12시간 스냅숏을 얻게 되어 한 주 간의 스냅숏을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-341">You potentially get hourly snapshots for three days, plus 12-hour snapshots for another four days, which gives you an entire week of snapshots.</span></span>

<span data-ttu-id="9320c-342">Cron 내에서 예약 hello 스크립트는 몇 분 정도 만큼 지연 표시 하지 않는 한 특정 시간에 하나의 스크립트를 실행 해야 하기 때문에 작업은 복잡할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-342">Scheduling within cron can be tricky, because only one script should be executed at any particular time, unless hello scripts are staggered by several minutes.</span></span> <span data-ttu-id="9320c-343">장기 보존에 대 한 매일 백업 하려는 경우 (수와 함께 보존 각 7), 12 시간 스냅숏과 함께 일일 스냅숏은 유지 됩니다 또는 hello 시간별 스냅숏 10 분 후 시차를 두고 진행된 tootake 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-343">If you want daily backups for long-term retention, either a daily snapshot is kept along with a 12-hour snapshot (with a retention count of seven each), or hello hourly snapshot is staggered tootake place 10 minutes later.</span></span> <span data-ttu-id="9320c-344">하나의 일일 스냅숏은 hello 프로덕션 볼륨에 보관 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-344">Only one daily snapshot is kept in hello production volume.</span></span>
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 7
10 0 * * * ./azure_hana_backup.pl lhanad01 daily 7
```
<span data-ttu-id="9320c-345">여기에 나열 된 hello 주파수는 예일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-345">hello frequencies listed here are only examples.</span></span> <span data-ttu-id="9320c-346">tooderive 최적의 수가 스냅숏, 다음 기준을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="9320c-346">tooderive your optimum number of snapshots, use hello following criteria:</span></span>

- <span data-ttu-id="9320c-347">지정 시간 복구에 대한 복구 시간 목표의 요구 사항</span><span class="sxs-lookup"><span data-stu-id="9320c-347">Requirements in recovery time objective for point-in-time recovery.</span></span>
- <span data-ttu-id="9320c-348">공간 사용</span><span class="sxs-lookup"><span data-stu-id="9320c-348">Space usage.</span></span>
- <span data-ttu-id="9320c-349">잠재적 재해 복구를 위한 복구 지점 목표 및 복구 시간 목표의 요구 사항</span><span class="sxs-lookup"><span data-stu-id="9320c-349">Requirements in recovery point objective and recovery time objective for potential disaster recovery.</span></span>
- <span data-ttu-id="9320c-350">디스크에 대한 HANA 전체 데이터베이스 백업의 최종 실행</span><span class="sxs-lookup"><span data-stu-id="9320c-350">Eventual execution of HANA full database backups against disks.</span></span> <span data-ttu-id="9320c-351">디스크에 대해 전체 데이터베이스 백업 될 때마다 또는 _backint_ 인터페이스를 수행 storage 스냅숏 hello 실행이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-351">Whenever a full database backup against disks, or _backint_ interface, is performed, hello execution of storage snapshots fails.</span></span> <span data-ttu-id="9320c-352">Storage 스냅숏 기반으로 tooexecute 전체 데이터베이스 백업 하려는 경우 저장소 스냅숏 hello 실행이이 시간 동안 사용할 수 없다는 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-352">If you plan tooexecute full database backups on top of storage snapshots, make sure that hello execution of storage snapshots is disabled during this time.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="9320c-353">SAP HANA 백업에 대 한 스냅숏 저장소 hello 사용 hello 스냅숏을 SAP HANA 로그 백업과 함께에서 수행 될 때만 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-353">hello use of storage snapshots for SAP HANA backups is valid only when hello snapshots are performed in conjunction with SAP HANA log backups.</span></span> <span data-ttu-id="9320c-354">이러한 로그 백업 필요 toobe 수 toocover hello hello 저장소 스냅숏 간의 기간 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-354">These log backups need toobe able toocover hello time periods between hello storage snapshots.</span></span> <span data-ttu-id="9320c-355">30 일의 지정 시간 복구가 약정 toousers를 설정한 경우 hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-355">If you've set a commitment toousers of a point-in-time recovery of 30 days, you need hello following:</span></span>

- <span data-ttu-id="9320c-356">기능 tooaccess 저장소 스냅숏 30 일입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-356">Ability tooaccess a storage snapshot that is 30 days old.</span></span>
- <span data-ttu-id="9320c-357">Hello 지난 30 일 이내를 통해 연속 로그 백업입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-357">Contiguous log backups over hello last 30 days.</span></span>

<span data-ttu-id="9320c-358">로그 백업의 범위 hello도 hello 백업 로그 볼륨의 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-358">In hello range of log backups, create a snapshot of hello backup log volume as well.</span></span> <span data-ttu-id="9320c-359">그러나 수 있는지 tooperform 수 있도록를 정기적인 로그 백업:</span><span class="sxs-lookup"><span data-stu-id="9320c-359">However, be sure tooperform regular log backups so that you can:</span></span>

- <span data-ttu-id="9320c-360">Hello 연속 로그 백업은 지정 시간 복구 tooperform 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-360">Have hello contiguous log backups needed tooperform point-in-time recoveries.</span></span>
- <span data-ttu-id="9320c-361">Hello SAP HANA 로그 볼륨의 공간이 부족에서 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-361">Prevent hello SAP HANA log volume from running out of space.</span></span>

<span data-ttu-id="9320c-362">Hello 마지막 단계 중 하나에서 SAP HANA Studio tooschedule SAP HANA 백업 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-362">One of hello last steps is tooschedule SAP HANA backup logs in SAP HANA Studio.</span></span> <span data-ttu-id="9320c-363">hello SAP HANA 백업 로그 대상 위치는 특별히 만든 hello hana/로그\_/hana/log/backups hello 탑재 지점은으로 볼륨을 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-363">hello SAP HANA backup log target destination is hello specially created hana/log\_backups volume with hello mount point of /hana/log/backups.</span></span>

![SAP HANA Studio에서 SAP HANA 백업 로그 예약](./media/hana-overview-high-availability-disaster-recovery/image5-schedule-backup.png)

<span data-ttu-id="9320c-365">15분보다 더 자주 수행된 백업을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-365">You can choose backups that are more frequent than every 15 minutes.</span></span> <span data-ttu-id="9320c-366">일부 사용자도 1분마다 로그 백업을 수행할 수 있지만 15분 _이상_은 권장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-366">Some users even perform log backups every minute, although we do not recommend going _over_ 15 minutes.</span></span>

<span data-ttu-id="9320c-367">hello 최종 단계 tooperform 파일 기반 백업 (이후 hello SAP HANA의 초기 설치) toocreate hello 백업 카탈로그 내에 있어야 하는 단일 백업 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-367">hello final step is tooperform a file-based backup (after hello initial installation of SAP HANA) toocreate a single backup entry that must exist within hello backup catalog.</span></span> <span data-ttu-id="9320c-368">그렇지 않으면 SAP HANA는 지정된 로그 백업을 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-368">Otherwise SAP HANA cannot initiate your specified log backups.</span></span>

![파일 기반 백업 toocreate 단일 백업 항목 만들기](./media/hana-overview-high-availability-disaster-recovery/image6-make-backup.png)

### <a name="monitoring-hello-number-and-size-of-snapshots-on-hello-disk-volume"></a><span data-ttu-id="9320c-370">Hello 디스크 볼륨의 스냅숏의 hello 수와 크기를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-370">Monitoring hello number and size of snapshots on hello disk volume</span></span>

<span data-ttu-id="9320c-371">특정 저장소 볼륨을 스냅숏 및 스냅숏 hello 저장소 소비 hello 수를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-371">On a particular storage volume, you can monitor hello number of snapshots and hello storage consumption of snapshots.</span></span> <span data-ttu-id="9320c-372">hello `ls` 명령 hello 스냅숏 디렉터리 또는 파일은 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-372">hello `ls` command doesn't show hello snapshot directory or files.</span></span> <span data-ttu-id="9320c-373">그러나 Linux 운영 체제 명령 hello `du` 명령 뒤 hello로 않습니다:</span><span class="sxs-lookup"><span data-stu-id="9320c-373">However, hello Linux OS command `du` does, with hello following commands:</span></span>

- <span data-ttu-id="9320c-374">`du –sh .snapshot`hello 스냅숏 디렉터리 내에서 모든 스냅숏의 합계를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-374">`du –sh .snapshot` provides a total of all snapshots within hello snapshot directory.</span></span>
- <span data-ttu-id="9320c-375">`du –sh --max-depth=1`각 스냅숏의 hello 크기 및 hello.snapshot 폴더에 저장 된 모든 스냅숏을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-375">`du –sh --max-depth=1` lists all snapshots that are saved in hello .snapshot folder and hello size of each snapshot.</span></span>
- <span data-ttu-id="9320c-376">`du –hc`모든 스냅숏에 사용 되는 hello 전체 크기를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-376">`du –hc` provides hello total size used by all snapshots.</span></span>

<span data-ttu-id="9320c-377">이러한 명령을 toomake 수행 되 고 저장 하는 hello 스냅숏 hello 볼륨에서 모든 hello 저장소를 사용 하지는 있는지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-377">Use these commands toomake sure that hello snapshots that are taken and stored are not consuming all hello storage on hello volumes.</span></span>

### <a name="reducing-hello-number-of-snapshots-on-a-server"></a><span data-ttu-id="9320c-378">서버에서의 스냅숏 hello 수 줄이기</span><span class="sxs-lookup"><span data-stu-id="9320c-378">Reducing hello number of snapshots on a server</span></span>

<span data-ttu-id="9320c-379">이전에 설명한 대로 hello의 스냅숏 저장 하는 특정 레이블 수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-379">As explained earlier, you can reduce hello number of certain labels of snapshots that you store.</span></span> <span data-ttu-id="9320c-380">hello tooretain hello 명령 tooinitiate 스냅숏으로 레이블과 hello 원하는 스냅숏 개수는 두 개의 매개 변수를 지속 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-380">hello last two parameters of hello command tooinitiate a snapshot are a label and hello number of snapshots you want tooretain.</span></span>
```
./azure_hana_backup.pl lhanad01 customer 20
```
<span data-ttu-id="9320c-381">이전 예에서 hello hello 스냅숏 레이블은 _고객_ 이며이 레이블 toobe 유지를 사용 하 여 스냅숏의 hello 수 _20_합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-381">In hello previous example, hello snapshot label is _customer_ and hello number of snapshots with this label toobe retained is _20_.</span></span> <span data-ttu-id="9320c-382">Toodisk 공간 소비를 응답 tooreduce hello 수의 저장 된 스냅숏이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-382">As you respond toodisk space consumption, you might want tooreduce hello number of stored snapshots.</span></span> <span data-ttu-id="9320c-383">hello 쉽게 스냅숏 tooreduce hello 번호는 마지막 매개 변수 집합 too5 hello 사용 하 여 toorun hello 스크립트:</span><span class="sxs-lookup"><span data-stu-id="9320c-383">hello easy way tooreduce hello number of snapshots is toorun hello script with hello last parameter set too5:</span></span>
```
./azure_hana_backup.pl lhanad01 customer 5
```
<span data-ttu-id="9320c-384">스냅숏, 스냅숏, hello 새 저장소를 포함 하 여 hello 수는이 설정 사용 하 여 hello 스크립트 실행의 결과로 _5_합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-384">As a result of running hello script with this setting, hello number of snapshots, including hello new storage snapshot, is _5_.</span></span>

 >[!NOTE]
 > <span data-ttu-id="9320c-385">이 스크립트는 hello 가장 최근의 이전 스냅숏 시간 넘은 경우에 hello 스냅숏 수를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-385">This script reduces hello number of snapshots only if hello most recent previous snapshot is more than one hour old.</span></span> <span data-ttu-id="9320c-386">hello 스크립트 보다 작거나 1 시간 전의 스냅숏은 삭제 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-386">hello script does not delete snapshots that are less than one hour old.</span></span>

<span data-ttu-id="9320c-387">이러한 제한 사항은 관련된 toohello 선택적 재해 복구 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-387">These restrictions are related toohello optional disaster-recovery functionality offered.</span></span>

<span data-ttu-id="9320c-388">하지 않기로 toomaintain의 해당 접두사로 스냅숏 집합을 사용 하 여 hello 스크립트를 실행할 수 없습니다 _0_ hello 보존 번호 tooremove 해당 접두사와 일치 하는 모든 스냅숏으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-388">If you no longer want toomaintain a set of snapshots with that prefix, you can execute hello script with _0_ as hello retention number tooremove all snapshots matching that prefix.</span></span> <span data-ttu-id="9320c-389">그러나 모든 스냅숏 제거 재해 복구의 hello 기능 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-389">However, removing all snapshots can affect hello capabilities of disaster recovery.</span></span>

### <a name="recovering-toohello-most-recent-hana-snapshot"></a><span data-ttu-id="9320c-390">가장 최근의 HANA 스냅숏으로 toohello 복구</span><span class="sxs-lookup"><span data-stu-id="9320c-390">Recovering toohello most recent HANA snapshot</span></span>

<span data-ttu-id="9320c-391">Hello 이벤트에서 프로덕션 다운 시나리오, 저장소 스냅숏에서 복구 과정 hello 발생할 있습니다 시작할 수 있습니다 Azure 서비스 관리에서 SAP HANA 인 고객 인시던트에으로.</span><span class="sxs-lookup"><span data-stu-id="9320c-391">In hello event that you experience a production-down scenario, hello process of recovering from a storage snapshot can be initiated as a customer incident with SAP HANA on Azure Service Management.</span></span> <span data-ttu-id="9320c-392">이러한 예기치 않은 시나리오는 프로덕션 시스템 및 hello 유일한 방법은 tooretrieve hello 데이터는 toorestore hello 프로덕션 데이터베이스에서 데이터가 삭제 하는 긴급도 높은 것 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-392">Such an unexpected scenario might be a high-urgency matter if data was deleted in a production system and hello only way tooretrieve hello data is toorestore hello production database.</span></span>

<span data-ttu-id="9320c-393">Hello에 반면, 지정 시간 복구 낮은 긴급도 될 수 및 일에 대 한 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-393">On hello other hand, a point-in-time recovery could be low urgency and planned for days in advance.</span></span> <span data-ttu-id="9320c-394">우선 순위 문제를 발생시키는 대신 Azure의 SAP HANA Service Management를 사용하여 이 복구를 계획할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-394">You can plan this recovery with SAP HANA on Azure Service Management instead of raising a high-priority issue.</span></span> <span data-ttu-id="9320c-395">예를 들어 있습니다 수 수립 tootry hello SAP 소프트웨어를 업그레이드 하는 새 향상 패키지 하 고 적용 하 여 다음 toorevert hello EHP 업그레이드 하기 전에 hello 상태를 나타내는 tooa 스냅숏을 백업 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-395">For example, you might be planning tootry an upgrade of hello SAP software by applying a new enhancement package, and you then need toorevert back tooa snapshot that represents hello state before hello EHP upgrade.</span></span>

<span data-ttu-id="9320c-396">Hello 요청을 실행 하기 전에 몇 가지 준비 toodo 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-396">Before you issue hello request, you need toodo some preparation.</span></span> <span data-ttu-id="9320c-397">Azure 서비스 관리 팀에 SAP HANA 다음를 처리 하 여 hello 요청 복원 hello 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-397">SAP HANA on Azure Service Management team can then handle hello request and provide hello restored volumes.</span></span> <span data-ttu-id="9320c-398">나중에 hello 스냅숏을 기반으로 하는 tooyou toorestore hello HANA 데이터베이스를 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-398">Afterward, it is up tooyou toorestore hello HANA database based on hello snapshots.</span></span> <span data-ttu-id="9320c-399">다음은 tooprepare hello에 대 한 요청 방법:</span><span class="sxs-lookup"><span data-stu-id="9320c-399">Here is how tooprepare for hello request:</span></span>

>[!NOTE]
><span data-ttu-id="9320c-400">사용자 인터페이스 스크린샷 SAP HANA 릴리스를 사용 하는 hello에 따라 다음 hello에서 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-400">Your user interface might vary from hello following screenshots, depending on hello SAP HANA release you are using.</span></span>

1. <span data-ttu-id="9320c-401">스냅숏 toorestore를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-401">Decide which snapshot toorestore.</span></span> <span data-ttu-id="9320c-402">라는 메시지가 표시 되 고, 그렇지 않으면만 hello hana/데이터 볼륨을 복원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-402">Only hello hana/data volume would be restored unless you are instructed otherwise.</span></span>

2. <span data-ttu-id="9320c-403">Hello HANA 인스턴스를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-403">Shut down hello HANA instance.</span></span>

 ![Hello HANA 인스턴스 종료](./media/hana-overview-high-availability-disaster-recovery/image7-shutdown-hana.png)

3. <span data-ttu-id="9320c-405">각 HANA 데이터베이스 노드에 hello 데이터 볼륨을 분리 하십시오.</span><span class="sxs-lookup"><span data-stu-id="9320c-405">Unmount hello data volumes on each HANA database node.</span></span> <span data-ttu-id="9320c-406">hello 스냅숏의 hello 복원 hello 데이터 볼륨 탑재 되지 않은 경우 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-406">hello restoration of hello snapshot fails if hello data volumes are not unmounted.</span></span>

 ![각 HANA 데이터베이스 노드에 hello 데이터 볼륨을 분리 합니다.](./media/hana-overview-high-availability-disaster-recovery/image8-unmount-data-volumes.png)

4. <span data-ttu-id="9320c-408">특정 스냅숏의 Azure 지원 요청 tooinstruct hello 복원을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-408">Open an Azure support request tooinstruct hello restoration of a specific snapshot.</span></span>

 - <span data-ttu-id="9320c-409">Hello 복원 하는 동안: Azure 서비스 관리에서 SAP HANA tooattend 데이터가 없는 어떠한 손실도 하는 전화 회의 tooensure 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-409">During hello restoration: SAP HANA on Azure Service Management might ask you tooattend a conference call tooensure that no data is getting lost.</span></span>

 - <span data-ttu-id="9320c-410">Hello 복원 후: Azure 서비스 관리에서 SAP HANA 알리는 hello 저장소 스냅숏이 복원 된 경우.</span><span class="sxs-lookup"><span data-stu-id="9320c-410">After hello restoration: SAP HANA on Azure Service Management notifies you when hello storage snapshot has been restored.</span></span>

5. <span data-ttu-id="9320c-411">Hello 복원 프로세스가 완료 되 면 모든 데이터 볼륨을 다시 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-411">After hello restoration process is complete, remount all data volumes.</span></span>

 ![모든 데이터 볼륨 다시 탑재](./media/hana-overview-high-availability-disaster-recovery/image9-remount-data-volumes.png)

6. <span data-ttu-id="9320c-413">수행 하지 자동으로 만들 수 있기 때문 tooHANA DB SAP HANA Studio를 통해 다시 연결 하면 SAP HANA Studio 내에서 복구 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-413">Select recovery options within SAP HANA Studio, if they do not automatically come up when you reconnect tooHANA DB through SAP HANA Studio.</span></span> <span data-ttu-id="9320c-414">hello 다음 예제에서는 복원 toohello 마지막 HANA 스냅숏</span><span class="sxs-lookup"><span data-stu-id="9320c-414">hello following example shows a restoration toohello last HANA snapshot.</span></span> <span data-ttu-id="9320c-415">저장소 스냅숏 HANA 스냅숏 하나 포함 되 고 toohello 가장 최근의 저장소 스냅숏으로 복원 하는 가장 최근의 HANA 스냅숏으로 hello 상태 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-415">A storage snapshot embeds one HANA snapshot, and if you are restoring toohello most recent storage snapshot, it should be hello most recent HANA snapshot.</span></span> <span data-ttu-id="9320c-416">(Toolocate tooolder storage 스냅숏을 복원 하는 경우 필요한 hello HANA hello 시간 hello 저장소 스냅숏을 기반 스냅숏을.)</span><span class="sxs-lookup"><span data-stu-id="9320c-416">(If you are restoring tooolder storage snapshots, you need toolocate hello HANA snapshot based on hello time hello storage snapshot was taken.)</span></span>

 ![SAP HANA Studio 내에서 복구 옵션 선택](./media/hana-overview-high-availability-disaster-recovery/image10-recover-options-a.png)

7. <span data-ttu-id="9320c-418">선택 **복구 hello 데이터베이스 tooa 특정 데이터 백업이 나 저장소 스냅숏을**합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-418">Select **Recover hello database tooa specific data backup or storage snapshot**.</span></span>

 ![hello "복구 유형 선택" 창](./media/hana-overview-high-availability-disaster-recovery/image11-recover-options-b.png)

8. <span data-ttu-id="9320c-420">**카탈로그 없이 백업 지정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-420">Select **Specify backup without catalog**.</span></span>

 ![hello "백업 위치 지정" 창](./media/hana-overview-high-availability-disaster-recovery/image12-recover-options-c.png)

9. <span data-ttu-id="9320c-422">Hello에 **대상 형식** 목록에서 **스냅숏**합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-422">In hello **Destination Type** list, select **Snapshot**.</span></span>

 ![hello "지정 hello 백업 tooRecover" 창](./media/hana-overview-high-availability-disaster-recovery/image13-recover-options-d.png)

10. <span data-ttu-id="9320c-424">클릭 **마침** toostart hello 복구 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-424">Click **Finish** toostart hello recovery process.</span></span>

 ![Toostart hello 복구 프로세스 "마침"을 클릭 합니다.](./media/hana-overview-high-availability-disaster-recovery/image14-recover-options-e.png)

11. <span data-ttu-id="9320c-426">hello HANA 데이터베이스 복원 되 고 toohello HANA 스냅숏 hello 저장소 스냅숏에 포함 된 복구.</span><span class="sxs-lookup"><span data-stu-id="9320c-426">hello HANA database is restored and recovered toohello HANA snapshot that's included in hello storage snapshot.</span></span>

 ![HANA 데이터베이스를 복원 하 고 복구 된 toohello HANA 스냅숏](./media/hana-overview-high-availability-disaster-recovery/image15-recover-options-f.png)

### <a name="recovering-toohello-most-recent-state"></a><span data-ttu-id="9320c-428">Toohello 가장 최근 상태 복구</span><span class="sxs-lookup"><span data-stu-id="9320c-428">Recovering toohello most recent state</span></span>

<span data-ttu-id="9320c-429">hello 다음 프로세스 복원 hello 저장소 스냅숏에 포함 된 hello HANA 스냅숏 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-429">hello following process restores hello HANA snapshot that is included in hello storage snapshot.</span></span> <span data-ttu-id="9320c-430">그런 다음 hello 저장소 스냅숏을 복원 하기 전에 hello 트랜잭션 로그 백업을 toohello의 가장 최근 상태 hello 데이터베이스를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-430">It then restores hello transaction log backups toohello most recent state of hello database before restoring hello storage snapshot.</span></span>

>[!IMPORTANT]
><span data-ttu-id="9320c-431">계속 진행하기 전에 트랜잭션 로그 백업의 완전한 연속 체인이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-431">Before you proceed, make sure that you have a complete and contiguous chain of transaction log backups.</span></span> <span data-ttu-id="9320c-432">이러한 백업 없이 hello hello 데이터베이스의 현재 상태를 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-432">Without these backups, you cannot restore hello current state of hello database.</span></span>

1. <span data-ttu-id="9320c-433">Hello 앞에 "Recovering toohello 가장 최근의 HANA 스냅숏입니다." 절차의 1-6 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-433">Complete steps 1-6 of hello preceding procedure in "Recovering toohello most recent HANA snapshot."</span></span>

2. <span data-ttu-id="9320c-434">선택 **hello 데이터베이스 tooits 가장 최근 상태를 복구**합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-434">Select **Recover hello database tooits most recent state**.</span></span>

 !["Hello 데이터베이스 tooits 가장 최근 상태를 복구"를 선택 합니다.](./media/hana-overview-high-availability-disaster-recovery/image16-recover-database-a.png)

3. <span data-ttu-id="9320c-436">Hello 가장 최근의 HANA 로그 백업의 hello 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-436">Specify hello location of hello most recent HANA log backups.</span></span> <span data-ttu-id="9320c-437">hello 위치는 toocontain hello HANA 스냅숏 toohello 가장 최근 상태에서 HANA 트랜잭션 로그 백업을 모두 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-437">hello location needs toocontain all HANA transaction log backups from hello HANA snapshot toohello most recent state.</span></span>

 ![Hello 가장 최근의 HANA 로그 백업의 hello 위치 지정](./media/hana-overview-high-availability-disaster-recovery/image17-recover-database-b.png)

4. <span data-ttu-id="9320c-439">백업을 toorecover hello 데이터베이스에서 기본으로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-439">Select a backup as a base from which toorecover hello database.</span></span> <span data-ttu-id="9320c-440">예제에서는이 속성은 hello 저장소 스냅숏에 포함 된 hello HANA 스냅숏입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-440">In our example, this is hello HANA snapshot that was included in hello storage snapshot.</span></span> <span data-ttu-id="9320c-441">(하나만 스냅숏 hello 스크린 샷 뒤에 나열 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="9320c-441">(Only one snapshot is listed in hello following screenshot.)</span></span>

 ![백업 toorecover hello 데이터베이스에서 기본으로 선택](./media/hana-overview-high-availability-disaster-recovery/image18-recover-database-c.png)

5. <span data-ttu-id="9320c-443">지우기 hello **델타 백업을 사용** 확인란 hello HANA 스냅숏의 hello 시간과 hello 가장 최근 상태 간의 델타를 존재 하지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="9320c-443">Clear hello **Use Delta Backups** check box if deltas do not exist between hello time of hello HANA snapshot and hello most recent state.</span></span>

 ![지우기 hello "델타 백업을 사용" 확인란 없는 델타가 존재 하는 경우](./media/hana-overview-high-availability-disaster-recovery/image19-recover-database-d.png)

6. <span data-ttu-id="9320c-445">Hello 요약 화면에서 클릭 **마침** toostart hello 복원 절차입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-445">On hello summary screen, click **Finish** toostart hello restoration procedure.</span></span>

 ![Hello 요약 화면에서 "마침"을 클릭](./media/hana-overview-high-availability-disaster-recovery/image20-recover-database-e.png)

### <a name="recovering-tooanother-point-in-time"></a><span data-ttu-id="9320c-447">복구 중 tooanother 지정 시간</span><span class="sxs-lookup"><span data-stu-id="9320c-447">Recovering tooanother point in time</span></span>
<span data-ttu-id="9320c-448">toorecover tooa 지정 hello HANA 스냅숏 (hello 저장소 스냅숏에 포함) 사이의 다른 하나는 hello HANA 스냅숏 지정 시간 복구 보다 이후 시간에 따라 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-448">toorecover tooa point in time between hello HANA snapshot (included in hello storage snapshot) and one that is later than hello HANA snapshot point-in-time recovery, do hello following:</span></span>

1. <span data-ttu-id="9320c-449">Hello HANA 스냅숏 toohello 시간 toorecover 원하는에서 트랜잭션 로그 백업을 모두 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-449">Make sure that you have all transaction log backups from hello HANA snapshot toohello time you want toorecover.</span></span>
2. <span data-ttu-id="9320c-450">"Recovering toohello 최신 상태입니다." hello 절차를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-450">Begin hello procedure under "Recovering toohello most recent state."</span></span>
3. <span data-ttu-id="9320c-451">Hello에 hello 절차의 2 단계에서 **복구 유형 선택** 창에서 **지정 시간 복구 hello 데이터베이스 toohello 다음**hello 지정 시간을 지정 하 고 3-6 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-451">In step 2 of hello procedure, in hello **Specify Recovery Type** window, select **Recover hello database toohello following point in time**, specify hello point in time, and then complete steps 3-6.</span></span>

## <a name="monitoring-hello-execution-of-snapshots"></a><span data-ttu-id="9320c-452">스냅숏 hello 실행 모니터링</span><span class="sxs-lookup"><span data-stu-id="9320c-452">Monitoring hello execution of snapshots</span></span>

<span data-ttu-id="9320c-453">스냅숏 저장소 toomonitor hello 실행을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-453">You need toomonitor hello execution of storage snapshots.</span></span> <span data-ttu-id="9320c-454">저장소 스냅숏으로 실행 하는 hello 스크립트 출력 tooa 파일에 쓰고 toohello 저장 hello Perl 스크립트와 같은 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-454">hello script that executes a storage snapshot writes output tooa file and then saves it toohello same location as hello Perl scripts.</span></span> <span data-ttu-id="9320c-455">각 스냅숏에 대해 별도 파일을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-455">A separate file is written for each snapshot.</span></span> <span data-ttu-id="9320c-456">각 파일의 hello 출력이 hello 스냅숏 스크립트를 실행 하는 다양 한 단계로 hello를 명확 하 게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-456">hello output of each file clearly shows hello various phases that hello snapshot script executes:</span></span>

- <span data-ttu-id="9320c-457">찾기 toocreate를 필요로 하는 hello 볼륨 스냅숏</span><span class="sxs-lookup"><span data-stu-id="9320c-457">Finding hello volumes that need toocreate a snapshot</span></span>
- <span data-ttu-id="9320c-458">이러한 볼륨에서 생성 된 hello 스냅숏 찾기</span><span class="sxs-lookup"><span data-stu-id="9320c-458">Finding hello snapshots taken from these volumes</span></span>
- <span data-ttu-id="9320c-459">최종 기존 스냅숏을 toomatch hello 스냅숏 개수 지정한 삭제</span><span class="sxs-lookup"><span data-stu-id="9320c-459">Deleting eventual existing snapshots toomatch hello number of snapshots you specified</span></span>
- <span data-ttu-id="9320c-460">HANA 스냅숏 만들기</span><span class="sxs-lookup"><span data-stu-id="9320c-460">Creating a HANA snapshot</span></span>
- <span data-ttu-id="9320c-461">Hello 볼륨 hello 저장소 스냅숏 만들기</span><span class="sxs-lookup"><span data-stu-id="9320c-461">Creating hello storage snapshot over hello volumes</span></span>
- <span data-ttu-id="9320c-462">Hello HANA 스냅샷 삭제</span><span class="sxs-lookup"><span data-stu-id="9320c-462">Deleting hello HANA snapshot</span></span>
- <span data-ttu-id="9320c-463">가장 최근의 hello 너무 스냅숏 이름 바꾸기**.0**</span><span class="sxs-lookup"><span data-stu-id="9320c-463">Renaming hello most recent snapshot too**.0**</span></span>

<span data-ttu-id="9320c-464">hello 스크립트의 가장 중요 한 부분 hello은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-464">hello most important part of hello script is this:</span></span>
```
**********************Creating HANA snapshot**********************
Creating hello HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data create snapshot"" ...
HANA snapshot created successfully.
**********************Creating Storage snapshot**********************
Taking snapshot hourly.recent for hana_data_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_log_backup_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_log_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_shared_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for sapmnt_lhanad01_t020_vol ...
Snapshot created successfully.
**********************Deleting HANA snapshot**********************
Deleting hello HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data drop snapshot"" ...
HANA snapshot deletion successfully.
```
<span data-ttu-id="9320c-465">어떻게 hello 스크립트 레코드 hello hello HANA 스냅숏 만든이이 샘플에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-465">You can see from this sample how hello script records hello creation of hello HANA snapshot.</span></span> <span data-ttu-id="9320c-466">Hello 확장의 경우에서이 프로세스는 hello 마스터 노드에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-466">In hello scale-out case, this process is initiated on hello master node.</span></span> <span data-ttu-id="9320c-467">hello 마스터 노드는 각 hello 작업자 노드에서 hello 스냅숏 hello 동기 만들기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-467">hello master node initiates hello synchronous creation of hello snapshots on each of hello worker nodes.</span></span> <span data-ttu-id="9320c-468">Hello 저장소 스냅숏을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-468">Then hello storage snapshot is taken.</span></span> <span data-ttu-id="9320c-469">Hello 저장소 스냅숏 hello 성공적으로 실행 후 hello HANA 스냅숏이 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9320c-469">After hello successful execution of hello storage snapshots, hello HANA snapshot is deleted.</span></span>
