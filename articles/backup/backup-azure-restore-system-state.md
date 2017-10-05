---
title: "Azure Backup: Windows Server에 시스템 상태 복원 | Microsoft Docs"
description: "Azure의 백업에서 Windows Server 시스템 상태를 복원하기 위한 단계별 설명입니다."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/18/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 320c85f8045d9b72cf7f430d2e2736ba8e5ec269
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="restore-system-state-to-windows-server"></a><span data-ttu-id="383fd-103">Windows Server에 시스템 상태 복원</span><span class="sxs-lookup"><span data-stu-id="383fd-103">Restore System State to Windows Server</span></span>

<span data-ttu-id="383fd-104">이 문서에서는 Azure Recovery Services 자격 증명 모음에서 Windows Server 시스템 상태 백업을 복원하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-104">This article explains how to restore Windows Server System State backups from an Azure Recovery Services vault.</span></span> <span data-ttu-id="383fd-105">시스템 상태를 복원하려면 시스템 상태 백업([시스템 상태 백업](backup-azure-system-state.md#back-up-windows-server-system-state-preview)의 지침을 사용하여 만듬)이 있어야 하고 [최신 버전의 MARS(Microsoft Azure Recovery Services) 에이전트](http://aka.ms/azurebackup_agent)를 설치했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-105">To restore System State, you must have a System State backup (created using the instructions in [Back up System State](backup-azure-system-state.md#back-up-windows-server-system-state-preview)), and make sure you have installed the [latest version of the Microsoft Azure Recovery Services (MARS) agent](http://aka.ms/azurebackup_agent).</span></span> <span data-ttu-id="383fd-106">Azure Recovery Services 자격 증명 모음에서 Windows Server 시스템 상태 데이터를 복구하는 작업은 두 단계로 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-106">Recovering Windows Server System State data from an Azure Recovery Services vault is a two-step process:</span></span>

1. <span data-ttu-id="383fd-107">Azure Backup에서 파일로 시스템 상태 복원</span><span class="sxs-lookup"><span data-stu-id="383fd-107">Restore System State as files from Azure Backup.</span></span> <span data-ttu-id="383fd-108">Azure Backup에서 파일로 시스템 상태를 복원할 경우 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-108">When restoring System State as files from Azure Backup, you can either:</span></span>
  * <span data-ttu-id="383fd-109">백업이 수행된 동일한 서버에 시스템 상태 복원 또는</span><span class="sxs-lookup"><span data-stu-id="383fd-109">Restore System State to the same server where the backups were taken, or</span></span>
  * <span data-ttu-id="383fd-110">대체 서버에 시스템 상태 파일 복원</span><span class="sxs-lookup"><span data-stu-id="383fd-110">Restore System State file to an alternate server.</span></span>

2. <span data-ttu-id="383fd-111">Windows Server에 복원된 시스템 상태 파일 적용</span><span class="sxs-lookup"><span data-stu-id="383fd-111">Apply the restored System State files to a Windows Server.</span></span>


## <a name="recover-system-state-files-to-the-same-server"></a><span data-ttu-id="383fd-112">동일한 서버에 시스템 상태 파일 복구</span><span class="sxs-lookup"><span data-stu-id="383fd-112">Recover System State files to the same server</span></span>
<span data-ttu-id="383fd-113">다음 단계에서는 Windows Server 구성을 이전 상태로 롤백하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-113">The following steps explain how to roll back your Windows Server configuration to a previous state.</span></span> <span data-ttu-id="383fd-114">서버 구성을 알려진 안정적인 상태로 다시 롤백하는 작업은 매우 중요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-114">Rolling your server configuration back to a known, stable state, can be extremely valuable.</span></span> <span data-ttu-id="383fd-115">다음 단계는 Recovery Services 자격 증명 모음에서 서버의 시스템 상태를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-115">The following steps restore the server's System State from a Recovery Services vault.</span></span> 

1. <span data-ttu-id="383fd-116">**Microsoft Azure Backup** 스냅인을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-116">Open the **Microsoft Azure Backup** snap-in.</span></span> <span data-ttu-id="383fd-117">스냅인이 설치된 위치를 모르는 경우 컴퓨터 또는 서버에서 **Microsoft Azure Backup**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-117">If you don't know where the snap-in was installed, search the computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="383fd-118">데스크톱 앱이 검색 결과에 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-118">The desktop app should appear in the search results.</span></span>

2. <span data-ttu-id="383fd-119">마법사를 시작하려면 **데이터 복구**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-119">Click **Recover Data** to start the wizard.</span></span>

    ![데이터 복구](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="383fd-121">**시작** 창에서 동일한 서버 또는 컴퓨터로 데이터를 복원하려면 **이 서버(`<server name>`)**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-121">On the **Getting Started** pane, to restore the data to the same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![같은 컴퓨터에 데이터를 복원하려면 이 서버 옵션을 선택합니다.](./media/backup-azure-restore-system-state/samemachine.png)

4. <span data-ttu-id="383fd-123">**복구 모드 선택** 창에서 **시스템 상태**를 선택하고 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-123">On the **Select Recovery Mode** pane, choose **System State** and then click **Next**.</span></span>

    ![파일 찾아보기](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. <span data-ttu-id="383fd-125">**볼륨 및 날짜 선택** 창의 일정에서 복구 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-125">On the calendar in **Select Volume and Date** pane, select a recovery point.</span></span> 

    <span data-ttu-id="383fd-126">어떤 복구 시점에서라도 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-126">You can restore from any recovery point in time.</span></span> <span data-ttu-id="383fd-127">**굵게** 표시된 날짜는 하나 이상의 복구 지점을 사용 가능함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-127">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="383fd-128">날짜를 선택하고 여러 복구 지점을 사용할 수 있는 경우 **시간** 드롭다운 메뉴에서 특정 복구 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-128">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![볼륨 및 날짜](./media/backup-azure-restore-system-state/select-date.png)

6. <span data-ttu-id="383fd-130">복원할 복구 지점을 선택했으면 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-130">Once you have chosen the recovery point to restore, click **Next**.</span></span>

    <span data-ttu-id="383fd-131">Azure Backup은 로컬 복구 지점을 마운트하고 이를 복구 볼륨으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-131">Azure Backup mounts the local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="383fd-132">다음 창에서 복구된 시스템 상태 파일에 대상을 지정하고 **찾아보기**를 클릭하여 Windows Explorer를 열고 원하는 파일 및 폴더를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-132">On the next pane, specify the destination for the recovered System State files and click **Browse** to open Windows Explorer and find the files and folders you want.</span></span> <span data-ttu-id="383fd-133">**두 버전 모두 유지하도록 복사본 만들기** 옵션을 통해 전체 시스템 상태 아카이브의 복사본을 만드는 대신 기존의 시스템 상태 파일 아카이브에서 개별 파일의 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-133">The option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating the copy of the entire System State archive.</span></span>

    ![복구 옵션](./media/backup-azure-restore-system-state/recover-as-files.png)

8. <span data-ttu-id="383fd-135">**확인** 창에서 복구의 세부 정보를 확인하고 **복구**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-135">Verify the details of recovery on the **Confirmation** pane and click **Recover**.</span></span>

   ![복구를 클릭하여 복구 작업 승인](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. <span data-ttu-id="383fd-137">복구 대상에서 *WindowsImageBackup* 디렉터리를 서버의 중요하지 않은 볼륨에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-137">Copy the *WindowsImageBackup* directory in the Recovery destination to a non-critical volume of the server.</span></span> <span data-ttu-id="383fd-138">일반적으로 Windows OS 볼륨은 중요한 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-138">Usually, the Windows OS volume is the critical volume.</span></span>

10. <span data-ttu-id="383fd-139">성공적으로 복구되면 [Windows Server에 복원된 시스템 상태 파일 적용](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server) 섹션의 단계에 따라 시스템 상태 복구 프로세스를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-139">Once the recovery is successful, follow the steps in the section, [Apply restored System State files to the Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), to complete the System State recovery process.</span></span>

## <a name="recover-system-state-files-to-an-alternate-server"></a><span data-ttu-id="383fd-140">대체 서버에 시스템 상태 파일 복구</span><span class="sxs-lookup"><span data-stu-id="383fd-140">Recover System State files to an alternate server</span></span>

<span data-ttu-id="383fd-141">Windows Server가 손상되었거나 액세스할 수 없고 Windows Server 시스템 상태를 복구하여 안정적인 상태로 복원하려는 경우 다른 서버에서 손상된 서버의 시스템 상태를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-141">If your Windows Server is corrupted or inaccessible, and you want to restore it to a stable state by recovering the Windows Server System State, you can restore the corrupted server's System State from another server.</span></span> <span data-ttu-id="383fd-142">별도 서버에서 시스템 상태를 복원하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-142">Use the following steps to the restore System State on a separate server.</span></span>  

<span data-ttu-id="383fd-143">다음 단계에서 사용되는 용어는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-143">The terminology used in these steps includes:</span></span>

- <span data-ttu-id="383fd-144">*원본 컴퓨터* – 처음에 백업이 수행되었고 현재는 사용할 수 없는 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-144">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
- <span data-ttu-id="383fd-145">*대상 컴퓨터* – 데이터가 복구되는 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-145">*Target machine* – The machine to which the data is being recovered.</span></span>
- <span data-ttu-id="383fd-146">*샘플 자격 증명 모음* – *원본 컴퓨터* 및 *대상 컴퓨터*가 등록된 복구 서비스 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-146">*Sample vault* – The Recovery Services vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="383fd-147">이전 버전의 운영 체제를 실행 중인 컴퓨터에는 컴퓨터에서 수행된 백업을 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-147">Backups taken from one machine cannot be restored to a machine running an earlier version of the operating system.</span></span> <span data-ttu-id="383fd-148">예를 들어 Windows Server 2016 컴퓨터에서 수행된 백업은 Windows Server 2012 R2로 복원될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-148">For example, backups taken from a Windows Server 2016 machine can't be restored to Windows Server 2012 R2.</span></span> <span data-ttu-id="383fd-149">그러나 반대는 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-149">However, the inverse is possible.</span></span> <span data-ttu-id="383fd-150">Windows Server 2016을 복원하려면 Windows Server 2012 R2에서 백업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-150">You can use backups from Windows Server 2012 R2 to restore Windows Server 2016.</span></span>
>

1. <span data-ttu-id="383fd-151">**대상 컴퓨터**에서 *Microsoft Azure Backup* 스냅인을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-151">Open the **Microsoft Azure Backup** snap-in on the *Target machine*.</span></span>
2. <span data-ttu-id="383fd-152">*대상 컴퓨터* 및 *원본 컴퓨터*가 동일한 복구 서비스 자격 증명 모음에 등록됐는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-152">Ensure that the *Target machine* and the *Source machine* are registered to the same Recovery Services vault.</span></span>
3. <span data-ttu-id="383fd-153">**데이터 복구** 를 클릭하여 워크플로를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-153">Click **Recover Data** to initiate the workflow.</span></span>

    ![데이터 복구](./media/backup-azure-restore-windows-server-classic/recover.png)

4. <span data-ttu-id="383fd-155">**다른 서버**</span><span class="sxs-lookup"><span data-stu-id="383fd-155">Select **Another server**</span></span>

    ![다른 서버](./media/backup-azure-restore-system-state/anotherserver.png)

5. <span data-ttu-id="383fd-157">*샘플 자격 증명 모음*에 해당하는 자격 증명 모음 파일을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-157">Provide the vault credential file that corresponds to the *Sample vault*.</span></span> <span data-ttu-id="383fd-158">자격 증명 모음 파일이 유효하지 않거나 만료된 경우 Azure Portal의 *샘플 자격 증명 모음* 에서 새 자격 증명 모음 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-158">If the vault credential file is invalid (or expired), download a new vault credential file from the *Sample vault* in the Azure portal.</span></span> <span data-ttu-id="383fd-159">자격 증명 모음 파일이 제공되면 자격 증명 모음 파일과 연결된 Recovery Services 자격 증명 모음이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-159">Once the vault credential file is provided, the Recovery Services vault associated with the vault credential file appears.</span></span>

6. <span data-ttu-id="383fd-160">백업 서버 선택 창의 표시된 컴퓨터 목록에서 *원본 컴퓨터*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-160">On the Select Backup Server pane, select the *Source machine* from the list of displayed machines.</span></span>

    ![컴퓨터 목록](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. <span data-ttu-id="383fd-162">복구 모드 선택 창에서 **시스템 상태**를 선택하고 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-162">On the Select Recovery Mode pane, choose **System State** and click **Next**.</span></span> 

    ![검색](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. <span data-ttu-id="383fd-164">**볼륨 및 날짜 선택** 창의 일정에서 복구 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-164">On the Calendar in the **Select Volume and Date** pane, select a recovery point.</span></span> <span data-ttu-id="383fd-165">어떤 복구 시점에서라도 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-165">You can restore from any recovery point in time.</span></span> <span data-ttu-id="383fd-166">**굵게** 표시된 날짜는 하나 이상의 복구 지점을 사용 가능함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-166">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="383fd-167">날짜를 선택하고 여러 복구 지점을 사용할 수 있는 경우 **시간** 드롭다운 메뉴에서 특정 복구 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-167">Once  you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span> 

    ![검색 항목](./media/backup-azure-restore-system-state/select-date.png)

9. <span data-ttu-id="383fd-169">복원할 복구 지점을 선택했으면 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-169">Once you have chosen the recovery point to restore, click **Next**.</span></span>

10. <span data-ttu-id="383fd-170">**시스템 상태 복구 모드 선택** 창에서 시스템 상태 파일을 복구하려는 대상을 지정한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-170">On the **Select System State Recovery Mode** pane, specify the destination where you want System State files to be recovered, then click **Next**.</span></span>

    ![암호화](./media/backup-azure-restore-system-state/recover-as-files.png)

    <span data-ttu-id="383fd-172">**두 버전 모두 유지하도록 복사본 만들기** 옵션을 통해 전체 시스템 상태 아카이브의 복사본을 만드는 대신 기존의 시스템 상태 파일 아카이브에서 개별 파일의 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-172">The option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating the copy of the entire System State archive.</span></span>

11. <span data-ttu-id="383fd-173">확인 창에서 복구의 세부 정보를 확인하고 **복구**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-173">Verify the details of recovery on the Confirmation pane, and click **Recover**.</span></span> 

    ![복구 단추를 클릭하여 복구 프로세스 확인](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. <span data-ttu-id="383fd-175">*WindowsImageBackup* 디렉터리를 서버의 중요하지 않은 볼륨에 복사합니다(예: d:\).</span><span class="sxs-lookup"><span data-stu-id="383fd-175">Copy the *WindowsImageBackup* directory to a non-critical volume of the server (for example D:\).</span></span> <span data-ttu-id="383fd-176">일반적으로 Windows OS 볼륨은 중요한 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-176">Usually the Windows OS volume is the critical volume.</span></span>

13. <span data-ttu-id="383fd-177">복구 프로세스를 완료하려면 다음 섹션을 사용하여 [Windows Server에서 복원된 시스템 상태 파일을 적용](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server)합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-177">To complete the recovery process, use the following section to [apply the restored System State files on a Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span></span>




## <a name="apply-restored-system-state-on-a-windows-server"></a><span data-ttu-id="383fd-178">Windows Server에서 복원된 시스템 상태 적용</span><span class="sxs-lookup"><span data-stu-id="383fd-178">Apply restored System State on a Windows Server</span></span>

<span data-ttu-id="383fd-179">Azure Recovery Services 에이전트를 사용하여 시스템 상태를 파일로 복구했다면 Windows Server 백업 유틸리티를 사용하여 복구된 시스템 상태를 Windows Server에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-179">Once you have recovered System State as files using Azure Recovery Services Agent, use the Windows Server Backup utility to apply the recovered System State to Windows Server.</span></span> <span data-ttu-id="383fd-180">Windows Server Backup 유틸리티를 서버에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-180">The Windows Server Backup utility is already available on the server.</span></span> <span data-ttu-id="383fd-181">다음 단계에서는 복구된 시스템 상태를 적용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-181">The following steps explain how to apply the recovered System State.</span></span>

1. <span data-ttu-id="383fd-182">다음 명령을 사용하여 *디렉터리 서비스 복구 모드*로 서버를 다시 부팅합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-182">Use the following commands to reboot your server in *Directory Services Repair Mode*.</span></span> <span data-ttu-id="383fd-183">관리자 권한 명령 프롬프트에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-183">In an elevated command prompt:</span></span>

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. <span data-ttu-id="383fd-184">다시 부팅한 후에 Windows Server Backup 스냅인을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-184">After the reboot, open the Windows Server Backup snap-in.</span></span> <span data-ttu-id="383fd-185">스냅인이 설치된 위치를 모르는 경우 컴퓨터 또는 서버에서 **Windows Server Backup**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-185">If you don't know where the snap-in was installed, search the computer or server for **Windows Server Backup**.</span></span>

    <span data-ttu-id="383fd-186">데스크톱 앱이 검색 결과에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-186">The desktop app appears in the search results.</span></span>

3. <span data-ttu-id="383fd-187">스냅인에서 **로컬 백업**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-187">In the snap-in, select **Local Backup**.</span></span>

    ![여기에서 복원할 로컬 백업 선택](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. <span data-ttu-id="383fd-189">로컬 백업 콘솔의 **작업 창**에서 **복구**를 클릭하여 복구 마법사를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-189">On the Local Backup console, in the **Actions Pane**, click **Recover** to open the Recovery Wizard.</span></span>

5. <span data-ttu-id="383fd-190">**다른 위치에 저장된 백업** 옵션을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-190">Select the option, **A backup stored in another location**, and click **Next**.</span></span>

   ![다른 서버에 복구하도록 선택](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. <span data-ttu-id="383fd-192">시스템 상태 백업을 다른 서버로 복구한 경우 위치 형식에 지정할 때 **원격 공유 폴더**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-192">When specifying the location type, select **Remote shared folder** if your System State backup was recovered to another server.</span></span> <span data-ttu-id="383fd-193">시스템 상태가 로컬로 복구된 경우 **로컬 드라이브**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-193">If your System State was recovered locally, then select **Local drives**.</span></span> 

    ![로컬 서버가 아니면 다른 서버로부터 복구 선택](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. <span data-ttu-id="383fd-195">*WindowsImageBackup* 디렉터리에 대한 경로를 입력하거나 Azure Recovery Services 에이전트를 사용하여 시스템 상태 파일 복구의 일부로 복구된 이 디렉터리(예: D:\WindowsImageBackup)를 포함하는 로컬 드라이브를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-195">Enter the path to the *WindowsImageBackup* directory, or choose the local drive containing this directory (for example, D:\WindowsImageBackup), recovered as part of the System State files recovery using Azure Recovery Services Agent and click **Next**.</span></span>

    ![공유 파일에 대한 경로](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. <span data-ttu-id="383fd-197">복원하려는 시스템 상태 버전을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-197">Select the System State version that you want to restore, and click **Next**.</span></span>

9. <span data-ttu-id="383fd-198">복구 유형 선택 창에서 **시스템 상태**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-198">In the Select Recovery Type pane, select **System State** and click **Next**.</span></span>

10. <span data-ttu-id="383fd-199">시스템 상태 복구 위치에서 **원래 위치**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-199">For the location of the System State Recovery, select **Original Location**, and click **Next**.</span></span>

11. <span data-ttu-id="383fd-200">확인 세부 정보를 검토하고, 다시 부팅 설정을 확인하고, **복구**를 클릭하여 복원된 시스템 상태 파일을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-200">Review the confirmation details, verify the reboot settings, and click **Recover** to applly the restored System State files.</span></span>

    ![복원된 시스템 상태 파일 시작](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a><span data-ttu-id="383fd-202">Active Directory 서버에서 시스템 상태 복구에 대한 특별 고려 사항</span><span class="sxs-lookup"><span data-stu-id="383fd-202">Special considerations for System State recovery on Active Directory server</span></span>

<span data-ttu-id="383fd-203">시스템 상태 백업은 Active Directory 데이터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-203">System State backup includes Active Directory data.</span></span> <span data-ttu-id="383fd-204">다음 단계를 사용하여 현재 상태에서 이전 상태로 AD DS(Active Directory Domain Service)를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-204">Use the following steps to restore Active Directory Domain Service (AD DS) from its current state to a previous state.</span></span>

1. <span data-ttu-id="383fd-205">DSRM(디렉터리 서비스 복원 모드)로 도메인 컨트롤러를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-205">Restart the domain controller in Directory Services Restore Mode (DSRM).</span></span>
2. <span data-ttu-id="383fd-206">Windows Server Backup cmdlet을 사용하여 AD DS를 복구하려면 [여기](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) 있는 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-206">Follow the steps [here](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) to use Windows Server Backup cmdlets to recover AD DS.</span></span>


## <a name="troubleshoot-failed-system-state-restore"></a><span data-ttu-id="383fd-207">실패한 시스템 상태 복원 문제 해결</span><span class="sxs-lookup"><span data-stu-id="383fd-207">Troubleshoot failed System State restore</span></span>

<span data-ttu-id="383fd-208">시스템 상태를 적용하는 이전 프로세스가 성공적으로 완료되지 않으면 Win RE(Windows Recovery Environment)를 사용하여 Windows Server를 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-208">If the previous process of applying System State does not complete successfully, use the Windows Recovery Environment (Win RE) to recover your Windows Server.</span></span> <span data-ttu-id="383fd-209">다음 단계에서는 Win RE를 사용하여 복구하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-209">The following steps explain how to recover using Win RE.</span></span> <span data-ttu-id="383fd-210">시스템 상태 복원 후에 Windows Server가 정상적으로 부팅되지 않는 경우에만 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-210">Use This option only if Windows Server does not boot normally after a System State restore.</span></span> <span data-ttu-id="383fd-211">다음 프로세스는 비 시스템 데이터를 지우고 주의를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-211">The following process erases non-system data, use caution.</span></span> 

1. <span data-ttu-id="383fd-212">Win RE(Windows Recovery Environment)로 Windows Server를 부팅합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-212">Boot your Windows Server into the Windows Recovery Environment (Win RE).</span></span>

2. <span data-ttu-id="383fd-213">사용 가능한 세 가지 옵션 중에서 문제 해결을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-213">Select Troubleshoot from the three available options.</span></span>

    ![메뉴 열기](./media/backup-azure-restore-system-state/winre-1.png)

3. <span data-ttu-id="383fd-215">**고급 옵션** 화면에서 **명령 프롬프트**를 선택하고 서버 관리 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-215">From the **Advanced Options** screen, select **Command Prompt** and provide the server administrator username and password.</span></span>

   ![메뉴 열기](./media/backup-azure-restore-system-state/winre-2.png)

4. <span data-ttu-id="383fd-217">서버 관리 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-217">Provide the server administrator username and password.</span></span>

    ![메뉴 열기](./media/backup-azure-restore-system-state/winre-3.png)

5. <span data-ttu-id="383fd-219">관리자 모드에서 명령 프롬프트를 여는 경우 시스템 상태 백업 버전을 가져오는 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-219">When you open the command prompt in administrator mode, run following command to get the System State backup versions.</span></span>

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![시스템 상태 백업 버전 가져오기](./media/backup-azure-restore-system-state/winre-4.png)

6. <span data-ttu-id="383fd-221">백업에 사용할 수 있는 모든 볼륨을 가져오는 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-221">Run the following command to get all volumes available in the backup.</span></span>

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![시스템 상태 백업 버전 가져오기](./media/backup-azure-restore-system-state/winre-5.png)

7. <span data-ttu-id="383fd-223">다음 명령은 시스템 상태 백업이 포함된 모든 볼륨을 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-223">The following command recovers all volumes that are part of the System State Backup.</span></span> <span data-ttu-id="383fd-224">이 단계는 시스템 상태가 포함된 중요한 볼륨만을 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-224">Note that this step recovers only the critical volumes that are part of the System State.</span></span> <span data-ttu-id="383fd-225">모든 비 시스템 데이터가 지워집니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-225">All non-System data is erased.</span></span>

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![시스템 상태 백업 버전 가져오기](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a><span data-ttu-id="383fd-227">다음 단계</span><span class="sxs-lookup"><span data-stu-id="383fd-227">Next steps</span></span>
* <span data-ttu-id="383fd-228">파일과 폴더를 복구했으므로 [백업을 관리](backup-azure-manage-windows-server.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="383fd-228">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
