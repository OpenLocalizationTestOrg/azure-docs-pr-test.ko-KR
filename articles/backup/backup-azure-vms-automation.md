---
title: "PowerShell을 사용하여 Resource Manager 배포 VM에 대한 백업 배포 및 관리 | Microsoft Docs"
description: "PowerShell을 사용하여 Azure에서 Resource Manager 배포 VM에 대한 백업 배포 및 관리"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 68606e4f-536d-4eac-9f80-8a198ea94d52
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/28/2017
ms.author: markgal;trinadhk
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 861346a50df6641abb9e454644228146e14b4078
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azurermrecoveryservicesbackup-cmdlets-to-back-up-virtual-machines"></a><span data-ttu-id="d2570-103">AzureRM.RecoveryServices.Backup cmdlet을 사용하여 가상 컴퓨터 백업</span><span class="sxs-lookup"><span data-stu-id="d2570-103">Use AzureRM.RecoveryServices.Backup cmdlets to back up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d2570-104">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="d2570-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="d2570-105">클래식</span><span class="sxs-lookup"><span data-stu-id="d2570-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="d2570-106">이 문서는 Azure PowerShell cmdlet을 사용하여 복구 서비스 자격 증명 모음으로부터 Azure VM(가상 컴퓨터)을 복원하고 백업하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-106">This article shows you how to use Azure PowerShell cmdlets to back up and recover an Azure virtual machine (VM) from a Recovery Services vault.</span></span> <span data-ttu-id="d2570-107">복구 서비스 자격 증명 모음은 Azure Resource Manager 리소스이며 Azure 백업 및 Azure Site Recovery 서비스에서 데이터와 자산을 보호하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-107">A Recovery Services vault is an Azure Resource Manager resource and is used to protect data and assets in both Azure Backup and Azure Site Recovery services.</span></span> <span data-ttu-id="d2570-108">Recovery Services 자격 증명 모음을 사용하여 Azure Resource Manager 배포 VM은 물론, Azure 서비스 관리자 배포 VM도 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-108">You can use a Recovery Services vault to protect Azure Service Manager-deployed VMs, and Azure Resource Manager-deployed VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="d2570-109">Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델인 [리소스 관리자와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-109">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d2570-110">이 문서는 리소스 관리자 모델을 사용하여 생성된 VM 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-110">This article is for use with VMs created using the Resource Manager model.</span></span>
>
>

<span data-ttu-id="d2570-111">이 문서는 PowerShell을 사용하여 VM을 보호하고, 복구 지점으로부터 데이터를 복원하는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-111">This article walks you through using PowerShell to protect a VM, and restore data from a recovery point.</span></span>

## <a name="concepts"></a><span data-ttu-id="d2570-112">개념</span><span class="sxs-lookup"><span data-stu-id="d2570-112">Concepts</span></span>
<span data-ttu-id="d2570-113">Azure Backup Service를 잘 모르는 경우, [Azure 백업이란?](backup-introduction-to-azure-backup.md)에서 서비스에 대한 개요를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="d2570-113">If you are not familiar with the Azure Backup service, for an overview of the service, check out [What is Azure Backup?](backup-introduction-to-azure-backup.md)</span></span> <span data-ttu-id="d2570-114">시작하기 전에 먼저 Azure 백업 작업에 필요한 필수 조건 및 현재 VM 솔루션의 제한에 관한 기본 사항을 다루었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-114">Before you start, ensure that you cover the essentials about the prerequisites needed to work with Azure Backup, and the limitations of the current VM backup solution.</span></span>

<span data-ttu-id="d2570-115">PowerShell을 효과적으로 사용하기 위해 개체의 계층 구조와 시작하는 위치를 이해하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-115">To use PowerShell effectively, it is necessary to understand the hierarchy of objects and from where to start.</span></span>

