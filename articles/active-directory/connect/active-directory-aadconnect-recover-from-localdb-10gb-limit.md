---
title: "Azure AD Connect: 어떻게 10GB LocalDB에서 toorecover 제한 문제 | Microsoft Docs"
description: "이 항목에서는 방법을 toorecover Azure AD Connect 동기화 서비스 LocalDB 10GB를 발견 한 경우 설명 문제를 제한 합니다."
services: active-directory
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 41d081af-ed89-4e17-be34-14f7e80ae358
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: 7b8ce6e19b68837639017bb0315eda4b924d525a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-how-toorecover-from-localdb-10-gb-limit"></a><span data-ttu-id="17451-103">Azure AD Connect: 어떻게 toorecover LocalDB 10GB 제한에서</span><span class="sxs-lookup"><span data-stu-id="17451-103">Azure AD Connect: How toorecover from LocalDB 10-GB limit</span></span>
<span data-ttu-id="17451-104">Azure AD Connect SQL Server 데이터베이스 toostore id 데이터를 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-104">Azure AD Connect requires a SQL Server database toostore identity data.</span></span> <span data-ttu-id="17451-105">Hello 기본 Azure AD Connect와 함께 설치 된 SQL Server 2012 Express LocalDB를 사용 하거나 사용자 고유의 전체 SQL을 사용 하 여 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17451-105">You can either use hello default SQL Server 2012 Express LocalDB installed with Azure AD Connect or use your own full SQL.</span></span> <span data-ttu-id="17451-106">SQL Server Express는 10GB 크기 제한을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-106">SQL Server Express imposes a 10-GB size limit.</span></span> <span data-ttu-id="17451-107">LocalDB를 사용하고 이 제한에 도달하는 경우 Azure AD Connect 동기화 서비스는 더 이상 제대로 시작하거나 동기화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="17451-107">When using LocalDB and this limit is reached, Azure AD Connect Synchronization Service can no longer start or synchronize properly.</span></span> <span data-ttu-id="17451-108">이 문서는 hello 복구 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-108">This article provides hello recovery steps.</span></span>

## <a name="symptoms"></a><span data-ttu-id="17451-109">증상</span><span class="sxs-lookup"><span data-stu-id="17451-109">Symptoms</span></span>
<span data-ttu-id="17451-110">두 가지 일반적인 증상이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17451-110">There are two common symptoms:</span></span>

* <span data-ttu-id="17451-111">Azure AD Connect 동기화 Service **실행 되 고** 하지만 실패와 toosynchronize *"중지 됨-데이터베이스-디스크-full"을* 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="17451-111">Azure AD Connect Synchronization Service **is running** but fails toosynchronize with *“stopped-database-disk-full”* error.</span></span>

* <span data-ttu-id="17451-112">Azure AD Connect 동기화 Service **가 없습니다 toostart**합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-112">Azure AD Connect Synchronization Service **is unable toostart**.</span></span> <span data-ttu-id="17451-113">6323 이벤트 및 오류 메시지와 함께 실패 toostart hello 서비스를 만들려고 하면 *"hello 서버 오류가 발생 했습니다 SQL Server 디스크 공간이 부족 하기 때문에."*</span><span class="sxs-lookup"><span data-stu-id="17451-113">When you attempt toostart hello service, it fails with event 6323 and error message *"hello server encountered an error because SQL Server is out of disk space."*</span></span>

