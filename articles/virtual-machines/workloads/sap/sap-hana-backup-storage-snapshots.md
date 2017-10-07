---
title: "aaaSAP HANA Azure 백업 스냅숏을 기반으로 저장소 | Microsoft Docs"
description: "Azure 가상 컴퓨터에는 SAP HANA에 대한 두 가지 주요 백업 방법이 있습니다. 이 문서에서는 저장소 스냅숏에 기반한 SAP HANA 백업에 대해 설명합니다"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ums.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 3/13/2017
ms.author: rclaus
ms.openlocfilehash: 32bb80f5a928a2cf63699bfe4f4cf5bbad81e6fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-backup-based-on-storage-snapshots"></a><span data-ttu-id="87e2c-103">저장소 스냅숏에 기반한 SAP HANA 백업</span><span class="sxs-lookup"><span data-stu-id="87e2c-103">SAP HANA backup based on storage snapshots</span></span>

## <a name="introduction"></a><span data-ttu-id="87e2c-104">소개</span><span class="sxs-lookup"><span data-stu-id="87e2c-104">Introduction</span></span>

<span data-ttu-id="87e2c-105">이 문서는 3부로 구성된 SAP HANA 백업 관련 문서 시리즈의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-105">This is part of a three-part series of related articles on SAP HANA backup.</span></span> <span data-ttu-id="87e2c-106">[Azure 가상 컴퓨터에서 SAP HANA에 대 한 백업 가이드](sap-hana-backup-guide.md) 시작, 대 한 개요 및 정보를 제공 하 고 [SAP HANA Azure에 백업 파일 수준](sap-hana-backup-file-level.md) 표지 hello 파일 기반 백업 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-106">[Backup guide for SAP HANA on Azure Virtual Machines](sap-hana-backup-guide.md) provides an overview and information on getting started, and [SAP HANA Azure Backup on file level](sap-hana-backup-file-level.md) covers hello file-based backup option.</span></span>

<span data-ttu-id="87e2c-107">단일 인스턴스 내부에서 올인원 데모 시스템에 대 한 VM 백업 기능을 사용할 경우 HANA 백업 hello 운영 체제 수준에서 관리 하는 대신 VM 백업을 수행 하나를 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-107">When using a VM backup feature for a single-instance all-in-one demo system, one should consider doing a VM backup instead of managing HANA backups at hello OS level.</span></span> <span data-ttu-id="87e2c-108">연결 된 tooa 가상 컴퓨터에 있으며 hello HANA 데이터 파일을 보관할 수 있는 개별 가상 디스크의 tootake Azure blob 스냅숏을 toocreate 복사본 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-108">An alternative is tootake Azure blob snapshots toocreate copies of individual virtual disks, which are attached tooa virtual machine, and keep hello HANA data files.</span></span> <span data-ttu-id="87e2c-109">하지만 중요 한 점은 hello 시스템이 가동 하는 동안 VM 백업 또는 디스크 스냅숏 생성 및 실행 하는 경우 응용 프로그램 일관성을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-109">But a critical point is app consistency when creating a VM backup or disk snapshot while hello system is up and running.</span></span> <span data-ttu-id="87e2c-110">참조 _저장소 스냅샷을 사용할 때 SAP HANA 데이터 일관성_ hello 관련된 문서에서 [Azure 가상 컴퓨터에서 SAP HANA에 대 한 백업 가이드](sap-hana-backup-guide.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-110">See _SAP HANA data consistency when taking storage snapshots_ in hello related article [Backup guide for SAP HANA on Azure Virtual Machines](sap-hana-backup-guide.md).</span></span> <span data-ttu-id="87e2c-111">SAP HANA에는 이러한 종류의 저장소 스냅숏을 지원하는 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-111">SAP HANA has a feature that supports these kinds of storage snapshots.</span></span>

## <a name="sap-hana-snapshots"></a><span data-ttu-id="87e2c-112">SAP HANA 스냅숏</span><span class="sxs-lookup"><span data-stu-id="87e2c-112">SAP HANA snapshots</span></span>

<span data-ttu-id="87e2c-113">저장소 스냅숏 만들기를 지원하는 SAP HANA 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-113">There is a feature in SAP HANA that supports taking a storage snapshot.</span></span> <span data-ttu-id="87e2c-114">그러나 2016 년 12 월을 기준으로 제한이 됩니다 toosingle 컨테이너 시스템.</span><span class="sxs-lookup"><span data-stu-id="87e2c-114">However, as of December 2016, there is a restriction toosingle-container systems.</span></span> <span data-ttu-id="87e2c-115">다중 테넌트 컨테이너 구성에서는 이러한 종류의 데이터베이스 스냅숏을 지원하지 않습니다([저장소 스냅숏 만들기(SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm)(영문) 참조).</span><span class="sxs-lookup"><span data-stu-id="87e2c-115">Multitenant container configurations do not support this kind of database snapshot (see [Create a Storage Snapshot (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm)).</span></span>

