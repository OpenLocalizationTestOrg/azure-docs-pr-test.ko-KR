---
title: "Azure에서 Windows VM에서 디스크 aaaEncrypt | Microsoft Docs"
description: "Tooencrypt 가상 디스크에 대 한 Windows VM에 Azure PowerShell을 사용 하 여 보안을 강화 하는 방법"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/10/2017
ms.author: iainfou
ms.openlocfilehash: 77c42a67cb57a9dc5fe3159fce0be75e3a965be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-windows-vm"></a>어떻게 tooencrypt Windows VM에서 가상 디스크
VM(가상 컴퓨터)의 보안과 규정 준수 상태를 향상시키기 위해 Azure에서 가상 디스크를 암호화할 수 있습니다. 디스크는 Azure Key Vault에 안전하게 보관되는 암호화 키를 사용하여 암호화됩니다. 이러한 암호화 키를 제어하고 용도를 감사할 수 있습니다. 이 세부 정보를 어떻게 문서 tooencrypt Azure PowerShell을 사용 하 여 Windows VM에서 가상 디스크입니다. 수도 있습니다 [hello Azure CLI 2.0을 사용 하 여 Linux VM 암호화](../linux/encrypt-disks.md)합니다.

## <a name="overview-of-disk-encryption"></a>디스크 암호화 개요
Windows VM의 가상 디스크는 미사용 시 Bitlocker를 사용하여 암호화됩니다. Azure에서 가상 디스크 암호화는 무료입니다. 암호화 키가 소프트웨어 보호를 사용 하 여 Azure 키 자격 증명 모음에 저장 하거나 가져오거나 140-2 수준 2 표준 tooFIPS 인증 된 하드웨어 보안 모듈 (Hsm)의 키를 생성할 수 있습니다. 이러한 암호화 한 키를 사용 하는 tooencrypt 가상 디스크 연결 된 tooyour VM의 암호를 해독 합니다. 이러한 암호화 키에 대한 제어를 유지하고 그 사용을 감사할 수 있습니다. Azure Active Directory 서비스 사용자는 VM이 켜지고 꺼지는 경우 이러한 암호화 키 발급을 위한 보안 메커니즘을 제공합니다.

VM을 암호화 하기 위한 hello 프로세스는 다음과 같습니다.

1. Azure Key Vault에서 암호화 키를 만듭니다.
2. 암호화 키 toobe hello 디스크를 암호화 하는 데 사용할 수 있는 구성 합니다.
3. hello Azure 키 자격 증명 모음에서에서 tooread hello 암호화 키 hello 적절 한 권한이 있는 사용자는 Azure Active Directory 서비스를 만듭니다.
4. Hello 명령 tooencrypt hello Azure Active Directory 서비스 사용자 및 사용 되는 적절 한 암호화 키 toobe 지정 하 여 가상 디스크를 실행 합니다.
5. hello Azure Active Directory 서비스 보안 주체 요청 hello Azure 키 자격 증명 모음에서 필요한 암호화 키입니다.
6. hello 가상 디스크는 암호화 키를 제공 하는 hello를 사용 하 여 암호화 됩니다.

## <a name="encryption-process"></a>암호화 프로세스
다음과 같은 추가 구성 요소가 hello 디스크 암호화를 사용 합니다.

* **Azure 키 자격 증명 모음** -toosafeguard 암호화 키 및 hello 디스크 암호화/암호 해독 프로세스에 사용 되는 암호를 사용 합니다. 
  * 이미 존재하는 경우 기존 Azure Key Vault를 사용할 수 있습니다. 없는 toodedicate 주요 자격 증명 모음 tooencrypting 디스크.
  * tooseparate 관리 범위 및 키 가시성 전용된 키 자격 증명 모음을 만들 수 있습니다.
* **Azure Active Directory** -핸들 hello 필요한 암호화 키의 보안 교환 및 인증에 대 한 작업을 요청 합니다. 
  * 일반적으로 응용 프로그램 보유를 위해 Azure Active Directory 인스턴스를 사용할 수 있습니다.
  * hello 서비스 사용자는 보안 메커니즘 toorequest 제공 하 고 hello 적절 한 암호화 키를 실행할 수 있습니다. Azure Active Directory와 통합되는 실제 응용 프로그램을 개발하지는 않습니다.

