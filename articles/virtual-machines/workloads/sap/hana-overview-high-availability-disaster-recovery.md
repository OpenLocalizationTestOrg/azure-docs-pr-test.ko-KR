---
title: "Azure(큰 인스턴스)의 SAP HANA에 대한 고가용성 및 재해 복구 | Microsoft Docs"
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
ms.openlocfilehash: f95e944fc3ec3a831d97386443eb644420ae54dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="sap-hana-large-instances-high-availability-and-disaster-recovery-on-azure"></a><span data-ttu-id="fd249-103">Azure(큰 인스턴스)의 SAP HANA 고가용성 및 재해 복구</span><span class="sxs-lookup"><span data-stu-id="fd249-103">SAP HANA (large instances) high availability and disaster recovery on Azure</span></span> 

<span data-ttu-id="fd249-104">Azure(큰 인스턴스) 서버에서 업무상 중요한 SAP HANA를 실행할 때 고가용성 및 재해 복구는 중요한 측면입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-104">High availability and disaster recovery are important aspects of running your mission-critical SAP HANA on Azure (large instances) servers.</span></span> <span data-ttu-id="fd249-105">SAP, 시스템 통합업체 또는 Microsoft와 협의하여 적합한 고가용성/재해복구 전략을 설계하고 구현하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-105">It's important to work with SAP, your system integrator, or Microsoft to properly architect and implement the right high-availability/disaster-recovery strategy.</span></span> <span data-ttu-id="fd249-106">사용자 환경에 지정된 복구 지점 목표와 복구 시간 목표를 고려하는 것도 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-106">It is also important to consider the recovery point objective and recovery time objective, which are specific to your environment.</span></span>

## <a name="high-availability"></a><span data-ttu-id="fd249-107">고가용성</span><span class="sxs-lookup"><span data-stu-id="fd249-107">High availability</span></span>

<span data-ttu-id="fd249-108">Microsoft에서는 SAP HANA 고가용성 메서드를 "바로" 지원하며 여기에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-108">Microsoft supports SAP HANA high-availability methods "out of the box," which include:</span></span>

- <span data-ttu-id="fd249-109">**저장소 복제:** 동일한 데이터 센터 또는 별도의 위치 내에서 다른 위치에 모든 데이터를 복제하는 저장소 시스템의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-109">**Storage replication:** The storage system's ability to replicate all data to another location (within, or separate from, the same datacenter).</span></span> <span data-ttu-id="fd249-110">SAP HANA는 이 메서드와 독립적으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-110">SAP HANA operates independently of this method.</span></span>
- <span data-ttu-id="fd249-111">**HANA 시스템 복제:** 별도 SAP HANA 시스템으로 SAP HANA에 있는 모든 데이터를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-111">**HANA system replication:** The replication of all data in SAP HANA to a separate SAP HANA system.</span></span> <span data-ttu-id="fd249-112">복구 시간 목표는 정기적으로 데이터 복제를 통해 최소화됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-112">The recovery time objective is minimized through data replication at regular intervals.</span></span> <span data-ttu-id="fd249-113">SAP HANA는 비동기 모드, 메모리 내 동기 모드 및 동기 모드를 지원합니다(동일한 데이터 센터 내에 있거나 100KM 이내에 있는 SAP HANA 시스템에만 권장됨).</span><span class="sxs-lookup"><span data-stu-id="fd249-113">SAP HANA supports asynchronous, synchronous in-memory, and synchronous modes (recommended only for SAP HANA systems that are within the same datacenter or less than 100 KM apart).</span></span> <span data-ttu-id="fd249-114">HANA 큰 인스턴스 스탬프의 현재 디자인에서 고가용성을 위해 HANA 시스템 복제만을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-114">In the current design of HANA large-instance stamps, HANA system replication can be used for high availability only.</span></span>
- <span data-ttu-id="fd249-115">**자동 장애 조치 호스트:** 시스템 복제하는 대신 사용할 로컬 오류 복구 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-115">**Host auto-failover:** A local fault-recovery solution to use as an alternative to system replication.</span></span> <span data-ttu-id="fd249-116">하나 이상의 대기 SAP HANA 노드를 확장 모드로 구성하고 마스터 노드를 사용할 수 없을 때 SAP HANA를 자동으로 다른 노드에 장애 조치합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-116">When the master node becomes unavailable, one or more standby SAP HANA nodes are configured in scale-out mode and SAP HANA automatically fails over to another node.</span></span>

<span data-ttu-id="fd249-117">SAP HANA 고가용성에 대한 자세한 내용은 다음 SAP 정보를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fd249-117">For more information on SAP HANA high availability, see the following SAP information:</span></span>