<span data-ttu-id="87e2c-116">다음과 같이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-116">It works as follows:</span></span>

- <span data-ttu-id="87e2c-117">Hello SAP HANA 스냅숏 시작 하 여 저장소 스냅숏에 대 한 준비</span><span class="sxs-lookup"><span data-stu-id="87e2c-117">Prepare for a storage snapshot by initiating hello SAP HANA snapshot</span></span>
- <span data-ttu-id="87e2c-118">Hello 저장소 스냅숏 (스냅숏, 예를 들어 Azure blob)를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-118">Run hello storage snapshot (Azure blob snapshot, for example)</span></span>
- <span data-ttu-id="87e2c-119">SAP HANA 스냅숏 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-119">Confirm hello SAP HANA snapshot</span></span>

![SQL 문을 통해 SAP HANA 데이터 스냅숏을 만들 수 있음을 보여 주는 스크린샷](media/sap-hana-backup-storage-snapshots/image011.png)

<span data-ttu-id="87e2c-121">이 스크린샷에서는 SQL 문을 통해 SAP HANA 데이터 스냅숏을 만들 수 있음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-121">This screenshot shows that an SAP HANA data snapshot can be created via a SQL statement.</span></span>

![다음에 스냅숏 hello SAP HANA Studio에서 백업 카탈로그 hello에에서도 나타납니다.](media/sap-hana-backup-storage-snapshots/image012.png)

<span data-ttu-id="87e2c-123">그런 다음 스냅숏을 hello SAP HANA Studio에서 백업 카탈로그 hello에에서도 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-123">hello snapshot then also appears in hello backup catalog in SAP HANA Studio.</span></span>

![디스크에 스냅숏 hello에에서 표시 hello SAP HANA 데이터 디렉터리](media/sap-hana-backup-storage-snapshots/image013.png)

<span data-ttu-id="87e2c-125">디스크에 hello 스냅숏 표시 hello SAP HANA 데이터 디렉터리에 됩니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-125">On disk, hello snapshot shows up in hello SAP HANA data directory.</span></span>

<span data-ttu-id="87e2c-126">SAP HANA hello 스냅숏 준비 모드에 있는 동안 hello 저장소 스냅숏을 실행 하기 전에 hello 파일 시스템 일관성 보장이 tooensure에 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-126">One has tooensure that hello file system consistency is also guaranteed before running hello storage snapshot while SAP HANA is in hello snapshot preparation mode.</span></span> <span data-ttu-id="87e2c-127">참조 _저장소 스냅샷을 사용할 때 SAP HANA 데이터 일관성_ hello 관련된 문서에서 [Azure 가상 컴퓨터에서 SAP HANA에 대 한 백업 가이드](sap-hana-backup-guide.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-127">See _SAP HANA data consistency when taking storage snapshots_ in hello related article [Backup guide for SAP HANA on Azure Virtual Machines](sap-hana-backup-guide.md).</span></span>

<span data-ttu-id="87e2c-128">Hello 저장소 스냅숏 작업이 완료 되 면은 중요 한 tooconfirm hello SAP HANA 스냅숏입니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-128">Once hello storage snapshot is done, it is critical tooconfirm hello SAP HANA snapshot.</span></span> <span data-ttu-id="87e2c-129">해당 SQL 문이 toorun: 백업 데이터 닫기 스냅숏을 (참조 [백업 데이터 닫기 스냅숏 문 (백업 및 복구)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/9739966f7f4bd5818769ad4ce6a7f8/content.htm)).</span><span class="sxs-lookup"><span data-stu-id="87e2c-129">There is a corresponding SQL statement toorun: BACKUP DATA CLOSE SNAPSHOT (see [BACKUP DATA CLOSE SNAPSHOT Statement (Backup and Recovery)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/9739966f7f4bd5818769ad4ce6a7f8/content.htm)).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="87e2c-130">Hello HANA 스냅숏을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-130">Confirm hello HANA snapshot.</span></span> <span data-ttu-id="87e2c-131">기한 너무&quot;쓰기 시 복사&quot; 모드에서 추가 디스크 공간이 스냅숏-준비 하 고 hello SAP HANA 스냅숏 확인 될 때까지 새 백업을 가능한 toostart는 SAP HANA 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-131">Due too&quot;Copy-on-Write,&quot; SAP HANA might require additional disk space in snapshot-prepare mode, and it is not possible toostart new backups until hello SAP HANA snapshot is confirmed.</span></span>

