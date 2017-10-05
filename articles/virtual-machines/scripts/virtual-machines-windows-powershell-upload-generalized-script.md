---
title: "일반화된 VHD를 Azure PowerShell 스크립트 샘플에 업로드 | Microsoft Docs"
description: "리소스 관리자 배포 모델과 Managed Disks를 사용하여 Azure에 일반화된 VHD를 업로드하고 새 VM을 만드는 PowerShell 샘플 스크립트입니다."
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
ms.openlocfilehash: cd3d87bb4384971e28d3330cd5c1a3d351129036
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="sample-script-to-upload-a-vhd-to-azure-and-create-a-new-vm"></a><span data-ttu-id="98aca-103">Azure에 VHD를 업로드하고 새 VM을 만드는 샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="98aca-103">Sample script to upload a VHD to Azure and create a new VM</span></span>

<span data-ttu-id="98aca-104">이 스크립트는 일반화된 VM에서 로컬 .vhd 파일을 가져와서 Azure에 업로드하고, Managed Disk 이미지를 만들고, 새 VM을 만드는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-104">This script takes a local .vhd file from a generalized VM and uploads it to Azure, creates a Managed Disk image and uses the to create a new VM.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="98aca-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="98aca-105">Sample script</span></span>

```powershell
# Provide values for the variables
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

# Get the username and password to be used for the administrators account on the VM. 
# This is used when connecting to the VM using RDP.

$cred = Get-Credential

# Upload the VHD
New-AzureRmResourceGroup -Name $resourceGroup -Location $location
New-AzureRmStorageAccount -ResourceGroupName $resourceGroup -Name $storageAccount -Location $location `
    -SkuName $storageType -Kind "Storage"
$urlOfUploadedImageVhd = ('https://' + $storageaccount + '.blob.core.windows.net/' + $containername + '/' + $vhdName)
Add-AzureRmVhd -ResourceGroupName $resourceGroup -Destination $urlOfUploadedImageVhd `
    -LocalFilePath $localPath

# Note: Uploading the VHD may take awhile!

# Create a managed image from the uploaded VHD 
$imageConfig = New-AzureRmImageConfig -Location $location
$imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized `
    -BlobUri $urlOfUploadedImageVhd
$image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $resourceGroup -Image $imageConfig
 
# Create the networking resources
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

# Start building the VM configuration
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

# Set the VM image as source image for the new VM
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id

# Finish the VM configuration and add the NIC.
$vm = Set-AzureRmVMOSDisk -VM $vm  -DiskSizeInGB $diskSizeGB -CreateOption FromImage -Caching ReadWrite
$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

# Create the VM
New-AzureRmVM -VM $vm -ResourceGroupName $resourceGroup -Location $location

# Verify that the VM was created
$vmList = Get-AzureRmVM -ResourceGroupName $resourceGroup
$vmList.Name


