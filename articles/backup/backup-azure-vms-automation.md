---
title: "aaaDeploy 및 PowerShell을 사용 하 여 리소스 관리자를 통해 배포 된 Vm에 대 한 백업 관리 | Microsoft Docs"
description: "PowerShell toodeploy를 사용 하 고 리소스 관리자를 통해 배포 된 Vm에 대 한 azure에서 백업 관리"
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
ms.openlocfilehash: 486fb3ae1902403fe6bf303df57244b76677ab17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azurermrecoveryservicesbackup-cmdlets-tooback-up-virtual-machines"></a><span data-ttu-id="d95e2-103">가상 컴퓨터를 AzureRM.RecoveryServices.Backup cmdlet tooback를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="d95e2-103">Use AzureRM.RecoveryServices.Backup cmdlets tooback up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d95e2-104">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="d95e2-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="d95e2-105">클래식</span><span class="sxs-lookup"><span data-stu-id="d95e2-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="d95e2-106">이 문서를 toouse Azure PowerShell cmdlet tooback 및 복구할 복구 서비스에서 Azure 가상 컴퓨터 (VM)의 저장소를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-106">This article shows you how toouse Azure PowerShell cmdlets tooback up and recover an Azure virtual machine (VM) from a Recovery Services vault.</span></span> <span data-ttu-id="d95e2-107">복구 서비스 자격 증명 모음은 Azure 리소스 관리자 리소스 이며 tooprotect 사용 되는 데이터 및 Azure 백업과 Azure Site Recovery 서비스에서 자산 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-107">A Recovery Services vault is an Azure Resource Manager resource and is used tooprotect data and assets in both Azure Backup and Azure Site Recovery services.</span></span> <span data-ttu-id="d95e2-108">복구 서비스 자격 증명 모음 tooprotect Azure 서비스 관리자를 통해 배포 된 Vm 및 Azure 리소스 관리자를 통해 배포 된 Vm을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-108">You can use a Recovery Services vault tooprotect Azure Service Manager-deployed VMs, and Azure Resource Manager-deployed VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="d95e2-109">Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델인 [리소스 관리자와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-109">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d95e2-110">이 문서는 hello 리소스 관리자 모델을 사용 하 여 만든 Vm과 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-110">This article is for use with VMs created using hello Resource Manager model.</span></span>
>
>

<span data-ttu-id="d95e2-111">이 문서 안내 tooprotect PowerShell을 사용 하 여 VM 및 복원 데이터 복구 지점에서.</span><span class="sxs-lookup"><span data-stu-id="d95e2-111">This article walks you through using PowerShell tooprotect a VM, and restore data from a recovery point.</span></span>

