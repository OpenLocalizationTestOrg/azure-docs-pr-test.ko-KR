---
title: "Azure VM 백업 | Microsoft Docs"
description: "Azure 가상 컴퓨터를 검색하고, 등록하고, Recovery Services 자격 증명 모음에 백업합니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "가상 컴퓨터 백업; 가상 컴퓨터 백업; 백업 및 재해 복구; ARM VM 백업"
ms.assetid: 5c68481d-7be3-4e68-b87c-0961c267053e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: trinadhk;jimpark;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40983a3de104238d09b976b5fcf2419da42c1bba
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="back-up-azure-virtual-machines-to-a-recovery-services-vault"></a><span data-ttu-id="8501f-104">Recovery Services 자격 증명 모음에 Azure 가상 컴퓨터 백업</span><span class="sxs-lookup"><span data-stu-id="8501f-104">Back up Azure virtual machines to a Recovery Services vault</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8501f-105">복구 서비스 자격 증명 모음에 VM 백업</span><span class="sxs-lookup"><span data-stu-id="8501f-105">Back up VMs to Recovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="8501f-106">백업 자격 증명 모음에 VM 백업</span><span class="sxs-lookup"><span data-stu-id="8501f-106">Back up VMs to Backup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="8501f-107">이 문서에서는 Azure VM(Resource Manager 배포 및 클래식 배포 모두)을 Recovery Services 자격 증명 모음에 백업하는 방법에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-107">This article details how to back up Azure VMs (both Resource Manager-deployed and Classic-deployed) to a Recovery Services vault.</span></span> <span data-ttu-id="8501f-108">VM을 백업하기 위한 작업은 대부분 준비 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-108">Most of the work for backing up VMs is the preparation.</span></span> <span data-ttu-id="8501f-109">VM을 백업하거나 보호할 수 있으려면, VM을 보호하도록 환경을 준비하기 위한 [필수 구성 요소](backup-azure-arm-vms-prepare.md) 를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-109">Before you can back up or protect a VM, you must complete the [prerequisites](backup-azure-arm-vms-prepare.md) to prepare your environment for protecting your VMs.</span></span> <span data-ttu-id="8501f-110">필수 구성 요소를 완비하고 나면, VM의 스냅숏을 만드는 백업 작업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-110">Once you have completed the prerequisites, then you can initiate the backup operation to take snapshots of your VM.</span></span>


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

