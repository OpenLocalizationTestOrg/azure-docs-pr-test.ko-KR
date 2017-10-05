---
title: "소개 - 백업 자격 증명으로 Azure VM 백업 | Microsoft Docs"
description: "클래식 포털을 사용하여 Backup 자격 증명 모음에 Azure VM을 백업합니다. 이 자습서에서는 Backup 자격 증명 모음 만들기, VM 등록, 백업 정책 만들기 및 초기 백업 작업 실행을 포함하는 모든 단계를 설명합니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 722820dc-b65f-425c-a9e5-c1946e896a87
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;
ms.openlocfilehash: fc31d7654e455ec5b4e4bb9af4cf1a166f1661ee
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="first-look-backing-up-azure-virtual-machines"></a><span data-ttu-id="39a71-104">소개: Azure 가상 컴퓨터 백업</span><span class="sxs-lookup"><span data-stu-id="39a71-104">First look: Backing up Azure virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="39a71-105">복구 서비스 자격 증명 모음으로 VM 보호</span><span class="sxs-lookup"><span data-stu-id="39a71-105">Protect VMs with a recovery services vault</span></span>](backup-azure-vms-first-look-arm.md)
> * [<span data-ttu-id="39a71-106">백업 자격 증명으로 Azure VM 보호</span><span class="sxs-lookup"><span data-stu-id="39a71-106">Protect Azure VMs with a backup vault</span></span>](backup-azure-vms-first-look.md)
>
>

<span data-ttu-id="39a71-107">이 자습서에서는 Azure 가상 컴퓨터(VM)를 Azure의 백업 자격 증명 모음에 백업하는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-107">This tutorial takes you through the steps for backing up an Azure virtual machine (VM) to a backup vault in Azure.</span></span> <span data-ttu-id="39a71-108">이 문서에서는 VM을 백업하기 위해 클래식 모델 또는 서비스 관리자 배포 모델을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-108">This article describes the classic model or Service Manager deployment model, for backing up VMs.</span></span> <span data-ttu-id="39a71-109">다음 단계는 클래식 포털에서 만든 Backup 자격 증명 모음에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-109">The following steps apply only to Backup vaults created in the classic portal.</span></span> <span data-ttu-id="39a71-110">새로운 배포에 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-110">Microsoft recommends using the Resource Manager model for new deployments.</span></span>

