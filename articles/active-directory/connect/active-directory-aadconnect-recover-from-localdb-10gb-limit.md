---
title: "Azure AD Connect: LocalDB 10GB 제한 문제에서 복구하는 방법 | Microsoft Docs"
description: "이 항목에서는 LocalDB 10GB 제한 문제가 발생한 경우 Azure AD Connect 동기화 서비스를 복구하는 방법을 설명합니다."
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
ms.openlocfilehash: 08e682c51b12d4506019d2f6b68e1eae0798b990
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-how-to-recover-from-localdb-10-gb-limit"></a><span data-ttu-id="64213-103">Azure AD Connect: LocalDB 10GB 제한에서 복구하는 방법</span><span class="sxs-lookup"><span data-stu-id="64213-103">Azure AD Connect: How to recover from LocalDB 10-GB limit</span></span>
<span data-ttu-id="64213-104">Azure AD Connect는 ID 데이터를 저장하기 위한 SQL Server 데이터베이스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-104">Azure AD Connect requires a SQL Server database to store identity data.</span></span> <span data-ttu-id="64213-105">Azure AD connect로 설치된 기본 SQL Server 2012 Express LocalDB를 사용하거나 사용자 고유의 전체 SQL을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64213-105">You can either use the default SQL Server 2012 Express LocalDB installed with Azure AD Connect or use your own full SQL.</span></span> <span data-ttu-id="64213-106">SQL Server Express는 10GB 크기 제한을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-106">SQL Server Express imposes a 10-GB size limit.</span></span> <span data-ttu-id="64213-107">LocalDB를 사용하고 이 제한에 도달하는 경우 Azure AD Connect 동기화 서비스는 더 이상 제대로 시작하거나 동기화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="64213-107">When using LocalDB and this limit is reached, Azure AD Connect Synchronization Service can no longer start or synchronize properly.</span></span> <span data-ttu-id="64213-108">이 문서에서는 복구 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-108">This article provides the recovery steps.</span></span>

## <a name="symptoms"></a><span data-ttu-id="64213-109">증상</span><span class="sxs-lookup"><span data-stu-id="64213-109">Symptoms</span></span>
<span data-ttu-id="64213-110">두 가지 일반적인 증상이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64213-110">There are two common symptoms:</span></span>

* <span data-ttu-id="64213-111">Azure AD Connect 동기화 서비스가 **실행**되지만 *“stopped-database-disk-full”* 오류로 동기화에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-111">Azure AD Connect Synchronization Service **is running** but fails to synchronize with *“stopped-database-disk-full”* error.</span></span>

* <span data-ttu-id="64213-112">Azure AD Connect 동기화 서비스를 **시작할 수 없습니다**.</span><span class="sxs-lookup"><span data-stu-id="64213-112">Azure AD Connect Synchronization Service **is unable to start**.</span></span> <span data-ttu-id="64213-113">서비스를 시작하려고 할 때 이벤트 6323 및 오류 메시지 *"SQL Server의 디스크 공간이 부족하기 때문에 서버에서 오류가 발생했습니다."*와 함께 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-113">When you attempt to start the service, it fails with event 6323 and error message *"The server encountered an error because SQL Server is out of disk space."*</span></span>

