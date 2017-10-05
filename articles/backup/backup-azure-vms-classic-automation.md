---
title: "PowerShell을 사용하여 Azure VM의 배포 및 백업 관리 | Microsoft Docs"
description: "PowerShell을 사용하여 Azure 백업을 배포 및 관리하는 방법을 알아봅니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 2e24b1d9-4375-4049-a28d-e3bc01152f32
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;trinadhk;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5f0f06adb8177ce2d17aa0b40666470279c04e22
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-azurermbackup-cmdlets-to-back-up-virtual-machines"></a><span data-ttu-id="5a8e4-103">AzureRM.Backup cmdlet을 사용하여 가상 컴퓨터 백업</span><span class="sxs-lookup"><span data-stu-id="5a8e4-103">Use AzureRM.Backup cmdlets to back up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5a8e4-104">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="5a8e4-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="5a8e4-105">클래식</span><span class="sxs-lookup"><span data-stu-id="5a8e4-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="5a8e4-106">이 문서에서는 Azure VM의 백업 및 복구를 위한 Azure PowerShell을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-106">This article shows you how to use Azure PowerShell for backup and recovery of Azure VMs.</span></span> <span data-ttu-id="5a8e4-107">Azure는 리소스를 만들고 작업하기 위한 두 가지 배포 모델로 리소스 관리자와 클래식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-107">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="5a8e4-108">이 문서에서는 클래식 배포 모델을 사용하여 백업 자격 증명 모음으로 데이터 백업에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-108">This article covers using the Classic deployment model to back up data to a Backup vault.</span></span> <span data-ttu-id="5a8e4-109">구독에서 백업 자격 증명 모음을 만들지 않은 경우 이 문서의 리소스 관리자 버전, [AzureRM.RecoveryServices.Backup cmdlet을 사용하여 가상 컴퓨터 백업](backup-azure-vms-automation.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-109">If you have not created a Backup vault in your subscription, see the Resource Manager version of this article, [Use AzureRM.RecoveryServices.Backup cmdlets to back up virtual machines](backup-azure-vms-automation.md).</span></span> <span data-ttu-id="5a8e4-110">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a8e4-111">이제 Backup 자격 증명 모음을 Recovery Services 자격 증명 모음으로 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-111">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="5a8e4-112">자세한 내용은 [Recovery Services 자격 증명 모음으로 Backup 자격 증명 모음 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-112">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="5a8e4-113">Backup 자격 증명 모음을 Recovery Services 자격 증명 모음으로 업그레이드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-113">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="5a8e4-114">2017년 10월 15일 이후부터는 PowerShell을 사용하여 Backup 자격 증명 모음을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-114">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="5a8e4-115">**2017년 11월 1일까지**:</span><span class="sxs-lookup"><span data-stu-id="5a8e4-115">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="5a8e4-116">남아 있는 모든 Backup 자격 증명 모음이 Recovery Services 자격 증명 모음으로 자동 업그레이드됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-116">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="5a8e4-117">클래식 포털에서는 백업 데이터에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-117">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="5a8e4-118">대신 Azure Portal을 사용하여 Recovery Services 자격 증명 모음에서 백업 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-118">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="concepts"></a><span data-ttu-id="5a8e4-119">개념</span><span class="sxs-lookup"><span data-stu-id="5a8e4-119">Concepts</span></span>
<span data-ttu-id="5a8e4-120">이 문서에서는 가상 컴퓨터를 백업하는 데 사용되는 PowerShell cmdlet 관련 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-120">This article provides information specific to the PowerShell cmdlets used to back up virtual machines.</span></span> <span data-ttu-id="5a8e4-121">Azure VM을 보호하는 방법에 대한 소개 정보는 [Azure에서 VM 백업 인프라 계획](backup-azure-vms-introduction.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-121">For introductory information about protecting Azure VMs, please see [Plan your VM backup infrastructure in Azure](backup-azure-vms-introduction.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5a8e4-122">시작하기 전에 먼저 Azure 백업 작업에 필요한 [필수 조건](backup-azure-vms-prepare.md) 및 현재 VM 백업 솔루션의 [제한](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-122">Before you start, read the [prerequisites](backup-azure-vms-prepare.md) required to work with Azure Backup, and the [limitations](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) of the current VM backup solution.</span></span>
>
>

<span data-ttu-id="5a8e4-123">PowerShell을 효과적으로 사용하려면 개체의 계층 구조와 시작하는 위치를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-123">To use PowerShell effectively, take a moment to understand the hierarchy of objects and from where to start.</span></span>

![개체 계층 구조](./media/backup-azure-vms-classic-automation/object-hierarchy.png)

<span data-ttu-id="5a8e4-125">두 개의 가장 중요한 흐름은 VM에 대한 보호를 사용하는 것과 복구 지점으로부터 데이터를 복원하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-125">The two most important flows are enabling protection for a VM, and restoring data from a recovery point.</span></span> <span data-ttu-id="5a8e4-126">이 문서는 이들 두 시나리오를 사용하기 위해 PowerShell cmdlet으로 작업 시 적용하는 데 중점을 두고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-126">The focus of this article is to help you become adept at working with the PowerShell cmdlets to enable these two scenarios.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="5a8e4-127">설정 및 등록</span><span class="sxs-lookup"><span data-stu-id="5a8e4-127">Setup and Registration</span></span>
<span data-ttu-id="5a8e4-128">시작하려면</span><span class="sxs-lookup"><span data-stu-id="5a8e4-128">To begin:</span></span>

1. <span data-ttu-id="5a8e4-129">[최신 PowerShell을 다운로드](https://github.com/Azure/azure-powershell/releases) 합니다(필요한 최소 버전: 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="5a8e4-129">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="5a8e4-130">다음 명령을 입력하여 사용할 수 있는 Azure 백업 PowerShell cmdlet을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-130">Find the Azure Backup PowerShell cmdlets available by typing the following command:</span></span>

```
PS C:\> Get-Command *azurermbackup*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Backup-AzureRmBackupItem                           1.0.1      AzureRM.Backup
Cmdlet          Disable-AzureRmBackupProtection                    1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupContainerReregistration        1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupProtection                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupContainer                         1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupItem                              1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJob                               1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJobDetails                        1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupRecoveryPoint                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVaultCredentials                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupRetentionPolicyObject             1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Register-AzureRmBackupContainer                    1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupProtectionPolicy               1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupVault                          1.0.1      AzureRM.Backup
Cmdlet          Restore-AzureRmBackupItem                          1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Stop-AzureRmBackupJob                              1.0.1      AzureRM.Backup
Cmdlet          Unregister-AzureRmBackupContainer                  1.0.1      AzureRM.Backup
Cmdlet          Wait-AzureRmBackupJob                              1.0.1      AzureRM.Backup
```

<span data-ttu-id="5a8e4-131">PowerShell로 다음과 같은 설정 및 등록 작업을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-131">The following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="5a8e4-132">백업 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="5a8e4-132">Create a backup vault</span></span>
* <span data-ttu-id="5a8e4-133">Azure 백업 서비스에 VM 등록</span><span class="sxs-lookup"><span data-stu-id="5a8e4-133">Registering the VMs with the Azure Backup service</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="5a8e4-134">백업 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="5a8e4-134">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="5a8e4-135">처음으로 Azure 백업을 사용하는 고객의 경우, 구독과 함께 사용할 Azure 백업 공급자를 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-135">For customers using Azure Backup for the first time, you need to register the Azure Backup provider to be used with your subscription.</span></span> <span data-ttu-id="5a8e4-136">이는 다음 명령을 실행하여 수행할 수 있습니다. Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="5a8e4-136">This can be done by running the following command: Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="5a8e4-137">**New-AzureRmBackupVault** cmdlet을 사용하여 새 백업 자격 증명 모음을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-137">You can create a new backup vault using the **New-AzureRmBackupVault** cmdlet.</span></span> <span data-ttu-id="5a8e4-138">백업 저장소는 ARM 리소스이므로 리소스 그룹 내에 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-138">The backup vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="5a8e4-139">승격된 Azure PowerShell 콘솔에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-139">In an elevated Azure PowerShell console, run the following commands:</span></span>

```
PS C:\> New-AzureRmResourceGroup –Name “test-rg” –Location “West US”
PS C:\> $backupvault = New-AzureRmBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="5a8e4-140">**Get-AzureRmBackupVault** cmdlet을 사용하여 지정된 구독의 모든 백업 자격 증명 모음 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-140">You can get a list of all the backup vaults in a given subscription using the **Get-AzureRmBackupVault** cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="5a8e4-141">백업 저장소 개체를 변수에 저장하면 편리합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-141">It is convenient to store the backup vault object into a variable.</span></span> <span data-ttu-id="5a8e4-142">저장소 개체는 많은 Azure 백업 cmdlet에 대한 입력으로서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-142">The vault object is needed as an input for many Azure Backup cmdlets.</span></span>
>
>

### <a name="registering-the-vms"></a><span data-ttu-id="5a8e4-143">VM 등록</span><span class="sxs-lookup"><span data-stu-id="5a8e4-143">Registering the VMs</span></span>
<span data-ttu-id="5a8e4-144">Azure 백업으로 백업을 구성하는 첫 번째 단계는 Azure 백업 저장소에 사용자 컴퓨터 또는 VM을 등록하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-144">The first step towards configuring backup with Azure Backup is to register your machine or VM with an Azure Backup vault.</span></span> <span data-ttu-id="5a8e4-145">**Register-AzureRmBackupContainer** cmdlet은 Azure IaaS 가상 컴퓨터의 입력 정보를 받아 지정된 자격 증명 모음에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-145">The **Register-AzureRmBackupContainer** cmdlet takes the input information of an Azure IaaS virtual machine and registers it with the specified vault.</span></span> <span data-ttu-id="5a8e4-146">등록 작업은 Azure 가상 컴퓨터를 백업 저장소와 연결하고 백업 수명 주기를 통해 VM을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-146">The register operation associates the Azure virtual machine with the backup vault and tracks the VM through the backup lifecycle.</span></span>

<span data-ttu-id="5a8e4-147">Azure 백업 서비스와 VM을 등록하면 최상위 컨테이너 개체가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-147">Registering your VM with the Azure Backup service creates a top-level container object.</span></span> <span data-ttu-id="5a8e4-148">컨테이너에는 일반적으로 백업할 수 있는 여러 항목이 있지만, VM의 경우 해당 컨테이너에 대해 단 하나의 백업 항목만 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-148">A container typically contains multiple items that can be backed up, but in the case of VMs there will be only one backup item for the container.</span></span>

```
PS C:\> $registerjob = Register-AzureRmBackupContainer -Vault $backupvault -Name "testvm" -ServiceName "testvm"
```

## <a name="backup-azure-vms"></a><span data-ttu-id="5a8e4-149">Azure VM 백업</span><span class="sxs-lookup"><span data-stu-id="5a8e4-149">Backup Azure VMs</span></span>
### <a name="create-a-protection-policy"></a><span data-ttu-id="5a8e4-150">보호 정책 만들기 </span><span class="sxs-lookup"><span data-stu-id="5a8e4-150">Create a protection policy</span></span>
<span data-ttu-id="5a8e4-151">VM의 백업을 시작하기 위한 새 보호 정책을 만들지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-151">It is not mandatory to create a new protection policy to start backup of your VMs.</span></span> <span data-ttu-id="5a8e4-152">저장소는 빠르게 보호하는 데 사용할 수 있는 ‘기본 정책’이 적용된 다음, 나중에 올바른 세부 정보로 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-152">The vault comes with a 'Default Policy' that can be used to quickly enable protection, and then edited later with the right details.</span></span> <span data-ttu-id="5a8e4-153">다음과 같이 **Get-AzureRmBackupProtectionPolicy** cmdlet을 사용하여 자격 증명 모음에서 사용 가능한 정책 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-153">You can get a list of the policies available in the vault by using the **Get-AzureRmBackupProtectionPolicy** cmdlet:</span></span>

```
PS C:\> Get-AzureRmBackupProtectionPolicy -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DefaultPolicy             AzureVM            Daily              26-Aug-15 12:30:00 AM
```

> [!NOTE]
> <span data-ttu-id="5a8e4-154">PowerShell에서 BackupTime 필드의 표준 시간대는 UTC입니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-154">The timezone of the BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="5a8e4-155">그러나 백업 시간이 Azure 포털에 표시될 때 표준 시간대는 UTC 오프셋과 함께 로컬 시스템에 맞춰집니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-155">However, when the backup time is shown in the Azure portal, the timezone is aligned to your local system along with the UTC offset.</span></span>
>
>

<span data-ttu-id="5a8e4-156">백업 정책은 하나 이상의 보존 정책과 연관됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-156">A backup policy is associated with at least one retention policy.</span></span> <span data-ttu-id="5a8e4-157">보존 정책은 Azure 백업의 복구 지점을 얼마나 오래 유지할지를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-157">The retention policy defines how long a recovery point is kept with Azure Backup.</span></span> <span data-ttu-id="5a8e4-158">**New-AzureRmBackupRetentionPolicy** cmdlet은 보존 정책 정보를 포함하는 PowerShell 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-158">The **New-AzureRmBackupRetentionPolicy** cmdlet creates PowerShell objects that hold retention policy information.</span></span> <span data-ttu-id="5a8e4-159">이러한 보존 정책 개체는 *New-AzureRmBackupProtectionPolicy* cmdlet에 대한 입력으로 사용되거나 *Enable-AzureRmBackupProtection* cmdlet과 함께 직접 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-159">These retention policy objects are used as inputs to the *New-AzureRmBackupProtectionPolicy* cmdlet, or directly with the *Enable-AzureRmBackupProtection* cmdlet.</span></span>

<span data-ttu-id="5a8e4-160">백업 정책은 항목의 백업 수행 시점과 빈도를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-160">A backup policy defines when and how often the backup of an item is done.</span></span> <span data-ttu-id="5a8e4-161">**New-AzureRmBackupProtectionPolicy** cmdlet은 백업 정책 정보를 포함하는 PowerShell 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-161">The **New-AzureRmBackupProtectionPolicy** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="5a8e4-162">백업 정책은 *Enable-AzureRmBackupProtection* cmdlet에 대한 입력으로서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-162">The backup policy is used as an input to the *Enable-AzureRmBackupProtection* cmdlet.</span></span>

```
PS C:\> $Daily = New-AzureRmBackupRetentionPolicyObject -DailyRetention -Retention 30
PS C:\> $newpolicy = New-AzureRmBackupProtectionPolicy -Name DailyBackup01 -Type AzureVM -Daily -BackupTime ([datetime]"3:30 PM") -RetentionPolicy $Daily -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DailyBackup01             AzureVM            Daily              01-Sep-15 3:30:00 PM
```

### <a name="enable-protection"></a><span data-ttu-id="5a8e4-163">보호 사용</span><span class="sxs-lookup"><span data-stu-id="5a8e4-163">Enable protection</span></span>
<span data-ttu-id="5a8e4-164">보호를 사용하면 동일한 저장소에 속한 두 개체, 즉 항목과 정책을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-164">Enabling protection involves two objects - the Item and the Policy, and both need to belong to the same vault.</span></span> <span data-ttu-id="5a8e4-165">정책이 항목과 연관되면, 백업 워크플로는 정해진 일정에 따라 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-165">Once the policy has been associated with the item, the backup workflow will kick in at the defined schedule.</span></span>

```
PS C:\> Get-AzureRmBackupContainer -Type AzureVM -Status Registered -Vault $backupvault | Get-AzureRmBackupItem | Enable-AzureRmBackupProtection -Policy $newpolicy
```

### <a name="initial-backup"></a><span data-ttu-id="5a8e4-166">초기 백업</span><span class="sxs-lookup"><span data-stu-id="5a8e4-166">Initial backup</span></span>
<span data-ttu-id="5a8e4-167">백업 일정은 항목에 대한 전체 초기 복사와 후속 백업에 대한 증분 복사 작업을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-167">The backup schedule will take care of doing the full initial copy for the item and the incremental copy for the subsequent backups.</span></span> <span data-ttu-id="5a8e4-168">그러나 초기 백업을 강제로 특정 시간에 수행하거나 즉시 수행하려는 경우 다음과 같이 **Backup-AzureRmBackupItem** cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-168">However, if you want to force the initial backup to happen at a certain time or even immediately then use the **Backup-AzureRmBackupItem** cmdlet:</span></span>

```
PS C:\> $container = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -Name "testvm"
PS C:\> $backupjob = Get-AzureRmBackupItem -Container $container | Backup-AzureRmBackupItem
PS C:\> $backupjob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

> [!NOTE]
> <span data-ttu-id="5a8e4-169">PowerShell에서 표시되는 StartTime 및 EndTime 필드의 표준 시간대는 UTC입니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-169">The timezone of the StartTime and EndTime fields shown in PowerShell is UTC.</span></span> <span data-ttu-id="5a8e4-170">그러나 유사한 정보가 Azure 포털에 표시될 때 표준 시간대는 로컬 시스템 클록에 맞춰집니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-170">However, when the similar information is shown in the Azure portal, the timezone is aligned to your local system clock.</span></span>
>
>

### <a name="monitoring-a-backup-job"></a><span data-ttu-id="5a8e4-171">백업 작업 모니터링</span><span class="sxs-lookup"><span data-stu-id="5a8e4-171">Monitoring a backup job</span></span>
<span data-ttu-id="5a8e4-172">Azure 백업의 장기 실행 작업 대부분은 하나의 작업으로 모델링됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-172">Most long-running operations in Azure Backup are modelled as a job.</span></span> <span data-ttu-id="5a8e4-173">이는 Azure 포털이 항상 열려 있지 않아도 진행률을 쉽게 추적할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-173">This makes it easy to track progress without having to keep the Azure portal open at all times.</span></span>

<span data-ttu-id="5a8e4-174">진행 중인 작업의 최신 상태를 가져오려면 **Get-AzureRmBackupJob** cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-174">To get the latest status of an in-progress job, use the **Get-AzureRmBackupJob** cmdlet.</span></span>

```
PS C:\> $joblist = Get-AzureRmBackupJob -Vault $backupvault -Status InProgress
PS C:\> $joblist[0]

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

<span data-ttu-id="5a8e4-175">이러한 작업을 완료하기 위해 폴링하는 대신(불필요한 추가 코드) **Wait-AzureRmBackupJob** cmdlet을 사용하는 것이 더 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-175">Instead of polling these jobs for completion - which is unnecessary, additional code - it is simpler to use the **Wait-AzureRmBackupJob** cmdlet.</span></span> <span data-ttu-id="5a8e4-176">스크립트를 사용하면 작업이 완료되거나 지정된 시간 제한 값에 도달할 때까지 cmdlet이 실행을 일시 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-176">When used in a script, the cmdlet will pause the execution until either the job completes or the specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmBackupJob -Job $joblist[0] -Timeout 43200
```


## <a name="restore-an-azure-vm"></a><span data-ttu-id="5a8e4-177">Azure VM 복원</span><span class="sxs-lookup"><span data-stu-id="5a8e4-177">Restore an Azure VM</span></span>
<span data-ttu-id="5a8e4-178">백업 데이터를 복원하려면 백업 항목 및 지정 시간 데이터가 포함된 복구 지점을 식별해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-178">In order to restore backup data, you need to identify the backed-up Item and the Recovery Point that holds the point-in-time data.</span></span> <span data-ttu-id="5a8e4-179">이 정보는 저장소에서 고객의 계정으로 데이터의 복원을 시작하도록 Restore-AzureRmBackupItem cmdlet에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-179">This information is supplied to the Restore-AzureRmBackupItem cmdlet to initiate a restore of data from the vault to the customer's account.</span></span>

### <a name="select-the-vm"></a><span data-ttu-id="5a8e4-180">VM 선택</span><span class="sxs-lookup"><span data-stu-id="5a8e4-180">Select the VM</span></span>
<span data-ttu-id="5a8e4-181">올바른 백업 항목을 식별하는 PowerShell 개체를 가져오려면 해당 저장소에 있는 컨테이너에서 시작하고 개체 계층 구조를 따라 내려가는 방식으로 작업해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-181">To get the PowerShell object that identifies the right backup Item, you need to start from the Container in the vault, and work your way down object hierarchy.</span></span> <span data-ttu-id="5a8e4-182">VM을 나타내는 컨테이너를 선택하려면 **Get-AzureRmBackupContainer** cmdlet을 사용하고 **Get-AzureRmBackupItem** cmdlet으로 파이프합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-182">To select the container that represents the VM, use the **Get-AzureRmBackupContainer** cmdlet and pipe that to the **Get-AzureRmBackupItem** cmdlet.</span></span>

```
PS C:\> $backupitem = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -name "testvm" | Get-AzureRmBackupItem
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="5a8e4-183">복구 지점 선택</span><span class="sxs-lookup"><span data-stu-id="5a8e4-183">Choose a recovery point</span></span>
<span data-ttu-id="5a8e4-184">이제 **Get-AzureRmBackupRecoveryPoint** cmdlet을 사용하여 백업 항목에 대한 모든 복구 지점을 나열하고 복원할 복구 지점을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-184">You can now list all the recovery points for the backup item using the **Get-AzureRmBackupRecoveryPoint** cmdlet, and choose the recovery point to restore.</span></span> <span data-ttu-id="5a8e4-185">일반적으로 사용자는 목록에서 가장 최근의 *AppConsistent* 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-185">Typically users pick the most recent *AppConsistent* point in the list.</span></span>

```
PS C:\> $rp =  Get-AzureRmBackupRecoveryPoint -Item $backupitem
PS C:\> $rp

RecoveryPointId    RecoveryPointType  RecoveryPointTime      ContainerName
---------------    -----------------  -----------------      -------------
15273496567119     AppConsistent      01-Sep-15 12:27:38 PM  iaasvmcontainer;testvm;testv...
```

<span data-ttu-id="5a8e4-186">```$rp``` 변수는 선택한 백업 항목에 대한 복구 지점의 배열로, 시간의 역순으로 정렬되며 최신 복구 지점은 인덱스 0에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-186">The variable ```$rp``` is an array of recovery points for the selected backup item, sorted in reverse order of time - the latest recovery point is at index 0.</span></span> <span data-ttu-id="5a8e4-187">복구 지점을 선택하려면 표준 PowerShell 배열 인덱싱을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-187">Use standard PowerShell array indexing to pick the recovery point.</span></span> <span data-ttu-id="5a8e4-188">예를 들어 ```$rp[0]``` 은 최신 복구 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-188">For example: ```$rp[0]``` will select the latest recovery point.</span></span>

### <a name="restoring-disks"></a><span data-ttu-id="5a8e4-189">디스크 복원</span><span class="sxs-lookup"><span data-stu-id="5a8e4-189">Restoring disks</span></span>
<span data-ttu-id="5a8e4-190">Azure 포털 및 Azure PowerShell을 통해 수행된 복원 작업 간의 주요 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-190">There is a key difference between the restore operations done through the Azure portal and through Azure PowerShell.</span></span> <span data-ttu-id="5a8e4-191">PowerShell을 사용하면 복구 지점에서 디스크 및 구성 정보를 복원할 때 복원 작업이 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-191">With PowerShell, the restore operation stops at restoring the disks and config information from the recovery point.</span></span> <span data-ttu-id="5a8e4-192">가상 컴퓨터를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-192">It does not create a virtual machine.</span></span>

> [!WARNING]
> <span data-ttu-id="5a8e4-193">Restore-AzureRmBackupItem은 VM을 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-193">The Restore-AzureRmBackupItem does not create a VM.</span></span> <span data-ttu-id="5a8e4-194">지정된 저장소 계정에 디스크 복원만 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-194">It only restores the disks to the specified storage account.</span></span> <span data-ttu-id="5a8e4-195">이는 Azure 포털에서 보게 될 동작과는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-195">This is not the same behavior you will experience in the Azure portal.</span></span>
>
>

```
PS C:\> $restorejob = Restore-AzureRmBackupItem -StorageAccountName "DestAccount" -RecoveryPoint $rp[0]
PS C:\> $restorejob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Restore         InProgress      01-Sep-15 1:14:01 PM   01-Jan-01 12:00:00 AM
```

<span data-ttu-id="5a8e4-196">복원 작업이 완료되면 **Get-AzureRmBackupJobDetails** cmdlet을 사용하여 복원 작업의 세부 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-196">You can get the details of the restore operation using the **Get-AzureRmBackupJobDetails** cmdlet once the Restore job has completed.</span></span> <span data-ttu-id="5a8e4-197">*ErrorDetails* 속성에는 VM을 다시 빌드하는 데 필요한 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-197">The *ErrorDetails* property will have the information needed to rebuild the VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmBackupJobDetails -Job $restorejob
```

### <a name="build-the-vm"></a><span data-ttu-id="5a8e4-198">VM 빌드</span><span class="sxs-lookup"><span data-stu-id="5a8e4-198">Build the VM</span></span>
<span data-ttu-id="5a8e4-199">복원된 디스크 외부의 VM 빌드는 이전의 Azure 서비스 관리 PowerShell cmdlet, 새 Azure Resource Manager 템플릿 또는 Azure 포털을 사용해서도 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-199">Building the VM out of the restored disks can be done using the older Azure Service Management PowerShell cmdlets, the new Azure Resource Manager templates, or even using the Azure portal.</span></span> <span data-ttu-id="5a8e4-200">간단한 예제에서는 Azure 서비스 관리 cmdlet을 사용하여 도달하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-200">In a quick example, we will show how to get there using the Azure Service Management cmdlets.</span></span>

```
$properties  = $details.Properties

$storageAccountName = $properties["Target Storage Account Name"]
$containerName = $properties["Config Blob Container Name"]
$blobName = $properties["Config Blob Name"]

$keys = Get-AzureStorageKey -StorageAccountName $storageAccountName
$storageAccountKey = $keys.Primary
$storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey


$destination_path = "C:\Users\admin\Desktop\vmconfig.xml"
Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path -Context $storageContext


$obj = [xml](((Get-Content -Path $destination_path -Encoding UniCode)).TrimEnd([char]0x00))
$pvr = $obj.PersistentVMRole
$os = $pvr.OSVirtualHardDisk
$dds = $pvr.DataVirtualHardDisks
$osDisk = Add-AzureDisk -MediaLocation $os.MediaLink -OS $os.OS -DiskName "panbhaosdisk"
$vm = New-AzureVMConfig -Name $pvr.RoleName -InstanceSize $pvr.RoleSize -DiskName $osDisk.DiskName

if (!($dds -eq $null))
{
    foreach($d in $dds.DataVirtualHardDisk)
    {
        $lun = 0
        if(!($d.Lun -eq $null))
        {
            $lun = $d.Lun
        }
        $name = "panbhadataDisk" + $lun
        Add-AzureDisk -DiskName $name -MediaLocation $d.MediaLink
        $vm | Add-AzureDataDisk -Import -DiskName $name -LUN $lun
    }
}

New-AzureVM -ServiceName "panbhasample" -Location "SouthEast Asia" -VM $vm
```

<span data-ttu-id="5a8e4-201">복원된 디스크로부터 VM을 빌드하는 방법에 대한 자세한 내용은 다음 cmdlet을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-201">For more information on how to build a VM from the restored disks, read about the following cmdlets:</span></span>

* [<span data-ttu-id="5a8e4-202">Add-AzureDisk</span><span class="sxs-lookup"><span data-stu-id="5a8e4-202">Add-AzureDisk</span></span>](https://msdn.microsoft.com/library/azure/dn495252.aspx)
* [<span data-ttu-id="5a8e4-203">New-AzureVMConfig</span><span class="sxs-lookup"><span data-stu-id="5a8e4-203">New-AzureVMConfig</span></span>](https://msdn.microsoft.com/library/azure/dn495159.aspx)
* [<span data-ttu-id="5a8e4-204">New-AzureVM</span><span class="sxs-lookup"><span data-stu-id="5a8e4-204">New-AzureVM</span></span>](https://msdn.microsoft.com/library/azure/dn495254.aspx)

## <a name="code-samples"></a><span data-ttu-id="5a8e4-205">코드 샘플</span><span class="sxs-lookup"><span data-stu-id="5a8e4-205">Code samples</span></span>
### <a name="1-get-the-completion-status-of-job-sub-tasks"></a><span data-ttu-id="5a8e4-206">1. 작업 하위 작업의 완료 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="5a8e4-206">1. Get the completion status of job sub-tasks</span></span>
<span data-ttu-id="5a8e4-207">개별 하위 작업의 완료 상태를 추적하려면 **Get-AzureRmBackupJobDetails** cmdlet을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-207">To track the completion status of individual sub-tasks, you can use the **Get-AzureRmBackupJobDetails** cmdlet:</span></span>

```
PS C:\> $details = Get-AzureRmBackupJobDetails -JobId $backupjob.InstanceId -Vault $backupvault
PS C:\> $details.SubTasks

Name                                                        Status
----                                                        ------
Take Snapshot                                               Completed
Transfer data to Backup vault                               InProgress
```

### <a name="2-create-a-dailyweekly-report-of-backup-jobs"></a><span data-ttu-id="5a8e4-208">2. 백업 작업의 일별/주별 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="5a8e4-208">2. Create a daily/weekly report of backup jobs</span></span>
<span data-ttu-id="5a8e4-209">일반적으로 관리자는 지난 24시간 동안 실행된 백업 작업과 해당 작업의 상태를 파악하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-209">Administrators typically want to know what backup jobs ran in the last 24 hours, the status of those backup jobs.</span></span> <span data-ttu-id="5a8e4-210">또한 전송된 데이터의 양을 통해 관리자는 월별 데이터 사용량을 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-210">Additionally, the amount of data transferred gives administrators a way to estimate their monthly data usage.</span></span> <span data-ttu-id="5a8e4-211">아래의 스크립트는 Azure 백업 서비스에서 원시 데이터를 가져오고 PowerShell 콘솔에 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-211">The script below pulls the raw data from the Azure Backup service and displays the information in the PowerShell console.</span></span>

```
param(  [Parameter(Mandatory=$True,Position=1)]
        [string]$backupvaultname,

        [Parameter(Mandatory=$False,Position=2)]
        [int]$numberofdays = 7)


#Initialize variables
$DAILYBACKUPSTATS = @()
$backupvault = Get-AzureRmBackupVault -Name $backupvaultname
$enddate = ([datetime]::Today).AddDays(1)
$startdate = ([datetime]::Today)

for( $i = 1; $i -le $numberofdays; $i++ )
{
    # We query one day at a time because pulling 7 days of data might be too much
    $dailyjoblist = Get-AzureRmBackupJob -Vault $backupvault -From $startdate -To $enddate -Type AzureVM -Operation Backup
    Write-Progress -Activity "Getting job information for the last $numberofdays days" -Status "Day -$i" -PercentComplete ([int]([decimal]$i*100/$numberofdays))

    foreach( $job in $dailyjoblist )
    {
        #Extract the information for the reports
        $newstatsobj = New-Object System.Object
        $newstatsobj | Add-Member -Type NoteProperty -Name Date -Value $startdate
        $newstatsobj | Add-Member -Type NoteProperty -Name VMName -Value $job.WorkloadName
        $newstatsobj | Add-Member -Type NoteProperty -Name Duration -Value $job.Duration
        $newstatsobj | Add-Member -Type NoteProperty -Name Status -Value $job.Status

        $details = Get-AzureRmBackupJobDetails -Job $job
        $newstatsobj | Add-Member -Type NoteProperty -Name BackupSize -Value $details.Properties["Backup Size"]
        $DAILYBACKUPSTATS += $newstatsobj
    }

    $enddate = $enddate.AddDays(-1)
    $startdate = $startdate.AddDays(-1)
}

$DAILYBACKUPSTATS | Out-GridView
```

<span data-ttu-id="5a8e4-212">이 보고서 출력에 차트 기능을 추가하려는 경우 TechNet 블로그 게시물에서 [PowerShell을 사용한 차트 작성](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span><span class="sxs-lookup"><span data-stu-id="5a8e4-212">If you want to add charting capabilities to this report output, learn from the TechNet blog post [Charting with PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a8e4-213">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5a8e4-213">Next steps</span></span>
<span data-ttu-id="5a8e4-214">PowerShell을 사용하여 Azure 리소스와 연결하려는 경우 Windows Server를 보호하기 위한 PowerShell 문서, [Windows Server에 대한 백업 배포 및 관리](backup-client-automation-classic.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-214">If you prefer using PowerShell to engage with your Azure resources, check out the PowerShell article for protecting Windows Server, [Deploy and Manage Backup for Windows Server](backup-client-automation-classic.md).</span></span> <span data-ttu-id="5a8e4-215">DPM 백업을 관리하기 위한 PowerShell 문서, [DPM에 대한 백업 배포 및 관리](backup-dpm-automation-classic.md)도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-215">There is also a PowerShell article for managing DPM backups, [Deploy and Manage Backup for DPM](backup-dpm-automation-classic.md).</span></span> <span data-ttu-id="5a8e4-216">이러한 문서 모두에 Resource Manager 배포용 버전뿐 아니라 클래식 배포용 버전도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a8e4-216">Both of these articles have a version for Resource Manager deployments as well as Classic deployments.</span></span>
