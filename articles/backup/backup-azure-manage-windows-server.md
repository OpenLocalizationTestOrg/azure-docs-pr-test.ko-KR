---
title: "Azure 복구 서비스 자격 증명 모음 및 서버 관리 | Microsoft Docs"
description: "이 자습서를 사용하여 Azure 복구 서비스 자격 증명 모음 및 서버를 관리하는 방법을 알아봅니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: 4eea984b-7ed6-4600-ac60-99d2e9cb6d8a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markgal
ms.openlocfilehash: 5922e308f5c205a07bd329c28322ae82cea0e1fa
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a><span data-ttu-id="b1d89-103">Windows 컴퓨터용 Azure 복구 서비스 자격 증명 모음 및 서버 모니터링 및 관리</span><span class="sxs-lookup"><span data-stu-id="b1d89-103">Monitor and manage Azure recovery services vaults and servers for Windows machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b1d89-104">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="b1d89-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="b1d89-105">클래식</span><span class="sxs-lookup"><span data-stu-id="b1d89-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="b1d89-106">이 문서에서는 Azure Portal 및 Microsoft Azure Backup 에이전트를 통해 사용할 수 있는 백업 모니터 및 관리 작업의 개요를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-106">In this article you'll find an overview of the backup monitor and management tasks available through the Azure portal and the Microsoft Azure Backup agent.</span></span> <span data-ttu-id="b1d89-107">이 문서에서는 이미 Azure 구독이 있으며 하나 이상의 Recovery Services Vault 를 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-107">This article assumes you already have an Azure subscription and have created at least one Recovery Services vault.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a><span data-ttu-id="b1d89-108">Recovery Services Vault 열기</span><span class="sxs-lookup"><span data-stu-id="b1d89-108">Open a Recovery Services vault</span></span>

<span data-ttu-id="b1d89-109">Recovery Services Vault 대시보드에는 Recovery Services Vault의 세부 정보 또는 특성이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-109">The Recovery Services vault dashboard shows you the details or attributes of a Recovery Services vault.</span></span>

