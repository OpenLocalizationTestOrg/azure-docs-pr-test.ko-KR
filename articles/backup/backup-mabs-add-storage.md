---
title: "Azure 백업 서버 v 2와 함께 최신 백업 저장소 aaaUse | Microsoft Docs"
description: "Hello Azure 백업 서버 v 2의 새로운 기능에 알아봅니다. 이 문서에서는 설명 방법을 tooupgrade 백업 서버 설치 합니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: b2a1ed27a6a682bd611fea1d2df9ef93314404e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-storage-tooazure-backup-server-v2"></a><span data-ttu-id="6e067-104">저장소 tooAzure v2 백업 서버를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-104">Add storage tooAzure Backup Server v2</span></span>

<span data-ttu-id="6e067-105">Azure Backup Server v2에는 System Center 2016 Data Protection Manager Modern Backup Storage가 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-105">Azure Backup Server v2 comes with System Center 2016 Data Protection Manager Modern Backup Storage.</span></span> <span data-ttu-id="6e067-106">Modern Backup Storage를 사용하면 저장소를 50% 절약할 수 있고, 백업이 3배 더 빨라지고, 저장소를 더 효율적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-106">Modern Backup Storage offers storage savings of 50 percent, backups that are three times faster, and more efficient storage.</span></span> <span data-ttu-id="6e067-107">저장소에서 워크로드를 인식할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-107">It also offers workload-aware storage.</span></span> 

> [!NOTE]
> <span data-ttu-id="6e067-108">최신 백업 저장소 toouse Windows Server 2016의 백업 서버 v 2를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-108">toouse Modern Backup Storage, you must run Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="6e067-109">Backup Server v2를 이전 버전의 Windows Server에서 실행하면 Azure Backup Server는 Modern Backup Storage를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-109">If you run Backup Server v2 on an earlier version of Windows Server, Azure Backup Server can't take advantage of Modern Backup Storage.</span></span> <span data-ttu-id="6e067-110">대신에 Backup Server v1에서 보호하는 것처럼 워크로드를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-110">Instead, it protects workloads as it does with Backup Server v1.</span></span> <span data-ttu-id="6e067-111">자세한 내용은 hello 백업 서버 버전을 참조 하십시오. [보호 매트릭스](backup-mabs-protection-matrix.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-111">For more information, see hello Backup Server version [protection matrix](backup-mabs-protection-matrix.md).</span></span>

## <a name="volumes-in-backup-server-v2"></a><span data-ttu-id="6e067-112">Backup Server v2의 볼륨</span><span class="sxs-lookup"><span data-stu-id="6e067-112">Volumes in Backup Server v2</span></span>

<span data-ttu-id="6e067-113">Backup Server v2는 저장소 볼륨을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-113">Backup Server v2 accepts storage volumes.</span></span> <span data-ttu-id="6e067-114">볼륨을 추가 하는 경우 백업 서버 hello 볼륨 tooResilient ReFS 파일 시스템 ()을 최신 백업 저장소에서 사용 하는 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-114">When you add a volume, Backup Server formats hello volume tooResilient File System (ReFS), which Modern Backup Storage requires.</span></span> <span data-ttu-id="6e067-115">tooadd, 볼륨 및 tooexpand 나중 해야 할 경우이 워크플로 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-115">tooadd a volume, and tooexpand it later if you need to, we suggest that you use this workflow:</span></span>

1.  <span data-ttu-id="6e067-116">VM에 Backup Server v2를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-116">Set up Backup Server v2 on a VM.</span></span>
2.  <span data-ttu-id="6e067-117">저장소 풀의 가상 디스크에 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-117">Create a volume on a virtual disk in a storage pool:</span></span>
    1.  <span data-ttu-id="6e067-118">디스크 tooa 저장소 풀을 추가 하 고 단순 레이아웃으로 가상 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-118">Add a disk tooa storage pool and create a virtual disk with simple layout.</span></span>
    2.  <span data-ttu-id="6e067-119">추가 디스크를 추가 하 고 hello 가상 디스크를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-119">Add any additional disks, and extend hello virtual disk.</span></span>
    3.  <span data-ttu-id="6e067-120">Hello 가상 디스크에 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-120">Create volumes on hello virtual disk.</span></span>
