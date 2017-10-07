---
title: "Azure AD Connect 동기화: 스케줄러 | Microsoft Docs"
description: "이 항목에서는 Azure AD Connect 동기화의 기본 제공 스케줄러 기능을 hello 설명 합니다."
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
ms.openlocfilehash: c587039cc68d305862a07beff364894b6f74cd2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-scheduler"></a><span data-ttu-id="89976-103">Azure AD Connect 동기화: 스케줄러</span><span class="sxs-lookup"><span data-stu-id="89976-103">Azure AD Connect sync: Scheduler</span></span>
<span data-ttu-id="89976-104">이 항목에서는 Azure AD Connect 동기화의 기본 제공 스케줄러 hello (규칙 하위 설명</span><span class="sxs-lookup"><span data-stu-id="89976-104">This topic describes hello built-in scheduler in Azure AD Connect sync (a.k.a.</span></span> <span data-ttu-id="89976-105">설명합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-105">sync engine).</span></span>

<span data-ttu-id="89976-106">이 기능은 빌드 1.1.105.0(2016년 2월에 발표됨)에서 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="89976-106">This feature was introduced with build 1.1.105.0 (released February 2016).</span></span>

## <a name="overview"></a><span data-ttu-id="89976-107">개요</span><span class="sxs-lookup"><span data-stu-id="89976-107">Overview</span></span>
<span data-ttu-id="89976-108">Azure AD Connect 동기화는 스케줄러를 사용하여 온-프레미스 디렉터리에서 발생하는 변경 내용을 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-108">Azure AD Connect sync synchronize changes occurring in your on-premises directory using a scheduler.</span></span> <span data-ttu-id="89976-109">두 개의 스케줄러 프로세스가 있으며, 하나는 암호 동기화용이고 다른 하나는 개체/특성 동기화 및 유지 관리 작업용입니다.</span><span class="sxs-lookup"><span data-stu-id="89976-109">There are two scheduler processes, one for password sync and another for object/attribute sync and maintenance tasks.</span></span> <span data-ttu-id="89976-110">이 항목에서는 hello 후자를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="89976-110">This topic covers hello latter.</span></span>

<span data-ttu-id="89976-111">이전 릴리스에서 개체와 특성에 대 한 hello 스케줄러 외부 toohello 동기화 엔진이 했습니다.</span><span class="sxs-lookup"><span data-stu-id="89976-111">In earlier releases, hello scheduler for objects and attributes was external toohello sync engine.</span></span> <span data-ttu-id="89976-112">Windows 작업 스케줄러 또는 별도 Windows 서비스 tootrigger hello 동기화 프로세스를 사용.</span><span class="sxs-lookup"><span data-stu-id="89976-112">It used Windows task scheduler or a separate Windows service tootrigger hello synchronization process.</span></span> <span data-ttu-id="89976-113">1.1 릴리스에 기본 제공 toohello 동기화 엔진이 hello를 일부 사용자 지정을 허용지 않습니다 hello 스케줄러와는 합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-113">hello scheduler is with hello 1.1 releases built-in toohello sync engine and do allow some customization.</span></span> <span data-ttu-id="89976-114">hello 새 기본 동기화 빈도 30 분입니다.</span><span class="sxs-lookup"><span data-stu-id="89976-114">hello new default synchronization frequency is 30 minutes.</span></span>

<span data-ttu-id="89976-115">hello 스케줄러는 두 가지 작업을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-115">hello scheduler is responsible for two tasks:</span></span>

* <span data-ttu-id="89976-116">**동기화 주기**.</span><span class="sxs-lookup"><span data-stu-id="89976-116">**Synchronization cycle**.</span></span> <span data-ttu-id="89976-117">hello 프로세스 tooimport, 동기화 및 내보내기 변경.</span><span class="sxs-lookup"><span data-stu-id="89976-117">hello process tooimport, sync, and export changes.</span></span>
* <span data-ttu-id="89976-118">**유지 관리 작업**.</span><span class="sxs-lookup"><span data-stu-id="89976-118">**Maintenance tasks**.</span></span> <span data-ttu-id="89976-119">암호 재설정 및 DRS(장치 등록 서비스)에 대한 키와 인증서를 갱신합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-119">Renew keys and certificates for Password reset and Device Registration Service (DRS).</span></span> <span data-ttu-id="89976-120">Hello 작업 로그에서 이전 항목을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-120">Purge old entries in hello operations log.</span></span>

<span data-ttu-id="89976-121">자체 hello 스케줄러가 실행 되 고 항상 이지만 하나 또는 이러한 작업을 실행 하는 구성 된 tooonly 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89976-121">hello scheduler itself is always running, but it can be configured tooonly run one or none of these tasks.</span></span> <span data-ttu-id="89976-122">예를 들어 사용자가 소유한 동기화 주기 프로세스 toohave 해야 할 경우 hello 스케줄러에서는이 작업이 있지만 여전히 실행된 hello 유지 관리 작업 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89976-122">For example, if you need toohave your own synchronization cycle process, you can disable this task in hello scheduler but still run hello maintenance task.</span></span>

## <a name="scheduler-configuration"></a><span data-ttu-id="89976-123">스케줄러 구성</span><span class="sxs-lookup"><span data-stu-id="89976-123">Scheduler configuration</span></span>
<span data-ttu-id="89976-124">toosee 현재 구성 설정, tooPowerShell 돌아가서 실행 `Get-ADSyncScheduler`합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-124">toosee your current configuration settings, go tooPowerShell and run `Get-ADSyncScheduler`.</span></span> <span data-ttu-id="89976-125">아래 그림과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="89976-125">It shows you something like this picture:</span></span>

![GetSyncScheduler](./media/active-directory-aadconnectsync-feature-scheduler/getsynccyclesettings2016.png)

<span data-ttu-id="89976-127">표시 되 면 **hello 동기화 명령 또는 cmdlet를 사용할 수 없습니다** 이 cmdlet을 실행 하면 다음 hello PowerShell 모듈이 로드 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="89976-127">If you see **hello sync command or cmdlet is not available** when you run this cmdlet, then hello PowerShell module is not loaded.</span></span> <span data-ttu-id="89976-128">이 문제는 도메인 컨트롤러 또는 hello 기본 설정 보다 더 높은 PowerShell 제한 수준 사용 하 여 서버에서 Azure AD Connect를 실행 하는 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89976-128">This problem could happen if you run Azure AD Connect on a domain controller or on a server with higher PowerShell restriction levels than hello default settings.</span></span> <span data-ttu-id="89976-129">이 오류를 표시 하는 경우 다음 실행 `Import-Module ADSync` toomake hello cmdlet 사용 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-129">If you see this error, then run `Import-Module ADSync` toomake hello cmdlet available.</span></span>

* <span data-ttu-id="89976-130">**AllowedSyncCycleInterval**.</span><span class="sxs-lookup"><span data-stu-id="89976-130">**AllowedSyncCycleInterval**.</span></span> <span data-ttu-id="89976-131">hello 가장 짧은 시간 간격 Azure AD에서 허용 하는 동기화 주기 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="89976-131">hello shortest time interval between synchronization cycles allowed by Azure AD.</span></span> <span data-ttu-id="89976-132">이 설정보다 더 자주 동기화할 수 없으며 계속 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="89976-132">You cannot synchronize more frequently than this setting and still be supported.</span></span>
* <span data-ttu-id="89976-133">**CurrentlyEffectiveSyncCycleInterval**.</span><span class="sxs-lookup"><span data-stu-id="89976-133">**CurrentlyEffectiveSyncCycleInterval**.</span></span> <span data-ttu-id="89976-134">hello 일정 현재 적용에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-134">hello schedule currently in effect.</span></span> <span data-ttu-id="89976-135">Hello CustomizedSyncInterval과 같은 값인 있기 (하는 경우 설정) AllowedSyncInterval 보다 더 잦은 빈도로 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="89976-135">It has hello same value as CustomizedSyncInterval (if set) if it is not more frequent than AllowedSyncInterval.</span></span> <span data-ttu-id="89976-136">1.1.281 이전 빌드를 사용하고 CustomizedSyncCycleInterval을 변경한 경우 이 변경 내용은 다음 동기화 주기 후에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="89976-136">If you use a build before 1.1.281 and you change CustomizedSyncCycleInterval, this change takes effect after next synchronization cycle.</span></span> <span data-ttu-id="89976-137">1.1.281 빌드에서 hello 변경 즉시 적용이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89976-137">From build 1.1.281 hello change takes effect immediately.</span></span>
* <span data-ttu-id="89976-138">**CustomizedSyncCycleInterval**.</span><span class="sxs-lookup"><span data-stu-id="89976-138">**CustomizedSyncCycleInterval**.</span></span> <span data-ttu-id="89976-139">30 분 hello 기본값과 빈도로 hello 스케줄러 toorun 하려는 경우이 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-139">If you want hello scheduler toorun at any other frequency than hello default 30 minutes, then you configure this setting.</span></span> <span data-ttu-id="89976-140">위의 hello 그림에서 hello 스케줄러 설정한 toorun 매시간 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-140">In hello picture above, hello scheduler has been set toorun every hour instead.</span></span> <span data-ttu-id="89976-141">이 설정은 tooa 값을 설정 하면 AllowedSyncInterval 보다 낮은 경우 후자 hello 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89976-141">If you set this setting tooa value lower than AllowedSyncInterval, then hello latter is used.</span></span>
* <span data-ttu-id="89976-142">**NextSyncCyclePolicyType**.</span><span class="sxs-lookup"><span data-stu-id="89976-142">**NextSyncCyclePolicyType**.</span></span> <span data-ttu-id="89976-143">델타 또는 초기입니다.</span><span class="sxs-lookup"><span data-stu-id="89976-143">Either Delta or Initial.</span></span> <span data-ttu-id="89976-144">다음 실행 하는 hello 프로세스 델타 변경 내용만 해야 하거나 hello 다음 실행 작업을 수행 해야 전체 정의 가져오기 및 동기화 합니다. 후자의 hello 또한 새롭거나 변경 된 모든 규칙을 다시 처리 것입니다.</span><span class="sxs-lookup"><span data-stu-id="89976-144">Defines if hello next run should only process delta changes, or if hello next run should do a full import and sync. hello latter would also reprocess any new or changed rules.</span></span>
* <span data-ttu-id="89976-145">**NextSyncCycleStartTimeInUTC**.</span><span class="sxs-lookup"><span data-stu-id="89976-145">**NextSyncCycleStartTimeInUTC**.</span></span> <span data-ttu-id="89976-146">다음 번 hello 스케줄러 시작 hello 다음 동기화 주기 합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-146">Next time hello scheduler starts hello next sync cycle.</span></span>
* <span data-ttu-id="89976-147">**PurgeRunHistoryInterval**.</span><span class="sxs-lookup"><span data-stu-id="89976-147">**PurgeRunHistoryInterval**.</span></span> <span data-ttu-id="89976-148">hello 시간 작업 로그를 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-148">hello time operation logs should be kept.</span></span> <span data-ttu-id="89976-149">이러한 로그는 hello 동기화 서비스 관리자에서 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89976-149">These logs can be reviewed in hello synchronization service manager.</span></span> <span data-ttu-id="89976-150">기본 hello 7 일 동안 tookeep 이러한 로그 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89976-150">hello default is tookeep these logs for 7 days.</span></span>
* <span data-ttu-id="89976-151">**SyncCycleEnabled**.</span><span class="sxs-lookup"><span data-stu-id="89976-151">**SyncCycleEnabled**.</span></span> <span data-ttu-id="89976-152">경우 hello 스케줄러가 실행 되 고 hello 가져오기, 동기화 및 내보내기 프로세스는 작업의 일부로 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="89976-152">Indicates if hello scheduler is running hello import, sync, and export processes as part of its operation.</span></span>
* <span data-ttu-id="89976-153">**MaintenanceEnabled**.</span><span class="sxs-lookup"><span data-stu-id="89976-153">**MaintenanceEnabled**.</span></span> <span data-ttu-id="89976-154">Hello 유지 관리 프로세스를 사용 하는 경우를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="89976-154">Shows if hello maintenance process is enabled.</span></span> <span data-ttu-id="89976-155">Hello 인증서/키를 업데이트 하 고 제거 작업 로그 hello 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="89976-155">It updates hello certificates/keys and purges hello operations log.</span></span>
* <span data-ttu-id="89976-156">**StagingModeEnabled**.</span><span class="sxs-lookup"><span data-stu-id="89976-156">**StagingModeEnabled**.</span></span> <span data-ttu-id="89976-157">[스테이징 모드](active-directory-aadconnectsync-operations.md#staging-mode)를 사용할 수 있는지 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-157">Shows if [staging mode](active-directory-aadconnectsync-operations.md#staging-mode) is enabled.</span></span> <span data-ttu-id="89976-158">이 설정을 사용 하는 경우 다음 표시 되지 않도록 hello 내보내기 실행에서 되지만 여전히 가져오기 및 동기화를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-158">If this setting is enabled, then it suppresses hello exports from running but still run import and synchronization.</span></span>
* <span data-ttu-id="89976-159">**SchedulerSuspended**.</span><span class="sxs-lookup"><span data-stu-id="89976-159">**SchedulerSuspended**.</span></span> <span data-ttu-id="89976-160">실행에서 하는 동안 업그레이드 tootemporarily 블록 hello 스케줄러 연결 하 여 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-160">Set by Connect during an upgrade tootemporarily block hello scheduler from running.</span></span>

<span data-ttu-id="89976-161">`Set-ADSyncScheduler`(으)로 이러한 모든 설정 중 일부를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89976-161">You can change some of these settings with `Set-ADSyncScheduler`.</span></span> <span data-ttu-id="89976-162">hello 매개 변수 뒤에 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89976-162">hello following parameters can be modified:</span></span>

* <span data-ttu-id="89976-163">CustomizedSyncCycleInterval</span><span class="sxs-lookup"><span data-stu-id="89976-163">CustomizedSyncCycleInterval</span></span>
* <span data-ttu-id="89976-164">NextSyncCyclePolicyType</span><span class="sxs-lookup"><span data-stu-id="89976-164">NextSyncCyclePolicyType</span></span>
* <span data-ttu-id="89976-165">PurgeRunHistoryInterval</span><span class="sxs-lookup"><span data-stu-id="89976-165">PurgeRunHistoryInterval</span></span>
* <span data-ttu-id="89976-166">SyncCycleEnabled</span><span class="sxs-lookup"><span data-stu-id="89976-166">SyncCycleEnabled</span></span>
* <span data-ttu-id="89976-167">MaintenanceEnabled</span><span class="sxs-lookup"><span data-stu-id="89976-167">MaintenanceEnabled</span></span>

<span data-ttu-id="89976-168">Azure AD Connect의 이전 빌드에서 **isStagingModeEnabled**는 Set-ADSyncScheduler에서 노출되었습니다.</span><span class="sxs-lookup"><span data-stu-id="89976-168">In earlier builds of Azure AD Connect, **isStagingModeEnabled** was exposed in Set-ADSyncScheduler.</span></span> <span data-ttu-id="89976-169">**지원 되지 않는** tooset이이 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="89976-169">It is **unsupported** tooset this property.</span></span> <span data-ttu-id="89976-170">속성을 hello **SchedulerSuspended** connect 수정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-170">hello property **SchedulerSuspended** should only be modified by Connect.</span></span> <span data-ttu-id="89976-171">**지원 되지 않는** tooset 직접 powershell이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89976-171">It is **unsupported** tooset this with PowerShell directly.</span></span>

<span data-ttu-id="89976-172">hello 스케줄러 구성은 Azure AD에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89976-172">hello scheduler configuration is stored in Azure AD.</span></span> <span data-ttu-id="89976-173">준비 서버를 설정한 경우 hello 주 서버의 모든 변경 (제외 IsStagingModeEnabled) 서버를 준비 하는 hello도 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89976-173">If you have a staging server, any change on hello primary server also affects hello staging server (except IsStagingModeEnabled).</span></span>

### <a name="customizedsynccycleinterval"></a><span data-ttu-id="89976-174">CustomizedSyncCycleInterval</span><span class="sxs-lookup"><span data-stu-id="89976-174">CustomizedSyncCycleInterval</span></span>
<span data-ttu-id="89976-175">구문: `Set-ADSyncScheduler -CustomizedSyncCycleInterval d.HH:mm:ss`</span><span class="sxs-lookup"><span data-stu-id="89976-175">Syntax: `Set-ADSyncScheduler -CustomizedSyncCycleInterval d.HH:mm:ss`</span></span>  
<span data-ttu-id="89976-176">d -일, HH - 시간, mm - 분, ss - 초</span><span class="sxs-lookup"><span data-stu-id="89976-176">d - days, HH - hours, mm - minutes, ss - seconds</span></span>

<span data-ttu-id="89976-177">예: `Set-ADSyncScheduler -CustomizedSyncCycleInterval 03:00:00`</span><span class="sxs-lookup"><span data-stu-id="89976-177">Example: `Set-ADSyncScheduler -CustomizedSyncCycleInterval 03:00:00`</span></span>  
<span data-ttu-id="89976-178">스케줄러 toorun 3 시간 마다 hello 하는 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-178">Changes hello scheduler toorun every 3 hours.</span></span>

<span data-ttu-id="89976-179">예: `Set-ADSyncScheduler -CustomizedSyncCycleInterval 1.0:0:0`</span><span class="sxs-lookup"><span data-stu-id="89976-179">Example: `Set-ADSyncScheduler -CustomizedSyncCycleInterval 1.0:0:0`</span></span>  
<span data-ttu-id="89976-180">변경은 hello 스케줄러 toorun를 매일 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89976-180">Changes change hello scheduler toorun daily.</span></span>

### <a name="disable-hello-scheduler"></a><span data-ttu-id="89976-181">Hello 스케줄러를 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="89976-181">Disable hello scheduler</span></span>  
<span data-ttu-id="89976-182">Toomake 구성을 변경 해야 할 경우 toodisable hello 스케줄러를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89976-182">If you need toomake configuration changes, then you want toodisable hello scheduler.</span></span> <span data-ttu-id="89976-183">예를 들어 있습니다 [필터링을 구성](active-directory-aadconnectsync-configure-filtering.md) 또는 [변경할 toosynchronization 규칙](active-directory-aadconnectsync-change-the-configuration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-183">For example, when you [configure filtering](active-directory-aadconnectsync-configure-filtering.md) or [make changes toosynchronization rules](active-directory-aadconnectsync-change-the-configuration.md).</span></span>

<span data-ttu-id="89976-184">실행 되는 toodisable hello 스케줄러 `Set-ADSyncScheduler -SyncCycleEnabled $false`합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-184">toodisable hello scheduler, run `Set-ADSyncScheduler -SyncCycleEnabled $false`.</span></span>

![Hello 스케줄러를 사용 하지 않도록 설정](./media/active-directory-aadconnectsync-change-the-configuration/schedulerdisable.png)

<span data-ttu-id="89976-186">변경 내용을 수행 했으면를 사용 하 여 다시 tooenable hello 스케줄러 잊지 마십시오 `Set-ADSyncScheduler -SyncCycleEnabled $true`합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-186">When you've made your changes, do not forget tooenable hello scheduler again with `Set-ADSyncScheduler -SyncCycleEnabled $true`.</span></span>

## <a name="start-hello-scheduler"></a><span data-ttu-id="89976-187">Hello 스케줄러를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-187">Start hello scheduler</span></span>
<span data-ttu-id="89976-188">hello 스케줄러는 기본적으로 30 분 마다 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-188">hello scheduler is by default run every 30 minutes.</span></span> <span data-ttu-id="89976-189">경우에 따라 동기화 주기 사이 hello toorun 주기를 예약 또는 toorun 다른 종류를 만들어야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89976-189">In some cases, you might want toorun a sync cycle in between hello scheduled cycles or you need toorun a different type.</span></span>

<span data-ttu-id="89976-190">**델타 동기화 주기**</span><span class="sxs-lookup"><span data-stu-id="89976-190">**Delta sync cycle**</span></span>  
<span data-ttu-id="89976-191">델타 동기화 주기 단계를 수행 하는 hello를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89976-191">A delta sync cycle includes hello following steps:</span></span>

* <span data-ttu-id="89976-192">모든 커넥터에서 델타 가져오기</span><span class="sxs-lookup"><span data-stu-id="89976-192">Delta import on all Connectors</span></span>
* <span data-ttu-id="89976-193">모든 커넥터에서 델타 동기화</span><span class="sxs-lookup"><span data-stu-id="89976-193">Delta sync on all Connectors</span></span>
* <span data-ttu-id="89976-194">모든 커넥터에서 내보내기</span><span class="sxs-lookup"><span data-stu-id="89976-194">Export on all Connectors</span></span>

<span data-ttu-id="89976-195">긴급 한 있다고 것 toomanually는 이유는 즉시 동기화 할 변경 주기를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-195">It could be that you have an urgent change that must be synchronized immediately, which is why you need toomanually run a cycle.</span></span> <span data-ttu-id="89976-196">Toomanually 해야 할 경우 주기를 실행 하는 PowerShell에서 다음 실행 `Start-ADSyncSyncCycle -PolicyType Delta`합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-196">If you need toomanually run a cycle, then from PowerShell run `Start-ADSyncSyncCycle -PolicyType Delta`.</span></span>

<span data-ttu-id="89976-197">**전체 동기화 주기**</span><span class="sxs-lookup"><span data-stu-id="89976-197">**Full sync cycle**</span></span>  
<span data-ttu-id="89976-198">Hello 구성 변경 내용이 다음 중 하나를 수행 해야 전체 동기화 주기 toorun (규칙 하위</span><span class="sxs-lookup"><span data-stu-id="89976-198">If you have made one of hello following configuration changes, you need toorun a full sync cycle (a.k.a.</span></span> <span data-ttu-id="89976-199">합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-199">Initial):</span></span>

* <span data-ttu-id="89976-200">원본 디렉터리에서 가져온 더 많은 개체 또는 특성 toobe 추가</span><span class="sxs-lookup"><span data-stu-id="89976-200">Added more objects or attributes toobe imported from a source directory</span></span>
* <span data-ttu-id="89976-201">변경 toohello 동기화 규칙</span><span class="sxs-lookup"><span data-stu-id="89976-201">Made changes toohello Synchronization rules</span></span>
* <span data-ttu-id="89976-202">다른 수의 개체가 포함되도록 [필터링](active-directory-aadconnectsync-configure-filtering.md) 변경</span><span class="sxs-lookup"><span data-stu-id="89976-202">Changed [filtering](active-directory-aadconnectsync-configure-filtering.md) so a different number of objects should be included</span></span>

<span data-ttu-id="89976-203">이러한 변경 중 하나를 수행 해야 toorun 전체 동기화 주기 hello 동기화 엔진이 hello 기회 tooreconsolidate hello 커넥터 공간을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="89976-203">If you have made one of these changes, then you need toorun a full sync cycle so hello sync engine has hello opportunity tooreconsolidate hello connector spaces.</span></span> <span data-ttu-id="89976-204">전체 동기화 주기 단계를 수행 하는 hello를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89976-204">A full sync cycle includes hello following steps:</span></span>

* <span data-ttu-id="89976-205">모든 커넥터에서 전체 가져오기</span><span class="sxs-lookup"><span data-stu-id="89976-205">Full Import on all Connectors</span></span>
* <span data-ttu-id="89976-206">모든 커넥터에서 전체 동기화</span><span class="sxs-lookup"><span data-stu-id="89976-206">Full Sync on all Connectors</span></span>
* <span data-ttu-id="89976-207">모든 커넥터에서 내보내기</span><span class="sxs-lookup"><span data-stu-id="89976-207">Export on all Connectors</span></span>

<span data-ttu-id="89976-208">전체 동기화 주기 tooinitiate 실행 `Start-ADSyncSyncCycle -PolicyType Initial` PowerShell 프롬프트에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-208">tooinitiate a full sync cycle, run `Start-ADSyncSyncCycle -PolicyType Initial` from a PowerShell prompt.</span></span> <span data-ttu-id="89976-209">이 명령은 전체 동기화 주기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-209">This command starts a full sync cycle.</span></span>

## <a name="stop-hello-scheduler"></a><span data-ttu-id="89976-210">Hello 스케줄러를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-210">Stop hello scheduler</span></span>
<span data-ttu-id="89976-211">Toostop hello 스케줄러 동기화 주기 현재 실행 중인 경우 필요할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="89976-211">If hello scheduler is currently running a synchronization cycle, you might need toostop it.</span></span> <span data-ttu-id="89976-212">예를 들어 hello 설치 마법사를 시작 하 고이 오류가 발생할 경우:</span><span class="sxs-lookup"><span data-stu-id="89976-212">For example if you start hello installation wizard and you get this error:</span></span>

![SyncCycleRunningError](./media/active-directory-aadconnectsync-feature-scheduler/synccyclerunningerror.png)

<span data-ttu-id="89976-214">동기화 주기를 실행 중일 때 구성을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="89976-214">When a sync cycle is running, you cannot make configuration changes.</span></span> <span data-ttu-id="89976-215">Hello 스케줄러 hello 프로세스 완료 되지만 변경 내용을 즉시 확인할 수 있도록 또한 중지할 수 있습니다 때까지 기다릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89976-215">You could wait until hello scheduler has finished hello process, but you can also stop it so you can make your changes immediately.</span></span> <span data-ttu-id="89976-216">현재 주기 hello 중지 유해한 아니며 보류 중인 변경 내용이 처리 된 다음 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-216">Stopping hello current cycle is not harmful and pending changes are processed with next run.</span></span>

1. <span data-ttu-id="89976-217">현재 hello 스케줄러 toostop 알림으로써 시작 hello PowerShell cmdlet과 주기 `Stop-ADSyncSyncCycle`합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-217">Start by telling hello scheduler toostop its current cycle with hello PowerShell cmdlet `Stop-ADSyncSyncCycle`.</span></span>
2. <span data-ttu-id="89976-218">경우 1.1.281, 전에 빌드를 사용 하 고 hello 스케줄러를 중지 해도 hello 현재는 현재 작업에서 커넥터입니다.</span><span class="sxs-lookup"><span data-stu-id="89976-218">If you use a build before 1.1.281, then stopping hello scheduler does not stop hello current Connector from its current task.</span></span> <span data-ttu-id="89976-219">tooforce 커넥터 toostop hello, 수행할 작업을 수행 하는 hello: ![StopAConnector](./media/active-directory-aadconnectsync-feature-scheduler/stopaconnector.png)</span><span class="sxs-lookup"><span data-stu-id="89976-219">tooforce hello Connector toostop, take hello following actions: ![StopAConnector](./media/active-directory-aadconnectsync-feature-scheduler/stopaconnector.png)</span></span>
   * <span data-ttu-id="89976-220">시작 **동기화 서비스** hello 시작 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-220">Start **Synchronization Service** from hello start menu.</span></span> <span data-ttu-id="89976-221">너무 이동**커넥터**, hello 커넥터 hello 상태로 강조 표시 **실행**를 선택 하 고 **중지** hello 동작에서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-221">Go too**Connectors**, highlight hello Connector with hello state **Running**, and select **Stop** from hello Actions.</span></span>

<span data-ttu-id="89976-222">hello 스케줄러 아직 활성 상태 이며 다음 기회에 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-222">hello scheduler is still active and starts again on next opportunity.</span></span>

## <a name="custom-scheduler"></a><span data-ttu-id="89976-223">사용자 지정 스케줄러</span><span class="sxs-lookup"><span data-stu-id="89976-223">Custom scheduler</span></span>
<span data-ttu-id="89976-224">hello이 섹션에 설명 된 cmdlet만에서 사용할 수 있는 빌드 [1.1.130.0](active-directory-aadconnect-version-history.md#111300) 이상.</span><span class="sxs-lookup"><span data-stu-id="89976-224">hello cmdlets documented in this section are only available in build [1.1.130.0](active-directory-aadconnect-version-history.md#111300) and later.</span></span>

<span data-ttu-id="89976-225">기본 제공 스케줄러 hello 요구 사항을 충족 하지 않으면, PowerShell을 사용 하 여 hello 커넥터를 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89976-225">If hello built-in scheduler does not satisfy your requirements, then you can schedule hello Connectors using PowerShell.</span></span>

### <a name="invoke-adsyncrunprofile"></a><span data-ttu-id="89976-226">Invoke-ADSyncRunProfile</span><span class="sxs-lookup"><span data-stu-id="89976-226">Invoke-ADSyncRunProfile</span></span>
<span data-ttu-id="89976-227">다음과 같이 커넥터에 대한 프로필을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89976-227">You can start a profile for a Connector in this way:</span></span>

```
Invoke-ADSyncRunProfile -ConnectorName "name of connector" -RunProfileName "name of profile"
```

<span data-ttu-id="89976-228">에 대 한 hello 이름 toouse [커넥터 이름](active-directory-aadconnectsync-service-manager-ui-connectors.md) 및 [실행 프로필 이름은](active-directory-aadconnectsync-service-manager-ui-connectors.md#configure-run-profiles) hello에서 찾을 수 [동기화 서비스 관리자 UI](active-directory-aadconnectsync-service-manager-ui.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-228">hello names toouse for [Connector names](active-directory-aadconnectsync-service-manager-ui-connectors.md) and [Run Profile Names](active-directory-aadconnectsync-service-manager-ui-connectors.md#configure-run-profiles) can be found in hello [Synchronization Service Manager UI](active-directory-aadconnectsync-service-manager-ui.md).</span></span>

![실행 프로필 호출](./media/active-directory-aadconnectsync-feature-scheduler/invokerunprofile.png)  

<span data-ttu-id="89976-230">hello `Invoke-ADSyncRunProfile` cmdlet은 동기, 즉, 돌아가지 않습니다 제어 성공적으로 또는 오류가 발생 하 여 hello 커넥터 hello 작업을 완료할 때까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-230">hello `Invoke-ADSyncRunProfile` cmdlet is synchronous, that is, it does not return control until hello Connector has completed hello operation, either successfully or with an error.</span></span>

<span data-ttu-id="89976-231">커넥터를 예약할 때 hello 좋습니다 tooschedule 순서에 따라 hello에서 해당:</span><span class="sxs-lookup"><span data-stu-id="89976-231">When you schedule your Connectors, hello recommendation is tooschedule them in hello following order:</span></span>

1. <span data-ttu-id="89976-232">(전체/델타) Active Directory와 같은 온-프레미스 디렉터리에서 가져오기</span><span class="sxs-lookup"><span data-stu-id="89976-232">(Full/Delta) Import from on-premises directories, such as Active Directory</span></span>
2. <span data-ttu-id="89976-233">(전체/델타) Azure AD에서 가져오기</span><span class="sxs-lookup"><span data-stu-id="89976-233">(Full/Delta) Import from Azure AD</span></span>
3. <span data-ttu-id="89976-234">(전체/델타) Active Directory와 같은 온-프레미스 디렉터리에서 동기화</span><span class="sxs-lookup"><span data-stu-id="89976-234">(Full/Delta) Synchronization from on-premises directories, such as Active Directory</span></span>
4. <span data-ttu-id="89976-235">(전체/델타) Azure AD에서 동기화</span><span class="sxs-lookup"><span data-stu-id="89976-235">(Full/Delta) Synchronization from Azure AD</span></span>
5. <span data-ttu-id="89976-236">TooAzure AD 내보내기</span><span class="sxs-lookup"><span data-stu-id="89976-236">Export tooAzure AD</span></span>
6. <span data-ttu-id="89976-237">내보내기 tooon 온-프레미스 디렉터리를 Active Directory와 같은</span><span class="sxs-lookup"><span data-stu-id="89976-237">Export tooon-premises directories, such as Active Directory</span></span>

<span data-ttu-id="89976-238">이 순서는 기본 제공 스케줄러 hello hello 커넥터를 실행 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="89976-238">This order is how hello built-in scheduler runs hello Connectors.</span></span>

### <a name="get-adsyncconnectorrunstatus"></a><span data-ttu-id="89976-239">Get-ADSyncConnectorRunStatus</span><span class="sxs-lookup"><span data-stu-id="89976-239">Get-ADSyncConnectorRunStatus</span></span>
<span data-ttu-id="89976-240">또한 사용 중인지 또는 유휴 상태 이면 hello 동기화 엔진 toosee를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89976-240">You can also monitor hello sync engine toosee if it is busy or idle.</span></span> <span data-ttu-id="89976-241">이 cmdlet는 동기화 엔진 hello 유휴 상태이 고 커넥터를 실행 되지 않는 경우 빈 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-241">This cmdlet returns an empty result if hello sync engine is idle and is not running a Connector.</span></span> <span data-ttu-id="89976-242">커넥터를 실행 중인 경우 hello 커넥터의 hello 이름을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-242">If a Connector is running, it returns hello name of hello Connector.</span></span>

```
Get-ADSyncConnectorRunStatus
```

![커넥터 실행 상태](./media/active-directory-aadconnectsync-feature-scheduler/getconnectorrunstatus.png)  
<span data-ttu-id="89976-244">위의 hello 그림에서 hello 첫 번째 줄은 hello 동기화 엔진은 유휴 상태에서입니다.</span><span class="sxs-lookup"><span data-stu-id="89976-244">In hello picture above, hello first line is from a state where hello sync engine is idle.</span></span> <span data-ttu-id="89976-245">hello hello Azure AD 커넥터를 실행 중인 경우에서 두 번째 줄.</span><span class="sxs-lookup"><span data-stu-id="89976-245">hello second line from when hello Azure AD Connector is running.</span></span>

## <a name="scheduler-and-installation-wizard"></a><span data-ttu-id="89976-246">스케줄러 및 설치 마법사</span><span class="sxs-lookup"><span data-stu-id="89976-246">Scheduler and installation wizard</span></span>
<span data-ttu-id="89976-247">Hello 설치 마법사를 시작 하는 경우 hello 스케줄러 일시적으로 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89976-247">If you start hello installation wizard, then hello scheduler is temporarily suspended.</span></span> <span data-ttu-id="89976-248">이 동작은 간주 되므로 구성을 변경 하 고 hello 동기화 엔진을 실행 하는 경우에 이러한 설정을 적용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="89976-248">This behavior is because it is assumed you make configuration changes and these settings cannot be applied if hello sync engine is actively running.</span></span> <span data-ttu-id="89976-249">이러한 이유로 두지 마십시오 hello 설치 마법사 열기 이후 모든 동기화 작업을 수행 하는 hello 동기화 엔진이 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-249">For this reason, do not leave hello installation wizard open since it stops hello sync engine from performing any synchronization actions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89976-250">다음 단계</span><span class="sxs-lookup"><span data-stu-id="89976-250">Next steps</span></span>
<span data-ttu-id="89976-251">Hello에 대 한 자세한 [Azure AD Connect 동기화](active-directory-aadconnectsync-whatis.md) 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="89976-251">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="89976-252">[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="89976-252">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
