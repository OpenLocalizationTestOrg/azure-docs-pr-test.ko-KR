---
title: "Azure에서 aaaSecure SSL과 함께 IIS 인증서 | Microsoft Docs"
description: "Toosecure hello IIS 웹 서버 Azure에서 Windows VM에서 SSL 인증서를 사용 하는 방법에 대해 알아봅니다"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/14/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 7a9e0ce07be2f55095fdb5347b64faf5caa4f7e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-iis-web-server-with-ssl-certificates-on-a-windows-virtual-machine-in-azure"></a>Azure의 Windows 가상 컴퓨터에서 SSL 인증서로 IIS 웹 서버 보호
toosecure 웹 서버, 나중에 SSL (Secure Sockets) 인증서 수 tooencrypt 웹 트래픽을 사용 합니다. 이 SSL 인증서 Azure 키 자격 증명 모음에 저장할 수 있으며 Azure에서 인증서 tooWindows 가상 컴퓨터 (Vm)의 보안 배포를 허용 합니다. 이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * Azure Key Vault 만들기
> * 생성 또는 인증서 toohello 주요 자격 증명 모음 업로드
> * VM을 만들고 hello IIS 웹 서버 설치
> * Hello VM hello 인증서 삽입 및을 SSL 바인딩과 함께 IIS를 구성 합니다.

이 자습서는 Azure PowerShell 모듈 버전 3.6 이상 hello가 필요합니다. 실행 ` Get-Module -ListAvailable AzureRM` toofind hello 버전입니다. Tooupgrade 필요한 경우 참조 [Azure PowerShell 설치 모듈](/powershell/azure/install-azurerm-ps)합니다.


## <a name="overview"></a>개요
Azure Key Vault는 암호화 키 및 비밀 정보(인증서 또는 암호)를 보호합니다. 주요 자격 증명 모음은 hello 인증서 관리 프로세스를 간소화 하는 데 도움이 됩니다 하 고 해당 인증서에 액세스 하는 키의 toomaintain 제어 있습니다. Key Vault 내에 자체 서명된 인증서를 만들거나 이미 소유하고 있는 기존의 신뢰할 수 있는 인증서를 업로드할 수 있습니다.

내재된 인증서를 포함하는 사용자 지정 VM 이미지를 사용하는 대신 실행 중인 VM에 인증서를 삽입합니다. 이 프로세스 hello 최신 인증서 배포 하는 동안 웹 서버에 설치 되어 있는지 확인 합니다. 인증서를 바꾸거나 갱신도 없으면 toocreate 새 사용자 지정 VM 이미지입니다. hello 최신 인증서는 추가 Vm을 만들 때 자동으로 삽입 됩니다. Hello 전체 과정 hello 인증서 되지 hello Azure 플랫폼에서 나 가지 스크립트, 명령줄 기록 또는 서식 파일에 표시 됩니다.


## <a name="create-an-azure-key-vault"></a>Azure Key Vault 만들기
Key Vault 및 인증서를 만들려면 먼저 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)을 사용하여 리소스 그룹을 만듭니다. hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroupSecureWeb* hello에 *미국 동부* 위치:

```powershell
$resourceGroup = "myResourceGroupSecureWeb"
$location = "East US"
New-AzureRmResourceGroup -ResourceGroupName $resourceGroup -Location $location
```

다음으로 [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault)를 사용하여 Key Vault를 만듭니다. 각 Key Vault에는 고유한 이름이 필요하며 모두 소문자여야 합니다. 대체 `<mykeyvault>` 다음 예에서는 고유 키 자격 증명 모음 이름으로 hello에:

```powershell
$keyvaultName="<mykeyvault>"
New-AzureRmKeyVault -VaultName $keyvaultName `
    -ResourceGroup $resourceGroup `
    -Location $location `
    -EnabledForDeployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a>인증서 생성 및 Key Vault에 저장
프로덕션 사용을 위해 [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate)를 사용하여 신뢰할 수 있는 공급자가 서명한 유효한 인증서를 가져와야 합니다. 이 자습서에 대 한 hello 다음 예제와 자체 서명 된 인증서를 생성 하는 방법을 [추가 AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) 사용 하 여 기본 인증 정책에서 hello는 [ 새 AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy)합니다. 

```powershell
$policy = New-AzureKeyVaultCertificatePolicy `
    -SubjectName "CN=www.contoso.com" `
    -SecretContentType "application/x-pkcs12" `
    -IssuerName Self `
    -ValidityInMonths 12

Add-AzureKeyVaultCertificate `
    -VaultName $keyvaultName `
    -Name "mycert" `
    -CertificatePolicy $policy 
