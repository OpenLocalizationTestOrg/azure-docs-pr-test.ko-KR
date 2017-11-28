---
title: "Azure 백업을 사용 하 여 Vm을 암호화 aaaBackup 및 복원"
description: "이 문서 hello 백업에 대 한 고 Vm에 대 한 복원 환경을 Azure 디스크 암호화를 사용 하 여 암호화 합니다."
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 8387f186-7d7b-400a-8fc3-88a85403ea63
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/27/2017
ms.author: pajosh;markgal;trinadhk
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c19ef6f58e3259949535dab32a55aaf7a8c658fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-encrypted-virtual-machines-with-azure-backup"></a><span data-ttu-id="f2119-103">tooback 및 복원 Azure 백업을 사용 하 여 가상 컴퓨터를 암호화 된는 방법</span><span class="sxs-lookup"><span data-stu-id="f2119-103">How tooback up and restore encrypted virtual machines with Azure Backup</span></span>
<span data-ttu-id="f2119-104">이 문서의 단계 toobackup 복원 가상 컴퓨터 및 Azure 백업을 사용 하는 방법에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-104">This article talks about steps toobackup and restore virtual machines using Azure Backup.</span></span> <span data-ttu-id="f2119-105">또한 지원되는 시나리오, 필수 조건 및 오류 사례에 대한 문제 해결 조치에 대한 자세한 정보도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-105">It also provides details about supported scenarios, pre-requisites, and troubleshooting steps for error cases.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="f2119-106">지원되는 시나리오</span><span class="sxs-lookup"><span data-stu-id="f2119-106">Supported scenarios</span></span>
> [!NOTE]
> * <span data-ttu-id="f2119-107">암호화된 VM의 백업 및 복원은 Resource Manager에서 배포한 가상 컴퓨터에 대해서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-107">Backup and restore of encrypted VMs is supported only for Resource Manager deployed virtual machines.</span></span> <span data-ttu-id="f2119-108">클래식 가상 컴퓨터에서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-108">It is not supported for Classic virtual machines.</span></span> <br>
> * <span data-ttu-id="f2119-109">Windows hello 업계 표준 BitLocker 기능 및 디스크의 Linux tooprovide 암호화 DM 암호화 기능을 활용 하는 Azure 디스크 암호화를 사용 하 여 Windows와 Linux 가상 컴퓨터에 대해 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-109">It is supported for both Windows and Linux virtual machines using Azure Disk Encryption, which leverages hello industry standard BitLocker feature of Windows and DM-Crypt feature of Linux tooprovide encryption of disks.</span></span> <br>
> * <span data-ttu-id="f2119-110">BitLocker 암호화 키와 키 암호화 키를 모두 사용하여 암호화된 가상 컴퓨터에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-110">It is supported only for virtual machines encrypted using BitLocker Encryption Key and Key Encryption Key both.</span></span> <span data-ttu-id="f2119-111">BitLocker 암호화 키만 사용하여 암호화된 가상 컴퓨터에서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-111">It is not supported for virtual machines encrypted using BitLocker Encryption Key only.</span></span> <br>
>
>

