---
title: "aaaCreate BizTalk 서비스의 백업을 복원 | Microsoft Docs"
description: "BizTalk 서비스에는 백업 및 복원이 포함되어 있습니다. 자세한 내용은 방법 toocreate 백업을 복원 하 고 백업 대상 결정 합니다. MABS, WABS"
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
ms.openlocfilehash: 32356ad870678fa5fd5bbbbf13d9377188f770a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-backup-and-restore"></a><span data-ttu-id="42479-105">BizTalk 서비스: 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="42479-105">BizTalk Services: Backup and Restore</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="42479-106">Azure BizTalk 서비스에는 백업 및 복원 기능이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42479-106">Azure BizTalk Services includes Backup and Restore capabilities.</span></span> <span data-ttu-id="42479-107">이 항목에서는 toobackup 및 복원 BizTalk 서비스를 사용 하 여 Azure 클래식 포털을 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-107">This topic describes how toobackup and restore BizTalk Services using hello Azure classic portal.</span></span>

<span data-ttu-id="42479-108">Hello를 사용 하 여 BizTalk 서비스를 백업할 수도 있습니다 [BizTalk 서비스 REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584)합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-108">You can also back up BizTalk Services using hello [BizTalk Services REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span></span> 

> [!NOTE]
> <span data-ttu-id="42479-109">하이브리드 연결 hello 버전에 관계 없이, 백업 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="42479-109">Hybrid Connections are NOT backed up, regardless of hello Edition.</span></span> <span data-ttu-id="42479-110">하이브리드 연결을 다시 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-110">You must recreate your hybrid connections.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="42479-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="42479-111">Before you Begin</span></span>
* <span data-ttu-id="42479-112">일부 버전에서는 백업 및 복원을 사용하지 못할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42479-112">Backup and Restore may not be available for all editions.</span></span> <span data-ttu-id="42479-113">[BizTalk 서비스: 버전 차트](biztalk-editions-feature-chart.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="42479-113">See [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>
* <span data-ttu-id="42479-114">Hello Azure 클래식 포털을 사용 하는 요청 시 백업을 만들려면 하거나 예약 된 백업을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42479-114">Using hello Azure classic portal, you can create an On Demand backup or create a scheduled backup.</span></span> 
* <span data-ttu-id="42479-115">콘텐츠 백업 BizTalk 서비스가 동일한 서버 인스턴스나 tooa 복원된 toohello 수 새 BizTalk 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="42479-115">Backup content can be restored toohello same BizTalk Service or tooa new BizTalk Service.</span></span> <span data-ttu-id="42479-116">toorestore hello 이름이 같은 기존 BizTalk 서비스는 hello를 삭제 해야 하는 hello를 사용 하 여 BizTalk 서비스 하 고 hello 이름을 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-116">toorestore hello BizTalk Service using hello same name, hello existing BizTalk Service must be deleted and hello name must be available.</span></span> <span data-ttu-id="42479-117">BizTalk 서비스를 삭제 한 후 동일한 hello에 대 한 원하는 보다 더 긴 시간이 걸릴 수 있습니다 사용할 수 있는 이름 toobe 합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-117">After you delete a BizTalk Service, it can take longer time than wanted for hello same name toobe available.</span></span> <span data-ttu-id="42479-118">Hello 기다릴 수 없는 경우 동일한 이름을 toobe를 사용할 수 있는 지정한 다음 tooa 복원 새 BizTalk 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="42479-118">If you cannot wait for hello same name toobe available, then restore tooa new BizTalk Service.</span></span>
* <span data-ttu-id="42479-119">BizTalk Services 복원된 toohello 수 언어 버전과 동일한 버전 또는 더 높은 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="42479-119">BizTalk Services can be restored toohello same edition or a higher edition.</span></span> <span data-ttu-id="42479-120">BizTalk 서비스 tooa 복원 hello 백업을 수행한 경우에서 낮은 버전에서는 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="42479-120">Restoring BizTalk Services tooa lower edition, from when hello backup was taken, is not supported.</span></span>
  
    <span data-ttu-id="42479-121">예를 들어 Basic Edition 수 hello를 사용 하 여 백업을 복원할 toohello Premium Edition.</span><span class="sxs-lookup"><span data-stu-id="42479-121">For example, a backup using hello Basic Edition can be restored toohello Premium Edition.</span></span> <span data-ttu-id="42479-122">Premium 버전 수 없습니다 hello를 사용 하 여 백업을 복원할 toohello Standard Edition.</span><span class="sxs-lookup"><span data-stu-id="42479-122">A backup using hello Premium Edition cannot be restored toohello Standard Edition.</span></span>
