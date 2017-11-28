---
title: "aaaAzure VM 백업 FAQ | Microsoft Docs"
description: "에 대 한 toocommon 질문에 답변: Azure VM의 백업 작동, 제한 사항 및 어떤 상황이 발생 하는 방법 변경 toopolicy 발생 하는 경우"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "Azure VM 백업, Azure VM 복원, 백업 정책"
ms.assetid: c4cd7ff6-8206-45a3-adf5-787f64dbd7e1
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: trinadhk;pullabhk;
ms.openlocfilehash: a1ad2cb3a379577a8c4258c8207ce75809e11a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-vm-backup-service"></a><span data-ttu-id="f2151-104">Hello Azure VM 백업 서비스에 대 한 질문</span><span class="sxs-lookup"><span data-stu-id="f2151-104">Questions about hello Azure VM Backup service</span></span>
<span data-ttu-id="f2151-105">이 기술 자료이 문서에 대 한 답변 toocommon 질문 toohelp hello Azure VM 백업 구성 요소를 신속 하 게 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2151-105">This article has answers toocommon questions toohelp you quickly understand hello Azure VM Backup components.</span></span> <span data-ttu-id="f2151-106">일부 hello 대답의 링크 toohello 문서 포괄적인 정보가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2151-106">In some of hello answers, there are links toohello articles that have comprehensive information.</span></span> <span data-ttu-id="f2151-107">Hello에 hello Azure 백업 서비스에 대 한 질문을 게시할 수도 있습니다 [토론 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2151-107">You can also post questions about hello Azure Backup service in hello [discussion forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).</span></span>

## <a name="configure-backup"></a><span data-ttu-id="f2151-108">백업 구성</span><span class="sxs-lookup"><span data-stu-id="f2151-108">Configure backup</span></span>
### <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a><span data-ttu-id="f2151-109">Recovery Services 자격 증명 모음은 클래식 VM 또는 Resource Manager 기반 VM을 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="f2151-109">Do Recovery Services vaults support classic VMs or Resource Manager based VMs?</span></span> <br/>
<span data-ttu-id="f2151-110">Recovery Services 자격 증명 모음은 두 모델을 모두 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f2151-110">Recovery Services vaults support both models.</span></span>  <span data-ttu-id="f2151-111">클래식 (hello 클래식 포털에서 만든)를 VM 또는 복구 서비스 자격 증명 모음 (hello Azure 포털에서에서 만든) 리소스 관리자 VM tooa를 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2151-111">You can back up a classic VM (created in hello Classic portal), or a Resource Manager VM (created in hello Azure portal) tooa Recovery Services vault.</span></span>

### <a name="what-configurations-are-not-supported-by-azure-vm-backup-"></a><span data-ttu-id="f2151-112">Azure VM 백업에서 지원되지 않는 구성은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="f2151-112">What configurations are not supported by Azure VM backup ?</span></span>
<span data-ttu-id="f2151-113">[지원되는 운영 체제](backup-azure-arm-vms-prepare.md#supported-operating-system-for-backup) 및 [VM 백업 제한](backup-azure-arm-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2151-113">Please go through [Supported operating systems](backup-azure-arm-vms-prepare.md#supported-operating-system-for-backup) and [Limitations of VM backup](backup-azure-arm-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)</span></span>

### <a name="why-cant-i-see-my-vm-in-configure-backup-wizard"></a><span data-ttu-id="f2151-114">백업 구성 마법사에서 내 VM을 볼 수 없는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="f2151-114">Why can't I see my VM in configure backup wizard?</span></span>
<span data-ttu-id="f2151-115">백업 구성 마법사에서 Azure Backup은 다음과 같은 VM만 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="f2151-115">In Configure backup wizard, Azure Backup only lists VMs which are:</span></span>
* <span data-ttu-id="f2151-116">아직 보호-tooVM 블레이드를 이동 하 hello 블레이드의 설정 메뉴에서 백업 상태를 검사 하 여 VM의 hello 백업 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2151-116">Not already protected - You can verify hello backup status of a VM by going tooVM blade and checking on Backup status from Settings Menu of hello blade.</span></span> <span data-ttu-id="f2151-117">너무 자세한 방법에 대 한 자세한 내용은[VM의 백업 상태를 확인 합니다.](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-vm-management-blade)</span><span class="sxs-lookup"><span data-stu-id="f2151-117">Learn more on how too[Check backup status of a VM](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-vm-management-blade)</span></span>
* <span data-ttu-id="f2151-118">VM으로 toosame 영역 속한</span><span class="sxs-lookup"><span data-stu-id="f2151-118">Belongs toosame region as VM</span></span>

## <a name="backup"></a><span data-ttu-id="f2151-119">백업</span><span class="sxs-lookup"><span data-stu-id="f2151-119">Backup</span></span>
### <a name="will-on-demand-backup-job-follow-same-retention-schedule-as-scheduled-backups"></a><span data-ttu-id="f2151-120">주문형 백업 작업은 예약된 백업과 동일한 보존 일정을 따르나요?</span><span class="sxs-lookup"><span data-stu-id="f2151-120">Will on-demand backup job follow same retention schedule as scheduled backups?</span></span>
<span data-ttu-id="f2151-121">아니요.</span><span class="sxs-lookup"><span data-stu-id="f2151-121">No.</span></span> <span data-ttu-id="f2151-122">Toospecify hello 보존 범위는 요청 시 백업 작업에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f2151-122">You need toospecify hello retention range for an on-demand backup job.</span></span> <span data-ttu-id="f2151-123">기본적으로 포털에서 트리거된 이후 30일 동안 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2151-123">By default, it will be retained for 30 days when triggered from portal.</span></span> 

### <a name="i-recently-enabled-azure-disk-encryption-on-some-vms-will-my-backups-continue-toowork"></a><span data-ttu-id="f2151-124">최근에 일부 VM에서 Azure Disk Encryption을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2151-124">I recently enabled Azure Disk Encryption on some VMs.</span></span> <span data-ttu-id="f2151-125">백업이 계속 toowork?</span><span class="sxs-lookup"><span data-stu-id="f2151-125">Will my backups continue toowork?</span></span>
<span data-ttu-id="f2151-126">Azure 백업 서비스 tooaccess 주요 자격 증명 모음에 대 한 toogive 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2151-126">You need toogive permissions for Azure Backup service tooaccess Key Vault.</span></span> <span data-ttu-id="f2151-127">[PowerShell 설명서](backup-azure-vms-automation.md)의 *백업 사용* 섹션에서 설명하는 단계를 사용하여 PowerShell에서 이러한 권한을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2151-127">You can provide these permissions in PowerShell using steps mentioned in *Enable Backup* section of [PowerShell](backup-azure-vms-automation.md) documentation.</span></span>

### <a name="i-migrated-disks-of-a-vm-toomanaged-disks-will-my-backups-continue-toowork"></a><span data-ttu-id="f2151-128">I VM toomanaged 디스크의 디스크 마이그레이션됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2151-128">I migrated disks of a VM toomanaged disks.</span></span> <span data-ttu-id="f2151-129">백업이 계속 toowork?</span><span class="sxs-lookup"><span data-stu-id="f2151-129">Will my backups continue toowork?</span></span>
<span data-ttu-id="f2151-130">예, 백업을 원활 하 게 작동 하 고 필요 toore 없습니다-백업을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2151-130">Yes, backups work seamlessly and no need toore-configure backup.</span></span> 

## <a name="restore"></a><span data-ttu-id="f2151-131">복원</span><span class="sxs-lookup"><span data-stu-id="f2151-131">Restore</span></span>
### <a name="how-do-i-decide-between-restoring-disks-versus-full-vm-restore"></a><span data-ttu-id="f2151-132">디스크 복원과 전체 VM 복원 중에서 어떻게 결정해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="f2151-132">How do I decide between restoring disks versus full VM restore?</span></span>
<span data-ttu-id="f2151-133">복원된 VM에 대해 빠른 만들기 옵션을 사용하는 방법으로 Azure 전체 VM 복원을 생각해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2151-133">Think of Azure full VM restore as a way of quick create option for restored VM.</span></span> <span data-ttu-id="f2151-134">VM 복원 컨테이너에서 사용 하는 디스크, 공용 IP 주소, 네트워크 인터페이스를 가져오는 VM 만들기의 일부로 생성 된 리소스의 고유성에 대 한 이름, 옵션에는 디스크의 hello 이름이 변경 됩니다. 또한 hello VM tooavailability 집합 하지 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2151-134">Restore VM option will change hello names of disks, containers used by disks,public IP addresses, network interface names for uniqueness of resources getting created as part of VM creation.It will also not add hello VM tooavailability set.</span></span> 

<span data-ttu-id="f2151-135">복원 디스크를 사용하여 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2151-135">Use restore disks to:</span></span>
* <span data-ttu-id="f2151-136">Hello 백업 구성에서 hello 크기를 변경 하는 등의 시간 구성 요소에서 생성 되는 VM을 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="f2151-136">Customize hello VM that gets created from point in time configuration like changing hello size from backup configuration</span></span>
* <span data-ttu-id="f2151-137">백업 hello 시 존재 하지 않는 구성을 추가합니다</span><span class="sxs-lookup"><span data-stu-id="f2151-137">Add configurations which are not present at hello time of backup</span></span> 
* <span data-ttu-id="f2151-138">가져오는 생성 된 리소스에 대 한 제어 hello 명명 규칙</span><span class="sxs-lookup"><span data-stu-id="f2151-138">Control hello naming convention for resources getting created</span></span>
* <span data-ttu-id="f2151-139">VM tooavailability 집합 추가</span><span class="sxs-lookup"><span data-stu-id="f2151-139">Add VM tooavailability set</span></span>
* <span data-ttu-id="f2151-140">PowerShell/선언적 템플릿 정의를 통해서만 설정할 수 있는 구성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2151-140">You have any configuration which can be achieved only using PowerShell/a declarative template definition</span></span>

## <a name="manage-vm-backups"></a><span data-ttu-id="f2151-141">VM 백업 관리</span><span class="sxs-lookup"><span data-stu-id="f2151-141">Manage VM backups</span></span>
### <a name="what-happens-when-i-change-a-backup-policy-on-vms"></a><span data-ttu-id="f2151-142">VM에서 백업 정책을 변경하면 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="f2151-142">What happens when I change a backup policy on VM(s)?</span></span>
<span data-ttu-id="f2151-143">새 정책을 VM(s)에 적용 되 면 일정 및 보존 hello 새 정책의 뒤 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2151-143">When a new policy is applied on VM(s), schedule and retention of hello new policy will be followed.</span></span> <span data-ttu-id="f2151-144">보존을 연장 기존 복구 지점이 표시될지 tookeep 새 정책에 따라 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2151-144">If retention is extended, existing recovery points will be marked tookeep them as per new policy.</span></span> <span data-ttu-id="f2151-145">보존을 줄이면 정리 hello 다음 정리 작업에서 표시 되 고 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2151-145">If retention is reduced, they are marked for pruning in hello next cleanup job and will be deleted.</span></span> 