## <a name="requirements-and-limitations"></a>요구 사항 및 제한 사항
디스크 암호화에 대해 지원되는 시나리오 및 요구 사항은 다음과 같습니다.

* Azure Marketplace 이미지 또는 사용자 지정 VHD 이미지에서 새 Windows VM에 대해 암호화 사용
* Azure에서 기존 Windows VM에 대해 암호화 사용
* 저장소 공간을 사용하여 구성된 Windows VM에서 암호화 사용
* Windows VM에 대한 OS 및 데이터 드라이브에서 암호화 사용 안 함
* 모든 리소스 (예: 키 자격 증명 모음, 저장소 계정 및 VM) hello에 있어야 합니다. 같은 Azure 지역 및 구독 합니다.
* 표준 계층 VM(예: A, D, DS, G 및 GS 시리즈 VM)

디스크 암호화 hello 다음 시나리오에서에서 현재 지원 되지 않습니다.

* 기본 계층 VM.
* Hello 클래식 배포 모델을 사용 하 여 만든 Vm입니다.
* Hello 이미 암호화 된 VM에서 암호화 키를 업데이트합니다.
* 온-프레미스 키 관리 서비스와의 통합

## <a name="create-azure-key-vault-and-keys"></a>Azure Key Vault 및 키 만들기
시작 하기 전에 있는지 확인 hello 최신 버전의 hello Azure PowerShell 모듈 설치 되었습니다. 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다. Hello 명령 예에서는 전체에서 고유한 이름, 위치 및 키 값으로 모든 예제에서는 매개 변수를 대체 합니다. hello 다음 예에서는 사용의 규칙 *myResourceGroup*, *myKeyVault*, *myVM*등입니다.

hello 첫 번째 단계는 Azure 키 자격 증명 모음 toostore toocreate 암호화 키입니다. Azure 주요 자격 증명, 비밀 키를 저장할 수 있습니다 또는 암호 toosecurely를 허용 하는 응용 프로그램 및 서비스에 구현 합니다. 가상 디스크 암호화, 키 자격 증명 모음 toostore tooencrypt 사용된 되는 암호화 키를 만들거나 가상 디스크의 암호를 해독 합니다. 

Hello Azure 키 자격 증명 모음 공급자와 Azure 구독 내에서 사용 하도록 설정 [레지스터 AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), 리소스 그룹을 만드는 다음 [새로 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)합니다. hello 다음 예제에서는 리소스 그룹 이름을 만듭니다 *myResourceGroup* hello에 *미국 동부* 위치:

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

hello Azure 키 자격 증명 모음 포함 hello 암호화 키와 연결 된 계산 hello VM 자체 저장소 같은 리소스에 있어야 합니다. 동일한 지역을 hello 합니다. Azure 키 자격 증명 모음 만들기와 [새로 AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) 디스크 암호화와 함께 사용 하기 위해 주요 자격 증명 모음 hello를 사용 하도록 설정 합니다. *keyVaultName*에 대한 고유한 Key Vault 이름을 다음과 같이 지정합니다.

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

소프트웨어 또는 HSM(하드웨어 보안 모델) 보호를 사용하여 암호화 키를 저장할 수 있습니다. HSM을 사용하려면 프리미엄 Key Vault가 필요합니다. 소프트웨어 보호 키를 저장 하는 표준 주요 자격 증명 모음 보다는 주요 자격 증명 모음 프리미엄은 추가 비용 toocreating 합니다. toocreate hello 앞 단계에서에서 프리미엄 주요 자격 증명 추가 hello *-Sku "프리미엄"* 매개 변수입니다. hello 다음 예제에서는 소프트웨어 보호 키 이후 표준 주요 자격 증명 모음을 만들었습니다. 