## <a name="hana-vm-backup-via-azure-backup-service"></a><span data-ttu-id="87e2c-132">Azure Backup 서비스를 통한 HANA VM 백업</span><span class="sxs-lookup"><span data-stu-id="87e2c-132">HANA VM backup via Azure Backup service</span></span>

<span data-ttu-id="87e2c-133">2016 년 12 월을 기준으로 hello Azure 백업 서비스의 hello 백업 에이전트를 Linux Vm에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-133">As of December 2016, hello backup agent of hello Azure Backup service is not available for Linux VMs.</span></span> <span data-ttu-id="87e2c-134">Azure 백업 사용할 toomake hello 파일/디렉터리 수준에서 하나는 SAP HANA 백업 파일 tooa Windows VM 복사한 다음 hello 백업 에이전트를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-134">toomake use of Azure backup on hello file/directory level, one would copy SAP HANA backup files tooa Windows VM and then use hello backup agent.</span></span> <span data-ttu-id="87e2c-135">그렇지 않으면 전체 Linux VM 백업만 hello Azure 백업 서비스를 통해 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-135">Otherwise, only a full Linux VM backup is possible via hello Azure Backup service.</span></span> <span data-ttu-id="87e2c-136">참조 [hello의 개요 기능 Azure 백업에서](../../../backup/backup-introduction-to-azure-backup.md) 자세히 toofind 합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-136">See [Overview of hello features in Azure Backup](../../../backup/backup-introduction-to-azure-backup.md) toofind out more.</span></span>

<span data-ttu-id="87e2c-137">Azure 백업 서비스 hello 최대 옵션 tooback 제공 하 고 VM을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-137">hello Azure Backup service offers an option tooback up and restore a VM.</span></span> <span data-ttu-id="87e2c-138">이 서비스 및 작동 방식에 대 한 자세한 내용은 hello 문서에서 참조할 수 있습니다 [Azure에서 VM 백업 인프라 계획](../../../backup/backup-azure-vms-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-138">More information about this service and how it works can be found in hello article [Plan your VM backup infrastructure in Azure](../../../backup/backup-azure-vms-introduction.md).</span></span>

<span data-ttu-id="87e2c-139">Toothat 문서에 따라 두 가지 중요 한 고려 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-139">There are two important considerations according toothat article:</span></span>

<span data-ttu-id="87e2c-140">_&quot;Linux 가상 컴퓨터에만 파일에 일관적인 백업은 가능 Linux 동등한 플랫폼 tooVSS 없기 때문입니다.&quot;_</span><span class="sxs-lookup"><span data-stu-id="87e2c-140">_&quot;For Linux virtual machines, only file-consistent backups are possible, since Linux does not have an equivalent platform tooVSS.&quot;_</span></span>

<span data-ttu-id="87e2c-141">_&quot;응용 프로그램 필요 tooimplement 자신의 &quot;픽스업&quot; 메커니즘 hello에 데이터를 복원 합니다.&quot;_</span><span class="sxs-lookup"><span data-stu-id="87e2c-141">_&quot;Applications need tooimplement their own &quot;fix-up&quot; mechanism on hello restored data.&quot;_</span></span>

<span data-ttu-id="87e2c-142">따라서 하나 toomake hello 백업이 시작 될 때 SAP HANA이 디스크에서 일관 된 상태에 있는지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-142">Therefore, one has toomake sure SAP HANA is in a consistent state on disk when hello backup starts.</span></span> <span data-ttu-id="87e2c-143">참조 _SAP HANA 스냅숏을_ hello 문서의 앞부분에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-143">See _SAP HANA snapshots_ described earlier in hello document.</span></span> <span data-ttu-id="87e2c-144">그러나 SAP HANA에서 이 스냅숏 준비 모드를 유지할 때 잠재적인 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-144">But there is a potential issue when SAP HANA stays in this snapshot preparation mode.</span></span> <span data-ttu-id="87e2c-145">자세한 내용은 [저장소 스냅숏 만들기(SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="87e2c-145">See [Create a Storage Snapshot (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm) for more information.</span></span>

<span data-ttu-id="87e2c-146">이 문서에서는 다음과 같이 설명하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-146">That article states:</span></span>

