---
title: "Azure Backup Server v2에서 Modern Backup Storage 사용 | Microsoft Docs"
description: "Azure Backup Server v2의 새로운 기능에 대해 알아봅니다. 이 문서에서는 Backup Server 설치를 업그레이드하는 방법을 설명합니다."
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
ms.openlocfilehash: 751b9b495fd368dff1f72429707f5f33a0ccb569
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="add-storage-to-azure-backup-server-v2"></a><span data-ttu-id="ff6d7-104">Azure Backup Server v2에 저장소 추가</span><span class="sxs-lookup"><span data-stu-id="ff6d7-104">Add storage to Azure Backup Server v2</span></span>

<span data-ttu-id="ff6d7-105">Azure Backup Server v2에는 System Center 2016 Data Protection Manager Modern Backup Storage가 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-105">Azure Backup Server v2 comes with System Center 2016 Data Protection Manager Modern Backup Storage.</span></span> <span data-ttu-id="ff6d7-106">Modern Backup Storage를 사용하면 저장소를 50% 절약할 수 있고, 백업이 3배 더 빨라지고, 저장소를 더 효율적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-106">Modern Backup Storage offers storage savings of 50 percent, backups that are three times faster, and more efficient storage.</span></span> <span data-ttu-id="ff6d7-107">저장소에서 워크로드를 인식할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-107">It also offers workload-aware storage.</span></span> 

> [!NOTE]
> <span data-ttu-id="ff6d7-108">Modern Backup Storage를 사용하려면 Windows Server 2016에서 Backup Server v2를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-108">To use Modern Backup Storage, you must run Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="ff6d7-109">Backup Server v2를 이전 버전의 Windows Server에서 실행하면 Azure Backup Server는 Modern Backup Storage를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-109">If you run Backup Server v2 on an earlier version of Windows Server, Azure Backup Server can't take advantage of Modern Backup Storage.</span></span> <span data-ttu-id="ff6d7-110">대신에 Backup Server v1에서 보호하는 것처럼 워크로드를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-110">Instead, it protects workloads as it does with Backup Server v1.</span></span> <span data-ttu-id="ff6d7-111">자세한 내용은 Backup Server 버전 [보호 매트릭스](backup-mabs-protection-matrix.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-111">For more information, see the Backup Server version [protection matrix](backup-mabs-protection-matrix.md).</span></span>

## <a name="volumes-in-backup-server-v2"></a><span data-ttu-id="ff6d7-112">Backup Server v2의 볼륨</span><span class="sxs-lookup"><span data-stu-id="ff6d7-112">Volumes in Backup Server v2</span></span>

<span data-ttu-id="ff6d7-113">Backup Server v2는 저장소 볼륨을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-113">Backup Server v2 accepts storage volumes.</span></span> <span data-ttu-id="ff6d7-114">볼륨을 추가하면 Backup Server에서는 볼륨 형식을 Modern Backup Storage에 필요한 ReFS(Resilient File System)로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-114">When you add a volume, Backup Server formats the volume to Resilient File System (ReFS), which Modern Backup Storage requires.</span></span> <span data-ttu-id="ff6d7-115">볼륨을 추가하고 필요한 경우 나중에 확장하려면 이 워크플로를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-115">To add a volume, and to expand it later if you need to, we suggest that you use this workflow:</span></span>

1.  <span data-ttu-id="ff6d7-116">VM에 Backup Server v2를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-116">Set up Backup Server v2 on a VM.</span></span>
2.  <span data-ttu-id="ff6d7-117">저장소 풀의 가상 디스크에 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-117">Create a volume on a virtual disk in a storage pool:</span></span>
    1.  <span data-ttu-id="ff6d7-118">저장소 풀에 디스크를 추가하고 간단한 레이아웃으로 가상 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-118">Add a disk to a storage pool and create a virtual disk with simple layout.</span></span>
    2.  <span data-ttu-id="ff6d7-119">다른 디스크를 추가하고 가상 디스크를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-119">Add any additional disks, and extend the virtual disk.</span></span>
    3.  <span data-ttu-id="ff6d7-120">가상 디스크에 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-120">Create volumes on the virtual disk.</span></span>