## <a name="prerequisites"></a><span data-ttu-id="f2119-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f2119-112">Prerequisites</span></span>
1. <span data-ttu-id="f2119-113">가상 컴퓨터가 [Azure Disk Encryption](../security/azure-security-disk-encryption.md)을 사용하여 암호화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-113">Virtual machine has been encrypted using [Azure Disk Encryption](../security/azure-security-disk-encryption.md).</span></span> <span data-ttu-id="f2119-114">이 경우 BitLocker 암호화 키와 키 암호화 키를 모두 사용하여 암호화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-114">It should be encrypted using BitLocker Encryption Key and Key Encryption Key both.</span></span>
2. <span data-ttu-id="f2119-115">복구 서비스 자격 증명 모음을 만든 저장소 복제를 사용 하 여 설정 hello 문서에 언급 된 단계와 [백업에 대 한 환경 준비](backup-azure-arm-vms-prepare.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-115">Recovery services vault has been created and storage replication set using steps mentioned in hello article [Prepare your environment for backup](backup-azure-arm-vms-prepare.md).</span></span>
3. <span data-ttu-id="f2119-116">Azure 백업에 지정 된 [권한 tooaccess 주요 자격 증명 모음](#provide-permissions-to-azure-backup) 에 대 한 비밀 암호화 키가 포함 된, Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-116">Azure Backup has been given [permissions tooaccess key vault](#provide-permissions-to-azure-backup) containing keys, secrets for encrypted VMs.</span></span>

## <a name="backup-encrypted-vm"></a><span data-ttu-id="f2119-117">암호화된 VM 백업</span><span class="sxs-lookup"><span data-stu-id="f2119-117">Backup encrypted VM</span></span>
<span data-ttu-id="f2119-118">단계 tooset 백업 목표를 수행 하는 hello를 사용 하 여 하 고, 정책을 정의 하 고, 항목 및 트리거 백업 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-118">Use hello following steps tooset backup goal, define policy, configure items and trigger backup.</span></span>

### <a name="configure-backup"></a><span data-ttu-id="f2119-119">백업 구성</span><span class="sxs-lookup"><span data-stu-id="f2119-119">Configure backup</span></span>
1. <span data-ttu-id="f2119-120">복구 서비스 자격 증명 모음 열고 이미 있는 경우 toonext 단계를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-120">If you already have a Recovery Services vault open, proceed toonext step.</span></span> <span data-ttu-id="f2119-121">복구 서비스 자격 증명 모음 열기를 갖지 않는 hello hello 허브 메뉴에서 Azure 포털에 있지만 클릭 **찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-121">If you do not have a Recovery Services vault open, but are in hello Azure portal, on hello Hub menu, click **Browse**.</span></span>

   * <span data-ttu-id="f2119-122">Hello 리소스 목록에 입력 **복구 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-122">In hello list of resources, type **Recovery Services**.</span></span>
   * <span data-ttu-id="f2119-123">입력을 시작할 때 hello 사용자 입력에 따라 필터를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-123">As you begin typing, hello list filters based on your input.</span></span> <span data-ttu-id="f2119-124">**복구 서비스 자격 증명 모음**이 표시되면 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-124">When you see **Recovery Services vaults**, click it.</span></span>

      ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     <span data-ttu-id="f2119-126">복구 서비스 자격 증명 모음 hello 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-126">hello list of Recovery Services vaults appears.</span></span> <span data-ttu-id="f2119-127">복구 서비스 자격 증명 모음 hello 목록에서 자격 증명 모음을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-127">From hello list of Recovery Services vaults, select a vault.</span></span>

     <span data-ttu-id="f2119-128">hello 선택한 자격 증명 모음 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-128">hello selected vault dashboard opens.</span></span>
2. <span data-ttu-id="f2119-129">Hello 목록에서 항목의 자격 증명 모음 아래에 나타나는 클릭 **백업** tooopen hello 백업 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-129">From hello list of items that appears under vault, click **Backup** tooopen hello Backup blade.</span></span>

      ![백업 블레이드 열기](./media/backup-azure-vms-encryption/select-backup.png)
3. <span data-ttu-id="f2119-131">Hello 백업 블레이드에서 클릭 **백업 목표** tooopen hello 백업 목표 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-131">On hello Backup blade, click **Backup goal** tooopen hello Backup Goal blade.</span></span>

      ![시나리오 블레이드 열기](./media/backup-azure-vms-encryption/select-backup-goal-one.png)
4. <span data-ttu-id="f2119-133">Hello 백업 목표 블레이드에서 설정 **여기서 작업이 실행 되는** tooAzure 및 **어떻게 하 시겠습니까 toobackup 원하는** tooVirtual 클릭 한 다음 컴퓨터을 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-133">On hello Backup Goal blade, set **Where is your workload running** tooAzure and **What do you want toobackup** tooVirtual machine, then click **OK**.</span></span>

   <span data-ttu-id="f2119-134">hello 백업 목표 블레이드 닫히고 hello 백업 정책 블레이드에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-134">hello Backup Goal blade closes and hello Backup policy blade opens.</span></span>

   ![시나리오 블레이드 열기](./media/backup-azure-vms-encryption/select-backup-goal-two.png)
5. <span data-ttu-id="f2119-136">Hello 백업 정책 블레이드에서 tooapply toohello 자격 증명 모음을 클릭 하 여 hello 백업 정책을 선택 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-136">On hello Backup policy blade, select hello backup policy you want tooapply toohello vault and click **OK**.</span></span>

      ![백업 정책 선택](./media/backup-azure-vms-encryption/setting-rs-backup-policy-new.png)

    <span data-ttu-id="f2119-138">hello 기본 정책의 hello 세부 정보는 hello 세부 정보에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-138">hello details of hello default policy are listed in hello details.</span></span> <span data-ttu-id="f2119-139">Toocreate 정책을 선택 **새로 만들기** hello 드롭 다운 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-139">If you want toocreate a policy, select **Create New** from hello drop-down menu.</span></span> <span data-ttu-id="f2119-140">클릭 한 후 **확인**, hello 백업 정책을 hello 자격 증명 모음과 연결 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-140">Once you click **OK**, hello backup policy is associated with hello vault.</span></span>

    <span data-ttu-id="f2119-141">그런 다음 hello Vm tooassociate hello 자격 증명 모음을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-141">Next choose hello VMs tooassociate with hello vault.</span></span>
6. <span data-ttu-id="f2119-142">Hello 암호화 tooassociate hello로 정책을 지정 하 고 클릭 하 여 가상 컴퓨터 선택 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-142">Choose hello encrypted virtual machines tooassociate with hello specified policy and click **OK**.</span></span>

      ![암호화된 VM 선택](./media/backup-azure-vms-encryption/selected-encrypted-vms.png)
7. <span data-ttu-id="f2119-144">이 페이지에는 암호화 관련된 toohello Vm 선택 키 자격 증명 모음에 대 한 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-144">This page shows a message about key vault associated toohello encrypted VMs selected.</span></span> <span data-ttu-id="f2119-145">백업 서비스에는 읽기 전용 액세스 toohello 키와 hello 키 자격 증명 모음의 암호 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-145">Backup service requires read-only access toohello keys and secrets in hello key vault.</span></span> <span data-ttu-id="f2119-146">사용 하 여 이러한 권한을 toobackup 키 및 비밀 hello 함께 Vm 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-146">It uses these permissions toobackup key and secret, along with hello associated VMs.</span></span> <span data-ttu-id="f2119-147">**백업 toowork에 대 한 사용 권한을 toobackup 서비스 tooaccess 주요 자격 증명 모음을 부여 해야**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-147">**You must give permissions toobackup service tooaccess key vault for backups toowork**.</span></span> <span data-ttu-id="f2119-148">사용 하 여 이러한 권한을 제공할 수 있습니다 [hello 섹션 아래에 설명 된 단계](#provide-permissions-to-azure-backup)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-148">You can provide these permissions using [steps mentioned in hello section below](#provide-permissions-to-azure-backup).</span></span>

      ![암호화된 VM 메시지](./media/backup-azure-vms-encryption/encrypted-vm-warning-message.png)

      <span data-ttu-id="f2119-150">이제 정의한 hello 백업 블레이드에서 hello 자격 증명 모음에 대 한 모든 설정을 클릭 hello hello 페이지 맨 아래에 대 한 백업 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-150">Now that you have defined all settings for hello vault, in hello Backup blade click Enable Backup at hello bottom of hello page.</span></span> <span data-ttu-id="f2119-151">사용 하도록 설정 백업 hello 정책 toohello 자격 증명 모음 및 hello Vm에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-151">Enable  Backup deploys hello policy toohello vault and hello VMs.</span></span>
8. <span data-ttu-id="f2119-152">hello 준비 과정에서 다음 단계를 설치 하는 hello VM 에이전트 또는 작업 있는지 hello VM 에이전트가 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-152">hello next phase in preparation is installing hello VM Agent or making sure hello VM Agent is installed.</span></span> <span data-ttu-id="f2119-153">toodo 동일 hello, hello 문서에 언급 된 hello 단계를 사용 하 여 [백업에 대 한 환경 준비](backup-azure-arm-vms-prepare.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-153">toodo hello same, use hello steps mentioned in hello article [Prepare your environment for backup](backup-azure-arm-vms-prepare.md).</span></span>

### <a name="triggering-backup-job"></a><span data-ttu-id="f2119-154">백업 작업 트리거</span><span class="sxs-lookup"><span data-stu-id="f2119-154">Triggering backup job</span></span>
<span data-ttu-id="f2119-155">Hello 문서에 언급 된 hello 단계를 사용 하 여 [백업 Azure Vm toorecovery 서비스 자격 증명 모음](backup-azure-arm-vms.md) tootrigger 백업 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-155">Use hello steps mentioned in hello article [Backup Azure VMs toorecovery services vault](backup-azure-arm-vms.md) tootrigger backup job.</span></span>

### <a name="continue-backups-of-already-backed-up-vms-with-encryption-enabled"></a><span data-ttu-id="f2119-156">암호화를 설정한 상태로 이미 백업한 VM의 백업 계속</span><span class="sxs-lookup"><span data-stu-id="f2119-156">Continue backups of already backed up VMs with encryption enabled</span></span>  
<span data-ttu-id="f2119-157">Vm 복구 서비스 자격 증명 모음에 백업 되 고 이미 있고 나중에는 암호화에 사용 된 경우 백업 toocontinue에 대 한 사용 권한을 toobackup 서비스 tooaccess 주요 자격 증명 모음을 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-157">If you have VMs already being backup up in recovery services vault and have been enabled for encryption at a later point, you must give permissions toobackup service tooaccess key vault for backups toocontinue.</span></span> <span data-ttu-id="f2119-158">사용 하 여 이러한 권한을 제공할 수 있습니다 [아래 hello 섹션의 단계를](#provide-permissions-to-azure-backup) PowerShell을 사용 하 여에서 언급 한 단계 또는 **백업 사용** 섹션 [PowerShell 설명서](backup-azure-vms-automation.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-158">You can provide these permissions using [steps in hello section below](#provide-permissions-to-azure-backup) or using PowerShell steps mentioned in **Enable Backup** section of [PowerShell documentation](backup-azure-vms-automation.md).</span></span> 

## <a name="provide-permissions-tooazure-backup"></a><span data-ttu-id="f2119-159">사용 권한 tooAzure 백업 제공</span><span class="sxs-lookup"><span data-stu-id="f2119-159">Provide permissions tooAzure Backup</span></span>
<span data-ttu-id="f2119-160">단계 tooprovide 관련 사용 권한을 tooAzure 백업 tooaccess 주요 자격 증명 모음을 수행 하는 hello를 사용 하 고 암호화 된 Vm의 백업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-160">Use hello following steps tooprovide relevant permissions tooAzure Backup tooaccess key vault and perform backup of encrypted VMs:</span></span>
1. <span data-ttu-id="f2119-161">**추가 서비스**를 선택하고 **키 자격 증명 모음**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-161">Select **More Services** and search for **Key vaults**.</span></span>

    ![키 자격 증명 모음 검색](./media/backup-azure-vms-encryption/search-key-vault.png)
    
2. <span data-ttu-id="f2119-163">키 자격 증명 모음 hello 목록에서 hello 주요 자격 증명 모음 관련 된 백업 toobe는 암호화 된 VM과 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-163">From hello list of key vaults, select hello key vault associated with encrypted VM, which needs toobe backed up.</span></span>

     ![키 자격 증명 모음 선택](./media/backup-azure-vms-encryption/select-key-vault.png)
     
3. <span data-ttu-id="f2119-165">**액세스 정책** 및 **새로 추가**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-165">Click **Access policies** and then **Add new**.</span></span>

    ![액세스 정책 추가](./media/backup-azure-vms-encryption/select-key-vault-access-policy.png)
    
4. <span data-ttu-id="f2119-167">클릭 **보안 주체 선택** 유형과 **백업 관리 서비스** hello 검색 표시줄에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-167">Click **Select principal** and type **Backup Management Service** in hello search bar.</span></span> 

    ![백업 서비스 검색](./media/backup-azure-vms-encryption/search-backup-service.png)
    
5. <span data-ttu-id="f2119-169">**백업 관리 서비스**를 선택하고 선택 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-169">Select **Backup Management Service** and click Select button.</span></span>

    ![백업 서비스 선택](./media/backup-azure-vms-encryption/select-backup-service.png)
    
6. <span data-ttu-id="f2119-171">템플릿 드롭다운의 구성에서 **Azure Backup**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-171">Select **Azure Backup** in Configure from template drop down.</span></span> <span data-ttu-id="f2119-172">키 사용 권한에서 hello 필요한 권한을 미리 채우도록 및 보안 권한을 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-172">It pre-fills hello required permissions in Key permissions and Secret permissions drop down.</span></span> 

    ![Azure Backup 선택](./media/backup-azure-vms-encryption/select-backup-template.png)
    
7. <span data-ttu-id="f2119-174">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-174">Click **OK**.</span></span> <span data-ttu-id="f2119-175">Backup Management Service를 액세스 정책 블레이드에서 추가했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-175">Notice that Backup Management Service gets added in Access Policies blade.</span></span> 

    ![서비스 액세스 정책 백업](./media/backup-azure-vms-encryption/backup-service-access-policy.png)
    
8. <span data-ttu-id="f2119-177">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-177">Click **Save**.</span></span> <span data-ttu-id="f2119-178">이렇게 하면 필요한 hello 권한 tooAzure 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-178">This will give hello required permissions tooAzure Backup.</span></span>

    ![서비스 액세스 정책 백업](./media/backup-azure-vms-encryption/save-access-policy.png)

<span data-ttu-id="f2119-180">사용 권한이 성공적으로 주어지면 암호화된 VM에 백업을 사용하도록 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-180">Once permissions are successfully provided, you can proceed with enabling backup for encrypted VMs.</span></span>

## <a name="restore-encrypted-vm"></a><span data-ttu-id="f2119-181">암호화된 VM 복원</span><span class="sxs-lookup"><span data-stu-id="f2119-181">Restore encrypted VM</span></span>
<span data-ttu-id="f2119-182">toorestore VM 암호화, 섹션에서 설명 된 단계를 사용 하 여 첫 번째 복원 디스크 **디스크 백업 복원** 에 [선택 VM 구성 복원](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-182">toorestore encrypted VM, first Restore Disks using steps mentioned in section **Restore backed up disks** in [Choosing VM restore configuration](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration).</span></span> <span data-ttu-id="f2119-183">그 후 hello 다음 옵션 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-183">After that, you can use one of hello following options:</span></span>
* <span data-ttu-id="f2119-184">에 언급 된 hello PowerShell 단계를 사용 하 여 [복원 된 디스크에서 VM을 만들](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate 복원 된 디스크에서 VM을 전체.</span><span class="sxs-lookup"><span data-stu-id="f2119-184">Use hello PowerShell steps mentioned in [Create a VM from restored disks](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate full VM from restored disks.</span></span>
* <span data-ttu-id="f2119-185">OR, [디스크 복원의 일부로 생성 된 서식 파일을 사용](backup-azure-arm-restore-vms.md#use-templates-to-customize-restore-vm) 복원 된 디스크에서 Vm toocreate 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-185">OR, [Use template generated as part of Restore Disks](backup-azure-arm-restore-vms.md#use-templates-to-customize-restore-vm) toocreate VMs from restored disks.</span></span> <span data-ttu-id="f2119-186">템플릿은 2017년 4월 26일 이후에 만들어진 복원 지점에 대해서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-186">Templates can be used only for recovery points created after 26 April 2017.</span></span>

## <a name="troubleshooting-errors"></a><span data-ttu-id="f2119-187">문제 해결 오류</span><span class="sxs-lookup"><span data-stu-id="f2119-187">Troubleshooting errors</span></span>
| <span data-ttu-id="f2119-188">작업</span><span class="sxs-lookup"><span data-stu-id="f2119-188">Operation</span></span> | <span data-ttu-id="f2119-189">오류 세부 정보</span><span class="sxs-lookup"><span data-stu-id="f2119-189">Error details</span></span> | <span data-ttu-id="f2119-190">해결 방법</span><span class="sxs-lookup"><span data-stu-id="f2119-190">Resolution</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f2119-191">백업</span><span class="sxs-lookup"><span data-stu-id="f2119-191">Backup</span></span> |<span data-ttu-id="f2119-192">가상 컴퓨터가 BEK만으로 암호화되었기 때문에 유효성 검사에 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-192">Validation failed as virtual machine is encrypted with BEK alone.</span></span> <span data-ttu-id="f2119-193">BEK와 KEK 모두로 암호화된 가상 컴퓨터에서만 백업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-193">Backups can be enabled only for virtual machines encrypted with both BEK and KEK.</span></span> |<span data-ttu-id="f2119-194">가상 컴퓨터는 BEK와 KEK를 사용하여 암호화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-194">Virtual machine should be encrypted using BEK and KEK.</span></span> <span data-ttu-id="f2119-195">먼저 hello VM의 암호를 해독 하 고 BEK와 KEK를 사용 하 여 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-195">First decrypt hello VM and encrypt it using both BEK and KEK.</span></span> <span data-ttu-id="f2119-196">VM이 BEK와 KEK를 사용하여 암호화되면 백업을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-196">Enable backup once VM is encrypted using both BEK and KEK.</span></span> <span data-ttu-id="f2119-197">자세한 내용은 하는 방법에 대 한 자세한 [암호를 해독 하 고 hello VM 암호화](../security/azure-security-disk-encryption.md)</span><span class="sxs-lookup"><span data-stu-id="f2119-197">Learn more on how you can [decrypt and encrypt hello VM](../security/azure-security-disk-encryption.md)</span></span>  |
| <span data-ttu-id="f2119-198">복원</span><span class="sxs-lookup"><span data-stu-id="f2119-198">Restore</span></span> |<span data-ttu-id="f2119-199">이 VM과 연결된 키 자격 증명 모음이 없기 때문에 이 암호화된 VM을 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-199">You cannot restore this encrypted VM since key vault associated with this VM does not exist.</span></span> |<span data-ttu-id="f2119-200">키 자격 증명 모음을 만들려면 [Azure Key Vault 시작](../key-vault/key-vault-get-started.md)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-200">Create key vault using [Get Started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span> <span data-ttu-id="f2119-201">Hello 문서 참조 [주요 자격 증명 모음 키와 Azure Backup을 사용 하 여 보안을 복원](backup-azure-restore-key-secret.md) toorestore 키와 암호가 동일한 경우 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-201">Refer hello article [Restore key vault key and secret using Azure Backup](backup-azure-restore-key-secret.md) toorestore key and secret if they are not present.</span></span> |
| <span data-ttu-id="f2119-202">복원</span><span class="sxs-lookup"><span data-stu-id="f2119-202">Restore</span></span> |<span data-ttu-id="f2119-203">이 VM과 연결된 키와 비밀이 없기 때문에 이 암호화된 VM을 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-203">You cannot restore this encrypted VM since key and secret associated with this VM do not exist.</span></span> |<span data-ttu-id="f2119-204">Hello 문서 참조 [주요 자격 증명 모음 키와 Azure Backup을 사용 하 여 보안을 복원](backup-azure-restore-key-secret.md) toorestore 키와 암호가 동일한 경우 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-204">Refer hello article [Restore key vault key and secret using Azure Backup](backup-azure-restore-key-secret.md) toorestore key and secret if they are not present.</span></span> |
| <span data-ttu-id="f2119-205">복원</span><span class="sxs-lookup"><span data-stu-id="f2119-205">Restore</span></span> |<span data-ttu-id="f2119-206">백업 서비스 구독에 있는 권한 부여 tooaccess 리소스가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-206">Backup Service does not have authorization tooaccess resources in your subscription.</span></span> |<span data-ttu-id="f2119-207">위에서 설명된 것처럼 먼저 [VM 복원 구성 선택](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration)의 **백업된 디스크 복원** 섹션에 제공된 단계에 따라 디스크를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-207">As mentioned above, Restore Disks first, using steps mentioned in section **Restore backed up disks** in [Choosing VM restore configuration](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration).</span></span> <span data-ttu-id="f2119-208">PowerShell 사용자, 후 너무[복원 된 디스크에서 VM을 만들](backup-azure-vms-automation.md#create-a-vm-from-restored-disks)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-208">After that, user PowerShell too[Create a VM from restored disks](backup-azure-vms-automation.md#create-a-vm-from-restored-disks).</span></span> |
|<span data-ttu-id="f2119-209">백업</span><span class="sxs-lookup"><span data-stu-id="f2119-209">Backup</span></span> | <span data-ttu-id="f2119-210">Azure 백업 서비스에 없는 충분 한 사용 권한을 tooKey 자격 증명 모음에 대 한 백업을 암호화 가상 컴퓨터의</span><span class="sxs-lookup"><span data-stu-id="f2119-210">Azure Backup Service does not have sufficient permissions tooKey Vault for Backup of Encrypted Virtual Machines</span></span> | <span data-ttu-id="f2119-211">이 경우 가상 시스템을 BitLocker 암호화 키와 키 암호화 키를 모두 사용하여 암호화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-211">Virtual machine should be encrypted using both BitLocker Encryption Key and Key Encryption Key.</span></span> <span data-ttu-id="f2119-212">그런 후에 백업을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-212">After that, backup should be enabled.</span></span>  <span data-ttu-id="f2119-213">백업 서비스를 사용 하 여 이러한 권한을 제공 해야 [위의 hello 섹션에서 언급 한 단계](#provide-permissions-to-azure-backup) 또는 hello에 언급 된 PowerShell 단계를 사용 하 여 **보호 사용** hello PowerShell의 섹션 설명서 [가상 컴퓨터를 사용 하 여 AzureRM.RecoveryServices.Backup cmdlet tooback](backup-azure-vms-automation.md#back-up-azure-vms)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2119-213">Backup service should be provided these permissions using [steps mentioned in hello section above](#provide-permissions-to-azure-backup) or by using PowerShell steps mentioned in hello **Enable protection** section of hello PowerShell documentation at [Use AzureRM.RecoveryServices.Backup cmdlets tooback up virtual machines](backup-azure-vms-automation.md#back-up-azure-vms).</span></span> |  