* <span data-ttu-id="42479-123">hello 컨트롤 번호의 toomaintain 연속성 hello EDI 제어 번호는 백업 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42479-123">hello EDI Control numbers are backed up toomaintain continuity of hello control numbers.</span></span> <span data-ttu-id="42479-124">Hello 마지막 백업 이후 메시지를 처리 하는 경우이 백업 콘텐츠를 복원 중복 컨트롤 번호를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42479-124">If messages are processed after hello last backup, restoring this backup content can cause duplicate control numbers.</span></span>
* <span data-ttu-id="42479-125">일괄 처리의 활성 메시지에 있는 경우 hello 일괄 처리 **전에** 백업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-125">If a batch has active messages, process hello batch **before** running a backup.</span></span> <span data-ttu-id="42479-126">필요에 따라 백업을 만들거나 예약된 백업을 만들 때 배치의 메시지는 저장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="42479-126">When creating a backup (as needed or scheduled), messages in batches are never stored.</span></span> 
  
    <span data-ttu-id="42479-127">**일괄 처리의 활성 메시지가 있는 상태에서 백업하면 이러한 메시지는 백업되지 않으므로 손실됩니다.**</span><span class="sxs-lookup"><span data-stu-id="42479-127">**If a backup is taken with active messages in a batch, these messages are not backed up and are therefore lost.**</span></span>
* <span data-ttu-id="42479-128">선택 사항: hello BizTalk 서비스 포털에서에서 모든 관리 작업이 중지.</span><span class="sxs-lookup"><span data-stu-id="42479-128">Optional: In hello BizTalk Services Portal, stop any management operations.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="42479-129">백업 만들기</span><span class="sxs-lookup"><span data-stu-id="42479-129">Create a backup</span></span>
<span data-ttu-id="42479-130">언제든 백업을 만들어 완벽하게 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42479-130">A backup can be taken at any time and is completely controlled by you.</span></span> <span data-ttu-id="42479-131">이 섹션에서는 Azure 클래식 hello를 사용 하 여 hello 단계 toocreate 백업을 포함 하 여 포털:</span><span class="sxs-lookup"><span data-stu-id="42479-131">This section lists hello steps toocreate backups using hello Azure classic portal, including:</span></span>