3.  <span data-ttu-id="ff6d7-121">Backup Server에 볼륨을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-121">Add the volumes to Backup Server.</span></span>
4.  <span data-ttu-id="ff6d7-122">워크로드 인식 저장소를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-122">Configure workload-aware storage.</span></span>

## <a name="create-a-volume-for-modern-backup-storage"></a><span data-ttu-id="ff6d7-123">Modern Backup Storage에 대한 볼륨 만들기</span><span class="sxs-lookup"><span data-stu-id="ff6d7-123">Create a volume for Modern Backup Storage</span></span>

<span data-ttu-id="ff6d7-124">볼륨이 포함된 Backup Server v2를 디스크 저장소로 사용하면 저장소를 지속적으로 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-124">Using Backup Server v2 with volumes as disk storage can help you maintain control over storage.</span></span> <span data-ttu-id="ff6d7-125">볼륨은 단일 디스크일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-125">A volume can be a single disk.</span></span> <span data-ttu-id="ff6d7-126">하지만 나중에 저장소를 확장하려는 경우에는 저장소 공간을 사용하여 만들어진 디스크에서 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-126">However, if you want to extend storage in the future, create a volume out of a disk created by using storage spaces.</span></span> <span data-ttu-id="ff6d7-127">이렇게 하면 백업 저장소용 볼륨을 확장하려는 경우 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-127">This can help if you want to expand the volume for backup storage.</span></span> <span data-ttu-id="ff6d7-128">이 섹션에서는 이 설정을 통해 볼륨을 만드는 모범 사례를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-128">This section offers best practices for creating a volume with this setup.</span></span>