## <a name="concepts"></a><span data-ttu-id="d95e2-112">개념</span><span class="sxs-lookup"><span data-stu-id="d95e2-112">Concepts</span></span>
<span data-ttu-id="d95e2-113">Hello hello 서비스의 개요에 대 한 Azure 백업 서비스에 잘 알고 없는 경우 체크 아웃 [Azure 백업 이란?](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="d95e2-113">If you are not familiar with hello Azure Backup service, for an overview of hello service, check out [What is Azure Backup?](backup-introduction-to-azure-backup.md)</span></span> <span data-ttu-id="d95e2-114">시작 하기 전에 Azure 백업을 사용 하 여 필요한 필수 구성 요소 toowork hello에 대 한 hello essentials를 포함 하 고 hello 현재 VM 백업 솔루션의 제한 사항 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-114">Before you start, ensure that you cover hello essentials about hello prerequisites needed toowork with Azure Backup, and hello limitations of hello current VM backup solution.</span></span>

<span data-ttu-id="d95e2-115">PowerShell toouse 필요한 toounderstand hello 계층 개체의 및 위치는 효과적으로 toostart 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-115">toouse PowerShell effectively, it is necessary toounderstand hello hierarchy of objects and from where toostart.</span></span>

![복구 서비스 개체 계층 구조](./media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

<span data-ttu-id="d95e2-117">tooview hello AzureRm.RecoveryServices.Backup PowerShell cmdlet 참조 참조 hello [Azure 백업-복구 서비스 Cmdlet](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) hello Azure 라이브러리에서에서.</span><span class="sxs-lookup"><span data-stu-id="d95e2-117">tooview hello AzureRm.RecoveryServices.Backup PowerShell cmdlet reference, see hello [Azure Backup - Recovery Services Cmdlets](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) in hello Azure library.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="d95e2-118">설정 및 등록</span><span class="sxs-lookup"><span data-stu-id="d95e2-118">Setup and Registration</span></span>
<span data-ttu-id="d95e2-119">toobegin:</span><span class="sxs-lookup"><span data-stu-id="d95e2-119">toobegin:</span></span>

1. <span data-ttu-id="d95e2-120">[Hello 최신 버전의 PowerShell 다운로드](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (필요한 hello 최소 버전은: 1.4.0)</span><span class="sxs-lookup"><span data-stu-id="d95e2-120">[Download hello latest version of PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (hello minimum version required is: 1.4.0)</span></span>
2. <span data-ttu-id="d95e2-121">Hello 다음 명령을 입력 하 여 사용할 수 있는 hello Azure 백업 PowerShell cmdlet을 찾으려면</span><span class="sxs-lookup"><span data-stu-id="d95e2-121">Find hello Azure Backup PowerShell cmdlets available by typing hello following command:</span></span>

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


<span data-ttu-id="d95e2-122">PowerShell과 함께 작업을 수행 하는 hello는 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-122">hello following tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="d95e2-123">복구 서비스 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="d95e2-123">Create a Recovery Services vault</span></span>
* <span data-ttu-id="d95e2-124">Azure VM 백업</span><span class="sxs-lookup"><span data-stu-id="d95e2-124">Back up Azure VMs</span></span>
* <span data-ttu-id="d95e2-125">백업 작업 트리거</span><span class="sxs-lookup"><span data-stu-id="d95e2-125">Trigger a backup job</span></span>
* <span data-ttu-id="d95e2-126">백업 작업 모니터링</span><span class="sxs-lookup"><span data-stu-id="d95e2-126">Monitor a backup job</span></span>
* <span data-ttu-id="d95e2-127">Azure VM 복원</span><span class="sxs-lookup"><span data-stu-id="d95e2-127">Restore an Azure VM</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="d95e2-128">복구 서비스 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="d95e2-128">Create a recovery services vault</span></span>
<span data-ttu-id="d95e2-129">단계를 수행 하는 hello 복구 서비스 자격 증명 모음을 만드는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-129">hello following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="d95e2-130">복구 서비스 자격 증명 모음은 백업 자격 증명 모음과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-130">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="d95e2-131">을 사용 중인 Azure 백업 hello에 대 한 처음으로 hello를 사용 해야  **[레지스터 AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)**  cmdlet tooregister hello Azure 복구 서비스 공급자를 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-131">If you are using Azure Backup for hello first time, you must use hello **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)** cmdlet tooregister hello Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="d95e2-132">hello 복구 서비스 자격 증명 모음이 리소스 관리자 리소스 tooplace 있으므로 리소스 그룹 내에서.</span><span class="sxs-lookup"><span data-stu-id="d95e2-132">hello Recovery Services vault is a Resource Manager resource, so you need tooplace it within a resource group.</span></span> <span data-ttu-id="d95e2-133">기존 리소스 그룹을 사용 하거나 hello로 리소스 그룹을 만들 수 있습니다  **[새로 AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)**  cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d95e2-133">You can use an existing resource group, or create a resource group with hello **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)** cmdlet.</span></span> <span data-ttu-id="d95e2-134">리소스 그룹을 만들 때 hello 이름과 hello 리소스 그룹에 대 한 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-134">When creating a resource group, specify hello name and location for hello resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="d95e2-135">사용 하 여 hello  **[새로 AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)**  복구 서비스 자격 증명 모음 cmdlet toocreate hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-135">Use hello **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)** cmdlet toocreate hello Recovery Services vault.</span></span> <span data-ttu-id="d95e2-136">Hello 리소스 그룹에 대해 사용한 것과 toospecify hello hello 자격 증명 모음에 대해 동일한 위치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-136">Be sure toospecify hello same location for hello vault as was used for hello resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="d95e2-137">Hello 유형의 저장소 중복성 toouse;를 지정 합니다. 사용할 수 있습니다 [로컬 중복 저장소 (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) 또는 [지역 중복 저장소 (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage)합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-137">Specify hello type of storage redundancy toouse; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="d95e2-138">hello 다음 예제에서는 testvault에 대 한 hello-BackupStorageRedundancy 옵션 tooGeoRedundant 설정</span><span class="sxs-lookup"><span data-stu-id="d95e2-138">hello following example shows hello -BackupStorageRedundancy option for testvault is set tooGeoRedundant.</span></span>

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testvault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > <span data-ttu-id="d95e2-139">많은 Azure 백업 cmdlet을 입력으로 hello 복구 서비스 자격 증명 모음 개체를 필요로합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-139">Many Azure Backup cmdlets require hello Recovery Services vault object as an input.</span></span> <span data-ttu-id="d95e2-140">이러한 이유로 변수의 편리한 toostore hello 백업 복구 서비스 자격 증명 모음 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-140">For this reason, it is convenient toostore hello Backup Recovery Services vault object in a variable.</span></span>
   >
   >

## <a name="view-hello-vaults-in-a-subscription"></a><span data-ttu-id="d95e2-141">구독에서 보기 hello 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="d95e2-141">View hello vaults in a subscription</span></span>
<span data-ttu-id="d95e2-142">사용 하 여  **[Get AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)**  tooview hello 목록이 hello 현재 구독에서 모든 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-142">Use **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)** tooview hello list of all vaults in hello current subscription.</span></span> <span data-ttu-id="d95e2-143">이 명령은 toocheck 만들어진 새 자격 증명 모음 또는 toosee hello hello 구독에서 사용할 수 있는 자격 증명 모음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-143">You can use this command toocheck that a new vault was created, or toosee hello available vaults in hello subscription.</span></span>

<span data-ttu-id="d95e2-144">Hello 구독에서 hello 명령, Get-AzureRmRecoveryServicesVault tooview 모든 자격 증명 모음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-144">Run hello command, Get-AzureRmRecoveryServicesVault, tooview all vaults in hello subscription.</span></span> <span data-ttu-id="d95e2-145">hello 다음 예제에서는 각 자격 증명 모음에 대해 표시 되는 hello 정보</span><span class="sxs-lookup"><span data-stu-id="d95e2-145">hello following example shows hello information displayed for each vault.</span></span>

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


## <a name="back-up-azure-vms"></a><span data-ttu-id="d95e2-146">Azure VM 백업</span><span class="sxs-lookup"><span data-stu-id="d95e2-146">Back up Azure VMs</span></span>
<span data-ttu-id="d95e2-147">복구 서비스 자격 증명 모음 tooprotect 가상 컴퓨터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-147">Use a Recovery Services vault tooprotect your virtual machines.</span></span> <span data-ttu-id="d95e2-148">Hello 보호를 적용 하기 전에 hello 자격 증명 모음 컨텍스트 (hello 자격 증명 모음에서 보호 되는 데이터의 hello 형식)를 설정 하 고 hello 보호 정책을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-148">Before you apply hello protection, set hello vault context (hello type of data protected in hello vault), and verify hello protection policy.</span></span> <span data-ttu-id="d95e2-149">hello 보호 정책은 hello 일정 hello 백업 작업이 실행 될 때 및 각 백업 스냅숏에 유지 되는 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-149">hello protection policy is hello schedule when hello backup jobs run, and how long each backup snapshot is retained.</span></span>

### <a name="set-vault-context"></a><span data-ttu-id="d95e2-150">자격 증명 모음 컨텍스트 설정</span><span class="sxs-lookup"><span data-stu-id="d95e2-150">Set vault context</span></span>
<span data-ttu-id="d95e2-151">VM에 대 한 보호를 활성화 하기 전에 사용 하 여  **[집합 AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  tooset hello 자격 증명 모음 컨텍스트.</span><span class="sxs-lookup"><span data-stu-id="d95e2-151">Before enabling protection on a VM, use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** tooset hello vault context.</span></span> <span data-ttu-id="d95e2-152">Hello 자격 증명 모음 컨텍스트가 설정 되 고 나면 tooall 후속 cmdlet이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-152">Once hello vault context is set, it applies tooall subsequent cmdlets.</span></span> <span data-ttu-id="d95e2-153">hello 다음 예제에서는 설정 hello 자격 증명 모음에 대 한 자격 증명 모음 컨텍스트 hello *testvault*합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-153">hello following example sets hello vault context for hello vault, *testvault*.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name "testvault" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a><span data-ttu-id="d95e2-154">보호 정책 만들기 </span><span class="sxs-lookup"><span data-stu-id="d95e2-154">Create a protection policy</span></span>
<span data-ttu-id="d95e2-155">Recovery Services 자격 증명 모음을 만들면 기본 보호 및 보존 정책이 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-155">When you create a Recovery Services vault, it comes with default protection and retention policies.</span></span> <span data-ttu-id="d95e2-156">hello 기본 보호 정책 지정된 된 시간에 매일 백업 작업을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-156">hello default protection policy triggers a backup job each day at a specified time.</span></span> <span data-ttu-id="d95e2-157">hello 기본 보존 정책을 30 일 동안 hello 일별 복구 지점을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-157">hello default retention policy retains hello daily recovery point for 30 days.</span></span> <span data-ttu-id="d95e2-158">Hello 기본값을 사용할 수 있습니다 정책 tooquickly VM을 보호 하 고 나중에 다른 세부 정보를 사용 하 여 hello 정책을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-158">You can use hello default policy tooquickly protect your VM and edit hello policy later with different details.</span></span>

<span data-ttu-id="d95e2-159">사용 하 여  **[Get AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)**  hello 자격 증명 모음에 tooview hello 보호 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-159">Use **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)** tooview hello protection policies in hello vault.</span></span> <span data-ttu-id="d95e2-160">이 cmdlet tooget 특정 정책 또는 작업 유형과 연관 tooview hello 정책을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-160">You can use this cmdlet tooget a specific policy, or tooview hello policies associated with a workload type.</span></span> <span data-ttu-id="d95e2-161">다음 예제는 hello AzureVM 작업 형식에 대 한 정책을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-161">hello following example gets policies for workload type, AzureVM.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType "AzureVM"
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> <span data-ttu-id="d95e2-162">PowerShell에서 hello BackupTime 필드의 hello 표준 시간대는 UTC입니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-162">hello timezone of hello BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="d95e2-163">그러나 hello 백업 시간 hello Azure 포털에에서 표시 되며, hello 시간은 tooyour 조정 된 현지 표준 시간대입니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-163">However, when hello backup time is shown in hello Azure portal, hello time is adjusted tooyour local timezone.</span></span>
>
>

<span data-ttu-id="d95e2-164">백업 보호 정책은 하나 이상의 보존 정책과 연관됩니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-164">A backup protection policy is associated with at least one retention policy.</span></span> <span data-ttu-id="d95e2-165">보존 정책은 복구 지점을 삭제하기 전에 얼마나 오래 유지할지를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-165">Retention policy defines how long a recovery point is kept before it is deleted.</span></span> <span data-ttu-id="d95e2-166">사용 하 여  **[Get AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)**  tooview hello 기본 보존 정책을 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-166">Use **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)** tooview hello default retention policy.</span></span>  <span data-ttu-id="d95e2-167">사용할 수는 마찬가지로  **[Get AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)**  tooobtain hello 기본 일정 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-167">Similarly you can use **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)** tooobtain hello default schedule policy.</span></span> <span data-ttu-id="d95e2-168">hello  **[새로 AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet은 백업 정책 정보를 포함 하는 PowerShell 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-168">hello **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="d95e2-169">hello 일정 및 보존 정책 개체를 사용 하 toohello 입력으로  **[새로 AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d95e2-169">hello schedule and retention policy objects are used as inputs toohello **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet.</span></span> <span data-ttu-id="d95e2-170">hello 다음 예제에서는 hello 일정 정책 및 hello 보존 정책을 변수에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-170">hello following example stores hello schedule policy and hello retention policy in variables.</span></span> <span data-ttu-id="d95e2-171">hello 예제 보호 정책을 만들 때 이러한 변수 toodefine hello 매개 변수 사용 하 여 *NewPolicy*합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-171">hello example uses those variables toodefine hello parameters when creating a protection policy, *NewPolicy*.</span></span>

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType "AzureVM" -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```


### <a name="enable-protection"></a><span data-ttu-id="d95e2-172">보호 사용</span><span class="sxs-lookup"><span data-stu-id="d95e2-172">Enable protection</span></span>
<span data-ttu-id="d95e2-173">Hello 백업 보호 정책을 정의한 경우 항목에 대 한 hello 정책 여전히 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-173">Once you have defined hello backup protection policy, you still must enable hello policy for an item.</span></span> <span data-ttu-id="d95e2-174">사용 하 여  **[Enable AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)**  tooenable 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-174">Use **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)** tooenable protection.</span></span> <span data-ttu-id="d95e2-175">보호를 사용 하려면 두 개체-hello 항목과 hello 정책 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-175">Enabling protection requires two objects - hello item and hello policy.</span></span> <span data-ttu-id="d95e2-176">Hello 정책 hello 자격 증명 모음과 연결 되 면 hello 백업 워크플로 hello 정책 일정에 정의 된 hello 시간에 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-176">Once hello policy has been associated with hello vault, hello backup workflow is triggered at hello time defined in hello policy schedule.</span></span>

<span data-ttu-id="d95e2-177">hello NewPolicy hello 정책을 사용 하 여 V2VM, hello 항목에 대 한 예제 사용 하도록 설정 보호를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-177">hello following example enables protection for hello item, V2VM, using hello policy, NewPolicy.</span></span> <span data-ttu-id="d95e2-178">암호화 되지 않은 리소스 관리자 Vm에서 tooenable hello 보호</span><span class="sxs-lookup"><span data-stu-id="d95e2-178">tooenable hello protection on non-encrypted Resource Manager VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="d95e2-179">에 대 한 tooenable hello 보호 (BEK 및 KEK를 사용 하 여 암호화 된) Vm을 암호화 하 고 toogive hello Azure 백업 서비스 권한 tooread 키 및 키 자격 증명 모음에서 암호를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-179">tooenable hello protection on encrypted VMs (encrypted using BEK and KEK), you need toogive hello Azure Backup service permission tooread keys and secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="d95e2-180">에 대 한 tooenable hello 보호 (만 BEK를 사용 하 여 암호화 된) Vm 암호화 toogive hello Azure 백업 서비스 권한 tooread 비밀 키 자격 증명 모음에서 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-180">tooenable hello protection on encrypted VMs (encrypted using BEK only), you need toogive hello Azure Backup service permission tooread secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToSecrets backup,get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> <span data-ttu-id="d95e2-181">Hello Azure Government 클라우드를 사용 하는 경우 다음 사용 하 여 hello 값 ff281ffe-705c-4f53-9f37-a40e6f2c68f3 hello 매개 변수에 대 한 **-ServicePrincipalName** 에 [Set-azurermkeyvaultaccesspolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet .</span><span class="sxs-lookup"><span data-stu-id="d95e2-181">If you are using hello Azure Government cloud, then use hello value ff281ffe-705c-4f53-9f37-a40e6f2c68f3 for hello parameter **-ServicePrincipalName** in [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.</span></span>
>
>

<span data-ttu-id="d95e2-182">클래식 VM</span><span class="sxs-lookup"><span data-stu-id="d95e2-182">For classic VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a><span data-ttu-id="d95e2-183">보호 정책 수정</span><span class="sxs-lookup"><span data-stu-id="d95e2-183">Modify a protection policy</span></span>
<span data-ttu-id="d95e2-184">toomodify hello 보호 정책을 사용 하 여 [집합 AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) toomodify hello SchedulePolicy 또는 보존 정책 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-184">toomodify hello protection policy, use [Set-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) toomodify hello SchedulePolicy or RetentionPolicy objects.</span></span>

<span data-ttu-id="d95e2-185">hello 다음 예제에서는 변경 hello 복구 지점 보존 too365 일 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-185">hello following example changes hello recovery point retention too365 days.</span></span>

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy $RetPol
```

## <a name="trigger-a-backup"></a><span data-ttu-id="d95e2-186">백업 트리거</span><span class="sxs-lookup"><span data-stu-id="d95e2-186">Trigger a backup</span></span>
<span data-ttu-id="d95e2-187">사용할 수 있습니다  **[백업 AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)**  tootrigger 백업 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-187">You can use **[Backup-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)** tootrigger a backup job.</span></span> <span data-ttu-id="d95e2-188">초기 백업을 hello 인 경우 전체 백업입니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-188">If it is hello initial backup, it is a full backup.</span></span> <span data-ttu-id="d95e2-189">후속 백업에서는 증분 복사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-189">Subsequent backups take an incremental copy.</span></span> <span data-ttu-id="d95e2-190">수 있는지 toouse  **[집합 AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  hello 백업 작업을 트리거하기 전에 tooset hello 자격 증명 모음 컨텍스트.</span><span class="sxs-lookup"><span data-stu-id="d95e2-190">Be sure toouse **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** tooset hello vault context before triggering hello backup job.</span></span> <span data-ttu-id="d95e2-191">다음 예에서는 hello 자격 증명 모음 컨텍스트가 set 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-191">hello following example assumes vault context was set.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName "V2VM"
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> <span data-ttu-id="d95e2-192">PowerShell의 hello StartTime과 EndTime 필드 hello 표준 시간대는 UTC입니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-192">hello timezone of hello StartTime and EndTime fields in PowerShell is UTC.</span></span> <span data-ttu-id="d95e2-193">그러나 hello 시간 hello Azure 포털에에서 표시 되며, hello 시간은 tooyour 조정 된 현지 표준 시간대입니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-193">However, when hello time is shown in hello Azure portal, hello time is adjusted tooyour local timezone.</span></span>
>
>

## <a name="monitoring-a-backup-job"></a><span data-ttu-id="d95e2-194">백업 작업 모니터링</span><span class="sxs-lookup"><span data-stu-id="d95e2-194">Monitoring a backup job</span></span>
<span data-ttu-id="d95e2-195">Hello Azure 포털을 사용 하지 않고 백업 작업 같은 장기 실행 작업을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-195">You can monitor long-running operations, such as backup jobs, without using hello Azure portal.</span></span> <span data-ttu-id="d95e2-196">tooget hello 상태의 진행 중인 작업을 사용 하 여 hello  **[Get AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)**  cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d95e2-196">tooget hello status of an in-progress job, use hello **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="d95e2-197">이 cmdlet은 특정 자격 증명 모음에 대 한 백업 작업 hello 가져오고 해당 자격 증명 모음 자격 증명 모음 컨텍스트 hello에에서 지정 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-197">This cmdlet gets hello backup jobs for a specific vault, and that vault is specified in hello vault context.</span></span> <span data-ttu-id="d95e2-198">hello 다음 예제에서는 배열, 진행 중인 작업의 hello 상태를 가져오고 hello 상태 hello $joblist 변수에 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-198">hello following example gets hello status of an in-progress job as an array, and stores hello status in hello $joblist variable.</span></span>

```
PS C:\> $joblist = Get-AzureRmRecoveryservicesBackupJob –Status "InProgress"
PS C:\> $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="d95e2-199">이러한 작업 완료-추가 코드가 필요 없는 기능에 대 한 폴링 대신 hello를 사용 하 여  **[대기 AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d95e2-199">Instead of polling these jobs for completion - which is unnecessary additional code - use hello **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="d95e2-200">이 cmdlet hello 작업을 완료 하거나 hello 지정한 시간 제한 값에 도달 하기 전까지 hello 실행이 일시 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-200">This cmdlet pauses hello execution until either hello job completes or hello specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a><span data-ttu-id="d95e2-201">Azure VM 복원</span><span class="sxs-lookup"><span data-stu-id="d95e2-201">Restore an Azure VM</span></span>
<span data-ttu-id="d95e2-202">Hello Azure 포털을 사용 하 여 복원 PowerShell을 사용 하는 VM 및 VM을 복원 하는 hello 간에 중요 한 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-202">There is a key difference between hello restoring a VM using hello Azure portal and restoring a VM using PowerShell.</span></span> <span data-ttu-id="d95e2-203">PowerShell을 사용 하 여 hello 디스크 및 구성 정보 hello 복구 지점에서이 만들어지면 hello 복원 작업이 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-203">With PowerShell, hello restore operation is complete once hello disks and configuration information from hello recovery point are created.</span></span>

> [!NOTE]
> <span data-ttu-id="d95e2-204">hello 복원 작업에서 가상 컴퓨터를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-204">hello restore operation does not create a virtual machine.</span></span>
>
>

<span data-ttu-id="d95e2-205">hello 섹션을 참조 하는 디스크에서 가상 컴퓨터 toocreate [저장된 디스크에서 VM 만들기 hello](backup-azure-vms-automation.md#create-a-vm-from-stored-disks)합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-205">toocreate a virtual machine from disk, see hello section, [Create hello VM from stored disks](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span></span> <span data-ttu-id="d95e2-206">기본 단계 toorestore hello Azure VM에는</span><span class="sxs-lookup"><span data-stu-id="d95e2-206">hello basic steps toorestore an Azure VM are:</span></span>

* <span data-ttu-id="d95e2-207">Hello VM을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-207">Select hello VM</span></span>
* <span data-ttu-id="d95e2-208">복구 지점 선택</span><span class="sxs-lookup"><span data-stu-id="d95e2-208">Choose a recovery point</span></span>
* <span data-ttu-id="d95e2-209">Hello 디스크를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-209">Restore hello disks</span></span>
* <span data-ttu-id="d95e2-210">저장된 디스크에서 hello VM 만들기</span><span class="sxs-lookup"><span data-stu-id="d95e2-210">Create hello VM from stored disks</span></span>

<span data-ttu-id="d95e2-211">hello 다음 그래픽에서는 toohello BackupRecoveryPoint 아래로 RecoveryServicesVault hello에서 hello 개체 계층 구조</span><span class="sxs-lookup"><span data-stu-id="d95e2-211">hello following graphic shows hello object hierarchy from hello RecoveryServicesVault down toohello BackupRecoveryPoint.</span></span>

![BackupContainer를 표시하는 복구 서비스 개체 계층 구조](./media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

<span data-ttu-id="d95e2-213">toorestore 백업 데이터를 hello 백업한 항목 및 hello 지정 시간 데이터를 보유 하는 hello 복구 지점을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-213">toorestore backup data, identify hello backed-up item and hello recovery point that holds hello point-in-time data.</span></span> <span data-ttu-id="d95e2-214">사용 하 여 hello  **[복원 AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  cmdlet toorestore 데이터로 hello toohello 고객의 계정 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-214">Use hello **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet toorestore data from hello vault toohello customer's account.</span></span>

### <a name="select-hello-vm"></a><span data-ttu-id="d95e2-215">Hello VM을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-215">Select hello VM</span></span>
<span data-ttu-id="d95e2-216">hello를 바로 식별 하는 tooget hello PowerShell 개체 항목을 백업, hello 볼트의 hello 컨테이너에서 시작 및 hello 개체 계층 구조 아래로 프로그램 방식으로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-216">tooget hello PowerShell object that identifies hello right backup item, start from hello container in hello vault, and work your way down hello object hierarchy.</span></span> <span data-ttu-id="d95e2-217">VM을 사용 하 여 hello hello 나타내는 tooselect hello 컨테이너  **[Get AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)**  cmdlet 및 해당 toohello 파이프  **[ Get AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)**  cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d95e2-217">tooselect hello container that represents hello VM, use hello **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)** cmdlet and pipe that toohello **[Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)** cmdlet.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType "AzureVM" –Status "Registered" -FriendlyName "V2VM"
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="d95e2-218">복구 지점 선택</span><span class="sxs-lookup"><span data-stu-id="d95e2-218">Choose a recovery point</span></span>
<span data-ttu-id="d95e2-219">사용 하 여 hello  **[Get AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)**  cmdlet toolist hello 백업 항목에 대 한 모든 복구 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-219">Use hello **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)** cmdlet toolist all recovery points for hello backup item.</span></span> <span data-ttu-id="d95e2-220">복구 지점 toorestore hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-220">Then choose hello recovery point toorestore.</span></span> <span data-ttu-id="d95e2-221">어떤 복구 지점 toouse 해야 할지 잘 모를 경우 좋습니다 toochoose hello 가장 최근의 RecoveryPointType = hello 목록의 AppConsistent 포인트입니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-221">If you are unsure which recovery point toouse, it is a good practice toochoose hello most recent RecoveryPointType = AppConsistent point in hello list.</span></span>

<span data-ttu-id="d95e2-222">다음 스크립트는 hello, 변수, hello **$rp**, hello 백업 항목에서에서 선택한 hello 지난 7 일 동안 복구 지점의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-222">In hello following script, hello variable, **$rp**, is an array of recovery points for hello selected backup item, from hello past seven days.</span></span> <span data-ttu-id="d95e2-223">인덱스 0에 hello 최신 복구 지점으로 시간의 hello 배열은 반대 순서로 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-223">hello array is sorted in reverse order of time with hello latest recovery point at index 0.</span></span> <span data-ttu-id="d95e2-224">Toopick hello 복구 지점 인덱싱 표준 PowerShell 배열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-224">Use standard PowerShell array indexing toopick hello recovery point.</span></span> <span data-ttu-id="d95e2-225">Hello 예제 $rp [0] hello 최신 복구 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-225">In hello example, $rp[0] selects hello latest recovery point.</span></span>

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



### <a name="restore-hello-disks"></a><span data-ttu-id="d95e2-226">Hello 디스크를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-226">Restore hello disks</span></span>
<span data-ttu-id="d95e2-227">사용 하 여 hello  **[복원 AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  cmdlet toorestore 백업 항목의 데이터 및 구성 tooa 복구 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-227">Use hello **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet toorestore a backup item's data and configuration tooa recovery point.</span></span> <span data-ttu-id="d95e2-228">복구 지점을 식별 후 값으로 사용할 hello hello에 대 한 **-RecoveryPoint** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-228">Once you have identified a recovery point, use it as hello value for hello **-RecoveryPoint** parameter.</span></span> <span data-ttu-id="d95e2-229">Hello 이전 샘플 코드와 **$rp [0]** hello 복구 지점 toouse 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-229">In hello previous sample code, **$rp[0]** was hello recovery point toouse.</span></span> <span data-ttu-id="d95e2-230">샘플 코드를 다음 hello에 **$rp [0]** hello 디스크 복원에 대 한 복구 지점 toouse hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-230">In hello following sample code, **$rp[0]** is hello recovery point toouse for restoring hello disk.</span></span>

<span data-ttu-id="d95e2-231">toorestore hello 디스크 및 구성 정보:</span><span class="sxs-lookup"><span data-stu-id="d95e2-231">toorestore hello disks and configuration information:</span></span>

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName "DestAccount" -StorageAccountResourceGroupName "DestRG"
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="d95e2-232">사용 하 여 hello  **[대기 AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  cmdlet toowait 복원 작업 toocomplete hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-232">Use hello **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet toowait for hello Restore job toocomplete.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

<span data-ttu-id="d95e2-233">Hello를 사용 하 여 hello 복원 작업이 완료 되 면  **[Get AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)**  cmdlet tooget hello 세부 정보 hello의 복원 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-233">Once hello Restore job has completed, use hello **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)** cmdlet tooget hello details of hello restore operation.</span></span> <span data-ttu-id="d95e2-234">hello 위해 JobDetails 속성 hello 정보 필요한 toorebuild hello VM에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-234">hello JobDetails property has hello information needed toorebuild hello VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

<span data-ttu-id="d95e2-235">Hello 디스크를 복원한 후 toohello 다음 섹션 toocreate hello VM을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-235">Once you restore hello disks, go toohello next section toocreate hello VM.</span></span>

## <a name="create-a-vm-from-restored-disks"></a><span data-ttu-id="d95e2-236">복원된 디스크에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="d95e2-236">Create a VM from restored disks</span></span>
<span data-ttu-id="d95e2-237">Hello 디스크를 복원한 후 이러한 단계 toocreate를 사용 하 고 디스크에서 hello 가상 컴퓨터를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-237">After you have restored hello disks, use these steps toocreate and configure hello virtual machine from disk.</span></span>

> [!NOTE]
> <span data-ttu-id="d95e2-238">toocreate 복원 된 디스크에서 Vm을 암호화, Azure 역할 사용 권한 tooperform hello 동작이 있어야 **Microsoft.KeyVault/vaults/deploy/action**합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-238">toocreate encrypted VMs from restored disks, your Azure role must have permission tooperform hello action, **Microsoft.KeyVault/vaults/deploy/action**.</span></span> <span data-ttu-id="d95e2-239">사용자의 역할에 이 사용 권한이 없는 경우 이 작업이 포함된 사용자 지정 역할을 만드세요.</span><span class="sxs-lookup"><span data-stu-id="d95e2-239">If your role does not have this permission, create a custom role with this action.</span></span> <span data-ttu-id="d95e2-240">자세한 내용은 [Azure RBAC에서 사용자 지정 역할](../active-directory/role-based-access-control-custom-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d95e2-240">For more information, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>
>
>

1. <span data-ttu-id="d95e2-241">쿼리 hello hello 작업 세부 정보에 대 한 디스크 속성을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-241">Query hello restored disk properties for hello job details.</span></span>

  ```
  PS C:\> $properties = $details.properties
  PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
  PS C:\> $containerName = $properties["Config Blob Container Name"]
  PS C:\> $blobName = $properties["Config Blob Name"]
  ```

2. <span data-ttu-id="d95e2-242">Hello Azure 저장소 컨텍스트를 설정 하 고 hello JSON 구성 파일을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-242">Set hello Azure storage context and restore hello JSON configuration file.</span></span>

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName "testvault"
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```

3. <span data-ttu-id="d95e2-243">Hello JSON 구성 파일 toocreate hello VM 구성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-243">Use hello JSON configuration file toocreate hello VM configuration.</span></span>

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.'properties.hardwareProfile'.vmSize -VMName "testrestore"
    ```

4. <span data-ttu-id="d95e2-244">Hello OS 디스크 및 데이터 디스크를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-244">Attach hello OS disk and data disks.</span></span> <span data-ttu-id="d95e2-245">Vm의 hello 구성에 따라 hello에서 관련 링크 tooview 해당 cmdlet을 클릭 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d95e2-245">Depending on hello configuration of your VMs, click on hello relevant link tooview respective cmdlets:</span></span> 
    - [<span data-ttu-id="d95e2-246">관리 되지 않는, 암호화 되지 않은 Vm</span><span class="sxs-lookup"><span data-stu-id="d95e2-246">Non-managed, non-encrypted VMs</span></span>](#non-managed-non-encrypted-vms)
    - [<span data-ttu-id="d95e2-247">관리 되지 않는, 암호화 된 Vm (BEK에만 해당)</span><span class="sxs-lookup"><span data-stu-id="d95e2-247">Non-managed, encrypted VMs (BEK only)</span></span>](#non-managed-encrypted-vms-bek-only)
    - [<span data-ttu-id="d95e2-248">관리 되지 않는, 암호화 된 Vm (BEK 및 KEK)</span><span class="sxs-lookup"><span data-stu-id="d95e2-248">Non-managed, encrypted VMs (BEK and KEK)</span></span>](#non-managed-encrypted-vms-bek-and-kek)
    - [<span data-ttu-id="d95e2-249">관리 되는 암호화 되지 않은 Vm</span><span class="sxs-lookup"><span data-stu-id="d95e2-249">Managed, non-encrypted VMs</span></span>](#managed-non-encrypted-vms)
    - [<span data-ttu-id="d95e2-250">관리 되 고, 암호화 된 Vm (BEK 및 KEK)</span><span class="sxs-lookup"><span data-stu-id="d95e2-250">Managed, encrypted VMs (BEK and KEK)</span></span>](#managed-encrypted-vms-bek-and-kek)
    
    #### <a name="non-managed-non-encrypted-vms"></a><span data-ttu-id="d95e2-251">관리되지 않고 암호화되지 않은 VM</span><span class="sxs-lookup"><span data-stu-id="d95e2-251">Non-managed, non-encrypted VMs</span></span>

    <span data-ttu-id="d95e2-252">관리 되지 않는, 암호화 되지 않은 Vm에 대 한 샘플 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-252">Use hello following sample for non-managed, non-encrypted VMs.</span></span>

    ```
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.StorageProfile'.osDisk.vhd.Uri -CreateOption "Attach"
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.StorageProfile'.OsDisk.OsType
    PS C:\> foreach($dd in $obj.'properties.StorageProfile'.DataDisks)
    {
    $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="non-managed-encrypted-vms-bek-only"></a><span data-ttu-id="d95e2-253">관리되지 않고 암호화된 VM(BEK만 해당)</span><span class="sxs-lookup"><span data-stu-id="d95e2-253">Non-managed, encrypted VMs (BEK only)</span></span>

    <span data-ttu-id="d95e2-254">관리 되지 않는, 암호화 된 Vm (만 BEK를 사용 하 여 암호화 됨)을 위한 있어야만 toorestore hello toohello 비밀 키 자격 증명 모음 디스크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-254">For non-managed, encrypted VMs (encrypted using BEK only), you need toorestore hello secret toohello key vault before you can attach disks.</span></span> <span data-ttu-id="d95e2-255">자세한 내용은 hello 문서를 참조 하세요 [암호화 된 가상 컴퓨터를 Azure 백업 복구 지점에서 복원](backup-azure-restore-key-secret.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-255">For more information, please see hello article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="d95e2-256">다음 예제는 hello tooattach OS 및 데이터 디스크를 Vm이 암호화 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-256">hello following sample shows how tooattach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="non-managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="d95e2-257">관리되지 않고 암호화된 VM(BEK 및 KEK)</span><span class="sxs-lookup"><span data-stu-id="d95e2-257">Non-managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="d95e2-258">관리 되지 않는, 암호화 된 Vm (BEK 및 KEK를 사용 하 여 암호화)을 위한 있어야만 toorestore hello 키와 비밀 toohello 주요 자격 증명 모음 디스크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-258">For non-managed, encrypted VMs (encrypted using BEK and KEK), you need toorestore hello key and secret toohello key vault before you can attach disks.</span></span> <span data-ttu-id="d95e2-259">자세한 내용은 hello 문서를 참조 하세요 [암호화 된 가상 컴퓨터를 Azure 백업 복구 지점에서 복원](backup-azure-restore-key-secret.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-259">For more information, please see hello article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="d95e2-260">다음 예제는 hello tooattach OS 및 데이터 디스크를 Vm이 암호화 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-260">hello following sample shows how tooattach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="managed-non-encrypted-vms"></a><span data-ttu-id="d95e2-261">관리되고 암호화되지 않은 VM</span><span class="sxs-lookup"><span data-stu-id="d95e2-261">Managed, non-encrypted VMs</span></span>

    <span data-ttu-id="d95e2-262">관리 되는 암호화 되지 않은 Vm에 대 한 blob 저장소에서 관리 되는 toocreate 디스크가 필요 하 고 hello 디스크를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-262">For managed non-encrypted VMs, you'll need toocreate managed disks from blob storage, and then attach hello disks.</span></span> <span data-ttu-id="d95e2-263">자세한 내용을 보려면 hello 문서 참조 [데이터 디스크 tooa Windows VM 연결 PowerShell을 사용 하 여](../virtual-machines/windows/attach-disk-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-263">For in-depth information, see hello article, [Attach a data disk tooa Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="d95e2-264">다음 샘플 코드는 hello tooattach 관리 되는 암호화 되지 않은 Vm에 대 한 데이터 디스크를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-264">hello following sample code shows how tooattach hello data disks for managed non-encrypted VMs.</span></span>

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

    #### <a name="managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="d95e2-265">관리되고 암호화된 VM(BEK 및 KEK)</span><span class="sxs-lookup"><span data-stu-id="d95e2-265">Managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="d95e2-266">관리 되는 암호화 된 Vm (BEK 및 KEK를 사용 하 여 암호화)을 위한 blob 저장소에서 관리 되는 toocreate 디스크가 필요 하 고 hello 디스크를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-266">For managed encrypted VMs (encrypted using BEK and KEK), you'll need toocreate managed disks from blob storage, and then attach hello disks.</span></span> <span data-ttu-id="d95e2-267">자세한 내용을 보려면 hello 문서 참조 [데이터 디스크 tooa Windows VM 연결 PowerShell을 사용 하 여](../virtual-machines/windows/attach-disk-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-267">For in-depth information, see hello article, [Attach a data disk tooa Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="d95e2-268">hello 다음 샘플 코드에서는 tooattach 관리 되는 암호화 된 Vm에 대 한 데이터 디스크를 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d95e2-268">hello following sample code shows how tooattach hello data disks for managed encrypted VMs.</span></span>

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

5. <span data-ttu-id="d95e2-269">Hello 네트워크 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-269">Set hello Network settings.</span></span>

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. <span data-ttu-id="d95e2-270">Hello 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-270">Create hello virtual machine.</span></span>

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a><span data-ttu-id="d95e2-271">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d95e2-271">Next steps</span></span>
<span data-ttu-id="d95e2-272">Azure 리소스와 toouse PowerShell tooengage를 선호 하는 경우 참조 hello PowerShell 문서 [배포 및 Windows Server에 대 한 백업 관리](backup-client-automation.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-272">If you prefer toouse PowerShell tooengage with your Azure resources, see hello PowerShell article, [Deploy and Manage Backup for Windows Server](backup-client-automation.md).</span></span> <span data-ttu-id="d95e2-273">DPM 백업을 관리 하는 경우 참조 hello 문서 [배포 및 DPM에 대 한 백업 관리](backup-dpm-automation.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-273">If you manage DPM backups, see hello article, [Deploy and Manage Backup for DPM](backup-dpm-automation.md).</span></span> <span data-ttu-id="d95e2-274">이러한 문서 모두에 Resource Manager 배포용 버전뿐 아니라 클래식 배포용 버전도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d95e2-274">Both of these articles have a version for Resource Manager deployments and Classic deployments.</span></span>  
