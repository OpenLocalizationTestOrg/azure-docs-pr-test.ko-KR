---
title: "Packer를 사용하여 Windows Azure VM 이미지를 만드는 방법 | Microsoft Docs"
description: "Azure에서 Packer를 사용하여 Windows 가상 컴퓨터의 이미지를 만드는 방법에 대해 알아보기"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: 11a4a4d65be09e6c518836c25bb455a6df738dcb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-packer-to-create-windows-virtual-machine-images-in-azure"></a>Azure에서 Packer를 사용하여 Windows 가상 컴퓨터 이미지를 만드는 방법
Azure의 각 VM(가상 컴퓨터)은 Windows 배포판 및 OS 버전을 정의하는 이미지에서 만들어집니다. 이미지는 사전 설치된 응용 프로그램 및 구성을 포함할 수 있습니다. Azure Marketplace는 가장 일반적인 OS 및 응용 프로그램 환경에 대한 다양한 자사 및 타사 이미지를 제공하거나 사용자 요구에 맞게 사용자 지정 이미지를 만들 수 있습니다. 이 문서에는 오픈 소스 도구 [Packer](https://www.packer.io/)를 사용하여 Azure에서 사용자 지정 이미지를 정의하고 작성하는 방법을 자세히 설명합니다.


## <a name="create-azure-resource-group"></a>Azure 리소스 그룹 만들기
빌드 프로세스 동안 Packer는 원본 VM을 빌드하므로 임시 Azure 리소스를 만듭니다. 이미지로 사용하기 위해 해당 원본 VM을 캡처하려면 리소스 그룹을 정의해야 합니다. Packer 빌드 프로세스의 출력은 이 리소스 그룹에 저장됩니다.

[New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)을 사용하여 리소스 그룹을 만듭니다. 다음 예제에서는 *eastus* 위치에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.

```powershell
$rgName = "myResourceGroup"
$location = "East US"
New-AzureRmResourceGroup -Name $rgName -Location $location
```

## <a name="create-azure-credentials"></a>Azure 자격 증명 만들기
Packer는 서비스 사용자를 사용하여 Azure를 인증합니다. Azure 서비스 사용자는 앱, 서비스 및 Packer와 같은 자동화 도구를 사용할 수 있는 보안 ID입니다. 서비스 사용자가 Azure에서 수행할 수 있는 작업에 대한 사용 권한은 사용자가 제어하고 정의합니다.

[New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal)을 사용하여 서비스 사용자를 만들고 [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment)를 사용하여 리소스를 만들고 관리하는 권한을 서비스 사용자에게 할당합니다.

```powershell
$sp = New-AzureRmADServicePrincipal -DisplayName "Azure Packer IKF" -Password "P@ssw0rd!"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

Azure를 인증하려면 [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription)을 사용하여 Azure 테넌트 및 구독 ID를 가져와야 합니다.

```powershell
$sub = Get-AzureRmSubscription
$sub.TenantId
$sub.SubscriptionId
```

다음 단계에서 이러한 두 개의 ID를 사용합니다.


## <a name="define-packer-template"></a>Packer 템플릿 정의
이미지를 작성하려면 JSON 파일로 템플릿을 만듭니다. 템플릿에서 실제 빌드 프로세스를 통해 수행하는 작성기와 프로비저너를 정의합니다. Packer에는 이전 단계에서 만든 서비스 사용자 자격 증명과 같은 Azure 리소스를 정의하도록 허용하는 [Azure용 프로비저너](https://www.packer.io/docs/builders/azure.html)가 있습니다.

*windows.json*이라는 파일을 만들고 다음 콘텐츠를 붙여 넣습니다. 다음에 대해 사용자 고유의 값을 입력합니다.

| 매개 변수                           | 얻을 수 있는 위치 |
|-------------------------------------|----------------------------------------------------|
| *client_id*                         | `$sp.applicationId`를 사용하여 서비스 사용자 ID 보기 |
| *client_secret*                     | `$securePassword`에서 지정한 암호 |
| *tenant_id*                         | `$sub.TenantId` 명령의 출력 |
| *subscription_id*                   | `$sub.SubscriptionId` 명령의 출력 |
| *object_id*                         | `$sp.Id`를 사용하여 서비스 사용자 개체 ID 보기 |
| *managed_image_resource_group_name* | 첫 번째 단계에서 만든 리소스 그룹의 이름 |
| *managed_image_name*                | 만들어진 관리되는 디스크 이미지의 이름 |

```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "0831b578-8ab6-40b9-a581-9a880a94aab1",
    "client_secret": "P@ssw0rd!",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",
    "object_id": "a7dfb070-0d5b-47ac-b9a5-cf214fff0ae2",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Windows",
    "image_publisher": "MicrosoftWindowsServer",
    "image_offer": "WindowsServer",
    "image_sku": "2016-Datacenter",

    "communicator": "winrm",
    "winrm_use_ssl": "true",
    "winrm_insecure": "true",
    "winrm_timeout": "3m",
    "winrm_username": "packer",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "type": "powershell",
    "inline": [
      "Add-WindowsFeature Web-Server",
      "if( Test-Path $Env:SystemRoot\\windows\\system32\\Sysprep\\unattend.xml ){ rm $Env:SystemRoot\\windows\\system32\\Sysprep\\unattend.xml -Force}",
      "& $Env:SystemRoot\\System32\\Sysprep\\Sysprep.exe /oobe /generalize /shutdown /quiet"
    ]
  }]
}
```

이 템플릿은 Windows Server 2016 VM을 빌드하고 IIS를 설치한 다음 Sysprep을 사용하여 VM을 일반화합니다.


## <a name="build-packer-image"></a>Packer 이미지 작성
로컬 컴퓨터에 Packer를 아직 설치하지 않은 경우 [Packer 설치 지침을 따릅니다](https://www.packer.io/docs/install/index.html).

다음과 같이 Packer 템플릿 파일을 지정하여 이미지를 작성합니다.

```bash
./packer build windows.json
```

이전 명령에서 출력의 예는 다음과 같습니다.

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> task : Image deployment
==> azure-arm:  ->> dept : Engineering
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting the certificate’s URL ...
==> azure-arm:  -> Key Vault Name        : ‘pkrkvpq0mthtbtt’
==> azure-arm:  -> Key Vault Secret Name : ‘packerKeyVaultSecret’
==> azure-arm:  -> Certificate URL       : ‘https://pkrkvpq0mthtbtt.vault.azure.net/secrets/packerKeyVaultSecret/8c7bd823e4fa44e1abb747636128adbb'
==> azure-arm: Setting the certificate’s URL ...
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting the VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.55.35’
==> azure-arm: Waiting for WinRM to become available...
==> azure-arm: Connected to WinRM!
==> azure-arm: Provisioning with Powershell...
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-powershell-provisioner902510110
    azure-arm: #< CLIXML
    azure-arm:
    azure-arm: Success Restart Needed Exit Code      Feature Result
    azure-arm: ------- -------------- ---------      --------------
    azure-arm: True    No             Success        {Common HTTP Features, Default Document, D...
    azure-arm: <Objs Version=“1.1.0.1” xmlns=“http://schemas.microsoft.com/powershell/2004/04"><Obj S=“progress” RefId=“0"><TN RefId=“0”><T>System.Management.Automation.PSCustomObject</T><T>System.Object</T></TN><MS><I64 N=“SourceId”>1</I64><PR N=“Record”><AV>Preparing modules for first use.</AV><AI>0</AI><Nil /><PI>-1</PI><PC>-1</PC><T>Completed</T><SR>-1</SR><SD> </SD></PR></MS></Obj></Objs>
==> azure-arm: Querying the machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> ComputeName       : ‘pkrvmpq0mthtbtt’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-pq0mthtbtt/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> ComputeName       : ‘pkrvmpq0mthtbtt’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> Compute Name              : ‘pkrvmpq0mthtbtt’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm: Deleting the temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. The artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```

