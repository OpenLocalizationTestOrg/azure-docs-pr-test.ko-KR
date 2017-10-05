---
title: "Azure 백업을 사용하여 테이프 인프라 대체ㅣMicrosoft Docs"
description: "Azure 백업이 Azure에서 데이터를 백업하고 복원할 수 있도록 하는 테이프와 같은 의미 체계를 제공하는 방법을 알아봅니다."
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
ms.openlocfilehash: f0f3152daf5f91f7c9e540797bf09b21969d2d33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="move-your-long-term-storage-from-tape-to-the-azure-cloud"></a><span data-ttu-id="d2f20-103">장기 저장소를 테이프에서 Azure 클라우드로 이동</span><span class="sxs-lookup"><span data-stu-id="d2f20-103">Move your long-term storage from tape to the Azure cloud</span></span>
<span data-ttu-id="d2f20-104">Azure 백업 및 System Center Data Protection Manager 고객은 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2f20-104">Azure Backup and System Center Data Protection Manager customers can:</span></span>

* <span data-ttu-id="d2f20-105">해당 조직의 요구에 가장 적합한 일정으로 데이터를 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="d2f20-105">Back up data in schedules which best suit the organizational needs.</span></span>
* <span data-ttu-id="d2f20-106">백업 데이터를 더 오랜 기간 동안 보존</span><span class="sxs-lookup"><span data-stu-id="d2f20-106">Retain the backup data for longer periods</span></span>
* <span data-ttu-id="d2f20-107">장기 보존 시 (테이프 대신) Azure를 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="d2f20-107">Make Azure a part of their long-term retention needs (instead of tape).</span></span>