<span data-ttu-id="87e2c-147">_&quot;것 tooconfirm이 가장 좋습니다 또는 만들어진 후 저장소 스냅숏을 가능한 한 빨리 중단. Hello 저장소 스냅숏 준비를 하 고 또는 hello 생성 하는 동안 스냅숏 관련 데이터 고정 필드입니다. Hello 스냅숏 관련 데이터 중지 된 동안 hello 데이터베이스에 변경 내용이 여전히 가능 합니다. 이러한 변경 내용이 변경 된 스냅숏 관련 데이터 toobe 고정 hello를 발생 하지 않습니다. 대신, hello 변경 내용이 toopositions hello 저장소 스냅숏에서 분리 된 hello 데이터 영역에 기록 합니다. 변경 내용은 toohello 로그도 기록 됩니다. 그러나 hello 긴 hello 스냅숏 관련 데이터의 고정 유지, 데이터 볼륨 증가할 수 있는 더 많은 hello hello.&quot;_</span><span class="sxs-lookup"><span data-stu-id="87e2c-147">_&quot;It is strongly recommended tooconfirm or abandon a storage snapshot as soon as possible after it has been created. While hello storage snapshot is being prepared or created, hello snapshot-relevant data is frozen. While hello snapshot-relevant data remains frozen, changes can still be made in hello database. Such changes will not cause hello frozen snapshot-relevant data toobe changed. Instead, hello changes are written toopositions in hello data area that are separate from hello storage snapshot. Changes are also written toohello log. However, hello longer hello snapshot-relevant data is kept frozen, hello more hello data volume can grow.&quot;_</span></span>

<span data-ttu-id="87e2c-148">Azure 백업은 Azure VM 확장을 통해 파일 시스템 일관성 hello 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-148">Azure Backup takes care of hello file system consistency via Azure VM extensions.</span></span> <span data-ttu-id="87e2c-149">이러한 VM 확장은 독립 실행형으로 제공되지 않으며 Azure Backup 서비스와 함께 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-149">These extensions are not available standalone, and work only in combination with Azure Backup service.</span></span> <span data-ttu-id="87e2c-150">그럼에도 불구 하 고 요구 사항 toomanage는 SAP HANA 스냅숏 tooguarantee 응용 프로그램 일관성은 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-150">Nevertheless, it is still a requirement toomanage an SAP HANA snapshot tooguarantee app consistency.</span></span>

<span data-ttu-id="87e2c-151">Azure Backup에는 다음 두 가지 주요 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-151">Azure Backup has two major phases:</span></span>

- <span data-ttu-id="87e2c-152">스냅숏 만들기</span><span class="sxs-lookup"><span data-stu-id="87e2c-152">Take Snapshot</span></span>
- <span data-ttu-id="87e2c-153">전송 데이터 toovault</span><span class="sxs-lookup"><span data-stu-id="87e2c-153">Transfer data toovault</span></span>

<span data-ttu-id="87e2c-154">스냅숏을 만드는의 hello Azure 백업 서비스 단계가 완료 되 면 hello SAP HANA 스냅숏을 확인 될 수 있습니다 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-154">So one could confirm hello SAP HANA snapshot once hello Azure Backup service phase of taking a snapshot is completed.</span></span> <span data-ttu-id="87e2c-155">Hello Azure 포털에서에서 몇 분 toosee를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-155">It might take several minutes toosee in hello Azure portal.</span></span>

![이 그림 hello 백업 작업 목록이 Azure 백업 서비스의 일부를 보여 줍니다.](media/sap-hana-backup-storage-snapshots/image014.png)

<span data-ttu-id="87e2c-157">이 그림에서는 hello 백업 작업 목록이 사용 되는 tooback hello HANA 테스트 VM 하 던는 Azure 백업 서비스의 일부를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-157">This figure shows part of hello backup job list of an Azure Backup service, which was used tooback up hello HANA test VM.</span></span>

![tooshow hello 작업 세부 정보 클릭 hello hello Azure 포털에서에서 백업 작업](media/sap-hana-backup-storage-snapshots/image015.png)

