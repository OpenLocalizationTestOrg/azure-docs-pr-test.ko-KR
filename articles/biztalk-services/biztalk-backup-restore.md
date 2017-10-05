---
title: "BizTalk 서비스에서 백업 만들기 및 복원 | Microsoft Docs"
description: "BizTalk 서비스에는 백업 및 복원이 포함되어 있습니다. 백업을 만들고 복원하며 백업 대상을 결정하는 방법에 대해 알아봅니다. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 59f91173-4683-48df-abd5-41262bfce6df
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: c55d1ab124441c42101b4ad60924a9ea28231408
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-backup-and-restore"></a><span data-ttu-id="60eaf-105">BizTalk 서비스: 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="60eaf-105">BizTalk Services: Backup and Restore</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="60eaf-106">Azure BizTalk 서비스에는 백업 및 복원 기능이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-106">Azure BizTalk Services includes Backup and Restore capabilities.</span></span> <span data-ttu-id="60eaf-107">이 토픽에서는 Azure 클래식 포털을 사용하여 BizTalk 서비스를 백업하고 복원하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-107">This topic describes how to backup and restore BizTalk Services using the Azure classic portal.</span></span>

<span data-ttu-id="60eaf-108">[BizTalk 서비스 REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584)를 사용하여 BizTalk 서비스를 백업할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-108">You can also back up BizTalk Services using the [BizTalk Services REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span></span> 