```


## <a name="create-a-virtual-machine"></a>가상 컴퓨터 만들기
관리자 사용자 이름 및 암호를 사용 하 여 VM hello 집합 [Get-credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

이제 만들 수 있는 VM hello [새로 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)합니다. hello 다음 예제에서는 운영 체제 hello 구성 hello 필요한 가상 네트워크 구성 요소를 만든 다음 만듭니다 라는 VM *myVM*:

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -Name "myVnet" `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRuleRDP"  `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

# Create an inbound network security group rule for port 443
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRuleWWW"  `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name "myNic" `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS2" | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName "myVM" -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName "MicrosoftWindowsServer" `
    -Offer "WindowsServer" -Skus "2016-Datacenter" -Version "latest" | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Create virtual machine
New-AzureRmVM -ResourceGroupName $resourceGroup -Location $location -VM $vmConfig

# Use hello Custom Script Extension tooinstall IIS
Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server -IncludeManagementTools"}'
```

Hello VM toobe 생성에 대 한 몇 가지 분 걸립니다. hello 마지막 단계 사용 하 여 hello Azure 사용자 지정 스크립트 확장 tooinstall hello IIS 웹 서버와 [집합 AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension)합니다.


## <a name="add-a-certificate-toovm-from-key-vault"></a>키 자격 증명 모음에서 인증서 tooVM 추가
주요 자격 증명 모음 tooa VM에서에서 tooadd hello 인증서와 인증서의 hello ID를 가져오려면 [Get AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret)합니다. Hello 인증서 toohello VM 추가와 [추가 AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):

```powershell
$certURL=(Get-AzureKeyVaultSecret -VaultName $keyvaultName -Name "mycert").id

$vm=Get-AzureRMVM -ResourceGroupName $resourceGroup -Name "myVM"
$vaultId=(Get-AzureRmKeyVault -ResourceGroupName $resourceGroup -VaultName $keyVaultName).ResourceId
$vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $vaultId -CertificateStore "My" -CertificateUrl $certURL

Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
```


## <a name="configure-iis-toouse-hello-certificate"></a>IIS toouse hello 인증서 구성
사용 하 여 사용자 지정 스크립트 확장을 사용 하 여 다시 hello [집합 AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooupdate hello IIS 구성 합니다. 이 업데이트는 hello 인증서 키 자격 증명 모음 tooIIS에서 삽입을 적용 하 고 hello 웹 바인딩을 구성 합니다.

```powershell
$PublicSettings = '{
    "fileUris":["https://raw.githubusercontent.com/iainfoulds/azure-samples/master/secure-iis.ps1"],
    "commandToExecute":"powershell -ExecutionPolicy Unrestricted -File secure-iis.ps1"
}'

Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString $publicSettings
```


### <a name="test-hello-secure-web-app"></a>Hello 보안 웹 응용 프로그램 테스트
Hello를 사용 하 여 VM의 공용 IP 주소 가져오기 [Get AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress)합니다. hello 다음 예제에서는 가져옵니다 hello IP 주소를 `myPublicIP` 앞에서 만든:

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName $resourceGroup -Name "myPublicIP" | select "IpAddress"
```

웹 브라우저를 열고 입력 수 이제 `https://<myPublicIP>` hello 주소 표시줄에 있습니다. 자체 서명 된 인증서를 사용 하는 경우 tooaccept hello 보안 경고 선택 **세부 정보** 차례로 **toohello 웹 페이지에서 이동**:

![웹 브라우저 보안 경고 허용](./media/tutorial-secure-web-server/browser-warning.png)

보안된 IIS 웹 사이트 hello 다음 예제와 같이 표시 됩니다.

![실행 중인 보안 IIS 사이트 보기](./media/tutorial-secure-web-server/secured-iis.png)


## <a name="next-steps"></a>다음 단계

이 자습서에서는 Azure Key Vault에 저장된 SSL 인증서를 사용하여 IIS 웹 서버를 보호했습니다. 다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * Azure Key Vault 만들기
> * 생성 또는 인증서 toohello 주요 자격 증명 모음 업로드
> * VM을 만들고 hello IIS 웹 서버 설치
> * Hello VM hello 인증서 삽입 및을 SSL 바인딩과 함께 IIS를 구성 합니다.

가상 컴퓨터 스크립트 샘플을 미리 만들어진이 링크 toosee를 따릅니다.

> [!div class="nextstepaction"]
> [Windows 가상 컴퓨터 스크립트 샘플 ](./powershell-samples.md)