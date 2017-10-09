---
title: "일반화 된 VHD tooAzure PowerShell 스크립트 샘플 aaaUpload | Microsoft Docs"
description: "PowerShell은 스크립트 tooupload 일반화 된 VHD tooAzure 샘플 및 hello 리소스 관리자 배포 모델 및 관리 하는 디스크를 사용 하 여 새 VM을 만듭니다."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/18/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 72b4ff09eb7a6ba1604b9d5cbac51e60eded7545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-script-tooupload-a-vhd-tooazure-and-create-a-new-vm"></a>새 vm 및 VHD tooAzure 스크립트 tooupload 샘플

이 스크립트는 일반화 된 VM에서 로컬.vhd 파일을 가져와 및 tooAzure 업로드, 관리 되는 디스크 이미지를 만들고 hello toocreate 새 VM을 사용 하 여 합니다.

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트

```powershell
# Provide values for hello variables
$resourceGroup = 'myResourceGroup'
$location = 'EastUS'
$storageaccount = 'mystorageaccount'
$storageType = 'Standard_LRS'
$containername = 'mycontainer'
$localPath = 'C:\Users\Public\Documents\Hyper-V\VHDs\generalized.vhd'
$vmName = 'myVM'
$imageName = 'myImage'
$vhdName = 'myUploadedVhd.vhd'
$diskSizeGB = '128'
$subnetName = 'mySubnet'
$vnetName = 'myVnet'
$ipName = 'myPip'
$nicName = 'myNic'
$nsgName = 'myNsg'
$ruleName = 'myRdpRule'
$vmName = 'myVM'
$computerName = 'myComputerName'
$vmSize = 'Standard_DS1_v2'

# Get hello username and password toobe used for hello administrators account on hello VM. 
# This is used when connecting toohello VM using RDP.

$cred = Get-Credential

# Upload hello VHD
New-AzureRmResourceGroup -Name $resourceGroup -Location $location
New-AzureRmStorageAccount -ResourceGroupName $resourceGroup -Name $storageAccount -Location $location `
    -SkuName $storageType -Kind "Storage"
$urlOfUploadedImageVhd = ('https://' + $storageaccount + '.blob.core.windows.net/' + $containername + '/' + $vhdName)
Add-AzureRmVhd -ResourceGroupName $resourceGroup -Destination $urlOfUploadedImageVhd `
    -LocalFilePath $localPath

# Note: Uploading hello VHD may take awhile!

# Create a managed image from hello uploaded VHD 
$imageConfig = New-AzureRmImageConfig -Location $location
$imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized `
    -BlobUri $urlOfUploadedImageVhd
$image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $resourceGroup -Image $imageConfig
 
# Create hello networking resources
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $resourceGroup -Location $location `
    -AllocationMethod Dynamic
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $resourceGroup -Location $location `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description 'Allow RDP' -Access Allow `
    -Protocol Tcp -Direction Inbound -Priority 110 -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $resourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $resourceGroup -Name $vnetName

# Start building hello VM configuration
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

# Set hello VM image as source image for hello new VM
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id

# Finish hello VM configuration and add hello NIC.
$vm = Set-AzureRmVMOSDisk -VM $vm  -DiskSizeInGB $diskSizeGB -CreateOption FromImage -Caching ReadWrite
$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

# Create hello VM
New-AzureRmVM -VM $vm -ResourceGroupName $resourceGroup -Location $location

# Verify that hello VM was created
$vmList = Get-AzureRmVM -ResourceGroupName $resourceGroup
$vmList.Name


```


<!-- 
[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-iis/create-windows-vm-iis.ps1 "Create VM IIS")] -->

## <a name="clean-up-deployment"></a>배포 정리 

Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.