![복구 서비스 개체 계층 구조](./media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

<span data-ttu-id="d2570-117">AzureRm.RecoveryServices.Backup PowerShell cmdlet 참조를 보려면 Azure 라이브러리의 [Azure Backup - Recovery Services cmdlet](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2570-117">To view the AzureRm.RecoveryServices.Backup PowerShell cmdlet reference, see the [Azure Backup - Recovery Services Cmdlets](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) in the Azure library.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="d2570-118">설정 및 등록</span><span class="sxs-lookup"><span data-stu-id="d2570-118">Setup and Registration</span></span>
<span data-ttu-id="d2570-119">시작하려면</span><span class="sxs-lookup"><span data-stu-id="d2570-119">To begin:</span></span>

1. <span data-ttu-id="d2570-120">[PowerShell 최신 버전 다운로드](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (필요한 최소 버전: 1.4.0)</span><span class="sxs-lookup"><span data-stu-id="d2570-120">[Download the latest version of PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (the minimum version required is: 1.4.0)</span></span>
2. <span data-ttu-id="d2570-121">다음 명령을 입력하여 사용할 수 있는 Azure 백업 PowerShell cmdlet을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-121">Find the Azure Backup PowerShell cmdlets available by typing the following command:</span></span>

```
PS C:\> Get-Command *azurermrecoveryservices*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Backup-AzureRmRecoveryServicesBackupItem           1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Disable-AzureRmRecoveryServicesBackupProtection    1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Enable-AzureRmRecoveryServicesBackupProtection     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupContainer         1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupItem              1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupJob               1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupJobDetails        1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupManagementServer  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupProperties        1.4.0      AzureRM.RecoveryServices
Cmdlet          Get-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRMRecoveryServicesBackupRecoveryPoint     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupRetentionPolic... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupSchedulePolicy... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesVault                   1.4.0      AzureRM.RecoveryServices
Cmdlet          Get-AzureRmRecoveryServicesVaultSettingsFile       1.4.0      AzureRM.RecoveryServices
Cmdlet          New-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          New-AzureRmRecoveryServicesVault                   1.4.0      AzureRM.RecoveryServices
Cmdlet          Remove-AzureRmRecoveryServicesProtectionPolicy     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Remove-AzureRmRecoveryServicesVault                1.4.0      AzureRM.RecoveryServices
Cmdlet          Restore-AzureRMRecoveryServicesBackupItem          1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Set-AzureRmRecoveryServicesBackupProperties        1.4.0      AzureRM.RecoveryServices
Cmdlet          Set-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Set-AzureRmRecoveryServicesVaultContext            1.4.0      AzureRM.RecoveryServices
Cmdlet          Stop-AzureRmRecoveryServicesBackupJob              1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Unregister-AzureRmRecoveryServicesBackupContainer  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Unregister-AzureRmRecoveryServicesBackupManagem... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Wait-AzureRmRecoveryServicesBackupJob              1.4.0      AzureRM.RecoveryServices.Backup
```


<span data-ttu-id="d2570-122">다음 작업은 PowerShell로 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-122">The following tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="d2570-123">복구 서비스 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="d2570-123">Create a Recovery Services vault</span></span>
* <span data-ttu-id="d2570-124">Azure VM 백업</span><span class="sxs-lookup"><span data-stu-id="d2570-124">Back up Azure VMs</span></span>
* <span data-ttu-id="d2570-125">백업 작업 트리거</span><span class="sxs-lookup"><span data-stu-id="d2570-125">Trigger a backup job</span></span>
* <span data-ttu-id="d2570-126">백업 작업 모니터링</span><span class="sxs-lookup"><span data-stu-id="d2570-126">Monitor a backup job</span></span>
* <span data-ttu-id="d2570-127">Azure VM 복원</span><span class="sxs-lookup"><span data-stu-id="d2570-127">Restore an Azure VM</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="d2570-128">복구 서비스 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="d2570-128">Create a recovery services vault</span></span>
<span data-ttu-id="d2570-129">다음 단계는 복구 서비스 자격 증명 모음을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-129">The following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="d2570-130">복구 서비스 자격 증명 모음은 백업 자격 증명 모음과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-130">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="d2570-131">처음으로 Azure Backup을 사용하는 경우 **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)** cmdlet을 사용하여 구독에 Azure Recovery Service 공급자를 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-131">If you are using Azure Backup for the first time, you must use the **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)** cmdlet to register the Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="d2570-132">Recovery Services 자격 증명 모음은 Resource Manager 리소스이므로 리소스 그룹 내에 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-132">The Recovery Services vault is a Resource Manager resource, so you need to place it within a resource group.</span></span> <span data-ttu-id="d2570-133">기존 리소스 그룹을 사용하거나 **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)** cmdlet을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-133">You can use an existing resource group, or create a resource group with the **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)** cmdlet.</span></span> <span data-ttu-id="d2570-134">리소스 그룹을 만들 때 리소스 그룹의 이름과 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-134">When creating a resource group, specify the name and location for the resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="d2570-135">**[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)** cmdlet을 사용하여 Recovery Services 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-135">Use the **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)** cmdlet to create the Recovery Services vault.</span></span> <span data-ttu-id="d2570-136">리소스 그룹에 사용된 동일한 위치를 자격 증명 모음에도 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-136">Be sure to specify the same location for the vault as was used for the resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="d2570-137">[LRS(로컬 중복 저장소)](../storage/common/storage-redundancy.md#locally-redundant-storage) 또는 [GRS(지역 중복 저장소)](../storage/common/storage-redundancy.md#geo-redundant-storage) 중에 사용할 저장소 중복 유형을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-137">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="d2570-138">다음 예제는 testvault에 대한 -BackupStorageRedundancy 옵션이 GeoRedundant로 설정된 것을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-138">The following example shows the -BackupStorageRedundancy option for testvault is set to GeoRedundant.</span></span>

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testvault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > <span data-ttu-id="d2570-139">많은 Azure 백업 cmdlet에는 복구 서비스 자격 증명 모음 개체가 입력으로 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-139">Many Azure Backup cmdlets require the Recovery Services vault object as an input.</span></span> <span data-ttu-id="d2570-140">이런 이유 때문에, 백업 복구 서비스 자격 증명 모음 개체를 변수에 저장하는 것이 편리합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-140">For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.</span></span>
   >
   >

## <a name="view-the-vaults-in-a-subscription"></a><span data-ttu-id="d2570-141">구독의 자격 증명 모음 보기</span><span class="sxs-lookup"><span data-stu-id="d2570-141">View the vaults in a subscription</span></span>
<span data-ttu-id="d2570-142">**[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)**를 사용하여 현재 구독의 모든 자격 증명 모음 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-142">Use **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)** to view the list of all vaults in the current subscription.</span></span> <span data-ttu-id="d2570-143">이 명령을 사용하여 새 자격 증명 모음이 만들어졌는지 확인하거나 구독에서 사용할 수 있는 자격 증명 모음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-143">You can use this command to check that a new vault was created, or to see the available vaults in the subscription.</span></span>

<span data-ttu-id="d2570-144">구독의 모든 자격 증명 모음을 보려면 Get-AzureRmRecoveryServicesVault 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-144">Run the command, Get-AzureRmRecoveryServicesVault, to view all vaults in the subscription.</span></span> <span data-ttu-id="d2570-145">다음 예제에서는 각 자격 증명 모음에 대해 표시되는 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-145">The following example shows the information displayed for each vault.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault
Name              : Contoso-vault
ID                : /subscriptions/1234
Type              : Microsoft.RecoveryServices/vaults
Location          : WestUS
ResourceGroupName : Contoso-docs-rg
SubscriptionId    : 1234-567f-8910-abc
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
```


## <a name="back-up-azure-vms"></a><span data-ttu-id="d2570-146">Azure VM 백업</span><span class="sxs-lookup"><span data-stu-id="d2570-146">Back up Azure VMs</span></span>
<span data-ttu-id="d2570-147">Recovery Services 자격 증명 모음을 사용하여 가상 컴퓨터를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-147">Use a Recovery Services vault to protect your virtual machines.</span></span> <span data-ttu-id="d2570-148">보호를 적용하기 전에 자격 증명 모음 컨텍스트(자격 증명 모음에 보호된 데이터 형식)를 설정하고 보호 정책을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-148">Before you apply the protection, set the vault context (the type of data protected in the vault), and verify the protection policy.</span></span> <span data-ttu-id="d2570-149">보호 정책은 백업 작업을 실행하는 시간과 각 백업 스냅숏을 유지하는 기간에 대한 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-149">The protection policy is the schedule when the backup jobs run, and how long each backup snapshot is retained.</span></span>

### <a name="set-vault-context"></a><span data-ttu-id="d2570-150">자격 증명 모음 컨텍스트 설정</span><span class="sxs-lookup"><span data-stu-id="d2570-150">Set vault context</span></span>
<span data-ttu-id="d2570-151">VM에서 보호를 사용하도록 설정하기 전에 **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**를 사용하여 자격 증명 모음 컨텍스트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-151">Before enabling protection on a VM, use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** to set the vault context.</span></span> <span data-ttu-id="d2570-152">자격 증명 모음 컨텍스트가 설정되면 모든 후속 cmdlet에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-152">Once the vault context is set, it applies to all subsequent cmdlets.</span></span> <span data-ttu-id="d2570-153">다음 예제에서는 자격 증명 모음, *testvault*에 대한 자격 증명 모음 컨텍스트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-153">The following example sets the vault context for the vault, *testvault*.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name "testvault" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a><span data-ttu-id="d2570-154">보호 정책 만들기 </span><span class="sxs-lookup"><span data-stu-id="d2570-154">Create a protection policy</span></span>
<span data-ttu-id="d2570-155">Recovery Services 자격 증명 모음을 만들면 기본 보호 및 보존 정책이 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-155">When you create a Recovery Services vault, it comes with default protection and retention policies.</span></span> <span data-ttu-id="d2570-156">기본 보호 정책은 매일 지정된 시간에 백업 작업을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-156">The default protection policy triggers a backup job each day at a specified time.</span></span> <span data-ttu-id="d2570-157">기본 보존 정책은 매일 복구 지점을 30일 동안 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-157">The default retention policy retains the daily recovery point for 30 days.</span></span> <span data-ttu-id="d2570-158">기본 정책을 사용하여 VM을 신속하게 보호하고, 나중에 다른 세부 정보로 정책을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-158">You can use the default policy to quickly protect your VM and edit the policy later with different details.</span></span>

<span data-ttu-id="d2570-159">자격 증명 모음에서 사용할 수 있는 정책의 목록을 보려면 **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-159">Use **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)** to view the protection policies in the vault.</span></span> <span data-ttu-id="d2570-160">특정 정책을 받거나 워크로드 유형과 연결된 정책을 보려면 이 cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-160">You can use this cmdlet to get a specific policy, or to view the policies associated with a workload type.</span></span> <span data-ttu-id="d2570-161">다음 예제에서는 워크로드 유형, AzureVM에 대한 정책을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-161">The following example gets policies for workload type, AzureVM.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType "AzureVM"
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> <span data-ttu-id="d2570-162">PowerShell에서 BackupTime 필드의 표준 시간대는 UTC입니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-162">The timezone of the BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="d2570-163">하지만, 백업 시간이 Azure 포털에 표시될 때는, 사용자의 현지 표준 시간대로 시간이 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-163">However, when the backup time is shown in the Azure portal, the time is adjusted to your local timezone.</span></span>
>
>

<span data-ttu-id="d2570-164">백업 보호 정책은 하나 이상의 보존 정책과 연관됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-164">A backup protection policy is associated with at least one retention policy.</span></span> <span data-ttu-id="d2570-165">보존 정책은 복구 지점을 삭제하기 전에 얼마나 오래 유지할지를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-165">Retention policy defines how long a recovery point is kept before it is deleted.</span></span> <span data-ttu-id="d2570-166">기본 보존 정책을 보려면 **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-166">Use **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)** to view the default retention policy.</span></span>  <span data-ttu-id="d2570-167">마찬가지로 **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)**를 사용하여 기본 일정 정책을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-167">Similarly you can use **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)** to obtain the default schedule policy.</span></span> <span data-ttu-id="d2570-168">**[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet은 백업 정책 정보를 보유하는 PowerShell 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-168">The **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="d2570-169">일정 및 보존 정책 개체는 **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet에 대해 입력으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-169">The schedule and retention policy objects are used as inputs to the **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet.</span></span> <span data-ttu-id="d2570-170">다음 예제에서는 일정 정책 및 보존 정책을 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-170">The following example stores the schedule policy and the retention policy in variables.</span></span> <span data-ttu-id="d2570-171">예제에서는 이러한 변수를 사용하여 보호 정책, *NewPolicy*를 만들 때 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-171">The example uses those variables to define the parameters when creating a protection policy, *NewPolicy*.</span></span>

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType "AzureVM" -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```


### <a name="enable-protection"></a><span data-ttu-id="d2570-172">보호 사용</span><span class="sxs-lookup"><span data-stu-id="d2570-172">Enable protection</span></span>
<span data-ttu-id="d2570-173">백업 보호 정책을 정의한 후에는 항목에 대한 정책을 계속 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-173">Once you have defined the backup protection policy, you still must enable the policy for an item.</span></span> <span data-ttu-id="d2570-174">보호를 사용하도록 설정하려면 **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-174">Use **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)** to enable protection.</span></span> <span data-ttu-id="d2570-175">보호를 사용하도록 설정하는 데에는 항목 및 정책이라는 두 가지 개체가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-175">Enabling protection requires two objects - the item and the policy.</span></span> <span data-ttu-id="d2570-176">정책이 자격 증명 모음과 연결되고 나면, 백업 워크플로가 정책 일정에 정의된 시간에 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-176">Once the policy has been associated with the vault, the backup workflow is triggered at the time defined in the policy schedule.</span></span>

<span data-ttu-id="d2570-177">다음 예제에서는 NewPolicy 정책을 사용하여 V2VM 항목에 대해 보호를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-177">The following example enables protection for the item, V2VM, using the policy, NewPolicy.</span></span> <span data-ttu-id="d2570-178">암호화되지 않은 Resource Manager VM에 대한 보호를 사용하도록 설정하려면</span><span class="sxs-lookup"><span data-stu-id="d2570-178">To enable the protection on non-encrypted Resource Manager VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="d2570-179">암호화된 VM(BEK 및 KEK를 사용하여 암호화된)에 대한 보호를 사용하도록 설정하려면 Azure Backup 서비스에 주요 자격 증명 모음에서 키 및 암호를 읽을 수 있는 권한을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-179">To enable the protection on encrypted VMs (encrypted using BEK and KEK), you need to give the Azure Backup service permission to read keys and secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="d2570-180">암호화된 VM(BEK만 사용하여 암호화된)에 대한 보호를 사용하도록 설정하려면 Azure Backup 서비스에 주요 자격 증명 모음에서 비밀을 읽을 수 있는 권한을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-180">To enable the protection on encrypted VMs (encrypted using BEK only), you need to give the Azure Backup service permission to read secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToSecrets backup,get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> <span data-ttu-id="d2570-181">Azure Government 클라우드를 사용 중이라면 [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet에서 **-ServicePrincipalName** 매개 변수에 대한 ff281ffe-705c-4f53-9f37-a40e6f2c68f3 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-181">If you are using the Azure Government cloud, then use the value ff281ffe-705c-4f53-9f37-a40e6f2c68f3 for the parameter **-ServicePrincipalName** in [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.</span></span>
>
>

<span data-ttu-id="d2570-182">클래식 VM</span><span class="sxs-lookup"><span data-stu-id="d2570-182">For classic VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a><span data-ttu-id="d2570-183">보호 정책 수정</span><span class="sxs-lookup"><span data-stu-id="d2570-183">Modify a protection policy</span></span>
<span data-ttu-id="d2570-184">보호 정책을 수정하려면 [Set-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy)를 사용하여 SchedulePolicy 또는 RetentionPolicy 개체를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-184">To modify the protection policy, use [Set-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) to modify the SchedulePolicy or RetentionPolicy objects.</span></span>

<span data-ttu-id="d2570-185">다음 예제는 복구 지점 보존 기간을 365일로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-185">The following example changes the recovery point retention to 365 days.</span></span>

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy $RetPol
```

## <a name="trigger-a-backup"></a><span data-ttu-id="d2570-186">백업 트리거</span><span class="sxs-lookup"><span data-stu-id="d2570-186">Trigger a backup</span></span>
<span data-ttu-id="d2570-187">**[Backup-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)**을 사용하여 백업 작업을 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-187">You can use **[Backup-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)** to trigger a backup job.</span></span> <span data-ttu-id="d2570-188">초기 백업인 경우 전체 백업입니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-188">If it is the initial backup, it is a full backup.</span></span> <span data-ttu-id="d2570-189">후속 백업에서는 증분 복사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-189">Subsequent backups take an incremental copy.</span></span> <span data-ttu-id="d2570-190">**[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**를 사용하여 백업 작업을 트리거하기 전에 자격 증명 모음 컨텍스트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-190">Be sure to use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** to set the vault context before triggering the backup job.</span></span> <span data-ttu-id="d2570-191">다음 예제에서는 자격 증명 모음 컨텍스트가 설정되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-191">The following example assumes vault context was set.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName "V2VM"
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> <span data-ttu-id="d2570-192">PowerShell에서 표시되는 StartTime 및 EndTime 필드의 시간대는 UTC입니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-192">The timezone of the StartTime and EndTime fields in PowerShell is UTC.</span></span> <span data-ttu-id="d2570-193">하지만, 시간이 Azure 포털에 표시될 때는, 사용자의 현지 표준 시간대로 시간이 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-193">However, when the time is shown in the Azure portal, the time is adjusted to your local timezone.</span></span>
>
>

## <a name="monitoring-a-backup-job"></a><span data-ttu-id="d2570-194">백업 작업 모니터링</span><span class="sxs-lookup"><span data-stu-id="d2570-194">Monitoring a backup job</span></span>
<span data-ttu-id="d2570-195">Azure Portal을 사용하지 않고 백업 작업과 같은 장기 실행 작업을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-195">You can monitor long-running operations, such as backup jobs, without using the Azure portal.</span></span> <span data-ttu-id="d2570-196">진행 중인 작업의 상태를 가져오려면 **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)** cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-196">To get the status of an in-progress job, use the **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="d2570-197">이 cmdlet은 특정 자격 증명 모음에 대한 백업 작업을 가져오고 해당 자격 증명 모음은 자격 증명 모음 컨텍스트에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-197">This cmdlet gets the backup jobs for a specific vault, and that vault is specified in the vault context.</span></span> <span data-ttu-id="d2570-198">다음 예제에서는 배열과 같은 진행 중인 작업의 상태를 가져와 $joblist 변수에 상태를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-198">The following example gets the status of an in-progress job as an array, and stores the status in the $joblist variable.</span></span>

```
PS C:\> $joblist = Get-AzureRmRecoveryservicesBackupJob –Status "InProgress"
PS C:\> $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="d2570-199">이러한 작업을 완료하기 위해 폴링하는 대신(불필요한 추가 코드) **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-199">Instead of polling these jobs for completion - which is unnecessary additional code - use the **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="d2570-200">이 cmdlet은 작업이 완료되거나 지정된 시간 제한 값에 도달할 때까지 실행을 일시 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-200">This cmdlet pauses the execution until either the job completes or the specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a><span data-ttu-id="d2570-201">Azure VM 복원</span><span class="sxs-lookup"><span data-stu-id="d2570-201">Restore an Azure VM</span></span>
<span data-ttu-id="d2570-202">Azure 포털을 사용하여 VM을 복원하는 방식과 PowerShell을 사용하여 VM을 복원하는 방식 간에는 주요 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-202">There is a key difference between the restoring a VM using the Azure portal and restoring a VM using PowerShell.</span></span> <span data-ttu-id="d2570-203">PowerShell을 사용하면 복구 지점에서 디스크 및 구성 정보가 만들어질 때 복원 작업이 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-203">With PowerShell, the restore operation is complete once the disks and configuration information from the recovery point are created.</span></span>

> [!NOTE]
> <span data-ttu-id="d2570-204">복원 작업 중에 가상 컴퓨터는 만들어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-204">The restore operation does not create a virtual machine.</span></span>
>
>

<span data-ttu-id="d2570-205">디스크에서 가상 컴퓨터를 만들려면 [저장된 디스크에서 VM 만들기](backup-azure-vms-automation.md#create-a-vm-from-stored-disks) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2570-205">To create a virtual machine from disk, see the section, [Create the VM from stored disks](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span></span> <span data-ttu-id="d2570-206">Azure VM을 복원하는 기본 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-206">The basic steps to restore an Azure VM are:</span></span>

* <span data-ttu-id="d2570-207">VM 선택</span><span class="sxs-lookup"><span data-stu-id="d2570-207">Select the VM</span></span>
* <span data-ttu-id="d2570-208">복구 지점 선택</span><span class="sxs-lookup"><span data-stu-id="d2570-208">Choose a recovery point</span></span>
* <span data-ttu-id="d2570-209">디스크 복원</span><span class="sxs-lookup"><span data-stu-id="d2570-209">Restore the disks</span></span>
* <span data-ttu-id="d2570-210">저장된 디스크에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="d2570-210">Create the VM from stored disks</span></span>

<span data-ttu-id="d2570-211">다음 그래픽에서는 RecoveryServicesVault에서 BackupRecoveryPoint까지로 내려가는 개체 계층 구조를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-211">The following graphic shows the object hierarchy from the RecoveryServicesVault down to the BackupRecoveryPoint.</span></span>

![BackupContainer를 표시하는 복구 서비스 개체 계층 구조](./media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

<span data-ttu-id="d2570-213">백업 데이터를 복원하려면 백업 항목 및 지정 시간 데이터가 포함된 복구 지점을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-213">To restore backup data, identify the backed-up item and the recovery point that holds the point-in-time data.</span></span> <span data-ttu-id="d2570-214">**[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet을 사용하여 자격 증명 모음에서 고객의 계정으로 데이터를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-214">Use the **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet to restore data from the vault to the customer's account.</span></span>

### <a name="select-the-vm"></a><span data-ttu-id="d2570-215">VM 선택</span><span class="sxs-lookup"><span data-stu-id="d2570-215">Select the VM</span></span>
<span data-ttu-id="d2570-216">올바른 백업 항목을 식별하는 PowerShell 개체를 가져오려면, 자격 증명 모음에 있는 컨테이너에서 시작하여, 개체 계층 구조를 따라 내려가는 방식으로 작업해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-216">To get the PowerShell object that identifies the right backup item, start from the container in the vault, and work your way down the object hierarchy.</span></span> <span data-ttu-id="d2570-217">VM을 나타내는 컨테이너를 선택하려면 **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)** cmdlet을 사용하고 **[Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)** cmdlet으로 파이프합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-217">To select the container that represents the VM, use the **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)** cmdlet and pipe that to the **[Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)** cmdlet.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType "AzureVM" –Status "Registered" -FriendlyName "V2VM"
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="d2570-218">복구 지점 선택</span><span class="sxs-lookup"><span data-stu-id="d2570-218">Choose a recovery point</span></span>
<span data-ttu-id="d2570-219">**[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)** cmdlet을 사용하여 백업 항목에 대한 모든 복구 지점을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-219">Use the **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)** cmdlet to list all recovery points for the backup item.</span></span> <span data-ttu-id="d2570-220">그런 후 복원할 복구 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-220">Then choose the recovery point to restore.</span></span> <span data-ttu-id="d2570-221">사용할 복구 지점을 잘 모를 경우 목록에서 가장 최근의 RecoveryPointType = AppConsistent 지점을 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-221">If you are unsure which recovery point to use, it is a good practice to choose the most recent RecoveryPointType = AppConsistent point in the list.</span></span>

<span data-ttu-id="d2570-222">다음 스크립트에서 변수 **$rp**는 과거 7일부터 선택한 백업 항목에 대한 복구 지점의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-222">In the following script, the variable, **$rp**, is an array of recovery points for the selected backup item, from the past seven days.</span></span> <span data-ttu-id="d2570-223">배열은 인덱스 0의 가장 최근 복구 지점부터 역 시간순으로 정렬됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-223">The array is sorted in reverse order of time with the latest recovery point at index 0.</span></span> <span data-ttu-id="d2570-224">복구 지점을 선택하려면 표준 PowerShell 배열 인덱싱을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-224">Use standard PowerShell array indexing to pick the recovery point.</span></span> <span data-ttu-id="d2570-225">예에서, $rp[0]은 최신 복구 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-225">In the example, $rp[0] selects the latest recovery point.</span></span>

```
PS C:\> $startDate = (Get-Date).AddDays(-7)
PS C:\> $endDate = Get-Date
PS C:\> $rp = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $backupitem -StartDate $startdate.ToUniversalTime() -EndDate $enddate.ToUniversalTime()
PS C:\> $rp[0]
RecoveryPointAdditionalInfo :
SourceVMStorageType         : NormalStorage
Name                        : 15260861925810
ItemName                    : VM;iaasvmcontainer;RGName1;V2VM
RecoveryPointId             : /subscriptions/XX/resourceGroups/ RGName1/providers/Microsoft.RecoveryServices/vaults/testvault/backupFabrics/Azure/protectionContainers/IaasVMContainer;iaasvmcontainer;RGName1;V2VM/protectedItems/VM;iaasvmcontainer; RGName1;V2VM/recoveryPoints/15260861925810
RecoveryPointType           : AppConsistent
RecoveryPointTime           : 4/23/2016 5:02:04 PM
WorkloadType                : AzureVM
ContainerName               : IaasVMContainer;iaasvmcontainer; RGName1;V2VM
ContainerType               : AzureVM
BackupManagementType        : AzureVM
```



### <a name="restore-the-disks"></a><span data-ttu-id="d2570-226">디스크 복원</span><span class="sxs-lookup"><span data-stu-id="d2570-226">Restore the disks</span></span>
<span data-ttu-id="d2570-227">**[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet을 사용하여 백업 항목의 데이터 및 구성을 복구 지점으로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-227">Use the **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet to restore a backup item's data and configuration to a recovery point.</span></span> <span data-ttu-id="d2570-228">복구 지점을 식별하면 이 지점을 **-RecoveryPoint** 매개 변수의 값으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-228">Once you have identified a recovery point, use it as the value for the **-RecoveryPoint** parameter.</span></span> <span data-ttu-id="d2570-229">이전 샘플 코드에서 **$rp[0]**이 사용할 복구 지점이었지만,</span><span class="sxs-lookup"><span data-stu-id="d2570-229">In the previous sample code, **$rp[0]** was the recovery point to use.</span></span> <span data-ttu-id="d2570-230">아래 샘플 코드에서는 **$rp[0]**이 디스크를 복원하는 데 사용할 복구 지점이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-230">In the following sample code, **$rp[0]** is the recovery point to use for restoring the disk.</span></span>

<span data-ttu-id="d2570-231">디스크 및 구성 정보를 복원하려면</span><span class="sxs-lookup"><span data-stu-id="d2570-231">To restore the disks and configuration information:</span></span>

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName "DestAccount" -StorageAccountResourceGroupName "DestRG"
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="d2570-232">복원 작업이 완료될 때까지 대기하는 동안 **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-232">Use the **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet to wait for the Restore job to complete.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

<span data-ttu-id="d2570-233">복원 작업이 완료되면 **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)** cmdlet을 사용하여 복원 작업의 세부 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-233">Once the Restore job has completed, use the **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)** cmdlet to get the details of the restore operation.</span></span> <span data-ttu-id="d2570-234">JobDetails 속성에는 VM을 다시 빌드하는 데 필요한 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-234">The JobDetails property has the information needed to rebuild the VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

<span data-ttu-id="d2570-235">디스크를 복원한 후 다음 섹션으로 이동하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-235">Once you restore the disks, go to the next section to create the VM.</span></span>

## <a name="create-a-vm-from-restored-disks"></a><span data-ttu-id="d2570-236">복원된 디스크에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="d2570-236">Create a VM from restored disks</span></span>
<span data-ttu-id="d2570-237">디스크를 복원한 후 다음 단계를 사용하여 디스크에서 가상 컴퓨터를 만들고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-237">After you have restored the disks, use these steps to create and configure the virtual machine from disk.</span></span>

> [!NOTE]
> <span data-ttu-id="d2570-238">복원된 디스크에서 암호화된 VM을 만들려면 Azure 역할에 **Microsoft.KeyVault/vaults/deploy/action** 작업을 수행할 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-238">To create encrypted VMs from restored disks, your Azure role must have permission to perform the action, **Microsoft.KeyVault/vaults/deploy/action**.</span></span> <span data-ttu-id="d2570-239">사용자의 역할에 이 사용 권한이 없는 경우 이 작업이 포함된 사용자 지정 역할을 만드세요.</span><span class="sxs-lookup"><span data-stu-id="d2570-239">If your role does not have this permission, create a custom role with this action.</span></span> <span data-ttu-id="d2570-240">자세한 내용은 [Azure RBAC에서 사용자 지정 역할](../active-directory/role-based-access-control-custom-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2570-240">For more information, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>
>
>

1. <span data-ttu-id="d2570-241">복원된 디스크 속성에서 작업 세부 정보를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-241">Query the restored disk properties for the job details.</span></span>

  ```
  PS C:\> $properties = $details.properties
  PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
  PS C:\> $containerName = $properties["Config Blob Container Name"]
  PS C:\> $blobName = $properties["Config Blob Name"]
  ```

2. <span data-ttu-id="d2570-242">Azure 저장소 컨텍스트를 설정하고 JSON 구성 파일을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-242">Set the Azure storage context and restore the JSON configuration file.</span></span>

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName "testvault"
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```

3. <span data-ttu-id="d2570-243">JSON 구성 파일을 사용하여 VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-243">Use the JSON configuration file to create the VM configuration.</span></span>

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.'properties.hardwareProfile'.vmSize -VMName "testrestore"
    ```

4. <span data-ttu-id="d2570-244">OS 디스크 및 데이터 디스크를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-244">Attach the OS disk and data disks.</span></span> <span data-ttu-id="d2570-245">Vm 구성에 따라 해당 cmdlet을 보려면 관련 링크를 클릭 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d2570-245">Depending on the configuration of your VMs, click on the relevant link to view respective cmdlets:</span></span> 
    - [<span data-ttu-id="d2570-246">관리 되지 않는, 암호화 되지 않은 Vm</span><span class="sxs-lookup"><span data-stu-id="d2570-246">Non-managed, non-encrypted VMs</span></span>](#non-managed-non-encrypted-vms)
    - [<span data-ttu-id="d2570-247">관리 되지 않는, 암호화 된 Vm (BEK에만 해당)</span><span class="sxs-lookup"><span data-stu-id="d2570-247">Non-managed, encrypted VMs (BEK only)</span></span>](#non-managed-encrypted-vms-bek-only)
    - [<span data-ttu-id="d2570-248">관리 되지 않는, 암호화 된 Vm (BEK 및 KEK)</span><span class="sxs-lookup"><span data-stu-id="d2570-248">Non-managed, encrypted VMs (BEK and KEK)</span></span>](#non-managed-encrypted-vms-bek-and-kek)
    - [<span data-ttu-id="d2570-249">관리 되는 암호화 되지 않은 Vm</span><span class="sxs-lookup"><span data-stu-id="d2570-249">Managed, non-encrypted VMs</span></span>](#managed-non-encrypted-vms)
    - [<span data-ttu-id="d2570-250">관리 되 고, 암호화 된 Vm (BEK 및 KEK)</span><span class="sxs-lookup"><span data-stu-id="d2570-250">Managed, encrypted VMs (BEK and KEK)</span></span>](#managed-encrypted-vms-bek-and-kek)
    
    #### <a name="non-managed-non-encrypted-vms"></a><span data-ttu-id="d2570-251">관리되지 않고 암호화되지 않은 VM</span><span class="sxs-lookup"><span data-stu-id="d2570-251">Non-managed, non-encrypted VMs</span></span>

    <span data-ttu-id="d2570-252">관리되지 않고 암호화되지 않은 VM에 다음 샘플을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-252">Use the following sample for non-managed, non-encrypted VMs.</span></span>

    ```
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.StorageProfile'.osDisk.vhd.Uri -CreateOption "Attach"
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.StorageProfile'.OsDisk.OsType
    PS C:\> foreach($dd in $obj.'properties.StorageProfile'.DataDisks)
    {
    $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="non-managed-encrypted-vms-bek-only"></a><span data-ttu-id="d2570-253">관리되지 않고 암호화된 VM(BEK만 해당)</span><span class="sxs-lookup"><span data-stu-id="d2570-253">Non-managed, encrypted VMs (BEK only)</span></span>

    <span data-ttu-id="d2570-254">관리되지 않고 암호화된 VM의 경우(BEK만 사용하여 암호화됨) 디스크를 연결할 수 있으려면 비밀을 Key Vault로 복원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-254">For non-managed, encrypted VMs (encrypted using BEK only), you need to restore the secret to the key vault before you can attach disks.</span></span> <span data-ttu-id="d2570-255">자세한 내용은 [Azure Backup 복구 지점에서 암호화된 가상 컴퓨터 복원](backup-azure-restore-key-secret.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2570-255">For more information, please see the article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="d2570-256">다음 샘플은 암호화된 VM에 대해 OS 및 데이터 디스크를 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-256">The following sample shows how to attach OS and data disks for encrypted VMs.</span></span>

    ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.storageProfile'.osDisk.vhd.uri -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.storageProfile'.osDisk.osType
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

    #### <a name="non-managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="d2570-257">관리되지 않고 암호화된 VM(BEK 및 KEK)</span><span class="sxs-lookup"><span data-stu-id="d2570-257">Non-managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="d2570-258">관리되지 않고 암호화된 VM의 경우(BEK 및 KEK를 암호화됨) 디스크를 연결할 수 있으려면 키 및 비밀을 Key Vault로 복원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-258">For non-managed, encrypted VMs (encrypted using BEK and KEK), you need to restore the key and secret to the key vault before you can attach disks.</span></span> <span data-ttu-id="d2570-259">자세한 내용은 [Azure Backup 복구 지점에서 암호화된 가상 컴퓨터 복원](backup-azure-restore-key-secret.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2570-259">For more information, please see the article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="d2570-260">다음 샘플은 암호화된 VM에 대해 OS 및 데이터 디스크를 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-260">The following sample shows how to attach OS and data disks for encrypted VMs.</span></span>

    ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $kekUrl = "https://ContosoKeyVault.vault.azure.net:443/keys/ContosoKey007/x9xxx00000x0000x9b9949999xx0x006"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.storageProfile'.osDisk.vhd.uri -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -KeyEncryptionKeyUrl $kekUrl -KeyEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.storageProfile'.osDisk.osType
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

    #### <a name="managed-non-encrypted-vms"></a><span data-ttu-id="d2570-261">관리되고 암호화되지 않은 VM</span><span class="sxs-lookup"><span data-stu-id="d2570-261">Managed, non-encrypted VMs</span></span>

    <span data-ttu-id="d2570-262">관리되고 암호화되지 않은 VM의 경우 Blob Storage에서 관리 디스크를 만든 후 디스크를 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-262">For managed non-encrypted VMs, you'll need to create managed disks from blob storage, and then attach the disks.</span></span> <span data-ttu-id="d2570-263">자세한 내용은 [PowerShell을 사용하여 Windows VM에 데이터 디스크 연결](../virtual-machines/windows/attach-disk-ps.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2570-263">For in-depth information, see the article, [Attach a data disk to a Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="d2570-264">다음 샘플 코드는 관리 및 암호화되지 않은 VM에 대해 데이터 디스크를 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-264">The following sample code shows how to attach the data disks for managed non-encrypted VMs.</span></span>

    ```
    PS C:\> $storageType = "StandardLRS"
    PS C:\> $osDiskName = $vm.Name + "_osdisk"
    PS C:\> $osVhdUri = $obj.'properties.storageProfile'.osDisk.vhd.uri
    PS C:\> $diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $osVhdUri
    PS C:\> $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk $diskConfig -ResourceGroupName "test"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -CreateOption "Attach" -Windows
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $dataDiskName = $vm.Name + $dd.name ;
     $dataVhdUri = $dd.vhd.uri ;
     $dataDiskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $dataVhdUri ;
     $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $dataDiskConfig -ResourceGroupName "test" ;
     Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -ManagedDiskId $dataDisk2.Id -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="d2570-265">관리되고 암호화된 VM(BEK 및 KEK)</span><span class="sxs-lookup"><span data-stu-id="d2570-265">Managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="d2570-266">관리 및 암호화되는 VM의 경우(BEK 및 KEK를 암호화됨) Blob Storage에서 관리 디스크를 만든 후 디스크를 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-266">For managed encrypted VMs (encrypted using BEK and KEK), you'll need to create managed disks from blob storage, and then attach the disks.</span></span> <span data-ttu-id="d2570-267">자세한 내용은 [PowerShell을 사용하여 Windows VM에 데이터 디스크 연결](../virtual-machines/windows/attach-disk-ps.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2570-267">For in-depth information, see the article, [Attach a data disk to a Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="d2570-268">다음 샘플 코드는 관리 및 암호화된 VM에 대해 데이터 디스크를 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-268">The following sample code shows how to attach the data disks for managed encrypted VMs.</span></span>

     ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $kekUrl = "https://ContosoKeyVault.vault.azure.net:443/keys/ContosoKey007/x9xxx00000x0000x9b9949999xx0x006"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> $storageType = "StandardLRS"
    PS C:\> $osDiskName = $vm.Name + "_osdisk"
    PS C:\> $osVhdUri = $obj.'properties.storageProfile'.osDisk.vhd.uri
    PS C:\> $diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $osVhdUri
    PS C:\> $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk $diskConfig -ResourceGroupName "test"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -KeyEncryptionKeyUrl $kekUrl -KeyEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $dataDiskName = $vm.Name + $dd.name ;
     $dataVhdUri = $dd.vhd.uri ;
     $dataDiskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $dataVhdUri ;
     $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $dataDiskConfig -ResourceGroupName "test" ;
     Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -ManagedDiskId $dataDisk2.Id -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

5. <span data-ttu-id="d2570-269">네트워크 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-269">Set the Network settings.</span></span>

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. <span data-ttu-id="d2570-270">가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-270">Create the virtual machine.</span></span>

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a><span data-ttu-id="d2570-271">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d2570-271">Next steps</span></span>
<span data-ttu-id="d2570-272">PowerShell을 사용하여 Azure 리소스와 연결하려는 경우 [Windows Server용 백업 배포 및 관리](backup-client-automation.md) PowerShell 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2570-272">If you prefer to use PowerShell to engage with your Azure resources, see the PowerShell article, [Deploy and Manage Backup for Windows Server](backup-client-automation.md).</span></span> <span data-ttu-id="d2570-273">DPM 백업을 관리하는 경우 [DPM에 대한 Backup 배포 및 관리](backup-dpm-automation.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2570-273">If you manage DPM backups, see the article, [Deploy and Manage Backup for DPM](backup-dpm-automation.md).</span></span> <span data-ttu-id="d2570-274">이러한 문서 모두에 Resource Manager 배포용 버전뿐 아니라 클래식 배포용 버전도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2570-274">Both of these articles have a version for Resource Manager deployments and Classic deployments.</span></span>  
