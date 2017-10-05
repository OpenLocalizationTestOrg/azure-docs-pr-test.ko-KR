---
title: "Azure Backup Server v2 설치 | Microsoft Docs"
description: "Azure Backup Server v2에서는 VM, 파일 및 폴더, 워크로드 등을 보호하기 위한 향상된 백업 기능을 제공합니다. Azure Backup Server v2를 설치하거나 이 버전으로 업그레이드하는 방법을 알아봅니다."
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
ms.openlocfilehash: 1bbb16afef7940933b4c3ae23873f212770137e0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="install-azure-backup-server-v2"></a><span data-ttu-id="689cb-104">Azure Backup Server v2 설치</span><span class="sxs-lookup"><span data-stu-id="689cb-104">Install Azure Backup Server v2</span></span>

<span data-ttu-id="689cb-105">Azure Backup Server를 사용하여 VM(가상 컴퓨터), 워크로드, 파일 및 폴더 등을 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-105">Azure Backup Server helps protect your virtual machines (VMs), workloads, files and folders, and more.</span></span> <span data-ttu-id="689cb-106">Azure Backup Server v2는 Azure Backup Server v1을 기반으로 빌드되고 v1에서 사용할 수 없는 새로운 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-106">Azure Backup Server v2 builds on Azure Backup Server v1, and gives you new features that are not available in v1.</span></span> <span data-ttu-id="689cb-107">v1 및 v2의 기능 비교에 대해서는 [Azure Backup Server 보호 매트릭스](backup-mabs-protection-matrix.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="689cb-107">For a comparison of features between v1 and v2, see [Azure Backup Server protection matrix](backup-mabs-protection-matrix.md).</span></span> 

<span data-ttu-id="689cb-108">Backup Server v2의 추가 기능은 Backup Server v1의 업그레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-108">The additional features in Backup Server v2 are an upgrade from Backup Server v1.</span></span> <span data-ttu-id="689cb-109">하지만 Backup Server v1은 Backup Server v2를 설치하기 위한 필수 구성 요소가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-109">However, Backup Server v1 is not a prerequisite for installing Backup Server v2.</span></span> <span data-ttu-id="689cb-110">Backup Server v1에서 Backup Server v2로 업그레이드하려면 Backup Server v2를 Backup Server 보호 서버에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-110">If you want to upgrade from Backup Server v1 to Backup Server v2, install Backup Server v2 on the Backup Server protection server.</span></span> <span data-ttu-id="689cb-111">기존 Backup Server 설정은 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-111">Your existing Backup Server settings remain intact.</span></span>

<span data-ttu-id="689cb-112">Backup Server v2를 Windows Server 2012 R2 또는 Windows Server 2016에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-112">You can install Backup Server v2 on Windows Server 2012 R2 or Windows Server 2016.</span></span> <span data-ttu-id="689cb-113">System Center 2016 Data Protection Manager Modern Backup Storage 같은 새로운 기능을 활용하려면 Backup Server v2를 Windows Server 2016에 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-113">To take advantage of new features like System Center 2016 Data Protection Manager Modern Backup Storage, you must install Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="689cb-114">Backup Server v2로 업그레이드하거나 이 버전을 설치하기 전에 [installation prerequisites](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites)(설치 필수 구성 요소)를 읽어 보세요.</span><span class="sxs-lookup"><span data-stu-id="689cb-114">Before you upgrade to or install Backup Server v2, read about the [installation prerequisites](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span></span>

> [!NOTE]
> <span data-ttu-id="689cb-115">Azure Backup Server에는 System Center Data Protection Manager와 동일한 코드베이스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-115">Azure Backup Server has the same code base as System Center Data Protection Manager.</span></span> <span data-ttu-id="689cb-116">Backup Server v1은 Data Protection Manager 2012 R2에 해당하고 Backup Server v2는 Data Protection Manager 2016에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-116">Backup Server v1 is equivalent to Data Protection Manager 2012 R2, and Backup Server v2 is equivalent to Data Protection Manager 2016.</span></span> <span data-ttu-id="689cb-117">이 문서에서는 때때로 Data Protection Manager 설명서를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-117">This article occasionally references the Data Protection Manager documentation.</span></span>
>
>

## <a name="upgrade-backup-server-to-v2"></a><span data-ttu-id="689cb-118">Backup Server를 v2로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="689cb-118">Upgrade Backup Server to v2</span></span>
<span data-ttu-id="689cb-119">Backup Server v1에서 Backup Server v2로 업그레이드하려면 설치에 필수 업데이트가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-119">To upgrade from Backup Server v1 to Backup Server v2, make sure your installation has the required updates:</span></span>

- <span data-ttu-id="689cb-120">보호된 서버에서 [보호 에이전트를 업데이트](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent)합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-120">[Update the protection agents](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) on the protected servers.</span></span>
- <span data-ttu-id="689cb-121">Windows Server 2012 R2를 Windows Server 2016으로 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-121">Upgrade Windows Server 2012 R2 to Windows Server 2016.</span></span>
- <span data-ttu-id="689cb-122">모든 프로덕션 서버에서 Azure Backup Server 원격 관리자를 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-122">Upgrade Azure Backup Server Remote Administrator on all production servers.</span></span>
- <span data-ttu-id="689cb-123">백업이 프로덕션 서버를 다시 시작하지 않고 계속하도록 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-123">Ensure that backups are set to continue without restarting your production server.</span></span>


### <a name="upgrade-steps-for-backup-server-v2"></a><span data-ttu-id="689cb-124">Backup Server v2에 대한 업그레이드 단계</span><span class="sxs-lookup"><span data-stu-id="689cb-124">Upgrade steps for Backup Server v2</span></span>

1. <span data-ttu-id="689cb-125">다운로드 센터에서 [업그레이드 설치 관리자를 다운로드](https://go.microsoft.com/fwlink/?LinkId=626082)합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-125">In the Download Center, [download the upgrade installer](https://go.microsoft.com/fwlink/?LinkId=626082).</span></span>

2. <span data-ttu-id="689cb-126">설치 마법사를 추출한 후 **setup.exe 실행**이 선택되어 있는지 확인하고 나서 **마침**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-126">After you extract the setup wizard, make sure that **Execute setup.exe** is selected, and then select **Finish**.</span></span>

  ![설치 관리자 - 설치 프로그램 실행](./media/backup-mabs-upgrade-to-v2/run-setup.png)

3. <span data-ttu-id="689cb-128">Microsoft Azure Backup Server 마법사의 **설치**에서 **Microsoft Azure Backup Server**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-128">In the Microsoft Azure Backup Server wizard, under **Install**, select **Microsoft Azure Backup Server**.</span></span>

  ![설치 관리자 - 설치 선택](./media/backup-mabs-upgrade-to-v2/mabs-installer-s1.png)

4. <span data-ttu-id="689cb-130">**시작** 페이지에서 경고를 검토하고 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-130">On the **Welcome** page, review the warnings, and then select **Next**.</span></span>

  ![설치 관리자 - 시작 페이지](./media/backup-mabs-upgrade-to-v2/mabs-installer-s2.png)

5. <span data-ttu-id="689cb-132">설치 마법사에서는 필수 구성 요소 확인을 수행하여 사용자 환경을 업그레이드할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-132">The setup wizard performs prerequisite checks to make sure your environment can upgrade.</span></span> <span data-ttu-id="689cb-133">**필수 구성 요소 확인** 페이지에서 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-133">On the **Prerequisite Checks** page, select **Check**.</span></span>

  ![설치 관리자 - 필수 구성 요소 확인 페이지](./media/backup-mabs-upgrade-to-v2/mabs-installer-s3-perform-checks.png)

6. <span data-ttu-id="689cb-135">사용자 환경은 필수 구성 요소 확인을 통과해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-135">Your environment must pass the prerequisite checks.</span></span> <span data-ttu-id="689cb-136">사용자 환경이 확인을 통과하지 못하면 문제를 확인하고 해결하세요.</span><span class="sxs-lookup"><span data-stu-id="689cb-136">If your environment doesn't pass the checks, note the issues and fix them.</span></span> <span data-ttu-id="689cb-137">그다음에 **다시 확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-137">Then, select **Check Again**.</span></span> <span data-ttu-id="689cb-138">필수 구성 요소 확인을 통과한 후 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-138">After you pass the prerequisite checks, select **Next**.</span></span>

  ![설치 관리자 - 다시 확인 단추](./media/backup-mabs-upgrade-to-v2/mabs-installer-s4-pass-checks.png)

7. <span data-ttu-id="689cb-140">**SQL 설정** 페이지에서 SQL 설치에 대한 관련 옵션을 선택하고 **확인 후 설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-140">On the **SQL Settings** page, select the relevant option for your SQL installation, and then select **Check and Install**.</span></span>

  ![설치 관리자 - SQL 설정 페이지](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5-sql-settings.png)

  <span data-ttu-id="689cb-142">확인은 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-142">The checks might take a few minutes.</span></span> <span data-ttu-id="689cb-143">확인이 완료되면 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-143">When the checks are finished, select **Next**.</span></span>

  ![설치 관리자 - SQL 설정 확인 및 설치 단추](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5a-check-and fix-settings.png)

8. <span data-ttu-id="689cb-145">**설치 설정** 페이지에서 Backup Server가 설치된 위치 및 스크래치 위치를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-145">On the **Installation Settings** page, make any changes to the location where Backup Server is installed, or to the Scratch Location.</span></span> <span data-ttu-id="689cb-146">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-146">Select **Next**.</span></span>

  ![설치 관리자 - 설치 설정 페이지](./media/backup-mabs-upgrade-to-v2/mabs-installer-s6-installation-settings.png)

9. <span data-ttu-id="689cb-148">설치 마법사를 완료하려면 **마침**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-148">To finish the setup wizard, select **Finish**.</span></span>

  ![설치 관리자 - 마침](./media/backup-mabs-upgrade-to-v2/run-setup.png)



## <a name="add-storage-for-modern-backup-storage"></a><span data-ttu-id="689cb-150">Modern Backup Storage에 대한 저장소 추가</span><span class="sxs-lookup"><span data-stu-id="689cb-150">Add storage for Modern Backup Storage</span></span>

<span data-ttu-id="689cb-151">백업 저장소 효율성을 개선하기 위해 Backup Server v2에서는 볼륨에 대한 지원을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-151">To improve backup storage efficiency, Backup Server v2 adds support for volumes.</span></span> <span data-ttu-id="689cb-152">Backup Server v1처럼 Backup Server v2는 디스크를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-152">Like Backup Server v1, Backup Server v2 supports disks.</span></span>

### <a name="add-volumes-and-disks"></a><span data-ttu-id="689cb-153">볼륨 및 디스크 추가</span><span class="sxs-lookup"><span data-stu-id="689cb-153">Add volumes and disks</span></span>
<span data-ttu-id="689cb-154">Windows Server 2016에서 Backup Server v2를 실행할 경우 볼륨을 사용하여 백업 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-154">If you run Backup Server v2 on Windows Server 2016, you can use volumes to store backup data.</span></span> <span data-ttu-id="689cb-155">볼륨을 사용하면 저장소가 절약되고 더 빠르게 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-155">Volumes offer storage savings and faster backups.</span></span> <span data-ttu-id="689cb-156">볼륨은 Backup Server의 새로운 기능이므로 볼륨을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-156">Because volumes are new to Backup Server, you must add them.</span></span> 

<span data-ttu-id="689cb-157">볼륨을 Backup Server에 추가할 때 볼륨에 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-157">When you add a volume to Backup Server, you can give the volume a friendly name.</span></span> <span data-ttu-id="689cb-158">이름을 지정할 볼륨의 **이름** 열을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-158">Click the **Friendly Name** column of the volume you want to name.</span></span> <span data-ttu-id="689cb-159">필요한 경우 나중에 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-159">You can change the name later, if necessary.</span></span> <span data-ttu-id="689cb-160">PowerShell을 사용하여 볼륨의 이름을 추가하거나 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-160">You also can use PowerShell to add or change friendly names for volumes.</span></span>

<span data-ttu-id="689cb-161">관리자 콘솔에서 볼륨을 추가하려면:</span><span class="sxs-lookup"><span data-stu-id="689cb-161">To add a volume in the Administrator Console:</span></span>

1. <span data-ttu-id="689cb-162">Azure Backup Server 관리자 콘솔에서 **관리** > **디스크 저장소** > **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-162">In the Azure Backup Server Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![[디스크 저장소 추가] 마법사를 엽니다.](./media//backup-mabs-upgrade-to-v2/open-add-disk-storage-wizard.png)

    <span data-ttu-id="689cb-164">[디스크 저장소 추가] 마법사가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-164">This opens the Add Disk Storage wizard.</span></span>

2. <span data-ttu-id="689cb-165">**디스크 저장소 추가** 페이지의 **사용 가능한 볼륨** 상자에서 볼륨을 선택하고 나서 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-165">On the **Add Disk Storage** page, in the **Available volumes** box, select a volume, and then select **Add**.</span></span>
3. <span data-ttu-id="689cb-166">**선택한 볼륨** 상자에 볼륨의 이름을 입력하고 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-166">In the **Selected volumes** box, enter a friendly name for the volume, and then select **OK**.</span></span>

      ![디스크 저장소 추가 마법사 - 볼륨 추가](./media/backup-mabs-upgrade-to-v2/add-volume.png)

  <span data-ttu-id="689cb-168">디스크를 추가하려면 레거시 저장소가 있는 보호 그룹에 디스크가 속해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-168">If you want to add a disk, the disk must belong to a protection group that has legacy storage.</span></span> <span data-ttu-id="689cb-169">이러한 디스크는 해당 보호 그룹에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-169">These disks can only be used for these protection groups.</span></span> <span data-ttu-id="689cb-170">Backup Server에 레거시 보호가 있는 원본이 없다면 디스크가 나열되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-170">If Backup Server doesn't have sources that have legacy protection, the disk isn't listed.</span></span>

  <span data-ttu-id="689cb-171">디스크 추가에 대한 자세한 내용은 [Adding disks to increase legacy storage](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage)(디스크를 추가하여 레거시 저장소 늘리기)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="689cb-171">For more information about adding disks, see [Adding disks to increase legacy storage](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span></span> <span data-ttu-id="689cb-172">디스크에는 이름을 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-172">You can't give a disk a friendly name.</span></span>


### <a name="assign-workloads-to-volumes"></a><span data-ttu-id="689cb-173">볼륨에 워크로드 할당</span><span class="sxs-lookup"><span data-stu-id="689cb-173">Assign workloads to volumes</span></span>

<span data-ttu-id="689cb-174">Backup Server에서 어떤 볼륨에 어떤 워크로드를 할당할지 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-174">In Backup Server, you specify which workloads are assigned to which volumes.</span></span> <span data-ttu-id="689cb-175">예를 들어 빈번한 대규모 백업이 필요한 워크로드만 저장하도록 많은 수의 IOPS(초당 입/출력 작업)를 지원하는 확장 볼륨을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-175">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) to store only workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="689cb-176">예를 들어 트랜잭션 로그가 포함된 SQL Server가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-176">An example is SQL Server with transaction logs.</span></span>

#### <a name="update-dpmdiskstorage"></a><span data-ttu-id="689cb-177">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="689cb-177">Update-DPMDiskStorage</span></span>

<span data-ttu-id="689cb-178">Backup Server의 저장소 풀에서 볼륨 속성을 업데이트하려면 PowerShell cmdlet Update-DPMDiskStorage를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-178">To update the properties of a volume in the storage pool in Backup Server, use the PowerShell cmdlet Update-DPMDiskStorage.</span></span>

<span data-ttu-id="689cb-179">구문</span><span class="sxs-lookup"><span data-stu-id="689cb-179">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

<span data-ttu-id="689cb-180">PowerShell을 사용하여 변경한 모든 내용은 UI에 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-180">All changes that you make by using PowerShell are reflected in the UI.</span></span>


## <a name="protect-data-sources"></a><span data-ttu-id="689cb-181">데이터 원본 보호</span><span class="sxs-lookup"><span data-stu-id="689cb-181">Protect data sources</span></span>
<span data-ttu-id="689cb-182">데이터 원본 보호를 시작하려면 보호 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-182">To begin protecting data sources, create a protection group.</span></span> <span data-ttu-id="689cb-183">다음 단계에서는 [새 보호 그룹] 마법사에 대한 변경 내용이나 추가 내용을 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-183">The following steps highlight changes or additions to the New Protection Group wizard.</span></span>

<span data-ttu-id="689cb-184">보호 그룹을 만들려면:</span><span class="sxs-lookup"><span data-stu-id="689cb-184">To create a protection group:</span></span>

1. <span data-ttu-id="689cb-185">Backup Server 관리자 콘솔에서 **보호**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-185">In the Backup Server Administrator Console, select **Protection**.</span></span>

2. <span data-ttu-id="689cb-186">도구 리본에서 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-186">On the tool ribbon, select **New**.</span></span>

    <span data-ttu-id="689cb-187">[새 보호 그룹 만들기] 마법사가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-187">This opens the Create New Protection Group wizard.</span></span>

  ![새 보호 그룹 만들기 마법사](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-1.png)

3. <span data-ttu-id="689cb-189">**Welcome** 페이지에서 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-189">On the **Welcome** page, select **Next**.</span></span>
4. <span data-ttu-id="689cb-190">**보호 그룹 형식 선택** 페이지에서 만들려는 보호 그룹의 형식을 선택하고 나서 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-190">On the **Select Protection Group Type** page, select the type of protection group you want to create, and then select **Next**.</span></span>

  ![보호 그룹 형식 선택 페이지](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-2.png)

5. <span data-ttu-id="689cb-192">**그룹 구성원 선택** 페이지의 **사용 가능한 구성원** 창에서 보호 에이전트가 있는 구성원이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-192">On the **Select Group Members** page, in the **Available members** pane, the members with protection agents are listed.</span></span> <span data-ttu-id="689cb-193">이 예제에서는 볼륨 D:\ 및 E:\를 선택하고 **선택한 구성원** 창에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-193">For this example, select volume D:\ and E:\ and add them to the **Selected members** pane.</span></span> <span data-ttu-id="689cb-194">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-194">Select **Next**.</span></span>

  ![그룹 구성원 선택 페이지](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-3.png)

6. <span data-ttu-id="689cb-196">**데이터 보호 방법 선택** 페이지에서 **보호 그룹 이름**을 입력하고, 보호 방법을 선택하고 나서, **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-196">On the **Select Data Protection Method** page, enter a **Protection group name**, select the protection method, and then select **Next**.</span></span> <span data-ttu-id="689cb-197">단기 보호가 필요하면 **디스크** 백업 방법을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-197">If you want short-term protection, you must select the **Disk** backup method.</span></span>

  ![데이터 보호 방법 선택 페이지](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-4.png)

7. <span data-ttu-id="689cb-199">**단기 목표 지정** 페이지에서 **보존 범위** 및 **동기화 빈도**에 대한 세부 정보를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-199">On the **Specify Short-Term Goals** page, select the details for **Retention range** and **Synchronization frequency**.</span></span> <span data-ttu-id="689cb-200">그다음에 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-200">Then, select **Next**.</span></span> <span data-ttu-id="689cb-201">필요한 경우 복구 지점이 발생하는 일정을 변경하려면 **수정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-201">Optionally, to change the schedule for when recovery points are taken, select **Modify**.</span></span>

  ![단기 목표 지정 페이지](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-5.png)

8. <span data-ttu-id="689cb-203">**디스크 저장소 할당 검토** 페이지에서 선택한 데이터 원본에 대한 세부 정보, 데이터 원본 크기 및 프로비전할 공간과 대상 저장소 볼륨에 대한 값을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-203">On the **Review Disk Storage Allocation** page, review details about the data sources you selected, their size, and  values for the space to be provisioned and the target storage volume.</span></span>

  ![디스크 저장소 할당 검토 페이지](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-6.png)

  <span data-ttu-id="689cb-205">저장소 볼륨은 워크로드 볼륨 할당(PowerShell을 사용하여 설정됨) 및 사용 가능한 저장소에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-205">Storage volumes are based on the workload volume allocation (set by using PowerShell) and the available storage.</span></span> <span data-ttu-id="689cb-206">드롭다운 메뉴에서 다른 볼륨을 선택하여 저장소 볼륨을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-206">You can change the storage volumes by selecting other volumes in the drop-down menu.</span></span> <span data-ttu-id="689cb-207">**대상 저장소** 값을 변경하면 **사용 가능한 공간** 및 **Underprovisioned Space**(미달 프로비전된 공간) 아래 값을 반영하도록 **사용 가능한 디스크 저장소**가 크게 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-207">If you change the value for **Target Storage**, the value for **Available disk storage** dynamically changes to reflect values under **Free Space** and **Underprovisioned Space**.</span></span>

  <span data-ttu-id="689cb-208">데이터 원본이 계획대로 증가하면 **사용 가능한 디스크 저장소**의 **Underprovisioned Space**(미달 프로비전된 공간) 열의 값은 필요한 추가 저장소의 크기를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-208">If the data sources grow as planned, the value for the **Underprovisioned Space** column in **Available disk storage** reflects the amount of additional storage that's needed.</span></span> <span data-ttu-id="689cb-209">이 값을 사용하면 원활한 백업에 필요한 저장소를 계획하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-209">Use this value to help plan your storage needs for smooth backups.</span></span> <span data-ttu-id="689cb-210">값이 0이면 예측 가능한 미래에 저장소 관련 문제가 발생할 가능성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-210">If the value is zero, there are no potential problems with storage in the foreseeable future.</span></span> <span data-ttu-id="689cb-211">값이 0 이외의 숫자이면 보호 정책 및 보호된 구성원의 데이터 크기에 따라 할당된 저장소가 충분하지 않은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-211">If the value is a number other than zero, you do not have sufficient storage allocated  (based on your protection policy and the data size of your protected members).</span></span>

  ![미달 할당된 디스크 저장소](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-7.png)

   <span data-ttu-id="689cb-213">보호 그룹 만들기를 마치려면 마법사를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-213">To finish creating your protection group, complete the wizard.</span></span>

## <a name="migrate-legacy-storage-to-modern-backup-storage"></a><span data-ttu-id="689cb-214">Modern Backup Storage로 레거시 저장소 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="689cb-214">Migrate legacy storage to Modern Backup Storage</span></span>
<span data-ttu-id="689cb-215">Backup Server v2로 업그레이드하거나 이 버전을 설치하고 운영 체제를 Windows Server 2016으로 업그레이드한 후 Modern Backup Storage를 사용하도록 보호 그룹을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-215">After you upgrade to or install Backup Server v2 and upgrade the operating system to Windows Server 2016, update your protection groups to use Modern Backup Storage.</span></span> <span data-ttu-id="689cb-216">기본적으로 보호 그룹은 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-216">By default, protection groups are not changed.</span></span> <span data-ttu-id="689cb-217">보호 그룹은 처음에 설정된 대로 계속 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-217">They continue to function as they were initially set up.</span></span> 

<span data-ttu-id="689cb-218">Modern Backup Storage를 사용하도록 보호 그룹을 업데이트하는 것은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-218">Updating protection groups to use Modern Backup Storage is optional.</span></span> <span data-ttu-id="689cb-219">보호 그룹을 업데이트하려면 데이터 보존 옵션을 사용하여 모든 데이터 원본의 보호를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-219">To update the protection group, stop protection of all data sources by using the retain data option.</span></span> <span data-ttu-id="689cb-220">그다음에 데이터 원본을 새 보호 그룹에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-220">Then, add the data sources to a new protection group.</span></span>

1. <span data-ttu-id="689cb-221">관리자 콘솔에서 **보호** 기능을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-221">In the Administrator Console, select the **Protection** feature.</span></span> <span data-ttu-id="689cb-222">**보호 그룹 구성원** 목록에서 구성원을 마우스 오른쪽 단추로 클릭하고 **구성원 보호 중지**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-222">In the **Protection Group Member** list, right-click the member, and then select **Stop protection of member**.</span></span>

  ![구성원 보호 중지](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-stop-protection1.png)

2. <span data-ttu-id="689cb-224">**그룹에서 제거** 대화 상자에서 저장소 풀의 사용된 디스크 공간 및 사용 가능한 공간을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-224">In the **Remove from Group** dialog box, review the used disk space and the available free space for the storage pool.</span></span> <span data-ttu-id="689cb-225">기본값은 디스크에서 복구 지점을 유지하고 관련 보존 정책에 따라 만료되도록 허용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-225">The default is to leave the recovery points on the disk and allow them to expire per their associated retention policy.</span></span> <span data-ttu-id="689cb-226">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-226">Click **OK**.</span></span>

  <span data-ttu-id="689cb-227">사용된 디스크 공간을 사용 가능한 저장소 풀로 즉시 반환하려면 **디스크의 복제본 삭제** 확인란을 선택하여 해당 구성원과 연결된 백업 데이터(및 복구 지점)를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-227">If you want to immediately return the used disk space to the free storage pool, select the **Delete replica on disk** check box to delete the backup data (and recovery points) associated with that member.</span></span>

  ![그룹에서 제거 대화 상자](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-retain-data.png)

3. <span data-ttu-id="689cb-229">Modern Backup Storage를 사용하는 보호 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-229">Create a protection group that uses Modern Backup Storage.</span></span> <span data-ttu-id="689cb-230">보호되지 않는 데이터 원본을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-230">Include the unprotected data sources.</span></span>


## <a name="add-disks-to-increase-legacy-storage"></a><span data-ttu-id="689cb-231">디스크를 추가하여 레거시 저장소 늘리기</span><span class="sxs-lookup"><span data-stu-id="689cb-231">Add disks to increase legacy storage</span></span>

<span data-ttu-id="689cb-232">Backup Server에서 레거시 저장소를 사용하려면 디스크를 추가하여 레거시 저장소를 늘려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-232">If you want to use legacy storage with Backup Server, you might need to add disks to increase legacy storage.</span></span> 

<span data-ttu-id="689cb-233">디스크 저장소를 추가하려면:</span><span class="sxs-lookup"><span data-stu-id="689cb-233">To add disk storage:</span></span>

1. <span data-ttu-id="689cb-234">관리자 콘솔에서 **관리** > **디스크 저장소** > **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-234">In the Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![디스크 저장소 추가 대화 상자](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-add-disk-storage.png)

4. <span data-ttu-id="689cb-236">**디스크 저장소 추가** 대화 상자에서 **디스크 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-236">In the **Add Disk Storage** dialog, select **Add disks**.</span></span>

5. <span data-ttu-id="689cb-237">사용 가능한 디스크 목록에서 추가할 디스크를 선택하고, **추가**를 선택하고 나서, **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-237">In the list of available disks, select the disks you want to add, select **Add**, and then select **OK**.</span></span>

## <a name="update-the-data-protection-manager-protection-agent"></a><span data-ttu-id="689cb-238">Data Protection Manager 보호 에이전트 업데이트</span><span class="sxs-lookup"><span data-stu-id="689cb-238">Update the Data Protection Manager protection agent</span></span>

<span data-ttu-id="689cb-239">Backup Server에서는 업데이트에 System Center Data Protection Manager 보호 에이전트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-239">Backup Server uses the System Center Data Protection Manager protection agent for updates.</span></span> <span data-ttu-id="689cb-240">네트워크에 연결되지 않은 보호 에이전트를 업그레이드할 경우 연결된 에이전트 업그레이드를 완료하는 데는 Data Protection Manager 관리자 콘솔을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-240">If you are upgrading a protection agent that is not connected to the network, you cannot use the Data Protection Manager Administrator Console to complete a connected agent upgrade.</span></span> <span data-ttu-id="689cb-241">비활성 도메인 환경에서 보호 에이전트를 업그레이드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-241">You must upgrade the protection agent in a nonactive domain environment.</span></span> <span data-ttu-id="689cb-242">클라이언트 컴퓨터가 네트워크에 연결될 때까지 Data Protection Manager 관리자 콘솔에는 보호 에이전트 업데이트가 보류 중인 것으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-242">Until the client computer is connected to the network, the Data Protection Manager Administrator Console shows that the protection agent update is pending.</span></span>

<span data-ttu-id="689cb-243">다음 섹션에서는 연결되거나 연결되지 않은 클라이언트 컴퓨터에 대한 보호 에이전트를 업데이트하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-243">The following sections describe how to update protection agents for client computers that are connected and client computers that are not connected.</span></span>

### <a name="update-a-protection-agent-for-a-connected-client-computer"></a><span data-ttu-id="689cb-244">연결된 클라이언트 컴퓨터에 대한 보호 에이전트 업데이트</span><span class="sxs-lookup"><span data-stu-id="689cb-244">Update a protection agent for a connected client computer</span></span>

1. <span data-ttu-id="689cb-245">Backup Server 관리자 콘솔에서 **관리** > **에이전트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-245">In the Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="689cb-246">표시 창에서 보호 에이전트를 업데이트할 클라이언트 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-246">In the display pane, select the client computers for which you want to update the protection agent.</span></span>

  > [!NOTE]
  > <span data-ttu-id="689cb-247">**에이전트 업데이트** 열에는 각 보호된 컴퓨터에 보호 에이전트 업데이트를 사용할 수 있는 시기가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-247">The **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="689cb-248">**작업** 창에서 **업데이트** 작업은 보호된 컴퓨터가 선택되고 업데이트가 사용 가능한 경우에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-248">In the **Actions** pane, the **Update** action is available only when a protected computer is selected and updates are available.</span></span>
  >
  >

3. <span data-ttu-id="689cb-249">선택된 컴퓨터에 업데이트된 보호 에이전트를 설치하려면 **작업** 창에서 **업데이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-249">To install updated protection agents on the selected computers, in the **Actions** pane, select **Update**.</span></span>

### <a name="update-a-protection-agent-on-a-client-computer-that-is-not-connected"></a><span data-ttu-id="689cb-250">연결되지 않은 클라이언트 컴퓨터에 대한 보호 에이전트 업데이트</span><span class="sxs-lookup"><span data-stu-id="689cb-250">Update a protection agent on a client computer that is not connected</span></span>

1. <span data-ttu-id="689cb-251">Backup Server 관리자 콘솔에서 **관리** > **에이전트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-251">In the Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="689cb-252">표시 창에서 보호 에이전트를 업데이트할 클라이언트 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-252">In the display pane, select the client computers for which you want to update the protection agent.</span></span>

  > [!NOTE]
   > <span data-ttu-id="689cb-253">**에이전트 업데이트** 열에는 각 보호된 컴퓨터에 보호 에이전트 업데이트를 사용할 수 있는 시기가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-253">The **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="689cb-254">업데이트가 사용 가능하지 않으면 보호된 컴퓨터가 선택된 경우 **작업** 창에서 **업데이트** 작업을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-254">In the **Actions** pane, the **Update** action is not available when a protected computer is selected unless updates are available.</span></span>
  >
  >

3. <span data-ttu-id="689cb-255">선택된 컴퓨터에 업데이트된 보호 에이전트를 설치하려면 **업데이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-255">To install updated protection agents on the selected computers, select **Update**.</span></span>

4. <span data-ttu-id="689cb-256">네트워크에 연결되지 않은 클라이언트 컴퓨터의 경우 컴퓨터가 네트워크에 연결될 때까지 **에이전트 상태** 열에는 **업데이트 보류 중** 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-256">For a client computer that is not connected to the network, until the computer is connected to the network, the **Agent Status** column shows a status of **Update Pending**.</span></span>

  <span data-ttu-id="689cb-257">클라이언트 컴퓨터가 네트워크에 연결된 후 클라이언트 컴퓨터에 대한 **에이전트 업데이트** 열에는 **업데이트 중** 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-257">After a client computer is connected to the network, the **Agent Updates** column for the client computer shows a status of **Updating**.</span></span>
  
### <a name="move-legacy-protection-groups-from-old-version-and-sync-the-new-version-with-azure"></a><span data-ttu-id="689cb-258">이전 버전에서 레거시 보호 그룹 이동 및 새 버전과 Azure 동기화</span><span class="sxs-lookup"><span data-stu-id="689cb-258">Move legacy Protection groups from old version and sync the new version with Azure</span></span>

<span data-ttu-id="689cb-259">Azure Backup Server와 OS가 모두 업데이트되면 Modern Backup Storage를 사용하여 새 데이터 원본을 보호할 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-259">Once Azure Backup Server and the OS are both updated, you are ready to protect new data sources using Modern Backup Storage.</span></span> <span data-ttu-id="689cb-260">이미지 보호된 데이터 원본은 Azure Backup Server에 있는 것처럼 레거시 방법으로 계속 보호되지만, 완전 새로운 보호 기능은 Modern Backup Storage를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-260">However already protected data sources will continue to be protected in the legacy way as they were in Azure Backup Server but all new protection will use Modern Backup Storage.</span></span>

<span data-ttu-id="689cb-261">아래 단계는 보호의 레거시 모드에서 Modern Backup Storage로 데이터 원본을 마이그레이션하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-261">Below steps are to migrate data sources from legacy  mode of protection to Modern backup storage.</span></span>

<span data-ttu-id="689cb-262">• 새 볼륨을 DPM 저장소 풀에 추가하고 원하는 경우 친숙한 이름과 데이터 원본 태그를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-262">• Add the new volume(s) to the DPM storage pool and assign friendly names and data source tags if desired.</span></span>
<span data-ttu-id="689cb-263">• 레거시 모드의 각 데이터 원본의 경우 데이터 원본의 보호를 중지하고 “보호된 데이터를 보존”합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-263">• For each data source that is in legacy mode, stop protection of the data sources and “Retain Protected Data”.</span></span>  <span data-ttu-id="689cb-264">이렇게 하면 마이그레이션 후 이전 복구 지점을 복구할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-264">This will allow recovery of old recovery points after migration.</span></span>

<span data-ttu-id="689cb-265">• 새 PG를 만들고 새 형식을 사용하여 저장할 수 있는 데이터 원본을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-265">• Create a new PG and select the data sources that are to be stored using new format.</span></span>
<span data-ttu-id="689cb-266">• DPM은 레거시 백업 저장소에서 Modern Backup Storage 볼륨으로 로컬에서 복제본 복사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-266">• DPM will do a replica copy from the legacy backup storage into the Modern Backup Storage volume locally.</span></span>
<span data-ttu-id="689cb-267">참고: 이 작업은 사후 복구 작업으로 간주됩니다. • 그런 다음 모든 새로운 동기화 및 복구 지점은 Modern Backup Storage에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-267">Note: This will be seen as a post-recovery operation job • All new sync and recovery points will then be stored in Modern Backup Storage.</span></span>
<span data-ttu-id="689cb-268">• 이전 복구 지점은 만료되면 사용할 수 없게 되며 결과적으로 디스크 공간은 늘어납니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-268">• Old recovery points will be pruned out as they expire and eventually free up the disk space.</span></span>
<span data-ttu-id="689cb-269">• 모든 기존 볼륨이 이전 저장소에서 삭제되면 디스크를 Azure Backup 및 시스템에서 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-269">• Once all the legacy volumes are deleted from the old storage, the disk can be removed from Azure backup and the system.</span></span>
<span data-ttu-id="689cb-270">• Azure DPMDB를 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-270">• Take a backup of the  Azure DPMDB.</span></span>

<span data-ttu-id="689cb-271">파트 2:-중요 항목 > 새 서버는 원래 Azure Backup Server와 같은 이름으로 지정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-271">Part 2: -Important items> The new server will need to be named same as the original Azure Backup server.</span></span> <span data-ttu-id="689cb-272">이전 저장소 풀 및 DPMDB을 사용하여 복구 지점을 유지하려는 경우 새 Azure Backup Server의 이름을 변경할 수 없습니다. 복원에 필요하므로 DPMDB의 백업본을 가지고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-272">You cannot change the name of the new Azure backup server if you want to use old storage pool and DPMDB to retain recovery points -Must have backup of DPMDB  as it will need to be restored</span></span>

1) <span data-ttu-id="689cb-273">원래 Azure Backup Server를 종료하거나 끕니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-273">Shutdown the original Azure backup server or take it off the wire.</span></span>
2) <span data-ttu-id="689cb-274">활성 디렉터리에서 컴퓨터 계정을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-274">Reset the machine account in active directory.</span></span>
3) <span data-ttu-id="689cb-275">새 컴퓨터에 Server 2016을 설치하고 원래 Azure Backup Server와 동일한 컴퓨터 이름으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-275">Install Server 2016 on new machine and name it the same machine name as the original Azure Backup server.</span></span>
4) <span data-ttu-id="689cb-276">도메인 조인</span><span class="sxs-lookup"><span data-stu-id="689cb-276">Join the Domain</span></span>
5) <span data-ttu-id="689cb-277">Azure Backup Server V2 설치(DPM 저장소 풀 디스크를 이전 서버에서 이동 및 가져오기)</span><span class="sxs-lookup"><span data-stu-id="689cb-277">Install Azure Backup server V2 (Move DPM Storage pool disks from old server and import)</span></span>
6) <span data-ttu-id="689cb-278">파트 2의 끝에서 가져온 DPMDB 복원</span><span class="sxs-lookup"><span data-stu-id="689cb-278">Restore the DPMDB taken from end of part 2</span></span>
7) <span data-ttu-id="689cb-279">저장소를 원래 백업 서버에서 새 서버로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-279">Attach the storage from the original backup server to the new server.</span></span>
8) <span data-ttu-id="689cb-280">SQL에서 DPMDB 복원</span><span class="sxs-lookup"><span data-stu-id="689cb-280">From SQL Restore the DPMDB</span></span>
9) <span data-ttu-id="689cb-281">새 서버의 관리 명령줄에서 Microsoft Azure Backup 설치 위치 및 bin 폴더로 cd</span><span class="sxs-lookup"><span data-stu-id="689cb-281">From admin command line on new server cd to Microsoft Azure Backup install location and bin folder</span></span>

