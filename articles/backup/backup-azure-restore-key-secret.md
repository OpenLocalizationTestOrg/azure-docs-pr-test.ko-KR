---
title: "Azure Backup을 사용하여 암호화된 VM의 Key Vault 키 및 암호 복원 | Microsoft Docs"
description: "PowerShell을 사용하여 Azure Backup에서 Key Vault 키 및 암호를 복원하는 방법을 알아봅니다."
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 45214083-d5fc-4eb3-a367-0239dc59e0f6
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f2db3449187d655248b13198b268841052570626
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a><span data-ttu-id="18af4-103">Azure Backup을 사용하여 암호화된 VM의 Key Vault 키 및 암호 복원</span><span class="sxs-lookup"><span data-stu-id="18af4-103">Restore Key Vault key and secret for encrypted VMs using Azure Backup</span></span>
<span data-ttu-id="18af4-104">이 문서에서는 Key Vault에 키와 암호가 존재하지 않는 경우 Azure VM Backup을 사용하여 암호화된 Azure VM의 복원을 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="18af4-104">This article talks about using Azure VM Backup to perform restore of encrypted Azure VMs, if your key and secret do not exist in the key vault.</span></span> <span data-ttu-id="18af4-105">복원된 VM에 대한 키(키 암호화 키)와 암호(BitLocker 암호화 키)의 별도의 복사본을 유지하려는 경우 이러한 단계도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18af4-105">These steps can also be used if you want to maintain a separate copy of key (Key Encryption Key) and secret (BitLocker Encryption Key) for the restored VM.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18af4-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="18af4-106">Prerequisites</span></span>
* <span data-ttu-id="18af4-107">**암호화된 VM 백업** - 암호화된 Azure VM은 Azure Backup을 사용하여 백업됩니다.</span><span class="sxs-lookup"><span data-stu-id="18af4-107">**Backup encrypted VMs** - Encrypted Azure VMs have been backed up using Azure Backup.</span></span> <span data-ttu-id="18af4-108">암호화된 Azure VM을 백업하는 방법에 대한 자세한 내용은 [PowerShell을 사용하여 Azure VM의 백업 및 복원 관리](backup-azure-vms-automation.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18af4-108">Refer the article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md) for details about how to backup encrypted Azure VMs.</span></span>
* <span data-ttu-id="18af4-109">**Azure Key Vault 구성** – 키 및 암호를 복원해야 하는 Key Vault가 이미 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="18af4-109">**Configure Azure Key Vault** – Ensure that key vault to which keys and secrets need to be restored is already present.</span></span> <span data-ttu-id="18af4-110">Key Vault 관리에 대한 자세한 내용은 [Azure Key Vault 시작](../key-vault/key-vault-get-started.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18af4-110">Refer the article [Get Started with Azure Key Vault](../key-vault/key-vault-get-started.md) for details about key vault management.</span></span>
* <span data-ttu-id="18af4-111">**디스크 복원** - [PowerShell 단계](backup-azure-vms-automation.md#restore-an-azure-vm)를 사용하여 암호화된 VM에 대한 디스크를 복원하는 복원 작업을 트리거했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="18af4-111">**Restore disk** - Ensure that you have triggered restore job for restoring disks for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm).</span></span> <span data-ttu-id="18af4-112">이 작업은 복원할 암호화된 VM의 키 및 암호가 포함된 저장소 계정에 JSON 파일을 생성하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="18af4-112">This is because this job generates a JSON file in your storage account containing keys and secrets for the encrypted VM to be restored.</span></span>

## <a name="get-key-and-secret-from-azure-backup"></a><span data-ttu-id="18af4-113">Azure Backup에서 키 및 비밀 가져오기</span><span class="sxs-lookup"><span data-stu-id="18af4-113">Get key and secret from Azure Backup</span></span>

> [!NOTE]
> <span data-ttu-id="18af4-114">암호화된 VM의 디스크가 복원되면 다음 사항을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="18af4-114">Once disk has been restored for the encrypted VM, ensure that:</span></span>
> 1. <span data-ttu-id="18af4-115">[디스크 복원 섹션의 PowerShell 단계](backup-azure-vms-automation.md#restore-an-azure-vm)에 설명된 것처럼 $details가 디스크 복원 작업 세부 정보로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="18af4-115">$details is populated with restore disk job details, as mentioned in [PowerShell steps in Restore the Disks section](backup-azure-vms-automation.md#restore-an-azure-vm)</span></span>
> 2. <span data-ttu-id="18af4-116">**키 및 비밀이 키 자격 증명 모음으로 복원된 후**에만 복원된 디스크에서 VM이 만들어져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18af4-116">VM should be created from restored disks only **after key and secret is restored to key vault**.</span></span>
>
>

<span data-ttu-id="18af4-117">복원된 디스크 속성에서 작업 세부 정보를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="18af4-117">Query the restored disk properties for the job details.</span></span>

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

<span data-ttu-id="18af4-118">Azure 저장소 컨텍스트를 설정하고 암호화된 VM에 대한 키 및 비밀 세부 정보가 포함된 JSON 구성 파일을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="18af4-118">Set the Azure storage context and restore JSON configuration file containing key and secret details for encrypted VM.</span></span>

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a><span data-ttu-id="18af4-119">키 복원</span><span class="sxs-lookup"><span data-stu-id="18af4-119">Restore key</span></span>
<span data-ttu-id="18af4-120">위에 언급된 대상 경로에 JSON 파일이 생성되면 JSON에서 키 BLOB 파일을 생성하고 restore key cmdlet에 제공하여 해당 키(KEK)를 다시 키 자격 증명 모음에 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="18af4-120">Once the JSON file is generated in the destination path mentioned above, generate key blob file from the JSON and feed it to restore key cmdlet to put the key (KEK) back in the key vault.</span></span>

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a><span data-ttu-id="18af4-121">암호 복원</span><span class="sxs-lookup"><span data-stu-id="18af4-121">Restore secret</span></span>
<span data-ttu-id="18af4-122">위에서 생성된 JSON 파일을 사용하여 비밀 이름 및 값을 가져오고 set secret cmdlet에 제공하여 해당 비밀(BEK)을 다시 키 자격 증명 모음에 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="18af4-122">Use the JSON file generated above to get secret name and value and feed it to set secret cmdlet to put the secret (BEK) back in the key vault.</span></span> <span data-ttu-id="18af4-123">**VM이 BEK 및 KEK를 사용하여 암호화된 경우 이러한 cmdlet을 사용합니다.**</span><span class="sxs-lookup"><span data-stu-id="18af4-123">**Use these cmdlets if your VM is encrypted using BEK and KEK.**</span></span>

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

<span data-ttu-id="18af4-124">VM이 **BEK만 사용하여 암호화된 경우** JSON에서 비밀 Blob 파일을 생성하고 공급하여 비밀 cmdlet을 복원함으로써 비밀(BEK)을 다시 Key Vault에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="18af4-124">If your VM is **encrypted using BEK only**, generate secret blob file from the JSON and feed it to restore secret cmdlet to put the secret (BEK) back in the key vault.</span></span>

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. <span data-ttu-id="18af4-125">$secretname 값은 $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl 출력을 참조하고 secrets/ 뒤의 텍스트를 사용하여 얻을 수 있습니다. 예를 들어 출력 비밀 URL은 https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163이고 비밀 이름은 B3284AAA-DAAA-4AAA-B393-60CAA848AAAA입니다.</span><span class="sxs-lookup"><span data-stu-id="18af4-125">Value for $secretname can be obtained by referring to the output of $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="18af4-126">DiskEncryptionKeyFileName 태그 값은 비밀 이름과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="18af4-126">Value of the tag DiskEncryptionKeyFileName is same as secret name.</span></span>
>
>

## <a name="create-virtual-machine-from-restored-disk"></a><span data-ttu-id="18af4-127">복원된 디스크에서 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="18af4-127">Create virtual machine from restored disk</span></span>
<span data-ttu-id="18af4-128">Azure VM Backup을 사용하여 암호화된 VM을 백업한 경우 위에 언급된 PowerShell cmdlet은 키 및 비밀을 Key Vault로 다시 복원하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18af4-128">If you have backed up encrypted VM using Azure VM Backup, the PowerShell cmdlets mentioned above help you restore key and secret back to the key vault.</span></span> <span data-ttu-id="18af4-129">복원한 후에는 [PowerShell을 사용하여 Azure VM의 백업 및 복원 관리](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) 문서를 참조하여 복원된 디스크, 키 및 비밀에서 암호화된 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18af4-129">After restoring them, refer the article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) to create encrypted VMs from restored disk, key, and secret.</span></span>

## <a name="legacy-approach"></a><span data-ttu-id="18af4-130">기존의 접근 방식</span><span class="sxs-lookup"><span data-stu-id="18af4-130">Legacy approach</span></span>
<span data-ttu-id="18af4-131">위에 설명된 접근 방식이 모든 복구 지점에 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="18af4-131">The approach mentioned above would work for all the recovery points.</span></span> <span data-ttu-id="18af4-132">그렇지만 BEK 및 KEK를 사용하여 암호화된 VM의 경우는 복구 지점에서 키 및 비밀 정보를 가져오는 이전의 접근 방식도 2017년 7월 11일 이전의 복구 지점에 계속 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="18af4-132">However, the older approach of getting key and secret information from recovery point, would be valid for recovery points older than July 11, 2017 for VMs encrypted using BEK and KEK.</span></span> <span data-ttu-id="18af4-133">[PowerShell 단계](backup-azure-vms-automation.md#restore-an-azure-vm)를 사용하여 암호화된 VM에 대한 디스크 복원 작업을 완료하면 $rp가 유효한 값으로 채워졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="18af4-133">Once restore disk job is complete for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm), ensure that $rp is populated with a valid value.</span></span>

### <a name="restore-key"></a><span data-ttu-id="18af4-134">키 복원</span><span class="sxs-lookup"><span data-stu-id="18af4-134">Restore key</span></span>
<span data-ttu-id="18af4-135">다음 cmdlet을 사용하여 복구 지점에서 키(KEK) 정보를 가져오고 restore key cmdlet에 제공하여 키 자격 증명 모음에 다시 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="18af4-135">Use the following cmdlets to get key (KEK) information from recovery point and feed it to restore key cmdlet to put it back in the key vault.</span></span>

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a><span data-ttu-id="18af4-136">암호 복원</span><span class="sxs-lookup"><span data-stu-id="18af4-136">Restore secret</span></span>
<span data-ttu-id="18af4-137">다음 cmdlet을 사용하여 복구 지점에서 비밀(BEK) 정보를 가져오고 set secret cmdlet에 제공하여 키 자격 증명 모음에 다시 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="18af4-137">Use the following cmdlets to get secret (BEK) information from recovery point and feed it to set secret cmdlet to put it back in the key vault.</span></span>

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. <span data-ttu-id="18af4-138">$secretname 값은 $rp1.KeyAndSecretDetails.SecretUrl 출력을 참조하고 secrets/ 뒤의 텍스트를 사용하여 얻을 수 있습니다. 예를 들어 출력 비밀 URL은 https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163이고 비밀 이름은 B3284AAA-DAAA-4AAA-B393-60CAA848AAAA입니다.</span><span class="sxs-lookup"><span data-stu-id="18af4-138">Value for $secretname can be obtained by referring to the output of $rp1.KeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="18af4-139">DiskEncryptionKeyFileName 태그 값은 비밀 이름과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="18af4-139">Value of the tag DiskEncryptionKeyFileName is same as secret name.</span></span>
> 3. <span data-ttu-id="18af4-140">키를 다시 복원한 후 [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet을 사용하여 DiskEncryptionKeyEncryptionKeyURL에 대한 값을 Key Vault에서 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18af4-140">Value for DiskEncryptionKeyEncryptionKeyURL can be obtained from key vault after restoring the keys back and using [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="18af4-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="18af4-141">Next steps</span></span>
<span data-ttu-id="18af4-142">키 및 비밀을 키 자격 증명 모음으로 다시 복원한 후에는 [PowerShell을 사용하여 Azure VM의 백업 및 복원 관리](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) 문서를 참조하여 복원된 디스크, 키 및 비밀에서 암호화된 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18af4-142">After restoring key and secret back to key vault, refer the article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) to create encrypted VMs from restored disk, key and secret.</span></span>
