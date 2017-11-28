---
title: "Azure 백업 서버 v2 aaaInstall | Microsoft Docs"
description: "Azure Backup Server v2에서는 VM, 파일 및 폴더, 워크로드 등을 보호하기 위한 향상된 백업 기능을 제공합니다. 자세한 내용은 방법 tooinstall 또는 업그레이드 tooAzure 백업 서버 v 2입니다."
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
ms.openlocfilehash: 5b1699dadd3a173f1c0ef91a1a600bc5e12f20ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-azure-backup-server-v2"></a><span data-ttu-id="d3627-104">Azure Backup Server v2 설치</span><span class="sxs-lookup"><span data-stu-id="d3627-104">Install Azure Backup Server v2</span></span>

<span data-ttu-id="d3627-105">Azure Backup Server를 사용하여 VM(가상 컴퓨터), 워크로드, 파일 및 폴더 등을 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-105">Azure Backup Server helps protect your virtual machines (VMs), workloads, files and folders, and more.</span></span> <span data-ttu-id="d3627-106">Azure Backup Server v2는 Azure Backup Server v1을 기반으로 빌드되고 v1에서 사용할 수 없는 새로운 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-106">Azure Backup Server v2 builds on Azure Backup Server v1, and gives you new features that are not available in v1.</span></span> <span data-ttu-id="d3627-107">v1 및 v2의 기능 비교에 대해서는 [Azure Backup Server 보호 매트릭스](backup-mabs-protection-matrix.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3627-107">For a comparison of features between v1 and v2, see [Azure Backup Server protection matrix](backup-mabs-protection-matrix.md).</span></span> 

<span data-ttu-id="d3627-108">백업 서버 v 2에서 추가 기능 hello는 백업 서버 v 1에서 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-108">hello additional features in Backup Server v2 are an upgrade from Backup Server v1.</span></span> <span data-ttu-id="d3627-109">하지만 Backup Server v1은 Backup Server v2를 설치하기 위한 필수 구성 요소가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-109">However, Backup Server v1 is not a prerequisite for installing Backup Server v2.</span></span> <span data-ttu-id="d3627-110">백업 서버 v1 tooBackup 서버 v2에서에서 tooupgrade 원한다 면 hello 백업 서버 보호 서버에 백업 서버 v 2를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-110">If you want tooupgrade from Backup Server v1 tooBackup Server v2, install Backup Server v2 on hello Backup Server protection server.</span></span> <span data-ttu-id="d3627-111">기존 Backup Server 설정은 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-111">Your existing Backup Server settings remain intact.</span></span>

<span data-ttu-id="d3627-112">Backup Server v2를 Windows Server 2012 R2 또는 Windows Server 2016에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-112">You can install Backup Server v2 on Windows Server 2012 R2 or Windows Server 2016.</span></span> <span data-ttu-id="d3627-113">새 기능을 활용 tootake 같은 System Center 2016 데이터 보호 Manager 최신 백업 저장소, Windows Server 2016에는 백업 서버 v 2를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-113">tootake advantage of new features like System Center 2016 Data Protection Manager Modern Backup Storage, you must install Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="d3627-114">백업 서버 v2 tooor 설치를 업그레이드 하기 전에 hello에 대 한 읽기 [설치 필수 구성 요소](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-114">Before you upgrade tooor install Backup Server v2, read about hello [installation prerequisites](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span></span>

> [!NOTE]
> <span data-ttu-id="d3627-115">Azure 백업 서버 hello에 동일한 코드 베이스로 System Center Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="d3627-115">Azure Backup Server has hello same code base as System Center Data Protection Manager.</span></span> <span data-ttu-id="d3627-116">백업 서버 v 1은 해당 tooData Protection Manager 2012 R2, 및 백업 서버 v 2는 해당 tooData Protection Manager 2016 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-116">Backup Server v1 is equivalent tooData Protection Manager 2012 R2, and Backup Server v2 is equivalent tooData Protection Manager 2016.</span></span> <span data-ttu-id="d3627-117">이 문서는 가끔 hello Data Protection Manager 설명서를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-117">This article occasionally references hello Data Protection Manager documentation.</span></span>
>
>

## <a name="upgrade-backup-server-toov2"></a><span data-ttu-id="d3627-118">백업 서버 toov2 업그레이드</span><span class="sxs-lookup"><span data-stu-id="d3627-118">Upgrade Backup Server toov2</span></span>
<span data-ttu-id="d3627-119">tooupgrade 백업 서버 v1 tooBackup 서버 v 2에서에서 설치에 필요한 hello 업데이트가 설치 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-119">tooupgrade from Backup Server v1 tooBackup Server v2, make sure your installation has hello required updates:</span></span>

- <span data-ttu-id="d3627-120">[Hello 보호 에이전트 업데이트](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) hello에 서버를 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-120">[Update hello protection agents](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) on hello protected servers.</span></span>
- <span data-ttu-id="d3627-121">Windows Server 2012 R2 tooWindows Server 2016 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-121">Upgrade Windows Server 2012 R2 tooWindows Server 2016.</span></span>
- <span data-ttu-id="d3627-122">모든 프로덕션 서버에서 Azure Backup Server 원격 관리자를 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-122">Upgrade Azure Backup Server Remote Administrator on all production servers.</span></span>
- <span data-ttu-id="d3627-123">백업을 toocontinue 프로덕션 서버를 다시 시작 하지 않고 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-123">Ensure that backups are set toocontinue without restarting your production server.</span></span>


### <a name="upgrade-steps-for-backup-server-v2"></a><span data-ttu-id="d3627-124">Backup Server v2에 대한 업그레이드 단계</span><span class="sxs-lookup"><span data-stu-id="d3627-124">Upgrade steps for Backup Server v2</span></span>

1. <span data-ttu-id="d3627-125">Hello 다운로드 센터에서에서 [hello 업그레이드 설치 관리자 다운로드](https://go.microsoft.com/fwlink/?LinkId=626082)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-125">In hello Download Center, [download hello upgrade installer](https://go.microsoft.com/fwlink/?LinkId=626082).</span></span>

2. <span data-ttu-id="d3627-126">설치 마법사 hello 압축을 푼 후 다음 사항을 확인 **setup.exe를 실행** 을 선택한 다음 선택 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-126">After you extract hello setup wizard, make sure that **Execute setup.exe** is selected, and then select **Finish**.</span></span>

  ![설치 관리자 - 설치 프로그램 실행](./media/backup-mabs-upgrade-to-v2/run-setup.png)

3. <span data-ttu-id="d3627-128">Hello Microsoft Azure 백업 서버 마법사에서 아래 **설치**선택, **Microsoft Azure 백업 서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-128">In hello Microsoft Azure Backup Server wizard, under **Install**, select **Microsoft Azure Backup Server**.</span></span>

  ![설치 관리자 - 설치 선택](./media/backup-mabs-upgrade-to-v2/mabs-installer-s1.png)

4. <span data-ttu-id="d3627-130">Hello에 **시작** 페이지 hello 경고를 검토 한 다음 선택 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-130">On hello **Welcome** page, review hello warnings, and then select **Next**.</span></span>

  ![설치 관리자 - 시작 페이지](./media/backup-mabs-upgrade-to-v2/mabs-installer-s2.png)

5. <span data-ttu-id="d3627-132">hello 설치 마법사는 필수 구성 요소 검사 toomake 환경을 업그레이드할 수 있는지를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-132">hello setup wizard performs prerequisite checks toomake sure your environment can upgrade.</span></span> <span data-ttu-id="d3627-133">Hello에 **Prerequisite Checks** 페이지에서 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-133">On hello **Prerequisite Checks** page, select **Check**.</span></span>

  ![설치 관리자 - 필수 구성 요소 확인 페이지](./media/backup-mabs-upgrade-to-v2/mabs-installer-s3-perform-checks.png)

6. <span data-ttu-id="d3627-135">사용자 환경 hello 필수 구성 요소 검사를 통과 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-135">Your environment must pass hello prerequisite checks.</span></span> <span data-ttu-id="d3627-136">사용자 환경 hello 검사를 통과 하지 않는 hello 문제에 유의 수정 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d3627-136">If your environment doesn't pass hello checks, note hello issues and fix them.</span></span> <span data-ttu-id="d3627-137">그다음에 **다시 확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-137">Then, select **Check Again**.</span></span> <span data-ttu-id="d3627-138">Hello 필수 구성 요소 검사를 통과 한 후 선택 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-138">After you pass hello prerequisite checks, select **Next**.</span></span>

  ![설치 관리자 - 다시 확인 단추](./media/backup-mabs-upgrade-to-v2/mabs-installer-s4-pass-checks.png)

7. <span data-ttu-id="d3627-140">Hello에 **SQL 설정** 페이지 hello SQL 설치를 위한 관련 옵션을 선택 하 고 다음 선택 **확인 후 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-140">On hello **SQL Settings** page, select hello relevant option for your SQL installation, and then select **Check and Install**.</span></span>

  ![설치 관리자 - SQL 설정 페이지](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5-sql-settings.png)

  <span data-ttu-id="d3627-142">hello 검사 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-142">hello checks might take a few minutes.</span></span> <span data-ttu-id="d3627-143">Hello 검사는 완료, 선택 때 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-143">When hello checks are finished, select **Next**.</span></span>

  ![설치 관리자 - SQL 설정 확인 및 설치 단추](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5a-check-and fix-settings.png)

8. <span data-ttu-id="d3627-145">Hello에 **설치 설정** 페이지에서 백업 서버 설치 되어 있는 모든 변경 내용 toohello 위치 또는 toohello 스크래치 위치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-145">On hello **Installation Settings** page, make any changes toohello location where Backup Server is installed, or toohello Scratch Location.</span></span> <span data-ttu-id="d3627-146">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-146">Select **Next**.</span></span>

  ![설치 관리자 - 설치 설정 페이지](./media/backup-mabs-upgrade-to-v2/mabs-installer-s6-installation-settings.png)

9. <span data-ttu-id="d3627-148">toofinish hello 설치 마법사에서 선택 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-148">toofinish hello setup wizard, select **Finish**.</span></span>

  ![설치 관리자 - 마침](./media/backup-mabs-upgrade-to-v2/run-setup.png)



## <a name="add-storage-for-modern-backup-storage"></a><span data-ttu-id="d3627-150">Modern Backup Storage에 대한 저장소 추가</span><span class="sxs-lookup"><span data-stu-id="d3627-150">Add storage for Modern Backup Storage</span></span>

<span data-ttu-id="d3627-151">tooimprove 백업 저장소 효율성을 백업 서버 v2 볼륨에 대 한 지원을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-151">tooimprove backup storage efficiency, Backup Server v2 adds support for volumes.</span></span> <span data-ttu-id="d3627-152">Backup Server v1처럼 Backup Server v2는 디스크를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-152">Like Backup Server v1, Backup Server v2 supports disks.</span></span>

### <a name="add-volumes-and-disks"></a><span data-ttu-id="d3627-153">볼륨 및 디스크 추가</span><span class="sxs-lookup"><span data-stu-id="d3627-153">Add volumes and disks</span></span>
<span data-ttu-id="d3627-154">Windows Server 2016의 백업 서버 v 2를 실행 하는 경우에 볼륨 toostore 백업 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-154">If you run Backup Server v2 on Windows Server 2016, you can use volumes toostore backup data.</span></span> <span data-ttu-id="d3627-155">볼륨을 사용하면 저장소가 절약되고 더 빠르게 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-155">Volumes offer storage savings and faster backups.</span></span> <span data-ttu-id="d3627-156">볼륨은 새 tooBackup 서버 이기 때문에 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-156">Because volumes are new tooBackup Server, you must add them.</span></span> 

<span data-ttu-id="d3627-157">볼륨 tooBackup 서버를 추가 하면 hello 볼륨을는 친숙 한 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-157">When you add a volume tooBackup Server, you can give hello volume a friendly name.</span></span> <span data-ttu-id="d3627-158">Hello 클릭 **이름** 열 tooname hello 볼륨의 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-158">Click hello **Friendly Name** column of hello volume you want tooname.</span></span> <span data-ttu-id="d3627-159">필요한 경우 나중에 hello 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-159">You can change hello name later, if necessary.</span></span> <span data-ttu-id="d3627-160">또한 PowerShell tooadd 사용 하거나 변경할 수 있습니다 볼륨에 대 한 친숙 한 이름을 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-160">You also can use PowerShell tooadd or change friendly names for volumes.</span></span>

<span data-ttu-id="d3627-161">tooadd hello 관리자 콘솔에서에서 볼륨:</span><span class="sxs-lookup"><span data-stu-id="d3627-161">tooadd a volume in hello Administrator Console:</span></span>

1. <span data-ttu-id="d3627-162">Hello Azure 백업 서버 관리자 콘솔에서에서 선택 **관리** > **디스크 저장소** > **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-162">In hello Azure Backup Server Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![열기 hello 디스크 저장소 추가 마법사](./media//backup-mabs-upgrade-to-v2/open-add-disk-storage-wizard.png)

    <span data-ttu-id="d3627-164">Hello 디스크 저장소 추가 마법사를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-164">This opens hello Add Disk Storage wizard.</span></span>

2. <span data-ttu-id="d3627-165">Hello에 **디스크 저장소 추가** 페이지 hello **사용할 수 있는 볼륨** 상자 볼륨을 선택한 다음 선택 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-165">On hello **Add Disk Storage** page, in hello **Available volumes** box, select a volume, and then select **Add**.</span></span>
3. <span data-ttu-id="d3627-166">Hello에 **볼륨 선택** 상자 hello 볼륨에 대 한 이름을 입력 한 다음 선택 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-166">In hello **Selected volumes** box, enter a friendly name for hello volume, and then select **OK**.</span></span>

      ![디스크 저장소 추가 마법사 - 볼륨 추가](./media/backup-mabs-upgrade-to-v2/add-volume.png)

  <span data-ttu-id="d3627-168">디스크 tooadd 원한다 면 hello 디스크는 tooa 보호 그룹 레거시 저장소에 속해 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-168">If you want tooadd a disk, hello disk must belong tooa protection group that has legacy storage.</span></span> <span data-ttu-id="d3627-169">이러한 디스크는 해당 보호 그룹에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-169">These disks can only be used for these protection groups.</span></span> <span data-ttu-id="d3627-170">백업 서버에는 레거시 보호 된 원본의 없으면 hello 디스크 나열 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-170">If Backup Server doesn't have sources that have legacy protection, hello disk isn't listed.</span></span>

  <span data-ttu-id="d3627-171">디스크를 추가 하는 방법에 대 한 자세한 내용은 참조 [디스크 tooincrease 레거시 저장소 추가](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-171">For more information about adding disks, see [Adding disks tooincrease legacy storage](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span></span> <span data-ttu-id="d3627-172">디스크에는 이름을 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-172">You can't give a disk a friendly name.</span></span>


### <a name="assign-workloads-toovolumes"></a><span data-ttu-id="d3627-173">작업 부하 toovolumes 할당</span><span class="sxs-lookup"><span data-stu-id="d3627-173">Assign workloads toovolumes</span></span>

<span data-ttu-id="d3627-174">백업 서버 작업이 toowhich 볼륨에 할당 된 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-174">In Backup Server, you specify which workloads are assigned toowhich volumes.</span></span> <span data-ttu-id="d3627-175">예를 들어 비용이 많이 드는 볼륨을 지 원하는 많은 수의 두 번째 (IOPS) toostore 전용 작업 자주, 대용량 백업 해야 하는 초당 입력/출력 작업을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-175">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) toostore only workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="d3627-176">예를 들어 트랜잭션 로그가 포함된 SQL Server가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-176">An example is SQL Server with transaction logs.</span></span>

#### <a name="update-dpmdiskstorage"></a><span data-ttu-id="d3627-177">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="d3627-177">Update-DPMDiskStorage</span></span>

<span data-ttu-id="d3627-178">백업 서버 hello 저장소 풀의 볼륨의 tooupdate hello 속성 업데이트 DPMDiskStorage hello PowerShell cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-178">tooupdate hello properties of a volume in hello storage pool in Backup Server, use hello PowerShell cmdlet Update-DPMDiskStorage.</span></span>

<span data-ttu-id="d3627-179">구문</span><span class="sxs-lookup"><span data-stu-id="d3627-179">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

<span data-ttu-id="d3627-180">PowerShell을 사용 하 여 수행한 모든 변경 내용은 hello UI에에서 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-180">All changes that you make by using PowerShell are reflected in hello UI.</span></span>


## <a name="protect-data-sources"></a><span data-ttu-id="d3627-181">데이터 원본 보호</span><span class="sxs-lookup"><span data-stu-id="d3627-181">Protect data sources</span></span>
<span data-ttu-id="d3627-182">데이터 원본을 보호 하는 toobegin, 보호 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-182">toobegin protecting data sources, create a protection group.</span></span> <span data-ttu-id="d3627-183">hello 강조 변경 또는 추가 사항을 toohello 새 보호 그룹 마법사 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-183">hello following steps highlight changes or additions toohello New Protection Group wizard.</span></span>

<span data-ttu-id="d3627-184">보호 그룹 toocreate:</span><span class="sxs-lookup"><span data-stu-id="d3627-184">toocreate a protection group:</span></span>

1. <span data-ttu-id="d3627-185">Hello 백업 서버 관리자 콘솔에서에서 선택 **보호**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-185">In hello Backup Server Administrator Console, select **Protection**.</span></span>

2. <span data-ttu-id="d3627-186">Hello 도구 리본에서 선택 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-186">On hello tool ribbon, select **New**.</span></span>

    <span data-ttu-id="d3627-187">Hello 새 보호 그룹 만들기 마법사를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-187">This opens hello Create New Protection Group wizard.</span></span>

  ![새 보호 그룹 만들기 마법사](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-1.png)

3. <span data-ttu-id="d3627-189">Hello에 **시작** 페이지에서 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-189">On hello **Welcome** page, select **Next**.</span></span>
4. <span data-ttu-id="d3627-190">Hello에 **보호 그룹 종류 선택** 페이지에서 보호 그룹 toocreate, 한 다음 선택의 hello 유형을 선택 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-190">On hello **Select Protection Group Type** page, select hello type of protection group you want toocreate, and then select **Next**.</span></span>

  ![보호 그룹 형식 선택 페이지](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-2.png)

5. <span data-ttu-id="d3627-192">Hello에 **그룹 구성원 선택** 페이지 hello **사용 가능한 구성원** 창, hello 구성원과 보호 에이전트와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-192">On hello **Select Group Members** page, in hello **Available members** pane, hello members with protection agents are listed.</span></span> <span data-ttu-id="d3627-193">예를 들어 D:\ 볼륨을 선택 하 고 E:\ toohello 추가할 **선택한 구성원** 창.</span><span class="sxs-lookup"><span data-stu-id="d3627-193">For this example, select volume D:\ and E:\ and add them toohello **Selected members** pane.</span></span> <span data-ttu-id="d3627-194">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-194">Select **Next**.</span></span>

  ![그룹 구성원 선택 페이지](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-3.png)

6. <span data-ttu-id="d3627-196">Hello에 **데이터 보호 방법 선택** 페이지에서 입력 한 **보호 그룹 이름이**hello 보호 방법을 선택한 다음 선택 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-196">On hello **Select Data Protection Method** page, enter a **Protection group name**, select hello protection method, and then select **Next**.</span></span> <span data-ttu-id="d3627-197">단기 보호 하려는 경우에 hello 선택 해야 **디스크** 메서드를 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-197">If you want short-term protection, you must select hello **Disk** backup method.</span></span>

  ![데이터 보호 방법 선택 페이지](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-4.png)

7. <span data-ttu-id="d3627-199">Hello에 **단기 목표 지정** 페이지에 대 한 세부 정보 선택 hello **보존 범위** 및 **동기화 빈도**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-199">On hello **Specify Short-Term Goals** page, select hello details for **Retention range** and **Synchronization frequency**.</span></span> <span data-ttu-id="d3627-200">그다음에 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-200">Then, select **Next**.</span></span> <span data-ttu-id="d3627-201">필요에 따라 toochange hello 일정을 작성, 선택 복구 지점이 표시 되는 경우 **수정**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-201">Optionally, toochange hello schedule for when recovery points are taken, select **Modify**.</span></span>

  ![단기 목표 지정 페이지](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-5.png)

8. <span data-ttu-id="d3627-203">Hello에 **디스크 저장소 할당 검토** 페이지 선택한 hello 데이터 원본에 대 한 세부 정보, 크기 및 hello 공간 toobe 프로 비전에 대 한 값을 검토 하 고 대상 저장소 볼륨 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-203">On hello **Review Disk Storage Allocation** page, review details about hello data sources you selected, their size, and  values for hello space toobe provisioned and hello target storage volume.</span></span>

  ![디스크 저장소 할당 검토 페이지](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-6.png)

  <span data-ttu-id="d3627-205">저장소 볼륨 hello 작업 볼륨 할당 (PowerShell을 사용 하 여 설정)를 기반으로 하 고 사용 가능한 저장소 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-205">Storage volumes are based on hello workload volume allocation (set by using PowerShell) and hello available storage.</span></span> <span data-ttu-id="d3627-206">Hello 드롭 다운 메뉴에서 다른 볼륨을 선택 하 여 hello 저장소 볼륨을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-206">You can change hello storage volumes by selecting other volumes in hello drop-down menu.</span></span> <span data-ttu-id="d3627-207">Hello 값을 변경 하는 경우 **대상 저장소**, 값에 대 한 hello **사용 가능한 디스크 저장소** tooreflect 아래에 값을 동적으로 변경 **여유 공간이** 및 **공간 underprovisioned**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-207">If you change hello value for **Target Storage**, hello value for **Available disk storage** dynamically changes tooreflect values under **Free Space** and **Underprovisioned Space**.</span></span>

  <span data-ttu-id="d3627-208">데이터 원본 hello 증가 함에 따라 계획 한 대로 경우 hello hello에 대 한 값 **Underprovisioned 공간** 열에 **사용 가능한 디스크 저장소** hello 필요한 추가 저장소 크기를 반영 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-208">If hello data sources grow as planned, hello value for hello **Underprovisioned Space** column in **Available disk storage** reflects hello amount of additional storage that's needed.</span></span> <span data-ttu-id="d3627-209">저장소 요구량 부드러운 백업에 대 한이 값 toohelp 계획을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-209">Use this value toohelp plan your storage needs for smooth backups.</span></span> <span data-ttu-id="d3627-210">Hello 값이 0 이면 많은 경우 저장소에 잠재적 문제가 없는지 hello 장래에 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-210">If hello value is zero, there are no potential problems with storage in hello foreseeable future.</span></span> <span data-ttu-id="d3627-211">할당 된 충분 한 저장소가 없는 hello 값이 0이 아닌 숫자 이면 (보호 된 멤버의 사용자 보호 정책 및 hello 데이터 크기에 따라).</span><span class="sxs-lookup"><span data-stu-id="d3627-211">If hello value is a number other than zero, you do not have sufficient storage allocated  (based on your protection policy and hello data size of your protected members).</span></span>

  ![미달 할당된 디스크 저장소](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-7.png)

   <span data-ttu-id="d3627-213">보호 그룹, 전체 hello 마법사 만들기 toofinish 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-213">toofinish creating your protection group, complete hello wizard.</span></span>

## <a name="migrate-legacy-storage-toomodern-backup-storage"></a><span data-ttu-id="d3627-214">레거시 저장소 tooModern 백업 저장소 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="d3627-214">Migrate legacy storage tooModern Backup Storage</span></span>
<span data-ttu-id="d3627-215">백업 서버 v2 tooor 설치 및 업그레이드 hello 운영 체제 tooWindows Server 2016로 업그레이드 한 후 보호 그룹 toouse 최신 백업 저장소를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-215">After you upgrade tooor install Backup Server v2 and upgrade hello operating system tooWindows Server 2016, update your protection groups toouse Modern Backup Storage.</span></span> <span data-ttu-id="d3627-216">기본적으로 보호 그룹은 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-216">By default, protection groups are not changed.</span></span> <span data-ttu-id="d3627-217">처음 설정 된 것 처럼 toofunction을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-217">They continue toofunction as they were initially set up.</span></span> 

<span data-ttu-id="d3627-218">보호 그룹 toouse 최신 백업 저장소를 업데이트 하는 것은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-218">Updating protection groups toouse Modern Backup Storage is optional.</span></span> <span data-ttu-id="d3627-219">tooupdate hello 보호 그룹 데이터 옵션을 보관 하는 hello를 사용 하 여 모든 데이터 원본의 보호를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-219">tooupdate hello protection group, stop protection of all data sources by using hello retain data option.</span></span> <span data-ttu-id="d3627-220">Hello 데이터 원본 tooa 새 보호 그룹을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-220">Then, add hello data sources tooa new protection group.</span></span>

1. <span data-ttu-id="d3627-221">Hello 관리자 콘솔에서에서 선택 hello **보호** 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-221">In hello Administrator Console, select hello **Protection** feature.</span></span> <span data-ttu-id="d3627-222">Hello에 **보호 그룹 구성원** 목록 오른쪽 hello 멤버를 마우스 오른쪽 단추로 클릭 한 다음 선택 **구성원 보호 중지**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-222">In hello **Protection Group Member** list, right-click hello member, and then select **Stop protection of member**.</span></span>

  ![구성원 보호 중지](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-stop-protection1.png)

2. <span data-ttu-id="d3627-224">Hello에 **그룹에서 제거** 대화 상자, 검토 hello 사용 되는 디스크 공간 및 hello hello 저장소 풀에 사용 가능한 공간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-224">In hello **Remove from Group** dialog box, review hello used disk space and hello available free space for hello storage pool.</span></span> <span data-ttu-id="d3627-225">hello 기본 hello 디스크에 tooleave hello 복구 지점 이며 해당 관련된 보존 정책에 따라 tooexpire를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-225">hello default is tooleave hello recovery points on hello disk and allow them tooexpire per their associated retention policy.</span></span> <span data-ttu-id="d3627-226">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-226">Click **OK**.</span></span>

  <span data-ttu-id="d3627-227">Tooimmediately 반환 hello 사용 되는 디스크 공간 toohello 사용 가능한 저장소 풀을 사용 하도록 하려는 경우 선택 hello **디스크에서 복제본 삭제** 해당 멤버와 연결 된 확인란 toodelete hello에 대 한 백업 데이터 (및 복구 지점)입니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-227">If you want tooimmediately return hello used disk space toohello free storage pool, select hello **Delete replica on disk** check box toodelete hello backup data (and recovery points) associated with that member.</span></span>

  ![그룹에서 제거 대화 상자](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-retain-data.png)

3. <span data-ttu-id="d3627-229">Modern Backup Storage를 사용하는 보호 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-229">Create a protection group that uses Modern Backup Storage.</span></span> <span data-ttu-id="d3627-230">보호 되지 않은 상태로 hello 데이터 소스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-230">Include hello unprotected data sources.</span></span>


## <a name="add-disks-tooincrease-legacy-storage"></a><span data-ttu-id="d3627-231">디스크 tooincrease 레거시 저장소 추가</span><span class="sxs-lookup"><span data-stu-id="d3627-231">Add disks tooincrease legacy storage</span></span>

<span data-ttu-id="d3627-232">백업 서버와 toouse 레거시 저장 하려는 경우 tooadd 디스크 tooincrease 레거시 저장소를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-232">If you want toouse legacy storage with Backup Server, you might need tooadd disks tooincrease legacy storage.</span></span> 

<span data-ttu-id="d3627-233">tooadd 디스크 저장소:</span><span class="sxs-lookup"><span data-stu-id="d3627-233">tooadd disk storage:</span></span>

1. <span data-ttu-id="d3627-234">Hello 관리자 콘솔에서에서 선택 **관리** > **디스크 저장소** > **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-234">In hello Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![디스크 저장소 추가 대화 상자](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-add-disk-storage.png)

4. <span data-ttu-id="d3627-236">Hello에 **디스크 저장소 추가** 대화 상자에서 **디스크 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-236">In hello **Add Disk Storage** dialog, select **Add disks**.</span></span>

5. <span data-ttu-id="d3627-237">사용 가능한 디스크의 hello 목록에서 선택 tooadd, hello 디스크 **추가**를 선택한 후 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-237">In hello list of available disks, select hello disks you want tooadd, select **Add**, and then select **OK**.</span></span>

## <a name="update-hello-data-protection-manager-protection-agent"></a><span data-ttu-id="d3627-238">Hello Data Protection Manager 보호 에이전트를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-238">Update hello Data Protection Manager protection agent</span></span>

<span data-ttu-id="d3627-239">백업 서버 업데이트에 대 한 hello System Center Data Protection Manager 보호 에이전트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-239">Backup Server uses hello System Center Data Protection Manager protection agent for updates.</span></span> <span data-ttu-id="d3627-240">연결 된 toohello 네트워크를 보호 에이전트를 업그레이드 하는 hello 관리자 콘솔 toocomplete 연결된 된 에이전트 업그레이드를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-240">If you are upgrading a protection agent that is not connected toohello network, you cannot use hello Data Protection Manager Administrator Console toocomplete a connected agent upgrade.</span></span> <span data-ttu-id="d3627-241">비활성 도메인 환경에서 hello 보호 에이전트를 업그레이드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-241">You must upgrade hello protection agent in a nonactive domain environment.</span></span> <span data-ttu-id="d3627-242">Hello 클라이언트 컴퓨터가 연결 된 toohello 네트워크 인 될 때까지 관리자 콘솔에서 해당 hello 보호 에이전트 업데이트 표시 hello 보류 중입니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-242">Until hello client computer is connected toohello network, hello Data Protection Manager Administrator Console shows that hello protection agent update is pending.</span></span>

<span data-ttu-id="d3627-243">hello 다음 섹션에서는 설명 어떻게 연결 되어 있는 클라이언트 컴퓨터와 연결 되지 않은 클라이언트 컴퓨터에 대 한 보호 에이전트 tooupdate 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-243">hello following sections describe how tooupdate protection agents for client computers that are connected and client computers that are not connected.</span></span>

### <a name="update-a-protection-agent-for-a-connected-client-computer"></a><span data-ttu-id="d3627-244">연결된 클라이언트 컴퓨터에 대한 보호 에이전트 업데이트</span><span class="sxs-lookup"><span data-stu-id="d3627-244">Update a protection agent for a connected client computer</span></span>

1. <span data-ttu-id="d3627-245">Hello 백업 서버 관리자 콘솔에서에서 선택 **관리** > **에이전트**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-245">In hello Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="d3627-246">Hello 디스플레이 창에서 원하는 tooupdate hello 보호 에이전트를 hello 클라이언트 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-246">In hello display pane, select hello client computers for which you want tooupdate hello protection agent.</span></span>

  > [!NOTE]
  > <span data-ttu-id="d3627-247">hello **에이전트 업데이트** 보호 에이전트 업데이트를 각 보호 된 컴퓨터에 사용할 수 있는 경우 열에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-247">hello **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="d3627-248">Hello에 **동작** 창, hello **업데이트** 작업은 사용할 수 있고 경우에 보호 된 컴퓨터가 선택 된 업데이트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-248">In hello **Actions** pane, hello **Update** action is available only when a protected computer is selected and updates are available.</span></span>
  >
  >

3. <span data-ttu-id="d3627-249">tooinstall hello에 hello 선택한 컴퓨터에 보호 에이전트 업데이트 **동작** 창 선택 **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-249">tooinstall updated protection agents on hello selected computers, in hello **Actions** pane, select **Update**.</span></span>

### <a name="update-a-protection-agent-on-a-client-computer-that-is-not-connected"></a><span data-ttu-id="d3627-250">연결되지 않은 클라이언트 컴퓨터에 대한 보호 에이전트 업데이트</span><span class="sxs-lookup"><span data-stu-id="d3627-250">Update a protection agent on a client computer that is not connected</span></span>

1. <span data-ttu-id="d3627-251">Hello 백업 서버 관리자 콘솔에서에서 선택 **관리** > **에이전트**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-251">In hello Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="d3627-252">Hello 디스플레이 창에서 원하는 tooupdate hello 보호 에이전트를 hello 클라이언트 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-252">In hello display pane, select hello client computers for which you want tooupdate hello protection agent.</span></span>

  > [!NOTE]
   > <span data-ttu-id="d3627-253">hello **에이전트 업데이트** 보호 에이전트 업데이트를 각 보호 된 컴퓨터에 사용할 수 있는 경우 열에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-253">hello **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="d3627-254">Hello에 **동작** 창, hello **업데이트** 없는데 보호 된 컴퓨터에서 선택 된 업데이트를 사용할 수 있는 경우이 작업은 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-254">In hello **Actions** pane, hello **Update** action is not available when a protected computer is selected unless updates are available.</span></span>
  >
  >

3. <span data-ttu-id="d3627-255">tooinstall hello 선택한 컴퓨터에 보호 에이전트 업데이트 **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-255">tooinstall updated protection agents on hello selected computers, select **Update**.</span></span>

4. <span data-ttu-id="d3627-256">Hello 컴퓨터에 연결 된 toohello 네트워크 될 때까지 toohello 네트워크 연결 되지 않은 클라이언트 컴퓨터에 대 한 hello **에이전트 상태** 열 표시의 상태 **업데이트 보류 중**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-256">For a client computer that is not connected toohello network, until hello computer is connected toohello network, hello **Agent Status** column shows a status of **Update Pending**.</span></span>

  <span data-ttu-id="d3627-257">클라이언트 컴퓨터에 연결 된 toohello 네트워크 되 면 hello **에이전트 업데이트** hello 클라이언트 컴퓨터에 대 한 열에 상태가 표시 **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-257">After a client computer is connected toohello network, hello **Agent Updates** column for hello client computer shows a status of **Updating**.</span></span>
  
### <a name="move-legacy-protection-groups-from-old-version-and-sync-hello-new-version-with-azure"></a><span data-ttu-id="d3627-258">이전 버전 및 Azure 사용한 동기화 hello 새 버전에서 기존 보호 그룹 이동</span><span class="sxs-lookup"><span data-stu-id="d3627-258">Move legacy Protection groups from old version and sync hello new version with Azure</span></span>

<span data-ttu-id="d3627-259">Azure 백업 서버 및 운영 체제 hello 모두 업데이트 되 준비 tooprotect 최신 백업 저장소를 사용 하는 새 데이터 원본이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-259">Once Azure Backup Server and hello OS are both updated, you are ready tooprotect new data sources using Modern Backup Storage.</span></span> <span data-ttu-id="d3627-260">그러나 이미 보호 된 데이터 원본 toobe 방식으로 Azure 백업 서버에 있는 것 이지만 모든 새 보호 그룹에서 최신 백업 저장소를 사용 하는 레거시 hello에서 보호를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-260">However already protected data sources will continue toobe protected in hello legacy way as they were in Azure Backup Server but all new protection will use Modern Backup Storage.</span></span>

<span data-ttu-id="d3627-261">다음 단계는 toomigrate 데이터 소스 보호 tooModern 백업 저장소의 레거시 모드에서입니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-261">Below steps are toomigrate data sources from legacy  mode of protection tooModern backup storage.</span></span>

<span data-ttu-id="d3627-262">•는 Hello 새 볼륨 toohello DPM 저장소 풀을 추가 하 고 원하는 경우 친숙 한 이름 및 데이터 소스 태그를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-262">• Add hello new volume(s) toohello DPM storage pool and assign friendly names and data source tags if desired.</span></span>
<span data-ttu-id="d3627-263">레거시 모드에서는 보호를 중지 하 고 "보호 된 데이터 보존" hello 데이터 원본에에서 있는 각 데이터 원본에 대 한 • 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-263">• For each data source that is in legacy mode, stop protection of hello data sources and “Retain Protected Data”.</span></span>  <span data-ttu-id="d3627-264">이렇게 하면 마이그레이션 후 이전 복구 지점을 복구할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-264">This will allow recovery of old recovery points after migration.</span></span>

<span data-ttu-id="d3627-265">• 새 PG 만들고 toobe 새 형식을 사용 하 여 저장 하는 hello 데이터 원본이 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-265">• Create a new PG and select hello data sources that are toobe stored using new format.</span></span>
<span data-ttu-id="d3627-266">• DPM hello 최신 백업 저장소 볼륨을 로컬에 hello 레거시 백업 저장소에서 복제본 복사를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-266">• DPM will do a replica copy from hello legacy backup storage into hello Modern Backup Storage volume locally.</span></span>
<span data-ttu-id="d3627-267">참고: 이 작업은 사후 복구 작업으로 간주됩니다. • 그런 다음 모든 새로운 동기화 및 복구 지점은 Modern Backup Storage에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-267">Note: This will be seen as a post-recovery operation job • All new sync and recovery points will then be stored in Modern Backup Storage.</span></span>
<span data-ttu-id="d3627-268">• 이전 복구 지점이 만료 되 고 결국 hello 디스크 공간을 확보 아웃 정리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-268">• Old recovery points will be pruned out as they expire and eventually free up hello disk space.</span></span>
<span data-ttu-id="d3627-269">• 모든 hello 레거시 볼륨 hello 이전 저장소를 hello 디스크에서 삭제 한 후 Azure 백업 및 hello 시스템에서 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-269">• Once all hello legacy volumes are deleted from hello old storage, hello disk can be removed from Azure backup and hello system.</span></span>
<span data-ttu-id="d3627-270">•는 Hello Azure DPMDB의 백업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-270">• Take a backup of hello  Azure DPMDB.</span></span>

<span data-ttu-id="d3627-271">2 부:-중요 한 항목 > 새 서버 hello toobe hello 원래 Azure 백업 서버와 같은 이름으로 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-271">Part 2: -Important items> hello new server will need toobe named same as hello original Azure Backup server.</span></span> <span data-ttu-id="d3627-272">Toouse 이전 저장소 풀에서 사용할 DPMDB tooretain 복구 지점-있어야 DPMDB의 백업을 복원 toobe 필요 하는 경우에 hello 이름을 hello 새 Azure 백업 서버를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-272">You cannot change hello name of hello new Azure backup server if you want toouse old storage pool and DPMDB tooretain recovery points -Must have backup of DPMDB  as it will need toobe restored</span></span>

1) <span data-ttu-id="d3627-273">종료 원래 Azure 백업 서버 hello 또는 hello 와이어 오프 라인입니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-273">Shutdown hello original Azure backup server or take it off hello wire.</span></span>
2) <span data-ttu-id="d3627-274">Active directory의 hello 컴퓨터 계정 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-274">Reset hello machine account in active directory.</span></span>
3) <span data-ttu-id="d3627-275">원래 Azure 백업 서버 hello와 동일한 컴퓨터 이름을 hello 이름과 새 컴퓨터에 서버 2016을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-275">Install Server 2016 on new machine and name it hello same machine name as hello original Azure Backup server.</span></span>
4) <span data-ttu-id="d3627-276">Hello 도메인 가입</span><span class="sxs-lookup"><span data-stu-id="d3627-276">Join hello Domain</span></span>
5) <span data-ttu-id="d3627-277">Azure Backup Server V2 설치(DPM 저장소 풀 디스크를 이전 서버에서 이동 및 가져오기)</span><span class="sxs-lookup"><span data-stu-id="d3627-277">Install Azure Backup server V2 (Move DPM Storage pool disks from old server and import)</span></span>
6) <span data-ttu-id="d3627-278">2 부의 끝에서 가져온 DPMDB hello 복원</span><span class="sxs-lookup"><span data-stu-id="d3627-278">Restore hello DPMDB taken from end of part 2</span></span>
7) <span data-ttu-id="d3627-279">Hello 원본 서버 백업 toohello 새 서버에서 hello 저장소에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-279">Attach hello storage from hello original backup server toohello new server.</span></span>
8) <span data-ttu-id="d3627-280">SQL 복원 hello DPMDB에서</span><span class="sxs-lookup"><span data-stu-id="d3627-280">From SQL Restore hello DPMDB</span></span>
9) <span data-ttu-id="d3627-281">관리자의 새로운 서버 cd tooMicrosoft Azure 백업에서 명령줄 설치 위치 및 bin 폴더</span><span class="sxs-lookup"><span data-stu-id="d3627-281">From admin command line on new server cd tooMicrosoft Azure Backup install location and bin folder</span></span>