<span data-ttu-id="689cb-282">경로 예: C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span><span class="sxs-lookup"><span data-stu-id="689cb-282">Path example: C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span></span>
<span data-ttu-id="689cb-283">Azure Backup, DPMSYNC -SYNC 실행</span><span class="sxs-lookup"><span data-stu-id="689cb-283">to Azure backup Run DPMSYNC -SYNC</span></span>

10) <span data-ttu-id="689cb-284">DPMSYNC -SYNC 실행 이전 것을 옮기는 대신 DPM Storage 풀에 새 디스크를 추가했다면 DPMSYNC -Reallocatereplica 실행</span><span class="sxs-lookup"><span data-stu-id="689cb-284">Run DPMSYNC -SYNC Note If you have added NEW disks to the DPM Storage pool instead of moving the old ones, then run DPMSYNC -Reallocatereplica</span></span>

## <a name="new-powershell-cmdlets-in-v2"></a><span data-ttu-id="689cb-285">v2의 새로운 PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="689cb-285">New PowerShell cmdlets in v2</span></span>

<span data-ttu-id="689cb-286">Azure Backup Server v2를 설치하면 두 개의 새로운 cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-286">When you install Azure Backup Server v2, two new cmdlets are available:</span></span> 
* [<span data-ttu-id="689cb-287">Mount-DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="689cb-287">Mount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787159.aspx)
* [<span data-ttu-id="689cb-288">Dismount-DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="689cb-288">Dismount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787158.aspx)

## <a name="next-steps"></a><span data-ttu-id="689cb-289">다음 단계</span><span class="sxs-lookup"><span data-stu-id="689cb-289">Next steps</span></span>

<span data-ttu-id="689cb-290">서버를 준비하는 방법을 알아보거나 워크로드 보호를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="689cb-290">Learn how to prepare your server or begin protecting a workload:</span></span>
- [<span data-ttu-id="689cb-291">Backup Server 워크로드 준비</span><span class="sxs-lookup"><span data-stu-id="689cb-291">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="689cb-292">Backup Server를 사용하여 VMware 서버 백업</span><span class="sxs-lookup"><span data-stu-id="689cb-292">Use Backup Server to back up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="689cb-293">Backup Server를 사용하여 SQL Server 백업</span><span class="sxs-lookup"><span data-stu-id="689cb-293">Use Backup Server to back up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="689cb-294">Backup Server에서 Modern Backup Storage 사용</span><span class="sxs-lookup"><span data-stu-id="689cb-294">Use Modern Backup Storage with Backup Server</span></span>](backup-mabs-add-storage.md)