1. <span data-ttu-id="ff6d7-129">서버 관리자에서 **파일 및 저장소 서비스** > **볼륨** > **저장소 풀**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-129">In Server Manager, select **File and Storage Services** > **Volumes** > **Storage Pools**.</span></span> <span data-ttu-id="ff6d7-130">**실제 디스크**에서 **새 저장소 풀**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-130">Under **PHYSICAL DISKS**, select **New Storage Pool**.</span></span> 

    ![새 저장소 풀 만들기](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. <span data-ttu-id="ff6d7-132">**작업** 드롭다운 상자에서 **새 가상 디스크**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-132">In the **TASKS** drop-down box, select **New Virtual Disk**.</span></span>

    ![가상 디스크 추가](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. <span data-ttu-id="ff6d7-134">저장소 풀을 선택하고 나서 **실제 디스크 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-134">Select the storage pool, and then select **Add Physical Disk**.</span></span>

    ![실제 디스크 추가](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. <span data-ttu-id="ff6d7-136">실제 디스크를 선택하고 나서 **가상 디스크 확장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-136">Select the physical disk, and then select **Extend Virtual Disk**.</span></span>

    ![가상 디스크 확장](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. <span data-ttu-id="ff6d7-138">가상 디스크를 선택하고 나서 **새 볼륨**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-138">Select the virtual disk, and then select **New Volume**.</span></span>

    ![새 볼륨 만들기](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. <span data-ttu-id="ff6d7-140">**서버 및 디스크 선택** 대화 상자에서 서버와 새 디스크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-140">In the **Select the server and disk** dialog, select the server and the new disk.</span></span> <span data-ttu-id="ff6d7-141">그다음에 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-141">Then, select **Next**.</span></span>

    ![서버 및 디스크 선택](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-to-backup-server-disk-storage"></a><span data-ttu-id="ff6d7-143">Backup Server 디스크 저장소에 볼륨 추가</span><span class="sxs-lookup"><span data-stu-id="ff6d7-143">Add volumes to Backup Server disk storage</span></span>

<span data-ttu-id="ff6d7-144">Backup Server에 볼륨을 추가하려면 **관리** 창에서 저장소를 다시 검사하고 나서 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-144">To add a volume to Backup Server, in the **Management** pane, rescan the storage, and then select **Add**.</span></span> <span data-ttu-id="ff6d7-145">Backup Server 저장소에 추가할 수 있는 모든 볼륨 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-145">A list of all the volumes available to be added for Backup Server Storage appears.</span></span> <span data-ttu-id="ff6d7-146">사용 가능한 볼륨이 선택한 볼륨 목록에 추가된 후 해당 볼륨에 이름을 지정하면 관리하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-146">After available volumes are added to the list of selected volumes, you can give them a friendly name to help you manage them.</span></span> <span data-ttu-id="ff6d7-147">이러한 볼륨의 형식을 ReFS로 지정하여 Backup Server에서 Modern Backup Storage의 이점을 활용할 수 있게 하려면 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-147">To format these volumes to ReFS so Backup Server can use the benefits of Modern Backup Storage, select **OK**.</span></span>

![사용 가능한 볼륨 추가](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a><span data-ttu-id="ff6d7-149">워크로드 인식 저장소 설정</span><span class="sxs-lookup"><span data-stu-id="ff6d7-149">Set up workload-aware storage</span></span>

<span data-ttu-id="ff6d7-150">워크로드 인식 저장소를 사용하면 특정 종류의 워크로드를 선별적으로 저장하는 볼륨을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-150">With workload-aware storage, you can select the volumes that preferentially store certain kinds of workloads.</span></span> <span data-ttu-id="ff6d7-151">예를 들어 빈번한 대규모 백업이 필요한 워크로드만 저장하도록 많은 수의 IOPS(초당 입/출력 작업)를 지원하는 확장 볼륨을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-151">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) to store only the workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="ff6d7-152">예를 들어 트랜잭션 로그가 포함된 SQL Server가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-152">An example is SQL Server with transaction logs.</span></span> <span data-ttu-id="ff6d7-153">VM과 같이 덜 빈번하게 백업되는 다른 워크로드는 저비용 볼륨으로 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-153">Other workloads that are backed up less frequently, like VMs, can be backed up to low-cost volumes.</span></span>

### <a name="update-dpmdiskstorage"></a><span data-ttu-id="ff6d7-154">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="ff6d7-154">Update-DPMDiskStorage</span></span>

<span data-ttu-id="ff6d7-155">Data Protection Manager 서버의 저장소 풀에서 볼륨 속성을 업데이트하는 PowerShell cmdlet Update-DPMDiskStorage를 사용하여 워크로드 인식 저장소를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-155">You can set up workload-aware storage by using the PowerShell cmdlet Update-DPMDiskStorage, which updates the properties of a volume in the storage pool on a Data Protection Manager server.</span></span>

<span data-ttu-id="ff6d7-156">구문</span><span class="sxs-lookup"><span data-stu-id="ff6d7-156">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
<span data-ttu-id="ff6d7-157">다음 스크린샷은 PowerShell 창의 Update-DPMDiskStorage cmdlet을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-157">The following screenshot shows the Update-DPMDiskStorage cmdlet in the PowerShell window.</span></span>

![PowerShell 창의 Update-DPMDiskStorage 명령](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

<span data-ttu-id="ff6d7-159">PowerShell을 사용하여 변경하는 내용은 Backup Server 관리자 콘솔에 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-159">The changes you make by using PowerShell are reflected in the Backup Server Administrator Console.</span></span>

![관리자 콘솔의 디스크 및 볼륨](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a><span data-ttu-id="ff6d7-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ff6d7-161">Next steps</span></span>
<span data-ttu-id="ff6d7-162">Backup Server를 설치한 후 서버를 준비하는 방법을 알아보거나 워크로드 보호를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6d7-162">After you install Backup Server, learn how to prepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="ff6d7-163">Backup Server 워크로드 준비</span><span class="sxs-lookup"><span data-stu-id="ff6d7-163">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="ff6d7-164">Backup Server를 사용하여 VMware 서버 백업</span><span class="sxs-lookup"><span data-stu-id="ff6d7-164">Use Backup Server to back up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="ff6d7-165">Backup Server를 사용하여 SQL Server 백업</span><span class="sxs-lookup"><span data-stu-id="ff6d7-165">Use Backup Server to back up SQL Server</span></span>](backup-azure-sql-mabs.md)

