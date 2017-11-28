---
title: "Azure에서 Windows Server 또는 Windows 컴퓨터로 데이터 복원 | Microsoft Docs"
description: "Azure에 저장된 데이터를 Windows Server 또는 Windows 컴퓨터로 복원하는 방법에 대해 알아봅니다."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 742f4b9e-c0ab-4eeb-8e22-ee29b83c22c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/16/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 231dd61f95267b3a504ed70e9b3a5abc470b69b2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="restore-files-to-a-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a><span data-ttu-id="1c50b-103">Resource Manager 배포 모델을 사용하여 Windows 서버 또는 Windows 클라이언트 컴퓨터로 파일 복원</span><span class="sxs-lookup"><span data-stu-id="1c50b-103">Restore files to a Windows server or Windows client machine using Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1c50b-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="1c50b-104">Azure portal</span></span>](backup-azure-restore-windows-server.md)
> * [<span data-ttu-id="1c50b-105">클래식 포털</span><span class="sxs-lookup"><span data-stu-id="1c50b-105">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
>
>

<span data-ttu-id="1c50b-106">이 문서에서는 백업 자격 증명 모음을 복원하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-106">This article explains how to restore data from a backup vault.</span></span> <span data-ttu-id="1c50b-107">데이터를 복원하려면 MARS(Microsoft Azure Recovery Services) 에이전트에서 데이터 복구 마법사를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-107">To restore data, you use the Recover Data wizard in the Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="1c50b-108">데이터를 복원하면 다음이 가능해집니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-108">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="1c50b-109">백업을 수행한 동일한 컴퓨터에 데이터를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-109">Restore data to the same machine from which the backups were taken.</span></span>
* <span data-ttu-id="1c50b-110">다른 컴퓨터에 데이터를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-110">Restore data to an alternate machine.</span></span>

<span data-ttu-id="1c50b-111">2017년 1월 Microsoft는 MARS 에이전트에 대한 미리 보기 업데이트를 릴리스했습니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-111">In January 2017, Microsoft released a Preview update to the MARS agent.</span></span> <span data-ttu-id="1c50b-112">버그 수정과 함께 이번 업데이트는 쓰기 가능한 복구 지점 스냅숏을 복구 볼륨으로 탑재할 수 있도록 해주는 즉시 복원을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-112">Along with bug fixes, this update enables Instant Restore, which allows you to mount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="1c50b-113">그런 다음 복구 볼륨을 탐색하고 파일을 로컬 컴퓨터에 복사하여 파일을 선택적으로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-113">You can then explore the recovery volume and copy files to a local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="1c50b-114">즉시 복원을 사용하여 데이터를 복원하려면 [2017년 1월 Azure Backup 업데이트](https://support.microsoft.com/en-us/help/3216528?preview)가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-114">The [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want to use Instant Restore to restore data.</span></span> <span data-ttu-id="1c50b-115">또한 백업 데이터는 지원 문서에 나열된 로캘의 자격 증명 모음에서 보호되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-115">Also the backup data must be protected in vaults in locales listed in the support article.</span></span> <span data-ttu-id="1c50b-116">즉시 복원을 지원하는 최신 로캘 목록은 [2017년 1월 Azure Backup 업데이트](https://support.microsoft.com/en-us/help/3216528?preview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c50b-116">Consult the [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for the latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="1c50b-117">즉시 복원은 현재 **일부** 로캘에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-117">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="1c50b-118">즉시 복원은 Azure Portal의 Recovery Services 자격 증명 모음에서 그리고 클래식 포털의 Backup 자격 증명 모음에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-118">Instant Restore is available for use in Recovery Services vaults in the Azure portal and Backup vaults in the classic portal.</span></span> <span data-ttu-id="1c50b-119">즉시 복원을 사용하려면 MARS 업데이트를 다운로드하고 즉시 복원을 언급하는 절차를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="1c50b-119">If you want to use Instant Restore, download the MARS update, and follow the procedures that mention Instant Restore.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="use-instant-restore-to-recover-data-to-the-same-machine"></a><span data-ttu-id="1c50b-120">즉시 복원을 사용하여 데이터를 동일한 컴퓨터로 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-120">Use Instant Restore to recover data to the same machine</span></span>

<span data-ttu-id="1c50b-121">파일을 실수로 삭제했는데 (백업이 수행된) 동일한 컴퓨터에서 복원하려는 경우 다음 단계를 사용하면 데이터를 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-121">If you accidentally deleted a file and wish to restore it to the same machine (from which the backup is taken), the following steps will help you recover the data.</span></span>

1. <span data-ttu-id="1c50b-122">**Microsoft Azure 백업** 스냅인을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-122">Open the **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="1c50b-123">스냅인이 설치된 위치를 모르는 경우 컴퓨터 또는 서버에서 **Microsoft Azure Backup**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-123">If you don't know where the snap in was installed, search the computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="1c50b-124">데스크톱 앱이 검색 결과에 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-124">The desktop app should appear in the search results.</span></span>

2. <span data-ttu-id="1c50b-125">마법사를 시작하려면 **데이터 복구**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-125">Click **Recover Data** to start the wizard.</span></span>

    ![데이터 복구](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="1c50b-127">**시작** 창에서 동일한 서버 또는 컴퓨터로 데이터를 복원하려면 **이 서버(`<server name>`)**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-127">On the **Getting Started** pane, to restore the data to the same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![같은 컴퓨터에 데이터를 복원하려면 이 서버 옵션을 선택합니다.](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="1c50b-129">**복구 모드 선택** 창에서 **개별 파일 및 폴더**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-129">On the **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![파일 찾아보기](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="1c50b-131">**볼륨 및 날짜 선택** 창에서 복원할 파일 및/또는 폴더가 들어있는 볼륨을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-131">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="1c50b-132">달력에서 복구 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-132">On the calendar, select a recovery point.</span></span> <span data-ttu-id="1c50b-133">어떤 복구 시점에서라도 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-133">You can restore from any recovery point in time.</span></span> <span data-ttu-id="1c50b-134">**굵게** 표시된 날짜는 하나 이상의 복구 지점을 사용 가능함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-134">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="1c50b-135">날짜를 선택하고 여러 복구 지점을 사용할 수 있는 경우 **시간** 드롭다운 메뉴에서 특정 복구 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-135">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![볼륨 및 날짜](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="1c50b-137">복원할 복구 지점을 선택했으면 **탑재**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-137">Once you have chosen the recovery point to restore, click **Mount**.</span></span>

    <span data-ttu-id="1c50b-138">Azure Backup은 로컬 복구 지점을 마운트하고 이를 복구 볼륨으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-138">Azure Backup mounts the local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="1c50b-139">**파일 찾아보기 및 복구** 창에서 **찾아보기**를 클릭하여 Windows 탐색기를 열고 원하는 파일 및 폴더를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-139">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![복구 옵션](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="1c50b-141">Windows 탐색기에서 복원할 파일 및/또는 폴더를 복사하여 서버 또는 컴퓨터의 로컬 위치에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-141">In Windows Explorer, copy the files and/or folders you want to restore and paste them to any location local to the server or computer.</span></span> <span data-ttu-id="1c50b-142">복구 볼륨에서 직접 파일을 열거나 스트리밍하여 올바른 버전이 복구되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-142">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![탑재된 볼륨의 파일 및 폴더를 복사하여 로컬 위치에 붙여 넣기](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="1c50b-144">파일 및/또는 폴더 복원이 완료되면 **찾아보기 및 복구 파일** 창에서 **마운트 해제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-144">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="1c50b-145">그런 다음 **예**를 클릭하여 볼륨 마운트 해제를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-145">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![볼륨을 마운트 해제하고 확인](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="1c50b-147">마운트 해제를 클릭하지 않으면 복구 볼륨이 마운트된 후 6시간 동안 마운트된 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-147">If you do not click Unmount, the Recovery Volume will remain mounted for 6 hours from the time when it was mounted.</span></span> <span data-ttu-id="1c50b-148">그러나 탑재 시간은 진행 중인 파일 복사의 경우 최대 24시간까지 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-148">However, the mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="1c50b-149">볼륨이 마운트되는 동안 백업 작업은 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-149">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="1c50b-150">볼륨이 마운트된 시간 동안 실행되도록 스케줄된 모든 백업 작업은 복구 볼륨이 마운트 해제된 후에 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-150">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >


## <a name="use-instant-restore-to-restore-data-to-an-alternate-machine"></a><span data-ttu-id="1c50b-151">즉시 복원을 사용하여 데이터를 대체 컴퓨터에 복원</span><span class="sxs-lookup"><span data-stu-id="1c50b-151">Use Instant Restore to restore data to an alternate machine</span></span>
<span data-ttu-id="1c50b-152">전체 서버가 손실된 경우에도 Azure 백업에서 데이터를 다른 컴퓨터에 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-152">If your entire server is lost, you can still recover data from Azure Backup to a different machine.</span></span> <span data-ttu-id="1c50b-153">다음 단계는 워크플로를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-153">The following steps illustrate the workflow.</span></span>


<span data-ttu-id="1c50b-154">다음 단계에서 사용되는 용어는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-154">The terminology used in these steps includes:</span></span>

* <span data-ttu-id="1c50b-155">*원본 컴퓨터* – 처음에 백업이 수행되었고 현재는 사용할 수 없는 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-155">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="1c50b-156">*대상 컴퓨터* – 데이터가 복구되는 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-156">*Target machine* – The machine to which the data is being recovered.</span></span>
* <span data-ttu-id="1c50b-157">*샘플 자격 증명 모음* – *원본 컴퓨터* 및 *대상 컴퓨터*가 등록된 복구 서비스 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-157">*Sample vault* – The Recovery Services vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="1c50b-158">이전 버전의 운영 체제를 실행하는 대상 시스템으로 백업을 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-158">Backups can't be restored to a target machine running an earlier version of the operating system.</span></span> <span data-ttu-id="1c50b-159">예를 들어, Windows 7 컴퓨터에서 가져온 백업은 Windows 8 이상의 컴퓨터에서 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-159">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="1c50b-160">Windows 8 컴퓨터에서 가져온 백업은 Windows 7 컴퓨터로 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-160">A backup taken from a Windows 8 computer cannot be restored to a Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="1c50b-161">**대상 컴퓨터** 에서 *Microsoft Azure 백업*스냅인을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-161">Open the **Microsoft Azure Backup** snap in on the *Target machine*.</span></span>

2. <span data-ttu-id="1c50b-162">*대상 컴퓨터* 및 *원본 컴퓨터*가 동일한 Recovery Services 자격 증명 모음에 등록됐는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-162">Ensure the *Target machine* and the *Source machine* are registered to the same Recovery Services vault.</span></span>

3. <span data-ttu-id="1c50b-163">**데이터 복구**를 클릭하여 **데이터 복구 마법사**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-163">Click **Recover Data** to open the **Recover Data wizard**.</span></span>

    ![데이터 복구](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="1c50b-165">**시작** 창에서 **다른 서버**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-165">On the **Getting Started** pane, select **Another server**</span></span>

    ![다른 서버](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="1c50b-167">*샘플 자격 증명 모음*에 해당하는 자격 증명 모음 파일을 제공하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-167">Provide the vault credential file that corresponds to the *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="1c50b-168">자격 증명 모음 파일이 유효하지 않거나 만료된 경우 Azure Portal의 *샘플 자격 증명 모음* 에서 새 자격 증명 모음 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-168">If the vault credential file is invalid (or expired), download a new vault credential file from the *Sample vault* in the Azure portal.</span></span> <span data-ttu-id="1c50b-169">유효한 자격 증명 모음을 제공하면 해당 백업 자격 증명 모음의 이름이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-169">Once you provide a valid vault credential, the name of the corresponding Backup Vault appears.</span></span>


6. <span data-ttu-id="1c50b-170">**백업 서버 선택** 창에서 표시된 컴퓨터 목록에서 *원본 컴퓨터*를 선택하고 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-170">On the **Select Backup Server** pane, select the *Source machine* from the list of displayed machines and provide the passphrase.</span></span> <span data-ttu-id="1c50b-171">그런 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-171">Then click **Next**.</span></span>

    ![컴퓨터 목록](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="1c50b-173">**복구 모드 선택** 창에서 **개별 파일 및 폴더**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-173">On the **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Search](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="1c50b-175">**볼륨 및 날짜 선택** 창에서 복원할 파일 및/또는 폴더가 들어있는 볼륨을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-175">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="1c50b-176">달력에서 복구 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-176">On the calendar, select a recovery point.</span></span> <span data-ttu-id="1c50b-177">어떤 복구 시점에서라도 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-177">You can restore from any recovery point in time.</span></span> <span data-ttu-id="1c50b-178">**굵게** 표시된 날짜는 하나 이상의 복구 지점을 사용 가능함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-178">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="1c50b-179">날짜를 선택하고 여러 복구 지점을 사용할 수 있는 경우 **시간** 드롭다운 메뉴에서 특정 복구 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-179">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![검색 항목](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="1c50b-181">복구 지점을 *대상 컴퓨터*에 복구 볼륨으로 로컬로 마운트하려면 **탑재**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-181">Click **Mount** to locally mount the recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="1c50b-182">**파일 찾아보기 및 복구** 창에서 **찾아보기**를 클릭하여 Windows 탐색기를 열고 원하는 파일 및 폴더를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-182">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![암호화](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="1c50b-184">Windows 탐색기에서 복구 볼륨의 파일 및/또는 폴더를 복사하여 *대상 컴퓨터* 위치에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-184">In Windows Explorer, copy the files and/or folders from the recovery volume and paste them to your *Target machine* location.</span></span> <span data-ttu-id="1c50b-185">복구 볼륨에서 직접 파일을 열거나 스트리밍하여 올바른 버전이 복구되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-185">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![암호화](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="1c50b-187">파일 및/또는 폴더 복원이 완료되면 **찾아보기 및 복구 파일** 창에서 **마운트 해제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-187">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="1c50b-188">그런 다음 **예**를 클릭하여 볼륨 마운트 해제를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-188">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![암호화](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="1c50b-190">마운트 해제를 클릭하지 않으면 복구 볼륨이 마운트된 후 6시간 동안 마운트된 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-190">If you do not click Unmount, the Recovery Volume will remain mounted for 6 hours from the time when it was mounted.</span></span> <span data-ttu-id="1c50b-191">그러나 탑재 시간은 진행 중인 파일 복사의 경우 최대 24시간까지 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-191">However, the mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="1c50b-192">볼륨이 마운트되는 동안 백업 작업은 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-192">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="1c50b-193">볼륨이 마운트된 시간 동안 실행되도록 스케줄된 모든 백업 작업은 복구 볼륨이 마운트 해제된 후에 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-193">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >

## <a name="troubleshooting"></a><span data-ttu-id="1c50b-194">문제 해결</span><span class="sxs-lookup"><span data-stu-id="1c50b-194">Troubleshooting</span></span>
<span data-ttu-id="1c50b-195">Azure Backup이 **탑재**를 클릭하고 몇 분 후에 복구 볼륨을 성공적으로 탑재하지 않거나 하나 이상의 오류가 발생하여 복구 볼륨을 탑재하는 데 실패하면 일반적으로 복구를 시작하려면 아래 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-195">If Azure Backup does not successfully mount the recovery volume even after several minutes of clicking **Mount** or fails to mount the recovery volume with one or more errors, follow the steps below to begin recovering normally.</span></span>

1.  <span data-ttu-id="1c50b-196">몇 분 동안 실행된 경우 진행 중인 탑재 프로세스를 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-196">Cancel the ongoing mount process in case it has been running for several minutes.</span></span>

2.  <span data-ttu-id="1c50b-197">최신 버전의 Azure Backup 에이전트가 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-197">Ensure that you are on the latest version of the Azure Backup agent.</span></span> <span data-ttu-id="1c50b-198">Azure Backup 에이전트의 버전 정보를 확인하려면 Microsoft Azure Backup 콘솔의 **작업** 창에서 **Microsoft Azure Recovery Services 에이전트 정보**를 클릭하고 **버전**이 [이 문서](https://go.microsoft.com/fwlink/?linkid=229525)에 언급된 버전 이상인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-198">To find out the version information of Azure Backup agent, click on **About Microsoft Azure Recovery Services Agent** on the **Actions** pane of Microsoft Azure Backup console and ensure that the **Version** number is equal to or higher than the version mentioned in [this article](https://go.microsoft.com/fwlink/?linkid=229525).</span></span> <span data-ttu-id="1c50b-199">최신 버전은 [여기](https://go.microsoft.com/fwLink/?LinkID=288905)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-199">You can download the latest version from [here](https://go.microsoft.com/fwLink/?LinkID=288905)</span></span>

3.  <span data-ttu-id="1c50b-200">**장치 관리자** -> **저장소 컨트롤러**로 이동하고 **Microsoft iSCSI 초기자**를 찾을 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-200">Go to **Device Manager** -> **Storage Controllers** and ensure that you can locate **Microsoft iSCSI Initiator**.</span></span> <span data-ttu-id="1c50b-201">찾을 수 있는 경우 바로 아래의 7단계로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-201">If you can locate it, directly go to step 7 below.</span></span> 

4.  <span data-ttu-id="1c50b-202">3단계에서 설명한 대로 Microsoft iSCSI 초기자 서비스를 찾을 수 없는 경우 하드웨어 ID와 **ROOT\ISCSIPRT**를 포함한 **알 수 없는 장치**라는 항목을 **장치 관리자** -> **저장소 컨트롤러**에서 찾을 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-202">If you cannot locate Microsoft iSCSI Initiator service as mentioned in step 3, check to see if you can find an entry under **Device Manager** -> **Storage Controllers** called **Unknown Device** with Hardware ID **ROOT\ISCSIPRT**.</span></span>

5.  <span data-ttu-id="1c50b-203">**알 수 없는 장치**를 마우스 오른쪽 단추로 클릭하고 **업데이트 드라이버 소프트웨어**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-203">Right click on **Unknown Device** and select **Update Driver Software**.</span></span>

6.  <span data-ttu-id="1c50b-204">**업데이트된 드라이버 소프트웨어를 자동으로 검색**하는 옵션을 선택하여 드라이버를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-204">Update the driver by selecting the option to  **Search automatically for updated driver software**.</span></span> <span data-ttu-id="1c50b-205">업데이트가 완료되면 다음과 같이 **알 수 없는 장치**를 **Microsoft iSCSI 초기자**로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-205">Completion of the update should change **Unknown Device** to **Microsoft iSCSI Initiator** as shown below.</span></span> 

    ![암호화](./media/backup-azure-restore-windows-server/UnknowniSCSIDevice.png)

7.  <span data-ttu-id="1c50b-207">**작업 관리자** -> **서비스(로컬)** -> **Microsoft iSCSI 초기자 서비스**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-207">Go to **Task Manager** -> **Services (Local)** -> **Microsoft iSCSI Initiator Service**.</span></span> 

    ![암호화](./media/backup-azure-restore-windows-server/MicrosoftInitiatorServiceRunning.png)
    
8.  <span data-ttu-id="1c50b-209">서비스를 마우스 오른쪽 단추로 클릭하고 **중지**를 클릭한 다음 마우스 오른쪽 단추로 다시 클릭하고 **시작**을 클릭하여 Microsoft iSCSI 초기자 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-209">Restart the Microsoft iSCSI Initiator service by right-clicking on the service, clicking on **Stop** and further right clicking again and clicking on **Start**.</span></span>

9.  <span data-ttu-id="1c50b-210">인스턴트 복원을 사용하여 복구를 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="1c50b-210">Retry recovering using Instant Restore.</span></span> 

<span data-ttu-id="1c50b-211">복구가 계속 실패하면 서버/클라이언트를 다시 부팅합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-211">If the recovery still fails, reboot your server/client.</span></span> <span data-ttu-id="1c50b-212">다시 부팅이 바람직하지 않거나 서버를 다시 부팅한 후에도 복구가 계속 실패하는 경우 다른 컴퓨터에서 복구를 시도하고 [Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)로 이동하고 지원 요청을 제출하여 Azure 지원에 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-212">If a reboot is not desirable or the recovery still fails even after rebooting the server, try recovering from an Alternate Machine, and contact Azure Support by going to [Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and submitting a support request.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c50b-213">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1c50b-213">Next steps</span></span>
* <span data-ttu-id="1c50b-214">파일과 폴더를 복구했으므로 [백업을 관리](backup-azure-manage-windows-server.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c50b-214">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
