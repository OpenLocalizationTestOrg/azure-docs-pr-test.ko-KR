---
title: "Azure AD Connect 동기화: 스케줄러 | Microsoft Docs"
description: "이 항목에서는 Azure AD Connect 동기화의 기본 제공 스케줄러 기능을 설명합니다."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b1a598f-89c0-4244-9b20-f4aaad5233cf
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 63f69756b3933fecdec75cc677e1098447e5b94e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-scheduler"></a><span data-ttu-id="7e235-103">Azure AD Connect 동기화: 스케줄러</span><span class="sxs-lookup"><span data-stu-id="7e235-103">Azure AD Connect sync: Scheduler</span></span>
<span data-ttu-id="7e235-104">이 토픽은 Azure AD Connect 동기화(동기화 엔진이라고도 함)의 기본 제공 스케줄러를</span><span class="sxs-lookup"><span data-stu-id="7e235-104">This topic describes the built-in scheduler in Azure AD Connect sync (a.k.a.</span></span> <span data-ttu-id="7e235-105">설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-105">sync engine).</span></span>

<span data-ttu-id="7e235-106">이 기능은 빌드 1.1.105.0(2016년 2월에 발표됨)에서 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-106">This feature was introduced with build 1.1.105.0 (released February 2016).</span></span>

## <a name="overview"></a><span data-ttu-id="7e235-107">개요</span><span class="sxs-lookup"><span data-stu-id="7e235-107">Overview</span></span>
<span data-ttu-id="7e235-108">Azure AD Connect 동기화는 스케줄러를 사용하여 온-프레미스 디렉터리에서 발생하는 변경 내용을 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-108">Azure AD Connect sync synchronize changes occurring in your on-premises directory using a scheduler.</span></span> <span data-ttu-id="7e235-109">두 개의 스케줄러 프로세스가 있으며, 하나는 암호 동기화용이고 다른 하나는 개체/특성 동기화 및 유지 관리 작업용입니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-109">There are two scheduler processes, one for password sync and another for object/attribute sync and maintenance tasks.</span></span> <span data-ttu-id="7e235-110">이 항목에서는 후자에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-110">This topic covers the latter.</span></span>

<span data-ttu-id="7e235-111">이전 릴리스에서 개체와 특성에 대한 스케줄러는 동기화 엔진과 무관했습니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-111">In earlier releases, the scheduler for objects and attributes was external to the sync engine.</span></span> <span data-ttu-id="7e235-112">Windows 작업 스케줄러를 사용하거나 별도의 Windows 서비스로 동기화 프로세스를 트리거했습니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-112">It used Windows task scheduler or a separate Windows service to trigger the synchronization process.</span></span> <span data-ttu-id="7e235-113">스케줄러는 동기화 엔진에 기본 제공된 1.1 릴리스를 사용하며 일부 사용자 지정을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-113">The scheduler is with the 1.1 releases built-in to the sync engine and do allow some customization.</span></span> <span data-ttu-id="7e235-114">새 기본 동기화 빈도는 30분입니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-114">The new default synchronization frequency is 30 minutes.</span></span>

<span data-ttu-id="7e235-115">스케줄러는 두 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-115">The scheduler is responsible for two tasks:</span></span>

* <span data-ttu-id="7e235-116">**동기화 주기**.</span><span class="sxs-lookup"><span data-stu-id="7e235-116">**Synchronization cycle**.</span></span> <span data-ttu-id="7e235-117">변경 내용 가져오기, 동기화 및 내보내기 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-117">The process to import, sync, and export changes.</span></span>
* <span data-ttu-id="7e235-118">**유지 관리 작업**.</span><span class="sxs-lookup"><span data-stu-id="7e235-118">**Maintenance tasks**.</span></span> <span data-ttu-id="7e235-119">암호 재설정 및 DRS(장치 등록 서비스)에 대한 키와 인증서를 갱신합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-119">Renew keys and certificates for Password reset and Device Registration Service (DRS).</span></span> <span data-ttu-id="7e235-120">작업 로그의 이전 항목을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-120">Purge old entries in the operations log.</span></span>

<span data-ttu-id="7e235-121">스케줄러 자체가 항상 실행되지만 이러한 작업 중 하나만 실행되도록 구성하거나 하나도 실행되지 않도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-121">The scheduler itself is always running, but it can be configured to only run one or none of these tasks.</span></span> <span data-ttu-id="7e235-122">예를 들어 고유한 동기화 주기 프로세스가 필요한 경우 스케줄러에서 이 작업을 사용하지 않도록 설정할 수 있지만 유지 관리 작업은 여전히 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-122">For example, if you need to have your own synchronization cycle process, you can disable this task in the scheduler but still run the maintenance task.</span></span>

## <a name="scheduler-configuration"></a><span data-ttu-id="7e235-123">스케줄러 구성</span><span class="sxs-lookup"><span data-stu-id="7e235-123">Scheduler configuration</span></span>
<span data-ttu-id="7e235-124">현재 구성 설정을 보려면 PowerShell로 이동하고 `Get-ADSyncScheduler`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-124">To see your current configuration settings, go to PowerShell and run `Get-ADSyncScheduler`.</span></span> <span data-ttu-id="7e235-125">아래 그림과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-125">It shows you something like this picture:</span></span>

![GetSyncScheduler](./media/active-directory-aadconnectsync-feature-scheduler/getsynccyclesettings2016.png)

<span data-ttu-id="7e235-127">이 cmdlet을 실행했을 때 **사용할 수 없는 동기화 명령 또는 cmdlet** 이 나타나면 PowerShell 모듈이 로드되지 않은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-127">If you see **The sync command or cmdlet is not available** when you run this cmdlet, then the PowerShell module is not loaded.</span></span> <span data-ttu-id="7e235-128">기본 설정보다 PowerShell 제한 수준이 높은 도메인 컨트롤러 또는 서버에서 Azure AD Connect를 실행할 경우 이 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-128">This problem could happen if you run Azure AD Connect on a domain controller or on a server with higher PowerShell restriction levels than the default settings.</span></span> <span data-ttu-id="7e235-129">이 오류가 나타나면 `Import-Module ADSync`을(를) 실행하여 cmdlet을 사용할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-129">If you see this error, then run `Import-Module ADSync` to make the cmdlet available.</span></span>

* <span data-ttu-id="7e235-130">**AllowedSyncCycleInterval**.</span><span class="sxs-lookup"><span data-stu-id="7e235-130">**AllowedSyncCycleInterval**.</span></span> <span data-ttu-id="7e235-131">Azure AD에서 허용되는 동기화 주기 간의 가장 짧은 시간 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-131">The shortest time interval between synchronization cycles allowed by Azure AD.</span></span> <span data-ttu-id="7e235-132">이 설정보다 더 자주 동기화할 수 없으며 계속 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-132">You cannot synchronize more frequently than this setting and still be supported.</span></span>
* <span data-ttu-id="7e235-133">**CurrentlyEffectiveSyncCycleInterval**.</span><span class="sxs-lookup"><span data-stu-id="7e235-133">**CurrentlyEffectiveSyncCycleInterval**.</span></span> <span data-ttu-id="7e235-134">현재 적용 중인 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-134">The schedule currently in effect.</span></span> <span data-ttu-id="7e235-135">AllowedSyncInterval보다 낮은 경우 CustomizedSyncInterval(설정된 경우)과 동일한 값을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-135">It has the same value as CustomizedSyncInterval (if set) if it is not more frequent than AllowedSyncInterval.</span></span> <span data-ttu-id="7e235-136">1.1.281 이전 빌드를 사용하고 CustomizedSyncCycleInterval을 변경한 경우 이 변경 내용은 다음 동기화 주기 후에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-136">If you use a build before 1.1.281 and you change CustomizedSyncCycleInterval, this change takes effect after next synchronization cycle.</span></span> <span data-ttu-id="7e235-137">1.1.281 빌드의 경우 변경 내용은 즉시 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-137">From build 1.1.281 the change takes effect immediately.</span></span>
* <span data-ttu-id="7e235-138">**CustomizedSyncCycleInterval**.</span><span class="sxs-lookup"><span data-stu-id="7e235-138">**CustomizedSyncCycleInterval**.</span></span> <span data-ttu-id="7e235-139">스케줄러를 기본값 30분이 아닌 다른 빈도로 실행하려면 이 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-139">If you want the scheduler to run at any other frequency than the default 30 minutes, then you configure this setting.</span></span> <span data-ttu-id="7e235-140">위의 그림에서는 스케줄러가 1시간마다 실행되도록 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-140">In the picture above, the scheduler has been set to run every hour instead.</span></span> <span data-ttu-id="7e235-141">이 설정을 AllowedSyncInterval보다 낮은 값으로 설정하면 후자가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-141">If you set this setting to a value lower than AllowedSyncInterval, then the latter is used.</span></span>
* <span data-ttu-id="7e235-142">**NextSyncCyclePolicyType**.</span><span class="sxs-lookup"><span data-stu-id="7e235-142">**NextSyncCyclePolicyType**.</span></span> <span data-ttu-id="7e235-143">델타 또는 초기입니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-143">Either Delta or Initial.</span></span> <span data-ttu-id="7e235-144">다음 실행 시 델타 변경만 처리할지 또는 전체 가져오기 및 동기화를 수행할지 여부를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-144">Defines if the next run should only process delta changes, or if the next run should do a full import and sync.</span></span> <span data-ttu-id="7e235-145">후자는 새 규칙 또는 변경된 규칙을 다시 처리하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-145">The latter would also reprocess any new or changed rules.</span></span>
* <span data-ttu-id="7e235-146">**NextSyncCycleStartTimeInUTC**.</span><span class="sxs-lookup"><span data-stu-id="7e235-146">**NextSyncCycleStartTimeInUTC**.</span></span> <span data-ttu-id="7e235-147">스케줄러가 다음 동기화 주기를 시작하는 다음 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-147">Next time the scheduler starts the next sync cycle.</span></span>
* <span data-ttu-id="7e235-148">**PurgeRunHistoryInterval**.</span><span class="sxs-lookup"><span data-stu-id="7e235-148">**PurgeRunHistoryInterval**.</span></span> <span data-ttu-id="7e235-149">작업 로그가 유지되어야 하는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-149">The time operation logs should be kept.</span></span> <span data-ttu-id="7e235-150">이러한 로그는 Synchronization Service Manager에서 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-150">These logs can be reviewed in the synchronization service manager.</span></span> <span data-ttu-id="7e235-151">기본값은 7일 동안 로그를 유지하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-151">The default is to keep these logs for 7 days.</span></span>
* <span data-ttu-id="7e235-152">**SyncCycleEnabled**.</span><span class="sxs-lookup"><span data-stu-id="7e235-152">**SyncCycleEnabled**.</span></span> <span data-ttu-id="7e235-153">스케줄러가 작업의 일부로 가져오기, 동기화 및 내보내기 프로세스를 실행 중인지 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-153">Indicates if the scheduler is running the import, sync, and export processes as part of its operation.</span></span>
* <span data-ttu-id="7e235-154">**MaintenanceEnabled**.</span><span class="sxs-lookup"><span data-stu-id="7e235-154">**MaintenanceEnabled**.</span></span> <span data-ttu-id="7e235-155">유지 관리 프로세스를 사용할 수 있는지 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-155">Shows if the maintenance process is enabled.</span></span> <span data-ttu-id="7e235-156">인증서/키를 업데이트하고 작업 로그를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-156">It updates the certificates/keys and purges the operations log.</span></span>
* <span data-ttu-id="7e235-157">**StagingModeEnabled**.</span><span class="sxs-lookup"><span data-stu-id="7e235-157">**StagingModeEnabled**.</span></span> <span data-ttu-id="7e235-158">[스테이징 모드](active-directory-aadconnectsync-operations.md#staging-mode)를 사용할 수 있는지 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-158">Shows if [staging mode](active-directory-aadconnectsync-operations.md#staging-mode) is enabled.</span></span> <span data-ttu-id="7e235-159">이 설정을 사용하는 경우 내보내기는 무시되지만 가져오기 및 동기화는 계속 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-159">If this setting is enabled, then it suppresses the exports from running but still run import and synchronization.</span></span>
* <span data-ttu-id="7e235-160">**SchedulerSuspended**.</span><span class="sxs-lookup"><span data-stu-id="7e235-160">**SchedulerSuspended**.</span></span> <span data-ttu-id="7e235-161">업그레이드 중에 스케줄러 실행을 일시적으로 차단하기 위해 Connect에 의해 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-161">Set by Connect during an upgrade to temporarily block the scheduler from running.</span></span>

<span data-ttu-id="7e235-162">`Set-ADSyncScheduler`(으)로 이러한 모든 설정 중 일부를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-162">You can change some of these settings with `Set-ADSyncScheduler`.</span></span> <span data-ttu-id="7e235-163">다음 매개 변수를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-163">The following parameters can be modified:</span></span>

* <span data-ttu-id="7e235-164">CustomizedSyncCycleInterval</span><span class="sxs-lookup"><span data-stu-id="7e235-164">CustomizedSyncCycleInterval</span></span>
* <span data-ttu-id="7e235-165">NextSyncCyclePolicyType</span><span class="sxs-lookup"><span data-stu-id="7e235-165">NextSyncCyclePolicyType</span></span>
* <span data-ttu-id="7e235-166">PurgeRunHistoryInterval</span><span class="sxs-lookup"><span data-stu-id="7e235-166">PurgeRunHistoryInterval</span></span>
* <span data-ttu-id="7e235-167">SyncCycleEnabled</span><span class="sxs-lookup"><span data-stu-id="7e235-167">SyncCycleEnabled</span></span>
* <span data-ttu-id="7e235-168">MaintenanceEnabled</span><span class="sxs-lookup"><span data-stu-id="7e235-168">MaintenanceEnabled</span></span>

<span data-ttu-id="7e235-169">Azure AD Connect의 이전 빌드에서 **isStagingModeEnabled**는 Set-ADSyncScheduler에서 노출되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-169">In earlier builds of Azure AD Connect, **isStagingModeEnabled** was exposed in Set-ADSyncScheduler.</span></span> <span data-ttu-id="7e235-170">이 속성을 설정하는 것은 **지원되지 않습니다**.</span><span class="sxs-lookup"><span data-stu-id="7e235-170">It is **unsupported** to set this property.</span></span> <span data-ttu-id="7e235-171">속성 **SchedulerSuspended**는 Connect에서만 수정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-171">The property **SchedulerSuspended** should only be modified by Connect.</span></span> <span data-ttu-id="7e235-172">PowerShell에서 직접 설정하는 것은 **지원되지 않습니다**.</span><span class="sxs-lookup"><span data-stu-id="7e235-172">It is **unsupported** to set this with PowerShell directly.</span></span>

<span data-ttu-id="7e235-173">스케줄러 구성은 Azure AD에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-173">The scheduler configuration is stored in Azure AD.</span></span> <span data-ttu-id="7e235-174">스테이징 서버가 있는 경우 주 서버를 변경하면 스테이징 서버에도 영향을 줍니다(IsStagingModeEnabled 제외).</span><span class="sxs-lookup"><span data-stu-id="7e235-174">If you have a staging server, any change on the primary server also affects the staging server (except IsStagingModeEnabled).</span></span>

### <a name="customizedsynccycleinterval"></a><span data-ttu-id="7e235-175">CustomizedSyncCycleInterval</span><span class="sxs-lookup"><span data-stu-id="7e235-175">CustomizedSyncCycleInterval</span></span>
<span data-ttu-id="7e235-176">구문: `Set-ADSyncScheduler -CustomizedSyncCycleInterval d.HH:mm:ss`</span><span class="sxs-lookup"><span data-stu-id="7e235-176">Syntax: `Set-ADSyncScheduler -CustomizedSyncCycleInterval d.HH:mm:ss`</span></span>  
<span data-ttu-id="7e235-177">d -일, HH - 시간, mm - 분, ss - 초</span><span class="sxs-lookup"><span data-stu-id="7e235-177">d - days, HH - hours, mm - minutes, ss - seconds</span></span>

<span data-ttu-id="7e235-178">예제: `Set-ADSyncScheduler -CustomizedSyncCycleInterval 03:00:00`</span><span class="sxs-lookup"><span data-stu-id="7e235-178">Example: `Set-ADSyncScheduler -CustomizedSyncCycleInterval 03:00:00`</span></span>  
<span data-ttu-id="7e235-179">3시간마다 실행되도록 스케줄러를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-179">Changes the scheduler to run every 3 hours.</span></span>

<span data-ttu-id="7e235-180">예제: `Set-ADSyncScheduler -CustomizedSyncCycleInterval 1.0:0:0`</span><span class="sxs-lookup"><span data-stu-id="7e235-180">Example: `Set-ADSyncScheduler -CustomizedSyncCycleInterval 1.0:0:0`</span></span>  
<span data-ttu-id="7e235-181">매일 실행되도록 스케줄러를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-181">Changes change the scheduler to run daily.</span></span>

### <a name="disable-the-scheduler"></a><span data-ttu-id="7e235-182">스케줄러 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="7e235-182">Disable the scheduler</span></span>  
<span data-ttu-id="7e235-183">구성을 변경해야 할 경우 스케줄러를 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-183">If you need to make configuration changes, then you want to disable the scheduler.</span></span> <span data-ttu-id="7e235-184">예를 들어 [필터링 구성](active-directory-aadconnectsync-configure-filtering.md) 또는 [동기화 규칙을 변경](active-directory-aadconnectsync-change-the-configuration.md)하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-184">For example, when you [configure filtering](active-directory-aadconnectsync-configure-filtering.md) or [make changes to synchronization rules](active-directory-aadconnectsync-change-the-configuration.md).</span></span>

<span data-ttu-id="7e235-185">스케줄러를 비활성화하려면 `Set-ADSyncScheduler -SyncCycleEnabled $false`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-185">To disable the scheduler, run `Set-ADSyncScheduler -SyncCycleEnabled $false`.</span></span>

![스케줄러 사용 안 함](./media/active-directory-aadconnectsync-change-the-configuration/schedulerdisable.png)

<span data-ttu-id="7e235-187">변경했으면 잊지 말고 `Set-ADSyncScheduler -SyncCycleEnabled $true`로 스케줄러를 다시 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-187">When you've made your changes, do not forget to enable the scheduler again with `Set-ADSyncScheduler -SyncCycleEnabled $true`.</span></span>

## <a name="start-the-scheduler"></a><span data-ttu-id="7e235-188">스케줄러 시작</span><span class="sxs-lookup"><span data-stu-id="7e235-188">Start the scheduler</span></span>
<span data-ttu-id="7e235-189">스케줄러는 기본적으로 30분마다 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-189">The scheduler is by default run every 30 minutes.</span></span> <span data-ttu-id="7e235-190">경우에 따라 예약된 주기 사이에서 동기화 주기를 실행하려고 하거나 다른 유형을 실행해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-190">In some cases, you might want to run a sync cycle in between the scheduled cycles or you need to run a different type.</span></span>

<span data-ttu-id="7e235-191">**델타 동기화 주기**</span><span class="sxs-lookup"><span data-stu-id="7e235-191">**Delta sync cycle**</span></span>  
<span data-ttu-id="7e235-192">델타 동기화 주기에는 다음 단계가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-192">A delta sync cycle includes the following steps:</span></span>

* <span data-ttu-id="7e235-193">모든 커넥터에서 델타 가져오기</span><span class="sxs-lookup"><span data-stu-id="7e235-193">Delta import on all Connectors</span></span>
* <span data-ttu-id="7e235-194">모든 커넥터에서 델타 동기화</span><span class="sxs-lookup"><span data-stu-id="7e235-194">Delta sync on all Connectors</span></span>
* <span data-ttu-id="7e235-195">모든 커넥터에서 내보내기</span><span class="sxs-lookup"><span data-stu-id="7e235-195">Export on all Connectors</span></span>

<span data-ttu-id="7e235-196">즉시 동기화되어야 하는 긴급한 변경 사항이 있을 수 있습니다. 이것이 주기를 수동으로 실행해야 하는 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-196">It could be that you have an urgent change that must be synchronized immediately, which is why you need to manually run a cycle.</span></span> <span data-ttu-id="7e235-197">수동으로 주기를 실행해야 하는 경우 PowerShell에서 `Start-ADSyncSyncCycle -PolicyType Delta`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-197">If you need to manually run a cycle, then from PowerShell run `Start-ADSyncSyncCycle -PolicyType Delta`.</span></span>

<span data-ttu-id="7e235-198">**전체 동기화 주기**</span><span class="sxs-lookup"><span data-stu-id="7e235-198">**Full sync cycle**</span></span>  
<span data-ttu-id="7e235-199">다음 구성 변경 사항 중 하나를 수행한 경우 전체 동기화 주기(초기화라고도 함)를 실행해야</span><span class="sxs-lookup"><span data-stu-id="7e235-199">If you have made one of the following configuration changes, you need to run a full sync cycle (a.k.a.</span></span> <span data-ttu-id="7e235-200">합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-200">Initial):</span></span>

* <span data-ttu-id="7e235-201">소스 디렉터리에서 가져올 더 많은 개체 및 특성 추가</span><span class="sxs-lookup"><span data-stu-id="7e235-201">Added more objects or attributes to be imported from a source directory</span></span>
* <span data-ttu-id="7e235-202">동기화 규칙 변경</span><span class="sxs-lookup"><span data-stu-id="7e235-202">Made changes to the Synchronization rules</span></span>
* <span data-ttu-id="7e235-203">다른 수의 개체가 포함되도록 [필터링](active-directory-aadconnectsync-configure-filtering.md) 변경</span><span class="sxs-lookup"><span data-stu-id="7e235-203">Changed [filtering](active-directory-aadconnectsync-configure-filtering.md) so a different number of objects should be included</span></span>

<span data-ttu-id="7e235-204">이러한 변경 사항 중 하나를 수행한 경우 전체 동기화 주기를 실행하여 동기화 엔진이 커넥터 공간을 다시 병합할 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-204">If you have made one of these changes, then you need to run a full sync cycle so the sync engine has the opportunity to reconsolidate the connector spaces.</span></span> <span data-ttu-id="7e235-205">전체 동기화 주기에는 다음 단계가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-205">A full sync cycle includes the following steps:</span></span>

* <span data-ttu-id="7e235-206">모든 커넥터에서 전체 가져오기</span><span class="sxs-lookup"><span data-stu-id="7e235-206">Full Import on all Connectors</span></span>
* <span data-ttu-id="7e235-207">모든 커넥터에서 전체 동기화</span><span class="sxs-lookup"><span data-stu-id="7e235-207">Full Sync on all Connectors</span></span>
* <span data-ttu-id="7e235-208">모든 커넥터에서 내보내기</span><span class="sxs-lookup"><span data-stu-id="7e235-208">Export on all Connectors</span></span>

<span data-ttu-id="7e235-209">전체 동기화 주기를 시작하려면 PowerShell 프롬프트에서 `Start-ADSyncSyncCycle -PolicyType Initial`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-209">To initiate a full sync cycle, run `Start-ADSyncSyncCycle -PolicyType Initial` from a PowerShell prompt.</span></span> <span data-ttu-id="7e235-210">이 명령은 전체 동기화 주기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-210">This command starts a full sync cycle.</span></span>

## <a name="stop-the-scheduler"></a><span data-ttu-id="7e235-211">스케줄러 중지</span><span class="sxs-lookup"><span data-stu-id="7e235-211">Stop the scheduler</span></span>
<span data-ttu-id="7e235-212">스케줄러가 현재 동기화 주기를 실행 중인 경우 중지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-212">If the scheduler is currently running a synchronization cycle, you might need to stop it.</span></span> <span data-ttu-id="7e235-213">예를 들어 설치 마법사를 시작하는 경우 이 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-213">For example if you start the installation wizard and you get this error:</span></span>

![SyncCycleRunningError](./media/active-directory-aadconnectsync-feature-scheduler/synccyclerunningerror.png)

<span data-ttu-id="7e235-215">동기화 주기를 실행 중일 때 구성을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-215">When a sync cycle is running, you cannot make configuration changes.</span></span> <span data-ttu-id="7e235-216">스케줄러에서 프로세스를 완료할 때까지 기다릴 수 있지만 이를 중지하여 즉시 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-216">You could wait until the scheduler has finished the process, but you can also stop it so you can make your changes immediately.</span></span> <span data-ttu-id="7e235-217">현재 주기를 중지해도 나쁜 영향을 주지 않으며 변경 사항은 다음 실행 시 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-217">Stopping the current cycle is not harmful and pending changes are processed with next run.</span></span>

1. <span data-ttu-id="7e235-218">먼저 PowerShell cmdlet `Stop-ADSyncSyncCycle`을 사용하여 스케줄러가 현재 주기를 중지하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-218">Start by telling the scheduler to stop its current cycle with the PowerShell cmdlet `Stop-ADSyncSyncCycle`.</span></span>
2. <span data-ttu-id="7e235-219">1.1.281 이전 빌드를 사용 중인 경우 스케줄러를 중지해도 현재 작업에서 현재 커넥터는 중지되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-219">If you use a build before 1.1.281, then stopping the scheduler does not stop the current Connector from its current task.</span></span> <span data-ttu-id="7e235-220">커넥터를 강제로 중지하려면 ![StopAConnector](./media/active-directory-aadconnectsync-feature-scheduler/stopaconnector.png) 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-220">To force the Connector to stop, take the following actions: ![StopAConnector](./media/active-directory-aadconnectsync-feature-scheduler/stopaconnector.png)</span></span>
   * <span data-ttu-id="7e235-221">시작 메뉴에서 **동기화 서비스**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-221">Start **Synchronization Service** from the start menu.</span></span> <span data-ttu-id="7e235-222">**커넥터**로 이동하여 **실행** 상태인 커넥터를 강조 표시하고 작업에서 **중지**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-222">Go to **Connectors**, highlight the Connector with the state **Running**, and select **Stop** from the Actions.</span></span>

<span data-ttu-id="7e235-223">스케줄러가 아직 활성화되어 있으며 다음에 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-223">The scheduler is still active and starts again on next opportunity.</span></span>

## <a name="custom-scheduler"></a><span data-ttu-id="7e235-224">사용자 지정 스케줄러</span><span class="sxs-lookup"><span data-stu-id="7e235-224">Custom scheduler</span></span>
<span data-ttu-id="7e235-225">이 섹션에서 설명하는 cmdlet은 빌드 [1.1.130.0](active-directory-aadconnect-version-history.md#111300) 이상에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-225">The cmdlets documented in this section are only available in build [1.1.130.0](active-directory-aadconnect-version-history.md#111300) and later.</span></span>

<span data-ttu-id="7e235-226">기본 제공 스케줄러가 요구 사항을 충족하지 않으면 PowerShell을 사용하여 커넥터를 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-226">If the built-in scheduler does not satisfy your requirements, then you can schedule the Connectors using PowerShell.</span></span>

### <a name="invoke-adsyncrunprofile"></a><span data-ttu-id="7e235-227">Invoke-ADSyncRunProfile</span><span class="sxs-lookup"><span data-stu-id="7e235-227">Invoke-ADSyncRunProfile</span></span>
<span data-ttu-id="7e235-228">다음과 같이 커넥터에 대한 프로필을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-228">You can start a profile for a Connector in this way:</span></span>

```
Invoke-ADSyncRunProfile -ConnectorName "name of connector" -RunProfileName "name of profile"
```

<span data-ttu-id="7e235-229">[커넥터 이름](active-directory-aadconnectsync-service-manager-ui-connectors.md)과 [실행 프로필 이름](active-directory-aadconnectsync-service-manager-ui-connectors.md#configure-run-profiles)에 사용할 이름은 [Synchronization Service Manager UI](active-directory-aadconnectsync-service-manager-ui.md)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-229">The names to use for [Connector names](active-directory-aadconnectsync-service-manager-ui-connectors.md) and [Run Profile Names](active-directory-aadconnectsync-service-manager-ui-connectors.md#configure-run-profiles) can be found in the [Synchronization Service Manager UI](active-directory-aadconnectsync-service-manager-ui.md).</span></span>

![실행 프로필 호출](./media/active-directory-aadconnectsync-feature-scheduler/invokerunprofile.png)  

<span data-ttu-id="7e235-231">`Invoke-ADSyncRunProfile` cmdlet은 동기화됩니다. 즉 커넥터가 성공적으로든 오류가 발생한 상태로든 작업을 완료할 때까지는 컨트롤을 반환하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-231">The `Invoke-ADSyncRunProfile` cmdlet is synchronous, that is, it does not return control until the Connector has completed the operation, either successfully or with an error.</span></span>

<span data-ttu-id="7e235-232">커넥터를 예약할 경우 다음 순서대로 예약하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-232">When you schedule your Connectors, the recommendation is to schedule them in the following order:</span></span>

1. <span data-ttu-id="7e235-233">(전체/델타) Active Directory와 같은 온-프레미스 디렉터리에서 가져오기</span><span class="sxs-lookup"><span data-stu-id="7e235-233">(Full/Delta) Import from on-premises directories, such as Active Directory</span></span>
2. <span data-ttu-id="7e235-234">(전체/델타) Azure AD에서 가져오기</span><span class="sxs-lookup"><span data-stu-id="7e235-234">(Full/Delta) Import from Azure AD</span></span>
3. <span data-ttu-id="7e235-235">(전체/델타) Active Directory와 같은 온-프레미스 디렉터리에서 동기화</span><span class="sxs-lookup"><span data-stu-id="7e235-235">(Full/Delta) Synchronization from on-premises directories, such as Active Directory</span></span>
4. <span data-ttu-id="7e235-236">(전체/델타) Azure AD에서 동기화</span><span class="sxs-lookup"><span data-stu-id="7e235-236">(Full/Delta) Synchronization from Azure AD</span></span>
5. <span data-ttu-id="7e235-237">Azure AD로 내보내기</span><span class="sxs-lookup"><span data-stu-id="7e235-237">Export to Azure AD</span></span>
6. <span data-ttu-id="7e235-238">Active Directory와 같은 온-프레미스 디렉터리로 내보내기</span><span class="sxs-lookup"><span data-stu-id="7e235-238">Export to on-premises directories, such as Active Directory</span></span>

<span data-ttu-id="7e235-239">이 순서는 기본 제공 스케줄러에서 커넥터를 실행 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-239">This order is how the built-in scheduler runs the Connectors.</span></span>

### <a name="get-adsyncconnectorrunstatus"></a><span data-ttu-id="7e235-240">Get-ADSyncConnectorRunStatus</span><span class="sxs-lookup"><span data-stu-id="7e235-240">Get-ADSyncConnectorRunStatus</span></span>
<span data-ttu-id="7e235-241">동기화 엔진이 사용 중인지 또는 유휴 상태인지 모니터링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-241">You can also monitor the sync engine to see if it is busy or idle.</span></span> <span data-ttu-id="7e235-242">이 cmdlet은 동기화 엔진이 유휴 상태이고 커넥터를 실행하고 있지 않은 경우 빈 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-242">This cmdlet returns an empty result if the sync engine is idle and is not running a Connector.</span></span> <span data-ttu-id="7e235-243">커넥터가 실행 중이면 커넥터의 이름을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-243">If a Connector is running, it returns the name of the Connector.</span></span>

```
Get-ADSyncConnectorRunStatus
```

![커넥터 실행 상태](./media/active-directory-aadconnectsync-feature-scheduler/getconnectorrunstatus.png)  
<span data-ttu-id="7e235-245">위의 그림에서 첫 번째 줄은 동기화 엔진이 유휴 상태인 경우이고,</span><span class="sxs-lookup"><span data-stu-id="7e235-245">In the picture above, the first line is from a state where the sync engine is idle.</span></span> <span data-ttu-id="7e235-246">두 번째 줄은 Azure AD 커넥터가 실행 중인 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-246">The second line from when the Azure AD Connector is running.</span></span>

## <a name="scheduler-and-installation-wizard"></a><span data-ttu-id="7e235-247">스케줄러 및 설치 마법사</span><span class="sxs-lookup"><span data-stu-id="7e235-247">Scheduler and installation wizard</span></span>
<span data-ttu-id="7e235-248">설치 마법사를 시작하면 스케줄러가 일시 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-248">If you start the installation wizard, then the scheduler is temporarily suspended.</span></span> <span data-ttu-id="7e235-249">이는 구성을 변경했다고 가정하기 때문이며 동기화 엔진이 실행 중인 경우에는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-249">This behavior is because it is assumed you make configuration changes and these settings cannot be applied if the sync engine is actively running.</span></span> <span data-ttu-id="7e235-250">이러한 이유로 동기화 엔진이 동기화 작업을 수행하지 못하므로 설치 마법사를 연 상태로 두지 마세요.</span><span class="sxs-lookup"><span data-stu-id="7e235-250">For this reason, do not leave the installation wizard open since it stops the sync engine from performing any synchronization actions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e235-251">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7e235-251">Next steps</span></span>
<span data-ttu-id="7e235-252">[Azure AD Connect 동기화](active-directory-aadconnectsync-whatis.md) 구성에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-252">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="7e235-253">[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7e235-253">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
