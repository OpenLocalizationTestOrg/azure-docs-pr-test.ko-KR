---
title: "Window Server 및 Windows 클라이언트에 대한 Azure 하이브리드 사용 혜택 | Microsoft Docs"
description: "Azure에 온-프레미스 라이선스를 가져오기 위해 Windows Software Assurance 혜택을 최대화하는 방법에 대해 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: kmouss
manager: timlt
editor: 
ms.assetid: 332583b6-15a3-4efb-80c3-9082587828b0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 5/26/2017
ms.author: xujing
ms.openlocfilehash: 210635624946ddb293427167e9d476c377bcc9b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-hybrid-use-benefit-for-windows-server-and-windows-client"></a><span data-ttu-id="74b09-103">Window Server 및 Windows 클라이언트에 대한 Azure 하이브리드 사용 혜택</span><span class="sxs-lookup"><span data-stu-id="74b09-103">Azure Hybrid Use Benefit for Windows Server and Windows Client</span></span>
<span data-ttu-id="74b09-104">Software Assurance 고객은 Azure 하이브리드 사용 혜택을 통해 온-프레미스 Windows Server 및 Windows 클라이언트 라이선스를 사용하고 Azure에서 Windows 가상 컴퓨터를 실행하여 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-104">For customers with Software Assurance, Azure Hybrid Use Benefit allows you to use your on-premises Windows Server and Windows Client licenses and run Windows virtual machines in Azure at a reduced cost.</span></span> <span data-ttu-id="74b09-105">Windows Server에 대한 Azure 하이브리드 사용 혜택에는 Windows Server 2008R2, Windows Server 2012, Windows Server 2012R2 및 Windows Server 2016이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-105">Azure Hybrid Use Benefit for Windows Server includes Windows Server 2008R2, Windows Server 2012, Windows Server 2012R2, and Windows Server 2016.</span></span> <span data-ttu-id="74b09-106">Windows 클라이언트에 대한 Azure 하이브리드 사용 혜택에는 Windows 10이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-106">Azure Hybrid Use Benefit for Windows Client includes Windows 10.</span></span> <span data-ttu-id="74b09-107">자세한 내용은 [Azure 하이브리드 사용 혜택 라이선싱 페이지](https://azure.microsoft.com/pricing/hybrid-use-benefit/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="74b09-107">For more information, please see the [Azure Hybrid Use Benefit licensing page](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span></span>

>[!IMPORTANT]
><span data-ttu-id="74b09-108">Windows 클라이언트에 대한 Azure 하이브리드 사용 혜택은 현재 Azure Marketplace의 Windows 10 이미지를 사용하여 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-108">Azure Hybrid Use Benefits for Windows Client is currently in Preview using the Windows 10 image in the Azure Marketplace.</span></span> <span data-ttu-id="74b09-109">사용자별 Windows 10 Enterprise E3/E5 또는 사용자별 Windows VDA(사용자 구독 라이선스 또는 추가 기능 사용자 구독 라이선스)를 보유한 엔터프라이즈 고객("적격 라이선스")만 혜택을 누릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-109">Only Enterprise customers with Windows 10 Enterprise E3/E5 per user or Windows VDA per user (User Subscription Licenses or Add-on User Subscription Licenses) (“Qualifying Licenses”) are eligible.</span></span>
>
>

## <a name="ways-to-use-azure-hybrid-use-benefit"></a><span data-ttu-id="74b09-110">Azure 하이브리드 사용 혜택을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="74b09-110">Ways to use Azure Hybrid Use Benefit</span></span>
<span data-ttu-id="74b09-111">Azure 하이브리드 사용 혜택을 사용하여 Windows VM을 배포하는 몇 가지 다른 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-111">There are a couple of different ways to deploy Windows VMs with the Azure Hybrid Use Benefit:</span></span>

