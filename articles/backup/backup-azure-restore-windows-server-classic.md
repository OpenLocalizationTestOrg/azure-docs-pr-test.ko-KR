---
title: "클래식 배포 모델을 사용하여 Azure에서 Windows 서버 또는 Windows 클라이언트로 데이터 복원 | Microsoft Docs"
description: "Windows 서버 또는 Windows 클라이언트에서 복원하는 방법을 알아보세요."
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
ms.openlocfilehash: 300b2b17b44e21ed446fd63d572a2461e2fc1343
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="restore-files-to-a-windows-server-or-windows-client-machine-using-the-classic-deployment-model"></a><span data-ttu-id="b08f8-103">클래식 배포 모델을 사용하여 Windows 서버 또는 Windows 클라이언트 컴퓨터로 파일 복원</span><span class="sxs-lookup"><span data-stu-id="b08f8-103">Restore files to a Windows server or Windows client machine using the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b08f8-104">클래식 포털</span><span class="sxs-lookup"><span data-stu-id="b08f8-104">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
> * [<span data-ttu-id="b08f8-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="b08f8-105">Azure portal</span></span>](backup-azure-restore-windows-server.md)
>
>

<span data-ttu-id="b08f8-106">이 문서에서는 백업 자격 증명 모음에서 데이터를 복구하고 서버 또는 컴퓨터로 복원하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-106">This article explains how to recover data from a backup vault and restore it to a server or computer.</span></span> <span data-ttu-id="b08f8-107">2017년 3월부터는 클래식 포털에서 더 이상 백업 자격 증명 모음을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-107">Starting in March 2017, you can no longer create backup vaults in the classic portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b08f8-108">이제 Backup 자격 증명 모음을 Recovery Services 자격 증명 모음으로 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-108">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="b08f8-109">자세한 내용은 [Recovery Services 자격 증명 모음으로 Backup 자격 증명 모음 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b08f8-109">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="b08f8-110">Backup 자격 증명 모음을 Recovery Services 자격 증명 모음으로 업그레이드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-110">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="b08f8-111">**2017년 10월 15일**부터는 PowerShell을 사용하여 Backup 자격 증명 모음을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-111">**October 15, 2017**, you will no longer be able to use PowerShell to create Backup vaults.</span></span> <br/> <span data-ttu-id="b08f8-112">**2017년 11월 1일 시작**:</span><span class="sxs-lookup"><span data-stu-id="b08f8-112">**Starting November 1, 2017**:</span></span>
>- <span data-ttu-id="b08f8-113">나머지 모든 Backup 자격 증명 모음은 자동으로 Recovery Services 자격 증명 모음으로 업그레이드됩니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-113">Any remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="b08f8-114">클래식 포털에서는 백업 데이터에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-114">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="b08f8-115">대신 Azure Portal을 사용하여 Recovery Services 자격 증명 모음에서 백업 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-115">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

<span data-ttu-id="b08f8-116">데이터를 복원하려면 MARS(Microsoft Azure Recovery Services) 에이전트에서 데이터 복구 마법사를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-116">To restore data, you use the Recover Data wizard in the Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="b08f8-117">데이터를 복원하면 다음이 가능해집니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-117">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="b08f8-118">백업을 수행한 동일한 컴퓨터에 데이터를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-118">Restore data to the same machine from which the backups were taken.</span></span>
* <span data-ttu-id="b08f8-119">다른 컴퓨터에 데이터를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-119">Restore data to an alternate machine.</span></span>

<span data-ttu-id="b08f8-120">2017년 1월 Microsoft는 MARS 에이전트에 대한 미리 보기 업데이트를 릴리스했습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-120">In January 2017, Microsoft released a Preview update to the MARS agent.</span></span> <span data-ttu-id="b08f8-121">버그 수정과 함께 이번 업데이트는 쓰기 가능한 복구 지점 스냅숏을 복구 볼륨으로 탑재할 수 있도록 해주는 즉시 복원을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-121">Along with bug fixes, this update enables Instant Restore, which allows you to mount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="b08f8-122">그런 다음 복구 볼륨을 탐색하고 파일을 로컬 컴퓨터에 복사하여 파일을 선택적으로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-122">You can then explore the recovery volume and copy files to a local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="b08f8-123">즉시 복원을 사용하여 데이터를 복원하려면 [2017년 1월 Azure Backup 업데이트](https://support.microsoft.com/en-us/help/3216528?preview)가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-123">The [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want to use Instant Restore to restore data.</span></span> <span data-ttu-id="b08f8-124">또한 백업 데이터는 지원 문서에 나열된 로캘의 자격 증명 모음에서 보호되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-124">Also the backup data must be protected in vaults in locales listed in the support article.</span></span> <span data-ttu-id="b08f8-125">즉시 복원을 지원하는 최신 로캘 목록은 [2017년 1월 Azure Backup 업데이트](https://support.microsoft.com/en-us/help/3216528?preview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b08f8-125">Consult the [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for the latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="b08f8-126">즉시 복원은 현재 **일부** 로캘에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-126">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="b08f8-127">즉시 복원은 Azure Portal의 Recovery Services 자격 증명 모음에서 그리고 클래식 포털의 Backup 자격 증명 모음에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-127">Instant Restore is available for use in Recovery Services vaults in the Azure portal and Backup vaults in the classic portal.</span></span> <span data-ttu-id="b08f8-128">즉시 복원을 사용하려면 MARS 업데이트를 다운로드하고 즉시 복원을 언급하는 절차를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="b08f8-128">If you want to use Instant Restore, download the MARS update, and follow the procedures that mention Instant Restore.</span></span>


## <a name="use-instant-restore-to-recover-data-to-the-same-machine"></a><span data-ttu-id="b08f8-129">즉시 복원을 사용하여 데이터를 동일한 컴퓨터로 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-129">Use Instant Restore to recover data to the same machine</span></span>

<span data-ttu-id="b08f8-130">파일을 실수로 삭제했는데 (백업이 수행된) 동일한 컴퓨터에서 복원하려는 경우 다음 단계를 사용하면 데이터를 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-130">If you accidentally deleted a file and wish to restore it to the same machine (from which the backup is taken), the following steps will help you recover the data.</span></span>

1. <span data-ttu-id="b08f8-131">**Microsoft Azure 백업** 스냅인을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-131">Open the **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="b08f8-132">스냅인이 설치된 위치를 모르는 경우 컴퓨터 또는 서버에서 **Microsoft Azure Backup**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-132">If you don't know where the snap in was installed, search the computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="b08f8-133">데스크톱 앱이 검색 결과에 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-133">The desktop app should appear in the search results.</span></span>

2. <span data-ttu-id="b08f8-134">마법사를 시작하려면 **데이터 복구**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-134">Click **Recover Data** to start the wizard.</span></span>

    ![데이터 복구](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="b08f8-136">**시작** 창에서 동일한 서버 또는 컴퓨터로 데이터를 복원하려면 **이 서버(`<server name>`)**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-136">On the **Getting Started** pane, to restore the data to the same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![같은 컴퓨터에 데이터를 복원하려면 이 서버 옵션을 선택합니다.](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="b08f8-138">**복구 모드 선택** 창에서 **개별 파일 및 폴더**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-138">On the **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![파일 찾아보기](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="b08f8-140">**볼륨 및 날짜 선택** 창에서 복원할 파일 및/또는 폴더가 들어있는 볼륨을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-140">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="b08f8-141">달력에서 복구 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-141">On the calendar, select a recovery point.</span></span> <span data-ttu-id="b08f8-142">어떤 복구 시점에서라도 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-142">You can restore from any recovery point in time.</span></span> <span data-ttu-id="b08f8-143">**굵게** 표시된 날짜는 하나 이상의 복구 지점을 사용 가능함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-143">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="b08f8-144">날짜를 선택하고 여러 복구 지점을 사용할 수 있는 경우 **시간** 드롭다운 메뉴에서 특정 복구 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-144">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![볼륨 및 날짜](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="b08f8-146">복원할 복구 지점을 선택했으면 **탑재**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-146">Once you have chosen the recovery point to restore, click **Mount**.</span></span>

    <span data-ttu-id="b08f8-147">Azure Backup은 로컬 복구 지점을 마운트하고 이를 복구 볼륨으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-147">Azure Backup mounts the local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="b08f8-148">**파일 찾아보기 및 복구** 창에서 **찾아보기**를 클릭하여 Windows 탐색기를 열고 원하는 파일 및 폴더를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-148">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![복구 옵션](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="b08f8-150">Windows 탐색기에서 복원할 파일 및/또는 폴더를 복사하여 서버 또는 컴퓨터의 로컬 위치에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-150">In Windows Explorer, copy the files and/or folders you want to restore and paste them to any location local to the server or computer.</span></span> <span data-ttu-id="b08f8-151">복구 볼륨에서 직접 파일을 열거나 스트리밍하여 올바른 버전이 복구되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-151">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![탑재된 볼륨의 파일 및 폴더를 복사하여 로컬 위치에 붙여 넣기](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="b08f8-153">파일 및/또는 폴더 복원이 완료되면 **찾아보기 및 복구 파일** 창에서 **마운트 해제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-153">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="b08f8-154">그런 다음 **예**를 클릭하여 볼륨 마운트 해제를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-154">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![볼륨을 마운트 해제하고 확인](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="b08f8-156">마운트 해제를 클릭하지 않으면 복구 볼륨이 마운트된 후 6시간 동안 마운트된 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-156">If you do not click Unmount, the Recovery Volume will remain mounted for six hours from the time when it was mounted.</span></span> <span data-ttu-id="b08f8-157">볼륨이 마운트되는 동안 백업 작업은 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-157">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="b08f8-158">볼륨이 마운트된 시간 동안 실행되도록 스케줄된 모든 백업 작업은 복구 볼륨이 마운트 해제된 후에 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-158">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >


## <a name="recover-data-to-the-same-machine"></a><span data-ttu-id="b08f8-159">동일한 컴퓨터로 데이터 복구</span><span class="sxs-lookup"><span data-stu-id="b08f8-159">Recover data to the same machine</span></span>
<span data-ttu-id="b08f8-160">파일을 실수로 삭제했는데 (백업이 수행된) 동일한 컴퓨터에서 복원하려는 경우 다음 단계를 사용하면 데이터를 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-160">If you accidentally deleted a file and wish to restore it to the same machine (from which the backup is taken), the following steps will help you recover the data.</span></span>

1. <span data-ttu-id="b08f8-161">**Microsoft Azure 백업** 스냅인을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-161">Open the **Microsoft Azure Backup** snap in.</span></span>
2. <span data-ttu-id="b08f8-162">**데이터 복구** 를 클릭하여 워크플로를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-162">Click **Recover Data** to initiate the workflow.</span></span>

    ![데이터 복구](./media/backup-azure-restore-windows-server-classic/recover.png)
3. <span data-ttu-id="b08f8-164">동일한 컴퓨터에 백업된 파일을 복원하려면 **이 서버(*yourmachinename*)** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-164">Select the **This server (*yourmachinename*)** option to restore the backed up file on the same machine.</span></span>

    ![동일한 컴퓨터](./media/backup-azure-restore-windows-server-classic/samemachine.png)
4. <span data-ttu-id="b08f8-166">**파일 찾아보기** 또는 **파일 검색**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-166">Choose to **Browse for files** or **Search for files**.</span></span>

    <span data-ttu-id="b08f8-167">경로가 알려져 있는 하나 이상의 파일을 복원하려는 경우 기본 옵션을 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-167">Leave the default option if you plan to restore one or more files whose path is known.</span></span> <span data-ttu-id="b08f8-168">폴더 구조를 잘 모르지만 파일을 검색하려는 경우 **파일 검색** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-168">If you are not sure about the folder structure but would like to search for a file, pick the **Search for files** option.</span></span> <span data-ttu-id="b08f8-169">이 섹션에서는 기본 옵션을 사용하여 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-169">For the purpose of this section, we will proceed with the default option.</span></span>

    ![파일 찾아보기](./media/backup-azure-restore-windows-server-classic/browseandsearch.png)
5. <span data-ttu-id="b08f8-171">다음 화면에서는 파일을 복원하려는 볼륨을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-171">Select the volume from which you wish to restore the file.</span></span>

    <span data-ttu-id="b08f8-172">어떤 지점이라도 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-172">You can restore from any point in time.</span></span> <span data-ttu-id="b08f8-173">달력 컨트롤에 **굵게** 표시되는 날짜는 복원 지점이 사용 가능함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-173">Dates which appear in **bold** in the calendar control indicate the availability of a restore point.</span></span> <span data-ttu-id="b08f8-174">날짜가 선택되면 백업 일정(및 백업 작업의 성공 여부)에 따라 **시간** 드롭다운에서 특정 시점을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-174">Once a date is selected, based on your backup schedule (and the success of a backup operation), you can select a point in time from the **Time** drop down.</span></span>

    ![볼륨 및 날짜](./media/backup-azure-restore-windows-server-classic/volanddate.png)
6. <span data-ttu-id="b08f8-176">복구할 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-176">Select the items to recover.</span></span> <span data-ttu-id="b08f8-177">복원하려는 폴더/파일을 다중 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-177">You can multi-select folders/files you wish to restore.</span></span>

    ![파일 선택](./media/backup-azure-restore-windows-server-classic/selectfiles.png)
7. <span data-ttu-id="b08f8-179">복구 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-179">Specify the recovery parameters.</span></span>

    ![복구 옵션](./media/backup-azure-restore-windows-server-classic/recoveroptions.png)

   * <span data-ttu-id="b08f8-181">원래 위치로 복원(파일/폴더가 덮어써짐) 또는 동일한 컴퓨터의 다른 위치로 복원하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-181">You have an option of restoring to the original location (in which the file/folder would be overwritten) or to another location in the same machine.</span></span>
   * <span data-ttu-id="b08f8-182">복원하려는 파일/폴더가 대상 위치에 있는 경우 복사본 만들기(동일한 파일의 두 버전) 또는 대상 위치의 파일 덮어쓰기 또는 대상에 있는 파일의 복구 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-182">If the file/folder you wish to restore exists in the target location, you can create copies (two versions of the same file), overwrite the files in the target location, or skip the recovery of the files which exist in the target.</span></span>
   * <span data-ttu-id="b08f8-183">복구할 파일의 ACL을 복원하는 기본 옵션을 그대로 두는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-183">It is highly recommended that you leave the default option of restoring the ACLs on the files which are being recovered.</span></span>
8. <span data-ttu-id="b08f8-184">이러한 입력을 제공하면 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-184">Once these inputs are provided, click **Next**.</span></span> <span data-ttu-id="b08f8-185">이 컴퓨터에 파일을 복원하는 복구 워크플로를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-185">The recovery workflow, which restores the files to this machine, will begin.</span></span>

## <a name="recover-to-an-alternate-machine"></a><span data-ttu-id="b08f8-186">다른 컴퓨터로 복구</span><span class="sxs-lookup"><span data-stu-id="b08f8-186">Recover to an alternate machine</span></span>
<span data-ttu-id="b08f8-187">전체 서버가 손실된 경우에도 Azure 백업에서 데이터를 다른 컴퓨터에 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-187">If your entire server is lost, you can still recover data from Azure Backup to a different machine.</span></span> <span data-ttu-id="b08f8-188">다음 단계는 워크플로를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-188">The following steps illustrate the workflow.</span></span>  

<span data-ttu-id="b08f8-189">다음 단계에서 사용되는 용어는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-189">The terminology used in these steps includes:</span></span>

* <span data-ttu-id="b08f8-190">*원본 컴퓨터* – 처음에 백업이 수행되었고 현재는 사용할 수 없는 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-190">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="b08f8-191">*대상 컴퓨터* – 데이터가 복구되는 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-191">*Target machine* – The machine to which the data is being recovered.</span></span>
* <span data-ttu-id="b08f8-192">*샘플 자격 증명 모음* – *원본 컴퓨터* 및 *대상 컴퓨터*가 등록된 백업 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-192">*Sample vault* – The Backup vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="b08f8-193">이전 버전의 운영 체제를 실행 중인 컴퓨터에는 컴퓨터에서 수행된 백업을 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-193">Backups taken from a machine cannot be restored on a machine which is running an earlier version of the operating system.</span></span> <span data-ttu-id="b08f8-194">예를 들어 백업이 Windows 7 컴퓨터에서 수행된 경우 Windows 8 이상의 컴퓨터에서 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-194">For example, if backups are taken from a Windows 7 machine, it can be restored on a Windows 8 or above machine.</span></span> <span data-ttu-id="b08f8-195">그러나 그 반대의 경우는 그렇지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-195">However, the vice-versa does not hold true.</span></span>
>
>

1. <span data-ttu-id="b08f8-196">**대상 컴퓨터** 에서 *Microsoft Azure 백업*스냅인을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-196">Open the **Microsoft Azure Backup** snap in on the *Target machine*.</span></span>
2. <span data-ttu-id="b08f8-197">*대상 컴퓨터* 및 *원본 컴퓨터*가 동일한 백업 자격 증명 모음에 등록됐는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-197">Ensure that the *Target machine* and the *Source machine* are registered to the same backup vault.</span></span>
3. <span data-ttu-id="b08f8-198">**데이터 복구** 를 클릭하여 워크플로를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-198">Click **Recover Data** to initiate the workflow.</span></span>

    ![데이터 복구](./media/backup-azure-restore-windows-server-classic/recover.png)
4. <span data-ttu-id="b08f8-200">**다른 서버**</span><span class="sxs-lookup"><span data-stu-id="b08f8-200">Select **Another server**</span></span>

    ![다른 서버](./media/backup-azure-restore-windows-server-classic/anotherserver.png)
5. <span data-ttu-id="b08f8-202">*샘플 자격 증명 모음*에 해당하는 자격 증명 모음 파일을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-202">Provide the vault credential file that corresponds to the *Sample vault*.</span></span> <span data-ttu-id="b08f8-203">자격 증명 모음 파일이 잘못되었거나 만료된 경우 Azure 클래식 포털의 *샘플 자격 증명 모음* 에서 새 자격 증명 모음 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-203">If the vault credential file is invalid (or expired) download a new vault credential file from the *Sample vault* in the Azure classic portal.</span></span> <span data-ttu-id="b08f8-204">자격 증명 모음 파일이 제공되면 자격 증명 모음 파일에 대한 백업 자격 증명 모음이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-204">Once the vault credential file is provided, the backup vault against the vault credential file is displayed.</span></span>
6. <span data-ttu-id="b08f8-205">표시된 컴퓨터 목록에서 *원본 컴퓨터* 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-205">Select the *Source machine* from the list of displayed machines.</span></span>

    ![컴퓨터 목록](./media/backup-azure-restore-windows-server-classic/machinelist.png)
7. <span data-ttu-id="b08f8-207">**파일 검색** 또는 **파일 찾아보기** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-207">Select either the **Search for files** or **Browse for files** option.</span></span> <span data-ttu-id="b08f8-208">이 섹션에서는 **파일 검색** 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-208">For the purpose of this section, we will use the **Search for files** option.</span></span>

    ![이를 통해 검색](./media/backup-azure-restore-windows-server-classic/search.png)
8. <span data-ttu-id="b08f8-210">다음 화면에서는 날짜와 볼륨을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-210">Select the volume and date in the next screen.</span></span> <span data-ttu-id="b08f8-211">복원하려는 폴더/파일 이름을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-211">Search for the folder/file name you want to restore.</span></span>

    ![검색 항목](./media/backup-azure-restore-windows-server-classic/searchitems.png)
9. <span data-ttu-id="b08f8-213">파일을 복원해야 하는 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-213">Select the location where the files need to be restored.</span></span>

    ![복원 위치](./media/backup-azure-restore-windows-server-classic/restorelocation.png)
10. <span data-ttu-id="b08f8-215">*원본 컴퓨터*를 *샘플 자격 증명 모음*으로 등록할 때 제공한 암호화의 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-215">Provide the encryption passphrase that was provided during *Source machine’s* registration to *Sample vault*.</span></span>

    ![암호화](./media/backup-azure-restore-windows-server-classic/encryption.png)
11. <span data-ttu-id="b08f8-217">입력을 제공하면 제공된 대상에 백업된 파일을 복원하는 작업을 트리거하는 **복구**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-217">Once the input is provided, click **Recover**, which triggers the restore of the backed up files to the destination provided.</span></span>

## <a name="use-instant-restore-to-restore-data-to-an-alternate-machine"></a><span data-ttu-id="b08f8-218">즉시 복원을 사용하여 데이터를 대체 컴퓨터에 복원</span><span class="sxs-lookup"><span data-stu-id="b08f8-218">Use Instant Restore to restore data to an alternate machine</span></span>
<span data-ttu-id="b08f8-219">전체 서버가 손실된 경우에도 Azure 백업에서 데이터를 다른 컴퓨터에 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-219">If your entire server is lost, you can still recover data from Azure Backup to a different machine.</span></span> <span data-ttu-id="b08f8-220">다음 단계는 워크플로를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-220">The following steps illustrate the workflow.</span></span>

<span data-ttu-id="b08f8-221">다음 단계에서 사용되는 용어는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-221">The terminology used in these steps includes:</span></span>

* <span data-ttu-id="b08f8-222">*원본 컴퓨터* – 처음에 백업이 수행되었고 현재는 사용할 수 없는 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-222">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="b08f8-223">*대상 컴퓨터* – 데이터가 복구되는 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-223">*Target machine* – The machine to which the data is being recovered.</span></span>
* <span data-ttu-id="b08f8-224">*샘플 자격 증명 모음* – *원본 컴퓨터* 및 *대상 컴퓨터*가 등록된 복구 서비스 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-224">*Sample vault* – The Recovery Services vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="b08f8-225">이전 버전의 운영 체제를 실행하는 대상 시스템으로 백업을 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-225">Backups can't be restored to a target machine running an earlier version of the operating system.</span></span> <span data-ttu-id="b08f8-226">예를 들어, Windows 7 컴퓨터에서 가져온 백업은 Windows 8 이상의 컴퓨터에서 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-226">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="b08f8-227">Windows 8 컴퓨터에서 가져온 백업은 Windows 7 컴퓨터로 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-227">A backup taken from a Windows 8 computer cannot be restored to a Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="b08f8-228">**대상 컴퓨터** 에서 *Microsoft Azure 백업*스냅인을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-228">Open the **Microsoft Azure Backup** snap in on the *Target machine*.</span></span>

2. <span data-ttu-id="b08f8-229">*대상 컴퓨터* 및 *원본 컴퓨터*가 동일한 Recovery Services 자격 증명 모음에 등록됐는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-229">Ensure the *Target machine* and the *Source machine* are registered to the same Recovery Services vault.</span></span>

3. <span data-ttu-id="b08f8-230">**데이터 복구**를 클릭하여 **데이터 복구 마법사**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-230">Click **Recover Data** to open the **Recover Data wizard**.</span></span>

    ![데이터 복구](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="b08f8-232">**시작** 창에서 **다른 서버**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-232">On the **Getting Started** pane, select **Another server**</span></span>

    ![다른 서버](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="b08f8-234">*샘플 자격 증명 모음*에 해당하는 자격 증명 모음 파일을 제공하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-234">Provide the vault credential file that corresponds to the *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="b08f8-235">자격 증명 모음 파일이 유효하지 않거나 만료된 경우 Azure Portal의 *샘플 자격 증명 모음* 에서 새 자격 증명 모음 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-235">If the vault credential file is invalid (or expired), download a new vault credential file from the *Sample vault* in the Azure portal.</span></span> <span data-ttu-id="b08f8-236">유효한 자격 증명 모음을 제공하면 해당 백업 자격 증명 모음의 이름이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-236">Once you provide a valid vault credential, the name of the corresponding Backup Vault appears.</span></span>

6. <span data-ttu-id="b08f8-237">**백업 서버 선택** 창에서 표시된 컴퓨터 목록에서 *원본 컴퓨터*를 선택하고 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-237">On the **Select Backup Server** pane, select the *Source machine* from the list of displayed machines and provide the passphrase.</span></span> <span data-ttu-id="b08f8-238">그런 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-238">Then click **Next**.</span></span>

    ![컴퓨터 목록](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="b08f8-240">**복구 모드 선택** 창에서 **개별 파일 및 폴더**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-240">On the **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Search](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="b08f8-242">**볼륨 및 날짜 선택** 창에서 복원할 파일 및/또는 폴더가 들어있는 볼륨을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-242">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="b08f8-243">달력에서 복구 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-243">On the calendar, select a recovery point.</span></span> <span data-ttu-id="b08f8-244">어떤 복구 시점에서라도 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-244">You can restore from any recovery point in time.</span></span> <span data-ttu-id="b08f8-245">**굵게** 표시된 날짜는 하나 이상의 복구 지점을 사용 가능함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-245">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="b08f8-246">날짜를 선택하고 여러 복구 지점을 사용할 수 있는 경우 **시간** 드롭다운 메뉴에서 특정 복구 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-246">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![검색 항목](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="b08f8-248">복구 지점을 *대상 컴퓨터*에 복구 볼륨으로 로컬로 마운트하려면 **탑재**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-248">Click **Mount** to locally mount the recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="b08f8-249">**파일 찾아보기 및 복구** 창에서 **찾아보기**를 클릭하여 Windows 탐색기를 열고 원하는 파일 및 폴더를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-249">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![암호화](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="b08f8-251">Windows 탐색기에서 복구 볼륨의 파일 및/또는 폴더를 복사하여 *대상 컴퓨터* 위치에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-251">In Windows Explorer, copy the files and/or folders from the recovery volume and paste them to your *Target machine* location.</span></span> <span data-ttu-id="b08f8-252">복구 볼륨에서 직접 파일을 열거나 스트리밍하여 올바른 버전이 복구되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-252">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![암호화](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="b08f8-254">파일 및/또는 폴더 복원이 완료되면 **찾아보기 및 복구 파일** 창에서 **마운트 해제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-254">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="b08f8-255">그런 다음 **예**를 클릭하여 볼륨 마운트 해제를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-255">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![암호화](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="b08f8-257">마운트 해제를 클릭하지 않으면 복구 볼륨이 마운트된 후 6시간 동안 마운트된 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-257">If you do not click Unmount, the Recovery Volume will remain mounted for six hours from the time when it was mounted.</span></span> <span data-ttu-id="b08f8-258">볼륨이 마운트되는 동안 백업 작업은 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-258">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="b08f8-259">볼륨이 마운트된 시간 동안 실행되도록 스케줄된 모든 백업 작업은 복구 볼륨이 마운트 해제된 후에 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b08f8-259">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >


## <a name="next-steps"></a><span data-ttu-id="b08f8-260">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b08f8-260">Next steps</span></span>
* [<span data-ttu-id="b08f8-261">Azure 백업 - FAQ</span><span class="sxs-lookup"><span data-stu-id="b08f8-261">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
* <span data-ttu-id="b08f8-262">[Azure 백업 포럼](http://go.microsoft.com/fwlink/p/?LinkId=290933)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="b08f8-262">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span></span>

## <a name="learn-more"></a><span data-ttu-id="b08f8-263">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="b08f8-263">Learn more</span></span>
* [<span data-ttu-id="b08f8-264">Azure 백업 개요</span><span class="sxs-lookup"><span data-stu-id="b08f8-264">Azure Backup Overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=222425)
* [<span data-ttu-id="b08f8-265">Azure 가상 컴퓨터 백업</span><span class="sxs-lookup"><span data-stu-id="b08f8-265">Backup Azure virtual machines</span></span>](backup-azure-vms-introduction.md)
* [<span data-ttu-id="b08f8-266">Microsoft 워크로드 백업</span><span class="sxs-lookup"><span data-stu-id="b08f8-266">Backup up Microsoft workloads</span></span>](backup-azure-dpm-introduction.md)