## <a name="short-term-recovery-steps"></a><span data-ttu-id="64213-114">단기 복구 단계</span><span class="sxs-lookup"><span data-stu-id="64213-114">Short-term recovery steps</span></span>
<span data-ttu-id="64213-115">이 섹션에서는 Azure AD Connect 동기화 서비스를 다시 시작하는 작업에 필요한 DB 공간을 회수하는 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-115">This section provides the steps to reclaim DB space required for Azure AD Connect Synchronization Service to resume operation.</span></span> <span data-ttu-id="64213-116">단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="64213-116">The steps include:</span></span>
1. [<span data-ttu-id="64213-117">동기화 서비스 상태 확인</span><span class="sxs-lookup"><span data-stu-id="64213-117">Determine the Synchronization Service status</span></span>](#determine-the-synchronization-service-status)
2. [<span data-ttu-id="64213-118">데이터베이스 축소</span><span class="sxs-lookup"><span data-stu-id="64213-118">Shrink the database</span></span>](#shrink-the-database)
3. [<span data-ttu-id="64213-119">실행 기록 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="64213-119">Delete run history data</span></span>](#delete-run-history-data)
4. [<span data-ttu-id="64213-120">실행 기록 데이터에 대한 보존 기간 단축</span><span class="sxs-lookup"><span data-stu-id="64213-120">Shorten retention period for run history data</span></span>](#shorten-retention-period-for-run-history-data)

### <a name="determine-the-synchronization-service-status"></a><span data-ttu-id="64213-121">동기화 서비스 상태 확인</span><span class="sxs-lookup"><span data-stu-id="64213-121">Determine the Synchronization Service status</span></span>
<span data-ttu-id="64213-122">먼저 동기화 서비스가 계속 실행 중인지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-122">First, determine whether the Synchronization Service is still running or not:</span></span>

1. <span data-ttu-id="64213-123">관리자 권한으로 Azure AD Connect 서버에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-123">Log in to your Azure AD Connect server as administrator.</span></span>

2. <span data-ttu-id="64213-124">**서비스 제어 관리자**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-124">Go to **Service Control Manager**.</span></span>

3. <span data-ttu-id="64213-125">**Microsoft Azure AD Sync**의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-125">Check the status of **Microsoft Azure AD Sync**.</span></span>


4. <span data-ttu-id="64213-126">실행 중인 경우 서비스를 중지하거나 다시 시작하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="64213-126">If it is running, do not stop or restart the service.</span></span> <span data-ttu-id="64213-127">[데이터베이스 축소](#shrink-the-database) 단계를 건너뛰고 [실행 기록 데이터 삭제](#delete-run-history-data) 단계로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-127">Skip [Shrink the database](#shrink-the-database) step and go to [Delete run history data](#delete-run-history-data) step.</span></span>

5. <span data-ttu-id="64213-128">실행 중이 아닌 경우 서비스를 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="64213-128">If it is not running, try to start the service.</span></span> <span data-ttu-id="64213-129">서비스가 성공적으로 시작하는 경우 [데이터베이스 축소](#shrink-the-database) 단계를 건너뛰고 [실행 기록 데이터 삭제](#delete-run-history-data) 단계로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-129">If the service starts successfully, skip [Shrink the database](#shrink-the-database) step and go to [Delete run history data](#delete-run-history-data) step.</span></span> <span data-ttu-id="64213-130">그렇지 않으면 [데이터베이스 축소](#shrink-the-database) 단계를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-130">Otherwise, continue with [Shrink the database](#shrink-the-database) step.</span></span>

### <a name="shrink-the-database"></a><span data-ttu-id="64213-131">데이터베이스 축소</span><span class="sxs-lookup"><span data-stu-id="64213-131">Shrink the database</span></span>
<span data-ttu-id="64213-132">축소 작업을 사용하여 동기화 서비스를 시작하는 데 충분한 DB 공간을 확보합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-132">Use the Shrink operation to free up enough DB space to start the Synchronization Service.</span></span> <span data-ttu-id="64213-133">데이터베이스에서 공백을 제거하여 DB 공간을 확보합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-133">It frees up DB space by removing whitespaces in the database.</span></span> <span data-ttu-id="64213-134">항상 공백을 복구할 수 있다고 보장되지 않으므로 이 단계가 최선적입니다.</span><span class="sxs-lookup"><span data-stu-id="64213-134">This step is best-effort as it is not guaranteed that you can always recover space.</span></span> <span data-ttu-id="64213-135">축소 작업에 대한 자세한 내용은 이 [데이터베이스 축소](https://msdn.microsoft.com/library/ms189035.aspx) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="64213-135">To learn more about Shrink operation, read this article [Shrink a database](https://msdn.microsoft.com/library/ms189035.aspx).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="64213-136">동기화 서비스를 실행할 수 있는 경우 이 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="64213-136">Skip this step if you can get the Synchronization Service to run.</span></span> <span data-ttu-id="64213-137">늘어난 조각화로 인해 성능 저하가 발생할 수 있으므로 SQL DB를 축소하는 것은 좋지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="64213-137">It is not recommended to shrink the SQL DB as it can lead to poor performance due to increased fragmentation.</span></span>

<span data-ttu-id="64213-138">Azure AD Connect에 대해 만든 데이터베이스의 이름은 **ADSync**입니다.</span><span class="sxs-lookup"><span data-stu-id="64213-138">The name of the database created for Azure AD Connect is **ADSync**.</span></span> <span data-ttu-id="64213-139">축소 작업을 수행하려면 sysadmin 또는 데이터베이스의 DBO로 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-139">To perform a Shrink operation, you must log in either as the sysadmin or DBO of the database.</span></span> <span data-ttu-id="64213-140">Azure AD Connect를 설치하는 동안 다음 계정에 sysadmin 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="64213-140">During Azure AD Connect installation, the following accounts are granted sysadmin rights:</span></span>
* <span data-ttu-id="64213-141">로컬 관리자</span><span class="sxs-lookup"><span data-stu-id="64213-141">Local Administrators</span></span>
* <span data-ttu-id="64213-142">Azure AD Connect 설치를 실행하는 데 사용한 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="64213-142">The user account that was used to run Azure AD Connect installation.</span></span>
* <span data-ttu-id="64213-143">Azure AD Connect 동기화 서비스의 운영 컨텍스트로 사용되는 동기화 서비스 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="64213-143">The Sync Service account that is used as the operating context of Azure AD Connect Synchronization Service.</span></span>
* <span data-ttu-id="64213-144">설치 중 생성된 로컬 그룹 ADSyncAdmins입니다.</span><span class="sxs-lookup"><span data-stu-id="64213-144">The local group ADSyncAdmins that was created during installation.</span></span>

1. <span data-ttu-id="64213-145">`%ProgramFiles%\program files\Microsoft Azure AD Sync\Data` 아래에 위치한 **ADSync.mdf** 및 **ADSync_log.ldf** 파일을 복사하여 데이터베이스를 안전한 위치로 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-145">Back up the database by copying **ADSync.mdf** and **ADSync_log.ldf** files located under `%ProgramFiles%\program files\Microsoft Azure AD Sync\Data` to a safe location.</span></span>

2. <span data-ttu-id="64213-146">새 PowerShell 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-146">Start a new PowerShell session.</span></span>

3. <span data-ttu-id="64213-147">`%ProgramFiles%\Program Files\Microsoft SQL Server\110\Tools\Binn` 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-147">Navigate to folder `%ProgramFiles%\Program Files\Microsoft SQL Server\110\Tools\Binn`.</span></span>

4. <span data-ttu-id="64213-148">`./SQLCMD.EXE -S “(localdb)\.\ADSync” -U <Username> -P <Password>` 명령을 실행하고 sysadmin 또는 DBO 데이터베이스의 자격 증명을 사용하여 **sqlcmd** 유틸리티를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-148">Start **sqlcmd** utility by running the command `./SQLCMD.EXE -S “(localdb)\.\ADSync” -U <Username> -P <Password>`, using the credential of a sysadmin or the database DBO.</span></span>

5. <span data-ttu-id="64213-149">데이터베이스를 축소하려면 Sqlcmd 프롬프트(1>)에서 다음 줄에 `GO`가 따라오는 `DBCC Shrinkdatabase(ADSync,1);`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-149">To shrink the database, at the sqlcmd prompt (1>), enter `DBCC Shrinkdatabase(ADSync,1);`, followed by `GO` in the next line.</span></span>

6. <span data-ttu-id="64213-150">작업이 성공한 경우 동기화 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-150">If the operation is successful, try to start the Synchronization Service again.</span></span> <span data-ttu-id="64213-151">동기화 서비스를 시작할 수 있는 경우 [실행 기록 데이터 삭제](#delete-run-history-data) 단계로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-151">If you can start the Synchronization Service, go to [Delete run history data](#delete-run-history-data) step.</span></span> <span data-ttu-id="64213-152">그렇지 않은 경우 고객 지원으로 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="64213-152">If not, contact Support.</span></span>

### <a name="delete-run-history-data"></a><span data-ttu-id="64213-153">실행 기록 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="64213-153">Delete run history data</span></span>
<span data-ttu-id="64213-154">기본적으로 Azure AD Connect는 7일 동안 실행 기록 데이터를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-154">By default, Azure AD Connect retains up to seven days’ worth of run history data.</span></span> <span data-ttu-id="64213-155">이 단계에서는 실행 기록 데이터를 삭제하여 Azure AD Connect 동기화 서비스가 동기화를 다시 시작할 수 있도록 DB 공간을 확보합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-155">In this step, we delete the run history data to reclaim DB space so that Azure AD Connect Synchronization Service can start syncing again.</span></span>

1.  <span data-ttu-id="64213-156">시작 → 동기화 서비스로 이동하여 **Synchronization Service Manager**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-156">Start **Synchronization Service Manager** by going to START → Synchronization Service.</span></span>

2.  <span data-ttu-id="64213-157">**Operations** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-157">Go to the **Operations** tab.</span></span>

3.  <span data-ttu-id="64213-158">**Actions** 아래에서 **Clear Runs**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-158">Under **Actions**, select **Clear Runs**…</span></span>

4.  <span data-ttu-id="64213-159">**Clear all runs** 또는 **Clear runs before… <date>** 옵션 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64213-159">You can either choose **Clear all runs** or **Clear runs before… <date>** option.</span></span> <span data-ttu-id="64213-160">2일보다 오래된 실행 기록 데이터를 삭제하여 시작하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="64213-160">It is recommended that you start by clearing run history data that are older than two days.</span></span> <span data-ttu-id="64213-161">DB 크기 문제가 계속되면 **Clear all runs** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-161">If you continue to run into DB size issue, then choose the **Clear all runs** option.</span></span>

### <a name="shorten-retention-period-for-run-history-data"></a><span data-ttu-id="64213-162">실행 기록 데이터에 대한 보존 기간 단축</span><span class="sxs-lookup"><span data-stu-id="64213-162">Shorten retention period for run history data</span></span>
<span data-ttu-id="64213-163">이 단계는 여러 동기화 주기 후 10GB 제한 문제의 발생 가능성을 줄이는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="64213-163">This step is to reduce the likelihood of running into the 10-GB limit issue after multiple sync cycles.</span></span>

1. <span data-ttu-id="64213-164">새 PowerShell 세션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64213-164">Open a new PowerShell session.</span></span>

2. <span data-ttu-id="64213-165">`Get-ADSyncScheduler`를 실행하고 현재 보존 기간을 지정하는 PurgeRunHistoryInterval 속성을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="64213-165">Run `Get-ADSyncScheduler` and take note of the PurgeRunHistoryInterval property, which specifies the current retention period.</span></span>

3. <span data-ttu-id="64213-166">`Set-ADSyncScheduler -PurgeRunHistoryInterval 2.00:00:00`을 실행하여 보존 기간을 2일로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-166">Run `Set-ADSyncScheduler -PurgeRunHistoryInterval 2.00:00:00` to set the retention period to two days.</span></span> <span data-ttu-id="64213-167">보존 기간을 적절하게 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-167">Adjust the retention period as appropriate.</span></span>

## <a name="long-term-solution--migrate-to-full-sql"></a><span data-ttu-id="64213-168">장기 솔루션 – 전체 SQL로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="64213-168">Long-term solution – Migrate to full SQL</span></span>
<span data-ttu-id="64213-169">일반적으로 문제는 Azure AD Connect가 온-프레미스 Active Directory를 Azure AD로 동기화하는 데 10GB의 데이터베이스 크기는 더 이상 충분하지 않다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="64213-169">In general, the issue is indicative that 10-GB database size is no longer sufficient for Azure AD Connect to synchronize your on-premises Active Directory to Azure AD.</span></span> <span data-ttu-id="64213-170">SQL 서버의 전체 버전을 사용하도록 전환하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="64213-170">It is recommended that you switch to using the full version of SQL server.</span></span> <span data-ttu-id="64213-171">기존 Azure AD Connect 배포의 LocalDB를 정식 버전의 SQL 데이터베이스와 직접 바꿀 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="64213-171">You cannot directly replace the LocalDB of an existing Azure AD Connect deployment with the database of the full version of SQL.</span></span> <span data-ttu-id="64213-172">대신 SQL의 정식 버전으로 새 Azure AD Connect 서버를 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64213-172">Instead, you must deploy a new Azure AD Connect server with the full version of SQL.</span></span> <span data-ttu-id="64213-173">새 Azure AD Connect 서버(SQL DB로)가 기존 Azure AD Connect 서버(LocalDB로) 옆의 스테이징 서버로 배포되는 스윙 마이그레이션을 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="64213-173">It is recommended that you do a swing migration where the new Azure AD Connect server (with SQL DB) is deployed as a staging server, next to the existing Azure AD Connect server (with LocalDB).</span></span> 
* <span data-ttu-id="64213-174">Azure AD Connect로 원격 SQL을 구성하는 방법에 대한 지침은 [Azure AD Connect의 사용자 지정 설치](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-custom) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="64213-174">For instruction on how to configure remote SQL with Azure AD Connect, refer to article [Custom installation of Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-custom).</span></span>
* <span data-ttu-id="64213-175">Azure AD Connect 업그레이드를 위한 스윙 마이그레이션에 대한 지침은 [Azure AD Connect:이전 버전에서 최신 버전으로 업그레이드](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version#swing-migration) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="64213-175">For instructions on swing migration for Azure AD Connect upgrade, refer to article [Azure AD Connect: Upgrade from a previous version to the latest](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version#swing-migration).</span></span>

## <a name="next-steps"></a><span data-ttu-id="64213-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="64213-176">Next steps</span></span>
<span data-ttu-id="64213-177">[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="64213-177">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
