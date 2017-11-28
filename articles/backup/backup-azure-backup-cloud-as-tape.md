---
title: "Azure 백업 tooreplace aaaUse 테이프 인프라 | Microsoft Docs"
description: "Azure 백업을 제공 하는 방법을 사용할 수 있는 테이프 같은 의미 체계가 toobackup 자세히 알아보고 Azure에서 데이터를 복원 합니다."
services: backup
documentationcenter: 
author: trinadhk
manager: vijayts
editor: 
ms.assetid: 2e1bb67d-986c-4437-8056-3a63169b4214
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 1/10/2017
ms.author: saurse;trinadhk;markgal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4c5b095d95d39267c54b1eed9427bda09658bb94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-your-long-term-storage-from-tape-toohello-azure-cloud"></a><span data-ttu-id="748db-103">테이프 toohello Azure 클라우드에서에서 장기 저장소를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="748db-103">Move your long-term storage from tape toohello Azure cloud</span></span>
<span data-ttu-id="748db-104">Azure 백업 및 System Center Data Protection Manager 고객은 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="748db-104">Azure Backup and System Center Data Protection Manager customers can:</span></span>

* <span data-ttu-id="748db-105">Hello 조직의 요구에 가장 적합 있는 일정의 데이터를 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="748db-105">Back up data in schedules which best suit hello organizational needs.</span></span>
* <span data-ttu-id="748db-106">시간이 늘어나면 hello 백업 데이터를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="748db-106">Retain hello backup data for longer periods</span></span>
* <span data-ttu-id="748db-107">장기 보존 시 (테이프 대신) Azure를 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="748db-107">Make Azure a part of their long-term retention needs (instead of tape).</span></span>

