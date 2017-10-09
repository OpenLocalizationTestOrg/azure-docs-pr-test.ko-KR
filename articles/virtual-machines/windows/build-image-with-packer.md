---
title: "aaaHow toocreate Packer 사용 하 여 Windows Azure VM 이미지 | Microsoft Docs"
description: "자세한 내용은 방법 toouse Packer toocreate 이미지의 Windows Azure 가상 컴퓨터"
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
ms.openlocfilehash: d310fae3becb453b52d21281cb8ac53fa14a3fc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-windows-virtual-machine-images-in-azure"></a>Azure에서 toouse Packer toocreate Windows 가상 컴퓨터 이미지 하는 방법
Azure의 각 가상 컴퓨터 (VM) hello Windows 배포 및 운영 체제 버전을 정의 하는 이미지에서 만들어집니다. 이미지는 사전 설치된 응용 프로그램 및 구성을 포함할 수 있습니다. 응용 프로그램 환경 하거나 만들 수 있습니다 맞게 사용자 지정 이미지 tooyour 요구 사항 및 Azure 마켓플레이스 hello 가장 일반적인 OS에 대 한 첫 번째 및 제 3 자에 대 한 여러 이미지를 제공 합니다. 이 문서 toouse hello 소스 도구를 열고 하는 방법을 자세히 설명 [Packer](https://www.packer.io/) Azure의 toodefine 및 빌드 사용자 지정 이미지입니다.


## <a name="create-azure-resource-group"></a>Azure 리소스 그룹 만들기
Hello 빌드 프로세스 동안 Packer hello 원본 VM는 것과 같이 임시 Azure 리소스를 만듭니다. 이미지 형식으로 사용 하기 위해 VM의 소스가 되 toocapture, 리소스 그룹을 정의 해야 합니다. hello hello Packer 빌드 프로세스의 출력에에서 저장 됩니다이 리소스 그룹.

[New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)을 사용하여 리소스 그룹을 만듭니다. hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치:

```powershell
$rgName = "myResourceGroup"
$location = "East US"
New-AzureRmResourceGroup -Name $rgName -Location $location
```

## <a name="create-azure-credentials"></a>Azure 자격 증명 만들기
Packer는 서비스 사용자를 사용하여 Azure를 인증합니다. Azure 서비스 사용자는 앱, 서비스 및 Packer와 같은 자동화 도구를 사용할 수 있는 보안 ID입니다. 제어 하 고이 정보를 toowhat 작업 hello 서비스 사용자는 Azure에서 수행할 수 있는 대로 hello 사용 권한을 정의 합니다.

서비스와 사용자 만들기 [새로 AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) 서비스 보안 주체 toocreate hello에 대 한 권한을 할당 하 고 사용 하 여 리소스를 관리 하 고 [새로 AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):

```powershell
$sp = New-AzureRmADServicePrincipal -DisplayName "Azure Packer IKF" -Password "P@ssw0rd!"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

tooauthenticate tooAzure 또한 해야 tooobtain Azure 테 넌 트 및 구독 Id와 [Get AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):

```powershell
$sub = Get-AzureRmSubscription
$sub.TenantId
$sub.SubscriptionId
```

Hello 다음 단계에서 이러한 두 개의 Id를 사용합니다.


## <a name="define-packer-template"></a>Packer 템플릿 정의
toobuild 이미지를 JSON 파일로 템플릿을 만듭니다. Hello 서식 파일에 빌더를 정의 하 고 provisioners hello 실제을 수행 하는 빌드 프로세스입니다. Packer에는 [provisioner Azure에 대 한](https://www.packer.io/docs/builders/azure.html) toodefine Azure 사용할 수 있는 hello 서비스 사용자 자격 증명 hello 앞 단계에서에서 만든 등의 리소스입니다.

라는 파일을 만들어 *windows.json* 붙여넣기 hello에 따라 콘텐츠입니다. Hello 다음에 대 한 고유한 값을 입력 합니다.

| 매개 변수                           | 여기서 tooobtain |
|-------------------------------------|----------------------------------------------------|
| *client_id*                         | `$sp.applicationId`를 사용하여 서비스 사용자 ID 보기 |
| *client_secret*                     | `$securePassword`에서 지정한 암호 |
| *tenant_id*                         | `$sub.TenantId` 명령의 출력 |
| *subscription_id*                   | `$sub.SubscriptionId` 명령의 출력 |
| *object_id*                         | `$sp.Id`를 사용하여 서비스 사용자 개체 ID 보기 |
| *managed_image_resource_group_name* | Hello 첫 번째 단계에서 만든 리소스 그룹의 이름 |
| *managed_image_name*                | 만들어진 hello 관리 되는 디스크 이미지에 대 한 이름 |

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

이 서식 파일 빌드는 Windows Server 2016 VM을 IIS 설치를 다음 hello Sysprep 사용 하 여 VM을 일반화 하 여 합니다.


## <a name="build-packer-image"></a>Packer 이미지 작성
로컬 컴퓨터에 설치 된 Packer 아직 없는 경우 [hello Packer 설치 지침을 따라](https://www.packer.io/docs/install/index.html)합니다.

Hello 이미지 프로그램 Packer를 지정 하 여 서식 파일을 다음과 같이 만듭니다.

```bash
./packer build windows.json
```

Hello 명령 앞에서 hello 출력의 예는 다음과 같습니다.

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
==> azure-arm: Getting hello certificate’s URL ...
==> azure-arm:  -> Key Vault Name        : ‘pkrkvpq0mthtbtt’
==> azure-arm:  -> Key Vault Secret Name : ‘packerKeyVaultSecret’
==> azure-arm:  -> Certificate URL       : ‘https://pkrkvpq0mthtbtt.vault.azure.net/secrets/packerKeyVaultSecret/8c7bd823e4fa44e1abb747636128adbb'
==> azure-arm: Setting hello certificate’s URL ...
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.55.35’
==> azure-arm: Waiting for WinRM toobecome available...
==> azure-arm: Connected tooWinRM!
==> azure-arm: Provisioning with Powershell...
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-powershell-provisioner902510110
    azure-arm: #< CLIXML
    azure-arm:
    azure-arm: Success Restart Needed Exit Code      Feature Result
    azure-arm: ------- -------------- ---------      --------------
    azure-arm: True    No             Success        {Common HTTP Features, Default Document, D...
    azure-arm: <Objs Version=“1.1.0.1” xmlns=“http://schemas.microsoft.com/powershell/2004/04"><Obj S=“progress” RefId=“0"><TN RefId=“0”><T>System.Management.Automation.PSCustomObject</T><T>System.Object</T></TN><MS><I64 N=“SourceId”>1</I64><PR N=“Record”><AV>Preparing modules for first use.</AV><AI>0</AI><Nil /><PI>-1</PI><PC>-1</PC><T>Completed</T><SR>-1</SR><SD> </SD></PR></MS></Obj></Objs>
==> azure-arm: Querying hello machine’s properties ...
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
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```

Hello 배포를 정리 하 고 hello provisioners 실행 Packer toobuild hello VM에 대 한 몇 가지 분 걸립니다.


## <a name="create-vm-from-azure-image"></a>Azure 이미지에서 VM 만들기
된 hello Vm에 대 한 관리자 사용자 이름 및 암호 설정 [Get-credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential)합니다.

```powershell
$cred = Get-Credential
```

이제 [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)을 사용하여 이미지에서 VM을 만들 수 있습니다. hello 다음 예제에서는 V *myVM* 에서 *myPackerImage*합니다.

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

# Define hello image created by Packer
$image = Get-AzureRMImage -ImageName myPackerImage -ResourceGroupName $rgName

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -Id $image.Id | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```

몇 분 toocreate hello VM이 필요합니다.


## <a name="test-vm-and-iis"></a>VM 및 IIS 테스트
Hello를 사용 하 여 VM의 공용 IP 주소 가져오기 [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)합니다. hello 다음 예제에서는 가져옵니다 hello IP 주소를 *myPublicIP* 앞에서 만든:

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName $rgName `
    -Name "myPublicIP" | select "IpAddress"
```

그런 다음 tooa 웹 브라우저에서 hello 공용 IP 주소를 입력할 수 있습니다.

![IIS 기본 사이트](./media/build-image-with-packer/iis.png) 


## <a name="next-steps"></a>다음 단계
이 예제에서는 IIS가 이미 설치 된 Packer toocreate VM 이미지를 사용 합니다. 이 VM 이미지 toodeploy 앱 tooVMs hello Team Services, Ansible, Chef 또는 Puppet를 사용 하 여 이미지에서에서 만든 같은 기존 배포 워크플로 함께 사용할 수 있습니다.

다른 Windows 배포판에 대한 추가 예제 Packer 템플릿은 [이 GitHub 리포지토리](https://github.com/hashicorp/packer/tree/master/examples/azure)를 참조하세요.