<span data-ttu-id="87e2c-159">tooshow hello 작업 세부 정보는 hello hello Azure 포털에서에서 백업 작업을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-159">tooshow hello job details, click hello backup job in hello Azure portal.</span></span> <span data-ttu-id="87e2c-160">여기에서는 두 개의 단계로 hello를 볼 수 하나.</span><span class="sxs-lookup"><span data-stu-id="87e2c-160">Here, one can see hello two phases.</span></span> <span data-ttu-id="87e2c-161">Hello 스냅숏 단계를 완료 됨으로 표시할 때까지 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-161">It might take a few minutes until it shows hello snapshot phase as completed.</span></span> <span data-ttu-id="87e2c-162">대부분의 hello hello 데이터 전송 단계에서 소비 됩니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-162">Most of hello time is spent in hello data transfer phase.</span></span>

## <a name="hana-vm-backup-automation-via-azure-backup-service"></a><span data-ttu-id="87e2c-163">Azure Backup 서비스를 통한 HANA VM 백업 자동화</span><span class="sxs-lookup"><span data-stu-id="87e2c-163">HANA VM backup automation via Azure Backup service</span></span>

<span data-ttu-id="87e2c-164">앞에서 설명한 대로 hello Azure 백업 스냅숏 단계 완료 되 면 관리자 hello Azure 포털에서에서 백업 작업 목록 hello를 모니터링할 수 없다는 것이 도움이 tooconsider 자동화 되므로 hello SAP HANA 스냅숏을 수동으로 확인 될 수 있습니다 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-164">One could manually confirm hello SAP HANA snapshot once hello Azure Backup snapshot phase is completed, as described earlier, but it is helpful tooconsider automation because an admin might not monitor hello backup job list in hello Azure portal.</span></span>

<span data-ttu-id="87e2c-165">다음은 Azure PowerShell cmdlet을 통해 이 기능을 수행할 수 있는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-165">Here is an explanation how it could be accomplished via Azure PowerShell cmdlets.</span></span>

![Hello 이름 hana-백업-자격 증명 모음는 Azure 백업 서비스를 만들었습니다.](media/sap-hana-backup-storage-snapshots/image016.png)

<span data-ttu-id="87e2c-167">Hello 이름으로는 Azure 백업 서비스를 만든 &quot;hana-백업-자격 증명 모음&quot; PS 명령 hello **Get AzureRmRecoveryServicesVault-hana-백업-자격 증명 모음 이름을** 검색 hello 해당 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-167">An Azure Backup service was created with hello name &quot;hana-backup-vault.&quot; hello PS command **Get-AzureRmRecoveryServicesVault -Name hana-backup-vault** retrieves hello corresponding object.</span></span> <span data-ttu-id="87e2c-168">이 개체에 있으면 hello 다음 그림에 표시 된 대로 사용 되는 tooset hello 백업 컨텍스트.</span><span class="sxs-lookup"><span data-stu-id="87e2c-168">This object is then used tooset hello backup context as seen on hello next figure.</span></span>

![Hello 현재 진행 중인 백업 작업을 확인할 수 있습니다 하나](media/sap-hana-backup-storage-snapshots/image017.png)

<span data-ttu-id="87e2c-170">설정 hello 올바른 컨텍스트 후 hello 현재 진행 중인 백업 작업에 대 한 확인 하 고 작업 세부 정보를 찾습니다 수 하나.</span><span class="sxs-lookup"><span data-stu-id="87e2c-170">After setting hello correct context, one can check for hello backup job currently in progress, and then look for its job details.</span></span> <span data-ttu-id="87e2c-171">hello 하위 태스크 목록은 hello 백업 작업을 Azure의 hello 스냅숏 단계가 이미 완료 되었는지 여부를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-171">hello subtask list shows if hello snapshot phase of hello Azure backup job is already completed:</span></span>

```
$ars = Get-AzureRmRecoveryServicesVault -Name hana-backup-vault
Set-AzureRmRecoveryServicesVaultContext -Vault $ars
$jid = Get-AzureRmRecoveryServicesBackupJob -Status InProgress | select -ExpandProperty jobid
Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
```

![TooCompleted 설정 될 때까지 루프에서 폴링 hello 값](media/sap-hana-backup-storage-snapshots/image018.png)

<span data-ttu-id="87e2c-173">Hello 작업 세부 정보는 변수에으로 저장 되 고 나면 단순히 PS 구문 tooget toohello 첫 번째 배열 항목 되며 hello 상태 값을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-173">Once hello job details are stored in a variable, it is simply PS syntax tooget toohello first array entry and retrieve hello status value.</span></span> <span data-ttu-id="87e2c-174">toocomplete hello 자동화 스크립트 될 때까지 루프에서 폴링 hello 값 이면 너무&quot;완료 합니다.&quot;</span><span class="sxs-lookup"><span data-stu-id="87e2c-174">toocomplete hello automation script, poll hello value in a loop until it turns too&quot;Completed.&quot;</span></span>

