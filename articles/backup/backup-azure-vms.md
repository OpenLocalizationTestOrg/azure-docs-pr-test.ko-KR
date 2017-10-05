---
title: "백업 자격 증명 모음에 클래식 배포 Azure Virtual Machines 백업 | Microsoft Docs"
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
ms.openlocfilehash: e1da8bce96078a43c656f84005cefc8bbe81c9e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a><span data-ttu-id="bfbef-104">Azure Virtual Machines 백업(클래식 포털)</span><span class="sxs-lookup"><span data-stu-id="bfbef-104">Back up Azure virtual machines (classic portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bfbef-105">복구 서비스 자격 증명 모음에 VM 백업</span><span class="sxs-lookup"><span data-stu-id="bfbef-105">Back up VMs to Recovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="bfbef-106">백업 자격 증명 모음에 VM 백업</span><span class="sxs-lookup"><span data-stu-id="bfbef-106">Back up VMs to Backup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="bfbef-107">이 문서는 클래식 배포 Azure VM(가상 컴퓨터)을 백업 자격 증명 모음에 백업하기 위한 절차를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-107">This article provides the procedures for backing up a Classic-deployed Azure virtual machine (VM) to a Backup vault.</span></span> <span data-ttu-id="bfbef-108">Azure 가상 컴퓨터를 백업하기 전에 몇 가지 처리해야 하는 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-108">There are a few tasks you need to take care of before you can back up an Azure virtual machine.</span></span> <span data-ttu-id="bfbef-109">아직 수행하지 않은 경우 먼저 VM 백업용 환경을 준비하기 위한 [필수 구성 요소](backup-azure-vms-prepare.md) 를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-109">If you haven't already done so, complete the [prerequisites](backup-azure-vms-prepare.md) to prepare your environment for backing up your VMs.</span></span>

<span data-ttu-id="bfbef-110">자세한 내용은 [Azure에서 VM 백업 인프라 계획](backup-azure-vms-introduction.md) 및 [Azure Virtual Machines](https://azure.microsoft.com/documentation/services/virtual-machines/)에 대한 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bfbef-110">For additional information, see the articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

> [!NOTE]
> <span data-ttu-id="bfbef-111">Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델인 [리소스 관리자와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-111">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="bfbef-112">백업 자격 증명 모음은 클래식 배포 VM만 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-112">A Backup vault can only protect Classic-deployed VMs.</span></span> <span data-ttu-id="bfbef-113">백업 자격 증명 모음을 사용하여 Resource Manager 배포 VM을 보호할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-113">You cannot protect Resource Manager-deployed VMs with a Backup vault.</span></span> <span data-ttu-id="bfbef-114">복구 서비스 자격 증명 모음을 사용하는 방법에 대한 자세한 내용은 [복구 서비스 자격 증명 모음에 VM 백업](backup-azure-arm-vms.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bfbef-114">See [Back up VMs to Recovery Services vault](backup-azure-arm-vms.md) for details on working with Recovery Services vaults.</span></span>
>
>

<span data-ttu-id="bfbef-115">Azure 가상 컴퓨터 백업에는 3가지 주요 단계가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-115">Backing up Azure virtual machines involves three key steps:</span></span>

![Azure IaaS VM를 백업하는 세 단계](./media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> <span data-ttu-id="bfbef-117">가상 컴퓨터 백업은 로컬 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-117">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="bfbef-118">한 지역에서 다른 지역의 백업 자격 증명 모음에 가상 컴퓨터를 백업할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-118">You cannot back up virtual machines in one region to a backup vault in another region.</span></span> <span data-ttu-id="bfbef-119">따라서 백업할 VM이 있는 각 Azure 지역에 백업 자격 증명 모음을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-119">So, you must create a backup vault in each Azure region, where there are VMs that will be backed up.</span></span>
>
> [!IMPORTANT]
> <span data-ttu-id="bfbef-120">2017년 3월부터는 백업 자격 증명 모음을 만드는 데 더 이상 클래식 포털을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-120">Starting March 2017, you can no longer use the classic portal to create Backup vaults.</span></span>
> <span data-ttu-id="bfbef-121">이제 Backup 자격 증명 모음을 Recovery Services 자격 증명 모음으로 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-121">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="bfbef-122">자세한 내용은 [Recovery Services 자격 증명 모음으로 Backup 자격 증명 모음 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bfbef-122">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="bfbef-123">Backup 자격 증명 모음을 Recovery Services 자격 증명 모음으로 업그레이드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-123">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="bfbef-124">2017년 10월 15일 이후부터는 PowerShell을 사용하여 Backup 자격 증명 모음을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-124">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="bfbef-125">**2017년 11월 1일까지**:</span><span class="sxs-lookup"><span data-stu-id="bfbef-125">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="bfbef-126">남아 있는 모든 Backup 자격 증명 모음이 Recovery Services 자격 증명 모음으로 자동 업그레이드됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-126">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="bfbef-127">클래식 포털에서는 백업 데이터에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-127">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="bfbef-128">대신 Azure Portal을 사용하여 Recovery Services 자격 증명 모음에서 백업 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-128">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="step-1---discover-azure-virtual-machines"></a><span data-ttu-id="bfbef-129">1단계 - Azure 가상 컴퓨터 검색</span><span class="sxs-lookup"><span data-stu-id="bfbef-129">Step 1 - Discover Azure virtual machines</span></span>
<span data-ttu-id="bfbef-130">등록하기 전에 구독에 추가된 새 VM(가상 컴퓨터)이 식별되도록 하려면 검색 프로세스를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-130">To ensure any new virtual machines (VMs) added to the subscription are identified before registering, run the discovery process.</span></span> <span data-ttu-id="bfbef-131">프로세스는 클라우드 서비스 이름 및 지역과 같은 추가 정보와 함께 구독의 가상 컴퓨터 목록을 Azure에 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-131">The process queries Azure for the list of virtual machines in the subscription, along with additional information like the cloud service name and the region.</span></span>

1. <span data-ttu-id="bfbef-132">[클래식 포털](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="bfbef-132">Sign in to the [Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="bfbef-133">Azure 서비스 목록에서 **복구 서비스**를 클릭하여 백업 및 사이트 복구 자격 증명 모음 목록을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-133">In the list of Azure services, click **Recovery Services** to open the list of Backup and Site Recovery vaults.</span></span>
    <span data-ttu-id="bfbef-134">![자격 증명 모음 목록 열기](./media/backup-azure-vms/choose-vault-list.png)</span><span class="sxs-lookup"><span data-stu-id="bfbef-134">![Open vault list](./media/backup-azure-vms/choose-vault-list.png)</span></span>
3. <span data-ttu-id="bfbef-135">백업 자격 증명 모음 목록에서 VM을 백업할 자격 증명 모음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-135">In the list of Backup vaults, select the vault to back up a VM.</span></span>

    <span data-ttu-id="bfbef-136">새 자격 증명 모음인 경우 포털에서 **빠른 시작** 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-136">If this is a new vault the portal opens to the **Quick Start** page.</span></span>

    ![등록된 항목 열기 메뉴](./media/backup-azure-vms/vault-quick-start.png)

    <span data-ttu-id="bfbef-138">이전에 자격 증명 모음을 구성한 경우 포털에서 가장 최근에 사용된 메뉴가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-138">If the vault has previously been configured, the portal opens to the most recently used menu.</span></span>
4. <span data-ttu-id="bfbef-139">자격 증명 모음 메뉴(페이지 맨 위에 있음)에서 **등록된 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-139">From the vault menu (at the top of the page), click **Registered Items**.</span></span>

    ![등록된 항목 열기 메뉴](./media/backup-azure-vms/vault-menu.png)
5. <span data-ttu-id="bfbef-141">**형식** 메뉴에서 **Azure 가상 컴퓨터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-141">From the **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![워크로드 선택](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="bfbef-143">페이지 맨 아래에서 **검색** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-143">Click **DISCOVER** at the bottom of the page.</span></span>
    <span data-ttu-id="bfbef-144">![검색 단추](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="bfbef-144">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="bfbef-145">검색 프로세스는 가상 컴퓨터를 표로 정리하는 동안 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-145">The discovery process may take a few minutes while the virtual machines are being tabulated.</span></span> <span data-ttu-id="bfbef-146">화면 맨 아래에 있는 알림은 프로세스가 실행되고 있다는 것을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-146">There is a notification at the bottom of the screen that lets you know that the process is running.</span></span>

    ![VM 검색](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="bfbef-148">프로세스가 완료되면 알림이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-148">The notification changes when the process is complete.</span></span> <span data-ttu-id="bfbef-149">검색 프로세스에서 가상 컴퓨터를 찾지 못한 경우 먼저 VM이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-149">If the discovery process did not find the virtual machines, first ensure the VMs exist.</span></span> <span data-ttu-id="bfbef-150">VM이 있는 경우 VM이 백업 자격 증명 모음과 동일한 지역에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-150">If the VMs exist, ensure the VMs are in the same region as the backup vault.</span></span> <span data-ttu-id="bfbef-151">VM이 동일한 지역에 있는 경우 VM이 백업 자격 증명 모음에 아직 등록되지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-151">If the VMs exist and are in the same region, ensure the VMs are not already registered to a backup vault.</span></span> <span data-ttu-id="bfbef-152">VM이 백업 자격 증명 모음에 할당된 경우 다른 백업 자격 증명 모음에 할당할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-152">If a VM is assigned to a backup vault it is not available to be assigned to other backup vaults.</span></span>

    ![검색 완료](./media/backup-azure-vms/discovery-complete.png)

    <span data-ttu-id="bfbef-154">새 항목을 검색했으면 2단계로 이동하여 VM을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-154">Once you have discovered the new items, go to Step 2 and register your VMs.</span></span>

## <a name="step-2---register-azure-virtual-machines"></a><span data-ttu-id="bfbef-155">2단계 - Azure 가상 컴퓨터 등록</span><span class="sxs-lookup"><span data-stu-id="bfbef-155">Step 2 - Register Azure virtual machines</span></span>
<span data-ttu-id="bfbef-156">Azure 가상 컴퓨터를 등록하여 Azure 백업 서비스와 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-156">You register an Azure virtual machine to associate it with the Azure Backup service.</span></span> <span data-ttu-id="bfbef-157">일반적으로 일회성 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-157">This is typically a one-time activity.</span></span>

1. <span data-ttu-id="bfbef-158">Azure Portal의 **Recovery Services**에 있는 백업 저장소로 이동한 다음, **등록된 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-158">Navigate to the backup vault under **Recovery Services** in the Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="bfbef-159">드롭다운 메뉴에서 **Azure 가상 컴퓨터** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-159">Select **Azure Virtual Machine** from the drop-down menu.</span></span>

    ![워크로드 선택](./media/backup-azure-vms/discovery-select-workload.png)
3. <span data-ttu-id="bfbef-161">페이지의 맨 아래에서 **등록** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-161">Click **REGISTER** at the bottom of the page.</span></span>
    <span data-ttu-id="bfbef-162">![등록 단추](./media/backup-azure-vms/register-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="bfbef-162">![Register button](./media/backup-azure-vms/register-button-only.png)</span></span>
4. <span data-ttu-id="bfbef-163">**등록 항목** 바로 가기 메뉴에서 등록하려는 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-163">In the **Register Items** shortcut menu, select the virtual machines that you want to register.</span></span> <span data-ttu-id="bfbef-164">동일한 이름을 가진 가상 컴퓨터가 두 개 이상 있는 경우 클라우드 서비스를 사용하여 가상 컴퓨터를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-164">If there are two or more virtual machines with the same name, use the cloud service to distinguish between them.</span></span>

   > [!TIP]
   > <span data-ttu-id="bfbef-165">한 번에 여러 가상 컴퓨터를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-165">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="bfbef-166">선택한 각 가상 컴퓨터에 대한 작업이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-166">A job is created for each virtual machine that you've selected.</span></span>
5. <span data-ttu-id="bfbef-167">알림에서 **작업 보기**를 클릭하여 **작업** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-167">Click **View Job** in the notification to go to the **Jobs** page.</span></span>

    ![작업 등록](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="bfbef-169">또한 등록 작업의 상태와 함께 가상 컴퓨터가 등록된 항목 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-169">The virtual machine also appears in the list of registered items, along with the status of the registration operation.</span></span>

    ![등록 상태 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="bfbef-171">작업이 완료되면 상태가 *등록된* 상태를 반영하도록 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-171">When the operation completes, the status changes to reflect the *registered* state.</span></span>

    ![등록 상태 2](./media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a><span data-ttu-id="bfbef-173">3단계 - Azure 가상 컴퓨터 보호</span><span class="sxs-lookup"><span data-stu-id="bfbef-173">Step 3 - Protect Azure virtual machines</span></span>
<span data-ttu-id="bfbef-174">이제 가상 컴퓨터에 대한 백업 및 보존 정책을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-174">Now you can set up a backup and retention policy for the virtual machine.</span></span> <span data-ttu-id="bfbef-175">단일 보호 작업을 사용하여 여러 가상 컴퓨터를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-175">Multiple virtual machines can be protected by using a single protect action.</span></span>

<span data-ttu-id="bfbef-176">2015년 5월 이후에 만든 Azure 백업 자격 증명 모음은 자격 증명 모음에 기본 제공되는 기본 정책을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-176">Azure Backup vaults created after May 2015 come with a default policy built into the vault.</span></span> <span data-ttu-id="bfbef-177">이 기본 정책을 30일의 기본 보존 기간 및 하루 한 번 백업 일정과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-177">This default policy comes with a default retention of 30 days and a once-daily backup schedule.</span></span>

1. <span data-ttu-id="bfbef-178">Azure Portal의 **Recovery Services**에 있는 백업 저장소로 이동한 다음, **등록된 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-178">Navigate to the backup vault under **Recovery Services** in the Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="bfbef-179">드롭다운 메뉴에서 **Azure 가상 컴퓨터** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-179">Select **Azure Virtual Machine** from the drop-down menu.</span></span>

    ![포털에서 워크로드 선택](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="bfbef-181">페이지 맨 아래에 있는 **보호** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-181">Click **PROTECT** at the bottom of the page.</span></span>

    <span data-ttu-id="bfbef-182">**보호 항목 마법사** 가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-182">The **Protect Items wizard** appears.</span></span> <span data-ttu-id="bfbef-183">이 마법사는 등록되고 보호되지 않은 가상 컴퓨터만을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-183">The wizard only lists virtual machines that are registered and not protected.</span></span> <span data-ttu-id="bfbef-184">보호하려는 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-184">Select the virtual machines that you want to protect.</span></span>

    <span data-ttu-id="bfbef-185">동일한 이름으로 둘 이상의 가상 컴퓨터가 있는 경우 가상 컴퓨터 사이에서 구별하기 위해 클라우드 서비스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-185">If there are two or more virtual machines with the same name, use the cloud service to distinguish between the virtual machines.</span></span>

   > [!TIP]
   > <span data-ttu-id="bfbef-186">한 번에 여러 가상 컴퓨터를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-186">You can protect multiple virtual machines at one time.</span></span>
   >
   >

    ![규모로 보호 구성](./media/backup-azure-vms/protect-at-scale.png)

4. <span data-ttu-id="bfbef-188">**백업 일정** 을 선택하여 선택한 가상 컴퓨터를 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-188">Choose a **backup schedule** to back up the virtual machines that you've selected.</span></span> <span data-ttu-id="bfbef-189">정책의 기존 집합에서 선택하거나 새로 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-189">You can pick from an existing set of policies or define a new one.</span></span>

    <span data-ttu-id="bfbef-190">각 백업 정책 정책에는 해당 정책과 연관된 여러 가상 컴퓨터가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-190">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="bfbef-191">그러나 가상 컴퓨터는 특정 시간에 한 정책에만 연관될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-191">However, the virtual machine can only be associated with one policy at any given point in time.</span></span>

    ![새 정책으로 보호](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="bfbef-193">백업 정책은 예약된 백업의 보존 체계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-193">A backup policy includes a retention scheme for the scheduled backups.</span></span> <span data-ttu-id="bfbef-194">기존 백업 정책을 선택하면 다음 단계에서 보존 옵션을 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-194">If you select an existing backup policy, you cannot modify the retention options in the next step.</span></span>
   >
   >

5. <span data-ttu-id="bfbef-195">**보존 범위** 를 선택하여 백업과 연관시킵니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-195">Choose a **retention range** to associate with the backups.</span></span>

    ![유연한 보존으로 보호](./media/backup-azure-vms/policy-retention.png)

    <span data-ttu-id="bfbef-197">보존 정책은 백업을 저장하는 시간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-197">Retention policy specifies the length of time for storing a backup.</span></span> <span data-ttu-id="bfbef-198">백업이 수행되는 시기에 따라 다른 보존 정책을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-198">You can specify different retention policies based on when the backup is taken.</span></span> <span data-ttu-id="bfbef-199">예를 들어 매일 수행된 백업 지점(작업 복구 지점으로 사용됨)은 90일 동안 보존될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-199">For example, a backup point taken daily (which serves as an operational recovery point) might be preserved for 90 days.</span></span> <span data-ttu-id="bfbef-200">반면에 각 분기 말에 수행된 백업 지점(감사 용도)은 수개월 또는 수년 동안 보존되어야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-200">In comparison, a backup point taken at the end of each quarter (for audit purposes) may need to be preserved for many months or years.</span></span>

    ![가상 컴퓨터는 복구 지점으로 백업됨](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="bfbef-202">이 예제 이미지에서</span><span class="sxs-lookup"><span data-stu-id="bfbef-202">In this example image:</span></span>

   * <span data-ttu-id="bfbef-203">**일 단위 보존 정책**: 매일 수행된 백업이 30일 동안 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-203">**Daily retention policy**: Backups taken daily are stored for 30 days.</span></span>
   * <span data-ttu-id="bfbef-204">**주 단위 보존 정책**: 매주 일요일에 수행된 백업이 104주 동안 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-204">**Weekly retention policy**: Backups taken every week on Sunday are preserved for 104 weeks.</span></span>
   * <span data-ttu-id="bfbef-205">**월 단위 보존 정책**: 매달 마지막 주 일요일에 수행된 백업이 120개월 동안 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-205">**Monthly retention policy**: Backups taken on the last Sunday of each month are preserved for 120 months.</span></span>
   * <span data-ttu-id="bfbef-206">**월 단위 보존 정책**: 매년 1월 첫째 주 일요일에 수행된 백업이 99년 동안 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-206">**Yearly retention policy**: Backups taken on the first Sunday of every January are preserved for 99 years.</span></span>

     <span data-ttu-id="bfbef-207">작업은 선택한 가상 컴퓨터 각각에 대해 보호 정책을 구성하고 가상 컴퓨터를 해당 정책과 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-207">A job is created to configure the protection policy and associate the virtual machines to that policy for each virtual machine that you've selected.</span></span>
6. <span data-ttu-id="bfbef-208">**보호 구성** 작업 목록을 보려면 자격 증명 모음 메뉴에서 **작업**을 클릭하고 **작업** 필터에서 **보호 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-208">To view the list of **Configure Protection** jobs, from the vaults menu, click **Jobs** and select **Configure Protection** from the **Operation** filter.</span></span>

    ![보호 작업 구성](./media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a><span data-ttu-id="bfbef-210">초기 백업</span><span class="sxs-lookup"><span data-stu-id="bfbef-210">Initial backup</span></span>
<span data-ttu-id="bfbef-211">가상 컴퓨터가 정책으로 보호되면, 이는 **보호됨 - (초기 백업 보류 중)** 상태로 *보호된 항목*탭 아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-211">Once the virtual machine is protected with a policy, it shows up under the **Protected Items** tab with the status of *Protected - (pending initial backup)*.</span></span> <span data-ttu-id="bfbef-212">기본적으로 첫 번째 예약된 백업은 *초기 백업*입니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-212">By default, the first scheduled backup is the *initial backup*.</span></span>

<span data-ttu-id="bfbef-213">보호를 구성한 후에 즉시 초기 백업을 트리거하려면.</span><span class="sxs-lookup"><span data-stu-id="bfbef-213">To trigger the initial backup immediately after configuring protection:</span></span>

1. <span data-ttu-id="bfbef-214">**보호된 항목** 페이지 아래쪽에서 **지금 백업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-214">At the bottom of the **Protected Items** page, click **Backup Now**.</span></span>

    <span data-ttu-id="bfbef-215">Azure 백업 서비스는 초기 백업 작업에 대한 백업 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-215">The Azure Backup service creates a backup job for the initial backup operation.</span></span>
2. <span data-ttu-id="bfbef-216">**작업** 탭을 클릭하여 작업 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-216">Click the **Jobs** tab to view the list of jobs.</span></span>

    ![진행 중인 백업](./media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> <span data-ttu-id="bfbef-218">백업 작업 동안 Azure Backup 서비스는 각 가상 컴퓨터에서 백업 확장에 대한 명령을 발행하여 모든 쓰기 작업을 플러시하고 일관된 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-218">During the backup operation, the Azure Backup service issues a command to the backup extension in each virtual machine to flush all write jobs and take a consistent snapshot.</span></span>
>
>

<span data-ttu-id="bfbef-219">초기 백업이 완료되면 **보호된 항목** 탭에서 가상 컴퓨터의 상태가 *보호됨*으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-219">When the initial backup finishes, the status of the virtual machine in the **Protected Items** tab is *Protected*.</span></span>

![가상 컴퓨터는 복구 지점으로 백업됨](./media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a><span data-ttu-id="bfbef-221">백업 상태 및 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="bfbef-221">Viewing backup status and details</span></span>
<span data-ttu-id="bfbef-222">보호되면 가상 컴퓨터 수가 **대시보드** 페이지 요약에서도 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-222">Once protected, the virtual machine count also increases in the **Dashboard** page summary.</span></span> <span data-ttu-id="bfbef-223">또한 **대시보드** 페이지에서 지난 24시간 내의 *성공* 및 *실패*한 작업 수와 아직 *진행 중*인 작업 수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-223">The **Dashboard** page also shows the number of jobs from the last 24 hours that were *successful*, have *failed*, and are *in progress*.</span></span> <span data-ttu-id="bfbef-224">**작업** 페이지에서 **상태**, **작업** 또는 **시작** 및 **끝** 메뉴를 사용하여 작업을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-224">On the **Jobs** page, use the **Status**, **Operation**, or **From** and **To** menus to filter the jobs.</span></span>

![대시보드 페이지에서 백업 상태](./media/backup-azure-vms/dashboard-protectedvms.png)

<span data-ttu-id="bfbef-226">대시보드의 값은 24시간마다 한 번 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="bfbef-226">Values in the dashboard are refreshed once every 24 hours.</span></span>

## <a name="troubleshooting-errors"></a><span data-ttu-id="bfbef-227">문제 해결 오류</span><span class="sxs-lookup"><span data-stu-id="bfbef-227">Troubleshooting errors</span></span>
<span data-ttu-id="bfbef-228">가상 컴퓨터를 백업하는 동안 문제를 실행하는 경우 도움말은 [VM 문제 해결 문서](backup-azure-vms-troubleshoot.md)를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="bfbef-228">If you run into issues while backing up your virtual machine, look at the [VM     troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfbef-229">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bfbef-229">Next steps</span></span>
* [<span data-ttu-id="bfbef-230">가상 컴퓨터 관리 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="bfbef-230">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="bfbef-231">가상 컴퓨터 복원</span><span class="sxs-lookup"><span data-stu-id="bfbef-231">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
