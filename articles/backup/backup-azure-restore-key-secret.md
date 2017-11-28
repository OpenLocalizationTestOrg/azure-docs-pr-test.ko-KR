---
title: "aaaRestore 키 자격 증명 모음 키 및 암호에 대 한 Azure 백업을 사용 하 여 Vm 암호화 | Microsoft Docs"
description: "자세한 내용은 방법 toorestore 키 자격 증명 모음 키 및 PowerShell을 사용 하 여 Azure 백업에는 암호"
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
ms.openlocfilehash: 659b2f647493ffcc9494caee111c8bd584ef9c7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a><span data-ttu-id="6f43e-103">Azure Backup을 사용하여 암호화된 VM의 Key Vault 키 및 암호 복원</span><span class="sxs-lookup"><span data-stu-id="6f43e-103">Restore Key Vault key and secret for encrypted VMs using Azure Backup</span></span>
<span data-ttu-id="6f43e-104">이 문서는 hello 키 자격 증명 모음에 키와 비밀 존재 하지 않는 경우 암호화 된 Azure Vm의 Azure VM 백업 tooperform 복원을 사용 하는 방법에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="6f43e-104">This article talks about using Azure VM Backup tooperform restore of encrypted Azure VMs, if your key and secret do not exist in hello key vault.</span></span> <span data-ttu-id="6f43e-105">키 (키 암호화 키)의 별도 복사본 toomaintain와 hello에 대 한 보안 (BitLocker 암호화 키) VM을 복원할 경우 다음이 단계를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f43e-105">These steps can also be used if you want toomaintain a separate copy of key (Key Encryption Key) and secret (BitLocker Encryption Key) for hello restored VM.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f43e-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6f43e-106">Prerequisites</span></span>
* <span data-ttu-id="6f43e-107">**암호화된 VM 백업** - 암호화된 Azure VM은 Azure Backup을 사용하여 백업됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f43e-107">**Backup encrypted VMs** - Encrypted Azure VMs have been backed up using Azure Backup.</span></span> <span data-ttu-id="6f43e-108">Hello 문서 참조 [PowerShell을 사용 하 여 Azure Vm의 백업 및 복원 관리](backup-azure-vms-automation.md) toobackup Azure Vm을 암호화 하는 방법에 대 한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f43e-108">Refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md) for details about how toobackup encrypted Azure VMs.</span></span>
* <span data-ttu-id="6f43e-109">**Azure 키 자격 증명 모음 구성** – toowhich 키를 키 자격 증명 모음을 확인 하 고 복원 하는 암호 필요 toobe 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f43e-109">**Configure Azure Key Vault** – Ensure that key vault toowhich keys and secrets need toobe restored is already present.</span></span> <span data-ttu-id="6f43e-110">Hello 문서 참조 [Azure 키 자격 증명 모음 시작](../key-vault/key-vault-get-started.md) 주요 자격 증명 모음 관리에 대 한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f43e-110">Refer hello article [Get Started with Azure Key Vault](../key-vault/key-vault-get-started.md) for details about key vault management.</span></span>
* <span data-ttu-id="6f43e-111">**디스크 복원** - [PowerShell 단계](backup-azure-vms-automation.md#restore-an-azure-vm)를 사용하여 암호화된 VM에 대한 디스크를 복원하는 복원 작업을 트리거했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6f43e-111">**Restore disk** - Ensure that you have triggered restore job for restoring disks for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm).</span></span> <span data-ttu-id="6f43e-112">이 작업 저장소 계정의 키 및 암호화 하는 hello VM toobe 복원에 대 한 암호를 포함 하는 JSON 파일을 생성 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="6f43e-112">This is because this job generates a JSON file in your storage account containing keys and secrets for hello encrypted VM toobe restored.</span></span>

## <a name="get-key-and-secret-from-azure-backup"></a><span data-ttu-id="6f43e-113">Azure Backup에서 키 및 비밀 가져오기</span><span class="sxs-lookup"><span data-stu-id="6f43e-113">Get key and secret from Azure Backup</span></span>

> [!NOTE]
> <span data-ttu-id="6f43e-114">Hello 암호화 VM 디스크에 대 한 복원 된 후 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f43e-114">Once disk has been restored for hello encrypted VM, ensure that:</span></span>
> 1. <span data-ttu-id="6f43e-115">$details 채워집니다 복원 디스크 작업 세부 정보에서 설명한 것 처럼 [복원 hello 디스크 섹션의 단계를 PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm)</span><span class="sxs-lookup"><span data-stu-id="6f43e-115">$details is populated with restore disk job details, as mentioned in [PowerShell steps in Restore hello Disks section](backup-azure-vms-automation.md#restore-an-azure-vm)</span></span>
> 2. <span data-ttu-id="6f43e-116">복원 된 디스크에서 VM을 생성할지 **키와 비밀 복원된 tookey 자격 증명 모음을**합니다.</span><span class="sxs-lookup"><span data-stu-id="6f43e-116">VM should be created from restored disks only **after key and secret is restored tookey vault**.</span></span>
>
>

<span data-ttu-id="6f43e-117">쿼리 hello hello 작업 세부 정보에 대 한 디스크 속성을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f43e-117">Query hello restored disk properties for hello job details.</span></span>

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

<span data-ttu-id="6f43e-118">Hello Azure 저장소 컨텍스트를 설정 하 고 암호화 된 VM에 대 한 키와 비밀 세부 정보를 포함 하는 JSON 구성 파일을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f43e-118">Set hello Azure storage context and restore JSON configuration file containing key and secret details for encrypted VM.</span></span>

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a><span data-ttu-id="6f43e-119">키 복원</span><span class="sxs-lookup"><span data-stu-id="6f43e-119">Restore key</span></span>
<span data-ttu-id="6f43e-120">위에서 언급 한 hello 대상 경로에 hello JSON 파일 생성 되 면 hello JSON에서에서 키 blob 파일을 생성 하 고 hello 주요 자격 증명 모음에 다시 toorestore 키 cmdlet tooput hello 키 (KEK) 피드.</span><span class="sxs-lookup"><span data-stu-id="6f43e-120">Once hello JSON file is generated in hello destination path mentioned above, generate key blob file from hello JSON and feed it toorestore key cmdlet tooput hello key (KEK) back in hello key vault.</span></span>

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a><span data-ttu-id="6f43e-121">암호 복원</span><span class="sxs-lookup"><span data-stu-id="6f43e-121">Restore secret</span></span>
<span data-ttu-id="6f43e-122">사용 하 여 hello JSON 파일 tooget 비밀 이름 및 값 위에 생성 하 고 hello 주요 자격 증명 모음에 다시 tooset 비밀 cmdlet tooput hello 암호 (BEK) 피드.</span><span class="sxs-lookup"><span data-stu-id="6f43e-122">Use hello JSON file generated above tooget secret name and value and feed it tooset secret cmdlet tooput hello secret (BEK) back in hello key vault.</span></span> <span data-ttu-id="6f43e-123">**VM이 BEK 및 KEK를 사용하여 암호화된 경우 이러한 cmdlet을 사용합니다.**</span><span class="sxs-lookup"><span data-stu-id="6f43e-123">**Use these cmdlets if your VM is encrypted using BEK and KEK.**</span></span>

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

<span data-ttu-id="6f43e-124">VM이 **만 BEK를 사용 하 여 암호화**hello JSON에서에서 비밀 blob 파일을 생성 하 고 hello 주요 자격 증명 모음에 다시 toorestore 비밀 cmdlet tooput hello 암호 (BEK) 피드.</span><span class="sxs-lookup"><span data-stu-id="6f43e-124">If your VM is **encrypted using BEK only**, generate secret blob file from hello JSON and feed it toorestore secret cmdlet tooput hello secret (BEK) back in hello key vault.</span></span>

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. <span data-ttu-id="6f43e-125">예를 들어 출력 보안 URL은 https://keyvaultname.vault.azure.net/secrets//$encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl의 toohello 출력 참조 및 비밀 후 텍스트를 사용 하 여 $secretname에 대 한 값을 가져올 수 있습니다. B3284AAA-DAAA-4AAA-B393-60CAA848AAAA를 B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 및 비밀 이름이</span><span class="sxs-lookup"><span data-stu-id="6f43e-125">Value for $secretname can be obtained by referring toohello output of $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="6f43e-126">Hello 태그 DiskEncryptionKeyFileName 값 암호 이름이 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6f43e-126">Value of hello tag DiskEncryptionKeyFileName is same as secret name.</span></span>
>
>

## <a name="create-virtual-machine-from-restored-disk"></a><span data-ttu-id="6f43e-127">복원된 디스크에서 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="6f43e-127">Create virtual machine from restored disk</span></span>
<span data-ttu-id="6f43e-128">Azure VM 백업을 사용 하 여 암호화 된 VM을 백업 하는 경우 PowerShell cmdlet hello 위에서 언급 한 도움말 키와 비밀 백 toohello 키 자격 증명 모음을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f43e-128">If you have backed up encrypted VM using Azure VM Backup, hello PowerShell cmdlets mentioned above help you restore key and secret back toohello key vault.</span></span> <span data-ttu-id="6f43e-129">을 복원한 후 hello 문서 참조 [PowerShell을 사용 하 여 Azure Vm의 백업 및 복원 관리](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate 복원 된 디스크, 키 및 암호에서 Vm을 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f43e-129">After restoring them, refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate encrypted VMs from restored disk, key, and secret.</span></span>

## <a name="legacy-approach"></a><span data-ttu-id="6f43e-130">기존의 접근 방식</span><span class="sxs-lookup"><span data-stu-id="6f43e-130">Legacy approach</span></span>
<span data-ttu-id="6f43e-131">위에서 언급 한 hello 접근 방식을 모든 hello 복구 지점에 대해 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f43e-131">hello approach mentioned above would work for all hello recovery points.</span></span> <span data-ttu-id="6f43e-132">그러나 hello 복구 지점에서 키와 비밀 정보를 얻는 이전의 접근 방식 수 2017 년 7 월 11, BEK 및 KEK를 사용 하 여 암호화 하는 Vm에 대 한 보다 오래 된 복구 지점에 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f43e-132">However, hello older approach of getting key and secret information from recovery point, would be valid for recovery points older than July 11, 2017 for VMs encrypted using BEK and KEK.</span></span> <span data-ttu-id="6f43e-133">[PowerShell 단계](backup-azure-vms-automation.md#restore-an-azure-vm)를 사용하여 암호화된 VM에 대한 디스크 복원 작업을 완료하면 $rp가 유효한 값으로 채워졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6f43e-133">Once restore disk job is complete for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm), ensure that $rp is populated with a valid value.</span></span>

### <a name="restore-key"></a><span data-ttu-id="6f43e-134">키 복원</span><span class="sxs-lookup"><span data-stu-id="6f43e-134">Restore key</span></span>
<span data-ttu-id="6f43e-135">복구 지점에서 다음 cmdlet tooget (KEK) 키 정보 hello를 사용 하 고 hello 주요 자격 증명 모음에서 다시 toorestore 키 cmdlet tooput 피드.</span><span class="sxs-lookup"><span data-stu-id="6f43e-135">Use hello following cmdlets tooget key (KEK) information from recovery point and feed it toorestore key cmdlet tooput it back in hello key vault.</span></span>

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a><span data-ttu-id="6f43e-136">암호 복원</span><span class="sxs-lookup"><span data-stu-id="6f43e-136">Restore secret</span></span>
<span data-ttu-id="6f43e-137">복구 지점에서 다음 cmdlet tooget (BEK) 비밀 정보 hello를 사용 하 고 hello 주요 자격 증명 모음에서 다시 tooset 비밀 cmdlet tooput 피드.</span><span class="sxs-lookup"><span data-stu-id="6f43e-137">Use hello following cmdlets tooget secret (BEK) information from recovery point and feed it tooset secret cmdlet tooput it back in hello key vault.</span></span>

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. <span data-ttu-id="6f43e-138">$Rp1의 toohello 출력을 참조 하 여 $secretname에 대 한 값을 가져올 수 있습니다. KeyAndSecretDetails.SecretUrl 및 텍스트를 사용 하 여 비밀 후 / 예를 들어 출력 비밀 URL https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 이며 암호 이름이 B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="6f43e-138">Value for $secretname can be obtained by referring toohello output of $rp1.KeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="6f43e-139">Hello 태그 DiskEncryptionKeyFileName 값 암호 이름이 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6f43e-139">Value of hello tag DiskEncryptionKeyFileName is same as secret name.</span></span>
> 3. <span data-ttu-id="6f43e-140">다시 hello 키를 복원 하 고 사용 하 여 주요 자격 증명 모음에서 DiskEncryptionKeyEncryptionKeyURL에 대 한 값을 가져올 수 있습니다 [Get AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet</span><span class="sxs-lookup"><span data-stu-id="6f43e-140">Value for DiskEncryptionKeyEncryptionKeyURL can be obtained from key vault after restoring hello keys back and using [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="6f43e-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6f43e-141">Next steps</span></span>
<span data-ttu-id="6f43e-142">키와 비밀 백 tookey 자격 증명 모음을 복원한 후 hello 문서 참조 [PowerShell을 사용 하 여 Azure Vm의 백업 및 복원 관리](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate 복원 된 디스크, 키 및 암호에서 Vm을 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f43e-142">After restoring key and secret back tookey vault, refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate encrypted VMs from restored disk, key and secret.</span></span>