3.  <span data-ttu-id="6e067-121">Hello 볼륨 tooBackup 서버를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-121">Add hello volumes tooBackup Server.</span></span>
4.  <span data-ttu-id="6e067-122">워크로드 인식 저장소를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-122">Configure workload-aware storage.</span></span>

## <a name="create-a-volume-for-modern-backup-storage"></a><span data-ttu-id="6e067-123">Modern Backup Storage에 대한 볼륨 만들기</span><span class="sxs-lookup"><span data-stu-id="6e067-123">Create a volume for Modern Backup Storage</span></span>

<span data-ttu-id="6e067-124">볼륨이 포함된 Backup Server v2를 디스크 저장소로 사용하면 저장소를 지속적으로 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-124">Using Backup Server v2 with volumes as disk storage can help you maintain control over storage.</span></span> <span data-ttu-id="6e067-125">볼륨은 단일 디스크일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-125">A volume can be a single disk.</span></span> <span data-ttu-id="6e067-126">그러나 hello에 tooextend 저장소를 지정 하지 않고 향후 하려는 경우 저장소 공간을 사용 하 여 만든 디스크 공간 부족 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-126">However, if you want tooextend storage in hello future, create a volume out of a disk created by using storage spaces.</span></span> <span data-ttu-id="6e067-127">백업 저장을 위해 tooexpand hello 볼륨을 하려는 경우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-127">This can help if you want tooexpand hello volume for backup storage.</span></span> <span data-ttu-id="6e067-128">이 섹션에서는 이 설정을 통해 볼륨을 만드는 모범 사례를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-128">This section offers best practices for creating a volume with this setup.</span></span>

