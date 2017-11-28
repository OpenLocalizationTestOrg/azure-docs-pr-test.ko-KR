---
title: Azure vm aaaBack | Microsoft Docs
description: "검색 하 고, 등록 및 Azure 가상 컴퓨터 tooa 복구 서비스 자격 증명 모음에 백업 합니다."
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
ms.openlocfilehash: a204a42726450a7fd89b5563a786b5070578b113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-tooa-recovery-services-vault"></a><span data-ttu-id="ce7cd-104">Azure 가상 컴퓨터를 백업 tooa 복구 서비스 자격 증명 모음에</span><span class="sxs-lookup"><span data-stu-id="ce7cd-104">Back up Azure virtual machines tooa Recovery Services vault</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ce7cd-105">Vm tooRecovery 서비스 자격 증명 모음에 백업</span><span class="sxs-lookup"><span data-stu-id="ce7cd-105">Back up VMs tooRecovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="ce7cd-106">Vm tooBackup 자격 증명 모음에 백업</span><span class="sxs-lookup"><span data-stu-id="ce7cd-106">Back up VMs tooBackup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="ce7cd-107">이 문서 tooback를 Azure Vm (리소스 관리자를 통해 배포 및 클래식 배포) tooa 복구 서비스 자격 증명 모음에 대해 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-107">This article details how tooback up Azure VMs (both Resource Manager-deployed and Classic-deployed) tooa Recovery Services vault.</span></span> <span data-ttu-id="ce7cd-108">대부분의 Vm를 백업 하기 위한 hello 작업 hello 준비입니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-108">Most of hello work for backing up VMs is hello preparation.</span></span> <span data-ttu-id="ce7cd-109">백업 또는 VM 보호를 완료 해야 hello [필수 구성 요소](backup-azure-arm-vms-prepare.md) tooprepare Vm을 보호 하기 위한 사용자 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-109">Before you can back up or protect a VM, you must complete hello [prerequisites](backup-azure-arm-vms-prepare.md) tooprepare your environment for protecting your VMs.</span></span> <span data-ttu-id="ce7cd-110">Hello 필수 구성 요소를 완료 한 후 VM의 hello 백업 작업 tootake 스냅숏을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-110">Once you have completed hello prerequisites, then you can initiate hello backup operation tootake snapshots of your VM.</span></span>


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

