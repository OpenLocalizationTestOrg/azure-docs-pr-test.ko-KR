---
title: "Azure Backup으로 암호화된 VM 백업 및 복원"
description: "이 문서에서는 Azure Disk Encryption을 사용하여 암호화된 VM의 백업 및 복원 환경에 대해 설명합니다."
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
ms.openlocfilehash: 89492cda8eff23509bee7693bb5f7e6ab5eb10d1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-back-up-and-restore-encrypted-virtual-machines-with-azure-backup"></a><span data-ttu-id="a7782-103">Azure Backup으로 암호화된 가상 컴퓨터를 백업 및 복원하는 방법</span><span class="sxs-lookup"><span data-stu-id="a7782-103">How to back up and restore encrypted virtual machines with Azure Backup</span></span>
<span data-ttu-id="a7782-104">이 문서에서는 Azure Backup을 사용하여 가상 컴퓨터를 백업하고 복원하는 단계에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-104">This article talks about steps to backup and restore virtual machines using Azure Backup.</span></span> <span data-ttu-id="a7782-105">또한 지원되는 시나리오, 필수 조건 및 오류 사례에 대한 문제 해결 조치에 대한 자세한 정보도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-105">It also provides details about supported scenarios, pre-requisites, and troubleshooting steps for error cases.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="a7782-106">지원되는 시나리오</span><span class="sxs-lookup"><span data-stu-id="a7782-106">Supported scenarios</span></span>
> [!NOTE]
> * <span data-ttu-id="a7782-107">암호화된 VM의 백업 및 복원은 Resource Manager에서 배포한 가상 컴퓨터에 대해서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-107">Backup and restore of encrypted VMs is supported only for Resource Manager deployed virtual machines.</span></span> <span data-ttu-id="a7782-108">클래식 가상 컴퓨터에서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-108">It is not supported for Classic virtual machines.</span></span> <br>
> * <span data-ttu-id="a7782-109">Azure Disk Encryption을 사용하는 Windows 및 Linux Virtual Machines 둘 다에 대해 지원됩니다. 이 암호화 방식은 Windows의 업계 표준 BitLocker 기능과 Linux의 DM 암호화 기능을 활용하여 디스크 암호화 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-109">It is supported for both Windows and Linux virtual machines using Azure Disk Encryption, which leverages the industry standard BitLocker feature of Windows and DM-Crypt feature of Linux to provide encryption of disks.</span></span> <br>
> * <span data-ttu-id="a7782-110">BitLocker 암호화 키와 키 암호화 키를 모두 사용하여 암호화된 가상 컴퓨터에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-110">It is supported only for virtual machines encrypted using BitLocker Encryption Key and Key Encryption Key both.</span></span> <span data-ttu-id="a7782-111">BitLocker 암호화 키만 사용하여 암호화된 가상 컴퓨터에서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-111">It is not supported for virtual machines encrypted using BitLocker Encryption Key only.</span></span> <br>
>
>

