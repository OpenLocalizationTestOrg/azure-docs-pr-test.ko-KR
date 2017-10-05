---
title: "Azure Backup Server에서 데이터 복구 | Microsoft Docs"
description: "Recovery Services 자격 증명 모음에 보호해 둔 데이터를 해당 자격 증명 모음에 등록된 모든 Azure Backup Server에서 복구할 수 있습니다."
services: backup
documentationcenter: 
author: nkolli1
manager: shreeshd
editor: 
ms.assetid: a55f8c6b-3627-42e1-9d25-ed3e4ab17b1f
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: adigan;giridham;trinadhk;markgal
ms.openlocfilehash: 688d155b68bc2d76d53f78d251bc2f659582845f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="recover-data-from-azure-backup-server"></a><span data-ttu-id="e64ca-103">Azure Backup Server에서 데이터 복구</span><span class="sxs-lookup"><span data-stu-id="e64ca-103">Recover data from Azure Backup Server</span></span>
<span data-ttu-id="e64ca-104">Azure Backup Server를 사용하여 Recovery Services 자격 증명 모음으로 백업한 데이터를 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-104">You can use Azure Backup Server to recover the data you've backed up to a Recovery Services vault.</span></span> <span data-ttu-id="e64ca-105">이 과정이 Azure Backup Server 관리 콘솔에 통합되며 다른 Azure Backup 구성 요소의 복구 워크플로와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-105">The process for doing so is integrated into the Azure Backup Server management console, and is similar to the recovery workflow for other Azure Backup components.</span></span>

