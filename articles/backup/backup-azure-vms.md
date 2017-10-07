---
title: "Azure 가상 컴퓨터 클래식 배포 tooa 백업 자격 증명 모음을 aaaBack | Microsoft Docs"
description: "Azure 가상 컴퓨터 백업에 대한 이 절차를 사용하여 가상 컴퓨터 검색, 등록 및 백업합니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "가상 컴퓨터 백업; 가상 컴퓨터 백업 백업; 백업 및 재해 복구; VM 백업"
ms.assetid: c0ab5469-65fd-4af5-ae9b-f5d183f82ce8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 048e32d9b2bd5bdd7a125225a71a6d805bb4fbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a><span data-ttu-id="d8336-104">Azure Virtual Machines 백업(클래식 포털)</span><span class="sxs-lookup"><span data-stu-id="d8336-104">Back up Azure virtual machines (classic portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d8336-105">Vm tooRecovery 서비스 자격 증명 모음에 백업</span><span class="sxs-lookup"><span data-stu-id="d8336-105">Back up VMs tooRecovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="d8336-106">Vm tooBackup 자격 증명 모음에 백업</span><span class="sxs-lookup"><span data-stu-id="d8336-106">Back up VMs tooBackup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="d8336-107">이 문서는 클래식 배포 된 Azure 가상 컴퓨터 (VM) tooa 백업 자격 증명 모음에 백업에 대 한 hello 절차를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-107">This article provides hello procedures for backing up a Classic-deployed Azure virtual machine (VM) tooa Backup vault.</span></span> <span data-ttu-id="d8336-108">Azure 가상 컴퓨터를 백업할 수 전에의 care tootake 필요한 몇 가지 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-108">There are a few tasks you need tootake care of before you can back up an Azure virtual machine.</span></span> <span data-ttu-id="d8336-109">따라서, 전체 hello 아직 수행 하지 않은 경우 [필수 구성 요소](backup-azure-vms-prepare.md) tooprepare Vm에 백업에 대 한 사용자 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-109">If you haven't already done so, complete hello [prerequisites](backup-azure-vms-prepare.md) tooprepare your environment for backing up your VMs.</span></span>

<span data-ttu-id="d8336-110">자세한 내용은 hello 문서를 참조 [Azure에서 VM 백업 인프라 계획](backup-azure-vms-introduction.md) 및 [Azure 가상 컴퓨터](https://azure.microsoft.com/documentation/services/virtual-machines/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-110">For additional information, see hello articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

> [!NOTE]
> <span data-ttu-id="d8336-111">Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델인 [리소스 관리자와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-111">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d8336-112">백업 자격 증명 모음은 클래식 배포 VM만 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-112">A Backup vault can only protect Classic-deployed VMs.</span></span> <span data-ttu-id="d8336-113">백업 자격 증명 모음을 사용하여 Resource Manager 배포 VM을 보호할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-113">You cannot protect Resource Manager-deployed VMs with a Backup vault.</span></span> <span data-ttu-id="d8336-114">참조 [Vm tooRecovery 서비스 자격 증명 모음에 백업](backup-azure-arm-vms.md) 자격 증명 모음 복구 서비스 작업에 대 한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-114">See [Back up VMs tooRecovery Services vault](backup-azure-arm-vms.md) for details on working with Recovery Services vaults.</span></span>
>
>

<span data-ttu-id="d8336-115">Azure 가상 컴퓨터 백업에는 3가지 주요 단계가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-115">Backing up Azure virtual machines involves three key steps:</span></span>

![Azure IaaS VM을 tooback 세 단계](./media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> <span data-ttu-id="d8336-117">가상 컴퓨터 백업은 로컬 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-117">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="d8336-118">하나의 영역 tooa 백업 자격 증명 모음에 다른 지역에서 가상 컴퓨터를 백업할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-118">You cannot back up virtual machines in one region tooa backup vault in another region.</span></span> <span data-ttu-id="d8336-119">따라서 백업할 VM이 있는 각 Azure 지역에 백업 자격 증명 모음을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-119">So, you must create a backup vault in each Azure region, where there are VMs that will be backed up.</span></span>
>
> [!IMPORTANT]
> <span data-ttu-id="d8336-120">2017 년 3 월 부터는 hello 클래식 포털 toocreate 백업 자격 증명 모음은 더 이상 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-120">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
> <span data-ttu-id="d8336-121">이제 사용자 백업 자격 증명 모음 tooRecovery 서비스 자격 증명 모음을 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-121">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="d8336-122">자세한 내용은 hello 문서 참조 [복구 서비스 자격 증명 모음에 백업 자격 증명 모음 tooa 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-122">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="d8336-123">Microsoft는 것이 권장 tooupgrade 백업 tooRecovery 서비스 자격 증명 모음 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-123">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="d8336-124">2017 년 10 월 15 후 PowerShell toocreate 백업 자격 증명 모음을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-124">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="d8336-125">**2017년 11월 1일까지**:</span><span class="sxs-lookup"><span data-stu-id="d8336-125">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="d8336-126">모든 나머지 백업 자격 증명 모음을 자동으로 업그레이드 된 tooRecovery 서비스 자격 증명 모음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-126">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="d8336-127">하면 hello 클래식 포털에서 수 tooaccess 백업 데이터 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-127">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="d8336-128">대신, 복구 서비스 자격 증명 모음에 hello Azure 포털 tooaccess 백업 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-128">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="step-1---discover-azure-virtual-machines"></a><span data-ttu-id="d8336-129">1단계 - Azure 가상 컴퓨터 검색</span><span class="sxs-lookup"><span data-stu-id="d8336-129">Step 1 - Discover Azure virtual machines</span></span>
<span data-ttu-id="d8336-130">모든 새 가상 컴퓨터 (Vm) 추가 toohello 구독을 등록 하기 전에 식별 된 tooensure hello 검색 프로세스를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-130">tooensure any new virtual machines (VMs) added toohello subscription are identified before registering, run hello discovery process.</span></span> <span data-ttu-id="d8336-131">추가 정보와 함께 hello 구독에서 가상 컴퓨터의 hello 목록에 대 한 hello 프로세스 쿼리 Azure hello 클라우드 서비스 이름 및 hello 영역 같은입니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-131">hello process queries Azure for hello list of virtual machines in hello subscription, along with additional information like hello cloud service name and hello region.</span></span>

1. <span data-ttu-id="d8336-132">Toohello 로그인 [클래식 포털](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="d8336-132">Sign in toohello [Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="d8336-133">Hello Azure 서비스 목록에서 클릭 **복구 서비스** 의 백업 및 사이트 복구 자격 증명 모음 tooopen hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-133">In hello list of Azure services, click **Recovery Services** tooopen hello list of Backup and Site Recovery vaults.</span></span>
    <span data-ttu-id="d8336-134">![자격 증명 모음 목록 열기](./media/backup-azure-vms/choose-vault-list.png)</span><span class="sxs-lookup"><span data-stu-id="d8336-134">![Open vault list](./media/backup-azure-vms/choose-vault-list.png)</span></span>
3. <span data-ttu-id="d8336-135">백업 자격 증명 모음은의 hello 목록의 hello 자격 증명 모음 tooback VM 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-135">In hello list of Backup vaults, select hello vault tooback up a VM.</span></span>

    <span data-ttu-id="d8336-136">이 새로운 자격 증명 모음 hello 포털 toohello 열립니다 **빠른 시작** 페이지.</span><span class="sxs-lookup"><span data-stu-id="d8336-136">If this is a new vault hello portal opens toohello **Quick Start** page.</span></span>

    ![등록된 항목 열기 메뉴](./media/backup-azure-vms/vault-quick-start.png)

    <span data-ttu-id="d8336-138">이전에 구성 된 자격 증명 모음 hello hello 포털 가장 최근에 사용한 toohello 메뉴를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-138">If hello vault has previously been configured, hello portal opens toohello most recently used menu.</span></span>
4. <span data-ttu-id="d8336-139">Hello 자격 증명 모음의 메뉴에서 (hello 페이지의 위쪽 hello)를 클릭 **등록 된 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-139">From hello vault menu (at hello top of hello page), click **Registered Items**.</span></span>

    ![등록된 항목 열기 메뉴](./media/backup-azure-vms/vault-menu.png)
5. <span data-ttu-id="d8336-141">Hello에서 **형식** 메뉴 선택 **Azure 가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-141">From hello **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![워크로드 선택](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="d8336-143">클릭 **DISCOVER** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-143">Click **DISCOVER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="d8336-144">![검색 단추](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="d8336-144">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="d8336-145">hello 검색 프로세스는 hello 가상 컴퓨터 정리 된 되는 동안 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-145">hello discovery process may take a few minutes while hello virtual machines are being tabulated.</span></span> <span data-ttu-id="d8336-146">알림을 hello hello 프로세스가 실행 되 고 있는지 알려 주는 hello 화면 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-146">There is a notification at hello bottom of hello screen that lets you know that hello process is running.</span></span>

    ![VM 검색](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="d8336-148">hello 알림이 hello 프로세스가 완료 되 면 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-148">hello notification changes when hello process is complete.</span></span> <span data-ttu-id="d8336-149">Hello 검색 프로세스는 hello 가상 컴퓨터를 찾지 못했습니다 먼저 hello Vm 존재 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-149">If hello discovery process did not find hello virtual machines, first ensure hello VMs exist.</span></span> <span data-ttu-id="d8336-150">Hello Vm 존재 하는 경우 확인 hello Vm은에 hello 동일 지역 hello 백업 자격 증명 모음으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-150">If hello VMs exist, ensure hello VMs are in hello same region as hello backup vault.</span></span> <span data-ttu-id="d8336-151">있으면 hello Vm에서 동일한 지역 hello 하 hello Vm은 아직 등록 된 tooa 백업 자격 증명 모음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-151">If hello VMs exist and are in hello same region, ensure hello VMs are not already registered tooa backup vault.</span></span> <span data-ttu-id="d8336-152">VM은 할당 된 tooa 백업 자격 증명 모음의 경우 할당 된 사용 가능한 toobe tooother 백업 자격 증명 모음 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-152">If a VM is assigned tooa backup vault it is not available toobe assigned tooother backup vaults.</span></span>

    ![검색 완료](./media/backup-azure-vms/discovery-complete.png)

    <span data-ttu-id="d8336-154">Hello 새 항목을 검색 한 후 tooStep 2로 이동 하 고 Vm을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-154">Once you have discovered hello new items, go tooStep 2 and register your VMs.</span></span>

## <a name="step-2---register-azure-virtual-machines"></a><span data-ttu-id="d8336-155">2단계 - Azure 가상 컴퓨터 등록</span><span class="sxs-lookup"><span data-stu-id="d8336-155">Step 2 - Register Azure virtual machines</span></span>
<span data-ttu-id="d8336-156">Azure 가상 컴퓨터 tooassociate 등록 사용 하 여 hello Azure 백업 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-156">You register an Azure virtual machine tooassociate it with hello Azure Backup service.</span></span> <span data-ttu-id="d8336-157">일반적으로 일회성 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-157">This is typically a one-time activity.</span></span>

1. <span data-ttu-id="d8336-158">백업 자격 증명 모음을 toohello 이동 **복구 서비스** Azure 포털 hello와 클릭 **등록 된 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-158">Navigate toohello backup vault under **Recovery Services** in hello Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="d8336-159">선택 **Azure 가상 컴퓨터** hello 드롭 다운 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-159">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![워크로드 선택](./media/backup-azure-vms/discovery-select-workload.png)
3. <span data-ttu-id="d8336-161">클릭 **등록** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-161">Click **REGISTER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="d8336-162">![등록 단추](./media/backup-azure-vms/register-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="d8336-162">![Register button](./media/backup-azure-vms/register-button-only.png)</span></span>
4. <span data-ttu-id="d8336-163">Hello에 **등록 항목** 바로 가기 메뉴, tooregister 않겠다고 선택 hello 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="d8336-163">In hello **Register Items** shortcut menu, select hello virtual machines that you want tooregister.</span></span> <span data-ttu-id="d8336-164">두 개 이상의 가상 컴퓨터가 있는 경우 동일한 hello 이름을 서로 클라우드 서비스 toodistinguish hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-164">If there are two or more virtual machines with hello same name, use hello cloud service toodistinguish between them.</span></span>

   > [!TIP]
   > <span data-ttu-id="d8336-165">한 번에 여러 가상 컴퓨터를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-165">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="d8336-166">선택한 각 가상 컴퓨터에 대한 작업이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-166">A job is created for each virtual machine that you've selected.</span></span>
5. <span data-ttu-id="d8336-167">클릭 **작업 보기** hello 알림 toogo toohello에 **작업** 페이지.</span><span class="sxs-lookup"><span data-stu-id="d8336-167">Click **View Job** in hello notification toogo toohello **Jobs** page.</span></span>

    ![작업 등록](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="d8336-169">hello 가상 컴퓨터도 hello 등록 작업의 hello 상태와 함께 등록 된 항목의 hello 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-169">hello virtual machine also appears in hello list of registered items, along with hello status of hello registration operation.</span></span>

    ![등록 상태 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="d8336-171">Hello 작업이 완료 되 면 hello 상태 변경 tooreflect hello *등록* 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-171">When hello operation completes, hello status changes tooreflect hello *registered* state.</span></span>

    ![등록 상태 2](./media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a><span data-ttu-id="d8336-173">3단계 - Azure 가상 컴퓨터 보호</span><span class="sxs-lookup"><span data-stu-id="d8336-173">Step 3 - Protect Azure virtual machines</span></span>
<span data-ttu-id="d8336-174">이제 hello 가상 컴퓨터에 대 한 백업 및 보존 정책을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-174">Now you can set up a backup and retention policy for hello virtual machine.</span></span> <span data-ttu-id="d8336-175">단일 보호 작업을 사용하여 여러 가상 컴퓨터를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-175">Multiple virtual machines can be protected by using a single protect action.</span></span>

<span data-ttu-id="d8336-176">Azure 백업 자격 증명 모음은 함께 제공 2015 년 5 월 이후에 만들어진 hello 자격 증명 모음에 기본 제공 기본 정책.</span><span class="sxs-lookup"><span data-stu-id="d8336-176">Azure Backup vaults created after May 2015 come with a default policy built into hello vault.</span></span> <span data-ttu-id="d8336-177">이 기본 정책을 30일의 기본 보존 기간 및 하루 한 번 백업 일정과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-177">This default policy comes with a default retention of 30 days and a once-daily backup schedule.</span></span>

1. <span data-ttu-id="d8336-178">백업 자격 증명 모음을 toohello 이동 **복구 서비스** Azure 포털 hello와 클릭 **등록 된 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-178">Navigate toohello backup vault under **Recovery Services** in hello Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="d8336-179">선택 **Azure 가상 컴퓨터** hello 드롭 다운 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-179">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![포털에서 워크로드 선택](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="d8336-181">클릭 **보호** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-181">Click **PROTECT** at hello bottom of hello page.</span></span>

    <span data-ttu-id="d8336-182">hello **항목 보호 마법사** 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-182">hello **Protect Items wizard** appears.</span></span> <span data-ttu-id="d8336-183">hello 마법사만 등록 되 고 보호 되지 않는 가상 컴퓨터를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-183">hello wizard only lists virtual machines that are registered and not protected.</span></span> <span data-ttu-id="d8336-184">원하는 tooprotect hello 가상 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-184">Select hello virtual machines that you want tooprotect.</span></span>

    <span data-ttu-id="d8336-185">두 개 이상의 가상 컴퓨터가 있는 경우 동일한 hello 이름을 hello 가상 컴퓨터 간의 클라우드 서비스 toodistinguish hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-185">If there are two or more virtual machines with hello same name, use hello cloud service toodistinguish between hello virtual machines.</span></span>

   > [!TIP]
   > <span data-ttu-id="d8336-186">한 번에 여러 가상 컴퓨터를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-186">You can protect multiple virtual machines at one time.</span></span>
   >
   >

    ![규모로 보호 구성](./media/backup-azure-vms/protect-at-scale.png)

4. <span data-ttu-id="d8336-188">선택 된 **백업 일정** tooback 선택한 hello 가상 컴퓨터를 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-188">Choose a **backup schedule** tooback up hello virtual machines that you've selected.</span></span> <span data-ttu-id="d8336-189">정책의 기존 집합에서 선택하거나 새로 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-189">You can pick from an existing set of policies or define a new one.</span></span>

    <span data-ttu-id="d8336-190">각 백업 정책 정책에는 해당 정책과 연관된 여러 가상 컴퓨터가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-190">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="d8336-191">그러나 시간에서 hello 가상 컴퓨터는 특정된 시점에서 하나의 정책과 연결할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-191">However, hello virtual machine can only be associated with one policy at any given point in time.</span></span>

    ![새 정책으로 보호](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="d8336-193">백업 정책을 hello 예약 된 백업에 대 한 보존 규칙에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-193">A backup policy includes a retention scheme for hello scheduled backups.</span></span> <span data-ttu-id="d8336-194">기존 백업 정책을 선택 하는 경우 hello 다음 단계에서 hello 보존 옵션을 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-194">If you select an existing backup policy, you cannot modify hello retention options in hello next step.</span></span>
   >
   >

5. <span data-ttu-id="d8336-195">선택 된 **보존 범위** tooassociate hello 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-195">Choose a **retention range** tooassociate with hello backups.</span></span>

    ![유연한 보존으로 보호](./media/backup-azure-vms/policy-retention.png)

    <span data-ttu-id="d8336-197">보존 정책은 백업 저장에 대해 hello 길이 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-197">Retention policy specifies hello length of time for storing a backup.</span></span> <span data-ttu-id="d8336-198">Hello 백업이 수행 되는 경우에 따라 서로 다른 보존 정책을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-198">You can specify different retention policies based on when hello backup is taken.</span></span> <span data-ttu-id="d8336-199">예를 들어 매일 수행된 백업 지점(작업 복구 지점으로 사용됨)은 90일 동안 보존될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-199">For example, a backup point taken daily (which serves as an operational recovery point) might be preserved for 90 days.</span></span> <span data-ttu-id="d8336-200">이 비해 hello (감사 목적) 각 분기 끝에 수행 하는 백업 지점 toobe 많은 개월 또는 수 년에 대 한 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-200">In comparison, a backup point taken at hello end of each quarter (for audit purposes) may need toobe preserved for many months or years.</span></span>

    ![가상 컴퓨터는 복구 지점으로 백업됨](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="d8336-202">이 예제 이미지에서</span><span class="sxs-lookup"><span data-stu-id="d8336-202">In this example image:</span></span>

   * <span data-ttu-id="d8336-203">**일 단위 보존 정책**: 매일 수행된 백업이 30일 동안 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-203">**Daily retention policy**: Backups taken daily are stored for 30 days.</span></span>
   * <span data-ttu-id="d8336-204">**주 단위 보존 정책**: 매주 일요일에 수행된 백업이 104주 동안 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-204">**Weekly retention policy**: Backups taken every week on Sunday are preserved for 104 weeks.</span></span>
   * <span data-ttu-id="d8336-205">**매월 보존 정책**: 매월 마지막 일요일 hello에서 수행 된 백업을 120 개월 동안 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-205">**Monthly retention policy**: Backups taken on hello last Sunday of each month are preserved for 120 months.</span></span>
   * <span data-ttu-id="d8336-206">**연간 보존 정책**: 99 년 동안 매년 1 월의 첫 번째 일요일 hello에서 수행 된 백업을 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-206">**Yearly retention policy**: Backups taken on hello first Sunday of every January are preserved for 99 years.</span></span>

     <span data-ttu-id="d8336-207">작업에는 선택한 각 가상 컴퓨터에 대 한 hello 가상 컴퓨터 toothat 정책을 연결와 tooconfigure hello 보호 정책을 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-207">A job is created tooconfigure hello protection policy and associate hello virtual machines toothat policy for each virtual machine that you've selected.</span></span>
6. <span data-ttu-id="d8336-208">tooview hello 목록이 **보호 구성** hello 자격 증명 모음 메뉴에서 작업을 클릭 하 여 **작업** 선택 **보호 구성** hello에서 **작업**  필터입니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-208">tooview hello list of **Configure Protection** jobs, from hello vaults menu, click **Jobs** and select **Configure Protection** from hello **Operation** filter.</span></span>

    ![보호 작업 구성](./media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a><span data-ttu-id="d8336-210">초기 백업</span><span class="sxs-lookup"><span data-stu-id="d8336-210">Initial backup</span></span>
<span data-ttu-id="d8336-211">정책을 사용 하 여 hello 가상 컴퓨터가 보호 되 고 나면 그 아래에 표시 hello **보호 된 항목** hello 상태와 함께 탭 *(보류 중 초기 백업) 보호 됨-*합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-211">Once hello virtual machine is protected with a policy, it shows up under hello **Protected Items** tab with hello status of *Protected - (pending initial backup)*.</span></span> <span data-ttu-id="d8336-212">기본적으로 첫 번째 예약 된 백업을 hello는 hello *초기 백업을*합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-212">By default, hello first scheduled backup is hello *initial backup*.</span></span>

<span data-ttu-id="d8336-213">보호 구성 직후 tootrigger hello의 초기 백업:</span><span class="sxs-lookup"><span data-stu-id="d8336-213">tootrigger hello initial backup immediately after configuring protection:</span></span>

1. <span data-ttu-id="d8336-214">Hello hello 맨 아래에 **보호 된 항목** 페이지 **지금 백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-214">At hello bottom of hello **Protected Items** page, click **Backup Now**.</span></span>

    <span data-ttu-id="d8336-215">hello Azure 백업 서비스는 hello 초기 백업 작업에 대 한 백업 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-215">hello Azure Backup service creates a backup job for hello initial backup operation.</span></span>
2. <span data-ttu-id="d8336-216">Hello 클릭 **작업** 작업 목록이 tooview hello 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-216">Click hello **Jobs** tab tooview hello list of jobs.</span></span>

    ![진행 중인 백업](./media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> <span data-ttu-id="d8336-218">Hello 백업 작업 동안 hello Azure 백업 서비스에서 모든 작업을 작성 하 고 일관 된 스냅숏을 각 가상 컴퓨터 tooflush 명령 toohello 백업 확장을 발급 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-218">During hello backup operation, hello Azure Backup service issues a command toohello backup extension in each virtual machine tooflush all write jobs and take a consistent snapshot.</span></span>
>
>

<span data-ttu-id="d8336-219">Hello 초기 백업을 완료 되 면 hello에 hello 가상 컴퓨터의 hello 상태 **보호 된 항목** 탭은 *Protected*합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-219">When hello initial backup finishes, hello status of hello virtual machine in hello **Protected Items** tab is *Protected*.</span></span>

![가상 컴퓨터는 복구 지점으로 백업됨](./media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a><span data-ttu-id="d8336-221">백업 상태 및 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="d8336-221">Viewing backup status and details</span></span>
<span data-ttu-id="d8336-222">가상 컴퓨터 개수 hello hello도 증가 보호 되 면 **대시보드** 페이지 요약 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-222">Once protected, hello virtual machine count also increases in hello **Dashboard** page summary.</span></span> <span data-ttu-id="d8336-223">hello **대시보드** 페이지에 표시 된 지난 24 시간 동안 hello에서 작업의 hello 수 *성공*, 있어야 *실패*, 되며 *진행*.</span><span class="sxs-lookup"><span data-stu-id="d8336-223">hello **Dashboard** page also shows hello number of jobs from hello last 24 hours that were *successful*, have *failed*, and are *in progress*.</span></span> <span data-ttu-id="d8336-224">Hello에 **작업** 페이지에서 hello를 사용 하 여 **상태**, **작업**, 또는 **에서** 및 **를** 메뉴 toofilter hello 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-224">On hello **Jobs** page, use hello **Status**, **Operation**, or **From** and **To** menus toofilter hello jobs.</span></span>

![대시보드 페이지에서 백업 상태](./media/backup-azure-vms/dashboard-protectedvms.png)

<span data-ttu-id="d8336-226">Hello 대시보드의 값은 24 시간 마다 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-226">Values in hello dashboard are refreshed once every 24 hours.</span></span>

## <a name="troubleshooting-errors"></a><span data-ttu-id="d8336-227">문제 해결 오류</span><span class="sxs-lookup"><span data-stu-id="d8336-227">Troubleshooting errors</span></span>
<span data-ttu-id="d8336-228">가상 컴퓨터를 백업 하는 동안 문제를 실행 하면 확인 hello [VM 문제 해결 문서](backup-azure-vms-troubleshoot.md) 에 대 한 도움말입니다.</span><span class="sxs-lookup"><span data-stu-id="d8336-228">If you run into issues while backing up your virtual machine, look at hello [VM     troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8336-229">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d8336-229">Next steps</span></span>
* [<span data-ttu-id="d8336-230">가상 컴퓨터 관리 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="d8336-230">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="d8336-231">가상 컴퓨터 복원</span><span class="sxs-lookup"><span data-stu-id="d8336-231">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