## <a name="prerequisites"></a><span data-ttu-id="a7782-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a7782-112">Prerequisites</span></span>
1. <span data-ttu-id="a7782-113">가상 컴퓨터가 [Azure Disk Encryption](../security/azure-security-disk-encryption.md)을 사용하여 암호화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-113">Virtual machine has been encrypted using [Azure Disk Encryption](../security/azure-security-disk-encryption.md).</span></span> <span data-ttu-id="a7782-114">이 경우 BitLocker 암호화 키와 키 암호화 키를 모두 사용하여 암호화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-114">It should be encrypted using BitLocker Encryption Key and Key Encryption Key both.</span></span>
2. <span data-ttu-id="a7782-115">[백업 환경 준비](backup-azure-arm-vms-prepare.md)에서 언급한 단계를 사용하여 복구 서비스 자격 증명 모음이 만들어졌으며 저장소 복제가 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-115">Recovery services vault has been created and storage replication set using steps mentioned in the article [Prepare your environment for backup](backup-azure-arm-vms-prepare.md).</span></span>
3. <span data-ttu-id="a7782-116">Azure Backup에는 암호화된 VM에 대한 키, 비밀을 포함한 [키 자격 증명 모음에 액세스할 수 있는 사용 권한](#provide-permissions-to-azure-backup)이 지정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-116">Azure Backup has been given [permissions to access key vault](#provide-permissions-to-azure-backup) containing keys, secrets for encrypted VMs.</span></span>

## <a name="backup-encrypted-vm"></a><span data-ttu-id="a7782-117">암호화된 VM 백업</span><span class="sxs-lookup"><span data-stu-id="a7782-117">Backup encrypted VM</span></span>
<span data-ttu-id="a7782-118">다음 단계를 사용하여 백업 목표를 설정하고, 정책을 정의하며, 항목을 구성하고, 백업을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-118">Use the following steps to set backup goal, define policy, configure items and trigger backup.</span></span>

### <a name="configure-backup"></a><span data-ttu-id="a7782-119">백업 구성</span><span class="sxs-lookup"><span data-stu-id="a7782-119">Configure backup</span></span>
1. <span data-ttu-id="a7782-120">이미 Recovery Services 자격 증명 모음이 열려 있으면 다음 단계로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-120">If you already have a Recovery Services vault open, proceed to next step.</span></span> <span data-ttu-id="a7782-121">복구 서비스 자격 증명 모음이 열려 있지 않지만 Azure 포털에 있는 경우 허브 메뉴에서 **찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-121">If you do not have a Recovery Services vault open, but are in the Azure portal, on the Hub menu, click **Browse**.</span></span>

   * <span data-ttu-id="a7782-122">리소스 목록에서 **복구 서비스**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-122">In the list of resources, type **Recovery Services**.</span></span>
   * <span data-ttu-id="a7782-123">입력을 시작하면 입력한 내용을 바탕으로 목록이 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-123">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="a7782-124">**복구 서비스 자격 증명 모음**이 표시되면 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-124">When you see **Recovery Services vaults**, click it.</span></span>

      ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     <span data-ttu-id="a7782-126">복구 서비스 자격 증명 모음의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-126">The list of Recovery Services vaults appears.</span></span> <span data-ttu-id="a7782-127">복구 서비스 자격 증명 모음의 목록에서 자격 증명 모음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-127">From the list of Recovery Services vaults, select a vault.</span></span>

     <span data-ttu-id="a7782-128">선택한 자격 증명 모음 대시보드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-128">The selected vault dashboard opens.</span></span>
2. <span data-ttu-id="a7782-129">자격 증명 모음 아래쪽에 나타나는 항목 목록에서 **백업**을 클릭하여 [백업] 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-129">From the list of items that appears under vault, click **Backup** to open the Backup blade.</span></span>

      ![백업 블레이드 열기](./media/backup-azure-vms-encryption/select-backup.png)
3. <span data-ttu-id="a7782-131">백업 블레이드에서 **백업 목표** 를 클릭하여 백업 목표 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-131">On the Backup blade, click **Backup goal** to open the Backup Goal blade.</span></span>

      ![시나리오 블레이드 열기](./media/backup-azure-vms-encryption/select-backup-goal-one.png)
4. <span data-ttu-id="a7782-133">[백업 목표] 블레이드에서 **워크로드 실행 위치**를 Azure로 설정하고 **백업할 항목**을 가상 컴퓨터로 설정한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-133">On the Backup Goal blade, set **Where is your workload running** to Azure and **What do you want to backup** to Virtual machine, then click **OK**.</span></span>

   <span data-ttu-id="a7782-134">백업 목표 블레이드가 닫히고 백업 정책 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-134">The Backup Goal blade closes and the Backup policy blade opens.</span></span>

   ![시나리오 블레이드 열기](./media/backup-azure-vms-encryption/select-backup-goal-two.png)
5. <span data-ttu-id="a7782-136">백업 정책 블레이드에서 자격 증명 모음에 적용할 백업 정책을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-136">On the Backup policy blade, select the backup policy you want to apply to the vault and click **OK**.</span></span>

      ![백업 정책 선택](./media/backup-azure-vms-encryption/setting-rs-backup-policy-new.png)

    <span data-ttu-id="a7782-138">상세 정보에 기본 정책에 대한 자세한 내용이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-138">The details of the default policy are listed in the details.</span></span> <span data-ttu-id="a7782-139">정책을 만들려는 경우 드롭다운 메뉴에서 **새로 만들기** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-139">If you want to create a policy, select **Create New** from the drop-down menu.</span></span> <span data-ttu-id="a7782-140">**확인**을 클릭하면 백업 정책이 자격 증명 모음과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-140">Once you click **OK**, the backup policy is associated with the vault.</span></span>

    <span data-ttu-id="a7782-141">다음으로 자격 증명 모음과 연결할 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-141">Next choose the VMs to associate with the vault.</span></span>
6. <span data-ttu-id="a7782-142">지정된 정책과 연결할 암호화된 가상 컴퓨터를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-142">Choose the encrypted virtual machines to associate with the specified policy and click **OK**.</span></span>

      ![암호화된 VM 선택](./media/backup-azure-vms-encryption/selected-encrypted-vms.png)
7. <span data-ttu-id="a7782-144">이 페이지에서는 선택한 암호화된 VM에 연결된 키 자격 증명 모음에 대한 메시지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-144">This page shows a message about key vault associated to the encrypted VMs selected.</span></span> <span data-ttu-id="a7782-145">백업 서비스를 사용하려면 키 자격 증명 모음의 키와 비밀에 대한 읽기 전용 액세스 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-145">Backup service requires read-only access to the keys and secrets in the key vault.</span></span> <span data-ttu-id="a7782-146">이 권한을 사용하여 연결된 VM과 함께 키와 암호를 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-146">It uses these permissions to backup key and secret, along with the associated VMs.</span></span> <span data-ttu-id="a7782-147">**백업 서비스에 백업이 작동하도록 키 자격 증명 모음에 액세스하는 권한을 부여해야 합니다**.</span><span class="sxs-lookup"><span data-stu-id="a7782-147">**You must give permissions to backup service to access key vault for backups to work**.</span></span> <span data-ttu-id="a7782-148">[아래 섹션에 설명된 단계](#provide-permissions-to-azure-backup)를 사용하여 이러한 사용 권한을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-148">You can provide these permissions using [steps mentioned in the section below](#provide-permissions-to-azure-backup).</span></span>

      ![암호화된 VM 메시지](./media/backup-azure-vms-encryption/encrypted-vm-warning-message.png)

      <span data-ttu-id="a7782-150">이제 자격 증명 모음의 모든 설정을 정의했으므로 [백업] 블레이드에서 페이지 아래쪽의 [백업 사용]을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-150">Now that you have defined all settings for the vault, in the Backup blade click Enable Backup at the bottom of the page.</span></span> <span data-ttu-id="a7782-151">[백업 사용]은 정책을 자격 증명 모음 및 VM에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-151">Enable  Backup deploys the policy to the vault and the VMs.</span></span>
8. <span data-ttu-id="a7782-152">다음 준비 단계는 VM 에이전트를 설치하거나 VM 에이전트가 설치되었는지 확인하는 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-152">The next phase in preparation is installing the VM Agent or making sure the VM Agent is installed.</span></span> <span data-ttu-id="a7782-153">이 작업을 수행하려면 [백업 환경 준비](backup-azure-arm-vms-prepare.md)에서 언급한 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-153">To do the same, use the steps mentioned in the article [Prepare your environment for backup](backup-azure-arm-vms-prepare.md).</span></span>

### <a name="triggering-backup-job"></a><span data-ttu-id="a7782-154">백업 작업 트리거</span><span class="sxs-lookup"><span data-stu-id="a7782-154">Triggering backup job</span></span>
<span data-ttu-id="a7782-155">백업 작업을 트리거하려면 [복구 서비스 자격 증명 모음에 Azure VM 백업](backup-azure-arm-vms.md) 문서에서 언급한 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-155">Use the steps mentioned in the article [Backup Azure VMs to recovery services vault](backup-azure-arm-vms.md) to trigger backup job.</span></span>

### <a name="continue-backups-of-already-backed-up-vms-with-encryption-enabled"></a><span data-ttu-id="a7782-156">암호화를 설정한 상태로 이미 백업한 VM의 백업 계속</span><span class="sxs-lookup"><span data-stu-id="a7782-156">Continue backups of already backed up VMs with encryption enabled</span></span>  
<span data-ttu-id="a7782-157">복구 서비스 자격 증명 모음에서 VM이 이미 백업되었으며 나중에 암호화가 설정된 경우 백업이 계속될 수 있게 백업 서비스에 Key Vault에 액세스할 수 있는 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-157">If you have VMs already being backup up in recovery services vault and have been enabled for encryption at a later point, you must give permissions to backup service to access key vault for backups to continue.</span></span> <span data-ttu-id="a7782-158">[아래 섹션의 단계](#provide-permissions-to-azure-backup) 또는 [PowerShell 설명서](backup-azure-vms-automation.md)의 **백업 사용** 섹션에서 설명한 PowerShell 단계를 사용하여 이러한 사용 권한을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-158">You can provide these permissions using [steps in the section below](#provide-permissions-to-azure-backup) or using PowerShell steps mentioned in **Enable Backup** section of [PowerShell documentation](backup-azure-vms-automation.md).</span></span> 

## <a name="provide-permissions-to-azure-backup"></a><span data-ttu-id="a7782-159">Azure Backup에 사용 권한 제공</span><span class="sxs-lookup"><span data-stu-id="a7782-159">Provide permissions to Azure Backup</span></span>
<span data-ttu-id="a7782-160">키 자격 증명 모음에 액세스하고 암호화된 VM의 백업을 수행하기 위해 다음 단계를 사용하여 Azure Backup에 관련 사용 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-160">Use the following steps to provide relevant permissions to Azure Backup to access key vault and perform backup of encrypted VMs:</span></span>
1. <span data-ttu-id="a7782-161">**추가 서비스**를 선택하고 **키 자격 증명 모음**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-161">Select **More Services** and search for **Key vaults**.</span></span>

    ![키 자격 증명 모음 검색](./media/backup-azure-vms-encryption/search-key-vault.png)
    
2. <span data-ttu-id="a7782-163">키 자격 증명 모음 목록에서 백업해야 하는 암호화된 VM에 관련된 키 자격 증명 모음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-163">From the list of key vaults, select the key vault associated with encrypted VM, which needs to be backed up.</span></span>

     ![키 자격 증명 모음 선택](./media/backup-azure-vms-encryption/select-key-vault.png)
     
3. <span data-ttu-id="a7782-165">**액세스 정책** 및 **새로 추가**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-165">Click **Access policies** and then **Add new**.</span></span>

    ![액세스 정책 추가](./media/backup-azure-vms-encryption/select-key-vault-access-policy.png)
    
4. <span data-ttu-id="a7782-167">**보안 주체 선택**을 클릭하고 검색 창에서 **백업 관리 서비스**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-167">Click **Select principal** and type **Backup Management Service** in the search bar.</span></span> 

    ![백업 서비스 검색](./media/backup-azure-vms-encryption/search-backup-service.png)
    
5. <span data-ttu-id="a7782-169">**백업 관리 서비스**를 선택하고 선택 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-169">Select **Backup Management Service** and click Select button.</span></span>

    ![백업 서비스 선택](./media/backup-azure-vms-encryption/select-backup-service.png)
    
6. <span data-ttu-id="a7782-171">템플릿 드롭다운의 구성에서 **Azure Backup**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-171">Select **Azure Backup** in Configure from template drop down.</span></span> <span data-ttu-id="a7782-172">키 사용 권한 및 비밀 사용 권한 드롭다운에서 필요한 권한을 미리 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-172">It pre-fills the required permissions in Key permissions and Secret permissions drop down.</span></span> 

    ![Azure Backup 선택](./media/backup-azure-vms-encryption/select-backup-template.png)
    
7. <span data-ttu-id="a7782-174">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-174">Click **OK**.</span></span> <span data-ttu-id="a7782-175">Backup Management Service를 액세스 정책 블레이드에서 추가했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-175">Notice that Backup Management Service gets added in Access Policies blade.</span></span> 

    ![서비스 액세스 정책 백업](./media/backup-azure-vms-encryption/backup-service-access-policy.png)
    
8. <span data-ttu-id="a7782-177">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-177">Click **Save**.</span></span> <span data-ttu-id="a7782-178">이렇게 하면 Azure Backup에 필요한 사용 권한이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-178">This will give the required permissions to Azure Backup.</span></span>

    ![서비스 액세스 정책 백업](./media/backup-azure-vms-encryption/save-access-policy.png)

<span data-ttu-id="a7782-180">사용 권한이 성공적으로 주어지면 암호화된 VM에 백업을 사용하도록 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-180">Once permissions are successfully provided, you can proceed with enabling backup for encrypted VMs.</span></span>

## <a name="restore-encrypted-vm"></a><span data-ttu-id="a7782-181">암호화된 VM 복원</span><span class="sxs-lookup"><span data-stu-id="a7782-181">Restore encrypted VM</span></span>
<span data-ttu-id="a7782-182">암호화된 VM을 복원하려면 먼저 [VM 복원 구성 선택](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration)의 **백업된 디스크 복원** 섹션에 제공된 단계에 따라 디스크를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-182">To restore encrypted VM, first Restore Disks using steps mentioned in section **Restore backed up disks** in [Choosing VM restore configuration](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration).</span></span> <span data-ttu-id="a7782-183">그런 후에 다음 옵션 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-183">After that, you can use one of the following options:</span></span>
* <span data-ttu-id="a7782-184">[복원된 디스크에서 VM 만들기](backup-azure-vms-automation.md#create-a-vm-from-restored-disks)에 설명된 PowerShell 단계를 사용하여 복원된 디스크에서 전체 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-184">Use the PowerShell steps mentioned in [Create a VM from restored disks](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) to create full VM from restored disks.</span></span>
* <span data-ttu-id="a7782-185">또는 [디스크 복원의 일부로 생성된 템플릿을 사용](backup-azure-arm-restore-vms.md#use-templates-to-customize-restore-vm)하여 복원된 디스크에서 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-185">OR, [Use template generated as part of Restore Disks](backup-azure-arm-restore-vms.md#use-templates-to-customize-restore-vm) to create VMs from restored disks.</span></span> <span data-ttu-id="a7782-186">템플릿은 2017년 4월 26일 이후에 만들어진 복원 지점에 대해서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-186">Templates can be used only for recovery points created after 26 April 2017.</span></span>

## <a name="troubleshooting-errors"></a><span data-ttu-id="a7782-187">문제 해결 오류</span><span class="sxs-lookup"><span data-stu-id="a7782-187">Troubleshooting errors</span></span>
| <span data-ttu-id="a7782-188">작업</span><span class="sxs-lookup"><span data-stu-id="a7782-188">Operation</span></span> | <span data-ttu-id="a7782-189">오류 세부 정보</span><span class="sxs-lookup"><span data-stu-id="a7782-189">Error details</span></span> | <span data-ttu-id="a7782-190">해결 방법</span><span class="sxs-lookup"><span data-stu-id="a7782-190">Resolution</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a7782-191">백업</span><span class="sxs-lookup"><span data-stu-id="a7782-191">Backup</span></span> |<span data-ttu-id="a7782-192">가상 컴퓨터가 BEK만으로 암호화되었기 때문에 유효성 검사에 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-192">Validation failed as virtual machine is encrypted with BEK alone.</span></span> <span data-ttu-id="a7782-193">BEK와 KEK 모두로 암호화된 가상 컴퓨터에서만 백업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-193">Backups can be enabled only for virtual machines encrypted with both BEK and KEK.</span></span> |<span data-ttu-id="a7782-194">가상 컴퓨터는 BEK와 KEK를 사용하여 암호화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-194">Virtual machine should be encrypted using BEK and KEK.</span></span> <span data-ttu-id="a7782-195">먼저 VM의 암호를 해독하고 BEK와 KEK를 사용하여 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-195">First decrypt the VM and encrypt it using both BEK and KEK.</span></span> <span data-ttu-id="a7782-196">VM이 BEK와 KEK를 사용하여 암호화되면 백업을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-196">Enable backup once VM is encrypted using both BEK and KEK.</span></span> <span data-ttu-id="a7782-197">[VM 암호 해독 및 암호화](../security/azure-security-disk-encryption.md)에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="a7782-197">Learn more on how you can [decrypt and encrypt the VM](../security/azure-security-disk-encryption.md)</span></span>  |
| <span data-ttu-id="a7782-198">복원</span><span class="sxs-lookup"><span data-stu-id="a7782-198">Restore</span></span> |<span data-ttu-id="a7782-199">이 VM과 연결된 키 자격 증명 모음이 없기 때문에 이 암호화된 VM을 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-199">You cannot restore this encrypted VM since key vault associated with this VM does not exist.</span></span> |<span data-ttu-id="a7782-200">키 자격 증명 모음을 만들려면 [Azure Key Vault 시작](../key-vault/key-vault-get-started.md)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-200">Create key vault using [Get Started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span> <span data-ttu-id="a7782-201">키와 비밀이 없는 경우 이를 복원하려면 [Azure Backup으로 키 자격 증명 모음 키 및 비밀 복원](backup-azure-restore-key-secret.md)(영문) 문서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-201">Refer the article [Restore key vault key and secret using Azure Backup](backup-azure-restore-key-secret.md) to restore key and secret if they are not present.</span></span> |
| <span data-ttu-id="a7782-202">복원</span><span class="sxs-lookup"><span data-stu-id="a7782-202">Restore</span></span> |<span data-ttu-id="a7782-203">이 VM과 연결된 키와 비밀이 없기 때문에 이 암호화된 VM을 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-203">You cannot restore this encrypted VM since key and secret associated with this VM do not exist.</span></span> |<span data-ttu-id="a7782-204">키와 비밀이 없는 경우 이를 복원하려면 [Azure Backup으로 키 자격 증명 모음 키 및 비밀 복원](backup-azure-restore-key-secret.md)(영문) 문서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-204">Refer the article [Restore key vault key and secret using Azure Backup](backup-azure-restore-key-secret.md) to restore key and secret if they are not present.</span></span> |
| <span data-ttu-id="a7782-205">복원</span><span class="sxs-lookup"><span data-stu-id="a7782-205">Restore</span></span> |<span data-ttu-id="a7782-206">백업 서비스는 구독의 리소스에 액세스할 수 있는 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-206">Backup Service does not have authorization to access resources in your subscription.</span></span> |<span data-ttu-id="a7782-207">위에서 설명된 것처럼 먼저 [VM 복원 구성 선택](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration)의 **백업된 디스크 복원** 섹션에 제공된 단계에 따라 디스크를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-207">As mentioned above, Restore Disks first, using steps mentioned in section **Restore backed up disks** in [Choosing VM restore configuration](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration).</span></span> <span data-ttu-id="a7782-208">그런 후에 PowerShell을 사용하여 [복원된 디스크에서 VM을 만듭니다](backup-azure-vms-automation.md#create-a-vm-from-restored-disks).</span><span class="sxs-lookup"><span data-stu-id="a7782-208">After that, user PowerShell to [Create a VM from restored disks](backup-azure-vms-automation.md#create-a-vm-from-restored-disks).</span></span> |
|<span data-ttu-id="a7782-209">백업</span><span class="sxs-lookup"><span data-stu-id="a7782-209">Backup</span></span> | <span data-ttu-id="a7782-210">Azure Backup 서비스에는 암호화된 가상 컴퓨터의 백업을 위한 Key Vault에 대해 충분한 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-210">Azure Backup Service does not have sufficient permissions to Key Vault for Backup of Encrypted Virtual Machines</span></span> | <span data-ttu-id="a7782-211">이 경우 가상 시스템을 BitLocker 암호화 키와 키 암호화 키를 모두 사용하여 암호화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-211">Virtual machine should be encrypted using both BitLocker Encryption Key and Key Encryption Key.</span></span> <span data-ttu-id="a7782-212">그런 후에 백업을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-212">After that, backup should be enabled.</span></span>  <span data-ttu-id="a7782-213">백업 서비스는 [위의 섹션에서 언급한 단계](#provide-permissions-to-azure-backup) 또는 [AzureRM.RecoveryServices.Backup cmdlet을 사용하여 가상 컴퓨터 백업](backup-azure-vms-automation.md#back-up-azure-vms)에서 PowerShell 설명서의 **보호 사용** 섹션에서 언급한 PowerShell 단계를 사용하여 이러한 사용 권한을 제공받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7782-213">Backup service should be provided these permissions using [steps mentioned in the section above](#provide-permissions-to-azure-backup) or by using PowerShell steps mentioned in the **Enable protection** section of the PowerShell documentation at [Use AzureRM.RecoveryServices.Backup cmdlets to back up virtual machines](backup-azure-vms-automation.md#back-up-azure-vms).</span></span> |  