1. <span data-ttu-id="74b09-112">Azure 하이브리드 사용 혜택을 이용하여 미리 구성된 [특정 Marketplace 이미지](#deploy-a-vm-using-the-azure-marketplace)(Windows Server 2016, Windows Server 2012R2, Windows Server 2012 및 Windows Server 2008SP1)에서 VM을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-112">You can deploy VMs from [specific Marketplace images](#deploy-a-vm-using-the-azure-marketplace) that are pre-configured with Azure Hybrid Use Benefit - Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span></span>
2. <span data-ttu-id="74b09-113">[사용자 지정 VM을 업로드](#upload-a-windows-vhd)하거나 [Resource Manager 템플릿](#deploy-a-vm-via-resource-manager) 또는 [Azure PowerShell을 사용하여 배포](#detailed-powershell-deployment-walkthrough)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-113">You can [upload a custom VM](#upload-a-windows-vhd) and [deploy using a Resource Manager template](#deploy-a-vm-via-resource-manager) or [Azure PowerShell](#detailed-powershell-deployment-walkthrough).</span></span>

## <a name="deploy-a-vm-using-the-azure-marketplace"></a><span data-ttu-id="74b09-114">Azure Marketplace를 사용하여 VM 배포</span><span class="sxs-lookup"><span data-stu-id="74b09-114">Deploy a VM using the Azure Marketplace</span></span>
<span data-ttu-id="74b09-115">Windows Server 2016, Windows Server 2012R2, Windows Server 2012 및 Windows Server 2008SP1 이미지는 Azure 하이브리드 사용 혜택을 이용하여 미리 구성된 Marketplace에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-115">Following images are available in the Marketplace pre-configured with Azure Hybrid Use Benefit: Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span></span> <span data-ttu-id="74b09-116">이러한 이미지는 Azure Portal, Resource Manager 템플릿 또는 Azure PowerShell에서 직접 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-116">These images can be deployed directly from the Azure portal, Resource Manager templates, or Azure PowerShell.</span></span>

<span data-ttu-id="74b09-117">Azure Portal에서 직접 이러한 이미지를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-117">You can deploy these images directly from the Azure portal.</span></span> <span data-ttu-id="74b09-118">Resource Manager 템플릿 및 Azure PowerShell에서 사용하려면 다음과 같은 이미지 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-118">For use in Resource Manager templates and with Azure PowerShell, view the list of images as follows:</span></span>

<span data-ttu-id="74b09-119">Windows Server:</span><span class="sxs-lookup"><span data-stu-id="74b09-119">For Windows Server:</span></span>
```powershell
Get-AzureRmVMImagesku -Location westus -PublisherName MicrosoftWindowsServer -Offer WindowsServer
```
- <span data-ttu-id="74b09-120">2016-Datacenter 버전 2016.127.20170406 이상</span><span class="sxs-lookup"><span data-stu-id="74b09-120">2016-Datacenter version 2016.127.20170406 or above</span></span>

- <span data-ttu-id="74b09-121">2012-R2-Datacenter 버전 4.127.20170406 이상</span><span class="sxs-lookup"><span data-stu-id="74b09-121">2012-R2-Datacenter version 4.127.20170406 or above</span></span>

- <span data-ttu-id="74b09-122">2012-Datacenter 버전 3.127.20170406 이상</span><span class="sxs-lookup"><span data-stu-id="74b09-122">2012-Datacenter version 3.127.20170406 or above</span></span>

- <span data-ttu-id="74b09-123">2008-R2-SP1 버전 2.127.20170406 이상</span><span class="sxs-lookup"><span data-stu-id="74b09-123">2008-R2-SP1 version 2.127.20170406 or above</span></span>

<span data-ttu-id="74b09-124">Windows 클라이언트:</span><span class="sxs-lookup"><span data-stu-id="74b09-124">For Windows Client:</span></span>
```powershell
Get-AzureRMVMImageSku -Location "West US" -Publisher "MicrosoftWindowsServer" `
    -Offer "Windows-HUB"
```

## <a name="upload-a-windows-server-vhd"></a><span data-ttu-id="74b09-125">Windows Server VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="74b09-125">Upload a Windows Server VHD</span></span>
<span data-ttu-id="74b09-126">Azure에서 Windows Server VM을 배포하려면 먼저 기본 Windows 빌드를 포함하는 VHD를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-126">To deploy a Windows Server VM in Azure, you first need to create a VHD that contains your base Windows build.</span></span> <span data-ttu-id="74b09-127">이 VHD는 Azure에 업로드하기 전에 Sysprep을 통해 적절하게 준비되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-127">This VHD must be appropriately prepared via Sysprep before you upload it to Azure.</span></span> <span data-ttu-id="74b09-128">자세한 내용은 [VHD 요구 사항 및 Sysprep 프로세스](upload-generalized-managed.md) 및 [서버 역할에 대한 Sysprep 지원](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="74b09-128">You can [read more about the VHD requirements and Sysprep process](upload-generalized-managed.md) and [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span> <span data-ttu-id="74b09-129">Sysprep를 실행하기 전에 VM을 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-129">Back up the VM before running Sysprep.</span></span> 

<span data-ttu-id="74b09-130">먼저 [최신 Azure PowerShell을 설치 및 구성](/powershell/azure/overview)했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-130">Make sure you have [installed and configured the latest Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="74b09-131">VHD를 준비했으면 다음과 같이 `Add-AzureRmVhd` cmdlet을 사용하여 Azure 저장소 계정에 VHD를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-131">Once you have prepared your VHD, upload the VHD to your Azure Storage account using the `Add-AzureRmVhd` cmdlet as follows:</span></span>

```powershell
Add-AzureRmVhd -ResourceGroupName "myResourceGroup" -LocalFilePath "C:\Path\To\myvhd.vhd" `
    -Destination "https://mystorageaccount.blob.core.windows.net/vhds/myvhd.vhd"
```

> [!NOTE]
> <span data-ttu-id="74b09-132">Microsoft SQL Server, SharePoint 서버 및 Dynamics는 또한 Software Assurance 라이선스를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-132">Microsoft SQL Server, SharePoint Server, and Dynamics can also utilize your Software Assurance licensing.</span></span> <span data-ttu-id="74b09-133">Windows Server 이미지를 준비하려면 응용 프로그램 구성 요소를 설치하고 라이선스 키를 적절하게 제공한 다음, 디스크 이미지를 Azure에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-133">You still need to prepare the Windows Server image by installing your application components and providing license keys accordingly, then uploading the disk image to Azure.</span></span> <span data-ttu-id="74b09-134">응용 프로그램과 함께 [Sysprep를 사용하여 SQL Server 설치에 대한 고려 사항](https://msdn.microsoft.com/library/ee210754.aspx) 또는 [SharePoint Server 2016 참조 이미지 빌드(Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx)와 같은 Sysprep 실행에 대한 적합한 설명서를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-134">Review the appropriate documentation for running Sysprep with your application, such as [Considerations for Installing SQL Server using Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) or [Build a SharePoint Server 2016 Reference Image (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).</span></span>
>
>

<span data-ttu-id="74b09-135">자세한 내용은 [Azure에 VHD 업로드 프로세스](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="74b09-135">You can also read more about [uploading the VHD to Azure process](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)</span></span>


## <a name="deploy-a-vm-via-resource-manager-template"></a><span data-ttu-id="74b09-136">Resource Manager 템플릿을 통해 VM 배포</span><span class="sxs-lookup"><span data-stu-id="74b09-136">Deploy a VM via Resource Manager Template</span></span>
<span data-ttu-id="74b09-137">Resource Manager 템플릿 내에서 `licenseType` 에 대한 추가 매개 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-137">Within your Resource Manager templates, an additional parameter for `licenseType` can be specified.</span></span> <span data-ttu-id="74b09-138">[Azure Resource Manager 템플릿 작성](../../resource-group-authoring-templates.md)에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-138">You can read more about [authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="74b09-139">Azure에 VHD를 업로드하고 나면 Resource Manager 템플릿을 편집하여 계산 공급자의 일부로 라이선스 유형을 포함하고 정상적으로 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-139">Once you have your VHD uploaded to Azure, edit you Resource Manager template to include the license type as part of the compute provider and deploy your template as normal:</span></span>

<span data-ttu-id="74b09-140">Windows Server:</span><span class="sxs-lookup"><span data-stu-id="74b09-140">For Windows Server:</span></span>
```json
"properties": {  
   "licenseType": "Windows_Server",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

<span data-ttu-id="74b09-141">Windows 클라이언트를 Azure Marketplace 이미지에만 사용하려면:</span><span class="sxs-lookup"><span data-stu-id="74b09-141">For Windows Client to use with Azure Marketplace Image only:</span></span>
```json
"properties": {  
   "licenseType": "Windows_Client",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

## <a name="deploy-a-vm-via-powershell-quickstart"></a><span data-ttu-id="74b09-142">PowerShell 빠른 시작을 통해 VM 배포</span><span class="sxs-lookup"><span data-stu-id="74b09-142">Deploy a VM via PowerShell quickstart</span></span>
<span data-ttu-id="74b09-143">PowerShell을 통해 Windows Server VM을 배포할 때는 `-LicenseType`에 대한 추가 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-143">When deploying your Windows Server VM via PowerShell, you have an additional parameter for `-LicenseType`.</span></span> <span data-ttu-id="74b09-144">Azure에 VHD를 업로드하고 나면 다음과 같이 `New-AzureRmVM`을 사용하여 VM을 만들고 라이선싱 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-144">Once you have your VHD uploaded to Azure, you create a VM using `New-AzureRmVM` and specify the licensing type as follows:</span></span>

<span data-ttu-id="74b09-145">Windows Server:</span><span class="sxs-lookup"><span data-stu-id="74b09-145">For Windows Server:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Server"
```

<span data-ttu-id="74b09-146">Windows 클라이언트를 Azure Marketplace 이미지에만 사용하려면:</span><span class="sxs-lookup"><span data-stu-id="74b09-146">For Windows Client to use with Azure Marketplace Image only:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Client"
```

<span data-ttu-id="74b09-147">아래에서 [PowerShell을 통해 Azure에서 VM을 배포하는 보다 자세한 연습을 확인](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough)하거나, [Resource Manager 및 PowerShell을 사용하여 Windows VM 만들기](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 수행하는 다른 단계에 대해 보다 자세히 설명하는 더 자세한 지침을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="74b09-147">You can [read a more detailed walkthrough on deploying a VM in Azure via PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) below, or read a more descriptive guide on the different steps to [create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="verify-your-vm-is-utilizing-the-licensing-benefit"></a><span data-ttu-id="74b09-148">VM이 라이선싱 혜택을 사용하고 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="74b09-148">Verify your VM is utilizing the licensing benefit</span></span>
<span data-ttu-id="74b09-149">PowerShell 또는 Resource Manager 배포 메서드를 통해 VM을 배포한 후 다음과 같이 `Get-AzureRmVM` 을 사용하여 라이선스 형식을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-149">Once you have deployed your VM through either the PowerShell or Resource Manager deployment method, verify the license type with `Get-AzureRmVM` as follows:</span></span>

```powershell
Get-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="74b09-150">Windows Server의 경우 다음 예제와 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-150">The output is similar to the following example for Windows Server:</span></span>

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              : Windows_Server
```

<span data-ttu-id="74b09-151">이 출력은 Azure 갤러리에서 바로 배포된 VM과 같이 Azure 하이브리드 사용 혜택 라이선싱 없이 배포된 다음 VM과는 대조됩니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-151">This output contrasts with the following VM deployed without Azure Hybrid Use Benefit licensing, such as a VM deployed straight from the Azure Gallery:</span></span>

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              :
```

## <a name="detailed-powershell-deployment-walkthrough"></a><span data-ttu-id="74b09-152">자세한 PowerShell 배포 연습</span><span class="sxs-lookup"><span data-stu-id="74b09-152">Detailed PowerShell deployment walkthrough</span></span>
<span data-ttu-id="74b09-153">다음 자세한 PowerShell 단계는 VM의 전체 배포를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-153">The following detailed PowerShell steps show a full deployment of a VM.</span></span> <span data-ttu-id="74b09-154">[Resource Manager 및 PowerShell을 사용하여 Windows VM 만들기](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 만든 실제 cmdlet 및 다른 구성 요소에 대해 자세한 컨텍스트를 읽어볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-154">You can read more context as to the actual cmdlets and different components being created in [Create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="74b09-155">단계별로 리소스 그룹, 저장소 계정 및 가상 네트워킹을 만든 다음 VM을 정의하고 마지막으로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-155">You step through creating your resource group, storage account, and virtual networking, then define your VM and finally create your VM.</span></span>

<span data-ttu-id="74b09-156">먼저 안전하게 자격 증명을 얻고, 위치를 설정하고, 리소스 그룹 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-156">First, securely obtain credentials, set a location, and resource group name:</span></span>

```powershell
$cred = Get-Credential
$location = "West US"
$resourceGroupName = "myResourceGroup"
```

<span data-ttu-id="74b09-157">공용 IP 만들기:</span><span class="sxs-lookup"><span data-stu-id="74b09-157">Create a public IP:</span></span>

```powershell
$publicIPName = "myPublicIP"
$publicIP = New-AzureRmPublicIpAddress -Name $publicIPName -ResourceGroupName $resourceGroupName `
    -Location $location -AllocationMethod "Dynamic"
```

<span data-ttu-id="74b09-158">서브넷, NIC 및 VNET을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-158">Define your subnet, NIC, and VNET:</span></span>

```powershell
$subnetName = "mySubnet"
$nicName = "myNIC"
$vnetName = "myVnet"
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/8
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location `
    -AddressPrefix 10.0.0.0/8 -Subnet $subnetconfig
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $resourceGroupName -Location $location `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $publicIP.Id
```

<span data-ttu-id="74b09-159">VM 이름을 지정하고 VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-159">Name your VM and create a VM config:</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A1"
```

<span data-ttu-id="74b09-160">OS 정의:</span><span class="sxs-lookup"><span data-stu-id="74b09-160">Define your OS:</span></span>

```powershell
$computerName = "myVM"
$vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="74b09-161">VM에 NIC를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-161">Add your NIC to the VM:</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="74b09-162">사용할 저장소 계정 정의:</span><span class="sxs-lookup"><span data-stu-id="74b09-162">Define the storage account to use:</span></span>

```powershell
$storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -AccountName mystorageaccount
```

<span data-ttu-id="74b09-163">VHD를 업로드하고, 적절하게 준비하고, 사용을 위해 VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-163">Upload your VHD, suitably prepared, and attach to your VM for use:</span></span>

```powershell
$osDiskName = "licensing.vhd"
$osDiskUri = '{0}vhds/{1}{2}.vhd' -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/vhd/myvhd.vhd"
$vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption FromImage `
    -SourceImageUri $urlOfUploadedImageVhd -Windows
```

<span data-ttu-id="74b09-164">마지막으로, VM을 만들고 Azure 하이브리드 사용 혜택을 사용하기 위한 라이선싱 유형을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-164">Finally, create your VM and define the licensing type to utilize Azure Hybrid Use Benefit:</span></span>

<span data-ttu-id="74b09-165">Windows Server:</span><span class="sxs-lookup"><span data-stu-id="74b09-165">For Windows Server:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName $resourceGroupName -Location $location -VM $vm -LicenseType "Windows_Server"
```

## <a name="deploy-a-virtual-machine-scale-set-via-resource-manager-template"></a><span data-ttu-id="74b09-166">Resource Manager 템플릿을 사용하여 가상 컴퓨터 크기 집합 배포</span><span class="sxs-lookup"><span data-stu-id="74b09-166">Deploy a virtual machine scale set via Resource Manager template</span></span>
<span data-ttu-id="74b09-167">VMSS Resource Manager 템플릿 내에서 `licenseType` 에 대한 추가 매개 변수를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-167">Within your VMSS Resource Manager templates, an additional parameter for `licenseType` must be specified.</span></span> <span data-ttu-id="74b09-168">[Azure Resource Manager 템플릿 작성](../../resource-group-authoring-templates.md)에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-168">You can read more about [authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="74b09-169">크기 집합 virtualMachineProfile의 일부로 licenseType 속성을 포함하고 일반적인 방법으로 템플릿을 배포하도록 Resource Manager 템플릿을 편집합니다. 2016 Windows Server 이미지를 사용하는 아래 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="74b09-169">Edit your Resource Manager template to include the licenseType property as part of the scale set’s virtualMachineProfile and deploy your template as normal - see example below using 2016 Windows Server image:</span></span>


```json
"virtualMachineProfile": {
    "storageProfile": {
        "osDisk": {
            "createOption": "FromImage"
        },
        "imageReference": {
            "publisher": "MicrosoftWindowsServer",
            "offer": "WindowsServer",
            "sku": "2016-Datacenter",
            "version": "latest"
        }
    },
    "licenseType": "Windows_Server",
    "osProfile": {
            "computerNamePrefix": "[parameters('vmssName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
    }
```

> [!NOTE]
> <span data-ttu-id="74b09-170">PowerShell 및 다른 SDK 도구를 통해 AHUB 기능을 활용하여 가상 컴퓨터 크기 집합을 배포하는 방식은 곧 지원될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-170">Support for deploying a virtual machine scale set with AHUB benefits through PowerShell and other SDK tools is coming soon.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="74b09-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="74b09-171">Next steps</span></span>
<span data-ttu-id="74b09-172">자세한 내용은 [Azure 하이브리드 사용 혜택 라이선싱](https://azure.microsoft.com/pricing/hybrid-use-benefit/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="74b09-172">Read more about [Azure Hybrid Use Benefit licensing](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span></span>

<span data-ttu-id="74b09-173">[Resource Manager 템플릿 사용](../../azure-resource-manager/resource-group-overview.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="74b09-173">Learn more about [using Resource Manager templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="74b09-174">[Azure 하이브리드 사용 혜택 및 Azure Site Recovery를 사용하여 응용 프로그램을 Azure로 훨씬 간편하게 마이그레이션하는 방법](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="74b09-174">Learn more about [Azure Hybrid Use Benefit and Azure Site Recovery make migrating applications to Azure even more cost-effective](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).</span></span>