```
$st = Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
$st[0] | select -ExpandProperty status
```

## <a name="hana-license-key-and-vm-restore-via-azure-backup-service"></a><span data-ttu-id="87e2c-175">Azure Backup 서비스를 통한 HANA 라이선스 키 및 VM 복원</span><span class="sxs-lookup"><span data-stu-id="87e2c-175">HANA license key and VM restore via Azure Backup service</span></span>

<span data-ttu-id="87e2c-176">hello Azure 백업 서비스는 설계 된 새 VM toocreate 복원 중입니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-176">hello Azure Backup service is designed toocreate a new VM during restore.</span></span> <span data-ttu-id="87e2c-177">계획은 없습니다 지금은 toodo는 &quot;내부&quot; 기존 Azure VM의 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-177">There is no plan right now toodo an &quot;in-place&quot; restore of an existing Azure VM.</span></span>

![이 그림은 hello Azure 포털에서에서 hello Azure 서비스의 hello 복원 옵션을 보여 줍니다.](media/sap-hana-backup-storage-snapshots/image019.png)

<span data-ttu-id="87e2c-179">이 그림 hello Azure 포털에서에서 hello Azure 서비스의 hello 복원 옵션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-179">This figure shows hello restore option of hello Azure service in hello Azure portal.</span></span> <span data-ttu-id="87e2c-180">하나 복원 하는 동안 VM을 만들거나 hello 디스크 복원 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-180">One can choose between creating a VM during restore or restoring hello disks.</span></span> <span data-ttu-id="87e2c-181">Hello 디스크를 복원한 후 것이 여전히 필요한 toocreate 그 위에 새 VM 합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-181">After restoring hello disks, it is still necessary toocreate a new VM on top of it.</span></span> <span data-ttu-id="87e2c-182">Azure의 hello 고유한 VM ID 변경 내용에 새 VM 생성 될 때마다 (참조 [액세스 및 Azure VM 고유 ID를 사용 하 여](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/)).</span><span class="sxs-lookup"><span data-stu-id="87e2c-182">Whenever a new VM gets created on Azure hello unique VM ID changes (see [Accessing and Using Azure VM Unique ID](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/)).</span></span>

![이 그림 이전 및 Azure 백업 서비스를 통해 hello 복원 후 hello Azure VM에 대 한 고유 ID를 보여 줍니다.](media/sap-hana-backup-storage-snapshots/image020.png)

<span data-ttu-id="87e2c-184">이 그림 전과 후 Azure 백업 서비스를 통해 hello 복원 hello Azure VM에 대 한 고유 ID를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-184">This figure shows hello Azure VM unique ID before and after hello restore via Azure Backup service.</span></span> <span data-ttu-id="87e2c-185">hello SAP 하드웨어 키를 사용 되는 SAP 라이선스에 대 한 고유한 VM ID를 사용 하는</span><span class="sxs-lookup"><span data-stu-id="87e2c-185">hello SAP hardware key, which is used for SAP licensing, is using this unique VM ID.</span></span> <span data-ttu-id="87e2c-186">이 인해 새 SAP 라이선스에 toobe VM 복원 후에 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-186">As a consequence, a new SAP license has toobe installed after a VM restore.</span></span>

<span data-ttu-id="87e2c-187">이 백업 가이드의 hello 생성 중에 새로운 Azure 백업 기능 미리 보기 모드에서 발표 합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-187">A new Azure Backup feature was presented in preview mode during hello creation of this backup guide.</span></span> <span data-ttu-id="87e2c-188">Hello VM 스냅숏으로 hello VM에 대 한 백업 기반 파일 수준 복원을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-188">It allows a file level restore based on hello VM snapshot that was taken for hello VM backup.</span></span> <span data-ttu-id="87e2c-189">이 hello 필요 toodeploy 새 VM을 방지할 수 따라서 hello 고유한 VM ID 유지 되며 hello 동일 하 고 새 SAP HANA 라이선스 키가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-189">This avoids hello need toodeploy a new VM, and therefore hello unique VM ID stays hello same and no new SAP HANA license key is required.</span></span> <span data-ttu-id="87e2c-190">이 기능에 대한 자세한 설명서는 완전히 테스트한 후에 제공될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-190">More documentation on this feature will be provided after it is fully tested.</span></span>