## <a name="short-term-recovery-steps"></a><span data-ttu-id="17451-114">단기 복구 단계</span><span class="sxs-lookup"><span data-stu-id="17451-114">Short-term recovery steps</span></span>
<span data-ttu-id="17451-115">이 섹션에서는 Azure AD Connect 동기화 Service tooresume 작업에 필요한 hello 단계 tooreclaim DB 공간을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-115">This section provides hello steps tooreclaim DB space required for Azure AD Connect Synchronization Service tooresume operation.</span></span> <span data-ttu-id="17451-116">hello 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="17451-116">hello steps include:</span></span>
1. [<span data-ttu-id="17451-117">Hello 동기화 서비스 상태 확인</span><span class="sxs-lookup"><span data-stu-id="17451-117">Determine hello Synchronization Service status</span></span>](#determine-the-synchronization-service-status)
2. [<span data-ttu-id="17451-118">Hello 데이터베이스 축소</span><span class="sxs-lookup"><span data-stu-id="17451-118">Shrink hello database</span></span>](#shrink-the-database)
3. [<span data-ttu-id="17451-119">실행 기록 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="17451-119">Delete run history data</span></span>](#delete-run-history-data)
4. [<span data-ttu-id="17451-120">실행 기록 데이터에 대한 보존 기간 단축</span><span class="sxs-lookup"><span data-stu-id="17451-120">Shorten retention period for run history data</span></span>](#shorten-retention-period-for-run-history-data)

### <a name="determine-hello-synchronization-service-status"></a><span data-ttu-id="17451-121">Hello 동기화 서비스 상태 확인</span><span class="sxs-lookup"><span data-stu-id="17451-121">Determine hello Synchronization Service status</span></span>
<span data-ttu-id="17451-122">첫째, 여부 여전히 hello 동기화 서비스가 실행 중인지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-122">First, determine whether hello Synchronization Service is still running or not:</span></span>

1. <span data-ttu-id="17451-123">관리자 권한으로 Azure AD Connect 서버 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-123">Log in tooyour Azure AD Connect server as administrator.</span></span>

2. <span data-ttu-id="17451-124">너무 이동**서비스 제어 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-124">Go too**Service Control Manager**.</span></span>

3. <span data-ttu-id="17451-125">Hello 상태를 확인 **Microsoft Azure AD Sync**합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-125">Check hello status of **Microsoft Azure AD Sync**.</span></span>


4. <span data-ttu-id="17451-126">실행 중인 경우 중지 하지 않거나 hello 서비스를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-126">If it is running, do not stop or restart hello service.</span></span> <span data-ttu-id="17451-127">Skip [축소 hello 데이터베이스](#shrink-the-database) 단계를 너무 이동[실행 기록 데이터 삭제](#delete-run-history-data) 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="17451-127">Skip [Shrink hello database](#shrink-the-database) step and go too[Delete run history data](#delete-run-history-data) step.</span></span>

5. <span data-ttu-id="17451-128">실행 되지 않는 경우 toostart hello 서비스를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="17451-128">If it is not running, try toostart hello service.</span></span> <span data-ttu-id="17451-129">Hello 서비스가 시작 되 면 건너뛸 [축소 hello 데이터베이스](#shrink-the-database) 단계를 너무 이동[실행 기록 데이터 삭제](#delete-run-history-data) 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="17451-129">If hello service starts successfully, skip [Shrink hello database](#shrink-the-database) step and go too[Delete run history data](#delete-run-history-data) step.</span></span> <span data-ttu-id="17451-130">그렇지 않은 경우 계속 [축소 hello 데이터베이스](#shrink-the-database) 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="17451-130">Otherwise, continue with [Shrink hello database](#shrink-the-database) step.</span></span>

### <a name="shrink-hello-database"></a><span data-ttu-id="17451-131">Hello 데이터베이스 축소</span><span class="sxs-lookup"><span data-stu-id="17451-131">Shrink hello database</span></span>
<span data-ttu-id="17451-132">Hello 축소 작업 toofree 충분 한 DB 공간 toostart hello 동기화 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-132">Use hello Shrink operation toofree up enough DB space toostart hello Synchronization Service.</span></span> <span data-ttu-id="17451-133">Hello 데이터베이스에 있는 공백이 제거 하 여 DB 공간을 확보 합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-133">It frees up DB space by removing whitespaces in hello database.</span></span> <span data-ttu-id="17451-134">항상 공백을 복구할 수 있다고 보장되지 않으므로 이 단계가 최선적입니다.</span><span class="sxs-lookup"><span data-stu-id="17451-134">This step is best-effort as it is not guaranteed that you can always recover space.</span></span> <span data-ttu-id="17451-135">이 문서를 참조 하는 축소 작업에 대해 자세히 toolearn [데이터베이스 축소](https://msdn.microsoft.com/library/ms189035.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-135">toolearn more about Shrink operation, read this article [Shrink a database](https://msdn.microsoft.com/library/ms189035.aspx).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="17451-136">동기화 서비스 toorun hello를 얻을 수 있는 경우이 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="17451-136">Skip this step if you can get hello Synchronization Service toorun.</span></span> <span data-ttu-id="17451-137">Tooincreased 조각화 인해 toopoor 성능 시킬 수 있으므로 tooshrink hello SQL DB 하지 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="17451-137">It is not recommended tooshrink hello SQL DB as it can lead toopoor performance due tooincreased fragmentation.</span></span>

<span data-ttu-id="17451-138">hello Azure AD Connect에 대 한 생성 hello 데이터베이스 이름이 **ADSync**합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-138">hello name of hello database created for Azure AD Connect is **ADSync**.</span></span> <span data-ttu-id="17451-139">tooperform 축소 작업으로 hello sysadmin 또는 hello 데이터베이스의 DBO에 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-139">tooperform a Shrink operation, you must log in either as hello sysadmin or DBO of hello database.</span></span> <span data-ttu-id="17451-140">Azure AD Connect 설치 하는 동안 다음 계정 hello sysadmin 권한이 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17451-140">During Azure AD Connect installation, hello following accounts are granted sysadmin rights:</span></span>
* <span data-ttu-id="17451-141">로컬 관리자</span><span class="sxs-lookup"><span data-stu-id="17451-141">Local Administrators</span></span>
* <span data-ttu-id="17451-142">사용 되는 toorun Azure AD Connect 설치 했던 hello 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="17451-142">hello user account that was used toorun Azure AD Connect installation.</span></span>
* <span data-ttu-id="17451-143">Azure AD 동기화 서비스 연결의 컨텍스트를 운영 하는 hello로 사용 되는 동기화 서비스 계정 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="17451-143">hello Sync Service account that is used as hello operating context of Azure AD Connect Synchronization Service.</span></span>
* <span data-ttu-id="17451-144">hello 로컬 설치 중에 만들어진 ADSyncAdmins 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="17451-144">hello local group ADSyncAdmins that was created during installation.</span></span>

1. <span data-ttu-id="17451-145">복사 하 여 hello 데이터베이스를 백업 **ADSync.mdf** 및 **ADSync_log.ldf** 아래에 있는 파일 `%ProgramFiles%\program files\Microsoft Azure AD Sync\Data` tooa 안전한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="17451-145">Back up hello database by copying **ADSync.mdf** and **ADSync_log.ldf** files located under `%ProgramFiles%\program files\Microsoft Azure AD Sync\Data` tooa safe location.</span></span>

2. <span data-ttu-id="17451-146">새 PowerShell 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-146">Start a new PowerShell session.</span></span>

3. <span data-ttu-id="17451-147">Toofolder 이동 `%ProgramFiles%\Program Files\Microsoft SQL Server\110\Tools\Binn`합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-147">Navigate toofolder `%ProgramFiles%\Program Files\Microsoft SQL Server\110\Tools\Binn`.</span></span>

4. <span data-ttu-id="17451-148">시작 **sqlcmd** hello 명령을 실행 하 여 유틸리티 `./SQLCMD.EXE -S “(localdb)\.\ADSync” -U <Username> -P <Password>`sysadmin의 hello 자격 증명을 사용 하 여, 또는 데이터베이스 DBO hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-148">Start **sqlcmd** utility by running hello command `./SQLCMD.EXE -S “(localdb)\.\ADSync” -U <Username> -P <Password>`, using hello credential of a sysadmin or hello database DBO.</span></span>

5. <span data-ttu-id="17451-149">hello sqlcmd 프롬프트 tooshrink hello 데이터베이스 (1 >)를 입력 `DBCC Shrinkdatabase(ADSync,1);`옵니다 `GO` hello 다음 줄에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17451-149">tooshrink hello database, at hello sqlcmd prompt (1>), enter `DBCC Shrinkdatabase(ADSync,1);`, followed by `GO` in hello next line.</span></span>

6. <span data-ttu-id="17451-150">Hello 작업이 성공한 경우 toostart hello 동기화 서비스를 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-150">If hello operation is successful, try toostart hello Synchronization Service again.</span></span> <span data-ttu-id="17451-151">Hello 동기화 서비스를 시작할 수 있으면 너무 이동[실행 기록 데이터 삭제](#delete-run-history-data) 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="17451-151">If you can start hello Synchronization Service, go too[Delete run history data](#delete-run-history-data) step.</span></span> <span data-ttu-id="17451-152">그렇지 않은 경우 고객 지원으로 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="17451-152">If not, contact Support.</span></span>

### <a name="delete-run-history-data"></a><span data-ttu-id="17451-153">실행 기록 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="17451-153">Delete run history data</span></span>
<span data-ttu-id="17451-154">기본적으로 Azure AD Connect tooseven 일 분량의 실행된 기록 데이터를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-154">By default, Azure AD Connect retains up tooseven days’ worth of run history data.</span></span> <span data-ttu-id="17451-155">이 단계에서는 Azure AD Connect 동기화 Service 동기화를 다시 시작할 수 있도록 기록 데이터 tooreclaim DB 공간을 실행 하는 hello를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-155">In this step, we delete hello run history data tooreclaim DB space so that Azure AD Connect Synchronization Service can start syncing again.</span></span>

1.  <span data-ttu-id="17451-156">시작 **동기화 서비스 관리자** tooSTART → 라인으로 전환 하 여 동기화 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="17451-156">Start **Synchronization Service Manager** by going tooSTART → Synchronization Service.</span></span>

2.  <span data-ttu-id="17451-157">Toohello 이동 **작업** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-157">Go toohello **Operations** tab.</span></span>

3.  <span data-ttu-id="17451-158">**Actions** 아래에서 **Clear Runs**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-158">Under **Actions**, select **Clear Runs**…</span></span>

4.  <span data-ttu-id="17451-159">**Clear all runs** 또는 **Clear runs before… <date>** 옵션 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17451-159">You can either choose **Clear all runs** or **Clear runs before… <date>** option.</span></span> <span data-ttu-id="17451-160">2일보다 오래된 실행 기록 데이터를 삭제하여 시작하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="17451-160">It is recommended that you start by clearing run history data that are older than two days.</span></span> <span data-ttu-id="17451-161">Hello를 눌러 toorun로 만들려면 DB 크기를 계속 진행 **모든 실행 취소** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="17451-161">If you continue toorun into DB size issue, then choose hello **Clear all runs** option.</span></span>

### <a name="shorten-retention-period-for-run-history-data"></a><span data-ttu-id="17451-162">실행 기록 데이터에 대한 보존 기간 단축</span><span class="sxs-lookup"><span data-stu-id="17451-162">Shorten retention period for run history data</span></span>
<span data-ttu-id="17451-163">이 단계는 여러 동기화 주기 후 hello 10GB 제한 문제를 일으키지 tooreduce hello 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17451-163">This step is tooreduce hello likelihood of running into hello 10-GB limit issue after multiple sync cycles.</span></span>

1. <span data-ttu-id="17451-164">새 PowerShell 세션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="17451-164">Open a new PowerShell session.</span></span>

2. <span data-ttu-id="17451-165">실행 `Get-ADSyncScheduler` hello hello 현재 보존 기간을 지정 하는 PurgeRunHistoryInterval 속성을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-165">Run `Get-ADSyncScheduler` and take note of hello PurgeRunHistoryInterval property, which specifies hello current retention period.</span></span>

3. <span data-ttu-id="17451-166">실행 `Set-ADSyncScheduler -PurgeRunHistoryInterval 2.00:00:00` tooset hello 보존 기간 tootwo 일 합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-166">Run `Set-ADSyncScheduler -PurgeRunHistoryInterval 2.00:00:00` tooset hello retention period tootwo days.</span></span> <span data-ttu-id="17451-167">적절 하 게 hello 보존 기간을 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-167">Adjust hello retention period as appropriate.</span></span>

## <a name="long-term-solution--migrate-toofull-sql"></a><span data-ttu-id="17451-168">마이그레이션 toofull SQL 등 장기 솔루션</span><span class="sxs-lookup"><span data-stu-id="17451-168">Long-term solution – Migrate toofull SQL</span></span>
<span data-ttu-id="17451-169">일반적으로 hello 문제는 10GB의 데이터베이스 크기는 더 이상 Azure AD Connect toosynchronize에 대 한 충분 한 온-프레미스 Active Directory tooAzure AD 합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-169">In general, hello issue is indicative that 10-GB database size is no longer sufficient for Azure AD Connect toosynchronize your on-premises Active Directory tooAzure AD.</span></span> <span data-ttu-id="17451-170">Toousing hello 정식 버전의 SQL server 전환 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="17451-170">It is recommended that you switch toousing hello full version of SQL server.</span></span> <span data-ttu-id="17451-171">직접 sql hello 정식 버전의 hello 데이터베이스와 함께 기존 Azure AD Connect 배포의 LocalDB hello을 바꿀 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="17451-171">You cannot directly replace hello LocalDB of an existing Azure AD Connect deployment with hello database of hello full version of SQL.</span></span> <span data-ttu-id="17451-172">대신, SQL의 hello 전체 버전을 사용 하 여 새 Azure AD Connect 서버를 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-172">Instead, you must deploy a new Azure AD Connect server with hello full version of SQL.</span></span> <span data-ttu-id="17451-173">수행 하는 회전 마이그레이션 (SQL DB)와 함께 새 Azure AD Connect 서버 hello를 스테이징 서버에 다음 toohello 기존 Azure AD Connect 서버 (LocalDB)으로 배포 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="17451-173">It is recommended that you do a swing migration where hello new Azure AD Connect server (with SQL DB) is deployed as a staging server, next toohello existing Azure AD Connect server (with LocalDB).</span></span> 
* <span data-ttu-id="17451-174">원격 SQL Azure AD Connect로 참조 하는 tooconfigure 방법에 대 한 tooarticle [Azure AD Connect의 사용자 지정 설치](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-custom)합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-174">For instruction on how tooconfigure remote SQL with Azure AD Connect, refer tooarticle [Custom installation of Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-custom).</span></span>
* <span data-ttu-id="17451-175">Azure AD Connect 업그레이드가 회전 마이그레이션에 대 한 자세한 내용은 참조 tooarticle [Azure AD Connect:는 이전 버전 toohello 최신 버전에서 업그레이드](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version#swing-migration)합니다.</span><span class="sxs-lookup"><span data-stu-id="17451-175">For instructions on swing migration for Azure AD Connect upgrade, refer tooarticle [Azure AD Connect: Upgrade from a previous version toohello latest](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version#swing-migration).</span></span>

## <a name="next-steps"></a><span data-ttu-id="17451-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="17451-176">Next steps</span></span>
<span data-ttu-id="17451-177">[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="17451-177">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
