---
title: "Azure 스택에서 PowerShell을 사용 하 여 Windows 가상 컴퓨터 만들기 | Microsoft Docs"
description: "Azure 스택에서 PowerShell과 함께 Windows 가상 컴퓨터를 만듭니다."
services: azure-stack
documentationcenter: 
author: mattbriggs
manager: femila
editor: 
ms.assetid: 7CA6C0AC-23B7-4007-BA32-7A950FD1F3B8
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 09/25/2017
ms.author: mabrigg
ms.custom: mvc
ms.openlocfilehash: 688ab6c55867d72d55e27c21c883c14ef90078d2
ms.sourcegitcommit: a5f16c1e2e0573204581c072cf7d237745ff98dc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2017
---
# <a name="create-a-windows-virtual-machine-by-using-powershell-in-azure-stack"></a>Azure 스택에서 PowerShell을 사용 하 여 Windows 가상 컴퓨터 만들기

*적용 대상: Azure 스택 시스템 통합*

Azure 스택에서 Windows Server 2016 가상 컴퓨터를 만드는 PowerShell을 사용 하 여이 가이드 정보입니다. VPN을 통해 연결 되어 있는 경우 Azure 스택 개발 키트 또는 Windows 기반 외부 클라이언트에서이 문서에 설명 된 단계를 실행할 수 있습니다. 

## <a name="prerequisites"></a>필수 조건 

* Azure 스택 연산자 Azure 스택 마켓플레이스에 "Windows Server 2016" 이미지에 추가 되었는지 확인 합니다.  

* Azure 스택 특정 버전의 Azure PowerShell을 만들고 관리 하는 리소스를 필요 합니다. Azure 스택에 대해 구성 된 PowerShell를 설정 하지 않은 경우의 단계에 따라 [설치](azure-stack-powershell-install.md) 및 [구성](azure-stack-powershell-configure-user.md) PowerShell 합니다.    

## <a name="create-a-resource-group"></a>리소스 그룹 만들기

리소스 그룹은 리소스는 Azure 스택에 배포 되 고 관리 하는 논리 컨테이너입니다. 개발 키트 또는 Azure 스택 통합 시스템에서 리소스 그룹을 만들려면 다음 코드 블록을 실행 합니다. 이 문서에서 모든 변수에 대 한 값을 할당할 것, 되었거나 다른 값을 할당할 그대로 사용할 수 있습니다.  

```powershell
# Create variables to store the location and resource group names.
$location = "local"
$ResourceGroupName = "myResourceGroup"

New-AzureRmResourceGroup `
  -Name $ResourceGroupName `
  -Location $location
```

## <a name="create-storage-resources"></a>저장소 리소스 만들기 

저장소 계정 및 Windows Server 2016 이미지를 저장할 저장소 컨테이너를 만듭니다.

```powershell
# Create variables to store the storage account name and the storage account SKU information
$StorageAccountName = "mystorageaccount"
$SkuName = "Standard_LRS"

# Create a new storage account
$StorageAccount = New-AzureRMStorageAccount `
  -Location $location `
  -ResourceGroupName $ResourceGroupName `
  -Type $SkuName `
  -Name $StorageAccountName

Set-AzureRmCurrentStorageAccount `
  -StorageAccountName $storageAccountName `
  -ResourceGroupName $resourceGroupName

# Create a storage container to store the virtual machine image
$containerName = 'osdisks'
$container = New-AzureStorageContainer `
  -Name $containerName `
  -Permission Blob
```

## <a name="create-networking-resources"></a>네트워킹 리소스 만들기

가상 네트워크, 서브넷 및 공용 IP 주소를 만듭니다. 이러한 리소스는 가상 컴퓨터에 네트워크 연결을 제공 하는 데 사용 됩니다.  

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -Name MyVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -AllocationMethod Static `
  -IdleTimeoutInMinutes 4 `
  -Name "mypublicdns$(Get-Random)"
```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a>네트워크 보안 그룹 및 네트워크 보안 그룹 규칙 만들기

네트워크 보안 그룹 인바운드 및 아웃 바운드 규칙을 사용 하 여 가상 컴퓨터를 보호 합니다. 포트 3389 들어오는 원격 데스크톱 연결을 허용 하도록에 대 한 인바운드 규칙 및 포트 80에 들어오는 웹 트래픽을 허용 하는 인바운드 규칙을 만들 수 있습니다.

```powershell
# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRuleRDP `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1000 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 3389 `
  -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRuleWWW `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1001 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRuleRDP,$nsgRuleWeb 
```
 
### <a name="create-a-network-card-for-the-virtual-machine"></a>가상 컴퓨터에 대한 네트워크 카드 만들기