```powershell
Remove-AzureRmResourceGroup -Name $resourceGroup
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 toocreate hello 배포한 후에 hello를 사용 합니다. Hello 테이블의 각 항목 toocommand 특정 문서를 연결합니다.

| 명령                                                                                                             | 참고 사항                                                                                                                                                                                |
|---------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)                           | 모든 리소스가 저장되는 리소스 그룹을 만듭니다.                                                                                                                          |
| [New-AzureRmStorageAccount](/powershell/module/azurerm.resources/new-azurermstorageaccount)                         | 저장소 계정을 만듭니다.                                                                                                                                                           |
| [Add-AzureRmVhd](/powershell/module/azurerm.resources/add-azurermvhd)                                               | Azure의 클라우드 저장소 계정에는 온-프레미스 가상 컴퓨터 tooa blob에서 가상 하드 디스크를 업로드합니다.                                                                       |
| [New-AzureRmImageConfig](/powershell/module/azurerm.resources/new-azurermimageconfig)                               | 구성 가능한 이미지 개체를 만듭니다.                                                                                                                                                 |
| [Set-AzureRmImageOsDisk](/powershell/module/azurerm.resources/set-azurermimageosdisk)                               | Image 개체에 hello 운영 체제 디스크 속성을 설정합니다.                                                                                                                        |
| [New-AzureRmImage](/powershell/module/azurerm.resources/new-azurermimage)                                           | 새 이미지를 만듭니다.                                                                                                                                                                 |
| [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.resources/new-azurermvirtualnetworksubnetconfig) | 서브넷 구성을 만듭니다. 이 구성은 hello 가상 네트워크 만들기 프로세스에 사용 됩니다.                                                                                |
| [새-AzureRmVirtualNetwork](/powershell/module/azurerm.resources/new-azurermvirtualnetwork)                         | 가상 네트워크를 만듭니다.                                                                                                                                                           |
| [New-AzureRmPublicIpAddress](/powershell/module/azurerm.resources/new-azurermpublicipaddress)                       | 공용 IP 주소를 만듭니다.                                                                                                                                                         |
| [새-AzureRmNetworkInterface](/powershell/module/azurerm.resources/new-azurermnetworkinterface)                     | 네트워크 인터페이스를 만듭니다.                                                                                                                                                         |
| [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermnetworksecurityruleconfig)   | 네트워크 보안 그룹 규칙 구성을 만듭니다. 이 구성은 hello NSG를 만들 때 사용 되는 toocreate NSG 규칙입니다.                                                       |
| [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.resources/new-azurermnetworksecuritygroup)             | 네트워크 보안 그룹을 만듭니다.                                                                                                                                                    |
| [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.resources/get-azurermvirtualnetwork)                         | 리소스 그룹의 가상 네트워크를 가져옵니다.                                                                                                                                          |
| [New-AzureRmVMConfig](/powershell/module/azurerm.resources/new-azurermvmconfig)                                     | VM 구성을 만듭니다. 이 구성은 VM 이름, 운영 체제 및 관리자 자격 증명 등의 정보를 포함합니다. hello 구성은 VM 만드는 동안 사용 됩니다. |
| [Set-AzureRmVMSourceImage](/powershell/module/azurerm.resources/set-azurermvmsourceimage)                           | 가상 컴퓨터에 대한 이미지를 지정합니다.                                                                                                                                            |
| [Set-AzureRmVMOSDisk](/powershell/module/azurerm.resources/set-azurermvmosdisk)                                     | 가상 컴퓨터에서 hello 운영 체제 디스크 속성을 설정합니다.                                                                                                                      |
| [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.resources/set-azurermvmoperatingsystem)                   | 가상 컴퓨터에서 hello 운영 체제 디스크 속성을 설정합니다.                                                                                                                      |
| [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.resources/add-azurermvmnetworkinterface)                 | 네트워크 인터페이스 tooa 가상 컴퓨터를 추가합니다.                                                                                                                                       |
| [New-AzureRmVM](/powershell/module/azurerm.resources/new-azurermvm)                                                 | 가상 컴퓨터를 만듭니다.                                                                                                                                                            |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup)                     | 리소스 그룹 및 포함된 모든 리소스를 제거합니다.                                                                                                                         |

## <a name="next-steps"></a>다음 단계

Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.

가상 컴퓨터가 추가 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Windows VM 설명서](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