<span data-ttu-id="39a71-111">리소스 그룹에 속해 있는 Recovery Services 자격 증명 모음에 VM을 백업하려는 경우 [소개: 복구 서비스 자격 증명 모음으로 VM 보호](backup-azure-vms-first-look-arm.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39a71-111">If you are interested in backing up a VM to a Recovery Services vault that belongs to a Resource Group, see [First look: Protect VMs with a recovery services vault](backup-azure-vms-first-look-arm.md).</span></span>

<span data-ttu-id="39a71-112">다음 자습서를 성공적으로 완료하려면 다음과 같은 필수 조건을 갖추어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-112">To successfully complete the following tutorial, these prerequisites must exist:</span></span>

* <span data-ttu-id="39a71-113">Azure 구독에서 VM을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-113">You have created a VM in your Azure subscription.</span></span>
* <span data-ttu-id="39a71-114">VM은 Azure공용 IP 주소에 연결되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-114">The VM has connectivity to Azure public IP addresses.</span></span> <span data-ttu-id="39a71-115">자세한 내용은 [네트워크 연결](backup-azure-vms-prepare.md#network-connectivity)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39a71-115">For additional information, see [Network connectivity](backup-azure-vms-prepare.md#network-connectivity).</span></span>


> [!NOTE]
> <span data-ttu-id="39a71-116">Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델인 [리소스 관리자와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-116">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="39a71-117">이 자습서는 클래식 포털에서 만든 가상 컴퓨터와 함께 사용하도록 준비되었습니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-117">This tutorial is for use with virtual machines created in the classic portal.</span></span>
>
>

## <a name="create-a-backup-vault"></a><span data-ttu-id="39a71-118">백업 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="39a71-118">Create a backup vault</span></span>
<span data-ttu-id="39a71-119">백업 자격 증명 모음은 모든 백업과 시간에 따라 생성된 복구 지점을 저장하는 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-119">A backup vault is an entity that stores all the backups and recovery points that have been created over time.</span></span> <span data-ttu-id="39a71-120">백업 자격 증명 모음에는 백업 중인 가상 컴퓨터에 적용할 백업 정책도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-120">The backup vault also contains the backup policies that are applied to the virtual machines being backed up.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39a71-121">2017년 3월부터는 Backup 자격 증명 모음을 만드는 데 더 이상 클래식 포털을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-121">Starting March 2017, you can no longer use the classic portal to create Backup vaults.</span></span>
> <span data-ttu-id="39a71-122">Backup 자격 증명 모음을 Recovery Services 자격 증명 모음으로 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-122">You can upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="39a71-123">자세한 내용은 [Recovery Services 자격 증명 모음으로 Backup 자격 증명 모음 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39a71-123">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="39a71-124">Backup 자격 증명 모음을 Recovery Services 자격 증명 모음으로 업그레이드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-124">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="39a71-125">2017년 10월 15일 이후부터는 PowerShell을 사용하여 Backup 자격 증명 모음을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-125">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="39a71-126">**2017년 11월 1일까지**:</span><span class="sxs-lookup"><span data-stu-id="39a71-126">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="39a71-127">남아 있는 모든 Backup 자격 증명 모음이 Recovery Services 자격 증명 모음으로 자동 업그레이드됩니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-127">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="39a71-128">클래식 포털에서는 백업 데이터에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-128">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="39a71-129">대신 Azure Portal을 사용하여 Recovery Services 자격 증명 모음에서 백업 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-129">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="discover-and-register-azure-virtual-machines"></a><span data-ttu-id="39a71-130">Azure 가상 컴퓨터 검색 및 등록</span><span class="sxs-lookup"><span data-stu-id="39a71-130">Discover and Register Azure virtual machines</span></span>
<span data-ttu-id="39a71-131">VM에 자격 증명 모음을 등록하기 전에, 검색 프로세스를 실행하여 새 VM이 있는지 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-131">Before registering the VM with a vault, run the discovery process to identify any new VMs.</span></span> <span data-ttu-id="39a71-132">이 작업은 구독에 클라우드 서비스 이름 및 지역과 같은 추가 정보와 함께 가상 컴퓨터 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-132">This returns a list of virtual machines in the subscription, along with additional information like the cloud service name and the region.</span></span>

1. <span data-ttu-id="39a71-133">[Azure 클래식 포털](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="39a71-133">Sign in to the [Azure Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="39a71-134">Azure 클래식 포털에서 **Recovery Services**를 클릭하여 Recovery Services 자격 증명 모음 목록을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-134">In the Azure classic portal, click **Recovery Services** to open the list of Recovery Services vaults.</span></span>
    <span data-ttu-id="39a71-135">![워크로드 선택](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span><span class="sxs-lookup"><span data-stu-id="39a71-135">![Select workload](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span></span>
3. <span data-ttu-id="39a71-136">자격 증명 모음 목록에서 VM을 백업할 자격 증명 모음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-136">From the list of vaults, select the vault to back up a VM.</span></span>

    <span data-ttu-id="39a71-137">자격 증명 모음을 선택하면 **빠른 시작** 페이지에 열립니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-137">When you select your vault, it opens in the **Quick Start** page</span></span>
4. <span data-ttu-id="39a71-138">자격 증명 모음 메뉴에서 **등록된 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-138">From the vault menu, click **Registered Items**.</span></span>

    ![워크로드 선택](./media/backup-azure-vms-first-look/configure-registered-items.png)
5. <span data-ttu-id="39a71-140">**형식** 메뉴에서 **Azure Virtual Machine**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-140">From the **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![워크로드 선택](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="39a71-142">페이지 맨 아래에서 **검색** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-142">Click **DISCOVER** at the bottom of the page.</span></span>
    <span data-ttu-id="39a71-143">![검색 단추](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="39a71-143">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="39a71-144">검색 프로세스는 가상 컴퓨터를 표로 정리하는 동안 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-144">The discovery process may take a few minutes while the virtual machines are being tabulated.</span></span> <span data-ttu-id="39a71-145">화면 맨 아래에 있는 알림은 프로세스가 실행되고 있다는 것을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-145">There is a notification at the bottom of the screen that lets you know that the process is running.</span></span>

    ![VM 검색](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="39a71-147">프로세스가 완료되면 알림이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-147">The notification changes when the process is complete.</span></span>

    ![검색 완료](./media/backup-azure-vms-first-look/discovery-complete.png)
7. <span data-ttu-id="39a71-149">페이지의 맨 아래에서 **등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-149">Click **REGISTER** at the bottom of the page.</span></span>
    <span data-ttu-id="39a71-150">![등록 단추](./media/backup-azure-vms-first-look/register-icon.png)</span><span class="sxs-lookup"><span data-stu-id="39a71-150">![Register button](./media/backup-azure-vms-first-look/register-icon.png)</span></span>
8. <span data-ttu-id="39a71-151">**등록 항목** 바로 가기 메뉴에서 등록하려는 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-151">In the **Register Items** shortcut menu, select the virtual machines that you want to register.</span></span>

   > [!TIP]
   > <span data-ttu-id="39a71-152">한 번에 여러 가상 컴퓨터를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-152">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="39a71-153">선택한 각 가상 컴퓨터에 대한 작업이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-153">A job is created for each virtual machine that you've selected.</span></span>
9. <span data-ttu-id="39a71-154">알림에서 **작업 보기**를 클릭하여 **작업** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-154">Click **View Job** in the notification to go to the **Jobs** page.</span></span>

    ![작업 등록](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="39a71-156">또한 등록 작업의 상태와 함께 가상 컴퓨터가 등록된 항목 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-156">The virtual machine also appears in the list of registered items, along with the status of the registration operation.</span></span>

    ![등록 상태 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="39a71-158">작업이 완료되면 상태가 *등록된* 상태를 반영하도록 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-158">When the operation completes, the status changes to reflect the *registered* state.</span></span>

    ![등록 상태 2](./media/backup-azure-vms/register-status02.png)

## <a name="install-the-vm-agent-on-the-virtual-machine"></a><span data-ttu-id="39a71-160">가상 컴퓨터에 VM 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="39a71-160">Install the VM Agent on the virtual machine</span></span>
<span data-ttu-id="39a71-161">Azure VM 에이전트는 작업할 Backup 확장을 위한 Azure 가상 컴퓨터에 설치되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-161">The Azure VM Agent must be installed on the Azure virtual machine for the Backup extension to work.</span></span> <span data-ttu-id="39a71-162">Azure 갤러리에서 VM을 만든 경우 VM 에이전트는 이미 VM에 있습니다. [VM 보호](backup-azure-vms-first-look.md#create-the-backup-policy)로 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-162">If your VM was created from the Azure gallery, the VM Agent is already present on the VM; you can skip to [protecting your VMs](backup-azure-vms-first-look.md#create-the-backup-policy).</span></span>

<span data-ttu-id="39a71-163">VM이 온-프레미스 데이터 센터에서 마이그레이션된 경우에는, VM에 VM 에이전트가 설치어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-163">If your VM migrated from an on-premises datacenter, the VM probably does not have the VM Agent installed.</span></span> <span data-ttu-id="39a71-164">VM을 보호하도록 진행하기 전에 가상 컴퓨터에 VM 에이전트를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-164">You must install the VM Agent on the virtual machine before proceeding to protect the VM.</span></span> <span data-ttu-id="39a71-165">VM 에이전트 설치에 대한 자세한 단계는 [VM  Backup 문서의 VM 에이전트 섹션](backup-azure-vms-prepare.md#vm-agent)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39a71-165">For detailed steps on installing the VM Agent, see the [VM Agent section of the Backup VMs article](backup-azure-vms-prepare.md#vm-agent).</span></span>

## <a name="create-the-backup-policy"></a><span data-ttu-id="39a71-166">백업 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="39a71-166">Create the backup policy</span></span>
<span data-ttu-id="39a71-167">초기 백업 작업을 트리거하기 전에, 백업 스냅숏을 생성하는 일정을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-167">Before you trigger the initial backup job, set the schedule when backup snapshots are taken.</span></span> <span data-ttu-id="39a71-168">백업 스냅숏을 생성하는 일정 및 스냅숏을 보존하는 기간이 백업 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-168">The schedule when backup snapshots are taken, and the length of time those snapshots are retained, is the backup policy.</span></span> <span data-ttu-id="39a71-169">보존 정보는 GFS(Grandfather-Father-Son) 백업 회전 체계를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-169">The retention information is based on Grandfather-father-son backup rotation scheme.</span></span>

1. <span data-ttu-id="39a71-170">Azure 클래식 포털의 **Recovery Services**에 있는 백업 저장소로 이동하여 **등록된 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-170">Navigate to the backup vault under **Recovery Services** in the Azure Classic portal, and  click **Registered Items**.</span></span>
2. <span data-ttu-id="39a71-171">드롭다운 메뉴에서 **Azure 가상 컴퓨터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-171">Select **Azure Virtual Machine** from the drop-down menu.</span></span>

    ![포털에서 워크로드 선택](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="39a71-173">페이지 맨 아래에 있는 **보호**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-173">Click **PROTECT** at the bottom of the page.</span></span>
    <span data-ttu-id="39a71-174">![보호 클릭](./media/backup-azure-vms-first-look/protect-icon.png)</span><span class="sxs-lookup"><span data-stu-id="39a71-174">![Click Protect](./media/backup-azure-vms-first-look/protect-icon.png)</span></span>

    <span data-ttu-id="39a71-175">**항목 마법사 보호**가 나타나고 등록되었지만 보호되지 않은 가상 컴퓨터 *만* 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-175">The **Protect Items wizard** appears and lists *only* virtual machines that are registered and not protected.</span></span>

    ![규모로 보호 구성](./media/backup-azure-vms/protect-at-scale.png)
4. <span data-ttu-id="39a71-177">보호하려는 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-177">Select the virtual machines that you want to protect.</span></span>

    <span data-ttu-id="39a71-178">동일한 이름으로 둘 이상의 가상 컴퓨터가 있는 경우 가상 컴퓨터 사이에서 구별하기 위해 클라우드 서비스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-178">If there are two or more virtual machines with the same name, use the Cloud Service to distinguish between the virtual machines.</span></span>
5. <span data-ttu-id="39a71-179">**보호 구성** 메뉴에서 기존 정책을 선택하거나 새 정책을 만들어서 식별한 가상 컴퓨터를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-179">On the **Configure protection** menu select an existing policy or create a new policy to protect the virtual machines that you identified.</span></span>

    <span data-ttu-id="39a71-180">새 Backup 자격 증명 모음에는 자격 증명 모음과 연결된 기본 정책이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-180">New Backup vaults have a default policy associated with the vault.</span></span> <span data-ttu-id="39a71-181">이 정책은 매일 저녁 스냅숏을 생성하고, 일일 스냅숏은 30일간 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-181">This policy takes a daily snapshot each evening, and the daily snapshot is retained for 30 days.</span></span> <span data-ttu-id="39a71-182">각 백업 정책 정책에는 해당 정책과 연관된 여러 가상 컴퓨터가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-182">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="39a71-183">그러나 가상 컴퓨터는 한 번에 한 정책에만 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-183">However, the virtual machine can only be associated with one policy at a time.</span></span>

    ![새 정책으로 보호](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="39a71-185">백업 정책은 예약된 백업의 보존 체계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-185">A backup policy includes a retention scheme for the scheduled backups.</span></span> <span data-ttu-id="39a71-186">기존 백업 정책을 선택하면 다음 단계에서 보존 옵션을 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-186">If you select an existing backup policy, you will be unable to modify the retention options in the next step.</span></span>
   >
   >
6. <span data-ttu-id="39a71-187">**보존 범위**에서 특정 백업 지점에 대한 매일, 매주, 매월 및 매년 범위를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-187">On **Retention Range** define the daily, weekly, monthly, and yearly scope for the specific backup points.</span></span>

    ![가상 컴퓨터는 복구 지점으로 백업됨](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="39a71-189">보존 정책은 백업을 저장하는 시간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-189">Retention policy specifies the length of time for storing a backup.</span></span> <span data-ttu-id="39a71-190">백업이 수행되는 시기에 따라 다른 보존 정책을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-190">You can specify different retention policies based on when the backup is taken.</span></span>
7. <span data-ttu-id="39a71-191">**작업**을 클릭하고 **보호 구성** 작업 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-191">Click **Jobs** to view the list of **Configure Protection** jobs.</span></span>

    ![보호 작업 구성](./media/backup-azure-vms/protect-configureprotection.png)

    <span data-ttu-id="39a71-193">정책을 설정했으므로 다음 단계로 이동하여 초기 백업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-193">Now that you've established the policy, go to the next step and run the initial backup.</span></span>

## <a name="initial-backup"></a><span data-ttu-id="39a71-194">초기 백업</span><span class="sxs-lookup"><span data-stu-id="39a71-194">Initial backup</span></span>
<span data-ttu-id="39a71-195">가상 컴퓨터가 정책으로 보호되면 **보호된 항목** 탭에서 해당 관계를 볼 수 있습니다. 초기 백업이 발생할 때까지 **보호 상태**는 **보호됨 - (초기 백업 보류 중)**으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-195">Once a virtual machine has been protected with a policy, you can view that relationship on the **Protected Items** tab. Until the initial backup occurs, the **Protection Status** shows as **Protected - (pending initial backup)**.</span></span> <span data-ttu-id="39a71-196">기본적으로 첫 번째 예약된 백업은 *초기 백업*입니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-196">By default, the first scheduled backup is the *initial backup*.</span></span>

![보류 중인 백업](./media/backup-azure-vms-first-look/protection-pending-border.png)

<span data-ttu-id="39a71-198">초기 백업을 지금 시작하려면:</span><span class="sxs-lookup"><span data-stu-id="39a71-198">To start the initial backup now:</span></span>

1. <span data-ttu-id="39a71-199">**보호된 항목** 페이지의 아래쪽에서 **지금 백업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-199">On the **Protected Items** page, click **Backup Now** at the bottom of the page.</span></span>
    <span data-ttu-id="39a71-200">![지금 백업 아이콘](./media/backup-azure-vms-first-look/backup-now-icon.png)</span><span class="sxs-lookup"><span data-stu-id="39a71-200">![Backup Now icon](./media/backup-azure-vms-first-look/backup-now-icon.png)</span></span>

    <span data-ttu-id="39a71-201">Azure Backup 서비스는 초기 백업 작업에 대한 백업 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-201">The Azure Backup service creates a backup job for the initial backup operation.</span></span>
2. <span data-ttu-id="39a71-202">**작업** 탭을 클릭하여 작업 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-202">Click the **Jobs** tab to view the list of jobs.</span></span>

    ![진행 중인 백업](./media/backup-azure-vms-first-look/protect-inprogress.png)

    <span data-ttu-id="39a71-204">초기 백업이 완료되면 **보호된 항목** 탭에서 가상 컴퓨터의 상태가 *보호됨*으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-204">When initial backup is complete, the status of the virtual machine in the **Protected Items** tab is *Protected*.</span></span>

    ![가상 컴퓨터는 복구 지점으로 백업됨](./media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > <span data-ttu-id="39a71-206">가상 컴퓨터 백업은 로컬 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-206">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="39a71-207">한 지역에서 다른 지역의 백업 자격 증명 모음에 가상 컴퓨터를 백업할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-207">You cannot back up virtual machines from one region to a backup vault in another region.</span></span> <span data-ttu-id="39a71-208">따라서 백업해야 하는 VM이 있는 모든 Azure 지역의 경우, 해당 지역에 1개 이상의 백업 저장소가 만들어져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-208">So, for every Azure region that has VMs that need to be backed up, at least one backup vault must be created in that region.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="39a71-209">다음 단계</span><span class="sxs-lookup"><span data-stu-id="39a71-209">Next steps</span></span>
<span data-ttu-id="39a71-210">이제 VM을 성공적으로 백업하면 도움이 될 수 있는 다음 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-210">Now that you have successfully backed up a VM, there are several next steps that could be of interest.</span></span> <span data-ttu-id="39a71-211">가장 논리적인 단계는 사용자 자신이 데이터를 VM에 복원하는 것과 친숙해지는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-211">The most logical step is to familiarize yourself with restoring data to a VM.</span></span> <span data-ttu-id="39a71-212">하지만 데이터를 안전하게 유지하고 비용을 최소화하는 방법을 이해하는 데 도움을 주는 관리 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39a71-212">However, there are management tasks that will help you understand how to keep your data safe and minimize costs.</span></span>

* [<span data-ttu-id="39a71-213">가상 컴퓨터 관리 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="39a71-213">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="39a71-214">가상 컴퓨터 복원</span><span class="sxs-lookup"><span data-stu-id="39a71-214">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
* [<span data-ttu-id="39a71-215">문제 해결 지침</span><span class="sxs-lookup"><span data-stu-id="39a71-215">Troubleshooting guidance</span></span>](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a><span data-ttu-id="39a71-216">질문이 있으십니까?</span><span class="sxs-lookup"><span data-stu-id="39a71-216">Questions?</span></span>
<span data-ttu-id="39a71-217">질문이 있거나 포함되었으면 하는 기능이 있는 경우 [의견을 보내 주세요](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="39a71-217">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>