- [<span data-ttu-id="fd249-118">SAP HANA 고가용성 백서</span><span class="sxs-lookup"><span data-stu-id="fd249-118">SAP HANA High-Availability Whitepaper</span></span>](http://go.sap.com/documents/2016/05/f8e5eeba-737c-0010-82c7-eda71af511fa.html)
- [<span data-ttu-id="fd249-119">SAP HANA 관리 가이드</span><span class="sxs-lookup"><span data-stu-id="fd249-119">SAP HANA Administration Guide</span></span>](http://help.sap.com/hana/SAP_HANA_Administration_Guide_en.pdf)
- [<span data-ttu-id="fd249-120">SAP HANA 시스템 복제에 대한 SAP Academy 비디오</span><span class="sxs-lookup"><span data-stu-id="fd249-120">SAP Academy Video on SAP HANA System Replication</span></span>](http://scn.sap.com/community/hana-in-memory/blog/2015/05/19/sap-hana-system-replication)
- [<span data-ttu-id="fd249-121">SAP 지원 참고 사항 #1999880 – SAP HANA 시스템 복제에 대한 FAQ</span><span class="sxs-lookup"><span data-stu-id="fd249-121">SAP Support Note #1999880 – FAQ on SAP HANA System Replication</span></span>](https://bcs.wdf.sap.corp/sap/support/notes/1999880)
- <span data-ttu-id="fd249-122">[SAP 지원 참고 사항 #2165547 – SAP HANA 시스템 복제 환경 내의 SAP HANA 백업 및 복원](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3231363535343726)</span><span class="sxs-lookup"><span data-stu-id="fd249-122">[SAP Support Note #2165547 – SAP HANA Backup and Restore within SAP HANA System Replication Environment](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3231363535343726)</span></span>
- <span data-ttu-id="fd249-123">[SAP 지원 참고 사항 #1984882 – 가동 중지 시간이 최소/없는 하드웨어 Exchange에 대한 SAP HANA 시스템 복제 사용](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3139383438383226)</span><span class="sxs-lookup"><span data-stu-id="fd249-123">[SAP Support Note #1984882 – Using SAP HANA System Replication for Hardware Exchange with Minimum/Zero Downtime](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3139383438383226)</span></span>

## <a name="disaster-recovery"></a><span data-ttu-id="fd249-124">재해 복구</span><span class="sxs-lookup"><span data-stu-id="fd249-124">Disaster recovery</span></span>

<span data-ttu-id="fd249-125">Azure(큰 인스턴스)의 SAP HANA가 지역 정책 지역에 있는 여러 Azure 지역에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-125">SAP HANA on Azure (large instances) is offered in two Azure regions in a geopolitical region.</span></span> <span data-ttu-id="fd249-126">재해 복구 중 두 개의 서로 다른 지역에 있는 두 개의 큰 인스턴스 스탬프 간에 데이터를 복제하는 네트워크에 직접 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-126">Between the two large-instance stamps of two different regions is a direct network connectivity for replicating data during disaster recovery.</span></span> <span data-ttu-id="fd249-127">데이터의 복제는 저장소 인프라를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-127">The replication of the data is storage-infrastructure based.</span></span> <span data-ttu-id="fd249-128">기본적으로 복제가 수행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-128">The replication is not done by default.</span></span> <span data-ttu-id="fd249-129">고객 구성에서 재해 복구를 주문한 경우에 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-129">It is done for the customer configurations that ordered the disaster recovery.</span></span> <span data-ttu-id="fd249-130">현재 디자인에서 재해 복구를 위해 HANA 시스템 복제를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-130">In the current design, HANA system replication can't be used for disaster recovery.</span></span>

<span data-ttu-id="fd249-131">그러나 재해 복구를 활용하기 위해 두 개의 서로 다른 Azure 지역에 대한 네트워크 연결을 디자인하기 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-131">However, to take advantage of the disaster recovery, you need to start to design the network connectivity to the two different Azure regions.</span></span> <span data-ttu-id="fd249-132">이를 위해 사용자의 기본 Azure 지역에 있는 온-프레미스에서 Azure ExpressRoute 회로 연결 및 온-프레미스에서 사용자의 재해 복구 지역에 다른 회로 연결이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-132">To do so, you need an Azure ExpressRoute circuit connection from on-premises in your main Azure region and another circuit connection from on-premises to your disaster-recovery region.</span></span> <span data-ttu-id="fd249-133">이러한 측정값은 MSEE(Microsoft Enterprise Edge 라우터) 위치를 포함하는 전체 Azure 지역에 문제가 발생한 상황에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-133">This measure would cover a situation in which a complete Azure region, including a Microsoft enterprise edge router (MSEE) location, has an issue.</span></span>

<span data-ttu-id="fd249-134">두 번째 측정값으로 해당 ExpressRoute 회로 모두에 대한 지역 중 하나에 있는 Azure(큰 인스턴스)의 SAP HANA에 연결된 모든 Azure 가상 네트워크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-134">As a second measure, you can connect all Azure virtual networks that connect to SAP HANA on Azure (large instances) in one of the regions to both of those ExpressRoute circuits.</span></span> <span data-ttu-id="fd249-135">이 측정값은 Azure와 온-프레미스 위치를 연결하는 MSEE 위치 중 하나가 작동하지 않는 경우에 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-135">This measure addresses a case where only one of the MSEE locations that connects your on-premises location with Azure goes off duty.</span></span>

<span data-ttu-id="fd249-136">다음 그림에서는 재해 복구에 대한 최적의 구성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-136">The following figure shows the optimal configuration for disaster recovery:</span></span>

![재해 복구에 대한 최적의 구성](./media/hana-overview-high-availability-disaster-recovery/image1-optimal-configuration.png)

<span data-ttu-id="fd249-138">네트워크 재해 복구 구성에 대한 최적의 사례는 온-프레미스에서 두 개의 다른 Azure 지역까지 두 개의 ExpressRoute 회로를 배치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-138">The optimal case for a disaster-recovery configuration of the network is to have two ExpressRoute circuits from on-premises to the two different Azure regions.</span></span> <span data-ttu-id="fd249-139">하나의 회로는 #1 지역으로 연결되어 프로덕션 인스턴스를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-139">One circuit goes to region #1, running a production instance.</span></span> <span data-ttu-id="fd249-140">두 번째 ExpressRoute 회로는 #2 지역으로 이동하여 일부 비프로덕션 HANA 인스턴스를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-140">The second ExpressRoute circuit goes to region #2, running some non-production HANA instances.</span></span> <span data-ttu-id="fd249-141">(이것은 MSEE 및 큰 인스턴스의 스탬프를 비롯한 전체 Azure 지역이 그리드를 중단하는 경우에 중요합니다.)</span><span class="sxs-lookup"><span data-stu-id="fd249-141">(This is important if an entire Azure region, including the MSEE and large-instance stamp, goes off the grid.)</span></span>

<span data-ttu-id="fd249-142">두 번째 측정값으로 다양한 가상 네트워크는 Azure(큰 인스턴스)의 SAP HANA에 연결되어 있는 다양한 ExpressRoute 회로에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-142">As a second measure, the various virtual networks are connected to the various ExpressRoute circuits that are connected to SAP HANA on Azure (large instances).</span></span> <span data-ttu-id="fd249-143">나중에 설명된 대로 MSEE가 실패한 위치를 무시하거나 재해 복구에 대한 복구 지점 목표를 낮출 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-143">You can bypass the location where an MSEE is failing, or you can lower the recovery point objective for disaster recovery, as we discuss later.</span></span>

<span data-ttu-id="fd249-144">재해 복구 설정에 대한 이후 요구 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-144">The next requirements for a disaster-recovery setup are:</span></span>

- <span data-ttu-id="fd249-145">사용자의 프로덕션 SKU와 동일한 크기인 Azure(큰 인스턴스)의 SAP HANA를 주문하고 재해 복구 지역에서 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-145">You must order SAP HANA on Azure (large instances) SKUs of the same size as your production SKUs and deploy them in the disaster-recovery region.</span></span> <span data-ttu-id="fd249-146">이러한 인스턴스를 사용하여 테스트, 샌드박스 또는 QA HANA 인스턴스를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-146">These instances can be used to run test, sandbox, or QA HANA instances.</span></span>
- <span data-ttu-id="fd249-147">필요한 경우 재해 복구 사이트에서 복구하려는 사용자의 Azure(큰 인스턴스)의 SAP HANA SKU 각각에 대한 재해 복구 프로필을 주문해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-147">You must order a disaster-recovery profile for each of your SAP HANA on Azure (large instances) SKUs that you want to recover in the disaster-recovery site, if necessary.</span></span> <span data-ttu-id="fd249-148">이 작업으로 인해 프로덕션 지역에서 재해 복구 지역까지 저장소 복제의 대상인 저장소 볼륨을 할당하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-148">This action leads to the allocation of storage volumes, which are the target of the storage replication from your production region into the disaster-recovery region.</span></span>

<span data-ttu-id="fd249-149">앞의 요구 사항을 충족한 후에 사용자는 저장소 복제를 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-149">After you meet the preceding requirements, it is your responsibility to start the storage replication.</span></span> <span data-ttu-id="fd249-150">Azure(큰 인스턴스)의 SAP HANA에 사용되는 저장소 인프라에서 저장소 복제의 기본은 저장소 스냅숏입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-150">In the storage infrastructure used for SAP HANA on Azure (large instances), the basis of storage replication is storage snapshots.</span></span> <span data-ttu-id="fd249-151">재해 복구 복제를 시작하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-151">To start the disaster-recovery replication, you need to perform:</span></span>

- <span data-ttu-id="fd249-152">앞서 설명한 대로 부팅 LUN의 스냅숏</span><span class="sxs-lookup"><span data-stu-id="fd249-152">A snapshot of your boot LUN, as described earlier.</span></span>
- <span data-ttu-id="fd249-153">앞서 설명한 대로 HANA 관련 볼륨의 스냅숏</span><span class="sxs-lookup"><span data-stu-id="fd249-153">A snapshot of your HANA-related volumes, as described earlier.</span></span>

<span data-ttu-id="fd249-154">이러한 스냅숏을 실행한 후에 재해 복구 지역에 있는 재해 복구 프로필과 연결된 볼륨에 볼륨의 초기 복제본이 시드됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-154">After you execute these snapshots, an initial replica of the volumes is seeded on the volumes that are associated with your disaster-recovery profile in the disaster-recovery region.</span></span>

<span data-ttu-id="fd249-155">이후에 최신 저장소 스냅숏은 1시간마다 저장소 볼륨을 개발하는 델타를 복제하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-155">Subsequently, the most recent storage snapshot is used every hour to replicate the deltas that develop on the storage volumes.</span></span>

<span data-ttu-id="fd249-156">이 구성을 사용하여 달성된 복구 지점 목표는 60에서 90분입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-156">The recovery point objective that's achieved with this configuration is from 60 to 90 minutes.</span></span> <span data-ttu-id="fd249-157">재해 복구 사례에서 복구 지점 목표를 향상시키려면 Azure(큰 인스턴스)의 SAP HANA에 있는 HANA 트랜잭션 로그 백업을 다른 Azure 지역에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-157">To achieve a better recovery point objective in the disaster-recovery case, copy the HANA transaction log backups from SAP HANA on Azure (large instances) to the other Azure region.</span></span> <span data-ttu-id="fd249-158">이 복구 지점 목표를 달성하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-158">To achieve this recovery point objective, do the following:</span></span>

1. <span data-ttu-id="fd249-159">HANA 트랜잭션 로그를 가능한 한 자주 /hana/log/backup에 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-159">Back up the HANA transaction log as frequently as possible to /hana/log/backup.</span></span>
2. <span data-ttu-id="fd249-160">Azure VM(가상 컴퓨터)에 완료되는 경우 트랜잭션 로그 백업을 복사합니다. 해당 항목은 Azure(큰 인스턴스)의 SAP HANA 서버에 연결된 가상 네트워크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-160">Copy the transaction log backups when they are finished to an Azure virtual machine (VM), which is in a virtual network that's connected to the SAP HANA on Azure (large instances) server.</span></span>
3. <span data-ttu-id="fd249-161">해당 VM에서 재해 복구 지역에 있는 가상 네트워크의 VM에 백업을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-161">From that VM, copy the backup to a VM that's in a virtual network in the disaster-recovery region.</span></span>
4. <span data-ttu-id="fd249-162">VM의 해당 지역에서 트랜잭션 로그 백업을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-162">Keep the transaction log backups in that region in the VM.</span></span>

<span data-ttu-id="fd249-163">재해 복구 프로필이 실제 서버에 배포된 후에 재해 발생 시 VM에서 Azure(큰 인스턴스)의 SAP HANA로 트랜잭션 로그 백업을 복사합니다. 해당 위치는 이제 재해 복구 지역의 주 서버로 해당 백업을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-163">In case of disaster, after the disaster-recovery profile has been deployed on an actual server, copy the transaction log backups from the VM to the SAP HANA on Azure (large instances) that is now the primary server in the disaster-recovery region, and restore those backups.</span></span> <span data-ttu-id="fd249-164">이 복구는 재해 복구 디스크에 대한 HANA의 상태는 HANA 스냅숏의 상태이기 때문에 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-164">This recovery is possible because the state of HANA on the disaster-recovery disks is that of a HANA snapshot.</span></span> <span data-ttu-id="fd249-165">트랜잭션 로그 백업의 추가 복원에 대한 오프셋 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-165">This is the offset point for further restorations of transaction log backups.</span></span>

## <a name="backup-and-restore"></a><span data-ttu-id="fd249-166">백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="fd249-166">Backup and restore</span></span>

<span data-ttu-id="fd249-167">운영 데이터베이스에 대한 가장 중요한 측면 중 하나는 다양한 치명적인 이벤트에서 데이터베이스를 보호할 수 있다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-167">One of the most important aspects to operating databases is making sure the database can be protected from various catastrophic events.</span></span> <span data-ttu-id="fd249-168">자연 재해부터 간단한 사용자 오류까지 다양한 원인으로 인해 이러한 이벤트가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-168">These events can be caused by anything from natural disasters to simple user errors.</span></span>

<span data-ttu-id="fd249-169">지정 시점(예: 누군가가 중요한 데이터를 삭제하기 전에)으로 복원하는 기능을 사용하여 데이터베이스를 백업하면 중단이 발생하기 전의 방식에 가장 가까운 상태로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-169">Backing up a database, with the ability to restore it to any point in time (such as before somebody deleted critical data), allows restoration to a state that is as close as possible to the way it was before the disruption occurred.</span></span>

<span data-ttu-id="fd249-170">최상의 결과를 위해 두 가지 백업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-170">Two types of backups must be performed for best results:</span></span>

- <span data-ttu-id="fd249-171">데이터베이스 백업</span><span class="sxs-lookup"><span data-stu-id="fd249-171">Database backups</span></span>
- <span data-ttu-id="fd249-172">트랜잭션 로그 백업</span><span class="sxs-lookup"><span data-stu-id="fd249-172">Transaction log backups</span></span>

<span data-ttu-id="fd249-173">응용 프로그램 수준에서 수행되는 전체 데이터베이스 백업 외에도 저장소 스냅숏에 백업을 수행하여 더욱 철저해질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-173">In addition to full database backups performed at an application-level, you can be even more thorough by performing backups with storage snapshots.</span></span> <span data-ttu-id="fd249-174">로그 백업을 수행하는 작업은 데이터베이스 복원에 중요하고 커밋된 트랜잭션에서 로그를 비우게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-174">Performing log backups is also important for restoring the database (and to empty the logs from already committed transactions).</span></span>

<span data-ttu-id="fd249-175">Azure(큰 인스턴스)의 SAP HANA는 다음과 같은 두 개의 백업과 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-175">SAP HANA on Azure (large instances) offers two backup and restore options:</span></span>

- <span data-ttu-id="fd249-176">DIY(Do It Yourself)</span><span class="sxs-lookup"><span data-stu-id="fd249-176">Do it yourself (DIY).</span></span> <span data-ttu-id="fd249-177">디스크 공간이 충분한지 계산한 후에 해당 디스크에 대한 디스크 백업 메서드를 사용하여 전체 데이터베이스 및 로그 백업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-177">After you calculate to ensure enough disk space, perform full database and log backups by using disk backup methods (to those disks).</span></span> <span data-ttu-id="fd249-178">사실상 무제한인 저장소로 Azure 기반 파일 서버를 설정한 후에 시간이 지남에 따라 백업은 Azure Storage 계정에 복사되거나 Azure Backup Vault 또는 Azure 콜드 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-178">Over time, the backups are copied to an Azure storage account (after you set up an Azure-based file server with virtually unlimited storage), or use an Azure Backup vault or Azure cold storage.</span></span> <span data-ttu-id="fd249-179">또 다른 옵션은 백업을 저장소 계정에 복사한 후에 저장하기 위해 Commvault와 같은 타사 데이터 보호 도구를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-179">Another option is to use a third-party data protection tool, such as Commvault, to store the backups after they are copied to a storage account.</span></span> <span data-ttu-id="fd249-180">DIY 백업 옵션은 준수 및 감사 목적으로 인해 장기간 저장되어야 하는 데이터에 필요할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-180">The DIY backup option might also be necessary for data that needs to be stored for longer periods for compliancy and auditing purposes.</span></span>
- <span data-ttu-id="fd249-181">Azure(큰 인스턴스)의 SAP HANA 기본 인프라가 제공하는 백업 및 복원 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-181">Use the backup and restore functionality that the underlying infrastructure of SAP HANA on Azure (large instances) provides.</span></span> <span data-ttu-id="fd249-182">이 옵션은 백업에 대한 필요성을 충족하고 데이터 백업이 규정 준수를 위해 필요한 경우를 제외하고 수동 백업을 거의 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-182">This option fulfills the need for backups, and it makes manual backups nearly obsolete (except where data backups are required for compliance purposes).</span></span> <span data-ttu-id="fd249-183">이 섹션의 나머지 부분에서는 HANA 큰 인스턴스와 함께 제공되는 백업 및 복원 기능을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-183">The rest of this section addresses the backup and restore functionality that's offered with HANA (large instances).</span></span>

> [!NOTE]
> <span data-ttu-id="fd249-184">HANA(큰 인스턴스)의 기본 인프라에서 사용하는 스냅숏 기술은 SAP HANA 스냅숏에 대한 종속성을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-184">The snapshot technology that is used by the underlying infrastructure of HANA (large instances) has a dependency on SAP HANA snapshots.</span></span> <span data-ttu-id="fd249-185">SAP HANA 스냅숏은 SAP HANA 다중 테넌트 데이터베이스 컨테이너와 함께 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-185">SAP HANA snapshots do not work in conjunction with SAP HANA Multitenant Database Containers.</span></span> <span data-ttu-id="fd249-186">결과적으로, SAP HANA 다중 테넌트 데이터베이스 컨테이너를 배포하는 데 백업의 메서드를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-186">As a result, this method of backup cannot be used to deploy SAP HANA Multitenant Database Containers.</span></span>

### <a name="using-storage-snapshots-of-sap-hana-on-azure-large-instances"></a><span data-ttu-id="fd249-187">Azure(큰 인스턴스)의 SAP HANA 저장소 스냅숏 사용</span><span class="sxs-lookup"><span data-stu-id="fd249-187">Using storage snapshots of SAP HANA on Azure (large instances)</span></span>

<span data-ttu-id="fd249-188">Azure(큰 인스턴스)의 SAP HANA에 기반한 저장소 인프라는 볼륨 저장소 스냅숏의 개념을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-188">The storage infrastructure underlying SAP HANA on Azure (large instances) supports the notion of a storage snapshot of volumes.</span></span> <span data-ttu-id="fd249-189">특정 볼륨의 백업 및 복원은 모두 다음 고려 사항으로 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-189">Both backup and restoration of a particular volume are supported, with the following considerations:</span></span>

- <span data-ttu-id="fd249-190">데이터베이스 백업 대신 저장소 볼륨 스냅숏을 자주 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-190">Instead of database backups, storage volume snapshots are taken on a frequent basis.</span></span>
- <span data-ttu-id="fd249-191">저장소 스냅숏은 저장소 스냅숏을 실행하기 전에 SAP HANA 스냅숏을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-191">The storage snapshot initiates an SAP HANA snapshot before it executes the storage snapshot.</span></span> <span data-ttu-id="fd249-192">이 SAP HANA 스냅숏은 저장소 스냅숏을 복구한 후에 최종 로그 복원에 대한 설치 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-192">This SAP HANA snapshot is the setup point for eventual log restorations after recovery of the storage snapshot.</span></span>
- <span data-ttu-id="fd249-193">저장소 스냅숏이 성공적으로 실행되는 시점에서 SAP HANA 스냅숏이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-193">At the point where the storage snapshot is executed successfully, the SAP HANA snapshot is deleted.</span></span>
- <span data-ttu-id="fd249-194">로그 백업은 자주 사용되며 로그 백업 볼륨 또는 Azure에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-194">Log backups are taken frequently and stored in the log backup volume or in Azure.</span></span>
- <span data-ttu-id="fd249-195">데이터베이스를 특정 시점으로 복원해야 하는 경우 특정 저장소 스냅숏을 복원(예: 샌드박스 시스템을 원래 상태로의 계획된 복원)하도록 Microsoft Azure 지원(프로덕션 작동 중단) 또는 Azure의 SAP HANA Service Management에 대한 요청이 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-195">If the database must be restored to a certain point in time, a request is made to Microsoft Azure Support (production outage) or SAP HANA on Azure Service Management to restore to a certain storage snapshot (for example, a planned restoration of a sandbox system to its original state).</span></span>
- <span data-ttu-id="fd249-196">저장소 스냅숏에 포함된 SAP HANA 스냅숏은 저장소 스냅숏을 만든 후에 실행되고 저장된 로그 백업에 적용하는 오프셋 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-196">The SAP HANA snapshot that's included in the storage snapshot is an offset point for applying log backups that have been executed and stored after the storage snapshot was taken.</span></span>
- <span data-ttu-id="fd249-197">이러한 로그 백업을 사용하여 데이터베이스를 다시 특정 시점으로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-197">These log backups are taken to restore the database back to a certain point in time.</span></span>

<span data-ttu-id="fd249-198">backup\_name을 지정하면 다음 볼륨의 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-198">Specifying the backup\_name creates a snapshot of the following volumes:</span></span>

- <span data-ttu-id="fd249-199">hana/data</span><span class="sxs-lookup"><span data-stu-id="fd249-199">hana/data</span></span>
- <span data-ttu-id="fd249-200">hana/log</span><span class="sxs-lookup"><span data-stu-id="fd249-200">hana/log</span></span>
- <span data-ttu-id="fd249-201">hana/log\_backup(hana/log에 백업으로 탑재됨)</span><span class="sxs-lookup"><span data-stu-id="fd249-201">hana/log\_backup (mounted as backup into hana/log)</span></span>
- <span data-ttu-id="fd249-202">hana/shared</span><span class="sxs-lookup"><span data-stu-id="fd249-202">hana/shared</span></span>

### <a name="storage-snapshot-considerations"></a><span data-ttu-id="fd249-203">저장소 스냅숏 고려 사항</span><span class="sxs-lookup"><span data-stu-id="fd249-203">Storage snapshot considerations</span></span>

>[!NOTE]
><span data-ttu-id="fd249-204">추가 저장소 공간이 할당되어야 하기 때문에 저장소 스냅숏은 무료로 제공되지 _않습니다_.</span><span class="sxs-lookup"><span data-stu-id="fd249-204">Storage snapshots are _not_ provided free of charge, because additional storage space must be allocated.</span></span>

<span data-ttu-id="fd249-205">Azure(큰 인스턴스)의 SAP HANA에 대한 저장소 스냅숏의 특정 역학에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-205">The specific mechanics of storage snapshots for SAP HANA on Azure (large instances) include:</span></span>

- <span data-ttu-id="fd249-206">만들어진 시점에서 특정 저장소 스냅숏은 아주 작은 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-206">A specific storage snapshot (at the point in time when it is taken) consumes very little storage.</span></span>
- <span data-ttu-id="fd249-207">SAP HANA 데이터 파일의 데이터 콘텐츠 변경 내용 및 콘텐츠는 저장소 볼륨에서 변경되고 스냅숏은 원래 블록 콘텐츠를 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-207">As data content changes and the content in SAP HANA data files change on the storage volume, the snapshot needs to store the original block content.</span></span>
- <span data-ttu-id="fd249-208">저장소 스냅숏의 크기가 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-208">The storage snapshot increases in size.</span></span> <span data-ttu-id="fd249-209">스냅숏이 오래 존재할수록 저장소 스냅숏은 커집니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-209">The longer the snapshot exists, the larger the storage snapshot becomes.</span></span>
- <span data-ttu-id="fd249-210">스토리지 스냅샷의 수명 동안 SAP HANA 데이터베이스 볼륨에 변경 내용이 많을수록 스토리지 스냅샷이 소진하는 공간이 커집니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-210">The more changes made to the SAP HANA database volume over the lifetime of a storage snapshot, the larger the space consumption of the storage snapshot becomes.</span></span>

<span data-ttu-id="fd249-211">Azure(큰 인스턴스)의 SAP HANA는 SAP HANA 데이터 및 로그 볼륨에 대한 고정된 볼륨 크기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-211">SAP HANA on Azure (large instances) comes with fixed volume sizes for the SAP HANA data and log volume.</span></span> <span data-ttu-id="fd249-212">해당 볼륨의 스냅숏을 수행하면 사용자의 볼륨 공간을 사용하게 되므로 Azure의 SAP HANA [큰 인스턴스] 프로세스 내에서 저장소 스냅숏을 예약해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-212">Performing snapshots of those volumes eats into your volume space, so it is your responsibility to schedule storage snapshots (within the SAP HANA on Azure [large instances] process).</span></span>

<span data-ttu-id="fd249-213">다음 섹션에서는 일반적인 권장 사항을 비롯한 이러한 스냅숏을 수행하는 방법에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-213">The following sections provide information for performing these snapshots, including general recommendations:</span></span>

- <span data-ttu-id="fd249-214">하드웨어가 볼륨당 255개의 스냅숏을 유지할 수 있지만 이 숫자보다 훨씬 낮게 유지하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-214">Though the hardware can sustain 255 snapshots per volume, we highly recommend that you stay well below this number.</span></span>
- <span data-ttu-id="fd249-215">스냅숏 저장소를 수행하기 전에 여유 공간을 모니터링하고 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-215">Before you perform storage snapshots, monitor and keep track of free space.</span></span>
- <span data-ttu-id="fd249-216">사용 가능한 공간에 따라 저장소 스냅숏의 수를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-216">Lower the number of storage snapshots based on free space.</span></span> <span data-ttu-id="fd249-217">유지할 수 있는 스냅숏 수를 줄이거나 볼륨을 확장해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-217">You might need to lower the number of snapshots that you keep, or you might need to extend the volumes.</span></span> <span data-ttu-id="fd249-218">(추가 저장소를 1TB 단위로 주문할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="fd249-218">(You can order additional storage in 1-TB units.)</span></span>
- <span data-ttu-id="fd249-219">시스템 마이그레이션 도구(R3load 또는 백업에서 SAP HANA 데이터베이스 복원)를 사용하여 SAP HANA에 데이터를 이동하는 것과 같은 작업 중에 저장소 스냅숏을 수행하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-219">During activities such as moving data into SAP HANA with system migration tools (with R3load, or by restoring SAP HANA databases from backups), we highly recommended that you not perform any storage snapshots.</span></span> <span data-ttu-id="fd249-220">(시스템 마이그레이션이 새 SAP HANA 시스템에서 수행되는 경우 저장소 스냅숏을 수행할 필요가 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="fd249-220">(If a system migration is being done on a new SAP HANA system, storage snapshots would not need to be performed.)</span></span>
- <span data-ttu-id="fd249-221">SAP HANA 테이블을 크게 재구성하는 동안 저장소 스냅숏을 가능하면 사용하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-221">During larger reorganizations of SAP HANA tables, storage snapshots should be avoided if possible.</span></span>
- <span data-ttu-id="fd249-222">저장소 스냅숏은 Azure(큰 인스턴스)의 SAP HANA 중 재해 복구 기능을 수행하는 필수 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-222">Storage snapshots are a prerequisite to engaging the disaster-recovery capabilities of SAP HANA on Azure (large instances).</span></span>

### <a name="setting-up-storage-snapshots"></a><span data-ttu-id="fd249-223">저장소 스냅숏 설정</span><span class="sxs-lookup"><span data-stu-id="fd249-223">Setting up storage snapshots</span></span>

1. <span data-ttu-id="fd249-224">Perl이 HANA(큰 인스턴스) 서버의 Linux 운영 체제에 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-224">Make sure that Perl is installed in the Linux operating system on the HANA (large instances) server.</span></span>
2. <span data-ttu-id="fd249-225">/etc/ssh/ssh\_config를 수정하여 _MACs hmac-sha1_ 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-225">Modify /etc/ssh/ssh\_config to add the line _MACs hmac-sha1_.</span></span>
3. <span data-ttu-id="fd249-226">적용할 수 있는 경우 실행하는 SAP HANA 인스턴스마다 마스터 노드에서 SAP HANA 백업 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-226">Create an SAP HANA backup user account on the master node for each SAP HANA instance you are running (if applicable).</span></span>
4. <span data-ttu-id="fd249-227">SAP HANA HDB 클라이언트는 모든 SAP HANA(큰 인스턴스) 서버에 설치되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-227">The SAP HANA HDB client must be installed on all SAP HANA (large instances) servers.</span></span>
5. <span data-ttu-id="fd249-228">각 지역의 첫 번째 SAP HANA(큰 인스턴스) 서버에서 스냅숏 생성을 제어하는 기본 저장소 인프라에 액세스하기 위해 공개 키를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-228">On the first SAP HANA (large instances) server of each region, a public key must be created to access the underlying storage infrastructure that controls snapshot creation.</span></span>
6. <span data-ttu-id="fd249-229">azure\_hana\_backup.pl 스크립트를 /scripts에서 SAP HANA 설치의 **hdbsql** 위치에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-229">Copy the script azure\_hana\_backup.pl from /scripts to the location of **hdbsql** of the SAP HANA installation.</span></span>
7. <span data-ttu-id="fd249-230">HANABackupDetails.txt 파일을 /scripts에서 Perl 스크립트와 동일한 위치에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-230">Copy the HANABackupDetails.txt file from /scripts to the same location as the Perl script.</span></span>
8. <span data-ttu-id="fd249-231">적절한 고객 사양에 대한 필요에 따라 HANABackupDetails.txt 파일을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-231">Modify the HANABackupDetails.txt file as necessary for the appropriate customer specifications.</span></span>

### <a name="step-1-install-sap-hana-hdbclient"></a><span data-ttu-id="fd249-232">1단계: SAP HANA HDBClient 설치</span><span class="sxs-lookup"><span data-stu-id="fd249-232">Step 1: Install SAP HANA HDBClient</span></span>

<span data-ttu-id="fd249-233">Azure(큰 인스턴스)의 SAP HANA에 설치된 Linux는 백업 및 재해 복구를 위해 SAP HANA 저장소 스냅숏을 실행하는 데 필요한 폴더와 스크립트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-233">The Linux installed on SAP HANA on Azure (large instances) includes the folders and scripts necessary to execute SAP HANA storage snapshots for backup and disaster-recovery purposes.</span></span> <span data-ttu-id="fd249-234">그러나 SAP HANA를 설치하는 동안 SAP HANA HDBclient를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-234">However, it is your responsibility to install SAP HANA HDBclient while you are installing SAP HANA.</span></span> <span data-ttu-id="fd249-235">(Microsoft에서는 HDBclient나 SAP HANA를 모두 설치하지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="fd249-235">(Microsoft installs neither the HDBclient nor SAP HANA.)</span></span>

### <a name="step-2-change-etcsshsshconfig"></a><span data-ttu-id="fd249-236">2단계: /etc/ssh/ssh\_config 변경</span><span class="sxs-lookup"><span data-stu-id="fd249-236">Step 2: Change /etc/ssh/ssh\_config</span></span>

<span data-ttu-id="fd249-237">여기에 표시된 _MACs hmac-sha1_ 줄을 추가하여 /etc/ssh/ssh\_config를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-237">Change /etc/ssh/ssh\_config by adding _MACs hmac-sha1_ line as shown here:</span></span>
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

### <a name="step-3-create-a-public-key"></a><span data-ttu-id="fd249-238">3단계: 공개 키 만들기</span><span class="sxs-lookup"><span data-stu-id="fd249-238">Step 3: Create a public key</span></span>

<span data-ttu-id="fd249-239">각 Azure 지역의 첫 번째 Azure(큰 인스턴스)의 SAP HANA 서버에서 스냅숏을 만들 수 있도록 저장소 인프라에 액세스하는 데 사용되는 공개 키를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-239">On the first SAP HANA on Azure (large instances) server in each Azure region, create a public key to be used to access the storage infrastructure so that you can create snapshots.</span></span> <span data-ttu-id="fd249-240">공개 키를 통해 저장소에 로그인하는 데 암호를 요구하지 않도록 하면 해당 암호 자격 증명이 유지되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-240">The public key ensures that a password is not required to sign in to the storage and that password credentials are not maintained.</span></span> <span data-ttu-id="fd249-241">SAP HANA(큰 인스턴스) 서버의 Linux에서 공개 키를 생성하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-241">In Linux on the SAP HANA (large instances) server, execute the following command to generate the public key:</span></span>
```
  ssh-keygen –t dsa –b 1024
```
<span data-ttu-id="fd249-242">새 위치는 _/root/.ssh/id\_dsa.pub입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-242">The new location is _/root/.ssh/id\_dsa.pub.</span></span> <span data-ttu-id="fd249-243">실제 암호를 입력하지 마세요. 그렇지 않으면 로그인할 때마다 암호를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-243">Do not enter an actual passphrase, or else you will be required to enter the passphrase each time you sign in.</span></span> <span data-ttu-id="fd249-244">대신, **Enter**를 두 번 눌러서 로그인에 대한 입력 암호 요구 사항을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-244">Instead, press **Enter** twice to remove the enter passphrase requirement for signing in.</span></span>

<span data-ttu-id="fd249-245">폴더를 /root/.ssh/로 변경한 다음 **ls** 명령을 실행하여 예상 대로 공개 키가 수정되었는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-245">Check to make sure that the public key was corrected as expected by changing folders to /root/.ssh/ and then executing the **ls** command.</span></span> <span data-ttu-id="fd249-246">키가 있는 경우 다음 명령을 실행하여 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-246">If the key is present, you can copy it by running the following command:</span></span>

![이 명령을 실행하여 공개 키를 복사합니다.](./media/hana-overview-high-availability-disaster-recovery/image2-public-key.png)

<span data-ttu-id="fd249-248">이 시점에서 Azure Service Management의 SAP HANA에 문의하고 키를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-248">At this point, contact SAP HANA on Azure Service Management and provide the key.</span></span> <span data-ttu-id="fd249-249">서비스 담당자는 공개 키를 사용하여 기본 저장소 인프라에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-249">The service representative uses the public key to register it in the underlying storage infrastructure.</span></span>

### <a name="step-4-create-an-sap-hana-user-account"></a><span data-ttu-id="fd249-250">4단계: SAP HANA 사용자 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="fd249-250">Step 4: Create an SAP HANA user account</span></span>

<span data-ttu-id="fd249-251">백업을 목적으로 SAP HANA Studio 내에서 SAP HANA 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-251">Create an SAP HANA user account within SAP HANA Studio for backup purposes.</span></span> <span data-ttu-id="fd249-252">이 계정에는 _백업 관리_ 및 _카탈로그 읽기_ 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-252">This account must have the following privileges: _Backup Admin_ and _Catalog Read_.</span></span> <span data-ttu-id="fd249-253">이 예제에서는 사용자 이름 SCADMIN을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-253">In this example, the username SCADMIN is created.</span></span>

![HANA Studio에서 사용자 만들기](./media/hana-overview-high-availability-disaster-recovery/image3-creating-user.png)

### <a name="step-5-authorize-the-sap-hana-user-account"></a><span data-ttu-id="fd249-255">5단계: SAP HANA 사용자 계정 권한 부여</span><span class="sxs-lookup"><span data-stu-id="fd249-255">Step 5: Authorize the SAP HANA user account</span></span>

<span data-ttu-id="fd249-256">스크립트를 실행할 때마다 권한 부여를 요구하지 않고 스크립트에 의해 사용되는 SAP HANA 사용자 계정에 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-256">Authorize the SAP HANA user account (to be used by the scripts without requiring authorization every time the script is run).</span></span> <span data-ttu-id="fd249-257">SAP HANA 명령 `hdbuserstore`을 사용하면 하나 이상의 SAP HANA 노드에 저장되는 SAP HANA 사용자 키를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-257">The SAP HANA command `hdbuserstore` allows the creation of an SAP HANA user key, which is stored on one or more SAP HANA nodes.</span></span> <span data-ttu-id="fd249-258">또한 사용자 키를 사용하면 나중에 설명할 스크립팅 프로세스 내에서 암호를 관리하지 않고도 SAP HANA에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-258">The user key also allows the user to access SAP HANA without having to manage passwords from within the scripting process that's discussed later.</span></span>

>[!IMPORTANT]
><span data-ttu-id="fd249-259">다음 명령을 `_root_`로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-259">Run the following command as `_root_`.</span></span> <span data-ttu-id="fd249-260">그렇지 않으면 스크립트가 제대로 작동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-260">Otherwise, the script cannot work properly.</span></span>

<span data-ttu-id="fd249-261">`hdbuserstore` 명령을 다음과 같이 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-261">Enter the `hdbuserstore` command as follows:</span></span>

![hdbuserstore 명령을 입력합니다.](./media/hana-overview-high-availability-disaster-recovery/image4-hdbuserstore-command.png)

<span data-ttu-id="fd249-263">사용자가 SCADMIN01이고 호스트 이름이 lhanad01인 다음 예제에서 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-263">In the following example, where the user is SCADMIN01 and the hostname is lhanad01, the command is:</span></span>
```
hdbuserstore set SCADMIN01 lhanad01:30115 <backup username> <password>
```
<span data-ttu-id="fd249-264">확장 HANA 인스턴스의 단일 서버에서 모든 스크립트를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-264">Manage all scripting from a single server for scale-out HANA instances.</span></span> <span data-ttu-id="fd249-265">이 예제에서는 키에 관련된 호스트를 반영하는 방식으로 각 호스트에 대해 SAP HANA 키 SCADMIN01를 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-265">In this example, the SAP HANA key SCADMIN01 must be altered for each host in a way that reflects the host that is related to the key.</span></span> <span data-ttu-id="fd249-266">즉, SAP HANA 백업 계정은 **lhanad**라는 HANA DB의 인스턴스 번호를 사용하여 수정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-266">That is, the SAP HANA backup account is amended with the instance number of the HANA DB, **lhanad**.</span></span> <span data-ttu-id="fd249-267">키는 할당된 호스트에 대한 관리자 권한이 있어야 하며, 확장에 대한 백업 사용자는 모든 SAP HANA 인스턴스에 대한 액세스 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-267">The key must have administrative privileges on the host it is assigned to, and the backup user for scale-out must have access rights to all SAP HANA instances.</span></span>
```
hdbuserstore set SCADMIN01 lhanad:30015 SCADMIN <password>
hdbuserstore set SCADMIN02 lhanad:30115 SCADMIN <password>
hdbuserstore set SCADMIN03 lhanad:30215 SCADMIN <password>
```

### <a name="step-6-copy-items-from-the-scripts-folder"></a><span data-ttu-id="fd249-268">6단계: /scripts 폴더에서 항목 복사</span><span class="sxs-lookup"><span data-stu-id="fd249-268">Step 6: Copy items from the /scripts folder</span></span>

<span data-ttu-id="fd249-269">설치의 골드 이미지에 포함된 /scripts 폴더에서 **hdbsql**에 대한 작업 디렉터리까지 다음 항목을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-269">Copy the following items from the /scripts folder (included on the gold image of the installation) to the working directory for **hdbsql**.</span></span> <span data-ttu-id="fd249-270">현재 HANA 설치의 경우 이 디렉터리는 /hana/shared/D01/exe/linuxx86\_64/hdb입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-270">For current HANA installations, this directory is /hana/shared/D01/exe/linuxx86\_64/hdb.</span></span>
```
azure\_hana\_backup.pl
testHANAConnection.pl
testStorageSnapshotConnection.pl
removeTestStorageSnapshot.pl
HANABackupCustomerDetails.txt
```
<span data-ttu-id="fd249-271">확장 또는 OLAP를 실행 중인 경우 다음 항목을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-271">Copy the following items if they are running scale-out or OLAP:</span></span>
```
azure\_hana\_backup\_bw.pl
testHANAConnectionBW.pl
testStorageSnapshotConnectionBW.pl
removeTestStorageSnapshotBW.pl
HANABackupCustomerDetailsBW.txt
```
<span data-ttu-id="fd249-272">HANABackupCustomerDetails.txt 파일은 강화 배포의 경우 다음과 같이 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-272">The HANABackupCustomerDetails.txt file is modifiable as follows for a scale-up deployment.</span></span> <span data-ttu-id="fd249-273">저장소 스냅숏을 실행하는 스크립트의 컨트롤 및 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-273">It is the control and configuration file for the script that runs the storage snapshots.</span></span> <span data-ttu-id="fd249-274">사용자의 인스턴스를 배포한 Azure의 SAP HANA Service Management에서 _저장소 백업 이름_ 및 _저장소 IP 주소_를 수신했어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-274">You should have received the _Storage Backup Name_ and _Storage IP Address_ from SAP HANA on Azure Service Management when your instances were deployed.</span></span> <span data-ttu-id="fd249-275">변수의 시퀀스, 순서 또는 간격을 수정할 수 없습니다. 그렇지 않으면 스크립트가 제대로 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-275">You cannot modify the sequence, ordering, or spacing of any of the variables, or the script does not run properly.</span></span>

<span data-ttu-id="fd249-276">강화 배포의 경우 구성 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-276">For a scale-up deployment, the configuration file would look like:</span></span>
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Created by customer using hdbuserstore
HANA Backup Name: SCADMIND01
```
<span data-ttu-id="fd249-277">확장 구성의 경우 HANABackupCustomerDetailsBW.txt 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-277">For a scale-out configuration, the HANABackupCustomerDetailsBW.txt file would look like:</span></span>
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
><span data-ttu-id="fd249-278">현재 노드 1 세부 정보만 실제 HANA 저장소 스냅숏 스크립트에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-278">Currently, only Node 1 details are used in the actual HANA storage snapshot script.</span></span> <span data-ttu-id="fd249-279">마스터 백업 노드가 변경되는 경우 노드 1의 세부 정보를 수정하여 다른 노드가 해당 위치를 사용할 수 있도록 모든 HANA 노드 간의 액세스를 테스트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-279">We recommend that you test access to or from all HANA nodes so that, if the master backup node ever changes, you have already ensured that any other node can take its place by modifying the details in Node 1.</span></span>

<span data-ttu-id="fd249-280">구성 파일에서 올바른 구성 또는 HANA 인스턴스에 대한 적절한 연결을 확인하려면 다음 스크립트 중 하나를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-280">To check for the correct configurations in the configuration file or proper connectivity to the HANA instances, run either of the following scripts:</span></span>
- <span data-ttu-id="fd249-281">강화 구성의 경우(SAP 워크로드에 독립적임):</span><span class="sxs-lookup"><span data-stu-id="fd249-281">For a scale-up configuration (independent on SAP workload):</span></span>

 ```
testHANAConnection.pl
```
- <span data-ttu-id="fd249-282">확장 구성의 경우:</span><span class="sxs-lookup"><span data-stu-id="fd249-282">For a scale-out configuration:</span></span>

 ```
testHANAConnectionBW.pl
```

<span data-ttu-id="fd249-283">마스터 HANA 인스턴스에 모든 필수 HANA 서버에 대한 액세스 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-283">Ensure that the master HANA instance has access to all required HANA servers.</span></span> <span data-ttu-id="fd249-284">스크립트에 대한 매개 변수가 없지만 스크립트를 적절하게 실행하려면 HANABackupCustomerDetails/ HANABackupCustomerDetailsBW 파일을 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-284">There are no parameters to the script, but you must complete the appropriate HANABackupCustomerDetails/ HANABackupCustomerDetailsBW file for the script to run properly.</span></span> <span data-ttu-id="fd249-285">셸 명령 오류 코드만 반환되기 때문에 스크립트가 모든 인스턴스의 오류를 검사하는 것은 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-285">Because only the shell command error codes are returned, it is not possible for the script to error-check every instance.</span></span> <span data-ttu-id="fd249-286">이런 경우에도 스크립트는 다시 확인하기 위한 몇 가지 유용한 설명을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-286">Even so, the script does provide some helpful comments for you to double-check.</span></span>

<span data-ttu-id="fd249-287">스크립트를 실행하려면</span><span class="sxs-lookup"><span data-stu-id="fd249-287">To run the script:</span></span>
```
 ./testHANAConnection.pl
```
 <span data-ttu-id="fd249-288">스크립트가 HANA 인스턴스의 상태를 가져오는 데 성공한 경우 HANA 연결이 성공적이라는 메시지를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-288">If the script successfully obtains the status of the HANA instance, it displays a message that the HANA connection was successful.</span></span>

<span data-ttu-id="fd249-289">또한 저장소에 로그인하는 마스터 HANA 인스턴스 서버의 기능을 확인하는 데 사용할 수 있는 스크립트의 두 번째 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-289">Additionally, there is a second type of script you can use to check the master HANA instance server's ability to sign in to the storage.</span></span> <span data-ttu-id="fd249-290">azure\_hana\_backup(\_bw).pl 스크립트를 실행하기 전에 다음 스크립트를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-290">Before you execute the azure\_hana\_backup(\_bw).pl script, you must execute the next script.</span></span> <span data-ttu-id="fd249-291">볼륨에 스냅숏이 없는 경우 볼륨이 단순히 비어 있는지 아니면 스냅숏 정보를 포함한 ssh 오류가 있는지를 결정하는 것이 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-291">If a volume contains no snapshots, it is impossible to determine whether the volume is simply empty or there is an ssh failure to obtain the snapshot details.</span></span> <span data-ttu-id="fd249-292">이러한 이유로 스크립트는 다음 두 단계를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-292">For this reason, the script executes two steps:</span></span>

- <span data-ttu-id="fd249-293">저장소 콘솔에 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-293">It verifies that the storage console is accessible.</span></span>
- <span data-ttu-id="fd249-294">HANA 인스턴스에서 각 볼륨의 테스트, 더미 또는 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-294">It creates a test, or dummy, snapshot for each volume by HANA instance.</span></span>

<span data-ttu-id="fd249-295">이러한 이유로 HANA 인스턴스를 인수로 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-295">For this reason, the HANA instance is included as an argument.</span></span> <span data-ttu-id="fd249-296">마찬가지로 저장소 연결에 대한 오류 검사를 제공할 수 없지만 실행이 실패하는 경우 스크립트는 유용한 힌트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-296">Again, it is not possible to provide error checking for the storage connection, but the script provides helpful hints if the execution fails.</span></span>

<span data-ttu-id="fd249-297">스크립트는 다음의 경우 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-297">The script is run as:</span></span>
```
 ./testStorageSnapshotConnection.pl <hana instance>
```
<span data-ttu-id="fd249-298">또는 다음의 경우 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-298">Or it is run as:</span></span>
```
./testStorageSnapshotConnectionBW.pl <hana instance>
```
<span data-ttu-id="fd249-299">또한 스크립트는 배포된 저장소 테넌트에 적절하게 로그인할 수 있다는 메시지를 표시합니다. 해당 테넌트는 사용자가 소유한 서버 인스턴스에서 사용하는 LUN(논리적 단위 수)으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-299">The script also displays a message that you are able to sign in appropriately to your deployed storage tenant, which is organized around the logical unit numbers (LUNs) that are used by the server instances you own.</span></span>

<span data-ttu-id="fd249-300">첫 번째 저장소 스냅숏 기반 백업을 실행하기 전에 이러한 스크립트를 실행하여 구성이 올바른지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-300">Before you execute the first storage snapshot-based backups, run the next scripts to make sure that the configuration is correct.</span></span>

<span data-ttu-id="fd249-301">이러한 스크립트를 실행한 후에 다음을 실행하여 스냅숏을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-301">After running these scripts, you can delete the snapshots by executing:</span></span>
```
./removeTestStorageSnapshot.pl <hana instance>
```
<span data-ttu-id="fd249-302">또는</span><span class="sxs-lookup"><span data-stu-id="fd249-302">Or</span></span>
```
./removeTestStorageSnapshot.pl <hana instance>
```

### <a name="step-7-perform-on-demand-snapshots"></a><span data-ttu-id="fd249-303">7단계: 주문형 스냅숏 수행</span><span class="sxs-lookup"><span data-stu-id="fd249-303">Step 7: Perform on-demand snapshots</span></span>

<span data-ttu-id="fd249-304">여기에서 설명한 대로 주문형 스냅숏을 수행할 뿐만 아니라 cron를 사용하여 일반 스냅숏을 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-304">Perform on-demand snapshots (as well as schedule regular snapshots by using cron) as described here.</span></span>

<span data-ttu-id="fd249-305">강화 구성의 경우 다음 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-305">For scale-up configurations, execute the following script:</span></span>
```
./azure_hana_backup.pl lhanad01 customer 20
```
<span data-ttu-id="fd249-306">확장 구성의 경우 다음 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-306">For scale-out configurations, execute the following script:</span></span>
```
./azure_hana_backup_bw.pl lhanad01 customer 20
```
<span data-ttu-id="fd249-307">확장 스크립트는 모든 HANA 서버에 액세스할 수 있도록 추가 검사를 수행하고, 모든 HANA 인스턴스는 SAP HANA 또는 저장소 스냅숏을 계속 만들기 전에 적절한 인스턴스 상태를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-307">The scale-out script does some additional checking to make sure that all HANA servers can be accessed, and all HANA instances return appropriate status of the instance before proceeding with creating SAP HANA or storage snapshots.</span></span>

<span data-ttu-id="fd249-308">다음과 같은 인수가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-308">The following arguments are required:</span></span>

- <span data-ttu-id="fd249-309">HANA 인스턴스 요구 백업</span><span class="sxs-lookup"><span data-stu-id="fd249-309">The HANA instance requiring backup.</span></span>
- <span data-ttu-id="fd249-310">저장소 스냅숏의 스냅숏 접두사</span><span class="sxs-lookup"><span data-stu-id="fd249-310">The snapshot prefix for the storage snapshot.</span></span>
- <span data-ttu-id="fd249-311">특정 접두사에 대해 유지되는 스냅숏 개수</span><span class="sxs-lookup"><span data-stu-id="fd249-311">The number of snapshots to be kept for the specific prefix.</span></span>

```
./azure_hana_backup.pl lhanad01 customer 20
```

<span data-ttu-id="fd249-312">스크립트를 실행하면 이러한 세 가지 단계에서 저장소 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-312">The execution of the script creates the storage snapshot in these three distinct phases:</span></span>

- <span data-ttu-id="fd249-313">HANA 스냅숏을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-313">Execute a HANA snapshot.</span></span>
- <span data-ttu-id="fd249-314">저장소 스냅숏을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-314">Execute a storage snapshot.</span></span>
- <span data-ttu-id="fd249-315">HANA 스냅숏을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-315">Remove the HANA snapshot.</span></span>

<span data-ttu-id="fd249-316">스크립트가 복사되었던 HDB 실행 파일 폴더에서 호출하여 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-316">Execute the script by calling it from the HDB executable folder that it was copied to.</span></span> <span data-ttu-id="fd249-317">최소한 다음 볼륨을 백업하지만 볼륨 이름에 명시적 SAP HANA 인스턴스 이름을 가진 모든 볼륨도 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-317">It backs up at least the following volumes, but it also backs up any volume that has the explicit SAP HANA instance name in the volume name.</span></span>
```
hana_data_<hana instance>_prod_t020_vol
hana_log_<hana instance>_prod_t020_vol
hana_log_backup_<hana instance>_prod_t020_vol
hana_shared_<hana instance>_prod_t020_vol
```
<span data-ttu-id="fd249-318">보존 기간은 스크립트를 실행할 경우 매개 변수로 제출되는 스냅숏 개수와 함께 엄격하게 관리됩니다(예: 20처럼 이전에 표시됨).</span><span class="sxs-lookup"><span data-stu-id="fd249-318">The retention period is strictly administered, with the number of snapshots submitted as a parameter when you execute the script (such as 20, shown previously).</span></span> <span data-ttu-id="fd249-319">따라서 시간의 양은 스크립트의 호출에서 실행 기간 및 스냅숏 개수의 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-319">So the amount of time is a function of the period of execution and the number of snapshots in the call of the script.</span></span> <span data-ttu-id="fd249-320">유지되는 스냅숏 개수가 스냅숏 스크립트의 호출에서 매개 변수로 이름이 지정된 수를 초과하면 새 스냅숏을 실행하기 전에 이 레이블의 가장 오래된 저장소가 삭제됩니다(앞의 경우 _사용자 지정_).</span><span class="sxs-lookup"><span data-stu-id="fd249-320">If the number of snapshots that are kept exceeds the number that are named as a parameter in the call of the script, the oldest storage snapshot of this label (in our previous case, _custom_) is deleted before a new snapshot is executed.</span></span> <span data-ttu-id="fd249-321">즉, 호출의 마지막 매개 변수로 지정한 숫자는 스냅숏 개수를 제어하는 데 사용할 수 있는 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-321">This means the number you give as the last parameter of the call is the number you can use to control the number of snapshots.</span></span>

>[!NOTE]
><span data-ttu-id="fd249-322">레이블을 변경하면 즉시 계수가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-322">As soon as you change the label, the counting starts again.</span></span>

<span data-ttu-id="fd249-323">다중 노드 환경에서 스냅숏을 만드는 경우 Azure의 SAP HANA Service Management에서 인수로 제공하는 HANA 인스턴스 이름을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-323">You need to include the HANA instance name that's provided by SAP HANA on Azure Service Management as an argument if they are creating snapshots in multi-node environments.</span></span> <span data-ttu-id="fd249-324">단일 노드 환경에서 Azure(큰 인스턴스)의 SAP HANA 단위의 이름도 충분하지만 HANA 인스턴스 이름을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-324">In single-node environments, the name of the SAP HANA on Azure (large instances) unit is sufficient, but the HANA instance name is still recommended.</span></span>

<span data-ttu-id="fd249-325">또한 동일한 스크립트를 사용하여 부팅 volumes\LUNs를 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-325">Additionally, you can back up boot volumes\LUNs by using the same script.</span></span> <span data-ttu-id="fd249-326">처음 HANA를 실행하는 경우 한 번 이상 부팅 볼륨을 백업해야 합니다. 하지만 cron의 부팅에 대해 주간 또는 야간 백업 일정을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-326">You must back up your boot volume at least once when you first run HANA, although we recommend a weekly or nightly backup schedule for booting in cron.</span></span> <span data-ttu-id="fd249-327">SAP HANA 인스턴스 이름을 추가하는 대신 다음과 같이 스크립트에 _부팅_을 인수로 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-327">Rather than add an SAP HANA instance name, insert _boot_ as the argument into the script as follows:</span></span>
```
./azure_hana_backup boot customer 20
```
<span data-ttu-id="fd249-328">부팅 볼륨에도 동일한 보존 정책을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-328">The same retention policy is afforded to the boot volume as well.</span></span> <span data-ttu-id="fd249-329">앞에 설명한 대로 특별한 경우에만 주문형 스냅숏을 사용합니다(예: SAP EHP(Enhancement Package) 업그레이드 중 또는 고유한 저장소 스냅숏을 만들어야 하는 경우).</span><span class="sxs-lookup"><span data-stu-id="fd249-329">Use on-demand snapshots, as described previously, for special cases only, such as during an SAP enhancement package (EHP) upgrade, or when you need to create a distinct storage snapshot.</span></span>

<span data-ttu-id="fd249-330">cron를 사용하여 예약된 저장소 스냅숏을 수행하는 것이 좋으며, 모든 백업 및 재해 복구 요구 사항에 동일한 스크립트를 사용하는 것이 좋습니다(요청된 다른 백업 시간과 일치하도록 스크립트 입력 수정).</span><span class="sxs-lookup"><span data-stu-id="fd249-330">We encourage you to perform scheduled storage snapshots using cron, and we recommend that you use the same script for all backups and disaster-recovery needs (modifying the script inputs to match the various requested backup times).</span></span> <span data-ttu-id="fd249-331">해당 실행 시간(매시간, 12시간, 매일 또는 매주)에 따라 cron에서 모두 다르게 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-331">These are all scheduled differently in cron depending on their execution time: hourly, 12-hour, daily, or weekly.</span></span> <span data-ttu-id="fd249-332">장기 오프사이트 백업의 경우 cron 일정은 앞에 설명한 보존 레이블과 일치하는 저장소 스냅숏을 만들도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-332">The cron schedule is designed to create storage snapshots that match the previously discussed retention labeling for long-term off-site backup.</span></span> <span data-ttu-id="fd249-333">스크립트는 요청된 해당 빈도에 따라 모든 프로덕션 볼륨을 백업하는 명령을 포함합니다. 데이터 및 로그 파일이 매시간 백업되는 반면 부팅 볼륨은 매일 백업됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-333">The script includes commands to back up all production volumes, depending on their requested frequency (data and log files are backed up hourly, whereas the boot volume is backed up daily).</span></span>

<span data-ttu-id="fd249-334">다음 cron 스크립트에 있는 항목은 매시간 10분 단위, 12시간마다 10분 단위 및 매일 10분 단위로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-334">The entries in the following cron script run every hour at the tenth minute, every 12 hours at the tenth minute, and daily at the tenth minute.</span></span> <span data-ttu-id="fd249-335">cron 작업은 특정 시간 동안 하나의 SAP HANA 저장소 스냅숏을 만드는 방식으로 만들어집니다. 따라서 매시간 및 매일 백업은 동시에(오전 12시 10분) 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-335">The cron jobs are created in such a way that only one SAP HANA storage snapshot takes place during any particular hour, so that the hourly and daily backups do not occur at the same time (12:10 AM).</span></span> <span data-ttu-id="fd249-336">Azure의 SAP HANA Service Management에서는 스냅숏 생성 및 복제를 최적화하기 위해 백업을 실행하는 사용자에게 권장된 시간을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-336">To help optimize your snapshot creation and replication, SAP HANA on Azure Service Management provides the recommended time for you to run your backups.</span></span>

<span data-ttu-id="fd249-337">/etc/crontab에서 예약된 기본 cron은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-337">The default cron scheduling in /etc/crontab is as follows:</span></span>
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 14
```
<span data-ttu-id="fd249-338">앞의 cron 지침에서 부팅 볼륨 없는 HANA 볼륨은 레이블의 스냅숏을 매시간 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-338">In the previous cron instructions, the HANA volumes (without boot volume) get an hourly snapshot with the label.</span></span> <span data-ttu-id="fd249-339">이러한 66개의 스냅숏이 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-339">Of these snapshots, 66 are retained.</span></span> <span data-ttu-id="fd249-340">또한 12시간 레이블을 포함한 14 스냅숏이 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-340">Additionally, 14 snapshots with the 12-hour label are retained.</span></span> <span data-ttu-id="fd249-341">잠재적으로 3일 간의 매시간 스냅숏에 추가로 4일 간의 12시간 스냅숏을 얻게 되어 한 주 간의 스냅숏을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-341">You potentially get hourly snapshots for three days, plus 12-hour snapshots for another four days, which gives you an entire week of snapshots.</span></span>

<span data-ttu-id="fd249-342">스크립트가 몇 분 사이에 엇갈리게 배치되지 않는 한 특정 시간에 하나의 스크립트만을 실행해야 하기 때문에 cron 내에서 예약 작업은 복잡할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-342">Scheduling within cron can be tricky, because only one script should be executed at any particular time, unless the scripts are staggered by several minutes.</span></span> <span data-ttu-id="fd249-343">매일 백업을 장기 보존하려는 경우 각각 보존 개수가 7인 매일 스냅숏을 12시간 스냅숏과 함께 유지하거나 매시간 스냅숏을 10분 후에 만들도록 지연합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-343">If you want daily backups for long-term retention, either a daily snapshot is kept along with a 12-hour snapshot (with a retention count of seven each), or the hourly snapshot is staggered to take place 10 minutes later.</span></span> <span data-ttu-id="fd249-344">프로덕션 볼륨에는 하나의 매일 스냅숏만이 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-344">Only one daily snapshot is kept in the production volume.</span></span>
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 7
10 0 * * * ./azure_hana_backup.pl lhanad01 daily 7
```
<span data-ttu-id="fd249-345">여기에 나열된 빈도는 예제일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-345">The frequencies listed here are only examples.</span></span> <span data-ttu-id="fd249-346">스냅숏의 최적수를 알아내려면 다음 조건을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-346">To derive your optimum number of snapshots, use the following criteria:</span></span>

- <span data-ttu-id="fd249-347">지정 시간 복구에 대한 복구 시간 목표의 요구 사항</span><span class="sxs-lookup"><span data-stu-id="fd249-347">Requirements in recovery time objective for point-in-time recovery.</span></span>
- <span data-ttu-id="fd249-348">공간 사용</span><span class="sxs-lookup"><span data-stu-id="fd249-348">Space usage.</span></span>
- <span data-ttu-id="fd249-349">잠재적 재해 복구를 위한 복구 지점 목표 및 복구 시간 목표의 요구 사항</span><span class="sxs-lookup"><span data-stu-id="fd249-349">Requirements in recovery point objective and recovery time objective for potential disaster recovery.</span></span>
- <span data-ttu-id="fd249-350">디스크에 대한 HANA 전체 데이터베이스 백업의 최종 실행</span><span class="sxs-lookup"><span data-stu-id="fd249-350">Eventual execution of HANA full database backups against disks.</span></span> <span data-ttu-id="fd249-351">디스크 또는 _backint_ 인터페이스에 대한 전체 데이터베이스 백업이 실행되는 경우 저장소 스냅숏의 실행에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-351">Whenever a full database backup against disks, or _backint_ interface, is performed, the execution of storage snapshots fails.</span></span> <span data-ttu-id="fd249-352">저장소 스냅숏을 기반으로 전체 데이터베이스 백업을 실행하려는 경우 이 시간 동안 저장소 스냅숏이 실행되지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-352">If you plan to execute full database backups on top of storage snapshots, make sure that the execution of storage snapshots is disabled during this time.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="fd249-353">SAP HANA 백업에 대한 저장소 스냅숏 사용은 스냅숏이 SAP HANA 로그 백업과 함께 수행된 경우에만 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-353">The use of storage snapshots for SAP HANA backups is valid only when the snapshots are performed in conjunction with SAP HANA log backups.</span></span> <span data-ttu-id="fd249-354">이러한 로그 백업은 저장소 스냅숏 간에 기간에 적용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-354">These log backups need to be able to cover the time periods between the storage snapshots.</span></span> <span data-ttu-id="fd249-355">30일이라는 지정 시간 복구의 사용자에 대한 커밋을 설정한 경우 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-355">If you've set a commitment to users of a point-in-time recovery of 30 days, you need the following:</span></span>

- <span data-ttu-id="fd249-356">30일이 지난 저장소 스냅숏에 액세스하는 기능</span><span class="sxs-lookup"><span data-stu-id="fd249-356">Ability to access a storage snapshot that is 30 days old.</span></span>
- <span data-ttu-id="fd249-357">지난 30일 동안의 연속 로그 백업</span><span class="sxs-lookup"><span data-stu-id="fd249-357">Contiguous log backups over the last 30 days.</span></span>

<span data-ttu-id="fd249-358">로그 백업의 범위에서 백업 로그 볼륨의 스냅숏도 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-358">In the range of log backups, create a snapshot of the backup log volume as well.</span></span> <span data-ttu-id="fd249-359">그러나 다음을 수행할 수 있도록 정기적인 로그 백업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-359">However, be sure to perform regular log backups so that you can:</span></span>

- <span data-ttu-id="fd249-360">지정 시간 복구를 수행하는 데 필요한 연속 로그 백업을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-360">Have the contiguous log backups needed to perform point-in-time recoveries.</span></span>
- <span data-ttu-id="fd249-361">SAP HANA 로그 볼륨의 공간이 부족하지 않도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-361">Prevent the SAP HANA log volume from running out of space.</span></span>

<span data-ttu-id="fd249-362">마지막 단계 중 하나는 SAP HANA Studio에서 SAP HANA 백업 로그를 예약하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-362">One of the last steps is to schedule SAP HANA backup logs in SAP HANA Studio.</span></span> <span data-ttu-id="fd249-363">SAP HANA 백업 로그 대상 위치는 탑재 지점이 /hana/log/backups인 특별히 만든 hana/log\_backups 백업 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-363">The SAP HANA backup log target destination is the specially created hana/log\_backups volume with the mount point of /hana/log/backups.</span></span>

![SAP HANA Studio에서 SAP HANA 백업 로그 예약](./media/hana-overview-high-availability-disaster-recovery/image5-schedule-backup.png)

<span data-ttu-id="fd249-365">15분보다 더 자주 수행된 백업을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-365">You can choose backups that are more frequent than every 15 minutes.</span></span> <span data-ttu-id="fd249-366">일부 사용자도 1분마다 로그 백업을 수행할 수 있지만 15분 _이상_은 권장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-366">Some users even perform log backups every minute, although we do not recommend going _over_ 15 minutes.</span></span>

<span data-ttu-id="fd249-367">최종 단계는 SAP HANA의 초기 설치 후에 파일 기반 백업을 수행하여 백업 카탈로그 내에 있어야 하는 단일 백업 항목을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-367">The final step is to perform a file-based backup (after the initial installation of SAP HANA) to create a single backup entry that must exist within the backup catalog.</span></span> <span data-ttu-id="fd249-368">그렇지 않으면 SAP HANA는 지정된 로그 백업을 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-368">Otherwise SAP HANA cannot initiate your specified log backups.</span></span>

![단일 백업 항목을 만드는 파일 기반 백업 수행](./media/hana-overview-high-availability-disaster-recovery/image6-make-backup.png)

### <a name="monitoring-the-number-and-size-of-snapshots-on-the-disk-volume"></a><span data-ttu-id="fd249-370">디스크 볼륨에서 스냅숏의 개수 및 크기 모니터링</span><span class="sxs-lookup"><span data-stu-id="fd249-370">Monitoring the number and size of snapshots on the disk volume</span></span>

<span data-ttu-id="fd249-371">특정 저장소 볼륨에서 스냅숏의 개수 및 스냅숏의 저장소 사용을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-371">On a particular storage volume, you can monitor the number of snapshots and the storage consumption of snapshots.</span></span> <span data-ttu-id="fd249-372">`ls` 명령은 스냅숏 디렉터리 또는 파일을 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-372">The `ls` command doesn't show the snapshot directory or files.</span></span> <span data-ttu-id="fd249-373">그러나 Linux OS 명령인 `du`는 다음 명령을 사용하여 해당 항목을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-373">However, the Linux OS command `du` does, with the following commands:</span></span>

- <span data-ttu-id="fd249-374">`du –sh .snapshot`는 스냅숏 디렉터리 내에서 모든 스냅숏을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-374">`du –sh .snapshot` provides a total of all snapshots within the snapshot directory.</span></span>
- <span data-ttu-id="fd249-375">`du –sh --max-depth=1`는 .snapshot 폴더에 저장된 모든 스냅숏 및 각 스냅숏의 크기를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-375">`du –sh --max-depth=1` lists all snapshots that are saved in the .snapshot folder and the size of each snapshot.</span></span>
- <span data-ttu-id="fd249-376">`du –hc`는 모든 스냅숏에서 사용하는 전체 크기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-376">`du –hc` provides the total size used by all snapshots.</span></span>

<span data-ttu-id="fd249-377">이러한 명령을 사용하여 만들고 저장한 스냅숏이 볼륨에서 모든 저장소를 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-377">Use these commands to make sure that the snapshots that are taken and stored are not consuming all the storage on the volumes.</span></span>

### <a name="reducing-the-number-of-snapshots-on-a-server"></a><span data-ttu-id="fd249-378">서버에서 스냅숏 개수 감소</span><span class="sxs-lookup"><span data-stu-id="fd249-378">Reducing the number of snapshots on a server</span></span>

<span data-ttu-id="fd249-379">앞에서 설명한 대로 사용자가 저장한 스냅숏의 특정 레이블 수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-379">As explained earlier, you can reduce the number of certain labels of snapshots that you store.</span></span> <span data-ttu-id="fd249-380">스냅숏을 시작하는 명령의 마지막 두 매개 변수는 레이블과 보존할 스냅숏 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-380">The last two parameters of the command to initiate a snapshot are a label and the number of snapshots you want to retain.</span></span>
```
./azure_hana_backup.pl lhanad01 customer 20
```
<span data-ttu-id="fd249-381">앞의 예제에서 스냅숏 레이블은 _고객_이고, 보존할 이 레이블의 스냅숏 개수는 _20_입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-381">In the previous example, the snapshot label is _customer_ and the number of snapshots with this label to be retained is _20_.</span></span> <span data-ttu-id="fd249-382">디스크 공간 사용량에 응답하는 대로 저장된 스냅숏 수를 줄이려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-382">As you respond to disk space consumption, you might want to reduce the number of stored snapshots.</span></span> <span data-ttu-id="fd249-383">스냅숏 수를 줄이는 가장 좋은 방법은 마지막 매개 변수를 5로 설정한 스크립트를 실행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-383">The easy way to reduce the number of snapshots is to run the script with the last parameter set to 5:</span></span>
```
./azure_hana_backup.pl lhanad01 customer 5
```
<span data-ttu-id="fd249-384">이 설정으로 스크립트를 실행한 결과로 새 저장소 스냅숏을 포함한 스냅숏 개수는 _5_입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-384">As a result of running the script with this setting, the number of snapshots, including the new storage snapshot, is _5_.</span></span>

 >[!NOTE]
 > <span data-ttu-id="fd249-385">이 스크립트는 가장 최근의 이전 스냅숏이 한 시간 이전인 경우에만 스냅숏 수를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-385">This script reduces the number of snapshots only if the most recent previous snapshot is more than one hour old.</span></span> <span data-ttu-id="fd249-386">스크립트는 한 시간이 되지 않은 스냅숏을 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-386">The script does not delete snapshots that are less than one hour old.</span></span>

<span data-ttu-id="fd249-387">이러한 제한 사항은 제공되는 선택적 재해 복구 기능과 관련되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-387">These restrictions are related to the optional disaster-recovery functionality offered.</span></span>

<span data-ttu-id="fd249-388">해당 접두사를 사용하는 스냅숏 집합을 더 이상 유지하지 않으려면 _0_을 포함하는 스크립트를 보존 숫자로 실행하여 해당 접두사와 일치하는 모든 스냅숏을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-388">If you no longer want to maintain a set of snapshots with that prefix, you can execute the script with _0_ as the retention number to remove all snapshots matching that prefix.</span></span> <span data-ttu-id="fd249-389">그러나 모든 스냅숏을 제거하면 재해 복구의 기능에 영향을 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-389">However, removing all snapshots can affect the capabilities of disaster recovery.</span></span>

### <a name="recovering-to-the-most-recent-hana-snapshot"></a><span data-ttu-id="fd249-390">가장 최근 HANA 스냅숏으로 복구</span><span class="sxs-lookup"><span data-stu-id="fd249-390">Recovering to the most recent HANA snapshot</span></span>

<span data-ttu-id="fd249-391">프로덕션 중단 시나리오를 경험한 이벤트에서 Azure의 SAP HANA Service Management를 사용한 고객 인시던트처럼 저장소 스냅숏에서 복구하는 프로세스를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-391">In the event that you experience a production-down scenario, the process of recovering from a storage snapshot can be initiated as a customer incident with SAP HANA on Azure Service Management.</span></span> <span data-ttu-id="fd249-392">예기치 않은 시나리오는 데이터가 프로덕션 시스템에서 삭제되고 데이터를 다시 가져올 유일한 방법이 프로덕션 데이터베이스를 복원하는 것인 경우 긴급한 문제가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-392">Such an unexpected scenario might be a high-urgency matter if data was deleted in a production system and the only way to retrieve the data is to restore the production database.</span></span>

<span data-ttu-id="fd249-393">반면에 지정 시간 복구는 낮은 긴급도로 몇 일 앞서 계획될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-393">On the other hand, a point-in-time recovery could be low urgency and planned for days in advance.</span></span> <span data-ttu-id="fd249-394">우선 순위 문제를 발생시키는 대신 Azure의 SAP HANA Service Management를 사용하여 이 복구를 계획할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-394">You can plan this recovery with SAP HANA on Azure Service Management instead of raising a high-priority issue.</span></span> <span data-ttu-id="fd249-395">예를 들어, 새로운 Enhancement Package를 적용하여 SAP 소프트웨어의 업그레이드를 시도하려는 경우 EHP 업그레이드 전에 상태를 나타내는 스냅숏으로 다시 전환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-395">For example, you might be planning to try an upgrade of the SAP software by applying a new enhancement package, and you then need to revert back to a snapshot that represents the state before the EHP upgrade.</span></span>

<span data-ttu-id="fd249-396">요청을 실행하기 전에 몇 가지 준비를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-396">Before you issue the request, you need to do some preparation.</span></span> <span data-ttu-id="fd249-397">Azure의 SAP HANA Service Management 팀은 요청을 처리하고 복원된 볼륨을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-397">SAP HANA on Azure Service Management team can then handle the request and provide the restored volumes.</span></span> <span data-ttu-id="fd249-398">나중에 사용자는 스냅숏을 기반으로 HANA 데이터베이스를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-398">Afterward, it is up to you to restore the HANA database based on the snapshots.</span></span> <span data-ttu-id="fd249-399">요청에 대해 준비하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-399">Here is how to prepare for the request:</span></span>

>[!NOTE]
><span data-ttu-id="fd249-400">사용자 인터페이스는 사용하는 SAP HANA 릴리스에 따라 다음 스크린샷에서 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-400">Your user interface might vary from the following screenshots, depending on the SAP HANA release you are using.</span></span>

1. <span data-ttu-id="fd249-401">복원할 스냅숏을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-401">Decide which snapshot to restore.</span></span> <span data-ttu-id="fd249-402">달리 지시하지 않으면 hana/data 볼륨은 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-402">Only the hana/data volume would be restored unless you are instructed otherwise.</span></span>

2. <span data-ttu-id="fd249-403">HANA 인스턴스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-403">Shut down the HANA instance.</span></span>

 ![HANA 인스턴스를 종료합니다.](./media/hana-overview-high-availability-disaster-recovery/image7-shutdown-hana.png)

3. <span data-ttu-id="fd249-405">각 HANA 데이터베이스 노드에서 데이터 볼륨을 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-405">Unmount the data volumes on each HANA database node.</span></span> <span data-ttu-id="fd249-406">데이터 볼륨이 탑재되지 않은 경우 스냅숏 복원에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-406">The restoration of the snapshot fails if the data volumes are not unmounted.</span></span>

 ![각 HANA 데이터베이스 노드에서 데이터 볼륨 분리](./media/hana-overview-high-availability-disaster-recovery/image8-unmount-data-volumes.png)

4. <span data-ttu-id="fd249-408">Azure 지원 요청을 열어서 특정 스냅숏을 복원하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-408">Open an Azure support request to instruct the restoration of a specific snapshot.</span></span>

 - <span data-ttu-id="fd249-409">복원 중 Azure의 SAP HANA Service Management는 데이터를 손실하지 않도록 전화 회의에 참석하도록 요청할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-409">During the restoration: SAP HANA on Azure Service Management might ask you to attend a conference call to ensure that no data is getting lost.</span></span>

 - <span data-ttu-id="fd249-410">복원한 후에 Azure의 SAP HANA Service Management에서는 저장소 스냅숏이 복원된 시기를 알립니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-410">After the restoration: SAP HANA on Azure Service Management notifies you when the storage snapshot has been restored.</span></span>

5. <span data-ttu-id="fd249-411">복원 프로세스가 완료된 후에 모든 데이터 볼륨을 다시 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-411">After the restoration process is complete, remount all data volumes.</span></span>

 ![모든 데이터 볼륨 다시 탑재](./media/hana-overview-high-availability-disaster-recovery/image9-remount-data-volumes.png)

6. <span data-ttu-id="fd249-413">SAP HANA Studio를 통해 HANA DB에 다시 연결하는 경우 자동으로 표시되지 않으면 SAP HANA Studio 내에서 복구 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-413">Select recovery options within SAP HANA Studio, if they do not automatically come up when you reconnect to HANA DB through SAP HANA Studio.</span></span> <span data-ttu-id="fd249-414">다음 예제에서는 최신 HANA 스냅숏에 대한 복원을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-414">The following example shows a restoration to the last HANA snapshot.</span></span> <span data-ttu-id="fd249-415">저장소 스냅숏에는 하나의 HANA 스냅숏이 포함되고, 가장 최근의 저장소 스냅숏으로 복원하는 경우 가장 최근의 HANA 스냅숏이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-415">A storage snapshot embeds one HANA snapshot, and if you are restoring to the most recent storage snapshot, it should be the most recent HANA snapshot.</span></span> <span data-ttu-id="fd249-416">(이전 저장소 스냅숏으로 복원하는 경우 저장소 스냅숏이 만들어진 시간에 따라 HANA 스냅숏을 배치해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="fd249-416">(If you are restoring to older storage snapshots, you need to locate the HANA snapshot based on the time the storage snapshot was taken.)</span></span>

 ![SAP HANA Studio 내에서 복구 옵션 선택](./media/hana-overview-high-availability-disaster-recovery/image10-recover-options-a.png)

7. <span data-ttu-id="fd249-418">**특정 데이터 백업이나 저장소 스냅숏으로 데이터베이스 복구**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-418">Select **Recover the database to a specific data backup or storage snapshot**.</span></span>

 !["복구 유형 지정" 창](./media/hana-overview-high-availability-disaster-recovery/image11-recover-options-b.png)

8. <span data-ttu-id="fd249-420">**카탈로그 없이 백업 지정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-420">Select **Specify backup without catalog**.</span></span>

 !["백업 위치 지정" 창](./media/hana-overview-high-availability-disaster-recovery/image12-recover-options-c.png)

9. <span data-ttu-id="fd249-422">**대상 형식** 목록에서 **스냅숏**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-422">In the **Destination Type** list, select **Snapshot**.</span></span>

 !["복구할 백업 지정" 창](./media/hana-overview-high-availability-disaster-recovery/image13-recover-options-d.png)

10. <span data-ttu-id="fd249-424">**마침**을 클릭하여 복구 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-424">Click **Finish** to start the recovery process.</span></span>

 !["마침"을 클릭하여 복구 프로세스를 시작합니다.](./media/hana-overview-high-availability-disaster-recovery/image14-recover-options-e.png)

11. <span data-ttu-id="fd249-426">HANA 데이터베이스는 저장소 스냅숏이 포함된 HANA 스냅숏으로 복원되고 복구됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-426">The HANA database is restored and recovered to the HANA snapshot that's included in the storage snapshot.</span></span>

 ![HANA 데이터베이스는 HANA 스냅숏으로 복원되고 복구됩니다.](./media/hana-overview-high-availability-disaster-recovery/image15-recover-options-f.png)

### <a name="recovering-to-the-most-recent-state"></a><span data-ttu-id="fd249-428">가장 최근 상태로 복구</span><span class="sxs-lookup"><span data-stu-id="fd249-428">Recovering to the most recent state</span></span>

<span data-ttu-id="fd249-429">다음 프로세스는 저장소 스냅숏에 포함되는 HANA 스냅숏을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-429">The following process restores the HANA snapshot that is included in the storage snapshot.</span></span> <span data-ttu-id="fd249-430">그런 다음 저장소 스냅숏을 복원하기 전에 트랜잭션 로그 백업을 데이터베이스의 가장 최근 상태로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-430">It then restores the transaction log backups to the most recent state of the database before restoring the storage snapshot.</span></span>

>[!IMPORTANT]
><span data-ttu-id="fd249-431">계속 진행하기 전에 트랜잭션 로그 백업의 완전한 연속 체인이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-431">Before you proceed, make sure that you have a complete and contiguous chain of transaction log backups.</span></span> <span data-ttu-id="fd249-432">이러한 백업 없이 데이터베이스의 현재 상태를 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-432">Without these backups, you cannot restore the current state of the database.</span></span>

1. <span data-ttu-id="fd249-433">"가장 최근 HANA 스냅숏으로 복구"에서 이전 절차의 1~6단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-433">Complete steps 1-6 of the preceding procedure in "Recovering to the most recent HANA snapshot."</span></span>

2. <span data-ttu-id="fd249-434">**가장 최근 상태로 데이터베이스 복구**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-434">Select **Recover the database to its most recent state**.</span></span>

 !["가장 최근 상태로 데이터베이스 복구"를 선택합니다.](./media/hana-overview-high-availability-disaster-recovery/image16-recover-database-a.png)

3. <span data-ttu-id="fd249-436">가장 최근인 HANA 로그 백업의 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-436">Specify the location of the most recent HANA log backups.</span></span> <span data-ttu-id="fd249-437">위치는 HANA 스냅숏에서 가장 최근 상태까지 모든 HANA 트랜잭션 로그 백업을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-437">The location needs to contain all HANA transaction log backups from the HANA snapshot to the most recent state.</span></span>

 ![가장 최근인 HANA 로그 백업의 위치를 지정합니다.](./media/hana-overview-high-availability-disaster-recovery/image17-recover-database-b.png)

4. <span data-ttu-id="fd249-439">데이터베이스를 복구하는 기본으로 백업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-439">Select a backup as a base from which to recover the database.</span></span> <span data-ttu-id="fd249-440">이 예제에서 다음은 저장소 스냅숏이 포함되었던 HANA 스냅숏입니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-440">In our example, this is the HANA snapshot that was included in the storage snapshot.</span></span> <span data-ttu-id="fd249-441">(하나의 스냅숏만 다음 스크린샷에 나열됩니다.)</span><span class="sxs-lookup"><span data-stu-id="fd249-441">(Only one snapshot is listed in the following screenshot.)</span></span>

 ![데이터베이스를 복구하는 기본으로 백업을 선택합니다.](./media/hana-overview-high-availability-disaster-recovery/image18-recover-database-c.png)

5. <span data-ttu-id="fd249-443">델타가 HANA 스냅숏 시간과 가장 최근의 상태 간에 존재하지 않는 경우 **델타 백업 사용** 확인란의 선택을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-443">Clear the **Use Delta Backups** check box if deltas do not exist between the time of the HANA snapshot and the most recent state.</span></span>

 ![델타가 존재하지 않는 경우 "델타 백업 사용" 확인란의 선택을 취소합니다](./media/hana-overview-high-availability-disaster-recovery/image19-recover-database-d.png)

6. <span data-ttu-id="fd249-445">요약 화면에서 **마침**을 클릭하여 복원 절차를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-445">On the summary screen, click **Finish** to start the restoration procedure.</span></span>

 ![요약 페이지에서 "마침"을 클릭합니다.](./media/hana-overview-high-availability-disaster-recovery/image20-recover-database-e.png)

### <a name="recovering-to-another-point-in-time"></a><span data-ttu-id="fd249-447">다른 지정 시점으로 복구</span><span class="sxs-lookup"><span data-stu-id="fd249-447">Recovering to another point in time</span></span>
<span data-ttu-id="fd249-448">저장소 스냅숏에 포함된 HANA 스냅숏과 HANA 스냅숏 지정 시점 복구보다 이후인 스냅숏 간의 지정 시점으로 복구하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-448">To recover to a point in time between the HANA snapshot (included in the storage snapshot) and one that is later than the HANA snapshot point-in-time recovery, do the following:</span></span>

1. <span data-ttu-id="fd249-449">HANA 스냅숏에서 복구하려는 시간까지 모든 트랜잭션 로그 백업이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-449">Make sure that you have all transaction log backups from the HANA snapshot to the time you want to recover.</span></span>
2. <span data-ttu-id="fd249-450">"가장 최근 상태로 복구"에서 절차를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-450">Begin the procedure under "Recovering to the most recent state."</span></span>
3. <span data-ttu-id="fd249-451">프로시저의 2단계에 있는 **복구 유형 선택** 창에서 **데이터베이스를 다음 지정 시점으로 복구**를 선택한 다음 3~6단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-451">In step 2 of the procedure, in the **Specify Recovery Type** window, select **Recover the database to the following point in time**, specify the point in time, and then complete steps 3-6.</span></span>

## <a name="monitoring-the-execution-of-snapshots"></a><span data-ttu-id="fd249-452">스냅숏의 실행 모니터링</span><span class="sxs-lookup"><span data-stu-id="fd249-452">Monitoring the execution of snapshots</span></span>

<span data-ttu-id="fd249-453">저장소 스냅숏의 실행을 모니터링해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-453">You need to monitor the execution of storage snapshots.</span></span> <span data-ttu-id="fd249-454">저장소 스냅숏을 실행하는 스크립트는 파일에 출력을 작성한 다음 Perl 스크립트와 동일한 위치에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-454">The script that executes a storage snapshot writes output to a file and then saves it to the same location as the Perl scripts.</span></span> <span data-ttu-id="fd249-455">각 스냅숏에 대해 별도 파일을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-455">A separate file is written for each snapshot.</span></span> <span data-ttu-id="fd249-456">각 파일의 출력은 스냅숏 스크립트가 실행되는 다양한 단계를 명확하게 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-456">The output of each file clearly shows the various phases that the snapshot script executes:</span></span>

- <span data-ttu-id="fd249-457">스냅숏을 만드는 데 필요한 볼륨 찾기</span><span class="sxs-lookup"><span data-stu-id="fd249-457">Finding the volumes that need to create a snapshot</span></span>
- <span data-ttu-id="fd249-458">이러한 볼륨에서 만든 스냅숏 찾기</span><span class="sxs-lookup"><span data-stu-id="fd249-458">Finding the snapshots taken from these volumes</span></span>
- <span data-ttu-id="fd249-459">최종 기존 스냅숏을 삭제하여 지정한 스냅숏 개수와 일치</span><span class="sxs-lookup"><span data-stu-id="fd249-459">Deleting eventual existing snapshots to match the number of snapshots you specified</span></span>
- <span data-ttu-id="fd249-460">HANA 스냅숏 만들기</span><span class="sxs-lookup"><span data-stu-id="fd249-460">Creating a HANA snapshot</span></span>
- <span data-ttu-id="fd249-461">볼륨을 통해 저장소 스냅숏 만들기</span><span class="sxs-lookup"><span data-stu-id="fd249-461">Creating the storage snapshot over the volumes</span></span>
- <span data-ttu-id="fd249-462">HANA 스냅숏 삭제</span><span class="sxs-lookup"><span data-stu-id="fd249-462">Deleting the HANA snapshot</span></span>
- <span data-ttu-id="fd249-463">가장 최근의 스냅숏의 이름을 **.0**으로 지정</span><span class="sxs-lookup"><span data-stu-id="fd249-463">Renaming the most recent snapshot to **.0**</span></span>

<span data-ttu-id="fd249-464">스크립트의 가장 중요한 부분은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-464">The most important part of the script is this:</span></span>
```
**********************Creating HANA snapshot**********************
Creating the HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data create snapshot"" ...
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
Deleting the HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data drop snapshot"" ...
HANA snapshot deletion successfully.
```
<span data-ttu-id="fd249-465">스크립트가 HANA 스냅숏의 생성을 기록하는 방법을 이 샘플에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-465">You can see from this sample how the script records the creation of the HANA snapshot.</span></span> <span data-ttu-id="fd249-466">확장 사례의 경우 이 프로세스는 마스터 노드에서 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-466">In the scale-out case, this process is initiated on the master node.</span></span> <span data-ttu-id="fd249-467">마스터 노드는 각 작업자 노드에서 스냅숏을 동기적으로 생성하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-467">The master node initiates the synchronous creation of the snapshots on each of the worker nodes.</span></span> <span data-ttu-id="fd249-468">그런 다음 저장소 스냅숏이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-468">Then the storage snapshot is taken.</span></span> <span data-ttu-id="fd249-469">저장소 스냅숏을 성공적으로 실행한 후에 HANA 스냅숏이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd249-469">After the successful execution of the storage snapshots, the HANA snapshot is deleted.</span></span>