<span data-ttu-id="8501f-111">자세한 내용은 [Azure에서 VM 백업 인프라 계획](backup-azure-vms-introduction.md) 및 [Azure 가상 컴퓨터](https://azure.microsoft.com/documentation/services/virtual-machines/)에 대한 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8501f-111">For more information, see the articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

## <a name="triggering-the-backup-job"></a><span data-ttu-id="8501f-112">백업 작업 트리거</span><span class="sxs-lookup"><span data-stu-id="8501f-112">Triggering the backup job</span></span>
<span data-ttu-id="8501f-113">복구 서비스 자격 증명 모음과 연결된 백업 정책은, 백업 작업이 실행되는 빈도와 시기를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-113">The backup policy associated with the Recovery Services vault defines how often and when the backup operation runs.</span></span> <span data-ttu-id="8501f-114">기본적으로 첫 번째 예약된 백업은 초기 백업입니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-114">By default, the first scheduled backup is the initial backup.</span></span> <span data-ttu-id="8501f-115">초기 백업이 발생할 때까지 **백업 작업** 블레이드에서 최신 백업 상태가 **경고(초기 백업 보류 중)**로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-115">Until the initial backup occurs, the Last Backup Status on the **Backup Jobs** blade shows as **Warning(initial backup pending)**.</span></span>

![보류 중인 백업](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

<span data-ttu-id="8501f-117">초기 백업을 곧 시작할 예정이 아니라면 **지금 백업**을 실행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-117">Unless your initial backup is due to begin soon, it is recommended that you run **Back up Now**.</span></span> <span data-ttu-id="8501f-118">자격 증명 모음 대시보드에서 다음 절차가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-118">The following procedure starts from the vault dashboard.</span></span> <span data-ttu-id="8501f-119">이 절차는 모든 필수 구성 요소를 완비한 후에 초기 백업 작업을 실행하기 위한 용도입니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-119">This procedure serves for running the initial backup job after you have completed all prerequisites.</span></span> <span data-ttu-id="8501f-120">초기 백업 작업이 이미 실행되었으면, 이 절차는 제공되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-120">If the initial backup job has already been run, this procedure is not available.</span></span> <span data-ttu-id="8501f-121">연결된 백업 정책이 다음 백업 작업을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-121">The associated backup policy determines the next backup job.</span></span>  

<span data-ttu-id="8501f-122">초기 백업 작업을 실행하려면:</span><span class="sxs-lookup"><span data-stu-id="8501f-122">To run the initial backup job:</span></span>

1. <span data-ttu-id="8501f-123">자격 증명 모음 대시보드의 **백업 항목**에 있는 번호를 클릭하거나 **백업 항목** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-123">On the vault dashboard, click the number under **Backup Items**, or click the **Backup Items** tile.</span></span> <br/><span data-ttu-id="8501f-124">
  ![설정 아이콘](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span><span class="sxs-lookup"><span data-stu-id="8501f-124">
![Settings icon](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span></span>

  <span data-ttu-id="8501f-125">**백업 항목** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-125">The **Backup Items** blade opens.</span></span>

  ![항목 백업](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. <span data-ttu-id="8501f-127">**백업 항목** 블레이드에서 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-127">On the **Backup Items** blade, select the item.</span></span>

  ![설정 아이콘](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  <span data-ttu-id="8501f-129">**백업 항목** 목록이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-129">The **Backup Items** list opens.</span></span> <br/>

  ![백업 작업 트리거됨](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. <span data-ttu-id="8501f-131">**백업 항목** 목록에서 줄임표 **...**를 클릭하여 상황에 맞는 메뉴를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-131">On the **Backup Items** list, click the ellipses **...** to open the Context menu.</span></span>

  ![상황에 맞는 메뉴](./media/backup-azure-vms-first-look-arm/context-menu.png)

  <span data-ttu-id="8501f-133">상황에 맞는 메뉴가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-133">The Context menu appears.</span></span>

  ![상황에 맞는 메뉴](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. <span data-ttu-id="8501f-135">상황에 맞는 메뉴에서 **지금 백업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-135">On the Context menu, click **Backup now**.</span></span>

  ![상황에 맞는 메뉴](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  <span data-ttu-id="8501f-137">지금 백업 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-137">The Backup Now blade opens.</span></span>

  ![지금 백업 블레이드를 표시합니다.](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. <span data-ttu-id="8501f-139">지금 백업 블레이드에서 달력 아이콘을 클릭하고 달력 컨트롤을 사용하여 이 복구 지점을 유지할 마지막 날을 선택하고 **백업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-139">On the Backup Now blade, click the calendar icon, use the calendar control to select the last day this recovery point is retained, and click **Backup**.</span></span>

  ![지금 백업 복구 지점을 유지할 마지막 날을 설정합니다.](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  <span data-ttu-id="8501f-141">배포 알림을 통해 백업 작업이 트리거되고 백업 작업 페이지에서 작업의 진행률을 모니터링할 수 있다는 것을 알립니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-141">Deployment notifications let you know the backup job has been triggered, and that you can monitor the progress of the job on the Backup jobs page.</span></span> <span data-ttu-id="8501f-142">VM의 크기에 따라 초기 백업을 만드는 데 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-142">Depending on the size of your VM, creating the initial backup may take a while.</span></span>

6. <span data-ttu-id="8501f-143">초기 백업의 상태를 보거나 추적하려면 자격 증명 모음 대시보드의 **백업 작업** 타일에서 **진행 중**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-143">To view or track the status of the initial backup, on the vault dashboard, on the **Backup Jobs** tile click **In progress**.</span></span>

  ![백업 작업 타일](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  <span data-ttu-id="8501f-145">백업 작업 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-145">The Backup Jobs blade opens.</span></span>

  ![백업 작업 타일](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  <span data-ttu-id="8501f-147">**백업 작업** 블레이드에서 모든 작업의 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-147">In the **Backup jobs** blade, you can see the status of all jobs.</span></span> <span data-ttu-id="8501f-148">VM에 대한 백업 작업이 진행 중인지 또는 완료되었는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-148">Check if the backup job for your VM is still in progress, or if it has finished.</span></span> <span data-ttu-id="8501f-149">백업 작업이 완료되면 상태는 *완료됨*입니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-149">When a backup job is finished, the status is *Completed*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="8501f-150">백업 작업의 일부로 Azure 백업 서비스는 각 VM에서 백업 확장에 대한 명령을 발행하여 모든 쓰기를 플러시하고 일관된 스냅숏을 찍습니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-150">As a part of the backup operation, the Azure Backup service issues a command to the backup extension in each VM to flush all writes and take a consistent snapshot.</span></span>
  >
  >

## <a name="troubleshooting-errors"></a><span data-ttu-id="8501f-151">문제 해결 오류</span><span class="sxs-lookup"><span data-stu-id="8501f-151">Troubleshooting errors</span></span>
<span data-ttu-id="8501f-152">가상 컴퓨터를 백업하는 동안 문제가 발생한 경우 [VM 문제 해결 문서](backup-azure-vms-troubleshoot.md)의 도움말을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8501f-152">If you run into issues while backing up your virtual machine, see the [VM troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8501f-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8501f-153">Next steps</span></span>
<span data-ttu-id="8501f-154">VM을 보호했으므로 다음 문서를 확인하여 VM 관리 작업과 VM 복원 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8501f-154">Now that you have protected your VM, see the following articles to learn about VM management tasks, and how to restore VMs.</span></span>

* [<span data-ttu-id="8501f-155">가상 컴퓨터 관리 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="8501f-155">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="8501f-156">가상 컴퓨터 복원</span><span class="sxs-lookup"><span data-stu-id="8501f-156">Restore virtual machines</span></span>](backup-azure-arm-restore-vms.md)