두 보호 모델에 대 한 hello Azure 플랫폼 toobe hello VM toodecrypt hello 가상 디스크를 부팅 될 때 액세스 toorequest hello에 대 한 암호화 키에 부여 해야 합니다. [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey)를 사용하여 Key Vault에 암호화 키를 만듭니다. hello 다음 예제에서는 라는 키 *myKey*:

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-hello-azure-active-directory-service-principal"></a>Hello Azure Active Directory 서비스 사용자 만들기
가상 디스크를 암호화 하거나 암호를 해독할 때 계정 toohandle hello 인증 및 자격 증명 모음 키에서에서 암호화 키의 교환 지정 합니다. 이 계정에는 Azure Active Directory 서비스 사용자 hello Azure 플랫폼 toorequest hello VM hello 대신 하 여 적절 한 암호화 키를 수 있습니다. 기본 Azure Active Directory 인스턴스를 구독 내에서 사용할 수 있지만 많은 조직이 전용 Azure Active Directory 디렉터리를 두고 있습니다.

[New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal)을 사용하여 Azure Active Directory에 서비스 주체를 만듭니다. hello를 수행 하는 보안 암호 toospecify [암호 정책 및 Azure Active Directory에서 제한](../../active-directory/active-directory-passwords-policy.md):

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

toosuccessfully 암호화 또는 가상 디스크를 암호 해독, 키 자격 증명 모음에 저장 된 hello 암호화 키에 대 한 권한 집합 toopermit hello Azure Active Directory 서비스 보안 주체 tooread hello 키 여야 합니다. [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy)를 사용하여 Key Vault에 대한 사용 권한을 설정합니다.

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a>가상 컴퓨터 만들기
tootest 암호화 프로세스를 hello, VM을 만들어 보겠습니다. hello 다음 예제에서는 V *myVM* 를 사용 하는 *Windows Server 2016 Datacenter* 이미지:

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName `
    -Location $location `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress -ResourceGroupName $rgName `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "mypublicdns$(Get-Random)"

$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName `
    -Location $location `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface -Name myNic `
    -ResourceGroupName $rgName `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$cred = Get-Credential

$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```


## <a name="encrypt-virtual-machine"></a>가상 컴퓨터 암호화
tooencrypt hello 가상 디스크를 모아 놓은 모든 hello 이전 구성 요소:

1. Hello Azure Active Directory 서비스 사용자 및 암호를 지정 합니다.
2. Hello 주요 자격 증명 모음 toostore hello 메타 데이터에 대 한 암호화 된 디스크를 지정 합니다.
3. Hello 실제 암호화 및 암호 해독에 대 한 암호화 키 toouse hello를 지정 합니다.
4. Tooencrypt hello OS 디스크, hello 데이터 디스크 또는 모두 사용할지를 지정 합니다.

암호화를 사용 하 여 VM [집합 AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) hello Azure 키 자격 증명 모음 키와 Azure Active Directory 서비스 사용자 자격 증명을 사용 하 여 합니다. hello 다음 예제에서는 hello 키 정보를 모두 검색 한 다음 암호화 hello 라는 VM *myVM*:

```powershell
$keyVault = Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $rgName;
$diskEncryptionKeyVaultUrl = $keyVault.VaultUri;
$keyVaultResourceId = $keyVault.ResourceId;
$keyEncryptionKeyUrl = (Get-AzureKeyVaultKey -VaultName $keyVaultName -Name myKey).Key.kid;

Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $rgName `
    -VMName $vmName `
    -AadClientID $app.ApplicationId `
    -AadClientSecret $securePassword `
    -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl `
    -DiskEncryptionKeyVaultId $keyVaultResourceId `
    -KeyEncryptionKeyUrl $keyEncryptionKeyUrl `
    -KeyEncryptionKeyVaultId $keyVaultResourceId
```

Hello 프롬프트 toocontinue hello VM 암호화를 적용 합니다. hello 프로세스 중 hello VM 다시 시작합니다. Hello 암호화 상태를 검토 하는 hello 암호화 프로세스가 완료 되 면 hello VM 다시 부팅 했습니다. [Get AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

hello 비슷한 toohello 다음은 예제 출력:

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a>다음 단계
* Azure Key Vault 관리 방법에 대한 자세한 내용은 [가상 컴퓨터에 대한 Key Vault 설정](key-vault-setup.md)을 참조하세요.
* 암호화 된 사용자 지정 VM tooupload tooAzure를 준비 하 고 같은 디스크 암호화에 대 한 자세한 내용은 참조 하십시오. [Azure 디스크 암호화](../../security/azure-security-disk-encryption.md)합니다.