1. <span data-ttu-id="6e067-129">서버 관리자에서 **파일 및 저장소 서비스** > **볼륨** > **저장소 풀**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-129">In Server Manager, select **File and Storage Services** > **Volumes** > **Storage Pools**.</span></span> <span data-ttu-id="6e067-130">**실제 디스크**에서 **새 저장소 풀**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-130">Under **PHYSICAL DISKS**, select **New Storage Pool**.</span></span> 

    ![새 저장소 풀 만들기](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. <span data-ttu-id="6e067-132">Hello에 **작업** 드롭다운 상자 **새 가상 디스크**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-132">In hello **TASKS** drop-down box, select **New Virtual Disk**.</span></span>

    ![가상 디스크 추가](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. <span data-ttu-id="6e067-134">Hello 저장소 풀을 선택한 다음 선택 **실제 디스크 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-134">Select hello storage pool, and then select **Add Physical Disk**.</span></span>

    ![실제 디스크 추가](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. <span data-ttu-id="6e067-136">Hello 실제 디스크를 선택한 다음 선택 **가상 디스크 확장**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-136">Select hello physical disk, and then select **Extend Virtual Disk**.</span></span>

    ![Hello 가상 디스크를 확장 합니다.](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. <span data-ttu-id="6e067-138">Hello 가상 디스크를 선택한 다음 선택 **새 볼륨**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-138">Select hello virtual disk, and then select **New Volume**.</span></span>

    ![새 볼륨 만들기](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. <span data-ttu-id="6e067-140">Hello에 **hello 서버 및 디스크 선택** 대화 상자, 선택 hello 서버 및 hello 새 디스크.</span><span class="sxs-lookup"><span data-stu-id="6e067-140">In hello **Select hello server and disk** dialog, select hello server and hello new disk.</span></span> <span data-ttu-id="6e067-141">그다음에 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-141">Then, select **Next**.</span></span>

    ![Hello 서버 및 디스크 선택](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-toobackup-server-disk-storage"></a><span data-ttu-id="6e067-143">볼륨 tooBackup 서버 디스크 저장소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-143">Add volumes tooBackup Server disk storage</span></span>

<span data-ttu-id="6e067-144">hello에 볼륨 tooBackup 서버 tooadd **관리** hello 저장소 다시 검사 하 고 다음을 선택 하는 창 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-144">tooadd a volume tooBackup Server, in hello **Management** pane, rescan hello storage, and then select **Add**.</span></span> <span data-ttu-id="6e067-145">모든 hello 볼륨 사용 가능한 toobe 서버는 백업 저장소에 대 한 추가 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-145">A list of all hello volumes available toobe added for Backup Server Storage appears.</span></span> <span data-ttu-id="6e067-146">사용할 수 있는 볼륨 선택한 볼륨의 toohello 목록에 추가 된 후 관리 하는 이름 toohelp을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-146">After available volumes are added toohello list of selected volumes, you can give them a friendly name toohelp you manage them.</span></span> <span data-ttu-id="6e067-147">이러한 볼륨 tooReFS 백업 서버 hello 이점의 최신 백업 저장소를 사용할 수 있도록 선택 tooformat **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-147">tooformat these volumes tooReFS so Backup Server can use hello benefits of Modern Backup Storage, select **OK**.</span></span>

![사용 가능한 볼륨 추가](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a><span data-ttu-id="6e067-149">워크로드 인식 저장소 설정</span><span class="sxs-lookup"><span data-stu-id="6e067-149">Set up workload-aware storage</span></span>

<span data-ttu-id="6e067-150">작업량 감지 저장소 우선적으로 특정 종류의 작업 부하를 저장 하는 hello 볼륨을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-150">With workload-aware storage, you can select hello volumes that preferentially store certain kinds of workloads.</span></span> <span data-ttu-id="6e067-151">예를 들어 비용이 많이 드는 볼륨을 지 원하는 많은 수의 두 번째 (IOPS) toostore 전용 hello 작업 자주, 대용량 백업 해야 하는 초당 입력/출력 작업을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-151">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) toostore only hello workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="6e067-152">예를 들어 트랜잭션 로그가 포함된 SQL Server가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-152">An example is SQL Server with transaction logs.</span></span> <span data-ttu-id="6e067-153">Vm의 경우와 같은 덜를 자주 백업 되는 다른 워크 로드 toolow 비용 볼륨을 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-153">Other workloads that are backed up less frequently, like VMs, can be backed up toolow-cost volumes.</span></span>

### <a name="update-dpmdiskstorage"></a><span data-ttu-id="6e067-154">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="6e067-154">Update-DPMDiskStorage</span></span>

<span data-ttu-id="6e067-155">Data Protection Manager 서버의 hello 저장소 풀에 볼륨의 hello 속성을 업데이트 하는 업데이트-DPMDiskStorage hello PowerShell cmdlet을 사용 하 여 작업 부하 인식 저장소를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-155">You can set up workload-aware storage by using hello PowerShell cmdlet Update-DPMDiskStorage, which updates hello properties of a volume in hello storage pool on a Data Protection Manager server.</span></span>

<span data-ttu-id="6e067-156">구문</span><span class="sxs-lookup"><span data-stu-id="6e067-156">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
<span data-ttu-id="6e067-157">hello 다음 스크린샷은 hello 업데이트 DPMDiskStorage cmdlet hello PowerShell 창에서.</span><span class="sxs-lookup"><span data-stu-id="6e067-157">hello following screenshot shows hello Update-DPMDiskStorage cmdlet in hello PowerShell window.</span></span>

![hello hello PowerShell 창에서 업데이트 DPMDiskStorage 명령](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

<span data-ttu-id="6e067-159">PowerShell을 사용 하 여 hello 변경 hello 백업 서버 관리자 콘솔에에서 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-159">hello changes you make by using PowerShell are reflected in hello Backup Server Administrator Console.</span></span>

![Hello 관리자 콘솔의에서 디스크와 볼륨](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a><span data-ttu-id="6e067-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6e067-161">Next steps</span></span>
<span data-ttu-id="6e067-162">백업 서버를 설치한 후에 대해 알아봅니다 어떻게 tooprepare 서버의 작업 보호를 시작 또는 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e067-162">After you install Backup Server, learn how tooprepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="6e067-163">Backup Server 워크로드 준비</span><span class="sxs-lookup"><span data-stu-id="6e067-163">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="6e067-164">백업 서버 tooback VMware 서버를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="6e067-164">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="6e067-165">SQL Server를 tooback 백업 서버를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="6e067-165">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)