Packer가 VM을 빌드하고 프로비저너를 실행하고 배포를 정리하는 데 몇 분 정도 걸립니다.


## <a name="create-vm-from-azure-image"></a>Azure 이미지에서 VM 만들기
[Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential)을 사용하여 VM의 관리자 사용자 이름과 암호를 설정합니다.

```powershell
$cred = Get-Credential
```

이제 [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)을 사용하여 이미지에서 VM을 만들 수 있습니다. 다음 예제에서는 *myPackerImage*에서 *myVM*이라는 VM을 만듭니다.

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $rgName `
    -Location $location `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName $rgName `
    -Location $location `
    -AllocationMethod "Static" `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleWWW  `
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
    -ResourceGroupName $rgName `
    -Location $location `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName $rgName `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Define the image created by Packer
$image = Get-AzureRMImage -ImageName myPackerImage -ResourceGroupName $rgName

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -Id $image.Id | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```

VM을 만드는 데 몇 분이 걸립니다.


## <a name="test-vm-and-iis"></a>VM 및 IIS 테스트
[Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)를 사용하여 VM의 공용 IP 주소를 가져옵니다. 다음 예제에서는 앞서 만든 *myPublicIP*의 IP 주소를 가져옵니다.

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName $rgName `
    -Name "myPublicIP" | select "IpAddress"
```

그런 다음 웹 브라우저에 공용 IP 주소를 입력할 수 있습니다.

![IIS 기본 사이트](./media/build-image-with-packer/iis.png) 


## <a name="next-steps"></a>다음 단계
이 예제에서는 이미 설치된 IIS를 사용하여 VM 이미지를 만드는 데 Packer를 사용했습니다. Team Services, Ansible, Chef 또는 Puppet를 사용하여 이미지에서 만든 VM에 앱을 배포하는 것과 같은 기존 배포 워크플로와 함께 이 VM 이미지를 사용할 수 있습니다.

다른 Windows 배포판에 대한 추가 예제 Packer 템플릿은 [이 GitHub 리포지토리](https://github.com/hashicorp/packer/tree/master/examples/azure)를 참조하세요.