<span data-ttu-id="ce7cd-111">자세한 내용은에 hello 문서 참조 [Azure에서 VM 백업 인프라 계획](backup-azure-vms-introduction.md) 및 [Azure 가상 컴퓨터](https://azure.microsoft.com/documentation/services/virtual-machines/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-111">For more information, see hello articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

## <a name="triggering-hello-backup-job"></a><span data-ttu-id="ce7cd-112">Hello 백업 작업 트리거</span><span class="sxs-lookup"><span data-stu-id="ce7cd-112">Triggering hello backup job</span></span>
<span data-ttu-id="ce7cd-113">복구 서비스 자격 증명 모음에 hello와 연결 된 hello 백업 정책을 hello 백업 작업이 실행 되 고 빈도 및 시기를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-113">hello backup policy associated with hello Recovery Services vault defines how often and when hello backup operation runs.</span></span> <span data-ttu-id="ce7cd-114">기본적으로 첫 번째 예약 된 백업을 hello hello 초기 백업이입니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-114">By default, hello first scheduled backup is hello initial backup.</span></span> <span data-ttu-id="ce7cd-115">Hello 초기 백업을 수행 될 때까지 hello에서 마지막 백업 상태 hello **백업 작업** 블레이드로 표시 **경고 (초기 백업 보류 중인)**합니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-115">Until hello initial backup occurs, hello Last Backup Status on hello **Backup Jobs** blade shows as **Warning(initial backup pending)**.</span></span>

![보류 중인 백업](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

<span data-ttu-id="ce7cd-117">초기 백업 기간이 하지 않는 한 toobegin 곧 것이 좋습니다를 실행 하는 **지금 백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-117">Unless your initial backup is due toobegin soon, it is recommended that you run **Back up Now**.</span></span> <span data-ttu-id="ce7cd-118">hello 다음 절차에서에서 시작 hello 자격 증명 모음 대시보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-118">hello following procedure starts from hello vault dashboard.</span></span> <span data-ttu-id="ce7cd-119">이 절차는 모든 필수 구성 요소를 완료 한 후 hello 초기 백업 작업을 실행 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-119">This procedure serves for running hello initial backup job after you have completed all prerequisites.</span></span> <span data-ttu-id="ce7cd-120">Hello 초기 백업 작업을 이미 실행 하는 경우이 절차 ´ ù.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-120">If hello initial backup job has already been run, this procedure is not available.</span></span> <span data-ttu-id="ce7cd-121">hello 연결 된 백업 정책에 따라 결정 hello 다음 백업 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-121">hello associated backup policy determines hello next backup job.</span></span>  

<span data-ttu-id="ce7cd-122">toorun hello 초기 백업 작업:</span><span class="sxs-lookup"><span data-stu-id="ce7cd-122">toorun hello initial backup job:</span></span>

1. <span data-ttu-id="ce7cd-123">Hello 자격 증명 모음 대시보드에서 hello 숫자 아래를 클릭 합니다. **백업 항목**, 하거나 클릭 hello **백업 항목** 바둑판식으로 배열 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-123">On hello vault dashboard, click hello number under **Backup Items**, or click hello **Backup Items** tile.</span></span> <br/><span data-ttu-id="ce7cd-124">
  ![설정 아이콘](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span><span class="sxs-lookup"><span data-stu-id="ce7cd-124">
![Settings icon](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span></span>

  <span data-ttu-id="ce7cd-125">hello **백업 항목** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-125">hello **Backup Items** blade opens.</span></span>

  ![항목 백업](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. <span data-ttu-id="ce7cd-127">Hello에 **백업 항목** 블레이드, hello 선택 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-127">On hello **Backup Items** blade, select hello item.</span></span>

  ![설정 아이콘](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  <span data-ttu-id="ce7cd-129">hello **백업 항목** 목록 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-129">hello **Backup Items** list opens.</span></span> <br/>

  ![백업 작업 트리거됨](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. <span data-ttu-id="ce7cd-131">Hello에 **백업 항목** 목록에서 줄임표 hello **...**  tooopen hello 상황에 맞는 메뉴입니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-131">On hello **Backup Items** list, click hello ellipses **...** tooopen hello Context menu.</span></span>

  ![상황에 맞는 메뉴](./media/backup-azure-vms-first-look-arm/context-menu.png)

  <span data-ttu-id="ce7cd-133">hello 상황에 맞는 메뉴가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-133">hello Context menu appears.</span></span>

  ![상황에 맞는 메뉴](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. <span data-ttu-id="ce7cd-135">Hello 상황에 맞는 메뉴에서 클릭 **지금 백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-135">On hello Context menu, click **Backup now**.</span></span>

  ![상황에 맞는 메뉴](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  <span data-ttu-id="ce7cd-137">hello 지금 백업 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-137">hello Backup Now blade opens.</span></span>

  ![hello 지금 백업 블레이드를 표시합니다.](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. <span data-ttu-id="ce7cd-139">Hello 지금 백업 블레이드의 hello 달력 아이콘을 hello 달력 컨트롤 tooselect hello 마지막 날이 복구 지점을 유지 하 고 클릭을 사용 하 여 **백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-139">On hello Backup Now blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>

  ![hello 마지막 날 hello 지금 백업 복구 지점을 유지 되는 설정](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  <span data-ttu-id="ce7cd-141">배포 알림 hello 백업 작업 트리거 되었으며 hello 작업 hello 백업 작업 페이지의 hello 진행률을 모니터링할 수 있습니다 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-141">Deployment notifications let you know hello backup job has been triggered, and that you can monitor hello progress of hello job on hello Backup jobs page.</span></span> <span data-ttu-id="ce7cd-142">VM의 hello 크기에 따라 hello 초기 백업을 만드는 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-142">Depending on hello size of your VM, creating hello initial backup may take a while.</span></span>

6. <span data-ttu-id="ce7cd-143">hello에 hello 자격 증명 모음 대시보드에서 hello 초기 백업 tooview 또는 트랙 hello 상태 **백업 작업** 타일 클릭 **진행에서**합니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-143">tooview or track hello status of hello initial backup, on hello vault dashboard, on hello **Backup Jobs** tile click **In progress**.</span></span>

  ![백업 작업 타일](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  <span data-ttu-id="ce7cd-145">hello 백업 작업이 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-145">hello Backup Jobs blade opens.</span></span>

  ![백업 작업 타일](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  <span data-ttu-id="ce7cd-147">Hello에 **백업 작업** 블레이드에서 모든 작업의 hello 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-147">In hello **Backup jobs** blade, you can see hello status of all jobs.</span></span> <span data-ttu-id="ce7cd-148">Hello VM에 대 한 백업 작업이 아직 진행 중인 경우, 또는 마친 경우 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-148">Check if hello backup job for your VM is still in progress, or if it has finished.</span></span> <span data-ttu-id="ce7cd-149">백업 작업이 완료 되 면 hello 상태는 *Completed*합니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-149">When a backup job is finished, hello status is *Completed*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="ce7cd-150">Hello 백업 작업의 일부로 hello Azure 백업 서비스에 모두 작성 하 고 일관 된 스냅숏을 각 VM tooflush 명령 toohello 백업 확장을 발급 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-150">As a part of hello backup operation, hello Azure Backup service issues a command toohello backup extension in each VM tooflush all writes and take a consistent snapshot.</span></span>
  >
  >

## <a name="troubleshooting-errors"></a><span data-ttu-id="ce7cd-151">문제 해결 오류</span><span class="sxs-lookup"><span data-stu-id="ce7cd-151">Troubleshooting errors</span></span>
<span data-ttu-id="ce7cd-152">가상 컴퓨터를 백업 하는 동안 문제를 실행 하면 참조 hello [VM 문제 해결 문서](backup-azure-vms-troubleshoot.md) 에 대 한 도움말입니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-152">If you run into issues while backing up your virtual machine, see hello [VM troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce7cd-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ce7cd-153">Next steps</span></span>
<span data-ttu-id="ce7cd-154">지금 VM을 보호 하는 참조 문서 toolearn VM 관리 작업에 대 한 다음 hello와 방법을 toorestore Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="ce7cd-154">Now that you have protected your VM, see hello following articles toolearn about VM management tasks, and how toorestore VMs.</span></span>

* [<span data-ttu-id="ce7cd-155">가상 컴퓨터 관리 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="ce7cd-155">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="ce7cd-156">가상 컴퓨터 복원</span><span class="sxs-lookup"><span data-stu-id="ce7cd-156">Restore virtual machines</span></span>](backup-azure-arm-restore-vms.md)
