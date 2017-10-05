---
title: "저장소 스냅숏에 기반한 SAP HANA Azure 백업 | Microsoft Docs"
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
ms.openlocfilehash: f332b8ac091b75a23489ac27f15ad1fd10d24ec6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="sap-hana-backup-based-on-storage-snapshots"></a><span data-ttu-id="4671d-103">저장소 스냅숏에 기반한 SAP HANA 백업</span><span class="sxs-lookup"><span data-stu-id="4671d-103">SAP HANA backup based on storage snapshots</span></span>

## <a name="introduction"></a><span data-ttu-id="4671d-104">소개</span><span class="sxs-lookup"><span data-stu-id="4671d-104">Introduction</span></span>

<span data-ttu-id="4671d-105">이 문서는 3부로 구성된 SAP HANA 백업 관련 문서 시리즈의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-105">This is part of a three-part series of related articles on SAP HANA backup.</span></span> <span data-ttu-id="4671d-106">[Azure Virtual Machines의 SAP HANA 백업 가이드](sap-hana-backup-guide.md)에서 시작에 대한 개요와 정보를 제공하고, [파일 수준의 SAP HANA Azure Backup](sap-hana-backup-file-level.md)에서 파일 기반 백업 옵션을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-106">[Backup guide for SAP HANA on Azure Virtual Machines](sap-hana-backup-guide.md) provides an overview and information on getting started, and [SAP HANA Azure Backup on file level](sap-hana-backup-file-level.md) covers the file-based backup option.</span></span>

<span data-ttu-id="4671d-107">단일 인스턴스 통합(all-in-one) 데모 시스템에 VM 백업 기능을 사용하는 경우 OS 수준에서 HANA 백업을 관리하는 대신 VM 백업을 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-107">When using a VM backup feature for a single-instance all-in-one demo system, one should consider doing a VM backup instead of managing HANA backups at the OS level.</span></span> <span data-ttu-id="4671d-108">다른 방법으로는 Azure Blob 스냅숏을 만들어 가상 컴퓨터에 연결된 개별 가상 디스크의 복사본을 만들고 HANA 데이터 파일을 유지하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-108">An alternative is to take Azure blob snapshots to create copies of individual virtual disks, which are attached to a virtual machine, and keep the HANA data files.</span></span> <span data-ttu-id="4671d-109">그러나 중요한 점은 시스템 가동 중에 VM 백업 또는 디스크 스냅숏을 만들 때 앱 일관성을 유지하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-109">But a critical point is app consistency when creating a VM backup or disk snapshot while the system is up and running.</span></span> <span data-ttu-id="4671d-110">[Azure Virtual Machines의 SAP HANA 백업 가이드](sap-hana-backup-guide.md) 관련 문서의 _저장소 스냅숏을 만들 때의 SAP HANA 데이터 일관성_을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4671d-110">See _SAP HANA data consistency when taking storage snapshots_ in the related article [Backup guide for SAP HANA on Azure Virtual Machines](sap-hana-backup-guide.md).</span></span> <span data-ttu-id="4671d-111">SAP HANA에는 이러한 종류의 저장소 스냅숏을 지원하는 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-111">SAP HANA has a feature that supports these kinds of storage snapshots.</span></span>

## <a name="sap-hana-snapshots"></a><span data-ttu-id="4671d-112">SAP HANA 스냅숏</span><span class="sxs-lookup"><span data-stu-id="4671d-112">SAP HANA snapshots</span></span>