> [!NOTE]
> <span data-ttu-id="e64ca-106">이 문서는 [최신 Azure Backup 에이전트](http://aka.ms/azurebackup_agent)와 결합된 [System Center Data Protection Manager 2012 R2 UR7 이상](https://support.microsoft.com/en-us/kb/3065246)에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-106">This article is applicable for [System Center Data Protection Manager 2012 R2 with UR7 or later] (https://support.microsoft.com/en-us/kb/3065246), combined with the [latest Azure Backup agent](http://aka.ms/azurebackup_agent).</span></span>
>
>

<span data-ttu-id="e64ca-107">Azure Backup Server에서 데이터를 복구하려면</span><span class="sxs-lookup"><span data-stu-id="e64ca-107">To recover data from an Azure Backup Server:</span></span>

1. <span data-ttu-id="e64ca-108">Azure Backup Server 관리 콘솔의 **복구** 탭에서 화면 왼쪽 상단에 있는 **‘외부 DPM 추가’**(화면 왼쪽 맨 위에 있음)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-108">From the **Recovery** tab of the Azure Backup Server management console, click **'Add External DPM'** (at the top left of the screen).</span></span>   
    <span data-ttu-id="e64ca-109">![외부 DPM 추가](./media/backup-azure-alternate-dpm-server/add-external-dpm.png)</span><span class="sxs-lookup"><span data-stu-id="e64ca-109">![Add External DPM](./media/backup-azure-alternate-dpm-server/add-external-dpm.png)</span></span>
2. <span data-ttu-id="e64ca-110">데이터를 복구할 **Azure Backup Server**와 연결된 자격 증명 모음에서 새 **보관 자격 증명**을 다운로드하고, Recovery Services 자격 증명 모음에 등록된 Azure Backup Server 목록에서 Azure Backup Server를 선택하고, 데이터를 복구할 서버에 연결된 **암호화 암호**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-110">Download new **vault credentials** from the vault associated with the **Azure Backup Server** where the data is being recovered, choose the Azure Backup Server from the list of Azure Backup Servers registered with the Recovery Services vault, and provide the **encryption passphrase** associated with the server whose data is being recovered.</span></span>

    ![외부 DPM 자격 증명](./media/backup-azure-alternate-dpm-server/external-dpm-credentials.png)

   > [!NOTE]
   > <span data-ttu-id="e64ca-112">같은 등록 저장소로 연결된 Azure Backup Server끼리만 데이터를 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-112">Only Azure Backup Servers associated with the same registration vault can recover each other’s data.</span></span>
   >
   >

    <span data-ttu-id="e64ca-113">외부 Azure Backup Server가 성공적으로 추가되면 **복구** 탭에서 외부 Azure Backup Server와 로컬 Azure Backup Server의 데이터를 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-113">Once the External Azure Backup Server is successfully added, you can browse the data of the external server and the local Azure Backup Server from the **Recovery** tab.</span></span>
3. <span data-ttu-id="e64ca-114">외부 Azure Backup Server에서 보호하는 사용 가능한 프로덕션 서버의 목록을 찾아보고 적절한 데이터 원본을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-114">Browse the available list of production servers protected by the external Azure Backup Server and select the appropriate data source.</span></span>

    ![외부 DPM 서버 찾아보기](./media/backup-azure-alternate-dpm-server/browse-external-dpm.png)
4. <span data-ttu-id="e64ca-116">**복구 지점** 드롭다운에서 **월 및 연도**를 선택하고 **복구 날짜**에서 복구 지점이 생성된 날짜를, **복구 시간**에서 시간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-116">Select **the month and year** from the **Recovery points** drop down, select the required **Recovery date** for when the recovery point was created, and select the **Recovery time**.</span></span>

    <span data-ttu-id="e64ca-117">아래 창에 파일 및 폴더의 목록이 표시되며 여기서 찾아 어떤 위치로든 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-117">A list of files and folders appears in the bottom pane, which can be browsed and recovered to any location.</span></span>

    ![외부 DPM 서버 복구 지점](./media/backup-azure-alternate-dpm-server/external-dpm-recoverypoint.png)
5. <span data-ttu-id="e64ca-119">적절한 항목을 마우스 오른쪽 단추로 클릭하고 **복구**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-119">Right click the appropriate item and click **Recover**.</span></span>

    ![외부 DPM 복구](./media/backup-azure-alternate-dpm-server/recover.png)
6. <span data-ttu-id="e64ca-121">**복구 선택 사항**을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-121">Review the **Recover Selection**.</span></span> <span data-ttu-id="e64ca-122">복구될 백업 복사본의 날짜와 시간, 백업 복사본이 만들어진 원본을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-122">Verify the data and time of the backup copy being recovered, as well as the source from which the backup copy was created.</span></span> <span data-ttu-id="e64ca-123">선택 항목이 올바르지 않으면 **취소** 를 클릭하여 다시 백업 탭으로 돌아가 적절한 복구 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-123">If the selection is incorrect, click **Cancel** to navigate back to recovery tab to select appropriate recovery point.</span></span> <span data-ttu-id="e64ca-124">선택 항목이 올바르면 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-124">If the selection is correct, click **Next**.</span></span>

    ![외부 DPM 복구 요약](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-summary.png)
7. <span data-ttu-id="e64ca-126">**대체 위치로 복구**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-126">Select **Recover to an alternate location**.</span></span> <span data-ttu-id="e64ca-127">**찾아보기** 를 선택하여 복구할 올바른 위치를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-127">**Browse** to the correct location for the recovery.</span></span>

    ![외부 DPM 복구 대체 위치](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-alternate-location.png)
8. <span data-ttu-id="e64ca-129">**복사본 만들기**, **건너뛰기** 또는 **덮어쓰기** 옵션 중에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-129">Choose the option related to **create copy**, **Skip**, or **Overwrite**.</span></span>

   * <span data-ttu-id="e64ca-130">**복사본 만들기** - 이름이 충돌할 경우 파일의 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-130">**Create copy** - creates a copy of the file if there is a name collision.</span></span>
   * <span data-ttu-id="e64ca-131">**건너뛰기** - 이름이 충돌할 경우 원본 파일을 남기고 파일은 복구하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-131">**Skip** - if there is a name collision, does not recover the file which leaves the original file.</span></span>
   * <span data-ttu-id="e64ca-132">**덮어쓰기** - 이름이 충돌할 경우 기존 파일 복사본을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-132">**Overwrite** - if there is a name collision, overwrites the existing copy of the file.</span></span>

     <span data-ttu-id="e64ca-133">**복원 보안**에서 적절한 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-133">Choose the appropriate option to **Restore security**.</span></span> <span data-ttu-id="e64ca-134">데이터를 복구할 대상 컴퓨터의 보안 설정을 적용하거나 복구 지점이 생성된 시기에 사용된 보안 설정을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-134">You can apply the security settings of the destination computer where the data is being recovered or the security settings that were applicable to product at the time the recovery point was created.</span></span>

     <span data-ttu-id="e64ca-135">복구가 성공적으로 완료되면 **알림**을 전송할지 여부를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-135">Identify whether a **Notification** is sent, once the recovery successfully completes.</span></span>

     ![외부 DPM 복구 알림](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-notifications.png)
9. <span data-ttu-id="e64ca-137">**요약** 화면에 지금까지 선택한 옵션이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-137">The **Summary** screen lists the options chosen so far.</span></span> <span data-ttu-id="e64ca-138">**'복구'**를 클릭하면 데이터가 적절한 온-프레미스 위치에 복구됩니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-138">Once you click **‘Recover’**, the data is recovered to the appropriate on-premises location.</span></span>

    ![외부 DPM 복구 옵션 요약](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-options-summary.png)

   > [!NOTE]
   > <span data-ttu-id="e64ca-140">복구 작업은 Azure Backup Server의 **모니터링** 탭에서 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-140">The recovery job can be monitored in the **Monitoring** tab of the Azure Backup Server.</span></span>
   >
   >

    ![복구 모니터링](./media/backup-azure-alternate-dpm-server/monitoring-recovery.png)
10. <span data-ttu-id="e64ca-142">외부 DPM 서버를 보지 않으려면 **복구** 탭에서 **외부 DPM 지우기**를 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-142">You can click **Clear External DPM** on the **Recovery** tab of the DPM server to remove the view of the external DPM server.</span></span>

    ![외부 DPM 지우기](./media/backup-azure-alternate-dpm-server/clear-external-dpm.png)

## <a name="troubleshooting-error-messages"></a><span data-ttu-id="e64ca-144">오류 메시지 문제 해결</span><span class="sxs-lookup"><span data-stu-id="e64ca-144">Troubleshooting Error Messages</span></span>
| <span data-ttu-id="e64ca-145">번호</span><span class="sxs-lookup"><span data-stu-id="e64ca-145">No.</span></span> | <span data-ttu-id="e64ca-146">오류 메시지</span><span class="sxs-lookup"><span data-stu-id="e64ca-146">Error Message</span></span> | <span data-ttu-id="e64ca-147">문제 해결 단계</span><span class="sxs-lookup"><span data-stu-id="e64ca-147">Troubleshooting steps</span></span> |
|:---:|:--- |:--- |
| <span data-ttu-id="e64ca-148">1.</span><span class="sxs-lookup"><span data-stu-id="e64ca-148">1.</span></span> |<span data-ttu-id="e64ca-149">이 서버는 저장소 자격 증명을 통해 지정된 저장소에 등록되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-149">This server is not registered to the vault specified by the vault credential.</span></span> |<span data-ttu-id="e64ca-150">**원인:** 이 오류는 선택한 보관 자격 증명 파일이 복구를 시도하려는 Azure Backup Server와 연결된 Recovery Services 자격 증명 모음에 속해 있지 않을 때 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-150">**Cause:** This error appears when the vault credential file selected does not belong to the Recovery Services vault associated with Azure Backup Server on which the recovery is attempted.</span></span> <br> <span data-ttu-id="e64ca-151">**해결 방법:** Azure Backup Server가 등록된 Recovery Services 자격 증명 모음에서 보관 자격 증명 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-151">**Resolution:** Download the vault credential file from the Recovery Services vault to which the Azure Backup Server is registered.</span></span> |
| <span data-ttu-id="e64ca-152">2.</span><span class="sxs-lookup"><span data-stu-id="e64ca-152">2.</span></span> |<span data-ttu-id="e64ca-153">복구 가능한 데이터가 없거나 선택한 서버가 DPM 서버가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-153">Either the recoverable data is not available or the selected server is not a DPM server.</span></span> |<span data-ttu-id="e64ca-154">**원인:** Recovery Services 자격 증명 모음에 다른 Azure Backup Server가 등록되지 않았거나, 서버에서 아직 메타데이터를 업로드하지 않았거나, 선택한 서버가 Azure Backup Server가 아닙니다(즉, Windows Server 또는 Windows 클라이언트).</span><span class="sxs-lookup"><span data-stu-id="e64ca-154">**Cause:** There are no other Azure Backup Servers registered to the Recovery Services vault, or the servers have not yet uploaded the metadata, or the selected server is not an Azure Backup Server (aka Windows Server or Windows Client).</span></span> <br> <span data-ttu-id="e64ca-155">**해결 방법:** Recovery Services 자격 증명 모음에 다른 Azure Backup Server가 등록된 경우 최신 Azure Backup 에이전트가 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-155">**Resolution:** If there are other Azure Backup Servers registered to the Recovery Services vault, ensure that the latest Azure Backup agent is installed.</span></span> <br><span data-ttu-id="e64ca-156">다른 Azure Backup Server가 Recovery Services 자격 증명 모음에 등록된 경우, 설치하고 하루 동안 기다린 다음 복구 프로세스를 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="e64ca-156">If there are other Azure Backup Servers registered to the Recovery Services vault, wait for a day after installation to start the recovery process.</span></span> <span data-ttu-id="e64ca-157">야간 작업을 통해 보호된 모든 백업에 대한 메타데이터가 클라우드로 업로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-157">The nightly job will upload the metadata for all the protected backups to cloud.</span></span> <span data-ttu-id="e64ca-158">이제 데이터를 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-158">The data will be available for recovery.</span></span> |
| <span data-ttu-id="e64ca-159">3.</span><span class="sxs-lookup"><span data-stu-id="e64ca-159">3.</span></span> |<span data-ttu-id="e64ca-160">이 저장소에 DPM 서버가 등록되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-160">No other DPM server is registered to this vault.</span></span> |<span data-ttu-id="e64ca-161">**원인:** 복구가 시도된 자격 증명 모음에 등록된 다른 Azure Backup Server가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-161">**Cause:** There are no other Azure Backup Servers  that are registered to the vault from which the recovery is being attempted.</span></span><br><span data-ttu-id="e64ca-162">**해결 방법:** Recovery Services 자격 증명 모음에 다른 Azure Backup Server가 등록된 경우 최신 Azure Backup 에이전트가 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-162">**Resolution:** If there are other Azure Backup Servers registered to the Recovery Services vault, ensure that the latest Azure Backup agent is installed.</span></span><br><span data-ttu-id="e64ca-163">다른 Azure Backup Server가 Recovery Services 자격 증명 모음에 등록된 경우, 설치하고 하루 동안 기다린 다음 복구 프로세스를 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="e64ca-163">If there are other Azure Backup Servers registered to the Recovery Services vault, wait for a day after installation to start the recovery process.</span></span> <span data-ttu-id="e64ca-164">야간 작업을 통해 보호된 모든 백업에 대한 메타데이터가 클라우드로 업로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-164">The nightly job uploads the metadata for all protected backups to cloud.</span></span> <span data-ttu-id="e64ca-165">이제 데이터를 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-165">The data will be available for recovery.</span></span> |
| <span data-ttu-id="e64ca-166">4.</span><span class="sxs-lookup"><span data-stu-id="e64ca-166">4.</span></span> |<span data-ttu-id="e64ca-167">암호화 암호가 다음 서버에 연결된 암호와 일치하지 않습니다. **<server name>**</span><span class="sxs-lookup"><span data-stu-id="e64ca-167">The encryption passphrase provided does not match with passphrase associated with the following server: **<server name>**</span></span> |<span data-ttu-id="e64ca-168">**원인:** 데이터를 복구하려는 Azure Backup Server의 데이터를 암호화하는 데 사용된 암호화 암호가 입력한 암호화 암호와 일치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-168">**Cause:** The encryption passphrase used in the process of encrypting the data from the Azure Backup Server’s data that is being recovered does not match the encryption passphrase provided.</span></span> <span data-ttu-id="e64ca-169">에이전트는 데이터의 암호를 해독할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-169">The agent is unable to decrypt the data.</span></span> <span data-ttu-id="e64ca-170">따라서 복구가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-170">Hence the recovery fails.</span></span><br><span data-ttu-id="e64ca-171">**해결 방법:** 데이터를 복구하려는 Azure Backup Server에 연결된 암호화 암호를 정확하게 입력하세요.</span><span class="sxs-lookup"><span data-stu-id="e64ca-171">**Resolution:** Please provide the exact same encryption passphrase associated with the Azure Backup Server whose data is being recovered.</span></span> |

## <a name="frequently-asked-questions"></a><span data-ttu-id="e64ca-172">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="e64ca-172">Frequently asked questions</span></span>

### <a name="why-cant-i-add-an-external-dpm-server-after-installing-ur7-and-latest-azure-backup-agent"></a><span data-ttu-id="e64ca-173">UR7과 최신 Azure Backup 에이전트를 설치한 후에 외부 DPM 서버를 추가할 수 없는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="e64ca-173">Why can’t I add an external DPM server after installing UR7 and latest Azure Backup agent?</span></span>

<span data-ttu-id="e64ca-174">데이터 원본이 클라우드에 보호되어 있는 DPM 서버의 경우(업데이트 롤업 7 이전의 업데이트 롤업을 사용하여), UR7과 최신 Azure Backup 에이전트를 설치한 다음 하루 이상 기다린 후에 **외부 DPM 서버 추가**를 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-174">For the DPM servers with data sources that are protected to the cloud (by using an update rollup earlier than Update Rollup 7), you must wait at least one day after installing the UR7 and latest Azure Backup agent, to start **Add External DPM server**.</span></span> <span data-ttu-id="e64ca-175">DPM 보호 그룹의 메타데이터가 Azure에 업로드되는 데는 1일의 기간이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-175">The one-day time period is needed to upload the metadata of the DPM protection groups to Azure.</span></span> <span data-ttu-id="e64ca-176">보호 그룹 메타데이터는 야간 작업을 통해 처음으로 업로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-176">Protection group metadata is uploaded the first time through a nightly job.</span></span>

### <a name="what-is-the-minimum-version-of-the-microsoft-azure-recovery-services-agent-needed"></a><span data-ttu-id="e64ca-177">필요한 Microsoft Azure Recovery Services 에이전트의 최소 버전은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="e64ca-177">What is the minimum version of the Microsoft Azure Recovery Services agent needed?</span></span>

<span data-ttu-id="e64ca-178">이 기능을 사용하도록 설정하는 데 필요한 Microsoft Azure Recovery Services 에이전트 또는 Azure Backup 에이전트의 최소 버전은 2.0.8719.0입니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-178">The minimum version of the Microsoft Azure Recovery Services agent, or Azure Backup agent, required to enable this feature is 2.0.8719.0.</span></span>  <span data-ttu-id="e64ca-179">에이전트 버전을 보려면 제어판 **>** 모든 제어판 항목 **>** 프로그램 및 기능 **>** Microsoft Azure Recovery Services 에이전트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e64ca-179">To view the agent's version: open Control Panel **>** All Control Panel items **>** Programs and features **>** Microsoft Azure Recovery Services Agent.</span></span> <span data-ttu-id="e64ca-180">버전이 2.0.8719.0보다 낮은 경우 [최신 Azure Backup 에이전트](https://go.microsoft.com/fwLink/?LinkID=288905)를 다운로드하여 설치하세요.</span><span class="sxs-lookup"><span data-stu-id="e64ca-180">If the version is less than 2.0.8719.0, download and install the [latest Azure Backup agent](https://go.microsoft.com/fwLink/?LinkID=288905).</span></span>

![외부 DPM 지우기](./media/backup-azure-alternate-dpm-server/external-dpm-azurebackupagentversion.png)

## <a name="next-steps"></a><span data-ttu-id="e64ca-182">다음 단계:</span><span class="sxs-lookup"><span data-stu-id="e64ca-182">Next steps:</span></span>
<span data-ttu-id="e64ca-183">•   [Azure Backup FAQ](backup-azure-backup-faq.md)</span><span class="sxs-lookup"><span data-stu-id="e64ca-183">•    [Azure Backup FAQ](backup-azure-backup-faq.md)</span></span>