<span data-ttu-id="d3627-282">경로 예: C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span><span class="sxs-lookup"><span data-stu-id="d3627-282">Path example: C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span></span>
<span data-ttu-id="d3627-283">tooAzure 백업 실행 DPMSYNC-SYNC</span><span class="sxs-lookup"><span data-stu-id="d3627-283">tooAzure backup Run DPMSYNC -SYNC</span></span>

10) <span data-ttu-id="d3627-284">Dpmsync-SYNC 참고 hello 이전 구성을 이동 하는 대신 새 toohello DPM 저장소 풀 디스크를 추가한 경우 DPMSYNC-Reallocatereplica 실행 한 다음</span><span class="sxs-lookup"><span data-stu-id="d3627-284">Run DPMSYNC -SYNC Note If you have added NEW disks toohello DPM Storage pool instead of moving hello old ones, then run DPMSYNC -Reallocatereplica</span></span>

## <a name="new-powershell-cmdlets-in-v2"></a><span data-ttu-id="d3627-285">v2의 새로운 PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="d3627-285">New PowerShell cmdlets in v2</span></span>

<span data-ttu-id="d3627-286">Azure Backup Server v2를 설치하면 두 개의 새로운 cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3627-286">When you install Azure Backup Server v2, two new cmdlets are available:</span></span> 
* [<span data-ttu-id="d3627-287">Mount-DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="d3627-287">Mount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787159.aspx)
* [<span data-ttu-id="d3627-288">Dismount-DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="d3627-288">Dismount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787158.aspx)

## <a name="next-steps"></a><span data-ttu-id="d3627-289">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d3627-289">Next steps</span></span>

<span data-ttu-id="d3627-290">자세한 내용은 방법 tooprepare 서버 작업 보호를 시작 하거나:</span><span class="sxs-lookup"><span data-stu-id="d3627-290">Learn how tooprepare your server or begin protecting a workload:</span></span>
- [<span data-ttu-id="d3627-291">Backup Server 워크로드 준비</span><span class="sxs-lookup"><span data-stu-id="d3627-291">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="d3627-292">백업 서버 tooback VMware 서버를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="d3627-292">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="d3627-293">SQL Server를 tooback 백업 서버를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="d3627-293">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="d3627-294">Backup Server에서 Modern Backup Storage 사용</span><span class="sxs-lookup"><span data-stu-id="d3627-294">Use Modern Backup Storage with Backup Server</span></span>](backup-mabs-add-storage.md)