<span data-ttu-id="87e2c-191">Azure 백업 결국을 사용 하면 개별 Azure 가상 디스크의 백업 및 파일 및 디렉터리를 내부 hello VM입니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-191">Azure Backup will eventually allow backup of individual Azure virtual disks, plus files and directories from inside hello VM.</span></span> <span data-ttu-id="87e2c-192">Azure Backup의 큰 이점이 toodo 하는 것과 hello 고객을 저장 하는 모든 hello 백업 관리는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-192">A major advantage of Azure Backup is its management of all hello backups, saving hello customer from having toodo it.</span></span> <span data-ttu-id="87e2c-193">복원 작업은 필요, Azure 백업는 선택 hello 올바른 백업 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-193">If a restore becomes necessary, Azure Backup will select hello correct backup toouse.</span></span>

## <a name="sap-hana-vm-backup-via-manual-disk-snapshot"></a><span data-ttu-id="87e2c-194">수동 디스크 스냅숏을 통한 SAP HANA VM 백업</span><span class="sxs-lookup"><span data-stu-id="87e2c-194">SAP HANA VM backup via manual disk snapshot</span></span>

<span data-ttu-id="87e2c-195">Hello Azure 백업 서비스를 사용 하는 대신 PowerShell 통해 수동으로 Azure vhd blob 스냅숏을 만들면 개별 백업 솔루션을 구성할 수 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-195">Instead of using hello Azure Backup service, one could configure an individual backup solution by creating blob snapshots of Azure VHDs manually via PowerShell.</span></span> <span data-ttu-id="87e2c-196">참조 [PowerShell과 함께 사용 하 여 blob 스냅숏을](https://blogs.msdn.microsoft.com/cie/2016/05/17/using-blob-snapshots-with-powershell/) hello 단계의 설명에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-196">See [Using blob snapshots with PowerShell](https://blogs.msdn.microsoft.com/cie/2016/05/17/using-blob-snapshots-with-powershell/) for a description of hello steps.</span></span>

<span data-ttu-id="87e2c-197">유연성을 제공 하지만이 문서의 앞부분에서 설명 하는 hello 문제가 해결 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-197">It provides more flexibility but does not resolve hello issues explained earlier in this document:</span></span>

- <span data-ttu-id="87e2c-198">여전히 SAP HANA가 일관된 상태인지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-198">One still must make sure that SAP HANA is in a consistent state</span></span>
- <span data-ttu-id="87e2c-199">VM의 할당이 취소 됩니다 내용을 입력 하는 오류가 발생 한 임 대권을 hello 있는 경우에 hello OS 디스크를 덮어쓸 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-199">hello OS disk cannot be overwritten even if hello VM is deallocated because of an error stating that a lease exists.</span></span> <span data-ttu-id="87e2c-200">VM tooa 새 고유 VM ID와 hello 필요 tooinstall 새 SAP 라이선스 이어질 hello 삭제 한 후에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-200">It only works after deleting hello VM, which would lead tooa new unique VM ID and hello need tooinstall a new SAP license.</span></span>

![Azure VM의 가능한 toorestore 유일한 hello 데이터 디스크는](media/sap-hana-backup-storage-snapshots/image021.png)

<span data-ttu-id="87e2c-202">가능한 toorestore 새 고유 VM ID를 가져오는 hello 문제를 방지 하는 Azure VM의 데이터 디스크 에서만 hello 이며, 따라서 hello SAP 라이선스를 무효화:</span><span class="sxs-lookup"><span data-stu-id="87e2c-202">It is possible toorestore only hello data disks of an Azure VM, avoiding hello problem of getting a new unique VM ID and, therefore, invalidated hello SAP license:</span></span>

- <span data-ttu-id="87e2c-203">Hello 테스트에 대 한 두 개의 Azure 데이터 디스크 연결 된 tooa VM 했으며 소프트웨어 RAID 위쪽에 정의 된</span><span class="sxs-lookup"><span data-stu-id="87e2c-203">For hello test, two Azure data disks were attached tooa VM and software RAID was defined on top of them</span></span> 
- <span data-ttu-id="87e2c-204">SAP HANA 스냅숏 기능을 통해 SAP HANA가 일관된 상태에 있음을 확인했습니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-204">It was confirmed that SAP HANA was in a consistent state by SAP HANA snapshot feature</span></span>
- <span data-ttu-id="87e2c-205">파일 시스템 고정 (참조 _저장소 스냅샷을 사용할 때 SAP HANA 데이터 일관성_ hello 관련된 문서에서 [Azure 가상 컴퓨터에서 SAP HANA에 대 한 백업 가이드](sap-hana-backup-guide.md))</span><span class="sxs-lookup"><span data-stu-id="87e2c-205">File system freeze (see _SAP HANA data consistency when taking storage snapshots_ in hello related article [Backup guide for SAP HANA on Azure Virtual Machines](sap-hana-backup-guide.md))</span></span>
- <span data-ttu-id="87e2c-206">두 데이터 디스크에서 Blob 스냅숏을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-206">Blob snapshots were taken from both data disks</span></span>
- <span data-ttu-id="87e2c-207">파일 시스템을 고정 취소했습니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-207">File system unfreeze</span></span>
- <span data-ttu-id="87e2c-208">SAP HANA 스냅숏을 확인했습니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-208">SAP HANA snapshot confirmation</span></span>
- <span data-ttu-id="87e2c-209">양쪽 디스크가 모두 분리 및 toorestore hello 데이터 디스크 hello VM 종료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-209">toorestore hello data disks, hello VM was shut down and both disks detached</span></span>
- <span data-ttu-id="87e2c-210">Hello 이전 blob 스냅숏을 사용한 덮어쓸 된 hello 디스크를 분리 후</span><span class="sxs-lookup"><span data-stu-id="87e2c-210">After detaching hello disks, they were overwritten with hello former blob snapshots</span></span>
- <span data-ttu-id="87e2c-211">복원 하는 hello 가상 디스크가 연결 된 다음 다시 toohello VM</span><span class="sxs-lookup"><span data-stu-id="87e2c-211">Then hello restored virtual disks were attached again toohello VM</span></span>
- <span data-ttu-id="87e2c-212">시작 hello hello 소프트웨어 RAID 제대로 작동 하며 toohello blob 설정 된 모든 VM 스냅숏 시간 후</span><span class="sxs-lookup"><span data-stu-id="87e2c-212">After starting hello VM, everything on hello software RAID worked fine and was set back toohello blob snapshot time</span></span>
- <span data-ttu-id="87e2c-213">HANA 다시 toohello HANA 스냅숏 설정 된</span><span class="sxs-lookup"><span data-stu-id="87e2c-213">HANA was set back toohello HANA snapshot</span></span>

<span data-ttu-id="87e2c-214">SAP HANA 아래로 가능한 tooshut hello blob 스냅숏 전에 되었으면 hello 프로시저 덜 복잡 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-214">If it was possible tooshut down SAP HANA before hello blob snapshots, hello procedure would be less complex.</span></span> <span data-ttu-id="87e2c-215">이 경우 하나 수 hello HANA 스냅숏 건너뛰고, hello 시스템에서 진행 되만 수행 하는 경우 hello 파일 시스템 고정을 건너뛸 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-215">In that case, one could skip hello HANA snapshot and, if nothing else is going on in hello system, also skip hello file system freeze.</span></span> <span data-ttu-id="87e2c-216">복잡 한 추가 온라인 상태 이며 모든 것이 필요한 toodo 스냅숏을 경우 hello 그림으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-216">Added complexity comes into hello picture when it is necessary toodo snapshots while everything is online.</span></span> <span data-ttu-id="87e2c-217">참조 _저장소 스냅샷을 사용할 때 SAP HANA 데이터 일관성_ hello 관련된 문서에서 [Azure 가상 컴퓨터에서 SAP HANA에 대 한 백업 가이드](sap-hana-backup-guide.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-217">See _SAP HANA data consistency when taking storage snapshots_ in hello related article [Backup guide for SAP HANA on Azure Virtual Machines](sap-hana-backup-guide.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="87e2c-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="87e2c-218">Next steps</span></span>
* <span data-ttu-id="87e2c-219">[Azure Virtual Machines의 SAP HANA 백업 가이드](sap-hana-backup-guide.md) - 시작에 대한 개요 및 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-219">[Backup guide for SAP HANA on Azure Virtual Machines](sap-hana-backup-guide.md) gives an overview and information on getting started.</span></span>
* <span data-ttu-id="87e2c-220">[SAP HANA 백업 파일 수준에 따라](sap-hana-backup-file-level.md) 표지 hello 파일 기반 백업 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-220">[SAP HANA backup based on file level](sap-hana-backup-file-level.md) covers hello file-based backup option.</span></span>
* <span data-ttu-id="87e2c-221">tooestablish 고가용성 및 (대형 인스턴스) Azure에서 SAP HANA의 재해 복구 계획의 참조 toolearn [SAP HANA (대형 인스턴스) 고가용성 및 재해 복구 Azure에서](hana-overview-high-availability-disaster-recovery.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="87e2c-221">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span>