[<span data-ttu-id="42479-132">주문형 백업</span><span class="sxs-lookup"><span data-stu-id="42479-132">On Demand backup</span></span>](#backupnow)

[<span data-ttu-id="42479-133">백업 예약</span><span class="sxs-lookup"><span data-stu-id="42479-133">Schedule a backup</span></span>](#backupschedule)

#### <span data-ttu-id="42479-134"><a name="backupnow"></a>주문형 백업</span><span class="sxs-lookup"><span data-stu-id="42479-134"><a name="backupnow"></a>On Demand backup</span></span>
1. <span data-ttu-id="42479-135">Hello Azure 클래식 포털에서에서 선택 **BizTalk 서비스**을 다음 선택 hello toobackup BizTalk 서비스 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42479-135">In hello Azure classic portal, select **BizTalk Services**, and then select hello BizTalk Service you want toobackup.</span></span>
2. <span data-ttu-id="42479-136">Hello에 **대시보드** 탭에서 **백업** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42479-136">In hello **Dashboard** tab, select **Back up** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="42479-137">백업 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-137">Enter a backup name.</span></span> <span data-ttu-id="42479-138">예를 들어 *myBizTalkService*BU*날짜*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-138">For example, enter *myBizTalkService*BU*Date*.</span></span>
4. <span data-ttu-id="42479-139">Blob 저장소 계정 및 선택 hello 확인 표시 toostart hello 백업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-139">Choose a blob storage account and select hello checkmark toostart hello backup.</span></span>

<span data-ttu-id="42479-140">Hello 백업이 완료 되 면 hello 저장소 계정에는 컨테이너를 입력 하는 hello 백업 이름으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="42479-140">Once hello backup completes, a container with hello backup name you enter is created in hello storage account.</span></span> <span data-ttu-id="42479-141">이 컨테이너에는 BizTalk 서비스 백업 구성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="42479-141">This container contains your BizTalk Service backup configuration.</span></span>

#### <span data-ttu-id="42479-142"><a name="backupschedule"></a>백업 예약</span><span class="sxs-lookup"><span data-stu-id="42479-142"><a name="backupschedule"></a>Schedule a backup</span></span>
1. <span data-ttu-id="42479-143">Hello Azure 클래식 포털에서에서 선택 **BizTalk 서비스**, 선택 hello tooschedule hello 백업 하 고 hello를 선택 하면 BizTalk 서비스 이름을 **구성** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-143">In hello Azure classic portal, select **BizTalk Services**, select hello BizTalk Service name you want tooschedule hello backup, and then select hello **Configure** tab.</span></span>
2. <span data-ttu-id="42479-144">집합 hello **백업 상태** 너무**자동**합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-144">Set hello **Backup Status** too**Automatic**.</span></span> 
3. <span data-ttu-id="42479-145">선택 hello **저장소 계정** toostore 백업 hello, hello 입력 **주파수** 백업과 기간 tookeep hello 백업을 toocreate hello (**보존 일**):</span><span class="sxs-lookup"><span data-stu-id="42479-145">Select hello **Storage Account** toostore hello backup, enter hello **Frequency** toocreate hello backups, and how long tookeep hello backups (**Retention Days**):</span></span>
   
    ![][AutomaticBU]
   
    <span data-ttu-id="42479-146">**참고 사항**</span><span class="sxs-lookup"><span data-stu-id="42479-146">**Notes**</span></span>     
   
   * <span data-ttu-id="42479-147">**보존 일**, hello 보존 기간 hello 백업 빈도 보다 커야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-147">In **Retention Days**, hello retention period must be greater than hello backup frequency.</span></span>
   * <span data-ttu-id="42479-148">선택 **항상 하나 이상의 백업 유지**hello 보존 기간이 경과 되는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-148">Select **Always keep at least one backup**, even if it is past hello retention period.</span></span>
4. <span data-ttu-id="42479-149">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-149">Select **Save**.</span></span>

<span data-ttu-id="42479-150">예약 된 백업 작업이 실행 될 때 입력 한 hello 저장소 계정에서 컨테이너 (toostore 백업 데이터)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="42479-150">When a scheduled backup job runs, it creates a container (toostore backup data) in hello storage account you entered.</span></span> <span data-ttu-id="42479-151">hello hello 컨테이너의 이름이 *BizTalk 서비스 이름-날짜-시간*합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-151">hello name of hello container is named *BizTalk Service Name-date-time*.</span></span> 

<span data-ttu-id="42479-152">표시 되는 hello BizTalk 서비스 대시보드는 **실패** 상태:</span><span class="sxs-lookup"><span data-stu-id="42479-152">If hello BizTalk Service dashboard shows a **Failed** status:</span></span>

![마지막으로 예약된 백업 상태][BackupStatus] 

<span data-ttu-id="42479-154">hello 링크 hello toohelp 문제를 해결 하는 관리 서비스 작업 로그를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="42479-154">hello link opens hello Management Services Operation Logs toohelp troubleshoot.</span></span> <span data-ttu-id="42479-155">[BizTalk 서비스: 작업 로그를 사용하여 문제 해결](http://go.microsoft.com/fwlink/p/?LinkId=391211)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="42479-155">See [BizTalk Services: Troubleshoot using operation logs](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span></span>

## <a name="restore"></a><span data-ttu-id="42479-156">복원</span><span class="sxs-lookup"><span data-stu-id="42479-156">Restore</span></span>
<span data-ttu-id="42479-157">Hello 또는 hello Azure 클래식 포털에서에서 백업을 복원할 수 있습니다 [BizTalk 서비스 REST API 복원](http://go.microsoft.com/fwlink/p/?LinkID=325582)합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-157">You can restore backups from hello Azure classic portal or from hello [Restore BizTalk Service REST API](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span></span> <span data-ttu-id="42479-158">이 섹션에는 hello 단계 toorestore hello 클래식 포털을 사용 하 여 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-158">This section lists hello steps toorestore using hello classic portal.</span></span>

#### <a name="before-restoring-a-backup"></a><span data-ttu-id="42479-159">복원하기 전에</span><span class="sxs-lookup"><span data-stu-id="42479-159">Before restoring a backup</span></span>
* <span data-ttu-id="42479-160">BizTalk 서비스를 복원하는 동안 새로운 추적, 보관 및 모니터링 저장소를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42479-160">New tracking, archiving, and monitoring stores can be entered while restoring a BizTalk Service.</span></span>
* <span data-ttu-id="42479-161">동일한 EDI 런타임 데이터를 복원 하는 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="42479-161">hello same EDI Runtime data is restored.</span></span> <span data-ttu-id="42479-162">hello EDI 런타임 백업 hello 제어 번호를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-162">hello EDI Runtime backup stores hello control numbers.</span></span> <span data-ttu-id="42479-163">복원 하는 hello 제어 번호는 hello hello 백업 시간에서 시퀀스의입니다.</span><span class="sxs-lookup"><span data-stu-id="42479-163">hello restored control numbers are in sequence from hello time of hello backup.</span></span> <span data-ttu-id="42479-164">Hello 마지막 백업 이후 메시지를 처리 하는 경우이 백업 콘텐츠를 복원 중복 컨트롤 번호를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42479-164">If messages are processed after hello last backup, restoring this backup content can cause duplicate control numbers.</span></span>

#### <a name="restore-a-backup"></a><span data-ttu-id="42479-165">백업 복원</span><span class="sxs-lookup"><span data-stu-id="42479-165">Restore a backup</span></span>
1. <span data-ttu-id="42479-166">Hello Azure 클래식 포털에서에서 선택 **새로** > **응용 프로그램 서비스** > **BizTalk 서비스** > **복원** :</span><span class="sxs-lookup"><span data-stu-id="42479-166">In hello Azure classic portal, select **New** > **App Services** > **BizTalk Service** > **Restore**:</span></span>
   
    ![백업 복원][Restore]
2. <span data-ttu-id="42479-168">**백업 URL**, hello 폴더 아이콘을 선택 하 고 저장소 hello 구성 백업 BizTalk 서비스는 hello Azure 저장소 계정을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-168">In **Backup URL**, select hello folder icon and expand hello Azure storage account that stores hello BizTalk Service configuration backup.</span></span> <span data-ttu-id="42479-169">Hello 컨테이너를 확장 하 고 hello 오른쪽 창에서.txt 파일을 백업에 해당 하는 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-169">Expand hello container and in hello right pane, select hello corresponding back up .txt file.</span></span> 
   <br/><br/>
   <span data-ttu-id="42479-170">**열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-170">Select **Open**.</span></span>
3. <span data-ttu-id="42479-171">Hello에 **복원 BizTalk 서비스** 페이지에서 입력 한 **BizTalk 서비스 이름** hello 확인 **도메인 URL**, **Edition**, 및 **지역** hello 복원 BizTalk 서비스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-171">On hello **Restore BizTalk Service** page, enter a **BizTalk Service Name** and verify hello **Domain URL**, **Edition**, and **Region** for hello restored BizTalk Service.</span></span> <span data-ttu-id="42479-172">**새 SQL 데이터베이스 인스턴스를 만들어** hello 추적 데이터베이스에 대 한:</span><span class="sxs-lookup"><span data-stu-id="42479-172">**Create a new SQL database instance** for hello tracking database:</span></span>
   
    ![][RestoreBizTalkService]
   
    <span data-ttu-id="42479-173">Hello 다음 화살표를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-173">Select hello next arrow.</span></span>
4. <span data-ttu-id="42479-174">Hello SQL 데이터베이스의 hello 이름이 유효한 지 확인 하 고 해당 서버에 대 한 hello SQL 데이터베이스를 만들 위치를 hello 물리적 서버 및 사용자 이름/암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-174">Verify hello name of hello SQL database, enter hello physical server where hello SQL database will be created, and a username/password for that server.</span></span>

    <span data-ttu-id="42479-175">Tooconfigure hello SQL 데이터베이스 버전, 크기 및 기타 속성을 하려는 경우 선택 **고급 데이터베이스 설정 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-175">If you want tooconfigure hello SQL database edition, size, and other properties, select  **Configure Advanced Database Settings**.</span></span> 

    <span data-ttu-id="42479-176">Hello 다음 화살표를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-176">Select hello next arrow.</span></span>

1. <span data-ttu-id="42479-177">새 저장소 계정을 만들거나 hello BizTalk 서비스에 대 한 기존 저장소 계정을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-177">Create a new storage account or enter an existing storage account for hello BizTalk Service.</span></span>
2. <span data-ttu-id="42479-178">Hello, toostart hello 복원 확인 표시를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-178">Select hello checkmark toostart hello restore.</span></span>

<span data-ttu-id="42479-179">Hello 복원을 성공적으로 완료 되 면 새 BizTalk 서비스는 hello BizTalk 서비스 페이지 hello Azure 클래식 포털에서에서 일시 중단된 된 상태에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42479-179">Once hello restoration successfully completes, a new BizTalk Service is listed in a suspended state on hello BizTalk Services page in hello Azure classic portal.</span></span>

### <span data-ttu-id="42479-180"><a name="postrestore"></a>백업을 복원한 후</span><span class="sxs-lookup"><span data-stu-id="42479-180"><a name="postrestore"></a>After restoring a backup</span></span>
<span data-ttu-id="42479-181">hello BizTalk 서비스는 항상 복원는 **Suspended** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="42479-181">hello BizTalk Service is always restored in a **Suspended** state.</span></span> <span data-ttu-id="42479-182">이 상태에서는 hello 새 환경 기능을 포함 하는 전에 구성 변경 내용을 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42479-182">In this state, you can make any configuration changes before hello new environment is functional, including:</span></span>

* <span data-ttu-id="42479-183">Hello Azure BizTalk 서비스 SDK를 사용 하 여 BizTalk 서비스 응용 프로그램을 만든 경우 해당 응용 프로그램 toowork hello 복원 환경에 tootooupdate hello ACS (액세스 제어) 자격 증명을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42479-183">If you created BizTalk Service applications using hello Azure BizTalk Services SDK, you may need tootooupdate hello Access Control (ACS) credentials in those applications toowork with hello restored environment.</span></span>
* <span data-ttu-id="42479-184">BizTalk 서비스 tooreplicate 기존 BizTalk 서비스 환경에 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-184">You restore a BizTalk Service tooreplicate an existing BizTalk Service environment.</span></span> <span data-ttu-id="42479-185">FTP 소스 폴더를 사용 하는 계약 hello 원래 BizTalk 서비스 포털에 구성 된 경우이 상황에서 새로 복원 hello 환경 toouse 다른 소스 FTP 폴더의에서 tooupdate hello 계약을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42479-185">In this situation, if there are agreements configured in hello original BizTalk Services portal that use a source FTP folder, you may need tooupdate hello agreements in hello newly restored environment toouse a different source FTP folder.</span></span> <span data-ttu-id="42479-186">그렇지 않으면 있을 수 있습니다 toopull 시도 하는 두 개의 서로 다른 계약 hello 동일한 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="42479-186">Otherwise, there may be two different agreements trying toopull hello same message.</span></span>
* <span data-ttu-id="42479-187">여러 BizTalk 서비스 환경 toohave 복원한 경우 hello Visual Studio 응용 프로그램, PowerShell cmdlet, REST Api 또는 거래 업체 관리 OM Api에서 올바른 환경 hello 대상 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-187">If you restored toohave multiple BizTalk Service environments, make sure you target hello correct environment in hello Visual Studio applications, PowerShell cmdlets, REST APIs, or Trading Partner Management OM APIs.</span></span>
* <span data-ttu-id="42479-188">새로 복원한 hello BizTalk 서비스 환경에는 것이 좋습니다 tooconfigure 자동화 된 백업 이며</span><span class="sxs-lookup"><span data-stu-id="42479-188">It's a good practice tooconfigure automated backups on hello newly restored BizTalk Service environment.</span></span>

<span data-ttu-id="42479-189">BizTalk 서비스와 선택 hello Azure 클래식 포털 선택 hello에에서 대 한 BizTalk 서비스 toostart hello 복원 **Resume** hello 작업 표시줄에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-189">toostart hello BizTalk Service in hello Azure classic portal, select hello restored BizTalk Service and select **Resume** in hello task bar.</span></span> 

## <a name="what-gets-backed-up"></a><span data-ttu-id="42479-190">백업 대상</span><span class="sxs-lookup"><span data-stu-id="42479-190">What gets backed up</span></span>
<span data-ttu-id="42479-191">백업을 만들 때 hello 다음과 같은 항목이 백업 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42479-191">When a backup is created, hello following items are backed up:</span></span>

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH><span data-ttu-id="42479-192">백업되는 항목</span><span class="sxs-lookup"><span data-stu-id="42479-192">Items backed up</span></span></TH> 
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="42479-193">
 <strong>Azure BizTalk Services 포털</strong></span><span class="sxs-lookup"><span data-stu-id="42479-193">
 <strong>Azure BizTalk Services Portal</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="42479-194">구성 및 런타임</span><span class="sxs-lookup"><span data-stu-id="42479-194">Configuration and Runtime</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="42479-195">파트너 및 프로필 세부 정보</span><span class="sxs-lookup"><span data-stu-id="42479-195">Partner and profile details</span></span></li>
<li><span data-ttu-id="42479-196">파트너 계약</span><span class="sxs-lookup"><span data-stu-id="42479-196">Partner Agreements</span></span></li>
<li><span data-ttu-id="42479-197">배포된 사용자 지정 어셈블리</span><span class="sxs-lookup"><span data-stu-id="42479-197">Custom assemblies deployed</span></span></li>
<li><span data-ttu-id="42479-198">배포된 브리지</span><span class="sxs-lookup"><span data-stu-id="42479-198">Bridges deployed</span></span></li>
<li><span data-ttu-id="42479-199">인증서</span><span class="sxs-lookup"><span data-stu-id="42479-199">Certificates</span></span></li>
<li><span data-ttu-id="42479-200">배포된 변환</span><span class="sxs-lookup"><span data-stu-id="42479-200">Transforms deployed</span></span></li>
<li><span data-ttu-id="42479-201">파이프라인</span><span class="sxs-lookup"><span data-stu-id="42479-201">Pipelines</span></span></li>
<li><span data-ttu-id="42479-202">Hello BizTalk 서비스 포털에서에서 만들고 저장 하는 서식 파일</span><span class="sxs-lookup"><span data-stu-id="42479-202">Templates created and saved in hello BizTalk Services Portal</span></span></li>
<li><span data-ttu-id="42479-203">X12 ST01 및 GS01 매핑</span><span class="sxs-lookup"><span data-stu-id="42479-203">X12 ST01 and GS01 mappings</span></span></li>
<li><span data-ttu-id="42479-204">제어 번호(EDI)</span><span class="sxs-lookup"><span data-stu-id="42479-204">Control numbers (EDI)</span></span></li>
<li><span data-ttu-id="42479-205">AS2 메시지 MIC 값</span><span class="sxs-lookup"><span data-stu-id="42479-205">AS2 Message MIC values</span></span></li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2"><span data-ttu-id="42479-206">
 <strong>Azure BizTalk 서비스</strong></span><span class="sxs-lookup"><span data-stu-id="42479-206">
 <strong>Azure BizTalk Service</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="42479-207">SSL 인증서</span><span class="sxs-lookup"><span data-stu-id="42479-207">SSL Certificate</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="42479-208">SSL 인증서 데이터</span><span class="sxs-lookup"><span data-stu-id="42479-208">SSL Certificate Data</span></span></li>
<li><span data-ttu-id="42479-209">SSL 인증서 암호</span><span class="sxs-lookup"><span data-stu-id="42479-209">SSL Certificate Password</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td><span data-ttu-id="42479-210">BizTalk 서비스 설정</span><span class="sxs-lookup"><span data-stu-id="42479-210">BizTalk Service Settings</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="42479-211">배율 단위 수</span><span class="sxs-lookup"><span data-stu-id="42479-211">Scale unit count</span></span></li>
<li><span data-ttu-id="42479-212">버전</span><span class="sxs-lookup"><span data-stu-id="42479-212">Edition</span></span></li>
<li><span data-ttu-id="42479-213">제품 버전</span><span class="sxs-lookup"><span data-stu-id="42479-213">Product Version</span></span></li>
<li><span data-ttu-id="42479-214">지역/데이터 센터</span><span class="sxs-lookup"><span data-stu-id="42479-214">Region/Datacenter</span></span></li>
<li><span data-ttu-id="42479-215">ACS(액세스 제어 서비스) 네임스페이스 및 키</span><span class="sxs-lookup"><span data-stu-id="42479-215">Access Control Service (ACS) namespace and key</span></span></li>
<li><span data-ttu-id="42479-216">추적 데이터베이스 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="42479-216">Tracking database connection string</span></span></li>
<li><span data-ttu-id="42479-217">보관 저장소 계정 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="42479-217">Archiving Storage account connection string</span></span></li>
<li><span data-ttu-id="42479-218">모니터링 저장소 계정 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="42479-218">Monitoring storage account connection string</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="42479-219">
 <strong>추가 항목</strong></span><span class="sxs-lookup"><span data-stu-id="42479-219">
 <strong>Additional Items</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="42479-220">추적 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="42479-220">Tracking Database</span></span></td> 
<td><span data-ttu-id="42479-221">Hello BizTalk 서비스를 만들면 hello Azure SQL 데이터베이스 서버 및 hello 추적 데이터베이스 이름을 포함 하 여 hello 추적 데이터베이스 세부 정보 입력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42479-221">When hello BizTalk Service is created, hello Tracking Database details are entered, including hello Azure SQL Database Server and hello Tracking Database name.</span></span> <span data-ttu-id="42479-222">hello 추적 데이터베이스를 자동으로 백업 하지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42479-222">hello Tracking Database is not automatically backed up.</span></span>
<br/><br/><span data-ttu-id="42479-223">
<strong>중요</strong></span><span class="sxs-lookup"><span data-stu-id="42479-223">
<strong>Important</strong></span></span><br/>
<span data-ttu-id="42479-224">Hello 추적 데이터베이스 삭제 되 고 복구 데이터베이스 요구를 hello, 이전 백업 존재 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-224">If hello Tracking Database is deleted and hello database needs recovered, a previous backup must exist.</span></span> <span data-ttu-id="42479-225">백업이 없는 경우 hello 추적 데이터베이스 및 해당 데이터는 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="42479-225">If a backup does not exist, hello Tracking Database and its data are not recoverable.</span></span> <span data-ttu-id="42479-226">이 경우 새 추적 데이터베이스를 만들 hello로 동일한 데이터베이스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="42479-226">In this situation, create a new Tracking Database with hello same database name.</span></span> <span data-ttu-id="42479-227">지역에서 복제가 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="42479-227">Geo-Replication is recommended.</span></span></td>
</tr> 
</table>

## <a name="next"></a><span data-ttu-id="42479-228">다음</span><span class="sxs-lookup"><span data-stu-id="42479-228">Next</span></span>
<span data-ttu-id="42479-229">toocreate Azure BizTalk 서비스에서 Azure 클래식 포털, go를 너무 hello[BizTalk 서비스: 프로 비전 사용 하 여 Azure 클래식 포털](http://go.microsoft.com/fwlink/p/?LinkID=302280)합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-229">toocreate Azure BizTalk Services in hello Azure classic portal, go too[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span></span> <span data-ttu-id="42479-230">응용 프로그램을 이동 너무 만들 toostart[Azure BizTalk 서비스](http://go.microsoft.com/fwlink/p/?LinkID=235197)합니다.</span><span class="sxs-lookup"><span data-stu-id="42479-230">toostart creating applications, go too[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="42479-231">참고 항목</span><span class="sxs-lookup"><span data-stu-id="42479-231">See Also</span></span>
* [<span data-ttu-id="42479-232">BizTalk 서비스 백업</span><span class="sxs-lookup"><span data-stu-id="42479-232">Backup BizTalk Service</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [<span data-ttu-id="42479-233">백업에서 BizTalk 서비스 복원</span><span class="sxs-lookup"><span data-stu-id="42479-233">Restore BizTalk Service from Backup</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [<span data-ttu-id="42479-234">BizTalk 서비스: Developer, Basic, Standard 및 Premium Editions 차트</span><span class="sxs-lookup"><span data-stu-id="42479-234">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [<span data-ttu-id="42479-235">BizTalk 서비스: Azure 클래식 포털을 사용하여 프로비전</span><span class="sxs-lookup"><span data-stu-id="42479-235">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [<span data-ttu-id="42479-236">BizTalk 서비스: 프로비저닝 상태 차트</span><span class="sxs-lookup"><span data-stu-id="42479-236">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [<span data-ttu-id="42479-237">BizTalk 서비스: 대시보드, 모니터 및 크기 조정 탭</span><span class="sxs-lookup"><span data-stu-id="42479-237">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [<span data-ttu-id="42479-238">BizTalk 서비스: 제한</span><span class="sxs-lookup"><span data-stu-id="42479-238">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [<span data-ttu-id="42479-239">BizTalk 서비스: 발급자 이름 및 발급자 키</span><span class="sxs-lookup"><span data-stu-id="42479-239">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [<span data-ttu-id="42479-240">Azure BizTalk 서비스 SDK를 hello 어떻게 사용 하 여 시작 합니까</span><span class="sxs-lookup"><span data-stu-id="42479-240">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