> [!NOTE]
> <span data-ttu-id="60eaf-109">하이브리드 연결은 버전에 상관없이 백업되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-109">Hybrid Connections are NOT backed up, regardless of the Edition.</span></span> <span data-ttu-id="60eaf-110">하이브리드 연결을 다시 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-110">You must recreate your hybrid connections.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="60eaf-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="60eaf-111">Before you Begin</span></span>
* <span data-ttu-id="60eaf-112">일부 버전에서는 백업 및 복원을 사용하지 못할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-112">Backup and Restore may not be available for all editions.</span></span> <span data-ttu-id="60eaf-113">[BizTalk 서비스: 버전 차트](biztalk-editions-feature-chart.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60eaf-113">See [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>
* <span data-ttu-id="60eaf-114">Azure 클래식 포털을 사용하여 주문형 백업 또는 예약된 백업을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-114">Using the Azure classic portal, you can create an On Demand backup or create a scheduled backup.</span></span> 
* <span data-ttu-id="60eaf-115">백업 콘텐츠는 동일한 BizTalk 서비스 또는 새로운 BizTalk 서비스로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-115">Backup content can be restored to the same BizTalk Service or to a new BizTalk Service.</span></span> <span data-ttu-id="60eaf-116">동일한 이름을 사용하여 BizTalk 서비스를 복원하려면 기존 BizTalk 서비스를 삭제해야 하며 이름을 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-116">To restore the BizTalk Service using the same name, the existing BizTalk Service must be deleted and the name must be available.</span></span> <span data-ttu-id="60eaf-117">BizTalk 서비스를 삭제한 후 동일한 이름의 서비스를 사용하려면 시간이 좀 더 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-117">After you delete a BizTalk Service, it can take longer time than wanted for the same name to be available.</span></span> <span data-ttu-id="60eaf-118">동일한 이름의 서비스를 사용할 수 있을 때까지 기다릴 수 없으면 새 BizTalk 서비스로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-118">If you cannot wait for the same name to be available, then restore to a new BizTalk Service.</span></span>
* <span data-ttu-id="60eaf-119">BizTalk 서비스는 동일한 버전 이상으로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-119">BizTalk Services can be restored to the same edition or a higher edition.</span></span> <span data-ttu-id="60eaf-120">BizTalk 서비스를 백업이 만들어진 버전보다 낮은 버전으로 복원할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-120">Restoring BizTalk Services to a lower edition, from when the backup was taken, is not supported.</span></span>
  
    <span data-ttu-id="60eaf-121">예를 들어, Basic Edition을 사용한 백업을 Premium Edition으로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-121">For example, a backup using the Basic Edition can be restored to the Premium Edition.</span></span> <span data-ttu-id="60eaf-122">그러나 Premium Edition을 사용한 백업은 Standard Edition으로 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-122">A backup using the Premium Edition cannot be restored to the Standard Edition.</span></span>
* <span data-ttu-id="60eaf-123">EDI 제어 번호는 제어 번호의 연속성을 유지할 수 있도록 백업됩니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-123">The EDI Control numbers are backed up to maintain continuity of the control numbers.</span></span> <span data-ttu-id="60eaf-124">마지막 백업 후 메시지가 처리되는 경우 이 백업 콘텐츠를 복원하면 제어 번호가 중복될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-124">If messages are processed after the last backup, restoring this backup content can cause duplicate control numbers.</span></span>
* <span data-ttu-id="60eaf-125">일괄 처리에 활성 메시지가 있는 경우 백업을 실행하기 **전에** 일괄 처리를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-125">If a batch has active messages, process the batch **before** running a backup.</span></span> <span data-ttu-id="60eaf-126">필요에 따라 백업을 만들거나 예약된 백업을 만들 때 배치의 메시지는 저장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-126">When creating a backup (as needed or scheduled), messages in batches are never stored.</span></span> 
  
    <span data-ttu-id="60eaf-127">**일괄 처리의 활성 메시지가 있는 상태에서 백업하면 이러한 메시지는 백업되지 않으므로 손실됩니다.**</span><span class="sxs-lookup"><span data-stu-id="60eaf-127">**If a backup is taken with active messages in a batch, these messages are not backed up and are therefore lost.**</span></span>
* <span data-ttu-id="60eaf-128">선택 사항: BizTalk 서비스 포털에서 모든 관리 작업을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-128">Optional: In the BizTalk Services Portal, stop any management operations.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="60eaf-129">백업 만들기</span><span class="sxs-lookup"><span data-stu-id="60eaf-129">Create a backup</span></span>
<span data-ttu-id="60eaf-130">언제든 백업을 만들어 완벽하게 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-130">A backup can be taken at any time and is completely controlled by you.</span></span> <span data-ttu-id="60eaf-131">이 섹션에서는 다음을 비롯해 Azure 클래식 포털을 사용하여 백업을 만드는 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-131">This section lists the steps to create backups using the Azure classic portal, including:</span></span>

[<span data-ttu-id="60eaf-132">주문형 백업</span><span class="sxs-lookup"><span data-stu-id="60eaf-132">On Demand backup</span></span>](#backupnow)

[<span data-ttu-id="60eaf-133">백업 예약</span><span class="sxs-lookup"><span data-stu-id="60eaf-133">Schedule a backup</span></span>](#backupschedule)

#### <span data-ttu-id="60eaf-134"><a name="backupnow"></a>주문형 백업</span><span class="sxs-lookup"><span data-stu-id="60eaf-134"><a name="backupnow"></a>On Demand backup</span></span>
1. <span data-ttu-id="60eaf-135">Azure 클래식 포털에서 **BizTalk 서비스**를 선택한 후 백업할 BizTalk 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-135">In the Azure classic portal, select **BizTalk Services**, and then select the BizTalk Service you want to backup.</span></span>
2. <span data-ttu-id="60eaf-136">**대시보드** 탭에서 페이지 맨 아래에 있는 **백업**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-136">In the **Dashboard** tab, select **Back up** at the bottom of the page.</span></span>
3. <span data-ttu-id="60eaf-137">백업 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-137">Enter a backup name.</span></span> <span data-ttu-id="60eaf-138">예를 들어 *myBizTalkService*BU*날짜*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-138">For example, enter *myBizTalkService*BU*Date*.</span></span>
4. <span data-ttu-id="60eaf-139">Blob 저장소 계정을 선택한 후 확인 표시를 선택하여 백업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-139">Choose a blob storage account and select the checkmark to start the backup.</span></span>

<span data-ttu-id="60eaf-140">백업이 완료되면 입력한 백업 이름의 컨테이너가 저장소 계정에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-140">Once the backup completes, a container with the backup name you enter is created in the storage account.</span></span> <span data-ttu-id="60eaf-141">이 컨테이너에는 BizTalk 서비스 백업 구성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-141">This container contains your BizTalk Service backup configuration.</span></span>

#### <span data-ttu-id="60eaf-142"><a name="backupschedule"></a>백업 예약</span><span class="sxs-lookup"><span data-stu-id="60eaf-142"><a name="backupschedule"></a>Schedule a backup</span></span>
1. <span data-ttu-id="60eaf-143">Azure 클래식 포털에서 **BizTalk Services**를 선택하고 백업을 예약할 BizTalk 서비스 이름을 선택한 후 **구성** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-143">In the Azure classic portal, select **BizTalk Services**, select the BizTalk Service name you want to schedule the backup, and then select the **Configure** tab.</span></span>
2. <span data-ttu-id="60eaf-144">**백업 상태**를 **자동**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-144">Set the **Backup Status** to **Automatic**.</span></span> 
3. <span data-ttu-id="60eaf-145">백업을 저장할 **저장소 계정**을 선택하고 백업을 만들 **빈도** 및 백업을 유지할 기간(**보존 기간(일)**)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-145">Select the **Storage Account** to store the backup, enter the **Frequency** to create the backups, and how long to keep the backups (**Retention Days**):</span></span>
   
    ![][AutomaticBU]
   
    <span data-ttu-id="60eaf-146">**참고 사항**</span><span class="sxs-lookup"><span data-stu-id="60eaf-146">**Notes**</span></span>     
   
   * <span data-ttu-id="60eaf-147">**보존 기간(일)**에서 보존 기간은 백업 빈도보다 커야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-147">In **Retention Days**, the retention period must be greater than the backup frequency.</span></span>
   * <span data-ttu-id="60eaf-148">보존 기간이 지난 경우에도 **항상 하나 이상의 백업 유지**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-148">Select **Always keep at least one backup**, even if it is past the retention period.</span></span>
4. <span data-ttu-id="60eaf-149">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-149">Select **Save**.</span></span>

<span data-ttu-id="60eaf-150">예약된 백업 작업이 실행될 경우 입력한 저장소 계정으로 컨테이너(백업 데이터를 저장할 컨테이너)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-150">When a scheduled backup job runs, it creates a container (to store backup data) in the storage account you entered.</span></span> <span data-ttu-id="60eaf-151">컨테이너 이름은 *BizTalk 서비스 이름-날짜-시간*입니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-151">The name of the container is named *BizTalk Service Name-date-time*.</span></span> 

<span data-ttu-id="60eaf-152">BizTalk 서비스 대시보드에 **실패** 상태가 표시된 경우:</span><span class="sxs-lookup"><span data-stu-id="60eaf-152">If the BizTalk Service dashboard shows a **Failed** status:</span></span>

![마지막으로 예약된 백업 상태][BackupStatus] 

<span data-ttu-id="60eaf-154">이 링크를 클릭하면 문제 해결에 도움이 되는 관리 서비스 작업 로그가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-154">The link opens the Management Services Operation Logs to help troubleshoot.</span></span> <span data-ttu-id="60eaf-155">[BizTalk 서비스: 작업 로그를 사용하여 문제 해결](http://go.microsoft.com/fwlink/p/?LinkId=391211)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60eaf-155">See [BizTalk Services: Troubleshoot using operation logs](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span></span>

## <a name="restore"></a><span data-ttu-id="60eaf-156">복원</span><span class="sxs-lookup"><span data-stu-id="60eaf-156">Restore</span></span>
<span data-ttu-id="60eaf-157">Azure 클래식 포털 또는 [BizTalk 서비스 REST API 복원](http://go.microsoft.com/fwlink/p/?LinkID=325582)에서 백업을 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-157">You can restore backups from the Azure classic portal or from the [Restore BizTalk Service REST API](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span></span> <span data-ttu-id="60eaf-158">이 섹션에서는 클래식 포털을 사용하여 복원하는 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-158">This section lists the steps to restore using the classic portal.</span></span>

#### <a name="before-restoring-a-backup"></a><span data-ttu-id="60eaf-159">복원하기 전에</span><span class="sxs-lookup"><span data-stu-id="60eaf-159">Before restoring a backup</span></span>
* <span data-ttu-id="60eaf-160">BizTalk 서비스를 복원하는 동안 새로운 추적, 보관 및 모니터링 저장소를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-160">New tracking, archiving, and monitoring stores can be entered while restoring a BizTalk Service.</span></span>
* <span data-ttu-id="60eaf-161">동일한 EDI 런타임 데이터가 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-161">The same EDI Runtime data is restored.</span></span> <span data-ttu-id="60eaf-162">EDI 런타임 백업은 제어 번호를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-162">The EDI Runtime backup stores the control numbers.</span></span> <span data-ttu-id="60eaf-163">복원된 제어 번호는 백업 시간부터 차례로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-163">The restored control numbers are in sequence from the time of the backup.</span></span> <span data-ttu-id="60eaf-164">마지막 백업 후 메시지가 처리되는 경우 이 백업 콘텐츠를 복원하면 제어 번호가 중복될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-164">If messages are processed after the last backup, restoring this backup content can cause duplicate control numbers.</span></span>

#### <a name="restore-a-backup"></a><span data-ttu-id="60eaf-165">백업 복원</span><span class="sxs-lookup"><span data-stu-id="60eaf-165">Restore a backup</span></span>
1. <span data-ttu-id="60eaf-166">Azure 클래식 포털에서 **새로 만들기** > **App Services** > **BizTalk 서비스** > **복원**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-166">In the Azure classic portal, select **New** > **App Services** > **BizTalk Service** > **Restore**:</span></span>
   
    ![백업 복원][Restore]
2. <span data-ttu-id="60eaf-168">**URL 백업**에서 폴더 아이콘을 선택하고 BizTalk 서비스 구성 백업을 저장하는 Azure 저장소 계정을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-168">In **Backup URL**, select the folder icon and expand the Azure storage account that stores the BizTalk Service configuration backup.</span></span> <span data-ttu-id="60eaf-169">컨테이너를 확장하고 오른쪽 창에서 해당 백업 .txt 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-169">Expand the container and in the right pane, select the corresponding back up .txt file.</span></span> 
   <br/><br/>
   <span data-ttu-id="60eaf-170">**열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-170">Select **Open**.</span></span>
3. <span data-ttu-id="60eaf-171">**BizTalk 서비스 복원** 페이지에서 **BizTalk 서비스 이름**을 입력하고 복원된 BizTalk 서비스의 **도메인 URL**, **버전** 및 **지역**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-171">On the **Restore BizTalk Service** page, enter a **BizTalk Service Name** and verify the **Domain URL**, **Edition**, and **Region** for the restored BizTalk Service.</span></span> <span data-ttu-id="60eaf-172">**새 SQL 데이터베이스 인스턴스 만들기** 를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-172">**Create a new SQL database instance** for the tracking database:</span></span>
   
    ![][RestoreBizTalkService]
   
    <span data-ttu-id="60eaf-173">다음 화살표를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-173">Select the next arrow.</span></span>
4. <span data-ttu-id="60eaf-174">SQL 데이터베이스의 이름을 확인하고, SQL 데이터베이스를 만들 실제 서버와 해당 서버의 사용자 이름/암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-174">Verify the name of the SQL database, enter the physical server where the SQL database will be created, and a username/password for that server.</span></span>

    <span data-ttu-id="60eaf-175">SQL 데이터베이스 버전, 크기 및 기타 속성을 구성하려면 **고급 데이터베이스 설정 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-175">If you want to configure the SQL database edition, size, and other properties, select  **Configure Advanced Database Settings**.</span></span> 

    <span data-ttu-id="60eaf-176">다음 화살표를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-176">Select the next arrow.</span></span>

1. <span data-ttu-id="60eaf-177">BizTalk 서비스에 대한 새 저장소 계정을 만들거나 기존 저장소 계정을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-177">Create a new storage account or enter an existing storage account for the BizTalk Service.</span></span>
2. <span data-ttu-id="60eaf-178">확인 표시를 선택하여 복원을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-178">Select the checkmark to start the restore.</span></span>

<span data-ttu-id="60eaf-179">복원이 완료되면 Azure 클래식 포털의 BizTalk 서비스 페이지에서 새로운 BizTalk 서비스가 일시 중단 상태로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-179">Once the restoration successfully completes, a new BizTalk Service is listed in a suspended state on the BizTalk Services page in the Azure classic portal.</span></span>

### <span data-ttu-id="60eaf-180"><a name="postrestore"></a>백업을 복원한 후</span><span class="sxs-lookup"><span data-stu-id="60eaf-180"><a name="postrestore"></a>After restoring a backup</span></span>
<span data-ttu-id="60eaf-181">BizTalk 서비스는 항상 **일시 중단** 상태로 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-181">The BizTalk Service is always restored in a **Suspended** state.</span></span> <span data-ttu-id="60eaf-182">이 상태에서는 새 환경을 작동하기 전에 다음을 비롯한 구성 변경을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-182">In this state, you can make any configuration changes before the new environment is functional, including:</span></span>

* <span data-ttu-id="60eaf-183">Azure BizTalk 서비스 SDK를 사용하여 BizTalk 서비스 응용 프로그램을 만든 경우 복원된 환경에서 작동할 응용 프로그램에서 ACS(액세스 제어) 자격 증명을 업데이트해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-183">If you created BizTalk Service applications using the Azure BizTalk Services SDK, you may need to to update the Access Control (ACS) credentials in those applications to work with the restored environment.</span></span>
* <span data-ttu-id="60eaf-184">기존 BizTalk 서비스 환경을 복제하도록 BizTalk 서비스를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-184">You restore a BizTalk Service to replicate an existing BizTalk Service environment.</span></span> <span data-ttu-id="60eaf-185">이 경우 원래 BizTalk 서비스 포털에 원본 FTP 폴더를 사용하는 계약이 구성되어 있으면 새로 복원한 환경에서 다른 원본 FTP 폴더를 사용하도록 계약을 업데이트해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-185">In this situation, if there are agreements configured in the original BizTalk Services portal that use a source FTP folder, you may need to update the agreements in the newly restored environment to use a different source FTP folder.</span></span> <span data-ttu-id="60eaf-186">그렇지 않으면 두 가지 계약에서 동일한 메시지를 가져오려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-186">Otherwise, there may be two different agreements trying to pull the same message.</span></span>
* <span data-ttu-id="60eaf-187">여러 BizTalk 서비스 환경을 유지하도록 복원한 경우 Visual Studio 응용 프로그램, PowerShell cmdlet, REST API 또는 거래 업체 관리 도구 OM API에서 올바른 환경을 대상으로 하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-187">If you restored to have multiple BizTalk Service environments, make sure you target the correct environment in the Visual Studio applications, PowerShell cmdlets, REST APIs, or Trading Partner Management OM APIs.</span></span>
* <span data-ttu-id="60eaf-188">새로 복원한 BizTalk 서비스 환경에서 자동 백업을 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-188">It's a good practice to configure automated backups on the newly restored BizTalk Service environment.</span></span>

<span data-ttu-id="60eaf-189">Azure 클래식 포털에서 BizTalk 서비스를 시작하려면 복원된 BizTalk 서비스를 선택한 후 작업 표시줄에서 **계속** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-189">To start the BizTalk Service in the Azure classic portal, select the restored BizTalk Service and select **Resume** in the task bar.</span></span> 

## <a name="what-gets-backed-up"></a><span data-ttu-id="60eaf-190">백업 대상</span><span class="sxs-lookup"><span data-stu-id="60eaf-190">What gets backed up</span></span>
<span data-ttu-id="60eaf-191">백업을 만들 때 다음 항목이 백업됩니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-191">When a backup is created, the following items are backed up:</span></span>

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH><span data-ttu-id="60eaf-192">백업되는 항목</span><span class="sxs-lookup"><span data-stu-id="60eaf-192">Items backed up</span></span></TH> 
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="60eaf-193">
 <strong>Azure BizTalk Services 포털</strong></span><span class="sxs-lookup"><span data-stu-id="60eaf-193">
 <strong>Azure BizTalk Services Portal</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="60eaf-194">구성 및 런타임</span><span class="sxs-lookup"><span data-stu-id="60eaf-194">Configuration and Runtime</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="60eaf-195">파트너 및 프로필 세부 정보</span><span class="sxs-lookup"><span data-stu-id="60eaf-195">Partner and profile details</span></span></li>
<li><span data-ttu-id="60eaf-196">파트너 계약</span><span class="sxs-lookup"><span data-stu-id="60eaf-196">Partner Agreements</span></span></li>
<li><span data-ttu-id="60eaf-197">배포된 사용자 지정 어셈블리</span><span class="sxs-lookup"><span data-stu-id="60eaf-197">Custom assemblies deployed</span></span></li>
<li><span data-ttu-id="60eaf-198">배포된 브리지</span><span class="sxs-lookup"><span data-stu-id="60eaf-198">Bridges deployed</span></span></li>
<li><span data-ttu-id="60eaf-199">인증서</span><span class="sxs-lookup"><span data-stu-id="60eaf-199">Certificates</span></span></li>
<li><span data-ttu-id="60eaf-200">배포된 변환</span><span class="sxs-lookup"><span data-stu-id="60eaf-200">Transforms deployed</span></span></li>
<li><span data-ttu-id="60eaf-201">파이프라인</span><span class="sxs-lookup"><span data-stu-id="60eaf-201">Pipelines</span></span></li>
<li><span data-ttu-id="60eaf-202">BizTalk 서비스 포털에서 만들어지고 저장된 템플릿</span><span class="sxs-lookup"><span data-stu-id="60eaf-202">Templates created and saved in the BizTalk Services Portal</span></span></li>
<li><span data-ttu-id="60eaf-203">X12 ST01 및 GS01 매핑</span><span class="sxs-lookup"><span data-stu-id="60eaf-203">X12 ST01 and GS01 mappings</span></span></li>
<li><span data-ttu-id="60eaf-204">제어 번호(EDI)</span><span class="sxs-lookup"><span data-stu-id="60eaf-204">Control numbers (EDI)</span></span></li>
<li><span data-ttu-id="60eaf-205">AS2 메시지 MIC 값</span><span class="sxs-lookup"><span data-stu-id="60eaf-205">AS2 Message MIC values</span></span></li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2"><span data-ttu-id="60eaf-206">
 <strong>Azure BizTalk 서비스</strong></span><span class="sxs-lookup"><span data-stu-id="60eaf-206">
 <strong>Azure BizTalk Service</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="60eaf-207">SSL 인증서</span><span class="sxs-lookup"><span data-stu-id="60eaf-207">SSL Certificate</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="60eaf-208">SSL 인증서 데이터</span><span class="sxs-lookup"><span data-stu-id="60eaf-208">SSL Certificate Data</span></span></li>
<li><span data-ttu-id="60eaf-209">SSL 인증서 암호</span><span class="sxs-lookup"><span data-stu-id="60eaf-209">SSL Certificate Password</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td><span data-ttu-id="60eaf-210">BizTalk 서비스 설정</span><span class="sxs-lookup"><span data-stu-id="60eaf-210">BizTalk Service Settings</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="60eaf-211">배율 단위 수</span><span class="sxs-lookup"><span data-stu-id="60eaf-211">Scale unit count</span></span></li>
<li><span data-ttu-id="60eaf-212">버전</span><span class="sxs-lookup"><span data-stu-id="60eaf-212">Edition</span></span></li>
<li><span data-ttu-id="60eaf-213">제품 버전</span><span class="sxs-lookup"><span data-stu-id="60eaf-213">Product Version</span></span></li>
<li><span data-ttu-id="60eaf-214">지역/데이터 센터</span><span class="sxs-lookup"><span data-stu-id="60eaf-214">Region/Datacenter</span></span></li>
<li><span data-ttu-id="60eaf-215">ACS(액세스 제어 서비스) 네임스페이스 및 키</span><span class="sxs-lookup"><span data-stu-id="60eaf-215">Access Control Service (ACS) namespace and key</span></span></li>
<li><span data-ttu-id="60eaf-216">추적 데이터베이스 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="60eaf-216">Tracking database connection string</span></span></li>
<li><span data-ttu-id="60eaf-217">보관 저장소 계정 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="60eaf-217">Archiving Storage account connection string</span></span></li>
<li><span data-ttu-id="60eaf-218">모니터링 저장소 계정 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="60eaf-218">Monitoring storage account connection string</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="60eaf-219">
 <strong>추가 항목</strong></span><span class="sxs-lookup"><span data-stu-id="60eaf-219">
 <strong>Additional Items</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="60eaf-220">추적 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="60eaf-220">Tracking Database</span></span></td> 
<td><span data-ttu-id="60eaf-221">BizTalk 서비스를 만들 때 Azure SQL 데이터베이스 서버 및 추적 데이터베이스 이름을 포함한 추적 데이터베이스 세부 정보가 입력됩니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-221">When the BizTalk Service is created, the Tracking Database details are entered, including the Azure SQL Database Server and the Tracking Database name.</span></span> <span data-ttu-id="60eaf-222">추적 데이터베이스는 자동으로 백업되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-222">The Tracking Database is not automatically backed up.</span></span>
<br/><br/><span data-ttu-id="60eaf-223">
<strong>중요</strong></span><span class="sxs-lookup"><span data-stu-id="60eaf-223">
<strong>Important</strong></span></span><br/>
<span data-ttu-id="60eaf-224">추적 데이터베이스가 삭제되어 데이터베이스를 복구해야 하는 경우 이전 백업이 존재해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-224">If the Tracking Database is deleted and the database needs recovered, a previous backup must exist.</span></span> <span data-ttu-id="60eaf-225">백업이 존재하지 않는 경우 추적 데이터베이스 및 데이터를 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-225">If a backup does not exist, the Tracking Database and its data are not recoverable.</span></span> <span data-ttu-id="60eaf-226">이런 경우에는 동일한 데이터베이스 이름으로 새로운 추적 데이터베이스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-226">In this situation, create a new Tracking Database with the same database name.</span></span> <span data-ttu-id="60eaf-227">지역에서 복제가 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="60eaf-227">Geo-Replication is recommended.</span></span></td>
</tr> 
</table>

## <a name="next"></a><span data-ttu-id="60eaf-228">다음</span><span class="sxs-lookup"><span data-stu-id="60eaf-228">Next</span></span>
<span data-ttu-id="60eaf-229">Azure 클래식 포털에서 Azure BizTalk 서비스를 만들려면 [BizTalk 서비스: Azure 클래식 포털을 사용하여 프로비전](http://go.microsoft.com/fwlink/p/?LinkID=302280)으로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="60eaf-229">To create Azure BizTalk Services in the Azure classic portal, go to [BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span></span> <span data-ttu-id="60eaf-230">응용 프로그램을 만들려면 [Azure BizTalk 서비스](http://go.microsoft.com/fwlink/p/?LinkID=235197)로 이동하십시오.</span><span class="sxs-lookup"><span data-stu-id="60eaf-230">To start creating applications, go to [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="60eaf-231">참고 항목</span><span class="sxs-lookup"><span data-stu-id="60eaf-231">See Also</span></span>
* [<span data-ttu-id="60eaf-232">BizTalk 서비스 백업</span><span class="sxs-lookup"><span data-stu-id="60eaf-232">Backup BizTalk Service</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [<span data-ttu-id="60eaf-233">백업에서 BizTalk 서비스 복원</span><span class="sxs-lookup"><span data-stu-id="60eaf-233">Restore BizTalk Service from Backup</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [<span data-ttu-id="60eaf-234">BizTalk 서비스: Developer, Basic, Standard 및 Premium Editions 차트</span><span class="sxs-lookup"><span data-stu-id="60eaf-234">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [<span data-ttu-id="60eaf-235">BizTalk 서비스: Azure 클래식 포털을 사용하여 프로비전</span><span class="sxs-lookup"><span data-stu-id="60eaf-235">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [<span data-ttu-id="60eaf-236">BizTalk 서비스: 프로비저닝 상태 차트</span><span class="sxs-lookup"><span data-stu-id="60eaf-236">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [<span data-ttu-id="60eaf-237">BizTalk 서비스: 대시보드, 모니터 및 크기 조정 탭</span><span class="sxs-lookup"><span data-stu-id="60eaf-237">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [<span data-ttu-id="60eaf-238">BizTalk 서비스: 제한</span><span class="sxs-lookup"><span data-stu-id="60eaf-238">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [<span data-ttu-id="60eaf-239">BizTalk 서비스: 발급자 이름 및 발급자 키</span><span class="sxs-lookup"><span data-stu-id="60eaf-239">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [<span data-ttu-id="60eaf-240">Azure BizTalk 서비스 SDK로 시작하는 방법</span><span class="sxs-lookup"><span data-stu-id="60eaf-240">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