네트워크 카드는 서브넷, 네트워크 보안 그룹 및 공용 IP 주소에 가상 컴퓨터를 연결합니다.

```powershell
# Create a virtual network card and associate it with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
  -Name myNic `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id `
  -NetworkSecurityGroupId $nsg.Id 
```

## <a name="create-a-virtual-machine"></a>가상 컴퓨터 만들기

가상 컴퓨터 구성을 만듭니다. 구성에 가상 컴퓨터 이미지, 크기, 자격 증명 등 가상 컴퓨터를 배포할 때 사용 되는 설정을 포함 합니다.

```powershell
# Define a credential object to store the username and password for the virtual machine
$UserName='demouser'
$Password='Password@123'| ConvertTo-SecureString -Force -AsPlainText
$Credential=New-Object PSCredential($UserName,$Password)

# Create the virtual machine configuration object
$VmName = "VirtualMachinelatest"
$VmSize = "Standard_A1"
$VirtualMachine = New-AzureRmVMConfig `
  -VMName $VmName `
  -VMSize $VmSize 

$VirtualMachine = Set-AzureRmVMOperatingSystem `
  -VM $VirtualMachine `
  -Windows `
  -ComputerName "MainComputer" `
  -Credential $Credential 

$VirtualMachine = Set-AzureRmVMSourceImage `
  -VM $VirtualMachine `
  -PublisherName "MicrosoftWindowsServer" `
  -Offer "WindowsServer" `
  -Skus "2016-Datacenter" `
  -Version "latest"

$osDiskName = "OsDisk"
$osDiskUri = '{0}vhds/{1}-{2}.vhd' -f `
  $StorageAccount.PrimaryEndpoints.Blob.ToString(),`
  $vmName.ToLower(), `
  $osDiskName

# Sets the operating system disk properties on a virtual machine. 
$VirtualMachine = Set-AzureRmVMOSDisk `
  -VM $VirtualMachine `
  -Name $osDiskName `
  -VhdUri $OsDiskUri `
  -CreateOption FromImage | `
  Add-AzureRmVMNetworkInterface -Id $nic.Id 

#Create the virtual machine.
New-AzureRmVM `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -VM $VirtualMachine
```

## <a name="connect-to-the-virtual-machine"></a>가상 컴퓨터에 연결

이전 단계에서 만든 가상 컴퓨터에 원격으로 하려면 해당 공용 IP 주소가 필요 합니다. 가상 컴퓨터의 공용 IP 주소를 얻기 위해 다음 명령을 실행 합니다. 

```powershell
Get-AzureRmPublicIpAddress `
  -ResourceGroupName $ResourceGroupName | Select IpAddress
```
 
다음 명령을 사용 하 여 가상 컴퓨터와 원격 데스크톱 세션을 만듭니다. IP 주소를 가상 컴퓨터의 publicIPAddress 바꿉니다. 대화 상자가 나타나면 사용자 이름 및 가상 컴퓨터를 만들 때 사용한 암호를 입력 합니다.

```powershell
mstsc /v <publicIpAddress>
```

## <a name="install-iis-via-powershell"></a>PowerShell을 통해 IIS 설치

이제 Azure VM에 로그인했으므로 IIS를 설치하고 웹 트래픽을 허용하는 로컬 방화벽 규칙을 사용하려면 PowerShell의 단일 줄을 사용할 수 있습니다. PowerShell 프롬프트를 열고 다음 명령을 실행합니다.

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-the-iis-welcome-page"></a>IIS 시작 페이지 보기

IIS를 설치하고 현재 포트 80이 인터넷에서 VM에 열려 있으면 사용자가 선택한 웹 브라우저를 사용하여 기본 IIS 시작 페이지를 볼 수 있습니다. 위에 설명한 *publicIpAddress*를 사용하여 기본 페이지를 방문해야 합니다. 

![IIS 기본 사이트](./media/azure-stack-quick-create-vm-windows-powershell/default-iis-website.png) 


## <a name="delete-the-virtual-machine"></a>가상 컴퓨터 삭제

더 이상 필요 없는, 가상 컴퓨터와 해당 관련된 리소스를 포함 하는 리소스 그룹을 제거 하려면 다음 명령을 사용 합니다.

```powershell
Remove-AzureRmResourceGroup `
  -Name $ResourceGroupName
```

## <a name="next-steps"></a>다음 단계

이 퀵 스타트의 간단한 Windows 가상 컴퓨터를 배포한 합니다. Azure 스택 가상 컴퓨터에 대 한 자세한 내용은 계속 [스택 Azure의에서 가상 컴퓨터에 대 한 고려 사항](azure-stack-vm-considerations.md)합니다.