```


<!-- 
[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-iis/create-windows-vm-iis.ps1 "Create VM IIS")] -->

## <a name="clean-up-deployment"></a><span data-ttu-id="98aca-106">배포 정리</span><span class="sxs-lookup"><span data-stu-id="98aca-106">Clean up deployment</span></span> 

<span data-ttu-id="98aca-107">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-107">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $resourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="98aca-108">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="98aca-108">Script explanation</span></span>

<span data-ttu-id="98aca-109">이 스크립트는 다음 명령을 사용하여 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-109">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="98aca-110">테이블에 있는 각 항목은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-110">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="98aca-111">명령</span><span class="sxs-lookup"><span data-stu-id="98aca-111">Command</span></span>                                                                                                             | <span data-ttu-id="98aca-112">참고 사항</span><span class="sxs-lookup"><span data-stu-id="98aca-112">Notes</span></span>                                                                                                                                                                                |
|---------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="98aca-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="98aca-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)                           | <span data-ttu-id="98aca-114">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-114">Creates a resource group in which all resources are stored.</span></span>                                                                                                                          |
| [<span data-ttu-id="98aca-115">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="98aca-115">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.resources/new-azurermstorageaccount)                         | <span data-ttu-id="98aca-116">저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-116">Creates a storage account.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="98aca-117">Add-AzureRmVhd</span><span class="sxs-lookup"><span data-stu-id="98aca-117">Add-AzureRmVhd</span></span>](/powershell/module/azurerm.resources/add-azurermvhd)                                               | <span data-ttu-id="98aca-118">온-프레미스 가상 컴퓨터에서 Azure의 클라우드 저장소 계정에 있는 blob으로 가상 하드 디스크를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-118">Uploads a virtual hard disk from an on-premises virtual machine to a blob in a cloud storage account in Azure.</span></span>                                                                       |
| [<span data-ttu-id="98aca-119">New-AzureRmImageConfig</span><span class="sxs-lookup"><span data-stu-id="98aca-119">New-AzureRmImageConfig</span></span>](/powershell/module/azurerm.resources/new-azurermimageconfig)                               | <span data-ttu-id="98aca-120">구성 가능한 이미지 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-120">Creates a configurable image object.</span></span>                                                                                                                                                 |
| [<span data-ttu-id="98aca-121">Set-AzureRmImageOsDisk</span><span class="sxs-lookup"><span data-stu-id="98aca-121">Set-AzureRmImageOsDisk</span></span>](/powershell/module/azurerm.resources/set-azurermimageosdisk)                               | <span data-ttu-id="98aca-122">이미지 개체의 운영 체제 디스크 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-122">Sets the operating system disk properties on an image object.</span></span>                                                                                                                        |
| [<span data-ttu-id="98aca-123">New-AzureRmImage</span><span class="sxs-lookup"><span data-stu-id="98aca-123">New-AzureRmImage</span></span>](/powershell/module/azurerm.resources/new-azurermimage)                                           | <span data-ttu-id="98aca-124">새 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-124">Creates a new image.</span></span>                                                                                                                                                                 |
| [<span data-ttu-id="98aca-125">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="98aca-125">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="98aca-126">서브넷 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-126">Creates a subnet configuration.</span></span> <span data-ttu-id="98aca-127">이 구성은 가상 네트워크 만들기 프로세스에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-127">This configuration is used with the virtual network creation process.</span></span>                                                                                |
| [<span data-ttu-id="98aca-128">새-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="98aca-128">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetwork)                         | <span data-ttu-id="98aca-129">가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-129">Creates a virtual network.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="98aca-130">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="98aca-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.resources/new-azurermpublicipaddress)                       | <span data-ttu-id="98aca-131">공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-131">Creates a public IP address.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="98aca-132">새-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="98aca-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.resources/new-azurermnetworkinterface)                     | <span data-ttu-id="98aca-133">네트워크 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-133">Creates a network interface.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="98aca-134">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="98aca-134">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecurityruleconfig)   | <span data-ttu-id="98aca-135">네트워크 보안 그룹 규칙 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-135">Creates a network security group rule configuration.</span></span> <span data-ttu-id="98aca-136">이 구성은 NSG가 만들어질 때 NSG 규칙을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-136">This configuration is used to create an NSG rule when the NSG is created.</span></span>                                                       |
| [<span data-ttu-id="98aca-137">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="98aca-137">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecuritygroup)             | <span data-ttu-id="98aca-138">네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-138">Creates a network security group.</span></span>                                                                                                                                                    |
| [<span data-ttu-id="98aca-139">Get-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="98aca-139">Get-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/get-azurermvirtualnetwork)                         | <span data-ttu-id="98aca-140">리소스 그룹의 가상 네트워크를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-140">Gets a virtual network in a resource group.</span></span>                                                                                                                                          |
| [<span data-ttu-id="98aca-141">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="98aca-141">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvmconfig)                                     | <span data-ttu-id="98aca-142">VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-142">Creates a VM configuration.</span></span> <span data-ttu-id="98aca-143">이 구성은 VM 이름, 운영 체제 및 관리자 자격 증명 등의 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-143">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="98aca-144">이 구성은 VM을 만드는 중에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-144">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="98aca-145">Set-AzureRmVMSourceImage</span><span class="sxs-lookup"><span data-stu-id="98aca-145">Set-AzureRmVMSourceImage</span></span>](/powershell/module/azurerm.resources/set-azurermvmsourceimage)                           | <span data-ttu-id="98aca-146">가상 컴퓨터에 대한 이미지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-146">Specifies an image for a virtual machine.</span></span>                                                                                                                                            |
| [<span data-ttu-id="98aca-147">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="98aca-147">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.resources/set-azurermvmosdisk)                                     | <span data-ttu-id="98aca-148">가상 컴퓨터의 운영 체제 디스크 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-148">Sets the operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="98aca-149">Set-AzureRmVMOperatingSystem</span><span class="sxs-lookup"><span data-stu-id="98aca-149">Set-AzureRmVMOperatingSystem</span></span>](/powershell/module/azurerm.resources/set-azurermvmoperatingsystem)                   | <span data-ttu-id="98aca-150">가상 컴퓨터의 운영 체제 디스크 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-150">Sets the operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="98aca-151">Add-AzureRmVMNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="98aca-151">Add-AzureRmVMNetworkInterface</span></span>](/powershell/module/azurerm.resources/add-azurermvmnetworkinterface)                 | <span data-ttu-id="98aca-152">가상 컴퓨터에 네트워크 인터페이스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-152">Adds a network interface to a virtual machine.</span></span>                                                                                                                                       |
| [<span data-ttu-id="98aca-153">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="98aca-153">New-AzureRmVM</span></span>](/powershell/module/azurerm.resources/new-azurermvm)                                                 | <span data-ttu-id="98aca-154">가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-154">Create a virtual machine.</span></span>                                                                                                                                                            |
| [<span data-ttu-id="98aca-155">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="98aca-155">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)                     | <span data-ttu-id="98aca-156">리소스 그룹 및 포함된 모든 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-156">Removes a resource group and all resources contained within.</span></span>                                                                                                                         |

## <a name="next-steps"></a><span data-ttu-id="98aca-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="98aca-157">Next steps</span></span>

<span data-ttu-id="98aca-158">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98aca-158">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="98aca-159">추가 가상 컴퓨터 PowerShell 스크립트 샘플은 [Azure Windows VM 설명서](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98aca-159">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
