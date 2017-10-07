---
title: "aaaRestore 데이터 tooa Windows Server 또는 Windows 클라이언트에서 사용 하 여 Azure 클래식 배포 모델을 hello | Microsoft Docs"
description: "자세한 방법을 toorestore Windows 서버 또는 Windows 클라이언트에서."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 85585dfc-c764-4e8c-8f0e-40b969640ac2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 4d1458d5233c4f55004ecfa95cbf7b3b18a03dde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-hello-classic-deployment-model"></a><span data-ttu-id="8e1fd-103">파일 tooa Windows server 또는 hello 클래식 배포 모델을 사용 하 여 Windows 클라이언트 컴퓨터를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-103">Restore files tooa Windows server or Windows client machine using hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8e1fd-104">클래식 포털</span><span class="sxs-lookup"><span data-stu-id="8e1fd-104">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
> * [<span data-ttu-id="8e1fd-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="8e1fd-105">Azure portal</span></span>](backup-azure-restore-windows-server.md)
>
>

<span data-ttu-id="8e1fd-106">이 문서에서는 toorecover 데이터 백업에서 자격 증명 모음 및 tooa 서버나 컴퓨터로 복원 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-106">This article explains how toorecover data from a backup vault and restore it tooa server or computer.</span></span> <span data-ttu-id="8e1fd-107">2017 년 3 월 부터는 hello 클래식 포털에서 백업 자격 증명 모음을 더 이상 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-107">Starting in March 2017, you can no longer create backup vaults in hello classic portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e1fd-108">이제 사용자 백업 자격 증명 모음 tooRecovery 서비스 자격 증명 모음을 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-108">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="8e1fd-109">자세한 내용은 hello 문서 참조 [복구 서비스 자격 증명 모음에 백업 자격 증명 모음 tooa 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-109">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="8e1fd-110">Microsoft는 것이 권장 tooupgrade 백업 tooRecovery 서비스 자격 증명 모음 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-110">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="8e1fd-111">**2017 년 10 월 15**, 수 toouse PowerShell toocreate 백업 자격 증명 모음은 더 이상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-111">**October 15, 2017**, you will no longer be able toouse PowerShell toocreate Backup vaults.</span></span> <br/> <span data-ttu-id="8e1fd-112">**2017년 11월 1일 시작**:</span><span class="sxs-lookup"><span data-stu-id="8e1fd-112">**Starting November 1, 2017**:</span></span>
>- <span data-ttu-id="8e1fd-113">나머지 모든 백업 자격 증명 모음을 자동으로 업그레이드 된 tooRecovery 서비스 자격 증명 모음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-113">Any remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="8e1fd-114">하면 hello 클래식 포털에서 수 tooaccess 백업 데이터 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-114">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="8e1fd-115">대신, 복구 서비스 자격 증명 모음에 hello Azure 포털 tooaccess 백업 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-115">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

<span data-ttu-id="8e1fd-116">hello Microsoft Azure 복구 서비스 (MARS) 에이전트에서 hello 데이터 복구 마법사를 사용 하면 toorestore 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-116">toorestore data, you use hello Recover Data wizard in hello Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="8e1fd-117">데이터를 복원하면 다음이 가능해집니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-117">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="8e1fd-118">동일 컴퓨터에서 hello 백업을 복원 데이터 toohello 수행 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-118">Restore data toohello same machine from which hello backups were taken.</span></span>
* <span data-ttu-id="8e1fd-119">데이터 tooan 대체 컴퓨터를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-119">Restore data tooan alternate machine.</span></span>

<span data-ttu-id="8e1fd-120">2017 년 1 월 Microsoft는 미리 보기 업데이트 toohello MARS 에이전트를 릴리스 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-120">In January 2017, Microsoft released a Preview update toohello MARS agent.</span></span> <span data-ttu-id="8e1fd-121">버그 수정 프로그램과 함께이 업데이트를 통해 toomount 수 있는 인스턴트 복원 쓰기 가능한 복구 지점 스냅숏을 복구 볼륨으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-121">Along with bug fixes, this update enables Instant Restore, which allows you toomount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="8e1fd-122">그런 다음 hello 복구 볼륨 및 복사 파일 tooa 로컬 컴퓨터 파일을 복원 함으로써 선택적으로 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-122">You can then explore hello recovery volume and copy files tooa local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="8e1fd-123">hello [2017 년 1 월 Azure Backup 업데이트](https://support.microsoft.com/en-us/help/3216528?preview) 는 toouse toorestore 데이터 인스턴트 복원 하려는 경우에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-123">hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want toouse Instant Restore toorestore data.</span></span> <span data-ttu-id="8e1fd-124">또한 로캘에서 hello 지원 문서에 나열 된 자격 증명 모음에 hello 백업 데이터를 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-124">Also hello backup data must be protected in vaults in locales listed in hello support article.</span></span> <span data-ttu-id="8e1fd-125">Hello 참조 [2017 년 1 월 Azure Backup 업데이트](https://support.microsoft.com/en-us/help/3216528?preview) hello 최신 목록은 로캘 지 원하는 즉시 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-125">Consult hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for hello latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="8e1fd-126">즉시 복원은 현재 **일부** 로캘에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-126">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="8e1fd-127">클래식 포털 hello 인스턴트 복원 hello Azure 포털에서에서 복구 서비스 자격 증명 모음에서 사용 하 고 백업 자격 증명 모음은 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-127">Instant Restore is available for use in Recovery Services vaults in hello Azure portal and Backup vaults in hello classic portal.</span></span> <span data-ttu-id="8e1fd-128">Toouse 인스턴트 복원 하려는 경우 hello MARS 업데이트를 다운로드 하 고 인스턴트 복원 언급 하는 hello 절차를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-128">If you want toouse Instant Restore, download hello MARS update, and follow hello procedures that mention Instant Restore.</span></span>


## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a><span data-ttu-id="8e1fd-129">Toorecover 데이터 toohello 인스턴트 Restore를 사용 하 여 동일한 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="8e1fd-129">Use Instant Restore toorecover data toohello same machine</span></span>

<span data-ttu-id="8e1fd-130">파일 및 희망 toorestore 실수로 삭제 한 경우이 단계를 같은 컴퓨터 (어떤 hello에서 백업을 수행할 때) 다음 hello toohello hello 데이터를 복구 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-130">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="8e1fd-131">열기 hello **Microsoft Azure 백업** 에 snap 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-131">Open hello **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="8e1fd-132">Hello 컴퓨터 또는 서버 hello 스냅인에 설치 된 알 수 없는 경우 검색 **Microsoft Azure 백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-132">If you don't know where hello snap in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="8e1fd-133">hello를 데스크톱 응용 프로그램 hello 검색 결과에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-133">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="8e1fd-134">클릭 **데이터 복구** toostart hello 마법사.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-134">Click **Recover Data** toostart hello wizard.</span></span>

    ![데이터 복구](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="8e1fd-136">Hello에 **시작** 창, toorestore hello 데이터 toohello 동일한 서버 또는 컴퓨터 선택 **이 서버 (`<server name>`)** 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-136">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![이 서버 옵션 toorestore hello 데이터 toohello 선택 동일한 컴퓨터](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="8e1fd-138">Hello에 **복구 모드 선택** 창 선택 **개별 파일과 폴더** 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-138">On hello **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![파일 찾아보기](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="8e1fd-140">Hello에 **볼륨 및 날짜 선택** 창, hello 파일 및/또는 toorestore 폴더를 포함 하는 select hello 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-140">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="8e1fd-141">Hello 달력에서 복구 지점을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-141">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="8e1fd-142">어떤 복구 시점에서라도 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-142">You can restore from any recovery point in time.</span></span> <span data-ttu-id="8e1fd-143">날짜 **굵게** 복구 지점이 하나 이상 hello 가용성을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-143">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="8e1fd-144">여러 복구 지점을 사용할 수 있는 경우 날짜를 선택 하면 hello에서 hello 특정 복구 지점 선택 **시간** 드롭 다운 메뉴.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-144">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![볼륨 및 날짜](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="8e1fd-146">복구 지점 toorestore hello를 선택 하면 클릭 **탑재**합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-146">Once you have chosen hello recovery point toorestore, click **Mount**.</span></span>

    <span data-ttu-id="8e1fd-147">Azure 백업 탑재 hello 로컬 복구 지점으로 사용 하 여 복구 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-147">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="8e1fd-148">Hello에 **찾아보기 및 파일 복구** 창에서 클릭 **찾아보기** 원하는 tooopen Windows 탐색기 및 찾기 hello 파일 및 폴더.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-148">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![복구 옵션](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="8e1fd-150">Windows 탐색기, hello 파일 복사 및/또는 폴더에서 toorestore 원하고 tooany 위치 toohello 로컬 서버 또는 컴퓨터에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-150">In Windows Explorer, copy hello files and/or folders you want toorestore and paste them tooany location local toohello server or computer.</span></span> <span data-ttu-id="8e1fd-151">있습니다 수 또는 hello 복구 볼륨에서 직접 hello 파일 스트림 열고 hello 올바른 버전은 복구를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-151">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![복사 및 붙여넣기 toolocal 위치 탑재 된 볼륨에서에서 파일 및 폴더](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="8e1fd-153">끝나면 hello 파일 및/또는 폴더 hello에 복원 중인 **찾아보기 및 복구 파일** 창에서 클릭 **탑재 해제**합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-153">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="8e1fd-154">클릭 **예** tooconfirm toounmount hello 볼륨 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-154">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Hello 볼륨을 분리 하 고 확인](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="8e1fd-156">탑재 해제를 클릭 하지 않으면 경우 탑재 된 경우 hello 시간에서 6 시간 동안 hello 복구 볼륨 탑재 된 상태로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-156">If you do not click Unmount, hello Recovery Volume will remain mounted for six hours from hello time when it was mounted.</span></span> <span data-ttu-id="8e1fd-157">Hello 볼륨이 탑재 하는 동안 백업 작업이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-157">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="8e1fd-158">Hello 볼륨 탑재 되는 경우 hello 시간 동안 모든 예약 된 백업 작업 toorun hello 복구 볼륨 탑재 된 후 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-158">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="recover-data-toohello-same-machine"></a><span data-ttu-id="8e1fd-159">복구할 데이터 toohello 동일한 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="8e1fd-159">Recover data toohello same machine</span></span>
<span data-ttu-id="8e1fd-160">파일 및 희망 toorestore 실수로 삭제 한 경우이 단계를 같은 컴퓨터 (어떤 hello에서 백업을 수행할 때) 다음 hello toohello hello 데이터를 복구 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-160">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="8e1fd-161">열기 hello **Microsoft Azure 백업** 에 snap 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-161">Open hello **Microsoft Azure Backup** snap in.</span></span>
2. <span data-ttu-id="8e1fd-162">클릭 **데이터 복구** tooinitiate hello 워크플로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-162">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![데이터 복구](./media/backup-azure-restore-windows-server-classic/recover.png)
3. <span data-ttu-id="8e1fd-164">선택 hello  **이 서버 (*yourmachinename*) * * 옵션 toorestore hello 백업 된 파일 hello에 동일한 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-164">Select hello **This server (*yourmachinename*)** option toorestore hello backed up file on hello same machine.</span></span>

    ![동일한 컴퓨터](./media/backup-azure-restore-windows-server-classic/samemachine.png)
4. <span data-ttu-id="8e1fd-166">너무 선택**파일 찾아보기** 또는 **파일 검색**합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-166">Choose too**Browse for files** or **Search for files**.</span></span>

    <span data-ttu-id="8e1fd-167">하나 이상의 파일 경로가 있는 알려져 toorestore 하려는 경우 hello 기본 옵션을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-167">Leave hello default option if you plan toorestore one or more files whose path is known.</span></span> <span data-ttu-id="8e1fd-168">Hello 폴더 구조에 대 한 확실 하지 않은 하지만 파일에 대 한 toosearch 하려는 경우 선택 hello **파일 검색** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-168">If you are not sure about hello folder structure but would like toosearch for a file, pick hello **Search for files** option.</span></span> <span data-ttu-id="8e1fd-169">이 섹션의 hello 용도로 hello 기본 옵션으로 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-169">For hello purpose of this section, we will proceed with hello default option.</span></span>

    ![파일 찾아보기](./media/backup-azure-restore-windows-server-classic/browseandsearch.png)
5. <span data-ttu-id="8e1fd-171">Toorestore hello 파일 원하는 hello 볼륨을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-171">Select hello volume from which you wish toorestore hello file.</span></span>

    <span data-ttu-id="8e1fd-172">어떤 지점이라도 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-172">You can restore from any point in time.</span></span> <span data-ttu-id="8e1fd-173">에 표시 되는 날짜 **굵게** hello 달력 컨트롤에서의 복원 지점 hello 가용성을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-173">Dates which appear in **bold** in hello calendar control indicate hello availability of a restore point.</span></span> <span data-ttu-id="8e1fd-174">날짜를 선택 및 사항에 따라 백업 일정 (백업 작업의 성공 hello)를 선택할 수 있습니다는 지점 hello에서 시간에 **시간** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-174">Once a date is selected, based on your backup schedule (and hello success of a backup operation), you can select a point in time from hello **Time** drop down.</span></span>

    ![볼륨 및 날짜](./media/backup-azure-restore-windows-server-classic/volanddate.png)
6. <span data-ttu-id="8e1fd-176">Hello 항목 toorecover를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-176">Select hello items toorecover.</span></span> <span data-ttu-id="8e1fd-177">원하는 toorestore 폴더/파일 여러 개 선택 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-177">You can multi-select folders/files you wish toorestore.</span></span>

    ![파일 선택](./media/backup-azure-restore-windows-server-classic/selectfiles.png)
7. <span data-ttu-id="8e1fd-179">Hello 복구 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-179">Specify hello recovery parameters.</span></span>

    ![복구 옵션](./media/backup-azure-restore-windows-server-classic/recoveroptions.png)

   * <span data-ttu-id="8e1fd-181">(에 hello 파일/폴더를 덮어쓰게 될) toohello 원래 위치 또는 hello tooanother 위치를 복원 하는 옵션을 동일한 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-181">You have an option of restoring toohello original location (in which hello file/folder would be overwritten) or tooanother location in hello same machine.</span></span>
   * <span data-ttu-id="8e1fd-182">경우 hello 파일/폴더 toorestore hello 대상 위치에 있는 원하는 사본을 만들 수 있습니다 (두 가지 버전의 hello 같은 파일) hello 대상 위치에 hello 파일 덮어쓰거나 hello 대상에 존재 하는 hello 파일의 hello 복구를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-182">If hello file/folder you wish toorestore exists in hello target location, you can create copies (two versions of hello same file), overwrite hello files in hello target location, or skip hello recovery of hello files which exist in hello target.</span></span>
   * <span data-ttu-id="8e1fd-183">Hello Acl에 복구 되는지 hello 파일을 복원 하는 hello 기본 옵션을 그대로 두는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-183">It is highly recommended that you leave hello default option of restoring hello ACLs on hello files which are being recovered.</span></span>
8. <span data-ttu-id="8e1fd-184">이러한 입력을 제공하면 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-184">Once these inputs are provided, click **Next**.</span></span> <span data-ttu-id="8e1fd-185">hello 파일 toothis 컴퓨터 복원 되 면 hello 복구 워크플로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-185">hello recovery workflow, which restores hello files toothis machine, will begin.</span></span>

## <a name="recover-tooan-alternate-machine"></a><span data-ttu-id="8e1fd-186">Tooan 대체 컴퓨터 복구</span><span class="sxs-lookup"><span data-stu-id="8e1fd-186">Recover tooan alternate machine</span></span>
<span data-ttu-id="8e1fd-187">전체 서버를 잃어버린 경우 Azure 백업 tooa 서로 다른 컴퓨터에서 데이터를 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-187">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="8e1fd-188">단계를 수행 하는 hello hello 워크플로를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-188">hello following steps illustrate hello workflow.</span></span>  

<span data-ttu-id="8e1fd-189">다음이 단계에 사용 된 hello 용어에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-189">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="8e1fd-190">*원본 컴퓨터* – hello 원래 컴퓨터 hello 백업에서 백업 하 고 있는 현재 사용할 수 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-190">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="8e1fd-191">*대상 컴퓨터* – hello 컴퓨터 toowhich hello 데이터 복구 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-191">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="8e1fd-192">*샘플 자격 증명 모음* – hello 백업 자격 증명 모음 toowhich hello *원본 컴퓨터* 및 *대상 컴퓨터* 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-192">*Sample vault* – hello Backup vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="8e1fd-193">컴퓨터에서 만든 백업은 이전 버전의 hello 운영 체제를 실행 중인 컴퓨터에 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-193">Backups taken from a machine cannot be restored on a machine which is running an earlier version of hello operating system.</span></span> <span data-ttu-id="8e1fd-194">예를 들어 백업이 Windows 7 컴퓨터에서 수행된 경우 Windows 8 이상의 컴퓨터에서 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-194">For example, if backups are taken from a Windows 7 machine, it can be restored on a Windows 8 or above machine.</span></span> <span data-ttu-id="8e1fd-195">그러나 hello 반대로 true을 유지 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-195">However, hello vice-versa does not hold true.</span></span>
>
>

1. <span data-ttu-id="8e1fd-196">열기 hello **Microsoft Azure 백업** hello에 snap *대상 컴퓨터*합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-196">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>
2. <span data-ttu-id="8e1fd-197">해당 hello 확인 *대상 컴퓨터* 및 hello *원본 컴퓨터* 등록된 toohello는 동일한 백업 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-197">Ensure that hello *Target machine* and hello *Source machine* are registered toohello same backup vault.</span></span>
3. <span data-ttu-id="8e1fd-198">클릭 **데이터 복구** tooinitiate hello 워크플로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-198">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![데이터 복구](./media/backup-azure-restore-windows-server-classic/recover.png)
4. <span data-ttu-id="8e1fd-200">**다른 서버**</span><span class="sxs-lookup"><span data-stu-id="8e1fd-200">Select **Another server**</span></span>

    ![다른 서버](./media/backup-azure-restore-windows-server-classic/anotherserver.png)
5. <span data-ttu-id="8e1fd-202">Hello toohello 해당 하는 자격 증명 모음 자격 증명 파일을 제공 *샘플 자격 증명 모음*합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-202">Provide hello vault credential file that corresponds toohello *Sample vault*.</span></span> <span data-ttu-id="8e1fd-203">Hello 자격 증명 모음 자격 증명 파일이 잘못 되었거나 (만료 된) 경우 hello에서 새 자격 증명 모음 자격 증명 파일을 다운로드 *샘플 자격 증명 모음* hello Azure 클래식 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-203">If hello vault credential file is invalid (or expired) download a new vault credential file from hello *Sample vault* in hello Azure classic portal.</span></span> <span data-ttu-id="8e1fd-204">Hello 자격 증명 모음 자격 증명 파일 제공 되 면 hello 자격 증명 모음 자격 증명 파일에 대 한 백업 자격 증명 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-204">Once hello vault credential file is provided, hello backup vault against hello vault credential file is displayed.</span></span>
6. <span data-ttu-id="8e1fd-205">선택 hello *원본 컴퓨터* hello 목록이 표시 된 컴퓨터에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-205">Select hello *Source machine* from hello list of displayed machines.</span></span>

    ![컴퓨터 목록](./media/backup-azure-restore-windows-server-classic/machinelist.png)
7. <span data-ttu-id="8e1fd-207">어느 hello 선택 **파일 검색** 또는 **파일 찾아보기** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-207">Select either hello **Search for files** or **Browse for files** option.</span></span> <span data-ttu-id="8e1fd-208">이 섹션의 hello 용도로 hello를 사용 합니다 **파일 검색** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-208">For hello purpose of this section, we will use hello **Search for files** option.</span></span>

    ![검색](./media/backup-azure-restore-windows-server-classic/search.png)
8. <span data-ttu-id="8e1fd-210">Hello 다음 화면에서 hello 볼륨 및 날짜를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-210">Select hello volume and date in hello next screen.</span></span> <span data-ttu-id="8e1fd-211">검색 하려는 toorestore hello 폴더/파일 이름에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-211">Search for hello folder/file name you want toorestore.</span></span>

    ![검색 항목](./media/backup-azure-restore-windows-server-classic/searchitems.png)
9. <span data-ttu-id="8e1fd-213">Hello 위치 hello 파일이 toobe 복원 해야 하는 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-213">Select hello location where hello files need toobe restored.</span></span>

    ![복원 위치](./media/backup-azure-restore-windows-server-classic/restorelocation.png)
10. <span data-ttu-id="8e1fd-215">중에 제공 된 hello 암호화 암호를 제공 *원본 컴퓨터의* 등록 너무*샘플 자격 증명 모음*합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-215">Provide hello encryption passphrase that was provided during *Source machine’s* registration too*Sample vault*.</span></span>

    ![암호화](./media/backup-azure-restore-windows-server-classic/encryption.png)
11. <span data-ttu-id="8e1fd-217">Hello 입력 제공 되 면 클릭 **복구**이며 트리거 hello hello 제공 된 파일 toohello 대상을 백업 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-217">Once hello input is provided, click **Recover**, which triggers hello restore of hello backed up files toohello destination provided.</span></span>

## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a><span data-ttu-id="8e1fd-218">인스턴트 복원 toorestore 데이터 tooan 대체 컴퓨터 사용</span><span class="sxs-lookup"><span data-stu-id="8e1fd-218">Use Instant Restore toorestore data tooan alternate machine</span></span>
<span data-ttu-id="8e1fd-219">전체 서버를 잃어버린 경우 Azure 백업 tooa 서로 다른 컴퓨터에서 데이터를 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-219">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="8e1fd-220">단계를 수행 하는 hello hello 워크플로를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-220">hello following steps illustrate hello workflow.</span></span>

<span data-ttu-id="8e1fd-221">다음이 단계에 사용 된 hello 용어에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-221">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="8e1fd-222">*원본 컴퓨터* – hello 원래 컴퓨터 hello 백업에서 백업 하 고 있는 현재 사용할 수 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-222">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="8e1fd-223">*대상 컴퓨터* – hello 컴퓨터 toowhich hello 데이터 복구 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-223">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="8e1fd-224">*샘플 자격 증명 모음* – hello 복구 서비스 자격 증명 모음 toowhich hello *원본 컴퓨터* 및 *대상 컴퓨터* 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-224">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="8e1fd-225">백업을 이전 버전의 hello 운영 체제를 실행 하는 복원 된 tooa 대상 컴퓨터 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-225">Backups can't be restored tooa target machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="8e1fd-226">예를 들어, Windows 7 컴퓨터에서 가져온 백업은 Windows 8 이상의 컴퓨터에서 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-226">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="8e1fd-227">Windows 8 컴퓨터에서 수행한 백업 복원된 tooa Windows 7 컴퓨터 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-227">A backup taken from a Windows 8 computer cannot be restored tooa Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="8e1fd-228">열기 hello **Microsoft Azure 백업** hello에 snap *대상 컴퓨터*합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-228">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>

2. <span data-ttu-id="8e1fd-229">Hello 확인 *대상 컴퓨터* 및 hello *원본 컴퓨터* 동일한 복구 서비스 자격 증명 모음에 등록 된 toohello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-229">Ensure hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>

3. <span data-ttu-id="8e1fd-230">클릭 **데이터 복구** tooopen hello **데이터 복구 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-230">Click **Recover Data** tooopen hello **Recover Data wizard**.</span></span>

    ![데이터 복구](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="8e1fd-232">Hello에 **시작** 창 선택 **다른 서버**</span><span class="sxs-lookup"><span data-stu-id="8e1fd-232">On hello **Getting Started** pane, select **Another server**</span></span>

    ![다른 서버](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="8e1fd-234">Hello toohello 해당 하는 자격 증명 모음 자격 증명 파일을 제공 *샘플 자격 증명 모음*를 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-234">Provide hello vault credential file that corresponds toohello *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="8e1fd-235">Hello 자격 증명 모음 자격 증명 파일을 잘못 된 (또는 만료 된) 경우 hello에서 새 자격 증명 모음 자격 증명 파일을 다운로드 *샘플 자격 증명 모음* hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-235">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="8e1fd-236">올바른 자격 증명 모음 자격 증명을 제공한 경우 백업 자격 증명 모음에 해당 하는 hello hello 이름이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-236">Once you provide a valid vault credential, hello name of hello corresponding Backup Vault appears.</span></span>

6. <span data-ttu-id="8e1fd-237">Hello에 **백업 서버 선택** 창, 선택 hello *원본 컴퓨터* hello 목록이 표시 된 컴퓨터에서 및 hello 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-237">On hello **Select Backup Server** pane, select hello *Source machine* from hello list of displayed machines and provide hello passphrase.</span></span> <span data-ttu-id="8e1fd-238">그런 후 **Next**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-238">Then click **Next**.</span></span>

    ![컴퓨터 목록](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="8e1fd-240">Hello에 **복구 모드 선택** 창, 선택 **개별 파일과 폴더** 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-240">On hello **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![검색](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="8e1fd-242">Hello에 **볼륨 및 날짜 선택** 창, hello 파일 및/또는 toorestore 폴더를 포함 하는 select hello 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-242">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="8e1fd-243">Hello 달력에서 복구 지점을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-243">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="8e1fd-244">어떤 복구 시점에서라도 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-244">You can restore from any recovery point in time.</span></span> <span data-ttu-id="8e1fd-245">날짜 **굵게** 복구 지점이 하나 이상 hello 가용성을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-245">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="8e1fd-246">여러 복구 지점을 사용할 수 있는 경우 날짜를 선택 하면 hello에서 hello 특정 복구 지점 선택 **시간** 드롭 다운 메뉴.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-246">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![검색 항목](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="8e1fd-248">클릭 **탑재** toolocally 탑재 hello 복구 지점에서 복구 볼륨으로 프로그램 *대상 컴퓨터*합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-248">Click **Mount** toolocally mount hello recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="8e1fd-249">Hello에 **찾아보기 및 파일 복구** 창에서 클릭 **찾아보기** 원하는 tooopen Windows 탐색기 및 찾기 hello 파일 및 폴더.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-249">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![암호화](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="8e1fd-251">Windows 탐색기에서 hello 복구 볼륨에서 hello 파일 및/또는 폴더를 복사 하 고 tooyour 붙여넣을 *대상 컴퓨터* 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-251">In Windows Explorer, copy hello files and/or folders from hello recovery volume and paste them tooyour *Target machine* location.</span></span> <span data-ttu-id="8e1fd-252">있습니다 수 또는 hello 복구 볼륨에서 직접 hello 파일 스트림 열고 hello 올바른 버전은 복구를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-252">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![암호화](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="8e1fd-254">끝나면 hello 파일 및/또는 폴더 hello에 복원 중인 **찾아보기 및 복구 파일** 창에서 클릭 **탑재 해제**합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-254">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="8e1fd-255">클릭 **예** tooconfirm toounmount hello 볼륨 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-255">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![암호화](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="8e1fd-257">탑재 해제를 클릭 하지 않으면 경우 탑재 된 경우 hello 시간에서 6 시간 동안 hello 복구 볼륨 탑재 된 상태로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-257">If you do not click Unmount, hello Recovery Volume will remain mounted for six hours from hello time when it was mounted.</span></span> <span data-ttu-id="8e1fd-258">Hello 볼륨이 탑재 하는 동안 백업 작업이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-258">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="8e1fd-259">Hello 볼륨 탑재 되는 경우 hello 시간 동안 모든 예약 된 백업 작업 toorun hello 복구 볼륨 탑재 된 후 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-259">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="next-steps"></a><span data-ttu-id="8e1fd-260">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8e1fd-260">Next steps</span></span>
* [<span data-ttu-id="8e1fd-261">Azure 백업 - FAQ</span><span class="sxs-lookup"><span data-stu-id="8e1fd-261">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
* <span data-ttu-id="8e1fd-262">Hello 방문 [Azure 백업 포럼](http://go.microsoft.com/fwlink/p/?LinkId=290933)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-262">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span></span>

## <a name="learn-more"></a><span data-ttu-id="8e1fd-263">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="8e1fd-263">Learn more</span></span>
* [<span data-ttu-id="8e1fd-264">Azure 백업 개요</span><span class="sxs-lookup"><span data-stu-id="8e1fd-264">Azure Backup Overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=222425)
* [<span data-ttu-id="8e1fd-265">Azure 가상 컴퓨터 백업</span><span class="sxs-lookup"><span data-stu-id="8e1fd-265">Backup Azure virtual machines</span></span>](backup-azure-vms-introduction.md)
* [<span data-ttu-id="8e1fd-266">Microsoft 워크로드 백업</span><span class="sxs-lookup"><span data-stu-id="8e1fd-266">Backup up Microsoft workloads</span></span>](backup-azure-dpm-introduction.md)