<span data-ttu-id="4671d-113">저장소 스냅숏 만들기를 지원하는 SAP HANA 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-113">There is a feature in SAP HANA that supports taking a storage snapshot.</span></span> <span data-ttu-id="4671d-114">그러나 2016년 12월 현재 단일 컨테이너 시스템에는 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-114">However, as of December 2016, there is a restriction to single-container systems.</span></span> <span data-ttu-id="4671d-115">다중 테넌트 컨테이너 구성에서는 이러한 종류의 데이터베이스 스냅숏을 지원하지 않습니다([저장소 스냅숏 만들기(SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm)(영문) 참조).</span><span class="sxs-lookup"><span data-stu-id="4671d-115">Multitenant container configurations do not support this kind of database snapshot (see [Create a Storage Snapshot (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm)).</span></span>

<span data-ttu-id="4671d-116">다음과 같이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-116">It works as follows:</span></span>

- <span data-ttu-id="4671d-117">SAP HANA 스냅숏을 시작하여 저장소 스냅숏 준비</span><span class="sxs-lookup"><span data-stu-id="4671d-117">Prepare for a storage snapshot by initiating the SAP HANA snapshot</span></span>
- <span data-ttu-id="4671d-118">저장소 스냅숏 실행(예: Azure Blob 스냅숏)</span><span class="sxs-lookup"><span data-stu-id="4671d-118">Run the storage snapshot (Azure blob snapshot, for example)</span></span>
- <span data-ttu-id="4671d-119">SAP HANA 스냅숏 확인</span><span class="sxs-lookup"><span data-stu-id="4671d-119">Confirm the SAP HANA snapshot</span></span>

![SQL 문을 통해 SAP HANA 데이터 스냅숏을 만들 수 있음을 보여 주는 스크린샷](media/sap-hana-backup-storage-snapshots/image011.png)

<span data-ttu-id="4671d-121">이 스크린샷에서는 SQL 문을 통해 SAP HANA 데이터 스냅숏을 만들 수 있음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-121">This screenshot shows that an SAP HANA data snapshot can be created via a SQL statement.</span></span>

![SAP HANA Studio의 백업 카탈로그에 표시된 스냅숏](media/sap-hana-backup-storage-snapshots/image012.png)

<span data-ttu-id="4671d-123">또한 스냅숏은 SAP HANA Studio의 백업 카탈로그에도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-123">The snapshot then also appears in the backup catalog in SAP HANA Studio.</span></span>

![디스크의 SAP HANA 데이터 디렉터리에 표시된 스냅숏](media/sap-hana-backup-storage-snapshots/image013.png)

<span data-ttu-id="4671d-125">스냅숏은 디스크의 SAP HANA 데이터 디렉터리에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-125">On disk, the snapshot shows up in the SAP HANA data directory.</span></span>

<span data-ttu-id="4671d-126">SAP HANA가 스냅숏 준비 모드에 있는 동안 저장소 스냅숏을 실행하기 전에 파일 시스템 일관성도 보장되는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-126">One has to ensure that the file system consistency is also guaranteed before running the storage snapshot while SAP HANA is in the snapshot preparation mode.</span></span> <span data-ttu-id="4671d-127">[Azure Virtual Machines의 SAP HANA 백업 가이드](sap-hana-backup-guide.md) 관련 문서의 _저장소 스냅숏을 만들 때의 SAP HANA 데이터 일관성_을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4671d-127">See _SAP HANA data consistency when taking storage snapshots_ in the related article [Backup guide for SAP HANA on Azure Virtual Machines](sap-hana-backup-guide.md).</span></span>

<span data-ttu-id="4671d-128">저장소 스냅숏이 완료되면 SAP HANA 스냅숏을 확인하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-128">Once the storage snapshot is done, it is critical to confirm the SAP HANA snapshot.</span></span> <span data-ttu-id="4671d-129">실행할 SQL 문은 BACKUP DATA CLOSE SNAPSHOT입니다([BACKUP DATA CLOSE SNAPSHOT 문(백업 및 복구)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/9739966f7f4bd5818769ad4ce6a7f8/content.htm)(영문) 참조).</span><span class="sxs-lookup"><span data-stu-id="4671d-129">There is a corresponding SQL statement to run: BACKUP DATA CLOSE SNAPSHOT (see [BACKUP DATA CLOSE SNAPSHOT Statement (Backup and Recovery)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/9739966f7f4bd5818769ad4ce6a7f8/content.htm)).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4671d-130">HANA 스냅숏을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-130">Confirm the HANA snapshot.</span></span> <span data-ttu-id="4671d-131">&quot;Copy-on-Write&quot;로 인해 SAP HANA에는 스냅숏 준비 모드에서 추가 디스크 공간이 필요할 수 있으며, 먼저 SAP HANA 스냅숏이 확인되어야 새 백업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-131">Due to &quot;Copy-on-Write,&quot; SAP HANA might require additional disk space in snapshot-prepare mode, and it is not possible to start new backups until the SAP HANA snapshot is confirmed.</span></span>

## <a name="hana-vm-backup-via-azure-backup-service"></a><span data-ttu-id="4671d-132">Azure Backup 서비스를 통한 HANA VM 백업</span><span class="sxs-lookup"><span data-stu-id="4671d-132">HANA VM backup via Azure Backup service</span></span>

<span data-ttu-id="4671d-133">2016년 12월 현재 Azure Backup 서비스의 백업 에이전트는 Linux VM에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-133">As of December 2016, the backup agent of the Azure Backup service is not available for Linux VMs.</span></span> <span data-ttu-id="4671d-134">파일/디렉터리 수준에서 Azure Backup을 사용하려면 SAP HANA 백업 파일을 Windows VM에 복사한 다음 백업 에이전트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-134">To make use of Azure backup on the file/directory level, one would copy SAP HANA backup files to a Windows VM and then use the backup agent.</span></span> <span data-ttu-id="4671d-135">그렇지 않으면 전체 Linux VM 백업만 Azure Backup 서비스를 통해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-135">Otherwise, only a full Linux VM backup is possible via the Azure Backup service.</span></span> <span data-ttu-id="4671d-136">자세한 내용은 [Azure Backup의 기능에 대한 개요](../../../backup/backup-introduction-to-azure-backup.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4671d-136">See [Overview of the features in Azure Backup](../../../backup/backup-introduction-to-azure-backup.md) to find out more.</span></span>

<span data-ttu-id="4671d-137">Azure Backup 서비스는 VM을 백업하고 복원하는 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-137">The Azure Backup service offers an option to back up and restore a VM.</span></span> <span data-ttu-id="4671d-138">이 서비스 및 작동 방법에 대한 자세한 내용은 [Azure에서 VM 백업 인프라 계획](../../../backup/backup-azure-vms-introduction.md) 문서에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-138">More information about this service and how it works can be found in the article [Plan your VM backup infrastructure in Azure](../../../backup/backup-azure-vms-introduction.md).</span></span>

<span data-ttu-id="4671d-139">이 문서에 따라 다음 두 가지의 중요한 고려 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-139">There are two important considerations according to that article:</span></span>

<span data-ttu-id="4671d-140">_&quot;Linux 가상 컴퓨터의 경우 VSS에 해당하는 플랫폼이 Linux에 없기 때문에 파일 일치 백업만 가능합니다.&quot;_</span><span class="sxs-lookup"><span data-stu-id="4671d-140">_&quot;For Linux virtual machines, only file-consistent backups are possible, since Linux does not have an equivalent platform to VSS.&quot;_</span></span>

<span data-ttu-id="4671d-141">_&quot;응용 프로그램은 복원된 데이터에 대해 고유한 &quot;수정&quot; 메커니즘을 구현해야 합니다.&quot;_</span><span class="sxs-lookup"><span data-stu-id="4671d-141">_&quot;Applications need to implement their own &quot;fix-up&quot; mechanism on the restored data.&quot;_</span></span>

<span data-ttu-id="4671d-142">따라서 백업이 시작될 때 SAP HANA가 일관된 디스크 상태에 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-142">Therefore, one has to make sure SAP HANA is in a consistent state on disk when the backup starts.</span></span> <span data-ttu-id="4671d-143">이 문서의 앞부분에서 설명한 _SAP HANA 스냅숏_을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4671d-143">See _SAP HANA snapshots_ described earlier in the document.</span></span> <span data-ttu-id="4671d-144">그러나 SAP HANA에서 이 스냅숏 준비 모드를 유지할 때 잠재적인 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-144">But there is a potential issue when SAP HANA stays in this snapshot preparation mode.</span></span> <span data-ttu-id="4671d-145">자세한 내용은 [저장소 스냅숏 만들기(SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4671d-145">See [Create a Storage Snapshot (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm) for more information.</span></span>

<span data-ttu-id="4671d-146">이 문서에서는 다음과 같이 설명하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-146">That article states:</span></span>

<span data-ttu-id="4671d-147">_&quot;저장소 스냅숏을 만든 후 가능한 한 빨리 확인하거나 중단하는 것이 좋습니다. 저장소 스냅숏을 준비하거나 만드는 동안 스냅숏 관련 데이터는 고정(freeze)됩니다. 스냅숏 관련 데이터가 고정된 상태에서도 데이터베이스에서 변경할 수 있습니다. 이러한 변경으로 인해 고정된 스냅숏 관련 데이터가 변경되지는 않습니다. 대신 변경 내용은 저장소 스냅숏과 별도로 데이터 영역의 위치에 기록됩니다. 변경 내용은 로그에도 기록됩니다. 그러나 스냅숏 관련 데이터가 고정된 상태로 유지될수록 데이터 볼륨이 커질 수 있습니다.&quot;_</span><span class="sxs-lookup"><span data-stu-id="4671d-147">_&quot;It is strongly recommended to confirm or abandon a storage snapshot as soon as possible after it has been created. While the storage snapshot is being prepared or created, the snapshot-relevant data is frozen. While the snapshot-relevant data remains frozen, changes can still be made in the database. Such changes will not cause the frozen snapshot-relevant data to be changed. Instead, the changes are written to positions in the data area that are separate from the storage snapshot. Changes are also written to the log. However, the longer the snapshot-relevant data is kept frozen, the more the data volume can grow.&quot;_</span></span>

<span data-ttu-id="4671d-148">Azure Backup은 Azure VM 확장을 통해 파일 시스템 일관성을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-148">Azure Backup takes care of the file system consistency via Azure VM extensions.</span></span> <span data-ttu-id="4671d-149">이러한 VM 확장은 독립 실행형으로 제공되지 않으며 Azure Backup 서비스와 함께 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-149">These extensions are not available standalone, and work only in combination with Azure Backup service.</span></span> <span data-ttu-id="4671d-150">그럼에도 불구하고 SAP HANA 스냅숏을 관리하여 앱 일관성을 보장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-150">Nevertheless, it is still a requirement to manage an SAP HANA snapshot to guarantee app consistency.</span></span>

<span data-ttu-id="4671d-151">Azure Backup에는 다음 두 가지 주요 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-151">Azure Backup has two major phases:</span></span>

- <span data-ttu-id="4671d-152">스냅숏 만들기</span><span class="sxs-lookup"><span data-stu-id="4671d-152">Take Snapshot</span></span>
- <span data-ttu-id="4671d-153">자격 증명 모음에 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="4671d-153">Transfer data to vault</span></span>

<span data-ttu-id="4671d-154">스냅숏을 만드는 Azure Backup 서비스 단계가 완료되면 SAP HANA 스냅숏을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-154">So one could confirm the SAP HANA snapshot once the Azure Backup service phase of taking a snapshot is completed.</span></span> <span data-ttu-id="4671d-155">Azure Portal에서 확인하는 데 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-155">It might take several minutes to see in the Azure portal.</span></span>

![그림: Azure Backup 서비스의 백업 작업 목록 일부](media/sap-hana-backup-storage-snapshots/image014.png)

<span data-ttu-id="4671d-157">이 그림에서는 HANA 테스트 VM을 백업하는 데 사용된 Azure Backup 서비스의 백업 작업 목록 일부를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-157">This figure shows part of the backup job list of an Azure Backup service, which was used to back up the HANA test VM.</span></span>

![Azure Portal에서 백업 작업을 클릭하여 작업 세부 정보 표시](media/sap-hana-backup-storage-snapshots/image015.png)

<span data-ttu-id="4671d-159">작업 세부 정보를 표시하려면 Azure Portal에서 백업 작업을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-159">To show the job details, click the backup job in the Azure portal.</span></span> <span data-ttu-id="4671d-160">여기에서 두 단계를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-160">Here, one can see the two phases.</span></span> <span data-ttu-id="4671d-161">완료된 스냅숏 단계가 표시되는 데 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-161">It might take a few minutes until it shows the snapshot phase as completed.</span></span> <span data-ttu-id="4671d-162">대부분의 시간이 데이터 전송 단계에서 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-162">Most of the time is spent in the data transfer phase.</span></span>

## <a name="hana-vm-backup-automation-via-azure-backup-service"></a><span data-ttu-id="4671d-163">Azure Backup 서비스를 통한 HANA VM 백업 자동화</span><span class="sxs-lookup"><span data-stu-id="4671d-163">HANA VM backup automation via Azure Backup service</span></span>

<span data-ttu-id="4671d-164">앞에서 설명한 대로 Azure Backup 스냅숏 단계가 완료되면 SAP HANA 스냅숏을 수동으로 확인할 수 있지만, 관리자가 Azure Portal에서 백업 작업 목록을 모니터링하지 않을 수 있으므로 자동화를 고려하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-164">One could manually confirm the SAP HANA snapshot once the Azure Backup snapshot phase is completed, as described earlier, but it is helpful to consider automation because an admin might not monitor the backup job list in the Azure portal.</span></span>

<span data-ttu-id="4671d-165">다음은 Azure PowerShell cmdlet을 통해 이 기능을 수행할 수 있는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-165">Here is an explanation how it could be accomplished via Azure PowerShell cmdlets.</span></span>

![hana-backup-vault라는 이름으로 만든 Azure Backup 서비스](media/sap-hana-backup-storage-snapshots/image016.png)

<span data-ttu-id="4671d-167">Azure Backup 서비스를 &quot;hana-backup-vault&quot;라는 이름으로 만들었습니다. **Get-AzureRmRecoveryServicesVault -Name hana-backup-vault** PS 명령은 해당 개체를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-167">An Azure Backup service was created with the name &quot;hana-backup-vault.&quot; The PS command **Get-AzureRmRecoveryServicesVault -Name hana-backup-vault** retrieves the corresponding object.</span></span> <span data-ttu-id="4671d-168">이 개체는 다음 그림과 같이 백업 컨텍스트를 설정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-168">This object is then used to set the backup context as seen on the next figure.</span></span>

![현재 진행 중인 백업 작업 확인](media/sap-hana-backup-storage-snapshots/image017.png)

<span data-ttu-id="4671d-170">올바른 컨텍스트를 설정한 후 현재 진행 중인 백업 작업을 확인한 다음 작업 세부 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-170">After setting the correct context, one can check for the backup job currently in progress, and then look for its job details.</span></span> <span data-ttu-id="4671d-171">하위 작업 목록에는 Azure Backup 작업의 스냅숏 단계가 이미 완료되었는지 여부가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-171">The subtask list shows if the snapshot phase of the Azure backup job is already completed:</span></span>

```
$ars = Get-AzureRmRecoveryServicesVault -Name hana-backup-vault
Set-AzureRmRecoveryServicesVaultContext -Vault $ars
$jid = Get-AzureRmRecoveryServicesBackupJob -Status InProgress | select -ExpandProperty jobid
Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
```

![Completed(완료됨) 상태가 될 때까지 폴링하는 루프 값](media/sap-hana-backup-storage-snapshots/image018.png)

<span data-ttu-id="4671d-173">작업 세부 정보가 변수에 저장되면 첫 번째 배열 항목으로 이동하여 상태 값을 검색하는 것은 PS 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-173">Once the job details are stored in a variable, it is simply PS syntax to get to the first array entry and retrieve the status value.</span></span> <span data-ttu-id="4671d-174">자동화 스크립트를 완료하려면 &quot;Completed&quot;로 바뀔 때까지 루프의 값을 폴링합니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-174">To complete the automation script, poll the value in a loop until it turns to &quot;Completed.&quot;</span></span>

```
$st = Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
$st[0] | select -ExpandProperty status
```

## <a name="hana-license-key-and-vm-restore-via-azure-backup-service"></a><span data-ttu-id="4671d-175">Azure Backup 서비스를 통한 HANA 라이선스 키 및 VM 복원</span><span class="sxs-lookup"><span data-stu-id="4671d-175">HANA license key and VM restore via Azure Backup service</span></span>

<span data-ttu-id="4671d-176">Azure Backup 서비스는 복원 중에 새 VM을 만들도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-176">The Azure Backup service is designed to create a new VM during restore.</span></span> <span data-ttu-id="4671d-177">현재는 기존 Azure VM의 &quot;내부&quot; 복원을 수행하는 계획이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-177">There is no plan right now to do an &quot;in-place&quot; restore of an existing Azure VM.</span></span>

![그림: Azure Portal의 Azure 서비스 복원 옵션](media/sap-hana-backup-storage-snapshots/image019.png)

<span data-ttu-id="4671d-179">이 그림에서는 Azure Portal에서 Azure 서비스의 복원 옵션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-179">This figure shows the restore option of the Azure service in the Azure portal.</span></span> <span data-ttu-id="4671d-180">복원 중에 VM 만들기와 디스크 복원 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-180">One can choose between creating a VM during restore or restoring the disks.</span></span> <span data-ttu-id="4671d-181">디스크를 복원한 후에도 그 위에 새 VM을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-181">After restoring the disks, it is still necessary to create a new VM on top of it.</span></span> <span data-ttu-id="4671d-182">Azure에서 새 VM을 만들었을 때마다 고유한 VM ID가 변경됩니다([Azure VM 고유 ID 액세스 및 사용](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/)(영문) 참조).</span><span class="sxs-lookup"><span data-stu-id="4671d-182">Whenever a new VM gets created on Azure the unique VM ID changes (see [Accessing and Using Azure VM Unique ID](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/)).</span></span>

![그림: Azure Backup 서비스를 통한 복원 전후의 Azure VM 고유 ID](media/sap-hana-backup-storage-snapshots/image020.png)

<span data-ttu-id="4671d-184">이 그림에서는 Azure Backup 서비스를 통한 복원 전후의 Azure VM 고유 ID를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-184">This figure shows the Azure VM unique ID before and after the restore via Azure Backup service.</span></span> <span data-ttu-id="4671d-185">이 고유한 VM ID는 SAP 라이선스에 사용되는 SAP 하드웨어 키에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-185">The SAP hardware key, which is used for SAP licensing, is using this unique VM ID.</span></span> <span data-ttu-id="4671d-186">따라서 VM을 복원한 후에는 새 SAP 라이선스를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-186">As a consequence, a new SAP license has to be installed after a VM restore.</span></span>

<span data-ttu-id="4671d-187">이 백업 가이드를 만드는 중에 미리 보기 모드에서 새로운 Azure Backup 기능이 제공되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-187">A new Azure Backup feature was presented in preview mode during the creation of this backup guide.</span></span> <span data-ttu-id="4671d-188">여기서는 VM 백업을 위해 만든 VM 스냅숏을 기반으로 하여 파일 수준에서 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-188">It allows a file level restore based on the VM snapshot that was taken for the VM backup.</span></span> <span data-ttu-id="4671d-189">이렇게 하면 새 VM을 배포할 필요가 없으므로 고유한 VM ID가 그대로 유지되며 새로운 SAP HANA 라이선스 키도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-189">This avoids the need to deploy a new VM, and therefore the unique VM ID stays the same and no new SAP HANA license key is required.</span></span> <span data-ttu-id="4671d-190">이 기능에 대한 자세한 설명서는 완전히 테스트한 후에 제공될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-190">More documentation on this feature will be provided after it is fully tested.</span></span>

<span data-ttu-id="4671d-191">결국에는 Azure Backup에서 개별 Azure 가상 디스크 및 VM 내의 파일과 디렉터리를 백업하도록 할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-191">Azure Backup will eventually allow backup of individual Azure virtual disks, plus files and directories from inside the VM.</span></span> <span data-ttu-id="4671d-192">Azure Backup의 가장 큰 장점은 모든 백업을 관리하여 고객이 백업하지 않아도 된다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-192">A major advantage of Azure Backup is its management of all the backups, saving the customer from having to do it.</span></span> <span data-ttu-id="4671d-193">복원이 필요할 경우 Azure Backup에서 올바른 백업을 사용하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-193">If a restore becomes necessary, Azure Backup will select the correct backup to use.</span></span>

## <a name="sap-hana-vm-backup-via-manual-disk-snapshot"></a><span data-ttu-id="4671d-194">수동 디스크 스냅숏을 통한 SAP HANA VM 백업</span><span class="sxs-lookup"><span data-stu-id="4671d-194">SAP HANA VM backup via manual disk snapshot</span></span>

<span data-ttu-id="4671d-195">Azure Backup 서비스를 사용하는 대신 Azure VHD의 Blob 스냅숏을 PowerShell을 통해 수동으로 만들어 개별 백업 솔루션을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-195">Instead of using the Azure Backup service, one could configure an individual backup solution by creating blob snapshots of Azure VHDs manually via PowerShell.</span></span> <span data-ttu-id="4671d-196">단계에 대한 설명은 [PowerShell과 함께 Blob 스냅숏 사용](https://blogs.msdn.microsoft.com/cie/2016/05/17/using-blob-snapshots-with-powershell/)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4671d-196">See [Using blob snapshots with PowerShell](https://blogs.msdn.microsoft.com/cie/2016/05/17/using-blob-snapshots-with-powershell/) for a description of the steps.</span></span>

<span data-ttu-id="4671d-197">이 방법은 더욱 유연하지만 다음과 같이 이 문서의 앞부분에서 설명한 문제를 해결하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-197">It provides more flexibility but does not resolve the issues explained earlier in this document:</span></span>

- <span data-ttu-id="4671d-198">여전히 SAP HANA가 일관된 상태인지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-198">One still must make sure that SAP HANA is in a consistent state</span></span>
- <span data-ttu-id="4671d-199">임대가 있다고 알리는 오류로 인해 VM 할당이 취소된 경우에도 OS 디스크를 덮어쓸 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-199">The OS disk cannot be overwritten even if the VM is deallocated because of an error stating that a lease exists.</span></span> <span data-ttu-id="4671d-200">VM을 삭제한 후에만 작동하므로 새 고유 VM ID를 가져오고 새 SAP 라이선스를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-200">It only works after deleting the VM, which would lead to a new unique VM ID and the need to install a new SAP license.</span></span>

![Azure VM의 데이터 디스크만 복원할 수 있습니다.](media/sap-hana-backup-storage-snapshots/image021.png)

<span data-ttu-id="4671d-202">다음과 같이 Azure VM의 데이터 디스크만 복원하여 새 고유 VM ID를 가져오는 문제를 방지하므로 SAP 라이선스를 무효화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-202">It is possible to restore only the data disks of an Azure VM, avoiding the problem of getting a new unique VM ID and, therefore, invalidated the SAP license:</span></span>

- <span data-ttu-id="4671d-203">테스트를 위해 두 개의 Azure 데이터 디스크를 VM에 연결하고 그 위에 소프트웨어 RAID를 정의했습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-203">For the test, two Azure data disks were attached to a VM and software RAID was defined on top of them</span></span> 
- <span data-ttu-id="4671d-204">SAP HANA 스냅숏 기능을 통해 SAP HANA가 일관된 상태에 있음을 확인했습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-204">It was confirmed that SAP HANA was in a consistent state by SAP HANA snapshot feature</span></span>
- <span data-ttu-id="4671d-205">파일 시스템을 고정했습니다([Azure Virtual Machines의 SAP HANA 백업 가이드](sap-hana-backup-guide.md) 관련 문서의 _저장소 스냅숏을 만들 때의 SAP HANA 데이터 일관성_ 참조).</span><span class="sxs-lookup"><span data-stu-id="4671d-205">File system freeze (see _SAP HANA data consistency when taking storage snapshots_ in the related article [Backup guide for SAP HANA on Azure Virtual Machines](sap-hana-backup-guide.md))</span></span>
- <span data-ttu-id="4671d-206">두 데이터 디스크에서 Blob 스냅숏을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-206">Blob snapshots were taken from both data disks</span></span>
- <span data-ttu-id="4671d-207">파일 시스템을 고정 취소했습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-207">File system unfreeze</span></span>
- <span data-ttu-id="4671d-208">SAP HANA 스냅숏을 확인했습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-208">SAP HANA snapshot confirmation</span></span>
- <span data-ttu-id="4671d-209">데이터 디스크를 복원하기 위해 VM을 종료하고 두 디스크를 분리했습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-209">To restore the data disks, the VM was shut down and both disks detached</span></span>
- <span data-ttu-id="4671d-210">디스크를 분리한 후 이전의 Blob 스냅숏으로 덮어썼습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-210">After detaching the disks, they were overwritten with the former blob snapshots</span></span>
- <span data-ttu-id="4671d-211">그런 다음 복원된 가상 디스크를 VM에 다시 연결했습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-211">Then the restored virtual disks were attached again to the VM</span></span>
- <span data-ttu-id="4671d-212">VM을 시작한 후 소프트웨어 RAID의 모든 파일이 잘 작동하고 Blob 스냅숏 시간으로 다시 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-212">After starting the VM, everything on the software RAID worked fine and was set back to the blob snapshot time</span></span>
- <span data-ttu-id="4671d-213">HANA를 HANA 스냅숏으로 다시 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-213">HANA was set back to the HANA snapshot</span></span>

<span data-ttu-id="4671d-214">Blob 스냅숏 이전에 SAP HANA를 종료할 수 있다면 절차가 덜 복잡하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-214">If it was possible to shut down SAP HANA before the blob snapshots, the procedure would be less complex.</span></span> <span data-ttu-id="4671d-215">이 경우 HANA 스냅숏을 건너뛸 수 있으며, 시스템에서 다른 작업이 수행되고 있지 않으면 파일 시스템 고정도 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-215">In that case, one could skip the HANA snapshot and, if nothing else is going on in the system, also skip the file system freeze.</span></span> <span data-ttu-id="4671d-216">모든 것이 온라인 상태인 동안에 스냅숏을 만들어야 하는 경우 더 복잡하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-216">Added complexity comes into the picture when it is necessary to do snapshots while everything is online.</span></span> <span data-ttu-id="4671d-217">[Azure Virtual Machines의 SAP HANA 백업 가이드](sap-hana-backup-guide.md) 관련 문서의 _저장소 스냅숏을 만들 때의 SAP HANA 데이터 일관성_을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4671d-217">See _SAP HANA data consistency when taking storage snapshots_ in the related article [Backup guide for SAP HANA on Azure Virtual Machines](sap-hana-backup-guide.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4671d-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4671d-218">Next steps</span></span>
* <span data-ttu-id="4671d-219">[Azure Virtual Machines의 SAP HANA 백업 가이드](sap-hana-backup-guide.md) - 시작에 대한 개요 및 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-219">[Backup guide for SAP HANA on Azure Virtual Machines](sap-hana-backup-guide.md) gives an overview and information on getting started.</span></span>
* <span data-ttu-id="4671d-220">[파일 수준 기반 SAP HANA 백업](sap-hana-backup-file-level.md)에서는 파일 기반 백업 옵션에 대해 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-220">[SAP HANA backup based on file level](sap-hana-backup-file-level.md) covers the file-based backup option.</span></span>
* <span data-ttu-id="4671d-221">[Azure의 SAP HANA(큰 인스턴스) 고가용성 및 재해 복구](hana-overview-high-availability-disaster-recovery.md) - Azure의 SAP HANA(큰 인스턴스)에 대한 고가용성 및 재해 복구 계획을 설정하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4671d-221">To learn how to establish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span>
