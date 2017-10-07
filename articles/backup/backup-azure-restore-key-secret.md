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
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a>Azure Backup을 사용하여 암호화된 VM의 Key Vault 키 및 암호 복원
이 문서는 hello 키 자격 증명 모음에 키와 비밀 존재 하지 않는 경우 암호화 된 Azure Vm의 Azure VM 백업 tooperform 복원을 사용 하는 방법에 대 한 설명입니다. 키 (키 암호화 키)의 별도 복사본 toomaintain와 hello에 대 한 보안 (BitLocker 암호화 키) VM을 복원할 경우 다음이 단계를 사용할 수도 있습니다.

## <a name="prerequisites"></a>필수 조건
* **암호화된 VM 백업** - 암호화된 Azure VM은 Azure Backup을 사용하여 백업됩니다. Hello 문서 참조 [PowerShell을 사용 하 여 Azure Vm의 백업 및 복원 관리](backup-azure-vms-automation.md) toobackup Azure Vm을 암호화 하는 방법에 대 한 세부 정보에 대 한 합니다.
* **Azure 키 자격 증명 모음 구성** – toowhich 키를 키 자격 증명 모음을 확인 하 고 복원 하는 암호 필요 toobe 이미 있습니다. Hello 문서 참조 [Azure 키 자격 증명 모음 시작](../key-vault/key-vault-get-started.md) 주요 자격 증명 모음 관리에 대 한 세부 정보에 대 한 합니다.
* **디스크 복원** - [PowerShell 단계](backup-azure-vms-automation.md#restore-an-azure-vm)를 사용하여 암호화된 VM에 대한 디스크를 복원하는 복원 작업을 트리거했는지 확인합니다. 이 작업 저장소 계정의 키 및 암호화 하는 hello VM toobe 복원에 대 한 암호를 포함 하는 JSON 파일을 생성 하기 때문입니다.

## <a name="get-key-and-secret-from-azure-backup"></a>Azure Backup에서 키 및 비밀 가져오기

> [!NOTE]
> Hello 암호화 VM 디스크에 대 한 복원 된 후 되어 있는지 확인 합니다.
> 1. $details 채워집니다 복원 디스크 작업 세부 정보에서 설명한 것 처럼 [복원 hello 디스크 섹션의 단계를 PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm)
> 2. 복원 된 디스크에서 VM을 생성할지 **키와 비밀 복원된 tookey 자격 증명 모음을**합니다.
>
>

쿼리 hello hello 작업 세부 정보에 대 한 디스크 속성을 복원 합니다.

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

Hello Azure 저장소 컨텍스트를 설정 하 고 암호화 된 VM에 대 한 키와 비밀 세부 정보를 포함 하는 JSON 구성 파일을 복원 합니다.

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a>키 복원
위에서 언급 한 hello 대상 경로에 hello JSON 파일 생성 되 면 hello JSON에서에서 키 blob 파일을 생성 하 고 hello 주요 자격 증명 모음에 다시 toorestore 키 cmdlet tooput hello 키 (KEK) 피드.

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a>암호 복원
사용 하 여 hello JSON 파일 tooget 비밀 이름 및 값 위에 생성 하 고 hello 주요 자격 증명 모음에 다시 tooset 비밀 cmdlet tooput hello 암호 (BEK) 피드. **VM이 BEK 및 KEK를 사용하여 암호화된 경우 이러한 cmdlet을 사용합니다.**

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

VM이 **만 BEK를 사용 하 여 암호화**hello JSON에서에서 비밀 blob 파일을 생성 하 고 hello 주요 자격 증명 모음에 다시 toorestore 비밀 cmdlet tooput hello 암호 (BEK) 피드.

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. 예를 들어 출력 보안 URL은 https://keyvaultname.vault.azure.net/secrets//$encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl의 toohello 출력 참조 및 비밀 후 텍스트를 사용 하 여 $secretname에 대 한 값을 가져올 수 있습니다. B3284AAA-DAAA-4AAA-B393-60CAA848AAAA를 B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 및 비밀 이름이
> 2. Hello 태그 DiskEncryptionKeyFileName 값 암호 이름이 같습니다.
>
>

## <a name="create-virtual-machine-from-restored-disk"></a>복원된 디스크에서 가상 컴퓨터 만들기
Azure VM 백업을 사용 하 여 암호화 된 VM을 백업 하는 경우 PowerShell cmdlet hello 위에서 언급 한 도움말 키와 비밀 백 toohello 키 자격 증명 모음을 복원 합니다. 을 복원한 후 hello 문서 참조 [PowerShell을 사용 하 여 Azure Vm의 백업 및 복원 관리](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate 복원 된 디스크, 키 및 암호에서 Vm을 암호화 합니다.

## <a name="legacy-approach"></a>기존의 접근 방식
위에서 언급 한 hello 접근 방식을 모든 hello 복구 지점에 대해 작동 합니다. 그러나 hello 복구 지점에서 키와 비밀 정보를 얻는 이전의 접근 방식 수 2017 년 7 월 11, BEK 및 KEK를 사용 하 여 암호화 하는 Vm에 대 한 보다 오래 된 복구 지점에 유효 합니다. [PowerShell 단계](backup-azure-vms-automation.md#restore-an-azure-vm)를 사용하여 암호화된 VM에 대한 디스크 복원 작업을 완료하면 $rp가 유효한 값으로 채워졌는지 확인합니다.

### <a name="restore-key"></a>키 복원
복구 지점에서 다음 cmdlet tooget (KEK) 키 정보 hello를 사용 하 고 hello 주요 자격 증명 모음에서 다시 toorestore 키 cmdlet tooput 피드.

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a>암호 복원
복구 지점에서 다음 cmdlet tooget (BEK) 비밀 정보 hello를 사용 하 고 hello 주요 자격 증명 모음에서 다시 tooset 비밀 cmdlet tooput 피드.

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. $Rp1의 toohello 출력을 참조 하 여 $secretname에 대 한 값을 가져올 수 있습니다. KeyAndSecretDetails.SecretUrl 및 텍스트를 사용 하 여 비밀 후 / 예를 들어 출력 비밀 URL https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 이며 암호 이름이 B3284AAA-DAAA-4AAA-B393-60CAA848AAAA
> 2. Hello 태그 DiskEncryptionKeyFileName 값 암호 이름이 같습니다.
> 3. 다시 hello 키를 복원 하 고 사용 하 여 주요 자격 증명 모음에서 DiskEncryptionKeyEncryptionKeyURL에 대 한 값을 가져올 수 있습니다 [Get AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet
>
>

## <a name="next-steps"></a>다음 단계
키와 비밀 백 tookey 자격 증명 모음을 복원한 후 hello 문서 참조 [PowerShell을 사용 하 여 Azure Vm의 백업 및 복원 관리](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate 복원 된 디스크, 키 및 암호에서 Vm을 암호화 합니다.