<span data-ttu-id="d2f20-108">이 문서에서는 고객이 백업 및 보존 정책을 사용 하도록 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d2f20-108">This article explains how customers can enable backup and retention policies.</span></span> <span data-ttu-id="d2f20-109">테이프를 사용하여 장기 보존 요구 사항을 해결하는 고객들은 이제 이 기능을 사용하여 강력하고 실행 가능한 대안을 마련할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2f20-109">Customers who use tapes to address their long-term-retention needs now have a powerful and viable alternative with the availability of this feature.</span></span> <span data-ttu-id="d2f20-110">이 기능은 Azure 백업의 최신 릴리스( [여기](http://aka.ms/azurebackup_agent)에서 사용 가능)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2f20-110">The feature is enabled in the latest release of the Azure Backup (which is available [here](http://aka.ms/azurebackup_agent)).</span></span> <span data-ttu-id="d2f20-111">System Center DPM 고객은 DPM을 Azure Backup 서비스에 사용하려면 먼저 DPM 2012 R2 UR5 이상으로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2f20-111">System Center DPM customers must update to, at least, DPM 2012 R2 UR5 before using DPM with the Azure Backup service.</span></span>

## <a name="what-is-the-backup-schedule"></a><span data-ttu-id="d2f20-112">백업 일정은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d2f20-112">What is the Backup Schedule?</span></span>
<span data-ttu-id="d2f20-113">백업 일정은 백업 작업의 빈도를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d2f20-113">The backup schedule indicates the frequency of the backup operation.</span></span> <span data-ttu-id="d2f20-114">예를 들어, 다음 화면의 설정은 백업이 매일 오후 6시와 자정에 수행되는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d2f20-114">For example, the settings in the following screen indicate that backups are taken daily at 6pm and at midnight.</span></span>

![일별 일정](./media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

<span data-ttu-id="d2f20-116">고객은 주간 백업을 예약할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2f20-116">Customers can also schedule a weekly backup.</span></span> <span data-ttu-id="d2f20-117">예를 들어, 다음 화면의 설정은 백업이 매주 일요일과 수요일 오전 9시 30분과 새벽 1시에 번갈아서 수행되는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="d2f20-117">For example, the settings in the following screen indicate that backups are taken every alternate Sunday & Wednesday at 9:30AM and 1:00AM.</span></span>

![주별 일정](./media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-the-retention-policy"></a><span data-ttu-id="d2f20-119">보존 정책은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d2f20-119">What is the Retention Policy?</span></span>
<span data-ttu-id="d2f20-120">보존 정책은 백업의 저장 기간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d2f20-120">The retention policy specifies the duration for which the backup must be stored.</span></span> <span data-ttu-id="d2f20-121">모든 백업 지점에 대한 "일반 정책"을 지정하는 대신 백업이 수행되는 시기에 따라 다른 보존 정책을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2f20-121">Rather than just specifying a “flat policy” for all backup points, customers can specify different retention policies based on when the backup is taken.</span></span> <span data-ttu-id="d2f20-122">예를 들어 매일 수행된 백업 지점(작업 복구 지점으로 사용됨)은 90일 동안 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2f20-122">For example, the backup point taken daily, which serves as an operational recovery point, is preserved for 90 days.</span></span> <span data-ttu-id="d2f20-123">감사를 위해 매분기 말에 수행한 백업 지점은 더 오래 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2f20-123">The backup point taken at the end of each quarter for audit purposes is preserved for a longer duration.</span></span>

![보존 정책](./media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

<span data-ttu-id="d2f20-125">이 정책에 지정된 "보존 지점"의 총 수는 90(일별 지점) + 40(10년 동안 각 분기별) = 130입니다.</span><span class="sxs-lookup"><span data-stu-id="d2f20-125">The total number of “retention points” specified in this policy is 90 (daily points) + 40 (one each quarter for 10 years) = 130.</span></span>

## <a name="example--putting-both-together"></a><span data-ttu-id="d2f20-126">예 - 두 가지를 결합</span><span class="sxs-lookup"><span data-stu-id="d2f20-126">Example – Putting both together</span></span>
![샘플 화면](./media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. <span data-ttu-id="d2f20-128">**일 단위 보존 정책**: 매일 수행된 백업이 7일 동안 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2f20-128">**Daily retention policy**: Backups taken daily are stored for seven days.</span></span>
2. <span data-ttu-id="d2f20-129">**주 단위 보존 정책**: 매주 토요일 자정과 오후 6시에 수행된 백업이 4주 동안 유지됩니다</span><span class="sxs-lookup"><span data-stu-id="d2f20-129">**Weekly retention policy**: Backups taken every day at midnight and 6PM Saturday are preserved for four weeks</span></span>
3. <span data-ttu-id="d2f20-130">**월 단위 보존 정책**: 매달 마지막 주 토요일 자정과 오후 6시에 수행된 백업이 12개월 동안 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2f20-130">**Monthly retention policy**: Backups taken at midnight and 6pm on the last Saturday of each month are preserved for 12 months</span></span>
4. <span data-ttu-id="d2f20-131">**연 단위 보존 정책**: 매년 3월 마지막 주 토요일 자정에 수행된 백업이 10년 동안 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2f20-131">**Yearly retention policy**: Backups taken at midnight on the last Saturday of every March are preserved for 10 years</span></span>

<span data-ttu-id="d2f20-132">앞의 도표에서 "보존 지점"(데이터를 복원할 수 있는 지점)의 총 수는 다음과 같이 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2f20-132">The total number of “retention points” (points from which a customer can restore data) in the preceding diagram is computed as follows:</span></span>

* <span data-ttu-id="d2f20-133">7일 동안 매일 2지점 = 복구 지점 14개</span><span class="sxs-lookup"><span data-stu-id="d2f20-133">two points per day for seven days = 14 recovery points</span></span>
* <span data-ttu-id="d2f20-134">4주 동안 매주 2지점 = 복구 지점 8개</span><span class="sxs-lookup"><span data-stu-id="d2f20-134">two points per week for four weeks = 8 recovery points</span></span>
* <span data-ttu-id="d2f20-135">12개월 동안 매달 2지점 = 복구 지점 24개</span><span class="sxs-lookup"><span data-stu-id="d2f20-135">two points per month for 12 months = 24 recovery points</span></span>
* <span data-ttu-id="d2f20-136">10년 동안 매년 1지점 = 복구 지점 10개</span><span class="sxs-lookup"><span data-stu-id="d2f20-136">one point per year per 10 years = 10 recovery points</span></span>

<span data-ttu-id="d2f20-137">복구 지점의 총 수는 56개입니다.</span><span class="sxs-lookup"><span data-stu-id="d2f20-137">The total number of recovery points is 56.</span></span>

> [!NOTE]
> <span data-ttu-id="d2f20-138">Azure 백업은 복구 지점 개수에 대한 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d2f20-138">Azure backup doesn't have a restriction on number of recovery points.</span></span>
>
>

## <a name="advanced-configuration"></a><span data-ttu-id="d2f20-139">고급 구성</span><span class="sxs-lookup"><span data-stu-id="d2f20-139">Advanced configuration</span></span>
<span data-ttu-id="d2f20-140">앞의 화면에서 **수정** 을 클릭하면 보존 일정을 더 유연하게 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2f20-140">By clicking **Modify** in the preceding screen, customers have further flexibility in specifying retention schedules.</span></span>

![수정](./media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a><span data-ttu-id="d2f20-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d2f20-142">Next Steps</span></span>
<span data-ttu-id="d2f20-143">Azure 백업에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2f20-143">For more information about Azure Backup, see:</span></span>

* [<span data-ttu-id="d2f20-144">Azure 백업 소개</span><span class="sxs-lookup"><span data-stu-id="d2f20-144">Introduction to Azure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="d2f20-145">Azure 백업 시도</span><span class="sxs-lookup"><span data-stu-id="d2f20-145">Try Azure Backup</span></span>](backup-try-azure-backup-in-10-mins.md)