<span data-ttu-id="748db-108">이 문서에서는 고객이 백업 및 보존 정책을 사용 하도록 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="748db-108">This article explains how customers can enable backup and retention policies.</span></span> <span data-ttu-id="748db-109">Tooaddress 테이프를 사용 하는 고객의 장기-단기 보존 생깁니다이 기능의 hello 가용성은 강력 하 고 실행 가능한 대안이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="748db-109">Customers who use tapes tooaddress their long-term-retention needs now have a powerful and viable alternative with hello availability of this feature.</span></span> <span data-ttu-id="748db-110">hello에서 기능이 사용 되는지 hello Azure Backup의 최신 릴리스에 hello (사용 하지 않는 [여기](http://aka.ms/azurebackup_agent)).</span><span class="sxs-lookup"><span data-stu-id="748db-110">hello feature is enabled in hello latest release of hello Azure Backup (which is available [here](http://aka.ms/azurebackup_agent)).</span></span> <span data-ttu-id="748db-111">System Center DPM 고객을 업데이트 해야, 적어도 사용 하는 DPM을 사용 하기 전에 DPM 2012 R2 UR5 hello Azure 백업 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="748db-111">System Center DPM customers must update to, at least, DPM 2012 R2 UR5 before using DPM with hello Azure Backup service.</span></span>

## <a name="what-is-hello-backup-schedule"></a><span data-ttu-id="748db-112">백업 일정 hello 이란?</span><span class="sxs-lookup"><span data-stu-id="748db-112">What is hello Backup Schedule?</span></span>
<span data-ttu-id="748db-113">백업 일정 hello hello 백업 작업의 hello 빈도를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="748db-113">hello backup schedule indicates hello frequency of hello backup operation.</span></span> <span data-ttu-id="748db-114">예를 들어 hello 다음 화면에서에서 hello 설정에 따르면 자정에 및 매일 오후 6 시에 백업이 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="748db-114">For example, hello settings in hello following screen indicate that backups are taken daily at 6pm and at midnight.</span></span>

![일별 일정](./media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

<span data-ttu-id="748db-116">고객은 주간 백업을 예약할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="748db-116">Customers can also schedule a weekly backup.</span></span> <span data-ttu-id="748db-117">예를 들어 hello hello 다음 화면에서에서 설정을 나타낼는 백업 하는 모든 대체 일요일 & 수요일 오전 9시 30분부터 오전 1시입니다.</span><span class="sxs-lookup"><span data-stu-id="748db-117">For example, hello settings in hello following screen indicate that backups are taken every alternate Sunday & Wednesday at 9:30AM and 1:00AM.</span></span>

![주별 일정](./media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-hello-retention-policy"></a><span data-ttu-id="748db-119">Hello 보존 정책 이란?</span><span class="sxs-lookup"><span data-stu-id="748db-119">What is hello Retention Policy?</span></span>
<span data-ttu-id="748db-120">hello 보존 정책 hello 백업 해야 합니다 저장 되어야 하는 hello 기간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="748db-120">hello retention policy specifies hello duration for which hello backup must be stored.</span></span> <span data-ttu-id="748db-121">모든 백업 지점에 대 한 "플랫 정책"을 지정 하면, 대신 고객 hello 백업이 수행 되는 경우에 따라 서로 다른 보존 정책을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="748db-121">Rather than just specifying a “flat policy” for all backup points, customers can specify different retention policies based on when hello backup is taken.</span></span> <span data-ttu-id="748db-122">예를 들어 hello 백업 지점 매일 수행 작업 복구 지점으로 사용 하는 90 일 동안 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="748db-122">For example, hello backup point taken daily, which serves as an operational recovery point, is preserved for 90 days.</span></span> <span data-ttu-id="748db-123">더 긴 시간에 대 한 hello 감사 목적에 대 한 각 분기 끝에 수행 하는 hello 백업 지점 보존 됩니다.</span><span class="sxs-lookup"><span data-stu-id="748db-123">hello backup point taken at hello end of each quarter for audit purposes is preserved for a longer duration.</span></span>

![보존 정책](./media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

<span data-ttu-id="748db-125">hello 지점의 총 수 "보존"이이 정책에 지정 된은 90 (매일 포인트) + 40 (각각 10 년에 대 한 분기가) = 130입니다.</span><span class="sxs-lookup"><span data-stu-id="748db-125">hello total number of “retention points” specified in this policy is 90 (daily points) + 40 (one each quarter for 10 years) = 130.</span></span>

## <a name="example--putting-both-together"></a><span data-ttu-id="748db-126">예 - 두 가지를 결합</span><span class="sxs-lookup"><span data-stu-id="748db-126">Example – Putting both together</span></span>
![샘플 화면](./media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. <span data-ttu-id="748db-128">**일 단위 보존 정책**: 매일 수행된 백업이 7일 동안 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="748db-128">**Daily retention policy**: Backups taken daily are stored for seven days.</span></span>
2. <span data-ttu-id="748db-129">**주 단위 보존 정책**: 매주 토요일 자정과 오후 6시에 수행된 백업이 4주 동안 유지됩니다</span><span class="sxs-lookup"><span data-stu-id="748db-129">**Weekly retention policy**: Backups taken every day at midnight and 6PM Saturday are preserved for four weeks</span></span>
3. <span data-ttu-id="748db-130">**매월 보존 정책**: 자정과 6pm hello에 각 달의 마지막 토요일에 수행 된 백업을 12 개월 동안 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="748db-130">**Monthly retention policy**: Backups taken at midnight and 6pm on hello last Saturday of each month are preserved for 12 months</span></span>
4. <span data-ttu-id="748db-131">**연간 보존 정책**: 모든 3 월의 마지막 토요일 마다 자정 hello에 수행 된 백업을 10 년 동안 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="748db-131">**Yearly retention policy**: Backups taken at midnight on hello last Saturday of every March are preserved for 10 years</span></span>

<span data-ttu-id="748db-132">지점의 총 수 "보존" hello (고객 데이터를 복원할 수 있는 포인트) hello에 위의 다이어그램 다음과 같이 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="748db-132">hello total number of “retention points” (points from which a customer can restore data) in hello preceding diagram is computed as follows:</span></span>

* <span data-ttu-id="748db-133">7일 동안 매일 2지점 = 복구 지점 14개</span><span class="sxs-lookup"><span data-stu-id="748db-133">two points per day for seven days = 14 recovery points</span></span>
* <span data-ttu-id="748db-134">4주 동안 매주 2지점 = 복구 지점 8개</span><span class="sxs-lookup"><span data-stu-id="748db-134">two points per week for four weeks = 8 recovery points</span></span>
* <span data-ttu-id="748db-135">12개월 동안 매달 2지점 = 복구 지점 24개</span><span class="sxs-lookup"><span data-stu-id="748db-135">two points per month for 12 months = 24 recovery points</span></span>
* <span data-ttu-id="748db-136">10년 동안 매년 1지점 = 복구 지점 10개</span><span class="sxs-lookup"><span data-stu-id="748db-136">one point per year per 10 years = 10 recovery points</span></span>

<span data-ttu-id="748db-137">hello 총 복구 지점 수는 56 합니다.</span><span class="sxs-lookup"><span data-stu-id="748db-137">hello total number of recovery points is 56.</span></span>

> [!NOTE]
> <span data-ttu-id="748db-138">Azure 백업은 복구 지점 개수에 대한 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="748db-138">Azure backup doesn't have a restriction on number of recovery points.</span></span>
>
>

## <a name="advanced-configuration"></a><span data-ttu-id="748db-139">고급 구성</span><span class="sxs-lookup"><span data-stu-id="748db-139">Advanced configuration</span></span>
<span data-ttu-id="748db-140">클릭 하 여 **수정** hello 화면 앞에 고객이 더 이상 유연한 보존 일정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="748db-140">By clicking **Modify** in hello preceding screen, customers have further flexibility in specifying retention schedules.</span></span>

![수정](./media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a><span data-ttu-id="748db-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="748db-142">Next Steps</span></span>
<span data-ttu-id="748db-143">Azure 백업에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="748db-143">For more information about Azure Backup, see:</span></span>

* [<span data-ttu-id="748db-144">소개 tooAzure 백업</span><span class="sxs-lookup"><span data-stu-id="748db-144">Introduction tooAzure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="748db-145">Azure 백업 시도</span><span class="sxs-lookup"><span data-stu-id="748db-145">Try Azure Backup</span></span>](backup-try-azure-backup-in-10-mins.md)