1. <span data-ttu-id="b1d89-110">Azure 구독을 사용하여 [Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-110">Sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="b1d89-111">허브 메뉴에서 **추가 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-111">On the Hub menu, click **More Services**.</span></span>

    ![Recovery Services Vault 목록 열기 1단계](./media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. <span data-ttu-id="b1d89-113">Recovery Services Vault를 열려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-113">You want to open a Recovery Services vault.</span></span> <span data-ttu-id="b1d89-114">대화 상자에서 **Recovery Services** 입력을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-114">In the dialog box, start typing **Recovery Services**.</span></span> <span data-ttu-id="b1d89-115">입력을 시작하면 목록이 입력에 따라 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-115">As you begin typing, the list will filter based on your input.</span></span> <span data-ttu-id="b1d89-116">**Recovery Services Vault**를 클릭하여 구독의 Recovery Services Vault 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-116">Click **Recovery Services vaults** to display the list of Recovery Services vaults in your subscription.</span></span>

    ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    <span data-ttu-id="b1d89-118">Recovery Services Vault 목록이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-118">The list of Recovery Services vaults opens.</span></span>

    ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. <span data-ttu-id="b1d89-120">Vault 목록에서 열려는 Recovery Services Vault의 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-120">From the list of vaults, select the name of the Recovery Services vault you want to open.</span></span> <span data-ttu-id="b1d89-121">복구 서비스 자격 증명 모음 대시보드 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-121">The Recovery Services vault dashboard blade opens.</span></span>

    ![복구 서비스 자격 증명 모음 대시보드](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    <span data-ttu-id="b1d89-123">Recovery Services Vault를 열었으므로 모니터링 또는 관리 작업을 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="b1d89-123">Now that you have opened the Recovery Services vault, try any of the monitoring or management tasks.</span></span>

## <a name="monitor-backup-jobs-and-alerts"></a><span data-ttu-id="b1d89-124">백업 작업 및 경고 모니터링</span><span class="sxs-lookup"><span data-stu-id="b1d89-124">Monitor backup jobs and alerts</span></span>

<span data-ttu-id="b1d89-125">다음 정보가 표시되는 복구 서비스 자격 증명 모음 대시보드에서 작업 및 경고를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-125">You monitor jobs and alerts from the Recovery Services vault dashboard, where you see:</span></span>

* <span data-ttu-id="b1d89-126">백업 경고 세부 정보</span><span class="sxs-lookup"><span data-stu-id="b1d89-126">Backup alerts details</span></span>
* <span data-ttu-id="b1d89-127">파일 및 폴더, 그리고 클라우드에 보호되는 Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="b1d89-127">Files and folders, as well as Azure virtual machines protected in the cloud</span></span>
* <span data-ttu-id="b1d89-128">Azure에서 사용되는 총 저장소</span><span class="sxs-lookup"><span data-stu-id="b1d89-128">Total storage consumed in Azure</span></span>
* <span data-ttu-id="b1d89-129">백업 작업 상태</span><span class="sxs-lookup"><span data-stu-id="b1d89-129">Backup job status</span></span>

![백업 대시보드 작업](./media/backup-azure-manage-windows-server/dashboard-tiles.png)

<span data-ttu-id="b1d89-131">이러한 각 타일의 정보를 클릭하면 관련 작업을 관리하는 연결된 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-131">Clicking the information in each of these tiles will open the associated blade where you manage related tasks.</span></span>

<span data-ttu-id="b1d89-132">대시보드의 맨 위에서:</span><span class="sxs-lookup"><span data-stu-id="b1d89-132">From the top of the Dashboard:</span></span>

* <span data-ttu-id="b1d89-133">사용할 수 있는 백업 작업에 대한 액세스를 제공하는 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-133">Settings provides access available backup tasks.</span></span>
* <span data-ttu-id="b1d89-134">백업 - 새 파일 및 폴더(또는 Azure VM)을 복구 서비스 자격 증명 모음에 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-134">Backup - helps you back up new files and folders (or Azure VMs) to the Recovery Services vault.</span></span>
* <span data-ttu-id="b1d89-135">삭제 - 복구 서비스 자격 증명 모음이 더 이상 사용할 수 없는 경우 삭제하여 저장소 공간을 확보할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-135">Delete - If a recovery services vault is no longer being used, you can delete it to free up storage space.</span></span> <span data-ttu-id="b1d89-136">삭제는 등록된 모든 보호된 서버가 자격 증명 모음에서 삭제된 후에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-136">Delete is only enabled after all protected servers have been deleted from the vault.</span></span>

![백업 대시보드 작업](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a><span data-ttu-id="b1d89-138">Azure 백업 에이전트에 의한 백업 경고</span><span class="sxs-lookup"><span data-stu-id="b1d89-138">Alerts for backups using Azure backup agent:</span></span>
| <span data-ttu-id="b1d89-139">경고 수준</span><span class="sxs-lookup"><span data-stu-id="b1d89-139">Alert Level</span></span> | <span data-ttu-id="b1d89-140">전송되는 경고</span><span class="sxs-lookup"><span data-stu-id="b1d89-140">Alerts sent</span></span> |
| --- | --- |
| <span data-ttu-id="b1d89-141">중요</span><span class="sxs-lookup"><span data-stu-id="b1d89-141">Critical</span></span> |<span data-ttu-id="b1d89-142">백업 실패, 복구 실패</span><span class="sxs-lookup"><span data-stu-id="b1d89-142">Backup failure, recovery failure</span></span> |
| <span data-ttu-id="b1d89-143">Warning</span><span class="sxs-lookup"><span data-stu-id="b1d89-143">Warning</span></span> |<span data-ttu-id="b1d89-144">백업이 완료되었지만 경고가 발생했습니다(손상 문제로 인해 100개 미만의 파일이 백업되지 않았고 1백만 개 이상의 파일이 성공적으로 백업된 경우).</span><span class="sxs-lookup"><span data-stu-id="b1d89-144">Backup completed with warnings (when fewer than one hundred files are not backed up due to corruption issues, and more than one million files are successfully backed up)</span></span> |
| <span data-ttu-id="b1d89-145">정보 제공</span><span class="sxs-lookup"><span data-stu-id="b1d89-145">Informational</span></span> |<span data-ttu-id="b1d89-146">없음</span><span class="sxs-lookup"><span data-stu-id="b1d89-146">None</span></span> |

## <a name="manage-backup-alerts"></a><span data-ttu-id="b1d89-147">백업 경고 관리</span><span class="sxs-lookup"><span data-stu-id="b1d89-147">Manage Backup alerts</span></span>
<span data-ttu-id="b1d89-148">**백업 경고** 타일을 클릭하여 **백업 경고** 블레이드를 열고 경고를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-148">Click the **Backup Alerts** tile to open the **Backup Alerts** blade and manage alerts.</span></span>

![백업 경고](./media/backup-azure-manage-windows-server/manage-backup-alerts.png)

<span data-ttu-id="b1d89-150">백업 경고 타일은 다음 사항의 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-150">The Backup Alerts tile shows you the number of:</span></span>

* <span data-ttu-id="b1d89-151">지난 24 시간 동안 확인되지 않은 중요한 경고</span><span class="sxs-lookup"><span data-stu-id="b1d89-151">critical alerts unresolved in last 24 hours</span></span>
* <span data-ttu-id="b1d89-152">지난 24 시간 동안 확인되지 않은 경고</span><span class="sxs-lookup"><span data-stu-id="b1d89-152">warning alerts unresolved in last 24 hours</span></span>

<span data-ttu-id="b1d89-153">이 링크를 각각 클릭하면 **백업 경고** 블레이드로 이동하며 이 경고의 필터링된 보기(중요 또는 경고)가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-153">Clicking on each of these links takes you to the **Backup Alerts** blade with a filtered view of these alerts (critical or warning).</span></span>

<span data-ttu-id="b1d89-154">백업 경고 블레이드에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-154">From the Backup Alerts blade, you:</span></span>

* <span data-ttu-id="b1d89-155">경고와 함께 포함할 적절한 정보를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-155">Choose the appropriate information to include with your alerts.</span></span>

    ![열 선택](./media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* <span data-ttu-id="b1d89-157">심각도, 상태 및 시작/종료 시간에 대한 경고를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-157">Filter alerts for severity, status and start/end times.</span></span>

    ![경고 필터링](./media/backup-azure-manage-windows-server/filter-alerts.png)
* <span data-ttu-id="b1d89-159">심각도, 빈도 및 받는 사람에 대한 알림을 구성하며 경고를 켜거나 끕니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-159">Configure notifications for severity, frequency and recipients, as well as turn alerts on or off.</span></span>

    ![경고 필터링](./media/backup-azure-manage-windows-server/configure-notifications.png)

<span data-ttu-id="b1d89-161">**경보별**을 **알림** 빈도로 선택한 경우 메일 그룹화 또는 축소가 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-161">If **Per Alert** is selected as the **Notify** frequency no grouping or reduction in emails occurs.</span></span> <span data-ttu-id="b1d89-162">모든 경고에 대해 알림 1개가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-162">Every alert results in 1 notification.</span></span> <span data-ttu-id="b1d89-163">이것이 기본 설정이며 확인 메일도 즉시 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-163">This is the default setting and the resolution email is also sent out immediately.</span></span>

<span data-ttu-id="b1d89-164">**시간별 요약**을 **알림** 빈도로 선택하면 지난 한 시간 동안 생성되어 확인되지 않은 새 경고가 있음을 알려 주는 메일 한 개가 사용자에게 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-164">If **Hourly Digest** is selected as the **Notify** frequency one email is sent to the user telling them that there are unresolved new alerts generated in the last hour.</span></span> <span data-ttu-id="b1d89-165">한 시간이 끝날 때 확인 메일이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-165">A resolution email is sent out at the end of the hour.</span></span>

<span data-ttu-id="b1d89-166">다음 심각도 수준의 경고를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-166">Alerts can be sent for the following severity levels:</span></span>

* <span data-ttu-id="b1d89-167">중요</span><span class="sxs-lookup"><span data-stu-id="b1d89-167">critical</span></span>
* <span data-ttu-id="b1d89-168">Warning</span><span class="sxs-lookup"><span data-stu-id="b1d89-168">warning</span></span>
* <span data-ttu-id="b1d89-169">정보</span><span class="sxs-lookup"><span data-stu-id="b1d89-169">information</span></span>

<span data-ttu-id="b1d89-170">작업 세부 정보 블레이드의 **비활성화** 단추로 경고를 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-170">You inactivate the alert with the **inactivate** button in the job details blade.</span></span> <span data-ttu-id="b1d89-171">비활성화를 클릭하면 확인 참고 사항을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-171">When you click inactivate, you can provide resolution notes.</span></span>

<span data-ttu-id="b1d89-172">**열 선택** 단추를 사용하여 경고의 일부로 나타낼 열을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-172">You choose the columns you want to appear as part of the alert with the **Choose columns** button.</span></span>

> [!NOTE]
> <span data-ttu-id="b1d89-173">**설정** 블레이드에서 **모니터링 및 보고서 > 경고 및 이벤트 > 백업 경고**를 선택한 다음 **필터** 또는 **알림 구성**을 클릭하여 백업 경고를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-173">From the **Settings** blade, you manage backup alerts by selecting **Monitoring and Reports > Alerts and Events > Backup Alerts** and then clicking **Filter** or **Configure Notifications**.</span></span>
>
>

## <a name="manage-backup-items"></a><span data-ttu-id="b1d89-174">백업 항목 관리</span><span class="sxs-lookup"><span data-stu-id="b1d89-174">Manage Backup items</span></span>
<span data-ttu-id="b1d89-175">온-프레미스 백업 관리는 이제 관리 포털에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-175">Managing on-premises backups is now available in the management portal.</span></span> <span data-ttu-id="b1d89-176">대시보드의 백업 섹션에서 **백업 항목** 타일은 자격 증명 모음에 보호된 백업 항목 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-176">In the Backup section of the dashboard, the **Backup Items** tile shows the number of backup items protected to the vault.</span></span>

<span data-ttu-id="b1d89-177">백업 항목 타일에서 **파일-폴더** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-177">Click **File-Folders** in the Backup Items tile.</span></span>

![백업 항목 타일](./media/backup-azure-manage-windows-server/backup-items-tile.png)

<span data-ttu-id="b1d89-179">백업 항목 블레이드가 열리고 필터가 나열된 각 특정 백업 항목을 볼 수 있는 파일-폴더로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-179">The Backup Items blade opens with the filter set to File-Folder where you see each specific backup item listed.</span></span>

![백업 항목](./media/backup-azure-manage-windows-server/backup-item-list.png)

<span data-ttu-id="b1d89-181">목록에서 특정 백업 항목을 선택하면 해당 항목에 대한 필수 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-181">If you select a specific backup item from the list, you see the essential details for that item.</span></span>

> [!NOTE]
> <span data-ttu-id="b1d89-182">**설정** 블레이드에서 **보호된 항목 > 백업 항목**을 선택하고 드롭다운 메뉴에서 **파일-폴더**를 선택하여 파일 및 폴더를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-182">From the **Settings** blade, you manage files and folders by selecting **Protected Items > Backup Items** and then selecting **File-Folders** from the drop down menu.</span></span>
>
>

![설정에서 항목 백업](./media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a><span data-ttu-id="b1d89-184">백업 작업 관리</span><span class="sxs-lookup"><span data-stu-id="b1d89-184">Manage Backup jobs</span></span>
<span data-ttu-id="b1d89-185">온-프레미스(온-프레미스 서버가 Azure에 백업하는 경우)와 Azure 백업 둘 다에 대한 백업 작업을 대시보드에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-185">Backup jobs for both on-premises (when the on-premises server is backing up to Azure) and Azure backups are visible in the dashboard.</span></span>

<span data-ttu-id="b1d89-186">대시보드의 백업 섹션에서 백업 작업 타일에 작업 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-186">In the Backup section of the dashboard, the Backup job tile shows the number of jobs:</span></span>

* <span data-ttu-id="b1d89-187">진행 중</span><span class="sxs-lookup"><span data-stu-id="b1d89-187">in progress</span></span>
* <span data-ttu-id="b1d89-188">지난 24시간 동안 실패한 작업.</span><span class="sxs-lookup"><span data-stu-id="b1d89-188">failed in the last 24 hours.</span></span>

<span data-ttu-id="b1d89-189">백업 작업을 관리하려면 **백업 작업** 타일을 클릭하여 백업 작업 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-189">To manage your backup jobs, click the **Backup Jobs** tile, which opens the Backup Jobs blade.</span></span>

![설정에서 항목 백업](./media/backup-azure-manage-windows-server/backup-jobs.png)

<span data-ttu-id="b1d89-191">페이지 맨 위의 **열 선택** 단추로 백업 작업 블레이드에 사용할 수 있는 정보를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-191">You modify the information available in the Backup Jobs blade with the **Choose columns** button at the top of the page.</span></span>

<span data-ttu-id="b1d89-192">**필터** 단추를 사용하여 파일과 폴더 및 Azure 가상 컴퓨터 백업 중에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-192">Use the **Filter** button to select between Files and folders and Azure virtual machine backup.</span></span>

<span data-ttu-id="b1d89-193">백업 파일 및 폴더가 보이지 않으면 페이지 맨 위의 **필터** 단추를 클릭하고 항목 유형 메뉴에서 **파일 및 폴더**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-193">If you don't see your backed up files and folders, click **Filter** button at the top of the page and select **Files and folders** from the Item Type menu.</span></span>

> [!NOTE]
> <span data-ttu-id="b1d89-194">**설정** 블레이드에서 **모니터링 및 보고서 > 작업 > 백업 작업**을 선택한 다음 드롭다운 메뉴에서 **파일-폴더**를 선택하여 백업 작업을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-194">From the **Settings** blade, you manage backup jobs by selecting **Monitoring and Reports > Jobs > Backup Jobs** and then selecting **File-Folders** from the drop down menu.</span></span>
>
>

## <a name="monitor-backup-usage"></a><span data-ttu-id="b1d89-195">백업 사용 모니터링</span><span class="sxs-lookup"><span data-stu-id="b1d89-195">Monitor Backup usage</span></span>
<span data-ttu-id="b1d89-196">대시보드의 백업 섹션에서 백업 사용 타일이 Azure에서 사용한 저장소를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-196">In the Backup section of the dashboard, the Backup Usage tile shows the storage consumed in Azure.</span></span> <span data-ttu-id="b1d89-197">다음에 대한 저장소 사용량이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-197">Storage usage is provided for:</span></span>

* <span data-ttu-id="b1d89-198">자격 증명 모음과 연결된 클라우드 LRS 저장소 사용량</span><span class="sxs-lookup"><span data-stu-id="b1d89-198">Cloud LRS storage usage associated with the vault</span></span>
* <span data-ttu-id="b1d89-199">자격 증명 모음과 연결된 클라우드 GRS 저장소 사용량</span><span class="sxs-lookup"><span data-stu-id="b1d89-199">Cloud GRS storage usage associated with the vault</span></span>

## <a name="manage-your-production-servers"></a><span data-ttu-id="b1d89-200">프로덕션 서버 관리</span><span class="sxs-lookup"><span data-stu-id="b1d89-200">Manage your production servers</span></span>
<span data-ttu-id="b1d89-201">프로덕션 서버를 관리하려면 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-201">To manage your production servers, click **Settings**.</span></span>

<span data-ttu-id="b1d89-202">관리 아래에서 **백업 인프라 > 프로덕션 서버**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-202">Under Manage click **Backup infrastructure > Production Servers**.</span></span>

<span data-ttu-id="b1d89-203">프로덕션 서버 블레이드에 모든 사용 가능한 프로덕션 서버의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-203">The Production Servers blade lists of all your available production servers.</span></span> <span data-ttu-id="b1d89-204">목록에서 서버를 클릭하면 서버 세부 정보가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-204">Click on a server in the list to open the server details.</span></span>

![보호된 항목](./media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-the-azure-backup-agent"></a><span data-ttu-id="b1d89-206">Azure 백업 에이전트 열기</span><span class="sxs-lookup"><span data-stu-id="b1d89-206">Open the Azure Backup agent</span></span>
<span data-ttu-id="b1d89-207">**Microsoft Azure 백업 에이전트**를 엽니다(*Microsoft Azure 백업*에 대한 컴퓨터를 검색하여 찾을 수 있음).</span><span class="sxs-lookup"><span data-stu-id="b1d89-207">Open the **Microsoft Azure Backup agent** (you find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/snap-in-search.png)

<span data-ttu-id="b1d89-209">백업 에이전트 콘솔의 오른쪽에 있는 **작업**에서 다음 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-209">From the **Actions** available at the right of the backup agent console you perform the following management tasks:</span></span>

* <span data-ttu-id="b1d89-210">서버 등록</span><span class="sxs-lookup"><span data-stu-id="b1d89-210">Register Server</span></span>
* <span data-ttu-id="b1d89-211">백업 예약</span><span class="sxs-lookup"><span data-stu-id="b1d89-211">Schedule Backup</span></span>
* <span data-ttu-id="b1d89-212">지금 백업</span><span class="sxs-lookup"><span data-stu-id="b1d89-212">Back Up now</span></span>
* <span data-ttu-id="b1d89-213">속성 변경</span><span class="sxs-lookup"><span data-stu-id="b1d89-213">Change Properties</span></span>

![Microsoft Azure 백업 에이전트 콘솔 작업](./media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> <span data-ttu-id="b1d89-215">**데이터를 복구**하려면 [Windows 서버 또는 Windows 클라이언트 컴퓨터로 파일 복원](backup-azure-restore-windows-server.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1d89-215">To **Recover Data**, see [Restore files to a Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

## <a name="modify-the-backup-schedule"></a><span data-ttu-id="b1d89-216">백업 일정 수정</span><span class="sxs-lookup"><span data-stu-id="b1d89-216">Modify the backup schedule</span></span>
1. <span data-ttu-id="b1d89-217">Microsoft Azure 백업 에이전트에서 **백업 예약**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-217">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/schedule-backup.png)
2. <span data-ttu-id="b1d89-219">**백업 예약 마법사**에서 **백업 항목 또는 시간 변경** 옵션을 선택된 상태로 두고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-219">In the **Schedule Backup Wizard** leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="b1d89-221">항목을 추가하거나 변경하려면 **백업할 항목 선택** 화면에서 **항목 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-221">If you want to add or change items, on the **Select Items to Backup** screen click **Add Items**.</span></span>

    <span data-ttu-id="b1d89-222">마법사의 이 페이지에서 **제외 설정**을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-222">You can also set **Exclusion Settings** from this page in the wizard.</span></span> <span data-ttu-id="b1d89-223">파일 또는 파일 형식을 제외하려면 [제외 설정](#manage-exclusion-settings)추가 절차를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="b1d89-223">If you want to exclude files or file types read the procedure for adding [exclusion settings](#manage-exclusion-settings).</span></span>
4. <span data-ttu-id="b1d89-224">백업할 파일 및 폴더를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-224">Select the files and folders you want to back up and click **Okay**.</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/add-items-modify.png)
5. <span data-ttu-id="b1d89-226">**백업 일정**을 지정하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-226">Specify the **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="b1d89-227">매일(하루에 최대 3회) 또는 매주 백업을 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-227">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Windows Server 백업에 대한 항목](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="b1d89-229">백업 일정을 지정하는 방법은 [문서](backup-azure-backup-cloud-as-tape.md)에 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-229">Specifying the backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

6. <span data-ttu-id="b1d89-230">백업 복사본에 대한 **재방문 주기 정책**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-230">Select the **Retention Policy** for the backup copy and click **Next**.</span></span>

    ![Windows Server 백업에 대한 항목](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. <span data-ttu-id="b1d89-232">**확인** 화면에서 정보를 검토하고 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-232">On the **Confirmation** screen review the information and click **Finish**.</span></span>
8. <span data-ttu-id="b1d89-233">마법사가 **백업 일정** 생성을 완료하면 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-233">Once the wizard finishes creating the **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="b1d89-234">보호를 수정한 후 **작업** 탭으로 이동해 변경 내용이 백업 작업에 반영되는지 확인하여 백업이 올바르게 트리거되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-234">After modifying protection, you can confirm that backups are triggering correctly by going to the **Jobs** tab and confirming that changes are reflected in the backup jobs.</span></span>

## <a name="enable-network-throttling"></a><span data-ttu-id="b1d89-235">네트워크 제한 사용</span><span class="sxs-lookup"><span data-stu-id="b1d89-235">Enable Network Throttling</span></span>

<span data-ttu-id="b1d89-236">Azure 백업 에이전트는 데이터 전송 중에 네트워크 대역폭이 사용되는 방식을 제어할 수 있는 제한 탭을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-236">The Azure Backup agent provides a Throttling tab which allows you to control how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="b1d89-237">근무 시간에 데이터를 백업해야 하는데 백업 프로세스가 다른 인터넷 트래픽을 방해하지 말아야 할 때 유용한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-237">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other internet traffic.</span></span> <span data-ttu-id="b1d89-238">데이터 전송 제한은 백업 및 복원 작업에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-238">Throttling of data transfer applies to back up and restore activities.</span></span>  

<span data-ttu-id="b1d89-239">제한을 사용하려면</span><span class="sxs-lookup"><span data-stu-id="b1d89-239">To enable throttling:</span></span>

1. <span data-ttu-id="b1d89-240">**백업 에이전트**에서 **속성 변경**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-240">In the **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="b1d89-241">**제한 탭에서 **백업 작업에 인터넷 대역폭 사용 제한 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-241">On the **Throttling tab, select **Enable internet bandwidth usage throttling for backup operations**.</span></span>

    ![네트워크 제한](./media/backup-azure-manage-windows-server/throttling-dialog.png)

    <span data-ttu-id="b1d89-243">제한을 사용하도록 설정했으면 **근무 시간** 및 **휴무 시간** 중에 백업 데이터 전송에 허용되는 대역폭을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-243">Once you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="b1d89-244">대역폭 값은 초당 512Kb(Kbps)에서 시작하여 최대 초당 1023Mb(Mbps)까지 증가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-244">The bandwidth values begin at 512 kilobytes per second (Kbps) and can go up to 1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="b1d89-245">또한 **근무 시간**의 시작 및 완료 시간과 근무일로 간주되는 요일을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-245">You can also designate the start and finish for **Work hours**, and which days of the week are considered Work days.</span></span> <span data-ttu-id="b1d89-246">지정된 근무 시간 이외의 시간은 휴무 시간으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-246">The time outside of the designated Work hours is considered to be non-work hours.</span></span>
3. <span data-ttu-id="b1d89-247">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-247">Click **OK**.</span></span>

## <a name="manage-exclusion-settings"></a><span data-ttu-id="b1d89-248">제외 설정 관리</span><span class="sxs-lookup"><span data-stu-id="b1d89-248">Manage exclusion settings</span></span>
1. <span data-ttu-id="b1d89-249">**Microsoft Azure 백업 에이전트**를 엽니다(*Microsoft Azure 백업*에 대한 컴퓨터를 검색하여 찾을 수 있음).</span><span class="sxs-lookup"><span data-stu-id="b1d89-249">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/snap-in-search.png)
2. <span data-ttu-id="b1d89-251">Microsoft Azure 백업 에이전트에서 **백업 예약**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-251">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/schedule-backup.png)
3. <span data-ttu-id="b1d89-253">백업 예약 마법사에서 **백업 항목 또는 시간 변경** 옵션을 선택된 상태로 두고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-253">In the Schedule Backup Wizard leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="b1d89-255">**제외 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-255">Click **Exclusions Settings**.</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/exclusion-settings.png)
5. <span data-ttu-id="b1d89-257">**제외 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-257">Click **Add Exclusion**.</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/add-exclusion.png)
6. <span data-ttu-id="b1d89-259">위치를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-259">Select the location and then, click **OK**.</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/exclusion-location.png)
7. <span data-ttu-id="b1d89-261">**파일 형식** 필드에서 파일 확장명을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-261">Add the file extension in the **File Type** field.</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    <span data-ttu-id="b1d89-263">.mp3 확장명 추가</span><span class="sxs-lookup"><span data-stu-id="b1d89-263">Adding an .mp3 extension</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    <span data-ttu-id="b1d89-265">다른 확장명을 추가하려면 **제외 추가**를 클릭하고 다른 파일 형식 확장명(.jpeg 확장명 추가)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-265">To add another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/exclude-jpg.png)
8. <span data-ttu-id="b1d89-267">모든 확장을 추가했으면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-267">When you've added all the extensions, click **OK**.</span></span>
9. <span data-ttu-id="b1d89-268">**확인 페이지**가 나타날 때까지 **다음**을 클릭하여 백업 예약 마법사를 계속 진행한 후 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-268">Continue through the Schedule Backup Wizard by clicking **Next** until the **Confirmation page**, then click **Finish**.</span></span>

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="b1d89-270">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="b1d89-270">Frequently asked questions</span></span>
<span data-ttu-id="b1d89-271">**Q1. 백업 작업 상태가 Azure 백업 에이전트에서 완료된 것으로 표시되는데, 포털에 즉시 반영되지 않는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="b1d89-271">**Q1. The backup job status shows as completed in the Azure backup agent, why doesn't it get reflected immediately in portal?**</span></span>

<span data-ttu-id="b1d89-272">A1.</span><span class="sxs-lookup"><span data-stu-id="b1d89-272">A1.</span></span> <span data-ttu-id="b1d89-273">백업 작업 상태가 Azure 백업 에이전트와 Azure 포털에 반영될 때까지 최대 15분이 지연됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-273">There is at maximum delay of 15 mins between the backup job status reflected in the Azure backup agent and the Azure portal.</span></span>

<span data-ttu-id="b1d89-274">**Q.2 백업 작업이 실패하는 경우, 경고가 발생할 때까지 얼마나 걸리나요?**</span><span class="sxs-lookup"><span data-stu-id="b1d89-274">**Q.2 When a backup job fails, how long does it take to raise an alert?**</span></span>

<span data-ttu-id="b1d89-275">A.2 경고는 Azure 백업 실패 후 20분 이내에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-275">A.2 An alert is raised within 20 mins of the Azure backup failure.</span></span>

<span data-ttu-id="b1d89-276">**Q3. 알림이 구성된 경우 메일이 전송되지 않는 경우가 있나요?**</span><span class="sxs-lookup"><span data-stu-id="b1d89-276">**Q3. Is there a case where an email won’t be sent if notifications are configured?**</span></span>

<span data-ttu-id="b1d89-277">A3.</span><span class="sxs-lookup"><span data-stu-id="b1d89-277">A3.</span></span> <span data-ttu-id="b1d89-278">아래는 경고 노이즈를 줄이기 위해 알림이 전송되지 않는 경우의 사례입니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-278">Below are the cases when the notification will not be sent in order to reduce the alert noise:</span></span>

* <span data-ttu-id="b1d89-279">알림이 매시간 구성되고 알림이 발생하고 한 시간 이내에 확인되는 경우</span><span class="sxs-lookup"><span data-stu-id="b1d89-279">If notifications are configured hourly and an alert is raised and resolved within the hour</span></span>
* <span data-ttu-id="b1d89-280">작업이 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-280">Job is canceled.</span></span>
* <span data-ttu-id="b1d89-281">원래 백업 작업이 진행 중이므로 두 번째 백업 작업이 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-281">Second backup job failed because original backup job is in progress.</span></span>

## <a name="troubleshooting-monitoring-issues"></a><span data-ttu-id="b1d89-282">모니터링 문제 해결</span><span class="sxs-lookup"><span data-stu-id="b1d89-282">Troubleshooting Monitoring Issues</span></span>
<span data-ttu-id="b1d89-283">**문제:** 포털에서 Azure Backup 에이전트의 작업과 경고가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-283">**Issue:** Jobs and/or alerts from the Azure Backup agent do not appear in the portal.</span></span>

<span data-ttu-id="b1d89-284">**문제 해결 단계:** ```OBRecoveryServicesManagementAgent``` 프로세스에서 Azure Backup 서비스 작업 및 경고 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-284">**Troubleshooting steps:** The process, ```OBRecoveryServicesManagementAgent```, sends the job and alert data to the Azure Backup service.</span></span> <span data-ttu-id="b1d89-285">때때로 이 프로세스가 멈추거나 종료될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-285">Occasionally this process can become stuck or shutdown.</span></span>

1. <span data-ttu-id="b1d89-286">프로세스가 실행되고 있지 않은지 확인하려면 **작업 관리자**를 열고 ```OBRecoveryServicesManagementAgent``` 프로세스가 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-286">To verify the process is not running, open **Task Manager** and check if the ```OBRecoveryServicesManagementAgent``` process is running.</span></span>
2. <span data-ttu-id="b1d89-287">프로세스가 실행되고 있지 않으면 **제어판**을 열고 서비스 목록을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-287">Assuming that the process is not running, open **Control Panel** and browse the list of services.</span></span> <span data-ttu-id="b1d89-288">**Microsoft Azure Recovery Services 관리 에이전트**를 시작하거나 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-288">Start or restart **Microsoft Azure Recovery Services Management Agent**.</span></span>

    <span data-ttu-id="b1d89-289">자세한 내용은 다음 위치에 있는 로그를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d89-289">For further information, browse the logs at:</span></span><br/><span data-ttu-id="b1d89-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` 예:</span><span class="sxs-lookup"><span data-stu-id="b1d89-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` For example:</span></span><br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a><span data-ttu-id="b1d89-291">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b1d89-291">Next steps</span></span>
* [<span data-ttu-id="b1d89-292">Azure에서 Windows Server 또는 Windows 클라이언트 복원</span><span class="sxs-lookup"><span data-stu-id="b1d89-292">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="b1d89-293">Azure 백업에 대한 자세한 내용은 [Azure 백업 개요](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="b1d89-293">To learn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="b1d89-294">[Azure 백업 포럼](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="b1d89-294">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
